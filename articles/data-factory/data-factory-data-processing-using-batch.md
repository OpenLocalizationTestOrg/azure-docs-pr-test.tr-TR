---
title: "Veri Fabrikası ve toplu işlemi kullanarak büyük ölçekli veri kümeleri işlem | Microsoft Docs"
description: "Azure Batch paralel işleme yeteneğini kullanarak büyük miktarlarda bir Azure Data Factory işlem hattı verileri işlemek açıklar."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 9defbf7a6a515740fa3b3cb1c67a2f5f9d9baa01
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="7d3eb-103">Data Factory ve Batch kullanarak büyük ölçekli veri kümelerini işleme</span><span class="sxs-lookup"><span data-stu-id="7d3eb-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="7d3eb-104">Bu makalede bir taşır ve büyük ölçekli veri kümeleri otomatik ve zamanlanmış bir şekilde işleyen örnek bir çözüm mimarisini açıklar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="7d3eb-105">Ayrıca, Azure Data Factory ile Azure Batch çözümü uygulamak için bir uçtan uca izlenecek yol da sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-105">It also provides an end-to-end walkthrough to implement the solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="7d3eb-106">Bu makalede bizim tipik makale uzun çünkü tüm örnek çözümünü bir kılavuz içerir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="7d3eb-107">Bu hizmetler hakkında bilgi edinebilirsiniz Batch ve Data Factory, yeni varsa ve nasıl birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-107">If you are new to Batch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="7d3eb-108">Hizmetler hakkında bir şey bilmeniz ve tasarlama/çözüm mimarisi oluşturma, yalnızca üzerinde odaklanmanıza [mimarisi bölümüne](#architecture-of-sample-solution) makalenin ve prototip ya da bir çözüm geliştiriyorsanız, ayrıca denemek isteyebilirsiniz adım adım yönergeleri [izlenecek](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-108">If you know something about the services and are designing/architecting a solution, you may focus just on the [architecture section](#architecture-of-sample-solution) of the article and if you are developing a prototype or a solution, you may also want to try out step-by-step instructions in the [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="7d3eb-109">Bu içerik ve bunu nasıl kullandığı hakkında yorumlarınızı davet ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="7d3eb-110">İlk olarak, nasıl veri fabrikası ve toplu işlem Hizmetleri ile büyük veri kümelerini bulutta işleme yardımcı olabilir bakalım.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in the cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="7d3eb-111">Neden Azure toplu işlem?</span><span class="sxs-lookup"><span data-stu-id="7d3eb-111">Why Azure Batch?</span></span>
<span data-ttu-id="7d3eb-112">Azure Batch, büyük ölçekli paralel ve yüksek performanslı bilgi işlem (HPC) uygulamalarını bulutta verimli bir şekilde çalıştırmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-112">Azure Batch enables you to run large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="7d3eb-113">Yönetilen sanal makineler koleksiyonunda çalıştırılacak işlem yoğunluklu işi zamanlayan ve işinizin gereksinimlerini karşılayacak işlem kaynakların otomatik olarak ölçekleyebilen bir platform hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-113">It's a platform service that schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="7d3eb-114">Batch hizmetiyle, uygulamalarınızı paralel olarak ve ölçekte yürütmek için Azure işlem kaynaklarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-114">With the Batch service, you define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="7d3eb-115">İsteğe bağlı veya zamanlanmış işlerinizi çalıştırabilirsiniz; HPC kümesi, tek tek sanal makineler, sanal ağlar veya karmaşık iş ve görev zamanlama altyapısını el ile oluşturmanız, yapılandırmanız ve yönetmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-115">You can run on-demand or scheduled jobs, and you don't need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="7d3eb-116">Bu makalede açıklanan çözüm mimarisi/uyarlamasını anlamaya yardımcı olması gibi Azure Batch ile bilmiyorsanız aşağıdaki makalelere bakın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-116">See the following articles if you are not familiar with Azure Batch as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>   

* [<span data-ttu-id="7d3eb-117">Azure Batch temel bilgileri</span><span class="sxs-lookup"><span data-stu-id="7d3eb-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="7d3eb-118">Batch özelliklerine genel bakış</span><span class="sxs-lookup"><span data-stu-id="7d3eb-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="7d3eb-119">(isteğe bağlı) Azure Batch hakkında daha fazla bilgi için bkz: [için Azure Batch öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-119">(optional) To learn more about Azure Batch, see the [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="7d3eb-120">Neden Azure Data Factory?</span><span class="sxs-lookup"><span data-stu-id="7d3eb-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="7d3eb-121">Data Factory, verilerin taşınmasını ve dönüştürülmesini düzenleyen ve otomatikleştiren bulut tabanlı bir veri tümleştirme hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-121">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="7d3eb-122">Data Factory hizmeti kullanıldığında, şirket içi veri taşıma ve bulut merkezi veri deposuna veri depolarına yönetilen veri ardışık oluşturabilirsiniz (örneğin: Azure Blob Storage) ve işlem/dönüştürme Azure Hdınsight ve Azure gibi hizmetleri kullanarak verileri Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-122">Using the Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores to a centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="7d3eb-123">Veri ardışık zamanlanmış şekilde (saatlik, günlük, haftalık, vb.) ve İzleyicisi'nde çalıştırın ve sorunları belirlemek ve eylem için bir bakışta yönetmek için de zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-123">You can also schedule data pipelines to run in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance to identify issues and take action.</span></span>

<span data-ttu-id="7d3eb-124">Bu makalede açıklanan çözüm mimarisi/uyarlamasını anlamaya yardımcı olması gibi Azure Data Factory ile bilmiyorsanız aşağıdaki makalelere bakın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-124">See the following articles if you are not familiar with Azure Data Factory as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>  

* [<span data-ttu-id="7d3eb-125">Azure Data Factory giriş</span><span class="sxs-lookup"><span data-stu-id="7d3eb-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="7d3eb-126">İlk veri hattınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="7d3eb-127">(isteğe bağlı) Azure Data Factory hakkında daha fazla bilgi için bkz: [Azure Data Factory öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-127">(optional) To learn more about Azure Data Factory, see the [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="7d3eb-128">Veri Fabrikası ve birlikte toplu işlem</span><span class="sxs-lookup"><span data-stu-id="7d3eb-128">Data Factory and Batch together</span></span>
<span data-ttu-id="7d3eb-129">Veri Fabrikası hedef veri deposu kaynak veri deposuna ve Hive etkinliği Azure üzerinde Hadoop kümeleri (Hdınsight) kullanarak verileri işlemek için copy/move veri kopyalama etkinliği gibi yerleşik etkinlikler içerir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-129">Data Factory includes built-in activities such as Copy Activity to copy/move data from a source data store to a destination data store and Hive Activity to process data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="7d3eb-130">Bkz: [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) desteklenen dönüştürme etkinliklerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="7d3eb-131">Ayrıca, taşımak veya kendi mantığı ile verileri işlemek ve bu etkinlikler Azure Hdınsight kümesinde veya bir Azure Batch havuzunda VM'lerin çalıştırmak için özel .NET etkinlikler oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-131">It also allows you to create custom .NET activities to move or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="7d3eb-132">Azure Batch kullandığınızda otomatik ölçek havuzuna yapılandırabilirsiniz (ekleme veya iş yüküne göre sanal makineleri kaldırın) sağladığınız bir formüle dayanarak.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-132">When you use Azure Batch, you can configure the pool to auto-scale (add or remove VMs based on the workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="7d3eb-133">Örnek çözümü mimarisi</span><span class="sxs-lookup"><span data-stu-id="7d3eb-133">Architecture of sample solution</span></span>
<span data-ttu-id="7d3eb-134">Bu makalede açıklanan mimarisi için basit bir çözüm olsa da, finansal hizmetler, görüntü işleme ve işleme ve genomic analiz tarafından modelleme risk gibi karmaşık senaryolar için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-134">Even though the architecture described in this article is for a simple solution, it is relevant to complex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="7d3eb-135">Aşağıdaki diyagramda, 1) nasıl Data Factory veri hareketlerini ve işleme düzenleyen ve Azure Batch verileri paralel bir biçimde 2) nasıl işlediği açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-135">The diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes the data in a parallel manner.</span></span> <span data-ttu-id="7d3eb-136">Karşıdan yükle ve kolay başvuru (11 x 17 inç. diyagramı yazdırma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-136">Download and print the diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="7d3eb-137">veya A3 boyutu): [Azure Batch ve Data Factory kullanarak HPC ve veriler orchestration](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="7d3eb-138">[![Büyük ölçekli veri işleme diyagramı](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="7d3eb-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="7d3eb-139">Aşağıdaki listede işleminin temel adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-139">The following list provides the basic steps of the process.</span></span> <span data-ttu-id="7d3eb-140">Çözüm, kod ve uçtan uca çözümü oluşturmak için açıklamalar içerir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-140">The solution includes code and explanations to build the end-to-end solution.</span></span>

1. <span data-ttu-id="7d3eb-141">**Azure Batch (VM'ler) işlem düğümlerinin bir havuzuyla yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="7d3eb-142">Düğüm sayısını ve her düğümün boyutu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-142">You can specify the number of nodes and size of each node.</span></span>
2. <span data-ttu-id="7d3eb-143">**Azure Data Factory örneğini oluşturabilir** Azure blob depolama, Azure toplu işlem hizmeti, girdi/çıktı verilerini ve iş akışı/ardışık taşıyın ve veri dönüştürme etkinlikleri ile temsil eden varlık ile yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="7d3eb-144">**Özel bir .NET etkinliği içinde Data Factory işlem hattı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-144">**Create a custom .NET activity in the Data Factory pipeline**.</span></span> <span data-ttu-id="7d3eb-145">Azure Batch havuzunda çalıştıran kullanıcı kodunuzu etkinliktir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-145">The activity is your user code that runs on the Azure Batch pool.</span></span>
4. <span data-ttu-id="7d3eb-146">**Azure depolama alanında bloblar büyük miktarlarda giriş veri depolamak**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="7d3eb-147">Veriler (genellikle zamanına göre) mantıksal dilimlere bölünür.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="7d3eb-148">**Veri Fabrikası paralel olarak işlenir verileri kopyalar** ikincil konuma.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-148">**Data Factory copies data that is processed in parallel** to the secondary location.</span></span>
6. <span data-ttu-id="7d3eb-149">**Veri Fabrikası çalışan toplu işi tarafından ayrılan havuzunu kullanan özel etkinlik**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-149">**Data Factory runs the custom activity using the pool allocated by Batch**.</span></span> <span data-ttu-id="7d3eb-150">Veri Fabrikası etkinlikleri birlikte çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="7d3eb-151">Her etkinlik veri dilimini işler.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="7d3eb-152">Sonuçları Azure depolama alanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-152">The results are stored in Azure storage.</span></span>
7. <span data-ttu-id="7d3eb-153">**Veri Fabrikası son sonuçları üçüncü bir konuma taşır**, bir uygulama aracılığıyla dağıtım için veya diğer araçları tarafından işlenmesi için.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-153">**Data Factory moves the final results to a third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="7d3eb-154">Örnek çözümü uygulaması</span><span class="sxs-lookup"><span data-stu-id="7d3eb-154">Implementation of sample solution</span></span>
<span data-ttu-id="7d3eb-155">Örnek çözümü kasıtlı olarak basit bir işlemdir ve Data Factory ve toplu birlikte veri kümeleri işlemek için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-155">The sample solution is intentionally simple and is to show you how to use Data Factory and Batch together to process datasets.</span></span> <span data-ttu-id="7d3eb-156">Çözüm yalnızca bir arama terimi ("Microsoft") oluşumu bir zaman serisinin düzenlenmiş giriş dosyalarında sayar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-156">The solution simply counts the number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="7d3eb-157">Çıkış dosyaları için sayısı çıkarır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-157">It outputs the count to output files.</span></span>

<span data-ttu-id="7d3eb-158">**Zaman**: Azure Data Factory ve Batch temelleri ile tanıdık ve aşağıda listelenen önkoşulları tamamladığınızdan varsa, bu çözüm tamamlanması 1-2 saat sürer tahmin ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed the prerequisites listed below, we estimate this solution takes 1-2 hours to complete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="7d3eb-159">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7d3eb-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="7d3eb-160">Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="7d3eb-160">Azure subscription</span></span>
<span data-ttu-id="7d3eb-161">Bir Azure aboneliğiniz yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7d3eb-162">Bkz: [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="7d3eb-163">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="7d3eb-163">Azure storage account</span></span>
<span data-ttu-id="7d3eb-164">Bu öğreticide verileri depolamak için bir Azure depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-164">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="7d3eb-165">Bir Azure depolama hesabınız yoksa bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="7d3eb-166">Örnek çözümü blob depolama kullanır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-166">The sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="7d3eb-167">Azure toplu işlem hesabı</span><span class="sxs-lookup"><span data-stu-id="7d3eb-167">Azure Batch account</span></span>
<span data-ttu-id="7d3eb-168">Bir Azure Batch hesabı kullanarak oluşturduğunuz [Azure portal](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-168">Create an Azure Batch account using the [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="7d3eb-169">Bkz: [oluşturma ve bir Azure Batch hesabını yönetmek](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="7d3eb-170">Azure Batch hesabı adını ve hesap anahtarını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-170">Note the Azure Batch account name and account key.</span></span> <span data-ttu-id="7d3eb-171">Aynı zamanda [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) bir Azure Batch hesabı oluşturmak için cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet to create an Azure Batch account.</span></span> <span data-ttu-id="7d3eb-172">Bkz: [Azure Batch PowerShell cmdlet'leri kullanmaya başlama](../batch/batch-powershell-cmdlets-get-started.md) bu cmdlet'in kullanımı hakkında ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="7d3eb-173">Örnek çözümü (üzerinden dolaylı olarak bir Azure Data Factory işlem hattı) Azure Batch havuzunda işlem düğümlerinin (sanal makineler yönetilen koleksiyonu) paralel şekilde veri işlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-173">The sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) to process data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="7d3eb-174">Azure Batch havuzundaki sanal makineler (VM'ler)</span><span class="sxs-lookup"><span data-stu-id="7d3eb-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="7d3eb-175">Oluşturma bir **Azure Batch havuzu** en az 2 ile işlem düğümleri.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="7d3eb-176">İçinde [Azure portal](https://portal.azure.com), tıklatın **Gözat** sol menüsüne ve ardından içinde **toplu işlem hesaplarını**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-176">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="7d3eb-177">Açmak için Azure Batch hesabınızı seçin **toplu işlem hesabı** dikey.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-177">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
3. <span data-ttu-id="7d3eb-178">Tıklatın **havuzları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="7d3eb-179">İçinde **havuzları** dikey penceresinde, araç çubuğunda bir havuzu eklemek için Ekle düğmesini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-179">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
   1. <span data-ttu-id="7d3eb-180">Havuzu için bir kimlik girin (**havuzu kimliği**).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-180">Enter an ID for the pool (**Pool ID**).</span></span> <span data-ttu-id="7d3eb-181">Not **havuzun kimliği**; Data Factory çözüm oluşturulurken gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-181">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
   2. <span data-ttu-id="7d3eb-182">Belirtin **Windows Server 2012 R2** işletim sistemi ailesi ayarı için.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-182">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
   3. <span data-ttu-id="7d3eb-183">Seçin bir **düğüm fiyatlandırma katmanı**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="7d3eb-184">Girin **2** olarak değer **hedef ayrılmış** ayarı.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-184">Enter **2** as value for the **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="7d3eb-185">Girin **2** olarak değer **en fazla düğüm başına görevleri** ayarı.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-185">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="7d3eb-186">Havuzu oluşturmak için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-186">Click **OK** to create the pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="7d3eb-187">Azure Depolama Gezgini</span><span class="sxs-lookup"><span data-stu-id="7d3eb-187">Azure Storage Explorer</span></span>
<span data-ttu-id="7d3eb-188">[Azure Depolama Gezgini 6 (aracı)](https://azurestorageexplorer.codeplex.com/) veya [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (ClumsyLeaf yazılımından).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="7d3eb-189">İnceleme veya bulutta barındırılan uygulamalarınızı günlükleri de dahil olmak üzere Azure Storage projelerinizi verileri değiştirme için bu araçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-189">You use these tools for inspecting and altering the data in your Azure Storage projects including the logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="7d3eb-190">Adlı bir kapsayıcı oluşturmak **mycontainer** özel erişim (anonim erişimi yok)</span><span class="sxs-lookup"><span data-stu-id="7d3eb-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="7d3eb-191">Kullanıyorsanız **CloudXplorer**, klasörler ve alt klasörler ile aşağıdaki yapısını oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-191">If you are using **CloudXplorer**, create folders and subfolders with the following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="7d3eb-192">`Inputfolder`ve `outputfolder` en üst düzey klasörlerde bulunan `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="7d3eb-193">`inputfolder` Tarih-saat Damgalar (YYYY-AA-GG-ss) ile klasörleri varsa.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-193">The `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="7d3eb-194">Kullanıyorsanız **Azure Storage Gezgini**, sonraki adımda adlara sahip dosyaları karşıya yüklemek gerekir: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-194">If you are using **Azure Storage Explorer**, in the next step, you need to upload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="7d3eb-195">Bu adım, klasörleri otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-195">This step automatically creates the folders.</span></span>
3. <span data-ttu-id="7d3eb-196">Bir metin dosyası oluşturun **dosya.txt'yi** anahtar sözcüğü sahip içerikle makinenizde **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-196">Create a text file **file.txt** on your machine with content that has the keyword **Microsoft**.</span></span> <span data-ttu-id="7d3eb-197">Örneğin: "Özel Etkinlik Microsoft test özel etkinlik Microsoft test".</span><span class="sxs-lookup"><span data-stu-id="7d3eb-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="7d3eb-198">Azure blob depolama alanındaki aşağıdaki giriş klasörlere dosyası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-198">Upload the file to the following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="7d3eb-199">Kullanıyorsanız **Azure Storage Gezgini**, dosyayı karşıya yüklemeyi **dosya.txt'yi** için **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-199">If you are using **Azure Storage Explorer**, upload the file **file.txt** to **mycontainer**.</span></span> <span data-ttu-id="7d3eb-200">Tıklatın **kopyalama** blob bir kopyasını oluşturmak için araç çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-200">Click **Copy** on the toolbar to create a copy of the blob.</span></span> <span data-ttu-id="7d3eb-201">İçinde **kopyalama Blob** iletişim kutusu, değişiklik **hedef blob adı** için `inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-201">In the **Copy Blob** dialog box, change the **destination blob name** to `inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="7d3eb-202">Oluşturmak için bu adımı yineleyin `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-202">Repeat this step to create `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="7d3eb-203">Bu eylem, klasörleri otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-203">This action automatically creates the folders.</span></span>
5. <span data-ttu-id="7d3eb-204">Adlı başka bir kapsayıcı oluşturma: `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="7d3eb-205">Bu kapsayıcıya özel etkinlik zip dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-205">You upload the custom activity zip file to this container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="7d3eb-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7d3eb-206">Visual Studio</span></span>
<span data-ttu-id="7d3eb-207">Veri Fabrikası çözümde kullanılacak özel toplu iş etkinliği oluşturmak için Microsoft Visual Studio 2012 veya sonraki sürümünü yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-207">Install Microsoft Visual Studio 2012 or later to create the custom Batch activity to be used in the Data Factory solution.</span></span>

### <a name="high-level-steps-to-create-the-solution"></a><span data-ttu-id="7d3eb-208">Çözüm oluşturmak için üst düzey adımlar</span><span class="sxs-lookup"><span data-stu-id="7d3eb-208">High-level steps to create the solution</span></span>
1. <span data-ttu-id="7d3eb-209">Veri işleme mantığı içeren özel bir aktivite oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-209">Create a custom activity that contains the data processing logic.</span></span>
2. <span data-ttu-id="7d3eb-210">Özel Etkinlik kullanan bir Azure data factory oluşturun:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-210">Create an Azure data factory that uses the custom activity:</span></span>

### <a name="create-the-custom-activity"></a><span data-ttu-id="7d3eb-211">Özel etkinlik oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-211">Create the custom activity</span></span>
<span data-ttu-id="7d3eb-212">Veri Fabrikası özel Bu örnek çözümü Kalp etkinliktir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-212">The Data Factory custom activity is the heart of this sample solution.</span></span> <span data-ttu-id="7d3eb-213">Örnek çözümü Özel Etkinlik çalıştırmak için Azure Batch kullanır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-213">The sample solution uses Azure Batch to run the custom activity.</span></span> <span data-ttu-id="7d3eb-214">Bkz: [bir Azure Data Factory ardışık düzeninde özel etkinlikleri kullanmak](data-factory-use-custom-activities.md) özel etkinlikler geliştirmek ve bunları Azure Data Factory ardışık düzenlerinde temel bilgi.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for the basic information to develop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="7d3eb-215">Oluşturmanıza gerek bir Azure Data Factory ardışık düzeninde kullanabileceğiniz bir .NET özel etkinlik oluşturmak için bir **.NET sınıf kitaplığı** uygulayan bir sınıf projeyle **IDotNetActivity** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-215">To create a .NET custom activity that you can use in an Azure Data Factory pipeline, you need to create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="7d3eb-216">Bu arabirim yalnızca bir yöntemi vardır: **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="7d3eb-217">Yöntem imzası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-217">Here is the signature of the method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="7d3eb-218">Yöntem anlamanız için gereken birkaç anahtar bileşenleri içerir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-218">The method has a few key components that you need to understand.</span></span>

* <span data-ttu-id="7d3eb-219">Yöntemi, dört parametreleri alır:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-219">The method takes four parameters:</span></span>

  1. <span data-ttu-id="7d3eb-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-220">**linkedServices**.</span></span> <span data-ttu-id="7d3eb-221">Giriş/Çıkış veri kaynakları bağlantı bağlı hizmetler numaralandırılabilir bir listesini (örneğin: Azure Blob Storage) veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) to the data factory.</span></span> <span data-ttu-id="7d3eb-222">Bu örnekte, yalnızca bir bağlantılı hizmet türü girdi ve çıktı için kullanılan Azure Storage yok.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="7d3eb-223">**veri kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-223">**datasets**.</span></span> <span data-ttu-id="7d3eb-224">Bu veri kümeleri numaralandırılabilir bir listesidir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="7d3eb-225">Giriş ve çıkış veri kümeleri tarafından tanımlanan şemaları ve konumlarını almak için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-225">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="7d3eb-226">**Etkinlik**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-226">**activity**.</span></span> <span data-ttu-id="7d3eb-227">Bu parametre, geçerli işlem varlık - bu durumda, bir Azure Batch hizmetini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-227">This parameter represents the current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="7d3eb-228">**Günlükçü**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-228">**logger**.</span></span> <span data-ttu-id="7d3eb-229">Günlükçü ardışık düzeni için "Kullanıcı" günlük olarak o yüzeyini hata ayıklama açıklamaları yazmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-229">The logger lets you write debug comments that surface as the “User” log for the pipeline.</span></span>
* <span data-ttu-id="7d3eb-230">Bu yöntem, özel etkinlikler gelecekte zincir için kullanılan bir sözlüğü döndürür.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-230">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="7d3eb-231">Bu özellik henüz uygulanmadı, bu nedenle boş bir sözlük döndürme.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-231">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>

#### <a name="procedure-create-the-custom-activity"></a><span data-ttu-id="7d3eb-232">Yordam: özel etkinlik oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-232">Procedure: Create the custom activity</span></span>
1. <span data-ttu-id="7d3eb-233">Visual Studio'da .NET sınıf kitaplığı proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="7d3eb-234">Başlatma **Visual Studio 2012**/**2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="7d3eb-235">**Dosya**’ya tıklayın, **Yeni**’nin üzerine gelin ve **Proje**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-235">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="7d3eb-236">Genişletme **şablonları**seçip **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="7d3eb-237">Bu kılavuzda, kullandığınız C\#, ancak özel etkinlik geliştirmek için herhangi bir .NET dil kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-237">In this walkthrough, you use C\#, but you can use any .NET language to develop the custom activity.</span></span>
   4. <span data-ttu-id="7d3eb-238">Seçin **sınıf kitaplığı** proje türleri sağdaki listeden.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-238">Select **Class Library** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="7d3eb-239">Girin **MyDotNetActivity** için **adı**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-239">Enter **MyDotNetActivity** for the **Name**.</span></span>
   6. <span data-ttu-id="7d3eb-240">Seçin **C:\\ADF** için **konumu**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-240">Select **C:\\ADF** for the **Location**.</span></span> <span data-ttu-id="7d3eb-241">Bir klasör oluşturun **ADF** henüz yoksa.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-241">Create the folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="7d3eb-242">Projeyi oluşturmak için **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-242">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="7d3eb-243">**Araçlar**'a tıklayın, **NuGet Paket Yöneticisi**'nin üzerine gelin ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-243">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="7d3eb-244">İçinde **Paket Yöneticisi Konsolu**, içeri aktarmak için aşağıdaki komutu yürütün **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-244">In the **Package Manager Console**, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="7d3eb-245">İçeri aktarma **Azure Storage** projesi için NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-245">Import the **Azure Storage** NuGet package in to the project.</span></span> <span data-ttu-id="7d3eb-246">Bu örnek Blob storage'da API kullandığından, bu paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-246">You need this package because you use the Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="7d3eb-247">Aşağıdakileri ekleyin **kullanarak** projenin kaynak dosyasında yönergeleri.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-247">Add the following **using** directives to the source file in the project.</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="7d3eb-248">Adını değiştirmek **ad alanı** için **MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-248">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="7d3eb-249">Sınıfın adını değiştirmek **MyDotNetActivity** ve buradan türetebilir **IDotNetActivity** arabirim aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-249">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="7d3eb-250">Uygulama (Ekle) **yürütme** yöntemi **IDotNetActivity** arabirimini **MyDotNetActivity** sınıfı ve aşağıdaki örnek kod yöntemi kopyalayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-250">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span> <span data-ttu-id="7d3eb-251">Bkz: [yöntemi Çalıştır](#execute-method) Bu yöntemde kullanılan mantığı için bir açıklama için bölüm.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-251">See the [Execute Method](#execute-method) section for explanation for the logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using the same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // To create an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass the connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize the continuation token before using it in the do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get the list of input blobs from the input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns the number of occurrences of
           // the search term (“Microsoft”) in each blob associated
           // with the data slice.
           //
           // definition of the method is shown in the next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob to the folder: {0}", folderPath);
    
       // create a storage object for the output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write the name of the file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload the output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} to the output blob", output);
       outputBlob.UploadText(output);
    
       // The dictionary can be used to chain custom activities together in the future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="7d3eb-252">Aşağıdaki yardımcı yöntemler sınıfına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-252">Add the following helper methods to the class.</span></span> <span data-ttu-id="7d3eb-253">Bu yöntemler tarafından çağrılan **yürütme** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-253">These methods are invoked by the **Execute** method.</span></span> <span data-ttu-id="7d3eb-254">En önemlisi, **Hesapla** yöntemi her bir blob tekrarlanan kod yalıtır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-254">Most importantly, the **Calculate** method isolates the code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets the fileName value from the input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
    /// and prepares the output text that is written to the output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="7d3eb-255">**GetFolderPath** yöntemi dataset işaret klasörünün yolunu döndürür ve **GetFileName** yöntemi dataset işaret blob/dosya adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-255">The **GetFolderPath** method returns the path to the folder that the dataset points to and the **GetFileName** method returns the name of the blob/file that the dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="7d3eb-256">**Hesapla** yöntemi hesaplar anahtar sözcüğü örnek sayısı **Microsoft** giriş dosyalarında (BLOB klasöründe).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-256">The **Calculate** method calculates the number of instances of keyword **Microsoft** in the input files (blobs in the folder).</span></span> <span data-ttu-id="7d3eb-257">Arama terimi kodda sabit kodlanmış ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="7d3eb-257">The search term (“Microsoft”) is hard-coded in the code.</span></span>

1. <span data-ttu-id="7d3eb-258">Projeyi derleyin.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-258">Compile the project.</span></span> <span data-ttu-id="7d3eb-259">Tıklatın **yapı** tıklatın ve menüden **yapı çözümü**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-259">Click **Build** from the menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="7d3eb-260">Başlatma **Windows Explorer**ve gidin **bin\\hata ayıklama** veya **bin\\yayın** klasörü yapı türüne bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-260">Launch **Windows Explorer**, and navigate to **bin\\debug** or **bin\\release** folder depending on the type of build.</span></span>
3. <span data-ttu-id="7d3eb-261">Zip dosyası oluşturun **MyDotNetActivity.zip** içindeki tüm ikili dosyaları içeren  **\\bin\\hata ayıklama** klasör.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-261">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the **\\bin\\Debug** folder.</span></span> <span data-ttu-id="7d3eb-262">MyDotNetActivity eklemek isteyebilirsiniz. **pdb** bir hata oluştuğunda, soruna neden kaynak kodunda satır numarası gibi ek ayrıntıları almak için dosya.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-262">You may want to include the MyDotNetActivity.**pdb** file so that you get additional details such as line number in the source code that caused the issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="7d3eb-263">Karşıya yükleme **MyDotNetActivity.zip** blob kapsayıcıya bir BLOB: `customactivitycontainer` Azure blob depolamada, **StorageLinkedService** bağlı hizmetinde  **ADFTutorialDataFactory** kullanır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-263">Upload **MyDotNetActivity.zip** as a blob to the blob container: `customactivitycontainer` in the Azure blob storage that the **StorageLinkedService** linked service in the **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="7d3eb-264">Blob kapsayıcı oluşturun `customactivitycontainer` zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-264">Create the blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="7d3eb-265">Execute yöntemi</span><span class="sxs-lookup"><span data-stu-id="7d3eb-265">Execute method</span></span>
<span data-ttu-id="7d3eb-266">Bu bölümde daha fazla ayrıntı ve yürütme yönteminin kodda hakkında notlar sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-266">This section provides more details and notes about the code in the Execute method.</span></span>

1. <span data-ttu-id="7d3eb-267">Giriş koleksiyonu yineleme için üyeleri bulunan [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) ad alanı.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-267">The members for iterating through the input collection are found in the [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="7d3eb-268">Blob koleksiyonu yineleme yapma kullanılması **BlobContinuationToken** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-268">Iterating through the blob collection requires using the **BlobContinuationToken** class.</span></span> <span data-ttu-id="7d3eb-269">Esas olarak, bir kullanın-while döngüsünü döngüden çıkma mekanizması olarak belirteci ile.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-269">In essence, you must use a do-while loop with the token as the mechanism for exiting the loop.</span></span> <span data-ttu-id="7d3eb-270">Daha fazla bilgi için bkz: [Blob storage kullanma konusunda](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-270">For more information, see [How to use Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="7d3eb-271">Temel bir döngü burada gösterilir:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize the continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get the list of input blobs from the input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="7d3eb-272">Belgelerine bakın [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) Ayrıntılar için yöntem.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-272">See the documentation for the [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="7d3eb-273">BLOB'ları kümesi aracılığıyla mantıksal olarak çalışmak için kod içinde do gider-while döngüsünü.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-273">The code for working through the set of blobs logically goes within the do-while loop.</span></span> <span data-ttu-id="7d3eb-274">İçinde **yürütme** yöntemi, do-döngü BLOB'ları listesi adlı bir yönteme geçirir **Hesapla**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-274">In the **Execute** method, the do-while loop passes the list of blobs to a method named **Calculate**.</span></span> <span data-ttu-id="7d3eb-275">Adlı bir dize değişkeni yöntemi döndürür **çıkış** kesimindeki tüm BLOB'lar aracılığıyla yinelendiğinde başka bir deyişle sonucu.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-275">The method returns a string variable named **output** that is the result of having iterated through all the blobs in the segment.</span></span>

   <span data-ttu-id="7d3eb-276">Arama terimi oluşumları sayısını döndürür (**Microsoft**) için geçirilen blob'daki **Hesapla** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-276">It returns the number of occurrences of the search term (**Microsoft**) in the blob passed to the **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="7d3eb-277">Bir kez **Hesapla** yöntemi iş Bitti, bunu yeni bir blob için yazılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-277">Once the **Calculate** method has done the work, it must be written to a new blob.</span></span> <span data-ttu-id="7d3eb-278">Bu nedenle her işlenen BLOB'lar kümesi için yeni blob sonuçlarıyla yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-278">So for every set of blobs processed, a new blob can be written with the results.</span></span> <span data-ttu-id="7d3eb-279">Yeni bir blob yazmak için ilk çıkış veri kümesi bulun.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-279">To write to a new blob, first find the output dataset.</span></span>

    ```csharp
    // Get the output dataset using the name of the dataset matched to a name in the Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="7d3eb-280">Kod ayrıca yardımcı yöntemini çağırır: **GetFolderPath** klasör yolu (depolama kapsayıcısı adı) alınamadı.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-280">The code also calls a helper method: **GetFolderPath** to retrieve the folder path (the storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="7d3eb-281">**GetFolderPath** FolderPath adlı bir özelliği olan bir AzureBlobDataSet DataSet nesnesine çevirir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-281">The **GetFolderPath** casts the DataSet object to an AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="7d3eb-282">Kod çağrıları **GetFileName** dosya adı (blob) alma yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-282">The code calls the **GetFileName** method to retrieve the file name (blob name).</span></span> <span data-ttu-id="7d3eb-283">Klasör yolu almak için yukarıdaki kod için kod benzer.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-283">The code is similar to the above code to get the folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="7d3eb-284">Dosyanın adını bir URI nesnesinden oluşturarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-284">The name of the file is written by creating a URI object.</span></span> <span data-ttu-id="7d3eb-285">URI Oluşturucusu kullanan **BlobEndpoint** kapsayıcı adını döndürmek için özellik.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-285">The URI constructor uses the **BlobEndpoint** property to return the container name.</span></span> <span data-ttu-id="7d3eb-286">Klasör yolunu ve dosya adı, çıktı blob URI'si oluşturmak eklenir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-286">The folder path and file name are added to construct the output blob URI.</span></span>  

    ```csharp
    // Write the name of the file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="7d3eb-287">Dosyanın adını yazılmış ve şimdi çıktı dizeden yazabilirsiniz **Hesapla** yöntemi yeni bir blob için:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-287">The name of the file has been written and now you can write the output string from the **Calculate** method to a new blob:</span></span>

    ```csharp
    // Create a blob and upload the output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} to the output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-the-data-factory"></a><span data-ttu-id="7d3eb-288">Veri Fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-288">Create the data factory</span></span>
<span data-ttu-id="7d3eb-289">İçinde [özel etkinlik oluşturmak](#create-the-custom-activity) bölüm, özel bir aktivite oluşturulur ve bir Azure blob kapsayıcısına ikili dosyaları zip dosyasıyla ve PDB dosya karşıya.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-289">In the [Create the custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded the zip file with binaries and the PDB file to an Azure blob container.</span></span> <span data-ttu-id="7d3eb-290">Bu bölümde, oluşturduğunuz Azure **veri fabrikası** ile bir **ardışık düzen** kullanan **özel etkinlik**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-290">In this section, you create an Azure **data factory** with a **pipeline** that uses the **custom activity**.</span></span>

<span data-ttu-id="7d3eb-291">Özel Etkinlik için giriş veri kümesi (dosyaları) BLOB giriş klasöründe temsil eder (`mycontainer\\inputfolder`) blob depolama.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-291">The input dataset for the custom activity represents the blobs (files) in the input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="7d3eb-292">Çıktı veri kümesi etkinliğinin çıkış klasöründe çıkış BLOB'ları temsil eder (`mycontainer\\outputfolder`) blob depolama.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-292">The output dataset for the activity represents the output blobs in the output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="7d3eb-293">Bir veya daha fazla giriş klasörlerde bırak:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-293">Drop one or more files in the input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="7d3eb-294">Örneğin, bir dosya (dosya.txt'yi) aşağıdaki içerik ile her klasörler bırakın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-294">For example, drop one file (file.txt) with the following content into each of the folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="7d3eb-295">2 veya daha fazla dosya klasör sahip olsa bile her giriş klasörü Azure Data factory'de bir dilim karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-295">Each input folder corresponds to a slice in Azure Data Factory even if the folder has 2 or more files.</span></span> <span data-ttu-id="7d3eb-296">Her dilimi ardışık düzen tarafından işlendiğinde, özel etkinlik tüm BLOB'ları, dilim için giriş klasörü dolaşır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-296">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="7d3eb-297">Aynı içeriğe sahip beş çıktı dosyalarına bakın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-297">You see five output files with the same content.</span></span> <span data-ttu-id="7d3eb-298">Örneğin, 2015-11-16-00 klasöründeki dosyaya işlemesini çıktı dosyası aşağıdaki içeriğe sahip:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-298">For example, the output file from processing the file in the 2015-11-16-00 folder has the following content:</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="7d3eb-299">Giriş klasörü aynı içeriğe sahip birden çok dosya (dosya.txt'yi, file2.txt, file3.txt) bırakma, çıktı dosyasında aşağıdaki içeriğe bakın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with the same content to the input folder, you see the following content in the output file.</span></span> <span data-ttu-id="7d3eb-300">Her bir klasör (2015-11-16-00, vb.) birden çok giriş dosyaları klasörü olmasına rağmen bir dilim bu örnekteki karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-300">Each folder (2015-11-16-00, etc.) corresponds to a slice in this sample even though the folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="7d3eb-301">Çıktı dosyası üç satır artık, her girdi dosyasında (blob) (2015-11-16-00) dilimle ilişkili klasörü için bir tane var.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-301">The output file has three lines now, one for each input file (blob) in the folder associated with the slice (2015-11-16-00).</span></span>

<span data-ttu-id="7d3eb-302">Bir görev çalıştırmak her etkinlik için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-302">A task is created for each activity run.</span></span> <span data-ttu-id="7d3eb-303">Bu örnekte, ardışık düzeninde yalnızca bir etkinlik yok.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-303">In this sample, there is only one activity in the pipeline.</span></span> <span data-ttu-id="7d3eb-304">Bir dilim ardışık düzen tarafından işlendiğinde, özel etkinlik dilim işlemek için Azure Batch üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-304">When a slice is processed by the pipeline, the custom activity runs on Azure Batch to process the slice.</span></span> <span data-ttu-id="7d3eb-305">Beş dilimleri (her dilim birden çok BLOB veya dosya olabilir) olduğundan, Azure Batch oluşturulan beş görevler vardır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="7d3eb-306">Bir görev toplu olarak çalıştığında, gerçekte çalıştıran özel etkinlik olduğu.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-306">When a task runs on Batch, it is actually the custom activity that is running.</span></span>

<span data-ttu-id="7d3eb-307">Aşağıdaki örneklerde ek ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-307">The following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="7d3eb-308">1. adım: veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-308">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="7d3eb-309">Oturum açtıktan sonra [Azure portal](https://portal.azure.com/), aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-309">After logging in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>

   1. <span data-ttu-id="7d3eb-310">Sol menüde **YENİ**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-310">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="7d3eb-311">Tıklatın **veri + analiz** içinde **yeni** dikey.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-311">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="7d3eb-312">**Veri analizi** dikey penceresinde **Data Factory**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-312">Click **Data Factory** on the **Data analytics** blade.</span></span>
2. <span data-ttu-id="7d3eb-313">İçinde **yeni data factory** dikey penceresinde girin **CustomActivityFactory** adı.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-313">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="7d3eb-314">Azure veri fabrikasının adı genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-314">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="7d3eb-315">Hatayı alırsanız: **veri fabrikası adı "CustomActivityFactory" kullanılabilir değil**, data factory adını değiştirin (örneğin, **yournameCustomActivityFactory**) ve oluşturmayı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-315">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="7d3eb-316">Tıklatın **kaynak grubu adı**, varolan bir kaynak grubu seçin veya bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="7d3eb-317">Oluşturulacak data factory bölgesini ve doğru aboneliğin kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-317">Verify that you are using the correct subscription and region where you want the data factory to be created.</span></span>
5. <span data-ttu-id="7d3eb-318">**Yeni data factory** dikey penceresinde **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-318">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="7d3eb-319">Oluşturulmakta veri fabrikası gördüğünüz **Pano** Azure portalının.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-319">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="7d3eb-320">Data factory sorunsuz oluşturulduktan sonra data factory sayfasını görürsünüz, burada size data factory içeriği gösterilir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-320">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="7d3eb-321">2. adım: bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-321">Step 2: Create linked services</span></span>
<span data-ttu-id="7d3eb-322">Bağlı hizmetler veri depolarını veya işlem hizmetlerini Azure data factory’ye bağlar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-322">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="7d3eb-323">Bu adımda, bağlantı, **Azure Storage** hesabı ve **Azure Batch** hesabınızı data factory'nize.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-323">In this step, you link your **Azure Storage** account and **Azure Batch** account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="7d3eb-324">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="7d3eb-325">Tıklatın **yazar ve dağıtma** döşemesinin **DATA FACTORY** dikey **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-325">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="7d3eb-326">Data Factory Düzenleyici bakın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-326">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="7d3eb-327">Tıklatın **yeni veri deposu** komut çubuğu ve seçin **Azure depolama.**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-327">Click **New data store** on the command bar and choose **Azure storage.**</span></span> <span data-ttu-id="7d3eb-328">Düzenleyicide Azure Storage bağlı hizmeti oluşturmak için JSON betiğini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-328">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="7d3eb-329">**accountname** sözcüğünü Azure depolama hesabınızın adıyla, **accountkey** sözcüğünü de Azure depolama hesabının erişim anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-329">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="7d3eb-330">Depolama erişim anahtarınızı nasıl alacağınız hakkında bilgi için bkz. [Depolama erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-330">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="7d3eb-331">Bağlı hizmeti dağıtmak için komut çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-331">Click **Deploy** on the command bar to deploy the linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="7d3eb-332">Azure Batch bağlı hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="7d3eb-333">Bu adımda oluşturduğunuz için bağlı hizmet, **Azure Batch** Data Factory Özel Etkinlik çalıştırmak için kullanılan hesap.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-333">In this step, you create a linked service for your **Azure Batch** account that is used to run the Data Factory custom activity.</span></span>

1. <span data-ttu-id="7d3eb-334">Tıklatın **yeni işlem** komut çubuğu ve seçin **Azure Batch.**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-334">Click **New compute** on the command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="7d3eb-335">Düzenleyicide Azure Batch bağlı hizmeti oluşturmak için JSON betiğini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-335">You should see the JSON script for creating an Azure Batch linked service in the editor.</span></span>
2. <span data-ttu-id="7d3eb-336">JSON betiği:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-336">In the JSON script:</span></span>

   1. <span data-ttu-id="7d3eb-337">Değiştir **hesap adı** Azure Batch hesabınızın adı.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-337">Replace **account name** with the name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="7d3eb-338">Değiştir **erişim tuşu** Azure Batch hesabının erişim anahtarı ile.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-338">Replace **access key** with the access key of the Azure Batch account.</span></span>
   3. <span data-ttu-id="7d3eb-339">İçin havuz Kimliğini girin **poolName** özelliği**.**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-339">Enter the ID of the pool for the **poolName** property**.**</span></span> <span data-ttu-id="7d3eb-340">Bu özellik için ya da havuz adı belirtin veya Havuz kimliği.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="7d3eb-341">URI toplu girmek için **batchUri** JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-341">Enter the batch URI for the **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="7d3eb-342">**URL** gelen **Azure Batch hesabı dikey** aşağıdaki biçimdedir: \<accountname\>.\< Bölge\>. batch.azure.com. İçin **batchUri** özelliği JSON içinde gereken **"accountname." Kaldır**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-342">The **URL** from the **Azure Batch account blade** is in the following format: \<accountname\>.\<region\>.batch.azure.com. For the **batchUri** property in the JSON, you need to **remove "accountname."**</span></span> <span data-ttu-id="7d3eb-343">URL.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-343">from the URL.</span></span> <span data-ttu-id="7d3eb-344">Örnek: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="7d3eb-345">İçin **poolName** özelliği, havuzu havuzunun adı yerine Kimliğini de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-345">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7d3eb-346">Hdınsight için yaptığı gibi Data Factory hizmeti Azure toplu işlem için bir isteğe bağlı seçeneği desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-346">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="7d3eb-347">Bu gibi durumlarda, kendi Azure Batch havuzu yalnızca bir Azure data factory kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="7d3eb-348">Belirtin **StorageLinkedService** için **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-348">Specify **StorageLinkedService** for the **linkedServiceName** property.</span></span> <span data-ttu-id="7d3eb-349">Bu bağlı hizmeti önceki adımda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-349">You created this linked service in the previous step.</span></span> <span data-ttu-id="7d3eb-350">Bu depolama dosyaları ve günlükleri için hazırlama alanı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="7d3eb-351">Bağlı hizmeti dağıtmak için komut çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-351">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="7d3eb-352">3. adım: veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-352">Step 3: Create datasets</span></span>
<span data-ttu-id="7d3eb-353">Bu adımda, girdi ve çıktı verilerini temsil edecek veri kümeleri oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-353">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="7d3eb-354">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-354">Create input dataset</span></span>
1. <span data-ttu-id="7d3eb-355">İçinde **Düzenleyicisi** veri fabrikası için tıklatın **yeni veri kümesi** düğmesini tıklatın ve araç **Azure Blob Depolama** açılır menüsünden.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-355">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="7d3eb-356">Sağ bölmedeki JSON aşağıdaki JSON parçacığıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-356">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    <span data-ttu-id="7d3eb-357">Başlangıç saati ile bu kılavuzda daha sonra bir işlem hattı oluşturma: 2015-11-16T00:00:00Z ve bitiş zamanı: 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="7d3eb-358">Veri üretmek için zamanlanmış **saatlik**, 5 giriş/çıkış dilimler olduklarından (arasında **00**: 00:00 -\> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-358">It is scheduled to produce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="7d3eb-359">**Sıklığı** ve **aralığı** girdi veri kümesi ayarlanmıştır **saat** ve **1**, girdi dilimi saatlik kullanılabilir olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-359">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span>

    <span data-ttu-id="7d3eb-360">Tarafından temsil edilen her dilim için başlangıç zamanlarını işte **SliceStart** yukarıdaki JSON parçacığında bulunan sistem değişkeni.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-360">Here are the start times for each slice, which is represented by **SliceStart** system variable in the above JSON snippet.</span></span>

    | <span data-ttu-id="7d3eb-361">**Dilim**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-361">**Slice**</span></span> | <span data-ttu-id="7d3eb-362">**Başlangıç zamanı**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="7d3eb-363">1</span><span class="sxs-lookup"><span data-stu-id="7d3eb-363">1</span></span>         | <span data-ttu-id="7d3eb-364">2015 11 16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="7d3eb-365">2</span><span class="sxs-lookup"><span data-stu-id="7d3eb-365">2</span></span>         | <span data-ttu-id="7d3eb-366">2015 11 16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="7d3eb-367">3</span><span class="sxs-lookup"><span data-stu-id="7d3eb-367">3</span></span>         | <span data-ttu-id="7d3eb-368">2015 11 16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="7d3eb-369">4</span><span class="sxs-lookup"><span data-stu-id="7d3eb-369">4</span></span>         | <span data-ttu-id="7d3eb-370">2015 11 16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="7d3eb-371">5</span><span class="sxs-lookup"><span data-stu-id="7d3eb-371">5</span></span>         | <span data-ttu-id="7d3eb-372">2015 11 16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="7d3eb-373">**FolderPath** dilim başlangıç zamanı yıl, ay, gün ve saat parçası kullanılarak hesaplanır (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="7d3eb-373">The **folderPath** is calculated by using the year, month, day, and hour part of the slice start time (**SliceStart**).</span></span> <span data-ttu-id="7d3eb-374">Bu nedenle, işte bir giriş klasörü için bir dilim nasıl eşlendi.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-374">Therefore, here is how an input folder is mapped to a slice.</span></span>

    | <span data-ttu-id="7d3eb-375">**Dilim**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-375">**Slice**</span></span> | <span data-ttu-id="7d3eb-376">**Başlangıç zamanı**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-376">**Start time**</span></span>          | <span data-ttu-id="7d3eb-377">**Giriş klasörü**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="7d3eb-378">1</span><span class="sxs-lookup"><span data-stu-id="7d3eb-378">1</span></span>         | <span data-ttu-id="7d3eb-379">2015 11 16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="7d3eb-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="7d3eb-381">2</span><span class="sxs-lookup"><span data-stu-id="7d3eb-381">2</span></span>         | <span data-ttu-id="7d3eb-382">2015 11 16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="7d3eb-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="7d3eb-384">3</span><span class="sxs-lookup"><span data-stu-id="7d3eb-384">3</span></span>         | <span data-ttu-id="7d3eb-385">2015 11 16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="7d3eb-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="7d3eb-387">4</span><span class="sxs-lookup"><span data-stu-id="7d3eb-387">4</span></span>         | <span data-ttu-id="7d3eb-388">2015 11 16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="7d3eb-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="7d3eb-390">5</span><span class="sxs-lookup"><span data-stu-id="7d3eb-390">5</span></span>         | <span data-ttu-id="7d3eb-391">2015 11 16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="7d3eb-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="7d3eb-393">Tıklatın **dağıtma** oluşturmak ve dağıtmak için araç çubuğunda **InputDataset** tablo.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-393">Click **Deploy** on the toolbar to create and deploy the **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="7d3eb-394">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-394">Create output dataset</span></span>
<span data-ttu-id="7d3eb-395">Bu adımda, çıktı verilerini göstermek için AzureBlob türünde başka bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-395">In this step, you create another dataset of type AzureBlob to represent the output data.</span></span>

1. <span data-ttu-id="7d3eb-396">İçinde **Düzenleyicisi** veri fabrikası için tıklatın **yeni veri kümesi** düğmesini tıklatın ve araç **Azure Blob Depolama** açılır menüsünden.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-396">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="7d3eb-397">Sağ bölmedeki JSON aşağıdaki JSON parçacığıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-397">Replace the JSON in the right pane with the following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    <span data-ttu-id="7d3eb-398">Bir çıkış blob/dosyası, her girdi dilimi için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="7d3eb-399">İşte bir çıktı dosyası için her dilimi nasıl adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="7d3eb-400">Bir çıkış klasöründe oluşturulan tüm çıktı dosyaları: `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-400">All the output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="7d3eb-401">**Dilim**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-401">**Slice**</span></span> | <span data-ttu-id="7d3eb-402">**Başlangıç zamanı**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-402">**Start time**</span></span>          | <span data-ttu-id="7d3eb-403">**Çıkış dosyası**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="7d3eb-404">1</span><span class="sxs-lookup"><span data-stu-id="7d3eb-404">1</span></span>         | <span data-ttu-id="7d3eb-405">2015 11 16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="7d3eb-406">2015-11-16 -**00. txt**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="7d3eb-407">2</span><span class="sxs-lookup"><span data-stu-id="7d3eb-407">2</span></span>         | <span data-ttu-id="7d3eb-408">2015 11 16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="7d3eb-409">2015-11-16 -**01. txt**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="7d3eb-410">3</span><span class="sxs-lookup"><span data-stu-id="7d3eb-410">3</span></span>         | <span data-ttu-id="7d3eb-411">2015 11 16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="7d3eb-412">2015-11-16 -**02. txt**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="7d3eb-413">4</span><span class="sxs-lookup"><span data-stu-id="7d3eb-413">4</span></span>         | <span data-ttu-id="7d3eb-414">2015 11 16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="7d3eb-415">2015-11-16 -**03. txt**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="7d3eb-416">5</span><span class="sxs-lookup"><span data-stu-id="7d3eb-416">5</span></span>         | <span data-ttu-id="7d3eb-417">2015 11 16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="7d3eb-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="7d3eb-418">2015-11-16 -**04. txt**</span><span class="sxs-lookup"><span data-stu-id="7d3eb-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="7d3eb-419">Unutmayın Giriş bir klasördeki tüm dosyalar (örneğin: 2015-11-16-00) bir dilim başlangıç saatine sahip bir parçasıdır: 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-419">Remember that all the files in an input folder (for example: 2015-11-16-00) are part of a slice with the start time: 2015-11-16-00.</span></span> <span data-ttu-id="7d3eb-420">Bu dilim işlendiğinde özel etkinlik her dosyası aracılığıyla tarar ve arama terimi ("Microsoft"), yineleme sayısı ile çıkış dosyasındaki bir satır üretir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-420">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="7d3eb-421">2015-11-16-00 klasöründe üç dosya varsa, üç satırları vardır çıktı dosyasına: 2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-421">If there are three files in the folder 2015-11-16-00, there are three lines in the output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="7d3eb-422">Tıklatın **dağıtma** oluşturmak ve dağıtmak için araç çubuğunda **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-422">Click **Deploy** on the toolbar to create and deploy the **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-the-pipeline-with-custom-activity"></a><span data-ttu-id="7d3eb-423">4. adım: Oluşturma ve özel etkinliği ile işlem hattı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-423">Step 4: Create and run the pipeline with custom activity</span></span>
<span data-ttu-id="7d3eb-424">Bu adımda, bir etkinlik, daha önce oluşturduğunuz özel etkinliği ile işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-424">In this step, you create a pipeline with one activity, the custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7d3eb-425">Karşıya henüz yüklediyseniz **dosya.txt'yi** klasörleri blob kapsayıcısında giriş için işlem hattı oluşturmadan önce bunu.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-425">If you haven't uploaded the **file.txt** to input folders in the blob container, do so before creating the pipeline.</span></span> <span data-ttu-id="7d3eb-426">**İsPaused** özelliği ayarlanmış JSON, işlem hattındaki false ardışık hemen nedenle olarak **Başlat** geçmişte tarihidir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-426">The **isPaused** property is set to false in the pipeline JSON, so the pipeline runs immediately as the **start** date is in the past.</span></span>
>
>

1. <span data-ttu-id="7d3eb-427">Data Factory Düzenleyici'yi tıklatın **yeni işlem hattı** komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-427">In the Data Factory Editor, click **New pipeline** on the command bar.</span></span> <span data-ttu-id="7d3eb-428">Komut görmüyorsanız tıklatın **... (Üç nokta)**  görmek için.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-428">If you do not see the command, click **... (Ellipsis)** to see it.</span></span>
2. <span data-ttu-id="7d3eb-429">Sağ bölmedeki JSON aşağıdaki JSON betiği ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-429">Replace the JSON in the right pane with the following JSON script:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="7d3eb-430">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-430">Note the following points:</span></span>

   * <span data-ttu-id="7d3eb-431">Ardışık düzeninde yalnızca bir etkinlik vardır ve bu tür: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-431">There is only one activity in the pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="7d3eb-432">**AssemblyName** DLL adına ayarlayın: **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-432">**AssemblyName** is set to the name of the DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="7d3eb-433">**EntryPoint** ayarlanır **MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-433">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="7d3eb-434">Temelde olan \<ad alanı\>.\< ClassName\> kodunuzda.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="7d3eb-435">**PackageLinkedService** ayarlanır **StorageLinkedService** özel etkinlik zip dosyasını içeren blob depolama alanına işaret eder.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-435">**PackageLinkedService** is set to **StorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="7d3eb-436">Giriş/çıkış dosyaları ve özel etkinlik zip dosyası için farklı Azure depolama hesapları kullanıyorsanız, başka bir Azure Storage bağlı hizmeti oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-436">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you have to create another Azure Storage linked service.</span></span> <span data-ttu-id="7d3eb-437">Bu makalede, aynı Azure Storage hesabını kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-437">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="7d3eb-438">**PackageFile** ayarlanır **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-438">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="7d3eb-439">Şu biçimdedir: \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-439">It is in the format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="7d3eb-440">Özel Etkinlik alır **InputDataset** giriş olarak ve **OutputDataset** çıktı olarak.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-440">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="7d3eb-441">**LinkedServiceName** özel etkinlik özelliğinin işaret **AzureBatchLinkedService**, özel etkinlik Azure toplu olarak çalıştırmak için gereken bir Azure Data Factory söyler.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-441">The **linkedServiceName** property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch.</span></span>
   * <span data-ttu-id="7d3eb-442">**Eşzamanlılık** ayarı önemlidir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-442">The **concurrency** setting is important.</span></span> <span data-ttu-id="7d3eb-443">1, 2 veya daha fazla işlem düğümleri Azure Batch havuzunda olsa dahi, varsayılan değeri kullanırsanız dilimleri işlenir birbiri ardından.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-443">If you use the default value, which is 1, even if you have 2 or more compute nodes in the Azure Batch pool, the slices are processed one after another.</span></span> <span data-ttu-id="7d3eb-444">Bu nedenle, Azure batch paralel işleme yeteneğinden olmuyor.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-444">Therefore, you are not taking advantage of the parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="7d3eb-445">Ayarlarsanız **eşzamanlılık** daha yüksek bir değere deyin 2, bu iki dilimler anlamına gelir (Azure Batch iki görevlere karşılık gelir) aynı anda; bu durumda VM'ler havuzu kullanıldığı Azure Batch içinde işlenir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-445">If you set **concurrency** to a higher value, say 2, it means that two slices (corresponds to two tasks in Azure Batch) can be processed at the same time, in which case, both the VMs in the Azure Batch pool are utilized.</span></span> <span data-ttu-id="7d3eb-446">Bu nedenle, eşzamanlılık özelliğini uygun şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-446">Therefore, set the concurrency property appropriately.</span></span>
   * <span data-ttu-id="7d3eb-447">Yalnızca bir görev (dilim) varsayılan olarak, varsayılan olarak herhangi bir noktada bir VM üzerinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="7d3eb-448">, Varsayılan olarak, bir nedeni **maksimum VM başına görevleri** için bir Azure Batch havuzu 1 ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-448">The reason is that, by default, the **Maximum tasks per VM** is set to 1 for an Azure Batch pool.</span></span> <span data-ttu-id="7d3eb-449">Önkoşullar bir parçası olarak, bu özelliği 2'ye iki Data Factory dilimler bir VM üzerinde aynı anda çalışabilir şekilde ayarlanmış bir havuzu oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-449">As part of prerequisites, you created a pool with this property set to 2, so two Data Factory slices can be running on a VM at the same time.</span></span>

    -   <span data-ttu-id="7d3eb-450">**isPaused** özelliği varsayılan olarak false değerine ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-450">**isPaused** property is set to false by default.</span></span> <span data-ttu-id="7d3eb-451">Geçmişte dilimleri başlatmak için ardışık düzen hemen bu örnekte çalışır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-451">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="7d3eb-452">Bu özelliği, ardışık düzen duraklatma ve yeniden başlatmak için geri false olarak ayarlamak için true olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-452">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>

    -   <span data-ttu-id="7d3eb-453">**Başlat** zaman ve **son** kez beş saatten birbirinden olur ve dilimlerinin saatlik, ardışık düzen tarafından beş dilimlerinin şekilde.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-453">The **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>

1. <span data-ttu-id="7d3eb-454">İşlem hattını dağıtmak için komut çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-454">Click **Deploy** on the command bar to deploy the pipeline.</span></span>

#### <a name="step-5-test-the-pipeline"></a><span data-ttu-id="7d3eb-455">5. adım: Test ardışık düzeni</span><span class="sxs-lookup"><span data-stu-id="7d3eb-455">Step 5: Test the pipeline</span></span>
<span data-ttu-id="7d3eb-456">Bu adımda, ardışık düzen giriş klasörler halinde dosyaları bırakarak sınayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-456">In this step, you test the pipeline by dropping files into the input folders.</span></span> <span data-ttu-id="7d3eb-457">Bir giriş klasörü başına bir dosyayı ile işlem hattı testi ile başlayalım.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-457">Let’s start with testing the pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="7d3eb-458">Azure Portal'daki Data Factory dikey penceresinde tıklayın **diyagramı**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-458">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="7d3eb-459">Diyagram Görünümü'nde girdi veri kümesi çift tıklatın: **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-459">In the diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="7d3eb-460">Görmeniz gerekir **InputDataset** beş dikey dilimi hazır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-460">You should see the **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="7d3eb-461">Bildirim **DİLİM başlangıç saati** ve **DİLİM bitiş saati** her dilim için.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-461">Notice the **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="7d3eb-462">İçinde **diyagram görünümü**, şimdi **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-462">In the **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="7d3eb-463">Bunlar zaten oluşturulmuş olduğunu beş çıkış dilimi hazır durumda olduğunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-463">You should see that the five output slices are in the Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="7d3eb-464">Görüntülemek için Azure portal'ı kullanmanızı **görevleri** ile ilişkili **dilimler** ve her dilim çalıştırdı hangi VM bakın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-464">Use Azure portal to view the **tasks** associated with the **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="7d3eb-465">Bkz: [Data Factory ve toplu tümleştirme](#data-factory-and-batch-integration) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="7d3eb-466">Çıkış dosyaları görmelisiniz `outputfolder` , `mycontainer` , Azure blob depolamada.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-466">You should see the output files in the `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="7d3eb-467">Bir giriş her dilim için beş çıktı dosyalarını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="7d3eb-468">Her çıktı dosyasının içeriği aşağıdaki çıkış benzer olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-468">Each of the output file should have content similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="7d3eb-469">Aşağıdaki diyagram, veri fabrikası dilimler Azure Batch görevlerinde nasıl eşleneceğine gösterir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-469">The following diagram illustrates how the Data Factory slices map to tasks in Azure Batch.</span></span> <span data-ttu-id="7d3eb-470">Bu örnekte, yalnızca bir çalışma bir dilimi var.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="7d3eb-471">Şimdi, bir klasördeki birden çok dosyalarla deneyelim.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="7d3eb-472">Dosyaları oluşturun: **file2.txt**, **file3.txt**, **file4.txt**, ve **file5.txt** klasöründeki dosya.txt'yi olduğu gibi aynı içeriğe sahip:  **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with the same content as in file.txt in the folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="7d3eb-473">Çıkış klasöründe **silmek** çıktı dosyası: **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-473">In the output folder, **delete** the output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="7d3eb-474">Şimdi **OutputDataset** dikey penceresinde bir dilimle sağ tıklatın **DİLİM başlangıç saati** kümesine **11/16/2015 01:00:00 AM**, tıklatıp **çalıştırmak** için yeniden çalıştır/yeniden-process dilim.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-474">Now, in the **OutputDataset** blade, right-click the slice with **SLICE START TIME** set to **11/16/2015 01:00:00 AM**, and click **Run** to rerun/re-process the slice.</span></span> <span data-ttu-id="7d3eb-475">Şimdi, dilim beş dosya yerine bir dosya vardır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-475">Now, the slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="7d3eb-476">Dilim çalıştırır ve durumu sonra **hazır**, bu dilim için çıktı dosyasında içeriği doğrulayın (**2015-11-16-01.txt**) içinde `outputfolder` , `mycontainer` blob depolama alanınızın içinde.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-476">After the slice runs and its status is **Ready**, verify the content in the output file for this slice (**2015-11-16-01.txt**) in the `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="7d3eb-477">Dilimin her dosya için bir satır olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-477">There should be a line for each file of the slice.</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="7d3eb-478">Beş giriş dosyalarıyla denemeden önce çıktı dosyası 2015-11-16-01.txt silmedi, tek bir çizgi önceki dilim çalıştırma ve geçerli dilimin çalıştırma beş satırları bakın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-478">If you did not delete the output file 2015-11-16-01.txt before trying with five input files, you see one line from the previous slice run and five lines from the current slice run.</span></span> <span data-ttu-id="7d3eb-479">Varsayılan olarak, içeriği zaten varsa çıkış dosyasına eklenir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-479">By default, the content is appended to output file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="7d3eb-480">Veri Fabrikası ve toplu tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="7d3eb-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="7d3eb-481">Data Factory hizmetinin bir iş Azure Batch adıyla oluşturur: `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-481">The Data Factory service creates a job in Azure Batch with the name: `adf-poolname:job-xxx`.</span></span>

![Azure Data Factory - toplu işler](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="7d3eb-483">İş bir görevde bir dilim her etkinlik çalıştırması için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-483">A task in the job is created for each activity run of a slice.</span></span> <span data-ttu-id="7d3eb-484">10 dilimler işlenmeye hazır varsa, 10 görevleri işi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-484">If there are 10 slices ready to be processed, 10 tasks are created in the job.</span></span> <span data-ttu-id="7d3eb-485">Birden çok işlem düğümleri havuzunda varsa paralel olarak çalışan birden fazla dilim olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-485">You can have more than one slice running in parallel if you have multiple compute nodes in the pool.</span></span> <span data-ttu-id="7d3eb-486">İşlem düğümü başına en fazla görevleri ayarlarsanız > 1'e, aynı işlem üzerinde çalışan birden fazla dilim olabilir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-486">If the maximum tasks per compute node is set to > 1, there can be more than one slice running on the same compute.</span></span>

<span data-ttu-id="7d3eb-487">Bu örnekte, beş dilimler, Azure Batch kadar beş görevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="7d3eb-488">İle **eşzamanlılık** kümesine **5** Azure veri fabrikası'nda JSON işlem hattındaki ve **maksimum VM başına görevleri** kümesine **2** Azure Batch havuzunda ile **2** VM'ler, (görevler için başlangıç ve bitiş zamanlarını denetleyin) görevleri çalıştırır hızlı.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-488">With the **concurrency** set to **5** in the pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set to **2** in Azure Batch pool with **2** VMs, the tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="7d3eb-489">Toplu işlem ve ilişkili görevleri görüntülemek üzere portalı kullanın **dilimler** ve her dilim çalıştırdı hangi VM bakın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-489">Use the portal to view the Batch job and its tasks that are associated with the **slices** and see what VM each slice ran on.</span></span>

![Azure Data Factory - toplu iş görevleri](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-the-pipeline"></a><span data-ttu-id="7d3eb-491">Ardışık Düzen hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="7d3eb-491">Debug the pipeline</span></span>
<span data-ttu-id="7d3eb-492">Hata ayıklama birkaç temel teknikten oluşur:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="7d3eb-493">Girdi dilimi ayarlanmamışsa **hazır**, giriş klasör yapısı doğru olduğunu ve dosya.txt'yi giriş klasörlerde var olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-493">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and file.txt exists in the input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="7d3eb-494">İçinde **yürütme** özel etkinliklerinizi, kullanım yöntemi **IActivityLogger** sorunlarını gidermenize yardımcı olacak bilgileri oturum nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-494">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="7d3eb-495">Günlüğe kaydedilen iletilere kullanıcı görünmesini\_0. günlük dosyası.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-495">The logged messages show up in the user\_0.log file.</span></span>

   <span data-ttu-id="7d3eb-496">İçinde **OutputDataset** dikey penceresinde görmek için dilimi tıklatın **veri DİLİMİ** dikey penceresinde, dilim için.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-496">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="7d3eb-497">Gördüğünüz **etkinlik çalışması** bu dilim için.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="7d3eb-498">Bir etkinlik için dilim görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-498">You should see one activity run for the slice.</span></span> <span data-ttu-id="7d3eb-499">Tıklatırsanız **çalıştırmak** komut çubuğunda, aynı dilim için başka bir etkinlik başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-499">If you click **Run** in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="7d3eb-500">Etkinliğin çalışma tıklattığınızda gördüğünüz **etkinlik çalışma ayrıntıları** günlük dosyalarının listesini içeren dikey.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-500">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="7d3eb-501">İçinde günlüğe kaydedilen iletilere bakın **kullanıcı\_0. günlük** dosya.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-501">You see logged messages in the **user\_0.log** file.</span></span> <span data-ttu-id="7d3eb-502">Hata oluştuğunda, yeniden deneme sayısı 3 JSON ardışık düzeni/etkinliği olarak ayarlandığından, üç Etkinlik çalışması görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-502">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="7d3eb-503">Etkinlik Çalıştır'ı tıklatın, hatayı gidermek için gözden geçirebilirsiniz günlük dosyalarına bakın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-503">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="7d3eb-504">Günlük dosyaları listesinde tıklatın **kullanıcı 0.log**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-504">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="7d3eb-505">Sağ panelde kullanarak sonucu olan **IActivityLogger.Write** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-505">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="7d3eb-506">Sistem hata iletileri ve özel durumlar için sistem 0.log denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="7d3eb-507">Dahil **PDB** hata ayrıntılarını bilgileri gibi böylece zip dosyasında dosya **çağrı yığını** bir hata oluştuğunda.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-507">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="7d3eb-508">Özel Etkinlik için zip dosyası tüm dosyalarda olmalıdır **üst düzey** klasörsüz ile.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-508">All the files in the zip file for the custom activity must be at the **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="7d3eb-509">Emin **assemblyName** (MyDotNetActivity.dll) **entryPoint** (MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) ve **packageLinkedService** (zip dosyasını içeren Azure blob depolama alanına işaret etmelidir) için doğru değerleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-509">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the Azure blob storage that contains the zip file) are set to correct values.</span></span>
6. <span data-ttu-id="7d3eb-510">Bir hatayı düzelttiyseniz ve dilimi yeniden işlemek istiyorsanız **OutputDataset** dikey penceresindeki dilime sağ tıklayın ve **Çalıştır**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-510">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="7d3eb-511">Gördüğünüz bir **kapsayıcı** adlı Azure Blob storage'da: `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="7d3eb-512">Bu kapsayıcı otomatik olarak silinmez, ancak tamamlandıktan sonra güvenle silebilirsiniz çözüm test ediliyor.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-512">This container is not automatically deleted, but you can safely delete it after you are done testing the solution.</span></span> <span data-ttu-id="7d3eb-513">Benzer şekilde, bir Azure Batch Data Factory çözüm oluşturur **iş** adlı: `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-513">Similarly, the Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="7d3eb-514">İsterseniz, çözümü test ettikten sonra bu iş silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-514">You can delete this job after you test the solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="7d3eb-515">Özel Etkinlik kullanmayan **app.config** paketinizi dosyasından.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-515">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="7d3eb-516">Bu nedenle, kodunuzu yapılandırma dosyasından bağlantı dizelerini yazıyorsa, çalışma zamanında çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-516">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="7d3eb-517">Azure Batch kullanarak tüm gizli tutmak için olduğunda en iyi uygulama bir **Azure KeyVault**keyvault korumak için bir sertifika tabanlı hizmet sorumlusu kullanın ve Azure Batch havuzu sertifikaya dağıtın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-517">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the keyvault, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="7d3eb-518">Böylece .NET özel etkinliği çalıştırma sırasında KeyVault’tan parolalara erişebilir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-518">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="7d3eb-519">Bu çözüm genel bir ve gizli anahtarı, yalnızca bağlantı dizesi herhangi bir türde ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-519">This solution is a generic one and can scale to any type of secret, not just connection string.</span></span>

    <span data-ttu-id="7d3eb-520">Daha kolay bir çözüm (ancak en iyi yöntem değildir): oluşturabileceğiniz bir **Azure SQL bağlı hizmeti** bağlantı dizesi ayarlarıyla bağlantılı hizmet kullanan bir veri kümesi oluşturma ve sahte bir giriş veri kümesi için özel .NET etkinlik olarak dataset zincir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="7d3eb-521">Özel Etkinlik kodu bağlantılı hizmetin bağlantı dizesinde sonra erişebilir ve çalışma zamanında düzgün çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-521">You can then access the linked service's connection string in the custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-the-sample"></a><span data-ttu-id="7d3eb-522">Örnek genişletme</span><span class="sxs-lookup"><span data-stu-id="7d3eb-522">Extend the sample</span></span>
<span data-ttu-id="7d3eb-523">Azure Data Factory ve Azure Batch özellikleri hakkında daha fazla bilgi için bu örnek genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-523">You can extend this sample to learn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="7d3eb-524">Örneğin, farklı bir zaman aralığı dilimleri işlemek için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-524">For example, to process slices in a different time range, do the following steps:</span></span>

1. <span data-ttu-id="7d3eb-525">Aşağıdaki klasörlerdeki eklemek `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 ve Yerleştir bu klasörlerdeki girişi dosyaları.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-525">Add the following subfolders in the `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="7d3eb-526">Ardışık düzen tarafından bitiş zamanını değiştirin `2015-11-16T05:00:00Z` için `2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-526">Change the end time for the pipeline from `2015-11-16T05:00:00Z` to `2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="7d3eb-527">İçinde **diyagram görünümü**, çift **InputDataset**ve girdi dilimlerinin hazır olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-527">In the **Diagram View**, double-click the **InputDataset**, and confirm that the input slices are ready.</span></span> <span data-ttu-id="7d3eb-528">Çift **OuptutDataset** çıkış dilimler durumunu görmek için.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-528">Double-click **OuptutDataset** to see the state of output slices.</span></span> <span data-ttu-id="7d3eb-529">Hazır durumda olmaları durumunda çıkış dosyaları için çıkış klasörünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-529">If they are in Ready state, check the output folder for the output files.</span></span>
2. <span data-ttu-id="7d3eb-530">Artırma veya azaltma **eşzamanlılık** özellikle Azure Batch oluşan işleme çözümünüzün performansını nasıl etkilediği anlamak için ayarı.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-530">Increase or decrease the **concurrency** setting to understand how it affects the performance of your solution, especially the processing that occurs on Azure Batch.</span></span> <span data-ttu-id="7d3eb-531">(Bkz. adım 4: oluşturun ve daha fazla bilgi için ardışık düzen çalıştıracağınız **eşzamanlılık** ayarı.)</span><span class="sxs-lookup"><span data-stu-id="7d3eb-531">(See Step 4: Create and run the pipeline for more on the **concurrency** setting.)</span></span>
3. <span data-ttu-id="7d3eb-532">Küçük daha yüksek bir havuz oluşturma **maksimum VM başına görevleri**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="7d3eb-533">Oluşturduğunuz yeni havuzu kullanmak için veri fabrikası çözüm bağlı Azure Batch hizmetinde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-533">To use the new pool you created, update the Azure Batch linked service in the Data Factory solution.</span></span> <span data-ttu-id="7d3eb-534">(Bkz. adım 4: oluşturun ve daha fazla bilgi için ardışık düzen çalıştırmak **maksimum VM başına görevleri** ayarı.)</span><span class="sxs-lookup"><span data-stu-id="7d3eb-534">(See Step 4: Create and run the pipeline for more on the **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="7d3eb-535">Bir Azure Batch havuzu oluşturma **otomatik ölçeklendirme** özelliği.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="7d3eb-536">Bir Azure Batch havuzunda işlem düğümlerini otomatik olarak ölçeklendirme, uygulamanız tarafından kullanılan güç işleme dinamik ayarlanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-536">Automatically scaling compute nodes in an Azure Batch pool is the dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="7d3eb-537">Formül örneği burada aşağıdaki davranışı elde eder: havuzu başlangıçta oluşturulduğunda 1 VM ile başlar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-537">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="7d3eb-538">$PendingTasks ölçüm tanımlar görev sayısı çalışan + (kuyruğa alınmış) etkin durumu.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-538">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="7d3eb-539">Formül Son 180 saniye içinde görevleri bekleyen ortalama sayısı bulur ve TargetDedicated uygun şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-539">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="7d3eb-540">TargetDedicated hiçbir zaman 25 VM'ler gider sağlar.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="7d3eb-541">Bu nedenle, yeni görevler gönderildiği haliyle havuzu otomatik olarak büyür ve görevler tamamlanınca VM'ler boş bir birer birer hale ve bu sanal makineleri otomatik ölçeklendirmeyi küçültür.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="7d3eb-542">startingNumberOfVMs ve maxNumberofVMs gereksinimlerinize göre ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-542">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>
 
    <span data-ttu-id="7d3eb-543">Otomatik ölçeklendirme formülü:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="7d3eb-544">Bkz: [ölçek işlem düğümlerini Azure Batch havuzunda otomatik olarak](../batch/batch-automatic-scaling.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="7d3eb-545">Varsayılan havuzu kullanıyorsanız [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), Batch hizmeti VM özel etkinlik çalıştırmadan önce hazırlamak için 15-30 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-545">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="7d3eb-546">Havuz farklı autoScaleEvaluationInterval kullanıyorsanız, Batch hizmeti autoScaleEvaluationInterval + 10 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-546">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="7d3eb-547">Örnek çözümde **yürütme** yöntemini çağırır **Hesapla** bir çıktı veri dilimi üretmek için bir giriş veri dilimi işleyen yöntem.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-547">In the sample solution, the **Execute** method invokes the **Calculate** method that processes an input data slice to produce an output data slice.</span></span> <span data-ttu-id="7d3eb-548">Girdi verilerini işlemek ve yönteminizi çağrısıyla yürütme yönteminin hesapla yöntem çağrısında değiştirmek için kendi yönteminizi yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-548">You can write your own method to process input data and replace the Calculate method call in the Execute method with a call to your method.</span></span>

### <a name="next-steps-consume-the-data"></a><span data-ttu-id="7d3eb-549">Sonraki adımlar: verileri kullanmak</span><span class="sxs-lookup"><span data-stu-id="7d3eb-549">Next steps: Consume the data</span></span>
<span data-ttu-id="7d3eb-550">Veri işleme sonra onu gibi çevrimiçi araçlarla tüketebileceği **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="7d3eb-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="7d3eb-551">Power BI ve Azure'da kullanma anlamanıza yardımcı olması için bağlantılar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7d3eb-551">Here are links to help you understand Power BI and how to use it in Azure:</span></span>

* [<span data-ttu-id="7d3eb-552">Power BI kümesinde keşfedin</span><span class="sxs-lookup"><span data-stu-id="7d3eb-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="7d3eb-553">Power BI Desktop kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7d3eb-553">Getting started with the Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="7d3eb-554">Power bı'da veri yenileme</span><span class="sxs-lookup"><span data-stu-id="7d3eb-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="7d3eb-555">Azure ve Power BI - temel genel bakış</span><span class="sxs-lookup"><span data-stu-id="7d3eb-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="7d3eb-556">Başvurular</span><span class="sxs-lookup"><span data-stu-id="7d3eb-556">References</span></span>
* [<span data-ttu-id="7d3eb-557">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7d3eb-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="7d3eb-558">Azure Data Factory Hizmeti'ne Giriş</span><span class="sxs-lookup"><span data-stu-id="7d3eb-558">Introduction to Azure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="7d3eb-559">Azure Data Factory ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7d3eb-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="7d3eb-560">Bir Azure Data Factory işlem hattında özel etkinlikler kullanma</span><span class="sxs-lookup"><span data-stu-id="7d3eb-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="7d3eb-561">Azure toplu işlem</span><span class="sxs-lookup"><span data-stu-id="7d3eb-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="7d3eb-562">Azure Batch temel bilgileri</span><span class="sxs-lookup"><span data-stu-id="7d3eb-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="7d3eb-563">Azure Batch özelliklerine genel bakış</span><span class="sxs-lookup"><span data-stu-id="7d3eb-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="7d3eb-564">Azure portalında Azure Batch hesabı oluşturabilir ve yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7d3eb-564">Create and manage Azure Batch account in the Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="7d3eb-565">Azure Batch kitaplığını .NET ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="7d3eb-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
