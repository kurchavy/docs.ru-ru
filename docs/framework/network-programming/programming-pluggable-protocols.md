---
title: "программирование подключаемых протоколов"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- downloading Internet resources, pluggable protocols
- WebRequest class, pluggable protocols
- response to Internet request, pluggable protocols
- WebResponse class, pluggable protocols
- sending data, pluggable protocols
- network resources, pluggable protocols
- Internet, pluggable protocols
- programming pluggable protocols
- pluggable protocols, programming
- requesting data from Internet, pluggable protocols
- receiving data, pluggable protocols
- protocols, pluggable
ms.assetid: 66ef8456-7576-4e97-8956-959b216373db
caps.latest.revision: "12"
author: mcleblanc
ms.author: markl
manager: markl
ms.workload: dotnet
ms.openlocfilehash: c97b64c9e042706fedabac435b8982aed65a8be4
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="programming-pluggable-protocols"></a>программирование подключаемых протоколов
Абстрактные классы <xref:System.Net.WebRequest> и <xref:System.Net.WebResponse> реализуют основу для подключаемых протоколов. Создавая производные классы для определенных протоколов на основе классов <xref:System.Net.WebRequest> и <xref:System.Net.WebResponse>, приложение может запрашивать данные интернет-ресурса и считывать ответ, не указывая используемый протокол.  
  
 Прежде чем создавать класс <xref:System.Net.WebRequest> для определенного протокола, необходимо зарегистрировать его метод Create. Используйте статический метод <xref:System.Net.WebRequest.RegisterPrefix%28System.String%2CSystem.Net.IWebRequestCreate%29> класса <xref:System.Net.WebRequest> для регистрации потомка <xref:System.Net.WebRequest>, который будет обрабатывать набор запросов к конкретной интернет-схеме, к схеме и серверу либо к схеме, серверу и пути.  
  
 В большинстве случаев можно отправлять и получать данные с помощью методов и свойств класса <xref:System.Net.WebRequest>. Однако если нужно получить доступ к свойствам определенного протокола, можно выполнить приведение типа <xref:System.Net.WebRequest> к конкретному экземпляру производного класса.  
  
 Чтобы использовать преимущества подключаемых протоколов, потомки класса <xref:System.Net.WebRequest> должны предоставлять применяемую по умолчанию операцию "запрос-ответ", для которой не требуется задавать свойства определенного протокола. Например, класс <xref:System.Net.HttpWebRequest>, который реализует класс <xref:System.Net.WebRequest> для HTTP, предоставляет запрос `GET` по умолчанию и возвращает <xref:System.Net.HttpWebResponse>, который содержит поток, возвращенный веб-сервером.  
  
## <a name="see-also"></a>См. также  
 [Наследование от WebResponse](../../../docs/framework/network-programming/deriving-from-webrequest.md)  
 [Наследование от класса WebResponse](../../../docs/framework/network-programming/deriving-from-webresponse.md)  
 [Сетевое программирование в .NET Framework](../../../docs/framework/network-programming/index.md)  
 [Практическое руководство. Приведение типа объекта WebRequest для доступа к свойствам, связанным с определенным протоколом](../../../docs/framework/network-programming/how-to-typecast-a-webrequest-to-access-protocol-specific-properties.md)
