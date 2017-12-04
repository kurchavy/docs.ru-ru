---
title: "События домена. Проектирование и реализация"
description: "Архитектура Микрослужбами .NET для приложений .NET в контейнерах | События домена, проектирования и реализации"
keywords: "Docker, микрослужбы, ASP.NET, контейнер"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 05/26/2017
ms.prod: .net-core
ms.technology: dotnet-docker
ms.topic: article
ms.openlocfilehash: 2d98b302be4ee72d8225526944fc3e41cbadcb5f
ms.sourcegitcommit: bd1ef61f4bb794b25383d3d72e71041a5ced172e
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/18/2017
---
# <a name="domain-events-design-and-implementation"></a>События домена: проектирование и реализация

События домена используйте явно реализовать побочные эффекты изменений в том же домене. В другие слова и с помощью терминологии ддд домена события можно используйте чтобы явно реализовать побочные эффекты в несколько статистических выражений. При необходимости для повышения масштабируемости и менее без влияния на блокировок базы данных используйте окончательной согласованности между статистические выражения в том же домене.

## <a name="what-is-a-domain-event"></a>Что такое событие домена?

Событие — это то, что произошло в прошлом. События домена, логически, то, что произошло в определенном домене, и что-то предполагается домену (внутрипроцессный) следует учитывать и потенциально реагирования на другие части.

Важное преимущество событий домена — что побочные эффекты после что-то произошло в домене можно выразить явно вместо неявно. Эти эффекты должны быть согласованы, либо все связанные с бизнес-задачи выполняются операции на стороне, или ни один из них. Кроме того события домена включить лучшего разделения областей ответственности между классами в том же домене.

Например если используется только просто Entity Framework и сущности или даже статистических выражений, если должно быть в варианте использования вызывает побочные эффекты, те будет реализован в качестве неявного понятием в связанной кода после произошла ошибка. Но видны только этот код может быть неизвестно, если этот код (побочным эффектом) является частью основной операции или если это побочный эффект. С другой стороны использование события домена делает концепции явного и частью единый язык. Например в приложении eShopOnContainers Создание заказа не практически порядке; он обновляет или создает статистические покупателя, на основе исходного пользователя, поскольку пользователь не является покупателем, до момента заказа. При использовании события домена можно выразить явно, правило домена в единый язык, предоставляемые специалистами в предметной области.

События домена чем-то похожи на события стиле сообщений, с одним важным отличием. С реальными обмена сообщениями, очереди сообщений, посредникам или service bus с помощью AMPQ сообщение всегда асинхронной рассылки и передается между процессами и компьютеров. Это полезно для интеграции нескольких ограниченных контекстах, микрослужбами или даже в разных приложениях. С событиями домена, необходимо вызвать событие операция домена, которым в данный момент работает, однако требуется никаких побочных эффектов, в том же домене.

События домена и их побочные эффекты (действия после этого запускается под управлением обработчики событий) должно выполняться почти мгновенно, обычно в процессе и в том же домене. Таким образом события домена могут быть синхронными или асинхронными. События интеграции, тем не менее, должно всегда выполняться асинхронно.

## <a name="domain-events-versus-integration-events"></a>События домена и события интеграции

Семантически, домена и интеграцию события — это то же самое: уведомления о том, произошедшего. Тем не менее их реализации должны быть разными. События домена — это просто сообщений, отправленных на диспетчер событий домена, который может быть реализован как посредника в памяти, на основе контейнер IoC или любой другой метод.

С другой стороны события интеграции предназначено для распространения зафиксированных транзакций и обновления для дополнительных подсистем, вне зависимости от их других микрослужбами, ограниченных контекстах или даже внешними приложениями. Следовательно, их следует выполнять, только если сущность успешно сохранен, так как во многих сценариях в случае сбоя всей операции эффективно никогда не происходило.

Дополнительно и как сказано выше, интеграция события должны быть основаны на асинхронное взаимодействие между несколькими микрослужбами (других ограниченных контекстах) или внешних систем и приложений. Таким образом интерфейс шины событий должен некоторые инфраструктуры, которая позволяет процессу между и распределенных обмен данными между потенциально удаленной службы. Он может основываться на коммерческих служебной шины, очереди, общей базы данных, используемый в качестве почтового ящика или любой другой распределенных и в идеале Push-уведомлений системы обмена сообщениями на основе.

## <a name="domain-events-as-a-preferred-way-to-trigger-side-effects-across-multiple-aggregates-within-the-same-domain"></a>События домена как предпочтительный способ запуска побочные эффекты в несколько агрегатов в том же домене

Если при выполнении команды, связанной с одного экземпляра агрегатной функции требует дополнительного домена правил для выполнения на один или несколько дополнительных статистических выражений, следует проектировании и реализации этих побочные эффекты, которое будет вызвано события домена. Как показано на рисунке 9-14 и как один из наиболее важные варианты использования, событие домена следует использовать для распространения изменений состояния в несколько агрегатов в одной модели домена.

![](./media/image15.png)

**Рис. 9-14**. События домена для обеспечения согласованности между несколько статистических выражений в том же домене

На рисунке когда пользователь инициирует заказ, событие OrderStarted домена запускает создание объекта покупателей в упорядочивания микрослужбу, на основе исходные сведения о пользователе из удостоверения микрослужбу (сведения о командой CreateOrder). Событие домена формируется с помощью агрегирования заказа при его создании в первую очередь.

Кроме того можно иметь статистические корневой подписан на события, вызванные члены его агрегатов (дочерние объекты). Для экземпляра каждой дочерней сущности OrderItem может вызвать событие, когда цена товара превышает определенный промежуток или сумма продукта элементов слишком велико. Агрегатные корневой можно получать эти события и выполнить расчет глобальных или статистической обработки.

Важно понимать, что это взаимодействие на основе событий не реализован непосредственно в статистические функции; необходимо реализовать обработчики событий для домена. Обработка событий домена является аспектом приложения. Уровень модели домена должна быть направлена только на доменную логику — факторов расценит эксперта, не инфраструктуры приложений как обработчики и действий сохраняемости побочных эффектов, с помощью репозиториев. Таким образом приложения слоя будет представлять уровень которой должны выглядеть домена обработчики событий, запускающего действия при возникновении события домена.

События домена может также использоваться для запуска любого числа действий приложения и что является более важным, должен быть открытым, чтобы увеличить это число в будущем несвязанной способом. Для экземпляра при его запуске, можно опубликовать событие домена для распространения, info или другими статистическими выражениями или даже для вызова действий приложения, таких как уведомления.

Основная задача — открыть количество действий для выполнения при возникновении события домена. Со временем действия и правила в домене и приложение будет увеличиваться. Сложность или количество побочным эффектом действия, когда происходит событие будет увеличиваться, но если код были вместе с «связующего» (то есть просто создание экземпляров объектов с помощью нового ключевого слова в C\#), то каждый раз, вам необходимо, чтобы добавить новое действие необходимо для Изменение исходного кода. Это может привести к новые ошибки, так как с каждой новое требование может потребоваться изменить исходный поток кода. Это противоречит [Open или Closed принцип](https://en.wikipedia.org/wiki/Open/closed_principle) из [СПЛОШНОЙ](https://en.wikipedia.org/wiki/SOLID_(object-oriented_design)). Это не единственная, исходный класс, оркестрация операции будет иметь, а, которая противоречит [один принцип ответственности (SRP)](https://en.wikipedia.org/wiki/Single_responsibility_principle).

С другой стороны при использовании события домена можно создать точного и несвязанной реализация по возможности размещая обязанности, используя этот подход:

1.  Отправьте команду (например, CreateOrder).
2.  Получать команды в обработчике команды.
    -   Выполните транзакцию одного статистического выражения.
    -   (Необязательно) Вызов событий домена для побочные эффекты (например, OrderStartedDomainDvent).
1.  Дескриптор домена события (в текущий процесс) thast выполнит откройте число побочные эффекты в нескольких статистических выражений или действий приложения. Пример:
    -   Проверьте или создать метод Покупатель "и" Оплата ".
    -   Создание и отправка событий связанных интеграции шину событий выходят за микрослужбами или триггера внешних действий Отправка сообщения электронной почты покупателю состояний.
    -   Обрабатывать никаких побочных эффектов.

Как показано на рисунке 9-15, начиная с того же домена события, можно обрабатывать несколько действий, связанных с другими статистическими функциями в домене или дополнительное приложение действия, необходимые для выполнения между микрослужбами соединение с помощью интеграции событий и событий шины.

![](./media/image16.png)

**Рис. 9-15**. Обработка нескольких действий в домене

Обработчики событий обычно являются на уровне приложения, так как объекты инфраструктуры, такие как репозиториев или API, приложение будет использовать для микрослужбу поведения. В этом смысле обработчики событий аналогичны обработчики команд, поэтому оба являются частью на уровне приложения. Важное отличие заключается в том, что команды должны обрабатываться только один раз. Событие домена может быть обработано ноль или  *n*  время ожидания, поскольку если могут быть получены нескольких получателей или обработчики событий с целью разных для каждого обработчика.

Возможность открыть количество обработчиков на событие домена позволяет добавлять множество дополнительных правил домена без влияния на текущий код. Например реализации следующих бизнес-правила, не произошло справа после события может быть так же легко, как добавить несколько обработчиков событий (или хотя бы один):

Общая сумма, приобретенных клиентом в хранилище через любое количество заказов, превышает 6000, применяются 10% от скидки каждый новый заказ и уведомление клиента с адресом электронной почты об этой скидки для заказов в будущем.

## <a name="implementing-domain-events"></a>Реализация событий в домене

В C# событие домена является просто хранения данных структуры или класса, например DTO, со всеми сведениями, связанные с произошедшее в домене, как показано в следующем примере:

```csharp
public class OrderStartedDomainEvent : IAsyncNotification
{
    public int CardTypeId { get; private set; }
    public string CardNumber { get; private set; }
    public string CardSecurityNumber { get; private set; }
    public string CardHolderName { get; private set; }
    public DateTime CardExpiration { get; private set; }
    public Order Order { get; private set; }

    public OrderStartedDomainEvent(Order order,
        int cardTypeId, string cardNumber,
        string cardSecurityNumber, string cardHolderName,
        DateTime cardExpiration)
    {
        Order = order;
        CardTypeId = cardTypeId;
        CardNumber = cardNumber;
        CardSecurityNumber = cardSecurityNumber;
        CardHolderName = cardHolderName;
        CardExpiration = cardExpiration;
    }
}
```

Это по сути класс, содержащий все данные, относящиеся к событию OrderStarted.

С точки зрения единый язык домена так как событие является то, что произошло в прошлом, имя класса события должны быть представлены как команда прошедшем времени, например OrderStartedDomainEvent или OrderShippedDomainEvent. Это реализации упорядочивания микрослужбу в eShopOnContainers событие домена.

Как мы отмечали важной характеристикой событий является, так как событие является то, что произошло в прошлом, не следует изменять. Поэтому он должен являться неизменяемого класса. Вы увидите в приведенном выше коде, что свойства доступны только для чтения вне объекта. Единственный способ обновления объекта — через конструктор при создании объекта события.

### <a name="raising-domain-events"></a>Создание домена событий

Следующий вопрос заключается в том, как инициировать событие домена, поэтому достигнет соответствующих обработчиков событий, связанных. Можно использовать несколько подходов.

Ранее было предложено UDI Dahan (например, в нескольких связанных записей, такие как [события домена — требует 2](http://udidahan.com/2008/08/25/domain-events-take-2/)) с помощью статического класса для управления и вызов событий. Сюда могут относиться статический класс с именем DomainEvents, приведет к возникновению событий домена немедленно в том случае, когда он вызывается с помощью синтаксиса, подобного DomainEvents.Raise (событие myEvent). Джимми Богард производили запись в блоге ([повышению уровня домена: события домена](https://lostechies.com/jimmybogard/2010/04/08/strengthening-your-domain-domain-events/)), корпорация Майкрософт рекомендует подобный подход.

Тем не менее если класс событий домена является статическим, он также отправляет обработчикам немедленно. Это усложняет тестирование и отладка, поскольку обработчики событий с логикой побочные эффекты выполняются сразу же после события. Тестирование и отладка необходимо сосредоточиться на и только что происходит в текущей статистической классов. не требуется внезапно перенаправляться на другие обработчики для побочные эффекты, связанные с другими статистические функции или логику приложения. Именно поэтому других подходов, отражающих развитие, как описано в следующем разделе.

#### <a name="the-deferred-approach-for-raising-and-dispatching-events"></a>Отложенное подход для вызова и диспетчеризации событий

Вместо немедленно диспетчеризации с обработчиком событий домена, лучшим подходом является добавление событий в коллекцию и последующей отправки этих событий домена *прямо перед* или *правой*  *После* фиксации транзакции (как при использовании SaveChanges в EF). (Джимми Богард описанного этот подход в этой записи [лучше шаблон события домена](https://lostechies.com/jimmybogard/2014/05/13/a-better-domain-events-pattern/).)

Выбор при отправке события домена до или правом сразу после фиксации транзакции важна, так как он определяет, включаются ли в рамках одной транзакции или в разных транзакциях побочные эффекты. В последнем случае необходимо работать с окончательной согласованности между несколько статистических выражений. В этом разделе рассматривается в следующем разделе.

Отложенное подход заключается в какой eShopOnContainers используется. Сначала добавьте событиях, происходящих в сущностях в коллекцию или список событий по сущности. Этот список должно быть частью объекта сущности или даже лучше, частью базовой сущности класса, как показано в следующем примере:

```csharp
public abstract class Entity
{
    private List<IAsyncNotification> _domainEvents;

    public List<IAsyncNotification> DomainEvents => _domainEvents;

    public void AddDomainEvent(IAsyncNotification eventItem)
    {
        _domainEvents = _domainEvents ?? new List<IAsyncNotification>();
        _domainEvents.Add(eventItem);
    }

    public void RemoveDomainEvent(IAsyncNotification eventItem)
    {
        if (_domainEvents is null) return;
        _domainEvents.Remove(eventItem);
    }
    // ...
}
```

При необходимости создайте событие, нужно просто добавить его в коллекцию событий для размещения в методе статистические сущности, как показано в следующем коде:

```csharp
var orderStartedDomainEvent = new OrderStartedDomainEvent(this, //Order object
    cardTypeId,
    cardNumber,
    cardSecurityNumber,
    cardHolderName,
    cardExpiration);
this.AddDomainEvent(orderStartedDomainEvent);
```

Обратите внимание, что единственное, что делает AddDomainEvent метод добавления события в список. Событие не возникает еще и нет обработчика вызывается еще.

Фактически вы хотите позже на диспетчеризации событий при фиксации транзакции в базу данных. При использовании Entity Framework Core, то есть в метод SaveChanges вашей EF DbContext, как показано в следующем коде:

```csharp
// EF Core DbContext
public class OrderingContext : DbContext, IUnitOfWork
{
    // ...
    public async Task<int> SaveEntitiesAsync()
    {
        // Dispatch Domain Events collection.
        // Choices:
        // A) Right BEFORE committing data (EF SaveChanges) into the DB. This makes
        // a single transaction including side effects from the domain event
        // handlers that are using the same DbContext with Scope lifetime
        // B) Right AFTER committing data (EF SaveChanges) into the DB. This makes
        // multiple transactions. You will need to handle eventual consistency and
        // compensatory actions in case of failures.
        await _mediator.DispatchDomainEventsAsync(this);
        // After this line runs, all the changes (from the Command Handler and Domain
        // event handlers) performed through the DbContext will be commited
        var result = await base.SaveChangesAsync();
    }
}
```

Этот код отправляют события объектов в их обработчики событий.

Общий результат является, что вы лишается вызова события домена (простого добавления в список в памяти) распределения его в обработчик событий. Кроме того в зависимости от того, какого рода dispatcher используется, может отправлять события синхронно или асинхронно.

Имейте в виду здесь воспроизвести границы транзакций, следует учитывать значительные. Если единиц работы и транзакция может охватывать более одного агрегата (как при использовании EF Core и реляционной базы данных), это может работать хорошо. Но если транзакция не может включать статистические выражения, например при использовании баз данных NoSQL, таких как Azure DocumentDB необходимо реализовывать дополнительные шаги для поддержания согласованности. Это еще одна причина, почему сохраняемости не является универсальной; Это зависит от используемой системы хранения.

### <a name="single-transaction-across-aggregates-versus-eventual-consistency-across-aggregates"></a>Одной транзакции между статистические выражения и окончательной согласованности между статистические функции

Вопрос, следует ли выполнять одной транзакции между статистические выражения и полагаться на окончательной согласованности между этими статистические выражения является противоречивым. DDD инструкция SQL, как Eric Evans и Vernon Вон представление правило, одна транзакция = одного агрегата и поэтому аргументы в пользу окончательной согласованности между статистических выражений. Например, в своей книге *сей разработки*, Eric Evans указано следующее:

Любое правило, охватывающий статистические выражения, не следует ожидать будут обновленными в любое время. Посредством обработки события, пакетная обработка или другие механизмы обновления другие зависимости, могут быть устранены в некоторых определенное время. (стр. 128)

Vernon Вон говорится в следующие [эффективной статистической схемы. Часть II: Создание агрегирует рабочих вместе](http://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_2.pdf):

Таким образом, если выполнение команды для одного экземпляра агрегатной функции требует, что дополнительные бизнес-правила выполнения на один или несколько статистических выражений, используйте окончательной согласованности \[...\] Нет удобным способом для поддержки окончательной согласованности в модели ддд. Статистический метод публикует домена событие, которое времени для одного или нескольких подписчиков асинхронной.

Является основой на принятие детально транзакции вместо транзакциях, объединяющих несколько статистических выражений или сущности. Идея заключается во втором случае числа блокировок базы данных будет значительной в больших приложениях с высокой масштабируемостью. Тот факт, что высокий масштабируемых приложений должны использоваться мгновенных транзакционную согласованность между несколькими статистические выражения в рамках помогает принимать концепцию окончательной согласованности. Указанные изменения часто не нужны бизнес и отвечает в любом случае экспертов домена можно сказать, необходимы ли определенных операций атомарные транзакции. Если операция всегда должен атомарной транзакции между несколькими статистические выражения, может запросить ли ваш статистическое выражение должно быть больше или не был правильно разработанный.

Тем не менее, другие разработчики и архитекторы, как Джимми Богард не затронуты охват одной транзакции через несколько статистических выражений, но только если эти дополнительные статистические выражения относятся к побочные эффекты для одной и той же исходной команды. Например, в [лучше шаблон события домена](https://lostechies.com/jimmybogard/2014/05/13/a-better-domain-events-pattern/), Богард указано следующее:

Как правило, требуется побочные эффекты домена события происходят в одной и той же логической транзакции, но не в той же области домена события \[...\] Непосредственно перед мы зафиксировать наш транзакцию, мы перенаправления нашей их соответствующих обработчиков событий.

Если диспетчеризации событий право домена *перед* фиксации исходной транзакции, это означает, что вы хотите побочные эффекты этих событий, которые будут включены в той же транзакции. Например при сбое метода EF DbContext SaveChanges, будет произведен откат транзакции все изменения, включая результат операций побочный эффект, реализуемый обработчики событий связанных доменах. Это имеет поскольку область DbContext жизни по умолчанию определяется как «область.» Таким образом объект DbContext распределяется между несколькими объектами репозитория, создание экземпляров в пределах одной области или в граф объекта. Совпадает с областью HttpRequest при разработке веб-API или MVC-приложений.

На самом деле оба подхода (одной атомарной транзакции и окончательной согласованности) может быть справа. Это зависит домена или бизнес-требований и что специалистами в предметной области сообщить. Он также зависит от как масштабируемой необходима служба быть (более детального транзакции не нарушать по отношению к базе данных блокировки). И он зависит от того, какой объем инвестиций вы готовы внести в код, поскольку для окончательной согласованности требуется более сложный код для обнаружения несогласованности между статистические выражения и необходимость реализации Компенсационный выходной действия. Принять во внимание, что при фиксации изменений для исходной статистических вычислений, и после этого при событиях доставляются, имеется ли проблема и обработчики событий не удается зафиксировать их побочные эффекты, будет иметь несоответствия между статистические выражения.

Способ предоставления Компенсационный выходной действия будет хранить события домена в таблицах дополнительную базу данных, чтобы они могли быть частью исходной транзакции. После этого можно создать пакетную обработку, которая обнаруживает несогласованности и выполняет Компенсационный выходной действия путем сравнения список событий с текущим состоянием статистические выражения. Компенсационный выходной действия являются частью сложная тема, требующей глубокий анализ с вашей стороны, включая обсуждали ее с бизнес-пользователь и специалистами в предметной области.

В любом случае можно выбрать подход, что нужно. Но первоначального отложенное подход — вызов событий перед фиксацией, чтобы использовать одну транзакцию — наиболее простой подход, при использовании EF Core и реляционной базе данных. Это проще реализовать и допустимым во многих случаях бизнеса. Это также этот подход используется в упорядочивания микрослужбу в eShopOnContainers.

Но, как вы фактически отправляют эти события в их обработчики событий? Что такое \_объект посредником, содержатся в предыдущем примере? Его методы и артефакты, которые можно использовать для сопоставления событий и их обработчики событий.

### <a name="the-domain-event-dispatcher-mapping-from-events-to-event-handlers"></a>Диспетчер событий домена: сопоставление из журналов событий для обработчиков событий

После возможность перенаправлять или публикация событий, необходимо каким-либо артефакта, который будет публиковать события, чтобы каждый связанный обработчик может получить его, и процесс побочные эффекты на основе этого события.

Один из подходов заключается в системе real обмена сообщениями или даже события, возможно на основе шины на служебной шины, в отличие от событий в памяти. Однако в случае первого реальный обмен сообщениями бы чрезмерными для обработки события домена, поскольку необходимо обработать эти события в одном процессе (то есть, в том же слое домена и приложения).

Другой способ сопоставить события нескольких обработчиков событий — с помощью регистрации типов в контейнер IoC, чтобы могут динамически определять место для отправки событий. Другими словами необходимо знать, какие обработчики событий необходимо получить определенное событие. Упрощенный подход, показаны на рис. 9-16.

![](./media/image17.png)

**На рисунке 9 – 16**. Диспетчер событий домена с помощью IoC

Можно построить коммуникации и артефакты для реализации такого подхода самостоятельно. Тем не менее, можно использовать доступных библиотек как [MediatR](https://github.com/jbogard/MediatR), в системе использующий IoT контейнера. Может поэтому напрямую использовать стандартные интерфейсы и методы объекта посредником публикации диспетчеризации.

В коде необходимо сначала зарегистрировать типы обработчиков событий в контейнер IoC, как показано в следующем примере:

```csharp
public class MediatorModule : Autofac.Module
{
    protected override void Load(ContainerBuilder builder)
    {
        // Other registrations ...
        // Register the DomainEventHandler classes (they implement
        // IAsyncNotificationHandler<>) in assembly holding the Domain Events
        builder.RegisterAssemblyTypes(
            typeof(ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler)
            .GetTypeInfo().Assembly)
            .Where(t => t.IsClosedTypeOf(typeof(IAsyncNotificationHandler<>)))
            .AsImplementedInterfaces();
        // Other registrations ...
    }
}
```

Код сначала идентифицирует сборку, которая содержит обработчики событий домена, найдя сборку, которая содержит все обработчики (с помощью typeof(ValidateOrAddBuyerAggregateWhenXxxx), но можно выбрать другой обработчик событий для обнаружения сборки). Поскольку все обработчики событий реализует интерфейс IAsyncNotificationHandler, код, а затем просто ищет те типы и регистрирует все обработчики событий.

### <a name="how-to-subscribe-to-domain-events"></a>Как подписаться на события домена

При использовании MediatR каждый обработчик событий, необходимо использовать тип событий, который предоставляется на универсальный параметр IAsyncNotificationHandler интерфейса, как видно в следующем коде:

```csharp
public class ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler
  : IAsyncNotificationHandler<OrderStartedDomainEvent>
```

На основе связи между событием и обработчик событий, который может считаться подписки, артефакта MediatR может обнаружить все обработчики событий для каждого события и запустить каждый из этих обработчиков событий.

### <a name="how-to-handle-domain-events"></a>Способ обработки событий домена

Наконец обработчик события обычно реализует приложения слой кода, использующего репозиториев инфраструктуры для получения необходимых дополнительных агрегатов и для выполнения логики домена побочных эффектов. Вот пример кода:

```csharp
public class ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler
    : IAsyncNotificationHandler<OrderStartedDomainEvent>
{
    private readonly ILoggerFactory _logger;
    private readonly IBuyerRepository<Buyer> _buyerRepository;
    private readonly IIdentityService _identityService;
    public ValidateOrAddBuyerAggregateWhenOrderStartedDomainEventHandler(
        ILoggerFactory logger,
        IBuyerRepository<Buyer> buyerRepository,
        IIdentityService identityService)
    {
        // Parameter validations
        //...
    }

    public async Task Handle(OrderStartedDomainEvent orderStartedEvent)
    {
        var cardTypeId = (orderStartedEvent.CardTypeId != 0) ?
            orderStartedEvent.CardTypeId : 1;
        var userGuid = _identityService.GetUserIdentity();
        var buyer = await _buyerRepository.FindAsync(userGuid);
        bool buyerOriginallyExisted = (buyer == null) ? false : true;
        if (!buyerOriginallyExisted)
        {
            buyer = new Buyer(userGuid);
        }
        buyer.VerifyOrAddPaymentMethod(cardTypeId,
            $"Payment Method on {DateTime.UtcNow}",
            orderStartedEvent.CardNumber,
            orderStartedEvent.CardSecurityNumber,
            orderStartedEvent.CardHolderName,
            orderStartedEvent.CardExpiration,
            orderStartedEvent.Order.Id);
        var buyerUpdated = buyerOriginallyExisted ? _buyerRepository.Update(buyer) :
        _buyerRepository.Add(buyer);
        await _buyerRepository.UnitOfWork.SaveEntitiesAsync();
        // Logging code using buyerUpdated info, etc.
    }
}
```

Этот код обработчика событий считается код уровня приложения так, как она использует инфраструктуру репозиториев, как описано в следующем разделе на уровне инфраструктуры сохраняемости. Обработчики событий также можно использовать другие компоненты инфраструктуры.

#### <a name="domain-events-can-generate-integration-events-to-be-published-outside-of-the-microservice-boundaries"></a>События домена может создавать события интеграции для публикации вне границ микрослужбу

Наконец важно говоря о том, что иногда может потребоваться распространяется на несколько микрослужбами события. Считается интеграции события и может быть опубликован через шину событий из любого обработчика событий для конкретного домена.

## <a name="conclusions-on-domain-events"></a>Выводы о событиях домена 

Как уже говорилось, используйте события домена явно реализовать побочные эффекты изменений в том же домене. Чтобы использовать DDD терминология, домена события можно используйте для явно реализовать побочные эффекты в один или несколько статистических выражений. Кроме того и для повышения масштабируемости и меньше влияет на блокировки базы данных используйте окончательной согласованности между статистические выражения в том же домене.

#### <a name="additional-resources"></a>Дополнительные ресурсы

-   **Грег Янг. Что такое событие домена? ** 
     [ *http://codebetter.com/gregyoung/2010/04/11/what-is-a-domain-event/*](http://codebetter.com/gregyoung/2010/04/11/what-is-a-domain-event/)

-   **Stenberg января. События домена и окончательной согласованности**
    [*https://www.infoq.com/news/2015/09/domain-events-consistency*](https://www.infoq.com/news/2015/09/domain-events-consistency)

-   **Джимми Богард (Jimmy Bogard). Шаблон события лучше домена**
    [*https://lostechies.com/jimmybogard/2014/05/13/a-better-domain-events-pattern/*](https://lostechies.com/jimmybogard/2014/05/13/a-better-domain-events-pattern/)

-   **Вон Вернон (Vaughn Vernon). Эффективных статистических конструктора, часть II: Внесения рабочих статистические выражения вместе**
    [*http://dddcommunity.org/wp-content/uploads/files/pdf\_статьи или Vernon\_2011\_ 2. pdf*](http://dddcommunity.org/wp-content/uploads/files/pdf_articles/Vernon_2011_2.pdf)

-   **Джимми Богард (Jimmy Bogard). Усиление домена: события домена**
    *<https://lostechies.com/jimmybogard/2010/04/08/strengthening-your-domain-domain-events/>*

-   **Tony Truong. События домена шаблона пример**
    [*http://www.tonytruong.net/domain-events-pattern-example/*](http://www.tonytruong.net/domain-events-pattern-example/)

-   **UDI Dahan. Как создать полностью инкапсулирован моделей домена**
    [*http://udidahan.com/2008/02/29/how-to-create-fully-encapsulated-domain-models/*](http://udidahan.com/2008/02/29/how-to-create-fully-encapsulated-domain-models/)

-   **UDI Dahan. События домена — требует 2**
    [*http://udidahan.com/2008/08/25/domain-events-take-2/*](http://udidahan.com/2008/08/25/domain-events-take-2/%20)

-   **UDI Dahan. События домена — дать**
    [*http://udidahan.com/2009/06/14/domain-events-salvation/*](http://udidahan.com/2009/06/14/domain-events-salvation/)

-   **Kronquist января. Не публиковать события домена, возвращают их! ** 
     [ *https://blog.jayway.com/2013/06/20/dont-publish-domain-events-return-them/*](https://blog.jayway.com/2013/06/20/dont-publish-domain-events-return-them/)

-   **Сезар де ла Торре (Cesar de la Torre). Vs событий домена. События интеграции в архитектурах ддд и микрослужбами**
    [*https://blogs.msdn.microsoft.com/cesardelatorre/2017/02/07/domain-events-vs-integration-events-in-domain-driven-design-and-microservices-architectures/*](https://blogs.msdn.microsoft.com/cesardelatorre/2017/02/07/domain-events-vs-integration-events-in-domain-driven-design-and-microservices-architectures/)


>[!div class="step-by-step"]
[Предыдущие] (клиент стороны validation.md) [Далее] (инфраструктуры сохраняемости слоя design.md)