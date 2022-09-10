# Основы C#

## Подготовка к работе

Для начала нужно установить интерпретатор c# - .net. После установки перейти в папку, где будет храниться код, зайти в консоль из папки и ввести команду

```
dotnet new console
```

После этого в папке появятся нужные файлы. Файл Program - это наша программа и с ней будем работать в дальнейшем. Откроем файл и посмотрим, что в нем.

```csharp
using System;

namespace c_Learning
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

Могут быть незначительные отличия, но код будем выполнять в методах класса. В нашем случае код выполняется в методе Main() класса Program.

Для запуска программы в консоли, с места расположения файла, нужно ввести команду.

```
dotnet run
```

## Часто используемые типы переменных

int(integer) - число  
float - дробь  
str(string) - строка  
bool(boolean) - логика

Объявление переменных бывает как такое

```csharp
int a = 10;
```
 Или такое
 
 ```csharp
 int a;
 ```
 
 ```csharp
 # Формат записи
 
 int a =1;
 float a = 1f; float a = 10.5f;
 bool a = true;
 ```
 
 Во втором случае значение переменной можно вписать в ходе программы.

## Простые математические действия

Действие|Символ|
---|---|
Сложение|+|
Вычитание|-|
Умножение|*|
Деление|/|

Сложение двух чисел
```csharp
static void Main(string[] args)
        {
            int a=3;
            int b=2;
            int c=a+b;
            
            Console.WriteLine(c);
        }
```

### Условия

Синтаксис условий

```csharp
if(условие)
{
    код
}
else
{
    код
}
```

### Цикл for

В цикл помещается код, который нужно выполнить несколько раз.

Пример цикла

```csharp
static void Main(string[] args)
        {
            
            for (int i=1;i<=5;i++)
            {
                Console.WriteLine(i);
            }
            
        }
```

Разберем цикл. В фигурных скобках выполняется код цикла, а в круглых записывается сам цикл.

1. int i=1 - начальное значение итерируемой переменной.
2. i<=5 - условие. В данном случае цикл будет выполняться, пока переменная не станет больше или равной 5.
3. i++ - аналог записи i=i+1. Счетчик, который увеличивает итерируемую переменную на 1.

### Цикл While

Пример цикла

```csharp
int a=0;
while(a<=10)
{
    Console.WriteLine(a);
    a++;
}
```

В данном примере пока a не станет больше или равной 10, цикл будет выполняться. Неосторожное использование цикла While может привести к созданию бесконечного цикла, что может привести к разным последствиям!

### Массивы и цикл foreach

Массив позволяют хранить в себе набор однотипных данных. Ниже показан не самый лучший, но простой способ создания массива.

```csharp
int [] nummer={1,2,5,7,8};
```

Цикл foreach позволит удобно перебрать элементы массива.

```csharp
foreach(int num in nummer)
{
    Console.WriteLine(num);
}
```
