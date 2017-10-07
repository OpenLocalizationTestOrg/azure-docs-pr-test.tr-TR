---
title: "aaaHow toouse Service Bus kuyrukları Node.js içinde | Microsoft Docs"
description: "Hizmet veri yolu toouse Azure'da bir Node.js uygulamasını nasıl kuyruklar öğrenin."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a>Node.js ile nasıl toouse Service Bus kuyrukları

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Bu makalede, Node.js ile nasıl toouse Service Bus kuyrukları açıklanmaktadır. Merhaba örnekler JavaScript'te yazılmış ve hello Node.js Azure modülü kullanın. Merhaba kapsanan senaryolar dahil **sıra oluşturma**, **ileti gönderme ve alma**, ve **sıraları silme**. Merhaba kuyruklar hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a>Node.js uygulaması oluşturma
Boş bir Node.js uygulaması oluşturun. Yönergeler için toocreate bir Node.js uygulaması bkz [oluşturma ve bir Node.js uygulaması tooan Azure Web sitesi dağıtma][Create and deploy a Node.js application tooan Azure Website], veya [Node.js bulut hizmeti] [ Node.js Cloud Service] Windows PowerShell kullanarak.

## <a name="configure-your-application-toouse-service-bus"></a>Uygulama toouse Service Bus yapılandırın
toouse Azure Service Bus, indirin ve hello Node.js Azure paketini kullanın. Bu paket hello Service Bus REST Hizmetleri ile iletişim kitaplıkları kümesi içerir.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Düğüm paketi Yöneticisi (NPM) tooobtain hello paketini kullanın
1. Kullanım hello **Node.js için Windows PowerShell** komut penceresinde toonavigate toohello **c:\\düğümü\\sbqueues\\WebRole1** içinde oluşturduğunuz klasörü, örnek uygulama.
2. Tür **npm yükleme azure** hello komut penceresinde, neden çıktı benzer toohello aşağıdakileri:

    ```
    azure@0.7.5 node_modules\azure
        ├── dateformat@1.0.2-1.2.3
        ├── xmlbuilder@0.4.2
        ├── node-uuid@1.2.0
        ├── mime@1.2.9
        ├── underscore@1.4.4
        ├── validator@1.1.1
        ├── tunnel@0.0.2
        ├── wns@0.5.3
        ├── xml2js@0.2.7 (sax@0.5.2)
        └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
    ```
3. Merhaba el ile çalıştırabilirsiniz **ls** komutu tooverify, bir **node_modules** klasörü oluşturuldu. Bu klasör Bul hello içinde **azure** tooaccess Service Bus kuyruklarını ihtiyacınız hello kitaplıklarını içeren paket.

### <a name="import-hello-module"></a>İçeri aktarma hello Modülü
Not Defteri'nde veya başka bir metin düzenleyicisi kullanarak eklemek hello toohello üstündeki aşağıdaki hello **server.js** hello uygulama dosyası:

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a>Bir Azure hizmet veri yolu bağlantı kurma
Hello Azure modül okur hello ortam değişkeni `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain bilgi tooconnect tooService veri yolu gerekiyor. Bu ortam değişkenini ayarlanmamışsa çağrılırken hello hesap bilgileri belirtmelisiniz `createServiceBusService`.

Azure bulut hizmeti için yapılandırma dosyasında hello ortam değişkenlerini ayarlama örneği için bkz: [depolama Node.js bulut hizmetiyle][Node.js Cloud Service with Storage].

Hello hello ortam değişkenlerini ayarlama örneği için [Azure portal] [ Azure portal] bir Azure Web sitesi için bkz: [Node.js Web uygulaması depolama ile] [ Node.js Web Application with Storage].

## <a name="create-a-queue"></a>Bir kuyruk oluşturma
Merhaba **ServiceBusService** nesnesi, Service Bus kuyrukları ile toowork sağlar. Merhaba aşağıdaki kod oluşturur bir **ServiceBusService** nesnesi. Merhaba hello yukarıya yakın eklemek **server.js** hello deyimi tooimport hello Azure modülü sonra dosyayı:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Çağırarak `createQueueIfNotExists` hello üzerinde **ServiceBusService** nesnesi, hello belirtilen sıra döndürülür (varsa) veya hello belirtilen ada sahip yeni bir sıra oluşturulur. Merhaba aşağıdaki kod kullanır `createQueueIfNotExists` toocreate veya adlı toohello sıra bağlanmak `myqueue`:

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

Merhaba `createServiceBusService` yöntemi de ileti zaman toolive veya en büyük sıra boyutu gibi toooverride varsayılan sıra ayarları etkinleştirmek ek seçenekleri destekler. Merhaba aşağıdaki örnek hello en büyük sıra boyutu too5 GB ve bir süre toolive (TTL) değerini 1 dakika ayarlar:

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a>Filtreler
İsteğe bağlı filtreleme operations kullanılarak gerçekleştirilen uygulanan toooperations olabilir **ServiceBusService**. İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. Filtreleri hello imza yöntemiyle uygulayan nesneler şunlardır:

```javascript
function handle (requestOptions, next)
```

Ön işleme hello isteği seçenekleri yaptıktan sonra hello yöntemini çağırmalı `next`, bir geri çağırma imza aşağıdaki hello ile geçirme:

```javascript
function (returnObject, finalCallback, next)
```

İşleme hello sonra bu geri çağırma `returnObject` (Merhaba isteği toohello sunucudan yanıt hello) hello geri çağırma gerekir ya da çağırma `next` , diğer filtrelerle işleme toocontinue var veya yalnızca çağırma `finalCallback`, hangi sona erer Merhaba hizmet başlatma.

Yeniden deneme mantığını uygulaması iki filtre hello Node.js için Azure SDK ile birlikte `ExponentialRetryPolicyFilter` ve `LinearRetryPolicyFilter`. Merhaba aşağıdaki kod oluşturur bir `ServiceBusService` hello kullanan nesneyi `ExponentialRetryPolicyFilter`:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a>İletileri tooa sırası Gönder
ileti tooa Service Bus kuyruğuna toosend, uygulamanızın çağırır hello `sendQueueMessage` hello yöntemi **ServiceBusService** nesnesi. İletileri çok gönderilen (ve öğesinden alınan) hizmet kuyruklar veri yolu **BrokeredMessage** nesneleri ve bir standart özellikler kümesi sahip (gibi **etiket** ve **TimeToLive**), kullanılan toohold özel uygulamaya özgü özellikler ve rastgele uygulama verileri gövdesi sözlüğü. Bir uygulama, bir dize selamlama iletisine geçirerek hello hello ileti gövdesi ayarlayabilirsiniz. Gerekli tüm standart özellikleri varsayılan değerlerle doldurulur.

Merhaba aşağıdaki örnekte nasıl toosend adlı bir sınama iletisi toohello sırası gösteren `myqueue` kullanarak `sendQueueMessage`:

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

Service Bus kuyruklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md). Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir. Merhaba bir kuyrukta tutulan ileti sayısına bir sınır yoktur ancak kuyruk tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur. Bu kuyruk boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir. Kotalar hakkında daha fazla bilgi için bkz: [Service Bus kotaları][Service Bus quotas].

## <a name="receive-messages-from-a-queue"></a>Kuyruktan ileti alma
İletileri hello kullanarak bir kuyruktan alınan `receiveQueueMessage` hello yöntemi **ServiceBusService** nesnesi. Varsayılan olarak, bunlar okurken iletiler hello sıradan silinir; Ancak, (Özet) okuma ve kilitleme selamlama iletisine hello isteğe bağlı parametre ayarı tarafından hello sıradan silmeden `isPeekLock` çok**doğru**.

Okuma varsayılan davranışını hello ve hello parçası işlemi aldıklarında hello iletisi siliniyor hello en basit modeldir ve uygulamanın bir hatanın hello Olay iletisinde işlenmiyor dayanabileceği senaryolarda en iyi şekilde çalışır. toounderstand Bu, hangi hello tüketici sorunları hello alma isteği bir senaryo düşünün ve işlemeden önce çöküyor. Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.

Merhaba, `isPeekLock` parametresi çok ayarlanırsa**true**, hello alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur. Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur. Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), hello hello ikinci aşamasını tamamlar çağırarak alma işleminin `deleteMessage` yöntemi ve parametre olarak silinmiş hello ileti toobe sağlama. Merhaba `deleteMessage` yöntemi hello iletiyi kullanılıyor olarak işaretler ve hello kuyruktan kaldırır.

Merhaba aşağıdaki örnekte nasıl tooreceive ve işlem iletileri kullanarak gösteren `receiveQueueMessage`. Merhaba örnek ilk alır ve bir iletiyi siler ve kullanarak bir ileti alır `isPeekLock` çok ayarlamak**true**, iletiyi kullanarak siler hello sonra `deleteMessage`:

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri
Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar. Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlockMessage` hello yöntemi **ServiceBusService** nesnesi. Bu hizmet veri yolu toounlock hello sıra içinde ileti neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.

Ayrıca hello kuyrukta kilitlenen iletiye ilişkin bir zaman aşımı vardır ve hello tooprocess önce iletiyi hello hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus selamlama iletisine otomatik olarak kilitlenmeden kilit zaman aşımı dolmadan ve yeniden alınan kullanılabilir toobe yapın.

Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `deleteMessage` yöntemi çağrıldıktan sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır. Bu genellikle adlandırılır *en az bir kez işleme*, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim. Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir. Bu genellikle hello kullanılarak elde edilen **MessageID** teslimat denemelerinde hello iletinin özelliği.

## <a name="next-steps"></a>Sonraki adımlar
Kuyruklar hakkında daha fazla toolearn kaynakları aşağıdaki hello bakın.

* [Kuyruklar, konu başlıkları ve abonelikler][Queues, topics, and subscriptions]
* [Düğümü için Azure SDK] [ Azure SDK for Node] github'daki
* [Node.js Geliştirici Merkezi](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
