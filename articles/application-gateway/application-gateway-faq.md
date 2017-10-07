---
title: "Azure uygulama ağ geçidi sorular aaaFrequently | Microsoft Docs"
description: "Bu sayfayı yanıtlar sağlayan Azure uygulama ağ geçidi hakkında sorular toofrequently"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a>Uygulama ağ geçidi için sık sorulan sorular

## <a name="general"></a>Genel

**Q. Uygulama ağ geçidi nedir?**

Azure uygulama ağ geçidi uygulama teslim denetleyici (ADC) bir hizmet olarak çeşitli katman 7 Yük Dengeleme, uygulamalarınız için sunumu ' dir. Azure tarafından tam olarak yönetilen, yüksek oranda kullanılabilir ve ölçeklenebilir hizmet sunar.

**Q. Hangi özelliklerin uygulama ağ geçidi destekliyor mu?**

Uygulama ağ geçidi SSL boşaltma ve bitiş tooend SSL, Web uygulaması güvenlik duvarı, tanımlama bilgisi tabanlı oturum benzeşimi, url yolu tabanlı yönlendirme, çoklu siteyi barındıran ve diğerleri destekler. Desteklenen özelliklerin tam listesi için ziyaret [giriş tooApplication ağ geçidi](application-gateway-introduction.md)

**Q. Uygulama ağ geçidi ve Azure yük dengeleyici arasındaki hello fark nedir?**

Uygulama ağ geçidi web trafiği ile yalnızca (HTTP/HTTPS/WebSocket) çalıştığı anlamına gelir bir katman 7 yük dengeleyicidir. Bu, Yük Dengeleme trafiğini SSL sonlandırma, tanımlama bilgisi tabanlı oturum benzeşimi ve hepsini bir kez gibi özellikleri destekler. Yük Dengeleyici, 4 (TCP/UDP) katmanında bakiyelerini trafiğin yük.

**Q. Hangi protokollerin, uygulama ağ geçidi destekliyor mu?**

Uygulama ağ geçidi, HTTP, HTTPS ve WebSocket destekler.

**Q. Hangi kaynaklara arka uç havuzu bir parçası olarak bugün destekleniyor mu?**

Arka uç havuzları olan NIC'ler, sanal makine ölçek kümeleri, genel IP'ler birleştirilebilen, iç IP, tam etki alanı adları (FQDN) ve çok kiracılı arka Azure Web Apps gibi uçları. Uygulama ağ geçidi arka uç havuzu üye olmayan tooan kullanılabilirlik kümesine bağlıdır. IP bağlantısını sahip oldukları sürece arka uç havuzları üyeleri kümeler, veri merkezleri arasında veya Azure dışında olabilir.

**Q. Hangi bölgeleri hizmettir hello kullanılabilir?**

Uygulama ağ geçidi genel Azure tüm bölgelerde kullanılabilir. Ayrıca, kullanılabilir [Azure Çin](https://www.azure.cn/) ve [Azure kamu](https://azure.microsoft.com/en-us/overview/clouds/government/)

**Q. Bu Aboneliğimi için adanmış bir dağıtımı veya müşterileri arasında paylaşılan?**

Uygulama ağ geçidi, sanal ağınızda adanmış bir dağıtımıdır.

**Q. İş HTTP -> desteklenen HTTPS yeniden yönlendirmesi?**

Yeniden yönlendirme desteklenir. Ziyaret [uygulama ağ geçidi yeniden yönlendirmeye genel bakış](application-gateway-redirect-overview.md) toolearn daha fazla.

**Q. Hangi sırayla dinleyicileri işlenir?**

Dinleyicileri bunlar gösterilir hello sırada işlenir. Gelen bir istek temel dinleyici eşleşiyorsa, bu nedenle ilk işler.  Çok siteli dinleyicileri yönlendirilmiş toohello doğru arka uç temel dinleyici tooensure trafiğidir önce yapılandırılması gerekir.

**Q. Uygulama ağ geçidi IP ve DNS nerede bulabilirim?**

Bir ortak IP adresi bir uç nokta kullanılırken, bu bilgileri hello ortak IP adresi kaynağı veya hello genel bakış sayfasında hello portal hello uygulama ağ geçidi için bulunabilir. İç IP adresleri için bu hello genel bakış sayfasında bulunabilir.

**Q. Merhaba IP veya DNS hello uygulama ağ geçidi hello ömrü boyunca değişiyor mu?**

Merhaba ağ geçidi durduruldu ve hello müşteri tarafından başlatılan hello VIP değiştirebilirsiniz. Uygulama ağ geçidi ile ilişkili DNS Hello hello yaşam döngüsü hello ağ geçidi değiştirmez. Bu nedenle, olmasından hello uygulama ağ geçidi toohello DNS adresi gelin ve CNAME diğer adını toouse önerilir.

**Q. Uygulama ağ geçidi, statik IP destekliyor mu?**

Hayır, uygulama ağ geçidi ortak statik IP adresleri desteklemez, ancak statik iç IP desteklemiyor.

**Q. Uygulama ağ geçidi birden çok ortak IP hello ağ geçidinde destekliyor mu?**

Yalnızca bir genel IP adresi, bir uygulama ağ geçidi üzerinde desteklenir.

**Q. Uygulama ağ geçidi x-iletilen-için üstbilgiler destekliyor mu?**

Evet, uygulama ağ geçidi, x-iletilen-için x iletilen proto ekler ve toohello arka uç x iletilen bağlantı üstbilgileri hello isteği halinde iletilir. Merhaba x-iletilen-için üstbilgisi IP: BağlantıNoktası, virgülle ayrılmış listesini biçimidir. Merhaba geçerli x iletilen proto http veya https değerler. X-iletilen-bağlantı noktası başlangıç bağlantı noktası uygulama ağ geçidi hello üst sınırına hangi hello isteğinde belirtir.

**Q. Bir uygulama ağ geçidi toodeploy ne kadar sürer? My uygulama ağ geçidi, güncelleştirilen zaman hala çalışıyor mu?**

Yeni uygulama ağ geçidi dağıtımları too20 dakika tooprovision alabilir. Değişiklikleri tooinstance boyutu/sayısı kesintiye uğratan değildir ve hello ağ geçidi bu süre boyunca etkin kalır.

## <a name="configuration"></a>Yapılandırma

**Q. Uygulama ağ geçidi, sanal bir ağa her zaman dağıtılır?**

Evet, uygulama ağ geçidi her zaman bir sanal ağ alt ağında dağıtılır. Bu alt ağ yalnızca uygulama ağ geçitleri içerebilir.

**Q. Uygulama ağ geçidi tooinstances kendi sanal ağ dışından iletişim kurabilirsiniz?**

Uygulama ağ geçidi IP bağlantısı var olduğu sürece, olarak hello sanal ağ dışında tooinstances iletişim kurabilirsiniz. Toouse düşünüyorsanız, arka uç havuzu üyeleri, ardından dahili Ips'ler gerektirir [VNET eşlemesi](../virtual-network/virtual-network-peering-overview.md) veya [VPN ağ geçidi](../vpn-gateway/vpn-gateway-about-vpngateways.md).

**Q. Merhaba uygulama ağ geçidi alt ağdaki başka bir şey dağıtabilir miyim?**

Hayır, ancak diğer uygulama ağ geçitleri hello alt dağıtabilirsiniz.

**Q. Ağ güvenlik grupları hello uygulama ağ geçidi alt ağda destekleniyor mu?**

Ağ güvenlik grupları hello uygulama ağ geçidi alt ağda ile kısıtlamaları aşağıdaki hello desteklenir:

* Özel durumlar gelen trafiği için bağlantı noktalarını 65503 65534 arka uç sistem durumu toowork için doğru koyun gerekir.

* Giden internet bağlantısı engellenebilir değil.

* Merhaba AzureLoadBalancer etiketi gelen trafiği için izin verilmelidir.

**Q. Uygulama ağ geçidi hello sınırları nelerdir? Bu sınırları artırmak?**

Ziyaret [uygulama ağ geçidi sınırları](../azure-subscription-service-limits.md#application-gateway-limits) tooview hello sınırlar.

**Q. Uygulama ağ geçidi iç ve dış trafiği için aynı anda kullanabilir miyim?**

Evet, uygulama ağ geçidini bir iç IP ve bir dış IP başına uygulama ağ geçidi destekler.

**Q. VNet eşlemesi destekleniyor mu?**

Evet, VNet eşlemesi desteklenir ve Yük Dengeleme trafiğini diğer sanal ağlarda için yararlıdır.

**Q. Tooon içi sunucular, ExpressRoute ya da VPN tünelleri tarafından bağlıyken iletişim kurabilirsiniz?**

Evet, trafiğe izin sürece.

**Q. Birçok uygulama farklı bağlantı noktaları üzerinde hizmet veren bir arka uç havuzu olabilir mi?**

Mikro hizmet mimarisi desteklenir. Farklı bağlantı noktaları üzerinde birden çok http yapılandırılan ayarları tooprobe gerekir.

**Q. Özel araştırmalara joker karakter/regex yanıt verileri destekler mi?**

Özel araştırmalara joker karakter veya regex yanıt verileri desteklemez. 

**Q. Kuralları nasıl işlenir?**

Yapılandırılmış olan hello sırada işlenir. Merhaba temel kural değerlendirilen bağlantı noktası önceki toohello çok siteli kurala göre trafiği eşleşecek şekilde trafiği temel kurallar tooreduce hello fırsat toohello uygunsuz arka uç yönlendirilen önce çok siteli kuralları yapılandırılır önerilir.

**Q. Kuralları nasıl işlenir?**

Oluşturuldukları hello sırada işlenir. Çok siteli kuralları önce temel kurallar yapılandırılır önerilir. Çok siteli dinleyicileri ilk yapılandırarak, bu yapılandırma yönlendirilmiş toohello uygunsuz arka uç trafiğidir hello olasılığını azaltır. Merhaba temel kural değerlendirilen bağlantı noktası önceki toohello çok siteli kurala göre trafiği eşleşecek şekilde yönlendirme Bu sorun ortaya çıkabilir.

**Q. Hangi özel araştırmalara hello ana bilgisayar alanı belirtmek?**

Ana bilgisayar alanı hello adı toosend hello araştırma için belirtir. Geçerli yalnızca çok siteli uygulama ağ geçidi üzerinde yapılandırılmış, aksi takdirde '127.0.0.1' kullanın. Bu değer VM ana bilgisayar adından farklı olduğundan ve biçimde \<Protokolü\>://\<konak\>:\<bağlantı noktası\>\<yolu\>.

**Q. Beyaz liste uygulama ağ geçidi erişim tooa yükleyebilir miyim az IP'leri kaynak?**

Bu senaryo yapılabilir uygulama ağ geçidi alt ağda Nsg'leri kullanarak. Merhaba kısıtlamaları aşağıdaki listelenen hello öncelik sırasına göre hello alt ağdaki sokulmalıdır:

* IP/IP aralığı kaynağından gelen trafiğe izin verecek.

* Tüm kaynakları tooports 65503 65534 için gelen gelen istekleri izin [arka uç sağlık iletişimi](application-gateway-diagnostics.md).

* Gelen Azure yük dengeleyici araştırmalar (AzureLoadBalancer etiketi) ve gelen sanal ağ trafiğini (VirtualNetwork etiketi) üzerinde hello izin [NSG](../virtual-network/virtual-networks-nsg.md).

* Bir reddetme ile diğer tüm gelen trafiği engelle tüm kuralı.

* Giden trafik toohello izin Internet tüm hedefler için.

## <a name="performance"></a>Performans

**Q. Uygulama ağ geçidi, yüksek kullanılabilirlik ve ölçeklenebilirlik nasıl destekler?**

Uygulama ağ geçidi dağıtılan iki veya daha çok örneği varsa, yüksek kullanılabilirlik senaryolarını destekler. Azure tüm örneklerini hello dönme güncelleştirme ve hata etki alanları tooensure üzerinden bu örnekler dağıtır aynı anda. Uygulama ağ geçidi, birden çok örneğini hello ekleyerek ölçeklenebilirlik destekler aynı ağ geçidi tooshare hello yük.

**Q. Nasıl ı DR senaryosuna uygulama ağ geçidi ile veri merkezleri arasında elde etmek?**

Müşteriler, farklı veri merkezlerinde bulunan birden çok uygulama ağ geçidi üzerinden trafik Yöneticisi toodistribute trafiği kullanabilirsiniz.

**Q. Otomatik ölçeklendirme destekleniyor mu?**

Hayır, ancak uygulama ağ geçidi kullanılan tooalert olabilir bir işleme ölçümü, bir Eşiğe ulaşıldığında. El ile örnekleri ekleme veya boyutunu değiştirme hello ağ geçidini yeniden değil ve varolan trafiği etkilemez.

**Q. El ile ölçek yukarı/aşağı neden kapalı kalma süresi mu?**

Kapalı kalma süresi olmadan, örnekler yükseltme etki alanları ve hata etki alanları arasında dağıtılır.

**Q. Orta toolarge kesintiye uğratmadan gelen örnek boyutu değiştirebilirim?**

Evet, Azure örnekleri tüm örneklerini hello dönme güncelleştirme ve hata etki alanları tooensure dağıtır aynı anda. Birden çok örneğini ekleyerek ölçeklendirme uygulama ağ geçidi destekler, aynı ağ geçidi tooshare hello yük hello.

## <a name="ssl-configuration"></a>SSL yapılandırması

**Q. Hangi sertifikaların uygulama ağ geçidinde destekleniyor mu?**

Otomatik olarak imzalanan sertifikaları, CA sertifikaları ve joker sertifikaları desteklenir. EV sertifikaları desteklenmez.

**Q. Uygulama ağ geçidi tarafından desteklenen hello geçerli şifre paketleri nelerdir?**

Merhaba, uygulama ağ geçidi tarafından desteklenen hello geçerli şifre paketleri şunlardır. Ziyaret edin: [yapılandırma SSL İlkesi sürümleri ve şifre paketleri uygulama ağ geçidi üzerinde](application-gateway-configure-ssl-policy-powershell.md) toolearn nasıl toocustomize SSL seçenekleri.

- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

**Q. Uygulama ağ geçidi de trafiği toohello arka uç yeniden şifrelenmesini destekliyor mu?**

Evet, uygulama ağ geçidi destekler SSL boşaltma ve son tooend hello trafiği toohello arka uç yeniden şifreler SSL.

**Q. SSL ilke toocontrol SSL protokol sürümleri yapılandırabilir miyim?**

Evet, uygulama ağ geçidi toodeny yapılandırabilirsiniz TLS1.0, TLS1.1 ve TLS1.2. SSL 2.0 ve 3.0 zaten varsayılan olarak devre dışıdır ve yapılandırılabilir değildir.

**Q. Şifre paketleri ve ilke sırasını yapılandırabilir miyim?**

Evet, [şifre paketleri yapılandırmasını](application-gateway-ssl-policy-overview.md) desteklenir. Özel bir ilke tanımlandığında, şifre paketleri aşağıdaki hello en az birinin etkinleştirilmesi gerekir. Uygulama ağ geçidi SHA256 toofor arka uç yönetim kullanır.

* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
* TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_256_CBC_SHA256
* TLS_RSA_WITH_AES_128_CBC_SHA256

**Q. Kaç tane SSL sertifikalarını destekleniyor mu?**

Too20 SSL sertifikaları desteklenir.

**Q. Arka uç yeniden şifreleme için kaç tane kimlik doğrulama sertifikaları destekleniyor mu?**

Too10 5 bir varsayılan kimlik doğrulama sertifikaları desteklenir.

**Q. Uygulama ağ geçidi, Azure anahtar kasası ile yerel olarak tümleşik çalışıyor mu?**

Hayır, bunu Azure anahtar kasası ile tümleşiktir değil.

## <a name="web-application-firewall-waf-configuration"></a>Web uygulaması Güvenlik Duvarı (WAF) yapılandırması

**Q. Merhaba WAF SKU standart SKU hello ile kullanılabilen tüm hello özellikleri sunar?**

Evet, WAF hello standart SKU tüm hello özelliklerini destekler.

**Q. Uygulama ağ geçidi destekleyen hello CRS sürümü nedir?**

Uygulama ağ geçidi destekleyen CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) ve CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).

**Q. WAF nasıl izlerim?**

WAF tanılama günlük aracılığıyla izlenen, tanılama günlüğe kaydetme hakkında daha fazla bilgi bulunabilir [tanılama günlüğe kaydetme ve uygulama ağ geçidi ölçümleri](application-gateway-diagnostics.md)

**Q. Algılama modunu akışa mu?**

Hayır, algılama modunu yalnızca WAF kuralını tetikleyen trafiği günlüğe kaydeder.

**Q. WAF kuralları nasıl özelleştirebilirim?**

Evet, WAF kuralları nasıl toocustomize ziyaret hakkında daha fazla bilgi için özelleştirilebilir [özelleştirme WAF kural gruplar ve kurallar](application-gateway-customize-waf-rules-portal.md)

**Q. Hangi kuralları şu anda kullanılabilir?**

WAF şu anda CRS destekler [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) ve [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), ilk 10 güvenlik açıkları hello açık Web uygulaması güvenlik proje (burada bulunan OWASP) tarafından tanımlanan hello çoğunu karşı temel güvenlik sağlayın [OWASP ilk 10 güvenlik açıkları](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)

* SQL ekleme koruması

* Siteler arası komut dosyası koruması

* Komut ekleme, HTTP isteği kaçakçılığı, HTTP yanıtı bölme ve uzak dosya ekleme saldırıcı gibi Yaygın Web Saldırıları Koruması

* HTTP protokolü ihlallerine karşı koruma

* Eksik konak kullanıcısı-aracısı ve kabul üst bilgileri gibi HTTP protokolü anormalliklerine karşı koruma

* Robotlar, gezginler ve tarayıcıları önleme

* Ortak uygulama yapılandırma hataları (diğer bir deyişle, Apache, IIS, vb.) algılanması

**Q. WAF de DDoS önleme destekliyor mu?**

Hayır, WAF DDoS önleme sağlamaz.

## <a name="diagnostics-and-logging"></a>Tanılama ve günlüğe kaydetme

**Q. Ne tür günlükleri ile uygulama ağ geçidi var mı?**

Uygulama ağ geçidi için üç günlükleri vardır. Bu günlükler ve diğer tanılama yetenekleri hakkında daha fazla bilgi için ziyaret [arka uç sistem durumu, tanılama günlüklerini ve uygulama ağ geçidi ölçümleri](application-gateway-diagnostics.md).

- **ApplicationGatewayAccessLog** -hello erişim günlüğü içerir gönderilen her isteği toohello uygulama ağ geçidi ön uç. Dönüş kodu, bayt ve kapatma, hello arayanın IP, istenen URL yanıt gecikme Hello veri içerir. Erişim günlüğüne 300 saniyede toplanır. Bu günlük, uygulama ağ geçidi örneği başına bir kayıt içerir.
- **ApplicationGatewayPerformanceLog** -hello performans günlüğü sunulan, toplam istek dahil olmak üzere her örneği bazında üretilen iş bayt performans bilgilerini yakalar, toplam istek sayısı sunulan, sağlıklı ve sağlıksız başarısız istek sayısı arka uç örnek sayısı.
- **ApplicationGatewayFirewallLog** -hello güvenlik duvarı günlüğü, web uygulaması güvenlik duvarı ile yapılandırılmış bir uygulama Ağ Geçidi algılama veya önleme modu üzerinden oturum isteklerini içerir.

**Q. My arka uç havuzu üyeleri sağlıklı olup olmadığını nasıl anlayabilirim?**

Merhaba PowerShell cmdlet'ini kullanabilirsiniz `Get-AzureRmApplicationGatewayBackendHealth` veya sistem durumu hello Portalı aracılığıyla ziyaret ederek doğrulamak [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md)

**Q. Merhaba bekletme ilkesi hello tanılama günlükleri'nedir?**

Akış toohello müşteri depolama hesabına tanılama günlükleri ve müşterilerin kendi tercihine göre hello bekletme ilkesi ayarlayabilirsiniz. Tanılama günlüklerini de tooan olay hub'ı veya günlük analizi gönderilebilir. Ziyaret [uygulama ağ geçidi tanılama](application-gateway-diagnostics.md) daha fazla ayrıntı için.

**Q. Uygulama ağ geçidi için denetim günlüklerini nasıl sağlarım?**

Denetim günlükleri, uygulama ağ geçidi için kullanılabilir. Merhaba Portalı'nda tıklatın **etkinlik günlüğü** hello menü dikey bir uygulama ağ geçidi tooaccess hello denetim günlüğü. 

**Q. Uygulama ağ geçidi uyarılarla ayarlayabilir miyim?**

Evet, uygulama ağ geçidi uyarıları destek, uyarılar ölçümleri yapılandırılır.  Uygulama ağ geçidi şu anda yapılandırılmış tooalert olabilir "işleme" ölçüsü yok. Uyarıları hakkında daha fazla toolearn ziyaret [uyarı bildirimleri alma](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

**Q. Arka uç sistem durumu bilinmeyen durum, bu durum neden olabilecek verir?**

Merhaba en yaygın nedeni, bir NSG veya özel DNS tarafından erişim toohello arka uç engelleniyor olmasıdır. Ziyaret [arka uç sistem durumu, tanılama günlüğe kaydetme ve uygulama ağ geçidi ölçümleri](application-gateway-diagnostics.md) toolearn daha fazla.

## <a name="next-steps"></a>Sonraki Adımlar

Uygulama ağ geçidi hakkında daha fazla ziyaret toolearn [giriş tooApplication ağ geçidi](application-gateway-introduction.md).
