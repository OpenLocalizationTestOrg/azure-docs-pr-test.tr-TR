---
title: Azure WebJobs SDK nedir?
description: "Azure WebJobs SDK Giriş. SDK nedir, yararlıdır ve kod örnekleri tipik senaryolar açıklanmaktadır."
services: app-service\web, storage
documentationcenter: .net
author: ggailey777
manager: erikre
editor: jimbe
ms.assetid: 8281267b-572b-4b14-a328-6704493ea682
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2016
ms.author: glenga
ms.openlocfilehash: 8eb05b7cbfb4505f2e94c5b8e6d367ec63a2f033
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-the-azure-webjobs-sdk"></a>Azure WebJobs SDK nedir?
## <a id="overview"></a>Genel bakış
Bu makalede WebJobs SDK nedir açıklanmakta, bazı ortak senaryolar için faydalı olur ve kodunuzda kullanma hakkında genel bir bakış sunar inceler.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[Web işleri](websites-webjobs-resources.md) bir web uygulaması, API uygulaması veya mobil uygulama olarak aynı bağlamda bir program veya komut dosyasını çalıştırmanıza olanak sağlayan bir Azure uygulama hizmeti özelliğidir. Amacı [WebJobs SDK](websites-webjobs-resources.md) bir Web işi gerçekleştirebilirsiniz, görüntü işleme, sıra işleme, RSS toplama, dosya bakımı gibi ortak görevler için yazdığınız kodları kolaylaştırmaktır ve e-postaları gönderme. Web işleri SDK'si, Azure Storage ve Service Bus ile çalışmak için görev zamanlama ve hataları işleme ve diğer birçok yaygın senaryolar için yerleşik özellikler vardır. Ayrıca, Genişletilebilir olmak için tasarlanmıştır. [Web işleri SDK'si açık kaynak olan](https://github.com/Azure/azure-webjobs-sdk/)ve bir [uzantıları için açık kaynak deposu](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

WebJobs SDK aşağıdaki bileşenleri içerir:

* **NuGet paketlerini**. Visual Studio konsol uygulaması projesine ekleyin NuGet paketlerini yöntemlerinizi Web işleri SDK'si özniteliklerle tasarlayarak kodunuzun kullandığı bir çerçeve sağlar.
* **Pano**. WebJobs SDK parçası Azure App Service içinde bulunur ve zengin izleme ve tanılama NuGet paketlerini kullanan programlar için sağlar. Bu izleme ve tanılama özellikleri kullanmak için kod yazmak zorunda değilsiniz.

## <a id="scenarios"></a>Senaryoları
Azure WebJobs SDK ile daha kolay işleyebilir bazı tipik senaryolar şunlardır:

* İşlem ya da diğer CPU yoğunluklu iş görüntü. Bir ortak Web siteleri görüntüler veya videoları karşıya yükleme olanağı özelliğidir. Genellikle, karşıya ancak bunu bekleyin kullanıcı yapmak istemiyorsanız sonra içeriği işlemek istersiniz.
* Sıranın işleme. Arka uç hizmeti ile iletişim kurmak web ön uç için yaygın bir yolu sıraları kullanmaktır. Web sitesi işlerini halletmek ihtiyaç duyduğunda üzerine bir sıraya bir ileti iter. Arka uç hizmeti sırasından ileti çeker ve çalışır. Görüntü işleme için kuyrukları kullanabilirsiniz: kullanıcı dosya sayısı gönderildikten sonra Örneğin, dosya adları bir kuyruk iletisi işleme için arka uç tarafından çekilmesi yerleştirin. Veya site yanıt hızını artırmak için kuyrukları kullanabilirsiniz. Örneğin, bir SQL veritabanına doğrudan yazmak yerine, bir kuyruğa işiniz bittiğinde, kullanıcıya bildir yazma ve iş arka uç hizmeti tanıtıcı Yüksek gecikmeli ilişkisel veritabanı izin verin. Görüntü işlemine işleme sırası örneği için bkz: [WebJobs SDK Başlarken Öğreticisi](websites-dotnet-webjobs-sdk-get-started.md).
* RSS toplama. RSS akışları listesini tutar bir siteniz varsa, tüm arka plan işlemi akışlarında makalelerinden çekme.
* Dosya bakımı, toplama veya günlük dosyalarını temizleme gibi.  Bazı siteler tarafından veya bunlar üzerinde analiz işlerini çalıştırmak için birleştirmek istediğiniz ayrı zaman aralıkları için oluşturulan günlük dosyalarını olabilir. Veya, eski günlük dosyaları temizlemek için haftalık çalıştırmak için bir görev zamanlama isteyebilirsiniz.
* Giriş Azure tablolara. Depolanan dosyaların ve blobları sahip ve bunları ayrıştırma ve tablolarındaki verileri depolamak istediğiniz. Giriş işlevi çok sayıda satır (bazı durumlarda milyonlarca) yazmak ve Web işleri SDK'si, bu işlev kolayca uygulamak mümkün kılar. SDK, ayrıca İlerleme göstergesi tabloda yazılmış satır sayısı gibi gerçek zamanlı izlenmesini sağlar.
* Arka plan iş parçacığında, çalıştırmak istediğiniz diğer uzun süre çalışan görevler [e-postaları gönderme](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure). 
* Yedekleme işlemi her gece gerçekleştirme gibi bir zamanlamaya göre çalıştırmak istediğiniz herhangi bir görevi.

Bu senaryolar çoğunu birden çok Web işleri aynı anda çalıştırırsınız: birden çok VM çalıştırmak için bir web uygulaması ölçeklendirme isteyebilirsiniz. Bazı senaryolarda bu birden çok kez işlenen aynı veri kaybına neden, ancak yerleşik sırası, blob ve WebJobs SDK, Service Bus Tetikleyicileri kullandığınızda bu bir sorun değildir. SDK işlevlerinizi yalnızca bir kez her ileti veya blob işleneceğini sağlar.

WebJobs SDK Ayrıca ortak hata senaryoları işleme işlemek kolaylaştırır. Bir işlev işlemi başarısız olur ve zaman aşımları belirtilen süre sınırı içinde tamamlanmazsa bir işlev otomatik olarak iptal ayarlayabilirsiniz bildirimleri göndermek için uyarıları ayarlayın.

## <a id="code"></a>Kod örnekleri
Azure Storage ile çalışma genel görevler işlemek için kod basittir. Konsol uygulamanızın içinde `Main` yöntemi, oluşturduğunuz bir `JobHost` yazma yöntemleri çağrıları koordine eden nesne. Web işleri SDK'si framework yöntemlerinizi çağrısının ne zaman ve ne kullanılacak parametre değerlerini bunları kullandığınız Web işleri SDK'si özniteliklerini temel alarak bilir. SDK sağlar *Tetikleyicileri* belirten çağrılacak, işlev hangi koşullar neden ve *bağlayıcıları* bilgilerin içine ve dışına yöntem parametreleri nasıl alınacağını belirtin.

Örneğin, [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) özniteliği neden olan bir sırada bir ileti aldı ve ileti biçimi JSON bir bayt dizisi veya özel bir tür için ileti otomatik olarak seri durumdan çıkarılmış ise, çağrılacak işlev. [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) özniteliği, yeni blob Azure depolama hesabınız oluşturulduğunda bir işlem tetikler.

Bir kuyruk yoklar ve alınan her kuyruk iletisi için bir blob oluşturan basit bir program şöyledir:

        public static void Main()
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)
        {
            writer.WriteLine(inputText);
        }

`JobHost` Nesnesi bir arka plan işlevler kümesi için bir kapsayıcıdır. `JobHost` Nesne İşlevler, Gözcü bunları tetikleyen olayları izler ve tetikleyici olaylar meydana geldiğinde işlevleri yürütür. Çağırmanız bir `JobHost` yöntemi geçerli iş parçacığının veya bir arka plan iş parçacığı çalışmaya kapsayıcı işlem isteyip istemediğinizi belirtin. Örnekte, `RunAndBlock` yöntemi çalışan işlemi sürekli olarak geçerli iş parçacığı üzerinde.

Çünkü `ProcessQueueMessage` yöntemi bu örnekte sahip bir `QueueTrigger` özniteliği, tetikleyici bu işlevi yeni bir kuyruk iletisi alınması için. `JobHost` Nesne izleyen yeni bir kuyruk iletisi belirtilen sırada (Bu örnekte "webjobsqueue") için ve biri bulunduğunda, çağıran `ProcessQueueMessage`. 

`QueueTrigger` Özniteliği bağlamalar `inputText` kuyruk iletisini değeri parametresi. Ve `Blob` özniteliği bağlamalar bir `TextWriter` "containername" adlı bir kapsayıcı "blobname" adlı bir blob nesnesi.  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

İşlevi bu parametreler için blob kuyruk iletisini değerini yazmak için sonra kullanır:

        writer.WriteLine(inputText);

WebJobs SDK tetikleyici ve bağlayıcı özelliklerini yazmak zorunda kod büyük ölçüde basitleştirir. Kuyruklar, BLOB'lar veya dosyalarını işlemek için veya zamanlanmış görevler başlatmak için gereken alt düzey kodu sizin için Web işleri SDK'si çerçevesi tarafından yapılır. Örneğin, framework açılır henüz yoksa sıraları kuyruk oluşturur, iletileri okuma kuyruk, işleme tamamlandı, yoksa blob kapsayıcıları oluşturur henüz BLOB'lar vb. için yazar zaman siler iletileri kuyruğa.

Aşağıdaki kod örneğinde bir WebJob içinde Tetikleyicileri çeşitli gösterir: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, ve `ErrorTrigger`. 

```
    public class Functions
    {
        public static void ProcessQueueMessage([QueueTrigger("queue")] string message,
        TextWriter log)
        {
            log.WriteLine(message);
        }

        public static void ProcessFileAndUploadToBlob(
            [FileTrigger(@"import\{name}", "*.*", autoDelete: true)] Stream file,
            [Blob(@"processed/{name}", FileAccess.Write)] Stream output,
            string name,
            TextWriter log)
        {
            output = file;
            file.Close();
            log.WriteLine(string.Format("Processed input file '{0}'!", name));
        }

        [Singleton]
        public static void ProcessWebHookA([WebHookTrigger] string body, TextWriter log)
        {
            log.WriteLine(string.Format("WebHookA invoked! Body: {0}", body));
        }

        public static void ProcessGitHubWebHook([WebHookTrigger] string body, TextWriter log)
        {
            dynamic issueEvent = JObject.Parse(body);
            log.WriteLine(string.Format("GitHub WebHook invoked! ('{0}', '{1}')",
                issueEvent.issue.title, issueEvent.action));
        }

        public static void ErrorMonitor(
        [ErrorTrigger("00:01:00", 1)] TraceFilter filter, TextWriter log,
        [SendGrid(
            To = "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors to the Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <a id="schedule"></a>Zamanlama
`TimerTrigger` Özniteliği imkanı sunar, tetikleyici işlevlere bir zamanlamaya göre çalıştır. WebJobs SDK'yı kullanarak bir Web işinin Azure veya zamanlama tekil işlevler aracılığıyla bir bütün olarak bir Web işi zamanlama `TimerTrigger`. Kod örneği aşağıda verilmiştir.

```
public class Functions
{
    public static void ProcessTimer([TimerTrigger("*/15 * * * * *", RunOnStartup = true)]
    TimerInfo info, [Queue("queue")] out string message)
    {
        message = info.FormatNextOccurrences(1);
    }
}
```

Daha fazla örnek kod için bkz: [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) Github.com'u üzerinde azure webjobs sdk uzantıları deposunda.

## <a name="extensibility"></a>Genişletilebilirlik
Yerleşik işlevselliği--sınırlı değil WebJobs SDK özel tetikleyiciler ve bağlayıcıları yazmanızı sağlar.  Örneğin, önbellek olayları ve düzenli zamanlamaları Tetikleyicileri yazabilirsiniz. Bir [açık kaynak deposu](https://github.com/Azure/azure-webjobs-sdk-extensions) içeren bir [WebJobs SDK genişletilebilirlik hakkında ayrıntılı kılavuz](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) ve yardımcı olması için örnek kod başlatılan kendi Tetikleyicileri ve bağlayıcıları yazma.

## <a id="workerrole"></a>Web işleri dışında WebJobs SDK'sını kullanarak
Kullanan bir programı Web işleri SDK'si standart bir konsol uygulamasıdır ve her yerden çalıştırabilirsiniz--Web işi çalıştırmak sahip değil. Program geliştirme bilgisayarınızda yerel olarak sınayabilirsiniz ve bu ortamlarda birini tercih ederseniz üretimde bir bulut hizmeti çalışan rolü veya bir Windows hizmeti çalıştırabilirsiniz. 

Ancak, Pano yalnızca bir Azure App Service web uygulaması için bir uzantı olarak kullanılabilir. Bir Web işi dışında çalıştırın ve panoyu kullanmaya devam istiyorsanız, WebJobs SDK Pano bağlantı dizenizi başvurduğu ve web uygulamanızın Web işleri Panosu'nu sonra işlevi yürütme hakkındaki verileri gösterecek aynı depolama hesabı kullanmak için bir web uygulaması yapılandırabilirsiniz programınızdan, başka bir yere çalışıyor. URL https:// kullanarak panoya alabilirsiniz*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions. Daha fazla bilgi için bkz: [WebJobs SDK ile yerel geliştirme için bir Pano alma](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ancak blog postası eski bir bağlantı dizesi adı gösterdiğine dikkat edin. 

## <a id="nostorage"></a>Pano özellikleri
Web işleri SDK'si Tetikleyicileri veya bağlayıcıları kullanmayın olsa bile WebJobs SDK çeşitli avantajları sağlar:

* Panodan işlevleri çağırabilir.
* Panodan işlevleri oynatabilirsiniz.
* Belirli Web işi (Console.Out, Console.Error, izleme, vb. kullanılarak yazılmış uygulama günlükleri) ile bağlantılı ya da bunları oluşturulan belirli işlevi çağırma bağlı panosundaki günlüklerini görüntüleyebilirsiniz (günlükleri kullanılarak yazılmış bir `TextWriter` nesnesi SDK işlevi için parametre olarak geçtiğini). 

Daha fazla bilgi için bkz: [el ile bir işlevi çağırmak nasıl](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) ve [nasıl günlüklerini yazma](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>Sonraki adımlar
WebJobs SDK'sı hakkında daha fazla bilgi için bkz: [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).

WebJobs SDK'sının en son geliştirmeleri hakkında daha fazla bilgi için bkz: [sürüm notları](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).

