# Git

В этом материале будут описаны некоторые команды git.

## Первичные настройки

После установки Git необходимо зарегистрироваться на сайте и, в самом Git заполнить данные. Вся работа производится в консоли.

```
git config - -global user.name "Name"
git config - -global user.email "Email"
```

## Начало работы с репозиторием

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

## Работа с Github

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