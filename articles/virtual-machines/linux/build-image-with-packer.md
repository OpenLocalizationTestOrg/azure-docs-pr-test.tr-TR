---
title: "aaaHow toocreate Packer ile Linux Azure VM görüntüleri | Microsoft Docs"
description: "Bilgi nasıl toouse Packer toocreate görüntüleri Linux sanal makinelerinin Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/18/2017
ms.author: iainfou
ms.openlocfilehash: 5990598859e73efac477884bc8de5fd5138bf6e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-packer-toocreate-linux-virtual-machine-images-in-azure"></a>Azure'da nasıl toouse Packer toocreate Linux sanal makine görüntüleri
Her sanal makine (VM) azure'da hello Linux dağıtım ve işletim sistemi sürümü tanımlayan bir görüntüden oluşturulur. Görüntüleri, önceden yüklenmiş uygulamalar ve yapılandırmalar içerebilir. en yaygın dağıtımları ve uygulama ortamları için birçok ilk ve üçüncü taraf görüntüsü Hello Azure Marketi sağlar veya kendi özel görüntülerinizi uyarlanmış tooyour gereksinimlerini oluşturabilirsiniz. Bu makalede nasıl toouse hello açık kaynak aracı ayrıntıları [Packer](https://www.packer.io/) azure'da toodefine ve yapı özel görüntüler.


## <a name="create-azure-resource-group"></a>Azure kaynak grubu oluşturun
Merhaba kaynak VM derlemeler gibi hello oluşturma işlemi sırasında geçici Azure kaynaklarını Packer oluşturur. bir görüntü olarak kullanmak üzere VM kaynak toocapture, bir kaynak grubu tanımlamanız gerekir. Merhaba hello Packer oluşturma işleminin çıktısı bu kaynak grubunda depolanır.

[az group create](/cli/azure/group#create) ile bir kaynak grubu oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:

```azurecli
az group create -n myResourceGroup -l eastus
```


## <a name="create-azure-credentials"></a>Azure kimlik bilgileri oluşturun
Packer bir hizmet sorumlusu kullanarak Azure ile kimliğini doğrular. Bir Azure hizmet sorumlusu uygulamaları, hizmetleri ve Packer gibi Otomasyon araçları ile birlikte kullanabileceğiniz bir güvenlik kimliğidir. Denetim ve toowhat işlemleri hello hizmet sorumlusu Azure'da gerçekleştirebilirsiniz gibi hello izinleri tanımlayın.

Bir hizmet sorumlusu ile oluşturma [az ad sp oluşturma-için-rbac](/cli/azure/ad/sp#create-for-rbac) ve Packer gereken çıktı hello kimlik bilgileri:

```azurecli
az ad sp create-for-rbac --query [appId,password,tenant]
```

Komutları önceki hello hello çıktının bir örnek aşağıdaki gibidir:

```azurecli
"f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
"0e760437-bf34-4aad-9f8d-870be799c55d",
"72f988bf-86f1-41af-91ab-2d7cd011db47"
```

tooauthenticate tooAzure etmeniz, Azure aboneliğinizin kimliği ile tooobtain [az hesabı Göster](/cli/azure/account#show):

```azurecli
az account show --query [id] --output tsv
```

Bu iki komutlarının hello çıktısını hello sonraki adımda kullanın.


## <a name="define-packer-template"></a>Packer şablon oluştur
toobuild görüntüleri bir JSON dosyası olarak bir şablon oluşturun. Merhaba şablonunda hello gerçek taşımak provisioners derleme işlemi ve oluşturucular tanımlayın. Packer sahip bir [Azure sağlayıcısı](https://www.packer.io/docs/builders/azure.html) toodefine Azure sağlayan adım önceki hello oluşturulan hello hizmet asıl kimlik bilgileri gibi kaynaklar.

Adlı bir dosya oluşturun *ubuntu.json* ve Yapıştır hello aşağıdaki içeriği. Kendi değerlerinizi için hello aşağıdakileri girin:

| Parametre                           | Burada tooobtain |
|-------------------------------------|----------------------------------------------------|
| *client_id*                         | İlk satırı çıktısı `az ad sp` Oluştur komutu - *AppID* |
| *client_secret*                     | İkinci satır çıktısı `az ad sp` Oluştur komutu - *parola* |
| *tenant_id*                         | Üçüncü satır çıktısı `az ad sp` Oluştur komutu - *Kiracı* |
| *ABONELİK_KİMLİĞİ*                   | Çıktı `az account show` komutu |
| *managed_image_resource_group_name* | Merhaba ilk adımda oluşturduğunuz kaynak grubunun adı |
| *managed_image_name*                | Oluşturulan hello yönetilen disk görüntüsü için adı |


```json
{
  "builders": [{
    "type": "azure-arm",

    "client_id": "f5b6a5cf-fbdf-4a9f-b3b8-3c2cd00225a4",
    "client_secret": "0e760437-bf34-4aad-9f8d-870be799c55d",
    "tenant_id": "72f988bf-86f1-41af-91ab-2d7cd011db47",
    "subscription_id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx",

    "managed_image_resource_group_name": "myResourceGroup",
    "managed_image_name": "myPackerImage",

    "os_type": "Linux",
    "image_publisher": "Canonical",
    "image_offer": "UbuntuServer",
    "image_sku": "16.04-LTS",

    "azure_tags": {
        "dept": "Engineering",
        "task": "Image deployment"
    },

    "location": "East US",
    "vm_size": "Standard_DS2_v2"
  }],
  "provisioners": [{
    "execute_command": "chmod +x {{ .Path }}; {{ .Vars }} sudo -E sh '{{ .Path }}'",
    "inline": [
      "apt-get update",
      "apt-get upgrade -y",
      "apt-get -y install nginx",

      "/usr/sbin/waagent -force -deprovision+user && export HISTSIZE=0 && sync"
    ],
    "inline_shebang": "/bin/sh -x",
    "type": "shell"
  }]
}
```

Bu şablon bir Ubuntu 16.04 LTS görüntü oluşturur, NGINX yükler ve sonra hello VM deprovisions.

> [!NOTE]
> Bu şablon tooprovision kullanıcı kimlik bilgilerini genişletirseniz, Ayarla deprovisions Azure Aracısı tooread hello hello sağlayıcısı komutu `-deprovision` yerine `deprovision+user`.
> Merhaba `+user` bayrağını hello kaynak VM tüm kullanıcı hesaplarını kaldırır.


## <a name="build-packer-image"></a>Packer yansıması oluştur
Yerel makinenizde yüklü Packer zaten yoksa [hello Packer yükleme yönergelerini izleyin](https://www.packer.io/docs/install/index.html).

Merhaba görüntüsünü, Packer belirterek şablon dosyasını aşağıdaki gibi oluşturabilirsiniz:

```bash
./packer build ubuntu.json
```

Komutları önceki hello hello çıktının bir örnek aşağıdaki gibidir:

```bash
azure-arm output will be in this color.

==> azure-arm: Running builder ...
    azure-arm: Creating Azure Resource Manager (ARM) client ...
==> azure-arm: Creating resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Location          : ‘East US’
==> azure-arm:  -> Tags              :
==> azure-arm:  ->> dept : Engineering
==> azure-arm:  ->> task : Image deployment
==> azure-arm: Validating deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Deploying deployment template ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> DeploymentName    : ‘pkrdpswtxmqm7ly’
==> azure-arm: Getting hello VM’s IP address ...
==> azure-arm:  -> ResourceGroupName   : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> PublicIPAddressName : ‘packerPublicIP’
==> azure-arm:  -> NicName             : ‘packerNic’
==> azure-arm:  -> Network Connection  : ‘PublicEndpoint’
==> azure-arm:  -> IP Address          : ‘40.76.218.147’
==> azure-arm: Waiting for SSH toobecome available...
==> azure-arm: Connected tooSSH!
==> azure-arm: Provisioning with shell script: /var/folders/h1/ymh5bdx15wgdn5hvgj1wc0zh0000gn/T/packer-shell868574263
    azure-arm: WARNING! hello waagent service will be stopped.
    azure-arm: WARNING! Cached DHCP leases will be deleted.
    azure-arm: WARNING! root password will be disabled. You will not be able toologin as root.
    azure-arm: WARNING! /etc/resolvconf/resolv.conf.d/tail and /etc/resolvconf/resolv.conf.d/original will be deleted.
    azure-arm: WARNING! packer account and entire home directory will be deleted.
==> azure-arm: Querying hello machine’s properties ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Managed OS Disk   : ‘/subscriptions/guid/resourceGroups/packer-Resource-Group-swtxmqm7ly/providers/Microsoft.Compute/disks/osdisk’
==> azure-arm: Powering off machine ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> ComputeName       : ‘pkrvmswtxmqm7ly’
==> azure-arm: Capturing image ...
==> azure-arm:  -> Compute ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm:  -> Compute Name              : ‘pkrvmswtxmqm7ly’
==> azure-arm:  -> Compute Location          : ‘East US’
==> azure-arm:  -> Image ResourceGroupName   : ‘myResourceGroup’
==> azure-arm:  -> Image Name                : ‘myPackerImage’
==> azure-arm:  -> Image Location            : ‘eastus’
==> azure-arm: Deleting resource group ...
==> azure-arm:  -> ResourceGroupName : ‘packer-Resource-Group-swtxmqm7ly’
==> azure-arm: Deleting hello temporary OS disk ...
==> azure-arm:  -> OS Disk : skipping, managed disk was used...
Build ‘azure-arm’ finished.

==> Builds finished. hello artifacts of successful builds are:
--> azure-arm: Azure.ResourceManagement.VMImage:

ManagedImageResourceGroupName: myResourceGroup
ManagedImageName: myPackerImage
ManagedImageLocation: eastus
```


## <a name="create-vm-from-azure-image"></a>Azure görüntüden VM oluşturma
Artık bir VM ile görüntüden oluşturabilirsiniz [az vm oluşturma](/cli/azure/vm#create). Merhaba hello ile oluşturulan görüntüsü belirtin `--image` parametresi. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* gelen *myPackerImage* ve zaten mevcut değilse SSH anahtarları oluşturur:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image myPackerImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

Birkaç dakika toocreate hello VM alır. Merhaba VM oluşturulduktan sonra hello not edin `publicIpAddress` hello Azure CLI tarafından görüntülenir. Bu adres kullanılan tooaccess hello NGINX bir web tarayıcısı aracılığıyla sitedir.

açık bağlantı noktası 80 hello Internet gelen ile VM'nizi tooallow web trafiği tooreach [az vm Aç-port](/cli/azure/vm#open-port):

```azurecli
az vm open-port \
    --resource-group myResourceGroup \
    --name myVM \
    --port 80
```

## <a name="test-vm-and-nginx"></a>Test VM ve NGINX
Bir web tarayıcısı açın ve girin artık `http://publicIpAddress` hello adres çubuğundaki. Kendi ortak sağlamak hello VM IP adresinden oluşturma işlemi. Merhaba varsayılan NGINX sayfası aşağıdaki örneğine hello olduğu gibi görüntülenir:

![Varsayılan NGINX sitesi](./media/build-image-with-packer/nginx.png) 


## <a name="next-steps"></a>Sonraki adımlar
Bu örnekte, Packer toocreate bir VM görüntüsü zaten yüklü NGINX ile kullanılır. Var olan dağıtım iş akışları, uygulama tooVMs hello Ansible, Chef veya Puppet görüntüsüyle oluşturulan toodeploy gibi yanı sıra bu VM görüntüsü kullanabilirsiniz.

Diğer Linux distro'lar için ek örnek Packer şablonları için bkz: [bu GitHub deposuna](https://github.com/hashicorp/packer/tree/master/examples/azure).