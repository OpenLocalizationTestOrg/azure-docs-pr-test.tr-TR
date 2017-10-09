---
title: "aaaHow toouse Azure Service Bus kuyrukları ile Söyleniş | Microsoft Docs"
description: "Azure'da nasıl toouse Service Bus kuyrukları öğrenin. Ruby içinde yazılan kod örnekleri."
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 0a11eab2-823f-4cc7-842b-fbbe0f953751
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 7270154583f98e3372e82efbb967ea7a5acd1686
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-ruby"></a>Ruby ile nasıl toouse Service Bus kuyrukları

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Bu kılavuzda açıklanmaktadır nasıl toouse Service Bus kuyruklarını. Merhaba örnekler içinde Ruby yazılır ve hello Azure gem kullanır. Merhaba kapsanan senaryolar dahil **ileti gönderme ve alma sıra oluşturma**, ve **sıraları silme**. Service Bus kuyruklarını hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next-steps) bölümü.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]
   
[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="how-toocreate-a-queue"></a>Nasıl bir kuyruk toocreate
Merhaba **Azure::ServiceBusService** nesne kuyruklarla toowork sağlar. toocreate bir sıra kullanmak hello `create_queue()` yöntemi. Merhaba aşağıdaki örnekte bir kuyruk oluşturur veya tüm hataları yazdırır.

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  queue = azure_service_bus_service.create_queue("test-queue")
rescue
  puts $!
end
```

Ayrıca iletebilirsiniz bir **Azure::ServiceBus::Queue** nesne ek seçeneklerle toooverride hello varsayılan sıra ayarları, ileti zaman toolive veya en büyük sıra boyutu gibi sağlar. Aşağıdaki örnek hello nasıl tooset en büyük sıra boyutu too5 GB hello ve toolive too1 minute zaman gösterir:

```ruby
queue = Azure::ServiceBus::Queue.new("test-queue")
queue.max_size_in_megabytes = 5120
queue.default_message_time_to_live = "PT1M"

queue = azure_service_bus_service.create_queue(queue)
```

## <a name="how-toosend-messages-tooa-queue"></a>Nasıl toosend iletileri tooa sırası
ileti tooa Service Bus kuyruğuna toosend, uygulamanızın çağırır hello `send_queue_message()` hello yöntemi **Azure::ServiceBusService** nesnesi. İletileri çok gönderilen (ve öğesinden alınan) hizmet kuyruklar veri yolu **Azure::ServiceBus::BrokeredMessage** nesneleri ve bir standart özellikler kümesi sahip (gibi `label` ve `time_to_live`), kullanılan toohold bir sözlüğü Özel uygulamaya özgü özellikler ve rastgele uygulama verileri gövdesi. Bir uygulama selamlama iletisine bir dize değeri geçirerek hello hello ileti gövdesini ayarlayabilir ve gerekli tüm standart özellikleri varsayılan değerlerle doldurulur.

Merhaba aşağıdaki örnekte nasıl toosend adlı bir sınama iletisi toohello sırası gösteren `test-queue` kullanarak `send_queue_message()`:

```ruby
message = Azure::ServiceBus::BrokeredMessage.new("test queue message")
message.correlation_id = "test-correlation-id"
azure_service_bus_service.send_queue_message("test-queue", message)
```

Service Bus kuyruklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md). Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir. Merhaba bir kuyrukta tutulan ileti sayısına bir sınır yoktur ancak kuyruk tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur. Bu kuyruk boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.

## <a name="how-tooreceive-messages-from-a-queue"></a>Nasıl tooreceive kuyruktan iletileri
İletileri hello kullanarak bir kuyruktan alınan `receive_queue_message()` hello yöntemi **Azure::ServiceBusService** nesnesi. Varsayılan olarak, iletileri okumak ve hello sıradan silinir olmadan kilitli. Ayarı hello tarafından okurken ancak iletileri hello sıradan silebilirsiniz `:peek_lock` çok seçenek**false**.

Merhaba varsayılan davranışı okumak ve ayrıca, iletilere olası toosupport uygulamaları kılar bir iki aşamalı işlemi silme hello yapar. Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur. Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin `delete_queue_message()` yöntemi ve parametre olarak silinmiş hello ileti toobe sağlama. Merhaba `delete_queue_message()` yöntemi hello iletiyi kullanılıyor olarak işaretler ve hello sıradan kaldırın.

Merhaba, `:peek_lock` parametresi çok ayarlanırsa**yanlış**, okuma ve hello iletisi siliniyor hello basit model olur ve senaryoları bir uygulama içinde tolerans hello olayı içinde ileti işlenirken değil en iyi şekilde çalışır bir hata oluştu. toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor. Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında, kullanılan olarak işaretlenmiş olduğundan, onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.

Merhaba aşağıdaki örnekte nasıl tooreceive ve işlem iletileri kullanarak gösteren `receive_queue_message()`. Merhaba örneği ilk alır ve bir iletiyi kullanarak siler `:peek_lock` çok ayarlamak**false**, ardından başka bir ileti alır ve ardından iletiyi kullanarak siler hello `delete_queue_message()`:

```ruby
message = azure_service_bus_service.receive_queue_message("test-queue",
  { :peek_lock => false })
message = azure_service_bus_service.receive_queue_message("test-queue")
azure_service_bus_service.delete_queue_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri
Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar. Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlock_queue_message()` hello yöntemi **Azure::ServiceBusService** nesnesi. Bu çağrı nedenler Service Bus toounlock hello hello sıra içinde ileti gönderme ve yeniden alınan kullanılabilir toobe olun ya da göre hello aynı uygulama veya başka bir kullanıcı uygulama tarafından kullanma.

Ayrıca hello kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus hello iletinin kilidini açar hello kilit zaman aşımı dolmadan otomatik olarak yeniden alınan kullanılabilir toobe yapar.

Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `delete_queue_message()` yöntemi çağrıldıktan sonra hello ileti yeniden teslim toohello uygulama başlatıldığında içindir. Bu işlem genellikle adlı *en az bir kez işleme*; diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim. Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir. Bu genellikle hello kullanılarak elde edilen `message_id` teslimat denemelerinde hello iletinin özelliği.

## <a name="next-steps"></a>Sonraki adımlar
Artık Service Bus kuyruklarını hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

* Genel Bakış [kuyruklar, konu başlıkları ve abonelikler](service-bus-queues-topics-subscriptions.md).
* Merhaba ziyaret [Ruby için Azure SDK](https://github.com/Azure/azure-sdk-for-ruby) github'daki.

Bu makalede açıklanan hello Azure Service Bus kuyrukları ve Azure hello ele alınan sıraları arasında bir karşılaştırma için [nasıl toouse ruby'den kuyruk depolama](../storage/queues/storage-ruby-how-to-use-queue-storage.md) makale için bkz: [Azure kuyrukları ve Azure hizmet veri yolu kuyrukları - karşılaştırma ve Contrasted](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

