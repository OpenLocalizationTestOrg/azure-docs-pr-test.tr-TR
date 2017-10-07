---
title: "aaaConfigure özel IP adresleri VM'ler - Azure CLI 2.0 için | Microsoft Docs"
description: "Nasıl tooconfigure özel IP adresleri kullanarak sanal makineleri için Azure komut satırı arabirimi (CLI) 2.0 hello öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a>Hello Azure CLI 2.0 kullanarak bir sanal makine için özel IP adreslerini yapılandırın

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi 

CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak: 

- [Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için 
- [Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -bizim gelecek nesil CLI hello kaynak yönetimi dağıtım modeli (Bu makalede)

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede, hello Resource Manager dağıtım modeli yer almaktadır. Ayrıca [hello Klasik dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> Merhaba aşağıdaki örnek Azure CLI 2.0 komutları önceden oluşturulmuş basit bir ortam bekler. Bu belgede gösterildiği toorun hello komutları istiyorsanız, ilk derleme açıklanan hello test ortamı [vnet oluşturma](virtual-networks-create-vnet-arm-cli.md).

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a>Bir VM oluşturulurken özel bir statik IP adresi belirtin

toocreate adlı bir VM'den *DNS01* hello içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet* özel bir statik IP *192.168.1.101*, Merhaba adımları izleyin:

1. Henüz henüz, yüklemek ve hello son yapılandırırsanız [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login). 

2. Merhaba VM için bir genel IP ile Merhaba oluşturma [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create) komutu. Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.

    > [!NOTE]
    > İstediğiniz ya da ortamınıza bağlı olarak bu, bağımsız değişkenler için farklı değerler toouse ve sonraki adımları gerekir.
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    Beklenen çıktı:
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * `--resource-group`: Hangi toocreate hello ortak IP hello kaynak grubunun adı.
   * `--name`: Hello genel IP adı.
   * `--location`: Hangi toocreate hello genel IP azure bölgesinde.

3. Merhaba çalıştırmak [az ağ NIC oluşturmak](/cli/azure/network/nic#create) komutu toocreate NIC statik özel IP ile. Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır. 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    Beklenen çıktı:
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    Parametreler:

    * `--private-ip-address`: Merhaba NIC özel statik IP adresi
    * `--vnet-name`: Hangi toocreate NIC hello hello Vnet'in adı
    * `--subnet`: Hangi toocreate hello NIC hello alt ağ adı

4. Merhaba çalıştırmak [azure vm oluşturma](/cli/azure/vm/nic#create) hello genel IP NIC ile VM oluşturulan yukarıdaki komut toocreate hello. Merhaba çıktıdan sonra gösterilen hello listede kullanılan hello parametreler açıklanmaktadır.
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    Beklenen çıktı:
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   Merhaba temel dışında parametreleri [az vm oluşturma](/cli/azure/vm#create) parametreleri.

   * `--nics`: Hello NIC toowhich hello VM adını eklenir.
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a>Bir VM için özel statik IP adresi bilgilerini alma

oluşturduğunuz tooview hello statik özel IP adresi Azure CLI komutu aşağıdaki hello çalıştırın ve hello değerlerini uyun *özel IP ayırma yöntemi* ve *özel IP adresi*:

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

Beklenen çıktı:

```json
"192.168.1.101"
```

toodisplay hello NIC belirli IP bilgilerini bu VM, sorgu hello NIC özellikle hello:

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

Merhaba çıktısı aşağıdakine benzer şöyledir:

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a>Özel bir statik IP adresi bir sanal makineden kaldırın

Resource manager dağıtımları için Azure CLI içinde nıc'den özel bir statik IP adresi kaldıramazsınız. Yapmanız gerekir:
- Dinamik IP kullanan yeni bir NIC oluşturun
- NIC yeni oluşturulan VM hello hello üzerinde Hello NIC ayarlayın 

VM kullanılan yukarıdaki hello komutları hello toochange Merhaba NIC hello adımları izleyin.

1. Merhaba çalıştırmak **azure ağı NIC grubu oluşturmak** toocreate dinamik IP ayırma ile yeni bir IP adresi kullanarak yeni bir NIC komutu. IP adresi belirtildiğinden, hello ayırma yöntemi olduğuna dikkat edin **dinamik**.

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    Beklenen çıktı:

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. Merhaba çalıştırmak **azure vm kümesi** komutu toochange hello NIC VM hello tarafından kullanılır.
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    Beklenen çıktı:
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > Merhaba VM büyüklükte toohave ise hello çalıştıran birden çok NIC **azure ağı NIC silme** toodelete hello eski NIC komutu
   
## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.
* Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.
* Merhaba başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).

