# Helium


[Helium](https://github.com/mherrmann/helium) - надстройка над Selenium дающая возможность писать более лаконичный код.

**Примечание**. В руководстве будет часто использоваться метод поиска элементов через Xpath. Автор руководства считает, что это наиболее удобный и гибкий способ поиска элементов.

## Основы работы

Установка
```python
pip install helium
```

Импорт библиотеки
```python
from helium import *
```

Запуск браузера. Headless - фоновый режим
```python
start_chrome("адрес", headless=true/false)
start_firefox("адрес", headless=true/false)
```

Еще команды
```python
write('текст') #ввести текст в поле
press(клавиша) #нажать клавишу
click('значение') #кликнуть по элементу с значением
go_to('адрес') #перейти по адресу
refresh() # Обновить страницу
kill_browser() #закрыть браузер
```

Поиск элемента и вывод значения
```python
print(S("xpath").web_element.text)
```

Поиск элемента и вывод атрибута
```python
print(S("xpath").web_element.get_attribute("атрибут"))
```

Поиск элементов
```python
a=find_all(S("xpath"))
for i in a:
    # Действие с элементом
```

Скроллинг
```python
scroll_down(числоПикселей) # Скроллинг вниз
scroll_up(числоПикселей) # Скроллинг вверх
scroll_left(числоПикселей) # Скроллинг влево
scroll_right(числоПикселей) # Скроллинг вправо
```

Навести курсор мыши можно при помощи hover, параметром нужно передать элемент, на который навести курсор.

```python
hover(S("xpath"))
hover(Point(x, y)) # x и y - координаты дисплея.
```

Пример скрипта
```python
from helium import *
start_chrome('google.com')
write('helium selenium github')
press(ENTER)
click('mherrmann/helium')
go_to('github.com/login')
write('username', into='Username')
write('password', into='Password')
click('Sign in')
kill_browser()
```