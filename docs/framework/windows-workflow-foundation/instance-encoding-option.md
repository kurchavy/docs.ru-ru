---
title: "Параметр кодировки экземпляров"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 89e4b029-4f68-438c-8117-9b21fe094ef4
caps.latest.revision: "7"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: a7664eecb68ff9aec0f5e3e31aa08058700f0e92
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="instance-encoding-option"></a>Параметр кодировки экземпляров
**Instance Encoding Option** свойство хранилища экземпляров рабочих процессов SQL позволяет указать, должен ли поставщик сохраняемости SQL сжимать сведения о состоянии экземпляра рабочего процесса с применением алгоритма GZip перед сохранением сведения в базе данных сохраняемости. Допустимы значения этого свойства GZip и None. По умолчанию используется значение None. Эти варианты описаны в следующем списке.  
  
1.  **GZip**. Поставщик сохраняемости кодирует сведения о состоянии с использованием алгоритма сжатия GZip перед их сохранением в базе данных сохраняемости.  
  
2.  **Нет**. Поставщик сохраняемости не сжимает сведения о состоянии перед их сохранением в базе данных сохраняемости.  
  
 При кодировании и сжатии сведений о состоянии экземпляра рабочего процесса с использованием экземпляра GZip снижается потребление памяти базой данных SQL, а также снижается нагрузка на сеть (в случае если база данных расположена на другом компьютере в сети, а не на компьютере, на котором запущена служба рабочего процесса). Общие рекомендации заключается в задании **Instance Encoding Option** свойства **нет** при небольших состояние экземпляра рабочего процесса.
