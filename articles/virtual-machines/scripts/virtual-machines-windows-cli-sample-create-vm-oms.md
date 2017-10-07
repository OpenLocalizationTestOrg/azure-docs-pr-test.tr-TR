---
title: "aaaAzure CLI komut dosyası örneği - OMS izleme ile bir Windows Server 2016 VM oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - OMS izleme ile bir Windows Server 2016 VM oluşturma"
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
ms.author: rclaus
ms.openlocfilehash: 4f070430ccc5d5402ed4a80ead3b78eff25dcd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="4991c-103">Bir VM Operations Management Suite ile izleme</span><span class="sxs-lookup"><span data-stu-id="4991c-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="4991c-104">Bu komut dosyasını bir Azure sanal makinesi oluşturur, hello Operations Management Suite (OMS) Aracısı'nı yükler ve bir OMS çalışma hello sistemiyle kaydeder.</span><span class="sxs-lookup"><span data-stu-id="4991c-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="4991c-105">Merhaba betik çalıştıktan sonra hello sanal makine hello OMS konsolunda görünür.</span><span class="sxs-lookup"><span data-stu-id="4991c-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4991c-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="4991c-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4991c-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="4991c-107">Clean up deployment</span></span> 

<span data-ttu-id="4991c-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="4991c-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="4991c-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="4991c-109">Script explanation</span></span>

<span data-ttu-id="4991c-110">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="4991c-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="4991c-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="4991c-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4991c-112">Komut</span><span class="sxs-lookup"><span data-stu-id="4991c-112">Command</span></span> | <span data-ttu-id="4991c-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="4991c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4991c-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="4991c-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4991c-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4991c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4991c-116">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="4991c-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="4991c-117">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="4991c-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="4991c-118">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4991c-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="4991c-119">Azure vm uzantısı kümesi</span><span class="sxs-lookup"><span data-stu-id="4991c-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="4991c-120">VM uzantısı bir sanal makineye karşı çalışır.</span><span class="sxs-lookup"><span data-stu-id="4991c-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="4991c-121">Bu durumda, hello Operations Management Suite Aracı Uzantısı kullanılan tooinstall hello OMS aracısı ve hello bir OMS çalışma alanında VM kaydolun.</span><span class="sxs-lookup"><span data-stu-id="4991c-121">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="4991c-122">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="4991c-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="4991c-123">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="4991c-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4991c-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4991c-124">Next steps</span></span>

<span data-ttu-id="4991c-125">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4991c-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4991c-126">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4991c-126">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
