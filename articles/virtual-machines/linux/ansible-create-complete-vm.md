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
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a>Ansible ile azure'da eksiksiz bir Linux sanal makine ortamı oluşturma
Ansible ortamınızda tooautomate hello dağıtım ve kaynakların yapılandırmasını sağlar. Herhangi bir kaynağa olduğu gibi aynı Merhaba, da Ansible toomanage Azure'da sanal makineleri (VM'ler) kullanın. Bu makale size nasıl gösterir toocreate eksiksiz bir Linux ortamı ve Ansible kaynaklarla destekleme. Ayrıca çok nasıl öğrenebilirsiniz[Ansible ile temel bir VM oluşturma](ansible-create-vm.md).


## <a name="prerequisites"></a>Ön koşullar
toomanage Azure Ansible kaynaklarla, aşağıdaki hello gerekir:

- Ansible ve ana bilgisayar sisteminizde yüklü Azure Python SDK'sını modülleri hello.
    - Ansible yüklemek [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), ve [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)
- Azure kimlik ve yapılandırılmış Ansible toouse bunları.
    - [Azure kimlik bilgileri oluşturun ve Ansible yapılandırın](ansible-install-configure.md#create-azure-credentials)
- Azure CLI Sürüm 2.0.4 veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. 
    - Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). Aynı zamanda [bulut Kabuk](/azure/cloud-shell/quickstart) tarayıcınızdan.


## <a name="create-virtual-network"></a>Sanal ağ oluşturma
Merhaba Ansible playbook aşağıdaki bölümde adlı bir sanal ağ oluşturur *myVnet* hello içinde *10.0.0.0/16* adres alanı:

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

tooadd bir alt ağ, bölümden hello oluşturur adlı bir alt ağ *mySubnet* hello içinde *myVnet* sanal ağ:

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a>Ortak IP adresi oluştur
Merhaba Internet üzerinden tooaccess kaynakları oluşturun ve genel bir IP adresi tooyour VM atayın. Merhaba Ansible playbook aşağıdaki bölümde oluşturur adlı ortak IP adresi *myPublicIP*:

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a>Ağ güvenlik grubu oluşturun
Ağ güvenlik grupları, VM ve ağ trafiğini hello akışını denetler. Merhaba Ansible playbook aşağıdaki bölümde adlı bir ağ güvenlik grubu oluşturur *myNetworkSecurityGroup* ve TCP bağlantı noktası 22 kuralı tooallow SSH trafiği tanımlar:

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


## <a name="create-virtual-network-interface-card"></a>Sanal ağ arabirim kartı oluşturma
Bir sanal ağ arabirim kartı (NIC) verilen sanal ağ, genel IP adresi ve ağ güvenlik grubu, VM tooa bağlanır. Merhaba Ansible playbook aşağıdaki bölümde oluşturur adlı bir sanal NIC *myNIC* bağlı toohello sanal ağ kaynaklarını oluşturduğunuz:

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


## <a name="create-virtual-machine"></a>Sanal makine oluşturma
Merhaba son adımı toocreate VM ve oluşturulan tüm hello kaynakları kullanın. Merhaba Ansible playbook aşağıdaki bölümde oluşturur adlı bir VM'den *myVM* ve ekler hello adlı bir sanal NIC *myNIC*. Kendi ortak anahtar verileri hello girin *key_data* gibi eşleştirin:

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

## <a name="complete-ansible-playbook"></a>Tam Ansible playbook
toobring bu bölümler birlikte adlı bir Ansible playbook oluşturma *azure_create_complete_vm.yml* ve Yapıştır hello aşağıdaki içeriği:

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

Ansible tüm kaynaklarınızı içine bir kaynak grubu toodeploy gerekir. [az group create](/cli/azure/vm#create) ile bir kaynak grubu oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:

```azurecli
az group create --name myResourceGroup --location eastus
```

toocreate hello tam VM ortamıyla Ansible, hello playbook aşağıdaki gibi çalıştırın:

```bash
ansible-playbook azure_create_complete_vm.yml
```

Merhaba çıkış benzer toohello hello VM başarıyla oluşturulup oluşturulmadığını gösteren örnek aşağıdaki gibidir:

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

## <a name="next-steps"></a>Sonraki adımlar
Bu örnek hello gereken sanal ağ kaynakları içeren tam bir VM ortamı oluşturur. Bir daha doğrudan örnek toocreate için varsayılan seçenekleri ile var olan ağ kaynaklarına içine bir VM, bkz: [bir VM oluşturma](ansible-create-vm.md).
