---
title: "Kullanım Docker Compose azure'da bir Linux VM üzerinde | Microsoft Docs"
description: "Azure CLI ile Linux sanal makinelerde Docker ve Oluştur kullanma"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 02ab8cf9-318d-4a28-9d0c-4a31dccc2a84
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 541722cb02dd991228726e62a2304b49cdd806f2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-docker-and-compose-to-define-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="0e975-103">Docker ve oluşturma tanımlamak ve Azure'da çok kapsayıcı uygulamayı çalıştırmak için kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0e975-103">Get started with Docker and Compose to define and run a multi-container application in Azure</span></span>
<span data-ttu-id="0e975-104">İle [oluşturma](http://github.com/docker/compose), birden çok Docker kapsayıcıları için oluşan bir uygulamayı tanımlamak için basit bir metin dosyası kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e975-104">With [Compose](http://github.com/docker/compose), you use a simple text file to define an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="0e975-105">Ardından, uygulamanızda tanımlanan ortamınıza dağıtmak için her şeyi yapar tek bir komut Yukarı Döndür.</span><span class="sxs-lookup"><span data-stu-id="0e975-105">You then spin up your application in a single command that does everything to deploy your defined environment.</span></span> <span data-ttu-id="0e975-106">Örnek olarak, bu makalede, bir WordPress blog arka ucu MariaDB SQL veritabanındaki bir Ubuntu VM ile hızlı bir şekilde ayarlama gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0e975-106">As an example, this article shows you how to quickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="0e975-107">Oluştur, daha karmaşık uygulamalar ayarlamak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e975-107">You can also use Compose to set up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="0e975-108">Bir Linux VM Docker ana bilgisayar olarak ayarlama</span><span class="sxs-lookup"><span data-stu-id="0e975-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="0e975-109">Bir Linux VM oluşturun ve Docker ana bilgisayar olarak ayarlamak için Azure Marketi'nde çeşitli Azure yordamları ve kullanılabilir görüntüler veya Resource Manager şablonları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e975-109">You can use various Azure procedures and available images or Resource Manager templates in the Azure Marketplace to create a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="0e975-110">Örneğin, [ortamınıza dağıtmak için Docker VM uzantısı kullanılarak](dockerextension.md) kullanarak bir Ubuntu VM Azure Docker VM uzantısı ile hızlı bir şekilde oluşturmak için bir [hızlı başlatma şablonunu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="0e975-110">For example, see [Using the Docker VM Extension to deploy your environment](dockerextension.md) to quickly create an Ubuntu VM with the Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="0e975-111">Docker VM uzantısı kullandığınızda, VM otomatik olarak Docker ana bilgisayar olarak ayarlanır ve oluşturma zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="0e975-111">When you use the Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="0e975-112">Azure CLI 2.0 ile Docker konak oluştur</span><span class="sxs-lookup"><span data-stu-id="0e975-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="0e975-113">En son yükleme [Azure CLI 2.0](/cli/azure/install-az-cli2) ve bir Azure hesabı kullanarak oturum açma [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0e975-113">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="0e975-114">İlk olarak, Docker ortamınız için bir kaynak grubu oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="0e975-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0e975-115">Aşağıdaki örnek, bir kaynak grubu oluşturur *myResourceGroup* içinde *westus* konumu:</span><span class="sxs-lookup"><span data-stu-id="0e975-115">The following example creates a resource group named *myResourceGroup* in the *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="0e975-116">Ardından, bir VM'yi dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) Azure Docker VM uzantısını içeren [github'daki bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="0e975-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes the Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="0e975-117">Kendi değerlerini sağlamanız *newStorageAccountName*, *adminUsername*, *Admınpassword*, ve *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="0e975-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="0e975-118">Tamamlamak için dağıtım için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="0e975-118">It takes a few minutes for the deployment to finish.</span></span> <span data-ttu-id="0e975-119">Dağıtım tamamlandıktan sonra [sonraki adımına geçmek](#verify-that-compose-is-installed) SSH, VM için.</span><span class="sxs-lookup"><span data-stu-id="0e975-119">Once the deployment is finished, [move to next step](#verify-that-compose-is-installed) to SSH to your VM.</span></span> 

<span data-ttu-id="0e975-120">Bunun yerine denetim komut istemini dönüp işlemi arka planda devam dağıtım izin için isteğe bağlı olarak ekleyin `--no-wait` yukarıdaki komut için bayrak.</span><span class="sxs-lookup"><span data-stu-id="0e975-120">Optionally, to instead return control to the prompt and let the deployment continue in the background, add the `--no-wait` flag to the preceding command.</span></span> <span data-ttu-id="0e975-121">Bu işlem birkaç dakika dağıtım devam ederken diğer iş CLI işlemleri yapmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="0e975-121">This process allows you to perform other work in the CLI while the deployment continues for a few minutes.</span></span> <span data-ttu-id="0e975-122">Ardından Docker ana durumuyla ilgili ayrıntıları görüntüleyebilirsiniz [az vm Göster](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="0e975-122">You can then view details about the Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="0e975-123">Aşağıdaki örnek adlı VM durumunu denetler *myDockerVM* (varsayılan ad şablondan - bu adı değişmez) kaynak grubunda adlı *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0e975-123">The following example checks the status of the VM named *myDockerVM* (the default name from the template - don't change this name) in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="0e975-124">Bu komut döndüğünde *başarılı*, dağıtım sona erdi ve sonraki adımda VM için SSH kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e975-124">When this command returns *Succeeded*, the deployment has finished and you can SSH to the VM in the following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="0e975-125">Oluşturma yüklü olduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="0e975-125">Verify that Compose is installed</span></span>
<span data-ttu-id="0e975-126">Dağıtım tamamlandıktan sonra DNS kullanarak, yeni Docker konağına SSH, dağıtım sırasında sağladığınız ad.</span><span class="sxs-lookup"><span data-stu-id="0e975-126">Once the deployment is finished, SSH to your new Docker host using the DNS name you provided during deployment.</span></span> <span data-ttu-id="0e975-127">Kullanabileceğiniz `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` DNS adı dahil olmak üzere, VM ayrıntılarını görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="0e975-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` to view details of your VM, including the DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="0e975-128">VM Oluştur yüklü olduğunu denetlemek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="0e975-128">To check that Compose is installed on the VM, run the following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="0e975-129">Benzer bir çıktı görmeniz *1.6.2 docker compose'u, 4 d 72027 yapı*.</span><span class="sxs-lookup"><span data-stu-id="0e975-129">You see output similar to *docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="0e975-130">Docker ana oluşturmak ve yüklemenize gerek için başka bir yöntem kullandıysanız kendiniz oluşturmak için bkz: [belgeleri oluşturma](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="0e975-130">If you used another method to create a Docker host and need to install Compose yourself, see the [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="0e975-131">Docker-compose.yml yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="0e975-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="0e975-132">Ardından, oluşturduğunuz bir `docker-compose.yml` VM çalıştırmak için Docker kapsayıcıları tanımlamak için yalnızca bir metin yapılandırma dosyası, dosya.</span><span class="sxs-lookup"><span data-stu-id="0e975-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, to define the Docker containers to run on the VM.</span></span> <span data-ttu-id="0e975-133">Görüntünün her kapsayıcı üzerinde çalıştırmak için dosyayı belirtir (veya bir Dockerfile derleme olabilir), gerekli ortam değişkenleri ve bağımlılıkları, bağlantı noktalarını ve kapsayıcılar arasındaki bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="0e975-133">The file specifies the image to run on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and the links between containers.</span></span> <span data-ttu-id="0e975-134">Yml dosya sözdizimi hakkında daha fazla bilgi için bkz: [dosya başvurusu oluşturan](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="0e975-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="0e975-135">Oluşturma *docker-compose.yml* gibi dosya:</span><span class="sxs-lookup"><span data-stu-id="0e975-135">Create the *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="0e975-136">Bazı verileri eklemek için sık kullandığınız metin düzenleyiciyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="0e975-136">Use your favorite text editor to add some data to the file.</span></span> <span data-ttu-id="0e975-137">Aşağıdaki örnek kullanır *VI* Düzenleyicisi:</span><span class="sxs-lookup"><span data-stu-id="0e975-137">The following example uses the *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="0e975-138">Aşağıdaki örnekte, metin dosyasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="0e975-138">Paste the following example into your text file.</span></span> <span data-ttu-id="0e975-139">Bu yapılandırma görüntülerden kullanıyor [DockerHub kayıt defteri](https://registry.hub.docker.com/_/wordpress/) WordPress (açık kaynak blog ve içerik yönetim sistemi) ve bağlantılı arka uç MariaDB SQL veritabanını yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="0e975-139">This configuration uses images from the [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) to install WordPress (the open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="0e975-140">Kendi girin *MYSQL_ROOT_PASSWORD* gibi:</span><span class="sxs-lookup"><span data-stu-id="0e975-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

```sh
wordpress:
  image: wordpress
  links:
    - db:mysql
  ports:
    - 80:80

db:
  image: mariadb
  environment:
    MYSQL_ROOT_PASSWORD: <your password>
```

## <a name="start-the-containers-with-compose"></a><span data-ttu-id="0e975-141">Kapsayıcıları oluşturma ile Başlat</span><span class="sxs-lookup"><span data-stu-id="0e975-141">Start the containers with Compose</span></span>
<span data-ttu-id="0e975-142">Aynı dizinde, *docker-compose.yml* dosya, aşağıdaki komutu çalıştırın (ortamınıza bağlı olarak çalıştırmanız gerekebilir `docker-compose` kullanarak `sudo`):</span><span class="sxs-lookup"><span data-stu-id="0e975-142">In the same directory as your *docker-compose.yml* file, run the following command (depending on your environment, you might need to run `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="0e975-143">Bu komut belirtilen Docker kapsayıcıları başlatır *docker-compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="0e975-143">This command starts the Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="0e975-144">Bir veya iki bu adımı tamamlamak için dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="0e975-144">It takes a minute or two for this step to complete.</span></span> <span data-ttu-id="0e975-145">Aşağıdaki örneğe benzer bir çıktı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="0e975-145">You see output similar to the following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="0e975-146">Kullandığınızdan emin olun **-d** kapsayıcıları arka planda sürekli çalışmasını böylece üzerinde başlatma seçeneği.</span><span class="sxs-lookup"><span data-stu-id="0e975-146">Be sure to use the **-d** option on start-up so that the containers run in the background continuously.</span></span>


<span data-ttu-id="0e975-147">Kapsayıcılar yukarı olduğunu doğrulamak için aşağıdakileri yazın `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="0e975-147">To verify that the containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="0e975-148">Benzer bir şey görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="0e975-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="0e975-149">Şimdi doğrudan bağlantı noktası 80 üzerinde VM üzerinde WordPress bağlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0e975-149">You can now connect to WordPress directly on the VM on port 80.</span></span> <span data-ttu-id="0e975-150">Bir web tarayıcısı açın ve VM DNS adını girin (gibi `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="0e975-150">Open a web browser and enter the DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="0e975-151">WordPress görmelisiniz başlangıç ekranında, burada yüklemeyi tamamlamak ve uygulama ile çalışmaya başlama.</span><span class="sxs-lookup"><span data-stu-id="0e975-151">You should now see the WordPress start screen, where you can complete the installation and get started with the application.</span></span>

![WordPress başlangıç ekranı][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="0e975-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0e975-153">Next steps</span></span>
* <span data-ttu-id="0e975-154">Git [Docker VM uzantısı Kullanıcı Kılavuzu'na](https://github.com/Azure/azure-docker-extension/blob/master/README.md) Docker ve oluşturma, Docker VM yapılandırmak daha fazla seçenek için.</span><span class="sxs-lookup"><span data-stu-id="0e975-154">Go to the [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options to configure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="0e975-155">Örneğin, bir (dönüştürülen JSON olarak) oluşturma yml dosyayı yerleştirmek için doğrudan Docker VM uzantısı yapılandırmasında seçenektir.</span><span class="sxs-lookup"><span data-stu-id="0e975-155">For example, one option is to put the Compose yml file (converted to JSON) directly in the configuration of the Docker VM extension.</span></span>
* <span data-ttu-id="0e975-156">Kullanıma [komut satırı başvurusu oluşturan](http://docs.docker.com/compose/reference/) ve [Kullanıcı Kılavuzu](http://docs.docker.com/compose/) oluşturma ve birden çok kapsayıcı uygulamaları dağıtmaya diğer örnekler için.</span><span class="sxs-lookup"><span data-stu-id="0e975-156">Check out the [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="0e975-157">Bir Azure Resource Manager şablonu ya da kullanmak, kendi ya da bir katkısı [topluluk](https://azure.microsoft.com/documentation/templates/), Docker ve oluşturma ile ayarlanmış bir uygulama ile bir Azure VM dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="0e975-157">Use an Azure Resource Manager template, either your own or one contributed from the [community](https://azure.microsoft.com/documentation/templates/), to deploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="0e975-158">Örneğin, [bir WordPress blog docker'la dağıtmak](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) hızlı bir şekilde bir Ubuntu VM bir MySQL arka uç ile WordPress dağıtmak için şablon kullanır Docker ve oluştur.</span><span class="sxs-lookup"><span data-stu-id="0e975-158">For example, the [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose to quickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="0e975-159">Docker Compose Docker Swarm kümesi ile tümleştirme deneyin.</span><span class="sxs-lookup"><span data-stu-id="0e975-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="0e975-160">Bkz: [kullanarak oluşturan Swarm ile](https://docs.docker.com/compose/swarm/) senaryoları için.</span><span class="sxs-lookup"><span data-stu-id="0e975-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
