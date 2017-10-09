---
title: "sanal ağ - Azure CLI 2.0 aaaCreate | Microsoft Docs"
description: "Azure CLI 2.0 kullanarak bir sanal ağ toocreate hello nasıl öğrenin."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a><span data-ttu-id="7753a-103">Hello Azure CLI 2.0 kullanarak bir sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="7753a-103">Create a virtual network using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="7753a-104">Azure'un iki dağıtım modeli vardır: Azure Resource Manager ve klasik.</span><span class="sxs-lookup"><span data-stu-id="7753a-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="7753a-105">Microsoft, kaynakları hello Resource Manager dağıtım modeli üzerinden oluşturma önerir.</span><span class="sxs-lookup"><span data-stu-id="7753a-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="7753a-106">Merhaba iki modelleri arasındaki farklar hakkında daha fazla bilgi toolearn hello okuma hello [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7753a-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="7753a-107">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="7753a-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="7753a-108">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="7753a-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="7753a-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için</span><span class="sxs-lookup"><span data-stu-id="7753a-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="7753a-110">[Azure CLI 2.0](#create-a-virtual-network) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli (Bu makalede) için '</span><span class="sxs-lookup"><span data-stu-id="7753a-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for hello resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="7753a-111">Ayrıca, bir VNet kaynak diğer araçları kullanarak Yöneticisi aracılığıyla oluşturabilir veya liste aşağıdaki hello farklı bir seçeneği seçerek hello Klasik dağıtım modeli üzerinden bir VNet oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7753a-111">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7753a-112">Portal</span><span class="sxs-lookup"><span data-stu-id="7753a-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="7753a-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7753a-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="7753a-114">CLI</span><span class="sxs-lookup"><span data-stu-id="7753a-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="7753a-115">Şablon</span><span class="sxs-lookup"><span data-stu-id="7753a-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="7753a-116">Portal (Klasik)</span><span class="sxs-lookup"><span data-stu-id="7753a-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="7753a-117">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="7753a-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="7753a-118">CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="7753a-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="7753a-119">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="7753a-119">Create a virtual network</span></span>

<span data-ttu-id="7753a-120">kullanarak bir sanal ağ toocreate Azure CLI 2.0, aşağıdaki adımları tam hello hello:</span><span class="sxs-lookup"><span data-stu-id="7753a-120">toocreate a virtual network using hello Azure CLI 2.0, complete hello following steps:</span></span>

1. <span data-ttu-id="7753a-121">Merhaba son yükleyip [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="7753a-121">Install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="7753a-122">Hello kullanarak VNet için bir kaynak grubu oluşturmak [az grubu oluşturma](/cli/azure/group#create) hello komutunu `--name` ve `--location` bağımsız değişkenler:</span><span class="sxs-lookup"><span data-stu-id="7753a-122">Create a resource group for your VNet using hello [az group create](/cli/azure/group#create) command with hello `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="7753a-123">VNet ve bir alt ağ oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7753a-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="7753a-124">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="7753a-124">Expected output:</span></span>
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    <span data-ttu-id="7753a-125">Kullanılan parametreler:</span><span class="sxs-lookup"><span data-stu-id="7753a-125">Parameters used:</span></span>

    - <span data-ttu-id="7753a-126">`--name TestVNet`: Merhaba VNet toobe oluşturulan adı.</span><span class="sxs-lookup"><span data-stu-id="7753a-126">`--name TestVNet`: Name of hello VNet toobe created.</span></span>
    - <span data-ttu-id="7753a-127">`--resource-group TestRG`: hello kaynağı denetleyen # hello kaynak grubu adı.</span><span class="sxs-lookup"><span data-stu-id="7753a-127">`--resource-group TestRG`: # hello resource group name that controls hello resource.</span></span> 
    - <span data-ttu-id="7753a-128">`--location centralus`: Merhaba hangi toodeploy konumuna.</span><span class="sxs-lookup"><span data-stu-id="7753a-128">`--location centralus`: hello location into which toodeploy.</span></span>
    - <span data-ttu-id="7753a-129">`--address-prefix 192.168.0.0/16`: Merhaba adres öneki ve blok.</span><span class="sxs-lookup"><span data-stu-id="7753a-129">`--address-prefix 192.168.0.0/16`: hello address prefix and block.</span></span>  
    - <span data-ttu-id="7753a-130">`--subnet-name FrontEnd`: hello alt hello adı.</span><span class="sxs-lookup"><span data-stu-id="7753a-130">`--subnet-name FrontEnd`: hello name of hello subnet.</span></span>
    - <span data-ttu-id="7753a-131">`--subnet-prefix 192.168.1.0/24`: Merhaba adres öneki ve blok.</span><span class="sxs-lookup"><span data-stu-id="7753a-131">`--subnet-prefix 192.168.1.0/24`: hello address prefix and block.</span></span>

    <span data-ttu-id="7753a-132">toolist hello temel bilgileri toouse hello içinde sonraki komutunu hello VNet kullanarak sorgulayabilir bir [sorgu filtresi](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="7753a-132">toolist hello basic information toouse in hello next command, you can query hello VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="7753a-133">Hangi çıktı aşağıdaki hello üretir:</span><span class="sxs-lookup"><span data-stu-id="7753a-133">Which produces hello following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="7753a-134">Bir alt ağ oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7753a-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="7753a-135">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="7753a-135">Expected output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    <span data-ttu-id="7753a-136">Kullanılan parametreler:</span><span class="sxs-lookup"><span data-stu-id="7753a-136">Parameters used:</span></span>

    - <span data-ttu-id="7753a-137">`--address-prefix 192.168.2.0/24`: Alt ağ CIDR bloğu.</span><span class="sxs-lookup"><span data-stu-id="7753a-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="7753a-138">`--name BackEnd`: Hello yeni alt ağ adı.</span><span class="sxs-lookup"><span data-stu-id="7753a-138">`--name BackEnd`: Name of hello new subnet.</span></span>
    - <span data-ttu-id="7753a-139">`--resource-group TestRG`: hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="7753a-139">`--resource-group TestRG`: hello resource group.</span></span>
    - <span data-ttu-id="7753a-140">`--vnet-name TestVNet`: VNet sorumlu hello hello adı.</span><span class="sxs-lookup"><span data-stu-id="7753a-140">`--vnet-name TestVNet`: hello name of hello owning VNet.</span></span>

5. <span data-ttu-id="7753a-141">Sorgu hello özelliklerini yeni VNet hello:</span><span class="sxs-lookup"><span data-stu-id="7753a-141">Query hello properties of hello new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="7753a-142">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="7753a-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="7753a-143">Merhaba alt sorgu hello özellikleri:</span><span class="sxs-lookup"><span data-stu-id="7753a-143">Query hello properties of hello subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="7753a-144">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="7753a-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="7753a-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7753a-145">Next steps</span></span>

<span data-ttu-id="7753a-146">Bilgi nasıl tooconnect:</span><span class="sxs-lookup"><span data-stu-id="7753a-146">Learn how tooconnect:</span></span>

- <span data-ttu-id="7753a-147">Merhaba okuyarak sanal makine (VM) tooa sanal ağ [bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7753a-147">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="7753a-148">Merhaba makaleleri hello adımlarda bir VNet ve alt ağ oluşturmak yerine, bir VM'ye mevcut VNet ve alt ağ tooconnect seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7753a-148">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="7753a-149">sanal ağ tooother sanal ağlar hello okuyarak hello [sanal ağlara bağlanma](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7753a-149">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="7753a-150">bir siteden siteye sanal özel ağ (VPN) veya expressroute bağlantı hattı kullanarak hello sanal ağ tooan şirket içi ağ.</span><span class="sxs-lookup"><span data-stu-id="7753a-150">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="7753a-151">Bilgi hello okuyarak nasıl [bir siteden siteye VPN kullanarak bir VNet tooan şirket içi ağ bağlanmak](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) ve [VNet tooan expressroute bağlantı hattı bağlantı](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7753a-151">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
