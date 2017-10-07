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
# <a name="event-aggregation-and-collection-using-eventflow"></a>Olay toplama ve EventFlow kullanarak koleksiyonu

[Microsoft tanılama EventFlow](https://github.com/Azure/diagnostics-eventflow) düğümü tooone ya da daha fazla izleme hedefleri olaylarından yönlendirebilir. Hizmet projenizdeki NuGet paketi olarak dahil olduğundan Azure Tanılama hakkında daha önce bahsedilen hello düğüm başına yapılandırma sorunu ortadan hello hizmetiyle EventFlow kod ve yapılandırma ilerler. EventFlow hizmet işlemi içinde çalıştırılan ve yapılandırılmış toohello çıkışları doğrudan bağlanır. Merhaba doğrudan bağlantı nedeniyle EventFlow Azure, kapsayıcı ve şirket içi hizmet dağıtımları için çalışır. Her EventFlow ardışık düzen bir dış bağlantısı yaptığından EventFlow yüksek yoğunluklu senaryolarda gibi bir kapsayıcıda çalıştırırsanız dikkatli olun. Bu nedenle, çeşitli işlemleri barındırıyorsanız, birkaç giden bağlantılar alın! Bu Service Fabric uygulamaları için kadar bir sorun olduğundan değil tüm çoğaltmaları bir `ServiceType` çalıştırın hello aynı işlemi ve bu giden bağlantılar hello sayısını sınırlar. Böylece hello belirtilen filtreyle eşleşen hello olayları gönderilir EventFlow ayrıca olay filtreleme, sunar.

## <a name="setting-up-eventflow"></a>EventFlow ayarlama

EventFlow ikili dosyaları NuGet paketlerini bir dizi kullanılabilir. tooadd EventFlow tooa Service Fabric hizmeti projesi, hello Çözüm Gezgini hello projeye sağ tıklayın ve "Manage NuGet paketlerini."'i seçin Toohello "Gözat" sekmesini ve aramak için anahtar "`Diagnostics.EventFlow`":

![Visual Studio NuGet Paket Yöneticisi kullanıcı Arabirimi EventFlow NuGet paketleri](./media/service-fabric-diagnostics-event-aggregation-eventflow/eventflow-nuget.png)

Çeşitli paketler, "Girdi" ve "Çıkaran" etiketli gösteri listesini görürsünüz. EventFlow çeşitli farklı günlüğü sağlayıcıları ve çözümleyiciler destekler. hello service EventFlow barındırma hello kaynak ve hedef hello uygulama günlükleri için bağlı olarak uygun paketleri içermelidir. Ayrıca toohello çekirdek ServiceFabric paketi, ayrıca en az bir giriş ve çıkış yapılandırılması gerekir. Exmaple için paketler toosent EventSource olaylarını tooApplication Öngörüler aşağıdaki hello ekleyebilirsiniz:

* `Microsoft.Diagnostics.EventFlow.Input.EventSource`toocapture veri hello hizmetin EventSource sınıfı ve gibi standart EventSources *Microsoft ServiceFabric Hizmetleri* ve *Microsoft ServiceFabric aktörler*)
* `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`(biz toosend hello günlükleri tooan Azure Application Insights kaynağı kalacaklarını)
* `Microsoft.Diagnostics.EventFlow.ServiceFabric`(Merhaba EventFlow ardışık Service Fabric hizmet yapılandırmasından başlatma sağlar ve Service Fabric sistem durumu raporlarının Tanılama verileri gönderme ile herhangi bir sorun raporları)

>[!NOTE]
>`Microsoft.Diagnostics.EventFlow.Input.EventSource`Paket hello hizmet projesi tootarget .NET Framework 4.6 gerektiren ya da daha yeni. Bu paketi yüklemeden önce Proje Özellikleri'nde hello uygun hedef framework ayarladığınızdan emin olun.

Tüm hello paketleri yüklendi, hello sonraki adımı tooconfigure ve EventFlow hello hizmeti etkinleştirin.

## <a name="configuring-and-enabling-log-collection"></a>Yapılandırma ve günlük toplama etkinleştirme
Merhaba EventFlow ardışık düzen hello günlükleri göndermek için sorumlu bir yapılandırma dosyasında depolanan belirtiminden oluşturulur. Merhaba `Microsoft.Diagnostics.EventFlow.ServiceFabric` paketi yükler altında başlangıç EventFlow yapılandırma dosyası `PackageRoot\Config` adlı Çözüm klasörü `eventFlowConfig.json`. Bu yapılandırma dosyasını değiştirdi toobe toocapture verilerinin hello varsayılan hizmetinden gerekir. `EventSource` sınıfı ve tooconfigure istediğiniz ve veri toohello uygun yere gönderme tüm diğer girişler.

Örnek bir işte *eventFlowConfig.json* yukarıda belirtilen hello NuGet paketlerini göre:
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

Merhaba hizmetin ServiceEventSource adıdır hello hello adını hello değerini `EventSourceAttribute` toohello ServiceEventSource sınıfı uygulanır. Tüm hello belirtildiği `ServiceEventSource.cs` hello hizmet kod parçası olan dosya. Örneğin, hello aşağıdaki kod parçacığını hello hello ServiceEventSource adıdır *Şirketim Application1 Stateless1*:

```csharp
[EventSource(Name = "MyCompany-Application1-Stateless1")]
internal sealed class ServiceEventSource : EventSource
{
    // (rest of ServiceEventSource implementation)
}
```

Unutmayın `eventFlowConfig.json` dosya hizmeti yapılandırma paketi bir parçasıdır. Tam veya yapılandırma-yalnızca hello hizmetinin yükseltmeleri değişiklikleri toothis dosya eklenebilir, konu tooService doku yükseltin sistem durumu denetimlerinin ve Otomatik geri alma yükseltme hatası ise. Daha fazla bilgi için bkz: [Service Fabric uygulama yükseltme](service-fabric-application-upgrade.md).

Merhaba *filtreleri* hello yapılandırma bölümünü toofurther verir hello değiştirmek toodrop izin vererek hello EventFlow ardışık düzen toohello çıkışlarını üzerinden giderek toogo hello bilgileri özelleştirin veya belirli bilgiler içerir Merhaba olay veri yapısı. Filtreleri hakkında daha fazla bilgi için bkz: [EventFlow filtreleri](https://github.com/Azure/diagnostics-eventflow#filters).

Merhaba son adımdır tooinstantiate EventFlow ardışık Hizmetinizin başlangıç kod içinde bulunan, `Program.cs` dosyası:

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

### <a name="using-service-fabric-settings-and-application-parameters-tooin-eventflowconfig"></a>Service Fabric ayarları ve uygulama parametreleri tooin eventFlowConfig kullanma

Service Fabric ve uygulama parametreler tooconfigure EventFlow ayarlarını EventFlow kullanılmasını destekler. Bu özel bir sözdizimi için değerleri kullanarak tooService yapı ayarları parametrelerini başvurabilir:

```json
servicefabric:/<section-name>/<setting-name>
``` 

`<section-name>`Merhaba Service Fabric yapılandırma bölümü Hello adıdır ve `<setting-name>` hello yapılandırma ayarı EventFlow ayarı kullanılan tooconfigure hello değer sağlama. tooread nasıl hakkında daha fazla toodo Bu, Git çok[Service Fabric ayarları ve uygulama parametreleri desteği](https://github.com/Azure/diagnostics-eventflow#support-for-service-fabric-settings-and-application-parameters).

## <a name="verification"></a>Doğrulama

Hizmetinizi başlatın ve hata ayıklama hello uyun Visual Studio çıktı penceresinde. Merhaba hizmeti başlatıldıktan sonra yapılandırdığınız toohello çıkış hizmetinizi gönderme bulgu kayıtları görmeye başlayacaksınız. Tooyour olay çözümleme ve görselleştirme platform gidin ve günlükleri tooshow başlatılmış olduğunu onaylayın Yukarı (birkaç dakika sürebilir).

## <a name="next-steps"></a>Sonraki adımlar

* [Olay çözümleme ve görselleştirme Application Insights ile](service-fabric-diagnostics-event-analysis-appinsights.md)
* [Olay çözümleme ve OMS Görselleştirme](service-fabric-diagnostics-event-analysis-oms.md)
* [EventFlow belgeleri](https://github.com/Azure/diagnostics-eventflow)