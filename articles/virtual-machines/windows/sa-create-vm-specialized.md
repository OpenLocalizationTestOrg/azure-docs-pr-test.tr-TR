---
title: "Azure özel bir diskten VM aaaCreate | Microsoft Docs"
description: "Merhaba Resource Manager dağıtım modelinde bir özelleştirilmiş yönetilmeyen disk ekleyerek yeni bir VM oluşturun."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a>Bir depolama hesabında özelleştirilmiş bir VHD'den bir VM oluşturma

Powershell kullanarak hello işletim sistemi diski olarak özel bir yönetilmeyen disk ekleyerek yeni bir VM oluşturun. Özelleştirilmiş bir disk hello kullanıcı hesapları, uygulamaları ve diğer Durum verilerini orijinal VM tutar mevcut bir VM'yi VHD'den kopyasıdır. 

İki seçeneğiniz vardır:
* [Bir VHD’yi karşıya yükleme](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [Merhaba mevcut bir Azure VM'i VHD kopyalayın](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a>Başlamadan önce
PowerShell'i kullanırsanız, hello hello AzureRM.Compute PowerShell modülü en son sürümüne sahip olduğunuzdan emin olun. Çalıştırma hello komut tooinstall onu.

```powershell
Install-Module AzureRM.Compute 
```
Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).


## <a name="option-1-upload-a-specialized-vhd"></a>Seçenek 1: özel bir VHD yüklemek

Hyper-V ya da VM başka bir buluttan dışarı gibi bir şirket içi sanallaştırma aracı ile özel bir VM VHD'den oluşturulan hello karşıya yükleyebilirsiniz.

### <a name="prepare-hello-vm"></a>Merhaba VM hazırlama
Bir şirket içi VM veya başka bir buluttan dışa aktarılan bir VHD kullanılarak oluşturulmuş özel bir VHD karşıya yükleyebilirsiniz. Özel bir VHD hello kullanıcı hesapları, uygulamaları ve diğer Durum verilerini orijinal VM tutar. Toouse düşünüyorsanız, VHD olarak hello-toocreate yeni bir VM olan aşağıdaki adımları hello tamamlanır emin olun. 
  
  * [Bir Windows VHD tooupload tooAzure hazırlama](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). **Sağlamadığı** generalize Sysprep kullanarak VM hello.
  * Konuk sanallaştırma araçları ve hello VM (yani VMware araçları) üzerinde yüklü aracıları kaldırın.
  * Merhaba VM olun yapılandırılmış toopull kendi IP adresini ve DNS ayarlarını DHCP yoluyla değil. Bu başladığında hello sunucu hello VNet içindeki bir IP adresi alacağı sağlar. 


### <a name="get-hello-storage-account"></a>Merhaba depolama hesabı edinin
Azure toostore karşıya hello VM görüntüsündeki bir depolama hesabı gerekir. Mevcut bir depolama hesabını kullanabilir veya yeni bir tane oluşturun. 

tooshow hello kullanılabilir depolama hesaplarını yazın:

```powershell
Get-AzureRmStorageAccount
```

Mevcut bir depolama hesabını toouse istiyorsanız, toohello devam [karşıya yükleme hello VM görüntüsü](#upload-the-vm-vhd-to-your-storage-account) bölümü.

Bir depolama hesabı toocreate gerekiyorsa, şu adımları izleyin:

1. Merhaba hello depolama hesabı nerede oluşturulacağını hello kaynak grubunun adını gerekir. toofind, aboneliğinizdeki türü tüm hello kaynak gruplarını çıkışı:
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    bir kaynak grubu adında toocreate **myResourceGroup** hello içinde **Batı ABD** bölge, türü:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. Adlı depolama hesabı oluşturma **mystorageaccount** hello kullanarak bu kaynak grubundaki [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a>Merhaba VHD tooyour depolama hesabı karşıya yükle
Kullanım hello [Ekle AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) depolama hesabınızdaki cmdlet tooupload hello görüntü tooa kapsayıcı. Karşıya dosya hello Bu örnek **myVHD.vhd** gelen `"C:\Users\Public\Documents\Virtual hard disks\"` adlı tooa depolama hesabı **mystorageaccount** hello içinde **myResourceGroup** kaynak grubu. Merhaba dosya adlı hello kapsayıcıya yerleştirilecek **mycontainer** ve hello yeni dosya adı olacaktır **myUploadedVHD.vhd**.

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
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

Bu komut, ağ bağlantısı ve VHD dosyanızı hello boyutuna bağlı olarak biraz zaman alabilir toocomplete.


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a>Seçenek 2: Kopyalama hello mevcut bir Azure VM'i VHD'den

Yeni, yinelenen bir VM oluştururken, bir VHD tooanother depolama hesabı toouse kopyalayabilirsiniz.

### <a name="before-you-begin"></a>Başlamadan önce
Olduğundan emin olun:

* Merhaba ilgili bilgiler **kaynak ve hedef depolama hesapları**. Merhaba kaynak VM toohave hello depolama hesabı ve kapsayıcı adları olması gerekir. Genellikle, hello kapsayıcı adı olacaktır **VHD'ler**. Ayrıca toohave bir hedef depolama hesabı gerekir. Zaten yoksa, her iki hello portalı kullanarak bir tane oluşturabilirsiniz (**daha Hizmetleri** > depolama hesapları > Ekle) veya hello kullanarak [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet'i. 
* İndirilen ve hello yüklenmiş [AzCopy aracı](../../storage/common/storage-use-azcopy.md). 

### <a name="deallocate-hello-vm"></a>Merhaba VM serbest bırakma
Merhaba kopyalanan hello VHD toobe boşaltır VM serbest bırakma. 

* **Portal**: tıklatın **sanal makineleri** > **myVM** > Durdur
* **PowerShell**: kullanım [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) adlı VM hello **myVM** kaynak grubunda **myResourceGroup**.

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

Merhaba **durum** hello Azure VM hello için portal değişiklikleri **durduruldu** çok**durduruldu (serbest bırakıldı)**.

### <a name="get-hello-storage-account-urls"></a>Merhaba depolama hesabı URL'lerini alma
Merhaba kaynak ve hedef depolama hesapları hello URL'lerini gerekir. Merhaba URL'leri neye benzediğini gösteren: `https://<storageaccount>.blob.core.windows.net/<containerName>/`. Merhaba depolama hesabı ve kapsayıcı adını biliyorsanız, hello köşeli toocreate arasında hello bilgi URL'nizi yalnızca değiştirebilirsiniz. 

Hello Azure portalında veya Azure Powershell tooget hello URL kullanabilirsiniz:

* **Portal**: tıklatın hello  **>**  için **daha fazla hizmet** > **depolama hesapları**  >   *Depolama hesabı* > **BLOB'lar** ve kaynak VHD dosyası büyük olasılıkla hello **VHD'ler** kapsayıcı. Tıklatın **özellikleri** hello kapsayıcı ve etiketli hello metin Kopyala **URL**. Her iki hello kaynak ve hedef kapsayıcılarını hello URL'lerini gerekir. 
* **PowerShell**: kullanım [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello bilgi adlı VM için **myVM** hello kaynak grubunda **myResourceGroup**. Merhaba sonuçlarında hello Ara **depolama profili** hello bölümüne **Vhd Uri'si**. Merhaba ilk hello URI hello URL toohello kapsayıcı bir parçasıdır ve hello son hello hello VM için işletim sistemi VHD ad parçasıdır.

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a>Merhaba depolama erişim anahtarı alma
Merhaba erişim tuşları hello için kaynak ve hedef depolama hesapları bulun. Erişim anahtarları hakkında daha fazla bilgi için bkz: [Azure storage hesapları hakkında](../../storage/common/storage-create-storage-account.md).

* **Portal**: tıklatın **daha fazla hizmet** > **depolama hesapları** > *depolama hesabı*  >  **Erişim anahtarları**. Kopya hello anahtar etiketli olarak **key1**.
* **PowerShell**: kullanım [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello depolama anahtarı hello depolama hesabı için **mystorageaccount** hello kaynak grubunda  **myResourceGroup**. Etiketli kopyalama hello anahtar **key1**.

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a>Merhaba VHD kopyalayın
AzCopy kullanarak depolama hesapları arasında dosya kopyalayabilirsiniz. Merhaba belirtilen kapsayıcı mevcut değilse hello hedef kapsayıcı için sizin için oluşturulur. 

toouse AzCopy, yerel makinenizde bir komut istemi açın ve AzCopy yüklendiği toohello klasörüne gidin. Bu çok benzer olacaktır*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*. 

Tüm hello dosyaları bir kapsayıcıda toocopy kullandığınız hello **/S** geçin. Bu kullanılan toocopy hello OS VHD olabilir ve kullanılıyorlarsa hello veri disklerin tümü aynı kapsayıcı hello. Bu örnekte gösterilir nasıl tüm hello dosyaları hello kapsayıcısında toocopy **mysourcecontainer** depolama hesabındaki **mysourcestorageaccount** toohello kapsayıcı **mydestinationcontainer**  hello içinde **mydestinationstorageaccount** depolama hesabı. Merhaba depolama hesapları ve kapsayıcıları Hello adlarını kendi ile değiştirin. Değiştir `<sourceStorageAccountKey1>` ve `<destinationStorageAccountKey1>` kendi anahtarlara sahip.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

Toocopy belirli bir VHD'yi bir kapsayıcıda yalnızca sahip birden çok dosya istiyorsanız, ayrıca hello /Pattern anahtar kullanılarak hello dosya adını belirtebilirsiniz. Bu örnekte, yalnızca adlı dosya hello **myFileName.vhd** kopyalanacak.

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


Tamamlandığında, aşağıdakine benzer bir ileti alırsınız:

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a>Sorun giderme
* Merhaba hatası görürseniz, AZCopy, "Sunucu tooauthenticate hello isteği başarısız oldu" kullandığınızda hello Authorization Üstbilgisi hello değeri doğru hello imza dahil olmak üzere biçimlendirildiğinden emin olun. Anahtar 2 veya hello ikincil depolama anahtarı kullanıyorsanız, hello birincil ya da 1 depolama anahtarı kullanmayı deneyin.

## <a name="create-hello-new-vm"></a>Oluşturma yeni VM hello 

Toocreate ağ ve hello tarafından kullanılan diğer VM kaynakları toobe gereken yeni VM.

### <a name="create-hello-subnet-and-vnet"></a>Merhaba alt ağ ve sanal ağ oluşturma

Merhaba vNet ve alt hello oluşturma [sanal ağ](../../virtual-network/virtual-networks-overview.md).

1. Merhaba alt ağ oluşturun. Bu örnek adlı bir alt ağı oluşturur **mySubNet**, hello kaynak grubunda **myResourceGroup**, ve ayarlar hello alt ağ adresi ön eki çok**10.0.0.0/24**.
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Merhaba vNet oluşturun. Ayarlar hello sanal ağ adı toobe Bu örnek **myVnetName**, konum çok hello**Batı ABD**, ve hello sanal ağ için adres ön eki çok hello**10.0.0.0/16**. 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a>Bir ortak IP adresi ve NIC oluşturun
ihtiyacınız tooenable iletişimi hello sanal ağındaki hello sanal makineyle bir [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) ve ağ arabirimi.

1. Merhaba genel IP oluşturun. Bu örnekte hello ortak IP adresi adı çok ayarlanır**myIP**.
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Merhaba NIC oluşturun Bu örnekte, hello NIC adı çok ayarlanır**myNicName**.
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Merhaba ağ güvenlik grubu ve bir RDP kuralı oluşturma
toobe mümkün toolog tooyour içinde RDP kullanarak VM toohave 3389 numaralı bağlantı noktası üzerinde RDP erişimine izin veren bir güvenlik kuralı gerekir. Yeni VM mevcut bir oluşturulduğu hello Merhaba VHD özelleştirilmiş çünkü hello VM, oluşturulduktan sonra VM hello kaynak sanal makineden RDP kullanma izni toolog sahip var olan bir hesap kullanabilirsiniz.
Bu örnek kümeleri hello NSG adı çok**myNsg** ve hello RDP kural adı çok**myRdpRule**.

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

Uç noktaları ve NSG kuralları hakkında daha fazla bilgi için bkz: [bağlantı noktalarını tooa VM PowerShell kullanarak Azure içinde açma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="set-hello-vm-name-and-size"></a>Merhaba sanal makine adını ve boyutunu ayarlama

Ayarlar hello VM adını bu örnek çok "myVM" ve hello VM çok boyutu "Standard_A2".
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>Merhaba NIC ekleme
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a>Merhaba işletim sistemi diski yapılandırın

1. Merhaba URI hello karşıya veya kopyalanan VHD için ayarlayın. Bu örnekte, VHD dosyası adlı hello **myOsDisk.vhd** adlı bir depolama hesabında tutulur **myStorageAccount** adlı bir kapsayıcıda **myContainer**.

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. Merhaba işletim sistemi diski ekleyin. Hello işletim sistemi diski oluşturulduğunda bu örnekte, appened toohello VM toocreate hello işletim sistemi disk adı hello terimi "osDisk" şeklindedir. Bu örnek ayrıca bu Windows tabanlı VHD ekli toohello hello işletim sistemi diski olarak VM olması gerektiğini belirtir.
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

İsteğe bağlı: veri diski varsa, bu gereksinimi toobe toohello VM ekli veri VHD'ler hello URL'leri kullanarak hello veri diski ekleyin ve uygun mantıksal birim numarası (Lun) hello.

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

Bir depolama hesabı kullanılırken hello veri ve işletim sistemi disk URL'leri aşağıdaki gibi görünmelidir: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`. Bu hello portalında toohello hedef depolama kapsayıcısı hello işletim sistemi veya veri kopyalanan VHD tıklatarak, tarama ve hello URL Merhaba içeriğine kopyalama bulabilirsiniz.


### <a name="complete-hello-vm"></a>Tam hello VM 

Oluşturma yeni oluşturduğumuz hello yapılandırmaları kullanarak VM hello.

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
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
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a>Sonraki adımlar
tooyour yeni sanal makine, hello içinde Gözat toohello VM toosign [portal](https://portal.azure.com), tıklatın **Bağlan**ve açık hello Uzak Masaüstü RDP dosyası. Özgün sanal makine toosign Hello hesabı kimlik bilgilerini tooyour yeni sanal makinede kullanın. Daha fazla bilgi için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](connect-logon.md).

