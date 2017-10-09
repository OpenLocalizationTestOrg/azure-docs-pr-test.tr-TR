---
title: "aaaUse Docker Compose azure'da bir Linux VM üzerinde | Microsoft Docs"
description: "Azure CLI toouse Docker ve oluşturma ile Linux sanal makinelerde nasıl hello"
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
ms.openlocfilehash: cf7254ad4813ccdc641fcacbb06ed1514a93cee5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-docker-and-compose-toodefine-and-run-a-multi-container-application-in-azure"></a><span data-ttu-id="283fc-103">Docker ve oluşturma toodefine ile başlatılan alın ve Azure'da çok kapsayıcı uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="283fc-103">Get started with Docker and Compose toodefine and run a multi-container application in Azure</span></span>
<span data-ttu-id="283fc-104">İle [oluşturma](http://github.com/docker/compose), basit bir metin dosyası toodefine birden çok Docker kapsayıcıları için oluşan bir uygulama kullanın.</span><span class="sxs-lookup"><span data-stu-id="283fc-104">With [Compose](http://github.com/docker/compose), you use a simple text file toodefine an application consisting of multiple Docker containers.</span></span> <span data-ttu-id="283fc-105">Ardından, her şeyi yapar tek bir komut uygulamanızda Yukarı Döndür toodeploy tanımlanan ortamınızı.</span><span class="sxs-lookup"><span data-stu-id="283fc-105">You then spin up your application in a single command that does everything toodeploy your defined environment.</span></span> <span data-ttu-id="283fc-106">Örnek olarak, bu makalede nasıl tooquickly bir arka uç ile bir WordPress blog MariaDB SQL veritabanı bir Ubuntu VM ayarlanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="283fc-106">As an example, this article shows you how tooquickly set up a WordPress blog with a backend MariaDB SQL database on an Ubuntu VM.</span></span> <span data-ttu-id="283fc-107">Daha karmaşık uygulamaları oluşturma tooset de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="283fc-107">You can also use Compose tooset up more complex applications.</span></span>


## <a name="set-up-a-linux-vm-as-a-docker-host"></a><span data-ttu-id="283fc-108">Bir Linux VM Docker ana bilgisayar olarak ayarlama</span><span class="sxs-lookup"><span data-stu-id="283fc-108">Set up a Linux VM as a Docker host</span></span>
<span data-ttu-id="283fc-109">Çeşitli Azure yordamları ve kullanılabilir görüntüler veya Resource Manager şablonları hello Azure Marketi toocreate bir Linux VM kullanın ve Docker ana bilgisayar olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="283fc-109">You can use various Azure procedures and available images or Resource Manager templates in hello Azure Marketplace toocreate a Linux VM and set it up as a Docker host.</span></span> <span data-ttu-id="283fc-110">Örneğin, [hello Docker VM uzantısı toodeploy ortamınızı kullanarak](dockerextension.md) tooquickly oluşturma bir Ubuntu VM hello Azure Docker VM uzantısı ile kullanarak bir [hızlı başlatma şablonunu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="283fc-110">For example, see [Using hello Docker VM Extension toodeploy your environment](dockerextension.md) tooquickly create an Ubuntu VM with hello Azure Docker VM extension by using a [quickstart template](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> 

<span data-ttu-id="283fc-111">Merhaba Docker VM uzantısı kullandığınızda, VM otomatik olarak Docker ana bilgisayar olarak ayarlanır ve oluşturma zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="283fc-111">When you use hello Docker VM extension, your VM is automatically set up as a Docker host and Compose is already installed.</span></span>


### <a name="create-docker-host-with-azure-cli-20"></a><span data-ttu-id="283fc-112">Azure CLI 2.0 ile Docker konak oluştur</span><span class="sxs-lookup"><span data-stu-id="283fc-112">Create Docker host with Azure CLI 2.0</span></span>
<span data-ttu-id="283fc-113">Son yükleme hello [Azure CLI 2.0](/cli/azure/install-az-cli2) ve tooan Azure hesabını kullanarak oturum [az oturum açma](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="283fc-113">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="283fc-114">İlk olarak, Docker ortamınız için bir kaynak grubu oluşturmak [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="283fc-114">First, create a resource group for your Docker environment with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="283fc-115">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westus* konumu:</span><span class="sxs-lookup"><span data-stu-id="283fc-115">hello following example creates a resource group named *myResourceGroup* in hello *westus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

<span data-ttu-id="283fc-116">Ardından, bir VM'yi dağıtmak [az grup dağıtımı oluşturmak](/cli/azure/group/deployment#create) hello Azure Docker VM uzantısını içeren [github'daki bu Azure Resource Manager şablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span><span class="sxs-lookup"><span data-stu-id="283fc-116">Next, deploy a VM with [az group deployment create](/cli/azure/group/deployment#create) that includes hello Azure Docker VM extension from [this Azure Resource Manager template on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu).</span></span> <span data-ttu-id="283fc-117">Kendi değerlerini sağlamanız *newStorageAccountName*, *adminUsername*, *Admınpassword*, ve *dnsNameForPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="283fc-117">Provide your own values for *newStorageAccountName*, *adminUsername*, *adminPassword*, and *dnsNameForPublicIP*:</span></span>

```azurecli
az group deployment create --resource-group myResourceGroup \
  --parameters '{"newStorageAccountName": {"value": "mystorageaccount"},
    "adminUsername": {"value": "azureuser"},
    "adminPassword": {"value": "P@ssw0rd!"},
    "dnsNameForPublicIP": {"value": "mypublicdns"}}' \
  --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/docker-simple-on-ubuntu/azuredeploy.json
```

<span data-ttu-id="283fc-118">Merhaba dağıtım toofinish birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="283fc-118">It takes a few minutes for hello deployment toofinish.</span></span> <span data-ttu-id="283fc-119">Merhaba dağıtım tamamlandıktan sonra [toonext adım taşıma](#verify-that-compose-is-installed) tooSSH tooyour VM.</span><span class="sxs-lookup"><span data-stu-id="283fc-119">Once hello deployment is finished, [move toonext step](#verify-that-compose-is-installed) tooSSH tooyour VM.</span></span> 

<span data-ttu-id="283fc-120">İsteğe bağlı olarak tooinstead dönüş denetimi toohello istemi ve let hello dağıtım hello arka planda devam hello ekleyin `--no-wait` komutu önceki toohello bayrak.</span><span class="sxs-lookup"><span data-stu-id="283fc-120">Optionally, tooinstead return control toohello prompt and let hello deployment continue in hello background, add hello `--no-wait` flag toohello preceding command.</span></span> <span data-ttu-id="283fc-121">Bu işlem tooperform sağlar hello hello dağıtım için bir kaç dakika devam ederken CLI diğer iş.</span><span class="sxs-lookup"><span data-stu-id="283fc-121">This process allows you tooperform other work in hello CLI while hello deployment continues for a few minutes.</span></span> <span data-ttu-id="283fc-122">Ardından hello Docker ana bilgisayar durumu ile ilgili ayrıntıları görüntüleyebilirsiniz [az vm Göster](/cli/azure/vm#show).</span><span class="sxs-lookup"><span data-stu-id="283fc-122">You can then view details about hello Docker host status with [az vm show](/cli/azure/vm#show).</span></span> <span data-ttu-id="283fc-123">Merhaba aşağıdaki örnek hello durumunu hello adlı VM denetler *myDockerVM* (Merhaba hello şablondan varsayılan adı - bu adı değiştirmemeniz) adlı hello kaynak grubunda *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="283fc-123">hello following example checks hello status of hello VM named *myDockerVM* (hello default name from hello template - don't change this name) in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm show \
    --resource-group myResourceGroup \
    --name myDockerVM \
    --query [provisioningState] \
    --output tsv
```

<span data-ttu-id="283fc-124">Bu komut döndüğünde *başarılı*hello dağıtımı tamamlandı ve SSH toohello VM adım aşağıdaki hello de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="283fc-124">When this command returns *Succeeded*, hello deployment has finished and you can SSH toohello VM in hello following step.</span></span>


## <a name="verify-that-compose-is-installed"></a><span data-ttu-id="283fc-125">Oluşturma yüklü olduğunu doğrulayın</span><span class="sxs-lookup"><span data-stu-id="283fc-125">Verify that Compose is installed</span></span>
<span data-ttu-id="283fc-126">Merhaba DNS adını kullanarak SSH tooyour yeni Docker ana bilgisayar Hello dağıtım tamamlandıktan sonra dağıtım sırasında sağladığınız.</span><span class="sxs-lookup"><span data-stu-id="283fc-126">Once hello deployment is finished, SSH tooyour new Docker host using hello DNS name you provided during deployment.</span></span> <span data-ttu-id="283fc-127">Kullanabileceğiniz `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` hello DNS adı dahil olmak üzere, VM tooview ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="283fc-127">You can use  `az vm show -g myResourceGroup -n myDockerVM -d --query [fqdns] -o tsv` tooview details of your VM, including hello DNS name.</span></span>

```bash
ssh azureuser@mypublicdns.westus.cloudapp.azure.com
```

<span data-ttu-id="283fc-128">Oluşturan toocheck hello üzerinde VM, komutu aşağıdaki hello çalıştırmak yüklenir:</span><span class="sxs-lookup"><span data-stu-id="283fc-128">toocheck that Compose is installed on hello VM, run hello following command:</span></span>

```bash
docker-compose --version
```

<span data-ttu-id="283fc-129">Çok benzer bir çıktı görmeniz*1.6.2 docker compose'u, 4 d 72027 yapı*.</span><span class="sxs-lookup"><span data-stu-id="283fc-129">You see output similar too*docker-compose 1.6.2, build 4d72027*.</span></span>

> [!TIP]
> <span data-ttu-id="283fc-130">Başka bir yöntem toocreate Docker ana kullanılan ve tooinstall kendiniz oluşturan varsa hello bkz [belgeleri oluşturma](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span><span class="sxs-lookup"><span data-stu-id="283fc-130">If you used another method toocreate a Docker host and need tooinstall Compose yourself, see hello [Compose documentation](https://github.com/docker/compose/blob/882dc673ce84b0b29cd59b6815cb93f74a6c4134/docs/install.md).</span></span>


## <a name="create-a-docker-composeyml-configuration-file"></a><span data-ttu-id="283fc-131">Docker-compose.yml yapılandırma dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="283fc-131">Create a docker-compose.yml configuration file</span></span>
<span data-ttu-id="283fc-132">Ardından, oluşturduğunuz bir `docker-compose.yml` yalnızca bir metin yapılandırma dosyası, toodefine hello Docker kapsayıcıları toorun hello VM üzerinde dosya.</span><span class="sxs-lookup"><span data-stu-id="283fc-132">Next you create a `docker-compose.yml` file, which is just a text configuration file, toodefine hello Docker containers toorun on hello VM.</span></span> <span data-ttu-id="283fc-133">Merhaba dosya her kapsayıcı hello görüntü toorun belirtir (veya bir Dockerfile derleme olabilir), gerekli ortam değişkenleri ve bağımlılıkları, bağlantı noktalarını ve kapsayıcılar arasındaki hello bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="283fc-133">hello file specifies hello image toorun on each container (or it could be a build from a Dockerfile), necessary environment variables and dependencies, ports, and hello links between containers.</span></span> <span data-ttu-id="283fc-134">Yml dosya sözdizimi hakkında daha fazla bilgi için bkz: [dosya başvurusu oluşturan](https://docs.docker.com/compose/compose-file/).</span><span class="sxs-lookup"><span data-stu-id="283fc-134">For details on yml file syntax, see [Compose file reference](https://docs.docker.com/compose/compose-file/).</span></span>

<span data-ttu-id="283fc-135">Merhaba oluşturma *docker-compose.yml* gibi dosya:</span><span class="sxs-lookup"><span data-stu-id="283fc-135">Create hello *docker-compose.yml* file as follows:</span></span>

```bash
touch docker-compose.yml
```

<span data-ttu-id="283fc-136">Sık kullandığınız metin düzenleyicisi tooadd bazı veri toohello dosyasını kullanın.</span><span class="sxs-lookup"><span data-stu-id="283fc-136">Use your favorite text editor tooadd some data toohello file.</span></span> <span data-ttu-id="283fc-137">Merhaba aşağıdaki örnek kullanır hello *VI* Düzenleyicisi:</span><span class="sxs-lookup"><span data-stu-id="283fc-137">hello following example uses hello *vi* editor:</span></span>

```bash
vi docker-compose.yml
```

<span data-ttu-id="283fc-138">Örnek metin dosyanıza aşağıdaki hello yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="283fc-138">Paste hello following example into your text file.</span></span> <span data-ttu-id="283fc-139">Bu yapılandırma hello görüntülerden kullanıyor [DockerHub kayıt defteri](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (Merhaba açık kaynak blog ve içerik yönetim sistemi) ve bağlantılı arka uç MariaDB SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="283fc-139">This configuration uses images from hello [DockerHub Registry](https://registry.hub.docker.com/_/wordpress/) tooinstall WordPress (hello open source blogging and content management system) and a linked backend MariaDB SQL database.</span></span> <span data-ttu-id="283fc-140">Kendi girin *MYSQL_ROOT_PASSWORD* gibi:</span><span class="sxs-lookup"><span data-stu-id="283fc-140">Enter your own *MYSQL_ROOT_PASSWORD* as follows:</span></span>

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

## <a name="start-hello-containers-with-compose"></a><span data-ttu-id="283fc-141">Merhaba kapsayıcılara oluşturma ile Başlat</span><span class="sxs-lookup"><span data-stu-id="283fc-141">Start hello containers with Compose</span></span>
<span data-ttu-id="283fc-142">İçinde aynı hello olarak dizin, *docker-compose.yml* dosyası, komut aşağıdaki hello çalıştırın (ortamınıza bağlı olarak toorun gerekebilecek `docker-compose` kullanarak `sudo`):</span><span class="sxs-lookup"><span data-stu-id="283fc-142">In hello same directory as your *docker-compose.yml* file, run hello following command (depending on your environment, you might need toorun `docker-compose` using `sudo`):</span></span>

```bash
docker-compose up -d
```

<span data-ttu-id="283fc-143">Bu komut belirtilen hello Docker kapsayıcıları başlatır *docker-compose.yml*.</span><span class="sxs-lookup"><span data-stu-id="283fc-143">This command starts hello Docker containers specified in *docker-compose.yml*.</span></span> <span data-ttu-id="283fc-144">Bir veya iki Bu adım toocomplete için dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="283fc-144">It takes a minute or two for this step toocomplete.</span></span> <span data-ttu-id="283fc-145">Aşağıdaki örnek çıkış benzer toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="283fc-145">You see output similar toohello following example:</span></span>

```bash
Creating wordpress_db_1...
Creating wordpress_wordpress_1...
...
```

> [!NOTE]
> <span data-ttu-id="283fc-146">Emin toouse hello olması **-d** Merhaba kapsayıcılara hello arka planda sürekli çalışmasını böylece üzerinde başlatma seçeneği.</span><span class="sxs-lookup"><span data-stu-id="283fc-146">Be sure toouse hello **-d** option on start-up so that hello containers run in hello background continuously.</span></span>


<span data-ttu-id="283fc-147">Merhaba kapsayıcılara hazır tooverify türü `docker-compose ps`.</span><span class="sxs-lookup"><span data-stu-id="283fc-147">tooverify that hello containers are up, type `docker-compose ps`.</span></span> <span data-ttu-id="283fc-148">Benzer bir şey görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="283fc-148">You should see something like:</span></span>

```bash
        Name                       Command               State         Ports
-----------------------------------------------------------------------------------
azureuser_db_1          docker-entrypoint.sh mysqld      Up      3306/tcp
azureuser_wordpress_1   docker-entrypoint.sh apach ...   Up      0.0.0.0:80->80/tcp
```

<span data-ttu-id="283fc-149">Şimdi doğrudan hello VM bağlantı noktası 80 üzerinde tooWordPress bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="283fc-149">You can now connect tooWordPress directly on hello VM on port 80.</span></span> <span data-ttu-id="283fc-150">Bir web tarayıcısı açın ve VM hello DNS adını girin (gibi `http://mypublicdns.westus.cloudapp.azure.com`).</span><span class="sxs-lookup"><span data-stu-id="283fc-150">Open a web browser and enter hello DNS name of your VM (such as `http://mypublicdns.westus.cloudapp.azure.com`).</span></span> <span data-ttu-id="283fc-151">WordPress başlangıç ekranında, burada hello yüklemeyi tamamlamak ve Merhaba uygulaması ile çalışmaya başlama hello görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="283fc-151">You should now see hello WordPress start screen, where you can complete hello installation and get started with hello application.</span></span>

![WordPress başlangıç ekranı][wordpress_start]

## <a name="next-steps"></a><span data-ttu-id="283fc-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="283fc-153">Next steps</span></span>
* <span data-ttu-id="283fc-154">Toohello Git [Docker VM uzantısı Kullanıcı Kılavuzu'na](https://github.com/Azure/azure-docker-extension/blob/master/README.md) daha fazla seçenekleri tooconfigure Docker ve Docker VM oluşturma.</span><span class="sxs-lookup"><span data-stu-id="283fc-154">Go toohello [Docker VM extension user guide](https://github.com/Azure/azure-docker-extension/blob/master/README.md) for more options tooconfigure Docker and Compose in your Docker VM.</span></span> <span data-ttu-id="283fc-155">Örneğin, bir seçenek tooput hello oluşturma yml (dönüştürülen tooJSON) doğrudan hello Docker VM uzantısı hello yapılandırmasını dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="283fc-155">For example, one option is tooput hello Compose yml file (converted tooJSON) directly in hello configuration of hello Docker VM extension.</span></span>
* <span data-ttu-id="283fc-156">Merhaba denetleyin [komut satırı başvurusu oluşturan](http://docs.docker.com/compose/reference/) ve [Kullanıcı Kılavuzu](http://docs.docker.com/compose/) oluşturma ve birden çok kapsayıcı uygulamaları dağıtmaya diğer örnekler için.</span><span class="sxs-lookup"><span data-stu-id="283fc-156">Check out hello [Compose command-line reference](http://docs.docker.com/compose/reference/) and [user guide](http://docs.docker.com/compose/) for more examples of building and deploying multi-container apps.</span></span>
* <span data-ttu-id="283fc-157">Bir Azure Resource Manager şablonu ya da kullanmak, veya bir tane katkıda hello [topluluk](https://azure.microsoft.com/documentation/templates/), toodeploy Docker ve bir uygulama ile bir Azure VM oluşturma ile ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="283fc-157">Use an Azure Resource Manager template, either your own or one contributed from hello [community](https://azure.microsoft.com/documentation/templates/), toodeploy an Azure VM with Docker and an application set up with Compose.</span></span> <span data-ttu-id="283fc-158">Örneğin, hello [bir WordPress blog docker'la dağıtmak](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) oluşturma tooquickly bir Ubuntu VM bir MySQL arka uç ile WordPress dağıtmak ve şablonu Docker kullanır.</span><span class="sxs-lookup"><span data-stu-id="283fc-158">For example, hello [Deploy a WordPress blog with Docker](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-wordpress-mysql) template uses Docker and Compose tooquickly deploy WordPress with a MySQL backend on an Ubuntu VM.</span></span>
* <span data-ttu-id="283fc-159">Docker Compose Docker Swarm kümesi ile tümleştirme deneyin.</span><span class="sxs-lookup"><span data-stu-id="283fc-159">Try integrating Docker Compose with a Docker Swarm cluster.</span></span> <span data-ttu-id="283fc-160">Bkz: [kullanarak oluşturan Swarm ile](https://docs.docker.com/compose/swarm/) senaryoları için.</span><span class="sxs-lookup"><span data-stu-id="283fc-160">See [Using Compose with Swarm](https://docs.docker.com/compose/swarm/) for scenarios.</span></span>

<!--Image references-->

[wordpress_start]: media/docker-compose-quickstart/WordPress.png
