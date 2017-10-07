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
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="b675e-104">VPN Gateway’i sıfırlama</span><span class="sxs-lookup"><span data-stu-id="b675e-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="b675e-105">Bir veya daha fazla Siteden Siteye VPN tünelinde şirketler arası VPN bağlantısını kaybederseniz bir Azure VPN ağ geçidinin sıfırlanması yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="b675e-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="b675e-106">Bu durumda, şirket içi VPN cihazlarınızı tüm düzgün şekilde çalışıp çalışmadığını, ancak şu tooestablish hello Azure VPN ağ geçitleri ile IPSec tünelleri.</span><span class="sxs-lookup"><span data-stu-id="b675e-106">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="b675e-107">Bu makalede, VPN ağ geçidinizi sıfırlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b675e-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="b675e-108">Sıfırlama sırasında ne olur?</span><span class="sxs-lookup"><span data-stu-id="b675e-108">What happens during a reset?</span></span>

<span data-ttu-id="b675e-109">Bir VPN ağ geçidi etkin bekleme yapılandırmasında çalışan iki VM örneğinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="b675e-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="b675e-110">Merhaba ağ geçidi sıfırladığınızda hello ağ geçidi yeniden başlatılır ve ardından yeniden uygular hello yapılandırmaları tooit şirketler arası.</span><span class="sxs-lookup"><span data-stu-id="b675e-110">When you reset hello gateway, it reboots hello gateway, and then reapplies hello cross-premises configurations tooit.</span></span> <span data-ttu-id="b675e-111">Merhaba ağ geçidi zaten sahip hello ortak IP adresini tutar.</span><span class="sxs-lookup"><span data-stu-id="b675e-111">hello gateway keeps hello public IP address it already has.</span></span> <span data-ttu-id="b675e-112">Bu, yeni bir ortak IP adresi ile tooupdate hello VPN yönlendirici yapılandırmasını Azure VPN ağ geçidi için gerekli olmadığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b675e-112">This means you won’t need tooupdate hello VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="b675e-113">Merhaba komutu tooreset hello ağ geçidi verdiğinizde, hello geçerli etkin örneği hello Azure VPN ağ geçidi hemen yeniden.</span><span class="sxs-lookup"><span data-stu-id="b675e-113">When you issue hello command tooreset hello gateway, hello current active instance of hello Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="b675e-114">Örnekten (yeniden başlatılan), hello etkin toohello bekleme örneğine hello yük devretme sırasında kısa bir boşluk olacaktır.</span><span class="sxs-lookup"><span data-stu-id="b675e-114">There will be a brief gap during hello failover from hello active instance (being rebooted), toohello standby instance.</span></span> <span data-ttu-id="b675e-115">Merhaba boşluk bir dakikadan az olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b675e-115">hello gap should be less than one minute.</span></span>

<span data-ttu-id="b675e-116">Merhaba bağlantı hello ilk yeniden başlatma sonrasında geri değil, sorunu hello aynı tooreboot hello ikinci VM örneği (Merhaba yeni etkin ağ geçidi) yeniden komutu.</span><span class="sxs-lookup"><span data-stu-id="b675e-116">If hello connection is not restored after hello first reboot, issue hello same command again tooreboot hello second VM instance (hello new active gateway).</span></span> <span data-ttu-id="b675e-117">Merhaba iki yeniden başlatma istenen geri tooback varsa, olacaktır biraz daha uzun süre burada her iki VM örneğinin (etkin ve bekleme) yeniden başlatılıyor.</span><span class="sxs-lookup"><span data-stu-id="b675e-117">If hello two reboots are requested back tooback, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="b675e-118">Merhaba VPN bağlantısı, sanal makineleri toocomplete hello yeniden başlatmalar için too2 too4 dakika üzerinde bu uzun bir boşluğa neden olur.</span><span class="sxs-lookup"><span data-stu-id="b675e-118">This will cause a longer gap on hello VPN connectivity, up too2 too4 minutes for VMs toocomplete hello reboots.</span></span>

<span data-ttu-id="b675e-119">Şirketler arası bağlantı sorunları yaşamaya devam ediyorsanız, iki yeniden başlatma sonrasında, Azure portal hello Lütfen bir destek isteği açın.</span><span class="sxs-lookup"><span data-stu-id="b675e-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from hello Azure portal.</span></span>

## <span data-ttu-id="b675e-120"><a name="before"></a>Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b675e-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="b675e-121">Geçidinizi sıfırlamadan her IPSec-siteye (S2S) VPN tüneli için aşağıda listelenen hello anahtar öğeleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b675e-121">Before you reset your gateway, verify hello key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="b675e-122">Merhaba öğeleri öğelerdeki uyuşmazlık S2S VPN tünelleri hello bağlantıyı kes içinde neden olur.</span><span class="sxs-lookup"><span data-stu-id="b675e-122">Any mismatch in hello items will result in hello disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="b675e-123">Doğrulama ve şirket içi ve Azure VPN ağ geçitleri için hello yapılandırmaları düzeltme gereksiz yeniden başlatmalardan kaydeder ve hello ağ geçitleri üzerinde çalışan diğer bağlantılar için kesinti hello.</span><span class="sxs-lookup"><span data-stu-id="b675e-123">Verifying and correcting hello configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for hello other working connections on hello gateways.</span></span>

<span data-ttu-id="b675e-124">Ağ geçidinizi sıfırlamadan önce aşağıdaki öğelerindeki hello doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="b675e-124">Verify hello following items before resetting your gateway:</span></span>

* <span data-ttu-id="b675e-125">Hello Internet IP (VIP) için hem hello Azure VPN ağ geçidi adreslerini ve hello içi bağlı VPN ağ geçidi hem hello Azure ve hello şirket içi VPN ilkelerinde doğru şekilde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="b675e-125">hello Internet IP addresses (VIPs) for both hello Azure VPN gateway and hello on-premises VPN gateway are configured correctly in both hello Azure and hello on-premises VPN policies.</span></span>
* <span data-ttu-id="b675e-126">Merhaba önceden paylaşılan anahtar gerekir olması hello hem Azure hem de şirket içi VPN ağ geçitlerinde aynı.</span><span class="sxs-lookup"><span data-stu-id="b675e-126">hello pre-shared key must be hello same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="b675e-127">Şifreleme algoritmaları ve PSF (kusursuz iletme gizliliği), karma, her ikisi de Azure hello ve şirket içi VPN ağ geçitleri sahip hello emin olun gibi belirli IPSec/IKE yapılandırmalarını uygularsanız aynı yapılandırmaları.</span><span class="sxs-lookup"><span data-stu-id="b675e-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both hello Azure and on-premises VPN gateways have hello same configurations.</span></span>

## <span data-ttu-id="b675e-128"><a name="portal"></a>Azure portalı</span><span class="sxs-lookup"><span data-stu-id="b675e-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="b675e-129">Hello Azure portal kullanarak bir Resource Manager VPN ağ geçidi sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b675e-129">You can reset a Resource Manager VPN gateway using hello Azure portal.</span></span> <span data-ttu-id="b675e-130">Merhaba tooreset klasik bir ağ geçidi istiyorsanız bkz [PowerShell](#resetclassic) adımları.</span><span class="sxs-lookup"><span data-stu-id="b675e-130">If you want tooreset a classic gateway, see hello [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="b675e-131">Resource Manager dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="b675e-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="b675e-132">Açık hello [Azure portal](https://portal.azure.com) ve tooreset istediğiniz toohello Resource Manager sanal ağ geçidi gidin.</span><span class="sxs-lookup"><span data-stu-id="b675e-132">Open hello [Azure portal](https://portal.azure.com) and navigate toohello Resource Manager virtual network gateway that you want tooreset.</span></span>
2. <span data-ttu-id="b675e-133">Merhaba dikey penceresinde hello sanal ağ geçidi, 'Sıfırla' yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b675e-133">On hello blade for hello virtual network gateway, click 'Reset'.</span></span>

  ![VPN ağ geçidi dikey Sıfırla](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="b675e-135">Merhaba sıfırlama dikey penceresinde, hello tıklatın **sıfırlama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="b675e-135">On hello Reset blade, click hello **Reset** button.</span></span>

## <span data-ttu-id="b675e-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="b675e-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="b675e-137">Resource Manager dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="b675e-137">Resource Manager deployment model</span></span>

<span data-ttu-id="b675e-138">bir ağ geçidi sıfırlama için cmdlet hello **sıfırlama AzureRmVirtualNetworkGateway**.</span><span class="sxs-lookup"><span data-stu-id="b675e-138">hello cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="b675e-139">Sıfırlama gerçekleştirmeden önce en son sürümünü hello hello olduğundan emin olun [Resource Manager PowerShell cmdlet'leri](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="b675e-139">Before performing a reset, make sure you have hello latest version of hello [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="b675e-140">Merhaba aşağıdaki örnek hello TestRG1 kaynak grubunda VNet1GW adlı bir sanal ağ geçidi sıfırlar:</span><span class="sxs-lookup"><span data-stu-id="b675e-140">hello following example resets a virtual network gateway named VNet1GW in hello TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="b675e-141">Sonuç:</span><span class="sxs-lookup"><span data-stu-id="b675e-141">Result:</span></span>

<span data-ttu-id="b675e-142">Dönüş sonucu aldığınızda, hello ağ geçidi sıfırlama başarılı varsayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b675e-142">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="b675e-143">Ancak, hiçbir şey yoktur açıkça o hello sıfırlama başarıyla tamamlandığını belirten hello dönüş sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="b675e-143">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="b675e-144">Merhaba geçmişi toosee en yakından toolook istiyorsanız tam olarak hello ağ geçidi sıfırlandığında oluştu, hello bu bilgileri görüntüleyebilir [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b675e-144">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b675e-145">Merhaba Portalı'nda çok gidin**'GatewayName' -> kaynak durumu**.</span><span class="sxs-lookup"><span data-stu-id="b675e-145">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="b675e-146"><a name="resetclassic"></a>Klasik dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="b675e-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="b675e-147">bir ağ geçidi sıfırlama için cmdlet hello **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="b675e-147">hello cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="b675e-148">Sıfırlama gerçekleştirmeden önce en son sürümünü hello hello olduğundan emin olun [Hizmet Yönetimi (SM) PowerShell cmdlet'lerini](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="b675e-148">Before performing a reset, make sure you have hello latest version of hello [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="b675e-149">Merhaba aşağıdaki örnekte "ContosoVNet" adlı bir sanal ağ için ağ geçidi hello sıfırlar:</span><span class="sxs-lookup"><span data-stu-id="b675e-149">hello following example resets hello gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="b675e-150">Sonuç:</span><span class="sxs-lookup"><span data-stu-id="b675e-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="b675e-151"><a name="cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b675e-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="b675e-152">tooreset hello ağ geçidi, kullanım hello [az ağ vnet-gateway sıfırlama](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) komutu.</span><span class="sxs-lookup"><span data-stu-id="b675e-152">tooreset hello gateway, use hello [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="b675e-153">Merhaba aşağıdaki örnek vnet5gw'un hello TestRG5 kaynak grubunda adlı bir sanal ağ geçidi sıfırlar:</span><span class="sxs-lookup"><span data-stu-id="b675e-153">hello following example resets a virtual network gateway named VNet5GW in hello TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="b675e-154">Sonuç:</span><span class="sxs-lookup"><span data-stu-id="b675e-154">Result:</span></span>

<span data-ttu-id="b675e-155">Dönüş sonucu aldığınızda, hello ağ geçidi sıfırlama başarılı varsayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b675e-155">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="b675e-156">Ancak, hiçbir şey yoktur açıkça o hello sıfırlama başarıyla tamamlandığını belirten hello dönüş sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="b675e-156">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="b675e-157">Merhaba geçmişi toosee en yakından toolook istiyorsanız tam olarak hello ağ geçidi sıfırlandığında oluştu, hello bu bilgileri görüntüleyebilir [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b675e-157">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b675e-158">Merhaba Portalı'nda çok gidin**'GatewayName' -> kaynak durumu**.</span><span class="sxs-lookup"><span data-stu-id="b675e-158">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>
