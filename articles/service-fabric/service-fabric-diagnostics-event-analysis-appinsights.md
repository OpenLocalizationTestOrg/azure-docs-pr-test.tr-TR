---
title: "Service Fabric olay çözümleme Application Insights ile aaaAzure | Microsoft Docs"
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
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>Olay çözümleme ve görselleştirme Application Insights ile

Azure Application Insights, uygulama izleme ve tanılama için genişletilebilir bir platformdur. Uyarı seçenekleri de dahil olmak üzere daha fazla otomatik ve güçlü analytics ve aracı, özelleştirilebilir bir Pano ve görselleştirmeleri sorgulama içerir. Bu izleme için platform ve tanılama Service Fabric uygulamaları ve Hizmetleri için önerilen hello olur.

## <a name="setting-up-application-insights"></a>Application Insights ayarlama

### <a name="creating-an-ai-resource"></a>AI kaynak oluşturma

toocreate bir AI kaynak, toohello Azure Marketi ve "Application Insights" araması üzerinden head. Bunu hello ilk çözüm ("Web + mobil" kategorisi altında olduğu) olarak gösterilmesi gerekir. Tıklatın **oluşturma** zaman, arıyor hello sağ kaynakta (yolunuzu hello resimde eşleştiğini onaylayın).

![Yeni Application Insights kaynağı](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

Bazı bilgiler tooprovision hello kaynak çıkışı toofill doğru gerekir. Merhaba, *uygulama türü* alanını kullan "ASP.NET web uygulaması", Service Fabric birini kullanıyorsanız modellerini programlama veya bir .NET uygulama toohello küme yayımlama. Konuk yürütülebilir dosyalar ve kapsayıcıları dağıtacaksanız "Genel" kullanın. Genel olarak, varsayılan toousing "ASP.NET web uygulaması" tookeep seçeneklerinizi hello gelecekteki açın. Merhaba adı tooyour tercih olduğunu ve hello kaynak grubu ve abonelik hello kaynak değiştirilebilir dağıtım sonrası. AI kaynağınız hello olduğunu öneririz, kümeniz ile aynı kaynak grubunda. Daha fazla bilgiye ihtiyacınız varsa, lütfen bakın [Application Insights kaynağı oluşturma](../application-insights/app-insights-create-new-resource.md)

Olay toplama aracıyla hello AI izleme anahtarını tooconfigure AI gerekir. AI kaynağınız (Merhaba dağıtım doğrulandıktan sonra birkaç dakika sürer) ayarladıktan sonra tooit gidin ve hello bulur **özellikleri** hello sol gezinti çubuğunda bölümü. Yeni bir dikey pencere gösteren açılır bir *izleme ANAHTARINI*. Toochange hello abonelik veya kaynak grubu hello kaynağının gerekiyorsa, bunu burada de yapılabilir.

### <a name="configuring-ai-with-wad"></a>AI WAD ile yapılandırma

Hangi ayrıntılı biçimde açıklandığı gibi bir AI havuz toohello WAD yapılandırma ekleyerek elde toosend verilerden WAD tooAzure AI, birincil iki yolu vardır [bu makalede](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>Azure portalında bir küme oluştururken, bir AI izleme anahtarını ekleyin

![Bir AIKey ekleme](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

"Açık" tanılama etkinleştirdiyseniz bir küme oluştururken, bir isteğe bağlı alan tooenter bir uygulama Insights izleme anahtarı gösterir. AI IKey burada yapıştırırsanız hello AI havuz otomatik olarak kullanılan toodeploy olan hello Resource Manager şablonunda kümenizi yapılandırdığınız.

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a>Merhaba AI havuz toohello Resource Manager şablonu Ekle

Aşağıdaki iki değişiklikler hello dahil ederek "Havuz" Hello "WadCfg" Merhaba Resource Manager şablonu, ekleyin:

1. Merhaba havuz yapılandırma ekleyin:

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

2. Merhaba havuz hello "WadCfg" "DiagnosticMonitorConfiguration" satırında şu hello ekleyerek hello DiagnosticMonitorConfiguration şunlardır:

    ```json
    "sinks": "applicationInsights"
    ```

Her iki hello kod parçacıkları hello yukarıda kullanılan toodescribe hello havuz adı "Applicationınsights" içindeydi. Bu zorunlu değildir ve "havuzlarını içinde" hello havuz hello adını dahil olduğu sürece, başlangıç ad tooany dizesi ayarlayabilirsiniz.

Şu anda hello küme günlüklerinden AI'ın günlük Görüntüleyici içindeki olarak görünecektir. Çoğu hello platformundan gelen hello izlemeleri düzeyi "Bilgilendirici" olduğundan, türü "Kritik" veya "Error" Merhaba havuz yapılandırma tooonly gönderme günlükleri değiştirme de düşünebilirsiniz. Bu "Kanalları" tooyour havuz ekleyerek şekilde yapılabilir [bu makalede](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md).

>[!NOTE]
>Yanlış bir AI IKey portalında veya Resource Manager şablonunu kullanırsanız, toomanually hello anahtarını değiştirin ve hello küme güncelleştirme / yeniden dağıtmanız gerekir. 

### <a name="configuring-ai-with-eventflow"></a>AI EventFlow ile yapılandırma

EventFlow tooaggregate olayları kullanıyorsanız emin tooimport hello olun `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet paketi. Merhaba aşağıdaki sahip hello dahil toobe *çıkarır* hello bölümünü *eventFlowConfig.json*:

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

Filtrelerinizi içinde emin toomake hello gerekli değişiklikleri yapın gibi başka bir giriş (birlikte ilgili kendi NuGet paketleri) içerir.

## <a name="aisdk"></a>AI. SDK'SI

Toouse EventFlow genellikle önerilir ve WAD toplama çözümler olarak çünkü için daha modüler bir yaklaşım toodiagnostics sağlarlar ve EventFlow, çıkışlarından toochange istiyorsanız, yani izleme, gerçek hiçbir değişiklik tooyour gerektirir İzleme, yalnızca bir basit bir değişiklikle tooyour yapılandırma dosyası. Ancak, Application Insights kullanarak tooinvest karar verin ve büyük olasılıkla toochange tooa farklı platform olmayan varsa, olay toplama ve tooAI göndermek için AI'ın yeni bir SDK kullanarak görünmelidir. Bu tooconfigure EventFlow toosend veri tooAI artık yoktur, ancak bunun yerine hello ApplicationInsight'ın Service Fabric NuGet paketini yükleyecek anlamına gelir. Ayrıntılar hello paketinizdeki bulunabilir [burada](https://github.com/Microsoft/ApplicationInsights-ServiceFabric).

[Application Insights mikro ve kapsayıcıları için desteği](https://azure.microsoft.com/app-insights-microservices/) bazı gösterir (üzerinde hala halen beta) çalışan hello yeni özellikleri, hangi izin toohave daha zengin Giden kutusu izleme seçeneklerini AI ile. Bu bağımlılık izleme (bir AppMap, tüm hizmet ve uygulamaların küme ve hello iletişimde aralarında oluşturulmasında kullanılan) ve daha iyi bağıntı hizmetlerinizin (daha iyi bir sorunu hello yerini tam olarak belirtmekte yardımcı olur'ten gelen izlemeleri içerir İş akışı bir uygulama veya hizmet).

.NET geliştirme ve olasılığı olması bazı Service Fabric'ın programlama modeli kullanarak ve izlemenizi olarak AI SDK rota hello Git öneririz sonra olay ve günlük verilerini çözümleme ve görselleştirme için platformunuz olarak istekli toouse AI demektir ve Tanılama iş akışı. Okuma [bu](../application-insights/app-insights-asp-net-more.md) ve [bu](../application-insights/app-insights-asp-net-trace-logs.md) tooget AI toocollect kullanmaya ve günlüklerinizi görüntüler.

## <a name="navigating-hello-ai-resource-in-azure-portal"></a>Azure portalında Hello AI kaynak gezinme

Olayları ve günlükleri için bir çıktı olarak AI yapılandırdıktan sonra bilgi tooshow AI kaynağınız birkaç dakika içinde Başlat. Toohello AI kaynak Panosu sürer toohello AI kaynak gidin. Tıklatın **arama** alınan hello AI görev toosee hello son izlemeleri ve toobe mümkün toofilter gezinebilirsiniz.

*Ölçüm Gezgini* uygulamaları, hizmetleri ve küme raporlama ölçümleri temel özel panolar oluşturmak için yararlı bir araçtır. Bkz: [keşfetme ölçümleri Application ınsights'ta](../application-insights/app-insights-metrics-explorer.md) tooset kendiniz birkaç grafiklerde yukarı dayalı toplama hello verileri.

Tıklatarak **Analytics** burada olayları ve büyük kapsam ve isteğe bağlı olma izlemeleri sorgulayabilir toohello uygulama Öngörüler Analytics portalı sürer. Şu anda hakkında daha fazla bilgiyi [Application Insights analizleri](../application-insights/app-insights-analytics.md).

## <a name="next-steps"></a>Sonraki adımlar

* [AI uyarıları ayarlama](../application-insights/app-insights-alerts.md) performans veya kullanım değişiklikleri hakkında bildirimde toobe
* [Akıllı algılama Application ınsights'ta](../application-insights/app-insights-proactive-diagnostics.md) tooAI toowarn hello telemetri gönderimini öngörülü bir analizini gerçekleştirir, olası performans sorunları
