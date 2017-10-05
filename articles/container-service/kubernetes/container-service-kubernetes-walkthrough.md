---
title: "Hızlı Başlangıç - Linux için Azure Kubernetes kümesi | Microsoft Docs"
description: "Azure CLI ile Azure Container Service'de Linux kapsayıcıları için Kubernetes kümesi oluşturmayı hızlı bir şekilde öğrenin."
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
ms.openlocfilehash: 5a2131659903e79b28f4d1b795d25a31d8d4ce8d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-kubernetes-cluster-for-linux-containers"></a><span data-ttu-id="7343c-103">Linux kapsayıcıları için Kubernetes kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="7343c-103">Deploy Kubernetes cluster for Linux containers</span></span>

<span data-ttu-id="7343c-104">Bu hızlı başlangıçta, Azure CLI kullanılarak Kubernetes kümesi dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="7343c-104">In this quick start, a Kubernetes cluster is deployed using the Azure CLI.</span></span> <span data-ttu-id="7343c-105">Ardından web ön ucu ve bir Redis örneğinden oluşan çok kapsayıcılı bir uygulama dağıtılıp küme üzerinde çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="7343c-105">A multi-container application consisting of web front end and a Redis instance is then deployed and run on the cluster.</span></span> <span data-ttu-id="7343c-106">Tamamlandığında, uygulamaya İnternet üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="7343c-106">Once completed, the application is accessible over the internet.</span></span> 

<span data-ttu-id="7343c-107">Bu belgede kullanılan örnek uygulama Python’da yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="7343c-107">The example application used in this document is written in Python.</span></span> <span data-ttu-id="7343c-108">Kavramlar ve burada ayrıntıları verilen adımlar herhangi bir kapsayıcı görüntüsünü Kubernetes kümesine dağıtmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7343c-108">The concepts and steps detailed here can be used to deploy any container image into a Kubernetes cluster.</span></span> <span data-ttu-id="7343c-109">Kod, Dockerfile ve bu projeyle ilgili önceden oluşturulmuş Kubernetes bildirim dosyaları [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git)’da vardır.</span><span class="sxs-lookup"><span data-stu-id="7343c-109">The code, Dockerfile, and pre-created Kubernetes manifest files related to this project are available on [GitHub](https://github.com/Azure-Samples/azure-voting-app-redis.git).</span></span>

![Azure Vote’a göz atma görüntüsü](media/container-service-kubernetes-walkthrough/azure-vote.png)

<span data-ttu-id="7343c-111">Bu hızlı başlangıçta temel Kubernetes kavramlarını bildiğiniz varsayılmıştır. Kubernetes hakkında ayrıntılı bilgi için bkz. [Kubernetes belgeleri]( https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="7343c-111">This quick start assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation]( https://kubernetes.io/docs/home/).</span></span>

<span data-ttu-id="7343c-112">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7343c-112">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7343c-113">CLI'yi yerel olarak yükleyip kullanmayı seçerseniz bu hızlı başlangıç için Azure CLI 2.0.4 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7343c-113">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7343c-114">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7343c-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="7343c-115">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7343c-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="7343c-116">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="7343c-116">Create a resource group</span></span>

<span data-ttu-id="7343c-117">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7343c-117">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="7343c-118">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği mantıksal bir gruptur.</span><span class="sxs-lookup"><span data-stu-id="7343c-118">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="7343c-119">Aşağıdaki örnek *westeurope* konumunda *myResourceGroup* adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7343c-119">The following example creates a resource group named *myResourceGroup* in the *westeurope* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="7343c-120">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="7343c-120">Output:</span></span>

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

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="7343c-121">Kubernetes kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7343c-121">Create Kubernetes cluster</span></span>

<span data-ttu-id="7343c-122">Azure Container Service'te [az acs create](/cli/azure/acs#create) komutuyla Kubernetes kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7343c-122">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> <span data-ttu-id="7343c-123">Aşağıdaki örnekte, bir Linux ana düğümü ve üç Linux aracı düğümüyle *myK8sCluster* adlı bir küme oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="7343c-123">The following example creates a cluster named *myK8sCluster* with one Linux master node and three Linux agent nodes.</span></span>

```azurecli-interactive 
az acs create --orchestrator-type kubernetes --resource-group myResourceGroup --name myK8sCluster --generate-ssh-keys 
```

<span data-ttu-id="7343c-124">Birkaç dakika sonra komut tamamlanır ve küme hakkında json tarafından biçimlendirilmiş bilgiler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="7343c-124">After several minutes, the command completes and returns json formatted information about the cluster.</span></span> 

## <a name="connect-to-the-cluster"></a><span data-ttu-id="7343c-125">Kümeye bağlanma</span><span class="sxs-lookup"><span data-stu-id="7343c-125">Connect to the cluster</span></span>

<span data-ttu-id="7343c-126">Bir Kubernetes kümesini yönetmek için Kubernetes komut satırı istemcisi [kubectl](https://kubernetes.io/docs/user-guide/kubectl/)’i kullanın.</span><span class="sxs-lookup"><span data-stu-id="7343c-126">To manage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="7343c-127">Azure CloudShell kullanıyorsanız kubectl zaten yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="7343c-127">If you're using Azure CloudShell, kubectl is already installed.</span></span> <span data-ttu-id="7343c-128">Yerel olarak yüklemek istiyorsanız [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) komutunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7343c-128">If you want to install it locally, you can use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="7343c-129">kubectl’i Kubernetes kümenize bağlanacak şekilde yapılandırmak için [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7343c-129">To configure kubectl to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="7343c-130">Bu adım kimlik bilgilerini indirir ve Kubernetes CLI’yi bunları kullanacak şekilde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7343c-130">This step downloads credentials and configures the Kubernetes CLI to use them.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="7343c-131">Kümenize bağlantıyı doğrulamak için [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutunu kullanarak küme düğümleri listesini alın.</span><span class="sxs-lookup"><span data-stu-id="7343c-131">To verify the connection to your cluster, use the [kubectl get](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command to return a list of the cluster nodes.</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="7343c-132">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="7343c-132">Output:</span></span>

```bash
NAME                    STATUS                     AGE       VERSION
k8s-agent-14ad53a1-0    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-1    Ready                      10m       v1.6.6
k8s-agent-14ad53a1-2    Ready                      10m       v1.6.6
k8s-master-14ad53a1-0   Ready,SchedulingDisabled   10m       v1.6.6
```

## <a name="run-the-application"></a><span data-ttu-id="7343c-133">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7343c-133">Run the application</span></span>

<span data-ttu-id="7343c-134">Kubernetes bildirim dosyası, hangi kapsayıcı görüntülerinin çalıştırılması gerektiği de dahil olmak üzere, küme için istenen durumu tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7343c-134">A Kubernetes manifest file defines a desired state for the cluster, including what container images should be running.</span></span> <span data-ttu-id="7343c-135">Bu örnekte, Azure Vote uygulamasını çalıştırmak için gerekli tüm nesneleri oluşturmak için bir bildirim kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7343c-135">For this example, a manifest is used to create all objects needed to run the Azure Vote application.</span></span> 

<span data-ttu-id="7343c-136">`azure-vote.yml` adlı bir dosya oluşturun ve dosyayı aşağıdaki YAML’ye kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="7343c-136">Create a file named `azure-vote.yml` and copy into it the following YAML.</span></span> <span data-ttu-id="7343c-137">Azure Cloud Shell'de çalışıyorsanız, bu dosya bir sanal veya fiziksel sistemde olduğu gibi vi veya Nano kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="7343c-137">If you are working in Azure Cloud Shell, this file can be created using vi or Nano as if working on a virtual or physical system.</span></span>

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

<span data-ttu-id="7343c-138">Uygulamayı çalıştırmak için [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7343c-138">Use the [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command to run the application.</span></span>

```azurecli-interactive
kubectl create -f azure-vote.yml
```

<span data-ttu-id="7343c-139">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="7343c-139">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-the-application"></a><span data-ttu-id="7343c-140">Uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="7343c-140">Test the application</span></span>

<span data-ttu-id="7343c-141">Uygulama çalıştırıldığında, uygulama ön ucunu İnternet üzerinden kullanıma sunan bir [Kubernetes hizmeti](https://kubernetes.io/docs/concepts/services-networking/service/) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7343c-141">As the application is run, a [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created that exposes the application front end to the internet.</span></span> <span data-ttu-id="7343c-142">Bu işlemin tamamlanması birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="7343c-142">This process can take a few minutes to complete.</span></span> 

<span data-ttu-id="7343c-143">İlerleme durumunu izlemek için [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutunu `--watch` bağımsız değişkeniyle birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="7343c-143">To monitor progress, use the [kubectl get service](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="7343c-144">Başlangıçta *azure-vote-front* için **EXTERNAL-IP** durumu *pending* olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="7343c-144">Initially the **EXTERNAL-IP** for the *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="7343c-145">EXTERNAL-IP adresi *pending* durumundan *IP address* değerine değiştiğinde kubectl izleme işlemini durdurmak için `CTRL-C` komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7343c-145">Once the EXTERNAL-IP address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span> 
  
```bash
azure-vote-front   10.0.34.242   <pending>     80:30676/TCP   7s
azure-vote-front   10.0.34.242   52.179.23.131   80:30676/TCP   2m
```

<span data-ttu-id="7343c-146">Artık Azure Vote Uygulamasını görmek için dış IP adresine göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7343c-146">You can now browse to the external IP address to see the Azure Vote App.</span></span>

![Azure Vote’a göz atma görüntüsü](media/container-service-kubernetes-walkthrough/azure-vote.png)  

## <a name="delete-cluster"></a><span data-ttu-id="7343c-148">Kümeyi silme</span><span class="sxs-lookup"><span data-stu-id="7343c-148">Delete cluster</span></span>
<span data-ttu-id="7343c-149">Kümeye artık ihtiyacınız yoksa [az group delete](/cli/azure/group#delete) komutunu kullanarak kaynak grubunu, kapsayıcı hizmetini ve ilgili tüm kaynakları kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7343c-149">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes --no-wait
```

## <a name="get-the-code"></a><span data-ttu-id="7343c-150">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="7343c-150">Get the code</span></span>

<span data-ttu-id="7343c-151">Bu hızlı başlangıçta, Kubernetes dağıtımı oluşturmak için önceden oluşturulmuş kapsayıcı görüntüleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7343c-151">In this quick start, pre-created container images have been used to create a Kubernetes deployment.</span></span> <span data-ttu-id="7343c-152">İlgili uygulama kodu, Dockerfile ve Kubernetes bildirim dosyası GitHub'da bulunur.</span><span class="sxs-lookup"><span data-stu-id="7343c-152">The related application code, Dockerfile, and Kubernetes manifest file are available on GitHub.</span></span>

[<span data-ttu-id="7343c-153">https://github.com/Azure-Samples/azure-voting-app-redis</span><span class="sxs-lookup"><span data-stu-id="7343c-153">https://github.com/Azure-Samples/azure-voting-app-redis</span></span>](https://github.com/Azure-Samples/azure-voting-app-redis.git)

## <a name="next-steps"></a><span data-ttu-id="7343c-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7343c-154">Next steps</span></span>

<span data-ttu-id="7343c-155">Bu hızlı başlangıçta, bir Kubernetes kümesi dağıtıp ve bu kümeye çok kapsayıcılı bir uygulama dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="7343c-155">In this quick start, you deployed a Kubernetes cluster and deployed a multi-container application to it.</span></span> 

<span data-ttu-id="7343c-156">Azure Container Service hakkında daha fazla bilgi ve dağıtım örneği için tam kod açıklaması için Kubernetes küme öğreticisine geçin.</span><span class="sxs-lookup"><span data-stu-id="7343c-156">To learn more about Azure Container Service, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7343c-157">ACS Kubernetes kümesini yönetme</span><span class="sxs-lookup"><span data-stu-id="7343c-157">Manage an ACS Kubernetes cluster</span></span>](./container-service-tutorial-kubernetes-prepare-app.md)
