---
title: ActivityTransfer
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fc40ef17-2a92-4ce2-853c-6ba8e5d571f3
caps.latest.revision: "5"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 7f3db50a32fabc117c79eef5ac086a7798f86ed3
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="activitytransfer"></a>ActivityTransfer
Событие перенаправления действия  
  
## <a name="syntax"></a>Синтаксис  
  
```  
class ActivityTransfer : WSAT_TraceEvent  
{  
  object ActivityID;  
  object RelatedActivityID;  
};  
```  
  
## <a name="methods"></a>Методы  
 Класс ActivityTransfer не определяет никакие методы.  
  
## <a name="properties"></a>Свойства  
 Класс ActivityTransfer имеет следующие свойства.  
  
### <a name="activityid"></a>ActivityID  
  
-   Тип данных: объект  
    Тип доступа: только для чтения  
  
-   Идентификатор действия  
  
### <a name="relatedactivityid"></a>RelatedActivityID  
  
-   Тип данных: объект  
    Тип доступа: только для чтения  
  
-   Связанный идентификатор действия  
  
## <a name="requirements"></a>Требования  
  
|MOF|Объявлено в файле Servicemodel.mof.|  
|---------|-----------------------------------|  
|Пространство имен|Определено в root\ServiceModel.|
