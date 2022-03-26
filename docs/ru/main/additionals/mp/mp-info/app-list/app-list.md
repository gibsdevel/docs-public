Магазин приложений VK Cloud Solutions включает ряд решений для комфортной разработки.

**Docker** - программное обеспечение для автоматизации развертывания и управления приложениями в средах с поддержкой контейнеризации. Данное ПО позволяет упаковать приложение со всем его окружением и зависимостями в контейнер, который может быть перенесен на любую Linux-систему с поддержкой cgroups в ядре, а также предоставляет среду по управлению контейнерами.

Маркетплейс VK CS предлагает две составляющие для корректной и удобной работы с приложениями - само программное обеспечение Docker CE (Community Edition) и Docker Registry - серверное приложение для размещения и распространения неограниченного количества публичных docker-образов.

Docker Registry может использоваться для контроля над местом хранения и распространением образов, а также для интеграции хранения и распространения образов в процессе разработки.

**ELK** - это аббревиатура из названий трех продуктов: Elasticsearch, Logstash, kibana. Эти продукты в определенный момент времени стали принадлежать одной компании и развиваться в одном направлении.

Elasticsearch— это собственно механизм индексирования и хранения полученной информации, а также полнотекстового поиска по ней. Он основан на библиотеке Apache Lucene и, по сути, является NoSQL database решением. Главная задача этого инструмента — организация быстрого и гибкого поиска по полученным данным. Для ее решения имеется возможность выбора анализаторов текста, функционал «нечеткого поиска», поддерживается поиск по информации на восточных языках (корейский, китайский, японский). Работа с информацией происходит с помощью REST API, который позволяет добавлять, просматривать, модифицировать и удалять данные. Однако в случае использования ELK этот вопрос остается внутри «черной коробочки», поскольку у нас есть уже выше описанный Logstash и Kibana.

Logstash— это инструмент получения, преобразования и сохранения данных в общем хранилище. Его первой задачей является прием данных в каком-либо виде: из файла, базы данных, логов или информационных каналов. Далее полученная информация может модифицироваться с помощью фильтров, например, единая строка может быть разбита на поля, могут добавляться или изменяться данные, несколько строк могут агрегироваться и т.п. Обработанная информация посылается в системы — потребители этой информации. Говоря о связке ELK, потребителем информации будет Elasticsearch, однако возможны другие варианты, например системы мониторинга и управления (Nagios, Jira и др.), системы хранения информации (Google Cloud Storage, syslog и др.), файлы на диске. Возможен даже запуск команды при получении особого набора данных.

Kibana— это user friendly интерфейс, для Elasticsearch, который имеет большое количество возможностей по поиску данных в дебрях индексов Elasticsearch и отображению этих данных в удобочитаемых видах таблиц, графиков и диаграмм.

Сейчас ELK мощный инструмент сбора и аналитики информации.

VK Cloud Solutions позволяет создать либо одну виртуальную машину со стеком ELK, либо комплекс из двух инстанов ELK Multi Instance - elasticsearch instance и gateway instance.

**Комплекты для разработки приложений**
---------------------------------------

**GitLab CE** (Community Edition) - это система управления репозиториями Git и совместной разработки проектов с открытым исходным кодом.

Минимальные требования для установки GitLab - 4 CPU и 4 RAM для поддержки дот 500 пользователей.

**Sonatype Nexus** - приватный maven репозиторий, который выполняет следующие задачи: проксирование библиотек для быстрого доступа к ним (целесообразно, если nexus находится в локальной сети - библиотеки единожды скачиваются в nexus из разных репозиториев и далее хранятся там); релиз библиотек разных версий.

В отличие от Nexus 2, Nexus 3 обладает функцией Docker Registry.

**Apache Tomcat** - контейнер сервлетов и веб-сервер с открытыми исходным кодом, поддерживающий множество крупномасштабных приложений в самых разных отраслях и организациях.

Реализует спецификацию сервлетов, спецификацию JavaServerPages и JavaServerFaces. Позволяет запускать веб-приложения и содержит ряд программ для самоконфигурирования.

**Wordpress**\- система управления содержимым сайта с открытым исходным кодом. Wordpress использует PHP и MySQL, которые поддерживаются практически всеми хостинг провайдерами. Сфера применения - от блогов до сложных новостных ресурсов. Встроенная система "тем" и "плагинов" вместе с удачной архитектурой позволяет конструировать проекты широкой функциональной сложности.

**Jenkins** - программная система с открытым исходным кодом на Java, предназначенная для обеспечения процесса непрерывной интеграции программного обеспечения. Jenkins позволяет автоматизировать часть процесса разработки ПО, в котором необязательно участие человека, обеспечивая функции непрерывной интеграции. Поддерживает инструменты системы управления версиями, включая AccuRev, CVS, Subversion, Git, Mercurial, Perforce, Clearcase, RTC. Может собирать проекты с использованием Apache Ant и Apache Maven, а также выполнять произвольные сценарии оболочки и пакетные файлы Windows. Сборка может быть запущена разными способами, например, по событию фиксации изменений в системе управления версиями, по расписанию, по запросу на определенный URL, после завершения другой сборки в очереди.

**Стеки для разработчиков**
---------------------------

LAMP stack - комплекс серверного программного обеспечения. Включает в себя следующие компоненты:

*   LEMP stack
*   MEAN stack
*   Мониторинг
*   Prometheus Kit