---
title: "Фильтрация"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4002946c-e34a-4356-8cfb-e25912a4be63
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 6f67a7f6ac423bd66d9d25b834edc9cf55a5d6a8
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="filtering"></a>Фильтрация
Система фильтрации [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] может использовать декларативные фильтры для сопоставления сообщений и принятия операционных решений. Фильтры можно использовать для определения того, что делать с сообщением, основываясь на проверке части сообщения. Процесс организации очереди, например, может использовать запрос XPath 1.0 для проверки элемента приоритета заданного заголовка, чтобы определить, требуется ли переместить сообщение вперед по очереди.  
  
 Система фильтрации состоит из набора классов, которые позволяют определить, какому набору фильтров присвоено значение `true` для определенного сообщения [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Система фильтрации является ключевым компонентом обмена сообщениями [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] и разработана для обеспечения максимальной скорости. Каждая реализация фильтра оптимизирована для определенного типа сопоставления сообщениям [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Система фильтрации не является потокобезопасной. Приложение должно обрабатывать любую семантику блокировки. Однако оно поддерживает один пишущий поток и несколько читающих потоков.  
  
## <a name="where-filtering-fits"></a>Применение фильтрации  
 Фильтрация выполняется после получения сообщения и является частью процесса диспетчеризации сообщения в соответствующий компонент приложения. В структуре системы фильтрации учитываются требования нескольких подсистем [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], включая обмен сообщениями, маршрутизацию, безопасность, обработку событий и управление системой.  
  
## <a name="filters"></a>Фильтры  
 Модуль фильтрации состоит из двух основных компонентов: фильтров и таблиц фильтров. Фильтр принимает логические решения относительно сообщения на основании логических условий, заданных пользователем. Фильтры реализуют класс <xref:System.ServiceModel.Dispatcher.MessageFilter>.  
  
 Методы <xref:System.ServiceModel.Dispatcher.MessageFilter.Match%2A> используются для определения соответствия сообщения фильтру. Один из методов проверяет заголовок сообщения, но не может проверить тело сообщения. Другой метод принимает *буфер сообщений* в качестве входного параметра и может проверять текст сообщения.  
  
 Как правило, фильтры проверяются не по отдельности, а в составе таблицы фильтров, которая является универсальным классом, создаваемым методом <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601.CreateFilterTable%2A>.  
  
 Существует несколько типов фильтров, каждый из которых предназначен для соответствия определенному типу логического условия. После создания фильтра изменить его условия невозможно. Чтобы изменить условия фильтра, необходимо создать новый фильтр и удалить существующий.  
  
### <a name="action-filters"></a>Фильтры действий  
 Фильтр действий <xref:System.ServiceModel.Dispatcher.ActionMessageFilter> содержит список строк действий. Если какое-либо действие в списке фильтра соответствует заголовку действия в сообщении или в буфере сообщений, метод `Match` возвращает значение `true`. Если этот список пуст, считается, что фильтр соответствует всем действиям в любом сообщении или в буфере сообщений, и метод `Match` возвращает значение `true`. Если никакие действия в списке фильтра не соответствуют заголовку действия в сообщении или в буфере сообщений, метод `Match` возвращает значение `false`. Если сообщение не содержит действий, а список непуст, метод `Match` возвращает значение `false`.  
  
### <a name="endpoint-address-filters"></a>Фильтры адресов конечных точек  
 Фильтр адресов конечных точек <xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter> фильтрует сообщения и буферы сообщений по адресам конечных точек, представленным в коллекции заголовков. Чтобы сообщение прошло такой фильтр, должны выполняться следующие условия.  
  
-   Универсальный код ресурса (URI) адреса, указанный в фильтре, должен в заголовке сообщения "Кому".  
  
-   Каждому параметру конечной точки в адресе фильтра (коллекция `address.Headers`) должен сопоставляться заголовок в сообщении. Дополнительные заголовки в сообщении или в буфере сообщений допустимы для сохранения значения соответствия `true`.  
  
### <a name="prefix-endpoint-address-filters"></a>Фильтры префиксов адресов конечных точек  
  
1.  Принцип действия фильтра <xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter> аналогичен принципу действия фильтра <xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter>, за исключением того, что сопоставляется префикс универсального кода ресурса (URI) сообщения. Например, фильтр, задающий адрес http://www.adatum.com, соответствует сообщениям, направленным по адресу http://www.adatum.com/userA.  
  
### <a name="xpath-message-filters"></a>Фильтры сообщений XPath  
 Фильтр сообщений <xref:System.ServiceModel.Dispatcher.XPathMessageFilter> использует выражение XPath для определения, содержит ли документ XML конкретные элементы, атрибуты, текст или другие конструкции синтаксиса XML. Фильтр оптимизирован для максимальной эффективности при работе со строгим подмножеством XPath. Описывается язык XML Path в [путь язык W3C XML 1.0 спецификация](http://go.microsoft.com/fwlink/?LinkId=94779).  
  
 Обычно приложение использует фильтр <xref:System.ServiceModel.Dispatcher.XPathMessageFilter> в конечной точке, чтобы запросить контент сообщения SOAP, а затем предпринять соответствующее действие на основании результатов запроса. Процесс организации очереди, например, может использовать запрос XPath для проверки приоритета заданного заголовка, чтобы определить, требуется ли переместить сообщение вперед по очереди.  
  
## <a name="filter-tables"></a>Таблицы фильтров  
 Таблицы фильтров используются для хранения пар "ключ-значение", где фильтр - это ключ, а связанные с ним данные - значение. Данные фильтра могут использоваться для указания действий, предпринимаемых, если фильтр в таблице соответствует сообщению, а тип данных фильтра является универсальным параметром для класса таблицы фильтров. Данные фильтра могут включать правила маршрутизации, состояние безопасности сеанса, прослушиватели канала и т. д. Эти данные можно использовать, если необходимо управление потоком данных.  
  
 Таблицы фильтров реализуют универсальный интерфейс <xref:System.ServiceModel.Dispatcher.IMessageFilterTable%601>.  
  
 В таблице фильтров предусмотрено несколько методов сопоставления сообщения и всех фильтров в таблице, которые возвращают неупорядоченную коллекцию фильтров или данных, удовлетворяющих условию. Некоторые их таких методов поиска совпадений ориентированы на множество совпадений и возвращают все соответствующие элементы. Другие методы ориентированы на одно совпадение, возвращают только один элемент и вызывают исключение <xref:System.ServiceModel.Dispatcher.MultipleFilterMatchesException>, если сообщению соответствует несколько фильтров.  
  
### <a name="message-filter-table"></a>Таблица фильтров сообщений  
 Таблица фильтров сообщений <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601> - это наиболее общая реализация класса <xref:System.ServiceModel.Dispatcher.IMessageFilterTable%601>. В таблице можно хранить фильтры всех типов.  
  
 Фильтрам можно задать числовые свойства, т. е. фильтр с наибольшим номером будет иметь самый высокий приоритет. Несколько типов фильтров могут иметь одинаковый приоритет. Определенный тип фильтра может встречаться на нескольких уровнях приоритета.  
  
 Сопоставление выполняется, начиная с фильтра с самым высоким приоритетом, и если фильтр с определенным приоритетом удовлетворяет условию, проверка фильтров меньшего приоритета не выполняется. Следовательно, если при использовании метода сопоставления по одному фильтру сообщению соответствует несколько фильтров и у каждого из них различные приоритеты, исключения не вызываются, и возвращается фильтр с самым высоким приоритетом. Аналогично, метод сопоставления по нескольким фильтрам возвращает только удовлетворяющие условию фильтры высшего приоритета.  
  
### <a name="xpath-message-filter-table"></a>Таблица фильтров сообщений XPath  
 Таблица <xref:System.ServiceModel.Dispatcher.XPathMessageFilterTable%601> оптимизирована для декларативных фильтров XPath, поэтому ключом таблицы является <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>.  
  
 Класс <xref:System.ServiceModel.Dispatcher.XPathMessageFilterTable%601> оптимизирует сопоставление для подмножества XPath, которое покрывает большую часть сценариев обмена сообщениями и поддерживает полную грамматику XPath 1.0. Он содержит оптимизированные алгоритмы эффективного параллельного сопоставления.  
  
 В данной таблице содержится несколько специализированных методов `Match`, работающих с объектами <xref:System.Xml.XPath.XPathNavigator> и <xref:System.ServiceModel.Dispatcher.SeekableXPathNavigator>. Класс <xref:System.ServiceModel.Dispatcher.SeekableXPathNavigator> расширяет класс <xref:System.Xml.XPath.XPathNavigator>, добавляя свойства <xref:System.ServiceModel.Dispatcher.SeekableXPathNavigator.CurrentPosition%2A>. Данное свойство позволяет быстро сохранить и загрузить позиции документа XML без клонирования навигатора и дорогостоящего выделения памяти, необходимого объекту <xref:System.Xml.XPath.XPathNavigator> для выполнения данной операции. Механизм XPath [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] постоянно фиксирует позицию курсора во время выполнения запросов в документах XML, поэтому объект <xref:System.ServiceModel.Dispatcher.SeekableXPathNavigator> обеспечивает важную оптимизацию процесса обработки сообщений.  
  
## <a name="customer-scenarios"></a>Пользовательские сценарии  
 Фильтрацию можно использовать при каждой отправке сообщения в разные модули обработки в зависимости от данных, содержащихся в сообщении. Два типичных сценария, маршрутизирующих сообщение на основании его кода действия и демультиплексирующих поток сообщений на основании адреса конечной точки сообщений.  
  
### <a name="routing"></a>Маршрутизация  
 Прослушиватель конечной точки прослушивает сообщения с одним или несколькими кодами действий в заголовке SOAP сообщения. Это реализуется путем создания объекта <xref:System.ServiceModel.Dispatcher.ActionMessageFilter> и передачи массива, содержащего коды действий, его конструктору. Он использует такой фильтр для регистрации в `ListenerFactory`, поэтому только сообщения, действие которых соответствует одному из действий, указанных в фильтре, поступают в определенную конечную точку.  
  
### <a name="de-multiplexing"></a>Демультиплексирование  
 Если несколько конечных точек получают сообщения от одного `ServiceListener` сети, единственным способом демультиплексировать сообщения и узнать, принадлежат ли они определенному адресу конечной точки, является использование объектов <xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter>, которые фильтруют сообщения по зарегистрированным конечным точкам, выполняя поиск в информации, хранящейся в заголовках. Только сообщения, прошедшие эти фильтры, имеют все необходимые заголовки, соответствующие:  
  
-   универсальному коду ресурса (URI) в `EndpointAddress` и  
  
-   остальным параметрам конечной точки в `EndpointAddress`, как указано в объекте <xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter>.  
  
## <a name="see-also"></a>См. также  
 [Передача данных и сериализация](../../../../docs/framework/wcf/feature-details/data-transfer-and-serialization.md)
