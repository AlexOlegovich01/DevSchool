# Django

Этот материал посвящен фреймворку Django для создания веб приложений.

## Начало работы

Установка
 Рекомендовано ставить LTS версию - она имеет долгосрочную поддержку.
 
```
pip install django
```

С указанием версии...

```
pip install django==версия
```

Для создания базовой структуры нужно перейти в нужную папку и в консоли ввести команду

```
django-admin startproject название проекта
```

После ввода данной команды можно увидеть, что появилась новая папка с названием проекта. Перейдя в нее видна еще одна папка с названием проекта - **будем называть ее корневая директория** и файл manage.py. После этих действий консоль можно закрыть.

Файл manage.py содержит основную логику проекта. Перейдя в директорию с этим файлом и введя команду в консоль manage.py --help можно увидеть все основные команды.

Теперь можно запустить сервер, введя команду.

```
manage.py runserver
```

Перейдя по http ссылке, можно перейти на активированный сервер. Ctrl C - остановить сервер.

## Архитектура проекта

__init__.py - необходим для того, чтобы Python рассматривал все лежащие файлы как модули. Он обычно пустой и не требует заполнения. Во всех новых папках должен быть этот файл.  
settings.py - отвечает за все настройки, которые нужны для проекта.  
urls.py - хранит url адреса всех страниц.  
wsgi.py - предназначен для размещения проекта в интернете и чтобы проект стал общедоступным.

### settings.py

BASE_DIR - хранит абсолютный путь проекта.  
SECRET_KEY - секретный ключ. Отвечает за безопасную работу с данными. Ключ шифрования.  
DEBUG - благодаря этому информация об ошибках будет отображаться как в консоли, так и на сайте.  
ALLOWED_HOSTS - хосты доступные для сервера. Можно указать \"\*\", тем самым дав понять, что сервер доступен для любых хостов.  
INSTALLED_APPS - сюда перечисляются все приложения на сайте.  
MIDDLEWARE - хранит промежуточные слои между сервером и клиентом. Промежуточные слои помогают хранить информацию о сессии, аутентификации пользователя. Как бы готовые решения для авторизации пользователя.  
ROOT_URLCONF - здесь хранится путь до адресов сайта, то есть до urls.py.  
TEMPLATES - хранит в себе информацию о том, как работать с будущими шаблонами.  
DATABASES - хранит настройки для баз данных.  
AUTH_PASSWORD_VALIDATORS - валидация паролей.  
LANGUAGE_CODE - язык проекта.  TIME_ZONE - часовой пояс.  

### urls.py

Здесь в строке urlpatterns лежит информация о ссылках, в данном случае лежит ссылка на админ панель. Если в браузере после локального адреса написать /admin, можно попасть на страницу админ панели. При переходе видна ошибка, так как еще не настроена база данных. Если в файле конфигурации изменить значение переменной DEBUG, то будет отображаться только заголовок ошибки без информации о ней.

## Создание приложений

В Django сайт состоит из приложений, каждое из которых выполняет свою роль. Для создания нового приложения нужно войти в папку с проектом и в консоли выполнить команду

```
manage.py startapp название
```

После этого можно увидеть, что в основной папке проекта появилась еще одна папка. Теперь нужно перейти в ранее созданную папку, открыть settings.py и в переменную INSTALLED_APPS в конец списка добавить имя созданного приложения. В приложении так же есть набор файлов.

migrations - содержит файлы, которые нужны для дальнейшей разработки базы данных.  
__init__.py - выполняет те же функции, что и в именной папке с проектом.  
admin.py - содержит информацию о том, какую базу данных нужно отображать в админ панели и о том как можно взаимодействовать с базой данных.  
apps.py - информация о приложении.  
models.py - хранит информацию о таблицах баз данных.  
tests.py - содержится тестовая логика.  
views.py - логика отображения страниц.

## Работа с веб страницами

Предполагается, что у вас есть уже созданные html страницы с css стилями и вложениями, например из картинок.

В созданном приложении нужно создать папку templates, перейти в нее и создать папку с таким же названием как у приложения. Это нужно для того, чтобы избежать путаницы с файлами в дальнейшем, так как приложений на сайте может быть много так же как и файлов index.html, например. В этой папке как раз и хранятся html документы. Теперь нужно создать папку для css стилей и прочих дополнений к страницам. Для этого нужно перейти в основную папку проекта и там создать папку static. В нее и закидывается.

Теперь пришло время написать контроллеры отображения страницы. Как было сказано ранее, за них отвечает файл views.py, в него нужно перейти и написать следующую функцию

```python
def index(request):
	return render(request,'products/index.html')
```

Таким образом был создан контроллер отображения страницы index.html. Теперь нужно перейти в корневую папку и открыть файл urls.py для того, чтобы отобразить ранее созданный контроллер. Нужно вспомнить, что файлы - это по сути модули, а модули можно импортировать, поэтому мы импортируем в файл urls.py ранее созданную функцию контроллера.

После строк с импортами нужно ввести

```python
from products.views import index
```

В список urlpatterns добавить это

```python
path('',index,name='index')
```

'' - имеется ввиду, что будет открыта главная страница, так как после основного адреса, после слеша ничего нет на главной странице. index - имя функции, которую нужно просто передать, без скобок. name='index' - название адреса. Стоит отметить, что названия могут быть произвольно другими.

Теперь надо подгрузить стили. Для этого перейти в settings.py и под переменной STATIC_URL создать кортеж STATICFILES_DIRS.

```python
STATICFILES_DIRS = (
    BASE_DIR /'static',
    )
```

Сюда по сути передаются рути к статике - стили, медиа и так далее.

Теперь нужно перейти в index.html и в теге link прописать правильный путь.

## Динамический контент

Далее пойдет речь о создании контента не из html кода, а программно, при помощи Djsngo.

Для примера нужно создать html страницу и поместить ее туда, где хранятся другие html страницы - пока что в ту папку, где и index. Для примера назовем ее test.html. В странице должен быть пустой каркас html документа.

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
</head>
<body>
	
</body>
</html>
```

Далее пеейти в views.py и написать контроллер для этой страницы.

```python
def test(request):
	return render(request,'products/test.html')
```

После, перейти в urls.py и добавить там новый адрес.

```python
path('test',test,name='test'),
```

В данном примере нужно, чтобы на пустой странице программно вывелся заголовок. Изменить функцию test, добавив в нее словарь context и передав его в возвращаемые параметры.

```python
def test(request):
	context={
		"header":"Hello"
	}
	return render(request,'products/test.html',context)
```

Открыть test.html и добавить заголовок. В него передать конструкцию из двойных фигурных скобок. В них нужно вписать нужный ключ словаря.

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<title>Document</title>
</head>
<body>
	<h1>{{header}}</h1>
</body>
</html>
```

### Циклы и работа с словарями

Как и в обычном программировании, теперь есть возможность использовать циклы в веб странице. Немного видоизсеним переменную context.

```python
context={
	"names":["Alex","Nick","Jeb"]
}
```

Задача - вывести имена на странице в цикле. Далее нужно перейти в тестовую html страницу и ввести такую конструкцию. Обратите внимание на фигурные скобки и проценты в них - таким образом можно обращаться к питоновскому коду из html документа. Двоеточие в этом случае, в цикле, не ставится. В конце цикла нужно как бы закрыть его используя конструкцию {%endfor%}.

```html
<body>
	{%for name in names%}
		<h1>Привет, {{name}}</h1>
	{%endfor%}
</body>
```

Для дальнейшего примера снова нужно изменить переменную context. Теперь в словаре будет лежать информация о персонажах и иж жизнях. Нужно создать словарь в переменной context и в ключ perses передать список с словарями.

```python
context={
	"perses":[
		{"name":"Jeb","lives":10},
		{"name":"Jack","lives":5},
		{"name":"Jackson","lives":8},
	]
}
```

Затем перейти в html документ и написать такой цикл. Обратите внимание на то, как передаются значения словаря - не через квадратные скобки, а через точку.

```python
<body>
	{%for pers in perses%}
		<h1>Привет, {{pers.name}}, у тебя {{pers.lives}} жизней.</h1>
	{%endfor%}
</body>
```

Так же можно выполнять условия. Для примера условие будет провелять - истинно или ложно значение у ключа.

```python
context={
	"mode":True
}
```

На странице будет выводиться один текст, если mode истинно и другой, если ложно.

```html
<body>
	{%if mode%}
		<h1>Доступ разрешен</h1>
	{%else%}
		<h1>Доступ ограничен</h1>
	{%endif%}
</body>
```

### Меняем гиперссылки

После работ с Django ссылки в привычном виде уже не работают. Одна из причин, что, к примеру, страница test.html не имеет в адресе расширение файла. При стандартной разметке расширение сохранилось бы, поэтому нужно внести изменения в гиперссылки.

Перейдя в файл urls.py, можно увидеть там, где были прописаны пути, параметр name - с этим и будет проводиться работа в дальнейшем. Напомню, что сейчас у нас есть 2 пути - главная и тестовая страницы.

```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('',index,name='index'),
    path('test',test,name='test'),
]
```

Для примера в html файл нужно вписать следующее.

```html
<body>
	<a href=""><div class="but">1</div></a>
</body>
```

Пусть ссылка ведет в тестовый файл. Синтаксис тут таков...

```html
<body>
	<a href="{%url 'test'%}"><div class="but">1</div></a>
</body>
```

Здесь test - имя страницы, которое указано в параметре name в urls.py.

### Наследование шаблонов

Обычно в сайтах есть общие элементы, которые повторяются на каждой странице - заголовки, меню, футеры и так далее. С точки зрения оптимизации это не правильно, так как лишний код делает проект тяжелее.

Для примера создадим типа сайт, который будет состоять из 2 страниц - все те же index.html и test.html. Представим, что этот сайт с статьями, имеет шапку сайта с названием, блок меню, блок с основным контентом и дополнительной информацией. В нашем случае блок с дополнительной информацией не играет никакой функциональной роли, но при желании можно там разместить информацию об аккаунте, например. Страницы отличаются лишь содержимым в центральном блоке - на главной странице идет перечень статей, например, если бы это была главная страница новостного сайта, а тестовая страница - своего рода страница с статьей.

index.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link rel="stylesheet" href="static/styles/styles.css">
	<title>Document</title>
</head>
<body>
	<div class="sitehead"><h1>Название сайта</h1></div>
	<div class="content">
		<div class="side"><a href="{%url 'test'%}">Меню</a></div>
		<div class="center">Список публикаций</div>
		<div class="side">Дополнительная информация</div>
		<div class="clearfix"></div>
	</div>
</body>
</html>
```

test.html

```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link rel="stylesheet" href="static/styles/styles.css">
	<title>Document</title>
</head>
<body>
	<div class="sitehead"><h1>Название сайта</h1></div>
	<div class="content">
		<div class="side">Меню</div>
		<div class="center">Страница с публикацией</div>
		<div class="side">Дополнительная информация</div>
		<div class="clearfix"></div>
	</div>
</body>
</html>
```

styles.css - этот файл единый для index.html и test.html.

```css
*{padding:0px;margin:0px;}
.sitehead{
	background:black;
	color:white;
	font-size:50px;
	text-align:center;
	width:100%;
	height:100px;
}
.content{margin-top:5px;}
.side{
	background:black;
	color:green;
	font-size:50px;
	text-align:center;
	width:20%;
	min-height:800px;
	float:left;
}
.center{
	background:white;
	color:black;
	font-size:50px;
	text-align:center;
	width:60%;
	min-height:800px;
	float:left;
}
```

Здесь хорошо видно, что в обоих файлах есть повторяющиеся элементы, поэтому нужно их как-то сократить.. Для начала нужно создать файл, в котором будет лежать вся html страница, например файла index и который будет шаблоном всех страниц - то есть будет хранить тот код, который повторяется на всех страницах. В этом примере он будет называться base.html.

Скопируем в него все из index.html, найдем там уникальный тег и заменим его на специальный тег.

```html
Это
<div class="center">Список публикаций</div>
Заменить на
{%block sitecontent%}{%endblock%}
```

Здесь sitecontent - имя блока - любое на ваше усмотрение. И так поступить со всеми тегами с уникальными значениями, если они у вас есть. Теперь перейти в index.html и перед строкой <!DOCTYPE html> вписать следующее

```html
{%extends 'products/base.html'%}

{%block sitecontent%}
	<div class="center">Список публикаций</div>
{%endblock%}
```

Используя тег extends, идет наследование от файла base.html. Остальной код можно смело удалять. Таким образом страницы будут выглядеть так

base.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link rel="stylesheet" href="static/styles/styles.css">
	<title>Document</title>
</head>
<body>
	<div class="sitehead"><h1>Название сайта</h1></div>
	<div class="content">
		<div class="side"><a href="{%url 'test'%}">Меню</a></div>
		{%block sitecontent%}{%endblock%}
		<div class="side">Дополнительная информация</div>
		<div class="clearfix"></div>
	</div>
</body>
</html>
```

index.html
```html
{%extends 'products/base.html'%}
{%block sitecontent%}
	<div class="center">Список публикаций</div>
{%endblock%}
```

test.html
```html
{%extends 'products/base.html'%}
{%block sitecontent%}
	<div class="center">Страница с публикацией</div>
{%endblock%}
```

## Работа с базами данных

Подготовка таблиц для базы данных производится в файле models.py, который находится в созданном приложении. Подготовка таблицы происходит путем создания класса, который наследуется от джанговского класса. В созданном классе можно простым способом передать поля и типы полей, которые будут в таблицах базы данных. Модели - это те же таблицы в базах данных.

Для примера создадим базу данных игроков вымышленной игры. В ней будет одна таблица, в которой будут имена игроков, количество жизней, роль и виртуальный вораст. Выглядеть это будет так.

```python
class Perses(models.Model):
	name=models.CharField(max_length=15)
	lives=models.IntegerField()
	role=models.CharField(max_length=20)
	age=models.IntegerField()
```

### Основные параметры

Эти параметры указываются в скобках.

max_length - максимальная длина поля.  
uniqque - уникальность поля True или False.  
blank - если True, то не будет возникать ошибки, если поле пустое.  
default - значение по умолчанию.  

### Миграции

Миграции переводят классы в базы данных SQL. Сейчас, если запускать сервер, он запустится, нго можно увидеть, что выводится сообщение о непримененных миграциях.Для начала в консоли, в папке, откуда запускается сервер, нужно ввести следующее

```
manage.py makemigrations
```

После ввода команды можно увидеть, что были созданы миграции для ранее созданного класса. Так же был создан файл 0001_initial.py в папке migrations - этот файл как раз и переводит из формата класса в формат таблицы в базе данных. Теперь надо применить миграции. Для этого ввести

```
manage.py migrate
```

Будут применены все имеющиеся миграции.

Для просмотра базы данных можно использовать программу SQLite Studio. Напомню, что база данных расположена в корне и называется db.sqlite3. При открытии можно увидеть много таблиц, среди которых есть и нами созданная.

### Работа с полями базы данных

Есть 2 способа взаимодействовать с БД - при помощи консоли и при помощи админ-панели.

Для первого способа нужно сделать следующее - открыть терминал и в корне, вписать следующее

```
manage.py shell
```

Таким образом можно попасть в обычную питоновскую консоль. Далее введем

```
from products.models import Perses
```

Другими словами из папки products мы импортируем файл models и из файла уже импортируем наш ранее созданный класс Perses. Далее можно выполнять и другие команды. Для примера создадим моего тезку - Алекса и сохраним запись в базу данных. Выглядеть это будет следующим образом.

```
pers=Perses(name='Alex',lives=10,role='Admin',age=30)
pers.save()
```

Тут мы делали экземпляр класса Perses, но можно поступить немного проще - обратиться к классу напрямую. Создадим еще одного персонажа, которого будут звать Вадим.

```
Perses.objects.create(name='Vadim',lives=7,role='Moderator',age=25)
```

Тут уже не нужно писать дополнительную строку для сохранения - оно происходит сразу.

Так же нужно научиться просматривать поля из консоли, а так же использовать выборку. Для просмотра таблицы используется метод all(), но перед его применением нужно внести изменения в класс таблицы, иначе информация выводиться будет, но не та, что надо. После изменения в классе и перезапуска консоли будут выводиться имена.

```python
class Perses(models.Model):
	name=models.CharField(max_length=15)
	lives=models.IntegerField()
	role=models.CharField(max_length=20)
	age=models.IntegerField()
	def __str__(self):
		return self.name
```

Можно выводить и другие поля, если добавить в вывод простой конкатенацией.

```python
return self.name+' '+self.role
```

ВАЖНО!  
При определении новых методов в классе база данных никак не меняется, но если вносить изменения в настройки полей, то нужно заново создавать и применять миграции.

Пришло время произвести простую выборку. Просто узнаем, кто админ в этой игре.

```
Perses.objects.filter(role='Admin')
```

Так же можно достать данные ячейки при помощи метода get(). Узнаем, кто такой Вадим.

```
Perses.objects.get(name='Vadim')
```

Узнаем, сколько ему лет

```
Perses.objects.get(name='Vadim').age
```

#### Работа с базой данных из админ-панели

Для начала нужно создать суперпользователя, то есть админа. Ввести в консоли следующую команду, ввести логин и пароль - любые.

```
manage.py createsuperuser
```

Далее перейти на наш сайт/admin и ввести логин с паролем. Таблицы с персонажами там всеж нет - ее нужно зарегистрировать. Делается это в файле admin.py

```python
from products.models import Perses
admin.site.register(Perses)
```

Снова перейдем в админку и на этот раз увидим название приложения products и в нем таблицу Perses. Щелкнув по ней, перейдем в нее и увидим персонажей - тут они названы как ранее передавали в магическом методе str. Щелкнув по нужному персонажу, можно просмотреть его данные, изменить их, а так же удалить персонажа. Выйдя назад - к списку персов, можно добавить нового, нажав на Add Имя таблицы.

### Работа с медиафайлами

В класс Perses добавим поле с картинкой? сохраним файл и добавим миграции, после этого применив их.

```python
image=models.ImageField(upload_to='images',blank=True)
```

Здесь параметр upload_to отвечает, в какую папку будут сохраняться картинки. Далее перейти в settings.py и вписать под STATICFILES_DIRS две переменные - это как раз пути к папке, где будут храниться медиафайлы. Нужно не забыть создать папку media в корне.

```python
MEDIA_URL='/media/'
MEDIA_ROOT=BASE_DIR /'media'
```

Отличие медиа от статики в том, что статика обычно создается 1 раз и не меняется, то есть имеет статичный вид. В статике могут быть и медиафайлы, например фоновое изображение или те, которые динамически меняться скорее всего не будут. В свое время медиа можно менять часто и это удобно делать. А теперь вспомним новосозданное поле с картинкой, а конкретно параметр upload_to='images'. Папка images будет находиться в папке media.

Чтобы медиафайлы отображались, для них нужно сделать ссылку. Для этого нужно перейти в urls.py. В нем импортировать некоторые джанговские классы и в конце написать условие.

```python
from django.conf.urls.static import static
from django.conf import settings # Для доступа к переменным с media
if settings.DEBUG: #Обращение к переменной DEBUG в файле settings.py
	urlpatterns+=static(settings.MEDIA_URL,document_root=settings.MEDIA_ROOT)
```

А теперь видоизменим index.html по красоте. Удалим из него все - пока что файлом base.html пользоваться не будем.

index.html

```html
<!DOCTYPE html>
<html lang="ru">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link rel="stylesheet" href="static/styles/styles.css">
	<title>Document</title>
</head>
<body>
	<div class="sitehead"><h1>Список игроков</h1></div>
	<div class="content">
		<div class="pers">
			<div class="pers-img"></div>
			<div class="pers-name">Имя</div>
			<div class="pers-role">Роль</div>
			<div class="pers-lives">0</div>
			<div class="pers-years">20</div>
		</div>
		<div class="clearfix"></div>
	</div>
</body>
</html>
```

styles.css

```css
*{padding:0px;margin:0px;box-sizing:border-box;}
body{background:#373B42}
.sitehead{
	background:black;
	color:white;
	font-size:40px;
	text-align:center;
	width:100%;
	height:100px;
}
.content{margin-top:5px;}
.pers{
	float:left;
	margin:5px;
	width:250px;
	border:2px black solid;
	font-size:25px;
	text-align:right;
}
.pers-img{
	width:100%;
	height:200px;
	border-bottom:2px black solid;
}
.pers-name{
	width:100%;
	height:40px;
	border-bottom:2px black solid;
	color:white;
}
.pers-role{
	width:100%;
	height:40px;
	border-bottom:2px black solid;
	color:#2BFF00;
}
.pers-lives{
	width:100%;
	height:40px;
	border-bottom:2px black solid;
	color:red;
}
.pers-years{
	width:100%;
	height:40px;
	border-bottom:2px black solid;
	color:yellow;
}
```

Теперь перейдя в админку и открыв таблицу Perses, можно добавить изображение.

Вспомним о том, как передавали щначения из переменной context. Так вот, тогда это были тесты, как и сейчас конечно, но сейчас мы можем передать туда нашу базу данных.

```python
def index(request):
	context={
		"perses":Perses.objects.all(),
	}
	return render(request,'products/index.html',context)
```

База данных синхронизирована с сайтом. Уже можно в админке добавлять новые ячейки в базу и они будут отображаться на сайте.

## Пространство имен

Некоторые проекты могут иметь много приложений, а каждое приложение имеет свой набор из страниц. Бывает так, что страницы имеют одинаковые названия, что может привести к конфликтам. Для недопущения этого используется пространство имен.

Для примера создадим файл game.html и скопируем в него все из index.html, но изменим имя стилей на game-styles.css. Так же создадим файл game-styles.css и скопируем в него все из styles.css. Далее вставим в файлы следующий код.

В index.html

```html
<!DOCTYPE html>
<html lang="ru">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1.0">
	<link rel="stylesheet" href="static/styles/styles.css">
	<title>Document</title>
</head>
<body>
	<div class="cont">
		<a href="{%url 'game'%}"><div class="but">ПЕРЕЙТИ НА САЙТ</div></a>
	</div>
</body>
</html>
```

styles.css

```css
*{padding:0px;margin:0px;box-sizing:border-box;}
body{background:#373B42}
.cont{text-align:center;height:700px;}

.but{
	display:inline-block;
	color:orange;
	font-size:60px;
	font-weight:900;
	border:5px orange solid;
	margin-top:20%;
}
```

views.py

```python
def index(request):
	return render(request,'products/index.html')
def game(request):
	context={
		"perses":Perses.objects.all(),
	}
	return render(request,'products/game.html',context)
```

urls.py

```python
urlpatterns = [
    path('admin/', admin.site.urls),
    path('',index,name='index'),
    path('game',game,name='game'),
```

По сути ничего не поменялось, просто появилась главная страница с кнопкой для перехода на страницу с игроками.

Теперь перейдем в папку приложения и создадим там файл urls.py, в который импортируем нужные модули и впишем следующее.

```python
from django.urls import path
from products.views import game
app_name='products'
urlpatterns = [
    path('',game,name='index'),
]
```

Перейдем в urls.py, но уже в папке с проектом.

```python
from django.contrib import admin
from django.urls import path,include
from products.views import index
from django.conf.urls.static import static
from django.conf import settings # Для доступа к переменным с media
urlpatterns = [
    path('admin/', admin.site.urls),
    path('',index,name='index'),
    path('products',include('products.urls',namespace='game')),
]
if settings.DEBUG: #Обращение к переменной DEBUG в файле settings.py
	urlpatterns+=static(settings.MEDIA_URL,document_root=settings.MEDIA_ROOT)
```

Тут мы импортировали include, чтобы подключить пространство имен. Теперь не страшно, что в проекте может быть несколько одноименных контроллеров. Осталось заменить в index.html ссылку - теперь она будет наследоваться от products.

```html
<a href="{%url 'products:index'%}"><div class="but">ПЕРЕЙТИ НА САЙТ</div></a>
```

## Фикстуры

Хранить базу данных в проекте можно, если проект расположен локально, но при отправке проекта куда-либо принято выгружать данные из базы в файлы, которые называются фикстурами и потом уже загружать из фикстуры данные в базу. Еще одна причина создавать фикстуры - делать бэкапы для предотвращения потери данных.

Выгрузка данных в фикстуру

```
manage.py dumpdata приложение.Класс таблицы >Имя файла.json
```

После, создать в папке приложения папку fixtures и переместить фикстуру в нее.

Лучше сделать бэкап проекта. Симитируем неприятную ситуацию, удалив дазу данных. Запустим сервер и увидим, что создалась пустая база данных. Теперь можно применить миграции и далее вписать следующую команду.

```
manage.py loaddata путь и имя файла
```

Осталось снова создать админа и можно пользоваться как обычно.

## Регистрация и авторизация

Стоит отметить, что в Django уже есть готовый набор для авторизации и регистрации, но он немного неполноценен, поэтому будем создавать свой.

Подкорректируем следующие файлы.

index.html

```html
<body>
	<div class="userblock">
		<div class="auth">Sign Up</div>
		<div class="auth">Log In</div>
		<div class="clearfix"></div>
	</div>
    <div class="cont">
        <a href="{%url 'products:index'%}"><div class="but">ПЕРЕЙТИ НА САЙТ</div></a>
    </div>
</body>
```

Дописать в styles.css

```css
.userblock{height:100px;color:#AAB6CD;}
.auth{
	background:#555B66;
	width:10%;
	height:50%;
	border:2px #AAB6CD solid;
	text-align:center;
	font-size:20px;
	font-weight:700;
	float:right;
	margin:20px 10px 0px 0px;
	padding:7px;
}
```

Создадим новое приложение users - в нем будет происходить регистрация и авторизация. Потом в новом приложении открыть models.py, импортировать в него так называемую абстрактную джанговскую модель и создать модель, которая будет так же наследоваться. Далее в модели создается поле с изображением, которого как раз нет в дефолтной модели.

models.py

```python
from django.db import models
from django.contrib.auth.models import AbstractUser
class User(AbstractUser):
	image=models.ImageField(upload_to='users-images',blank=True)
```

Так же стоит отметить, что эту модель мы переопределяем, так как она существует, пусть и в примитивном виде, поэтому нужно дописать еще одну служебную переменную AUTH_USER_MODEL='users.User' в settings.py. Здесь users - название приложения, а User - модель. Не забудьте добавить приложение в settings.py.

Теперь нужно создать миграцию. Если применить миграцию, то возникнет ошибка, поскольку пользователи уже есть в базе данных и происходит конфликт. Для исправления этой ошибки нужно удалить базу данных и подгрузить ранее созданную фикстуру. Если ее нет, то перед удалением БД нужно ее создать.

Если сейчас запустить сервер и войти в админку, то можно увидеть, что таблицы Users нет - это потому, что она была переопределена. Теперь ее надо зарегистрировать в файле admin.py, но уже в папке приложения users. После этого в админке появится приложение users с таблицей.

```python
from django.contrib import admin
from users.models import User
admin.site.register(User)
```

### Формы

В приложении users нужно создать папку templates, где будут храниться html шаблоны для авторизации и регистрации. Далее в ней создать папку users. В ней создадим файлы login.html и register.html. Далее как обычно открываем файл с контроллерами.

```python
from django.shortcuts import render
def login(request):
	return render(request,'users/login.html')
def register(request):
	return render(request,'users/register.html')
```

Создать urls.py.

```python
from django.urls import path
from users.views import login,register
app_name='users'
urlpatterns = [
    path('login',login,name='login'),
    path('register',register,name='register'),
]
```

И в главном urls.py создать пространство имен.

```python
path('users',include('users.urls',namespace='users')),
```







