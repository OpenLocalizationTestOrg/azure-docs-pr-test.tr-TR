---
title: "Bir şablondan bir Linux VM oluşturma | Microsoft Docs"
description: "Bir Resource Manager şablonu bir Linux VM oluşturmak için Azure CLI 2.0 kullanma"
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
ms.openlocfilehash: 908a8a0c82b2d21fb25c9b33dbd714570d1ac272
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-virtual-machine-with-azure-resource-manager-templates"></a><span data-ttu-id="d7c97-103">Azure Resource Manager şablonları ile Linux sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7c97-103">How to create a Linux virtual machine with Azure Resource Manager templates</span></span>
<span data-ttu-id="d7c97-104">Bu makalede Azure Resource Manager şablonları ve Azure CLI 2.0 ile Linux sanal makine (VM) hızlı bir şekilde dağıtma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d7c97-104">This article shows you how to quickly deploy a Linux virtual machine (VM) with Azure Resource Manager templates and the Azure CLI 2.0.</span></span> <span data-ttu-id="d7c97-105">Bu adımları [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md) ile de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7c97-105">You can also perform these steps with the [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).</span></span>


## <a name="templates-overview"></a><span data-ttu-id="d7c97-106">Şablonlara genel bakış</span><span class="sxs-lookup"><span data-stu-id="d7c97-106">Templates overview</span></span>
<span data-ttu-id="d7c97-107">Azure Resource Manager şablonları altyapısı ve Azure çözümünüzü yapılandırmasını tanımlayan JSON dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="d7c97-107">Azure Resource Manager templates are JSON files that define the infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="d7c97-108">Bir şablon kullanarak çözümünü yaşam döngüsü boyunca defalarca dağıtabilir ve kaynaklarınızın tutarlı bir durumda dağıtıldığından emin olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d7c97-108">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="d7c97-109">Şablon ve oluşturmak nasıl biçimi hakkında daha fazla bilgi için bkz: [, ilk Azure Resource Manager şablonu oluşturma](../../azure-resource-manager/resource-manager-create-first-template.md).</span><span class="sxs-lookup"><span data-stu-id="d7c97-109">To learn more about the format of the template and how you construct it, see [Create your first Azure Resource Manager template](../../azure-resource-manager/resource-manager-create-first-template.md).</span></span> <span data-ttu-id="d7c97-110">Kaynak türleri için JSON söz dizimini görüntülemek üzere bkz. [Azure Resource Manager şablonlarında kaynak tanımlama](/azure/templates/).</span><span class="sxs-lookup"><span data-stu-id="d7c97-110">To view the JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>


## <a name="create-resource-group"></a><span data-ttu-id="d7c97-111">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7c97-111">Create resource group</span></span>
<span data-ttu-id="d7c97-112">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="d7c97-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="d7c97-113">Bir kaynak grubu bir sanal makine önce oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d7c97-113">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="d7c97-114">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroupVM* içinde *eastus* bölge:</span><span class="sxs-lookup"><span data-stu-id="d7c97-114">The following example creates a resource group named *myResourceGroupVM* in the *eastus* region:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="d7c97-115">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="d7c97-115">Create virtual machine</span></span>
<span data-ttu-id="d7c97-116">Aşağıdaki örnek, bir VM'den oluşturur [bu Azure Resource Manager şablonu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) ile [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="d7c97-116">The following example creates a VM from [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="d7c97-117">İçeriği gibi kendi SSH ortak anahtarı değerini sağlamalısınız *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="d7c97-117">Provide the value of your own SSH public key, such as the contents of *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="d7c97-118">SSH anahtar çifti oluşturmanız gerekiyorsa, bkz: [nasıl oluşturulacağı ve Linux VM'ler için Azure'da SSH anahtar çifti kullanılmaya](mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="d7c97-118">If you need to create an SSH key pair, see [How to create and use an SSH key pair for Linux VMs in Azure](mac-create-ssh-keys.md).</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

<span data-ttu-id="d7c97-119">Bu örnekte, Github'da depolanan bir şablon belirtilen.</span><span class="sxs-lookup"><span data-stu-id="d7c97-119">In this example, you specified a template stored in GitHub.</span></span> <span data-ttu-id="d7c97-120">Ayrıca indirin veya bir şablon oluşturmak ve yerel yolu ile aynı belirtin `--template-file` parametresi.</span><span class="sxs-lookup"><span data-stu-id="d7c97-120">You can also download or create a template and specify the local path with the same `--template-file` parameter.</span></span>

<span data-ttu-id="d7c97-121">VM için SSH için ortak IP adresi ile elde [az ağ ortak IP Göster](/cli/azure/network/public-ip#show):</span><span class="sxs-lookup"><span data-stu-id="d7c97-121">To SSH to your VM, obtain the public IP address with [az network public-ip show](/cli/azure/network/public-ip#show):</span></span>

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="d7c97-122">Normal olarak, VM için SSH kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d7c97-122">You can then SSH to your VM as normal:</span></span>

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a><span data-ttu-id="d7c97-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d7c97-123">Next steps</span></span>
<span data-ttu-id="d7c97-124">Bu örnekte, temel bir Linux VM oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="d7c97-124">In this example, you created a basic Linux VM.</span></span> <span data-ttu-id="d7c97-125">Uygulama çerçeveleri dahil etmek veya daha karmaşık ortamları oluşturma daha fazla Resource Manager şablonları için Gözat [Azure hızlı başlangıç Şablon Galerisi](https://azure.microsoft.com/documentation/templates/).</span><span class="sxs-lookup"><span data-stu-id="d7c97-125">For more Resource Manager templates that include application frameworks or create more complex environments, browse the [Azure quickstart templates gallery](https://azure.microsoft.com/documentation/templates/).</span></span>