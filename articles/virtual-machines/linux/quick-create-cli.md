---
title: "aaaAzure hızlı başlangıç - VM CLI oluşturun | Microsoft Docs"
description: "Hızlı bir şekilde hello Azure CLI toocreate sanal makinelerle öğrenin."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="484ac-103">Hello Azure CLI ile Linux sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="484ac-103">Create a Linux virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="484ac-104">Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="484ac-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="484ac-105">Ubuntu server çalıştıran bir sanal makine Hello Azure CLI toodeploy kullanarak bu kılavuzu ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="484ac-105">This guide details using hello Azure CLI toodeploy a virtual machine running Ubuntu server.</span></span> <span data-ttu-id="484ac-106">Merhaba sunucu dağıtıldığında, bir SSH bağlantısı oluşturulur ve bir NGINX Web sunucusu yüklenir.</span><span class="sxs-lookup"><span data-stu-id="484ac-106">Once hello server is deployed, an SSH connection is created, and an NGINX webserver is installed.</span></span>

<span data-ttu-id="484ac-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="484ac-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="484ac-108">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="484ac-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="484ac-109">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="484ac-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="484ac-110">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="484ac-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="484ac-111">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="484ac-111">Create a resource group</span></span>

<span data-ttu-id="484ac-112">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="484ac-112">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="484ac-113">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="484ac-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="484ac-114">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.</span><span class="sxs-lookup"><span data-stu-id="484ac-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="484ac-115">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="484ac-115">Create virtual machine</span></span>

<span data-ttu-id="484ac-116">Bir VM ile Merhaba oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="484ac-116">Create a VM with hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="484ac-117">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* ve zaten bir varsayılan anahtar konumda yoksa, SSH anahtarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="484ac-117">hello following example creates a VM named *myVM* and creates SSH keys if they do not already exist in a default key location.</span></span> <span data-ttu-id="484ac-118">toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="484ac-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

<span data-ttu-id="484ac-119">Merhaba VM oluşturduğunuzda hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir.</span><span class="sxs-lookup"><span data-stu-id="484ac-119">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="484ac-120">Merhaba not edin `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="484ac-120">Take note of hello `publicIpAddress`.</span></span> <span data-ttu-id="484ac-121">Kullanılan tooaccess hello VM adresidir.</span><span class="sxs-lookup"><span data-stu-id="484ac-121">This address is used tooaccess hello VM.</span></span>

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="484ac-122">Web trafiği için 80 numaralı bağlantı noktasını açın</span><span class="sxs-lookup"><span data-stu-id="484ac-122">Open port 80 for web traffic</span></span> 

<span data-ttu-id="484ac-123">Varsayılan olarak, Azure’a dağıtılmış Linux sanal makinelerinde yalnızca SSH bağlantılarına izin verilir.</span><span class="sxs-lookup"><span data-stu-id="484ac-123">By default only SSH connections are allowed into Linux virtual machines deployed in Azure.</span></span> <span data-ttu-id="484ac-124">Bu VM toobe bir Web sunucusu olacaksa, hello Internet gelen tooopen bağlantı noktası 80 gerekir.</span><span class="sxs-lookup"><span data-stu-id="484ac-124">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="484ac-125">Kullanım hello [az vm Aç-port](/cli/azure/vm#open-port) komutu tooopen hello istenen bağlantı noktası.</span><span class="sxs-lookup"><span data-stu-id="484ac-125">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a><span data-ttu-id="484ac-126">VM’ye SSH uygulama</span><span class="sxs-lookup"><span data-stu-id="484ac-126">SSH into your VM</span></span>

<span data-ttu-id="484ac-127">Kullanım hello aşağıdaki toocreate SSH oturumu hello sanal makineyle bir komutu.</span><span class="sxs-lookup"><span data-stu-id="484ac-127">Use hello following command toocreate an SSH session with hello virtual machine.</span></span> <span data-ttu-id="484ac-128">Emin tooreplace olun  *<publicIpAddress>*  hello ile sanal makinenize genel IP adresini düzeltin.</span><span class="sxs-lookup"><span data-stu-id="484ac-128">Make sure tooreplace *<publicIpAddress>* with hello correct public IP address of your virtual machine.</span></span>  <span data-ttu-id="484ac-129">Yukarıdaki örneğimizde IP adresi *40.68.254.142* şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="484ac-129">In our example above our IP address was *40.68.254.142*.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a><span data-ttu-id="484ac-130">NGINX yükleme</span><span class="sxs-lookup"><span data-stu-id="484ac-130">Install NGINX</span></span>

<span data-ttu-id="484ac-131">Kullanım hello aşağıdaki komut dosyası tooupdate paket kaynaklarını bash ve hello son NGINX paketini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="484ac-131">Use hello following bash script tooupdate package sources and install hello latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a><span data-ttu-id="484ac-132">Merhaba NGINX Karşılama sayfasını görüntüle</span><span class="sxs-lookup"><span data-stu-id="484ac-132">View hello NGINX welcome page</span></span>

<span data-ttu-id="484ac-133">Yüklü NGINX ve bağlantı noktası 80, VM'den hello Internet - üzerinde şimdi açık seçim tooview hello varsayılan NGINX Hoş Geldiniz sayfasını bir web tarayıcısı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="484ac-133">With NGINX installed and port 80 now open on your VM from hello Internet - you can use a web browser of your choice tooview hello default NGINX welcome page.</span></span> <span data-ttu-id="484ac-134">Emin toouse hello olması *Publicıpaddress* toovisit hello varsayılan sayfa belgelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="484ac-134">Be sure toouse hello *publicIpAddress* you documented above toovisit hello default page.</span></span> 

![Varsayılan NGINX sitesi](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="484ac-136">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="484ac-136">Clean up resources</span></span>

<span data-ttu-id="484ac-137">Artık gerektiğinde Merhaba kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="484ac-137">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="484ac-138">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="484ac-138">Next steps</span></span>

<span data-ttu-id="484ac-139">Bu hızlı başlangıçta basit bir sanal makine ve bir ağ güvenlik grubu kuralı dağıtıp, bir web sunucusu yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="484ac-139">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="484ac-140">Azure sanal makinelerde hakkında daha fazla toolearn toohello öğretici Linux VM'ler için devam edin.</span><span class="sxs-lookup"><span data-stu-id="484ac-140">toolearn more about Azure virtual machines, continue toohello tutorial for Linux VMs.</span></span>


> [!div class="nextstepaction"]
> [<span data-ttu-id="484ac-141">Azure Linux sanal makine öğreticileri</span><span class="sxs-lookup"><span data-stu-id="484ac-141">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
