---
title: "Azure CLI örnek komut dosyası - ile NGINX bir Linux VM oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 416624d9e378d09f4fb0593119dbc30adeb09f91
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="e0e66-103">İle NGINX bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0e66-103">Create a VM with NGINX</span></span>

<span data-ttu-id="e0e66-104">Bu komut dosyasını bir Azure sanal makine oluşturur ve NGINX yüklemek için Azure sanal makine özel betik uzantısı kullanır.</span><span class="sxs-lookup"><span data-stu-id="e0e66-104">This script creates an Azure Virtual Machine and uses the Azure Virtual Machine Custom Script Extension to install NGINX.</span></span> <span data-ttu-id="e0e66-105">Betiği çalıştırdıktan sonra sanal makine genel IP adresi demo Web sitesine erişebilir.</span><span class="sxs-lookup"><span data-stu-id="e0e66-105">After running the script, you can access a demo website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e0e66-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="e0e66-106">Sample script</span></span>

<span data-ttu-id="e0e66-107">[!code-azurecli-interactive[Ana](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "hızlı VM oluştur")]</span><span class="sxs-lookup"><span data-stu-id="e0e66-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]</span></span>

## <a name="custom-script-extension"></a><span data-ttu-id="e0e66-108">Özel Betik Uzantısı</span><span class="sxs-lookup"><span data-stu-id="e0e66-108">Custom Script Extension</span></span>

<span data-ttu-id="e0e66-109">Bu komut dosyasını, sanal makineyi özel betik uzantısı kopyalar.</span><span class="sxs-lookup"><span data-stu-id="e0e66-109">The custom script extension copies this script onto the virtual machine.</span></span> <span data-ttu-id="e0e66-110">Komut dosyası sonra NGINX web sunucusu yüklemek ve yapılandırmak için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e0e66-110">The script is then run to install and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="e0e66-111">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="e0e66-111">Clean up deployment</span></span> 

<span data-ttu-id="e0e66-112">Kaynak grubu, VM ve tüm ilgili kaynaklar kaldırmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e0e66-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e0e66-113">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="e0e66-113">Script explanation</span></span>

<span data-ttu-id="e0e66-114">Bu komut, bir kaynak grubu, sanal makine ve tüm ilgili kaynaklar oluşturmak için aşağıdaki komutları kullanır.</span><span class="sxs-lookup"><span data-stu-id="e0e66-114">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="e0e66-115">Komut belirli belgeleri tablo bağlanan her komut.</span><span class="sxs-lookup"><span data-stu-id="e0e66-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e0e66-116">Komut</span><span class="sxs-lookup"><span data-stu-id="e0e66-116">Command</span></span> | <span data-ttu-id="e0e66-117">Notlar</span><span class="sxs-lookup"><span data-stu-id="e0e66-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e0e66-118">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0e66-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e0e66-119">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0e66-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e0e66-120">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="e0e66-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="e0e66-121">Sanal makine oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0e66-121">Creates the virtual machine.</span></span> <span data-ttu-id="e0e66-122">Bu komut ayrıca kullanılacak sanal makine görüntüsü ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e0e66-122">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="e0e66-123">az vm-bağlantı noktası Aç</span><span class="sxs-lookup"><span data-stu-id="e0e66-123">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="e0e66-124">Gelen trafiğe izin vermek için bir ağ güvenlik grubu kural oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e0e66-124">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="e0e66-125">Bu örnekte, bağlantı noktası 80 HTTP trafiği için açıldı.</span><span class="sxs-lookup"><span data-stu-id="e0e66-125">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="e0e66-126">Azure vm uzantısı kümesi</span><span class="sxs-lookup"><span data-stu-id="e0e66-126">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e0e66-127">Ekler ve bir sanal makine uzantısı için bir VM çalışır.</span><span class="sxs-lookup"><span data-stu-id="e0e66-127">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="e0e66-128">Bu örnekte, özel betik uzantısı NGINX yüklemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e0e66-128">In this sample, the custom script extension is used to install NGINX.</span></span>|
| [<span data-ttu-id="e0e66-129">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="e0e66-129">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e0e66-130">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="e0e66-130">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e0e66-131">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e0e66-131">Next steps</span></span>

<span data-ttu-id="e0e66-132">Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0e66-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e0e66-133">Ek sanal makine CLI kod örnekleri bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e0e66-133">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
