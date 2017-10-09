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
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a>Azure Ansible ile temel bir sanal makine oluşturun
Ansible ortamınızda tooautomate hello dağıtım ve kaynakların yapılandırmasını sağlar. Herhangi bir kaynağa olduğu gibi aynı Merhaba, da Ansible toomanage Azure'da sanal makineleri (VM'ler) kullanın. Bu makale size nasıl gösterir toocreate Ansible ile temel bir VM. Ayrıca çok nasıl öğrenebilirsiniz[Ansible ile eksiksiz bir VM ortamı oluşturma](ansible-create-complete-vm.md).


## <a name="prerequisites"></a>Ön koşullar
toomanage Azure Ansible kaynaklarla, aşağıdaki hello gerekir:

- Ansible ve ana bilgisayar sisteminizde yüklü Azure Python SDK'sını modülleri hello.
    - Ansible yüklemek [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), ve [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)
- Azure kimlik ve yapılandırılmış Ansible toouse bunları.
    - [Azure kimlik bilgileri oluşturun ve Ansible yapılandırın](ansible-install-configure.md#create-azure-credentials)
- Azure CLI Sürüm 2.0.4 veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. 
    - Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). Aynı zamanda [bulut Kabuk](/azure/cloud-shell/quickstart) tarayıcınızdan.


## <a name="create-supporting-azure-resources"></a>Azure kaynaklarını destekleyen oluşturma
Bu örnekte, var olan bir altyapısının bir VM dağıtır bir runbook oluşturun. İlk olarak, kaynak grubu ile oluşturma [az grubu oluşturma](/cli/azure/vm#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:

```azurecli
az group create --name myResourceGroup --location eastus
```

İle VM için sanal ağ oluşturma [az ağ vnet oluşturma](/cli/azure/network/vnet#create). Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet* ve adlı bir alt ağ *mySubnet*:

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a>Oluşturma ve Ansible playbook çalıştırma
Adlı bir Ansible playbook oluşturma **azure_create_vm.yml** ve Yapıştır hello aşağıdaki içeriği. Bu örnek, tek bir VM'ye oluşturur ve SSH kimlik bilgilerini yapılandırır. Kendi ortak anahtar verileri hello girin *key_data* gibi eşleştirin:

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

toocreate hello VM ile Ansible, hello playbook aşağıdaki gibi çalıştırın:

```bash
ansible-playbook azure_create_vm.yml
```

Merhaba çıkış benzer toohello hello VM başarıyla oluşturulup oluşturulmadığını gösteren örnek aşağıdaki gibidir:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a>Sonraki adımlar
Bu örnek bir VM varolan bir kaynak grubu ve dağıtılmış bir sanal ağ oluşturur. Konusunda daha ayrıntılı bir örnek için bir sanal ağ ve ağ güvenlik grubu kuralları gibi toouse Ansible toocreate destekleyici kaynakları bkz [Ansible ile eksiksiz bir VM ortamı oluşturma](ansible-create-complete-vm.md).
