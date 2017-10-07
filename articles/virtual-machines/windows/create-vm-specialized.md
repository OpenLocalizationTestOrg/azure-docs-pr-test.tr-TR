---
title: "bir Windows VM Azure özelleştirilmiş bir VHD'den aaaCreate | Microsoft Docs"
description: "Yeni bir Windows VM hello Resource Manager dağıtım modeli kullanılarak hello işletim sistemi diski olarak özel bir yönetilen disk ekleyerek oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a>Özelleştirilmiş bir diskten bir Windows VM oluşturma

Powershell kullanarak hello işletim sistemi diski olarak özel bir yönetilen disk ekleyerek yeni bir VM oluşturun. Özelleştirilmiş bir disk hello kullanıcı hesapları, uygulamaları ve diğer Durum verilerini orijinal VM tutar mevcut bir VM'yi sanal sabit disk (VHD) bir kopyasını arasındadır. 

Özel bir VHD toocreate yeni bir VM kullandığınızda, yeni VM hello bilgisayar adını korur hello özgün VM hello. Diğer bilgisayar özgü bilgiler de olması tutulur ve bazı durumlarda, bu yinelenen bilgiler sorunlara neden. Ne tür bilgisayara özgü bilgileri uygulamalarınızı VM kopyalarken kullanır dikkat edin.

İki seçeneğiniz vardır:
* [Bir VHD’yi karşıya yükleme](#option-1-upload-a-specialized-vhd)
* [Mevcut bir Azure VM'yi kopyalama](#option-2-copy-an-existing-azure-vm)

Bu konu toouse diskleri nasıl yönetileceğini gösterir. Eski dağıtım varsa gerektiren bir depolama hesabı kullanarak, bkz: [depolama hesabındaki özelleştirilmiş bir VHD'den bir VM oluşturma](sa-create-vm-specialized.md)

## <a name="before-you-begin"></a>Başlamadan önce
PowerShell'i kullanırsanız, hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun. 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Seçenek 1: özel bir VHD yüklemek

Hyper-V ya da VM başka bir buluttan dışarı gibi bir şirket içi sanallaştırma aracı ile özel bir VM VHD'den oluşturulan hello karşıya yükleyebilirsiniz.

### <a name="prepare-hello-vm"></a>Merhaba VM hazırlama
Toouse düşünüyorsanız, VHD olarak hello-toocreate yeni bir VM olan aşağıdaki adımları hello tamamlanır emin olun. 
  
  * [Bir Windows VHD tooupload tooAzure hazırlama](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Sağlamadığı** generalize Sysprep kullanarak VM hello.
  * Konuk sanallaştırma araçları ve hello VM (gibi VMware araçları) yüklenmiş aracıları kaldırın.
  * Merhaba VM olun yapılandırılmış toopull kendi IP adresini ve DNS ayarlarını DHCP yoluyla değil. Bu başladığında hello sunucu hello VNet içindeki bir IP adresi alacağı sağlar. 


### <a name="get-hello-storage-account"></a>Merhaba depolama hesabı edinin
Bir depolama alanına ihtiyacınız Azure toostore hello hesabında karşıya VHD. Mevcut bir depolama hesabını kullanabilir veya yeni bir tane oluşturun. 

tooshow hello kullanılabilir depolama hesaplarını yazın:

```powershell
Get-AzureRmStorageAccount
```

Mevcut bir depolama hesabını toouse istiyorsanız, toohello devam [karşıya yükleme hello VHD](#upload-the-vhd-to-your-storage-account) bölümü.

Bir depolama hesabı toocreate gerekiyorsa, şu adımları izleyin:

1. Merhaba hello depolama hesabı nerede oluşturulacağını hello kaynak grubunun adını gerekir. toofind, aboneliğinizdeki türü tüm hello kaynak gruplarını çıkışı:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    bir kaynak grubu adında toocreate *myResourceGroup* hello içinde *Batı ABD* bölge, türü:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Adlı depolama hesabı oluşturma *mystorageaccount* hello kullanarak bu kaynak grubundaki [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a>Merhaba VHD tooyour depolama hesabı karşıya yükle 
Kullanım hello [Ekle AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) depolama hesabınızdaki cmdlet tooupload hello VHD tooa kapsayıcı. Karşıya dosya hello Bu örnek *myVHD.vhd* gelen `"C:\Users\Public\Documents\Virtual hard disks\"` adlı tooa depolama hesabı *mystorageaccount* hello içinde *myResourceGroup* kaynak grubu. Merhaba dosya adlı hello kapsayıcısında depolanır *mycontainer* ve hello yeni dosya adı olacaktır *myUploadedVHD.vhd*.

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


Başarılı olursa, benzer toothis benzeyen bir yanıt alın:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

Bu komut, ağ bağlantısı ve VHD dosyanızı hello boyutuna bağlı olarak biraz zaman alabilir toocomplete

### <a name="create-a-managed-disk-from-hello-vhd"></a>VHD hello yönetilen bir disk oluşturun

Hello yönetilen bir disk oluşturma, depolama hesabı kullanarak VHD özelleştirilmiş [yeni AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk). Bu örnekte **myOSDisk1** hello disk adı için disk yerleştirmelerin hello *StandardLRS* depolama ve kullandığı *https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd* hello kaynak VHD URI hello gibi.

Hello için yeni bir kaynak grubu oluşturma yeni VM.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Oluşturma hello yeni işletim sistemi diskinden hello karşıya VHD. 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a>Seçenek 2: mevcut bir Azure VM'yi kopyalama

Bir hello VM anlık görüntüsü tarafından yönetilen disklerde kullanır ve ardından bu anlık görüntü toocreate kullanarak yeni bir disk ve yeni bir VM yönetilen VM bir kopyasını oluşturabilirsiniz.


### <a name="take-a-snapshot-of-hello-os-disk"></a>Merhaba işletim sistemi diski bir anlık görüntüsünü

(Tüm diskler dahil), anlık görüntü ve tüm VM alabilir veya yalnızca tek bir disk. Merhaba aşağıdaki adımlar, nasıl tootake bir anlık görüntü yalnızca VM kullanmanın hello işletim sistemi diskinin hello gösterir [yeni AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet'i. 

Bazı parametreler ayarlayın. 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

Merhaba VM nesnesini alın.

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
Merhaba işletim sistemi disk adı alın.

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

Başlangıç anlık görüntü yapılandırmasını oluşturun. 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

Başlangıç anlık görüntü alın.

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


Toouse hello anlık görüntü toocreate toobe yüksek performanslı gereken VM planlıyorsanız, hello parametresini kullanın `-AccountType Premium_LRS` hello yeni AzureRmSnapshot komutu. Merhaba parametre hello anlık görüntü oluşturur, böylece yönetilen bir Premium Disk depolanır. Premium yönetilen diskleri standart daha pahalıdır. Bu nedenle, Premium hello parametre kullanmadan önce gerçekten emin olun.

### <a name="create-a-new-disk-from-hello-snapshot"></a>Merhaba anlık görüntüden yeni bir disk oluşturma

Yönetilen bir disk kullanarak anlık görüntü hello oluşturma [yeni AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk). Bu örnekte *myOSDisk* hello disk adı.

Hello için yeni bir kaynak grubu oluşturma yeni VM.

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

Merhaba işletim sistemi disk adı ayarlayın. 

```powershell
$osDiskName = 'myOsDisk'
```

Merhaba yönetilen diski oluşturun.

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a>Oluşturma yeni VM hello 

Ağ ve hello tarafından kullanılan diğer VM kaynakları toobe oluşturmak yeni VM.

### <a name="create-hello-subnet-and-vnet"></a>Merhaba alt ağ ve sanal ağ oluşturma

Merhaba vNet ve alt hello oluşturma [sanal ağ](../../virtual-network/virtual-networks-overview.md).

Merhaba alt ağ oluşturun. Bu örnek adlı bir alt ağı oluşturur **mySubNet**, hello kaynak grubunda **myDestinationResourceGroup**, ve ayarlar hello alt ağ adresi ön eki çok**10.0.0.0/24**.
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

Merhaba vNet oluşturun. Ayarlar hello sanal ağ adı toobe Bu örnek **myVnetName**, konum çok hello**Batı ABD**, ve hello sanal ağ için adres ön eki çok hello**10.0.0.0/16**. 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Merhaba ağ güvenlik grubu ve bir RDP kuralı oluşturma
toobe mümkün toolog tooyour içinde RDP kullanarak VM toohave 3389 numaralı bağlantı noktası üzerinde RDP erişimine izin veren bir güvenlik kuralı gerekir. Çünkü yeni VM, var olan bir özel sanal makineden oluşturulduğu hello için VHD Merhaba, RDP hello kaynak sanal makineden bir hesap kullanabilirsiniz.

Bu örnek kümeleri hello NSG adı çok**myNsg** ve hello RDP kural adı çok**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Uç noktaları ve NSG kuralları hakkında daha fazla bilgi için bkz: [bağlantı noktalarını tooa VM PowerShell kullanarak Azure içinde açma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="create-a-public-ip-address-and-nic"></a>Bir ortak IP adresi ve NIC oluşturun
ihtiyacınız tooenable iletişimi hello sanal ağındaki hello sanal makineyle bir [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) ve ağ arabirimi.

Merhaba genel IP oluşturun. Bu örnekte hello ortak IP adresi adı çok ayarlanır**myIP**.
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

Merhaba NIC oluşturun Bu örnekte, hello NIC adı çok ayarlanır**myNicName**.
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a>Merhaba sanal makine adını ve boyutunu ayarlama

Bu örnek kümeleri hello VM adı çok*myVM* ve hello VM boyutu çok*Standard_A2*.

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Merhaba NIC ekleme
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a>Merhaba işletim sistemi disk ekleme 

Merhaba işletim sistemi disk yapılandırması toohello kullanılarak eklemek [kümesi AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk). Bu örnek hello hello disk boyutunu çok ayarlar*128 GB* ekler hello yönetilen diski olarak ve bir *Windows* işletim sistemi diski.
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a>Tam hello VM 

VM Hello kullanarak oluşturduğunuz [New-AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello yeni oluşturduğumuz yapılandırmaları.

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

Bu komutun başarılı olduysa, benzer bir çıktı görürsünüz:

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>VM oluşturulduğu bu hello doğrulayın
Merhaba yeni oluşturulan VM ya da hello görmelisiniz [Azure portal](https://portal.azure.com)altında **Gözat** > **sanal makineleri**, veya PowerShell aşağıdaki hello kullanarak komutlar:

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a>Sonraki adımlar
tooyour yeni sanal makine, hello içinde Gözat toohello VM toosign [portal](https://portal.azure.com), tıklatın **Bağlan**ve açık hello Uzak Masaüstü RDP dosyası. Özgün sanal makine toosign Hello hesabı kimlik bilgilerini tooyour yeni sanal makinede kullanın. Daha fazla bilgi için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](connect-logon.md).

