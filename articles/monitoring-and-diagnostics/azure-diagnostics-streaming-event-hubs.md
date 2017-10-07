---
title: "aaaStreaming hello etkin yolunuzda olay hub'ları kullanarak Azure Tanılama verileri | Microsoft Docs"
description: "Olay hub'ları ile Azure tanılamaları yapılandırmayı ortak senaryoları için yönergeler de dahil olmak üzere tooend sonlandırın."
services: event-hubs
documentationcenter: na
author: rboucher
manager: carmonm
editor: 
ms.assetid: edeebaac-1c47-4b43-9687-f28e7e1e446a
ms.service: monitoring-and-diagnostics
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/13/2017
ms.author: robb
ms.openlocfilehash: a2528ddd0688d1c23a8631e769ca016dd79e4159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a>Olay hub'ları kullanarak hello etkin yolunuzda Azure Tanılama verileri akış
Azure tanılama esnek yöntemler toocollect ölçümleri sağlar ve oturumu bulut Hizmetleri sanal makineleri (VM'ler) ve sonuçları tooAzure depolama aktarın. Merhaba Mart 2016 (SDK 2.9) zaman dilimi içinde başlayarak, veri kaynaklarını tanılama toocustom gönderebilir ve etkin yolunuzda veri aktarımının saniye cinsinden kullanarak [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).

Desteklenen veri türleri şunlardır:

* Windows için Olay İzleme (ETW) olayları
* Performans sayaçları
* Windows olay günlükleri
* Uygulama günlükleri
* Azure tanılama altyapı günlükleri

Bu makalede nasıl tooend tooconfigure Azure Tanılama Olay hub'larından ile sona gösterilmektedir. Yönergeler de yaygın senaryolar aşağıdaki Merhaba sağlanır:

* Nasıl toocustomize hello ve tooEvent hub gönderilen ölçümleri
* Nasıl her ortamında toochange yapılandırmaları
* Nasıl tooview olay hub'ları veri akışı
* Nasıl tootroubleshoot hello bağlantı  

## <a name="prerequisites"></a>Ön koşullar
Olay hub'ları receieving Azure Tanılama verileri bulut Hizmetleri, sanal makineleri, sanal makine ölçek kümeleri ve Service Fabric başlangıç hello Azure SDK 2.9 ve Azure Araçları Visual Studio için karşılık gelen hello desteklenir.

* Azure tanılama uzantısını 1.6 ([veya daha sonra .NET 2.9 için Azure SDK](https://azure.microsoft.com/downloads/) bu varsayılan olarak hedefler)
* [Visual Studio 2013 veya üzeri](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* Var olan Azure tanılama yapılandırmalarında kullanarak bir uygulama bir *.wadcfgx* dosya ve yöntemleri aşağıdaki hello biri:
  * Visual Studio: [tanılama Azure bulut Hizmetleri ve sanal makineler için yapılandırma](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)
  * Windows PowerShell: [PowerShell kullanarak Azure Cloud Services tanılamayı etkinleştirme](../cloud-services/cloud-services-diagnostics-powershell.md)
* Olay hub'ları ad alanı Hello makale sağlanan [Event Hubs ile çalışmaya başlama](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a>Azure tanılama tooEvent hub havuz Bağlan
Varsayılan olarak, Azure tanılama günlüklerini ve ölçümleri tooan Azure depolama hesabı her zaman gönderir. Bir uygulama aynı zamanda veri tooEvent hub yeni ekleyerek gönderebilir **iç havuzlar** hello bölümünde **PublicConfig** / **WadCfg** hello öğesinin*.wadcfgx* dosya. Visual Studio'da hello *.wadcfgx* dosya yolu aşağıdaki hello depolanır: **bulut hizmeti projesini** > **rolleri** > **() RoleName)** > **diagnostics.wadcfgx** dosya.

```xml
<SinksConfig>
  <Sink name="HotPath">
    <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" />
  </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "HotPath",
            "EventHub": {
                "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
                "SharedAccessKeyName": "SendRule"
            }
        }
    ]
}
```

Bu örnekte, hello olay hub'ın ad alanı hello event hub'ı URL ayarlanmış toohello tam olarak nitelenmiş: olay hub'ları ad alanı + "/" + olay hub'ı adı.  

Merhaba event hub'ı URL hello görüntülenen [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) hello olay hub'ları Panoda.  

Merhaba **havuzu** adı hello aynı değere tutarlı bir şekilde hello yapılandırma dosyası kullanılan sürece tooany geçerli bir dize ayarlanabilir.

> [!NOTE]
> Olabilir ek havuzlarını aşağıdaki gibi *Applicationınsights* Bu bölümde yapılandırılmış. Azure tanılama sağlayan bir veya daha fazla havuzlarını her havuz da hello bildirilirse tanımlanan toobe **PrivateConfig** bölümü.  
>
>

Merhaba olay hub'ları havuz gerekir de bildirilen ve hello tanımlanan **PrivateConfig** hello bölümünü *.wadcfgx* yapılandırma dosyası.

```XML
<PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <StorageAccount name="{account name}" key="{account key}" endpoint="{optional storage endpoint}" />
  <EventHub Url="https://diags-mycompany-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
</PrivateConfig>
```
```JSON
{
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{optional storage endpoint}",
    "EventHub": {
        "Url": "https://diags-mycompany-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    }
}
```

Merhaba `SharedAccessKeyName` değeri bir paylaşılan erişim imzası (SAS) anahtarı ve hello tanımlanan ilke eşleşmelidir **olay hub'ları** ad alanı. Toohello olay hub'ları hello panosunda Gözat [Azure portal](https://manage.windowsazure.com), hello tıklatın **Yapılandır** sekmesini tıklatın ve sahip bir adlandırılmış ilkeyi kurmak (örneğin, "SendRule") *göndermek* izinler. Merhaba **StorageAccount** içinde bildirilmiş **PrivateConfig**. Gerek yoktur buraya toochange değerler bunlar çalışıyorsanız. Bu örnekte, biz hello değerleri boş bir aşağı akış varlık hello değerleri ayarlayacaksınız oturum olduğu bırakın. Örneğin, hello *ServiceConfiguration.Cloud.cscfg* ortam yapılandırma dosyası hello ortamı uygun adları ve anahtarları ayarlar.  

> [!WARNING]
> Merhaba olay hub'ları SAS anahtarı, düz metin olarak hello depolanır *.wadcfgx* dosya. Genellikle, bu anahtarı toosource kodu denetiminde denetlenir veya uygun şekilde korumanız gerekir böylece yapı sunucunuz bir varlığı olarak kullanılabilir. Bir SAS anahtarıyla burada kullanmanızı öneririz *yalnızca gönderme* izinleri böylece kötü niyetli bir kullanıcı toohello olay hub'ı, yazma ancak tooit dinlemek veya yönetme.
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a>Azure tanılama toosend günlüklerini ve ölçümleri tooEvent hub'ları yapılandırma
Tüm varsayılan ve özel tanılama veri daha önce açıklandığı gibi diğer bir deyişle, ölçümleri ve günlükleri, otomatik olarak gönderilir tooAzure depolama yapılandırılmış hello aralıklarla. Olay hub'ları ve ek bir havuz ile Merhaba hiyerarşi toobe toohello olay hub'ı gönderilen herhangi bir kök veya yaprak düğümü belirtebilirsiniz. Bu, ETW olayları, performans sayaçları, Windows olay günlüklerini ve uygulama günlükleri içerir.   

Kaç tane veri noktaları gerçekte olmalıdır tooconsider tooEvent hub aktarılan önemlidir. Genellikle, geliştiriciler tüketilen ve hızlı bir şekilde yorumlanır düşük gecikme süreli hot yolu veri aktarın. Uyarıları veya otomatik ölçeklendirme kurallarını izleyen örnekler sistemleridir. Bir geliştirici ayrıca bir alternatif analiz deposu yapılandırma veya deposu--Azure akış analizi, Elasticsearch, özel bir izleme sistemi veya diğer sık kullanılan bir izleme sistemi arama.

Merhaba, bazı örnek yapılandırmalar şunlardır.

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "sinks": "HotPath",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        }
    ]
}
```

Yukarıdaki örnek Hello hello havuz uygulanan toohello üst olduğu **performans sayaçları** tüm alt anlamına gelir hello hiyerarşisinde düğüm **performans sayaçları** tooEvent hub gönderilir.  

```xml
<PerformanceCounters scheduledTransferPeriod="PT1M">
  <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" sinks="HotPath" />
  <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" sinks="HotPath"/>
  <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" sinks="HotPath"/>
</PerformanceCounters>
```
```JSON
"PerformanceCounters": {
    "scheduledTransferPeriod": "PT1M",
    "PerformanceCounterConfiguration": [
        {
            "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\Memory\\Available MBytes",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
            "sampleRate": "PT3M"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Rejected",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        },
        {
            "counterSpecifier": "\\ASP.NET\\Requests Queued",
            "sampleRate": "PT3M",
            "sinks": "HotPath"
        }
    ]
}
```

Uygulanan tooonly üç sayaç hello havuz Hello önceki örnekte olduğu: **sıraya alınan istek sayısı**, **reddedilen istekleri**, ve **% işlemci zamanı**.  

Merhaba aşağıdaki örnek bir geliştirici bu hizmetin sistem durumu için kullanılan gönderilen veri toobe hello kritik ölçümleri hello miktarını nasıl sınırlayabilir gösterir.  

```XML
<Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
```
```JSON
"Logs": {
    "scheduledTransferPeriod": "PT1M",
    "scheduledTransferLogLevelFilter": "Error",
    "sinks": "HotPath"
}
```

Bu örnekte, hello havuz uygulanan toologs ve yalnızca filtrelenen tooerror düzeyi izleme.

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a>Dağıtma ve bulut Hizmetleri uygulama ve tanılama config güncelleştir
Visual Studio hello en kolay yolu toodeploy hello uygulama ve Event Hubs havuz yapılandırmasını sağlar. tooview ve düzenleme hello dosya, açık hello *.wadcfgx* dosya Visual Studio'da, düzenlemek ve dosyayı kaydedin. Merhaba yolu **bulut hizmeti projesini** > **rolleri** > **(RoleName)** > **diagnostics.wadcfgx**.  

Bu noktada, tüm dağıtım ve dağıtım eylemlerini Visual Studio, Visual Studio Team System ve tüm komutları veya MSBuild üzerinde temel alır ve hello kullanan betikler güncelleştirme **/t: yayımlama** hedef dahil hello *.wadcfgx*  hello paketleme işleminde. Ayrıca, dağıtımlar ve güncelleştirmeleri hello dosya tooAzure hello uygun Azure Tanılama Aracı Uzantısı Vm'leriniz kullanarak dağıtın.

Merhaba uygulaması ve Azure tanılama yapılandırması dağıttıktan sonra hemen hello panosunda hello olay hub'ın etkinliğini görür. Bu, tercih ettiğiniz hello dinleyicisi istemci ya da analiz aracı tooviewing hello hot yolu veriler üzerinde hazır toomove olduğunuz gösterir.  

Aşağıdaki şekilde hello tanılama veri toohello olay hub'ı süre 23'sonra Başlangıç sağlıklı gönderme hello olay hub'ları Panosu gösterir. Ne zaman olan hello uygulama dağıtılan güncelleştirilmiş ile *.wadcfgx* dosya ve hello havuzu düzgün bir şekilde yapılandırıldı.

![][0]  

> [!NOTE]
> Güncelleştirmeleri toohello Azure tanılama yapılandırma dosyası (.wadcfgx) yaptığınızda, Visual Studio yayımlama veya bir Windows PowerShell komut dosyası kullanarak hello güncelleştirmeleri toohello tüm uygulama ve bunun yanı sıra hello yapılandırma itme önerilir.  
>
>

## <a name="view-hot-path-data"></a>Hot yol verileri görüntüleme
Daha önce anlatıldığı gibi birçok kullanım durumları için olay hub'ları veri işleme dinleme tooand vardır.

Bir basit toocreate bir küçük test konsol uygulaması toolisten toohello olay hub'ı ve yazdırma hello çıkış akışı yaklaşımdır. Daha ayrıntılı olarak anlatılmıştır kod aşağıdaki hello yerleştirebilirsiniz [Event Hubs ile çalışmaya başlama](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), bir konsol uygulamasında.  

Merhaba konsol uygulaması hello içermelidir Not [olay işlemcisi konağı NuGet paketi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).  

Merhaba açılı ayraç tooreplace hello değerleri unutmayın **ana** kaynaklarınız için değerlerle işlevi.   

```csharp
//Console application code for EventHub test client
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using Microsoft.ServiceBus.Messaging;

namespace EventHubListener
{
    class SimpleEventProcessor : IEventProcessor
    {
        Stopwatch checkpointStopWatch;

        async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
            if (reason == CloseReason.Shutdown)
            {
                await context.CheckpointAsync();
            }
        }

        Task IEventProcessor.OpenAsync(PartitionContext context)
        {
            Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
            this.checkpointStopWatch = new Stopwatch();
            this.checkpointStopWatch.Start();
            return Task.FromResult<object>(null);
        }

        async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (EventData eventData in messages)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                    Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                        context.Lease.PartitionId, data));

                foreach (var x in eventData.Properties)
                {
                    Console.WriteLine(string.Format("    {0} = {1}", x.Key, x.Value));
                }
            }

            //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
            if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
            {
                await context.CheckpointAsync();
                this.checkpointStopWatch.Restart();
            }
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            string eventHubConnectionString = "Endpoint= <your connection string>”
            string eventHubName = "<Event hub name>";
            string storageAccountName = "<Storage account name>";
            string storageAccountKey = "<Storage account key>”;
            string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);

            string eventProcessorHostName = Guid.NewGuid().ToString();
            EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
            Console.WriteLine("Registering EventProcessor...");
            var options = new EventProcessorOptions();
            options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
            eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();

            Console.WriteLine("Receiving. Press enter key toostop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a>Olay hub'ları havuzlarını sorun giderme
* Merhaba olay hub'ı beklendiği gibi gelen veya giden olay etkinlik göstermez.

    Olay hub'ınızı başarıyla sağlandığından emin olun. Merhaba, tüm bağlantı bilgisi **PrivateConfig** bölümünü *.wadcfgx* kaynağınız hello değerlerini hello Portalı'nda görülen eşleşmesi gerekir. Tanımlanan bir SAS İlkesi (Merhaba örnekte "SendRule") hello portal ve sahip olduğunuzdan emin olun *Gönder* izin verilir.  
* Bir güncelleştirme sonrası hello olay hub'ı artık gelen veya giden olay etkinliğini gösterir.

    İlk olarak, hello olay hub'ı ve yapılandırma bilgileri daha önce açıklandığı gibi doğru olduğundan emin olun. Bazen hello **PrivateConfig** dağıtım güncelleştirmede sıfırlanır. Merhaba önerilir düzeltme tüm değişiklikler çok toomake*.wadcfgx* hello proje ve tam uygulama güncelleştirmesi Anında iletme. Bu mümkün değilse, bu hello tanılama güncelleştirmeyi iter tamamı emin olun **PrivateConfig** hello SAS anahtarı içerir.  
* Merhaba önerileri denedi ve hello olay hub'ı hala çalışmıyor.

    Günlükleri ve hataları Azure tanılama için kendisini içeren hello Azure Storage tablo bakarak deneyin: **WADDiagnosticInfrastructureLogsTable**. Bir seçenektir toouse gibi bir araç [Azure Storage Gezgini](http://www.storageexplorer.com) tooconnect toothis depolama hesabı, bu tabloyu görüntülemek ve bir sorgu için zaman damgası hello son 24 saat ekleyin. Merhaba aracı tooexport bir .csv dosyasını kullanın ve Microsoft Excel gibi bir uygulamada açın. Excel kılar arama kartı dizeleri için kolay toosearch gibi **EventHubs**, toosee hangi hata bildirilir.  

## <a name="next-steps"></a>Sonraki adımlar
• [Event Hubs hakkında daha fazla bilgi edinin](https://azure.microsoft.com/services/event-hubs/)

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a>Ek: Azure tanılama yapılandırma dosyası (.wadcfgx) örneği tamamlayın
```xml
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticsConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <WadCfg>
      <DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="applicationInsights.errors">
        <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter="Error" />
        <Directories scheduledTransferPeriod="PT1M">
          <IISLogs containerName="wad-iis-logfiles" />
          <FailedRequestLogs containerName="wad-failedrequestlogs" />
        </Directories>
        <PerformanceCounters scheduledTransferPeriod="PT1M" sinks="HotPath">
          <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
        </PerformanceCounters>
        <WindowsEventLog scheduledTransferPeriod="PT1M">
          <DataSource name="Application!*" />
        </WindowsEventLog>
        <CrashDumps>
          <CrashDumpConfiguration processName="WaIISHost.exe" />
          <CrashDumpConfiguration processName="WaWorkerHost.exe" />
          <CrashDumpConfiguration processName="w3wp.exe" />
        </CrashDumps>
        <Logs scheduledTransferPeriod="PT1M" sinks="HotPath" scheduledTransferLogLevelFilter="Error" />
      </DiagnosticMonitorConfiguration>
      <SinksConfig>
        <Sink name="HotPath">
          <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" />
        </Sink>
        <Sink name="applicationInsights">
          <ApplicationInsights />
          <Channels>
            <Channel logLevel="Error" name="errors" />
          </Channels>
        </Sink>
      </SinksConfig>
    </WadCfg>
    <StorageAccount>ACCOUNT_NAME</StorageAccount>
  </PublicConfig>
  <PrivateConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
    <StorageAccount name="{account name}" key="{account key}" endpoint="{storage endpoint}" />
    <EventHub Url="https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py" SharedAccessKeyName="SendRule" SharedAccessKey="YOUR_KEY_HERE" />
  </PrivateConfig>
  <IsEnabled>true</IsEnabled>
</DiagnosticsConfiguration>
```

Merhaba tamamlayıcı *ServiceConfiguration.Cloud.cscfg* için bu örnek hello aşağıdaki gibi görünür.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="MyFixItCloudService" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2015-04.2.6">
  <Role name="MyFixIt.WorkerRole">
    <Instances count="1" />
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="YOUR_CONNECTION_STRING" />
    </ConfigurationSettings>
  </Role>
</ServiceConfiguration>
```

Sanal makineler için eşdeğer tabanlı Json ayarlar aşağıdaki gibidir:
```JSON
"settings": {
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 4096,
            "sinks": "applicationInsights.errors",
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "Directories": {
                "scheduledTransferPeriod": "PT1M",
                "IISLogs": {
                    "containerName": "wad-iis-logfiles"
                },
                "FailedRequestLogs": {
                    "containerName": "wad-failedrequestlogs"
                }
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "sinks": "HotPath",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Memory\\Available MBytes",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\ISAPI Extension Requests/sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Web Service(_Total)\\Bytes Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Requests/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET Applications(__Total__)\\Errors Total/Sec",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Queued",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\ASP.NET\\Requests Rejected",
                        "sampleRate": "PT3M"
                    },
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT3M"
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT1M",
                "DataSource": [
                    {
                        "name": "Application!*"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Error",
                "sinks": "HotPath"
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "HotPath",
                    "EventHub": {
                        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
                        "SharedAccessKeyName": "SendRule"
                    }
                },
                {
                    "name": "applicationInsights",
                    "ApplicationInsights": "",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "errors"
                            }
                        ]
                    }
                }
            ]
        }
    },
    "StorageAccount": "{account name}"
}


"protectedSettings": {
    "storageAccountName": "{account name}",
    "storageAccountKey": "{account key}",
    "storageAccountEndPoint": "{storage endpoint}",
    "EventHub": {
        "Url": "https://diageventhub-py-ns.servicebus.windows.net/diageventhub-py",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "YOUR_KEY_HERE"
    }
}
```

## <a name="next-steps"></a>Sonraki adımlar
Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:

* [Event Hubs’a genel bakış](../event-hubs/event-hubs-what-is-event-hubs.md)
* [Olay Hub’ı oluşturma](../event-hubs/event-hubs-create.md)
* [Event Hubs ile ilgili SSS](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
