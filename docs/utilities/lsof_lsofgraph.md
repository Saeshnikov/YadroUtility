Утилиты **lsof** и **lsofgraph**.

**lsof** (от англ. LiSt of Open Files) — утилита, служащая для вывода информации о том, какие файлы используются теми или иными процессами.

Вывод команды lsof без опций:

Имя процесса; ID процесса; пользователь, которому принадлежит этот процесс; номер файлового дискриптора; тип файла; устройство, на котором и расположен этот файл; размер устройства; имя устройства, которое совпадает с его расположением.

Lsof используется в файловой системе, чтобы определить, кто использует какие-либо файлы в этой файловой системе. Вы можете запустить команду lsof в файловой системе Linux, и выходные данные идентифицируют владельца и информацию о процессах для процессов, использующих файл, как показано в следующих выходных данных.

- sudo lsof: Вывод списка всех открытых файлов
- lsof -u user: Вывод списка всех файлов, открытых пользователям
- lsof -i: Вывод списка открытых сетевых сокетов

Опции:

- **-b** : заставляет lsof избегать функций ядра, которые могут блокировать -lstat(2), readlink(2) и stat(2).
- **-c**  **c** : выбирает список файлов для процессов, выполняющих команду, начинающуюся с символов c. Можно указать несколько команд, используя несколько опций -c.
- **+c w** : определяет максимальное количество начальных символов имени, предоставляемого диалектом UNIX, команды UNIX, связанной с процессом, которое должно быть напечатано в столбце COMMAND. (Значение lsof по умолчанию равно девяти.)
- **-C** : отключает отображение любых компонентов с именами путей из кэша имен ядра.
- **+d s** : заставляет lsof выполнять поиск всех открытых экземпляров каталога s, а также файлов и каталогов, которые он содержит, на его верхнем уровне.
- **-d s** : указывает список файловых дескрипторов (FD), которые следует исключить из выходного списка или включить в него. Файловые дескрипторы указаны в наборе s, разделенных запятыми
- **+D D** : заставляет lsof выполнять поиск всех открытых экземпляров каталога D и всех файлов и каталогов, которые он содержит, на всю глубину.
- **+|-e s** : освобождает файловую систему, путь к которой равен s, от выполнения вызовов функций ядра, которые могут блокироваться. Опция +e освобождает stat(2), lstat(2) и большинство вызовов функций ядра readlink(2). Параметр -e исключает только вызовы функций ядра stat(2) и lstat(2).
- **+|-E** : +E указывает, что файлы Linux pipe, Linux UNIX socket и Linux pseudoterminal должны отображаться с информацией о конечной точке, и файлы конечных точек также должны отображаться. -E указывает, что файлы Linux pipe и Linux UNIX socket должны отображаться с информацией о конечной точке, но не файлы конечных точек.
- **+|-f [cfgGn]**: f сам по себе разъясняет, как следует интерпретировать аргументы имени пути. Если за ним следуют c, f, g, G или n в любой комбинации, это указывает на то, что список информации о файловой структуре ядра должен быть включен (`+') или запрещен (`-').
- **-F f** : задает список символов f, который выбирает поля, которые будут выводиться для обработки другой программой, и символ, который завершает каждое поле вывода. Каждое поле, которое будет выводиться, задается одним символом в f.
- **-g [s]**: исключает или выбирает список файлов для процессов, необязательные идентификационные номера групп процессов (PGID) которых находятся в наборе s, разделенных запятыми
- **-i [i]**: выбирает список файлов, любой из интернет-адресов которых совпадает с адресом, указанным в i. Если адрес не указан, этот параметр выбирает список всех сетевых файлов Интернета и x.25 (HP-UX).
- **-K k** : выбирает список задач (потоков) процессов на диалектах, где поддерживается отчетность по задачам (потокам).
- **-k k** : указывает файл списка имен ядра k вместо /vmunix, /mach и т.д.
- **-l** : запрещает преобразование идентификационных номеров пользователей в имена для входа. Это также полезно, когда поиск имени для входа работает неправильно или медленно.
- **+|-L [l]**: включает (`+') или отключает (`-') отображение количества ссылок на файлы там, где они доступны - например, они недоступны для сокетов или большинства FIFO и каналов.
- **+|-m m** : указывает альтернативный файл памяти ядра или активирует обработку дополнения таблицы монтирования.
- **+|-M** : включает (+) или отключает (-) отчетность о регистрациях portmapper для локальных портов TCP, UDP и UDPLITE, где поддерживается сопоставление портов.
- **-n** : запрещает преобразование сетевых номеров в имена хостов для сетевых файлов. Запрещение преобразования может ускорить запуск lsof. Это также полезно, когда поиск имени хоста не работает должным образом.
- **-N** : выбирает список файлов NFS.
- **-o** : предписывает lsof постоянно отображать смещение файла. Это приводит к изменению заголовка выходного столбца SIZE/OFF на OFFSET.
- **-o o** : определяет количество десятичных цифр (o), которые должны быть напечатаны после `0t" для смещения файла перед переключением формы на `0x..."
- **-O** : направляет lsof на обход стратегии, которую он использует, чтобы избежать блокировки некоторыми операциями ядра, т.е. выполнения их в разветвленных дочерних процессах.
- **-p s** : исключает или выбирает список файлов для процессов, необязательные идентификационные номера процессов (PID) которых находятся в наборе s, разделенных запятыми
- **-P** : запрещает преобразование номеров портов в имена портов для сетевых файлов.
- **+|-r [t[m\<fmt\>]]**: переводит lsof в режим повтора. Там lsof перечисляет открытые файлы, выбранные другими параметрами, задерживает t секунд (по умолчанию 15), затем повторяет перечисление, задерживая и выводя список повторно, пока не остановится по условию, определяемому префиксом к опции.
- **-R** : направляет lsof на перечисление идентификационного номера родительского процесса в столбце PPID.
- **-s [p:s]**: только s указывает lsof на постоянное отображение размера файла. Это приводит к изменению заголовка столбца вывода SIZE/OFF на SIZE. Если файл не имеет размера, ничего не отображается. Необязательная форма -s p:s доступна только для выбранных диалектов и только тогда, когда она указана в выходных данных справки -h или -?.
- **-S [t]**: указывает необязательное значение времени ожидания в секундах для функций ядра - lstat(2), readlink(2) и stat(2), которые в противном случае могли бы привести к взаимоблокировке. Минимальное значение для t равно двум; по умолчанию 15
- **-T [t]**: управляет передачей некоторой информации TCP/TPI, также сообщаемой netstat(1), после сетевых адресов. При обычном выводе информация выводится в круглых скобках, каждый элемент, за исключением названия состояния TCP или TPI, идентифицируется ключевым словом, за которым следует `=', отделенный от других одним пробелом
- **-t** : указывает, что lsof должен выдавать сжатый вывод только с идентификаторами процессов и без заголовка - например, чтобы вывод можно было передать по конвейеру для завершения (1). -t выбирает опцию -w.
- **-u s** : выбирает список файлов для пользователя, чьи имена для входа в систему или идентификационные номера пользователей указаны в наборе s, разделенных запятыми
- **-U** : выбирает список файлов доменных сокетов UNIX.
- **-v** : выбирает список информации о версии lsof, включая: номер редакции; когда был создан двоичный файл lsof; кто создал двоичный файл и где; имя компилятора, используемого для создания двоичного файла lsof; номер версии компилятора, когда он легко доступен; флаги компилятора и загрузчика, используемые для создания двоичный файл lsof; и системная информация
- **-V** : указывает lsof на элементы, которые его попросили перечислить и которые не удалось найти - имена команд, имена файлов, интернет-адреса или файлы, имена для входа в систему, файлы NFS, PID, PGID и UID.
- **+|-w** : включает (+) или отключает (-) подавление предупреждающих сообщений.
- **-x [fl]**: может сопровождать опции +d и +Dd, чтобы направлять их обработку на пересечение символических ссылок и|или точек монтирования файловой системы, обнаруженных при сканировании каталога (+d) или дерева каталогов (+D).
- -X: это опция, зависящая от диалекта.

AIX: Эта опция IBM AIX RISC/System 6000 запрашивает отчет о выполненных ссылках на текстовые файлы и общие библиотеки.

Linux: Этот параметр Linux запрашивает, чтобы lsof пропускал представление информации обо всех открытых файлах TCP, UDP и UDPLITE IPv4 и IPv6.

Solaris 10 и выше: Этот параметр Solaris 10 и выше запрашивает отчет о кэшированных путях для файлов, которые были удалены - т.е. удалены с помощью rm(1) или unlink(2).

- **-z [z]**: указывает, как должна обрабатываться информация о зоне в Solaris 10 и более поздних версиях. Без следующего аргумента - например, БЕЗ z - параметр указывает, что имена зон должны быть указаны в столбце вывода ЗОНЫ.
- **-Z [Z]**: указывает, как должны обрабатываться контексты безопасности SELinux. Поддержка выходных символов It и поля 'Z' запрещена, когда SELinux отключен в запущенном ядре Linux.


У команды lsof есть опция –F, которая позволяет показывать вывод не в виде таблицы, а в виде отдельных строк. **lsofgraph** был написан под эту опцию -F. Небольшая утилита для преобразования выходных данных Unix lsof в график, показывающий взаимодействие между FIFO и UNIX-процессами.

lsofgraph был написан на Lua, и был переписан на python: lsofgraph-python.

Чтобы получить полную картину по системе, то надо использовать sudo.

Вывод результата:

Чтобы создать граф:

**sudo lsof -n -F | python lsofgraph.py | dot -Tjpg \> /tmp/a.jpg**

или

**sudo lsof -n -F | python lsofgraph.py | dot -T svg \> /tmp/a.svg**

Запуск c unflatten, чтобы график был более компактным:

**sudo lsof -n -F | python lsofgraph.py | unflatten -l 1 -c 6 | dot -T jpg \> /tmp/a.jpg**

или

**sudo lsof -n -F | python lsofgraph.py | unflatten -l 1 -c 6 | dot -T svg \> /tmp/a.svg**