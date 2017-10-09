---
title: "aaaAzure CLI komut dosyası örneği - hızlı Oluştur bir Linux VM | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - hızlı bir Linux VM oluşturma"
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
ms.openlocfilehash: edecf274f4e401af3603e5be37a989e2e0eb22c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine"></a><span data-ttu-id="449d5-103">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="449d5-103">Create a virtual machine</span></span>

<span data-ttu-id="449d5-104">Bu komut dosyasını bir Ubuntu işletim sistemi ve ilgili ağ kaynaklarını ile bir Azure sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="449d5-104">This script creates an Azure Virtual Machine with an Ubuntu operating system and related networking resources.</span></span> <span data-ttu-id="449d5-105">Hello komut dosyasını çalıştırdıktan sonra hello sanal makineye SSH üzerinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="449d5-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="449d5-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="449d5-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="449d5-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="449d5-107">Clean up deployment</span></span> 

<span data-ttu-id="449d5-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="449d5-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="449d5-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="449d5-109">Script explanation</span></span>

<span data-ttu-id="449d5-110">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="449d5-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="449d5-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="449d5-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="449d5-112">Komut</span><span class="sxs-lookup"><span data-stu-id="449d5-112">Command</span></span> | <span data-ttu-id="449d5-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="449d5-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="449d5-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="449d5-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="449d5-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="449d5-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="449d5-116">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="449d5-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="449d5-117">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve ağ güvenlik grubu bağlanır.</span><span class="sxs-lookup"><span data-stu-id="449d5-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="449d5-118">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe belirtir ve yönetici kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="449d5-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="449d5-119">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="449d5-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="449d5-120">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="449d5-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="449d5-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="449d5-121">Next steps</span></span>

<span data-ttu-id="449d5-122">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="449d5-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="449d5-123">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="449d5-123">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
