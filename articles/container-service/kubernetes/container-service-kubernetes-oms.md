---
title: "aaaMonitor Azure Kubernetes küme - Operations Management | Microsoft Docs"
description: "Microsoft Operations Management Suite kullanarak Azure kapsayıcı hizmeti kümesinde Kubernetes izleme"
services: container-service
documentationcenter: 
author: bburns
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="718ff-103">İzleyici bir Azure kapsayıcı hizmeti kümesi Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="718ff-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="718ff-104">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="718ff-104">Prerequisites</span></span>
<span data-ttu-id="718ff-105">Bu kılavuz, sahibi olduğunuzu varsayar [Azure kapsayıcı hizmeti kullanarak Kubernetes küme oluşturulan](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="718ff-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="718ff-106">Ayrıca, hello sahibi olduğunuzu varsayar `az` Azure CLI ve `kubectl` araçları yüklü.</span><span class="sxs-lookup"><span data-stu-id="718ff-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="718ff-107">Merhaba varsa test edebilirsiniz `az` çalıştırarak yüklü aracı:</span><span class="sxs-lookup"><span data-stu-id="718ff-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="718ff-108">Merhaba yoksa `az` yüklü, aracı yönergeler vardır [burada](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="718ff-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="718ff-109">Alternatif olarak, kullanabileceğiniz [Azure bulut Kabuk](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), hello olan `az` Azure CLI ve `kubectl` Araçları zaten yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="718ff-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has hello `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="718ff-110">Merhaba varsa test edebilirsiniz `kubectl` çalıştırarak yüklü aracı:</span><span class="sxs-lookup"><span data-stu-id="718ff-110">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="718ff-111">Sahip değilseniz `kubectl` yüklü çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="718ff-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="718ff-112">kubectl aracına kubernetes anahtarları varsa tootest çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="718ff-112">tootest if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="718ff-113">Merhaba, komut hataları, kubectl aracına tooinstall kubernetes küme anahtarları gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="718ff-113">If hello above command errors out, you need tooinstall kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="718ff-114">Bu komutu aşağıdaki hello ile yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="718ff-114">You can do that with hello following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="718ff-115">Operations Management Suite (OMS) ile izleme kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="718ff-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="718ff-116">Microsoft Operations Management (OMS) yönetmenize ve şirket içi korumak ve altyapı bulut yardımcı olan Microsoft'un bulut tabanlı BT yönetimi çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="718ff-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="718ff-117">Kapsayıcı, bir çözümde hello kapsayıcı envanterini görüntüleme, performans ve günlükleri tek bir konumda yardımcı olan OMS günlük analizi çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="718ff-117">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="718ff-118">Denetim, merkezi konumda hello günlükleri görüntüleyerek kapsayıcıları sorun giderme ve bir ana bilgisayar üzerindeki fazladan kapsayıcı tüketen gürültülü bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="718ff-118">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="718ff-119">Kapsayıcı çözüm hakkında daha fazla bilgi için lütfen toothe bakın [kapsayıcı çözüm günlük analizi](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="718ff-119">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="718ff-120">OMS Kubernetes üzerinde yükleme</span><span class="sxs-lookup"><span data-stu-id="718ff-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="718ff-121">Çalışma alanı kimliği ve anahtarı edinin</span><span class="sxs-lookup"><span data-stu-id="718ff-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="718ff-122">Merhaba OMS Aracısı tootalk toohello hizmeti için bir çalışma alanı kimliği ve çalışma alanı anahtarı ile yapılandırılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="718ff-122">For hello OMS agent tootalk toohello service it needs toobe configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="718ff-123">Hesap tooget hello çalışma alanı kimliği ve anahtarı toocreate bir OMS ihtiyacınız adresindeki <https://mms.microsoft.com>. Lütfen başlangıç adımları toocreate bir hesap izleyin.</span><span class="sxs-lookup"><span data-stu-id="718ff-123">tooget hello workspace id and key you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="718ff-124">Merhaba hesabı oluşturulurken tamamladıktan sonra tooobtain kimliği ve anahtarı tıklayarak ihtiyacınız **ayarları**, ardından **bağlı kaynakları**ve ardından **Linux sunucuları**, aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="718ff-124">Once you are done creating hello account, you need tooobtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a><span data-ttu-id="718ff-125">Bir DaemonSet kullanarak hello OMS aracı yükleme</span><span class="sxs-lookup"><span data-stu-id="718ff-125">Install hello OMS agent using a DaemonSet</span></span>
<span data-ttu-id="718ff-126">DaemonSets Kubernetes toorun tarafından kullanılan bir kapsayıcı hello kümedeki her ana bilgisayarda tek bir örneği.</span><span class="sxs-lookup"><span data-stu-id="718ff-126">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="718ff-127">Bunlar izleme aracıları çalıştırmak için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="718ff-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="718ff-128">Merhaba işte [DaemonSet YAML dosya](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="718ff-128">Here is hello [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="718ff-129">Kaydedin tooa dosya adlı `oms-daemonset.yaml` ve hello yer tutucu değerlerini değiştirme `WSID` ve `KEY` çalışma alanı kimliği ve anahtarı hello dosyasında.</span><span class="sxs-lookup"><span data-stu-id="718ff-129">Save it tooa file named `oms-daemonset.yaml` and replace hello place-holder values for `WSID` and `KEY` with your workspace id and key in hello file.</span></span>

<span data-ttu-id="718ff-130">Çalışma alanı kimliği ve anahtarı toohello DaemonSet yapılandırma ekledikten sonra kümenizdeki hello ile Merhaba OMS Aracısı yükleyebilirsiniz `kubectl` komut satırı aracı:</span><span class="sxs-lookup"><span data-stu-id="718ff-130">Once you have added your workspace ID and key toohello DaemonSet configuration, you can install hello OMS agent on your cluster with hello `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="718ff-131">Merhaba OMS Aracısı Kubernetes gizli anahtarı kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="718ff-131">Installing hello OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="718ff-132">tooprotect OMS çalışma alanı kimliği ve anahtarı Kubernetes gizli DaemonSet YAML dosyasının bir parçası olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="718ff-132">tooprotect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="718ff-133">Merhaba komut dosyası, gizli şablon dosyası ve hello DaemonSet YAML dosya kopyalama (gelen [depo](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) ve üzerinde hello olduklarından emin olmak aynı dizin.</span><span class="sxs-lookup"><span data-stu-id="718ff-133">Copy hello script, secret template file and hello DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on hello same directory.</span></span> 
      - <span data-ttu-id="718ff-134">Komut dosyası - gizli gen.sh üretiliyor gizli</span><span class="sxs-lookup"><span data-stu-id="718ff-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="718ff-135">Gizli şablon - gizli template.yaml</span><span class="sxs-lookup"><span data-stu-id="718ff-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="718ff-136">DaemonSet YAML dosyası - omsagent ds secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="718ff-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="718ff-137">Merhaba komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="718ff-137">Run hello script.</span></span> <span data-ttu-id="718ff-138">Merhaba betik Merhaba OMS çalışma alanı kimliği ve birincil anahtar sorar.</span><span class="sxs-lookup"><span data-stu-id="718ff-138">hello script will ask for hello OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="718ff-139">Lütfen, Ekle ve çalıştırabilirsiniz şekilde hello betik gizli yaml dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="718ff-139">Please insert that and hello script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="718ff-140">Merhaba gizli pod hello aşağıdakini çalıştırarak oluşturun:``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="718ff-140">Create hello secrets pod by running hello following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="718ff-141">toocheck, Hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="718ff-141">toocheck, run hello following:</span></span> 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - <span data-ttu-id="718ff-142">Arka plan programı kümesi çalıştırarak, omsagent oluşturma``` kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="718ff-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="718ff-143">Sonuç</span><span class="sxs-lookup"><span data-stu-id="718ff-143">Conclusion</span></span>
<span data-ttu-id="718ff-144">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="718ff-144">That's it!</span></span> <span data-ttu-id="718ff-145">Birkaç dakika sonra tooyour OMS Pano akan mümkün toosee veriler olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="718ff-145">After a few minutes, you should be able toosee data flowing tooyour OMS dashboard.</span></span>
