# Somov Detective

Сатирический линейный point-and-click квест в оригинальном сказочно-провинциальном мире **«Уезд №13»**.

## Статус

**Pre-production первой игры завершён. Проект готов к переходу в coding + asset production phase.**

До отдельной команды на разработку игровой код не пишем.

Первая игра:

# «Дело о пропавшем четверге»

В Тихореченске уже две недели подряд жители проживают четверг полностью, но после наступления пятницы теряют память о прошедшем дне. Физические следы, документы и сделанная работа остаются.

Частный детектив Аркадий Петрович Сомов после второго случая обнаруживает, что во вчерашний забытый четверг уже расследовал это же дело, и начинает заново идти по собственным следам.

## Канон

- мир: **Уезд №13**;
- город: **Тихореченск**;
- эпоха: оригинальная условная русская провинция с ощущением 1970–1980-х и старой сказки;
- сказочные существа всегда живут рядом с людьми;
- главный закон: **«Всякое чудо оставляет след»**;
- герой: **Аркадий Петрович Сомов**, частный детектив и бывший журналист;
- секретарь: **Клавдия Семёновна**, кикимора;
- первая история полностью спроектирована от начала до финала;
- финал тизерит следующее дело через звонок Лешего.

## Документы

### База проекта

- [`docs/GAME_BIBLE.md`](docs/GAME_BIBLE.md) — главная актуальная сводка.
- [`docs/PREPRODUCTION_COMPLETE.md`](docs/PREPRODUCTION_COMPLETE.md) — Definition of Ready и итог pre-production.

### Мир и стиль

- [`docs/WORLD.md`](docs/WORLD.md) — канон мира.
- [`docs/MAP.md`](docs/MAP.md) — география Тихореченска и scope первой игры.
- [`docs/VISUAL_BIBLE.md`](docs/VISUAL_BIBLE.md) — визуальный язык.
- [`docs/assets/map_tikhorechensk_v2.png`](docs/assets/map_tikhorechensk_v2.png) — утверждённая карта v2.

### Сюжет и игровой контент

- [`docs/STORY.md`](docs/STORY.md) — утверждённая сюжетная повесть.
- [`docs/CHARACTERS.md`](docs/CHARACTERS.md) — канонический состав персонажей.
- [`docs/LOCATIONS.md`](docs/LOCATIONS.md) — 8 игровых узлов / 14 core backgrounds.
- [`docs/SCENES.md`](docs/SCENES.md) — 5 актов, 21 смысловая сцена + эпилог.
- [`docs/DETECTIVE_GRAPH.md`](docs/DETECTIVE_GRAPH.md) — улики, факты, версии и progression gates.
- [`docs/PUZZLES.md`](docs/PUZZLES.md) — 14 core puzzles/interactions.
- [`docs/SIDE_TASKS.md`](docs/SIDE_TASKS.md) — optional mini-tasks и ambient content.
- [`docs/DIALOGUE_BIBLE.md`](docs/DIALOGUE_BIBLE.md) — голоса персонажей и правила текста.
- [`docs/DIALOGUE_SCRIPT.md`](docs/DIALOGUE_SCRIPT.md) — основной обязательный диалоговый сценарий.
- [`docs/HOTSPOTS.md`](docs/HOTSPOTS.md) — интерактивные зоны и states каждого core-фона.
- [`docs/WALKTHROUGH.md`](docs/WALKTHROUGH.md) — канонический QA-проход.

### Production / implementation planning

- [`docs/UI_UX.md`](docs/UI_UX.md) — desktop/mobile UI/UX.
- [`docs/ASSET_LIST.md`](docs/ASSET_LIST.md) — фоны, персонажи, анимации, props, UI, FX и звук.
- [`docs/ASTRA_ASSET_BATCH_01.md`](docs/ASTRA_ASSET_BATCH_01.md) — первое production-ТЗ для AstraGPT; визуальные концепты берутся из `docs/assets/`.
- [`docs/CONTENT_REGISTRY.md`](docs/CONTENT_REGISTRY.md) — стабильные IDs контента и save-state сущностей.
- [`docs/TECH_ARCHITECTURE.md`](docs/TECH_ARCHITECTURE.md) — архитектура Godot/платформ без реализации.
- [`docs/QA_RELEASE_PLAN.md`](docs/QA_RELEASE_PLAN.md) — QA, сохранения, платформы и release gates.

## Production scope первой игры

- **8** глобальных игровых узлов;
- **14** core backgrounds;
- **5** актов;
- **21** смысловая сцена + эпилог;
- **14** core puzzle/interactions;
- небольшой сюжетный инвентарь;
- обязательная к производству эмоциональная optional-линия `Самолётик`;
- ориентир обычного первого прохождения: **90–120 минут**.

## Платформы

Архитектурно закладываются отдельные adapters:

- Local/browser development;
- Яндекс Игры;
- Пикабу Игры.

Core gameplay не зависит напрямую от SDK.

Сохранения: **local-first + cloud sync + versioned state**.

## Текущий asset production

Первый тестовый batch для AstraGPT:

[`docs/ASTRA_ASSET_BATCH_01.md`](docs/ASTRA_ASSET_BATCH_01.md)

Локальный путь проекта для Astra:

`C:\Users\Роман\Documents\GitHub\Games\somov-detective`

Все утверждённые визуальные concept/reference-изображения складываются в:

`docs/assets/`

Astra обязана использовать их как основной визуальный ориентир и не менять игровой код.

## Следующая фаза

После отдельной команды на начало разработки:

1. подготовить Godot 4 Web-проект;
2. собрать core systems через Local adapter;
3. сделать vertical slice:

`Агентство → карта → Котельная №3 → улика → блокнот → autosave/load → Агентство`;

4. после проверки slice масштабировать систему на всю игру;
5. отдельно подключить Яндекс и Пикабу adapters;
6. затем production polish, QA и модерация.

Главное правило проекта:

> **Сначала целиком понимаем игру. Потом код реализует утверждённую игру, а не игра подстраивается под случайно написанный код.**
