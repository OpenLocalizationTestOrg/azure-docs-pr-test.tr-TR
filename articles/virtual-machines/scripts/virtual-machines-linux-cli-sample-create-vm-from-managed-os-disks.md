---
title: "Azure CLI betik örnek - yönetilen bir disk işletim sistemi diski olarak ekleyerek bir VM oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - yönetilen bir disk işletim sistemi diski olarak ekleyerek bir VM oluşturma"
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
ms.openlocfilehash: 18eefee869b243b35d4426c226eff5f48cd490a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="2527f-103">Mevcut yönetilen işletim sistemi diski ile CLI kullanarak bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="2527f-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="2527f-104">Bu komut dosyasını varolan yönetilen disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2527f-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="2527f-105">Senaryolar önceki içinde bu komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="2527f-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="2527f-106">Yönetilen bir diskten farklı Abonelikteki kopyalanan var olan bir diskten yönetilen işletim sistemi bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2527f-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="2527f-107">Özel bir VHD dosyasından oluşturulmuş var olan bir diskten yönetilen bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2527f-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="2527f-108">Bir anlık görüntüden oluşturulmuş var olan bir diskten yönetilen işletim sistemi bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="2527f-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2527f-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="2527f-109">Sample script</span></span>

<span data-ttu-id="2527f-110">[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "yönetilen bir diskten VM oluşturma")]</span><span class="sxs-lookup"><span data-stu-id="2527f-110">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2527f-111">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="2527f-111">Clean up deployment</span></span> 

<span data-ttu-id="2527f-112">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2527f-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2527f-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="2527f-113">Script explanation</span></span>

<span data-ttu-id="2527f-114">Bu komut, yönetilen disk özelliklerini alma, yönetilen bir diske yeni bir VM'e ve bir VM oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="2527f-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="2527f-115">Komut belirli belgeleri tablo bağlanan her öğe.</span><span class="sxs-lookup"><span data-stu-id="2527f-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2527f-116">Komut</span><span class="sxs-lookup"><span data-stu-id="2527f-116">Command</span></span> | <span data-ttu-id="2527f-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="2527f-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2527f-118">az disk Göster</span><span class="sxs-lookup"><span data-stu-id="2527f-118">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="2527f-119">Disk adı ve kaynak grubu adı kullanarak yönetilen disk özelliklerini alır.</span><span class="sxs-lookup"><span data-stu-id="2527f-119">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="2527f-120">ID özelliği, yönetilen bir diske yeni bir VM'e için kullanılır</span><span class="sxs-lookup"><span data-stu-id="2527f-120">Id property is used to attach a managed disk to a new VM</span></span> |
| [<span data-ttu-id="2527f-121">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="2527f-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="2527f-122">Yönetilen bir işletim sistemi diski kullanarak VM oluşturur</span><span class="sxs-lookup"><span data-stu-id="2527f-122">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="2527f-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2527f-123">Next steps</span></span>

<span data-ttu-id="2527f-124">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2527f-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2527f-125">Ek sanal makine CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2527f-125">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
