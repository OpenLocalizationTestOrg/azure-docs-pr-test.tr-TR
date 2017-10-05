---
title: "Denetim bir Azure Virtual Network - PowerShell - Klasik yönlendirme | Microsoft Docs"
description: "PowerShell kullanarak Vnet'lerde yönlendirilmesini denetlemesini öğrenin | Klasik"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: e9564d223cb85529f1fa97bc398d35c6debcedae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="e988d-103">Yönlendirme denetlemek ve PowerShell kullanarak sanal gereçler (Klasik) kullanma</span><span class="sxs-lookup"><span data-stu-id="e988d-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="e988d-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e988d-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="e988d-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e988d-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="e988d-106">Şablon</span><span class="sxs-lookup"><span data-stu-id="e988d-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="e988d-107">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="e988d-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="e988d-108">CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="e988d-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="e988d-109">Azure kaynaklarıyla çalışmadan önce Azure’da şu anda iki dağıtım modeli olduğunu anlamak önemlidir: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="e988d-109">Before you work with Azure resources, it's important to understand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="e988d-110">Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-resource-manager/resource-manager-deployment-model.md) iyice anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e988d-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="e988d-111">Bu makalenin üst seçeneklerden birini seçerek, farklı araçlarla ilgili belgeleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e988d-111">You can view the documentation for different tools by selecting an option at the top of this article.</span></span> <span data-ttu-id="e988d-112">Bu makale, klasik dağıtım modelini kapsamaktadır.</span><span class="sxs-lookup"><span data-stu-id="e988d-112">This article covers the classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="e988d-113">Örnek senaryo yukarıdaki Azure PowerShell önceden oluşturulmuş basit bir ortam aşağıdaki komutları beklediğiniz temel.</span><span class="sxs-lookup"><span data-stu-id="e988d-113">The sample Azure PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="e988d-114">Bu belgede gösterildiği komutları çalıştırmak istiyorsanız, gösterildiği ortamı oluşturmak [PowerShell kullanarak bir sanal ağ (Klasik) oluşturmak](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="e988d-114">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="e988d-115">Ön uç alt UDR oluşturma</span><span class="sxs-lookup"><span data-stu-id="e988d-115">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="e988d-116">Yol tablosu ve yukarıdaki senaryoyu temel ön uç alt ağ için gereken rota oluşturmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="e988d-116">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="e988d-117">Ön uç alt ağ için yol tablosu oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e988d-117">Run the following command to create a route table for the front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="e988d-118">İçin bir yol (192.168.2.0/24) arka uç alt ağa giden tüm trafiği göndermek için yol tablosu oluşturmak için aşağıdaki komutu çalıştırın **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="e988d-118">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="e988d-119">Yol tablosu ile ilişkilendirmek için aşağıdaki komutu çalıştırın **ön uç** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="e988d-119">Run the following command to associate the route table with the **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="e988d-120">Arka uç alt ağ için UDR oluşturma</span><span class="sxs-lookup"><span data-stu-id="e988d-120">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="e988d-121">Yol tablosu ve senaryoyu temel arka uç alt ağ için gereken rota oluşturmak için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="e988d-121">To create the route table and route needed for the back end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="e988d-122">Arka uç alt ağ için yol tablosu oluşturmak için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e988d-122">Run the following command to create a route table for the back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="e988d-123">İçin bir yol (192.168.1.0/24) ön uç alt ağa giden tüm trafiği göndermek için yol tablosu oluşturmak için aşağıdaki komutu çalıştırın **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="e988d-123">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="e988d-124">Yol tablosu ile ilişkilendirmek için aşağıdaki komutu çalıştırın **arka uç** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="e988d-124">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-the-fw1-vm"></a><span data-ttu-id="e988d-125">FW1 VM'de IP iletimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e988d-125">Enable IP forwarding on the FW1 VM</span></span>

<span data-ttu-id="e988d-126">IP FW1 VM'yi iletmeyi etkinleştirmek için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="e988d-126">To enable IP forwarding in the FW1 VM, complete the following steps:</span></span>

1. <span data-ttu-id="e988d-127">IP iletimi durumunu denetlemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="e988d-127">Run the following command to check the status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="e988d-128">IP için iletmeyi etkinleştirmek için aşağıdaki komutu çalıştırın *FW1* VM:</span><span class="sxs-lookup"><span data-stu-id="e988d-128">Run the following command to enable IP forwarding for the *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
