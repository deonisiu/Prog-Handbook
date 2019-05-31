# C# Изучение

---
## Навигация


---
## Понятия
### 1) Составное форматирование - строка с индексированными местозаполнителями
* Индексированные местозаполнители соответствуют объектам из списка
* Поддерживают следующие методы :
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
Console.WriteLine("Name = {0}, age = {1}", name, age);
// Output : "Name = Fred, age = 33"
```

### 2) Интерполяция строк - внедрение любого выражения в строку 
* Интерполированная строка начинается с символа **$**
* Между символом **$** и знаком кавычки не должно быть пробелов
* *Интерполированное выражение* обозначается фигурными скобками `{выражение}`

---
## Основы

### Типы данных

#### 1) Краткий список

```c#
bool    - System.Boolean
byte    - System.Byte    (1 byte): 0...255
sbyte   - System.SByte   (1 byte):-128...127
short   - System.Int16   (2 bytes):-32.768...32.767
ushort  - System.UInt16  (2 bytes):0...65.535
int     - System.Int32   (4 bytes):-2.147.483.648...2.147.483.647 (int a = 5)
uint    - System.UInt32  (4 bytes):0...4.294.967.295 (uint a = 5u)
long    - System.Int64   (8 bytes):-9.223.372.036.854.775.808...9.223.372.036.854.775.807 (long a = 5l)
ulong   - System.UInt64  (4 bytes):0...18.446.744.073.709.551.615 (ulong a = 5ul)
float   - System.Single  (4 bytes):-3.4*10^38...3.4*10^38 (float a = 3.14f)
double  - System.Double  (8 bytes):+-5.0*10^-324...+-1.7*10^308 (double a = 3.14) (15 знаков после запятой)
decimal - System.Decimal (16bytes):+-1.0*10^-28...+-7.9228*10^28 (decimal a = 3.14m) (28 знаков после запятой)
char    - System.Char    (2 bytes)
string  - System.String  (набор символов Unicode)
object  - System.Object  (4-8 bytes 32x-64x)
```

#### 2) ***var*** - Неявная типизация
* При объявлении всегда задается значение
* Не может быть = null
```c#
var str = "Hello"; // верно
var c = 20;        // верно
var d;             // ошибка
var n = null;      // ошибка
```

### Консольный вывод

#### 1) Простой вариант
```c#
string name = "Tom";
int age = 22;
double height = 1.7;
Console.WriteLine($"Имя: {name} Возраст: {age} Рост:{height}м");
```

#### 2) Интерполяция