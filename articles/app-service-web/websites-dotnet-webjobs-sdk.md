---
title: "hello Azure WebJobs SDK aaaWhat olduğu"
description: "Giriş toohello Azure WebJobs SDK. Hangi hello SDK, tipik senaryolar için kullanışlıdır olduğu ve kod örnekleri açıklanmaktadır."
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
ms.openlocfilehash: efac7a75c3b68a6a6601fb298f2ccac9bd71709d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-azure-webjobs-sdk"></a>Hello Azure WebJobs SDK nedir
## <a id="overview"></a>Genel bakış
Bu makale, hangi Web işleri SDK'si hello açıklar ise, bazı ortak senaryolar için faydalı olur ve kodunuzda kullanma hakkında genel bir bakış sunar inceler.

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

[Web işleri](websites-webjobs-resources.md) toorun sağlayan bir Azure uygulama hizmeti bir program veya komut dosyasında hello özelliğidir bir web uygulaması, API uygulaması veya mobil uygulama olarak aynı bağlamı. Merhaba hello amacı [WebJobs SDK](websites-webjobs-resources.md) toosimplify hello kodu yazma için bir Web işi gerçekleştirebilirsiniz, görüntü işleme, sıra işleme, RSS toplama, dosya bakımı gibi genel görevleri ve e-postaları gönderme. Merhaba Web işleri SDK'si, Azure Storage ve Service Bus ile çalışmak için görev zamanlama ve hataları işleme ve diğer birçok yaygın senaryolar için yerleşik özelliğine sahiptir. Ayrıca, tasarlanmış toobe genişletilebilir. Merhaba [Web işleri SDK'si açık kaynak olan](https://github.com/Azure/azure-webjobs-sdk/)ve bir [uzantıları için açık kaynak deposu](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).

Merhaba WebJobs SDK hello aşağıdaki bileşenleri içerir:

* **NuGet paketlerini**. NuGet paketleri tooa Visual Studio konsol uygulama projesi Ekle yöntemlerinizi Web işleri SDK'si özniteliklerle tasarlayarak kodunuzun kullandığı bir çerçeve sağlar.
* **Pano**. Merhaba WebJobs SDK parçası Azure App Service içinde bulunur ve zengin izleme ve tanılama hello NuGet paketlerini kullanan programlar için sağlar. Bu izleme ve tanılama özellikleri toowrite kod toouse yok.

## <a id="scenarios"></a>Senaryoları
Hello Azure WebJobs SDK ile daha kolay işleyebilir bazı tipik senaryolar şunlardır:

* İşlem ya da diğer CPU yoğunluklu iş görüntü. Bir ortak Web siteleri hello özelliği tooupload görüntülere veya videolara özelliğidir. Genellikle, yüklenir, ancak bunu sırada toomake hello kullanıcı bekleme istemediğiniz sonra toomanipulate hello içerik istiyor.
* Sıranın işleme. Bir ortak bir arka uç hizmeti ile bir web ön uç toocommunicate toouse sıraları yoldur. Merhaba Web sitesi tooget işlerini gerektiğinde, bir sıra üzerine bir ileti iter. Arka uç hizmeti hello sırasından ileti çeker ve iş hello. Görüntü işleme için kuyrukları kullanabilirsiniz: hello kullanıcı dosya sayısı gönderildikten sonra Örneğin, hello dosya adları hello arka uç işleme göre toplanmış bir kuyruk iletisi toobe yerleştirin. Veya sıraları tooimprove site yanıtlama kullanabilir. Örneğin, doğrudan tooa SQL veritabanına yazma, yerine tooa sıra yazma, işiniz bittiğinde ve iş hello arka uç hizmeti tanıtıcı Yüksek gecikmeli ilişkisel veritabanı izin hello kullanıcı söyleyin. Merhaba görüntü işlemine işleme sırası bir örnek için bkz [WebJobs SDK Başlarken Öğreticisi](websites-dotnet-webjobs-sdk-get-started.md).
* RSS toplama. RSS akışları listesini tutar bir siteniz varsa, tüm arka plan işlemi hello akışlarında hello makalelerinden çekme.
* Dosya bakımı, toplama veya günlük dosyalarını temizleme gibi.  Bazı siteler tarafından ya da ayrı için oluşturulan günlük dosyalarını olabilir toocombine istediğiniz zaman aralıkları sipariş toorun analiz işleri üzerlerinde. Veya tooschedule görev toorun haftalık tooclean eski günlük dosyalarını isteyebilirsiniz.
* Giriş Azure tablolara. Depolanan dosyaların ve BLOB'lar ve tooparse istiyorsanız bunları tablolarda hello veri depolamak ve. Merhaba Giriş işlevi çok sayıda satır (bazı durumlarda milyonlarca) yazma ve hello Web işleri SDK'si olası tooimplement kılar bu işlevselliği kolayca. Merhaba SDK ayrıca İlerleme göstergesi hello hello tablosuna yazılan satır sayısı gibi gerçek zamanlı izlenmesini sağlar.
* Bir arka plan iş parçacığında toorun gibi istediğiniz diğer uzun süre çalışan görevler [e-postaları gönderme](https://github.com/victorhurdugaci/AzureWebJobsSamples/tree/master/SendEmailOnFailure). 
* Yedekleme işlemi her gece gerçekleştirme gibi bir zamanlamada toorun istediğiniz herhangi bir görevi.

Bu senaryolar çoğunu tooscale birden çok Web işleri aynı anda çalıştırırsınız: birden çok VM üzerinde bir web uygulaması toorun isteyebilirsiniz. Bu hello aynı işlenen veri sonuçlanabilir bazı senaryolarda birden çok kez değildir, ancak bu bir sorun hello yerleşik sırası, blob ve hello WebJobs SDK, Service Bus Tetikleyicileri kullandığınızda. Merhaba SDK işlevlerinizi yalnızca bir kez her ileti veya blob işleneceğini sağlar.

Merhaba WebJobs SDK ayrıca kolay toohandle ortak hata işleme senaryolarını kolaylaştırır. Bir işlev işlemi başarısız olur ve zaman aşımları belirtilen süre sınırı içinde tamamlanmazsa bir işlev otomatik olarak iptal ayarlayabilirsiniz, uyarıları toosend bildirimler ayarlayabilirsiniz.

## <a id="code"></a>Kod örnekleri
Azure Storage ile çalışma genel görevler işlemek için hello kod basittir. Konsol uygulamanızın içinde `Main` yöntemi, oluşturduğunuz bir `JobHost` hello koordinatları nesnesi yazdığınız toomethods çağırır. Merhaba WebJobs SDK framework zaman yöntemlerinizi ve toouse hangi parametre değerleri temel Web işleri SDK'si hello üzerinde toocall özniteliklerine bilir bunları kullanın. Merhaba SDK sağlar *Tetikleyicileri* belirten hello işlevi toobe olarak adlandırılan, hangi koşullar neden ve *bağlayıcıları* belirten nasıl tooget bilgi içine ve dışına yöntem parametreleri.

Örneğin, hello [QueueTrigger](websites-dotnet-webjobs-sdk-storage-queues-how-to.md) özniteliği bir sırada bir ileti aldı ve hello ileti biçimi bir bayt dizisi veya özel bir tür için JSON ise, selamlama iletisine otomatik olarak seri durumdan çıkarılmış olduğunda adlı bir işlev toobe neden olur. Merhaba [BlobTrigger](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md) özniteliği, yeni blob Azure depolama hesabınız oluşturulduğunda bir işlem tetikler.

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

Merhaba `JobHost` nesne bir arka plan işlevler kümesi için bir kapsayıcıdır. Merhaba `JobHost` nesne izleyiciler hello işlevleri, bunları tetikleyen olayları izler ve tetikleyici olaylar meydana geldiğinde hello işlevleri yürütür. Çağırmanız bir `JobHost` yöntemi tooindicate hello kapsayıcı işlem toorun istediğinizi hello geçerli iş parçacığının veya bir arka plan iş parçacığı. Merhaba örnekte hello `RunAndBlock` yöntemi çalışmaları hello işlem sürekli hello geçerli iş parçacığı üzerinde.

Çünkü hello `ProcessQueueMessage` yöntemi bu örnekte sahip bir `QueueTrigger` özniteliği, hello tetikleyici bu işlevi yeni bir kuyruk iletisi hello alınması için. Merhaba `JobHost` nesne izleyen yeni kuyruk iletileri hello belirtilen sırasına (Bu örnekte "webjobsqueue") için ve biri bulunduğunda, çağıran `ProcessQueueMessage`. 

Merhaba `QueueTrigger` özniteliği bağlar hello `inputText` hello kuyruk iletisi parametre toohello değeri. Ve hello `Blob` özniteliği bağlamalar bir `TextWriter` nesne tooa blob adındaki "containername" adlı bir kapsayıcı "blobname".  

        public static void ProcessQueueMessage([QueueTrigger("webjobsqueue")]] string inputText, 
            [Blob("containername/blobname")]TextWriter writer)

Merhaba işlevi sonra hello sıraya ileti toohello blob bu parametreleri toowrite hello değerini kullanır:

        writer.WriteLine(inputText);

Hello tetikleyici ve bağlayıcı özelliklerini hello WebJobs SDK hello kod toowrite sahip büyük ölçüde basitleştirir. alt düzey kodu gerekli tooprocess kuyruklar, BLOB'lar, veya dosyaları ya da tooinitiate zamanlanmış görevler Merhaba, sizin için Web işleri SDK'si framework hello tarafından yapılır. Örneğin, hello framework henüz mevcut kuyruklar oluşturur, açılır sıra Merhaba, okuma iletileri kuyruğa, işlem tamamlandığında, yoksa blob kapsayıcıları oluşturur henüz tooblobs vb. Yazar zaman siler iletileri kuyruğa.

Merhaba aşağıdaki kod örneğinde Tetikleyicileri çeşitli bir WebJob içinde gösterilmektedir: `QueueTrigger`, `FileTrigger`, `WebHookTrigger`, ve `ErrorTrigger`. 

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
            too= "admin@emailaddress.com",
            Subject = "Error!")]
         SendGridMessage message)
        {
            // log last 5 detailed errors toohello Dashboard
            log.WriteLine(filter.GetDetailedMessage(5));
            message.Text = filter.GetDetailedMessage(1);
        }
    }
```

## <a id="schedule"></a>Zamanlama
Merhaba `TimerTrigger` özniteliği özelliği tootrigger işlevleri toorun bir zamanlamaya göre hello sağlar. Web işleri SDK'si kullanarak bir Web işi bir tüm ile Azure veya zamanlama tekil işlevler hello gibi bir Web işi zamanlayabilirsiniz `TimerTrigger`. Kod örneği aşağıda verilmiştir.

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

Daha fazla örnek kod için bkz: [TimerSamples.cs](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/ExtensionsSample/Samples/TimerSamples.cs) hello azure webjobs sdk uzantıları deposundaki Github.com'u.

## <a name="extensibility"></a>Genişletilebilirlik
Toobuilt bileşenini sınırlı değil işlevsellik--hello Web işleri SDK'si sağlar, toowrite özel tetikleyiciler ve bağlayıcıları.  Örneğin, önbellek olayları ve düzenli zamanlamaları Tetikleyicileri yazabilirsiniz. Bir [açık kaynak deposu](https://github.com/Azure/azure-webjobs-sdk-extensions) içeren bir [WebJobs SDK genişletilebilirlik hakkında ayrıntılı kılavuz](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview) ve örnek kod toohelp başlamanıza kendi Tetikleyicileri ve bağlayıcıları yazma alın.

## <a id="workerrole"></a>Merhaba WebJobs SDK Web işleri dışında kullanma
Web işleri SDK'si standart bir konsol uygulamasıdır ve herhangi bir yere--çalıştırabilirsiniz hello hello kullanan bir programı bir Web işi toorun sahip değil. Geliştirme bilgisayarınızda ve bu ortamlarda birini tercih ederseniz, bir bulut hizmeti çalışan rolü veya bir Windows hizmeti çalıştırabilirsiniz üretim hello programı yerel olarak sınayabilirsiniz. 

Ancak, hello Panosu yalnızca bir Azure App Service web uygulaması için bir uzantı olarak kullanılabilir. Bir Web işi dışında toorun istediğiniz ve hala hello Pano kullanıyorsanız, bir web yapılandırabilirsiniz uygulama toouse hello WebJobs SDK Pano bağlantı dizenizi başvuruyor ve bu web uygulamanızın Web işleri Panosu'nu o işlevi hakkında veri gösterecektir aynı depolama hesabı yürütme programınızdan başka bir yere çalışıyor. Merhaba URL https:// kullanarak toohello Pano alabilirsiniz*{webappname}*.scm.azurewebsites.net/azurejobs/#/functions. Daha fazla bilgi için bkz: [hello WebJobs SDK ile yerel geliştirme için bir Pano alma](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), ancak hello blog gönderisi eski bir bağlantı dizesi adı gösterdiğine dikkat edin. 

## <a id="nostorage"></a>Pano özellikleri
Web işleri SDK'si Tetikleyicileri veya bağlayıcıları kullanmayın olsa bile hello WebJobs SDK çeşitli avantajları sağlar:

* Merhaba Pano işlevleri çağırabilir.
* Merhaba Pano işlevlerden oynatabilirsiniz.
* Hello Panosu, bağlı toohello günlüklerini görüntüleyebilirsiniz belirli WebJob (Console.Out, Console.Error, izleme, vb. kullanılarak yazılmış uygulama günlükleri) veya bağlı bunları oluşturulan toohello belirli işlev çağrısını (günlükleri kullanılarak yazılmış bir `TextWriter` Bu hello SDK toohello işlevi parametre olarak geçirir. nesne). 

Daha fazla bilgi için bkz: [nasıl bir işlevi çağırmak toomanually](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#manual) ve [nasıl toowrite günlükleri](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#logs) 

## <a id="nextsteps"></a>Sonraki adımlar
Merhaba WebJobs SDK hakkında daha fazla bilgi için bkz: [Azure Web işleri önerilen kaynakları](http://go.microsoft.com/fwlink/?linkid=390226).

Merhaba hello en son geliştirmeleri toohello WebJobs SDK hakkında daha fazla bilgi için bkz [sürüm notları](https://github.com/Azure/azure-webjobs-sdk/wiki/Release-Notes).

