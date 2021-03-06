---
title: "Общие сведения о TextPattern модели автоматизации пользовательского интерфейса"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- UI Automation, TextPattern class
- TextPattern class
- classes, TextPattern
ms.assetid: 41787927-df1f-4f4a-aba3-641662854fc4
caps.latest.revision: "38"
author: Xansky
ms.author: mhopkins
manager: markl
ms.workload: dotnet
ms.openlocfilehash: 610b2d44fca43f2745b7b423a5cdb73c5a7d74d1
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="ui-automation-textpattern-overview"></a>Общие сведения о TextPattern модели автоматизации пользовательского интерфейса
> [!NOTE]
>  Эта документация предназначена для разработчиков .NET Framework, желающих использовать управляемые классы [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , заданные в пространстве имен <xref:System.Windows.Automation> . Последние сведения о [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]см. в разделе [API автоматизации Windows. Автоматизация пользовательского интерфейса](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 В этом обзоре описывается использование [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] для предоставления текстового содержимого, в том числе атрибутов формата и стиля, текстовых элементов управления на платформах, поддерживаемых [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]. Помимо прочих, в эти элементы управления входят [!INCLUDE[TLA#tla_winfx](../../../includes/tlasharptla-winfx-md.md)] <xref:System.Windows.Controls.TextBox> и <xref:System.Windows.Controls.RichTextBox> а также их эквиваленты [!INCLUDE[TLA2#tla_win32](../../../includes/tla2sharptla-win32-md.md)] .  
  
 Предоставление текстового содержимого элемента управления осуществляется с помощью шаблона элемента управления <xref:System.Windows.Automation.TextPattern> , который представляет содержимое текстового контейнера в качестве текстового потока. В свою очередь <xref:System.Windows.Automation.TextPattern> требует поддержки класса <xref:System.Windows.Automation.Text.TextPatternRange> для предоставления атрибутов формата и стиля. <xref:System.Windows.Automation.Text.TextPatternRange> поддерживает <xref:System.Windows.Automation.TextPattern> , предоставляя непрерывный текст или несколько раздельных фрагментов текста в текстовый контейнер с коллекцией конечных точек <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start> и <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> . <xref:System.Windows.Automation.Text.TextPatternRange> поддерживает такие функциональные возможности, как выбор, сравнение, извлечение и обход.  
  
> [!NOTE]
>  Классы <xref:System.Windows.Automation.TextPattern> не предоставляют средства для вставки или изменения текста. Тем не менее в зависимости от элемента управления это может выполняться [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] <xref:System.Windows.Automation.ValuePattern> или посредством прямого ввода с клавиатуры. Пример см. в разделе [TextPattern Insert Text Sample](http://msdn.microsoft.com/en-us/67353f93-7ee2-42f2-ab76-5c078cf6ca16) .  
  
 Функции, описанные в этом обзоре, исключительно важны для поставщиков вспомогательных технологий и их пользователей. Вспомогательные технологии могут использовать [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] для сбора полных сведений о форматировании текста для пользователя и предоставления программной навигации и выбора текста с помощью <xref:System.Windows.Automation.Text.TextUnit> (символа, слова, строки или абзаца).  
  
<a name="UI_Automation_TextPattern_vs__Cicero"></a>   
## <a name="ui-automation-textpattern-vs-text-services-framework"></a>Сравнение TextPattern модели автоматизации пользовательского интерфейса и  инфраструктуры текстовых служб (TSF)  
 [!INCLUDE[TLA#tla_tsf](../../../includes/tlasharptla-tsf-md.md)] — это простая и масштабируемая системная инфраструктура, которая обеспечивает службы естественных языков и расширенный ввод текста на рабочем столе и в приложениях. Помимо обеспечения интерфейсов для приложений, чтобы предоставлять их текстовое хранилище, она также поддерживает метаданные для этого текстового хранилища.  
  
 Однако [!INCLUDE[TLA2#tla_tsf](../../../includes/tla2sharptla-tsf-md.md)] была разработана для приложений, которым требуется вставлять входные данные в контекстно зависимые сценарии, в то время как <xref:System.Windows.Automation.TextPattern> является решением только для чтения (с ограниченным обходным путем, указанным выше), предназначенным для обеспечения оптимизированного доступа к текстовому хранилищу для средств чтения с экрана и устройств с использованием шрифта Брайля.  
  
 Иными словами, доступные технологии, которым необходим доступ только для чтения к текстовому хранилищу, могут использовать <xref:System.Windows.Automation.TextPattern>, но потребуется более сложная функциональность [!INCLUDE[TLA2#tla_tsf](../../../includes/tla2sharptla-tsf-md.md)] для контекстно зависимого ввода.  
  
<a name="Control_Types"></a>   
## <a name="control-types"></a>Типы элементов управления  
  
#### <a name="text"></a>Text  
 Элемент управления «Текст» является базовым элементом, представляющим фрагмент текста на экране.  
  
 Отдельный элемент управления «Текст» может использоваться в качестве метки или статического текста в форме. Элементы управления «Текст» могут также содержаться в структуре <xref:System.Windows.Automation.ControlType.ListItem>, <xref:System.Windows.Automation.ControlType.TreeItem> или <xref:System.Windows.Automation.ControlType.DataItem>.  
  
> [!NOTE]
>  Элементы управления "Текст" могут не отображаться в представлении содержимого дерева [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] (см. раздел [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)). Это объясняется тем, что элементы управления «Текст» часто отображаются посредством свойства «Имя» другого элемента управления. Например текст, который используется для метки элемента управления «Поле ввода», предоставляется посредством свойства «Имя» элемента управления «Поле ввода». Поскольку элемент управления «Поле ввода» находится в представлении содержимого дерева [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] , сам текстовый элемент не обязательно должен присутствовать в этом представлении дерева [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] . Единственный текст, который отображается в представлении содержимого, это текст, не являющийся избыточными сведениями. Это позволяет любой вспомогательной технологии быстро отфильтровывать только те части сведений, которые нужны пользователям.  
  
#### <a name="edit"></a>Edit  
 Элементы управления «Поле ввода» предоставляют пользователям возможность просматривать и редактировать одну строку текста.  
  
> [!NOTE]
>  В некоторых сценариях макета одна строка текста может переноситься.  
  
#### <a name="document"></a>Document  
 С помощью элементов управления «Документ» пользователи могут перемещаться по нескольким страницам текста и получать из них сведения.  
  
<a name="TextPattern_Client_API_s"></a>   
## <a name="textpattern-client-apis"></a>API клиента TextPattern  
  
|||  
|-|-|  
|`System.Windows.Automation.TextPattern Class`|Точка входа для текстовой модели [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] .<br /><br /> Этот класс также содержит два прослушивателя событий <xref:System.Windows.Automation.TextPattern> , <xref:System.Windows.Automation.TextPattern.TextSelectionChangedEvent> и <xref:System.Windows.Automation.TextPattern.TextChangedEvent>.|  
|`System.Windows.Automation.Text.TextPatternRange Class`|Представление фрагмента текста в текстовом контейнере, который поддерживает <xref:System.Windows.Automation.TextPattern>.<br /><br /> Клиенты автоматизации пользовательского интерфейса должны уделять особое внимание текущей действительности текстового диапазона, созданного с помощью <xref:System.Windows.Automation.Text.TextPatternRange>. Если исходный текст в элементе управления «Текст» полностью заменяется новым текстом, текущий диапазон текста становится недействительным. Однако текстовый диапазон по-прежнему может иметь некоторую целесообразность, если изменялась только часть исходного текста, и базовый элемент управления «Текст» управляет своим текстовым «указателем» с помощью привязок (или конечных точек), а не с помощью абсолютного расположения символов.<br /><br /> Клиенты могут прослушивать <xref:System.Windows.Automation.TextPattern.TextChangedEvent> для уведомления о каких-либо изменениях текстового содержимого, с которым они работают.|  
|`System.Windows.Automation.AutomationTextAttribute Class`|Используется для идентификации атрибутов форматирования текстового диапазона.|  
  
<a name="TextPattern_Provider_API_s"></a>   
## <a name="textpattern-provider-apis"></a>API поставщика TextPattern  
 Элементы пользовательского интерфейса или элементы управления, которые поддерживают <xref:System.Windows.Automation.TextPattern> путем реализации интерфейсов <xref:System.Windows.Automation.Provider.ITextProvider> и <xref:System.Windows.Automation.Provider.ITextRangeProvider> либо непосредственно, либо через прокси [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] , могут предоставлять подробные сведения об атрибутах для любого текста, который они содержат, а также мощные возможности навигации.  
  
 Поставщик <xref:System.Windows.Automation.TextPattern> не должен поддерживать все атрибуты текста, если элемент управления не предоставляет поддержку для какого-либо конкретного атрибута.  
  
 Поставщик <xref:System.Windows.Automation.TextPattern> должен поддерживать функции <xref:System.Windows.Automation.TextPattern.GetSelection%2A> и <xref:System.Windows.Automation.Text.TextPatternRange.Select%2A> , если элемент управления поддерживает выделение текста или помещение текстового курсора (или системного курсора) в текстовое поле. Если элемент управления не поддерживает эту функциональность, то он не должен поддерживать ни один из этих методов. Однако этот элемент управления должен предоставлять тип выделения текста, который он поддерживает, путем реализации свойства <xref:System.Windows.Automation.Provider.ITextProvider.SupportedTextSelection%2A> .  
  
 Поставщик <xref:System.Windows.Automation.TextPattern> всегда должен поддерживать константы <xref:System.Windows.Automation.Text.TextUnit> <xref:System.Windows.Automation.Text.TextUnit.Character> и <xref:System.Windows.Automation.Text.TextUnit.Document> , а также любые другие константы <xref:System.Windows.Automation.Text.TextUnit> , которые он способен поддерживать.  
  
> [!NOTE]
>  Поставщик может пропустить поддержку определенных <xref:System.Windows.Automation.Text.TextUnit> откладывая поддержку до следующего наибольшего объекта <xref:System.Windows.Automation.Text.TextUnit> , поддерживаемого в следующем порядке: <xref:System.Windows.Automation.Text.TextUnit.Character>, <xref:System.Windows.Automation.Text.TextUnit.Format>, <xref:System.Windows.Automation.Text.TextUnit.Word>, <xref:System.Windows.Automation.Text.TextUnit.Line>, <xref:System.Windows.Automation.Text.TextUnit.Paragraph>, <xref:System.Windows.Automation.Text.TextUnit.Page>и <xref:System.Windows.Automation.Text.TextUnit.Document>.  
  
|||  
|-|-|  
|`ITextProvider Interface`|Предоставляет методы, свойства и атрибуты, которые поддерживают <xref:System.Windows.Automation.TextPattern> в клиентских приложениях (см. <xref:System.Windows.Automation.Provider.ITextProvider>).|  
|`ITextRangeProvider Interface`|Представляет фрагмент текста в поставщике текста (см. <xref:System.Windows.Automation.Provider.ITextRangeProvider>).|  
|`System.Windows.Automation.TextPatternIdentifiers Class`|Содержит значения, используемые в качестве идентификаторов для поставщиков текста (см. <xref:System.Windows.Automation.TextPatternIdentifiers>).|  
  
<a name="Security"></a>   
## <a name="security"></a>Безопасность  
 Классы [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] разработана с учетом безопасности (см. раздел [UI Automation Security Overview](../../../docs/framework/ui-automation/ui-automation-security-overview.md)). Однако для классов TextPattern, рассматриваемых в этом обзоре, требуются некоторые особые рекомендации по обеспечению безопасности.  
  
-   Поставщики текста[!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] предоставляют интерфейсы только для чтения и не предоставляют возможность изменения существующего текста в элементе управления.  
  
-   Клиенты автоматизации пользовательского интерфейса могут использовать [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] , только если являются полностью "доверенными". Примером будет защищенный рабочий стол входа в систему, где можно запускать только известные и доверенные приложения.  
  
-   Разработчики поставщиков автоматизации пользовательского интерфейса должны иметь в виду, что все данные, которые они предполагают предоставлять в своих элементах управления с помощью [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] , по существу являются открытыми и полностью доступными другому коду. [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] не пытается определить надежность любого клиента автоматизации пользовательского интерфейса и, следовательно, поставщик автоматизации пользовательского интерфейса не должен предоставлять защищенное содержимое или конфиденциальные текстовые сведения (например, поля паролей).  
  
-   Одно из наиболее важных изменений в системе безопасности [!INCLUDE[TLA#tla_winvista](../../../includes/tlasharptla-winvista-md.md)] широко известно как «безопасный ввод», который включает такие технологии, как учетные записи пользователей с минимальными привилегиями или ограниченные учетные записи пользователей(LUA) и изоляция уровня привилегий пользовательского интерфейса (UIPI).  
  
    -   UIPI запрещает программам управление и наблюдение за другими более «привилегированными» программами, предотвращая межпроцессные атаки оконных сообщений, которые подделывают пользовательский ввод.  
  
    -   LUA устанавливает ограничения на права приложений, запускаемых пользователями из группы «Администраторы». Приложения не обязательно будут иметь административные привилегии, но будут выполняться с наименьшими необходимыми правами. В результате в сценариях LUA возможны некоторые ограничения. В первую очередь это усечение строк (в том числе строк TextPattern), где это может требоваться для ограничения размера строк, извлекаемых из приложений уровня администратора, чтобы им не приходилось выделять память до момента отключения приложения.  
  
<a name="Performance"></a>   
## <a name="performance"></a>Производительность  
 Поскольку TextPattern основывается на межпроцессных вызовах для большей части своих функциональных возможностей, он не предоставляет механизм кэширования для повышения производительности при обработке содержимого. В этом состоит отличие от других шаблонов элементов управления в [!INCLUDE[TLA#tla_uiautomation](../../../includes/tlasharptla-uiautomation-md.md)] , которые могут быть доступны с помощью методов <xref:System.Windows.Automation.AutomationElement.GetCachedPattern%2A> или <xref:System.Windows.Automation.AutomationElement.TryGetCachedPattern%2A> .  
  
 Один из способов повышения производительности состоит в том, чтобы клиенты автоматизации пользовательского интерфейса гарантированно пытались извлекать блоки текста среднего размера с помощью <xref:System.Windows.Automation.Text.TextPatternRange.GetText%2A>. Например, вызовы GetText(1) повлекут за собой межпроцессные попадания для каждого символа, тогда как один вызов GetText(-1) повлечет за собой одно межпроцессное попадание, но может иметь высокую задержку в зависимости от размера поставщика текста.  
  
<a name="Glossary"></a>   
## <a name="textpattern-terminology"></a>Терминология TextPattern  
 **Attribute (XElement Dynamic Property)** (Attribute (динамическое свойство XElement))  
 Характеристика форматирования текстового диапазона (например, <xref:System.Windows.Automation.TextPattern.IsItalicAttribute> или <xref:System.Windows.Automation.TextPattern.FontNameAttribute>).  
  
 **Вырожденный диапазон**  
 Вырожденный диапазон — это пустой или содержащий нулевые символы текстовый диапазон. Применительно к целям шаблона элемента управления TextPattern точка вставки текста (или системного курсора) считается вырожденным диапазоном. Если никакой текст не выбран, метод <xref:System.Windows.Automation.TextPattern.GetSelection%2A> вернет вырожденный диапазон в точке вставки текста, а метод <xref:System.Windows.Automation.TextPattern.RangeFromPoint%2A> вернет вырожденный диапазон в качестве своей начальной точки. Методы<xref:System.Windows.Automation.TextPattern.RangeFromChild%2A> и <xref:System.Windows.Automation.TextPattern.GetVisibleRanges%2A> могут возвращать вырожденные диапазоны, когда поставщик текста не может найти текстовые диапазоны, соответствующие заданному условию. Этот вырожденный диапазон можно использовать в качестве начальной точки в поставщике текста. Методы<xref:System.Windows.Automation.Text.TextPatternRange.FindText%2A> и <xref:System.Windows.Automation.Text.TextPatternRange.FindAttribute%2A> возвращают пустую ссылку (`Nothing` в [!INCLUDE[TLA2#tla_visualbnet](../../../includes/tla2sharptla-visualbnet-md.md)]), чтобы не путать обнаруженный диапазон и вырожденный диапазон.  
  
 **Внедренный объект**  
 В текстовой модели [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] существует два типа внедренных объектов. Они состоят из элементов с текстовым содержимым, таких как гиперссылки или таблицы, и элементов управления, таких как изображения и кнопки. Дополнительные сведения см. в разделе [Access Embedded Objects Using UI Automation](../../../docs/framework/ui-automation/access-embedded-objects-using-ui-automation.md).  
  
 **Конечная точка**  
 Абсолютная точка <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.Start> или <xref:System.Windows.Automation.Text.TextPatternRangeEndpoint.End> текстового диапазона в текстовом контейнере.  
  
 ![TextPatternRangeEndpoints &#40; начала и окончания &#41;. ] (../../../docs/framework/ui-automation/media/uia-textpattern-endpoints.PNG "UIA_TextPattern_Endpoints")  
Ниже демонстрируется задание начальной и конечной точками.  
  
 **TextRange**  
 Представление фрагмента текста с начальной и конечной точками в текстовом контейнере, включающее все связанные атрибуты и функциональные возможности.  
  
 <xref:System.Windows.Automation.Text.TextUnit>  
 Предопределенная единица текста (символ, слово, строка или абзац), используемая для навигации по логическим сегментам текстового диапазона.  
  
## <a name="see-also"></a>См. также  
 [Шаблоны элементов управления модели автоматизации пользовательского интерфейса для клиентов](../../../docs/framework/ui-automation/ui-automation-control-patterns-for-clients.md)  
 [Общие сведения о шаблонах элементов управления модели автоматизации пользовательского интерфейса](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md)  
 [Общие сведения о дереве модели автоматизации пользовательского интерфейса](../../../docs/framework/ui-automation/ui-automation-tree-overview.md)  
 [Использование кэширования в модели автоматизации пользовательского интерфейса](../../../docs/framework/ui-automation/use-caching-in-ui-automation.md)  
 [Поддержка шаблонов элементов управления в поставщике автоматизации пользовательского интерфейса](../../../docs/framework/ui-automation/support-control-patterns-in-a-ui-automation-provider.md)  
 [Сопоставление шаблона элемента управления для клиентов автоматизации пользовательского интерфейса](../../../docs/framework/ui-automation/control-pattern-mapping-for-ui-automation-clients.md)  
 [Платформа текстовых служб](http://msdn.microsoft.com/library/default.asp?url=/library/tsf/tsf/text_services_framework.asp)
