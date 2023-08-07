# Парсинг в requests и bs4

Установка

```
pip install beautifulsoup4
pip install lxml
```

## bs4

Для начала нужно понять как работать с имеющимся html кодом. Для примера будет использоваться фрагмент html кода, который поместится в переменную, а дальше будет к нему обращение при помощи BeautifulSoup.

```python
from bs4 import BeautifulSoup

html_doc = """<html><head><title>The Dormouse's story</title></head>
<body>
<p class="title"><b>The Dormouse's story</b></p>

<p class="story">Once upon a time there were three little sisters; and their names were
<a href="http://example.com/elsie" class="sister" id="link1">Elsie</a>,
<a href="http://example.com/lacie" class="sister" id="link2">Lacie</a> and
<a href="http://example.com/tillie" class="sister" id="link3">Tillie</a>;
and they lived at the bottom of a well.</p>

<p class="story">...</p>
"""

soup=BeautifulSoup(html_doc,'html.parser') #Создание экземпляра класса
```

Теперь можно обращаться к экземпляру.

```python
soup.title #Выводить блок title
soup.title.string # Выводит сам title
soup.title.parent.name # Выводит имя блока-родителя
soup.p # Выводит блок первого параграфа
soup.p.attrs # Выводит атрибуты в виде словаря
soup.p['class'] #Возвращает имя класса первого параграфа. Если атрибут имеет несколько значений, выводиться будет список.
soup.a # Выдает блок первой ссылки
soup.find_all('элемент') # Возвращает все элементы соответствующие запросу
soup.find(атрибут='значение') # Выдает результат поиска по атрибуту
soup.get_text() # Выводит весь текст страницы
```

Часто нужно перебрать элементы в цикле for. Делается это следующим образом.

```python
for i in soup.find_all('элемент'):
    print(i.text+' '+i.get('атрибут'))
```

Здесь text выводит текст элемента, а в get передается атрибут и выводится значение атрибута.

### Открытие документа из файла.

Для начала избавимся от переменной с html кодом, перенеся код в отдельный файл, а потом можно обращаться к нему как обычно. В примере получим текст документа.

```python
with open ('файл.html')as f:
    soup=BeautifulSoup(f,'html.parser')
    print(soup.get_text())
```


### Навигация

Самое простое, что можно сделать - это обратиться непосредственно к элементам. Например, можно добавить заголовок первого уровня в наш шаблон и потом получить его в принте `soup.h1.text`.

Так же можно спускаться в дочерние элемента. Добавим в шаблон этот фрагмент.

```html
<div>
    <h1>Hello</h1>
</div>
```

`soup.div.h1.text` выведет заголовок. **Обратите внимание, что выводится только первый элемент!**

Для получения всех элементов используется `find_all('элемент')`, но именно так перебираются однотипные элементы - только ссылки, параграфы, заголовки и так далее.

Для получения дочерних элементов используется `contents`. Для примера изменим в шаблоне блок.

```html
<div>
    <h1>Hello</h1>
    <h2>Hello2</h2>
    <h3>Hello3</h3>
    <h4>Hello4</h4>
    <h5>Hello5</h5>
</div>
```

```python
print(soup.div.contents)
```

Для перебора в цикле лучше использовать `children`

```python
for i in soup.div.children:
    print(i.text)
```

Для получения фрагмента с родительским классом используется метод `parent`.

```python
print(soup.h1.parent)
```

Для обращения к следующему элементу используется `next_sibling`, а для возвращения предыдущего - `previous_sibling`. **Здесь стоит обратить внимание на странное поведение этих методов. Для корректной работы необходимо, чтобы в разметке не было отступов, то есть, чтобы все элементы шли в одну строку, что странно.**

Чтобы этого не происходило, нужно передать объект в переменную, а уже потом вызвать метод. Вот пример кода.

```python
with open ('index.html')as f:
    soup=BeautifulSoup(f,'html.parser')
    nxt=soup.h1
    print(nxt.next_sibling)
```

#### find() и find_all()

find() ищет первый элемент, а find_all() ищет все элементы и помещает их в список, поэтому предстоит итерация. Здесь мы более подробно разберем эти 2 метода. Имеется несколько способов поиска.

##### Способ 1 - через строку с названием элемента

```python
for i in soup.find_all('элемент'):
    print(i.get('href'))
```

##### Способ 2 - через регулярные выражения.

```python
import re
...
for i in soup.find_all(re.compile('запрос')):
    print(i)
```

##### Способ 3 - через список

```python
for i in soup.find_all(['элемент1','элемент2']):
    print(i)
```

##### Способ 4 - через конкретные значения.

```python
for i in soup.find_all(class_="значение",id="значение"):
    print(i.text)
```

Обратите внимание на то, что тут класс передается с нижним подчеркиванием, так как это слово зарезервировано. В таком примере найдутся элементы, у которых есть класс с определенным именем и определенный айди.

Правильнее будет обратиться к методу attrs и передать в виде ключа и значения словаря.

```python
for i in soup.find_all(attrs={"атрибут":"значение"}):
    print(i.text)
```

Ну или по конкретному элементу.

```python
for i in soup.find_all("элемент",class_="название"):
    print(i.text)
```

## requests

Создание простого get запроса

```python
r=requests.get('сайт')
print(r.url) # Выводит url
# Вывод - сайт

dct={'k1':'value11'}
r=requests.get('сайт',params=dct)
print(r.url) # Выводит url
# Вывод - сайт?k1=value11

print(r.text) # Выводит ответ сервера

print(r.encoding) # Выводит кодировку

r.encoding='новая кодировка' # Изменить кодировку

print(r.status_code) # Выводит код статуса
```

### Чтение двоичных данных

Может пригодиться для работы с изображениями и другими медиафайлами. Здесь нужно импортировать новый модуль, который используется для чтения двоичных данных. Так же импортируем библиотеку для работы с изображениями.

```python
import requests
from PIL import Image # Для работы с изображениями
from io import BytesIO # Для чтения двоичных данных

r=requests.get("url картинки")
i=Image.open(BytesIO(r.content)) # Открытие изображения
i.save('имя.расширение') # Сохранить изображение
i.show() # Показать изображение
```

### Работа с json

Если на странице есть json, его можно так же получить.

```python
import requests

r=requests.get("страница с json")
print(r.json())
```

### Работа с заголовками

Это может быть полезным для кастомизации запросов. Например, можно указать другой user-agent - в примере ниже происходит как раз это.

```python
import requests
headers={'user-agent': 'агент'}
r=requests.get("https://api.github.com/events",headers=headers)
```

### Поиск по XPATH

Таким образом можно искать элементы по XPATH.

```python
import requests
from bs4 import BeautifulSoup
from lxml import etree
url=requests.get("сайт",headers=заголовок)
sp=BeautifulSoup(url.content,'html.parser')
dom=etree.HTML(str(sp)) # Получение древа страницы
print(dom.xpath("//h1")[0].text)
```

Обратите внимание, что нужно явно указывать индекс элемента или перебирать в цикле, так как этот метод ищет список элементов.