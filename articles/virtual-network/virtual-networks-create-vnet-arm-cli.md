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
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a>Hello Azure CLI 2.0 kullanarak bir sanal ağ oluşturma

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure'un iki dağıtım modeli vardır: Azure Resource Manager ve klasik. Microsoft, kaynakları hello Resource Manager dağıtım modeli üzerinden oluşturma önerir. Merhaba iki modelleri arasındaki farklar hakkında daha fazla bilgi toolearn hello okuma hello [anlamak Azure dağıtım modelleri](../azure-resource-manager/resource-manager-deployment-model.md) makalesi.

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- [Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için
- [Azure CLI 2.0](#create-a-virtual-network) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli (Bu makalede) için '
 
    Ayrıca, bir VNet kaynak diğer araçları kullanarak Yöneticisi aracılığıyla oluşturabilir veya liste aşağıdaki hello farklı bir seçeneği seçerek hello Klasik dağıtım modeli üzerinden bir VNet oluşturun:

> [!div class="op_single_selector"]
> * [Portal](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [Şablon](virtual-networks-create-vnet-arm-template-click.md)
> * [Portal (Klasik)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (Klasik)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [CLI (Klasik)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a>Sanal ağ oluşturma

kullanarak bir sanal ağ toocreate Azure CLI 2.0, aşağıdaki adımları tam hello hello:

1. Merhaba son yükleyip [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).

2. Hello kullanarak VNet için bir kaynak grubu oluşturmak [az grubu oluşturma](/cli/azure/group#create) hello komutunu `--name` ve `--location` bağımsız değişkenler:

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. VNet ve bir alt ağ oluşturun:

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    Beklenen çıktı:
    
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

    Kullanılan parametreler:

    - `--name TestVNet`: Merhaba VNet toobe oluşturulan adı.
    - `--resource-group TestRG`: hello kaynağı denetleyen # hello kaynak grubu adı. 
    - `--location centralus`: Merhaba hangi toodeploy konumuna.
    - `--address-prefix 192.168.0.0/16`: Merhaba adres öneki ve blok.  
    - `--subnet-name FrontEnd`: hello alt hello adı.
    - `--subnet-prefix 192.168.1.0/24`: Merhaba adres öneki ve blok.

    toolist hello temel bilgileri toouse hello içinde sonraki komutunu hello VNet kullanarak sorgulayabilir bir [sorgu filtresi](/cli/azure/query-az-cli2):

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    Hangi çıktı aşağıdaki hello üretir:

        Where      Name      Group

        centralus  TestVNet  TestRG

4. Bir alt ağ oluşturun:

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    Beklenen çıktı:

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

    Kullanılan parametreler:

    - `--address-prefix 192.168.2.0/24`: Alt ağ CIDR bloğu.
    - `--name BackEnd`: Hello yeni alt ağ adı.
    - `--resource-group TestRG`: hello kaynak grubu.
    - `--vnet-name TestVNet`: VNet sorumlu hello hello adı.

5. Sorgu hello özelliklerini yeni VNet hello:

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    Beklenen çıktı:

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. Merhaba alt sorgu hello özellikleri:

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    Beklenen çıktı:

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a>Sonraki adımlar

Bilgi nasıl tooconnect:

- Merhaba okuyarak sanal makine (VM) tooa sanal ağ [bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md) makalesi. Merhaba makaleleri hello adımlarda bir VNet ve alt ağ oluşturmak yerine, bir VM'ye mevcut VNet ve alt ağ tooconnect seçebilirsiniz.
- sanal ağ tooother sanal ağlar hello okuyarak hello [sanal ağlara bağlanma](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) makalesi.
- bir siteden siteye sanal özel ağ (VPN) veya expressroute bağlantı hattı kullanarak hello sanal ağ tooan şirket içi ağ. Bilgi hello okuyarak nasıl [bir siteden siteye VPN kullanarak bir VNet tooan şirket içi ağ bağlanmak](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) ve [VNet tooan expressroute bağlantı hattı bağlantı](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).
