---
title: "Windows Server ve Windows İstemcisi için karma kullanımı avantajı aaaAzure | Microsoft Docs"
description: "Nasıl toomaximize Windows Yazılım Güvencesi avantajları toobring şirket içi öğrenin tooAzure lisansları"
services: virtual-machines-windows
documentationcenter: 
author: kmouss
manager: timlt
editor: 
ms.assetid: 332583b6-15a3-4efb-80c3-9082587828b0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 5/26/2017
ms.author: xujing
ms.openlocfilehash: f24487320a60132aaf766a31f3e6f3726d4a3bd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a>Windows Server ve Windows İstemcisi için Azure karma kullanımı avantajı
Yazılım Güvencesi ile müşteriler için Azure karma kullanımı avantajı toouse sayesinde şirket içi Windows Server ve Windows istemci lisansları ve çalışma Windows azure'da sanal makineler düşük maliyetle. Azure karma kullanımı avantajı Windows Server için Windows Server 2008R2, Windows Server 2012, Windows Server 2012 R2 ve Windows Server 2016 içerir. Azure karma kullanımı avantajı için Windows İstemcisi Windows 10 içerir. Daha fazla bilgi için lütfen hello bkz [Azure karma kullanımı avantajı lisans sayfası](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

>[!IMPORTANT]
>Azure karma kullanım avantajları için Windows şu anda önizlemede hello Azure Marketi hello Windows 10 görüntüsü kullanarak istemcidir. Yalnızca Kurumsal müşteriler Windows 10 Kurumsal E3/E5 ile kullanıcı başına ya da Windows VDA (kullanıcı Abonelik lisansı veya eklenti kullanıcı Abonelik Lisansı) kullanıcı başına uygun ("uygun lisansları").
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a>Yolları toouse Azure karma kullanımı avantajı
Birkaç farklı şekilde toodeploy Windows VM'ler hello Azure karma kullanımı avantajı ile vardır:

1. Vm'lerden dağıtabilirsiniz [belirli Market görüntülerini](#deploy-a-vm-using-the-azure-marketplace) Azure karma kullanımı avantajı ile - Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 ve Windows Server 2008SP1 önceden yapılandırılmış olan.
2. Yapabilecekleriniz [özel bir VM karşıya](#upload-a-windows-vhd) ve [Resource Manager şablonunu kullanarak dağıtın](#deploy-a-vm-via-resource-manager) veya [Azure PowerShell](#detailed-powershell-deployment-walkthrough).

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a>Hello Azure Marketi kullanarak bir VM'i dağıtma
Aşağıdaki görüntüleri hello Marketi Azure karma kullanımı avantajı ile önceden yapılandırılmış kullanılabilir: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 ve Windows Server 2008SP1. Bu görüntüler, doğrudan hello Azure portal, Resource Manager şablonları veya Azure PowerShell dağıtılabilir.

Bu görüntüleri doğrudan hello Azure portal dağıtabilirsiniz. Resource Manager şablonları ve Azure PowerShell ile kullanmak için aşağıdaki gibi görüntüleri hello listesini görüntüleyin:

Windows Server için:
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- 2016 Datacenter sürümü 2016.127.20170406 veya üstü

- 2012 R2 Datacenter sürümü 4.127.20170406 veya üstü

- 2012 Datacenter sürümü 3.127.20170406 veya üstü

- 2008 R2 SP1 sürümü 2.127.20170406 veya üstü

Windows İstemcisi için:
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a>Windows Server VHD karşıya yükle
bir Windows Server VM azure'da toodeploy, ilk toocreate temel Windows yapınızın içeren bir VHD gerekir. TooAzure karşıya yüklemeden önce bu VHD Sysprep uygun şekilde hazırlanması gerekir. Yapabilecekleriniz [hello VHD gereksinimleri ve Sysprep süreci hakkında daha fazla](upload-generalized-managed.md) ve [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles). VM Hello, Sysprep çalıştırılmadan önce yedekleyin. 

Olduğundan emin olun [en son Azure PowerShell yüklenmiş ve yapılandırılmış hello](/powershell/azure/overview). VHD hazır olduktan sonra hello kullanarak hello VHD tooyour Azure depolama hesabı karşıya `Add-AzureRmVhd` şekilde cmdlet:

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> Microsoft SQL Server, SharePoint Server ve Dynamics Yazılım Güvencesi lisans de kullanabilir. Uygulama bileşenlerinizin yükleme ve lisans anahtarları uygun şekilde sağlayarak ardından hello disk görüntü tooAzure karşıya hala tooprepare hello Windows Server görüntüsü gerekir. Sysprep uygulamanızla birlikte gibi çalıştırmak için uygun belgelerine hello gözden [yükleme Sysprep kullanarak SQL Server için ilgili önemli noktalar](https://msdn.microsoft.com/library/ee210754.aspx) veya [SharePoint Server 2016 başvuru yansıması (Sysprep)Oluştur](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).
>
>

Ayrıca daha fazla hakkında bilgiyi [hello VHD tooAzure işlem karşıya yükleme](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)


## <a name="deploy-a-vm-via-resource-manager-template"></a>Resource Manager şablonu aracılığıyla bir VM'yi dağıtmak
Resource Manager şablonlarınızı için ek bir parametre içinde `licenseType` belirtilebilir. Daha fazla bilgi edinebilirsiniz [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md). Karşıya yüklenen VHD tooAzure sahip olduğunda, hello parçası sağlayıcı işlem ve normal olarak şablonunuzu dağıtmak gibi Resource Manager şablonu tooinclude hello lisans türü düzenleyin:

Windows Server için:
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

Windows İstemcisi toouse için Azure Market görüntüsü ile yalnızca:
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a>PowerShell quickstart aracılığıyla bir VM'yi dağıtmak
Windows Server VM'nize PowerShell aracılığıyla dağıtırken için ek bir parametre olan `-LicenseType`. Karşıya yüklenen VHD tooAzure sahip olduğunda, kullanarak bir VM oluşturun `New-AzureRmVM` ve hello lisans türü aşağıdaki gibi belirtin:

Windows Server için:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

Windows İstemcisi toouse için Azure Market görüntüsü ile yalnızca:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

Yapabilecekleriniz [PowerShell aracılığıyla azure'da VM dağıtma konusunda daha ayrıntılı bir kılavuz okuma](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) aşağıdaki ya da okuma daha açıklayıcı Kılavuzu'hello farklı adımlar çok[Resource Manager ve PowerShellkullanarakbirWindowsVMoluşturma](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a>VM hello lisans avantajı kullanılarak doğrulayın
Merhaba PowerShell ya da Resource Manager dağıtım yöntemi aracılığıyla, VM dağıtıldığında hello lisans türü ile doğrulayın `Get-AzureRmVM` gibi:

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

Merhaba, benzer toohello Windows Server için aşağıdaki örneğine çıktı:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

Bu çıktı Azure karma kullanımı avantajı, doğrudan hello Azure Galerisi ' dağıtılan VM gibi lisans olmadan aşağıdaki VM dağıtılan hello ile karşılaştırır:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a>Ayrıntılı PowerShell Dağıtım Kılavuzu
Merhaba aşağıdaki PowerShell adımları Göster VM tam dağıtımını ayrıntılı. Daha fazla bağlam toohello gerçek cmdlet'leri ve oluşturulmakta farklı bileşenler olarak okuyabilirsiniz [Resource Manager ve PowerShell kullanarak bir Windows VM oluşturma](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Kaynak grubu, depolama hesabı ve sanal ağ oluşturmak adım adım sonra VM tanımlanır ve son olarak, VM oluşturun.

İlk olarak, güvenli bir şekilde kimlik bilgilerini elde etmek için bir konum ve kaynak grubu adı ayarlayın:

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

Genel IP oluşturun:

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

Alt ağ, NIC ve sanal ağ tanımlayın:

```powershell
$subnetName = "mySubnet"
$nicName = "myNIC"
$vnetName = "myVnet"
$subnetconfig = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/8
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $resourceGroupName -Location $location `
    -AddressPrefix 10.0.0.0/8 -Subnet $subnetconfig
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $resourceGroupName -Location $location `
    -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $publicIP.Id
```

VM adı ve bir VM yapılandırması oluşturun:

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

İşletim sisteminizde tanımlayın:

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

VM, NIC toohello ekleyin:

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Merhaba depolama hesabı toouse tanımlayın:

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

Uygun hazırlanmış, VHD yüklemek ve kullanmak için tooyour VM ekleyin:

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

Son olarak, VM oluşturma ve türü tooutilize Azure karma kullanımı avantajı lisans hello tanımlayın:

Windows Server için:
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a>Resource Manager şablonu sanal makine ölçek dağıtma
VMSS Resource Manager şablonlarınızı için ek bir parametre içinde `licenseType` belirtilmesi gerekir. Daha fazla bilgi edinebilirsiniz [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md). Merhaba ölçek kümesinin virtualMachineProfile bir parçası olarak, Resource Manager şablonu tooinclude hello LicenseType değeri özelliğini düzenleyin ve normal olarak şablonunuzu dağıtmak - 2016 Windows sunucu görüntüsü kullanarak aşağıdaki örneğe bakın:


```json
"virtualMachineProfile": {
    "storageProfile": {
        "osDisk": {
            "createOption": "FromImage"
        },
        "imageReference": {
            "publisher": "MicrosoftWindowsServer",
            "offer": "WindowsServer",
            "sku": "2016-Datacenter",
            "version": "latest"
        }
    },
    "licenseType": "Windows_Server",
    "osProfile": {
            "computerNamePrefix": "[parameters('vmssName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
    }
```

> [!NOTE]
> PowerShell ve diğer SDK Araçları aracılığıyla AHUB avantajları kümesi bir sanal makine ölçek dağıtılması desteği yakında geliyor.
>

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinin [Azure karma kullanımı avantajı lisans](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

Daha fazla bilgi edinmek [Resource Manager şablonları kullanarak](../../azure-resource-manager/resource-group-overview.md).

Daha fazla bilgi edinmek [Azure karma kullanımı avantajı Azure Site Recovery yapıp geçirme uygulamaları tooAzure daha düşük maliyetli](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).
