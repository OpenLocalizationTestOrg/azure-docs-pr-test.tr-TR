---
title: "Hızlı Başlangıç - Windows için Azure Kubernetes kümesi | Microsoft Docs"
description: "Azure CLI ile Azure Container Service'te Windows kapsayıcıları için Kubernetes kümesi oluşturmayı hızlı bir şekilde öğrenin."
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: danlep
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: f9bf4c4094addfa9654e3b99d91add03079ee045
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="d48c7-103">Windows kapsayıcıları için Kubernetes kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="d48c7-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="d48c7-104">Azure CLI, komut satırından veya betik içindeki Azure kaynaklarını oluşturmak ve yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d48c7-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="d48c7-105">Bu kılavuzda, [Azure Container Service](../container-service-intro.md)'te [Kubernetes](https://kubernetes.io/docs/home/) kümesi dağıtmak için Azure CLI'yi nasıl kullanacağınız ayrıntılı olarak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d48c7-105">This guide details using the Azure CLI to deploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="d48c7-106">Küme dağıtıldıktan sonra, Kubernetes `kubectl` komut satırı aracı ile kümeye bağlanır ve ilk Windows kapsayıcınızı dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="d48c7-106">Once the cluster is deployed, you connect to it with the Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="d48c7-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d48c7-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d48c7-108">CLI'yi yerel olarak yükleyip kullanmayı seçerseniz bu hızlı başlangıç için Azure CLI 2.0.4 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d48c7-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="d48c7-109">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d48c7-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="d48c7-110">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d48c7-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="d48c7-111">Azure Container Service'te Kubernetes için Windows kapsayıcıları desteği önizleme aşamasındadır.</span><span class="sxs-lookup"><span data-stu-id="d48c7-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="d48c7-112">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d48c7-112">Create a resource group</span></span>

<span data-ttu-id="d48c7-113">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d48c7-113">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="d48c7-114">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği mantıksal bir gruptur.</span><span class="sxs-lookup"><span data-stu-id="d48c7-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="d48c7-115">Aşağıdaki örnek *eastus* konumunda *myResourceGroup* adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d48c7-115">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="d48c7-116">Kubernetes kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="d48c7-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="d48c7-117">Azure Container Service'te [az acs create](/cli/azure/acs#create) komutuyla Kubernetes kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d48c7-117">Create a Kubernetes cluster in Azure Container Service with the [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="d48c7-118">Aşağıdaki örnekte, bir Linux ana düğümü ve iki Windows aracı düğümüyle *myK8sCluster* adlı bir küme oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="d48c7-118">The following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="d48c7-119">Bu örnekte, Linux ana düğümüne bağlanmak için gereken SSH anahtarları oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="d48c7-119">This example creates SSH keys needed to connect to the Linux master.</span></span> <span data-ttu-id="d48c7-120">Bu örnekte, yönetici kullanıcı adı olarak *azureuser*, Windows düğümlerindeki parola olarak ise *myPassword12* kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="d48c7-120">This example uses *azureuser* for an administrative user name and *myPassword12* as the password on the Windows nodes.</span></span> <span data-ttu-id="d48c7-121">Bu değerleri ortamınız için uygun olan bir değerle güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d48c7-121">Update these values to something appropriate to your environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="d48c7-122">Birkaç dakika sonra komut tamamlanır ve size dağıtımınız hakkındaki bilgiler gösterilir.</span><span class="sxs-lookup"><span data-stu-id="d48c7-122">After several minutes, the command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="d48c7-123">Kubectl yükleyin</span><span class="sxs-lookup"><span data-stu-id="d48c7-123">Install kubectl</span></span>

<span data-ttu-id="d48c7-124">İstemci bilgisayarınızdan Kubernetes kümesine bağlanmak için Kubernetes’in komut satırı istemcisini ([`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/)) kullanın.</span><span class="sxs-lookup"><span data-stu-id="d48c7-124">To connect to the Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), the Kubernetes command-line client.</span></span> 

<span data-ttu-id="d48c7-125">Azure CloudShell'i kullanıyorsanız `kubectl` zaten yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="d48c7-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="d48c7-126">Yerel olarak yüklemek istiyorsanız [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) komutunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d48c7-126">If you want to install it locally, you can use the [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="d48c7-127">Aşağıdaki Azure CLI örneğinde `kubectl`, sisteminize yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d48c7-127">The following Azure CLI example installs `kubectl` to your system.</span></span> <span data-ttu-id="d48c7-128">Windows'da bu komutu yönetici olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d48c7-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="d48c7-129">kubectl ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="d48c7-129">Connect with kubectl</span></span>

<span data-ttu-id="d48c7-130">`kubectl` öğesini Kubernetes kümenize bağlanacak şekilde yapılandırmak için [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d48c7-130">To configure `kubectl` to connect to your Kubernetes cluster, run the [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="d48c7-131">Aşağıdaki örnekte, Kubernetes kümeniz için küme yapılandırması indirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="d48c7-131">The following example downloads the cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="d48c7-132">Makinenizden küme bağlantısını doğrulamak için şunu çalıştırmayı deneyin:</span><span class="sxs-lookup"><span data-stu-id="d48c7-132">To verify the connection to your cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="d48c7-133">`kubectl`, ana ve aracı düğümleri listeler.</span><span class="sxs-lookup"><span data-stu-id="d48c7-133">`kubectl` lists the master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="d48c7-134">Windows IIS kapsayıcısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="d48c7-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="d48c7-135">Bir veya daha fazla kapsayıcı içeren bir Kubernetes *pod*'unun içinde Docker kapsayıcısı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d48c7-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="d48c7-136">Bu temel örnekte Microsoft Internet Information Server (IIS) kapsayıcısı belirtmek için bir JSON dosyası kullanılmış ve ardından `kubctl apply` komutu kullanılarak pod oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="d48c7-136">This basic example uses a JSON file to specify a Microsoft Internet Information Server (IIS) container, and then creates the pod using the `kubctl apply` command.</span></span> 

<span data-ttu-id="d48c7-137">`iis.json` adlı bir yerel dosya oluşturun ve aşağıdaki metni kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="d48c7-137">Create a local file named `iis.json` and copy the following text.</span></span> <span data-ttu-id="d48c7-138">Bu dosya Kubernetes'e, Windows Server 2016 Nano Server üzerinde, [Docker Hub](https://hub.docker.com/r/nanoserver/iis/)'daki genel bir görüntüyü kullanarak IIS çalıştırmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="d48c7-138">This file tells Kubernetes to run IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="d48c7-139">Kapsayıcı 80 numaralı bağlantı noktasını kullanır, ancak başlangıçta yalnızca küme ağından erişim sağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="d48c7-139">The container uses port 80, but initially is only accessible within the cluster network.</span></span>

 ```JSON
 {
  "apiVersion": "v1",
  "kind": "Pod",
  "metadata": {
    "name": "iis",
    "labels": {
      "name": "iis"
    }
  },
  "spec": {
    "containers": [
      {
        "name": "iis",
        "image": "nanoserver/iis",
        "ports": [
          {
          "containerPort": 80
          }
        ]
      }
    ],
    "nodeSelector": {
     "beta.kubernetes.io/os": "windows"
     }
   }
 }
 ```

<span data-ttu-id="d48c7-140">Pod'u başlatmak için şunları yazın:</span><span class="sxs-lookup"><span data-stu-id="d48c7-140">To start the pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="d48c7-141">Dağıtımı izlemek için şunları yazın:</span><span class="sxs-lookup"><span data-stu-id="d48c7-141">To track the deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="d48c7-142">Pod dağıtılırken durum şudur: `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="d48c7-142">While the pod is deploying, the status is `ContainerCreating`.</span></span> <span data-ttu-id="d48c7-143">Kapsayıcının `Running` durumuna geçmesi birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="d48c7-143">It can take a few minutes for the container to enter the `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="d48c7-144">IIS karşılama sayfasını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="d48c7-144">View the IIS welcome page</span></span>

<span data-ttu-id="d48c7-145">Pod'u genel bir IP adresiyle herkesin kullanımına sunmak için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="d48c7-145">To expose the pod to the world with a public IP address, type the following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="d48c7-146">Bu komutla Kubernetes, hizmet için genel bir IP adresiyle birlikte bir hizmet ve [Azure yük dengeleyici kuralı](container-service-kubernetes-load-balancing.md) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d48c7-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for the service.</span></span> 

<span data-ttu-id="d48c7-147">Hizmetin durumunu görmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d48c7-147">Run the following command to see the status of the service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="d48c7-148">IP adresi başlangıçta `pending` olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="d48c7-148">Initially the IP address appears as `pending`.</span></span> <span data-ttu-id="d48c7-149">Birkaç dakika sonra, `iis` pod'unun dış IP adresi şu şekilde ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="d48c7-149">After a few minutes, the external IP address of the `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="d48c7-150">Dış IP adresinde varsayılan IIS karşılama sayfasını görmek için istediğiniz bir web tarayıcısını kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d48c7-150">You can use a web browser of your choice to see the default IIS welcome page at the external IP address:</span></span>

![IIS’e göz atma görüntüsü](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="d48c7-152">Kümeyi silme</span><span class="sxs-lookup"><span data-stu-id="d48c7-152">Delete cluster</span></span>
<span data-ttu-id="d48c7-153">Kümeye artık ihtiyacınız yoksa [az group delete](/cli/azure/group#delete) komutunu kullanarak kaynak grubunu, kapsayıcı hizmetini ve ilgili tüm kaynakları kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d48c7-153">When the cluster is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="d48c7-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d48c7-154">Next steps</span></span>

<span data-ttu-id="d48c7-155">Bu hızlı başlangıçta, `kubectl` bağlantılı bir Kubernetes kümesi ve IIS kapsayıcısı ile birlikte bir pod dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="d48c7-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="d48c7-156">Azure Container Service hakkında daha fazla bilgi edinmek için Kubernetes öğreticisine geçin.</span><span class="sxs-lookup"><span data-stu-id="d48c7-156">To learn more about Azure Container Service, continue to the Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d48c7-157">ACS Kubernetes kümesini yönetme</span><span class="sxs-lookup"><span data-stu-id="d48c7-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
