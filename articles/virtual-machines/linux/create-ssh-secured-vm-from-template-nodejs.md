---
title: "Azure CLI 1.0 ile bir Azure şablonu kullanarak bir Linux VM oluşturma | Microsoft Docs"
description: "Azure CLI 1.0 ve Azure Resource Manager şablonu kullanarak Azure'da bir Linux VM oluşturma."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 33d4aaa78fcdf3bd9e2e236606f2d3049f464a8a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-linux-vm-using-the-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="fd742-103">Bir Azure Resource Manager şablonu Azure CLI 1.0 kullanarak bir Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="fd742-103">How to create a Linux VM using the Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="fd742-104">Bu makalede hızlı bir şekilde Azure CLI 1.0 ve Azure Resource Manager şablonu kullanarak bir Linux sanal makine dağıtma gösterilir.</span><span class="sxs-lookup"><span data-stu-id="fd742-104">This article shows you how to quickly deploy a Linux Virtual Machine using the Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="fd742-105">Bu makale için şunlar gereklidir:</span><span class="sxs-lookup"><span data-stu-id="fd742-105">The article requires:</span></span>

* <span data-ttu-id="fd742-106">bir Azure hesabı ([ücretsiz deneme sürümü edinin](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="fd742-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="fd742-107">[Azure CLI 1.0](../../cli-install-nodejs.md) oturum açarken `azure login`.</span><span class="sxs-lookup"><span data-stu-id="fd742-107">the [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="fd742-108">Azure CLI'si, `azure config mode arm` Azure Resource Manager modunda *olmalıdır*.</span><span class="sxs-lookup"><span data-stu-id="fd742-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="fd742-109">[Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)’ı kullanarak da hızlı bir şekilde Linux VM şablonu dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd742-109">You can also quickly deploy a Linux VM template by using the [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="fd742-110">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="fd742-110">CLI versions to complete the task</span></span>
<span data-ttu-id="fd742-111">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fd742-111">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="fd742-112">[Azure CLI 1.0](#quick-command-summary) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="fd742-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="fd742-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız</span><span class="sxs-lookup"><span data-stu-id="fd742-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="fd742-114">Hızlı Komut Özeti</span><span class="sxs-lookup"><span data-stu-id="fd742-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="fd742-115">Ayrıntılı Kılavuz</span><span class="sxs-lookup"><span data-stu-id="fd742-115">Detailed Walkthrough</span></span>
<span data-ttu-id="fd742-116">Şablonlar, kullanıcı adları ve ana bilgisayar adları gibi çalıştırma sırasında özelleştirmek istediğiniz ayarlarla Azure'da VM'ler oluşturmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="fd742-116">Templates allow you to create VMs on Azure with settings that you want to customize during the launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="fd742-117">Bu makalede; SSH'ye açık, 22 numaralı bağlantı noktasına sahip bir ağ güvenlik grubu (NSG) ile birlikte Ubuntu VM'yi kullanarak bir Azure şablonu başlatıyoruz.</span><span class="sxs-lookup"><span data-stu-id="fd742-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="fd742-118">Azure Resource Manager şablonları, bir defalık basit görevler (örneğin, bu makalede yapıldığı gibi bir Ubuntu VM'nin başlatılması) için kullanılabilen JSON dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="fd742-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="fd742-119">Azure Şablonları; test, geliştirme veya üretim dağıtım yığını gibi tüm ortamların karmaşık Azure yapılandırmalarını oluşturmak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fd742-119">Azure Templates can also be used to construct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-the-linux-vm"></a><span data-ttu-id="fd742-120">Linux VM’i oluşturma</span><span class="sxs-lookup"><span data-stu-id="fd742-120">Create the Linux VM</span></span>
<span data-ttu-id="fd742-121">Aşağıdaki kod örneği [bu Azure Resource Manager şablonunu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) kullanarak bir kaynak grubu oluşturmak ve aynı zamanda bir SSH güvenlikli Linux VM dağıtmak için `azure group create` çağrısının nasıl gerçekleştireceğini açıklar.</span><span class="sxs-lookup"><span data-stu-id="fd742-121">The following code example shows how to call `azure group create` to create a resource group and deploy an SSH-secured Linux VM at the same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="fd742-122">Örneğinizde ortamınıza özel adları kullanmanız gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fd742-122">Remember that in your example you need to use names that are unique to your environment.</span></span> <span data-ttu-id="fd742-123">Bu örnekte *myResourceGroup* kaynak grubu adı olarak ve *myVM* VM adı.</span><span class="sxs-lookup"><span data-stu-id="fd742-123">This example uses *myResourceGroup* as the resource group name, and *myVM* as the VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="fd742-124">Çıktı aşağıdaki çıktı bloğu gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="fd742-124">The output should look like the following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for the following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="fd742-125">Bu örnekte, `--template-uri` parametresi kullanılarak bir VM dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="fd742-125">That example deployed a VM using the `--template-uri` parameter.</span></span>  <span data-ttu-id="fd742-126">Ayrıca şablon dosyasının yolu ile birlikte `--template-file` parametresini bağımsız değişken şeklinde kullanarak bir şablonu indirebilir, yerel olarak oluşturabilir ve şablonun geçişini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fd742-126">You can also download or create a template locally and pass the template using the `--template-file` parameter with a path to the template file as an argument.</span></span> <span data-ttu-id="fd742-127">Azure CLI sizden şablon için gerekli parametreleri isteyecektir.</span><span class="sxs-lookup"><span data-stu-id="fd742-127">The Azure CLI prompts you for the parameters required by the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd742-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fd742-128">Next steps</span></span>
<span data-ttu-id="fd742-129">Daha sonra dağıtılacak uygulama altyapılarını keşfetmek için [şablon galerisi](https://azure.microsoft.com/documentation/templates/)nde arama yapın.</span><span class="sxs-lookup"><span data-stu-id="fd742-129">Search the [templates gallery](https://azure.microsoft.com/documentation/templates/) to discover what app frameworks to deploy next.</span></span>

