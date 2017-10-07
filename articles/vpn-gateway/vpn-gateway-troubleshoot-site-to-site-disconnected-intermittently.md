---
title: "Azure siteden siteye VPN bağlantısını keser aralıklı aaaTroubleshoot | Microsoft Docs"
description: "Nasıl tootroubleshoot hello düzenli olarak bağlantısı kesilmiş hangi hello siteden siteye VPN bağlantısı sorun hakkında bilgi edinin."
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a>Sorun giderme: Azure siteden siteye VPN aralıklı keser

Yeni veya var olan bir Microsoft Azure noktadan siteye VPN bağlantısı kararlı değilse veya düzenli olarak keser hello sorunla karşılaşabilirsiniz. Bu makalede, sorun giderme adımları toohelp tanımlamak ve hello hello sorunun nedenini çözümleyin sağlanmaktadır. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Sorun giderme adımları

### <a name="prerequisite-step"></a>Önkoşul adım

Azure sanal ağ geçidi Hello türünü kontrol edin:

1. Çok Git[Azure portal](https://portal.azure.com).
2. Merhaba denetleyin **genel bakış** hello sanal ağ geçidi hello türü bilgi sayfası.
    
    ![Merhaba ağ geçidi Hello genel bakış](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>Merhaba VPN cihazı doğrulanır içi olup olmadığını 1 onay adım

1. Kullanmakta olduğunuz olup olmadığını denetleyin bir [VPN cihazı ve işletim sistemi sürümü doğrulandı](vpn-gateway-about-vpn-devices.md#devicetable). Merhaba VPN cihazı doğrulanmaz, herhangi bir uyumluluk sorunu varsa toocontact hello aygıt üreticisi toosee olabilir.
2. Bu hello VPN cihazı doğru yapılandırıldığından emin olun. Daha fazla bilgi için bkz: [cihaz yapılandırma örneklerini düzenleme](vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a>2. adım onay hello güvenlik ilişkisi ayarlarını (ilke tabanlı Azure sanal ağ geçitleri)

1. Bu hello sanal ağ, alt ağları ve, aralıkları hello emin olun **yerel ağ geçidi** Microsoft Azure tanımında hello şirket içi VPN cihazı hello yapılandırmasına aynı.
2. Merhaba güvenlik ilişkisi ayarları eşleşen doğrulayın.

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a>Ağ geçidi alt ağı üzerinde kullanıcı tanımlı yollar veya ağ güvenlik grupları için 3. adım denetimi

Bir kullanıcı tarafından tanımlanan rota hello ağ geçidi alt ağı üzerinde bazı trafiği kısıtlama ve diğer trafiğe izin. Bu hello VPN bağlantısı güvenilir olmayan bir miktar trafik için ve başkaları için iyi görünmesini sağlar. 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a>Adım 4 onay "bir VPN tüneli alt ağ çifti başına" Merhaba (ilke tabanlı sanal ağ geçitleri için) ayarlama

Bu hello şirket içi VPN cihazı toohave ayarlanmış olduğundan emin olun **alt ağ çifti başına bir VPN tüneli** ilke tabanlı sanal ağ geçitleri için.

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a>Adım 5 (için ilke tabanlı sanal ağ geçitleri) güvenlik ilişkisi sınırlaması denetle

Merhaba ilke tabanlı sanal ağ geçidi 200 alt ağ güvenlik ilişkisi çiftleri sınırı vardır. Azure sanal ağ alt ağları Hello sayısının kez çarpımı varsa hello tarafından yerel alt ağları sayısı 200'den büyükse, kesme durumlarıyla alt bakın.

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a>Adım 6 onay içi VPN cihazı dış arabirimi adresi

- Merhaba, IP adresi hello VPN aygıtının Internet'e hello dahil **yerel ağ geçidi** tanımı Azure'da, kullanımın bağlantısının kesilmesi karşılaşabilirsiniz.
- Merhaba cihazın dış arabirimi hello üzerinde doğrudan Internet olmalıdır. Hiçbir ağ adresi çevirisi (NAT) veya güvenlik duvarı hello Internet ve hello aygıt arasında olmalıdır.
-  Bir sanal IP Güvenlik Duvarı kümeleme toohave yapılandırırsanız, hello küme bölme ve ağ geçidi hello tooa ortak arabirimi ile arabirim doğrudan hello VPN Gereci kullanıma sunar.

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a>Merhaba içi bağlı VPN cihazı kusursuz iletme etkin gizliliği sahip olup olmadığını 7 onay adım

Merhaba **kusursuz iletme gizliliği** özelliği hello bağlantı kesme sorunlara neden olabilir. Merhaba VPN cihazı varsa **kusursuz iletme gizliliği** hello özelliği etkinse, devre dışı bırakın. Ardından [hello sanal ağ geçidi IPSec ilkesi güncelleştirmesi](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).

## <a name="next-steps"></a>Sonraki adımlar

- [Siteden siteye bağlantı tooa sanal ağ yapılandırma](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [Siteden siteye VPN bağlantıları için IPSec/IKE ilkesi yapılandırma](vpn-gateway-ipsecikepolicy-rm-powershell.md)

