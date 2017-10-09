---
title: "aaaMonitor canlı bir ASP.NET web uygulaması Azure Application Insights ile | Microsoft Docs"
description: "Yeniden dağıtmadan web sitesinin performansını izleme. Şirket içinde, sanal makinelerde veya Azure üzerinde ASP.NET web uygulamaları ile çalışır."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a>Application Insights ile çalışma zamanında web uygulamalarını izleme


Azure Application Insights, canlı web uygulamasıyla toomodify gerek kalmadan izleme ya da kodunuzu yeniden dağıtın. Uygulamalarınız şirket içi IIS sunucusu tarafından barındırılıyorsa, Durum İzleyicisi’ni yükleyin. Azure web uygulamaları olduğunuz veya bir Azure VM çalıştırmak, Application Insights hello Azure Denetim Masası'ndan izleme geçiş yapabilirsiniz. ([Canlı J2EE web uygulamaları](app-insights-java-live.md) ve [Azure Cloud Services](app-insights-cloudservices.md) izleme hakkında ayrı makaleler de vardır.) [Microsoft Azure](http://azure.com) aboneliğiniz olması gerekir.

![örnek grafikler](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

Üç yollar tooapply Application Insights tooyour .NET web uygulamalarının seçenekleriniz vardır:

* **Derleme süresi:** [Ekle hello Application Insights SDK'sı] [ greenbrown] tooyour web uygulama kodu.
* **Çalışma zamanı:** yeniden oluşturma ve hello kod dağıtarak, aşağıda açıklandığı gibi hello sunucuda web uygulamanızı izleme.
* **Her ikisi:** web uygulaması kodunuza hello SDK derleme ve hello çalışma zamanı uzantıları de geçerlidir. Merhaba her iki seçenek en iyi alın.

Burada, her yöntemle kazanacaklarınızın bir özeti verilmiştir:

|  | Derleme zamanı | Çalışma zamanı |
| --- | --- | --- |
| İstekler ve özel durumlar |Evet |Evet |
| [Daha ayrıntılı özel durumlar](app-insights-asp-net-exceptions.md) | |Yes |
| [Bağımlılık tanılaması](app-insights-asp-net-dependencies.md) |.NET 4.6+ üzerinde ancak daha az ayrıntılı |Evet, tam ayrıntılı: sonuç kodları, SQL komut metni, HTTP fiili|
| [Sistem performans sayaçları](app-insights-performance-counters.md) |Evet |Evet |
| [Özel telemetri için API][api] |Evet |Hayır |
| [İzleme günlüğü tümleştirmesi](app-insights-asp-net-trace-logs.md) |Evet |Hayır |
| [Sayfa görünümü ve kullanıcı verileri](app-insights-javascript.md) |Evet |Hayır |
| Toorebuild kodu gerekli |Evet | Hayır |


## <a name="monitor-a-live-azure-web-app"></a>Canlı bir Azure web uygulamasını izleme

Uygulamanız bir Azure web Service'in, burada çalışıp çalışmadığını nasıl izleme tooswitch:

* Azure'da hello uygulamanın Denetim Masası'Application Insights'ı seçin.

    ![Bir Azure web uygulaması için Application Insights’ı ayarlama](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* Merhaba Application Insights Özet sayfası açıldığında, hello alt tooopen hello tam Application Insights kaynağı hello bağlantısını tıklatın.

    ![TooApplication Insights'ı tıklatın](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

[Bulut ve VM uygulamalarını izleme](app-insights-azure.md).

### <a name="enable-client-side-monitoring-in-azure"></a>Azure'da istemci tarafı izlemeyi etkinleştirme

Azure'da Application Insights'ı etkinleştirdiyseniz sayfa görüntülemesi ve kullanıcı telemetrisi ekleyebilirsiniz.

1. Ayarlar > Uygulama Ayarları'nı seçin.
2.  Uygulama Ayarları'nın altında yeni bir anahtar değer çifti ekleyin: 
   
    Anahtar: `APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    Değer:`true`
3. **Kaydet** hello ayarları ve **yeniden** uygulamanızı.

Merhaba Application Insights JavaScript SDK'sı şimdi her web sayfasına eklenmiş.

## <a name="monitor-a-live-iis-web-app"></a>Canlı bir IIS web uygulamasını izleme

Uygulamanız bir IIS sunucusunda barındırılıyorsa, Durum İzleyici’yi kullanarak Application Insights’ı etkinleştirin.

1. IIS web sunucunuzda yönetici kimlik bilgileriyle oturum açın.
2. Application Insights Durum İzleyicisi zaten yüklü değilse, indirme ve hello çalıştırma [Durum İzleyicisi yükleyici](http://go.microsoft.com/fwlink/?LinkId=506648) (veya çalıştırmak [Web Platformu yükleyicisi](https://www.microsoft.com/web/downloads/platform.aspx) ve uygulama Öngörüler durumu da arayın İzleyici).
3. Durum İzleyicisi'nde hello yüklü web uygulaması veya toomonitor istediğiniz Web sitesi seçin. Azure kimlik bilgilerinizle oturum açın.

    Merhaba kaynak toosee hello sonuçları hello Application Insights portalında istediğiniz yapılandırın. (Normalde, en iyi toocreate yeni bir kaynak olur. Bu uygulama için zaten [web testleriniz][availability] veya [istemci izleme][client] özelliği varsa mevcut bir kaynağı seçin.) 

    ![Uygulama ve kaynak seçin.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. IIS’yi yeniden başlatın.

    ![Merhaba iletişim hello üstündeki yeniden Başlat'ı seçin.](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    Web hizmetiniz kısa bir süre kesintiye uğrar.

## <a name="customize-monitoring-options"></a>İzlemeyi özelleştirme seçenekleri

Application Insights etkinleştirilmesi ekler DLL'ler ve Applicationınsights.config tooyour web uygulaması. Yapabilecekleriniz [hello .config dosyasını düzenleyin](app-insights-configuration-with-applicationinsights-config.md) toochange bazı hello seçenekleri.

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a>Uygulamanızı yeniden yayımladığınızda, Application Insights’ı yeniden etkinleştirin

Uygulamanızı yeniden yayımlamadan önce göz önünde bulundurun [Visual Studio'da Application Insights toohello kod ekleme][greenbrown]. Daha ayrıntılı telemetri ve hello özelliği toowrite özel telemetri elde edersiniz.

Toore istiyorsanız-Application Insights toohello kodu eklemeden yayımlama, hello dağıtım işlemini hello DLL'leri Sil ve Applicationınsights.config hello gelen yayımlanan web sitesi unutmayın. Bu nedenle:

1. ApplicationInsights.config dosyasını düzenlediyseniz, uygulamanızı yeniden yayımlamadan önce bir kopyasını alın.
2. Uygulamanızı yeniden yayımlayın.
3. Application Insights izlemeyi yeniden etkinleştirin. (Merhaba uygun yöntemi kullanın: hello Azure web uygulaması Denetim Masası veya bir IIS konaktaki Durum İzleyicisi Merhaba.)
4. Merhaba .config dosyası üzerinde gerçekleştirilen herhangi bir düzenleme yeniden devreye sokmanız.


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a>Application Insights çalışma zamanı yapılandırma sorunlarını giderme

### <a name="cant-connect-no-telemetry"></a>Bağlanamıyor musunuz? Telemetri yok mu?

* Açık [hello gerekli giden bağlantı noktaları](app-insights-ip-addresses.md#outgoing-ports) sunucunuzun güvenlik duvarı tooallow Durum İzleyicisi toowork içinde.

* Durum İzleyicisi’ni açın ve sol bölmede uygulamanızı seçin. Bu uygulamada hello "Yapılandırma bildirimleri" bölümü için herhangi bir tanılama iletisi olup olmadığını denetleyin:

  ![Merhaba performans dikey toosee istek, yanıt süresi, bağımlılık ve diğer verileri açın](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* "Yetersiz izinler" hakkında bir ileti görürseniz, hello sunucuda hello aşağıdakileri deneyin:
  * IIS Yöneticisi'nde, uygulama havuzunu seçin açmak **Gelişmiş ayarları**ve altında **işlem modeli** hello kimliğini not edin.
  * Bilgisayar Yönetimi Denetim Masası'nda bu kimlik toohello Performans İzleyicisi kullanıcıları grubuna ekleyin.
* Sunucunuza yüklenmiş MMA/SCOM (System Center Operations Manager) varsa bazı sürümler çakışabilir. Hem SCOM'u hem de Durum İzleyicisi'ni kaldırın ve hello en son sürümleri yeniden yükleyin.
* Bkz. [Sorun giderme][qna].

## <a name="system-requirements"></a>Sistem Gereksinimleri
Sunucuda Application Insights Durum İzleyicisi için işletim sistemi desteği:

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows server 2012 R2
* Windows Server 2016

en son SP ve .NET Framework 4.5 ile

Merhaba istemci tarafında: Windows 7, 8, 8.1 ve 10, .NET Framework 4.5 ile yeniden

IIS desteği: IIS 7, 7.5, 8, 8.5 (IIS gereklidir)

## <a name="automation-with-powershell"></a>PowerShell ile Automation
IIS sunucunuzda PowerShell'i kullanarak izlemeyi başlatabilir ve durdurabilirsiniz.

İlk hello Application Insights modülünü içeri aktarın:

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

Hangi uygulamaların izlenmekte olduğunu öğrenin:

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* `-Name`Bir web uygulaması adı (isteğe bağlı) hello.
* Görüntüler, bu IIS sunucusundaki her web uygulaması (veya uygulama adlı hello) Application Insights izleme durumunu hello.
* Her uygulama için `ApplicationInsightsApplication` döndürür:

  * `SdkState==EnabledAfterDeployment`: Uygulama izlenmektedir ve çalışma zamanında hello Durum İzleyicisi aracıyla veya tarafından izlendi `Start-ApplicationInsightsMonitoring`.
  * `SdkState==Disabled`: hello uygulama için Application Insights değil işaretlenir. Hiçbir zaman izlendi ya da çalışma zamanı izlemesi devre dışı hello Durum İzleyicisi aracıyla veya ile `Stop-ApplicationInsightsMonitoring`.
  * `SdkState==EnabledByCodeInstrumentation`: hello uygulama izlenmiş hello SDK toohello kaynak kodu ekleyerek. SDK’si güncelleştirilemez veya durdurulamaz.
  * `SdkVersion`Bu uygulamanın izlenmesi için kullanımda Hello sürümünü gösterir.
  * `LatestAvailableSdkVersion`şu anda kullanılabilir Hello sürüm hello NuGet galerisinde gösterir. tooupgrade hello uygulamanın toothis sürüm, kullanım `Update-ApplicationInsightsMonitoring`.

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* `-Name`IIS'de hello uygulamasının Hello adı
* `-InstrumentationKey`Merhaba hello sonuçları toobe görüntülenmesini istediğiniz Application Insights kaynağı ikey hello.
* Bu cmdlet yalnızca henüz izlenmemiş uygulamaları etkiler; başka bir deyişle zaten işaretlendiğine değil - diğer bir deyişle, SdkState==NotInstrumented.

    Merhaba cmdlet, zaten izlenmiş olan uygulamayı etkilemez. Bırakmaz hello uygulama hello SDK toohello kodu ekleyerek derleme zamanında izlenmektedir olup olmadığını önemli, veya bu cmdlet'in önceki bir kullanımıyla çalışma zamanı sırasında.

    Merhaba SDK kullanılan sürümü tooinstrument hello son çoğu hello sürüm toothis Sunucusu'nu indirdiğiniz uygulamasıdır.

    toodownload hello en son sürümü, Update-Applicationınsightsversion kullanın.
* Başarılı bir şekilde `ApplicationInsightsApplication` döndürür. Başarısız olursa izleme toostderr günlüğe kaydeder.

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* `-Name`IIS'de bir uygulamanın Hello adı
* `-All` Bu IIS sunucusunda, şu koşulu sağlayan tüm uygulamaları izlemeyi durdurur: `SdkState==EnabledAfterDeployment`
* Merhaba izlemesini durdurur, belirtilen uygulamaların ve izlemeyi kaldırır. Durum izleme aracını veya Start-Applicationınsightsapplication kullanarak çalışma zamanında izleme eklenmiş uygulamalar hello için yalnızca çalışır. (`SdkState==EnabledAfterDeployment`)
* ApplicationInsightsApplication döndürür.

`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]

* `-Name`: IIS'de web uygulamasının hello adı.
* `-InstrumentationKey` (İsteğe bağlı.) Bu toochange hello kaynak toowhich hello uygulamanın telemetri gönderildiği kullanın.
* Bu cmdlet:
  * Uygulama toohello hello SDK sürümü adlı yükseltmeler hello toothis makine en son indirilen. (Yalnızca `SdkState==EnabledAfterDeployment` ise çalışır)
  * İzleme anahtarını sağlarsanız, uygulama adlı hello yeniden yapılandırılan toosend telemetri toohello aynı anahtarla kaynaktır. (`SdkState != Disabled` ise çalışır)

`Update-ApplicationInsightsVersion`

* Merhaba en son Application Insights SDK'sı toohello sunucusu yükler.

## <a name="questions"></a>Durum İzleyicisi hakkında sorular

### <a name="what-is-status-monitor"></a>Durum İzleyicisi nedir?

IIS web sunucunuza yüklediğiniz bir masaüstü uygulamasıdır. Web uygulamalarını izleyip yapılandırmanıza yardımcı olur. 

### <a name="when-do-i-use-status-monitor"></a>Durum İzleyicisi’ni ne zaman kullanırım?

* zaten çalışıyor olsa bile herhangi bir web uygulamanız IIS sunucunuzda - çalıştıran uygulaması tooinstrument.
* Silinmiş web uygulamaları için ek telemetri tooenable [hello Application Insights SDK'sı ile oluşturulan](app-insights-asp-net.md) derleme zamanında. 

### <a name="can-i-close-it-after-it-runs"></a>Çalıştıktan sonra kapatabilir miyim?

Evet. Seçtiğiniz hello Web siteleri izlenmiş sonra kapatabilirsiniz.

Telemetriyi tek başına toplamaz. Yalnızca hello web uygulamaları yapılandırır ve bazı izinleri ayarlar.

### <a name="what-does-status-monitor-do"></a>Durum İzleyicisi ne yapar?

Bir web uygulaması için Durum İzleyicisi tooinstrument seçtiğinizde:

* İndirir ve hello web uygulamanızın ikili dosyaları klasörüne hello Application Insights derlemeler ve .config dosyasına yerleştirir.
* Değiştirir `web.config` tooadd hello uygulama Öngörüler HTTP izleme modülü.
* CLR toocollect bağımlılık çağrıları profil sağlar.

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a>Merhaba uygulama güncelleştirdiğinizde toorun Durum İzleyicisi ihtiyacım var mı?

Artımlı olarak dağıtmanız durumunda gerekli değildir. 

Hello hello 'var olan dosyaları silin' seçeneği belirlerseniz işlem yayımlama, toore çalıştırma Durum İzleyicisi tooconfigure Application Insights gerekir.

### <a name="what-telemetry-is-collected"></a>Hangi telemetri toplanır?

Durum İzleyicisi'ni kullanarak yalnızca çalışma zamanında izlediğiniz uygulamalar için:

* HTTP istekleri
* Toodependencies çağırır
* Özel durumlar
* Performans sayaçları

Derleme zamanında zaten izlenmekte olan uygulamalar için:

 * İşlem sayaçları.
 * Bağımlılık çağrıları (.NET 4.5); bağımlılık çağrılarındaki dönüş değerleri (.NET 4.6).
 * Özel durum yığın izleme değerleri.

[Daha fazla bilgi](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next"></a>Sonraki adımlar

Telemetrinizi görüntüleyin:

* [Ölçümleri keşfedin](app-insights-metrics-explorer.md) toomonitor performansı ve kullanımı
* [Olayları ve günlükleri arayın] [ diagnostic] toodiagnose sorunları
* Daha gelişmiş sorgular için [analiz](app-insights-analytics.md)
* [Panolar oluşturun](app-insights-dashboards.md)

Daha fazla telemetri ekleyin:

* [Web testleri oluşturma] [ availability] toomake sitenizin Canlı kaldığından emin.
* [Web istemcisi telemetrisini ekleyin] [ usage] web sayfası koduna ve eklediğiniz toolet toosee özel durumlar çağrıları izleme.
* [Application Insights SDK'sı tooyour kodu ekleyin] [ greenbrown] izleme ekleyin ve oturum çağrıları

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
