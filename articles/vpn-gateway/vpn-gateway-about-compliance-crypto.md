---
title: "aaaAbout şifreleme gereksinimleri ve Azure VPN ağ geçitleri | Microsoft Docs"
description: "Bu makalede, şifreleme gereksinimleri ve Azure VPN ağ geçitleri açıklanmaktadır"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/22/2017
ms.author: yushwang
ms.openlocfilehash: af5f14d66beeea5316218f9788c4ad7876826162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a>Şifreleme gereksinimleri ve Azure VPN ağ geçitleri hakkında

Bu makalede, Azure VPN ağ geçitleri toosatisfy şifreleme gereksinimlerinizi hem şirket içi S2S VPN tünelleri, hem de VNet-VNet bağlantıları Azure içinde nasıl yapılandırabileceğiniz anlatılmaktadır. 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a>IPSec ve IKE İlkesi parametreleri hakkında Azure VPN ağ geçitleri için
IPSec ve IKE protokolü standart çeşitli bileşimlerde çok çeşitli şifreleme algoritmalarını destekler. Müşteriler, şifreleme algoritmaları ve parametreleri belirli bir bileşimini isteme, Azure VPN ağ geçitleri varsayılan teklifleri kümesi kullanın. Merhaba varsayılan ilkeyi ayarlar çeşitli üçüncü taraf VPN aygıtları ile toomaximize birlikte çalışabilirlik varsayılan yapılandırması seçilmiştir. Sonuç olarak, hello ilkeleri ve tekliflerini hello sayısı kullanılabilir şifreleme algoritmaları ve anahtar gücü tüm olası birleşimlerini ele olamaz.

Varsayılan ilke Azure VPN ağ geçidi hello belgesinde listelenen için kümesi Hello: [VPN cihazları hakkında ve siteden siteye VPN Gateway bağlantıları için IPSec/IKE parametreleri](vpn-gateway-about-vpn-devices.md).

## <a name="cryptographic-requirements"></a>Şifreleme gereksinimleri
Belirli şifreleme algoritmalarının veya parametreler gerektiren iletişimleri için genellikle toocompliance veya güvenlik gereksinimleri, müşteriler artık kendi Azure VPN ağ geçitleri toouse özel bir IPSec/IKE ilke özel şifreleme ile yapılandırabilirsiniz algoritmaları ve anahtar gücü yerine hello Azure varsayılan ilkeyi ayarlar.

Örneğin, müşteriler Grup 14 (2048 bit), Grup 24 (2048 bit MODP grup) ya da ECP (Eliptik gibi IKE kullanılan toospecify daha güçlü grupları toobe gerekebilir ancak hello Ikev2 ana mod ilkelerini Azure VPN ağ geçitleri için Diffie-Hellman grubu 2 (1024 bit), yalnızca kullanma Eğri grupları) 256 veya 384 bit (sırasıyla 19 ve Grup 20, Grup). Benzer gereksinimleri tooIPsec hızlı mod ilkelerini de geçerlidir.

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a>Azure VPN ağ geçitleri ile özel IPSec/IKE İlkesi
Azure VPN ağ geçitleri artık bağlantı başına, özel IPSec/IKE ilke destekler. Siteden siteye veya VNet-VNet bağlantısı için şifreleme algoritmaları belirli bir bileşimini IPSec ve IKE için istenen hello anahtar gücü ile hello aşağıdaki örnekte gösterildiği gibi seçebilirsiniz:

![IPSec IKE İlkesi](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

Bir IPSec/IKE ilkesi oluşturun ve tooa yeni veya var olan bağlantı uygulayın. 

### <a name="workflow"></a>İş akışı

1. Diğer nasıl toodocuments açıklandığı gibi Hello sanal ağlar, VPN ağ geçitleri veya yerel ağ geçitleri bağlanabilirlik topolojiniz için oluşturun
2. Bir IPSec/IKE ilkesi oluşturun
3. S2S veya VNet-VNet bağlantısı oluşturduğunuzda hello ilkesi uygulayabilir.
4. Merhaba bağlantıyı zaten oluşturduysanız, uygulama veya hello İlkesi tooan var olan bağlantıyı güncelleştir


## <a name="ipsecike-policy-faq"></a>IPSec/IKE İlkesi hakkında SSS

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a>Sonraki adımlar
Bkz: [IPSec/IKE yapılandırma İlkesi](vpn-gateway-ipsecikepolicy-rm-powershell.md) bir bağlantıda özel IPSec/IKE ilkesini yapılandırma hakkında adım adım yönergeler için.

Ayrıca bkz. [birden çok ilke tabanlı VPN aygıtlarını bağlamak](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn hello UsePolicyBasedTrafficSelectors seçeneği hakkında daha fazla bilgi.
