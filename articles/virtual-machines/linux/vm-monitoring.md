---
title: "aaaEnable veya Azure VM izleme devre dışı bırakma"
description: "Açıklar nasıl tooEnable veya Azure VM izlemeyi devre dışı bırak"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="97eef-103">Etkinleştirmek veya Azure VM izleme devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="97eef-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="97eef-104">Bu bölümde, nasıl Azure üzerinde çalışan tooenable veya izleme devre dışı üzerinde sanal makineleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="97eef-104">This section describes how tooenable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="97eef-105">Etkinleştirmek veya Mac, Linux ve Windows (hello Azure CLI) için hello portalı veya Azure komut satırı arabirimi kullanarak izlemeyi devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="97eef-105">You can enable or disable monitoring using hello portal or Azure Command-line Interface for Mac, Linux, and Windows (hello Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97eef-106">Bu belgede hello Linux tanılama kullanım dışı bırakılmış uzantısının 2.3 sürümü açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="97eef-106">This document describes version 2.3 of hello Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="97eef-107">Sürüm 2.3 30 Haziran 2018 kadar desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="97eef-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="97eef-108">Merhaba Linux tanılama uzantısını 3.0 sürümü yerine etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="97eef-108">Version 3.0 of hello Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="97eef-109">Daha fazla bilgi için bkz: [hello belgelerine](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="97eef-109">For more information, see [hello documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a><span data-ttu-id="97eef-110">Etkinleştir / Azure portal hello izlemeyi devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="97eef-110">Enable / Disable Monitoring through hello Azure portal</span></span>

<span data-ttu-id="97eef-111">1 dakikalık dönemlerini örneğinizi hakkında veriler sağlayan Azure VM'yi, izlemeyi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97eef-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="97eef-112">(depolama değişiklikler uygulanır).</span><span class="sxs-lookup"><span data-stu-id="97eef-112">(storage changes apply).</span></span> <span data-ttu-id="97eef-113">Ayrıntılı tanılama verilerini, ardından hello VM hello portal grafiklerde veya hello API aracılığıyla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="97eef-113">Detailed diagnostics data is then available for hello VM in hello portal graphs or through hello API.</span></span> <span data-ttu-id="97eef-114">Varsayılan olarak, Azure portal, ölçümleri sınırlı sayıda ana bilgisayar tabanlı izleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="97eef-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="97eef-115">VM çalıştıran hello veya durdurulmuş durumdaki bir VM içinde ölçümleri izleme etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97eef-115">You can enable monitoring of metrics from within a VM while hello VM is running or in stopped state.</span></span>

* <span data-ttu-id="97eef-116">Açık hello Azure portal adresindeki [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="97eef-116">Open hello Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="97eef-117">Sol gezinti hello, sanal makineleri'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="97eef-117">In hello left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="97eef-118">Hello listesi sanal makinelerde çalışan veya durdurulmuş bir örnek seçin.</span><span class="sxs-lookup"><span data-stu-id="97eef-118">In hello list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="97eef-119">Merhaba "Sanal makine" dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="97eef-119">hello "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="97eef-120">Tüm ayarlar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="97eef-120">Click All settings.</span></span>
* <span data-ttu-id="97eef-121">Tanılama'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="97eef-121">Click Diagnostics.</span></span>
* <span data-ttu-id="97eef-122">Değişiklik durumu tooOn veya kapalı.</span><span class="sxs-lookup"><span data-stu-id="97eef-122">Change status tooOn or Off.</span></span> <span data-ttu-id="97eef-123">Ayrıntılar için sanal makine tooenable ister misiniz izleme bu dikey penceresinde hello düzeyindeki seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97eef-123">You can also pick in this blade hello level of monitoring details you would like tooenable for your virtual machine.</span></span>

![Etkinleştir / hello Azure portal izleme devre dışı bırakın.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="97eef-125">Etkinleştir / Azure CLI ile izleme devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="97eef-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="97eef-126">tooenable bir Azure VM için izleme.</span><span class="sxs-lookup"><span data-stu-id="97eef-126">tooenable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="97eef-127">(PrivateConfig.json gibi adlandırılmış) dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="97eef-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* <span data-ttu-id="97eef-128">Azure CLI aracılığıyla Hello uzantıyı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="97eef-128">Enable hello extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="97eef-129">Daha fazla bilgi için bkz: [Linux tanılama uzantısını kullanarak tooMonitor Linux sanal makinenin performans ve tanılama verilerini](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="97eef-129">For more information, see [Using Linux Diagnostic Extension tooMonitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
