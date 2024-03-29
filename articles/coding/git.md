# Git

В этом материале будут описаны некоторые команды git.

## Первичные настройки

После установки Git необходимо зарегистрироваться на сайте и, в самом Git заполнить данные. Вся работа производится в консоли.

```
git config - -global user.name "Name"
git config - -global user.email "Email"
```

## Общие сведения. Начало работы с репозиторием

|Команда|Описание
|---|---
|git init|Инициализация git в папке.
|git status|Показывает новые файлы и статус git. Если подсвечено красным, нужно ввести команду
|git add имя файла|Добавляет файл в репозиторий.
|git add .|Ддобавляет все новые и измененные файлы в репозиторий.
|git commit -m "Текст коммита"|Информация об изменениях.
|git log|Показать коммиты. Выйти можно при помощи клавиши q.
|git log --oneline|Краткое содержимое коммитов.
|git log --oneline --all|стория всех коммитов во всех ветках.
|git show хеш коммита|Показать конкретный коммит.
|git checkout имя файла|Восстановить случайно удаленный файл. Работает до применения коммита
|git checkout хеш коммита путь к файлу|Восстанавливает содержимое файла, которое было в коммите.
|git checkout -b имя ветки|Создание ветки от последнего коммита.
|git diff - -slaged имя файла|Посмотреть последние изменения.
|git commit --amend -m "текст"|Изменить сообщение последнего коммита.
|git checkout хеш коммита -b - имя ветки|Перемещение коммита в другую ветку.
|git merge имя ветки которую надо залить -m имя ветки куда заливать|Слияние веток.

### Клонирование репозитория

После создания репозитория его нужно клонировать на ПК. Для этого нужно перейти в созданный репозиторий, нажать зеленую кнопку Code и скопировать ссылку. Далее перейти в папку, где будет храниться репозиторий и из консоли ввести...

```
git clone скопированная ссылка
```

### Пуш на Github

После внесения изменений, в консоли написать...

```
git add.
git commit -m "Текст коммита"
git push
```

## Подробно о Git и Github

Git нужен для управления версиями файлов в проекте. Например, если в проекте пишется программа, то с помощью Git можно сохранить разные версии файла и спомощью него же откатиться на более раннюю или позднюю стадию разработки. Проект, который использует Git называется репозиторием. Github - сайт для хранения репозиториев.

### Создание репозитория и добавление файлов

В папке с проектом нужно инициализировать Git. Для этого в терминале нужно перейти в папку с проектом и прописать
```
git init
```

После этого появится скрытая папка git.

Далее нужно добавить файлы в git. Для этого в той же папке, в терминале, ввести 
```
git add имяФайла
или для добавления всех файлов
git add .
```

Вторую запись можно использовать и при обновлении некоторых файлов. В таком будут добавлены лишь те файлы, которые были изменены. Команду add можно использовать при любых изменениях, а не только при добавлении файлов.

### Статус

Статус репозитория можно посмотреть, введя следующую команду
```
git status
```

Если файлы не добавлены в репозиторий при помощи add, то они будут подсвечены красным в сообщении статуса.

### Коммиты

Коммит - это описание того, что было изменено. При вводе команды add файлы добавляются в репозиторий, но не закрепляются. Для закрепления нужно ввести после добавления следующую команду
```
git commit -m "Текст коммита"
```

Будет создан коммит, которому присваивается индекс. Эти индексы нужны для дальнейшей работы с коммитами.

### .gitignore

Часто бывает так, что некоторые файлы не нужно отслеживать гитом. Например, если открыть файл с кодом в IDE, то IDE может оставлять там свои файлы и папки. Для того, чтобы добавить файлы в "черный список", нужно в папке с проектом создать файл .gitignore и в нем написать те файлы, которые не будут отслеживаться в гит. Так же нужно будет добавить .gitignore при помощи add.

.gitignore можно создать глобально. Для этого в терминале нужно написать
```
git config --global core.excludefile ~/.gitignore
```

### Ветвления

При инициализации гита создается основная ветка main, но часто бывает так, что над проектом работает несколько человек или нужно внести тестовые изменения не затрагивая основную разработку. Для этого и применяются ветки, которые можно создавать, удалять и объединять. Так же ветки актуальны при поддержке нескольких версий программ.

Есть еще понятие HEAD - это условно говоря место в пространстве гит, где мы находимся на данный момент. При перемещении на другую ветку HEAD будет располагаться в конце нее - на последнем коммите.

Для создания ветки нужно написать следующую команду `git branch названиеВетки`, а чтобы показать все имеющиеся ветки нужно просто ввести `git branch`. Чтобы перейти в другую созданную ветку нужно ввести `git checkout названиеВетки`. Теперь для того, чтобы сделать коммит в нужной ветке, нужно перейти в нее и уже потом коммитить как обычно.

```
ПРИМЕР

1. Создайте в репозитории текстовый файл и добавьте его в репозиторий. Не забудьте про коммит.
2. Создайте новую ветку.
3. Напишите в текстовом файле произвольный текст и сохраните.
4. Добавьте и закоммитьте изменения.
5. Откройте файл и убедитесь, что написанный текст есть. Теперь закройте файл.
6. Перейдите в основную ветку и откройте файл. Видно, что в файле пусто.
```

#### Срочное переключение на другую ветку

Бывают ситуации, когда нужно срочно перейти в другую ветку, но уже есть определенные изменения в файлах, которые еще не добавлены в репозиторий и по какой-либо причине их добавлять сейчас не нужно. Если просто использовать checkout, то будет ошибка. Можно поступить двумя путями.
1. Ввести `git checkout -f названиеВетки`, но в таком случае, если потом повторно перейти обратно, можно увидеть, что проделанные ранее изменения не сохранились.
2. Архивировать изменения при помощи команды `git stash` и после этого переходить в другую ветку. Если перейти в предыдущую ветку, то можно увидеть, что изменения не сохранены, но они заархивированы. Для того, чтобы их разархивировать, нужно ввести `git stash pop`. ВНИМАНИЕ! Заархивированные данные не привязаны к конкретной ветке, поэтому нужно быть осторожными так как можно разархивировать данные не в той ветке.

#### Откат на предыдущие коммиты

Далее будет рассмотрена возможность отката к более ранним коммитам, а следовательно к более ранним версиям файлов.

Для отката к последнему коммиту можно воспользоваться `git checkout -f HEAD`. Ранее было сказано, что HEAD находится на последнем коммите ветки. Можно кстати не указывать HEAD. Для отката к последнему коммиту какой-либо ветки можно использовать `git checkout названиеВетки названиеФайла` - в этом случае файл откатится до последнего коммита заданной ветки, но переход в заданную ветку не будет.

#### Слияние веток

Для слияния нужно перейти в основную ветку и ввести `git merge названиеВетки`, где в качестве названия указать ту ветку, которую нужно присоединить.

Существует вероятность конфликтации, когда в разных ветках была работа с одним и тем же файлом. При слиянии может возникнуть конфликт. Обычно он возникает, когда создается новая ветка, но тем не менее продолжается работа с файлом и в основной ветке. 
По умолчанию берутся последние изменения в основной ветке и последние изменения в другой ветке и происходит слияние. Но тут возможны конфликты, когда и в той и той ветке идет работа с одним файлом. Гиту нужно понять, какую версию файла нужно брать.

#### Удаление ветки

Для удаления ветки нужно выйти с нее и ввести `git branch -d названиеВетки`.


#### Пуш на Github. если несколько веток

Если в репозитории 1 ветка , то можно воспользоваться `git push`, но если веток несколько, то нужно указать нужную при пуше. `git push origin названиеВетки`

### История изменений

Для просмотра истории коммитов можно использовать команду `git log`. Чтобы вывести эту информацию в кратком виде можно использовать `git log oneline`. Для того, чтобы вывести историю коммитов для определенной ветки можно ввести `git log названиеВетки` или `git log названиеВетки --oneline`.

Чтобы вывести информацию о последних изменениях, можно воспользоваться `git show` или `git show названиеВетки`, или `git show идентификаторКоммита`.

Чтобы увидеть информацию несколько коммитов назад можно ввести `git show HEAD~числоКоммитовНазад`.
