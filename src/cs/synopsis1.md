# Конспект по курсу "Продвинутый C# Шаг1"

## Общии заметки

* ***Абстрагирование*** - отделение существенного от несущественного

## Основы ООП

### Абстракция
* Обобщение и сокрытие реализации
* Общее представление об объекте
* Сокрытие ненужных деталей реализации

### Инкапсуляция
* Сокрытие данных и состояний, от неправильного внешнего воздействия
* Упаковка(соединение) данных и функций в единый компонент(класс)

### Наследование
* Возможность создавать типы на основе других типов
* Расширение функционала на основе базового типа
* Не нужно использование повторного кода

### Полиморфизм подтипов
* Один интерфейс - множество реализаций
* Базовая абстракция(тип) которую реализуют другие типы
* Подтипы от базовой абстракции, определяющие свое поведение

## Синтаксис

### Классы и объекты
* Класс определяет тип
* Объект значение определенного типа
* Объект содержит поля и методы

### Нотация полей
* Поля с мод. ***public*** - С большой буквы без нижнего подчеркивания `Speed, Type, Health`
* Поля с мод. ***private*** - С маленькой буквы + нижнее подчеркивание `_speed, _type, _health`
```php
class Example {
  public int Speed;
  public float Health;
  private int _size;
  private string _type;
}
```

### Общая суть ***Инкапсуляции*** в C#
* Сокрытие прямого доступа к полям для избежания ввода недопустимых значений - ***private***
* Обращение к полям через методы, которые проверяют входные данные
* Полудоступ к данным через свойства : 1) только чтение - ***get*** 2) только запись - ***set***

### Конструктор
* Метод вызываемый при создании объекта класса
* Задает первоначальные настройки для объекта (значение полей, вызов начальных методов)
* Одноименное название с классом
* Может принимать параметры
* Может быть перегруженным
```php
class Example {
  public Example() {...}             // Конструктор класса Example
  public Example(int x, int y) {...} // Перегруженный конструктор с 2 параметрами 
}
```

### Выражение композиции и агрегации через конструктор
* При ***Агрегации*** - одна сущность содержит в себе другую, но не контролирует её время жизни
```php
class NPC {
  int x;
  public int GetX() {
    return x;
  }
}

// Renderer содержит в себе NPC
class Renderer {
  private NPC _npc;
  public Renderer(NPC npc) {
    _npc = npc;
  }
  public void Draw() {
    _npc.GetX();
  }
}

// Оба объекта создаются отдельно друг от друга
NPC npc = new NPC();
Renderer renderer = new Renderer(npc); 

// Объект renderer содержит в себе npc
// Но при этом не контролирует его время жизни
renderer = null; // Объекта renderer больше нет, но объект npc остался
```
* ***Композиции*** - одна сущность создает внутри себя другие сущности, общее время жизни
```php
// Car создает внутри себя Motor, который отдельно от Car не будет иметь смысла
class Car {
  class Motor {...}
  private Motor _motor;

  public Car() {
    _motor = new Motor();
  }
}

Car car = new Car(); // Motor будет создан автоматически внутри car
car = null;          // При удалении объекта car, объект _motor также удаляется
```

### Свойства
* Способ получения доступа к полям через ***get*** и ***set***
```php
class Example {
  private int _x;

  // 1) Стандартная запись свойства
  public int X {
    get { return _x; }  // получить поле _х
    set { _x = value; } // задать поле _х
  }

  // 2) Сокращенная запись свойства
  public int Y { get; set; }          // поле y создается автоматически
  public int Z { get; private set; }  // поле z можно читать извне но менять только внутри
}

// Использование
Example examp = new Example();
examp.X = 10;       // _x = 10
examp.Y = examp.X;  //  y = 10
examp.Z = examp.X;  //  Ошибка поле z нельзя изменить извне
```

### Деструкторы и сборка мусора(garbage collector)
* Сборка мусора удаляет все объекты из кучи, на которые в программе нет больше ссылок 
* При не удалении неиспользуемых объектов появляется "утечка памяти"
* При удалении объекта вызывается деструктор `~ClassName() {...}`
```php
class Example {
  // Конструктор
  public Example {...}

  // Деструктор
  ~Example() {
    Console.WriteLine("Destruct");
  }
}
```

### Наследование
* При наследовании производные классы не имеют доступа к ***private*** полям и методам
* Производные классы имеют доступ к ***public*** и ***protected*** полям базового класса
* ***Protected*** поля также не доступны извне, только в классах наследниках

### Цепочка вызовов конструкторов
* При создании объектов дочерних классов всегда вызываются конструкторы базовых классов
* Вызов родительских классов начинается с самого первого предка, далее вниз до последнего дочернего
* Родительские конструкторы вызываются ***всегда***, даже если это происходит не явно
```php
class Parent1 {
  public Parent1() : this("aaa") {
    Console.WriteLine("Parent1 constructor");
  }

  public Parent1(string a) {
    Console.WriteLine("Another Parent1 consturctor + " + a);
  }
}
class Child1 : Parent1 {
  public Child1() : base() {
    Console.WriteLine("Child1 constructor");
  }
}

class Child2 : Child1 {
  public Child2() : base() {
    Console.WriteLine("Child2 constructor");
  }
}

Child2 child2 = new Child2(); // Создание объекта Child2
// В консоль будет выведено :
// Another Parent1 consturctor + aaa
// Parent1 constructor
// Child1 constructor
// Child2 constructor
```

## Полиморфизм подтипов

### Виртуальный метод
* Метод базового класса, который может быть переопределен в дочернем классе
* В базовом классе ***virtual***
* В дочернем классе ***override***
```php
class A {
  public void hide() {
    Console.WriteLine("Hide, A!");
  }
  public virtual void show() {
      Console.WriteLine("Hello, A!");
  }
}
class B : A {
  public void hide() {
    Console.WriteLine("Hide, B!");
  }
  public override void show() {
      Console.WriteLine("Hello, B!");
  }
}

A a = new B();
a.hide(); // result : Hide, A!
a.show(); // result : Hello, B!
```
* Дает возможность создания списка разных объектов от общего базового, собранных в одном месте(array, List...)

### Цикл обновления
* При создании ***virtual*** метода ***Upload*** в базовом классе мы может наследовать данный метод, как основную логику, которую будут выполнять каждый цикл все дочернии классы от базового
```php
// Behaviour - Поведение
class Behaviour {
  public virtual void Update() {...}
}
class Mover : Behaviour {
  public override void Update() {...}
}
class Jumper : Behaviour {
  public override void Update() {...}
}

// Создание массива объектов от базового Behaviour
Behaviour[] behaviours = {
  new Mover(),
  new Jumper()
};

// Перебор всех сущностей объекта behaviour
foreach(var behaviour in behaviours) {
  behaviour.Update();
}
```

### Интерфейс
* Предоставляет доступ к чистым абстракциям
* Тип не имеющий ***никакой*** реализации
* Может содержать в себе только описание функциональных членов, кроме конструктора
* Вместо ***class*** начинается с ***interface***, первый символ название ***I***
```php
// Вместо класса Behaviour создаем интерфейс
interface IUpdatable {
  // Не может иметь реализации методов
  void Update(); // Может иметь возвращаемый тип и набор параметров
}
class Mover : IUpdatable {
  public void Update() {...} // слово override уже не нужно
}
class Jumper : IUpdatable {
  public void Update() {...} // слово override уже не нужно
}

IUpdatable updatable  = new IUpdatable(); // Ошибка, нельзя создавать объекты интерфейса
IUpdatable updatable2 = new Mover();      // А так можно 

// Создание массива объектов от интерфейса
IUpdatable[] behaviours = {
  new Mover(),
  new Jumper()
};
```
* Нельзя наследовать больше одного класса, но можно наследовать множество интерфейсов
```php
class Parent1 {...}
class Parent2 {...}
interface Inter1 {...}
interface Inter2 {...}

class Child1 : Parent1, Inter1,  Inter2 {...} // Верно, 1 класс, несколько интерфейсов
class Child2 : Parent1, Parent2, Inter2 {...} // Ошибка, больше 1 класса не может быть
```

### Абстрактный класс(АК)
* Что то среднее между обычным классом и интерфейсом
* Имеет реализацию, но она не полная
* Нельзя создавать объекты класса
* Наследование только в одном экземпляре как от обычных
* При реализации АК нужно реализовывать все его элементы
* Если у класса есть хотя бы один абстрактный метод, класс тоже должен быть абстрактным
```php
// Вариант.1 При реализации через интерфейс имеем два класса с дублированным кодом
interface IDamageable {
  int Health { get; }
  void ApplyDamage(int damage);
}

class SimpleUnit : IDamageable{
  private int _health;          // дублированное поле
  public int Health => _health; // дублированное поле

  public void ApplyDamage(int damage) { // дублированный метод
    _health -= damage;
  }
}

class Warrior : IDamageable {
  private int _health;          // дублированное поле
  public int Health => _health; // дублированное поле

  public void ApplyDamage(int damage) { // дублированный метод
    _health -= damage / 2;              // + небольшое изменение
  }
}

// Вариант.2 Избавление от дублирующегося кода через абстракцию

class Damageable {
  public int Health { get; private set; }
  
  // Метод который нельзя переопределять в наследниках
  public void ApplyDamage(int damage) {
    Health -= ProccessDamage(damage);
  }

  // Метод возвращающий урон
  protected abstract int ProccessDamage(int damage);
}

class SimpleUnit : Damageable{
  protected override int ProccessDamage(int damage) {
    return damage;
  }
}
class Warrior : Damageable {
  protected override int ProccessDamage(int damage) {
    return damage / 2;
  }
}
```

## Статика

### Статическое элемент
* Общий элемент с общим значением для всех объектов класса
* Доступ к элементу через идентификатор класса `ClassName.StaticFieldName`
```php
class User {
  public static int Ids = 0;
  public int Id;

  public User() {
    Id = ++Ids;
  }
}

User user1 = new User(); // user1.Id = 1
User user2 = new User(); // user2.Id = 2
```

### Статический конструктор
* Не имеет модификаторов доступа
* Не имеет параметров
* Нельзя вызывать явно
* Вызывается при первом использовании класса, создании объекта класса и т.п.
```php
class Example {
  public static int Speed; 
  static Example() {
    Speed = 10;
  }
}
```

### Почему статика это плохо
* Портит общую концепцию ООП
* Усложняет возможность расширения проограммы
* Даёт легкое решение проблемы, лишая возможности для развития

## Структуры

### Определение структур
* Ключевое слово ***struct***
* Все элементы по умолчанию ***public***(но модификаторы указывать нужно всегда явно)
* При объявлении структуры не нужно вызывать конструктор `Point point1;`(не нужно писать new `Point()`)
* При использовании конструктора нужно обязательно инициализировать все поля структуры
```php
struct Example {
  public int a;
}
```

### Структуры против классов
* Отличаются в первую очередь семантикой
* Объект класса : ***Entity*** не равен другому объекту, даже если все поля одинаковые
* Объект структуры : ***Valued Object*** равен другому объекту, если все поля одинаковые
```php
// Хороший пример класса
class User {
  public string name;
  public int age;
}
User user1 = new User();
User user2 = new User();
// user1 != user2 даже если имя и возраст совпадают это могут быть 2 разных человека

// Хороший пример структуры
struct Point {
  public int x;
  public int y;
}
Point point1;
Point point2;
point1.x = 5;
point2.x = 5;
point1.y = 3;
point2.y = 3;
// point1 == point2 если 2 точки имеют одинаковые координаты, очевидно что они равны
```