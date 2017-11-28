---
title: "aaaAzure CLI komut dosyası örneği - bir anlık görüntüden bir VM oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - bir anlık görüntüden bir VM oluşturma"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: ddc95289dcb8a0ca7c7854d969983f96b8f4613f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-cli"></a><span data-ttu-id="14e24-103">Anlık görüntü CLI ile bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="14e24-103">Create a virtual machine from a snapshot with CLI</span></span>

<span data-ttu-id="14e24-104">Bu komut dosyasını bir sanal makine işletim sistemi diski bir anlık görüntüden oluşturur.</span><span class="sxs-lookup"><span data-stu-id="14e24-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="14e24-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="14e24-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.sh "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="14e24-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="14e24-106">Clean up deployment</span></span> 

<span data-ttu-id="14e24-107">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="14e24-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="14e24-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="14e24-108">Script explanation</span></span>

<span data-ttu-id="14e24-109">Bu komut dosyası komutları toocreate yönetilen bir disk, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="14e24-109">This script uses hello following commands toocreate a managed disk, virtual machine, and all related resources.</span></span> <span data-ttu-id="14e24-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="14e24-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="14e24-111">Komut</span><span class="sxs-lookup"><span data-stu-id="14e24-111">Command</span></span> | <span data-ttu-id="14e24-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="14e24-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="14e24-113">az anlık görüntü Göster</span><span class="sxs-lookup"><span data-stu-id="14e24-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="14e24-114">Anlık görüntü anlık görüntü adı ve kaynak grubu adı kullanılarak alır.</span><span class="sxs-lookup"><span data-stu-id="14e24-114">Gets snapshot using snapshot name and resource group name.</span></span> <span data-ttu-id="14e24-115">Kullanılan toocreate yönetilen bir disk kimliği nesnesi döndürülen hello özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="14e24-115">Id property of hello returned object is used toocreate a managed disk.</span></span>  |
| [<span data-ttu-id="14e24-116">az disketi oluşturma</span><span class="sxs-lookup"><span data-stu-id="14e24-116">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="14e24-117">Bir anlık görüntüden yönetilen diskleri oluşturur kullanarak snapshot kimliği, disk adı, depolama türünü ve boyutu</span><span class="sxs-lookup"><span data-stu-id="14e24-117">Creates managed disks from a snapshot using snapshot Id, disk name, storage type, and size</span></span>  |
| [<span data-ttu-id="14e24-118">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="14e24-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="14e24-119">Yönetilen bir işletim sistemi diski kullanarak VM oluşturur</span><span class="sxs-lookup"><span data-stu-id="14e24-119">Creates a VM using a managed OS disk</span></span> |

## <a name="next-steps"></a><span data-ttu-id="14e24-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="14e24-120">Next steps</span></span>

<span data-ttu-id="14e24-121">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="14e24-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="14e24-122">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="14e24-122">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
