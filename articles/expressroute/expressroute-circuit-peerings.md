---
title: "Azure ExpressRoute bağlantı hatları ve Yönlendirme etki alanları | Microsoft Docs"
description: "Bu sayfa ExpressRoute bağlantı hatları ve Yönlendirme etki alanları genel bir bakış sağlar."
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
ms.openlocfilehash: bbf34d6ccd51091facd4f0dcea4855529e4e92e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="expressroute-circuits-and-routing-domains"></a>ExpressRoute bağlantı hatları ve Yönlendirme etki alanları
 Sipariş gerekir bir *expressroute bağlantı hattı* şirket içi altyapınızı bağlantı sağlayıcı Microsoft'a bağlanmak için. Aşağıdaki şekilde bir mantıksal temsilini WAN ve Microsoft arasında bağlantı sağlar.

![](./media/expressroute-circuit-peerings/expressroute-basic.png)

## <a name="expressroute-circuits"></a>ExpressRoute bağlantı hatları
Bir *expressroute bağlantı hattı* şirket içi altyapınızı ve bağlantı sağlayıcı üzerinden Microsoft bulut hizmetleri arasında mantıksal bağlantıyı temsil eder. Birden çok ExpressRoute bağlantı hatları sıralayabilirsiniz. Her bağlantı hattı, aynı veya farklı bölgelerde olabilir ve şirketinizde farklı bağlantı sağlayıcıları üzerinden bağlanır. 

ExpressRoute bağlantı hatları için herhangi bir fiziksel varlık eşleme yok. Bir bağlantı hattı benzersiz GUID bir hizmet anahtarı (s-anahtarı) adlı bir standart olarak tanımlanır. Hizmet anahtarı yalnızca Microsoft, bağlantı sağlayıcısı ve sizin arasında alınıp bilgidir. S anahtarı güvenlik amacıyla bir gizlilik değil. Bir expressroute bağlantı hattı ve s anahtar arasındaki 1:1 eşleme yoktur.

Bir expressroute bağlantı hattı en fazla üç bağımsız eşlemenin sahip olabilir: Azure genel, Azure özel ve Microsoft. Her eşleme bağımsız BGP çiftinin her bunların nedenle yüksek kullanılabilirlik için yapılandırılmış oturumdur. 1: n yoktur (1 < = N < = 3) arasında bir expressroute bağlantı hattı eşlemesi ve Yönlendirme etki alanları. Bir expressroute bağlantı hattı herhangi biri, iki veya üç eşlemenin expressroute bağlantı hattı etkin tamamını olabilir.

Her bağlantı hattı (50 MB/sn, 100 MB/sn, 200 MB/sn, 500 MB/sn, 1 GB/sn, 10 GB/sn) sabit bir bant genişliğine sahiptir ve bağlantı sağlayıcı ve eşleme konumu eşlendi. Seçtiğiniz bant genişliği bağlantı hattı için tüm eşlemeler arasında paylaşılır. 

### <a name="quotas-limits-and-limitations"></a>Kotalar, sınırlar ve sınırlamalar
Varsayılan kotalar ve sınırlar her expressroute bağlantı hattı için geçerlidir. Başvurmak [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md) Kotalar hakkında güncel bilgi sayfası.

## <a name="expressroute-routing-domains"></a>ExpressRoute yönlendirme etki alanları
Bir expressroute bağlantı hattı kendisiyle ilişkili birden fazla Yönlendirme etki alanları sahiptir: Azure genel, Azure özel ve Microsoft. Her bir yönlendirme etki alanları aynı yönlendiriciler çifti üzerinde yapılandırılmış (etkin-etkin ya da yük paylaşma yapılandırma) yüksek kullanılabilirlik için. Azure Hizmetleri olarak kategorilere *Azure genel* ve *Azure özel* IP adresleme şemasını temsil etmek için.

![](./media/expressroute-circuit-peerings/expressroute-peerings.png)

### <a name="private-peering"></a>Özel eşleme
Azure işlem Hizmetleri, yani sanal makineler (Iaas) ve bir sanal ağ içindeki dağıtılan bulut hizmetlerini (PaaS) üzerinden özel eşleme etki alanına bağlanabilir. Özel Eşleme etki alanı çekirdek ağınıza Microsoft Azure için güvenilen bir uzantısı olarak kabul edilir. Azure sanal ağlar (Vnet'ler) ve çekirdek ağınızı arasında çift yönlü bağlantı ayarlayabilirsiniz. Bu eşleme, sanal makinelere bağlanmak ve özel IP adresleri doğrudan Services'de bulut sağlar.  

Özel Eşleme etki alanı için birden fazla sanal ağ bağlanabilir. Gözden geçirme [SSS sayfasını](expressroute-faqs.md) sınırlar ve sınırlamalar hakkında bilgi için. Ziyaret ettiğiniz [Azure aboneliği ve hizmet sınırları, kotaları ve kısıtlamaları](../azure-subscription-service-limits.md) sınırları hakkında güncel bilgi sayfası.  Başvurmak [yönlendirme](expressroute-routing.md) yönlendirme yapılandırması hakkında ayrıntılı bilgi için sayfa.

### <a name="public-peering"></a>Ortak eşleme
Azure Storage, SQL veritabanları ve Web siteleri gibi hizmetleri ortak IP adreslerini sunulur. Özel olarak, bulut hizmetleriyle ortak eşleme Yönlendirme etki alanı VIP'ler dahil olmak üzere, genel IP adresleri barındırılan hizmetlere bağlanabilir. Ortak eşleme etki alanı için çevre ağınız bağlanmak ve ortak IP adresleri üzerindeki tüm Azure hizmetlerine WAN'ınız Internet üzerinden bağlanmak zorunda kalmadan bağlanın. 

Bağlantı, her zaman Microsoft Azure hizmetlerini WAN'ınız başlatılır. Microsoft Azure Hizmetleri, ağınızda bu yönlendirme etki alanı aracılığıyla bağlantılar başlatamaz olmaz. Ortak eşleme etkinleştirildikten sonra tüm Azure hizmetlerine bağlanmasına olacaktır. Biz, seçmeli olarak biz yolları tanıtma Hizmetleri seçmenize olanak izin vermez. Size bildirmek için bu eşlemenin aracılığıyla önekleri listesini gözden geçirebilirsiniz [Microsoft Azure veri merkezi IP aralıkları](http://www.microsoft.com/download/details.aspx?id=41653) sayfası. Sayfa haftalık güncelleştirilir.

Yalnızca gereksinim duyduğunuz yolların tüketmeye ağınızın içinde özel yol filtreleri tanımlayabilirsiniz. Başvurmak [yönlendirme](expressroute-routing.md) yönlendirme yapılandırması hakkında ayrıntılı bilgi için sayfa. 

Bkz: [SSS sayfasını](expressroute-faqs.md) desteklenen ortak eşleme Yönlendirme etki alanı hizmetleri hakkında daha fazla bilgi için. 

### <a name="microsoft-peering"></a>Microsoft eşlemesi
[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

Tüm diğer Microsoft Çevrimiçi Hizmetleri için bağlantı (örneğin, Office 365 Hizmetleri) Microsoft eşleme aracılığıyla olacaktır. Biz, WAN ve Microsoft bulut hizmetleriyle Microsoft eşliği Yönlendirme etki alanı arasında çift yönlü bağlantı etkinleştirin. Yalnızca siz veya bağlantı sağlayıcınız tarafından sahip olunan genel IP adresleri üzerinden Microsoft bulut hizmetlerine bağlanmak ve tüm tanımlı kurallara uymalıdır. Bkz: [ExpressRoute önkoşulları](expressroute-prerequisites.md) daha fazla bilgi için.

Bkz: [SSS sayfasını](expressroute-faqs.md) daha fazla bilgi desteklenen Hizmetleri, maliyetleri ve yapılandırma ayrıntıları. Bkz: [ExpressRoute konumları](expressroute-locations.md) Microsoft eşleme desteği sunan bağlantı sağlayıcıları listesi hakkında bilgi için sayfa.

## <a name="routing-domain-comparison"></a>Yönlendirme etki alanı karşılaştırma
Aşağıdaki tabloda, üç yönlendirme etki alanları karşılaştırır.

|  | **Özel eşleme** | **Ortak eşleme** | **Microsoft eşlemesi** |
| --- | --- | --- | --- |
| **Maks. eşleme başına desteklenen # önekleri** |Varsayılan olarak, ExpressRoute Premium 10.000 4000 |200 |200 |
| **Desteklenen IP adres aralıkları** |Geçerli bir IPv4 adresi WAN'ınız içinde. |Siz veya bağlantı sağlayıcınız tarafından sahip olunan genel IPv4 adresi. |Siz veya bağlantı sağlayıcınız tarafından sahip olunan genel IPv4 adresi. |
| **Gereksinim sayısı olarak** |Özel ve ortak AS numaraları. Ortak sahibi kullanmayı seçerseniz bir sayı olarak. |Özel ve ortak AS numaraları. Ancak, genel IP adresleri sahipliğini kanıtlamanız gerekir. |Özel ve ortak AS numaraları. Ancak, genel IP adresleri sahipliğini kanıtlamanız gerekir. |
| **Yönlendirme arabirimi IP adresleri** |RFC1918 ve genel IP adresleri |Genel IP adresleri kayıt defterlerini yönlendirme kaydettiniz. |Genel IP adresleri kayıt defterlerini yönlendirme kaydettiniz. |
| **MD5 karma değeri desteği** |Evet |Evet |Evet |

Bir veya daha fazla Yönlendirme etki alanları, expressroute bağlantı hattı bir parçası olarak etkinleştirmeyi seçebilirsiniz. Tek bir yönlendirme etki alanına birleştirmek istiyorsanız aynı VPN put tüm Yönlendirme etki alanları sahip olmayı seçebilirsiniz. Ayrıca bunları farklı yönlendirme etki alanları, diyagrama benzer koyabilirsiniz. Önerilen özel eşleme çekirdek ağı'na doğrudan bağlı ve genel ve Microsoft eşleme bağlantıları çevre ağınız bağlı yapılandırmadır.

Tüm üç eşliği oturumlarını tercih ediyorsanız, BGP oturumları (her eşleme türü için bir çift) üç çiftleri bulunmalıdır. BGP oturumu çiftleri yüksek oranda kullanılabilir bir bağlantı sağlayın. Katman 2 bağlantı sağlayıcıları bağlanıyorsanız, yapılandırma ve yönlendirme yönetmekten sorumlu olacaktır. İnceleyerek daha fazla bilgi edinebilirsiniz [iş akışları](expressroute-workflows.md) ExpressRoute ayarlama.

## <a name="next-steps"></a>Sonraki adımlar
* Bir hizmet sağlayıcı bulun. Bkz: [ExpressRoute hizmet sağlayıcıları ve konumları](expressroute-locations.md).
* Tüm önkoşulların sağlandığından emin olun. Bkz. [ExpressRoute önkoşulları](expressroute-prerequisites.md).
* ExpressRoute bağlantınızı yapılandırın.
  * [ExpressRoute devreleri oluşturup yönetme](expressroute-howto-circuit-portal-resource-manager.md)
  * [ExpressRoute işlem hatları için yönlendirmeyi (eşleme) yapılandırma](expressroute-howto-routing-portal-resource-manager.md)

