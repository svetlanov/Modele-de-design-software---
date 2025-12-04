# Лабораторная работа a_9  
## Тема: Логические выражения и операторы

В этой лабораторной работе я повторила логические значения, операторы сравнения и логические операторы в C#, а также поведение && и || при ленивой (lazy) оценке.

---

## Вопросы на понимание

### 1.

```csharp
bool a = true;
Console.WriteLine(a);
```

**Ответ:** программа компилируется и выводит `True`.

---

### 2.

```csharp
bool a = null;
```

**Ответ:** код не компилируется. Тип `bool` не может принимать значение `null`.

---

### 3.

```csharp
bool a = 1 == 2;
Console.WriteLine(a);
```

`1 == 2` даёт `false`.

**Ответ:** в консоль выводится `False`.

---

### 4.

```csharp
int x = 3;
int y = 4;
bool b = x == y;
Console.WriteLine(b);
```

`3 == 4` → `false`.

**Ответ:** в консоль выводится `False`.

---

### 5.

```csharp
int x = 3;
int y = 4;
bool b = x * 2 == y + 4;
Console.WriteLine(b);
```

`x * 2 = 6`, `y + 4 = 8`, `6 == 8` → `false`.

**Ответ:** в консоль выводится `False`.

---

### 6.

```csharp
bool a = 1 > 2;
a = 3 == 3;
Console.WriteLine(a);
```

Сначала `a = false`, затем `a = true`.

**Ответ:** в консоль выводится `True`.

---

### 7.

```csharp
bool a = true;
F(a);

static void F(bool x)
{
    Console.WriteLine(x);
}
```

**Ответ:** при вызове `F(a)` в консоль выводится `True`.

И аналогично:

```csharp
F(5 > 3);

static void F(bool flag)
{
    Console.WriteLine(flag);
}
```

`5 > 3` → `true`.

**Ответ:** в консоль выводится `True`.

---

### 8.

```csharp
bool result = F();
Console.WriteLine(result);

static bool F()
{
    return true;
}
```

Функция возвращает `true`.

**Ответ:** в консоль выводится `True`.

---

### 9.

```csharp
bool result = IsGreater(5, 3);
Console.WriteLine(result);

static bool IsGreater(int a, int b)
{
    return a > b;
}
```

`5 > 3` → `true`.

**Ответ:** в консоль выводится `True`.

---

### 10.

```csharp
bool a = true;
bool b = false;
bool c = a == b;
Console.WriteLine(c);
```

`true == false` → `false`.

**Ответ:** в консоль выводится `False`.

---

### 11.

```csharp
bool a = false;
bool b = !a;
Console.WriteLine(b);
```

`!false` → `true`.

**Ответ:** в консоль выводится `True`.

---

### 12.

```csharp
bool a = true;
bool b = false;
bool c = a && b;
Console.WriteLine(c);
```

`true && false` → `false`.

**Ответ:** в консоль выводится `False`.

---

### 13. 

```csharp
bool result = A() && B();

static bool A()
{
    Console.WriteLine("A");
    return true;
}

static bool B()
{
    Console.WriteLine("B");
    return true;
}
```

Сначала вызывается `A()` → печатает `A`, возвращает `true`.  
Потом вызывается `B()` → печатает `B`, возвращает `true`.  
`result` будет `true`, но его не печатают.

**Ответ:** в консоли:

```
A
B
```

---

### 14.

```csharp
bool result = A() && B();

static bool A()
{
    Console.WriteLine("A");
    return true;
}

static bool B()
{
    Console.WriteLine("B");
    return false;
}
```

`A()` печатает `A`, возвращает `true`.  
`B()` печатает `B`, возвращает `false`.  
`result` будет `false`.

**Ответ:** в консоли:

```
A
B
```

---

### 15.

```csharp
bool result = A() && B();

static bool A()
{
    Console.WriteLine("A");
    return false;
}

static bool B()
{
    Console.WriteLine("B");
    return true;
}
```

При `&&` если первый операнд даёт `false`, второй **не вычисляется** (lazy evaluation).  

`A()` печатает `A`, возвращает `false`, `B()` не вызывается.

**Ответ:** в консоли:

```
A
```

---

### 16. 

```csharp
bool result = A() || B();

static bool A()
{
    Console.WriteLine("A");
    return true;
}

static bool B()
{
    Console.WriteLine("B");
    return true;
}
```

При `||` если первый операнд даёт `true`, второй **не вычисляется**.

`A()` печатает `A`, возвращает `true`, `B()` не вызывается.

`result` будет `true`.

**Ответ:** в консоли:

```
A
```

---

## Итог

В этой работе я закрепила:

- как работают логические типы и выражения в C#;
- что делают операторы сравнения и логические операторы;
- как `&&` и `||` лениво вычисляют второй операнд;
- как передавать логические значения в функции и возвращать их из функций.
