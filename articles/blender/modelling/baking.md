# Запекание

## Запекание с объекта на объект

1. Скопировать нужный объект или создать копию. У второго объекта может быть меньше полигонов. Объекты должны находиться в одном месте.
2. На втором объекте удалить все материалы, назначить новый материал.
3. В Shader Editor добавить Image Texture и создать новое изображение.
4. В Edit Mode выделить весь объект, нажать U - Snart UV Project.
5. Рендер выставить в Cycles, в вкладке рендера спуститься к пункту Bake. Здесь поставить галочку в Selected to Active, развернуть, Ray Distance=0.05. Выбрать, что именно будем запекать.
6. Выделить Image Texture, затем высокополигональную модель, затем низкополигональную и нажать в вкладке рендера кнопку Bake.