---
title: "aaaVirtual Linux için uzantıları ve özellikleri makine | Microsoft Docs"
description: "Hangi uzantıları ne bunlar sağlayın veya geliştirmek tarafından gruplandırılmış Azure sanal makineler için kullanılabilir olduğunu öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 52f5d0ec-8f75-49e7-9e15-88d46b420e63
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: nepeters
ms.openlocfilehash: e0d2ce794c76815ccc6743e8788ee5d9d931e9a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machine-extensions-and-features-for-linux"></a><span data-ttu-id="5087e-103">Sanal makine uzantıları ve Linux için özellikleri</span><span class="sxs-lookup"><span data-stu-id="5087e-103">Virtual machine extensions and features for Linux</span></span>

<span data-ttu-id="5087e-104">Azure sanal makine uzantıları Azure sanal makinelerde dağıtım sonrası yapılandırma ve Otomasyon görevlerini sağlayan küçük uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="5087e-104">Azure virtual machine extensions are small applications that provide post-deployment configuration and automation tasks on Azure virtual machines.</span></span> <span data-ttu-id="5087e-105">Örneğin, bir sanal makineye yazılım yükleme, virüsten koruma veya Docker yapılandırma gerektiriyorsa, VM uzantısı için kullanılan toocomplete bu görevleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-105">For example, if a virtual machine requires software installation, anti-virus protection, or Docker configuration, a VM extension can be used toocomplete these tasks.</span></span> <span data-ttu-id="5087e-106">Azure VM uzantıları ve Azure portal hello hello Azure CLI, PowerShell, Azure Resource Manager şablonları kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5087e-106">Azure VM extensions can be run using hello Azure CLI, PowerShell, Azure Resource Manager templates, and hello Azure portal.</span></span> <span data-ttu-id="5087e-107">Uzantıları ile yeni bir sanal makine dağıtımı paketlenebilir veya varolan bir sistemle bağlantılı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5087e-107">Extensions can be bundled with a new virtual machine deployment, or run against any existing system.</span></span>

<span data-ttu-id="5087e-108">Bu belge VM uzantıları, Azure VM uzantıları ve Kılavuzu nasıl toodetect, yönetme ve VM uzantıları kaldırma üzerinde kullanma önkoşulları genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="5087e-108">This document provides an overview of VM extensions, prerequisites for using Azure VM extensions, and guidance on how toodetect, manage, and remove VM extensions.</span></span> <span data-ttu-id="5087e-109">Birçok VM uzantıları bulunduğundan, bu belgede genelleştirilmiş bilgiler sağlanmaktadır her potansiyel olarak benzersiz bir yapılandırmaya sahip.</span><span class="sxs-lookup"><span data-stu-id="5087e-109">This document provides generalized information because many VM extensions are available, each with a potentially unique configuration.</span></span> <span data-ttu-id="5087e-110">Uzantı özel ayrıntıları her belge belirli toohello tek tek uzantısı'nda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-110">Extension-specific details can be found in each document specific toohello individual extension.</span></span>

## <a name="use-cases-and-samples"></a><span data-ttu-id="5087e-111">Kullanım örnekleri ve örnekler</span><span class="sxs-lookup"><span data-stu-id="5087e-111">Use cases and samples</span></span>

<span data-ttu-id="5087e-112">Birkaç farklı Azure VM uzantıları kullanılabilir, her biri belirli bir kullanım örneği.</span><span class="sxs-lookup"><span data-stu-id="5087e-112">Several different Azure VM extensions are available, each with a specific use case.</span></span> <span data-ttu-id="5087e-113">Bazı örnekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5087e-113">Some examples are:</span></span>

- <span data-ttu-id="5087e-114">Linux için hello DSC uzantısı kullanarak PowerShell istenen durum yapılandırması tooa sanal makine uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5087e-114">Apply PowerShell Desired State configurations tooa virtual machine using hello DSC extension for Linux.</span></span> <span data-ttu-id="5087e-115">Daha fazla bilgi için bkz: [Azure istenen durum yapılandırması uzantısı](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span><span class="sxs-lookup"><span data-stu-id="5087e-115">For more information, see [Azure Desired State configuration extension](https://github.com/Azure/azure-linux-extensions/tree/master/DSC).</span></span>
- <span data-ttu-id="5087e-116">Bir sanal makinenin hello Microsoft İzleme Aracısı VM uzantısı ile izlemeyi yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="5087e-116">Configure monitoring of a virtual machine with hello Microsoft Monitoring Agent VM extension.</span></span> <span data-ttu-id="5087e-117">Daha fazla bilgi için bkz: [nasıl toomonitor bir Linux VM](tutorial-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="5087e-117">For more information, see [How toomonitor a Linux VM](tutorial-monitoring.md).</span></span>
- <span data-ttu-id="5087e-118">Azure altyapınızın hello Datadog uzantısı ile izlemeyi yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="5087e-118">Configure monitoring of your Azure infrastructure with hello Datadog extension.</span></span> <span data-ttu-id="5087e-119">Daha fazla bilgi için bkz: Merhaba [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span><span class="sxs-lookup"><span data-stu-id="5087e-119">For more information, see hello [Datadog blog](https://www.datadoghq.com/blog/introducing-azure-monitoring-with-one-click-datadog-deployment/).</span></span>
- <span data-ttu-id="5087e-120">Docker ana hello Docker VM uzantısı kullanılarak Azure sanal makinesi üzerinde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="5087e-120">Configure a Docker host on an Azure virtual machine using hello Docker VM extension.</span></span> <span data-ttu-id="5087e-121">Daha fazla bilgi için bkz: [Docker VM uzantısı](dockerextension.md).</span><span class="sxs-lookup"><span data-stu-id="5087e-121">For more information, see [Docker VM extension](dockerextension.md).</span></span>

<span data-ttu-id="5087e-122">Ayrıca tooprocess özgü uzantılar, özel betik uzantısı hem Windows hem de Linux sanal makineler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-122">In addition tooprocess-specific extensions, a Custom Script extension is available for both Windows and Linux virtual machines.</span></span> <span data-ttu-id="5087e-123">Merhaba özel betik uzantısı Linux için bir sanal makine üzerinde çalışan tüm Bash betik toobe sağlar.</span><span class="sxs-lookup"><span data-stu-id="5087e-123">hello Custom Script extension for Linux allows any Bash script toobe run on a virtual machine.</span></span> <span data-ttu-id="5087e-124">Özel komut dosyaları, yerel hangi Azure araçlar sağlayabilir ötesinde yapılandırma gerektiren Azure dağıtımları tasarlamak için faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="5087e-124">Custom scripts are useful for designing Azure deployments that require configuration beyond what native Azure tooling can provide.</span></span> <span data-ttu-id="5087e-125">Daha fazla bilgi için bkz: [Linux VM özel betik uzantısı](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="5087e-125">For more information, see [Linux VM Custom Script extension](extensions-customscript.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="5087e-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5087e-126">Prerequisites</span></span>

<span data-ttu-id="5087e-127">Her sanal makine uzantısı önkoşulları kendi kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-127">Each virtual machine extension might have its own set of prerequisites.</span></span> <span data-ttu-id="5087e-128">Örneği için bir önkoşul desteklenen Linux dağıtım hello Docker VM uzantısı vardır.</span><span class="sxs-lookup"><span data-stu-id="5087e-128">For instance, hello Docker VM extension has a prerequisite of a supported Linux distribution.</span></span> <span data-ttu-id="5087e-129">Tek tek uzantıların gereksinimlerini hello uzantıya özgü belgelerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5087e-129">Requirements of individual extensions are detailed in hello extension-specific documentation.</span></span>

### <a name="azure-vm-agent"></a><span data-ttu-id="5087e-130">Azure VM aracısı</span><span class="sxs-lookup"><span data-stu-id="5087e-130">Azure VM agent</span></span>

<span data-ttu-id="5087e-131">Hello Azure VM Aracısı bir Azure sanal makinesi ve hello Azure yapı denetleyicisi arasındaki etkileşimler yönetir.</span><span class="sxs-lookup"><span data-stu-id="5087e-131">hello Azure VM agent manages interactions between an Azure virtual machine and hello Azure fabric controller.</span></span> <span data-ttu-id="5087e-132">Merhaba VM Aracısı dağıtma ve yönetme Azure sanal makineler, çalışan VM uzantıları dahil olmak üzere birçok işlevsel görünüşlere için sorumludur.</span><span class="sxs-lookup"><span data-stu-id="5087e-132">hello VM agent is responsible for many functional aspects of deploying and managing Azure virtual machines, including running VM extensions.</span></span> <span data-ttu-id="5087e-133">Hello Azure VM Aracısı Azure Marketi görüntülerinde önceden yüklenmiş ve desteklenen işletim sistemlerinde el ile yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-133">hello Azure VM agent is preinstalled on Azure Marketplace images and can be installed manually on supported operating systems.</span></span>

<span data-ttu-id="5087e-134">Desteklenen işletim sistemleri ve yükleme yönergeleri hakkında daha fazla bilgi için bkz: [Azure sanal makine Aracısı](../windows/classic/agents-and-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="5087e-134">For information on supported operating systems and installation instructions, see [Azure virtual machine agent](../windows/classic/agents-and-extensions.md).</span></span>

## <a name="discover-vm-extensions"></a><span data-ttu-id="5087e-135">VM uzantıları Bul</span><span class="sxs-lookup"><span data-stu-id="5087e-135">Discover VM extensions</span></span>

<span data-ttu-id="5087e-136">Birçok farklı VM uzantıları, Azure sanal makineler ile kullanmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-136">Many different VM extensions are available for use with Azure virtual machines.</span></span> <span data-ttu-id="5087e-137">tam bir listesi, toosee hello Azure CLI komutuyla izleyerek, tercih ettiğiniz hello konumla hello Örnek konum değiştirme hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5087e-137">toosee a complete list, run hello following command with hello Azure CLI, replacing hello example location with hello location of your choice.</span></span>

```azurecli
az vm extension image list --location westus -o table
```

## <a name="run-vm-extensions"></a><span data-ttu-id="5087e-138">VM uzantıları çalıştırın</span><span class="sxs-lookup"><span data-stu-id="5087e-138">Run VM extensions</span></span>

<span data-ttu-id="5087e-139">Azure sanal makine uzantıları toomake yapılandırma değişiklikleri gerekir ya da bağlantı zaten dağıtılmış bir VM'de kurtarmak bağlandığınızda yararlıdır ve mevcut sanal makineler üzerinde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-139">Azure virtual machine extensions can be run on existing virtual machines, which are useful when you need toomake configuration changes or recover connectivity on an already deployed VM.</span></span> <span data-ttu-id="5087e-140">VM uzantıları, Azure Resource Manager şablonu dağıtımlarında da gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-140">VM extensions can also be bundled with Azure Resource Manager template deployments.</span></span> <span data-ttu-id="5087e-141">Resource Manager şablonları ile uzantıları kullanarak, Azure sanal makineleri dağıtılabilir ve dağıtım sonrası müdahalesi olmadan yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="5087e-141">By using extensions with Resource Manager templates, Azure virtual machines can be deployed and configured without post-deployment intervention.</span></span>

<span data-ttu-id="5087e-142">yöntemler aşağıdaki hello kullanılan toorun uzantı var olan bir sanal makineye karşı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-142">hello following methods can be used toorun an extension against an existing virtual machine.</span></span>

### <a name="azure-cli"></a><span data-ttu-id="5087e-143">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5087e-143">Azure CLI</span></span>

<span data-ttu-id="5087e-144">Azure sanal makine uzantıları çalıştırılabilir karşı var olan bir sanal makine hello kullanarak `az vm extension set` komutu.</span><span class="sxs-lookup"><span data-stu-id="5087e-144">Azure virtual machine extensions can be run against an existing virtual machine by using hello `az vm extension set` command.</span></span> <span data-ttu-id="5087e-145">Bu örnek, bir sanal makine hello özel betik uzantısı çalışır.</span><span class="sxs-lookup"><span data-stu-id="5087e-145">This example runs hello custom script extension against a virtual machine.</span></span>

```azurecli
az vm extension set `
  --resource-group exttest `
  --vm-name exttest `
  --name customScript `
  --publisher Microsoft.Azure.Extensions `
  --settings '{"fileUris": ["https://gist.github.com/ahmetalpbalkan/b5d4a856fe15464015ae87d5587a4439/raw/466f5c30507c990a4d5a2f5c79f901fa89a80841/hello.sh"],"commandToExecute": "./hello.sh"}'
```

<span data-ttu-id="5087e-146">komut dosyası oluşturduğu çıktı benzer toohello metin aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="5087e-146">hello script produces output similar toohello following text:</span></span>

```azurecli
info:    Executing command vm extension set
+ Looking up hello VM "myVM"
+ Installing extension "CustomScript", VM: "mvVM"
info:    vm extension set command OK
```

### <a name="azure-portal"></a><span data-ttu-id="5087e-147">Azure portalına</span><span class="sxs-lookup"><span data-stu-id="5087e-147">Azure portal</span></span>

<span data-ttu-id="5087e-148">VM uzantıları hello Azure portal aracılığıyla uygulanan tooan varolan sanal makine olabilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-148">VM extensions can be applied tooan existing virtual machine through hello Azure portal.</span></span> <span data-ttu-id="5087e-149">toodo hello sanal makine, bu nedenle, seçin seçin **uzantıları**, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="5087e-149">toodo so, select hello virtual machine, choose **Extensions**, and click **Add**.</span></span> <span data-ttu-id="5087e-150">Kullanılabilir uzantılar hello listeden istediğiniz ve hello hello sihirbazındaki yönergeleri izleyin hello uzantıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="5087e-150">Select hello extension you want from hello list of available extensions and follow hello instructions in hello wizard.</span></span>

<span data-ttu-id="5087e-151">Merhaba aşağıdaki görüntüde hello Linux özel betik uzantısı hello Azure Portalı'ndan hello yüklemesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="5087e-151">hello following image shows hello installation of hello Linux Custom Script extension from hello Azure portal.</span></span>

![Özel betik uzantısı yükleyin](./media/extensions-features/installscriptextensionlinux.png)

### <a name="azure-resource-manager-templates"></a><span data-ttu-id="5087e-153">Azure Resource Manager şablonları</span><span class="sxs-lookup"><span data-stu-id="5087e-153">Azure Resource Manager templates</span></span>

<span data-ttu-id="5087e-154">VM uzantıları eklenen tooan Azure Resource Manager şablonu olabilir ve hello şablon hello dağıtımı ile yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="5087e-154">VM extensions can be added tooan Azure Resource Manager template and executed with hello deployment of hello template.</span></span> <span data-ttu-id="5087e-155">Bir şablon uzantılı dağıttığınızda, tam olarak yapılandırılmış Azure dağıtımları oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="5087e-155">When you deploy an extension with a template, you can create fully configured Azure deployments.</span></span> <span data-ttu-id="5087e-156">Örneğin, aşağıdaki JSON bir Resource Manager şablondan alınmış hello.</span><span class="sxs-lookup"><span data-stu-id="5087e-156">For example, hello following JSON is taken from a Resource Manager template.</span></span> <span data-ttu-id="5087e-157">Merhaba şablonu bir dizi yük dengeli sanal makineler ve Azure SQL Veritabanını dağıtır ve ardından bir .NET Core uygulaması her VM yükler.</span><span class="sxs-lookup"><span data-stu-id="5087e-157">hello template deploys a set of load-balanced virtual machines and an Azure SQL database, and then installs a .NET Core application on each VM.</span></span> <span data-ttu-id="5087e-158">Merhaba VM uzantısı hello yazılım yüklemesini mvc'deki.</span><span class="sxs-lookup"><span data-stu-id="5087e-158">hello VM extension takes care of hello software installation.</span></span>

<span data-ttu-id="5087e-159">Daha fazla bilgi için bkz: hello tam [Resource Manager şablonu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span><span class="sxs-lookup"><span data-stu-id="5087e-159">For more information, see hello full [Resource Manager template](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).</span></span>

```json
{
    "apiVersion": "2015-06-15",
    "type": "extensions",
    "name": "config-app",
    "location": "[resourceGroup().location]",
    "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
    ],
    "tags": {
    "displayName": "config-app"
    },
    "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
        "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
        ]
    },
    "protectedSettings": {
        "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
    }
}
```

<span data-ttu-id="5087e-160">Daha fazla bilgi için bkz: [Azure Resource Manager şablonları yazma](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span><span class="sxs-lookup"><span data-stu-id="5087e-160">For more information, see [Authoring Azure Resource Manager templates](../windows/template-description.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#extensions).</span></span>

## <a name="secure-vm-extension-data"></a><span data-ttu-id="5087e-161">VM uzantısı verileri güvenli</span><span class="sxs-lookup"><span data-stu-id="5087e-161">Secure VM extension data</span></span>

<span data-ttu-id="5087e-162">VM uzantısı çalıştırırken kimlik bilgilerini, depolama hesabı adları ve depolama hesabı erişim anahtarlarını gibi hassas bilgileri gerekli tooinclude olabilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-162">When you're running a VM extension, it may be necessary tooinclude sensitive information such as credentials, storage account names, and storage account access keys.</span></span> <span data-ttu-id="5087e-163">Birçok VM uzantıları verileri şifreler ve yalnızca hello hedef sanal makine içinde şifresini çözer korumalı bir yapılandırmayı içerir.</span><span class="sxs-lookup"><span data-stu-id="5087e-163">Many VM extensions include a protected configuration that encrypts data and only decrypts it inside hello target virtual machine.</span></span> <span data-ttu-id="5087e-164">Belirli korumalı yapılandırma şeması her uzantısına sahip ve her uzantıya özgü belgelerinde ayrıntılı olarak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5087e-164">Each extension has a specific protected configuration schema, and each is detailed in extension-specific documentation.</span></span>

<span data-ttu-id="5087e-165">Aşağıdaki örneğine hello Linux için hello özel betik uzantısı örneğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="5087e-165">hello following example shows an instance of hello Custom Script extension for Linux.</span></span> <span data-ttu-id="5087e-166">Bu hello komutu tooexecute kimlik bilgileri kümesi içerir dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="5087e-166">Notice that hello command tooexecute includes a set of credentials.</span></span> <span data-ttu-id="5087e-167">Bu örnekte, hello komutu tooexecute şifrelenmez.</span><span class="sxs-lookup"><span data-stu-id="5087e-167">In this example, hello command tooexecute will not be encrypted.</span></span>


```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ],
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

<span data-ttu-id="5087e-168">Taşıma hello **komutu tooexecute** özelliği toohello **korumalı** yapılandırma hello yürütme dize güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="5087e-168">Moving hello **command tooexecute** property toohello **protected** configuration secures hello execution string.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', concat(variables('vmName'),copyindex()))]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "CustomScript",
    "typeHandlerVersion": "2.0",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-linux/scripts/config-music.sh"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('sudo sh config-music.sh ',variables('musicStoreSqlName'), ' ', parameters('adminUsername'), ' ', parameters('sqlAdminPassword'))]"
    }
  }
}
```

## <a name="troubleshoot-vm-extensions"></a><span data-ttu-id="5087e-169">VM uzantıları sorun giderme</span><span class="sxs-lookup"><span data-stu-id="5087e-169">Troubleshoot VM extensions</span></span>

<span data-ttu-id="5087e-170">Her VM uzantısı sorun giderme adımları belirli toohello uzantısına sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-170">Each VM extension may have troubleshooting steps specific toohello extension.</span></span> <span data-ttu-id="5087e-171">Örneğin, hello özel betik uzantısı kullanırken, komut dosyası yürütme ayrıntılarını yerel olarak hello uzantısı çalıştırıldığı hello sanal makine üzerinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-171">For example, when you're using hello Custom Script extension, script execution details can be found locally on hello virtual machine on which hello extension was run.</span></span> <span data-ttu-id="5087e-172">Uzantı özel sorun giderme işlemleri uzantıya özgü belgelerinde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5087e-172">Any extension-specific troubleshooting steps are detailed in extension-specific documentation.</span></span>

<span data-ttu-id="5087e-173">Aşağıdaki sorun giderme adımları hello tooall sanal makine uzantıları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="5087e-173">hello following troubleshooting steps apply tooall virtual machine extensions.</span></span>

### <a name="view-extension-status"></a><span data-ttu-id="5087e-174">Uzantı durumunu görüntüle</span><span class="sxs-lookup"><span data-stu-id="5087e-174">View extension status</span></span>

<span data-ttu-id="5087e-175">Bir sanal makine uzantısı bir sanal makine çalıştırdıktan sonra Azure CLI komutu tooreturn uzantı durumunu izleyen hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="5087e-175">After a virtual machine extension has been run against a virtual machine, use hello following Azure CLI command tooreturn extension status.</span></span> <span data-ttu-id="5087e-176">Örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5087e-176">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension list --resource-group myResourceGroup --vm-name myVM -o table
```

<span data-ttu-id="5087e-177">Merhaba çıktı hello metin aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="5087e-177">hello output looks like hello following text:</span></span>

```azurecli
AutoUpgradeMinorVersion    Location    Name          ProvisioningState    Publisher                   ResourceGroup      TypeHandlerVersion  VirtualMachineExtensionType
-------------------------  ----------  ------------  -------------------  --------------------------  ---------------  --------------------  -----------------------------
True                       westus      customScript  Succeeded            Microsoft.Azure.Extensions  exttest                             2  customScript
```

<span data-ttu-id="5087e-178">Uzantı yürütme durumu da hello Azure portalında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="5087e-178">Extension execution status can also be found in hello Azure portal.</span></span> <span data-ttu-id="5087e-179">tooview hello durumu select hello sanal makine, bir uzantı seçin **uzantıları**, ve hello istenen uzantı seçin.</span><span class="sxs-lookup"><span data-stu-id="5087e-179">tooview hello status of an extension, select hello virtual machine, choose **Extensions**, and select hello desired extension.</span></span>

### <a name="rerun-a-vm-extension"></a><span data-ttu-id="5087e-180">VM uzantısı yeniden çalıştırın</span><span class="sxs-lookup"><span data-stu-id="5087e-180">Rerun a VM extension</span></span>

<span data-ttu-id="5087e-181">Bir sanal makine uzantısı toobe gereken durumlar olabilir yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5087e-181">There may be cases in which a virtual machine extension needs toobe rerun.</span></span> <span data-ttu-id="5087e-182">Uzantı, kaldırarak ve tercih ettiğiniz yürütme yöntemiyle hello uzantısı yeniden çalıştırma çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5087e-182">You can rerun an extension by removing it, and then rerunning hello extension with an execution method of your choice.</span></span> <span data-ttu-id="5087e-183">bir uzantı tooremove hello Azure CLI komutuyla aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5087e-183">tooremove an extension, run hello following command with hello Azure CLI.</span></span> <span data-ttu-id="5087e-184">Örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5087e-184">Replace example parameter names with your own values.</span></span>

```azurecli
az vm extension delete --name customScript --resource-group myResourceGroup --vm-name myVM
```

<span data-ttu-id="5087e-185">Uzantı hello Azure Portalı'ndaki adımları izleyerek hello kullanarak kaldırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5087e-185">You can remove an extension by using hello following steps in hello Azure portal:</span></span>

1. <span data-ttu-id="5087e-186">Bir sanal makineyi seçin.</span><span class="sxs-lookup"><span data-stu-id="5087e-186">Select a virtual machine.</span></span>
2. <span data-ttu-id="5087e-187">Seçin **uzantıları**.</span><span class="sxs-lookup"><span data-stu-id="5087e-187">Choose **Extensions**.</span></span>
3. <span data-ttu-id="5087e-188">İstenen hello uzantıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="5087e-188">Select hello desired extension.</span></span>
4. <span data-ttu-id="5087e-189">Seçin **kaldırma**.</span><span class="sxs-lookup"><span data-stu-id="5087e-189">Choose **Uninstall**.</span></span>

## <a name="common-vm-extension-reference"></a><span data-ttu-id="5087e-190">Ortak VM uzantısı başvurusu</span><span class="sxs-lookup"><span data-stu-id="5087e-190">Common VM extension reference</span></span>
| <span data-ttu-id="5087e-191">Uzantı adı</span><span class="sxs-lookup"><span data-stu-id="5087e-191">Extension name</span></span> | <span data-ttu-id="5087e-192">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5087e-192">Description</span></span> | <span data-ttu-id="5087e-193">Daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="5087e-193">More information</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5087e-194">Linux için özel betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="5087e-194">Custom Script extension for Linux</span></span> |<span data-ttu-id="5087e-195">Bir Azure sanal makinesi karşı komut dosyalarını çalıştır</span><span class="sxs-lookup"><span data-stu-id="5087e-195">Run scripts against an Azure virtual machine</span></span> |[<span data-ttu-id="5087e-196">Linux için özel betik uzantısı</span><span class="sxs-lookup"><span data-stu-id="5087e-196">Custom Script extension for Linux</span></span>](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="5087e-197">Docker uzantısı</span><span class="sxs-lookup"><span data-stu-id="5087e-197">Docker extension</span></span> |<span data-ttu-id="5087e-198">Merhaba Docker arka plan programı toosupport uzak Docker komutları yükleyin.</span><span class="sxs-lookup"><span data-stu-id="5087e-198">Install hello Docker daemon toosupport remote Docker commands.</span></span> |[<span data-ttu-id="5087e-199">Docker VM uzantısı</span><span class="sxs-lookup"><span data-stu-id="5087e-199">Docker VM extension</span></span>](dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) |
| <span data-ttu-id="5087e-200">VM Erişimi uzantısı</span><span class="sxs-lookup"><span data-stu-id="5087e-200">VM Access extension</span></span> |<span data-ttu-id="5087e-201">Erişim tooan Azure sanal makinesi yeniden elde</span><span class="sxs-lookup"><span data-stu-id="5087e-201">Regain access tooan Azure virtual machine</span></span> |[<span data-ttu-id="5087e-202">VM Erişimi uzantısı</span><span class="sxs-lookup"><span data-stu-id="5087e-202">VM Access extension</span></span>](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess) |
| <span data-ttu-id="5087e-203">Azure tanılama uzantısını</span><span class="sxs-lookup"><span data-stu-id="5087e-203">Azure Diagnostics extension</span></span> |<span data-ttu-id="5087e-204">Azure tanılama yönetme</span><span class="sxs-lookup"><span data-stu-id="5087e-204">Manage Azure Diagnostics</span></span> |[<span data-ttu-id="5087e-205">Azure tanılama uzantısını</span><span class="sxs-lookup"><span data-stu-id="5087e-205">Azure Diagnostics extension</span></span>](https://azure.microsoft.com/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/) |
| <span data-ttu-id="5087e-206">Azure VM erişim uzantısı</span><span class="sxs-lookup"><span data-stu-id="5087e-206">Azure VM Access extension</span></span> |<span data-ttu-id="5087e-207">Kullanıcılar ve kimlik bilgilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="5087e-207">Manage users and credentials</span></span> |[<span data-ttu-id="5087e-208">Linux VM erişim uzantısı</span><span class="sxs-lookup"><span data-stu-id="5087e-208">VM Access extension for Linux</span></span>](https://azure.microsoft.com/en-us/blog/using-vmaccess-extension-to-reset-login-credentials-for-linux-vm/) |
