---
title: "Java ile aaaHow toouse Azure Service Bus konularını | Microsoft Docs"
description: "Azure'da Service Bus konuları ve abonelikleri kullanın."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="5a635-103">Nasıl toouse Service Bus konuları ve abonelikleri Java ile</span><span class="sxs-lookup"><span data-stu-id="5a635-103">How toouse Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="5a635-104">Bu kılavuzda açıklanmaktadır nasıl toouse Service Bus konuları ve abonelikleri.</span><span class="sxs-lookup"><span data-stu-id="5a635-104">This guide describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="5a635-105">Merhaba örnekleri Java'da yazılmış ve hello kullan [Java için Azure SDK][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="5a635-105">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="5a635-106">Merhaba kapsanan senaryolar dahil **konuları ve abonelikleri oluşturma**, **abonelik filtreleri oluşturma**, **iletileri tooa konu gönderme**, **alma bir abonelik iletilerden**, ve **konuları ve abonelikleri silmeyi**.</span><span class="sxs-lookup"><span data-stu-id="5a635-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="5a635-107">Service Bus konuları ve abonelikleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="5a635-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="5a635-108">Service Bus konuları ve abonelikleri *publish/subscribe* mesajlaşma iletişim modelini destekler.</span><span class="sxs-lookup"><span data-stu-id="5a635-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="5a635-109">Konular ve abonelikler kullanıldığında, dağıtılmış uygulamanın bileşenleri birbirleriyle doğrudan iletişim kurmazlar; bunun yerine bir aracı gibi davranan bir konu aracılığıyla iletileri değiş tokuş eder.</span><span class="sxs-lookup"><span data-stu-id="5a635-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="5a635-111">Service Bus kuyruklarının tersine, burada her ileti bir tüketici tarafından işlenir; konular ve abonelikler, publish/subscribe modelini kullanarak iletişimin "bir-çok" biçimini sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a635-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="5a635-112">Birden çok abonelik tooa konu kaydetmek mümkündür.</span><span class="sxs-lookup"><span data-stu-id="5a635-112">It is possible to register multiple subscriptions tooa topic.</span></span> <span data-ttu-id="5a635-113">Tooa konu bir ileti gönderildiğinde, ardından kullanılabilir tooeach abonelik toohandle/işlem bağımsız olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="5a635-113">When a message is sent tooa topic, it is then made available tooeach subscription toohandle/process independently.</span></span>

<span data-ttu-id="5a635-114">Bir abonelik tooa konu toohello konu gönderilen Merhaba iletileri kopyalarını alan sanal kuyruğa benzer.</span><span class="sxs-lookup"><span data-stu-id="5a635-114">A subscription tooa topic resembles a virtual queue that receives copies of hello messages that were sent toohello topic.</span></span> <span data-ttu-id="5a635-115">Filtre kuralları toofilter kısıtlamak/hangi iletileri tooa konu hangi konu abonelikleriyle alınan sağlayan bir abonelik başına temelinde bir konu için isteğe bağlı olarak kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a635-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you toofilter/restrict which messages tooa topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="5a635-116">Service Bus konuları ve abonelikleri çok sayıda kullanıcılar ve uygulamalar arasında tooscale tooprocess iletileri çok fazla sayıda etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="5a635-116">Service Bus topics and subscriptions enable you tooscale tooprocess a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="5a635-117">Hizmet ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a635-117">Create a service namespace</span></span>
<span data-ttu-id="5a635-118">Azure'da Service Bus konuları ve abonelikleri kullanarak toobegin ilk uygulamanızı Service Bus kaynaklarını adreslemek için kapsam bir kapsayıcı sağlar bir ad alanı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a635-118">toobegin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="5a635-119">toocreate bir ad alanı:</span><span class="sxs-lookup"><span data-stu-id="5a635-119">toocreate a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="5a635-120">Uygulama toouse Service Bus yapılandırın</span><span class="sxs-lookup"><span data-stu-id="5a635-120">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="5a635-121">Merhaba yüklediğinizden emin olun [Java için Azure SDK] [ Azure SDK for Java] önce bu örnek oluşturma.</span><span class="sxs-lookup"><span data-stu-id="5a635-121">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="5a635-122">Eclipse kullanıyorsanız, hello yükleyebilirsiniz [Eclipse için Azure Araç Seti] [ Azure Toolkit for Eclipse] hello Java için Azure SDK'sı içerir.</span><span class="sxs-lookup"><span data-stu-id="5a635-122">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="5a635-123">Merhaba daha sonra ekleyebilirsiniz **Java için Microsoft Azure kitaplıkları** tooyour proje:</span><span class="sxs-lookup"><span data-stu-id="5a635-123">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="5a635-124">Merhaba aşağıdakileri ekleyin `import` deyimleri toohello dosyasının üst kısmında hello Java:</span><span class="sxs-lookup"><span data-stu-id="5a635-124">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="5a635-125">Java tooyour için Hello Azure kitaplıkları yolu oluştur ve proje dağıtım derlemenizi dahil ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5a635-125">Add hello Azure Libraries for Java tooyour build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="5a635-126">Konu başlığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a635-126">Create a topic</span></span>
<span data-ttu-id="5a635-127">Service Bus konu başlıklarına yönelik yönetim işlemlerini aracılığıyla gerçekleştirilebilecek **ServiceBusContract** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5a635-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="5a635-128">A **ServiceBusContract** nesnesini izinlere toomanage ile SAS belirteci ve hello yalıtır uygun bir yapılandırma ile oluşturulan **ServiceBusContract** sınıftır hello tek nokta Azure ile iletişimi.</span><span class="sxs-lookup"><span data-stu-id="5a635-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="5a635-129">Merhaba **ServiceBusService** sınıfı yöntemleri toocreate sağlar, sıralama ve konuları silin.</span><span class="sxs-lookup"><span data-stu-id="5a635-129">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete topics.</span></span> <span data-ttu-id="5a635-130">örnekte gösterildiği nasıl aşağıdaki hello bir **ServiceBusService** nesnesi, bir konu adında kullanılan toocreate olabilir `TestTopic`, adlı bir ad alanı ile `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="5a635-130">hello following example shows how a **ServiceBusService** object can be used toocreate a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="5a635-131">Yöntemleri vardır **TopicInfo** ayarlanacak hello konu özelliklerini etkinleştirme (örneğin: tooset hello varsayılan yaşam süresi (TTL) değerini uygulanan toobe toomessages gönderilen toohello konu).</span><span class="sxs-lookup"><span data-stu-id="5a635-131">There are methods on **TopicInfo** that enable properties of hello topic to be set (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello topic).</span></span> <span data-ttu-id="5a635-132">Merhaba aşağıdaki örnekte nasıl toocreate bir konu adlı gösterir `TestTopic` maksimum 5 GB boyuta sahip:</span><span class="sxs-lookup"><span data-stu-id="5a635-132">hello following example shows how toocreate a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="5a635-133">Merhaba kullanabileceğinizi unutmayın **listTopics** yöntemi **ServiceBusContract** bir hizmet ad alanında belirtilen ada sahip bir konu zaten varsa toocheck nesneleri.</span><span class="sxs-lookup"><span data-stu-id="5a635-133">Note that you can use hello **listTopics** method on **ServiceBusContract** objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="5a635-134">Abonelikleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a635-134">Create subscriptions</span></span>
<span data-ttu-id="5a635-135">Abonelikler tootopics de hello ile oluşturulan **ServiceBusService** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5a635-135">Subscriptions tootopics are also created with hello **ServiceBusService** class.</span></span> <span data-ttu-id="5a635-136">Abonelikler adlandırılır ve hello toohello aboneliğin sanal kuyruğuna gönderilen ileti kümesini sınırlayan isteğe bağlı bir filtre içerebilir.</span><span class="sxs-lookup"><span data-stu-id="5a635-136">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="5a635-137">Merhaba varsayılan (MatchAll) filtreyle abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a635-137">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="5a635-138">Merhaba **MatchAll** yeni bir abonelik oluşturulurken filtre belirtilmeyen varsa, kullanılan hello varsayılan filtre filtredir.</span><span class="sxs-lookup"><span data-stu-id="5a635-138">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="5a635-139">Ne zaman hello **MatchAll** filtre kullanıldığında, tüm iletileri yayımlanan toohello konu aboneliğin sanal kuyruğuna yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="5a635-139">When hello **MatchAll** filter is used, all messages published toohello topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="5a635-140">Merhaba aşağıdaki örnekte "AllMessages" adlı bir abonelik oluşturur ve kullanır hello varsayılan **MatchAll** Filtresi.</span><span class="sxs-lookup"><span data-stu-id="5a635-140">hello following example creates a subscription named "AllMessages" and uses hello default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="5a635-141">Filtre içeren abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a635-141">Create subscriptions with filters</span></span>
<span data-ttu-id="5a635-142">Hangi iletilerin tooa konu içinde belirli konu aboneliği göstermelidir gönderilen tooscope sağlayan filtreler de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a635-142">You can also create filters that enable you tooscope which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="5a635-143">Merhaba en esnek filtre abonelikler tarafından desteklenen türünde [SqlFilter][SqlFilter], SQL92 alt kümesi uygular.</span><span class="sxs-lookup"><span data-stu-id="5a635-143">hello most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="5a635-144">SQL filtreleri yayımlanan toohello konu hello iletilerinin hello özelliklerini çalışır.</span><span class="sxs-lookup"><span data-stu-id="5a635-144">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="5a635-145">Merhaba SQL Filtresi ile kullanılabilen hello ifadeler hakkında daha fazla ayrıntı için gözden [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sözdizimi.</span><span class="sxs-lookup"><span data-stu-id="5a635-145">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="5a635-146">Merhaba aşağıdaki örnek adlı bir abonelik oluşturulur `HighMessages` ile bir [SqlFilter] [ SqlFilter] yalnızca özel iletileri seçen nesne **MessageNumber** özellik 3'ten büyük:</span><span class="sxs-lookup"><span data-stu-id="5a635-146">hello following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="5a635-147">Benzer şekilde, hello aşağıdaki örnek adlı bir abonelik oluşturur `LowMessages` ile bir [SqlFilter] [ SqlFilter] yalnızca sahip iletileri seçen nesnesi bir **MessageNumber** özelliği daha az veya bu değere eşit too3:</span><span class="sxs-lookup"><span data-stu-id="5a635-147">Similarly, hello following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal too3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="5a635-148">Ne zaman bir ileti artık gönderilir çok`TestTopic`, her zaman abone tooreceivers toohello teslim `AllMessages` abonelik ve abone olunan seçmeli olarak teslim tooreceivers toohello `HighMessages` ve `LowMessages` abonelikleri () ileti içeriği bağlı olarak).</span><span class="sxs-lookup"><span data-stu-id="5a635-148">When a message is now sent too`TestTopic`, it will always be delivered tooreceivers subscribed toohello `AllMessages` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="5a635-149">İletileri tooa konu gönderin</span><span class="sxs-lookup"><span data-stu-id="5a635-149">Send messages tooa topic</span></span>
<span data-ttu-id="5a635-150">toosend ileti tooa Service Bus konu, uygulamanızı alacağı bir **ServiceBusContract** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="5a635-150">toosend a message tooa Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="5a635-151">Merhaba aşağıdaki kodu gösterir nasıl toosend hello için bir ileti `TestTopic` hello içinde daha önce oluşturduğunuz konu `HowToSample` ad alanı:</span><span class="sxs-lookup"><span data-stu-id="5a635-151">hello following code demonstrates how toosend a message for hello `TestTopic` topic created previously within hello `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="5a635-152">TooService Bus konu başlıklarına gönderilen iletiler örnekleridir [BrokeredMessage] [ BrokeredMessage] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="5a635-152">Messages sent tooService Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="5a635-153">[BrokeredMessage][BrokeredMessage]* nesneler sahip bir dizi standart yöntem (gibi **setLabel** ve **TimeToLive**), kullanılan toohold özel bir sözlüğü uygulamaya özgü özellikler ve rastgele uygulama verileri gövdesi.</span><span class="sxs-lookup"><span data-stu-id="5a635-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="5a635-154">Bir uygulama herhangi bir seri hale getirilebilir nesnesi hello oluşturucusuna geçirerek ileti gövdesini hello ayarlayabilirsiniz [BrokeredMessage][BrokeredMessage]ve hello uygun **DataContractSerializer**  kullanılan tooserialize hello nesne sonra olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5a635-154">An application can set hello body of the message by passing any serializable object into hello constructor of the [BrokeredMessage][BrokeredMessage], and hello appropriate **DataContractSerializer** will then be used tooserialize hello object.</span></span> <span data-ttu-id="5a635-155">Alternatif olarak, bir **java.io.InputStream** sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="5a635-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="5a635-156">Merhaba aşağıdaki örnekte nasıl toothe toosend beş test iletisi gösteren `TestTopic` **MessageSender** biz hello kod parçacığında yukarıdaki elde.</span><span class="sxs-lookup"><span data-stu-id="5a635-156">hello following example demonstrates how toosend five test messages toothe `TestTopic` **MessageSender** we obtained in hello code snippet above.</span></span>
<span data-ttu-id="5a635-157">Not nasıl hello **MessageNumber** her ileti özelliği değeri değişir hello döngü hello yinelemesi (Bu alacak abonelikleri belirler):</span><span class="sxs-lookup"><span data-stu-id="5a635-157">Note how hello **MessageNumber** property value of each message varies on hello iteration of hello loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="5a635-158">Service Bus konu başlıklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="5a635-158">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="5a635-159">Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="5a635-159">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="5a635-160">Merhaba konu başlığında tutulan ileti sayısına bir sınır yoktur ancak konu başlığı tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="5a635-160">There is no limit on hello number of messages held in a topic but there is a limit on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="5a635-161">Bu konu başlığı boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="5a635-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-tooreceive-messages-from-a-subscription"></a><span data-ttu-id="5a635-162">Nasıl tooreceive abonelikten iletileri</span><span class="sxs-lookup"><span data-stu-id="5a635-162">How tooreceive messages from a subscription</span></span>
<span data-ttu-id="5a635-163">bir aboneliğe ilişkin tooreceive iletileri kullanan bir **ServiceBusContract** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="5a635-163">tooreceive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="5a635-164">Alınan iletiler, iki farklı modda çalışabilir: **ReceiveAndDelete** ve **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="5a635-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="5a635-165">Merhaba kullanırken **ReceiveAndDelete** modu, alma bir tek işlemi - diğer bir deyişle, Service Bus iletiye yönelik Okuma isteği aldığında, hello iletiyi kullanılıyor olarak işaretler ve toothe uygulama döndürür.</span><span class="sxs-lookup"><span data-stu-id="5a635-165">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks hello message as being consumed and returns it toothe application.</span></span> <span data-ttu-id="5a635-166">**ReceiveAndDelete** modu hello en basit modeldir ve senaryoları bir uygulama içinde tolerans bir hatanın hello Olay iletisinde işlenmiyor en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="5a635-166">**ReceiveAndDelete** mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="5a635-167">toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor.</span><span class="sxs-lookup"><span data-stu-id="5a635-167">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="5a635-168">Hizmet veri yolu ileti hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş olduğundan, onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.</span><span class="sxs-lookup"><span data-stu-id="5a635-168">Because Service Bus will have marked the message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="5a635-169">İçinde **PeekLock** modu, alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur.</span><span class="sxs-lookup"><span data-stu-id="5a635-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="5a635-170">Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur.</span><span class="sxs-lookup"><span data-stu-id="5a635-170">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="5a635-171">Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin **silmek** hello alınan ileti üzerinde.</span><span class="sxs-lookup"><span data-stu-id="5a635-171">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="5a635-172">Hizmet veri yolu hello gördüğünde **silmek** çağrısı hello iletiyi kullanılıyor olarak işaretler ve hello konusundan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5a635-172">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello topic.</span></span>

<span data-ttu-id="5a635-173">Merhaba aşağıdaki örnek nasıl ileti aldı ve işlenen kullanarak gösterir **PeekLock** (Merhaba varsayılan modu değil).</span><span class="sxs-lookup"><span data-stu-id="5a635-173">hello example below demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="5a635-174">Merhaba aşağıdaki örnek bir döngü gerçekleştirir ve hello "HighMessages" abonelik iletilerinde işler ve daha fazla ileti olduğunda çıkar (Alternatif olarak, yeni iletiler için toowait ayarlanması).</span><span class="sxs-lookup"><span data-stu-id="5a635-174">hello example below performs a loop and processes messages in hello "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set toowait for new messages).</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello topic message.
            System.out.print("From topic: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="5a635-175">Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri</span><span class="sxs-lookup"><span data-stu-id="5a635-175">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="5a635-176">Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a635-176">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="5a635-177">Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz **unlockMessage** hello alınan ileti üzerinde yöntemi (hello yerine **deleteMessage** yöntemi).</span><span class="sxs-lookup"><span data-stu-id="5a635-177">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="5a635-178">Bu hizmet veri yolu toounlock selamlama iletisine hello konusu içinde neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.</span><span class="sxs-lookup"><span data-stu-id="5a635-178">This will cause Service Bus toounlock hello message within hello topic and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="5a635-179">Ayrıca konusu içinde kilitli bir ileti ile ilişkili bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus selamlama iletisine otomatik olarak kilitlenmeden kilit zaman aşımı dolmadan ve yeniden alınan kullanılabilir toobe yapın.</span><span class="sxs-lookup"><span data-stu-id="5a635-179">There is also a timeout associated with a message locked within the topic, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="5a635-180">Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor **deleteMessage** isteği bildirilmeden sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5a635-180">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="5a635-181">Bu genellikle adlandırılır **en az bir kez işleme**, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="5a635-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="5a635-182">Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5a635-182">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="5a635-183">Bu genellikle hello kullanılarak elde edilen **getMessageId** teslimat denemelerinde hello iletisinin yöntemi.</span><span class="sxs-lookup"><span data-stu-id="5a635-183">This is often achieved using hello **getMessageId** method of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="5a635-184">Konu başlıklarını ve abonelikleri silme</span><span class="sxs-lookup"><span data-stu-id="5a635-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="5a635-185">birincil yolu toodelete konuları hello ve abonelikleri içindir toouse bir **ServiceBusContract** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="5a635-185">hello primary way toodelete topics and subscriptions is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="5a635-186">Konu başlığı silindiğinde hello konu başlığıyla kaydedilen tüm abonelikler de silinir.</span><span class="sxs-lookup"><span data-stu-id="5a635-186">Deleting a topic will also delete any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="5a635-187">Ayrıca, abonelikler bağımsız olarak da silinebilir.</span><span class="sxs-lookup"><span data-stu-id="5a635-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="5a635-188">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="5a635-188">Next Steps</span></span>
<span data-ttu-id="5a635-189">Artık Service Bus kuyruklarını hello temellerini öğrendiğinize göre bkz: [Service Bus kuyrukları, konu başlıkları ve abonelikler] [ Service Bus queues, topics, and subscriptions] daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="5a635-189">Now that you've learned hello basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
