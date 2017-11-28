---
title: "Azure CLI 1.0 ile bir Azure şablonu kullanarak bir Linux VM aaaCreate | Microsoft Docs"
description: "Hello Azure CLI 1.0 ve Azure Resource Manager şablonu kullanarak Azure'da bir Linux VM oluşturma."
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
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a><span data-ttu-id="072f9-103">Azure CLI 1.0 bir Azure Resource Manager şablonu kullanarak Linux VM bir toocreate hello nasıl</span><span class="sxs-lookup"><span data-stu-id="072f9-103">How toocreate a Linux VM using hello Azure CLI 1.0 an Azure Resource Manager template</span></span>
<span data-ttu-id="072f9-104">Bu makalede nasıl tooquickly hello Azure CLI 1.0 ve Azure Resource Manager şablonu kullanarak bir Linux sanal makine dağıtma gösterilir.</span><span class="sxs-lookup"><span data-stu-id="072f9-104">This article shows you how tooquickly deploy a Linux Virtual Machine using hello Azure CLI 1.0 and an Azure Resource Manager template.</span></span> <span data-ttu-id="072f9-105">Merhaba makale gerektirir:</span><span class="sxs-lookup"><span data-stu-id="072f9-105">hello article requires:</span></span>

* <span data-ttu-id="072f9-106">bir Azure hesabı ([ücretsiz deneme sürümü edinin](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="072f9-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="072f9-107">Merhaba [Azure CLI 1.0](../../cli-install-nodejs.md) oturum açarken `azure login`.</span><span class="sxs-lookup"><span data-stu-id="072f9-107">hello [Azure CLI 1.0](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="072f9-108">Hello Azure CLI *olmalıdır* Azure Resource Manager moduna `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="072f9-108">hello Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>

<span data-ttu-id="072f9-109">Hello kullanarak bir Linux VM şablonu da hızlı bir şekilde dağıtabilirsiniz [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="072f9-109">You can also quickly deploy a Linux VM template by using hello [Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="072f9-110">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="072f9-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="072f9-111">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="072f9-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="072f9-112">[Azure CLI 1.0](#quick-command-summary) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="072f9-112">[Azure CLI 1.0](#quick-command-summary) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="072f9-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="072f9-113">[Azure CLI 2.0](create-ssh-secured-vm-from-template.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="quick-command-summary"></a><span data-ttu-id="072f9-114">Hızlı Komut Özeti</span><span class="sxs-lookup"><span data-stu-id="072f9-114">Quick Command Summary</span></span>
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="072f9-115">Ayrıntılı Kılavuz</span><span class="sxs-lookup"><span data-stu-id="072f9-115">Detailed Walkthrough</span></span>
<span data-ttu-id="072f9-116">Şablonları toocreate sanal makineleri Azure üzerinde toocustomize istediğiniz hello başlatma, kullanıcı adları ve ana bilgisayar adları gibi ayarları sırasında ayarlarla sağlar.</span><span class="sxs-lookup"><span data-stu-id="072f9-116">Templates allow you toocreate VMs on Azure with settings that you want toocustomize during hello launch, settings like usernames and hostnames.</span></span> <span data-ttu-id="072f9-117">Bu makalede; SSH'ye açık, 22 numaralı bağlantı noktasına sahip bir ağ güvenlik grubu (NSG) ile birlikte Ubuntu VM'yi kullanarak bir Azure şablonu başlatıyoruz.</span><span class="sxs-lookup"><span data-stu-id="072f9-117">For this article, we are launching an Azure template utilizing an Ubuntu VM along with a network security group (NSG) with port 22 open for SSH.</span></span>

<span data-ttu-id="072f9-118">Azure Resource Manager şablonları, bir defalık basit görevler (örneğin, bu makalede yapıldığı gibi bir Ubuntu VM'nin başlatılması) için kullanılabilen JSON dosyalarıdır.</span><span class="sxs-lookup"><span data-stu-id="072f9-118">Azure Resource Manager templates are JSON files that can be used for simple one-off tasks like launching an Ubuntu VM as done in this article.</span></span>  <span data-ttu-id="072f9-119">Azure şablonları kullanılan tooconstruct Azure yapılandırmalarını tüm ortamları gibi bir test, geliştirme veya Üretim dağıtımı yığını de olabilir.</span><span class="sxs-lookup"><span data-stu-id="072f9-119">Azure Templates can also be used tooconstruct complex Azure configurations of entire environments like a testing, dev, or production deployment stack.</span></span>

## <a name="create-hello-linux-vm"></a><span data-ttu-id="072f9-120">Merhaba Linux VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="072f9-120">Create hello Linux VM</span></span>
<span data-ttu-id="072f9-121">Kod örnekteki nasıl aşağıdaki hello toocall `azure group create` toocreate bir kaynak grubu ve hello sırasında bir SSH güvenlikli Linux VM dağıtmak kullanarak aynı zaman [bu Azure Resource Manager şablonu](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="072f9-121">hello following code example shows how toocall `azure group create` toocreate a resource group and deploy an SSH-secured Linux VM at hello same time using [this Azure Resource Manager template](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json).</span></span> <span data-ttu-id="072f9-122">Benzersiz tooyour ortamı toouse adları olması gerekir, örneğin unutmayın.</span><span class="sxs-lookup"><span data-stu-id="072f9-122">Remember that in your example you need toouse names that are unique tooyour environment.</span></span> <span data-ttu-id="072f9-123">Bu örnekte *myResourceGroup* hello kaynak grubu adı olarak ve *myVM* hello VM adı olarak.</span><span class="sxs-lookup"><span data-stu-id="072f9-123">This example uses *myResourceGroup* as hello resource group name, and *myVM* as hello VM name.</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

<span data-ttu-id="072f9-124">Merhaba çıktı hello çıkış bloğuna aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="072f9-124">hello output should look like hello following output block:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
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

<span data-ttu-id="072f9-125">Bu örnek hello kullanarak bir VM'i dağıtılan `--template-uri` parametresi.</span><span class="sxs-lookup"><span data-stu-id="072f9-125">That example deployed a VM using hello `--template-uri` parameter.</span></span>  <span data-ttu-id="072f9-126">Ayrıca indirin veya yerel olarak bir şablon oluşturmak ve hello kullanarak hello şablonunu geçirmek `--template-file` bağımsız değişken olarak bir yol toohello şablon dosyası parametresiyle.</span><span class="sxs-lookup"><span data-stu-id="072f9-126">You can also download or create a template locally and pass hello template using hello `--template-file` parameter with a path toohello template file as an argument.</span></span> <span data-ttu-id="072f9-127">Hello Azure CLI hello şablon tarafından gereken hello parametrelerini ister.</span><span class="sxs-lookup"><span data-stu-id="072f9-127">hello Azure CLI prompts you for hello parameters required by hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="072f9-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="072f9-128">Next steps</span></span>
<span data-ttu-id="072f9-129">Arama hello [Şablon Galerisi](https://azure.microsoft.com/documentation/templates/) toodiscover hangi uygulama çerçeveleri toodeploy sonraki.</span><span class="sxs-lookup"><span data-stu-id="072f9-129">Search hello [templates gallery](https://azure.microsoft.com/documentation/templates/) toodiscover what app frameworks toodeploy next.</span></span>

