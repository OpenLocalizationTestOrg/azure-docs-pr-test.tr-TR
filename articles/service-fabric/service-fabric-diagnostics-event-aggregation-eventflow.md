---
title: Service Fabric olay toplama EventFlow aaaAzure | Microsoft Docs
description: "Toplama ve izleme ve tanılama Azure Service Fabric kümeleri için EventFlow kullanarak olay toplama hakkında bilgi edinin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: c0141d3ed72d835139250af3589e298fd22d8f89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="fc03a-103">Olay toplama ve EventFlow kullanarak koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="fc03a-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="fc03a-104">[Microsoft tanılama EventFlow](https://github.com/Azure/diagnostics-eventflow) düğümü tooone ya da daha fazla izleme hedefleri olaylarından yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="fc03a-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node tooone or more monitoring destinations.</span></span> <span data-ttu-id="fc03a-105">Hizmet projenizdeki NuGet paketi olarak dahil olduğundan Azure Tanılama hakkında daha önce bahsedilen hello düğüm başına yapılandırma sorunu ortadan hello hizmetiyle EventFlow kod ve yapılandırma ilerler.</span><span class="sxs-lookup"><span data-stu-id="fc03a-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with hello service, eliminating hello per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="fc03a-106">EventFlow hizmet işlemi içinde çalıştırılan ve yapılandırılmış toohello çıkışları doğrudan bağlanır.</span><span class="sxs-lookup"><span data-stu-id="fc03a-106">EventFlow runs within your service process, and connects directly toohello configured outputs.</span></span> <span data-ttu-id="fc03a-107">Merhaba doğrudan bağlantı nedeniyle EventFlow Azure, kapsayıcı ve şirket içi hizmet dağıtımları için çalışır.</span><span class="sxs-lookup"><span data-stu-id="fc03a-107">Because of hello direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="fc03a-108">Her EventFlow ardışık düzen bir dış bağlantısı yaptığından EventFlow yüksek yoğunluklu senaryolarda gibi bir kapsayıcıda çalıştırırsanız dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="fc03a-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="fc03a-109">Bu nedenle, çeşitli işlemleri barındırıyorsanız, birkaç giden bağlantılar alın!</span><span class="sxs-lookup"><span data-stu-id="fc03a-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="fc03a-110">Bu Service Fabric uygulamaları için kadar bir sorun olduğundan değil tüm çoğaltmaları bir `ServiceType` çalıştırın hello aynı işlemi ve bu giden bağlantılar hello sayısını sınırlar.</span><span class="sxs-lookup"><span data-stu-id="fc03a-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in hello same process, and this limits hello number of outbound connections.</span></span> <span data-ttu-id="fc03a-111">Böylece hello belirtilen filtreyle eşleşen hello olayları gönderilir EventFlow ayrıca olay filtreleme, sunar.</span><span class="sxs-lookup"><span data-stu-id="fc03a-111">EventFlow also offers event filtering, so that only hello events that match hello specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="fc03a-112">EventFlow ayarlama</span><span class="sxs-lookup"><span data-stu-id="fc03a-112">Setting up EventFlow</span></span>

<span data-ttu-id="fc03a-113">EventFlow ikili dosyaları NuGet paketlerini bir dizi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fc03a-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="fc03a-114">tooadd EventFlow tooa Service Fabric hizmeti projesi, hello Çözüm Gezgini hello projeye sağ tıklayın ve "Manage NuGet paketlerini."'i seçin</span><span class="sxs-lookup"><span data-stu-id="fc03a-114">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="fc03a-115">Toohello "Gözat" sekmesini ve aramak için anahtar "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="fc03a-115">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Visual Studio NuGet Paket Yöneticisi kullanıcı Arabirimi EventFlow NuGet paketleri](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="fc03a-117">Çeşitli paketler, "Girdi" ve "Çıkaran" etiketli gösteri listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="fc03a-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="fc03a-118">EventFlow çeşitli farklı günlüğü sağlayıcıları ve çözümleyiciler destekler.</span><span class="sxs-lookup"><span data-stu-id="fc03a-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="fc03a-119">hello service EventFlow barındırma hello kaynak ve hedef hello uygulama günlükleri için bağlı olarak uygun paketleri içermelidir.</span><span class="sxs-lookup"><span data-stu-id="fc03a-119">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="fc03a-120">Ayrıca toohello çekirdek ServiceFabric paketi, ayrıca en az bir giriş ve çıkış yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fc03a-120">In addition toohello core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="fc03a-121">Exmaple için paketler toosent EventSource olaylarını tooApplication Öngörüler aşağıdaki hello ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fc03a-121">For exmaple, you can add hello following packages toosent EventSource events tooApplication Insights:</span></span>

* <span data-ttu-id="fc03a-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture veri hello hizmetin EventSource sınıfı ve gibi standart EventSources *Microsoft ServiceFabric Hizmetleri* ve *Microsoft ServiceFabric aktörler*)</span><span class="sxs-lookup"><span data-stu-id="fc03a-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="fc03a-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(biz toosend hello günlükleri tooan Azure Application Insights kaynağı kalacaklarını)</span><span class="sxs-lookup"><span data-stu-id="fc03a-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going toosend hello logs tooan Azure Application Insights resource)</span></span>
* <span data-ttu-id="fc03a-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(Merhaba EventFlow ardışık Service Fabric hizmet yapılandırmasından başlatma sağlar ve Service Fabric sistem durumu raporlarının Tanılama verileri gönderme ile herhangi bir sorun raporları)</span><span class="sxs-lookup"><span data-stu-id="fc03a-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="fc03a-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource`Paket hello hizmet projesi tootarget .NET Framework 4.6 gerektiren ya da daha yeni.</span><span class="sxs-lookup"><span data-stu-id="fc03a-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="fc03a-126">Bu paketi yüklemeden önce Proje Özellikleri'nde hello uygun hedef framework ayarladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fc03a-126">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="fc03a-127">Tüm hello paketleri yüklendi, hello sonraki adımı tooconfigure ve EventFlow hello hizmeti etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="fc03a-127">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="fc03a-128">Yapılandırma ve günlük toplama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="fc03a-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="fc03a-129">Merhaba EventFlow ardışık düzen hello günlükleri göndermek için sorumlu bir yapılandırma dosyasında depolanan belirtiminden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fc03a-129">hello EventFlow pipeline responsible for sending hello logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="fc03a-130">Merhaba `Microsoft.Diagnostics.EventFlow.ServiceFabric` paketi yükler altında başlangıç EventFlow yapılandırma dosyası `PackageRoot\Config` adlı Çözüm klasörü `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="fc03a-130">hello `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="fc03a-131">Bu yapılandırma dosyasını değiştirdi toobe toocapture verilerinin hello varsayılan hizmetinden gerekir. `EventSource` sınıfı ve tooconfigure istediğiniz ve veri toohello uygun yere gönderme tüm diğer girişler.</span><span class="sxs-lookup"><span data-stu-id="fc03a-131">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class, and any other inputs you want tooconfigure, and send data toohello appropriate place.</span></span>

<span data-ttu-id="fc03a-132">Örnek bir işte *eventFlowConfig.json* yukarıda belirtilen hello NuGet paketlerini göre:</span><span class="sxs-lookup"><span data-stu-id="fc03a-132">Here is a sample *eventFlowConfig.json* based on hello NuGet packages mentioned above:</span></span>
```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace hello following value with your service's ServiceEventSource name)
        { "providerName": "your-service-EventSource-name" }
      ]
    }
  ],
  "filters": [
    {
      "type": "drop",
      "include": "Level == Verbose"
    }
  ],
  "outputs": [
    {
      "type": "ApplicationInsights",
      // (replace hello following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

<span data-ttu-id="fc03a-133">Merhaba hizmetin ServiceEventSource adıdır hello hello adını hello değerini `EventSourceAttribute` toohello ServiceEventSource sınıfı uygulanır.</span><span class="sxs-lookup"><span data-stu-id="fc03a-133">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="fc03a-134">Tüm hello belirtildiği `ServiceEventSource.cs` hello hizmet kod parçası olan dosya.</span><span class="sxs-lookup"><span data-stu-id="fc03a-134">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="fc03a-135">Örneğin, hello aşağıdaki kod parçacığını hello hello ServiceEventSource adıdır *Şirketim Application1 Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="fc03a-135">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="fc03a-136">Unutmayın `eventFlowConfig.json` dosya hizmeti yapılandırma paketi bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="fc03a-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="fc03a-137">Tam veya yapılandırma-yalnızca hello hizmetinin yükseltmeleri değişiklikleri toothis dosya eklenebilir, konu tooService doku yükseltin sistem durumu denetimlerinin ve Otomatik geri alma yükseltme hatası ise.</span><span class="sxs-lookup"><span data-stu-id="fc03a-137">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="fc03a-138">Daha fazla bilgi için bkz: [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="fc03a-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="fc03a-139">Merhaba *filtreleri* hello yapılandırma bölümünü toofurther verir hello değiştirmek toodrop izin vererek hello EventFlow ardışık düzen toohello çıkışlarını üzerinden giderek toogo hello bilgileri özelleştirin veya belirli bilgiler içerir Merhaba olay veri yapısı.</span><span class="sxs-lookup"><span data-stu-id="fc03a-139">hello *filters* section of hello config allows you toofurther customize hello information that is going toogo through hello EventFlow pipeline toohello outputs, allowing you toodrop or include certain information, or change hello structure of hello event data.</span></span> <span data-ttu-id="fc03a-140">Filtreleri hakkında daha fazla bilgi için bkz: [EventFlow filtreleri](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="fc03a-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="fc03a-141">Merhaba son adımdır tooinstantiate EventFlow ardışık Hizmetinizin başlangıç kod içinde bulunan, `Program.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="fc03a-141">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric;
using Microsoft.ServiceFabric.Services.Runtime;

// **** EventFlow namespace
using Microsoft.Diagnostics.EventFlow.ServiceFabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>
        private static void Main()
        {
            try
            {
                // **** Instantiate log collection via EventFlow
                using (var diagnosticsPipeline = ServiceFabricDiagnosticPipelineFactory.CreatePipeline("MyApplication-MyService-DiagnosticsPipeline"))
                {

                    ServiceRuntime.RegisterServiceAsync("Stateless1Type",
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                    ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                    Thread.Sleep(Timeout.Infinite);
                }
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
                throw;
            }
        }
    }
}
```

<span data-ttu-id="fc03a-142">Merhaba adı hello hello parametre olarak geçirilen `CreatePipeline` hello yöntemi `ServiceFabricDiagnosticsPipelineFactory` hello hello adıdır *sistem durumu varlık* hello EventFlow günlük toplama ardışık temsil eden.</span><span class="sxs-lookup"><span data-stu-id="fc03a-142">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="fc03a-143">Bu ad EventFlow karşılaşırsa kullanılır ve hata ve Service Fabric sistem durumu alt hello bildirir.</span><span class="sxs-lookup"><span data-stu-id="fc03a-143">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a><span data-ttu-id="fc03a-144">Service Fabric ayarları ve uygulama parametreleri tooin eventFlowConfig kullanma</span><span class="sxs-lookup"><span data-stu-id="fc03a-144">Using Service Fabric settings and application parameters tooin eventFlowConfig</span></span>

<span data-ttu-id="fc03a-145">Service Fabric ve uygulama parametreler tooconfigure EventFlow ayarlarını EventFlow kullanılmasını destekler.</span><span class="sxs-lookup"><span data-stu-id="fc03a-145">EventFlow supports using Service Fabric settings and application paremeters tooconfigure EventFlow settings.</span></span> <span data-ttu-id="fc03a-146">Bu özel bir sözdizimi için değerleri kullanarak tooService yapı ayarları parametrelerini başvurabilir:</span><span class="sxs-lookup"><span data-stu-id="fc03a-146">You can refer tooService Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="fc03a-147">`<section-name>`Merhaba Service Fabric yapılandırma bölümü Hello adıdır ve `<setting-name>` hello yapılandırma ayarı EventFlow ayarı kullanılan tooconfigure hello değer sağlama.</span><span class="sxs-lookup"><span data-stu-id="fc03a-147">`<section-name>` is hello name of hello Service Fabric configuration section, and `<setting-name>` is hello configuration setting providing hello value that will be used tooconfigure an EventFlow setting.</span></span> <span data-ttu-id="fc03a-148">tooread nasıl hakkında daha fazla toodo Bu, Git çok[Service Fabric ayarları ve uygulama parametreleri desteği](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="fc03a-148">tooread more about how toodo this, go too[Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="fc03a-149">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="fc03a-149">Verification</span></span>

<span data-ttu-id="fc03a-150">Hizmetinizi başlatın ve hata ayıklama hello uyun Visual Studio çıktı penceresinde.</span><span class="sxs-lookup"><span data-stu-id="fc03a-150">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="fc03a-151">Merhaba hizmeti başlatıldıktan sonra yapılandırdığınız toohello çıkış hizmetinizi gönderme bulgu kayıtları görmeye başlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fc03a-151">After hello service is started, you should start seeing evidence that your service is sending records toohello output that you have configured.</span></span> <span data-ttu-id="fc03a-152">Tooyour olay çözümleme ve görselleştirme platform gidin ve günlükleri tooshow başlatılmış olduğunu onaylayın Yukarı (birkaç dakika sürebilir).</span><span class="sxs-lookup"><span data-stu-id="fc03a-152">Navigate tooyour event analysis and visualization platform and confirm that logs have started tooshow up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc03a-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc03a-153">Next steps</span></span>

* [<span data-ttu-id="fc03a-154">Olay çözümleme ve görselleştirme Application Insights ile</span><span class="sxs-lookup"><span data-stu-id="fc03a-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="fc03a-155">Olay çözümleme ve OMS Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="fc03a-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="fc03a-156">EventFlow belgeleri</span><span class="sxs-lookup"><span data-stu-id="fc03a-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)