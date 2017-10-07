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
# <a name="streaming-azure-diagnostics-data-in-hello-hot-path-by-using-event-hubs"></a><span data-ttu-id="e8884-103">Olay hub'ları kullanarak hello etkin yolunuzda Azure Tanılama verileri akış</span><span class="sxs-lookup"><span data-stu-id="e8884-103">Streaming Azure Diagnostics data in hello hot path by using Event Hubs</span></span>
<span data-ttu-id="e8884-104">Azure tanılama esnek yöntemler toocollect ölçümleri sağlar ve oturumu bulut Hizmetleri sanal makineleri (VM'ler) ve sonuçları tooAzure depolama aktarın.</span><span class="sxs-lookup"><span data-stu-id="e8884-104">Azure Diagnostics provides flexible ways toocollect metrics and logs from cloud services virtual machines (VMs) and transfer results tooAzure Storage.</span></span> <span data-ttu-id="e8884-105">Merhaba Mart 2016 (SDK 2.9) zaman dilimi içinde başlayarak, veri kaynaklarını tanılama toocustom gönderebilir ve etkin yolunuzda veri aktarımının saniye cinsinden kullanarak [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="e8884-105">Starting in hello March 2016 (SDK 2.9) time frame, you can send Diagnostics toocustom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="e8884-106">Desteklenen veri türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e8884-106">Supported data types include:</span></span>

* <span data-ttu-id="e8884-107">Windows için Olay İzleme (ETW) olayları</span><span class="sxs-lookup"><span data-stu-id="e8884-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="e8884-108">Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="e8884-108">Performance counters</span></span>
* <span data-ttu-id="e8884-109">Windows olay günlükleri</span><span class="sxs-lookup"><span data-stu-id="e8884-109">Windows event logs</span></span>
* <span data-ttu-id="e8884-110">Uygulama günlükleri</span><span class="sxs-lookup"><span data-stu-id="e8884-110">Application logs</span></span>
* <span data-ttu-id="e8884-111">Azure tanılama altyapı günlükleri</span><span class="sxs-lookup"><span data-stu-id="e8884-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="e8884-112">Bu makalede nasıl tooend tooconfigure Azure Tanılama Olay hub'larından ile sona gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="e8884-112">This article shows you how tooconfigure Azure Diagnostics with Event Hubs from end tooend.</span></span> <span data-ttu-id="e8884-113">Yönergeler de yaygın senaryolar aşağıdaki Merhaba sağlanır:</span><span class="sxs-lookup"><span data-stu-id="e8884-113">Guidance is also provided for hello following common scenarios:</span></span>

* <span data-ttu-id="e8884-114">Nasıl toocustomize hello ve tooEvent hub gönderilen ölçümleri</span><span class="sxs-lookup"><span data-stu-id="e8884-114">How toocustomize hello logs and metrics that get sent tooEvent Hubs</span></span>
* <span data-ttu-id="e8884-115">Nasıl her ortamında toochange yapılandırmaları</span><span class="sxs-lookup"><span data-stu-id="e8884-115">How toochange configurations in each environment</span></span>
* <span data-ttu-id="e8884-116">Nasıl tooview olay hub'ları veri akışı</span><span class="sxs-lookup"><span data-stu-id="e8884-116">How tooview Event Hubs stream data</span></span>
* <span data-ttu-id="e8884-117">Nasıl tootroubleshoot hello bağlantı</span><span class="sxs-lookup"><span data-stu-id="e8884-117">How tootroubleshoot hello connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="e8884-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e8884-118">Prerequisites</span></span>
<span data-ttu-id="e8884-119">Olay hub'ları receieving Azure Tanılama verileri bulut Hizmetleri, sanal makineleri, sanal makine ölçek kümeleri ve Service Fabric başlangıç hello Azure SDK 2.9 ve Azure Araçları Visual Studio için karşılık gelen hello desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e8884-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in hello Azure SDK 2.9 and hello corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="e8884-120">Azure tanılama uzantısını 1.6 ([veya daha sonra .NET 2.9 için Azure SDK](https://azure.microsoft.com/downloads/) bu varsayılan olarak hedefler)</span><span class="sxs-lookup"><span data-stu-id="e8884-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="e8884-121">Visual Studio 2013 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="e8884-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="e8884-122">Var olan Azure tanılama yapılandırmalarında kullanarak bir uygulama bir *.wadcfgx* dosya ve yöntemleri aşağıdaki hello biri:</span><span class="sxs-lookup"><span data-stu-id="e8884-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of hello following methods:</span></span>
  * <span data-ttu-id="e8884-123">Visual Studio: [tanılama Azure bulut Hizmetleri ve sanal makineler için yapılandırma](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="e8884-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="e8884-124">Windows PowerShell: [PowerShell kullanarak Azure Cloud Services tanılamayı etkinleştirme](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="e8884-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="e8884-125">Olay hub'ları ad alanı Hello makale sağlanan [Event Hubs ile çalışmaya başlama](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="e8884-125">Event Hubs namespace provisioned per hello article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-tooevent-hubs-sink"></a><span data-ttu-id="e8884-126">Azure tanılama tooEvent hub havuz Bağlan</span><span class="sxs-lookup"><span data-stu-id="e8884-126">Connect Azure Diagnostics tooEvent Hubs sink</span></span>
<span data-ttu-id="e8884-127">Varsayılan olarak, Azure tanılama günlüklerini ve ölçümleri tooan Azure depolama hesabı her zaman gönderir.</span><span class="sxs-lookup"><span data-stu-id="e8884-127">By default, Azure Diagnostics always sends logs and metrics tooan Azure Storage account.</span></span> <span data-ttu-id="e8884-128">Bir uygulama aynı zamanda veri tooEvent hub yeni ekleyerek gönderebilir **iç havuzlar** hello bölümünde **PublicConfig** / **WadCfg** hello öğesinin*.wadcfgx* dosya.</span><span class="sxs-lookup"><span data-stu-id="e8884-128">An application may also send data tooEvent Hubs by adding a new **Sinks** section under hello **PublicConfig** / **WadCfg** element of hello *.wadcfgx* file.</span></span> <span data-ttu-id="e8884-129">Visual Studio'da hello *.wadcfgx* dosya yolu aşağıdaki hello depolanır: **bulut hizmeti projesini** > **rolleri** > **() RoleName)** > **diagnostics.wadcfgx** dosya.</span><span class="sxs-lookup"><span data-stu-id="e8884-129">In Visual Studio, hello *.wadcfgx* file is stored in hello following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

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

<span data-ttu-id="e8884-130">Bu örnekte, hello olay hub'ın ad alanı hello event hub'ı URL ayarlanmış toohello tam olarak nitelenmiş: olay hub'ları ad alanı + "/" + olay hub'ı adı.</span><span class="sxs-lookup"><span data-stu-id="e8884-130">In this example, hello event hub URL is set toohello fully qualified namespace of hello event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="e8884-131">Merhaba event hub'ı URL hello görüntülenen [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) hello olay hub'ları Panoda.</span><span class="sxs-lookup"><span data-stu-id="e8884-131">hello event hub URL is displayed in hello [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on hello Event Hubs dashboard.</span></span>  

<span data-ttu-id="e8884-132">Merhaba **havuzu** adı hello aynı değere tutarlı bir şekilde hello yapılandırma dosyası kullanılan sürece tooany geçerli bir dize ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e8884-132">hello **Sink** name can be set tooany valid string as long as hello same value is used consistently throughout hello config file.</span></span>

> [!NOTE]
> <span data-ttu-id="e8884-133">Olabilir ek havuzlarını aşağıdaki gibi *Applicationınsights* Bu bölümde yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="e8884-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="e8884-134">Azure tanılama sağlayan bir veya daha fazla havuzlarını her havuz da hello bildirilirse tanımlanan toobe **PrivateConfig** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e8884-134">Azure Diagnostics allows one or more sinks toobe defined if each sink is also declared in hello **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="e8884-135">Merhaba olay hub'ları havuz gerekir de bildirilen ve hello tanımlanan **PrivateConfig** hello bölümünü *.wadcfgx* yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="e8884-135">hello Event Hubs sink must also be declared and defined in hello **PrivateConfig** section of hello *.wadcfgx* config file.</span></span>

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

<span data-ttu-id="e8884-136">Merhaba `SharedAccessKeyName` değeri bir paylaşılan erişim imzası (SAS) anahtarı ve hello tanımlanan ilke eşleşmelidir **olay hub'ları** ad alanı.</span><span class="sxs-lookup"><span data-stu-id="e8884-136">hello `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in hello **Event Hubs** namespace.</span></span> <span data-ttu-id="e8884-137">Toohello olay hub'ları hello panosunda Gözat [Azure portal](https://manage.windowsazure.com), hello tıklatın **Yapılandır** sekmesini tıklatın ve sahip bir adlandırılmış ilkeyi kurmak (örneğin, "SendRule") *göndermek* izinler.</span><span class="sxs-lookup"><span data-stu-id="e8884-137">Browse toohello Event Hubs dashboard in hello [Azure portal](https://manage.windowsazure.com), click hello **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="e8884-138">Merhaba **StorageAccount** içinde bildirilmiş **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="e8884-138">hello **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="e8884-139">Gerek yoktur buraya toochange değerler bunlar çalışıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="e8884-139">There is no need toochange values here if they are working.</span></span> <span data-ttu-id="e8884-140">Bu örnekte, biz hello değerleri boş bir aşağı akış varlık hello değerleri ayarlayacaksınız oturum olduğu bırakın.</span><span class="sxs-lookup"><span data-stu-id="e8884-140">In this example, we leave hello values empty, which is a sign that a downstream asset will set hello values.</span></span> <span data-ttu-id="e8884-141">Örneğin, hello *ServiceConfiguration.Cloud.cscfg* ortam yapılandırma dosyası hello ortamı uygun adları ve anahtarları ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e8884-141">For example, hello *ServiceConfiguration.Cloud.cscfg* environment configuration file sets hello environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="e8884-142">Merhaba olay hub'ları SAS anahtarı, düz metin olarak hello depolanır *.wadcfgx* dosya.</span><span class="sxs-lookup"><span data-stu-id="e8884-142">hello Event Hubs SAS key is stored in plain text in hello *.wadcfgx* file.</span></span> <span data-ttu-id="e8884-143">Genellikle, bu anahtarı toosource kodu denetiminde denetlenir veya uygun şekilde korumanız gerekir böylece yapı sunucunuz bir varlığı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="e8884-143">Often, this key is checked in toosource code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="e8884-144">Bir SAS anahtarıyla burada kullanmanızı öneririz *yalnızca gönderme* izinleri böylece kötü niyetli bir kullanıcı toohello olay hub'ı, yazma ancak tooit dinlemek veya yönetme.</span><span class="sxs-lookup"><span data-stu-id="e8884-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write toohello event hub, but not listen tooit or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-toosend-logs-and-metrics-tooevent-hubs"></a><span data-ttu-id="e8884-145">Azure tanılama toosend günlüklerini ve ölçümleri tooEvent hub'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e8884-145">Configure Azure Diagnostics toosend logs and metrics tooEvent Hubs</span></span>
<span data-ttu-id="e8884-146">Tüm varsayılan ve özel tanılama veri daha önce açıklandığı gibi diğer bir deyişle, ölçümleri ve günlükleri, otomatik olarak gönderilir tooAzure depolama yapılandırılmış hello aralıklarla.</span><span class="sxs-lookup"><span data-stu-id="e8884-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent tooAzure Storage in hello configured intervals.</span></span> <span data-ttu-id="e8884-147">Olay hub'ları ve ek bir havuz ile Merhaba hiyerarşi toobe toohello olay hub'ı gönderilen herhangi bir kök veya yaprak düğümü belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e8884-147">With Event Hubs and any additional sink, you can specify any root or leaf node in hello hierarchy toobe sent toohello event hub.</span></span> <span data-ttu-id="e8884-148">Bu, ETW olayları, performans sayaçları, Windows olay günlüklerini ve uygulama günlükleri içerir.</span><span class="sxs-lookup"><span data-stu-id="e8884-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="e8884-149">Kaç tane veri noktaları gerçekte olmalıdır tooconsider tooEvent hub aktarılan önemlidir.</span><span class="sxs-lookup"><span data-stu-id="e8884-149">It is important tooconsider how many data points should actually be transferred tooEvent Hubs.</span></span> <span data-ttu-id="e8884-150">Genellikle, geliştiriciler tüketilen ve hızlı bir şekilde yorumlanır düşük gecikme süreli hot yolu veri aktarın.</span><span class="sxs-lookup"><span data-stu-id="e8884-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="e8884-151">Uyarıları veya otomatik ölçeklendirme kurallarını izleyen örnekler sistemleridir.</span><span class="sxs-lookup"><span data-stu-id="e8884-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="e8884-152">Bir geliştirici ayrıca bir alternatif analiz deposu yapılandırma veya deposu--Azure akış analizi, Elasticsearch, özel bir izleme sistemi veya diğer sık kullanılan bir izleme sistemi arama.</span><span class="sxs-lookup"><span data-stu-id="e8884-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="e8884-153">Merhaba, bazı örnek yapılandırmalar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="e8884-153">hello following are some example configurations.</span></span>

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

<span data-ttu-id="e8884-154">Yukarıdaki örnek Hello hello havuz uygulanan toohello üst olduğu **performans sayaçları** tüm alt anlamına gelir hello hiyerarşisinde düğüm **performans sayaçları** tooEvent hub gönderilir.</span><span class="sxs-lookup"><span data-stu-id="e8884-154">In hello above example, hello sink is applied toohello parent **PerformanceCounters** node in hello hierarchy, which means all child **PerformanceCounters** will be sent tooEvent Hubs.</span></span>  

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

<span data-ttu-id="e8884-155">Uygulanan tooonly üç sayaç hello havuz Hello önceki örnekte olduğu: **sıraya alınan istek sayısı**, **reddedilen istekleri**, ve **% işlemci zamanı**.</span><span class="sxs-lookup"><span data-stu-id="e8884-155">In hello previous example, hello sink is applied tooonly three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="e8884-156">Merhaba aşağıdaki örnek bir geliştirici bu hizmetin sistem durumu için kullanılan gönderilen veri toobe hello kritik ölçümleri hello miktarını nasıl sınırlayabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="e8884-156">hello following example shows how a developer can limit hello amount of sent data toobe hello critical metrics that are used for this service’s health.</span></span>  

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

<span data-ttu-id="e8884-157">Bu örnekte, hello havuz uygulanan toologs ve yalnızca filtrelenen tooerror düzeyi izleme.</span><span class="sxs-lookup"><span data-stu-id="e8884-157">In this example, hello sink is applied toologs and is filtered only tooerror level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="e8884-158">Dağıtma ve bulut Hizmetleri uygulama ve tanılama config güncelleştir</span><span class="sxs-lookup"><span data-stu-id="e8884-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="e8884-159">Visual Studio hello en kolay yolu toodeploy hello uygulama ve Event Hubs havuz yapılandırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e8884-159">Visual Studio provides hello easiest path toodeploy hello application and Event Hubs sink configuration.</span></span> <span data-ttu-id="e8884-160">tooview ve düzenleme hello dosya, açık hello *.wadcfgx* dosya Visual Studio'da, düzenlemek ve dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e8884-160">tooview and edit hello file, open hello *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="e8884-161">Merhaba yolu **bulut hizmeti projesini** > **rolleri** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="e8884-161">hello path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="e8884-162">Bu noktada, tüm dağıtım ve dağıtım eylemlerini Visual Studio, Visual Studio Team System ve tüm komutları veya MSBuild üzerinde temel alır ve hello kullanan betikler güncelleştirme **/t: yayımlama** hedef dahil hello *.wadcfgx*  hello paketleme işleminde.</span><span class="sxs-lookup"><span data-stu-id="e8884-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use hello **/t:publish** target include hello *.wadcfgx* in hello packaging process.</span></span> <span data-ttu-id="e8884-163">Ayrıca, dağıtımlar ve güncelleştirmeleri hello dosya tooAzure hello uygun Azure Tanılama Aracı Uzantısı Vm'leriniz kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e8884-163">In addition, deployments and updates deploy hello file tooAzure by using hello appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="e8884-164">Merhaba uygulaması ve Azure tanılama yapılandırması dağıttıktan sonra hemen hello panosunda hello olay hub'ın etkinliğini görür.</span><span class="sxs-lookup"><span data-stu-id="e8884-164">After you deploy hello application and Azure Diagnostics configuration, you will immediately see activity in hello dashboard of hello event hub.</span></span> <span data-ttu-id="e8884-165">Bu, tercih ettiğiniz hello dinleyicisi istemci ya da analiz aracı tooviewing hello hot yolu veriler üzerinde hazır toomove olduğunuz gösterir.</span><span class="sxs-lookup"><span data-stu-id="e8884-165">This indicates that you're ready toomove on tooviewing hello hot-path data in hello listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="e8884-166">Aşağıdaki şekilde hello tanılama veri toohello olay hub'ı süre 23'sonra Başlangıç sağlıklı gönderme hello olay hub'ları Panosu gösterir.</span><span class="sxs-lookup"><span data-stu-id="e8884-166">In hello following figure, hello Event Hubs dashboard shows healthy sending of diagnostics data toohello event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="e8884-167">Ne zaman olan hello uygulama dağıtılan güncelleştirilmiş ile *.wadcfgx* dosya ve hello havuzu düzgün bir şekilde yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="e8884-167">That's when hello application was deployed with an updated *.wadcfgx* file, and hello sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="e8884-168">Güncelleştirmeleri toohello Azure tanılama yapılandırma dosyası (.wadcfgx) yaptığınızda, Visual Studio yayımlama veya bir Windows PowerShell komut dosyası kullanarak hello güncelleştirmeleri toohello tüm uygulama ve bunun yanı sıra hello yapılandırma itme önerilir.</span><span class="sxs-lookup"><span data-stu-id="e8884-168">When you make updates toohello Azure Diagnostics config file (.wadcfgx), it's recommended that you push hello updates toohello entire application as well as hello configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="e8884-169">Hot yol verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e8884-169">View hot-path data</span></span>
<span data-ttu-id="e8884-170">Daha önce anlatıldığı gibi birçok kullanım durumları için olay hub'ları veri işleme dinleme tooand vardır.</span><span class="sxs-lookup"><span data-stu-id="e8884-170">As discussed previously, there are many use cases for listening tooand processing Event Hubs data.</span></span>

<span data-ttu-id="e8884-171">Bir basit toocreate bir küçük test konsol uygulaması toolisten toohello olay hub'ı ve yazdırma hello çıkış akışı yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="e8884-171">One simple approach is toocreate a small test console application toolisten toohello event hub and print hello output stream.</span></span> <span data-ttu-id="e8884-172">Daha ayrıntılı olarak anlatılmıştır kod aşağıdaki hello yerleştirebilirsiniz [Event Hubs ile çalışmaya başlama](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), bir konsol uygulamasında.</span><span class="sxs-lookup"><span data-stu-id="e8884-172">You can place hello following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="e8884-173">Merhaba konsol uygulaması hello içermelidir Not [olay işlemcisi konağı NuGet paketi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="e8884-173">Note that hello console application must include hello [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="e8884-174">Merhaba açılı ayraç tooreplace hello değerleri unutmayın **ana** kaynaklarınız için değerlerle işlevi.</span><span class="sxs-lookup"><span data-stu-id="e8884-174">Remember tooreplace hello values in angle brackets in hello **Main** function with values for your resources.</span></span>   

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

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="e8884-175">Olay hub'ları havuzlarını sorun giderme</span><span class="sxs-lookup"><span data-stu-id="e8884-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="e8884-176">Merhaba olay hub'ı beklendiği gibi gelen veya giden olay etkinlik göstermez.</span><span class="sxs-lookup"><span data-stu-id="e8884-176">hello event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="e8884-177">Olay hub'ınızı başarıyla sağlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="e8884-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="e8884-178">Merhaba, tüm bağlantı bilgisi **PrivateConfig** bölümünü *.wadcfgx* kaynağınız hello değerlerini hello Portalı'nda görülen eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e8884-178">All connection info in hello **PrivateConfig** section of *.wadcfgx* must match hello values of your resource as seen in hello portal.</span></span> <span data-ttu-id="e8884-179">Tanımlanan bir SAS İlkesi (Merhaba örnekte "SendRule") hello portal ve sahip olduğunuzdan emin olun *Gönder* izin verilir.</span><span class="sxs-lookup"><span data-stu-id="e8884-179">Make sure that you have a SAS policy defined ("SendRule" in hello example) in hello portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="e8884-180">Bir güncelleştirme sonrası hello olay hub'ı artık gelen veya giden olay etkinliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="e8884-180">After an update, hello event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="e8884-181">İlk olarak, hello olay hub'ı ve yapılandırma bilgileri daha önce açıklandığı gibi doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e8884-181">First, make sure that hello event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="e8884-182">Bazen hello **PrivateConfig** dağıtım güncelleştirmede sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="e8884-182">Sometimes hello **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="e8884-183">Merhaba önerilir düzeltme tüm değişiklikler çok toomake*.wadcfgx* hello proje ve tam uygulama güncelleştirmesi Anında iletme.</span><span class="sxs-lookup"><span data-stu-id="e8884-183">hello recommended fix is toomake all changes too*.wadcfgx* in hello project and then push a complete application update.</span></span> <span data-ttu-id="e8884-184">Bu mümkün değilse, bu hello tanılama güncelleştirmeyi iter tamamı emin olun **PrivateConfig** hello SAS anahtarı içerir.</span><span class="sxs-lookup"><span data-stu-id="e8884-184">If this is not possible, make sure that hello diagnostics update pushes a complete **PrivateConfig** that includes hello SAS key.</span></span>  
* <span data-ttu-id="e8884-185">Merhaba önerileri denedi ve hello olay hub'ı hala çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="e8884-185">I tried hello suggestions, and hello event hub is still not working.</span></span>

    <span data-ttu-id="e8884-186">Günlükleri ve hataları Azure tanılama için kendisini içeren hello Azure Storage tablo bakarak deneyin: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="e8884-186">Try looking in hello Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="e8884-187">Bir seçenektir toouse gibi bir araç [Azure Storage Gezgini](http://www.storageexplorer.com) tooconnect toothis depolama hesabı, bu tabloyu görüntülemek ve bir sorgu için zaman damgası hello son 24 saat ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e8884-187">One option is toouse a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) tooconnect toothis storage account, view this table, and add a query for TimeStamp in hello last 24 hours.</span></span> <span data-ttu-id="e8884-188">Merhaba aracı tooexport bir .csv dosyasını kullanın ve Microsoft Excel gibi bir uygulamada açın.</span><span class="sxs-lookup"><span data-stu-id="e8884-188">You can use hello tool tooexport a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="e8884-189">Excel kılar arama kartı dizeleri için kolay toosearch gibi **EventHubs**, toosee hangi hata bildirilir.</span><span class="sxs-lookup"><span data-stu-id="e8884-189">Excel makes it easy toosearch for calling-card strings, such as **EventHubs**, toosee what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e8884-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e8884-190">Next steps</span></span>
<span data-ttu-id="e8884-191">• [Event Hubs hakkında daha fazla bilgi edinin](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="e8884-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="e8884-192">Ek: Azure tanılama yapılandırma dosyası (.wadcfgx) örneği tamamlayın</span><span class="sxs-lookup"><span data-stu-id="e8884-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
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

<span data-ttu-id="e8884-193">Merhaba tamamlayıcı *ServiceConfiguration.Cloud.cscfg* için bu örnek hello aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="e8884-193">hello complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like hello following.</span></span>

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

<span data-ttu-id="e8884-194">Sanal makineler için eşdeğer tabanlı Json ayarlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="e8884-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="e8884-195">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e8884-195">Next steps</span></span>
<span data-ttu-id="e8884-196">Bağlantılar aşağıdaki hello ziyaret ederek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e8884-196">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="e8884-197">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="e8884-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="e8884-198">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e8884-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="e8884-199">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="e8884-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
