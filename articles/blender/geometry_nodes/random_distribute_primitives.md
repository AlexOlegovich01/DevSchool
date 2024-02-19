# Рандомное распределение примитивов

1. Создать плоскость и добавить на нее новую геоноду.
2. Добавить ноду Distribute Points on Faces.
3. После нее добавить ноду Instance on Points. Поставить галочку Pick Instance.
4. В InstanceIndex[Instance on Points] соединить с [Random Value]Value. Тип выставить в Integer. А Instance[Instance on Points] соединить с [Join Geometry]Geometry. Это по сути и есть коллекция. На вход Geometry подаются примитивы. Разберем лишь один, все остальные по аналогии цепляем на вход Join Geometry.
5. В Geometry[Join Geometry] соединить с [Instance on Points]Instances. Points[Instance on Points]+[Mesh Line]Mesh. Здесь Count=1, все остальное не трогать. Instances[Instance on Points]+[Нужный меш примитив]Mesh.