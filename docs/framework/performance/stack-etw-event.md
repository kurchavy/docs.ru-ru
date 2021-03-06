---
title: "События стека (трассировка событий Windows)"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stack event [.NET Framework]
- ETW, stack event (CLR)
ms.assetid: f612fa5b-4b62-4593-a19e-85c9b1018dce
caps.latest.revision: "5"
author: mairaw
ms.author: mairaw
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 1107c6608fe5136eb6159b1d4f0a438e95c4dabb
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="stack-etw-event"></a>События стека (трассировка событий Windows)
Событие стека должно использоваться вместе с другими событиями для создания трассировок стека после вызова события. Оно регистрируется при включенном поставщике среды выполнения. Это очень часто случающееся событие, так как оно сопровождает создание другого события времени выполнения. По этой причине рекомендуется использовать его с осторожностью.  
  
 В таблице ниже показаны ключевое слово и уровень. (Дополнительные сведения см. в разделе [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md).)  
  
|Ключевое слово для вызова события|Уровень|  
|-----------------------------------|-----------|  
|`StackKeyword` (0x40000000)|LogAlways(0)|  
  
 В таблице ниже представлены сведения о событии.  
  
|Событие|Идентификатор события|Условие вызова|  
|-----------|--------------|-----------------|  
|`CLRStackWalk`|82|Вместе с другими событиями для создания трассировок стека после этого события.|  
  
 В таблице ниже представлены данные события.  
  
|Имя поля|Тип данных|Описание|  
|----------------|---------------|-----------------|  
|ClrInstanceID|win:Uint16|Уникальный идентификатор среды выполнения.|  
|Reserved1|win:UInt8|Зарезервировано.|  
|Reserved2|win:UInt8|Зарезервировано.|  
|FrameCount|win:UInt32|Число кадров в трассировке стека.|  
|Стек|win:Pointer|Столбцы указателей инструкций.|  
  
## <a name="see-also"></a>См. также  
 [События трассировки событий Windows в среде CLR](../../../docs/framework/performance/clr-etw-events.md)
