---
title: aaaMigrate tooResource Manager PowerShell ile | Microsoft Docs
description: "Bu makalede hello platform desteklenen geçiş Iaas kaynakların sanal makineleri (VM'ler), sanal ağlar (Vnet'ler) ve depolama hesapları gibi Klasik tooAzure Resource Manager (ARM) Azure PowerShell komutlarını kullanarak anlatılmaktadır"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a>Iaas kaynaklarına Klasik tooAzure Resource Manager Azure PowerShell kullanarak geçirme
Bu adımlar nasıl hello Klasik dağıtım modeli toohello Azure Resource Manager dağıtım modeli hizmet (Iaas) kaynaklardan olarak toomigrate altyapı toouse Azure PowerShell komutları gösterir.

İsterseniz, ayrıca kaynakları hello kullanarak geçirebileceğiniz [Azure komut satırı arabirimi (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).

* Desteklenen geçiş senaryoları hakkında daha fazla bilgiler için bkz: [Klasik tooAzure Resource Manager Iaas kaynaklardan Platform desteklenen geçişini](migration-classic-resource-manager-overview.md).
* Ayrıntılı yönergeler ve bir geçiş kılavuz için bkz: [teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik tooAzure Kaynak Yöneticisi'nden](migration-classic-resource-manager-deep-dive.md).
* [En sık karşılaşılan geçiş hatalarını gözden geçirme](migration-classic-resource-manager-errors.md)

<br>
Adımları bir geçiş işlemi sırasında yürütülen toobe gereken bir akış çizelgesi tooidentify hello siparişi İşte

![Merhaba geçiş adımlarını gösteren ekran görüntüsü](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a>1. adım: geçişini planlama
Klasik tooResource Yöneticisi geçirme Iaas kaynaklardan değerlendirirken öneririz birkaç en iyi uygulamalar şunlardır:

* Merhaba okuma [desteklenen ve desteklenmeyen özellikler ve yapılandırmalar](migration-classic-resource-manager-overview.md). Desteklenmeyen yapılandırmaları veya özellikleri kullanan sanal makineler varsa, hello yapılandırma/özellik destek toobe duyurdu için beklemenizi öneririz. Alternatif olarak, gereksinimlerinize uygun değilse, bu özelliği kaldırmak veya yapılandırma tooenable geçişin dışına taşıyın.
* Bugün, altyapı ve uygulamalarınızı dağıtma komut otomatik değilse, geçiş için bu komut dosyalarını kullanarak toocreate benzer bir test Kurulum deneyin. Alternatif olarak, örnek ortamları hello Azure portal kullanarak ayarlayabilirsiniz.

> [!IMPORTANT]
> Uygulama ağ geçitleri, Klasik tooResource Yöneticisi geçiş için şu anda desteklenmemektedir. toomigrate bir uygulama ağ geçidi ile klasik sanal ağ hazırlama işlemi toomove hello ağ çalıştırmadan önce hello ağ geçidi kaldırın. Merhaba ağ geçidi Azure Kaynak Yöneticisi'nde hello geçişi tamamlandıktan sonra yeniden bağlanın.
>
>ExpressRoute ağ geçidi başka bir Abonelikteki tooExpressRoute devreler bağlanma otomatik olarak geçirilemez. Böyle durumlarda, hello ExpressRoute ağ geçidi kaldırın, hello sanal ağını geçirin ve hello ağ geçidi oluşturun. Lütfen bakın [geçirmek ExpressRoute bağlantı hattına ve hello Klasik toohello Resource Manager dağıtım modeli sanal ağlardan ilişkili](../../expressroute/expressroute-migration-classic-resource-manager.md) daha fazla bilgi için.
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a>2. adım: hello Azure PowerShell'in en son sürümünü yükleme
İki ana seçeneğiniz tooinstall Azure PowerShell vardır: [PowerShell Galerisi](https://www.powershellgallery.com/profiles/azure-sdk/) veya [Web Platformu Yükleyicisi (Webpı)](http://aka.ms/webpi-azps). Webpı aylık güncelleştirmeleri alır. PowerShell Galerisi sürekli güncelleştirmeleri alır. Bu makalede, Azure PowerShell sürüm 2.1.0 temel alır.

Yükleme yönergeleri için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a>3. adım: Azure portalında hello abonelik için bir yönetici olduğundan emin olun
tooperform bu geçiş hello hello aboneliğinin ortak yönetici olarak eklenmelidir [Azure portal](https://portal.azure.com).

1. Merhaba içine oturum [Azure portal](https://portal.azure.com).
2. Merhaba Hub menüsünde seçin **abonelik**. Göremiyorsanız, seçin **daha fazla hizmet**.
3. Merhaba uygun abonelik girişini bulun, sonra hello Ara **MY ROL** alan. Bir ortak yönetici için hello değer olmalıdır _Hesap Yöneticisi_.

Ardından mümkün tooadd bir ortak yönetici değilse, bir Hizmet Yöneticisi veya ortak yönetici için hello abonelik tooget kendiniz eklenen başvurun.   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a>4. adım: aboneliğinizi ayarlamak ve geçiş için kaydolun
İlk olarak, bir PowerShell istemi başlatın. Geçiş için her iki Klasik için ortamınızı kurma tooset gerekir ve Resource Manager.

Merhaba Resource Manager modeli için tooyour hesabında oturum açın.

```powershell
    Login-AzureRmAccount
```

Kullanılabilir abonelikler Hello komutu aşağıdaki hello kullanarak alın:

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

Azure aboneliğiniz için hello geçerli oturum ayarlayın. Bu örnek kümeleri hello varsayılan abonelik adı çok**My Azure aboneliği**. Merhaba örnek abonelik adı kendinizinkilerle değiştirin.

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> Kayıt tek seferlik bir adımdır, ancak geçişi denemeden önce bir kez yapmanız gerekir. Kayıt olmadan, hata iletisi aşağıdaki hello bakın:
>
> *BadRequest: Abonelik geçiş için kayıtlı değil.*
>
>

Merhaba geçiş kaynak sağlayıcısı ile komutu aşağıdaki hello kullanarak kaydedin:

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Merhaba kayıt toofinish için beş dakika bekleyin. Komutu aşağıdaki hello kullanarak hello hello onay durumunu denetleyebilirsiniz:

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

RegistrationState olduğundan emin olun `Registered` devam etmeden önce.

Şimdi oturum açma tooyour hesabı hello Klasik modeli için.

```powershell
    Add-AzureAccount
```

Kullanılabilir abonelikler Hello komutu aşağıdaki hello kullanarak alın:

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

Azure aboneliğiniz için hello geçerli oturum ayarlayın. Bu örnek hello varsayılan abonelik çok ayarlar**My Azure aboneliği**. Merhaba örnek abonelik adı kendinizinkilerle değiştirin.

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>5. adım: hello geçerli dağıtım veya VNET Azure bölgesi yeterli Azure Resource Manager sanal makinesi çekirdeğe sahip olduğunuzdan emin olun
PowerShell komut toocheck hello geçerli Azure Kaynak Yöneticisi'nde sahip çekirdek sayısı aşağıdaki hello kullanabilirsiniz. toolearn çekirdek kotaları hakkında daha fazla bilgi görmek [sınırları ve hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).

Bu örnek hello hello kullanılabilirliğini denetler **Batı ABD** bölge. Merhaba örnek bölge adı kendinizinkilerle değiştirin.

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a>6. adım: Iaas kaynaklarınızı komutları toomigrate çalıştırma
> [!NOTE]
> Burada açıklanan tüm hello ıdempotent işlemleridir. Desteklenmeyen bir özellik veya bir yapılandırma hatası başka bir sorun varsa, hello yeniden deneme öneririz hazırlamak, iptal etmek veya yürütme işlemi. Merhaba platform sonra hello eylemi yeniden dener.
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a>6.1. adım: 1. seçenek - sanal makineler bir bulut hizmetinde (değil, sanal ağ için) geçirme
Komutu aşağıdaki hello kullanarak bulut Hizmetleri ve çekme hello bulut hizmeti toomigrate istediğiniz Get hello listesi. Merhaba VM'ler hello bulut hizmetindeki bir sanal ağ veya web veya çalışan rolleri varsa, hello komutu bir hata iletisi döndürür.

```powershell
    Get-AzureService | ft Servicename
```

Merhaba dağıtım adı hello bulut hizmeti için alın. Bu örnekte, hello hizmet adı olan **Hizmetim**. Merhaba örnek hizmet adı, kendi hizmet adı ile değiştirin.

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

Merhaba sanal makineleri hello bulut hizmetinde geçiş için hazırlayın. Gelen iki seçenekleri toochoose sahip.

* **Seçenek 1. Merhaba VM'ler tooa platform tarafından oluşturulan sanal ağını geçirin**

    Merhaba aşağıdaki komutları kullanarak hello bulut hizmeti geçirirseniz ilk olarak, doğrulama:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    Merhaba önceki komutu tüm uyarıları ve geçiş engelleme hataları görüntüler. Doğrulama başarılı olduğunda sonra toohello üzerinde taşıyabilirsiniz **Prepare** . adım:

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* **Seçenek 2. Mevcut sanal ağda hello Resource Manager dağıtım modeli tooan geçirme**

    Bu örnek kümeleri hello kaynak grubu adı çok**myResourceGroup**, sanal ağ adı çok hello**myVirtualNetwork** ve alt ağ adı çok hello**mySubNet**. Merhaba adları hello örnekte kendi kaynaklarını hello adlarıyla değiştirin.

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    İlk olarak, komutu aşağıdaki hello kullanarak hello sanal ağ geçirirseniz doğrulama:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    Merhaba önceki komutu tüm uyarıları ve geçiş engelleme hataları görüntüler. Doğrulama başarılı olursa, hazırlama adımı aşağıdaki hello ile devam edebilirsiniz:

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

Merhaba Hazırlama işlemi seçenekleri önceki hello birini kullanarak başarılı olduktan sonra hello VM'ler hello geçiş durumu sorgu. Hello olduklarından emin olun `Prepared` durumu.

Bu örnek kümeleri hello VM adı çok**myVM**. Merhaba örnek adı kendi VM adıyla değiştirin.

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

PowerShell veya hello Azure portal kullanarak kaynakları hazırlanmış hello için başlangıç yapılandırmasını denetleyin. Geçiş için hazır olmayan ve toogo geri toohello eski durum istiyorsanız hello aşağıdaki komutu kullanın:

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

Merhaba hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve komut aşağıdaki hello kullanarak hello kaynakları Yürüt:

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a>6.1. adım: 2. seçenek - bir sanal ağdaki sanal makineleri geçirme

toomigrate sanal makinelere sanal bir ağa hello sanal ağ geçirme. Merhaba sanal makineleri otomatik olarak hello sanal ağ ile geçirin. Çekme hello sanal ağ toomigrate istiyor.
> [!NOTE]
> [Tek Klasik sanal makineyi geçirmek](migrate-single-classic-to-resource-manager.md) diskleri yönetilen hello sanal makinenin hello VHD (işletim sistemi ve veri) dosyalarını kullanarak yeni bir kaynak yöneticisi sanal makine oluşturarak.
<br>

> [!NOTE]
> Merhaba sanal ağ adı ne hello gösterilenden farklı olabilir yeni portalı. Merhaba yeni Azure Portal görüntüler hello adıyla `[vnet-name]` ancak hello gerçek sanal ağ adı türü `Group [resource-group-name] [vnet-name]`. Geçiş, arama hello gerçek sanal ağ adı hello komutunu kullanarak önce `Get-AzureVnetSite | Select -Property Name` veya hello görüntüleyin eski Azure Portal. 

Bu örnek kümeleri hello sanal ağ adı çok**myVnet**. Merhaba örnek sanal ağ adı kendinizinkilerle değiştirin.

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> Merhaba sanal ağ ile desteklenmeyen yapılandırmalar web veya çalışan rolleri ya da sanal makineleri içeriyorsa, bir doğrulama hata iletisi alırsınız.
>
>

Komutu aşağıdaki hello kullanarak hello sanal ağ geçirebilirsiniz, ilk olarak, doğrulama:

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

Merhaba önceki komutu tüm uyarıları ve geçiş engelleme hataları görüntüler. Doğrulama başarılı olursa, hazırlama adımı aşağıdaki hello ile devam edebilirsiniz:

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

Sanal makineler Azure PowerShell veya hello Azure portal kullanarak hazırlanmış hello için başlangıç yapılandırmasını denetleyin. Geçiş için hazır olmayan ve toogo geri toohello eski durum istiyorsanız hello aşağıdaki komutu kullanın:

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

Merhaba hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve komut aşağıdaki hello kullanarak hello kaynakları Yürüt:

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a>Adım 6.2 geçirme bir depolama hesabı
Merhaba sanal makinelerin geçirilmesine bitirdiğinizde hello depolama hesapları geçirme öneririz.

Merhaba depolama hesabı geçirmeden önce önkoşul denetimleri önceki gerçekleştirin:

* **Klasik sanal makineleri, diskler hello depolama hesabında depolanır**

    Önceki komutu tüm hello Klasik VM diskleri RoleName ve DiskName özelliklerini hello depolama hesabında döndürür. RoleName bir diskin eklendiği hello sanal makine toowhich hello adıdır. Komut önceki diskleri sonra olun bu diskleri eklenir, sanal makineleri toowhich geçirmeden önce geçirilir döndürürse hello depolama hesabı.
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* **Merhaba depolama hesabında depolanan eklenmemiş Klasik VM diskleri silme**

    Merhaba depolama Klasik eklenmemiş VM diskleri komutu kullanarak hesap bulun:

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    Komut döndürür diskleri ardından komutu kullanarak bu diskleri silerseniz:

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* **Sil VM görüntüleri Hello depolama hesabında depolanan**

    Önceki komutu tüm hello VM görüntüleri hello depolama hesabında depolanan işletim sistemi diski ile döndürür.
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     Komut önceki hello depolama hesabında depolanan veri diskleri içeren tüm hello VM görüntüleri döndürür.
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    Önceki komutu kullandıktan komutları tarafından döndürülen tüm hello VM görüntüleri silin:
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

Her Depolama hesabı geçiş için komutu aşağıdaki hello kullanarak doğrulayın. Bu örnekte, hello depolama hesabı adı olan **myStorageAccount**. Merhaba örnek adı hello kendi depolama hesabınızın adıyla değiştirin.

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

Geçiş için tooPrepare hello depolama hesabı sonraki adımdır

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

Depolama hesabı Azure PowerShell veya hello Azure portal kullanarak hazırlanmış hello için başlangıç yapılandırmasını denetleyin. Geçiş için hazır olmayan ve toogo geri toohello eski durum istiyorsanız hello aşağıdaki komutu kullanın:

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

Merhaba hazırlanan yapılandırma iyi görünüyorsa, ilerlemek ve komut aşağıdaki hello kullanarak hello kaynakları Yürüt:

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a>Sonraki adımlar
* [Klasik tooAzure Resource Manager Iaas kaynaklardan platform desteklenen geçişini genel bakış](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Teknik ya ilişkin ayrıntılar platform desteklenen geçiş Klasik tooAzure Kaynak Yöneticisi'nden](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini planlama](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI toomigrate Iaas kaynaklarına Klasik tooAzure Kaynak Yöneticisi'ni kullanın](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Iaas kaynaklardan Klasik tooAzure Kaynak Yöneticisi geçişini ile Yardım için topluluk araçları](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [En sık karşılaşılan geçiş hatalarını gözden geçirme](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Gözden geçirme hello en sık Klasik tooAzure Kaynak Yöneticisi geçirme Iaas kaynaklardan hakkında sorular](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
