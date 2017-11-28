---
title: "Azure CLI örnek komut dosyası - WordPress ile bir Linux VM oluşturma | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - WordPress ile bir Linux VM oluşturma"
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
ms.openlocfilehash: cc95a190b58cb208ac0b642fc9dc2253e993ca23
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="f696c-103">WordPress ile bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="f696c-103">Create a VM with WordPress</span></span>

<span data-ttu-id="f696c-104">Bu komut dosyasını bir sanal makine oluşturur ve WordPress yüklemek için Azure sanal makine özel betik uzantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="f696c-104">This script creates a virtual machine, and then uses the Azure Virtual Machine custom script extension to install WordPress.</span></span> <span data-ttu-id="f696c-105">Komut dosyasını çalıştırdıktan sonra WordPress yapılandırma sitesinde erişebilirsiniz `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="f696c-105">After running the script, you can access the WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f696c-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f696c-106">Sample script</span></span>

<span data-ttu-id="f696c-107">[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "hızlı VM oluştur")]</span><span class="sxs-lookup"><span data-stu-id="f696c-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f696c-108">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="f696c-108">Clean up deployment</span></span> 

<span data-ttu-id="f696c-109">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f696c-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f696c-110">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="f696c-110">Script explanation</span></span>

<span data-ttu-id="f696c-111">Bu komut, bir kaynak grubu, sanal makine ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="f696c-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="f696c-112">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="f696c-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f696c-113">Komut</span><span class="sxs-lookup"><span data-stu-id="f696c-113">Command</span></span> | <span data-ttu-id="f696c-114">Notlar</span><span class="sxs-lookup"><span data-stu-id="f696c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f696c-115">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f696c-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f696c-116">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f696c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f696c-117">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="f696c-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="f696c-118">Sanal makine oluşturur ve ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="f696c-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="f696c-119">Bu komut ayrıca kullanılacak sanal makine görüntüsü ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f696c-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="f696c-120">az vm-bağlantı noktası Aç</span><span class="sxs-lookup"><span data-stu-id="f696c-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="f696c-121">Gelen trafiğe izin vermek için bir ağ güvenlik grubu kural oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f696c-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="f696c-122">Bu örnekte, bağlantı noktası 80 HTTP trafiği için açıldı.</span><span class="sxs-lookup"><span data-stu-id="f696c-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="f696c-123">az vm uzantısı kümesi</span><span class="sxs-lookup"><span data-stu-id="f696c-123">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="f696c-124">Özel betik uzantısının WordPress yüklemek için bir komut dosyası çağırır sanal makine için ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f696c-124">Add the Custom Script Extension to the virtual machine, which invokes a script to install WordPress.</span></span> |
| [<span data-ttu-id="f696c-125">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="f696c-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f696c-126">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="f696c-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f696c-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f696c-127">Next steps</span></span>

<span data-ttu-id="f696c-128">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f696c-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f696c-129">Ek sanal makine CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f696c-129">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
