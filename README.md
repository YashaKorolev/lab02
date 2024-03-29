## Laboratory work II

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [x] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial
Установка переменных
```ShellSession 
$ export GITHUB_USERNAME=YashaKorolev                               # Установка переменной GITHUB_USERNAME
$ export GITHUB_EMAIL=korolev.yasha@gmail.com                       # Установка переменной GITHUB_EMAIL
$ export GITHUB_TOKEN=ae541d5bc326278a7543380a65d13c73e349abfe      # Установка переменной GITHUB_TOKEN
$ alias edit=nano                                                   # Установка синонима команды edit
```
Подготовка рабочего места
```ShellSession
$ cd ${GITHUB_USERNAME}/workspace                     # Переход в папку workspace
$ source scripts/activate                             # Выполнение скрипта подготовки
```
Конфигурация hub
```ShellSession
$ mkdir ~/.config                           # Создание папки с конфигами
mkdir: cannot create directory ‘/home/yasha/.config’: File exists

$ cat > ~/.config/hub <<EOF                  # Создание файла конфига hub и запись в него
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https     # Установка переменной конфига git
```
Работа с git
```ShellSession
$ mkdir projects/lab02 && cd projects/lab02         # Создание папки и переход в нее
$ git init                                          # Создание пустого репозиторий
Initialized empty Git repository in /home/yasha/YashaKorolev/workspace/projects/lab02/.git/

$ git config --global user.name ${GITHUB_USERNAME}     # Установка переменной конфига user.name для git
$ git config --global user.email ${GITHUB_EMAIL}       # Установка переменной конфига user.email для git
# check your git global settings
$ git config -e --global                              # Вывод всего конфига из git
[hub]
        protocol = https
[user]
        name = YashaKorolev
        email = korolev.yasha@gmail.com
        
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git    # Добавление ссылки на репозиторий на гитхабе
$ git pull origin master                                                     # Перенос изменения с гитхаба
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/YashaKorolev/lab02
 * branch            master     -> FETCH_HEAD

$ touch README.md                                           # Создать README.md
$ git status                                                # Посмотреть статус репозитория
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	README.md

nothing added to commit but untracked files present (use "git add" to track)

$ git add README.md                               # Добавить README.md в список фиксированных
$ git commit -m"added README.md"                 # Закоммитить фиксированные изменения
[master 645f5bd] added README.md
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 README.md

$ git push origin master                        # Отправить изменения на гитхаб
Username for 'https://github.com': YashaKorolev
Password for 'https://YashaKorolev@github.com': 
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 285 bytes | 285.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/YashaKorolev/lab02.git
   2aa96b9..645f5bd  master -> master


```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```ShellSession
*build*/
*install*/
*.swp
.idea/
```
Перенос изменений с гитхаба
```ShellSession
$ git pull origin master                      # Перенос изменений с гитхаба
remote: Enumerating objects: 4, done.
remote: Counting objects: 100% (4/4), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
Unpacking objects: 100% (3/3), done.
From https://github.com/YashaKorolev/lab02
 * branch            master     -> FETCH_HEAD
   645f5bd..f8cf00a  master     -> origin/master
Updating 645f5bd..f8cf00a
Fast-forward
 .gitignore | 4 ++++
 1 file changed, 4 insertions(+)
 create mode 100644 .gitignore

$ git log                # Просмотр коммитов
commit f8cf00a5ffd3bf079e1021eea37b9a9069cf94e6 (HEAD -> master, origin/master)
Author: YashaKorolev <47750082+YashaKorolev@users.noreply.github.com>
Date:   Mon Jun 10 19:43:39 2019 +0300

    Create .gitignore

commit 645f5bd68f9ef5108daf2f1d3b62c83c25a73ad3
Author: YashaKorolev <korolev.yasha@gmail.com>
Date:   Mon Jun 10 19:40:40 2019 +0300

    added README.md

commit 2aa96b9831442fa150826ecd85ea32723d5571e2
Author: YashaKorolev <47750082+YashaKorolev@users.noreply.github.com>
Date:   Mon Jun 10 19:27:54 2019 +0300

    Initial commit

```
Создание папок и файла с кодом
```ShellSession
$ mkdir sources         # Создание папки sources
$ mkdir include         # Создание папки include
$ mkdir examples        # Создание папки examples
$ cat > sources/print.cpp <<EOF   # Запись кода в файл
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
Создание файла с кодом
```ShellSession
$ cat > include/print.hpp <<EOF       # Запись кода в файл
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```
Создание файла с кодом
```ShellSession
$ cat > examples/example1.cpp <<EOF     # Запись кода в файл
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```
Создание файла с кодом
```ShellSession
$ cat > examples/example2.cpp <<EOF            # Запись кода в файл 
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```
Редактирование README.md
```ShellSession
$ edit README.md          # Редактировать README.md
```
Просмотр состояния репозитория и отправка изменений на гитхаб
```ShellSession
$ git status               # Просмотр статуса репозитория
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	examples/
	include/
	sources/

nothing added to commit but untracked files present (use "git add" to track)

$ git add .                 # Фиксация всех изменений
$ git commit -m"added sources"      # Коммит зафиксированных изменений
[master e4c22c1] added sources
 4 files changed, 32 insertions(+)
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 sources/print.cpp

$ git push origin master                   # Отправка изменений на гитхаб
Username for 'https://github.com': YashaKorolev
Password for 'https://YashaKorolev@github.com': 
Enumerating objects: 10, done.
Counting objects: 100% (10/10), done.
Compressing objects: 100% (7/7), done.
Writing objects: 100% (9/9), 969 bytes | 969.00 KiB/s, done.
Total 9 (delta 0), reused 0 (delta 0)
To https://github.com/YashaKorolev/lab02.git
   f8cf00a..e4c22c1  master -> master

```

## Report

```ShellSession
$ cd ~/workspace/labs/
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
4. Добавьте этот файл в локальную копию репозитория.
5. Закоммитьте изменения с *осмысленным* сообщением.
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
8. Запуште изменения в удалёный репозиторий.
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
3. **commit**, **push** локальную ветку в удалённый репозиторий.
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
7. Сделайте *force push* в ветку `patch2`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2019 The ISC Authors
```
