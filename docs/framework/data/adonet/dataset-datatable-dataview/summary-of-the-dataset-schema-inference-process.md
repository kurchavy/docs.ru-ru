---
title: "Общие сведения о процессе определения схемы набора данных"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fd0891c8-d068-4e30-a76f-7c375f078bf7
caps.latest.revision: "4"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 63ab866785f1fea66ed72fa17589a5be790fcdaa
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2018
---
# <a name="summary-of-the-dataset-schema-inference-process"></a>Общие сведения о процессе определения схемы набора данных
Процесс вывода схемы из XML-документа вначале определяет, какие элементы будут выведены как таблицы. Из оставшегося XML процесс вывода схемы определяет столбцы этих таблиц. Для вложенных таблиц процесс вывода формирует вложенные объекты <xref:System.Data.DataRelation> и <xref:System.Data.ForeignKeyConstraint>.  
  
 Далее представлена краткая сводка правил вывода.  
  
-   Элементы с атрибутами выводятся как таблицы.  
  
-   Элементы, имеющие дочерние элементы, выводятся как таблицы.  
  
-   Повторяющиеся элементы выводятся как одна таблица.  
  
-   Если элемент документа (корневой элемент) не имеет ни атрибутов, ни дочерних элементов, которые выводились бы как столбцы, он выводится как <xref:System.Data.DataSet>. В противном случае элемент документа выводится как таблица.  
  
-   Атрибуты выводятся как столбцы.  
  
-   Элементы, которые не повторяются и не имеют ни атрибутов, ни дочерних элементов, выводятся как столбцы.  
  
-   Для элементов, которые выводятся как таблицы, вложенные в другие элементы, которые также выводятся как таблицы, вложенный **DataRelation** создается между двумя таблицами. Новый столбец первичного ключа с именем **TableName_Id** добавляется к обеим таблицам и используемые **DataRelation**. Объект **ForeignKeyConstraint** создается между двумя таблицами с помощью **TableName_Id** столбца.  
  
-   Для элементов, которые выводятся как таблицы и содержит текст, но не имеют дочерних элементов, новый столбец с именем **TableName_Text** создается для каждого из элементов текста. Если элемент выводится как таблица и имеет текст, но при этом имеет дочерние элементы, текст пропускается.  
  
## <a name="see-also"></a>См. также  
 [Определение реляционной структуры DataSet из XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/inferring-dataset-relational-structure-from-xml.md)  
 [Загрузка DataSet из XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-a-dataset-from-xml.md)  
 [Загрузка сведений о схеме DataSet из XML](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/loading-dataset-schema-information-from-xml.md)  
 [Использование XML в наборах данных](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/using-xml-in-a-dataset.md)  
 [Наборы данных, таблицы данных и объекты DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 [Центр разработчиков наборов данных и управляемых поставщиков ADO.NET](http://go.microsoft.com/fwlink/?LinkId=217917)
