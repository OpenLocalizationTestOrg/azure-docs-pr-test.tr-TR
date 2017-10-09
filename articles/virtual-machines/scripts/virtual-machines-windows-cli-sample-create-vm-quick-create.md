---
title: "aaaAzure CLI komut dosyası örneği - hızlı Oluştur bir Windows Server 2016 VM | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - hızlı bir Windows Server 2016 VM oluştur"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rickstercdn
ms.openlocfilehash: 4c736ce9e2ecc9ee75b34f903cad52c9c0ee0707
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="c4311-103">Hello Azure CLI ile bir sanal makineyi hızlı oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4311-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="c4311-104">Bu komut dosyasını Windows Server 2016 çalıştıran bir Azure sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c4311-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="c4311-105">Merhaba komut dosyasını çalıştırdıktan sonra hello sanal makine bir Uzak Masaüstü bağlantısı üzerinden erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4311-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c4311-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="c4311-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-quick/create-windows-vm-quick.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c4311-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="c4311-107">Clean up deployment</span></span> 

<span data-ttu-id="c4311-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="c4311-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="c4311-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="c4311-109">Script explanation</span></span>

<span data-ttu-id="c4311-110">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="c4311-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="c4311-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="c4311-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c4311-112">Komut</span><span class="sxs-lookup"><span data-stu-id="c4311-112">Command</span></span> | <span data-ttu-id="c4311-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="c4311-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c4311-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4311-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c4311-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c4311-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c4311-116">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="c4311-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c4311-117">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve ağ güvenlik grubu bağlanır.</span><span class="sxs-lookup"><span data-stu-id="c4311-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="c4311-118">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe belirtir ve yönetici kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c4311-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="c4311-119">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="c4311-119">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c4311-120">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="c4311-120">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c4311-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c4311-121">Next steps</span></span>

<span data-ttu-id="c4311-122">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c4311-122">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c4311-123">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c4311-123">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
