---
title: "bir Azure Virtual Network - CLI - Klasik aaaControl yönlendirme | Microsoft Docs"
description: "Nasıl Azure CLI kullanarak Vnet içinde yönlendirme toocontrol hello Klasik dağıtım modelinde hello öğrenin"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a><span data-ttu-id="90eff-103">Denetim Yönlendirme ve sanal gereçler (Klasik) kullanarak Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="90eff-103">Control routing and use virtual appliances (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="90eff-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90eff-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="90eff-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="90eff-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="90eff-106">Şablon</span><span class="sxs-lookup"><span data-stu-id="90eff-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="90eff-107">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="90eff-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="90eff-108">CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="90eff-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="90eff-109">Bu makalede, hello Klasik dağıtım modeli yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="90eff-109">This article covers hello classic deployment model.</span></span> <span data-ttu-id="90eff-110">Ayrıca [kontrol Yönlendirme ve hello Resource Manager dağıtım modelinde sanal gereçler kullanma](virtual-network-create-udr-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="90eff-110">You can also [control routing and use virtual appliances in hello Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="90eff-111">Merhaba aşağıdaki örnek Azure CLI komutları zaten senaryosunda hello yukarıdaki göre oluşturulan basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="90eff-111">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="90eff-112">Bu belgede gösterildiği toorun hello komutları istiyorsanız, gösterildiği hello ortamı oluşturmak [hello Azure CLI kullanarak VNet (Klasik) oluşturma](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="90eff-112">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="90eff-113">Merhaba UDR hello ön uç alt ağ için oluşturma</span><span class="sxs-lookup"><span data-stu-id="90eff-113">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="90eff-114">toocreate hello yol tablosu ve yukarıdaki hello senaryoyu temel hello ön uç alt ağ için gereken rota hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="90eff-114">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="90eff-115">Komut tooswitch tooclassic modu aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="90eff-115">Run hello following command tooswitch tooclassic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="90eff-116">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="90eff-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="90eff-117">Komut toocreate aşağıdaki hello hello ön uç alt ağ için yol tablosu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="90eff-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="90eff-118">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="90eff-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="90eff-119">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="90eff-119">Parameters:</span></span>
   
   * <span data-ttu-id="90eff-120">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="90eff-120">**-l (or --location)**.</span></span> <span data-ttu-id="90eff-121">Merhaba yeni NSG oluşturulacağı azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="90eff-121">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="90eff-122">Bizim senaryomuz için *westus*.</span><span class="sxs-lookup"><span data-stu-id="90eff-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="90eff-123">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="90eff-123">**-n (or --name)**.</span></span> <span data-ttu-id="90eff-124">Hello için ad yeni NSG.</span><span class="sxs-lookup"><span data-stu-id="90eff-124">Name for hello new NSG.</span></span> <span data-ttu-id="90eff-125">Bizim senaryomuz için *NSG ön uç*.</span><span class="sxs-lookup"><span data-stu-id="90eff-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="90eff-126">Tüm giden trafiğe toohello arka uç alt ağ (192.168.2.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="90eff-126">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="90eff-127">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="90eff-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="90eff-128">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="90eff-128">Parameters:</span></span>
   
   * <span data-ttu-id="90eff-129">**-r (veya--yol tablosu adı)**.</span><span class="sxs-lookup"><span data-stu-id="90eff-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="90eff-130">Merhaba rota ekleneceği hello yol tablosu adı.</span><span class="sxs-lookup"><span data-stu-id="90eff-130">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="90eff-131">Bizim senaryomuz için *UDR ön uç*.</span><span class="sxs-lookup"><span data-stu-id="90eff-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="90eff-132">**-a (veya--adres-önek)**.</span><span class="sxs-lookup"><span data-stu-id="90eff-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="90eff-133">Paketler için burada hedefleyen hello alt ağ adresi öneki.</span><span class="sxs-lookup"><span data-stu-id="90eff-133">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="90eff-134">Bizim senaryomuz için *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="90eff-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="90eff-135">**-t (veya--sonraki atlama türü)**.</span><span class="sxs-lookup"><span data-stu-id="90eff-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="90eff-136">Nesne trafik türü için gönderilir.</span><span class="sxs-lookup"><span data-stu-id="90eff-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="90eff-137">Olası değerler şunlardır: *değerinin VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, veya *hiçbiri*.</span><span class="sxs-lookup"><span data-stu-id="90eff-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="90eff-138">**-p (veya--sonraki atlama IP adresi**).</span><span class="sxs-lookup"><span data-stu-id="90eff-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="90eff-139">Sonraki atlama IP adresi.</span><span class="sxs-lookup"><span data-stu-id="90eff-139">IP address for next hop.</span></span> <span data-ttu-id="90eff-140">Bizim senaryomuz için *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="90eff-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="90eff-141">Çalışma hello şu komutu tooassociate hello yol tablosu ile Merhaba oluşturulan **ön uç** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="90eff-141">Run hello following command tooassociate hello route table created with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="90eff-142">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="90eff-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="90eff-143">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="90eff-143">Parameters:</span></span>
   
   * <span data-ttu-id="90eff-144">**-t (veya--vnet-ad)**.</span><span class="sxs-lookup"><span data-stu-id="90eff-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="90eff-145">Merhaba hello alt bulunduğu VNet adı.</span><span class="sxs-lookup"><span data-stu-id="90eff-145">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="90eff-146">Bizim senaryomuz için bu *TestVNet* ’tir.</span><span class="sxs-lookup"><span data-stu-id="90eff-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="90eff-147">**-n (veya--alt ağ adı**.</span><span class="sxs-lookup"><span data-stu-id="90eff-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="90eff-148">Merhaba alt hello yol tablosu adı eklenir.</span><span class="sxs-lookup"><span data-stu-id="90eff-148">Name of hello subnet hello route table will be added to.</span></span> <span data-ttu-id="90eff-149">Bizim senaryomuz için bu *FrontEnd* ’dir.</span><span class="sxs-lookup"><span data-stu-id="90eff-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="90eff-150">Merhaba UDR hello arka uç alt ağ için oluşturma</span><span class="sxs-lookup"><span data-stu-id="90eff-150">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="90eff-151">toocreate hello yol tablosu ve hello senaryo, aşağıdaki adımları tam hello hello arka uç alt ağ için gereken yolu:</span><span class="sxs-lookup"><span data-stu-id="90eff-151">toocreate hello route table and route needed for hello back-end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="90eff-152">Komut toocreate aşağıdaki hello hello arka uç alt ağ için yol tablosu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="90eff-152">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="90eff-153">Tüm giden trafiğe toohello ön uç alt ağı (192.168.1.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="90eff-153">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="90eff-154">Çalışma hello komutu tooassociate hello yol tablosu hello ile aşağıdaki **arka uç** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="90eff-154">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

