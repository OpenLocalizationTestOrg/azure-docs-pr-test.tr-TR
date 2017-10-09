---
title: "Windows için Ağ İzleyicisi Aracısı sanal makine uzantısı aaaAzure | Microsoft Docs"
description: "Bir sanal makine uzantısını kullanarak Windows sanal makine üzerinde Ağ İzleyicisi Aracısı Hello dağıtın."
services: virtual-machines-windows
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 27e46af7-2150-45e8-b084-ba33de8c5e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: 21298706e462ff32c4d314f9a1ad127074ddf481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="3f39b-103">Windows için Ağ İzleyicisi Aracısı sanal makine uzantısı</span><span class="sxs-lookup"><span data-stu-id="3f39b-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="3f39b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3f39b-104">Overview</span></span>

<span data-ttu-id="3f39b-105">[Azure Ağ İzleyicisi](https://review.docs.microsoft.com/en-us/azure/network-watcher/) Azure ağları için izleme sağlayan bir ağ performans izleme, tanılama ve analiz hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="3f39b-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="3f39b-106">Ağ İzleyicisi Aracısı sanal makine uzantısı Hello Azure sanal makinelerde hello Ağ İzleyicisi özelliklerinden bazıları için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="3f39b-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="3f39b-107">Bu, isteğe bağlı ve diğer gelişmiş işlevler üzerindeki ağ trafiğini yakalama içerir.</span><span class="sxs-lookup"><span data-stu-id="3f39b-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="3f39b-108">Bu belge ayrıntıları hello platformları ve dağıtım seçenekleri için Windows hello Ağ İzleyicisi Aracısı sanal makine uzantısı için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="3f39b-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f39b-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="3f39b-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="3f39b-110">İşletim sistemi</span><span class="sxs-lookup"><span data-stu-id="3f39b-110">Operating system</span></span>

<span data-ttu-id="3f39b-111">Windows, Windows Server 2008 R2 karşı çalıştırılabilir için hello Ağ İzleyicisi Aracısı uzantısı 2012, 2012 R2 ve 2016 serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="3f39b-111">hello Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="3f39b-112">Nano Server hello Not şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="3f39b-112">Note that hello Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="3f39b-113">İnternet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="3f39b-113">Internet connectivity</span></span>

<span data-ttu-id="3f39b-114">Merhaba Ağ İzleyicisi Aracısı işlevleri bazıları hello hedef sanal makinenin bağlı toohello Internet olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f39b-114">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="3f39b-115">Merhaba özelliği tooestablish giden bağlantılar hello Ağ İzleyicisi Aracısı özelliklerden bazıları düzgün çalışmamasına veya kullanılamaz hale.</span><span class="sxs-lookup"><span data-stu-id="3f39b-115">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="3f39b-116">Daha fazla ayrıntı için lütfen bkz hello [Ağ İzleyicisi belgeleri](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3f39b-116">For more details, please see hello [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="3f39b-117">Uzantı Şeması</span><span class="sxs-lookup"><span data-stu-id="3f39b-117">Extension schema</span></span>

<span data-ttu-id="3f39b-118">Merhaba aşağıdaki JSON hello Ağ İzleyicisi Aracısı uzantısı için hello şema gösterir.</span><span class="sxs-lookup"><span data-stu-id="3f39b-118">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="3f39b-119">Merhaba uzantısı ne gerektirir ya da şu anda herhangi bir kullanıcı tarafından sağlanan ayarını destekler ve kendi varsayılan yapılandırmasına dayanır.</span><span class="sxs-lookup"><span data-stu-id="3f39b-119">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

```json
{
    "type": "extensions",
    "name": "Microsoft.Azure.NetworkWatcher",
    "apiVersion": "[variables('apiVersion')]",
    "location": "[resourceGroup().location]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "properties": {
        "publisher": "Microsoft.Azure.NetworkWatcher",
        "type": "NetworkWatcherAgentWindows",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="3f39b-120">Özellik değerleri</span><span class="sxs-lookup"><span data-stu-id="3f39b-120">Property values</span></span>

| <span data-ttu-id="3f39b-121">Ad</span><span class="sxs-lookup"><span data-stu-id="3f39b-121">Name</span></span> | <span data-ttu-id="3f39b-122">Değer / örnek</span><span class="sxs-lookup"><span data-stu-id="3f39b-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="3f39b-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="3f39b-123">apiVersion</span></span> | <span data-ttu-id="3f39b-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="3f39b-124">2015-06-15</span></span> |
| <span data-ttu-id="3f39b-125">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="3f39b-125">publisher</span></span> | <span data-ttu-id="3f39b-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="3f39b-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="3f39b-127">type</span><span class="sxs-lookup"><span data-stu-id="3f39b-127">type</span></span> | <span data-ttu-id="3f39b-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="3f39b-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="3f39b-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="3f39b-129">typeHandlerVersion</span></span> | <span data-ttu-id="3f39b-130">1.4</span><span class="sxs-lookup"><span data-stu-id="3f39b-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="3f39b-131">Şablon dağıtımı</span><span class="sxs-lookup"><span data-stu-id="3f39b-131">Template deployment</span></span>

<span data-ttu-id="3f39b-132">Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="3f39b-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="3f39b-133">Merhaba JSON şeması Hello önceki bölümde ayrıntılı bir Azure Resource Manager şablon dağıtımı sırasında bir Azure Resource Manager şablonu toorun hello Ağ İzleyicisi Aracısı uzantısı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="3f39b-133">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="3f39b-134">PowerShell dağıtım</span><span class="sxs-lookup"><span data-stu-id="3f39b-134">PowerShell deployment</span></span>

<span data-ttu-id="3f39b-135">Merhaba `Set-AzureRmVMExtension` komutu kullanılan toodeploy hello Ağ İzleyicisi Aracısı sanal makine uzantısı tooan varolan sanal makine olabilir.</span><span class="sxs-lookup"><span data-stu-id="3f39b-135">hello `Set-AzureRmVMExtension` command can be used toodeploy hello Network Watcher Agent virtual machine extension tooan existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="3f39b-136">Sorun giderme ve destek</span><span class="sxs-lookup"><span data-stu-id="3f39b-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="3f39b-137">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="3f39b-137">Troubleshooting</span></span>

<span data-ttu-id="3f39b-138">Veri uzantısı dağıtımları hello durumuyla ilgili hello Azure portal ve hello Azure PowerShell modülü kullanılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="3f39b-138">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure PowerShell module.</span></span> <span data-ttu-id="3f39b-139">Aşağıdaki komutu kullanarak çalışma hello belirli bir VM için uzantıların toosee hello dağıtım durumu hello Azure PowerShell modülü.</span><span class="sxs-lookup"><span data-stu-id="3f39b-139">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="3f39b-140">Uzantı yürütme hello bulunan oturum toofiles directory aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="3f39b-140">Extension execution output is logged toofiles found in hello following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="3f39b-141">Destek</span><span class="sxs-lookup"><span data-stu-id="3f39b-141">Support</span></span>

<span data-ttu-id="3f39b-142">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, toohello Ağ İzleyicisi kullanıcı kılavuzu belgelerine başvurun veya hello Azure başvurun hello uzmanlarıyla [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="3f39b-142">If you need more help at any point in this article, you can refer toohello Network Watcher User Guide documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="3f39b-143">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="3f39b-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="3f39b-144">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin.</span><span class="sxs-lookup"><span data-stu-id="3f39b-144">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="3f39b-145">Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="3f39b-145">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
