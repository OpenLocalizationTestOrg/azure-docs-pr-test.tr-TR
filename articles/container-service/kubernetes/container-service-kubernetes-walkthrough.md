---
title: "aaaQuickstart - Linux Azure Kubernetes küme | Microsoft Docs"
description: "Hızlı bir şekilde toocreate Kubernetes küme hello Azure CLI ile Azure kapsayıcı Hizmeti'nde Linux kapsayıcıları için öğrenin."
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 8da267e8-2aeb-4c24-9a7a-65bdca3a82d6
ms.service: container-service
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 8b0d7a803148c1cbf329f4b76f2e99b4b7e14983
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="b91ae-103">Linux kapsayıcıları için Kubernetes kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="b91ae-103">Deploy Kubernetes cluster for Linux containers</span></span>

<span data-ttu-id="b91ae-104">Bu Hızlı Başlangıç, Kubernetes küme hello Azure CLI kullanarak dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="b91ae-104">In this quick start, a Kubernetes cluster is deployed using hello Azure CLI.</span></span> <span data-ttu-id="b91ae-105">Web ön uç ve bir Redis örneği oluşan çok kapsayıcı uygulama sonra dağıtılan ve hello kümede çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b91ae-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on hello cluster.</span></span> <span data-ttu-id="b91ae-106">Tamamlandığında, Merhaba uygulaması üzerinden erişilebilen Internet hello.</span><span class="sxs-lookup"><span data-stu-id="b91ae-106">Once completed, hello application is accessible over hello internet.</span></span> 

<span data-ttu-id="b91ae-107">Bu belgede kullanılan Merhaba örnek uygulaması Python içinde yazılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b91ae-107">hello example application used in this document is written in Python.</span></span> <span data-ttu-id="b91ae-108">Merhaba kavramlar ve burada ayrıntılı adımlar herhangi bir kapsayıcısına görüntü Kubernetes kümesine kullanılan toodeploy olabilir.</span><span class="sxs-lookup"><span data-stu-id="b91ae-108">hello concepts and steps detailed here can be used toodeploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="b91ae-109">Merhaba kodu, Dockerfile ve önceden oluşturulmuş Kubernetes bildirim dosyaları ilgili toothis proje kullanılabilir [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span><span class="sxs-lookup"><span data-stu-id="b91ae-109">hello code, Dockerfile, and pre-created Kubernetes manifest files related toothis project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![TooAzure oy göz atma görüntüsü](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="b91ae-111">Bu hızlı başlangıç Kubernetes kavramları temel bir anlayış varsayar, hello Kubernetes hakkında ayrıntılı bilgi için bkz: [Kubernetes belgelerine]( https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="b91ae-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see hello [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="b91ae-112">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b91ae-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b91ae-113">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="b91ae-113">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="b91ae-114">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="b91ae-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b91ae-115">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b91ae-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="b91ae-116">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91ae-116">Create a resource group</span></span>

<span data-ttu-id="b91ae-117">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="b91ae-117">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="b91ae-118">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği mantıksal bir gruptur.</span><span class="sxs-lookup"><span data-stu-id="b91ae-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="b91ae-119">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *westeurope* konumu.</span><span class="sxs-lookup"><span data-stu-id="b91ae-119">hello following example creates a resource group named *myResourceGroup* in hello *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="b91ae-120">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="b91ae-120">Output:</span></span>

```json
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup",
  "location": "westeurope",
  "managedBy": null,
  "name": "myResourceGroup",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="b91ae-121">Kubernetes kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b91ae-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="b91ae-122">Kubernetes küme Azure kapsayıcı hizmeti ile Merhaba oluşturmak [az acs oluşturmak](/cli/azure/acs#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="b91ae-122">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> <span data-ttu-id="b91ae-123">Merhaba aşağıdaki örnek adlı bir küme oluşturur *myK8sCluster* ile bir Linux ana düğümü ve üç Linux Aracısı düğümleri.</span><span class="sxs-lookup"><span data-stu-id="b91ae-123">hello following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

<span data-ttu-id="b91ae-124">Birkaç dakika sonra hello komut tamamlandıktan ve biçimlendirilmiş json hello kümesi hakkında bilgi verir.</span><span class="sxs-lookup"><span data-stu-id="b91ae-124">After several minutes, hello command completes and returns json formatted information about hello cluster.</span></span> 

## <a name="connect-toohello-cluster"></a><span data-ttu-id="b91ae-125">Toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="b91ae-125">Connect toohello cluster</span></span>

<span data-ttu-id="b91ae-126">toomanage Kubernetes küme kullanmak [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes komut satırı istemcisi.</span><span class="sxs-lookup"><span data-stu-id="b91ae-126">toomanage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="b91ae-127">Azure CloudShell kullanıyorsanız kubectl zaten yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="b91ae-127">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="b91ae-128">Tooinstall isterseniz, yerel olarak kullanabileceğiniz hello [az acs kubernetes yükleme-CLI](/cli/azure/acs/kubernetes#install-cli) komutu.</span><span class="sxs-lookup"><span data-stu-id="b91ae-128">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="b91ae-129">Merhaba çalıştırmak tooconfigure kubectl tooconnect tooyour Kubernetes küme, [az acs kubernetes get-kimlik](/cli/azure/acs/kubernetes#get-credentials) komutu.</span><span class="sxs-lookup"><span data-stu-id="b91ae-129">tooconfigure kubectl tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="b91ae-130">Bu adım kimlik bilgileri indirmeleri ve hello Kubernetes CLI toouse yapılandırır bunları.</span><span class="sxs-lookup"><span data-stu-id="b91ae-130">This step downloads credentials and configures hello Kubernetes CLI toouse them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="b91ae-131">tooverify hello bağlantı tooyour küme, kullanım hello [kubectl almak](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu tooreturn hello küme düğümlerinin bir listesi.</span><span class="sxs-lookup"><span data-stu-id="b91ae-131">tooverify hello connection tooyour cluster, use hello [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command tooreturn a list of hello cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="b91ae-132">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="b91ae-132">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-hello-application"></a><span data-ttu-id="b91ae-133">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="b91ae-133">Run hello application</span></span>

<span data-ttu-id="b91ae-134">Kubernetes bildirim dosyası kapsayıcı görüntüleri çalıştırma dahil hello küme için istenen bir durum tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b91ae-134">A Kubernetes manifest file defines a desired state for hello cluster, including what container images should be running.</span></span> <span data-ttu-id="b91ae-135">Bu örnekte, bir bildirim tüm nesneleri toorun Azure oy uygulama hello kullanılan toocreate ' dir.</span><span class="sxs-lookup"><span data-stu-id="b91ae-135">For this example, a manifest is used toocreate all objects needed toorun hello Azure Vote application.</span></span> 

<span data-ttu-id="b91ae-136">Adlı bir dosya oluşturun `azure-vote.yml` kopyalayıp içine hello YAML.</span><span class="sxs-lookup"><span data-stu-id="b91ae-136">Create a file named `azure-vote.yml` and copy into it hello following YAML.</span></span> <span data-ttu-id="b91ae-137">Azure Cloud Shell'de çalışıyorsanız, bu dosya bir sanal veya fiziksel sistemde olduğu gibi vi veya Nano kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="b91ae-137">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

```yaml
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-back
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-back
    spec:
      containers:
      - name: azure-vote-back
        image: redis
        ports:
        - containerPort: 6379
          name: redis
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-back
spec:
  ports:
  - port: 6379
  selector:
    app: azure-vote-back
---
apiVersion: apps/v1beta1
kind: Deployment
metadata:
  name: azure-vote-front
spec:
  replicas: 1
  template:
    metadata:
      labels:
        app: azure-vote-front
    spec:
      containers:
      - name: azure-vote-front
        image: microsoft/azure-vote-front:redis-v1
        ports:
        - containerPort: 80
        env:
        - name: REDIS
          value: "azure-vote-back"
---
apiVersion: v1
kind: Service
metadata:
  name: azure-vote-front
spec:
  type: LoadBalancer
  ports:
  - port: 80
  selector:
    app: azure-vote-front
```

<span data-ttu-id="b91ae-138">Kullanım hello [kubectl oluşturma](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) toorun Merhaba uygulaması komutu.</span><span class="sxs-lookup"><span data-stu-id="b91ae-138">Use hello [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command toorun hello application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="b91ae-139">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="b91ae-139">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-hello-application"></a><span data-ttu-id="b91ae-140">Merhaba uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="b91ae-140">Test hello application</span></span>

<span data-ttu-id="b91ae-141">Merhaba uygulaması çalıştırılırken bir [Kubernetes hizmet](https://kubernetes.io/docs/concepts/services-networking/service/) düzenlemenizi sağlayan uygulama ön uç toohello hello oluşturulan Internet.</span><span class="sxs-lookup"><span data-stu-id="b91ae-141">As hello application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes hello application front end toohello internet.</span></span> <span data-ttu-id="b91ae-142">Bu işlem birkaç dakika toocomplete alabilir.</span><span class="sxs-lookup"><span data-stu-id="b91ae-142">This process can take a few minutes toocomplete.</span></span> 

<span data-ttu-id="b91ae-143">toomonitor ilerleme, kullanım hello [kubectl alma hizmeti](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) hello komutunu `--watch` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="b91ae-143">toomonitor progress, use hello [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command with hello `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="b91ae-144">Başlangıçta hello **dış IP** hello için *azure oy ön* hizmeti görünür olarak *bekleyen*.</span><span class="sxs-lookup"><span data-stu-id="b91ae-144">Initially hello **EXTERNAL-IP** for hello *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="b91ae-145">Merhaba dış IP adresi değiştiğinden sonra *bekleyen* tooan *IP adresi*, kullanın `CTRL-C` toostop hello kubectl izleme işlemi.</span><span class="sxs-lookup"><span data-stu-id="b91ae-145">Once hello EXTERNAL-IP address has changed from *pending* tooan *IP address*, use `CTRL-C` toostop hello kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="b91ae-146">Toohello dış IP adresi toosee hello Azure oylama uygulaması gözatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b91ae-146">You can now browse toohello external IP address toosee hello Azure Vote App.</span></span>

![TooAzure oy göz atma görüntüsü](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="b91ae-148">Kümeyi silme</span><span class="sxs-lookup"><span data-stu-id="b91ae-148">Delete cluster</span></span>
<span data-ttu-id="b91ae-149">Merhaba küme artık gerekli olmadığında hello kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, kapsayıcı hizmeti ve ilgili tüm kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="b91ae-149">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-hello-code"></a><span data-ttu-id="b91ae-150">Merhaba kod alın</span><span class="sxs-lookup"><span data-stu-id="b91ae-150">Get hello code</span></span>

<span data-ttu-id="b91ae-151">Bu Hızlı Başlangıç, önceden oluşturulmuş kapsayıcı görüntüleri kullanılan toocreate Kubernetes dağıtım silinmiş.</span><span class="sxs-lookup"><span data-stu-id="b91ae-151">In this quick start, pre-created container images have been used toocreate a Kubernetes deployment.</span></span> <span data-ttu-id="b91ae-152">uygulama kodu, Dockerfile, Hello ilgili ve Kubernetes bildirim dosyası Github'da bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b91ae-152">hello related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[<span data-ttu-id="b91ae-153">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="b91ae-153">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="b91ae-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b91ae-154">Next steps</span></span>

<span data-ttu-id="b91ae-155">Bu hızlı başlangıç Kubernetes küme dağıtılan ve çok kapsayıcı uygulama tooit dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="b91ae-155">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application tooit.</span></span> 

<span data-ttu-id="b91ae-156">Azure kapsayıcı hizmeti ve tam bir kod toodeployment örnek aracılığıyla ilerlemesi hakkında daha fazla toolearn toohello Kubernetes küme öğretici devam edin.</span><span class="sxs-lookup"><span data-stu-id="b91ae-156">toolearn more about Azure Container Service, and walk through a complete code toodeployment example, continue toohello Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b91ae-157">ACS Kubernetes kümesini yönetme</span><span class="sxs-lookup"><span data-stu-id="b91ae-157">Manage an ACS Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-prepare-app.md)
