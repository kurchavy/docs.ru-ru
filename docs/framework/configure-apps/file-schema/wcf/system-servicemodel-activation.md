---
title: '&lt;system.serviceModel.activation&gt;'
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c0cae85f-56cb-4030-8807-6f96edff8d2d
caps.latest.revision: "9"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: ae6fb19fe956d819337c7c06a0c5b58ac70c8327
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="ltsystemservicemodelactivationgt"></a>&lt;system.serviceModel.activation&gt;
В данном разделе конфигурации представлены параметры конфигурации для средства SMSvcHost.exe. Элементы конфигурации можно задать в файле SMSvcHost.exe.config. В частности в нем содержатся все параметры компьютера, которые необходимо настроить.  
  
## <a name="sample-configuration-file"></a>Образец файла конфигурации  
 Далее приведен образец файла конфигурации (SMSvcHost.exe.config), используемый процессом прослушивателя SMSvcHost.exe.  
  
```xml  
<configuration>  
   <runtime>  
      <gcConcurrent enabled="false" />  
   </runtime>  
   <system.serviceModel.activation>  
       <net.tcp listenBacklog="10"  
          maxPendingAccepts="2"  
          maxPendingConnections="100"  
          receiveTimeout="00:00:10"  
          teredoEnabled="false">  
          <allowAccounts>  
             <!-- LocalSystem account -->  
             <add securityIdentifier="S-1-5-18"/>  
             <!-- LocalService account -->  
             <add securityIdentifier="S-1-5-19"/>  
             <!-- Network Service account -->  
            <add securityIdentifier="S-1-5-20"/>   
             <!-- Administrators account -->  
            <add securityIdentifier="S-1-5-32-544" />   
             <!-- IIS_IUSRS account (Vista only) -->  
             <add securityIdentifier="S-1-5-32-568"/>  
           </allowAccounts>  
       </net.tcp>  
       <net.pipe maxConnectionsPendingDispatch="100"  
          maxPendingAccepts="2"  
          receiveTimeout="00:00:10">  
          <allowAccounts>  
             <!-- LocalSystem account -->  
             <add securityIdentifier="S-1-5-18"/>  
             <!-- LocalService account -->  
             <add securityIdentifier="S-1-5-19"/>  
             <!-- Network Service account -->  
            <add securityIdentifier="S-1-5-20"/>   
             <!-- Administrators account -->  
            <add securityIdentifier="S-1-5-32-544" />   
             <!-- IIS_IUSRS account (Vista only) -->  
             <add securityIdentifier="S-1-5-32-568"/>  
           </allowAccounts>  
       </net.pipe>  
       <diagnostics performanceCountersEnabled="true" />  
   </system.serviceModel.activation>  
</configuration>  
```  
  
## <a name="see-also"></a>См. также  
 <xref:System.ServiceModel.Activation.Configuration>
