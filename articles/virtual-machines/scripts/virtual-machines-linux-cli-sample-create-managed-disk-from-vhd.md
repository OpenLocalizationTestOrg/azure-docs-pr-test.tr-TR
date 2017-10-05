---
title: "Azure CLI betik örnek - yönetilen bir disk bir depolama hesabı aynı abonelikte VHD dosyasında oluşturun | Microsoft Docs"
description: "Azure CLI betik örnek - yönetilen bir disk bir depolama hesabı aynı abonelikte VHD dosyasında oluşturun"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: 448636e87db126defc804a613bb61ff19a086ad9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-the-same-subscription-with-cli"></a><span data-ttu-id="43a72-103">CLI ile aynı abonelikte depolama hesabındaki bir VHD dosyasından yönetilen bir disk oluşturma</span><span class="sxs-lookup"><span data-stu-id="43a72-103">Create a managed disk from a VHD file in a storage account in the same subscription with CLI</span></span>

<span data-ttu-id="43a72-104">Bu komut dosyası yönetilen bir disk bir depolama hesabı aynı abonelikte VHD dosyasında oluşturur.</span><span class="sxs-lookup"><span data-stu-id="43a72-104">This script creates a managed disk from a VHD file in a storage account in the same subscription.</span></span> <span data-ttu-id="43a72-105">Özelleştirilmiş içeri aktarmak için bu betiği kullanın (değil genelleştirilmiş/Sysprep kullanılarak hazırlanmış) bir sanal makine oluşturmak için yönetilen işletim sistemi diski VHD'ye.</span><span class="sxs-lookup"><span data-stu-id="43a72-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="43a72-106">Ya da yönetilen veri diski VHD veri aktarmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="43a72-106">Or, use it to import a data VHD to managed data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="43a72-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="43a72-107">Sample script</span></span>

<span data-ttu-id="43a72-108">[!code-azurecli[Ana](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "VHD'den yönetilen disk oluştur")]</span><span class="sxs-lookup"><span data-stu-id="43a72-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="43a72-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="43a72-109">Script explanation</span></span>

<span data-ttu-id="43a72-110">Bu komut dosyasını bir VHD'den yönetilen bir disk oluşturmak için komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="43a72-110">This script uses following commands to create a managed disk from a VHD.</span></span> <span data-ttu-id="43a72-111">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="43a72-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="43a72-112">Komut</span><span class="sxs-lookup"><span data-stu-id="43a72-112">Command</span></span> | <span data-ttu-id="43a72-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="43a72-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="43a72-114">az disketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="43a72-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="43a72-115">Bir depolama hesabı aynı abonelikte VHD URI kullanılarak yönetilen bir disk oluşturur</span><span class="sxs-lookup"><span data-stu-id="43a72-115">Creates a managed disk using URI of a VHD in a storage account in the same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="43a72-116">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="43a72-116">Next steps</span></span>

[<span data-ttu-id="43a72-117">Yönetilen bir disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="43a72-117">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="43a72-118">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="43a72-118">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="43a72-119">Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="43a72-119">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
