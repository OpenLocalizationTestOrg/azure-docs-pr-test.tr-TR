---
title: "Azure Kubernetes Helm ile aaaDeploy kapsayıcıları | Microsoft Docs"
description: "Azure kapsayıcı hizmeti Kubernetes kümesinde Hello Helm paketleme aracı toodeploy kapsayıcıları kullanma"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="aedbf-103">Kubernetes kümede Helm toodeploy kapsayıcılar kullanma</span><span class="sxs-lookup"><span data-stu-id="aedbf-103">Use Helm toodeploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="aedbf-104">[Helm](https://github.com/kubernetes/helm/) yükleyip Kubernetes uygulamaların hello yaşam döngüsünü yönetmenize yardımcı olan bir açık kaynak paketleme aracıdır.</span><span class="sxs-lookup"><span data-stu-id="aedbf-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage hello lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="aedbf-105">Benzer tooLinux paket yöneticileri Apt get ve Yum gibi Helm paketleri önceden yapılandırılmış Kubernetes kaynakların kullanılan toomanage Kubernetes grafikler, ' dir.</span><span class="sxs-lookup"><span data-stu-id="aedbf-105">Similar tooLinux package managers such as Apt-get and Yum, Helm is used toomanage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="aedbf-106">Bu makalede, Azure kapsayıcı Hizmeti'nde bir Kubernetes kümesinde toowork Helm ile nasıl dağıtılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="aedbf-106">This article shows you how toowork with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="aedbf-107">Helm iki bileşenden oluşur:</span><span class="sxs-lookup"><span data-stu-id="aedbf-107">Helm has two components:</span></span> 
* <span data-ttu-id="aedbf-108">Merhaba **Helm CLI** makinenizde yerel olarak veya hello bulutta çalışan bir istemci</span><span class="sxs-lookup"><span data-stu-id="aedbf-108">hello **Helm CLI** is a client that runs on your machine locally or in hello cloud</span></span>  

* <span data-ttu-id="aedbf-109">**Tiller** hello Kubernetes kümede çalışan ve hello yaşam Kubernetes uygulamalarınızın yönetir. bir sunucu</span><span class="sxs-lookup"><span data-stu-id="aedbf-109">**Tiller** is a server that runs on hello Kubernetes cluster and manages hello lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="aedbf-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="aedbf-110">Prerequisites</span></span>

* <span data-ttu-id="aedbf-111">[Kubernetes küme oluşturma](container-service-kubernetes-walkthrough.md) Azure kapsayıcı Hizmeti'nde</span><span class="sxs-lookup"><span data-stu-id="aedbf-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="aedbf-112">[Yükleme ve yapılandırma `kubectl` ](../container-service-connect.md) yerel bir bilgisayarda</span><span class="sxs-lookup"><span data-stu-id="aedbf-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="aedbf-113">[Helm yüklemek](https://github.com/kubernetes/helm/blob/master/docs/install.md) yerel bir bilgisayarda</span><span class="sxs-lookup"><span data-stu-id="aedbf-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="aedbf-114">Helm temelleri</span><span class="sxs-lookup"><span data-stu-id="aedbf-114">Helm basics</span></span> 

<span data-ttu-id="aedbf-115">Merhaba Kubernetes küme hakkında Tiller yükleme ve komut aşağıdaki hello yazmak için uygulamalarınızı dağıtma olduğundan tooview bilgi:</span><span class="sxs-lookup"><span data-stu-id="aedbf-115">tooview information about hello Kubernetes cluster that you are installing Tiller and deploying your applications to, type hello following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl küme bilgisi](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="aedbf-117">Helm yükledikten sonra Tiller hello aşağıdaki komutu yazarak Kubernetes kümenizde yükleyin:</span><span class="sxs-lookup"><span data-stu-id="aedbf-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing hello following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="aedbf-118">Başarıyla tamamlandığında, çıkış hello aşağıdaki gibi bakın:</span><span class="sxs-lookup"><span data-stu-id="aedbf-118">When it completes successfully, you see output like hello following:</span></span>

![Tiller yükleme](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="aedbf-120">tooview tüm hello Helm grafiklerde kullanılabilir hello deposu, aşağıdaki türü hello komutu:</span><span class="sxs-lookup"><span data-stu-id="aedbf-120">tooview all hello Helm charts available in hello repository, type hello following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="aedbf-121">Merhaba aşağıdaki gibi bir çıktı bakın:</span><span class="sxs-lookup"><span data-stu-id="aedbf-121">You see output like hello following:</span></span>

![Helm arama](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="aedbf-123">tooupdate hello grafikleri tooget hello en son sürümleri, yazın:</span><span class="sxs-lookup"><span data-stu-id="aedbf-123">tooupdate hello charts tooget hello latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="aedbf-124">Bir Nginx giriş denetleyicisi grafik dağıtma</span><span class="sxs-lookup"><span data-stu-id="aedbf-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="aedbf-125">toodeploy Nginx giriş denetleyicisi grafik, tek bir komut yazın:</span><span class="sxs-lookup"><span data-stu-id="aedbf-125">toodeploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Giriş denetleyicisi dağıtma](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="aedbf-127">Yazarsanız `kubectl get svc` tooview hello küme üzerinde çalışan tüm hizmetleri, bir IP adresi toohello giriş denetleyicisi atanır bakın.</span><span class="sxs-lookup"><span data-stu-id="aedbf-127">If you type `kubectl get svc` tooview all services that are running on hello cluster, you see that an IP address is assigned toohello ingress controller.</span></span> <span data-ttu-id="aedbf-128">(Merhaba atama işlemi devam ederken, gördüğünüz `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="aedbf-128">(While hello assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="aedbf-129">İşlem birkaç dakika toocomplete alır.)</span><span class="sxs-lookup"><span data-stu-id="aedbf-129">It takes a couple of minutes toocomplete.)</span></span> 

<span data-ttu-id="aedbf-130">Başlangıç IP adresi atandıktan sonra çalışan hello dış IP adresi toosee hello Nginx arka uç toohello değerini gidin.</span><span class="sxs-lookup"><span data-stu-id="aedbf-130">After hello IP address is assigned, navigate toohello value of hello external IP address toosee hello Nginx backend running.</span></span> 
 
![Giriş IP adresi](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="aedbf-132">toosee kümenizde türü yüklü grafikleri listesi:</span><span class="sxs-lookup"><span data-stu-id="aedbf-132">toosee a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="aedbf-133">Merhaba komutu çok kısaltma`helm ls`.</span><span class="sxs-lookup"><span data-stu-id="aedbf-133">You can abbreviate hello command too`helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="aedbf-134">MariaDB grafik ve istemci dağıtma</span><span class="sxs-lookup"><span data-stu-id="aedbf-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="aedbf-135">Şimdi bir MariaDB grafik ve MariaDB istemci tooconnect toohello veritabanı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="aedbf-135">Now deploy a MariaDB chart and a MariaDB client tooconnect toohello database.</span></span>

<span data-ttu-id="aedbf-136">toodeploy hello MariaDB grafik, komutu aşağıdaki türü hello:</span><span class="sxs-lookup"><span data-stu-id="aedbf-136">toodeploy hello MariaDB chart, type hello following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="aedbf-137">Burada `--name` olan sürümleri için kullanılan bir etiket.</span><span class="sxs-lookup"><span data-stu-id="aedbf-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="aedbf-138">Merhaba dağıtımı başarısız olursa çalıştırmak `helm repo update` ve yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="aedbf-138">If hello deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="aedbf-139">tooview tüm hello grafikler kümenizde türü dağıtılan:</span><span class="sxs-lookup"><span data-stu-id="aedbf-139">tooview all hello charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="aedbf-140">tooview, küme üzerinde çalışan tüm dağıtımlar yazın:</span><span class="sxs-lookup"><span data-stu-id="aedbf-140">tooview all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="aedbf-141">Son olarak, toorun pod tooaccess hello istemci yazın:</span><span class="sxs-lookup"><span data-stu-id="aedbf-141">Finally, toorun a pod tooaccess hello client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="aedbf-142">tooconnect toohello istemci, aşağıdaki komut, değiştirme türü hello `v1-mariadb` dağıtımınızın hello adıyla:</span><span class="sxs-lookup"><span data-stu-id="aedbf-142">tooconnect toohello client, type hello following command, replacing `v1-mariadb` with hello name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="aedbf-143">Şimdi kullanabileceğiniz standart SQL komutlarını toocreate veritabanları, tablolar vb.. Örneğin, `Create DATABASE testdb1;` boş bir veritabanı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="aedbf-143">You can now use standard SQL commands toocreate databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="aedbf-144">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aedbf-144">Next steps</span></span>

* <span data-ttu-id="aedbf-145">Merhaba Kubernetes grafikleri yönetme hakkında daha fazla bilgi için bkz: [Helm belgelerine](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="aedbf-145">For more information about managing Kubernetes charts, see hello [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

