---
title: "Параметр кодировки экземпляров | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 89e4b029-4f68-438c-8117-9b21fe094ef4
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Параметр кодировки экземпляров
Свойство **Instance Encoding Option** для хранилища экземпляров рабочего процесса SQL позволяет указать, должен ли поставщик сохраняемости SQL сжимать сведения о состоянии экземпляра рабочего процесса с применением алгоритма GZip перед сохранением данных в базе данных сохраняемости.Допустимы значения этого свойства GZip и None.По умолчанию используется значение None.Эти варианты описаны в следующем списке.  
  
1.  **GZip**.Поставщик сохраняемости кодирует сведения о состоянии с использованием алгоритма сжатия GZip перед их сохранением в базе данных сохраняемости.  
  
2.  **None**.Поставщик сохраняемости не сжимает сведения о состоянии перед их сохранением в базе данных сохраняемости.  
  
 При кодировании и сжатии сведений о состоянии экземпляра рабочего процесса с использованием экземпляра GZip снижается потребление памяти базой данных SQL, а также снижается нагрузка на сеть \(в случае если база данных расположена на другом компьютере в сети, а не на компьютере, на котором запущена служба рабочего процесса\).Как правило, рекомендуется задавать для свойства **Instance Encoding Option** значение **None**, если состояние экземпляра рабочего процесса имеет небольшой размер.