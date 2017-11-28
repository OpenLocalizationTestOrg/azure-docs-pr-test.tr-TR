---
title: "aaaAzure CLI komut dosyası örneği - hello depolama hesabında bir VHD dosyasından yönetilen bir disk oluşturmak aynı abonelik | Microsoft Docs"
description: "Azure CLI betik örnek - hello depolama hesabında bir VHD dosyasından yönetilen bir disk oluşturma aynı abonelik"
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
ms.openlocfilehash: 6cfb3c54a7692b0f3999c585861340c1a6b4d348
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a><span data-ttu-id="4e187-103">Bir VHD dosyasının hello depolama hesabında yönetilen bir disk oluşturmak CLI ile aynı abonelik</span><span class="sxs-lookup"><span data-stu-id="4e187-103">Create a managed disk from a VHD file in a storage account in hello same subscription with CLI</span></span>

<span data-ttu-id="4e187-104">Bu komut dosyasını bir VHD dosyasının hello depolama hesabında yönetilen bir disk oluşturur aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="4e187-104">This script creates a managed disk from a VHD file in a storage account in hello same subscription.</span></span> <span data-ttu-id="4e187-105">Bu komut dosyası tooimport bir özel (değil genelleştirilmiş/Sysprep kullanılarak hazırlanmış) VHD toomanaged işletim sistemi disk toocreate bir sanal makine kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e187-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="4e187-106">Veya tooimport veri VHD toomanaged veri diski kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e187-106">Or, use it tooimport a data VHD toomanaged data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4e187-107">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="4e187-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="4e187-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="4e187-108">Script explanation</span></span>

<span data-ttu-id="4e187-109">Bu komut dosyasını komutları toocreate VHD yönetilen bir diskten kullanır.</span><span class="sxs-lookup"><span data-stu-id="4e187-109">This script uses following commands toocreate a managed disk from a VHD.</span></span> <span data-ttu-id="4e187-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="4e187-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4e187-111">Komut</span><span class="sxs-lookup"><span data-stu-id="4e187-111">Command</span></span> | <span data-ttu-id="4e187-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="4e187-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4e187-113">az disketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e187-113">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="4e187-114">Merhaba depolama hesabında VHD URI kullanılarak yönetilen bir disk oluşturur aynı abonelik</span><span class="sxs-lookup"><span data-stu-id="4e187-114">Creates a managed disk using URI of a VHD in a storage account in hello same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4e187-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4e187-115">Next steps</span></span>

[<span data-ttu-id="4e187-116">Yönetilen bir disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="4e187-116">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="4e187-117">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4e187-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4e187-118">Ek bir sanal makine ve yönetilen diskleri CLI kod örnekleri hello bulunan [Azure Linux VM'de belgelerine](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4e187-118">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
