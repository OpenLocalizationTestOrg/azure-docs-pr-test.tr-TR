---
title: "Java ile Azure Service Bus konu başlıklarını kullanma | Microsoft Docs"
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
ms.openlocfilehash: b561d6fdcf4fb2839908ac8f53832fb0830dd576
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-java"></a><span data-ttu-id="3a05f-103">Service Bus konuları ve abonelikleri Java ile kullanma</span><span class="sxs-lookup"><span data-stu-id="3a05f-103">How to use Service Bus topics and subscriptions with Java</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="3a05f-104">Bu kılavuz, Service Bus konu başlıklarını ve aboneliklerini kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="3a05f-104">This guide describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="3a05f-105">Java ve kullanım örnekleri yazılır [Java için Azure SDK][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="3a05f-105">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="3a05f-106">Kapsamdaki senaryolar dahil **konuları ve abonelikleri oluşturma**, **abonelik filtreleri oluşturma**, **konu başlığına ileti gönderme**, **abonelikten ileti alma**, ve **konuları ve abonelikleri silmeyi**.</span><span class="sxs-lookup"><span data-stu-id="3a05f-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

## <a name="what-are-service-bus-topics-and-subscriptions"></a><span data-ttu-id="3a05f-107">Service Bus konuları ve abonelikleri nelerdir?</span><span class="sxs-lookup"><span data-stu-id="3a05f-107">What are Service Bus topics and subscriptions?</span></span>
<span data-ttu-id="3a05f-108">Service Bus konuları ve abonelikleri *publish/subscribe* mesajlaşma iletişim modelini destekler.</span><span class="sxs-lookup"><span data-stu-id="3a05f-108">Service Bus topics and subscriptions support a *publish/subscribe* messaging communication model.</span></span> <span data-ttu-id="3a05f-109">Konular ve abonelikler kullanıldığında, dağıtılmış uygulamanın bileşenleri birbirleriyle doğrudan iletişim kurmazlar; bunun yerine bir aracı gibi davranan bir konu aracılığıyla iletileri değiş tokuş eder.</span><span class="sxs-lookup"><span data-stu-id="3a05f-109">When using topics and subscriptions, components of a distributed application do not communicate directly with each other; instead they exchange messages via a topic, which acts as an intermediary.</span></span>

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

<span data-ttu-id="3a05f-111">Service Bus kuyruklarının tersine, burada her ileti bir tüketici tarafından işlenir; konular ve abonelikler, publish/subscribe modelini kullanarak iletişimin "bir-çok" biçimini sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a05f-111">In contrast with Service Bus queues, in which each message is processed by a single consumer, topics and subscriptions provide a "one-to-many" form of communication, using a publish/subscribe pattern.</span></span> <span data-ttu-id="3a05f-112">Bir konuya birden fazla abonelik kaydedilebilir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-112">It is possible to register multiple subscriptions to a topic.</span></span> <span data-ttu-id="3a05f-113">Bir konuya ileti gönderildiğinde, bundan sonra, bağımsız olarak ele almak/işlemek amacıyla her abonelik için kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-113">When a message is sent to a topic, it is then made available to each subscription to handle/process independently.</span></span>

<span data-ttu-id="3a05f-114">Bir konuya abone olunması, konuya gönderilmiş olan iletilerin kopyaların alan sanal kuyruğa benzer.</span><span class="sxs-lookup"><span data-stu-id="3a05f-114">A subscription to a topic resembles a virtual queue that receives copies of the messages that were sent to the topic.</span></span> <span data-ttu-id="3a05f-115">İsteğe bağlı olarak, filtre kuralları konuyla ilgili filtre/bir konunun hangi iletileri hangi konu abonelikleriyle kısıtlamanızı olanak tanıyan bir abonelik başına temelinde kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a05f-115">You can optionally register filter rules for a topic on a per-subscription basis, which allows you to filter/restrict which messages to a topic are received by which topic subscriptions.</span></span>

<span data-ttu-id="3a05f-116">Service Bus konuları ve Abonelikleri, çok sayıda kullanıcılar ve uygulamalar arasında çok çok sayıda iletileri işlemek için ölçeklendirmek etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3a05f-116">Service Bus topics and subscriptions enable you to scale to process a very large number of messages across a very large number of users and applications.</span></span>

## <a name="create-a-service-namespace"></a><span data-ttu-id="3a05f-117">Hizmet ad alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a05f-117">Create a service namespace</span></span>
<span data-ttu-id="3a05f-118">Azure'da Service Bus konu başlıklarını ve aboneliklerini kullanmaya başlamak için önce uygulamanızın Service Bus kaynaklarını adreslemek için kapsam bir kapsayıcı sağlar bir ad alanı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-118">To begin using Service Bus topics and subscriptions in Azure, you must first create a namespace, which provides a scoping container for addressing Service Bus resources within your application.</span></span>

<span data-ttu-id="3a05f-119">Ad alanı oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="3a05f-119">To create a namespace:</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="3a05f-120">Service Bus hizmetini kullanmak için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="3a05f-120">Configure your application to use Service Bus</span></span>
<span data-ttu-id="3a05f-121">Yüklediğinizden emin olun [Java için Azure SDK] [ Azure SDK for Java] önce bu örnek oluşturma.</span><span class="sxs-lookup"><span data-stu-id="3a05f-121">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="3a05f-122">Eclipse kullanıyorsanız, yükleyebileceğiniz [Eclipse için Azure Araç Seti] [ Azure Toolkit for Eclipse] Java için Azure SDK'sı içerir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-122">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="3a05f-123">Daha sonra ekleyebilirsiniz **Java için Microsoft Azure kitaplıkları** projenize:</span><span class="sxs-lookup"><span data-stu-id="3a05f-123">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

<span data-ttu-id="3a05f-124">Aşağıdakileri ekleyin `import` deyimlerini Java dosyanın en üstüne ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3a05f-124">Add the following `import` statements to the top of the Java file:</span></span>

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

<span data-ttu-id="3a05f-125">Java için Azure kitaplıkları, yapı yoluna ekleyin ve proje dağıtım derlemenizi içerir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-125">Add the Azure Libraries for Java to your build path and include it in your project deployment assembly.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="3a05f-126">Konu başlığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a05f-126">Create a topic</span></span>
<span data-ttu-id="3a05f-127">Service Bus konu başlıklarına yönelik yönetim işlemlerini aracılığıyla gerçekleştirilebilecek **ServiceBusContract** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3a05f-127">Management operations for Service Bus topics can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="3a05f-128">A **ServiceBusContract** nesnesi, yönetmek için gerekli izinlere sahip SAS belirteci yalıtır uygun bir yapılandırma ile oluşturulur ve **ServiceBusContract** sınıfı Azure ile iletişimin tek noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="3a05f-128">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="3a05f-129">**ServiceBusService** sınıfı oluşturmak, numaralandırır ve konuları silmek için yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a05f-129">The **ServiceBusService** class provides methods to create, enumerate, and delete topics.</span></span> <span data-ttu-id="3a05f-130">Aşağıdaki örnekte gösterildiği nasıl bir **ServiceBusService** nesnesi, adlandırılan bir konu oluşturmak için kullanılabilir `TestTopic`, adlı bir ad alanı ile `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="3a05f-130">The following example shows how a **ServiceBusService** object can be used to create a topic named `TestTopic`, with a namespace called `HowToSample`:</span></span>

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

<span data-ttu-id="3a05f-131">Yöntemleri vardır **TopicInfo** ayarlanacak konunun özelliklerini etkinleştirme (örneğin: konu başlığına gönderilen iletilere uygulanacak varsayılan yaşam süresi (TTL) değerini ayarlamak için).</span><span class="sxs-lookup"><span data-stu-id="3a05f-131">There are methods on **TopicInfo** that enable properties of the topic to be set (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the topic).</span></span> <span data-ttu-id="3a05f-132">Aşağıdaki örnek adlı bir konu oluşturun gösterilmektedir `TestTopic` maksimum 5 GB boyuta sahip:</span><span class="sxs-lookup"><span data-stu-id="3a05f-132">The following example shows how to create a topic named `TestTopic` with a maximum size of 5 GB:</span></span>

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

<span data-ttu-id="3a05f-133">Kullanabileceğiniz Not **listTopics** yöntemi **ServiceBusContract** nesneleri zaten bir hizmet ad alanında belirtilen ada sahip bir konu var olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="3a05f-133">Note that you can use the **listTopics** method on **ServiceBusContract** objects to check if a topic with a specified name already exists within a service namespace.</span></span>

## <a name="create-subscriptions"></a><span data-ttu-id="3a05f-134">Abonelikleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a05f-134">Create subscriptions</span></span>
<span data-ttu-id="3a05f-135">Konular için abonelikleri ile de oluşturulur **ServiceBusService** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3a05f-135">Subscriptions to topics are also created with the **ServiceBusService** class.</span></span> <span data-ttu-id="3a05f-136">Abonelikler adlandırılır ve aboneliğin sanal kuyruğuna gönderilen ileti kümesini sınırlayan isteğe bağlı bir filtre içerebilir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-136">Subscriptions are named and can have an optional filter that restricts the set of messages passed to the subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="3a05f-137">Varsayılan (MatchAll) filtreyle abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a05f-137">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="3a05f-138">**MatchAll** filtresi, yeni bir abonelik oluşturulurken filtre belirtilmeyen durumlarda kullanılan varsayılan filtredir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-138">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="3a05f-139">Zaman **MatchAll** filtre kullanıldığında, konu başlığında yayımlanan tüm iletiler aboneliğin sanal kuyruğuna yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-139">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="3a05f-140">Aşağıdaki örnekte "AllMessages" adlı bir abonelik oluşturulur ve varsayılan **MatchAll** filtresi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3a05f-140">The following example creates a subscription named "AllMessages" and uses the default **MatchAll** filter.</span></span>

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="3a05f-141">Filtre içeren abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="3a05f-141">Create subscriptions with filters</span></span>
<span data-ttu-id="3a05f-142">Bir konu başlığına gönderilen iletileri içinde belirli konu aboneliği göstermelidir kapsamına sağlayan filtreler de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3a05f-142">You can also create filters that enable you to scope which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="3a05f-143">Filtre abonelikler tarafından desteklenen en esnek türü [SqlFilter][SqlFilter], SQL92 alt kümesi uygular.</span><span class="sxs-lookup"><span data-stu-id="3a05f-143">The most flexible type of filter supported by subscriptions is the [SqlFilter][SqlFilter], which implements a subset of SQL92.</span></span> <span data-ttu-id="3a05f-144">SQL filtreleri, konu başlığında yayımlanan iletilerin özelliklerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="3a05f-144">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="3a05f-145">SQL Filtresi ile kullanılabilen ifadeler hakkında daha fazla ayrıntı için gözden [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sözdizimi.</span><span class="sxs-lookup"><span data-stu-id="3a05f-145">For more details about the expressions that can be used with a SQL filter, review the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="3a05f-146">Aşağıdaki örnek adlı bir abonelik oluşturur `HighMessages` ile bir [SqlFilter] [ SqlFilter] yalnızca özel iletileri seçen nesne **MessageNumber** özelliği 3'ten büyük:</span><span class="sxs-lookup"><span data-stu-id="3a05f-146">The following example creates a subscription named `HighMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a custom **MessageNumber** property greater than 3:</span></span>

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

<span data-ttu-id="3a05f-147">Benzer şekilde, aşağıdaki örnekte adlı bir abonelik oluşturulur `LowMessages` ile bir [SqlFilter] [ SqlFilter] yalnızca sahip iletileri seçen nesnesi bir **MessageNumber** özelliğine daha az veya bu değere eşit 3:</span><span class="sxs-lookup"><span data-stu-id="3a05f-147">Similarly, the following example creates a subscription named `LowMessages` with a [SqlFilter][SqlFilter] object that only selects messages that have a **MessageNumber** property less than or equal to 3:</span></span>

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete the default rule, otherwise the new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

<span data-ttu-id="3a05f-148">Ne zaman bir ileti artık gönderildi `TestTopic`, bu her zaman alıcılara teslim edilecek `AllMessages` aboneliği ve alıcılara teslim seçmeli olarak `HighMessages` ve `LowMessages` abonelikleri (ileti içeriği bağlı olarak).</span><span class="sxs-lookup"><span data-stu-id="3a05f-148">When a message is now sent to `TestTopic`, it will always be delivered to receivers subscribed to the `AllMessages` subscription, and selectively delivered to receivers subscribed to the `HighMessages` and `LowMessages` subscriptions (depending upon the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="3a05f-149">Konu başlığına ileti gönderme</span><span class="sxs-lookup"><span data-stu-id="3a05f-149">Send messages to a topic</span></span>
<span data-ttu-id="3a05f-150">Service Bus konu başlığına bir ileti göndermek için uygulamanızı alacağı bir **ServiceBusContract** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3a05f-150">To send a message to a Service Bus topic, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="3a05f-151">Aşağıdaki kodda bir ileti göndermeye gösterilmiştir `TestTopic` konu içinde daha önce oluşturduğunuz `HowToSample` ad alanı:</span><span class="sxs-lookup"><span data-stu-id="3a05f-151">The following code demonstrates how to send a message for the `TestTopic` topic created previously within the `HowToSample` namespace:</span></span>

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

<span data-ttu-id="3a05f-152">Service Bus konu başlıklarına gönderilen iletiler örnekleridir [BrokeredMessage] [ BrokeredMessage] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3a05f-152">Messages sent to Service Bus Topics are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="3a05f-153">[BrokeredMessage][BrokeredMessage]* nesneler sahip bir dizi standart yöntem (gibi **setLabel** ve **TimeToLive**), bir uygulamaya özgü özel özellikleri tutmak için kullanılan bir sözlük ve rastgele uygulama verileri gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-153">[BrokeredMessage][BrokeredMessage]* objects have a set of standard methods (such as **setLabel** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="3a05f-154">Bir uygulama herhangi bir seri hale getirilebilir nesne oluşturucusuna geçirerek ileti gövdesini ayarlayabilir [BrokeredMessage][BrokeredMessage]ve uygun **DataContractSerializer** daha sonra nesneyi serileştirmek için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="3a05f-154">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate **DataContractSerializer** will then be used to serialize the object.</span></span> <span data-ttu-id="3a05f-155">Alternatif olarak, bir **java.io.InputStream** sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-155">Alternatively, a **java.io.InputStream** can be provided.</span></span>

<span data-ttu-id="3a05f-156">Aşağıdaki örnekte nasıl beş test iletisi göndereceğinizi gösterir `TestTopic` **MessageSender** biz Yukarıdaki kod parçacığında elde.</span><span class="sxs-lookup"><span data-stu-id="3a05f-156">The following example demonstrates how to send five test messages to the `TestTopic` **MessageSender** we obtained in the code snippet above.</span></span>
<span data-ttu-id="3a05f-157">Not nasıl **MessageNumber** özellik değeri her iletinin tekrarına döngü üzerinde (Bu alacak abonelikleri belirler):</span><span class="sxs-lookup"><span data-stu-id="3a05f-157">Note how the **MessageNumber** property value of each message varies on the iteration of the loop (this will determine which subscriptions receive it):</span></span>

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for the body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message to the topic
service.sendTopicMessage("TestTopic", message);
}
```

<span data-ttu-id="3a05f-158">Service Bus konu başlıkları, [Standart katmanda](service-bus-premium-messaging.md) maksimum 256 KB ve [Premium katmanda](service-bus-premium-messaging.md) maksimum 1 MB ileti boyutunu destekler.</span><span class="sxs-lookup"><span data-stu-id="3a05f-158">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="3a05f-159">Standart ve özel uygulama özelliklerini içeren üst bilginin maksimum dosya boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-159">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="3a05f-160">Bir konu başlığında tutulan ileti sayısına bir sınır yoktur ancak konu başlığı tarafından tutulan iletilerin toplam boyutu bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="3a05f-160">There is no limit on the number of messages held in a topic but there is a limit on the total size of the messages held by a topic.</span></span> <span data-ttu-id="3a05f-161">Bu konu başlığı boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-161">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="how-to-receive-messages-from-a-subscription"></a><span data-ttu-id="3a05f-162">Abonelikten ileti alma</span><span class="sxs-lookup"><span data-stu-id="3a05f-162">How to receive messages from a subscription</span></span>
<span data-ttu-id="3a05f-163">Abonelikten ileti almak için kullandığınız bir **ServiceBusContract** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3a05f-163">To receive messages from a subscription, use a **ServiceBusContract** object.</span></span> <span data-ttu-id="3a05f-164">Alınan iletiler, iki farklı modda çalışabilir: **ReceiveAndDelete** ve **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="3a05f-164">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="3a05f-165">Kullanırken **ReceiveAndDelete** modu, alma bir tek işlemi - diğer bir deyişle, Service Bus iletiye yönelik Okuma isteği aldığında, iletiyi kullanılıyor olarak işaretler ve uygulamaya döndürür.</span><span class="sxs-lookup"><span data-stu-id="3a05f-165">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="3a05f-166">**ReceiveAndDelete** modu, en basit modeldir ve uygulamanın hata oluştuğunda bir iletinin işlenmemesine izin verebileceği senaryolarda en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="3a05f-166">**ReceiveAndDelete** mode is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="3a05f-167">Bu durumu daha iyi anlamak için müşterinin bir alma isteği bildirdiğini ve bu isteğin işlenmeden çöktüğünü varsayın.</span><span class="sxs-lookup"><span data-stu-id="3a05f-167">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="3a05f-168">Service Bus iletiyi kullanılıyor olarak işaretlenmiş nedeniyle uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında, sonra da çökmenin öncesinde kullanılan iletiyi atlamış olur.</span><span class="sxs-lookup"><span data-stu-id="3a05f-168">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="3a05f-169">İçinde **PeekLock** modu, alma, iletilere veremeyen uygulamaları desteklemenin mümkün kılar bir iki aşamalı işlemi olur.</span><span class="sxs-lookup"><span data-stu-id="3a05f-169">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="3a05f-170">Service Bus bir istek aldığında bir sonraki kullanılacak iletiyi bulur, diğer tüketicilerin bu iletiyi almasını engellemek için kilitler ve ardından uygulamaya döndürür.</span><span class="sxs-lookup"><span data-stu-id="3a05f-170">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="3a05f-171">Uygulama iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), çağırarak alma işleminin ikinci aşamasını tamamlar **silmek** alınan iletide.</span><span class="sxs-lookup"><span data-stu-id="3a05f-171">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="3a05f-172">Hizmet veri yolu gördüğünde **silmek** çağrısı iletiyi kullanılıyor olarak işaretler ve konusundan kaldırın.</span><span class="sxs-lookup"><span data-stu-id="3a05f-172">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the topic.</span></span>

<span data-ttu-id="3a05f-173">Aşağıdaki örnek nasıl ileti aldı ve işlenen kullanarak gösterir **PeekLock** modu (varsayılan mod değil).</span><span class="sxs-lookup"><span data-stu-id="3a05f-173">The example below demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="3a05f-174">Aşağıdaki örnek bir döngü gerçekleştirir ve "HighMessages" Abonelikteki iletileri işler ve daha fazla ileti olduğunda çıkar (Alternatif olarak, yeni iletiler için beklenecek ayarlanması).</span><span class="sxs-lookup"><span data-stu-id="3a05f-174">The example below performs a loop and processes messages in the "HighMessages" subscription and then exits when there are no more messages (alternatively, it could be set to wait for new messages).</span></span>

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
            // Display the topic message.
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
            // Added to handle no more messages.
            // Could instead wait for more messages to be added.
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="3a05f-175">Uygulama çökmelerini ve okunmayan iletileri giderme</span><span class="sxs-lookup"><span data-stu-id="3a05f-175">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="3a05f-176">Service Bus, uygulamanızda gerçekleşen hataları veya ileti işlenirken oluşan zorlukları rahat bir şekilde ortadan kaldırmanıza yardımcı olmak için işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="3a05f-176">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="3a05f-177">Alıcı uygulamanın iletiyi herhangi bir nedenden dolayı işleyemedi sonra işleyememesi **unlockMessage** alınan iletide yöntemi (yerine **deleteMessage** yöntemi).</span><span class="sxs-lookup"><span data-stu-id="3a05f-177">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="3a05f-178">Bu konu içinde ileti kilidini açmak ve aynı kullanıcı uygulama tarafından veya başka bir kullanıcı uygulama tarafından tekrar alınabilir kullanılabilir hale getirmek Service Bus neden olur.</span><span class="sxs-lookup"><span data-stu-id="3a05f-178">This will cause Service Bus to unlock the message within the topic and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="3a05f-179">Ayrıca konusu içinde kilitli bir ileti ile ilişkili bir zaman aşımı vardır ve uygulama önce iletiyi işleyemezse (örneğin, uygulama çökerse) hizmet veri yolu ileti otomatik olarak kilidini açmasına ve tekrar alınabilir hale kilit zaman aşımı dolmadan.</span><span class="sxs-lookup"><span data-stu-id="3a05f-179">There is also a timeout associated with a message locked within the topic, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="3a05f-180">Uygulama iletiyi ancak önce çökmesi durumunda, **deleteMessage** isteği bildirilmeden, sonra yeniden başlatıldığında ileti uygulamaya tekrar teslim edilir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-180">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="3a05f-181">Bu genellikle adlandırılır **en az bir kez işleme**, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="3a05f-181">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="3a05f-182">Senaryo yinelenen işlemeyi kabul etmiyorsa yinelenen ileti teslimine izin vermek için uygulama geliştiricilerin uygulamaya ilave bir mantık eklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-182">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="3a05f-183">Bu genellikle kullanılarak elde edilen **getMessageId** yöntemi iletinin teslimat denemelerinde.</span><span class="sxs-lookup"><span data-stu-id="3a05f-183">This is often achieved using the **getMessageId** method of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="3a05f-184">Konu başlıklarını ve abonelikleri silme</span><span class="sxs-lookup"><span data-stu-id="3a05f-184">Delete topics and subscriptions</span></span>
<span data-ttu-id="3a05f-185">Konuları ve abonelikleri silmek için birincil yolu bir **ServiceBusContract** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="3a05f-185">The primary way to delete topics and subscriptions is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="3a05f-186">Konu başlığı silindiğinde konu başlığıyla kaydedilen tüm abonelikler de silinir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-186">Deleting a topic will also delete any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="3a05f-187">Ayrıca, abonelikler bağımsız olarak da silinebilir.</span><span class="sxs-lookup"><span data-stu-id="3a05f-187">Subscriptions can also be deleted independently.</span></span>

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a><span data-ttu-id="3a05f-188">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="3a05f-188">Next Steps</span></span>
<span data-ttu-id="3a05f-189">Service Bus kuyruklarına öğrendiğinize göre bkz: [Service Bus kuyrukları, konu başlıkları ve abonelikler] [ Service Bus queues, topics, and subscriptions] daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="3a05f-189">Now that you've learned the basics of Service Bus queues, see [Service Bus queues, topics, and subscriptions][Service Bus queues, topics, and subscriptions] for more information.</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
