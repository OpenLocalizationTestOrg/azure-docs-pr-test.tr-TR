---
title: "kullanarak aaaControl Yönlendirme ve sanal gereçler hello Azure CLI 1.0 | Microsoft Docs"
description: "Azure CLI 1.0 kullanarak toocontrol Yönlendirme ve sanal gereçler nasıl hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a><span data-ttu-id="cc07a-103">Kullanıcı tanımlı yolları (UDR) hello Azure CLI 1.0 kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc07a-103">Create User-Defined Routes (UDR) using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="cc07a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc07a-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="cc07a-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="cc07a-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="cc07a-106">Şablon</span><span class="sxs-lookup"><span data-stu-id="cc07a-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="cc07a-107">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="cc07a-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="cc07a-108">CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="cc07a-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="cc07a-109">Özel Yönlendirme ve sanal gereçler hello Azure CLI kullanarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc07a-109">Create custom routing and virtual appliances using hello Azure CLI.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="cc07a-110">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="cc07a-110">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="cc07a-111">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="cc07a-111">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="cc07a-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="cc07a-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="cc07a-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="cc07a-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="cc07a-114">Merhaba aşağıdaki örnek Azure CLI komutları zaten senaryosunda hello yukarıdaki göre oluşturulan basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="cc07a-114">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="cc07a-115">Bu belgede gösterildiği toorun hello komutları istiyorsanız, önce hello test ortamı dağıtarak yapı [bu şablonu](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), tıklatın **tooAzure dağıtmak**, hello varsayılan parametre değerlerini değiştirin Gerekirse ve izleme hello yönergelerinde portal hello durumunda.</span><span class="sxs-lookup"><span data-stu-id="cc07a-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="cc07a-116">Merhaba UDR hello ön uç alt ağ için oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc07a-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="cc07a-117">toocreate hello yol tablosu ve yukarıdaki hello senaryoyu temel hello ön uç alt ağ için gereken rota hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="cc07a-117">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="cc07a-118">Komut toocreate aşağıdaki hello hello ön uç alt ağ için yol tablosu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cc07a-118">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="cc07a-119">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cc07a-119">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    <span data-ttu-id="cc07a-120">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="cc07a-120">Parameters:</span></span>
   
   * <span data-ttu-id="cc07a-121">**-g (veya --resource-group)**.</span><span class="sxs-lookup"><span data-stu-id="cc07a-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="cc07a-122">Merhaba UDR oluşturulacağı hello kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="cc07a-122">Name of hello resource group where hello UDR will be created.</span></span> <span data-ttu-id="cc07a-123">Bizim senaryomuz için bu *TestRG* ’dir.</span><span class="sxs-lookup"><span data-stu-id="cc07a-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="cc07a-124">**-l (veya --location)**.</span><span class="sxs-lookup"><span data-stu-id="cc07a-124">**-l (or --location)**.</span></span> <span data-ttu-id="cc07a-125">Merhaba yeni UDR oluşturulacağı azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="cc07a-125">Azure region where hello new UDR will be created.</span></span> <span data-ttu-id="cc07a-126">Bizim senaryomuz için *westus*.</span><span class="sxs-lookup"><span data-stu-id="cc07a-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="cc07a-127">**-n (veya --name)**.</span><span class="sxs-lookup"><span data-stu-id="cc07a-127">**-n (or --name)**.</span></span> <span data-ttu-id="cc07a-128">Hello için ad yeni UDR.</span><span class="sxs-lookup"><span data-stu-id="cc07a-128">Name for hello new UDR.</span></span> <span data-ttu-id="cc07a-129">Bizim senaryomuz için *UDR ön uç*.</span><span class="sxs-lookup"><span data-stu-id="cc07a-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="cc07a-130">Tüm giden trafiğe toohello arka uç alt ağ (192.168.2.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="cc07a-130">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="cc07a-131">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cc07a-131">Output:</span></span>
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    <span data-ttu-id="cc07a-132">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="cc07a-132">Parameters:</span></span>
   
   * <span data-ttu-id="cc07a-133">**-r (veya--yol tablosu adı)**.</span><span class="sxs-lookup"><span data-stu-id="cc07a-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="cc07a-134">Merhaba rota ekleneceği hello yol tablosu adı.</span><span class="sxs-lookup"><span data-stu-id="cc07a-134">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="cc07a-135">Bizim senaryomuz için *UDR ön uç*.</span><span class="sxs-lookup"><span data-stu-id="cc07a-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="cc07a-136">**-a (veya--adres-önek)**.</span><span class="sxs-lookup"><span data-stu-id="cc07a-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="cc07a-137">Paketler için burada hedefleyen hello alt ağ adresi öneki.</span><span class="sxs-lookup"><span data-stu-id="cc07a-137">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="cc07a-138">Bizim senaryomuz için *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="cc07a-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="cc07a-139">**-y (veya--sonraki atlama türü)**.</span><span class="sxs-lookup"><span data-stu-id="cc07a-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="cc07a-140">Nesne trafik türü için gönderilir.</span><span class="sxs-lookup"><span data-stu-id="cc07a-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="cc07a-141">Olası değerler şunlardır: *değerinin VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, veya *hiçbiri*.</span><span class="sxs-lookup"><span data-stu-id="cc07a-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="cc07a-142">**-p (veya--sonraki atlama IP adresi**).</span><span class="sxs-lookup"><span data-stu-id="cc07a-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="cc07a-143">Sonraki atlama IP adresi.</span><span class="sxs-lookup"><span data-stu-id="cc07a-143">IP address for next hop.</span></span> <span data-ttu-id="cc07a-144">Bizim senaryomuz için *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="cc07a-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="cc07a-145">Çalışma hello şu komutu tooassociate hello yol tablosu ile Merhaba yukarıda oluşturduğunuz **ön uç** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="cc07a-145">Run hello following command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="cc07a-146">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cc07a-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    <span data-ttu-id="cc07a-147">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="cc07a-147">Parameters:</span></span>
   
   * <span data-ttu-id="cc07a-148">**-e (veya--vnet-ad)**.</span><span class="sxs-lookup"><span data-stu-id="cc07a-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="cc07a-149">Merhaba hello alt bulunduğu VNet adı.</span><span class="sxs-lookup"><span data-stu-id="cc07a-149">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="cc07a-150">Bizim senaryomuz için bu *TestVNet* ’tir.</span><span class="sxs-lookup"><span data-stu-id="cc07a-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="cc07a-151">Merhaba UDR hello arka uç alt ağ için oluşturma</span><span class="sxs-lookup"><span data-stu-id="cc07a-151">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="cc07a-152">toocreate hello yol tablosu ve yukarıdaki adımları izleyerek tam hello hello senaryoya göre hello arka uç alt ağ için gereken rota:</span><span class="sxs-lookup"><span data-stu-id="cc07a-152">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="cc07a-153">Komut toocreate aşağıdaki hello hello arka uç alt ağ için yol tablosu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cc07a-153">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="cc07a-154">Tüm giden trafiğe toohello ön uç alt ağı (192.168.1.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="cc07a-154">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="cc07a-155">Çalışma hello komutu tooassociate hello yol tablosu hello ile aşağıdaki **arka uç** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="cc07a-155">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="cc07a-156">FW1 üstünde IP iletimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="cc07a-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="cc07a-157">Merhaba tarafından kullanılan NIC tooenable IP iletme **FW1**tam hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="cc07a-157">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="cc07a-158">İzleyen ve dikkat edin hello değeri hello komutu çalıştırmak **etkinleştirmek IP iletimini**.</span><span class="sxs-lookup"><span data-stu-id="cc07a-158">Run hello command that follows and notice hello value for **Enable IP forwarding**.</span></span> <span data-ttu-id="cc07a-159">Çok ayarlanmalıdır*false*.</span><span class="sxs-lookup"><span data-stu-id="cc07a-159">It should be set too*false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="cc07a-160">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cc07a-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. <span data-ttu-id="cc07a-161">Komut tooenable IP iletimini aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="cc07a-161">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="cc07a-162">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cc07a-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    <span data-ttu-id="cc07a-163">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="cc07a-163">Parameters:</span></span>
   
   * <span data-ttu-id="cc07a-164">**-f (veya--etkinleştir IP İletimi)**.</span><span class="sxs-lookup"><span data-stu-id="cc07a-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="cc07a-165">*doğru* veya *false*.</span><span class="sxs-lookup"><span data-stu-id="cc07a-165">*true* or *false*.</span></span>

