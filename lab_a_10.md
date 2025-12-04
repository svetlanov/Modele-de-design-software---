# Лабораторная работа 10 

## Концепты
- if, else, else if  
- while (true), continue, break  
- do ... while  
- Логические выражения  

---

## Примеры на понимание

### 1.
```csharp
if (true)
{
    Console.WriteLine("Hello");
}
```
**Ответ:** выводится `Hello`.

---

### 2.
```csharp
if (false)
{
    Console.WriteLine("Hello");
}
```
**Ответ:** ничего не выводится.

---

### 3.
```csharp
bool execute = true;
if (execute)
{
    Console.WriteLine("Hello");
}

bool notExecute = !execute;
if (notExecute)
{
    Console.WriteLine("Not executed");
}
```
**Ответ:** выводится только `Hello`.

---

## Функциональное и семантическое различие F1, F2, F3

- **Функционально:** все три функции дают одинаковый результат — при A() == true и B() == true выводят `Hello`.
- **Семантически:**  
  - **F1** вызывает A(), затем (при true) вызывает B().  
  - **F2** использует lazy-evaluation: B() вызывается только если A() вернул true.  
  - **F3** вызывает A() и B() всегда, даже если A() == false.

---

### Что значит «функциональное» и «семантическое»?  
- **Функциональное** — что делает программа (вывод, результат).  
- **Семантическое** — как она это делает (порядок вызовов, логика, поведение выражений).

---

### 4.
```csharp
static void F1()
{
    if (A())
    {
        if (B())
        {
            Console.WriteLine("Hello");
        }
    }
}

static void F2()
{
    if (A() && B())
    {
        Console.WriteLine("Hello");
    }
}

static void F3()
{
    bool a = A();
    bool b = B();
    bool ok = a && b;
    if (ok)
    {
        Console.WriteLine("Hello");
    }
}

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
**Ответ:** выводится:
```csharp
A
B
Hello
```

### 5.

```csharp
if (1)
{
    Console.WriteLine("Hello");
}
```
**Ответ:** не компилируется — условие должно быть bool.

---

### 6.
```csharp
if (false)
{
    Console.WriteLine("A");
    Console.WriteLine("B");
}
```
**Ответ:** ничего не выводится.

---

### 7.
```csharp
if (false)
    Console.WriteLine("A");
    Console.WriteLine("B");
```
**Ответ:** выводится `B`, потому что только первая строка относится к if.

---

### 8.
```csharp
if (false)
{
    Console.WriteLine("A");
}
else
{
    Console.WriteLine("B");
}
```
**Ответ:** выводится `B`.

---

### 9.
```csharp
bool a = true;
if (a)
{
    a = false;
}
else
{
    Console.WriteLine("B");
}
```
**Ответ:** ничего не выводится.

---

### 10.
```csharp
if (true)
{
    return;
}
else
{
    Console.WriteLine("Else");
}
Console.WriteLine("After Else");
```
**Ответ:** ничего не выводится — функция завершается.

---

### 11.
```csharp
if (true)
    Console.WriteLine("A");
else
    Console.WriteLine("B");
Console.WriteLine("C");
```
**Ответ:**  
```
A
C
```

---

### 12.
```csharp
if (true)
    Console.WriteLine("A");
else
{
    Console.WriteLine("B");
}
```
**Ответ:** `A`.

---

## 13.

Исходный код:
```csharp
if (a)
{
    Console.WriteLine("A");
}
else
{
    if (b)
    {
        Console.WriteLine("B");
    }
    else
    {
        if (c)
        {
            Console.WriteLine("C");
        }
    }
}
```

**Ответ (цепочка):**
```csharp
if (a)
    Console.WriteLine("A");
else if (b)
    Console.WriteLine("B");
else if (c)
    Console.WriteLine("C");
```

---

## 14.

Исходный код превращается в:

### Ответ (guard clause):
```csharp
if (a)
{
    Console.WriteLine("A");
    return;
}

Console.WriteLine("After A");

if (b)
{
    Console.WriteLine("B");
    return;
}

Console.WriteLine("After B");

if (c)
{
    Console.WriteLine("C");
    return;
}

Console.WriteLine("After C");
```

### Зачем нужен guard clause?
Чтобы упростить чтение кода и уменьшить вложенность.

---

## 15.
```csharp
int i = 0;
while (true)
{
   if (i == 4)
   {
       Console.WriteLine("ERROR: Should not happen");
       break;
   }
   if (i == 3)
   {
       Console.WriteLine("Exit");
       break;
   }
   if (i == 0)
   {
       Console.WriteLine("Increase by 2 on first iter");
       i += 2;
       continue;
   }

   Console.WriteLine("Increase by 1 normally");
   i++;

   // Implicit continue.
   // continue;
}
```

### Код:
```
i = 0 → "Increase by 2 on first iter" → i = 2  
i = 2 → "Increase by 1 normally" → i = 3  
i = 3 → "Exit" → break  
```

### Ответ:
- **continue** пропускает остаток цикла и переходит к следующей итерации.  
- **break** полностью выходит из цикла.

---

## 16.

```csharp
static int F()
{
    while (true)
    {
       if (true)
       {
           return 0;
       }
       break;
    }
    return 1;
}
```

**Ответ:** всегда возвращает `0` (до break программа никогда не дойдёт).


