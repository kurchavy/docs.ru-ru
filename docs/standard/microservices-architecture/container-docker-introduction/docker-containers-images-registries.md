---
title: "Контейнеры docker, изображения и реестров"
description: "Архитектура Микрослужбами .NET для приложений .NET в контейнерах | Контейнеры docker, изображения и реестров"
keywords: "Docker, микрослужбы, ASP.NET, контейнер"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.openlocfilehash: 224fed34f06d10760b14aa9ecbae6c0e912915cf
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="docker-containers-images-and-registries"></a>Контейнеры docker, изображения и реестров

При использовании Docker, разработчик создает приложение или служба и пакеты его и его зависимости в образ контейнера. Образ — это статическое представление приложения или службы и его конфигурации и зависимостей.

Для выполнения приложения или службы, чтобы создать контейнер, в котором будут выполняться на узле Docker создается образ приложения. Контейнеров, изначально проверены в среде разработки или ПК.

Разработчикам следует хранить изображения в реестре, который выступает в качестве библиотеки изображений и требуются при развертывании в рабочей среде orchestrators. Docker обслуживает открытого реестра через [Docker Hub](https://hub.docker.com/); другие поставщики предлагают реестров для различных коллекций изображений. Кроме того, предприятия могут иметь частного реестра локальными для своих собственных образов Docker.

На рисунке 2 – 4 показано, как изображения и реестров в Docker связаны с другими компонентами. Он также содержит несколько предложений реестра от поставщиков.

![](./media/image5.PNG)

**На рисунке 2 – 4**. Классификация Docker термины и основные понятия

Размещение изображений в реестре позволяет хранить разряды статические и неизменяемый приложения, включая все их зависимости на уровне framework. Эти образы можно затем числовые версии и развертываются в нескольких средах и таким образом предоставляют единицу развертывания.

Реестры частный образ либо размещенной в локальной или в облаке, рекомендуется использовать при:

-   Изображения не должен быть общим открыто из-за конфиденциальность.

-   Требуется минимальная сетевая задержка между образов и среды выбранного развертывания. Например если облако Azure рабочей среды, может потребоваться хранения рисунков в реестре контейнера Azure, чтобы сетевая задержка будет минимальной. Аналогичным образом Если в локальной рабочей среды может потребоваться иметь локальные доверенный реестр Docker в той же локальной сети.

>[!div class="step-by-step"]
[Предыдущие] docker (terminology.md) [Далее] (.. /NET-Core-NET-Framework-Containers/index.MD)
