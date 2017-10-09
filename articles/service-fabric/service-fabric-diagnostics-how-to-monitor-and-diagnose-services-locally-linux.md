---
title: "Linux içindeki Azure mikro aaaDebug | Microsoft Docs"
description: "Bilgi nasıl toomonitor ve bir yerel geliştirme makinede Microsoft Azure Service Fabric kullanılarak yazılmış hizmetlerinizi tanılama."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 4eebe937-ab42-4429-93db-f35c26424321
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: bee47bbabcf6b84ff2da14079e026529e36a198b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a><span data-ttu-id="9f46b-103">İzleme ve yerel makine geliştirme Kurulum Hizmetleri'nde tanılama</span><span class="sxs-lookup"><span data-stu-id="9f46b-103">Monitor and diagnose services in a local machine development setup</span></span>


> [!div class="op_single_selector"]
> * [<span data-ttu-id="9f46b-104">Windows</span><span class="sxs-lookup"><span data-stu-id="9f46b-104">Windows</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [<span data-ttu-id="9f46b-105">Linux</span><span class="sxs-lookup"><span data-stu-id="9f46b-105">Linux</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

<span data-ttu-id="9f46b-106">İzleme, algılama, tanılama ve sorun giderme hizmetleri toocontinue en az kesintiyi toohello kullanıcı deneyimi ile ayırın.</span><span class="sxs-lookup"><span data-stu-id="9f46b-106">Monitoring, detecting, diagnosing, and troubleshooting allow for services toocontinue with minimal disruption toohello user experience.</span></span> <span data-ttu-id="9f46b-107">İzleme ve tanılama gerçek dağıtılmış üretim ortamında önemlidir.</span><span class="sxs-lookup"><span data-stu-id="9f46b-107">Monitoring and diagnostics are critical in an actual deployed production environment.</span></span> <span data-ttu-id="9f46b-108">Benzer bir model Hizmetleri geliştirme sırasında benimsenmesi tooa üretim ortamına taşıdığınızda bu hello tanılama ardışık düzen çalışmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9f46b-108">Adopting a similar model during development of services ensures that hello diagnostic pipeline works when you move tooa production environment.</span></span> <span data-ttu-id="9f46b-109">Service Fabric tek makineli yerel geliştirme kurulumları ve gerçek üretim küme kurulumları arasında sorunsuz bir şekilde çalışabilirsiniz hizmet geliştiricileri tooimplement tanılama kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="9f46b-109">Service Fabric makes it easy for service developers tooimplement diagnostics that can seamlessly work across both single-machine local development setups and real-world production cluster setups.</span></span>


## <a name="debugging-service-fabric-java-applications"></a><span data-ttu-id="9f46b-110">Service Fabric Java uygulamalarında hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="9f46b-110">Debugging Service Fabric Java applications</span></span>

<span data-ttu-id="9f46b-111">Java uygulamaları için [birden çok günlük altyapıları](http://en.wikipedia.org/wiki/Java_logging_framework) kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9f46b-111">For Java applications, [multiple logging frameworks](http://en.wikipedia.org/wiki/Java_logging_framework) are available.</span></span> <span data-ttu-id="9f46b-112">Bu yana `java.util.logging` hello varsayılan seçenektir hello JRE Merhaba kullanılır [kod örnekleri github'da](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9f46b-112">Since `java.util.logging` is hello default option with hello JRE, it is also used for hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  <span data-ttu-id="9f46b-113">Merhaba aşağıdaki tartışma açıklar nasıl tooconfigure hello `java.util.logging` framework.</span><span class="sxs-lookup"><span data-stu-id="9f46b-113">hello following discussion explains how tooconfigure hello `java.util.logging` framework.</span></span>

<span data-ttu-id="9f46b-114">Uygulamanızı yeniden yönlendirebilirsiniz java.util.logging kullanarak toomemory, çıkış akışları, konsol dosyaları veya yuva günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9f46b-114">Using java.util.logging you can redirect your application logs toomemory, output streams, console files, or sockets.</span></span> <span data-ttu-id="9f46b-115">Bu seçeneklerin her biri için varsayılan işleyicisi zaten hello framework sağlanan vardır.</span><span class="sxs-lookup"><span data-stu-id="9f46b-115">For each of these options, there are default handlers already provided in hello framework.</span></span> <span data-ttu-id="9f46b-116">Oluşturabileceğiniz bir `app.properties` dosya tooconfigure hello dosya işleyicisi tüm, uygulama tooredirect için tooa yerel dosya günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="9f46b-116">You can create a `app.properties` file tooconfigure hello file handler for your application tooredirect all logs tooa local file.</span></span>

<span data-ttu-id="9f46b-117">Aşağıdaki kod parçacığını hello örnek bir yapılandırma içerir:</span><span class="sxs-lookup"><span data-stu-id="9f46b-117">hello following code snippet contains an example configuration:</span></span>

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

<span data-ttu-id="9f46b-118">Merhaba klasörünü işaret tooby hello `app.properties` dosya bulunmalıdır.</span><span class="sxs-lookup"><span data-stu-id="9f46b-118">hello folder pointed tooby hello `app.properties` file must exist.</span></span> <span data-ttu-id="9f46b-119">Merhaba sonra `app.properties` dosyası oluşturuldu, tooalso gerek giriş noktası kodunuzu değiştirmek `entrypoint.sh` hello içinde `<applicationfolder>/<servicePkg>/Code/` klasör tooset hello özelliği `java.util.logging.config.file` çok`app.propertes` dosya.</span><span class="sxs-lookup"><span data-stu-id="9f46b-119">After hello `app.properties` file is created, you need tooalso modify your entry point script, `entrypoint.sh` in hello `<applicationfolder>/<servicePkg>/Code/` folder tooset hello property `java.util.logging.config.file` too`app.propertes` file.</span></span> <span data-ttu-id="9f46b-120">Merhaba girişi hello parçacığını aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="9f46b-120">hello entry should look like hello following snippet:</span></span>

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


<span data-ttu-id="9f46b-121">Bu yapılandırma sırasında dönen bir şekilde toplanmakta olan günlükleri sonuçlanır `/tmp/servicefabric/logs/`.</span><span class="sxs-lookup"><span data-stu-id="9f46b-121">This configuration results in logs being collected in a rotating fashion at `/tmp/servicefabric/logs/`.</span></span> <span data-ttu-id="9f46b-122">Merhaba günlük dosyası bu durumda adlandırılan mysfapp%u.%g.log burada:</span><span class="sxs-lookup"><span data-stu-id="9f46b-122">hello log file in this case is named mysfapp%u.%g.log where:</span></span>
* <span data-ttu-id="9f46b-123">**%u** benzersiz bir numara tooresolve eşzamanlı Java işlemleri arasındaki çakışmaları olan.</span><span class="sxs-lookup"><span data-stu-id="9f46b-123">**%u** is a unique number tooresolve conflicts between simultaneous Java processes.</span></span>
* <span data-ttu-id="9f46b-124">**%g** hello nesil numara toodistinguish günlükleri döndürme arasında değil.</span><span class="sxs-lookup"><span data-stu-id="9f46b-124">**%g** is hello generation number toodistinguish between rotating logs.</span></span>

<span data-ttu-id="9f46b-125">Hiçbir işleyici açıkça yapılandırdıysanız, varsayılan olarak hello konsol işleyicisi kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="9f46b-125">By default if no handler is explicitly configured, hello console handler is registered.</span></span> <span data-ttu-id="9f46b-126">Bir syslog /var/log/syslog altında hello günlükleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f46b-126">One can view hello logs in syslog under /var/log/syslog.</span></span>

<span data-ttu-id="9f46b-127">Daha fazla bilgi için bkz: Merhaba [kod örnekleri github'da](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9f46b-127">For more information, see hello [code examples in github](http://github.com/Azure-Samples/service-fabric-java-getting-started).</span></span>  


## <a name="debugging-service-fabric-c-applications"></a><span data-ttu-id="9f46b-128">Service Fabric C# uygulamalarının hatalarını ayıklama</span><span class="sxs-lookup"><span data-stu-id="9f46b-128">Debugging Service Fabric C# applications</span></span>


<span data-ttu-id="9f46b-129">Birden çok çerçeveyi CoreCLR uygulamaları Linux izleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="9f46b-129">Multiple frameworks are available for tracing CoreCLR applications on Linux.</span></span> <span data-ttu-id="9f46b-130">Daha fazla bilgi için bkz: [GitHub: günlüğü](http:/github.com/aspnet/logging).</span><span class="sxs-lookup"><span data-stu-id="9f46b-130">For more information, see [GitHub: logging](http:/github.com/aspnet/logging).</span></span>  <span data-ttu-id="9f46b-131">EventSource tanıdık tooC # geliştiricileri, olduğundan ' CoreCLR örnekleri Linux izleme için bu makalede EventSource kullanır.</span><span class="sxs-lookup"><span data-stu-id="9f46b-131">Since EventSource is familiar tooC# developers,\`this article uses EventSource for tracing in CoreCLR samples on Linux.</span></span>

<span data-ttu-id="9f46b-132">Merhaba ilk adım tooinclude System.Diagnostics.Tracing, böylelikle günlükleri toomemory, çıkış akışları veya konsol dosyalarını yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9f46b-132">hello first step is tooinclude System.Diagnostics.Tracing so that you can write your logs toomemory, output streams, or console files.</span></span>  <span data-ttu-id="9f46b-133">EventSource kullanarak günlüğe kaydetme için proje tooyour project.json aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9f46b-133">For logging using EventSource, add hello following project tooyour project.json:</span></span>

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

<span data-ttu-id="9f46b-134">Merhaba hizmet olayı için özel bir EventListener toolisten kullanın ve ardından bunları tootrace dosyaları uygun şekilde yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="9f46b-134">You can use a custom EventListener toolisten for hello service event and then appropriately redirect them tootrace files.</span></span> <span data-ttu-id="9f46b-135">Merhaba aşağıdaki kod parçacığını bir örnek uygulama EventSource ve özel EventListener kullanarak günlük gösterir:</span><span class="sxs-lookup"><span data-stu-id="9f46b-135">hello following code snippet shows a sample implementation of logging using EventSource and a custom EventListener:</span></span>


```csharp

 public class ServiceEventSource : EventSource
 {
        public static ServiceEventSource Current = new ServiceEventSource();

        [NonEvent]
        public void Message(string message, params object[] args)
        {
            if (this.IsEnabled())
            {
                var finalMessage = string.Format(message, args);
                this.Message(finalMessage);
            }
        }

        // TBD: Need tooadd method for sample event.

}

```


```csharp
   internal class ServiceEventListener : EventListener
   {

        protected override void OnEventSourceCreated(EventSource eventSource)
        {
            EnableEvents(eventSource, EventLevel.LogAlways, EventKeywords.All);
        }
        protected override void OnEventWritten(EventWrittenEventArgs eventData)
        {
            using (StreamWriter Out = new StreamWriter( new FileStream("/tmp/MyServiceLog.txt", FileMode.Append)))           
        { 
                 // report all event information               
         Out.Write(" {0} ",  Write(eventData.Task.ToString(), eventData.EventName, eventData.EventId.ToString(), eventData.Level,""));
                if (eventData.Message != null)              
            Out.WriteLine(eventData.Message, eventData.Payload.ToArray());              
            else             
        { 
                    string[] sargs = eventData.Payload != null ? eventData.Payload.Select(o => o.ToString()).ToArray() : null; 
                    Out.WriteLine("({0}).", sargs != null ? string.Join(", ", sargs) : "");             
        }
           }
        }
    }
```


<span data-ttu-id="9f46b-136">Merhaba Yukarıdaki kod parçacığında çıkarır hello günlükleri tooa dosyasında `/tmp/MyServiceLog.txt`.</span><span class="sxs-lookup"><span data-stu-id="9f46b-136">hello preceding snippet outputs hello logs tooa file in `/tmp/MyServiceLog.txt`.</span></span> <span data-ttu-id="9f46b-137">Bu dosya adı güncelleştirilmesini toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="9f46b-137">This file name needs toobe appropriately updated.</span></span> <span data-ttu-id="9f46b-138">Tooredirect hello günlükleri tooconsole olasılığına parçacığı özelleştirilmiş EventListener sınıfınızda aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9f46b-138">In case you want tooredirect hello logs tooconsole, use hello following snippet in your customized EventListener class:</span></span>

```csharp
public static TextWriter Out = Console.Out;
```

<span data-ttu-id="9f46b-139">Merhaba, örnekleri [C# örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) EventSource ve bir özel EventListener toolog olayları tooa dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="9f46b-139">hello samples at [C# Samples](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) use EventSource and a custom EventListener toolog events tooa file.</span></span>



## <a name="next-steps"></a><span data-ttu-id="9f46b-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9f46b-140">Next steps</span></span>
<span data-ttu-id="9f46b-141">Merhaba eklenen aynı izleme kodu tooyour uygulama uygulamanızın Azure bir kümede hello Tanılama ile de çalışır.</span><span class="sxs-lookup"><span data-stu-id="9f46b-141">hello same tracing code added tooyour application also works with hello diagnostics of your application on an Azure cluster.</span></span> <span data-ttu-id="9f46b-142">Merhaba hello araçları için farklı seçenekleri ele ve açıklayan Bu makaleler kullanıma nasıl tooset bunları ayarlama.</span><span class="sxs-lookup"><span data-stu-id="9f46b-142">Check out these articles that discuss hello different options for hello tools and describe how tooset them up.</span></span>
* [<span data-ttu-id="9f46b-143">Nasıl toocollect ile Azure tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="9f46b-143">How toocollect logs with Azure Diagnostics</span></span>](service-fabric-diagnostics-how-to-setup-lad.md)
