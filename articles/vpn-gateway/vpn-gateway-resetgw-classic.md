---
title: "IPSec tünelleri yeniden kurmak için bir Azure VPN gateway sıfırlama | Microsoft Docs"
description: "Bu makalede IPSec tünelleri kurulmaya Azure VPN Gateway'i sıfırlama adımları anlatılmaktadır. Makale VPN ağ geçitleri hem Klasik ve Resource Manager dağıtım modelleri için geçerlidir."
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
ms.openlocfilehash: 7c5ba9310568571991708ab54a5275df6ea84a39
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="a5c97-104">VPN Gateway’i sıfırlama</span><span class="sxs-lookup"><span data-stu-id="a5c97-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="a5c97-105">Bir veya daha fazla Siteden Siteye VPN tünelinde şirketler arası VPN bağlantısını kaybederseniz bir Azure VPN ağ geçidinin sıfırlanması yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="a5c97-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="a5c97-106">Bu durumda şirket içi VPN cihazlarınızın tümü düzgün çalışır, ancak Azure VPN ağ geçitleriyle IPsec tünelleri kuramaz.</span><span class="sxs-lookup"><span data-stu-id="a5c97-106">In this situation, your on-premises VPN devices are all working correctly, but are not able to establish IPsec tunnels with the Azure VPN gateways.</span></span> <span data-ttu-id="a5c97-107">Bu makalede, VPN ağ geçidinizi sıfırlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="a5c97-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="a5c97-108">Sıfırlama sırasında ne olur?</span><span class="sxs-lookup"><span data-stu-id="a5c97-108">What happens during a reset?</span></span>

<span data-ttu-id="a5c97-109">Bir VPN ağ geçidi etkin bekleme yapılandırmasında çalışan iki VM örneğinden oluşur.</span><span class="sxs-lookup"><span data-stu-id="a5c97-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="a5c97-110">Ağ geçidi sıfırladığınızda, ağ geçidi yeniden başlatılır ve ona şirketler arası yapılandırmalar yeniden uygular.</span><span class="sxs-lookup"><span data-stu-id="a5c97-110">When you reset the gateway, it reboots the gateway, and then reapplies the cross-premises configurations to it.</span></span> <span data-ttu-id="a5c97-111">Ağ geçidi, sahip olduğu genel IP adresini tutar.</span><span class="sxs-lookup"><span data-stu-id="a5c97-111">The gateway keeps the public IP address it already has.</span></span> <span data-ttu-id="a5c97-112">Bu durum VPN yönlendirici yapılandırmasını Azure VPN ağ geçidi için yeni bir ortak IP adresi ile güncelleştirmenizin gerekli olmadığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="a5c97-112">This means you won’t need to update the VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="a5c97-113">Ağ geçidi sıfırlamak için komutu verdiğinizde, Azure VPN ağ geçidi geçerli etkin örneği hemen yeniden.</span><span class="sxs-lookup"><span data-stu-id="a5c97-113">When you issue the command to reset the gateway, the current active instance of the Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="a5c97-114">Bekleme örneğine etkin örnekten (yeniden başlatılan), yük devretme sırasında kısa bir boşluk olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a5c97-114">There will be a brief gap during the failover from the active instance (being rebooted), to the standby instance.</span></span> <span data-ttu-id="a5c97-115">Boşluk bir dakikadan az olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a5c97-115">The gap should be less than one minute.</span></span>

<span data-ttu-id="a5c97-116">İlk yeniden başlatma sonrasında bağlantı geri kazanılmazsa ikinci sanal makine örneğini (yeni etkin ağ geçidi) yeniden başlatmak için aynı komutu yeniden verin.</span><span class="sxs-lookup"><span data-stu-id="a5c97-116">If the connection is not restored after the first reboot, issue the same command again to reboot the second VM instance (the new active gateway).</span></span> <span data-ttu-id="a5c97-117">Arka arkaya iki yeniden başlatma istenirse her iki sanal makine örneğinin (etkin ve bekleme) yeniden başlatılma süresi biraz daha uzun olur.</span><span class="sxs-lookup"><span data-stu-id="a5c97-117">If the two reboots are requested back to back, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="a5c97-118">Bu, sanal makinelerin yeniden başlatma işlemlerini tamamlaması için VPN bağlantısı üzerinde 2 ila 4 dakikaya varan daha uzun bir boşluğa neden olur.</span><span class="sxs-lookup"><span data-stu-id="a5c97-118">This will cause a longer gap on the VPN connectivity, up to 2 to 4 minutes for VMs to complete the reboots.</span></span>

<span data-ttu-id="a5c97-119">Şirketler arası bağlantı sorunları yaşamaya devam ediyorsanız, iki yeniden başlatma sonrasında, lütfen Azure Portalı'ndan bir destek isteği açın.</span><span class="sxs-lookup"><span data-stu-id="a5c97-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from the Azure portal.</span></span>

## <span data-ttu-id="a5c97-120"><a name="before"></a>Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="a5c97-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="a5c97-121">Ağ geçidinizi sıfırlamadan önce her bir IPsec Siteden Siteye (S2S) VPN tüneli için aşağıda listelenen anahtar öğeleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a5c97-121">Before you reset your gateway, verify the key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="a5c97-122">Öğelerdeki uyuşmazlık S2S VPN tünellerinin bağlantısının kesilmesiyle sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="a5c97-122">Any mismatch in the items will result in the disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="a5c97-123">Doğrulama ve şirket içi ve Azure VPN ağ geçitleri için yapılandırmaları düzeltme gereksiz yeniden başlatmalardan ve kesintilerden üzerinde çalışan diğer bağlantılar ağ geçitleri için gelen kaydeder.</span><span class="sxs-lookup"><span data-stu-id="a5c97-123">Verifying and correcting the configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for the other working connections on the gateways.</span></span>

<span data-ttu-id="a5c97-124">Ağ geçidinizi sıfırlamadan önce aşağıdaki öğeleri doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="a5c97-124">Verify the following items before resetting your gateway:</span></span>

* <span data-ttu-id="a5c97-125">Hem Azure VPN ağ geçidi hem de şirket içi VPN ağ geçidi için İnternet IP adresleri (VIP) hem Azure hem de şirket içi VPN ilkelerinde doğru şekilde yapılandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a5c97-125">The Internet IP addresses (VIPs) for both the Azure VPN gateway and the on-premises VPN gateway are configured correctly in both the Azure and the on-premises VPN policies.</span></span>
* <span data-ttu-id="a5c97-126">Önceden paylaşılan anahtar Azure ve şirket içi VPN ağ geçitlerinde aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a5c97-126">The pre-shared key must be the same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="a5c97-127">Şifreleme, karma algoritmaları ve PFS (Kusursuz İletme Gizliliği) gibi belirli IPsec/IKE yapılandırmalarını uygularsanız hem Azure hem de şirket içi VPN ağ geçitlerinin aynı yapılandırmalara sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="a5c97-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both the Azure and on-premises VPN gateways have the same configurations.</span></span>

## <span data-ttu-id="a5c97-128"><a name="portal"></a>Azure portalı</span><span class="sxs-lookup"><span data-stu-id="a5c97-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="a5c97-129">Azure Portalı'nı kullanarak bir Resource Manager VPN ağ geçidi sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5c97-129">You can reset a Resource Manager VPN gateway using the Azure portal.</span></span> <span data-ttu-id="a5c97-130">Klasik bir ağ geçidi sıfırlamak istiyorsanız, bkz: [PowerShell](#resetclassic) adımları.</span><span class="sxs-lookup"><span data-stu-id="a5c97-130">If you want to reset a classic gateway, see the [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="a5c97-131">Resource Manager dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="a5c97-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="a5c97-132">Açık [Azure portal](https://portal.azure.com) ve sıfırlamak istediğiniz kaynak yöneticisi sanal ağ geçidi gidin.</span><span class="sxs-lookup"><span data-stu-id="a5c97-132">Open the [Azure portal](https://portal.azure.com) and navigate to the Resource Manager virtual network gateway that you want to reset.</span></span>
2. <span data-ttu-id="a5c97-133">Sanal ağ geçidi için dikey 'Sıfırla' yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a5c97-133">On the blade for the virtual network gateway, click 'Reset'.</span></span>

  ![VPN ağ geçidi dikey Sıfırla](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="a5c97-135">Sıfırlama dikey penceresinde **sıfırlama** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="a5c97-135">On the Reset blade, click the **Reset** button.</span></span>

## <span data-ttu-id="a5c97-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5c97-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="a5c97-137">Resource Manager dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="a5c97-137">Resource Manager deployment model</span></span>

<span data-ttu-id="a5c97-138">Bir ağ geçidi sıfırlama cmdlet'i **sıfırlama AzureRmVirtualNetworkGateway**.</span><span class="sxs-lookup"><span data-stu-id="a5c97-138">The cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="a5c97-139">Sıfırlama gerçekleştirmeden önce en son sürümünü olduğundan emin olun [Resource Manager PowerShell cmdlet'leri](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span><span class="sxs-lookup"><span data-stu-id="a5c97-139">Before performing a reset, make sure you have the latest version of the [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="a5c97-140">Aşağıdaki örnek TestRG1 kaynak grubunda VNet1GW adlı bir sanal ağ geçidi sıfırlar:</span><span class="sxs-lookup"><span data-stu-id="a5c97-140">The following example resets a virtual network gateway named VNet1GW in the TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="a5c97-141">Sonuç:</span><span class="sxs-lookup"><span data-stu-id="a5c97-141">Result:</span></span>

<span data-ttu-id="a5c97-142">Dönüş sonucu aldığınızda, ağ geçidi sıfırlama başarılı varsayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5c97-142">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="a5c97-143">Ancak, hiçbir şey yoktur açıkça sıfırlama işleminin başarılı olduğunu belirten dönüş sonucu.</span><span class="sxs-lookup"><span data-stu-id="a5c97-143">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="a5c97-144">Ağ geçidi sıfırlama gerçekleştiği tam olarak görmek için geçmiş yakından aramak istiyorsanız, bu bilgiyi görüntüleyebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5c97-144">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a5c97-145">Portalı'nda gidin **'GatewayName' -> kaynak durumu**.</span><span class="sxs-lookup"><span data-stu-id="a5c97-145">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="a5c97-146"><a name="resetclassic"></a>Klasik dağıtım modeli</span><span class="sxs-lookup"><span data-stu-id="a5c97-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="a5c97-147">Bir ağ geçidi sıfırlama cmdlet'i **Reset-AzureVNetGateway**.</span><span class="sxs-lookup"><span data-stu-id="a5c97-147">The cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="a5c97-148">Sıfırlama gerçekleştirmeden önce en son sürümünü olduğundan emin olun [Hizmet Yönetimi (SM) PowerShell cmdlet'lerini](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span><span class="sxs-lookup"><span data-stu-id="a5c97-148">Before performing a reset, make sure you have the latest version of the [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="a5c97-149">Aşağıdaki örnekte "ContosoVNet" adlı bir sanal ağ için ağ geçidi sıfırlar:</span><span class="sxs-lookup"><span data-stu-id="a5c97-149">The following example resets the gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="a5c97-150">Sonuç:</span><span class="sxs-lookup"><span data-stu-id="a5c97-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="a5c97-151"><a name="cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a5c97-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="a5c97-152">Ağ geçidini sıfırlamaya kullanmak [az ağ vnet-gateway sıfırlama](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) komutu.</span><span class="sxs-lookup"><span data-stu-id="a5c97-152">To reset the gateway, use the [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="a5c97-153">Aşağıdaki örnek vnet5gw'un TestRG5 kaynak grubunda adlı bir sanal ağ geçidi sıfırlar:</span><span class="sxs-lookup"><span data-stu-id="a5c97-153">The following example resets a virtual network gateway named VNet5GW in the TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="a5c97-154">Sonuç:</span><span class="sxs-lookup"><span data-stu-id="a5c97-154">Result:</span></span>

<span data-ttu-id="a5c97-155">Dönüş sonucu aldığınızda, ağ geçidi sıfırlama başarılı varsayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a5c97-155">When you receive a return result, you can assume the gateway reset was successful.</span></span> <span data-ttu-id="a5c97-156">Ancak, hiçbir şey yoktur açıkça sıfırlama işleminin başarılı olduğunu belirten dönüş sonucu.</span><span class="sxs-lookup"><span data-stu-id="a5c97-156">However, there is nothing in the return result that indicates explicitly that the reset was successful.</span></span> <span data-ttu-id="a5c97-157">Ağ geçidi sıfırlama gerçekleştiği tam olarak görmek için geçmiş yakından aramak istiyorsanız, bu bilgiyi görüntüleyebilirsiniz [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a5c97-157">If you want to look closely at the history to see exactly when the gateway reset occurred, you can view that information in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="a5c97-158">Portalı'nda gidin **'GatewayName' -> kaynak durumu**.</span><span class="sxs-lookup"><span data-stu-id="a5c97-158">In the portal, navigate to **'GatewayName' -> Resource Health**.</span></span>