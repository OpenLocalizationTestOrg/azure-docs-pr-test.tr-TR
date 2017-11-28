---
title: "Azure Docker VM uzantısını kullanan | Microsoft Docs"
description: "Docker VM uzantısı hızlı ve güvenli bir şekilde Azure Resource Manager şablonları ve Azure CLI 2.0 kullanarak Docker bir ortamda dağıtmak için nasıl kullanılacağını öğrenin"
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
ms.openlocfilehash: 63d0d80999fd57d014c74d5c6aef3733ec2afe85
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension"></a><span data-ttu-id="02711-103">Docker VM uzantısı kullanarak Azure'da bir Docker ortam oluşturma</span><span class="sxs-lookup"><span data-stu-id="02711-103">Create a Docker environment in Azure using the Docker VM extension</span></span>
<span data-ttu-id="02711-104">Docker popüler kapsayıcı yönetimi ve hızlı bir şekilde ile kapsayıcıları Linux üzerinde çalışmanıza olanak sağlar görüntüleme platform ' dir.</span><span class="sxs-lookup"><span data-stu-id="02711-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux.</span></span> <span data-ttu-id="02711-105">Azure'da, sizin ihtiyaçlarınıza göre Docker dağıtabilirsiniz çeşitli yolları vardır.</span><span class="sxs-lookup"><span data-stu-id="02711-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="02711-106">Bu makalede, Docker VM uzantısı ve Azure Resource Manager şablonları ile Azure CLI 2.0 kullanarak odaklanır.</span><span class="sxs-lookup"><span data-stu-id="02711-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates with the Azure CLI 2.0.</span></span> <span data-ttu-id="02711-107">Bu adımları [Azure CLI 1.0](dockerextension-nodejs.md) ile de gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02711-107">You can also perform these steps with the [Azure CLI 1.0](dockerextension-nodejs.md).</span></span>

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="02711-108">Azure Docker VM uzantısı genel bakış</span><span class="sxs-lookup"><span data-stu-id="02711-108">Azure Docker VM extension overview</span></span>
<span data-ttu-id="02711-109">Azure Docker VM uzantısı yükler ve Docker arka plan programı, Docker istemcisi ve Docker Compose, Linux sanal makine (VM) yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="02711-109">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="02711-110">Azure Docker VM uzantısı kullanarak, daha fazla denetim ve yalnızca Docker makine kullanarak veya kendiniz Docker ana oluşturarak daha özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="02711-110">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="02711-111">Gibi bu ek özellikler [Docker Compose](https://docs.docker.com/compose/overview/), Azure Docker VM uzantısı daha sağlam geliştirici veya üretim ortamları için uygun olun.</span><span class="sxs-lookup"><span data-stu-id="02711-111">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="02711-112">Docker makine ve Azure kapsayıcı hizmetlerini kullanma dahil farklı dağıtım yöntemi hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="02711-112">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="02711-113">Uygulama bir hızlı bir şekilde prototip için kullanarak tek bir Docker ana oluşturabilirsiniz [Docker makine](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="02711-113">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="02711-114">Ek planlama ve yönetim araçları sağlar üretime hazır, ölçeklenebilir ortamlar oluşturmak için dağıtabileceğiniz bir [Azure kapsayıcı hizmetlerini Docker Swarm kümesinde](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="02711-114">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="02711-115">Bir şablonu Azure Docker VM uzantısı ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="02711-115">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="02711-116">Şimdi yüklemek ve Docker ana yapılandırmak için Azure Docker VM uzantısını kullanan bir Ubuntu VM oluşturmak için var olan bir hızlı başlangıç şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="02711-116">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="02711-117">Şablon burada görüntüleyebilirsiniz: [basit bir Ubuntu VM docker'la dağıtımını](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="02711-117">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="02711-118">En son gereksinim [Azure CLI 2.0](/cli/azure/install-az-cli2) yüklü ve bir Azure hesabı kullanarak oturum açmış [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="02711-118">You need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="02711-119">İlk olarak, bir kaynak grubu ile oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="02711-119">First, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="02711-120">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroup* içinde *westus* konumu:</span><span class="sxs-lookup"><span data-stu-id="02711-120">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="02711-121">Ardından, bir VM'yi dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) Azure Docker VM uzantısını içeren [github'daki bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="02711-121">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="02711-122">Kendi değerlerini sağlamanız *newStorageAccountName*, *adminUsername*, *Admınpassword*, ve *dnsNameForPublicIP* gibi:</span><span class="sxs-lookup"><span data-stu-id="02711-122">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP* as follows:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="02711-123">Tamamlamak için dağıtım için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="02711-123">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="02711-124">Dağıtım tamamlandıktan sonra [sonraki adımına geçmek](#deploy-your-first-nginx-container) SSH, VM için.</span><span class="sxs-lookup"><span data-stu-id="02711-124">Once the deployment is finished, [move to next step](#deploy-your-first-nginx-container) to SSH to your VM.</span></span> 

<span data-ttu-id="02711-125">Bunun yerine denetim komut istemini dönüp işlemi arka planda devam dağıtım izin için isteğe bağlı olarak ekleyin `--no-wait` yukarıdaki komut için bayrak.</span><span class="sxs-lookup"><span data-stu-id="02711-125">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="02711-126">Bu işlem birkaç dakika dağıtım devam ederken diğer iş CLI işlemleri yapmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="02711-126">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> 

<span data-ttu-id="02711-127">Ardından Docker ana durumuyla ilgili ayrıntıları görüntüleyebilirsiniz [az vm Göster](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="02711-127">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="02711-128">Aşağıdaki örnek adlı VM durumunu denetler *myDockerVM* (varsayılan ad şablondan - bu adı değişmez) kaynak grubunda adlı *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="02711-128">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="02711-129">Bu komut döndüğünde *başarılı*, dağıtım sona erdi ve sonraki adımda VM için SSH kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02711-129">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="02711-130">İlk nginx kapsayıcısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="02711-130">Deploy your first nginx container</span></span>
<span data-ttu-id="02711-131">DNS adı dahil olmak üzere, VM ayrıntılarını görüntülemek için kullanın `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span><span class="sxs-lookup"><span data-stu-id="02711-131">To view details of your VM, including the DNS name, use `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv`.</span></span> <span data-ttu-id="02711-132">Yeni Docker SSH yerel bilgisayarınızdan gibi ana bilgisayar:</span><span class="sxs-lookup"><span data-stu-id="02711-132">SSH to your new Docker host from your local computer as follows:</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="02711-133">Şimdi Docker ana bilgisayara oturum açtıktan sonra bir nginx kapsayıcısı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="02711-133">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="02711-134">Çıktı nginx görüntü yüklenir ve bir kapsayıcı başlatıldı olarak aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="02711-134">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

```bash
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
efd26ecc9548: Pull complete
a3ed95caeb02: Pull complete
a48df1751a97: Pull complete
8ddc2d7beb91: Pull complete
Digest: sha256:2ca2638e55319b7bc0c7d028209ea69b1368e95b01383e66dfe7e4f43780926d
Status: Downloaded newer image for nginx:latest
b6ed109fb743a762ff21a4606dd38d3e5d35aff43fa7f12e8d4ed1d920b0cd74
```

<span data-ttu-id="02711-135">Aşağıdaki gibi Docker ana bilgisayarında çalışan kapsayıcılar durumunu kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="02711-135">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="02711-136">Çıktı aşağıdaki örneğe benzer, nginx kapsayıcısı gösteren çalıştığını ve 80 ve 443 numaralı TCP bağlantı noktaları ve iletilen:</span><span class="sxs-lookup"><span data-stu-id="02711-136">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="02711-137">Uygulamada, kapsayıcı görmek için bir web tarayıcısını açın ve Docker ana bilgisayarının DNS adını girin:</span><span class="sxs-lookup"><span data-stu-id="02711-137">To see your container in action, open up a web browser and enter the DNS name of your Docker host:</span></span>

![Çalışan ngnix kapsayıcı](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="02711-139">Azure Docker VM uzantısı şablon başvurusu</span><span class="sxs-lookup"><span data-stu-id="02711-139">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="02711-140">Önceki örnekte, var olan bir Hızlı Başlangıç şablonu kullanır.</span><span class="sxs-lookup"><span data-stu-id="02711-140">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="02711-141">Ayrıca, Azure Docker VM uzantısı kendi Resource Manager şablonları ile dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02711-141">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="02711-142">Bunu yapmak için aşağıdaki tanımlama, Resource Manager şablonlarınızı ekleyin `vmName` vm'nizin uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="02711-142">To do so, add the following to your Resource Manager templates, defining the `vmName` of your VM appropriately:</span></span>

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

<span data-ttu-id="02711-143">İzlenecek okuyarak Resource Manager şablonları kullanma hakkında daha ayrıntılı bulabilirsiniz [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="02711-143">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="02711-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="02711-144">Next steps</span></span>
<span data-ttu-id="02711-145">İçin isteyebilir [Docker daemon TCP bağlantı noktası yapılandırma](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), anlamak [Docker güvenlik](https://docs.docker.com/engine/security/security/), veya kullanarak kapsayıcıları dağıtma [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="02711-145">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="02711-146">Azure Docker VM uzantısı kendisi hakkında daha fazla bilgi için bkz: [GitHub proje](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="02711-146">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="02711-147">Azure'da ek Docker dağıtım seçenekleri hakkında daha fazla bilgi okuyun:</span><span class="sxs-lookup"><span data-stu-id="02711-147">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="02711-148">Docker makine Azure sürücüsüyle kullanın</span><span class="sxs-lookup"><span data-stu-id="02711-148">Use Docker Machine with the Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="02711-149">[Docker ve oluşturma tanımlamak ve bir Azure sanal makine üzerinde birden çok kapsayıcı uygulamayı çalıştırmak için kullanmaya başlama](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="02711-149">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="02711-150">Azure Container Service kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="02711-150">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

