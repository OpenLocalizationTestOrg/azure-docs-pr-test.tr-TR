---
title: aaaUse Ansible toocreate azure'da temel bir Linux VM | Microsoft Docs
description: "Bilgi nasıl toouse Ansible toocreate ve temel Linux sanal makine azure'da yönetin"
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
ms.openlocfilehash: ffe278b3f846924ff9c4d026120565146f951152
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="142f1-103">Azure Ansible ile temel bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="142f1-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="142f1-104">Ansible ortamınızda tooautomate hello dağıtım ve kaynakların yapılandırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="142f1-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="142f1-105">Herhangi bir kaynağa olduğu gibi aynı Merhaba, da Ansible toomanage Azure'da sanal makineleri (VM'ler) kullanın.</span><span class="sxs-lookup"><span data-stu-id="142f1-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="142f1-106">Bu makale size nasıl gösterir toocreate Ansible ile temel bir VM.</span><span class="sxs-lookup"><span data-stu-id="142f1-106">This article shows you how toocreate a basic VM with Ansible.</span></span> <span data-ttu-id="142f1-107">Ayrıca çok nasıl öğrenebilirsiniz[Ansible ile eksiksiz bir VM ortamı oluşturma](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="142f1-107">You can also learn how too[Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="142f1-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="142f1-108">Prerequisites</span></span>
<span data-ttu-id="142f1-109">toomanage Azure Ansible kaynaklarla, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="142f1-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="142f1-110">Ansible ve ana bilgisayar sisteminizde yüklü Azure Python SDK'sını modülleri hello.</span><span class="sxs-lookup"><span data-stu-id="142f1-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="142f1-111">Ansible yüklemek [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), ve [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="142f1-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="142f1-112">Azure kimlik ve yapılandırılmış Ansible toouse bunları.</span><span class="sxs-lookup"><span data-stu-id="142f1-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="142f1-113">Azure kimlik bilgileri oluşturun ve Ansible yapılandırın</span><span class="sxs-lookup"><span data-stu-id="142f1-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="142f1-114">Azure CLI Sürüm 2.0.4 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="142f1-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="142f1-115">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="142f1-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="142f1-116">Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="142f1-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="142f1-117">Aynı zamanda [bulut Kabuk](/azure/cloud-shell/quickstart) tarayıcınızdan.</span><span class="sxs-lookup"><span data-stu-id="142f1-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="142f1-118">Azure kaynaklarını destekleyen oluşturma</span><span class="sxs-lookup"><span data-stu-id="142f1-118">Create supporting Azure resources</span></span>
<span data-ttu-id="142f1-119">Bu örnekte, var olan bir altyapısının bir VM dağıtır bir runbook oluşturun.</span><span class="sxs-lookup"><span data-stu-id="142f1-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="142f1-120">İlk olarak, kaynak grubu ile oluşturma [az grubu oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="142f1-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="142f1-121">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="142f1-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="142f1-122">İle VM için sanal ağ oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="142f1-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="142f1-123">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* ve adlı bir alt ağ *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="142f1-123">hello following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="142f1-124">Oluşturma ve Ansible playbook çalıştırma</span><span class="sxs-lookup"><span data-stu-id="142f1-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="142f1-125">Adlı bir Ansible playbook oluşturma **azure_create_vm.yml** ve Yapıştır hello aşağıdaki içeriği.</span><span class="sxs-lookup"><span data-stu-id="142f1-125">Create an Ansible playbook named **azure_create_vm.yml** and paste hello following contents.</span></span> <span data-ttu-id="142f1-126">Bu örnek, tek bir VM'ye oluşturur ve SSH kimlik bilgilerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="142f1-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="142f1-127">Kendi ortak anahtar verileri hello girin *key_data* gibi eşleştirin:</span><span class="sxs-lookup"><span data-stu-id="142f1-127">Enter your own public key data in hello *key_data* pair as follows:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="142f1-128">toocreate hello VM ile Ansible, hello playbook aşağıdaki gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="142f1-128">toocreate hello VM with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="142f1-129">Merhaba çıkış benzer toohello hello VM başarıyla oluşturulup oluşturulmadığını gösteren örnek aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="142f1-129">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="142f1-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="142f1-130">Next steps</span></span>
<span data-ttu-id="142f1-131">Bu örnek bir VM varolan bir kaynak grubu ve dağıtılmış bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="142f1-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="142f1-132">Konusunda daha ayrıntılı bir örnek için bir sanal ağ ve ağ güvenlik grubu kuralları gibi toouse Ansible toocreate destekleyici kaynakları bkz [Ansible ile eksiksiz bir VM ortamı oluşturma](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="142f1-132">For a more detailed example on how toouse Ansible toocreate supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>
