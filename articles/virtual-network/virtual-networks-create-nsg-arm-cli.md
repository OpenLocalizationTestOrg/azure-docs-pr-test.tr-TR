---
title: "Azure CLI 2.0 aaaCreate ağ güvenlik grupları - | Microsoft Docs"
description: "Bilgi nasıl toocreate ve ağ güvenlik grupları hello Azure CLI 2.0 kullanarak dağıtın."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9ea82c09-f4a6-4268-88bc-fc439db40c48
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 30b1d60676331bf5e2bbbb046c747477be9d3338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a><span data-ttu-id="86152-103">Ağ güvenlik grupları hello Azure CLI 2.0 kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="86152-103">Create network security groups using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="86152-104">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="86152-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="86152-105">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="86152-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="86152-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için</span><span class="sxs-lookup"><span data-stu-id="86152-106">[Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="86152-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -bizim gelecek nesil CLI hello kaynak yönetimi dağıtım modeli (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="86152-107">[Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="86152-108">Merhaba örnek Azure CLI 2.0 zaten senaryosunda hello önceki göre oluşturulan basit bir ortam aşağıdaki beklediğiniz komutları.</span><span class="sxs-lookup"><span data-stu-id="86152-108">hello sample Azure CLI 2.0 commands following expect a simple environment already created based on hello scenario preceding.</span></span> 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a><span data-ttu-id="86152-109">Merhaba Merhaba NSG oluşturma `FrontEnd` alt ağ</span><span class="sxs-lookup"><span data-stu-id="86152-109">Create hello NSG for hello `FrontEnd` subnet</span></span>

<span data-ttu-id="86152-110">toocreate adlı bir NSG *NSG ön uç* senaryosunda hello önceki bağlı olarak, hello adımları aşağıdaki izleyin.</span><span class="sxs-lookup"><span data-stu-id="86152-110">toocreate an NSG named *NSG-FrontEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="86152-111">Henüz henüz, yüklemek ve hello son yapılandırırsanız [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="86152-111">If you haven't yet, install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span> 

2. <span data-ttu-id="86152-112">Hello kullanarak bir NSG oluşturma [az ağ nsg oluşturma](/cli/azure/network/nsg#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="86152-112">Create an NSG using hello [az network nsg create](/cli/azure/network/nsg#create) command.</span></span> 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    <span data-ttu-id="86152-113">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="86152-113">Parameters:</span></span>
   
   * <span data-ttu-id="86152-114">`--resource-group`: Merhaba NSG oluşturulduğu hello kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="86152-114">`--resource-group`: Name of hello resource group where hello NSG is created.</span></span> <span data-ttu-id="86152-115">Bizim senaryomuz için bu *TestRG* ’dir.</span><span class="sxs-lookup"><span data-stu-id="86152-115">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="86152-116">`--location`: Merhaba yeni NSG oluşturulduğu azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="86152-116">`--location`: Azure region where hello new NSG is created.</span></span> <span data-ttu-id="86152-117">Bizim senaryomuz için *westus*.</span><span class="sxs-lookup"><span data-stu-id="86152-117">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="86152-118">`--name`: Hello için ad yeni NSG.</span><span class="sxs-lookup"><span data-stu-id="86152-118">`--name`: Name for hello new NSG.</span></span> <span data-ttu-id="86152-119">Bizim senaryomuz için *NSG ön uç*.</span><span class="sxs-lookup"><span data-stu-id="86152-119">For our scenario, *NSG-FrontEnd*.</span></span>

    <span data-ttu-id="86152-120">Merhaba çıkış oldukça bit tüm hello varsayılan kuralları listesi dahil olmak üzere bilgilerinin beklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="86152-120">hello expected output is quite a bit of information including a list of all hello default rules.</span></span> <span data-ttu-id="86152-121">Merhaba aşağıdaki örnekte bir JMESPATH sorgu Filtresi ile hello kullanarak hello varsayılan kuralları gösterir `table` çıktı biçimi:</span><span class="sxs-lookup"><span data-stu-id="86152-121">hello following example shows hello default rules using a JMESPATH query filter with hello `table` output format:</span></span>

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   <span data-ttu-id="86152-122">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="86152-122">Output:</span></span>

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. <span data-ttu-id="86152-123">Merhaba Internet hello ile gelen erişim tooport 3389 (RDP) sağlayan bir kural oluşturmak [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="86152-123">Create a rule that allows access tooport 3389 (RDP) from hello Internet with hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86152-124">Kullanmakta olduğunuz hello Kabuk bağlı olarak toomodify hello gerekebilecek `*` hello bağımsız şekilde olarak tooexpand hello bağımsız değişkeni değil yürütmeden önce aşağıdaki karakter.</span><span class="sxs-lookup"><span data-stu-id="86152-124">Depending on hello shell you are using, you might need toomodify hello `*` character in hello arguments following so as not tooexpand hello argument before execution.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name rdp-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 3389
    ```
   
    <span data-ttu-id="86152-125">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="86152-125">Expected output:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "3389",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule",
        "name": "rdp-rule",
        "priority": 100,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

    <span data-ttu-id="86152-126">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="86152-126">Parameters:</span></span>

    * <span data-ttu-id="86152-127">`--resource-group testrg`: kaynak grubu toouse hello.</span><span class="sxs-lookup"><span data-stu-id="86152-127">`--resource-group testrg`: hello resource group toouse.</span></span> <span data-ttu-id="86152-128">Büyük küçük harf duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="86152-128">Note that it is case-insensitive.</span></span>
    * <span data-ttu-id="86152-129">`--nsg-name NSG-FrontEnd`: Hangi hello kural oluşturulur hello NSG adı.</span><span class="sxs-lookup"><span data-stu-id="86152-129">`--nsg-name NSG-FrontEnd`: Name of hello NSG in which hello rule is created.</span></span>
    * <span data-ttu-id="86152-130">`--name rdp-rule`: Hello yeni kural adı.</span><span class="sxs-lookup"><span data-stu-id="86152-130">`--name rdp-rule`: Name for hello new rule.</span></span>
    * <span data-ttu-id="86152-131">`--access Allow`: Erişim düzeyi hello kuralın (Engelle veya izin ver).</span><span class="sxs-lookup"><span data-stu-id="86152-131">`--access Allow`: Access level for hello rule (Deny or Allow).</span></span>
    * <span data-ttu-id="86152-132">`--protocol Tcp`: Protokolü (Tcp, Udp veya *).</span><span class="sxs-lookup"><span data-stu-id="86152-132">`--protocol Tcp`: Protocol (Tcp, Udp, or *).</span></span>
    * <span data-ttu-id="86152-133">`--direction Inbound`: Hello bağlantısı (gelen veya giden) yönü.</span><span class="sxs-lookup"><span data-stu-id="86152-133">`--direction Inbound`: Direction of hello connection (Inbound or Outbound).</span></span>
    * <span data-ttu-id="86152-134">`--priority 100`: Hello kuralı için öncelik.</span><span class="sxs-lookup"><span data-stu-id="86152-134">`--priority 100`: Priority for hello rule.</span></span>
    * <span data-ttu-id="86152-135">`--source-address-prefix Internet`: CIDR veya varsayılan etiketleri kullanılarak kaynak adres ön eki.</span><span class="sxs-lookup"><span data-stu-id="86152-135">`--source-address-prefix Internet`: Source address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="86152-136">`--source-port-range "*"`: Bağlantı noktası veya bağlantı noktası aralığı kaynağı.</span><span class="sxs-lookup"><span data-stu-id="86152-136">`--source-port-range "*"`: Source port or port range.</span></span> <span data-ttu-id="86152-137">Merhaba bağlantı açılan bağlantı.</span><span class="sxs-lookup"><span data-stu-id="86152-137">Port that opened hello connection.</span></span>
    * <span data-ttu-id="86152-138">`--destination-address-prefix "*"`: CIDR veya varsayılan etiketleri kullanılarak hedef adres ön eki.</span><span class="sxs-lookup"><span data-stu-id="86152-138">`--destination-address-prefix "*"`: Destination address prefix in CIDR or using default tags.</span></span>
    * <span data-ttu-id="86152-139">`--destination-port-range 3389`: Hedef bağlantı noktası veya bağlantı noktası aralığı.</span><span class="sxs-lookup"><span data-stu-id="86152-139">`--destination-port-range 3389`: Destination port or port range.</span></span> <span data-ttu-id="86152-140">Merhaba bağlantı isteğini alan bağlantı.</span><span class="sxs-lookup"><span data-stu-id="86152-140">Port that receives hello connection request.</span></span>



4. <span data-ttu-id="86152-141">Merhaba Internet gelen erişim tooport 80 (HTTP) sağlayan bir kural oluşturmak **az ağ nsg kuralını** komutu.</span><span class="sxs-lookup"><span data-stu-id="86152-141">Create a rule that allows access tooport 80 (HTTP) from hello Internet **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-FrontEnd \
    --name web-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 200 \
    --source-address-prefix Internet \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 80
    ```
   
    <span data-ttu-id="86152-142">Beklenen putput:</span><span class="sxs-lookup"><span data-stu-id="86152-142">Expected putput:</span></span>
   
    ```json
    {
        "access": "Allow",
        "description": null,
        "destinationAddressPrefix": "*",
        "destinationPortRange": "80",
        "direction": "Inbound",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule",
        "name": "web-rule",
        "priority": 200,
        "protocol": "Tcp",
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "sourceAddressPrefix": "Internet",
        "sourcePortRange": "*"
    }
    ```

5. <span data-ttu-id="86152-143">Merhaba NSG toohello bağlamak **ön uç** alt ağ ile Merhaba [az ağ sanal ağ alt ağı güncelleştirme](/cli/azure/network/vnet/subnet#update) komutu.</span><span class="sxs-lookup"><span data-stu-id="86152-143">Bind hello NSG toohello **FrontEnd** subnet with hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command.</span></span>
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    <span data-ttu-id="86152-144">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="86152-144">Expected output:</span></span>
   
    ```json
    {
        "addressPrefix": "192.168.1.0/24",
        "etag": "W/\"<guid>\"",
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/FrontEnd",
        "ipConfigurations": [
            {
            "etag": null,
            "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
            "name": null,
            "privateIpAddress": null,
            "privateIpAllocationMethod": null,
            "provisioningState": null,
            "publicIpAddress": null,
            "resourceGroup": "TestRG",
            "subnet": null
            }
        ],
        "name": "FrontEnd",
        "networkSecurityGroup": {
            "defaultSecurityRules": null,
            "etag": null,
            "id": "/subscriptions/<guid>f/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd",
            "location": null,
            "name": null,
            "networkInterfaces": null,
            "provisioningState": null,
            "resourceGroup": "testrg",
            "resourceGuid": null,
            "securityRules": null,
            "subnets": null,
            "tags": null,
            "type": null
        },
        "provisioningState": "Succeeded",
        "resourceGroup": "testrg",
        "resourceNavigationLinks": null,
        "routeTable": null
    }
    ```

## <a name="create-hello-nsg-for-hello-backend-subnet"></a><span data-ttu-id="86152-145">Merhaba Merhaba NSG oluşturma `BackEnd` alt ağ</span><span class="sxs-lookup"><span data-stu-id="86152-145">Create hello NSG for hello `BackEnd` subnet</span></span>
<span data-ttu-id="86152-146">toocreate adlı bir NSG *NSG arka uç* senaryosunda hello önceki bağlı olarak, hello adımları aşağıdaki izleyin.</span><span class="sxs-lookup"><span data-stu-id="86152-146">toocreate an NSG named *NSG-BackEnd* based on hello scenario preceding, follow hello steps following.</span></span>

1. <span data-ttu-id="86152-147">Merhaba oluşturma `NSG-BackEnd` NSG ile **az ağ nsg oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="86152-147">Create hello `NSG-BackEnd` NSG with **az network nsg create**.</span></span>
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    <span data-ttu-id="86152-148">Adım 2, önceki, olduğu gibi hello çıkış varsayılan kuralları da dahil olmak üzere oldukça büyük beklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="86152-148">As in step 2, preceding, hello expected output is quite large, including default rules.</span></span>
   
2. <span data-ttu-id="86152-149">Merhaba gelen erişim tooport 1433 (SQL) sağlayan bir kural oluşturmak `FrontEnd` alt ağ ile Merhaba **az ağ nsg kuralını** komutu.</span><span class="sxs-lookup"><span data-stu-id="86152-149">Create a rule that allows access tooport 1433 (SQL) from hello `FrontEnd` subnet with hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name sql-rule \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix 192.168.1.0/24 \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range 1433
    ```
   
    <span data-ttu-id="86152-150">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="86152-150">Expected output:</span></span>

    ```json  
    {
    "access": "Allow",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "1433",
    "direction": "Inbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule",
    "name": "sql-rule",
    "priority": 100,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "192.168.1.0/24",
    "sourcePortRange": "*"
    }
    ```

3. <span data-ttu-id="86152-151">Kullanarak toohello Internet erişimini engelleyen bir kural oluşturmak hello **az ağ nsg kuralını** komutu.</span><span class="sxs-lookup"><span data-stu-id="86152-151">Create a rule that denies access toohello Internet using hello **az network nsg rule create** command.</span></span>
   
    ```azurecli
    az network nsg rule create \
    --resource-group testrg \
    --nsg-name NSG-BackEnd \
    --name web-rule \
    --access Deny \
    --protocol Tcp  \
    --direction Outbound  \
    --priority 200 \
    --source-address-prefix "*" \
    --source-port-range "*" \
    --destination-address-prefix "*" \
    --destination-port-range "*"
    ```
   
    <span data-ttu-id="86152-152">Beklenen putput:</span><span class="sxs-lookup"><span data-stu-id="86152-152">Expected putput:</span></span>
   
    ```json
    {
    "access": "Deny",
    "description": null,
    "destinationAddressPrefix": "*",
    "destinationPortRange": "*",
    "direction": "Outbound",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/web-rule",
    "name": "web-rule",
    "priority": 200,
    "protocol": "Tcp",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "sourceAddressPrefix": "*",
    "sourcePortRange": "*"
    }
    ```

4. <span data-ttu-id="86152-153">Merhaba NSG toohello bağlamak `BackEnd` hello kullanarak alt **az ağ sanal alt ağ kümesi** komutu.</span><span class="sxs-lookup"><span data-stu-id="86152-153">Bind hello NSG toohello `BackEnd` subnet using hello **az network vnet subnet set** command.</span></span>
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    <span data-ttu-id="86152-154">Beklenen çıktı:</span><span class="sxs-lookup"><span data-stu-id="86152-154">Expected output:</span></span>
   
    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/TestVNET/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": {
        "defaultSecurityRules": null,
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "location": null,
        "name": null,
        "networkInterfaces": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "resourceGuid": null,
        "securityRules": null,
        "subnets": null,
        "tags": null,
        "type": null
    },
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```
