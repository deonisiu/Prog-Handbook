# C# Изучение

---
## <a name="0">Навигация</a>
* [Понятия](#1)
	* [Составное форматирование](#1_1)
	* [Интерполяция строк](#1_2)
* [Основы](#2)
	* [Типы данных](#2_1)
      * [Краткий список](#2_1_1)
      * [***var*** неявная типизация](#2_1_2)
      * [Преобразование типов](#2_1_3)
      * [Инкремент(декремент)](#2_1_4)
	* [Логические операции](#2_2) (`&, |, ^, ~, <<, >>`)
	* [Операции присваивания](#2_3)
	* [Преобразования базовых типов](#2_4)
	* [Условные логические операции](#2_5) (`|, ||, &, &&, !, ^`)
	* [Условные конструкции](#2_6)
	* [Циклы](#2_7)
	* [Массивы](#2_8)
      * [Многомерные массивы](#2_8_1)
      * [Простой перебор двумерного массива](#2_8_2)
      * [Перебор двум.мас. по каждой строке столбца](#2_8_3)
      * [Массив массивов (зубчатый массив)](#2_8_4)
	* [Методы](#2_9)
      * [Сокращенная запись методов](#2_9_1)
      * [Параметры методов](#2_9_2)
      * [Передача параметров (ref, out)](#2_9_3)
      * [Массив параметров (params)](#2_9_4)
	* [Рекурсивные фун-ции](#2_10)
	* [Перечисления enum](#2_11)
	* [Кортежи](#2_12)
      * [Использование кортежей в функциях](#2_12_1)
* [Классы (ООП)](#3)

---
## [&uarr;](#0)  <a name="1">Понятия</a>
### [&uarr;](#0)  <a name="1_1">1) Составное форматирование - строка с индексированными местозаполнителями</a>
* Индексированные местозаполнители `{0}` соответствуют объектам из списка `name`
* Поддерживают следующие **методы** :
```php
Console.WriteLine
String.Format
StringBuilder.AppendFormat
TextWriter.WriteLine
StreamWriter
HtmlTextWriter
Debug.WriteLine
Trace.TraceError
Trace.TraceInformation
Trace.TraceWarning
TraceSource.TraceInformation
```
* Пример :
```c#
string name = "Fred";
int age = 33;
Console.WriteLine("Имя = {0}, возраст = {1}", name, age);
// Output : "Имя = Fred, возраст = 33"
```

### [&uarr;](#0)  <a name="1_2">2) Интерполяция строк - внедрение любого выражения в строку </a>
* Интерполированная строка начинается с символа **$**
* Между символом **$** и знаком кавычки не должно быть пробелов
* *Интерполированное выражение* обозначается фигурными скобками `{выражение}`
* Условный оператор заключается в круглые скобки `{(условный оператор)}`
* Примеры :
```c#
string name = "Tom";
int age = 22;
Console.WriteLine($"Hello, {name}! Your age is {age}"); // стандартная интерполяция
Console.WriteLine($"{name} is {age} year{(age == 1 ? "true" : "false")} old."); // условный оператор
```

---
## [&uarr;](#0)  <a name="2">Основы</a>

### [&uarr;](#0)  <a name="2_1">Типы данных</a>

#### [&uarr;](#0)  <a name="2_1_1">1) Краткий список</a>

```c#
bool    - System.Boolean
byte    - System.Byte    (1 byte): 0...255
sbyte   - System.SByte   (1 byte):-128...127
short   - System.Int16   (2 bytes):-32.768...32.767
ushort  - System.UInt16  (2 bytes):0...65.535
int     - System.Int32   (4 bytes):-2.147.483.648...2.147.483.647 (int a = 5)
uint    - System.UInt32  (4 bytes):0...4.294.967.295 (uint a = 5u)
long    - System.Int64   (8 bytes):-9.223.372.036.854.775.808...9.223.372.036.854.775.807 (long a = 5l)
ulong   - System.UInt64  (8 bytes):0...18.446.744.073.709.551.615 (ulong a = 5ul)
float   - System.Single  (4 bytes):-3.4*10^38...3.4*10^38 (float a = 3.14f)
double  - System.Double  (8 bytes):+-5.0*10^-324...+-1.7*10^308 (double a = 3.14) (15 знаков после запятой)
decimal - System.Decimal (16bytes):+-1.0*10^-28...+-7.9228*10^28 (decimal a = 3.14m) (28 знаков после запятой)
char    - System.Char    (2 bytes)
string  - System.String  (набор символов Unicode)
object  - System.Object  (4-8 bytes 32x-64x)
enum		- System.Enum    (набор значений)
```

#### [&uarr;](#0)  <a name="2_1_2">2) ***var*** - Неявная типизация</a>
* При объявлении всегда задается значение
* Не может быть = null
```c#
var str = "Hello"; // верно
var c = 20;        // верно
var d;             // ошибка
var n = null;      // ошибка
```

#### [&uarr;](#0)  <a name="2_1_3">3) Преобразование типов</a>
```c#
string num = "35";
Convert.ToInt32(num) // к типу int
Convert.ToDouble(num) // к типу double
Convert.ToDecimal(num) // к типу decimal
```

#### [&uarr;](#0)  <a name="2_1_4">4) Инкремент(декремент)</a>
```c#
int i=0;
Console.WriteLine(i++ + ") i = " + i);   // out: 0) i = 1
Console.WriteLine(i++ + ") i = " + ++i); // out: 1) i = 3
```

### [&uarr;](#0)  <a name="2_2">Логические операции (&, |, ^, >>, <<)</a>
* ***&*** (логическое умножение) - поразрядное умножение в двоичном виде
```c#
int x = 2;       //  010 = 2
int y = 5;       //  101 = 5
                 // *
int sum = x & y; //  000 = 0
```
* ***|*** (логическое сложение) - поразрядное сложение в двоичном виде
```c#
int x = 3;       //  011 = 3
int y = 5;       //  101 = 5
                 // +
int sum = x | y; //  111 = 7
```
* ***^*** (логическое исключающее ИЛИ - XOR) - если значения разные ? 1 : 0
```c#
int x = 3;       //  011 = 3
int y = 5;       //  101 = 5
                 // ^
int sum = x ^ y; //  110 = 6
```
* ***~*** (логическое отрицание или инверсия)
```c#
int x = 12;       //  00001100 =  12
                  // ~
int result = ~x;  //  11110011 = -12
```
* ***>>, <<*** (операции сдвига разрядов)
```c#
int x = 4;            //   100  = 4
                      // <<
int result = x << 1;  //   1000 = 8

x = 4;                //   100 = 4
                      // >>
int result = x >> 1;  //   10  = 2
```

### [&uarr;](#0)  <a name="2_3">Операции присваивания</a>
```c#
int a = 10;
a += 10;    // = 20
a -= 4;     // = 16
a *= 2;     // = 32
a /= 8;     // = 4  =     100b
a <<= 4;    // = 64 = 1000000b
a >>= 2;    // = 16 =   10000b
a >>= 2;    // = 4  =     100b 
            // 6    =    *110b
a &= 6;     // = 4  =     100b
            // 9    =   +1001b
a |= 9;     // = 13 =    1101b
            // 15   =   ^1111b
a ^= 15;    // = 2  =    0010b
```

### [&uarr;](#0)  <a name="2_4">Преобразования базовых типов</a>
* Операции сложения(+) и вычитания(-) возвращают значение типа int, если нет типа данных больше чем int
```c#
byte a = 4;
byte b = a + 70;         // ошибка
byte b = (byte)(a + 70); // верно
``` 
* Расширяющие(неявное) преобразование [таблица](https://metanit.com/sharp/tutorial/pics/2.9.png) - дополнение разрядностей 

[Положительное число](https://metanit.com/sharp/tutorial/pics/2.7.png)
```c#
byte a = 4;   //         0000100b
ushort b = a; // 000000000000100b (a>0 дополнение нулями)
```
[Отричательное число](https://metanit.com/sharp/tutorial/pics/2.8.png)
```c#
sbyte a = -4; //         1111100b
short b = a;  // 111111111111100b (a<0 дополнение еденицами)
```
* Сужающие(явное) преобразование - в скобках указывается нужный тип данных 
```c#
ushort c = 4;      // 000000000000100b
byte d = (byte) c; //         0000100b
```
* Проверка на переполнение (***checked***) - выбрасывает исключение OverflowException
```c#
try {
	int a = 33;
	int b = 600;
	byte c = checked((byte)(a+b));
} catch (OverflowException ex) {}
```

### [&uarr;](#0)  <a name="2_5">Условные логические операции (`|, ||, &, &&, !, ^`)</a>
* Операции `&&, ||` и `&, |` возвращают одинаковый результат, но работают по разному
* Операции `&&, ||` работают до первого успеха/отказа (true/false)
* Операции `&, |` работают до конца в любом случае
```c#
int a = 3;
int b = 3;
bool c;
c = (a++ > 0 || b++ > 0); // a = 4, b = 3 (a-changed, b-not)
c = (a++ > 0 |  b++ > 0); // a = 5, b = 4 (a,b - changed)
c = (a++ >10 && b++ > 0); // a = 6, b = 4 (a-changed, b-not)
c = (a++ >10 &  b++ > 0); // a = 7, b = 5 (a,b - changed)
```
* Операция `!`(отрицания) меняет ***true*** на ***false*** и наоборот
* Операция `^`(XOR) дает ***true*** если операнды разные и ***false*** если одинаковые
```c#
bool a = true;  // a = true
bool b = !a;    // b = false
bool c = a ^ b  // c = true
bool d = a ^ !b // d = false
```

### [&uarr;](#0)  <a name="2_6">Условные конструкции</a>
* if/else
* switch напоминалка :
```c#
switch (value) {
	case 1:
		Console.WriteLine("1");
		break;
	case "Y":
		Console.WriteLine("Yes");
		break;
	default:
		Console.WriteLine("Default");
		break;
}
```
* Тернарная операция - `(condition) ? true : false;`
```c#
//             (condition) ?   true   :  false  ;
string result = (55 > 60)  ? "Wrong!" : "Right!"; // result = "Right!"
```

### [&uarr;](#0)  <a name="2_7">Циклы</a>
* for
* while
* do...while
* foreach - `foreach (тип_данных название_переменной in контейнер) {действия}`
```c#
int[] numbers = new int[] {1,2,3,4,5};

foreach (int i in numbers) {
	Consoole.WriteLine(i);
}
```

### [&uarr;](#0)  <a name="2_8">Массивы</a> [Примеры](https://metanit.com/sharp/tutorial/pics/array.png)
* ***Ранг***(rank): количиство измерений массива
* ***Длина измерения***(dimension length): длина отдельного измерения массива
* ***Длина массива***(array length): количество всех элементов массива
```php
// Квадратные скобки ставятся после типа переменной
int[] numbers;  // верно
int numbers2[]; // ошибка

// Размер массива не может быть указан в объявлении переменной
int[] numbers3;   // верно
int[2] numbers4;  // ошибка

// При создании массива размер массива указывается обязательно
int[] numbers3 = new int[2]; // верно
int[] numbers4 = new int[];  // ошибка

// Примеры правильного создания простого массива
int[] nums1 = new int[4] { 1, 2, 3, 5 };
int[] nums2 = new int[] { 1, 2, 3, 5 };
int[] nums3 = new[] { 1, 2, 3, 5 };
int[] nums4 = { 1, 2, 3, 5 };
```

#### [&uarr;](#0)  <a name="2_8_1">1) Многомерные массивы</a>
```c#
// Двухмерный массив
int[,] nums1;
int[,] nums2 = new int[2, 3];
int[,] nums3 = new int[2, 3] { { 0, 1, 2 }, { 3, 4, 5 } };
int[,] nums4 = new int[,] { { 0, 1, 2 }, { 3, 4, 5 } };
int[,] nums5 = new [,]{ { 0, 1, 2 }, { 3, 4, 5 } };
int[,] nums6 = { { 0, 1, 2 }, { 3, 4, 5 } };

// Трехмерный массив
int[,,] nums1 = new int[2, 3, 4];
```

#### [&uarr;](#0)  <a name="2_8_2">2) Простой перебор двумерного массива</a>
```c#
int[,] mas = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 }, { 10, 11, 12 } };
foreach (int i in mas)
    Console.Write($"{i} ");
Console.WriteLine();
// result : "1 2 3 4 5 6 7 8 9 10 11 12 "
```

#### [&uarr;](#0)  <a name="2_8_3">3) Перебор двумерного массива по каждой строке таблицы</a>
* Метод GetUpperBound(dimension) - возвращает индекс последнего элемента в размерности `dimension`
```c#
int[,] mas1 = { { 1, 2, 3 } };
int[,] mas2 = { { 1, 2, 3 }, { 4, 5, 6 } };
int[,] mas3 = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };
int[,] mas4 = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 }, { 10, 11, 12 } };

int[,] mas5 = { { 1, 3 }, { 4 } }; // Ошибка внутренний индекс не может быть разным 

// Индексация идет с 0
int n;
n = mas1.GetUpperBound(0); // = 0 - индекс последнего элемента
n = mas2.GetUpperBound(0); // = 1   в первой(0) мерности
n = mas3.GetUpperBound(0); // = 2
n = mas4.GetUpperBound(0); // = 3

n = mas1.GetUpperBound(1); // = 2 - индекс последнего элемента
n = mas2.GetUpperBound(1); // = 2   во второй(1) мерности
n = mas3.GetUpperBound(1); // = 2
n = mas4.GetUpperBound(1); // = 2

n = mas1.GetUpperBound(2); // Ошибка массив не имеет 3 мерности

// ----------------- Конечный перебор -------------------------
// Находим количество строк и столбцов в двухмерном массиве
int[,] mas = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 }, { 10, 11, 12 } };

int rows = mas.GetUpperBound(0) + 1;
int columns = mas.GetUpperBound(1) + 1;

for(int i=0; i<rows; i++) {
	for(int j=0; j<columns; j++) {
		Console.Write($"{mas[i,j]} \t");
	}
	Console.WriteLine();
}
```

#### [&uarr;](#0)  <a name="2_8_4">4) Массив массивов (зубчатый массив)</a>
* Две группы квадратных скобок `[][]` указывают на массив массивов
* Длина указывается только в первых скобках `[3][]`
* Размерность каждого подмассива может не совпадать
```c#
int[][] nums1 = new int[3][];
nums1[0] = new int[2] { 1, 2 };          // выделяем память для первого подмассива
nums1[1] = new int[3] { 1, 2, 3 };       // выделяем память для второго подмассива
nums1[2] = new int[5] { 1, 2, 3, 4, 5 }; // выделяем память для третьего подмассива

// В качестве подмасивов могут быть многомерные массивы
int[][,] nums2 = new int[3][,] 
{
    new int[,] { {1,2}, {3,4} },
    new int[,] { {1,2}, {3,6} },
    new int[,] { {1,2}, {3,5}, {8, 13} } 
};

// Перебор зубчатого массива
foreach(int[] row in nums1) {
	foreach(int number in row) {
		// code..
	}
}
```

### [&uarr;](#0)  <a name="2_9">Методы</a>
```c#
[модификатор] тип_возвращаемого_значения название_метода ([параметры])
{
	// тело метода
	return возвращаемое_значение; // возврат и выход из метода
}
```
#### [&uarr;](#0)  <a name="2_9_1">1) Сокращенная запись методов</a>
```c#
// -------- 1 ----------
// ВМЕСТО
static void SayHello() {
	Console.WirteLine("Hello");
}
// БУДЕТ
static void SayHello() => Console.WriteLine("Hello");

// -------- 2 ----------
// ВМЕСТО
static string GetHello() {
	return "hello";
}
// БУДЕТ
static string GetHello() => "hello";
```

#### [&uarr;](#0)  <a name="2_9_2">2) Параметры методов</a>
```c#
// name - обязательный параметр
// age  - не обязательный параметр

static void Display(string name, int age=20) {
    Console.WriteLine($"Name: {name}  Age: {age}");
}

Display("Tom", 24); // Name: Tom  Age: 24
Display("Tom");     // Name: Tom  Age: 20
 
    
```

#### [&uarr;](#0)  <a name="2_9_3">3) Передача параметров (ref, out)</a>
* Стандартно простые параметры передаются по значению
* Передача параметров по ссылке требует модификатор ***ref***
```c#
// параметр x передается по ссылке (ref)
static void Addition(ref int x, int y) => x += y;

int x = 10;
int y = 15;
Addition(ref x, y);   // вызов метода
Console.WriteLine(x); // x = 25
```
* Чтобы сделать параметры выходными используется модификатор ***out***
```c#
static void Sum(int x, int y, out int a) => a = x + y;

int x = 10;
int z;
Sum(x, 15, out z); // z = 25

// Методы с модификатором out обязательно должны присваивать значение out параметрам
static void Sum(int x, int y, out int out1) => y = x + out1; // Ошибка значение для out не задано 
static void Sum(int x, int y, out int out1) => out1 = x + y; // Верно 
```

#### [&uarr;](#0)  <a name="2_9_4">4) Массив параметров (params)</a>
* Используя ключевое слово ***params***, можно передавать неопределенное кол-во пар-ов
```c#
static void Addition(params int[] integers) {...}

int[] array = new int[] {1,2,3,4,5};

Addition(1, 2, 3);    // верно
Addition(1, 2, 3, 4); // верно
Addition(array);      // верно
Addition();           // верно
```

### [&uarr;](#0)  <a name="2_10">Рекурсивные фун-ции</a>
* Функция вызывающая сама себя, стремящаяся к базовому варианту.
```c#
// функция факториала
static int Factorial(int x) {
    if (x == 0) {
        return 1;
    } else {
        return x * Factorial(x - 1);
    }
};

// функция фиббоначчи
static int Fibonachi(int n) {
    if (n == 0) {
        return 0;
    }
    if (n == 1) {
        return 1;
    } else {
        return Fibonachi(n - 1) + Fibonachi(n - 2);
    }
}
```

### [&uarr;](#0)  <a name="2_11">Перечисления enum</a>
* ***enum*** - набор логически связанных констант
* Тип перечисление(default:int) указывается обязательно (byte, int, short, long)
* Стандартно каждому элементу присваивается целочисленное значение начиная с 0
```c#
// значения по умолчанию
enum Days : byte {
  Monday,    // = 0
  Tuesday,   // = 1
  Wednesday, // = 2
  Thursday,  // = 3
  Friday,    // = 4
  Saturday,  // = 5
  Sunday     // = 6
}

// значения явным образом
enum Operation
{ 
    Add = 2,      // = 2
    Subtract = 4, // = 4
    Multiply = 8, // = 8
    Divide = 16   // = 16
}

// использование
Operation operat;
operat = Operation.Add;
Console.WriteLine(operat);     // = "Add"
Console.WriteLine((int)operat) // = 2
```

### [&uarr;](#0)  <a name="2_12">Кортежи (c# v7.0)</a>
* Кортежи - удобный способ работы с набором значений
* Представляют набор значений, в круглых скобках
```c#
// создание кортежа c неявными типами
var tuple = (5, 10);

// обращение к кортежу
Console.WriteLine(tuple.Item1) // = 5
Console.WriteLine(tuple.Item2) // = 10
tuple.Item1 += 25;
Console.WriteLine(tuple.Item1) // = 30

// создание кортежа с явными типами
(int, int) tuple = (5, 10);
(string, int, double) person = ("Tom", 25, 81.236);

// создание кортежа с названиями полей
var tuple = (count:5, sum:10);
// обращение к полям
Console.WriteLine(tuple.count); // = 5
Console.WriteLine(tuple.sum);   // = 10

// кортеж без имени переменной в рамках метода или блока
var (name, age) = ("Tom", 23);
Console.WriteLine(name); // = "Tom"
Console.WriteLine(age);  // = 23

```

#### [&uarr;](#0)  <a name="2_12">1) Использование кортежей в функциях</a>
* Кортежи могут передоваться параметрами в метод
* Кортежи могут быть возвращаемым результатом функции
```c#
// передача кортежа в метод
private static void Tuple((string n, int a) tuple, int x) {
	string str = tuple.n;
	int num = tuple.a;
}

// возврат кортежа из функции
private static (int, int) GetValues() {
	var result = (1, 3);
	return result;
}
```

### [&uarr;](#0)  <a name="3">Классы (ООП)</a>
* Описанием ***объекта*** является ***класс***
* ***Объект*** представляет экземпляр ***класса***
* Вся функциональность класса выражена его :
	* ***Конструктором*** - `public Person() { name = "Tom"; age = 19; }`
	* ***Полями*** - `string name; int age;`
	* ***Свойствами*** - `public string Name { get; set; }`
	* ***Методами*** - `public getName() => this.name;`
	* ***Событиями*** - ???
```php
// ------------- Пример объявления класса Person + (поля, свойства, конструктор, метод)-------------
class Person {
  public string name; // поле name
  //public int age;   // поле age создается автоматически ниже

  public string Name {         // свойство для поля name
    get { return name };
    set { name = value }; 
  }
  public int Age { get; set; } // свойство для поля age (создает поле age)

  public Person() { name = "Неизвестно"; age = 18; } // конструктор

  public void GetInfo() { Console.WriteLine($"Имя: {name}  Возраст: {age}"); } // метод
}
```

#### Ключевое слово this в классах
* Слово ***this*** ссылается на текущий экземпляр класса
* Слово ***this*** в основном используется для :
	* ***1) Квалификации элементов***, скрытых одинаковыми именами
	* ***2) Передачи*** другим ***методам*** объекта в качестве параметра
	* ***3) Создания цепочки конструкторов (Constructor chaining)***
```php
// ------ 1) Квалификация элементов ------
// Конструктор
public SomeClass(string name, int age) {
	// присваиваем значение аргументов, полям класса
	this.name = name;
	this.age = age;
}

// ------ 2) Передача методам ------
// Метод1 внутри класса
public void method1() {
	// передача объекта класса в метод2 в виде параметра
	method2(this);
}
private void method2(SomeClass classObject) {
	// code..
}

// ------ 3) Создания цепочки конструкторов (Constructor chaining) ------
// --- Принцип работы Constructor chaining ---
// 1) Создание нескольких конструкторов
// 2) Вызов одного конструктора из другого : UserInfo() : this()

// class UserInfo; поля: Name, Family, Age
// создание "цепочки" конструкторов
public UserInfo() : this("None","None",0) {}
public UserInfo(UserInfo obj) : this(obj.Name, obj.Family, obj.Age) {}
public UserInfo(string Name, string Family, int Age) {
	this.Name = Name;
	this.Family = Family;
	this.Age = Age;
}

// Использование в программе
UserInfo ui1 = new UserInfo();
UserInfo ui2 = new UserInfo("Alex", "Green", 25);
UserInfo ui3 = new UserInfo(ui2);

// ЗАМЕЧАНИЕ : Начиная с версии .NET 4.0 цепочки можно заменить на необязательные аргументы

```

#### Инициализаторы объектов
* Передача в `{}` скобках значений доступным полям и свойствам объекта
```php
class Person() {
	public string name;
	public int age;
	private int height;
}

Person p = new Person { name = "Tom", age = 32 }; // верно
Person p = new Person { name = "Tom", age = 32, height = 160 }; // Ошибка! height-недоступен

```

#### Организация памяти в .NET [Пример](http://stormy-lake-9982.herokuapp.com/assets/Stack%20and%20Heap-0714abf8c6b49cc57365a4aafbba510c.png)
* Память делится на два типа
	* ***Стек*** - В стеке хранятся `типы значений` и `ссылки на адреса в куче`
	* ***Куча(heap)*** - В хипе хранятся `ссылочные типы` на которые указывают ссылки из ***Стека***
* Если из ***Стека*** удаляются все ссылки на объект, автоматический `сборщик мусора` удаляет объект из кучи и очищает память


#### Типы значений и ссылочные типы
* Типы значений :
	* Целочисленные типы (`byte, sbyte, char, short, ushort, int, uint, long, ulong`)
	* Типы с плавающей запятой (float, double)
	* decimal
	* bool
	* enum
	* Структуры (struct)

* Ссылочные типы :
	* Object
	* string
	* Классы (class)
	* Интерфейсы (interface)
	* Делегаты (delegate)

#### Передача параметров по значению и по ссылке (***ref***)
* Передача параметров :
	* ***По значению*** :
		* Передается копия ссылки на объект.
		* Изменяет поля и свойства объекта, но не сам объект.
	* ***По ссылке***(ключевое слово ***ref***) :
		* Передается сама ссылка на объект.
		* Изменяет как поля и свойства, так и сам объект.
```php
Person p = new Person { name = "Tom", age = 23 };

// ------ 1) Передача параметров по значению ------
ChangePerson(p);

public void ChangePerson(Person person) {
	person.name = "Alice";                           // Изменит в p.name Tom на Alice
	person = new Person { name = "Bill", age = 45 }; // Не изменит в p ничего
}

// ------ 2) Передача параметров по ссылке ------
ChangePerson(ref p);

public void ChangePerson(ref Person person) {
	person.name = "Alice";                           // Изменит в p.name Tom на Alice
	person = new Person { name = "Bill", age = 45 }; // Изменит весь объект p
}
```

#### Модификаторы доступа (допустимая область видимости)
* ***Пространства имен*** (`namespace`) не имеют ограничений доступа
* В C# применяются модификаторы :
	* ***public*** : Неограниченный доступ
	* ***private*** : Доступ ограничен содержащим типом
	* ***protected*** : Доступен из любого места в текущем классе или в производных классах
	* ***internal*** : Доступ ограничен текущей сборкой
	* ***protected internal*** : Доступен из текущей сборки и из производных классов
	* ***private protected*** (C# v7.2) : Доступен в текущем классе или производных, той же сборки
* Классы объявленные без модификатора по умолчанию имеют доступ ***internal***
* Классы созданные в `пространстве имен` и не вложенные в другие классы могут быть либо ***public***, либо ***internal***

<table>
	<tr>
		<th>Члены типа</th>
		<th>Доступность по умолчанию</th>
		<th>Варианты доступности</th>
	</tr>
	<tr>
		<td>enum</td>
		<td>public</td>
		<td>Нет</td>
	</tr>
	<tr>
		<td>class</td>
		<td>private</td>
		<td>Все</td>
	</tr>
	<tr>
		<td>interface</td>
		<td>public</td>
		<td>Нет</td>
	</tr>
	<tr>
		<td>struct</td>
		<td>private</td>
		<td>public, internal, private</td>
	</tr>
</table>

#### Свойства (специальные методы доступа)
* Доступ к полям класса - `get; set;`
```php
class Person {
  private string name;
  public string Name {
    get { return name; }
    set { name = value; } // value представляет передаваемое значение
  }
}
Person p = new Person();
p.Name = "Tom";          // вызывает Name.set
string perName = p.Name; // вызывает Name.get
```
* Доступ к полю может быть ограничен одним из методов `get` или `set`
```php
// --- только метод get ---
public string Name {   // поле name без метода set
  get { return name; } // можно получить, нельзя изменить
}
// --- только метод set ---
public int Age {       // поле age без метода get
  set { age = value; } // можно изменить, нельзя получить
}
```
* Модификатор доступа(МД) для ***свойства***
	* Можно установить только когда есть и `get` и `set`
	* Только один блок `get` или `set` может иметь МД, но не оба сразу
	* МД блока `get` или `set` должен быть более ограничивающим, чем МД ***свойства***
* Сокращенная запись свойств :
```php
private string name;

// эквивалентно public string Name { get { return name; } }
public string Name => name;
```

#### Автоматические свойства(АС)
* Сокращенное объявление АС :
	* Сокращает запись объявления свойств
	* Убирает необходимость объявления одноименных полей
```php
class Person {
  public string Name { get; set; } // АС Name + создание поля (string)name
  public int Age { get; set; }     // АС Age  + создание поля (int)age

  public Person(string name, int age) {
    Name = name;
    Age = age;
  }
}
```
* АС можно присвоить значения по умолчанию(инициализация АС) :
```php
public string Name { get; set; } = "Tom"; // name = "Tom"
public int Age { get; set; } = 23;        // age = 23
```
* АС с МД :
```php
public string Name { get; private set; }
```
* АС без блока set :
```php
public string Name { get; } = "Tom";
```

#### Перегрузка методов
* Перегрузка - методы с разной сигнатурой :
  * Количество параметров
  * Типы параметров
  * Порядок параметров
  * Модификаторы параметров
```php
public void Add(int a, int b) {}                        // сигнатура : Add(int, int)
public void Add(int a, int b, int c) {}                 // сигнатура : Add(int, int, int)
public int Add(int a, int b, int c, int d) {return int} // сигнатура : Add(int, int, int, int)
public void Add(double a, double b) {}                  // сигнатура : Add(double, double)
public void Add(ref int a, ref int b) {}                // сигнатура : Add(ref int, ref int)
```

#### Модификатор static (статические элементы СЭ)
* Статические поля, методы и свойства относятся ко всему классу
* Для обращения к СЭ не нужно создавать экземпляр класса.
* Для СЭ будет создаваться участок в памяти, общий для всех объектов класса. [Рисунок](https://metanit.com/sharp/tutorial/pics/static.png)
* Память для СЭ выделяется, даже если не создано ни одного объекта
...Статические свойства и методы...