---
title: "Veri Fabrikası ve toplu işlemi kullanarak aaaProcess büyük ölçekli veri kümeleri | Microsoft Docs"
description: "Azure Batch paralel işleme yeteneğini kullanarak tooprocess büyük miktarlarda verinin bir Azure Data factory'de nasıl kanal açıklar."
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
ms.openlocfilehash: 6788f02de555d2e9d6588cc990a39043866d7e97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="84e8b-103">Data Factory ve Batch kullanarak büyük ölçekli veri kümelerini işleme</span><span class="sxs-lookup"><span data-stu-id="84e8b-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="84e8b-104">Bu makalede bir taşır ve büyük ölçekli veri kümeleri otomatik ve zamanlanmış bir şekilde işleyen örnek bir çözüm mimarisini açıklar.</span><span class="sxs-lookup"><span data-stu-id="84e8b-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="84e8b-105">Ayrıca, Azure Data Factory ve Azure Batch kullanarak bir uçtan uca kılavuz tooimplement hello çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="84e8b-105">It also provides an end-to-end walkthrough tooimplement hello solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="84e8b-106">Bu makalede bizim tipik makale uzun çünkü tüm örnek çözümünü bir kılavuz içerir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="84e8b-107">Bu hizmetler hakkında bilgi edinebilirsiniz yeni tooBatch ve Data Factory varsa ve nasıl birlikte çalışır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-107">If you are new tooBatch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="84e8b-108">Bir şey hello hizmetleri hakkında bilmeniz ve tasarlama/çözüm mimarisi oluşturma, yalnızca hello üzerinde odaklanmak [mimarisi bölümüne](#architecture-of-sample-solution) hello makale ve prototip ya da bir çözüm geliştirme varsa, da tootry isteyebilirsiniz Merhaba içindeki adım adım yönergeleri [izlenecek](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="84e8b-108">If you know something about hello services and are designing/architecting a solution, you may focus just on hello [architecture section](#architecture-of-sample-solution) of hello article and if you are developing a prototype or a solution, you may also want tootry out step-by-step instructions in hello [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="84e8b-109">Bu içerik ve bunu nasıl kullandığı hakkında yorumlarınızı davet ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="84e8b-110">İlk olarak, nasıl veri fabrikası ve toplu işlem Hizmetleri ile Merhaba bulut büyük veri kümelerinde işleme yardımcı olabilir bakalım.</span><span class="sxs-lookup"><span data-stu-id="84e8b-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in hello cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="84e8b-111">Neden Azure toplu işlem?</span><span class="sxs-lookup"><span data-stu-id="84e8b-111">Why Azure Batch?</span></span>
<span data-ttu-id="84e8b-112">Azure Batch toorun büyük ölçekli paralel ve yüksek performanslı) bilgi işlem (HPC uygulamaları hello bulutta verimli bir şekilde etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-112">Azure Batch enables you toorun large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="84e8b-113">Sanal makineler yönetilen koleksiyonu üzerinde işlem yoğunluklu iş toorun zamanlar bir platform hizmetidir ve ölçek kaynakları toomeet hello işleriniz ihtiyaçlarını işlem otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="84e8b-113">It's a platform service that schedules compute-intensive work toorun on a managed collection of virtual machines, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span>

<span data-ttu-id="84e8b-114">Merhaba Batch hizmeti, Azure işlem kaynakları tooexecute uygulamalarınızı paralel olarak ve ölçekte tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="84e8b-114">With hello Batch service, you define Azure compute resources tooexecute your applications in parallel, and at scale.</span></span> <span data-ttu-id="84e8b-115">İsteğe bağlı veya zamanlanmış çalıştırabilirsiniz işler ve toomanually gerekmez oluşturmak, yapılandırmak ve HPC Kümesi, tek tek sanal makineleri, sanal ağlar veya karmaşık iş yönetmek ve görev zamanlama altyapısını.</span><span class="sxs-lookup"><span data-stu-id="84e8b-115">You can run on-demand or scheduled jobs, and you don't need toomanually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="84e8b-116">Bu makalede açıklanan hello çözümünü hello mimarisi/uygulaması anlamaya yardımcı olması gibi Azure Batch ile bilmiyorsanız makaleleri aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-116">See hello following articles if you are not familiar with Azure Batch as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>   

* [<span data-ttu-id="84e8b-117">Azure Batch temel bilgileri</span><span class="sxs-lookup"><span data-stu-id="84e8b-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="84e8b-118">Batch özelliklerine genel bakış</span><span class="sxs-lookup"><span data-stu-id="84e8b-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="84e8b-119">(isteğe bağlı) toolearn Azure Batch hakkında daha fazla bilgi görmek hello [için Azure Batch öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="84e8b-119">(optional) toolearn more about Azure Batch, see hello [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="84e8b-120">Neden Azure Data Factory?</span><span class="sxs-lookup"><span data-stu-id="84e8b-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="84e8b-121">Veri Fabrikası düzenler ve hello taşınmasını ve dönüştürülmesini veri otomatikleştiren bir bulut tabanlı veri tümleştirme hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-121">Data Factory is a cloud-based data integration service that orchestrates and automates hello movement and transformation of data.</span></span> <span data-ttu-id="84e8b-122">Merhaba Data Factory hizmeti kullanıldığında, şirket içi veri taşıma ve bulut veri depoları tooa merkezi veri deposu yönetilen veri ardışık oluşturabilirsiniz (örneğin: Azure Blob Storage) ve işlem/dönüştürme Azure Hdınsight ve Azure gibi hizmetleri kullanarak verileri Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="84e8b-122">Using hello Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores tooa centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="84e8b-123">Veri ardışık düzen toorun zamanlanmış şekilde (saatlik, günlük, haftalık, vb.) ve İzleyicisi'nde zamanlayabilir ve bir bakışta tooidentify sorunu yönetmek ve eylemi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="84e8b-123">You can also schedule data pipelines toorun in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance tooidentify issues and take action.</span></span>

<span data-ttu-id="84e8b-124">Bu makalede açıklanan hello çözümünü hello mimarisi/uygulaması anlamaya yardımcı olması gibi Azure Data Factory ile bilmiyorsanız makaleleri aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-124">See hello following articles if you are not familiar with Azure Data Factory as it helps with understanding hello architecture/implementation of hello solution described in this article.</span></span>  

* [<span data-ttu-id="84e8b-125">Azure Data Factory giriş</span><span class="sxs-lookup"><span data-stu-id="84e8b-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="84e8b-126">İlk veri hattınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e8b-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="84e8b-127">(isteğe bağlı) toolearn Azure Data Factory hakkında daha fazla bilgi görmek hello [Azure Data Factory öğrenme yolu](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="84e8b-127">(optional) toolearn more about Azure Data Factory, see hello [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="84e8b-128">Veri Fabrikası ve birlikte toplu işlem</span><span class="sxs-lookup"><span data-stu-id="84e8b-128">Data Factory and Batch together</span></span>
<span data-ttu-id="84e8b-129">Veri Fabrikası tooa hedef veri deposuna ve Hive etkinliği tooprocess verilerini Azure üzerinde Hadoop kümeleri (Hdınsight) kullanarak kopyalama etkinliği toocopy/taşıma veri kaynağına veri depolamak gibi yerleşik etkinlikler içerir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-129">Data Factory includes built-in activities such as Copy Activity toocopy/move data from a source data store tooa destination data store and Hive Activity tooprocess data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="84e8b-130">Bkz: [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) desteklenen dönüştürme etkinliklerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="84e8b-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="84e8b-131">Ayrıca, toocreate özel .NET etkinliklerini kendi mantığınızı toomove ya da işlem verilerle sağlar ve bu etkinlikler Azure Hdınsight kümesinde veya bir Azure Batch havuzunda VM'lerin çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-131">It also allows you toocreate custom .NET activities toomove or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="84e8b-132">Azure Batch kullandığınızda hello havuzu tooauto ölçekli yapılandırabilirsiniz (ekleyip hello iş yüküne göre VM'ler) sağladığınız bir formüle dayanarak.</span><span class="sxs-lookup"><span data-stu-id="84e8b-132">When you use Azure Batch, you can configure hello pool tooauto-scale (add or remove VMs based on hello workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="84e8b-133">Örnek çözümü mimarisi</span><span class="sxs-lookup"><span data-stu-id="84e8b-133">Architecture of sample solution</span></span>
<span data-ttu-id="84e8b-134">Bu makalede açıklanan hello mimarisi için basit bir çözüm olsa da, finansal hizmetler, görüntü işleme ve işleme ve genomic analiz tarafından modelleme risk gibi ilgili toocomplex senaryoları olur.</span><span class="sxs-lookup"><span data-stu-id="84e8b-134">Even though hello architecture described in this article is for a simple solution, it is relevant toocomplex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="84e8b-135">Merhaba diyagram gösterir; 1) nasıl Data Factory veri taşıma düzenler ve işleme ve Azure Batch 2) nasıl işlediği hello verileri paralel bir biçimde.</span><span class="sxs-lookup"><span data-stu-id="84e8b-135">hello diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes hello data in a parallel manner.</span></span> <span data-ttu-id="84e8b-136">Karşıdan yükleme ve kolay başvuru (11 x 17 inç yazdırma hello diyagramı.</span><span class="sxs-lookup"><span data-stu-id="84e8b-136">Download and print hello diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="84e8b-137">veya A3 boyutu): [Azure Batch ve Data Factory kullanarak HPC ve veriler orchestration](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="84e8b-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="84e8b-138">[![Büyük ölçekli veri işleme diyagramı](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="84e8b-138">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="84e8b-139">Merhaba aşağıdaki listede hello işleminin hello temel adımları sağlar.</span><span class="sxs-lookup"><span data-stu-id="84e8b-139">hello following list provides hello basic steps of hello process.</span></span> <span data-ttu-id="84e8b-140">Merhaba çözüm toobuild hello uçtan uca çözüm kodu ve açıklamaları içerir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-140">hello solution includes code and explanations toobuild hello end-to-end solution.</span></span>

1. <span data-ttu-id="84e8b-141">**Azure Batch (VM'ler) işlem düğümlerinin bir havuzuyla yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="84e8b-142">Merhaba düğüm sayısını ve her düğümün boyutu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-142">You can specify hello number of nodes and size of each node.</span></span>
2. <span data-ttu-id="84e8b-143">**Azure Data Factory örneğini oluşturabilir** Azure blob depolama, Azure toplu işlem hizmeti, girdi/çıktı verilerini ve iş akışı/ardışık taşıyın ve veri dönüştürme etkinlikleri ile temsil eden varlık ile yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="84e8b-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="84e8b-144">**Özel bir .NET etkinliği hello Data Factory işlem hattı oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-144">**Create a custom .NET activity in hello Data Factory pipeline**.</span></span> <span data-ttu-id="84e8b-145">Merhaba, hello Azure Batch havuzu üzerinde çalışır, kullanıcı kodu etkinliktir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-145">hello activity is your user code that runs on hello Azure Batch pool.</span></span>
4. <span data-ttu-id="84e8b-146">**Azure depolama alanında bloblar büyük miktarlarda giriş veri depolamak**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="84e8b-147">Veriler (genellikle zamanına göre) mantıksal dilimlere bölünür.</span><span class="sxs-lookup"><span data-stu-id="84e8b-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="84e8b-148">**Veri Fabrikası paralel olarak işlenir verileri kopyalar** toohello ikincil konum.</span><span class="sxs-lookup"><span data-stu-id="84e8b-148">**Data Factory copies data that is processed in parallel** toohello secondary location.</span></span>
6. <span data-ttu-id="84e8b-149">**Veri Fabrikası çalışan toplu işi tarafından ayrılan hello havuzunu kullanan hello özel etkinlik**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-149">**Data Factory runs hello custom activity using hello pool allocated by Batch**.</span></span> <span data-ttu-id="84e8b-150">Veri Fabrikası etkinlikleri birlikte çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="84e8b-151">Her etkinlik veri dilimini işler.</span><span class="sxs-lookup"><span data-stu-id="84e8b-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="84e8b-152">Merhaba sonuçları Azure depolama alanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-152">hello results are stored in Azure storage.</span></span>
7. <span data-ttu-id="84e8b-153">**Veri Fabrikası taşır hello son sonuçları tooa üçüncü konumunu**, bir uygulama aracılığıyla dağıtım için veya diğer araçları tarafından işlenmesi için.</span><span class="sxs-lookup"><span data-stu-id="84e8b-153">**Data Factory moves hello final results tooa third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="84e8b-154">Örnek çözümü uygulaması</span><span class="sxs-lookup"><span data-stu-id="84e8b-154">Implementation of sample solution</span></span>
<span data-ttu-id="84e8b-155">Merhaba örnek çözümü kasıtlı olarak basit ve tooshow, nasıl toouse Data Factory ve toplu birlikte tooprocess veri kümeleri.</span><span class="sxs-lookup"><span data-stu-id="84e8b-155">hello sample solution is intentionally simple and is tooshow you how toouse Data Factory and Batch together tooprocess datasets.</span></span> <span data-ttu-id="84e8b-156">Merhaba çözüm yalnızca hello bir arama terimi ("Microsoft") oluşumları bir zaman serisinin düzenlenmiş giriş dosyalarında sayar.</span><span class="sxs-lookup"><span data-stu-id="84e8b-156">hello solution simply counts hello number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="84e8b-157">Merhaba sayısı toooutput dosyalarını çıkarır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-157">It outputs hello count toooutput files.</span></span>

<span data-ttu-id="84e8b-158">**Zaman**: Azure, veri fabrikası ve Batch temelleri ile tanıdık ve tamamlanan hello Önkoşullar aşağıda listelenen sahip, bu çözüm alır 1-2 saat toocomplete tahmin ediyoruz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed hello prerequisites listed below, we estimate this solution takes 1-2 hours toocomplete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="84e8b-159">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="84e8b-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="84e8b-160">Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="84e8b-160">Azure subscription</span></span>
<span data-ttu-id="84e8b-161">Bir Azure aboneliğiniz yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="84e8b-162">Bkz: [ücretsiz deneme sürümü](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="84e8b-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="84e8b-163">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="84e8b-163">Azure storage account</span></span>
<span data-ttu-id="84e8b-164">Bu öğreticide hello verileri depolamak için bir Azure depolama hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-164">You use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="84e8b-165">Bir Azure depolama hesabınız yoksa bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="84e8b-165">If you don't have an Azure storage account, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="84e8b-166">Merhaba örnek çözümü blob depolama kullanır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-166">hello sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="84e8b-167">Azure toplu işlem hesabı</span><span class="sxs-lookup"><span data-stu-id="84e8b-167">Azure Batch account</span></span>
<span data-ttu-id="84e8b-168">Hello kullanarak bir Azure Batch hesabı oluşturma [Azure portal](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="84e8b-168">Create an Azure Batch account using hello [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="84e8b-169">Bkz: [oluşturma ve bir Azure Batch hesabını yönetmek](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="84e8b-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="84e8b-170">Merhaba, Azure Batch hesabı adını ve hesap anahtarını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-170">Note hello Azure Batch account name and account key.</span></span> <span data-ttu-id="84e8b-171">Aynı zamanda [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate bir Azure Batch hesabı.</span><span class="sxs-lookup"><span data-stu-id="84e8b-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet toocreate an Azure Batch account.</span></span> <span data-ttu-id="84e8b-172">Bkz: [Azure Batch PowerShell cmdlet'leri kullanmaya başlama](../batch/batch-powershell-cmdlets-get-started.md) bu cmdlet'in kullanımı hakkında ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="84e8b-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="84e8b-173">Merhaba örnek çözümü Azure Batch (üzerinden dolaylı olarak bir Azure Data Factory işlem hattı) tooprocess verileri paralel şekilde havuzunda işlem düğümlerinin (sanal makineler yönetilen koleksiyonu) kullanır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-173">hello sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) tooprocess data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="84e8b-174">Azure Batch havuzundaki sanal makineler (VM'ler)</span><span class="sxs-lookup"><span data-stu-id="84e8b-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="84e8b-175">Oluşturma bir **Azure Batch havuzu** en az 2 ile işlem düğümleri.</span><span class="sxs-lookup"><span data-stu-id="84e8b-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="84e8b-176">Merhaba, [Azure portal](https://portal.azure.com), tıklatın **Gözat** hello soldaki menüden ve'ı tıklatın **toplu işlem hesaplarını**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-176">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="84e8b-177">Azure Batch hesabı tooopen hello seçin **toplu işlem hesabı** dikey.</span><span class="sxs-lookup"><span data-stu-id="84e8b-177">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
3. <span data-ttu-id="84e8b-178">Tıklatın **havuzları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="84e8b-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="84e8b-179">Merhaba, **havuzları** dikey penceresinde hello araç tooadd bir havuzu Ekle düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-179">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
   1. <span data-ttu-id="84e8b-180">Merhaba havuzu için bir kimlik girin (**havuzu kimliği**).</span><span class="sxs-lookup"><span data-stu-id="84e8b-180">Enter an ID for hello pool (**Pool ID**).</span></span> <span data-ttu-id="84e8b-181">Not hello **hello havuzun kimliği**; hello Data Factory çözüm oluşturulurken gerekir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-181">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
   2. <span data-ttu-id="84e8b-182">Belirtin **Windows Server 2012 R2** hello işletim sistemi ailesi ayarı için.</span><span class="sxs-lookup"><span data-stu-id="84e8b-182">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
   3. <span data-ttu-id="84e8b-183">Seçin bir **düğüm fiyatlandırma katmanı**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="84e8b-184">Girin **2** hello için değer olarak **hedef ayrılmış** ayarı.</span><span class="sxs-lookup"><span data-stu-id="84e8b-184">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="84e8b-185">Girin **2** hello için değer olarak **en fazla düğüm başına görevleri** ayarı.</span><span class="sxs-lookup"><span data-stu-id="84e8b-185">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="84e8b-186">Tıklatın **Tamam** toocreate hello havuzu.</span><span class="sxs-lookup"><span data-stu-id="84e8b-186">Click **OK** toocreate hello pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="84e8b-187">Azure Depolama Gezgini</span><span class="sxs-lookup"><span data-stu-id="84e8b-187">Azure Storage Explorer</span></span>
<span data-ttu-id="84e8b-188">[Azure Depolama Gezgini 6 (aracı)](https://azurestorageexplorer.codeplex.com/) veya [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (ClumsyLeaf yazılımından).</span><span class="sxs-lookup"><span data-stu-id="84e8b-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="84e8b-189">İnceleme veya bulutta barındırılan uygulamalarınızın hello günlükleri de dahil olmak üzere Azure Storage projelerinizi hello verileri değiştirme için bu araçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-189">You use these tools for inspecting and altering hello data in your Azure Storage projects including hello logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="84e8b-190">Adlı bir kapsayıcı oluşturmak **mycontainer** özel erişim (anonim erişimi yok)</span><span class="sxs-lookup"><span data-stu-id="84e8b-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="84e8b-191">Kullanıyorsanız **CloudXplorer**, klasörleri oluşturun ve alt klasörler ile Merhaba yapı izlenerek:</span><span class="sxs-lookup"><span data-stu-id="84e8b-191">If you are using **CloudXplorer**, create folders and subfolders with hello following structure:</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="84e8b-192">`Inputfolder`ve `outputfolder` en üst düzey klasörlerde bulunan `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="84e8b-192">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="84e8b-193">Merhaba `inputfolder` tarih-saat Damgalar (YYYY-AA-GG-ss) ile klasörleri varsa.</span><span class="sxs-lookup"><span data-stu-id="84e8b-193">hello `inputfolder` has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="84e8b-194">Kullanıyorsanız **Azure Storage Gezgini**, hello sonraki adımda adlara sahip tooupload dosyaları gerekir: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="84e8b-194">If you are using **Azure Storage Explorer**, in hello next step, you need tooupload files with names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt` and so on.</span></span> <span data-ttu-id="84e8b-195">Bu adım, hello klasörleri otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="84e8b-195">This step automatically creates hello folders.</span></span>
3. <span data-ttu-id="84e8b-196">Bir metin dosyası oluşturun **dosya.txt'yi** hello anahtar sözcüğü sahip içerikle makinenizde **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-196">Create a text file **file.txt** on your machine with content that has hello keyword **Microsoft**.</span></span> <span data-ttu-id="84e8b-197">Örneğin: "Özel Etkinlik Microsoft test özel etkinlik Microsoft test".</span><span class="sxs-lookup"><span data-stu-id="84e8b-197">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="84e8b-198">Azure blob depolama alanındaki giriş klasörleri aşağıdaki hello dosya toohello karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="84e8b-198">Upload hello file toohello following input folders in Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="84e8b-199">Kullanıyorsanız **Azure Storage Gezgini**, hello dosyayı karşıya yüklemeyi **dosya.txt'yi** çok**mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-199">If you are using **Azure Storage Explorer**, upload hello file **file.txt** too**mycontainer**.</span></span> <span data-ttu-id="84e8b-200">Tıklatın **kopyalama** hello araç toocreate hello blob bir kopyası üzerinde.</span><span class="sxs-lookup"><span data-stu-id="84e8b-200">Click **Copy** on hello toolbar toocreate a copy of hello blob.</span></span> <span data-ttu-id="84e8b-201">Merhaba, **kopyalama Blob** iletişim kutusu, değişiklik hello **hedef blob adı** çok`inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="84e8b-201">In hello **Copy Blob** dialog box, change hello **destination blob name** too`inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="84e8b-202">Bu adım toocreate yineleyin `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="84e8b-202">Repeat this step toocreate `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt` and so on.</span></span> <span data-ttu-id="84e8b-203">Bu eylemin hello klasörleri otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="84e8b-203">This action automatically creates hello folders.</span></span>
5. <span data-ttu-id="84e8b-204">Adlı başka bir kapsayıcı oluşturma: `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="84e8b-204">Create another container named: `customactivitycontainer`.</span></span> <span data-ttu-id="84e8b-205">Merhaba özel etkinlik ZIP dosyası toothis kapsayıcısı karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="84e8b-205">You upload hello custom activity zip file toothis container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="84e8b-206">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="84e8b-206">Visual Studio</span></span>
<span data-ttu-id="84e8b-207">Microsoft Visual Studio 2012 veya hello Data Factory çözüm kullanılan sonraki toocreate hello özel toplu iş etkinliği toobe yükleyin.</span><span class="sxs-lookup"><span data-stu-id="84e8b-207">Install Microsoft Visual Studio 2012 or later toocreate hello custom Batch activity toobe used in hello Data Factory solution.</span></span>

### <a name="high-level-steps-toocreate-hello-solution"></a><span data-ttu-id="84e8b-208">Üst düzey adımları toocreate hello çözümü</span><span class="sxs-lookup"><span data-stu-id="84e8b-208">High-level steps toocreate hello solution</span></span>
1. <span data-ttu-id="84e8b-209">Merhaba veri işleme mantığı içeren özel bir aktivite oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84e8b-209">Create a custom activity that contains hello data processing logic.</span></span>
2. <span data-ttu-id="84e8b-210">Merhaba özel etkinlik kullanan bir Azure data factory oluşturun:</span><span class="sxs-lookup"><span data-stu-id="84e8b-210">Create an Azure data factory that uses hello custom activity:</span></span>

### <a name="create-hello-custom-activity"></a><span data-ttu-id="84e8b-211">Merhaba özel etkinlik oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e8b-211">Create hello custom activity</span></span>
<span data-ttu-id="84e8b-212">Bu örnek çözümün hello Kalp Hello Data Factory özel etkinlik olur.</span><span class="sxs-lookup"><span data-stu-id="84e8b-212">hello Data Factory custom activity is hello heart of this sample solution.</span></span> <span data-ttu-id="84e8b-213">Merhaba örnek çözümü Azure Batch toorun hello özel etkinlik kullanır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-213">hello sample solution uses Azure Batch toorun hello custom activity.</span></span> <span data-ttu-id="84e8b-214">Bkz: [bir Azure Data Factory ardışık düzeninde özel etkinlikleri kullanmak](data-factory-use-custom-activities.md) hello temel bilgileri toodevelop özel etkinlikler ve kullanımı için bunları Azure Data Factory öğesinde ardışık düzenleri.</span><span class="sxs-lookup"><span data-stu-id="84e8b-214">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for hello basic information toodevelop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="84e8b-215">bir Azure Data Factory ardışık düzeninde kullanabileceğiniz bir .NET özel etkinlik toocreate, gereksinim duyduğunuz toocreate bir **.NET sınıf kitaplığı** uygulayan bir sınıf projeyle **IDotNetActivity** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="84e8b-215">toocreate a .NET custom activity that you can use in an Azure Data Factory pipeline, you need toocreate a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="84e8b-216">Bu arabirim yalnızca bir yöntemi vardır: **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-216">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="84e8b-217">Merhaba yöntemi hello imzası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="84e8b-217">Here is hello signature of hello method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="84e8b-218">Merhaba yöntemi toounderstand gereken birkaç anahtar bileşenleri içerir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-218">hello method has a few key components that you need toounderstand.</span></span>

* <span data-ttu-id="84e8b-219">Merhaba yöntemi dört parametreleri alır:</span><span class="sxs-lookup"><span data-stu-id="84e8b-219">hello method takes four parameters:</span></span>

  1. <span data-ttu-id="84e8b-220">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-220">**linkedServices**.</span></span> <span data-ttu-id="84e8b-221">Giriş/Çıkış veri kaynakları bağlantı bağlı hizmetler numaralandırılabilir bir listesini (örneğin: Azure Blob Storage) toohello veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="84e8b-221">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) toohello data factory.</span></span> <span data-ttu-id="84e8b-222">Bu örnekte, yalnızca bir bağlantılı hizmet türü girdi ve çıktı için kullanılan Azure Storage yok.</span><span class="sxs-lookup"><span data-stu-id="84e8b-222">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="84e8b-223">**veri kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-223">**datasets**.</span></span> <span data-ttu-id="84e8b-224">Bu veri kümeleri numaralandırılabilir bir listesidir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-224">This is an enumerable list of datasets.</span></span> <span data-ttu-id="84e8b-225">Bu parametre tooget hello konumları ve girdi ve çıktı veri kümeleri tarafından tanımlanan şemaları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-225">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="84e8b-226">**Etkinlik**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-226">**activity**.</span></span> <span data-ttu-id="84e8b-227">Bu parametre hello geçerli işlem varlık - bu durumda, bir Azure Batch hizmetini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="84e8b-227">This parameter represents hello current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="84e8b-228">**Günlükçü**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-228">**logger**.</span></span> <span data-ttu-id="84e8b-229">ardışık düzeni için "Kullanıcı" oturum hello olarak o yüzeyini hata ayıklama yorum yazmak hello Günlükçü sağlar hello.</span><span class="sxs-lookup"><span data-stu-id="84e8b-229">hello logger lets you write debug comments that surface as hello “User” log for hello pipeline.</span></span>
* <span data-ttu-id="84e8b-230">Merhaba yöntemi kullanılan toochain özel etkinlikler birlikte hello gelecekte olabilir bir sözlüğü döndürür.</span><span class="sxs-lookup"><span data-stu-id="84e8b-230">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="84e8b-231">Bu özellik henüz uygulanmadı, bu nedenle boş bir sözlük hello döndürme.</span><span class="sxs-lookup"><span data-stu-id="84e8b-231">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>

#### <a name="procedure-create-hello-custom-activity"></a><span data-ttu-id="84e8b-232">Yordam: hello özel etkinlik oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e8b-232">Procedure: Create hello custom activity</span></span>
1. <span data-ttu-id="84e8b-233">Visual Studio'da .NET sınıf kitaplığı proje oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84e8b-233">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="84e8b-234">Başlatma **Visual Studio 2012**/**2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-234">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="84e8b-235">Tıklatın **dosya**, çok noktası**yeni**, tıklatıp **proje**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-235">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="84e8b-236">Genişletme **şablonları**seçip **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-236">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="84e8b-237">Bu kılavuzda, kullandığınız C\#, ancak .NET dil toodevelop hello özel etkinlik kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-237">In this walkthrough, you use C\#, but you can use any .NET language toodevelop hello custom activity.</span></span>
   4. <span data-ttu-id="84e8b-238">Seçin **sınıf kitaplığı** hello sağ proje türlerinde hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="84e8b-238">Select **Class Library** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="84e8b-239">Girin **MyDotNetActivity** hello için **adı**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-239">Enter **MyDotNetActivity** for hello **Name**.</span></span>
   6. <span data-ttu-id="84e8b-240">Seçin **C:\\ADF** hello için **konumu**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-240">Select **C:\\ADF** for hello **Location**.</span></span> <span data-ttu-id="84e8b-241">Başlangıç klasörü oluşturmak **ADF** henüz yoksa.</span><span class="sxs-lookup"><span data-stu-id="84e8b-241">Create hello folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="84e8b-242">Tıklatın **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="84e8b-242">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="84e8b-243">Tıklatın **Araçları**, çok noktası**NuGet Paket Yöneticisi**, tıklatıp **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-243">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="84e8b-244">Merhaba, **Paket Yöneticisi Konsolu**, komut tooimport aşağıdaki hello yürütme **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-244">In hello **Package Manager Console**, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="84e8b-245">İçeri aktarma hello **Azure Storage** toohello projesinde NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="84e8b-245">Import hello **Azure Storage** NuGet package in toohello project.</span></span> <span data-ttu-id="84e8b-246">Bu örnekte hello Blob Depolama API kullandığından, bu paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-246">You need this package because you use hello Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="84e8b-247">Merhaba aşağıdakileri ekleyin **kullanarak** yönergeleri toohello kaynak hello proje dosyasında.</span><span class="sxs-lookup"><span data-stu-id="84e8b-247">Add hello following **using** directives toohello source file in hello project.</span></span>

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
6. <span data-ttu-id="84e8b-248">Değişiklik hello hello adını **ad alanı** çok**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-248">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="84e8b-249">Merhaba sınıfı Hello adı çok değiştirmek**MyDotNetActivity** ve hello türetilen **IDotNetActivity** arabirim aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="84e8b-249">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="84e8b-250">Uygulama (Ekle) hello **yürütme** hello yöntemi **IDotNetActivity** toohello arabirim **MyDotNetActivity** örnek kodu toohello yöntemi aşağıdaki sınıf ve kopyalama hello.</span><span class="sxs-lookup"><span data-stu-id="84e8b-250">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span> <span data-ttu-id="84e8b-251">Merhaba bkz [yöntemi Çalıştır](#execute-method) Bu yöntemde kullanılan hello mantığı için bir açıklama için bölüm.</span><span class="sxs-lookup"><span data-stu-id="84e8b-251">See hello [Execute Method](#execute-method) section for explanation for hello logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is hello only method of IDotNetActivity interface you must implement.
    /// In this sample, hello method invokes hello Calculate method tooperform hello core logic.  
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
    
       // using First method instead of Single since we are using hello same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // toocreate an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass hello connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize hello continuation token before using it in hello do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get hello list of input blobs from hello input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // Calculate method returns hello number of occurrences of
           // hello search term (“Microsoft”) in each blob associated
           // with hello data slice.
           //
           // definition of hello method is shown in hello next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob toohello folder: {0}", folderPath);
    
       // create a storage object for hello output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write hello name of hello file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload hello output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} toohello output blob", output);
       outputBlob.UploadText(output);
    
       // hello dictionary can be used toochain custom activities together in hello future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="84e8b-252">Yardımcı yöntemler toohello sınıfı aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="84e8b-252">Add hello following helper methods toohello class.</span></span> <span data-ttu-id="84e8b-253">Bu yöntemler hello tarafından çağrılan **yürütme** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="84e8b-253">These methods are invoked by hello **Execute** method.</span></span> <span data-ttu-id="84e8b-254">En önemlisi, hello **Hesapla** yöntemi her bir blob tekrarlanan hello kod yalıtır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-254">Most importantly, hello **Calculate** method isolates hello code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets hello folderPath value from hello input/output dataset.
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
    /// Gets hello fileName value from hello input/output dataset.
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
    /// Iterates through each blob (file) in hello folder, counts hello number of instances of search term in hello file,
    /// and prepares hello output text that is written toohello output blob.
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
               output += string.Format("{0} occurrences(s) of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="84e8b-255">Merhaba **GetFolderPath** yöntemi döndürür hello yolu toohello klasöründe bu hello dataset noktaları tooand hello **GetFileName** yöntemi dataset noktalarına hello hello blob/dosya hello adını döndürür.</span><span class="sxs-lookup"><span data-stu-id="84e8b-255">hello **GetFolderPath** method returns hello path toohello folder that hello dataset points tooand hello **GetFileName** method returns hello name of hello blob/file that hello dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="84e8b-256">Merhaba **Hesapla** yöntemi hesaplar hello anahtar sözcüğü örneklerinin sayısını **Microsoft** hello giriş dosyalarında (BLOB hello klasöründe).</span><span class="sxs-lookup"><span data-stu-id="84e8b-256">hello **Calculate** method calculates hello number of instances of keyword **Microsoft** in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="84e8b-257">Merhaba kodda sabit kodlanmış Hello arama terimi ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="84e8b-257">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>

1. <span data-ttu-id="84e8b-258">Merhaba projeyi derleyin.</span><span class="sxs-lookup"><span data-stu-id="84e8b-258">Compile hello project.</span></span> <span data-ttu-id="84e8b-259">Tıklatın **yapı** hello menüsüne ve ardından gelen **yapı çözümü**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-259">Click **Build** from hello menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="84e8b-260">Başlatma **Windows Explorer**ve çok gidin**bin\\hata ayıklama** veya **bin\\yayın** klasör yapısının hello türüne bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="84e8b-260">Launch **Windows Explorer**, and navigate too**bin\\debug** or **bin\\release** folder depending on hello type of build.</span></span>
3. <span data-ttu-id="84e8b-261">Zip dosyası oluşturun **MyDotNetActivity.zip** hello içindeki tüm hello ikili dosyaları içeren  **\\bin\\hata ayıklama** klasör.</span><span class="sxs-lookup"><span data-stu-id="84e8b-261">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello **\\bin\\Debug** folder.</span></span> <span data-ttu-id="84e8b-262">Tooinclude hello MyDotNetActivity isteyebilirsiniz. **pdb** bir hata oluştuğunda, hello soruna neden hello kaynak kodunda satır numarası gibi ek ayrıntıları almak için dosya.</span><span class="sxs-lookup"><span data-stu-id="84e8b-262">You may want tooinclude hello MyDotNetActivity.**pdb** file so that you get additional details such as line number in hello source code that caused hello issue when a failure occurs.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="84e8b-263">Karşıya yükleme **MyDotNetActivity.zip** blob toohello blob kapsayıcı olarak: `customactivitycontainer` bu hello hello Azure blob depolama **StorageLinkedService** bağlı hello hizmetinde  **ADFTutorialDataFactory** kullanır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-263">Upload **MyDotNetActivity.zip** as a blob toohello blob container: `customactivitycontainer` in hello Azure blob storage that hello **StorageLinkedService** linked service in hello **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="84e8b-264">Merhaba blob kapsayıcı oluşturun `customactivitycontainer` zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="84e8b-264">Create hello blob container `customactivitycontainer` if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="84e8b-265">Execute yöntemi</span><span class="sxs-lookup"><span data-stu-id="84e8b-265">Execute method</span></span>
<span data-ttu-id="84e8b-266">Bu bölümde daha fazla ayrıntı ve hello yürütme yönteminin hello kodda hakkında notlar sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-266">This section provides more details and notes about hello code in hello Execute method.</span></span>

1. <span data-ttu-id="84e8b-267">Merhaba giriş koleksiyonu yineleme için hello üyeleri hello bulunduğunda [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) ad alanı.</span><span class="sxs-lookup"><span data-stu-id="84e8b-267">hello members for iterating through hello input collection are found in hello [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="84e8b-268">Merhaba blob koleksiyonu yineleme yapma gerektirir hello kullanarak **BlobContinuationToken** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="84e8b-268">Iterating through hello blob collection requires using hello **BlobContinuationToken** class.</span></span> <span data-ttu-id="84e8b-269">Esas olarak, bir kullanın-while döngüsünü hello döngüden çıkma için hello mekanizması olarak hello belirteci ile.</span><span class="sxs-lookup"><span data-stu-id="84e8b-269">In essence, you must use a do-while loop with hello token as hello mechanism for exiting hello loop.</span></span> <span data-ttu-id="84e8b-270">Daha fazla bilgi için bkz: [nasıl toouse Blob depolama alanından .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="84e8b-270">For more information, see [How toouse Blob storage from .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="84e8b-271">Temel bir döngü burada gösterilir:</span><span class="sxs-lookup"><span data-stu-id="84e8b-271">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize hello continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get hello list of input blobs from hello input storage client object.
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
   <span data-ttu-id="84e8b-272">Merhaba Hello belgelerine bakın [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) Ayrıntılar için yöntem.</span><span class="sxs-lookup"><span data-stu-id="84e8b-272">See hello documentation for hello [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="84e8b-273">Merhaba kod içinde hello gider BLOB'lar hello kümesi aracılığıyla mantıksal olarak çalışmak için yapın-while döngüsünü.</span><span class="sxs-lookup"><span data-stu-id="84e8b-273">hello code for working through hello set of blobs logically goes within hello do-while loop.</span></span> <span data-ttu-id="84e8b-274">Merhaba, **yürütme** yöntemi, hello-döngü BLOB'lar hello listesi adlı tooa yöntemi geçirir **Hesapla**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-274">In hello **Execute** method, hello do-while loop passes hello list of blobs tooa method named **Calculate**.</span></span> <span data-ttu-id="84e8b-275">Merhaba yöntemi döndürür adlı bir dize değişkeni **çıkış** hello kesimindeki tüm hello BLOB'lar aracılığıyla yinelendiğinde başka bir deyişle hello sonucu.</span><span class="sxs-lookup"><span data-stu-id="84e8b-275">hello method returns a string variable named **output** that is hello result of having iterated through all hello blobs in hello segment.</span></span>

   <span data-ttu-id="84e8b-276">Merhaba arama terimi oluşumları hello sayısını döndürür (**Microsoft**) hello blob toohello geçirilen **Hesapla** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="84e8b-276">It returns hello number of occurrences of hello search term (**Microsoft**) in hello blob passed toohello **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of hello search term \"{1}\" were found in hello file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="84e8b-277">Bir kez hello **Hesapla** yöntemi hello iş Bitti, bu tooa yeni blob yazılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-277">Once hello **Calculate** method has done hello work, it must be written tooa new blob.</span></span> <span data-ttu-id="84e8b-278">Bu nedenle her işlenen BLOB'lar kümesi için yeni blob hello sonuçlarıyla yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-278">So for every set of blobs processed, a new blob can be written with hello results.</span></span> <span data-ttu-id="84e8b-279">toowrite tooa yeni blob, Bul hello ilk çıkış veri kümesi.</span><span class="sxs-lookup"><span data-stu-id="84e8b-279">toowrite tooa new blob, first find hello output dataset.</span></span>

    ```csharp
    // Get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="84e8b-280">Merhaba kod de yardımcı yöntemini çağırır: **GetFolderPath** tooretrieve hello klasör yolu (Merhaba depolama kapsayıcısı adı).</span><span class="sxs-lookup"><span data-stu-id="84e8b-280">hello code also calls a helper method: **GetFolderPath** tooretrieve hello folder path (hello storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="84e8b-281">Merhaba **GetFolderPath** atamaları hello veri kümesi nesnesi tooan FolderPath adlı bir özellik olan AzureBlobDataSet.</span><span class="sxs-lookup"><span data-stu-id="84e8b-281">hello **GetFolderPath** casts hello DataSet object tooan AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="84e8b-282">Merhaba kod çağrıları hello **GetFileName** yöntemi tooretrieve hello dosya adı (blob adı).</span><span class="sxs-lookup"><span data-stu-id="84e8b-282">hello code calls hello **GetFileName** method tooretrieve hello file name (blob name).</span></span> <span data-ttu-id="84e8b-283">Merhaba, kod tooget hello klasör yolu yukarıda benzer toohello kodudur.</span><span class="sxs-lookup"><span data-stu-id="84e8b-283">hello code is similar toohello above code tooget hello folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="84e8b-284">bir URI nesnesinden oluşturarak hello dosyasının Hello adı yazılır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-284">hello name of hello file is written by creating a URI object.</span></span> <span data-ttu-id="84e8b-285">Merhaba URI Oluşturucusu kullanan hello **BlobEndpoint** özelliği tooreturn hello kapsayıcı adı.</span><span class="sxs-lookup"><span data-stu-id="84e8b-285">hello URI constructor uses hello **BlobEndpoint** property tooreturn hello container name.</span></span> <span data-ttu-id="84e8b-286">Merhaba klasör yolu ve dosya adı tooconstruct hello çıkış blob URI'si eklenir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-286">hello folder path and file name are added tooconstruct hello output blob URI.</span></span>  

    ```csharp
    // Write hello name of hello file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="84e8b-287">Merhaba dosyasının Hello adı yazılmış ve şimdi hello hello çıkış dizesi yazabilirsiniz **Hesapla** yöntemi tooa yeni blob:</span><span class="sxs-lookup"><span data-stu-id="84e8b-287">hello name of hello file has been written and now you can write hello output string from hello **Calculate** method tooa new blob:</span></span>

    ```csharp
    // Create a blob and upload hello output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} toohello output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-hello-data-factory"></a><span data-ttu-id="84e8b-288">Merhaba veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e8b-288">Create hello data factory</span></span>
<span data-ttu-id="84e8b-289">Merhaba, [hello özel etkinlik oluşturmak](#create-the-custom-activity) bölümünde oluşturduğunuz özel etkinlik ve karşıya yüklenen hello zip dosyasıyla ikili dosyaları ve hello PDB dosya tooan Azure blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="84e8b-289">In hello [Create hello custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded hello zip file with binaries and hello PDB file tooan Azure blob container.</span></span> <span data-ttu-id="84e8b-290">Bu bölümde, oluşturduğunuz Azure **veri fabrikası** ile bir **ardışık düzen** hello kullanan **özel etkinlik**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-290">In this section, you create an Azure **data factory** with a **pipeline** that uses hello **custom activity**.</span></span>

<span data-ttu-id="84e8b-291">Merhaba girdi veri kümesi hello özel etkinlik hello BLOB'ları (dosyaları) hello giriş klasöründe gösterir (`mycontainer\\inputfolder`) blob depolama.</span><span class="sxs-lookup"><span data-stu-id="84e8b-291">hello input dataset for hello custom activity represents hello blobs (files) in hello input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="84e8b-292">Merhaba çıkış veri kümesi hello çıkış BLOB'lar hello çıkış klasöründe hello etkinliği gösterir (`mycontainer\\outputfolder`) blob depolama.</span><span class="sxs-lookup"><span data-stu-id="84e8b-292">hello output dataset for hello activity represents hello output blobs in hello output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="84e8b-293">Bir veya daha fazla hello giriş klasörlerde bırak:</span><span class="sxs-lookup"><span data-stu-id="84e8b-293">Drop one or more files in hello input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="84e8b-294">Örneğin, içeriği her hello klasörler aşağıdaki hello ile bir dosya (dosya.txt'yi) bırakın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-294">For example, drop one file (file.txt) with hello following content into each of hello folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="84e8b-295">Başlangıç klasörü 2 veya daha fazla dosya olsa bile her giriş klasörü Azure Data Factory tooa dilimi karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-295">Each input folder corresponds tooa slice in Azure Data Factory even if hello folder has 2 or more files.</span></span> <span data-ttu-id="84e8b-296">Her dilim hello ardışık düzen tarafından işlendiğinde hello özel etkinlik bu dilim için hello giriş klasöründeki tüm hello BLOB'lar dolaşır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-296">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="84e8b-297">Beş çıktı hello ile aynı içerik dosyaları bakın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-297">You see five output files with hello same content.</span></span> <span data-ttu-id="84e8b-298">Örneğin, hello 2015-11-16-00 klasöründeki hello dosyasını işlemesini hello çıktı dosyası içeriği aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="84e8b-298">For example, hello output file from processing hello file in hello 2015-11-16-00 folder has hello following content:</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="84e8b-299">Birden çok dosya (dosya.txt'yi, file2.txt, file3.txt) düşüş hello ile aynı toohello giriş klasörü içerik, içerik hello çıktı dosyasında aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-299">If you drop multiple files (file.txt, file2.txt, file3.txt) with hello same content toohello input folder, you see hello following content in hello output file.</span></span> <span data-ttu-id="84e8b-300">Her bir klasör (2015-11-16-00, vb.) birden fazla girdi dosyası hello klasörü olmasına rağmen bu örnekteki tooa dilim karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-300">Each folder (2015-11-16-00, etc.) corresponds tooa slice in this sample even though hello folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="84e8b-301">Merhaba çıktı dosyası üç satır artık, her girdi dosyasında (blob) hello dilim (2015-11-16-00) ile ilişkilendirilmiş hello klasör için bir tane var.</span><span class="sxs-lookup"><span data-stu-id="84e8b-301">hello output file has three lines now, one for each input file (blob) in hello folder associated with hello slice (2015-11-16-00).</span></span>

<span data-ttu-id="84e8b-302">Bir görev çalıştırmak her etkinlik için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="84e8b-302">A task is created for each activity run.</span></span> <span data-ttu-id="84e8b-303">Bu örnekte, hello ardışık düzeninde yalnızca bir etkinlik yok.</span><span class="sxs-lookup"><span data-stu-id="84e8b-303">In this sample, there is only one activity in hello pipeline.</span></span> <span data-ttu-id="84e8b-304">Bir dilim hello ardışık düzen tarafından işlendiğinde hello özel etkinlik Azure Batch tooprocess hello dilim üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-304">When a slice is processed by hello pipeline, hello custom activity runs on Azure Batch tooprocess hello slice.</span></span> <span data-ttu-id="84e8b-305">Beş dilimleri (her dilim birden çok BLOB veya dosya olabilir) olduğundan, Azure Batch oluşturulan beş görevler vardır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-305">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="84e8b-306">Bir görev toplu olarak çalıştığında, onu çalıştıran gerçekte hello özel etkinliktir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-306">When a task runs on Batch, it is actually hello custom activity that is running.</span></span>

<span data-ttu-id="84e8b-307">izlenecek yol aşağıdaki hello ek ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="84e8b-307">hello following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="84e8b-308">1. adım: hello veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e8b-308">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="84e8b-309">İçinde toohello oturum sonra [Azure portal](https://portal.azure.com/), adımları hello:</span><span class="sxs-lookup"><span data-stu-id="84e8b-309">After logging in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>

   1. <span data-ttu-id="84e8b-310">Tıklatın **yeni** hello sol menüdeki.</span><span class="sxs-lookup"><span data-stu-id="84e8b-310">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="84e8b-311">Tıklatın **veri + analiz** hello içinde **yeni** dikey.</span><span class="sxs-lookup"><span data-stu-id="84e8b-311">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="84e8b-312">Tıklatın **Data Factory** hello üzerinde **veri analizi** dikey.</span><span class="sxs-lookup"><span data-stu-id="84e8b-312">Click **Data Factory** on hello **Data analytics** blade.</span></span>
2. <span data-ttu-id="84e8b-313">Merhaba, **yeni data factory** dikey penceresinde girin **CustomActivityFactory** hello adı için.</span><span class="sxs-lookup"><span data-stu-id="84e8b-313">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="84e8b-314">Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-314">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="84e8b-315">Merhaba hatayı alırsanız: **veri fabrikası adı "CustomActivityFactory" kullanılabilir değil**, hello veri fabrikası hello adını değiştirin (örneğin, **yournameCustomActivityFactory**) ve oluşturmayı deneyin yeniden.</span><span class="sxs-lookup"><span data-stu-id="84e8b-315">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="84e8b-316">Tıklatın **kaynak grubu adı**, varolan bir kaynak grubu seçin veya bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84e8b-316">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="84e8b-317">Merhaba doğru abonelikte ve bölgede oluşturulan hello veri fabrikası toobe istediğiniz kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="84e8b-317">Verify that you are using hello correct subscription and region where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="84e8b-318">Tıklatın **oluşturma** hello üzerinde **yeni data factory** dikey.</span><span class="sxs-lookup"><span data-stu-id="84e8b-318">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="84e8b-319">Hello oluşturulmakta hello veri fabrikası gördüğünüz **Pano** hello Azure portal.</span><span class="sxs-lookup"><span data-stu-id="84e8b-319">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="84e8b-320">Merhaba veri fabrikası başarıyla oluşturulduktan sonra gösterir hello veri fabrikası sayfasına bakın hello hello data Factory içeriği.</span><span class="sxs-lookup"><span data-stu-id="84e8b-320">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="84e8b-321">2. adım: bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e8b-321">Step 2: Create linked services</span></span>
<span data-ttu-id="84e8b-322">Bağlı hizmetler veri depolarını veya hizmetleri tooan Azure data factory işlem.</span><span class="sxs-lookup"><span data-stu-id="84e8b-322">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="84e8b-323">Bu adımda, bağlantı, **Azure Storage** hesabı ve **Azure Batch** hesap tooyour veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="84e8b-323">In this step, you link your **Azure Storage** account and **Azure Batch** account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="84e8b-324">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e8b-324">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="84e8b-325">Merhaba tıklatın **yazar ve dağıtma** döşeme hello üzerinde **DATA FACTORY** dikey **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-325">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="84e8b-326">Merhaba Data Factory Düzenleyici bakın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-326">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="84e8b-327">Tıklatın **yeni veri deposu** hello komut çubuğu ve seçin **Azure depolama.**</span><span class="sxs-lookup"><span data-stu-id="84e8b-327">Click **New data store** on hello command bar and choose **Azure storage.**</span></span> <span data-ttu-id="84e8b-328">Görmeniz gerekir hello Azure depolama alanı oluşturmak için JSON betiği bağlantılı hizmeti hello düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="84e8b-328">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="84e8b-329">Değiştir **hesap adı** hello Azure depolama hesabınızın adını içeren ve **hesap anahtarı** hello erişim anahtarı hello Azure depolama hesabı olan.</span><span class="sxs-lookup"><span data-stu-id="84e8b-329">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="84e8b-330">toolearn tooget depolama alanınızın nasıl erişim anahtar, bkz: [erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma depolama](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="84e8b-330">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="84e8b-331">Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="84e8b-331">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="84e8b-332">Azure Batch bağlı hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e8b-332">Create Azure Batch linked service</span></span>
<span data-ttu-id="84e8b-333">Bu adımda oluşturduğunuz için bağlı hizmet, **Azure Batch** kullanılan toorun hello Data Factory özel etkinlik olan hesap.</span><span class="sxs-lookup"><span data-stu-id="84e8b-333">In this step, you create a linked service for your **Azure Batch** account that is used toorun hello Data Factory custom activity.</span></span>

1. <span data-ttu-id="84e8b-334">Tıklatın **yeni işlem** hello komut çubuğu ve seçin **Azure Batch.**</span><span class="sxs-lookup"><span data-stu-id="84e8b-334">Click **New compute** on hello command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="84e8b-335">Görmeniz gerekir hello bir Azure Batch oluşturmak için JSON betiği bağlantılı hizmeti hello düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="84e8b-335">You should see hello JSON script for creating an Azure Batch linked service in hello editor.</span></span>
2. <span data-ttu-id="84e8b-336">Merhaba JSON betiği:</span><span class="sxs-lookup"><span data-stu-id="84e8b-336">In hello JSON script:</span></span>

   1. <span data-ttu-id="84e8b-337">Değiştir **hesap adı** Azure Batch hesabınızın hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="84e8b-337">Replace **account name** with hello name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="84e8b-338">Değiştir **erişim tuşu** hello Azure Batch hesabı hello erişim anahtarı ile.</span><span class="sxs-lookup"><span data-stu-id="84e8b-338">Replace **access key** with hello access key of hello Azure Batch account.</span></span>
   3. <span data-ttu-id="84e8b-339">Merhaba Hello hello havuz Kimliğini girin **poolName** özelliği**.**</span><span class="sxs-lookup"><span data-stu-id="84e8b-339">Enter hello ID of hello pool for hello **poolName** property**.**</span></span> <span data-ttu-id="84e8b-340">Bu özellik için ya da havuz adı belirtin veya Havuz kimliği.</span><span class="sxs-lookup"><span data-stu-id="84e8b-340">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="84e8b-341">Hello için Hello toplu URI girin **batchUri** JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="84e8b-341">Enter hello batch URI for hello **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="84e8b-342">Merhaba **URL** hello gelen **Azure Batch hesabı dikey** biçimini izleyen hello olduğu: \<accountname\>.\< Bölge\>. batch.azure.com. Hello için **batchUri** hello JSON özelliğinde ihtiyacınız çok**"accountname." Kaldır**</span><span class="sxs-lookup"><span data-stu-id="84e8b-342">hello **URL** from hello **Azure Batch account blade** is in hello following format: \<accountname\>.\<region\>.batch.azure.com. For hello **batchUri** property in hello JSON, you need too**remove "accountname."**</span></span> <span data-ttu-id="84e8b-343">Merhaba URL'den.</span><span class="sxs-lookup"><span data-stu-id="84e8b-343">from hello URL.</span></span> <span data-ttu-id="84e8b-344">Örnek: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="84e8b-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="84e8b-345">Hello için **poolName** özelliği, hello hello havuzu hello havuzunun hello adı yerine Kimliğini de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-345">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="84e8b-346">Hdınsight için yaptığı gibi hello Data Factory hizmeti Azure toplu işlem için bir isteğe bağlı seçeneği desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="84e8b-346">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="84e8b-347">Bu gibi durumlarda, kendi Azure Batch havuzu yalnızca bir Azure data factory kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="84e8b-348">Belirtin **StorageLinkedService** hello için **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="84e8b-348">Specify **StorageLinkedService** for hello **linkedServiceName** property.</span></span> <span data-ttu-id="84e8b-349">Bu bağlı hizmetin hello önceki adımda oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-349">You created this linked service in hello previous step.</span></span> <span data-ttu-id="84e8b-350">Bu depolama dosyaları ve günlükleri için hazırlama alanı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="84e8b-351">Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="84e8b-351">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="84e8b-352">3. adım: veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e8b-352">Step 3: Create datasets</span></span>
<span data-ttu-id="84e8b-353">Bu adımda, veri kümeleri toorepresent girişi oluşturun ve çıktı verilerini.</span><span class="sxs-lookup"><span data-stu-id="84e8b-353">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="84e8b-354">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e8b-354">Create input dataset</span></span>
1. <span data-ttu-id="84e8b-355">Merhaba, **Düzenleyicisi** hello veri fabrikası'ı tıklatın **yeni veri kümesi** hello araç ve tıklatın düğmesinde **Azure Blob Depolama** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="84e8b-355">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="84e8b-356">Merhaba JSON hello sağ bölmedeki JSON parçacığı aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="84e8b-356">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

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

    <span data-ttu-id="84e8b-357">Başlangıç saati ile bu kılavuzda daha sonra bir işlem hattı oluşturma: 2015-11-16T00:00:00Z ve bitiş zamanı: 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="84e8b-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="84e8b-358">Zamanlanmış tooproduce verilerdir **saatlik**, 5 giriş/çıkış dilimler olduklarından (arasında **00**: 00:00 -\> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="84e8b-358">It is scheduled tooproduce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="84e8b-359">Merhaba **sıklığı** ve **aralığı** hello girdi veri kümesi çok ayarlamak için**saat** ve **1**, o hello başka bir deyişle, dilim kullanılabilir giriş saatlik.</span><span class="sxs-lookup"><span data-stu-id="84e8b-359">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span>

    <span data-ttu-id="84e8b-360">Hangi tarafından temsil edilen hello başlangıç zamanlarını her dilim için işte **SliceStart** JSON parçacığı yukarıda hello sistem değişkeninde.</span><span class="sxs-lookup"><span data-stu-id="84e8b-360">Here are hello start times for each slice, which is represented by **SliceStart** system variable in hello above JSON snippet.</span></span>

    | <span data-ttu-id="84e8b-361">**Dilim**</span><span class="sxs-lookup"><span data-stu-id="84e8b-361">**Slice**</span></span> | <span data-ttu-id="84e8b-362">**Başlangıç zamanı**</span><span class="sxs-lookup"><span data-stu-id="84e8b-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="84e8b-363">1</span><span class="sxs-lookup"><span data-stu-id="84e8b-363">1</span></span>         | <span data-ttu-id="84e8b-364">2015 11 16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="84e8b-365">2</span><span class="sxs-lookup"><span data-stu-id="84e8b-365">2</span></span>         | <span data-ttu-id="84e8b-366">2015 11 16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="84e8b-367">3</span><span class="sxs-lookup"><span data-stu-id="84e8b-367">3</span></span>         | <span data-ttu-id="84e8b-368">2015 11 16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="84e8b-369">4</span><span class="sxs-lookup"><span data-stu-id="84e8b-369">4</span></span>         | <span data-ttu-id="84e8b-370">2015 11 16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="84e8b-371">5</span><span class="sxs-lookup"><span data-stu-id="84e8b-371">5</span></span>         | <span data-ttu-id="84e8b-372">2015 11 16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="84e8b-373">Merhaba **folderPath** hello yıl, ay, gün ve saat parçası hello dilim başlangıç saati kullanılarak hesaplanır (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="84e8b-373">hello **folderPath** is calculated by using hello year, month, day, and hour part of hello slice start time (**SliceStart**).</span></span> <span data-ttu-id="84e8b-374">Bu nedenle, işte nasıl bir giriş eşlenen tooa dilim klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="84e8b-374">Therefore, here is how an input folder is mapped tooa slice.</span></span>

    | <span data-ttu-id="84e8b-375">**Dilim**</span><span class="sxs-lookup"><span data-stu-id="84e8b-375">**Slice**</span></span> | <span data-ttu-id="84e8b-376">**Başlangıç zamanı**</span><span class="sxs-lookup"><span data-stu-id="84e8b-376">**Start time**</span></span>          | <span data-ttu-id="84e8b-377">**Giriş klasörü**</span><span class="sxs-lookup"><span data-stu-id="84e8b-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="84e8b-378">1</span><span class="sxs-lookup"><span data-stu-id="84e8b-378">1</span></span>         | <span data-ttu-id="84e8b-379">2015 11 16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="84e8b-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="84e8b-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="84e8b-381">2</span><span class="sxs-lookup"><span data-stu-id="84e8b-381">2</span></span>         | <span data-ttu-id="84e8b-382">2015 11 16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="84e8b-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="84e8b-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="84e8b-384">3</span><span class="sxs-lookup"><span data-stu-id="84e8b-384">3</span></span>         | <span data-ttu-id="84e8b-385">2015 11 16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="84e8b-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="84e8b-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="84e8b-387">4</span><span class="sxs-lookup"><span data-stu-id="84e8b-387">4</span></span>         | <span data-ttu-id="84e8b-388">2015 11 16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="84e8b-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="84e8b-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="84e8b-390">5</span><span class="sxs-lookup"><span data-stu-id="84e8b-390">5</span></span>         | <span data-ttu-id="84e8b-391">2015 11 16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="84e8b-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="84e8b-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="84e8b-393">Tıklatın **dağıtma** araç toocreate hello ve hello dağıtmak **InputDataset** tablo.</span><span class="sxs-lookup"><span data-stu-id="84e8b-393">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="84e8b-394">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="84e8b-394">Create output dataset</span></span>
<span data-ttu-id="84e8b-395">Bu adımda, başka bir veri kaynağının veri türü AzureBlob toorepresent hello çıkış veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84e8b-395">In this step, you create another dataset of type AzureBlob toorepresent hello output data.</span></span>

1. <span data-ttu-id="84e8b-396">Merhaba, **Düzenleyicisi** hello veri fabrikası'ı tıklatın **yeni veri kümesi** hello araç ve tıklatın düğmesinde **Azure Blob Depolama** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="84e8b-396">In hello **Editor** for hello Data Factory, click **New dataset** button on hello toolbar and click **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="84e8b-397">Merhaba JSON hello sağ bölmedeki JSON parçacığı aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="84e8b-397">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

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

    <span data-ttu-id="84e8b-398">Bir çıkış blob/dosyası, her girdi dilimi için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="84e8b-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="84e8b-399">İşte bir çıktı dosyası için her dilimi nasıl adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="84e8b-400">Bir çıkış klasöründe oluşturulan tüm hello çıktı dosyaları: `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="84e8b-400">All hello output files are generated in one output folder: `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="84e8b-401">**Dilim**</span><span class="sxs-lookup"><span data-stu-id="84e8b-401">**Slice**</span></span> | <span data-ttu-id="84e8b-402">**Başlangıç zamanı**</span><span class="sxs-lookup"><span data-stu-id="84e8b-402">**Start time**</span></span>          | <span data-ttu-id="84e8b-403">**Çıkış dosyası**</span><span class="sxs-lookup"><span data-stu-id="84e8b-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="84e8b-404">1</span><span class="sxs-lookup"><span data-stu-id="84e8b-404">1</span></span>         | <span data-ttu-id="84e8b-405">2015 11 16T**00**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="84e8b-406">2015-11-16 -**00. txt**</span><span class="sxs-lookup"><span data-stu-id="84e8b-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="84e8b-407">2</span><span class="sxs-lookup"><span data-stu-id="84e8b-407">2</span></span>         | <span data-ttu-id="84e8b-408">2015 11 16T**01**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="84e8b-409">2015-11-16 -**01. txt**</span><span class="sxs-lookup"><span data-stu-id="84e8b-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="84e8b-410">3</span><span class="sxs-lookup"><span data-stu-id="84e8b-410">3</span></span>         | <span data-ttu-id="84e8b-411">2015 11 16T**02**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="84e8b-412">2015-11-16 -**02. txt**</span><span class="sxs-lookup"><span data-stu-id="84e8b-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="84e8b-413">4</span><span class="sxs-lookup"><span data-stu-id="84e8b-413">4</span></span>         | <span data-ttu-id="84e8b-414">2015 11 16T**03**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="84e8b-415">2015-11-16 -**03. txt**</span><span class="sxs-lookup"><span data-stu-id="84e8b-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="84e8b-416">5</span><span class="sxs-lookup"><span data-stu-id="84e8b-416">5</span></span>         | <span data-ttu-id="84e8b-417">2015 11 16T**04**: 00:00</span><span class="sxs-lookup"><span data-stu-id="84e8b-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="84e8b-418">2015-11-16 -**04. txt**</span><span class="sxs-lookup"><span data-stu-id="84e8b-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="84e8b-419">Tüm giriş klasöründeki dosyaları hello unutmayın (örneğin: 2015-11-16-00) hello başlangıç saatine sahip bir dilim parçasıdır: 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="84e8b-419">Remember that all hello files in an input folder (for example: 2015-11-16-00) are part of a slice with hello start time: 2015-11-16-00.</span></span> <span data-ttu-id="84e8b-420">Bu dilim işlendiğinde hello özel etkinlik her dosyası aracılığıyla tarar ve arama terimi ("Microsoft") oluşumları hello sayısıyla hello çıkış dosyasındaki bir satır üretir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-420">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="84e8b-421">Başlangıç klasörü 2015-11-16-00 üç dosya varsa vardır üç satır hello çıktı dosyasına: 2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="84e8b-421">If there are three files in hello folder 2015-11-16-00, there are three lines in hello output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="84e8b-422">Tıklatın **dağıtma** araç toocreate hello ve hello dağıtmak **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-422">Click **Deploy** on hello toolbar toocreate and deploy hello **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-hello-pipeline-with-custom-activity"></a><span data-ttu-id="84e8b-423">4. adım: Oluşturma ve hello ardışık düzen özel etkinliği ile çalıştırma</span><span class="sxs-lookup"><span data-stu-id="84e8b-423">Step 4: Create and run hello pipeline with custom activity</span></span>
<span data-ttu-id="84e8b-424">Bu adımda, bir etkinlik, daha önce oluşturduğunuz hello özel etkinliği ile işlem hattı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="84e8b-424">In this step, you create a pipeline with one activity, hello custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84e8b-425">Merhaba yüklemediniz varsa **dosya.txt'yi** tooinput klasörleri hello blob kapsayıcısında, bunu hello işlem hattı oluşturmadan önce.</span><span class="sxs-lookup"><span data-stu-id="84e8b-425">If you haven't uploaded hello **file.txt** tooinput folders in hello blob container, do so before creating hello pipeline.</span></span> <span data-ttu-id="84e8b-426">Merhaba **isPaused** özelliği ayarlanmış toofalse hello ile JSON işlem hattında, hello ardışık düzen hemen hello çalıştığında **Başlat** hello son tarihidir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-426">hello **isPaused** property is set toofalse in hello pipeline JSON, so hello pipeline runs immediately as hello **start** date is in hello past.</span></span>
>
>

1. <span data-ttu-id="84e8b-427">Hello Data Factory Düzenleyici'de, tıklatın **yeni işlem hattı** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="84e8b-427">In hello Data Factory Editor, click **New pipeline** on hello command bar.</span></span> <span data-ttu-id="84e8b-428">Merhaba komutu görmüyorsanız tıklatın **... (Üç nokta)**  toosee onu.</span><span class="sxs-lookup"><span data-stu-id="84e8b-428">If you do not see hello command, click **... (Ellipsis)** toosee it.</span></span>
2. <span data-ttu-id="84e8b-429">Merhaba JSON hello sağ bölmedeki JSON betiği aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="84e8b-429">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

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
   <span data-ttu-id="84e8b-430">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="84e8b-430">Note hello following points:</span></span>

   * <span data-ttu-id="84e8b-431">Hello ardışık düzeninde yalnızca bir etkinlik olduğu ve bu tür: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-431">There is only one activity in hello pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="84e8b-432">**AssemblyName** hello DLL toohello adına ayarlanır: **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-432">**AssemblyName** is set toohello name of hello DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="84e8b-433">**EntryPoint** çok ayarlanır**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-433">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="84e8b-434">Temelde olan \<ad alanı\>.\< ClassName\> kodunuzda.</span><span class="sxs-lookup"><span data-stu-id="84e8b-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="84e8b-435">**PackageLinkedService** çok ayarlanır**StorageLinkedService** hello özel etkinlik zip dosyasını içeren toohello blob depolama işaret eder.</span><span class="sxs-lookup"><span data-stu-id="84e8b-435">**PackageLinkedService** is set too**StorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="84e8b-436">Giriş/çıkış dosyaları ve hello özel etkinlik zip dosyası için farklı Azure depolama hesapları kullanıyorsanız, başka bir Azure Storage toocreate sahip bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="84e8b-436">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you have toocreate another Azure Storage linked service.</span></span> <span data-ttu-id="84e8b-437">Bu makalede, kullanmakta olduğunuz varsayılmaktadır hello aynı Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="84e8b-437">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="84e8b-438">**PackageFile** çok ayarlanır**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-438">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="84e8b-439">Merhaba biçimdedir: \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="84e8b-439">It is in hello format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="84e8b-440">Merhaba özel etkinlik alır **InputDataset** giriş olarak ve **OutputDataset** çıktı olarak.</span><span class="sxs-lookup"><span data-stu-id="84e8b-440">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="84e8b-441">Merhaba **linkedServiceName** hello özel etkinlik özelliğinin işaret toohello **AzureBatchLinkedService**, o hello özel etkinliği Azure Data Factory söyleyen Azure batch toorun gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="84e8b-441">hello **linkedServiceName** property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch.</span></span>
   * <span data-ttu-id="84e8b-442">Merhaba **eşzamanlılık** ayarı önemlidir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-442">hello **concurrency** setting is important.</span></span> <span data-ttu-id="84e8b-443">1, 2 veya daha fazla işlem düğümleri hello Azure Batch havuzunda olsa dahi, hello varsayılan değeri kullanırsanız hello dilimler işlenir birbiri ardından.</span><span class="sxs-lookup"><span data-stu-id="84e8b-443">If you use hello default value, which is 1, even if you have 2 or more compute nodes in hello Azure Batch pool, hello slices are processed one after another.</span></span> <span data-ttu-id="84e8b-444">Bu nedenle, Azure batch hello paralel işleme yeteneğinden olmuyor.</span><span class="sxs-lookup"><span data-stu-id="84e8b-444">Therefore, you are not taking advantage of hello parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="84e8b-445">Ayarlarsanız **eşzamanlılık** tooa daha yüksek değer, deyin 2 geldiğini iki dilimler (Azure Batch tootwo görevlerinde karşılık gelir) hello işlenen aynı zaman; bu durumda hem hello Vm'lerde hello Azure Batch havuzu kullanıldığı.</span><span class="sxs-lookup"><span data-stu-id="84e8b-445">If you set **concurrency** tooa higher value, say 2, it means that two slices (corresponds tootwo tasks in Azure Batch) can be processed at hello same time, in which case, both hello VMs in hello Azure Batch pool are utilized.</span></span> <span data-ttu-id="84e8b-446">Bu nedenle, hello eşzamanlılık özelliğini uygun şekilde ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-446">Therefore, set hello concurrency property appropriately.</span></span>
   * <span data-ttu-id="84e8b-447">Yalnızca bir görev (dilim) varsayılan olarak, varsayılan olarak herhangi bir noktada bir VM üzerinde yürütülür.</span><span class="sxs-lookup"><span data-stu-id="84e8b-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="84e8b-448">Merhaba, varsayılan olarak, hello nedeni **maksimum VM başına görevleri** too1 bir Azure Batch havuzu için ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-448">hello reason is that, by default, hello **Maximum tasks per VM** is set too1 for an Azure Batch pool.</span></span> <span data-ttu-id="84e8b-449">İki veri fabrikası dilimler hello konumundaki bir VM'de çalıştıran için Önkoşullar bir parçası olarak, bir havuz bu özellik kümesi too2 ile oluşturduğunuz aynı anda.</span><span class="sxs-lookup"><span data-stu-id="84e8b-449">As part of prerequisites, you created a pool with this property set too2, so two Data Factory slices can be running on a VM at hello same time.</span></span>

    -   <span data-ttu-id="84e8b-450">**isPaused** özelliği toofalse varsayılan olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-450">**isPaused** property is set toofalse by default.</span></span> <span data-ttu-id="84e8b-451">Hello dilimler hello geçmiş başlatmak için hello ardışık düzen hemen bu örnekte çalışır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-451">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="84e8b-452">Bu özellik tootrue toopause hello ardışık düzen ve geri toofalse toorestart ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-452">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>

    -   <span data-ttu-id="84e8b-453">Merhaba **Başlat** zaman ve **son** kez beş saatten birbirinden olur ve dilimlerinin saatlik, beş dilimler hello ardışık düzen tarafından üretilen şekilde.</span><span class="sxs-lookup"><span data-stu-id="84e8b-453">hello **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>

1. <span data-ttu-id="84e8b-454">Tıklatın **dağıtma** toodeploy hello ardışık çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="84e8b-454">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span>

#### <a name="step-5-test-hello-pipeline"></a><span data-ttu-id="84e8b-455">5. adım: Test hello ardışık düzen</span><span class="sxs-lookup"><span data-stu-id="84e8b-455">Step 5: Test hello pipeline</span></span>
<span data-ttu-id="84e8b-456">Bu adımda, hello giriş klasörler halinde dosyaları bırakarak hello ardışık düzen sınayın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-456">In this step, you test hello pipeline by dropping files into hello input folders.</span></span> <span data-ttu-id="84e8b-457">Sınama hello ardışık düzen ile bir giriş klasörü başına bir dosyayı ile başlayalım.</span><span class="sxs-lookup"><span data-stu-id="84e8b-457">Let’s start with testing hello pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="84e8b-458">Hello Azure portal'ın Hello Data Factory dikey penceresinde tıklayın **diyagramı**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-458">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="84e8b-459">Girdi veri kümesi Hello diyagram görünümünde çift: **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-459">In hello diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="84e8b-460">Merhaba görmelisiniz **InputDataset** beş dikey dilimi hazır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-460">You should see hello **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="84e8b-461">Bildirim hello **DİLİM başlangıç saati** ve **DİLİM bitiş saati** her dilim için.</span><span class="sxs-lookup"><span data-stu-id="84e8b-461">Notice hello **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="84e8b-462">Merhaba, **diyagram görünümü**, şimdi **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-462">In hello **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="84e8b-463">Bunlar zaten oluşturulmuş olduğunu hello beş çıkış dilimler hello hazır durumda olduğunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-463">You should see that hello five output slices are in hello Ready state if they have already been produced.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="84e8b-464">Kullanım Azure portal tooview hello **görevleri** hello ile ilişkili **dilimler** ve her dilim çalıştırdı hangi VM bakın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-464">Use Azure portal tooview hello **tasks** associated with hello **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="84e8b-465">Bkz: [Data Factory ve toplu tümleştirme](#data-factory-and-batch-integration) ayrıntıları bölümü.</span><span class="sxs-lookup"><span data-stu-id="84e8b-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="84e8b-466">Merhaba hello Çıkış dosyalarını görmelisiniz `outputfolder` , `mycontainer` , Azure blob depolamada.</span><span class="sxs-lookup"><span data-stu-id="84e8b-466">You should see hello output files in hello `outputfolder` of `mycontainer` in your Azure blob storage.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="84e8b-467">Bir giriş her dilim için beş çıktı dosyalarını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="84e8b-468">Her hello dosyasının çıkışı aşağıdaki içerik benzer toohello olmalıdır çıktı:</span><span class="sxs-lookup"><span data-stu-id="84e8b-468">Each of hello output file should have content similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="84e8b-469">Merhaba Aşağıdaki diyagramda nasıl hello Data Factory dilimler Azure Batch tootasks eşleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-469">hello following diagram illustrates how hello Data Factory slices map tootasks in Azure Batch.</span></span> <span data-ttu-id="84e8b-470">Bu örnekte, yalnızca bir çalışma bir dilimi var.</span><span class="sxs-lookup"><span data-stu-id="84e8b-470">In this example, a slice has only one run.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="84e8b-471">Şimdi, bir klasördeki birden çok dosyalarla deneyelim.</span><span class="sxs-lookup"><span data-stu-id="84e8b-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="84e8b-472">Dosyaları oluşturun: **file2.txt**, **file3.txt**, **file4.txt**, ve **file5.txt** hello ile aynı hello klasöründeki dosya.txt'yi olduğu gibi içerik: **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with hello same content as in file.txt in hello folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="84e8b-473">Merhaba çıkış klasöründe **silmek** hello çıktı dosyası: **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-473">In hello output folder, **delete** hello output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="84e8b-474">Şimdi hello içinde **OutputDataset** dikey penceresinde, sağ hello dilimle **DİLİM başlangıç saati** çok ayarlamak**11/16/2015 01:00:00 AM**, tıklatıp **çalıştırmak**toorerun/yeniden-process hello dilim.</span><span class="sxs-lookup"><span data-stu-id="84e8b-474">Now, in hello **OutputDataset** blade, right-click hello slice with **SLICE START TIME** set too**11/16/2015 01:00:00 AM**, and click **Run** toorerun/re-process hello slice.</span></span> <span data-ttu-id="84e8b-475">Şimdi, hello dilim beş dosya yerine bir dosya vardır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-475">Now, hello slice has five files instead of one file.</span></span>

    ![](./media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="84e8b-476">Durumunu Hello dilim çalıştırır ve sonra **hazır**, bu dilim için hello çıktı dosyasında hello içeriği doğrulayın (**2015-11-16-01.txt**) hello içinde `outputfolder` , `mycontainer` blob depolama alanınızın içinde.</span><span class="sxs-lookup"><span data-stu-id="84e8b-476">After hello slice runs and its status is **Ready**, verify hello content in hello output file for this slice (**2015-11-16-01.txt**) in hello `outputfolder` of `mycontainer` in your blob storage.</span></span> <span data-ttu-id="84e8b-477">Merhaba dilimin her dosya için bir satır olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-477">There should be a line for each file of hello slice.</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="84e8b-478">Beş giriş dosyalarıyla denemeden önce hello çıktı dosyası 2015-11-16-01.txt silmedi varsa bir satırından hello önceki dilim çalıştırın ve Çalıştır hello geçerli dilimin beş satırlarından bakın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-478">If you did not delete hello output file 2015-11-16-01.txt before trying with five input files, you see one line from hello previous slice run and five lines from hello current slice run.</span></span> <span data-ttu-id="84e8b-479">Zaten varsa, varsayılan olarak, hello içerik eklenmiş toooutput dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-479">By default, hello content is appended toooutput file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="84e8b-480">Veri Fabrikası ve toplu tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="84e8b-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="84e8b-481">Hello Data Factory hizmetinin hello adı ile Azure toplu işleminde bir işi oluşturur: `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="84e8b-481">hello Data Factory service creates a job in Azure Batch with hello name: `adf-poolname:job-xxx`.</span></span>

![Azure Data Factory - toplu işler](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="84e8b-483">Bir görev hello işteki her bir dilim etkinlik çalıştırması için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="84e8b-483">A task in hello job is created for each activity run of a slice.</span></span> <span data-ttu-id="84e8b-484">İşlenen 10 dilim hazır toobe varsa, 10 görevleri hello işinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="84e8b-484">If there are 10 slices ready toobe processed, 10 tasks are created in hello job.</span></span> <span data-ttu-id="84e8b-485">Birden çok işlem düğümleri hello havuzunda varsa paralel olarak çalışan birden fazla dilim olabilir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-485">You can have more than one slice running in parallel if you have multiple compute nodes in hello pool.</span></span> <span data-ttu-id="84e8b-486">Merhaba maksimum başına düğüm çok kümesi işlem görevlerini durumunda > 1, olabilir birden fazla bir dilim hello üzerinde çalışan aynı işlem.</span><span class="sxs-lookup"><span data-stu-id="84e8b-486">If hello maximum tasks per compute node is set too> 1, there can be more than one slice running on hello same compute.</span></span>

<span data-ttu-id="84e8b-487">Bu örnekte, beş dilimler, Azure Batch kadar beş görevleri vardır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="84e8b-488">Merhaba ile **eşzamanlılık** çok ayarlamak**5** hello Azure Data Factory JSON'de kanal ve **maksimum VM başına görevleri** çok ayarlamak**2** Azure toplu ile havuz **2** VM'ler, (görevler için başlangıç ve bitiş zamanlarını denetleyin) hello görevleri çalıştırır hızlı.</span><span class="sxs-lookup"><span data-stu-id="84e8b-488">With hello **concurrency** set too**5** in hello pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set too**2** in Azure Batch pool with **2** VMs, hello tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="84e8b-489">Merhaba portal tooview hello toplu ve hello ile ilişkili görevleri kullanma **dilimler** ve her dilim çalıştırdı hangi VM bakın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-489">Use hello portal tooview hello Batch job and its tasks that are associated with hello **slices** and see what VM each slice ran on.</span></span>

![Azure Data Factory - toplu iş görevleri](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-hello-pipeline"></a><span data-ttu-id="84e8b-491">Merhaba ardışık hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="84e8b-491">Debug hello pipeline</span></span>
<span data-ttu-id="84e8b-492">Hata ayıklama birkaç temel teknikten oluşur:</span><span class="sxs-lookup"><span data-stu-id="84e8b-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="84e8b-493">Merhaba girdi dilimi çok ayarlanmamışsa**hazır**, hello giriş klasör yapısı doğru olduğundan ve dosya.txt'yi hello giriş klasörlerde var olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-493">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and file.txt exists in hello input folders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="84e8b-494">Merhaba, **yürütme** özel etkinliklerinizi, kullanım hello yöntemi **IActivityLogger** yardımcı olan nesne toolog bilgileri sorunları giderme.</span><span class="sxs-lookup"><span data-stu-id="84e8b-494">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="84e8b-495">oturum karışılama iletileri hello kullanıcı görünmesini\_0. günlük dosyası.</span><span class="sxs-lookup"><span data-stu-id="84e8b-495">hello logged messages show up in hello user\_0.log file.</span></span>

   <span data-ttu-id="84e8b-496">Merhaba, **OutputDataset** dikey penceresinde hello dilim toosee hello tıklatın **veri DİLİMİ** dikey penceresinde, dilim için.</span><span class="sxs-lookup"><span data-stu-id="84e8b-496">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="84e8b-497">Gördüğünüz **etkinlik çalışması** bu dilim için.</span><span class="sxs-lookup"><span data-stu-id="84e8b-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="84e8b-498">Merhaba dilim için bir etkinlik görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-498">You should see one activity run for hello slice.</span></span> <span data-ttu-id="84e8b-499">Tıklatırsanız **çalıştırmak** hello komut çubuğunda hello için başka bir etkinlik başlatabilirsiniz aynı dilim.</span><span class="sxs-lookup"><span data-stu-id="84e8b-499">If you click **Run** in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="84e8b-500">Merhaba etkinlik tıklattığınızda hello bkz **etkinlik çalışma ayrıntıları** günlük dosyalarının listesini içeren dikey.</span><span class="sxs-lookup"><span data-stu-id="84e8b-500">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="84e8b-501">Merhaba, günlüğe kaydedilen iletilere bakın **kullanıcı\_0. günlük** dosya.</span><span class="sxs-lookup"><span data-stu-id="84e8b-501">You see logged messages in hello **user\_0.log** file.</span></span> <span data-ttu-id="84e8b-502">Hata oluştuğunda hello yeniden deneme sayısı hello ardışık düzen/JSON etkinliğinde too3 ayarlandığından üç Etkinlik çalışması bakın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-502">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="84e8b-503">Merhaba etkinlik tıklattığınızda tootroubleshoot hello hata inceleyebilirsiniz hello günlük dosyalarına bakın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-503">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="84e8b-504">Günlük dosyaları Hello listesinde hello tıklayın **kullanıcı 0.log**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-504">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="84e8b-505">Merhaba sağ panelde hello kullanarak hello sonucu olan **IActivityLogger.Write** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="84e8b-505">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="84e8b-506">Sistem hata iletileri ve özel durumlar için sistem 0.log denetleyin.</span><span class="sxs-lookup"><span data-stu-id="84e8b-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="84e8b-507">Merhaba dahil **PDB** hello hata ayrıntıları bilgileri gibi böylece hello zip dosyasında dosya **çağrı yığını** bir hata oluştuğunda.</span><span class="sxs-lookup"><span data-stu-id="84e8b-507">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="84e8b-508">Merhaba özel etkinlik hello olmalıdır tüm dosyaları hello zip dosyasında hello **üst düzey** klasörsüz ile.</span><span class="sxs-lookup"><span data-stu-id="84e8b-508">All hello files in hello zip file for hello custom activity must be at hello **top level** with no subfolders.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="84e8b-509">Bu hello olun **assemblyName** (MyDotNetActivity.dll) **entryPoint** (MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) ve **packageLinkedService** (noktası toohello Azure hello zip dosyasını içeren depolama blob) toocorrect değerlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-509">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
6. <span data-ttu-id="84e8b-510">Bir hata ve istediğiniz tooreprocess hello dilim sabit, hello hello dilimi sağ **OutputDataset** tıklayın ve dikey **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-510">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>

   ![](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="84e8b-511">Gördüğünüz bir **kapsayıcı** adlı Azure Blob storage'da: `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="84e8b-511">You see a **container** in your Azure Blob storage named: `adfjobs`.</span></span> <span data-ttu-id="84e8b-512">Bu kapsayıcı otomatik olarak silinmez, ancak test hello çözüm tamamladıktan sonra güvenle silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-512">This container is not automatically deleted, but you can safely delete it after you are done testing hello solution.</span></span> <span data-ttu-id="84e8b-513">Benzer şekilde, bir Azure Batch hello Data Factory çözüm oluşturur **iş** adlı: `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="84e8b-513">Similarly, hello Data Factory solution creates an Azure Batch **job** named: `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="84e8b-514">Merhaba çözüm isterseniz, test ettikten sonra bu iş silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-514">You can delete this job after you test hello solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="84e8b-515">Merhaba özel etkinlik hello kullanmaz **app.config** paketinizi dosyasından.</span><span class="sxs-lookup"><span data-stu-id="84e8b-515">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="84e8b-516">Bu nedenle, kodunuzu hello yapılandırma dosyasından bağlantı dizelerini yazıyorsa, çalışma zamanında çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="84e8b-516">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="84e8b-517">Azure Batch kullanarak toohold olduğunda en iyi yöntem herhangi parolalarında hello bir **Azure KeyVault**, sertifika tabanlı hizmet asıl tooprotect hello keyvault kullanın ve hello sertifika tooAzure Batch havuzu dağıtın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-517">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello keyvault, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="84e8b-518">.NET özel etkinlik hello sonra gizli hello KeyVault çalışma zamanında erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-518">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="84e8b-519">Bu çözüm genel bir ve gizli anahtarı, yalnızca bağlantı dizesi tooany türü ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-519">This solution is a generic one and can scale tooany type of secret, not just connection string.</span></span>

    <span data-ttu-id="84e8b-520">Daha kolay bir çözüm (ancak en iyi yöntem değildir): oluşturabileceğiniz bir **Azure SQL bağlı hizmeti** bağlantı dizesi ayarlarıyla kullanır bağlantılı hizmet ve sahte bir giriş veri kümesi olarak zinciri hello dataset hello bir veri kümesi oluşturma toohello özel .NET etkinlik.</span><span class="sxs-lookup"><span data-stu-id="84e8b-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="84e8b-521">Hizmetin bağlantı dizesi hello özel etkinlik kodda erişim hello bağlı ve çalışma zamanında düzgün çalışması gerekir. ardından kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-521">You can then access hello linked service's connection string in hello custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-hello-sample"></a><span data-ttu-id="84e8b-522">Merhaba örnek genişletme</span><span class="sxs-lookup"><span data-stu-id="84e8b-522">Extend hello sample</span></span>
<span data-ttu-id="84e8b-523">Bu örnek toolearn Azure Data Factory ve Azure Batch özellikler hakkında daha fazla genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-523">You can extend this sample toolearn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="84e8b-524">Örneğin, farklı bir zaman aralığı tooprocess dilimleri hello aşağıdaki adımları:</span><span class="sxs-lookup"><span data-stu-id="84e8b-524">For example, tooprocess slices in a different time range, do hello following steps:</span></span>

1. <span data-ttu-id="84e8b-525">Merhaba klasörlerdeki aşağıdaki hello eklemek `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 ve Yerleştir bu klasörlerdeki girişi dosyaları.</span><span class="sxs-lookup"><span data-stu-id="84e8b-525">Add hello following subfolders in hello `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="84e8b-526">Değiştirme hello bitiş saati başlangıç ardışık düzen tarafından `2015-11-16T05:00:00Z` çok`2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="84e8b-526">Change hello end time for hello pipeline from `2015-11-16T05:00:00Z` too`2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="84e8b-527">Merhaba, **diyagram görünümü**, hello çift **InputDataset**ve hello girdi dilimlerinin hazır olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="84e8b-527">In hello **Diagram View**, double-click hello **InputDataset**, and confirm that hello input slices are ready.</span></span> <span data-ttu-id="84e8b-528">Çift **OuptutDataset** çıkış dilimler toosee hello durumu.</span><span class="sxs-lookup"><span data-stu-id="84e8b-528">Double-click **OuptutDataset** toosee hello state of output slices.</span></span> <span data-ttu-id="84e8b-529">Hazır durumda olmaları durumunda hello çıkış dosyaları için hello çıkış klasörünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="84e8b-529">If they are in Ready state, check hello output folder for hello output files.</span></span>
2. <span data-ttu-id="84e8b-530">Artırma veya azaltma hello **eşzamanlılık** ayarı toounderstand Merhaba, çözümünüzün performansını etkiler nasıl özellikle hello işleme Azure Batch oluşan.</span><span class="sxs-lookup"><span data-stu-id="84e8b-530">Increase or decrease hello **concurrency** setting toounderstand how it affects hello performance of your solution, especially hello processing that occurs on Azure Batch.</span></span> <span data-ttu-id="84e8b-531">(Bkz. adım 4: oluşturup hello hakkında daha fazla bilgi için hello ardışık düzen çalıştırmak **eşzamanlılık** ayarı.)</span><span class="sxs-lookup"><span data-stu-id="84e8b-531">(See Step 4: Create and run hello pipeline for more on hello **concurrency** setting.)</span></span>
3. <span data-ttu-id="84e8b-532">Küçük daha yüksek bir havuz oluşturma **maksimum VM başına görevleri**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="84e8b-533">Merhaba, oluşturduğunuz yeni havuz güncelleştirme hello hello Data Factory çözüm bağlı Azure Batch hizmetinde toouse.</span><span class="sxs-lookup"><span data-stu-id="84e8b-533">toouse hello new pool you created, update hello Azure Batch linked service in hello Data Factory solution.</span></span> <span data-ttu-id="84e8b-534">(Bkz. adım 4: oluşturup hello hakkında daha fazla bilgi için hello ardışık düzen çalıştırmak **maksimum VM başına görevleri** ayarı.)</span><span class="sxs-lookup"><span data-stu-id="84e8b-534">(See Step 4: Create and run hello pipeline for more on hello **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="84e8b-535">Bir Azure Batch havuzu oluşturma **otomatik ölçeklendirme** özelliği.</span><span class="sxs-lookup"><span data-stu-id="84e8b-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="84e8b-536">Bir Azure Batch havuzunda işlem düğümlerini otomatik olarak ölçeklendirme, uygulamanız tarafından kullanılan güç işleme hello dinamik ayarlanmasıdır.</span><span class="sxs-lookup"><span data-stu-id="84e8b-536">Automatically scaling compute nodes in an Azure Batch pool is hello dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="84e8b-537">Merhaba formül örneği burada başarır davranış aşağıdaki hello: hello havuzu başlangıçta oluşturulduğunda 1 VM ile başlar.</span><span class="sxs-lookup"><span data-stu-id="84e8b-537">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="84e8b-538">Çalışan + (kuyruğa alınmış) etkin $PendingTasks ölçüm tanımlar hello sayıda görev durumu.</span><span class="sxs-lookup"><span data-stu-id="84e8b-538">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="84e8b-539">Merhaba formül hello ortalama sayısı Bekleyen Görevler hello Son 180 saniye bulur ve TargetDedicated uygun şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="84e8b-539">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="84e8b-540">TargetDedicated hiçbir zaman 25 VM'ler gider sağlar.</span><span class="sxs-lookup"><span data-stu-id="84e8b-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="84e8b-541">Bu nedenle, yeni görevler gönderildiği haliyle havuzu otomatik olarak büyür ve görevler tamamlanınca VM'ler boş bir birer birer hale ve bu VM'lerin hello otomatik ölçeklendirmeyi küçültür.</span><span class="sxs-lookup"><span data-stu-id="84e8b-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="84e8b-542">startingNumberOfVMs ve maxNumberofVMs ayarlanmış tooyour gereksinimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-542">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>
 
    <span data-ttu-id="84e8b-543">Otomatik ölçeklendirme formülü:</span><span class="sxs-lookup"><span data-stu-id="84e8b-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="84e8b-544">Bkz: [ölçek işlem düğümlerini Azure Batch havuzunda otomatik olarak](../batch/batch-automatic-scaling.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="84e8b-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="84e8b-545">Merhaba havuzu hello varsayılan kullanıyorsanız [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch hizmeti, 15-30 dakika tooprepare hello VM hello özel etkinlik çalıştırmadan önce sürebilir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-545">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="84e8b-546">Merhaba havuzu farklı autoScaleEvaluationInterval kullanıyorsanız, hello Batch hizmeti autoScaleEvaluationInterval + 10 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="84e8b-546">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="84e8b-547">Merhaba örnek çözümde hello **yürütme** yöntemini çağırır hello **Hesapla** bir giriş veri dilimi tooproduce bir çıktı veri dilimi işler yöntemi.</span><span class="sxs-lookup"><span data-stu-id="84e8b-547">In hello sample solution, hello **Execute** method invokes hello **Calculate** method that processes an input data slice tooproduce an output data slice.</span></span> <span data-ttu-id="84e8b-548">Kendi yöntemi tooprocess verileri girin ve bir çağrı tooyour yöntemiyle hello hesapla yöntem çağrısı hello Execute yöntemi Değiştir yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84e8b-548">You can write your own method tooprocess input data and replace hello Calculate method call in hello Execute method with a call tooyour method.</span></span>

### <a name="next-steps-consume-hello-data"></a><span data-ttu-id="84e8b-549">Sonraki adımlar: hello verileri kullanmak</span><span class="sxs-lookup"><span data-stu-id="84e8b-549">Next steps: Consume hello data</span></span>
<span data-ttu-id="84e8b-550">Veri işleme sonra onu gibi çevrimiçi araçlarla tüketebileceği **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="84e8b-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="84e8b-551">Power BI anlamak bağlantılar toohelp işte ve nasıl toouse Azure içinde:</span><span class="sxs-lookup"><span data-stu-id="84e8b-551">Here are links toohelp you understand Power BI and how toouse it in Azure:</span></span>

* [<span data-ttu-id="84e8b-552">Power BI kümesinde keşfedin</span><span class="sxs-lookup"><span data-stu-id="84e8b-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="84e8b-553">Merhaba Power BI Desktop ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="84e8b-553">Getting started with hello Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="84e8b-554">Power bı'da veri yenileme</span><span class="sxs-lookup"><span data-stu-id="84e8b-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="84e8b-555">Azure ve Power BI - temel genel bakış</span><span class="sxs-lookup"><span data-stu-id="84e8b-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="84e8b-556">Başvurular</span><span class="sxs-lookup"><span data-stu-id="84e8b-556">References</span></span>
* [<span data-ttu-id="84e8b-557">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="84e8b-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="84e8b-558">Giriş tooAzure Data Factory hizmeti</span><span class="sxs-lookup"><span data-stu-id="84e8b-558">Introduction tooAzure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="84e8b-559">Azure Data Factory ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="84e8b-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="84e8b-560">Bir Azure Data Factory işlem hattında özel etkinlikler kullanma</span><span class="sxs-lookup"><span data-stu-id="84e8b-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="84e8b-561">Azure toplu işlem</span><span class="sxs-lookup"><span data-stu-id="84e8b-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="84e8b-562">Azure Batch temel bilgileri</span><span class="sxs-lookup"><span data-stu-id="84e8b-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="84e8b-563">Azure Batch özelliklerine genel bakış</span><span class="sxs-lookup"><span data-stu-id="84e8b-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="84e8b-564">Hello Azure portal, Azure Batch hesabı oluşturabilir ve yönetebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="84e8b-564">Create and manage Azure Batch account in hello Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="84e8b-565">Azure Batch kitaplığını .NET ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="84e8b-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
