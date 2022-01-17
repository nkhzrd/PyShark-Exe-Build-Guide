# PyShark Exe Build Guide
##### Как собрать скрипт Python в exe, если вы используете модуль PyShark / How to build Python Script to exe if you are using PyShark module

Приветствую всех, здесь я покажу вам, как собрать код на языке Python в exe файл.
Лично столкнулся с проблемой при решении задачи по обработке pcap-файла. Считаю, что может быть полезным для программистов, которые встретят подобную проблему.

(Hi everyone, here I will show you how to compile python code into exe file.
I personally encountered a problem when solving the task of processing a pcap file. I think that it can be useful for programmers who meet a similar problem.)


## Порядок действий:

Что нам понадобится (What we need): 
- код, написанный на языке программирования Python (code written in the Python programming language)
- установленная библиотека PyInstaller (installed PyInstaller module)
```c
pip install PyInstaller
```
Открываем наш скрипт и добавляем следующие импорты
(Open our script and add the following imports):
```c
from py import _std
from py import __metainfo
from py import _builtin
from py import _error
from py import _xmlgen
from py import _code
from py import _io
from py import _log
from py import _path
from py import _process
from py import _path
from py import _vendored_packages
```

Переходим в папку со скриптом и выполняем следующую команду в терминале
(Go to the folder with the script and run the following command in the terminal):
```c
pyinstaller <name-of-script>.py
```

Далее, после сборки появляется файл <name-of-script>.spec.
В нём необходимо найти переменную hiddenimports и записать в неё следующее значение (Further, after the assembly, the <name-of-script>.spec file appears.
In it, you need to find the hiddenimports variable and write the following value into it):
```c
hiddenimports=['py._path.local','py._vendored_packages.iniconfig','pyshark.config']
```
  
После внесения изменений, необходимо вновь выполнить команду в терминале (After making changes, you need to run the command again in the terminal):
  ```c
  pyinstaller <name-of-script>.spec
  ```
 Терминал выдаст такое предложение, соглашаемся с ним (пересборка проекта) (Terminal will give you such, agreeing with him the proposal (rebuilding the project)). Press (Y):
  ```c
  WARNING: The output directory <path-to-script> and ALL ITS CONTENTS will be REMOVED! Continue? (y/N)
  ```
  
  Далее, переходим в каталог dist в директории, где находится проект, и копируем туда папку pyshark. (Папка находится в приложенном архиве).
  В файле config.ini необходимо изменить путь до tcpdump и tshark, если они были выставлены не по умолчанию при установке. (Next, go to the dist directory in the directory where   the project is located and copy the pyshark folder there. (The folder is in the attached archive).
  In the config.ini file, you need to change the path to tcpdump and tshark if they were not set by default during installation.)
  ```c
  [tshark]
# Specify the path to the tshark executable.
# If the configured path does not exist, these locations will be searched:
# (Linux): /usr/bin/tshark
# (Linux): /usr/sbin/tshark
# (Linux): /usr/lib/tshark/tshark
# (Linux): /usr/local/bin/tshark
# (Windows): %ProgramFiles%\Wireshark\tshark.exe
# (Windows): %ProgramFiles(x86)%\Wireshark\tshark.exe
tshark_path = C:\Program Files(x86)\Wireshark\tshark.exe

[dumpcap]
dumpcap_path = C:\Program Files(x86)\Wireshark\dumpcap.exe
```
Далее, запускаем exe файл из папки (Next, run the exe file from the folder):
```c
./dist/<name-of-script>/<name-of-script>.exe
```
[pyshark.zip](https://github.com/nkhzrd/Python-Pyshark-Exe-Guide/files/7882749/pyshark.zip)
  

## AUTHOR
    Vladislav Kotletkin (t.me/mrcnsldr)
    Vitaliy Bondarenko (t.me/medoook)

  
