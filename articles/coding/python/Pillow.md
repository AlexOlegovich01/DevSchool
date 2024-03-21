# Pillow

В этом материале речь пойдет о модуде **pillow**, который используется для обработки изображений и создания оных. 

Открытие изображения

```python
from PIL import Image
im = Image.open("hopper.ppm")
```
При открытии можно не указывать формат файла. 

**im.format** - формат изображения.  
**im.size** - размер. Возвращается в виде кортежа. 
**im.mode** - цветовой режим.  
**im.show** - показывает изображение.  
**im.save("имя.расширение")** - сохраняет в файл.

## Редактирование изображений

Для извлечения прямоугольной части из картинки используется метод `crop()`

```python
cr=img.crop((x1,y1,x2,y2))
```

Обратите внимание, что здесь x1 и y1 - верхняя левая координата, а x2 и y2 - правая нижняя.

Изменить размер картинки - то есть сжать или расширить.

```python
a=img.resize((64,64))
a=im.transpose(Image.Transpose.FLIP_TOP_BOTTOM) # Отразить по вертикали
a=im.transpose(Image.Transpose.FLIP_LEFT_RIGHT) # Отразить по вертикали
a=im.transpose(Image.Transpose.ROTATE_90) # Повернуть на 90 градусов
a=im.transpose(Image.Transpose.ROTATE_180) # Повернуть на 180 градусов
a=im.transpose(Image.Transpose.ROTATE_270) # Повернуть на 270 градусов
a=im.convert("L") # Делает картинку черно-белой. "RGB" - цветной.
```

## Фильтры

На картинки можно налаживать фильтры.

```python
im=im.filter(ImageFilter.BLUR)
im=im.filter(ImageFilter.EDGE_ENHANCE)
im=im.filter(ImageFilter.CONTOUR)
im=im.filter(ImageFilter.DETAIL)
im=im.filter(ImageFilter.EDGE_ENHANCE_MORE)
im=im.filter(ImageFilter.EMBOSS)
im=im.filter(ImageFilter.FIND_EDGES)
im=im.filter(ImageFilter.SHARPEN)
im=im.filter(ImageFilter.SMOOTH)
im=im.filter(ImageFilter.SMOOTH_MORE)
```

## Режимы отображения

Маркировка|Описание
---|---
1|Однопиксельный формат. 1 пиксель на байт
L|8 битные. Оттенки серого
P|То же, что и предыдущий режим, но с использованием палитры цвета.
RGB|Цветное изображение
RGBA|Цветное изображение с альфа каналом
CNYK|Изображение с разделением цвета
YCbCr|Формат цветного видео
LAB|Цветовое пространство LAB
HSV|Hue Saturation Value
I|Цветные пиксели со знаком
F|Цветные пиксели с знаком с плавающей запятой

## Используемые методы

Создать новое изображение

```python
im3=Image.new('цветовой_режим',(разрешение))
```

Создать фрактал Мандельброта

```python
im=Image.effect_mandelbrot((разрешение),(0,0,1,1),число_качества)
```

## Методы получения свойств

```python
print(im.getbands()) #Возвращает режим изображения
print(im.getbbox()) #Возвращает координаты изображения
print(list(im.getdata())) #Возвращает список кортежей всех цветов
print(im.getexif()) # Возвращает словарь с exif данными
print(im.getpixel((координаты))) # Возвращает RGB пикселя
print(im.filename) # Возвращает имя картинки
print(im.format) # Возвращает формат картинки
print(im.mode) # Возвращает режим картинки
print(im.size) # Возвращает разрешение картинки
print(im.width) # Возвращает ширину картинки
print(im.height) # Возвращает высоту картинки
```

## ImageCrops()

```python
from PIL import Image,ImageChops
```

```python
im=ImageChops.add(картинка1,картинка2) # Смешивает картинки
im=ImageChops.add_modulo(картинка1,картинка2) # Смешивает картинки
im=ImageChops.darker(картинка1,картинка2) # Смешивает картинки
im=ImageChops.difference(картинка1,картинка2) # Смешивает картинки
im=ImageChops.difference(картинка1,картинка2) # Смешивает картинки
```

## ImageColor

```python
print(ImageColor.getrgb('цвет')) # Возвращает RGB цвета
print(ImageColor.getcolor('цвет','режим')) # Возвращает цвет в стиле указанного ражима
```

## ImageDraw

Этот модуль нужен для исования

Вот шаблон использования данного модуля. В этом примере рисует эллипс

```python
from PIL import Image,ImageDraw
im=Image.new('режим',(разрешение),'цвет') # Создать новую картинку
dr=ImageDraw.Draw(im) # Создать объект рисования
dr.ellipse((4_координаты),'цвет') # Рисует эллипс
im.show() # Показывает картинку
```

### Нарисовать эллипс

```python
dr.ellipse((4_координаты),'цвет')
```

Параметры
outline='цвет' - цвет контура
fill='цвет' - цвет заливки
width=число - толщина контура

### Нарисовать линию

```python
dr.line((4_координаты))
```

fill='цвет' - цвет
width=число - толщина

### Нарисовать пиксель

```python
dr.point((1,1))
```

fill='цвет' - цвет

### Нарисовать полигон

```python
dr.polygon((координаты))
```

Нужно передать координаты всех точек.

fill='цвет' - цвет
width=число - толщина контура
outline='цвет' - цвет контура

### Правильный прямоугольник

```python
dr.regular_polygon((x,y,r))
```

r - радиус
x,y - координаты центра
n_sides - количество углов
fill='цвет' - цвет
width=число - толщина контура
outline='цвет' - цвет контура
rotation - угол поворота

### Прямоугольник

```python
dr.rectangle((4_координаты))
```

fill='цвет' - цвет
width=число - толщина контура
outline='цвет' - цвет контура