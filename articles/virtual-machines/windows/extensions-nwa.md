---
title: "Windows için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı | Microsoft Docs"
description: "Ağ İzleyicisi Aracısı'nı kullanarak bir sanal makine uzantısı Windows sanal makine dağıtın."
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
ms.openlocfilehash: b8d6a998bc86337b286a3434f44f762cca9b7e68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-windows"></a><span data-ttu-id="0194b-103">Windows için Ağ İzleyicisi Aracısı sanal makine uzantısı</span><span class="sxs-lookup"><span data-stu-id="0194b-103">Network Watcher Agent virtual machine extension for Windows</span></span>

## <a name="overview"></a><span data-ttu-id="0194b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0194b-104">Overview</span></span>

<span data-ttu-id="0194b-105">[Azure Ağ İzleyicisi](https://review.docs.microsoft.com/en-us/azure/network-watcher/) Azure ağları için izleme sağlayan bir ağ performans izleme, tanılama ve analiz hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="0194b-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="0194b-106">Ağ İzleyicisi Aracısı sanal makine uzantısı, Azure sanal makinelerde Ağ İzleyicisi özelliklerinden bazıları için bir gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="0194b-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="0194b-107">Bu, isteğe bağlı ve diğer gelişmiş işlevler üzerindeki ağ trafiğini yakalama içerir.</span><span class="sxs-lookup"><span data-stu-id="0194b-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="0194b-108">Bu belge, Windows için Ağ İzleyicisi Aracısı sanal makine uzantısı için dağıtım seçenekleri ve desteklenen platformlar ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="0194b-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Windows.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0194b-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0194b-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="0194b-110">İşletim sistemi</span><span class="sxs-lookup"><span data-stu-id="0194b-110">Operating system</span></span>

<span data-ttu-id="0194b-111">Windows, Windows Server 2008 R2 karşı çalıştırılabilir için Ağ İzleyicisi Aracısı uzantısı 2012, 2012 R2 ve 2016 serbest bırakır.</span><span class="sxs-lookup"><span data-stu-id="0194b-111">The Network Watcher Agent extension for Windows can be run against Windows Server 2008 R2, 2012, 2012 R2, and 2016 releases.</span></span> <span data-ttu-id="0194b-112">Nano Server şu anda desteklenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0194b-112">Note that the Nano Server is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="0194b-113">İnternet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="0194b-113">Internet connectivity</span></span>

<span data-ttu-id="0194b-114">Bazı Ağ İzleyicisi Aracısı işlevlerini hedef sanal makine Internet'e bağlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0194b-114">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="0194b-115">Giden bağlantıları kurmak için özelliği olmadan Ağ İzleyicisi Aracısı özelliklerden bazıları arıza veya kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="0194b-115">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="0194b-116">Daha fazla ayrıntı için lütfen bkz. [Ağ İzleyicisi belgeleri](../../network-watcher/network-watcher-monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0194b-116">For more details, please see the [Network Watcher documentation](../../network-watcher/network-watcher-monitoring-overview.md).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="0194b-117">Uzantı Şeması</span><span class="sxs-lookup"><span data-stu-id="0194b-117">Extension schema</span></span>

<span data-ttu-id="0194b-118">Aşağıdaki JSON şeması Ağ İzleyicisi Aracısı uzantısı gösterir.</span><span class="sxs-lookup"><span data-stu-id="0194b-118">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="0194b-119">Uzantı ne gerektirir ya da şu anda herhangi bir kullanıcı tarafından sağlanan ayarını destekler ve kendi varsayılan yapılandırmasına dayanır.</span><span class="sxs-lookup"><span data-stu-id="0194b-119">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="0194b-120">Özellik değerleri</span><span class="sxs-lookup"><span data-stu-id="0194b-120">Property values</span></span>

| <span data-ttu-id="0194b-121">Ad</span><span class="sxs-lookup"><span data-stu-id="0194b-121">Name</span></span> | <span data-ttu-id="0194b-122">Değer / örnek</span><span class="sxs-lookup"><span data-stu-id="0194b-122">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="0194b-123">apiVersion</span><span class="sxs-lookup"><span data-stu-id="0194b-123">apiVersion</span></span> | <span data-ttu-id="0194b-124">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="0194b-124">2015-06-15</span></span> |
| <span data-ttu-id="0194b-125">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="0194b-125">publisher</span></span> | <span data-ttu-id="0194b-126">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="0194b-126">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="0194b-127">type</span><span class="sxs-lookup"><span data-stu-id="0194b-127">type</span></span> | <span data-ttu-id="0194b-128">NetworkWatcherAgentWindows</span><span class="sxs-lookup"><span data-stu-id="0194b-128">NetworkWatcherAgentWindows</span></span> |
| <span data-ttu-id="0194b-129">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="0194b-129">typeHandlerVersion</span></span> | <span data-ttu-id="0194b-130">1.4</span><span class="sxs-lookup"><span data-stu-id="0194b-130">1.4</span></span> |


## <a name="template-deployment"></a><span data-ttu-id="0194b-131">Şablon dağıtımı</span><span class="sxs-lookup"><span data-stu-id="0194b-131">Template deployment</span></span>

<span data-ttu-id="0194b-132">Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="0194b-132">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="0194b-133">Önceki bölümde ayrıntılı JSON şeması bir Azure Resource Manager şablonunda bir Azure Resource Manager şablon dağıtımı sırasında Ağ İzleyicisi Aracısı uzantısı çalıştırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0194b-133">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="powershell-deployment"></a><span data-ttu-id="0194b-134">PowerShell dağıtım</span><span class="sxs-lookup"><span data-stu-id="0194b-134">PowerShell deployment</span></span>

<span data-ttu-id="0194b-135">`Set-AzureRmVMExtension` Komutu, Ağ İzleyicisi Aracısı sanal makine uzantısı olan bir sanal makineyi dağıtmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0194b-135">The `Set-AzureRmVMExtension` command can be used to deploy the Network Watcher Agent virtual machine extension to an existing virtual machine.</span></span>

```powershell
Set-AzureRmVMExtension -ResourceGroupName "myResourceGroup1" `
                       -Location "WestUS" `
                       -VMName "myVM1" `
                       -Name "networkWatcherAgent" `
                       -Publisher "Microsoft.Azure.NetworkWatcher" `
                       -Type "NetworkWatcherAgentWindows" `
                       -TypeHandlerVersion "1.4"
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="0194b-136">Sorun giderme ve destek</span><span class="sxs-lookup"><span data-stu-id="0194b-136">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="0194b-137">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="0194b-137">Troubleshooting</span></span>

<span data-ttu-id="0194b-138">Veri uzantısı dağıtımları durumuyla ilgili Azure portalından ve Azure PowerShell modülü kullanılarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="0194b-138">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure PowerShell module.</span></span> <span data-ttu-id="0194b-139">İçin belirli bir VM uzantıları dağıtım durumunu görmek için Azure PowerShell modülünü kullanarak şu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0194b-139">To see the deployment state of extensions for a given VM, run the following command using the Azure PowerShell module.</span></span>

```powershell
Get-AzureRmVMExtension -ResourceGroupName myResourceGroup1 -VMName myVM1 -Name networkWatcherAgent
```

<span data-ttu-id="0194b-140">Uzantı yürütme çıktısı aşağıdaki dizinde bulunan dosyalara kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="0194b-140">Extension execution output is logged to files found in the following directory:</span></span>

```cmd
C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentWindows\
```

### <a name="support"></a><span data-ttu-id="0194b-141">Destek</span><span class="sxs-lookup"><span data-stu-id="0194b-141">Support</span></span>

<span data-ttu-id="0194b-142">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, Ağ İzleyicisi Kullanıcı Kılavuzu belgelere bakın veya üzerinde Azure uzmanlar başvurun [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="0194b-142">If you need more help at any point in this article, you can refer to the Network Watcher User Guide documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="0194b-143">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="0194b-143">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="0194b-144">Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin.</span><span class="sxs-lookup"><span data-stu-id="0194b-144">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="0194b-145">Azure desteği hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="0194b-145">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
