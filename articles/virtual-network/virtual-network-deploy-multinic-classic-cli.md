---
title: "aaaCreate birden çok NIC - Azure CLI 1.0'yle bir VM'yi (Klasik) | Microsoft Docs"
description: "Nasıl toocreate (Klasik) kullanarak birden çok NIC ile VM hello Azure komut satırı arabirimi (CLI) 1.0 öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a>Hello Azure CLI 1.0 kullanarak birden çok NIC ile VM (Klasik) oluşturun

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Sanal makineler (VM'ler) oluşturma ve birden çok ağ arabirimlerine (NIC'ler) tooeach, VM'lerin ekleyin. Birden çok NIC NIC'ler arasında trafik türlerini ayrılması etkinleştirin. Örneğin, bir başka yalnızca iç kaynakları ile iletişim kurar değil sırada NIC hello Internet ile iletişim kurabileceği toohello Internet bağlı. Merhaba özelliği tooseparate ağ trafiği birden çok NIC boyunca uygulama sunma ve WAN iyileştirmesi çözümleri gibi birçok ağ sanal uygulamaları için gereklidir.

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Bilgi nasıl tooperform hello kullanarak şu adımları [Resource Manager dağıtım modeli](virtual-network-deploy-multinic-arm-cli.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Merhaba aşağıdaki adımları kullanın adlı bir kaynak grubu *IaaSStory* hello WEB sunucuları ve bir kaynak grubu için adlı *IaaSStory arka uç* hello DB sunucuları için.

## <a name="prerequisites"></a>Ön koşullar
DB sunucuları hello oluşturabilmeniz için önce toocreate hello gerekir *IaaSStory* hello gereken tüm kaynakların bu senaryo için kaynak grubuyla. Bu kaynaklar, tam izleyin adımları hello toocreate. Merhaba hello adımları izleyerek bir sanal ağ oluşturma [bir sanal ağ oluşturma](virtual-networks-create-vnet-classic-cli.md) makalesi.

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a>Merhaba arka uç dağıtmak VM'ler
Merhaba arka uç VM'ler kaynakları aşağıdaki hello hello oluşturulmasına bağlıdır:

* **Veri diskleri için depolama hesabı**. Daha iyi performans için premium depolama hesabı gerektirir katı hal sürücüsü (SSD) teknolojisi hello veritabanı sunucularında hello veri diski kullanır. Emin hello toosupport premium depolama dağıttığınız Azure konumu olun.
* **NIC**. Her VM veritabanı erişimi için iki NIC gerekir ve yönetimi için bir tane.
* **Kullanılabilirlik kümesi**. Tüm veritabanı sunucuları tooa tek kullanılabilirlik kümesi eklenir, tooensure hello VM'ler en az biri hazır ve çalışır bakımı sırasında.

### <a name="step-1---start-your-script"></a>1. adım - kodunuzu Başlat
Kullanılan hello tam bash komut dosyası indirebilirsiniz [burada](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh). Aşağıdaki adımları toochange hello betik toowork ortamınızdaki hello tamamlayın:

1. Değiştirme hello değişkenlerin değerleri yukarıda dağıtılmış varolan kaynak grubunuz göre hello aşağıdaki [Önkoşullar](#Prerequisites).

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. Merhaba değerlerini değiştirin arka uç dağıtımınız için toouse istediğiniz hello değişkenleri aşağıdaki hello değerlerine göre.

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>2. adım - Vm'leriniz için gerekli kaynakları oluşturma
1. Tüm arka uç VM'ler için yeni bir bulut hizmeti oluşturun. Bildirim hello hello kullanımını `$backendCSName` hello kaynak grubu adı için değişken ve `$location` hello Azure bölgesi için.

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. Premium depolama hesabı hello işletim sistemi için ve veri diskleri toobe sizin tarafından VM'ler kullanılan oluşturun.

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a>3. adım - VMs birden çok NIC ile oluşturma
1. Döngü toocreate üzerinde hello göre birden çok VM Başlat `numberOfVMs` değişkenleri.

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. Her bir VM hello adını ve her bir hello iki NIC IP adresi belirtin.

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. Merhaba VM oluşturun. Fark hello hello kullanımını `--nic-config` adı, alt ağ ve IP adresi ile tüm NIC listesini içeren parametresi.

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. Her bir VM, iki veri diski oluşturun.

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a>Adım 4 - çalışma hello komut dosyası
İndirilen ve hello betik hello betik toocreate hello geri çalıştırmak gereksinimlerinize göre değişti birden çok NIC içeren veritabanı VM'ler sonlandırın.

1. Komut dosyanızı kaydedin ve çalıştırın, **Bash** terminal. Merhaba ilk çıktısı, aşağıda gösterildiği gibi görürsünüz.

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. Birkaç dakika sonra hello yürütme sona erer ve hello rest aşağıda gösterildiği gibi hello çıktısını görürsünüz.

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
