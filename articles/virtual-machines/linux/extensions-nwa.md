---
title: "Linux için Ağ İzleyicisi Aracısı sanal makine uzantısı aaaAzure | Microsoft Docs"
description: "Bir sanal makine uzantısını kullanarak Linux sanal makine üzerinde Ağ İzleyicisi Aracısı Hello dağıtın."
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
ms.openlocfilehash: 84bed132cbda83d0917be490f9a50914578952a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="network-watcher-agent-virtual-machine-extension-for-linux"></a><span data-ttu-id="cc651-103">Linux için Ağ İzleyicisi Aracısı sanal makine uzantısı</span><span class="sxs-lookup"><span data-stu-id="cc651-103">Network Watcher Agent virtual machine extension for Linux</span></span>

## <a name="overview"></a><span data-ttu-id="cc651-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cc651-104">Overview</span></span>

<span data-ttu-id="cc651-105">[Azure Ağ İzleyicisi](https://review.docs.microsoft.com/en-us/azure/network-watcher/) Azure ağları için izleme sağlayan bir ağ performans izleme, tanılama ve analiz hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="cc651-105">[Azure Network Watcher](https://review.docs.microsoft.com/en-us/azure/network-watcher/) is a network performance monitoring, diagnostic, and analytics service that allows monitoring for Azure networks.</span></span> <span data-ttu-id="cc651-106">Ağ İzleyicisi Aracısı sanal makine uzantısı Hello Azure sanal makinelerde hello Ağ İzleyicisi özelliklerinden bazıları için gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="cc651-106">hello Network Watcher Agent virtual machine extension is a requirement for some of hello Network Watcher features on Azure virtual machines.</span></span> <span data-ttu-id="cc651-107">Bu, isteğe bağlı ve diğer gelişmiş işlevler üzerindeki ağ trafiğini yakalama içerir.</span><span class="sxs-lookup"><span data-stu-id="cc651-107">This includes capturing network traffic on demand and other advanced functionality.</span></span>

<span data-ttu-id="cc651-108">Bu belge ayrıntıları hello platformları ve dağıtım seçenekleri Linux için Ağ İzleyicisi Aracısı sanal makine uzantısı hello için desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="cc651-108">This document details hello supported platforms and deployment options for hello Network Watcher Agent virtual machine extension for Linux.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc651-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cc651-109">Prerequisites</span></span>

### <a name="operating-system"></a><span data-ttu-id="cc651-110">İşletim sistemi</span><span class="sxs-lookup"><span data-stu-id="cc651-110">Operating system</span></span>

<span data-ttu-id="cc651-111">Ağ İzleyicisi Aracısı uzantısı Hello bu Linux dağıtımları karşı çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cc651-111">hello Network Watcher Agent extension can be run against these Linux distributions:</span></span>

| <span data-ttu-id="cc651-112">Dağıtım</span><span class="sxs-lookup"><span data-stu-id="cc651-112">Distribution</span></span> | <span data-ttu-id="cc651-113">Sürüm</span><span class="sxs-lookup"><span data-stu-id="cc651-113">Version</span></span> |
|---|---|
| <span data-ttu-id="cc651-114">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="cc651-114">Ubuntu</span></span> | <span data-ttu-id="cc651-115">16.04 LTS, 14.04 LTS ve 12.04 LTS</span><span class="sxs-lookup"><span data-stu-id="cc651-115">16.04 LTS, 14.04 LTS and 12.04 LTS</span></span> |
| <span data-ttu-id="cc651-116">Debian</span><span class="sxs-lookup"><span data-stu-id="cc651-116">Debian</span></span> | <span data-ttu-id="cc651-117">7 ve 8</span><span class="sxs-lookup"><span data-stu-id="cc651-117">7 and 8</span></span> |
| <span data-ttu-id="cc651-118">RedHat</span><span class="sxs-lookup"><span data-stu-id="cc651-118">RedHat</span></span> | <span data-ttu-id="cc651-119">6.x ve 7.x</span><span class="sxs-lookup"><span data-stu-id="cc651-119">6.x and 7.x</span></span> |
| <span data-ttu-id="cc651-120">Oracle Linux</span><span class="sxs-lookup"><span data-stu-id="cc651-120">Oracle Linux</span></span> | <span data-ttu-id="cc651-121">7 x</span><span class="sxs-lookup"><span data-stu-id="cc651-121">7x</span></span> |
| <span data-ttu-id="cc651-122">SuSE</span><span class="sxs-lookup"><span data-stu-id="cc651-122">Suse</span></span> | <span data-ttu-id="cc651-123">11 ve 12</span><span class="sxs-lookup"><span data-stu-id="cc651-123">11 and 12</span></span> |
| <span data-ttu-id="cc651-124">OpenSuse</span><span class="sxs-lookup"><span data-stu-id="cc651-124">OpenSuse</span></span> | <span data-ttu-id="cc651-125">7.0</span><span class="sxs-lookup"><span data-stu-id="cc651-125">7.0</span></span> |
| <span data-ttu-id="cc651-126">CentOS</span><span class="sxs-lookup"><span data-stu-id="cc651-126">CentOS</span></span> | <span data-ttu-id="cc651-127">7.0</span><span class="sxs-lookup"><span data-stu-id="cc651-127">7.0</span></span> |

<span data-ttu-id="cc651-128">CoreOS şu anda desteklenmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cc651-128">Note that CoreOS is not supported at this time.</span></span>

### <a name="internet-connectivity"></a><span data-ttu-id="cc651-129">İnternet bağlantısı</span><span class="sxs-lookup"><span data-stu-id="cc651-129">Internet connectivity</span></span>

<span data-ttu-id="cc651-130">Merhaba Ağ İzleyicisi Aracısı işlevleri bazıları hello hedef sanal makinenin bağlı toohello Internet olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cc651-130">Some of hello Network Watcher Agent functionality requires that hello target virtual machine be connected toohello Internet.</span></span> <span data-ttu-id="cc651-131">Merhaba özelliği tooestablish giden bağlantılar hello Ağ İzleyicisi Aracısı özelliklerden bazıları düzgün çalışmamasına veya kullanılamaz hale.</span><span class="sxs-lookup"><span data-stu-id="cc651-131">Without hello ability tooestablish outgoing connections some of hello Network Watcher Agent features may malfunction or become unavailable.</span></span> <span data-ttu-id="cc651-132">Daha fazla ayrıntı için lütfen bkz hello [Ağ İzleyicisi belgeleri](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span><span class="sxs-lookup"><span data-stu-id="cc651-132">For more details, please see hello [Network Watcher documentation](https://review.docs.microsoft.com/en-us/azure/network-watcher/).</span></span>

## <a name="extension-schema"></a><span data-ttu-id="cc651-133">Uzantı Şeması</span><span class="sxs-lookup"><span data-stu-id="cc651-133">Extension schema</span></span>

<span data-ttu-id="cc651-134">Merhaba aşağıdaki JSON hello Ağ İzleyicisi Aracısı uzantısı için hello şema gösterir.</span><span class="sxs-lookup"><span data-stu-id="cc651-134">hello following JSON shows hello schema for hello Network Watcher Agent extension.</span></span> <span data-ttu-id="cc651-135">Merhaba uzantısı ne gerektirir ya da şu anda herhangi bir kullanıcı tarafından sağlanan ayarını destekler ve kendi varsayılan yapılandırmasına dayanır.</span><span class="sxs-lookup"><span data-stu-id="cc651-135">hello extension neither requires nor supports any user-supplied settings at this time and relies on its default configuration.</span></span>

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

### <a name="property-values"></a><span data-ttu-id="cc651-136">Özellik değerleri</span><span class="sxs-lookup"><span data-stu-id="cc651-136">Property values</span></span>

| <span data-ttu-id="cc651-137">Ad</span><span class="sxs-lookup"><span data-stu-id="cc651-137">Name</span></span> | <span data-ttu-id="cc651-138">Değer / örnek</span><span class="sxs-lookup"><span data-stu-id="cc651-138">Value / Example</span></span> |
| ---- | ---- |
| <span data-ttu-id="cc651-139">apiVersion</span><span class="sxs-lookup"><span data-stu-id="cc651-139">apiVersion</span></span> | <span data-ttu-id="cc651-140">2015-06-15</span><span class="sxs-lookup"><span data-stu-id="cc651-140">2015-06-15</span></span> |
| <span data-ttu-id="cc651-141">Yayımcı</span><span class="sxs-lookup"><span data-stu-id="cc651-141">publisher</span></span> | <span data-ttu-id="cc651-142">Microsoft.Azure.NetworkWatcher</span><span class="sxs-lookup"><span data-stu-id="cc651-142">Microsoft.Azure.NetworkWatcher</span></span> |
| <span data-ttu-id="cc651-143">type</span><span class="sxs-lookup"><span data-stu-id="cc651-143">type</span></span> | <span data-ttu-id="cc651-144">NetworkWatcherAgentLinux</span><span class="sxs-lookup"><span data-stu-id="cc651-144">NetworkWatcherAgentLinux</span></span> |
| <span data-ttu-id="cc651-145">typeHandlerVersion</span><span class="sxs-lookup"><span data-stu-id="cc651-145">typeHandlerVersion</span></span> | <span data-ttu-id="cc651-146">1.4</span><span class="sxs-lookup"><span data-stu-id="cc651-146">1.4</span></span> |

## <a name="template-deployment"></a><span data-ttu-id="cc651-147">Şablon dağıtımı</span><span class="sxs-lookup"><span data-stu-id="cc651-147">Template deployment</span></span>

<span data-ttu-id="cc651-148">Azure VM uzantıları, Azure Resource Manager şablonları ile dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="cc651-148">Azure VM extensions can be deployed with Azure Resource Manager templates.</span></span> <span data-ttu-id="cc651-149">Merhaba JSON şeması Hello önceki bölümde ayrıntılı bir Azure Resource Manager şablon dağıtımı sırasında bir Azure Resource Manager şablonu toorun hello Ağ İzleyicisi Aracısı uzantısı kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cc651-149">hello JSON schema detailed in hello previous section can be used in an Azure Resource Manager template toorun hello Network Watcher Agent extension during an Azure Resource Manager template deployment.</span></span>

## <a name="azure-cli-deployment"></a><span data-ttu-id="cc651-150">Azure CLI dağıtım</span><span class="sxs-lookup"><span data-stu-id="cc651-150">Azure CLI deployment</span></span>

<span data-ttu-id="cc651-151">Hello Azure CLI kullanılan toodeploy hello Ağ İzleyicisi Aracısı VM uzantısı tooan varolan sanal makine olabilir.</span><span class="sxs-lookup"><span data-stu-id="cc651-151">hello Azure CLI can be used toodeploy hello Network Watcher Agent VM extension tooan existing virtual machine.</span></span>

```azurecli
azure vm extension set myResourceGroup1 myVM1 NetworkWatcherAgentLinux Microsoft.Azure.NetworkWatcher 1.4
```

## <a name="troubleshooting-and-support"></a><span data-ttu-id="cc651-152">Sorun giderme ve destek</span><span class="sxs-lookup"><span data-stu-id="cc651-152">Troubleshooting and support</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="cc651-153">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="cc651-153">Troubleshooting</span></span>

<span data-ttu-id="cc651-154">Veri uzantısı dağıtımları hello durumuyla ilgili hello Azure portal ve hello Azure CLI kullanarak alınabilir.</span><span class="sxs-lookup"><span data-stu-id="cc651-154">Data about hello state of extension deployments can be retrieved from hello Azure portal, and by using hello Azure CLI.</span></span> <span data-ttu-id="cc651-155">toosee hello dağıtım durumu uzantılarının komutunu kullanarak aşağıdaki hello çalıştırmak, belirli bir VM için Azure CLI hello.</span><span class="sxs-lookup"><span data-stu-id="cc651-155">toosee hello deployment state of extensions for a given VM, run hello following command using hello Azure CLI.</span></span>

```azurecli
azure vm extension get myResourceGroup1 myVM1
```

<span data-ttu-id="cc651-156">Uzantı yürütme hello bulunan oturum toofiles directory aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="cc651-156">Extension execution output is logged toofiles found in hello following directory:</span></span>

`
/var/log/azure/Microsoft.Azure.NetworkWatcher.NetworkWatcherAgentLinux/
`

### <a name="support"></a><span data-ttu-id="cc651-157">Destek</span><span class="sxs-lookup"><span data-stu-id="cc651-157">Support</span></span>

<span data-ttu-id="cc651-158">Bu makalede herhangi bir noktada daha fazla yardıma gereksinim duyarsanız, toohello Ağ İzleyicisi belgelere bakın veya hello Azure başvurun hello uzmanlarıyla [MSDN Azure ve yığın taşması forumları](https://azure.microsoft.com/en-us/support/forums/).</span><span class="sxs-lookup"><span data-stu-id="cc651-158">If you need more help at any point in this article, you can refer toohello Network Watcher documentation or contact hello Azure experts on hello [MSDN Azure and Stack Overflow forums](https://azure.microsoft.com/en-us/support/forums/).</span></span> <span data-ttu-id="cc651-159">Alternatif olarak, Azure destek olay dosya.</span><span class="sxs-lookup"><span data-stu-id="cc651-159">Alternatively, you can file an Azure support incident.</span></span> <span data-ttu-id="cc651-160">Toohello Git [Azure Destek sitesi](https://azure.microsoft.com/en-us/support/options/) ve Get destek seçin.</span><span class="sxs-lookup"><span data-stu-id="cc651-160">Go toohello [Azure support site](https://azure.microsoft.com/en-us/support/options/) and select Get support.</span></span> <span data-ttu-id="cc651-161">Hello Azure destek kullanma hakkında daha fazla bilgi için okuma [Microsoft Azure desteği ile ilgili SSS](https://azure.microsoft.com/en-us/support/faq/).</span><span class="sxs-lookup"><span data-stu-id="cc651-161">For information about using Azure Support, read hello [Microsoft Azure support FAQ](https://azure.microsoft.com/en-us/support/faq/).</span></span>
