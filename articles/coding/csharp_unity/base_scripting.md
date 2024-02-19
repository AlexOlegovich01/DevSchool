# Базовый скриптинг

## Содержание

- [Методы скриптов](#Методы-скриптов)
- [2D проект](#2D-проект)
  - [Установка начального положения игрока](#Установка-начального-положения-игрока)
  - [Движение игрока по прямой](#Движение-игрока-по-прямой)
  - [Взаимодействие с другими объектами](#Взаимодействие-с-другими-объектами)
  - [OnTrigger2D и OnCollision2D](#OnTrigger2D-и-OnCollision2D)
- [Коррутины](#Коррутины)
- [Raycast](#Raycast)
- [Управление персонажем](#Управление-персонажем)
  - [Прыжки](#Прыжки)
- [События](#События)
  - [OnEnable и OnDisable](#OnEnable-и-OnDisable)
  - [OnBecameVisible и OnBecameInvisible](#OnBecameVisible-и-OnBecameInvisible)
  - [OnApplicationQuit](#OnApplicationQuit)
  - [OnCollision](#OnCollision)
  - [OnDestroy](#OnDestroy)
  - [OnMouse](#OnMouse)
  - [OnParticle](#OnParticle)
  - [OnTrigger](#OnTrigger)
- [Другие методы](#Другие-методы)
  - [Instantiate](#Instantiate)
  - [Destroy](#Destroy)
  - [DontDestroyOnLoad](#DontDestroyOnLoad)

## Методы скриптов [Назад](#)

- Start - запускается в момент создания объекта в игре.
- Update - выполняется каждый кадр.

## 2D проект [Назад](#)

В 2D проекте игровые элементы - это спрайты, но на них так же может действовать физика, но в двумерном пространстве. По горизонтали идет ось X, по вертикали - Y.

1. Добавим 2 спрайта - Floor и Player. Разместим игрока над полом.
2. Добавим на них компоненты коллайдер 2д. Это нужно, чтобы объекты не проходили сквозь друг друга.
3. Для Player добавим RigidBody и запустим игру.

### Установка начального положения игрока [Назад](#)

1. Создать скрипт, в нем написать этот код

```csharp
void Start()
    {
        transform.position = new Vector2(0, 10);
    }
```

2. Повесить скрипт на Player.

### Движение игрока по прямой [Назад](#)

1. Создать скрипт. В нем написать код.

```csharp
void Update()
    {
        transform.Translate(new Vector2(1*Time.deltaTime,0));
    }
```

2. Повесить скрипт на Player.

### Взаимодействие с другими объектами [Назад](#)

1. Добавим новый объект и назовем его Bonus - это будет что-то типа жизней или монет - да все, что угодно.
2. Создадим новый скрипт и повесим его на Bonus.

```csharp
public GameObject PlayerForDestroy;
void Update()
{
    if (PlayerForDestroy.transform.position.x>= transform.position.x)
    {
        Debug.Log("Бонус взят!");
    }
}
```

Обратите внимание на то, как мы объявили переменную. public указывает на то, что переменную можно менять в инспекторе.
3. В инспекторе бонуса видим скрипт, а в нем есть поле, которое называется так, как и переменная. Теперь перетащем префаб игрока в это поле. 

При запуске игры видим появившееся сообщение при достижении игрока центра бонуса.

### OnTrigger2D и OnCollision2D [Назад](#)

Обработка событий столкновений и взаимодействий. Если речь идет о 3D проекте, то окончание 2D ставить не нужно.

#### OnCollisionEnter2D [Назад](#)

Создадим скрипт и повесим его на игрока. При запуске игры увидим сообщение при столкновении игрока с другими телами.

```csharp
void OnCollisionEnter2D(Collision2D col)
{
    Debug.Log("Finish");
}
```

#### OnTriggerEnter2D [Назад](#)

Нижеприведенный скрипт нужно закинуть на объект, который будет триггером, например бонус. В объекте должен быть коллайдер, а в нем поставлена галочка Is Trigger.

```csharp
void OnTriggerEnter2D(Collider2D other)
{
    Debug.Log("Finish");
}
```

## Коррутины [Назад](#)

Коррутина - скрипт, который обеспечивает задержку во времени.

```csharp
float sp = 0.2f;
void Start()
{
    transform.position = new Vector2(-10, 10);
}

void Update()
{
    transform.Translate(new Vector2(sp*Time.deltaTime,0));
    if (transform.position.x>-6)
    {
        StartCoroutine(Speed()); /*Запуск коррутины*/
    }
}
IEnumerator Speed() /*Коррутина*/
{
    sp = 2; /*Во время срабатывания*/
    yield return new WaitForSeconds(1); /*Продолжительность работы*/
    sp = 0.2f; /*По истечении времени*/
}
```

## Raycast [Назад](#)

Речь пойдет о луче, который используется как прицел в играх и для других похожих вещей.

### Имитация прицеливания [Назад](#)

1. Создадим 3д проект, в нем создадим объект, который будет типа нашей целью.
2. Создать скрипт и повесить на камеру.

```csharp
public float rayDistance; /*Длина луча*/
void Update()
{
    Ray ray = Camera.main.ScreenPointToRay(Input.mousePosition); /*Получаем лучь объекта из позиции мыши*/
    Debug.DrawRay(transform.position, ray.direction * rayDistance); /*Выполняет рисование луча*/
    //transform.position - положение камеры
    //ray.direction - направление луча
    if (Input.GetMouseButtonDown(0)) /*Если нажата ЛКМ*/
    {
        if (Physics.Raycast(ray)) /*Если луч попадает в цель*/
        {
            Debug.Log("Вы попали в цель!");
        }
    }
}
```

3. При запуске игры, если щелкнуть ЛКМ по цели, в консоли появится сообщение. Если не выключать режим игры и перейти в вкладку сцены, то луч мы не видим. Чтобы его увидеть, нужно установить значение для публичной переменной rayDistance.
4. Есть проблема. Наш код реагирует на то, куда указывает луч, но, если длина луча не достигает цели, все равно выводится сообщение в консоль. Давайте сделаем так, чтобы сообщение выводилось только в том случае, когда длина луча достаточна, чтобы достигнуть цели.

```csharp
if (Physics.Raycast(ray,rayDistance))
```

5. Теперь поговорим об определении, в какой именно объект мы стреляем. Этого можно достигнуть при использовании переменной типа RaycastHit.

```csharp
RaycastHit hit;
if (Input.GetMouseButtonDown(0)) /*Если нажата ЛКМ*/
{
    if (Physics.Raycast(ray,out hit)) /*Если луч попадает в цель*/
    {
        Debug.Log("Вы попали в цель!"+hit.transform.position);
    }
}
```

В данном случае выведутся координаты того объекта, куда стреляли, но можно вывести и другие результаты, например имя.

```csharp
Debug.Log("Вы попали в цель!"+hit.collider.gameObject.name);
```

Или даже менять параметры

```csharp
if (Physics.Raycast(ray,out hit)) /*Если луч попадает в цель*/
{
    hit.collider.gameObject.name = "R.I.P";
}
```

6. Так же можно получать данные нескольких объектов, собрав их в массиве, если луч пересекает несколько объектов.

```csharp
RaycastHit[] hits;
if (Input.GetMouseButtonDown(0)) /*Если нажата ЛКМ*/
{
    hits = Physics.RaycastAll(ray);
    foreach (RaycastHit hit in hits)
    {
        Debug.Log(hit.transform.position);
    }
}
```

## Управление персонажем [Назад](#)

**ПРИМЕЧАНИЕ!  
Если создается 3D проект, то вместо Vector2 ставим Vector3 и убираем из методов приписку 2D.**

Создадим простой скрипт, с помощью которого можно перемещать персонажа влево и вправо.

```csharp
float speed = 1; /*Переменная для скорости*/
float speedMode; /*Направление персонажа*/

void FixedUpdate()
{
    if (Input.GetKey(KeyCode.D)) /*Если нажата D*/
    {
        speedMode = speed; /*Направление вправо*/
    }
    else if (Input.GetKey(KeyCode.A)) /*Если нажата A*/
    {
        speedMode = -speed; /*Направление влево*/
    }
    transform.Translate(new Vector2(speedMode, 0)*Time.deltaTime); /*Как раз перемещение персонажа*/
    speedMode = 0; Сброс скорости на 0, когда ничего не нажато

}
```

Теперь нужно сделать так, чтобы игрок смотрел в том направлении, в котором идет движение. Под объявленными переменными скорости, объявим еще 2, которые отвечают за Scale.

```csharp
float beginScale; /*Начальный размер игрока*/
float scale; /*Размер игрока*/
```

Суть в том, что,когда меняем размер на то же значение, но со знаком минус, объект инвертируется, то есть в нашем случае смотрит в другую сторону. Теперь надо в методе Start получить оригинальный размер игрока и записать его в переменную.

```csharp
void Start()
    {
        beginScale = transform.lossyScale.x;
    }
```

Теперь FixedUpdate немного преобразовался.

```csharp
void FixedUpdate()
{
    if (Input.GetKey(KeyCode.D))
    {
        speedMode = speed;
        scale = beginScale; /*Обычный размер*/
    }
    else if (Input.GetKey(KeyCode.A))
    {
        speedMode = -speed;
        scale = -beginScale; /*Инверсированный размер*/
    }
    transform.localScale = new Vector2(scale, transform.lossyScale.y); /*Как раз изменение размера*/
    transform.Translate(new Vector2(speedMode, 0)*Time.deltaTime);
    scale = beginScale; /*В любом случае переходит в начальный размер*/
    speedMode = 0;
}
```

### Прыжки [Назад](#)

Для удобства создадим новый скрипт. Объявим вне методов 3 переменные.

```csharp
float jump; /*Величина прыжка*/
Rigidbody rb; /*Переменная компонента RigidBody*/
bool mode; /*Переключатель*/
```

Получим компонент Rigidbody.

```csharp
void Start()
{
    rb = GetComponent<Rigidbody2D>();
}
```

Можно было бы просто вызвать условие нажатия клавиши для прыжка в методе FixedUpdate, но возникнет проблема - игрок будет прыгать не всегда. Объясняется это тем, что метод Update вызывается каждый кадр, а метод FixedUpdate - нет. Поэтому будем вызывать проверку в Update и вызывать прыжок в FixedUpdate. Вот тут и пригодится переменная переключатель.

```csharp
void Update()
{
    if (Input.GetKeyDown(KeyCode.W))
    {
        mode=true;
    }
}
```

Далее следует сбросить переключатель и выполнить прыжок в FixedUpdate, если нажата кнопка прыжка.

```csharp
void FixedUpdate()
{
    if (mode)
    {
        mode=false;
        rb.AddForce(new Vector2(0, jump), ForceMode2D.Impulse);
    }
}
```



Теперь камеру запихнуть в игрока, чтоб она была дочерним элементом. Но и сейчас есть проблема - при прыжке изображение может заваливаться. Чтобы такого не было, в RigidBody игрока нужно поставить констреинт на ось Z.

Игрок может подпрыгивать, когда находится в воздухе. Это нужно тоже исправить. Для начала надо создать еще одну булеву переменную вне методов. Она будет активна, когда игрок находится на поверхности.

```csharp
bool isGrounded;
```

Дополнить строку условия нажатия клавиши прыжка.

```csharp
if (Input.GetKeyDown(KeyCode.W) && isGrounded)
```

Далее нужно добавить 2 метода. OnCollisionEnter2D обрабатывает соьытия физического взаимодействия с объектом, а метод OnCollisionExit2D обрабатывает, что будет, когда объекты перестают взаимодействовать.

```csharp
void OnCollisionEnter2D(Collision2D col)
{
    if(col.gameObject.tag=="Ground")
    {
        isGrounded=true;
    }
}
void OnCollisionExit2D(Collision2D col)
{
    if(col.gameObject.tag=="Ground")
    {
        isGrounded=false;
    }
}
```

Обязаельно проставить всем поверхностям тег. В нашем случае - это тег Ground.

Небольшое пояснение по коду. Активная переменная isGrounded означает, что игрок стоит на поверхности. В условии сказано, что если кнопка прыжка нажата и игрок стоит на поверхности, значит выполняется физика прыжка. А когда игрок находится в воздухе, переменная isGrounded переходит в отрицание, которое не соответствует условию.

## События

### OnEnable и OnDisable [Назад](#)

Эти события срабатывают, когда объект активен или неактивен.

```csharp
void OnEnable()
{
    // Действие, когда объект активен
}
```

```csharp
void OnDisable()
{
    // Действие, когда объект неактивен
}
```

### OnBecameVisible и OnBecameInvisible [Назад](#)

**OnBecameVisible** вызывается, когда объект попадает в поле зрения камеры. **OnBecameInvisible** вызывается, когда объект покидает поле видимости камеры.

```csharp
void OnBecameVisible()
{
    // Действие
}
```

```csharp
void OnBecameInvisible()
{
    // Действие
}
```



### OnApplicationQuit [Назад](#)

Это событие вызывается при закрытии игры.

```csharp
void OnApplicationQuit()
{
    Действие
}
```

### OnCollision [Назад](#)

Эти методы возникают при физическом взаимодействии объектов. Для начала нужно назначить на объекты компоненты коллайдеров и твердого тела.

#### OnCollisionEnter

Событие вызывается в момент столкновения объекта.

```csharp
void OnCollisionEnter(Collision collision)
{
    // Действие
}
```

Для 2D используется OnCollisionEnter2D

#### OnCollisionExit

Событие вызывается когда объект перестает контактировать.

```csharp
void OnCollisionExit(Collision other)
{
    // Действие
}
```

Для 2D используется OnCollisionExit2D

#### OnCollisionStay

Событие вызывается когда объект перестает контактировать.

```csharp
void OnCollisionStay(Collision collisionInfo)
{
    // Действие
}
```

Для 2D используется OnCollisionStay2D

### OnDestroy [Назад](#)

Это событие срабатывает при уничтожении объекта

```csharp
void OnDestroy()
{
    // Действие
}
```

### OnMouse [Назад](#)

Дальнейшие события отвечают за поведение мыши.

#### OnMouseDown

Вызывается, если щелкнуть мышью по коллайдеру объекта

```csharp
void OnMouseDown()
{
    // Действие
}
```

#### OnMouseDrag

Вызывается, если щелкнуть и зажать мышь по коллайдеру объекта.

```csharp
void OnMouseDrag()
{
    // Действие
}
```
#### OnMouseEnter

Вызывается, если мышь входит в коллайдер объекта.

```csharp
void OnMouseEnter()
{
    // Действие
}
```
#### OnMouseOver

Вызывается, если мышь находится на коллайдере объекта

```csharp
void OnMouseOver()
{
    // Действие
}
```
#### OnMouseExit

Вызывается, если мышь выходит из коллайдера объекта.

```csharp
void OnMouseExit()
{
    // Действие
}
```

#### OnMouseUp

Вызывается, если кнопка мыши была нажата на коллайдере объекта и потом отжата. Обратите внимание, что, если после нажатия мышь переместить в другое место, событие так же сработает.

```csharp
void OnMouseUp()
{
    // Действие
}
```

#### OnMouseUpAsButton

Вызывается, если кнопка мыши была нажата на коллайдере объекта и потом отжата. Обратите внимание, что, если после нажатия мышь переместить в другое место, событие не сработает.

```csharp
void OnMouseUpAsButton()
{
    // Действие
}
```

### OnParticle [Назад](#)

Эти события отвечают за поведение систем частиц.

#### OnParticleTrigger

Событие возникает при взаимодействии частицы с коллайдером объекта. В системе частиц должна стоять галочка Trigger.

```csharp
void OnParticleTrigger()
{
    // Действие
}
```

### OnTrigger [Назад](#)

Эти события возникают при взаимодействии с триггерами. Объект, который выступает в роли триггера, должен иметь коллайдер и активную галочку в нем IsTrigger. На объекте, который будет входить в триггер должен стоять компонент RigidBody.

#### OnTriggerEnter

Вызывается, если объект входит в триггер.

```csharp
void OnTriggerEnter()
{
    // Действие
}
```

Для 2D используется OnTriggerEnter2D.

#### OnTriggerEnter

Вызывается, если объект входит в триггер.

```csharp
void OnTriggerEnter()
{
    // Действие
}
```

Для 2D используется OnTriggerEnter2D.

#### OnTriggerExit

Вызывается, если объект выходит из триггера.

```csharp
void OnTriggerExit()
{
    // Действие
}
```

Для 2D используется OnTriggerExit2D.

#### OnTriggerStay

Вызывается, если объект находится в триггере.

```csharp
void OnTriggerStay()
{
    // Действие
}
```

Для 2D используется OnTriggerStay2D.

## Другие методы

### Instantiate [Назад](#)

Позволяет создавать объекты из скрипта.

Создание объекта

```csharp
public GameObject obj; // То, что нужно спавнить
void Start()
{
    Instantiate(obj); // Спавн
}
```

Создание объекта с указанием его положения и кватерниона.

```csharp
public GameObject obj;
void Start()
{
    Instantiate(obj,new Vector3(0,0,0),Quaternion.identity);
}
```

### Destroy [Назад](#)

Этот метод нужен для уничтожения объектов.

```csharp
// Простое удаление объекта, на котором висит скрипт

void Метод()
{
    Destroy(gameObject);
}

// Уничтожение другого объекта

void Метод()
{
    public GameObject obj; // Сюда в проекте перетащить уничтожаемый объект
    Destroy(obj);
}

// Уничтожение не сразу

void Метод()
{
    public GameObject obj; // Сюда в проекте перетащить уничтожаемый объект
    Destroy(obj,10);
}

// Уничтожение текущего скрипта

void Метод()
{
    Destroy(this);
}

// Уничтожение компонента

void Метод()
{
    Destroy(GetComponent<BoxCollider>());
}
```

### DontDestroyOnLoad [Назад](#)

Данный пример еще не проверялся.

При переходе на новую сцену, все объекты из предыдущих сцен удаляются. DontDestroyOnLoad позволяет избежать этого. Так же не будут удаляться и дочерние объекты. Выполнение метода происходит в событии Awake.

```csharp
void Awake()
{
    DontDestroyOnLoad(this.gameObject);
}
```

## 3D проект

### Простейший контроллер управления мыши

Для реализации придется написать 2 скрипта - первый повесить на игрока, а второй на камеру. Камера должна быть дочерним объектом игрока. Скрипт, что на персонаже, будет отвечать за движение мышкой вправо/влево, а скрипт на камере будет отвечать за поворот вверх и вниз.


```csharp
// Для персонажа

private float mouseY;
public float Sens=100f;
void Update()
{
    mouseY=Input.GetAxis("Mouse X")*Sens*Time.deltaTime;
    transform.Rotate(new Vector3(0,mouseY,0));
}
```

```csharp
// Для камеры

private float mouseX;
public float Sens=100f;
void Update()
{
    mouseX=Input.GetAxis("Mouse Y")*Sens*Time.deltaTime;
    transform.Rotate(new Vector3(-mouseX,0,0));
}
```