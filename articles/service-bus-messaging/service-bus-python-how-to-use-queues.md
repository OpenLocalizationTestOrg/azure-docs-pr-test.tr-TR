---
title: "aaaHow toouse Azure Service Bus kuyrukları Python ile | Microsoft Docs"
description: "Python nasıl toouse Azure Service Bus kuyrukları öğrenin."
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a>Python ile nasıl toouse Service Bus kuyrukları

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Bu makalede nasıl toouse Service Bus kuyruklarını. Merhaba örnekleri Python içinde yazılmış ve hello kullan [Python Azure Service Bus paket][Python Azure Service Bus package]. Merhaba kapsanan senaryolar dahil **ileti gönderme ve alma sıra oluşturma**, ve **sıraları silme**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> Python veya hello tooinstall [Python Azure Service Bus paket][Python Azure Service Bus package], hello bkz [Python Yükleme Kılavuzu'na](../python-how-to-install.md).
> 
> 

## <a name="create-a-queue"></a>Bir kuyruk oluşturma
Merhaba **ServiceBusService** nesne kuyruklarla toowork sağlar. Tooprogrammatically erişim Service Bus istediğiniz herhangi bir Python dosyasının kaydedileceği hello üstüne yakın koddan hello ekleyin:

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

Merhaba aşağıdaki kod oluşturur bir **ServiceBusService** nesnesi. Değiştir `mynamespace`, `sharedaccesskeyname`, ve `sharedaccesskey` ad alanı, paylaşılan erişim imzası (SAS) anahtar adını ve değeri.

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Merhaba hello SAS anahtar adı ve değeri değerlerini hello bulunabilir [Azure portal] [ Azure portal] bağlantı bilgilerini veya hello Visual Studio **özellikleri** seçerken bölmesi Sunucu Gezgininde Service Bus ad alanı (Merhaba önceki bölümde gösterildiği gibi) hello.

```python
bus_service.create_queue('taskqueue')
```

Merhaba `create_queue` yöntemi de ileti toolive süresi (TTL) veya en büyük sıra boyutu gibi toooverride varsayılan sıra ayarları etkinleştirmek ek seçenekleri destekler. Merhaba aşağıdaki örnek hello en büyük sıra boyutu too5 GB ve hello TTL değeri too1 minute ayarlar:

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a>İletileri tooa sırası Gönder
ileti tooa Service Bus kuyruğuna toosend, uygulamanızın çağırır hello `send_queue_message` hello yöntemi **ServiceBusService** nesnesi.

Merhaba aşağıdaki örnekte nasıl toosend adlı bir sınama iletisi toohello sırası gösteren `taskqueue` kullanarak `send_queue_message`:

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

Service Bus kuyruklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md). Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir. Merhaba bir kuyrukta tutulan ileti sayısına bir sınır yoktur ancak kuyruk tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur. Bu kuyruk boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir. Kotalar hakkında daha fazla bilgi için bkz: [Service Bus kotaları][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>Kuyruktan ileti alma
İletileri hello kullanarak bir kuyruktan alınan `receive_queue_message` hello yöntemi **ServiceBusService** nesnesi:

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

İletileri zaman okunduğu gibi hello sıradan silinir parametre hello `peek_lock` çok ayarlanır**False**. (Özet) okuma ve ayarlama hello parametresiyle hello sıradan silmeden selamlama iletisine kilitlemek `peek_lock` çok**doğru**.

Okuma davranışını hello ve hello parçası işlemi aldıklarında hello iletisi siliniyor hello en basit modeldir ve uygulamanın bir hatanın hello Olay iletisinde işlenmiyor dayanabileceği senaryolarda en iyi şekilde çalışır. toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor. Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.

Merhaba, `peek_lock` parametresi çok ayarlanırsa**True**, hello alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur. Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur. Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar tarafından arama hello alma işleminin **silmek** hello yöntemi **ileti** nesnesi. Merhaba **silmek** yöntemi hello iletiyi kullanılıyor olarak işaretler ve hello sıradan kaldırın.

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri
Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar. Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz **kilidini** hello yöntemi **ileti** nesnesi. Bu hizmet veri yolu toounlock selamlama iletisine hello sıra içinde neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.

Ayrıca hello kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve hello tooprocess önce iletiyi hello hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus selamlama iletisine otomatik olarak kilitlenmeden kilit zaman aşımı dolmadan ve yeniden alınan kullanılabilir toobe yapın.

Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor **silmek** yöntemi çağrıldıktan sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır. Bu genellikle adlandırılır **en az bir kez işleme**, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim. Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir. Bu genellikle hello kullanılarak elde edilen **MessageID** teslimat denemelerinde hello iletinin özelliği.

## <a name="next-steps"></a>Sonraki adımlar
Service Bus kuyruklarını hello temel bilgileri öğrendiniz, daha fazla Bu makaleler toolearn bakın.

* [Kuyruklar, konu başlıkları ve abonelikler][Queues, topics, and subscriptions]

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

