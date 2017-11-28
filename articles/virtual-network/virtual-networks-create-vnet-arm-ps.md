---
title: "sanal ağ - Azure PowerShell aaaCreate | Microsoft Docs"
description: "Nasıl toocreate sanal bir ağ PowerShell'i kullanma hakkında bilgi edinin."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="4b65a-103">PowerShell kullanarak bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b65a-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="4b65a-104">Azure'un iki dağıtım modeli vardır: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="4b65a-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="4b65a-105">Microsoft, kaynakları hello Resource Manager dağıtım modeli üzerinden oluşturma önerir.</span><span class="sxs-lookup"><span data-stu-id="4b65a-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="4b65a-106">Merhaba iki modelleri arasındaki farklar hakkında daha fazla bilgi toolearn hello okuma hello [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="4b65a-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="4b65a-107">Bu makalede nasıl toocreate bir sanal ağ üzerinden hello Resource Manager dağıtım modeli PowerShell kullanarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4b65a-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="4b65a-108">Ayrıca, bir VNet kaynak diğer araçları kullanarak Yöneticisi aracılığıyla oluşturabilir veya liste aşağıdaki hello farklı bir seçeneği seçerek hello Klasik dağıtım modeli üzerinden bir VNet oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4b65a-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4b65a-109">Portal</span><span class="sxs-lookup"><span data-stu-id="4b65a-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="4b65a-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b65a-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="4b65a-111">CLI</span><span class="sxs-lookup"><span data-stu-id="4b65a-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="4b65a-112">Şablon</span><span class="sxs-lookup"><span data-stu-id="4b65a-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="4b65a-113">Portal (Klasik)</span><span class="sxs-lookup"><span data-stu-id="4b65a-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="4b65a-114">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="4b65a-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="4b65a-115">CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="4b65a-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="4b65a-116">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b65a-116">Create a virtual network</span></span>

<span data-ttu-id="4b65a-117">PowerShell, aşağıdaki tam hello kullanarak bir sanal ağ adımları toocreate:</span><span class="sxs-lookup"><span data-stu-id="4b65a-117">toocreate a virtual network using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="4b65a-118">Yükleme ve Azure PowerShell hello hello adımları izleyerek yapılandırma [nasıl tooInstall ve yapılandırma Azure PowerShell](/powershell/azure/overview) makalesi.</span><span class="sxs-lookup"><span data-stu-id="4b65a-118">Install and configure Azure PowerShell, by following hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="4b65a-119">Gerekirse, yeni bir kaynak grubunu aşağıda gösterildiği gibi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4b65a-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="4b65a-120">Bu senaryoda, bir kaynak grubu oluşturma *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="4b65a-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="4b65a-121">Kaynak grupları hakkında daha fazla bilgi için [Azure Resource Manager’a Genel Bakış](../azure-resource-manager/resource-group-overview.md)’ı ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="4b65a-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="4b65a-122">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="4b65a-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="4b65a-123">Adlı yeni bir VNet oluşturun *TestVNet*:</span><span class="sxs-lookup"><span data-stu-id="4b65a-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="4b65a-124">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="4b65a-124">Expected output:</span></span>

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. <span data-ttu-id="4b65a-125">Merhaba sanal ağ nesnesini bir değişkende saklayın:</span><span class="sxs-lookup"><span data-stu-id="4b65a-125">Store hello virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="4b65a-126">Adım 3 ve 4 çalıştırarak birleştirebilirsiniz `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span><span class="sxs-lookup"><span data-stu-id="4b65a-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="4b65a-127">Bir alt ağ toohello yeni VNet değişkenine ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4b65a-127">Add a subnet toohello new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="4b65a-128">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="4b65a-128">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. <span data-ttu-id="4b65a-129">Yukarıdaki 5. adım yineleme toocreate istediğiniz her alt ağ için.</span><span class="sxs-lookup"><span data-stu-id="4b65a-129">Repeat step 5 above for each subnet you want toocreate.</span></span> <span data-ttu-id="4b65a-130">Merhaba aşağıdaki komut oluşturur hello *arka uç* hello senaryo için alt ağ:</span><span class="sxs-lookup"><span data-stu-id="4b65a-130">hello following command creates hello *BackEnd* subnet for hello scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="4b65a-131">Alt ağları oluşturmuş olsanız da, bunlar şu anda yalnızca hello yerel değişken kullanılan tooretrieve hello yukarıdaki 4. adımda oluşturduğunuz sanal ağ yok.</span><span class="sxs-lookup"><span data-stu-id="4b65a-131">Although you create subnets, they currently only exist in hello local variable used tooretrieve hello VNet you create in step 4 above.</span></span> <span data-ttu-id="4b65a-132">komutu aşağıdaki hello çalıştırmak toosave hello değişiklikleri tooAzure:</span><span class="sxs-lookup"><span data-stu-id="4b65a-132">toosave hello changes tooAzure, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="4b65a-133">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="4b65a-133">Expected output:</span></span>
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a><span data-ttu-id="4b65a-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4b65a-134">Next steps</span></span>

<span data-ttu-id="4b65a-135">Bilgi nasıl tooconnect:</span><span class="sxs-lookup"><span data-stu-id="4b65a-135">Learn how tooconnect:</span></span>

- <span data-ttu-id="4b65a-136">Merhaba okuyarak sanal makine (VM) tooa sanal ağ [bir Windows VM oluşturma](../virtual-machines/virtual-machines-windows-ps-create.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="4b65a-136">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="4b65a-137">Merhaba makaleleri hello adımlarda bir VNet ve alt ağ oluşturmak yerine, bir VM'ye mevcut VNet ve alt ağ tooconnect seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b65a-137">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="4b65a-138">sanal ağ tooother sanal ağlar hello okuyarak hello [sanal ağlara bağlanma](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="4b65a-138">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="4b65a-139">bir siteden siteye sanal özel ağ (VPN) veya expressroute bağlantı hattı kullanarak hello sanal ağ tooan şirket içi ağ.</span><span class="sxs-lookup"><span data-stu-id="4b65a-139">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="4b65a-140">Bilgi hello okuyarak nasıl [bir siteden siteye VPN kullanarak bir VNet tooan şirket içi ağ bağlanmak](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) ve [VNet tooan expressroute bağlantı hattı bağlantı](../expressroute/expressroute-howto-linkvnet-arm.md) makaleleri.</span><span class="sxs-lookup"><span data-stu-id="4b65a-140">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
