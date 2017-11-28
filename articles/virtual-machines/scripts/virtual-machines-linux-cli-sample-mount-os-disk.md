---
title: "aaaAzure CLI komut dosyası örneği - bağlama işletim sistemi diski | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - bağlama işletim sistemi diski"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="5e20f-103">Sanal makineleri işletim sistemi disk sorunlarını gider</span><span class="sxs-lookup"><span data-stu-id="5e20f-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="5e20f-104">Bu komut dosyası hello işletim sistemi diski başarısız veya sorunlu bir sanal makinenin veri diski tooa ikinci sanal makine olarak bağlar.</span><span class="sxs-lookup"><span data-stu-id="5e20f-104">This script mounts hello operating system disk of a failed or problematic virtual machine as a data disk tooa second virtual machine.</span></span> <span data-ttu-id="5e20f-105">Sorun giderme disk sorunları ya da veri kurtarma bu kullanışlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="5e20f-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5e20f-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="5e20f-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a><span data-ttu-id="5e20f-107">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="5e20f-107">Script explanation</span></span>

<span data-ttu-id="5e20f-108">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="5e20f-108">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="5e20f-109">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="5e20f-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5e20f-110">Komut</span><span class="sxs-lookup"><span data-stu-id="5e20f-110">Command</span></span> | <span data-ttu-id="5e20f-111">Notlar</span><span class="sxs-lookup"><span data-stu-id="5e20f-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5e20f-112">az vm Göster</span><span class="sxs-lookup"><span data-stu-id="5e20f-112">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="5e20f-113">Sanal makinelerin listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="5e20f-113">Return a list of virtual machines.</span></span> <span data-ttu-id="5e20f-114">Bu durumda, hello sorgu kullanılan tooreturn hello sanal makine işletim sistemi diski seçenektir.</span><span class="sxs-lookup"><span data-stu-id="5e20f-114">In this case, hello query option is used tooreturn hello virtual machine operating system disk.</span></span> <span data-ttu-id="5e20f-115">Bu değer daha sonra tooa değişken adı 'uri' eklenir.</span><span class="sxs-lookup"><span data-stu-id="5e20f-115">This value is then added tooa variable name ‘uri’.</span></span> |
| [<span data-ttu-id="5e20f-116">az vm silme</span><span class="sxs-lookup"><span data-stu-id="5e20f-116">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="5e20f-117">Bir sanal makineyi siler.</span><span class="sxs-lookup"><span data-stu-id="5e20f-117">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="5e20f-118">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="5e20f-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="5e20f-119">Bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5e20f-119">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="5e20f-120">az vm diski kullanıma açın</span><span class="sxs-lookup"><span data-stu-id="5e20f-120">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="5e20f-121">Bir disk tooa sanal makineye iliştirir.</span><span class="sxs-lookup"><span data-stu-id="5e20f-121">Attaches a disk tooa virtual machine.</span></span> |
| [<span data-ttu-id="5e20f-122">az vm-IP-adresleri listesi</span><span class="sxs-lookup"><span data-stu-id="5e20f-122">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="5e20f-123">Bir sanal makine IP adreslerini döndürür hello.</span><span class="sxs-lookup"><span data-stu-id="5e20f-123">Returns hello IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5e20f-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5e20f-124">Next steps</span></span>

<span data-ttu-id="5e20f-125">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5e20f-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5e20f-126">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e20f-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
