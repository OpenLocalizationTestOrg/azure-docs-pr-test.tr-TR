---
title: Azure Container Service öğreticisi - Uygulamayı güncelleştirme
description: Azure Container Service öğreticisi - Uygulamayı güncelleştirme
services: container-service
author: neilpeterson
manager: timlt
ms.service: container-service
ms.topic: tutorial
ms.date: 09/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5ecaa3a79270e29ac002e91065f7df4f7e8914e7
ms.sourcegitcommit: 694e40a193980dea1e2f945471071f11030d5641
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/29/2018
---
# <a name="update-an-application-in-kubernetes"></a><span data-ttu-id="cefc2-103">Kubernetes'te uygulama güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="cefc2-103">Update an application in Kubernetes</span></span>

[!INCLUDE [aks-preview-redirect.md](../../../includes/aks-preview-redirect.md)]

<span data-ttu-id="cefc2-104">Bir uygulama Kubernetes’te dağıtıldıktan sonra, yeni bir kapsayıcı görüntüsü veya görüntü sürümü belirtilerek güncelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="cefc2-104">After an application has been deployed in Kubernetes, it can be updated by specifying a new container image or image version.</span></span> <span data-ttu-id="cefc2-105">Bu yapıldığında, güncelleştirme, dağıtımın yalnızca bir kısmı eşzamanlı olarak güncelleştirilecek şekilde hazırlanılır.</span><span class="sxs-lookup"><span data-stu-id="cefc2-105">When doing so, the update is staged so that only a portion of the deployment is concurrently updated.</span></span> <span data-ttu-id="cefc2-106">Hazırlanan bu güncelleştirme, uygulamanın güncelleştirme sırasında çalışmaya devam etmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="cefc2-106">This staged update enables the application to keep running during the update.</span></span> <span data-ttu-id="cefc2-107">Ayrıca bir dağıtım hatası oluşursa, bir geri alma mekanizması sağlar.</span><span class="sxs-lookup"><span data-stu-id="cefc2-107">It also provides a rollback mechanism if a deployment failure occurs.</span></span> 

<span data-ttu-id="cefc2-108">Bu yedi parçalı öğreticinin altıncı bölümünde, örnek Azure Vote uygulaması güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cefc2-108">In this tutorial, part six of seven, the sample Azure Vote app is updated.</span></span> <span data-ttu-id="cefc2-109">Tamamladığınız görevler şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="cefc2-109">Tasks that you complete include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cefc2-110">Ön uç uygulaması kodunu güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="cefc2-110">Updating the front-end application code</span></span>
> * <span data-ttu-id="cefc2-111">Güncelleştirilmiş kapsayıcı görüntüsü oluşturma</span><span class="sxs-lookup"><span data-stu-id="cefc2-111">Creating an updated container image</span></span>
> * <span data-ttu-id="cefc2-112">Kapsayıcı görüntüsünü Azure Container Registry’ye gönderme</span><span class="sxs-lookup"><span data-stu-id="cefc2-112">Pushing the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="cefc2-113">Güncelleştirilmiş kapsayıcı görüntüsünü dağıtma</span><span class="sxs-lookup"><span data-stu-id="cefc2-113">Deploying the updated container image</span></span>

<span data-ttu-id="cefc2-114">Sonraki öğreticilerde Kubernetes kümesini izlemek için Operations Management Suite yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="cefc2-114">In subsequent tutorials, Operations Management Suite is configured to monitor the Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="cefc2-115">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="cefc2-115">Before you begin</span></span>

<span data-ttu-id="cefc2-116">Önceki öğreticilerde, bir uygulama bir kapsayıcı görüntüsüne paketlendi, görüntü Azure Container Registry’ye yüklendi ve bir Kubernetes kümesi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cefc2-116">In previous tutorials, an application was packaged into a container image, the image uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="cefc2-117">Ardından uygulama Kubernetes kümesinde çalıştırıldı.</span><span class="sxs-lookup"><span data-stu-id="cefc2-117">The application was then run on the Kubernetes cluster.</span></span> 

<span data-ttu-id="cefc2-118">Bu öğreticide ayrıca uygulama kaynak kodunu içeren bir uygulama deposu da kopyalandı ve önceden oluşturulmuş bir Docker Compose dosyası kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="cefc2-118">An application repository was also cloned which includes the application source code, and a pre-created Docker Compose file used in this tutorial.</span></span> <span data-ttu-id="cefc2-119">Deponun bir kopyasını oluşturduğunuzu ve dizinleri kopyalanmış dizine değiştirdiğinizi doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-119">Verify that you have created a clone of the repo, and that you have changed directories into the cloned directory.</span></span> <span data-ttu-id="cefc2-120">İçeride `azure-vote` adlı bir dizin ve `docker-compose.yml` adlı bir dosya bulunuyor.</span><span class="sxs-lookup"><span data-stu-id="cefc2-120">Inside is a directory named `azure-vote` and a file named `docker-compose.yml`.</span></span>

<span data-ttu-id="cefc2-121">Bu adımları tamamlamadıysanız ve takip etmek istiyorsanız, [Öğretici 1 – Kapsayıcı görüntüleri oluşturma](./container-service-tutorial-kubernetes-prepare-app.md) konusuna dönün.</span><span class="sxs-lookup"><span data-stu-id="cefc2-121">If you haven't completed these steps, and want to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

## <a name="update-application"></a><span data-ttu-id="cefc2-122">Uygulamayı güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="cefc2-122">Update application</span></span>

<span data-ttu-id="cefc2-123">Bu öğreticide, uygulamada bir değişiklik yapıldı ve güncelleştirilmiş uygulama Kubernetes kümesine dağıtıldı.</span><span class="sxs-lookup"><span data-stu-id="cefc2-123">For this tutorial, a change is made to the application, and the updated application deployed to the Kubernetes cluster.</span></span> 

<span data-ttu-id="cefc2-124">Uygulama kaynak kodu `azure-vote` dizininde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="cefc2-124">The application source code can be found inside of the `azure-vote` directory.</span></span> <span data-ttu-id="cefc2-125">`config_file.cfg` dosyasını herhangi bir kod ya da metin düzenleyici ile açın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-125">Open the `config_file.cfg` file with any code or text editor.</span></span> <span data-ttu-id="cefc2-126">Bu örnekte `vi` kullanıldı.</span><span class="sxs-lookup"><span data-stu-id="cefc2-126">In this example `vi` is used.</span></span>

```bash
vi azure-vote/azure-vote/config_file.cfg
```

<span data-ttu-id="cefc2-127">`VOTE1VALUE` ile `VOTE2VALUE` değerlerini değiştirin ve sonra dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="cefc2-127">Change the values for `VOTE1VALUE` and `VOTE2VALUE`, and then save the file.</span></span>

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

<span data-ttu-id="cefc2-128">Dosyayı kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-128">Save and close the file.</span></span>

## <a name="update-container-image"></a><span data-ttu-id="cefc2-129">Kapsayıcı görüntüsünü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="cefc2-129">Update container image</span></span>

<span data-ttu-id="cefc2-130">Ön uç görüntüsünü yeniden oluşturmak için [docker-compose](https://docs.docker.com/compose/)’u kullanın ve güncelleştirilmiş uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-130">Use [docker-compose](https://docs.docker.com/compose/) to re-create the front-end image and run the updated application.</span></span> <span data-ttu-id="cefc2-131">`--build` bağımsız değişkeni, uygulama görüntüsünü yeniden oluşturmak üzere Docker Compose'a komut vermek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cefc2-131">The `--build` argument is used to instruct Docker Compose to re-create the application image.</span></span>

```bash
docker-compose up --build -d
```

## <a name="test-application-locally"></a><span data-ttu-id="cefc2-132">Uygulamayı yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="cefc2-132">Test application locally</span></span>

<span data-ttu-id="cefc2-133">Güncelleştirilmiş uygulamayı görüntülemek için http://localhost:8080 konumuna göz atın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-133">Browse to http://localhost:8080 to see the updated application.</span></span>

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a><span data-ttu-id="cefc2-135">Görüntüleri etiketleme ve gönderme</span><span class="sxs-lookup"><span data-stu-id="cefc2-135">Tag and push images</span></span>

<span data-ttu-id="cefc2-136">`azure-vote-front` görüntüsünü, kapsayıcı kayıt defterinin loginServer’ıyla etiketleyin.</span><span class="sxs-lookup"><span data-stu-id="cefc2-136">Tag the `azure-vote-front` image with the loginServer of the container registry.</span></span> 

<span data-ttu-id="cefc2-137">[az acr list](/cli/azure/acr#list) komutuyla oturum açma sunucusu adını alın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-137">Get the login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="cefc2-138">Görüntüyü etiketlemek için [docker tag](https://docs.docker.com/engine/reference/commandline/tag/)’i kullanın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-138">Use [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) to tag the image.</span></span> <span data-ttu-id="cefc2-139">`<acrLoginServer>` değerini, Azure Container Registry oturum açma sunucu adınız veya genel kayıt defteri ana bilgisayar adınız ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cefc2-139">Replace `<acrLoginServer>` with your Azure Container Registry login server name or public registry hostname.</span></span> <span data-ttu-id="cefc2-140">Ayrıca görüntü sürümünün `redis-v2` değerine güncelleştirildiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="cefc2-140">Also notice that the image version is updated to `redis-v2`.</span></span>

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="cefc2-141">Görüntüyü kayıt defterinize yüklemek için [docker push](https://docs.docker.com/engine/reference/commandline/push/)’u kullanın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-141">Use [docker push](https://docs.docker.com/engine/reference/commandline/push/) to upload the image to your registry.</span></span> <span data-ttu-id="cefc2-142">`<acrLoginServer>` değerini, Azure Container Registry oturum açma sunucu adınız ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cefc2-142">Replace `<acrLoginServer>` with your Azure Container Registry login server name.</span></span>

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a><span data-ttu-id="cefc2-143">Güncelleştirilmiş uygulamayı dağıtma</span><span class="sxs-lookup"><span data-stu-id="cefc2-143">Deploy update application</span></span>

<span data-ttu-id="cefc2-144">En uzun çalışma süresini sağlamak için uygulama podunun birden çok örneğinin çalıştırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="cefc2-144">To ensure maximum uptime, multiple instances of the application pod must be running.</span></span> <span data-ttu-id="cefc2-145">Bu yapılandırmayı [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutu ile doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-145">Verify this configuration with the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span>

```bash
kubectl get pod
```

<span data-ttu-id="cefc2-146">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cefc2-146">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

<span data-ttu-id="cefc2-147">azure-vote-front görüntüsünü çalıştıran birden çok podunuz yoksa, `azure-vote-front` dağıtımını ölçeklendirin.</span><span class="sxs-lookup"><span data-stu-id="cefc2-147">If you do not have multiple pods running the azure-vote-front image, scale the `azure-vote-front` deployment.</span></span>


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

<span data-ttu-id="cefc2-148">Uygulamayı güncelleştirmek için [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-148">To update the application, use the [kubectl set](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) command.</span></span> <span data-ttu-id="cefc2-149">`<acrLoginServer>` öğesini, kapsayıcı kayıt defterinizin oturum açma sunucusu veya ana bilgisayar adıyla güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="cefc2-149">Update `<acrLoginServer>` with the login server or host name of your container registry.</span></span>

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

<span data-ttu-id="cefc2-150">Dağıtımı izlemek için [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-150">To monitor the deployment, use the [kubectl get pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) command.</span></span> <span data-ttu-id="cefc2-151">Güncelleştirilmiş uygulama dağıtıldığında, podlarınız sonlandırılır ve yeni kapsayıcı görüntüsüyle yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="cefc2-151">As the updated application is deployed, your pods are terminated and re-created with the new container image.</span></span>

```azurecli-interactive
kubectl get pod
```

<span data-ttu-id="cefc2-152">Çıktı:</span><span class="sxs-lookup"><span data-stu-id="cefc2-152">Output:</span></span>

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a><span data-ttu-id="cefc2-153">Güncelleştirilmiş uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="cefc2-153">Test updated application</span></span>

<span data-ttu-id="cefc2-154">`azure-vote-front` hizmetinin dış IP adresini alın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-154">Get the external IP address of the `azure-vote-front` service.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front
```

<span data-ttu-id="cefc2-155">Güncelleştirilmiş uygulamayı görüntülemek için IP adresine göz atın.</span><span class="sxs-lookup"><span data-stu-id="cefc2-155">Browse to the IP address to see the updated application.</span></span>

![Azure’da Kubernetes kümesinin görüntüsü](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a><span data-ttu-id="cefc2-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cefc2-157">Next steps</span></span>

<span data-ttu-id="cefc2-158">Bu öğreticide, bir uygulamayı güncelleştirdiniz ve bu güncelleştirmeyi bir Kubernetes kümesine sundunuz.</span><span class="sxs-lookup"><span data-stu-id="cefc2-158">In this tutorial, you updated an application and rolled out this update to a Kubernetes cluster.</span></span> <span data-ttu-id="cefc2-159">Şu görevler tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="cefc2-159">The following tasks were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cefc2-160">Ön uç uygulaması kodu güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="cefc2-160">Updated the front-end application code</span></span>
> * <span data-ttu-id="cefc2-161">Güncelleştirilmiş kapsayıcı görüntüsü oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="cefc2-161">Created an updated container image</span></span>
> * <span data-ttu-id="cefc2-162">Kapsayıcı görüntüsü Azure Container Registry’ye gönderildi</span><span class="sxs-lookup"><span data-stu-id="cefc2-162">Pushed the container image to Azure Container Registry</span></span>
> * <span data-ttu-id="cefc2-163">Güncelleştirilmiş uygulama dağıtıldı</span><span class="sxs-lookup"><span data-stu-id="cefc2-163">Deployed the updated application</span></span>

<span data-ttu-id="cefc2-164">Operations Management Suite ile Kubernetes’in nasıl izlenileceği hakkında bilgi edinmek için sonraki öğreticiye ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="cefc2-164">Advance to the next tutorial to learn about how to monitor Kubernetes with Operations Management Suite.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cefc2-165">OMS ile Kubernetes’i izleme</span><span class="sxs-lookup"><span data-stu-id="cefc2-165">Monitor Kubernetes with OMS</span></span>](./container-service-tutorial-kubernetes-monitor.md)