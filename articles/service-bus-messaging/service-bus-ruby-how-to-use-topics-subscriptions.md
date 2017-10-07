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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a>Nasıl toouse Service Bus konuları ve abonelikleri Ruby ile
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Bu makalede nasıl toouse Service Bus konuları ve abonelikleri Söyleniş uygulamalardan. Merhaba kapsanan senaryolar dahil **konuları ve Abonelikleri, ileti gönderme, abonelik filtreleri oluşturma oluşturma** tooa konu **abonelikten ileti alma**, ve  **konuları ve abonelikleri silmeyi**. Konu başlıkları ve abonelikler hakkında daha fazla bilgi için bkz: hello [sonraki adımlar](#next-steps) bölümü.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a>Konu başlığı oluşturma
Merhaba **Azure::ServiceBusService** nesne konuları ile toowork sağlar. Merhaba aşağıdaki kod oluşturur bir **Azure::ServiceBusService** nesnesi. toocreate bir konu kullanmak hello `create_topic()` yöntemi. Aşağıdaki örnek hello bir konu oluşturur veya varsa hello hataları yazdırır.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

Ayrıca iletebilirsiniz bir **Azure::ServiceBus::Topic** toooverride varsayılan konu ayarları ileti zaman toolive veya en büyük sıra boyutu gibi etkinleştirin ek seçeneklere sahip nesne. Merhaba hello en büyük sıra ayarı aşağıdaki örnekte gösterildiği too5 GB boyutunu ve toolive too1 minute süresi:

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a>Abonelikleri oluşturma
Konu aboneliklerini ayrıca hello ile oluşturulan **Azure::ServiceBusService** nesnesi. Abonelikler adlandırılır ve hello toohello aboneliğin sanal kuyruğuna teslim edilen ileti kümesini sınırlayan isteğe bağlı bir filtre içerebilir.

Abonelikleri kalıcı ve tooexist ya da bunlar kadar devam eder veya hello konu bunların ilişkili silinir. Uygulama mantığı toocreate bir abonelik içeriyorsa, ilk hello abonelik zaten hello getSubscription yöntemini kullanarak olup olmadığını denetlemelisiniz.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Merhaba varsayılan (MatchAll) filtreyle abonelik oluşturma
Merhaba **MatchAll** yeni bir abonelik oluşturulurken filtre belirtilmeyen varsa, kullanılan hello varsayılan filtre filtredir. Ne zaman hello **MatchAll** filtre kullanıldığında, tüm iletileri yayımlanan toohello konu hello aboneliğin sanal kuyruğuna yerleştirilir. Merhaba aşağıdaki örnekte "tüm iletileri" adlı bir abonelik oluşturur ve kullanır hello varsayılan **MatchAll** Filtresi.

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a>Filtre içeren abonelik oluşturma
Ayrıca hangi iletilerin tooa konu içinde belirli bir aboneliği göstermelidir gönderilen toospecify etkinleştirmek filtreleri tanımlayabilirsiniz.

Merhaba en esnek filtre abonelikler tarafından desteklenen hello türünde **Azure::ServiceBus::SqlFilter**, SQL92 alt kümesi uygular. SQL filtreleri yayımlanan toohello konu hello iletilerinin hello özelliklerini çalışır. Merhaba SQL Filtresi ile kullanılabilen hello ifadeler hakkında daha fazla ayrıntı için gözden [SqlFilter](service-bus-messaging-sql-filter.md) sözdizimi.

Hello kullanarak filtreleri tooa aboneliğiniz ekleyebilirsiniz `create_rule()` hello yöntemi **Azure::ServiceBusService** nesnesi. Bu yöntem tooadd yeni filtreleri tooan varolan abonelik sağlar.

Merhaba varsayılan filtre otomatik olarak uygulanan bu yana tooall yeni abonelikler, ilk hello varsayılan filtresini kaldırın veya gerekir hello **MatchAll** belirttiğiniz diğer filtreleri geçersiz kılar. Hello kullanarak hello varsayılan kural kaldırabilirsiniz `delete_rule()` hello yöntemi **Azure::ServiceBusService** nesnesi.

Merhaba aşağıdaki örnekte "iletileri yüksek" adında bir abonelik oluşturur bir **Azure::ServiceBus::SqlFilter** özel iletileri yalnızca seçer `message_number` özelliği 3'ten büyük:

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

Benzer şekilde, hello aşağıdaki örnek adlı bir abonelik oluşturur `low-messages` ile bir **Azure::ServiceBus::SqlFilter** olan iletiler yalnızca seçer bir `message_number` özelliği daha az veya bu değere eşit too3:

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

Ne zaman bir ileti artık gönderilir çok`test-topic`, her zaman abone teslim tooreceivers toohello olacak olan `all-messages` konu aboneliği ve abone olunan seçmeli olarak teslim tooreceivers toohello `high-messages` ve `low-messages` konu abonelikleri () Merhaba ileti içeriği bağlı olarak).

## <a name="send-messages-tooa-topic"></a>İletileri tooa konu gönderin
toosend ileti tooa Service Bus konu, uygulamanızı hello kullanmalıdır `send_topic_message()` hello yöntemi **Azure::ServiceBusService** nesnesi. İletileri gönderilir tooService veri yolu konuları hello örneklerini **Azure::ServiceBus::BrokeredMessage** nesneleri. **Azure::ServiceBus::BrokeredMessage** nesneleri olan bir standart özellikler kümesi (gibi `label` ve `time_to_live`), kullanılan toohold özel uygulamaya özgü özellikler sözlüğü bir ve dize verileri gövdesi içerir. Bir uygulama bir dize değeri toohello geçirerek hello hello ileti gövdesini ayarlayabilir `send_topic_message()` yöntemi ve tüm gerekli standart özellikleri varsayılan değerlerle doldurulmuş.

Merhaba aşağıdaki örnekte nasıl toosend beş test çok iletileri gösterir`test-topic`. Bu hello Not `message_number` özel özellik değerini her iletinin hello döngü hello yinelemesi değişir (Bu abonelik aldığı belirler):

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

Service Bus konu başlıklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md). Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir. Merhaba konu başlığında tutulan ileti sayısına bir sınır yoktur ancak konu başlığı tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur. Bu konu başlığı boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.

## <a name="receive-messages-from-a-subscription"></a>Abonelikten ileti alma
İletileri hello kullanarak bir abonelikten alınan `receive_subscription_message()` hello yöntemi **Azure::ServiceBusService** nesnesi. Varsayılan olarak, iletiler read(peak) ve hello abonelikten silmeden kilitli. Okuma ve ayarlama hello tarafından hello abonelikten selamlama iletisine silmek `peek_lock` çok seçenek**false**.

Merhaba varsayılan davranışı okumak ve ayrıca, iletilere olası toosupport uygulamaları kılar bir iki aşamalı işlemi silme hello yapar. Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur. Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin `delete_subscription_message()` yöntemi ve parametre olarak silinmiş hello ileti toobe sağlama. Merhaba `delete_subscription_message()` yöntemi hello iletiyi kullanılıyor olarak işaretler ve hello abonelikten Kaldır.

Merhaba, `:peek_lock` parametresi çok ayarlanırsa**yanlış**, okuma ve hello iletisi siliniyor hello basit model olur ve senaryoları bir uygulama içinde tolerans hello olayı içinde ileti işlenirken değil en iyi şekilde çalışır bir hata oluştu. toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor. Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.

Merhaba aşağıdaki örnekte nasıl iletilerin alındığını ve işlenen kullanarak gösteren `receive_subscription_message()`. Merhaba örneği ilk alır ve bir ileti hello siler `low-messages` kullanarak abonelik `:peek_lock` çok ayarlamak**false**, hello başka bir ileti alır sonra `high-messages` ve ardından iletiyi kullanarak siler hello `delete_subscription_message()`:

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri
Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar. Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlock_subscription_message()` hello yöntemi **Azure::ServiceBusService** nesnesi. Hizmet veri yolu toounlock hello hello aboneliğin ileti gönderme ve yeniden alınan kullanılabilir toobe olun Bu nedenler ya da göre hello aynı uygulama veya başka bir kullanıcı uygulama tarafından kullanma.

Ayrıca hello abonelikte kilitlenen iletiye ilişkin bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus selamlama iletisine kilidini hello kilit zaman aşımı dolmadan otomatik olarak yeniden alınan kullanılabilir toobe olun.

Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `delete_subscription_message()` yöntemi çağrıldıktan sonra hello ileti yeniden teslim toohello uygulama başlatıldığında içindir. Bu genellikle adlandırılır *en az bir kez işleme*; diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim. Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir. Bu mantık, genellikle hello kullanılarak gerçekleştirilir `message_id` teslimat denemelerinde hello iletinin özelliği.

## <a name="delete-topics-and-subscriptions"></a>Konu başlıklarını ve abonelikleri silme
Konu başlıkları ve abonelikler kalıcıdır ve açıkça olmalıdır hello aracılığıyla ya da silinmiş [Azure portal] [ Azure portal] veya program aracılığıyla. Aşağıdaki örnek Hello gösterir nasıl toodelete hello konu adlı `test-topic`.

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

Bir konu başlığı silindiğinde hello konu başlığıyla kaydedilen tüm abonelikleri siler. Ayrıca, abonelikler bağımsız olarak da silinebilir. Merhaba aşağıdaki kodu nasıl toodelete hello abonelik adlı gösterir `high-messages` hello gelen `test-topic` konu:

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a>Sonraki adımlar
Artık Service Bus konu başlıklarını hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

* Bkz: [kuyruklar, konu başlıkları ve abonelikler](service-bus-queues-topics-subscriptions.md).
* [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter) için API başvurusu
* Merhaba ziyaret [Ruby için Azure SDK](https://github.com/Azure/azure-sdk-for-ruby) github'daki.

[Azure portal]: https://portal.azure.com
