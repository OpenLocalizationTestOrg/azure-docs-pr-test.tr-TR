---
title: "aaaAzure Application Insights birden çok bileşenleri, mikro ve kapsayıcıları için desteği | Microsoft Docs"
description: "Birden çok bileşenleri veya performans ve kullanım için rolleri oluşur uygulamaları izleme."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a>Application Insights (Önizleme) ile birden çok bileşen uygulamaları izleme

Birden çok sunucu bileşenlerini, roller veya hizmetlerle oluşur uygulamaları izleyebilirsiniz [Azure Application Insights](app-insights-overview.md). Merhaba durumunu hello bileşenler ve aralarındaki ilişkilerin hello tek bir uygulama harita üzerinde görüntülenir. Tek tek işlemleri otomatik HTTP bağıntı ile birden çok bileşeni aracılığıyla izleyebilirsiniz. Kapsayıcı tanılama tümleşiktir ve uygulama telemetri ile ilişkili. Tek bir Application Insights kaynağı hello bileşenlerinin tümünü uygulamanız için kullanın. 

![Birden çok bileşen uygulama eşlemesi](./media/app-insights-monitor-multi-role-apps/app-map.png)

'Bileşeni' kullanırız burada toomean büyük bir uygulama, herhangi bir işlevsel parçası. Örneğin, tipik iş uygulaması tooone Konuşmayı web tarayıcısında çalışan istemci kodunun oluşabilir veya hizmetleri sırayla geri kullanan daha fazla web uygulama hizmetleri bitemez. Sunucu bileşenleri barındırılan şirket içi hello bulutta üzerinde olabilir ya da Azure web ve çalışan rolleri olabilir veya kapsayıcılarında Docker veya Service Fabric gibi çalışabilir. 

### <a name="sharing-a-single-application-insights-resource"></a>Tek bir Application Insights kaynağı paylaşma 

Merhaba burada anahtar tekniği olan, uygulama toohello her bileşenin toosend telemetrisinden aynı Application Insights kaynağı ancak kullanım hello `cloud_RoleName` özelliği toodistinguish bileşenleri gerektiğinde. Merhaba Application Insights SDK'sı ekler hello `cloud_RoleName` özelliği toohello telemetri bileşenleri yayma. Örneğin, hello SDK web sitesi adı ya da hizmet rol adı toohello ekleyeceksiniz `cloud_RoleName` özelliği. Bu değer bir telemetryinitializer ile geçersiz kılabilirsiniz. Merhaba uygulama eşlemesi kullanan hello `cloud_RoleName` özelliği tooidentify hello bileşenleri hello haritaya.

Hakkında daha fazla bilgi için hello geçersiz kılma `cloud_RoleName` özelliği bakın [özellikleri ekleyin: ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer).  

Bazı durumlarda, bu uygun olmayabilir ve toouse ayrı kaynaklar bileşenleri farklı kullanıcı grupları için tercih edebilirsiniz. Örneğin, yönetim veya faturalandırma için toouse farklı kaynaklar gerekebilir. Ayrı kaynaklarını kullanan tüm hello bileşenleri tek bir uygulama haritada görüntülenmelerini görmüyorum anlamına gelir; ve bileşenler arasında sorgulanamıyor [Analytics](app-insights-analytics.md). Tooset hello ayrı kaynakları da vardır.

Bu uyarısıyla birlikte, bu belgenin hello kalan birden çok bileşenleri tooone Application Insights kaynağı toosend verileri istediğiniz varsayıyoruz.

## <a name="configure-multi-component-applications"></a>Birden çok bileşen uygulamaları yapılandır

birden çok bileşen uygulama tooget eşleme, bu hedefleri tooachieve gerekir:

* **Merhaba en son sürüm öncesi yüklemek** her bileşenin hello uygulamasının Application Insights paketinde. 
* **Tek bir Application Insights kaynağı paylaşma** tüm uygulama bileşenleri hello için.
* **Birden çok rol uygulama eşlemesi etkinleştirmek** hello önizlemeleri dikey penceresinde.

Her bileşen türü için hello uygun yöntemi kullanarak, uygulamanızın yapılandırın. ([ASP.NET](app-insights-asp-net.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), [JavaScript](app-insights-javascript.md).)

### <a name="1-install-hello-latest-pre-release-package"></a>1. Merhaba en son sürüm öncesi paketini yükle

Güncelleştirme veya hello projesinde her sunucu bileşeni için hello kullanılıyor Öngörüler paketlerini yükleyin. Visual Studio kullanıyorsanız:

1. Bir projeye sağ tıklayın ve seçin **NuGet paketlerini Yönet**. 
2. Seçin **dahil et**.
3. Application Insights paketleri güncelleştirmelerinde görünmüyorsa, bunları seçin. 

    Aksi takdirde, göz atın ve hello uygun paket yükleyin:
    
    * Microsoft.ApplicationInsights.WindowsServer
    * Microsoft.ApplicationInsights.ServiceFabric - Konuk yürütülebilir dosyalar ve Docker kapsayıcıları içinde bir Service Fabric uygulaması çalıştıran çalışan bileşenleri için
    * Microsoft.ApplicationInsights.ServiceFabric.Native - ServiceFabric uygulamaları güvenilir hizmetler için
    * Docker içinde Kubernetes üzerinde çalışan bileşenleri için Microsoft.ApplicationInsights.Kubernetes

### <a name="2-share-a-single-application-insights-resource"></a>2. Tek bir Application Insights kaynağı paylaşma

* Visual Studio'da bir projeye sağ tıklayın ve seçin **yapılandırma Application Insights**, veya **Application Insights > yapılandırma**. Merhaba ilk projeniz için hello Sihirbazı toocreate Application Insights kaynağı kullanın. Sonraki projeleri için aynı kaynak Seç hello.
* Application Insights menü ise, el ile yapılandırın:

   1. İçinde [Azure portal](https://portal,azure.com), başka bir bileşen için önceden oluşturulmuş hello Application Insights kaynağı açın.
   2. Merhaba genel bakış dikey penceresinde, açık hello Essentials açılan sekmesi ve kopyalama hello **izleme anahtarı.**
   3. Projenizdeki Applicationınsights.config açın ve Ekle:`<InstrumentationKey>your copied key</InstrumentationKey>`

![Merhaba araçları anahtar toohello .config dosyasını kopyalayın](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a>3. Birden çok rol uygulama eşlemesi etkinleştir

Hello Azure portal, uygulamanız için hello kaynak açın. Merhaba önizlemeleri dikey penceresinde, etkinleştirme *birden çok rol uygulama eşlemesi*.

### <a name="4-enable-docker-metrics-optional"></a>4. Docker ölçümleri (isteğe bağlı) etkinleştir 

Bir bileşen bir Azure Windows VM üzerinde barındırılan bir Docker çalıştırıyorsa, ek ölçümler hello kapsayıcıdan toplayabilirsiniz. Bu konuda eklemek, [Azure tanılama](../monitoring-and-diagnostics/azure-diagnostics.md) yapılandırma dosyası:

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a>Cloud_RoleName tooseparate bileşenleri kullanma

Merhaba `cloud_RoleName` ekli tooall telemetri bir özelliktir. Merhaba telemetri kaynaklanan hello bileşen - hello rol veya hizmete - tanımlar. (Bu, aynı paralel olarak birden çok sunucu işlemlerini veya makinelerde çalışan aynı roller ayıran cloud_RoleInstance olarak hello yok olur.)

Merhaba Portalı'nda, filtre ya da bu özelliği kullanan telemetrinizi segmentlere. Bu örnekte, hello hataları dikey penceresinde hello CRM API arka uç hatalarından çıkışı filtreleme hello ön uç web hizmetinden, filtrelenmiş tooshow yalnızca bilgiler şunlardır:

![Bulut rolü adıyla kesimli ölçüm grafik](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a>Bileşenleri arasında izleme işlemleri

Bir bileşen tooanother, tek bir işlem işlenirken yapılan hello çağrıları alanından izleyebilirsiniz.


![İşlem için telemetri Göster](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

Bu işlem için telemetri tooa bağıntılı listesi kullanılarak hello ön uç web sunucusunu ve hello arka uç API'si üzerinden tıklatın:

![Bileşenler genelinde arama](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a>Sonraki adımlar

* [Geliştirme, Test ve üretim ayrı telemetri](app-insights-separate-resources.md)
