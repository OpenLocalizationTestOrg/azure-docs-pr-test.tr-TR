---
title: "aaaAzure CLI komut dosyası örneği - VHD ile bir VM oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - bir sanal sabit disk kullanan bir VM oluşturma."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/09/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: ce39092697a51e4e8a8e59ba8eb919955f616458
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-virtual-hard-disk"></a><span data-ttu-id="1544a-103">Bir sanal sabit disk ile bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="1544a-103">Create a VM with a virtual hard disk</span></span>

<span data-ttu-id="1544a-104">Bu örnek, bir VHD'yi kullanarak bir sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1544a-104">This example creates a virtual machine using a VHD.</span></span>
<span data-ttu-id="1544a-105">Bir kaynak grubu, bir depolama hesabı ve kapsayıcı oluşturur, ardından hello VHD toohello kapsayıcı karşıya yükleyerek bir VM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1544a-105">It creates a resource group, a storage account, and a container, then it creates a VM by uploading hello VHD toohello container.</span></span>
<span data-ttu-id="1544a-106">Merhaba ssh ortak yerini böylece erişim toohello VM sahip anahtar ortak anahtarınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1544a-106">It replaces hello ssh public key with your public key so that you have access toohello VM.</span></span>

<span data-ttu-id="1544a-107">Önyüklenebilir bir VHD gerekir.</span><span class="sxs-lookup"><span data-stu-id="1544a-107">You'll need a bootable VHD.</span></span>
<span data-ttu-id="1544a-108">Https://azclisamples.blob.core.windows.net/vhds/sample.vhd hello kullandık VHD indirin veya kendi VHD kullanın.</span><span class="sxs-lookup"><span data-stu-id="1544a-108">You can download hello VHD that we used from https://azclisamples.blob.core.windows.net/vhds/sample.vhd, or use your own VHD.</span></span> <span data-ttu-id="1544a-109">Merhaba komut dosyası arar `~/sample.vhd`.</span><span class="sxs-lookup"><span data-stu-id="1544a-109">hello script looks for `~/sample.vhd`.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1544a-110">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="1544a-110">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-vhd/create-vm-vhd.sh "Create VM using a VHD")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1544a-111">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="1544a-111">Clean up deployment</span></span> 

<span data-ttu-id="1544a-112">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="1544a-112">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n az-cli-vhd
```

## <a name="script-explanation"></a><span data-ttu-id="1544a-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="1544a-113">Script explanation</span></span>

<span data-ttu-id="1544a-114">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine, kullanılabilirlik kümesi, yük dengeleyici ve tüm ilgili kaynaklar aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="1544a-114">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="1544a-115">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="1544a-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1544a-116">Komut</span><span class="sxs-lookup"><span data-stu-id="1544a-116">Command</span></span> | <span data-ttu-id="1544a-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="1544a-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1544a-118">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="1544a-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="1544a-119">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1544a-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1544a-120">az depolama hesabı listesi</span><span class="sxs-lookup"><span data-stu-id="1544a-120">az storage account list</span></span>](https://docs.microsoft.com/cli/azure/storage/account#list) | <span data-ttu-id="1544a-121">Listeleri depolama hesapları</span><span class="sxs-lookup"><span data-stu-id="1544a-121">Lists storage accounts</span></span> |
| [<span data-ttu-id="1544a-122">az depolama hesabı onay-adı</span><span class="sxs-lookup"><span data-stu-id="1544a-122">az storage account check-name</span></span>](https://docs.microsoft.com/cli/azure/storage/account#check-name) | <span data-ttu-id="1544a-123">Depolama hesabı adı geçerli olduğunu ve önceden var olmayan denetler</span><span class="sxs-lookup"><span data-stu-id="1544a-123">Checks that a storage account name is valid and that it doesn't already exist</span></span> |
| [<span data-ttu-id="1544a-124">az depolama hesabı anahtarları listesi</span><span class="sxs-lookup"><span data-stu-id="1544a-124">az storage account keys list</span></span>](https://docs.microsoft.com/cli/azure/storage/account/keys#list) | <span data-ttu-id="1544a-125">Merhaba depolama hesapları için anahtarları listeler</span><span class="sxs-lookup"><span data-stu-id="1544a-125">Lists keys for hello storage accounts</span></span> |
| [<span data-ttu-id="1544a-126">az depolama blob var.</span><span class="sxs-lookup"><span data-stu-id="1544a-126">az storage blob exists</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#exists) | <span data-ttu-id="1544a-127">Merhaba blob mevcut olup olmadığını denetler</span><span class="sxs-lookup"><span data-stu-id="1544a-127">Checks whether hello blob exists</span></span> |
| [<span data-ttu-id="1544a-128">az depolama kapsayıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1544a-128">az storage container create</span></span>](https://docs.microsoft.com/cli/azure/storage/container#create) | <span data-ttu-id="1544a-129">Bir depolama hesabında bir kapsayıcı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1544a-129">Creates a container in a storage account.</span></span> |
| [<span data-ttu-id="1544a-130">az depolama blob karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="1544a-130">az storage blob upload</span></span>](https://docs.microsoft.com/cli/azure/storage/blob#upload) | <span data-ttu-id="1544a-131">Bir blob karşıya yükleme hello VHD tarafından hello kapsayıcıda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1544a-131">Creates a blob in hello container by uploading hello VHD.</span></span> |
| [<span data-ttu-id="1544a-132">az vm listesi</span><span class="sxs-lookup"><span data-stu-id="1544a-132">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="1544a-133">İle kullanılan `--query` hello VM adı kullanımda olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="1544a-133">Used with `--query` check whether hello VM name is in use.</span></span> | 
| [<span data-ttu-id="1544a-134">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="1544a-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="1544a-135">Merhaba sanal makineler oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1544a-135">Creates hello virtual machines.</span></span> |
| [<span data-ttu-id="1544a-136">az vm kümesi linux kullanıcıya erişim</span><span class="sxs-lookup"><span data-stu-id="1544a-136">az vm access set-linux-user</span></span>](https://docs.microsoft.com/cli/azure/vm/access#set-linux-user) | <span data-ttu-id="1544a-137">Merhaba SSH anahtar toogive hello geçerli kullanıcı erişim toohello VM sıfırlar.</span><span class="sxs-lookup"><span data-stu-id="1544a-137">Resets hello SSH key toogive hello current user access toohello VM.</span></span> |
| [<span data-ttu-id="1544a-138">az vm-IP-adresleri listesi</span><span class="sxs-lookup"><span data-stu-id="1544a-138">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="1544a-139">Merhaba oluşturulan VM Hello IP adresini alır.</span><span class="sxs-lookup"><span data-stu-id="1544a-139">Gets hello IP address of hello VM that was created.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1544a-140">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1544a-140">Next steps</span></span>

<span data-ttu-id="1544a-141">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1544a-141">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="1544a-142">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1544a-142">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
