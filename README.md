## Лабораторная работа  

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [x] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Выполнить инструкцию учебного материала

## Tutorial
Создание переменных среды и установка их значений
```sh
#Создание переменных среды и установка их значений
$ export GITHUB_USERNAME=Gnole 
$ export GITHUB_EMAIL=olegbouchin@gmail.com 
$ export GITHUB_TOKEN=*******************************
#Cвязывание команды edit с вызовом текстового редактора Atom

```
Начало работы в каталоге `workspace`
```sh
# Переход в  рабочую директорию
$ cd ${GITHUB_USERNAME}/workspace
# Выполнение скрипта добавляющего Node.js в PATH
$ source scripts/activate
```
Создание директории `~/.config` с настройками конфигурации Git
```sh
$ mkdir ~/.config
#Создание файла hub с настройками конфигурации Git
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
# Установка конфигурации работы по протоколу  https утилиты hub  
$ git config --global hub.protocol https
```

```sh
$ mkdir projects/lab02 && cd projects/lab02
# Создание локального git-репозитория (подведение существующего каталога под версионный контроль)
$ git init
Initialized empty Git repository in /Users/evgengrmit/Evgengrmit/workspace/projects/lab02/.git/
# Указание пользовательских настроек: адреса почты , имени пользователя
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# Проверка настроек
$ git config -e --global
# # Подключение локального репозитория к удаленному серверу
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
# Объединение изменений, присутствующих в удаленном репозитории, в локальный рабочий каталог
$ git pull origin master
 # Создание пустого файла README.md
$ touch README.md
# Cписок изменений в каталоге
$ git status
#  Добавление файла README.md в отслеживаемые
$ git add README.md
# Фиксация изменений в локальном репозитории (коммит)
$ git commit -m"added README.md"
# Помещение изменений в главную ветку удаленного хранилища, связанного с рабочим каталогом
$ git push origin master
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```sh
*build*/
*install*/
*.swp
.idea/
```
Работа с локальным репозиторием
```sh
# Объединение изменений, присутствующих в удаленном репозитории, в локальный рабочий каталог
$ git pull origin master
# Cписок коммитов
$ git log
```
Работа в локальном репозитории - написание программы на C++
```sh
$ mkdir sources
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```sh
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```sh
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```sh
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```
Заполнение файла README.md
```sh
$ edit README.md
```
Публикация новых файлов на удаленном сервере
```sh
$ git status
# Подвести все файлы в каталоге под версионный контроль
$ git add .
$ git commit -m"added sources"
$ git push origin master
```

## Report
Создание отчета по лабораторной работе
```sh
$ cd ~/workspace/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md # Создание отчета
$ gist REPORT.md # Публикация отчета
```

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2020 The ISC Authors
```
