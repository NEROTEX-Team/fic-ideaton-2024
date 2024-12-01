# Архитектура высоконагруженного распределенного приложения

- [Архитектура высоконагруженного распределенного приложения](#архитектура-высоконагруженного-распределенного-приложения)
  - [Описание](#описание)
  - [Задача](#задача)
  - [Анализ существующих платформ в Реестре российского программного обеспечения для решения задачи](#анализ-существующих-платформ-в-реестре-российского-программного-обеспечения-для-решения-задачи)
    - [SberTech: Platform V](#sbertech-platform-v)
    - [1C: Облачная платформа](#1c-облачная-платформа)
      - [Решение](#решение)
      - [Особенности](#особенности)
    - [Diasoft: Digital Q](#diasoft-digital-q)
      - [Предлагаемые решения](#предлагаемые-решения)
      - [Особенности](#особенности-1)
    - [Другие компании предоставляющие облачные инфраструктуры](#другие-компании-предоставляющие-облачные-инфраструктуры)
  - [Архитектура приложения](#архитектура-приложения)
    - [Локальное или геораспределенное?](#локальное-или-геораспределенное)
    - [Монолит или микросервисы?](#монолит-или-микросервисы)
      - [Выводы](#выводы)
    - [Схема архитектуры](#схема-архитектуры)
      - [Верхнеуровневая архитектура решения](#верхнеуровневая-архитектура-решения)
      - [Архитектура внутри ЦОДа](#архитектура-внутри-цода)
    - [Реализация бизнес-процессов для учетной многостадийной информационной системы](#реализация-бизнес-процессов-для-учетной-многостадийной-информационной-системы)
      - [Разработка собственного Workflow-движка](#разработка-собственного-workflow-движка)
      - [Использование готового BPM-систем и Workflow-движков](#использование-готового-bpm-систем-и-workflow-движков)
      - [Выводы](#выводы-1)
  - [Стек технологий](#стек-технологий)
    - [База данных](#база-данных)
    - [Очередь/брокер сообщений](#очередьброкер-сообщений)
    - [Кэш](#кэш)
    - [GUI](#gui)
    - [Оркестратор](#оркестратор)
    - [Выводы](#выводы-2)
  - [Рекомендации по обеспечению безопасности и защиты от кибератак](#рекомендации-по-обеспечению-безопасности-и-защиты-от-кибератак)
    - [Продуктовые решения](#продуктовые-решения)
      - [Yandex Smart Web Security](#yandex-smart-web-security)
      - [Kaspersky Anti Targeted Attack](#kaspersky-anti-targeted-attack)
  - [Список источников](#список-источников)

<details>
<summary>Задача</summary>

## Описание

Требуется разработать веб-приложение, работающее как в
приватной (внутренний контур), так и в публичной сети и
взаимодействующее посредством портаал с неограниченным
кругом пользователей, как напрямую, так и через ЕПГУ и СМЭВ
(https://info.gosuslugi.ru/docs/). Необходимо провести поиск
архитектурных решений для создания высоконагруженного
территориально-распределенного веб-приложения, способного
обслуживать не менее 100 000 одновременных пользователей.

## Задача

Разработать концептуальную архитектуру веб-приложения с
учетом требований к безопасноит, защитой от кибератак, масштабируемости и высокой на всей территории России.

</details>

## Анализ существующих платформ в Реестре российского программного обеспечения для решения задачи

### SberTech: Platform V

### 1C: Облачная платформа

#### Решение

В готовом облаке 1С пользователю предоставляется рабочее решение пространство
для удаленного доступа из любой точки мира к информационной базе 1С формата
клиент-сервер. Информационная база - это экземпляр одного прикладного решения
"1С: Предприятия 8". Экземпляр состоит из нескольких сущностей:

- Конфигурация (поставщика, базы данных, основная). Программа, которая исполняется.
- База данных. Пользовательский набор данных, который записывается и хранится
- Административная информация. Это, например, могут быть списки пользователей и их роли в проекте или какие-то подобные данные

Данное решение предоставляется облачными провайдерами типа Selectel, Reg.ru и т. д.

Доступные продукты 1С:

- 1С: Бахгалтерия 8 ПРОФ
- 1С: Бухгалртерия 8 КОРП
- 1С: Зарплата и упралвение персоналом ПРОФ
- 1С: Розница
- 1С: Управление нашей фирмой
- 1С: Управление торговлей
- 1С: Документооборот КОРП
- 1С: Документооборот ПРОФ
- 1С: Корпоративный инструментальный пакет 8
- 1С: Предприятие 8. ERP Управление предприятием 2

#### Особенности

- Есть ограничения по количеству лицензий (пользователей) на кластер
- Мощность кластера ограничена мощностями конкретного провайдера и предоставляемыми конфигурациями сервера
- Нельзя сразу сделать кластер с несколькими вычислительными серверами
- Предоставляется только платформа и решения на базе 1С
- Дорогостоящие лицензии

### Diasoft: Digital Q

#### Предлагаемые решения

Компания Diasoft предлагает различные группы платформ для разработки корпоративных решений. При разработке бизнес-приложений используется компонентный подход. Компонентами служат Packaged Business Capabilities (PBC) - приложения, решающие конкретные бизнес-задачи и состоящие из нескольких микросервисов:

- Производственные платформы:
  - [Digital Q.CMDB](https://q.diasoft.ru/products/proizvodstvennye-platformy/digital-q-cmdb/): ведение учета IT-компонентов - от физических стендов до установленных на них продуктов
  - [Digital Q.DevOps](https://q.diasoft.ru/products/proizvodstvennye-platformy/digital-q-devops/): набор инструментов и технологий для процессов непрерывной интеграции, тестирования, доставки и развертывания программных продуктов
  - [Digital Q.DevProfile](https://q.diasoft.ru/products/proizvodstvennye-platformy/digital-q-devprofile/): объединение разных в различных системах ведения проектов для получения отчетностей о работе
  - [Digital Q.Management](https://q.diasoft.ru/products/proizvodstvennye-platformy/digital-q-management/): система управления проектами и спринтами
  - [Digital Q.Tasks](https://q.diasoft.ru/products/proizvodstvennye-platformy/digital-q-tasks/): система управления задачами
  - [Digital Q.Teams](https://q.diasoft.ru/products/proizvodstvennye-platformy/digital-q-teams/): система управления командами
  - [Digital Q.VCS](https://q.diasoft.ru/products/proizvodstvennye-platformy/digital-q-vcs/): система управления исходным кодом
- Технологические платформы:
  - [Digital Q.Archer](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-archer/)
  - [Digital Q.BPM](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-bpm/)
  - [Digital Q.DataFlows](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-dataflows/)
  - [Digital Q.Environment](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-environment/)
  - [Digital Q.Health](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-health/)
  - [Digital Q.MessageHub](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-messagehub/)
  - [Digital Q.Palette](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-palette/)
  - [Digital Q.Renovation](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-renovation/)
  - [Digital Q.Sequrity](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-security/)
  - [Digital Q.Sensor](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-sensor/)
  - [Digital Q.Blockchain](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-blockchain/)
  - [Digital Q.Integration](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-integration/)
- Инфраструктурные платформы:
  - [Digital Q.DataBase](https://q.diasoft.ru/products/infrastrukturnye-platformy/digital-q-database/): платформа для хранения данных на основе PostgreSQL
  - [Digital Q.ELK](https://q.diasoft.ru/products/infrastrukturnye-platformy/digital-q-elk/): классический ElasticSearch, Logstash и Kibana стэк
  - [Digital Q.Kafka](https://q.diasoft.ru/products/infrastrukturnye-platformy/digital-q-kafka/): Apache Kafka
  - [Digital Q.Kubernetes](https://q.diasoft.ru/products/infrastrukturnye-platformy/digital-q-kubernetes/): импортозамещенный Kubernetes и Docker
- Кросс-продуктовые платформы:
  - [Digital Q.Knowledge](https://q.diasoft.ru/products/kross-produktovye-platformy/digital-q-knowledge/): создание систем знаний
  - [Digital Q.ProductCatalog](https://q.diasoft.ru/products/kross-produktovye-platformy/digital-q-productcatalog/): создание и управление каталога цифровых продуктов
  - [Digital Q.Reference](https://q.diasoft.ru/products/kross-produktovye-platformy/digital-q-reference/): единые справочники для сервисов и продуктов
  - [Digital Q.ClientCatalog](https://q.diasoft.ru/products/kross-produktovye-platformy/digital-q-clientcatalog/): единая централизованная база данных всех участников бизнес-процессов организации

#### Особенности

- В основе практически всех решений Diasoft лежат Open Source продукты, которые при желании можно использовать вне экосистемы Diasoft Digital Q - с одной стороны, это плюс, т. к. нет вендор лока, а с другой непонятно, за что именно платим
- Как и другие платформенные решения, здесь есть возможность доработки продуктов только путем настройки конфигурации.
- Есть Low Code инструменты, позволяющие быстро собрать решение с BPM

### Другие компании предоставляющие облачные инфраструктуры

За частую такие компании, как Яндекс, Seletel, Timeweb, Nexign предоставляют облачную инфраструктуру для проектов, которые можно развернуть с использованием MongoDB, PostgreSQL, ELK, Kubernetes и т. д.

Данные решения позволяют снизить затраты на обслуживание инфраструктуры, настройку, бэкапы, выбор ЦОДа, но также они не имеют как-либо специфических доработок.

## Архитектура приложения

### Локальное или геораспределенное?

Учитывая масштаб приложения и требования к времени восстановления и катастрофоустойчивости, географически распределенные кластеры представляются более подходящим выбором. Они обеспечат:

- Высокую доступность благодаря распределению ресурсов и автоматическому управлению отказами.
- Гибкость и масштабируемость, позволяя быстро реагировать на изменяющиеся потребности.
- Сокращение времени восстановления за счет автоматизированных процессов и распределения данных.

### Монолит или микросервисы?

Учитывая масштаб и сложность проекта, а также нагрузку в 100 000 одновременных пользователей, микросервисная архитектура представляется более подходящей по следующим причинам:

1. Масштабируемость:
   - Позволяет эффективно масштабировать только те компоненты, которые требуют дополнительных ресурсов.
   - Обеспечивает гибкое управление ресурсами под высокой нагрузкой.

2. Поддерживаемость и развитие:
   - Облегчает управление сложным приложением за счёт разделения на небольшие, независимые сервисы.
   - Улучшаются возможности для параллельной разработки и быстрого внедрения новых функций.

3. Отказоустойчивость и надёжность:
   - Повышает стабильность системы за счёт изоляции сервисов.
   - Позволяет системе оставаться работоспособной при сбоях отдельных компонентов.

4. Гибкость технологий:
   - Возможность использовать наиболее подходящие технологии и языки программирования для каждого сервиса.
   - Облегчает внедрение новых технологий без необходимости переписывать всё приложение.

Однако, необходимо также учитывать следующие факторы:

- Опыт команды:
  - Микросервисная архитектура требует высокой квалификации разработчиков и опытной команды DevOps.
  - Если команда не обладает достаточным опытом, риски увеличиваются.

- Инфраструктурные ресурсы:
  - Необходимо инвестировать в инфраструктуру и инструменты для управления микросервисами.
  - Включает в себя настройку CI/CD, мониторинга, логирования, безопасности и т.д.

- Временные и финансовые затраты:
  - На первоначальном этапе разработка микросервисов может потребовать больше времени и ресурсов.
  - Нужно оценить, оправданы ли дополнительные затраты для вашего проекта.

Если же команда ограничена в ресурсах или отсутствует необходимость в сложной масштабируемости, возможно, стоит начать с хорошо спроектированной монолитной архитектуры:

- Монолит может быть более подходящим, если:
  - Проект нуждается в быстром выходе на рынок.
  - Команда небольшая и обладает ограниченными ресурсами.
  - Планируется постепенное развитие с возможностью в будущем перейти на микросервисную архитектуру.

- Модульный монолит:
  - Можно разработать монолитное приложение с чётким разделением на модули.
  - Это облегчит возможное разделение на микросервисы в будущем.

#### Выводы

Рекомендуется:

- Провести тщательный анализ требований:
  - Оценить реальные потребности в масштабируемости и отказоустойчивости.
  - Определить критические компоненты системы и их нагрузку.

- Оценить возможности команды:
  - Убедиться, что команда обладает необходимыми знаниями и ресурсами для реализации микросервисной архитектуры.
  - При необходимости провести обучение или привлечь экспертов.

- Планировать на будущее:
  - Если выбираете монолитную архитектуру, спроектируйте её таким образом, чтобы в будущем можно было разделить приложение на микросервисы.
  - Используйте принципы модульности и чистой архитектуры.

### Схема архитектуры

#### Верхнеуровневая архитектура решения

![alt-image](https://www.plantuml.com/plantuml/svg/RP0n2zD05CVt-nIF36uTsgwbL1fmiWuTN8HokJkRuEKk91SKHAWjWav5SNPqBaenLE9dUFUDV4ayDT12Bo-_zylZtNzLELwwEjVmIDk4Q-2bI3EdXAjBnLpcj0ByX5T_yE-mfUV97_0NVkjgEY_-37HqpSOV2TtyiLSkGCVLloVKKklCXBQrX2ZUR242Ne4q5IkuUC7t2jOwKyPL7HP_ojSCw4TDuo1wgX9OFD2ySBPOzb-_LCbkKF_t7jiaquhK8hL63MRUio2_OM6HTRmXyRdcLJg8GXecR5vOqyzwQ5mMnq-s95LffhGSB4vOIbknLBtYUsiWmezumP_qR_rRR8Pq_0TiyFRCO4lyEyLpmXzumuQ6bTn8cm_3jELoHw5p8rJ9cB5IqRol-0K_JuUTh9p2YCy2dutmFE0v2mbEblsLA6TOJ4Akx5zmC27ZxtL2J7TQeUZfUENHMz_lDhwFP_VndB6LChBEzMy0)

#### Архитектура внутри ЦОДа

![alt-image](https://www.plantuml.com/plantuml/svg/bPFFQXin4CRlUeh1XznisEqrc3n0APGSUkb5qKwRa8raQxNf8HWSXv2MjFGFFVKGUYezhejDqmRd6MRUgBDQ1s_Q9YOo237wVPvFCxDRHT0-b0SvP3feWpQW1-tDxbv04qgFAko5784-y9XFwP8dDAVVFE4J7bC5iitvjOGMSlKUw0Sjv6OYuKkWRtH1dwbI0stszKk4JXFfm942MSOT39oLZD3PHd-8lkY0Bg1epX5gbdLPBVuaQQPTFfQCOqaaUujF7aId3w8VHNeKzs69PIsuuBF8pcd6Rq64r_ARyfkc5FGBDZVG7cBk1jWrkIimwyT_7FxzTFfA5Ktfciz4DWS-ePzqnUSHVkNy_lzAyIp6MqYo3aZN0Uqtjjrzf4eCLK0pEIoak-TyMilYkEpe0jlkRcAY-qwLL6S6IGFl9FT1wH9AxuDwlTuIitTu_K9NmXxpfEuCo9I-az6ieiXeitlBglIap6fD3QsGP1sGhWFQXRmPvMv_sVSXTEMyREijHEAhalvpqzXN8wLMXTdSUE7o37qVZc3qt3vnsqyVHnlM5SDSjULDH6sXpUHB_mC0)

### Реализация бизнес-процессов для учетной многостадийной информационной системы

Решение данной проблемы зависит от команды специалистов и ресурсов, которые у нас есть для реализации, поэтому необходимо рассмотреть два варианта.

#### Разработка собственного Workflow-движка

Преимущества:

1. **Полная кастомизация**: Вы сможете создать систему, полностью соответствующую специфическим потребностям и процессам вашей организации, учитывая все нюансы и особенности.
2. **Гибкость в изменениях**: Собственное решение позволяет быстро вносить изменения и дополнять функционал без ограничений, которые могут быть в сторонних продуктах.
3. **Контроль над технологией**: Полный контроль над кодовой базой облегчает управление безопасностью, производительностью и совместимостью системы.
4. **Интеграция с внутренними системами**: Легче обеспечить бесшовную интеграцию с существующими внутренними приложениями и сервисами без необходимости обходных путей или дополнительных адаптеров.
5. **Отсутствие лицензионных ограничений**: Нет необходимости оплачивать лицензии или зависеть от ценовой политики поставщиков сторонних решений.
6. **Конкурентное преимущество**: Уникальный инструмент может стать отличительным фактором, повышающим эффективность и адаптивность бизнеса.

Недостатки:

1. Высокие затраты на разработку: Создание с нуля требует значительных инвестиций времени и ресурсов, включая команду опытных разработчиков и экспертов по бизнес-процессам.
2. Длительный срок внедрения: Процесс разработки, тестирования и внедрения может занять гораздо больше времени по сравнению с приобретением готового решения.
3. Поддержка и обслуживание: Все задачи по обновлению, исправлению ошибок и обеспечению безопасности ложатся на ваши плечи, что увеличивает операционные расходы.
4. Риски качества и надежности: Без обширного тестирования и опыта есть вероятность возникновения ошибок и сбоев, которые могут негативно повлиять на бизнес-процессы.
5. Отсутствие внешней экспертизы и поддержки: В случае проблем нет возможности обратиться за помощью к сообществу или поставщику, как это бывает с коммерческими продуктами.
6. Ограничения в функциональности: Разработчики могут не предусмотреть все необходимые функции и возможности, которые уже присутствуют в зрелых рыночных решениях.
7. Технологическая устарелость: Без постоянного обновления и модернизации собственный движок может быстро устареть в быстро меняющейся технологической среде.
8. Сложности с масштабируемостью: Могут возникнуть трудности при необходимости масштабирования системы для поддержки роста бизнеса.

#### Использование готового BPM-систем и Workflow-движков

Преимущества:

- **Визуальное моделирование процессов**: Упрощает понимание и изменение бизнес-логики.
- **Гибкость**: Легко адаптировать процессы под меняющиеся требования.
- **Управление сложными процессами**: Специализированные инструменты лучше подходят для сложных многошаговых процессов.

Недостатки:

- **Дополнительная сложность**: Требует внедрения и поддержки дополнительного ПО.
- **Производительность**: Возможны накладные расходы на выполнение процессов через BPM.
- **Зависимость от решений третьих сторон**: Может возникнуть привязка к конкретному продукту или поставщику.

#### Выводы

Рекомендуется:

- Провести тщательный анализ требований к BPM системе:
  - Оценить реальные потребности в гибкости и масштабируемости
  - Оценить ресурсы, которые можно выделить на подсистему бизнес-процессов при разработке с нуля
  - Оценить возможности по интеграции готовых BPM систем (например, [Digital Q.BPM](https://q.diasoft.ru/products/tekhnologicheskie-platformy/digital-q-bpm/))

## Стек технологий

### База данных

### Очередь/брокер сообщений

### Кэш

### GUI

### Оркестратор

### Выводы

## Рекомендации по обеспечению безопасности и защиты от кибератак

Защита высоконагруженного и распределенного приложения требует комплексного подхода, учитывающего различные уровни инфраструктуры и приложения. Основные концепции и рекомендации по защите:

1. Сетевая безопасность:
   - Защита от DDoS-атак:
     - Используйте сервисы защиты от DDoS, предоставляемые облачными провайдерами или специализированными компаниями.
     - Реализуйте распределение нагрузки и балансировку трафика для снижения нагрузки на отдельные узлы.
   - Межсетевые экраны и системы обнаружения вторжений:
     - Установите и настройте межсетевые экраны (файрволы) для контроля входящего и исходящего трафика.
     - Внедрите системы обнаружения и предотвращения вторжений (IDS/IPS) для мониторинга подозрительной активности.

2. Безопасность приложения:
   - Безопасное кодирование:
     - Соблюдайте принципы безопасного кодирования, предотвращая распространенные уязвимости (OWASP Top 10).
     - Реализуйте проверку входных данных для защиты от инъекций и XSS-атак.
   - Обновления и патчи:
     - Регулярно обновляйте программное обеспечение и применяйте патчи для устранения известных уязвимостей.
     - Автоматизируйте процесс развертывания обновлений через системы CI/CD с встроенными проверками безопасности.

3. Аутентификация и авторизация:
   - Многофакторная аутентификация (MFA):
     - Введите MFA для доступа к критическим системам и данным.
     - Используйте современные протоколы аутентификации (OAuth 2.0, OpenID Connect).
   - Управление доступом на основе ролей (RBAC):
     - Определите и примените политики доступа на основе ролей и обязанностей пользователей.
     - Ограничьте права доступа принципом наименьших привилегий.

4. Защита данных:
   - Шифрование данных:
     - Используйте шифрование для данных в состоянии покоя (at rest) и при передаче (in transit).
     - Применяйте проверенные криптографические алгоритмы и протоколы (TLS 1.2/1.3).
   - Управление ключами:
     - Используйте защищенные хранилища ключей и секретов.
     - Регулярно обновляйте и ротируйте ключи шифрования.

5. Мониторинг и логирование
   - Централизованный сбор логов:
     - Собирайте и анализируйте логи из всех компонентов системы.
     - Используйте SIEM-системы для обнаружения аномалий и корреляции событий.
   - Микросервисный мониторинг:
     - Внедрите инструменты мониторинга для отслеживания состояния микросервисов и взаимодействия между ними.
     - Используйте распределенный трейсинг для детального анализа запросов.

6. Управление уязвимостями
   - Регулярные аудиты безопасности:
     - Проводите периодические сканирования уязвимостей и пентесты.
     - Используйте автоматизированные инструменты для статического и динамического анализа кода.
   - Управление конфигурацией:
     - Внедрите системы управления конфигурацией для обеспечения единообразия настроек.
     - Контролируйте изменения конфигураций и используйте принципы Immutable Infrastructure.

7. Реагирование на инциденты
   - План реагирования:
     - Разработайте и документируйте планы реагирования на инциденты безопасности.
     - Проведите обучение команды по реагированию на инциденты и регулярные учения.
   - Резервное копирование и восстановление:
     - Настройте регулярное резервное копирование критических данных.
     - Периодически проверяйте возможность восстановления из резервных копий.

8. Безопасность распределенной системы
   - Защищенные коммуникации между узлами:
     - Используйте защищенные каналы связи (VPN, TLS) между различными компонентами системы.
     - Реализуйте аутентификацию и авторизацию сервисов при обмене данными.
   - API безопасность:
     - Ограничьте доступ к API с помощью ключей и токенов доступа.
     - Реализуйте лимиты потребления (rate limiting) для предотвращения злоупотреблений.

9. Безопасность в процессе разработки и развертывания
   - DevSecOps практики:
     - Интегрируйте проверки безопасности на всех этапах разработки и развертывания.
     - Используйте инструменты для анализа кода на уязвимости в процессе CI/CD.
   - Контейнерная безопасность:
     - Обеспечьте безопасность контейнерных образов, используя минимальные базовые образы и регулярно обновляя их.
     - Используйте изолированные пространства выполнения (namespaces) и ограничения по ресурсам (cgroups).

10. Соответствие стандартам и нормативным требованиям
    - Соблюдение отраслевых стандартов:
      - Ориентируйтесь на общепринятые стандарты безопасности (ISO 27001, NIST, PCI DSS).
      - Регулярно проводите аудиты на соответствие требованиям регуляторов.
    - Политики и процедуры безопасности:
      - Разработайте и внедрите внутренние политики информационной безопасности.
      - Обучайте персонал принципам безопасности и повышайте осведомленность о киберугрозах.

### Продуктовые решения

#### Yandex Smart Web Security

Smart Web Security обеспечивает защиту от DDoS‑атак и ботов на уровне приложений, а также защиту от эксплуатации уязвимостей веб‑приложений с помощью встроенного WAF. В его основе — технология Smart Protection от Яндекса, которая больше десяти лет защищает сервисы компании.

SWS состоит из трех ключевых модулей:

1. Защита от DDoS-атак и ботов на уровне приложений (L7). Можно создать правила фильтрации трафика по IP‑адресам, географии, HTTP‑параметрам или содержимому запроса. 
2. Web Application Firewall (WAF). Он анализирует HTTP‑запросы по набору правил OWASP Core Rule Set и защищает от самых опасных уязвимостей из рейтинга OWASP TOP‑10.
3. Advanced Rate Limirer. Он ограничивает количество HTTP‑запросов за определённый промежуток времени — от секунды до часа.

#### Kaspersky Anti Targeted Attack

Для защиты инфраструктуры изнутри необходим постоянный мониторинг и анализ процессов происходящих внутри систем. Для этого может подойти решения типа [Kaspersky Anti Targeted Attack](https://www.kaspersky.ru/enterprise-security/anti-targeted-attack-platform). Они позволяют минимизировать последствия сложных угроз и целевых атак благодаря оперативному выявлению действий злоумышленников за счет:

- Наглядной визуализации, мониторинга и автоматизации процесса сбора и хранения данных, цифровых улик и вердиктов
- Сформированного процесса по анализу сетевого трафика и телеметрии с рабочих мест и автоматическому обнаружению угроз с помощью ряда передовых технологий
- Многоуровневого динамического анализа объектов в изолированной среде для эмуляции вредоносного ПО и противодействия методам обхода песочницы
- Постоянного взаимодействия с глобальной базой знаний об угрозах и автоматического получения информации о репутации файлов, интернет-ресурсов и ПО
- Встроенного сопоставления обнаруженной подозрительной активности с уникальными индикаторами атак (IoA) и базой знаний MITRE ATT&CK
- Сформированной на основе набора разрозненных событий общей картины инцидента и предоставления рекомендаций по расследованию и реагированию

## Список источников

1. [Diasoft Q - Продукты](https://q.diasoft.ru/products/)
2. [Продукты Platform V - автоматизация процессов от СберТеха](https://platformv.sbertech.ru/products)
3. [Архитектура платформы 1С:Предприятие](https://v8.1c.ru/platforma/oblachnye-tehnologii/)
4. [Selectel - Калькулятор 1С](https://my.selectel.ru/ones/calculator)
5. [Kaspersky Anti Targeted Attack](https://www.kaspersky.ru/enterprise-security/anti-targeted-attack-platform)
6. [Как защитить веб-приложения от кибератак с помощью Yandex Smart Web Security](https://yandex.cloud/ru/blog/posts/2024/11/smart-web-security-protection)
7. [Habr: Привет, я робот Макс! Как устроен цифровой ассистент Госуслуг](https://habr.com/ru/companies/rtlabs/articles/587034/)
8. [Как устроена самая современная платежная система в МИРе: архитектура и безопасность](https://nesmelov.com/images/portfolio/polygraphy/mir.pdf)
9. [Архитектура платёжной системы: МИРовой взгляд (митап Skillbox и Мир Plat.Form)](https://www.youtube.com/watch?v=Y-zXikF-zR4)
10. [Разработка и проектирование высоконагруженных систем (часть 1) / Олег Бунин (Онтико)](https://www.youtube.com/watch?v=KmIE5K6adus)
11. [Разработка и проектирование высоконагруженных систем (часть 2) / Олег Бунин (Онтико)](https://www.youtube.com/watch?v=sCm4qUw28y4)
12. [Разработка и проектирование высоконагруженных систем (часть 3) / Олег Бунин (Онтико)](https://www.youtube.com/watch?v=MG8-HmgOXlk)
13. [Сравнение микросервисной и монолитной архитектур](https://www.atlassian.com/ru/microservices/microservices-architecture/microservices-vs-monolith)
14. [В чем разница между монолитной архитектурой и архитектурой микросервисов?](https://aws.amazon.com/ru/compare/the-difference-between-monolithic-and-microservices-architecture/)