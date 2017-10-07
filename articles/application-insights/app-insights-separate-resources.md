---
title: "aaaSeparating telemetri geliştirme, test ve yayın Azure Application Insights'ta | Microsoft Docs"
description: "Geliştirme, test ve üretim Damgalar için doğrudan telemetri toodifferent kaynaklar."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 578e30f0-31ed-4f39-baa8-01b4c2f310c9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: a294c8c70f46d7c29b460461c3494c83e13a0cbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="separating-telemetry-from-development-test-and-production"></a>Geliştirme, Test ve üretim telemetri ayırma

Bir web uygulaması sonraki sürümü hello geliştirirken hello yukarı toomix istemediğiniz [Application Insights](app-insights-overview.md) hello yeni sürümü ve hello önceden yayımlanan sürümü telemetrisinden. tooavoid Karışıklığı önlemek için farklı geliştirme gönderme hello telemetrisinden tooseparate Application Insights kaynakları ayrı izleme anahtarı (ikeys) ile aşamaları. toomake, bir sürüm olarak daha kolay toochange hello izleme anahtarını yararlı tooset hello ikey hello yapılandırma dosyasında yerine kodda olması bir aşamada tooanother taşır. 

(Sisteminiz bir Azure bulut hizmeti ise var. [ayrı ikeys ayarlama başka bir yöntem](app-insights-cloudservices.md).)

## <a name="about-resources-and-instrumentation-keys"></a>Kaynaklar ve izleme anahtarı hakkında

Web uygulamanız için Application Insights izleme işlevini ayarlama Application Insights oluşturduğunuzda *kaynak* Microsoft azure'da. Bu kaynak hello sipariş toosee Azure portalında açın ve hello telemetriyi uygulamanızdan toplanan analiz. Merhaba kaynak tarafından tanımlanan bir *izleme anahtarını* (ikey). Merhaba yüklediğinizde Application Insights toomonitor uygulamanızı paketleme, burada toosend hello telemetri bilir şekilde, hello izleme anahtarı ile yapılandırabilirsiniz.

Genellikle toouse ayrı kaynaklar ya da tek bir paylaşılan kaynağa farklı senaryolarda seçin:

* Farklı, bağımsız uygulamalar - her uygulama için ayrı kaynak ve ikey kullanın.
* Birden çok bileşenleri ya da bir iş uygulaması - rolleri kullanmak bir [tek bir paylaşılan kaynak](app-insights-monitor-multi-role-apps.md) tüm bileşen uygulamaları hello için. Telemetri filtre veya hello cloud_RoleName özelliği tarafından ayrılmış.
* Geliştirme, Test ve yayın - ayrı kaynak ve ikey sürümlerini 'damga' ın hello veya üretim aşaması için kullanın.
* A | B testi - tek bir kaynak kullanın. TelemetryInitializer tooadd hello çeşitleri tanımlayan bir özellik toohello telemetri oluşturun.


## <a name="dynamic-ikey"></a>Dinamik izleme anahtarı

toomake kolaylaştırır toochange hello ikey hello kod olarak üretim aşamaları arasında taşır yerine kodda hello yapılandırma dosyasında ayarlayın.

Başlangıç anahtarı başlatma yöntemini, bir ASP.NET hizmetinde global.aspx.cs gibi ayarlayın:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey = 
          // - for example -
          WebConfigurationManager.AppSettings["ikey"];
      ...

Bu örnekte, hello web yapılandırma dosyası farklı sürümlerini hello ikeys hello farklı kaynaklar yerleştirilir. -Hello yayın komut dosyasının bir parçası yapabileceğiniz - takası hello web yapılandırma dosyasını hello hedef kaynak değiştireceksiniz.

### <a name="web-pages"></a>Web sayfaları
Merhaba, uygulamanızın web sayfalarında de Hello iKey kullanıldığında [hello hızlı başlangıç dikey penceresinden aldığınız betik](app-insights-javascript.md). Harfi harfine hello komut dosyasına kodlama yerine, hello sunucu durumundan oluşturur. Örneğin, bir ASP.NET uygulamasında:

*Razor JavaScript'te*

    <script type="text/javascript">
    // Standard Application Insights web page script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      "@Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="create-additional-application-insights-resources"></a>Ek Application Insights kaynakları oluşturun
tooseparate telemetri farklı Damgalar (dev/test/üretim) hello ya da farklı uygulama bileşenleri için aynı bileşen toocreate yeni bir Application Insights kaynağı sahip.

Merhaba, [portal.azure.com](https://portal.azure.com), Application Insights kaynağı ekleyin:

![Yeni, Application Insights öğesine tıklayın](./media/app-insights-separate-resources/01-new.png)

* **Uygulama türü** hello genel bakış dikey penceresinde ve hello özellikler kullanılabilir Görünenleri etkiler [ölçüm Gezgini](app-insights-metrics-explorer.md). Uygulama, türünü görmüyorsanız, web sayfaları için hello web türlerinden birini seçin.
* **Kaynak grubu** gibi özellikleri yönetmek için kullanışlı olan [erişim denetimi](app-insights-resources-roles-access-control.md). Ayrı kaynak grupları, geliştirme, test ve üretim için kullanabilirsiniz.
* **Abonelik** ödeme hesabınız azure'da.
* **Konum** burada biz verilerinizi tutmak olduğu. Şu anda değiştirilemez. 
* **Toodashboard ekleme** kaynağınız için hızlı erişim kutucuğu, Azure giriş sayfasında koyar. 

Merhaba kaynak oluşturma birkaç saniye sürer. Bu yapıldığında, bir uyarı görürsünüz.

(Yazabileceğiniz bir [PowerShell Betiği](app-insights-powershell-script-create-resource.md) toocreate kaynak otomatik olarak.)

### <a name="getting-hello-instrumentation-key"></a>Merhaba izleme anahtarı alma
Merhaba izleme anahtarı oluşturduğunuz hello kaynak tanımlar. 

![Essentials'ı tıklatın, hello izleme anahtarı, CTRL + C](./media/app-insights-separate-resources/02-props.png)

Merhaba izleme anahtarı ihtiyacınız tüm hello kaynakları toowhich uygulamanızı verileri gönderir.

## <a name="filter-on-build-number"></a>Yapı numarası filtre
Uygulamanızı yeni bir sürümü yayımladığınızda, toobe mümkün tooseparate hello telemetri farklı yapılandırmalardan isteyeceksiniz.

Filtre uygulayabilirsiniz şekilde hello uygulama Version özelliği ayarlayabilirsiniz [arama](app-insights-diagnostic-search.md) ve [ölçüm Gezgini](app-insights-metrics-explorer.md) sonuçları.

![Bir özellik filtreleme](./media/app-insights-separate-resources/050-filter.png)

Merhaba uygulama Version özelliği ayarlama birkaç farklı yöntem vardır.

* Doğrudan ayarlayın:

    `telemetryClient.Context.Component.Version = typeof(MyProject.MyClass).Assembly.GetName().Version;`
* Bu satırda sarmalamak bir [telemetri Başlatıcı](app-insights-api-custom-events-metrics.md#defaults) TelemetryClient hepsinin tutarlı bir şekilde ayarlanan tooensure.
* [ASP.NET] Set hello sürümünde `BuildInfo.config`. Merhaba web modülü hello sürüm hello BuildLabel düğümünden yukarı seçer. Bu dosyayı projenize eklemek ve tooset hello her zaman Kopyala özelliği Çözüm Gezgini'nde unutmayın.

    ```XML

    <?xml version="1.0" encoding="utf-8"?>
    <DeploymentEvent xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/VisualStudio/DeploymentEvent/2013/06">
      <ProjectName>AppVersionExpt</ProjectName>
      <Build type="MSBuild">
        <MSBuild>
          <BuildLabel kind="label">1.0.0.2</BuildLabel>
        </MSBuild>
      </Build>
    </DeploymentEvent>

    ```
* [ASP.NET] BuildInfo.config Msbuild'de otomatik olarak oluşturur. toodo Bu, birkaç satırları tooyour ekleme `.csproj` dosyası:

    ```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
    ```

    Bu adlı bir dosya oluşturur *yourProjectName*. BuildInfo.config. hello yayımlama işlemi tooBuildInfo.config yeniden adlandırır.

    Visual Studio ile derlerken hello yapı etiketi yer tutucu (AutoGen_...) içerir. Ancak MSBuild ile yapılandırıldığında hello doğru sürüm numarasıyla doldurulur.

    kümesi hello sürümünü tooallow MSBuild toogenerate sürüm numaralarını, ister `1.0.*` AssemblyReference.cs içinde

## <a name="version-and-release-tracking"></a>Sürüm ve sürüm izleme
tootrack hello uygulama sürümü, emin olun `buildinfo.config` Microsoft Build Engine işlem tarafından oluşturulur. .csproj dosyanızda şunları ekleyin:  

```XML

    <PropertyGroup>
      <GenerateBuildInfoConfigFile>true</GenerateBuildInfoConfigFile>    <IncludeServerNameInBuildInfo>true</IncludeServerNameInBuildInfo>
    </PropertyGroup>
```

Merhaba yapı bilgisi mevcut olduğunda hello Application Insights web modülü otomatik olarak ekler **uygulama sürümü** telemetri özellik tooevery öğesi olarak. Böylece toofilter sürümü tarafından gerçekleştirdiğinizde [tanılama aramaları](app-insights-diagnostic-search.md), veya ne zaman, [ölçümleri keşfedin](app-insights-metrics-explorer.md).

Ancak, yalnızca Microsoft Build Engine, hello geliştirici tarafından değil, Visual Studio'da derleme hello hello derleme sürüm numarası oluşturan dikkat edin.

### <a name="release-annotations"></a>Sürüm ek açıklamaları
Visual Studio Team Services kullanıyorsanız, şunları yapabilirsiniz [bir ek açıklama işaretçisi almak](app-insights-annotations.md) yeni bir sürüm yayın her tooyour grafikler eklendi. Görüntü aşağıdaki Merhaba, bu işaret nasıl göründüğünü gösterir.

![Bir grafikteki örnek sürüm ek açıklamasının ekran görüntüsü](./media/app-insights-asp-net/release-annotation.png)
## <a name="next-steps"></a>Sonraki adımlar

* [Birden çok rol için paylaşılan kaynakları](app-insights-monitor-multi-role-apps.md)
* [Telemetri Başlatıcı toodistinguish A oluşturun | B çeşitleri](app-insights-api-filtering-sampling.md#add-properties)
