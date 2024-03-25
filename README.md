# Prototype of Linux Monitoring Utility

Данный проект представляет собой программу, которая выдаёт список неиспользуемых пакетов на системе. Главная задача этого приложения состоит в том, что оно ставится на систему, работает какое-то время, после этого выдаёт список пакетов, к файлам которых не было ни одного обращения.

## Проект ##

Главная цель приложения – это возможность проанализировать систему на наличие неиспользуемых пакетов, при этом не сильно нагружая саму систему, давая пользователю возможность выполнять свои задачи параллельно с работой приложения.

В приложении изначально происходит сбор используемых файлов с помощью скрипта на языке BPFtrace. Затем происходит поиск пакетов, в которые входят используемые файлы. Далее, собирается полный список всех пакетов на системе, из которого вычленяется список используемых пакетов, что в итоге дает список неиспользуемых пакетов на системе.

BPFtrace-скрипты отслеживают системные вызовы, прописанные в конфигурационном файле в каталоге config, а также у пользователя есть возможность изменить системные вызовы, которые будут отслеживаться, задав собственный конфигурационный файл в грамматике yaml.

## Стек проекта ##

В этом проекте используется:

1. Приложение написано на языке Golang
2. В качестве инструмента для сбора используемых файлов используются скрипты на языке BPFtrace

## Приступая к работе ##

Это руководство по началу работы с этим проектом и установке зависимостей, необходимых для запуска этого проекта локально.

### Требования ###

1. Приложение предназначено для систем на основе GNU/Linux
2. BPFtrace ???
3. Запуск приложения должен осуществляется от пользователя root ???

### Флаги ###

Следующие флаги доступны для облегчения настройки проекта:

- `-t` задает время работы одного скрипта bpftrace в секундах, дефолтное значение – 3600 секунд. Время работы одного bpftrace-скрипта не должно быть больше времени работы всей программы! ???
- `-T` задает время работы всей программы в секундах, дефолтное значение – 86400 секунд. Время работы всей программы не должно быть меньше времени работы одного bpftrace-скрипта! ???
- `-c` задает путь к конфигурационному файлу .yaml для задания требуемых системных вызовов для отслеживания, дефолтное значение - "../configs/defaultConf.yaml"
- `-o` задает путь для выходных отчетов, дефолтное значение – директория, откуда запускается проект

### Конфигурация ###

Для настройки приложения используется config-файл, расположенный в каталоге `/internal/config` проекта.

## Структура проекта ##

`/cmd`

Основной файл проекта – main.go.

`/internal`

Внутренний код приложения. Здесь располагаются файлы для всех слоев программы.

`/docs`

Проектная документация. В этом каталоге располагаются отчеты по различным темам, которые были написаны в ходе разработки этого приложения.

`/configs`

Шаблоны файлов конфигураций и файлы настроек по-умолчанию. На данный момент там располагается дефолтный файл конфигурации с системными вызовами для BPFtrace-скрипта.

`/scripts`

Скрипты для выполнения различных операций сборки, установки, анализа и т.п. операций. Будут добавлены позже.

## Структура кода ##

Дизайн проекта содержит несколько слоев, каждый из которых выполняет свою функцию.

### Слои: ###

1. Парсинг bpftrace-скриптов
2. Создание bpftrace-скриптов
3. Конфигурация
4. Работа с утилитой lsof
5. Работа с утилитой rpm
6. Исполнение задач

**Конфигурация**

В этом слое производится конфигурация приложения. Происходит обработка конфигурационного файла с системными вызовами и значений ключей командной строки.

**Создание bpftrace-скриптов**

Генерируются bpftrace-скрипты для отслеживания используемых файлов по заданным системным вызовам. Подробнее про системные вызовы и bpftrace-скрипты описано в каталоге `/docs/utilities`.

**Парсинг bpftrace-скриптов**

Результаты работы bpftrace-скрипта преобразуются и сохраняются в файл .txt.

**Работа с утилитой lsof**

С помощью утилиты lsof осуществляется сбор данных о файлах, которые были открыты на время запуска приложения. Подробнее про утилиту lsof описано в каталоге `/docs/utilities`.

**Работа с утилитой rpm**

С помощью утилиты rpm осуществляется сбор всех пакетов на системе и переход от используемых файлов к их пакетам. Также в этом слое происходит вычленение списка используемых пакетов из полного списка всех пакетов для получения итогового списка неиспользуемых пакетов.

**Исполнение задач**

Осуществляется запуск bpftrace-скриптов на заданное количество секунд.

## Обработка ошибок ##

В этом проекте ошибки возвращаются вызывающей стороне.
