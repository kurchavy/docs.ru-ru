---
title: "Пользовательское действие Hello World"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 72b1dd0a-9aad-47d5-95a9-a1024ee1d0a1
caps.latest.revision: "12"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 155726e5cd65c2f31a3205a8d18f662b66fb40e8
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="hello-world-custom-activity"></a>Пользовательское действие Hello World
В этом образце показано несколько ключевых возможностей [!INCLUDE[wf](../../../../includes/wf-md.md)], включая создание простого настраиваемого действия. Некоторые возможности, демонстрируемые в этом образце, создают пользовательское действие в C# и используют аргументы `in` и `out` (<xref:System.Activities.InArgument> и <xref:System.Activities.OutArgument>).  
  
> [!IMPORTANT]
>  Образцы уже могут быть установлены на компьютере. Перед продолжением проверьте следующий каталог (по умолчанию).  
>   
>  `<InstallDrive>:\WF_WCF_Samples`  
>   
>  Если этот каталог не существует, перейдите на страницу [Примеры Windows Communication Foundation (WCF) и Windows Workflow Foundation (WF) для .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) , чтобы скачать все примеры [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] и [!INCLUDE[wf1](../../../../includes/wf1-md.md)] . Этот образец расположен в следующем каталоге.  
>   
>  `<InstallDrive>:\WF_WCF_Samples\WF\Basic\CustomActivities\Code-Bodied\HelloWorld`  
  
## <a name="creating-a-workflow-in-code"></a>Создание рабочего процесса в коде  
 В этом образце создаются два пользовательских действия с использованием кода C#. Оба пользовательских действия наследуют непосредственно или косвенно от <xref:System.Activities.Activity%601> для возвращения одного значения. Преимуществом использования универсального возвращаемого значения вместо наследования от неуниверсального класса <xref:System.Activities.Activity> является то, что некоторые действия (такие как <xref:System.Activities.Statements.Assign>) могут обращаться к возвращаемому значению, если они используются как часть составного действия.  
  
 AppendString  
 Это действие наследует от класса <xref:System.Activities.Activity%601> и использует действие <xref:System.Activities.Statements.Assign>, которое объединяет две строки.  
  
 Prepend String  
 Это действие наследует непосредственно от <xref:System.Activities.CodeActivity%601> и создает аналогичные функциональные возможности для действия `AppendString`, которое использует логику, реализуемую в коде, а не уже имеющееся действие.  
  
 В этот проект включены следующие файлы.  
  
 AppendString.cs  
 Пользовательское действие, которое присоединяет строки друг к другу. Он принимает строку и объединяет их с текстовой строкой «говорит Здравствуй, мир!» в форму выходе полного сообщения.  
  
 PrependString.cs  
 Это действие вставляет заранее определенную строку в начало входной строки.  
  
 Sequence1.xaml  
 Рабочий процесс, который использует пользовательские действия `AppendString` и `PrependString`.  
  
 Program.cs  
 Программа, которая выполняет рабочий процесс.  
  
#### <a name="to-use-this-sample"></a>Использование этого образца  
  
1.  Откройте в среде [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] файл решения HelloWorld.sln.  
  
2.  Для построения решения нажмите CTRL+SHIFT+B.  
  
3.  Чтобы запустить решение, нажмите клавишу F5.