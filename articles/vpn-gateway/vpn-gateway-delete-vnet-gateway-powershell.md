---
title: "Bir sanal ağ geçidini silmek: PowerShell: Azure Resource Manager | Microsoft Docs"
description: "Resource Manager dağıtım modelinde PowerShell kullanarak bir sanal ağ geçidini silin."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 4d0f085423d5bd60b24d88649ee1d77bcd1d009f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell"></a><span data-ttu-id="b575d-103">PowerShell kullanarak bir sanal ağ geçidini Sil</span><span class="sxs-lookup"><span data-stu-id="b575d-103">Delete a virtual network gateway using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b575d-104">Azure portal</span><span class="sxs-lookup"><span data-stu-id="b575d-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="b575d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b575d-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="b575d-106">PowerShell (klasik)</span><span class="sxs-lookup"><span data-stu-id="b575d-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="b575d-107">Birkaç VPN ağ geçidi yapılandırması için bir sanal ağ geçidi silmek istediğinizde uygulayabileceğiniz çeşitli yaklaşımlar vardır.</span><span class="sxs-lookup"><span data-stu-id="b575d-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="b575d-108">Her şeyi silin ve üzerinde bir test ortamı durumda olduğu gibi başlatmak istiyorsanız, kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b575d-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="b575d-109">Bir kaynak grubunu silmek gruptaki tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="b575d-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="b575d-110">Bu yöntem olduğundan tüm kaynakların kaynak grubunda saklamak istemiyorsanız yalnızca önerilir.</span><span class="sxs-lookup"><span data-stu-id="b575d-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="b575d-111">Bu yaklaşımı kullanarak yalnızca birkaç kaynakları seçmeli olarak silemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="b575d-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="b575d-112">Bazı kaynakların kaynak grubunda tutmak istiyorsanız, bir sanal ağ geçidi silinmesi biraz daha karmaşık olabilir.</span><span class="sxs-lookup"><span data-stu-id="b575d-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="b575d-113">Sanal ağ geçidi silmeden önce ağ geçidinde bağımlı herhangi bir kaynağa silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b575d-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="b575d-114">İzleyeceğiniz adımlar oluşturduğunuz bağlantı türünü ve her bağlantı için bağımlı kaynakları bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b575d-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="b575d-115">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b575d-115">Before beginning</span></span>

### <a name="1-download-the-latest-azure-resource-manager-powershell-cmdlets"></a><span data-ttu-id="b575d-116">1. En son Azure Resource Manager PowerShell cmdlet'lerini indirin.</span><span class="sxs-lookup"><span data-stu-id="b575d-116">1. Download the latest Azure Resource Manager PowerShell cmdlets.</span></span>

<span data-ttu-id="b575d-117">Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyip yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="b575d-117">Download and install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="b575d-118">Karşıdan yükleme ve PowerShell cmdlet'leri hakkında daha fazla bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b575d-118">For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="b575d-119">2. Azure hesabınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="b575d-119">2. Connect to your Azure account.</span></span>

<span data-ttu-id="b575d-120">PowerShell konsolunuzu açın ve hesabınıza bağlanın.</span><span class="sxs-lookup"><span data-stu-id="b575d-120">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="b575d-121">Bağlanmanıza yardımcı olması için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="b575d-121">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="b575d-122">Hesapla ilişkili abonelikleri kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="b575d-122">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="b575d-123">Birden fazla aboneliğiniz varsa, kullanmak istediğiniz aboneliği belirtin.</span><span class="sxs-lookup"><span data-stu-id="b575d-123">If you have more than one subscription, specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="b575d-124"><a name="S2S"></a>Siteden siteye VPN ağ geçidini silin</span><span class="sxs-lookup"><span data-stu-id="b575d-124"><a name="S2S"></a>Delete a Site-to-Site VPN gateway</span></span>

<span data-ttu-id="b575d-125">Bir sanal ağ geçidi S2S yapılandırması için silmek için önce sanal ağ geçidi için ilgili her bir kaynağın silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b575d-125">To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="b575d-126">Belirli bir sırada bağımlılıkları nedeniyle kaynakları silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b575d-126">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="b575d-127">Diğer değerleri bir çıktı sonuç durumdayken aşağıda bazı örnekler ile çalışırken değerler belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="b575d-127">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="b575d-128">Aşağıdaki değerleri örneklerde tanıtım amacıyla kullanırız:</span><span class="sxs-lookup"><span data-stu-id="b575d-128">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="b575d-129">Sanal ağ adı: VNet1</span><span class="sxs-lookup"><span data-stu-id="b575d-129">VNet name: VNet1</span></span><br>
<span data-ttu-id="b575d-130">Kaynak grubu adı: RG1</span><span class="sxs-lookup"><span data-stu-id="b575d-130">Resource Group name: RG1</span></span><br>
<span data-ttu-id="b575d-131">Sanal ağ geçidi adı: GW1</span><span class="sxs-lookup"><span data-stu-id="b575d-131">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="b575d-132">Aşağıdaki adımlar Resource Manager dağıtım modeli için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b575d-132">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="b575d-133">1. Silmek istediğiniz sanal ağ geçidi alın.</span><span class="sxs-lookup"><span data-stu-id="b575d-133">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="b575d-134">2. Sanal ağ geçidi herhangi bir bağlantısı olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b575d-134">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
$Conns=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```

### <a name="3-delete-all-connections"></a><span data-ttu-id="b575d-135">3. Tüm bağlantılar silin.</span><span class="sxs-lookup"><span data-stu-id="b575d-135">3. Delete all connections.</span></span>

<span data-ttu-id="b575d-136">Her bağlantıların silme işlemini onaylamak için istenebilir.</span><span class="sxs-lookup"><span data-stu-id="b575d-136">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$Conns | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="4-delete-the-virtual-network-gateway"></a><span data-ttu-id="b575d-137">4. Sanal ağ geçidini silin.</span><span class="sxs-lookup"><span data-stu-id="b575d-137">4. Delete the virtual network gateway.</span></span>

<span data-ttu-id="b575d-138">Ağ geçidini silme işlemini onaylamak için istenebilir.</span><span class="sxs-lookup"><span data-stu-id="b575d-138">You may be prompted to confirm the deletion of the gateway.</span></span> <span data-ttu-id="b575d-139">Bu sanal ağa P2S yapılandırma S2S yapılandırmanızı yanı sıra varsa, sanal ağ geçidi siliniyor uyarmadan tüm P2S istemcileri otomatik olarak bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="b575d-139">If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.</span></span>


```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="b575d-140">Bu noktada, sanal ağ geçidinizi silindi.</span><span class="sxs-lookup"><span data-stu-id="b575d-140">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="b575d-141">Sonraki adımlar, artık kullanılmayan kaynakları silmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b575d-141">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="5-delete-the-local-network-gateways"></a><span data-ttu-id="b575d-142">5 yerel ağ geçitlerini silin.</span><span class="sxs-lookup"><span data-stu-id="b575d-142">5 Delete the local network gateways.</span></span>

<span data-ttu-id="b575d-143">Karşılık gelen yerel ağ geçitleri listesini alın.</span><span class="sxs-lookup"><span data-stu-id="b575d-143">Get the list of the corresponding local network gateways.</span></span>

```powershell
$LNG=Get-AzureRmLocalNetworkGateway -ResourceGroupName "RG1" | where-object {$_.Id -In $Conns.LocalNetworkGateway2.Id}
```

<span data-ttu-id="b575d-144">Yerel ağ geçitleri silin.</span><span class="sxs-lookup"><span data-stu-id="b575d-144">Delete the local network gateways.</span></span> <span data-ttu-id="b575d-145">Her bir yerel ağ geçidi silmeyi onaylamak için istenebilir.</span><span class="sxs-lookup"><span data-stu-id="b575d-145">You may be prompted to confirm the deletion of each of the local network gateway.</span></span>

```powershell
$LNG | ForEach-Object {Remove-AzureRmLocalNetworkGateway -Name $_.Name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="b575d-146">6. Genel IP adresi kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="b575d-146">6. Delete the Public IP address resources.</span></span>

<span data-ttu-id="b575d-147">Sanal ağ geçidinin IP yapılandırmalarını alma.</span><span class="sxs-lookup"><span data-stu-id="b575d-147">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="b575d-148">Bu sanal ağ geçidi için kullanılan genel IP adresi kaynakları listesini alın.</span><span class="sxs-lookup"><span data-stu-id="b575d-148">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="b575d-149">Sanal ağ geçidi etkin-etkin iki genel IP adresleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b575d-149">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="b575d-150">Genel IP kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="b575d-150">Delete the Public IP resources.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "RG1"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="b575d-151">7. Ağ geçidi alt ağını silmek ve yapılandırmasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b575d-151">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="b575d-152"><a name="v2v"></a>VNet-VNet VPN ağ geçidini silin</span><span class="sxs-lookup"><span data-stu-id="b575d-152"><a name="v2v"></a>Delete a VNet-to-VNet VPN gateway</span></span>

<span data-ttu-id="b575d-153">V2V yapılandırması için bir sanal ağ geçidi silmek için önce sanal ağ geçidi için ilgili her bir kaynağın silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b575d-153">To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="b575d-154">Belirli bir sırada bağımlılıkları nedeniyle kaynakları silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b575d-154">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="b575d-155">Diğer değerleri bir çıktı sonuç durumdayken aşağıda bazı örnekler ile çalışırken değerler belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="b575d-155">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="b575d-156">Aşağıdaki değerleri örneklerde tanıtım amacıyla kullanırız:</span><span class="sxs-lookup"><span data-stu-id="b575d-156">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="b575d-157">Sanal ağ adı: VNet1</span><span class="sxs-lookup"><span data-stu-id="b575d-157">VNet name: VNet1</span></span><br>
<span data-ttu-id="b575d-158">Kaynak grubu adı: RG1</span><span class="sxs-lookup"><span data-stu-id="b575d-158">Resource Group name: RG1</span></span><br>
<span data-ttu-id="b575d-159">Sanal ağ geçidi adı: GW1</span><span class="sxs-lookup"><span data-stu-id="b575d-159">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="b575d-160">Aşağıdaki adımlar Resource Manager dağıtım modeli için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b575d-160">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="b575d-161">1. Silmek istediğiniz sanal ağ geçidi alın.</span><span class="sxs-lookup"><span data-stu-id="b575d-161">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="b575d-162">2. Sanal ağ geçidi herhangi bir bağlantısı olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b575d-162">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="b575d-163">Farklı bir kaynak grubu parçası olan diğer sanal ağ geçidi bağlantıları olabilir.</span><span class="sxs-lookup"><span data-stu-id="b575d-163">There may be other connections to the virtual network gateway that are part of a different resource group.</span></span> <span data-ttu-id="b575d-164">Her ek kaynak grubunda ek bağlantılar olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b575d-164">Check for additional connections in each additional resource group.</span></span> <span data-ttu-id="b575d-165">Bu örnekte, biz RG2 gelen bağlantıları için denetleniyor.</span><span class="sxs-lookup"><span data-stu-id="b575d-165">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="b575d-166">Bu, her kaynak grubu için hangi sanal ağ geçidi bağlantı olabilir sahip çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b575d-166">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG2" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
```

### <a name="3-get-the-list-of-connections-in-both-directions"></a><span data-ttu-id="b575d-167">3. Her iki yönde de bağlantıların listesini alır.</span><span class="sxs-lookup"><span data-stu-id="b575d-167">3. Get the list of connections in both directions.</span></span>

<span data-ttu-id="b575d-168">Bu VNet-VNet yapılandırması olduğundan, her iki yönde bağlantıların listesini gerekir.</span><span class="sxs-lookup"><span data-stu-id="b575d-168">Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.</span></span>

```powershell
$ConnsL=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="b575d-169">Bu örnekte, biz RG2 gelen bağlantıları için denetleniyor.</span><span class="sxs-lookup"><span data-stu-id="b575d-169">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="b575d-170">Bu, her kaynak grubu için hangi sanal ağ geçidi bağlantı olabilir sahip çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b575d-170">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
 $ConnsR=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "<NameOfResourceGroup2>" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
 ```

### <a name="4-delete-all-connections"></a><span data-ttu-id="b575d-171">4. Tüm bağlantılar silin.</span><span class="sxs-lookup"><span data-stu-id="b575d-171">4. Delete all connections.</span></span>

<span data-ttu-id="b575d-172">Her bağlantıların silme işlemini onaylamak için istenebilir.</span><span class="sxs-lookup"><span data-stu-id="b575d-172">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$ConnsL | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
$ConnsR | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="5-delete-the-virtual-network-gateway"></a><span data-ttu-id="b575d-173">5. Sanal ağ geçidini silin.</span><span class="sxs-lookup"><span data-stu-id="b575d-173">5. Delete the virtual network gateway.</span></span>

<span data-ttu-id="b575d-174">Sanal ağ geçidini silme işlemini onaylamak için istenebilir.</span><span class="sxs-lookup"><span data-stu-id="b575d-174">You may be prompted to confirm the deletion of the virtual network gateway.</span></span> <span data-ttu-id="b575d-175">V2V yapılandırmanızı ek olarak, sanal ağlar P2S yapılandırmaları varsa, sanal ağ geçitlerini silme uyarmadan tüm P2S istemcileri otomatik olarak bağlantısını keser.</span><span class="sxs-lookup"><span data-stu-id="b575d-175">If you have P2S configurations to your VNets in addition to your V2V configuration, deleting the virtual network gateways will automatically disconnect all P2S clients without warning.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="b575d-176">Bu noktada, sanal ağ geçidinizi silindi.</span><span class="sxs-lookup"><span data-stu-id="b575d-176">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="b575d-177">Sonraki adımlar, artık kullanılmayan kaynakları silmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b575d-177">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="b575d-178">6. Genel IP adresi kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="b575d-178">6. Delete the Public IP address resources</span></span>

<span data-ttu-id="b575d-179">Sanal ağ geçidinin IP yapılandırmalarını alma.</span><span class="sxs-lookup"><span data-stu-id="b575d-179">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="b575d-180">Bu sanal ağ geçidi için kullanılan genel IP adresi kaynakları listesini alın.</span><span class="sxs-lookup"><span data-stu-id="b575d-180">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="b575d-181">Sanal ağ geçidi etkin-etkin iki genel IP adresleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b575d-181">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="b575d-182">Genel IP kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="b575d-182">Delete the Public IP resources.</span></span> <span data-ttu-id="b575d-183">Genel IP silme işlemini onaylamak için istenebilir.</span><span class="sxs-lookup"><span data-stu-id="b575d-183">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="b575d-184">7. Ağ geçidi alt ağını silmek ve yapılandırmasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b575d-184">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="b575d-185"><a name="deletep2s"></a>Bir noktadan siteye VPN ağ geçidini silin</span><span class="sxs-lookup"><span data-stu-id="b575d-185"><a name="deletep2s"></a>Delete a Point-to-Site VPN gateway</span></span>

<span data-ttu-id="b575d-186">P2S yapılandırması için bir sanal ağ geçidi silmek için önce sanal ağ geçidi için ilgili her bir kaynağın silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b575d-186">To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="b575d-187">Belirli bir sırada bağımlılıkları nedeniyle kaynakları silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b575d-187">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="b575d-188">Diğer değerleri bir çıktı sonuç durumdayken aşağıda bazı örnekler ile çalışırken değerler belirtilmelidir.</span><span class="sxs-lookup"><span data-stu-id="b575d-188">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="b575d-189">Aşağıdaki değerleri örneklerde tanıtım amacıyla kullanırız:</span><span class="sxs-lookup"><span data-stu-id="b575d-189">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="b575d-190">Sanal ağ adı: VNet1</span><span class="sxs-lookup"><span data-stu-id="b575d-190">VNet name: VNet1</span></span><br>
<span data-ttu-id="b575d-191">Kaynak grubu adı: RG1</span><span class="sxs-lookup"><span data-stu-id="b575d-191">Resource Group name: RG1</span></span><br>
<span data-ttu-id="b575d-192">Sanal ağ geçidi adı: GW1</span><span class="sxs-lookup"><span data-stu-id="b575d-192">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="b575d-193">Aşağıdaki adımlar Resource Manager dağıtım modeli için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b575d-193">The following steps apply to the Resource Manager deployment model.</span></span>


>[!NOTE]
> <span data-ttu-id="b575d-194">VPN ağ geçidini sildiğinizde, tüm bağlı istemcileri uyarmadan VNet kesilecektir.</span><span class="sxs-lookup"><span data-stu-id="b575d-194">When you delete the VPN gateway, all connected clients will be disconnected from the VNet without warning.</span></span>
>
>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="b575d-195">1. Silmek istediğiniz sanal ağ geçidi alın.</span><span class="sxs-lookup"><span data-stu-id="b575d-195">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-delete-the-virtual-network-gateway"></a><span data-ttu-id="b575d-196">2. Sanal ağ geçidini silin.</span><span class="sxs-lookup"><span data-stu-id="b575d-196">2. Delete the virtual network gateway.</span></span>

<span data-ttu-id="b575d-197">Sanal ağ geçidini silme işlemini onaylamak için istenebilir.</span><span class="sxs-lookup"><span data-stu-id="b575d-197">You may be prompted to confirm the deletion of the virtual network gateway.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="b575d-198">Bu noktada, sanal ağ geçidinizi silindi.</span><span class="sxs-lookup"><span data-stu-id="b575d-198">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="b575d-199">Sonraki adımlar, artık kullanılmayan kaynakları silmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b575d-199">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="3-delete-the-public-ip-address-resources"></a><span data-ttu-id="b575d-200">3. Genel IP adresi kaynakları silme</span><span class="sxs-lookup"><span data-stu-id="b575d-200">3. Delete the Public IP address resources</span></span>

<span data-ttu-id="b575d-201">Sanal ağ geçidinin IP yapılandırmalarını alma.</span><span class="sxs-lookup"><span data-stu-id="b575d-201">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="b575d-202">Bu sanal ağ geçidi için kullanılan genel IP adresleri listesi alınamadı.</span><span class="sxs-lookup"><span data-stu-id="b575d-202">Get the list of Public IP addresses used for this virtual network gateway.</span></span> <span data-ttu-id="b575d-203">Sanal ağ geçidi etkin-etkin iki genel IP adresleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b575d-203">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="b575d-204">Genel IP'ler silin.</span><span class="sxs-lookup"><span data-stu-id="b575d-204">Delete the Public IPs.</span></span> <span data-ttu-id="b575d-205">Genel IP silme işlemini onaylamak için istenebilir.</span><span class="sxs-lookup"><span data-stu-id="b575d-205">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="4-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="b575d-206">4. Ağ geçidi alt ağını silmek ve yapılandırmasını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b575d-206">4. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="b575d-207"><a name="delete"></a>Kaynak grubunu silerek bir VPN ağ geçidini Sil</span><span class="sxs-lookup"><span data-stu-id="b575d-207"><a name="delete"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="b575d-208">Kaynak grubunda kaynaklarınızın hiçbirini saklanması ilgili değildir ve baştan başlamak istiyorsanız, tüm kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b575d-208">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="b575d-209">Bu, her şeyi kaldırmak için hızlı bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="b575d-209">This is a quick way to remove everything.</span></span> <span data-ttu-id="b575d-210">Aşağıdaki adımlar yalnızca Resource Manager dağıtım modeli için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="b575d-210">The following steps apply only to the Resource Manager deployment model.</span></span>

### <a name="1-get-a-list-of-all-the-resource-groups-in-your-subscription"></a><span data-ttu-id="b575d-211">1. Aboneliğinizdeki tüm kaynak gruplarının bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="b575d-211">1. Get a list of all the resource groups in your subscription.</span></span>

```powershell
Get-AzureRmResourceGroup
```

### <a name="2-locate-the-resource-group-that-you-want-to-delete"></a><span data-ttu-id="b575d-212">2. Silmek istediğiniz kaynak grubunu bulun.</span><span class="sxs-lookup"><span data-stu-id="b575d-212">2. Locate the resource group that you want to delete.</span></span>

<span data-ttu-id="b575d-213">Silin ve bu kaynak grubunda kaynaklar listesi görüntülemek istediğiniz kaynak grubunu bulun.</span><span class="sxs-lookup"><span data-stu-id="b575d-213">Locate the resource group that you want to delete and view the list of resources in that resource group.</span></span> <span data-ttu-id="b575d-214">Örnekte, RG1 kaynak grubunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="b575d-214">In the example, the name of the resource group is RG1.</span></span> <span data-ttu-id="b575d-215">Tüm kaynakların bir listesini almak için örnek değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b575d-215">Modify the example to retrieve a list of all the resources.</span></span>

```powershell
Find-AzureRmResource -ResourceGroupNameContains RG1
```

### <a name="3-verify-the-resources-in-the-list"></a><span data-ttu-id="b575d-216">3. Listenin kaynaklarında doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b575d-216">3. Verify the resources in the list.</span></span>

<span data-ttu-id="b575d-217">Listenin döndürüldüğünde, kaynak grubunun yanı sıra, kaynak grubunun tüm kaynakları silmek istediğiniz doğrulamak için gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="b575d-217">When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself.</span></span> <span data-ttu-id="b575d-218">Bazı kaynakların kaynak grubunda tutmak istiyorsanız, adımlar bu makalenin önceki bölümlerinde, ağ geçidi silmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="b575d-218">If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.</span></span>

### <a name="4-delete-the-resource-group-and-resources"></a><span data-ttu-id="b575d-219">4. Kaynak grubu ve kaynakları silin.</span><span class="sxs-lookup"><span data-stu-id="b575d-219">4. Delete the resource group and resources.</span></span>

<span data-ttu-id="b575d-220">Kaynak grubu ve kaynak grubunda bulunan tüm kaynak silmek için örnek değiştirin ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b575d-220">To delete the resource group and all the resource contained in the resource group, modify the example and run.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name RG1
```

### <a name="5-check-the-status"></a><span data-ttu-id="b575d-221">5. Durumunu kontrol edin.</span><span class="sxs-lookup"><span data-stu-id="b575d-221">5. Check the status.</span></span>

<span data-ttu-id="b575d-222">Tüm kaynakları silmek Azure için biraz zaman alabilir.</span><span class="sxs-lookup"><span data-stu-id="b575d-222">It takes some time for Azure to delete all the resources.</span></span> <span data-ttu-id="b575d-223">Bu cmdlet'i kullanarak, kaynak grubunuzun durumunu kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b575d-223">You can check the status of your resource group by using this cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName RG1
```

<span data-ttu-id="b575d-224">Döndürülen sonucu 'Başarılı' gösterir.</span><span class="sxs-lookup"><span data-stu-id="b575d-224">The result that is returned shows 'Succeeded'.</span></span>

```
ResourceGroupName : RG1
Location          : eastus
ProvisioningState : Succeeded
```