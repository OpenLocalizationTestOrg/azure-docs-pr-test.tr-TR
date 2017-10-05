---
title: "Azure CLI betik örnek - OMS izleme ile bir Windows Server 2016 VM oluşturma | Microsoft Docs"
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
ms.openlocfilehash: ddb191163061dc47712e024c8c1d7a6f4bdf325b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="e8854-103">Bir VM Operations Management Suite ile izleme</span><span class="sxs-lookup"><span data-stu-id="e8854-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="e8854-104">Bu komut dosyasını bir Azure sanal makinesi oluşturur, Operations Management Suite (OMS) Aracısı'nı yükler ve bir OMS çalışma sistemiyle kaydeder.</span><span class="sxs-lookup"><span data-stu-id="e8854-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="e8854-105">Betik çalıştıktan sonra sanal makine OMS konsolunda görünür.</span><span class="sxs-lookup"><span data-stu-id="e8854-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e8854-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="e8854-106">Sample script</span></span>

<span data-ttu-id="e8854-107">[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "hızlı VM oluştur")]</span><span class="sxs-lookup"><span data-stu-id="e8854-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e8854-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="e8854-108">Clean up deployment</span></span> 

<span data-ttu-id="e8854-109">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e8854-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e8854-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="e8854-110">Script explanation</span></span>

<span data-ttu-id="e8854-111">Bu komut, bir kaynak grubu, sanal makine ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="e8854-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="e8854-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="e8854-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e8854-113">Komut</span><span class="sxs-lookup"><span data-stu-id="e8854-113">Command</span></span> | <span data-ttu-id="e8854-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="e8854-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e8854-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e8854-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e8854-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e8854-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e8854-117">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="e8854-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="e8854-118">Sanal makine oluşturur ve ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="e8854-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="e8854-119">Bu komut ayrıca kullanılacak sanal makine görüntüsü ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e8854-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="e8854-120">Azure vm uzantısı kümesi</span><span class="sxs-lookup"><span data-stu-id="e8854-120">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e8854-121">VM uzantısı bir sanal makineye karşı çalışır.</span><span class="sxs-lookup"><span data-stu-id="e8854-121">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="e8854-122">Bu durumda, Operations Management Suite Aracı Uzantısı OMS Aracısı'nı yüklemek ve bir OMS çalışma alanında VM kaydetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e8854-122">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="e8854-123">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="e8854-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e8854-124">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="e8854-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e8854-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e8854-125">Next steps</span></span>

<span data-ttu-id="e8854-126">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e8854-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e8854-127">Ek sanal makine CLI kod örnekleri bulunabilir [Azure Windows VM belgelerine](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8854-127">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
