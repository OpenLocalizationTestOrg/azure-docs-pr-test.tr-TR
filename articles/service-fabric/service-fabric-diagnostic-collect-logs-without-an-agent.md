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
# <a name="collect-logs-directly-from-an-azure-service-fabric-service-process"></a>Bir Azure Service Fabric hizmeti işleminin doğrudan günlüklerini toplayın
## <a name="in-process-log-collection"></a>İşlem içi oturum koleksiyonu
Günlüklerini kullanarak uygulama toplama [Azure tanılama uzantısını](service-fabric-diagnostics-how-to-setup-wad.md) için iyi bir seçenektir **Azure Service Fabric** Hizmetleri hello dizi günlük kaynakları ve hedeflere küçükse değiştirmez genellikle ve var. Merhaba kaynakları ve hedeflerine arasında basit bir eşlemedir. Aksi durumda, toohave Hizmetleri günlükleri tooa merkezi bir konum doğrudan göndermek alternatiftir. Bu işlem olarak bilinir **işlemdeki günlük toplama** ve birkaç olası üstünlüğü vardır:

* *Kolay yapılandırma ve dağıtma*

    * tanılama veri toplama Hello yapılandırmasının değil yalnızca hello hizmet yapılandırmasını parçası. "Hello ile eşitleme", rest hello uygulamasının kolay tooalways Canlı olur.
    * Her uygulama veya hizmet başına yapılandırma kolayca elde edilebilir.
        * Tabanlı aracı günlük toplama genellikle ayrı bir dağıtım ve bir ek yönetim görevini ve hataların olası kaynak hello Tanılama Aracı yapılandırmasını gerektirir. Genellikle yalnızca bir sanal makine (düğüm) başına izin verilen hello aracı örneği yoktur ve hello Aracısı yapılandırması tüm uygulamalar ve bu düğümde çalışan hizmetler tarafından paylaşılır. 

* *Esneklik*
   
    * toogo, gereken her yerde hedeflenen hello veri depolama sistemi destekleyen bir istemci kitaplığı var olduğu sürece Merhaba uygulaması hello veriler gönderebilir. Yeni hedefler eklenebilir istenen şekilde.
    * Karmaşık yakalama, filtreleme ve veri toplama kuralları uygulanabilir.
    * Tabanlı aracı günlük toplama Aracısı destekler hello hello veri havuzlarını tarafından çoğunlukla sınırlıdır. Bazı aracılar genişletilebilir.

* *Erişim toointernal uygulama verilerini ve içeriği*
   
    * Merhaba uygulama/hizmet işlemi içinde çalışan hello tanılama alt sistemi kolayca hello izlemeleri bağlamsal bilgi ile genişletebilirsiniz.
    * Günlük tabanlı aracı koleksiyonuyla hello veri Windows için olay izleme gibi bazı işlemler arası iletişim mekanizması aracılığıyla tooan Aracısı gönderilmelidir. Bu mekanizma ek sınırlamalar zorunlu tuttukları.

Bu olası toocombine ve her iki koleksiyon yöntemlerden avantajı olur. Aslında, pek çok uygulama hello en iyi çözüm olabilir. Aracı tabanlı koleksiyon günlükleri ilgili toohello tüm küme ve tekil küme düğümlerine toplamak için doğal bir çözümdür. İşlem içi oturum koleksiyonu, toodiagnose hizmeti başlatma sorunları ve kilitlenme daha çok daha güvenilir bir yolu değil. Ayrıca, Service Fabric kümesi içinde çalışan birçok Hizmetleri ile her hizmetin kendi işlem içi oturum koleksiyonu yapılması hello kümesinden çok sayıda giden bağlantılar sonuçlanır. Giden bağlantılar çok sayıda hello ağ alt sistemi hem hello günlük hedefi yükünü artırmasının tersine. Bir aracı gibi [ **Azure tanılama** ](../cloud-services/cloud-services-dotnet-diagnostics.md) birden çok Hizmetleri'nden veri toplamak ve üretilen iş iyileştirme birkaç bağlantıları üzerinden tüm verileri gönder. 

Bu makalede, bir işlem içi yukarı tooset nasıl oturum koleksiyonunu kullanarak olan gösteriyoruz [ **EventFlow açık kaynak Kitaplığı**](https://github.com/Azure/diagnostics-eventflow). Diğer kitaplıkları kullanılan Merhaba aynı amacı ancak EventFlow özellikle işlem içi oturum koleksiyonu ve toosupport Service Fabric Hizmetleri için tasarlanmış hello avantajına sahiptir. Kullanırız [ **Azure Application Insights** ](https://azure.microsoft.com/services/application-insights/) hello günlük hedefi olarak. Gibi diğer hedefleri [ **Event Hubs** ](https://azure.microsoft.com/services/event-hubs/) veya [ **Elasticsearch** ](https://www.elastic.co/products/elasticsearch) de desteklenir. Bu, uygun NuGet paketi yükleniyor ve hello hedef hello EventFlow yapılandırma dosyasındaki yapılandırma yalnızca bir soru olur. Application Insights dışında günlük hedefleri hakkında daha fazla bilgi için bkz: [EventFlow belgelerine](https://github.com/Azure/diagnostics-eventflow).

## <a name="adding-eventflow-library-tooa-service-fabric-service-project"></a>EventFlow kitaplığı tooa Service Fabric hizmeti projesi ekleme
EventFlow ikili dosyaları NuGet paketlerini bir dizi kullanılabilir. tooadd EventFlow tooa Service Fabric hizmeti projesi, hello Çözüm Gezgini hello projeye sağ tıklayın ve "Manage NuGet paketlerini."'i seçin Toohello "Gözat" sekmesini ve aramak için anahtar "`Diagnostics.EventFlow`":

![Visual Studio NuGet Paket Yöneticisi kullanıcı Arabirimi EventFlow NuGet paketleri][1]

hello service EventFlow barındırma hello kaynak ve hedef hello uygulama günlükleri için bağlı olarak uygun paketleri içermelidir. Paketleri aşağıdaki hello ekleyin: 

* `Microsoft.Diagnostics.EventFlow.Inputs.EventSource` 
    * (toocapture veri hello hizmetin EventSource sınıfı ve gibi standart EventSources *Microsoft ServiceFabric Hizmetleri* ve *Microsoft ServiceFabric aktörler*)
* `Microsoft.Diagnostics.EventFlow.Outputs.ApplicationInsights` 
    * (biz toosend hello günlükleri tooan Azure Application Insights kaynağı kalacaklarını)  
* `Microsoft.Diagnostics.EventFlow.ServiceFabric` 
    * (Merhaba EventFlow ardışık Service Fabric hizmet yapılandırmasından başlatma sağlar ve Service Fabric sistem durumu raporlarının Tanılama verileri gönderme ile herhangi bir sorun raporları)

> [!NOTE]
> `Microsoft.Diagnostics.EventFlow.Inputs.EventSource`Paket hello hizmet projesi tootarget .NET Framework 4.6 gerektiren ya da daha yeni. Bu paketi yüklemeden önce Proje Özellikleri'nde hello uygun hedef framework ayarladığınızdan emin olun. 

Tüm hello paketleri yüklendi, hello sonraki adımı tooconfigure ve EventFlow hello hizmeti etkinleştirin.

## <a name="configuring-and-enabling-log-collection"></a>Yapılandırma ve günlük toplama etkinleştirme
EventFlow ardışık düzen, hello günlükleri göndermek için sorumlu bir yapılandırma dosyasında depolanan belirtiminden oluşturulur. `Microsoft.Diagnostics.EventFlow.ServiceFabric`Paketi yükler altında başlangıç EventFlow yapılandırma dosyası `PackageRoot\Config` Çözüm klasörü. Merhaba dosya adı `eventFlowConfig.json`. Bu yapılandırma dosyasını değiştirdi toobe toocapture verilerinin hello varsayılan hizmetinden gerekir. `EventSource` sınıf ve veri tooApplication Öngörüler hizmeti gönderin.

> [!NOTE]
> Aşina olduğunuzu varsayıyoruz **Azure Application Insights** hizmet ve Service Fabric hizmetinizi toouse toomonitor planlama Application Insights kaynağı vardır. Daha fazla bilgiye ihtiyacınız varsa lütfen bkz [bir Application Insights kaynağı oluşturma](../application-insights/app-insights-create-new-resource.md).

Açık hello `eventFlowConfig.json` hello Düzenleyicisi'nde dosya ve içeriğini aşağıda gösterildiği gibi değiştirin. Emin tooreplace hello ServiceEventSource adı ve Application Insights izleme anahtarı toocomments göre yapın. 

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
> Merhaba hizmetin ServiceEventSource adıdır hello hello adını hello değerini `EventSourceAttribute` toohello ServiceEventSource sınıfı uygulanır. Tüm hello belirtildiği `ServiceEventSource.cs` hello hizmet kod parçası olan dosya. Örneğin, hello aşağıdaki kod parçacığını hello hello ServiceEventSource adıdır *Şirketim Application1 Stateless1*:
> ```csharp
> [EventSource(Name = "MyCompany-Application1-Stateless1")]
> internal sealed class ServiceEventSource : EventSource
> {
>    // (rest of ServiceEventSource implementation)
>} 
> ```

Unutmayın `eventFlowConfig.json` dosya hizmeti yapılandırma paketi bir parçasıdır. Tam veya yapılandırma-yalnızca hello hizmetinin yükseltmeleri değişiklikleri toothis dosya eklenebilir, konu tooService doku yükseltin sistem durumu denetimlerinin ve Otomatik geri alma yükseltme hatası ise. Daha fazla bilgi için bkz: [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md).

Merhaba son adımdır tooinstantiate EventFlow ardışık düzeninde bulunan Hizmetinizin başlangıç kodu `Program.cs` dosya. Hello başlayarak açıklamaları olan aşağıdaki örnek EventFlow ilgili eklemeler işaretlenmiş `****`:

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

Merhaba adı hello hello parametre olarak geçirilen `CreatePipeline` hello yöntemi `ServiceFabricDiagnosticsPipelineFactory` hello hello adıdır *sistem durumu varlık* hello EventFlow günlük toplama ardışık temsil eden. Bu ad EventFlow karşılaşırsa kullanılır ve hata ve Service Fabric sistem durumu alt hello bildirir.

## <a name="verification"></a>Doğrulama
Hizmetinizi başlatın ve hata ayıklama hello uyun Visual Studio çıktı penceresinde. Merhaba hizmeti başlatıldıktan sonra "Application Insights Telemetrisi" kayıtlarının hizmetinizin gönderiyor kanıt görmeye başlayacaksınız. Bir web tarayıcısı açın ve gidin tooyour Application Insights kaynağı gidin. (Üstündeki hello hello varsayılan "Genel bakış" dikey) "Ara" sekmesini açın. Kısa bir gecikmeden sonra izleri hello Application Insights portalında görmeye başlayacaksınız:

![Service Fabric uygulaması günlüklerinden gösteren uygulama Insights portalı][2]

## <a name="next-steps"></a>Sonraki adımlar
* [Tanılama ve bir Service Fabric hizmeti izleme hakkında daha fazla bilgi edinin](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)
* [EventFlow belgeleri](https://github.com/Azure/diagnostics-eventflow)


<!--Image references-->
[1]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/eventflow-nugets.png
[2]: ./media/service-fabric-diagnostics-collect-logs-without-an-agent/ai-traces.png
