---
title: "Azure web uygulamaları için aaaApplication performansı ile ilgili SSS | Microsoft Docs"
description: "Kullanılabilirlik, performans ve Azure App Service Web Apps özelliğini hello uygulama sorunları hakkında sorular yanıtlar toofrequently alın."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 7f2383743079e4c630fd548b0efd9993029afe11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-performance-faqs-for-web-apps-in-azure"></a>Azure Web uygulamaları için uygulama performansı ile ilgili SSS

Bu makalede hello için uygulama performans sorunları hakkında sorulan sorular (SSS) yanıtlar toofrequently sahip [Azure App Service Web Apps özelliğini](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="why-is-my-app-slow"></a>Neden Uygulamam yavaş mı?

Birden çok faktörünü tooslow uygulama performansı katkıda bulunabilir. Ayrıntılı sorun giderme adımları için bkz [sorun giderme yavaş web uygulaması performans](app-service-web-troubleshoot-performance-degradation.md).

## <a name="how-do-i-troubleshoot-a-high-cpu-consumption-scenario"></a>Yüksek CPU tüketimi senaryo nasıl sorun giderme?

Bazı yüksek CPU tüketimi senaryolarda uygulamanızı gerçekten daha fazla bilgi işlem kaynakları gerektirebilir. Bu durumda, gereken tüm hello kaynakları hello uygulama alır şekilde tooa daha yüksek hizmet katmanı ölçeklendirme göz önünde bulundurun. Diğer durumlarda, hatalı bir döngü veya kodlama bir uygulama tarafından yüksek CPU tüketimi kaynaklanabilir. Daha yüksek CPU kullanımına neden olan içine Insight alma iki parçalı bir işlemdir. İlk olarak, işlem dökümü oluşturun ve hello işlem dökümü analiz edin. Daha fazla bilgi için bkz: [yakalamak ve Web uygulamaları için yüksek CPU tüketimi için döküm dosyasını çözümlemek](https://blogs.msdn.microsoft.com/asiatech/2016/01/20/how-to-capture-dump-when-intermittent-high-cpu-happens-on-azure-web-app/).

## <a name="how-do-i-troubleshoot-a-high-memory-consumption-scenario"></a>Yüksek bellek tüketimine senaryo nasıl sorun giderme?

Bazı yüksek bellek tüketimine senaryolarda uygulamanızı gerçekten daha fazla bilgi işlem kaynakları gerektirebilir. Bu durumda, gereken tüm hello kaynakları hello uygulama alır şekilde tooa daha yüksek hizmet katmanı ölçeklendirme göz önünde bulundurun. Diğer durumlarda, bir bellek sızıntısı hello kodda bir hata neden olabilir. Bir kodlama yöntemi de bellek tüketimi artırabilir. Ne yüksek bellek tüketimi iki parçalı bir işlemdir tetikleme içine Insight alınıyor. İlk olarak, işlem dökümü oluşturun ve hello işlem dökümü analiz edin. Kilitlenme tanılayıcı hello Azure Site uzantı Galerisi gelen hem de şu adımları etkin şekilde gerçekleştirebilirsiniz. Daha fazla bilgi için bkz: [yakalamak ve Web uygulamaları için bir döküm dosyası aralıklı yüksek bellek için analiz](https://blogs.msdn.microsoft.com/asiatech/2016/02/02/how-to-capture-and-analyze-dump-for-intermittent-high-memory-on-azure-web-app/).

## <a name="how-do-i-automate-app-service-web-apps-by-using-powershell"></a>App Service web apps PowerShell kullanarak nasıl otomatikleştirmek?

App Service web apps korumak ve PowerShell cmdlet'leri toomanage kullanın. Bizim blog yayını içinde [PowerShell kullanarak Azure App Service içinde barındırılan web uygulamaları otomatikleştirmek](https://blogs.msdn.microsoft.com/puneetgupta/2016/03/21/automating-webapps-hosted-in-azure-app-service-through-powershell-arm-way/), biz açıklamak nasıl toouse Azure Resource Manager tabanlı PowerShell cmdlet'leri tooautomate ortak görevler. Merhaba blog gönderisi çeşitli web apps yönetim görevleri için örnek kod da sahiptir. Açıklamaları ve tüm App Service web apps cmdlet'leri için sözdizimi için bkz: [AzureRM.Websites](https://docs.microsoft.com/powershell/module/azurerm.websites/?view=azurermps-4.0.0).

## <a name="how-do-i-view-my-web-apps-event-logs"></a>My web uygulamanızın olay günlüklerini nasıl görüntüleyebilirim?

tooview web uygulamanızın olayı günlüğe kaydeder:

1. İçinde tooyour oturum [Kudu Web sitesi](https://*yourwebsitename*.scm.azurewebsites.net).
2. Merhaba menüde seçin **hata ayıklama Konsolu'nda** > **CMD**.
3. Select hello **LogFiles** klasör.
4. tooview olay günlükleri, seçin hello kalem simgesine sonraki çok**eventlog.xml**.
5. toodownload hello günlükleri Hello PowerShell cmdlet'ini çalıştırın, `Save-AzureWebSiteLog -Name webappname`.

## <a name="how-do-i-capture-a-user-mode-memory-dump-of-my-web-app"></a>My web uygulaması, bir kullanıcı modu bellek dökümü nasıl yakalama?

Kullanıcı modu bellek dökümü, web uygulamanızın toocapture:

1. İçinde tooyour oturum [Kudu Web sitesi](https://*yourwebsitename*.scm.azurewebsites.net).
2. Select hello **işlem Gezgini'ni** menüsü.
3. Sağ hello **w3wp.exe** işlem veya Web işi işlem.
4. Seçin **karşıdan bellek dökümü** > **tam döküm**.

## <a name="how-do-i-view-process-level-info-for-my-web-app"></a>Web Uygulamam için nasıl işlem düzeyinde bilgisi görüntüleyebilirim?

Web uygulamanız için işlem düzeyinde bilgilerini görüntülemek için iki seçeneğiniz vardır:

*   Hello Azure portal'de:
    1. Açık hello **işlem Gezgini'ni** hello web uygulaması için.
    2. toosee hello ayrıntıları, select hello **w3wp.exe** işlemi.
*   Merhaba Kudu konsolunda:
    1. İçinde tooyour oturum [Kudu Web sitesi](https://*yourwebsitename*.scm.azurewebsites.net).
    2. Select hello **işlem Gezgini'ni** menüsü.
    3. Hello için **w3wp.exe** işlemi, select **özellikleri**.

## <a name="when-i-browse-toomy-app-i-see-error-403---this-web-app-is-stopped-how-do-i-resolve-this"></a>Toomy uygulama göz attığınızda, "Hatası 403 - bu web uygulaması durduruldu." görüyorum Bu nasıl giderebilirim?

Üç koşul bu hataya neden olabilir:

* Merhaba web uygulaması bir fatura sınırına ulaştı ve sitenizi devre dışı bırakıldı.
* Merhaba web uygulaması hello Portalı'nda durduruldu.
* Merhaba web uygulaması tooa ücretsiz veya paylaşılan ölçek hizmeti planı geçerli olabilecek bir kaynak kota sınırına ulaştı.

toosee neyin neden hello hata ve tooresolve hello sorunu, izleme hello adımları [Web Apps: "Hatası 403 – bu web uygulaması durdurulduğunda"](https://blogs.msdn.microsoft.com/waws/2016/01/05/azure-web-apps-error-403-this-web-app-is-stopped/).

## <a name="where-can-i-learn-more-about-quotas-and-limits-for-various-app-service-plans"></a>Burada çeşitli uygulama hizmeti planları için kotalar ve sınırlar hakkında daha fazla bilgi edinebilirsiniz?

Kotalar ve sınırlar hakkında daha fazla bilgi için bkz: [App Service sınırları](../azure-subscription-service-limits.md#app-service-limits). 

## <a name="how-do-i-decrease-hello-response-time-for-hello-first-request-after-idle-time"></a>Boşta kalma süresi sonra hello ilk istek için hello yanıt süresi nasıl azaltmak?

Varsayılan olarak ayarlanmış bir süre için boşta olmaları durumunda web uygulamaları kaldırılır. Bu şekilde hello sistem kaynakların tasarrufu yapabilirsiniz. Merhaba dezavantajı hello hello web uygulaması kaldırılmadan sonra yanıt toohello ilk istek uzun, tooallow web uygulama tooload hello ve yanıtlara hizmet başlangıç olur. Temel ve standart hizmeti planlarında üzerinde hello kapatabilirsiniz **her zaman açık** ayarı tookeep hello uygulama her zaman yüklenir. Bu hello uygulama boşta kaldıktan sonra uzun yükleme süreleri ortadan kaldırır. toochange hello **her zaman açık** ayarı:

1. Hello Azure portal, tooyour web uygulamasına gidin.
2. Seçin **uygulama ayarları**.
3. İçin **her zaman açık**seçin **üzerinde**.

## <a name="how-do-i-turned-on-failed-request-tracing"></a>Nasıl ı etkinleştirilmiş başarısız istek izlemeyi?

başarısız istek izlemeyi tooturn:

1. Hello Azure portal, tooyour web uygulamasına gidin.
3. Seçin **tüm ayarları** > **tanılama günlükleri**.
4. İçin **başarısız istek izleme**seçin **üzerinde**.
5. **Kaydet**’i seçin.
6. Merhaba web uygulaması dikey penceresinde, seçin **Araçları**.
7. Seçin **Visual Studio Online**.
8. Merhaba ayarı değilse **üzerinde**seçin **üzerinde**.
9. Seçin **Git**.
10. Seçin **Web.config**.
11. System.webServer içinde bu yapılandırma (toocapture belirli bir URL) ekleyin:

    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*api*" />
    <add path="*api*">
    <traceAreas>
    <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
12. tootroubleshoot yavaş performans sorunlarını, bu yapılandırma (istek yakalama hello 30 saniyeden fazla sürüyorsa) ekleyin:
    ```
    <system.webServer>
    <tracing> <traceFailedRequests>
    <remove path="*" />
    <add path="*">
    <traceAreas> <add provider="ASP" verbosity="Verbose" />
    <add provider="ASPNET" areas="Infrastructure,Module,Page,AppServices" verbosity="Verbose" />
    <add provider="ISAPI Extension" verbosity="Verbose" />
    <add provider="WWW Server" areas="Authentication,Security,Filter,StaticFile,CGI,Compression, Cache,RequestNotifications,Module,FastCGI" verbosity="Verbose" />
    </traceAreas>
    <failureDefinitions timeTaken="00:00:30" statusCodes="200-999" />
    </add> </traceFailedRequests>
    </tracing>
    ```
13. toodownload hello başarısız istek izleme, hello [portal](https://portal.azure.com)gidin tooyour Web sitesi.
15. Seçin **Araçları** > **Kudu** > **Git**.
18. Merhaba menüde seçin **hata ayıklama Konsolu'nda** > **CMD**.
19. Select hello **LogFiles** klasörünü ve ardından hello klasörünü ile başlayan bir ada sahip **W3SVC**.
20. toosee hello XML dosyası, select hello kalem simgesine.

## <a name="i-see-hello-message-worker-process-requested-recycle-due-toopercent-memory-limit-how-do-i-address-this-issue"></a>Selamlama iletisine bakın "çalışan işlemi geri dönüşüm isteğinde son too'Percent bellek ' sınırı." Bu sorunu nasıl ele?

Merhaba en fazla kullanılabilir bellek miktarı 32 bitlik bir işlem için (hatta bir 64-bit işletim sisteminde) 2 GB'tır. Varsayılan olarak, hello çalışan işlemi too32-App Service içinde bitini (eski web uygulamalarıyla uyumluluk) ayarlanır.

Too64 bit işlemleri hello ek belleğe Web çalışanı rolünüz yararlanabilir şekilde değiştirmeyi düşünün. Bu web uygulamasını yeniden başlatır, böylece buna uygun şekilde zamanlayın.

Ayrıca bir 64-bit ortamı bir temel veya standart hizmet planı gerektirdiğini unutmayın. Ücretsiz ve paylaşılan planları her zaman bir 32 bit ortamda çalıştırılabilir.

Daha fazla bilgi için bkz: [App Service'te web uygulamalarını yapılandırma](https://docs.microsoft.com/azure/app-service-web/web-sites-configure).

## <a name="why-does-my-request-time-out-after-240-seconds"></a>Neden my isteği zaman aşımına 240 saniye sonra?

Azure yük dengeleyici, dört dakikalık varsayılan boşta kalma zaman aşımı ayarının. Bu genellikle bir web isteği için makul yanıt zaman sınırı içindir. Web uygulamanızın arka plan işleme gerektiriyorsa, Azure Web işleri kullanmanızı öneririz. Hello Azure web uygulaması Web işleri çağırabilir ve arka plan işlemi tamamlandığında bildirim. Web işleri, kuyruklar ve Tetikleyicileri dahil olmak üzere birden çok yöntemler arasından seçim yapabilirsiniz.

Web işleri arka plan işleme için tasarlanmıştır. WebJob içinde istediğiniz kadar arka plan işlemi yapabilirsiniz. Web işleri hakkında daha fazla bilgi için bkz: [arka plan görevleri ile Web işleri çalıştırma](https://docs.microsoft.com/azure/app-service-web/web-sites-create-web-jobs).

## <a name="aspnet-core-applications-that-are-hosted-in-app-service-sometimes-stop-responding-how-do-i-fix-this-issue"></a>App Service içinde bazen barındırılan ASP.NET Core uygulamaları yanıt vermiyor. Bu sorunu nasıl düzeltirim?

Daha önceki bir bilinen bir sorun [Kestrel sürüm](https://github.com/aspnet/KestrelHttpServer/issues/1182) uygulama hizmeti toointermittently vermemesine içinde barındırılan bir ASP.NET Core 1.0 uygulama neden olabilir. Ayrıca, bu iletiyi görebilirsiniz: "Merhaba belirtilen CGI uygulaması, bir hata ve hello sonlandırıldı sunucu hello işlemi karşılaştı."

Bu sorun Kestrel sürüm 1.0.2 düzeltilmiştir. Bu sürüm hello ASP.NET Core 1.0.3 güncelleştirme dahil edilir. tooresolve Bu sorun, uygulama bağımlılıkları toouse Kestrel 1.0.2 güncelleştirdiğinizden emin olun. Merhaba blog gönderisinde açıklandığı iki geçici çözümlerden birini kullanmanız alternatif olarak, [ASP.NET Core 1.0 yavaş performans sorunlarını App Service web apps](https://blogs.msdn.microsoft.com/waws/2016/12/11/asp-net-core-slow-perf-issues-on-azure-websites).


## <a name="i-cant-find-my-log-files-in-hello-file-structure-of-my-web-app-how-can-i-find-them"></a>My web uygulamasının hello dosya yapısı içinde my günlük dosyalarını bulmak olamaz. Bunları nasıl bulabilirim?

App Service'in hello yerel önbelleği özelliğini kullanırsanız, hello LogFiles hello klasör yapısını ve uygulama hizmeti Örneğiniz için veri klasörleri etkilenir. Yerel önbelleği kullanıldığında, alt klasörler hello depolama LogFiles ve veri klasörleri oluşturulur. Merhaba alt klasörleri kullanım hello adlandırma deseni "benzersiz tanımlayıcı" + zaman damgası. Her alt hangi hello web uygulaması çalıştıran veya çalıştırıldı tooa VM örneğine karşılık gelir.

toodetermine yerel önbellek, kullanmakta olduğunuz bulunup bulunmadığını uygulama hizmetiniz **uygulama ayarları** sekmesi. Yerel önbelleği kullanılıyorsa, uygulama ayarı hello `WEBSITE_LOCAL_CACHE_OPTION` çok ayarlanır`Always`. Merhaba yerel önbelleği hakkında daha fazla bilgi için bkz: [uygulama hizmeti yerel önbelleğinden genel bakış](https://docs.microsoft.com/azure/app-service/app-service-local-cache).

Yerel önbelleği kullanmıyorsanız ve bu sorunu yaşıyorsanız, bir destek isteği gönderin.

## <a name="i-see-hello-message-an-attempt-was-made-tooaccess-a-socket-in-a-way-forbidden-by-its-access-permissions-how-do-i-resolve-this"></a>Selamlama iletisine bakın "bir girişim yapıldı tarafından erişim izinlerini Yasak şekilde yuva tooaccess yapılan." Bu nasıl giderebilirim?

Merhaba giden TCP bağlantılarını hello VM örneğinde azalırsa genellikle bu hata oluşur. App Service içinde her bir VM örneği için yapılan giden bağlantılar hello sayısı için sınırlar uygulanır. Daha fazla bilgi için bkz: [arası VM sayısal sınırlar](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#cross-vm-numerical-limits).

Bu hata ayrıca uygulamanızdan tooaccess yerel bir adres deneyin oluşabilir. Daha fazla bilgi için bkz: [yerel adres istekleri](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox#local-address-requests).

Web uygulamanızda giden bağlantılar hakkında daha fazla bilgi için bkz: hello blog gönderisi hakkında [bağlantıları tooAzure Web siteleri giden](http://www.freekpaans.nl/2015/08/starving-outgoing-connections-on-windows-azure-web-sites/).

## <a name="how-do-i-use-visual-studio-tooremote-debug-my-app-service-web-app"></a>Visual Studio tooremote hata ayıklama App Service web Uygulamam nasıl kullanabilirim?

Toodebug Visual Studio'yu kullanarak web uygulamanızı nasıl görürüm gösteren ayrıntılı kılavuz [uzaktan hata ayıklama, App Service web uygulaması](https://blogs.msdn.microsoft.com/benjaminperkins/2016/09/22/remote-debug-your-azure-app-service-web-app/).
