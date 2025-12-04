# Лабораторная работа 5  
## Тема: Элементарные техники программирования

В этой лабораторной работе я изучила базовые техники программирования: вычисление выражений, использование блоков видимости, создание пользовательских типов (struct, class), работу с функциями и механизм вызова функций.

---

# Задание: моделирование заказов клиентов

В ассортименте есть три товара: напиток, первое блюдо и второе блюдо, например по ценам 10, 20 и 30.  
Есть два клиента, каждый делает свой выбор.  
Необходимо представить ситуацию в программе и вывести стоимость заказа каждого клиента.

---

## 1. Реализация:

```csharp
using System;

Meal_Prices mp = new()
{
    drink = 1,
    first_course = 2,
    second_course = 3
};

static int Client_Total(Meal_Prices mp, Client_Choise cc)
{
    return cc.drink * mp.drink + cc.first * mp.first_course + cc.second * mp.second_course;
}

{
    // int client_drink = 100; // 100г напитка
    // int client_first = 0; // нет первого
    // int client_second = 250; // 250г второго

    Client_Choise cc = new()
    {
        drink = 100,
        first = 0,
        second = 150
    };
    Print_Client_Total(mp, cc);

}


{
    // int client_drink = 0; // 0 напитка
    // int client_first = 300; // 300г первого
    // int client_second = 0; // 0 второго

    Client_Choise cc = new()
    {
        drink = 0,
        first = 120,
        second = 210
    };
    Print_Client_Total(mp, cc);

    // second_client = cc.drink * mp.drink + cc.first * mp.first_course + cc.second * mp.second_course;
}


    static void Print_Client_Total(Meal_Prices mp, Client_Choise cc)
    {

        int first_client = Client_Total(mp, cc);
        Console.WriteLine($"Сумма заказа клиента: {first_client}");
        // first_client = cc.drink * mp.drink + cc.first * mp.first_course + cc.second * mp.second_course;
    }

struct Meal_Prices
{
    public int drink;
    public int first_course;
    public int second_course;
}

struct Client_Choise
{
    public int drink;
    public int first;
    public int second;
}
```

---

# Вопросы на анализ

## Задание № 1.

```csharp
int b = 6;
F(b);
Console.WriteLine(b);

static void F(int a)
{
    a = 5;
}
```

### Ответ  
В стеке создаются переменные b и a (локальная копия). В хипе ничего нет. Строка a = 5 изменяет только локальную копию.  
Переменная b остаётся равной 6.  
Вывод: **6**.  
`void` используется потому, что функция ничего не возвращает.

---

## Задание № 2.

```csharp
int a = 6;
F(a);
Console.WriteLine(a);

static void F(int a)
{
    a = 5;
}
```

### Ответ  
Во время вызова создаётся новая локальная переменная a — это отдельная ячейка стека, не связанная с внешней.  
Внешняя a остаётся равной 6.  
Вывод: **6**.

---

## Задание № 3.

```csharp
string a = "hello";
F(a);
Console.WriteLine(a);

static void F(string b)
{
    b = "world";
}
```

### Ответ  
Создаётся один объект "hello" в хипе.  
Внутри функции создаётся копия ссылки b, указывающая на тот же объект.  
Присваивание b = "world" создаёт второй объект, но меняет только внутреннюю ссылку.  
Переменная a остаётся указывать на "hello".  
Вывод: **hello**.

---

## Задание № 4.

```csharp
A b = new()
{
    value = 1,
};
F(b);
Console.WriteLine(b.value);

static void F(A a)
{
    a.value = 2;
}

struct A
{
    public int value;
}
```

### Ответ  
Структуры — типы-значения.  
Создаётся один объект b в стеке.  
При вызове создаётся копия структуры, и изменение a.value не влияет на b.value.  
Вывод: **1**.  
Имя переменной значения не меняет.  
Если заменить struct на class, объект создастся в хипе, и обе переменные будут ссылаться на него → вывод будет **2**.

---

# Итог

В этой лабораторной я научилась моделировать реальные ситуации с помощью структур и функций, разобралась с механизмом передачи параметров, различиями между значимыми и ссылочными типами и углубила понимание работы памяти в C#.
