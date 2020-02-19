# GIT

    -- {path}

    сказать git что после `--` пойдёт путь

    большинство команд git игнорируют файлы которые не назодятся под наблюдением

`init`

> создание директории .git, слежение за изменением файлов

---

## add - _добавление изменений в индекс_

`.`

> добавление в индекс всех файлов в текущей директории директории и поддиректории

`-A`

> добавление в индекс всех файлов от корня проекта

---

## commit - _добавление изменений в репозиторий_

> добавление файлов из индекса в репозиторий с предварительным вызовом редактора для коментария изменений

`-v`

> открывает редактор, но в редакторе присутствует информация diff. что бы проверить всё ли вошло в комит, что требовалось

`-m "{comment}"`

> добавление файлов из индекса в репозиторий без вызова редактора, но с маленьким коментом

`-a`

> добавление файлов из рабочей области в индекс и в репозирий (только файлов которые ранее были в индексе)

`-am "{comment}"`

> добавление файлов из рабочей области в индекс и в репозирий с коментом (только файлов которые ранее были в индексе)

`-c ORIG_HEAD`

> берём описание из существующего. на случий когда сделали мягкий ресет. при этом откроется редактор для редактирования сообщения взятого с вершины

`-С ORIG_HEAD`

> берём описание из существующего. на случий когда сделали мягкий ресет. сообщение берётся как есть

---

## rm - _удаление_

`{file_name}`

> удаление файла из рабочей области

`--сached {file_name}`

> удаление файла из индекса, но не из рабочей директории

`-r {dir_name}`

> удаление директории из рабочей области

`-r --сached {dir_name}`

> удаление директории из индекса, но не из рабочей директории

---

## mv - _переименование файлов_

`{file_name} {file_name_2}`

> переименование файлов

---

## restore - _вынесение изменений из индекса_

`--staged {file_name}`

> вынесение из индекса ещё не закомиченых файлов

---

## branch - _работа с ветками_

> показывает какие есть ветки

`-v`

> показывает какие есть ветки с дополнительной информацией

`{name_new_branch}`

> создание новой ветки с именем

`{branch} {commit}`

> создаст ветку с указанным комитом

`-f {branch} {commit}`

> перенесёт ветку на указанный комит или ветку так как ветка это просто ссылка на коммит

`-f {branch} ORIG_HEAD`

> если при merge поняли, что поторопились со слиянием, то можно всё вернуть

`-d {branch}`

> удаление ссылки ветки, оставляя при этом все коммиты. работает только в том случае если ветка обьединена с текущей

`-D {branch}`

> удаляет ветку с комитами

---

## checkout - _перемещение по коммитам_

`{branch/commit}`

> переключение на другую ветку или коммит

`-b {branch}`

> создание новой ветки и переключение на неё

`-B {branch} {commit}`

> перенос ссылки ветки на новую ссылку комита и переключение за эту ветку

`-f {branch}`

> переключение на другую ветку, потеря не закомиченных изменений

`-f HEAD`

> переключение на текущую ветку при этом все незакомиченные изменения пропадут. (можно без указания HEAD или такое обозначение -> @, он идёт по умолчанию)

`{branch} {name_file}`

> откатывает файл. при этом добавляет в индекс для нового коммита

`{path}`

> откатывает изменения из индекса в рабочую директорию

`HEAD {path}`

> откатывает изменения из репозитория и индекса в рабочую директорию

`-- {path}`

> всё что после 2 дифиса воспринимается как путь. 2 дифис нужен когда ситуация неопределённая. например ветка и папка имеют одно имя

---

## stash - _отложенные изменений_

> архивируем не закомиченные изменения

`pop`

> возырвщвем архивируемые изменения

---

## log - _история_

> история коммитов

`--oneline`

> история коммитов в одну строку

`--oneline {branch/commit}`

> история конкретной ветки или комита в одну строку

`--oneline -g`

> переключает log в особое отображение рефлогов тоже самое что и `git reflog`

`--pretty=oneline`

> форматирование логов. вводит полный номер коммита

`--pretty=oneline --abbrev-commit`

> форматирование логов. вводит короткий номер коммита. тоже самое что и `git log --oneline`

`--no-decorate`

> вывод без ссылок на ветки

* `--pretty=format:'%h %ch | %s%d [%an]'`
* `--pretty=format:'%h %ch | %s%d [%an - %ae]'`
* `--pretty=format:'%h %cd | %s%d [%an - %ae]' --date=short`
* `--pretty=format:'%h %cd | %s%d [%an - %ae]' --date=format:'%F %R'`
* `--pretty=format:'%h %cd | %s%d [%an - %ae]' --date=format:'%d.%m.%Y %H:%M:%S'`
* `--pretty=format:'%C(yellow)%h %C(blue)%cd %C(reset)| %C(yellow)%s%C(green)%d %C(blue)[%an - %ae]' --date=format:'%d.%m.%Y %H:%M:%S'`

> кастомный формат вывода логов. больше в `git help log`

> формат дат не чать `git`. формат используется в функции `strfdate`. [можно посмотреть по ссылке](https://www.php.net/manual/ru/function.strftime.php)

`-p`

> вывод логов с тем что было сделано

`{commit} {commit} --graph`

> красиво отображает дерево

* `{commit1} ^{commit2}`
* `{commit2}..{commit1}`
* `HEAD..{commit1}`

> кареткой убираем вывод коммитов 2.

`{path}`

> вывод где учавствовал только этот файл

`--follow`

> наёдёт так же предыдущее имя файла

`--grep {commit_comment}`

> находит те комиты где встретит слово

* `--grep '{regex}'`
* `--grep '{regex}' -P`

> находит те комиты удовлетворяющие регулярному выражению. но поиск в сообщении комита

`-G{regex}`

> находит те комиты по регулярному выражению, но уже в самих файлах

---

## reflog - _история ссылок_

> показывает рефлоги

`--date=iso`

> показывает рефлоги с датой в формате iso

---

## show - _информация_

> информация о коммите (по дефолту HEAD или такое обозначение -> @)

`{branch/commit}`

> информация о конкретном комите или ветки

`{branch/commit}~`

> информация от конкретного комита или ветки вниз (сколько ~ столько шагов по истории вниз)

`{branch/commit}~2`

> информация от конкретного комита или ветки вниз (какое число после ~ столько шагов вниз по истории)

`@~:{name_file}`

> просмотр файла

`@~2:{name_file}`

> просмотр файла

`fix:{name_file}`

> просмотр файла на ветке fix

`:{name_file}`

> просмотр файла который в индексе

`:/{any_word}`

> просмотр файла в котором встретиться слово. возвращает самый свежий комит. ищет с любой ветки

---

## merge - _слияние_

`{branch/commit}`

> слияние веток перемоткой. если по одной ветке (прямой потомок) по одной ветке

`--abort`

> отмена слияния

`--no-commit`

> останавливает слияние до коммита в репозиторий. на тот случий если есть семантические ошибки

## merge-base - _информация_

`{branch/commit}` `{branch/commit}`

> выводит номер комита где произошло расхождение веток

---

## tag - _теги_

> выводит все теги

`{name_tag} {branch/commit/HEAD}`

> создание метки для коммита

`--contains {commit}`

> выводит теги которые указывают на комит

`-n`

> дополнительно выводит сообщение на коммите

`-n -l '{name_tag}*'`

> выводит теги по маске

`-d {name_tag}`

> удвление указанных тегов

`-a -m '{message}' {name_tag} {commit/branch/HEAD}`

> создание тега с аннотацией

---

## describe - _ближайшие теги_

> покажет ближайший анотированный тег

---

## archive - _архивируем коммиты_

`-o {path} HEAD`

> архивируем

---

## reset - _отмена коммитов и удаление не закомиченных изменений_

`--hard`

> откатываем изменения из индекса и рабочей директории текущего коммита и удаляем коммиты

`--hard {commit/@~/@~~/@~3/...}`

> откатываем на заданный коммит и удаляем коммиты

`--hard ORIG_HEAD`

> возвращаемся на коммит который заресетили

`--soft {@~/@~2/...}`

> оставляет файлы коммита с которого ушли. (как бы отминили коммит, обычно что бы переделать неудачные коммиты)

`--merge`

> удаляет изменения которые внесены в индекс

working directory | index | current branch | type
---|---|---|---
0 | 0 | <- | --soft
0 | <- | <- | --mixed _(default)_
<- | <- | <- | --hard

---

## clean - _удаление не отслеживаемых файлов_

`-d`

> удаление директорий

`-dx`

> удаление директорий и файлов в .gitignore

`-dxf`

> удаление директорий и файлов в .gitignore просто без f работать не будет

---

## diff - _сравнение веток / коммитов_

```
-U{number} - сколько строк показывать в контексте изменений (default=3)
```

```
по умолчанию git считает словом любую последовательность символов без пробелов. но драйвер сравнения можно поменять. напрмер в файле `.gitattributes` прописать `*.html diff=html`. который скажет git, что для всех файлов `html` применять встроенный друйвер `html`. командой `git help attributes` по слову `html` можно найти какие драйвера для слов поддерживает git
```

[файл самого git который предоставляет драйверы](https://github.com/git/git/blob/master/userdiff.c)

> сравнивает рабочую директорию с индексом. если в рабочей что то поменяли тогда покажутся новейшие изменения

* `{branch/commit} {branch/commit}`
* `{branch/commit}..{branch/commit}`

> сравнение веток или комитов

`{branch/commit} {branch/commit} {path}`

> раздичие между левым и правым в каком либо файле

`{branch/commit}...{branch/commit}`

> а что именно изменилось у второго с момента расходжения с первым. тоесть сравнивает то что после `...` с комитом где произошло расхождение с тем что до `...`

`{branch/commit/@~/@~2/...}`

> сравнение рабочей директории с коммитом этого момента

`HEAD`

> сравнит репозиторий с рабочей директорией

* `--chached`
* `--staged`

> сравнит репозиторий с индектом. с изменениями которые в индексе но не закомичены

`{path}`

> сравнит то что по пути находиться с текущей директорией

`--name-only {branch/commit} {branch/commit}`

> список путей без деталей. что бы посмотреть, что вообще изменяется если файлов много

`{commit1}:{path1} {commit2}:{path2}`

> сравнивает первый комит и файл со вторым комитом и файлом

`--word-diff`

> вывод различий по словам

`--color-words`

> вывод различий по словам только цветом