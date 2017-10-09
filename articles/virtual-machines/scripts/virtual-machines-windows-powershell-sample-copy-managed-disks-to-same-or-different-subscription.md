---
title: "aaaAzure PowerShell komut dosyası örneği - kopyalama (Taşı) yönetilen diskleri toosame veya farklı bir abonelik | Microsoft Docs"
description: "Azure PowerShell Betiği örnek - yönetilen kopyalama (Taşı) diskleri toosame veya farklı bir abonelik"
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
ms.openlocfilehash: 22e19a47228cbf628bebebd73012b8aa7baf073c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="1559a-103">Yönetilen kopyalama diskler hello aynı abonelik veya PowerShell ile farklı bir abonelik</span><span class="sxs-lookup"><span data-stu-id="1559a-103">Copy managed disks in hello same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="1559a-104">Bu komut dosyasını varolan bir yönetilen diski kopyasını hello oluşturur. aynı abonelik veya farklı bir abonelik.</span><span class="sxs-lookup"><span data-stu-id="1559a-104">This script creates a copy of an existing managed disk in hello same subscription or different subscription.</span></span> <span data-ttu-id="1559a-105">Merhaba yeni diski hello aynı oluşturulur hello üst bölgede yönetilen disk.</span><span class="sxs-lookup"><span data-stu-id="1559a-105">hello new disk is created in hello same region as hello parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1559a-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="1559a-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="1559a-107">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="1559a-107">Script explanation</span></span>

<span data-ttu-id="1559a-108">Aşağıdaki komutları toocreate kullanır hello hedef abonelik kullanarak yeni bir yönetilen disk hello hello kaynak kimliğini bu komut dosyası disk yönetilen.</span><span class="sxs-lookup"><span data-stu-id="1559a-108">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="1559a-109">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="1559a-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1559a-110">Komut</span><span class="sxs-lookup"><span data-stu-id="1559a-110">Command</span></span> | <span data-ttu-id="1559a-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="1559a-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1559a-112">AzureRmDiskConfig yeni</span><span class="sxs-lookup"><span data-stu-id="1559a-112">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="1559a-113">Disk oluşturmak için kullanılan disk yapılandırması oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1559a-113">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="1559a-114">Merhaba kaynak kimliği hello üst disk ve üst diski hello konumu olarak aynı konuma içerir.</span><span class="sxs-lookup"><span data-stu-id="1559a-114">It includes hello resource Id of hello parent disk and location that is same as hello location of parent disk.</span></span>  |
| [<span data-ttu-id="1559a-115">AzureRmDisk yeni</span><span class="sxs-lookup"><span data-stu-id="1559a-115">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="1559a-116">Disk yapılandırması, disk adı ve parametre olarak geçirilen kaynak grubu adı kullanarak bir disk oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1559a-116">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="1559a-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1559a-117">Next steps</span></span>

[<span data-ttu-id="1559a-118">Yönetilen bir diskten bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="1559a-118">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="1559a-119">Hello Azure PowerShell modülü hakkında daha fazla bilgi için bkz: [Azure PowerShell belgelerine](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1559a-119">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1559a-120">Ek sanal makine PowerShell komut dosyası örnekleri hello bulunabilir [Azure Windows VM belgelerine](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1559a-120">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
