---
title: "Tam bir Linux VM oluşturmak için Ansible kullanın | Microsoft Docs"
description: "Ansible azure'da tam bir Linux sanal makine ortamı oluşturmak ve yönetmek için nasıl kullanılacağını öğrenin"
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
ms.openlocfilehash: b2fcc288b40c12a9b3f966156ee2eedf4acca313
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a><span data-ttu-id="04693-103">Ansible ile azure'da eksiksiz bir Linux sanal makine ortamı oluşturma</span><span class="sxs-lookup"><span data-stu-id="04693-103">Create a complete Linux virtual machine environment in Azure with Ansible</span></span>
<span data-ttu-id="04693-104">Ansible dağıtma ve yapılandırmanın ortamınızdaki kaynakların otomatikleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="04693-104">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="04693-105">Azure, aynı herhangi bir kaynağa olduğu gibi sanal makineleri (VM'ler) yönetmek için Ansible kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04693-105">You can use Ansible to manage your virtual machines (VMs) in Azure, the same as you would any other resource.</span></span> <span data-ttu-id="04693-106">Bu makalede eksiksiz bir Linux ortamı ve Ansible kaynaklarla destekleme nasıl oluşturulacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="04693-106">This article shows you how to create a complete Linux environment and supporting resources with Ansible.</span></span> <span data-ttu-id="04693-107">Ayrıca öğrenebilirsiniz nasıl [Ansible ile temel bir VM oluşturma](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="04693-107">You can also learn how to [Create a basic VM with Ansible](ansible-create-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="04693-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="04693-108">Prerequisites</span></span>
<span data-ttu-id="04693-109">Ansible ile Azure kaynaklarınızı yönetmek için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="04693-109">To manage Azure resources with Ansible, you need the following:</span></span>

- <span data-ttu-id="04693-110">Ansible ve ana bilgisayar sisteminizde yüklü Azure Python SDK'sını modüller.</span><span class="sxs-lookup"><span data-stu-id="04693-110">Ansible and the Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="04693-111">Ansible yüklemek [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), ve [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="04693-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="04693-112">Azure kimlik ve onları kullanmak üzere yapılandırılmış Ansible.</span><span class="sxs-lookup"><span data-stu-id="04693-112">Azure credentials, and Ansible configured to use them.</span></span>
    - [<span data-ttu-id="04693-113">Azure kimlik bilgileri oluşturun ve Ansible yapılandırın</span><span class="sxs-lookup"><span data-stu-id="04693-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="04693-114">Azure CLI Sürüm 2.0.4 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="04693-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="04693-115">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="04693-115">Run `az --version` to find the version.</span></span> 
    - <span data-ttu-id="04693-116">Yükseltme gerekiyorsa, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="04693-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="04693-117">Aynı zamanda [bulut Kabuk](/azure/cloud-shell/quickstart) tarayıcınızdan.</span><span class="sxs-lookup"><span data-stu-id="04693-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-virtual-network"></a><span data-ttu-id="04693-118">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="04693-118">Create virtual network</span></span>
<span data-ttu-id="04693-119">Aşağıdaki bölümde Ansible playbook adlı bir sanal ağ oluşturur *myVnet* içinde *10.0.0.0/16* adres alanı:</span><span class="sxs-lookup"><span data-stu-id="04693-119">The following section in an Ansible playbook creates a virtual network named *myVnet* in the *10.0.0.0/16* address space:</span></span>

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

<span data-ttu-id="04693-120">Bir alt ağı eklemek için aşağıdaki bölümde adlı bir alt ağı oluşturur *mySubnet* içinde *myVnet* sanal ağ:</span><span class="sxs-lookup"><span data-stu-id="04693-120">To add a subnet, the following section creates a subnet named *mySubnet* in the *myVnet* virtual network:</span></span>

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a><span data-ttu-id="04693-121">Ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="04693-121">Create public IP address</span></span>
<span data-ttu-id="04693-122">Internet'te kaynaklara erişmek için oluşturmak ve VM'nize genel bir IP adresi atayın.</span><span class="sxs-lookup"><span data-stu-id="04693-122">To access resources across the Internet, create and assign a public IP address to your VM.</span></span> <span data-ttu-id="04693-123">Aşağıdaki bölümde Ansible playbook adlı ortak IP adresi oluşturur *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="04693-123">The following section in an Ansible playbook creates a public IP address named *myPublicIP*:</span></span>

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a><span data-ttu-id="04693-124">Ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="04693-124">Create Network Security Group</span></span>
<span data-ttu-id="04693-125">Ağ güvenlik grupları, VM ve ağ trafiği akışını denetler.</span><span class="sxs-lookup"><span data-stu-id="04693-125">Network Security Groups control the flow of network traffic in and out of your VM.</span></span> <span data-ttu-id="04693-126">Aşağıdaki bölümde Ansible playbook adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup* ve TCP bağlantı noktası 22 SSH trafiğine izin verecek bir kural tanımlar:</span><span class="sxs-lookup"><span data-stu-id="04693-126">The following section in an Ansible playbook creates a network security group named *myNetworkSecurityGroup* and defines a rule to allow SSH traffic on TCP port 22:</span></span>

```yaml
- name: Create Network Security Group that allows SSH
  azure_rm_securitygroup:
    resource_group: myResourceGroup
    name: myNetworkSecurityGroup
    rules:
      - name: SSH
        protocol: TCP
        destination_port_range: 22
        access: Allow
        priority: 1001
        direction: Inbound
```


## <a name="create-virtual-network-interface-card"></a><span data-ttu-id="04693-127">Sanal ağ arabirim kartı oluşturma</span><span class="sxs-lookup"><span data-stu-id="04693-127">Create virtual network interface card</span></span>
<span data-ttu-id="04693-128">Bir sanal ağ arabirim kartı (NIC), VM verilen sanal ağ, genel IP adresi ve ağ güvenlik grubu bağlanır.</span><span class="sxs-lookup"><span data-stu-id="04693-128">A virtual network interface card (NIC) connects your VM to a given virtual network, public IP address, and network security group.</span></span> <span data-ttu-id="04693-129">Adlı bir sanal NIC Ansible playbook aşağıdaki bölümde oluşturur *myNIC* oluşturduğunuz sanal ağ kaynaklarına bağlı:</span><span class="sxs-lookup"><span data-stu-id="04693-129">The following section in an Ansible playbook creates a virtual NIC named *myNIC* connected to the virtual networking resources you have created:</span></span>

```yaml
- name: Create virtual network inteface card
  azure_rm_networkinterface:
    resource_group: myResourceGroup
    name: myNIC
    virtual_network: myVnet
    subnet: mySubnet
    public_ip_name: myPublicIP
    security_group: myNetworkSecurityGroup
```


## <a name="create-virtual-machine"></a><span data-ttu-id="04693-130">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="04693-130">Create virtual machine</span></span>
<span data-ttu-id="04693-131">Son adım, bir VM oluşturun ve oluşturulan tüm kaynakları kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="04693-131">The final step is to create a VM and use all the resources created.</span></span> <span data-ttu-id="04693-132">Adlı bir VM'den Ansible playbook aşağıdaki bölümde oluşturur *myVM* ve adlı bir sanal NIC ekler *myNIC*.</span><span class="sxs-lookup"><span data-stu-id="04693-132">The following section in an Ansible playbook creates a VM named *myVM* and attaches the virtual NIC named *myNIC*.</span></span> <span data-ttu-id="04693-133">Kendi ortak anahtar verilerde *key_data* gibi eşleştirin:</span><span class="sxs-lookup"><span data-stu-id="04693-133">Enter your own public key data in the *key_data* pair as follows:</span></span>

```yaml
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
    network_interfaces: myNIC
    image:
      offer: CentOS
      publisher: OpenLogic
      sku: '7.3'
      version: latest
```

## <a name="complete-ansible-playbook"></a><span data-ttu-id="04693-134">Tam Ansible playbook</span><span class="sxs-lookup"><span data-stu-id="04693-134">Complete Ansible playbook</span></span>
<span data-ttu-id="04693-135">Bu bölümler araya getirmek için adlı bir Ansible playbook oluşturma *azure_create_complete_vm.yml* ve aşağıdaki içeriği yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="04693-135">To bring all these sections together, create an Ansible playbook named *azure_create_complete_vm.yml* and paste the following contents:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create virtual network
    azure_rm_virtualnetwork:
      resource_group: myResourceGroup
      name: myVnet
      address_prefixes: "10.0.0.0/16"
  - name: Add subnet
    azure_rm_subnet:
      resource_group: myResourceGroup
      name: mySubnet
      address_prefix: "10.0.1.0/24"
      virtual_network: myVnet
  - name: Create public IP address
    azure_rm_publicipaddress:
      resource_group: myResourceGroup
      allocation_method: Static
      name: myPublicIP
  - name: Create Network Security Group that allows SSH
    azure_rm_securitygroup:
      resource_group: myResourceGroup
      name: myNetworkSecurityGroup
      rules:
        - name: SSH
          protocol: Tcp
          destination_port_range: 22
          access: Allow
          priority: 1001
          direction: Inbound
  - name: Create virtual network inteface card
    azure_rm_networkinterface:
      resource_group: myResourceGroup
      name: myNIC
      virtual_network: myVnet
      subnet: mySubnet
      public_ip_name: myPublicIP
      security_group: myNetworkSecurityGroup
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
      network_interfaces: myNIC
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="04693-136">Ansible içine tüm kaynaklarınızı dağıtmak için bir kaynak grubu gerekir.</span><span class="sxs-lookup"><span data-stu-id="04693-136">Ansible needs a resource group to deploy all your resources into.</span></span> <span data-ttu-id="04693-137">[az group create](/cli/azure/vm#create) ile bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="04693-137">Create a resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="04693-138">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroup* içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="04693-138">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="04693-139">Ansible ile tam VM ortamı oluşturmak için playbook aşağıdaki gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="04693-139">To create the complete VM environment with Ansible, run the playbook as follows:</span></span>

```bash
ansible-playbook azure_create_complete_vm.yml
```

<span data-ttu-id="04693-140">Çıktı VM başarıyla oluşturulup oluşturulmadığını gösteren aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="04693-140">The output looks similar to the following example that shows the VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create virtual network] *********************************************
changed: [localhost]

TASK [Add subnet] *********************************************************
changed: [localhost]

TASK [Create public IP address] *******************************************
changed: [localhost]

TASK [Create Network Security Group that allows SSH] **********************
changed: [localhost]

TASK [Create virtual network inteface card] *******************************
changed: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=7    changed=6    unreachable=0    failed=0
```

## <a name="next-steps"></a><span data-ttu-id="04693-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="04693-141">Next steps</span></span>
<span data-ttu-id="04693-142">Bu örnek, gerekli sanal ağ kaynakları içeren tam bir VM ortamı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="04693-142">This example creates a complete VM environment including the required virtual networking resources.</span></span> <span data-ttu-id="04693-143">Var olan ağ kaynaklarına varsayılan seçeneklerle içine bir VM oluşturmak daha doğrudan örnek için bkz [bir VM oluşturma](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="04693-143">For a more direct example to create a VM into existing network resources with default options, see [Create a VM](ansible-create-vm.md).</span></span>