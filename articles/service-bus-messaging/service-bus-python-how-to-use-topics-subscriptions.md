---
title: "Python ile aaaHow toouse Azure Service Bus konularını | Microsoft Docs"
description: "Bilgi nasıl toouse Azure Service Bus konuları ve abonelikleri python'dan."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="7c548-103">Nasıl toouse Service Bus konuları ve abonelikleri Python ile</span><span class="sxs-lookup"><span data-stu-id="7c548-103">How toouse Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="7c548-104">Bu makalede nasıl toouse Service Bus konuları ve abonelikleri.</span><span class="sxs-lookup"><span data-stu-id="7c548-104">This article describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="7c548-105">Merhaba örnekleri Python içinde yazılmış ve hello kullan [Azure Python SDK paketi][Azure Python package].</span><span class="sxs-lookup"><span data-stu-id="7c548-105">hello samples are written in Python and use hello [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="7c548-106">Merhaba kapsanan senaryolar dahil **konuları ve abonelikleri oluşturma**, **abonelik filtreleri oluşturma**, **iletileri tooa konu gönderme**, **alma bir abonelik iletilerden**, ve **konuları ve abonelikleri silmeyi**.</span><span class="sxs-lookup"><span data-stu-id="7c548-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="7c548-107">Merhaba konu başlıkları ve abonelikler hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="7c548-107">For more information about topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="7c548-108">Tooinstall Python veya hello gereksinim duyarsanız [Azure Python paket][Azure Python package], hello bkz [Python Yükleme Kılavuzu'na](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="7c548-108">If you need tooinstall Python or hello [Azure Python package][Azure Python package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="7c548-109">Konu başlığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c548-109">Create a topic</span></span>
<span data-ttu-id="7c548-110">Merhaba **ServiceBusService** nesne konuları ile toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c548-110">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="7c548-111">Tooprogrammatically erişim Service Bus istediğiniz herhangi bir Python dosyasının kaydedileceği hello üstüne yakın Hello aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7c548-111">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="7c548-112">Merhaba aşağıdaki kod oluşturur bir **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7c548-112">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="7c548-113">Değiştir `mynamespace`, `sharedaccesskeyname`, ve `sharedaccesskey` ile gerçek ad alanınız, paylaşılan erişim imzası (SAS) anahtar adını ve anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="7c548-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="7c548-114">Hello hello değerleri hello SAS anahtar adını ve değeri elde [Azure portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="7c548-114">You can obtain hello values for hello SAS key name and value from hello [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="7c548-115">Merhaba `create_topic` yöntemi de ileti zaman toolive veya en büyük konu boyutu gibi toooverride varsayılan konu ayarlarını etkinleştir ek seçenekleri destekler.</span><span class="sxs-lookup"><span data-stu-id="7c548-115">hello `create_topic` method also supports additional options, which enable you toooverride default topic settings such as message time toolive or maximum topic size.</span></span> <span data-ttu-id="7c548-116">Merhaba aşağıdaki örnek hello en fazla konu boyutu too5 GB ve bir süre toolive (TTL) değerini 1 dakika ayarlar:</span><span class="sxs-lookup"><span data-stu-id="7c548-116">hello following example sets hello maximum topic size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="7c548-117">Abonelikleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c548-117">Create subscriptions</span></span>
<span data-ttu-id="7c548-118">Abonelikler tootopics de hello ile oluşturulan **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7c548-118">Subscriptions tootopics are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="7c548-119">Abonelikler adlandırılır ve hello toohello aboneliğin sanal kuyruğuna teslim edilen ileti kümesini sınırlayan isteğe bağlı bir filtre içerebilir.</span><span class="sxs-lookup"><span data-stu-id="7c548-119">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="7c548-120">Abonelikleri kalıcı ve tooexist ya da bunlar kadar devam eder veya hello konu toowhich bunlar abone olduğunuz silinir.</span><span class="sxs-lookup"><span data-stu-id="7c548-120">Subscriptions are persistent and will continue tooexist until either they, or hello topic toowhich they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="7c548-121">Merhaba varsayılan (MatchAll) filtreyle abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c548-121">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="7c548-122">Merhaba **MatchAll** yeni bir abonelik oluşturulurken filtre belirtilmeyen varsa, kullanılan hello varsayılan filtre filtredir.</span><span class="sxs-lookup"><span data-stu-id="7c548-122">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="7c548-123">Ne zaman hello **MatchAll** filtre kullanıldığında, tüm iletileri yayımlanan toohello konu hello aboneliğin sanal kuyruğuna yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7c548-123">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="7c548-124">Merhaba aşağıdaki örnek adlı bir abonelik oluşturulur `AllMessages` ve kullandığı varsayılan hello **MatchAll** Filtresi.</span><span class="sxs-lookup"><span data-stu-id="7c548-124">hello following example creates a subscription named `AllMessages` and uses hello default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="7c548-125">Filtre içeren abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c548-125">Create subscriptions with filters</span></span>
<span data-ttu-id="7c548-126">Ayrıca hangi iletilerin tooa konu içinde belirli konu aboneliği göstermelidir gönderilen toospecify etkinleştirmek filtreleri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c548-126">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="7c548-127">Merhaba en esnek filtre abonelikler tarafından desteklenen türünde bir **SqlFilter**, SQL92 alt kümesi uygular.</span><span class="sxs-lookup"><span data-stu-id="7c548-127">hello most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="7c548-128">SQL filtreleri yayımlanan toohello konu hello iletilerinin hello özelliklerini çalışır.</span><span class="sxs-lookup"><span data-stu-id="7c548-128">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="7c548-129">Merhaba SQL Filtresi ile kullanılabilen hello ifadeler hakkında daha fazla bilgi için bkz: [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sözdizimi.</span><span class="sxs-lookup"><span data-stu-id="7c548-129">For more information about hello expressions that can be used with a SQL filter, see hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="7c548-130">Hello kullanarak filtreleri tooa aboneliğiniz ekleyebilirsiniz **oluşturma\_kural** hello yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7c548-130">You can add filters tooa subscription by using hello **create\_rule** method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="7c548-131">Bu yöntem tooadd yeni filtreleri tooan varolan abonelik sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c548-131">This method allows you tooadd new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="7c548-132">Merhaba varsayılan filtre otomatik olarak uygulandığından tooall yeni abonelikler, hello varsayılan filtre veya hello önce kaldırmalısınız **MatchAll** belirttiğiniz diğer filtreleri geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="7c548-132">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="7c548-133">Hello kullanarak hello varsayılan kural kaldırabilirsiniz `delete_rule` hello yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7c548-133">You can remove hello default rule by using hello `delete_rule` method of hello **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="7c548-134">Merhaba aşağıdaki örnek adlı bir abonelik oluşturulur `HighMessages` ile bir **SqlFilter** özel iletileri yalnızca seçer `messagenumber` özelliği 3'ten büyük:</span><span class="sxs-lookup"><span data-stu-id="7c548-134">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="7c548-135">Benzer şekilde, hello aşağıdaki örnek adlı bir abonelik oluşturur `LowMessages` ile bir **SqlFilter** olan iletiler yalnızca seçer bir `messagenumber` özelliği daha az veya bu değere eşit too3:</span><span class="sxs-lookup"><span data-stu-id="7c548-135">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="7c548-136">Şimdi, ne zaman bir ileti gönderilir çok`mytopic` her zaman abone tooreceivers toohello teslim **AllMessages** konu aboneliği ve abone olunan seçmeli olarak teslim tooreceivers toohello **HighMessages**  ve **LowMessages** konu abonelikleri (bağlı olarak hello ileti içeriği).</span><span class="sxs-lookup"><span data-stu-id="7c548-136">Now, when a message is sent too`mytopic` it is always delivered tooreceivers subscribed toohello **AllMessages** topic subscription, and selectively delivered tooreceivers subscribed toohello **HighMessages** and **LowMessages** topic subscriptions (depending on hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="7c548-137">İletileri tooa konu gönderin</span><span class="sxs-lookup"><span data-stu-id="7c548-137">Send messages tooa topic</span></span>
<span data-ttu-id="7c548-138">toosend ileti tooa Service Bus konu, uygulamanızı hello kullanmalıdır `send_topic_message` hello yöntemi **ServiceBusService** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7c548-138">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message` method of hello **ServiceBusService** object.</span></span>

<span data-ttu-id="7c548-139">Merhaba aşağıdaki örnekte nasıl toosend beş test çok iletileri gösterir`mytopic`.</span><span class="sxs-lookup"><span data-stu-id="7c548-139">hello following example demonstrates how toosend five test messages too`mytopic`.</span></span> <span data-ttu-id="7c548-140">Bu hello Not `messagenumber` her ileti özelliği değeri değişir hello döngü hello yinelemesi (Bu alacak abonelikleri belirler):</span><span class="sxs-lookup"><span data-stu-id="7c548-140">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="7c548-141">Service Bus konu başlıklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="7c548-141">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="7c548-142">Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir.</span><span class="sxs-lookup"><span data-stu-id="7c548-142">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="7c548-143">Merhaba konu başlığında tutulan ileti sayısına bir sınır yoktur ancak konu başlığı tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="7c548-143">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="7c548-144">Bu konu başlığı boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="7c548-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="7c548-145">Kotalar hakkında daha fazla bilgi için bkz: [Service Bus kotaları][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="7c548-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="7c548-146">Abonelikten ileti alma</span><span class="sxs-lookup"><span data-stu-id="7c548-146">Receive messages from a subscription</span></span>
<span data-ttu-id="7c548-147">İletileri hello kullanarak bir abonelikten alınan `receive_subscription_message` hello yöntemi **ServiceBusService** nesnesi:</span><span class="sxs-lookup"><span data-stu-id="7c548-147">Messages are received from a subscription using hello `receive_subscription_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="7c548-148">İletileri zaman okunduğu gibi hello abonelikten silindi parametre hello `peek_lock` çok ayarlanır**False**.</span><span class="sxs-lookup"><span data-stu-id="7c548-148">Messages are deleted from hello subscription as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="7c548-149">(Özet) okuma ve ayarlama hello parametresiyle hello sıradan silmeden selamlama iletisine kilitlemek `peek_lock` çok**doğru**.</span><span class="sxs-lookup"><span data-stu-id="7c548-149">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="7c548-150">Okuma davranışını hello ve hello parçası işlemi aldıklarında hello iletisi siliniyor hello en basit modeldir ve uygulamanın bir hatanın hello Olay iletisinde işlenmiyor dayanabileceği senaryolarda en iyi şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="7c548-150">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="7c548-151">toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor.</span><span class="sxs-lookup"><span data-stu-id="7c548-151">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="7c548-152">Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.</span><span class="sxs-lookup"><span data-stu-id="7c548-152">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="7c548-153">Merhaba, `peek_lock` parametresi çok ayarlanırsa**True**, hello alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur.</span><span class="sxs-lookup"><span data-stu-id="7c548-153">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="7c548-154">Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur.</span><span class="sxs-lookup"><span data-stu-id="7c548-154">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="7c548-155">Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin `delete` hello yöntemi **ileti** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7c548-155">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete` method on hello **Message** object.</span></span> <span data-ttu-id="7c548-156">Merhaba `delete` yöntemi hello iletiyi kullanılıyor olarak işaretler ve hello abonelikten kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7c548-156">hello `delete` method marks hello message as being consumed and removes it from hello subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="7c548-157">Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri</span><span class="sxs-lookup"><span data-stu-id="7c548-157">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="7c548-158">Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c548-158">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="7c548-159">Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlock` hello yöntemi **ileti** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7c548-159">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock` method on hello **Message** object.</span></span> <span data-ttu-id="7c548-160">Bu hizmet veri yolu toounlock selamlama iletisine hello abonelik içindeki neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.</span><span class="sxs-lookup"><span data-stu-id="7c548-160">This will cause Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="7c548-161">Ayrıca hello abonelikte kilitlenen iletiye ilişkin bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus hello iletinin kilidini açar hello kilit zaman aşımı dolmadan otomatik olarak yeniden alınan kullanılabilir toobe yapar.</span><span class="sxs-lookup"><span data-stu-id="7c548-161">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="7c548-162">Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `delete` yöntemi çağrıldıktan sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7c548-162">In hello event that hello application crashes after processing hello message but before hello `delete` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="7c548-163">Bu genellikle adlandırılır *en az bir kez işleme*, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim.</span><span class="sxs-lookup"><span data-stu-id="7c548-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="7c548-164">Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c548-164">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="7c548-165">Bu genellikle hello kullanılarak elde edilen **MessageID** teslimat denemelerinde hello iletinin özelliği.</span><span class="sxs-lookup"><span data-stu-id="7c548-165">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="7c548-166">Konu başlıklarını ve abonelikleri silme</span><span class="sxs-lookup"><span data-stu-id="7c548-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="7c548-167">Konu başlıkları ve abonelikler kalıcıdır ve açıkça olmalıdır hello aracılığıyla ya da silinmiş [Azure portal] [ Azure portal] veya program aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="7c548-167">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="7c548-168">Merhaba aşağıdaki örnekte nasıl toodelete hello konu adlı gösterir `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="7c548-168">hello following example shows how toodelete hello topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="7c548-169">Bir konu başlığı silindiğinde hello konu başlığıyla kaydedilen tüm abonelikleri siler.</span><span class="sxs-lookup"><span data-stu-id="7c548-169">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="7c548-170">Ayrıca, abonelikler bağımsız olarak da silinebilir.</span><span class="sxs-lookup"><span data-stu-id="7c548-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="7c548-171">Merhaba aşağıdaki kod nasıl toodelete bir abonelik adlı gösterir `HighMessages` hello gelen `mytopic` konu:</span><span class="sxs-lookup"><span data-stu-id="7c548-171">hello following code shows how toodelete a subscription named `HighMessages` from hello `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="7c548-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7c548-172">Next steps</span></span>
<span data-ttu-id="7c548-173">Artık Service Bus konu başlıklarını hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="7c548-173">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="7c548-174">Bkz: [kuyruklar, konu başlıkları ve abonelikler][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="7c548-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="7c548-175">İçin başvuru [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="7c548-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
