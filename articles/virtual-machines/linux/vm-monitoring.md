---
title: "Etkinleştirme veya Azure VM izleme devre dışı bırakma"
description: "Etkinleştirmek veya Azure VM izlemeyi devre dışı açıklar"
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
ms.openlocfilehash: 9b2fe579113d6ca6bfd27d82eb9d4657657d44ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a><span data-ttu-id="aaf25-103">Etkinleştirmek veya Azure VM izleme devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="aaf25-103">Enable or Disable Azure VM Monitoring</span></span>

<span data-ttu-id="aaf25-104">Bu bölümde, etkinleştirme veya Azure üzerinde çalışan sanal makinelerde izleme devre dışı açıklar.</span><span class="sxs-lookup"><span data-stu-id="aaf25-104">This section describes how to enable or disable monitoring on Virtual machines running on Azure.</span></span> <span data-ttu-id="aaf25-105">Etkinleştirmek veya Mac, Linux ve Windows (Azure CLI) için portal veya Azure komut satırı arabirimi kullanarak izlemeyi devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="aaf25-105">You can enable or disable monitoring using the portal or Azure Command-line Interface for Mac, Linux, and Windows (the Azure CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aaf25-106">Bu belge Linux tanılama kullanım dışı bırakılmış uzantısının 2.3 sürümünü açıklar.</span><span class="sxs-lookup"><span data-stu-id="aaf25-106">This document describes version 2.3 of the Linux Diagnostic Extension, which has been deprecated.</span></span> <span data-ttu-id="aaf25-107">Sürüm 2.3 30 Haziran 2018 kadar desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="aaf25-107">Version 2.3 will be supported until June 30, 2018.</span></span>
>
> <span data-ttu-id="aaf25-108">Linux tanılama uzantısını 3.0 sürümü yerine etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="aaf25-108">Version 3.0 of the Linux Diagnostic Extension can be enabled instead.</span></span> <span data-ttu-id="aaf25-109">Daha fazla bilgi için bkz: [belgelerine](./diagnostic-extension.md).</span><span class="sxs-lookup"><span data-stu-id="aaf25-109">For more information, see [the documentation](./diagnostic-extension.md).</span></span>

## <a name="enable--disable-monitoring-through-the-azure-portal"></a><span data-ttu-id="aaf25-110">Etkinleştir / Azure portalı üzerinden izleme devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="aaf25-110">Enable / Disable Monitoring through the Azure portal</span></span>

<span data-ttu-id="aaf25-111">1 dakikalık dönemlerini örneğinizi hakkında veriler sağlayan Azure VM'yi, izlemeyi etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aaf25-111">You can enable  monitoring of your Azure VM, which provides data about your instance in 1-minute periods.</span></span> <span data-ttu-id="aaf25-112">(depolama değişiklikler uygulanır).</span><span class="sxs-lookup"><span data-stu-id="aaf25-112">(storage changes apply).</span></span> <span data-ttu-id="aaf25-113">Ayrıntılı tanılama verilerini sonra portal grafiklerde veya API'si aracılığıyla sanal makine için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="aaf25-113">Detailed diagnostics data is then available for the VM in the portal graphs or through the API.</span></span> <span data-ttu-id="aaf25-114">Varsayılan olarak, Azure portal, ölçümleri sınırlı sayıda ana bilgisayar tabanlı izleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="aaf25-114">By default, Azure portal enables host-based monitoring of a limited set of metrics.</span></span> <span data-ttu-id="aaf25-115">Ölçümleri VM çalışırken bir VM içinde veya durdurulmuş durumdaki izlemesini etkinleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aaf25-115">You can enable monitoring of metrics from within a VM while the VM is running or in stopped state.</span></span>

* <span data-ttu-id="aaf25-116">Azure portalında açmak [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aaf25-116">Open the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
* <span data-ttu-id="aaf25-117">Sol gezinti bölmesinde, sanal makineleri'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="aaf25-117">In the left navigation, click Virtual machines.</span></span>
* <span data-ttu-id="aaf25-118">Liste sanal makineleri bir çalışıyor veya durdurulmuştur örneği seçin.</span><span class="sxs-lookup"><span data-stu-id="aaf25-118">In the list Virtual machines, select a running or stopped instance.</span></span> <span data-ttu-id="aaf25-119">"Sanal makine" dikey pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="aaf25-119">The "Virtual machine" blade opens.</span></span>
* <span data-ttu-id="aaf25-120">Tüm ayarlar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="aaf25-120">Click All settings.</span></span>
* <span data-ttu-id="aaf25-121">Tanılama'yı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="aaf25-121">Click Diagnostics.</span></span>
* <span data-ttu-id="aaf25-122">Durum açık veya kapalı değiştirin.</span><span class="sxs-lookup"><span data-stu-id="aaf25-122">Change status to On or Off.</span></span> <span data-ttu-id="aaf25-123">Bu dikey pencerede etkinleştirmek için sanal makine istediğiniz ayrıntıları izleme düzeyini de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aaf25-123">You can also pick in this blade the level of monitoring details you would like to enable for your virtual machine.</span></span>

![Etkinleştir / Azure portalı üzerinden izleme devre dışı bırakın.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a><span data-ttu-id="aaf25-125">Etkinleştir / Azure CLI ile izleme devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="aaf25-125">Enable / Disable Monitoring with Azure CLI</span></span>

<span data-ttu-id="aaf25-126">Bir Azure VM için izlemeyi etkinleştirmek için.</span><span class="sxs-lookup"><span data-stu-id="aaf25-126">To enable monitoring for an Azure VM.</span></span>

* <span data-ttu-id="aaf25-127">(PrivateConfig.json gibi adlandırılmış) dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="aaf25-127">Create a file (named such as PrivateConfig.json):</span></span>

```json
{
        "storageAccountName":"the storage account to receive data",
        "storageAccountKey":"the key of the account"
}
```

* <span data-ttu-id="aaf25-128">Azure CLI aracılığıyla uzantıyı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="aaf25-128">Enable the extension via Azure CLI.</span></span>

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

<span data-ttu-id="aaf25-129">Daha fazla bilgi için bkz: [Linux tanılama uzantısını kullanarak İzleyici Linux sanal makinenin performans ve tanı veri](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aaf25-129">For more information, see [Using Linux Diagnostic Extension to Monitor Linux VM’s performance and diagnostic data](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).</span></span>

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
