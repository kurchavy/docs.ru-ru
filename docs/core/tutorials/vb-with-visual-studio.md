---
title: "Создание приложения Hello World на Visual Basic с помощью .NET Core в Visual Studio 2017"
description: "Узнайте, как создать простое консольное приложение .NET Core на Visual Basic с помощью Visual Studio 2017."
keywords: ".NET Core, консольное приложение .NET Core, Visual Studio 2017"
author: rpetrusha
ms.author: ronpet
ms.date: 08/07/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-vb
ms.devlang: vb
ms.translationtype: HT
ms.sourcegitcommit: e0271ba3392ce8861dc916714af8c16d4581ce4f
ms.openlocfilehash: 8eeb4cc5be716ede4397189429ed882dff4d9e91
ms.contentlocale: ru-ru
ms.lasthandoff: 08/14/2017

---

# <a name="build-a-visual-basic-hello-world-application-with-net-core-in-visual-studio-2017"></a><span data-ttu-id="4954d-104">Создание приложения Hello World на Visual Basic с помощью .NET Core в Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="4954d-104">Build a Visual Basic Hello World application with .NET Core in Visual Studio 2017</span></span>

<span data-ttu-id="4954d-105">В этой статье содержится пошаговое описание процессов сборки, отладки и публикации простого консольного приложения .NET Core на Visual Basic с помощью Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4954d-105">This topic provides a step-by-step introduction to building, debugging, and publishing a simple .NET Core console application using Visual Basic in Visual Studio 2017.</span></span> <span data-ttu-id="4954d-106">Visual Studio 2017 предоставляет полнофункциональную среду для разработки приложений .NET Core.</span><span class="sxs-lookup"><span data-stu-id="4954d-106">Visual Studio 2017 provides a full-featured development environment for building .NET Core applications.</span></span> <span data-ttu-id="4954d-107">Если само приложение не имеет зависимостей от конкретной платформы, его можно выполнять на любой официально поддерживаемой платформе .NET Core и в любой системе, в которой установлена .NET Core.</span><span class="sxs-lookup"><span data-stu-id="4954d-107">As long as the application doesn't have platform-specific dependencies, the application can run on any platform that .NET Core targets and on any system that has .NET Core installed.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4954d-108">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="4954d-108">Prerequisites</span></span>

<span data-ttu-id="4954d-109">[Visual Studio 2017](https://www.visualstudio.com/downloads/) с установленной рабочей нагрузкой "Кроссплатформенная разработка .NET Core".</span><span class="sxs-lookup"><span data-stu-id="4954d-109">[Visual Studio 2017](https://www.visualstudio.com/downloads/) with the ".NET Core cross-platform development" workload installed.</span></span> <span data-ttu-id="4954d-110">Приложение можно разработать с помощью .NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="4954d-110">You can develop your app with .NET Core 2.0.</span></span>

<span data-ttu-id="4954d-111">Дополнительные сведения см. в разделе [Необходимые компоненты для .NET Core в Windows](../../core/windows-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="4954d-111">For more information, see [Prerequisites for .NET Core on Windows](../../core/windows-prerequisites.md).</span></span>

## <a name="a-simple-hello-world-application"></a><span data-ttu-id="4954d-112">Простое приложение Hello World</span><span class="sxs-lookup"><span data-stu-id="4954d-112">A simple Hello World application</span></span>

<span data-ttu-id="4954d-113">Для начала создадим простое консольное приложение Hello World.</span><span class="sxs-lookup"><span data-stu-id="4954d-113">Begin by creating a simple "Hello World" console application.</span></span> <span data-ttu-id="4954d-114">Выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="4954d-114">Follow these steps:</span></span>

1. <span data-ttu-id="4954d-115">Запустите Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="4954d-115">Launch Visual Studio 2017.</span></span> <span data-ttu-id="4954d-116">Выберите **Файл** > **Создать** > **Проект** в меню.</span><span class="sxs-lookup"><span data-stu-id="4954d-116">Select **File** > **New** > **Project** from the menu bar.</span></span> <span data-ttu-id="4954d-117">В диалоговом окне *Новый проект* * выберите узел **Visual Basic**, а затем — узел **.NET Core**.</span><span class="sxs-lookup"><span data-stu-id="4954d-117">In the *New Project** dialog, select the **Visual Basic** node followed by the **.NET Core** node.</span></span> <span data-ttu-id="4954d-118">Выберите шаблон проекта **Консольное приложение (.NET Core)**.</span><span class="sxs-lookup"><span data-stu-id="4954d-118">Then select the **Console App (.NET Core)** project template.</span></span> <span data-ttu-id="4954d-119">В текстовом поле **Имя** введите "HelloWorld".</span><span class="sxs-lookup"><span data-stu-id="4954d-119">In the **Name** text box, type "HelloWorld".</span></span> <span data-ttu-id="4954d-120">Нажмите кнопку **OK**.</span><span class="sxs-lookup"><span data-stu-id="4954d-120">Select the **OK** button.</span></span>

   ![Диалоговое окно создания проекта, в котором выбран шаблон проекта консольного приложения](./media/vb-with-visual-studio/new-project.png)
   
1. <span data-ttu-id="4954d-122">Visual Studio использует шаблон для создания проекта.</span><span class="sxs-lookup"><span data-stu-id="4954d-122">Visual Studio uses the template to create your project.</span></span> <span data-ttu-id="4954d-123">Шаблон консольного приложения Visual Basic для .NET Core автоматически определяет класс `Program` с одним методом `Main`, который принимает в качестве аргумента массив <xref:System.String>.</span><span class="sxs-lookup"><span data-stu-id="4954d-123">The Visual Basic Console Application template for .NET Core automatically defines a class, `Program`, with a single method, `Main`, that takes a <xref:System.String> array as an argument.</span></span> <span data-ttu-id="4954d-124">`Main` — точка входа в приложение. Это метод, который автоматически вызывается средой выполнения при запуске приложения.</span><span class="sxs-lookup"><span data-stu-id="4954d-124">`Main` is the application entry point, the method that's called automatically by the runtime when it launches the application.</span></span> <span data-ttu-id="4954d-125">Все аргументы, предоставленные в командной строке при запуске приложения, доступны через массив *args*.</span><span class="sxs-lookup"><span data-stu-id="4954d-125">Any command-line arguments supplied when the application is launched are available in the *args* array.</span></span>

   ![Visual Studio и новый проект Hello World](./media/vb-with-visual-studio/devenv.png)

   <span data-ttu-id="4954d-127">Этот шаблон создает простое приложение Hello World.</span><span class="sxs-lookup"><span data-stu-id="4954d-127">The template creates a simple "Hello World" application.</span></span> <span data-ttu-id="4954d-128">Он вызывает метод <xref:System.Console.WriteLine(System.String)?displayProperty=fullName> для отображения литеральной строки "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="4954d-128">It calls the <xref:System.Console.WriteLine(System.String)?displayProperty=fullName> method to display the literal string "Hello World!"</span></span> <span data-ttu-id="4954d-129">в окне консоли.</span><span class="sxs-lookup"><span data-stu-id="4954d-129">in the console window.</span></span> <span data-ttu-id="4954d-130">Запустите программу в режиме отладки, нажав на панели инструментов кнопку **HelloWorld** с зеленой стрелкой.</span><span class="sxs-lookup"><span data-stu-id="4954d-130">By selecting the **HelloWorld** button with the green arrow on the toolbar, you can run the program in Debug mode.</span></span> <span data-ttu-id="4954d-131">Окно консоли появится на короткое время и затем сразу же закроется.</span><span class="sxs-lookup"><span data-stu-id="4954d-131">If you do, the console window is visible for only a brief time interval before it closes.</span></span> <span data-ttu-id="4954d-132">Это происходит потому, что метод `Main` и приложение в целом завершаются сразу же, как только будет выполнена единственная инструкция в методе `Main`.</span><span class="sxs-lookup"><span data-stu-id="4954d-132">This occurs because the `Main` method terminates and the application ends as soon as the single statement in the `Main` method executes.</span></span>

1. <span data-ttu-id="4954d-133">Чтобы приостановить приложение перед тем, как закроется окно консоли, добавьте следующий код сразу после вызова метода <xref:System.Console.WriteLine(System.String)?displayProperty=fullName>:</span><span class="sxs-lookup"><span data-stu-id="4954d-133">To cause the application to pause before it closes the console window, add the following code immediately after the call to the <xref:System.Console.WriteLine(System.String)?displayProperty=fullName> method:</span></span>

   ```vb
   Console.Write("Press any key to continue...")
   Console.ReadKey(true)
   ```
   <span data-ttu-id="4954d-134">Этот код предлагает пользователю нажать любую клавишу и приостанавливает работу программы до нажатия клавиши.</span><span class="sxs-lookup"><span data-stu-id="4954d-134">This code prompts the user to press any key and then pauses the program until a key is pressed.</span></span>

1. <span data-ttu-id="4954d-135">В строке меню выберите **Сборка** > **Собрать решение**.</span><span class="sxs-lookup"><span data-stu-id="4954d-135">On the menu bar, select **Build** > **Build Solution**.</span></span> <span data-ttu-id="4954d-136">При этом программа компилируется в промежуточный язык IL, который затем преобразуется в двоичный код JIT-компилятором.</span><span class="sxs-lookup"><span data-stu-id="4954d-136">This compiles your program into an intermediate language (IL) that's converted into binary code by a just-in-time (JIT) compiler.</span></span>

1. <span data-ttu-id="4954d-137">Запустите программу, нажав кнопку **HelloWorld** с зеленой стрелкой на панели инструментов.</span><span class="sxs-lookup"><span data-stu-id="4954d-137">Run the program by selecting the **HelloWorld** button with the green arrow on the toolbar.</span></span>

   ![Окно консоли с приложением Hello World и надписью "Чтобы продолжить, нажмите любую клавишу"](./media/with-visual-studio/helloworld1.png)

1. <span data-ttu-id="4954d-139">Для закрытия консольного окна нажмите любую клавишу.</span><span class="sxs-lookup"><span data-stu-id="4954d-139">Press any key to close the console window.</span></span>

## <a name="enhancing-the-hello-world-application"></a><span data-ttu-id="4954d-140">Расширение приложения Hello World</span><span class="sxs-lookup"><span data-stu-id="4954d-140">Enhancing the Hello World application</span></span>

<span data-ttu-id="4954d-141">Давайте расширим приложение. Теперь у пользователя будет запрашиваться имя, которое затем будет отображаться с датой и временем.</span><span class="sxs-lookup"><span data-stu-id="4954d-141">Enhance your application to prompt the user for his or her name and to display it along with the date and time.</span></span> <span data-ttu-id="4954d-142">Выполните следующие действия, чтобы изменить и протестировать программу.</span><span class="sxs-lookup"><span data-stu-id="4954d-142">To modify and test the program, do the following:</span></span>

1. <span data-ttu-id="4954d-143">Введите следующий код Visual Basic в окне редактирования кода между первой открывающей скобкой за строкой `Sub Main(args As String())` и первой закрывающей скобкой:</span><span class="sxs-lookup"><span data-stu-id="4954d-143">Enter the following Visual Basic code in the code window immediately after the opening bracket that follows the `Sub Main(args As String())` line and before the first closing bracket:</span></span>

   <span data-ttu-id="4954d-144">[!code-vb[GettingStarted#1](../../../samples/snippets/core/tutorials/vb-with-visual-studio/helloworld.vb#1)]</span><span class="sxs-lookup"><span data-stu-id="4954d-144">[!code-vb[GettingStarted#1](../../../samples/snippets/core/tutorials/vb-with-visual-studio/helloworld.vb#1)]</span></span>

   <span data-ttu-id="4954d-145">Этот код заменяет существующие операторы <xref:System.Console.WriteLine%2A?displayProperty=fullName>, <xref:System.Console.Write%2A?displayProperty=fullName> и <xref:System.Console.ReadKey%2A?displayProperty=fullName>.</span><span class="sxs-lookup"><span data-stu-id="4954d-145">This code replaces the existing <xref:System.Console.WriteLine%2A?displayProperty=fullName>, <xref:System.Console.Write%2A?displayProperty=fullName>, and <xref:System.Console.ReadKey%2A?displayProperty=fullName> statements.</span></span>

   ![Файл программы Visual Studio с обновленным методом Main](./media/vb-with-visual-studio/codewindow.png)

   <span data-ttu-id="4954d-147">Теперь код выдает строку "What is your name?" (Как вас зовут?)</span><span class="sxs-lookup"><span data-stu-id="4954d-147">This code displays "What is your name?"</span></span> <span data-ttu-id="4954d-148">в окно консоли и ожидает, чтобы пользователь ввел строку текста и нажал клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="4954d-148">in the console window and waits until the user enters a string followed by the Enter key.</span></span> <span data-ttu-id="4954d-149">Приложение сохраняет полученную строку в переменной с именем `name`.</span><span class="sxs-lookup"><span data-stu-id="4954d-149">It stores this string into a variable named `name`.</span></span> <span data-ttu-id="4954d-150">Оно также получает значение свойства <xref:System.DateTime.Now?displayProperty=fullName>, которое содержит текущее локальное время, и присваивает его переменной с именем `currentDate`.</span><span class="sxs-lookup"><span data-stu-id="4954d-150">It also retrieves the value of the <xref:System.DateTime.Now?displayProperty=fullName> property, which contains the current local time, and assigns it to a variable named `currentDate`.</span></span> <span data-ttu-id="4954d-151">Наконец, с помощью [интерполированной строки](../../csharp/language-reference/keywords/interpolated-strings.md) эти значения выводятся в окно консоли.</span><span class="sxs-lookup"><span data-stu-id="4954d-151">Finally, it uses an [interpolated string](../../csharp/language-reference/keywords/interpolated-strings.md) to display these values in the console window.</span></span>

1. <span data-ttu-id="4954d-152">Скомпилируйте программу, выбрав действие **Сборка** > **Собрать решение**.</span><span class="sxs-lookup"><span data-stu-id="4954d-152">Compile the program by choosing **Build** > **Build Solution**.</span></span>

1. <span data-ttu-id="4954d-153">Запустите программу в режиме отладки, выбрав на панели инструментов кнопку с зеленой стрелкой, нажав клавишу F5 или выбрав пункт меню **Отладка** > **Начать отладку**.</span><span class="sxs-lookup"><span data-stu-id="4954d-153">Run the program in Debug mode in Visual Studio by selecting the green arrow on the toolbar, pressing F5, or choosing the **Debug** > **Start Debugging** menu item.</span></span> <span data-ttu-id="4954d-154">В ответ на приглашение в командной строке введите имя и нажмите клавишу ВВОД.</span><span class="sxs-lookup"><span data-stu-id="4954d-154">Respond to the prompt by entering a name and pressing the Enter key.</span></span>

   ![Окно консоли с измененными выходными данными программы](./media/with-visual-studio/helloworld2.png)

1. <span data-ttu-id="4954d-156">Для закрытия консольного окна нажмите любую клавишу.</span><span class="sxs-lookup"><span data-stu-id="4954d-156">Press any key to close the console window.</span></span>

<span data-ttu-id="4954d-157">Вы создали и запустили приложение.</span><span class="sxs-lookup"><span data-stu-id="4954d-157">You've created and run your application.</span></span> <span data-ttu-id="4954d-158">Чтобы приложение достигло профессионального уровня, нужно выполнить еще несколько шагов для подготовки приложения к выпуску:</span><span class="sxs-lookup"><span data-stu-id="4954d-158">To develop a professional application, take some additional steps to make your application ready for release:</span></span>

- <span data-ttu-id="4954d-159">Сведения об отладке приложения см. в разделе [Отладка приложения Hello World на C# в Visual Studio 2017](debugging-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="4954d-159">For information on debugging your application, see [Debugging your C# Hello World application with Visual Studio 2017](debugging-with-visual-studio.md).</span></span>

- <span data-ttu-id="4954d-160">Сведения о разработке и публикации распространяемой версии приложения см. в разделе [Публикация приложения Hello World на C# с помощью Visual Studio 2017](publishing-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="4954d-160">For information on developing and publishing a distributable version of your application, see [Publishing your C# Hello World application with Visual Studio 2017](publishing-with-visual-studio.md).</span></span>

<!--
## Related topics

Instead of a console application, you can also build a class library with .NET Core and Visual Studio 2017. For a step-by-step introduction, see [Building a class library with C# and .NET Core in Visual Studio 2017](library-with-visual-studio.md).

You can also develop a .NET Core console app on Mac, Linux, and Windows by using [Visual Studio Code](https://code.visualstudio.com/), a downloadable code editor. For a step-by-step tutorial, see [Getting Started with Visual Studio Code](with-visual-studio-code.md). -->
