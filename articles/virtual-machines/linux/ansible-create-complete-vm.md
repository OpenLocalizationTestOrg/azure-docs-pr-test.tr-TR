---
title: aaaUse Ansible toocreate azure'da tam bir Linux VM | Microsoft Docs
description: "Bilgi nasıl toouse Ansible toocreate ve Azure tam bir Linux sanal makine ortamında yönetme"
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
ms.openlocfilehash: 970b0427f39fc23240f9faab868196ca4f444e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a><span data-ttu-id="2bbbd-103">Ansible ile azure'da eksiksiz bir Linux sanal makine ortamı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2bbbd-103">Create a complete Linux virtual machine environment in Azure with Ansible</span></span>
<span data-ttu-id="2bbbd-104">Ansible ortamınızda tooautomate hello dağıtım ve kaynakların yapılandırmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="2bbbd-105">Herhangi bir kaynağa olduğu gibi aynı Merhaba, da Ansible toomanage Azure'da sanal makineleri (VM'ler) kullanın.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="2bbbd-106">Bu makale size nasıl gösterir toocreate eksiksiz bir Linux ortamı ve Ansible kaynaklarla destekleme.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-106">This article shows you how toocreate a complete Linux environment and supporting resources with Ansible.</span></span> <span data-ttu-id="2bbbd-107">Ayrıca çok nasıl öğrenebilirsiniz[Ansible ile temel bir VM oluşturma](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2bbbd-107">You can also learn how too[Create a basic VM with Ansible](ansible-create-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="2bbbd-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2bbbd-108">Prerequisites</span></span>
<span data-ttu-id="2bbbd-109">toomanage Azure Ansible kaynaklarla, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="2bbbd-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="2bbbd-110">Ansible ve ana bilgisayar sisteminizde yüklü Azure Python SDK'sını modülleri hello.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="2bbbd-111">Ansible yüklemek [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), ve [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="2bbbd-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="2bbbd-112">Azure kimlik ve yapılandırılmış Ansible toouse bunları.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="2bbbd-113">Azure kimlik bilgileri oluşturun ve Ansible yapılandırın</span><span class="sxs-lookup"><span data-stu-id="2bbbd-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="2bbbd-114">Azure CLI Sürüm 2.0.4 veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="2bbbd-115">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="2bbbd-116">Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2bbbd-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="2bbbd-117">Aynı zamanda [bulut Kabuk](/azure/cloud-shell/quickstart) tarayıcınızdan.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-virtual-network"></a><span data-ttu-id="2bbbd-118">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="2bbbd-118">Create virtual network</span></span>
<span data-ttu-id="2bbbd-119">Merhaba Ansible playbook aşağıdaki bölümde adlı bir sanal ağ oluşturur *myVnet* hello içinde *10.0.0.0/16* adres alanı:</span><span class="sxs-lookup"><span data-stu-id="2bbbd-119">hello following section in an Ansible playbook creates a virtual network named *myVnet* in hello *10.0.0.0/16* address space:</span></span>

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

<span data-ttu-id="2bbbd-120">tooadd bir alt ağ, bölümden hello oluşturur adlı bir alt ağ *mySubnet* hello içinde *myVnet* sanal ağ:</span><span class="sxs-lookup"><span data-stu-id="2bbbd-120">tooadd a subnet, hello following section creates a subnet named *mySubnet* in hello *myVnet* virtual network:</span></span>

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a><span data-ttu-id="2bbbd-121">Ortak IP adresi oluştur</span><span class="sxs-lookup"><span data-stu-id="2bbbd-121">Create public IP address</span></span>
<span data-ttu-id="2bbbd-122">Merhaba Internet üzerinden tooaccess kaynakları oluşturun ve genel bir IP adresi tooyour VM atayın.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-122">tooaccess resources across hello Internet, create and assign a public IP address tooyour VM.</span></span> <span data-ttu-id="2bbbd-123">Merhaba Ansible playbook aşağıdaki bölümde oluşturur adlı ortak IP adresi *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="2bbbd-123">hello following section in an Ansible playbook creates a public IP address named *myPublicIP*:</span></span>

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a><span data-ttu-id="2bbbd-124">Ağ güvenlik grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="2bbbd-124">Create Network Security Group</span></span>
<span data-ttu-id="2bbbd-125">Ağ güvenlik grupları, VM ve ağ trafiğini hello akışını denetler.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-125">Network Security Groups control hello flow of network traffic in and out of your VM.</span></span> <span data-ttu-id="2bbbd-126">Merhaba Ansible playbook aşağıdaki bölümde adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup* ve TCP bağlantı noktası 22 kuralı tooallow SSH trafiği tanımlar:</span><span class="sxs-lookup"><span data-stu-id="2bbbd-126">hello following section in an Ansible playbook creates a network security group named *myNetworkSecurityGroup* and defines a rule tooallow SSH traffic on TCP port 22:</span></span>

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


## <a name="create-virtual-network-interface-card"></a><span data-ttu-id="2bbbd-127">Sanal ağ arabirim kartı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2bbbd-127">Create virtual network interface card</span></span>
<span data-ttu-id="2bbbd-128">Bir sanal ağ arabirim kartı (NIC) verilen sanal ağ, genel IP adresi ve ağ güvenlik grubu, VM tooa bağlanır.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-128">A virtual network interface card (NIC) connects your VM tooa given virtual network, public IP address, and network security group.</span></span> <span data-ttu-id="2bbbd-129">Merhaba Ansible playbook aşağıdaki bölümde oluşturur adlı bir sanal NIC *myNIC* bağlı toohello sanal ağ kaynaklarını oluşturduğunuz:</span><span class="sxs-lookup"><span data-stu-id="2bbbd-129">hello following section in an Ansible playbook creates a virtual NIC named *myNIC* connected toohello virtual networking resources you have created:</span></span>

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


## <a name="create-virtual-machine"></a><span data-ttu-id="2bbbd-130">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="2bbbd-130">Create virtual machine</span></span>
<span data-ttu-id="2bbbd-131">Merhaba son adımı toocreate VM ve oluşturulan tüm hello kaynakları kullanın.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-131">hello final step is toocreate a VM and use all hello resources created.</span></span> <span data-ttu-id="2bbbd-132">Merhaba Ansible playbook aşağıdaki bölümde oluşturur adlı bir VM'den *myVM* ve ekler hello adlı bir sanal NIC *myNIC*.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-132">hello following section in an Ansible playbook creates a VM named *myVM* and attaches hello virtual NIC named *myNIC*.</span></span> <span data-ttu-id="2bbbd-133">Kendi ortak anahtar verileri hello girin *key_data* gibi eşleştirin:</span><span class="sxs-lookup"><span data-stu-id="2bbbd-133">Enter your own public key data in hello *key_data* pair as follows:</span></span>

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

## <a name="complete-ansible-playbook"></a><span data-ttu-id="2bbbd-134">Tam Ansible playbook</span><span class="sxs-lookup"><span data-stu-id="2bbbd-134">Complete Ansible playbook</span></span>
<span data-ttu-id="2bbbd-135">toobring bu bölümler birlikte adlı bir Ansible playbook oluşturma *azure_create_complete_vm.yml* ve Yapıştır hello aşağıdaki içeriği:</span><span class="sxs-lookup"><span data-stu-id="2bbbd-135">toobring all these sections together, create an Ansible playbook named *azure_create_complete_vm.yml* and paste hello following contents:</span></span>

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

<span data-ttu-id="2bbbd-136">Ansible tüm kaynaklarınızı içine bir kaynak grubu toodeploy gerekir.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-136">Ansible needs a resource group toodeploy all your resources into.</span></span> <span data-ttu-id="2bbbd-137">[az group create](/cli/azure/vm#create) ile bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-137">Create a resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="2bbbd-138">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="2bbbd-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="2bbbd-139">toocreate hello tam VM ortamıyla Ansible, hello playbook aşağıdaki gibi çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="2bbbd-139">toocreate hello complete VM environment with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_complete_vm.yml
```

<span data-ttu-id="2bbbd-140">Merhaba çıkış benzer toohello hello VM başarıyla oluşturulup oluşturulmadığını gösteren örnek aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="2bbbd-140">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2bbbd-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="2bbbd-141">Next steps</span></span>
<span data-ttu-id="2bbbd-142">Bu örnek hello gereken sanal ağ kaynakları içeren tam bir VM ortamı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2bbbd-142">This example creates a complete VM environment including hello required virtual networking resources.</span></span> <span data-ttu-id="2bbbd-143">Bir daha doğrudan örnek toocreate için varsayılan seçenekleri ile var olan ağ kaynaklarına içine bir VM, bkz: [bir VM oluşturma](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="2bbbd-143">For a more direct example toocreate a VM into existing network resources with default options, see [Create a VM](ansible-create-vm.md).</span></span>
