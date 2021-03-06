---
title: "Монолитные приложения"
description: "Жизненный цикл приложений контейнерного Docker с помощью платформы Майкрософт и средств"
keywords: "Docker, микрослужбы, ASP.NET, контейнер"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/22/2017
ms.openlocfilehash: b4b61198129c584909d1345b64dc52feeee7b58e
ms.sourcegitcommit: 4f3fef493080a43e70e951223894768d36ce430a
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/21/2017
---
# <a name="monolithic-applications"></a>Монолитные приложения

В этом сценарии вы построение одно- и монолитные веб-приложения или службы и развертывание его в качестве контейнера. В приложении структуру может оказаться монолитные; также может содержать несколько библиотек, компонентов или даже слои (уровня приложения, уровня домена, уровень доступа к данным, и т. д.). Извне это один контейнер, как единый процесс, одного веб-приложения или службы единого.

Для управления этой модели, развернуть один контейнер для представления приложения. Чтобы масштабировать его, необходимо просто добавьте несколько копий с балансировкой нагрузки на переднем плане. Простота поступает от управления одно развертывание в одном контейнере или виртуальной машины (VM).

Следующий основной сервер делает самое только в один контейнер и делает это в одном процессе объединенный шаблон находится в конфликте. Как показано на рисунке 4-1, может включать несколько компонентов и библиотек или внутренней уровней в каждом контейнере.

![](./media/image1.png)

Рис. 4-1: пример архитектуры монолитные приложения

Недостатком этого подхода поступает, если или при расширении приложения, требующие масштабирование. Если масштабировать приложение в целом, это не действительно проблемы. В большинстве случаев несколько частей приложения весьма стягиванием точки, которые требуется масштабирование, в то время как менее используются другими компонентами.

Используя пример типичных электронной коммерции, скорее всего, необходим для масштабирования сведения компонента продукта. Многие Дополнительные клиенты просматривать продукты, чем их приобретение. Дополнительные клиенты использовать свою корзину не использовать конвейер оплаты. Меньшее количество клиентов, добавить комментарии или Просмотр истории покупок. И, скорее всего имеется лишь небольшое число сотрудников в одной области, необходимые для управления содержимым и маркетинговых кампаний. По масштабирование монолитные конструкции, весь код разворачивается несколько раз.

В дополнение к «масштаб-все» проблему, изменений к одному компоненту требуется полное повторное тестирование всего приложения, а также завершить повторное развертывание всех экземпляров.

Объединенный подход часто, и во многих организациях разрабатываемом с помощью этого метода архитектуры. Многие предоставляются блага достаточное количество результатов, в то время как другие возникнуть ограничения. Многие открыт свои приложения в этой модели, так как средства и инфраструктура были слишком трудно реализовать SOA, и они не увидят необходимость, пока его размер увеличивается.

С точки зрения инфраструктуры каждого сервера можно выполнять многие приложения, в том же узле и имеют допустимые доля эффективность в использования ресурсов, как показано на рисунке 4-2.

![](./media/image2.png)

Рис. 4-2: узел под управлением нескольких приложений или контейнеров

Монолитные приложения в Azure можно развернуть с помощью выделенных виртуальных машин для каждого экземпляра. С помощью [набора масштабирования виртуальных Машин Azure](https://docs.microsoft.com/azure/virtual-machine-scale-sets/), можно легко масштабировать виртуальных машин. [Службы приложений Azure](https://azure.microsoft.com/en-us/services/app-service/) можно запускать монолитные приложения и легко масштабировать экземпляры без необходимости управления виртуальными машинами. С момента 2016 г. службы приложений Azure можно запустить отдельные экземпляры контейнеры Docker, а также упрощения развертывания. И с помощью Docker, можно развернуть в одной виртуальной Машины узел Docker и запустить несколько экземпляров. С помощью балансировки Azure, как показано на рисунке 4-3, вы можете управлять масштабирования.

![](./media/image3.png)

Рис. 4-3: несколько узлов масштабирования одного приложения приложений или контейнеры Docker

Вы можете управлять для различных узлов через традиционные методы развертывания. Узлы Docker можно управлять с помощью команды `docker run` вручную, с помощью автоматизации, такие как конвейеры непрерывной поставки (CD), которые объясняются ниже в этой книге e.

## <a name="monolithic-application-deployed-as-a-container"></a>Монолитные приложения, развернуть как контейнер

Существуют преимущества при использовании контейнеров для управления развертываниями монолитные. Масштабирование экземпляров контейнеров гораздо быстрее и проще, чем развертывание дополнительных виртуальных машин. Несмотря на то, что набора масштабирования виртуальных Машин — Это прекрасная возможность для масштабирования виртуальных машин, которые требуются для размещения в контейнеры Docker, они принимают времени для установки. При развертывании в качестве экземпляров приложения, конфигурацию приложения осуществляется в рамках виртуальной машины.

Развертывание обновлений, как образы Docker гораздо быстрее и эффективно сети. Vn экземпляры можно настроить на те же узлы, как экземпляры Vn-1, устраняя добавлены затраты, возникающие в результате дополнительных ВМ. Образы docker, как правило, начинается в секундах, что позволяет ускорить процесс развертывания. То закрытие экземпляра Docker можно так же легко, как вызов `docker stop` команду, обычно Завершение менее чем за секунду.

Поскольку контейнеры являются по своей природе неизменяемыми, намеренно, никогда не нужно беспокоиться о поврежденных виртуальные машины, поскольку забыли сценарий обновления с учетом некоторых определенной конфигурации или файл, оставшегося на диске.

Несмотря на то, что монолитные приложения могут использовать преимущества Docker, мы прервать на только советы преимущества. Увеличить преимущества управления контейнерами поступает из развертывание с помощью orchestrators контейнера, управлять различных экземпляров и жизненный цикл экземпляра каждого контейнера. Разделить монолитные приложение в подсистемам, которые можно масштабировать, разработки и развертывания по отдельности представляет точку входа в область микрослужбами.

## <a name="publishing-a-single-docker-container-app-to-azure-app-service"></a>Публикация одного контейнера Docker приложения в службе приложений Azure

Либо потому, что вы хотите получить быстрый проверки контейнера, развернутой в Azure, либо потому, что приложение просто контейнер одного приложения службы приложений Azure предоставляет отличный способ предоставления масштабируемой один контейнер служб.

Служба приложений Azure с помощью интуитивно понятный и приступить к и быстрый запуск, так как она обеспечивает значительные Git интеграции использования вашего кода сборки в Microsoft Visual Studio, а также развернуть его непосредственно в Azure. Но, в большинстве случаев (с не Docker), при необходимости других возможностей, платформах и зависимости, которые не поддерживаются в службы приложения, необходимо дождаться, пока группа Azure обновляет эти зависимости в службе приложений или переключается на другие службы, такие как Service Fabric, облачные службы или даже простой виртуальных машин, для которых имеют управления и установить необходимый компонент или framework для приложения.

Теперь, но при этом (объявлено в Microsoft Connect 2016 в ноябре 2016) и как показано на 4‑4 рисунке, при использовании Visual Studio 2017 г., поддержка контейнера в службе приложений Azure дает возможность включать любые необходимые в вашей среде приложения. При добавлении зависимость приложения, так как вы используете его в контейнере, вы получаете возможность, в том числе эти зависимости в образ файла Dockerfile или Docker.

![](./media/image4.png)

Рис. 4-4: публикации контейнер службы приложений Azure из Visual Studio приложения контейнеры

Рис. 4-4 также показывает, что поток публикации помещает изображения с помощью реестра контейнера, который может быть реестра контейнера Azure (реестра вблизи к развертываниям в Azure и защищены учетные записи и группы Azure Active Directory) или любые другие реестра Docker как и реестров центр Docker или в локальной среде.


>[!div class="step-by-step"]
[Предыдущие] (Общие контейнера конструктора principles.md) [Далее] (state-and-data-in-docker-applications.md)
