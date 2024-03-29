# Материалы

# Содержание

- [Горячие клавиши](#Горячие-клавиши)
- [Введение в основы](#Введение-в-основы)
- [Создание материалов и способы применения](#Создание-материалов-и-способы-применения)
- [Шейдеры](#Шейдеры)
- [Текстуры](#Текстуры)
- [UV развертка](#UV-развертка)

Здесь рассмотрим особенности материалов и работы с нодами. Для раоты с нодами материалов используется **Shader Editor**.

## Горячие клавиши

|Сочетание клавиш|Описание
|----|----
|**Shift A**|Меню выбора нодов
|**H**|Сделать ноду компактной
|**Del, X**|Удалить ноду
|**Ctrl J**|Поместить несколько нодов в фрейм
|**Ctrl G**|Поместить выбранные

## Введение в основы

Все ноды разделены по группам. Есть шейдеры, есть текстуры, ноды обработки цвета и так далее. Дальше разберем некоторые группы подробнее.

**Shader** - здесь собраны все шейдеры. По сути это способ отрисовки всего остального и основа для любого материала.  
**Texture** - группа, где можно выбрать процедурные текстуры или загрузить конкретную картинку, или создать свою.  
**Color** - здесь все, что связано с обработкой и смешиванием цветов.  
**Vector** - различные ноды, которые определяют положение текстур, их отрисовку и так далее.  
**Converter** - ноды преобразования. Преобразуют одни данные в другие.  
**Search** - здесь можно искать ноды.

### Управление Shader Editor

Нажав Ctrl и проведя ПКМ по проводу, его можно перерезать. Если зажать Ctrl и зажать ЛКМ по гнезду входа, где есть соединение, можно отключить его от гнезда и переключить в другое. Щелкая по ноде и нажимая M, мы замораживаем ноду, фактически отключая ее. Колесо мыши масштабирует ноды. Ноду можно двигать мышкой или клавишей G и можно задать координату X или Y.

Поля, которые встречаются достаточно часто...

|Поле|Описание
|---|---
|**Color/Base Color**|Базовый цвет
|**Specular**|Влияние окружающей среды - отражения
|**Roughness**|Шероховатость
|**IOR**|Индекс преломления
|**Normal**|Вход для карт нормалей
|**Strength**|Интенсивность

## Создание материалов и способы применения

### 1 способ создания материала

1. Переходим в управление материалами.
2. Нажимаем New.
3. Здесь можно выбрать уже созданные материалы.
4. Можно и нужно переименовать материал и дать ему осмысленное имя.
5. Нажав на +, можно добавить еще один материал.
6. Нажав на значок щита, можно сохранить материал в памяти проекта. Таким образом он останется даже если его нигде не используют, а неиспользуемые материалы удаляются после закрытия программы.

### 2 способ создания материала

1. В Shader Editor нажать New. Появится стандартная связка материалов, которую можно изменить.
2. Рядом есть вкладка с слотами. Тут можно добавить материал, а дальше как и в предыдущем примере.

### Применение материала в режиме редактирования

Простой пример применения нескольких материалов на одном объекте в режиме редактирования.
1. Создать плоскость и подразделить ее.
2. Перейти в Shader Editor, нажать New - появится новый материал.
3. Нажать на слот, затем на +, а потом нажать New. Изменить материал как угодно.
4. Теперь выделить любые полигоны, нажать на слоты, выбрать нужный материал и нажать Assign.

## Шейдеры

Разберем некоторые шейдеры

|Название|Описание
|---|---
|**Principled BSDF**|Стандартный шейдер, в котором уже есть по сути все необходимое
|**Emission**|Шейдер свечения
|**Glass BSDF**|Шейдер стекла
|**Glossy**|Шейдер глянца
|**Mix Shader**|Смешивает 2 шейдера
|**Principled Volume**|Универсальный шейдер для Volume. Использовать рендер Cycles.
|**Translucent BSDF**|Позволяет сделать просвечиваемые материалы, как у листвы.

## Текстуры

Бывают процедурными и в виде готовых или создаваемых картинок. Ниже рассмотрим разные процедурные текстуры, которые подключим в Base Color.

### Часто встречающиеся поля
|Наименование|Описание
|---|---
|**Scale**|Размер
|**Vector**|Положение текстуры
|**Detail**|Детализация
|**Color**|Цвет
|**Distortion**|Искажение

### Список часто используемых процедурных текстур
|Название|Описание|Socketы
|---|---|---
|**Brick**|Кирпичная кладка|**Offset** - отступ. **Mortar** - цемент. **Mortar Size** - расстояние между кирпичами. **Mortar Smooth** - сглаживание границ. **Bias** - смешивает цвета. **Brick Width** - ширина кирпичей. **Row Height** - высота кирпичей.
|**Checker**|Шахматный вид|---
|**Enviromment**|Окружение, например для HDRI текстур|---
|**Gradient**|Градиент|---
|**Image**|Готовая картинка|---
|**Magic**|Описание отсутствует|**Depth** - уровень детализации.
|**Musgrave**|Описание отсутствует|**Dimension** - добавляет зернистость. **Lacunarity** - компанует зернистость ближе к крупным островкам.
|**Noise**|Шум|---
|**Sky**|Процедурная текстура неба|**Sun Disc** - включить/выключить отображение Солнца. **Sun Size** - размер Солнца. **Sun Intensit** - интенсивность свечения Солнца. **Sun Elevation** - угол наклона Солнца. **Sun Rotation** - угол вращения Солнца. **Air** - воздух. **Dust** - пыль. **Ozone** - озон.
|**Voronoi**|Описание отсутствует|**Randomness** - рандомные углы.
|**Wave**|Волна|**Phase Offset** - движение волны

### Положение текстуры

Помимо добавления шейдеров и текстур, важную роль играет и положение материала на объекте. Для дальнейших действий понадобится аддон **Node Wrangler**, который поставляется вместе с Blender.

Для примера нужно создать текстуру, выделить ее и нажать Ctrl T. Появится 2 ноды, которые и определяют положение текстуры.

**Mapping** - способ размещения текстуры.  
**Texture Coordinate** - способ наложения текстуры.

Здесь можно поменять способ наложения, например, если есть UV развертка.

### Карты нормалей

Для реалистичности нужно, чтобы у материала был рельеф, но создание рельефа вручную требует много полигонов, что влечет за собой проблемы производительности и сложности при экспорте модели или анимации.

Пример
1. На дефолтном кубе есть материал, если его нет, то создать.
2. Добавить Noise Texture и Bump.
3. Color из Noise Texture добавить в Height у Bump, а выход Normal у Bump соединить с Normal у PrincipledBSDF.
4. Перейти в режим шейдинга или рендера и можно увидеть результат.

Есть 2 ноды для карт нормалей и работают они по разным принципам.  
Bumo - преобразует изображение в карту нормалей. 
Normal Map - работает именно с картами нормалей.

## UV развертка

Для наложения текстуры меш нужно развернуть на плоскости. Делается это при помощи создания швов и разворачивании меша.

### Знакомство с UV Editor

Развертка будет отображаться в редакторе в том случае, если в вьюпорте выбран режим редактирования и выделены развернутые части.

В редакторе развертки нажмем на Owerlays. Здесь находятся настройки отображения развертки. Параметр Display Stretch показывает искажения развертки. Синий цвет - искажений нет. Другими словами - это идеальная развертка, но все индивидуально. Так же в Owerlays можно изменить способ отображения ребер.

### Порядок действий для UV развертки

1. В режиме выделения ребер выбираем швы.
2. Жмем **ПКМ** и выбираем **Mark Seam**.
3. Выделяем весь меш и жмем **U - Unwrap**. Все - развертка готова.
4. Выставляем в **Texture Coordinate** наложение **UV**.

[:rewind:**Вернуться назад**](../../../README.md)