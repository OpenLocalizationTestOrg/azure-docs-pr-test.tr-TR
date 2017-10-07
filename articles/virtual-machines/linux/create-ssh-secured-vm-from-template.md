---
title: "bir şablondan bir Linux VM azure'da aaaCreate | Microsoft Docs"
description: "Nasıl toouse hello Azure CLI 2.0 toocreate bir Resource Manager şablondan bir Linux VM"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="a4f9c-103">Nasıl toocreate Azure Resource Manager şablonları kullanarak Linux sanal makine</span><span class="sxs-lookup"><span data-stu-id="a4f9c-103">How toocreate a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="a4f9c-104">Bu makale size nasıl tooquickly dağıtmak Azure Resource Manager şablonları ve hello Azure CLI 2.0 ile Linux sanal makine (VM) gösterir.</span><span class="sxs-lookup"><span data-stu-id="a4f9c-104">This article shows you how tooquickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and hello Azure CLI 2.0.</span></span> <span data-ttu-id="a4f9c-105">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a4f9c-105">You can also perform these steps with hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="a4f9c-106">Şablonlara genel bakış</span><span class="sxs-lookup"><span data-stu-id="a4f9c-106">Templates overview</span></span>
<span data-ttu-id="a4f9c-107">Azure Resource Manager şablonları hello altyapısı ve Azure çözümünüzü yapılandırmasını tanımlayan JSON dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="a4f9c-107">Azure Resource Manager templates are JSON files that define hello infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="a4f9c-108">Bir şablon kullanarak çözümünü yaşam döngüsü boyunca defalarca dağıtabilir ve kaynaklarınızın tutarlı bir durumda dağıtıldığından emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4f9c-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="a4f9c-109">toolearn hello şablon ve onu nasıl oluşturmak hello biçimi hakkında daha fazla bilgi görmek [, ilk Azure Resource Manager şablonu oluşturma](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="a4f9c-109">toolearn more about hello format of hello template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="a4f9c-110">tooview hello JSON söz dizimi kaynak türleri için bkz: [kaynakları tanımlayan Azure Resource Manager şablonları](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="a4f9c-110">tooview hello JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="a4f9c-111">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4f9c-111">Create resource group</span></span>
<span data-ttu-id="a4f9c-112">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="a4f9c-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="a4f9c-113">Bir kaynak grubu bir sanal makine önce oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4f9c-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="a4f9c-114">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupVM* hello içinde *eastus* bölge:</span><span class="sxs-lookup"><span data-stu-id="a4f9c-114">hello following example creates a resource group named *myResourceGroupVM* in hello *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="a4f9c-115">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4f9c-115">Create virtual machine</span></span>
<span data-ttu-id="a4f9c-116">Merhaba aşağıdaki örnekte oluşturur bir VM'den [bu Azure Resource Manager şablonu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) ile [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="a4f9c-116">hello following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="a4f9c-117">Merhaba içeriğine gibi kendi SSH ortak anahtarını Hello değerini sağlamalısınız *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="a4f9c-117">Provide hello value of your own SSH public key, such as hello contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="a4f9c-118">SSH anahtar çifti toocreate gerekirse bkz [nasıl toocreate ve kullanım bir SSH çifti Azure Linux VM'ler için anahtar](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="a4f9c-118">If you need toocreate an SSH key pair, see [How toocreate and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="a4f9c-119">Bu örnekte, Github'da depolanan bir şablon belirtilen.</span><span class="sxs-lookup"><span data-stu-id="a4f9c-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="a4f9c-120">Ayrıca indirin veya bir şablon oluşturmak ve hello ile Merhaba yerel bir yol belirtin aynı `--template-file` parametresi.</span><span class="sxs-lookup"><span data-stu-id="a4f9c-120">You can also download or create a template and specify hello local path with hello same `--template-file` parameter.</span></span>

<span data-ttu-id="a4f9c-121">tooSSH tooyour VM elde hello ortak IP adresiyle [az ağ ortak IP Göster](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="a4f9c-121">tooSSH tooyour VM, obtain hello public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="a4f9c-122">Bundan sonra normal olarak SSH tooyour VM yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a4f9c-122">You can then SSH tooyour VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="a4f9c-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4f9c-123">Next steps</span></span>
<span data-ttu-id="a4f9c-124">Bu örnekte, temel bir Linux VM oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="a4f9c-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="a4f9c-125">Merhaba, uygulama çerçeveleri dahil etmek veya daha karmaşık ortamları oluşturma daha fazla Resource Manager şablonları için Gözat [Azure hızlı başlangıç Şablon Galerisi](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="a4f9c-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse hello [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>
