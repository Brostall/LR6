# Лабораторная работа №6. Система контроля версий

## Цель работы

Изучение базовых возможностей системы управления версиями, опыт работы с Git Api, опыт работы с локальным и удалённым репозиторием.

## Задание на программирование

Создать аккаунт на GitHub, сделать форк учебного репозитория, настроить Git, выполнить основные операции: клонирование, просмотр истории, слияние веток с разрешением конфликта, коммиты, откат коммита, оформить отчёт в файле README.md и отправить изменения в удалённый репозиторий.

## Выполнение работы

У меня уже был создан аккаунт на сайте GitHub под логином `Brostall`. Затем на странице репозитория https://github.com/Kurtyanik/LR6/ была нажата кнопка Fork, в результате чего копия репозитория появилась в личном хранилище (см. рисунок 1).

![Рисунок 1 – Репозиторий на GitHub после создания форка](screenshots/01_fork.png)

Git был установлен с сайта https://git-scm.com/. Клиент настроен командами из листинга 1: указаны имя пользователя в формате «Группа Фамилия И.О.» и адрес электронной почты, после чего настройки проверены командой `git config --list` (см. листинг 1).

**Листинг 1 – Настройка клиента Git**
```text
iduda@IngvarWin UCRT64 /
$ git config --global user.name "4514 Дударевв И.С"

iduda@IngvarWin UCRT64 /
$ git config --global user.email "i.dudarev04@gmail.com"

iduda@IngvarWin UCRT64 /
$ git config --list
diff.astextplain.textconv=astextplain
filter.lfs.clean=git-lfs clean -- %f
filter.lfs.smudge=git-lfs smudge -- %f
filter.lfs.process=git-lfs filter-process
filter.lfs.required=true
http.sslbackend=schannel
core.autocrlf=true
core.fscache=true
core.symlinks=false
pull.rebase=false
credential.helper=manager
credential.https://dev.azure.com.usehttppath=true
init.defaultbranch=main
core.editor="C:\Users\iduda\AppData\Local\Programs\Microsoft VS Code\bin\code" --wait
user.name=4514 Дударевв И.С
user.email=i.dudarev04@gmail.com
```

Личный удалённый репозиторий был клонирован в рабочую папку на компьютере (см. листинг 2).

**Листинг 2 – Клонирование репозитория**
```bash
cd "/c/Users/iduda/OneDrive/Desktop/2 курс/Основы Программирования/Лабы/Lab6"
git clone https://github.com/Brostall/LR6.git
cd LR6
```

Через веб-интерфейс GitHub (Add file → Create new file) был создан файл `new addon` и зафиксирован коммит (см. рисунок 2). После этого изменения были подтянуты в локальный репозиторий командой `git pull` (см. листинг 3).

![Рисунок 2 – Создание нового файла в репозитории](screenshots/02_github_new_file.png)

**Листинг 3 – Получение изменений из удалённого репозитория**
```text
$ git pull
remote: Enumerating objects: 3, done.
remote: Counting objects: 100% (3/3), done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
Unpacking objects: 100% (3/3), 1017 bytes | 63.00 KiB/s, done.
From https://github.com/Brostall/LR6
   921f53b..b051d7c  master     -> origin/master
Updating 921f53b..b051d7c
Fast-forward
 new addon | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 new addon
```

Список веток и история коммитов каждой из них были получены командами `git branch -a`, `git checkout master`, `git log`, `git log --oneline --graph --all` (см. листинг 4).

**Листинг 4 – Просмотр веток и истории**
```text
$ git checkout master
Already on 'master'
Your branch is up to date with 'origin/master'.

$ git log
commit b051d7cecbe7857f9c506cd14b4cdb53d7203832 (HEAD -> master, origin/master, origin/HEAD)
Author: Brostall <112848545+Brostall@users.noreply.github.com>
Date:   Sat Oct 24 12:32:58 2026 +0300

    Create new addon

    добавил баги

commit 921f53b8d0cebf542c791cf31f04e9b792f385a4
Author: Kurtyanik <45309985+Kurtyanik@users.noreply.github.com>
Date:   Sat Nov 21 20:09:49 2020 +0300

    Обновление информации

commit c08a654a63cfc3a7146b2b7015884d9020f5cbf5
Author: Kurtyanik <45309985+Kurtyanik@users.noreply.github.com>
Date:   Sat Nov 21 20:02:16 2020 +0300

    Файл создан пустым

commit 3c6e9131bb47ed6009c28226afb0535c7f6d5964
Author: Kurtyanik <45309985+Kurtyanik@users.noreply.github.com>
Date:   Sat Nov 21 19:58:20 2020 +0300

    Initial commit

$ git log --oneline --graph --all
* b051d7c (HEAD -> master, origin/master, origin/HEAD) Create new addon
* 921f53b Обновление информации
* c08a654 Файл создан пустым
* 3c6e913 Initial commit
```

Последние изменения в репозитории были просмотрены командой `git show` (см. листинг 5).

**Листинг 5 – Просмотр последних изменений**
```text
$ git show
commit b051d7cecbe7857f9c506cd14b4cdb53d7203832 (HEAD -> master, origin/master, origin/HEAD)
Author: Brostall <112848545+Brostall@users.noreply.github.com>
Date:   Sat Oct 24 12:32:58 2026 +0300

    Create new addon

    добавил баги

diff --git a/new addon b/new addon
new file mode 100644
index 0000000..a2edb5b
--- /dev/null
+++ b/new addon
@@ -0,0 +1 @@
+HelloWorld("print")
```

Ветка `dungeon` была создана от последнего коммита ветки `master` и собственных изменений не содержала, поэтому при первой попытке слияния Git сообщил, что слить нечего (см. листинг 6).

**Листинг 6 – Первая попытка слияния**
```text
$ git checkout master
$ git merge dungeon
Already up to date.
```

Для демонстрации разрешения конфликта он был создан намеренно: файл `conflict.txt` был создан в обеих ветках с разным содержимым. Сначала файл был создан и закоммичен в ветке `dungeon`, затем в ветке `master` (см. листинг 7).

**Листинг 7 – Создание конфликтующих изменений**
```bash
git checkout dungeon
echo "Строка из ветки dungeon" > conflict.txt
git add conflict.txt
git commit -m "Изменена строка в ветке dungeon"
git checkout master
echo "Строка из ветки master" > conflict.txt
git add conflict.txt
git commit -m "Изменена строка в ветке master"
```

После этого было выполнено слияние ветки `dungeon` в `master`. Git сообщил о конфликте: `Auto-merging conflict.txt`, `CONFLICT (add/add): Merge conflict in conflict.txt`, `Automatic merge failed; fix conflicts and then commit the result`. Открыв файл `conflict.txt` в редакторе VS Code, я увидел кнопку «Accept Current Changes», которая автоматически решает конфликт (см. рисунок 3).

![Рисунок 3 – Открытый файл в редакторе кода](screenshots/03_conflict_vscode.png)

Конфликт в ветках был решён (см. листинг 8).

**Листинг 8 – Завершение слияния**
```text
$ git merge dungeon
Auto-merging conflict.txt
CONFLICT (add/add): Merge conflict in conflict.txt
Automatic merge failed; fix conflicts and then commit the result.

$ git add conflict.txt
$ git commit -m "Слияние ветки dungeon в master"
```

После успешного слияния побочная ветка была удалена (см. листинг 9).

**Листинг 9 – Удаление ветки**
```text
$ git branch --merged
  dungeon
* master

$ git branch -D dungeon
Deleted branch dungeon (was e56ed28).

$ git branch
* master
```

В файлы репозитория были внесены изменения, каждое из которых зафиксировано отдельным коммитом с комментарием (см. листинг 10).

**Листинг 10 – Создание коммитов**
```bash
git add .
git commit -m "комментарий 1"
git add .
git commit -m "комментарий 2"
git add .
git commit -m "комментарий 3"
```

Для отмены коммита использована команда `git revert`. Она создаёт новый коммит, отменяющий изменения указанного, и сохраняет историю неизменной (см. листинг 11).

**Листинг 11 – Откат коммита**
```bash
git log --oneline
git revert <хэш код коммита>
```

## Лог команд

```bash
git config --global user.name "4514 Дударев И.С."
git config --global user.email "i.dudarev04@gmail.com"
git config --list
git clone https://github.com/Brostall/LR6.git
git pull
git branch -a
git log --oneline --graph --all
git show
git checkout master
git merge <побочная ветка>
git add <имя файла>
git commit
git branch -d <побочная ветка>
git add .
git commit -m "<комментарий>"
git revert <хэш коммита>
git checkout -b report
git log --pretty=format:"%h %ad %an %s" --date=short
git push -u origin report
git push origin master
```