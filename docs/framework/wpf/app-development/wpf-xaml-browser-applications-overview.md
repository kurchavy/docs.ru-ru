---
title: "Общие сведения о приложениях браузера WPF XAML"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-wpf
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- csharp
- vb
helpviewer_keywords:
- XBAP [WPF], XAML browser application
- WPF XAML browser applications (XBAP)
- XAML browser applications (XBAP)
- browser-hosted applications [WPF]
ms.assetid: 3a7a86a8-75d5-4898-96b9-73da151e5e16
caps.latest.revision: "47"
author: dotnet-bot
ms.author: dotnetcontent
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 0f4f410f0f6c209dbc43642a15ae85a788390f4a
ms.sourcegitcommit: c0dd436f6f8f44dc80dc43b07f6841a00b74b23f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/19/2018
---
# <a name="wpf-xaml-browser-applications-overview"></a>Общие сведения о приложениях браузера WPF XAML
<a name="introduction"></a>
[!INCLUDE[TLA#tla_xbap#plural](../../../../includes/tlasharptla-xbapsharpplural-md.md)]объединяет возможности веб-приложений и многофункциональных клиентских приложений. Как веб-приложения, XBAP можно развертывать на веб-сервере и запускать из Internet Explorer или Firefox. Как многофункциональные клиентские приложения, XBAP могут использовать все возможности [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)]. Кроме того, XBAP разрабатываются аналогично многофункциональным клиентским приложениям. Этот раздел содержит простое, общее введение в разработку XBAP и показывает, чем она отличается от разработки стандартных многофункциональных клиентов.  
  
 В этом разделе содержатся следующие подразделы.  
  
-   [Создание приложения обозревателя XAML (XBAP)](#creating_a_new_xaml_browser_application_xbap)  
  
-   [Развертывание XBAP](#deploying_a_xbap)  
  
-   [Связь с веб-страницей размещения](#communicating_with_the_host_web_page)  
  
-   [Вопросы безопасности XBAP](#xbap_security_considerations)  
  
-   [Влияние времени запуска XBAP на производительность](#xbap_start_time_performance_considerations)  
  
<a name="creating_a_new_xaml_browser_application_xbap"></a>   
## <a name="creating-a-new-xaml-browser-application-xbap"></a>Создание приложения обозревателя XAML (XBAP)  
 Проще всего создать проект XBAP с помощью [!INCLUDE[vs_dev10_ext](../../../../includes/vs-dev10-ext-md.md)]. При создании нового проекта выберите из списка шаблонов **приложение браузера WPF**. Дополнительные сведения см. в разделе [Практическое руководство. Создание нового проекта приложения обозревателя WPF](http://msdn.microsoft.com/library/72ef4d90-e163-42a1-8df0-ea7ccfd1901f).  
  
 При запуске проект XBAP откроется в окне браузера, а не в отдельном окне. При отладке XBAP в [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] приложение выполняется с разрешениями зоны Интернета и в случае, если эти разрешения будут превышены, выдает исключения безопасности. Дополнительные сведения см. в разделах [Безопасность](../../../../docs/framework/wpf/security-wpf.md) и [Безопасность частичного доверия в WPF](../../../../docs/framework/wpf/wpf-partial-trust-security.md).  
  
> [!NOTE]
>  Если вы не используете [!INCLUDE[TLA#tla_visualstu](../../../../includes/tlasharptla-visualstu-md.md)] при разработке или хотите изучить файлы проекта более подробно, см. раздел [Построение приложения WPF](../../../../docs/framework/wpf/app-development/building-a-wpf-application-wpf.md).  
  
<a name="deploying_a_xbap"></a>   
## <a name="deploying-an-xbap"></a>Развертывание XBAP  
 При построении XBAP создаются следующие три файла:  
  
|Файл|Описание:|  
|----------|-----------------|  
|Исполняемый файл (.EXE)|Содержит скомпилированный код и имеет расширение EXE.|  
|Манифест приложения (.MANIFEST)|Содержит метаданные, связанные с приложением, и имеет расширение MANIFEST.|  
|Манифест развертывания (.XBAP)|Содержит сведения, которые [!INCLUDE[TLA#tla_clickonce](../../../../includes/tlasharptla-clickonce-md.md)] использует для развертывания приложения, и имеет расширение XBAP.|  
  
 XBAP развертывается на веб-сервере, например [!INCLUDE[TLA#tla_iis50](../../../../includes/tlasharptla-iis50-md.md)] или более поздней версии. Устанавливать [!INCLUDE[TLA2#tla_winfx](../../../../includes/tla2sharptla-winfx-md.md)] на веб-сервер необязательно, но нужно зарегистрировать типы [!INCLUDE[TLA2#tla_wpf](../../../../includes/tla2sharptla-wpf-md.md)] [!INCLUDE[TLA#tla_mime](../../../../includes/tlasharptla-mime-md.md)] и расширения имен файлов. Дополнительные сведения см. в разделе [Практическое руководство. Настройка служб IIS 5.0 и IIS 6.0 для развертывания приложений WPF](../../../../docs/framework/wpf/app-development/how-to-configure-iis-5-0-and-iis-6-0-to-deploy-wpf-applications.md).  
  
 Чтобы подготовить XBAP для развертывания, скопируйте файл EXE и связанные с ним манифесты на веб-сервер. Создайте HTML-страницу, содержащую гиперссылку, чтобы открыть манифест развертывания, который является файлом с расширением XBAP. Когда пользователь щелкает ссылку на файл XBAP, [!INCLUDE[TLA2#tla_clickonce](../../../../includes/tla2sharptla-clickonce-md.md)] автоматически обрабатывает механизм загрузки и запуска приложения. В следующем примере кода показана HTML-страница, которая содержит гиперссылку, указывающую на XBAP.  
  
```html
<html>   
    <head></head>  
    <body>   
        <a href="XbapEx.xbap">Click this link to launch the application</a>  
    </body>   
</html>  
```  
  
 Кроме того, XBAP можно разместить во фрейме веб-страницы. Создайте веб-страницу с одним или несколькими фреймами. Назначьте исходное свойство фрейма файлу манифеста развертывания. Чтобы использовать встроенный механизм взаимодействия между веб-страницей размещения и XBAP, необходимо разместить приложение во фрейме. В следующем примере кода показана HTML-страница с двумя фреймами; в качестве источника для второго фрейма выбран XBAP.  
  
```html
<html>   
    <head>
        <title>A page with frames</title>
    </head>  
    <frameset cols="50%,50%">   
        <frame src="introduction.htm">   
        <frame src="XbapEx.xbap">   
    </frameset>   
</html>  
```  
  
### <a name="clearing-cached-xbaps"></a>Очистка кэшированных XBAP  
 В некоторых случаях после повторной сборки и запуска XBAP может оказаться, что открывается более ранняя версия XBAP. Это может произойти, например, если номер версии сборки XBAP статичен и XBAP запускается из командной строки. В этом случае в связи с тем, что номер кэшированной версии (версии, запущенной ранее) и новой версии остаются прежними, новая версия XBAP не загружается. Вместе нее загружается кэшированная версия.  
  
 В подобном случае можно удалить кэшированную версию с помощью команды **Mage** (устанавливается вместе с Visual Studio или [!INCLUDE[TLA2#tla_lhsdk](../../../../includes/tla2sharptla-lhsdk-md.md)]) в командной строке. Следующая команда очищает кэш приложения.  
  
 ```console
 Mage.exe -cc
 ```
  
 Она обеспечивает запуск последней версии XBAP. При отладке приложения в [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)] должна запускаться последняя версия XBAP. Как правило, номер версии развертывания необходимо обновлять при каждой сборке. Дополнительные сведения о команде Mage см. в разделе [Mage.exe (средство создания и редактирования манифеста)](../../../../docs/framework/tools/mage-exe-manifest-generation-and-editing-tool.md).  
  
<a name="communicating_with_the_host_web_page"></a>   
## <a name="communicating-with-the-host-web-page"></a>Связь с веб-страницей размещения  
 Если приложение находится во фрейме HTML, вы можете взаимодействовать с веб-страницей, которая содержит XBAP. Это делается путем получения <xref:System.Windows.Interop.BrowserInteropHelper.HostScript%2A> свойство <xref:System.Windows.Interop.BrowserInteropHelper>. Оно возвращает объект скрипта, представляющий окно HTML. Доступ к свойствам, методам и событиям можно получить в [объекте окна](http://go.microsoft.com/fwlink/?LinkId=160274), используя обычный синтаксис с точками. Также можно получить доступ к методам скрипта и глобальным переменным. В следующем примере показано, как извлечь объект скрипта и закрыть браузер.  
  
 [!code-csharp[XbapBrowserInterop#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/xbapbrowserinterop/cs/page1.xaml.cs#10)]
 [!code-vb[XbapBrowserInterop#10](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/xbapbrowserinterop/vb/page1.xaml.vb#10)]  
  
### <a name="debugging-xbaps-that-use-hostscript"></a>Отладка XBAP, в котором используется HostScript  
 Если XBAP использует <xref:System.Windows.Interop.BrowserInteropHelper.HostScript%2A> объекта для взаимодействия с окном HTML, имеется два параметра, которые нужно указать для запуска и отладки приложения в [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)]. Приложение должно иметь доступ к своему исходному сайту, а запустить его необходимо с HTML-страницы, которая содержит XBAP. Ниже описаны процедуры проверки двух этих параметров:  
  
1.  В Visual Studio откройте свойства проекта.  
  
2.  На вкладке **Безопасность** нажмите кнопку **Дополнительно**.  
  
     Откроется диалоговое окно "Дополнительные параметры безопасности".  
  
3.  Убедитесь, что флажок **Предоставить приложению доступ к своему исходному сайту** установлен, и нажмите кнопку **ОК**.  
  
4.  На вкладке **Отладка** выберите параметр **Запустить браузер, используя URL-адрес** и укажите URL-адрес HTML-страницы, содержащей XBAP.  
  
5.  В Internet Explorer нажмите кнопку **Сервис** и выберите **Свойства обозревателя**.  
  
     Откроется диалоговое окно «Свойства веб-обозревателя».  
  
6.  Откройте вкладку **Дополнительно** .  
  
7.  В списке **Параметры** в разделе **Безопасность** установите флажок **Разрешать запуск активного содержимого файлов на моем компьютере**.  
  
8.  Нажмите кнопку **ОК**.  
  
     Чтобы изменения вступили в силу, Internet Explorer необходимо перезапустить.  
  
> [!CAUTION]
>  Включение активного содержимого в Internet Explorer может подвергнуть компьютер риску. Дополнительные сведения см. в разделе [Средства безопасности и конфиденциальности в Internet Explorer](http://go.microsoft.com/fwlink/?LinkId=179286). Если вы не хотите изменять параметры безопасности Internet Explorer, запустите HTML-страницу с сервера и присоедините к процессу отладчик [!INCLUDE[TLA2#tla_visualstu](../../../../includes/tla2sharptla-visualstu-md.md)].  
  
<a name="xbap_security_considerations"></a>   
## <a name="xbap-security-considerations"></a>Вопросы безопасности XBAP  
 Обычно XBAP выполняются в изолированной среде безопасности частичного доверия, ограниченной набором разрешений зоны Интернета. В связи с этим ваша реализация должна поддерживать подмножество элементов [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)], которые поддерживаются в зоне Интернета; в противном случае разрешения приложения придется повысить. Дополнительные сведения см. в разделе [Безопасность](../../../../docs/framework/wpf/security-wpf.md).  
  
 При использовании <xref:System.Windows.Controls.WebBrowser> элемента управления в приложении WPF внутренним образом устанавливает собственный элемент управления WebBrowser ActiveX. Если ваше приложение — это XBAP частичного доверия, запущенный в браузере Internet Explorer, элемент управления ActiveX выполняется в выделенном потоке процесса Internet Explorer. В связи с этим применяются указанные ниже ограничения.  
  
-   <xref:System.Windows.Controls.WebBrowser> Элемент управления должен обеспечивать поведение, аналогичное браузеру узла, включая ограничения безопасности. Некоторыми из этих ограничений безопасности можно управлять с помощью параметров безопасности Internet Explorer. Дополнительные сведения см. в разделе [Безопасность](../../../../docs/framework/wpf/security-wpf.md).  
  
-   Если XBAP загружается на HTML-странице в междоменном режиме, возникнет исключение.  
  
-   Входные данные — в потоке, отдельном от WPF <xref:System.Windows.Controls.WebBrowser>, поэтому не может быть перехвачено ввод с клавиатуры и состояние IME не является общей.  
  
-   Время или порядок навигации могут отличаться, если элемент управления ActiveX выполняется в другом потоке. Например, переход на какую-либо страницу не всегда отменяется при запуске другого запроса навигации.  
  
-   Настраиваемый элемент управления ActiveX может испытывать проблемы со связью, поскольку приложение WPF выполняется в отдельном потоке.  
  
-   <xref:System.Windows.Interop.HwndHost.MessageHook>не возникает, поскольку <xref:System.Windows.Interop.HwndHost> невозможно определить подкласс окно работает в другой поток или процесс.  
  
### <a name="creating-a-full-trust-xbap"></a>Создание XBAP с полным доверием  
 Если XBAP требует полного доверия, проект можно изменить, предоставив ему соответствующее разрешение. Чтобы предоставить полное доверие, необходимо выполнить указанные ниже действия.  
  
1.  В Visual Studio откройте свойства проекта.  
  
2.  На вкладке **Безопасность** выберите параметр **Это приложение с полным доверием**.  
  
 При этом происходят следующие изменения:  
  
-   В файле проекта значение элемента `<TargetZone>` изменяется на `Custom`.  
  
-   В манифесте приложения (app.manifest) к элементу `PermissionSet` добавляется атрибут `Unrestricted="true"`.  
  
    ```xml
    <PermissionSet class="System.Security.PermissionSet"   
                   version="1"   
                   ID="Custom"   
                   SameSite="site"   
                   Unrestricted="true" />  
    ```  
  
### <a name="deploying-a-full-trust-xbap"></a>Развертывание XBAP с полным доверием  
 При развертывании XBAP с полным доверием, не основанного на модели доверенного развертывания ClickOnce, действия, выполняемые после того, как пользователь запустит приложение, зависят от зоны безопасности. В некоторых случаях пользователь получит предупреждение при попытке установить приложение. Пользователь может выбрать продолжение или отмену установки. В следующей таблице описаны поведение приложения для каждой зоны безопасности и действия, необходимые для получения приложением полного доверия.  
  
|Зона безопасности|Поведение|Получение полного доверия|  
|-------------------|--------------|------------------------|  
|Локальный компьютер|Автоматическое получение полного доверия|Никаких действий не требуется.|  
|Интрасеть и надежные веб-сайты|Запрос полного доверия|Подпишите приложение XBAP с помощью сертификата, чтобы пользователь видел источник в запросе.|  
|Интернет|Сбой с сообщением "Доверие не оказано"|Подпишите приложение XBAP с помощью сертификата.|  
  
> [!NOTE]
>  Поведение, описанное в предыдущей таблице, относится к приложениям XBAP с полным доверием, не следующим модели доверенного развертывания ClickOnce.  
  
 Для развертывания XBAP с полным доверием рекомендуется использовать модель доверенного развертывания ClickOnce. Она позволяет XBAP получать полное доверие автоматически, независимо от зоны безопасности и не запрашивая подтверждение пользователя. При использовании этой модели приложение должно быть подписано сертификатом надежного издателя. Дополнительные сведения см. в разделах [Общие сведения о развертывании доверенных приложений](/visualstudio/deployment/trusted-application-deployment-overview) и [Знакомство с подписыванием кода](http://go.microsoft.com/fwlink/?LinkId=166327).  
  
<a name="xbap_start_time_performance_considerations"></a>   
## <a name="xbap-start-time-performance-considerations"></a>Влияние времени запуска XBAP на производительность  
 Важную роль в производительности XBAP играет время его запуска. Если XBAP является первым загружаемым приложением WPF, время *холодного запуска* может составить от десяти секунд. Это связано с тем, что страницу хода выполнения обрабатывает WPF, а для того, чтобы отображать приложение, требуется холодный запуск CLR и WPF.  
  
 Начиная с версии [!INCLUDE[net_v35SP1_short](../../../../includes/net-v35sp1-short-md.md)], время холодного запуска XBAP уменьшается за счет того, что неуправляемая страница хода выполнения отображается на более раннем этапе цикла развертывания. Она открывается практически сразу после того, как приложение будет запущено, поскольку отображается машинным кодом размещения и выводится на экран в формате HTML.  
  
 Кроме того, улучшенный параллелизм последовательности загрузки [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] сокращает время запуска почти на десять процентов. После того, как [!INCLUDE[ndptecclick](../../../../includes/ndptecclick-md.md)] загрузит и проверит манифесты, запускается загрузка приложения, а индикатор выполнения начинает обновляться.  
  
## <a name="see-also"></a>См. также  
 [Настройка Visual Studio для отладки приложений браузера XAML для вызова веб-службы](../../../../docs/framework/wpf/app-development/configure-vs-to-debug-a-xaml-browser-to-call-a-web-service.md)  
 [Развертывание приложений WPF](../../../../docs/framework/wpf/app-development/deploying-a-wpf-application-wpf.md)
