---
title: "aaaAzure ExpressRoute bağlantı hatları ve Yönlendirme etki alanları | Microsoft Docs"
description: "Bu sayfa ExpressRoute bağlantı hatları ve etki alanlarını yönlendirme hello genel bakış sağlar."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: 6f0c5d8e-cc60-4a04-8641-2c211bda93d9
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: cherylmc
ms.openlocfilehash: 1d43cbf668accdd7aa4efb053ea1e9027d10e4a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-circuits-and-routing-domains"></a>ExpressRoute bağlantı hatları ve Yönlendirme etki alanları
 Sipariş gerekir bir *expressroute bağlantı hattı* tooconnect, şirket içi altyapı tooMicrosoft bağlantı sağlayıcı üzerinden. Aşağıdaki şekilde Hello bir mantıksal temsilini WAN ve Microsoft arasında bağlantı sağlar.

![](./media/expressroute-circuit-peerings/expressroute-basic.png)

## <a name="expressroute-circuits"></a>ExpressRoute bağlantı hatları
Bir *expressroute bağlantı hattı* şirket içi altyapınızı ve bağlantı sağlayıcı üzerinden Microsoft bulut hizmetleri arasında mantıksal bağlantıyı temsil eder. Birden çok ExpressRoute bağlantı hatları sıralayabilirsiniz. Her bağlantı hattı olabilir hello aynı ya da farklı bölgelerde ve farklı bağlantı sağlayıcıları üzerinden bağlı tooyour şirket içi olabilir. 

ExpressRoute bağlantı hatları tooany fiziksel varlıkları eşleme yok. Bir bağlantı hattı benzersiz GUID bir hizmet anahtarı (s-anahtarı) adlı bir standart olarak tanımlanır. Merhaba hizmet anahtarı hello yalnızca Microsoft, hello bağlantı sağlayıcısı ve sizin arasında alınıp bilgidir. Merhaba s anahtar güvenlik amacıyla bir gizlilik değil. Bir expressroute bağlantı hattı ve hello arasındaki 1:1 eşleme s anahtarı.

Bir expressroute bağlantı hattı toothree bağımsız eşlemeleri sahip olabilir: Azure genel, Azure özel ve Microsoft. Her eşleme bağımsız BGP çiftinin her bunların nedenle yüksek kullanılabilirlik için yapılandırılmış oturumdur. 1: n yoktur (1 < = N < = 3) arasında bir expressroute bağlantı hattı eşlemesi ve Yönlendirme etki alanları. Bir expressroute bağlantı hattı herhangi biri, iki veya üç eşlemenin expressroute bağlantı hattı etkin tamamını olabilir.

Her bağlantı hattı (50 MB/sn, 100 MB/sn, 200 MB/sn, 500 MB/sn, 1 GB/sn, 10 GB/sn) sabit bir bant genişliğine sahiptir ve eşlenen tooa bağlantı sağlayıcı ve eşleme konumu. Seçtiğiniz hello bant genişliği hello hattı için tüm hello eşlemeler arasında paylaşılır. 

### <a name="quotas-limits-and-limitations"></a>Kotalar, sınırlar ve sınırlamalar
Varsayılan kotalar ve sınırlar her expressroute bağlantı hattı için geçerlidir. Toohello başvuran [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md) Kotalar hakkında güncel bilgi sayfası.

## <a name="expressroute-routing-domains"></a>ExpressRoute yönlendirme etki alanları
Bir expressroute bağlantı hattı kendisiyle ilişkili birden fazla Yönlendirme etki alanları sahiptir: Azure genel, Azure özel ve Microsoft. Her hello Yönlendirme etki alanları aynı yönlendiriciler çifti üzerinde yapılandırılmış (etkin-etkin ya da yük paylaşma yapılandırma) yüksek kullanılabilirlik için. Azure Hizmetleri olarak kategorilere *Azure genel* ve *Azure özel* toorepresent hello IP adresleme düzeni.

![](./media/expressroute-circuit-peerings/expressroute-peerings.png)

### <a name="private-peering"></a>Özel eşleme
Azure işlem Hizmetleri, yani sanal makineler (Iaas) ve bulut hizmetlerini (PaaS), bir sanal ağ içindeki dağıtılan hello özel eşleme üzerinden etki alanına bağlanabilir. Merhaba özel eşleme etki alanı Microsoft Azure'da toobe çekirdek ağınızı, güvenilen bir uzantısı olarak kabul edilir. Azure sanal ağlar (Vnet'ler) ve çekirdek ağınızı arasında çift yönlü bağlantı ayarlayabilirsiniz. Bu eşleme toovirtual makinelere bağlanmak ve özel IP adresleri doğrudan Services'de bulut sağlar.  

Birden fazla sanal ağ toohello özel eşleme etki alanına bağlanabilir. Gözden geçirme hello [SSS sayfasını](expressroute-faqs.md) sınırlar ve sınırlamalar hakkında bilgi için. Merhaba ziyaret ettiğiniz [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md) sınırları hakkında güncel bilgi sayfası.  Toohello başvuran [yönlendirme](expressroute-routing.md) yönlendirme yapılandırması hakkında ayrıntılı bilgi için sayfa.

### <a name="public-peering"></a>Ortak eşleme
Azure Storage, SQL veritabanları ve Web siteleri gibi hizmetleri ortak IP adreslerini sunulur. Merhaba ortak eşleme Yönlendirme etki alanı aracılığıyla bulut hizmetlerinizi VIP'ler dahil olmak üzere, genel IP adresleri barındırılan tooservices özel olarak bağlanabilir. Merhaba ortak eşleme etki alanı tooyour DMZ bağlanabilir ve tooall Azure connect ortak IP adresleri üzerinden tooconnect kalmadan WAN bağlantınızdan Services'de hello Internet. 

Bağlantı, WAN tooMicrosoft Azure her zaman başlatılan Hizmetleri. Microsoft Azure Hizmetleri bu yönlendirme etki alanı ağınızdan mümkün tooinitiate bağlantıları olmaz. Ortak eşleme etkinleştirildikten sonra mümkün tooconnect tooall Azure olacaktır Hizmetleri. Biz biz yolları tanıtma tooselectively çekme Hizmetleri izin vermiyor. Biz bu üzerinde hello eşleme aracılığıyla tooyou tanıtma önekleri hello listesini gözden geçirebilirsiniz [Microsoft Azure veri merkezi IP aralıkları](http://www.microsoft.com/download/details.aspx?id=41653) sayfası. Başlangıç sayfası haftalık güncelleştirilir.

Gereksinim duyduğunuz ağ tooconsume yalnızca hello yollarınızı içinde özel yol filtreleri tanımlayabilirsiniz. Toohello başvuran [yönlendirme](expressroute-routing.md) yönlendirme yapılandırması hakkında ayrıntılı bilgi için sayfa. 

Merhaba bkz [SSS sayfasını](expressroute-faqs.md) hello ortak eşleme Yönlendirme etki alanı ile desteklenen hizmetleri hakkında daha fazla bilgi için. 

### <a name="microsoft-peering"></a>Microsoft eşlemesi
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Bağlantı tooall (Office 365 Hizmetleri gibi) diğer Microsoft online services hello Microsoft eşleme aracılığıyla olacaktır. Biz, WAN ve Microsoft bulut hizmetleriyle hello Microsoft eşliği Yönlendirme etki alanı arasında çift yönlü bağlantı etkinleştirin. Yalnızca siz veya bağlantı sağlayıcınız tarafından sahip olunan genel IP adresleri üzerinden tooMicrosoft bulut hizmetlerine bağlanacak ve tooall tanımlanan hello kuralları uyması gerekir. Merhaba bkz [ExpressRoute önkoşulları](expressroute-prerequisites.md) daha fazla bilgi için.

Merhaba bkz [SSS sayfasını](expressroute-faqs.md) daha fazla bilgi desteklenen Hizmetleri, maliyetleri ve yapılandırma ayrıntıları. Merhaba bkz [ExpressRoute konumları](expressroute-locations.md) Microsoft eşleme desteği sunan bağlantı sağlayıcıları hello listesinde bilgi sayfası.

## <a name="routing-domain-comparison"></a>Yönlendirme etki alanı karşılaştırma
Merhaba tabloda hello üç yönlendirme etki alanları karşılaştırır.

|  | **Özel eşleme** | **Ortak eşleme** | **Microsoft eşlemesi** |
| --- | --- | --- | --- |
| **Maks. eşleme başına desteklenen # önekleri** |Varsayılan olarak, ExpressRoute Premium 10.000 4000 |200 |200 |
| **Desteklenen IP adres aralıkları** |Geçerli bir IPv4 adresi WAN'ınız içinde. |Siz veya bağlantı sağlayıcınız tarafından sahip olunan genel IPv4 adresi. |Siz veya bağlantı sağlayıcınız tarafından sahip olunan genel IPv4 adresi. |
| **Gereksinim sayısı olarak** |Özel ve ortak AS numaraları. Size gereken ait hello ortak toouse birini seçerseniz bir sayı olarak. |Özel ve ortak AS numaraları. Ancak, genel IP adresleri sahipliğini kanıtlamanız gerekir. |Özel ve ortak AS numaraları. Ancak, genel IP adresleri sahipliğini kanıtlamanız gerekir. |
| **Yönlendirme arabirimi IP adresleri** |RFC1918 ve genel IP adresleri |Kayıt defterlerini yönlendirme içinde kayıtlı tooyou bir ortak IP adresleri. |Kayıt defterlerini yönlendirme içinde kayıtlı tooyou bir ortak IP adresleri. |
| **MD5 karma değeri desteği** |Evet |Evet |Evet |

ExpressRoute bağlantı hattınız bir parçası olarak bir veya daha fazla hello Yönlendirme etki alanlarının tooenable seçebilirsiniz. Yerleştirin tüm hello Yönlendirme etki alanları toohave seçebilirsiniz toocombine istiyorsanız aynı VPN hello bunları tek bir yönlendirme etki alanına. Bunları farklı yönlendirme etki alanları üzerinde benzer toohello diyagramı de koyabilirsiniz. Merhaba olduğundan bu özel eşleme bağlı doğrudan toohello Çekirdek Ağ ve hello ortak ve Microsoft eşleme bağlantıları bağlı tooyour DMZ yapılandırma önerilir.

Tüm üç eşliği oturumlarını toohave seçerseniz, BGP oturumları (her eşleme türü için bir çift) üç çiftleri bulunmalıdır. Merhaba BGP oturumu çiftleri yüksek oranda kullanılabilir bir bağlantı sağlayın. Katman 2 bağlantı sağlayıcıları bağlanıyorsanız, yapılandırma ve yönlendirme yönetmekten sorumlu olacaktır. Merhaba inceleyerek daha fazla bilgi edinebilirsiniz [iş akışları](expressroute-workflows.md) ExpressRoute ayarlama.

## <a name="next-steps"></a>Sonraki adımlar
* Bir hizmet sağlayıcı bulun. Bkz: [ExpressRoute hizmet sağlayıcıları ve konumları](expressroute-locations.md).
* Tüm önkoşulların sağlandığından emin olun. Bkz. [ExpressRoute önkoşulları](expressroute-prerequisites.md).
* ExpressRoute bağlantınızı yapılandırın.
  * [ExpressRoute devreleri oluşturup yönetme](expressroute-howto-circuit-portal-resource-manager.md)
  * [ExpressRoute işlem hatları için yönlendirmeyi (eşleme) yapılandırma](expressroute-howto-routing-portal-resource-manager.md)

