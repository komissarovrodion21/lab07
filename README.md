[![Build Status](https://travis-ci.org/komissarovrodion21/lab07.svg?branch=master)](https://travis-ci.org/komissarovrodion21/lab07)
## Laboratory work VII

Данная лабораторная работа посвещена изучению систем документирования исходного кода на примере **Doxygen**

```ShellSession
$ open https://www.stack.nl/~dimitri/doxygen/manual/index.html
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab07** на сервисе **GitHub**
- [x] 2. Выполнить инструкцию учебного материала
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial
Первоначальные настройки
```ShellSession
$ export GITHUB_USERNAME=komissarovrodion21 #устанавливаем значение переменнойGITHUB_USERNAME
$ alias edit=nano #Создаем алиас на редактирование файлов одним из редакторов(nano)
```
Проводим первоначальные настройки для соединения с репозиторием
```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab06 projects/lab07 #клонирование удаленного репозитория шестой й лабораторной в локальный каталог седьмой лабораторной
$ cd projects/lab07 #меняем директорию на lab07
$ git remote remove origin #отключаемся от удаленного репозитория шестой лабораторной
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab07 #подключаемся к удаленному репозиторию седьмой лабораторной
```
Начало работы с Doxygen
```ShellSession
$ mkdir docs #создаем каталог docs
$ doxygen -g docs/doxygen.conf #создаем файл doxygen.conf
$ cat docs/doxygen.conf | less #редактирование файла doxygen.conf
```
Работа с файлом doxygen.conf
```ShellSession
#Редактирование файла doxygen.conf при помощи команды sed и добавление информации в документацию doxygen.conf
$ sed -i 's/\(PROJECT_NAME.*=\).*$/\1 print/g' docs/doxygen.conf
$ sed -i 's/\(EXAMPLE_PATH.*=\).*$/\1 examples/g' docs/doxygen.conf
$ sed -i 's/\(INCLUDE_PATH.*=\).*$/\1 examples/g' docs/doxygen.conf
$ sed -i 's/\(EXTRACT_ALL.*=\).*$/\1 YES/g' docs/doxygen.conf
$ sed -i 's/\(INPUT *=\).*$/\1 README.md include/g' docs/doxygen.conf
$ sed -i 's/\(USE_MDFILE_AS_MAINPAGE.*=\).*$/\1 README.md/g' docs/doxygen.conf
$ sed -i 's/\(OUTPUT_DIRECTORY.*=\).*$/\1 docs/g' docs/doxygen.conf
```
Редактирование файла README.md
```ShellSession
$ gsed -i 's/lab06/lab07/g' README.md #редактирование файла README.md
```
Документируем функции print 
```ShellSession
# документируем функции print 
$ edit include/print.hpp
```

```ShellSession
$ git add .#добавляем все отредактированные файлы в подтвержденные
$ git commit -m"added doxygen.conf" #создаем коммит
$ git push origin master #выгружаем локальный репозиторий в удаленный репозиторий
```
Работа с Travis
```ShellSession
$ travis login --auto #авторизуемся своим GITHUB аккаунтом
$ travis enable #включаем репозиторий в Travis
```
Создание базового файла документации, перемещение файлов, отправление изменений на удаленный репозиторий седьмой лабораторной работы 

```ShellSession
$ doxygen docs/doxygen.conf
$ ls | grep "[^docs]" | xargs rm -rf #перемещение и удаление файлов
$ mv docs/html/* . && rm -rf docs
$ git checkout -b gh-pages #перемещаемся на ветку gh-pages
$ git add . #добавляем все отредактированные файлы в подтвержденные
$ git commit -m"added documentation" #создаем коммит
$ git push origin gh-pages #выгружаем локальный репозиторий в удаленный репозиторий
$ git checkout master #перемещаемся на ветку master
```

## Report

```ShellSession
$ popd
$ export LAB_NUMBER=07
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [HTML](https://ru.wikipedia.org/wiki/HTML)
- [LAΤΕΧ](https://ru.wikipedia.org/wiki/LaTeX)
- [man](https://ru.wikipedia.org/wiki/Man_(%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_Unix))
- [CHM](https://ru.wikipedia.org/wiki/HTMLHelp)
- [PostScript](https://ru.wikipedia.org/wiki/PostScript)

```
Copyright (c) 2017 Братья Вершинины
```
