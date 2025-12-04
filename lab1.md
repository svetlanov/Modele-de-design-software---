# Лабораторная работа 1  
## Тема: Установка .NET и создание первого C# проекта

### 1. Установка .NET SDK
- Установила .NET SDK с официального сайта: https://dotnet.microsoft.com/  
- Проверила установку:

```bash
dotnet --version
```

Команда вывела номер версии, значит всё установлено корректно.

---

### 2. Проверка доступности dotnet
```bash
dotnet
```
Команда успешно вывела список доступных операций.

---

### 3. Создание проекта вручную

Создала папку проекта и добавила файл конфигурации:

**MyProject.csproj**
```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>net8.0</TargetFramework>
  </PropertyGroup>
</Project>
```

Создала файл программы:

**Program.cs**
```csharp
Console.WriteLine("Hello, world!");
```

Запуск:

```bash
dotnet run
```

---

### 4. Создание проекта через шаблон dotnet

```bash
dotnet new console -o MySecondProject
```

---

### 5. Компиляция и выполнение программы

```bash
dotnet run
```

---
