---
title: "PowerShell komut dosyası örneği - yönetilen disk toosame veya farklı bir abonelik kopya (Taşı) anlık aaaAzure | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - yönetilen disk toosame veya farklı bir abonelik kopya (Taşı) anlık"
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
ms.openlocfilehash: d7b8a71cc09d1950271f472e89b95bb551323be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="fb620-103">Aynı abonelik ya da farklı bir abonelik PowerShell ile yönetilen bir disk görüntüsünü Kopyala</span><span class="sxs-lookup"><span data-stu-id="fb620-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="fb620-104">Bu komut dosyasının bir kopyasını bir anlık görüntü hello oluşturur aynı aynı abonelik veya farklı bir abonelik.</span><span class="sxs-lookup"><span data-stu-id="fb620-104">This script creates a copy of a snapshot in hello same same subscription or different subscription.</span></span> <span data-ttu-id="fb620-105">Bu komut dosyası toomove bir anlık görüntü toodifferent abonelik veri saklama için kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb620-105">Use this script toomove a snapshot toodifferent subscription for data retention.</span></span> <span data-ttu-id="fb620-106">Farklı Abonelikteki depolama anlık görüntüler, anlık görüntü ana aboneliğinizde yanlışlıkla silinmeye karşı koruyun.</span><span class="sxs-lookup"><span data-stu-id="fb620-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fb620-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="fb620-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="fb620-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="fb620-108">Script explanation</span></span>

<span data-ttu-id="fb620-109">Bu komut dosyası komutları toocreate aşağıdaki kullanır hello hedef abonelik kullanarak bir anlık görüntü hello hello kaynak anlık görüntü kimliği.</span><span class="sxs-lookup"><span data-stu-id="fb620-109">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="fb620-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="fb620-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fb620-111">Komut</span><span class="sxs-lookup"><span data-stu-id="fb620-111">Command</span></span> | <span data-ttu-id="fb620-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="fb620-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fb620-113">AzureRmSnapshotConfig yeni</span><span class="sxs-lookup"><span data-stu-id="fb620-113">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="fb620-114">Anlık görüntü oluşturmak için kullanılan anlık görüntü yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fb620-114">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="fb620-115">Merhaba kaynak hello üst anlık görüntü ve hello üst anlık görüntü olarak aynı konuma kimliğini içerir.</span><span class="sxs-lookup"><span data-stu-id="fb620-115">It includes hello resource Id of hello parent snapshot and location that is same as hello parent snapshot.</span></span>  |
| [<span data-ttu-id="fb620-116">AzureRmSnapshot yeni</span><span class="sxs-lookup"><span data-stu-id="fb620-116">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="fb620-117">Anlık görüntü yapılandırması, anlık görüntü adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir anlık görüntüsü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fb620-117">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="fb620-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fb620-118">Next steps</span></span>

[<span data-ttu-id="fb620-119">Bir sanal makine bir anlık görüntüden oluşturun</span><span class="sxs-lookup"><span data-stu-id="fb620-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="fb620-120">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fb620-120">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fb620-121">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fb620-121">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
