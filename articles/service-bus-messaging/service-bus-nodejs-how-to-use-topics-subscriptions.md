---
title: "aaaHow toouse Azure Service Bus konuları ve abonelikleri Node.js ile | Microsoft Docs"
description: "Bilgi nasıl toouse Service Bus konuları ve bir Node.js uygulaması Azure aboneliklerinde."
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b9f5db85-7b6c-4cc7-bd2c-bd3087c99875
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: e8f6e7ad6ed16d844c408337ac9e50f990e3fafd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-nodejs"></a>Nasıl tooUse Service Bus konuları ve abonelikleri Node.js ile

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Bu kılavuzda açıklanmaktadır nasıl toouse Service Bus konuları ve abonelikleri Node.js uygulamalardan. Merhaba kapsanan senaryolar dahil **konuları ve abonelikleri oluşturma**, **abonelik filtreleri oluşturma**, **ileti gönderme** tooa konu **alma bir abonelik iletilerden**, ve **konuları ve abonelikleri silmeyi**. Merhaba konu başlıkları ve abonelikler hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next-steps) bölümü.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-nodejs-application"></a>Node.js uygulaması oluşturma
Boş bir Node.js uygulaması oluşturun. Bir Node.js uygulaması oluşturma ile ilgili yönergeler için bkz: [oluşturma ve bir Node.js uygulaması tooan Azure Web sitesi dağıtma], [Node.js bulut hizmeti] [ Node.js Cloud Service] Windows kullanma PowerShell veya Web sitesini WebMatrix ile.

## <a name="configure-your-application-toouse-service-bus"></a>Uygulama toouse Service Bus yapılandırın
Hizmet veri yolu, toouse hello Node.js Azure paketini indirin. Bu paket hello Service Bus REST Hizmetleri ile iletişim kitaplıkları kümesi içerir.

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a>Düğüm paketi Yöneticisi (NPM) tooobtain hello paketini kullanın
1. Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows) **Terminal** (Mac) veya **Bash** (UNIX) örnek uygulamanızı oluşturulduğu toohello klasörüne gidin.
2. Tür **npm yükleme azure** hello komut penceresinde, neden çıktı aşağıdaki hello:

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
3. Merhaba el ile çalıştırabilirsiniz **ls** komutu tooverify, bir **düğümü\_modülleri** klasörü oluşturuldu. Bu klasöre Bul **azure** tooaccess Service Bus konu başlıklarını ihtiyacınız hello kitaplıklarını içeren paket.

### <a name="import-hello-module"></a>İçeri aktarma hello Modülü
Not Defteri'nde veya başka bir metin düzenleyicisi kullanarak eklemek hello toohello üstündeki aşağıdaki hello **server.js** hello uygulama dosyası:

```javascript
var azure = require('azure');
```

### <a name="set-up-a-service-bus-connection"></a>Hizmet veri yolu bağlantı kurma
Hello Azure modül okur hello ortam değişkenleri `AZURE_SERVICEBUS_NAMESPACE` ve `AZURE_SERVICEBUS_ACCESS_KEY` için bilgi tooconnect tooService veri yolu gerekiyor. Bu ortam değişkenleri ayarlanmamışsa çağrılırken hello hesap bilgileri belirtmelisiniz `createServiceBusService`.

Azure bulut hizmeti için hello ortam değişkenlerini ayarlama örneği için bkz: [depolama Node.js bulut hizmetiyle][Node.js Cloud Service with Storage].

Bir Azure Web sitesi için hello ortam değişkenlerini ayarlama örneği için bkz: [Node.js Web uygulaması depolama ile][Node.js Web Application with Storage].

## <a name="create-a-topic"></a>Konu başlığı oluşturma
Merhaba **ServiceBusService** nesne konuları ile toowork sağlar. Aşağıdaki kod oluşturur bir **ServiceBusService** nesnesi. Merhaba en üstüne yakın eklemek **server.js** hello deyimi tooimport hello azure modülü sonra dosyayı:

```javascript
var serviceBusService = azure.createServiceBusService();
```

Çağırarak `createTopicIfNotExists` hello üzerinde **ServiceBusService** nesnesi, hello belirtilen konu döndürülecek (varsa) veya hello belirtilen ada sahip yeni bir konu oluşturulur. Merhaba aşağıdaki kod kullanır `createTopicIfNotExists` toocreate veya toohello konu adlı bağlantı `MyTopic`:

```javascript
serviceBusService.createTopicIfNotExists('MyTopic',function(error){
    if(!error){
        // Topic was created or exists
        console.log('topic created or exists.');
    }
});
```

Merhaba `createServiceBusService` yöntemi de ileti yaşam süresi veya en büyük konu boyutu gibi toooverride varsayılan konu ayarlarını etkinleştir ek seçenekleri destekler. Merhaba aşağıdaki örnek hello en fazla konu boyutu too5GB süresi olan 1 dakika toolive ayarlar:

```javascript
var topicOptions = {
        MaxSizeInMegabytes: '5120',
        DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createTopicIfNotExists('MyTopic', topicOptions, function(error){
    if(!error){
        // topic was created or exists
    }
});
```

### <a name="filters"></a>Filtreler
İsteğe bağlı filtreleme operations kullanılarak gerçekleştirilen uygulanan toooperations olabilir **ServiceBusService**. İşlemleri filtreleme içerebilir günlüğe kaydetme, otomatik olarak yeniden deneniyor, vs. Filtreleri hello imza yöntemiyle uygulayan nesneler şunlardır:

```javascript
function handle (requestOptions, next)
```

Yöntem çağrıları hello Hello isteği seçenekleri ön işleme gerçekleştirdikten sonra `next`, bir geri çağırma imza aşağıdaki hello ile geçirme:

```javascript
function (returnObject, finalCallback, next)
```

İşleme hello sonra bu geri çağırma `returnObject` (Merhaba isteği toohello sunucudan yanıt hello) hello geri çağırma tooeither gereken diğer filtreleri işleme toocontinue varsa sonraki çağırma veya çağırma `finalCallback` Aksi takdirde tooend hello Hizmet başlatma.

Yeniden deneme mantığını uygulaması iki filtre hello Node.js için Azure SDK ile birlikte **ExponentialRetryPolicyFilter** ve **LinearRetryPolicyFilter**. Merhaba aşağıdaki oluşturur bir **ServiceBusService** hello kullanan nesneyi **ExponentialRetryPolicyFilter**:

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="create-subscriptions"></a>Abonelikleri oluşturma
Konu aboneliklerini ayrıca hello ile oluşturulan **ServiceBusService** nesnesi. Abonelikler adlandırılır ve hello toohello aboneliğin sanal kuyruğuna teslim edilen ileti kümesini sınırlayan isteğe bağlı bir filtre içerebilir.

> [!NOTE]
> Abonelikleri kalıcı ve tooexist ya da bunlar kadar devam eder veya hello konu bunların ilişkili silinir. Uygulama mantığı toocreate bir abonelik içeriyorsa, ilk hello abonelik zaten kullanarak olup olmadığını kontrol edin `getSubscription` yöntemi.
>
>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Merhaba varsayılan (MatchAll) filtreyle abonelik oluşturma
Merhaba **MatchAll** yeni bir abonelik oluşturulurken filtre belirtilmeyen varsa, kullanılan hello varsayılan filtre filtredir. Ne zaman hello **MatchAll** filtre kullanıldığında, tüm iletileri yayımlanan toohello konu aboneliğin sanal kuyruğuna yerleştirilir. Merhaba aşağıdaki örnekte 'AllMessages' adlı bir abonelik oluşturur ve kullanır hello varsayılan **MatchAll** Filtresi.

```javascript
serviceBusService.createSubscription('MyTopic','AllMessages',function(error){
    if(!error){
        // subscription created
    }
});
```

### <a name="create-subscriptions-with-filters"></a>Filtre içeren abonelik oluşturma
Ayrıca hangi iletilerin tooa konu içinde belirli konu aboneliği göstermelidir gönderilen tooscope izin filtreler oluşturabilirsiniz.

Merhaba en esnek filtre abonelikler tarafından desteklenen türünde **SqlFilter**, SQL92 alt kümesi uygular. SQL filtreleri yayımlanan toohello konu hello iletilerinin hello özelliklerini çalışır. Merhaba SQL Filtresi ile kullanılabilen hello ifadeler hakkında daha fazla ayrıntı için gözden [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] sözdizimi.

Filtreler eklenebilir tooa abonelik hello kullanarak `createRule` hello yöntemi **ServiceBusService** nesnesi. Bu yöntem yeni filtreleri tooan varolan abonelik eklemenize olanak tanır.

> [!NOTE]
> Merhaba varsayılan filtre otomatik olarak uygulandığından tooall yeni abonelikler, ilk hello varsayılan filtreyi kaldırmalısınız veya **MatchAll** belirttiğiniz diğer filtreleri geçersiz kılar. Hello kullanarak hello varsayılan kural kaldırabilirsiniz `deleteRule` yöntemi **ServiceBusService** nesnesi.
>
>

Merhaba aşağıdaki örnek adlı bir abonelik oluşturulur `HighMessages` ile bir **SqlFilter** özel iletileri yalnızca seçer `messagenumber` özelliği 3'ten büyük:

```javascript
serviceBusService.createSubscription('MyTopic', 'HighMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'HighMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber > 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'HighMessages',
            'HighMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

Benzer şekilde, hello aşağıdaki örnek adlı bir abonelik oluşturur `LowMessages` ile bir **SqlFilter** olan iletiler yalnızca seçer bir `messagenumber` özelliği daha az veya bu değere eşit too3:

```javascript
serviceBusService.createSubscription('MyTopic', 'LowMessages', function (error){
    if(!error){
        // subscription created
        rule.create();
    }
});
var rule={
    deleteDefault: function(){
        serviceBusService.deleteRule('MyTopic',
            'LowMessages',
            azure.Constants.ServiceBusConstants.DEFAULT_RULE_NAME,
            rule.handleError);
    },
    create: function(){
        var ruleOptions = {
            sqlExpressionFilter: 'messagenumber <= 3'
        };
        rule.deleteDefault();
        serviceBusService.createRule('MyTopic',
            'LowMessages',
            'LowMessageFilter',
            ruleOptions,
            rule.handleError);
    },
    handleError: function(error){
        if(error){
            console.log(error)
        }
    }
}
```

Ne zaman bir ileti artık gönderilir çok`MyTopic`, her zaman alıcılara toohello teslim `AllMessages` konu aboneliği ve abone olunan seçmeli olarak teslim tooreceivers toohello `HighMessages` ve `LowMessages` konu abonelikleri (Merhaba ileti içeriği bağlı olarak).

## <a name="how-toosend-messages-tooa-topic"></a>Nasıl toosend tooa konu iletileri
toosend ileti tooa Service Bus konu, uygulamanızı kullanmalıdır `sendTopicMessage` hello yöntemi **ServiceBusService** nesnesi.
Gönderilen iletileri tooService veri yolu konuları **BrokeredMessage** nesneleri.
**BrokeredMessage** nesneleri olan bir standart özellikler kümesi (gibi `Label` ve `TimeToLive`), kullanılan toohold özel uygulamaya özgü özellikler sözlüğü bir ve dize verileri gövdesi içerir. Bir uygulama hello bir dize değeri geçirerek hello hello ileti gövdesini ayarlayabilir `sendTopicMessage` ve gereken tüm standart özellikleri varsayılan değerlerle doldurulmuş.

Merhaba aşağıdaki örnekte nasıl toosend beş için sınama iletilerini gösterir `MyTopic`. Bu hello Not `messagenumber` her ileti özelliği değeri değişir hello döngü hello yinelemesi (Bu alacak abonelikleri belirler):

```javascript
var message = {
    body: '',
    customProperties: {
        messagenumber: 0
    }
}

for (i = 0;i < 5;i++) {
    message.customProperties.messagenumber=i;
    message.body='This is Message #'+i;
    serviceBusService.sendTopicMessage(topic, message, function(error) {
      if (error) {
        console.log(error);
      }
    });
}
```

Service Bus konu başlıklarını destek maksimum ileti boyutu 256 KB hello [standart katmanı](service-bus-premium-messaging.md) hello 1 MB [Premium katmanı](service-bus-premium-messaging.md). Merhaba standart ve özel uygulama özelliklerini içeren hello üstbilgi en büyük boyutu 64 KB olabilir. Merhaba konu başlığında tutulan ileti sayısına bir sınır yoktur ancak konu başlığı tarafından tutulan hello iletilerin toplam boyutu hello bir sınır yoktur. Bu konu başlığı boyutu, üst sınır 5 GB olacak şekilde oluşturulma zamanında belirlenir.

## <a name="receive-messages-from-a-subscription"></a>Abonelikten ileti alma
İletileri kullanarak bir abonelik alınan `receiveSubscriptionMessage` hello yöntemi **ServiceBusService** nesnesi. Varsayılan olarak, bunlar okurken iletiler hello abonelikten silinir; Ancak, (Özet) okuma ve kilitleme selamlama iletisine hello isteğe bağlı parametre ayarı tarafından hello abonelikten silmeden `isPeekLock` çok**doğru**.

Okuma ve alma işleminin parçası hello en basit modeldir ve uygulamanın bir hatanın hello Olay iletisinde işlenmiyor dayanabileceği senaryoları için en iyi şekilde hello iletisi siliniyor hello varsayılan davranışı. toounderstand Bu, tüketici sorunları hello isteği alma bir senaryo düşünün ve işlemeden önce çöküyor. Hizmet veri yolu selamlama iletisine hello uygulama yeniden başlatılıp iletileri tekrar kullanmaya başladığında olduğunda, ardından kullanılıyor olarak işaretlenmiş için onu olan hello iletiyi atlamış olur önceki toohello kilitlenme tüketilen.

Merhaba, `isPeekLock` parametresi çok ayarlanırsa**true**, hello alma iletilere olası toosupport uygulamaları iki aşamalı işlemi olur. Service Bus bir istek aldığında hello sonraki ileti toobe tüketilen, diğer tüketicilerin alırken tooprevent kilitler ve toohello uygulama döndürür bulur.
Merhaba uygulaması hello iletiyi işlemeyi tamamladıktan sonra (veya sonra işlemek için depoladıktan sonra), çağırarak hello alma işleminin ikinci aşamasını tamamlar **deleteMessage** yöntemi ve ileti toobe sağlama parametre olarak silindi. Merhaba **deleteMessage** yöntemi hello iletiyi kullanılıyor olarak işaretler ve hello abonelikten Kaldır.

Merhaba aşağıdaki örnekte nasıl iletilerin alındığını ve işlenen kullanarak gösteren `receiveSubscriptionMessage`. Merhaba örnek ilk alır ve bir ileti hello 'LowMessages' abonelik ' siler ve sonra abonelik 'HighMessages' hello kullanarak bir ileti alır `isPeekLock` tootrue ayarlayın. Ardından hello kullanarak iletiyi siler `deleteMessage`:

```javascript
serviceBusService.receiveSubscriptionMessage('MyTopic', 'LowMessages', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
        console.log(receivedMessage);
    }
});
serviceBusService.receiveSubscriptionMessage('MyTopic', 'HighMessages', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        console.log(lockedMessage);
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
                console.log('message has been deleted.');
            }
        }
    }
});
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Nasıl toohandle uygulaması kilitlenir ve Okunmayan iletileri
Hizmet veri yolu, gerçekleşen hataları uygulama ya da ileti işlenirken zorlukları rahat işlevselliği toohelp sağlar. Alıcı uygulamanın kaydedemediği tooprocess Merhaba ileti herhangi bir nedenden dolayı ardından hello çağırabilirsiniz `unlockMessage` yöntemi **ServiceBusService** nesnesi. Bu hizmet veri yolu toounlock hello abonelik içindeki ileti neden ve yeniden alınan kullanılabilir toobe olun, ya da göre aynı uygulama veya başka bir kullanıcı uygulama tarafından tüketen hello.

Ayrıca abonelikte kilitlenen iletiye ilişkin bir zaman aşımı vardır ve tooprocess selamlama iletisine önce hello uygulama başarısız olursa (örneğin, hello uygulama çökerse) Service Bus hello iletinin kilidini açar hello kilit zaman aşımı dolmadan otomatik olarak yeniden alınan kullanılabilir toobe yapar.

Merhaba ileti işlenirken sonra ancak hello önce uygulama hello olay Hello çöküyor `deleteMessage` yöntemi çağrıldıktan sonra başlatıldığında hello ileti yeniden teslim toohello uygulama olacaktır. Bu genellikle adlandırılır *en az bir kez işleme*, diğer bir deyişle, her ileti en az bir kez işlenir ancak belirli durumlarda hello aynı ileti yeniden teslim. Merhaba senaryo yinelenen işlemeyi kabul etmiyorsa, uygulama geliştiricilerinin ek mantık tootheir uygulama toohandle yinelenen ileti teslimi eklemeniz gerekir. Bu genellikle kullanılarak elde edilen **MessageID** teslimat denemelerinde hello iletinin özelliği.

## <a name="delete-topics-and-subscriptions"></a>Konu başlıklarını ve abonelikleri silme
Konu başlıkları ve abonelikler kalıcıdır ve açıkça olmalıdır hello aracılığıyla ya da silinmiş [Azure portal] [ Azure portal] veya program aracılığıyla.
Merhaba aşağıdaki örnekte nasıl toodelete hello konu adlı gösteren `MyTopic`:

```javascript
serviceBusService.deleteTopic('MyTopic', function (error) {
    if (error) {
        console.log(error);
    }
});
```

Konu başlığı silindiğinde hello konu başlığıyla kaydedilen tüm abonelikler de silinir. Ayrıca, abonelikler bağımsız olarak da silinebilir. Aşağıdaki örnek, nasıl bir abonelik toodelete adlı gösterir `HighMessages` hello gelen `MyTopic` konu:

```javascript
serviceBusService.deleteSubscription('MyTopic', 'HighMessages', function (error) {
    if(error) {
        console.log(error);
    }
});
```

## <a name="next-steps"></a>Sonraki Adımlar
Artık Service Bus konu başlıklarını hello temellerini öğrendiğinize göre daha fazla bu bağlantılar toolearn izleyin.

* Bkz: [kuyruklar, konu başlıkları ve abonelikler][Queues, topics, and subscriptions].
* [SqlFilter][SqlFilter] için API başvurusu.
* Merhaba ziyaret [düğümü için Azure SDK] [ Azure SDK for Node] github'daki.

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[oluşturma ve bir Node.js uygulaması tooan Azure Web sitesi dağıtma]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
