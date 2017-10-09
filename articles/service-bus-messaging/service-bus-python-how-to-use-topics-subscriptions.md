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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a>Nasıl toouse Service Bus konuları ve abonelikleri Python ile

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Bu makalede nasıl toouse Service Bus konuları ve abonelikleri. Merhaba örnekleri Python içinde yazılmış ve hello kullan [Azure Python SDK paketi][Azure Python package]. Merhaba kapsanan senaryolar dahil **konuları ve abonelikleri oluşturma**, **abonelik filtreleri oluşturma**, **iletileri tooa konu gönderme**, **alma bir abonelik iletilerden**, ve **konuları ve abonelikleri silmeyi**. Merhaba konu başlıkları ve abonelikler hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> Tooinstall Python veya hello gereksinim duyarsanız [Azure Python paket][Azure Python package], hello bkz [Python Yükleme Kılavuzu'na](../python-how-to-install.md).

## <a name="create-a-topic"></a>Konu başlığı oluşturma
Merhaba **ServiceBusService** nesne konuları ile toowork sağlar. Tooprogrammatically erişim Service Bus istediğiniz herhangi bir Python dosyasının kaydedileceği hello üstüne yakın Hello aşağıdakileri ekleyin:

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

Merhaba aşağıdaki kod oluşturur bir **ServiceBusService** nesnesi. Değiştir `mynamespace`, `sharedaccesskeyname`, ve `sharedaccesskey` ile gerçek ad alanınız, paylaşılan erişim imzası (SAS) anahtar adını ve anahtar değeri.

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

Hello hello değerleri hello SAS anahtar adını ve değeri elde [Azure portal][Azure portal].

```python
bus_service.create_topic('mytopic')
```

Merhaba `create_topic` yöntemi de ileti zaman toolive veya en büyük konu boyutu gibi toooverride varsayılan konu ayarlarını etkinleştir ek seçenekleri destekler. Merhaba aşağıdaki örnek hello en fazla konu boyutu too5 GB ve bir süre toolive (TTL) değerini 1 dakika ayarlar:

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a>Abonelikleri oluşturma
Abonelikler tootopics de hello ile oluşturulan **ServiceBusService** nesnesi. Abonelikler adlandırılır ve hello toohello aboneliğin sanal kuyruğuna teslim edilen ileti kümesini sınırlayan isteğe bağlı bir filtre içerebilir.

> [!NOTE]
> Abonelikleri kalıcı ve tooexist ya da bunlar kadar devam eder veya hello konu toowhich bunlar abone olduğunuz silinir.
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Merhaba varsayılan (MatchAll) filtreyle abonelik oluşturma
Merhaba **MatchAll** yeni bir abonelik oluşturulurken filtre belirtilmeyen varsa, kullanılan hello varsayılan filtre filtredir. Ne zaman hello **MatchAll** filtre kullanıldığında, tüm iletileri yayımlanan toohello konu hello aboneliğin sanal kuyruğuna yerleştirilir. Merhaba aşağıdaki örnek adlı bir abonelik oluşturulur `AllMessages` ve kullandığı varsayılan hello **MatchAll** Filtresi.

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a>Filtre içeren abonelik oluşturma
Ayrıca hangi iletilerin tooa konu içinde belirli konu aboneliği göstermelidir gönderilen toospecify etkinleştirmek filtreleri tanımlayabilirsiniz.

Merhaba en esnek filtre abonelikler tarafından desteklenen türünde bir **SqlFilter**, SQL92 alt kümesi uygular. SQL filtreleri yayımlanan toohello konu hello iletilerinin hello özelliklerini çalışır. Merhaba SQL Filtresi ile kullanılabilen hello ifadeler hakkında daha fazla bilgi için bkz: [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sözdizimi.

Hello kullanarak filtreleri tooa aboneliğiniz ekleyebilirsiniz **oluşturma\_kural** hello yöntemi **ServiceBusService** nesnesi. Bu yöntem tooadd yeni filtreleri tooan varolan abonelik sağlar.

> [!NOTE]
> Merhaba varsayılan filtre otomatik olarak uygulandığından tooall yeni abonelikler, hello varsayılan filtre veya hello önce kaldırmalısınız **MatchAll** belirttiğiniz diğer filtreleri geçersiz kılar. Hello kullanarak hello varsayılan kural kaldırabilirsiniz `delete_rule` hello yöntemi **ServiceBusService** nesnesi.
> 
> 

Merhaba aşağıdaki örnek adlı bir abonelik oluşturulur `HighMessages` ile bir **SqlFilter** özel iletileri yalnızca seçer `messagenumber` özelliği 3'ten büyük:

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

Benzer şekilde, hello aşağıdaki örnek adlı bir abonelik oluşturur `LowMessages` ile bir **SqlFilter** olan iletiler yalnızca seçer bir `messagenumber` özelliği daha az veya bu değere eşit too3:

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

Şimdi, ne zaman bir ileti gönderilir çok`mytopic` her zaman abone tooreceivers toohello teslim **AllMessages** konu aboneliği ve abone olunan seçmeli olarak teslim tooreceivers toohello **HighMessages**  ve **LowMessages** konu abonelikleri (bağlı olarak hello ileti içeriği).

## <a name="send-messages-tooa-topic"></a>İletileri tooa konu gönderin
toosend ileti tooa Service Bus konu, uygulamanızı hello kullanmalıdır `send_topic_message` hello yöntemi **ServiceBusService** nesnesi.

Merhaba aşağıdaki örnekte nasıl toosend beş test çok iletileri gösterir`mytopic`. Bu hello Not `messagenumber` her ileti özelliği değeri değişir hello döngü hello yinelemesi (Bu alacak abonelikleri belirler):

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

Service Bus konu başlıklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md). Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir. Merhaba konu başlığında tutulan ileti sayısına bir sınır yoktur ancak konu başlığı tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur. Bu konu başlığı boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir. Kotalar hakkında daha fazla bilgi için bkz: [Service Bus kotaları][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Abonelikten ileti alma
İletileri hello kullanarak bir abonelikten alınan `receive_subscription_message` hello yöntemi **ServiceBusService** nesnesi:

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

İletileri zaman okunduğu gibi hello abonelikten silindi parametre hello `peek_lock` çok ayarlanır**False**. (Özet) okuma ve ayarlama hello parametresiyle hello sıradan silmeden selamlama iletisine kilitlemek `peek_lock` çok**doğru**.

Okuma davranışını hello ve hello parçası işlemi aldıklarında hello iletisi siliniyor hello en basit modeldir ve uygulamanın bir hatanın hello Olay iletisinde işlenmiyor dayanabileceği senaryolarda en iyi şekilde çalışır. toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor. Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.

Merhaba, `peek_lock` parametresi çok ayarlanırsa**True**, hello alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur. Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur. Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin `delete` hello yöntemi **ileti** nesnesi. Merhaba `delete` yöntemi hello iletiyi kullanılıyor olarak işaretler ve hello abonelikten kaldırır.

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri
Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar. Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlock` hello yöntemi **ileti** nesnesi. Bu hizmet veri yolu toounlock selamlama iletisine hello abonelik içindeki neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.

Ayrıca hello abonelikte kilitlenen iletiye ilişkin bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus hello iletinin kilidini açar hello kilit zaman aşımı dolmadan otomatik olarak yeniden alınan kullanılabilir toobe yapar.

Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `delete` yöntemi çağrıldıktan sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır. Bu genellikle adlandırılır *en az bir kez işleme*, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim. Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir. Bu genellikle hello kullanılarak elde edilen **MessageID** teslimat denemelerinde hello iletinin özelliği.

## <a name="delete-topics-and-subscriptions"></a>Konu başlıklarını ve abonelikleri silme
Konu başlıkları ve abonelikler kalıcıdır ve açıkça olmalıdır hello aracılığıyla ya da silinmiş [Azure portal] [ Azure portal] veya program aracılığıyla. Merhaba aşağıdaki örnekte nasıl toodelete hello konu adlı gösterir `mytopic`:

```python
bus_service.delete_topic('mytopic')
```

Bir konu başlığı silindiğinde hello konu başlığıyla kaydedilen tüm abonelikleri siler. Ayrıca, abonelikler bağımsız olarak da silinebilir. Merhaba aşağıdaki kod nasıl toodelete bir abonelik adlı gösterir `HighMessages` hello gelen `mytopic` konu:

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a>Sonraki adımlar
Artık Service Bus konu başlıklarını hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

* Bkz: [kuyruklar, konu başlıkları ve abonelikler][Queues, topics, and subscriptions].
* İçin başvuru [SqlFilter.SqlExpression][SqlFilter.SqlExpression].

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
