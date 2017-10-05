---
title: "Linux için Azure Ağ İzleyicisi Aracısı sanal makine uzantısı | Microsoft Docs"
description: "Ağ İzleyicisi Aracısı'nı bir sanal makine uzantısını kullanarak Linux sanal makine dağıtın."
services: virtual-machines-linux
documentationcenter: 
author: dennisg
manager: amku
editor: 
tags: azure-resource-manager
ms.assetid: 5c81e94c-e127-4dd2-ae83-a236c4512345
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/14/2017
ms.author: dennisg
ms.openlocfilehash: eaadd531b9e05a54446e61f98584ae9d75470a5f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="baedc-103">Linux için Ağ İzleyicisi Aracısı sanal makine uzantısı</span><span class="sxs-lookup"><span data-stu-id="baedc-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="baedc-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="baedc-104">Overview</span></span>

<span data-ttu-id="baedc-105">[Azure Ağ İzleyicisi](https://review.docs.microsoft.com/en-us/azure/network-watcher/) Azure ağları için izleme sağlayan bir ağ performans izleme, tanılama ve analiz hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="baedc-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="baedc-106">Ağ İzleyicisi Aracısı sanal makine uzantısı, Azure sanal makinelerde Ağ İzleyicisi özelliklerinden bazıları için bir gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="baedc-106">The Network Watcher Agent virtual machine extension is a requirement for some of the Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="baedc-107">Bu, isteğe bağlı ve diğer gelişmiş işlevler üzerindeki ağ trafiğini yakalama içerir.</span><span class="sxs-lookup"><span data-stu-id="baedc-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="baedc-108">Bu belge desteklenen platformlar ve Linux için Ağ İzleyicisi Aracısı sanal makine uzantısı için dağıtım seçeneklerini ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="baedc-108">This document details the supported platforms and deployment options for the Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="baedc-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="baedc-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="baedc-110">İşletim sistemi</span><span class="sxs-lookup"><span data-stu-id="baedc-110">Operating system</span></span>

<span data-ttu-id="baedc-111">Ağ İzleyicisi Aracısı uzantısı bu Linux dağıtımları karşı çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="baedc-111">The Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="baedc-112">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="baedc-112">Distribution</span></span> | <span data-ttu-id="baedc-113">Sürüm</span><span class="sxs-lookup"><span data-stu-id="baedc-113">Version</span></span> |
|---|---|
| <span data-ttu-id="baedc-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="baedc-114">Ubuntu</span></span> | <span data-ttu-id="baedc-115">16.04 LTS, 14.04 LTS ve 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="baedc-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="baedc-116">Debian</span><span class="sxs-lookup"><span data-stu-id="baedc-116">Debian</span></span> | <span data-ttu-id="baedc-117">7 ve 8</span><span class="sxs-lookup"><span data-stu-id="baedc-117">7 and 8</span></span> |
| <span data-ttu-id="baedc-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="baedc-118">RedHat</span></span> | <span data-ttu-id="baedc-119">6.x ve 7.x</span><span class="sxs-lookup"><span data-stu-id="baedc-119">6.x and 7.x</span></span> |
| <span data-ttu-id="baedc-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="baedc-120">Oracle Linux</span></span> | <span data-ttu-id="baedc-121">7 x</span><span class="sxs-lookup"><span data-stu-id="baedc-121">7x</span></span> |
| <span data-ttu-id="baedc-122">SuSE</span><span class="sxs-lookup"><span data-stu-id="baedc-122">Suse</span></span> | <span data-ttu-id="baedc-123">11 ve 12</span><span class="sxs-lookup"><span data-stu-id="baedc-123">11 and 12</span></span> |
| <span data-ttu-id="baedc-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="baedc-124">OpenSuse</span></span> | <span data-ttu-id="baedc-125">7.0</span><span class="sxs-lookup"><span data-stu-id="baedc-125">7.0</span></span> |
| <span data-ttu-id="baedc-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="baedc-126">CentOS</span></span> | <span data-ttu-id="baedc-127">7.0</span><span class="sxs-lookup"><span data-stu-id="baedc-127">7.0</span></span> |

<span data-ttu-id="baedc-128">CoreOS şu anda desteklenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="baedc-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="baedc-129">İnternet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="baedc-129">Internet connectivity</span></span>

<span data-ttu-id="baedc-130">Bazı Ağ İzleyicisi Aracısı işlevlerini hedef sanal makine Internet'e bağlı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="baedc-130">Some of the Network Watcher Agent functionality requires that the target virtual machine be connected to the Internet.</span></span> <span data-ttu-id="baedc-131">Giden bağlantıları kurmak için özelliği olmadan Ağ İzleyicisi Aracısı özelliklerden bazıları arıza veya kullanılamıyor.</span><span class="sxs-lookup"><span data-stu-id="baedc-131">Without the ability to establish outgoing connections some of the Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="baedc-132">Daha fazla ayrıntı için lütfen bkz. [Ağ İzleyicisi belgeleri](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="baedc-132">For more details, please see the [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="baedc-133">Uzantı Şeması</span><span class="sxs-lookup"><span data-stu-id="baedc-133">Extension schema</span></span>

<span data-ttu-id="baedc-134">Aşağıdaki JSON şeması Ağ İzleyicisi Aracısı uzantısı gösterir.</span><span class="sxs-lookup"><span data-stu-id="baedc-134">The following JSON shows the schema for the Network Watcher Agent extension.</span></span> <span data-ttu-id="baedc-135">Uzantı ne gerektirir ya da şu anda herhangi bir kullanıcı tarafından sağlanan ayarını destekler ve kendi varsayılan yapılandırmasına dayanır.</span><span class="sxs-lookup"><span data-stu-id="baedc-135">The extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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
        "type": "NetworkWatcherAgentLinux",
        "typeHandlerVersion": "1.4",
        "autoUpgradeMinorVersion": true
    }
}
```

### <a name="property-values"></a><span data-ttu-id="baedc-136">Özellik değerleri</span><span class="sxs-lookup"><span data-stu-id="baedc-136">Property values</span></span>

| <span data-ttu-id="baedc-137">Ad</span><span class="sxs-lookup"><span data-stu-id="baedc-137">Name</span></span> | <span data-ttu-id="baedc-138">Değer / örnek</span><span class="sxs-lookup"><span data-stu-id="baedc-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="baedc-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="baedc-139">apiVersion</span></span> | <span data-ttu-id="baedc-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="baedc-140">2015-06-15</span></span> |
| <span data-ttu-id="baedc-141">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="baedc-141">publisher</span></span> | <span data-ttu-id="baedc-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="baedc-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="baedc-143">type</span><span class="sxs-lookup"><span data-stu-id="baedc-143">type</span></span> | <span data-ttu-id="baedc-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="baedc-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="baedc-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="baedc-145">typeHandlerVersion</span></span> | <span data-ttu-id="baedc-146">1.4</span><span class="sxs-lookup"><span data-stu-id="baedc-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="baedc-147">Şablon dağıtımı</span><span class="sxs-lookup"><span data-stu-id="baedc-147">Template deployment</span></span>

<span data-ttu-id="baedc-148">Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="baedc-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="baedc-149">Önceki bölümde ayrıntılı JSON şeması bir Azure Resource Manager şablonunda bir Azure Resource Manager şablon dağıtımı sırasında Ağ İzleyicisi Aracısı uzantısı çalıştırmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="baedc-149">The JSON schema detailed in the previous section can be used in an Azure Resource Manager template to run the Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="baedc-150">Azure CLI dağıtım</span><span class="sxs-lookup"><span data-stu-id="baedc-150">Azure CLI deployment</span></span>

<span data-ttu-id="baedc-151">Azure CLI Ağ İzleyicisi Aracısı VM uzantısı olan bir sanal makineyi dağıtmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="baedc-151">The Azure CLI can be used to deploy the Network Watcher Agent VM extension to an existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="baedc-152">Sorun giderme ve destek</span><span class="sxs-lookup"><span data-stu-id="baedc-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="baedc-153">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="baedc-153">Troubleshooting</span></span>

<span data-ttu-id="baedc-154">Veri uzantısı dağıtımları durumuyla ilgili Azure portalından ve Azure CLI kullanarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="baedc-154">Data about the state of extension deployments can be retrieved from the Azure portal, and by using the Azure CLI.</span></span> <span data-ttu-id="baedc-155">İçin belirli bir VM uzantıları dağıtım durumunu görmek için Azure CLI kullanarak şu komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="baedc-155">To see the deployment state of extensions for a given VM, run the following command using the Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="baedc-156">Uzantı yürütme çıktısı aşağıdaki dizinde bulunan dosyalara kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="baedc-156">Extension execution output is logged to files found in the following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="baedc-157">Destek</span><span class="sxs-lookup"><span data-stu-id="baedc-157">Support</span></span>

<span data-ttu-id="baedc-158">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, Ağ İzleyicisi belgelere bakın veya üzerinde Azure uzmanlar başvurun [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="baedc-158">If you need more help at any point in this article, you can refer to the Network Watcher documentation or contact the Azure experts on the [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="baedc-159">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="baedc-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="baedc-160">Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin.</span><span class="sxs-lookup"><span data-stu-id="baedc-160">Go to the [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="baedc-161">Azure desteği hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="baedc-161">For information about using Azure Support, read the [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
