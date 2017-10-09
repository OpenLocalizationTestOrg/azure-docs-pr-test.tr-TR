---
title: "ExpressRoute genel bakış: özel bir bağlantı üzerinden şirket içi ağ tooAzure genişletmek | Microsoft Docs"
description: "Bu ExpressRoute teknik genel bakış ExpressRoute bağlantısı tooextend, şirket içi ağ tooAzure özel bir bağlantı üzerinden nasıl çalıştığını açıklar."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: fd95dcd5-df1d-41d6-85dd-e91d0091af05
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 01301e1205c12ecdab34dc9d9b92bc7489e7826c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-overview"></a>ExpressRoute'a genel bakış
Microsoft Azure ExpressRoute bağlantı sağlayıcı tarafından kolaylaştırılan özel bir bağlantı üzerinden şirket içi ağlarınızı Microsoft bulut hello genişletmenizi sağlar. ExpressRoute ile Microsoft Azure, Office 365 ve Dynamics 365 gibi bağlantıları tooMicrosoft bulut Hizmetleri kurabilirsiniz.

Ortak yerleşim tesisinde bağlantı sağlayıcısı üzerinden herhangi bir ağdan herhangi bir ağa (IP VP), noktadan noktaya Ethernet ağı veya sanal çapraz bağlantısından bağlantı olabilir.  ExpressRoute bağlantıları hello Git değil genel Internet. Bu ExpressRoute bağlantıları toooffer daha fazla güvenilirlik, yüksek hız, düşük gecikme ve normal bağlantıları daha yüksek güvenlik hello Internet sağlar. Hakkında bilgi için tooconnect ExpressRoute kullanılarak, ağ tooMicrosoft bkz [ExpressRoute bağlantı modeli](expressroute-connectivity-models.md).

![](./media/expressroute-introduction/expressroute-connection-overview.png)

## <a name="key-benefits"></a>Önemli avantajlar

* Katman 3 bağlantısı şirket içi ağınız ile bağlantı sağlayıcı üzerinden hello Microsoft Cloud arasındaki. Herhangi bir ağdan herhangi bir (IPVPN) ağa, noktadan noktaya Ethernet bağlantısı veya Ethernet değişimi aracığıyla sanal çapraz bağlantısı üzerinden bağlantı olabilir.
* Merhaba coğrafi bölgedeki tüm bölgeler arasında bağlantı tooMicrosoft bulut Hizmetleri.
* Genel bağlantı tooMicrosoft Hizmetleri ExpressRoute premium eklentisine sahip tüm bölgelere arasında.
* Endüstri standardı protokolleri (BGP) üzerinden ağınız ve Microsoft arasında dinamik yönlendirme.
* Yüksek güvenilirlik için her eşleme konumunda yerleşik yedeklilik.
* Bağlantı çalışma süresi [SLA](https://azure.microsoft.com/support/legal/sla/).
* Skype Kurumsal için QoS.

Daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).

## <a name="features"></a>Özellikler

### <a name="layer-3-connectivity"></a>Katman 3 bağlantısı
Microsoft kullanır endüstri standart dinamik yönlendirme protokolü (BGP) tooexchange genel adresleri örneklerinizi azure'da, şirket içi ağınız ve Microsoft arasında yönlendirir.  Farklı trafik profilleri için ağınızda çoklu BGP oturumları kuruyoruz. Daha fazla ayrıntı hello bulunabilir [ExpressRoute bağlantı hattı ve Yönlendirme etki alanları](expressroute-circuit-peerings.md) makalesi.

### <a name="redundancy"></a>Yedeklilik
Her expressroute bağlantı hattı hello bağlantı sağlayıcısından iki bağlantı tootwo Microsoft Enterprise sınır yönlendiricileri (Msee) oluşur /, ağınızın kenarından. Microsoft hello bağlantı sağlayıcısından ikili BGP bağlantısı gerektiren / yan – bir tooeach MSEE. Yedekli cihazlara değil toodeploy seçebilir veya Ethernet bağlantı hattına tarafınızdaki. Ancak, bağlantı sağlayıcıları bağlantılarınızı tooMicrosoft gereksiz bir şekilde verilir. yedekli cihazlar tooensure kullanın. Yedekli Layer 3 bağlantı yapılandırması için bir gereksinimdir bizim [SLA](https://azure.microsoft.com/support/legal/sla/) toobe geçerli.

### <a name="connectivity-toomicrosoft-cloud-services"></a>Bağlantı tooMicrosoft bulut Hizmetleri
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

ExpressRoute bağlantıları Hizmetleri aşağıdaki erişim toohello etkinleştirin:

* Microsoft Azure hizmetleri
* Microsoft Office 365 hizmetleri
* Microsoft Dynamics 365

Merhaba ziyaret ettiğiniz [ExpressRoute SSS](expressroute-faqs.md) sayfa ExpressRoute üzerinde desteklenen hizmetlerin ayrıntılı bir listesi için.

### <a name="connectivity-tooall-regions-within-a-geopolitical-region"></a>Coğrafi bölge içindeki bağlantı tooall bölgeleri
TooMicrosoft birinde bağlanabilir bizim [eşleme konumları](expressroute-locations.md) ve erişim tooall bölgeler hello jeopolitik bölge içinde. 

Örneğin, tooMicrosoft amsterdam'da ExpressRoute aracılığıyla bağlandıysanız Kuzey Avrupa ve Batı Avrupa'da barındırılan erişim tooall Microsoft bulut hizmetlerine sahip. Merhaba bkz [ExpressRoute ortakları ve eşleme konumları](expressroute-locations.md) hello jeopolitik bölgeler, ilişkili Microsoft bulut bölgeleri ve karşılık gelen ExpressRoute eşleme konumlarına genel bir bakış için makale.

### <a name="global-connectivity-with-expressroute-premium-add-on"></a>ExpressRoute premium eklentisine ile genel bağlantı
Coğrafi sınırlar arasındaki hello ExpressRoute premium eklenti özelliğini tooextend bağlantı etkinleştirebilirsiniz. Örneğin, amsterdam'da ExpressRoute aracılığıyla bağlanan tooMicrosoft varsa, tüm bölgelerde Merhaba dünya genelindeki barındırılan erişim tooall Microsoft bulut hizmetlerine sahip olur (Ulusal Bulutlar dışında). Aynı şekilde size erişim hello Kuzey Güney Amerika ve Avustralya'da hello ve Batı Avrupa bölgeler dağıtılan Hizmetleri erişebilir.

### <a name="rich-connectivity-partner-ecosystem"></a>Zengin bağlantı iş ortağı ekosistemi
ExpressRoute sürekli büyüyen bağlantı sağlayıcıları ve SI ortakları ekosistemine sahiptir. Toohello başvurabilir [ExpressRoute sağlayıcıları ve konumları](expressroute-locations.md) hello en son bilgiler için makalenin.

### <a name="connectivity-toonational-clouds"></a>Bağlantı toonational Bulutlar
Microsoft, özel coğrafi bölgeler ve müşteri kesimine yönelik yalıtılmış bulut ortamlarını çalıştırır. Toohello başvuran [ExpressRoute sağlayıcıları ve konumları](expressroute-locations.md) sayfa Ulusal Bulutlar ve sağlayıcılar listesi.

### <a name="bandwidth-options"></a>Bant genişliği seçenekleri
ExpressRoute bağlantı hattını çeşitli sayıda bant genişlikleriyle satın alabilirsiniz. Desteklenen bant genişlikleri aşağıda listelenmiştir. Sağladıkları desteklenen bant genişlikleri bağlantı sağlayıcısı toodetermine hello listesi ile emin toocheck olabilir.

* 50 Mbps
* 100 Mbps
* 200 Mbps
* 500 Mbps
* 1 Gbps
* 2 Gbps
* 5 Gbps
* 10 Gbps

### <a name="dynamic-scaling-of-bandwidth"></a>Bant genişliğini dinamik ölçeklendirme
Bağlantılarınızı aşağı tootear gerek kalmadan hello expressroute bağlantı hattı bant genişliğini (en iyi çaba ilkesine) artırabilir. 

### <a name="flexible-billing-models"></a>Esnek faturalama modelleri
Size en uygun faturalama modelini seçin. Aşağıda listelenen faturalama modelleri hello arasından seçim yapın. Daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).

* **Sınırsız veri**. Merhaba expressroute bağlantı hattı aylık ücrete dayalı olarak ücretlendirilir ve tüm gelen ve giden veri aktarımı ücretsiz olarak yer. 
* **Tarifeli veri**. Merhaba expressroute bağlantı hattı aylık ücrete dayalı olarak ücretlendirilir. Tüm gelen veri aktarımı ücretsizdir. Giden veri aktarımı, her GB veri aktarımı için ücretlendirilir. Veri aktarımı bölgelere göre farklılık gösterir.
* **ExpressRoute premium eklentisi**. Merhaba ExpressRoute premium eklenti hello expressroute bağlantı hattı ' dir. Merhaba ExpressRoute premium eklentisi aşağıdaki yetenekleri hello sağlar: 
  * Azure ortak ve Azure özel 000 yollar 4.000 yollar too10 eşleme için artırılmış yol sınırları.
  * Hizmetler için genel bağlantı. (Ulusal Bulutlar dışında) herhangi bir bölgede oluşturulan expressroute bağlantı hattı üzerinden herhangi bir hello world bölgede erişim tooresources sahip olur. Örneğin, Batı Avrupa’da oluşturulan bir sana ağa Silikon Vadisi’nde sağlanan bir ExpressRoute bağlantı hattı üzerinden erişilebilir.
  * Merhaba bant genişliği hello bağlantı hattının bağlı olarak 10 tooa büyük sınırı expressroute bağlantı hattı başına VNet bağlantı sayısının artması.

## <a name="faq"></a>SSS

ExpressRoute hakkında sık sorulan sorular için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).

## <a name="next-steps"></a>Sonraki adımlar

* [ExpressRoute bağlantı modelleri](expressroute-connectivity-models.md) hakkında bilgi edinin.
* ExpressRoute bağlantıları ve yönlendirme etki alanları hakkında bilgi edinin. Bkz. [ExpressRoute bağlantı hatları ve etki alanlarını yönlendirme](expressroute-circuit-peerings.md).
* Bir hizmet sağlayıcı bulun. Bkz. [ExpressRoute ortakları ve eşleme konumları](expressroute-locations.md).
* Tüm önkoşulların sağlandığından emin olun. Bkz. [ExpressRoute önkoşulları](expressroute-prerequisites.md).
* Toohello gereksinimleri başvuran [yönlendirme](expressroute-routing.md), [NAT](expressroute-nat.md), ve [QoS](expressroute-qos.md).
* ExpressRoute bağlantınızı yapılandırın.
  * [ExpressRoute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md)
  * [ExpressRoute bağlantı hattı için eşleme yapılandırma](expressroute-howto-routing-portal-resource-manager.md)
  * [Sanal ağ tooan expressroute bağlantı hattı Bağlan](expressroute-howto-linkvnet-portal-resource-manager.md)
* Merhaba bazıları hakkında bilgi edinin başka bir anahtar [ağı yetenekleri](../networking/networking-overview.md) Azure.
