---
title: "bir Azure Virtual Network - PowerShell - Klasik aaaControl yönlendirme | Microsoft Docs"
description: "Bilgi nasıl toocontrol PowerShell kullanarak Vnet'lerde yönlendirme | Klasik"
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
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="3976c-103">Yönlendirme denetlemek ve PowerShell kullanarak sanal gereçler (Klasik) kullanma</span><span class="sxs-lookup"><span data-stu-id="3976c-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="3976c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3976c-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="3976c-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3976c-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="3976c-106">Şablon</span><span class="sxs-lookup"><span data-stu-id="3976c-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="3976c-107">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="3976c-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="3976c-108">CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="3976c-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="3976c-109">Azure kaynaklarıyla çalışmadan önce Azure'da şu anda iki dağıtım modeli olduğunu önemli toounderstand olduğu: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="3976c-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="3976c-110">Azure kaynaklarıyla çalışmadan önce [dağıtım modellerini ve araçlarlarını](../azure-resource-manager/resource-manager-deployment-model.md) iyice anladığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="3976c-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="3976c-111">Bu makalede hello üstündeki seçeneklerden birini seçerek hello farklı araçlarla ilgili belgeleri görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3976c-111">You can view hello documentation for different tools by selecting an option at hello top of this article.</span></span> <span data-ttu-id="3976c-112">Bu makalede, hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="3976c-112">This article covers hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="3976c-113">Azure PowerShell önceden oluşturulmuş basit bir ortam aşağıdaki komutları beklediğiniz Hello örnek senaryosunda hello yukarıdaki temel.</span><span class="sxs-lookup"><span data-stu-id="3976c-113">hello sample Azure PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="3976c-114">Bu belgede gösterildiği toorun hello komutları istiyorsanız, gösterildiği hello ortamı oluşturmak [PowerShell kullanarak bir sanal ağ (Klasik) oluşturmak](virtual-networks-create-vnet-classic-netcfg-ps.md).</span><span class="sxs-lookup"><span data-stu-id="3976c-114">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="3976c-115">Merhaba UDR hello ön uç alt ağ için oluşturma</span><span class="sxs-lookup"><span data-stu-id="3976c-115">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="3976c-116">toocreate hello yol tablosu ve yukarıdaki hello senaryoyu temel hello ön uç alt ağ için gereken rota hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="3976c-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="3976c-117">Komut toocreate aşağıdaki hello hello ön uç alt ağ için yol tablosu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3976c-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="3976c-118">Tüm giden trafiğe toohello arka uç alt ağ (192.168.2.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="3976c-118">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="3976c-119">Çalışma hello komutu tooassociate hello yol tablosu hello ile aşağıdaki **ön uç** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="3976c-119">Run hello following command tooassociate hello route table with hello **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="3976c-120">Merhaba UDR hello arka uç alt ağ için oluşturma</span><span class="sxs-lookup"><span data-stu-id="3976c-120">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="3976c-121">toocreate hello yol tablosu ve rota hello yedekleme için gerekli hello senaryoyu temel alt sonlandırmak için hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="3976c-121">toocreate hello route table and route needed for hello back end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="3976c-122">Komut toocreate aşağıdaki hello hello arka uç alt ağ için yol tablosu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3976c-122">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="3976c-123">Tüm giden trafiğe toohello ön uç alt ağı (192.168.1.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="3976c-123">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="3976c-124">Çalışma hello komutu tooassociate hello yol tablosu hello ile aşağıdaki **arka uç** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="3976c-124">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a><span data-ttu-id="3976c-125">Merhaba FW1 VM üzerinde IP iletimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="3976c-125">Enable IP forwarding on hello FW1 VM</span></span>

<span data-ttu-id="3976c-126">Merhaba FW1 VM, aşağıdaki adımları tam hello tooenable IP iletme:</span><span class="sxs-lookup"><span data-stu-id="3976c-126">tooenable IP forwarding in hello FW1 VM, complete hello following steps:</span></span>

1. <span data-ttu-id="3976c-127">Komut toocheck hello IP iletimini durumunu izleyen hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3976c-127">Run hello following command toocheck hello status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="3976c-128">Çalışma hello şu komutu tooenable IP iletme hello için *FW1* VM:</span><span class="sxs-lookup"><span data-stu-id="3976c-128">Run hello following command tooenable IP forwarding for hello *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
