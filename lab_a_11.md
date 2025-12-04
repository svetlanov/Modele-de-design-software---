# Лабораторная работа a_11  
## Тема: Перечисления (enum) и модель светофора

В этой лабораторной работе я реализовала модель светофора, используя механизм `enum` и базовые конструкции C#.  
Цель — научиться описывать состояния с помощью перечислений и управлять логикой программы через отдельные функции.

---

## Задание:
Представьте ситуацию одного светофора в программе:

-Светофор будет одного из 3-х цветов (зеленый, красный, желтый).
-Сделайте функцию, которая в зависимости от цвета, выдает действие, которое нужно совершить (ехать, ждать, готовиться).
-Сделайте функцию, которая, в зависимости от действия, печатает на экран выполненное действие.
-Сделайте функцию, которая переводит светофор в следующее состояние.
-Используйте все это в программе. Убедитесь, что состояния светофора циклируют.

---

## Реализация:
```csharp
enum TrafficLightColor
{
    Red,
    Yellow,
    Green
}

enum TrafficAction
{
    Wait,
    GetReady,
    Go
}

class Program
{
    static void Main()
    {
        TrafficLightColor current = TrafficLightColor.Red;

        for (int i = 0; i < 6; i++)
        {
            Console.WriteLine($"Цвет светофора: {current}");

            TrafficAction action = GetActionByColor(current);
            PrintAction(action);

            current = GetNextColor(current);

            Console.WriteLine(); // пустая строка
        }
    }

    static TrafficAction GetActionByColor(TrafficLightColor color)
    {
        switch (color)
        {
            case TrafficLightColor.Red:
                return TrafficAction.Wait;
            case TrafficLightColor.Yellow:
                return TrafficAction.GetReady;
            case TrafficLightColor.Green:
                return TrafficAction.Go;
            default:
                return TrafficAction.Wait;
        }
    }

    static void PrintAction(TrafficAction action)
    {
        switch (action)
        {
            case TrafficAction.Wait:
                Console.WriteLine("Действие: жду.");
                break;
            case TrafficAction.GetReady:
                Console.WriteLine("Действие: готовлюсь ехать.");
                break;
            case TrafficAction.Go:
                Console.WriteLine("Действие: еду.");
                break;
        }
    }

    static TrafficLightColor GetNextColor(TrafficLightColor current)
    {
        switch (current)
        {
            case TrafficLightColor.Red:
                return TrafficLightColor.Yellow;
            case TrafficLightColor.Yellow:
                return TrafficLightColor.Green;
            case TrafficLightColor.Green:
                return TrafficLightColor.Red;
            default:
                return TrafficLightColor.Red;
        }
    }
}
```

## Итоги

В ходе работы я создала модель светофора с использованием перечислений enum, что позволило удобно описать три состояния светофора и связанные с ними действия водителя. Я реализовала три функции: определение действия по текущему цвету, вывод этого действия на экран и переход к следующему состоянию светофора. Завершая работу, я объединила всё в основной программе и убедилась, что смена сигналов происходит циклически.

