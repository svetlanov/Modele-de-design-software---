# Лабораторная работа 8  
## Тема: Улучшение программы (мини-библиотека)

В этой лабораторной работе я реализовала простую систему библиотеки на C#.  
Есть 5 книг, у каждой есть название, год выпуска и статус: книга свободна или занята читателем.  
Я использовала структуры для группировки данных, массив для хранения книг, циклы для обработки всех элементов и отдельные функции для операций над библиотекой.

---

## Постановка задачи

В библиотеке хранится несколько книг. Для каждой книги есть:

- **название**;
- **год выпуска**;
- **статус** — выдана книга или доступна.

Необходимо реализовать следующие операции:

1. **Взять книгу по названию** – находим книгу и меняем статус на «занята».  
2. **Вернуть книгу по названию** – меняем статус на «свободна», если такая книга есть и она была занята; если книги с таким названием нет — выдаём ошибку.  
3. **Просмотреть все книги** – вывести на экран список книг и их статус.

Требования по технике программирования:

- использовать **класс или структуру** для представления книги;
- использовать **массив** для хранения нескольких книг;
- использовать **циклы** для обработки массива;
- создать **отдельные функции** для каждой операции: заимствование, возвращение, просмотр.

---

## Моя реализация (программа):

```csharp
Book[] books = new Book[5]
{
    new Book()
    {
        name = "Сияние (Стивен Кинг)",
        year = 1977,
        available = true
    },

    new Book()
    {
        name = "Доктор сон (Стивен Кинг)",
        year = 2013,
        available = true
    },

    new Book()
    {
        name = "Долорес Клейборн (Стивен Кинг)",
        year = 1992,
        available = true
    },

    new Book()
    {
        name = "Оно (Стивен Кинг)",
        year = 1986,
        available = true
    },

    new Book()
    {
        name = "Под куполом (Стивен Кинг)",
        year = 2009,
        available = true
    },
};

Book b;
b.available = true;
Console.WriteLine(b.available);

borrowBook(books);
returnBook(books);
printBooks(books);

return;


static void borrowBook(Book[] b)
{
    Console.WriteLine("Введите название книги, которую хотите взять: ");
    string borrowedBook = Console.ReadLine()!;

    int bookIndex = findBookIndex(b, borrowedBook);
    if (bookIndex == -1)
    {
        Console.WriteLine("Ошибка. Такой книги нет.");
        return;
    }

    ref Book book = ref b[bookIndex];
    if (book.available == true)
    {
        book.available = false;
        Console.WriteLine("Поздравляем, вы отдолжили эту книгу. Просьба вернуть в назначенный срок (через 2 недели)!");
        return;
    }
    
    // for (int i = 0; i < b.Length; i++)
    // {
    //     if (borrowedBook == b[i].name && b[i].available == true)
    //     {
    //         b[i].available = false;
    //         Console.WriteLine("Поздравляем, вы отдолжили эту книгу. Просьба вернуть в назначенный срок (через 2 недели)!");
    //         return;
    //     }
    // }
    Console.WriteLine("Ошибка. Такой книги нет.");
}

static void returnBook(Book[] b)
{
    Console.WriteLine("Введите название книги, которую хотите вернуть: ");
    string returnedBook = Console.ReadLine()!;

    int bookIndex = findBookIndex(b, returnedBook);
    if (bookIndex == -1)
    {
        Console.WriteLine("Ошибка. Такой книги нет.");
        return;
    }

    Book book = b[bookIndex];
    if (book.available == false)
    {
        book.available = true;
        Console.WriteLine("Книга возвращена.");
        return;
    }
    Console.WriteLine("Ошибка. Данная книга в наличии, вы ее не брали.");
    
    // for (int i = 0; i < b.Length; i++)
    // {
    //     if (returnedBook == b[i].name)
    //     {
    //         if (b[i].available == false)
    //         {
    //             b[i].available = true;
    //             Console.WriteLine("Книга возвращена.");
    //             return;
    //         }
    //         Console.WriteLine("Ошибка. Данная книга в наличии, вы ее не брали.");
    //         return;
    //     }
    // }
    // Console.WriteLine("Ошибка. Такой книги в списке не найденно.");
}

static void printBooks(Book[] b)
{
    for (int i = 0; i < b.Length; i++)
    {
        Console.WriteLine($"Книга № {i + 1}:");
        Console.WriteLine(b[i].name);
        Console.WriteLine(b[i].year);
        Console.WriteLine(b[i].available);
        Console.WriteLine();
    }
}


static int findBookIndex(Book[] b, string name)
{
    for (int i = 0; i < b.Length; i++)
    {
        if (b[i].name == name)
        {
            return i;
        }
    }

    return -1;
}

struct Book
{
    public required string name;
    public required int year;
    public required bool available;
}

```

---

## Итог

Данный подход показывает, как при помощи структур, массивов и функций можно сделать программу более аккуратной и избежать дублирования кода.
