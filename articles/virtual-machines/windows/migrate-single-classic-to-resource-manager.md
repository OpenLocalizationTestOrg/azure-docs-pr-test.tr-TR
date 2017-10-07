---
title: "aaaMigrate Klasik VM tooan ARM yönetilen Disk VM | Microsoft Docs"
description: "Tek bir Azure VM'ye hello Klasik dağıtımını geçirdikten tooManaged diskleri hello Resource Manager dağıtım modelinde model."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: cynthn
ms.openlocfilehash: d8c4b9431f5dd8a071fcbc2ee36581a33f76ba62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manually-migrate-a-classic-vm-tooa-new-arm-managed-disk-vm-from-hello-vhd"></a>Klasik VM tooa el ile geçirme yeni ARM yönetilen diski sanal makineden hello VHD 


Bu bölümde, toomigrate mevcut Azure Vm'leriniz hello Klasik dağıtım modelinden çok yardımcı[yönetilen diskleri](managed-disks-overview.md) hello Resource Manager dağıtım modelinde.


## <a name="plan-for-hello-migration-toomanaged-disks"></a>Plan hello geçiş için tooManaged diskleri

Bu bölümde, VM ve disk türleri hakkında toomake hello en iyi karar yardımcı olur.


### <a name="location"></a>Konum

Azure yönetilen diskleri kullanılabildiği bir konum seçin. TooPremium yönetilen diskleri geçiriyorsanız, ayrıca Premium depolama burada toomigrate için planlama hello bölgede kullanılabilir olduğundan emin olun. Bkz: [Azure Hizmetleri byRegion](https://azure.microsoft.com/regions/#services) kullanılabilir konumları hakkında güncel bilgi.

### <a name="vm-sizes"></a>VM boyutları

TooPremium yönetilen diskleri geçiriyorsanız, VM bulunduğu hello bölgede tooupdate hello hello VM tooPremium depolama özellikli boyutu kullanılabilir boyutuna sahip. Premium depolama özellikli hello VM boyutları gözden geçirin. Hello Azure VM boyutu belirtimleri içinde listelenen [sanal makineler için Boyutlar](sizes.md).
Premium Storage ile birlikte çalışmak ve işleminizi iş yükü en çok uyan hello en uygun VM boyutunu seçin sanal makineleri Hello performans özellikleri gözden geçirin. Yeterli bant genişliği kullanılabilir VM toodrive hello disk trafiğinde bulunduğundan emin olun.

### <a name="disk-sizes"></a>Disk boyutları

**Premium yönetilen diskleri**

Yedi disk türleri için VM ile kullanılabilen premium yönetilen vardır ve her belirli IOPS ve üretilen iş sahip sınırlar. Bu sınırlar yoğun yükler ve kapasite, performans, ölçeklenebilirlik açısından, uygulamanızın hello gereksinimlerine hello Premium disk türü, VM için temel seçerken göz önünde bulundurun.

| Premium diskler türü  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Disk boyutu           | 128 GB| 512 GB| 128 GB| 512 GB            | 1024 GB (1 TB)    | 2048 GB (2 TB)    | 4095 GB (4 TB)    | 
| Disk başına IOPS       | 120   | 240   | 500   | 2300              | 5000              | 7500              | 7500              | 
| Disk başına aktarım hızı | Saniye başına 25 MB  | Saniye başına 50 MB  | Saniyede 100 MB | 150 MB / saniye | 200 MB / saniye | Saniye başına 250 MB | Saniye başına 250 MB | 

**Standart yönetilen disk**

VM ile kullanılabilecek standart yönetilen disk yedi türü vardır. Bunların her biri farklı kapasiteye sahip ancak aynı IOPS ve üretilen iş sınırı vardır. Standart yönetilen disk uygulamanızın hello kapasite gereksinimlerine göre Hello türünü seçin.

| Standart Disk Türü  | S4               | S6               | S10              | S20              | S30              | S40              | S50              | 
|---------------------|---------------------|---------------------|------------------|------------------|------------------|------------------|------------------| 
| Disk boyutu           | 30 GB            | 64 GB            | 128 GB           | 512 GB           | 1024 GB (1 TB)   | 2048 GB (2TB)    | 4095 GB (4 TB)   | 
| Disk başına IOPS       | 500              | 500              | 500              | 500              | 500              | 500             | 500              | 
| Disk başına aktarım hızı | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB | Saniye başına 60 MB | 


### <a name="disk-caching-policy"></a>Önbellek İlkesi disk 

**Premium yönetilen diskleri**

Varsayılan olarak, ilke önbelleğe alma disktir *salt okunur* tüm Premium diskleri hello için ve *okuma-yazma* hello Premium işletim sistemi diski için toohello VM bağlı. Bu yapılandırma ayarının tooachieve hello en iyi performans için uygulamanızın IOs önerilir. (SQL Server günlük dosyaları gibi) ağır yazma ya da salt yazılır veri diskleri için daha iyi uygulama performansı elde etmek için disk önbelleğe almayı devre dışı bırakın.

### <a name="pricing"></a>Fiyatlandırma

Gözden geçirme hello [yönetilen diskler için fiyatlandırma](https://azure.microsoft.com/en-us/pricing/details/managed-disks/). Premium diskler yönetilen fiyatlandırma hello Premium yönetilmeyen diskleri aynıdır. Ancak standart yönetilen disk için fiyatlandırma standart yönetilmeyen disklerden farklı.


## <a name="checklist"></a>Denetim listesi

1.  TooPremium yönetilen diskleri geçiriyorsanız, bu için geçirdiğiniz hello bölgede kullanılabilir olduğundan emin olun.

2.  Merhaba, kullanarak yeni VM dizisi karar verin. TooPremium yönetilen diskleri geçiriyorsanız, Premium depolama özelliğine sahip olmalıdır.

3.  Geçirmekte olduğunuz hello bölgede kullanılabilir olan kullanacağınız hello tam VM boyutu karar verin. VM boyutu toobe büyüklükte toosupport hello sahip veri diski sayısı gerekir. Örneğin, dört veri diski varsa, hello VM iki veya daha fazla çekirdek olması gerekir. Ayrıca, işlemci gücü, bellek göz önünde bulundurun ve ağ bant genişliği gerekiyor.

4.  Merhaba geçerli VM ayrıntıları hello disklerin listesini ve karşılık gelen VHD BLOB'ları da dahil olmak üzere kullanışlı vardır.

Uygulamanızı kapalı kalma süresi için hazırlayın. toodo temiz bir geçiş, toostop hello geçerli sistemi tüm hello işleme sahip. Ancak bundan sonra geçirebileceğiniz tooconsistent durumu alabilirsiniz toohello yeni platformu. Kapalı kalma süresi hello hello diskleri toomigrate veri miktarına bağlıdır.


## <a name="migrate-hello-vm"></a>Merhaba VM geçirme

Uygulamanızı kapalı kalma süresi için hazırlayın. toodo temiz bir geçiş, toostop hello geçerli sistemi tüm hello işleme sahip. Ancak bundan sonra geçirebileceğiniz tooconsistent durumu alabilirsiniz toohello yeni platformu. Kapalı kalma süresi hello hello diskleri toomigrate veri miktarına bağlıdır.


1.  İlk olarak, hello ortak parametreleri ayarlayın:

    ```powershell
    $resourceGroupName = 'yourResourceGroupName'
    
    $location = 'your location' 
    
    $virtualNetworkName = 'yourExistingVirtualNetworkName'
    
    $virtualMachineName = 'yourVMName'
    
    $virtualMachineSize = 'Standard_DS3'
    
    $adminUserName = "youradminusername"
    
    $adminPassword = "yourpassword" | ConvertTo-SecureString -AsPlainText -Force
    
    $imageName = 'yourImageName'
    
    $osVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd'
    
    $dataVhdUri = 'https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk1.vhd'
    
    $dataDiskName = 'dataDisk1'
    ```

2.  Merhaba VHD hello gelen kullanarak yönetilen bir işletim sistemi diski oluşturma Klasik VM.

    Merhaba tamamlamak sağlanan hello OS VHD toohello $osVhdUri parametresi URI'sini, olduğundan emin olun. Ayrıca, girin **- AccountType** olarak **PremiumLRS** veya **StandardLRS** temel diskleri (Premium veya standart) türüne için geçirdiğiniz.

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $osVhdUri) '
    -ResourceGroupName $resourceGroupName
    ```

3.  Merhaba işletim sistemi disk toohello ekleme yeni VM.

    ```powershell
    $VirtualMachine = New-AzureRmVMConfig -VMName $virtualMachineName -VMSize $virtualMachineSize
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -ManagedDiskId $osDisk.Id '
    -StorageAccountType PremiumLRS -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

4.  Yönetilen veri diski hello veri VHD dosyası oluşturun ve toohello ekleyin yeni VM.

    ```powershell
    $dataDisk1 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig '
    -AccountType PremiumLRS -Location $location -CreationDataCreateOption Import '
    -SourceUri $dataVhdUri ) -ResourceGroupName $resourceGroupName
    
    $VirtualMachine = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName '
    -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
    ```

5.  Oluşturma genel IP, sanal ağ ve NIC ayarlayarak yeni VM hello

    ```powershell
    $publicIp = New-AzureRmPublicIpAddress -Name ($VirtualMachineName.ToLower()+'_ip') '
    -ResourceGroupName $resourceGroupName -Location $location -AllocationMethod Dynamic
    
    $vnet = Get-AzureRmVirtualNetwork -Name $virtualNetworkName -ResourceGroupName $resourceGroupName
    
    $nic = New-AzureRmNetworkInterface -Name ($VirtualMachineName.ToLower()+'_nic') '
    -ResourceGroupName $resourceGroupName -Location $location -SubnetId $vnet.Subnets[0].Id '
    -PublicIpAddressId $publicIp.Id
    
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $nic.Id
    
    New-AzureRmVM -VM $VirtualMachine -ResourceGroupName $resourceGroupName -Location $location
    ```

> [!NOTE]
>Ek adımlar gerekli toosupport olabilir, uygulama değil Bu kılavuz kapsamında.
>
>

## <a name="next-steps"></a>Sonraki adımlar

- Toohello sanal makineye bağlanın. Yönergeler için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

