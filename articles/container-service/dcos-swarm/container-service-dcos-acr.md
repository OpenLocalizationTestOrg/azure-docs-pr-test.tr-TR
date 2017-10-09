---
title: "bir Azure DC/OS kümesi ile aaaUsing ACR | Microsoft Docs"
description: "Azure kapsayıcı hizmeti DC/OS kümesinde ile bir Azure kapsayıcı kayıt defteri kullanma"
services: container-service
documentationcenter: 
author: julienstroheker
manager: dcaro
editor: 
tags: acs, azure-container-service, acr, azure-container-registry
keywords: "Docker, kapsayıcıları, mikro hizmetler, Mesos, Azure, dosya paylaşımı, CIFS"
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/23/2017
ms.author: juliens
ms.custom: mvc
ms.openlocfilehash: 9a2802da788b50147d8b4259436bdcdb0c929db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-acr-with-a-dcos-cluster-toodeploy-your-application"></a><span data-ttu-id="3acfa-104">ACR DC/OS kümesi toodeploy ile uygulamanızı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3acfa-104">Use ACR with a DC/OS cluster toodeploy your application</span></span>

<span data-ttu-id="3acfa-105">Bu makalede, biz keşfedin nasıl toouse Azure kapsayıcı kayıt defteri DC/OS kümesine sahip.</span><span class="sxs-lookup"><span data-stu-id="3acfa-105">In this article, we explore how toouse Azure Container Registry with a DC/OS cluster.</span></span> <span data-ttu-id="3acfa-106">ACR kullanarak tooprivately deposu sağlar ve kapsayıcı görüntüleri yönetin.</span><span class="sxs-lookup"><span data-stu-id="3acfa-106">Using ACR allows you tooprivately store and manage container images.</span></span> <span data-ttu-id="3acfa-107">Bu öğretici hello aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="3acfa-107">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3acfa-108">Azure kapsayıcı kayıt defteri (gerekirse) dağıtın</span><span class="sxs-lookup"><span data-stu-id="3acfa-108">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="3acfa-109">DC/OS kümesinde ACR kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3acfa-109">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="3acfa-110">Bir görüntü toohello Azure kapsayıcı kayıt defteri karşıya</span><span class="sxs-lookup"><span data-stu-id="3acfa-110">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="3acfa-111">Bir kapsayıcı görüntüsü hello Azure kapsayıcı kayıt defteri ' çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3acfa-111">Run a container image from hello Azure Container Registry</span></span>

<span data-ttu-id="3acfa-112">Bir ACS DC/küme toocomplete hello bu öğreticideki adımlar işletim sistemi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3acfa-112">You need an ACS DC/OS cluster toocomplete hello steps in this tutorial.</span></span> <span data-ttu-id="3acfa-113">Gerekirse, [bu komut dosyası örneği](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) sizin için bir tane oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3acfa-113">If needed, [this script sample](./../kubernetes/scripts/container-service-cli-deploy-dcos.md) can create one for you.</span></span>

<span data-ttu-id="3acfa-114">Bu öğretici hello Azure CLI Sürüm 2.0.4 gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="3acfa-114">This tutorial requires hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="3acfa-115">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="3acfa-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="3acfa-116">Tooupgrade gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="3acfa-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

## <a name="deploy-azure-container-registry"></a><span data-ttu-id="3acfa-117">Azure kapsayıcı kayıt defteri dağıtın</span><span class="sxs-lookup"><span data-stu-id="3acfa-117">Deploy Azure Container Registry</span></span>

<span data-ttu-id="3acfa-118">Gerekiyorsa, Azure kapsayıcı kayıt defteri ile Merhaba oluşturun [az acr oluşturmak](/cli/azure/acr#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="3acfa-118">If needed, create an Azure Container registry with hello [az acr create](/cli/azure/acr#create) command.</span></span> 

<span data-ttu-id="3acfa-119">Merhaba aşağıdaki örnekte oluşturur kayıt defteri ile bir rastgele adı oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="3acfa-119">hello following example creates a registry with a randomly generate name.</span></span> <span data-ttu-id="3acfa-120">Merhaba kayıt defteri hello kullanarak bir yönetici hesabıyla aynı zamanda yapılandırılmış `--admin-enabled` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="3acfa-120">hello registry is also configured with an admin account using hello `--admin-enabled` argument.</span></span>

```azurecli-interactive
az acr create --resource-group myResourceGroup --name myContainerRegistry$RANDOM --sku Basic --admin-enabled true
```

<span data-ttu-id="3acfa-121">Merhaba kayıt defteri oluşturulduktan sonra veri benzer toohello aşağıdaki hello Azure CLI çıkarır.</span><span class="sxs-lookup"><span data-stu-id="3acfa-121">Once hello registry has been created, hello Azure CLI outputs data similar toohello following.</span></span> <span data-ttu-id="3acfa-122">Merhaba not edin `name` ve `loginServer`, bunlar daha sonraki adımlarda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3acfa-122">Take note of hello `name` and `loginServer`, these are used in later steps.</span></span>

```azurecli
{
  "adminUserEnabled": false,
  "creationDate": "2017-06-06T03:40:56.511597+00:00",
  "id": "/subscriptions/f2799821-a08a-434e-9128-454ec4348b10/resourcegroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myContainerRegistry23489",
  "location": "eastus",
  "loginServer": "mycontainerregistry23489.azurecr.io",
  "name": "myContainerRegistry23489",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "mycontainerregistr034017"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

<span data-ttu-id="3acfa-123">Merhaba kapsayıcı kayıt defteri Hello kullanarak kimlik bilgilerini alma [az acr kimlik bilgisi Göster](/cli/azure/acr/credential) komutu.</span><span class="sxs-lookup"><span data-stu-id="3acfa-123">Get hello container registry credentials using hello [az acr credential show](/cli/azure/acr/credential) command.</span></span> <span data-ttu-id="3acfa-124">Yedek hello `--name` bir hello son adımda not ettiğiniz hello ile.</span><span class="sxs-lookup"><span data-stu-id="3acfa-124">Substitute hello `--name` with hello one noted in hello last step.</span></span> <span data-ttu-id="3acfa-125">Not bir parola bir sonraki adımda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="3acfa-125">Take note of one password, it is needed in a later step.</span></span>

```azurecli-interactive
az acr credential show --name myContainerRegistry23489
```

<span data-ttu-id="3acfa-126">Azure kapsayıcı kayıt defteri hakkında daha fazla bilgi için bkz: [giriş tooprivate Docker kapsayıcısı kayıt defterleri](../../container-registry/container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="3acfa-126">For more information on Azure Container Registry, see [Introduction tooprivate Docker container registries](../../container-registry/container-registry-intro.md).</span></span> 

## <a name="manage-acr-authentication"></a><span data-ttu-id="3acfa-127">ACR kimlik doğrulamasını yönetmek</span><span class="sxs-lookup"><span data-stu-id="3acfa-127">Manage ACR authentication</span></span>

<span data-ttu-id="3acfa-128">toofirst özel bir kayıt defteri toopush ve çekme görüntüdür hello geleneksel şekilde hello kayıt defteri ile kimlik doğrulaması.</span><span class="sxs-lookup"><span data-stu-id="3acfa-128">hello conventional way toopush and pull image from a private registry is toofirst authenticate with hello registry.</span></span> <span data-ttu-id="3acfa-129">toodo Merhaba, kullanacağınız `docker login` tooaccess hello özel kayıt defteri gereken herhangi bir istemci üzerinde komutu.</span><span class="sxs-lookup"><span data-stu-id="3acfa-129">toodo so, you would use hello `docker login` command on any client that needs tooaccess hello private registry.</span></span> <span data-ttu-id="3acfa-130">DC/OS kümesi tümü ACR hello ile kimlik doğrulaması toobe gerekir, birçok düğümleri içerebileceğinden bu işlem boyunca yararlı tooautomate olduğundan her düğümü.</span><span class="sxs-lookup"><span data-stu-id="3acfa-130">Because a DC/OS cluster can contain many nodes, all of which need toobe authenticated with hello ACR, it is helpful tooautomate this process across each node.</span></span> 

### <a name="create-shared-storage"></a><span data-ttu-id="3acfa-131">Paylaşılan depolama alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="3acfa-131">Create shared storage</span></span>

<span data-ttu-id="3acfa-132">Bu işlem, hello kümedeki her düğümde takıldıktan bir Azure dosya paylaşımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="3acfa-132">This process uses an Azure file share that has been mounted on each node in hello cluster.</span></span> <span data-ttu-id="3acfa-133">Paylaşılan depolama alanı zaten ayarlamadıysanız bkz [bir DC/OS küme içindeki bir dosya paylaşımı Kurulum](container-service-dcos-fileshare.md).</span><span class="sxs-lookup"><span data-stu-id="3acfa-133">If you have not already set up shared storage, see [Setup a file share inside a DC/OS cluster](container-service-dcos-fileshare.md).</span></span>

### <a name="configure-acr-authentication"></a><span data-ttu-id="3acfa-134">ACR kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3acfa-134">Configure ACR authentication</span></span>

<span data-ttu-id="3acfa-135">İlk olarak, hello DC/OS ana ve bir değişkende saklayın hello FQDN'sini alın.</span><span class="sxs-lookup"><span data-stu-id="3acfa-135">First, get hello FQDN of hello DC/OS master and store it in a variable.</span></span>

```azurecli-interactive
FQDN=$(az acs list --resource-group myResourceGroup --query "[0].masterProfile.fqdn" --output tsv)
```

<span data-ttu-id="3acfa-136">Bir SSH bağlantısı hello Yöneticisi (ya da hello ilk ana) DC/OS tabanlı kümenizin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3acfa-136">Create an SSH connection with hello master (or hello first master) of your DC/OS-based cluster.</span></span> <span data-ttu-id="3acfa-137">Varsayılan olmayan bir değer hello kümesi oluştururken kullanıldıysa hello kullanıcı adını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="3acfa-137">Update hello user name if a non-default value was used when creating hello cluster.</span></span>

```azurecli-interactive
ssh azureuser@$FQDN
```

<span data-ttu-id="3acfa-138">Komut toologin toohello Azure kapsayıcı kayıt defteri aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3acfa-138">Run hello following command toologin toohello Azure Container Registry.</span></span> <span data-ttu-id="3acfa-139">Hello yerine `--username` hello kapsayıcı kayıt defteri ve hello hello adıyla `--password` sağlanan hello parolaları biriyle.</span><span class="sxs-lookup"><span data-stu-id="3acfa-139">Replace hello `--username` with hello name of hello container registry, and hello `--password` with one of hello provided passwords.</span></span> <span data-ttu-id="3acfa-140">Merhaba son bağımsız değişken Değiştir *mycontainerregistry.azurecr.io* hello kapsayıcı kayıt defteri hello örnekte hello loginServer ada sahip.</span><span class="sxs-lookup"><span data-stu-id="3acfa-140">Replace hello last argument *mycontainerregistry.azurecr.io* in hello example with hello loginServer name of hello container registry.</span></span> 

<span data-ttu-id="3acfa-141">Bu komut hello kimlik doğrulaması değerleri hello altında yerel olarak depolar `~/.docker` yolu.</span><span class="sxs-lookup"><span data-stu-id="3acfa-141">This command stores hello authentication values locally under hello `~/.docker` path.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry.azurecr.io
```

<span data-ttu-id="3acfa-142">Merhaba kapsayıcı kayıt defteri kimlik doğrulama değerleri içeren sıkıştırılmış bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3acfa-142">Create a compressed file that contains hello container registry authentication values.</span></span>

```azurecli-interactive
tar czf docker.tar.gz .docker
```

<span data-ttu-id="3acfa-143">Bu dosya toohello Küme Paylaşılan depolama kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="3acfa-143">Copy this file toohello cluster shared storage.</span></span> <span data-ttu-id="3acfa-144">Bu adım hello dosya hello DC/OS kümenin tüm düğümlerinde kullanılabilir hale getirir.</span><span class="sxs-lookup"><span data-stu-id="3acfa-144">This step makes hello file available on all nodes of hello DC/OS cluster.</span></span>

```azurecli-interactive
cp docker.tar.gz /mnt/share/dcosshare
```

## <a name="upload-image-tooacr"></a><span data-ttu-id="3acfa-145">Görüntü tooACR karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="3acfa-145">Upload image tooACR</span></span>

<span data-ttu-id="3acfa-146">Şimdi bir geliştirme makine ya da herhangi bir yüklü Docker sistemiyle, bir görüntü oluşturun ve toohello Azure kapsayıcı kayıt defteri yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3acfa-146">Now from a development machine, or any other system with Docker installed, create an image and upload it toohello Azure Container Registry.</span></span>

<span data-ttu-id="3acfa-147">Merhaba Ubuntu görüntüsünden bir kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="3acfa-147">Create a container from hello Ubuntu image.</span></span>

```azurecli-interactive
docker run ubunut --name base-image
```

<span data-ttu-id="3acfa-148">Şimdi hello kapsayıcı yeni bir görüntüsünü yakalayın.</span><span class="sxs-lookup"><span data-stu-id="3acfa-148">Now capture hello container into a new image.</span></span> <span data-ttu-id="3acfa-149">Merhaba görüntü adı gerekiyor tooinclude hello `loginServer` hello kapsayıcı registrywith biçimlerinin bir adı `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="3acfa-149">hello image name needs tooinclude hello `loginServer` name of hello container registrywith a format of `loginServer/imageName`.</span></span>

```azurecli-interactive
docker -H tcp://localhost:2375 commit base-image mycontainerregistry30678.azurecr.io/dcos-demo
````

<span data-ttu-id="3acfa-150">Hello Azure kapsayıcı kayıt defteri uygulamasına oturum açın.</span><span class="sxs-lookup"><span data-stu-id="3acfa-150">Login into hello Azure Container Registry.</span></span> <span data-ttu-id="3acfa-151">Merhaba adı hello loginServer adla değiştirin,--kullanıcıadı hello adını hello kapsayıcı kayıt defteri ve hello--sağlanan hello parolaları biriyle parola ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="3acfa-151">Replace hello name with hello loginServer name, hello --username with hello name of hello container registry, and hello --password with one of hello provided passwords.</span></span>

```azurecli-interactive
docker login --username=myContainerRegistry23489 --password=//=ls++q/m+w+pQDb/xCi0OhD=2c/hST mycontainerregistry2675.azurecr.io
```

<span data-ttu-id="3acfa-152">Son olarak, hello görüntü toohello ACR kayıt defteri karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="3acfa-152">Finally, upload hello image toohello ACR registry.</span></span> <span data-ttu-id="3acfa-153">Bu örnek dcos demo adlı bir resim yükler.</span><span class="sxs-lookup"><span data-stu-id="3acfa-153">This example uploads an image named dcos-demo.</span></span>

```azurecli-interactive
docker push mycontainerregistry30678.azurecr.io/dcos-demo
```

## <a name="run-an-image-from-acr"></a><span data-ttu-id="3acfa-154">Bir görüntü ACR çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3acfa-154">Run an image from ACR</span></span>

<span data-ttu-id="3acfa-155">Resmin hello ACR kayıt defterinden toouse adları bir dosya oluşturun *acrDemo.json* ve kopyalama hello aşağıdaki metni içine.</span><span class="sxs-lookup"><span data-stu-id="3acfa-155">toouse an image from hello ACR registry, create a file names *acrDemo.json* and copy hello following text into it.</span></span> <span data-ttu-id="3acfa-156">Örneğin hello kapsayıcı kayıt defteri loginServer adı ve görüntü adı ile Hello görüntü adı yerine `loginServer/imageName`.</span><span class="sxs-lookup"><span data-stu-id="3acfa-156">Replace hello image name with hello container registry loginServer name and image name, for example `loginServer/imageName`.</span></span> <span data-ttu-id="3acfa-157">Merhaba not edin `uris` özelliği.</span><span class="sxs-lookup"><span data-stu-id="3acfa-157">Take note of hello `uris` property.</span></span> <span data-ttu-id="3acfa-158">Bu özellik hello hello DC/OS kümedeki her düğümde takılı hello Azure dosya paylaşımı bu durumda olan hello kapsayıcı kayıt defteri kimlik doğrulaması dosyasının konumunu, tutar.</span><span class="sxs-lookup"><span data-stu-id="3acfa-158">This property holds hello location of hello container registry authentication file, which in this case is hello Azure file share that is mounted on each node in hello DC/OS cluster.</span></span>

```json
{
  "id": "myapp",
  "container": {
    "type": "DOCKER",
    "docker": {
      "image": "mycontainerregistry30678.azurecr.io/dcos-demo",
      "network": "BRIDGE",
      "portMappings": [
        {
          "containerPort": 80,
          "hostPort": 80,
          "protocol": "tcp",
          "name": "80",
          "labels": null
        }
      ],
      "forcePullImage":true
    }
  },
  "instances": 3,
  "cpus": 0.1,
  "mem": 65,
  "healthChecks": [{
      "protocol": "HTTP",
      "path": "/",
      "portIndex": 0,
      "timeoutSeconds": 10,
      "gracePeriodSeconds": 10,
      "intervalSeconds": 2,
      "maxConsecutiveFailures": 10
  }],
  "uris":  [
       "file:///mnt/share/dcosshare/docker.tar.gz"
   ]
}
```

<span data-ttu-id="3acfa-159">Merhaba uygulaması hello DC/OC CLI ile dağıtın.</span><span class="sxs-lookup"><span data-stu-id="3acfa-159">Deploy hello application with hello DC/OC CLI.</span></span>

```azurecli-interactive
dcos marathon app add acrDemo.json
```

## <a name="next-steps"></a><span data-ttu-id="3acfa-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3acfa-160">Next steps</span></span>

<span data-ttu-id="3acfa-161">Bu öğreticide sahip yapılandırdığınız Azure kapsayıcı aşağıdaki hello dahil olmak üzere kayıt defteri görevleri DC/OS toouse:</span><span class="sxs-lookup"><span data-stu-id="3acfa-161">In this tutorial you have configure DC/OS toouse Azure Container Registry including hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="3acfa-162">Azure kapsayıcı kayıt defteri (gerekirse) dağıtın</span><span class="sxs-lookup"><span data-stu-id="3acfa-162">Deploy Azure Container Registry (if needed)</span></span>
> * <span data-ttu-id="3acfa-163">DC/OS kümesinde ACR kimlik doğrulamasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3acfa-163">Configure ACR authentication on a DC/OS cluster</span></span>
> * <span data-ttu-id="3acfa-164">Bir görüntü toohello Azure kapsayıcı kayıt defteri karşıya</span><span class="sxs-lookup"><span data-stu-id="3acfa-164">Uploaded an image toohello Azure Container Registry</span></span>
> * <span data-ttu-id="3acfa-165">Bir kapsayıcı görüntüsü hello Azure kapsayıcı kayıt defteri ' çalıştırın</span><span class="sxs-lookup"><span data-stu-id="3acfa-165">Run a container image from hello Azure Container Registry</span></span>
