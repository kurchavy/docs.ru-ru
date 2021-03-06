---
title: "Асинхронная модель на основе событий (EAP)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- asynchronous calls
- asynchronous programming, design patterns
- asynchronous programming
ms.assetid: c6baed9f-2a25-4728-9a9a-53b7b14840cf
caps.latest.revision: "20"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.openlocfilehash: 0b5f242b9586c4ea3b045daf8f10b84127b81085
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="event-based-asynchronous-pattern-eap"></a>Асинхронная модель на основе событий (EAP)
Существует несколько способов предоставить асинхронные возможности клиентскому коду. Асинхронная модель на основе событий задает для классов рекомендуемый способ работы в асинхронном режиме.  
  
> [!NOTE]
>  Начиная с [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)], библиотека параллельных задач предоставляет новую модель для асинхронного и параллельного программирования. Дополнительные сведения см. в разделе [Параллельное программирование](../../../docs/standard/parallel-programming/index.md).  
  
## <a name="in-this-section"></a>Содержание  
 [Обзор асинхронной модели, основанной на событиях](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md)  
 Описывает, как асинхронная модель на основе событий позволяет использовать преимущества многопоточных приложений и устраняет многие сложности, присущие многопоточности.  
  
 [Реализация асинхронной модели, основанной на событиях](../../../docs/standard/asynchronous-programming-patterns/implementing-the-event-based-asynchronous-pattern.md)  
 Описывает стандартизированный способ упаковки класса, имеющего асинхронные возможности.  
  
 [Рекомендации по реализации асинхронной модели, основанной на событиях](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)  
 Описывает требования для предоставления асинхронных возможностей в соответствии с асинхронной моделью на основе событий.  
  
 [Определение, когда следует реализовать асинхронную модель, основанную на событиях](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)  
 Описывает, в каких случаях следует реализовать асинхронную модель на основе событий вместо шаблона <xref:System.IAsyncResult>.  
  
 [Пошаговое руководство. Реализация компонента, поддерживающего асинхронную модель, основанную на событиях](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)  
 Демонстрирует, как создать компонент, реализующий асинхронную модель на основе событий. Она реализуется с использованием вспомогательных классов из пространства имен <xref:System.ComponentModel?displayProperty=nameWithType>, что обеспечивает правильную работу компонента при любой модели приложения.  
  
 [Практическое руководство. Использование компонентов, поддерживающих асинхронную модель, основанную на событиях](../../../docs/standard/asynchronous-programming-patterns/how-to-use-components-that-support-the-event-based-asynchronous-pattern.md)  
 Описывает использование компонента, поддерживающего асинхронную модель на основе событий.  
  
## <a name="reference"></a>Ссылка  
 <xref:System.ComponentModel.AsyncOperation>  
 Описывает класс <xref:System.ComponentModel.AsyncOperation> и содержит ссылки на все его члены.  
  
 <xref:System.ComponentModel.AsyncOperationManager>  
 Описывает класс <xref:System.ComponentModel.AsyncOperationManager> и содержит ссылки на все его члены.  
  
 <xref:System.ComponentModel.BackgroundWorker>  
 Описывает компонент <xref:System.ComponentModel.BackgroundWorker> и содержит ссылки на все его члены.  
  
## <a name="related-sections"></a>Связанные разделы  
 [Библиотека параллельных задач (TPL)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)  
 Описание модели программирования для асинхронных и параллельных операций.  
  
 [Работа с потоками](../../../docs/standard/threading/index.md)  
 Описание многопоточных функциональных возможностей платформы .NET Framework.  
  
 [Работа с потоками](http://msdn.microsoft.com/library/552f6c68-dbdb-4327-ae36-32cf9063d88c)  
 Описание возможностей многопоточности языков C# и Visual Basic.  
  
## <a name="see-also"></a>См. также  
 [Рекомендации по работе с потоками](../../../docs/standard/threading/managed-threading-best-practices.md)  
 [События](../../../docs/standard/events/index.md)  
 [Многопоточность в компонентах](http://msdn.microsoft.com/library/2fc31e68-fb71-4544-b654-0ce720478779)  
 [Шаблоны асинхронного программирования](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)
