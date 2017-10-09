---
title: "yönetilen bir Azure VM genelleştirilmiş şirket içi VHD'den aaaCreate | Microsoft Docs"
description: "Genelleştirilmiş bir VHD tooAzure karşıya yükleme ve toocreate kullanmak hello Resource Manager dağıtım modelinde yeni VM'ler."
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a>Genelleştirilmiş bir VHD yüklemek ve toocreate kullanmak azure'da yeni VM

Bu konu, PowerShell tooupload kullanılarak üzerinden genelleştirilmiş bir VM tooAzure VHD'sini açıklanmaktadır, VHD hello bir görüntü oluşturun ve bu görüntüden yeni bir VM oluşturun. Bir şirket içi sanallaştırma aracı ya da başka bir bulut dışa aktarılan bir VHD'yi yükleyebilirsiniz. Kullanarak [yönetilen diskleri](managed-disks-overview.md) hello yeni VM hello VM yönetimini basitleştirir ve bir kullanılabilirlik kümesine hello VM yerleştirildiğinde daha iyi kullanılabilirlik sağlar. 

Toouse bir örnek komut dosyası istiyorsanız, bkz: [örnek komut dosyası tooupload VHD tooAzure ve yeni bir VM oluşturun](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)

## <a name="before-you-begin"></a>Başlamadan önce

- Tüm VHD tooAzure karşıya yüklemeden önce uygulamanız gereken [Windows VHD veya VHDX tooupload tooAzure hazırlama](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
- Gözden geçirme [planlama hello geçiş için tooManaged diskleri](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) çok geçişinizi başlatmadan önce[yönetilen diskleri](managed-disks-overview.md).
- Merhaba AzureRM.Compute PowerShell modülü hello en son sürümüne sahip olduğunuzdan emin olun. Çalıştırma hello komut tooinstall onu.

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).


## <a name="generalize-hello-windows-vm-using-sysprep"></a>Generalize Sysprep kullanarak Windows VM hello

Sysprep tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılan hello makine toobe hazırlar. Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx).

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
6. Sysprep tamamlandığında hello sanal makineyi kapatır. Merhaba VM yeniden başlatmayın.



## <a name="log-in-tooazure"></a>İçinde tooAzure oturum
PowerShell sürüm 1.4 zaten yoksa veya üstü yüklü okuma [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).

1. Azure PowerShell'i açın ve tooyour Azure hesabı oturum açın. Açılır pencere, tooenter Azure hesabı kimlik bilgilerinizi açar.
   
    ```powershell
    Login-AzureRmAccount
    ```
2. Merhaba abonelik kimlikleri kullanılabilir aboneliklerinizi alın.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Merhaba doğru aboneliğin Hello abonelik kimliğini kullanarak ayarlayın Değiştir  *<subscriptionID>*  hello hello Kimliğine sahip abonelik düzeltin.
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a>Merhaba depolama hesabı edinin
Azure toostore karşıya hello VM görüntüsündeki bir depolama hesabı gerekir. Mevcut bir depolama hesabını kullanabilir veya yeni bir tane oluşturun. 

Merhaba VHD toocreate yönetilen bir disk için bir VM kullanacaksa, hello depolama hesap konumu burada hello VM oluşturma aynı hello konumu olmalıdır.

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

    bir kaynak grubu adında toocreate **myResourceGroup** hello içinde **Doğu ABD** bölge, türü:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. Adlı depolama hesabı oluşturma **mystorageaccount** hello kullanarak bu kaynak grubundaki [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    -SkuName için geçerli değerler şunlardır:
   
   * **Standard_LRS** -yerel olarak yedekli depolama. 
   * **Standard_ZRS** -bölge olarak yedekli depolama.
   * **Standard_GRS** -coğrafi olarak yedekli depolama. 
   * **Standard_RAGRS** -coğrafi olarak yedekli depolamaya okuma erişimi. 
   * **Premium_LRS** -Premium yerel olarak yedekli depolama. 

## <a name="upload-hello-vhd-tooyour-storage-account"></a>Merhaba VHD tooyour depolama hesabı karşıya yükle

Kullanım hello [Ekle AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) depolama hesabınızdaki cmdlet tooupload hello VHD tooa kapsayıcı. Karşıya dosya hello Bu örnek *myVHD.vhd* gelen *"C:\Users\Public\Documents\Virtual sabit diskleri\"*  adlı tooa depolama hesabı *mystorageaccount*hello içinde *myResourceGroup* kaynak grubu. Merhaba dosya adlı hello kapsayıcıya yerleştirilecek *mycontainer* ve hello yeni dosya adı olacaktır *myUploadedVHD.vhd*.

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

Bu komut, ağ bağlantısı ve VHD dosyanızı hello boyutuna bağlı olarak biraz zaman alabilir toocomplete

Merhaba Kaydet **hedef URI** yolu toouse toocreate yönetilen bir disk kalacaklarını veya VHD hello kullanarak yeni bir VM karşıya sonraki.

### <a name="other-options-for-uploading-a-vhd"></a>Bir VHD karşıya yükleme için diğer seçenekleri
 
 
Bir VHD tooyour depolama hesabını hello aşağıdakilerden birini kullanarak da yükleyebilirsiniz:

- [AzCopy](http://aka.ms/downloadazcopy)
- [Azure depolama kopyalama Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [Azure Depolama Gezgini karşıya BLOB'ları](https://azurestorageexplorer.codeplex.com/)
- [Depolama içeri/dışarı aktarma hizmeti REST API Başvurusu](https://msdn.microsoft.com/library/dn529096.aspx)
-   İçeri/dışarı aktarma hizmeti 7 günden daha uzun süre karşıya tahmini varsa kullanmanızı öneririz. Kullanabileceğiniz [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) veri boyutu ve aktarım birimi tooestimate başlangıç saati. 
    İçeri/dışarı aktarma olabilir toocopy tooa standart depolama hesabı kullanılır. AzCopy gibi bir araç kullanarak standart depolama toopremium depolama hesabından toocopy gerekir.


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a>Yönetilen oluşturmak hello görüntüden karşıya VHD 

Genelleştirilmiş OS VHD kullanılarak yönetilen bir görüntü oluşturun. Merhaba değerleri kendi bilgileriyle değiştirin.


1.  İlk olarak, hello ortak parametreleri ayarlayın:

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  Genelleştirilmiş OS VHD kullanarak hello görüntüsü oluşturun.

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a>Sanal ağ oluşturma
Merhaba vNet ve alt hello oluşturma [sanal ağ](../../virtual-network/virtual-networks-overview.md).

1. Merhaba alt ağ oluşturun. Bu örnek adlı bir alt ağı oluşturur *mySubnet* hello adres öneki ile *10.0.0.0/24*.  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. Merhaba sanal ağ oluşturun. Bu örnek adlı bir sanal ağ oluşturur *myVnet* hello adres öneki ile *10.0.0.0/16*.  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>Ortak IP adresi ve ağ arabirimi oluşturma

ihtiyacınız tooenable iletişimi hello sanal ağındaki hello sanal makineyle bir [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) ve ağ arabirimi.

1. Bir ortak IP adresi oluşturun. Bu örnek adlı ortak IP adresi oluşturur *myPip*. 
   
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

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>Merhaba ağ güvenlik grubu ve bir RDP kuralı oluşturma

toobe mümkün toolog tooyour içinde RDP kullanarak VM toohave 3389 numaralı bağlantı noktası üzerinde RDP erişimine izin veren bir ağ güvenlik kuralı (NSG) gerekir. 

Bu örnekte adlı bir NSG oluşturulur *myNsg* adlı kuralı içeren *myRdpRule* 3389 numaralı bağlantı noktası RDP trafiğine izin veren. Nsg'ler hakkında daha fazla bilgi için bkz: [bağlantı noktalarını tooa VM PowerShell kullanarak Azure içinde açma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>Merhaba sanal ağ için bir değişken oluşturma

Tamamlanan hello sanal ağ için bir değişken oluşturun. 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>Merhaba VM Hello kimlik bilgilerini alma

Merhaba aşağıdaki cmdlet'i yeni bir kullanıcı adı ve parola toouse hello yerel yönetici hesabı olarak hello VM uzaktan erişmek için gireceğiniz bir pencere açılır. 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a>Merhaba VM adını ve boyutunu toohello VM yapılandırmasına ekleyin.

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>Set hello VM görüntüsü hello için kaynak görüntüsü olarak yeni VM

Yönetilen hello VM görüntüsü Hello Kimliğini kullanarak hello kaynak görüntüsü ayarlayın.

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>Merhaba işletim sistemi yapılandırması ayarlayın ve hello NIC ekleyin

Merhaba depolama türü (PremiumLRS veya StandardLRS) ve hello işletim sistemi diski hello boyutunu girin. Bu örnek hello hesap türü çok ayarlar*PremiumLRS*, disk boyutu çok hello*128 GB* ve disk çok önbelleğe alma*ReadWrite*.

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>Merhaba VM oluşturma

Merhaba Yapılandırması'nı kullanarak yeni VM depolanan hello hello oluşturma **$vm** değişkeni.

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>VM oluşturulduğu bu hello doğrulayın
Tamamlandığında, yeni VM hello oluşturulan hello görmelisiniz [Azure portal](https://portal.azure.com) altında **Gözat** > **sanal makineleri**, veya hello aşağıdakileri kullanarak PowerShell komutları:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Sonraki adımlar

tooyour yeni sanal makine, hello içinde Gözat toohello VM toosign [portal](https://portal.azure.com), tıklatın **Bağlan**ve açık hello Uzak Masaüstü RDP dosyası. Özgün sanal makine toosign Hello hesabı kimlik bilgilerini tooyour yeni sanal makinede kullanın. Daha fazla bilgi için bkz: [nasıl Windows çalıştıran tooconnect ve oturum açma tooan Azure sanal makine](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

