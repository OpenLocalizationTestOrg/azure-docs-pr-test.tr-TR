---
title: "İzleyici Azure Kubernetes küme - Operations Management | Microsoft Docs"
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
ms.openlocfilehash: bd5c81435c091d25bc14710589b7c043e9f56a25
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="f4e90-103">İzleyici bir Azure kapsayıcı hizmeti kümesi Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="f4e90-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f4e90-104">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f4e90-104">Prerequisites</span></span>
<span data-ttu-id="f4e90-105">Bu kılavuz, sahibi olduğunuzu varsayar [Azure kapsayıcı hizmeti kullanarak Kubernetes küme oluşturulan](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="f4e90-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="f4e90-106">Ayrıca, sahibi olduğunuzu varsayar `az` Azure CLI ve `kubectl` araçları yüklü.</span><span class="sxs-lookup"><span data-stu-id="f4e90-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="f4e90-107">Varsa, test edebilirsiniz `az` çalıştırarak yüklü aracı:</span><span class="sxs-lookup"><span data-stu-id="f4e90-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="f4e90-108">Sahip değilseniz `az` yüklü, aracı yönergeler vardır [burada](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="f4e90-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="f4e90-109">Alternatif olarak, kullanabileceğiniz [Azure bulut Kabuk](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), sahip olduğu `az` Azure CLI ve `kubectl` Araçları zaten yüklenmiş.</span><span class="sxs-lookup"><span data-stu-id="f4e90-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has the `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="f4e90-110">Varsa, test edebilirsiniz `kubectl` çalıştırarak yüklü aracı:</span><span class="sxs-lookup"><span data-stu-id="f4e90-110">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="f4e90-111">Sahip değilseniz `kubectl` yüklü çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f4e90-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="f4e90-112">Kubectl aracınızı çalıştırabilirsiniz yüklü kubernetes anahtarları varsa test etmek için:</span><span class="sxs-lookup"><span data-stu-id="f4e90-112">To test if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="f4e90-113">Yukarıdaki komut hataları çıkışı, kubernetes küme anahtarları kubectl aracına yüklemeniz gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="f4e90-113">If the above command errors out, you need to install kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="f4e90-114">Bunu aşağıdaki komutla yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f4e90-114">You can do that with the following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="f4e90-115">Operations Management Suite (OMS) ile izleme kapsayıcıları</span><span class="sxs-lookup"><span data-stu-id="f4e90-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="f4e90-116">Microsoft Operations Management (OMS) yönetmenize ve şirket içi korumak ve altyapı bulut yardımcı olan Microsoft'un bulut tabanlı BT yönetimi çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="f4e90-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="f4e90-117">Kapsayıcı, tek bir konumda kapsayıcı envanter, performans ve günlükleri görüntülemenize yardımcı OMS günlük analizi çözümde çözümüdür.</span><span class="sxs-lookup"><span data-stu-id="f4e90-117">Container Solution is a solution in OMS Log Analytics, which helps you view the container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="f4e90-118">Denetim, merkezi konumda günlükler görüntüleyerek kapsayıcıları sorun giderme ve bir ana bilgisayar üzerindeki fazladan kapsayıcı tüketen gürültülü bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4e90-118">You can audit, troubleshoot containers by viewing the logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="f4e90-119">Kapsayıcı çözüm hakkında daha fazla bilgi için lütfen başvurmak [kapsayıcı çözüm günlük analizi](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="f4e90-119">For more information about Container Solution, please refer to the [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="f4e90-120">OMS Kubernetes üzerinde yükleme</span><span class="sxs-lookup"><span data-stu-id="f4e90-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="f4e90-121">Çalışma alanı kimliği ve anahtarı edinin</span><span class="sxs-lookup"><span data-stu-id="f4e90-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="f4e90-122">İçin OMS aracısı hizmetine iletişim kurabilecek şekilde bir çalışma alanı kimliği ve çalışma alanı anahtarı ile yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4e90-122">For the OMS agent to talk to the service it needs to be configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="f4e90-123">Çalışma alanı kimliği ve anahtarı OMS hesabı oluşturmanız gerekir almak için <https://mms.microsoft.com>. Lütfen bir hesap oluşturmak için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="f4e90-123">To get the workspace id and key you need to create an OMS account at <https://mms.microsoft.com>. Please follow the steps to create an account.</span></span> <span data-ttu-id="f4e90-124">İşiniz bittiğinde tıklayarak kimliği ve anahtarı elde etmeniz hesabı oluşturma, **ayarları**, sonra **bağlı kaynakları**ve ardından **Linux sunucuları**, aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="f4e90-124">Once you are done creating the account, you need to obtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-the-oms-agent-using-a-daemonset"></a><span data-ttu-id="f4e90-125">Bir DaemonSet kullanarak OMS aracısı yükleyin</span><span class="sxs-lookup"><span data-stu-id="f4e90-125">Install the OMS agent using a DaemonSet</span></span>
<span data-ttu-id="f4e90-126">DaemonSets Kubernetes tarafından bir kapsayıcı tek bir örneği kümedeki her ana bilgisayarda çalıştırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f4e90-126">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="f4e90-127">Bunlar izleme aracıları çalıştırmak için mükemmel.</span><span class="sxs-lookup"><span data-stu-id="f4e90-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="f4e90-128">Burada [DaemonSet YAML dosya](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="f4e90-128">Here is the [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="f4e90-129">Adlı bir dosyaya Kaydet `oms-daemonset.yaml` ve yer tutucu değerlerini değiştirme `WSID` ve `KEY` çalışma alanı kimliği ve anahtarı dosyasında.</span><span class="sxs-lookup"><span data-stu-id="f4e90-129">Save it to a file named `oms-daemonset.yaml` and replace the place-holder values for `WSID` and `KEY` with your workspace id and key in the file.</span></span>

<span data-ttu-id="f4e90-130">Çalışma alanı kimliği ve anahtarı DaemonSet yapılandırma ekledikten sonra kümenizdeki ile OMS Aracısı'nı yükleyebilirsiniz `kubectl` komut satırı aracı:</span><span class="sxs-lookup"><span data-stu-id="f4e90-130">Once you have added your workspace ID and key to the DaemonSet configuration, you can install the OMS agent on your cluster with the `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-the-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="f4e90-131">Kubernetes gizli anahtarı kullanarak OMS Aracısı yükleniyor</span><span class="sxs-lookup"><span data-stu-id="f4e90-131">Installing the OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="f4e90-132">OMS çalışma alanı Kimliğinizi korumak ve anahtarını Kubernetes gizli DaemonSet YAML dosyasının bir parçası olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4e90-132">To protect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="f4e90-133">Komut dosyası, gizli şablon dosyasını ve DaemonSet YAML dosyasını kopyalayın (gelen [depo](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) ve aynı dizinde olduklarından emin olun.</span><span class="sxs-lookup"><span data-stu-id="f4e90-133">Copy the script, secret template file and the DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on the same directory.</span></span> 
      - <span data-ttu-id="f4e90-134">Komut dosyası - gizli gen.sh üretiliyor gizli</span><span class="sxs-lookup"><span data-stu-id="f4e90-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="f4e90-135">Gizli şablon - gizli template.yaml</span><span class="sxs-lookup"><span data-stu-id="f4e90-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="f4e90-136">DaemonSet YAML dosyası - omsagent ds secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="f4e90-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="f4e90-137">Komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f4e90-137">Run the script.</span></span> <span data-ttu-id="f4e90-138">Komut dosyası OMS çalışma alanı kimliği ve birincil anahtar için sorar.</span><span class="sxs-lookup"><span data-stu-id="f4e90-138">The script will ask for the OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="f4e90-139">Lütfen, yerleştirin ve onu çalıştırabilmeniz için komut dosyasını bir gizli yaml dosyası oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f4e90-139">Please insert that and the script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="f4e90-140">Gizli pod aşağıdaki çalıştırarak oluşturun:``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="f4e90-140">Create the secrets pod by running the following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="f4e90-141">Denetlemek için şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f4e90-141">To check, run the following:</span></span> 

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
 
  - <span data-ttu-id="f4e90-142">Arka plan programı kümesi çalıştırarak, omsagent oluşturma``` kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="f4e90-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="f4e90-143">Sonuç</span><span class="sxs-lookup"><span data-stu-id="f4e90-143">Conclusion</span></span>
<span data-ttu-id="f4e90-144">İşte bu kadar!</span><span class="sxs-lookup"><span data-stu-id="f4e90-144">That's it!</span></span> <span data-ttu-id="f4e90-145">Birkaç dakika sonra OMS panonuz akan verileri görüyor olmalısınız.</span><span class="sxs-lookup"><span data-stu-id="f4e90-145">After a few minutes, you should be able to see data flowing to your OMS dashboard.</span></span>
