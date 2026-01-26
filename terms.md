<summary markdown="span">INSTRUCTIONS FOR TEXT MODELS (Glossary)</summary>

Purpose:
- Use this file as the authoritative glossary for terminology in answers.

Data format:
- Each entry is a block separated by `---`.
- The term header is a level-2 heading: `## <EN_TERM>`.
- Fields are inline metadata in the form `key:: value`.
- `aliases::` contains (and/or other) synonyms/explanations (semicolon-separated).
- `mean::` is the short meaning of the term (one line).

Rules:
1. If a term from this glossary is used in an answer (matched by the `## <EN_TERM>` header or any value in `aliases::`, case-insensitive), do NOT translate it and do NOT add an explanation/definition for it.
	- If the user explicitly `asks что такое <term>` / `объясни <term>`, then provide a short definition even if the term exists in the glossary
2. Treat the header `## <EN_TERM>` and any value in `aliases::` as interchangeable identifiers. If the user uses an alias, reply using the same alias (preferred) or the canonical header term (optional), but keep the meaning identical.
3. If a term is NOT found in this glossary:
	   - Provide a short common definition (1–2 sentences).
	   - Propose a new glossary block (in the exact format below) that the user can paste into this file.
4. Do not invent existing entries. If not found, treat as missing and follow rule #3.
5. Ask a clarification question only when the term is ambiguous and multiple glossary entries could match.
6. Keep answers concise and in Russian unless explicitly asked otherwise.
7. After reading this instruction, you should retell it in the chat you started. 


New entry template (paste-ready):
## <EN_TERM>
- aliases:: <RU_ALIAS_1>; <RU_ALIAS_2>
- mean:: <RU_MEANING_1_LINE>



---
## span 
- aliases:: спан; шаг трейса; операция в трейсе; операция внутри распределённого запроса
- mean:: Логическая единица работы (операция) в трейсинге: имеет имя операции, время начала и длительность; спаны могут быть вложенными и упорядоченными, образуя причинно‑следственные связи внутри trace.


---
## trace
- aliases:: дерево span’ов; граф span’ов; набор связанных span’ов
- mean:: «след» одного запроса/операции в распределённой системе: набор связанных между собой span’ов, которые вместе показывают полный путь выполнения через сервис(ы) и компоненты

---
## agent 
- aliases:: агент; агенты; коллектор; data collector; monitoring agent; log agent
- mean:: небольшая программа, установленная на целевой системе (хост, VM, контейнер), которая локально собирает данные (метрики, логи, события) и отправляет их на центральный сервер/платформу. Агент работает постоянно, имеет доступ к внутреннему состоянию системы (CPU, память, процессы, файлы логов) и поэтому даёт более детализированную и точную картину, чем удалённый опрос без установки софта.

---
## ingestion
- aliases:: инжест; сбор данных; приём данных; процесс сбора; процесс приёма данных
- mean:: Процесс доставки данных (логи/метрики/трейсы/события) из источников в систему хранения/аналитики для дальнейшей обработки и поиска.

---
## ETL pipeline
- aliases:: ETL-конвейер; конвейер Extract-Transform-Load
- mean:: Процесс Extract→Transform→Load: извлечь данные, преобразовать к нужной схеме/формату и загрузить в целевое хранилище (обычно батчево, но бывает и стриминг-реализация)


---
## батчево
- aliases:: batch processing
- mean:: когда данные/задачи не обрабатываются сразу по мере поступления, а **накапливаются** за период и потом обрабатываются “пачкой” по расписанию или при достижении объёма (например, раз в час/ночью)

---
## dashboard
- aliases:: дашборд; панель мониторинга
- mean:: Набор визуализаций (графики/таблицы/счётчики), собранных под конкретную задачу наблюдения (SLO/сервис/хост/инцидент) и обновляющихся из источников данных.

---
## metric query
- aliases:: запрос к метрикам; PromQL-запрос
- mean:: Запрос к хранилищу метрик (time-series) для агрегации/фильтрации/расчёта производных показателей и отображения их на графиках/в алертах

---
## time series
- aliases:: временной ряд; time-series
- mean:: Данные, где каждое значение привязано ко времени (обычно метрика), и анализ делается через тренды/агрегации по окнам времени

---
## log query
- aliases:: запрос к логам; фильтр логов
- mean:: Запрос/фильтрация по лог-хранилищу для нахождения событий по меткам/полям/строкам за заданный период (в зависимости от стека: ELK, Loki и т.д.)

---
## Explore
- aliases:: Explore (Grafana); режим исследования
- mean:: Раздел Grafana для быстрых ad-hoc запросов и анализа данных без создания дашборда: можно “покрутить” запросы, время, фильтры и посмотреть детали

---
## alert
- aliases:: алерт; тревога; оповещение
- mean:: Автоматическое уведомление по условию (порог/аномалия/ошибка), обычно на базе метрик или лог-сигналов, чтобы быстро начать реакцию на инцидент

---
## audit
- aliases:: аудит; audit trail; журнал аудита
- mean:: Практика/процесс фиксации “кто что сделал и когда” (доступы, изменения, действия) для расследований, соответствия требованиям и безопасности; часто опирается на централизованные логи

---
## bare metal
- aliases:: физический сервер; «железо»
- mean:: Сервер без слоя виртуализации/облака, то есть ОС работает напрямую на физическом оборудовании (в противоположность VM/containers в облаке)

---
## p95 latency
- aliases:: p95 latency; 95-й перцентиль задержки; p95 задержка
- mean:: Значение задержки, ниже которого укладываются 95% запросов за выбранный интервал; используется вместо “среднего”, чтобы видеть хвосты и реальный пользовательский опыт

---
## cluster
- aliases:: кластер Elasticsearch; ES cluster
- mean:: Набор связанных node Elasticsearch, которые совместно хранят данные и обслуживают запросы как единая система.​

---
## node
- aliases:: нода; узел Elasticsearch; сервер Elasticsearch
- mean:: Одна запущенная инстанция Elasticsearch (процесс/сервер), входящая в cluster и хранящая часть данных (shards) и/или выполняющая запросы.​

---
## shard
- aliases:: шард; shard; primary shard
- mean:: “Кусок” индекса: отдельная часть данных index, которая распределяется по node; бывает primary (основной) и replica (копия).​

---
## replica
- aliases:: реплика; replica shard
- mean:: Копия primary shard, размещаемая на другой node для отказоустойчивости и увеличения пропускной способности чтения (поиск/GET).

---
## [[ITSM]]
- aliases:: **Information Technology Service Management**
- mean:: подход (набор практик и процессов) к управлению ИТ как **сервисом**: проектировать, предоставлять, поддерживать и улучшать ИТ‑услуги так, чтобы они соответствовали потребностям бизнеса и пользователей

---
## [[ITIL]]
- aliases:: **Information Technology Infrastructure Library**
- mean:: наиболее распространённый фреймворк “лучших практик” внутри ITSM, который описывает, как эти процессы/практики выстроить




