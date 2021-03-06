---
title: "Практическое руководство. Проверка подлинности с использованием имени и пароля пользователя"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: authentication [WCF], user name and password
ms.assetid: a5415be2-0ef3-464c-9f76-c255cb8165a4
caps.latest.revision: "18"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 1554e8594a611aa75876d14ee7ad0689932372e8
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2017
---
# <a name="how-to-authenticate-with-a-user-name-and-password"></a>Практическое руководство. Проверка подлинности с использованием имени и пароля пользователя
В этом разделе показано, как включить службу [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] для проверки подлинности клиента с помощью имени пользователя домена Windows и пароля. Предполагается, что это рабочая резидентная служба WCF. Пример создания основных резидентной WCF службы см. в разделе [учебник по началу работы](../../../../docs/framework/wcf/getting-started-tutorial.md). В этом разделе предполагается, что служба настраивается в коде. Если вы хотите проверить пример настройки аналогичную службу с помощью файла конфигурации см. раздел [имя пользователя безопасности сообщения](../../../../docs/framework/wcf/samples/message-security-user-name.md)  
  
 Чтобы настроить службу для проверки подлинности клиентов с помощью имени пользователя и пароля домена Windows, используйте <<!--zz xref:System.ServiceModel.WsHttpBinding --> `xref:System.ServiceModel.WsHttpBinding`> и задайте его `Security.Mode` свойства `Message`. Кроме того, необходимо указать сертификат X509, который будет использован для шифрования имени пользователя и пароля, так как они передаются от клиента к службе.  
  
 На стороне клиента необходимо запрашивать у пользователя учетные данные и указать учетные данные пользователя в клиентском классе-посреднике WCF.  
  
### <a name="to-configure-a-wcf-service-to-authenticate-using-windows-domain-username-and-password"></a>Чтобы настроить службу WCF для проверки подлинности, используйте имя пользователя и пароль в домене Windows.  
  
1.  Создайте экземпляр класса <<!--zz xref:System.ServiceModel.WsHttpBinding --> `xref:System.ServiceModel.WsHttpBinding`>, установите режим безопасности привязки, `SecurityMode.Message`, задайте `ClientCredentialType` привязки `MessageCredentialType.UserName`и добавить конечную точку службы с помощью заданной привязки к узлу службы, как показано в следующем коде:  
  
    ```  
    // ...  
    WSHttpBinding userNameBinding = new WSHttpBinding();  
    userNameBinding.Security.Mode = SecurityMode.Message;  
    userNameBinding.Security.Message.ClientCredentialType = MessageCredentialType.UserName;  
    svcHost.AddServiceEndpoint(typeof(IService1), userNameBinding, "");  
    // ...  
    ```  
  
2.  Задает сертификат сервера, используемый для шифрования имени пользователя и пароля, передаваемых по сети. Этот код должен непосредственно следовать за показанным выше кодом. В следующем примере используется сертификат, созданный с помощью файла setup.bat из [имя пользователя безопасности сообщения](../../../../docs/framework/wcf/samples/message-security-user-name.md) образца:  
  
    ```  
    // ...  
    svcHost.Credentials.ServiceCertificate.SetCertificate(StoreLocation.LocalMachine, StoreName.My, X509FindType.FindBySubjectName, "localhost");  
    // ...  
    ```  
  
     Вы можете использовать собственный сертификат, просто укажите ссылку на него в коде. Дополнительные сведения о создании и использовании сертификатов в разделе [работа с сертификатами](../../../../docs/framework/wcf/feature-details/working-with-certificates.md). Убедитесь, что сертификат находится в хранилище сертификатов «Доверенные лица» для локального компьютера. Это можно сделать, запустив mmc.exe и выбрав **файл**, **добавить или удалить оснастку...**  элемента меню. В **Добавление или удаление оснасток** диалогового окна выберите **оснастку сертификатов** и нажмите кнопку **добавить**. В диалоговом окне оснастки сертификатов выберите **учетная запись компьютера**. По умолчанию сертификат, сформированный из образца «Безопасность сообщений с использованием имени пользователя», будет находиться в папке «Личное или сертификаты».  Оно будет указано как «localhost» в разделе «выпущен» столбца в окне MMC. Перетаскивание сертификат в **доверенные лица** папки. Это позволит WCF считать сертификат доверенным при выполнении проверки подлинности.  
  
### <a name="to-call-the-service-passing-username-and-password"></a>Вызов службы с передачей имени пользователя и пароля  
  
1.  Клиентское приложение должно предложить пользователю ввести имя пользователя и пароль. Следующий код запрашивает у пользователя имя пользователя и пароль.  
  
    > [!WARNING]
    >  Этот код не следует использовать в рабочей среде, так как пароль во время ввода отображается на экране.  
  
    ```  
    public static void GetPassword(out string username, out string password)  
            {  
                Console.WriteLine("Provide a valid machine or domain account. [domain\\user]");  
                Console.WriteLine("   Enter username:");  
                username = Console.ReadLine();  
                Console.WriteLine("   Enter password:");  
                password = Console.ReadLine();             
                return;  
            }  
    ```  
  
2.  Создайте экземпляр клиентского класса-посредника, указав учетные данные клиента, как показано в следующем коде:  
  
    ```  
    string username;  
    string password;  
  
    // Instantiate the proxy  
    Service1Client proxy = new Service1Client();  
  
    // Prompt the user for username & password  
    GetPassword(out username, out password);  
  
    // Set the user’s credentials on the proxy  
    proxy.ClientCredentials.UserName.UserName = username;  
    proxy.ClientCredentials.UserName.Password = password;  
  
    // Treat the test certificate as trusted  
    proxy.ClientCredentials.ServiceCertificate.Authentication.CertificateValidationMode = System.ServiceModel.Security.X509CertificateValidationMode.PeerOrChainTrust;  
    // Call the service operation using the proxy  
    ```  
  
## <a name="see-also"></a>См. также  
 <<!--zz xref:System.ServiceModel.WsHttpBinding --> `xref:System.ServiceModel.WsHttpBinding`>  
 <xref:System.ServiceModel.WSHttpSecurity>  
 <xref:System.ServiceModel.SecurityMode>  
 <xref:System.ServiceModel.Security.UserNamePasswordClientCredential.UserName%2A>  
 <xref:System.ServiceModel.Security.UserNamePasswordClientCredential.Password%2A>  
 <xref:System.ServiceModel.Security.UserNamePasswordClientCredential>  
 <xref:System.ServiceModel.WSHttpSecurity.Mode%2A>  
 <xref:System.ServiceModel.HttpTransportSecurity.ClientCredentialType%2A>  
 [Безопасность транспорта с обычной проверкой подлинности](../../../../docs/framework/wcf/feature-details/transport-security-with-basic-authentication.md)  
 [Защита распределенных приложений](../../../../docs/framework/wcf/feature-details/distributed-application-security.md)  
 [\<wsHttpBinding >](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md)
