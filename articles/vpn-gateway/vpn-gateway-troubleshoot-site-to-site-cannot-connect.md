---
title: "aaaTroubleshoot bağlanamıyor bir Azure siteden siteye VPN bağlantısı | Microsoft Docs"
description: "Bilgi nasıl tootroubleshoot bir siteden siteye VPN bağlantısı aniden çalışmayı durduruyor ve bağlanılamaz."
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a>Sorun giderme: Bir Azure siteden siteye VPN bağlantısı bağlanamıyor ve çalışmayı durduruyor

Bir şirket içi ağınız ve Azure sanal ağı arasında siteden siteye VPN bağlantısı yapılandırdıktan sonra hello VPN bağlantısı aniden çalışmayı durdurur ve yeniden bağlanılamaz. Bu makalede, sorun giderme adımları toohelp sağlanmaktadır. Bu sorunu çözün. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>Sorun giderme adımları

tooresolve hello sorun, ilk çok deneyin[sıfırlama hello Azure VPN ağ geçidi](vpn-gateway-resetgw-classic.md) ve hello tünel hello şirket içi VPN aygıttan sıfırlayın. Merhaba sorun devam ederse, bu adımları tooidentify hello neden hello sorununun izleyin.

### <a name="prerequisite-step"></a>Önkoşul adım

Merhaba hello Azure VPN ağ geçidi türünü kontrol edin.

1. Toohello Git [Azure portal](https://portal.azure.com).

2. Merhaba denetleyin **genel bakış** hello VPN ağ geçidi hello türü bilgi sayfası.
    
    ![Merhaba ağ geçidi'ne genel bakış](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>1. Adım Merhaba şirket içi VPN cihazı doğrulanıp doğrulanmadığını denetleyin

1. Kullanmakta olduğunuz olup olmadığını denetleyin bir [VPN cihazı ve işletim sistemi sürümü doğrulandı](vpn-gateway-about-vpn-devices.md#devicetable). Merhaba cihaz doğrulanan VPN cihazı değilse, bir uyumluluk sorunu varsa toocontact hello aygıt üreticisi toosee olabilir.

2. Bu hello VPN cihazı doğru yapılandırıldığından emin olun. Daha fazla bilgi için bkz: [cihaz yapılandırma örneklerini düzenleme](/vpn-gateway-about-vpn-devices.md#editing).

### <a name="step-2-verify-hello-shared-key"></a>2. Adım Merhaba paylaşılan anahtar doğrulayın

Merhaba şirket içi VPN aygıtının toohello Azure sanal ağ VPN toomake hello anahtarların eşleştiğinden emin için paylaşılan anahtar Hello karşılaştırın. 

tooview hello hello Azure VPN bağlantısı için paylaşılan anahtar yöntemleri aşağıdaki hello birini kullanın:

**Azure portal**

1. Oluşturduğunuz toohello VPN ağ geçidi siteden siteye bağlantı gidin.

2. Merhaba, **ayarları** 'yi tıklatın **paylaşılan anahtarı**.
    
    ![Paylaşılan anahtar](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

**Azure PowerShell**

Hello Azure Resource Manager dağıtım modeli için:

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

Merhaba Klasik dağıtım modeli için:

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a>3. Adım Merhaba VPN eş IP doğrulayın

-   Merhaba hello IP tanımında **yerel ağ geçidi** Azure nesnesinde hello şirket içi cihaz IP eşleşmelidir.
-   Merhaba hello üzerinde ayarlanır Azure ağ geçidi IP tanımı aygıt hello Azure ağ geçidi IP eşleşmelidir şirket içi.

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a>4. Adım. UDR ve Nsg'ler hello ağ geçidi alt ağda denetleyin

Denetleyin ve kullanıcı tanımlı yönlendirme (UDR) veya ağ güvenlik grupları (Nsg'ler) hello ağ geçidi alt ağda kaldırın ve sonra hello sonucunu sınayın. Merhaba sorun çözülmüşse UDR veya NSG uygulanan hello ayarlarını doğrulayın.

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a>5. Adım. Merhaba şirket içi VPN cihazı dış arabirimi adresi denetleyin

- Merhaba hello VPN cihazının Internet'e yönelik IP adresi hello eklenirse **yerel ağ** tanımı Azure'da, kullanımın bağlantısının kesilmesi karşılaşabilirsiniz.
- Merhaba cihazın dış arabirimi hello üzerinde doğrudan Internet olmalıdır. Hiçbir ağ adresi çevirisi veya güvenlik duvarı hello Internet ve hello aygıt arasında olmalıdır.
- tooconfigure kümeleme toohave sanal bir IP Güvenlik Duvarı, hello küme bölün ve tooa ortak arabirimi ile bu hello Ağ Geçidi Arabirimi doğrudan hello VPN Gereci kullanıma sunma.

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a>6. Adım. Merhaba alt tam olarak eşleştiğinden emin olun (Azure ilke tabanlı ağ geçitleri)

-   Merhaba alt hello Azure sanal ağı ve şirket içi tanımlarında hello Azure sanal ağı arasında tam olarak eşleştiğini doğrulayın.
-   Merhaba alt hello arasında tam olarak eşleştiğinden emin olun **yerel ağ geçidi** ve şirket içi hello şirket içi ağ için tanımlar.

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a>7. Adım. Hello Azure ağ geçidi durumu araştırması doğrulayın

1. Toohello Git [durumu araştırması](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).

2. Merhaba Sertifika uyarısı aracılığıyla'ı tıklatın.
3. Bir yanıtı alırsanız, hello VPN ağ geçidi sağlıklı olarak kabul edilir. Bir yanıt almazsanız, hello ağ geçidi sağlıklı olmayabilir veya hello ağ geçidi alt ağı üzerinde bir NSG hello soruna neden oluyor. Merhaba metin aşağıdaki örnek yanıt şöyledir:

    &lt;? xml version = "1.0"? > <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">birincil örneği: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6 < / dize&gt;

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a>8. adım. Merhaba VPN cihazı hello kusursuz iletme gizliliği özelliğinin etkin olduğu şirket içi olup olmadığını denetleyin

Merhaba kusursuz iletme gizliliği özelliği, bağlantı kesme sorunlara neden olabilir. Merhaba VPN cihazı etkin kusursuz iletme gizliliği varsa hello özelliği devre dışı bırakın. Ardından hello VPN ağ geçidi IPSec ilkesi güncelleştirin.

## <a name="next-steps"></a>Sonraki adımlar

-   [Siteden siteye bağlantı tooa sanal ağ yapılandırma](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [Siteden siteye VPN bağlantıları için bir IPSec/IKE ilkesi yapılandırma](vpn-gateway-ipsecikepolicy-rm-powershell.md)
