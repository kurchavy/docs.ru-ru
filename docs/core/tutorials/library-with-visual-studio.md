---
title: "Создание библиотеки классов .NET Standard с помощью C# и .NET Core в Visual Studio 2017"
description: "Сведения о создании библиотеки классов .NET Standard, написанной на языке C#, с помощью Visual Studio 2017."
keywords: ".NET Core, библиотека классов .NET Standard, Visual Studio 2017"
author: BillWagner
ms.author: wiwagn
ms.date: 08/07/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: c849ca26-6a25-4d35-9544-f343af88e0e7
ms.translationtype: HT
ms.sourcegitcommit: 3a25c1c3b540bac8ef963a8bbf708b0700c3e9e2
ms.openlocfilehash: 8b86f8f9cd02484cb91af3206606aced8fed1ecd
ms.contentlocale: ru-ru
ms.lasthandoff: 09/08/2017

---
# <a name="building-a-class-library-with-c-and-net-core-in-visual-studio-2017"></a><span data-ttu-id="bb7d1-104">Создание библиотеки классов с помощью C# и .NET Core в Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bb7d1-104">Building a class library with C# and .NET Core in Visual Studio 2017</span></span>

<span data-ttu-id="bb7d1-105">*Библиотека классов* определяет типы и методы, которые могут быть вызваны из любого приложения.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-105">A *class library* defines types and methods that are called by an application.</span></span> <span data-ttu-id="bb7d1-106">Библиотеку классов, предназначенную для .NET Standard 2.0, можно вызывать из любой реализации .NET, которая поддерживает эту версию .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-106">A class library that targets the .NET Standard 2.0 allows your library to be called by any .NET implementation that supports that version of the .NET Standard.</span></span> <span data-ttu-id="bb7d1-107">Когда вы завершите создание библиотеки классов, вы сможете по своему усмотрению распространять ее как независимый компонент или включить в состав одного или нескольких приложений.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-107">When you finish your class library, you can decide whether you want to distribute it as a third-party component or whether you want to include it as a bundled component with one or more applications.</span></span>

> [!NOTE]
> <span data-ttu-id="bb7d1-108">Список версий .NET Standard и поддерживаемых ими платформ см. в разделе [.NET Standard](../../standard/net-standard.md).</span><span class="sxs-lookup"><span data-stu-id="bb7d1-108">For a list of the .NET Standard versions and the platforms they support, see [.NET Standard](../../standard/net-standard.md).</span></span>

<span data-ttu-id="bb7d1-109">В этой статье вы создадите простую служебную библиотеку с одним методом для обработки строк.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-109">In this topic, you'll create a simple utility library that contains a single string-handling method.</span></span> <span data-ttu-id="bb7d1-110">Вы реализуете его как [метод расширения](../../csharp/programming-guide/classes-and-structs/extension-methods.md), чтобы вызывать его так же, как любой член класса <xref:System.String>.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-110">You'll implement it as an [extension method](../../csharp/programming-guide/classes-and-structs/extension-methods.md) so that you can call it as if it were a member of the <xref:System.String> class.</span></span>

## <a name="creating-a-class-library-solution"></a><span data-ttu-id="bb7d1-111">Создание решения для библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="bb7d1-111">Creating a class library solution</span></span>

<span data-ttu-id="bb7d1-112">Начнем с создания решения для нашего проекта библиотеки классов и связанных с ней проектов.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-112">Start by creating a solution for your class library project and its related projects.</span></span> <span data-ttu-id="bb7d1-113">Решение Visual Studio служит контейнером для одного или нескольких проектов.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-113">A Visual Studio Solution just serves as a container for one or more projects.</span></span> <span data-ttu-id="bb7d1-114">Чтобы создать решение, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-114">To create the solution:</span></span>

1. <span data-ttu-id="bb7d1-115">В строке меню Visual Studio выберите **Файл** > **Создать** > **Проект**.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-115">On the Visual Studio menu bar, choose **File** > **New** > **Project**.</span></span>

1. <span data-ttu-id="bb7d1-116">В диалоговом окне **Новый проект** разверните узел **Другие типы проектов** и выберите **Решения Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-116">In the **New Project** dialog, expand the **Other Project Types** node, and select **Visual Studio Solutions**.</span></span> <span data-ttu-id="bb7d1-117">Присвойте решению имя ClassLibraryProjects и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-117">Name the solution "ClassLibraryProjects" and select the **OK** button.</span></span>

   ![Диалоговое окно создания проекта](./media/library-with-visual-studio/newproject.png)

## <a name="creating-the-class-library-project"></a><span data-ttu-id="bb7d1-119">Создание проекта для библиотеки классов</span><span class="sxs-lookup"><span data-stu-id="bb7d1-119">Creating the class library project</span></span>

<span data-ttu-id="bb7d1-120">Теперь можно создать проект библиотеки классов.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-120">Create your class library project:</span></span>

1. <span data-ttu-id="bb7d1-121">В **обозревателе решений** щелкните правой кнопкой мыши решение **ClassLibraryProjects** и в контекстном меню выберите **Добавить** > **Новый проект**.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-121">In **Solution Explorer**, right-click on the **ClassLibraryProjects** solution file and from the context menu, select **Add** > **New Project**.</span></span>

1. <span data-ttu-id="bb7d1-122">В диалоговом окне **Добавление нового проекта** разверните узел **Visual C#**, выберите узел **.NET Standard**, а затем — шаблон проекта **Библиотека классов (.NET Standard)**.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-122">In the **Add New Project** dialog, expand the **Visual C#** node, then select the **.NET Standard** node followed by the **Class Library (.NET Standard)** project template.</span></span> <span data-ttu-id="bb7d1-123">В текстовом поле **Имя** введите имя проекта StringLibrary.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-123">In the **Name** text box, enter "StringLibrary" as the name of the project.</span></span> <span data-ttu-id="bb7d1-124">Нажмите **ОК**, чтобы создать проект библиотеки классов.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-124">Select **OK** to create the class library project.</span></span>

   ![Диалоговое окно "Добавление нового проекта"](./media/library-with-visual-studio/libproject.png)

   <span data-ttu-id="bb7d1-126">Окно кода затем откроется в среде разработки Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-126">The code window then opens in the Visual Studio development environment.</span></span>

   ![Окно приложения Visual Studio, отображающее код шаблона библиотеки классов по умолчанию](./media/library-with-visual-studio/stringlibrary.png)

1. <span data-ttu-id="bb7d1-128">Проверьте, предназначена ли библиотека для правильной версии .NET Standard.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-128">Check to make sure that our library targets the correct version of the .NET Standard.</span></span> <span data-ttu-id="bb7d1-129">В **обозревателе решений** щелкните проект библиотеки правой кнопкой мыши и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-129">Right-click on the library project in the **Solution Explorer** windows, then select **Properties**.</span></span> <span data-ttu-id="bb7d1-130">В текстовом поле **Целевая платформа** указано, что целевой платформой является .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-130">The **Target Framework** text box shows that we're targeting .NET Standard 2.0.</span></span>

   ![Свойства проекта для библиотеки классов](./media/library-with-visual-studio/properties.png)

1. <span data-ttu-id="bb7d1-132">Замените код, отображаемый в окне кода, следующим текстом, а затем сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-132">Replace the code in the code window with the following code and save the file:</span></span>

   <span data-ttu-id="bb7d1-133">[!CODE-csharp[ClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/classlib.cs)]</span><span class="sxs-lookup"><span data-stu-id="bb7d1-133">[!CODE-csharp[ClassLib#1](../../../samples/snippets/csharp/getting_started/with_visual_studio_2017/classlib.cs)]</span></span>

   <span data-ttu-id="bb7d1-134">Библиотека классов (`UtilityLibraries.StringLibrary`) содержит метод с именем `StartsWithUpper`, который возвращает значение <xref:System.Boolean>. Это значение указывает, является ли первым символом текущего экземпляра строки символ верхнего регистра.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-134">The class library, `UtilityLibraries.StringLibrary`, contains a method named `StartsWithUpper`, which returns a <xref:System.Boolean> value that indicates whether the current string instance begins with an uppercase character.</span></span> <span data-ttu-id="bb7d1-135">Символы верхнего регистра определяются по стандарту Юникод.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-135">The Unicode standard distinguishes uppercase characters from lowercase characters.</span></span> <span data-ttu-id="bb7d1-136">Метод <xref:System.Char.IsUpper(System.Char)?displayProperty=fullName> возвращает `true`, если символ является символом верхнего регистра.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-136">The <xref:System.Char.IsUpper(System.Char)?displayProperty=fullName> method returns `true` if a character is uppercase.</span></span>

1. <span data-ttu-id="bb7d1-137">В строке меню выберите **Сборка** > **Собрать решение**.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-137">On the menu bar, select **Build** > **Build Solution**.</span></span> <span data-ttu-id="bb7d1-138">Проект должен скомпилироваться без ошибок.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-138">The project should compile without error.</span></span>

   ![Область вывода, показывающая успешное завершение сборки](./media/library-with-visual-studio/buildsucceeds.png)

## <a name="next-step"></a><span data-ttu-id="bb7d1-140">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bb7d1-140">Next step</span></span>

<span data-ttu-id="bb7d1-141">Итак, вы успешно создали библиотеку.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-141">You've successfully built the library.</span></span> <span data-ttu-id="bb7d1-142">Пока вы еще не вызывали ее методов, поэтому нельзя быть уверенным, что все работает так, как ожидалось.</span><span class="sxs-lookup"><span data-stu-id="bb7d1-142">Because you haven't called any of its methods, you don't know whether it works as expected.</span></span> <span data-ttu-id="bb7d1-143">Следующий шаг в разработке библиотеки — тестирование с помощью [проекта модульного теста](testing-library-with-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="bb7d1-143">The next step in developing your library is to test it by using a [Unit Test Project](testing-library-with-visual-studio.md).</span></span>