---
title: "IPSec tünelleri bir Azure VPN ağ geçidi tooreestablish sıfırlama | Microsoft Docs"
description: "Bu makalede, Azure VPN ağ geçidi tooreestablish IPSec tünelleri sıfırlama adımları anlatılmaktadır. Merhaba makale tooVPN ağ geçitleri hem hello Klasik hem de hello Resource Manager dağıtım modelleri için geçerlidir."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a>VPN Gateway’i sıfırlama

Bir veya daha fazla Siteden Siteye VPN tünelinde şirketler arası VPN bağlantısını kaybederseniz bir Azure VPN ağ geçidinin sıfırlanması yararlıdır. Bu durumda, şirket içi VPN cihazlarınızı tüm düzgün şekilde çalışıp çalışmadığını, ancak şu tooestablish hello Azure VPN ağ geçitleri ile IPSec tünelleri. Bu makalede, VPN ağ geçidinizi sıfırlamanıza yardımcı olur.

### <a name="what-happens-during-a-reset"></a>Sıfırlama sırasında ne olur?

Bir VPN ağ geçidi etkin bekleme yapılandırmasında çalışan iki VM örneğinden oluşur. Merhaba ağ geçidi sıfırladığınızda hello ağ geçidi yeniden başlatılır ve ardından yeniden uygular hello yapılandırmaları tooit şirketler arası. Merhaba ağ geçidi zaten sahip hello ortak IP adresini tutar. Bu, yeni bir ortak IP adresi ile tooupdate hello VPN yönlendirici yapılandırmasını Azure VPN ağ geçidi için gerekli olmadığı anlamına gelir.

Merhaba komutu tooreset hello ağ geçidi verdiğinizde, hello geçerli etkin örneği hello Azure VPN ağ geçidi hemen yeniden. Örnekten (yeniden başlatılan), hello etkin toohello bekleme örneğine hello yük devretme sırasında kısa bir boşluk olacaktır. Merhaba boşluk bir dakikadan az olmalıdır.

Merhaba bağlantı hello ilk yeniden başlatma sonrasında geri değil, sorunu hello aynı tooreboot hello ikinci VM örneği (Merhaba yeni etkin ağ geçidi) yeniden komutu. Merhaba iki yeniden başlatma istenen geri tooback varsa, olacaktır biraz daha uzun süre burada her iki VM örneğinin (etkin ve bekleme) yeniden başlatılıyor. Merhaba VPN bağlantısı, sanal makineleri toocomplete hello yeniden başlatmalar için too2 too4 dakika üzerinde bu uzun bir boşluğa neden olur.

Şirketler arası bağlantı sorunları yaşamaya devam ediyorsanız, iki yeniden başlatma sonrasında, Azure portal hello Lütfen bir destek isteği açın.

## <a name="before"></a>Başlamadan önce

Geçidinizi sıfırlamadan her IPSec-siteye (S2S) VPN tüneli için aşağıda listelenen hello anahtar öğeleri doğrulayın. Merhaba öğeleri öğelerdeki uyuşmazlık S2S VPN tünelleri hello bağlantıyı kes içinde neden olur. Doğrulama ve şirket içi ve Azure VPN ağ geçitleri için hello yapılandırmaları düzeltme gereksiz yeniden başlatmalardan kaydeder ve hello ağ geçitleri üzerinde çalışan diğer bağlantılar için kesinti hello.

Ağ geçidinizi sıfırlamadan önce aşağıdaki öğelerindeki hello doğrulayın:

* Hello Internet IP (VIP) için hem hello Azure VPN ağ geçidi adreslerini ve hello içi bağlı VPN ağ geçidi hem hello Azure ve hello şirket içi VPN ilkelerinde doğru şekilde yapılandırılır.
* Merhaba önceden paylaşılan anahtar gerekir olması hello hem Azure hem de şirket içi VPN ağ geçitlerinde aynı.
* Şifreleme algoritmaları ve PSF (kusursuz iletme gizliliği), karma, her ikisi de Azure hello ve şirket içi VPN ağ geçitleri sahip hello emin olun gibi belirli IPSec/IKE yapılandırmalarını uygularsanız aynı yapılandırmaları.

## <a name="portal"></a>Azure portalı

Hello Azure portal kullanarak bir Resource Manager VPN ağ geçidi sıfırlayabilirsiniz. Merhaba tooreset klasik bir ağ geçidi istiyorsanız bkz [PowerShell](#resetclassic) adımları.

### <a name="resource-manager-deployment-model"></a>Resource Manager dağıtım modeli

1. Açık hello [Azure portal](https://portal.azure.com) ve tooreset istediğiniz toohello Resource Manager sanal ağ geçidi gidin.
2. Merhaba dikey penceresinde hello sanal ağ geçidi, 'Sıfırla' yı tıklatın.

  ![VPN ağ geçidi dikey Sıfırla](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. Merhaba sıfırlama dikey penceresinde, hello tıklatın **sıfırlama** düğmesi.

## <a name="ps"></a>PowerShell

### <a name="resource-manager-deployment-model"></a>Resource Manager dağıtım modeli

bir ağ geçidi sıfırlama için cmdlet hello **sıfırlama AzureRmVirtualNetworkGateway**. Sıfırlama gerçekleştirmeden önce en son sürümünü hello hello olduğundan emin olun [Resource Manager PowerShell cmdlet'leri](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0). Merhaba aşağıdaki örnek hello TestRG1 kaynak grubunda VNet1GW adlı bir sanal ağ geçidi sıfırlar:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

Sonuç:

Dönüş sonucu aldığınızda, hello ağ geçidi sıfırlama başarılı varsayabilirsiniz. Ancak, hiçbir şey yoktur açıkça o hello sıfırlama başarıyla tamamlandığını belirten hello dönüş sonuçlanır. Merhaba geçmişi toosee en yakından toolook istiyorsanız tam olarak hello ağ geçidi sıfırlandığında oluştu, hello bu bilgileri görüntüleyebilir [Azure portal](https://portal.azure.com). Merhaba Portalı'nda çok gidin**'GatewayName' -> kaynak durumu**.

### <a name="resetclassic"></a>Klasik dağıtım modeli

bir ağ geçidi sıfırlama için cmdlet hello **Reset-AzureVNetGateway**. Sıfırlama gerçekleştirmeden önce en son sürümünü hello hello olduğundan emin olun [Hizmet Yönetimi (SM) PowerShell cmdlet'lerini](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0). Merhaba aşağıdaki örnekte "ContosoVNet" adlı bir sanal ağ için ağ geçidi hello sıfırlar:

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

Sonuç:

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <a name="cli"></a>Azure CLI

tooreset hello ağ geçidi, kullanım hello [az ağ vnet-gateway sıfırlama](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) komutu. Merhaba aşağıdaki örnek vnet5gw'un hello TestRG5 kaynak grubunda adlı bir sanal ağ geçidi sıfırlar:

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

Sonuç:

Dönüş sonucu aldığınızda, hello ağ geçidi sıfırlama başarılı varsayabilirsiniz. Ancak, hiçbir şey yoktur açıkça o hello sıfırlama başarıyla tamamlandığını belirten hello dönüş sonuçlanır. Merhaba geçmişi toosee en yakından toolook istiyorsanız tam olarak hello ağ geçidi sıfırlandığında oluştu, hello bu bilgileri görüntüleyebilir [Azure portal](https://portal.azure.com). Merhaba Portalı'nda çok gidin**'GatewayName' -> kaynak durumu**.
