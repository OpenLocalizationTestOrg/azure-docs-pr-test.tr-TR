---
title: "aaaQuickstart - Windows için Azure Kubernetes küme | Microsoft Docs"
description: "Hızlı bir şekilde toocreate bir Kubernetes kümesi için Windows hello Azure CLI ile Azure kapsayıcı hizmeti kapsayıcı öğrenin."
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
ms.openlocfilehash: 85fe65a46ae8c78797e8a8a097c2a37f06329335
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-kubernetes-cluster-for-windows-containers"></a><span data-ttu-id="bc553-103">Windows kapsayıcıları için Kubernetes kümesi dağıtma</span><span class="sxs-lookup"><span data-stu-id="bc553-103">Deploy Kubernetes cluster for Windows containers</span></span>

<span data-ttu-id="bc553-104">Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin.</span><span class="sxs-lookup"><span data-stu-id="bc553-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="bc553-105">Hello Azure CLI toodeploy kullanarak bu kılavuzu ayrıntılarını bir [Kubernetes](https://kubernetes.io/docs/home/) kümesi [Azure kapsayıcı hizmeti](../container-service-intro.md).</span><span class="sxs-lookup"><span data-stu-id="bc553-105">This guide details using hello Azure CLI toodeploy a [Kubernetes](https://kubernetes.io/docs/home/) cluster in [Azure Container Service](../container-service-intro.md).</span></span> <span data-ttu-id="bc553-106">Merhaba küme dağıtıldıktan sonra Kubernetes hello ile tooit bağlanmak `kubectl` komut satırı aracı ve dağıtmak, ilk Windows kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="bc553-106">Once hello cluster is deployed, you connect tooit with hello Kubernetes `kubectl` command-line tool, and you deploy your first Windows container.</span></span>

<span data-ttu-id="bc553-107">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bc553-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bc553-108">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="bc553-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="bc553-109">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="bc553-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="bc553-110">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bc553-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

> [!NOTE]
> <span data-ttu-id="bc553-111">Azure Container Service'te Kubernetes için Windows kapsayıcıları desteği önizleme aşamasındadır.</span><span class="sxs-lookup"><span data-stu-id="bc553-111">Support for Windows containers on Kubernetes in Azure Container Service is in preview.</span></span> 
>

## <a name="create-a-resource-group"></a><span data-ttu-id="bc553-112">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc553-112">Create a resource group</span></span>

<span data-ttu-id="bc553-113">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="bc553-113">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="bc553-114">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği mantıksal bir gruptur.</span><span class="sxs-lookup"><span data-stu-id="bc553-114">An Azure resource group is a logical group in which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="bc553-115">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.</span><span class="sxs-lookup"><span data-stu-id="bc553-115">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-kubernetes-cluster"></a><span data-ttu-id="bc553-116">Kubernetes kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bc553-116">Create Kubernetes cluster</span></span>
<span data-ttu-id="bc553-117">Kubernetes küme Azure kapsayıcı hizmeti ile Merhaba oluşturmak [az acs oluşturmak](/cli/azure/acs#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="bc553-117">Create a Kubernetes cluster in Azure Container Service with hello [az acs create](/cli/azure/acs#create) command.</span></span> 

<span data-ttu-id="bc553-118">Merhaba aşağıdaki örnek adlı bir küme oluşturur *myK8sCluster* ile bir Linux ana düğüm ve iki Windows aracı düğümü.</span><span class="sxs-lookup"><span data-stu-id="bc553-118">hello following example creates a cluster named *myK8sCluster* with one Linux master node and two Windows agent nodes.</span></span> <span data-ttu-id="bc553-119">Bu örnek SSH anahtarları gerekli tooconnect toohello Linux ana oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bc553-119">This example creates SSH keys needed tooconnect toohello Linux master.</span></span> <span data-ttu-id="bc553-120">Bu örnekte *azureuser* bir yönetici kullanıcı adı ve *myPassword12* hello parolasını hello Windows düğümlerinde olarak.</span><span class="sxs-lookup"><span data-stu-id="bc553-120">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password on hello Windows nodes.</span></span> <span data-ttu-id="bc553-121">Bu değerleri toosomething uygun tooyour ortamı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="bc553-121">Update these values toosomething appropriate tooyour environment.</span></span> 



```azurecli-interactive 
az acs create --orchestrator-type=kubernetes \
    --resource-group myResourceGroup \
    --name=myK8sCluster \
    --agent-count=2 \
    --generate-ssh-keys \
    --windows --admin-username azureuser \
    --admin-password myPassword12
```

<span data-ttu-id="bc553-122">Birkaç dakika sonra hello komut tamamlandıktan ve dağıtımınız hakkında bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="bc553-122">After several minutes, hello command completes, and shows you information about your deployment.</span></span>

## <a name="install-kubectl"></a><span data-ttu-id="bc553-123">Kubectl yükleyin</span><span class="sxs-lookup"><span data-stu-id="bc553-123">Install kubectl</span></span>

<span data-ttu-id="bc553-124">tooconnect toohello Kubernetes küme kullanımı, istemci bilgisayardan [ `kubectl` ](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes komut satırı istemcisi.</span><span class="sxs-lookup"><span data-stu-id="bc553-124">tooconnect toohello Kubernetes cluster from your client computer, use [`kubectl`](https://kubernetes.io/docs/user-guide/kubectl/), hello Kubernetes command-line client.</span></span> 

<span data-ttu-id="bc553-125">Azure CloudShell'i kullanıyorsanız `kubectl` zaten yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="bc553-125">If you're using Azure CloudShell, `kubectl` is already installed.</span></span> <span data-ttu-id="bc553-126">Tooinstall isterseniz, yerel olarak kullanabileceğiniz hello [az acs kubernetes yükleme-CLI](/cli/azure/acs/kubernetes#install-cli) komutu.</span><span class="sxs-lookup"><span data-stu-id="bc553-126">If you want tooinstall it locally, you can use hello [az acs kubernetes install-cli](/cli/azure/acs/kubernetes#install-cli) command.</span></span>

<span data-ttu-id="bc553-127">Azure CLI örnek yükler aşağıdaki hello `kubectl` tooyour sistem.</span><span class="sxs-lookup"><span data-stu-id="bc553-127">hello following Azure CLI example installs `kubectl` tooyour system.</span></span> <span data-ttu-id="bc553-128">Windows'da bu komutu yönetici olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bc553-128">On Windows, run this command as an administrator.</span></span>

```azurecli-interactive 
az acs kubernetes install-cli
```


## <a name="connect-with-kubectl"></a><span data-ttu-id="bc553-129">kubectl ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="bc553-129">Connect with kubectl</span></span>

<span data-ttu-id="bc553-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes küme hello çalıştırmak, [az acs kubernetes get-kimlik](/cli/azure/acs/kubernetes#get-credentials) komutu.</span><span class="sxs-lookup"><span data-stu-id="bc553-130">tooconfigure `kubectl` tooconnect tooyour Kubernetes cluster, run hello [az acs kubernetes get-credentials](/cli/azure/acs/kubernetes#get-credentials) command.</span></span> <span data-ttu-id="bc553-131">Merhaba aşağıdaki örnek Kubernetes kümenizin hello küme yapılandırmasını indirir.</span><span class="sxs-lookup"><span data-stu-id="bc553-131">hello following example downloads hello cluster configuration for your Kubernetes cluster.</span></span>

```azurecli-interactive 
az acs kubernetes get-credentials --resource-group=myResourceGroup --name=myK8sCluster
```

<span data-ttu-id="bc553-132">tooverify hello bağlantı tooyour küme makinenizden, çalıştırmayı deneyin:</span><span class="sxs-lookup"><span data-stu-id="bc553-132">tooverify hello connection tooyour cluster from your machine, try running:</span></span>

```azurecli-interactive
kubectl get nodes
```

<span data-ttu-id="bc553-133">`kubectl`Hello Yöneticisi ve Aracısı düğümleri listeler.</span><span class="sxs-lookup"><span data-stu-id="bc553-133">`kubectl` lists hello master and agent nodes.</span></span>

```azurecli-interactive
NAME                    STATUS                     AGE       VERSION
k8s-agent-98dc3136-0    Ready                      5m        v1.5.3
k8s-agent-98dc3136-1    Ready                      5m        v1.5.3
k8s-master-98dc3136-0   Ready,SchedulingDisabled   5m        v1.5.3

```

## <a name="deploy-a-windows-iis-container"></a><span data-ttu-id="bc553-134">Windows IIS kapsayıcısı dağıtma</span><span class="sxs-lookup"><span data-stu-id="bc553-134">Deploy a Windows IIS container</span></span>

<span data-ttu-id="bc553-135">Bir veya daha fazla kapsayıcı içeren bir Kubernetes *pod*'unun içinde Docker kapsayıcısı çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bc553-135">You can run a Docker container inside a Kubernetes *pod*, which contains one or more containers.</span></span> 

<span data-ttu-id="bc553-136">Bu temel örnek bir JSON dosyası toospecify Microsoft Internet Information Server (IIS) kapsayıcı kullanır ve ardından hello kullanarak hello pod oluşturur `kubctl apply` komutu.</span><span class="sxs-lookup"><span data-stu-id="bc553-136">This basic example uses a JSON file toospecify a Microsoft Internet Information Server (IIS) container, and then creates hello pod using hello `kubctl apply` command.</span></span> 

<span data-ttu-id="bc553-137">Adlı bir yerel dosya oluşturma `iis.json` ve kopyalama hello aşağıdaki metin.</span><span class="sxs-lookup"><span data-stu-id="bc553-137">Create a local file named `iis.json` and copy hello following text.</span></span> <span data-ttu-id="bc553-138">Bu dosya, bir ortak kapsayıcı görüntüsünü kullanarak Windows Server 2016 Nano Server üzerinde Kubernetes toorun IIS söyler [Docker hub'a](https://hub.docker.com/r/nanoserver/iis/).</span><span class="sxs-lookup"><span data-stu-id="bc553-138">This file tells Kubernetes toorun IIS on Windows Server 2016 Nano Server, using a public container image from [Docker Hub](https://hub.docker.com/r/nanoserver/iis/).</span></span> <span data-ttu-id="bc553-139">Merhaba kapsayıcı 80 numaralı bağlantı noktasını kullanır, ancak başlangıçta yalnızca hello küme ağdan erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="bc553-139">hello container uses port 80, but initially is only accessible within hello cluster network.</span></span>

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

<span data-ttu-id="bc553-140">toostart hello pod, türü:</span><span class="sxs-lookup"><span data-stu-id="bc553-140">toostart hello pod, type:</span></span>
  
```azurecli-interactive
kubectl apply -f iis.json
```  

<span data-ttu-id="bc553-141">tootrack hello dağıtım türü:</span><span class="sxs-lookup"><span data-stu-id="bc553-141">tootrack hello deployment, type:</span></span>
  
```azurecli-interactive
kubectl get pods
```

<span data-ttu-id="bc553-142">Merhaba pod dağıtma sırasında hello durumudur `ContainerCreating`.</span><span class="sxs-lookup"><span data-stu-id="bc553-142">While hello pod is deploying, hello status is `ContainerCreating`.</span></span> <span data-ttu-id="bc553-143">Merhaba kapsayıcı tooenter hello birkaç dakika sürebilir `Running` durumu.</span><span class="sxs-lookup"><span data-stu-id="bc553-143">It can take a few minutes for hello container tooenter hello `Running` state.</span></span>

```azurecli-interactive
NAME     READY        STATUS        RESTARTS    AGE
iis      1/1          Running       0           32s
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="bc553-144">Görünüm hello IIS Karşılama sayfası</span><span class="sxs-lookup"><span data-stu-id="bc553-144">View hello IIS welcome page</span></span>

<span data-ttu-id="bc553-145">tooexpose hello pod toohello dünyayla komutu aşağıdaki türü hello bir ortak IP adresi:</span><span class="sxs-lookup"><span data-stu-id="bc553-145">tooexpose hello pod toohello world with a public IP address, type hello following command:</span></span>

```azurecli-interactive
kubectl expose pods iis --port=80 --type=LoadBalancer
```

<span data-ttu-id="bc553-146">Bu komutla bir hizmet Kubernetes oluşturur ve bir [Azure yük dengeleyici kuralı](container-service-kubernetes-load-balancing.md) hello hizmeti için genel IP adresine sahip.</span><span class="sxs-lookup"><span data-stu-id="bc553-146">With this command, Kubernetes creates a service and an [Azure load balancer rule](container-service-kubernetes-load-balancing.md) with a public IP address for hello service.</span></span> 

<span data-ttu-id="bc553-147">Komut toosee hello hello hizmetinin durumunu izleyen hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bc553-147">Run hello following command toosee hello status of hello service.</span></span>

```azurecli-interactive
kubectl get svc
```

<span data-ttu-id="bc553-148">Başlangıç IP adresi başlangıçta görünür `pending`.</span><span class="sxs-lookup"><span data-stu-id="bc553-148">Initially hello IP address appears as `pending`.</span></span> <span data-ttu-id="bc553-149">Birkaç dakika sonra hello dış IP adresi hello `iis` pod ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="bc553-149">After a few minutes, hello external IP address of hello `iis` pod is set:</span></span>
  
```azurecli-interactive
NAME         CLUSTER-IP     EXTERNAL-IP     PORT(S)        AGE       
kubernetes   10.0.0.1       <none>          443/TCP        21h       
iis          10.0.111.25    13.64.158.233   80/TCP         22m
```

<span data-ttu-id="bc553-150">Merhaba dış IP adresinde seçim toosee hello varsayılan IIS Karşılama sayfasını bir web tarayıcısı kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bc553-150">You can use a web browser of your choice toosee hello default IIS welcome page at hello external IP address:</span></span>

![TooIIS göz atma görüntüsü](./media/container-service-kubernetes-windows-walkthrough/kubernetes-iis.png)  


## <a name="delete-cluster"></a><span data-ttu-id="bc553-152">Kümeyi silme</span><span class="sxs-lookup"><span data-stu-id="bc553-152">Delete cluster</span></span>
<span data-ttu-id="bc553-153">Merhaba küme artık gerekli olmadığında hello kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, kapsayıcı hizmeti ve ilgili tüm kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="bc553-153">When hello cluster is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, container service, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="bc553-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bc553-154">Next steps</span></span>

<span data-ttu-id="bc553-155">Bu hızlı başlangıçta, `kubectl` bağlantılı bir Kubernetes kümesi ve IIS kapsayıcısı ile birlikte bir pod dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="bc553-155">In this quick start, you deployed a Kubernetes cluster, connected with `kubectl`, and deployed a pod with an IIS container.</span></span> <span data-ttu-id="bc553-156">Azure kapsayıcı hizmeti hakkında daha fazla toolearn toohello Kubernetes öğretici devam edin.</span><span class="sxs-lookup"><span data-stu-id="bc553-156">toolearn more about Azure Container Service, continue toohello Kubernetes tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bc553-157">ACS Kubernetes kümesini yönetme</span><span class="sxs-lookup"><span data-stu-id="bc553-157">Manage an ACS Kubernetes cluster</span></span>](container-service-tutorial-kubernetes-prepare-app.md)
