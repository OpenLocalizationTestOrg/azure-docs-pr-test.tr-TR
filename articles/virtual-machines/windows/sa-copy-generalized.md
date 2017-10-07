---
title: "genelleştirilmiş bir Azure VM'de yönetilmeyen görüntüsü aaaCreate | Microsoft Docs"
description: "Genelleştirilmiş bir Windows VM toouse toocreate unmanged görüntüsünü Azure'da VM birden çok kopyasını oluşturun."
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a>Nasıl toocreate yönetilmeyen VM görüntü bir Azure sanal makineden

Bu makalede, depolama hesapları kullanmayı ele alır. Bir depolama hesabı yerine yönetilen diskleri ve yönetilen görüntüleri kullanmanızı öneririz. Daha fazla bilgi için bkz: [genelleştirilmiş VM Azure ile yönetilen bir görüntüsünü yakalama](capture-image-resource.md).

Bu makale size nasıl gösterir toouse Azure PowerShell toocreate bir depolama hesabı kullanılarak genelleştirilmiş bir Azure VM görüntüsü. Daha sonra başka bir VM hello görüntü toocreate kullanabilirsiniz. Merhaba görüntü hello işletim sistemi diski ve ekli toohello sanal makine hello veri disklerinin içerir. Merhaba görüntü hello sanal ağ kaynaklarına içermeyen, yeni VM, oluşturduğunuzda, bu kaynakları tooset gereken şekilde hello. 

## <a name="prerequisites"></a>Ön koşullar
Toohave Azure PowerShell sürüm gereksinim 1.0.x ya da daha yeni yüklü. PowerShell henüz yüklemediyseniz, okuma [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) yükleme adımları için.

## <a name="generalize-hello-vm"></a>Merhaba VM generalize 
Bu bölümde, nasıl gösterilir toogeneralize Windows sanal makinenizi bir resim olarak kullanılacak. Bir VM genelleme tüm kişisel hesap bilgilerinize, başka şeylerin kaldırır ve bir görüntü olarak kullanılan hello makine toobe hazırlar. Sysprep hakkında daha fazla ayrıntı için bkz: [nasıl tooUse Sysprep: Giriş](http://technet.microsoft.com/library/bb457073.aspx).

Merhaba makine üzerinde çalışan hello sunucu rolleri Sysprep tarafından desteklendiğinden emin olun. Daha fazla bilgi için bkz: [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> Merhaba, VHD tooAzure ilk kez yüklüyorsanız olduğundan emin olun [VM'nizi hazırlanmış](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep çalıştırılmadan önce. 
> 
> 

Kullanarak bir Linux VM genelleştirmek `sudo waagent -deprovision+user` ve PowerShell toocapture hello VM kullanın. Merhaba CLI toocapture VM kullanma hakkında daha fazla bilgi için bkz: [nasıl toogeneralize ve kullanarak bir Linux sanal makine yakalama Azure CLI hello ](../linux/capture-image.md).


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

## <a name="log-in-tooazure-powershell"></a>TooAzure PowerShell oturumu
1. Azure PowerShell'i açın ve tooyour Azure hesabı oturum açın.
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    Açılır pencere, tooenter Azure hesabı kimlik bilgilerinizi açar.
2. Merhaba abonelik kimlikleri kullanılabilir aboneliklerinizi alın.
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. Merhaba doğru aboneliğin Hello abonelik kimliğini kullanarak ayarlayın
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a>Merhaba VM serbest bırakma ve hello durumu toogeneralized ayarlayın
1. Merhaba VM kaynakları serbest bırakma.
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    Merhaba *durum* hello Azure VM hello için portal değişiklikleri **durduruldu** çok**durduruldu (serbest bırakıldı)**.
2. Hello sanal makinenin başlangıç durumu çok Ayarla**Genelleştirmiş**. 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. Merhaba VM Hello durumunu denetleyin. Merhaba **OSState ve genelleştirilmiş** hello VM hello olmalıdır için bölüm **DisplayStatus** çok ayarlamak**VM genelleştirilmiş**.  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a>Merhaba görüntü oluşturma

Bir yönetilmeyen sanal makine görüntüsü bu komutu kullanarak hello hedef depolama kapsayıcıda oluşturun. Merhaba görüntüsü hello aynı oluşturulur özgün sanal makine hello gibi depolama hesabı. Merhaba `-Path` parametresi hello kaynak VM tooyour yerel bilgisayar için hello JSON şablonunun bir kopyasını kaydeder. Merhaba `-DestinationContainerName` parametredir görüntülerinizi toohold istediğiniz hello kapsayıcısının hello adı. Merhaba kapsayıcı yoksa, sizin için oluşturulur.
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
Görüntünüzün hello URL hello JSON dosyasını şablondan alabilirsiniz. Toohello Git **kaynakları** > **storageProfile** > **osDisk** > **görüntü**  >  **URI** hello tam yol için bir bölüm görüntünüzün. Merhaba görüntünün Hello URL'si arar gibi: `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`.
   
Merhaba URI hello portalında da doğrulayabilirsiniz. Merhaba görüntüdür adlı kopyalanan tooa kapsayıcı **sistem** depolama hesabınızdaki. 

## <a name="create-a-vm-from-hello-image"></a>Merhaba görüntüsünden bir VM oluşturma

Artık hello yönetilmeyen görüntüsünden bir veya daha fazla sanal makine oluşturabilirsiniz.

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
Merhaba aşağıdaki PowerShell hello sanal makine yapılandırmaları tamamlandıktan ve yönetilmeyen görüntü hello kaynak olarak hello yeni yükleme için kullanır.

</br>

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

### <a name="verify-that-hello-vm-was-created"></a>VM oluşturulduğu bu hello doğrulayın
Tamamlandığında, yeni VM hello oluşturulan hello görmelisiniz [Azure portal](https://portal.azure.com) altında **Gözat** > **sanal makineleri**, veya hello aşağıdakileri kullanarak PowerShell komutları:

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>Sonraki adımlar
Yeni sanal makinenizi Azure PowerShell ile toomanage bkz [Azure Resource Manager ve PowerShell kullanarak sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


