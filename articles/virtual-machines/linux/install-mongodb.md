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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm"></a><span data-ttu-id="27473-103">Nasıl tooinstall ve MongoDB bir Linux VM yapılandırma</span><span class="sxs-lookup"><span data-stu-id="27473-103">How tooinstall and configure MongoDB on a Linux VM</span></span>
<span data-ttu-id="27473-104">[MongoDB](http://www.mongodb.org) bir popüler açık kaynak, yüksek performanslı NoSQL veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="27473-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="27473-105">Bu makale size nasıl gösterir tooinstall ve MongoDB bir Linux VM hello Azure CLI 2.0 ile yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="27473-105">This article shows you how tooinstall and configure MongoDB on a Linux VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="27473-106">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](install-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="27473-106">You can also perform these steps with hello [Azure CLI 1.0](install-mongodb-nodejs.md).</span></span> <span data-ttu-id="27473-107">Örnekleri gösterilir, ayrıntı nasıl için:</span><span class="sxs-lookup"><span data-stu-id="27473-107">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="27473-108">El ile yükleyin ve temel bir MongoDB örneği yapılandırın</span><span class="sxs-lookup"><span data-stu-id="27473-108">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="27473-109">Resource Manager şablonu kullanarak temel MongoDB örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="27473-109">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="27473-110">Resource Manager şablonu kullanarak çoğaltma ile parçalı küme ayarlar karmaşık bir MongoDB oluşturma</span><span class="sxs-lookup"><span data-stu-id="27473-110">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="27473-111">El ile yükleyin ve bir VM üzerinde MongoDB yapılandırın</span><span class="sxs-lookup"><span data-stu-id="27473-111">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="27473-112">MongoDB [yükleme yönergelerinizi](https://docs.mongodb.com/manual/administration/install-on-linux/) Red Hat gibi Linux distro'lar için / CentOS, SUSE, Ubuntu ve Debian.</span><span class="sxs-lookup"><span data-stu-id="27473-112">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="27473-113">Merhaba aşağıdaki örnekte oluşturur bir *CentOS* VM.</span><span class="sxs-lookup"><span data-stu-id="27473-113">hello following example creates a *CentOS* VM.</span></span> <span data-ttu-id="27473-114">toocreate bu ortam hello son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="27473-114">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="27473-115">[az group create](/cli/azure/group#create) ile bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="27473-115">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="27473-116">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="27473-116">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="27473-117">[az vm create](/cli/azure/vm#create) ile bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="27473-117">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="27473-118">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den *myVM* adlı bir kullanıcı ile *azureuser* SSH ortak anahtar kimlik doğrulaması kullanma</span><span class="sxs-lookup"><span data-stu-id="27473-118">hello following example creates a VM named *myVM* with a user named *azureuser* using SSH public key authentication</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image CentOS \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="27473-119">SSH toohello kullanıcı adınızı ve hello kullanarak VM `publicIpAddress` hello önceki adımdaki hello çıktıda listelenen:</span><span class="sxs-lookup"><span data-stu-id="27473-119">SSH toohello VM using your own username and hello `publicIpAddress` listed in hello output from hello previous step:</span></span>

```bash
ssh azureuser@<publicIpAddress>
```

<span data-ttu-id="27473-120">MongoDB için tooadd hello yükleme kaynakları oluşturma bir **yum** şekilde depo dosyası:</span><span class="sxs-lookup"><span data-stu-id="27473-120">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="27473-121">Merhaba MongoDB depodaki dosyayı düzenlemek için açın.</span><span class="sxs-lookup"><span data-stu-id="27473-121">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="27473-122">Hello aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="27473-122">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="27473-123">MongoDB kullanarak yükleyin **yum** gibi:</span><span class="sxs-lookup"><span data-stu-id="27473-123">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="27473-124">Varsayılan olarak, MongoDB erişmesini engeller CentOS görüntüleri SELinux uygulanır.</span><span class="sxs-lookup"><span data-stu-id="27473-124">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="27473-125">İlke Yönetimi Araçları'nı yükleyin ve SELinux tooallow MongoDB toooperate, varsayılan TCP bağlantı noktası 27017 aşağıdaki gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="27473-125">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows:</span></span>

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="27473-126">Merhaba MongoDB hizmetini şu şekilde başlatın:</span><span class="sxs-lookup"><span data-stu-id="27473-126">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="27473-127">Merhaba yerel kullanarak bağlanarak Hello MongoDB yükleme doğrulayın `mongo` istemci:</span><span class="sxs-lookup"><span data-stu-id="27473-127">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="27473-128">Şimdi hello MongoDB örneği, bazı veriler ekleme ve ardından arama test edin:</span><span class="sxs-lookup"><span data-stu-id="27473-128">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="27473-129">İsterseniz, MongoDB toostart bir sistem yeniden başlatma sırasında otomatik olarak yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="27473-129">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="27473-130">Bir şablon kullanarak CentOS üzerinde temel MongoDB örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="27473-130">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="27473-131">Azure hızlı başlatma şablonunu Github'dan aşağıdaki hello kullanarak tek bir CentOS VM üzerinde temel bir MongoDB örneği oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27473-131">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="27473-132">Bu şablon için Linux tooadd hello özel betik uzantısı kullanan bir **yum** deposu tooyour CentOS VM'yeni oluşturulmuş ve MongoDB yükleyin.</span><span class="sxs-lookup"><span data-stu-id="27473-132">This template uses hello Custom Script extension for Linux tooadd a **yum** repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="27473-133">[CentOS temel MongoDB örneğinde](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="27473-133">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="27473-134">toocreate bu ortam hello son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="27473-134">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="27473-135">İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="27473-135">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="27473-136">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="27473-136">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="27473-137">Ardından, hello MongoDB şablonla dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="27473-137">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="27473-138">Kendi kaynak tanımlamak adları ve gibi gerektiğinde boyutları *newStorageAccountName*, *virtualNetworkName*, ve *vmSize*:</span><span class="sxs-lookup"><span data-stu-id="27473-138">Define your own resource names and sizes where needed such as for *newStorageAccountName*, *virtualNetworkName*, and *vmSize*:</span></span>

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

<span data-ttu-id="27473-139">VM toohello üzerinde oturum VM hello Genel DNS adresi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="27473-139">Log on toohello VM using hello public DNS address of your VM.</span></span> <span data-ttu-id="27473-140">Merhaba ortak DNS adresi ile görüntüleyebilirsiniz [az vm Göster](/cli/azure/vm#show):</span><span class="sxs-lookup"><span data-stu-id="27473-140">You can view hello public DNS address with [az vm show](/cli/azure/vm#show):</span></span>

```azurecli
az vm show -g myResourceGroup -n myVM -d --query [fqdns] -o tsv
```

<span data-ttu-id="27473-141">SSH tooyour kullanıcı adınızı ve Genel DNS adresi kullanarak VM:</span><span class="sxs-lookup"><span data-stu-id="27473-141">SSH tooyour VM using your own username and public DNS address:</span></span>

```bash
ssh azureuser@mypublicdns.eastus.cloudapp.azure.com
```

<span data-ttu-id="27473-142">Merhaba yerel kullanarak bağlanarak Hello MongoDB yükleme doğrulayın `mongo` şekilde istemci:</span><span class="sxs-lookup"><span data-stu-id="27473-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="27473-143">Bazı veriler ekleyerek ve aşağıdaki gibi arama artık test hello örneği:</span><span class="sxs-lookup"><span data-stu-id="27473-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="27473-144">Bir şablon kullanarak CentOS üzerinde karmaşık MongoDB parçalı küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="27473-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="27473-145">Azure hızlı başlatma şablonunu Github'dan aşağıdaki hello kullanarak karmaşık MongoDB parçalı kümesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27473-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="27473-146">Bu şablon hello izleyen [MongoDB parçalı küme en iyi yöntemler](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide artıklık ve yüksek kullanılabilirlik.</span><span class="sxs-lookup"><span data-stu-id="27473-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="27473-147">Merhaba şablon iki parça, her çoğaltma kümesinde üç düğümü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="27473-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="27473-148">Bir yapılandırma sunucusu çoğaltma ile üç düğüm kümesi de oluşturulur, iki **mongos** yönlendirici sunucuları tooprovide tutarlılık tooapplications gelen hello parça genelinde.</span><span class="sxs-lookup"><span data-stu-id="27473-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="27473-149">[MongoDB parçalama CentOS kümede](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="27473-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="27473-150">Bu karmaşık MongoDB parçalı kümesi dağıtma, 20'den fazla çekirdek, genellikle hello varsayılan çekirdek sayısı her bölge için bir abonelik olduğu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="27473-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="27473-151">Bir Azure destek isteği tooincrease çekirdek sayısı açın.</span><span class="sxs-lookup"><span data-stu-id="27473-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="27473-152">toocreate bu ortam hello son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="27473-152">toocreate this environment, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span> <span data-ttu-id="27473-153">İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="27473-153">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="27473-154">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu:</span><span class="sxs-lookup"><span data-stu-id="27473-154">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="27473-155">Ardından, hello MongoDB şablonla dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create).</span><span class="sxs-lookup"><span data-stu-id="27473-155">Next, deploy hello MongoDB template with [az group deployment create](/cli/azure/group/deployment#create).</span></span> <span data-ttu-id="27473-156">Kendi kaynak tanımlamak adları ve gibi gerektiğinde boyutları *mongoAdminUsername*, *sizeOfDataDiskInGB*, ve *configNodeVmSize*:</span><span class="sxs-lookup"><span data-stu-id="27473-156">Define your own resource names and sizes where needed such as for *mongoAdminUsername*, *sizeOfDataDiskInGB*, and *configNodeVmSize*:</span></span>

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

<span data-ttu-id="27473-157">Bu dağıtım üzerinde bir saat toodeploy alabilir ve tüm hello VM örnekleri yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="27473-157">This deployment can take over an hour toodeploy and configure all hello VM instances.</span></span> <span data-ttu-id="27473-158">Merhaba `--no-wait` bayrağı hello şablon dağıtımı hello Azure platformu tarafından kabul edildikten sonra komut tooreturn denetim toohello komut istemi önceki hello hello sonunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="27473-158">hello `--no-wait` flag is used at hello end of hello preceding command tooreturn control toohello command prompt once hello template deployment has been accepted by hello Azure platform.</span></span> <span data-ttu-id="27473-159">Merhaba dağıtım durumu ile sonra görüntüleyebileceğiniz [az grubu dağıtım Göster](/cli/azure/group/deployment#show).</span><span class="sxs-lookup"><span data-stu-id="27473-159">You can then view hello deployment status with [az group deployment show](/cli/azure/group/deployment#show).</span></span> <span data-ttu-id="27473-160">Merhaba aşağıdaki örnek görünümleri hello hello durumunun *myMongoDBCluster* hello dağıtımda *myResourceGroup* kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="27473-160">hello following example views hello status for hello *myMongoDBCluster* deployment in hello *myResourceGroup* resource group:</span></span>

```azurecli
az group deployment show \
    --resource-group myResourceGroup \
    --name myMongoDBCluster \
    --query [properties.provisioningState] \
    --output tsv
```

## <a name="next-steps"></a><span data-ttu-id="27473-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="27473-161">Next steps</span></span>
<span data-ttu-id="27473-162">Bu örneklerde, toohello MongoDB yerel olarak VM hello bağlanın.</span><span class="sxs-lookup"><span data-stu-id="27473-162">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="27473-163">Tooconnect toohello MongoDB örneği başka bir VM veya ağdan istiyorsanız, uygun hello olun [ağ güvenlik grubu kuralları oluşturulur](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="27473-163">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="27473-164">Bu örnekler hello çekirdek MongoDB ortamı geliştirme amacıyla dağıtın.</span><span class="sxs-lookup"><span data-stu-id="27473-164">These examples deploy hello core MongoDB environment for development purposes.</span></span> <span data-ttu-id="27473-165">Gerekli hello güvenlik yapılandırma seçenekleri, ortamınız için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="27473-165">Apply hello required security configuration options for your environment.</span></span> <span data-ttu-id="27473-166">Daha fazla bilgi için bkz: Merhaba [MongoDB güvenlik belgeleri](https://docs.mongodb.com/manual/security/).</span><span class="sxs-lookup"><span data-stu-id="27473-166">For more information, see hello [MongoDB security docs](https://docs.mongodb.com/manual/security/).</span></span>

<span data-ttu-id="27473-167">Merhaba şablonları kullanarak oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="27473-167">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="27473-168">Hello Azure Resource Manager şablonları hello özel betik uzantısının toodownload kullanın ve komut dosyaları Vm'leriniz yürütün.</span><span class="sxs-lookup"><span data-stu-id="27473-168">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="27473-169">Daha fazla bilgi için bkz: [kullanma hello Azure özel betik uzantısı ile Linux sanal makineleri](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="27473-169">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

