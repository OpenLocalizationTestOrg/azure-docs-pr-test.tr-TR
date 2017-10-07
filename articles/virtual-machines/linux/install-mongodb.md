---
title: "aaaInstall hello Azure CLI ile bir Linux VM üzerinde MongoDB | Microsoft Docs"
description: "Bilgi nasıl tooinstall ve Linux sanal makine iusing hello Azure CLI 2.0 üzerinde MongoDB yapılandırın"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 3f55b546-86df-4442-9ef4-8a25fae7b96e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 97a4d9913f0eeaf7b8bf15d7fc81befe538cdc8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a>Nasıl tooinstall ve MongoDB bir Linux VM yapılandırma
[MongoDB](http://www.mongodb.org) bir popüler açık kaynak, yüksek performanslı NoSQL veritabanıdır. Bu makale size nasıl gösterir tooinstall ve MongoDB bir Linux VM hello Azure CLI 2.0 ile yapılandırın. Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](install-mongodb-nodejs.md). Örnekleri gösterilir, ayrıntı nasıl için:

* [El ile yükleyin ve temel bir MongoDB örneği yapılandırın](#manually-install-and-configure-mongodb-on-a-vm)
* [Resource Manager şablonu kullanarak temel MongoDB örneği oluşturma](#create-basic-mongodb-instance-on-centos-using-a-template)
* [Resource Manager şablonu kullanarak çoğaltma ile parçalı küme ayarlar karmaşık bir MongoDB oluşturma](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a>El ile yükleyin ve bir VM üzerinde MongoDB yapılandırın
MongoDB [yükleme yönergelerinizi](https://docs.mongodb.com/manual/administration/install-on-linux/) Red Hat gibi Linux distro'lar için / CentOS, SUSE, Ubuntu ve Debian. Merhaba aşağıdaki örnekte oluşturur bir *CentOS* VM. toocreate bu ortam hello son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).

[az group create](/cli/azure/group#create) ile bir kaynak grubu oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:

```azurecli
az group create --name myResourceGroup --location eastus
```

[az vm create](/cli/azure/vm#create) ile bir VM oluşturun. Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* adlı bir kullanıcı ile *azureuser* SSH ortak anahtar kimlik doğrulaması kullanma

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

SSH toohello kullanıcı adınızı ve hello kullanarak VM `publicIpAddress` hello önceki adımdaki hello çıktıda listelenen:

```bash
ssh azureuser@<publicIpAddress>
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

Varsayılan olarak, MongoDB erişmesini engeller CentOS görüntüleri SELinux uygulanır. İlke Yönetimi Araçları'nı yükleyin ve SELinux tooallow MongoDB toooperate, varsayılan TCP bağlantı noktası 27017 aşağıdaki gibi yapılandırın:

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
Azure hızlı başlatma şablonunu Github'dan aşağıdaki hello kullanarak tek bir CentOS VM üzerinde temel bir MongoDB örneği oluşturabilirsiniz. Bu şablon için Linux tooadd hello özel betik uzantısı kullanan bir **yum** deposu tooyour CentOS VM'yeni oluşturulmuş ve MongoDB yükleyin.

* [CentOS temel MongoDB örneğinde](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json

toocreate bu ortam hello son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login). İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:

```azurecli
az group create --name myResourceGroup --location eastus
```

Ardından, hello MongoDB şablonla dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create). Kendi kaynak tanımlamak adları ve gibi gerektiğinde boyutları *newStorageAccountName*, *virtualNetworkName*, ve *vmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"},
    "virtualNetworkName": {"value": "myVnet"},
    "vmSize": {"value": "Standard_DS2_v2"},
    "vmName": {"value": "myVM"},
    "publicIPAddressName": {"value": "myPublicIP"},
    "nicName": {"value": "myNic"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

VM toohello üzerinde oturum VM hello Genel DNS adresi kullanarak. Merhaba ortak DNS adresi ile görüntüleyebilirsiniz [az vm Göster](/cli/azure/vm#show):

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

SSH tooyour kullanıcı adınızı ve Genel DNS adresi kullanarak VM:

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
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

toocreate bu ortam hello son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login). İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create). Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:

```azurecli
az group create --name myResourceGroup --location eastus
```

Ardından, hello MongoDB şablonla dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create). Kendi kaynak tanımlamak adları ve gibi gerektiğinde boyutları *mongoAdminUsername*, *sizeOfDataDiskInGB*, ve *configNodeVmSize*:

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "mongoAdminUsername": {"value": "mongoadmin"},
    "mongoAdminPassword": {"value": "P@ssw0rd!"},
    "dnsNamePrefix": {"value": "mypublicdns"},
    "environment": {"value": "AzureCloud"},
    "numDataDisks": {"value": "4"},
    "sizeOfDataDiskInGB": {"value": 20},
    "centOsVersion": {"value": "7.0"},
    "routerNodeVmSize": {"value": "Standard_DS3_v2"},
    "configNodeVmSize": {"value": "Standard_DS3_v2"},
    "replicaNodeVmSize": {"value": "Standard_DS3_v2"},
    "zabbixServerIPAddress": {"value": "Null"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json \
  --name myMongoDBCluster \
  --no-wait
```

Bu dağıtım üzerinde bir saat toodeploy alabilir ve tüm hello VM örnekleri yapılandırın. Merhaba `--no-wait` bayrağı hello şablon dağıtımı hello Azure platformu tarafından kabul edildikten sonra komut tooreturn denetim toohello komut istemi önceki hello hello sonunda kullanılır. Merhaba dağıtım durumu ile sonra görüntüleyebileceğiniz [az grubu dağıtım Göster](/cli/azure/group/deployment#show). Merhaba aşağıdaki örnek görünümleri hello hello durumunun *myMongoDBCluster* hello dağıtımda *myResourceGroup* kaynak grubu:

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a>Sonraki adımlar
Bu örneklerde, toohello MongoDB yerel olarak VM hello bağlanın. Tooconnect toohello MongoDB örneği başka bir VM veya ağdan istiyorsanız, uygun hello olun [ağ güvenlik grubu kuralları oluşturulur](nsg-quickstart.md).

Bu örnekler hello çekirdek MongoDB ortamı geliştirme amacıyla dağıtın. Gerekli hello güvenlik yapılandırma seçenekleri, ortamınız için geçerlidir. Daha fazla bilgi için bkz: Merhaba [MongoDB güvenlik belgeleri](https://docs.mongodb.com/manual/security/).

Merhaba şablonları kullanarak oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).

Hello Azure Resource Manager şablonları hello özel betik uzantısının toodownload kullanın ve komut dosyaları Vm'leriniz yürütün. Daha fazla bilgi için bkz: [kullanma hello Azure özel betik uzantısı ile Linux sanal makineleri](extensions-customscript.md).

