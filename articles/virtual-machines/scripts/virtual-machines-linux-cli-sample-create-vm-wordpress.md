---
title: "aaaAzure CLI komut dosyası örneği - WordPress ile bir Linux VM oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 2c5c03d08b6d5d27eb8c505b1dbd817eda5f2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="497d2-103">WordPress ile bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="497d2-103">Create a VM with WordPress</span></span>

<span data-ttu-id="497d2-104">Bu komut dosyasını bir sanal makine oluşturur ve ardından hello Azure sanal makine özel betik uzantısı tooinstall WordPress kullanır.</span><span class="sxs-lookup"><span data-stu-id="497d2-104">This script creates a virtual machine, and then uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="497d2-105">Çalışan hello betik sonra hello WordPress yapılandırma sitede erişebilirsiniz `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="497d2-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="497d2-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="497d2-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="497d2-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="497d2-107">Clean up deployment</span></span> 

<span data-ttu-id="497d2-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="497d2-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="497d2-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="497d2-109">Script explanation</span></span>

<span data-ttu-id="497d2-110">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="497d2-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="497d2-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="497d2-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="497d2-112">Komut</span><span class="sxs-lookup"><span data-stu-id="497d2-112">Command</span></span> | <span data-ttu-id="497d2-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="497d2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="497d2-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="497d2-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="497d2-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="497d2-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="497d2-116">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="497d2-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="497d2-117">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="497d2-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="497d2-118">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="497d2-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="497d2-119">az vm-bağlantı noktası Aç</span><span class="sxs-lookup"><span data-stu-id="497d2-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="497d2-120">Bir ağ güvenlik grubu kural tooallow oluşturur gelen trafiği.</span><span class="sxs-lookup"><span data-stu-id="497d2-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="497d2-121">Bu örnekte, bağlantı noktası 80 HTTP trafiği için açıldı.</span><span class="sxs-lookup"><span data-stu-id="497d2-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="497d2-122">az vm uzantısı kümesi</span><span class="sxs-lookup"><span data-stu-id="497d2-122">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="497d2-123">Merhaba özel betik uzantısının toohello sanal bir komut dosyası tooinstall WordPress çağıran makine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="497d2-123">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
| [<span data-ttu-id="497d2-124">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="497d2-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="497d2-125">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="497d2-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="497d2-126">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="497d2-126">Next steps</span></span>

<span data-ttu-id="497d2-127">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="497d2-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="497d2-128">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="497d2-128">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
