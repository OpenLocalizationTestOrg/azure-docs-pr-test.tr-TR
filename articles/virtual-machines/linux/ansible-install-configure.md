---
title: "aaaInstall ve Ansible Azure sanal makineler ile kullanmak için yapılandırma | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve Ubuntu, CentOS ve SLES Azure kaynaklarını yönetmek için Ansible yapılandırın"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: b33d1893909b6134a5474617c9af2d6e4f627c05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a><span data-ttu-id="9b5d9-103">Yükleme ve Azure'da Ansible toomanage sanal makineleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9b5d9-103">Install and configure Ansible toomanage virtual machines in Azure</span></span>
<span data-ttu-id="9b5d9-104">Bu makalede, en yaygın Linux distro'lar tooinstall Ansible ve bazı için gerekli Azure Python SDK'sını modüllerini nasıl hello ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-104">This article details how tooinstall Ansible and required Azure Python SDK modules for some of hello most common Linux distros.</span></span> <span data-ttu-id="9b5d9-105">Ansible diğer distro'lar üzerinde yüklü hello paketleri toofit ayarlayarak belirli platformunuz yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-105">You can install Ansible on other distros by adjusting hello installed packages toofit your particular platform.</span></span> <span data-ttu-id="9b5d9-106">toocreate Azure da bilgi kaynaklarına güvenli bir şekilde nasıl toocreate ve Ansible toouse bilgilerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-106">toocreate Azure resources in a secure manner, you also learn how toocreate and define credentials for Ansible toouse.</span></span> 

<span data-ttu-id="9b5d9-107">Daha fazla yükleme seçenekleri ve ek platformlar için adımlar için hello bkz [Ansible Yükleme Kılavuzu](https://docs.ansible.com/ansible/intro_installation.html).</span><span class="sxs-lookup"><span data-stu-id="9b5d9-107">For more installation options and steps for additional platforms, see hello [Ansible install guide](https://docs.ansible.com/ansible/intro_installation.html).</span></span>


## <a name="install-ansible"></a><span data-ttu-id="9b5d9-108">Ansible yükleyin</span><span class="sxs-lookup"><span data-stu-id="9b5d9-108">Install Ansible</span></span>
<span data-ttu-id="9b5d9-109">İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9b5d9-109">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9b5d9-110">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupAnsible* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-110">hello following example creates a resource group named *myResourceGroupAnsible* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

<span data-ttu-id="9b5d9-111">Şimdi bir VM oluşturun ve Ansible distro'lar aşağıdaki hello biri için yükleyin:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-111">Now create a VM and install Ansible for one of hello following distros:</span></span>

- [<span data-ttu-id="9b5d9-112">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="9b5d9-112">Ubuntu 16.04 LTS</span></span>](#ubuntu1604-lts)
- [<span data-ttu-id="9b5d9-113">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="9b5d9-113">CentOS 7.3</span></span>](#centos-73)
- [<span data-ttu-id="9b5d9-114">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="9b5d9-114">SLES 12.2 SP2</span></span>](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a><span data-ttu-id="9b5d9-115">Ubuntu 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="9b5d9-115">Ubuntu 16.04 LTS</span></span>
<span data-ttu-id="9b5d9-116">[az vm create](/cli/azure/vm#create) ile bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="9b5d9-117">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-117">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="9b5d9-118">SSH VM tooyour kullanarak hello `publicIpAddress` hello not ettiğiniz hello VM çıktısını oluşturma işlemi:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-118">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="9b5d9-119">VM'nizi üzerinde hello Azure Python SDK'sını modülleri ve Ansible hello gerekli paketleri gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-119">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo apt-get update && sudo apt-get install -y libssl-dev libffi-dev python-dev python-pip

## Install Azure SDKs via pip
pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via apt
sudo apt-get install -y software-properties-common
sudo apt-add-repository -y ppa:ansible/ansible
sudo apt-get update && sudo apt-get install -y ansible
```

<span data-ttu-id="9b5d9-120">Artık çok geçmek[oluşturma Azure kimlik bilgilerini](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="9b5d9-120">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="centos-73"></a><span data-ttu-id="9b5d9-121">CentOS 7.3</span><span class="sxs-lookup"><span data-stu-id="9b5d9-121">CentOS 7.3</span></span>
<span data-ttu-id="9b5d9-122">[az vm create](/cli/azure/vm#create) ile bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-122">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="9b5d9-123">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-123">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="9b5d9-124">SSH VM tooyour kullanarak hello `publicIpAddress` hello not ettiğiniz hello VM çıktısını oluşturma işlemi:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-124">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="9b5d9-125">VM'nizi üzerinde hello Azure Python SDK'sını modülleri ve Ansible hello gerekli paketleri gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-125">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

<span data-ttu-id="9b5d9-126">Artık çok geçmek[oluşturma Azure kimlik bilgilerini](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="9b5d9-126">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


### <a name="sles-122-sp2"></a><span data-ttu-id="9b5d9-127">SLES 12.2 SP2</span><span class="sxs-lookup"><span data-stu-id="9b5d9-127">SLES 12.2 SP2</span></span>
<span data-ttu-id="9b5d9-128">[az vm create](/cli/azure/vm#create) ile bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-128">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="9b5d9-129">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVMAnsible*:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-129">hello following example creates a VM named *myVMAnsible*:</span></span>

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="9b5d9-130">SSH VM tooyour kullanarak hello `publicIpAddress` hello not ettiğiniz hello VM çıktısını oluşturma işlemi:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-130">SSH tooyour VM using hello `publicIpAddress` noted in hello output from hello VM create operation:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="9b5d9-131">VM'nizi üzerinde hello Azure Python SDK'sını modülleri ve Ansible hello gerekli paketleri gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-131">On your VM, install hello required packages for hello Azure Python SDK modules and Ansible as follows:</span></span>

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

<span data-ttu-id="9b5d9-132">Artık çok geçmek[oluşturma Azure kimlik bilgilerini](#create-azure-credentials).</span><span class="sxs-lookup"><span data-stu-id="9b5d9-132">Now move on too[Create Azure credentials](#create-azure-credentials).</span></span>


## <a name="create-azure-credentials"></a><span data-ttu-id="9b5d9-133">Azure kimlik bilgileri oluşturun</span><span class="sxs-lookup"><span data-stu-id="9b5d9-133">Create Azure credentials</span></span>
<span data-ttu-id="9b5d9-134">Ansible bir kullanıcı adı ve parola veya bir hizmet sorumlusu kullanarak Azure ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-134">Ansible communicates with Azure using a username and password or a service principal.</span></span> <span data-ttu-id="9b5d9-135">Bir Azure hizmet sorumlusu uygulamaları, hizmetleri ve Ansible gibi Otomasyon araçları ile birlikte kullanabileceğiniz bir güvenlik kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-135">An Azure service principal is a security identity that you can use with apps, services, and automation tools like Ansible.</span></span> <span data-ttu-id="9b5d9-136">Denetim ve toowhat işlemleri hello hizmet sorumlusu Azure'da gerçekleştirebilirsiniz gibi hello izinleri tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-136">You control and define hello permissions as toowhat operations hello service principal can perform in Azure.</span></span> <span data-ttu-id="9b5d9-137">yalnızca bir kullanıcı adı ve parola sağlayarak tooimprove güvenliği, bu örnek temel bir hizmet sorumlusu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-137">tooimprove security over just providing a username and password, this example creates a basic service principal.</span></span>

<span data-ttu-id="9b5d9-138">Bir hizmet sorumlusu ile oluşturma [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac) ve Ansible gereken çıktı hello kimlik bilgileri:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-138">Create a service principal with [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) and output hello credentials that Ansible needs:</span></span>

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

<span data-ttu-id="9b5d9-139">Komutları önceki hello hello çıktının bir örnek aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-139">An example of hello output from hello preceding commands is as follows:</span></span>

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

<span data-ttu-id="9b5d9-140">tooauthenticate tooAzure etmeniz, Azure aboneliğinizin kimliği ile tooobtain [az hesabı Göster](/cli/azure/account#show):</span><span class="sxs-lookup"><span data-stu-id="9b5d9-140">tooauthenticate tooAzure, you also need tooobtain your Azure subscription ID with [az account show](/cli/azure/account#show):</span></span>

```azurecli
az account show --query [id] --output tsv
```

<span data-ttu-id="9b5d9-141">Bu iki komutlarının hello çıktısını hello sonraki adımda kullanın.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-141">You use hello output from these two commands in hello next step.</span></span>


## <a name="create-ansible-credentials-file"></a><span data-ttu-id="9b5d9-142">Ansible kimlik bilgileri dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="9b5d9-142">Create Ansible credentials file</span></span>
<span data-ttu-id="9b5d9-143">tooprovide tooAnsible kimlik bilgileri, ortam değişkenleri tanımlayın veya bir yerel kimlik bilgileri dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-143">tooprovide credentials tooAnsible, you define environment variables or create a local credentials file.</span></span> <span data-ttu-id="9b5d9-144">Hakkında daha fazla bilgi için bkz toodefine Ansible kimlik bilgileri, [kimlik bilgileri sağlama tooAzure modülleri](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span><span class="sxs-lookup"><span data-stu-id="9b5d9-144">For more information about how toodefine Ansible credentials, see [Providing Credentials tooAzure Modules](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules).</span></span> 

<span data-ttu-id="9b5d9-145">Bir geliştirme ortamı oluşturma bir *kimlik bilgileri* Ansible için VM konağınız üzerinde aşağıdaki gibi dosya:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-145">For a development environment, create a *credentials* file for Ansible on your host VM as follows:</span></span>

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

<span data-ttu-id="9b5d9-146">Merhaba *kimlik bilgileri* dosyasının kendisini hello abonelik kimliği bir hizmet sorumlusu oluşturma hello çıktı ile birleştirir.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-146">hello *credentials* file itself combines hello subscription ID with hello output of creating a service principal.</span></span> <span data-ttu-id="9b5d9-147">Merhaba önceki çıktı [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac) komuttur aynı hello sipariş için gerektiği şekilde *client_id*, *gizli*, ve *Kiracı* .</span><span class="sxs-lookup"><span data-stu-id="9b5d9-147">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *client_id*, *secret*, and *tenant*.</span></span> <span data-ttu-id="9b5d9-148">Örnek Hello *kimlik bilgileri* dosyasını hello önceki çıkış eşleşen bu değerleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-148">hello following example *credentials* file shows these values matching hello previous output.</span></span> <span data-ttu-id="9b5d9-149">Aşağıdaki gibi kendi değerlerinizi girin:</span><span class="sxs-lookup"><span data-stu-id="9b5d9-149">Enter your own values as follows:</span></span>

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a><span data-ttu-id="9b5d9-150">Ansible ortam değişkenlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="9b5d9-150">Use Ansible environment variables</span></span>
<span data-ttu-id="9b5d9-151">Ansible Kule ya da Jenkins gibi toouse araçları kullanacaksanız, ortam değişkenleri şu şekilde tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-151">If you are going toouse tools such as Ansible Tower or Jenkins, you can define environment variables as follows.</span></span> <span data-ttu-id="9b5d9-152">Bu değişkenler bir hizmet sorumlusu oluşturuluyor gelen hello çıktı hello abonelik kimliği birleştirin.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-152">These variables combine hello subscription ID with hello output from creating a service principal.</span></span> <span data-ttu-id="9b5d9-153">Merhaba önceki çıktı [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac) komuttur aynı hello sipariş için gerektiği şekilde *AZURE_CLIENT_ID*, *AZURE_SECRET*, ve *AZURE_ KİRACI*.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-153">Output from hello previous [az ad sp create-for-rbac](/cli/azure/ad/sp#create-for-rbac) command is hello same order as needed for *AZURE_CLIENT_ID*, *AZURE_SECRET*, and *AZURE_TENANT*.</span></span> 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a><span data-ttu-id="9b5d9-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9b5d9-154">Next steps</span></span>
<span data-ttu-id="9b5d9-155">Şimdi Ansible sahip ve hello Azure Python SDK'sını modülleri yüklü ve Ansible toouse için tanımlanmış kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="9b5d9-155">You now have Ansible and hello required Azure Python SDK modules installed, and credentials defined for Ansible toouse.</span></span> <span data-ttu-id="9b5d9-156">Nasıl çok öğrenin[Ansible ile bir VM oluşturma](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="9b5d9-156">Learn how too[create a VM with Ansible](ansible-create-vm.md).</span></span> <span data-ttu-id="9b5d9-157">Ayrıca çok nasıl öğrenebilirsiniz[tam bir Azure VM oluşturun ve Ansible kaynaklarla destekleyici](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="9b5d9-157">You can also learn how too[create a complete Azure VM and supporting resources with Ansible](ansible-create-complete-vm.md).</span></span>
