---
title: "sanal makine ölçek üzerinde bir uygulama aaaDeploy ayarlar"
description: "Azure sanal makine ölçek kümeleri üzerinde uzantıları toodepoy bir uygulama kullanın."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="78c25-103">Sanal makine ölçek kümeleri, uygulamanızda dağıtma</span><span class="sxs-lookup"><span data-stu-id="78c25-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="78c25-104">Bu makalede tooinstall yazılım hello zaman hello ölçekte nasıl kümesinin farklı şekilde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="78c25-104">This article describes different ways of how tooinstall software at hello time hello scale set is provisioned.</span></span>

<span data-ttu-id="78c25-105">Tooreview hello isteyebilirsiniz [ölçek kümesi tasarım genel bakış](virtual-machine-scale-sets-design-overview.md) makalenin hello sınır sanal makine ölçek kümeleri tarafından uygulanmaz bazıları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="78c25-105">You may want tooreview hello [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of hello limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="78c25-106">Yakalama ve görüntüyü yeniden</span><span class="sxs-lookup"><span data-stu-id="78c25-106">Capture and reuse an image</span></span>

<span data-ttu-id="78c25-107">Azure tooprepare temel görüntü, Ölçek kümesindeki bir sanal makine kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78c25-107">You can use a virtual machine you have in Azure tooprepare a base-image for your scale set.</span></span> <span data-ttu-id="78c25-108">Bu işlem, hello temel görüntü ölçek kümesi için başvuru depolama hesabınızda yönetilen bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="78c25-108">This process creates a managed disk in your storage account, which you can reference as hello base image for your scale set.</span></span> 

<span data-ttu-id="78c25-109">Adımları hello:</span><span class="sxs-lookup"><span data-stu-id="78c25-109">Do hello following steps:</span></span>

1. <span data-ttu-id="78c25-110">Bir Azure sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="78c25-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="78c25-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="78c25-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="78c25-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="78c25-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="78c25-113">Uzak içine hello sanal makine ve hello sistem tooyour istediğiniz özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78c25-113">Remote into hello virtual machine and customize hello system tooyour liking.</span></span>

   <span data-ttu-id="78c25-114">İsterseniz, uygulamanız şimdi yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78c25-114">If you want, you can install your application now.</span></span> <span data-ttu-id="78c25-115">Uygulamanızı şimdi yükleyerek uygulamanızı daha karmaşık tooremove gerekebileceğinden yükseltme yaptığınız ancak, bilinmesi, ilk.</span><span class="sxs-lookup"><span data-stu-id="78c25-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need tooremove it first.</span></span> <span data-ttu-id="78c25-116">Bunun yerine, bu adım tooinstall uygulamanız gerekebilir, gibi belirli bir çalışma zamanı veya işletim sistemi özelliği tüm Önkoşullar kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78c25-116">Instead, you can use this step tooinstall any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="78c25-117">Merhaba öğretici "bir makine yakalama" ya da izleyin [Linux] [ linux-vm-capture] veya [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="78c25-117">Follow hello "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="78c25-118">Oluşturma bir [sanal makine ölçek kümesi] [ vmss-create] ile Merhaba URI hello önceki adımda yakalanan görüntü.</span><span class="sxs-lookup"><span data-stu-id="78c25-118">Create a [Virtual Machine Scale Set][vmss-create] with hello image URI you captured in hello previous step.</span></span>

<span data-ttu-id="78c25-119">Diskler hakkında daha fazla bilgi için bkz: [yönetilen diskleri genel bakış](../virtual-machines/windows/managed-disks-overview.md) ve [eklenen veri disklerini kullanmak](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="78c25-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-hello-scale-set-is-provisioned"></a><span data-ttu-id="78c25-120">Merhaba ölçek kümesini sağlandığında yükleme</span><span class="sxs-lookup"><span data-stu-id="78c25-120">Install when hello scale set is provisioned</span></span>

<span data-ttu-id="78c25-121">Sanal makine uzantıları olabilir uygulanan tooa sanal makine ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="78c25-121">Virtual machine extensions can be applied tooa virtual machine scale set.</span></span> <span data-ttu-id="78c25-122">Bir sanal makine uzantısı ile tüm grup olarak ayarlanmış bir ölçek hello sanal makinelerde özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78c25-122">With a virtual machine extension, you can customize hello virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="78c25-123">Uzantıları hakkında daha fazla bilgi için bkz: [sanal makine uzantıları](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78c25-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="78c25-124">Kullanabileceğiniz üç ana uzantıları, Windows tabanlı veya Linux tabanlı açıksa işletim sisteminize bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="78c25-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="78c25-125">Windows</span><span class="sxs-lookup"><span data-stu-id="78c25-125">Windows</span></span>

<span data-ttu-id="78c25-126">Bir Windows tabanlı işletim sistemi için her iki hello kullanmak **özel komut dosyası v1.8** uzantısı veya hello **PowerShell DSC** uzantısı.</span><span class="sxs-lookup"><span data-stu-id="78c25-126">For a Windows-based operating system, use either hello **Custom Script v1.8** extension, or hello **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="78c25-127">Özel bir komut dosyası</span><span class="sxs-lookup"><span data-stu-id="78c25-127">Custom Script</span></span>

<span data-ttu-id="78c25-128">Merhaba özel betik uzantısı hello ölçek kümesindeki her sanal makine örneğindeki bir komut dosyasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="78c25-128">hello Custom Script extension runs a script on each virtual machine instance in hello scale set.</span></span> <span data-ttu-id="78c25-129">Bir yapılandırma dosyası veya değişken hangi dosyaların indirilen toohello sanal makine olduğunu ve ardından hangi komutu çalıştırır gösterir.</span><span class="sxs-lookup"><span data-stu-id="78c25-129">A config file or variable indicates which files are downloaded toohello virtual machine, and then what command runs.</span></span> <span data-ttu-id="78c25-130">Örneğin bu toorun bir yükleyici, bir komut dosyası, bir toplu iş dosyası, herhangi bir yürütülebilir dosya kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78c25-130">You could use this toorun an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="78c25-131">PowerShell hello ayarları için bir karma tablosu kullanır.</span><span class="sxs-lookup"><span data-stu-id="78c25-131">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="78c25-132">Bu örnek hello özel betik uzantısı toorun IIS yükleyen bir PowerShell komut dosyası yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="78c25-132">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="78c25-133">Kullanım hello `-ProtectedSetting` geçiş için hassas bilgiler içerebilir ayarları.</span><span class="sxs-lookup"><span data-stu-id="78c25-133">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="78c25-134">Azure CLI hello ayarları için bir json dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="78c25-134">Azure CLI uses a json file for hello settings.</span></span> <span data-ttu-id="78c25-135">Bu örnek hello özel betik uzantısı toorun IIS yükleyen bir PowerShell komut dosyası yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="78c25-135">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span> <span data-ttu-id="78c25-136">JSON dosyası olarak aşağıdaki hello Kaydet _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="78c25-136">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="78c25-137">Ardından, bu Azure CLI komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="78c25-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="78c25-138">Kullanım hello `--protected-settings` geçiş için hassas bilgiler içerebilir ayarları.</span><span class="sxs-lookup"><span data-stu-id="78c25-138">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="78c25-139">PowerShell DSC</span><span class="sxs-lookup"><span data-stu-id="78c25-139">PowerShell DSC</span></span>

<span data-ttu-id="78c25-140">PowerShell DSC toocustomize hello ölçek kümesi vm örneklerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78c25-140">You can use PowerShell DSC toocustomize hello scale set vm instances.</span></span> <span data-ttu-id="78c25-141">Merhaba **DSC** uzantısı yayımlanan tarafından **Microsoft.Powershell** dağıtır ve her sanal makine örneğinde sağlanan hello DSC yapılandırması çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="78c25-141">hello **DSC** extension published by **Microsoft.Powershell** deploys and runs hello provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="78c25-142">Bir yapılandırma dosyası veya değişken hello uzantısı söyler nerede *.zip* paketidir, hangilerinin _betik işlevi_ birleşimi toorun.</span><span class="sxs-lookup"><span data-stu-id="78c25-142">A config file or variable tells hello extension where *.zip* package is, and which _script-function_ combination toorun.</span></span>

<span data-ttu-id="78c25-143">PowerShell hello ayarları için bir karma tablosu kullanır.</span><span class="sxs-lookup"><span data-stu-id="78c25-143">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="78c25-144">Bu örnek, IIS yükleyen bir DSC paketi dağıtır.</span><span class="sxs-lookup"><span data-stu-id="78c25-144">This example deploys a DSC package that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="78c25-145">Kullanım hello `-ProtectedSetting` geçiş için hassas bilgiler içerebilir ayarları.</span><span class="sxs-lookup"><span data-stu-id="78c25-145">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="78c25-146">Azure CLI json hello ayarlarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="78c25-146">Azure CLI uses a json for hello settings.</span></span> <span data-ttu-id="78c25-147">Bu örnek, IIS yükleyen bir DSC paketi dağıtır.</span><span class="sxs-lookup"><span data-stu-id="78c25-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="78c25-148">JSON dosyası olarak aşağıdaki hello Kaydet _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="78c25-148">Save hello following json file as _settings.json_.</span></span>

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

<span data-ttu-id="78c25-149">Ardından, bu Azure CLI komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="78c25-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="78c25-150">Kullanım hello `--protected-settings` geçiş için hassas bilgiler içerebilir ayarları.</span><span class="sxs-lookup"><span data-stu-id="78c25-150">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="78c25-151">Linux</span><span class="sxs-lookup"><span data-stu-id="78c25-151">Linux</span></span>

<span data-ttu-id="78c25-152">Linux ya da hello kullanabileceğiniz **özel betik v2.0** uzantısı veya kullanım **bulut init** oluşturma sırasında.</span><span class="sxs-lookup"><span data-stu-id="78c25-152">Linux can use either hello **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="78c25-153">Özel komut dosyaları toohello sanal makine örnekleri indirir ve bir komut çalıştıran basit bir uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="78c25-153">Custom script is a simple extension that downloads files toohello virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="78c25-154">Özel bir komut dosyası</span><span class="sxs-lookup"><span data-stu-id="78c25-154">Custom Script</span></span>

<span data-ttu-id="78c25-155">JSON dosyası olarak aşağıdaki hello Kaydet _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="78c25-155">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="78c25-156">Sanal makine ölçek kümesi varolan bu uzantı tooan Hello Azure CLI tooadd kullanın.</span><span class="sxs-lookup"><span data-stu-id="78c25-156">Use hello Azure CLI tooadd this extension tooan existing virtual machine scale set.</span></span> <span data-ttu-id="78c25-157">Her bir sanal makine hello ölçeğinde çalıştırır hello uzantısı otomatik olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="78c25-157">Each virtual machine in hello scale set automatically runs hello extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="78c25-158">Kullanım hello `--protected-settings` geçiş için hassas bilgiler içerebilir ayarları.</span><span class="sxs-lookup"><span data-stu-id="78c25-158">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="78c25-159">Bulut başlatma</span><span class="sxs-lookup"><span data-stu-id="78c25-159">Cloud-Init</span></span>

<span data-ttu-id="78c25-160">Bulut Init Hello ölçek kümesi oluşturulurken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="78c25-160">Cloud-Init is used when hello scale set is created.</span></span> <span data-ttu-id="78c25-161">İlk olarak, adlı bir yerel dosya oluşturma _bulut init.txt_ ve yapılandırma tooit ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78c25-161">First, create a local file named _cloud-init.txt_ and add your configuration tooit.</span></span> <span data-ttu-id="78c25-162">Örneğin, [bu gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span><span class="sxs-lookup"><span data-stu-id="78c25-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="78c25-163">Kullanım hello Azure CLI toocreate ölçeği ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="78c25-163">Use hello Azure CLI toocreate a scale set.</span></span> <span data-ttu-id="78c25-164">Merhaba `--custom-data` alan bir bulut init betik hello dosya adını kabul eder.</span><span class="sxs-lookup"><span data-stu-id="78c25-164">hello `--custom-data` field accepts hello file name of a cloud-init script.</span></span>

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="78c25-165">Uygulama güncelleştirmeleri nasıl yönetebilirim?</span><span class="sxs-lookup"><span data-stu-id="78c25-165">How do I manage application updates?</span></span>

<span data-ttu-id="78c25-166">Uygulamanızı bir uzantısı aracılığıyla dağıttıysanız, bazı şekilde hello uzantısı tanımı alter.</span><span class="sxs-lookup"><span data-stu-id="78c25-166">If you deployed your application through an extension, alter hello extension definition in some way.</span></span> <span data-ttu-id="78c25-167">Bu değişiklik hello uzantısı imzalanmasını toobe tooall sanal makine örnekleri neden olur.</span><span class="sxs-lookup"><span data-stu-id="78c25-167">This change causes hello extension toobe redeployed tooall virtual machine instances.</span></span> <span data-ttu-id="78c25-168">Bir şey **gerekir** değiştirilmesi başvurulan dosyayı, aksi takdirde, yeniden adlandırma gibi hello uzantı hakkında Azure mu uzantısı hello görme değil değişti.</span><span class="sxs-lookup"><span data-stu-id="78c25-168">Something **must** be changed about hello extension, such as renaming a referenced file, otherwise, Azure does not see that hello extension has changed.</span></span>

<span data-ttu-id="78c25-169">Merhaba uygulaması kendi işletim sistemi görüntüsüne baked, bir otomatik dağıtım ardışık uygulama güncelleştirmelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="78c25-169">If you baked hello application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="78c25-170">Üretime ayarlayın aşamalı bir ölçek takas hızlı, mimarisi toofacilitate tasarlayın.</span><span class="sxs-lookup"><span data-stu-id="78c25-170">Design your architecture toofacilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="78c25-171">Bu yaklaşımın iyi bir örnek hello olan [Azure Spinnaker sürücü iş](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="78c25-171">A good example of this approach is hello [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="78c25-172">[Packer](https://www.packer.io/) ve [Terraform](https://www.terraform.io/) destek Azure Kaynak Yöneticisi, ayrıca görüntülerinizi "code" tanımlamak ve Azure'da, yapı ardından kullanır, bu nedenle hello VHD ölçek kümenizdeki.</span><span class="sxs-lookup"><span data-stu-id="78c25-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use hello VHD in your scale set.</span></span> <span data-ttu-id="78c25-173">Ancak, bunu yapmak bu nedenle burada Marketi'nden BITS doğrudan üzerinde değişiklik yapmazsınız beri uzantıları/özel komut dosyaları daha önemli hale Market görüntülerde sorunlu oluşur.</span><span class="sxs-lookup"><span data-stu-id="78c25-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="78c25-174">Bir ölçek ölçekler ayarladığınızda ne olduğunu çıkışı?</span><span class="sxs-lookup"><span data-stu-id="78c25-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="78c25-175">Bir veya daha fazla sanal makine tooa ölçek kümesi eklediğinizde, hello uygulama otomatik olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="78c25-175">When you add one or more virtual machines tooa scale set, hello application is automatically installed.</span></span> <span data-ttu-id="78c25-176">Örnek Hello ölçek kümesi uzantıları tanımlı sahipse için her oluşturulduğunda yeni bir sanal makinede çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="78c25-176">For example if hello scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="78c25-177">Merhaba ölçek kümesi üzerinde özel bir görüntü temel alıyorsa, yeni bir sanal makine hello kaynak özel görüntü kopyasıdır.</span><span class="sxs-lookup"><span data-stu-id="78c25-177">If hello scale set is based on a custom image, any new virtual machine is a copy of hello source custom image.</span></span> <span data-ttu-id="78c25-178">Merhaba ölçek kümesi sanal makineleri kapsayıcı ana bilgisayar varsa, bir özel betik uzantısı'nda başlangıç kod tooload Merhaba kapsayıcılara sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="78c25-178">If hello scale set virtual machines are container hosts, then you might have startup code tooload hello containers in a Custom Script Extension.</span></span> <span data-ttu-id="78c25-179">Veya, bir uzantı Azure kapsayıcı hizmeti gibi bir küme orchestrator ile kaydeder bir aracı yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78c25-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="78c25-180">Nasıl bir işletim sistemi güncelleştirmeyi güncelleştirme etki alanları arasında alma?</span><span class="sxs-lookup"><span data-stu-id="78c25-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="78c25-181">Merhaba sanal makine ölçek kümesi çalıştıran tutarken, işletim sistemi görüntüsü tooupdate istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="78c25-181">Suppose you want tooupdate your OS image while keeping hello virtual machine scale set running.</span></span> <span data-ttu-id="78c25-182">PowerShell ve Azure CLI hello hello sanal makine görüntüleri, aynı anda bir sanal makine güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78c25-182">PowerShell and hello Azure CLI can update hello virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="78c25-183">Merhaba [bir sanal makine ölçek kümesi yükseltme](./virtual-machine-scale-sets-upgrade-scale-set.md) makale ayrıca işletim sistemini yükseltme bir sanal makine ölçek kümesi boyunca kullanılabilir tooperform hangi seçeneklerdir daha fazla bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="78c25-183">hello [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available tooperform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="78c25-184">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="78c25-184">Next steps</span></span>

* [<span data-ttu-id="78c25-185">PowerShell toomanage kullanın, Ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="78c25-185">Use PowerShell toomanage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="78c25-186">Bir ölçek kümesi şablonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="78c25-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

