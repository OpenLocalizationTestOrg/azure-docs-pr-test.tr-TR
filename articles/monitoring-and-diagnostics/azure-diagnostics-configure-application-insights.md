---
title: "Azure tanılama verilerini Application Insights'a göndermek için yapılandırma | Microsoft Docs"
description: "Application Insights'a veri göndermek için Azure tanılama ortak yapılandırmasını güncelleştirin."
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: 
ms.assetid: f9e12c3e-c307-435e-a149-ef0fef20513a
ms.service: monitoring-and-diagnostics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2016
ms.author: robb
ms.openlocfilehash: 67dc2d5bbfa2012e4e098616edda593d023c4c1e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-service-virtual-machine-or-service-fabric-diagnostic-data-to-application-insights"></a><span data-ttu-id="5ec7d-103">Bulut hizmeti, sanal makine ya da Service Fabric tanılama verilerini Application Insights'a gönderme</span><span class="sxs-lookup"><span data-stu-id="5ec7d-103">Send Cloud Service, Virtual Machine, or Service Fabric diagnostic data to Application Insights</span></span>
<span data-ttu-id="5ec7d-104">Bulut Hizmetleri, sanal makineler, sanal makine ölçek kümeleri ve Service Fabric tüm Azure tanılama uzantısını verileri toplamak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-104">Cloud services, Virtual Machines, Virtual Machine Scale Sets and Service Fabric all use the Azure Diagnostics extension to collect data.</span></span>  <span data-ttu-id="5ec7d-105">Azure Tanılama verileri Azure Storage tablolara gönderir.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-105">Azure diagnostics sends data to Azure Storage tables.</span></span>  <span data-ttu-id="5ec7d-106">Ancak, aynı zamanda tüm kanal veya bir Azure tanılama uzantısını 1.5 veya daha sonraki kullanarak başka konumlara veri alt kümesini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-106">However, you can also pipe all or a subset of the data to other locations using Azure Diagnostics extension 1.5 or later.</span></span>

<span data-ttu-id="5ec7d-107">Bu makalede, Application Insights'a Azure tanılama uzantısını verileri göndermeyi açıklar.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-107">This article describes how to send data from the Azure Diagnostics extension to Application Insights.</span></span>

## <a name="diagnostics-configuration-explained"></a><span data-ttu-id="5ec7d-108">Açıklanan tanılama yapılandırması</span><span class="sxs-lookup"><span data-stu-id="5ec7d-108">Diagnostics configuration explained</span></span>
<span data-ttu-id="5ec7d-109">Tanılama verileri nerede Gönder ek konumları olduğu sunulan Azure tanılama uzantısını 1.5 havuzlarını.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-109">The Azure diagnostics extension 1.5 introduced sinks, which are additional locations where you can send diagnostic data.</span></span>

<span data-ttu-id="5ec7d-110">Bir havuz örnek yapılandırma Application Insights için:</span><span class="sxs-lookup"><span data-stu-id="5ec7d-110">Example configuration of a sink for Application Insights:</span></span>

```XML
<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
</SinksConfig>
```
```JSON
"SinksConfig": {
    "Sink": [
        {
            "name": "ApplicationInsights",
            "ApplicationInsights": "{Insert InstrumentationKey}",
            "Channels": {
                "Channel": [
                    {
                        "logLevel": "Error",
                        "name": "MyTopDiagData"
                    },
                    {
                        "logLevel": "Error",
                        "name": "MyLogData"
                    }
                ]
            }
        }
    ]
}
```
- <span data-ttu-id="5ec7d-111">**Havuz** *adı* havuzu benzersiz olarak tanımlayan bir dize değeri bir özniteliktir.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-111">The **Sink** *name* attribute is a string value that uniquely identifies the sink.</span></span>

- <span data-ttu-id="5ec7d-112">**Applicationınsights** öğesi Azure Tanılama verileri nerede gönderilir uygulama Öngörüler kaynağın izleme anahtarını belirtir.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-112">The **ApplicationInsights** element specifies instrumentation key of the Application insights resource where the Azure diagnostics data is sent.</span></span>
    - <span data-ttu-id="5ec7d-113">Varolan bir Application Insights kaynağı sahip değilseniz, bkz: [yeni bir Application Insights kaynağı oluşturma](../application-insights/app-insights-create-new-resource.md) kaynak oluşturma ve izleme anahtarı alma hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-113">If you don't have an existing Application Insights resource, see [Create a new Application Insights resource](../application-insights/app-insights-create-new-resource.md) for more information on creating a resource and getting the instrumentation key.</span></span>
    - <span data-ttu-id="5ec7d-114">Bir bulut hizmeti Azure SDK 2.8 ve daha sonra geliştiriyorsanız, bu izleme anahtarını otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-114">If you are developing a Cloud Service with Azure SDK 2.8 and later, this instrumentation key is automatically populated.</span></span> <span data-ttu-id="5ec7d-115">Dayanarak değeri **appınsıghts_ınstrumentatıonkey** Cloud Service projesi paketleme, hizmet yapılandırma ayarı.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-115">The value is based on the **APPINSIGHTS_INSTRUMENTATIONKEY** service configuration setting when packaging the Cloud Service project.</span></span> <span data-ttu-id="5ec7d-116">Bkz: [kullanım Application Insights'a Azure bulut hizmeti sorunlarını gidermek için tanılama](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span><span class="sxs-lookup"><span data-stu-id="5ec7d-116">See [Use Application Insights with Azure Diagnostics to troubleshoot Cloud Service issues](../cloud-services/cloud-services-dotnet-diagnostics-applicationinsights.md).</span></span>

- <span data-ttu-id="5ec7d-117">**Kanalları** öğesi içeren bir veya daha fazla **kanal** öğeleri.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-117">The **Channels** element contains one or more **Channel** elements.</span></span>
    - <span data-ttu-id="5ec7d-118">*Adı* özniteliği benzersiz olarak bu kanala başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-118">The *name* attribute uniquely refers to that channel.</span></span>
    - <span data-ttu-id="5ec7d-119">*Loglevel* özniteliği kanal günlük düzeyini belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-119">The *loglevel* attribute lets you specify the log level that the channel allows.</span></span> <span data-ttu-id="5ec7d-120">En az bilgilere sırada kullanılabilir günlük düzeyleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5ec7d-120">The available log levels in order of most to least information are:</span></span>
        - <span data-ttu-id="5ec7d-121">Ayrıntılı</span><span class="sxs-lookup"><span data-stu-id="5ec7d-121">Verbose</span></span>
        - <span data-ttu-id="5ec7d-122">Bilgi</span><span class="sxs-lookup"><span data-stu-id="5ec7d-122">Information</span></span>
        - <span data-ttu-id="5ec7d-123">Uyarı</span><span class="sxs-lookup"><span data-stu-id="5ec7d-123">Warning</span></span>
        - <span data-ttu-id="5ec7d-124">Hata</span><span class="sxs-lookup"><span data-stu-id="5ec7d-124">Error</span></span>
        - <span data-ttu-id="5ec7d-125">Kritik</span><span class="sxs-lookup"><span data-stu-id="5ec7d-125">Critical</span></span>

<span data-ttu-id="5ec7d-126">Bir kanal bir filtre gibi davranır ve hedef havuz göndermek için belirli günlük düzeyleri seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-126">A channel acts like a filter and allows you to select specific log levels to send to the target sink.</span></span> <span data-ttu-id="5ec7d-127">Örneğin, ayrıntılı günlükleri toplamak ve depolama alanına göndermeden ancak havuz yalnızca hataları gönderme.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-127">For example, you could collect verbose logs and send them to storage, but send only Errors to the sink.</span></span>

<span data-ttu-id="5ec7d-128">Aşağıdaki grafikte, bu ilişkiyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-128">The following graphic shows this relationship.</span></span>

![Tanılama genel yapılandırması](./media/azure-diagnostics-configure-applicationinsights/AzDiag_Channels_App_Insights.png)

<span data-ttu-id="5ec7d-130">Aşağıdaki grafikte yapılandırma değerlerini ve nasıl çalıştığını özetler.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-130">The following graphic summarizes the configuration values and how they work.</span></span> <span data-ttu-id="5ec7d-131">Hiyerarşideki farklı düzeylerde yapılandırmasında birden çok havuzlarını içerebilir.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-131">You can include multiple sinks in the configuration at different levels in the hierarchy.</span></span> <span data-ttu-id="5ec7d-132">En üst düzeyinde havuz genel ayar olarak davranır ve tek tek öğede belirtilen bir genel Bu ayar için bir geçersiz kılma gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-132">The sink at the top level acts as a global setting and the one specified at the individual element acts like an override to that global setting.</span></span>

![Tanılama yapılandırması Application Insights ile iç havuzlar](./media/azure-diagnostics-configure-applicationinsights/Azure_Diagnostics_Sinks.png)

## <a name="complete-sink-configuration-example"></a><span data-ttu-id="5ec7d-134">Tam havuz yapılandırma örneği</span><span class="sxs-lookup"><span data-stu-id="5ec7d-134">Complete sink configuration example</span></span>
<span data-ttu-id="5ec7d-135">İşte genel yapılandırmasının tam bir örnek dosya</span><span class="sxs-lookup"><span data-stu-id="5ec7d-135">Here is a complete example of the public configuration file that</span></span>
1. <span data-ttu-id="5ec7d-136">tüm hataları Application Insights'a gönderir (belirtilen **DiagnosticMonitorConfiguration** düğüm)</span><span class="sxs-lookup"><span data-stu-id="5ec7d-136">sends all errors to Application Insights (specified at the **DiagnosticMonitorConfiguration** node)</span></span>
2. <span data-ttu-id="5ec7d-137">Ayrıca ayrıntılı düzeyi günlükleri için uygulama günlüklerine gönderir (belirtilen **günlükleri** düğüm).</span><span class="sxs-lookup"><span data-stu-id="5ec7d-137">also sends Verbose level logs for the Application Logs (specified at the **Logs** node).</span></span>

```XML
<WadCfg>
  <DiagnosticMonitorConfiguration overallQuotaInMB="4096"
       sinks="ApplicationInsights.MyTopDiagData"> <!-- All info below sent to this channel -->
    <DiagnosticInfrastructureLogs />
    <PerformanceCounters>
      <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
    </PerformanceCounters>
    <WindowsEventLog scheduledTransferPeriod="PT1M">
      <DataSource name="Application!*" />
    </WindowsEventLog>
    <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose"
            sinks="ApplicationInsights.MyLogData"/> <!-- This specific info sent to this channel -->
  </DiagnosticMonitorConfiguration>

<SinksConfig>
    <Sink name="ApplicationInsights">
      <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>
      <Channels>
        <Channel logLevel="Error" name="MyTopDiagData"  />
        <Channel logLevel="Verbose" name="MyLogData"  />
      </Channels>
    </Sink>
  </SinksConfig>
</WadCfg>
```
```JSON
"WadCfg": {
    "DiagnosticMonitorConfiguration": {
        "overallQuotaInMB": 4096,
        "sinks": "ApplicationInsights.MyTopDiagData", "_comment": "All info below sent to this channel",
        "DiagnosticInfrastructureLogs": {
        },
        "PerformanceCounters": {
            "PerformanceCounterConfiguration": [
                {
                    "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                    "sampleRate": "PT3M"
                },
                {
                    "counterSpecifier": "\\Memory\\Available MBytes",
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
            "scheduledTransferLogLevelFilter": "Verbose",
            "sinks": "ApplicationInsights.MyLogData", "_comment": "This specific info sent to this channel"
        }
    },
    "SinksConfig": {
        "Sink": [
            {
                "name": "ApplicationInsights",
                "ApplicationInsights": "{Insert InstrumentationKey}",
                "Channels": {
                    "Channel": [
                        {
                            "logLevel": "Error",
                            "name": "MyTopDiagData"
                        },
                        {
                            "logLevel": "Verbose",
                            "name": "MyLogData"
                        }
                    ]
                }
            }
        ]
    }
}
```
<span data-ttu-id="5ec7d-138">Önceki yapılandırmada, aşağıdaki satırları şu anlama gelir:</span><span class="sxs-lookup"><span data-stu-id="5ec7d-138">In the previous configuration, the following lines have the following meanings:</span></span>

### <a name="send-all-the-data-that-is-being-collected-by-azure-diagnostics"></a><span data-ttu-id="5ec7d-139">Azure tanılama tarafından toplanan tüm verileri gönder</span><span class="sxs-lookup"><span data-stu-id="5ec7d-139">Send all the data that is being collected by Azure diagnostics</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights",
}
```

### <a name="send-only-error-logs-to-the-application-insights-sink"></a><span data-ttu-id="5ec7d-140">Application Insights havuz yalnızca hata günlüklerini Gönder</span><span class="sxs-lookup"><span data-stu-id="5ec7d-140">Send only error logs to the Application Insights sink</span></span>

```XML
<DiagnosticMonitorConfiguration overallQuotaInMB="4096" sinks="ApplicationInsights.MyTopDiagdata">
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyTopDiagData",
}
```

### <a name="send-verbose-application-logs-to-application-insights"></a><span data-ttu-id="5ec7d-141">Ayrıntılı uygulama günlüklerini Application Insights'a gönderme</span><span class="sxs-lookup"><span data-stu-id="5ec7d-141">Send Verbose application logs to Application Insights</span></span>

```XML
<Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Verbose" sinks="ApplicationInsights.MyLogData"/>
```
```JSON
"DiagnosticMonitorConfiguration": {
    "overallQuotaInMB": 4096,
    "sinks": "ApplicationInsights.MyLogData",
}
```

## <a name="limitations"></a><span data-ttu-id="5ec7d-142">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="5ec7d-142">Limitations</span></span>

- <span data-ttu-id="5ec7d-143">**Kanallar yalnızca türü ve değil performans sayaçlarını günlüğe kaydeder.**</span><span class="sxs-lookup"><span data-stu-id="5ec7d-143">**Channels only log type and not performance counters.**</span></span> <span data-ttu-id="5ec7d-144">Bir performans sayacı öğesi ile bir kanal belirtirseniz, yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-144">If you specify a channel with a performance counter element, it is ignored.</span></span>
- <span data-ttu-id="5ec7d-145">**Günlük düzeyi için bir kanal tarafından Azure tanılama toplanmakta için günlük düzeyi aşamaz.**</span><span class="sxs-lookup"><span data-stu-id="5ec7d-145">**The log level for a channel cannot exceed the log level for what is being collected by Azure diagnostics.**</span></span> <span data-ttu-id="5ec7d-146">Örneğin, olamaz toplama günlükleri öğesindeki uygulama günlüğü hataları ve ayrıntılı göndermeye uygulama Insight havuz günlükleri.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-146">For example, you cannot collect Application Log errors in the Logs element and try to send Verbose logs to the Application Insight sink.</span></span> <span data-ttu-id="5ec7d-147">*ScheduledTransferLogLevelFilter* özniteliği gerekir her zaman toplamak eşit veya günlükleri'den daha fazla günlükleri göndermek için bir havuz çalışıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-147">The *scheduledTransferLogLevelFilter* attribute must always collect equal or more logs than the logs you are trying to send to a sink.</span></span>
- <span data-ttu-id="5ec7d-148">**Blob verilerini Application Insights'a Azure tanılama uzantısını tarafından toplanan gönderemez.**</span><span class="sxs-lookup"><span data-stu-id="5ec7d-148">**You cannot send blob data collected by Azure diagnostics extension to Application Insights.**</span></span> <span data-ttu-id="5ec7d-149">Örneğin, altında belirtilen hiçbir şey *dizinleri* düğümü.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-149">For example, anything specified under the *Directories* node.</span></span> <span data-ttu-id="5ec7d-150">Kilitlenme dökümleri için gerçek kilitlenme döküm BLOB depolamaya gönderilir ve Application Insights'a yalnızca kilitlenme döküm oluşturulan bir bildirim gönderilir.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-150">For Crash Dumps the actual crash dump is sent to blob storage and only a notification that the crash dump was generated is sent to Application Insights.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ec7d-151">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="5ec7d-151">Next Steps</span></span>
* <span data-ttu-id="5ec7d-152">Bilgi edinmek için nasıl [Azure tanılama bilgilerinizi görüntülemek](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) Application ınsights'ta.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-152">Learn how to [view your Azure diagnostics information](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-cloudservices#view-azure-diagnostic-events) in Application Insights.</span></span>
* <span data-ttu-id="5ec7d-153">Kullanım [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) uygulamanız için Azure tanılama uzantısını etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="5ec7d-153">Use [PowerShell](../cloud-services/cloud-services-diagnostics-powershell.md) to enable the Azure diagnostics extension for your application.</span></span>
* <span data-ttu-id="5ec7d-154">Kullanım [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) uygulamanız için Azure tanılama uzantısını etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="5ec7d-154">Use [Visual Studio](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) to enable the Azure diagnostics extension for your application</span></span>
