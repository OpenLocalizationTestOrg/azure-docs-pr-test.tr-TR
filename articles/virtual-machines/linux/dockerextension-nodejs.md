---
title: "hello Azure CLI 1.0 ile aaaUse hello Azure Docker VM uzantısı | Microsoft Docs"
description: "Nasıl toouse Docker VM uzantısı tooquickly hello ve güvenli bir şekilde Azure Resource Manager şablonları kullanarak Docker bir ortamda dağıtmak öğrenin."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2133cdb1af741fe30093910fae5c3b2c91e8d5fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension-with-hello-azure-cli-10"></a><span data-ttu-id="48a91-103">Merhaba Docker VM uzantısı hello Azure CLI 1.0 ile kullanarak azure'da bir Docker ortam oluşturma</span><span class="sxs-lookup"><span data-stu-id="48a91-103">Create a Docker environment in Azure using hello Docker VM extension with hello Azure CLI 1.0</span></span>
<span data-ttu-id="48a91-104">Docker popüler kapsayıcı yönetimi ve kapsayıcıları Linux (ve Windows da) ile tooquickly çalışma sağlayan görüntüleme platform ' dir.</span><span class="sxs-lookup"><span data-stu-id="48a91-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="48a91-105">Azure'da, Docker tooyour gereksinimlerine göre dağıtabileceğiniz çeşitli yolları vardır.</span><span class="sxs-lookup"><span data-stu-id="48a91-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="48a91-106">Bu makalede hello Docker VM uzantısı ve Azure Resource Manager şablonları kullanarak odaklanır.</span><span class="sxs-lookup"><span data-stu-id="48a91-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="48a91-107">Docker makine ve Azure kapsayıcı hizmetlerini kullanma dahil olmak üzere hello farklı dağıtım yöntemleri hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="48a91-107">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="48a91-108">tooquickly prototip bir uygulama kullanarak tek bir Docker ana oluşturabilirsiniz [Docker makine](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="48a91-108">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="48a91-109">Daha büyük ve daha kararlı ortamlar için de destekler hello Azure Docker VM uzantısı kullanabileceğiniz [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate tutarlı kapsayıcı dağıtımlarını.</span><span class="sxs-lookup"><span data-stu-id="48a91-109">For larger, more stable environments, you can use hello Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) toogenerate consistent container deployments.</span></span> <span data-ttu-id="48a91-110">Bu makale Hello Azure Docker VM uzantısı kullanılarak ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="48a91-110">This article details using hello Azure Docker VM extension.</span></span>
* <span data-ttu-id="48a91-111">dağıtabileceğiniz ek planlama ve yönetim araçları sağlayan toobuild üretime hazır, ölçeklenebilir ortamlar, bir [Azure kapsayıcı hizmetlerini Docker Swarm kümesinde](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="48a91-111">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="48a91-112">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="48a91-112">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="48a91-113">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="48a91-113">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="48a91-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="48a91-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="48a91-115">[Azure CLI 2.0](dockerextension.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="48a91-115">[Azure CLI 2.0](dockerextension.md) - our next generation CLI for hello resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="48a91-116">Azure Docker VM uzantısı genel bakış</span><span class="sxs-lookup"><span data-stu-id="48a91-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="48a91-117">Hello Azure Docker VM uzantısı yükler ve hello Docker arka plan programı, Docker istemcisi ve Docker Compose, Linux sanal makine (VM) yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="48a91-117">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="48a91-118">Hello Azure Docker VM uzantısı kullanarak, daha fazla denetim ve yalnızca Docker makine kullanarak veya kendiniz hello Docker ana oluşturarak daha özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="48a91-118">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="48a91-119">Gibi bu ek özellikler [Docker Compose](https://docs.docker.com/compose/overview/), daha sağlam geliştirici veya üretim ortamları için uygun hello Azure Docker VM uzantısı olun.</span><span class="sxs-lookup"><span data-stu-id="48a91-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="48a91-120">Azure Resource Manager şablonları hello tüm ortamınızın yapısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="48a91-120">Azure Resource Manager templates define hello entire structure of your environment.</span></span> <span data-ttu-id="48a91-121">Şablonları toocreate izin ver ve hello Docker ana bilgisayar sanal makineleri, depolama, rol tabanlı erişim denetimi (RBAC) ve tanılama gibi kaynakları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="48a91-121">Templates allow you toocreate and configure resources such as hello Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="48a91-122">Bu şablonlar toocreate ek dağıtımlar tutarlı bir şekilde yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48a91-122">You can reuse these templates toocreate additional deployments in a consistent manner.</span></span> <span data-ttu-id="48a91-123">Azure Resource Manager ve şablonları hakkında daha fazla bilgi için bkz: [Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48a91-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="48a91-124">Şablon hello Azure Docker VM uzantısı ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="48a91-124">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="48a91-125">Şimdi var olan bir Hızlı Başlangıç şablonu toocreate hello Azure Docker VM uzantısı tooinstall kullanan bir Ubuntu VM kullanın ve hello Docker ana yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="48a91-125">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="48a91-126">Merhaba şablon burada görüntüleyebilirsiniz: [basit bir Ubuntu VM docker'la dağıtımını](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="48a91-126">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="48a91-127">Merhaba gereksinim [en son Azure CLI](../../cli-install-nodejs.md) yüklü ve aşağıdaki gibi hello Resource Manager modunu kullanarak oturum:</span><span class="sxs-lookup"><span data-stu-id="48a91-127">You need hello [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using hello Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="48a91-128">Merhaba hello şablon URI belirtme Azure CLI kullanarak hello şablonunu dağıtın.</span><span class="sxs-lookup"><span data-stu-id="48a91-128">Deploy hello template using hello Azure CLI, specifying hello template URI.</span></span> <span data-ttu-id="48a91-129">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westus* konumu.</span><span class="sxs-lookup"><span data-stu-id="48a91-129">hello following example creates a resource group named *myResourceGroup* in hello *westus* location.</span></span> <span data-ttu-id="48a91-130">Kendi kaynak grubu adı ve konumu aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="48a91-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="48a91-131">Depolama hesabınız Hello istemleri tooname yanıt, bir kullanıcı adı ve parola girin ve bir DNS adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="48a91-131">Answer hello prompts tooname your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="48a91-132">Merhaba, benzer toohello aşağıdaki örneğine çıktı:</span><span class="sxs-lookup"><span data-stu-id="48a91-132">hello output is similar toohello following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for hello following parameters
newStorageAccountName: mystorageaccount
adminUsername: azureuser
adminPassword: P@ssword!
dnsNameForPublicIP: mypublicidns
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

<span data-ttu-id="48a91-133">Hello Azure CLI yalnızca birkaç saniye sonra toohello istemi verir, ancak Docker ana bilgisayarınız hala oluşturuluyor ve Azure Docker VM uzantısı tarafından hello yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="48a91-133">hello Azure CLI returns you toohello prompt after only a few seconds, but your Docker host is still being created and configured by hello Azure Docker VM extension.</span></span> <span data-ttu-id="48a91-134">Merhaba dağıtım toofinish birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="48a91-134">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="48a91-135">Hello kullanarak hello Docker ana bilgisayar durumunu ilgili ayrıntıları görüntüleyebilirsiniz `azure vm show` komutu.</span><span class="sxs-lookup"><span data-stu-id="48a91-135">You can view details about hello Docker host status using hello `azure vm show` command.</span></span>

<span data-ttu-id="48a91-136">Merhaba aşağıdaki örnek hello durumunu hello adlı VM denetler *myDockerVM* (Merhaba hello şablondan varsayılan adı - bu adı değiştirmemeniz) adlı hello kaynak grubunda *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="48a91-136">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*.</span></span> <span data-ttu-id="48a91-137">Merhaba hello önceki adımda oluşturduğunuz hello kaynak grubunun adını girin:</span><span class="sxs-lookup"><span data-stu-id="48a91-137">Enter hello name of hello resource group you created in hello preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

<span data-ttu-id="48a91-138">Merhaba hello çıktısını `azure vm show` benzer toohello izlemektir örnek komut:</span><span class="sxs-lookup"><span data-stu-id="48a91-138">hello output of hello `azure vm show` command is similar toohello following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "myDockerVM"
+ Looking up hello NIC "myVMNicD"
+ Looking up hello public ip "myPublicIPD"
data:    Id                              :/subscriptions/guid/resourceGroups/myresourcegroup/providers/Microsoft.Compute/virtualMachines/MyDockerVM
data:    ProvisioningState               :Succeeded
data:    Name                            :MyDockerVM
data:    Location                        :westus
data:    Type                            :Microsoft.Compute/virtualMachines
[...]
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-33-D3-95
data:          Provisioning State        :Succeeded
data:          Name                      :myVMNicD
data:          Location                  :westus
data:            Public IP address       :13.91.107.235
data:            FQDN                    :mypublicdns.westus.cloudapp.azure.com
data:
data:    Diagnostics Instance View:
info:    vm show command OK
```

<span data-ttu-id="48a91-139">Hello gördüğünüz hello Çıktı Hello yukarıya yakın **ProvisioningState** hello VM.</span><span class="sxs-lookup"><span data-stu-id="48a91-139">Near hello top of hello output, you see hello **ProvisioningState** of hello VM.</span></span> <span data-ttu-id="48a91-140">Bu görüntülendiğinde *başarılı*hello dağıtımı tamamlandı ve SSH toohello VM kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48a91-140">When this displays *Succeeded*, hello deployment has finished and you can SSH toohello VM.</span></span>

<span data-ttu-id="48a91-141">Merhaba çıktı hello sonuna doğru *FQDN* Docker ana bilgisayarınız hello tam etki alanı adını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="48a91-141">Towards hello end of hello output, *FQDN* displays hello fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="48a91-142">Bu FQDN, kullandığınız olan adımları kalan hello tooSSH tooyour Docker ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="48a91-142">This FQDN is what you use tooSSH tooyour Docker host in hello remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="48a91-143">İlk nginx kapsayıcısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="48a91-143">Deploy your first nginx container</span></span>
<span data-ttu-id="48a91-144">Bir kez hello dağıtımı tamamlandı, SSH tooyour yeni Docker ana yerel bilgisayarınızdan.</span><span class="sxs-lookup"><span data-stu-id="48a91-144">Once hello deployment has finished, SSH tooyour new Docker host from your local computer.</span></span> <span data-ttu-id="48a91-145">Kullanıcı adınızı ve FQDN şu şekilde girin:</span><span class="sxs-lookup"><span data-stu-id="48a91-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="48a91-146">Şimdi toohello Docker ana oturum sonra bir nginx kapsayıcısı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="48a91-146">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="48a91-147">Merhaba nginx görüntü indirilen olarak aşağıdaki örneğine benzer toohello ve başlatılan bir kapsayıcı Hello çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="48a91-147">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

```bash
Unable toofind image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="48a91-148">Aşağıdaki gibi Docker ana bilgisayarında çalışan Merhaba kapsayıcılara Hello durumunu kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="48a91-148">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="48a91-149">Merhaba çıktı aşağıdaki örneğine benzer toohello, o hello nginx kapsayıcısı gösteren çalıştığını ve 80 ve 443 numaralı TCP bağlantı noktaları ve iletilen:</span><span class="sxs-lookup"><span data-stu-id="48a91-149">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="48a91-150">Eylem, kapsayıcıyı toosee açın yukarı bir web tarayıcısı ve hello FQDN, Docker ana bilgisayar adını girin:</span><span class="sxs-lookup"><span data-stu-id="48a91-150">toosee your container in action, open up a web browser and enter hello FQDN name of your Docker host:</span></span>

![Çalışan ngnix kapsayıcı](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="48a91-152">Azure Docker VM uzantısı şablon başvurusu</span><span class="sxs-lookup"><span data-stu-id="48a91-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="48a91-153">Merhaba önceki örneği var olan bir Hızlı Başlangıç şablonu kullanır.</span><span class="sxs-lookup"><span data-stu-id="48a91-153">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="48a91-154">Ayrıca kendi Resource Manager şablonları ile hello Azure Docker VM uzantısı dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="48a91-154">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="48a91-155">toodo, bu nedenle, tooyour Resource Manager şablonları aşağıdaki, hello tanımlama hello ekleyin *vmName* vm'nizin uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="48a91-155">toodo so, add hello following tooyour Resource Manager templates, defining hello *vmName* of your VM appropriately:</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachines/extensions",
  "name": "[concat(variables('vmName'), '/DockerExtension'))]",
  "apiVersion": "2015-05-01-preview",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
  ],
  "properties": {
    "publisher": "Microsoft.Azure.Extensions",
    "type": "DockerExtension",
    "typeHandlerVersion": "1.1",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="48a91-156">İzlenecek okuyarak Resource Manager şablonları kullanma hakkında daha ayrıntılı bulabilirsiniz [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="48a91-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="48a91-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="48a91-157">Next steps</span></span>
<span data-ttu-id="48a91-158">Çok isteyebilir[hello Docker arka plan programı TCP bağlantı noktası](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), anlamak [Docker güvenlik](https://docs.docker.com/engine/security/security/), veya kullanarak kapsayıcıları dağıtma [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="48a91-158">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="48a91-159">Merhaba hello Azure Docker VM uzantısı kendisi hakkında daha fazla bilgi için bkz: [GitHub proje](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="48a91-159">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="48a91-160">Merhaba ek Docker dağıtım seçenekleri Azure hakkında daha fazla bilgi okuyun:</span><span class="sxs-lookup"><span data-stu-id="48a91-160">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="48a91-161">Docker makine hello Azure sürücüsü ile kullanma</span><span class="sxs-lookup"><span data-stu-id="48a91-161">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="48a91-162">[Docker ile çalışmaya başlama ve toodefine oluşturma ve birden çok kapsayıcı uygulaması bir Azure sanal makine üzerinde çalışan](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="48a91-162">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="48a91-163">Azure Container Service kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="48a91-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

