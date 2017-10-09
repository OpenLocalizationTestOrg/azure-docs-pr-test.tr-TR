---
title: "aaaAzure CLI komut dosyası örneği - yönetilen bir disk işletim sistemi diski olarak ekleyerek bir VM oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="aa50d-103">Mevcut yönetilen işletim sistemi diski ile CLI kullanarak bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="aa50d-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="aa50d-104">Bu komut dosyasını varolan yönetilen disk işletim sistemi diski olarak ekleyerek bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aa50d-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="aa50d-105">Senaryolar önceki içinde bu komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="aa50d-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="aa50d-106">Yönetilen bir diskten farklı Abonelikteki kopyalanan var olan bir diskten yönetilen işletim sistemi bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa50d-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="aa50d-107">Özel bir VHD dosyasından oluşturulmuş var olan bir diskten yönetilen bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa50d-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="aa50d-108">Bir anlık görüntüden oluşturulmuş var olan bir diskten yönetilen işletim sistemi bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa50d-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="aa50d-109">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="aa50d-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="aa50d-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="aa50d-110">Clean up deployment</span></span> 

<span data-ttu-id="aa50d-111">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="aa50d-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="aa50d-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="aa50d-112">Script explanation</span></span>

<span data-ttu-id="aa50d-113">Bu komut dosyasını aşağıdaki komutları yönetilen tooget disk özelliklere hello kullanıyorsa, yönetilen disk tooa ekleme yeni VM ve VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aa50d-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="aa50d-114">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="aa50d-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="aa50d-115">Komut</span><span class="sxs-lookup"><span data-stu-id="aa50d-115">Command</span></span> | <span data-ttu-id="aa50d-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="aa50d-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="aa50d-117">az disk Göster</span><span class="sxs-lookup"><span data-stu-id="aa50d-117">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="aa50d-118">Disk adı ve kaynak grubu adı kullanarak yönetilen disk özelliklerini alır.</span><span class="sxs-lookup"><span data-stu-id="aa50d-118">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="aa50d-119">ID özelliği olan kullanılan tooattach yönetilen disk tooa yeni VM</span><span class="sxs-lookup"><span data-stu-id="aa50d-119">Id property is used tooattach a managed disk tooa new VM</span></span> |
| [<span data-ttu-id="aa50d-120">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="aa50d-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="aa50d-121">Yönetilen bir işletim sistemi diski kullanarak VM oluşturur</span><span class="sxs-lookup"><span data-stu-id="aa50d-121">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="aa50d-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aa50d-122">Next steps</span></span>

<span data-ttu-id="aa50d-123">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="aa50d-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="aa50d-124">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="aa50d-124">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
