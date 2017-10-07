---
title: "aaaAzure CLI komut dosyası örneği - DSC kullanarak IIS ile Windows Server 2016 VM oluşturma | Microsoft Docs"
description: "Azure CLI betik örnek - Windows Server 2016 VM DSC kullanarak IIS ile oluşturma"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 9883b5925dddca3dd53d083679a0e76d0fb982e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="5a890-103">Bir VM DSC kullanarak IIS ile oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a890-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="5a890-104">Bu komut dosyasını bir sanal makine oluşturur ve hello Azure sanal makine DSC özel betik uzantısı tooinstall kullanır ve IIS yapılandırmak.</span><span class="sxs-lookup"><span data-stu-id="5a890-104">This script creates a virtual machine, and uses hello Azure Virtual Machine DSC custom script extension tooinstall and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5a890-105">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="5a890-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5a890-106">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="5a890-106">Clean up deployment</span></span> 

<span data-ttu-id="5a890-107">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="5a890-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="5a890-108">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="5a890-108">Script explanation</span></span>

<span data-ttu-id="5a890-109">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="5a890-109">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="5a890-110">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="5a890-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5a890-111">Komut</span><span class="sxs-lookup"><span data-stu-id="5a890-111">Command</span></span> | <span data-ttu-id="5a890-112">Notlar</span><span class="sxs-lookup"><span data-stu-id="5a890-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5a890-113">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a890-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5a890-114">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="5a890-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5a890-115">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="5a890-115">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="5a890-116">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve NSG bağlanır.</span><span class="sxs-lookup"><span data-stu-id="5a890-116">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="5a890-117">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="5a890-117">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="5a890-118">az vm uzantısı kümesi</span><span class="sxs-lookup"><span data-stu-id="5a890-118">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="5a890-119">Merhaba özel betik uzantısının toohello sanal makineyi bir komut dosyası tooinstall IIS çağıran ekleyin.</span><span class="sxs-lookup"><span data-stu-id="5a890-119">Add hello Custom Script Extension toohello virtual machine which invokes a script tooinstall IIS.</span></span> |
| [<span data-ttu-id="5a890-120">az vm-bağlantı noktası Aç</span><span class="sxs-lookup"><span data-stu-id="5a890-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="5a890-121">Bir ağ güvenlik grubu kural tooallow oluşturur gelen trafiği.</span><span class="sxs-lookup"><span data-stu-id="5a890-121">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="5a890-122">Bu örnekte, bağlantı noktası 80 HTTP trafiği için açıldı.</span><span class="sxs-lookup"><span data-stu-id="5a890-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="5a890-123">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="5a890-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="5a890-124">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="5a890-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5a890-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5a890-125">Next steps</span></span>

<span data-ttu-id="5a890-126">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5a890-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5a890-127">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5a890-127">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
