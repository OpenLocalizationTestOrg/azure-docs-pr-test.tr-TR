---
title: "aaaInstall MongoDB kullanarak bir Linux VM üzerinde Azure CLI 1.0 hello | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve MongoDB hello Resource Manager dağıtım modelini kullanarak azure'da bir Linux sanal makinede yapılandırın."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 4ce21a2c63da7d00a4422e0a6766e2103e7f12d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a>Nasıl tooinstall ve MongoDB hello Azure CLI 1.0 kullanarak bir Linux VM üzerinde yapılandırma
[MongoDB](http://www.mongodb.org) bir popüler açık kaynak, yüksek performanslı NoSQL veritabanıdır. Bu makale size nasıl gösterir tooinstall ve MongoDB hello Resource Manager dağıtım modelini kullanarak azure'da bir Linux VM yapılandırın. Örnekleri gösterilir, ayrıntı nasıl için:

* [El ile yükleyin ve temel bir MongoDB örneği yapılandırın](#manually-install-and-configure-mongodb-on-a-vm)
* [Resource Manager şablonu kullanarak temel MongoDB örneği oluşturma](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Resource Manager şablonu kullanarak çoğaltma ile parçalı küme ayarlar karmaşık bir MongoDB oluşturma](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a>CLI sürümleri toocomplete hello görevi
CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:

- Azure CLI 1.0 – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)
- [Azure CLI 2.0](create-cli-complete-nodejs.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>El ile yükleyin ve bir VM üzerinde MongoDB yapılandırın
MongoDB [yükleme yönergelerinizi](https://docs.mongodb.com/manual/administration/install-on-linux/) Red Hat gibi Linux distro'lar için / CentOS, SUSE, Ubuntu ve Debian. Merhaba aşağıdaki örnekte oluşturur bir *CentOS* depolandığı bir SSH anahtarı kullanarak VM *~/.ssh/id_rsa.pub*. Yanıt hello depolama hesabı adı, DNS adı ve yönetici kimlik bilgileri ister:

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

VM toohello üzerinde oturum hello VM oluşturma adım önceki hello sonunda görüntülenen hello ortak IP adresi kullanarak:

```bash
ssh azureuser@40.78.23.145
```

MongoDB için tooadd hello yükleme kaynakları oluşturma bir **yum** şekilde depo dosyası:

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

Merhaba MongoDB depodaki dosyayı düzenlemek için açın. Hello aşağıdaki satırları ekleyin:

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

MongoDB kullanarak yükleyin **yum** gibi:

```bash
sudo yum install -y mongodb-org
```

Varsayılan olarak, MongoDB erişmesini engeller CentOS görüntüleri SELinux uygulanır. İlke Yönetimi Araçları'nı yükleyin ve SELinux tooallow MongoDB toooperate, varsayılan TCP bağlantı noktası 27017 şu şekilde yapılandırın. 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

Merhaba MongoDB hizmetini şu şekilde başlatın:

```bash
sudo service mongod start
```

Merhaba yerel kullanarak bağlanarak Hello MongoDB yükleme doğrulayın `mongo` istemci:

```bash
mongo
```

Şimdi hello MongoDB örneği, bazı veriler ekleme ve ardından arama test edin:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

İsterseniz, MongoDB toostart bir sistem yeniden başlatma sırasında otomatik olarak yapılandırın:

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a>Bir şablon kullanarak CentOS üzerinde temel MongoDB örneği oluşturma
Azure hızlı başlatma şablonunu Github'dan aşağıdaki hello kullanarak tek bir CentOS VM üzerinde temel bir MongoDB örneği oluşturabilirsiniz. Bu şablon için Linux tooadd hello özel betik uzantısı kullanan bir `yum` deposu tooyour CentOS VM'yeni oluşturulmuş ve MongoDB yükleyin.

* [CentOS temel MongoDB örneğinde](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

Merhaba aşağıdaki örnekte bir kaynak grubu hello adla oluşturur `myResourceGroup` hello içinde `eastus` bölge. Aşağıdaki gibi kendi değerlerinizi girin:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> Hello Azure CLI hello dağıtım ancak hello yükleme oluşturma birkaç saniye içinde tooa istemi döndürür ve birkaç dakika toocomplete yapılandırmasını alır. Hello dağıtımı ile Merhaba durumunu `azure group deployment show myResourceGroup`, kaynak grubunuzun adını hello uygun şekilde girme. Merhaba kadar bekleyin **ProvisioningState** gösterir *başarılı* çalışırken tooSSH toohello VM önce.

Merhaba dağıtım olduğunda SSH toohello VM tamamlayın. Hello kullanarak VM Hello IP adresi elde `azure vm show` komutunu aşağıdaki örneğine hello olduğu gibi:

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

Merhaba Çıktı Hello sonuna yakın hello genel IP adresi görüntülenir. Vm'nizin hello IP adresiyle SSH tooyour VM:

```bash
ssh azureuser@138.91.149.74
```

Merhaba yerel kullanarak bağlanarak Hello MongoDB yükleme doğrulayın `mongo` şekilde istemci:

```bash
mongo
```

Bazı veriler ekleyerek ve aşağıdaki gibi arama artık test hello örneği:

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a>Bir şablon kullanarak CentOS üzerinde karmaşık MongoDB parçalı küme oluşturma
Azure hızlı başlatma şablonunu Github'dan aşağıdaki hello kullanarak karmaşık MongoDB parçalı kümesi oluşturabilirsiniz. Bu şablon hello izleyen [MongoDB parçalı küme en iyi yöntemler](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide artıklık ve yüksek kullanılabilirlik. Merhaba şablon iki parça, her çoğaltma kümesinde üç düğümü oluşturur. Bir yapılandırma sunucusu çoğaltma ile üç düğüm kümesi de oluşturulur, iki **mongos** yönlendirici sunucuları tooprovide tutarlılık tooapplications gelen hello parça genelinde.

* [MongoDB parçalama CentOS kümede](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json

> [!WARNING]
> Bu karmaşık MongoDB parçalı kümesi dağıtma, 20'den fazla çekirdek, genellikle hello varsayılan çekirdek sayısı her bölge için bir abonelik olduğu gerektirir. Bir Azure destek isteği tooincrease çekirdek sayısı açın.

Merhaba aşağıdaki örnekte bir kaynak grubu hello adla oluşturur *myResourceGroup* hello içinde *eastus* bölge. Aşağıdaki gibi kendi değerlerinizi girin:

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> Hello Azure CLI hello dağıtım oluşturma birkaç saniye içinde tooa istemi verir, ancak hello yükleme ve yapılandırma bir saat toocomplete sürebilir. Hello dağıtımı ile Merhaba durumunu `azure group deployment show myResourceGroup`, kaynak grubunuzun adını hello buna uygun olarak ayarlama. Merhaba kadar bekleyin **ProvisioningState** gösterir *başarılı* toohello VM'ler bağlanmadan önce.


## <a name="next-steps"></a>Sonraki adımlar
Bu örneklerde, toohello MongoDB yerel olarak VM hello bağlanın. Tooconnect toohello MongoDB örneği başka bir VM veya ağdan istiyorsanız, uygun hello olun [ağ güvenlik grubu kuralları oluşturulur](nsg-quickstart.md).

Merhaba şablonları kullanarak oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).

Hello Azure Resource Manager şablonları hello özel betik uzantısının toodownload kullanın ve komut dosyaları Vm'leriniz yürütün. Daha fazla bilgi için bkz: [kullanma hello Azure özel betik uzantısı ile Linux sanal makineleri](extensions-customscript.md).

