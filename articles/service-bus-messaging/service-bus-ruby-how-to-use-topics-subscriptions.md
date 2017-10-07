---
title: "aaaHow toouse Service Bus konuları (Ruby) | Microsoft Docs"
description: "Bilgi nasıl toouse Service Bus konuları ve abonelikleri Azure. Kod örnekleri Söyleniş uygulamalarına yönelik yazılır."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="8e579-104">Nasıl toouse Service Bus konuları ve abonelikleri Ruby ile</span><span class="sxs-lookup"><span data-stu-id="8e579-104">How toouse Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="8e579-105">Bu makalede nasıl toouse Service Bus konuları ve abonelikleri Söyleniş uygulamalardan.</span><span class="sxs-lookup"><span data-stu-id="8e579-105">This article describes how toouse Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="8e579-106">Merhaba kapsanan senaryolar dahil **konuları ve Abonelikleri, ileti gönderme, abonelik filtreleri oluşturma oluşturma** tooa konu **abonelikten ileti alma**, ve  **konuları ve abonelikleri silmeyi**.</span><span class="sxs-lookup"><span data-stu-id="8e579-106">hello scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="8e579-107">Konu başlıkları ve abonelikler hakkında daha fazla bilgi için bkz: hello [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="8e579-107">For more information on topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="8e579-108">Konu başlığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8e579-108">Create a topic</span></span>
<span data-ttu-id="8e579-109">Merhaba **Azure::ServiceBusService** nesne konuları ile toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e579-109">hello **Azure::ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="8e579-110">Merhaba aşağıdaki kod oluşturur bir **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8e579-110">hello following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="8e579-111">toocreate bir konu kullanmak hello `create_topic()` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="8e579-111">toocreate a topic, use hello `create_topic()` method.</span></span> <span data-ttu-id="8e579-112">Aşağıdaki örnek hello bir konu oluşturur veya varsa hello hataları yazdırır.</span><span class="sxs-lookup"><span data-stu-id="8e579-112">hello following example creates a topic or prints out hello errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="8e579-113">Ayrıca iletebilirsiniz bir **Azure::ServiceBus::Topic** toooverride varsayılan konu ayarları ileti zaman toolive veya en büyük sıra boyutu gibi etkinleştirin ek seçeneklere sahip nesne.</span><span class="sxs-lookup"><span data-stu-id="8e579-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you toooverride default topic settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="8e579-114">Merhaba hello en büyük sıra ayarı aşağıdaki örnekte gösterildiği too5 GB boyutunu ve toolive too1 minute süresi:</span><span class="sxs-lookup"><span data-stu-id="8e579-114">hello following example shows setting hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="8e579-115">Abonelikleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="8e579-115">Create subscriptions</span></span>
<span data-ttu-id="8e579-116">Konu aboneliklerini ayrıca hello ile oluşturulan **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8e579-116">Topic subscriptions are also created with hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="8e579-117">Abonelikler adlandırılır ve hello toohello aboneliğin sanal kuyruğuna teslim edilen ileti kümesini sınırlayan isteğe bağlı bir filtre içerebilir.</span><span class="sxs-lookup"><span data-stu-id="8e579-117">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

<span data-ttu-id="8e579-118">Abonelikleri kalıcı ve tooexist ya da bunlar kadar devam eder veya hello konu bunların ilişkili silinir.</span><span class="sxs-lookup"><span data-stu-id="8e579-118">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="8e579-119">Uygulama mantığı toocreate bir abonelik içeriyorsa, ilk hello abonelik zaten hello getSubscription yöntemini kullanarak olup olmadığını denetlemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="8e579-119">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using hello getSubscription method.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="8e579-120">Merhaba varsayılan (MatchAll) filtreyle abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="8e579-120">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="8e579-121">Merhaba **MatchAll** yeni bir abonelik oluşturulurken filtre belirtilmeyen varsa, kullanılan hello varsayılan filtre filtredir.</span><span class="sxs-lookup"><span data-stu-id="8e579-121">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="8e579-122">Ne zaman hello **MatchAll** filtre kullanıldığında, tüm iletileri yayımlanan toohello konu hello aboneliğin sanal kuyruğuna yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8e579-122">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="8e579-123">Merhaba aşağıdaki örnekte "tüm iletileri" adlı bir abonelik oluşturur ve kullanır hello varsayılan **MatchAll** Filtresi.</span><span class="sxs-lookup"><span data-stu-id="8e579-123">hello following example creates a subscription named "all-messages" and uses hello default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="8e579-124">Filtre içeren abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="8e579-124">Create subscriptions with filters</span></span>
<span data-ttu-id="8e579-125">Ayrıca hangi iletilerin tooa konu içinde belirli bir aboneliği göstermelidir gönderilen toospecify etkinleştirmek filtreleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8e579-125">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific subscription.</span></span>

<span data-ttu-id="8e579-126">Merhaba en esnek filtre abonelikler tarafından desteklenen hello türünde **Azure::ServiceBus::SqlFilter**, SQL92 alt kümesi uygular.</span><span class="sxs-lookup"><span data-stu-id="8e579-126">hello most flexible type of filter supported by subscriptions is hello **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="8e579-127">SQL filtreleri yayımlanan toohello konu hello iletilerinin hello özelliklerini çalışır.</span><span class="sxs-lookup"><span data-stu-id="8e579-127">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="8e579-128">Merhaba SQL Filtresi ile kullanılabilen hello ifadeler hakkında daha fazla ayrıntı için gözden [SqlFilter](service-bus-messaging-sql-filter.md) sözdizimi.</span><span class="sxs-lookup"><span data-stu-id="8e579-128">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="8e579-129">Hello kullanarak filtreleri tooa aboneliğiniz ekleyebilirsiniz `create_rule()` hello yöntemi **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8e579-129">You can add filters tooa subscription by using hello `create_rule()` method of hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="8e579-130">Bu yöntem tooadd yeni filtreleri tooan varolan abonelik sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e579-130">This method enables you tooadd new filters tooan existing subscription.</span></span>

<span data-ttu-id="8e579-131">Merhaba varsayılan filtre otomatik olarak uygulanan bu yana tooall yeni abonelikler, ilk hello varsayılan filtresini kaldırın veya gerekir hello **MatchAll** belirttiğiniz diğer filtreleri geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="8e579-131">Since hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter, or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="8e579-132">Hello kullanarak hello varsayılan kural kaldırabilirsiniz `delete_rule()` hello yöntemi **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8e579-132">You can remove hello default rule by using hello `delete_rule()` method on hello **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="8e579-133">Merhaba aşağıdaki örnekte "iletileri yüksek" adında bir abonelik oluşturur bir **Azure::ServiceBus::SqlFilter** özel iletileri yalnızca seçer `message_number` özelliği 3'ten büyük:</span><span class="sxs-lookup"><span data-stu-id="8e579-133">hello following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="8e579-134">Benzer şekilde, hello aşağıdaki örnek adlı bir abonelik oluşturur `low-messages` ile bir **Azure::ServiceBus::SqlFilter** olan iletiler yalnızca seçer bir `message_number` özelliği daha az veya bu değere eşit too3:</span><span class="sxs-lookup"><span data-stu-id="8e579-134">Similarly, hello following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal too3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="8e579-135">Ne zaman bir ileti artık gönderilir çok`test-topic`, her zaman abone teslim tooreceivers toohello olacak olan `all-messages` konu aboneliği ve abone olunan seçmeli olarak teslim tooreceivers toohello `high-messages` ve `low-messages` konu abonelikleri () Merhaba ileti içeriği bağlı olarak).</span><span class="sxs-lookup"><span data-stu-id="8e579-135">When a message is now sent too`test-topic`, it is always be delivered tooreceivers subscribed toohello `all-messages` topic subscription, and selectively delivered tooreceivers subscribed toohello `high-messages` and `low-messages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="8e579-136">İletileri tooa konu gönderin</span><span class="sxs-lookup"><span data-stu-id="8e579-136">Send messages tooa topic</span></span>
<span data-ttu-id="8e579-137">toosend ileti tooa Service Bus konu, uygulamanızı hello kullanmalıdır `send_topic_message()` hello yöntemi **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8e579-137">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="8e579-138">İletileri gönderilir tooService veri yolu konuları hello örneklerini **Azure::ServiceBus::BrokeredMessage** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="8e579-138">Messages sent tooService Bus topics are instances of hello **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="8e579-139">**Azure::ServiceBus::BrokeredMessage** nesneleri olan bir standart özellikler kümesi (gibi `label` ve `time_to_live`), kullanılan toohold özel uygulamaya özgü özellikler sözlüğü bir ve dize verileri gövdesi içerir.</span><span class="sxs-lookup"><span data-stu-id="8e579-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="8e579-140">Bir uygulama bir dize değeri toohello geçirerek hello hello ileti gövdesini ayarlayabilir `send_topic_message()` yöntemi ve tüm gerekli standart özellikleri varsayılan değerlerle doldurulmuş.</span><span class="sxs-lookup"><span data-stu-id="8e579-140">An application can set hello body of hello message by passing a string value toohello `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="8e579-141">Merhaba aşağıdaki örnekte nasıl toosend beş test çok iletileri gösterir`test-topic`.</span><span class="sxs-lookup"><span data-stu-id="8e579-141">hello following example demonstrates how toosend five test messages too`test-topic`.</span></span> <span data-ttu-id="8e579-142">Bu hello Not `message_number` özel özellik değerini her iletinin hello döngü hello yinelemesi değişir (Bu abonelik aldığı belirler):</span><span class="sxs-lookup"><span data-stu-id="8e579-142">Note that hello `message_number` custom property value of each message varies on hello iteration of hello loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="8e579-143">Service Bus konu başlıklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="8e579-143">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="8e579-144">Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="8e579-144">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="8e579-145">Merhaba konu başlığında tutulan ileti sayısına bir sınır yoktur ancak konu başlığı tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="8e579-145">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="8e579-146">Bu konu başlığı boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="8e579-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="8e579-147">Abonelikten ileti alma</span><span class="sxs-lookup"><span data-stu-id="8e579-147">Receive messages from a subscription</span></span>
<span data-ttu-id="8e579-148">İletileri hello kullanarak bir abonelikten alınan `receive_subscription_message()` hello yöntemi **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8e579-148">Messages are received from a subscription using hello `receive_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="8e579-149">Varsayılan olarak, iletiler read(peak) ve hello abonelikten silmeden kilitli.</span><span class="sxs-lookup"><span data-stu-id="8e579-149">By default, messages are read(peak) and locked without deleting it from hello subscription.</span></span> <span data-ttu-id="8e579-150">Okuma ve ayarlama hello tarafından hello abonelikten selamlama iletisine silmek `peek_lock` çok seçenek**false**.</span><span class="sxs-lookup"><span data-stu-id="8e579-150">You can read and delete hello message from hello subscription by setting hello `peek_lock` option too**false**.</span></span>

<span data-ttu-id="8e579-151">Merhaba varsayılan davranışı okumak ve ayrıca, iletilere olası toosupport uygulamaları kılar bir iki aşamalı işlemi silme hello yapar.</span><span class="sxs-lookup"><span data-stu-id="8e579-151">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="8e579-152">Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur.</span><span class="sxs-lookup"><span data-stu-id="8e579-152">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="8e579-153">Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin `delete_subscription_message()` yöntemi ve parametre olarak silinmiş hello ileti toobe sağlama.</span><span class="sxs-lookup"><span data-stu-id="8e579-153">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_subscription_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="8e579-154">Merhaba `delete_subscription_message()` yöntemi hello iletiyi kullanılıyor olarak işaretler ve hello abonelikten Kaldır.</span><span class="sxs-lookup"><span data-stu-id="8e579-154">hello `delete_subscription_message()` method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="8e579-155">Merhaba, `:peek_lock` parametresi çok ayarlanırsa**yanlış**, okuma ve hello iletisi siliniyor hello basit model olur ve senaryoları bir uygulama içinde tolerans hello olayı içinde ileti işlenirken değil en iyi şekilde çalışır bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="8e579-155">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="8e579-156">toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor.</span><span class="sxs-lookup"><span data-stu-id="8e579-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="8e579-157">Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.</span><span class="sxs-lookup"><span data-stu-id="8e579-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="8e579-158">Merhaba aşağıdaki örnekte nasıl iletilerin alındığını ve işlenen kullanarak gösteren `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="8e579-158">hello following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="8e579-159">Merhaba örneği ilk alır ve bir ileti hello siler `low-messages` kullanarak abonelik `:peek_lock` çok ayarlamak**false**, hello başka bir ileti alır sonra `high-messages` ve ardından iletiyi kullanarak siler hello `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="8e579-159">hello example first receives and deletes a message from hello `low-messages` subscription by using `:peek_lock` set too**false**, then it receives another message from hello `high-messages` and then deletes hello message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="8e579-160">Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri</span><span class="sxs-lookup"><span data-stu-id="8e579-160">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="8e579-161">Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar.</span><span class="sxs-lookup"><span data-stu-id="8e579-161">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="8e579-162">Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlock_subscription_message()` hello yöntemi **Azure::ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="8e579-162">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="8e579-163">Hizmet veri yolu toounlock hello hello aboneliğin ileti gönderme ve yeniden alınan kullanılabilir toobe olun Bu nedenler ya da göre hello aynı uygulama veya başka bir kullanıcı uygulama tarafından kullanma.</span><span class="sxs-lookup"><span data-stu-id="8e579-163">This causes Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="8e579-164">Ayrıca hello abonelikte kilitlenen iletiye ilişkin bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus selamlama iletisine kilidini hello kilit zaman aşımı dolmadan otomatik olarak yeniden alınan kullanılabilir toobe olun.</span><span class="sxs-lookup"><span data-stu-id="8e579-164">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="8e579-165">Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `delete_subscription_message()` yöntemi çağrıldıktan sonra hello ileti yeniden teslim toohello uygulama başlatıldığında içindir.</span><span class="sxs-lookup"><span data-stu-id="8e579-165">In hello event that hello application crashes after processing hello message but before hello `delete_subscription_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="8e579-166">Bu genellikle adlandırılır *en az bir kez işleme*; diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="8e579-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="8e579-167">Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8e579-167">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="8e579-168">Bu mantık, genellikle hello kullanılarak gerçekleştirilir `message_id` teslimat denemelerinde hello iletinin özelliği.</span><span class="sxs-lookup"><span data-stu-id="8e579-168">This logic is often achieved using hello `message_id` property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="8e579-169">Konu başlıklarını ve abonelikleri silme</span><span class="sxs-lookup"><span data-stu-id="8e579-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="8e579-170">Konu başlıkları ve abonelikler kalıcıdır ve açıkça olmalıdır hello aracılığıyla ya da silinmiş [Azure portal] [ Azure portal] veya program aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="8e579-170">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="8e579-171">Aşağıdaki örnek Hello gösterir nasıl toodelete hello konu adlı `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="8e579-171">hello example below demonstrates how toodelete hello topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="8e579-172">Bir konu başlığı silindiğinde hello konu başlığıyla kaydedilen tüm abonelikleri siler.</span><span class="sxs-lookup"><span data-stu-id="8e579-172">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="8e579-173">Ayrıca, abonelikler bağımsız olarak da silinebilir.</span><span class="sxs-lookup"><span data-stu-id="8e579-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="8e579-174">Merhaba aşağıdaki kodu nasıl toodelete hello abonelik adlı gösterir `high-messages` hello gelen `test-topic` konu:</span><span class="sxs-lookup"><span data-stu-id="8e579-174">hello following code demonstrates how toodelete hello subscription named `high-messages` from hello `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="8e579-175">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8e579-175">Next steps</span></span>
<span data-ttu-id="8e579-176">Artık Service Bus konu başlıklarını hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="8e579-176">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="8e579-177">Bkz: [kuyruklar, konu başlıkları ve abonelikler](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="8e579-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="8e579-178">[SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter) için API başvurusu</span><span class="sxs-lookup"><span data-stu-id="8e579-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="8e579-179">Merhaba ziyaret [Ruby için Azure SDK](https://github.com/Azure/azure-sdk-for-ruby) github'daki.</span><span class="sxs-lookup"><span data-stu-id="8e579-179">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
