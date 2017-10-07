---
title: "Azure Service Bus kullanarak performansı artırmak için aaaBest yöntemler | Microsoft Docs"
description: "Nasıl toouse alışverişi sırasında Service Bus toooptimize performans iletileri aracılı açıklar."
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e756c15d-31fc-45c0-8df4-0bca0da10bb2
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/10/2017
ms.author: sethm
ms.openlocfilehash: 52764d227757cbb11246675878933f21685817f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-performance-improvements-using-service-bus-messaging"></a>Service Bus Mesajlaşma hizmeti kullanarak performans iyileştirmeleri için en iyi yöntemler

Bu makalede nasıl toouse [Azure Service Bus Mesajlaşma](https://azure.microsoft.com/services/service-bus/) alışverişi sırasında toooptimize performans aracılı iletiler. Bu konunun ilk bölümü Hello toohelp performansı artırır sunulan hello farklı mekanizmaları açıklar. Merhaba ikinci bölümü Kılavuzu nasıl toouse Service Bus sunabileceğiniz şekilde hello belirli bir senaryo en iyi performans sağlar.

Bu konu boyunca hello terimi "istemci" Service Bus erişen tooany varlık anlamına gelir. Bir istemci bir gönderici veya bir alıcı hello rolüne alabilir. Merhaba terimi "gönderen" iletileri tooa hizmet veri yolu kuyruğu ya da konu gönderdiği Service Bus kuyruk veya konu istemci için kullanılır. Merhaba terimi "alıcı" hizmet veri yolu kuyruğu ya da abonelik iletileri alan tooa hizmet veri yolu kuyruğu ya da abonelik istemci anlamına gelir.

Bu bölümler Service Bus toohelp artırma performans kullandığını birkaç kavramları tanıtır.

## <a name="protocols"></a>Protokoller
Hizmet veri yolu istemcileri toosend sağlar ve üç protokolden birini aracılığıyla iletileri alabilirsiniz:

1. Gelişmiş Message Queuing Protokolü (AMQP)
2. Service Bus Mesajlaşma protokolünü (SBMP)
3. HTTP

Merhaba Mesajlaşma fabrikası var olduğu sürece bunlar hello bağlantı tooService Bus korumak için AMQP ve SBMP daha etkili olurlar. Ayrıca, toplu işleme ve prefetching uygular. Açıkça belirtilmediği sürece, bu konudaki tüm içeriğin AMQP veya SBMP hello kullanımını varsayar.

## <a name="reusing-factories-and-clients"></a>Oluşturucular ve istemcilerin yeniden kullanma
Service Bus istemci nesneleri, gibi [QueueClient] [ QueueClient] veya [MessageSender][MessageSender], aracılığıyla oluşturulan bir [Eventhubclient] [ MessagingFactory] bağlantılarının iç yönetimi de sağlayan nesne. İleti gönderme ve hello sonraki ileti gönderirken daha sonra yeniden oluşturduktan sonra ileti oluşturucuları veya kuyruk, konu ve abonelik istemcileri kapatmalısınız değil. Bir Mesajlaşma fabrikası kapatma hello bağlantı toohello Service Bus hizmetini siler ve yeni bir bağlantı hello Fabrika yeniden zaman kurulur. Yeniden kullanarak önleyebilirsiniz pahalı bir işlem hello aynı Fabrika ve istemci bir bağlantıdır oluşturma için birden çok operations nesneleri. Güvenli bir şekilde hello kullanabilirsiniz [QueueClient] [ QueueClient] eşzamanlı zaman uyumsuz işlemleri ve birden çok iş parçacığı ileti göndermek için nesne. 

## <a name="concurrent-operations"></a>Eşzamanlı operasyonlar
Bir işlemi gerçekleştirilirken (gönderme, alma, silme, vb.) biraz zaman alabilir. Bu süre hello işlemi hello işlenmesini hello Service Bus hizmeti tarafından hello istek ve hello yanıt toohello gecikme ekleme içerir. saat başına işlemlerinin tooincrease hello sayısı, işlemler aynı anda yürütmeniz gerekir. Birkaç farklı yolla bunu yapabilirsiniz:

* **Zaman uyumsuz işlemleri**: hello istemci işlemlerini zaman uyumsuz işlemleri gerçekleştirerek zamanlar. Merhaba önceki isteği tamamlanmadan önce hello sonraki isteği başlatıldı. Merhaba, zaman uyumsuz gönderme işlemi örneği aşağıdadır:
  
 ```csharp
  BrokeredMessage m1 = new BrokeredMessage(body);
  BrokeredMessage m2 = new BrokeredMessage(body);
  
  Task send1 = queueClient.SendAsync(m1).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #1");
    });
  Task send2 = queueClient.SendAsync(m2).ContinueWith((t) => 
    {
      Console.WriteLine("Sent message #2");
    });
  Task.WaitAll(send1, send2);
  Console.WriteLine("All messages sent");
  ```
  
  Bu bir örnektir zaman uyumsuz bir alma işlemi:
  
  ```csharp
  Task receive1 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  Task receive2 = queueClient.ReceiveAsync().ContinueWith(ProcessReceivedMessage);
  
  Task.WaitAll(receive1, receive2);
  Console.WriteLine("All messages received");
  
  async void ProcessReceivedMessage(Task<BrokeredMessage> t)
  {
    BrokeredMessage m = t.Result;
    Console.WriteLine("{0} received", m.Label);
    await m.CompleteAsync();
    Console.WriteLine("{0} complete", m.Label);
  }
  ```
* **Birden çok oluşturucuları**: tarafından oluşturulan tüm istemciler (toplama tooreceivers Gönderenler) hello aynı Fabrika paylaşım bir TCP bağlantısı. Merhaba maksimum ileti işleme hello bu TCP bağlantısı üzerinden gidebilirsiniz işlemlerinin sayısı sınırlıdır. tek bir Fabrika ile elde edilebilir hello verimlilik TCP gidiş dönüş süreleri ve ileti boyutu olmadığına göre değişir. tooobtain yüksek işleme hızları, birden çok Mesajlaşma oluşturucuları kullanmanız gerekir.

## <a name="receive-mode"></a>Mod alma
Bir kuyruk veya abonelik istemci oluştururken, alma modu belirtebilirsiniz: *gözlem kilidinin* veya *alma ve silme*. Merhaba varsayılan alma modu olan [PeekLock][PeekLock]. Bu modda çalışırken hello istemci isteği tooreceive hizmet yolundan bir ileti gönderir. Merhaba istemci selamlama iletisine aldıktan sonra bir istek toocomplete hello iletisi gönderir.

Merhaba ayarı aldığınızda modu çok[ReceiveAndDelete][ReceiveAndDelete], her iki adım tek bir istekte birleştirilir. Bu hello işlemlerini Genel sayı azaltır ve hello artırabilir Genel ileti üretilen işi. Bu performans kazancı iletileri kaybı hello risk gelir.

Hizmet veri yolu, alma ve silme işlemleri için işlemleri desteklemiyor. Ayrıca, hangi hello istemci istediği toodefer tüm senaryolar için gözlem kilidinin semantiği gereklidir veya [sahipsiz](service-bus-dead-letter-queues.md) bir ileti.

## <a name="client-side-batching"></a>İstemci-tarafı toplu işleme
İstemci-tarafı toplu işleme, kuyruk veya konu istemci toodelay hello bir ileti belirli bir süre gönderme sağlar. Merhaba istemci bu süre içinde ek iletiler gönderirse, tek bir toplu hello iletilerinde iletir. İstemci-tarafı toplu işleme ayrıca neden olan kuyruk veya abonelik istemci toobatch birden çok **tam** tek bir istek isteklerine. Toplu işleme yüklenebilir yalnızca zaman uyumsuz **Gönder** ve **tam** işlemleri. Zaman uyumlu işlemler hemen toohello Service Bus hizmetini gönderilir. Toplu işleme için gözlem oluşur veya değil alma işlemleri ya da toplu işleme istemciler arasında etmiyorsa.

Varsayılan olarak, istemci bir toplu iş aralığı 20ms kullanır. Ayarı hello tarafından hello toplu aralığını değiştirebilirsiniz [BatchFlushInterval] [ BatchFlushInterval] oluşturmadan önce özelliği hello Mesajlaşma. Bu ayar bu fabrikası tarafından oluşturulan tüm istemcilerini etkiler.

toodisable toplu işleme, ayarlamak hello [BatchFlushInterval] [ BatchFlushInterval] özelliği çok**değeri, TimeSpan.Zero**. Örneğin:

```csharp
MessagingFactorySettings mfs = new MessagingFactorySettings();
mfs.TokenProvider = tokenProvider;
mfs.NetMessagingTransportSettings.BatchFlushInterval = TimeSpan.FromSeconds(0.05);
MessagingFactory messagingFactory = MessagingFactory.Create(namespaceUri, mfs);
```

Toplu işleme Faturalanabilir Mesajlaşma işlemlerinin hello sayısı etkilemez ve yalnızca hello Service Bus istemci protokolü kullanılabilir. Toplu işleme Hello HTTP protokolünü desteklemiyor.

## <a name="batching-store-access"></a>Mağaza erişimi toplu işleme
tooits iç deposu yazdığında tooincrease hello verimini kuyruk, konu veya abonelik, hizmet veri yolu birden fazla ileti toplu işlemleri. Bir kuyruk veya konu etkinleştirilirse, hello deposuna iletileri yazma toplu hale. Bir kuyruk veya abonelik etkinleştirilirse, hello deposundan iletilerini silerken toplu hale. Toplu depolama erişimi için bir varlık etkinleştirilirse, hizmet veri yolu tarafından varlık too20ms ayarlama ile ilgili bir depolama yazma işlemi geciktirir. Bu zaman aralığı boyunca gerçekleşen ek depolama işlem toohello toplu eklenir. Toplu depolama erişim yalnızca etkiler **Gönder** ve **tam** işlemleri; alma işlemleri etkilenmez. Toplu depolama erişim bir varlığı üzerinde bir özelliktir. Toplu işleme toplu depolama erişimi etkinleştir tüm varlıklar arasında oluşur.

Yeni Kuyruk, konu veya abonelik oluştururken, toplu depolama erişim varsayılan olarak etkindir. toodisable toplu depolama erişim, kümesi hello [EnableBatchedOperations] [ EnableBatchedOperations] özelliği çok**false** hello varlık oluşturmadan önce. Örneğin:

```csharp
QueueDescription qd = new QueueDescription();
qd.EnableBatchedOperations = false;
Queue q = namespaceManager.CreateQueue(qd);
```

Toplu depolama erişim Faturalanabilir Mesajlaşma işlemlerinin hello sayısı etkilemez ve kuyruk, konu veya abonelik bir özelliğidir. Merhaba bağımsız bir istemci ve hello Service Bus hizmeti arasında kullanılan modu ve hello Protokolü alırsınız.

## <a name="prefetching"></a>Prefetching
Bir alma işlemi gerçekleştirirken prefetching hello sıra ya da abonelik istemci tooload ek iletiler hello hizmetinden sağlar. Merhaba istemci bu iletiler bir yerel önbellekte depolar. Merhaba hello önbellek boyutunu hello tarafından belirlenir [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] veya [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] Özellikler. Prefetching sağlayan her bir istemci kendi önbelleğini korur. Bir önbellek istemcileri arasında paylaşılmaz. Merhaba istemci alma işlemi başlatır ve önbelleğinde boş ise, hello hizmet toplu iletiler iletir. Merhaba toplu iş boyutu Hello hello önbellek veya 256 KB hello boyutu eşittir, hangisi daha küçüktür. Merhaba istemci alma işlemi başlatır ve bir ileti hello önbellek içeriyorsa, selamlama iletisine hello önbellekten alınır.

Ne zaman bir ileti prefetched, hello hizmet kilitleri hello prefetched iletisi. Bunu yaparak, farklı bir alıcı tarafından hello prefetched ileti alınamıyor. Merhaba kilit süresi dolmadan önce hello alıcı selamlama iletisine tamamlanamazsa, selamlama iletisine kullanılabilir tooother alıcıları haline gelir. Merhaba iletinin kopyasını prefetched hello hello önbellekte kalır. Merhaba hello tüketir alıcı önbelleğe alınan süresi kopyalama ileti toocomplete çalıştığında, bir özel durum alır. Varsayılan olarak, hello ileti kilidi 60 saniye sonra süresi dolar. Bu değer, genişletilmiş too5 dakika olabilir. süresi dolan iletileri tooprevent hello tüketimini, hello önbellek boyutu her zaman bir istemci tarafından hello kilit zaman aşımı aralığı içinde kullanılabilecek iletileri hello sayısından küçük olmalıdır.

Hello varsayılan kilidi 60 saniye süre sonu kullanırken, iyi bir değer için [SubscriptionClient.PrefetchCount] [ SubscriptionClient.PrefetchCount] en fazla 20 kez hello hello Factory tüm alıcıları oranları işliyor. Örneğin, bir Fabrika 3 alıcıları oluşturur ve her alıcı too10 iletilerini saniye başına işleyebilir. Merhaba hazırlık sayısı, 20 X 3 X 10 = 600 aşamaz. Varsayılan olarak, [QueueClient.PrefetchCount] [ QueueClient.PrefetchCount] hiçbir ek iletiler hello hizmetinden getirilen anlamına gelir kümesi too0 değil.

Merhaba ileti işlemleri veya gidiş dönüş Genel sayı azalttığı için sıra veya abonelik genel üretilen işi artar hello iletileri prefetching. Merhaba ilk ileti getirme ancak, bu kadar (artan toohello ileti boyutu) daha uzun sürer. Bu iletiler hello istemci tarafından önceden yüklenmiş olan çünkü prefetched iletileri alma daha hızlı olacaktır.

Hello yaşam süresi (TTL) özelliği, bir iletinin hello sunucu hello ileti toohello istemci gönderir hello aynı anda hello sunucu tarafından denetlenir. Merhaba iletisi alındığında hello istemci selamlama iletisine'nın TTL özelliği denetlemez. Bunun yerine, selamlama iletisine hello iletinin TTL selamlama iletisine hello istemci tarafından önbelleğe olsa bile geçtiyse alınabilir.

Prefetching Faturalanabilir Mesajlaşma işlemlerinin hello sayısı etkilemez ve yalnızca hello Service Bus istemci protokolü kullanılabilir. Merhaba HTTP protokolü prefetching desteklemez. Prefetching zaman uyumlu ve zaman uyumsuz alma işlemleri için kullanılabilir.

## <a name="express-queues-and-topics"></a>Kuyruklar ve konu başlıkları express

İfade varlıkları yüksek verimlilik ve düşük gecikmeli senaryolar etkinleştirin ve yalnızca hello standart Mesajlaşma katmanında desteklenir. Oluşturulan varlık [Premium ad](service-bus-premium-messaging.md) hello express seçeneğini desteklemez. Bir ileti tooa kuyruk veya konu başlığı, gönderilirse express varlıklarıyla selamlama iletisine hemen hello Mesajlaşma deposunda depolanmaz. Bunun yerine, bellekte önbelleğe alınır. Bir ileti birden çok birkaç saniye boyunca hello sırada kalırsa, böylece tooan kesilmesi nedeniyle kaybına karşı koruma toostable depolama otomatik olarak yazılır. Bir önbellek Hello iletisine verimliliğini artırır ve hiçbir erişim toostable olduğundan gecikmesini azaltır yazma hello zaman hello iletiye depolama gönderilir. Birkaç saniye içinde tüketilen ileti deposu Mesajlaşma toohello yazılmaz. Aşağıdaki örnek hello hızlı bir konu oluşturur.

```csharp
TopicDescription td = new TopicDescription(TopicName);
td.EnableExpress = true;
namespaceManager.CreateTopic(td);
```

Kayıp olmaması gereken önemli bilgileri içeren bir ileti tooan express varlık gönderilirse hello gönderici Service Bus zorlayabilirsiniz tooimmediately kalıcı hello ileti toostable depolama ayarı hello tarafından [ForcePersistence] [ ForcePersistence] özelliği çok**doğru**.

> [!NOTE]
> İfade varlıkları işlemleri desteklemez.

## <a name="use-of-partitioned-queues-or-topics"></a>Bölümlenmiş sıraları veya konuları
Dahili olarak, hizmet veri yolu kullanır aynı düğüm ve depolama tooprocess Mesajlaşma hello ve tüm iletiler için bir Mesajlaşma varlığıyla (kuyruk veya konu) depolayın. Bölümlenmiş kuyruk veya konu, üzerinde hello diğer yandan, birden çok düğüm ve mesajlaşma depoları arasında dağıtılır. Bölümlenmiş kuyruklar ve konu başlıkları yalnızca normal kuyruklar ve konu başlıkları daha yüksek verimlilik elde etmek, bunlar ayrıca üst düzey kullanılabilirlik sergiler. toocreate bölümlenmiş bir varlık kümesi hello [EnablePartitioning] [ EnablePartitioning] özelliği çok**true**hello aşağıdaki örnekte gösterildiği gibi. Bölümlenen varlıklar hakkında daha fazla bilgi için bkz: [bölümlenmiş Mesajlaşma varlıkları][Partitioned messaging entities].

```csharp
// Create partitioned queue.
QueueDescription qd = new QueueDescription(QueueName);
qd.EnablePartitioning = true;
namespaceManager.CreateQueue(qd);
```

## <a name="use-of-multiple-queues"></a>Birden çok sıraya kullanımı

Bölümlenmiş kuyruk veya konu veya hello yük tek bölümlenmiş kuyruk veya konu tarafından işlenemez beklenen olası toouse değilse, birden çok Mesajlaşma varlıkları kullanmanız gerekir. Birden çok varlık kullanırken, ayrılmış bir istemci her varlık için oluşturma, hello aynı kullanmak yerine istemci tüm varlıklar için.

## <a name="development-and-testing-features"></a>Geliştirme ve test özellikleri

Hizmet veri yolu olan özellikle geliştirme için kullanılan bir özellik olan **üretim yapılandırmalarında hiçbir zaman kullanılmalıdır**: [TopicDescription.EnableFilteringMessagesBeforePublishing][].

Yeni kurallar veya filtreler toohello konu eklendiğinde, kullanabileceğiniz [TopicDescription.EnableFilteringMessagesBeforePublishing][] yeni filtre ifadesi hello tooverify beklendiği gibi çalıştığını.

## <a name="scenarios"></a>Senaryolar
Merhaba aşağıdaki bölümlerde tipik Mesajlaşma senaryolar açıklanmaktadır ve tercih edilen hello Service Bus ayarlar alır. Verimi sınıflandırılan küçük (1 saniye başına ileti daha azını), Orta (1 saniye başına ileti veya 100'den az ancak büyük ileti/saniye) ve yüksek (100 iletileri/ikinci veya daha büyük). Merhaba istemci sayısı küçük sınıflandırılır (5 veya daha az), Orta (5'ten fazla ancak küçüktür veya eşittir too20) ve büyük (birden çok 20).

### <a name="high-throughput-queue"></a>Yüksek verimlilik sırası
Hedef: tek bir sıraya hello verimini ekranı kaplamasını sağlayın. Merhaba göndericiler ile alıcılar küçük sayısıdır.

* Bölümlenmiş bir sıra, Gelişmiş performans ve kullanılabilirlik için kullanın.
* Genel tooincrease hello hello sıraya gönderme oranı, birden çok ileti oluşturucuları toocreate Gönderenler kullanın. Her gönderen için zaman uyumsuz işlemleri veya birden çok iş parçacığı kullanın.
* Genel tooincrease hello oranı hello kuyruktan alma, birden çok ileti oluşturucuları toocreate alıcıları kullanın.
* Zaman uyumsuz işlemleri tootake avantajlarından, istemci-tarafı toplu işleme kullanın.
* Aralık too50ms tooreduce hello Service Bus istemci iletişim kuralı iletimlerini sayısı toplu işleme hello ayarlayın. Birden çok Gönderenler kullandıysanız, aralığı too100ms toplu işleme hello artırın.
* Toplu depolama erişim etkin bırakın. Bu genel hello artırır, iletileri yazılabilir hello sıraya oranı.
* Merhaba hazırlık sayısı too20 saatleri bir Factory tüm alıcıları hello en yüksek işleme hızlarını ayarlayın. Bu hizmet veri yolu istemci iletişim kuralı iletimlerini hello sayısını azaltır.

### <a name="multiple-high-throughput-queues"></a>Birden çok yüksek işleme sırası
Hedef: birden çok sıraların genel üretilen işi en üst düzeye çıkarın. tek bir kuyruk Hello verimini, Orta veya yüksek.

tooobtain birden çok sıraya arasında en yüksek verimlilik, tek bir sıraya toomaximize hello verimini hello ayarları kullan özetlenen. Ayrıca, farklı sıralarından gönderip farklı oluşturucuları toocreate istemciler kullanır.

### <a name="low-latency-queue"></a>Düşük gecikme süresi sırası
Hedef: bir kuyruk veya konu uçtan uca gecikme süresi en aza indirin. Merhaba göndericiler ile alıcılar küçük sayısıdır. küçük veya Orta hello sırasının Hello işleme.

* Bölümlenmiş bir kuyruk için geliştirilmiş kullanılabilirlik kullanın.
* İstemci-tarafı toplu işleme devre dışı bırakın. Merhaba istemci hemen bir ileti gönderir.
* Toplu iş mağazası erişimini devre dışı bırakın. Merhaba hizmet hemen hello ileti toohello deposu yazar.
* Tek bir istemci kullanıyorsanız, hello hazırlık sayısı too20 kez hello işleme hızı hello alıcı ayarlayın. Birden çok ileti hello hello sıraya aynı ulaşırsa zaman, hello Service Bus istemci protokolü iletir bunları tüm hello aynı anda. Merhaba istemci hello sonraki ileti aldığında, bu iletiyi hello yerel önbellekte zaten var. Merhaba önbellek küçük olmalıdır.
* Birden çok istemci kullanıyorsanız, hello hazırlık sayısı too0 ayarlayın. Bunu yaparak, Hello ilk istemci hala hello ilk iletiyi işlerken hello ikinci istemci hello ikinci bir ileti alabilir.

### <a name="queue-with-a-large-number-of-senders"></a>Çok sayıda Gönderenler sıraya
Hedef: bir kuyruk veya konu çok sayıda göndericiler ile verimini ekranı kaplamasını sağlayın. Her göndereni Orta oranı içeren iletileri gönderir. Merhaba, alıcılar küçük sayısıdır.

Service Bus varlık Mesajlaşma too1000 eşzamanlı bağlantı tooa sağlar (veya 5000 AMQP kullanarak). Bu sınır hello ad alanı düzeyinde uygulanır ve ad alanı başına eşzamanlı bağlantı hello sınırının tarafından konuları/sıraları/abonelikleri tutulabilir. Sıralar için bu numara göndericiler ile alıcılar arasında paylaşılır. Göndericiler için tüm 1000 bağlantıları gerekirse, bir konu ve tek bir abonelik ile Merhaba sıra değiştirmeniz gerekir. Merhaba abonelik alıcıları gelen ek bir 1000 eşzamanlı bağlantıları kabul eder ancak bir konu, gönderenlerden too1000 eşzamanlı bağlantı kurma kabul eder. 1000'den fazla eşzamanlı Gönderenler gerekirse, hello Gönderenler iletileri toohello HTTP üzerinden Service Bus Protokolü göndermesi gerekir.

toomaximize üretilen işi aşağıdaki hello:

* Bölümlenmiş bir sıra, Gelişmiş performans ve kullanılabilirlik için kullanın.
* Farklı bir işlem içinde her göndereni bulunuyorsa, işlem başına yalnızca tek bir Fabrika kullanın.
* Zaman uyumsuz işlemleri tootake avantajlarından, istemci-tarafı toplu işleme kullanın.
* Hizmet veri yolu istemci iletişim kuralı iletimlerini 20ms tooreduce hello sayısı aralığı toplu işleme hello varsayılan kullanın.
* Toplu depolama erişim etkin bırakın. Bu genel hello artırır, iletileri yazılabilir hello kuyruk veya konu oranı.
* Merhaba hazırlık sayısı too20 saatleri bir Factory tüm alıcıları hello en yüksek işleme hızlarını ayarlayın. Bu hizmet veri yolu istemci iletişim kuralı iletimlerini hello sayısını azaltır.

### <a name="queue-with-a-large-number-of-receivers"></a>Çok sayıda alıcı sırası
Hedef: hello en üst düzeye çıkarmak sıra ya da çok sayıda alıcı abonelikle oranını alırsınız. Her alıcı Orta hızında iletilerini alır. Merhaba Gönderenler küçük sayısıdır.

Hizmet veri yolu too1000 eşzamanlı bağlantı tooan varlık sağlar. Bir kuyruk 1000'den fazla alıcıları gerektiriyorsa, hello sıra konu ve birden çok abonelik ile değiştirmeniz gerekir. Her abonelik too1000 eşzamanlı bağlantıları destekleyebilir. Alternatif olarak, alıcılar hello sıra hello HTTP protokolü aracılığıyla erişebilirsiniz.

toomaximize üretilen işi aşağıdaki hello:

* Bölümlenmiş bir sıra, Gelişmiş performans ve kullanılabilirlik için kullanın.
* Farklı bir işlem içinde her alıcı bulunuyorsa, işlem başına yalnızca tek bir Fabrika kullanın.
* Alıcılar, zaman uyumlu veya zaman uyumsuz işlemleri kullanabilirsiniz. Tek bir alıcı oranını Hello Orta Al, istemci-tarafı tam bir istek toplu işleme alıcı verimlilik etkilemez.
* Toplu depolama erişim etkin bırakın. Bu hello azaltır hello varlığın genel yükü. Ayrıca hello azaltır hangi iletileri yazılabilir hello kuyruk veya konu genel oranı.
* Merhaba hazırlık sayısı tooa küçük değeri ayarlayın (örneğin, PrefetchCount = 10). Bu alıcılar çok sayıda önbelleğe alınmış iletiyi diğer alıcılar varken boşta engeller.

### <a name="topic-with-a-small-number-of-subscriptions"></a>Konu Abonelikleri, küçük bir değere sahip
Hedef: abonelikler, küçük bir değere sahip bir konu hello verimini ekranı kaplamasını sağlayın. Bir ileti birleştirilmiş hello başka bir deyişle, pek çok abonelik tarafından alındığında alma oranı tüm abonelikleri üzerinde hello gönderme hızından daha büyük. Merhaba Gönderenler küçük sayısıdır. Merhaba, abonelik başına alıcıları küçük sayısıdır.

toomaximize üretilen işi aşağıdaki hello:

* Bölümlenmiş bir konu, Gelişmiş performans ve kullanılabilirlik için kullanın.
* Genel tooincrease hello hello konu ile gönderme oranı, birden çok ileti oluşturucuları toocreate Gönderenler kullanın. Her gönderen için zaman uyumsuz işlemleri veya birden çok iş parçacığı kullanın.
* Genel tooincrease hello oranı bir abonelik almak, birden çok ileti oluşturucuları toocreate alıcıları kullanın. Her alıcı için zaman uyumsuz işlemleri veya birden çok iş parçacığı kullanın.
* Zaman uyumsuz işlemleri tootake avantajlarından, istemci-tarafı toplu işleme kullanın.
* Hizmet veri yolu istemci iletişim kuralı iletimlerini 20ms tooreduce hello sayısı aralığı toplu işleme hello varsayılan kullanın.
* Toplu depolama erişim etkin bırakın. Bu genel hello artırır, iletileri yazılabilir hello konu ile oranı.
* Merhaba hazırlık sayısı too20 saatleri bir Factory tüm alıcıları hello en yüksek işleme hızlarını ayarlayın. Bu hizmet veri yolu istemci iletişim kuralı iletimlerini hello sayısını azaltır.

### <a name="topic-with-a-large-number-of-subscriptions"></a>Çok sayıda abonelikleri konuyla
Hedef: çok sayıda abonelikleri konuyla hello verimini ekranı kaplamasını sağlayın. Bir ileti birleştirilmiş hello başka bir deyişle, pek çok abonelik tarafından alındığında alma oranı tüm abonelikleri üzerinde hello gönderme hızından daha çok daha büyük. Merhaba Gönderenler küçük sayısıdır. Merhaba, abonelik başına alıcıları küçük sayısıdır.

Tüm iletileri yönlendirilmiş tooall abonelikleri varsa Abonelikleri, çok sayıda konularda genellikle düşük genel üretilen işi kullanıma sunar. Bu, her ileti birçok kez alınan ve konu başlığında yer alan tüm iletileri ve onun abonelikleri hello depolanan tüm aynı depolama hello olgusu kaynaklanır. Merhaba gönderenlerin sayısını ve abonelik başına alıcıları küçük olduğu varsayılır. Hizmet veri yolu too2, konu başına 000 abonelik yukarı destekler.

toomaximize üretilen işi aşağıdaki hello:

* Bölümlenmiş bir konu, Gelişmiş performans ve kullanılabilirlik için kullanın.
* Zaman uyumsuz işlemleri tootake avantajlarından, istemci-tarafı toplu işleme kullanın.
* Hizmet veri yolu istemci iletişim kuralı iletimlerini 20ms tooreduce hello sayısı aralığı toplu işleme hello varsayılan kullanın.
* Toplu depolama erişim etkin bırakın. Bu genel hello artırır, iletileri yazılabilir hello konu ile oranı.
* Merhaba hazırlık sayısı too20 saatleri beklenen hello alma hızı saniye cinsinden ayarlayın. Bu hizmet veri yolu istemci iletişim kuralı iletimlerini hello sayısını azaltır.

## <a name="next-steps"></a>Sonraki adımlar
Hizmet veri yolu performansı en iyi duruma getirme hakkında daha fazla toolearn bkz [bölümlenmiş Mesajlaşma varlıkları][Partitioned messaging entities].

[QueueClient]: /dotnet/api/microsoft.servicebus.messaging.queueclient
[MessageSender]: /dotnet/api/microsoft.servicebus.messaging.messagesender
[MessagingFactory]: /dotnet/api/microsoft.servicebus.messaging.messagingfactory
[PeekLock]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[ReceiveAndDelete]: /dotnet/api/microsoft.servicebus.messaging.receivemode
[BatchFlushInterval]: /dotnet/api/microsoft.servicebus.messaging.netmessagingtransportsettings.batchflushinterval#Microsoft_ServiceBus_Messaging_NetMessagingTransportSettings_BatchFlushInterval
[EnableBatchedOperations]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablebatchedoperations#Microsoft_ServiceBus_Messaging_QueueDescription_EnableBatchedOperations
[QueueClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.queueclient.prefetchcount#Microsoft_ServiceBus_Messaging_QueueClient_PrefetchCount
[SubscriptionClient.PrefetchCount]: /dotnet/api/microsoft.servicebus.messaging.subscriptionclient.prefetchcount#Microsoft_ServiceBus_Messaging_SubscriptionClient_PrefetchCount
[ForcePersistence]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage.forcepersistence#Microsoft_ServiceBus_Messaging_BrokeredMessage_ForcePersistence
[EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.enablepartitioning#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[Partitioned messaging entities]: service-bus-partitioning.md
[TopicDescription.EnableFilteringMessagesBeforePublishing]: /dotnet/api/microsoft.servicebus.messaging.topicdescription.enablefilteringmessagesbeforepublishing#Microsoft_ServiceBus_Messaging_TopicDescription_EnableFilteringMessagesBeforePublishing
