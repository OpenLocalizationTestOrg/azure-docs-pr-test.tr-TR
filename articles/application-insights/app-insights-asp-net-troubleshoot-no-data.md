---
title: "aaaTroubleshooting veri yok - .NET için Application Insights"
description: "Azure Application ınsights'ta verileri görmesini değil mi? Burada deneyin."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: e231569f-1b38-48f8-a744-6329f41d91d3
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 261c25c89884c46e41bbc305474ac854360221ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-no-data---application-insights-for-net"></a>Veri bulunmama sorunlarını giderme - .NET için Application Insights
## <a name="some-of-my-telemetry-is-missing"></a>My telemetri bazıları eksik
*Application Insights ' yalnızca bir kesir Uygulamam tarafından oluşturulan hello olayların görüyorum.*

* Tutarlı bir şekilde görüyorsanız aynı hello kesir, büyük olasılıkla son tooadaptive [örnekleme](app-insights-sampling.md). tooconfirm Bu, arama (Merhaba genel bakış dikey penceresinden) açın ve bir istek veya başka bir olay örneği arayın. Merhaba hello özellikler bölümü altındaki "..." tooget tam özelliği Ayrıntılar'ı tıklatın. Varsa sayısı > 1 isteyebilir ve sonra örnekleme olduğundan işlem. 
* Aksi takdirde, basarsa olası bir [veri hızı sınırı](app-insights-pricing.md#limits-summary) fiyatlandırma planınızın. Bu sınırlar dakika başına uygulanır.

## <a name="no-data-from-my-server"></a>My sunucusundan veri yok
*Uygulamam my web sunucusunda yüklü ve şimdi herhangi telemetrisinden göremiyorum. Geliştirme Makinem Tamam çalıştınız.*

* Güvenlik Duvarı sorunu büyük olasılıkla. [Application Insights toosend veri güvenlik duvarı özel durumlarını ayarlamak](app-insights-ip-addresses.md).

*I [Durum İzleyicisi yüklü](app-insights-monitor-performance-live-website-now.md) web sunucusu toomonitor varolan uygulamalarım üzerinde. Sonuç görmek yok.*

* Bkz: [Durum İzleyicisi sorun giderme](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights). 

## <a name="q01"></a>Visual Studio'da 'Application Insights Ekle' seçeneği
*Çözüm Gezgini'nde varolan bir projeye sağ tıklattığınızda, herhangi bir Application Insights seçeneği görmüyorum.*

* .NET projenin tüm türleri hello araçları tarafından desteklenir. Web ve WCF projeleri desteklenir. Masaüstü ya da hizmet uygulamalar gibi diğer proje türleri için yine [Application Insights SDK'sı tooyour projesinde el ile eklemeniz](app-insights-windows-desktop.md).
* Olduğundan emin olun [Visual Studio 2013 güncelleştirme 3 veya sonraki sürümü](http://go.microsoft.com/fwlink/?LinkId=397827). Merhaba Application Insights SDK'sı sağlayan Geliştirici analiz araçları ile önceden yüklenmiş olarak gelir.
* Seçin **Araçları**, **Uzantılar ve güncelleştirmeler** ve denetleyin **Geliştirici analiz araçları** yüklü ve etkin. Öyleyse **güncelleştirmeleri** kullanılabilir bir güncelleştirme ise toosee.
* Merhaba yeni proje iletişim kutusunu açın ve ASP.NET Web uygulaması seçin. Application Insights seçeneği yok hello sonra hello araçlarının yüklü olduğu görürseniz. Aksi durumda, kaldırma ve hello Application Insights araçları yeniden yüklemeyi deneyin.

## <a name="q02"></a>Application Insights ekleme başarısız oldu
*Tooadd Application Insights tooan mevcut proje çalıştığınızda hata iletisine bakın.*

Olası nedenler:

* Merhaba Application Insights portalı ile iletişimin başarısız; veya
* Azure hesabınızla ilgili bazı sorunları vardır;
* Yalnızca [okuma erişimi toohello abonelik veya burada denemeye toocreate hello yeni kaynak grubu](app-insights-resources-roles-access-control.md).

Düzeltme:

* Merhaba sağ Azure hesabı için oturum açma kimlik bilgileriyle sağlanan denetleyin. 
* Tarayıcınızda, sahip olduğunuz onay erişim toohello [Azure portal](https://portal.azure.com). Ayarları'nı açın ve herhangi bir kısıtlama olup olmadığına bakın.
* [Ekle Application Insights tooyour mevcut proje](app-insights-asp-net.md): Çözüm Gezgini'nde projenize sağ tıklayın ve "Application Insights ekleyin." seçin
* Hala çalışmıyorsa, hello izleyin [el ile yordamı](app-insights-windows-services.md) tooadd hello portalında bir kaynak ve hello SDK tooyour projesi ekleyin. 

## <a name="emptykey"></a>"İzleme anahtarını boş olamaz" hata alıyorum
Application Insights veya belki de günlüğe kaydetme bağdaştırıcısı yükleme sırada bir hata oluştuğundan gibi görünüyor.

Çözüm Gezgini'nde, projenize sağ tıklayın ve seçin **Application Insights > Application Insights yapılandırma**. Toosign, başvurulmasını bir iletişim kutusu içinde tooAzure elde edersiniz ve ya da bir Application Insights kaynağı oluşturun veya var olan bir yeniden kullanın.

## <a name="NuGetBuild"></a>"NuGet paketleri yapı sunucum eksik"
*Her şeyi Tamam my geliştirme makinenizde hata ayıklama, ancak hello yapı sunucuda bir NuGet hatası alıyorum oluşturur.*

Lütfen bakın [NuGet paketi geri yüklemesi](http://docs.nuget.org/Consume/Package-Restore) ve [otomatik paket geri yükleme](http://docs.nuget.org/Consume/package-restore/migrating-to-automatic-package-restore).

## <a name="missing-menu-command-tooopen-application-insights-from-visual-studio"></a>Eksik menü komutu tooopen Visual Studio'da Application Insights
*Çözüm Gezgini proje sağ tıklattığınızda, herhangi bir Application Insights komut görmüyorum ya da bir açık Application Insights komutu görmüyorum.*

Olası nedenler:

* Merhaba Application Insights kaynağını el ile oluşturulan ya da hello proje hello Application Insights araçları tarafından desteklenmeyen bir türde ise.
* Merhaba Geliştirici analiz araçları, Visual Studio'da devre dışı bırakılır. 
* Visual Studio 2013 güncelleştirme 3'den daha eski olduğunda.

Düzeltme:

* Visual Studio sürümünüze 2013 güncelleştirme 3 veya sonrası olduğundan emin olun.
* Seçin **Araçları**, **Uzantılar ve güncelleştirmeler** ve denetleyin **Geliştirici analiz araçları** yüklü ve etkin. Öyleyse **güncelleştirmeleri** kullanılabilir bir güncelleştirme ise toosee.
* Çözüm Gezgini'nde projenize sağ tıklayın. Merhaba komutu görürseniz **Application Insights > Application Insights yapılandırma**, tooconnect kullanmak hello Application Insights hizmeti, proje toohello kaynak.

Aksi takdirde, proje türü doğrudan hello Application Insights araçları tarafından desteklenmiyor. toosee telemetrinizi, oturum açma toohello [Azure portal](https://portal.azure.com)hello sol gezinti çubuğunda Application Insights'ı seçin ve uygulamanızı seçin.

## <a name="access-denied-on-opening-application-insights-from-visual-studio"></a>'Erişim engellendi' Visual Studio Application Insights açarken
*Merhaba 'Açık Application Insights' menü komutu bana toohello Azure portal alır ancak 'erişim engellendi' hatası alın.*

![](./media/app-insights-asp-net-troubleshoot-no-data/access-denied.png)

Microsoft oturum varsayılan tarayıcınızdaki son kullanılan açma Hello yoksa erişim çok[hello Application Insights toothis uygulama eklediğinizde, oluşturulan kaynak](app-insights-asp-net.md). İki olası nedenleri şunlardır: 

* Birden fazla Microsoft hesabı - belki de bir iş ve kişisel bir Microsoft hesabı var? Merhaba oturum-varsayılan tarayıcınızdaki son kullanılan farklı bir hesap için çok erişimi olan bir hello daha içindeydi[Application Insights toohello projesi eklemek](app-insights-asp-net.md). 
  
  * Düzeltme: adınızı tıklatın hello tarayıcı penceresinin sağ üst ve oturumu kapatın. Ardından erişimi hello hesabınızla oturum açın. Ardından hello sol gezinti çubuğunda Application Insights'ı tıklatın ve uygulamanızı seçin.
* Başka birinin Application Insights toohello projesi eklenir ve toogive unuttunuz, [erişim toohello kaynak grubu](app-insights-resources-roles-access-control.md) onu oluşturulduğu. 
  
  * Düzeltme: Kurumsal bir hesap kullandıysanız, bunlar, toohello takım ekleyebilirsiniz; veya, tek tek erişim toohello kaynak grubu verebilirsiniz.

## <a name="asset-not-found-on-opening-application-insights-from-visual-studio"></a>'Varlık bulunamadı' Visual Studio Application Insights açarken
*Merhaba 'Açık Application Insights' menü komutu bana toohello Azure portal alır ancak 'varlık bulunamadı' hata alın.*

Olası nedenler:

* Merhaba, uygulamanız için Application Insights kaynağı silinmiş; veya
* Merhaba izleme anahtarını ayarlamak veya bunu doğrudan hello proje dosyasını güncelleştirmeden düzenleyerek Applicationınsights.Config'de değiştirildi. 

Merhaba izleme anahtarını Applicationınsights.config denetimlerinde hello telemetri burada gönderilir. Visual Studio'da hello komutunu kullandığınızda hangi kaynağın açıldığında hello proje dosyasındaki bir satır denetler. 

Düzeltme:

* Çözüm Gezgini'nde hello projesine sağ tıklayın ve Application Insights, yapılandırma Application Insights'ı seçin. Merhaba iletişim kutusunda, toosend telemetri tooan varolan kaynağı seçin veya yeni bir tane oluşturun. Ya da:
* Merhaba kaynağı doğrudan açın. Çok oturum[Azure portal hello](https://portal.azure.com)hello sol gezinti çubuğunda Application Insights'ı tıklatın ve ardından uygulamanızı seçin.

## <a name="where-do-i-find-my-telemetry"></a>My telemetri nereden bulabilirim?
*İçinde toohello imzalı [Microsoft Azure portal](https://portal.azure.com), ve Azure giriş Pano hello arayarak. Bu nedenle burada Application Insights verilerimi bulabilirim?*

* Merhaba sol gezinti çubuğunda Application Insights, daha sonra uygulama adını tıklatın. Tüm projeleri var. yoksa, çok ihtiyacınız[eklemek veya web projenize Application Insights yapılandırmak](app-insights-asp-net.md).
  
    Var. bazı Özet grafikleri görürsünüz. Aralarında tıklayabilirsiniz toosee daha ayrıntılı bilgi.
* Uygulamanızın hatalarını ayıkladığınız sırada Visual Studio'da hello Application Insights düğmesine tıklayın.

## <a name="q03"></a>Hiçbir sunucu verisi (veya hiç veri yok)
*Uygulamam çalıştıran ve daha sonra Microsoft Azure'da hello Application Insights hizmeti açılır, ancak tüm grafikler Göster hello ' öğrenin nasıl toocollect...' veya 'Yapılandırılmamış.'* Veya, *sayfa görünümü ve kullanıcı verilerini, ancak hiçbir sunucu verisi.*

* Uygulamanızı (F5) Visual Studio'da hata ayıklama modunda çalıştırın. Merhaba uygulaması toogenerate birkaç telemetri kullanın. Merhaba Visual Studio çıktı penceresinde günlüğe kaydedilen olayları görebilirsiniz denetleyin. 
  
    ![](./media/app-insights-asp-net-troubleshoot-no-data/output-window.png)
* Merhaba Application Insights Portalı'nda açmak [tanılama arama](app-insights-diagnostic-search.md). Veri genellikle burada ilk görünür.
* Merhaba Yenile düğmesini tıklatın. Merhaba dikey kendisini düzenli aralıklarla yeniler, ancak aynı zamanda bunu el ile yapabilirsiniz. Merhaba yenileme aralığı daha büyük zaman aralıkları için uzun.
* Merhaba araçları anahtarlarının eşleşmesi denetleyin. Merhaba ana dikey penceresinde hello Application Insights portalında, hello uygulamanız için **Essentials** açılan listesinde, bakmak **izleme anahtarını**. Ardından, projenizi Visual Studio'da Applicationınsights.config açın ve hello bulur `<instrumentationkey>`. Merhaba iki anahtar eşit olup olmadığını denetleyin. Aksi takdirde:
  
  * Merhaba portalında Application Insights'ı tıklatın ve hello doğru anahtarla hello Uygulama kaynağı için bakın. veya
  * Visual Studio Çözüm Gezgini'nde, hello projesine sağ tıklayın ve Application Insights, Yapılandır'ı seçin. Merhaba uygulama toosend telemetri toohello doğru kaynak sıfırlayın.
  * Eşleşen anahtarlarla hello bulamazsanız, kullanmakta olduğunuz onay hello aynı oturum açma kimlik bilgilerini Visual Studio toohello portal olduğu gibi.
    
    ![](./media/app-insights-asp-net-troubleshoot-no-data/ikey-check.png)
* Merhaba, [Microsoft Azure giriş Pano](https://portal.azure.com), hello hizmet durumu eşleme arayın. Bazı uyarı göstergeleri varsa, bunlar tooOK döndürmüş kapatın ve, Application Insights uygulama dikey penceresini yeniden açın kadar bekleyin.
* Ayrıca kontrol [bizim durum blog](http://blogs.msdn.com/b/applicationinsights-status/).
* Hello için herhangi bir kod yazdım [sunucu tarafı SDK](app-insights-api-custom-events-metrics.md) hello izleme anahtarını değişebilir `TelemetryClient` örnekleri veya `TelemetryContext`? Veya, yazdım bir [filtre veya örnekleme yapılandırma](app-insights-api-filtering-sampling.md) filtrelemesi çok fazla çıkışı?
* Applicationınsights.config düzenlediyseniz hello yapılandırmasını dikkatle denetleyin [TelemetryInitializers ve TelemetryProcessors](app-insights-api-filtering-sampling.md). Bir hatalı adlı türü veya parametresi hello SDK toosend hiçbir veri neden olabilir.

## <a name="q04"></a>Sayfa görünümleri, tarayıcılar kullanımını veri yok
*Sunucu yanıt süresi ve sunucu istekleri grafiklerinde veri, ancak hiçbir veri sayfa görünümü yükleme süresi veya hello tarayıcı ya da kullanım Kanatlar görüyorum.*

Merhaba web sayfalarındaki komut dosyalarından Hello veriler gelir. 

* Web projesi, varolan Application Insights tooan eklediyseniz [tooadd hello betikleri el ile sahip](app-insights-javascript.md).
* Internet Explorer, site uyumluluk modunda görüntüleme olmadığından emin olun.
* Merhaba tarayıcınızın hata ayıklama özelliği (F12 bazı tarayıcılarda sonra seçin ağ) kullanmak veri çok gönderilen tooverify`dc.services.visualstudio.com`.

## <a name="no-dependency-or-exception-data"></a>Hiçbir bağımlılık veya özel durum verileri
Bkz: [bağımlılık telemetrisi](app-insights-asp-net-dependencies.md) ve [özel durum telemetrisi](app-insights-asp-net-exceptions.md).

## <a name="no-performance-data"></a>Hiçbir performans verisi
Performans verilerini (CPU, g/ç hızı vb.) için kullanılabilir [Java web Hizmetleri](app-insights-java-collectd.md), [Windows Masaüstü uygulamaları](app-insights-windows-desktop.md), [IIS, uygulama ve hizmetlere Durum İzleyicisi yüklerseniz web](app-insights-monitor-performance-live-website-now.md), ve [Azure Cloud Services](app-insights-azure.md). Sunucuları ayarlar altında bulabilirsiniz.

Azure Web siteleri için kullanılabilir değil.

## <a name="no-server-data-since-i-published-hello-app-toomy-server"></a>Merhaba uygulama toomy server yayımlandığı tarihten sonra hiçbir (sunucu) verisi
* Gerçekte tüm hello Microsoft kopyaladığınız denetleyin. Microsoft.Diagnostics.Instrumentation.Extensions.Intercept.dll birlikte Applicationınsights DLL'leri toohello sunucu
* Güvenlik Duvarı'nda, çok olabilir[bazı TCP bağlantı noktalarını açmak](app-insights-ip-addresses.md#data-access-api).
* Şirket ağınıza dışında bir proxy toosend toouse varsa, ayarlamak [defaultProxy](https://msdn.microsoft.com/library/aa903360.aspx) Web.config dosyasında
* Windows Server 2008: hello şu güncelleştirmeleri yüklediğinizden emin olun: [KB2468871](https://support.microsoft.com/kb/2468871), [KB2533523](https://support.microsoft.com/kb/2533523), [KB2600217](https://support.microsoft.com/kb/2600217).

## <a name="i-used-toosee-data-but-it-has-stopped"></a>Toosee veri kullanılır, ancak bunu durduruldu
* Merhaba denetleyin [durum blog](http://blogs.msdn.com/b/applicationinsights-status/).
* Veri noktalarının aylık kota ulaşıp? Hello ayarları/kota ve fiyatlandırma toofind kullanıma açın. Bu durumda, planınızı yükseltmek veya ek kapasite için ödeme yaparsınız. Merhaba bkz [düzeni fiyatlandırma](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="i-dont-see-all-hello-data-im-expecting"></a>Tüm hello veri bekleniyor görmüyorum
Uygulamanız çok miktarda veri gönderir ve kullandığınız ASP.NET sürüm 2.0.0-beta3 için Application Insights SDK'sı hello mı yoksa daha sonra hello [Uyarlamalı örnekleme](app-insights-sampling.md) özellik çalışır ve yalnızca bir yüzdesini telemetrinizi gönderme. 

Devre dışı bırakabilir, ancak bu önerilmez. Örnekleme ilgili telemetri doğru tanılama amacıyla aktarılan şekilde tasarlanmıştır. 

## <a name="wrong-geographical-data-in-user-telemetry"></a>Kullanıcı telemetri içinde yanlış coğrafi veriler
Merhaba Şehir, bölge ve ülke boyutları IP adreslerinden türetilmiş ve her zaman doğru değil.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Azure Cloud Services’da çalıştırma üzerine “yöntem bulunamadı” özel durumu
.NET 4.6 için mi oluşturdunuz? 4.6 sürümü Azure Cloud Services rollerinde otomatik olarak desteklenmez. Uygulamanızı çalıştırmadan önce [her role 4.6 sürümünü yükleyin](../cloud-services/cloud-services-dotnet-install-dotnet.md).

## <a name="still-not-working"></a>Hala çalışmıyor...
* [Uygulama Öngörüler Forumu](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

