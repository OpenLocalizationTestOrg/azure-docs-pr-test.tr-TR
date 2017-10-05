---
title: "Azure Docker VM uzantısı ile Azure CLI 1.0 kullanın | Microsoft Docs"
description: "Docker VM uzantısı hızlı ve güvenli bir şekilde Azure Resource Manager şablonları kullanarak Docker bir ortamda dağıtmak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: a3cbcf63533f4042dcd695e141655c5814bd7068
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-docker-environment-in-azure-using-the-docker-vm-extension-with-the-azure-cli-10"></a><span data-ttu-id="ded34-103">Docker VM uzantısı ile Azure CLI 1.0 kullanarak azure'da bir Docker ortam oluşturma</span><span class="sxs-lookup"><span data-stu-id="ded34-103">Create a Docker environment in Azure using the Docker VM extension with the Azure CLI 1.0</span></span>
<span data-ttu-id="ded34-104">Docker popüler kapsayıcı yönetimi ve Linux (ve de Windows) ile kapsayıcıları hızlı bir şekilde çalışmanıza olanak sağlayan görüntüleme platform ' dir.</span><span class="sxs-lookup"><span data-stu-id="ded34-104">Docker is a popular container management and imaging platform that allows you to quickly work with containers on Linux (and Windows as well).</span></span> <span data-ttu-id="ded34-105">Azure'da, sizin ihtiyaçlarınıza göre Docker dağıtabilirsiniz çeşitli yolları vardır.</span><span class="sxs-lookup"><span data-stu-id="ded34-105">In Azure, there are various ways you can deploy Docker according to your needs.</span></span> <span data-ttu-id="ded34-106">Bu makalede, Docker VM uzantısı ve Azure Resource Manager şablonları kullanarak odaklanır.</span><span class="sxs-lookup"><span data-stu-id="ded34-106">This article focuses on using the Docker VM extension and Azure Resource Manager templates.</span></span> 

<span data-ttu-id="ded34-107">Docker makine ve Azure kapsayıcı hizmetlerini kullanma dahil farklı dağıtım yöntemi hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="ded34-107">For more information about the different deployment methods, including using Docker Machine and Azure Container Services, see the following articles:</span></span>

* <span data-ttu-id="ded34-108">Uygulama bir hızlı bir şekilde prototip için kullanarak tek bir Docker ana oluşturabilirsiniz [Docker makine](docker-machine.md).</span><span class="sxs-lookup"><span data-stu-id="ded34-108">To quickly prototype an app, you can create a single Docker host using [Docker Machine](docker-machine.md).</span></span>
* <span data-ttu-id="ded34-109">Daha büyük ve daha kararlı ortamlar için de destekler Azure Docker VM uzantısı kullanabilirsiniz [Docker Compose](https://docs.docker.com/compose/overview/) tutarlı kapsayıcı dağıtımlarını oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="ded34-109">For larger, more stable environments, you can use the Azure Docker VM extension, which also supports [Docker Compose](https://docs.docker.com/compose/overview/) to generate consistent container deployments.</span></span> <span data-ttu-id="ded34-110">Bu makale Azure Docker VM uzantısı kullanılarak ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="ded34-110">This article details using the Azure Docker VM extension.</span></span>
* <span data-ttu-id="ded34-111">Ek planlama ve yönetim araçları sağlar üretime hazır, ölçeklenebilir ortamlar oluşturmak için dağıtabileceğiniz bir [Azure kapsayıcı hizmetlerini Docker Swarm kümesinde](../../container-service/dcos-swarm/container-service-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ded34-111">To build production-ready, scalable environments that provide additional scheduling and management tools, you can deploy a [Docker Swarm cluster on Azure Container Services](../../container-service/dcos-swarm/container-service-deployment.md).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="ded34-112">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="ded34-112">CLI versions to complete the task</span></span>
<span data-ttu-id="ded34-113">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ded34-113">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="ded34-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – bizim CLI Klasik ve kaynak yönetimi dağıtım modeline (Bu makalede)</span><span class="sxs-lookup"><span data-stu-id="ded34-114">[Azure CLI 1.0](#azure-docker-vm-extension-overview) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="ded34-115">[Azure CLI 2.0](dockerextension.md): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız</span><span class="sxs-lookup"><span data-stu-id="ded34-115">[Azure CLI 2.0](dockerextension.md) - our next generation CLI for the resource management deployment model</span></span> 

## <a name="azure-docker-vm-extension-overview"></a><span data-ttu-id="ded34-116">Azure Docker VM uzantısı genel bakış</span><span class="sxs-lookup"><span data-stu-id="ded34-116">Azure Docker VM extension overview</span></span>
<span data-ttu-id="ded34-117">Azure Docker VM uzantısı yükler ve Docker arka plan programı, Docker istemcisi ve Docker Compose, Linux sanal makine (VM) yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="ded34-117">The Azure Docker VM extension installs and configures the Docker daemon, Docker client, and Docker Compose in your Linux virtual machine (VM).</span></span> <span data-ttu-id="ded34-118">Azure Docker VM uzantısı kullanarak, daha fazla denetim ve yalnızca Docker makine kullanarak veya kendiniz Docker ana oluşturarak daha özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="ded34-118">By using the Azure Docker VM extension, you have more control and features than simply using Docker Machine or creating the Docker host yourself.</span></span> <span data-ttu-id="ded34-119">Gibi bu ek özellikler [Docker Compose](https://docs.docker.com/compose/overview/), Azure Docker VM uzantısı daha sağlam geliştirici veya üretim ortamları için uygun olun.</span><span class="sxs-lookup"><span data-stu-id="ded34-119">These additional features, such as [Docker Compose](https://docs.docker.com/compose/overview/), make the Azure Docker VM extension suited for more robust developer or production environments.</span></span>

<span data-ttu-id="ded34-120">Azure Resource Manager şablonları ortamınızın tamamını yapısını tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ded34-120">Azure Resource Manager templates define the entire structure of your environment.</span></span> <span data-ttu-id="ded34-121">Şablonları oluşturmak ve Docker ana bilgisayar sanal makineleri gibi kaynakları, depolama, rol tabanlı erişim denetimi (RBAC) ve tanılama yapılandırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ded34-121">Templates allow you to create and configure resources such as the Docker host VMs, storage, Role-Based Access Controls (RBAC), and diagnostics.</span></span> <span data-ttu-id="ded34-122">Başka dağıtımlar tutarlı bir şekilde oluşturmak için bu şablonları yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ded34-122">You can reuse these templates to create additional deployments in a consistent manner.</span></span> <span data-ttu-id="ded34-123">Azure Resource Manager ve şablonları hakkında daha fazla bilgi için bkz: [Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ded34-123">For more information about Azure Resource Manager and templates, see [Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span> 

## <a name="deploy-a-template-with-the-azure-docker-vm-extension"></a><span data-ttu-id="ded34-124">Bir şablonu Azure Docker VM uzantısı ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="ded34-124">Deploy a template with the Azure Docker VM extension</span></span>
<span data-ttu-id="ded34-125">Şimdi yüklemek ve Docker ana yapılandırmak için Azure Docker VM uzantısını kullanan bir Ubuntu VM oluşturmak için var olan bir hızlı başlangıç şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ded34-125">Let's use an existing quickstart template to create an Ubuntu VM that uses the Azure Docker VM extension to install and configure the Docker host.</span></span> <span data-ttu-id="ded34-126">Şablon burada görüntüleyebilirsiniz: [basit bir Ubuntu VM docker'la dağıtımını](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="ded34-126">You can view the template here: [Simple deployment of an Ubuntu VM with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="ded34-127">Gereksinim duyduğunuz [en son Azure CLI](../../cli-install-nodejs.md) yüklü ve Resource Manager modunu aşağıdaki gibi kullanarak oturum:</span><span class="sxs-lookup"><span data-stu-id="ded34-127">You need the [latest Azure CLI](../../cli-install-nodejs.md) installed and logged in using the Resource Manager mode as follows:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="ded34-128">URI şablonunu belirleme Azure CLI kullanarak şablonu dağıtın.</span><span class="sxs-lookup"><span data-stu-id="ded34-128">Deploy the template using the Azure CLI, specifying the template URI.</span></span> <span data-ttu-id="ded34-129">Aşağıdaki örnek *westus* konumunda *myResourceGroup* adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ded34-129">The following example creates a resource group named *myResourceGroup* in the *westus* location.</span></span> <span data-ttu-id="ded34-130">Kendi kaynak grubu adı ve konumu aşağıdaki şekilde kullanın:</span><span class="sxs-lookup"><span data-stu-id="ded34-130">Use your own resource group name and location as follows:</span></span>

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="ded34-131">Depolama hesabınızın adı, bir kullanıcı adı ve parola girin ve bir DNS ad ister yanıtlayın.</span><span class="sxs-lookup"><span data-stu-id="ded34-131">Answer the prompts to name your storage account, provide a username and password, and provide a DNS name.</span></span> <span data-ttu-id="ded34-132">Çıktı aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="ded34-132">The output is similar to the following example:</span></span>

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Updating resource group myResourceGroup
info:    Updated resource group myResourceGroup
info:    Supply values for the following parameters
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

<span data-ttu-id="ded34-133">Oluşturulan ve Azure Docker VM uzantısıyla yapılandırılmış yalnızca birkaç saniye, ancak Docker ana bilgisayarınız sonra istemi yine Azure CLI döndürür.</span><span class="sxs-lookup"><span data-stu-id="ded34-133">The Azure CLI returns you to the prompt after only a few seconds, but your Docker host is still being created and configured by the Azure Docker VM extension.</span></span> <span data-ttu-id="ded34-134">Tamamlamak için dağıtım için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="ded34-134">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="ded34-135">Docker ana bilgisayar durumu kullanma hakkında ayrıntılı bilgi görüntüleyebileceğiniz `azure vm show` komutu.</span><span class="sxs-lookup"><span data-stu-id="ded34-135">You can view details about the Docker host status using the `azure vm show` command.</span></span>

<span data-ttu-id="ded34-136">Aşağıdaki örnek adlı VM durumunu denetler *myDockerVM* (varsayılan ad şablondan - bu adı değişmez) kaynak grubunda adlı *myResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="ded34-136">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*.</span></span> <span data-ttu-id="ded34-137">Önceki adımda oluşturduğunuz kaynak grubunun adını girin:</span><span class="sxs-lookup"><span data-stu-id="ded34-137">Enter the name of the resource group you created in the preceding step:</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myDockerVM
```

<span data-ttu-id="ded34-138">Çıktısını `azure vm show` komutu aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="ded34-138">The output of the `azure vm show` command is similar to the following example:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up the VM "myDockerVM"
+ Looking up the NIC "myVMNicD"
+ Looking up the public ip "myPublicIPD"
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

<span data-ttu-id="ded34-139">Çıktı üst, gördüğünüz **ProvisioningState** VM.</span><span class="sxs-lookup"><span data-stu-id="ded34-139">Near the top of the output, you see the **ProvisioningState** of the VM.</span></span> <span data-ttu-id="ded34-140">Bu görüntülendiğinde *başarılı*, dağıtım sona erdi ve VM için SSH kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ded34-140">When this displays *Succeeded*, the deployment has finished and you can SSH to the VM.</span></span>

<span data-ttu-id="ded34-141">Çıktı sonuna *FQDN* , Docker ana bilgisayarın tam etki alanı adını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="ded34-141">Towards the end of the output, *FQDN* displays the fully qualified domain name of your Docker host.</span></span> <span data-ttu-id="ded34-142">Bu FQDN ne kalan adımlar, Docker ana SSH için kullandığınız yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="ded34-142">This FQDN is what you use to SSH to your Docker host in the remaining steps.</span></span>

## <a name="deploy-your-first-nginx-container"></a><span data-ttu-id="ded34-143">İlk nginx kapsayıcısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="ded34-143">Deploy your first nginx container</span></span>
<span data-ttu-id="ded34-144">Dağıtım, SSH yeni Docker konağına yerel bilgisayarınızdan tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="ded34-144">Once the deployment has finished, SSH to your new Docker host from your local computer.</span></span> <span data-ttu-id="ded34-145">Kullanıcı adınızı ve FQDN şu şekilde girin:</span><span class="sxs-lookup"><span data-stu-id="ded34-145">Enter your own username and FQDN as follows:</span></span>

```bash
ssh ops@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="ded34-146">Şimdi Docker ana bilgisayara oturum açtıktan sonra bir nginx kapsayıcısı çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ded34-146">Once logged in to the Docker host, let's run an nginx container:</span></span>

```bash
sudo docker run -d -p 80:80 nginx
```

<span data-ttu-id="ded34-147">Çıktı nginx görüntü yüklenir ve bir kapsayıcı başlatıldı olarak aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="ded34-147">The output is similar to the following example as the nginx image is downloaded and a container started:</span></span>

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

<span data-ttu-id="ded34-148">Aşağıdaki gibi Docker ana bilgisayarında çalışan kapsayıcılar durumunu kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="ded34-148">Check the status of the containers running on your Docker host as follows:</span></span>

```bash
sudo docker ps
```

<span data-ttu-id="ded34-149">Çıktı aşağıdaki örneğe benzer, nginx kapsayıcısı gösteren çalıştığını ve 80 ve 443 numaralı TCP bağlantı noktaları ve iletilen:</span><span class="sxs-lookup"><span data-stu-id="ded34-149">The output is similar to the following example, showing that the nginx container is running and TCP ports 80 and 443 and being forwarded:</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS                         NAMES
b6ed109fb743        nginx               "nginx -g 'daemon off"   About a minute ago   Up About a minute   0.0.0.0:80->80/tcp, 443/tcp   adoring_payne
```

<span data-ttu-id="ded34-150">Uygulamada, kapsayıcı görmek için bir web tarayıcısını açın ve Docker ana bilgisayar FQDN adını girin:</span><span class="sxs-lookup"><span data-stu-id="ded34-150">To see your container in action, open up a web browser and enter the FQDN name of your Docker host:</span></span>

![Çalışan ngnix kapsayıcı](./media/dockerextension/nginxrunning.png)

## <a name="azure-docker-vm-extension-template-reference"></a><span data-ttu-id="ded34-152">Azure Docker VM uzantısı şablon başvurusu</span><span class="sxs-lookup"><span data-stu-id="ded34-152">Azure Docker VM extension template reference</span></span>
<span data-ttu-id="ded34-153">Önceki örnekte, var olan bir Hızlı Başlangıç şablonu kullanır.</span><span class="sxs-lookup"><span data-stu-id="ded34-153">The previous example uses an existing quickstart template.</span></span> <span data-ttu-id="ded34-154">Ayrıca, Azure Docker VM uzantısı kendi Resource Manager şablonları ile dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ded34-154">You can also deploy the Azure Docker VM extension with your own Resource Manager templates.</span></span> <span data-ttu-id="ded34-155">Bunu yapmak için aşağıdaki tanımlama, Resource Manager şablonlarınızı ekleyin *vmName* vm'nizin uygun şekilde:</span><span class="sxs-lookup"><span data-stu-id="ded34-155">To do so, add the following to your Resource Manager templates, defining the *vmName* of your VM appropriately:</span></span>

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

<span data-ttu-id="ded34-156">İzlenecek okuyarak Resource Manager şablonları kullanma hakkında daha ayrıntılı bulabilirsiniz [Azure Resource Manager'a genel bakış](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ded34-156">You can find more detailed walkthrough on using Resource Manager templates by reading [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ded34-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ded34-157">Next steps</span></span>
<span data-ttu-id="ded34-158">İçin isteyebilir [Docker daemon TCP bağlantı noktası yapılandırma](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), anlamak [Docker güvenlik](https://docs.docker.com/engine/security/security/), veya kullanarak kapsayıcıları dağıtma [Docker Compose](https://docs.docker.com/compose/overview/).</span><span class="sxs-lookup"><span data-stu-id="ded34-158">You may wish to [configure the Docker daemon TCP port](https://docs.docker.com/engine/reference/commandline/dockerd/#/bind-docker-to-another-hostport-or-a-unix-socket), understand [Docker security](https://docs.docker.com/engine/security/security/), or deploy containers using [Docker Compose](https://docs.docker.com/compose/overview/).</span></span> <span data-ttu-id="ded34-159">Azure Docker VM uzantısı kendisi hakkında daha fazla bilgi için bkz: [GitHub proje](https://github.com/Azure/azure-docker-extension/).</span><span class="sxs-lookup"><span data-stu-id="ded34-159">For more information on the Azure Docker VM Extension itself, see the [GitHub project](https://github.com/Azure/azure-docker-extension/).</span></span>

<span data-ttu-id="ded34-160">Azure'da ek Docker dağıtım seçenekleri hakkında daha fazla bilgi okuyun:</span><span class="sxs-lookup"><span data-stu-id="ded34-160">Read more information about the additional Docker deployment options in Azure:</span></span>

* [<span data-ttu-id="ded34-161">Docker makine Azure sürücüsüyle kullanın</span><span class="sxs-lookup"><span data-stu-id="ded34-161">Use Docker Machine with the Azure driver</span></span>](docker-machine.md)  
* <span data-ttu-id="ded34-162">[Docker ve oluşturma tanımlamak ve bir Azure sanal makine üzerinde birden çok kapsayıcı uygulamayı çalıştırmak için kullanmaya başlama](docker-compose-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="ded34-162">[Get Started with Docker and Compose to define and run a multi-container application on an Azure virtual machine](docker-compose-quickstart.md).</span></span>
* [<span data-ttu-id="ded34-163">Azure Container Service kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="ded34-163">Deploy an Azure Container Service cluster</span></span>](../../container-service/dcos-swarm/container-service-deployment.md)

