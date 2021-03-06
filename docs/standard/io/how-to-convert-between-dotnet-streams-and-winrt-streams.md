---
title: "Практическое руководство. Преобразование между потоками .NET Framework и потоками среды выполнения Windows"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
ms.assetid: 23a763ea-8348-4244-9f8c-a4280b870b47
caps.latest.revision: "15"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.openlocfilehash: 11c22bf71109137ea328b8e1136180494364ce0e
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="how-to-convert-between-net-framework-streams-and-windows-runtime-streams"></a>Практическое руководство. Преобразование между потоками .NET Framework и потоками среды выполнения Windows
.NET Framework для приложений Магазина Windows — это подмножество полной платформы .NET Framework. Из-за требований к безопасности и другим аспектам в приложениях Магазина Windows нельзя использовать полный набор API платформы .NET Framework для открытия и чтения файлов. Дополнительные сведения см. в статье [Обзор .NET для приложений Магазина Windows](http://msdn.microsoft.com/library/windows/apps/br230302.aspx). Однако может потребоваться использовать API платформы .NET Framework для других операций обработки потока. Для работы с потоками может потребоваться выполнить преобразование между типом потока .NET Framework, таким как <xref:System.IO.MemoryStream> или <xref:System.IO.FileStream>, и потоком среды выполнения Windows, таким как [IInputStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.iinputstream.aspx), [IOutputStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.ioutputstream.aspx)или [IRandomAccessStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx).  
  
 Класс <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions>--> `System.IO.WindowsRuntimeStreamExtensions` содержит методы, которые позволяют легко выполнить эти преобразования. Однако существует ряд различий между потоками в платформе .NET Framework и среде выполнения Windows, которые влияют на результаты использования этих методов. Подробности описаны в следующих разделах.  
  
<a name="BKMK_ConvertingfromaWindowsRuntimestreamtoaNETFrameworkstream"></a>   
## <a name="converting-from-a-windows-runtime-stream-to-a-net-framework-stream"></a>Преобразование потока среды выполнения Windows в поток .NET Framework  
 Поток среды выполнения Windows можно преобразовать в поток .NET Framework, используя один из следующих методов <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions>--> `System.IO.WindowsRuntimeStreamExtensions` :  
  
 <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions.AsStream%2A> --> `System.IO.WindowsRuntimeStreamExtensions.AsStream`  
 Преобразует поток прямого доступа в среде выполнения Windows в управляемый поток подмножества .NET для приложений Магазина Windows.  
  
 <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions.AsStreamForWrite%2A> --> `System.IO.WindowsRuntimeStreamExtensions.AsStreamForWrite`
 Преобразует выходной поток в среде выполнения Windows в управляемый поток подмножества .NET для приложений Магазина Windows.  
  
 <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions.AsStreamForRead%2A> --> `System.IO.WindowsRuntimeStreamExtensions.AsStreamForRead`  
 Преобразует входной поток в среде выполнения Windows в управляемый поток подмножества .NET для приложений Магазина Windows.  
  
 Среда выполнения Windows предлагает типы потоков, которые поддерживают только чтение, только запись или же чтение и запись, и эти возможности поддерживаются при преобразовании потока среды выполнения Windows в поток .NET Framework. Кроме того, при преобразовании потока среды выполнения Windows в поток .NET Framework и обратно можно получить исходный экземпляр среды выполнения Windows. Рекомендуется использовать метод преобразования, соответствующий возможностями потока среды выполнения Windows, который необходимо преобразовать. Однако поскольку поток [IRandomAccessStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx) поддерживает чтение и запись (реализует как [IOutputStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.ioutputstream.aspx) , так и [IInputStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.iinputstream.aspx)), любые методы преобразования позволяют сохранить возможности исходного потока. Например, использование <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions.AsStreamForRead%2A> --> `System.IO.WindowsRuntimeStreamExtensions.AsStreamForRead` для преобразования [IRandomAccessStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.irandomaccessstream.aspx) не ограничит возможности преобразованного потока .NET Framework только чтением, поддержка записи также сохранится.  
  
#### <a name="to-convert-from-a-windows-runtime-random-access-stream-to-a-net-framework-stream"></a>Инструкции по преобразованию потока среды выполнения Windows в поток .NET Framework  
  
-   Воспользуйтесь методом <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions.AsStream%2A> --> `System.IO.WindowsRuntimeStreamExtensions.AsStream` .  
  
     В следующем примере кода показано, как предложить пользователю выбрать файл, открыть его с помощью API-интерфейсов среды выполнения Windows, а затем преобразовать его в поток платформы .NET Framework, который считывается и выводится в текстовый блок. В таких случаях перед выводом результатов обычно с помощью API-интерфейсов .NET Framework ведется работа с потоком.  
  
     Для выполнения этого примера необходимо создать XAML-приложение Магазина Windows, которое содержит текстовый блок с именем `TextBlock1` и кнопку с именем  `Button1`. В этом примере событие нажатия кнопки должно быть связано с методом `button1_Click` .  
  
     [!code-csharp[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/cs/mainpage.xaml.cs#imports)]
     [!code-vb[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/vb/mainpage.xaml.vb#imports)]  
    [!code-csharp[System.IO.WindowsRuntimeStreamExtensionsEx#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/cs/mainpage.xaml.cs#1)]
    [!code-vb[System.IO.WindowsRuntimeStreamExtensionsEx#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/vb/mainpage.xaml.vb#1)]  
  
<a name="BKMK_ConvertingfromaNETFrameworkstreamtoaWindowsRuntimestream"></a>   
## <a name="converting-from-a-net-framework-stream-to-a-windows-runtime-stream"></a>Преобразование потока .NET Framework в поток среды выполнения Windows  
 Поток среды выполнения .NET Framework можно преобразовать в поток Windows, используя один из следующих методов <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions>--> `System.IO.WindowsRuntimeStreamExtensions` :  
  
 <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions.AsInputStream%2A> --> `System.IO.WindowsRuntimeStreamExtensions.AsInputStream`  
 Преобразует управляемый поток подмножества .NET для приложений Магазина Windows во входной поток в среде выполнения Windows.  
  
<!--zz <xref:System.IO.WindowsRuntimeStreamExtensions.AsOutputStream%2A>  --> `System.IO.WindowsRuntimeStreamExtensions.AsOutputStream`
 Преобразует управляемый поток подмножества .NET для приложений Магазина Windows в выходной поток в среде выполнения Windows.  
  
 [AsRandomAccessStream](../../../docs/standard/cross-platform/windowsruntimestreamextensions-asrandomaccessstream-method.md)  
 Преобразует управляемый поток подмножества .NET для приложений Магазина Windows в поток прямого доступа, который можно использовать для чтения и записи в среде выполнения Windows.  
  
 При преобразовании потока .NET Framework в поток среды выполнения Windows возможности преобразованного потока зависят от исходного потока. Например, если исходный поток поддерживает чтение и запись, можно вызвать метод <!--zz <xref:System.IO.WindowsRuntimeStreamExtensions.AsInputStream%2A> --> `System.IO.WindowsRuntimeStreamExtensions.AsInputStream` для преобразования потока, после чего будет возвращен тип `IRandomAccessStream`, который реализует  `IInputStream` и `IOutputStream`и поддерживает чтение и запись  
  
 Потоки .NET Framework не поддерживают клонирование даже после преобразования. Это означает, что в случае преобразовании потока .NET Framework в поток среды выполнения Windows с последующим вызовом метода [GetInputStreamAt](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.inmemoryrandomaccessstream.getinputstreamat.aspx) или [GetOutputStreamAt](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.irandomaccessstream.getoutputstreamat.aspx), который вызывает [CloneStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.randomaccessstreamoverstream.clonestream.aspx) , или непосредственным вызовом метода [CloneStream](http://msdn.microsoft.com/library/windows/apps/windows.storage.streams.randomaccessstreamoverstream.clonestream.aspx) возникает исключение.  
  
#### <a name="to-convert-from-a-net-framework-stream-to-a-windows-runtime-random-access-stream"></a>Инструкции по преобразованию потока .NET Framework в поток среды выполнения Windows  
  
-   Используйте метод [AsRandomAccessStream](../../../docs/standard/cross-platform/windowsruntimestreamextensions-asrandomaccessstream-method.md) , как показано в следующем примере.  
  
    > [!IMPORTANT]
    >  Убедитесь, что используемый вами поток .NET Framework поддерживает поиск, или скопируйте его в поток, поддерживающий поиск. Чтобы это определить, используйте свойство <xref:System.IO.Stream.CanSeek%2A?displayProperty=nameWithType>.  
  
     Для выполнения этого примера необходимо создать XAML-приложение Магазина Windows, предназначенное для .NET Framework 4.5.1 и содержащее текстовый блок с именем `TextBlock2` и кнопку с именем `Button2`. В этом примере событие нажатия кнопки должно быть связано с методом `button2_Click` .  
  
     [!code-csharp[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/cs/mainpage.xaml.cs#imports)]
     [!code-vb[System.IO.WindowsRuntimeStreamExtensionsEx#Imports](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/vb/mainpage.xaml.vb#imports)]  
    [!code-csharp[System.IO.WindowsRuntimeStreamExtensionsEx#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/cs/mainpage.xaml.cs#2)]
    [!code-vb[System.IO.WindowsRuntimeStreamExtensionsEx#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.io.windowsruntimestreamextensionsex/vb/mainpage.xaml.vb#2)]  
  
## <a name="see-also"></a>См. также  
 [Краткое руководство: Чтение и запись файлов (Windows)](http://msdn.microsoft.com/library/windows/apps/hh464978.aspx)  
 [Обзор приложений .NET для магазина Windows](http://msdn.microsoft.com/library/windows/apps/br230302.aspx)  
 [Поддерживаемые API .NET для приложений Магазина Windows](http://msdn.microsoft.com/library/windows/apps/br230232.aspx)
