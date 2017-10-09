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
# <a name="how-tooinstall-and-configure-mongodb-on-a-linux-vm-using-hello-azure-cli-10"></a><span data-ttu-id="1a905-103">Nasıl tooinstall ve MongoDB hello Azure CLI 1.0 kullanarak bir Linux VM üzerinde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1a905-103">How tooinstall and configure MongoDB on a Linux VM using hello Azure CLI 1.0</span></span>
<span data-ttu-id="1a905-104">[MongoDB](http://www.mongodb.org) bir popüler açık kaynak, yüksek performanslı NoSQL veritabanıdır.</span><span class="sxs-lookup"><span data-stu-id="1a905-104">[MongoDB](http://www.mongodb.org) is a popular open-source, high-performance NoSQL database.</span></span> <span data-ttu-id="1a905-105">Bu makale size nasıl gösterir tooinstall ve MongoDB hello Resource Manager dağıtım modelini kullanarak azure'da bir Linux VM yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1a905-105">This article shows you how tooinstall and configure MongoDB on a Linux VM in Azure using hello Resource Manager deployment model.</span></span> <span data-ttu-id="1a905-106">Örnekleri gösterilir, ayrıntı nasıl için:</span><span class="sxs-lookup"><span data-stu-id="1a905-106">Examples are shown that detail how to:</span></span>

* [<span data-ttu-id="1a905-107">El ile yükleyin ve temel bir MongoDB örneği yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1a905-107">Manually install and configure a basic MongoDB instance</span></span>](#manually-install-and-configure-mongodb-on-a-vm)
* [<span data-ttu-id="1a905-108">Resource Manager şablonu kullanarak temel MongoDB örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="1a905-108">Create a basic MongoDB instance using a Resource Manager template</span></span>](#create-basic-mongodb-instance-on-centos-using-a-template)
* [<span data-ttu-id="1a905-109">Resource Manager şablonu kullanarak çoğaltma ile parçalı küme ayarlar karmaşık bir MongoDB oluşturma</span><span class="sxs-lookup"><span data-stu-id="1a905-109">Create a complex MongoDB sharded cluster with replica sets using a Resource Manager template</span></span>](#create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="1a905-110">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="1a905-110">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="1a905-111">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="1a905-111">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="1a905-112">Azure CLI 1.0 – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="1a905-112">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="1a905-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="1a905-113">[Azure CLI 2.0](create-cli-complete-nodejs.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="manually-install-and-configure-mongodb-on-a-vm"></a><span data-ttu-id="1a905-114">El ile yükleyin ve bir VM üzerinde MongoDB yapılandırın</span><span class="sxs-lookup"><span data-stu-id="1a905-114">Manually install and configure MongoDB on a VM</span></span>
<span data-ttu-id="1a905-115">MongoDB [yükleme yönergelerinizi](https://docs.mongodb.com/manual/administration/install-on-linux/) Red Hat gibi Linux distro'lar için / CentOS, SUSE, Ubuntu ve Debian.</span><span class="sxs-lookup"><span data-stu-id="1a905-115">MongoDB [provide installation instructions](https://docs.mongodb.com/manual/administration/install-on-linux/) for Linux distros including Red Hat / CentOS, SUSE, Ubuntu, and Debian.</span></span> <span data-ttu-id="1a905-116">Merhaba aşağıdaki örnekte oluşturur bir *CentOS* depolandığı bir SSH anahtarı kullanarak VM *~/.ssh/id_rsa.pub*.</span><span class="sxs-lookup"><span data-stu-id="1a905-116">hello following example creates a *CentOS* VM using an SSH key stored at *~/.ssh/id_rsa.pub*.</span></span> <span data-ttu-id="1a905-117">Yanıt hello depolama hesabı adı, DNS adı ve yönetici kimlik bilgileri ister:</span><span class="sxs-lookup"><span data-stu-id="1a905-117">Answer hello prompts for storage account name, DNS name, and admin credentials:</span></span>

```azurecli
azure vm quick-create \
    --image-urn CentOS \
    --ssh-publickey-file ~/.ssh/id_rsa.pub 
```

<span data-ttu-id="1a905-118">VM toohello üzerinde oturum hello VM oluşturma adım önceki hello sonunda görüntülenen hello ortak IP adresi kullanarak:</span><span class="sxs-lookup"><span data-stu-id="1a905-118">Log on toohello VM using hello public IP address displayed at hello end of hello preceding VM creation step:</span></span>

```bash
ssh azureuser@40.78.23.145
```

<span data-ttu-id="1a905-119">MongoDB için tooadd hello yükleme kaynakları oluşturma bir **yum** şekilde depo dosyası:</span><span class="sxs-lookup"><span data-stu-id="1a905-119">tooadd hello installation sources for MongoDB, create a **yum** repository file as follows:</span></span>

```bash
sudo touch /etc/yum.repos.d/mongodb-org-3.4.repo
```

<span data-ttu-id="1a905-120">Merhaba MongoDB depodaki dosyayı düzenlemek için açın.</span><span class="sxs-lookup"><span data-stu-id="1a905-120">Open hello MongoDB repo file for editing.</span></span> <span data-ttu-id="1a905-121">Hello aşağıdaki satırları ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1a905-121">Add hello following lines:</span></span>

```sh
[mongodb-org-3.4]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/3.4/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-3.4.asc
```

<span data-ttu-id="1a905-122">MongoDB kullanarak yükleyin **yum** gibi:</span><span class="sxs-lookup"><span data-stu-id="1a905-122">Install MongoDB using **yum** as follows:</span></span>

```bash
sudo yum install -y mongodb-org
```

<span data-ttu-id="1a905-123">Varsayılan olarak, MongoDB erişmesini engeller CentOS görüntüleri SELinux uygulanır.</span><span class="sxs-lookup"><span data-stu-id="1a905-123">By default, SELinux is enforced on CentOS images that prevents you from accessing MongoDB.</span></span> <span data-ttu-id="1a905-124">İlke Yönetimi Araçları'nı yükleyin ve SELinux tooallow MongoDB toooperate, varsayılan TCP bağlantı noktası 27017 şu şekilde yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="1a905-124">Install policy management tools and configure SELinux tooallow MongoDB toooperate on its default TCP port 27017 as follows.</span></span> 

```bash
sudo yum install -y policycoreutils-python
sudo semanage port -a -t mongod_port_t -p tcp 27017
```

<span data-ttu-id="1a905-125">Merhaba MongoDB hizmetini şu şekilde başlatın:</span><span class="sxs-lookup"><span data-stu-id="1a905-125">Start hello MongoDB service as follows:</span></span>

```bash
sudo service mongod start
```

<span data-ttu-id="1a905-126">Merhaba yerel kullanarak bağlanarak Hello MongoDB yükleme doğrulayın `mongo` istemci:</span><span class="sxs-lookup"><span data-stu-id="1a905-126">Verify hello MongoDB installation by connecting using hello local `mongo` client:</span></span>

```bash
mongo
```

<span data-ttu-id="1a905-127">Şimdi hello MongoDB örneği, bazı veriler ekleme ve ardından arama test edin:</span><span class="sxs-lookup"><span data-stu-id="1a905-127">Now test hello MongoDB instance by adding some data and then searching:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```

<span data-ttu-id="1a905-128">İsterseniz, MongoDB toostart bir sistem yeniden başlatma sırasında otomatik olarak yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="1a905-128">If desired, configure MongoDB toostart automatically during a system reboot:</span></span>

```bash
sudo chkconfig mongod on
```


## <a name="create-basic-mongodb-instance-on-centos-using-a-template"></a><span data-ttu-id="1a905-129">Bir şablon kullanarak CentOS üzerinde temel MongoDB örneği oluşturma</span><span class="sxs-lookup"><span data-stu-id="1a905-129">Create basic MongoDB instance on CentOS using a template</span></span>
<span data-ttu-id="1a905-130">Azure hızlı başlatma şablonunu Github'dan aşağıdaki hello kullanarak tek bir CentOS VM üzerinde temel bir MongoDB örneği oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a905-130">You can create a basic MongoDB instance on a single CentOS VM using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="1a905-131">Bu şablon için Linux tooadd hello özel betik uzantısı kullanan bir `yum` deposu tooyour CentOS VM'yeni oluşturulmuş ve MongoDB yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1a905-131">This template uses hello Custom Script extension for Linux tooadd a `yum` repository tooyour newly created CentOS VM and then install MongoDB.</span></span>

* <span data-ttu-id="1a905-132">[CentOS temel MongoDB örneğinde](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1a905-132">[Basic MongoDB instance on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-on-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json</span></span>

<span data-ttu-id="1a905-133">Merhaba aşağıdaki örnekte bir kaynak grubu hello adla oluşturur `myResourceGroup` hello içinde `eastus` bölge.</span><span class="sxs-lookup"><span data-stu-id="1a905-133">hello following example creates a resource group with hello name `myResourceGroup` in hello `eastus` region.</span></span> <span data-ttu-id="1a905-134">Aşağıdaki gibi kendi değerlerinizi girin:</span><span class="sxs-lookup"><span data-stu-id="1a905-134">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-on-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="1a905-135">Hello Azure CLI hello dağıtım ancak hello yükleme oluşturma birkaç saniye içinde tooa istemi döndürür ve birkaç dakika toocomplete yapılandırmasını alır.</span><span class="sxs-lookup"><span data-stu-id="1a905-135">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration takes a few minutes toocomplete.</span></span> <span data-ttu-id="1a905-136">Hello dağıtımı ile Merhaba durumunu `azure group deployment show myResourceGroup`, kaynak grubunuzun adını hello uygun şekilde girme.</span><span class="sxs-lookup"><span data-stu-id="1a905-136">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, entering hello name of your resource group accordingly.</span></span> <span data-ttu-id="1a905-137">Merhaba kadar bekleyin **ProvisioningState** gösterir *başarılı* çalışırken tooSSH toohello VM önce.</span><span class="sxs-lookup"><span data-stu-id="1a905-137">Wait until hello **ProvisioningState** shows *Succeeded* before trying tooSSH toohello VM.</span></span>

<span data-ttu-id="1a905-138">Merhaba dağıtım olduğunda SSH toohello VM tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="1a905-138">Once hello deployment is complete, SSH toohello VM.</span></span> <span data-ttu-id="1a905-139">Hello kullanarak VM Hello IP adresi elde `azure vm show` komutunu aşağıdaki örneğine hello olduğu gibi:</span><span class="sxs-lookup"><span data-stu-id="1a905-139">Obtain hello IP address of your VM using hello `azure vm show` command as in hello following example:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myLinuxVM
```

<span data-ttu-id="1a905-140">Merhaba Çıktı Hello sonuna yakın hello genel IP adresi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1a905-140">Near hello end of hello output, hello public IP address is displayed.</span></span> <span data-ttu-id="1a905-141">Vm'nizin hello IP adresiyle SSH tooyour VM:</span><span class="sxs-lookup"><span data-stu-id="1a905-141">SSH tooyour VM with hello IP address of your VM:</span></span>

```bash
ssh azureuser@138.91.149.74
```

<span data-ttu-id="1a905-142">Merhaba yerel kullanarak bağlanarak Hello MongoDB yükleme doğrulayın `mongo` şekilde istemci:</span><span class="sxs-lookup"><span data-stu-id="1a905-142">Verify hello MongoDB installation by connecting using hello local `mongo` client as follows:</span></span>

```bash
mongo
```

<span data-ttu-id="1a905-143">Bazı veriler ekleyerek ve aşağıdaki gibi arama artık test hello örneği:</span><span class="sxs-lookup"><span data-stu-id="1a905-143">Now test hello instance by adding some data and searching as follows:</span></span>

```sh
> db
test
> db.foo.insert( { a : 1 } )  
> db.foo.find()  
{ "_id" : ObjectId("57ec477cd639891710b90727"), "a" : 1 }
> exit
```


## <a name="create-a-complex-mongodb-sharded-cluster-on-centos-using-a-template"></a><span data-ttu-id="1a905-144">Bir şablon kullanarak CentOS üzerinde karmaşık MongoDB parçalı küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="1a905-144">Create a complex MongoDB Sharded Cluster on CentOS using a template</span></span>
<span data-ttu-id="1a905-145">Azure hızlı başlatma şablonunu Github'dan aşağıdaki hello kullanarak karmaşık MongoDB parçalı kümesi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1a905-145">You can create a complex MongoDB sharded cluster using hello following Azure quickstart template from GitHub.</span></span> <span data-ttu-id="1a905-146">Bu şablon hello izleyen [MongoDB parçalı küme en iyi yöntemler](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide artıklık ve yüksek kullanılabilirlik.</span><span class="sxs-lookup"><span data-stu-id="1a905-146">This template follows hello [MongoDB sharded cluster best practices](https://docs.mongodb.com/manual/core/sharded-cluster-components/) tooprovide redundancy and high availability.</span></span> <span data-ttu-id="1a905-147">Merhaba şablon iki parça, her çoğaltma kümesinde üç düğümü oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1a905-147">hello template creates two shards, with three nodes in each replica set.</span></span> <span data-ttu-id="1a905-148">Bir yapılandırma sunucusu çoğaltma ile üç düğüm kümesi de oluşturulur, iki **mongos** yönlendirici sunucuları tooprovide tutarlılık tooapplications gelen hello parça genelinde.</span><span class="sxs-lookup"><span data-stu-id="1a905-148">One config server replica set with three nodes is also created, plus two **mongos** router servers tooprovide consistency tooapplications from across hello shards.</span></span>

* <span data-ttu-id="1a905-149">[MongoDB parçalama CentOS kümede](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) -https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="1a905-149">[MongoDB Sharding Cluster on CentOS](https://github.com/Azure/azure-quickstart-templates/tree/master/mongodb-sharding-centos) - https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json</span></span>

> [!WARNING]
> <span data-ttu-id="1a905-150">Bu karmaşık MongoDB parçalı kümesi dağıtma, 20'den fazla çekirdek, genellikle hello varsayılan çekirdek sayısı her bölge için bir abonelik olduğu gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1a905-150">Deploying this complex MongoDB sharded cluster requires more than 20 cores, which is typically hello default core count per region for a subscription.</span></span> <span data-ttu-id="1a905-151">Bir Azure destek isteği tooincrease çekirdek sayısı açın.</span><span class="sxs-lookup"><span data-stu-id="1a905-151">Open an Azure support request tooincrease your core count.</span></span>

<span data-ttu-id="1a905-152">Merhaba aşağıdaki örnekte bir kaynak grubu hello adla oluşturur *myResourceGroup* hello içinde *eastus* bölge.</span><span class="sxs-lookup"><span data-stu-id="1a905-152">hello following example creates a resource group with hello name *myResourceGroup* in hello *eastus* region.</span></span> <span data-ttu-id="1a905-153">Aşağıdaki gibi kendi değerlerinizi girin:</span><span class="sxs-lookup"><span data-stu-id="1a905-153">Enter your own values as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location eastus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/mongodb-sharding-centos/azuredeploy.json
```

> [!NOTE]
> <span data-ttu-id="1a905-154">Hello Azure CLI hello dağıtım oluşturma birkaç saniye içinde tooa istemi verir, ancak hello yükleme ve yapılandırma bir saat toocomplete sürebilir.</span><span class="sxs-lookup"><span data-stu-id="1a905-154">hello Azure CLI returns you tooa prompt within a few seconds of creating hello deployment, but hello installation and configuration can take over an hour toocomplete.</span></span> <span data-ttu-id="1a905-155">Hello dağıtımı ile Merhaba durumunu `azure group deployment show myResourceGroup`, kaynak grubunuzun adını hello buna uygun olarak ayarlama.</span><span class="sxs-lookup"><span data-stu-id="1a905-155">Check hello status of hello deployment with `azure group deployment show myResourceGroup`, adjusting hello name of your resource group accordingly.</span></span> <span data-ttu-id="1a905-156">Merhaba kadar bekleyin **ProvisioningState** gösterir *başarılı* toohello VM'ler bağlanmadan önce.</span><span class="sxs-lookup"><span data-stu-id="1a905-156">Wait until hello **ProvisioningState** shows *Succeeded* before connecting toohello VMs.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1a905-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1a905-157">Next steps</span></span>
<span data-ttu-id="1a905-158">Bu örneklerde, toohello MongoDB yerel olarak VM hello bağlanın.</span><span class="sxs-lookup"><span data-stu-id="1a905-158">In these examples, you connect toohello MongoDB instance locally from hello VM.</span></span> <span data-ttu-id="1a905-159">Tooconnect toohello MongoDB örneği başka bir VM veya ağdan istiyorsanız, uygun hello olun [ağ güvenlik grubu kuralları oluşturulur](nsg-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="1a905-159">If you want tooconnect toohello MongoDB instance from another VM or network, ensure hello appropriate [Network Security Group rules are created](nsg-quickstart.md).</span></span>

<span data-ttu-id="1a905-160">Merhaba şablonları kullanarak oluşturma hakkında daha fazla bilgi için bkz: [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1a905-160">For more information about creating using templates, see hello [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="1a905-161">Hello Azure Resource Manager şablonları hello özel betik uzantısının toodownload kullanın ve komut dosyaları Vm'leriniz yürütün.</span><span class="sxs-lookup"><span data-stu-id="1a905-161">hello Azure Resource Manager templates use hello Custom Script Extension toodownload and execute scripts on your VMs.</span></span> <span data-ttu-id="1a905-162">Daha fazla bilgi için bkz: [kullanma hello Azure özel betik uzantısı ile Linux sanal makineleri](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="1a905-162">For more information, see [Using hello Azure Custom Script Extension with Linux Virtual Machines](extensions-customscript.md).</span></span>

