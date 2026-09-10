# CONTENT REGISTRY — «Дело о пропавшем четверге»

> Статус: **утверждённый pre-code registry**  
> Версия: 1.0

Этот документ фиксирует стабильные идентификаторы контента. При разработке можно менять пути сцен и внутреннюю структуру Node, но эти ID желательно сохранять, чтобы не ломать save, dialogue data и аналитику.

## 1. Acts

| ID | Название |
|---|---|
| `act_01_friday_again` | Опять пятница |
| `act_02_day_traces` | Следы дня, которого никто не помнит |
| `act_03_book_of_days` | Книга дней |
| `act_04_witness` | Человек, который помнит |
| `act_05_return_thursday` | Вернуть четверг |
| `act_epilogue` | Эпилог |

---

## 2. Locations

| ID | Название |
|---|---|
| `loc_agency` | Частный сыск А. П. Сомова |
| `loc_center` | Центральная площадь |
| `loc_newspaper` | Тихореченский вестник |
| `loc_boiler` | Котельная №3 |
| `loc_communal` | Коммунальная контора |
| `loc_archive` | Городской архив |
| `loc_institute` | НИИ прикладных явлений |
| `loc_station` | Тихореченский вокзал |

Future/non-playable first game IDs reserve only when content enters production; не создаём заранее десятки пустых сущностей.

---

## 3. Scene states

| ID | Назначение |
|---|---|
| `scene_agency_morning` | старт игры |
| `scene_center_first_visit` | город после второго четверга |
| `scene_newsroom_first_visit` | первый визит в редакцию |
| `scene_photo_lab_commission` | фотоплёнка и комиссия |
| `scene_editor_office_false_lead` | Рогов / ложный след |
| `scene_boiler_first_visit` | знакомство с Горынычем |
| `scene_boiler_repair_reconstruction` | доказательство ремонта |
| `scene_kruglov_first_visit` | ввод Круглова |
| `scene_agency_first_deduction` | GATE-01 |
| `scene_archive_request` | архивный запрос |
| `scene_archive_book_reveal` | открытие Книги |
| `scene_institute_checkpoint` | проходная НИИ |
| `scene_mukhin_anchor_rules` | правила якорей |
| `scene_station_records` | поезд комиссии |
| `scene_station_telegram` | вчерашняя телеграмма |
| `scene_luggage_first_visit` | запись Круглова |
| `scene_kruglov_receipt` | квитанция в пальто |
| `scene_station_burov_arrival` | свидетель Буров |
| `scene_kruglov_reconstruction` | реконструкция поступка |
| `scene_luggage_anchor_reveal` | обнаружение якоря |
| `scene_archive_memory_return` | возврат четверга |
| `scene_agency_epilogue` | финал и Леший |

---

## 4. NPC IDs

| ID | Персонаж |
|---|---|
| `npc_somov` | Аркадий Петрович Сомов |
| `npc_klavdia` | Клавдия Семёновна |
| `npc_kruglov` | Фёдор Павлович Круглов |
| `npc_gorynych` | Змей Горыныч |
| `npc_listova` | Анна Матвеевна Листова |
| `npc_mukhin` | Борис Аркадьевич Мухин |
| `npc_rogov` | Яков Семёнович Рогов |
| `npc_burov` | Виктор Андреевич Буров |
| `npc_sinitsyna` | Нина Петровна Синицына |
| `npc_maria` | Мария Ивановна |
| `npc_petya` | Петя |
| `npc_alexey` | Алексей Степанович |
| `npc_proofreader` | Вера Николаевна |
| `npc_photographer` | Геннадий Шмелёв |
| `npc_station_duty` | Павел Егорыч |
| `npc_leshy_voice` | Леший, только эпилог |

Фоновые жители получают ID только если сохраняют состояние или участвуют в scripted interaction.

---

## 5. Puzzle IDs

| ID | Название |
|---|---|
| `puzzle_01_self_traces` | Мои собственные следы |
| `puzzle_02_photo_negatives` | Фотография без автора |
| `puzzle_03_gorynych_boot` | Сапог Горыныча |
| `puzzle_04_boiler_repair` | Ремонт, которого никто не помнит |
| `puzzle_05_archive_request` | Архив любит точность |
| `puzzle_06_book_gap` | Чего не хватает Книге |
| `puzzle_07_institute_pass` | Вчерашний пропуск |
| `puzzle_08_effect_border` | Граница четверга |
| `puzzle_09_old_telegram` | Телеграмма, которую уже отправили |
| `puzzle_10_departure_timeline` | Кто уехал до полуночи |
| `puzzle_11_luggage_record` | Запись камеры хранения |
| `puzzle_12_coat_lining` | Подкладка |
| `puzzle_13_storage_cell` | Ячейка |
| `puzzle_14_restore_anchor` | Вернуть на место |

---

## 6. Main clue IDs

| ID | Содержание |
|---|---|
| `clue_somov_note` | вчерашняя запись Сомова |
| `clue_agency_traces` | физические следы в кабинете |
| `clue_friday_newspaper` | готовый пятничный выпуск |
| `clue_proofreader_marks` | правки корректора |
| `clue_commission_photo` | фото комиссии у Котельной №3 |
| `clue_somov_boiler_signature` | подпись Сомова в журнале котельной |
| `clue_fresh_boiler_repair` | свежий ремонт |
| `clue_boiler_meter` | механические показания/расход |
| `clue_initial_inspection_act` | первичный акт проверки |
| `clue_readiness_act` | ранний акт готовности Круглова |
| `clue_inspection_calendar` | дата проверки |
| `clue_kruglov_memo` | рабочая записка о риске остановки |
| `clue_editor_note` | НЕ СТАВИТЬ ЭТО НА ПЕРВУЮ ПОЛОСУ |
| `clue_archive_issue_log` | запись выдачи Книги НИИ |
| `clue_archive_cabinet_trace` | след спешного доступа к шкафу |
| `clue_thursday_gap` | пустое место якоря |
| `clue_anchor_research_card` | карточка исследования семи якорей |
| `clue_anchor_experiment_record` | запись о свойствах памяти |
| `clue_effect_border_record` | данные о локальности эффекта |
| `clue_commission_train_log` | поезд комиссии |
| `clue_old_telegram` | вчерашняя телеграмма Сомова |
| `clue_kruglov_luggage_log` | запись камеры хранения |
| `clue_luggage_receipt` | квитанция Круглова |
| `clue_large_paper_trace` | optional след крупного листа |
| `clue_burov_repair_testimony` | Буров о ремонте |
| `clue_final_inspection_result` | разрешение продолжить работу |
| `clue_burov_station_testimony` | Круглов с листом на вокзале |
| `clue_thursday_anchor` | физически найденный якорь |

---

## 7. Fact IDs

| ID | Факт |
|---|---|
| `fact_missing_memory` | происходили действия, которых никто не помнит |
| `fact_thursday_happened` | четверг физически происходил |
| `fact_first_thursday_inspection` | первый четверг совпал с проверкой |
| `fact_boiler_problem` | комиссия нашла дефект |
| `fact_boiler_repaired` | ремонт был выполнен в четверг |
| `fact_somov_investigated_yesterday` | Сомов уже расследовал второй четверг |
| `fact_memory_not_time` | исчезает память, не время |
| `fact_anchor_missing` | из Книги вынут Четверг |
| `fact_anchor_causes_repeat` | отсутствие якоря повторяет эффект еженедельно |
| `fact_outside_witness_possible` | уехавший человек может помнить |
| `fact_burov_is_witness` | Буров подходит под правило |
| `fact_kruglov_used_storage` | Круглов оформил ячейку |
| `fact_problem_was_already_fixed` | проблема решена до похищения листа |
| `fact_kruglov_carried_sheet` | Буров видел Круглова с листом |
| `fact_kruglov_removed_anchor` | Круглов совершил действие |
| `fact_kruglov_intended_one_day` | хотел выиграть одни сутки |
| `fact_kruglov_forgot_action` | сам забыл из-за эффекта |
| `fact_anchor_recovered` | якорь найден |
| `fact_memory_restored` | память города возвращена |

---

## 8. Hypothesis IDs

| ID | Версия | Финал |
|---|---|---|
| `hyp_editorial_coverup` | редакция хотела скрыть четверг | disproved |
| `hyp_institute_accident` | НИИ случайно запустил эффект | disproved |
| `hyp_kruglov_motive` | Круглов хотел скрыть проверку | evolved → confirmed cause |
| `hyp_thursday_never_happened` | четверга физически не было | disproved early |

Не плодить ложные версии ради количества. Четырёх достаточно для первой игры.

---

## 9. Item IDs

### Inventory

| ID | Предмет |
|---|---|
| `item_commission_photo` | фотография комиссии |
| `item_institute_pass` | временный пропуск НИИ |
| `item_luggage_receipt` | квитанция камеры хранения |
| `item_thursday_anchor` | якорь Четверг |
| `item_wooden_airplane` | самолётик, при необходимости временного взаимодействия |

### Evidence-only / notebook

- `evidence_friday_newspaper`
- `evidence_boiler_log`
- `evidence_inspection_act`
- `evidence_readiness_act`
- `evidence_archive_log`
- `evidence_anchor_scheme`
- `evidence_train_log`
- `evidence_telegram`
- `evidence_luggage_log`
- `evidence_final_inspection`

Не все evidence должны физически копироваться Сомовым; часть может храниться как запись/фото в блокноте.

---

## 10. Side task IDs

| ID | Название |
|---|---|
| `side_airplane` | Самолётик |
| `side_bread_debt` | Кто должен за хлеб? |
| `side_missing_wage` | Деньги за несуществующий день |

States:

- `not_started`
- `active`
- `completed`

---

## 11. Progress gates

| ID | Условный смысл |
|---|---|
| `gate_01_thursday_existed` | доказано: четверг был, память исчезла |
| `gate_02_need_outside_witness` | раскрыты правила якоря, нужен уехавший свидетель |
| `gate_03_kruglov_action_proven` | Круглов связан с листом и ячейкой, Буров подтверждает |
| `gate_04_anchor_found` | якорь физически найден |
| `gate_05_case_complete` | якорь возвращён, эпилог завершён |

---

## 12. Progress rank для save conflict

Линейная шкала используется только как tie-breaker при конфликте cloud/local save.

Примерные ранги:

- `0` — новое дело;
- `10` — блокнот найден;
- `20` — GATE-01;
- `30` — Книга обнаружена;
- `40` — правила НИИ поняты;
- `50` — запись камеры хранения;
- `60` — квитанция найдена;
- `70` — Буров дал свидетельство;
- `80` — Круглов реконструировал поступок;
- `90` — якорь найден;
- `100` — память возвращена;
- `110` — эпилог завершён.

Progress rank не используется для управления сюжетом внутри игры. Он является производным значением из подтверждённых gates.

---

## 13. Autosave events

Стабильные причины:

- `save_new_clue`
- `save_new_fact`
- `save_puzzle_completed`
- `save_item_changed`
- `save_location_unlocked`
- `save_dialogue_critical_complete`
- `save_gate_reached`
- `save_side_task_changed`
- `save_return_to_menu`
- `save_app_background`

Реализация может debounce несколько событий в один physical write/cloud sync.

---

## 14. Analytics event IDs

Минимальный словарь:

- `game_start`
- `new_game`
- `continue_game`
- `act_start`
- `act_complete`
- `location_enter`
- `clue_found`
- `fact_confirmed`
- `hypothesis_added`
- `hypothesis_disproved`
- `puzzle_start`
- `puzzle_complete`
- `hint_used`
- `side_task_complete`
- `fullscreen_requested`
- `fullscreen_result`
- `rewarded_requested`
- `rewarded_result`
- `save_local_ok`
- `save_cloud_fail`
- `case_complete`

Параметры события используют IDs из этого registry, а не русские отображаемые строки.

---

## 15. Versioning

После первого публичного release:

- существующий ID нельзя тихо переиспользовать для другого смысла;
- удалённый content ID при необходимости поддерживается migration-логикой;
- локализованный текст можно менять свободно, если смысл state effect не меняется;
- новые side tasks получают новые ID, не сдвигая старые числовые индексы.

Это делает save устойчивым к обновлениям игры.