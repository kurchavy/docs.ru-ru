---
title: "Как создать службу маркеров безопасности | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "федерация"
  - "WCF, федерация"
ms.assetid: 98e82101-4cff-4bb8-a220-f7abed3556e5
caps.latest.revision: 12
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 12
---
# Как создать службу маркеров безопасности
Служба маркеров безопасности реализует протокол, определенный в спецификации WS\-Trust.Данный протокол определяет форматы сообщения и шаблоны обмена сообщениями для выпуска, обновления, отмены и проверки маркеров безопасности.Данная служба маркеров безопасности дает одну или несколько из данных возможностей.В данном разделе рассматривается наиболее общий сценарий: реализация выпуска маркера.  
  
## Выпуск маркеров  
 WS\-Trust определяет форматы сообщения на основе элемента схемы `RequestSecurityToken` языка определения схемы XML \(XSD\) и элемента схемы XSD `RequestSecurityTokenResponse` для выпуска маркера.Кроме того, WS\-Trust определяет связанные универсальные коды ресурса \(URI\).Универсальным кодом ресурса \(URI\) действия, связанным с сообщением `RequestSecurityToken`, является http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/trust\/RST\/Issue.Универсальным кодом ресурса действия, связанным с сообщением `RequestSecurityTokenResponse` является http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/trust\/RSTR\/Issue.  
  
### Структура сообщения с запросом  
 Структура сообщения с запросом на выпуск обычно состоит из следующих элементов.  
  
-   Тип запроса универсального кода ресурса \(URI\) со значением http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/trust\/Issue.  
  
-   Универсальный код ресурса \(URI\) типа маркера.Для маркеров языка SAML 1.1 значением данного универсального кода ресурса \(URI\) является http:\/\/docs.oasis\-open.org\/wss\/oasis\-wss\-saml\-token\-profile\-1.1\#SAMLV1.1.  
  
-   Значение размера ключа, указывающее количество битов в ключе, связанное с выпущенным маркером.  
  
-   Универсальный код ресурса \(URI\) типа ключа.Для симметричных ключей значением данного универсального кода ресурсов \(URI\) является http:\/\/schemas.xmlsoap.org\/ws\/2005\/02\/trust\/SymmetricKey.  
  
 Кроме того, может присутствовать несколько других элементов.  
  
-   Материал ключа, предоставленный клиентом.  
  
-   Информация об области, показывающая целевую службу, с которой будут использоваться выпущенные маркеры.  
  
 При создании ответного сообщения о выпуске служба маркеров безопасности использует информацию письма с запросом на выпуск.  
  
## Структура ответного сообщения  
 Структура ответного сообщения о выпуске обычно состоит из следующих элементов.  
  
-   Выданный маркер безопасности, например, проверочное утверждение SAML 1.1.  
  
-   Маркер проверки, связанный с маркером безопасности.Для симметричных ключей такой маркер часто является зашифрованной формой материала ключа.  
  
-   Ссылки на выпущенный маркер безопасности.Обычно служба маркеров безопасности возвращает ссылку, которая может быть использована при появлении выданного маркера в последующем сообщении, отправленном клиентом, и другую ссылку, которая может быть использована, если маркер не присутствует в последующих сообщениях.  
  
 Кроме того, может присутствовать несколько других элементов.  
  
-   Материал ключа, предоставленный службой маркеров безопасности.  
  
-   Алгоритм, необходимый для расчета общего ключа.  
  
-   Сведения о времени существования выпущенного маркера.  
  
## Сообщения с запросом на обработку  
 Служба маркеров безопасности обрабатывает запросы на выпуск, анализируя различные фрагменты сообщения с запросом и проверяя возможность выпуска маркера, соответствующего запросу.Перед созданием выпускаемого маркера служба маркеров безопасности должна определить следующее.  
  
-   Действительно ли запрос является запросом на выпуск маркера.  
  
-   Поддерживает ли служба маркеров безопасности запрошенный тип маркера.  
  
-   Авторизован ли автор заявки на подачу заявки.  
  
-   Может ли служба маркеров безопасности оправдать ожидания автора заявки, относящиеся к материалу ключа.  
  
 Две ответственные части создания маркера определяют, каким ключом подписать маркер и при помощи какого ключа зашифровать общий ключ.Ключ должен быть подписан так, чтобы при предоставлении клиентом ключа целевой службе данная служба могла определить, что маркер был выпущен службой безопасности ключей, которой она доверяет.Материал ключа должен быть зашифрован так, чтобы целевая служба могла расшифровать данный материал ключа.  
  
 Подписывание утверждения SAML включает создание экземпляра <xref:System.IdentityModel.Tokens.SigningCredentials>.Конструктор для данного класса принимает следующее  
  
-   <xref:System.IdentityModel.Tokens.SecurityKey> для ключа, который будет использоваться при подписывании утверждения SAML.  
  
-   Строка, определяющая используемый алгоритм подписывания.  
  
-   Строка, определяющая используемый алгоритм дайджест\-проверки.  
  
-   Дополнительно можно указать <xref:System.IdentityModel.Tokens.SecurityKeyIdentifier>, определяющий используемый для подписывания утверждения ключ.  
  
 [!code-csharp[c_CreateSTS#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#1)]
 [!code-vb[c_CreateSTS#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#1)]  
  
 Шифрование общего ключа предполагает принятие материала ключа и его шифрование при помощи ключа, который целевая служба сможет использовать для расшифровки общего ключа.Обычно используется открытый ключ целевой службы.  
  
 [!code-csharp[c_CreateSTS#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#2)]
 [!code-vb[c_CreateSTS#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#2)]  
  
 Кроме того, для зашифрованного ключа необходим идентификатор <xref:System.IdentityModel.Tokens.SecurityKeyIdentifier>.  
  
 [!code-csharp[c_CreateSTS#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#3)]
 [!code-vb[c_CreateSTS#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#3)]  
  
 Затем идентификатор <xref:System.IdentityModel.Tokens.SecurityKeyIdentifier> используется для создания `SamlSubject` как части `SamlToken`.  
  
 [!code-csharp[c_CreateSTS#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#4)]
 [!code-vb[c_CreateSTS#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#4)]  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Образец федерации](../../../../docs/framework/wcf/samples/federation-sample.md).  
  
## Создание ответных сообщений  
 После обработки службой маркеров безопасности запроса на выпуск и создания для выпуска маркера и ключа проверки должно быть создано ответное сообщение, включающее, по крайней мере, запрошенный маркер, маркер проверки и ссылки выпущенного маркера.Выпущенный маркер обычно является маркером <xref:System.IdentityModel.Tokens.SamlSecurityToken>, созданным из <xref:System.IdentityModel.Tokens.SamlAssertion>, как показано в следующем примере.  
  
 [!code-csharp[c_CreateSTS#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#5)]
 [!code-vb[c_CreateSTS#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#5)]  
  
 В случае, когда служба маркеров безопасности предоставляет материал общего ключа, маркер проверки создается путем создания <xref:System.ServiceModel.Security.Tokens.BinarySecretSecurityToken>.  
  
 [!code-csharp[c_CreateSTS#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#6)]
 [!code-vb[c_CreateSTS#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#6)]  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] том, как создавать маркер проверки, когда и служба клиента, и служба маркеров безопасности предоставляют материал ключа для общего ключа, см. [Образец федерации](../../../../docs/framework/wcf/samples/federation-sample.md).  
  
 Ссылки выпущенного ключа создаются путем создания экземпляров класса <xref:System.IdentityModel.Tokens.SecurityKeyIdentifierClause>.  
  
 [!code-csharp[c_CreateSTS#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_creatests/cs/source.cs#7)]
 [!code-vb[c_CreateSTS#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_creatests/vb/source.vb#7)]  
  
 После этого различные значения сериализуются в ответное сообщение, возвращаемое клиенту.  
  
## Пример  
 Полный код для службы маркеров безопасности см. в [Образец федерации](../../../../docs/framework/wcf/samples/federation-sample.md).  
  
## См. также  
 <xref:System.IdentityModel.Tokens.SigningCredentials>   
 <xref:System.IdentityModel.Tokens.SecurityKey>   
 <xref:System.IdentityModel.Tokens.SecurityKeyIdentifier>   
 <xref:System.IdentityModel.Tokens.SamlSecurityToken>   
 <xref:System.IdentityModel.Tokens.SamlAssertion>   
 <xref:System.ServiceModel.Security.Tokens.BinarySecretSecurityToken>   
 <xref:System.IdentityModel.Tokens.SecurityKeyIdentifierClause>   
 [Образец федерации](../../../../docs/framework/wcf/samples/federation-sample.md)