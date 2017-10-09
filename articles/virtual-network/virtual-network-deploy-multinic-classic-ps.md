---
title: "aaaCreate birden çok NIC - Azure PowerShell'yle bir VM'yi (Klasik) | Microsoft Docs"
description: "Bilgi nasıl toocreate PowerShell kullanarak birden çok NIC'yle bir VM'yi (Klasik)."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a>PowerShell kullanarak birden çok NIC ile VM (Klasik) oluşturun

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

Sanal makineler (VM'ler) oluşturma ve birden çok ağ arabirimlerine (NIC'ler) tooeach, VM'lerin ekleyin. Birden çok NIC NIC'ler arasında trafik türlerini ayrılması etkinleştirin. Örneğin, bir başka yalnızca iç kaynakları ile iletişim kurar değil sırada NIC hello Internet ile iletişim kurabileceği toohello Internet bağlı. Merhaba özelliği tooseparate ağ trafiği birden çok NIC boyunca uygulama sunma ve WAN iyileştirmesi çözümleri gibi birçok ağ sanal uygulamaları için gereklidir.

> [!IMPORTANT]
> Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md). Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır. Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir. Bilgi nasıl tooperform hello kullanarak şu adımları [Resource Manager dağıtım modeli](virtual-network-deploy-multinic-arm-ps.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Merhaba aşağıdaki adımları kullanın adlı bir kaynak grubu *IaaSStory* hello WEB sunucuları ve bir kaynak grubu için adlı *IaaSStory arka uç* hello DB sunucuları için.

## <a name="prerequisites"></a>Ön koşullar

DB sunucuları hello oluşturabilmeniz için önce toocreate hello gerekir *IaaSStory* hello gereken tüm kaynakların bu senaryo için kaynak grubuyla. Bu kaynaklar, tam izleyin adımları hello toocreate. Merhaba hello adımları izleyerek bir sanal ağ oluşturma [bir sanal ağ oluşturma](virtual-networks-create-vnet-classic-netcfg-ps.md) makalesi.

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>Arka uç VM'ler Hello oluşturma
Merhaba arka uç VM'ler kaynakları aşağıdaki hello hello oluşturulmasına bağlıdır:

* **Arka uç alt**. Merhaba veritabanı sunucuları toosegregate trafiği ayrı bir alt parçası olacak. adlı sanal ağ içinde aşağıdaki Hello komut dosyası bekler bu alt ağ tooexist *WTestVnet*.
* **Veri diskleri için depolama hesabı**. Daha iyi performans için premium depolama hesabı gerektirir katı hal sürücüsü (SSD) teknolojisi hello veritabanı sunucularında hello veri diski kullanır. Emin hello toosupport premium depolama dağıttığınız Azure konumu olun.
* **Kullanılabilirlik kümesi**. Tüm veritabanı sunucuları tooa tek kullanılabilirlik kümesi eklenir, tooensure hello VM'ler en az biri hazır ve çalışır bakımı sırasında.

### <a name="step-1---start-your-script"></a>1. adım - kodunuzu Başlat
Kullanılan hello tam PowerShell komut dosyası indirebilirsiniz [burada](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1). Ortamınızdaki toochange hello betik toowork Hello adımları izleyin.

1. Değiştirme hello değişkenlerin değerleri yukarıda dağıtılmış varolan kaynak grubunuz göre hello aşağıdaki [Önkoşullar](#Prerequisites).

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. Merhaba değerlerini değiştirin arka uç dağıtımınız için toouse istediğiniz hello değişkenleri aşağıdaki hello değerlerine göre.

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>2. adım - Vm'leriniz için gerekli kaynakları oluşturma
Yeni bir bulut hizmeti ve bir depolama hello veri diskleri için tüm VM'ler için hesap toocreate gerekir. Ayrıca toospecify görüntü ve yerel yönetici hesabı hello VM'ler için gerekir. Bu kaynaklar toocreate tamamlamak hello adımları izleyin:

1. Yeni bir bulut hizmeti oluşturun.

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. Yeni bir premium depolama hesabı oluşturun.

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. Aboneliğiniz için geçerli depolama hesabı hello olarak yukarıda oluşturduğunuz hello depolama hesabını ayarlama.

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. Merhaba VM için bir görüntü seçin.

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. Merhaba yerel yönetici hesabının kimlik bilgilerini ayarlayın.

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a>3. adım - VMs oluşturma
Ve oluşturma gibi birçok VM gerekli NIC ve sanal makineleri hello döngü içinde hello gibi bir döngü toocreate toouse gerekir. toocreate hello NIC ve sanal makineleri, aşağıdaki adımları hello yürütün.

1. Başlangıç bir `for` döngü toorepeat hello komutların toocreate VM iki NIC gerektiği gibi birçok kez hello hello değerine bağlı olarak `$numberOfVMs` değişkeni.

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. Oluşturma bir `VMConfig` hello görüntüsü, boyutu ve kullanılabilirlik Merhaba VM kümesi belirtme nesnesi.

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. Merhaba VM Windows VM olarak sağlayın.

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. Merhaba varsayılan NIC ayarlayabilir ve statik bir IP adresi atayabilirsiniz.

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. Her VM için ikinci bir NIC ekleyin.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. Toodata diskler için her bir VM oluşturun.

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. Her VM ve son hello döngü oluşturun.

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a>Adım 4 - çalışma hello komut dosyası
İndirilen ve değiştirilen hello betik gereksinimlerinize bağlı olarak toocreate hello arka uç veritabanı birden çok NIC içeren VM'ler kendisinin komut dosyası çalışma temel.

1. Komut dosyanızı kaydedin ve hello çalıştırın **PowerShell** komut istemi veya **PowerShell ISE**. Merhaba ilk çıktısı, aşağıda gösterildiği gibi görürsünüz.

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. Merhaba kimlik bilgileri istemi ve tıklatın gerekli hello bilgileri doldurun **Tamam**. Merhaba çıktı aşağıdaki döndürülür.

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
