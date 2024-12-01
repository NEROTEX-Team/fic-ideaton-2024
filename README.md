# Архитектура высоконагруженного распределенного приложения

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

## Список источников

1. [Diasoft Q - Продукты](https://q.diasoft.ru/products/)