
# VSCode

В этом материале будет рассмотрено использование VSCode вместе с Python.

Перед использованием нужно установить расширение. Для этого перейти в Расширения и установить Python.

## Виртуальное окружение

После создания виртуального окружения можно подключить его как интерпретатор по умолчанию. Делается это следующим образом - нажать `ctrl` `shift` `p` и выбрать Select Interpreter, далее выбрать интерпретатор из списка или указать путь к нему.

При переходе в терминал должен появиться характерный признак виртуального окружения - его имя в скобках перед путем.

## Автодополнение

Если установлено расширение, VSCode автоматически будет выводить подсказки в код. В некоторых случаях, например, для атрибутов в html, можно поставить курсор между кавычек и нажать `ctrl` `space`.

## Отладка

Отладка нужна для отслеживания работы программы построчно. Отладка начинается с точки или точек останова и запускается соответствующей кнопкой. Точки останова включаются левее нумерации строк. В режиме отладки можно получить все доступные переменные и их значения на определенных моментах выполнения программы.

## Сниппеты

Сниппет - фрагмент кода, который можно вызвать набрав определенное слово. Полезно, если часто используете в проектах однотипные каркасы. Например, в плагине Emmet есть сниппет, который позволяет сделать каркас html страницы.

Перед тем как посмотреть имеющиеся сниппеты стоит понять, что для каждого формата файла будут доступны определенные сниппеты. Чтобы увидеть доступные сниппеты нужно открыть файл, в котором нужно активировать сниппет, далее нажать `Ctrl Shift P` и набрать `Insert Snippet`.

Для того, чтобы добавить свой сниппет, нужно так же нажать `Ctrl Shift P` и ввести `Configure User Snippets`. После чего произойдет переброс в json файл. Здесь в имеющемся словаре, нужно прописать свой сниппет. В качестве ключа выступает имя будущего сниппета, а в качестве значения - словарь с нужными данными. `prefix` - слово, которое активирует сниппет. `body` - код, который должен появиться. Обратите внимание, что строки кода являются элементами массива. Если нужна табуляция, применяется 4 пробела внутри строки.

```json
{
	"Имя_сниппета":{
		"prefix":"Слово",
		"body":[
			"строка_кода_1",
			"строка_кода_2"
		]
	}
}
```

## Полное удаление VS Code

Рассмотрим способ полного удаления VS Code с ПК. Способ работает на Windows 10, но не исключено, что он сработает и с более ранними версиями.

### Алгоритм

1. Удалить VS Code стандартным способом через настройки в пункте **Приложения**.
2. Перейти в c\users\user удалить папку **.vscode** 
3. Перейти в c\users\user\AppData\Roaming удалить папку **Code**
4. VS Code полностью удален с вашего ПК.