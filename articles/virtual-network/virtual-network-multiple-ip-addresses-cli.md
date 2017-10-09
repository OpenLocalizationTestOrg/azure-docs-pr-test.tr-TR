---
title: "hello Azure CLI 2.0 kullanarak birden çok IP adresleriyle aaaVM | Microsoft Docs"
description: "Nasıl tooassign birden çok IP adresleri öğrenin tooa kullanarak sanal makine hello Azure CLI 2.0 | Resource Manager."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a>Hello Azure CLI 2.0 kullanarak toovirtual makineleri birden çok IP adresi atayın

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Bu makalede nasıl toocreate hello Azure Resource Manager dağıtım modeli kullanılarak aracılığıyla sanal makine (VM) hello Azure CLI 2.0 açıklanmaktadır. Birden çok IP adresi hello Klasik dağıtım modeli aracılığıyla oluşturulan tooresources atanamaz. Merhaba okuma Azure dağıtım modelleri hakkında daha fazla toolearn [dağıtım modellerini anlama](../resource-manager-deployment-model.md) makalesi.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Birden çok IP adresiyle bir VM oluşturma

Hello Azure CLI 2.0 (Bu makalede) veya hello kullanarak bu görevi tamamlayabilirsiniz [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md). Ortamınız için uygun şekilde Hello değerlerini değiştirin. izleyin hello adımlarda hello senaryosunda açıklandığı şekilde nasıl toocreate örneği VM ile birden çok IP adresleri, açıklanmaktadır. Değişken değerleri değiştirmek "" ve IP adresi türleri, uygulamanız için gerekli olarak. 

1. Merhaba yüklemek [Azure CLI 2.0](/cli/azure/install-az-cli2) , zaten yüklü değilse.
2. Merhaba hello adımları tamamlayarak Linux VM'ler için bir SSH ortak ve özel anahtar çifti oluşturma [Linux VM'ler için bir SSH ortak ve özel anahtar çifti oluşturma](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. Oturum açma hello komutuyla bir komut kabuğu'ndan `az login` ve kullanmakta olduğunuz hello abonelik seçin.
4. Bir Linux veya Mac bilgisayarda aşağıdaki hello komut dosyası çalıştırarak Hello VM oluşturun. Merhaba komut dosyası bir kaynak grubu, bir sanal ağ (VNet), bir NIC üç IP yapılandırmaları olan ve bir VM ile Merhaba iki bağlı NIC tooit oluşturur. Merhaba NIC, ortak IP adresi, sanal ağ ve VM kaynakları tüm bulunmalıdır hello aynı konumu ve abonelik. Merhaba kaynakları tüm tooexist hello yok ancak aynı kaynak grubunda, yaptıkları komut dosyası izleyen hello.

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

Ayrıca toocreating 3 IP yapılandırmaları olan bir NIC ile VM, hello komut dosyası oluşturur:

- Tek bir premium disk varsayılan olarak yönetilen, ancak oluşturabileceğiniz hello disk türü için diğer seçeneğiniz vardır. Okuma hello [hello Azure CLI 2.0 kullanarak bir Linux VM oluşturma](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) Ayrıntılar için makale.
- Bir alt ağı ve iki genel IP adresine sahip bir sanal ağ. Alternatif olarak, kullanabileceğiniz *varolan* sanal ağ, alt ağ, NIC veya ortak IP adresi kaynakları. nasıl toouse varolan ağ kaynakları yerine ek kaynakları oluşturma girin toolearn `az vm create -h`.

Nominal bir ücret ortak IP adresine sahip. IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası. Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur. Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.

Merhaba VM oluşturulduktan sonra hello girin `az network nic show --name MyNic1 --resource-group myResourceGroup` komut tooview hello NIC yapılandırması. Merhaba girin `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview hello IP yapılandırmaları listesini ilişkili toohello NIC

Ekle hello özel IP adresleri toohello VM işletim sistemi işletim sisteminizin hello hello adımları tamamlayarak [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin.

## <a name="add"></a>IP adreslerini tooa VM ekleme

NIC izleyin hello adımları tamamlayarak varolan ek özel ve genel IP adresleri tooan ekleyebilirsiniz. Hello örnekleri derleme sırasında hello [senaryo](#Scenario) bu makalede açıklanan.

1. Bir komut kabuğu ve bu bölümdeki adımları tek bir oturum içinde kalan tam hello açın. Azure CLI yüklenmiş ve yapılandırılmış zaten sahip değilseniz, tam hello hello adımları [Azure CLI 2.0 yüklemesi](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) makale ve oturum açma tooyour hello Azure hesabı `az-login` komutu.

2. Aşağıdaki bölümlerde, gereksinimlerinize göre hello Hello adımları tamamlayın:

    **Özel bir IP adresi Ekle**
    
    özel bir IP adresi tooa NIC tooadd, izleyen hello komutunu kullanarak bir IP yapılandırması oluşturmanız gerekir. Merhaba statik IP adresi hello alt ağ için kullanılmayan bir adres olmalıdır.

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    Benzersiz yapılandırma adları ve özel IP adresleri (yapılandırmaları statik IP adresleriyle) kullanarak gereksinim duyduğunuz kadar çok yapılandırmaları oluşturun.

    **Bir ortak IP adresi Ekle**
    
    Bir ortak IP adresi tooeither ilişkilendirerek eklenen yeni bir IP yapılandırması veya var olan bir IP yapılandırması. Gereksinim duyduğunuz kadar izleyin, hello bölümlerden biri hello adımlarını tamamlayın.

    Nominal bir ücret ortak IP adresine sahip. IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası. Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur. Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.

    - **Merhaba kaynak tooa yeni IP yapılandırmasını ilişkilendirin**
    
        Yeni bir IP yapılandırmasında bir ortak IP adresi eklediğinizde, tüm IP yapılandırmalarının özel bir IP adresi olması gerektiği için özel bir IP adresi eklemelisiniz. Varolan bir ortak IP adresi kaynağı ekleyin veya yeni bir tane oluşturun. toocreate yeni bir hello aşağıdaki komutu girin:
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        Özel statik IP adresi ve ilişkili hello yeni bir IP yapılandırmasıyla toocreate *myPublicIP3* genel IP adresi kaynak, komutu aşağıdaki hello girin:

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - **İlişkilendirme hello kaynak tooan mevcut IP yapılandırması** genel bir IP adresi kaynağı yalnızca zaten ilişkili olmayan ilişkili tooan IP yapılandırması olabilir. Komutu aşağıdaki hello girerek bir IP yapılandırması ilişkili bir ortak IP adresi olup olmadığını belirleyebilirsiniz:

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        Çıkış döndürdü:
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        Merhaba itibaren **PublicIpAddressId** sütunu için *IpConfig 3* olan hello boş çıkış, hiçbir ortak IP adresi kaynağı şu anda ilişkili tooit. Bir var olan ortak IP adresi kaynak tooIpConfig-3 ekleyin veya komut toocreate bir aşağıdaki hello girin:

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        Tooassociate hello ortak IP adresi adlı kaynak toohello mevcut IP yapılandırması komutu aşağıdaki hello girin *IPConfig 3*:
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. Girerek NIC hello komutu aşağıdaki toohello atanan kaynak kimlikleri görünüm hello özel IP adresleri ve hello genel IP adresi:

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    Çıkış döndürdü: <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. Merhaba hello yönergeleri takip ederek toohello NIC toohello VM işletim sistemi eklenen hello özel IP adresleri ekleme [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin. Merhaba ortak IP adresleri toohello işletim sistemi eklemeyin.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
