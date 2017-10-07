---
title: "kullanarak aaaControl Yönlendirme ve sanal gereçler hello Azure CLI 2.0 | Microsoft Docs"
description: "Azure CLI 2.0 kullanarak toocontrol Yönlendirme ve sanal gereçler nasıl hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a><span data-ttu-id="f1e4c-103">Kullanıcı tanımlı yolları (UDR) hello Azure CLI 2.0 kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1e4c-103">Create User-Defined Routes (UDR) using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f1e4c-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1e4c-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="f1e4c-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f1e4c-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="f1e4c-106">Şablon</span><span class="sxs-lookup"><span data-stu-id="f1e4c-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="f1e4c-107">PowerShell (Klasik dağıtımı)</span><span class="sxs-lookup"><span data-stu-id="f1e4c-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="f1e4c-108">CLI (Klasik dağıtımı)</span><span class="sxs-lookup"><span data-stu-id="f1e4c-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="f1e4c-109">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="f1e4c-109">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="f1e4c-110">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-110">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="f1e4c-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için</span><span class="sxs-lookup"><span data-stu-id="f1e4c-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="f1e4c-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -bizim gelecek nesil CLI hello kaynak yönetimi dağıtım modeli (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="f1e4c-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="f1e4c-113">Merhaba aşağıdaki örnek Azure CLI komutları zaten senaryosunda hello yukarıdaki göre oluşturulan basit bir ortam bekler.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-113">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="f1e4c-114">Bu belgede gösterildiği toorun hello komutları istiyorsanız, önce hello test ortamı dağıtarak yapı [bu şablonu](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), tıklatın **tooAzure dağıtmak**, hello varsayılan parametre değerlerini değiştirin Gerekirse ve izleme hello yönergelerinde portal hello durumunda.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-114">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="f1e4c-115">Merhaba UDR hello ön uç alt ağ için oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1e4c-115">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="f1e4c-116">toocreate hello yol tablosu ve yukarıdaki hello senaryoyu temel hello ön uç alt ağ için gereken rota hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="f1e4c-117">Merhaba ile Merhaba ön uç alt ağ için bir yol tablosu oluşturmanız [az ağ yol tablosu oluşturmanız](/cli/azure/network/route-table#create) komutu:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-117">Create a route table for hello front-end subnet with hello [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="f1e4c-118">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-118">Output:</span></span>

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. <span data-ttu-id="f1e4c-119">Tüm giden trafiğe toohello arka uç alt ağ (192.168.2.0/24) toohello gönderir bir yol oluşturma **FW1** hello kullanarak VM (192.168.0.4) [az ağ yol tablosu yol oluşturma](/cli/azure/network/route-table/route#create) komutu:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-119">Create a route that sends all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) using hello [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="f1e4c-120">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-120">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    <span data-ttu-id="f1e4c-121">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-121">Parameters:</span></span>

    * <span data-ttu-id="f1e4c-122">**--yol tablosu adı**.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-122">**--route-table-name**.</span></span> <span data-ttu-id="f1e4c-123">Merhaba rota ekleneceği hello yol tablosu adı.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-123">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="f1e4c-124">Bizim senaryomuz için *UDR ön uç*.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="f1e4c-125">**--Adres-önek**.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-125">**--address-prefix**.</span></span> <span data-ttu-id="f1e4c-126">Paketler için burada hedefleyen hello alt ağ adresi öneki.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-126">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="f1e4c-127">Bizim senaryomuz için *192.168.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="f1e4c-128">**--sonraki atlama türü**.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-128">**--next-hop-type**.</span></span> <span data-ttu-id="f1e4c-129">Nesne trafik türü için gönderilir.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="f1e4c-130">Olası değerler şunlardır: *değerinin VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, veya *hiçbiri*.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="f1e4c-131">**--sonraki atlama IP adresi**.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="f1e4c-132">Sonraki atlama IP adresi.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-132">IP address for next hop.</span></span> <span data-ttu-id="f1e4c-133">Bizim senaryomuz için *192.168.0.4*.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="f1e4c-134">Merhaba çalıştırmak [az ağ sanal ağ alt ağı güncelleştirme](/cli/azure/network/vnet/subnet#update) komutu tooassociate hello yol tablosu ile Merhaba yukarıda oluşturulan **ön uç** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-134">Run hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="f1e4c-135">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-135">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    <span data-ttu-id="f1e4c-136">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-136">Parameters:</span></span>
    
    * <span data-ttu-id="f1e4c-137">**--vnet-ad**.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-137">**--vnet-name**.</span></span> <span data-ttu-id="f1e4c-138">Merhaba hello alt bulunduğu VNet adı.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-138">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="f1e4c-139">Bizim senaryomuz için bu *TestVNet* ’tir.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="f1e4c-140">Merhaba UDR hello arka uç alt ağ için oluşturma</span><span class="sxs-lookup"><span data-stu-id="f1e4c-140">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="f1e4c-141">toocreate hello yol tablosu ve yukarıdaki adımları izleyerek tam hello hello senaryoya göre hello arka uç alt ağ için gereken rota:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-141">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="f1e4c-142">Komut toocreate aşağıdaki hello hello arka uç alt ağ için yol tablosu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-142">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="f1e4c-143">Tüm giden trafiğe toohello ön uç alt ağı (192.168.1.0/24) toohello komutu toocreate hello rota tablosu toosend rotadaki aşağıdaki hello çalıştırmak **FW1** VM (192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="f1e4c-143">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="f1e4c-144">Çalışma hello komutu tooassociate hello yol tablosu hello ile aşağıdaki **arka uç** alt ağ:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-144">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="f1e4c-145">FW1 üstünde IP iletimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f1e4c-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="f1e4c-146">Merhaba tarafından kullanılan NIC tooenable IP iletme **FW1**tam hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-146">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="f1e4c-147">Merhaba çalıştırmak [az ağ NIC Göster](/cli/azure/network/nic#show) bir JMESPATH filtre toodisplay hello geçerli komutunu **etkinleştir IP iletimini** değerini **etkinleştirmek IP iletimini**.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-147">Run hello [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter toodisplay hello current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="f1e4c-148">Çok ayarlanmalıdır*false*.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-148">It should be set too*false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="f1e4c-149">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-149">Output:</span></span>

        false

2. <span data-ttu-id="f1e4c-150">Komut tooenable IP iletimini aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-150">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="f1e4c-151">Merhaba çıkış akış toohello konsol incelemek veya yalnızca hello belirli yeniden sınayın **enableIpForwarding** değeri:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-151">You can examine hello output streamed toohello console, or just retest for hello specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="f1e4c-152">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-152">Output:</span></span>

        true

    <span data-ttu-id="f1e4c-153">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="f1e4c-153">Parameters:</span></span>

    <span data-ttu-id="f1e4c-154">**--IP iletimini**: *true* veya *false*.</span><span class="sxs-lookup"><span data-stu-id="f1e4c-154">**--ip-forwarding**: *true* or *false*.</span></span>

