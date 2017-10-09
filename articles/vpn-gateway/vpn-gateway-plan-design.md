---
title: "Planlama ve tasarım şirket içi bağlantılar için: Azure VPN ağ geçidi | Microsoft Docs"
description: "VPN ağ geçidi planlama ve tasarım şirketler arası, karma ve VNet-VNet bağlantıları hakkında bilgi edinin"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d5aaab83-4e74-4484-8bf0-cc465811e757
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/27/2017
ms.author: cherylmc
ms.openlocfilehash: 3d4587ba31d163384212eca88a7e2c0ba8f3b21f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="planning-and-design-for-vpn-gateway"></a>VPN Gateway için planlama ve tasarım

Planlama ve tasarlama şirketler arası ve VNet-VNet yapılandırmaları basit ya da ağ gereksinimlerinize bağlı olarak karmaşık olabilir. Bu makalede temel planlama ve tasarım konuları anlatılmaktadır.

## <a name="planning"></a>Planlama

### <a name="compare"></a>Şirketler arası bağlantı seçenekleri

Tooconnect istiyorsanız, şirket içi siteler güvenli bir şekilde tooa sanal ağ, bu nedenle üç farklı şekilde toodo gerekir: siteden siteye noktadan siteye ve ExpressRoute. Kullanılabilir hello farklı şirket içi bağlantılar karşılaştırın. Merhaba seçeneği gibi çeşitli etmenlere bağlı olabilir:

* Çözümünüz ne tür bir verimlilik gerektiriyor?
* Merhaba toocommunicate istiyorsunuz genel Internet güvenli VPN aracılığıyla ya da özel bir bağlantı üzerinden mi?
* Genel bir IP adresi kullanılabilir toouse var mı?
* Toouse bir VPN cihazı planlıyor musunuz? Bu uyumlu bir VPN cihazı mı?
* Sadece bir kaç bilgisayarla mı bağlanıyorsunuz yoksa siteniz için kalıcı bir bağlantı istiyor musunuz?
* Ne tür bir VPN ağ geçidi gereklidir hello çözüm için toocreate istiyorsunuz?
* Hangi ağ geçidi SKU'su kullanmalısınız?

### <a name="planningtable"></a>Tablo planlama

Aşağıdaki tablonun hello hello çözümünüz için en iyi bağlantı seçeneğine karar vermenize yardımcı olabilir.

[!INCLUDE [vpn-gateway-cross-premises](../../includes/vpn-gateway-cross-premises-include.md)]

### <a name="gwsku"></a>Ağ Geçidi SKU'ları

[!INCLUDE [vpn-gateway-table-gwtype-aggtput](../../includes/vpn-gateway-table-gwtype-aggtput-include.md)]

### <a name="wf"></a>İş akışı

Merhaba aşağıdaki liste anahatları bulut bağlantı için genel iş akışı hello:

1. Tasarım ve tüm ağları için bağlantı topolojisi ve liste hello adres alanları planı tooconnect istiyor.
2. Bir Azure sanal ağı oluşturun. 
3. Merhaba sanal ağ için bir VPN ağ geçidi oluşturun.
4. Oluşturun ve bağlantıları tooon içi ağlarda veya diğer sanal (gerekirse) yapılandırın.
5. Oluşturun ve bir noktadan siteye bağlantı (gerektiğinde), Azure VPN ağ geçidi için yapılandırın.

## <a name="design"></a>Tasarım
### <a name="topologies"></a>Bağlantı topolojileri

Başlangıç hello hello diyagramlarda bakarak [VPN Gateway hakkında](vpn-gateway-about-vpngateways.md) makalesi. Merhaba makale temel diyagramları, hello dağıtım modellerinde her topoloji ve yapılandırmanızı toodeploy kullanabileceğiniz hello kullanılabilir dağıtım araçları içerir.

### <a name="designbasics"></a>Tasarım temelleri

Aşağıdaki bölümlerde hello hello VPN ağ geçidi temelleri tartışın. 

#### <a name="servicelimits"></a>Ağ Hizmetleri sınırları

Merhaba tabloları tooview arasında kaydırma [Ağ Hizmetleri sınırları](../azure-subscription-service-limits.md#networking-limits). listelenen hello sınırları tasarımınızı etkileyebilir.

#### <a name="subnets"></a>Alt ağlar hakkında

Bağlantıları oluştururken, alt ağ aralıklarını dikkate almanız gerekir. Alt ağ adres aralıklarını çakışan sahip olamaz. Çakışan bir alt ağla hello başka bir konuma hello aynı adres alanı içeren bir sanal ağ veya şirket içi konumunu içeren durumdur. Bu, ağ mühendisleri, yerel şirket içi ağlar toocarve, toouse için bir aralığı çıkışı için Azure IP için gereken alanı/alt adresleme anlamına gelir. Merhaba yerel şirket içi ağda kullanılmayan adres alanı gerekir.

VNet-VNet bağlantıları ile çalışırken çakışan alt ağlarınız önleme da önemlidir. Alt ağlarınızın çakışmayan bir IP adresi hello gönderme ve hedef sanal ağlar bulunuyorsa, VNet-VNet bağlantı başarısız. Merhaba hedef adres VNet gönderme hello parçası olduğundan azure diğer Vnet'in hello veri toohello yönlendiremezsiniz.

VPN ağ geçitleri bir ağ geçidi alt ağı olarak adlandırılan belirli bir alt gerektirir. Tüm ağ geçidi alt ağları GatewaySubnet toowork düzgün olarak adlandırılmalıdır. Mutlaka değil tooname farklı bir ağ geçidi alt ağınızı adlandırın ve Vm'leri veya herhangi bir şey başka toohello ağ geçidi alt ağı dağıtmazsınız. Bkz: [ağ geçidi alt ağları](vpn-gateway-about-vpn-gateway-settings.md#gwsub).

#### <a name="local"></a>Yerel ağ geçitleri hakkında

Merhaba yerel ağ geçidi genellikle tooyour içi konumunuz anlamına gelir. Merhaba Klasik dağıtım modelinde, başvurulan tooas bir yerel ağ Site hello yerel ağ geçididir. Bir yerel ağ geçidi yapılandırdığınızda hello hello şirket içi VPN cihazının genel IP adresini belirtin bir ad verin ve hello şirket içi konumdaysa hello adres öneklerini belirtirsiniz. Azure ağ trafiği için hello hedef adres öneklerine bakar, hello yerel ağ geçidi için belirttiğiniz hello yapılandırma bakar ve paketleri buna uygun şekilde yönlendirir. Merhaba adres öneklerini gerektiği gibi değiştirebilirsiniz. Daha fazla bilgi için bkz: [yerel ağ geçitleri](vpn-gateway-about-vpn-gateway-settings.md#lng).

#### <a name="gwtype"></a>Ağ geçidi türleri hakkında

Topolojiniz için Hello doğru ağ geçidi türünü seçme önemlidir. Merhaba yanlış tür seçerseniz, ağ geçidi düzgün çalışmaz. Merhaba ağ geçidinin nasıl bağlanır ve hello Resource Manager dağıtım modeli için gereken Yapılandırma ayarıdır Hello ağ geçidi türünü belirtir.

Merhaba ağ geçidi türleri şunlardır:

* VPN
* ExpressRoute

#### <a name="connectiontype"></a>Bağlantı türleri hakkında

Her bağlantı belirli bir bağlantı türü gerektirir. Merhaba bağlantı türleri şunlardır:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

#### <a name="vpntype"></a>VPN türleri hakkında

Her yapılandırma özel bir VPN türü gerektirir. Bir siteden siteye bağlantı ve noktadan siteye bağlantı toohello oluşturma gibi iki yapılandırmayı birleştiriyorsanız aynı sanal ağı, her iki bağlantı gereksinimini de karşılayan bir VPN türü kullanmalısınız.

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

tooeach bağlantı yapılandırması eşlemeleri gibi hello aşağıdaki tablolarda hello VPN türü gösterilmektedir. Emin hello toocreate istediğiniz ağ geçidi eşleşmeleri hello yapılandırmanız için VPN türü olun. 

[!INCLUDE [vpn-gateway-table-vpntype](../../includes/vpn-gateway-table-vpntype-include.md)]

### <a name="devices"></a>Siteden siteye bağlantıları için VPN cihazları

dağıtım modeli, bağımsız olarak tooconfigure bir Site siteye bağlantı aşağıdaki öğeleri hello gerekir:

* Azure VPN ağ geçitleri ile uyumlu bir VPN cihazı
* Bir genel kullanıma yönelik IPv4 IP adresi bir NAT'nin arkasında değildir

VPN Cihazınızı yapılandırmak toohave deneyimi ihtiyacınız veya birisi bu can sahip hello cihaz yapılandırdığınız.

[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

### <a name="forcedtunnel"></a>Zorlamalı tünel yönlendirme göz önünde bulundurun

Çoğu yapılandırmada zorlamalı tünel yapılandırabilirsiniz. Yeniden yönlendirme veya "tüm Internet'e bağlı trafik geri tooyour şirket içi konumu denetleme ve denetim için bir siteden siteye VPN tüneli aracılığıyla zorla" sağlar tünel zorlandı. Bu, çoğu kurumsal BT için kritik güvenlik gereksinimdir ilkeleri. 

Zorlamalı tünel olmadan, Internet'e bağlı trafik, vm'lerden azure'da her zaman toohello Internet hello seçeneği tooallow olmadan çıkışı doğrudan Azure ağ altyapısından, tooinspect ya da Denetim hello trafik dizinlere. Yetkisiz Internet erişimine olası tooinformation açığa çıkmasına veya diğer tür güvenlik ihlallerini yol açabilir.

Zorlamalı Tünel bağlantısı her iki dağıtım modeli ve farklı araçlar kullanılarak yapılandırılabilir. Daha fazla bilgi için bkz: [zorlamalı tüneli yapılandırma](vpn-gateway-forced-tunneling-rm.md).

**Zorlamalı tünel diyagramı**

![Azure VPN ağ geçidi zorlamalı tünel diyagramı](./media/vpn-gateway-plan-design/forced-tunneling-diagram.png)

## <a name="next-steps"></a>Sonraki adımlar

Merhaba bkz [VPN Gateway SSS](vpn-gateway-vpn-faq.md) ve [VPN Gateway hakkında](vpn-gateway-about-vpngateways.md) makaleler için daha fazla bilgi toohelp, tasarımınız ile.

Belirli ağ geçidi ayarları hakkında daha fazla bilgi için bkz: [hakkında VPN ağ geçidi ayarlarını](vpn-gateway-about-vpn-gateway-settings.md).