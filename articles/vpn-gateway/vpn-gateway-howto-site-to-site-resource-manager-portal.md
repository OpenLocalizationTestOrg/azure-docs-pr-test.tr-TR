---
title: "Şirket içi ağ tooan Azure sanal ağı bağlanın: siteden siteye VPN: portalı | Microsoft Docs"
description: "Şirket içi bir IPSec bağlantısı üzerinden tooan Azure sanal ağı ağ adımları toocreate genel Internet hello. Bu adımları hello portal kullanarak şirket içi siteden siteye VPN ağ geçidi bağlantı oluşturmanıza yardımcı olur."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 6f0acbaf1bf016026cefade048a116e94686103d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-site-to-site-connection-in-hello-azure-portal"></a>Hello Azure portalında bir siteden siteye bağlantı oluşturma

Bu makale size nasıl toouse hello Azure portal toocreate, şirket içi ağ toohello VNet bir siteden siteye VPN ağ geçidi bağlantısını gösterir. Bu makaledeki adımları Hello toohello Resource Manager dağıtım modeli uygulayın. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure portal (klasik)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>

Kullanılan tooconnect bir siteden siteye VPN gateway bağlantısı olan bir IPSec/IKE (Ikev1 veya Ikev2) VPN tüneli üzerinden tooan Azure sanal ağı şirket içi ağ. Bağlantı bu tür bir VPN cihazı bulunan dışarıya dönük bir genel IP adresi atanmış tooit olan şirket içi gerektirir. VPN ağ geçitleri hakkında daha fazla bilgi için bkz. [VPN ağ geçidi hakkında](vpn-gateway-about-vpngateways.md).

![Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı diyagramı](./media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

## <a name="before-you-begin"></a>Başlamadan önce

Ölçüt yapılandırmanıza başlamadan önce aşağıdaki hello karşıladığınızı doğrulayın:

* Uyumlu bir VPN cihazı ve mümkün tooconfigure olan birisi olduğundan emin olun. Uyumlu VPN cihazları ve cihaz yapılandırması hakkında daha fazla bilgi için bkz.[VPN Cihazları Hakkında](vpn-gateway-about-vpn-devices.md).
* VPN cihazınız için dışarıya dönük genel bir IPv4 adresi olduğunu doğrulayın. Bu IP adresi bir NAT’nin arkasında olamaz.
* Bulunan hello IP adresi aralıklarıyla ilgili bilginiz yoksa, şirket içi ağ, bu ayrıntıları sizin için sağlayabilecek biriyle toocoordinate gerekir. Bu yapılandırma oluşturduğunuzda, Azure tooyour şirket içi konumu yönlendirilecek hello IP adresi aralığı önekleri belirtmeniz gerekir. Şirket içi ağınıza hello ağların hiçbiri diz tooconnect için istediğiniz hello sanal ağ alt ağı üzerinden olabilir. 

### <a name="values"></a>Örnek değerler

Bu makaledeki örneklerde Hello değerleri aşağıdaki hello kullanın. Bu değerleri toocreate bir test ortamı kullanın veya toothem başvurun toobetter anlamak bu makaledeki hello örnekler.

* **VNet Name:** TestVNet1
* **Adres Alanı:** 
  * 10.11.0.0/16
  * 10.12.0.0/16 (bu alıştırma için isteğe bağlı)
* **Alt ağlar:**
  * FrontEnd: 10.11.0.0/24
  * BackEnd: 10.12.0.0/24 (bu alıştırma için isteğe bağlı)
* **GatewaySubnet:** 10.11.255.0/27
* **Kaynak Grubu:** TestRG1
* **Konum:** Doğu ABD
* **DNS Sunucusu:** İsteğe bağlıdır. Merhaba, DNS sunucunuzun IP adresi.
* **Sanal Ağ Geçidi Adı: VNet1GW**
* **Genel IP:** VNet1GWIP
* **VPN Türü:** Yol tabanlı
* **Bağlantı Türü:** Siteden siteye (IPsec)
* **Ağ Geçidi Türü:** VPN
* **Yerel Ağ Geçidi Adı:** Site2
* **Bağlantı Adı:** VNet1toSite2

## <a name="CreatVNet"></a>1. Sanal ağ oluşturma

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a>2. DNS sunucusu belirleme

DNS gerekli toocreate bir Site siteye bağlantı değil. Ancak, dağıtılan tooyour sanal ağ için kaynaklar toohave ad çözümlemesi istiyorsanız, bir DNS sunucusunu belirtmeniz gerekir. Bu ayar hello DNS sunucusu, bu sanal ağ için ad çözümlemesi için toouse istediğinizi belirtmenize olanak sağlar. Bir DNS sunucusu oluşturmaz. Ad çözümlemesi hakkında daha fazla bilgi için bkz. [VM'ler ve rol örnekleri için Ad Çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a>3. Merhaba ağ geçidi alt ağı oluşturun

[!INCLUDE [vpn-gateway-aboutgwsubnet](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a>4. Merhaba VPN ağ geçidi oluşturma

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a>5. Merhaba yerel ağ geçidi oluşturma

Merhaba yerel ağ geçidi genellikle tooyour içi konumunuz anlamına gelir. Merhaba site olarak Azure tooit bakın, sonra kullanabilirsiniz hello IP adresi belirtin bir ad verin hello şirket içi VPN aygıtının toowhich bir bağlantı oluşturur. Ayrıca, hello VPN ağ geçidi toohello VPN cihazı yönlendirilecek hello IP adresi öneklerini belirtin. Belirttiğiniz hello adres öneklerini hello öneklerini şirket içi ağınızda yer alan var. Şirket içi ağ değişikliklerinizi veya toochange hello genel IP adresi hello VPN cihazı için gerekiyorsa, hello değerleri daha sonra kolayca güncelleştirebilirsiniz.

[!INCLUDE [Add local network gateway](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a>6. VPN cihazınızı yapılandırma

Siteden siteye bağlantıları tooan şirket içi ağ bir VPN cihazı gerektirir. Bu adımda VPN cihazınızı yapılandıracaksınız. VPN Cihazınızı yapılandırırken hello aşağıdaki gerekir:

- Paylaşılan bir anahtar. Bu olduğu hello aynı paylaşılan siteden siteye VPN bağlantınızı oluştururken belirttiğiniz anahtarı. Bu örneklerde temel bir paylaşılan anahtar kullanılır. Daha karmaşık bir anahtar toouse oluşturmak öneririz.
- Merhaba sanal ağ geçidinizin genel IP adresi. Hello Azure portal, PowerShell veya CLI kullanarak hello ortak IP adresini görüntüleyebilirsiniz. toofind hello hello Azure portal kullanarak VPN ağ geçidinizin genel IP adresi gidin çok**sanal ağ geçitleri**, ağ geçidiniz hello adını tıklatın.

[!INCLUDE [Configure a VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a>7. Merhaba VPN bağlantısı oluşturun

Sanal ağ geçidiniz ve şirket içi VPN aygıtınızın arasında Hello siteden siteye VPN bağlantısı oluşturun.

[!INCLUDE [Add connections](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a>8. Merhaba VPN bağlantısını doğrulama

[!INCLUDE [Verify - Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="connectVM"></a>tooconnect tooa sanal makine

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="reset"></a>Nasıl tooreset bir VPN ağ geçidi

Bir veya daha fazla Siteden Siteye VPN tünelinde şirketler arası VPN bağlantısını kaybederseniz bir Azure VPN ağ geçidinin sıfırlanması yararlıdır. Bu durumda, şirket içi VPN cihazlarınızı tüm düzgün şekilde çalışıp çalışmadığını, ancak şu tooestablish hello Azure VPN ağ geçitleri ile IPSec tünelleri. Adımlar için bkz. [VPN ağ geçidini sıfırlama](vpn-gateway-resetgw-classic.md).

## <a name="resize"></a>Nasıl toochange bir ağ geçidi SKU'su (boyutlandırma bir ağ geçidi)

Merhaba, bir ağ geçidi SKU'su toochange adımları için bkz: [ağ geçidi SKU'ları](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

## <a name="next-steps"></a>Sonraki adımlar

* BGP hakkında daha fazla bilgi için bkz: Merhaba [BGP genel bakış](vpn-gateway-bgp-overview.md) ve [nasıl tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Zorlamalı Tünel Oluşturma hakkında bilgi için bkz. [Zorlamalı Tünel Oluşturma Hakkında](vpn-gateway-forced-tunneling-rm.md).
* Yüksek Oranda Kullanılabilir Etkin-Etkin bağlantılar hakkında bilgi için bkz. [Yüksek Oranda Kullanılabilir Şirket İçi ve Dışı ile Sanal Ağdan Sanal Ağa Bağlantı](vpn-gateway-highlyavailable.md).
