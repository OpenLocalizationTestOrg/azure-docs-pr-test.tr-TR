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
# <a name="monitor-and-diagnose-services-in-a-local-machine-development-setup"></a>İzleme ve yerel makine geliştirme Kurulum Hizmetleri'nde tanılama


> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
> * [Linux](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally-linux.md)
>
>

İzleme, algılama, tanılama ve sorun giderme hizmetleri toocontinue en az kesintiyi toohello kullanıcı deneyimi ile ayırın. İzleme ve tanılama gerçek dağıtılmış üretim ortamında önemlidir. Benzer bir model Hizmetleri geliştirme sırasında benimsenmesi tooa üretim ortamına taşıdığınızda bu hello tanılama ardışık düzen çalışmasını sağlar. Service Fabric tek makineli yerel geliştirme kurulumları ve gerçek üretim küme kurulumları arasında sorunsuz bir şekilde çalışabilirsiniz hizmet geliştiricileri tooimplement tanılama kolaylaştırır.


## <a name="debugging-service-fabric-java-applications"></a>Service Fabric Java uygulamalarında hata ayıklama

Java uygulamaları için [birden çok günlük altyapıları](http://en.wikipedia.org/wiki/Java_logging_framework) kullanılabilir. Bu yana `java.util.logging` hello varsayılan seçenektir hello JRE Merhaba kullanılır [kod örnekleri github'da](http://github.com/Azure-Samples/service-fabric-java-getting-started).  Merhaba aşağıdaki tartışma açıklar nasıl tooconfigure hello `java.util.logging` framework.

Uygulamanızı yeniden yönlendirebilirsiniz java.util.logging kullanarak toomemory, çıkış akışları, konsol dosyaları veya yuva günlüğe kaydeder. Bu seçeneklerin her biri için varsayılan işleyicisi zaten hello framework sağlanan vardır. Oluşturabileceğiniz bir `app.properties` dosya tooconfigure hello dosya işleyicisi tüm, uygulama tooredirect için tooa yerel dosya günlüğe kaydeder.

Aşağıdaki kod parçacığını hello örnek bir yapılandırma içerir:

```java
handlers = java.util.logging.FileHandler

java.util.logging.FileHandler.level = ALL
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
java.util.logging.FileHandler.limit = 1024000
java.util.logging.FileHandler.count = 10
java.util.logging.FileHandler.pattern = /tmp/servicefabric/logs/mysfapp%u.%g.log             
```

Merhaba klasörünü işaret tooby hello `app.properties` dosya bulunmalıdır. Merhaba sonra `app.properties` dosyası oluşturuldu, tooalso gerek giriş noktası kodunuzu değiştirmek `entrypoint.sh` hello içinde `<applicationfolder>/<servicePkg>/Code/` klasör tooset hello özelliği `java.util.logging.config.file` çok`app.propertes` dosya. Merhaba girişi hello parçacığını aşağıdaki gibi görünmelidir:

```sh
java -Djava.library.path=$LD_LIBRARY_PATH -Djava.util.logging.config.file=<path tooapp.properties> -jar <service name>.jar
```


Bu yapılandırma sırasında dönen bir şekilde toplanmakta olan günlükleri sonuçlanır `/tmp/servicefabric/logs/`. Merhaba günlük dosyası bu durumda adlandırılan mysfapp%u.%g.log burada:
* **%u** benzersiz bir numara tooresolve eşzamanlı Java işlemleri arasındaki çakışmaları olan.
* **%g** hello nesil numara toodistinguish günlükleri döndürme arasında değil.

Hiçbir işleyici açıkça yapılandırdıysanız, varsayılan olarak hello konsol işleyicisi kaydedildi. Bir syslog /var/log/syslog altında hello günlükleri görüntüleyebilirsiniz.

Daha fazla bilgi için bkz: Merhaba [kod örnekleri github'da](http://github.com/Azure-Samples/service-fabric-java-getting-started).  


## <a name="debugging-service-fabric-c-applications"></a>Service Fabric C# uygulamalarının hatalarını ayıklama


Birden çok çerçeveyi CoreCLR uygulamaları Linux izleme için kullanılabilir. Daha fazla bilgi için bkz: [GitHub: günlüğü](http:/github.com/aspnet/logging).  EventSource tanıdık tooC # geliştiricileri, olduğundan ' CoreCLR örnekleri Linux izleme için bu makalede EventSource kullanır.

Merhaba ilk adım tooinclude System.Diagnostics.Tracing, böylelikle günlükleri toomemory, çıkış akışları veya konsol dosyalarını yazabilirsiniz.  EventSource kullanarak günlüğe kaydetme için proje tooyour project.json aşağıdaki hello ekleyin:

```
    "System.Diagnostics.StackTrace": "4.0.1"
```

Merhaba hizmet olayı için özel bir EventListener toolisten kullanın ve ardından bunları tootrace dosyaları uygun şekilde yönlendirir. Merhaba aşağıdaki kod parçacığını bir örnek uygulama EventSource ve özel EventListener kullanarak günlük gösterir:


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


Merhaba Yukarıdaki kod parçacığında çıkarır hello günlükleri tooa dosyasında `/tmp/MyServiceLog.txt`. Bu dosya adı güncelleştirilmesini toobe gerekir. Tooredirect hello günlükleri tooconsole olasılığına parçacığı özelleştirilmiş EventListener sınıfınızda aşağıdaki hello kullan:

```csharp
public static TextWriter Out = Console.Out;
```

Merhaba, örnekleri [C# örnekleri](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started) EventSource ve bir özel EventListener toolog olayları tooa dosyasını kullanın.



## <a name="next-steps"></a>Sonraki adımlar
Merhaba eklenen aynı izleme kodu tooyour uygulama uygulamanızın Azure bir kümede hello Tanılama ile de çalışır. Merhaba hello araçları için farklı seçenekleri ele ve açıklayan Bu makaleler kullanıma nasıl tooset bunları ayarlama.
* [Nasıl toocollect ile Azure tanılama günlükleri](service-fabric-diagnostics-how-to-setup-lad.md)
