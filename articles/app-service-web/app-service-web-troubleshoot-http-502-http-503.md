---
title: "aaaFix 502 hatalı ağ geçidi, 503 Hizmet kullanılamıyor hatalarıyla | Microsoft Docs"
description: "502 hatalı ağ geçidi ve Azure App Service içinde barındırılan web uygulamanızda 503 Hizmet kullanılamıyor hatalarıyla ilgili sorunları giderme."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: "502 hatalı ağ geçidi 503 Hizmet kullanılamıyor hatası 503, hata 502"
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a>"502 hatalı ağ geçidi" ve "503 Hizmet kullanılamıyor", Azure web uygulamalarında HTTP hatalarını giderme
"502 hatalı ağ geçidi" ve "503 Hizmet kullanılamıyor" olan yaygın hatalar içinde barındırılan web uygulamanızda [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Bu makalede bu hataları gidermenize yardımcı olur.

Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, başvurabilirsiniz üzerinde Azure uzmanlar hello [MSDN Azure hello ve yığın taşması forumları hello](https://azure.microsoft.com/support/forums/). Alternatif olarak, Azure destek olay dosya. Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/support/options/) ve tıklayın **destek alın**.

## <a name="symptom"></a>Belirti
Toohello web uygulaması göz attığınızda, bir HTTP döndürür "502 hatalı ağ geçidi" hatası ya da bir HTTP "503 Hizmet kullanılamıyor" hatasını.

## <a name="cause"></a>Nedeni
Bu sorun sık sık uygulama düzeyi sorunları tarafından gibi neden olur:

* uzun süren istekleri
* yüksek bellek/CPU kullanarak uygulama
* tooan özel durum kilitlenen uygulama.

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a>Adımları toosolve "502 hatalı ağ geçidi" ve "503 Hizmet kullanılamıyor" hatalarını giderme
Sorun giderme sıralı bir düzende üç farklı görevler ayrılabilir:

1. [İnceleyin ve uygulama davranışı izleme](#observe)
2. [Veri toplama](#collect)
3. [Merhaba sorunu azaltmak](#mitigate)

[App Service Web Apps](/services/app-service/web/) her adımda çeşitli seçenekler sunar.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. İnceleyin ve uygulama davranışı izleme
#### <a name="track-service-health"></a>Hizmet durumu izleme
Microsoft Azure hizmet kesintisi veya performans düşüşü olduğundan her zaman publicizes. Merhaba üzerinde hello hello hizmet durumunu izleyebilirsiniz [Azure Portal](https://portal.azure.com/). Daha fazla bilgi için bkz: [hizmet durumu izleme](../monitoring-and-diagnostics/insights-service-health.md).

#### <a name="monitor-your-web-app"></a>Web uygulamanızı izlemek
Uygulamanızı sorunları yaşıyorsa bu seçenek, toofind çıkışı sağlar. Web uygulamanızın dikey penceresinde hello tıklayın **istekleri ve hataları** döşeme. Merhaba **ölçüm** dikey gösterir, tüm hello ölçümleri ekleyebilirsiniz.

Web uygulamanız için toomonitor isteyebilirsiniz hello ölçümleri bazıları

* Ortalama bellek çalışma kümesi
* Ortalama yanıt süresi
* CPU süresi
* Bellek çalışma kümesi
* İstekler

![HTTP hataları hatalı ağ geçidi 502 ve 503 Hizmet kullanılamıyor çözme doğrultusunda web uygulaması izleme](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

Daha fazla bilgi için bkz.

* [Azure App Service'te Web uygulamalarını izleme](web-sites-monitor.md)
* [Uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a>2. Veri toplama
#### <a name="use-hello-azure-app-service-support-portal"></a>Hello Azure App Service destek portalında kullanın
Web uygulamaları HTTP günlükleri, olay günlükleri, işlem dökümleri ve daha fazla bakarak hello özelliği tootroubleshoot sorunları ilgili tooyour web uygulaması ile sağlar. Bizim destek portalında kullanarak tüm bu bilgilere erişebilen **http://&lt;, uygulama adı >.scm.azurewebsites.net/Support**

Hello Azure App Service desteği portal üç ayrı sekmeler toosupport hello üç adımdan yaygın bir sorun giderme senaryo ile sağlar:

1. Şu anki davranışı inceleyin
2. Tanılama bilgilerini toplama ve yerleşik çözümleyiciler hello çalıştıran analiz eder.
3. Azaltmak

Merhaba sorunu şimdi oluşuyorsa tıklatın **Çözümle** > **tanılama** > **şimdi tanılamak** toocreate sizin için tanılama oturumu hangi HTTP toplar, Olay Görüntüleyicisi günlükleri, bellek dökümleri, PHP Hata günlüklerini ve PHP rapor işlem günlüğe kaydeder.

Merhaba veri toplandığında, ayrıca hello verilerini analiz çalıştırmak ve bir HTML raporu ile sağlayın.

Varsayılan olarak toodownload hello veri istemeniz durumunda, hello D:\home\data\DaaS klasöründe depolanması.

Hello Azure App Service desteği portal hakkında daha fazla bilgi için bkz: [yeni güncelleştirmeler tooSupport Azure Web siteleri için Site uzantısı](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Merhaba Kudu hata ayıklama konsolunu kullanma
Web uygulamaları, hata ayıklama, keşfetme, ortamınız hakkında bilgi almak için JSON bitiş noktaları yanı sıra, dosyaları karşıya yükleme için kullanabileceğiniz bir hata ayıklama konsolu ile birlikte gelir. Bu hello adlandırılır *Kudu konsol* veya hello *SCM Pano* web uygulamanız için.

Giden toohello bağlantısıyla bu panoya erişebilir **https://&lt;, uygulama adı >.scm.azurewebsites.net/**.

Kudu sağlar hello şeylerden bazıları şunlardır:

* Uygulamanız için ortam ayarları
* günlük akışı
* Tanılama dökümü
* hata ayıklama konsolunu Powershell cmdlet'leri ve temel DOS komutları çalıştırabilirsiniz.

Başka bir yararlı Kudu uygulamanızı ilk fırsat özel durum atma durumunda, Kudu kullanabilirsiniz ve hello SysInternals aracı Procdump toocreate bellek dökümleri, özelliğidir. Bu bellek dökümlerini hello işleminin anlık görüntüleri ve genellikle web uygulamanızı daha karmaşık sorunları gidermenize yardımcı olabilir.

Kudu içinde kullanılabilir özellikler hakkında daha fazla bilgi için bkz: [Azure Web siteleri çevrimiçi araçlar hakkında bilmeniz](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Merhaba sorunu azaltmak
#### <a name="scale-hello-web-app"></a>Ölçek hello web uygulaması
Azure App Service'te performansı artırmak ve üretilen işi için uygulamanızı çalıştıran hello ölçek ayarlayabilirsiniz. Bir web uygulamasını kurup ölçeklendirmeyi kapsar iki eylemlerin: fiyatlandırma katmanı ve daha yüksek fiyatlandırma katmanı toohello geçirildikten sonra belirli ayarları yapılandırma yüksek, uygulama hizmeti planı tooa değiştirme.

Ölçeklendirme ile ilgili daha fazla bilgi için bkz: [bir web uygulamasını Azure App Service'te ölçeklendirme](web-sites-scale.md).

Ayrıca, uygulamanızı birden fazla örneği üzerinde toorun seçebilirsiniz. Bu yalnızca ile daha fazla işleme yeteneği sağlar, ancak ayrıca miktar hataya dayanıklılık sağlar. Merhaba işlem bir örneğinde devre dışı kalırsa, hello diğer örneğe hala isteklere hizmet vermeyi devam eder.

Toobe el ile veya otomatik ölçeklendirme hello ayarlayabilirsiniz.

#### <a name="use-autoheal"></a>AutoHeal kullanın
AutoHeal (yapılandırma değişiklikleri, istekleri, bellek tabanlı sınırları veya hello zaman tooexecute bir istek gerekli gibi) seçtiğiniz ayarlarına dayanarak, uygulamanız için hello çalışan işlemi geri dönüştürüldüğünde. Başlangıç saati, çoğu hello en hızlı yolu toorecover bir sorun geri dönüşüm hello işlemidir. Her zaman hello web uygulamasından doğrudan hello Azure portalı içinde yeniden olsa AutoHeal onu otomatik olarak sizin için yapar. Toodo gereken tek şey, web uygulamanız için hello kök web.config dosyasında bazı tetikleyicileri ekleyin. Bu ayarları hello aynı çalışır, Not şekilde uygulamanızı bir .net olsa bile.

Daha fazla bilgi için bkz: [Azure Web siteleri otomatik düzeltme](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Merhaba web uygulaması yeniden
Bu genellikle hello en basit yolu toorecover tek seferlik sorunlardan olur. Merhaba üzerinde [Azure Portal](https://portal.azure.com/), web uygulamanızın dikey penceresinde hello seçenekleri toostop sahip veya uygulamanızı yeniden başlatın.

 ![Uygulama toosolve HTTP hataları 502 hatalı ağ geçidi 503 Hizmet kullanılamıyor ve yeniden başlatın](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

Web uygulamanızı Azure Powershell kullanarak da yönetebilirsiniz. Daha fazla bilgi için bkz. [Azure PowerShell'i Azure Resource Manager ile kullanma](../powershell-azure-resource-manager.md).

