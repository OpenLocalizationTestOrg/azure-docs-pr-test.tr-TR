---
title: Azure Visual Studio'da kod aaaOptimizing | Microsoft Docs
description: "Kodunuzu daha sağlam ve çökmelerin yapmak en iyi duruma getirme araçları Visual Studio hakkında nasıl Azure Kod yardımcı öğrenin."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a>Azure kodunuzu iyileştirme
Microsoft Azure kullanan uygulamalar programlama olduğunda toohelp izlediğiniz bazı kodlama uygulamalarını uygulama ölçeklenebilirlik, davranış ve bulut ortamında bulunan performans sorunları kaçının. Microsoft, tanır ve bu sık karşılaşılan sorunları çeşitli tanımlar ve bunları çözmenize yardımcı olacak bir Azure Kod Analizi aracı sağlar. Visual Studio'da NuGet aracılığıyla hello aracı yükleyebilirsiniz.

## <a name="azure-code-analysis-rules"></a>Azure Kod Analizi kuralları
Hello Azure Kod Analizi aracı tooautomatically bayrak Azure kodunuzu performansı etkileyen bilinen sorunlar bulduğunda kuralları aşağıdaki hello kullanır. Sorunları görünen uyarıları olarak algılanan veya derleyici hataları. Kod düzeltmeleri veya önerileri tooresolve hello uyarı veya hata genellikle sağlanan ampul simgesi üzerinden.

## <a name="avoid-using-default-in-process-session-state-mode"></a>Varsayılan (işlemdeki) oturum durumu modunu kullanmaktan kaçının
### <a name="id"></a>Kimlik
AP0000

### <a name="description"></a>Açıklama
Bulut uygulamaları için hello varsayılan (işlemdeki) oturum durumu modunu kullanıyorsanız, oturum durumu kaybedebilir.

Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Neden
Varsayılan olarak, işlem içi hello web.config dosyasında belirtilen hello oturum durumu modu. Ayrıca, hello yapılandırma dosyasında belirtilen giriş varsa, hello oturum durumu modu tooin işlem varsayar. Merhaba işlemdeki modu oturum durumu hello web sunucusu üzerindeki bellekte depolar. Örneği yeniden ya da yeni bir örneğini Yük Dengeleme veya yük devretme desteği için kullanılan bellek hello web sunucusunda depolanan hello oturum durumu kaydedilmez. Bu durum ölçeklenebilir hello bulutta engeller Merhaba uygulaması engeller.

ASP.NET oturum durumu için oturum durumu verilerini birkaç farklı depolama seçeneklerini destekler: InProc, StateServer, SQLServer, özel ve kapalı. Özel mod toohost veri bir dış oturum durumu deposunda gibi kullanmanız önerilir [Redis için Azure oturum durumu sağlayıcısı](http://go.microsoft.com/fwlink/?LinkId=401521).

### <a name="solution"></a>Çözüm
Bir önerilen bir yönetilen önbellek hizmeti toostore oturum durumu çözümüdür. Bilgi nasıl toouse [Redis için Azure oturum durumu sağlayıcısı](http://go.microsoft.com/fwlink/?LinkId=401521) toostore, oturum durumu. Uygulamanızı hello bulut üzerinde ölçeklenebilir diğer yerler tooensure de deposu oturum durumu. Lütfen okuyun alternatif çözümleri hakkında daha fazla toolearn [oturum durumu modu](https://msdn.microsoft.com/library/ms178586).

## <a name="run-method-should-not-be-async"></a>Run yöntemini zaman uyumsuz olmamalıdır
### <a name="id"></a>Kimlik
AP1000

### <a name="description"></a>Açıklama
Zaman uyumsuz yöntemleri oluşturun (gibi [await](https://msdn.microsoft.com/library/hh156528.aspx)) hello dışında [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi ve çağrı hello zaman uyumsuz yöntemleri [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx). Merhaba bildirme [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi zaman uyumsuz olarak hello çalışan rolü tooenter bir yeniden başlatma döngü neden olur.

Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Neden
Merhaba içinde zaman uyumsuz yöntemleri çağırma [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi hello bulut hizmeti çalışma zamanı toorecycle hello çalışan rolü neden olur. Çalışan rolü başladığında, tüm program yürütme hello içinde gerçekleşir [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi. Mevcut hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi hello çalışan rolü toorestart neden olur. Merhaba async yöntemi Hello çalışan rolü çalışma zamanı geldiğinde, tüm işlemleri hello async yöntemi sonra gönderir ve ardından döndürür. Bu hello çalışan rolü tooexit hello neden [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi ve yeniden başlatın. Merhaba sonraki yinelemede yürütme, hello çalışan rolü yeniden hello async yöntemi ve hello çalışan rolü toorecycle de yeniden neden yeniden kadardır.

### <a name="solution"></a>Çözüm
Merhaba dışında tüm zaman uyumsuz işlemler yerleştirin [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) yöntemi. Ardından, yeniden hello zaman uyumsuz yöntemden'ı çağırın hello içinde [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) RunAsync () .wait gibi yöntemi. Hello Azure Kod Analizi aracı, bu sorunu gidermenize yardımcı olabilir.

Aşağıdaki kod parçacığını hello hello kod düzeltme bu sorunun gösterir:

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a>Hizmet veri yolu paylaşılan erişim imzası kimlik doğrulamasını kullan
### <a name="id"></a>Kimlik
AP2000

### <a name="description"></a>Açıklama
Paylaşılan erişim imzası (SAS) kimlik doğrulaması için kullanın. Erişim denetimi Hizmeti'nden (ACS) hizmet veri yolu kimlik doğrulaması için kullanım dışıdır.

Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Neden
Gelişmiş güvenlik için Azure Active Directory ACS kimlik doğrulaması SAS kimlik doğrulaması ile değiştirmektir. Bkz: [Azure Active Directory olduğu hello ACS gelecekteki](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) hello geçiş planı hakkında bilgi için.

### <a name="solution"></a>Çözüm
SAS kimlik doğrulaması uygulamalarınızı kullanın. Aşağıdaki örnek hello nasıl toouse var olan bir SAS belirteci tooaccess bir hizmet veri yolu ad alanı veya varlık gösterir.

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

Merhaba aşağıdaki konularda daha fazla bilgi için bkz.

* Genel bir bakış için bkz: [paylaşılan erişim imzası kimlik doğrulaması Service Bus ile](https://msdn.microsoft.com/library/dn170477.aspx)
* [Nasıl toouse Service Bus ile paylaşılan erişim imzası kimlik doğrulaması](https://msdn.microsoft.com/library/dn205161.aspx)
* Örnek proje için bkz: [hizmet veri yolu abonelikleri ile kullanarak paylaşılan erişim imzası (SAS) kimlik doğrulaması](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a>"Döngü alırsınız" Onmessageoptions yöntemi tooavoid kullanmayı düşünün
### <a name="id"></a>Kimlik
AP2002

### <a name="description"></a>Açıklama
bir "alma döngü," giderek tooavoid arama hello **Onmessageoptions** yöntemdir arama hello daha iletileri almak için daha iyi bir çözüm **alma** yöntemi. Ancak, hello kullanmanız gerekiyorsa **alma** yöntemi ve varsayılan olmayan sunucu bekleme süresini belirtin, hello sunucu bekleme süresi bir dakikadan fazla olduğundan emin olun.

Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Neden
Çağrılırken **Onmessageoptions**, hello istemci sürekli hello sıra ya da abonelik yokladığı bir dahili ileti Pompalama başlatır. Bu ileti Pompalama tooreceive iletileri bir çağrı sorunları sonsuz bir döngüde içerir. Merhaba çağrısı zaman aşımına uğrarsa, yeni bir çağrı verir. Merhaba zaman aşımı aralığı hello hello değeri tarafından belirlenir [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) hello özelliğinin [Eventhubclient](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)kullanılan.

Merhaba kullanmanın avantajı **Onmessageoptions** çok karşılaştırıldığında**alma** kullanıcılar yoklamak için iletileri, özel durumları işleme, birden fazla ileti paralel işleme ve tamamlamak hello toomanually gerekmemesidir iletileri.

Çağırırsanız **alma** varsayılan değeri kullanmadan emin hello olması *ServerWaitTime* bir dakikadan fazla bir değerdir. Ayarı *ServerWaitTime* toomore bir dakika daha zaman aşımına uğruyor uygulamadan selamlama iletisine tam olarak alınan önce hello sunucu engeller.

### <a name="solution"></a>Çözüm
Önerilen kullanımlar için kod örnekleri aşağıdaki hello bakın. Daha fazla ayrıntı için bkz: [QueueClient.OnMessage yöntemi (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)ve [QueueClient.Receive yöntemi (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).

hello Azure Mesajlaşma altyapısı tooimprove hello performansını görmek hello tasarım deseni [zaman uyumsuz Mesajlaşma Primer](https://msdn.microsoft.com/library/dn589781.aspx).

Merhaba kullanmaya ilişkin bir örnek verilmiştir **Onmessageoptions** tooreceive iletileri.

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

Merhaba kullanmaya ilişkin bir örnek verilmiştir **alma** hello varsayılan sunucusuyla bekleme süresi.

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

Merhaba kullanmaya ilişkin bir örnek verilmiştir **alma** varsayılan olmayan sunucusuyla bekleme süresi.

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a>Zaman uyumsuz hizmet veri yolu yöntemleri kullanmayı düşünün
### <a name="id"></a>Kimlik
AP2003

### <a name="description"></a>Açıklama
Zaman uyumsuz hizmet veri yolu yöntemleri tooimprove performans aracılı Mesajlaşma ile kullanın.

Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Neden
Her çağrısının hello ana iş parçacığı engellemesini devre dışı bırakmak için zaman uyumsuz yöntemleri kullanarak uygulama programı eşzamanlılık sağlar. Service Bus Mesajlaşma yöntemleri, bir işlemi gerçekleştirilirken kullanırken (gönderme, alma, silme, vb.) zaman alır. Bu süre hello işlemi hello işlenmesini hello Service Bus hizmeti tarafından hello istek ve hello yanıt toohello gecikme ekleme içerir. saat başına işlemlerinin tooincrease hello sayısı, işlemler aynı anda yürütmeniz gerekir. Daha fazla bilgi için lütfen çok başvurun[performans iyileştirmeleri kullanarak Service Bus aracılı Mesajlaşma için en iyi uygulamaları](https://msdn.microsoft.com/library/azure/hh528527.aspx).

### <a name="solution"></a>Çözüm
Bkz: [QueueClient sınıfı (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) ne zaman uyumsuz yöntem toouse hello önerilen hakkında bilgi.

hello Azure Mesajlaşma altyapısı tooimprove hello performansını görmek hello tasarım deseni [zaman uyumsuz Mesajlaşma Primer](https://msdn.microsoft.com/library/dn589781.aspx).

## <a name="consider-partitioning-service-bus-queues-and-topics"></a>Bölümleme Service Bus kuyrukları ve konuları göz önünde bulundurun
### <a name="id"></a>Kimlik
AP2004

### <a name="description"></a>Açıklama
Bölüm Service Bus kuyrukları ve konularından Service Bus Mesajlaşma ile daha iyi performans için.

Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Neden
Merhaba bölümlenmiş kuyruk veya konu, genel üretilen işi artık tek ileti Aracısı ya da ileti deposu hello performans ile sınırlı olduğundan, Service Bus kuyrukları ve konularından bölümleme performans verimlilik ve hizmet kullanılabilirliğini artırır. Ayrıca, bir Mesajlaşma deposu geçici bir kesinti bölümlenmiş kuyruk veya konu kullanılamaz hale değil. Daha fazla bilgi için bkz: [Mesajlaşma varlıkları bölümleme](https://msdn.microsoft.com/library/azure/dn520246.aspx).

### <a name="solution"></a>Çözüm
kod parçacığı gösterir nasıl aşağıdaki hello Mesajlaşma toopartition.

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

Daha fazla bilgi için bkz: [bölümlenmiş Service Bus kuyrukları ve konularından | Microsoft Azure blogu](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) ve hello denetleyin [Microsoft Azure hizmet veri yolu kuyruğu bölümlenmiş](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) örnek.

## <a name="do-not-set-sharedaccessstarttime"></a>SharedAccessStartTime ayarlı değil
### <a name="id"></a>Kimlik
AP3001

### <a name="description"></a>Açıklama
SharedAccessStartTimeset toohello tooimmediately hello paylaşılan erişim ilkesi geçerli başlattığınızda yapmaktan kaçınmalısınız. Daha sonraki bir zamanda toostart hello paylaşılan erişim ilkesi istiyorsanız, bu özellik yalnızca tooset gerekir.

Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Neden
Saati eşitleme veri merkezleri arasında küçük zaman farkı neden olur. Örneğin, Hello DateTime.Now veya benzer bir yöntem kullanarak geçerli saati hello SAS İlkesi tootake etkisi hemen neden olacak şekilde bir depolama SAS İlkesi ayarı hello başlangıç saati mantıksal olarak düşünün. Ancak, veri merkezi zamanlarda biraz daha öncesinde, diğerlerinin hello başlangıç saati olabileceğinden hello hafif saat farklılıklarını veri merkezleri arasında bu sorunlara neden olabilir. Sonuç olarak, hello SAS İlkesi hızla (veya hatta hemen) dolabilir hello İlkesi yaşam süresi çok kısa olarak ayarlanmışsa.

Üzerinde Azure storage paylaşılan erişim imzası kullanma konusunda daha fazla yönergeler için bkz: [giriş tablosu SAS (paylaşılan erişim imzası), sıra SAS güncelleştirme tooBlob SAS - Microsoft Azure depolama ekibi blogu - Site ve giriş - MSDN Bloglarında](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Çözüm
Merhaba paylaşılan erişim ilkesi hello başlangıç saatini ayarlar hello deyimi kaldırın. Hello Azure Kod Analizi aracı bu sorun için düzeltme sağlar. Güvenlik yönetimi hakkında daha fazla bilgi için lütfen bkz hello tasarım deseni [Valet anahtar düzeni](https://msdn.microsoft.com/library/dn568102.aspx).

Aşağıdaki kod parçacığını hello hello kod düzeltme bu sorunun gösterir.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a>Paylaşılan Erişim İlkesi sona erme saati beş dakikadan fazla olmalıdır
### <a name="id"></a>Kimlik
AP3002

### <a name="description"></a>Açıklama
Beş dakikalık fark kadar tooa koşul "saat eğme." bilinen son farklı konumlardaki veri merkezleri arasında saatleri içinde olabilir zaman aşımına uğramak gelen tooprevent hello SAS İlkesi belirteci hello sona erme saati toobe beş dakikadan fazla planlanmış daha erken ayarlayın.

Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Neden
Merhaba Dünya farklı konumlardaki veri merkezlerine saati sinyali ile eşitleyin. Saat sinyal tootravel toodifferent konumları için zaman alır çünkü her şeyin beklendiği gibi eşitlenir ancak farklı coğrafi konumlardaki veri merkezlerine arasındaki zaman farkı olabilir. Bu zaman farkı, saat ve sona erme tarihi hello paylaşılan erişim ilkesi başlangıç aralığı etkileyebilir. Bu nedenle, tooensure paylaşılan erişim ilke hemen etkili olur, hello başlangıç saati belirtmezsiniz. Ayrıca, hello süre 5 dakika tooprevent erken zaman aşımından daha fazla olduğundan emin olun.

Azure depolama alanında paylaşılan erişim imzası kullanma hakkında daha fazla bilgi için bkz: [giriş tablosu SAS (paylaşılan erişim imzası), sıra SAS güncelleştirme tooBlob SAS - Microsoft Azure depolama ekibi blogu - Site ve giriş - MSDN Bloglarında](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).

### <a name="solution"></a>Çözüm
Güvenlik yönetimi hakkında daha fazla bilgi için bkz: hello tasarım deseni [Valet anahtar düzeni](https://msdn.microsoft.com/library/dn568102.aspx).

Merhaba, paylaşılan erişim ilkesi başlangıç zamanı belirtmeden bir örnek verilmiştir.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Merhaba, beş dakikadan uzun bir ilke sona erme süresi ile bir paylaşılan erişim ilkesi başlangıç saati belirten bir örnek verilmiştir.

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

Daha fazla bilgi için bkz: [oluşturmak ve paylaşılan erişim imzası kullanmak](https://msdn.microsoft.com/library/azure/jj721951.aspx).

## <a name="use-cloudconfigurationmanager"></a>CloudConfigurationManager kullanın
### <a name="id"></a>Kimlik
AP4000

### <a name="description"></a>Açıklama
Hello kullanarak [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) sınıf projelerde gibi Azure Web sitesine gidin ve Azure mobil hizmetler çalışma zamanı sorunlarına neden olmaz. En iyi uygulama, ancak iyi bir fikir toouse bulut olan[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) tüm Azure bulut uygulamaları için yapılandırmaları yönetme birleşik bir yolu olarak.

Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Neden
CloudConfigurationManager hello yapılandırma dosyasını uygun toohello uygulama ortamı okur.

[CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a>Çözüm
Kod toouse hello yeniden düzenlemeniz [CloudConfigurationManager sınıfı](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx). Bu sorun için bir kod düzeltme hello Azure Kod Analizi aracı tarafından sağlanır.

Aşağıdaki kod parçacığını hello hello kod düzeltme bu sorunun gösterir. Değiştir

`var settings = ConfigurationManager.AppSettings["mySettings"];`

İle

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

Burada, nasıl toostore hello yapılandırma ayarı App.config veya Web.config dosyasındaki bir örnek verilmiştir. Hello ayarları toohello appSettings bölümünde hello yapılandırma dosyası ekleyin. Merhaba, hello önceki kod örneğinde hello bir Web.config dosyası aşağıdadır.

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a>Sabit kodlanmış bağlantı dizelerini kullanmaktan kaçının
### <a name="id"></a>Kimlik
AP4001

### <a name="description"></a>Açıklama
Sabit kodlanmış bağlantı dizelerini kullanın ve tooupdate ihtiyacınız varsa bunları daha sonra siz toomake değişiklikleri tooyour kaynak koduna sahip ve hello uygulama yeniden derleyin. Yapılandırma dosyasında bağlantı dizelerinizi depolarsanız, ancak, bunu daha sonra hello yapılandırma dosyasını güncelleştirerek değiştirebilirsiniz.

Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Neden
Sabit kodlama bağlantı dizeleri nedeni hatalı bir uygulama bağlantı dizeleri hızlı bir şekilde değiştirilmiş toobe gerektiğinde sorunları tanıtır. Ayrıca, Hello proje toosource denetimindeki işaretli toobe gerekirse, sabit kodlanmış bağlantı dizeleri güvenlik açıkları hello dizeleri hello kaynak kodunda görüntülenebilir beri tanıtmaktadır.

### <a name="solution"></a>Çözüm
Bağlantı dizeleri hello yapılandırma dosyalarının veya Azure ortamı depolar.

* Bağımsız uygulamalar için app.config toostore bağlantı dizesi ayarlarını kullanın.
* IIS tarafından barındırılan web uygulamaları için web.config toostore bağlantı dizelerini kullanın.
* ASP.NET vNext uygulamaları için configuration.json toostore bağlantı dizelerini kullanın.

Web.config veya app.config gibi yapılandırma dosyalarını kullanma hakkında daha fazla bilgi için bkz: [ASP.NET Web yapılandırma yönergeleri](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx). Nasıl Azure ortam değişkenleri çalışma hakkında daha fazla bilgi için bkz: [Azure Web siteleri: nasıl uygulama dizeleri ve bağlantı dizeleri çalışma](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/). Bağlantı dizesi kaynak denetiminde depolama hakkında daha fazla bilgi için bkz: [bağlantı dizeleri gibi hassas bilgileri kaynak kodu deposunda saklanır dosyalarında Geçirilmemesi](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).

## <a name="use-diagnostics-configuration-file"></a>Tanılama yapılandırma dosyası kullanın
### <a name="id"></a>Kimlik
AP5000

### <a name="description"></a>Açıklama
API programlama Microsoft.WindowsAzure.Diagnostics Merhaba kullanarak kodunuzda gibi tanılama ayarları yapılandırmak yerine, hello diagnostics.wadcfg dosyasında tanılama ayarları yapılandırmanız gerekir. (Ya da Azure SDK 2.5 kullanıyorsanız diagnostics.wadcfgx). Bunu yaparak, kodunuzu toorecompile gerek kalmadan tanılama ayarlarını değiştirebilirsiniz.

Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Neden
Azure SDK 2.5 (hangi Azure tanılama 1.3 kullanır), Azure tanılama (WAD) birkaç farklı yöntemler kullanarak yapılandırılabilir önce: depolama biriminde, toohello yapılandırma blob, kesinlik temelli kod, bildirim temelli yapılandırma veya hello varsayılan kullanarak ekleme yapılandırma. Ancak, hello yolu tooconfigure tanılama toouse bir XML yapılandırma dosyasında (diagnostics.wadcfg veya diagnositcs.wadcfgx SDK 2.5 ve sonrası) hello uygulama projesi, tercih edilen. Bu yaklaşımda, hello diagnostics.wadcfg dosya tamamen hello yapılandırmasını tanımlar ve güncelleştirilebilir ve gerçekleştirilse imzalanmasını. Merhaba diagnostics.wadcfg yapılandırma dosyasının Hello kullanımı ile Merhaba hello kullanarak yapılandırmalarını ayarlama programlama yöntemleri karıştırma [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)veya [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) sınıfları tooconfusion yol açabilir. Bkz: [başlatılamadı ya da değişiklik Azure tanılama Yapılandırması](https://msdn.microsoft.com/library/azure/hh411537.aspx) daha fazla bilgi için.

WAD (Azure SDK 2.5 ile dahil) 1.3 ile başlayarak, olası toouse kod tooconfigure tanılama artık değildir. Sonuç olarak, yalnızca uygulama ya da hello tanılama uzantısını güncelleştirilirken hello yapılandırması sağlayabilir.

### <a name="solution"></a>Çözüm
Merhaba tanılama yapılandırması Tasarımcı toomove tanılama ayarlarını toohello tanılama yapılandırma dosyası (diagnositcs.wadcfg veya diagnositcs.wadcfgx SDK 2.5 ve sonrası) kullanın. Ayrıca, yüklemenizi tavsiye edilir [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) ve hello son Tanılama özelliğini kullanın.

1. Tooconfigure istediğiniz hello rolüne hello kısayol menüsünde Özellikler'i seçin ve sonra hello yapılandırma sekmesini seçin.
2. Merhaba, **tanılama** bölümünde, o hello emin olun **tanılamayı etkinleştir** onay kutusu seçilidir.
3. Merhaba seçin **yapılandırma** düğmesi.

   ![Merhaba tanılamayı etkinleştir seçeneğine erişme](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   Bkz: [yapılandırma tanılama Azure Cloud Services ve sanal makineler için](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) daha fazla bilgi için.

## <a name="avoid-declaring-dbcontext-objects-as-static"></a>DbContext nesneleri statik olarak bildirme kaçının
### <a name="id"></a>Kimlik
AP6000

### <a name="description"></a>Açıklama
toosave bellek DBContext nesneleri statik olarak bildirme kaçının.

Lütfen fikir ve geri bildirim sırasında paylaşımı [Azure Kod Analizi geri bildirim](http://go.microsoft.com/fwlink/?LinkId=403771).

### <a name="reason"></a>Neden
DBContext nesneleri hello sorgu sonuçlarındaki her çağrı basılı tutun. Merhaba uygulama etki alanı bellekten kaldırılana kadar statik DBContext nesneler atıldı değil. Bu nedenle, bir statik DBContext nesnesi, büyük miktarlarda bellek kullanabilir.

### <a name="solution"></a>Çözüm
Bir yerel değişken ya da statik olmayan örnek alanı olarak DBContext bildirme, bir görev için kullanacağınız ve sonra kullanıldıktan sonra elden sağlayabilirsiniz.

Aşağıdaki örnek MVC denetleyicisi sınıfı hello nasıl toouse hello DBContext nesne gösterir.

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a>Sonraki adımlar
en iyi duruma getirme ve Azure uygulamaları sorunlarını giderme hakkında daha fazla toolearn bkz [Visual Studio kullanarak Azure App Service web uygulamasında sorun giderme](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).
