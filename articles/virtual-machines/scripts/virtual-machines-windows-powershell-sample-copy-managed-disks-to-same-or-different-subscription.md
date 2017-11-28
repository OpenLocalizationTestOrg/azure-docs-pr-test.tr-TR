---
title: "Azure PowerShell Betiği örnek - kopyalama (Taşı) yönetilen aynı veya farklı bir abonelik disklere | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - kopyalama (Taşı) yönetilen aynı veya farklı bir abonelik disklere"
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
ms.openlocfilehash: 75beb35dc19fa530d9b2c19aed6040f74afafbc0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="copy-managed-disks-in-the-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="5c0ad-103">Aynı abonelik ya da farklı bir abonelik PowerShell ile yönetilen diskleri kopyalama</span><span class="sxs-lookup"><span data-stu-id="5c0ad-103">Copy managed disks in the same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="5c0ad-104">Bu komut dosyası, aynı abonelik ya da farklı bir abonelik varolan bir yönetilen diski bir kopyasını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-104">This script creates a copy of an existing managed disk in the same subscription or different subscription.</span></span> <span data-ttu-id="5c0ad-105">Yeni disk üst yönetilen disk ile aynı bölgede oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-105">The new disk is created in the same region as the parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5c0ad-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="5c0ad-106">Sample script</span></span>

<span data-ttu-id="5c0ad-107">[!code-powershell[Ana](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "kopya disk yönetilen")]</span><span class="sxs-lookup"><span data-stu-id="5c0ad-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="5c0ad-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="5c0ad-108">Script explanation</span></span>

<span data-ttu-id="5c0ad-109">Bu komut dosyasını yeni bir yönetilen disk kaynağı yönetilen disk kimliğini kullanarak hedef abonelikte oluşturmak için komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-109">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="5c0ad-110">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5c0ad-111">Komut</span><span class="sxs-lookup"><span data-stu-id="5c0ad-111">Command</span></span> | <span data-ttu-id="5c0ad-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="5c0ad-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5c0ad-113">AzureRmDiskConfig yeni</span><span class="sxs-lookup"><span data-stu-id="5c0ad-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="5c0ad-114">Disk oluşturmak için kullanılan disk yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="5c0ad-115">Kaynak Kimliği üst disk konumu olarak aynı konumu ve üst diski içerir.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-115">It includes the resource Id of the parent disk and location that is same as the location of parent disk.</span></span>  |
| [<span data-ttu-id="5c0ad-116">AzureRmDisk yeni</span><span class="sxs-lookup"><span data-stu-id="5c0ad-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="5c0ad-117">Disk yapılandırması, disk adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5c0ad-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="5c0ad-118">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5c0ad-118">Next steps</span></span>

[<span data-ttu-id="5c0ad-119">Yönetilen bir diskten bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="5c0ad-119">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="5c0ad-120">Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5c0ad-120">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5c0ad-121">Ek sanal makine PowerShell komut dosyası örnekleri bulunabilir [Azure Windows VM belgelerine](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5c0ad-121">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>