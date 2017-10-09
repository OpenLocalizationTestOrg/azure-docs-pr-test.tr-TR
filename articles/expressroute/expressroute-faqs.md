---
title: aaaAzure ExpressRoute SSS | Microsoft Docs
description: "Merhaba ExpressRoute SSS desteklenen Azure hizmetlerini, maliyet, veri ve bağlantıları, SLA, sağlayıcıları ve konumları, bant genişliği ve ek teknik ayrıntılar hakkında bilgi içerir."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 09b17bc4-d0b3-4ab0-8c14-eed730e1446e
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: c01e83f1497103e2fa85251dce6fb41844e46e9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-faq"></a>ExpressRoute SSS

## <a name="what-is-expressroute"></a>ExpressRoute nedir?

ExpressRoute, Microsoft veri merkezleri ile şirketinizde veya bir birlikte bulundurma yerde bulunan altyapı arasında özel bağlantılar oluşturmanızı sağlayan bir Azure hizmetidir. ExpressRoute bağlantıları hello ortak Internet ve teklif daha yüksek güvenlik, güvenilirlik geçmemektedir ve hızıyla hello Internet genel bağlantılara gecikmeleri düşürün.

### <a name="what-are-hello-benefits-of-using-expressroute-and-private-network-connections"></a>Merhaba ExpressRoute ve özel ağ bağlantıları kullanmanın avantajları nelerdir?

ExpressRoute bağlantıları hello Git değil genel Internet. Bunlar, daha yüksek güvenlik, güvenilirlik ve hello Internet üzerinden genel bağlantılara daha tutarlı ve daha düşük gecikme süreleriyle hızları sunar. Bazı durumlarda, ExpressRoute bağlantıları tootransfer verileri arasında kullanarak şirket içi cihazları ve Azure önemli maliyet avantajları sağlar.

### <a name="where-is-hello-service-available"></a>Burada hello hizmeti var mı?

Hizmet konumu ve kullanılabilirliği için bu sayfaya bakın: [ExpressRoute ortakları ve konumları](expressroute-locations.md).

### <a name="how-can-i-use-expressroute-tooconnect-toomicrosoft-if-i-dont-have-partnerships-with-one-of-hello-expressroute-carrier-partners"></a>I ortaklıkları hello taşıyıcı ExpressRoute ortakları ile yoksa, ExpressRoute tooconnect tooMicrosoft nasıl kullanabilirim?

Bölgesel bir operatör seçin ve sağlayıcı konumları Ethernet bağlantıları tooone desteklenen hello Exchange güden. Merhaba sağlayıcısı konumda Microsoft ile eş. Merhaba son Kısım denetleyin [ExpressRoute ortakları ve konumları](expressroute-locations.md) hizmet sağlayıcınıza hello exchange konumlardan herhangi birinde varsa, toosee. Ardından, bir expressroute bağlantı hattı üzerinden hello hizmet sağlayıcısı tooconnect tooAzure sıralayabilirsiniz.

### <a name="how-much-does-expressroute-cost"></a>ExpressRoute maliyet mu ne kadar?

Denetleme [fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/expressroute/) fiyatlandırma bilgileri için.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-does-hello-vpn-connection-i-purchase-from-my-network-service-provider-have-toobe-hello-same-speed"></a>Bir expressroute bağlantı hattı, belirli bir bant genişliği hello için VPN bağlantısı my ağ servis sağlayıcısı'ndan satın ı ödeme sahip toobe hello aynı hızı?

Hayır. Bir VPN bağlantısı herhangi hızı hizmet sağlayıcınızdan satın alabilirsiniz. Ancak, bağlantı tooAzure satın aldığınız sınırlı toohello ExpressRoute devresi bant genişliği ' dir.

### <a name="if-i-pay-for-an-expressroute-circuit-of-a-given-bandwidth-do-i-have-hello-ability-tooburst-up-toohigher-speeds-if-necessary"></a>Merhaba özelliği tooburst toohigher hızları gerekirse yukarı, belirli bir bant genişliği bir expressroute bağlantı hattı için ödeme yapıyorsanız var mı?

Evet. ExpressRoute bağlantı hatları, tooburst tootwo kez yedeklemek için ek ücret ödemeden temin bant genişliği sınırı hello yapılandırılmış tooallow ' dir. Bu özelliği destekleyen, servis sağlayıcı toosee ile kontrol edin.

### <a name="can-i-use-hello-same-private-network-connection-with-virtual-network-and-other-azure-services-simultaneously"></a>Merhaba kullanabilirim özel aynı ağ bağlantısı ile sanal ağ ve diğer Azure hizmetleriyle aynı anda?

Evet. Bir kez kurma, bir expressroute bağlantı hattı, bir sanal ağ içindeki tooaccess Hizmetleri ve diğer Azure hizmetleriyle aynı anda sağlar. Toovirtual ağlar hello özel eşleme yoluna ve tooother Hizmetleri üzerinden hello ortak eşleme yolu bağlanırsınız.

### <a name="does-expressroute-offer-a-service-level-agreement-sla"></a>ExpressRoute hizmet düzeyi sözleşmesi (SLA) sunar?

Bilgi için bkz: Merhaba [ExpressRoute SLA](https://azure.microsoft.com/support/legal/sla/) sayfası.

## <a name="supported-services"></a>Desteklenen hizmetler

ExpressRoute destekler [üç yönlendirme etki alanları](expressroute-circuit-peerings.md) çeşitli türlerdeki Hizmetleri için.

### <a name="private-peering"></a>Özel eşleme

* Tüm sanal makineler ve bulut Hizmetleri dahil olmak üzere, sanal ağlar

### <a name="public-peering"></a>Ortak eşleme

* Power BI
* Dynamics 365 Finans ve işlemleri (önceki adıyla Dynamics AX çevrimiçi bilinir)
* Çoğu hello Azure Hizmetleri, birkaç özel durum aşağıdaki hello ile:
  * CDN
  * Visual Studio Team Services yük test etme
  * Multi-factor Authentication
  * Traffic Manager

### <a name="microsoft-peering"></a>Microsoft eşlemesi

* [Office 365](http://aka.ms/ExpressRouteOffice365)
* Dynamics 365 müşteri katılım uygulamaları (önceki adıyla CRM Online bilinir)
  * Dynamics 365 satış
  * Dynamics 365 Müşteri Hizmetleri
  * Dynamics 365 alan hizmeti
  * Dynamics 365 proje hizmeti

## <a name="data-and-connections"></a>Veri ve bağlantıları

### <a name="are-there-limits-on-hello-amount-of-data-that-i-can-transfer-using-expressroute"></a>ExpressRoute kullanarak aktarabilirsiniz veri miktarına hello sınır var mıdır?

Biz bir sınır veri aktarımı hello miktarını ayarlamayın. Çok başvuran[fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/expressroute/) bant genişliği oranları hakkında bilgi için.

### <a name="what-connection-speeds-are-supported-by-expressroute"></a>Hangi bağlantı hızları ExpressRoute tarafından destekleniyor mu?

Desteklenen bant genişliği sunar:

50 Mb/sn, 100 Mb/sn, 200 Mb/sn, 500 Mb/sn, 1 Gb/sn, 2 Gb/sn, 5 Gb/sn, 10 Gb/sn

### <a name="which-service-providers-are-available"></a>Hangi hizmet sağlayıcıları var mı?

Bkz: [ExpressRoute ortakları ve konumları](expressroute-locations.md) hello listesi hizmet sağlayıcıları ve konumları için.

## <a name="technical-details"></a>Teknik Ayrıntılar

### <a name="what-are-hello-technical-requirements-for-connecting-my-on-premises-location-tooazure"></a>My şirket içi konumu tooAzure bağlamak için hello teknik gereksinimleri nelerdir?

Bkz: [ExpressRoute önkoşulları sayfasında](expressroute-prerequisites.md) gereksinimleri için.

### <a name="are-connections-tooexpressroute-redundant"></a>Bağlantıları tooExpressRoute yedek misiniz?

Evet. Her expressroute bağlantı hattı yapılandırılan bağlantıları tooprovide yüksek kullanılabilirlik çapraz yedek çifti var.

### <a name="will-i-lose-connectivity-if-one-of-my-expressroute-links-fail"></a>Bağlantı, ExpressRoute Bağlantılarım biri başarısız olursa kaybedersiniz?

Bağlantı varsa kaybetmezsiniz hello çapraz bağlantıları başarısız olarak. Kullanılabilir toosupport hello yük ağınızın bir yedek bağlantıdır. Ayrıca, birden çok bağlantı hatları bir farklı eşleme konumu tooachieve hatası esnekliği oluşturabilirsiniz.

### <a name="onep2plink"></a>Bulut değişiminde birlikte bulunan değilim ve my hizmet sağlayıcısı, noktadan noktaya bir bağlantı sunar, my şirket içi ağınız ve Microsoft arasında iki fiziksel bağlantılar tooorder ihtiyacım var mı?

Hizmet sağlayıcınıza iki Ethernet sanal devreler hello fiziksel bağlantı oluşturabilir, yalnızca tek bir fiziksel bağlantısı gerekir. Merhaba fiziksel bağlantı (örneğin, bir fiber optik) bir katman 1 (L1) cihaz sonlandırılır (Merhaba görüntü bakın). Merhaba iki Ethernet sanal devreler etiketli bir hello birincil hattı için farklı VLAN kimlikleri hello ikincil için bir tane. Bu VLAN kimlikleri hello dış 802.1Q Ethernet üstbilgisinde ' dir. (gösterilmez) hello iç 802.1Q Ethernet başlığıdır eşlenen tooa belirli [ExpressRoute Yönlendirme etki alanı](expressroute-circuit-peerings.md).

![](./media/expressroute-faqs/expressroute-p2p-ref-arch.png)

### <a name="can-i-extend-one-of-my-vlans-tooazure-using-expressroute"></a>ExpressRoute kullanarak my VLAN tooAzure birini genişletebilir miyim?

Hayır. Katman 2 bağlantı uzantıları Azure'da desteklemiyoruz.

### <a name="can-i-have-more-than-one-expressroute-circuit-in-my-subscription"></a>Aboneliğimi içinde birden fazla expressroute bağlantı hattı olabilir mi?

Evet. Aboneliğinizde birden fazla expressroute bağlantı hattı olabilir. Merhaba varsayılan sınır too10 ayarlanır. Gerekirse Microsoft Support tooincrease hello sınırı başvurabilirsiniz.

### <a name="can-i-have-expressroute-circuits-from-different-service-providers"></a>ExpressRoute bağlantı hatları farklı hizmet sağlayıcılarından olabilir mi?

Evet. Çok sayıda hizmet sağlayıcıları ile ExpressRoute bağlantı hattına sahip olabilir. Her expressroute bağlantı hattı, yalnızca bir hizmet sağlayıcısı ile ilişkilidir. 

### <a name="can-i-have-multiple-expressroute-circuits-in-hello-same-location"></a>Birden çok ExpressRoute bağlantı hatları hello olabilir aynı konuma?

Evet. Birden çok ExpressRoute bağlantı hattına sahip, ile aynı hello ya da farklı hizmet sağlayıcısı'nda aynı konuma hello. Ancak, birden fazla ExpressRoute bağlantı hattı toohello bağlayamazsınız hello aynı aynı sanal ağ konumu.

### <a name="how-do-i-connect-my-virtual-networks-tooan-expressroute-circuit"></a>My sanal ağlar tooan expressroute bağlantı hattı nasıl bağlayabilirim

Merhaba temel adımlar şunlardır:

* Bir expressroute bağlantı hattı oluşturun ve etkinleştirin hello hizmeti sağlayıcısı yüklü.
* Siz veya hello sağlayıcısı hello BGP eşliği (s) yapılandırmanız gerekir.
* Merhaba sanal ağ toohello expressroute bağlantı hattı bağlayın.

Daha fazla bilgi için bkz: [devre sağlama ve devre durumları için ExpressRoute iş akışlarını](expressroute-workflows.md).

### <a name="are-there-connectivity-boundaries-for-my-expressroute-circuit"></a>ExpressRoute devremi bağlantı sınırları vardır?

Evet. Merhaba [ExpressRoute ortakları ve konumları](expressroute-locations.md) makale, bir expressroute bağlantı hattı için hello bağlantı sınırları genel bir bakış sağlar. Bağlantı bir expressroute bağlantı hattı için sınırlı tooa tek coğrafi bölgedir. Bağlantı genişletilmiş toocross coğrafi bölgeler hello ExpressRoute premium özelliğini etkinleştirerek olabilir.

### <a name="can-i-link-toomore-than-one-virtual-network-tooan-expressroute-circuit"></a>Bir sanal ağ tooan expressroute bağlantı hattı daha toomore bağlayabilir miyim?

Evet. Standart bir expressroute bağlantı hattı too10 sanal ağlar bağlantılarında yukarı ve too100 yukarı olabilir bir [premium expressroute bağlantı hattı](#expressroute-premium). 

### <a name="i-have-multiple-azure-subscriptions-that-contain-virtual-networks-can-i-connect-virtual-networks-that-are-in-separate-subscriptions-tooa-single-expressroute-circuit"></a>Sanal ağları içeren birden çok Azure aboneliğiniz var. Ayrı abonelikleri tooa tek expressroute bağlantı hattı sanal ağları bağlayabilir miyim?

Evet. Too10 yetkilendirebilir başka Azure abonelikleri toouse tek bir expressroute bağlantı hattı. Bu sınır hello ExpressRoute premium özelliğini etkinleştirerek artırılabilir.

Daha fazla bilgi için bkz: [bir expressroute bağlantı hattı birden çok abonelik paylaşımı](expressroute-howto-linkvnet-arm.md).

### <a name="are-virtual-networks-connected-toohello-same-circuit-isolated-from-each-other"></a>Aynı bağlantı hattı yalıtılmış sanal ağlara bağlı toohello birbirinden misiniz?

Hayır. Bir yönlendirme perspektif, tüm sanal ağları Bağlantılı toohello aynı expressroute bağlantı hattı parçası olan hello aynı yönlendirme etki alanı ve birbirinden yalıtılmış değildir. Yalıtım rota varsa, toocreate ayrı bir expressroute bağlantı hattı gerekir.

### <a name="can-i-have-one-virtual-network-connected-toomore-than-one-expressroute-circuit"></a>Bir expressroute bağlantı hattı'den bir bağlı sanal ağ toomore olabilir mi?

Evet. Bir tek sanal ağ ile toofour ExpressRoute bağlantı hatları bağlayabilirsiniz. Bunlar farklı dört sıralanmalıdır [ExpressRoute konumları](expressroute-locations.md).

### <a name="can-i-access-hello-internet-from-my-virtual-networks-connected-tooexpressroute-circuits"></a>My sanal ağlar bağlı tooExpressRoute devreler hello Internet erişebilir mi?

Evet. Varsayılan yol (0.0.0.0/0) veya Internet rota öneki hello BGP oturumu üzerinden tanıtılan değil, bir sanal ağ bağlantılı tooan expressroute bağlantı hattı toohello Internet bağlanabilir.

### <a name="can-i-block-internet-connectivity-toovirtual-networks-connected-tooexpressroute-circuits"></a>Internet bağlantısı toovirtual ağlara bağlı tooExpressRoute devreler engelleyebilir miyim?

Evet. Tüm Internet bağlantısı toovirtual makineler bir sanal ağ içinde dağıtılır ve giden tüm trafiği hello expressroute bağlantı hattı üzerinden yönlendirmek varsayılan yol (0.0.0.0/0) tooblock tanıtabilirsiniz.

Varsayılan yolları tanıtma, biz ortak eşleme (örneğin, Azure storage ve SQL DB) geri tooyour şirket içinde sunulan trafik tooservices zorlar. Yönlendiriciler tooreturn trafiği tooAzure hello ortak eşleme yolu hello Internet üzerinden veya tooconfigure sahip olur.

### <a name="can-virtual-networks-linked-toohello-same-expressroute-circuit-talk-tooeach-other"></a>Sanal ağlar bağlantılı toohello için aynı expressroute bağlantı hattı konuşun tooeach diğer?

Evet. Sanal ağlar bağlı toohello aynı expressroute bağlantı hattı birbirleri ile iletişim kurabilen dağıtılan sanal makineleri.

### <a name="can-i-use-site-to-site-connectivity-for-virtual-networks-in-conjunction-with-expressroute"></a>ExpressRoute ile birlikte sanal ağlar için siteden siteye bağlantı kullanabilir miyim?

Evet. ExpressRoute ile siteden siteye VPN bulunabilir.

### <a name="can-i-move-a-virtual-network-from-site-to-site--point-to-site-configuration-toouse-expressroute"></a>Bir sanal ağ ExpressRoute siteden siteye / noktadan siteye yapılandırması toouse taşıyabilir miyim?

Evet. Sanal ağ içindeki bir ExpressRoute ağ geçidi toocreate gerekir. Merhaba işlemle ilişkili kısa bir kapalı kalma süresi yok.

### <a name="why-is-there-a-public-ip-address-associated-with-hello-expressroute-gateway-on-a-virtual-network"></a>Neden bir sanal ağ üzerinde hello ExpressRoute ağ geçidi ile ilgili genel bir IP adresi var mı?

Merhaba genel IP adresi, yalnızca dahili yönetimi için kullanılır. Bu genel IP adresi gösterilen toohello Internet değildir ve güvenlik açıklarını sanal ağınızın niteliğinde değildir.

### <a name="what-do-i-need-tooconnect-tooazure-storage-over-expressroute"></a>Ne ExpressRoute tooconnect tooAzure depolama ihtiyacım?

Bir expressroute bağlantı hattı kurmak ve ortak eşleme rotaları yapılandırmanız gerekir.

### <a name="are-there-limits-on-hello-number-of-routes-i-can-advertise"></a>Tanıtım yolları hello sayısına bir sınır var mıdır?

Evet. Özel eşliği için rota önekleri too4000 ve 200 her ortak eşleme ve Microsoft eşlemesi için kabul. Bu too10 hello ExpressRoute premium özelliğini etkinleştirirseniz, özel eşleme için 000 yollar artırabilir.

### <a name="are-there-restrictions-on-ip-ranges-i-can-advertise-over-hello-bgp-session"></a>IP aralıklarını hello BGP oturumunda tanıtmayı sınırlamalar var mı?

Biz ortak hello öneklerini (RFC1918) özel ve Microsoft eşleme BGP oturumu kabul etmeyin.

### <a name="what-happens-if-i-exceed-hello-bgp-limits"></a>Merhaba BGP sınırları aşmanız durumunda ne olur?

BGP oturumlarını bırakılır. Merhaba ön eki sayım hello limitin altında gider sonra bunlar sıfırlanır.

### <a name="what-is-hello-expressroute-bgp-hold-time-can-it-be-adjusted"></a>ExpressRoute BGP tutun zaman hello nedir? Ayarlanabilir mi?

Merhaba tutma süresi 180'dir. Merhaba etkin tutma iletileri 60 saniyede gönderilir. Bu ayarlar değiştirilemez Microsoft yan hello üzerinde düzeltilmiştir. Sizin için tooconfigure farklı zamanlayıcılar mümkündür ve hello BGP oturumu parametreleri uygun şekilde anlaşma.

### <a name="after-i-advertise-hello-default-route-00000-toomy-virtual-networks-i-cant-activate-windows-running-on-my-azure-vms-how-tooi-fix-this"></a>Merhaba varsayılan yol (0.0.0.0/0) toomy sanal ağlar tanıtma sonra ı my Azure VM'ler üzerinde çalıştırılan Windows etkinleştirilemiyor. Nasıl tooI düzeltme bu?

Aşağıdaki adımları hello hello etkinleştirme isteği tanıması Azure yardımcı olur:

1. Merhaba, expressroute bağlantı hattı için ortak eşleme oluşturun.
2. DNS araması gerçekleştirmek ve hello IP adresini bulmak **kms.core.windows.net**
3. Merhaba anahtar yönetimi hizmeti bu hello etkinleştirme isteği Azure ve Uy hello gelir görmelidir isteği. Üç görevleri aşağıdaki hello birini gerçekleştirin:

   * Şirket içi ağınızda hello trafiği yönlendirme hello için 2. adım arka tooAzure hello ortak eşleme aracılığıyla elde IP adresi hedefleyen.
   * Merhaba ortak eşleme aracılığıyla, NSP sağlayıcısı artı PIN hello trafiği arka tooAzure sahip.
   * Bir kullanıcı tarafından tanımlanan rota sonraki atlama olarak Internet sahip o noktaları hello IP oluşturabilir ve bu sanal makineleri nerede toohello alt ağı uygulayabilirsiniz.

### <a name="can-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Bir expressroute bağlantı hattı hello bant değiştirebilir miyim?

Evet, bant genişliği, expressroute bağlantı hattı hello Azure portal veya PowerShell kullanarak tooincrease hello deneyebilirsiniz. Varsa kapasite kullanılabilir hattınız oluşturulduğu hello fiziksel bağlantı noktası, değişikliğinizin başarılı olur. 

Merhaba geçerli bağlantı noktasında sol yeterli kapasitesi hiç ve toocreate hello daha yüksek bant genişliğine sahip yeni bir expressroute bağlantı hattı veya bu konumda hiçbir ek kapasite yok, bu durumda, açamazsınız gereksinim değişikliğinizin başarısız olursa, anlama tooincrease hello bant genişliği. 

Da toofollow, bağlantı sağlayıcısı tooensure ile Merhaba kısıtlamaları kendi ağları toosupport hello bant genişliği artış içinde güncelleştirme sahip olursunuz. Ancak, expressroute bağlantı hattı hello bant indiremezsiniz. Merhaba eski devreyi silmek ve daha düşük bant genişliğine sahip yeni bir expressroute bağlantı hattı toocreate sahip.

### <a name="how-do-i-change-hello-bandwidth-of-an-expressroute-circuit"></a>Bir expressroute bağlantı hattı hello bant nasıl değişiyor?

Merhaba bant genişliği hello REST API veya PowerShell cmdlet'ini kullanarak hello expressroute bağlantı hattı güncelleştirebilirsiniz.

## <a name="expressroute-premium"></a>ExpressRoute premium

### <a name="what-is-expressroute-premium"></a>ExpressRoute premium nedir?

ExpressRoute premium özellikleri aşağıdaki hello koleksiyonudur:

* Yönlendirme tablosu sayısı sınırını 4000 yollar too10 özel eşleme 000 yollar çıkardı.
* Artan bağlı toohello expressroute bağlantı hattı olabilir Vnet sayısı (varsayılan değer 10). Daha fazla bilgi için bkz: Merhaba [ExpressRoute sınırları](#limits) tablo.
* Bağlantı tooOffice 365 ve Dynamics 365.
* Genel bağlantı hello Microsoft Çekirdek Ağ üzerinden. Şimdi sanal ağ bir coğrafi bölge içinde başka bir bölgede bir expressroute bağlantı hattı ile bağlayabilirsiniz.<br>
    **Örnekler:**

    *  Batı Avrupa tooan Silikon Vadisi'nde oluşturulan expressroute bağlantı hattı oluşturulan bir sanal ağa bağlayabilirsiniz. 
    *  Sağlayacak şekilde, örneğin, SQL Azure Batı Avrupa, Silikon vadisi devredeki gelen bağlanabileceğiniz ortak hello eşleme, diğer jeopolitik bölgeler ön ekleri bildirilir.


### <a name="limits"></a>ExpressRoute premium etkinleştirilirse kaç tane sanal ağlar ı tooan expressroute bağlantı hattı bağlayabilir miyim?

Merhaba aşağıdaki tablolarda hello ExpressRoute sınırları ve expressroute bağlantı hattı başına Vnet hello sayısı gösterilmektedir:

[!INCLUDE [ExpressRoute limits](../../includes/expressroute-limits.md)]

### <a name="how-do-i-enable-expressroute-premium"></a>ExpressRoute premium nasıl etkinleştirebilirim?

ExpressRoute premium özellikleri hello özelliği etkinleştirilmişse, etkin ve hello devre durumunu güncelleştirerek kapatılabilir. ExpressRoute premium hattı oluşturma zamanında etkinleştirebilir ya da hello REST API'si çağırabilirsiniz / PowerShell cmdlet'i.

### <a name="how-do-i-disable-expressroute-premium"></a>ExpressRoute premium nasıl devre dışı bırakabilirim?

ExpressRoute premium hello REST API veya PowerShell cmdlet çağırarak devre dışı bırakabilirsiniz. ExpressRoute premium devre dışı bırakmadan önce bağlantı gereksinimlerini toomeet hello varsayılan sınırları ölçeklendirilmiş emin olmanız gerekir. Merhaba varsayılan sınırlarının dışına kullanımınızı ölçeklendirir hello isteği toodisable ExpressRoute premium başarısız olur.

### <a name="can-i-pick-and-choose-hello-features-i-want-from-hello-premium-feature-set"></a>I seçin ve hello premium özellik kümesinden istediğiniz hello özellikleri seçebilirsiniz.

Hayır. Merhaba özellikleri seçemezsiniz. ExpressRoute premium üzerinde etkinleştirdiğinizde tüm özelliklerini etkinleştiririz.

### <a name="how-much-does-expressroute-premium-cost"></a>ExpressRoute premium maliyet mu ne kadar?

Çok başvuran[fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/expressroute/) maliyeti.

### <a name="do-i-pay-for-expressroute-premium-in-addition-toostandard-expressroute-charges"></a>T için ExpressRoute premium ayrıca toostandard ExpressRoute ücretleri ödeme yaparım?

Evet. ExpressRoute premium ExpressRoute bağlantı hattı ücretleri ve ücretleri hello bağlantı sağlayıcı tarafından gerekli üstünde uygulanabilir.

## <a name="expressroute-for-office-365-and-dynamics-365"></a>Office 365 ve Dynamics 365 için ExpressRoute

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

### <a name="how-do-i-create-an-expressroute-circuit-tooconnect-toooffice-365-services-and-dynamics-365"></a>TooOffice 365 Hizmetleri bir ExpressRoute bağlantı hattı tooconnect nasıl oluşturabilirim ve Dynamics 365?

1. Gözden geçirme hello [ExpressRoute önkoşulları sayfasında](expressroute-prerequisites.md) toomake hello gereksinimleri karşıladığından emin.
2. bağlantınızı gereken tooensure yerine getirildiğinden, hizmet sağlayıcıları ve hello konumlarda hello listesini gözden geçirin [ExpressRoute ortakları ve konumları](expressroute-locations.md) makalesi.
3. Gözden geçirerek, kapasite gereksinimlerini planlama [ağ planlaması ve Office 365 için performans ayarlaması](http://aka.ms/tune/).
4. Bağlantı kurma hello iş akışları tooset listelenen hello adımları [devre sağlama ve devre durumları için ExpressRoute iş akışlarını](expressroute-workflows.md).

> [!IMPORTANT]
> Bağlantı tooOffice 365 Hizmetleri ve Dynamics 365 yapılandırırken ExpressRoute premium eklentisi etkinleştirdiğinizden emin olun.
> 
> 

### <a name="do-i-need-tooenable-azure-public-peering-tooconnect-toooffice-365-services-and-dynamics-365"></a>Tooenable Azure genel eşliği tooconnect tooOffice 365 Hizmetleri ve Dynamics 365 gerekiyor mu?

Hayır, yalnızca tooenable Microsoft Peering gerekir. Kimlik doğrulama trafiğini tooAzure AD Microsoft Peering gönderilir. 

### <a name="can-my-existing-expressroute-circuits-support-connectivity-toooffice-365-services-and-dynamics-365"></a>My mevcut ExpressRoute bağlantı hatları bağlantısı tooOffice 365 hizmetlerini ve Dynamics 365 destekliyor mu?

Evet. Mevcut expressroute bağlantı hattı yapılandırılmış toosupport bağlantı tooOffice 365 Hizmetleri olabilir. Yeterli kapasitesi tooconnect tooOffice 365 Hizmetleri sahip ve premium eklentisi etkinleştirdiğinizden emin olun. [Ağ planlaması ve Office 365 için performans ayarlaması](http://aka.ms/tune/) bağlantınızı planlamanıza yardımcı gerekiyor. Ayrıca bkz [oluşturma ve bir expressroute bağlantı hattı değiştirme](expressroute-howto-circuit-classic.md).

### <a name="what-office-365-services-can-be-accessed-over-an-expressroute-connection"></a>Hangi Office 365 Hizmetleri bir ExpressRoute bağlantı üzerinden erişilebilir?

Çok başvuran[Office 365 URL'leri ve IP adresi aralıkları](http://aka.ms/o365endpoints) ExpressRoute üzerinde desteklenen hizmetlerin güncel bir listesi için sayfa.

### <a name="how-much-does-expressroute-for-office-365-services-and-dynamics-365-cost"></a>Ne kadar ExpressRoute Office 365 hizmetlerinizi ve Dynamics 365 maliyet mu?

Office 365 Hizmetleri ve Dynamics 365 etkin premium eklenti toobe gerektirir. Merhaba bkz [fiyatlandırma ayrıntıları sayfası](https://azure.microsoft.com/pricing/details/expressroute/) maliyetleri için.

### <a name="what-regions-is-expressroute-for-office-365-supported-in"></a>Office 365 için ExpressRoute hangi bölgeleri desteklenir?

Bkz: [ExpressRoute ortakları ve konumları](expressroute-locations.md) bilgi.

### <a name="can-i-access-office-365-over-hello-internet-even-if-expressroute-was-configured-for-my-organization"></a>ExpressRoute Kuruluşum için yapılandırılmış olsa bile hello Internet Office 365 erişebilirim?

Evet. ExpressRoute, ağınız için yapılandırılmış olsa bile office 365 hizmet uç noktaları hello Internet erişilebilir. Yapılandırılmış tooconnect tooOffice 365 Hizmetleri ExpressRoute aracılığıyla bir konumda varsa, ExpressRoute aracılığıyla bağlanır.

### <a name="can-i-access-office-365-us-government-community-gcc-services-over-an-azure-us-government-expressroute-circuit"></a>Office 365 US Government topluluk (GCC) Hizmetleri Azure ABD devlet kurumları expressroute bağlantı hattı erişebilir mi?

Evet. Office 365 GCC hizmet uç noktaları hello Azure ABD devlet kurumları ExpressRoute erişilebilir. Ancak, bir destek bileti, ilk gerek tooopen tooadvertise tooMicrosoft düşündüğünüz Azure portal tooprovide hello öneklerini hello. Merhaba destek bileti çözümlendikten sonra bağlantı tooOffice 365 GCC Hizmetleri kurulur. 

### <a name="can-dynamics-365-for-operations-formerly-known-as-dynamics-ax-online-be-accessed-over-an-expressroute-connection"></a>Dynamics 365 (önceki adıyla Dynamics AX çevrimiçi bilinir) işlemleri için ExpressRoute bağlantısı üzerinden erişilebilir?

Evet. [Dynamics 365 işlemleri için](https://www.microsoft.com/dynamics365/operations) Azure üzerinde barındırılan. Azure ortak, ExpressRoute bağlantı hattı tooconnect tooit eşleme etkinleştirebilirsiniz.

## <a name="route-filters-for-microsoft-peering"></a>Microsoft eşlemesi için yol filtreleri

### <a name="i-am-turning-on-microsoft-peering-for-hello-first-time-what-routes-will-i-see"></a>Kapatma ilk kez Merhaba Microsoft eşlemesi üzerinde hangi yolları ı göreceksiniz?

Tüm yollar görmezsiniz. Bir rota filtre tooyour hattı toostart öneki reklamlar tooattach var. Yönergeler için bkz: [Microsoft eşlemesi için yapılandırma yol filtreleri](how-to-routefilter-powershell.md).

### <a name="i-turned-on-microsoft-peering-and-now-i-am-trying-tooselect-exchange-online-but-it-is-giving-me-an-error-that-i-am-not-authorized-toodo-it"></a>T Microsoft eşleme ve Exchange Online çalışırken tooselect istiyorum, ancak bunu bana yetkili toodo değilim hata veren artık açık.

Yol filtreleri kullanırken, Microsoft eşlemesi üzerinde herhangi bir müşteriye kapatabilirsiniz. Ancak, Office 365 Hizmetleri kullanma için hala Office 365 tarafından yetkili tooget gerekir.

### <a name="do-i-need-tooget-authorization-for-turning-on-dynamics-365-over-microsoft-peering"></a>Tooget yetkilendirme Microsoft eşlemesi üzerinde Dynamics 365 üzerinde etkinleştirilmesinde gerekiyor mu?

Hayır, yetkilendirme için Dynamics 365 gerekmez. Bir kural oluşturmak ve yetkilendirme olmadan Dynamics 365 topluluğu seçin.

### <a name="i-already-have-microsoft-peering-how-can-i-take-advantage-of-route-filters"></a>Microsoft eşlemesi zaten var, nasıl yol filtreleri avantajlarından alabilir?

Filtre tooyour Microsoft eşlemesi toouse istediğiniz ve attach select hello Hizmetleri Merhaba, bir rota filtre oluşturabilirsiniz. Yönergeler için bkz: [Microsoft eşlemesi için yapılandırma yol filtreleri](how-to-routefilter-powershell.md).

### <a name="i-have-microsoft-peering-at-one-location-now-i-am-trying-tooenable-it-at-another-location-and-i-am-not-seeing-any-prefixes"></a>Microsoft tooenable çalışıyorum artık bir konumda eşlemesini sahip, başka bir konumda ve tüm ön eklerin görüyorum değil.

* Önceki tooAugust 1 yapılandırılmış olan ExpressRoute bağlantı hatları Microsoft eşliği, yol filtreleri tanımlanmamış olsa bile 2017 Microsoft eşleme aracılığıyla tanıtılan tüm hizmet ön eklerin sahip olur.

* Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre bağlanana kadar tanıtılan toohello hattı. Varsayılan olarak hiçbir önekleri görürsünüz.
