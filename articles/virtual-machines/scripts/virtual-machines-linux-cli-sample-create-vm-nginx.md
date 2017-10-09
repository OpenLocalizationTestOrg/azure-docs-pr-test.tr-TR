---
title: "CLI komut dosyası örneği - aaaAzure ile NGINX bir Linux VM oluşturma | Microsoft Docs"
description: "Azure CLI örnek komut dosyası - ile NGINX bir Linux VM oluşturma"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="77728-103">İle NGINX bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="77728-103">Create a VM with NGINX</span></span>

<span data-ttu-id="77728-104">Bu komut dosyasını bir Azure sanal makine oluşturur ve hello Azure sanal makine özel betik uzantısının tooinstall NGINX kullanır.</span><span class="sxs-lookup"><span data-stu-id="77728-104">This script creates an Azure Virtual Machine and uses hello Azure Virtual Machine Custom Script Extension tooinstall NGINX.</span></span> <span data-ttu-id="77728-105">Merhaba komut dosyasını çalıştırdıktan sonra hello genel IP adresi hello sanal makinenin demo Web sitesine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="77728-105">After running hello script, you can access a demo website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="77728-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="77728-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a><span data-ttu-id="77728-107">Özel Betik Uzantısı</span><span class="sxs-lookup"><span data-stu-id="77728-107">Custom Script Extension</span></span>

<span data-ttu-id="77728-108">Merhaba özel betik uzantısı hello sanal makine bu betiğini kopyalar.</span><span class="sxs-lookup"><span data-stu-id="77728-108">hello custom script extension copies this script onto hello virtual machine.</span></span> <span data-ttu-id="77728-109">Merhaba betik tooinstall ardından çalıştırın ve bir NGINX web sunucusu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="77728-109">hello script is then run tooinstall and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="77728-110">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="77728-110">Clean up deployment</span></span> 

<span data-ttu-id="77728-111">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="77728-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="77728-112">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="77728-112">Script explanation</span></span>

<span data-ttu-id="77728-113">Bu komut dosyası komutları toocreate bir kaynak grubu, sanal makine aşağıdaki hello kullanır ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="77728-113">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="77728-114">Her komut hello tablosundaki toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="77728-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="77728-115">Komut</span><span class="sxs-lookup"><span data-stu-id="77728-115">Command</span></span> | <span data-ttu-id="77728-116">Notlar</span><span class="sxs-lookup"><span data-stu-id="77728-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="77728-117">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="77728-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="77728-118">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="77728-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="77728-119">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="77728-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="77728-120">Merhaba sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="77728-120">Creates hello virtual machine.</span></span> <span data-ttu-id="77728-121">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="77728-121">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="77728-122">az vm-bağlantı noktası Aç</span><span class="sxs-lookup"><span data-stu-id="77728-122">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="77728-123">Bir ağ güvenlik grubu kural tooallow oluşturur gelen trafiği.</span><span class="sxs-lookup"><span data-stu-id="77728-123">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="77728-124">Bu örnekte, bağlantı noktası 80 HTTP trafiği için açıldı.</span><span class="sxs-lookup"><span data-stu-id="77728-124">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="77728-125">Azure vm uzantısı kümesi</span><span class="sxs-lookup"><span data-stu-id="77728-125">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="77728-126">Ekler ve bir sanal makine uzantısı tooa VM çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="77728-126">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="77728-127">Bu örnekte kullanılan tooinstall NGINX hello özel komut dosyası uzantısıdır.</span><span class="sxs-lookup"><span data-stu-id="77728-127">In this sample, hello custom script extension is used tooinstall NGINX.</span></span>|
| [<span data-ttu-id="77728-128">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="77728-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="77728-129">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="77728-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="77728-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="77728-130">Next steps</span></span>

<span data-ttu-id="77728-131">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="77728-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="77728-132">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="77728-132">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
