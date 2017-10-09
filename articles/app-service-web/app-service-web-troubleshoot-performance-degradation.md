---
title: "Uygulama hizmeti aaaSlow web uygulaması performans | Microsoft Docs"
description: "Bu makale, Azure App Service'te yavaş web uygulaması performans sorunlarını gidermenize yardımcı olur."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "Web uygulama performansı, yavaş uygulama, uygulama yavaş"
ms.assetid: b8783c10-3a4a-4dd6-af8c-856baafbdde5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2016
ms.author: cephalin
ms.openlocfilehash: 3e56b99b48db0e7baae1fac797a7fcb9eff74c9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-web-app-performance-issues-in-azure-app-service"></a>Azure App Service'te yavaş web uygulaması performans sorunlarını giderme
Bu makalede yavaş web uygulaması performans sorunları gidermenize yardımcı [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure hello ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) ve tıklayın **destek alın**.

## <a name="symptom"></a>Belirti
Merhaba web uygulaması göz attığınızda, hello yük yavaş ve bazen zaman aşımı sayfaları.

## <a name="cause"></a>Nedeni
Bu sorun sık sık uygulama düzeyi sorunları tarafından gibi neden olur:

* ağ isteklerine uzun sürüyor
* uygulama kodu veya veritabanı sorguları verimsiz bırakılıyor
* yüksek bellek/CPU kullanarak uygulama
* tooan özel durum kilitlenen uygulama

## <a name="troubleshooting-steps"></a>Sorun giderme adımları
Sorun giderme sıralı bir düzende üç farklı görevler ayrılabilir:

1. [İnceleyin ve uygulama davranışı izleme](#observe)
2. [Veri toplama](#collect)
3. [Merhaba sorunu azaltmak](#mitigate)

[App Service Web Apps](/services/app-service/web/) her adımda çeşitli seçenekler sunar.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. İnceleyin ve uygulama davranışı izleme
#### <a name="track-service-health"></a>Hizmet durumu izleme
Microsoft Azure hizmet kesintisi veya performans düşüşü olduğundan her zaman publicizes. Merhaba üzerinde hello hello hizmet durumunu izleyebilirsiniz [Azure portal](https://portal.azure.com/). Daha fazla bilgi için bkz: [hizmet durumu izleme](../monitoring-and-diagnostics/insights-service-health.md).

#### <a name="monitor-your-web-app"></a>Web uygulamanızı izlemek
Uygulamanızı sorunları yaşıyorsa bu seçenek, toofind çıkışı sağlar. Web uygulamanızın dikey penceresinde hello tıklayın **istekleri ve hataları** döşeme. Merhaba **ölçüm** dikey gösterir, tüm hello ölçümleri ekleyebilirsiniz.

Web uygulamanız için toomonitor isteyebilirsiniz hello ölçümleri bazıları

* Ortalama bellek çalışma kümesi
* Ortalama yanıt süresi
* CPU süresi
* Bellek çalışma kümesi
* İstekler

![Web uygulaması performans izleme](./media/app-service-web-troubleshoot-performance-degradation/1-monitor-metrics.png)

Daha fazla bilgi için bkz.

* [Azure App Service'te Web uygulamalarını izleme](web-sites-monitor.md)
* [Uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

#### <a name="monitor-web-endpoint-status"></a>Web uç noktası durumunu izleme
Web uygulamanızı hello çalıştırıyorsanız, **standart** fiyatlandırma katmanı, Web uygulamaları iki uç nokta üç coğrafi konumdan izlemenize izin verir.

Uç nokta izleme web testleri test yanıt süresi ve web URL'leri çalışma süresini coğrafi olarak dağıtılmış konumlardan yapılandırır. Merhaba test her konumdan hello web URL toodetermine hello yanıt süresi ve çalışma süresi üzerinde bir HTTP GET işlemi gerçekleştirir. Yapılandırılmış her konum bir test beş dakikada bir çalışır.

Açık kalma süresi HTTP yanıt kodları kullanılarak izlenen ve yanıt süresini milisaniye cinsinden ölçülür. Büyük veya ona eşit too400 veya hello yanıt 30 saniyeden fazla alır, Hello HTTP yanıt kodunu ise, izleme testi başarısız olur. Bir uç nokta izleme testleri tümünden başarılı kullanılabilir sayılması hello belirtilen konumları.

tooset, görmek [Azure uygulama hizmetinde uygulamaları izleme](web-sites-monitor.md).

Ayrıca bkz [tutma Azure Web siteleri ve uç nokta izleme - Stefan Schackow ile](https://channel9.msdn.com/Shows/Azure-Friday/Keeping-Azure-Web-Sites-up-plus-Endpoint-Monitoring-with-Stefan-Schackow) uç nokta izleme hakkında bir video.

#### <a name="application-performance-monitoring-using-extensions"></a>Uzantıları kullanarak uygulama performansı izleme
Kullanarak, uygulama performansını izleyebilirsiniz *site uzantıları*.

Her App Service web uygulaması toouse sağlayan bir Genişletilebilir yönetim uç noktası bir güçlü site uzantıları olarak dağıtılan araçlar sağlar. Uzantıları aşağıdakileri içerir: 

- Kaynak kodu düzenleyicileri ister [Visual Studio Team Services](https://www.visualstudio.com/products/what-is-visual-studio-online-vs.aspx). 
- Bir MySQL veritabanı gibi bağlı kaynaklar için Yönetim Araçları tooa web uygulaması bağlı.

[Azure Application Insights](/services/application-insights/) ve [New Relic](/marketplace/partners/newrelic/newrelic/) hello performans kullanılabilir site uzantıları izleme ikisidir. New Relic toouse, çalışma zamanında bir aracı yükleyin. Azure Application Insights toouse, kodunuzu bir SDK ile yeniden oluşturun ve erişim tooadditional veri sağlayan bir uzantı de yükleyebilirsiniz. Merhaba SDK kod toomonitor hello kullanım ve performans, uygulamanızın daha ayrıntılı olarak yazmanızı sağlar.

toouse Application Insights, bkz: [web uygulamalarında performansı izleyerek](../application-insights/app-insights-web-monitor-performance.md).

toouse New Relic bkz [Azure ile ilgili yeni Relic uygulama performans yönetimi](../store-new-relic-cloud-services-dotnet-application-performance-management.md).

<a name="collect" />

### <a name="2-collect-data"></a>2. Veri toplama
Merhaba Web Apps ortam hello web sunucusu ve hello web uygulamasının içinden bilgileri günlüğe kaydetme için tanılama işlevi sağlar. Merhaba bilgileri, web sunucusu tanılama ve uygulama tanılama ayrılır.

#### <a name="enable-web-server-diagnostics"></a>Web sunucusu tanılamayı etkinleştirin
Etkinleştirmek veya tür günlüğe aşağıdaki hello devre dışı bırakabilirsiniz:

* **Hata günlüğü ayrıntılı** -ayrıntılı hata bilgileri (durum kodu 400 veya daha büyük) hatası olduğunu gösteren HTTP durum kodları için. Bu neden hello sunucu hello hata kodunu döndürdü belirlemenize yardımcı olabilecek bilgiler içerebilir.
* **Başarısız istek izleme** -ayrıntılı izleme hello IIS kullanılan bileşenler tooprocess hello isteği ve her bileşenin geçen hello süre dahil olmak üzere, başarısız istekler hakkında bilgi. Tooimprove web uygulaması performans çalıştığınız ya da belirli bir HTTP hata neden olan yalıtmak bu yararlı olabilir.
* **Web sunucusu günlüğe kaydetme** -hello W3C Genişletilmiş günlük dosyası biçimini kullanarak HTTP işlemler hakkında bilgi. Bu, işlenen istek hello sayısı veya belirli bir IP adresinden kaç isteklerdir gibi genel web uygulaması ölçümleri belirlerken yararlıdır.

#### <a name="enable-application-diagnostics"></a>Uygulama tanılamayı etkinleştirin
Çeşitli seçenekler toocollect uygulama performansı verileri Web uygulamalarından vardır, uygulamanızın Canlı Visual Studio'dan profil veya daha fazla bilgi ve izlemeleri uygulama kodu toolog değiştirin. Merhaba seçenekler seçebilirsiniz ne kadar erişimi toohello uygulamanız varsa ve izleme araçları hello gözlenen.

##### <a name="use-application-insights-profiler"></a>Uygulama Öngörüler profil oluşturucu kullanın
Ayrıntılı performans izlemelerini yakalama hello uygulama Öngörüler profil oluşturucu toostart etkinleştirebilirsiniz. Merhaba geçen gün önce tooinvestigate sorunları gerektiğinde oldu toofive yakalanan izlere erişebilirsiniz. Azure Portal'da erişim toohello web uygulamanızın Application Insights kaynağı sahip olduğu sürece bu seçeneği belirleyebilirsiniz.

Uygulama Öngörüler profil oluşturucu hangi satırlık bir kod hello yavaş yanıtlar neden gösteren yanıt süresi her bir web araması ve izlemeleri için istatistikler sağlar. Bir kullanıcı belirli kod yazılmaz bazen hello App Service uygulaması yavaş çünkü yolu. Paralel ve istenmeyen veritabanı kilit çakışmaları çalıştırılabilir sıralı kod örnekleri içerir. Bu performans sorunlarını hello kodda kaldırma hello uygulamanın performansı artırır ancak ayrıntılı izlemeleri ve günlükleri ayarlama olmadan sabit toodetect olur. Uygulama Öngörüler Profil Oluşturucu tarafından toplanan hello izlemeleri uygulama hizmeti uygulamalar için bu sorunu gidermek ve Merhaba uygulaması yavaşlatır kod hello satırlarını tanımlama yardımcı olur.

 Daha fazla bilgi için bkz: [profil oluşturma Canlı Azure web uygulamaları Application Insights ile](../application-insights/app-insights-profiler.md).

##### <a name="use-remote-profiling"></a>Uzaktan profil oluşturmayı kullanma
Azure App Service'te Web Apps, API uygulamaları ve Web işleri uzaktan profili. Merhaba tam olarak biliyorsanız, zaman aralığı hello performans sorunu olur ve nasıl tooreproduce hello sorunu bildirin veya erişim toohello web uygulama kaynağı varsa bu seçeneği belirleyin.

Uzaktan profil oluşturma hello hello işleminin CPU kullanımı yüksekse ve işleminizi beklenenden daha yavaş çalışıyor veya HTTP isteklerini hello gecikme normalden daha yüksek yaparsanız uzaktan işleminizi profil ve hello CPU örnekleme çağrı yığınları tooanalyze almak yararlı olur işlem etkinliği hello ve dinamik yollar kod.

Daha fazla bilgi için bkz: [uzaktan profil oluşturma desteği Azure App Service'te](https://azure.microsoft.com/blog/remote-profiling-support-in-azure-app-service).

##### <a name="set-up-diagnostic-traces-manually"></a>Tanılama izlemeleri el ile ayarlayın
Erişim toohello web uygulaması kaynak kodu varsa, uygulama Tanılama, web uygulama tarafından üretilen toocapture bilgileri sağlar. ASP.NET uygulamaları hello kullanabileceğiniz `System.Diagnostics.Trace` sınıfı toolog bilgi toohello uygulama tanılama günlük. Bununla birlikte, toochange gerek hello kod ve uygulamanızı yeniden dağıtın. Uygulamanızı test bir ortamda çalışıyorsa, bu yöntem önerilir.

Ayrıntılı yönergeler için günlüğe kaydetme, uygulamanızın tooconfigure bkz [Azure App Service'te web uygulamalarını için tanılama günlüğünü etkinleştirme](web-sites-enable-diagnostic-log.md).

#### <a name="use-hello-azure-app-service-support-portal"></a>Hello Azure App Service destek portalını kullanın
Web uygulamaları HTTP günlükleri, olay günlükleri, işlem dökümleri ve daha fazla bakarak hello özelliği tootroubleshoot sorunları ilgili tooyour web uygulaması ile sağlar. Bizim destek portalında kullanarak tüm bu bilgilere erişebilen **http://&lt;, uygulama adı >.scm.azurewebsites.net/Support**

Hello Azure App Service destek portal toosupport hello üç adımdan yaygın bir sorun giderme senaryo üç ayrı sekmeyle sağlar:

1. Şu anki davranışı inceleyin
2. Tanılama bilgilerini toplama ve yerleşik çözümleyiciler hello çalıştıran analiz eder.
3. Azaltmak

Merhaba sorunu şimdi oluşuyorsa tıklatın **Çözümle** > **tanılama** > **şimdi tanılamak** toocreate sizin için tanılama oturumu hangi HTTP günlükleri, Olay Görüntüleyicisi günlükleri, bellek dökümleri, PHP Hata günlüklerini ve PHP işlem raporu toplar.

Merhaba veri toplandığında, hello destek portal hello verilerini analiz çalışır ve bir HTML raporu ile sağlar.

Varsayılan olarak toodownload hello veri istemeniz durumunda, hello D:\home\data\DaaS klasöründe depolanması.

Hello Azure App Service destek portal hakkında daha fazla bilgi için bkz: [yeni güncelleştirmeler tooSupport Azure Web siteleri için Site uzantısı](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Merhaba Kudu hata ayıklama konsolunu kullanma
Web uygulamaları, hata ayıklama, keşfetme, ortamınız hakkında bilgi almak için JSON bitiş noktaları yanı sıra, dosyaları karşıya yükleme için kullanabileceğiniz bir hata ayıklama konsolu ile birlikte gelir. Bu konsolu hello adlı *Kudu konsol* veya hello *SCM Pano* web uygulamanız için.

Giden toohello bağlantısıyla bu panoya erişebilir **https://&lt;, uygulama adı >.scm.azurewebsites.net/**.

Kudu sağlar hello şeylerden bazıları şunlardır:

* Uygulamanız için ortam ayarları
* günlük akışı
* Tanılama dökümü
* hata ayıklama konsolunu Powershell cmdlet'leri ve temel DOS komutları çalıştırabilirsiniz.

Başka bir yararlı Kudu uygulamanızı ilk fırsat özel durum atma durumunda, Kudu kullanabilirsiniz ve hello SysInternals aracı Procdump toocreate bellek dökümleri, özelliğidir. Bu bellek dökümlerini hello işleminin anlık görüntüleri ve genellikle web uygulamanızı daha karmaşık sorunları gidermenize yardımcı olabilir.

Kudu içinde kullanılabilir özellikler hakkında daha fazla bilgi için bkz: [hakkında bilmeniz Azure Web siteleri Team Services Araçları](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Merhaba sorunu azaltmak
#### <a name="scale-hello-web-app"></a>Ölçek hello web uygulaması
Azure App Service'te performansı artırmak ve üretilen işi için uygulamanızı çalıştıran hello ölçek ayarlayabilirsiniz. Bir web uygulamasını kurup ölçeklendirmeyi kapsar iki eylemlerin: fiyatlandırma katmanı ve daha yüksek fiyatlandırma katmanı toohello geçirildikten sonra belirli ayarları yapılandırma yüksek, uygulama hizmeti planı tooa değiştirme.

Ölçeklendirme ile ilgili daha fazla bilgi için bkz: [bir web uygulamasını Azure App Service'te ölçeklendirme](web-sites-scale.md).

Ayrıca, uygulamanızı birden fazla örneği üzerinde toorun seçebilirsiniz. Ölçek genişletme yalnızca ile daha fazla işleme yeteneği sağlar, ancak ayrıca miktar hataya dayanıklılık sağlar. Merhaba işlem bir örneğinde devre dışı kalırsa, hello diğer örnekleri tooserve istekleri devam edin.

Toobe el ile veya otomatik ölçeklendirme hello ayarlayabilirsiniz.

#### <a name="use-autoheal"></a>AutoHeal kullanın
AutoHeal (yapılandırma değişiklikleri, istekleri, bellek tabanlı sınırları veya hello zaman tooexecute bir istek gerekli gibi) seçtiğiniz ayarlarına dayanarak, uygulamanız için hello çalışan işlemi geri dönüştürüldüğünde. Başlangıç saati, çoğu hello en hızlı yolu toorecover bir sorun geri dönüşüm hello işlemidir. Her zaman hello web uygulamasından doğrudan hello Azure portalı içinde yeniden olsa AutoHeal bunu otomatik olarak sizin için yapar. Toodo gereken tek şey, web uygulamanız için hello kök web.config dosyasında bazı tetikleyicileri ekleyin. Bu ayarları hello aynı çalışır şekilde uygulamanız .net uygulaması olsa bile.

Daha fazla bilgi için bkz: [Azure Web siteleri otomatik düzeltme](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Merhaba web uygulaması yeniden
Yeniden başlatma hello en basit yolu toorecover tek seferlik sorunlardan görülür. Merhaba üzerinde [Azure portal](https://portal.azure.com/), web uygulamanızın dikey penceresinde hello seçenekleri toostop sahip veya uygulamanızı yeniden başlatın.

 ![Web uygulaması toosolve performans sorunlarını yeniden başlatın](./media/app-service-web-troubleshoot-performance-degradation/2-restart.png)

Web uygulamanızı Azure Powershell kullanarak da yönetebilirsiniz. Daha fazla bilgi için bkz. [Azure PowerShell'i Azure Resource Manager ile kullanma](../powershell-azure-resource-manager.md).
