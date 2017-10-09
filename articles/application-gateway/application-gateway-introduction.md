---
title: "Uygulama ağ geçidi aaaIntroduction tooAzure | Microsoft Docs"
description: "Ağ geçidi boyutları dahil olmak üzere bu sayfayı hello uygulama ağ geçidi hizmeti katman 7 Yük Dengeleme için genel bir bakış sağlar, HTTP Yük Dengeleme, tanımlama bilgisi tabanlı oturum benzeşimi ve SSL boşaltma."
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: b37a2473-4f0e-496b-95e7-c0594e96f83e
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.custom: H1Hack27Feb2017
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: c40c9dba64ab03d9f6f81b3cb8f26c6562ac26c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-application-gateway"></a>Application Gateway'e genel bakış

Microsoft Azure Application Gateway, uygulama teslim denetleyicisini (ADC) hizmet olarak sunan özel bir sanal gereçtir. Uygulamanız için çeşitli 7. katman yük dengeleme özellikleri sunar. CPU yoğunluklu SSL sonlandırma toohello uygulama ağ geçidi boşaltarak müşteriler toooptimize web grubu verimlilik sağlar. Tek bir uygulama ağ geçidi arkasında birden çok Web sitesini hepsini bir kez dağıtımını gelen trafik, tanımlama bilgisi tabanlı oturum benzeşimi, URL yolu tabanlı Yönlendirme ve hello özelliği toohost dahil olmak üzere diğer katman 7 Yönlendirme yetenekleri de sağlar. Bir web uygulaması Güvenlik Duvarı (WAF) de hello uygulama ağ geçidi WAF SKU bir parçası olarak sağlanır. Bu ortak web Güvenlik Açıkları ve güvenlik açıklarına tooweb uygulamalardan koruma sağlar. Application Gateway; İnternet'e yönelik ağ geçidi, yalnızca dahili ağ geçidi veya bu ikisinin bir birleşimi olarak yapılandırılabilir. 

![senaryo](./media/application-gateway-introduction/scenario.png)

## <a name="features"></a>Özellikler

Uygulama ağ geçidi şu anda hello aşağıdaki özellikleri sağlar:


* **[Web uygulaması güvenlik duvarı](application-gateway-webapplicationfirewall-overview.md)**  -hello web uygulaması Güvenlik Duvarı (WAF) Azure uygulama ağ geçidi, SQL ekleme gibi ortak web tabanlı saldırıları, siteler arası komut dosyası saldırıları ve oturumu ele geçirilmesini web uygulamaları korur.
* **HTTP yük dengelemesi** - Application Gateway hepsini bir kez deneme yük dengelemesi sağlar. Yük dengelemesi 7. Katmanda yapılır ve yalnızca HTTP(S) trafiği için kullanılır.
* **Tanımlama bilgisi tabanlı oturum benzeşimi** -hello tanımlama bilgisi tabanlı oturum benzeşimi özelliğini, bir kullanıcı oturumunu hello üzerinde tookeep istediğinizde yararlıdır aynı arka uç. Ağ geçidi yönetilen tanımlama bilgilerini kullanarak hello uygulama ağ geçidi mümkün toodirect sonraki kullanıcı oturumu toohello trafiğinden olduğu aynı arka uç işleme için. Bu özellik, oturum durumu yerel olarak hello arka uç sunucuda bir kullanıcı oturumu için kaydedildiği durumlarda önemlidir.
* **[Güvenli Yuva Katmanı (SSL) yük boşaltma](application-gateway-ssl-arm.md)**  -bu özellik HTTPS trafiğini web sunucularınızın kapalı çözme hello maliyetli görevini alır. SSL bağlantısı hello uygulama ağ geçidi ve şifrelenmemiş hello istek toohello sunucusu iletme sonlandırma hello tarafından hello web sunucusu tarafından şifre çözme unburdened.  Uygulama ağ geçidi hello yanıt geri toohello istemci göndermeden önce yeniden şifreler. Bu özellik hello arka uç bulunduğu senaryolarda kullanışlıdır hello aynı sanal ağ uygulama ağ geçidi azure'da hello gibi güvenli.
* **[TooEnd SSL bitiş](application-gateway-backend-ssl.md)**  -uygulama ağ geçidi destekler bitiş tooend şifreleme trafiği. Uygulama ağ geçidi bunu hello uygulama ağ geçidi hello SSL bağlantısını sonlandırarak yapar. Hello ağ geçidi sonra toohello trafiği hello paket yeniden şifreler ve tanımlanan hello yönlendirme kurallarına göre hello paket toohello uygun arka uç iletir hello yönlendirme kuralları uygular. Merhaba web sunucusundan herhangi bir yanıt hello gider aynı işlemi geri toohello son kullanıcı.
* **[URL tabanlı içerik yönlendirme](application-gateway-url-route-overview.md)**  -bu özellik hello özelliği toouse farklı arka uç sunucular için farklı trafik sağlar. Trafik hello web sunucusunda bir klasöre veya bir CDN yönlendirilmiş tooa farklı arka uç olabilir. Bu özellik belirli içeriklere hizmet etmeyen arka uçlardaki gereksiz yükü azaltır.
* **[Çok siteli yönlendirme](application-gateway-multi-site-overview.md)**  -uygulama ağ geçidi, tooconsolidate tek bir uygulama ağ geçidi too20 sitelerinde yukarı sağlar.
* **[Websocket desteği](application-gateway-websocket.md)**  -başka bir önemli uygulama ağ geçidi Websocket için yerel destek hello özelliğidir.
* **[Sistem durumu izleme](application-gateway-probe-overview.md)**  -uygulama ağ geçidi varsayılan sistem durumu izleme arka uç kaynakların ve özel toomonitor daha belirli senaryolar için araştırmalarını sağlar.
* **[SSL ilke ve şifre](application-gateway-ssl-policy-overview.md)**  - toolimit hello SSL protokol sürümleri bu özellik hello sağlayabilir ve de hello şifrelemeleri desteklenir ve hello bunlar işlem sırası paketleri.
* **[Yeniden yönlendirme isteği](application-gateway-redirect-overview.md)**  -bu özellik, hello yetenek tooredirect HTTP isteklerini tooan HTTPS dinleyicisi sağlar.
* **[Çok kiracılı arka uç desteği](application-gateway-web-app-overview.md)**  - Application gateway, Azure Web Apps ve API Ağ Geçidi gibi çok kiracılı arka uç hizmetlerini arka uç havuz üyeleri olarak yapılandırmayı destekler. 
* **[Gelişmiş tanılama](application-gateway-diagnostics.md)** - Application gateway tam tanılama ve erişim günlükleri sağlar. Güvenlik duvarı günlükleri, WAF’nin etkin olduğu application gateway kaynakları için kullanılabilir.

## <a name="benefits"></a>Avantajlar

Application Gateway aşağıdakiler için yararlıdır:

* İstekleri gerektiren uygulamalar hello aynı kullanıcı/istemci oturumu tooreach hello aynı arka uç sanal makine. Bu uygulamaların örnekleri alışveriş sepeti uygulamaları ve web posta sunucularıdır.
* Web sunucusu grupları için SSL sonlandırma yükünü kaldırma.
* Bir içerik teslim ağı gibi uygulamalar aynı uzun süre çalışan TCP bağlantısı toobe yönlendirilmesini veya yük dengeli toodifferent arka uç sunucuları hello birden çok HTTP isteklerini gerektirir.
* Websocket trafiğini destekleyen uygulamalar
* Web uygulamalarını SQL ekleme, siteler arası komut dosyası saldırıları ve oturum ele geçirmeleri gibi yaygın web tabanlı saldırılardan koruma.
* Trafiğin url yolu veya etki alanı üst bilgileri gibi farklı yönlendirme ölçütlerine göre mantıksal dağıtımı.

Application Gateway tamamen Azure tarafından yönetilir, ölçeklenebilir ve yüksek oranda kullanılabilir. Daha iyi yönetilebilirlik için zengin tanılama ve günlüğe kaydetme özellikleri sağlar. Uygulama ağ geçidi oluşturduğunuzda, bir uç nokta (ortak VIP veya dahili ILB IP), giriş ağ trafiği için ilişkilendirilir ve kullanılır. Bu VIP veya ILB'nin IP Azure yük dengeleyici tarafından hello aktarım düzeyinde (TCP/UDP) çalışma ve yük dengeli toohello uygulama ağ geçidi çalışan örnekleri olan tüm gelen ağ trafiğini olması sağlanır. yolların kendi yapılandırmasına bağlı olarak bir sanal makine olup olmadığını HTTP/HTTPS trafiğini hello sonra uygulama ağ geçidi Hello bulut hizmeti, iç veya dış IP adresi.

Uygulama ağ geçidi bir Azure tarafından yönetilen hizmet hello bir katman 7 yük dengeleyicinin arkasına hello Azure yazılım yük dengeleyici sağlanmasına olanak tanır şekilde yük dengeleme. Trafik Yöneticisi kullanılan toocomplete hello senaryo görüntü, uygulama ağ geçidi sağlarken burada trafik Yöneticisi yeniden yönlendirme ve trafik kullanılabilirliğini toomultiple uygulama ağ geçidi kaynakları farklı bölgelerdeki sağlar aşağıdaki hello görülen olabilir Çapraz bölge katman 7 Yük Dengeleme. Bu senaryo örneği bulunabilir: [kullanarak Yük Dengeleme hello Azure bulut Hizmetleri](../traffic-manager/traffic-manager-load-balancing-azure.md)

![traffic manager ve application gateway senaryosu](./media/application-gateway-introduction/tm-lb-ag-scenario.png)

[!INCLUDE [load-balancer-compare-tm-ag-lb-include.md](../../includes/load-balancer-compare-tm-ag-lb-include.md)]

## <a name="gateway-sizes-and-instances"></a>Ağ geçidi boyutları ve örnekleri

Application Gateway şu anda üç büyüklükte sunulmaktadır: **Kısa**, **Orta** ve **Uzun**. Küçük örnek boyutları, geliştirme ve test senaryolarına yöneliktir.

Abonelik başına too50 uygulama ağ geçitleri oluşturan oluşturabilirsiniz ve her uygulama ağ geçidi too10 örneği her olabilir. Her uygulama ağ geçidi 20 http dinleyicisinden oluşabilir. Application Gateway limitlerinin tam listesi için bkz. [Application Gateway hizmet limitleri](../azure-subscription-service-limits.md?toc=%2fazure%2fapplication-gateway%2ftoc.json#application-gateway-limits).

Aşağıdaki tablonun hello her uygulama ağ geçidi örneği için bir ortalama performans işleme SSL boşaltması etkin gösterir:

| Arka uç sayfa yanıtı | Küçük | Orta | Büyük |
| --- | --- | --- | --- |
| 6K |7,5 Mbps |13 Mbps |50 Mbps |
| 100K |35 Mbps |100 Mbps |200 Mbps |

> [!NOTE]
> Bu değerler bir uygulama ağ geçidi verimliliği için yaklaşık değerlerdir. Merhaba gerçek verimlilik ortalama sayfa boyutu gibi çeşitli ortamı ayrıntılarını arka uç örnekleri ve işleme süresi tooserve bir sayfa konumunu bağlıdır. Tam performans rakamlarına ulaşmak için kendi testlerinizi çalıştırmanız gerekir. Bu değerler yalnızca kapasite planlama konusunda yardımcı olmak için verilmiştir.

## <a name="health-monitoring"></a>Sistem durumunu izleme

Azure uygulama ağ geçidi, temel veya özel sistem durumu araştırmalarının otomatik olarak hello arka uç örnekleri hello durumunu izler. Sistem durumu araştırmalarının kullanarak, yalnızca sağlıklı ana tootraffic yanıt vermesini sağlar. Daha fazla bilgi için bkz. [Application Gateway sistem durumunu izlemeye genel bakış](application-gateway-probe-overview.md).

## <a name="configuring-and-managing"></a>Yapılandırma ve yönetme

Uygulama ağ geçidi, uç noktası için bir genel IP, özel IP veya yapılandırıldığında her ikisine birden sahip olabilir. Application Gateway, kendi alt ağındaki bir sanal ağ içinde yapılandırılır. oluşturulan veya uygulama ağ geçidi için kullanılan hello alt herhangi bir kaynak türleri içeremez, hello alt ağda izin verilen hello yalnızca başka uygulama ağ geçitleri kaynaklardır. Merhaba arka uç sunucularının, arka uç kaynaklarına yer almalıdır hello farklı bir alt ağ içinde toosecure hello uygulama ağ geçidi aynı sanal ağ. Bu alt ağ hello arka uç uygulamalar için gerekli değildir. Başlangıç IP adresi Hello uygulama ağ geçidi ulaşabilir sürece, uygulama ağ geçidi mümkün tooprovide ADC yetenekleri hello arka uç sunucuları için ' dir. 

REST API’leri, PowerShell cmdlet’leri, Azure CLI veya [Azure portalını](https://portal.azure.com/) kullanarak bir uygulama ağ geçidi oluşturup yönetebilirsiniz. Uygulama ağ geçidi hakkında ek sorular şu adresi ziyaret edin [uygulama ağ geçidi SSS](application-gateway-faq.md) sık sorulan sorular tooview ortak listesi.

## <a name="pricing"></a>Fiyatlandırma

Fiyatlandırma, saatlik ağ geçidi örneği ücretine ve veri işleme ücretine bağlıdır. Saat başına WAF SKU hello için ağ geçidi fiyatlandırma standart SKU ücretlerden farklıdır. Bu fiyatlandırma bilgileri [Application Gateway fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/application-gateway/) sayfasında bulunabilir. Veri işleme ücretleri kalır hello aynı.

## <a name="faq"></a>SSS

Application Gateway hakkında sık sorulan sorular için bkz. [Application Gateway hakkında SSS](application-gateway-faq.md).

## <a name="next-steps"></a>Sonraki adımlar

Uygulama ağ geçidi hakkında daha fazla bilgi sonra şunları yapabilirsiniz [bir uygulama ağ geçidi oluşturma](application-gateway-create-gateway-portal.md) veya [SSL boşaltma bir uygulama ağ geçidi oluşturma](application-gateway-ssl-arm.md) tooload Bakiye HTTPS bağlantıları.

toolearn nasıl toocreate URL tabanlı içerik yönlendirme, kullanarak bir uygulama ağ geçidi Git çok[URL tabanlı yönlendirme kullanarak bir uygulama ağ geçidi oluşturma](application-gateway-create-url-route-arm-ps.md) daha fazla bilgi için.

Bazı toolearn Azure özelliklerini ağ başka bir anahtar Merhaba, bkz: [Azure ağ](../networking/networking-overview.md).
