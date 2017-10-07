---
title: "hello Azure CLI 1.0 kullanarak birden çok IP adresleriyle aaaVM | Microsoft Docs"
description: "Nasıl tooassign birden çok IP adresleri öğrenin tooa kullanarak sanal makine hello Azure CLI 1.0 | Resource Manager."
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
ms.openlocfilehash: 83ad48e67309fb21d5aca967d4f2c01afdc0b5cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-azure-cli-10"></a>Azure CLI 1.0 kullanarak toovirtual makineleri birden çok IP adresi atayın

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Bu makalede nasıl toocreate hello Azure Resource Manager dağıtım modeli kullanılarak aracılığıyla sanal makine (VM) hello Azure CLI 1.0 açıklanmaktadır. Birden çok IP adresi hello Klasik dağıtım modeli aracılığıyla oluşturulan tooresources atanamaz. Merhaba okuma Azure dağıtım modelleri hakkında daha fazla toolearn [dağıtım modellerini anlama](../resource-manager-deployment-model.md) makalesi.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Birden çok IP adresiyle bir VM oluşturma

Hello Azure CLI 1.0 (Bu makalede) veya hello kullanarak bu görevi tamamlayabilirsiniz [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md). izleyin hello adımlarda hello senaryosunda açıklandığı şekilde nasıl toocreate örneği VM ile birden çok IP adresleri, açıklanmaktadır. Değişken adları ve IP adresi türleri, uygulamanız için gerekli olarak değiştirin.

1. Azure CLI 1.0 aşağıdaki hello tarafından adımları hello hello yükleyip [hello Azure CLI yükleyip](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi ve hello Azure hesabınızla oturum `azure-login` komutu.

2. Kaynak grubu oluşturun:
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. Sanal ağ oluşturma:

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. Bir alt ağ hello sanal ağda oluşturun:

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. Merhaba VM için bir depolama hesabı oluşturun. Merhaba çalıştırmadan önce Değiştir komutu, aşağıdaki *mystorageaccount* benzersiz bir ada sahip. Merhaba adının Azure'da benzersiz olması gerekir:

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. Merhaba IP yapılandırmaları, bir NIC oluşturun ve hello IP yapılandırmaları toohello NIC atayın Eklemek, kaldırmak veya hello yapılandırmalarını gerektiği gibi değiştirin. aşağıdaki yapılandırmalar hello hello senaryoda açıklanmıştır:

    **Ipconfig-1**

    Toocreate izleyin hello komutları girin:

    - Bir statik genel IP adresi ile genel IP adresi kaynağı
    - Merhaba genel IP adresi ve statik bir özel IP adresi tooit atama bir NIC.
    
    Değiştir *mypublicdns* hello Azure konumu içinde benzersiz bir ada sahip.

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > Nominal bir ücret ortak IP adresine sahip. IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası. Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur. Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.

    **Ipconfig 2**

     Yeni bir ortak IP adresi kaynağı ve bir statik genel IP adresi ve özel bir statik IP adresi ile yeni bir IP yapılandırması komutları toocreate aşağıdaki hello girin:
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    **Ipconfig 3**

    Aşağıdaki komutları toocreate özel bir statik IP adresi ve ortak IP adresi bir IP yapılandırmasıyla hello girin:

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    >Bu makalede tüm IP yapılandırmaları tooa atar ancak tek NIC, birden çok IP yapılandırmaları tooany bir sanal NIC de atayabilirsiniz. toolearn toocreate birden çok NIC ile VM okuma nasıl oluşturma bir VM ile birden çok NIC makalesi hello.

7. Linux VM oluşturma 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    toochange hello VM boyutu tooStandard DS2 v2, örneğin, özellik aşağıdaki hello eklemeniz yeterlidir `--vm-size Standard_DS3_v2` toohello `azure vm create` adım 6 komutu.

8. Aşağıdaki komut tooview hello NIC hello girin ve ilişkili IP yapılandırmaları hello:

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. Ekle hello özel IP adresleri toohello VM işletim sistemi işletim sisteminizin hello hello adımları tamamlayarak [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin.

## <a name="add"></a>IP adreslerini tooa VM ekleme

NIC izleyin hello adımları tamamlayarak varolan ek özel ve genel IP adresleri tooan ekleyebilirsiniz. Hello örnekleri derleme sırasında hello [senaryo](#Scenario) bu makalede açıklanan.

1. Azure CLI ve bu bölümdeki adımları tek bir CLI oturumu içinde kalan tam hello açın. Azure CLI yüklenmiş ve yapılandırılmış zaten sahip değilseniz, tam hello hello adımları [hello Azure CLI yükleyip](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) makalesi ve Azure hesabınızda oturum açın.

2. Aşağıdaki bölümlerde, gereksinimlerinize göre hello Hello adımları tamamlayın:

    - **Özel bir IP adresi Ekle**
    
        özel bir IP adresi tooa NIC tooadd, aşağıdaki hello komutu kullanarak IP yapılandırması oluşturmanız gerekir. Merhaba statik adresi hello alt ağ için kullanılmayan bir adres olmalıdır.

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        Benzersiz yapılandırma adları ve özel IP adresleri (yapılandırmaları statik IP adresleriyle) kullanarak gereksinim duyduğunuz kadar çok yapılandırmaları oluşturun.

    - **Bir ortak IP adresi Ekle**
    
        Bir ortak IP adresi tooeither ilişkilendirerek eklenen yeni bir IP yapılandırması veya var olan bir IP yapılandırması. Gereksinim duyduğunuz kadar izleyin, hello bölümlerden biri hello adımlarını tamamlayın.

        > [!NOTE]
        > Nominal bir ücret ortak IP adresine sahip. IP hakkında daha fazla adres fiyatlandırma toolearn okuma hello [IP adresi fiyatlandırma](https://azure.microsoft.com/pricing/details/ip-addresses) sayfası. Bir abonelikte kullanılabilir genel IP adresleri sınırı toohello sayısı yoktur. Merhaba okuma hello sınırları hakkında daha fazla toolearn [Azure sınırlar](../azure-subscription-service-limits.md#networking-limits) makalesi.
        >

        **Merhaba kaynak tooa yeni IP yapılandırmasını ilişkilendirin**
    
        Yeni bir IP yapılandırmasında bir ortak IP adresi eklediğinizde, tüm IP yapılandırmalarının özel bir IP adresi olması gerektiği için özel bir IP adresi eklemelisiniz. Varolan bir ortak IP adresi kaynağı ekleyin veya yeni bir tane oluşturun. toocreate yeni bir hello aşağıdaki komutu girin:

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        Özel statik IP adresi ve ilişkili hello yeni bir IP yapılandırmasıyla toocreate *myPublicIP3* genel IP adresi kaynak, komutu aşağıdaki hello girin:

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        **Merhaba kaynak tooan var olan IP yapılandırmasını ilişkilendirin**

        Genel bir IP adresi kaynağı yalnızca zaten ilişkili olmayan ilişkili tooan IP yapılandırması olabilir. Komutu aşağıdaki hello girerek bir IP yapılandırması ilişkili bir ortak IP adresi olup olmadığını belirleyebilirsiniz:

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        Bir satır benzer toohello IPConfig-3 için çıktı döndürülen hello izleyen bir arayın:

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        Merhaba itibaren **genel IP** sütunu için *IpConfig 3* olduğundan, hiçbir ortak IP adresi kaynağı şu anda ilişkili tooit boştur. Bir var olan ortak IP adresi kaynak tooIpConfig-3 ekleyin veya komut toocreate bir aşağıdaki hello girin:

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        Tooassociate hello ortak IP adresi adlı kaynak toohello mevcut IP yapılandırması komutu aşağıdaki hello girin *IPConfig 3*:
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. Görünüm hello özel IP adresleri ve ortak IP adresi atanmış kaynaklar toohello girerek NIC hello komutu aşağıdaki hello:

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      Merhaba çıkış benzer toohello aşağıdaki döndürülür:
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. Merhaba hello yönergeleri takip ederek toohello NIC toohello VM işletim sistemi eklenen hello özel IP adresleri ekleme [eklemek IP adresleri tooa VM işletim sistemi](#os-config) bu makalenin. Merhaba ortak IP adresleri toohello işletim sistemi eklemeyin.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
