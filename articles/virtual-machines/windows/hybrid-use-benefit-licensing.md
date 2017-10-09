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
# <a name="azure-hybrid-use-benefit-for-windows-server-and-windows-client"></a><span data-ttu-id="421dd-103">Windows Server ve Windows İstemcisi için Azure karma kullanımı avantajı</span><span class="sxs-lookup"><span data-stu-id="421dd-103">Azure Hybrid Use Benefit for Windows Server and Windows Client</span></span>
<span data-ttu-id="421dd-104">Yazılım Güvencesi ile müşteriler için Azure karma kullanımı avantajı toouse sayesinde şirket içi Windows Server ve Windows istemci lisansları ve çalışma Windows azure'da sanal makineler düşük maliyetle.</span><span class="sxs-lookup"><span data-stu-id="421dd-104">For customers with Software Assurance, Azure Hybrid Use Benefit allows you toouse your on-premises Windows Server and Windows Client licenses and run Windows virtual machines in Azure at a reduced cost.</span></span> <span data-ttu-id="421dd-105">Azure karma kullanımı avantajı Windows Server için Windows Server 2008R2, Windows Server 2012, Windows Server 2012 R2 ve Windows Server 2016 içerir.</span><span class="sxs-lookup"><span data-stu-id="421dd-105">Azure Hybrid Use Benefit for Windows Server includes Windows Server 2008R2, Windows Server 2012, Windows Server 2012R2, and Windows Server 2016.</span></span> <span data-ttu-id="421dd-106">Azure karma kullanımı avantajı için Windows İstemcisi Windows 10 içerir.</span><span class="sxs-lookup"><span data-stu-id="421dd-106">Azure Hybrid Use Benefit for Windows Client includes Windows 10.</span></span> <span data-ttu-id="421dd-107">Daha fazla bilgi için lütfen hello bkz [Azure karma kullanımı avantajı lisans sayfası](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="421dd-107">For more information, please see hello [Azure Hybrid Use Benefit licensing page](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

>[!IMPORTANT]
><span data-ttu-id="421dd-108">Azure karma kullanım avantajları için Windows şu anda önizlemede hello Azure Marketi hello Windows 10 görüntüsü kullanarak istemcidir.</span><span class="sxs-lookup"><span data-stu-id="421dd-108">Azure Hybrid Use Benefits for Windows Client is currently in Preview using hello Windows 10 image in hello Azure Marketplace.</span></span> <span data-ttu-id="421dd-109">Yalnızca Kurumsal müşteriler Windows 10 Kurumsal E3/E5 ile kullanıcı başına ya da Windows VDA (kullanıcı Abonelik lisansı veya eklenti kullanıcı Abonelik Lisansı) kullanıcı başına uygun ("uygun lisansları").</span><span class="sxs-lookup"><span data-stu-id="421dd-109">Only Enterprise customers with Windows 10 Enterprise E3/E5 per user or Windows VDA per user (User Subscription Licenses or Add-on User Subscription Licenses) (“Qualifying Licenses”) are eligible.</span></span>
>
>

## <a name="ways-toouse-azure-hybrid-use-benefit"></a><span data-ttu-id="421dd-110">Yolları toouse Azure karma kullanımı avantajı</span><span class="sxs-lookup"><span data-stu-id="421dd-110">Ways toouse Azure Hybrid Use Benefit</span></span>
<span data-ttu-id="421dd-111">Birkaç farklı şekilde toodeploy Windows VM'ler hello Azure karma kullanımı avantajı ile vardır:</span><span class="sxs-lookup"><span data-stu-id="421dd-111">There are a couple of different ways toodeploy Windows VMs with hello Azure Hybrid Use Benefit:</span></span>

1. <span data-ttu-id="421dd-112">Vm'lerden dağıtabilirsiniz [belirli Market görüntülerini](#deploy-a-vm-using-the-azure-marketplace) Azure karma kullanımı avantajı ile - Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 ve Windows Server 2008SP1 önceden yapılandırılmış olan.</span><span class="sxs-lookup"><span data-stu-id="421dd-112">You can deploy VMs from [specific Marketplace images](#deploy-a-vm-using-the-azure-marketplace) that are pre-configured with Azure Hybrid Use Benefit - Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span>
2. <span data-ttu-id="421dd-113">Yapabilecekleriniz [özel bir VM karşıya](#upload-a-windows-vhd) ve [Resource Manager şablonunu kullanarak dağıtın](#deploy-a-vm-via-resource-manager) veya [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="421dd-113">You can [upload a custom VM](#upload-a-windows-vhd) and [deploy using a Resource Manager template](#deploy-a-vm-via-resource-manager) or [Azure PowerShell](#detailed-powershell-deployment-walkthrough).</span></span>

## <a name="deploy-a-vm-using-hello-azure-marketplace"></a><span data-ttu-id="421dd-114">Hello Azure Marketi kullanarak bir VM'i dağıtma</span><span class="sxs-lookup"><span data-stu-id="421dd-114">Deploy a VM using hello Azure Marketplace</span></span>
<span data-ttu-id="421dd-115">Aşağıdaki görüntüleri hello Marketi Azure karma kullanımı avantajı ile önceden yapılandırılmış kullanılabilir: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012 ve Windows Server 2008SP1.</span><span class="sxs-lookup"><span data-stu-id="421dd-115">Following images are available in hello Marketplace pre-configured with Azure Hybrid Use Benefit: Windows Server 2016, Windows Server 2012R2, Windows Server 2012 and Windows Server 2008SP1.</span></span> <span data-ttu-id="421dd-116">Bu görüntüler, doğrudan hello Azure portal, Resource Manager şablonları veya Azure PowerShell dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="421dd-116">These images can be deployed directly from hello Azure portal, Resource Manager templates, or Azure PowerShell.</span></span>

<span data-ttu-id="421dd-117">Bu görüntüleri doğrudan hello Azure portal dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="421dd-117">You can deploy these images directly from hello Azure portal.</span></span> <span data-ttu-id="421dd-118">Resource Manager şablonları ve Azure PowerShell ile kullanmak için aşağıdaki gibi görüntüleri hello listesini görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="421dd-118">For use in Resource Manager templates and with Azure PowerShell, view hello list of images as follows:</span></span>

<span data-ttu-id="421dd-119">Windows Server için:</span><span class="sxs-lookup"><span data-stu-id="421dd-119">For Windows Server:</span></span>
```powershell
Get-AzureRmVMImagesku -Location westus -PublisherName MicrosoftWindowsServer -Offer WindowsServer
```
- <span data-ttu-id="421dd-120">2016 Datacenter sürümü 2016.127.20170406 veya üstü</span><span class="sxs-lookup"><span data-stu-id="421dd-120">2016-Datacenter version 2016.127.20170406 or above</span></span>

- <span data-ttu-id="421dd-121">2012 R2 Datacenter sürümü 4.127.20170406 veya üstü</span><span class="sxs-lookup"><span data-stu-id="421dd-121">2012-R2-Datacenter version 4.127.20170406 or above</span></span>

- <span data-ttu-id="421dd-122">2012 Datacenter sürümü 3.127.20170406 veya üstü</span><span class="sxs-lookup"><span data-stu-id="421dd-122">2012-Datacenter version 3.127.20170406 or above</span></span>

- <span data-ttu-id="421dd-123">2008 R2 SP1 sürümü 2.127.20170406 veya üstü</span><span class="sxs-lookup"><span data-stu-id="421dd-123">2008-R2-SP1 version 2.127.20170406 or above</span></span>

<span data-ttu-id="421dd-124">Windows İstemcisi için:</span><span class="sxs-lookup"><span data-stu-id="421dd-124">For Windows Client:</span></span>
```powershell
Get-AzureRMVMImageSku -Location "West US" -Publisher "MicrosoftWindowsServer" `
    -Offer "Windows-HUB"
```

## <a name="upload-a-windows-server-vhd"></a><span data-ttu-id="421dd-125">Windows Server VHD karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="421dd-125">Upload a Windows Server VHD</span></span>
<span data-ttu-id="421dd-126">bir Windows Server VM azure'da toodeploy, ilk toocreate temel Windows yapınızın içeren bir VHD gerekir.</span><span class="sxs-lookup"><span data-stu-id="421dd-126">toodeploy a Windows Server VM in Azure, you first need toocreate a VHD that contains your base Windows build.</span></span> <span data-ttu-id="421dd-127">TooAzure karşıya yüklemeden önce bu VHD Sysprep uygun şekilde hazırlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="421dd-127">This VHD must be appropriately prepared via Sysprep before you upload it tooAzure.</span></span> <span data-ttu-id="421dd-128">Yapabilecekleriniz [hello VHD gereksinimleri ve Sysprep süreci hakkında daha fazla](upload-generalized-managed.md) ve [sunucu rolleri için Sysprep desteği](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="421dd-128">You can [read more about hello VHD requirements and Sysprep process](upload-generalized-managed.md) and [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span> <span data-ttu-id="421dd-129">VM Hello, Sysprep çalıştırılmadan önce yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="421dd-129">Back up hello VM before running Sysprep.</span></span> 

<span data-ttu-id="421dd-130">Olduğundan emin olun [en son Azure PowerShell yüklenmiş ve yapılandırılmış hello](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="421dd-130">Make sure you have [installed and configured hello latest Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="421dd-131">VHD hazır olduktan sonra hello kullanarak hello VHD tooyour Azure depolama hesabı karşıya `Add-AzureRmVhd` şekilde cmdlet:</span><span class="sxs-lookup"><span data-stu-id="421dd-131">Once you have prepared your VHD, upload hello VHD tooyour Azure Storage account using hello `Add-AzureRmVhd` cmdlet as follows:</span></span>

```powershell
Add-AzureRmVhd -ResourceGroupName "myResourceGroup" -LocalFilePath "C:\Path\To\myvhd.vhd" `
    -Destination "https://mystorageaccount.blob.core.windows.net/vhds/myvhd.vhd"
```

> [!NOTE]
> <span data-ttu-id="421dd-132">Microsoft SQL Server, SharePoint Server ve Dynamics Yazılım Güvencesi lisans de kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="421dd-132">Microsoft SQL Server, SharePoint Server, and Dynamics can also utilize your Software Assurance licensing.</span></span> <span data-ttu-id="421dd-133">Uygulama bileşenlerinizin yükleme ve lisans anahtarları uygun şekilde sağlayarak ardından hello disk görüntü tooAzure karşıya hala tooprepare hello Windows Server görüntüsü gerekir.</span><span class="sxs-lookup"><span data-stu-id="421dd-133">You still need tooprepare hello Windows Server image by installing your application components and providing license keys accordingly, then uploading hello disk image tooAzure.</span></span> <span data-ttu-id="421dd-134">Sysprep uygulamanızla birlikte gibi çalıştırmak için uygun belgelerine hello gözden [yükleme Sysprep kullanarak SQL Server için ilgili önemli noktalar](https://msdn.microsoft.com/library/ee210754.aspx) veya [SharePoint Server 2016 başvuru yansıması (Sysprep)Oluştur](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span><span class="sxs-lookup"><span data-stu-id="421dd-134">Review hello appropriate documentation for running Sysprep with your application, such as [Considerations for Installing SQL Server using Sysprep](https://msdn.microsoft.com/library/ee210754.aspx) or [Build a SharePoint Server 2016 Reference Image (Sysprep)](http://social.technet.microsoft.com/wiki/contents/articles/33789.build-a-sharepoint-server-2016-reference-image-sysprep.aspx).</span></span>
>
>

<span data-ttu-id="421dd-135">Ayrıca daha fazla hakkında bilgiyi [hello VHD tooAzure işlem karşıya yükleme](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span><span class="sxs-lookup"><span data-stu-id="421dd-135">You can also read more about [uploading hello VHD tooAzure process](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account)</span></span>


## <a name="deploy-a-vm-via-resource-manager-template"></a><span data-ttu-id="421dd-136">Resource Manager şablonu aracılığıyla bir VM'yi dağıtmak</span><span class="sxs-lookup"><span data-stu-id="421dd-136">Deploy a VM via Resource Manager Template</span></span>
<span data-ttu-id="421dd-137">Resource Manager şablonlarınızı için ek bir parametre içinde `licenseType` belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="421dd-137">Within your Resource Manager templates, an additional parameter for `licenseType` can be specified.</span></span> <span data-ttu-id="421dd-138">Daha fazla bilgi edinebilirsiniz [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="421dd-138">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="421dd-139">Karşıya yüklenen VHD tooAzure sahip olduğunda, hello parçası sağlayıcı işlem ve normal olarak şablonunuzu dağıtmak gibi Resource Manager şablonu tooinclude hello lisans türü düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="421dd-139">Once you have your VHD uploaded tooAzure, edit you Resource Manager template tooinclude hello license type as part of hello compute provider and deploy your template as normal:</span></span>

<span data-ttu-id="421dd-140">Windows Server için:</span><span class="sxs-lookup"><span data-stu-id="421dd-140">For Windows Server:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Server",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

<span data-ttu-id="421dd-141">Windows İstemcisi toouse için Azure Market görüntüsü ile yalnızca:</span><span class="sxs-lookup"><span data-stu-id="421dd-141">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```json
"properties": {  
   "licenseType": "Windows_Client",
   "hardwareProfile": {
        "vmSize": "[variables('vmSize')]"
   }
```

## <a name="deploy-a-vm-via-powershell-quickstart"></a><span data-ttu-id="421dd-142">PowerShell quickstart aracılığıyla bir VM'yi dağıtmak</span><span class="sxs-lookup"><span data-stu-id="421dd-142">Deploy a VM via PowerShell quickstart</span></span>
<span data-ttu-id="421dd-143">Windows Server VM'nize PowerShell aracılığıyla dağıtırken için ek bir parametre olan `-LicenseType`.</span><span class="sxs-lookup"><span data-stu-id="421dd-143">When deploying your Windows Server VM via PowerShell, you have an additional parameter for `-LicenseType`.</span></span> <span data-ttu-id="421dd-144">Karşıya yüklenen VHD tooAzure sahip olduğunda, kullanarak bir VM oluşturun `New-AzureRmVM` ve hello lisans türü aşağıdaki gibi belirtin:</span><span class="sxs-lookup"><span data-stu-id="421dd-144">Once you have your VHD uploaded tooAzure, you create a VM using `New-AzureRmVM` and specify hello licensing type as follows:</span></span>

<span data-ttu-id="421dd-145">Windows Server için:</span><span class="sxs-lookup"><span data-stu-id="421dd-145">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Server"
```

<span data-ttu-id="421dd-146">Windows İstemcisi toouse için Azure Market görüntüsü ile yalnızca:</span><span class="sxs-lookup"><span data-stu-id="421dd-146">For Windows Client toouse with Azure Marketplace Image only:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location "West US" -VM $vm -LicenseType "Windows_Client"
```

<span data-ttu-id="421dd-147">Yapabilecekleriniz [PowerShell aracılığıyla azure'da VM dağıtma konusunda daha ayrıntılı bir kılavuz okuma](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) aşağıdaki ya da okuma daha açıklayıcı Kılavuzu'hello farklı adımlar çok[Resource Manager ve PowerShellkullanarakbirWindowsVMoluşturma](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="421dd-147">You can [read a more detailed walkthrough on deploying a VM in Azure via PowerShell](hybrid-use-benefit-licensing.md#detailed-powershell-deployment-walkthrough) below, or read a more descriptive guide on hello different steps too[create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="verify-your-vm-is-utilizing-hello-licensing-benefit"></a><span data-ttu-id="421dd-148">VM hello lisans avantajı kullanılarak doğrulayın</span><span class="sxs-lookup"><span data-stu-id="421dd-148">Verify your VM is utilizing hello licensing benefit</span></span>
<span data-ttu-id="421dd-149">Merhaba PowerShell ya da Resource Manager dağıtım yöntemi aracılığıyla, VM dağıtıldığında hello lisans türü ile doğrulayın `Get-AzureRmVM` gibi:</span><span class="sxs-lookup"><span data-stu-id="421dd-149">Once you have deployed your VM through either hello PowerShell or Resource Manager deployment method, verify hello license type with `Get-AzureRmVM` as follows:</span></span>

```powershell
Get-AzureRmVM -ResourceGroup "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="421dd-150">Merhaba, benzer toohello Windows Server için aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="421dd-150">hello output is similar toohello following example for Windows Server:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              : Windows_Server
```

<span data-ttu-id="421dd-151">Bu çıktı Azure karma kullanımı avantajı, doğrudan hello Azure Galerisi ' dağıtılan VM gibi lisans olmadan aşağıdaki VM dağıtılan hello ile karşılaştırır:</span><span class="sxs-lookup"><span data-stu-id="421dd-151">This output contrasts with hello following VM deployed without Azure Hybrid Use Benefit licensing, such as a VM deployed straight from hello Azure Gallery:</span></span>

```powershell
Type                     : Microsoft.Compute/virtualMachines
Location                 : westus
LicenseType              :
```

## <a name="detailed-powershell-deployment-walkthrough"></a><span data-ttu-id="421dd-152">Ayrıntılı PowerShell Dağıtım Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="421dd-152">Detailed PowerShell deployment walkthrough</span></span>
<span data-ttu-id="421dd-153">Merhaba aşağıdaki PowerShell adımları Göster VM tam dağıtımını ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="421dd-153">hello following detailed PowerShell steps show a full deployment of a VM.</span></span> <span data-ttu-id="421dd-154">Daha fazla bağlam toohello gerçek cmdlet'leri ve oluşturulmakta farklı bileşenler olarak okuyabilirsiniz [Resource Manager ve PowerShell kullanarak bir Windows VM oluşturma](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="421dd-154">You can read more context as toohello actual cmdlets and different components being created in [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="421dd-155">Kaynak grubu, depolama hesabı ve sanal ağ oluşturmak adım adım sonra VM tanımlanır ve son olarak, VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="421dd-155">You step through creating your resource group, storage account, and virtual networking, then define your VM and finally create your VM.</span></span>

<span data-ttu-id="421dd-156">İlk olarak, güvenli bir şekilde kimlik bilgilerini elde etmek için bir konum ve kaynak grubu adı ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="421dd-156">First, securely obtain credentials, set a location, and resource group name:</span></span>

```powershell
$cred = Get-Credential
$location = "West US"
$resourceGroupName = "myResourceGroup"
```

<span data-ttu-id="421dd-157">Genel IP oluşturun:</span><span class="sxs-lookup"><span data-stu-id="421dd-157">Create a public IP:</span></span>

```powershell
$publicIPName = "myPublicIP"
$publicIP = New-AzureRmPublicIpAddress -Name $publicIPName -ResourceGroupName $resourceGroupName `
    -Location $location -AllocationMethod "Dynamic"
```

<span data-ttu-id="421dd-158">Alt ağ, NIC ve sanal ağ tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="421dd-158">Define your subnet, NIC, and VNET:</span></span>

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

<span data-ttu-id="421dd-159">VM adı ve bir VM yapılandırması oluşturun:</span><span class="sxs-lookup"><span data-stu-id="421dd-159">Name your VM and create a VM config:</span></span>

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A1"
```

<span data-ttu-id="421dd-160">İşletim sisteminizde tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="421dd-160">Define your OS:</span></span>

```powershell
$computerName = "myVM"
$vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName -Credential $cred `
    -ProvisionVMAgent -EnableAutoUpdate
```

<span data-ttu-id="421dd-161">VM, NIC toohello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="421dd-161">Add your NIC toohello VM:</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="421dd-162">Merhaba depolama hesabı toouse tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="421dd-162">Define hello storage account toouse:</span></span>

```powershell
$storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -AccountName mystorageaccount
```

<span data-ttu-id="421dd-163">Uygun hazırlanmış, VHD yüklemek ve kullanmak için tooyour VM ekleyin:</span><span class="sxs-lookup"><span data-stu-id="421dd-163">Upload your VHD, suitably prepared, and attach tooyour VM for use:</span></span>

```powershell
$osDiskName = "licensing.vhd"
$osDiskUri = '{0}vhds/{1}{2}.vhd' -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/vhd/myvhd.vhd"
$vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption FromImage `
    -SourceImageUri $urlOfUploadedImageVhd -Windows
```

<span data-ttu-id="421dd-164">Son olarak, VM oluşturma ve türü tooutilize Azure karma kullanımı avantajı lisans hello tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="421dd-164">Finally, create your VM and define hello licensing type tooutilize Azure Hybrid Use Benefit:</span></span>

<span data-ttu-id="421dd-165">Windows Server için:</span><span class="sxs-lookup"><span data-stu-id="421dd-165">For Windows Server:</span></span>
```powershell
New-AzureRmVM -ResourceGroupName $resourceGroupName -Location $location -VM $vm -LicenseType "Windows_Server"
```

## <a name="deploy-a-virtual-machine-scale-set-via-resource-manager-template"></a><span data-ttu-id="421dd-166">Resource Manager şablonu sanal makine ölçek dağıtma</span><span class="sxs-lookup"><span data-stu-id="421dd-166">Deploy a virtual machine scale set via Resource Manager template</span></span>
<span data-ttu-id="421dd-167">VMSS Resource Manager şablonlarınızı için ek bir parametre içinde `licenseType` belirtilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="421dd-167">Within your VMSS Resource Manager templates, an additional parameter for `licenseType` must be specified.</span></span> <span data-ttu-id="421dd-168">Daha fazla bilgi edinebilirsiniz [Azure Resource Manager şablonları yazma](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="421dd-168">You can read more about [authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span> <span data-ttu-id="421dd-169">Merhaba ölçek kümesinin virtualMachineProfile bir parçası olarak, Resource Manager şablonu tooinclude hello LicenseType değeri özelliğini düzenleyin ve normal olarak şablonunuzu dağıtmak - 2016 Windows sunucu görüntüsü kullanarak aşağıdaki örneğe bakın:</span><span class="sxs-lookup"><span data-stu-id="421dd-169">Edit your Resource Manager template tooinclude hello licenseType property as part of hello scale set’s virtualMachineProfile and deploy your template as normal - see example below using 2016 Windows Server image:</span></span>


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
> <span data-ttu-id="421dd-170">PowerShell ve diğer SDK Araçları aracılığıyla AHUB avantajları kümesi bir sanal makine ölçek dağıtılması desteği yakında geliyor.</span><span class="sxs-lookup"><span data-stu-id="421dd-170">Support for deploying a virtual machine scale set with AHUB benefits through PowerShell and other SDK tools is coming soon.</span></span>
>

## <a name="next-steps"></a><span data-ttu-id="421dd-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="421dd-171">Next steps</span></span>
<span data-ttu-id="421dd-172">Daha fazla bilgi edinin [Azure karma kullanımı avantajı lisans](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span><span class="sxs-lookup"><span data-stu-id="421dd-172">Read more about [Azure Hybrid Use Benefit licensing](https://azure.microsoft.com/pricing/hybrid-use-benefit/).</span></span>

<span data-ttu-id="421dd-173">Daha fazla bilgi edinmek [Resource Manager şablonları kullanarak](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="421dd-173">Learn more about [using Resource Manager templates](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="421dd-174">Daha fazla bilgi edinmek [Azure karma kullanımı avantajı Azure Site Recovery yapıp geçirme uygulamaları tooAzure daha düşük maliyetli](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span><span class="sxs-lookup"><span data-stu-id="421dd-174">Learn more about [Azure Hybrid Use Benefit and Azure Site Recovery make migrating applications tooAzure even more cost-effective](https://azure.microsoft.com/blog/hybrid-use-benefit-migration-with-asr/).</span></span>
