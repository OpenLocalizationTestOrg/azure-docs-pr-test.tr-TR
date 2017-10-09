---
title: "aaaCollect günlükleri doğrudan bir Azure hizmeti yapıdan hizmet işlemi | Microsoft Azure"
description: "Service Fabric tooa merkezi bir konum ister doğrudan Azure Application Insights veya Elasticsearch, Azure tanılama Aracısı'nı kullanmadan uygulamaları günlüklerini gönderebilirsiniz açıklar."
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: rwike77
editor: 
ms.assetid: ab92c99b-1edd-4677-8c28-4e591d909b47
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/18/2017
ms.author: karolz
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: d0681a2a6aaa76028d7cb469c31c006f24bbe954
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a><span data-ttu-id="dadbd-103">Bir Azure Service Fabric hizmeti işleminin doğrudan günlüklerini toplayın</span><span class="sxs-lookup"><span data-stu-id="dadbd-103">Collect logs directly from an Azure Service Fabric service process</span></span>
## <a name="in-process-log-collection"></a><span data-ttu-id="dadbd-104">İşlem içi oturum koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="dadbd-104">In-process log collection</span></span>
<span data-ttu-id="dadbd-105">Günlüklerini kullanarak uygulama toplama [Azure tanılama uzantısını](service-fabric-diagnostics-how-to-setup-wad.md) için iyi bir seçenektir **Azure Service Fabric** Hizmetleri hello dizi günlük kaynakları ve hedeflere küçükse değiştirmez genellikle ve var. Merhaba kaynakları ve hedeflerine arasında basit bir eşlemedir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-105">Collecting application logs using [Azure Diagnostics extension](service-fabric-diagnostics-how-to-setup-wad.md) is a good option for **Azure Service Fabric** services if hello set of log sources and destinations is small, does not change often, and there is a straightforward mapping between hello sources and their destinations.</span></span> <span data-ttu-id="dadbd-106">Aksi durumda, toohave Hizmetleri günlükleri tooa merkezi bir konum doğrudan göndermek alternatiftir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-106">If not, an alternative is toohave services send their logs directly tooa central location.</span></span> <span data-ttu-id="dadbd-107">Bu işlem olarak bilinir **işlemdeki günlük toplama** ve birkaç olası üstünlüğü vardır:</span><span class="sxs-lookup"><span data-stu-id="dadbd-107">This process is known as **in-process log collection** and has several potential advantages:</span></span>

* <span data-ttu-id="dadbd-108">*Kolay yapılandırma ve dağıtma*</span><span class="sxs-lookup"><span data-stu-id="dadbd-108">*Easy configuration and deployment*</span></span>

    * <span data-ttu-id="dadbd-109">tanılama veri toplama Hello yapılandırmasının değil yalnızca hello hizmet yapılandırmasını parçası.</span><span class="sxs-lookup"><span data-stu-id="dadbd-109">hello configuration of diagnostic data collection is just part of hello service configuration.</span></span> <span data-ttu-id="dadbd-110">"Hello ile eşitleme", rest hello uygulamasının kolay tooalways Canlı olur.</span><span class="sxs-lookup"><span data-stu-id="dadbd-110">It is easy tooalways keep it "in sync" with hello rest of hello application.</span></span>
    * <span data-ttu-id="dadbd-111">Her uygulama veya hizmet başına yapılandırma kolayca elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-111">Per-application or per-service configuration is easily achievable.</span></span>
        * <span data-ttu-id="dadbd-112">Tabanlı aracı günlük toplama genellikle ayrı bir dağıtım ve bir ek yönetim görevini ve hataların olası kaynak hello Tanılama Aracı yapılandırmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-112">Agent-based log collection usually requires a separate deployment and configuration of hello diagnostic agent, which is an extra administrative task and a potential source of errors.</span></span> <span data-ttu-id="dadbd-113">Genellikle yalnızca bir sanal makine (düğüm) başına izin verilen hello aracı örneği yoktur ve hello Aracısı yapılandırması tüm uygulamalar ve bu düğümde çalışan hizmetler tarafından paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="dadbd-113">Often there is only one instance of hello agent allowed per virtual machine (node) and hello agent configuration is shared among all applications and services running on that node.</span></span> 

* <span data-ttu-id="dadbd-114">*Esneklik*</span><span class="sxs-lookup"><span data-stu-id="dadbd-114">*Flexibility*</span></span>
   
    * <span data-ttu-id="dadbd-115">toogo, gereken her yerde hedeflenen hello veri depolama sistemi destekleyen bir istemci kitaplığı var olduğu sürece Merhaba uygulaması hello veriler gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-115">hello application can send hello data wherever it needs toogo, as long as there is a client library that supports hello targeted data storage system.</span></span> <span data-ttu-id="dadbd-116">Yeni hedefler eklenebilir istenen şekilde.</span><span class="sxs-lookup"><span data-stu-id="dadbd-116">New destinations can be added as desired.</span></span>
    * <span data-ttu-id="dadbd-117">Karmaşık yakalama, filtreleme ve veri toplama kuralları uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-117">Complex capture, filtering, and data-aggregation rules can be implemented.</span></span>
    * <span data-ttu-id="dadbd-118">Tabanlı aracı günlük toplama Aracısı destekler hello hello veri havuzlarını tarafından çoğunlukla sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="dadbd-118">Agent-based log collection is often limited by hello data sinks that hello agent supports.</span></span> <span data-ttu-id="dadbd-119">Bazı aracılar genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-119">Some agents are extensible.</span></span>

* <span data-ttu-id="dadbd-120">*Erişim toointernal uygulama verilerini ve içeriği*</span><span class="sxs-lookup"><span data-stu-id="dadbd-120">*Access toointernal application data and context*</span></span>
   
    * <span data-ttu-id="dadbd-121">Merhaba uygulama/hizmet işlemi içinde çalışan hello tanılama alt sistemi kolayca hello izlemeleri bağlamsal bilgi ile genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dadbd-121">hello diagnostic subsystem running inside hello application/service process can easily augment hello traces with contextual information.</span></span>
    * <span data-ttu-id="dadbd-122">Günlük tabanlı aracı koleksiyonuyla hello veri Windows için olay izleme gibi bazı işlemler arası iletişim mekanizması aracılığıyla tooan Aracısı gönderilmelidir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-122">With agent-based log collection, hello data must be sent tooan agent via some inter-process communication mechanism, such as Event Tracing for Windows.</span></span> <span data-ttu-id="dadbd-123">Bu mekanizma ek sınırlamalar zorunlu tuttukları.</span><span class="sxs-lookup"><span data-stu-id="dadbd-123">This mechanism could impose additional limitations.</span></span>

<span data-ttu-id="dadbd-124">Bu olası toocombine ve her iki koleksiyon yöntemlerden avantajı olur.</span><span class="sxs-lookup"><span data-stu-id="dadbd-124">It is possible toocombine and benefit from both collection methods.</span></span> <span data-ttu-id="dadbd-125">Aslında, pek çok uygulama hello en iyi çözüm olabilir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-125">Indeed, it might be hello best solution for many applications.</span></span> <span data-ttu-id="dadbd-126">Aracı tabanlı koleksiyon günlükleri ilgili toohello tüm küme ve tekil küme düğümlerine toplamak için doğal bir çözümdür.</span><span class="sxs-lookup"><span data-stu-id="dadbd-126">Agent-based collection is a natural solution for collecting logs related toohello whole cluster and individual cluster nodes.</span></span> <span data-ttu-id="dadbd-127">İşlem içi oturum koleksiyonu, toodiagnose hizmeti başlatma sorunları ve kilitlenme daha çok daha güvenilir bir yolu değil.</span><span class="sxs-lookup"><span data-stu-id="dadbd-127">It is much more reliable way, than in-process log collection, toodiagnose service startup problems and crashes.</span></span> <span data-ttu-id="dadbd-128">Ayrıca, Service Fabric kümesi içinde çalışan birçok Hizmetleri ile her hizmetin kendi işlem içi oturum koleksiyonu yapılması hello kümesinden çok sayıda giden bağlantılar sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="dadbd-128">Also, with many services running inside a Service Fabric cluster, each service doing its own in-process log collection results in numerous outgoing connections from hello cluster.</span></span> <span data-ttu-id="dadbd-129">Giden bağlantılar çok sayıda hello ağ alt sistemi hem hello günlük hedefi yükünü artırmasının tersine.</span><span class="sxs-lookup"><span data-stu-id="dadbd-129">Large number of outgoing connections is taxing both for hello network subsystem and for hello log destination.</span></span> <span data-ttu-id="dadbd-130">Bir aracı gibi [ **Azure tanılama** ](../cloud-services/cloud-services-dotnet-diagnostics.md) birden çok Hizmetleri'nden veri toplamak ve üretilen iş iyileştirme birkaç bağlantıları üzerinden tüm verileri gönder.</span><span class="sxs-lookup"><span data-stu-id="dadbd-130">An agent such as [**Azure Diagnostics**](../cloud-services/cloud-services-dotnet-diagnostics.md) can gather data from multiple services and send all data through a few connections, improving throughput.</span></span> 

<span data-ttu-id="dadbd-131">Bu makalede, bir işlem içi yukarı tooset nasıl oturum koleksiyonunu kullanarak olan gösteriyoruz [ **EventFlow açık kaynak Kitaplığı**](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="dadbd-131">In this article, we show how tooset up an in-process log collection using [**EventFlow open-source library**](https://github.com/Azure/diagnostics-eventflow).</span></span> <span data-ttu-id="dadbd-132">Diğer kitaplıkları kullanılan Merhaba aynı amacı ancak EventFlow özellikle işlem içi oturum koleksiyonu ve toosupport Service Fabric Hizmetleri için tasarlanmış hello avantajına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-132">Other libraries might be used for hello same purpose, but EventFlow has hello benefit of having been designed specifically for in-process log collection and toosupport Service Fabric services.</span></span> <span data-ttu-id="dadbd-133">Kullanırız [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) hello günlük hedefi olarak.</span><span class="sxs-lookup"><span data-stu-id="dadbd-133">We use [**Azure Application Insights**](https://azure.microsoft.com/services/application-insights/) as hello log destination.</span></span> <span data-ttu-id="dadbd-134">Gibi diğer hedefleri [ **Event Hubs** ](https://azure.microsoft.com/services/event-hubs/) veya [ **Elasticsearch** ](https://www.elastic.co/products/elasticsearch) de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-134">Other destinations such as [**Event Hubs**](https://azure.microsoft.com/services/event-hubs/) or [**Elasticsearch**](https://www.elastic.co/products/elasticsearch) are also supported.</span></span> <span data-ttu-id="dadbd-135">Bu, uygun NuGet paketi yükleniyor ve hello hedef hello EventFlow yapılandırma dosyasındaki yapılandırma yalnızca bir soru olur.</span><span class="sxs-lookup"><span data-stu-id="dadbd-135">It is just a question of installing appropriate NuGet package and configuring hello destination in hello EventFlow configuration file.</span></span> <span data-ttu-id="dadbd-136">Application Insights dışında günlük hedefleri hakkında daha fazla bilgi için bkz: [EventFlow belgelerine](https://github.com/Azure/diagnostics-eventflow).</span><span class="sxs-lookup"><span data-stu-id="dadbd-136">For more information on log destinations other than Application Insights, see [EventFlow documentation](https://github.com/Azure/diagnostics-eventflow).</span></span>

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a><span data-ttu-id="dadbd-137">EventFlow kitaplığı tooa Service Fabric hizmeti projesi ekleme</span><span class="sxs-lookup"><span data-stu-id="dadbd-137">Adding EventFlow library tooa Service Fabric service project</span></span>
<span data-ttu-id="dadbd-138">EventFlow ikili dosyaları NuGet paketlerini bir dizi kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-138">EventFlow binaries are available as a set of NuGet packages.</span></span> <span data-ttu-id="dadbd-139">tooadd EventFlow tooa Service Fabric hizmeti projesi, hello Çözüm Gezgini hello projeye sağ tıklayın ve "Manage NuGet paketlerini."'i seçin</span><span class="sxs-lookup"><span data-stu-id="dadbd-139">tooadd EventFlow tooa Service Fabric service project, right-click hello project in hello Solution Explorer and choose "Manage NuGet packages."</span></span> <span data-ttu-id="dadbd-140">Toohello "Gözat" sekmesini ve aramak için anahtar "`Diagnostics.EventFlow`":</span><span class="sxs-lookup"><span data-stu-id="dadbd-140">Switch toohello "Browse" tab and search for "`Diagnostics.EventFlow`":</span></span>

![Visual Studio NuGet Paket Yöneticisi kullanıcı Arabirimi EventFlow NuGet paketleri][1]

<span data-ttu-id="dadbd-142">hello service EventFlow barındırma hello kaynak ve hedef hello uygulama günlükleri için bağlı olarak uygun paketleri içermelidir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-142">hello service hosting EventFlow should include appropriate packages depending on hello source and destination for hello application logs.</span></span> <span data-ttu-id="dadbd-143">Paketleri aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="dadbd-143">Add hello following packages:</span></span> 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * <span data-ttu-id="dadbd-144">(toocapture veri hello hizmetin EventSource sınıfı ve gibi standart EventSources *Microsoft ServiceFabric Hizmetleri* ve *Microsoft ServiceFabric aktörler*)</span><span class="sxs-lookup"><span data-stu-id="dadbd-144">(toocapture data from hello service's EventSource class, and from standard EventSources such as *Microsoft-ServiceFabric-Services* and *Microsoft-ServiceFabric-Actors*)</span></span>
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * <span data-ttu-id="dadbd-145">(biz toosend hello günlükleri tooan Azure Application Insights kaynağı kalacaklarını)</span><span class="sxs-lookup"><span data-stu-id="dadbd-145">(we are going toosend hello logs tooan Azure Application Insights resource)</span></span>  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * <span data-ttu-id="dadbd-146">(Merhaba EventFlow ardışık Service Fabric hizmet yapılandırmasından başlatma sağlar ve Service Fabric sistem durumu raporlarının Tanılama verileri gönderme ile herhangi bir sorun raporları)</span><span class="sxs-lookup"><span data-stu-id="dadbd-146">(enables initialization of hello EventFlow pipeline from Service Fabric service configuration and reports any problems with sending diagnostic data as Service Fabric health reports)</span></span>

> [!NOTE]
> <span data-ttu-id="dadbd-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource`Paket hello hizmet projesi tootarget .NET Framework 4.6 gerektiren ya da daha yeni.</span><span class="sxs-lookup"><span data-stu-id="dadbd-147">`Microsoft.Diagnostics.EventFlow.Inputs.EventSource` package requires hello service project tootarget .NET Framework 4.6 or newer.</span></span> <span data-ttu-id="dadbd-148">Bu paketi yüklemeden önce Proje Özellikleri'nde hello uygun hedef framework ayarladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="dadbd-148">Make sure you set hello appropriate target framework in project properties before installing this package.</span></span> 

<span data-ttu-id="dadbd-149">Tüm hello paketleri yüklendi, hello sonraki adımı tooconfigure ve EventFlow hello hizmeti etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="dadbd-149">After all hello packages are installed, hello next step is tooconfigure and enable EventFlow in hello service.</span></span>

## <a name="configuring-and-enabling-log-collection"></a><span data-ttu-id="dadbd-150">Yapılandırma ve günlük toplama etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="dadbd-150">Configuring and enabling log collection</span></span>
<span data-ttu-id="dadbd-151">EventFlow ardışık düzen, hello günlükleri göndermek için sorumlu bir yapılandırma dosyasında depolanan belirtiminden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="dadbd-151">EventFlow pipeline, responsible for sending hello logs, is created from a specification stored in a configuration file.</span></span> <span data-ttu-id="dadbd-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric`Paketi yükler altında başlangıç EventFlow yapılandırma dosyası `PackageRoot\Config` Çözüm klasörü.</span><span class="sxs-lookup"><span data-stu-id="dadbd-152">`Microsoft.Diagnostics.EventFlow.ServiceFabric` package installs a starting EventFlow configuration file under `PackageRoot\Config` solution folder.</span></span> <span data-ttu-id="dadbd-153">Merhaba dosya adı `eventFlowConfig.json`.</span><span class="sxs-lookup"><span data-stu-id="dadbd-153">hello file name is `eventFlowConfig.json`.</span></span> <span data-ttu-id="dadbd-154">Bu yapılandırma dosyasını değiştirdi toobe toocapture verilerinin hello varsayılan hizmetinden gerekir. `EventSource` sınıf ve veri tooApplication Öngörüler hizmeti gönderin.</span><span class="sxs-lookup"><span data-stu-id="dadbd-154">This configuration file needs toobe modified toocapture data from hello default service `EventSource` class and send data tooApplication Insights service.</span></span>

> [!NOTE]
> <span data-ttu-id="dadbd-155">Aşina olduğunuzu varsayıyoruz **Azure Application Insights** hizmet ve Service Fabric hizmetinizi toouse toomonitor planlama Application Insights kaynağı vardır.</span><span class="sxs-lookup"><span data-stu-id="dadbd-155">We assume that you are familiar with **Azure Application Insights** service and that you have an Application Insights resource that you plan toouse toomonitor your Service Fabric service.</span></span> <span data-ttu-id="dadbd-156">Daha fazla bilgiye ihtiyacınız varsa lütfen bkz [bir Application Insights kaynağı oluşturma](../application-insights/app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="dadbd-156">If you need more information, please see [Create an Application Insights resource](../application-insights/app-insights-create-new-resource.md).</span></span>

<span data-ttu-id="dadbd-157">Açık hello `eventFlowConfig.json` hello Düzenleyicisi'nde dosya ve içeriğini aşağıda gösterildiği gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="dadbd-157">Open hello `eventFlowConfig.json` file in hello editor and change its content as shown below.</span></span> <span data-ttu-id="dadbd-158">Emin tooreplace hello ServiceEventSource adı ve Application Insights izleme anahtarı toocomments göre yapın.</span><span class="sxs-lookup"><span data-stu-id="dadbd-158">Make sure tooreplace hello ServiceEventSource name and Application Insights instrumentation key according toocomments.</span></span> 

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

> [!NOTE]
> <span data-ttu-id="dadbd-159">Merhaba hizmetin ServiceEventSource adıdır hello hello adını hello değerini `EventSourceAttribute` toohello ServiceEventSource sınıfı uygulanır.</span><span class="sxs-lookup"><span data-stu-id="dadbd-159">hello name of service's ServiceEventSource is hello value of hello Name property of hello `EventSourceAttribute` applied toohello ServiceEventSource class.</span></span> <span data-ttu-id="dadbd-160">Tüm hello belirtildiği `ServiceEventSource.cs` hello hizmet kod parçası olan dosya.</span><span class="sxs-lookup"><span data-stu-id="dadbd-160">It is all specified in hello `ServiceEventSource.cs` file, which is part of hello service code.</span></span> <span data-ttu-id="dadbd-161">Örneğin, hello aşağıdaki kod parçacığını hello hello ServiceEventSource adıdır *Şirketim Application1 Stateless1*:</span><span class="sxs-lookup"><span data-stu-id="dadbd-161">For example, in hello following code snippet hello name of hello ServiceEventSource is *MyCompany-Application1-Stateless1*:</span></span>
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

<span data-ttu-id="dadbd-162">Unutmayın `eventFlowConfig.json` dosya hizmeti yapılandırma paketi bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="dadbd-162">Note that `eventFlowConfig.json` file is part of service configuration package.</span></span> <span data-ttu-id="dadbd-163">Tam veya yapılandırma-yalnızca hello hizmetinin yükseltmeleri değişiklikleri toothis dosya eklenebilir, konu tooService doku yükseltin sistem durumu denetimlerinin ve Otomatik geri alma yükseltme hatası ise.</span><span class="sxs-lookup"><span data-stu-id="dadbd-163">Changes toothis file can be included in full- or configuration-only upgrades of hello service, subject tooService Fabric upgrade health checks and automatic rollback if there is upgrade failure.</span></span> <span data-ttu-id="dadbd-164">Daha fazla bilgi için bkz: [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="dadbd-164">For more information, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

<span data-ttu-id="dadbd-165">Merhaba son adımdır tooinstantiate EventFlow ardışık düzeninde bulunan Hizmetinizin başlangıç kodu `Program.cs` dosya.</span><span class="sxs-lookup"><span data-stu-id="dadbd-165">hello final step is tooinstantiate EventFlow pipeline in your service's startup code, located in `Program.cs` file.</span></span> <span data-ttu-id="dadbd-166">Hello başlayarak açıklamaları olan aşağıdaki örnek EventFlow ilgili eklemeler işaretlenmiş `****`:</span><span class="sxs-lookup"><span data-stu-id="dadbd-166">In hello following example  EventFlow-related additions are marked with comments starting with `****`:</span></span>

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

<span data-ttu-id="dadbd-167">Merhaba adı hello hello parametre olarak geçirilen `CreatePipeline` hello yöntemi `ServiceFabricDiagnosticsPipelineFactory` hello hello adıdır *sistem durumu varlık* hello EventFlow günlük toplama ardışık temsil eden.</span><span class="sxs-lookup"><span data-stu-id="dadbd-167">hello name passed as hello parameter of hello `CreatePipeline` method of hello `ServiceFabricDiagnosticsPipelineFactory` is hello name of hello *health entity* representing hello EventFlow log collection pipeline.</span></span> <span data-ttu-id="dadbd-168">Bu ad EventFlow karşılaşırsa kullanılır ve hata ve Service Fabric sistem durumu alt hello bildirir.</span><span class="sxs-lookup"><span data-stu-id="dadbd-168">This name is used if EventFlow encounters and error and reports it through hello Service Fabric health subsystem.</span></span>

## <a name="verification"></a><span data-ttu-id="dadbd-169">Doğrulama</span><span class="sxs-lookup"><span data-stu-id="dadbd-169">Verification</span></span>
<span data-ttu-id="dadbd-170">Hizmetinizi başlatın ve hata ayıklama hello uyun Visual Studio çıktı penceresinde.</span><span class="sxs-lookup"><span data-stu-id="dadbd-170">Start your service and observe hello Debug output window in Visual Studio.</span></span> <span data-ttu-id="dadbd-171">Merhaba hizmeti başlatıldıktan sonra "Application Insights Telemetrisi" kayıtlarının hizmetinizin gönderiyor kanıt görmeye başlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="dadbd-171">After hello service is started, you should start seeing evidence that your service is sending "Application Insights Telemetry" records.</span></span> <span data-ttu-id="dadbd-172">Bir web tarayıcısı açın ve gidin tooyour Application Insights kaynağı gidin.</span><span class="sxs-lookup"><span data-stu-id="dadbd-172">Open a web browser and navigate go tooyour Application Insights resource.</span></span> <span data-ttu-id="dadbd-173">(Üstündeki hello hello varsayılan "Genel bakış" dikey) "Ara" sekmesini açın.</span><span class="sxs-lookup"><span data-stu-id="dadbd-173">Open "Search" tab (at hello top of hello default "Overview" blade).</span></span> <span data-ttu-id="dadbd-174">Kısa bir gecikmeden sonra izleri hello Application Insights portalında görmeye başlayacaksınız:</span><span class="sxs-lookup"><span data-stu-id="dadbd-174">After a short delay you should start seeing your traces in hello Application Insights portal:</span></span>

![Service Fabric uygulaması günlüklerinden gösteren uygulama Insights portalı][2]

## <a name="next-steps"></a><span data-ttu-id="dadbd-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dadbd-176">Next steps</span></span>
* [<span data-ttu-id="dadbd-177">Tanılama ve bir Service Fabric hizmeti izleme hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="dadbd-177">Learn more about diagnosing and monitoring a Service Fabric service</span></span>](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [<span data-ttu-id="dadbd-178">EventFlow belgeleri</span><span class="sxs-lookup"><span data-stu-id="dadbd-178">EventFlow documentation</span></span>](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
