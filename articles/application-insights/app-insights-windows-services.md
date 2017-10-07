---
title: "aaaAzure için Application Insights Windows server ve çalışan rolleri | Microsoft Docs"
description: "Merhaba Application Insights SDK'sı tooyour ASP.NET uygulama tooanalyze kullanımını, kullanılabilirliğini ve performansını el ile ekleyin."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 106ba99b-b57a-43b8-8866-e02f626c8190
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 64643ef637195d10f87fc6020a77169bca66c1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-configure-application-insights-for-net-applications"></a>.NET uygulamaları için Application Insights’ı el ile yapılandırma

Yapılandırabileceğiniz [Application Insights](app-insights-overview.md) toomonitor çok çeşitli uygulamaları veya uygulama rollerini, bileşenleri veya mikro. Web uygulamaları ve hizmetleri için, Visual Studio [tek adımlı yapılandırma](app-insights-asp-net.md) sunar. Arka uç sunucu rolleri veya masaüstü uygulamaları gibi diğer .NET uygulaması türleri için Application Insights’ı el ile yapılandırabilirsiniz.

![Örnek performans izleme grafikleri](./media/app-insights-windows-services/10-perf.png)

#### <a name="before-you-start"></a>Başlamadan önce

Gerekenler:

* Bir abonelik çok[Microsoft Azure](http://azure.com). Merhaba sahibi ekibinizin ve kuruluşunuzun bir Azure aboneliğiniz varsa, tooit, ekleyebilir kullanarak, [Microsoft hesabı](http://live.com).
* Visual Studio 2013 veya üstü.

## <a name="add"></a>1. Application Insights kaynağı seçme

Burada, veriler toplanır ve hello Azure portalında görüntülenen Hello 'kaynak' değil. Toodecide gerekip gerekmediği toocreate yeni bir ya da mevcut bir paylaşabilirsiniz.

### <a name="part-of-a-larger-app-use-existing-resource"></a>Daha büyük bir uygulamanın parçası: Var olan kaynağı kullanma

Web uygulamanız - Örneğin, bir ön uç web uygulaması ve bir veya daha fazla arka uç hizmetlerinin - çeşitli bileşenleri sahip sonra tüm hello bileşenleri toohello telemetri göndermelisiniz aynı kaynak. Bu tek bir uygulama haritada görüntülenmelerini toobe etkinleştirmek ve olası tootrace bir bileşen tooanother isteğinden yapar.

Bu nedenle, bu uygulamanın diğer bileşenleri izliyorsanız sonra yalnızca kullanım hello aynı kaynak.

Merhaba kaynak hello açmak [Azure portal](https://portal.azure.com/). 

### <a name="self-contained-app-create-a-new-resource"></a>Kendi içinde uygulama: Yeni bir kaynak oluşturma

Merhaba yeni uygulama ilgisiz tooother uygulamalar varsa, kendi kaynak olmalıdır.

İçinde toohello oturum [Azure portal](https://portal.azure.com/)ve yeni bir Application Insights kaynağı oluşturun. ASP.NET hello uygulama türü olarak seçin.

![Yeni, Application Insights öğesine tıklayın](./media/app-insights-windows-services/01-new-asp.png)

uygulama türü Hello seçimi hello kaynak dikey pencerelerinin varsayılan içeriğini hello ayarlar.

## <a name="2-copy-hello-instrumentation-key"></a>2. Merhaba izleme anahtarını kopyalama
başlangıç anahtarı hello kaynak tanımlar. En kısa sürede hello SDK'sı, sıra toodirect veri toohello kaynak de yüklemeniz.

![Özellikler'i tıklatın, başlangıç anahtarı seçin ve ctrl + C tuşlarına basın](./media/app-insights-windows-services/02-props-asp.png)

## <a name="sdk"></a>3. Uygulamanızda Hello Application Insights paketini yükle
Yükleme ve yapılandırma hello Application Insights paketini hello platform üzerinde çalıştığınız bağlı olarak değişir. 

1. Visual Studio’da projenize sağ tıklayıp **NuGet Paketlerini Yönet**’i seçin.
   
    ![Merhaba projesine sağ tıklayın ve Nuget paketlerini Yönet seçin](./media/app-insights-windows-services/03-nuget.png)
2. Windows server uygulamaları, "Microsoft.ApplicationInsights.WindowsServer." Merhaba Application Insights paketini yükle
   
    !["Application Insights" araması yapın](./media/app-insights-windows-services/04-ai-nuget.png)
   
    *Hangi sürüm?*

    Denetleme **dahil et** bizim en son özellikleri tootry istiyorsanız. Merhaba ilgili belgeleri veya blog ön sürümü gerekip gerekmediğini unutmayın.
    
    *Diğer paketleri kullanabilir miyim?*
   
    Evet. Kendi telemetrinizi yalnızca toouse hello API toosend isterseniz, "Microsoft.ApplicationInsights" seçin. Merhaba Windows Server paketi hello API artı bir dizi performans sayacı toplama ve bağımlılık izleme gibi diğer paketleri içerir. 

### <a name="tooupgrade-toofuture-package-versions"></a>tooupgrade toofuture paketi sürümleri
Biz hello SDK zaman tootime gelen yeni bir sürümü kullanıma.

tooupgrade tooa [hello paketinin yeni sürümü](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases/), NuGet paket yöneticisini yeniden açın ve yüklü paketleri filtreleyin. **Microsoft.ApplicationInsights.WindowsServer** ve **Yükselt**’i seçin.

Tüm özelleştirmeler tooApplicationInsights.config yaptıysanız, yükseltme ve daha sonra değişikliklerinizi hello yeni sürümle birleştirin önce bir kopyasını kaydedin.

## <a name="4-send-telemetry"></a>4. Telemetri gönderme
**Yalnızca hello API paket yüklediyseniz:**

* Kümesinde hello izleme anahtarını kodda, örneğin `main()`: 
  
    `TelemetryConfiguration.Active.InstrumentationKey = "` *anahtarınız* `";` 
* [Merhaba API kullanarak kendi telemetrinizi yazmanızı](app-insights-api-custom-events-metrics.md#ikey).

**Diğer Application Insights paketleri yüklediyseniz** tercih ederseniz, hello .config dosyası tooset hello izleme anahtarını kullanabilirsiniz:

* (Hangi NuGet yükleme hello tarafından eklendi) Applicationınsights.config düzenleyin. Bu, yalnızca kapanış etiketi hello önce ekleyin:
  
    `<InstrumentationKey>`*kopyaladığınız hello izleme anahtarını*`</InstrumentationKey>`
* Çözüm Gezgini'nde Applicationınsights.config Hello özelliklerini çok ayarlandığından emin olun**yapı eylemi içerik, kopya tooOutput dizin = kopyalama =**.

Çok istiyorsanız yararlı tooset hello izleme anahtarını kodda olduğu[farklı derleme yapılandırmaları için anahtar hello anahtar](app-insights-separate-resources.md). Kodda hello anahtar ayarlarsanız, tooset yok hello içinde `.config` dosya.

## <a name="run"></a> Projenizi çalıştırma
Kullanım hello **F5** toorun uygulamanız ve deneyin: birkaç telemetri açık farklı sayfaları toogenerate.

Visual Studio'da gönderilmiş hello etkinliklerin sayısını görürsünüz.

![Visual Studio’da olay sayımı](./media/app-insights-windows-services/appinsights-09eventcount.png)

## <a name="monitor"></a> Telemetrinizi görüntüleme
Toohello iade [Azure portal](https://portal.azure.com/) ve tooyour Application Insights kaynağı göz atın.

Merhaba genel bakış grafiklerinde veri arayın. İlk olarak yalnızca bir veya iki nokta görürsünüz. Örneğin:

![Toomore verilerine tıklatın](./media/app-insights-windows-services/12-first-perf.png)

Tıklatın herhangi grafik toosee ayrıntılı ölçümler. [Ölçümler hakkında daha fazla bilgi edinin.](app-insights-web-monitor-performance.md)

### <a name="no-data"></a>Veri yok mu?
* Birkaç telemetri oluşturması için farklı sayfaları açarak hello uygulamasını kullanın.
* Açık hello [arama](app-insights-diagnostic-search.md) döşeme, olayları tek tek toosee. Bazen biraz uzun tooget hello ölçümleri ardışık düzeninden olayları alır.
* Birkaç saniye bekleyin ve **Yenile**’ye tıklayın. Grafikler kendilerini düzenli olarak yeniler, ancak için bazı veri tooshow bekliyorsanız el ile yenileyebilirsiniz.
* Bkz. [Sorun giderme](app-insights-troubleshoot-faq.md).

## <a name="publish-your-app"></a>Uygulamanızı yayımlama
Şimdi veri birleştirdiğinizde uygulama tooyour sunucunuz veya tooAzure ve izleme hello dağıtın.

![Visual Studio toopublish uygulamanızı kullanın](./media/app-insights-windows-services/15-publish.png)

Hata ayıklama modunda çalıştırdığınızda telemetri görüntülenen verileri saniyeler içinde görmeniz gerekir böylece hello ardışık düzen üzerinden hızlandırılır. Uygulamanızı Sürüm yapılandırmasında dağıttığınızda veriler daha yavaş birikir.

### <a name="no-data-after-you-publish-tooyour-server"></a>Tooyour sunucu yayımladıktan sonra veri yok mu?
Sunucunuzun güvenlik duvarında giden trafik için bağlantı noktalarını açın. Bkz: [bu sayfayı](https://docs.microsoft.com/azure/application-insights/app-insights-ip-addresses) gerekli adreslerini hello listesi 

### <a name="trouble-on-your-build-server"></a>Derleme sunucunuzda sorun mu yaşıyorsunuz?
Lütfen [bu Sorun Giderme maddesine](app-insights-asp-net-troubleshoot-no-data.md#NuGetBuild) bakın.

> [!NOTE]
> Uygulamanız çok sayıda telemetri oluşturuyorsa hello Uyarlamalı örnekleme modülü olayların yalnızca bir temsilci fraksiyonunu göndererek toohello portal gönderilen hello birim otomatik olarak azaltır. Ancak, böylece ilgili olaylar arasında gezinebilirsiniz olayları, ilgili toohello aynı istekte seçili veya bir grup olarak işaretli değildir. 
> [Örnekleme hakkında bilgi edinin](app-insights-sampling.md).
> 
> 

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Sonraki adımlar
* [Daha fazla telemetri ekleme](app-insights-asp-net-more.md) tooget hello uygulamanızın 360 derecelik tam görünümünü.

