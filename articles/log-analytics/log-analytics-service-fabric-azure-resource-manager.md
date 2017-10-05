---
title: "Günlük analizi Azure portalını kullanarak Service Fabric uygulamaları değerlendirmek | Microsoft Docs"
description: "Service Fabric çözüm risk ve Service Fabric uygulamaları, mikro hizmet, düğümleri ve kümelerini durumunu değerlendirmek için Azure portalını kullanarak günlük analizi kullanabilirsiniz."
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
ms.openlocfilehash: 8c564c0dcbb2f9be286917b2f4d8a40da5406fae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="assess-service-fabric-applications-and-micro-services-with-the-azure-portal"></a><span data-ttu-id="92c2d-103">Service Fabric uygulamaları ve mikro hizmetler Azure portal ile değerlendirin</span><span class="sxs-lookup"><span data-stu-id="92c2d-103">Assess Service Fabric applications and micro-services with the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="92c2d-104">Resource Manager</span><span class="sxs-lookup"><span data-stu-id="92c2d-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="92c2d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="92c2d-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>

![Service Fabric simgesi](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="92c2d-107">Bu makalede, tanımlamak ve, Service Fabric kümesi arasında sorunları gidermeye yardımcı olmak için günlük analizi Service Fabric çözümü kullanmayı açıklar.</span><span class="sxs-lookup"><span data-stu-id="92c2d-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span>

<span data-ttu-id="92c2d-108">Service Fabric çözüm Azure WAD tablolardan bu veriler toplayarak Service Fabric Vm'lerinizi Azure Tanılama verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="92c2d-108">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="92c2d-109">Günlük analizi, Service Fabric framework olaylar dahil olmak üzere, daha sonra okur **güvenilir hizmeti olayları**, **aktör olayları**, **çalışma olaylarını**, ve **özel ETW olayları**.</span><span class="sxs-lookup"><span data-stu-id="92c2d-109">Log Analytics then reads Service Fabric framework events, including **Reliable Service Events**, **Actor Events**, **Operational Events**, and **Custom ETW events**.</span></span> <span data-ttu-id="92c2d-110">Çözüm panosu ile Service Fabric ortamınızda önem düzeyindeki sorunlar ve ilgili olayları görüntülemek kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92c2d-110">With the solution dashboard, you are able to view notable issues and relevant events in your Service Fabric environment.</span></span>

<span data-ttu-id="92c2d-111">Çözüm ile çalışmaya başlamak için bir günlük analizi çalışma alanı, Service Fabric kümesi bağlanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="92c2d-111">To get started with the solution, you need to connect your Service Fabric cluster to a Log Analytics workspace.</span></span> <span data-ttu-id="92c2d-112">Dikkate alınması gereken üç senaryolar verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="92c2d-112">Here are three scenarios to consider:</span></span>

1. <span data-ttu-id="92c2d-113">Service Fabric kümesi dağıtmadıysanız içindeki adımları kullanın ***Service Fabric kümesi günlük analizi çalışma alanına bağlı dağıtma*** yeni bir küme dağıtmak ve günlük analizi raporu yapılandırılması için.</span><span class="sxs-lookup"><span data-stu-id="92c2d-113">If you have not deployed your Service Fabric cluster, use the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace*** to deploy a new cluster and have it configured to report to Log Analytics.</span></span>
2. <span data-ttu-id="92c2d-114">Güvenlik gibi diğer OMS çözümleri, Service Fabric kümesi kullanmak için ana performans sayaçları toplamak gerekiyorsa, adımları ***VM uzantısı ile günlük analizi çalışma alanı bağlı bir Service Fabric kümesi dağıtma yüklü.***</span><span class="sxs-lookup"><span data-stu-id="92c2d-114">If you need to collect performance counters from your hosts to use other OMS solutions such as Security on your Service Fabric Cluster, follow the steps in ***Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.***</span></span>
3. <span data-ttu-id="92c2d-115">Service Fabric kümesi ve günlük Analizi'ne bağlamak istiyorsanız zaten dağıttıysanız, adımları ***var olan bir depolama hesabı için günlük analizi ekleniyor.***</span><span class="sxs-lookup"><span data-stu-id="92c2d-115">If you have already deployed your Service Fabric cluster and want to connect it to Log Analytics, follow the steps in ***Adding an existing storage account to Log Analytics.***</span></span>

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace"></a><span data-ttu-id="92c2d-116">Günlük analizi çalışma alanına bağlı bir Service Fabric kümesi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="92c2d-116">Deploy a Service Fabric Cluster connected to a Log Analytics workspace.</span></span>
<span data-ttu-id="92c2d-117">Bu şablon şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="92c2d-117">This template does the following:</span></span>

1. <span data-ttu-id="92c2d-118">Zaten bir günlük analizi çalışma alanına bağlı bir Azure Service Fabric kümesi dağıtır.</span><span class="sxs-lookup"><span data-stu-id="92c2d-118">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="92c2d-119">Şablon dağıtma sırasında yeni bir çalışma alanı oluşturma seçeneğiniz vardır veya varolan bir günlük analizi çalışma alanı adı girin.</span><span class="sxs-lookup"><span data-stu-id="92c2d-119">You have the option to create a new workspace while deploying the template, or input the name of an already existing Log Analytics workspace.</span></span>
2. <span data-ttu-id="92c2d-120">Tanılama depolama hesabı için günlük analizi çalışma alanına ekler.</span><span class="sxs-lookup"><span data-stu-id="92c2d-120">Adds the diagnostic storage account to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="92c2d-121">Günlük analizi çalışma alanınızdaki Service Fabric çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="92c2d-121">Enables the Service Fabric solution in your Log Analytics workspace.</span></span>

<span data-ttu-id="92c2d-122">[![Azure’a dağıtma](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="92c2d-122">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="92c2d-123">Yukarıdaki Dağıt düğmesi seçtiğinizde, düzenlenecek parametrelerle Azure Portalı'nı açar.</span><span class="sxs-lookup"><span data-stu-id="92c2d-123">Once you select the deploy button above, the Azure portal opens with parameters for you to edit.</span></span> <span data-ttu-id="92c2d-124">Yeni bir günlük analizi çalışma alanı adı girin, yeni bir kaynak grubu oluşturmak emin olun:</span><span class="sxs-lookup"><span data-stu-id="92c2d-124">Be sure to create a new resource group if you input a new Log Analytics workspace name:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/2.png)

![Service Fabric](./media/log-analytics-service-fabric/3.png)

<span data-ttu-id="92c2d-127">Yasal koşulları kabul edin ve tıklatın **oluşturma** dağıtımı başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="92c2d-127">Accept the legal terms and click **Create** to start the deployment.</span></span> <span data-ttu-id="92c2d-128">Dağıtım tamamlandıktan sonra yeni çalışma alanını ve oluşturulan küme ve WADServiceFabric görmelisiniz * eklenen olayı, WADWindowsEventLogs ve WADETWEvent tabloları:</span><span class="sxs-lookup"><span data-stu-id="92c2d-128">Once the deployment is completed, you should see the new workspace and cluster created, and the WADServiceFabric*Event, WADWindowsEventLogs and WADETWEvent tables added:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/4.png)

## <a name="deploy-a-service-fabric-cluster-connected-to-a-log-analytics-workspace-with-vm-extension-installed"></a><span data-ttu-id="92c2d-130">VM uzantısı ile günlük analizi çalışma alanına bağlı bir Service Fabric kümesi dağıtın.</span><span class="sxs-lookup"><span data-stu-id="92c2d-130">Deploy a Service Fabric Cluster connected to a Log Analytics workspace with VM Extension installed.</span></span>

<span data-ttu-id="92c2d-131">Bu şablon şunları yapar:</span><span class="sxs-lookup"><span data-stu-id="92c2d-131">This template does the following:</span></span>

1. <span data-ttu-id="92c2d-132">Zaten bir günlük analizi çalışma alanına bağlı bir Azure Service Fabric kümesi dağıtır.</span><span class="sxs-lookup"><span data-stu-id="92c2d-132">Deploys an Azure Service Fabric cluster already connected to a Log Analytics workspace.</span></span> <span data-ttu-id="92c2d-133">Yeni bir çalışma alanı oluşturun veya var olan bir kullanın.</span><span class="sxs-lookup"><span data-stu-id="92c2d-133">You can create a new workspace or use an existing one.</span></span>
2. <span data-ttu-id="92c2d-134">Tanılama depolama hesapları için günlük analizi çalışma alanına ekler.</span><span class="sxs-lookup"><span data-stu-id="92c2d-134">Adds the diagnostic storage accounts to the Log Analytics workspace.</span></span>
3. <span data-ttu-id="92c2d-135">Günlük analizi çalışma alanındaki Service Fabric çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="92c2d-135">Enables the Service Fabric solution in the Log Analytics workspace.</span></span>
4. <span data-ttu-id="92c2d-136">Service Fabric kümesi her sanal makine ölçek MMA Aracı Uzantısı yükler.</span><span class="sxs-lookup"><span data-stu-id="92c2d-136">Installs the MMA agent extension in each virtual machine scale set in your Service Fabric cluster.</span></span> <span data-ttu-id="92c2d-137">MMA aracı yüklü olan düğümleriniz ilgili performans ölçümleri görüntüleyebilir.</span><span class="sxs-lookup"><span data-stu-id="92c2d-137">With the MMA agent installed, you are able to view performance metrics about your nodes.</span></span>

<span data-ttu-id="92c2d-138">[![Azure’a dağıtma](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="92c2d-138">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fazure%2Fazure-quickstart-templates%2Fmaster%2Fservice-fabric-vmss-oms%2F%2Fazuredeploy.json)</span></span>

<span data-ttu-id="92c2d-139">Yukarıdaki aynı adımları, aşağıdaki giriş gerekli parametreleri ve dağıtımı devre dışı tetiklersiniz.</span><span class="sxs-lookup"><span data-stu-id="92c2d-139">Following the same steps above, input the necessary parameters, and kick off a deployment.</span></span> <span data-ttu-id="92c2d-140">Bir kez daha yeni bir çalışma alanı, küme ve WAD tablolar tüm oluşturulan görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="92c2d-140">Once again you should see the new workspace, cluster and WAD tables all created:</span></span>

![Service Fabric](./media/log-analytics-service-fabric/5.png)

### <a name="viewing-performance-data"></a><span data-ttu-id="92c2d-142">Performans verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="92c2d-142">Viewing Performance Data</span></span>

<span data-ttu-id="92c2d-143">Performans verileri, düğümlerden görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="92c2d-143">To view Perf Data from your nodes:</span></span>


[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

- <span data-ttu-id="92c2d-144">Azure portalından günlük analizi çalışma alanı başlatın.</span><span class="sxs-lookup"><span data-stu-id="92c2d-144">Launch the Log Analytics workspace from the Azure portal.</span></span>
  <span data-ttu-id="92c2d-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span><span class="sxs-lookup"><span data-stu-id="92c2d-145">![Service Fabric](./media/log-analytics-service-fabric/6.png)</span></span>
- <span data-ttu-id="92c2d-146">Sol bölmede ayarlarınıza gidin ve verileri seçin >> Windows performans sayaçlarını >> "Seçili performans sayaçlarını Ekle": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span><span class="sxs-lookup"><span data-stu-id="92c2d-146">Go to Settings on the left pane, and select Data >> Windows Performance Counters >> "Add the selected performance counters": ![Service Fabric](./media/log-analytics-service-fabric/7.png)</span></span>
- <span data-ttu-id="92c2d-147">Günlük aramada aşağıdaki sorguları düğümleriniz ilgili ana metriklerini içine inceleyin için kullanın:</span><span class="sxs-lookup"><span data-stu-id="92c2d-147">In Log Search, use the following queries to delve into key metrics about your nodes:</span></span>

    <span data-ttu-id="92c2d-148">a.</span><span class="sxs-lookup"><span data-stu-id="92c2d-148">a.</span></span> <span data-ttu-id="92c2d-149">Ortalama CPU kullanımı tüm düğümleri arasında hangi düğümlerin sorunu yaşıyor ve ne zaman aralığında bir ani bir düğümün sahip görmek için son bir saat içinde karşılaştırın:</span><span class="sxs-lookup"><span data-stu-id="92c2d-149">Compare the average CPU Utilization across all your nodes in the last one hour to see which nodes are having issues and at what time interval a node had a spike:</span></span>

    ```
    Type=Perf ObjectName=Processor CounterName="% Processor Time"|measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/10.png)

    <span data-ttu-id="92c2d-151">b.</span><span class="sxs-lookup"><span data-stu-id="92c2d-151">b.</span></span> <span data-ttu-id="92c2d-152">Bu sorgu ile her bir düğümde kullanılabilir bellek benzer çizgi grafiklerde görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="92c2d-152">View similar line charts for available memory on each node with this query:</span></span>

    ```
    Type=Perf ObjectName=Memory CounterName="Available MBytes Memory" | measure avg(CounterValue) by Computer Interval 1HOUR.
    ```

    <span data-ttu-id="92c2d-153">Her düğüm için kullanılabilir MBayt için tam ortalama değer gösteren tüm düğümleriniz, listesini görüntülemek için bu sorguyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="92c2d-153">To view a listing of all your nodes, showing the exact average value for Available MBytes for each node, use this query:</span></span>

    ```
    Type=Perf (ObjectName=Memory) (CounterName="Available MBytes") | measure avg(CounterValue) by Computer
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/11.png)

    <span data-ttu-id="92c2d-155">c.</span><span class="sxs-lookup"><span data-stu-id="92c2d-155">c.</span></span> <span data-ttu-id="92c2d-156">Belirli bir düğümüne saatlik ortalama, en az, en fazla ve 75-yüzdelik CPU kullanımı inceleyerek detaya istediğiniz durumda da, bu sorgu (Değiştir bilgisayar alanı) kullanarak bunu yapabilir:</span><span class="sxs-lookup"><span data-stu-id="92c2d-156">In the case that you want to drill down into a specific node by examining the hourly average, minimum, maximum and 75-percentile CPU usage, you're able to do this by using this query (replace Computer field):</span></span>

    ```
    Type=Perf CounterName="% Processor Time" InstanceName=_Total Computer="BaconDC01.BaconLand.com"| measure min(CounterValue), avg(CounterValue), percentile75(CounterValue), max(CounterValue) by Computer Interval 1HOUR
    ```

    ![Service Fabric](./media/log-analytics-service-fabric/12.png)

<span data-ttu-id="92c2d-158">Günlük analizi performans ölçümlerini hakkında daha fazla bilgi okumak [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span><span class="sxs-lookup"><span data-stu-id="92c2d-158">Read more information about performance metrics in Log Analytics at the [Operations Management Suite blog](https://blogs.technet.microsoft.com/msoms/tag/metrics/).</span></span>


## <a name="adding-an-existing-storage-account-to-log-analytics"></a><span data-ttu-id="92c2d-159">Günlük analizi için mevcut bir depolama hesabını ekleme</span><span class="sxs-lookup"><span data-stu-id="92c2d-159">Adding an existing storage account to Log Analytics</span></span>

<span data-ttu-id="92c2d-160">Bu şablon, yalnızca yeni veya var olan günlük analizi çalışma alanına var olan depolama hesaplarınızı ekler.</span><span class="sxs-lookup"><span data-stu-id="92c2d-160">This template simply adds your existing storage accounts to a new or existing Log Analytics workspace.</span></span>

<span data-ttu-id="92c2d-161">[![Azure’a dağıtma](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="92c2d-161">[![Deploy to Azure](./media/log-analytics-service-fabric/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Foms-existing-storage-account%2Fazuredeploy.json)</span></span>

> [!NOTE]
> <span data-ttu-id="92c2d-162">Zaten varolan bir günlük analizi çalışma alanı ile çalışıyorsanız, bir kaynak grubu seçilmesinde "Var olanı kullan" ve aramak için günlük analizi çalışma alanı içeren kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="92c2d-162">In selecting a Resource Group, if you're working with an already existing Log Analytics workspace, select "Use Existing" and search for the resource group containing the Log Analytics workspace.</span></span> <span data-ttu-id="92c2d-163">Yeni bir olduğunda oluşturacak Aksi takdirde.</span><span class="sxs-lookup"><span data-stu-id="92c2d-163">Create a new one if otherwise.</span></span>
> <span data-ttu-id="92c2d-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span><span class="sxs-lookup"><span data-stu-id="92c2d-164">![Service Fabric](./media/log-analytics-service-fabric/8.png)</span></span>
>
>

<span data-ttu-id="92c2d-165">Bu şablon dağıtıldıktan sonra günlük analizi çalışma alanına bağlı depolama hesabı görmeye olacaktır.</span><span class="sxs-lookup"><span data-stu-id="92c2d-165">After this template has been deployed, you will be able to see the storage account connected to your Log Analytics workspace.</span></span> <span data-ttu-id="92c2d-166">Bu örnekte, bir daha fazla depolama hesabı ı yukarıda oluşturduğunuz Exchange çalışma alanına ekledim.</span><span class="sxs-lookup"><span data-stu-id="92c2d-166">In this instance, I added one more storage account to the Exchange workspace I created above.</span></span>
<span data-ttu-id="92c2d-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span><span class="sxs-lookup"><span data-stu-id="92c2d-167">![Service Fabric](./media/log-analytics-service-fabric/9.png)</span></span>

## <a name="view-service-fabric-events"></a><span data-ttu-id="92c2d-168">Service Fabric olaylarını görüntüle</span><span class="sxs-lookup"><span data-stu-id="92c2d-168">View Service Fabric events</span></span>

<span data-ttu-id="92c2d-169">Dağıtımları tamamlandı ve Service Fabric çözüm çalışma alanınızda etkinleştirildikten sonra seçeneğini **Service Fabric** döşeme Service Fabric panosunu başlatma için günlük analizi portalında.</span><span class="sxs-lookup"><span data-stu-id="92c2d-169">Once the deployments are completed and the Service Fabric solution has been enabled in your workspace, select the **Service Fabric** tile in the Log Analytics portal to launch the Service Fabric dashboard.</span></span> <span data-ttu-id="92c2d-170">Pano aşağıdaki tabloda gösterilen sütunları içerir.</span><span class="sxs-lookup"><span data-stu-id="92c2d-170">The dashboard includes the columns in the following table.</span></span> <span data-ttu-id="92c2d-171">Her bir sütunun üst 10 olayları belirtilen zaman aralığına ilişkin bu sütunun ölçütlerle eşleşen sayısına göre listeler.</span><span class="sxs-lookup"><span data-stu-id="92c2d-171">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="92c2d-172">Listenin tamamını tıklayarak sağlayan bir günlük arama çalıştırabilirsiniz **tümünü görmek** sağ alt her sütunun veya sütun başlığını tıklatarak.</span><span class="sxs-lookup"><span data-stu-id="92c2d-172">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="92c2d-173">**Service Fabric olay**</span><span class="sxs-lookup"><span data-stu-id="92c2d-173">**Service Fabric event**</span></span> | <span data-ttu-id="92c2d-174">**Açıklama**</span><span class="sxs-lookup"><span data-stu-id="92c2d-174">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="92c2d-175">Önemli sorunlar</span><span class="sxs-lookup"><span data-stu-id="92c2d-175">Notable Issues</span></span> |<span data-ttu-id="92c2d-176">Bir görüntü RunAsyncFailures RunAsynCancellations ve düğüm listeleri gibi sorunların.</span><span class="sxs-lookup"><span data-stu-id="92c2d-176">A Display of issues such as RunAsyncFailures RunAsynCancellations and Node Downs.</span></span> |
| <span data-ttu-id="92c2d-177">İşletimsel olayları</span><span class="sxs-lookup"><span data-stu-id="92c2d-177">Operational Events</span></span> |<span data-ttu-id="92c2d-178">Uygulama yükseltme ve dağıtımları gibi önemli çalışma olaylarını.</span><span class="sxs-lookup"><span data-stu-id="92c2d-178">Notable operational events such as application upgrade and deployments.</span></span> |
| <span data-ttu-id="92c2d-179">Güvenilir hizmeti olayları</span><span class="sxs-lookup"><span data-stu-id="92c2d-179">Reliable Service Events</span></span> |<span data-ttu-id="92c2d-180">Önemli güvenilir hizmeti olayları böyle bir Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="92c2d-180">Notable reliable service events such a Runasyncinvocations.</span></span> |
| <span data-ttu-id="92c2d-181">Aktör olayları</span><span class="sxs-lookup"><span data-stu-id="92c2d-181">Actor Events</span></span> |<span data-ttu-id="92c2d-182">Aktör yöntemi, aktör etkinleştirmeleri ve deactivations ve benzeri tarafından oluşturulan özel durumları gibi mikro-Hizmetleri tarafından oluşturulan önemli aktör olayları.</span><span class="sxs-lookup"><span data-stu-id="92c2d-182">Notable actor events generated by your micro-services, such as exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="92c2d-183">Uygulama olayları</span><span class="sxs-lookup"><span data-stu-id="92c2d-183">Application Events</span></span> |<span data-ttu-id="92c2d-184">Uygulamalarınız tarafından oluşturulan tüm özel ETW olayları.</span><span class="sxs-lookup"><span data-stu-id="92c2d-184">All custom ETW events generated by your applications.</span></span> |

![Service Fabric Panosu](./media/log-analytics-service-fabric/sf3.png)

![Service Fabric Panosu](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="92c2d-187">Aşağıdaki tabloda, veri toplama yöntemleri ve verileri için Service Fabric nasıl toplanır ilgili diğer ayrıntıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="92c2d-187">The following table shows data collection methods and other details about how data is collected for Service Fabric.</span></span>

| <span data-ttu-id="92c2d-188">Platform</span><span class="sxs-lookup"><span data-stu-id="92c2d-188">platform</span></span> | <span data-ttu-id="92c2d-189">Doğrudan Aracısı</span><span class="sxs-lookup"><span data-stu-id="92c2d-189">Direct Agent</span></span> | <span data-ttu-id="92c2d-190">Operations Manager Aracısı</span><span class="sxs-lookup"><span data-stu-id="92c2d-190">Operations Manager agent</span></span> | <span data-ttu-id="92c2d-191">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="92c2d-191">Azure Storage</span></span> | <span data-ttu-id="92c2d-192">Operations Manager gerekli?</span><span class="sxs-lookup"><span data-stu-id="92c2d-192">Operations Manager required?</span></span> | <span data-ttu-id="92c2d-193">Operations Manager Aracısı verilerinin yönetim grubu gönderilen</span><span class="sxs-lookup"><span data-stu-id="92c2d-193">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="92c2d-194">Toplama sıklığı</span><span class="sxs-lookup"><span data-stu-id="92c2d-194">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="92c2d-195">Windows</span><span class="sxs-lookup"><span data-stu-id="92c2d-195">Windows</span></span> |  |  | <span data-ttu-id="92c2d-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="92c2d-196">&#8226;</span></span> |  |  |<span data-ttu-id="92c2d-197">10 dakika</span><span class="sxs-lookup"><span data-stu-id="92c2d-197">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="92c2d-198">Bu olaylar Service Fabric çözümde kapsamını tıklatarak değiştirebilirsiniz **verilerini alarak son 7 gün** Pano üstündeki.</span><span class="sxs-lookup"><span data-stu-id="92c2d-198">You can change the scope of these events in the Service Fabric solution by clicking **Data based on last 7 days** at the top of the dashboard.</span></span> <span data-ttu-id="92c2d-199">Son yedi gün içinde bir gün veya altı saat oluşturulan olayları gösterir.</span><span class="sxs-lookup"><span data-stu-id="92c2d-199">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="92c2d-200">Ya da seçebilirsiniz **özel** özel bir tarih aralığı belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="92c2d-200">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="92c2d-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="92c2d-201">Next steps</span></span>

* <span data-ttu-id="92c2d-202">Kullanım [günlük analizi günlük aramalarda](log-analytics-log-searches.md) ayrıntılı Service Fabric olay verilerini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="92c2d-202">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
