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
# <a name="install-and-configure-ansible-toomanage-virtual-machines-in-azure"></a>Yükleme ve Azure'da Ansible toomanage sanal makineleri yapılandırma
Bu makalede, en yaygın Linux distro'lar tooinstall Ansible ve bazı için gerekli Azure Python SDK'sını modüllerini nasıl hello ayrıntıları. Ansible diğer distro'lar üzerinde yüklü hello paketleri toofit ayarlayarak belirli platformunuz yükleyebilirsiniz. toocreate Azure da bilgi kaynaklarına güvenli bir şekilde nasıl toocreate ve Ansible toouse bilgilerini tanımlayın. 

Daha fazla yükleme seçenekleri ve ek platformlar için adımlar için hello bkz [Ansible Yükleme Kılavuzu](https://docs.ansible.com/ansible/intro_installation.html).


## <a name="install-ansible"></a>Ansible yükleyin
İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupAnsible* hello içinde *eastus* konumu:

```azurecli
az group create --name myResourceGroupAnsible --location eastus
```

Şimdi bir VM oluşturun ve Ansible distro'lar aşağıdaki hello biri için yükleyin:

- [Ubuntu 16.04 LTS](#ubuntu1604-lts)
- [CentOS 7.3](#centos-73)
- [SLES 12.2 SP2](#sles-122-sp2)

### <a name="ubuntu-1604-lts"></a>Ubuntu 16.04 LTS
[az vm create](/cli/azure/vm#create) ile bir VM oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH VM tooyour kullanarak hello `publicIpAddress` hello not ettiğiniz hello VM çıktısını oluşturma işlemi:

```bash
ssh azureuser@<publicIpAddress>
```

VM'nizi üzerinde hello Azure Python SDK'sını modülleri ve Ansible hello gerekli paketleri gibi yükleyin:

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

Artık çok geçmek[oluşturma Azure kimlik bilgilerini](#create-azure-credentials).


### <a name="centos-73"></a>CentOS 7.3
[az vm create](/cli/azure/vm#create) ile bir VM oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH VM tooyour kullanarak hello `publicIpAddress` hello not ettiğiniz hello VM çıktısını oluşturma işlemi:

```bash
ssh azureuser@<publicIpAddress>
```

VM'nizi üzerinde hello Azure Python SDK'sını modülleri ve Ansible hello gerekli paketleri gibi yükleyin:

```bash
## Install pre-requisite packages
sudo yum check-update; sudo yum install -y gcc libffi-devel python-devel openssl-devel epel-release
sudo yum install -y python-pip python-wheel

## Install Azure SDKs via pip
sudo pip install "azure==2.0.0rc5" msrestazure

## Install Ansible via yum
sudo yum install -y ansible
```

Artık çok geçmek[oluşturma Azure kimlik bilgilerini](#create-azure-credentials).


### <a name="sles-122-sp2"></a>SLES 12.2 SP2
[az vm create](/cli/azure/vm#create) ile bir VM oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVMAnsible*:

```bash
az vm create \
    --name myVMAnsible \
    --resource-group myResourceGroupAnsible \
    --image SLES \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH VM tooyour kullanarak hello `publicIpAddress` hello not ettiğiniz hello VM çıktısını oluşturma işlemi:

```bash
ssh azureuser@<publicIpAddress>
```

VM'nizi üzerinde hello Azure Python SDK'sını modülleri ve Ansible hello gerekli paketleri gibi yükleyin:

```bash
## Install pre-requisite packages
sudo zypper refresh && sudo zypper --non-interactive install gcc libffi-devel-gcc5 python-devel \
    libopenssl-devel python-pip python-setuptools python-azure-sdk

## Install Ansible via zypper
sudo zypper addrepo http://download.opensuse.org/repositories/systemsmanagement/SLE_12_SP2/systemsmanagement.repo
sudo zypper refresh && sudo zypper install ansible
```

Artık çok geçmek[oluşturma Azure kimlik bilgilerini](#create-azure-credentials).


## <a name="create-azure-credentials"></a>Azure kimlik bilgileri oluşturun
Ansible bir kullanıcı adı ve parola veya bir hizmet sorumlusu kullanarak Azure ile iletişim kurar. Bir Azure hizmet sorumlusu uygulamaları, hizmetleri ve Ansible gibi Otomasyon araçları ile birlikte kullanabileceğiniz bir güvenlik kimliğidir. Denetim ve toowhat işlemleri hello hizmet sorumlusu Azure'da gerçekleştirebilirsiniz gibi hello izinleri tanımlayın. yalnızca bir kullanıcı adı ve parola sağlayarak tooimprove güvenliği, bu örnek temel bir hizmet sorumlusu oluşturur.

Bir hizmet sorumlusu ile oluşturma [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac) ve Ansible gereken çıktı hello kimlik bilgileri:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Komutları önceki hello hello çıktının bir örnek aşağıdaki gibidir:

```json
[
  "eec5624a-90f8-4386-8a87-02730b5410d5",
  "531dcffa-3aff-4488-99bb-4816c395ea3f",
  "72f988bf-86f1-41af-91ab-2d7cd011db47"
]
```

tooauthenticate tooAzure etmeniz, Azure aboneliğinizin kimliği ile tooobtain [az hesabı Göster](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Bu iki komutlarının hello çıktısını hello sonraki adımda kullanın.


## <a name="create-ansible-credentials-file"></a>Ansible kimlik bilgileri dosyası oluşturma
tooprovide tooAnsible kimlik bilgileri, ortam değişkenleri tanımlayın veya bir yerel kimlik bilgileri dosyası oluşturun. Hakkında daha fazla bilgi için bkz toodefine Ansible kimlik bilgileri, [kimlik bilgileri sağlama tooAzure modülleri](https://docs.ansible.com/ansible/guide_azure.html#providing-credentials-to-azure-modules). 

Bir geliştirme ortamı oluşturma bir *kimlik bilgileri* Ansible için VM konağınız üzerinde aşağıdaki gibi dosya:

```bash
mkdir ~/.azure
vi ~/.azure/credentials
```

Merhaba *kimlik bilgileri* dosyasının kendisini hello abonelik kimliği bir hizmet sorumlusu oluşturma hello çıktı ile birleştirir. Merhaba önceki çıktı [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac) komuttur aynı hello sipariş için gerektiği şekilde *client_id*, *gizli*, ve *Kiracı* . Örnek Hello *kimlik bilgileri* dosyasını hello önceki çıkış eşleşen bu değerleri gösterir. Aşağıdaki gibi kendi değerlerinizi girin:

```bash
[default]
subscription_id=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
client_id=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
secret=b8326643-f7e9-48fb-b0d5-952b68ab3def
tenant=72f988bf-86f1-41af-91ab-2d7cd011db47
```


## <a name="use-ansible-environment-variables"></a>Ansible ortam değişkenlerini kullanma
Ansible Kule ya da Jenkins gibi toouse araçları kullanacaksanız, ortam değişkenleri şu şekilde tanımlayabilirsiniz. Bu değişkenler bir hizmet sorumlusu oluşturuluyor gelen hello çıktı hello abonelik kimliği birleştirin. Merhaba önceki çıktı [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac) komuttur aynı hello sipariş için gerektiği şekilde *AZURE_CLIENT_ID*, *AZURE_SECRET*, ve *AZURE_ KİRACI*. 

```bash
export AZURE_SUBSCRIPTION_ID=xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
export AZURE_CLIENT_ID=66cf7166-dd13-40f9-bca2-3e9a43f2b3a4
export AZURE_SECRET=8326643-f7e9-48fb-b0d5-952b68ab3def
export AZURE_TENANT=72f988bf-86f1-41af-91ab-2d7cd011db47
```

## <a name="next-steps"></a>Sonraki adımlar
Şimdi Ansible sahip ve hello Azure Python SDK'sını modülleri yüklü ve Ansible toouse için tanımlanmış kimlik bilgileri gerekir. Nasıl çok öğrenin[Ansible ile bir VM oluşturma](ansible-create-vm.md). Ayrıca çok nasıl öğrenebilirsiniz[tam bir Azure VM oluşturun ve Ansible kaynaklarla destekleyici](ansible-create-complete-vm.md).
