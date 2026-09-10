# TECH ARCHITECTURE — pre-code

> Статус: **утверждённый архитектурный план, код ещё не пишем**  
> Версия: 1.0  
> Движок: Godot 4 / Web export  
> Платформы первого релиза: Яндекс Игры + Пикабу Игры + локальный browser fallback.

Этот документ нужен, чтобы после завершения pre-production начать разработку без архитектурных импровизаций. Здесь нет реализации и исходного кода.

## 1. Главный архитектурный принцип

Игровая логика **не знает**, где запущена игра.

Она работает с абстрактными сервисами:

- сохранения;
- реклама;
- lifecycle/pause;
- авторизация/игрок;
- аналитические события;
- platform-ready/loading.

Конкретные SDK Яндекса и Пикабу находятся в отдельных адаптерах.

Это позволяет:

- запускать игру локально без SDK;
- собирать один игровой core;
- не размазывать JavaScriptBridge по сценам;
- тестировать сюжет отдельно от платформы;
- позже добавлять новую площадку без переписывания квестовой логики.

---

# 2. Высокоуровневые слои

```text
GAME CONTENT
сцены / персонажи / диалоги / puzzle data
        ↓
GAMEPLAY SERVICES
story state / investigation / inventory / notebook / map
        ↓
CORE SERVICES
save / audio / settings / scene transitions / lifecycle
        ↓
PLATFORM FACADE
player / cloud save / ads / ready / platform events
        ↓
ADAPTER
Local | Yandex | Pikabu
        ↓
JavaScript / SDK / backend where required
```

Ни один конкретный NPC или puzzle не должен напрямую вызывать SDK рекламы или облачного сохранения.

---

# 3. Планируемая структура проекта

```text
project/
├── scenes/
│   ├── boot/
│   ├── menu/
│   ├── ui/
│   ├── locations/
│   └── transitions/
├── scripts/
│   ├── core/
│   ├── story/
│   ├── interaction/
│   ├── ui/
│   ├── platform/
│   │   ├── adapters/
│   │   └── bridge/
│   └── debug/
├── data/
│   ├── story/
│   ├── dialogue/
│   ├── clues/
│   ├── puzzles/
│   ├── locations/
│   └── localization/
├── assets/
│   └── ...
└── web/
    ├── yandex/
    └── pikabu/
```

Точные имена файлов определяются уже в начале coding phase, но разделение слоёв сохраняется.

---

# 4. Boot flow

Порядок запуска:

1. загрузка минимального Godot/Web shell;
2. определение платформы;
3. инициализация соответствующего SDK adapter;
4. загрузка локальных настроек;
5. инициализация Player/Save service;
6. получение облачного прогресса, если доступен;
7. разрешение local/cloud state;
8. загрузка первого визуального экрана;
9. сообщение платформе о готовности;
10. показ главного меню;
11. `Продолжить дело` или `Новое дело`.

Ошибка SDK **не должна ломать запуск игры**, если требования площадки позволяют локальный fallback. Игра показывает понятное состояние и пытается продолжить с локальным прогрессом.

---

# 5. Story State

Сюжет не хранится как сотни случайных boolean-переменных в сценах.

Нужна единая модель состояния дела.

### Основные группы

#### Meta

- save schema version;
- content version;
- platform;
- timestamp;
- playtime;
- completed flag.

#### Progress

- current act;
- current stable scene/location;
- last checkpoint;
- unlocked locations;
- visited locations.

#### Investigation

- discovered clue IDs;
- confirmed fact IDs;
- active hypothesis IDs;
- disproved hypothesis IDs;
- notebook objective IDs;
- chronology entries.

#### Inventory

- active item IDs;
- consumed item IDs;
- evidence/document IDs stored in notebook.

#### Puzzles

- puzzle state by ID;
- hint level used;
- completion status.

#### Dialogue

Храним не номер каждой показанной строки, а устойчивые состояния:

- topic unlocked;
- topic exhausted;
- critical conversation completed;
- NPC phase/state.

#### Side tasks

- not_started;
- active;
- completed;
- optional outcome flags.

#### Settings

Настройки можно хранить отдельно от сюжетного save:

- music volume;
- sfx volume;
- text speed;
- typewriter enabled;
- large text;
- hotspot assist;
- reduced motion.

---

# 6. ID-first content model

Все сюжетные сущности получают стабильные ID.

Примеры:

- `scene_agency_morning`
- `location_boiler`
- `npc_gorynych`
- `clue_visitor_log`
- `fact_thursday_happened`
- `puzzle_photo_negatives`
- `item_luggage_receipt`
- `dialogue_kruglov_phase_2`

Save хранит ID, а не ссылки на Node или пути текущей сцены.

Это позволяет менять структуру scene tree без уничтожения сохранений.

---

# 7. Сцена и hotspot

Каждый фон — отдельная location scene либо подscene общего location-контейнера.

Hotspot описывает:

- ID;
- тип действия;
- interaction point;
- направление Сомова;
- условие доступности;
- реакцию до/после сюжетного факта;
- возможную выдачу clue/item;
- target для inventory item.

Сюжетная логика не должна быть зашита исключительно в визуальный Node. Hotspot обращается к Story/Interaction service, который решает актуальное состояние.

---

# 8. Диалоги как данные

Диалоги первой игры желательно хранить отдельно от GDScript.

Каждый dialogue node содержит:

- ID;
- speaker;
- text/localization key;
- portrait/emotion;
- условия;
- effects после реплики;
- список тем/переходов.

Преимущества:

- проще редактировать весь сценарий;
- проще локализовать;
- легче проверять пропущенные ветки;
- код диалоговой системы не меняется при переписывании текста.

Формат выбирается в coding phase: JSON, Godot Resources или другой сериализуемый data format. Ключевое требование — контент отдельно от логики UI.

---

# 9. Investigation Service

Отдельный слой отвечает за:

- добавление улики;
- формирование факта;
- открытие/зачёркивание версии;
- добавление записи в хронологию;
- открытие цели;
- уведомление UI блокнота;
- запрос autosave.

Главный граф берётся из `DETECTIVE_GRAPH.md`.

Пазл не должен самостоятельно решать, какой акт игры наступил. Он сообщает результат, а story progression проверяет условия `GATE`.

---

# 10. Inventory Service

Минимальный набор функций на уровне дизайна:

- add item;
- remove/consume item;
- select/deselect;
- check compatibility with hotspot;
- inspect item;
- emit state change.

Документы, которые являются только уликой, после получения могут автоматически переходить в блокнот, чтобы не захламлять inventory.

---

# 11. Scene Transition / checkpoint

Переходы между крупными локациями:

1. запрос перехода;
2. блокировка управления;
3. fade/короткая переходная анимация;
4. autosave устойчивого состояния;
5. смена scene/location;
6. установка Сомова на entry point;
7. возврат управления.

Save не должен фиксировать героя в середине анимации открытия двери, передачи предмета или memory montage.

---

# 12. Save strategy — local first

Игра сюжетная, поэтому потеря прогресса недопустима.

Используем модель:

> **local-first + cloud sync + versioned save.**

### Локальное сохранение

После каждого смыслового изменения state сериализуется локально.

### Облако

Синхронизация выполняется пакетно:

- после значимого progress event;
- при переходе между актами;
- при уходе в паузу/hidden, если платформа позволяет;
- при выходе в меню;
- с debounce, чтобы не отправлять сеть на каждый клик.

### Не храним

- текущий frame анимации;
- позицию курсора;
- промежуточный символ typewriter;
- временный hover state.

### Схема

Каждый save имеет `schema_version`. При будущих обновлениях используются migrations, а не предположение, что старый JSON всегда совпадает с новой структурой.

---

# 13. Разрешение local/cloud конфликта

Не использовать слепо «самый новый timestamp», потому что часы устройства могут быть неверны.

У save должны быть:

- monotonically increased `revision`;
- completed acts / progress rank;
- timestamp как дополнительный сигнал.

При загрузке:

1. если есть только один state — используем его;
2. если schema совместима и revision различается — берём большую revision;
3. если revision конфликтует, выбираем state с более продвинутым устойчивым progress rank;
4. спорный случай не должен автоматически затирать оба варианта: сохраняем резервную копию локально.

Для первой линейной игры этого достаточно без сложного merge отдельных улик.

---

# 14. Яндекс Игры — архитектурный adapter

На момент фиксации официальная документация Яндекс Игр позволяет хранить player data через SDK. Для `player.setData` указан лимит данных до 200 КБ на игрока и ограничение частоты запросов, поэтому компактный JSON save первой сюжетной игры укладывается с большим запасом.

Adapter отвечает за:

- SDK init;
- player init/authorization state;
- get cloud save;
- set cloud save;
- fullscreen ads;
- rewarded ads при необходимости;
- loading/ready lifecycle;
- platform visibility/gameplay events;
- ошибки SDK без утечки их в gameplay code.

Для сюжета не требуется хранить изображения/диалоги в save — только IDs и state, поэтому облачный объём остаётся маленьким.

Официальные источники для повторной проверки перед реализацией:

- https://yandex.ru/dev/games/doc/ru/sdk
- https://yandex.ru/dev/games/doc/ru/sdk/sdk-player
- https://yandex.ru/dev/games/doc/ru/requirements/1/9

Перед написанием adapter обязательно ещё раз сверить документацию, так как SDK может измениться.

---

# 15. Пикабу Игры — архитектурный adapter

Пикабу SDK предоставляет player ID/authorization, рекламу и platform lifecycle. Актуальные требования платформы указывают на необходимость облачных сохранений, при этом игра размещается на собственном сервере.

Поэтому для Пикабу планируем собственное небольшое cloud-save API.

### Pikabu adapter

- SDK init;
- `gameStarted` после готовности игры;
- player ID;
- обработка авторизации во время сессии;
- signed player data для backend verification;
- ads;
- pause при platform modal/ad/visibility;
- cloud save через наш backend.

### Backend save API — концептуально

Нужны операции:

- создать/проверить сессию игрока через signed data;
- получить save;
- записать save;
- хранить revision/schema/content version;
- optionally backup previous revision.

Секрет платформы никогда не попадает в клиентский билд.

Официальные источники для проверки перед реализацией:

- https://games.pikabu.ru/sdk/docs/sdk/init
- https://games.pikabu.ru/sdk/docs/sdk/player
- https://games.pikabu.ru/sdk/docs/sdk/ads
- https://games.pikabu.ru/sdk/docs/sdk/verification
- https://games.pikabu.ru/sdk/docs/requirements/tech

---

# 16. Local adapter

Обязателен для разработки.

Поведение:

- SDK считается мгновенно готовым;
- локальный fake player;
- cloud methods работают через локальную заглушку;
- ads можно симулировать debug-панелью;
- platform pause events можно вызвать вручную;
- ошибки network/SDK можно эмулировать.

Благодаря этому основная разработка и тестирование не требуют каждый раз публиковать билд на площадку.

---

# 17. Реклама

Реклама находится только в Platform/Ads service.

Gameplay отправляет смысловой запрос типа:

- `natural_break_reached`;
- `optional_reward_requested`.

Решение показывать рекламу принимает platform adapter/ad policy.

### Fullscreen

Для первой игры рекомендуем потенциальные естественные точки:

1. после завершения Акта II перед переходом к Книге — только если с предыдущей рекламы прошло достаточно времени;
2. после завершения Акта IV перед финальной частью — только если не разрушает темп.

Не обязательно показывать обе за одну короткую сессию.

### Rewarded

Не блокирует историю.

Допустимый сценарий:

- игрок уже запросил обычный намёк;
- может бесплатно получить следующий уровень по стандартной UX-логике;
- rewarded можно позже предложить только как дополнительное удобство/моментальное раскрытие самой явной подсказки, если это не нарушает правила площадки.

На старте проекта можно вообще выпустить rewarded позже. Архитектура должна позволять добавить его без изменения puzzle code.

---

# 18. Lifecycle и pause

Игра должна корректно реагировать на:

- потерю фокуса;
- скрытие вкладки;
- platform ad;
- окно авторизации;
- platform modal;
- сворачивание браузера.

При platform pause:

- блокируется input;
- останавливаются gameplay animations/timers;
- ставится на паузу музыка и ambience;
- не продолжается typewriter/диалог за кадром;
- после resume состояние восстанавливается безопасно.

Это особенно важно для требований Пикабу и в целом корректного web UX.

---

# 19. Audio architecture

Отдельные bus/categories:

- Master;
- Music;
- SFX;
- Ambience;
- Voice reactions.

Настройки громкости сохраняются независимо от сюжетного прогресса.

Platform pause может временно mute audio без изменения пользовательских sliders.

---

# 20. Loading

Не загружать все 15 фонов и все animation sheets первой игры при старте.

Стратегия:

- boot/menu core;
- текущая локация;
- соседние/следующие вероятные assets prefetch после запуска;
- тяжёлые уникальные assets подгружаются по акту.

Цель — быстрый первый экран и контролируемое потребление памяти на мобильных браузерах.

---

# 21. Localization-ready

Первый язык — русский.

Но весь динамический текст закладываем через ключи/таблицы, чтобы позже добавить другие языки без перерисовки интерфейса.

Не запекать в изображения:

- диалоги;
- цели;
- описания улик;
- кнопки;
- системные уведомления.

Допускаются рисованные неизменяемые вывески внутри мира; для важных сюжетных документов текст лучше собирать поверх бумажного background.

---

# 22. Analytics events — минимальный план

Не строим игру вокруг аналитики, но закладываем события для понимания прохождения:

- game_started;
- new_game;
- continue_game;
- act_started / act_completed;
- scene_entered;
- clue_found;
- fact_confirmed;
- puzzle_started / completed;
- hint_level_used;
- side_task_completed;
- ad_requested / shown / failed / closed;
- save_failed;
- game_completed;
- reset_game.

Не отправлять текст свободного ввода и персональные данные игрока в собственную аналитику без необходимости.

Конкретный analytics backend можно выбрать позже; интерфейс события должен существовать отдельно от gameplay.

---

# 23. Debug tools — предусмотреть архитектурно

До контентного производства нужны developer-only возможности:

- перейти к сцене;
- установить act;
- добавить/удалить clue;
- установить puzzle state;
- открыть все locations;
- очистить local save;
- показать сериализованный save;
- эмулировать SDK offline;
- эмулировать ad success/fail/closed;
- эмулировать pause/resume;
- эмулировать cloud conflict;
- включить hotspot overlay.

Debug UI никогда не попадает в production-visible интерфейс.

---

# 24. Error handling

Игрок не должен видеть сырые JavaScript/Godot ошибки.

### Save cloud failed

- local save остаётся валидным;
- маленькое ненавязчивое уведомление только если ошибка длительная;
- sync повторяется позже.

### SDK unavailable

- логируем;
- adapter возвращает controlled failure;
- не зависаем на бесконечном loading.

### Ad unavailable

- игра продолжает работу;
- rewarded reward не выдаётся до подтверждённого успешного условия;
- fullscreen failure просто закрывает рекламный сценарий.

---

# 25. Security

- никакие platform secret keys не хранятся в клиенте;
- Пикабу signed player data проверяется backend-ом;
- клиентский save нельзя считать защищённым от ручной правки;
- для сюжетной одиночной игры это не критично, пока нет экономики/платежей;
- если позже появятся покупки, entitlement проверяется серверно/через platform API.

В первой игре покупки не планируются.

---

# 26. Performance target

В coding/optimization phase проверяем:

- web Compatibility renderer;
- отсутствие огромных неиспользуемых texture memory allocations;
- разумный atlas/sprite approach;
- lazy loading;
- стабильное воспроизведение на мобильных Chrome/Safari/Yandex Browser;
- отсутствие тяжёлых shaders ради декоративных мелочей;
- ограничение одновременно активных ambient animations.

Художественный стиль 2D должен быть преимуществом по производительности.

---

# 27. Coding order после завершения pre-production

Когда пользователь отдельно даст команду начать код, рекомендуемый порядок:

1. пустой boot + local platform adapter;
2. save/story state;
3. scene transition + interaction/hotspot;
4. dialogue system;
5. inventory;
6. notebook/investigation;
7. map;
8. vertical slice `Agency → Boiler → Agency`;
9. platform facade;
10. Yandex adapter;
11. Pikabu adapter + backend save;
12. остальные сцены по актам;
13. ads;
14. polish/optimization;
15. moderation builds.

**До отдельной команды на разработку этот порядок остаётся только планом.**