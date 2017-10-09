---
title: "aaaUse hello Azure Docker VM uzantısı | Microsoft Docs"
description: "Nasıl toouse Docker VM uzantısı tooquickly hello ve güvenli bir şekilde Azure Resource Manager şablonları kullanarak Docker bir ortamda dağıtmak ve Azure CLI 2.0 hello öğrenin"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 936d67d7-6921-4275-bf11-1e0115e66b7f
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 8e43adc594192773466ccd2d3e455105f14c1a61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-environment-in-azure-using-hello-docker-vm-extension"></a><span data-ttu-id="fc577-103">Azure'da hello Docker VM uzantısı kullanarak bir Docker ortam oluşturma</span><span class="sxs-lookup"><span data-stu-id="fc577-103">Create a Docker environment in Azure using hello Docker VM extension</span></span>
<span data-ttu-id="fc577-104">Docker popüler kapsayıcı yönetimi ve kapsayıcıları tooquickly çalışmak Linux'ta verir görüntüleme platform ' dir.</span><span class="sxs-lookup"><span data-stu-id="fc577-104">Docker is a popular container management and imaging platform that allows you tooquickly work with containers on Linux.</span></span> <span data-ttu-id="fc577-105">Azure'da, Docker tooyour gereksinimlerine göre dağıtabileceğiniz çeşitli yolları vardır.</span><span class="sxs-lookup"><span data-stu-id="fc577-105">In Azure, there are various ways you can deploy Docker according tooyour needs.</span></span> <span data-ttu-id="fc577-106">Bu makalede, Azure CLI 2.0 hello ile Merhaba Docker VM uzantısı ve Azure Resource Manager şablonları kullanarak odaklanır.</span><span class="sxs-lookup"><span data-stu-id="fc577-106">This article focuses on using hello Docker VM extension and Azure Resource Manager templates with hello Azure CLI 2.0.</span></span> <span data-ttu-id="fc577-107">Bu adımları hello ile de gerçekleştirebilirsiniz [Azure CLI 1.0](dockerextension-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="fc577-107">You can also perform these steps with hello [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="fc577-108">Azure Docker VM uzantısı genel bakış</span><span class="sxs-lookup"><span data-stu-id="fc577-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="fc577-109">Hello Azure Docker VM uzantısı yükler ve hello Docker arka plan programı, Docker istemcisi ve Docker Compose, Linux sanal makine (VM) yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="fc577-109">hello Azure Docker VM extension installs and configures hello Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="fc577-110">Hello Azure Docker VM uzantısı kullanarak, daha fazla denetim ve yalnızca Docker makine kullanarak veya kendiniz hello Docker ana oluşturarak daha özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="fc577-110">By using hello Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating hello Docker host yourself.</span></span> <span data-ttu-id="fc577-111">Gibi bu ek özellikler [Docker Compose](https://docs.docker.com/compose/overview/), daha sağlam geliştirici veya üretim ortamları için uygun hello Azure Docker VM uzantısı olun.</span><span class="sxs-lookup"><span data-stu-id="fc577-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make hello Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="fc577-112">Docker makine ve Azure kapsayıcı hizmetlerini kullanma dahil olmak üzere hello farklı dağıtım yöntemleri hakkında daha fazla bilgi makaleleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="fc577-112">For more information about hello different deployment methods, including using Docker Machine and Azure Container Services, see hello following articles:</span></span>

* <span data-ttu-id="fc577-113">tooquickly prototip bir uygulama kullanarak tek bir Docker ana oluşturabilirsiniz [Docker makine](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="fc577-113">tooquickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="fc577-114">dağıtabileceğiniz ek planlama ve yönetim araçları sağlayan toobuild üretime hazır, ölçeklenebilir ortamlar, bir [Azure kapsayıcı hizmetlerini Docker Swarm kümesinde](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="fc577-114">toobuild production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-hello-azure-docker-vm-extension"></a><span data-ttu-id="fc577-115">Şablon hello Azure Docker VM uzantısı ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="fc577-115">Deploy a template with hello Azure Docker VM extension</span></span>
<span data-ttu-id="fc577-116">Şimdi var olan bir Hızlı Başlangıç şablonu toocreate hello Azure Docker VM uzantısı tooinstall kullanan bir Ubuntu VM kullanın ve hello Docker ana yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="fc577-116">Let's use an existing quickstart template toocreate an Ubuntu VM that uses hello Azure Docker VM extension tooinstall and configure hello Docker host.</span></span> <span data-ttu-id="fc577-117">Merhaba şablon burada görüntüleyebilirsiniz: [basit bir Ubuntu VM docker'la dağıtımını](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="fc577-117">You can view hello template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="fc577-118">Merhaba son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve tooan Azure hesabı kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="fc577-118">You need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="fc577-119">İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="fc577-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="fc577-120">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westus* konumu:</span><span class="sxs-lookup"><span data-stu-id="fc577-120">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="fc577-121">Ardından, bir VM'yi dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) hello Azure Docker VM uzantısını içeren [github'daki bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="fc577-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="fc577-122">Kendi değerlerini sağlamanız *newStorageAccountName*, *adminUsername*, *Admınpassword*, ve *dnsNameForPublicIP* gibi:</span><span class="sxs-lookup"><span data-stu-id="fc577-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="fc577-123">Merhaba dağıtım toofinish birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="fc577-123">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="fc577-124">Merhaba dağıtım tamamlandıktan sonra [toonext adım taşıma](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="fc577-124">Once hello deployment is finished, [move toonext step](#deploy-your-first-nginx-container) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="fc577-125">İsteğe bağlı olarak tooinstead dönüş denetimi toohello istemi ve let hello dağıtım hello arka planda devam hello ekleyin `--no-wait` komutu önceki toohello bayrak.</span><span class="sxs-lookup"><span data-stu-id="fc577-125">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="fc577-126">Bu işlem tooperform sağlar hello hello dağıtım için bir kaç dakika devam ederken CLI diğer iş.</span><span class="sxs-lookup"><span data-stu-id="fc577-126">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> 

<span data-ttu-id="fc577-127">Ardından hello Docker ana bilgisayar durumu ile ilgili ayrıntıları görüntüleyebilirsiniz [az vm Göster](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="fc577-127">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="fc577-128">Merhaba aşağıdaki örnek hello durumunu hello adlı VM denetler *myDockerVM* (Merhaba hello şablondan varsayılan adı - bu adı değiştirmemeniz) adlı hello kaynak grubunda *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="fc577-128">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="fc577-129">Bu komut döndüğünde *başarılı*hello dağıtımı tamamlandı ve SSH toohello VM adım aşağıdaki hello de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc577-129">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="fc577-130">İlk nginx kapsayıcısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="fc577-130">Deploy your first nginx container</span></span>
<span data-ttu-id="fc577-131">tooview ayrıntıları dahil olmak üzere hello DNS adı, vm'nizin `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="fc577-131">tooview details of your VM, including hello DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="fc577-132">SSH tooyour yeni Docker ana bilgisayar yerel bilgisayarınızdan gibi:</span><span class="sxs-lookup"><span data-stu-id="fc577-132">SSH tooyour new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="fc577-133">Şimdi toohello Docker ana oturum sonra bir nginx kapsayıcısı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fc577-133">Once logged in toohello Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="fc577-134">Merhaba nginx görüntü indirilen olarak aşağıdaki örneğine benzer toohello ve başlatılan bir kapsayıcı Hello çıktısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="fc577-134">hello output is similar toohello following example as hello nginx image is downloaded and a container started:</span></span>

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

<span data-ttu-id="fc577-135">Aşağıdaki gibi Docker ana bilgisayarında çalışan Merhaba kapsayıcılara Hello durumunu kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="fc577-135">Check hello status of hello containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="fc577-136">Merhaba çıktı aşağıdaki örneğine benzer toohello, o hello nginx kapsayıcısı gösteren çalıştığını ve 80 ve 443 numaralı TCP bağlantı noktaları ve iletilen:</span><span class="sxs-lookup"><span data-stu-id="fc577-136">hello output is similar toohello following example, showing that hello nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="fc577-137">Eylem, kapsayıcıyı toosee açın yukarı bir web tarayıcısı ve Docker ana bilgisayarınız hello DNS adını girin:</span><span class="sxs-lookup"><span data-stu-id="fc577-137">toosee your container in action, open up a web browser and enter hello DNS name of your Docker host:</span></span>

![Çalışan ngnix kapsayıcı](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="fc577-139">Azure Docker VM uzantısı şablon başvurusu</span><span class="sxs-lookup"><span data-stu-id="fc577-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="fc577-140">Merhaba önceki örneği var olan bir Hızlı Başlangıç şablonu kullanır.</span><span class="sxs-lookup"><span data-stu-id="fc577-140">hello previous example uses an existing quickstart template.</span></span> <span data-ttu-id="fc577-141">Ayrıca kendi Resource Manager şablonları ile hello Azure Docker VM uzantısı dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fc577-141">You can also deploy hello Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="fc577-142">toodo, bu nedenle, tooyour Resource Manager şablonları aşağıdaki, hello tanımlama hello ekleyin `vmName` vm'nizin uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="fc577-142">toodo so, add hello following tooyour Resource Manager templates, defining hello `vmName` of your VM appropriately:</span></span>

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
    "typeHandlerVersion": "1.*",
    "autoUpgradeMinorVersion": true,
    "settings": {},
    "protectedSettings": {}
  }
}
```

<span data-ttu-id="fc577-143">İzlenecek okuyarak Resource Manager şablonları kullanma hakkında daha ayrıntılı bulabilirsiniz [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc577-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc577-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fc577-144">Next steps</span></span>
<span data-ttu-id="fc577-145">Çok isteyebilir[hello Docker arka plan programı TCP bağlantı noktası](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), anlamak [Docker güvenlik](https://docs.docker.com/engine/security/security/), veya kullanarak kapsayıcıları dağıtma [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="fc577-145">You may wish too[configure hello Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="fc577-146">Merhaba hello Azure Docker VM uzantısı kendisi hakkında daha fazla bilgi için bkz: [GitHub proje](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="fc577-146">For more information on hello Azure Docker VM Extension itself, see hello [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="fc577-147">Merhaba ek Docker dağıtım seçenekleri Azure hakkında daha fazla bilgi okuyun:</span><span class="sxs-lookup"><span data-stu-id="fc577-147">Read more information about hello additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="fc577-148">Docker makine hello Azure sürücüsü ile kullanma</span><span class="sxs-lookup"><span data-stu-id="fc577-148">Use Docker Machine with hello Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="fc577-149">[Docker ile çalışmaya başlama ve toodefine oluşturma ve birden çok kapsayıcı uygulaması bir Azure sanal makine üzerinde çalışan](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="fc577-149">[Get Started with Docker and Compose toodefine and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="fc577-150">Azure Container Service kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="fc577-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

