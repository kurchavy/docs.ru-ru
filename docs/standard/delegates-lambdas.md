---
title: "Делегаты и лямбда-выражения"
description: "Делегаты и лямбда-выражения"
keywords: .NET, .NET Core
author: richlander
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: fe2e4b4c-6483-4106-a4b4-a33e2e306591
translationtype: Human Translation
ms.sourcegitcommit: 9cf6022fc910bc5418c03c0fa81d9432d85be3b0
ms.openlocfilehash: 0d1dfc333f16acad44b1e276b75ff3c65a77e5aa

---

# <a name="delegates-and-lambdas"></a>Делегаты и лямбда-выражения

Делегаты определяют тип, указывающий конкретную сигнатуру метода. Метод (статический или экземпляр), удовлетворяющий сигнатуре, можно присвоить переменной этого типа и затем вызвать напрямую (с соответствующими аргументами) или передать в качестве аргумента другому методу и затем вызвать. В следующем примере показано использование делегата.

```cs
public class Program
{

  public delegate string Reverse(string s);

  static string ReverseString(string s)
  {
      return new string(s.Reverse().ToArray());
  }

  static void Main(string[] args)
  {
      Reverse rev = ReverseString;

      Console.WriteLine(rev("a string"));
  }
}

```

*   В строке 4 мы создаем тип делегата для определенной сигнатуры. В данном случае это метод, принимающий и возвращающий строковый параметр.
*   В строке 6 мы определяем реализацию делегата, указав метод с точно такой же сигнатурой.
*   В строке 13 метод назначается типу, который соответствует делегату `Reverse`.
*   Наконец, в строке 15 мы вызываем делегат, передав строку для обращения.

Чтобы упростить процесс разработки, платформа .NET содержит набор типов делегата, которые программисты могут повторно использовать, не создавая новые. Это `Func<>`, `Action<>` и `Predicate<>`, которые можно использовать в различных участках API-интерфейсов .NET без необходимости определения новых типов делегата. Безусловно между ними существуют некоторые различия, которые легко определить по сигнатурам. Это связано с их назначением:

*   `Action<>` применяется, когда требуется выполнить действие с использованием аргументов делегата.
*   `Func<>` обычно используется при наличии преобразования, то есть когда требуется преобразовать аргументы делегата в другой результат. Хорошим примером этого являются проекции.
*   `Predicate<>` используется, когда требуется определить, удовлетворяет ли аргумент условию делегата. Его также можно записать в виде `Func<T, bool>`.

Теперь можно обратиться к приведенному выше примеру и переписать его, используя делегат `Func<>` вместо пользовательского типа. При этом работа программы не изменится.

```cs
public class Program
{

  static string ReverseString(string s)
  {
      return new string(s.Reverse().ToArray());
  }

  static void Main(string[] args)
  {
      Func<string, string> rev = ReverseString;

      Console.WriteLine(rev("a string"));
  }
}

```

В этом простом примере определение метода за пределами метода Main() может показаться излишним. Это вызвано тем, что в .NET Framework 2.0 введена концепция **анонимных делегатов**. С их помощью можно создавать "встроенные" делегаты без указания дополнительного типа или метода. Вы просто встраиваете определение делегата там, где это необходимо.

Например, мы собираемся использовать анонимный делегат, чтобы отфильтровать только четные числа из списка и вывести их на консоль.

```cs
public class Program
{

  public static void Main(string[] args)
  {
    List<int> list = new List<int>();

    for (int i = 1; i <= 100; i++)
    {
        list.Add(i);
    }

    List<int> result = list.FindAll(
      delegate(int no)
      {
          return (no%2 == 0);
      }
    );

    foreach (var item in result)
    {
        Console.WriteLine(item);
    }
  }
}

```

Обратите внимание на выделенные строки. Как видно, тело делегата представляет собой набор выражений, как в любом другом делегате. Но вместо использования отдельного определения мы описали его _напрямую_ в нашем вызове метода `FindAll()` с типом `List<T>`.

Однако даже при таком подходе остается довольно много кода, от которого можно избавиться. Как раз для этого и могут пригодиться **лямбда-выражения**.

Впервые лямбда-выражения были введены в C# 3.0 в качестве одного из стандартных блоков LINQ. Они предоставляют более удобный синтаксис для использования делегатов. Они объявляют сигнатуру и тела метода, но не имеют собственного формального удостоверения, пока не будут назначены делегату. В отличие от делегатов их можно напрямую назначать в левой части при регистрации событий, а также в различных предложениях и методах LINQ.

Поскольку лямбда-выражение представляет собой просто еще один способ указания делегата, можно переписать приведенный выше пример, чтобы использовать лямбда-выражение вместо анонимного делегата.

```cs
public class Program
{

  public static void Main(string[] args)
  {
    List<int> list = new List<int>();

    for (int i = 1; i <= 100; i++)
    {
        list.Add(i);
    }

    List<int> result = list.FindAll(i => i % 2 == 0);

    foreach (var item in result)
    {
        Console.WriteLine(item);
    }
  }
}

```

Если взглянуть на выделенные строки, можно увидеть, как выглядит лямбда-выражение. Повторим, что это просто **очень** удобный синтаксис для использования делегатов, сам принцип действия аналогичен анонимному делегату.

Лямбда-выражения — это обычные делегаты, поэтому их без проблем можно использовать в качестве обработчика событий, как показано в следующем фрагменте кода.

```cs
public MainWindow()
{
    InitializeComponent();

    Loaded += (o, e) =>
    {
        this.Title = "Loaded";
    };
}

```

## <a name="further-reading-and-resources"></a>Дополнительные сведения и ресурсы

*   [Делегаты](https://msdn.microsoft.com/library/ms173171.aspx)
*   [Анонимные функции](https://msdn.microsoft.com/library/bb882516.aspx)
*   [Лямбда-выражения](https://msdn.microsoft.com/library/bb397687.aspx)



<!--HONumber=Nov16_HO1-->

