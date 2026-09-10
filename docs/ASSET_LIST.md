# ASSET LIST — «Дело о пропавшем четверге»

> Статус: **утверждённый production-план**  
> Версия: 1.0  
> Цель: подготовить полный список визуальных и аудио-ассетов до начала кода.

## 1. Общие технические правила ассетов

### Базовый формат сцены

- композиция: **16:9 landscape**;
- мастер-фоны: **1920×1080**;
- без запечённого игрового UI;
- текст на вывесках допустим только если это часть окружения;
- интерактивные предметы, которые меняют состояние, по возможности держать отдельными слоями/спрайтами;
- персонажи — прозрачный PNG/WebP master высокого качества;
- в Git храним финальные игровые файлы и при необходимости облегчённые preview; исходники дизайнера можно хранить отдельно, если они слишком тяжёлые.

### Визуальный канон

См. `VISUAL_BIBLE.md`.

Главное:

> сначала знакомая провинциальная жизнь, затем встроенная в неё сказочность.

---

# 2. Рекомендуемая структура ассетов

```text
assets/
├── backgrounds/
│   ├── agency/
│   ├── center/
│   ├── newspaper/
│   ├── boiler/
│   ├── communal/
│   ├── archive/
│   ├── institute/
│   ├── station/
│   └── optional/
├── characters/
│   ├── somov/
│   ├── klavdia/
│   ├── kruglov/
│   ├── gorynych/
│   ├── listova/
│   ├── mukhin/
│   ├── rogov/
│   ├── burov/
│   ├── sinitsyna/
│   └── townsfolk/
├── props/
├── clues/
├── ui/
├── fx/
├── audio/
│   ├── music/
│   ├── ambience/
│   ├── sfx/
│   └── voices/
└── promo/
```

`docs/assets/` остаётся для concept/reference материалов, включая утверждённую карту мира.

---

# 3. Фоны — обязательный набор

Цель: **14 основных уникальных фонов**, а повторные сюжетные сцены строятся изменением персонажей/props/диалогов, а не новым фоном.

## BG01 — Агентство Сомова

`backgrounds/agency/agency_office.webp`

Один широкий фон объединяет:

- рабочий стол Сомова;
- стол Клавдии;
- шкаф дел;
- календарь;
- телефон;
- чайник;
- окно;
- входную дверь.

Отдельные изменяемые props:

- блокнот;
- календарный лист;
- свежая спичка/пепельница;
- папка текущего дела;
- телефонный аппарат при звонке.

Используется: старт, промежуточная сверка, эпилог.

---

## BG02 — Центральная площадь / улица агентства

`backgrounds/center/central_square.webp`

Один широкий городской хаб.

Должны читаться:

- агентство в стороне/выход к нему;
- газетный киоск;
- автобусная остановка;
- гастроном как часть окружения;
- проход к редакции;
- обычные и сказочные жители.

Это позволяет не производить отдельный обязательный фон гастронома. Мини-задача с продавщицей может открывать короткий interior overlay либо происходить у открытого прилавка/входа.

---

## BG03 — Редакция, общий зал

`backgrounds/newspaper/newsroom.webp`

- столы;
- печатные машинки;
- свежий выпуск;
- корректор;
- фотограф;
- доска материалов;
- проход в кабинет Рогова и фотолабораторию.

---

## BG04 — Кабинет Рогова

`backgrounds/newspaper/editor_office.webp`

- стол;
- старые подшивки;
- телефон;
- записка «НЕ СТАВИТЬ ЭТО НА ПЕРВУЮ ПОЛОСУ»;
- шкаф/доска публикаций.

---

## BG05 — Фотолаборатория

`backgrounds/newspaper/photo_lab.webp`

- красноватый/тёплый свет, но не слишком тёмный;
- увеличитель;
- негативы;
- контактные отпечатки;
- ванночки;
- верёвка/сушка фотографий.

Для P02 требуется отдельный крупный puzzle-overlay фотоплёнки.

---

## BG06 — Котельная №3

`backgrounds/boiler/boiler_hall.webp`

Главный tone-reference фон.

- большой котёл;
- трубы;
- манометры;
- ремонтный узел;
- место Горыныча;
- журнал;
- уголь/технические предметы.

Ремонтный угол не делаем отдельным фоном: камера/композиция должна позволять рассмотреть его через zoom-overlay.

---

## BG07 — Коммунальная контора, коридор/приёмная

`backgrounds/communal/communal_reception.webp`

Короткий фон для ощущения учреждения и фоновых работников.

При production-сокращении может быть заменён коротким переходом и сразу кабинетом Круглова.

---

## BG08 — Кабинет Круглова

`backgrounds/communal/kruglov_office.webp`

- стол;
- папки «СРОЧНО»;
- телефон;
- шкаф;
- вешалка с пальто;
- портфель;
- календарь проверок.

Пальто и разрыв подкладки — отдельное интерактивное состояние.

---

## BG09 — Архив, читальный зал

`backgrounds/archive/archive_reading_room.webp`

- стойка Анны Матвеевны;
- каталоги;
- журналы выдачи;
- стол;
- дверь/проход в хранилище.

---

## BG10 — Архив, хранилище

`backgrounds/archive/archive_storage.webp`

- старый шкаф;
- Книга учёта дней;
- стеллажи;
- рабочая лампа;
- место для Клавдии и Анны.

Книга должна иметь отдельный крупный interactive overlay.

---

## BG11 — НИИ, проходная

`backgrounds/institute/checkpoint.webp`

- обычная скучная проходная;
- вахта;
- журнал;
- пропуска;
- коридор внутрь;
- минимум «секретной лаборатории».

---

## BG12 — Кабинет/лаборатория Мухина

`backgrounds/institute/mukhin_lab.webp`

- обычный кабинет исследователя;
- карточки;
- приборы;
- схема семи якорей;
- один бытовой аномальный предмет как визуальный гэг.

Не перегружать sci-fi устройствами.

---

## BG13 — Вокзал, зал ожидания

`backgrounds/station/station_hall.webp`

Объединяет:

- кассы;
- расписание;
- телеграфное окно;
- выход на перрон;
- переход к камере хранения.

---

## BG14 — Вокзал, камера хранения

`backgrounds/station/luggage_storage.webp`

- стойка Нины Петровны;
- книга хранения;
- ячейки/шкафы;
- финальная ячейка с листом.

---

## BG15 — Перрон

`backgrounds/station/platform.webp`

**Желательно производить.**

Нужен для красивого появления Бурова и ощущения внешнего мира.

Если budget-cut критичен, прибытие можно показать через окно/выход вокзала, но художественно отдельный перрон лучше.

---

# 4. Необязательные/резервные фоны

## OPT-BG01 — Набережная / Старый мост

Для короткой эмоциональной передышки. Не требуется основной логике.

## OPT-BG02 — Интерьер гастронома

Производить только если побочная задача «Кто должен за хлеб» остаётся отдельной полноценной сценой.

### Итог

- core minimum: **14 фонов** без отдельного коридора коммуналки или перрона;
- рекомендуемая версия: **15–16 фонов**;
- maximum с optional: **17**.

---

# 5. Крупные puzzle overlays / close-ups

Обязательные:

1. `clues/somov_notebook_first_note.webp`
2. `clues/newspaper_friday.webp`
3. `clues/photo_negatives_board.webp`
4. `clues/commission_photo.webp`
5. `clues/boiler_logs.webp`
6. `clues/boiler_repair_closeup.webp`
7. `clues/readiness_act.webp`
8. `clues/archive_issue_log.webp`
9. `clues/book_of_days_open.webp`
10. `clues/book_anchor_gap.webp`
11. `clues/institute_anchor_scheme.webp`
12. `clues/station_schedule.webp`
13. `clues/telegram_log.webp`
14. `clues/luggage_log.webp`
15. `clues/kruglov_coat_closeup.webp`
16. `clues/luggage_receipt.webp`
17. `clues/thursday_anchor.webp`
18. `clues/book_thursday_restored.webp`

Документные тексты лучше собирать UI-текстом поверх декоративной бумаги, если текст должен быть идеально читаемым и локализуемым. Запекать в изображение только короткие неизменяемые заголовки, если это художественно необходимо.

---

# 6. Сомов — полный animation sheet

Самый большой персонажный пакет.

## Направления

Для ходьбы нужны минимум:

- left;
- right;
- front/diagonal-down;
- back/diagonal-up.

Можно зеркалить left/right, если костюм и детали персонажа симметричны. Если есть асимметричная сумка/карман — учитывать это заранее.

## Core animations

1. `idle_neutral` — мягкое дыхание/перенос веса.
2. `idle_blink`.
3. `walk_side`.
4. `walk_front`.
5. `walk_back`.
6. `turn` / короткие transition poses.
7. `talk_neutral`.
8. `talk_question`.
9. `talk_dry` / небольшая жестикуляция.
10. `think`.
11. `surprise`.
12. `suspicious`.
13. `shrug`.
14. `inspect_magnifier`.
15. `inspect_low` / наклон или присед.
16. `point`.
17. `pick_up_low`.
18. `pick_up_table`.
19. `use_object`.
20. `open_door`.
21. `write_notebook`.
22. `take_from_pocket`.
23. `read_document`.
24. `hand_item_to_npc`.
25. `receive_item`.
26. `phone_listen` — для возможных сцен/будущего переиспользования.
27. `coat_on/off` не нужен как системная механика; одежда постоянна.

### Эмоциональные one-shot

- усталый вздох;
- короткая довольная реакция после дедукции;
- лёгкое смущение;
- «понял» — поднятый палец/взгляд;
- осознание собственного вчерашнего следа.

Не делать десятки уникальных анимаций, если их можно закрыть общими выразительными позами.

---

# 7. Клавдия Семёновна

Она чаще статична, поэтому пакет меньше.

1. idle at desk;
2. blink;
3. typewriter typing;
4. talk neutral;
5. talk sarcastic;
6. glasses adjust;
7. look over glasses;
8. stand/walk short cycle — если идёт в архив;
9. touch/listen to wall/cabinet;
10. arms crossed;
11. phone answer;
12. surprised/concerned subtle;
13. exit/enter short pose if required.

---

# 8. Круглов

1. idle seated;
2. idle standing;
3. talk bureaucratic;
4. talk nervous;
5. page through papers;
6. wipe forehead / anxiety;
7. shrug/confused;
8. hand documents;
9. inspect own coat;
10. shocked at receipt;
11. seated defeated/quiet;
12. memory-return reaction;
13. final conversation neutral.

Ходьба полноценным циклом нужна только если персонаж реально перемещается по сцене. Иначе достаточно 2–3 staging poses.

---

# 9. Змей Горыныч

Сложный персонаж — заранее разделить тело и головы по слоям, если анимация собирается модульно.

### Body

- idle;
- working at boiler;
- arms gesture;
- point to repair;
- receive boot;
- proud pose.

### Heads

Для каждой головы:

- idle;
- blink;
- talk;
- look_left/right;
- annoyed;
- laugh/smirk;

Дополнительно:

- правая голова sleep;
- wake;
- общий трёхголовый спор;
- memory return reaction.

Огонь из пасти не нужен как постоянная атака. Допустим один маленький бытовой FX, например прикурить/подогреть деталь, если сцена требует.

---

# 10. Остальные ключевые NPC

Для каждого базово:

- idle;
- blink;
- talk neutral;
- talk expressive;
- 2 характерные жестовые позы;
- 1 реакция на ключевую улику/финал.

## Анна Матвеевна

Дополнительно:

- листает журнал;
- бережно держит документ;
- ужас от неправильного хранения листа.

## Мухин

- поправляет очки;
- указывает на схему;
- записывает наблюдение;
- сухо корректирует термин Сомова.

## Рогов

- громко разговаривает;
- машет газетой;
- показывает фотографию/полосу;
- финальная реакция на воспоминание об опечатке.

## Буров

- стоит с портфелем;
- указывает по хронологии;
- показывает документ проверки;
- короткая усталая реакция.

## Нина Петровна

- сидит/стоит за стойкой;
- листает книгу;
- указание на правило/табличку;
- принимает квитанцию;
- открывает ячейку.

---

# 11. Малые NPC

## Обязательные

- корректор редакции;
- фотограф;
- дежурный/телеграфист вокзала;
- Петя;
- дед Алексей;
- 3–5 горожан на площади;
- 1 сказочный фоновый горожанин;
- 2 работника котельной/коммуналки как background sprites.

### Пакет малых NPC

Обычно достаточно:

- idle;
- blink;
- 2 talk poses;
- 1 action/reaction.

Не производить полноценные walk cycles всем, если они не ходят по сцене.

---

# 12. Предметы окружения с изменяемыми состояниями

Обязательные отдельные props:

### Agency

- notebook closed/open;
- calendar Wednesday/Friday;
- case folder;
- phone idle/ringing.

### Newspaper

- newspaper stack;
- note;
- negatives;
- developed commission photo.

### Boiler

- boot hidden/found;
- bucket/box moved;
- valve normal/repaired close-up;
- logs/documents.

### Communal

- readiness act;
- coat normal / lining opened;
- luggage receipt;
- briefcase open/closed.

### Archive

- cabinet normal/open;
- Book closed/open;
- anchor gap;
- restored anchor state.

### Institute

- visitor pass old/new;
- research cards;
- seven-anchor diagram.

### Station

- schedule;
- telegram slip/log;
- luggage register;
- storage cell closed/open;
- Thursday anchor rolled/unrolled.

### Emotional side task

- wooden airplane;
- child drawing / glue receipt depending final implementation.

---

# 13. UI asset pack

Все элементы **без запечённого динамического текста**, кроме декоративных неизменяемых надписей, если утверждены отдельно.

## HUD

- pause button normal/hover/pressed;
- inventory button normal/hover/pressed/active;
- notebook button states;
- map button states;
- hotspot highlight frame/marker;
- autosave icon/animation;
- small notification panel.

## Cursor pack desktop

- default;
- walk;
- magnifier/inspect;
- talk;
- take/use hand;
- exit;
- selected-item cursor frame;
- unavailable subtle state.

## Dialogue

- main dialogue strip 9-slice or scalable panel;
- portrait frame;
- speaker-name plaque;
- continue indicator;
- dialogue topic button states;
- thought strip;
- skip/fast text indicator if needed.

## Inventory

- container panel;
- slot normal/hover/selected;
- item quantity marker not required unless later needed;
- close/collapse control.

## Notebook

- cover;
- spread/background pages;
- tabs: Дело, Факты, Версии, Люди, Улики, Хронология;
- paper clips/tape decorative elements;
- crossed-out mark;
- pencil circle/underline marks;
- hint control.

## Map

- simplified working map background;
- location labels/frames;
- new-location pencil circle;
- active location marker;
- small note/pin/tape elements.

## Pause/settings

- pause paper/panel;
- buttons;
- sliders;
- toggles;
- text-size controls;
- hotspot-hint control.

## Main menu

- title treatment `Уезд №13`;
- subtitle treatment `Дело о пропавшем четверге`;
- menu button set;
- decorative case-folder motif.

---

# 14. FX

Стиль FX — рисованный, простой, не glossy.

Обязательные:

- tiny dust motes / boiler particles;
- furnace glow/fire loop;
- steam puff;
- telephone ring visual motion if used;
- light paper flutter;
- subtle pencil draw/circle animation for notebook/map;
- memory-return transition: **не магический взрыв**, а мягкий короткий визуальный shift/flash plus montage cut;
- scene transition fade.

Optional:

- rain/snow not needed in first game unless narrative changes;
- dragon tiny fire gag;
- birds/crow ambient animation.

---

# 15. Музыка

Минимальный музыкальный пакет:

1. `theme_main` — главное меню / тема Уезда №13.
2. `theme_agency` — спокойная детективная.
3. `theme_town` — лёгкая провинциальная.
4. `theme_investigation` — ненавязчивое любопытство.
5. `theme_boiler` — индустриально-комедийная вариация.
6. `theme_archive_institute` — тихая загадочность.
7. `theme_station` — движение/ожидание.
8. `theme_reveal` — позднее расследование, чуть напряжённее.
9. `theme_memory_return` — короткая тёплая финальная тема.
10. `theme_credits` — вариация главной темы.

Можно сократить до 5–6 композиций через вариации/переиспользование, если бюджет ограничен.

Музыка должна зацикливаться бесшовно и не мешать чтению.

---

# 16. Ambience / SFX

## Общие UI

- hover/click мягкий;
- открыть/закрыть блокнот;
- перелистывание страницы;
- карандаш;
- открыть карту;
- взять/положить предмет;
- autosave subtle;
- typewriter UI optional.

## Agency

- часы;
- улица за окном;
- печатная машинка Клавдии;
- чайник;
- телефон.

## Town

- автобус;
- редкие машины;
- шаги;
- птицы;
- городской гул.

## Newspaper

- машинки;
- бумага;
- фотолаборатория;
- телефон.

## Boiler

- котёл;
- пар;
- металл;
- уголь;
- инструменты;
- низкий промышленный loop.

## Archive

- бумага;
- шкаф;
- скрип пола;
- тихие часы.

## Institute

- лампа/гул прибора;
- карточки/бумага;
- один странный аномальный звук очень дозированно.

## Station

- объявления без обязательного разборчивого текста;
- поезд;
- двери;
- колёса;
- телеграф;
- ячейка хранения.

---

# 17. Voice reactions

Полная озвучка не обязательна.

Для живости можно записать короткие нейтральные вокальные SFX:

- вздох Сомова;
- кашель/«хм»;
- ворчание Клавдии;
- три разных тембра голов Горыныча;
- вздох Круглова;
- короткое «кхм» Рогова;
- нейтральные реакции малых NPC.

Все смысловые реплики остаются текстовыми.

---

# 18. Promo assets — заложить заранее

Чтобы после готовности билда не собирать маркетинг с нуля:

- square icon/master минимум 1024×1024;
- horizontal cover 1920×1080;
- 3–6 clean gameplay screenshots;
- key art с Сомовым и Тихореченском;
- logo/title transparent master;
- store description imagery;
- возможная вертикальная social cover отдельно.

В promo не использовать чужих известных персонажей/стили как прямую копию.

---

# 19. Производственные приоритеты

## Tier A — блокирует vertical slice

1. Сомов core movement + talk + inspect.
2. Агентство.
3. Клавдия.
4. базовый HUD/диалог.
5. блокнот.
6. карта.
7. одна полноценная расследовательская локация — Котельная №3.
8. Горыныч.

## Tier B — блокирует полное прохождение

Все остальные core backgrounds, Круглов, Листова, Мухин, Рогов, Буров, Нина, обязательные puzzle overlays и предметы.

## Tier C — polish

Фоновые NPC, optional backgrounds, дополнительные ambient animations, расширенный FX, дополнительные музыкальные темы.

---

# 20. Definition of Done для ассета

Ассет считается готовым, если:

1. совпадает с `VISUAL_BIBLE.md`;
2. имеет понятное имя и путь;
3. не содержит случайного UI/лишнего текста;
4. прозрачность корректна;
5. нет обрезанных теней/частей персонажа;
6. pivot/логическая опорная точка понятна разработчику;
7. состояния/кадры не меняют масштаб и пропорции персонажа случайно;
8. в игровом размере объект читается;
9. файл оптимизирован для web без заметной деградации;
10. для анимации известны fps/порядок кадров или отдельные именованные frames.

---

# 21. Что не производим до необходимости

- огромный набор эмоций каждого фонового NPC;
- локации леса/деревни второй части;
- дом Сомова, если он не появляется в первой игре;
- полноценную поликлинику;
- внутриигровые покупки/магазинный UI;
- боевые эффекты;
- 3D-модели;
- отдельные фоны для каждого повторного посещения.

Первая игра должна закончиться качественно, а не утонуть в количестве ассетов.