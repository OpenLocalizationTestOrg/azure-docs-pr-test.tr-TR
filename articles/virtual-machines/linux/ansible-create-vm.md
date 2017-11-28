---
title: "Temel bir Linux VM oluşturmak için Ansible kullanın | Microsoft Docs"
description: "Ansible oluşturmak ve azure'da temel bir Linux sanal makine yönetmek için nasıl kullanılacağını öğrenin"
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
ms.openlocfilehash: 526f3522334450564500c4ba0e401a683cae55f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="25576-103">Azure Ansible ile temel bir sanal makine oluşturun</span><span class="sxs-lookup"><span data-stu-id="25576-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="25576-104">Ansible dağıtma ve yapılandırmanın ortamınızdaki kaynakların otomatikleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="25576-104">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="25576-105">Azure, aynı herhangi bir kaynağa olduğu gibi sanal makineleri (VM'ler) yönetmek için Ansible kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="25576-105">You can use Ansible to manage your virtual machines (VMs) in Azure, the same as you would any other resource.</span></span> <span data-ttu-id="25576-106">Bu makalede Ansible ile temel bir VM oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="25576-106">This article shows you how to create a basic VM with Ansible.</span></span> <span data-ttu-id="25576-107">Ayrıca öğrenebilirsiniz nasıl [Ansible ile eksiksiz bir VM ortamı oluşturma](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="25576-107">You can also learn how to [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="25576-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="25576-108">Prerequisites</span></span>
<span data-ttu-id="25576-109">Ansible ile Azure kaynaklarınızı yönetmek için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="25576-109">To manage Azure resources with Ansible, you need the following:</span></span>

- <span data-ttu-id="25576-110">Ansible ve ana bilgisayar sisteminizde yüklü Azure Python SDK'sını modüller.</span><span class="sxs-lookup"><span data-stu-id="25576-110">Ansible and the Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="25576-111">Ansible yüklemek [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), ve [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="25576-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="25576-112">Azure kimlik ve onları kullanmak üzere yapılandırılmış Ansible.</span><span class="sxs-lookup"><span data-stu-id="25576-112">Azure credentials, and Ansible configured to use them.</span></span>
    - [<span data-ttu-id="25576-113">Azure kimlik bilgileri oluşturun ve Ansible yapılandırın</span><span class="sxs-lookup"><span data-stu-id="25576-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="25576-114">Azure CLI Sürüm 2.0.4 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="25576-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="25576-115">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="25576-115">Run `az --version` to find the version.</span></span> 
    - <span data-ttu-id="25576-116">Yükseltme gerekiyorsa, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="25576-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="25576-117">Aynı zamanda [bulut Kabuk](/azure/cloud-shell/quickstart) tarayıcınızdan.</span><span class="sxs-lookup"><span data-stu-id="25576-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="25576-118">Azure kaynaklarını destekleyen oluşturma</span><span class="sxs-lookup"><span data-stu-id="25576-118">Create supporting Azure resources</span></span>
<span data-ttu-id="25576-119">Bu örnekte, var olan bir altyapısının bir VM dağıtır bir runbook oluşturun.</span><span class="sxs-lookup"><span data-stu-id="25576-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="25576-120">İlk olarak, kaynak grubu ile oluşturma [az grubu oluşturma](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="25576-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="25576-121">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroup* içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="25576-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="25576-122">İle VM için sanal ağ oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="25576-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="25576-123">Aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* ve adlı bir alt ağ *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="25576-123">The following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="25576-124">Oluşturma ve Ansible playbook çalıştırma</span><span class="sxs-lookup"><span data-stu-id="25576-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="25576-125">Adlı bir Ansible playbook oluşturma **azure_create_vm.yml** ve aşağıdaki içeriğini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="25576-125">Create an Ansible playbook named **azure_create_vm.yml** and paste the following contents.</span></span> <span data-ttu-id="25576-126">Bu örnek, tek bir VM'ye oluşturur ve SSH kimlik bilgilerini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="25576-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="25576-127">Kendi ortak anahtar verilerde *key_data* gibi eşleştirin:</span><span class="sxs-lookup"><span data-stu-id="25576-127">Enter your own public key data in the *key_data* pair as follows:</span></span>

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

<span data-ttu-id="25576-128">VM ile Ansible oluşturmak için playbook aşağıdaki gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="25576-128">To create the VM with Ansible, run the playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="25576-129">Çıktı VM başarıyla oluşturulup oluşturulmadığını gösteren aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="25576-129">The output looks similar to the following example that shows the VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="25576-130">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="25576-130">Next steps</span></span>
<span data-ttu-id="25576-131">Bu örnek bir VM varolan bir kaynak grubu ve dağıtılmış bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="25576-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="25576-132">Bir sanal ağ ve ağ güvenlik grubu kuralları gibi destekleyici kaynakları oluşturmak için Ansible kullanma hakkında daha ayrıntılı bir örnek için bkz: [Ansible ile eksiksiz bir VM ortamı oluşturma](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="25576-132">For a more detailed example on how to use Ansible to create supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>