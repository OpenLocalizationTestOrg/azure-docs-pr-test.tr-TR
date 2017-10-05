---
title: "Olay hub'ları kullanarak etkin yolunuzda Azure Tanılama verileri akış | Microsoft Docs"
description: "Olay hub'ları yaygın senaryoları için yönergeler de dahil olmak üzere uca, ile Azure tanılama yapılandırılıyor."
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
ms.openlocfilehash: 1c05bd6dc4c4d394aa043b9995de9c184e4f14c6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="streaming-azure-diagnostics-data-in-the-hot-path-by-using-event-hubs"></a><span data-ttu-id="98db6-103">Olay hub'ları kullanarak Azure Tanılama verileri etkin yolunuzda akış</span><span class="sxs-lookup"><span data-stu-id="98db6-103">Streaming Azure Diagnostics data in the hot path by using Event Hubs</span></span>
<span data-ttu-id="98db6-104">Azure tanılama bulut Hizmetleri sanal makinelerden (VM'ler) ölçümleri ve günlükleri toplamak ve sonuçları Azure depolama birimine aktarmak için esnek yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="98db6-104">Azure Diagnostics provides flexible ways to collect metrics and logs from cloud services virtual machines (VMs) and transfer results to Azure Storage.</span></span> <span data-ttu-id="98db6-105">Mart 2016 (SDK 2.9) zaman çerçevesinde başlayarak, özel veri kaynaklarına tanılama gönderebilir ve etkin yolunuzda veri aktarımının saniye cinsinden kullanarak [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span><span class="sxs-lookup"><span data-stu-id="98db6-105">Starting in the March 2016 (SDK 2.9) time frame, you can send Diagnostics to custom data sources and transfer hot path data in seconds by using [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/).</span></span>

<span data-ttu-id="98db6-106">Desteklenen veri türleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="98db6-106">Supported data types include:</span></span>

* <span data-ttu-id="98db6-107">Windows için Olay İzleme (ETW) olayları</span><span class="sxs-lookup"><span data-stu-id="98db6-107">Event Tracing for Windows (ETW) events</span></span>
* <span data-ttu-id="98db6-108">Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="98db6-108">Performance counters</span></span>
* <span data-ttu-id="98db6-109">Windows olay günlükleri</span><span class="sxs-lookup"><span data-stu-id="98db6-109">Windows event logs</span></span>
* <span data-ttu-id="98db6-110">Uygulama günlükleri</span><span class="sxs-lookup"><span data-stu-id="98db6-110">Application logs</span></span>
* <span data-ttu-id="98db6-111">Azure tanılama altyapı günlükleri</span><span class="sxs-lookup"><span data-stu-id="98db6-111">Azure Diagnostics infrastructure logs</span></span>

<span data-ttu-id="98db6-112">Bu makalede Azure tanılama uçtan uca olay hub'larıyla yapılandırma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="98db6-112">This article shows you how to configure Azure Diagnostics with Event Hubs from end to end.</span></span> <span data-ttu-id="98db6-113">Yönergeler ayrıca aşağıdaki ortak senaryolar için sağlanır:</span><span class="sxs-lookup"><span data-stu-id="98db6-113">Guidance is also provided for the following common scenarios:</span></span>

* <span data-ttu-id="98db6-114">Günlükleri ve Event Hubs'a gönderilen ölçümleri nasıl özelleştirileceği</span><span class="sxs-lookup"><span data-stu-id="98db6-114">How to customize the logs and metrics that get sent to Event Hubs</span></span>
* <span data-ttu-id="98db6-115">Her ortamda yapılandırmalarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="98db6-115">How to change configurations in each environment</span></span>
* <span data-ttu-id="98db6-116">Olay hub'ları akış verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="98db6-116">How to view Event Hubs stream data</span></span>
* <span data-ttu-id="98db6-117">Bağlantı ile ilgili sorunları giderme</span><span class="sxs-lookup"><span data-stu-id="98db6-117">How to troubleshoot the connection</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="98db6-118">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="98db6-118">Prerequisites</span></span>
<span data-ttu-id="98db6-119">Olay hub'ları receieving Azure Tanılama verileri bulut Hizmetleri, sanal makineleri, sanal makine ölçek kümeleri ve Service Fabric Azure SDK 2.9 ve karşılık gelen Azure Araçları Visual Studio için başlangıç desteklenir.</span><span class="sxs-lookup"><span data-stu-id="98db6-119">Event Hubs receieving data from Azure Diagnostics is supported in Cloud Services, VMs, Virtual Machine Scale Sets, and Service Fabric starting in the Azure SDK 2.9 and the corresponding Azure Tools for Visual Studio.</span></span>

* <span data-ttu-id="98db6-120">Azure tanılama uzantısını 1.6 ([veya daha sonra .NET 2.9 için Azure SDK](https://azure.microsoft.com/downloads/) bu varsayılan olarak hedefler)</span><span class="sxs-lookup"><span data-stu-id="98db6-120">Azure Diagnostics extension 1.6 ([Azure SDK for .NET 2.9 or later](https://azure.microsoft.com/downloads/) targets this by default)</span></span>
* [<span data-ttu-id="98db6-121">Visual Studio 2013 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="98db6-121">Visual Studio 2013 or later</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* <span data-ttu-id="98db6-122">Var olan Azure tanılama yapılandırmalarında kullanarak bir uygulama bir *.wadcfgx* dosya ve aşağıdaki yöntemlerden birini:</span><span class="sxs-lookup"><span data-stu-id="98db6-122">Existing configurations of Azure Diagnostics in an application by using a *.wadcfgx* file and one of the following methods:</span></span>
  * <span data-ttu-id="98db6-123">Visual Studio: [tanılama Azure bulut Hizmetleri ve sanal makineler için yapılandırma](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span><span class="sxs-lookup"><span data-stu-id="98db6-123">Visual Studio: [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md)</span></span>
  * <span data-ttu-id="98db6-124">Windows PowerShell: [PowerShell kullanarak Azure Cloud Services tanılamayı etkinleştirme](../cloud-services/cloud-services-diagnostics-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="98db6-124">Windows PowerShell: [Enable diagnostics in Azure Cloud Services using PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md)</span></span>
* <span data-ttu-id="98db6-125">Olay hub'ları ad alanı makale sağlanan [Event Hubs ile çalışmaya başlama](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="98db6-125">Event Hubs namespace provisioned per the article, [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

## <a name="connect-azure-diagnostics-to-event-hubs-sink"></a><span data-ttu-id="98db6-126">Azure Tanılama Olay hub'ları havuz Bağlan</span><span class="sxs-lookup"><span data-stu-id="98db6-126">Connect Azure Diagnostics to Event Hubs sink</span></span>
<span data-ttu-id="98db6-127">Varsayılan olarak, Azure tanılama her zaman günlüklerini ve ölçümleri bir Azure depolama hesabı gönderir.</span><span class="sxs-lookup"><span data-stu-id="98db6-127">By default, Azure Diagnostics always sends logs and metrics to an Azure Storage account.</span></span> <span data-ttu-id="98db6-128">Bir uygulama da verileri Event Hubs'a yeni ekleyerek gönderebilir **iç havuzlar** altında bölümünde **PublicConfig** / **WadCfg** öğesinin *. wadcfgx* dosya.</span><span class="sxs-lookup"><span data-stu-id="98db6-128">An application may also send data to Event Hubs by adding a new **Sinks** section under the **PublicConfig** / **WadCfg** element of the *.wadcfgx* file.</span></span> <span data-ttu-id="98db6-129">Visual Studio'da *.wadcfgx* dosya şu yolda depolanır: **bulut hizmeti projesini** > **rolleri** > **() RoleName)** > **diagnostics.wadcfgx** dosya.</span><span class="sxs-lookup"><span data-stu-id="98db6-129">In Visual Studio, the *.wadcfgx* file is stored in the following path: **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx** file.</span></span>

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

<span data-ttu-id="98db6-130">Bu örnekte olay hub'ın tam ad alanına olay hub'ı URL'si ayarlanır: olay hub'ları ad alanı + "/" + olay hub'ı adı.</span><span class="sxs-lookup"><span data-stu-id="98db6-130">In this example, the event hub URL is set to the fully qualified namespace of the event hub: Event Hubs namespace  + "/" + event hub name.</span></span>  

<span data-ttu-id="98db6-131">Olay hub'ı URL görüntülenir [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) olay hub'ları Panoda.</span><span class="sxs-lookup"><span data-stu-id="98db6-131">The event hub URL is displayed in the [Azure portal](http://go.microsoft.com/fwlink/?LinkID=213885) on the Event Hubs dashboard.</span></span>  

<span data-ttu-id="98db6-132">**Havuzu** adı aynı değeri tutarlı bir şekilde yapılandırma dosyası kullanılan sürece için geçerli bir dize ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="98db6-132">The **Sink** name can be set to any valid string as long as the same value is used consistently throughout the config file.</span></span>

> [!NOTE]
> <span data-ttu-id="98db6-133">Olabilir ek havuzlarını aşağıdaki gibi *Applicationınsights* Bu bölümde yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="98db6-133">There may be additional sinks, such as *applicationInsights* configured in this section.</span></span> <span data-ttu-id="98db6-134">Azure tanılama sağlayan her havuz olarak da bildirilirse tanımlanması bir veya daha fazla havuzlarını **PrivateConfig** bölümü.</span><span class="sxs-lookup"><span data-stu-id="98db6-134">Azure Diagnostics allows one or more sinks to be defined if each sink is also declared in the **PrivateConfig** section.</span></span>  
>
>

<span data-ttu-id="98db6-135">Olay hub'ları havuz gerekir de bildirilen ve içinde tanımlanan **PrivateConfig** bölümünü *.wadcfgx* yapılandırma dosyası.</span><span class="sxs-lookup"><span data-stu-id="98db6-135">The Event Hubs sink must also be declared and defined in the **PrivateConfig** section of the *.wadcfgx* config file.</span></span>

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

<span data-ttu-id="98db6-136">`SharedAccessKeyName` Değeri bir paylaşılan erişim imzası (SAS) anahtarı ve içinde tanımlanan ilke eşleşmelidir **olay hub'ları** ad alanı.</span><span class="sxs-lookup"><span data-stu-id="98db6-136">The `SharedAccessKeyName` value must match a Shared Access Signature (SAS) key and policy that has been defined in the **Event Hubs** namespace.</span></span> <span data-ttu-id="98db6-137">Olay hub'ları panoya göz atın [Azure portal](https://manage.windowsazure.com), tıklatın **Yapılandır** sekmesini tıklatın ve sahip bir adlandırılmış ilkeyi kurmak (örneğin, "SendRule") *Gönder* izinleri.</span><span class="sxs-lookup"><span data-stu-id="98db6-137">Browse to the Event Hubs dashboard in the [Azure portal](https://manage.windowsazure.com), click the **Configure** tab, and set up a named policy (for example, "SendRule") that has *Send* permissions.</span></span> <span data-ttu-id="98db6-138">**StorageAccount** içinde bildirilmiş **PrivateConfig**.</span><span class="sxs-lookup"><span data-stu-id="98db6-138">The **StorageAccount** is also declared in **PrivateConfig**.</span></span> <span data-ttu-id="98db6-139">Bunlar çalışıyorsanız burada değerlerini değiştirmek için gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="98db6-139">There is no need to change values here if they are working.</span></span> <span data-ttu-id="98db6-140">Bu örnekte, biz değerleri boş bir aşağı akış varlık değerleri ayarlayacaksınız oturum olduğu bırakın.</span><span class="sxs-lookup"><span data-stu-id="98db6-140">In this example, we leave the values empty, which is a sign that a downstream asset will set the values.</span></span> <span data-ttu-id="98db6-141">Örneğin, *ServiceConfiguration.Cloud.cscfg* ortam yapılandırma dosyası ayarlar ortam uygun adları ve anahtarları.</span><span class="sxs-lookup"><span data-stu-id="98db6-141">For example, the *ServiceConfiguration.Cloud.cscfg* environment configuration file sets the environment-appropriate names and keys.</span></span>  

> [!WARNING]
> <span data-ttu-id="98db6-142">Olay hub'ları SAS anahtarı düz metin halinde depolanır *.wadcfgx* dosya.</span><span class="sxs-lookup"><span data-stu-id="98db6-142">The Event Hubs SAS key is stored in plain text in the *.wadcfgx* file.</span></span> <span data-ttu-id="98db6-143">Genellikle, bu anahtarı kaynak kod denetimine iade veya uygun şekilde korumanız gerekir böylece yapı sunucunuz bir varlığı olarak kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="98db6-143">Often, this key is checked in to source code control or is available as an asset in your build server, so you should protect it as appropriate.</span></span> <span data-ttu-id="98db6-144">Bir SAS anahtarıyla burada kullanmanızı öneririz *yalnızca gönderme* izinleri böylece kötü niyetli bir kullanıcı event hub'ına yazma ancak kendisine dinleme veya yönetme.</span><span class="sxs-lookup"><span data-stu-id="98db6-144">We recommend that you use a SAS key here with *Send only* permissions so that a malicious user can write to the event hub, but not listen to it or manage it.</span></span>
>
>

## <a name="configure-azure-diagnostics-to-send-logs-and-metrics-to-event-hubs"></a><span data-ttu-id="98db6-145">Tanılama günlüklerini ve ölçümleri Event Hubs'a göndermek için Azure Yapılandır</span><span class="sxs-lookup"><span data-stu-id="98db6-145">Configure Azure Diagnostics to send logs and metrics to Event Hubs</span></span>
<span data-ttu-id="98db6-146">Tüm varsayılan ve özel tanılama veri daha önce açıklandığı gibi diğer bir deyişle, ölçümleri ve günlükleri, otomatik olarak gönderilir Azure Storage yapılandırılmış işlevdeki.</span><span class="sxs-lookup"><span data-stu-id="98db6-146">As discussed previously, all default and custom diagnostics data, that is, metrics and logs, is automatically sent to Azure Storage in the configured intervals.</span></span> <span data-ttu-id="98db6-147">Olay hub'ları ve ek bir havuz, olay hub'ına gönderildiği hiyerarşideki herhangi bir kök veya yaprak düğümü belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98db6-147">With Event Hubs and any additional sink, you can specify any root or leaf node in the hierarchy to be sent to the event hub.</span></span> <span data-ttu-id="98db6-148">Bu, ETW olayları, performans sayaçları, Windows olay günlüklerini ve uygulama günlükleri içerir.</span><span class="sxs-lookup"><span data-stu-id="98db6-148">This includes ETW events, performance counters, Windows event logs, and application logs.</span></span>   

<span data-ttu-id="98db6-149">Kaç tane veri noktaları gerçekte Event Hubs'a aktarılması gerektiğini dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="98db6-149">It is important to consider how many data points should actually be transferred to Event Hubs.</span></span> <span data-ttu-id="98db6-150">Genellikle, geliştiriciler tüketilen ve hızlı bir şekilde yorumlanır düşük gecikme süreli hot yolu veri aktarın.</span><span class="sxs-lookup"><span data-stu-id="98db6-150">Typically, developers transfer low-latency hot-path data that must be consumed and interpreted quickly.</span></span> <span data-ttu-id="98db6-151">Uyarıları veya otomatik ölçeklendirme kurallarını izleyen örnekler sistemleridir.</span><span class="sxs-lookup"><span data-stu-id="98db6-151">Systems that monitor alerts or autoscale rules are examples.</span></span> <span data-ttu-id="98db6-152">Bir geliştirici ayrıca bir alternatif analiz deposu yapılandırma veya deposu--Azure akış analizi, Elasticsearch, özel bir izleme sistemi veya diğer sık kullanılan bir izleme sistemi arama.</span><span class="sxs-lookup"><span data-stu-id="98db6-152">A developer might also configure an alternate analysis store or search store -- for example, Azure Stream Analytics, Elasticsearch, a custom monitoring system, or a favorite monitoring system from others.</span></span>

<span data-ttu-id="98db6-153">Bazı örnek yapılandırmalar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="98db6-153">The following are some example configurations.</span></span>

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

<span data-ttu-id="98db6-154">Yukarıdaki örnekte, havuz üst öğeye uygulanan **PerformanceCounters** düğümü hiyerarşideki tüm alt anlamına gelir **performans sayaçları** Event Hubs'a gönderilir.</span><span class="sxs-lookup"><span data-stu-id="98db6-154">In the above example, the sink is applied to the parent **PerformanceCounters** node in the hierarchy, which means all child **PerformanceCounters** will be sent to Event Hubs.</span></span>  

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

<span data-ttu-id="98db6-155">Önceki örnekte, yalnızca üç sayaç havuz uygulanır: **sıraya alınan istek sayısı**, **reddedilen istekleri**, ve **% işlemci zamanı**.</span><span class="sxs-lookup"><span data-stu-id="98db6-155">In the previous example, the sink is applied to only three counters: **Requests Queued**, **Requests Rejected**, and **% Processor time**.</span></span>  

<span data-ttu-id="98db6-156">Aşağıdaki örnek, bir geliştirici bu hizmetin sistem durumu için kullanılan önemli ölçümleri olması için gönderilen veri miktarını nasıl sınırlayabilirsiniz gösterir.</span><span class="sxs-lookup"><span data-stu-id="98db6-156">The following example shows how a developer can limit the amount of sent data to be the critical metrics that are used for this service’s health.</span></span>  

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

<span data-ttu-id="98db6-157">Bu örnekte, havuz için günlükleri uygulanır ve yalnızca hata düzeyi izleme filtrelenir.</span><span class="sxs-lookup"><span data-stu-id="98db6-157">In this example, the sink is applied to logs and is filtered only to error level trace.</span></span>

## <a name="deploy-and-update-a-cloud-services-application-and-diagnostics-config"></a><span data-ttu-id="98db6-158">Dağıtma ve bulut Hizmetleri uygulama ve tanılama config güncelleştir</span><span class="sxs-lookup"><span data-stu-id="98db6-158">Deploy and update a Cloud Services application and diagnostics config</span></span>
<span data-ttu-id="98db6-159">Visual Studio uygulama ve Event Hubs havuz yapılandırma dağıtmak için en kolay yolu sağlar.</span><span class="sxs-lookup"><span data-stu-id="98db6-159">Visual Studio provides the easiest path to deploy the application and Event Hubs sink configuration.</span></span> <span data-ttu-id="98db6-160">Görüntülemek ve dosyayı düzenlemek için açın *.wadcfgx* dosya Visual Studio'da, düzenlemek ve dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="98db6-160">To view and edit the file, open the *.wadcfgx* file in Visual Studio, edit it, and save it.</span></span> <span data-ttu-id="98db6-161">Yolun **bulut hizmeti projesini** > **rolleri** > **(RoleName)** > **diagnostics.wadcfgx**.</span><span class="sxs-lookup"><span data-stu-id="98db6-161">The path is **Cloud Service Project** > **Roles** > **(RoleName)** > **diagnostics.wadcfgx**.</span></span>  

<span data-ttu-id="98db6-162">Bu noktada, tüm dağıtım ve dağıtım eylemlerini Visual Studio, Visual Studio Team System ve tüm komutları veya MSBuild ve kullanım göre betikleri güncelleştirme **/t: yayımlama** hedef dahil *.wadcfgx* paketleme işleminde.</span><span class="sxs-lookup"><span data-stu-id="98db6-162">At this point, all deployment and deployment update actions in Visual Studio, Visual Studio Team System, and all commands or scripts that are based on MSBuild and use the **/t:publish** target include the *.wadcfgx* in the packaging process.</span></span> <span data-ttu-id="98db6-163">Ayrıca, dağıtımları ve güncelleştirmeleri dosyayı Azure Vm'leriniz uygun Azure Tanılama Aracı uzantısını kullanarak dağıtın.</span><span class="sxs-lookup"><span data-stu-id="98db6-163">In addition, deployments and updates deploy the file to Azure by using the appropriate Azure Diagnostics agent extension on your VMs.</span></span>

<span data-ttu-id="98db6-164">Uygulama ve Azure tanılama yapılandırması dağıttıktan sonra hemen panosunda olay hub'ın etkinliğini görür.</span><span class="sxs-lookup"><span data-stu-id="98db6-164">After you deploy the application and Azure Diagnostics configuration, you will immediately see activity in the dashboard of the event hub.</span></span> <span data-ttu-id="98db6-165">Bu hot yol verileri dinleyicisi istemci ya da analiz aracı tercih ettiğiniz görüntülemeye devam etmeye hazır olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="98db6-165">This indicates that you're ready to move on to viewing the hot-path data in the listener client or analysis tool of your choice.</span></span>  

<span data-ttu-id="98db6-166">Aşağıdaki resimde sağlıklı olay hub'ına süre 23'sonra Başlangıç tanılama verilerini göndermeye olay hub'ları Panosu gösterir.</span><span class="sxs-lookup"><span data-stu-id="98db6-166">In the following figure, the Event Hubs dashboard shows healthy sending of diagnostics data to the event hub starting sometime after 11 PM.</span></span> <span data-ttu-id="98db6-167">Ne zaman olan uygulama dağıtıldıktan güncelleştirilmiş ile *.wadcfgx* dosya ve havuz düzgün yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="98db6-167">That's when the application was deployed with an updated *.wadcfgx* file, and the sink was configured properly.</span></span>

![][0]  

> [!NOTE]
> <span data-ttu-id="98db6-168">Azure tanılama yapılandırma dosyasına (.wadcfgx) güncelleştirmeleri yaptığınızda, güncelleştirmeleri yapılandırmanın yanı sıra tüm uygulama için Visual Studio yayımlama veya bir Windows PowerShell komut dosyası kullanarak anında iletme olduğunu önerilir.</span><span class="sxs-lookup"><span data-stu-id="98db6-168">When you make updates to the Azure Diagnostics config file (.wadcfgx), it's recommended that you push the updates to the entire application as well as the configuration by using either Visual Studio publishing, or a Windows PowerShell script.</span></span>  
>
>

## <a name="view-hot-path-data"></a><span data-ttu-id="98db6-169">Hot yol verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="98db6-169">View hot-path data</span></span>
<span data-ttu-id="98db6-170">Daha önce anlatıldığı gibi dinleme ve olay hub'ları veri işleme için birçok kullanım örnekleri vardır.</span><span class="sxs-lookup"><span data-stu-id="98db6-170">As discussed previously, there are many use cases for listening to and processing Event Hubs data.</span></span>

<span data-ttu-id="98db6-171">Basit bir yaklaşım, olay hub'ına dinle ve çıkış akışı yazdırmak için küçük test konsol uygulaması oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="98db6-171">One simple approach is to create a small test console application to listen to the event hub and print the output stream.</span></span> <span data-ttu-id="98db6-172">Daha ayrıntılı olarak anlatılmıştır aşağıdaki kodu yerleştirebilirsiniz [Event Hubs ile çalışmaya başlama](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), bir konsol uygulamasında.</span><span class="sxs-lookup"><span data-stu-id="98db6-172">You can place the following code, which is explained in more detail in [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)), in a console application.</span></span>  

<span data-ttu-id="98db6-173">Konsol uygulaması içermelidir Not [olay işlemcisi konağı NuGet paketi](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span><span class="sxs-lookup"><span data-stu-id="98db6-173">Note that the console application must include the [Event Processor Host NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost/).</span></span>  

<span data-ttu-id="98db6-174">Açılı ayraç değerleri değiştirin unutmayın **ana** kaynaklarınız için değerlerle işlevi.</span><span class="sxs-lookup"><span data-stu-id="98db6-174">Remember to replace the values in angle brackets in the **Main** function with values for your resources.</span></span>   

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

            Console.WriteLine("Receiving. Press enter key to stop worker.");
            Console.ReadLine();
            eventProcessorHost.UnregisterEventProcessorAsync().Wait();
        }
    }
}
```

## <a name="troubleshoot-event-hubs-sinks"></a><span data-ttu-id="98db6-175">Olay hub'ları havuzlarını sorun giderme</span><span class="sxs-lookup"><span data-stu-id="98db6-175">Troubleshoot Event Hubs sinks</span></span>
* <span data-ttu-id="98db6-176">Olay hub'ı beklendiği gibi gelen veya giden olay etkinlik göstermez.</span><span class="sxs-lookup"><span data-stu-id="98db6-176">The event hub does not show incoming or outgoing event activity as expected.</span></span>

    <span data-ttu-id="98db6-177">Olay hub'ınızı başarıyla sağlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="98db6-177">Check that your event hub is successfully provisioned.</span></span> <span data-ttu-id="98db6-178">Tüm bağlantı bilgilerini **PrivateConfig** bölümünü *.wadcfgx* kaynağınız değerlerini portalında göründüğü gibi eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="98db6-178">All connection info in the **PrivateConfig** section of *.wadcfgx* must match the values of your resource as seen in the portal.</span></span> <span data-ttu-id="98db6-179">Tanımlanan bir SAS İlkesi (örnekte "SendRule") portal ve sahip olduğunuzdan emin olun *Gönder* izin verilir.</span><span class="sxs-lookup"><span data-stu-id="98db6-179">Make sure that you have a SAS policy defined ("SendRule" in the example) in the portal and that *Send* permission is granted.</span></span>  
* <span data-ttu-id="98db6-180">Bir güncelleştirme sonrası olay hub'ı artık gelen veya giden olay etkinliğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="98db6-180">After an update, the event hub no longer shows incoming or outgoing event activity.</span></span>

    <span data-ttu-id="98db6-181">İlk olarak, olay hub'ı ve yapılandırma bilgileri daha önce açıklandığı gibi doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="98db6-181">First, make sure that the event hub and configuration info is correct as explained previously.</span></span> <span data-ttu-id="98db6-182">Bazen **PrivateConfig** dağıtım güncelleştirmede sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="98db6-182">Sometimes the **PrivateConfig** is reset in a deployment update.</span></span> <span data-ttu-id="98db6-183">Tüm değişiklik yapmak için önerilen düzeltme olan *.wadcfgx* proje ve ardından itme tam uygulama güncelleştirmesi.</span><span class="sxs-lookup"><span data-stu-id="98db6-183">The recommended fix is to make all changes to *.wadcfgx* in the project and then push a complete application update.</span></span> <span data-ttu-id="98db6-184">Bu mümkün değilse, tanılama güncelleştirme tamamı iter emin olun **PrivateConfig** SAS anahtarını içerir.</span><span class="sxs-lookup"><span data-stu-id="98db6-184">If this is not possible, make sure that the diagnostics update pushes a complete **PrivateConfig** that includes the SAS key.</span></span>  
* <span data-ttu-id="98db6-185">Öneriler denedi ve olay hub'ı hala çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="98db6-185">I tried the suggestions, and the event hub is still not working.</span></span>

    <span data-ttu-id="98db6-186">Günlükleri ve hataları Azure tanılama için kendisini içeren Azure Storage tablo bakarak deneyin: **WADDiagnosticInfrastructureLogsTable**.</span><span class="sxs-lookup"><span data-stu-id="98db6-186">Try looking in the Azure Storage table that contains logs and errors for Azure Diagnostics itself: **WADDiagnosticInfrastructureLogsTable**.</span></span> <span data-ttu-id="98db6-187">Bir seçenektir bir aracı gibi kullanmayı [Azure Storage Gezgini](http://www.storageexplorer.com) bu depolama hesabına bağlanmak için bu tabloyu görüntülemek ve bir sorgu için zaman damgası son 24 saat içinde ekleyin.</span><span class="sxs-lookup"><span data-stu-id="98db6-187">One option is to use a tool such as [Azure Storage Explorer](http://www.storageexplorer.com) to connect to this storage account, view this table, and add a query for TimeStamp in the last 24 hours.</span></span> <span data-ttu-id="98db6-188">Microsoft Excel gibi bir uygulamada açma ve bir .csv dosyasına dışarı aktarma için aracını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98db6-188">You can use the tool to export a .csv file and open it in an application such as Microsoft Excel.</span></span> <span data-ttu-id="98db6-189">Excel gibi için arama kartı dizeleri, arama yapmayı kolaylaştırır **EventHubs**, hangi hata bildirdi görmek için.</span><span class="sxs-lookup"><span data-stu-id="98db6-189">Excel makes it easy to search for calling-card strings, such as **EventHubs**, to see what error is reported.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="98db6-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98db6-190">Next steps</span></span>
<span data-ttu-id="98db6-191">• [Event Hubs hakkında daha fazla bilgi edinin](https://azure.microsoft.com/services/event-hubs/)</span><span class="sxs-lookup"><span data-stu-id="98db6-191">•    [Learn more about Event Hubs](https://azure.microsoft.com/services/event-hubs/)</span></span>

## <a name="appendix-complete-azure-diagnostics-configuration-file-wadcfgx-example"></a><span data-ttu-id="98db6-192">Ek: Azure tanılama yapılandırma dosyası (.wadcfgx) örneği tamamlayın</span><span class="sxs-lookup"><span data-stu-id="98db6-192">Appendix: Complete Azure Diagnostics configuration file (.wadcfgx) example</span></span>
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

<span data-ttu-id="98db6-193">Tamamlayıcı *ServiceConfiguration.Cloud.cscfg* için bu örnek aşağıdaki gibi görünür.</span><span class="sxs-lookup"><span data-stu-id="98db6-193">The complementary *ServiceConfiguration.Cloud.cscfg* for this example looks like the following.</span></span>

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

<span data-ttu-id="98db6-194">Sanal makineler için eşdeğer tabanlı Json ayarlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="98db6-194">Equivalent Json based settings for virtual machines is as follows:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="98db6-195">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98db6-195">Next steps</span></span>
<span data-ttu-id="98db6-196">Aşağıdaki bağlantıları inceleyerek Event Hubs hakkında daha fazla bilgi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="98db6-196">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="98db6-197">Event Hubs’a genel bakış</span><span class="sxs-lookup"><span data-stu-id="98db6-197">Event Hubs overview</span></span>](../event-hubs/event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="98db6-198">Olay Hub’ı oluşturma</span><span class="sxs-lookup"><span data-stu-id="98db6-198">Create an event hub</span></span>](../event-hubs/event-hubs-create.md)
* [<span data-ttu-id="98db6-199">Event Hubs ile ilgili SSS</span><span class="sxs-lookup"><span data-stu-id="98db6-199">Event Hubs FAQ</span></span>](../event-hubs/event-hubs-faq.md)

<!-- Images. -->
[0]: ../event-hubs/media/event-hubs-streaming-azure-diags-data/dashboard.png
