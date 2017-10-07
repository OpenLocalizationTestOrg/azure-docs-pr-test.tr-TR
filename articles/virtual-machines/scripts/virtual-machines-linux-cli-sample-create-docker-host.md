---
title: "aaaAzure CLI komut dosyası örneği - Docker ana bilgisayar oluştur | Microsoft Docs"
description: "Azure CLI betik örnek - Docker ana bilgisayar oluştur"
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
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7df2561c428ff5d3ab0a0d53c8e046781996be77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="f30ec-103">Docker ile bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="f30ec-103">Create a VM with Docker</span></span>

<span data-ttu-id="f30ec-104">Bu komut dosyası etkin Docker ile bir sanal makine oluşturur ve NGINX çalıştıran bir Docker kapsayıcısı başlatır.</span><span class="sxs-lookup"><span data-stu-id="f30ec-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="f30ec-105">Hello komut dosyasını çalıştırdıktan sonra hello NGINX web sunucusu hello Azure sanal makinesinin FQDN'si hello erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f30ec-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f30ec-106">Örnek komut dosyası</span><span class="sxs-lookup"><span data-stu-id="f30ec-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f30ec-107">Dağıtımı temizleme</span><span class="sxs-lookup"><span data-stu-id="f30ec-107">Clean up deployment</span></span> 

<span data-ttu-id="f30ec-108">Çalışma hello aşağıdaki tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="f30ec-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="f30ec-109">Komut dosyası açıklaması</span><span class="sxs-lookup"><span data-stu-id="f30ec-109">Script explanation</span></span>

<span data-ttu-id="f30ec-110">Bu komut dosyası komutları toocreate hello dağıtım aşağıdaki hello kullanır.</span><span class="sxs-lookup"><span data-stu-id="f30ec-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="f30ec-111">Merhaba tablosundaki her öğesi toocommand belirli belgeleri bağlar.</span><span class="sxs-lookup"><span data-stu-id="f30ec-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f30ec-112">Komut</span><span class="sxs-lookup"><span data-stu-id="f30ec-112">Command</span></span> | <span data-ttu-id="f30ec-113">Notlar</span><span class="sxs-lookup"><span data-stu-id="f30ec-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f30ec-114">az grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="f30ec-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f30ec-115">Tüm kaynaklar depolandığı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f30ec-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f30ec-116">az vm oluşturma</span><span class="sxs-lookup"><span data-stu-id="f30ec-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="f30ec-117">Merhaba sanal makine oluşturur ve toohello ağ kartı, sanal ağ, alt ağ ve ağ güvenlik grubu bağlanır.</span><span class="sxs-lookup"><span data-stu-id="f30ec-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="f30ec-118">Bu komut ayrıca kullanılan hello sanal makine görüntü toobe ve yönetici kimlik bilgilerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="f30ec-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="f30ec-119">az vm-bağlantı noktası Aç</span><span class="sxs-lookup"><span data-stu-id="f30ec-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="f30ec-120">Bir ağ güvenlik grubu kural tooallow oluşturur gelen trafiği.</span><span class="sxs-lookup"><span data-stu-id="f30ec-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="f30ec-121">Bu örnekte, bağlantı noktası 80 HTTP trafiği için açıldı.</span><span class="sxs-lookup"><span data-stu-id="f30ec-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="f30ec-122">Azure vm uzantısı kümesi</span><span class="sxs-lookup"><span data-stu-id="f30ec-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f30ec-123">Ekler ve bir sanal makine uzantısı tooa VM çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="f30ec-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="f30ec-124">Bu örnekte kullanılan tooconfigure Docker ana hello Docker VM uzantısı olur.</span><span class="sxs-lookup"><span data-stu-id="f30ec-124">In this sample, hello Docker VM extension is used tooconfigure a Docker host.</span></span>|
| [<span data-ttu-id="f30ec-125">az grubu Sil</span><span class="sxs-lookup"><span data-stu-id="f30ec-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f30ec-126">Tüm iç içe kaynaklar dahil olmak üzere bir kaynak grubu siler.</span><span class="sxs-lookup"><span data-stu-id="f30ec-126">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f30ec-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f30ec-127">Next steps</span></span>

<span data-ttu-id="f30ec-128">Hello Azure CLI hakkında daha fazla bilgi için bkz: [Azure CLI belgelerine](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f30ec-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f30ec-129">Ek sanal makine CLI kod örnekleri hello bulunabilir [Azure Linux VM'de belgelerine](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f30ec-129">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
