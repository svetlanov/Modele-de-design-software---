# Лабораторная работа a_08  
## Тема: Ввод данных с консоли

В этой лабораторной работе я разобралась, как читать данные из консоли, конвертировать строки в числа, обрабатывать ошибки ввода и использовать `out`‑параметры.

---

## Вопросы на понимание

### Что будет, если пользователь не введет строковое представление числа?

```csharp
string a = Console.ReadLine()!;
int b = int.Parse(a);
Console.WriteLine(b);
```

Если пользователь введёт не число (например, слово или пустую строку), `int.Parse(a)` выбросит исключение `FormatException`, и программа завершится с ошибкой, до вывода результата.

---

```csharp
string a = Console.ReadLine()!;
int b;
bool success = int.TryParse(a, out b);
Console.WriteLine(success);
Console.WriteLine(b);
```

Если пользователь введёт не число, `int.TryParse` вернёт `false`, а в переменную `b` запишется значение по умолчанию (0). В консоль выведется:

- `False`
- `0`

Если введено корректное число, `success` будет `true`, а в `b` попадёт введённое значение.

---

### Как работает этот код? Что выведется в консоль?

```csharp
int a = 0;
F(a);
Console.WriteLine(a);

static void F(int a)
{
    a = 1;
}
```

Значение `a` передаётся **по значению**, внутри функции меняется только копия. Снаружи `a` остаётся равно 0, в консоль выводится `0`.

---

```csharp
int a = 0;
F(out a);
Console.WriteLine(a);

static void F(out int b)
{
    b = 1;
}
```

Параметр передаётся с `out`, то есть функция напрямую меняет переменную вызывающей стороны. Внутри `F` в `b` записывается 1, снаружи `a` становится 1. В консоль выводится `1`.

---

```csharp
int a = 0;
F(out a);
Console.WriteLine(a);

static void F(out int a)
{
    a = 1;
}
```

Имя параметра не важно, принцип тот же: `out` меняет переменную снаружи. В консоль выводится `1`.

---

```csharp
A a;
F(out a);
Console.WriteLine(a.f1);
Console.WriteLine(a.f2);

static void F(out int b)
{
    b = 1;
}

struct A
{
    public int f1;
    public int f2;
}
```

Тип параметра функции `F` — `int`, а передаётся `A`. Такой код **не компилируется**: нельзя передать `out A` туда, где ожидается `out int`.

---

```csharp
A a;
F(out a);
Console.WriteLine(a.f1);
Console.WriteLine(a.f2);

static void F(out int a)
{
    a = 1;
}

struct A
{
    public int f1;
    public int f2;
}
```

Та же проблема: функция ожидает `out int`, а мы передаём `out A`. Код **не компилируется**.

---

```csharp
A a;
F(out a);
Console.WriteLine(a.f1);
Console.WriteLine(a.f2);

static void F(out A b)
{
    b = 1;
}

struct A
{
    public int f1;
    public int f2;
}
```

Здесь тип параметра совпадает (`out A`), но внутри функции выполняется `b = 1;`, а неявного преобразования `int → A` нет. Такой код тоже **не компилируется**.

---

```csharp
A a;
F(out a);
Console.WriteLine(a.f1);
Console.WriteLine(a.f2);

static void F(out A b)
{
    b.f1 = 1;
}

struct A
{
    public int f1;
    public int f2;
}
```

Для `out`‑параметра компилятор требует, чтобы ему явно присвоили значение перед первым использованием. Здесь полю `f1` пытаются присвоить значение, не инициализируя саму структуру `b`. Такой код **не компилируется**: параметр `b` должен быть присвоен целиком.

---

```csharp
A a;
F(out a);
Console.WriteLine(a.f1);
Console.WriteLine(a.f2);

static void F(out A b)
{
    b.f1 = 1;
    b.f2 = 2;
}

struct A
{
    public int f1;
    public int f2;
}
```

Ситуация та же: `b` как `out`‑параметр должен получить значение до использования, а тут сразу обращаются к его полям. Код **не компилируется**.

---

```csharp
A a;
F(out a);
Console.WriteLine(a.f1);
Console.WriteLine(a.f2);

static void F(out A b)
{
    b = new()
    {
        f1 = 1,
        f2 = 2,
    };
}

struct A
{
    public int f1;
    public int f2;
}
```

Здесь `out`‑параметру `b` присваивается новый экземпляр структуры `A`. После вызова `F(out a)` переменная `a` получает `f1 = 1` и `f2 = 2`. В консоль выводится:

```
1
2
```

---

```csharp
int a = 0;
F(out a);
Console.WriteLine(a);

static int F(out int b)
{
    b = 1;
    return 2;
}
```

Функция возвращает число `2`, а через `out`‑параметр `b` записывает `1`. Вызов `F(out a)` присваивает `a = 1`. Возвращаемое значение не используется. В консоль выводится `1`.

---

```csharp
int a = 0;
int b = 0;
b = F(out a);
Console.WriteLine(a);
Console.WriteLine(b);

static int F(out int c)
{
    c = 1;
    return 2;
}
```

После вызова:  
`a = 1` (через `out`),  
`b = 2` (возвращаемое значение).  

В консоль выводится:

```
1
2
```

---

```csharp
int a;
int b;
F(out a, out b);
Console.WriteLine(a);
Console.WriteLine(b);

static void F(out int c, out int d)
{
    c = 1;
    d = 2;
}
```

Функция присваивает: `c = 1`, `d = 2`.  
После вызова `a = 1`, `b = 2`.  

В консоль выводится:

```
1
2
```

---

```csharp
Position p = new()
{
    X = 0,
    Y = 1,
};
F(out p.X);
Console.WriteLine(p.X);

static void F(out int a)
{
    c = 2;
}

struct Position
{
    public int X;
    public int Y;
}
```

В таком виде код **не компилируется**, потому что внутри функции используется переменная `c`, которая не объявлена (должно быть `a = 2;`).  

Если исправить на:

```csharp
static void F(out int a)
{
    a = 2;
}
```

то `out p.X` передаст ссылку на поле `X`, функция запишет туда `2`, и на экран выведется `2`.

---

## Практика

**Задача:**  
Создать программу, которая:

- запрашивает у пользователя 3 числа, каждое **строго больше 2**;
- если пользователь вводит не число или число ≤ 2, запрашивает ввод заново;
- после ввода трёх корректных чисел считает их произведение и выводит результат.

### Реализация на C#

```csharp
int a = InputPositiveInt("a");
int b = InputPositiveInt("b");
int c = InputPositiveInt("c");
int multiplying = a * b * c;
Console.WriteLine(multiplying);

static int InputPositiveInt(string name)
{
    while (true)
{
    Console.WriteLine($"Введите число {name}: ");
    string str = Console.ReadLine()!;
    bool parsed = int.TryParse(str, out int result);

    if (!parsed)
    {
        Console.WriteLine("Введите корректное число.");
        continue;
    }
        if (result < 2)
        {
            Console.WriteLine("Ошибка. Введите число больше, чем 2.");
            continue;
        }
        return result;
    }
}

```

### Итог

Эта программа показывает на практике, как совмещать ввод с консоли, парсинг, проверки и циклы. 
