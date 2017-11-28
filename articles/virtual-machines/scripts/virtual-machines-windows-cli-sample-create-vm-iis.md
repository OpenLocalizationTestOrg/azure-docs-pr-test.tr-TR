---
title: "aaaAzure CLI komut dosyası örneği - IIS yüklemek | Microsoft Docs"
description: "Azure CLI komut dosyası örneği - IIS yükleme"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 2fabc9522f424cab4c672084ba8bedfd623c87cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="80881-103">Hello Azure CLI ile bir sanal makineyi hızlı oluşturma</span><span class="sxs-lookup"><span data-stu-id="80881-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="80881-104">Bu komut dosyasını Windows Server 2016 çalıştıran bir Azure sanal makine oluşturur ve hello Azure sanal makine özel betik uzantısının tooinstall IIS kullanır.</span><span class="sxs-lookup"><span data-stu-id="80881-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses hello Azure Virtual Machine Custom Script Extension tooinstall IIS.</span></span> <span data-ttu-id="80881-105">Merhaba komut dosyasını çalıştırdıktan sonra hello varsayılan IIS Web sitesinde hello genel IP adresi hello sanal makinenin erişebilir.</span><span class="sxs-lookup"><span data-stu-id="80881-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="80881-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="80881-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="80881-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="80881-107">Clean up deployment</span></span> 

<span data-ttu-id="80881-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="80881-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="80881-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="80881-109">Script explanation</span></span>

<span data-ttu-id="80881-110">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="80881-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="80881-111">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="80881-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="80881-112">Komut</span><span class="sxs-lookup"><span data-stu-id="80881-112">Command</span></span> | <span data-ttu-id="80881-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="80881-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="80881-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="80881-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="80881-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="80881-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="80881-116">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="80881-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="80881-117">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve ağ güvenlik grubu bağlanır.</span><span class="sxs-lookup"><span data-stu-id="80881-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="80881-118">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe belirtir ve yönetici kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="80881-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="80881-119">az vm-bağlantı noktası Aç</span><span class="sxs-lookup"><span data-stu-id="80881-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="80881-120">Bir ağ güvenlik grubu kural tooallow oluşturur gelen trafiği.</span><span class="sxs-lookup"><span data-stu-id="80881-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="80881-121">Bu örnekte, bağlantı noktası 80 HTTP trafiği için açıldı.</span><span class="sxs-lookup"><span data-stu-id="80881-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="80881-122">Azure vm uzantısı kümesi</span><span class="sxs-lookup"><span data-stu-id="80881-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="80881-123">Ekler ve bir sanal makine uzantısı tooa VM çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="80881-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="80881-124">Bu örnekte kullanılan tooinstall IIS hello özel komut dosyası uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="80881-124">In this sample, hello custom script extension is used tooinstall IIS.</span></span>|
| [<span data-ttu-id="80881-125">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="80881-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="80881-126">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="80881-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="80881-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="80881-127">Next steps</span></span>

<span data-ttu-id="80881-128">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="80881-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="80881-129">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Windows VM belgelerine](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="80881-129">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
