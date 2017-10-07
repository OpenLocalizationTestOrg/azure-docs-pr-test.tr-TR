---
title: "aaaUpload generalize VHD toocreate Azure birden çok VM | Microsoft Docs"
description: "Bir genelleştirilmiş VHD tooan Azure depolama hesabı toocreate hello Resource Manager dağıtım modeli içeren bir Windows VM toouse karşıya yükleyin."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a>Genelleştirilmiş bir VHD tooAzure toocreate yeni bir VM karşıya yükle

Bu konu, bir genelleştirilmiş yönetilmeyen disk tooa depolama hesabı karşıya yükleme ve karşıya hello diski kullanarak yeni bir VM oluşturma kapsar. Genelleştirilmiş bir VHD görüntüsü tüm kişisel hesap bilgilerinizi Sysprep kullanılarak kaldırılıncaya oluşturdu. 

Toocreate özel bir VHD depolama hesabındaki bir VM'den istiyorsanız, bkz: [özelleştirilmiş bir VHD'den bir VM oluşturma](sa-create-vm-specialized.md).

Depolama hesaplarını kullanarak bu konu şunları içerir, ancak bunun yerine müşteriler toousing yönetilen diskleri taşırken öneririz. Yönetilen disklerde nasıl tooprepare, karşıya yükleme ve kullanarak yeni bir VM oluşturmak eksiksiz bir kılavuz için bkz: [oluşturma yönetilen diskleri kullanılarak genelleştirilmiş bir VHD karşıya tooAzure yeni VM'den](upload-generalized-managed.md).



## <a name="prepare-hello-vm"></a>Merhaba VM hazırlama

Genelleştirilmiş bir VHD tüm kişisel hesap bilgilerinizi Sysprep kullanılarak kaldırılıncaya oluşturdu. Toouse hello VHD görüntüsü toocreate olarak amaçlıyorsanız, yeni VM'lerin, aşağıdakileri yapmalısınız:
  
  * [Bir Windows VHD tooupload tooAzure hazırlama](prepare-for-upload-vhd-image.md). 
  * Sysprep kullanarak Hello sanal makine generalize

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a>Sysprep kullanarak bir Windows sanal makine generalize
Bu bölümde, nasıl gösterilir toogeneralize Windows sanal makinenizi bir resim olarak kullanılacak. Sysprep tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılan hello makine toobe hazırlar. Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx).

Merhaba makine üzerinde çalışan hello sunucu rolleri Sysprep tarafından desteklendiğinden emin olun. Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Sysprep, VHD tooAzure hello için karşıya yüklemeden önce ilk kez çalıştırıyorsanız olduğundan emin olun [VM'nizi hazırlanmış](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep çalıştırılmadan önce. 
> 
> 

1. Windows sanal makine içinde toohello imzalayın.
2. Merhaba komut istemi penceresi bir yönetici olarak açın. Merhaba dizini çok değiştirmek**%windir%\system32\sysprep**ve ardından çalıştırın `sysprep.exe`.
3. Merhaba, **Sistem Hazırlama aracı** iletişim kutusunda **girin sistem Out-of-Box deneyimi (OOBE)**ve bu hello emin olun **Generalize** onay kutusu seçilidir.
4. İçinde **kapatma seçenekleri**seçin **kapatma**.
5. **Tamam** düğmesine tıklayın.
   
    ![Sysprep Başlat](./media/upload-generalized-managed/sysprepgeneral.png)
6. Sysprep tamamlandığında hello sanal makineyi kapatır. 

> [!IMPORTANT]
> Karşıya yükleme Bitti'yi hello VHD tooAzure veya VM hello bir görüntü oluşturma olana kadar hello VM yeniden başlatmayın. Merhaba VM yanlışlıkla yeniden, Sysprep toogeneralize çalışır. yeniden.
> 
> 


## <a name="upload-hello-vhd"></a>Merhaba VHD karşıya yükle

Merhaba VHD tooan Azure depolama hesabı karşıya yükleyin.

### <a name="log-in-tooazure"></a>İçinde tooAzure oturum
PowerShell sürüm 1.4 zaten yoksa veya üstü yüklü okuma [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

1. Azure PowerShell'i açın ve tooyour Azure hesabı oturum açın. Açılır pencere, tooenter Azure hesabı kimlik bilgilerinizi açar.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Merhaba abonelik kimlikleri kullanılabilir aboneliklerinizi alın.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Merhaba doğru aboneliğin Hello abonelik kimliğini kullanarak ayarlayın Değiştir `<subscriptionID>` hello hello Kimliğine sahip abonelik düzeltin.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

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
 
### <a name="start-hello-upload"></a>Başlangıç hello karşıya yükleme 

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


## <a name="create-a-new-vm"></a>Yeni bir VM oluşturun 

VHD toocreate yeni bir VM kullanım hello karşıya artık kullanabilirsiniz. 

### <a name="set-hello-uri-of-hello-vhd"></a>Merhaba hello VHD URI'si ayarlayın

Merhaba URI hello VHD toouse hello biçiminde olan: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd. Bu örnekte adlı VHD hello **myVHD** hello depolama hesabında **mystorageaccount** hello kapsayıcısında **mycontainer**.

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a>Sanal ağ oluşturma
Merhaba vNet ve alt hello oluşturma [sanal ağ](../../virtual-network/virtual-networks-overview.md).

1. Merhaba alt ağ oluşturun. Merhaba aşağıdaki örnek adlı bir alt ağı oluşturur **mySubnet** hello kaynak grubunda **myResourceGroup** hello adres öneki ile **10.0.0.0/24**.  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Merhaba sanal ağ oluşturun. Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur **myVnet** hello içinde **Batı ABD** hello adres öneki konumla **10.0.0.0/16**.  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a>Ortak IP adresi ve ağ arabirimi oluşturma
ihtiyacınız tooenable iletişimi hello sanal ağındaki hello sanal makineyle bir [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) ve ağ arabirimi.

1. Bir ortak IP adresi oluşturun. Bu örnek adlı ortak IP adresi oluşturur **myPip**. 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. Merhaba NIC oluşturun Bu örnek, adlandırılmış bir NIC oluşturur **myNic**. 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Merhaba ağ güvenlik grubu ve bir RDP kuralı oluşturma
toobe mümkün toolog tooyour içinde RDP kullanarak VM toohave 3389 numaralı bağlantı noktası üzerinde RDP erişimine izin veren bir güvenlik kuralı gerekir. 

Bu örnekte adlı bir NSG oluşturulur **myNsg** adlı kuralı içeren **myRdpRule** 3389 numaralı bağlantı noktası RDP trafiğine izin veren. Nsg'ler hakkında daha fazla bilgi için bkz: [bağlantı noktalarını tooa VM PowerShell kullanarak Azure içinde açma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a>Merhaba sanal ağ için bir değişken oluşturma
Tamamlanan hello sanal ağ için bir değişken oluşturun. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a>Merhaba VM oluşturma
Merhaba aşağıdaki PowerShell betiğini nasıl hello yeni yükleme için hello kaynak olarak VM görüntüsü tooset hello sanal makine yapılandırmaları ve kullanım hello karşıya gösterir.



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a>VM oluşturulduğu bu hello doğrulayın
Tamamlandığında, yeni VM hello oluşturulan hello görmelisiniz [Azure portal](https://portal.azure.com) altında **Gözat** > **sanal makineleri**, veya hello aşağıdakileri kullanarak PowerShell komutları:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Sonraki adımlar
Yeni sanal makinenizi Azure PowerShell ile toomanage bkz [Azure Resource Manager ve PowerShell kullanarak sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


