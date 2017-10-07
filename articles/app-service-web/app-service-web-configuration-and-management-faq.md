---
title: "Azure web uygulamaları için aaaConfiguration sık sorulan sorular | Microsoft Docs"
description: "Yapılandırması ve yönetimi sorunları hakkında Azure App Service'in Web Apps özelliği hello sorular yanıtlar toofrequently alın."
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
ms.openlocfilehash: 5aa405582813291a4aaf144d2f821ecb20a5edcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-faqs-for-web-apps-in-azure"></a>Azure Web uygulamalarının yapılandırması ve Yönetimi SSS

Bu makalede Merhaba yapılandırması ve yönetimi sorunları hakkında sorulan sorular (SSS) yanıtlar toofrequently sahip [Azure App Service Web Apps özelliğini](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="are-there-limitations-i-should-be-aware-of-if-i-want-toomove-app-service-resources"></a>Toomove App Service kaynakları istiyorsanız farkında olmalıdır sınırlamalar var mı?

Toomove uygulama hizmeti kaynakları tooa yeni kaynak grubu veya abonelik planı varsa bazı sınırlamalar toobe farkında. Daha fazla bilgi için bkz: [App Service sınırlamalar](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="how-do-i-use-a-custom-domain-name-for-my-web-app"></a>Web Uygulamam için özel etki alanı adı nasıl kullanabilirim?

Özel etki alanı adı, Azure web uygulaması ile kullanma hakkında toocommon soruları yanıtlar görmek için bizim yedi dakikalık video [özel etki alanı ekleme](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name). Merhaba video sunar nasıl bir kılavuz tooadd bir özel etki alanı adı. Açıkladığı nasıl toouse hello yerine kendi URL *. azurewebsites.net URL App Service web uygulaması ile. Ayrıntılı bilgileri de görebilirsiniz [nasıl toomap bir özel etki alanı adı](web-sites-custom-domain-name.md).


## <a name="how-do-i-purchase-a-new-custom-domain-for-my-web-app"></a>Web Uygulamam için nasıl yeni bir özel etki alanı satın?

toopurchase ve App Service web uygulamanız için özel bir etki alanı ayarlama nasıl görürüm toolearn [satın alın ve App Service'te özel etki alanı adı yapılandırma](custom-dns-web-site-buydomains-web-app.md).


## <a name="how-do-i-upload-and-configure-an-existing-ssl-certificate-for-my-web-app"></a>Nasıl karşıya yükleme ve web Uygulamam için mevcut bir SSL sertifikası yapılandırma?

tooupload ve bir var olan özel SSL sertifikası ayarlama nasıl görürüm toolearn [varolan özel SSL sertifika tooan Azure web uygulaması bağlama](app-service-web-tutorial-custom-ssl.md#upload).


## <a name="how-do-i-purchase-and-configure-a-new-ssl-certificate-in-azure-for-my-web-app"></a>Nasıl satın alın ve web Uygulamam için Azure'da yeni bir SSL sertifikası yapılandırma?

toopurchase ve App Service web uygulamanız için bir SSL sertifikası ayarlama nasıl görürüm toolearn [bir SSL sertifikası tooyour App Service uygulaması eklemek](web-sites-purchase-ssl-web-site.md).


## <a name="how-do-i-move-application-insights-resources"></a>Application Insights kaynakları nasıl taşıyabilirim?

Azure Application Insights hello taşıma işlemi şu anda desteklemiyor. Özgün kaynak grubunuz Application Insights kaynağı içeriyorsa, bu kaynak taşınamıyor. Bir App Service uygulaması toomove çalıştığınızda hello Application Insights kaynağı eklerseniz, tüm hello işlemi başarısız taşıyın. Ancak, Application Insights ve hello uygulama hizmeti planı içinde toobe gerek yoktur hello app hello uygulama toofunction için aynı kaynak grubunda doğru hello.

Daha fazla bilgi için bkz: [App Service sınırlamalar](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="where-can-i-find-a-guidance-checklist-and-learn-more-about-resource-move-operations"></a>Burada ı kılavuzu denetim bulabilir ve bilgi kaynağı hakkında daha fazla taşıma işlemlerini?

[App Service sınırlamalar](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations) nasıl toomove kaynakları tooeither yeni bir abonelik veya tooa yeni kaynak grubu hello aynı gösterir abonelik. Merhaba kaynak taşıma denetim listesi hakkında bilgi almak, hangi hizmetlerin hello taşıma işlemi desteklemek ve App Service sınırlamalar ve diğer konular hakkında daha fazla bilgi öğrenin.

## <a name="how-do-i-set-hello-server-time-zone-for-my-web-app"></a>Web Uygulamam için nasıl hello sunucusunun saat dilimini ayarlar?

web uygulamanız için tooset hello sunucu saat dilimi:

1. Merhaba, uygulama hizmeti aboneliğinizdeki Azure portal'ın toohello Git **uygulama ayarları** menüsü.
2. Altında **uygulama ayarları**, bu ayarı ekleyin:
    * Anahtar WEBSITE_TIME_ZONE =
    * Değer = *istediğiniz hello saat dilimi*
3. **Kaydet**’i seçin.

## <a name="why-do-my-continuous-webjobs-sometimes-fail"></a>Neden my sürekli Webjob'lar bazen başarısız?

Varsayılan olarak ayarlanmış bir süre için boşta olmaları durumunda web uygulamaları kaldırılır. Bu hello sistem kaynakların tasarrufu sağlar. Temel ve standart planlarda üzerinde hello kapatabilirsiniz **her zaman açık** yüklenen tüm hello zaman tookeep hello web uygulamasını ayarlama. Web uygulamanızı sürekli Webjob'lar çalıştırıyorsa, açmanız **her zaman açık**, ya da hello Web işleri çalışmıyor güvenilir. Daha fazla bilgi için bkz: [sürekli olarak çalışan bir WebJob oluşturma](web-sites-create-web-jobs.md#CreateContinuous).

## <a name="how-do-i-get-hello-outbound-ip-address-for-my-web-app"></a>Web Uygulamam hello giden IP adresi nasıl sağlarım?

web uygulamanız için giden IP adreslerinin tooget hello listesi:

1. Merhaba, web uygulaması dikey penceresinde Azure portal'ın toohello Git **özellikleri** menüsü.
2. Arama **giden IP adreslerini**.

Merhaba giden IP adreslerinin listesi görüntülenir.

Web sitenizin uygulama hizmeti ortamı'nda PowerApps, toolearn nasıl barındırılıyorsa tooget giden IP adresini bakın [giden ağ adresleri](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses).

## <a name="how-do-i-get-a-reserved-or-dedicated-inbound-ip-address-for-my-web-app"></a>Web Uygulamam için nasıl bir ayrılmış ya da ayrılmış gelen IP adresi elde?

tooset tooyour Azure uygulaması Web sitesine yapılan gelen çağrıları için adanmış veya ayrılmış bir IP adresini yükleyin ve bir IP tabanlı SSL sertifikası yapılandırın.

Bu toouse ayrılmış bir not veya ayrılmış IP adresi gelen çağrıları için bir temel veya daha yüksek hizmet planı uygulama hizmeti planınızın olması gerekir.

## <a name="can-i-export-my-app-service-certificate-toouse-outside-azure-such-as-for-a-website-hosted-elsewhere"></a>Azure dışında my uygulama hizmeti sertifika toouse gibi bir Web sitesi için başka bir yerde barındırılan dışa aktarabilirsiniz? 

Uygulama Hizmeti sertifikaları Azure kaynaklarını olarak kabul edilir. Bunlar Azure hizmetlerinizi dışında hedeflenen toouse değildir. Bunları Azure dışında toouse veremiyor. Daha fazla bilgi için bkz: [uygulama hizmeti sertifikaları ve özel etki alanları için SSS](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).

## <a name="can-i-export-my-app-service-certificate-toouse-with-other-azure-cloud-services"></a>Diğer Azure bulut Hizmetleri ile my uygulama hizmeti sertifika toouse dışa aktarabilirsiniz?

Merhaba portal, Azure anahtar kasası tooApp hizmet uygulamaları aracılığıyla bir uygulama hizmeti sertifikası dağıtmak için birinci sınıf bir deneyim sağlar. Ancak, biz müşteriler toouse gelen istekleri hello App Service platformu dışında bu sertifikaları Örneğin, Azure sanal makinelerle alıyor olabilir. toolearn toocreate uygulama hizmetiniz yerel bir PFX kopyasını nasıl sertifika diğer Azure kaynaklarıyla hello sertifika kullanabilmek için bkz: [yerel bir uygulama hizmeti Sertifika PFX kopyasını oluşturmak](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).

Daha fazla bilgi için bkz: [uygulama hizmeti sertifikaları ve özel etki alanları için SSS](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).


## <a name="why-do-i-see-hello-message-partially-succeeded-when-i-try-tooback-up-my-web-app"></a>Web Uygulamam tooback çalıştığımda neden selamlama iletisine "Kısmen başarılı oldu" görüyor?

Bir ortak yedekleme hatası bazı dosyaları hello uygulama tarafından kullanılmakta olan nedenidir. Merhaba yedekleme gerçekleştirirken kullanılmakta olan dosyaları kilitlenir. Bu, bu dosyaları yedeklenen engeller ve bir "Kısmen başarılı oldu" durumu sağlayabilir. Büyük olasılıkla bu dosya hello yedekleme işleminden hariç tutarak oluşmasını engelleyebilir. Yalnızca gerekli olanla yukarı tooback seçebilirsiniz. Daha fazla bilgi için bkz: [yalnızca önemli kısımlarını Azure web uygulamaları sitenizle hello yedekleme](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/).

## <a name="how-do-i-remove-a-header-from-hello-http-response"></a>HTTP yanıtı hello nasıl üstbilgi kaldırılsın mı?

Merhaba HTTP yanıtı tooremove hello üstbilgileri sitenizin web.config dosyasını güncelleştirin. Daha fazla bilgi için bkz: [kaldırmak, Azure Web siteleri standart sunucu üstbilgilerinde](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/).

## <a name="is-app-service-compliant-with-pci-standard-30-and-31"></a>Uygulama hizmeti PCI standart 3.0 ve 3.1 ile uyumlu mu?

Şu anda hello Web uygulamaları, Azure App Service uyumlu PCI veri güvenliği standardı (DSS) sürüm 3.0 düzey 1 özelliğidir. PCI DSS sürüm 3.1 bizim yol haritası üzerinde ' dir. Planlama zaten nasıl hello son standart benimsenmesi devam edecek için işleniyor.

PCI DSS sürüm 3.1 sertifika Aktarım Katmanı Güvenliği (TLS) 1.0 devre dışı bırakılması gerekir. Şu anda, TLS 1.0 devre dışı bırakma çoğu uygulama hizmeti planları için bir seçenek değil. Ancak, uygulama hizmeti ortamı kullanın veya istekli toomigrate, iş yükü tooApp hizmeti ortamı olduğundan, ortamınızın daha fazla denetim elde edebilirsiniz. Bu, TLS 1.0 Azure desteği ile iletişim kurarak devre dışı bırakma içerir. Yakın zaman Hello Biz bu ayarları erişilebilir toousers toomake planlayın.

Daha fazla bilgi için bkz: [PCI standart 3.0 ve 3.1 ile Microsoft Azure App Service web uygulama uyumluluğu](https://support.microsoft.com/help/3124528).

## <a name="how-do-i-use-hello-staging-environment-and-deployment-slots"></a>Hazırlama ortamı ve dağıtım yuvaları hello nasıl kullanabilirim?

Web uygulaması tooApp hizmetini dağıttığınızda, standart ve Premium uygulama hizmeti planlarında tooa ayrı bir dağıtım yuvası toohello varsayılan üretim yuvasına yerine dağıtabilirsiniz. Dağıtım yuvaları, kendi ana bilgisayar adları olan canlı web uygulamalardır. Web uygulaması içerik ve yapılandırma öğeleri hello üretim yuvası da dahil olmak üzere iki dağıtım yuvası arasında değişiklik yapılabilir.

Dağıtım yuvaları kullanma hakkında daha fazla bilgi için bkz: [hazırlama bir uygulama hizmeti ortamında ayarlama](web-sites-staged-publishing.md).

## <a name="how-do-i-access-and-review-webjob-logs"></a>Nasıl erişmek ve Web işi günlüklerini gözden geçirin?

tooreview WebJob kaydeder:

1. İçinde tooyour oturum [Kudu Web sitesi](https://*yourwebsitename*.scm.azurewebsites.net).
2. Merhaba Web işi seçin.
3. Select hello **geçiş çıktı** düğmesi.
4. toodownload hello çıktı dosyası, select hello **karşıdan** bağlantı.
5. Tek tek çalıştırmalarında seçin **tek tek çağırma**.
6. Select hello **geçiş çıktı** düğmesi.
7. Select hello indirme bağlantısı.

## <a name="im-trying-toouse-hybrid-connections-with-sql-server-why-do-i-see-hello-message-systemoverflowexception-arithmetic-operation-resulted-in-an-overflow"></a>SQL Server ile toouse karma bağlantılar çalışıyorum. Neden hello iletisini görüyorum "System.OverflowException: Aritmetik işlem taşması ile sonuçlandı"?

Karma bağlantılar tooaccess SQL Server kullanıyorsanız, Microsoft .NET güncelleştirmesi 10 Mayıs 2016 bağlantıları toofail neden olabilir. Bu iletiyi görebilirsiniz:

```
Exception: System.Data.Entity.Core.EntityException: hello underlying provider failed on Open. —> System.OverflowException: Arithmetic operation resulted in an overflow. or (64 bit Web app) System.OverflowException: Array dimensions exceeded supported range, at System.Data.SqlClient.TdsParser.ConsumePreLoginHandshake
```

### <a name="resolution"></a>Çözüm

Bu sorunu tooupdate karma Bağlantı Yöneticisi toofix çalışıyoruz. Geçici çözümler için bkz: [SQL Server ile karma bağlantılar hatası: System.OverflowException: Aritmetik işlem taşması ile sonuçlandı](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/).

## <a name="how-do-i-add-or-edit-a-url-rewrite-rule"></a>Nasıl eklemek veya bir URL yeniden yazma kuralı düzenleme?

tooadd veya bir URL yeniden yazma kuralı düzenleyin:

1. Internet Information Services (IIS) Manager'ı tooyour App Service web uygulaması bağlayan şekilde ayarlayın. tooconnect IIS Yöneticisi'ni tooApp hizmeti nasıl görürüm toolearn [uzaktan yönetimi, IIS Yöneticisi'ni kullanarak Azure Web siteleri](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/).
2. IIS Yöneticisi ' nde ekleyin veya bir URL yeniden yazma kuralı düzenleyin. toolearn tooadd veya bir URL yeniden yazma düzenleme nasıl kuralı için bkz: [Oluştur yeniden yazma kuralları hello URL yeniden yazma Modülü](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module).

## <a name="how-do-i-control-inbound-traffic-tooapp-service"></a>Gelen trafik tooApp hizmeti nasıl denetlerim?

Merhaba site düzeyinde gelen trafiği tooApp Hizmeti denetlemek için iki seçeneğiniz vardır:

* Dinamik IP kısıtlamaları etkinleştirin. dinamik IP kısıtlamaları üzerinde tooturn nasıl görürüm toolearn [Azure Web siteleri için IP ve etki alanı kısıtlamaları](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/).
* Modül güvenliği kapatın. tooturn Modülü güvenlik nasıl görürüm toolearn [ModSecurity web uygulaması Güvenlik Duvarı'nı Azure Web siteleri](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/).

Uygulama hizmeti ortamı kullanırsanız, kullanabileceğiniz [Barracuda Güvenlik Duvarı'nı](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/).

## <a name="how-do-i-block-ports-in-an-app-service-web-app"></a>Bir App Service web uygulaması'nda bağlantı noktaları nasıl engelleyebilir?

Kiracı ortamı Hello paylaşılan uygulama hizmeti, olası tooblock belirli bağlantı noktalarını hello altyapı hello doğası nedeniyle olmadığı. 4016, 4018 ve 4020 TCP bağlantı noktaları da Visual Studio uzaktan hata ayıklama için açık olabilir.

Uygulama hizmeti ortamı'nda, gelen ve giden trafik üzerinde tam denetime sahiptir. Ağ güvenlik grupları toorestrict veya blok belirli bağlantı noktalarını kullanabilirsiniz. Uygulama hizmeti ortamı hakkında daha fazla bilgi için bkz: [Tanıtımı uygulama hizmeti ortamı](https://azure.microsoft.com/blog/introducing-app-service-environment/).

## <a name="how-do-i-capture-an-f12-trace"></a>Bir F12 izleme nasıl yakalamak?

F12 izleme yakalamak için iki seçeneğiniz vardır:

* F12 HTTP izleme
* F12 konsol çıkışı

### <a name="f12-http-trace"></a>F12 HTTP izleme

1. Internet Explorer'da tooyour Web sitesine gidin. Sonraki adımlar hello önce onu bir önemli toosign konusu. Aksi takdirde hello F12 izleme oturum açma hassas verileri yakalar.
2. F12 tuşuna basın.
3. Bu hello doğrulayın **ağ** sekmesi seçilmiştir ve ardından hello yeşil **Yürüt** düğmesi.
4. Merhaba sorunu yeniden oluşturma adımları hello.
5. Select hello kırmızı **durdurmak** düğmesi.
6. Select hello **kaydetmek** düğmesini (disk simgesi) ve (Internet Explorer ve kenar) hello HAR dosyasını kaydedin *veya* hello HAR dosyasını sağ tıklatın ve ardından **içerikle HAR Kaydet** ( Chrome ').

### <a name="f12-console-output"></a>F12 konsol çıkışı

1. Select hello **konsol** sekmesi.
2. Sıfırdan fazla öğelerini içeren her sekmenin hello sekmesini seçin (**hata**, **uyarı**, veya **bilgi**). Merhaba sekmesi seçili değilse, bunu çıktığınızda hello imleç taşıdığınızda hello sekmesini gri veya siyah simgedir.
3. Merhaba ileti alanında hello bölmesini sağ tıklatın ve ardından **tüm kopyalayın**.
4. Yapıştır hello metin bir dosyaya kopyalanır ve hello dosyasını kaydedin.

tooview HAR dosya, kullanabileceğiniz hello [HAR Görüntüleyicisi](http://www.softwareishard.com/har/viewer/).

## <a name="why-do-i-get-an-error-when-i-try-tooconnect-an-app-service-web-app-tooa-virtual-network-that-is-connected-tooexpressroute"></a>Bir uygulama hizmeti tooconnect çalıştığımda neden bir hata bağlı tooExpressRoute web uygulama tooa sanal ağ sağlarım?

Tooconnect tooAzure ExpressRoute bağlanan bir Azure web uygulaması tooa sanal ağ çalışırsanız, başarısız olur. Merhaba aşağıdaki ileti görüntülenir: "Ağ geçidi değil bir VPN ağ geçidi."

Şu anda bağlı tooExpressRoute noktadan siteye VPN bağlantıları tooa sanal ağ sahip olamaz. Bir noktadan siteye VPN ve ExpressRoute Merhaba aynı olamayacağı sanal ağ. Daha fazla bilgi için bkz: [ExpressRoute ve siteden siteye VPN bağlantıları sınırlar ve sınırlamalar](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations).

## <a name="how-do-i-connect-an-app-service-web-app-tooa-virtual-network-that-has-a-static-routing-policy-based-gateway"></a>Statik yönlendirme (ilke tabanlı) ağ geçidi olan bir App Service web uygulaması tooa sanal ağ nasıl bağlayabilirim?

Şu anda, statik yönlendirme (ilke tabanlı) ağ geçidi olan bir App Service web uygulama tooa sanal ağa bağlanması desteklenmiyor. Hedef sanal ağınız zaten varsa, noktadan siteye VPN bağlı tooan uygulama kullanılabilmesi için öncelikle, dinamik yönlendirme ağ geçidi ile etkin olması gerekir. Ağ geçidiniz toostatic yönlendirme ayarlanırsa, noktadan siteye VPN etkinleştiremezsiniz. 

Daha fazla bilgi için bkz: [bir Azure sanal ağı ile bir uygulamayı tümleştirin](web-sites-integrate-with-vnet.md#getting-started).

## <a name="in-my-app-service-environment-why-can-i-create-only-one-app-service-plan-even-though-i-have-two-workers-available"></a>İki çalışanları kullanılabilir olmasına rağmen my uygulama hizmeti ortamı'nda neden yalnızca bir uygulama hizmeti planı oluşturabilirim?

tooprovide hata toleransı, her bir çalışan havuzu en az bir ek hesaplama kaynak gerektiğini uygulama hizmeti ortamı gerektirir. bir iş yükü Hello ek hesaplama kaynak atanamaz.

Daha fazla bilgi için bkz: [nasıl toocreate bir uygulama hizmeti ortamı](app-service-web-how-to-create-an-app-service-environment.md).

## <a name="why-do-i-see-timeouts-when-i-try-toocreate-an-app-service-environment"></a>Bir uygulama hizmeti ortamı toocreate çalıştığımda neden zaman aşımları görüyor?

Bazı durumlarda, bir uygulama hizmeti ortamı oluşturma başarısız olur. Bu durumda, etkinlik günlükleri hello hata aşağıdaki hello bakın:
```
ResourceID: /subscriptions/{SubscriptionID}/resourceGroups/Default-Networking/providers/Microsoft.Web/hostingEnvironments/{ASEname}
Error:{"error":{"code":"ResourceDeploymentFailure","message":"hello resource provision operation did not complete within hello allowed timeout period.”}}
```

tooresolve Bu, aşağıdaki koşullar hello hiçbiri doğru olduğundan emin olun:
* Merhaba alt çok küçük.
* Merhaba alt ağı boş değil.
* ExpressRoute hello ağ bağlantı gereksinimleri bir uygulama hizmeti ortamı engeller.
* Bozuk bir ağ güvenlik grubu hello ağ bağlantı gereksinimleri bir uygulama hizmeti ortamı engeller.
* Zorlamalı tünel açıktır.

Daha fazla bilgi için bkz: [(oluşturma) dağıtırken sorunları sık yeni bir Azure uygulama hizmeti ortamı](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/).

## <a name="why-cant-i-delete-my-app-service-plan"></a>Neden my uygulama hizmeti planı silemezsiniz?

Uygulama hizmeti uygulamalardan hello uygulama hizmeti planı ile ilişkiliyse, bir uygulama hizmeti planı silemezsiniz. Bir uygulama hizmeti planı silmeden önce ilişkili tüm App Service uygulamalarının hello uygulama hizmeti planı ' kaldırın.

## <a name="how-do-i-schedule-a-webjob"></a>Bir Web işi nasıl zamanlama?

Zamanlanmış Web işi Cron ifadeler kullanarak oluşturabilirsiniz:

1. Bir settings.job dosyası oluşturun.
2. Bu JSON dosyasında Cron ifade kullanarak bir zamanlama özellik içerir: 
    ```
    { "schedule": "{second}
    {minute} {hour} {day}
    {month} {day of hello week}" }
    ```

Zamanlanmış Web işleri hakkında daha fazla bilgi için bkz: [Cron ifade kullanarak bir zamanlanmış WebJob oluşturma](web-sites-create-web-jobs.md#CreateScheduledCRON).

## <a name="how-do-i-perform-penetration-testing-for-my-app-service-app"></a>Uygulama hizmeti Uygulamam için test sızma nasıl yaparım?

tooperform sızma test, [bir istek göndermek](https://security-forms.azure.com/penetration-testing/terms).

## <a name="how-do-i-configure-a-custom-domain-name-for-an-app-service-web-app-that-uses-traffic-manager"></a>Trafik Yöneticisi kullanan bir App Service web uygulaması için bir özel etki alanı adını nasıl yapılandırırım?

toouse Yük Dengeleme için Azure Traffic Manager kullanan bir uygulama hizmeti uygulaması ile özel etki alanı adı nasıl görürüm toolearn [trafik Yöneticisi ile bir Azure web uygulaması için bir özel etki alanı adı yapılandırma](web-sites-traffic-manager-custom-domain-name.md).

## <a name="my-app-service-certificate-is-flagged-for-fraud-how-do-i-resolve-this"></a>My uygulama hizmet sertifikası sahtekarlık için işaretlenir. Bu nasıl giderebilirim?

Merhaba etki alanı doğrulama bir uygulama hizmeti sertifika satın alma sırasında iletiden hello görebilirsiniz:

"Sertifikanızı olası sahtekarlık için işaretlendi. Merhaba isteği şu anda incelenmektedir. Merhaba sertifika 24 saat içinde kullanılabilir olmaz, lütfen Azure desteğine başvurun."

Selamlama iletisine da anlaşılacağı gibi bu sahtekarlık doğrulama işlemi too24 saatleri toocomplete alabilir. Bu süre boyunca toosee selamlama iletisine devam edeceğiz.

Uygulama hizmeti sertifikanızı tooshow bu iletiyi 24 saat sonra devam ederse, lütfen PowerShell Betiği aşağıdaki hello çalıştırın. Merhaba betik kişiler hello [sertifika sağlayıcısı](https://www.godaddy.com/) doğrudan tooresolve hello sorun.

```
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subId>
$actionProperties = @{
    "Name"= "<Customer Email Address>"
    };
Invoke-AzureRmResourceAction -ResourceGroupName "<App Service Certificate Resource Group Name>" -ResourceType Microsoft.CertificateRegistration/certificateOrders -ResourceName "<App Service Certificate Resource Name>" -Action resendRequestEmails -Parameters $actionProperties -ApiVersion 2015-08-01 -Force   
```

## <a name="how-do-authentication-and-authorization-work-in-app-service"></a>Nasıl kimlik doğrulaması ve yetkilendirme App Service içinde çalışır?

Kimlik doğrulaması ve yetkilendirme App Service içinde ayrıntılı belgeler için bkz: [uygulama hizmeti güvenlik](../app-service/app-service-security-readme.md). Merhaba belgeleri de bilgiler var. uygulama hizmeti toouse ayarlama hakkında çeşitli sağlayıcı oturum açma işlemleri tanımlayın:
* [Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)
* [Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)
* [Google](../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md)
* [Microsoft Hesabı](../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md)
* [Twitter](../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="how-do-i-redirect-hello-default-azurewebsitesnet-domain-toomy-azure-web-apps-custom-domain"></a>Ne ı yönlendirmek hello varsayılan *. azurewebsites.net etki alanı toomy Azure web uygulamanızın özel etki alanı?

Azure, varsayılan Web Apps kullanarak yeni bir Web sitesi oluşturduğunuzda *sitename*. azurewebsites.net etki alanı tooyour sitesine atanır. Özel ana bilgisayar adı tooyour siteyi eklemek ve kullanıcıların toobe mümkün tooaccess varsayılan istemiyorsanız, *. azurewebsites.net etki hello varsayılan URL yönlendirebilirsiniz. toolearn tooredirect tüm trafik, Web sitenizin varsayılan etki alanı tooyour özel etki alanından bkz [yeniden yönlendirme hello varsayılan etki alanı tooyour özel etki alanı Azure web uygulamalarında](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/).

## <a name="how-do-i-determine-which-version-of-net-version-is-installed-in-app-service"></a>Hangi sürümünün nasıl belirleyebilirim .NET App Service'te sürümü yüklenir?

Merhaba hızlı şekilde toofind hello App Service içinde yüklü Microsoft .NET hello Kudu konsolunu kullanarak sürümüdür. Merhaba portalından veya uygulama hizmeti uygulamanızı hello URL'sini kullanarak hello Kudu Konsolu erişebilir. Ayrıntılı yönergeler için bkz: [belirleme hello yüklü .NET sürüm App Service'te](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/).

## <a name="why-isnt-autoscale-working-as-expected"></a>Neden otomatik ölçeklendirme beklendiği gibi çalışmıyor?

Azure otomatik ölçeklendirme ölçeklendirilmiş değiştirilmediğini veya, beklendiği gibi hello web uygulama örneğini ölçeği, size hangi isteyerek değil tooscale tooavoid çok "dalgalanma." son sonsuz bir döngüde seçeneğini belirledik bir senaryo içine çalışmıyor olabilir Bu, genellikle hello genişleme ve ölçek bileşenini eşiklerin arasında yeterli bir kenar boşluğu olmadığında gerçekleşir. tooavoid "dalgalanma" ve diğer otomatik ölçeklendirme en iyi uygulamalar hakkında tooread nasıl görürüm toolearn [otomatik ölçeklendirme en iyi yöntemler](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices).

## <a name="why-does-autoscale-sometimes-scale-only-partially"></a>Neden otomatik bazen yalnızca kısmen ölçeklendirme?

Otomatik ölçeklendirme ölçüm önceden yapılandırılmış sınırları aştığında tetiklenir. Bazı durumlarda, hello kapasite beklediğiniz karşılaştırılan toowhat yalnızca kısmen girilir fark edebilirsiniz. Merhaba istediğiniz örneklerinin sayısını olmadığında bu durum oluşabilir. Bu senaryoda, otomatik ölçeklendirme kısmen hello kullanılabilir örneklerinin sayısını bilgileriyle doldurur. Otomatik ölçeklendirme, daha sonra daha fazla kapasite hello yeniden dengeleyin mantığı tooget çalıştırır. Örnekleri kalan hello ayırır. Bu işlem birkaç dakika sürebileceğini unutmayın.

Birkaç dakika sonra örnek sayısı beklenen hello görmüyorsanız, hello kısmi Dolum yeterli toobring hello ölçümleri hello sınırları içinde olduğundan olabilir. Ya da hello alt ölçümleri sınırına ulaştığından otomatik ölçeklendirme ölçeklendirilmiş.

Bu koşulların hiçbiri geçerli ve başlangıç sorun devam ederse, destek isteği gönderin.

## <a name="how-do-i-turn-on-http-compression-for-my-content"></a>İçeriğim için nasıl HTTP sıkıştırmasını etkinleştirmek?

tooturn sıkıştırmasını hem statik ve dinamik içerik türleri için aşağıdaki kodu toohello uygulama düzeyinde web.config dosyasına hello ekleyin:

```
<system.webServer>
<urlCompression doStaticCompression="true" doDynamicCompression="true" />
< /system.webServer>
```

Toocompress istediğiniz statik MIME türleri ve hello belirli dinamik de belirtebilirsiniz. Bizim yanıt tooa Forumu sorusuna daha fazla bilgi için bkz: [httpCompression ayarları basit bir Azure Web sitesinde](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview).

## <a name="how-do-i-migrate-from-an-on-premises-environment-tooapp-service"></a>Bir şirket içi ortamına tooApp hizmeti nasıl geçişini?

Windows ve Linux web sunucuları tooApp hizmet sitelerinden toomigrate, Azure App Service geçiş Yardımcısı'nı kullanabilirsiniz. Merhaba geçiş aracı gerektiğinde Azure web uygulamaları ve veritabanları oluşturur ve hello içeriği yayımlar. Daha fazla bilgi için bkz: [Azure App Service geçiş Yardımcısı](https://www.movemetothecloud.net/).
