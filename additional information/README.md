# Additional Information (Дополнительные сведения)

## Основы виртуализации:
Виртуализация – это сокрытие конкретной реализации за универсальным стандартизованным методом обращения к ресурсам. Иными словами, это создание абстракции над аппаратным обеспечением

### Существует много видов виртуализации, однако можно выделить три основных:

#### Аппаратная виртуализация:
Позволяет создавать независимые и изолированные друг от друга виртуальные компьютеры с помощью программной имитации ресурсов (процессора, памяти, сети, диска и др.) физического сервера. Физический сервер называют хостовой машиной (хостом), виртуальные компьютеры – виртуальными машинами, ВМ (иногда их также называют гостями). Программное обеспечение, которое создает виртуальные машины и управляет ими, называют гипервизором (а также виртуальным монитором или контрольной программой – вспомните CP-40 из начала статьи). На практике на виртуальных машинах могут использоваться разные ОС для разных целей – например, Windows Server под контроллер домена Active Directory и Debian под веб-сервер NGINX

#### Виртуализация рабочих столов:
Позволяет отделить логический рабочий стол (набор пользовательских программ, работающий под ОС) от физической инфраструктуры (например, персональных компьютеров). Одной из наиболее распространенных форм виртуализации рабочих столов является VDI (Virtual Desktop Infrastructure) – инфраструктура виртуальных рабочих столов. Каждый пользователь VDI имеет программную имитацию ОС с необходимым набором программ на физическом сервере под управлением гипервизора и может подключаться к ней по сети. На практике VDI может использоваться для работы большого количества сотрудников на «удаленке» для того, чтобы не закупать им отдельные рабочии станции и управлять инфраструктурой централизованно

#### Виртуализация на уровне ОС (контейнеризация):
Позволяет запускать программное обеспечение в изолированных на уровне операционной системы пространствах. Наиболее распространенной формой виртуализации на уровне ОС являются контейнеры (например, Docker). Контейнеры более легковесны, чем виртуальные машины, так как они опираются на функционал ядра ОС и им не требуется взаимодействовать с аппаратным обеспечением. На практике контейнеры представляют из себя изолированную среду для запуска любого приложения со всеми его зависимостями и настройками

#### Виртуализация серверов:
Виртуализация серверов – это процесс разделения физического сервера на несколько уникальных и изолированных виртуальных машин (серверов) с помощью программного обеспечения (гипервизора). На каждом виртуальном сервере могут независимо выполняться собственные операционные системы

#### Виртуализация серверов позволяет:

1. Оптимизировать затраты на покупку серверного оборудования. Под каждую задачу выделяется виртуальный сервер с необходимым количеством ресурсов (ЦПУ, ОЗУ и др.), простои оборудования минимизируются
2. Упростить сопровождение инфраструктуры. Создание, удаление или обслуживание виртуальной машины, как правило, проще и быстрее, чем аналогичные операции с физическим сервером
3. Повысить отказоустойчивость инфраструктуры. Виртуальные машины изолированы друг от друга, программный сбой на одной них не приведет к потере работоспособности сервисов и приложений на остальных

Гипервизор обеспечивает изолированную среду выполнения для каждой виртуальной машины, а также управляет доступом ВМ и гостевых ОС к аппаратным ресурсам физического сервера

Говоря простыми словами, гипервизор обеспечивает параллельное и независимое  функционирование нескольких операционных систем на одном компьютере

#### В классическом подходе гипервизоры группируются по двум типам:

1. Гипервизоры первого типа запускаются непосредственно на аппаратном обеспечении компьютера («железе»)
2. Гипервизорам второго типа для работы необходимо наличие хостовой операционной системы

В последние несколько лет классическая классификация претерпевает изменения – добавился гибридный тип гипервизоров (тип 1.5), который сочетает характеристики первого и второго типов

### Гипервизоры первого типа (native, bare-metal):
Гипервизор первого типа выполняется как контрольная программа непосредственно на аппаратной части компьютера и не требует ОС общего назначения. В данной архитектуре гипервизор управляет распределением вычислительных ресурсов и сам контролирует все обращения виртуальных машин к устройствам

Гипервизоры первого типа показывают высокое быстродействие, однако обладают очевидным недостатком – необходимость поддерживать драйверы устройств приводит к сужению списка совместимого аппаратного обеспечения

### Гипервизоры второго типа (hosted):
Гипервизор второго типа выполняется поверх хостовой операционной системы (как правило Linux). Он управляет гостевыми операционными системами, в то время как эмуляцией и управлением физическими ресурсами занимается хостовая ОС

Гипервизоры второго типа показывают меньшее относительно гипервизоров первого типа быстродействие и реже используются в промышленной эксплуатации, однако отлично подходят для задач обучения и разработки ПО

### Кластер узлов виртуализации:
Виртуализация на одном физическом сервере дает неплохие результаты, однако имеет ряд очевидных недостатков – например, в случае отказа этого сервера построенная инфраструктура полностью теряет работоспособность. По-настоящему ярко технология виртуализации раскрывается только при создании кластера из нескольких физических хостов. Кластер узлов виртуализации (или просто кластер виртуализации) – это объединение группы физических серверов, которое представляется конечным потребителям как общий вычислительный ресурс с единой точкой управления. При этом виртуальные машины запускаются на разных физических серверах и могут перемещаться (мигрировать) между ними, что обеспечивает высокую доступность (High Availability, HA) и гибкое распределение ресурсов (нагрузки)



## Основы контейнеризации:

#### Контейнеризация (виртуализация на уровне ОС):
Технология, которая позволяет запускать программное обеспечение в изолированных на уровне операционной системы пространствах. Контейнеры являются наиболее распространенной формой виртуализации на уровне ОС. С помощью контейнеров можно запустить несколько приложений на одном сервере (хостовой машине), изолируя их друг от друга

Процесс, запущенный в контейнере, выполняется внутри операционной системы хостовой машины, но при этом он изолирован от остальных процессов. Для самого процесса это вылядит так, будто он единственный работает в системе

### Механизмы изоляции контейнеров:

Изоляция процессов в контейнерах осуществляется благодаря двум механизмам ядра Linux – пространствам имен (namespaces) и контрольным группам (cgroups)

Пространства имен гарантируют, что процесс будет работать с собственным представлением системы

### Существует несколько типов пространств имен:

1. файловая система (mount, mnt) – изолирует файловую систему
2. UTS (UNIX Time-Sharing, uts) – изолирует хостнейм и доменное имя
3. идентификатор процессов (process identifier, pid) – изолирует процессы
4. сеть (network, net) – изолирует сетевые интерфейсы
5. межпроцессное взаимодействие (ipc) – изолирует конкурирующее взаимодействие процессами
6. пользовательские идентификаторы (user) – изолирует ID пользователей и групп

Процесс принадлежит не одному пространству имен, а одному пространству имен каждого типа

Контрольные группы гарантируют, что процесс не будет конкурировать за ресурсы, зарезервированные за другими процессами. Они ограничивают (контролируют) объем ресурсов, который процесс может потреблять – ЦПУ, ОЗУ, пропускную способность сети и др

## Docker: 

### Основные понятия:

#### Container image (образ):
Файл, в который упаковано приложение и его среда. Он содержит файловую систему, которая будет доступна приложению, и другие метаданные (например команды, которые должны быть выполнены при запуске контейнера). Образы контейнеров состоят из слоев (как правило один слой – одна инструкция). Разные образы могут содержать одни и те же слои, поскольку каждый слой надстроен поверх другого образа, а два разных образа могут использовать один и тот же родительский образ в качестве основы. Образы хранятся в Registry Server (реестре) и версионируются с помощью tag (тегов). Если тег не указан, то по умолчанию используется latest

``Примеры: Ubuntu, Postgres, NGINX.``

#### Registry Server (реестр, хранилище):
Это репозиторий, в котором хранятся образы. После создания образа на локальном компьютере его можно отправить (push) в хранилище, а затем извлечь (pull) на другом компьютере и запустить его там. Существуют общедоступные и закрытые реестры образов 

``Примеры: Docker Hub (репозитории docker.io)``

#### Container (контейнер):
Это экземпляр образа контейнера. Выполняемый контейнер – это запущенный процесс, изолированный от других процессов на сервере и ограниченный выделенным объемом ресурсов (ЦПУ, ОЗУ, диска и др.). Выполняемый контейнер сохраняет все слои образа с доступом на чтение и формирует сверху свой исполняемый слой с доступом на запись

#### Container Engine (движок контейнеризации):
Это программная платформа для упаковки, распространения и выполнения приложений, которая скачивает образы и с пользовательской точки зрения запускает контейнеры (на самом деле за создание и запуск контейнеров отвечает Container Runtime)

``Примеры: Docker, Podman``

#### Container Runtime (среда выполнения контейнеров):
Программный компонент для создания и запуска контейнеров

``Примеры: runc (инструмент командной строки, основанный на упоминавшейся выше библиотеке libcontainer), crun``

#### Host (хост):
Сервер, на котором запущен Container Engine и выполняются контейнеры

## Прокси:
https://www.oslogic.ru/knowledge/1013/chem-otlichaetsya-pryamoj-proksi-ot-obratnogo-proksi/

### Прокси-сервер:
Это компьютер, выполняющий роль посредника между пользователем и целевым сервером

#### Используется для:
Обеспечения безопасности, повышения производительности сети, доступа к "удаленным" ресурсам

### Обратный прокси-сервер:
Скрывается не IP клиента, а IP сервера, на который отправляется запрос.

#### Используется для:
Того, чтобы контролировать доступ к серверу и ограничивать неконтролируемый доступ к БД, а также для снижения трафика за счет кеширования информации  