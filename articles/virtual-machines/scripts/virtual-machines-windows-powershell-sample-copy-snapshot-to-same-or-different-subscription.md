---
title: "Azure PowerShell Betiği örnek - aynı veya farklı bir abonelik yönetilen bir diske kopyalama (Taşı) görüntüsünü | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - aynı veya farklı bir abonelik yönetilen bir diske görüntüsünü kopyala (taşıma)"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: f7b4869669a2c5e840f9bd384dcd6d6096ba58e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="0f0bf-103">Aynı abonelik ya da farklı bir abonelik PowerShell ile yönetilen bir disk görüntüsünü Kopyala</span><span class="sxs-lookup"><span data-stu-id="0f0bf-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="0f0bf-104">Bu komut dosyasının bir kopyasını bir anlık görüntü aynı aynı abonelik ya da farklı bir abonelik oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f0bf-104">This script creates a copy of a snapshot in the same same subscription or different subscription.</span></span> <span data-ttu-id="0f0bf-105">Veri saklama için farklı bir abonelik için bir anlık görüntü taşımak için bu komut dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f0bf-105">Use this script to move a snapshot to different subscription for data retention.</span></span> <span data-ttu-id="0f0bf-106">Farklı Abonelikteki depolama anlık görüntüler, anlık görüntü ana aboneliğinizde yanlışlıkla silinmeye karşı koruyun.</span><span class="sxs-lookup"><span data-stu-id="0f0bf-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0f0bf-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="0f0bf-107">Sample script</span></span>

<span data-ttu-id="0f0bf-108">[!code-powershell[Ana](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "kopyalama anlık görüntü")]</span><span class="sxs-lookup"><span data-stu-id="0f0bf-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="0f0bf-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="0f0bf-109">Script explanation</span></span>

<span data-ttu-id="0f0bf-110">Bu komut dosyası kaynağı anlık görüntü kimliğini kullanarak hedef abonelikte bir anlık görüntü oluşturmak için komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="0f0bf-110">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="0f0bf-111">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="0f0bf-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0f0bf-112">Komut</span><span class="sxs-lookup"><span data-stu-id="0f0bf-112">Command</span></span> | <span data-ttu-id="0f0bf-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="0f0bf-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0f0bf-114">AzureRmSnapshotConfig yeni</span><span class="sxs-lookup"><span data-stu-id="0f0bf-114">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="0f0bf-115">Anlık görüntü oluşturmak için kullanılan anlık görüntü yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f0bf-115">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="0f0bf-116">Kaynak Kimliği üst anlık görüntü ve üst anlık görüntü olarak aynı konumu içerir.</span><span class="sxs-lookup"><span data-stu-id="0f0bf-116">It includes the resource Id of the parent snapshot and location that is same as the parent snapshot.</span></span>  |
| [<span data-ttu-id="0f0bf-117">AzureRmSnapshot yeni</span><span class="sxs-lookup"><span data-stu-id="0f0bf-117">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="0f0bf-118">Anlık görüntü yapılandırması, anlık görüntü adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir anlık görüntüsü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f0bf-118">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="0f0bf-119">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0f0bf-119">Next steps</span></span>

[<span data-ttu-id="0f0bf-120">Bir sanal makine bir anlık görüntüden oluşturun</span><span class="sxs-lookup"><span data-stu-id="0f0bf-120">Create a virtual machine from a snapshot</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="0f0bf-121">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0f0bf-121">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0f0bf-122">Ek sanal makine PowerShell komut dosyası örnekleri bulunabilir [Azure Windows VM belgelerine](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f0bf-122">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>