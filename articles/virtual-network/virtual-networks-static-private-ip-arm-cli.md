---
title: "Özel IP adresleri VM'ler - Azure CLI 2.0 için yapılandırma | Microsoft Docs"
description: "Azure komut satırı arabirimi (CLI) 2.0 kullanarak sanal makineleri için özel IP adresleri yapılandırmayı öğrenin."
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
ms.openlocfilehash: 071156367c1f819a00d31f1d0335e301391fda81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-the-azure-cli-20"></a>Azure CLI 2.0 kullanarak bir sanal makine için özel IP adreslerini yapılandırın

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-to-complete-the-task"></a>Görevi tamamlamak için kullanılacak CLI sürümleri 

Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz: 

- [Azure CLI 1.0](virtual-networks-static-private-ip-cli-nodejs.md): Klasik ve kaynak yönetimi dağıtım modellerine yönelik CLI’mız 
- [Azure CLI 2.0](#specify-a-static-private-ip-address-when-creating-a-vm) -bizim gelecek nesil CLI kaynak yönetimi dağıtım modeli (Bu makalede)

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Bu makalede Resource Manager dağıtım modeli anlatılmaktadır. Ayrıca [Klasik dağıtım modelinde statik özel IP adresi yönetmek](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> Aşağıdaki örnek Azure CLI 2.0 komutları önceden oluşturulmuş basit bir ortam bekler. Bu belgede gösterildiği komutları çalıştırmak istiyorsanız, önce açıklanan test ortamı oluşturmak [vnet oluşturma](virtual-networks-create-vnet-arm-cli.md).

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a>Bir VM oluşturulurken özel bir statik IP adresi belirtin

Adlı bir VM oluşturmak için *DNS01* içinde *ön uç* adlı bir sanal ağ alt ağı *TestVNet* özel bir statik IP *192.168.1.101*, aşağıdaki adımları izleyin:

1. Henüz henüz yükleyin ve en son yapılandırırsanız [Azure CLI 2.0](/cli/azure/install-az-cli2) ve bir Azure hesabı kullanarak oturum açma [az oturum açma](/cli/azure/#login). 

2. VM için bir genel IP oluşturun [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create) komutu. Çıktıdan sonra gösterilen listede, kullanılan parametreler açıklanmaktadır.

    > [!NOTE]
    > İstediğiniz ya da ortamınıza bağlı olarak bu, bağımsız değişkenler için farklı değerler ve sonraki adımları kullanmak için gerekir.
   
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

   * `--resource-group`: Genel IP oluşturulacağı kaynak grubunun adı.
   * `--name`: Genel IP adı.
   * `--location`: Genel IP oluşturulacağı azure bölgesi.

3. Çalıştırma [az ağ NIC oluşturmak](/cli/azure/network/nic#create) statik özel IP ile NIC grubu oluşturmak için komutu. Çıktıdan sonra gösterilen listede, kullanılan parametreler açıklanmaktadır. 
   
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

    * `--private-ip-address`: NIC özel statik IP adresi
    * `--vnet-name`: İçinde NIC oluşturulacağı Vnet'in adı
    * `--subnet`: İçinde NIC oluşturulacağı alt ağın adı

4. Çalıştırma [azure vm oluşturma](/cli/azure/vm/nic#create) ortak IP yukarıda oluşturduğunuz NIC ile VM oluşturmak için komutu. Çıktıdan sonra gösterilen listede, kullanılan parametreler açıklanmaktadır.
   
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
   
   Parametreleri temel dışında [az vm oluşturma](/cli/azure/vm#create) parametreleri.

   * `--nics`: VM bağlı olduğu NIC adı.
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a>Bir VM için özel statik IP adresi bilgilerini alma

Oluşturduğunuz statik özel IP adresini görüntülemek için Azure CLI ve aşağıdaki komutu çalıştırın değerlerini gözlemlemek *özel IP ayırma yöntemi* ve *özel IP adresi*:

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

Beklenen çıktı:

```json
"192.168.1.101"
```

NIC bu VM için belirli IP bilgilerini görüntülemek için NIC özellikle sorgu:

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

Çıktı aşağıdakine benzer:

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
- NIC VM üzerinde yeni oluşturulan NIC ayarlayın 

Yukarıdaki komutlarda kullanılan VM NIC değiştirmek için aşağıdaki adımları izleyin.

1. Çalıştırma **azure ağı NIC grubu oluşturmak** dinamik IP ayırma ile yeni bir IP adresi kullanarak yeni bir NIC grubu oluşturmak için komutu. IP adresi belirtildiğinden ayırma yöntemi olduğuna dikkat edin **dinamik**.

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

2. Çalıştırma **azure vm kümesi** VM tarafından kullanılan NIC değiştirmek için komutu.
   
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
    > VM birden çok NIC için yeterince büyük olduğundan çalıştırırsanız **azure ağı NIC silme** eski NIC silmek için
   
## <a name="next-steps"></a>Sonraki adımlar
* Hakkında bilgi edinin [ayrılmış genel IP](virtual-networks-reserved-public-ip.md) adresleri.
* Hakkında bilgi edinin [örnek düzeyinde ortak IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adresleri.
* Başvurun [ayrılmış IP REST API'leri](https://msdn.microsoft.com/library/azure/dn722420.aspx).

