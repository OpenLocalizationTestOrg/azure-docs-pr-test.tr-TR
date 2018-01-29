---
title: "Application Insights ile Azure Service Fabric olay çözümleme | Microsoft Docs"
description: "Görselleştirme ve izleme ve tanılama Azure Service Fabric kümeleri için Application Insights kullanarak olayları analiz etme hakkında bilgi edinin."
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
ms.date: 10/15/2017
ms.author: dekapur
ms.openlocfilehash: 34f14f42150e46edae2d1352827f96a411117a62
ms.sourcegitcommit: a7c01dbb03870adcb04ca34745ef256414dfc0b3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/17/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>Olay çözümleme ve görselleştirme Application Insights ile

Azure Application Insights, uygulama izleme ve tanılama için genişletilebilir bir platformdur. Uyarı seçenekleri de dahil olmak üzere daha fazla otomatik ve güçlü analytics ve aracı, özelleştirilebilir bir Pano ve görselleştirmeleri sorgulama içerir. Bu izleme için önerilen platform ve Service Fabric uygulamaları ve Hizmetleri için tanılama olur.

## <a name="setting-up-application-insights"></a>Application Insights ayarlama

### <a name="creating-an-ai-resource"></a>AI kaynak oluşturma

Azure Marketi'nde baş üzerinden bir AI kaynak oluşturmak ve "Application Insights" için arama yapmak için. Bunu ("Web + mobil" kategorisi altında olduğu) ilk çözümü olarak gösterilmesi gerekir. Tıklatın **oluşturma** zaman, arıyor doğru kaynak (yolunuzu aşağıdaki görüntü eşleştiğini onaylayın).

![Yeni Application Insights kaynağı](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

Doğru kaynak sağlamak için bazı bilgileri doldurmanızı gerekecektir. İçinde *uygulama türü* alanını kullan "ASP.NET web uygulaması", Service Fabric birini kullanıyorsanız modellerini programlama veya küme için bir .NET uygulaması yayımlama. Konuk yürütülebilir dosyalar ve kapsayıcıları dağıtacaksanız "Genel" kullanın. "ASP.NET web uygulaması" genel olarak, varsayılan seçeneklerinizi gelecekte açık tutmak için. Adı tercihinizi kadar olduğunu ve kaynak grubu ve abonelik kaynak değiştirilebilir dağıtım sonrası. AI kaynağınız kümeniz ile aynı kaynak grubunda olduğunu öneririz. Daha fazla bilgiye ihtiyacınız varsa, lütfen bakın [Application Insights kaynağı oluşturma](../application-insights/app-insights-create-new-resource.md)

Olay toplama aracıyla AI yapılandırmak için AI izleme anahtarı gerekir. AI kaynağınız (dağıtım doğrulandıktan sonra birkaç dakika sürer) ayarladıktan sonra kendisine gidin ve bulmak **özellikleri** sol gezinti çubuğunda bölümü. Yeni bir dikey pencere gösteren açılır bir *izleme ANAHTARINI*. Abonelik veya kaynak grubu kaynağının adını değiştirmeniz gerekiyorsa, bunu burada de yapılabilir.

### <a name="configuring-ai-with-wad"></a>AI WAD ile yapılandırma

>[!NOTE]
>Bu yalnızca şu anda Windows kümeleri için geçerlidir.

İçinde ayrıntılı olarak WAD yapılandırma AI havuz ekleyerek elde Azure AI WAD veri göndermek için iki birincil yolla [bu makalede](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>Azure portalında bir küme oluştururken, bir AI izleme anahtarını ekleyin

![Bir AIKey ekleme](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

"Açık" tanılama etkinleştirdiyseniz bir küme oluştururken, bir uygulama Insights izleme anahtarı girmek için isteğe bağlı bir alan gösterir. AI IKey burada yapıştırırsanız, AI havuz otomatik olarak sizin için kümenizi dağıtmak için kullanılan Resource Manager şablonu olarak yapılandırılır.

#### <a name="add-the-ai-sink-to-the-resource-manager-template"></a>AI havuz için Resource Manager şablonu Ekle

"WadCfg" Resource Manager şablonu içinde aşağıdaki iki değişiklikler dahil ederek "Havuz" ekleyin:

1. Havuz yapılandırma, bildirme hemen sonra ekleyin `DiagnosticMonitorConfiguration` tamamlanır:

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. Havuz dahil `DiagnosticMonitorConfiguration` dosyasında aşağıdaki satırı ekleyerek `DiagnosticMonitorConfiguration` , `WadCfg` (önceki `EtwProviders` bildirilir):

    ```json
    "sinks": "applicationInsights"
    ```

Her iki kod parçacıkları yukarıdaki, adı "Applicationınsights" havuz açıklamak için kullanıldı. Bu bir gereklilik değildir ve havuz adı "havuzlarını" dahil olduğu sürece, herhangi bir dize adı ayarlayabilirsiniz.

Şu anda, küme günlüklerinden AI'ın günlük Görüntüleyici içindeki olarak görünecektir. Çoğu platformdan gelen izlemeleri düzeyi "Bilgilendirici" olduğundan, sadece "Kritik" veya "Error" türünde günlükleri göndermek için havuz yapılandırmasını değiştirme de düşünebilirsiniz. Bu, havuz için "Kanalları" ekleyerek şekilde yapılabilir [bu makalede](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

>[!NOTE]
>Yanlış bir AI IKey portalında veya Resource Manager şablonunu kullanırsanız, gerekir el ile kayıt anahtarını değiştirin ve kümeyi güncelleştirmek / yeniden dağıtmanız. 

### <a name="configuring-ai-with-eventflow"></a>AI EventFlow ile yapılandırma

Birleşik olaylarına EventFlow kullanıyorsanız, içeri aktarmak emin olun `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet paketi. Aşağıdakiler dahil edilecek sahip *çıkarır* bölümünü *eventFlowConfig.json*:

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace the following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

Yanı sıra, filtrelerinizi gerekli değişiklikleri yapın (birlikte ilgili kendi NuGet paketlerini) başka bir giriş eklemek emin olun.

## <a name="aisdk"></a>AI. SDK'SI

Tanılama ve izleme, daha modüler bir yaklaşım için başka bir deyişle, çıkışları EventFlow değiştirmek istiyorsanız, hiçbir değişiklik, gerçek araçları gerektirir sağlarlar çünkü EventFlow ve WAD toplama çözümler olarak kullanılması genellikle önerilir, yalnızca basit değişiklik yapılandırma dosyası. Ancak, Application Insights kullanarak yatırım karar ve farklı bir platform için değişmesi olasılığı olan değil, olay toplama ve AI için göndermek için AI'ın yeni bir SDK kullanarak görünmelidir. Bu, verileriniz için AI göndermek için EventFlow yapılandırmak artık olur, ancak bunun yerine ApplicationInsight'ın Service Fabric NuGet paketini yükleyecek anlamına gelir. Pakette Ayrıntılar bulunabilir [burada](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).

[Application Insights mikro ve kapsayıcıları için desteği](https://azure.microsoft.com/app-insights-microservices/) bazı gösterir (üzerinde hala halen beta) çalışan yeni özelliklerini hangi izin AI ile daha zengin Giden kutusu izleme seçeneğiniz vardır. Bu bağımlılık izleme (bir AppMap tüm hizmetleri ve uygulamaları bir küme ve bunların arasındaki iletişimi oluşturulmasında kullanılan) ve daha iyi bağıntı hizmetlerinizin (daha iyi bir sorun iş akışındaki yerini tam olarak belirtmekte yardımcı olur'ten gelen izlemeleri içerir bir uygulama veya hizmet).

.NET geliştirme ve büyük olasılıkla Service Fabric'ın programlama modelleri ve bu olay ve günlük verilerini çözümleme ve görselleştirme için platform olarak AI kullanmak istiyorum bazıları kullanacaklardır, ardından AI SDK yol izleme ve diagnos olarak aracılığıyla Git öneririz ı eşleştir iş akışı. Okuma [bu](../application-insights/app-insights-asp-net-more.md) ve [bu](../application-insights/app-insights-asp-net-trace-logs.md) AI toplamak ve günlüklerinizi görüntülemek için kullanmaya başlamak için.

## <a name="navigating-the-ai-resource-in-azure-portal"></a>Azure portalında AI kaynak gezinme

Olayları ve günlükleri için bir çıktı olarak AI yapılandırdıktan sonra bilgi AI kaynağınız birkaç dakika içinde gösterilmeye başlamanız gerekir. AI kaynak panoya sürer AI kaynağa gidin. Tıklatın **arama** görev çubuğunda AI alınan son izlemelerini görmek ve aralarında filtreleyebilirsiniz.

*Ölçüm Gezgini* uygulamaları, hizmetleri ve küme raporlama ölçümleri temel özel panolar oluşturmak için yararlı bir araçtır. Bkz: [keşfetme ölçümleri Application ınsights'ta](../application-insights/app-insights-metrics-explorer.md) kendiniz toplama verileri temel alan için birkaç grafikleri ayarlamak için.

Tıklatarak **Analytics** burada olayları ve büyük kapsam ve isteğe bağlı olma izlemeleri sorgulayabilir uygulama Öngörüler Analytics portalına sürer. Şu anda hakkında daha fazla bilgiyi [Application Insights analizleri](../application-insights/app-insights-analytics.md).

## <a name="next-steps"></a>Sonraki adımlar

* [AI uyarıları ayarlama](../application-insights/app-insights-alerts.md) performans veya kullanımı değişiklikler hakkında bildirim almak için
* [Akıllı algılama Application ınsights'ta](../application-insights/app-insights-proactive-diagnostics.md) AI için olası performans sorunları sizi uyaracak şekilde telemetri gönderimini öngörülü bir analizini gerçekleştirir