---
title: "Azure Application Insights ile ASP.NET web uygulaması analizi yukarı aaaSet | Microsoft Docs"
description: "Şirket içi veya Azure’de barındırılan ASP.NET web siteniz için performans, kullanılabilirlik ve kullanım analizi yapılandırın."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: d0eee3c0-b328-448f-8123-f478052751db
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/15/2017
ms.author: bwren
ms.openlocfilehash: 61a3cdce68da48bfb9450b1d296acc1535f50a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-application-insights-for-your-aspnet-website"></a>ASP.NET web siteniz için Application Insights'ı ayarlama

Bu yordam, ASP.NET web uygulaması toosend telemetri toohello yapılandırır [Azure Application Insights](app-insights-overview.md) hizmet. Kendi IIS sunucunuzu veya hello bulut barındırılan ASP.NET uygulamaları için çalışır. Grafikler alın ve yardımcı bir güçlü sorgu dili, uygulamanızın hello performansı ve nasıl kişiler, artı otomatik uyarıları hatalar veya performans sorunları kullandığını anlamak. Geliştiricilerin çoğu bu özellikleri harika olduklarından, ancak aynı zamanda genişletmek ve gerekirse hello telemetri özelleştirme gibi bulun.

Visual Studio'da kurulum yalnızca birkaç tıklama ile yapılır. Telemetri hello hacmi sınırlayarak hello seçeneği tooavoid ücretleri sahip. Bu, tooexperiment ve hata ayıklama veya toomonitor değil çok sayıda kullanıcı içeren bir site sağlar. Şimdi toogo istediğiniz ve üretim sitesini izleme karar verdiğinizde, daha sonra kolay tooraise hello sınırı olan.

## <a name="before-you-start"></a>Başlamadan önce
Gerekenler:

* Visual Studio 2013 güncelleştirme 3 veya sonraki bir sürümü. Ne kadar yeniyse o kadar iyidir.
* Bir abonelik çok[Microsoft Azure](http://azure.com). Ekibinizin ve kuruluşunuzun bir Azure aboneliğiniz varsa, hello sahibi, tooit, kullanarak ekleyebilir, [Microsoft hesabı](http://live.com).

İçinde ilgileniyorsanız alternatif konuları toolook adresindeki vardır:

* [Çalışma zamanında bir web uygulamasını izleme](app-insights-monitor-performance-live-website-now.md)
* [Azure Cloud Services](app-insights-cloudservices.md)

## <a name="ide"></a>1. adım: hello Application Insights SDK ekleme

Çözüm Gezgini'nde web uygulaması projenize sağ tıklayın ve **Ekle** > **, Application Insights Telemetrisi...**'ni veya **Application Insights'ı Yapılandır**'ı seçin.

![Application Insights Telemetrisi Ekle seçeneğinin vurgulandığı Çözüm Gezgini’nin ekran görüntüsü](./media/app-insights-asp-net/appinsights-03-addExisting.png)

(Visual Studio 2015'te de bulunmaktadır hello yeni proje iletişim kutusunda seçeneği tooadd Application Insights.)

Toohello Application Insights yapılandırma sayfası devam edin:

![Uygulamanızı Application Insights'a kaydedin sayfasının ekran görüntüsü](./media/app-insights-asp-net/visual-studio-register-dialog.png)

**a.** Merhaba hesabınızı ve aboneliğinizi tooaccess Azure kullandığınız seçin.

**b.** Toosee hello verilerin uygulamanızdan istediğiniz azure'da Hello kaynağı seçin. Genellikle:

* Tek bir uygulamanın [farklı bileşenleri için tek kaynak](app-insights-monitor-multi-role-apps.md) kullanın. 
* İlişkisiz uygulamalar için ayrı kaynaklar oluşturun.
 
Verilerinizin depolandığı tooset hello kaynak grubu veya hello konumu istiyorsanız, **ayarlarını yapılandırma**. Kaynak, kullanılan toocontrol erişim toodata gruplarıdır. Örneğin, form kısmı çeşitli uygulamalar varsa aynı hello sistemi içine Application Insights verilerini hello aynı kaynak grubu.

**c.** Bir uç tooavoid ücretleri hello boş veri birimi sınırı ayarlayın. Application Insights tooa ücretsiz belirli birim telemetri. Merhaba kaynak oluşturulduktan sonra açarak seçiminizi hello portalında değiştirebilirsiniz **özellikleri + fiyatlandırma** > **veri birimi Yönetimi** > **günlük Birim cap**.

**d.** Tıklatın **kaydetmek** devam toogo ve Application Insights web uygulamanız için yapılandırın. Telemetri toohello gönderilecek [Azure portal](https://portal.azure.com), hem hata ayıklama sırasında hem de uygulamanızı yayımladıktan sonra.

**e.** Hatalarını ayıkladığınız sırada toosend telemetri toohello portal istemiyorsanız, yalnızca hello Application Insights SDK'sı tooyour uygulama Ekle ancak kaynak hello Portalı'nda yapılandırmayın. Hata ayıklarken Visual Studio'da mümkün toosee telemetri olacaktır. Daha sonra toothis yapılandırma sayfasına dönmek veya uygulamanızı dağıttıktan sonra kadar beklemeniz ve [telemetriyi çalışma zamanında geçiş](app-insights-monitor-performance-live-website-now.md).


## <a name="run"></a> 2. Adım: Uygulamanızı çalıştırma
F5 tuşuna basarak uygulamanızı çalıştırın. Farklı sayfalara toogenerate bazı telemetriyi açın.

Visual Studio'da günlüğe kaydedilmiş hello etkinliklerin sayısını görürsünüz.

![Visual Studio’nun ekran görüntüsü. hata ayıklama sırasında Hello Application Insights düğmesi gösterilir.](./media/app-insights-asp-net/54.png)

## <a name="step-3-see-your-telemetry"></a>Adım 3: Telemetrinize bakma
Visual Studio'da veya hello Application Insights web Portalı'nda telemetrinizi görebilirsiniz. Arama telemetri Visual Studio toohelp uygulamanızın hatalarını ayıklama. Sisteminizin Canlı olduğunda performans ve kullanım hello web Portalı'nda izleyin. 

### <a name="see-your-telemetry-in-visual-studio"></a>Visual Studio'da telemetrinize bakma

Visual Studio'da hello Application Insights penceresini açın. Hello tıklayın **Application Insights** düğmesini ya da Çözüm Gezgini'nde, select projenize sağ tıklayıp **Application Insights**ve ardından **arama Canlı Telemetri**.

Merhaba Visual Studio uygulama Insights arama penceresinde hello bkz **hata ayıklama oturumu verilerden** hello sunucu tarafı, uygulamanızın içinde oluşturulan telemetri için görünümü. Hello filtrelerle denemeler yapın ve daha ayrıntılı olay toosee tıklayın.

![Ekran görüntüsü hello hata ayıklama oturumu verilerden hello Application Insights penceresinde görüntüleyebilirsiniz.](./media/app-insights-asp-net/55.png)

> [!NOTE]
> Herhangi bir veri görmüyorsanız, hello zaman aralığı doğru olduğundan ve hello arama simgesine tıklayın emin olun.

[Visual Studio’daki Application Insights araçları hakkında daha fazla bilgi edinin](app-insights-visual-studio.md).

<a name="monitor"></a>
### <a name="see-telemetry-in-web-portal"></a>Web portalında telemetriye bakma

(Tooinstall yalnızca hello SDK seçmedikçe) hello Application Insights web portalındaki telemetriyi de görebilirsiniz. Merhaba portal daha fazla grafikler, analiz aracı ve çapraz bileşen görünümleri Visual Studio'ya sahiptir. Merhaba portal ayrıca uyarılar sağlar.

Application Insights kaynağınızı açın. Ya da oturum içinde toohello [Azure portal](https://portal.azure.com/) ve onu yok veya sağ hello proje Visual Studio'da bulmak ve var olması çalışmasına izin.

![Ekran görüntüsü, Visual nasıl tooopen hello Application Insights portalındaki gösteren Studio](./media/app-insights-asp-net/appinsights-04-openPortal.png)

> [!NOTE]
> Erişim hata alırsanız: birden fazla dizi Microsoft kimlik bilgisi var ve bu hello yanlış kümesi ile imzalanmış? Merhaba portalında, oturumu kapatın ve yeniden oturum açın.

Merhaba portal uygulamanızdan hello telemetrinin bir görünümünü açar.

![Application Insights’a genel bakış sayfasının ekran görüntüsü](./media/app-insights-asp-net/66.png)

Merhaba Portalı'nda daha fazla ayrıntı döşeme veya grafiği toosee'ı tıklatın.

[Hello Azure portalında Application Insights kullanma hakkında daha fazla bilgi](app-insights-dashboards.md).

## <a name="step-4-publish-your-app"></a>4. Adım: Uygulamanızı yayımlama
Uygulama tooyour IIS sunucusu veya tooAzure yayımlayın. Gözcü [ölçümleri bir canlı akışı](app-insights-metrics-explorer.md#live-metrics-stream) toomake emin her şeyi sorunsuz çalışır.

Burada izleyebilir ölçümleri, telemetrinizi arama ve ayarlanan hello Application Insights portalında, telemetrinizi derlemeler [panolar](app-insights-dashboards.md). Ayrıca hello güçlü kullanabilirsiniz [günlük analizi sorgu dili](https://docs.loganalytics.io/) tooanalyze kullanım ve performans veya toofind belirli olaylar.

Ayrıca, telemetri tooanalyze devam edebilirsiniz [Visual Studio](app-insights-visual-studio.md), tanılama arama gibi araçlar ve [eğilimleri](app-insights-visual-studio-trends.md).

> [!NOTE]
> Uygulamanızı yeterli telemetri tooapproach hello gönderirse [azaltma sınırları](app-insights-pricing.md#limits-summary), otomatik [örnekleme](app-insights-sampling.md) anahtarlarını. Örnekleme tanılama amacıyla ilişkili verileri korurken, uygulamanızdan gönderilen telemetri hello miktarını azaltır.
>
>

## <a name="land"></a> İşiniz tamamlandı

Tebrikler! Uygulamanızda hello Application Insights paketini yüklü ve Azure üzerinde toosend telemetri toohello Application Insights hizmeti yapılandırılmış.

![Telemetri hareketlerinin diyagramı](./media/app-insights-asp-net/01-scheme.png)

Merhaba, uygulamanızın telemetri alır Azure kaynak tarafından tanımlanan bir *izleme anahtarını*. Bu anahtar hello Applicationınsights.config dosyasında bulabilirsiniz.


## <a name="upgrade-toofuture-sdk-versions"></a>Toofuture SDK sürümlerine yükseltme
tooupgrade tooa [hello SDK'ın yeni sürümüne](https://github.com/Microsoft/ApplicationInsights-dotnet-server/releases)açın hello **NuGet Paket Yöneticisi** yeniden ve yüklü paketleri filtre. **Microsoft.ApplicationInsights.Web**’i seçip **Yükselt**’i seçin.

Tüm özelleştirmeler tooApplicationInsights.config yaptıysanız yükseltmeden önce bir kopyasını kaydedin. Daha sonra değişikliklerinizi hello yeni sürümle birleştirin.

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>Sonraki adımlar

### <a name="more-telemetry"></a>Daha fazla telemetri

* **[Tarayıcı ve sayfa yükleme verileri](app-insights-javascript.md)** - Web sayfalarınıza bir kod parçacığı ekleyin.
* **[Daha ayrıntılı bağımlılık ve özel durum izlemesi alın](app-insights-monitor-performance-live-website-now.md)** - Sunucunuza Durum İzleyicisi yükleyin.
* **[Özel olaylar kod](app-insights-api-custom-events-metrics.md)**  toocount, saat ya da kullanıcı eylemlerini ölçün.
* **[Günlük verilerini alma](app-insights-asp-net-trace-logs.md)** - Günlük verilerini telemetrinizle ilişkilendirin.

### <a name="analysis"></a>Analiz

* **[Visual Studio’da Application Insights ile çalışma](app-insights-visual-studio.md)**<br/>Telemetri ile hata ayıklama hakkında bilgi içeren tanılama arama ve toocode ayrıntılarına gidin.
* **[Merhaba Application Insights portalıyla çalışma](app-insights-dashboards.md)**<br/> Panolar, güçlü tanılama ve analiz araçları, uyarılar, uygulamanızın canlı bağımlılık haritası ve telemetriyi dışarı aktarma hakkında bilgi içerir.
* **[Analytics](app-insights-analytics-tour.md)**  -hello güçlü sorgu dili.

### <a name="alerts"></a>Uyarılar

* [Kullanılabilirlik testleri](app-insights-monitor-web-app-availability.md): testleri oluşturma toomake sitenizi hello Web'de göründüğünden emin.
* [Akıllı tanılama](app-insights-proactive-diagnostics.md): toodo tooset herhangi bir şey yok Bu testler otomatik olarak çalıştırmaz, bu nedenle bunları ayarlama. Uygulamanızda olağan dışı oranda başarısız istek olup olmadığını bildirirler.
* [Ölçüm uyarıları](app-insights-alerts.md): Bu toowarn ayarlayın, bir ölçüm bir eşik kestiği durumunda. Bunları, uygulamanıza kodladığınız özel ölçümlerde ayarlayabilirsiniz.

### <a name="automation"></a>Otomasyon

* [Application Insights kaynağı oluşturmayı otomatikleştirme](app-insights-powershell.md)
