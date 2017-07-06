---
title: "UI Automation Support for the Spinner Control Type | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "UI Automation, Spinner control type"
  - "Spinner control type"
  - "control types, Spinner"
ms.assetid: 3a29d185-65d8-42e3-bcc3-7f43e96f40c5
caps.latest.revision: 21
author: "Xansky"
ms.author: "mhopkins"
manager: "markl"
caps.handback.revision: 21
---
# UI Automation Support for the Spinner Control Type
> [!NOTE]
>  Эта документация предназначена для разработчиков .NET Framework, желающих использовать управляемые классы [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], заданные в пространстве имен <xref:System.Windows.Automation>. Последние сведения о [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] см. в разделе [API автоматизации Windows. Автоматизация пользовательского интерфейса](http://go.microsoft.com/fwlink/?LinkID=156746).  
  
 В этом разделе содержатся сведения о поддержке [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] типа элемента управления Spinner. В [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] тип элемента управления — это набор условий, которым должен удовлетворять элемент управления для использования свойства <xref:System.Windows.Automation.AutomationElement.ControlTypeProperty>. Условия включают конкретные правила для древовидной структуры [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], значений свойств [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] и шаблонов элементов управления.  
  
 Элементы управления "Счетчик" используются для выбора из домена элементов или диапазона чисел.  
  
 В следующих разделах описывается необходимая древовидная структура [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], свойства, шаблоны элементов управления и события для типа элемента управления Spinner. Требования [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] применяются ко всем элементам управления "Счетчик", будь это [!INCLUDE[TLA#tla_winclient](../../../includes/tlasharptla-winclient-md.md)], [!INCLUDE[TLA#tla_win32](../../../includes/tlasharptla-win32-md.md)] или [!INCLUDE[TLA#tla_winforms](../../../includes/tlasharptla-winforms-md.md)].  
  
<a name="Required_UI_Automation_Tree_Structure"></a>   
## Требуемая древовидная структура модели автоматизации пользовательского интерфейса  
 В следующей таблице описываются представление элемента управления и представление содержимого дерева [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], которые относятся к элементам управления "Счетчик", когда они поддерживают шаблоны элементов управления Range Value, Value и Selection, и показывается, что может содержаться в каждом представлении. Дополнительные сведения о дереве [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] см. в разделе [UI Automation Tree Overview](../../../docs/framework/ui-automation/ui-automation-tree-overview.md).  
  
 **Шаблон элемента управления Range Value или Value**  
  
|Представление элемента управления|Представление содержимого|  
|---------------------------------------|-------------------------------|  
|Spinner<br /><br /> -   Edit \(0 или 1\)<br />-   Button \(2\)|Spinner|  
  
 **Selection \- шаблон элемента управления**  
  
|Представление элемента управления|Представление содержимого|  
|---------------------------------------|-------------------------------|  
|Spinner<br /><br /> -   Edit \(0 или 1\)<br />-   Button \(2\)<br />-   ListItem \(0 или более\)|Spinner<br /><br /> -   ListItem \(0 или более\)|  
  
 Чтобы средства автоматических тестов гарантированно могли различить две кнопки в поддереве представления элемента управления, назначьте `SmallIncrement` или `SmallDecrement` `AutomationId` соответствующим образом. В некоторых реализациях связанный элемент управления "Поле ввода" может быть одноранговым с элементом управления "Счетчик".  
  
<a name="Required_UI_Automation_Properties"></a>   
## Требуемые свойства модели автоматизации пользовательского интерфейса  
 В следующей таблице перечислены свойства [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], значения или определения которых особенно актуальны для элементов управления "Счетчик". Дополнительные сведения о свойствах [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)] см. в разделе [UI Automation Properties for Clients](../../../docs/framework/ui-automation/ui-automation-properties-for-clients.md).  
  
|Свойство [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)].|Значение|Примечания|  
|-------------------------------------------------------------------------------------|--------------|----------------|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationIdProperty>|См. примечания.|Значение этого свойства должно быть уникальным среди всех элементов управления в приложении.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|См. примечания.|Внешний прямоугольник, содержащий весь элемент управления.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ClickablePointProperty>|См. примечания.|Активная точка управления "Счетчик" перемещает фокус в область редактирования элемента управления.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsKeyboardFocusableProperty>|См. примечания.|Если элемент управления может получать фокус клавиатуры, он должен поддерживать это свойство.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.NameProperty>|См. примечания.|Обычно элемент управления "Счетчик" получает имя из статической текстовой метки.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LabeledByProperty>|См. примечания.|Элементы управления "Счетчик" имеют метку со статическим текстом.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.ControlTypeProperty>|Spinner|Это значение одинаково для всех инфраструктур пользовательского интерфейса.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.LocalizedControlTypeProperty>|"счетчик"|Локализованная строка, соответствующая типу элемента управления Spinner.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsContentElementProperty>|True|Элемент управления "Счетчик" всегда должен быть содержимым.|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.IsControlElementProperty>|True|Элемент управления "Счетчик" всегда должен быть элементом управления.|  
  
<a name="Required_UI_Automation_Control_Patterns_and_Properties"></a>   
## Необходимые шаблоны и свойства элементов управления модели автоматизации пользовательского интерфейса  
 В следующей таблице перечислены шаблоны элементов управления [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], которые должны поддерживаться элементами управления "Счетчик". Дополнительные сведения о шаблонах элементов управления см. в разделе [UI Automation Control Patterns Overview](../../../docs/framework/ui-automation/ui-automation-control-patterns-overview.md).  
  
|Шаблон элемента управления\/свойство шаблона|Поддержка\/значение|Примечания|  
|--------------------------------------------------|-------------------------|----------------|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider>|Зависит от обстоятельств|Элементы управления "Счетчик", имеющие список выбираемых элементов, должны поддерживать этот шаблон.|  
|<xref:System.Windows.Automation.Provider.ISelectionProvider.CanSelectMultiple%2A>|False|Элементы управления "Счетчик" всегда являются контейнерами с возможностью выбора одного варианта.|  
|<xref:System.Windows.Automation.Provider.IRangeValueProvider>|Зависит от обстоятельств|Элементы управления "Счетчик", которые охватывают числовой диапазон, могут поддерживать этот шаблон.|  
|<xref:System.Windows.Automation.Provider.IValueProvider>|Зависит от обстоятельств|Элементы управления "Счетчик", которые охватывают дискретный набор параметров или чисел, могут поддерживать этот шаблон.|  
  
<a name="Required_UI_Automation_Events"></a>   
## Необходимые события модели автоматизации пользовательского интерфейса  
 В следующей таблице перечислены события [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)], которые должны поддерживаться всеми элементами управления "Счетчик". Дополнительные сведения о событиях см. в разделе [UI Automation Events Overview](../../../docs/framework/ui-automation/ui-automation-events-overview.md).  
  
|Событие [!INCLUDE[TLA2#tla_uiautomation](../../../includes/tla2sharptla-uiautomation-md.md)]|Поддержка|Примечания|  
|-----------------------------------------------------------------------------------|---------------|----------------|  
|<xref:System.Windows.Automation.SelectionPatternIdentifiers.InvalidatedEvent>|Зависит от обстоятельств|Нет|  
|Событие изменения свойства <xref:System.Windows.Automation.AutomationElementIdentifiers.BoundingRectangleProperty>|Обязательно|Нет|  
|Событие изменения свойства <xref:System.Windows.Automation.AutomationElementIdentifiers.IsOffscreenProperty>|Обязательно|Нет|  
|Событие изменения свойства <xref:System.Windows.Automation.AutomationElementIdentifiers.IsEnabledProperty>|Обязательно|Нет|  
|Событие изменения свойства <xref:System.Windows.Automation.ValuePatternIdentifiers.ValueProperty>|Зависит от обстоятельств|Нет|  
|Событие изменения свойства <xref:System.Windows.Automation.RangeValuePatternIdentifiers.ValueProperty>|Зависит от обстоятельств|Нет|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.AutomationFocusChangedEvent>|Обязательный|Нет|  
|<xref:System.Windows.Automation.AutomationElementIdentifiers.StructureChangedEvent>|Обязательный|Нет|  
  
## См. также  
 <xref:System.Windows.Automation.ControlType.Spinner>   
 [UI Automation Control Types Overview](../../../docs/framework/ui-automation/ui-automation-control-types-overview.md)   
 [UI Automation Overview](../../../docs/framework/ui-automation/ui-automation-overview.md)