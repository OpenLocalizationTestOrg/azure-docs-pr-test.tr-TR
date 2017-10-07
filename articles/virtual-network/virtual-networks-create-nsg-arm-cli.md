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
# <a name="create-network-security-groups-using-hello-azure-cli-20"></a>Ağ güvenlik grupları hello Azure CLI 2.0 kullanarak oluşturma

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi 

CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak: 

- [Azure CLI 1.0](virtual-networks-create-nsg-cli-nodejs.md) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için 
- [Azure CLI 2.0](#Create-the-nsg-for-the-front-end-subnet) -bizim gelecek nesil CLI hello kaynak yönetimi dağıtım modeli (Bu makalede)

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

Merhaba örnek Azure CLI 2.0 zaten senaryosunda hello önceki göre oluşturulan basit bir ortam aşağıdaki beklediğiniz komutları. 

## <a name="create-hello-nsg-for-hello-frontend-subnet"></a>Merhaba Merhaba NSG oluşturma `FrontEnd` alt ağ

toocreate adlı bir NSG *NSG ön uç* senaryosunda hello önceki bağlı olarak, hello adımları aşağıdaki izleyin.

1. Henüz henüz, yüklemek ve hello son yapılandırırsanız [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login). 

2. Hello kullanarak bir NSG oluşturma [az ağ nsg oluşturma](/cli/azure/network/nsg#create) komutu. 

    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-FrontEnd \
    --location centralus 
    ```

    Parametreler:
   
   * `--resource-group`: Merhaba NSG oluşturulduğu hello kaynak grubunun adı. Bizim senaryomuz için bu *TestRG* ’dir.
   * `--location`: Merhaba yeni NSG oluşturulduğu azure bölgesi. Bizim senaryomuz için *westus*.
   * `--name`: Hello için ad yeni NSG. Bizim senaryomuz için *NSG ön uç*.

    Merhaba çıkış oldukça bit tüm hello varsayılan kuralları listesi dahil olmak üzere bilgilerinin beklenmektedir. Merhaba aşağıdaki örnekte bir JMESPATH sorgu Filtresi ile hello kullanarak hello varsayılan kuralları gösterir `table` çıktı biçimi:

    ```azurecli
    az network nsg show \
    -g testrg \
    -n nsg-frontend \
    --query 'defaultSecurityRules[].{Access:access,Desc:description,DestPortRange:destinationPortRange,Direction:direction,Priority:priority}' \
    -o table
    ```
   
   Çıktı:

        Access    Desc                                                    DestPortRange    Direction      Priority
        
        Allow     Allow inbound traffic from all VMs in VNET              *                Inbound           65000
        Allow     Allow inbound traffic from azure load balancer          *                Inbound           65001
        Deny      Deny all inbound traffic                                *                Inbound           65500
        Allow     Allow outbound traffic from all VMs tooall VMs in VNET  *                Outbound          65000
        Allow     Allow outbound traffic from all VMs tooInternet         *                Outbound          65001
        Deny      Deny all outbound traffic                               *                Outbound          65500



3. Merhaba Internet hello ile gelen erişim tooport 3389 (RDP) sağlayan bir kural oluşturmak [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) komutu.

    > [!NOTE]
    > Kullanmakta olduğunuz hello Kabuk bağlı olarak toomodify hello gerekebilecek `*` hello bağımsız şekilde olarak tooexpand hello bağımsız değişkeni değil yürütmeden önce aşağıdaki karakter.
   
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
   
    Beklenen çıktı:
   
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

    Parametreler:

    * `--resource-group testrg`: kaynak grubu toouse hello. Büyük küçük harf duyarlı olduğunu unutmayın.
    * `--nsg-name NSG-FrontEnd`: Hangi hello kural oluşturulur hello NSG adı.
    * `--name rdp-rule`: Hello yeni kural adı.
    * `--access Allow`: Erişim düzeyi hello kuralın (Engelle veya izin ver).
    * `--protocol Tcp`: Protokolü (Tcp, Udp veya *).
    * `--direction Inbound`: Hello bağlantısı (gelen veya giden) yönü.
    * `--priority 100`: Hello kuralı için öncelik.
    * `--source-address-prefix Internet`: CIDR veya varsayılan etiketleri kullanılarak kaynak adres ön eki.
    * `--source-port-range "*"`: Bağlantı noktası veya bağlantı noktası aralığı kaynağı. Merhaba bağlantı açılan bağlantı.
    * `--destination-address-prefix "*"`: CIDR veya varsayılan etiketleri kullanılarak hedef adres ön eki.
    * `--destination-port-range 3389`: Hedef bağlantı noktası veya bağlantı noktası aralığı. Merhaba bağlantı isteğini alan bağlantı.



4. Merhaba Internet gelen erişim tooport 80 (HTTP) sağlayan bir kural oluşturmak **az ağ nsg kuralını** komutu.
   
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
   
    Beklenen putput:
   
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

5. Merhaba NSG toohello bağlamak **ön uç** alt ağ ile Merhaba [az ağ sanal ağ alt ağı güncelleştirme](/cli/azure/network/vnet/subnet#update) komutu.
        
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name FrontEnd \
    --resource-group testrg \
    --network-security-group NSG-FrontEnd
    ```
   
    Beklenen çıktı:
   
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

## <a name="create-hello-nsg-for-hello-backend-subnet"></a>Merhaba Merhaba NSG oluşturma `BackEnd` alt ağ
toocreate adlı bir NSG *NSG arka uç* senaryosunda hello önceki bağlı olarak, hello adımları aşağıdaki izleyin.

1. Merhaba oluşturma `NSG-BackEnd` NSG ile **az ağ nsg oluşturma**.
   
    ```azurecli
    az network nsg create \
    --resource-group testrg \
    --name NSG-BackEnd \
    --location centralus
    ```
   
    Adım 2, önceki, olduğu gibi hello çıkış varsayılan kuralları da dahil olmak üzere oldukça büyük beklenmektedir.
   
2. Merhaba gelen erişim tooport 1433 (SQL) sağlayan bir kural oluşturmak `FrontEnd` alt ağ ile Merhaba **az ağ nsg kuralını** komutu.
   
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
   
    Beklenen çıktı:

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

3. Kullanarak toohello Internet erişimini engelleyen bir kural oluşturmak hello **az ağ nsg kuralını** komutu.
   
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
   
    Beklenen putput:
   
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

4. Merhaba NSG toohello bağlamak `BackEnd` hello kullanarak alt **az ağ sanal alt ağ kümesi** komutu.
   
    ```azurecli
    az network vnet subnet update \
    --vnet-name TestVNET \
    --name BackEnd \
    --resource-group testrg \
    --network-security-group NSG-BackEnd
    ```
   
    Beklenen çıktı:
   
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
