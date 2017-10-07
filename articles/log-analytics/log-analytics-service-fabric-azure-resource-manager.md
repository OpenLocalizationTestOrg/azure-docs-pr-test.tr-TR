---
title: "Günlük analizi kullanarak Service Fabric uygulamaları aaaAssess hello Azure portalı | Microsoft Docs"
description: "Günlük hello Azure portal tooassess hello risk ve Service Fabric uygulamalarınızı durumunu kullanarak analizleri hello Service Fabric çözüm kullanabilir mikro hizmetler, düğümleri ve kümelerini."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 9c91aacb-c48e-466c-b792-261f25940c0c
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: nini
ms.openlocfilehash: 891c7f6e5ed511ac18599bdc280ab3dc09700fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-hello-azure-portal"></a><span data-ttu-id="daa1d-103">Service Fabric uygulamaları ve mikro hizmetler hello Azure portal ile değerlendirin</span><span class="sxs-lookup"><span data-stu-id="daa1d-103">Assess Service Fabric applications and micro-services with hello Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="daa1d-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="daa1d-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="daa1d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="daa1d-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Service Fabric simgesi](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="daa1d-107">Bu makalede nasıl toouse hello günlük analizi toohelp Service Fabric çözümde tanımlamak ve Service Fabric küme genelinde sorunlarını giderme açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="daa1d-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="daa1d-108">Merhaba Service Fabric çözümü bu verileri Azure WAD tablolardan toplayarak Service Fabric Vm'lerinizi Azure Tanılama verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="daa1d-108">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="daa1d-109">Günlük analizi, Service Fabric framework olaylar dahil olmak üzere, daha sonra okur **güvenilir hizmeti olayları**, **aktör olayları**, **çalışma olaylarını**, ve **özel ETW olayları**.</span><span class="sxs-lookup"><span data-stu-id="daa1d-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="daa1d-110">Merhaba çözüm panosu ile Service Fabric ortamınızda mümkün tooview önemli sorunlar ve ilgili olayları şunlardır.</span><span class="sxs-lookup"><span data-stu-id="daa1d-110">With hello solution dashboard, you are able tooview notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="daa1d-111">Merhaba çözümüyle başlatılan tooget tooconnect ihtiyacınız Service Fabric kümesi tooa günlük analizi çalışma alanı.</span><span class="sxs-lookup"><span data-stu-id="daa1d-111">tooget started with hello solution, you need tooconnect your Service Fabric cluster tooa Log Analytics workspace.</span></span> <span data-ttu-id="daa1d-112">Üç senaryoları tooconsider şunlardır:</span><span class="sxs-lookup"><span data-stu-id="daa1d-112">Here are three scenarios tooconsider:</span></span>

1. <span data-ttu-id="daa1d-113">Service Fabric kümesi dağıtmadıysanız hello adımlarda kullanmak ***bir Service Fabric kümesi bağlı tooa günlük analizi çalışma alanı dağıtma*** toodeploy yeni bir küme ve tooreport tooLog Analytics yapılandırılmamış olabilir.</span><span class="sxs-lookup"><span data-stu-id="daa1d-113">If you have not deployed your Service Fabric cluster, use hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace*** toodeploy a new cluster and have it configured tooreport tooLog Analytics.</span></span>
2. <span data-ttu-id="daa1d-114">Konakları toouse toocollect performans sayaçları, Service Fabric kümesi güvenlik gibi diğer OMS çözümleri gerekiyorsa hello adımları ***Service Fabric kümesi bağlı tooa günlük analizi çalışma alanı VM uzantısı ile dağıtma yüklü.***</span><span class="sxs-lookup"><span data-stu-id="daa1d-114">If you need toocollect performance counters from your hosts toouse other OMS solutions such as Security on your Service Fabric Cluster, follow hello steps in ***Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="daa1d-115">Service Fabric kümesi zaten dağıttıysanız ve tooconnect istiyorsanız bunu tooLog Analytics, hello adımlarını izleyin ***var olan bir depolama hesabı tooLog Analytics ekleme.***</span><span class="sxs-lookup"><span data-stu-id="daa1d-115">If you have already deployed your Service Fabric cluster and want tooconnect it tooLog Analytics, follow hello steps in ***Adding an existing storage account tooLog Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace"></a><span data-ttu-id="daa1d-116">Service Fabric kümesi bağlı tooa günlük analizi çalışma alanı dağıtın.</span><span class="sxs-lookup"><span data-stu-id="daa1d-116">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace.</span></span>
<span data-ttu-id="daa1d-117">Bu şablon, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="daa1d-117">This template does hello following:</span></span>

1. <span data-ttu-id="daa1d-118">Azure Service Fabric kümesi zaten bağlı tooa günlük analizi çalışma alanı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="daa1d-118">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="daa1d-119">Yeni bir çalışma alanı hello şablon ya da zaten varolan bir günlük analizi çalışma alanını giriş hello adını dağıtırken hello seçeneği toocreate sahip.</span><span class="sxs-lookup"><span data-stu-id="daa1d-119">You have hello option toocreate a new workspace while deploying hello template, or input hello name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="daa1d-120">Merhaba tanılama depolama hesabı toohello günlük analizi çalışma alanı ekler.</span><span class="sxs-lookup"><span data-stu-id="daa1d-120">Adds hello diagnostic storage account toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="daa1d-121">Günlük analizi çalışma alanınızdaki Hello Service Fabric çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="daa1d-121">Enables hello Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="daa1d-122">[![TooAzure dağıtma](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="daa1d-122">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="daa1d-123">Seçtiğinizde, bundan sonra hello Dağıt düğmesi yukarıdaki, Azure portalı açıldığında, tooedit parametrelere sahip hello.</span><span class="sxs-lookup"><span data-stu-id="daa1d-123">Once you select hello deploy button above, hello Azure portal opens with parameters for you tooedit.</span></span> <span data-ttu-id="daa1d-124">Emin toocreate yeni bir kaynak grubu şöyle bir yeni günlük analizi çalışma alanı adı girin:</span><span class="sxs-lookup"><span data-stu-id="daa1d-124">Be sure toocreate a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="daa1d-127">Merhaba yasal koşulları kabul edin ve tıklatın **oluşturma** toostart hello dağıtım.</span><span class="sxs-lookup"><span data-stu-id="daa1d-127">Accept hello legal terms and click **Create** toostart hello deployment.</span></span> <span data-ttu-id="daa1d-128">Merhaba dağıtım tamamlandıktan sonra bkz: hello yeni çalışma ve oluşturulan küme ve gerekir WADServiceFabric hello * eklenen olayı, WADWindowsEventLogs ve WADETWEvent tabloları:</span><span class="sxs-lookup"><span data-stu-id="daa1d-128">Once hello deployment is completed, you should see hello new workspace and cluster created, and hello WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-tooa-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="daa1d-130">Service Fabric kümesi bağlı tooa günlük analizi çalışma alanı VM uzantısı ile dağıtın.</span><span class="sxs-lookup"><span data-stu-id="daa1d-130">Deploy a Service Fabric Cluster connected tooa Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="daa1d-131">Bu şablon, aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="daa1d-131">This template does hello following:</span></span>

1. <span data-ttu-id="daa1d-132">Azure Service Fabric kümesi zaten bağlı tooa günlük analizi çalışma alanı dağıtır.</span><span class="sxs-lookup"><span data-stu-id="daa1d-132">Deploys an Azure Service Fabric cluster already connected tooa Log Analytics workspace.</span></span> <span data-ttu-id="daa1d-133">Yeni bir çalışma alanı oluşturun veya var olan bir kullanın.</span><span class="sxs-lookup"><span data-stu-id="daa1d-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="daa1d-134">Merhaba tanılama depolama hesapları toohello günlük analizi çalışma alanı ekler.</span><span class="sxs-lookup"><span data-stu-id="daa1d-134">Adds hello diagnostic storage accounts toohello Log Analytics workspace.</span></span>
3. <span data-ttu-id="daa1d-135">Merhaba günlük analizi çalışma alanındaki Hello Service Fabric çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="daa1d-135">Enables hello Service Fabric solution in hello Log Analytics workspace.</span></span>
4. <span data-ttu-id="daa1d-136">Service Fabric kümesi her sanal makine ölçek Hello MMA Aracı Uzantısı yükler.</span><span class="sxs-lookup"><span data-stu-id="daa1d-136">Installs hello MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="daa1d-137">Yüklü hello MMA aracıyla düğümleriniz hakkında mümkün tooview performans ölçümleri olduğunuz.</span><span class="sxs-lookup"><span data-stu-id="daa1d-137">With hello MMA agent installed, you are able tooview performance metrics about your nodes.</span></span>

<span data-ttu-id="daa1d-138">[![TooAzure dağıtma](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="daa1d-138">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="daa1d-139">Aşağıdaki yukarıdaki, giriş hello gerekli parametreleri aynı adımları hello ve dağıtımı devre dışı tetiklersiniz.</span><span class="sxs-lookup"><span data-stu-id="daa1d-139">Following hello same steps above, input hello necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="daa1d-140">Bir kez daha hello yeni çalışma alanı, küme ve WAD tablolar tüm oluşturulan görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="daa1d-140">Once again you should see hello new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="daa1d-142">Performans verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="daa1d-142">Viewing Performance Data</span></span>

<span data-ttu-id="daa1d-143">Perf Veri tooview, düğümlerinden:</span><span class="sxs-lookup"><span data-stu-id="daa1d-143">tooview Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="daa1d-144">Merhaba günlük analizi çalışma alanından hello Azure portal'ı başlatın.</span><span class="sxs-lookup"><span data-stu-id="daa1d-144">Launch hello Log Analytics workspace from hello Azure portal.</span></span>
  <span data-ttu-id="daa1d-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="daa1d-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="daa1d-146">Merhaba soldaki bölmede tooSettings gidin ve veri seçin >> Windows performans sayaçlarını >> "Ekle hello Seçili performans sayaçlarını": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="daa1d-146">Go tooSettings on hello left pane, and select Data >> Windows Performance Counters >> "Add hello selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="daa1d-147">Günlük aramada sorguları toodelve düğümleriniz ilgili ana metriklerini içine aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="daa1d-147">In Log Search, use hello following queries toodelve into key metrics about your nodes:</span></span>

    <span data-ttu-id="daa1d-148">a.</span><span class="sxs-lookup"><span data-stu-id="daa1d-148">a.</span></span> <span data-ttu-id="daa1d-149">Karşılaştırma hangi düğümlerin sorunu yaşıyor hello son bir saat toosee, tüm düğümler arasında ortalama CPU kullanımı hello ve ne zaman aralığında bir ani bir düğüm vardı:</span><span class="sxs-lookup"><span data-stu-id="daa1d-149">Compare hello average CPU Utilization across all your nodes in hello last one hour toosee which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="daa1d-151">b.</span><span class="sxs-lookup"><span data-stu-id="daa1d-151">b.</span></span> <span data-ttu-id="daa1d-152">Bu sorgu ile her bir düğümde kullanılabilir bellek benzer çizgi grafiklerde görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="daa1d-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="daa1d-153">tooview listesini düğümlerinizin her düğüm için kullanılabilir MBayt için hello tam ortalama değer gösteren tüm, bu sorguyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="daa1d-153">tooview a listing of all your nodes, showing hello exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="daa1d-155">c.</span><span class="sxs-lookup"><span data-stu-id="daa1d-155">c.</span></span> <span data-ttu-id="daa1d-156">Hello saatlik ortalama inceleyerek, belirli bir düğümüne toodrill aşağı istediğiniz hello durumda CPU kullanımı, en az, en fazla ve 75-yüzdelik olduğunuz mümkün toodo bunu kullanarak bu sorgu (bilgisayar alanı değiştirin):</span><span class="sxs-lookup"><span data-stu-id="daa1d-156">In hello case that you want toodrill down into a specific node by examining hello hourly average, minimum, maximum and 75-percentile CPU usage, you're able toodo this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="daa1d-158">Günlük analizi performans ölçümlerini hello adresindeki hakkında daha fazla bilgi okumak [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="daa1d-158">Read more information about performance metrics in Log Analytics at hello [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-toolog-analytics"></a><span data-ttu-id="daa1d-159">Varolan bir depolama hesabı tooLog Analytics ekleme</span><span class="sxs-lookup"><span data-stu-id="daa1d-159">Adding an existing storage account tooLog Analytics</span></span>

<span data-ttu-id="daa1d-160">Bu şablon, yalnızca var olan depolama hesapları tooa yeni veya var olan günlük analizi çalışma alanınız ekler.</span><span class="sxs-lookup"><span data-stu-id="daa1d-160">This template simply adds your existing storage accounts tooa new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="daa1d-161">[![TooAzure dağıtma](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="daa1d-161">[![Deploy tooAzure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="daa1d-162">Zaten varolan bir günlük analizi çalışma alanı ile çalışıyorsanız, bir kaynak grubu seçilmesinde "Var olanı kullan" ve arama hello günlük analizi çalışma içeren hello kaynak grubu için seçin.</span><span class="sxs-lookup"><span data-stu-id="daa1d-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for hello resource group containing hello Log Analytics workspace.</span></span> <span data-ttu-id="daa1d-163">Yeni bir olduğunda oluşturacak Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="daa1d-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="daa1d-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="daa1d-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="daa1d-165">Bu şablon dağıtıldıktan sonra mümkün toosee hello depolama hesabı bağlı tooyour günlük analizi çalışma alanı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="daa1d-165">After this template has been deployed, you will be able toosee hello storage account connected tooyour Log Analytics workspace.</span></span> <span data-ttu-id="daa1d-166">Bu örnekte, t ı yukarıda oluşturduğunuz bir daha fazla depolama hesabı toohello Exchange çalışma eklendi.</span><span class="sxs-lookup"><span data-stu-id="daa1d-166">In this instance, I added one more storage account toohello Exchange workspace I created above.</span></span>
<span data-ttu-id="daa1d-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="daa1d-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="daa1d-168">Service Fabric olaylarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="daa1d-168">View Service Fabric events</span></span>

<span data-ttu-id="daa1d-169">Merhaba dağıtımları tamamlanır ve hello Service Fabric çözüm çalışma alanınızda etkinleştirildi sonra hello seçeneğini **Service Fabric** döşeme hello günlük analizi portal toolaunch hello Service Fabric panosunda.</span><span class="sxs-lookup"><span data-stu-id="daa1d-169">Once hello deployments are completed and hello Service Fabric solution has been enabled in your workspace, select hello **Service Fabric** tile in hello Log Analytics portal toolaunch hello Service Fabric dashboard.</span></span> <span data-ttu-id="daa1d-170">Merhaba Pano aşağıdaki tablonun hello hello sütunları içerir.</span><span class="sxs-lookup"><span data-stu-id="daa1d-170">hello dashboard includes hello columns in hello following table.</span></span> <span data-ttu-id="daa1d-171">Her sütun, belirtilen zaman aralığı hello sütunun ölçütlerine sayısı eşleştirerek hello üst 10 olaylarını listeler.</span><span class="sxs-lookup"><span data-stu-id="daa1d-171">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="daa1d-172">Merhaba tüm liste tıklayarak sağlar günlük arama çalıştırabilirsiniz **tümünü görmek** hello sağ alt her sütunun veya hello sütun başlığını tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="daa1d-172">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="daa1d-173">**Service Fabric olay**</span><span class="sxs-lookup"><span data-stu-id="daa1d-173">**Service Fabric event**</span></span> | <span data-ttu-id="daa1d-174">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="daa1d-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="daa1d-175">Önemli sorunlar</span><span class="sxs-lookup"><span data-stu-id="daa1d-175">Notable Issues</span></span> |<span data-ttu-id="daa1d-176">Bir görüntü RunAsyncFailures RunAsynCancellations ve düğüm listeleri gibi sorunların.</span><span class="sxs-lookup"><span data-stu-id="daa1d-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="daa1d-177">İşletimsel olayları</span><span class="sxs-lookup"><span data-stu-id="daa1d-177">Operational Events</span></span> |<span data-ttu-id="daa1d-178">Uygulama yükseltme ve dağıtımları gibi önemli çalışma olaylarını.</span><span class="sxs-lookup"><span data-stu-id="daa1d-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="daa1d-179">Güvenilir hizmeti olayları</span><span class="sxs-lookup"><span data-stu-id="daa1d-179">Reliable Service Events</span></span> |<span data-ttu-id="daa1d-180">Önemli güvenilir hizmeti olayları böyle bir Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="daa1d-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="daa1d-181">Aktör olayları</span><span class="sxs-lookup"><span data-stu-id="daa1d-181">Actor Events</span></span> |<span data-ttu-id="daa1d-182">Aktör yöntemi, aktör etkinleştirmeleri ve deactivations ve benzeri tarafından oluşturulan özel durumları gibi mikro-Hizmetleri tarafından oluşturulan önemli aktör olayları.</span><span class="sxs-lookup"><span data-stu-id="daa1d-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="daa1d-183">Uygulama olayları</span><span class="sxs-lookup"><span data-stu-id="daa1d-183">Application Events</span></span> |<span data-ttu-id="daa1d-184">Uygulamalarınız tarafından oluşturulan tüm özel ETW olayları.</span><span class="sxs-lookup"><span data-stu-id="daa1d-184">All custom ETW events generated by your applications.</span></span> |

![Service Fabric Panosu](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric Panosu](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="daa1d-187">Merhaba aşağıdaki tabloda veri toplama yöntemleri ve verileri için Service Fabric nasıl toplanır ilgili diğer ayrıntıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="daa1d-187">hello following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="daa1d-188">Platform</span><span class="sxs-lookup"><span data-stu-id="daa1d-188">platform</span></span> | <span data-ttu-id="daa1d-189">Doğrudan Aracısı</span><span class="sxs-lookup"><span data-stu-id="daa1d-189">Direct Agent</span></span> | <span data-ttu-id="daa1d-190">Operations Manager Aracısı</span><span class="sxs-lookup"><span data-stu-id="daa1d-190">Operations Manager agent</span></span> | <span data-ttu-id="daa1d-191">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="daa1d-191">Azure Storage</span></span> | <span data-ttu-id="daa1d-192">Operations Manager gerekli?</span><span class="sxs-lookup"><span data-stu-id="daa1d-192">Operations Manager required?</span></span> | <span data-ttu-id="daa1d-193">Operations Manager Aracısı verilerinin yönetim grubu gönderilen</span><span class="sxs-lookup"><span data-stu-id="daa1d-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="daa1d-194">Toplama sıklığı</span><span class="sxs-lookup"><span data-stu-id="daa1d-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="daa1d-195">Windows</span><span class="sxs-lookup"><span data-stu-id="daa1d-195">Windows</span></span> |  |  | <span data-ttu-id="daa1d-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="daa1d-196">&#8226;</span></span> |  |  |<span data-ttu-id="daa1d-197">10 dakika</span><span class="sxs-lookup"><span data-stu-id="daa1d-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="daa1d-198">Tıklayarak bu olayları hello Service Fabric çözüm hello kapsamını değiştirebilirsiniz **verilerini alarak son 7 gün** hello Pano hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="daa1d-198">You can change hello scope of these events in hello Service Fabric solution by clicking **Data based on last 7 days** at hello top of hello dashboard.</span></span> <span data-ttu-id="daa1d-199">Bir gün veya altı saat olmak üzere son yedi gün içinde hello oluşturulan olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="daa1d-199">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="daa1d-200">Ya da seçebilirsiniz **özel** toospecify özel bir tarih aralığı.</span><span class="sxs-lookup"><span data-stu-id="daa1d-200">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="daa1d-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="daa1d-201">Next steps</span></span>

* <span data-ttu-id="daa1d-202">Kullanım [günlük analizi günlük aramalarda](log-analytics-log-searches.md) tooview ayrıntılı Service Fabric olay verileri.</span><span class="sxs-lookup"><span data-stu-id="daa1d-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
