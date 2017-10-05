---
title: Azure Service Fabric olay toplama EventFlow | Microsoft Docs
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
ms.openlocfilehash: 90d26a77b749e70de3a7d910f15820653e2ef39b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="event-aggregation-and-collection-using-eventflow"></a><span data-ttu-id="09a5e-103">Olay toplama ve EventFlow kullanarak koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="09a5e-103">Event aggregation and collection using EventFlow</span></span>

<span data-ttu-id="09a5e-104">[Microsoft tanılama EventFlow](https://github.com/Azure/diagnostics-eventflow) olayları bir düğümden bir veya daha fazla izleme hedeflere yönlendirebilir.</span><span class="sxs-lookup"><span data-stu-id="09a5e-104">[Microsoft Diagnostics EventFlow](https://github.com/Azure/diagnostics-eventflow) can route events from a node to one or more monitoring destinations.</span></span> <span data-ttu-id="09a5e-105">Hizmet projenizdeki NuGet paketi olarak dahil olduğundan EventFlow kod ve yapılandırma hizmetiyle Azure Tanılama hakkında daha önce bahsedilen düğüm başına yapılandırma sorunu ortadan ilerler.</span><span class="sxs-lookup"><span data-stu-id="09a5e-105">Because it is included as a NuGet package in your service project, EventFlow code and configuration travel with the service, eliminating the per-node configuration issue mentioned earlier about Azure Diagnostics.</span></span> <span data-ttu-id="09a5e-106">EventFlow hizmet işlemi içinde çalıştırılan ve yapılandırılmış çıktıları doğrudan bağlanır.</span><span class="sxs-lookup"><span data-stu-id="09a5e-106">EventFlow runs within your service process, and connects directly to the configured outputs.</span></span> <span data-ttu-id="09a5e-107">Doğrudan bağlantı nedeniyle EventFlow Azure, kapsayıcı ve şirket içi hizmet dağıtımları için çalışır.</span><span class="sxs-lookup"><span data-stu-id="09a5e-107">Because of the direct connection, EventFlow works for Azure, container, and on-premises service deployments.</span></span> <span data-ttu-id="09a5e-108">Her EventFlow ardışık düzen bir dış bağlantısı yaptığından EventFlow yüksek yoğunluklu senaryolarda gibi bir kapsayıcıda çalıştırırsanız dikkatli olun.</span><span class="sxs-lookup"><span data-stu-id="09a5e-108">Be careful if you run EventFlow in high-density scenarios, such as in a container, because each EventFlow pipeline makes an external connection.</span></span> <span data-ttu-id="09a5e-109">Bu nedenle, çeşitli işlemleri barındırıyorsanız, birkaç giden bağlantılar alın!</span><span class="sxs-lookup"><span data-stu-id="09a5e-109">So, if you host several processes, you get several outbound connections!</span></span> <span data-ttu-id="09a5e-110">Bu Service Fabric uygulamaları için kadar bir sorun olduğundan değil tüm çoğaltmaları bir `ServiceType` aynı işlem içinde çalıştırın ve bu giden bağlantı sayısını sınırlar.</span><span class="sxs-lookup"><span data-stu-id="09a5e-110">This isn't as much a concern for Service Fabric applications, because all replicas of a `ServiceType` run in the same process, and this limits the number of outbound connections.</span></span> <span data-ttu-id="09a5e-111">Böylece yalnızca belirtilen filtreyle eşleşen olaylar gönderilen olay filtreleme, EventFlow de sunar.</span><span class="sxs-lookup"><span data-stu-id="09a5e-111">EventFlow also offers event filtering, so that only the events that match the specified filter are sent.</span></span>

## <a name="setting-up-eventflow"></a><span data-ttu-id="09a5e-112">EventFlow ayarlama</span><span class="sxs-lookup"><span data-stu-id="09a5e-112">Setting up EventFlow</span></span>

<span data-ttu-id="09a5e-113">EventFlow ikili dosyaları NuGet paketlerini bir dizi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="09a5e-113">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="09a5e-114">Bir Service Fabric hizmeti projesine EventFlow eklemek, Çözüm Gezgini'nde projeye sağ tıklayın ve "Manage NuGet paketlerini."</span><span class="sxs-lookup"><span data-stu-id="09a5e-114">To add EventFlow to a Service Fabric service project, right-click the project in the Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="09a5e-115">Arayın ve geçiş için "Gözat" sekmesinde "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="09a5e-115">Switch to the "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Visual Studio NuGet Paket Yöneticisi kullanıcı Arabirimi EventFlow NuGet paketleri](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

<span data-ttu-id="09a5e-117">Çeşitli paketler, "Girdi" ve "Çıkaran" etiketli gösteri listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="09a5e-117">You will see a list of various packages show up, labeled with "Inputs" and "Outputs".</span></span> <span data-ttu-id="09a5e-118">EventFlow çeşitli farklı günlüğü sağlayıcıları ve çözümleyiciler destekler.</span><span class="sxs-lookup"><span data-stu-id="09a5e-118">EventFlow supports various different logging providers and analyzers.</span></span> <span data-ttu-id="09a5e-119">EventFlow barındırma hizmeti için kaynak ve hedef uygulama günlüklerini bağlı olarak uygun paketleri içermelidir.</span><span class="sxs-lookup"><span data-stu-id="09a5e-119">The service hosting EventFlow should include appropriate packages depending on the source and destination for the application logs.</span></span> <span data-ttu-id="09a5e-120">Çekirdek ServiceFabric paketi yanı sıra da en az bir giriş gerekir ve çıktı yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="09a5e-120">In addition to the core ServiceFabric package, you also need at least one Input and Output configured.</span></span> <span data-ttu-id="09a5e-121">Exmaple için Application Insights gönderilen EventSource olaylarını aşağıdaki paketler ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09a5e-121">For exmaple, you can add the following packages to sent EventSource events to Application Insights:</span></span>

* <span data-ttu-id="09a5e-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource`verileri hizmetin EventSource sınıfı ve standart EventSources gibi yakalamak için *Microsoft ServiceFabric Hizmetleri* ve *Microsoft ServiceFabric aktörler*)</span><span class="sxs-lookup"><span data-stu-id="09a5e-122">`Microsoft.Diagnostics.EventFlow.Input.EventSource` to capture data from the service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* <span data-ttu-id="09a5e-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(biz günlükleri için Azure Application Insights kaynağı göndereceğiniz)</span><span class="sxs-lookup"><span data-stu-id="09a5e-123">`Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights` (we are going to send the logs to an Azure Application Insights resource)</span></span>
* <span data-ttu-id="09a5e-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(Service Fabric hizmet yapılandırmasını EventFlow ardışık düzen başlatma sağlar ve Service Fabric sistem durumu raporlarının Tanılama verileri gönderme ile herhangi bir sorun raporları)</span><span class="sxs-lookup"><span data-stu-id="09a5e-124">`Microsoft.Diagnostics.EventFlow.ServiceFabric`(enables initialization of the EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

>[!NOTE]
><span data-ttu-id="09a5e-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource`Paketi, .NET Framework 4.6 veya daha yeni hedeflemek için hizmet projesi gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="09a5e-125">`Microsoft.Diagnostics.EventFlow.Input.EventSource` package requires the service project to target .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="09a5e-126">Bu paketi yüklemeden önce Proje Özellikleri'nde uygun hedef Framework'ü ayarladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="09a5e-126">Make sure you set the appropriate target framework in project properties before installing this package.</span></span>

<span data-ttu-id="09a5e-127">Tüm paketler yüklendikten sonra sıradaki adım yapılandırın ve hizmeti EventFlow etkinleştirin olacak.</span><span class="sxs-lookup"><span data-stu-id="09a5e-127">After all the packages are installed, the next step is to configure and enable EventFlow in the service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="09a5e-128">Yapılandırma ve günlük toplama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="09a5e-128">Configuring and enabling log collection</span></span>
<span data-ttu-id="09a5e-129">Günlükleri göndermek için sorumlu EventFlow ardışık düzen yapılandırma dosyasında depolanan belirtiminden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="09a5e-129">The EventFlow pipeline responsible for sending the logs is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="09a5e-130">`Microsoft.Diagnostics.EventFlow.ServiceFabric` Paketi yükler altında başlangıç EventFlow yapılandırma dosyası `PackageRoot\Config` adlı Çözüm klasörü `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="09a5e-130">The `Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder, named `eventFlowConfig.json`.</span></span> <span data-ttu-id="09a5e-131">Bu yapılandırma dosyası varsayılan hizmet verilerini yakalamak için değiştirilmesi gereken `EventSource` sınıfı ve yapılandırmak ve uygun bir konuma veri göndermek istediğiniz girdi.</span><span class="sxs-lookup"><span data-stu-id="09a5e-131">This configuration file needs to be modified to capture data from the default service `EventSource` class, and any other inputs you want to configure, and send data to the appropriate place.</span></span>

<span data-ttu-id="09a5e-132">Örnek bir işte *eventFlowConfig.json* yukarıda belirtilen NuGet paketlerini göre:</span><span class="sxs-lookup"><span data-stu-id="09a5e-132">Here is a sample *eventFlowConfig.json* based on the NuGet packages mentioned above:</span></span>
```json
{
  "inputs": [
    {
      "type": "EventSource",
      "sources": [
        { "providerName": "Microsoft-ServiceFabric-Services" },
        { "providerName": "Microsoft-ServiceFabric-Actors" },
        // (replace the following value with your service's ServiceEventSource name)
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
      // (replace the following value with your AI resource's instrumentation key)
      "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
  ],
  "schemaVersion": "2016-08-11"
}
```

<span data-ttu-id="09a5e-133">Hizmetin ServiceEventSource adını adı özniteliğinin değeri `EventSourceAttribute` ServiceEventSource sınıfına uygulanan.</span><span class="sxs-lookup"><span data-stu-id="09a5e-133">The name of service's ServiceEventSource is the value of the Name property of the `EventSourceAttribute` applied to the ServiceEventSource class.</span></span> <span data-ttu-id="09a5e-134">Bunu tüm belirtilen `ServiceEventSource.cs` hizmet kod parçası olan dosya.</span><span class="sxs-lookup"><span data-stu-id="09a5e-134">It is all specified in the `ServiceEventSource.cs` file, which is part of the service code.</span></span> <span data-ttu-id="09a5e-135">Örneğin, aşağıdaki kod parçacığında ServiceEventSource adıdır *Şirketim Application1 Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="09a5e-135">For example, in the following code snippet the name of the ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

<span data-ttu-id="09a5e-136">Unutmayın `eventFlowConfig.json` dosya hizmeti yapılandırma paketi bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="09a5e-136">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="09a5e-137">Bu dosyadaki değişiklikler tam veya yapılandırma-salt yükseltmeler Service Fabric yükseltme sistem durumu denetimlerinin ve yükseltme hatası olursa otomatik geri alma tabi hizmetinin eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="09a5e-137">Changes to this file can be included in full- or configuration-only upgrades of the service, subject to Service Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="09a5e-138">Daha fazla bilgi için bkz: [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="09a5e-138">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="09a5e-139">*Filtreleri* yapılandırma bölümünde daha fazla EventFlow ardışık düzen üzerinden bırakma veya belirli bilgileri dahil izin veren çıktıları giderek bilgileri özelleştirin veya olay verilerinin yapısını değiştirme olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="09a5e-139">The *filters* section of the config allows you to further customize the information that is going to go through the EventFlow pipeline to the outputs, allowing you to drop or include certain information, or change the structure of the event data.</span></span> <span data-ttu-id="09a5e-140">Filtreleri hakkında daha fazla bilgi için bkz: [EventFlow filtreleri](https://github.com/Azure/diagnostics-eventflow#filters).</span><span class="sxs-lookup"><span data-stu-id="09a5e-140">For more information on filtering, see [EventFlow filters](https://github.com/Azure/diagnostics-eventflow#filters).</span></span>

<span data-ttu-id="09a5e-141">EventFlow ardışık düzeninde bulunan Hizmetinizin başlangıç kodu örneği oluşturmak için son adımdır `Program.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="09a5e-141">The final step is to instantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file:</span></span>

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
        /// This is the entry point of the service host process.
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

<span data-ttu-id="09a5e-142">Name parametresi olarak geçirilen `CreatePipeline` yöntemi `ServiceFabricDiagnosticsPipelineFactory` adı *sistem durumu varlık* EventFlow günlük toplama ardışık temsil eden.</span><span class="sxs-lookup"><span data-stu-id="09a5e-142">The name passed as the parameter of the `CreatePipeline` method of the `ServiceFabricDiagnosticsPipelineFactory` is the name of the *health entity* representing the EventFlow log collection pipeline.</span></span> <span data-ttu-id="09a5e-143">Bu ad EventFlow karşılaşırsa kullanılır ve hata ve Service Fabric sistem durumu alt raporlar.</span><span class="sxs-lookup"><span data-stu-id="09a5e-143">This name is used if EventFlow encounters and error and reports it through the Service Fabric health subsystem.</span></span>

### <a name="using-service-fabric-settings-and-application-parameters-to-in-eventflowconfig"></a><span data-ttu-id="09a5e-144">Service Fabric ayarları ve uygulama parametreleri eventFlowConfig içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="09a5e-144">Using Service Fabric settings and application parameters to in eventFlowConfig</span></span>

<span data-ttu-id="09a5e-145">EventFlow EventFlow ayarlarını yapılandırmak için Service Fabric ayarları ve uygulama parametreler kullanarak destekler.</span><span class="sxs-lookup"><span data-stu-id="09a5e-145">EventFlow supports using Service Fabric settings and application paremeters to configure EventFlow settings.</span></span> <span data-ttu-id="09a5e-146">Service Fabric ayarlar parametreleri için değerleri bu özel sözdizimini kullanarak başvurabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="09a5e-146">You can refer to Service Fabric settings parameters using this special syntax for values:</span></span>

```json
servicefabric:/<section-name>/<setting-name>
``` 

<span data-ttu-id="09a5e-147">`<section-name>`Service Fabric yapılandırma bölümü adıdır ve `<setting-name>` EventFlow ayarını yapılandırmak için kullanılan değer sağlayan yapılandırma ayarı.</span><span class="sxs-lookup"><span data-stu-id="09a5e-147">`<section-name>` is the name of the Service Fabric configuration section, and `<setting-name>` is the configuration setting providing the value that will be used to configure an EventFlow setting.</span></span> <span data-ttu-id="09a5e-148">Okumak için bunun nasıl yapılacağı hakkında daha fazla Git [Service Fabric ayarları ve uygulama parametreleri desteği](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span><span class="sxs-lookup"><span data-stu-id="09a5e-148">To read more about how to do this, go to [Support for Service Fabric settings and application parameters](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).</span></span>

## <a name="verification"></a><span data-ttu-id="09a5e-149">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="09a5e-149">Verification</span></span>

<span data-ttu-id="09a5e-150">Hizmetinizi başlatın ve hata ayıklama uyun Visual Studio çıktı penceresinde.</span><span class="sxs-lookup"><span data-stu-id="09a5e-150">Start your service and observe the Debug output window in Visual Studio.</span></span> <span data-ttu-id="09a5e-151">Hizmeti başlatıldıktan sonra hizmetiniz kayıtları yapılandırdığınız çıktı gönderiyor kanıt görmeye başlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="09a5e-151">After the service is started, you should start seeing evidence that your service is sending records to the output that you have configured.</span></span> <span data-ttu-id="09a5e-152">Olay çözümleme ve görselleştirme platformunuz için gidin ve günlükleri göstermek başlatılmış olduğunu onaylayın Yukarı (birkaç dakika sürebilir).</span><span class="sxs-lookup"><span data-stu-id="09a5e-152">Navigate to your event analysis and visualization platform and confirm that logs have started to show up (could take a few minutes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09a5e-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="09a5e-153">Next steps</span></span>

* [<span data-ttu-id="09a5e-154">Olay çözümleme ve görselleştirme Application Insights ile</span><span class="sxs-lookup"><span data-stu-id="09a5e-154">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="09a5e-155">Olay çözümleme ve OMS Görselleştirme</span><span class="sxs-lookup"><span data-stu-id="09a5e-155">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)
* [<span data-ttu-id="09a5e-156">EventFlow belgeleri</span><span class="sxs-lookup"><span data-stu-id="09a5e-156">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)