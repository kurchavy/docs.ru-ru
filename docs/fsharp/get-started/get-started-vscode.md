---
title: "Начало работы с F # в коде Visual Studio с Ionide"
description: "Сведения об использовании языка F # с кодом Visual Studio и suite Ionide подключаемого модуля."
keywords: "Visual f #, f #, функционального программирования, vscode .NET, Visual Studio Code Ionide"
author: cartermp
ms.author: phcart
ms.date: 09/28/2016
ms.topic: article
ms.prod: .net
ms.technology: devlang-fsharp
ms.devlang: fsharp
ms.assetid: 49775139-082e-442f-b5a2-dd402399b5d2
ms.openlocfilehash: 336316eaf474f4c10d63657f178ce4a336ad7a54
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="getting-started-with-f-in-visual-studio-code-with-ionide"></a>Начало работы с F # в коде Visual Studio с Ionide

Вы можете написать F # в [кода Visual Studio](https://code.visualstudio.com) с [Ionide подключаемый модуль](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp), чтобы получить прекрасные возможности кросс платформенных, простое IDE с технологией IntelliSense и рефакторинг кода.  Посетите [Ionide.io](http://ionide.io) для получения дополнительных сведений о наборе подключаемого модуля.

## <a name="prerequisites"></a>Предварительные требования

F # 4.0 или более поздней версии должны устанавливаться на компьютере для использования Ionide.

Также необходимо иметь [git установлен](https://git-scm.com/download) и доступна на путь, чтобы сделать использование шаблонов проектов в Ionide.  Убедитесь, что он правильно установлен, введя `git` нажимая команда prompt.and **ввод**.

### <a name="windows"></a>Windows

Если вы используете Windows, имеется два варианта установки F #.

Если вы уже установили Visual Studio и нет F #, вы можете [Установка средств Visual F #](get-started-visual-studio.md#installing-f).  Будут установлены все необходимые компоненты для записи, компиляции и выполнения кода F #.

Если вы предпочитаете не установки Visual Studio, используйте следующие инструкции:

1. Установка [.NET Framework 4.5 или более поздней](https://www.microsoft.com/en-US/download/details.aspx?id=30653) Если вы используете Windows 7.  Если вы используете Windows 8 или более поздней версии, необходимо сделать это.

2. Установите пакет Windows SDK для вашей операционной системе:

    * [Windows 10 SDK](https://dev.windows.com/en-US/downloads/windows-10-sdk)
    * [Windows 8.1 SDK](http://msdn.microsoft.com/windows/desktop/bg162891)
    * [Windows 8 SDK](http://msdn.microsoft.com/windows/hardware/hh852363.aspx)
    * [Windows 7 SDK](http://www.microsoft.com/download/details.aspx?id=8279)

3. Установка [Microsoft Build Tools 2015](https://www.microsoft.com/en-us/download/details.aspx?id=48159).  Может потребоваться установить [2013 средства построения Microsoft](https://www.microsoft.com/en-us/download/details.aspx?id=40760).

4. Установка [инструменты Visual F #](https://www.microsoft.com/en-us/download/details.aspx?id=48179).

На 64-разрядной версии Windows компилятор и средства находятся здесь:

```
C:\Program Files (x86)\Microsoft SDKs\F#\4.0\Framework\v4.0\fsc.exe
C:\Program Files (x86)\Microsoft SDKs\F#\4.0\Framework\v4.0\fsi.exe
C:\Program Files (x86)\Microsoft SDKs\F#\4.0\Framework\v4.0\fsiAnyCpu.exe
```

На 32-разрядной версии Windows средства компилятора находятся здесь:

```
C:\Program Files\Microsoft SDKs\F#\4.0\Framework\v4.0\fsc.exe
C:\Program Files\Microsoft SDKs\F#\4.0\Framework\v4.0\fsi.exe
C:\Program Files\Microsoft SDKs\F#\4.0\Framework\v4.0\fsiAnyCpu.exe
```

Ionide автоматически обнаруживает компилятора и инструментов, но если это не так, для какой-либо причине (например, Visual F # Tools были установлены в другой каталог), можно вручную добавить папку, содержащую (`...\Microsoft SDKs\F#\4.0`) в путь.

### <a name="macos"></a>MacOS

На macOS, использует Ionide [моно](http://www.mono-project.com).  Самый простой способ установить Mono на macOS — через Homebrew.  Просто введите следующую команду в окне терминала:

```
brew install mono
```

### <a name="linux"></a>Linux

В Linux, также использует Ionide [моно](http://www.mono-project.com).  Если вы на Debian и Ubuntu, можно использовать следующее:

```
sudo apt-get update
sudo apt-get install mono-complete fsharp
```

## <a name="installing-visual-studio-code-and-the-ionide-plugin"></a>Установка Visual Studio Code и подключаемый модуль Ionide

Можно установить Visual Studio код из [code.visualstudio.com](https://code.visualstudio.com) веб-сайта.  После этого можно найти подключаемый модуль Ionide двумя способами:

1. Использовать палитру команд (Ctrl + Shift + P в Windows, ⌘ + Shift + P на macOS Ctrl + Shift + P в Linux) и введите следующую команду:

    ```
    >ext install Ionide
    ```

2. Щелкните значок расширения и выполните поиск «Ionide»:

    ![](media/getting-started-vscode/vscode-ext.png)

Только для поддержки F # в коде Visual Studio требуется подключаемый модуль [Ionide fsharp](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-fsharp).  Тем не менее, можно также установить [Ionide ИМИТАЦИИ](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-FAKE) и получить [ПОДДЕЛАТЬ](http://fsharp.github.io/FAKE/) поддержки и [Ionide Paket](https://marketplace.visualstudio.com/items?itemName=Ionide.Ionide-Paket) для получения [Paket](https://fsprojects.github.io/Paket/) поддержки.  ПОДДЕЛАТЬ и Paket средства сообщества дополнительные F # для создания проектов и управление зависимостями, соответственно.

## <a name="creating-your-first-project-with-ionide"></a>Создание первого проекта с Ionide

Чтобы создать новый проект F #, откройте кода Visual Studio в новую папку (можно назвать его любым).

![](media/getting-started-vscode/vscode-open-dir.png)

Затем откройте в палитру команд (Ctrl + Shift + P в Windows, ⌘ + Shift + P на macOS Ctrl + Shift + P в Linux) и введите следующую команду:

```
>f#: New Project
```

Это работает на основе [FORGE](https://github.com/fsharp-editing/Forge) проекта.  Результат должен быть примерно таким:

![](media/getting-started-vscode/vscode-new-proj.png)

> [!NOTE]
Если вы не видите выше, обновите шаблоны, выполнив следующую команду в палитру команд: `>F#: Refresh Project Templates`.

Выберите «F #: новый проект», нажав **ввод**, которой вы перейдете этот шаг:

![](media/getting-started-vscode/vscode-proj-type.png)

Это будет выбрать шаблон для определенного типа проекта.  Существует довольно много вариантов, например [FsLab](http://fslab.org) шаблон для обработки и анализа данных или [Suave](https://suave.io) шаблона для веб-программирования.  В этой статье используется `classlib` шаблона, поэтому выделения и нажмите кнопку **ввод**.  Затем будет достигнут следующий шаг:

![](media/getting-started-vscode/vscode-new-dir.png)

Это позволяет при необходимости создания проекта в другом каталоге.  Не указывайте его сейчас.  Он будет создан проект в текущем каталоге.  После нажатия клавиши **ввод**, будет достигнут следующий шаг:

![](media/getting-started-vscode/vscode-proj-name.png)

Это позволяет имя проекта.  F # использует [случае Pascal](http://c2.com/cgi/wiki?PascalCase) для имен проектов.  В этой статье используется `ClassLibraryDemo` как имя.  Как только вы ввели имя для проекта, нажмите **ввод**.

Если были выполнены действия предыдущего шага, вы должны получить Visual Studio код рабочей области с левой стороны выглядит примерно следующим образом:

![](media/getting-started-vscode/vscode-new-proj-explorer.png)

Этот шаблон создает некоторые моменты, которые вы найдете полезные:

1. F # сам проект, под `ClassLibraryDemo` папки.
2. Правильной структуры каталогов для добавления пакетов через [ `Paket` ](http://fsprojects.github.io/Paket/).
3. Кросс платформенных создания скрипта с [ `FAKE` ](http://fsharp.github.io/FAKE/).
4. `paket.exe` Исполняемый файл, в которой можно получить пакеты и разрешить зависимости для вас.
5. Объект `.gitignore` файл, если вы хотите добавить этот проект с системой управления версиями, основанных на Git.

## <a name="writing-some-code"></a>Написание кода

Откройте *ClassLibraryDemo* папки.  Вы увидите следующие файлы:

1. `ClassLibraryDemo.fs`, файле реализации F # с помощью класса, определенного.
2. `CassLibraryDemo.fsproj`, F # файл проекта используется для построения данного проекта.
3. `Script.fsx`, в файл скрипта F # который загружает исходный файл.
4. `paket.references`, в файл Paket, который указывает зависимости проекта.

Откройте `Script.fsx`и добавьте следующий код в конце:

[!code-fsharp[ToPigLatin](../../../samples/snippets/fsharp/getting-started/to-pig-latin.fsx)]

Эта функция преобразует слова в форму [Pig латиница](https://en.wikipedia.org/wiki/Pig_Latin).  Следующим шагом является оценка с помощью F # интерактивный (FSI).

Выделите всей функции (должна быть 11 строк).  Как только он выделяется, удерживайте **Alt** ключа и нажмите кнопку **ввод**.  Вы заметите всплывающее ниже окна и будет выглядеть примерно следующим образом:

![](media/getting-started-vscode/vscode-fsi.png)

Это сделали три действия:

1. Он запущен процесс FSI.
2. Выделенный вами код передаваемых FSI процесса.
3. Процесс FSI вычисляется код, отправляемых по.

Из-за отправляемых по [функция](../language-reference/functions/index.md), теперь можно вызвать этой функции с FSI!  В интерактивном окне введите следующую команду:

```fsharp
toPigLatin "banana";;
```

Должен появиться следующий результат:

```fsharp
val it : string = "ananabay"
```

Теперь попробуем с первой буквой гласные. Введите следующий текст:

```fsharp
toPigLatin "apple";;
```

Должен появиться следующий результат:

```fsharp
val it : string = "appleyay"
```

По-видимому, функция работает, как ожидалось.  Итак, просто написал первой функции F # в Visual Studio Code и его для оценки FSI.

>[!NOTE]
Как можно заметить, в строках в FSI завершаются `;;`.  Это происходит потому FSI позволяет вводить несколько строк.  `;;` В конце позволяет FSI знать, когда код будет завершено.

## <a name="explaining-the-code"></a>Объясняется в коде

Если вы не уверены, что фактически выполняет код, вот пошаговые.

Как видите, `toPigLatin` является функция, которая принимает word в качестве входных данных и преобразует его в Латинской Pig слова.  Для этого правила таковы:

Если первый символ, слово, которое начинается с гласные, добавьте в конец слова «yay».  Если он не начинается с гласные, переместите первого знака в конец слова и «один» добавьте к нему.

Возможно, вы заметили в FSI следующие:

```
val toPigLatin : word:string -> string
```

Том, что `toPigLatin` является функция, которая принимает `string` в качестве входного (называется `word`) и возвращает другой `string`.  Это называется [сигнатура типа функции](https://fsharpforfunandprofit.com/posts/function-signatures/), основные части F #, который является ключом к пониманию кода F #.  Можно также заметить при наведении указателя на функцию в Visual Studio Code.

В теле функции вы увидите двух отдельных частей:

1. Внутренние функции, называемой `isVowel`, которое определяет, если данный символ (`c`) является гласные путем проверки, если он соответствует одному из указанных шаблонов через [соответствие шаблону](../language-reference/pattern-matching.md):

   [!code-fsharp[ToPigLatin](../../../samples/snippets/fsharp/getting-started/to-pig-latin.fsx#L2-L6)]

2. [ `if..then..else` ](../language-reference/conditional-expressions-if-then-else.md) Выражение, которое проверяет, если первый символ является гласные и создает значение, возвращаемое из входных символов на основе Если первый символ был гласные или нет:

   [!code-fsharp[ToPigLatin](../../../samples/snippets/fsharp/getting-started/to-pig-latin.fsx#L8-L11)]

Поток `toPigLatin` таким образом:

Проверьте, является ли первый символ слова входной гласные.  Если это так, приложите «yay» до конца слова.  В противном случае переместите первого знака в конец слова и «один» добавьте к нему.

Нет заключительную Обратите внимание, об этом: нет нет явных инструкций для возврата из функции, в отличие от многих других языков здесь.  Это происходит потому F # основано на выражении, и последнего выражения в теле функции является возвращаемым значением.  Поскольку `if..then..else` сам по себе является выражением, тело `then` блока или в теле `else` блок будет возвращаться в зависимости от входного значения.

## <a name="moving-your-script-code-into-the-implementation-file"></a>Перемещение кода скрипта в файле реализации

Предыдущие разделы этой статьи показано общих первым шагом в написании кода F #: функцию начальной записи и выполнить его в интерактивном режиме с FSI.  Это называется разработка REPL, где REPL означает «Цикла оценки печати чтения».  Это отличный способ поэкспериментировать с функциональные возможности, пока не получится, что-либо работы.

Следующий этап разработки на основе REPL является перемещение рабочий код в файле реализации F #.  Он затем может компилироваться компилятором F # в сборку, которая может быть выполнена.

Чтобы начать, откройте `ClassLibraryDemo.fs`.  Вы заметите, что определенный код уже существует.  Продолжить и удалить определение класса, но убедитесь в том оставить [ `namespace` ](../language-reference/namespaces.md) объявление в начале.

Создайте новый [ `module` ](../language-reference/modules.md) вызывается `PigLatin` и скопируйте `toPigLatin` функции в нее таким образом:

[!code-fsharp[ToPigLatin](../../../samples/snippets/fsharp/getting-started/pig-latin.fs#L1-L14)]

Это один из многих способов, которые можно организовать функций в коде F # и общий подход, если требуется вызов кода из C# или проекты Visual Basic.

Затем откройте `Script.fsx` файл еще раз и удалить весь `toPigLatin` работать, но не забудьте сохранить следующие две строки в файле:

```
#load "ClassLibraryDemo.fs"
open ClassLibraryDemo
```

Первая строка необходим для сценариев для загрузки FSI `ClassLibraryDemo.fs`.  Вторая строка — удобный: пропуск он необязателен, но вам будет нужно ввести `open ClassLibraryDemo` в окне с FSI, если вы хотите подключить `ToPigLatin` модуля в область действия.

Затем в окне «FSI» вызовите функцию с `PigLatin` модуля, определенного ранее:

```
> PigLatin.toPigLatin "banana";;
val it : string = "ananabay"
> PigLatin.toPigLatin "apple";;
val it : string = "appleyay"
```

Готово!  Получить те же результаты, но теперь загружаются из файла реализации F #.  Здесь основное отличие заключается в том, что исходными файлами F # компилируются в сборки, которые могут быть выполнены в любом месте, не только в FSI.

## <a name="summary"></a>Сводка

В этой статье вы узнали:

1. Как настроить Visual Studio код с Ionide.
2. Создание первого проекта F # с Ionide.
3. Инструкции по использованию скриптов F # для создания первой функции F # на Ionide, а затем выполнить его в FSI.
4. Как перенести код скрипта F # источника и затем вызвать этот код из FSI.

Вы теперь способны записывать гораздо большего объема кода F #, используя код Visual Studio и Ionide.

## <a name="troubleshooting"></a>Устранение неполадок

Ниже приведены несколько способов, которые можно устранить определенные неполадки, которые вы можете столкнуться.

1. Чтобы получить возможности редактирования кода среды Ionide, F #, файлы должны быть сохранены на диск и внутри папки, который открыт в рабочей области кода Visual Studio.
2. Если были внесены изменения в систему или установить необходимые компоненты Ionide с открытым кодом Visual Studio, перезапустите Visual Studio Code.
3. Проверьте, можно использовать компилятор F # и F # interactive из командной строки без полный путь.  Это можно сделать, введя `fsc` в командной строке компилятора F #, и `fsi` или `fsharpi` для Visual F # средств в Windows и Mono на Mac, Linux, соответственно.
4. Если у вас есть недопустимые символы в каталогах проекта, Ionide может не работать.  Переименование каталогов проекта, если это так.
5. Если ни одна из команд Ionide работают, проверьте вашей [сочетания клавиш в Visual Studio Code](https://code.visualstudio.com/docs/customization/keybindings#_customizing-shortcuts) для просмотра, если их переопределение случайно.
6. Если ни один из указанных выше проблема исправлена проблема Ionide разбивается на компьютере, попробуйте удалить `ionide-fsharp` каталог на компьютере и переустановите пакет подключаемого модуля.

Ionide является проекта с открытым кодом создаваемый и используемый средством членами сообщества F #.  Следует сообщить о проблемах и вы можете принять участие в [Ionide VSCode: репозитории FSharp GitHub](https://github.com/ionide/ionide-vscode-fsharp).

Если имеется проблема в отчет, выполните [инструкции по получению журналов для использования при сообщение о проблеме,](https://github.com/ionide/ionide-vscode-fsharp#how-to-get-logs-for-debugging--issue-reporting).

Также можно задать для получения дополнительных сведений из Ionide разработчиков и сообщества F # в [Ionide Gitter канала](https://gitter.im/ionide/ionide-project).

## <a name="next-steps"></a>Следующие шаги

Дополнительные сведения о F # и функции языка, извлечь [обзор языка F #](../tour.md).

## <a name="see-also"></a>См. также

[Обзор языка F#](../tour.md)

[Справочник по языку F#](../language-reference/index.md)

[Функции](../language-reference/functions/index.md)

[Модули](../language-reference/modules.md)

[Пространства имен](../language-reference/namespaces.md)

[Ionide VSCode: FSharp](https://github.com/ionide/ionide-vscode-fsharp)
