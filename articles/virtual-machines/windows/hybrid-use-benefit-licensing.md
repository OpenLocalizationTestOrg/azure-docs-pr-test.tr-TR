---
title: "Windows Server ve Windows İstemcisi için Azure karma kullanımı avantajı | Microsoft Docs"
description: "Azure için şirket içi lisansları getirmek için Windows Yazılım Güvencesi Avantajlarınızı en üst düzeye öğrenin"
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
ms.openlocfilehash: 210635624946ddb293427167e9d476c377bcc9b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a>Windows Server ve Windows İstemcisi için Azure karma kullanımı avantajı
Yazılım Güvencesi ile müşteriler için Azure karma kullanma avantajı, şirket içi Windows Server ve Windows istemci lisanslarınızı kullanın ve sınırlı bir ücret Azure'da Windows sanal makineleri çalıştırma olanak sağlar. Azure karma kullanımı avantajı Windows Server için Windows Server 2008R2, Windows Server 2012, Windows Server 2012 R2 ve Windows Server 2016 içerir. Azure karma kullanımı avantajı için Windows İstemcisi Windows 10 içerir. Daha fazla bilgi için lütfen bkz [Azure karma kullanımı avantajı lisans sayfası](https://azure.microsoft.com/pricing/hybrid-use-benefit/).

>[!IMPORTANT]
>Azure karma kullanımı avantajları için Windows şu anda Azure Marketi'nde Windows 10 görüntüsü kullanarak önizlemede istemcidir. Yalnızca Kurumsal müşteriler Windows 10 Kurumsal E3/E5 ile kullanıcı başına ya da Windows VDA (kullanıcı Abonelik lisansı veya eklenti kullanıcı Abonelik Lisansı) kullanıcı başına uygun ("uygun lisansları").
>
>

## <a name="ways-to-use-azure-hybrid-use-benefit"></a>Azure karma kullanma avantajını kullanmak için yollar
Çeşitli Azure karma kullanımı avantajı ile Windows sanal makineleri dağıtmak için farklı şekillerde vardır:

1. Vm'lerden dağıtabilirsiniz [belirli Market görüntülerini](#deploy-a-vm-using-the-azure-marketplace) Azure karma kullanımı avantajı ile - Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 ve Windows Server 2008SP1 önceden yapılandırılmış olan.
2. Yapabilecekleriniz [özel bir VM karşıya](#upload-a-windows-vhd) ve [Resource Manager şablonunu kullanarak dağıtın](#deploy-a-vm-via-resource-manager) veya [Azure PowerShell](#detailed-powershell-deployment-walkthrough).

## <a name="deploy-a-vm-using-the-azure-marketplace"></a>Azure Market kullanarak bir VM'i dağıtma
Aşağıdaki görüntüleri kullanılabilir Azure karma kullanımı avantajı ile önceden yapılandırılmış Market'te: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 ve Windows Server 2008SP1. Bu görüntüler doğrudan Azure portalından, Resource Manager şablonlarından veya Azure PowerShell’den dağıtılabilir.

Bu görüntüleri doğrudan Azure portalından dağıtabilirsiniz. Resource Manager şablonları ve Azure PowerShell ile kullanmak için aşağıdaki gibi görüntüleri listesini görüntüleyin:

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
Windows Server VM azure'da dağıtmak için önce temel Windows yapınızın içeren bir VHD oluşturmanız gerekir. Azure için karşıya yüklemeden önce bu VHD Sysprep uygun şekilde hazırlanması gerekir. Yapabilecekleriniz [Sysprep işlemi ve VHD gereksinimleri hakkında daha fazla](upload-generalized-managed.md) ve [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles). VM yedeklemesi, Sysprep çalıştırılmadan önce yedekleyin. 

Olduğundan emin olun [yüklenmiş ve yapılandırılmış en son Azure PowerShell](/powershell/azure/overview). VHD hazır olduktan sonra Azure depolama hesabı kullanmaya VHD'nin yüklenmesi `Add-AzureRmVhd` şekilde cmdlet:

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> Microsoft SQL Server, SharePoint Server ve Dynamics Yazılım Güvencesi lisans de kullanabilir. Hala uygulama bileşenlerinizin yükleme ve lisans anahtarları uygun şekilde sağlayarak, sonra disk görüntüsü Azure'a yüklenmesini tarafından Windows Server görüntüyü hazırlamanız gerekir. Sysprep uygulamanızla birlikte gibi çalıştırmak için uygun belgelerini gözden geçirin [yükleme Sysprep kullanarak SQL Server için ilgili önemli noktalar](https://msdn.microsoft.com/library/ee210754.aspx) veya [SharePoint Server 2016 başvuru yansıması (Sysprep)Oluştur](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).
>
>

Ayrıca daha fazla hakkında bilgiyi [VHD için Azure işlem karşıya yükleme](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)


## <a name="deploy-a-vm-via-resource-manager-template"></a>Resource Manager şablonu aracılığıyla bir VM'yi dağıtmak
Resource Manager şablonlarınızı için ek bir parametre içinde `licenseType` belirtilebilir. Daha fazla bilgi edinebilirsiniz [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md). Azure'a karşıya, VHD olduktan sonra lisans türü işlem sağlayıcısı bir parçası olarak dahil edin ve normal olarak, şablonunuzu dağıtmak için Resource Manager şablonunu düzenleyin:

Windows Server için:
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

Windows Azure Market görüntüsü ile yalnızca kullanmak istemci için:
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a>PowerShell quickstart aracılığıyla bir VM'yi dağıtmak
Windows Server VM'nize PowerShell aracılığıyla dağıtırken için ek bir parametre olan `-LicenseType`. Azure için karşıya, VHD'yi oluşturduktan sonra kullanarak bir VM oluşturun `New-AzureRmVM` ve lisans türü aşağıdaki gibi belirtin:

Windows Server için:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

Windows Azure Market görüntüsü ile yalnızca kullanmak istemci için:
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

Yapabilecekleriniz [PowerShell aracılığıyla azure'da VM dağıtma konusunda daha ayrıntılı bir kılavuz okuma](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) aşağıdaki ya da daha açıklayıcı bir kılavuzu için farklı adımlar üzerinde okuma [Resource Manager ve PowerShellkullanarakbirWindowsVMoluşturma](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="verify-your-vm-is-utilizing-the-licensing-benefit"></a>VM lisans avantajı kullanılarak doğrulayın
Her iki PowerShell veya Resource Manager dağıtım yöntemi, VM dağıttıktan sonra lisans türü ile doğrulayın `Get-AzureRmVM` gibi:

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

Windows Server için aşağıdaki örneğe benzer bir çıkış:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

Bu çelişir çıktı Azure karma kullanımı avantajı, doğrudan Azure galerisinden dağıtılan VM gibi lisans olmadan dağıtılan aşağıdaki VM ile:

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a>Ayrıntılı PowerShell Dağıtım Kılavuzu
VM tam dağıtımını aşağıdaki ayrıntılı PowerShell adımları gösterir. Oluşturulmakta farklı bileşenleri ve gerçek cmdlet'ler konusunda daha fazla bağlam okuyabilirsiniz [Resource Manager ve PowerShell kullanarak bir Windows VM oluşturma](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Kaynak grubu, depolama hesabı ve sanal ağ oluşturmak adım adım sonra VM tanımlanır ve son olarak, VM oluşturun.

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

VM, NIC ekleyin:

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

Depolama hesabı tanımlayın:

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

Uygun hazırlanmış, VHD yüklemek ve kullanmak için VM ekleyin:

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

Son olarak, VM oluşturun ve Azure karma kullanma avantajını kullanmak üzere lisans türünü tanımlayın:

Windows Server için:
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a>Resource Manager şablonu sanal makine ölçek dağıtma
VMSS Resource Manager şablonlarınızı için ek bir parametre içinde `licenseType` belirtilmesi gerekir. Daha fazla bilgi edinebilirsiniz [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md). Ölçek kümesinin virtualMachineProfile bir parçası olarak LicenseType değeri özellik içerir ve normal olarak şablonunuzu dağıtmak-2016 Windows sunucu görüntüsü kullanarak aşağıdaki örneğe bakın Kaynak Yöneticisi şablonunuzu düzenleyin:


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

Daha fazla bilgi edinmek [Azure karma kullanımı avantajı Azure Site Recovery yapıp Azure uygulamaları geçirme daha düşük maliyetli](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).
