---
title: "bir Azure Data Factory işlem hattı aaaUse özel etkinlikleri"
description: "Bilgi nasıl toocreate özel etkinlikler ve bunları bir Azure Data Factory işlem hattı kullanabilirsiniz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 8dd7ba14-15d2-4fd9-9ada-0b2c684327e9
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: 23e33727b2160541ab40938ffd911fdd484b3daa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-custom-activities-in-an-azure-data-factory-pipeline"></a><span data-ttu-id="4cdd1-103">Bir Azure Data Factory işlem hattında özel etkinlikler kullanma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-103">Use custom activities in an Azure Data Factory pipeline</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="4cdd1-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="4cdd1-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="4cdd1-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="4cdd1-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="4cdd1-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="4cdd1-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="4cdd1-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="4cdd1-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="4cdd1-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="4cdd1-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="4cdd1-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="4cdd1-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="4cdd1-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="4cdd1-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="4cdd1-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="4cdd1-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="4cdd1-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="4cdd1-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="4cdd1-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="4cdd1-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="4cdd1-114">İki tür kullanabileceğiniz bir Azure Data Factory ardışık düzeninde etkinlik yok.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-114">There are two types of activities that you can use in an Azure Data Factory pipeline.</span></span>

- <span data-ttu-id="4cdd1-115">[Veri taşıma etkinlikleri](data-factory-data-movement-activities.md) arasında toomove veri [desteklenen kaynak ve havuz veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="4cdd1-115">[Data Movement Activities](data-factory-data-movement-activities.md) toomove data between [supported source and sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>
- <span data-ttu-id="4cdd1-116">[Veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) kullanarak tootransform Veri Hizmetleri Azure Hdınsight, Azure Batch ve Azure Machine Learning gibi işlem.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-116">[Data Transformation Activities](data-factory-data-transformation-activities.md) tootransform data using compute services such as Azure HDInsight, Azure Batch, and Azure Machine Learning.</span></span> 

<span data-ttu-id="4cdd1-117">Veri Fabrikası desteklemiyor, bir veri deposu/toomove verileri oluşturma bir **özel etkinlik** kendi veri taşıma mantığı ve kullanım hello etkinliği ile bir ardışık düzende.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-117">toomove data to/from a data store that Data Factory does not support, create a **custom activity** with your own data movement logic and use hello activity in a pipeline.</span></span> <span data-ttu-id="4cdd1-118">Benzer şekilde, tootransform/işlemi verileri veri fabrikası tarafından desteklenmeyen bir şekilde kendi veri dönüştürme mantığı ile özel bir etkinlik oluşturmak ve bir ardışık düzende hello etkinliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-118">Similarly, tootransform/process data in a way that isn't supported by Data Factory, create a custom activity with your own data transformation logic and use hello activity in a pipeline.</span></span> 

<span data-ttu-id="4cdd1-119">Özel Etkinlik toorun yapılandırabileceğiniz bir **Azure Batch** sanal makine ya da Windows tabanlı bir havuzu **Azure Hdınsight** küme.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-119">You can configure a custom activity toorun on an **Azure Batch** pool of virtual machines or a Windows-based **Azure HDInsight** cluster.</span></span> <span data-ttu-id="4cdd1-120">Azure Batch kullanırken, mevcut bir Azure Batch havuzu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-120">When using Azure Batch, you can use only an existing Azure Batch pool.</span></span> <span data-ttu-id="4cdd1-121">Oysa Hdınsight kullanırken, mevcut bir Hdınsight kümesine ya da otomatik olarak oluşturulan bir küme, isteğe bağlı çalışma zamanında için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-121">Whereas, when using HDInsight, you can use an existing HDInsight cluster or a cluster that is automatically created for you on-demand at runtime.</span></span>  

<span data-ttu-id="4cdd1-122">Merhaba aşağıdaki örneklerde özel bir .NET etkinlik oluşturmak ve bir ardışık düzende hello özel etkinlik kullanmak için adım adım yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-122">hello following walkthrough provides step-by-step instructions for creating a custom .NET activity and using hello custom activity in a pipeline.</span></span> <span data-ttu-id="4cdd1-123">Merhaba izlenecek kullanan bir **Azure Batch** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-123">hello walkthrough uses an **Azure Batch** linked service.</span></span> <span data-ttu-id="4cdd1-124">toouse Azure Hdınsight bağlı hizmeti bunun yerine, türü bağlı hizmet oluşturma **Hdınsight** (kendi Hdınsight kümenizi) veya **HDInsightOnDemand** (Data Factory oluşturduğu bir Hdınsight kümesi İsteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="4cdd1-124">toouse an Azure HDInsight linked service instead, you create a linked service of type **HDInsight** (your own HDInsight cluster) or **HDInsightOnDemand** (Data Factory creates an HDInsight cluster on-demand).</span></span> <span data-ttu-id="4cdd1-125">Ardından, özel etkinlik toouse hello Hdınsight bağlı hizmeti yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-125">Then, configure custom activity toouse hello HDInsight linked service.</span></span> <span data-ttu-id="4cdd1-126">Bkz: [kullanım Azure Hdınsight bağlantılı Hizmetleri](#use-hdinsight-compute-service) Azure Hdınsight toorun hello özel etkinlik kullanımıyla ilgili ayrıntılar için bölüm.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-126">See [Use Azure HDInsight linked services](#use-hdinsight-compute-service) section for details on using Azure HDInsight toorun hello custom activity.</span></span>

> [!IMPORTANT]
> - <span data-ttu-id="4cdd1-127">Merhaba özel .NET etkinlikler yalnızca Windows tabanlı Hdınsight kümelerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-127">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="4cdd1-128">Bu sınırlama aşağıdaki haller için geçici çözüm toouse hello harita azaltmak etkinlik toorun özel Java kod Linux tabanlı Hdınsight kümesi üzerinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-128">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4cdd1-129">Toouse VM'ler toorun özel etkinlikler bir Hdınsight kümesi yerine bir Azure Batch havuzu başka bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-129">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
> - <span data-ttu-id="4cdd1-130">Olası toouse veri yönetimi ağ geçidi bir özel etkinlik tooaccess şirket içi veri kaynaklarından değil.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-130">It is not possible toouse a Data Management Gateway from a custom activity tooaccess on-premises data sources.</span></span> <span data-ttu-id="4cdd1-131">Şu anda [veri yönetimi ağ geçidi](data-factory-data-management-gateway.md) yalnızca hello kopyalama etkinliği ve saklı yordam etkinliği veri fabrikasında destekler.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-131">Currently, [Data Management Gateway](data-factory-data-management-gateway.md) supports only hello copy activity and stored procedure activity in Data Factory.</span></span>   

## <a name="walkthrough-create-a-custom-activity"></a><span data-ttu-id="4cdd1-132">İzlenecek yol: özel etkinlik oluşturma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-132">Walkthrough: create a custom activity</span></span>
### <a name="prerequisites"></a><span data-ttu-id="4cdd1-133">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4cdd1-133">Prerequisites</span></span>
* <span data-ttu-id="4cdd1-134">Visual Studio 2012/2013/2015</span><span class="sxs-lookup"><span data-stu-id="4cdd1-134">Visual Studio 2012/2013/2015</span></span>
* <span data-ttu-id="4cdd1-135">[Azure .NET SDK](https://azure.microsoft.com/downloads/)’yı indirip yükleyin</span><span class="sxs-lookup"><span data-stu-id="4cdd1-135">Download and install [Azure .NET SDK](https://azure.microsoft.com/downloads/)</span></span>

### <a name="azure-batch-prerequisites"></a><span data-ttu-id="4cdd1-136">Azure Batch önkoşulları</span><span class="sxs-lookup"><span data-stu-id="4cdd1-136">Azure Batch prerequisites</span></span>
<span data-ttu-id="4cdd1-137">Merhaba kılavuzda Azure toplu işlem kaynağı olarak kullanan özel .NET etkinliklerinizi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-137">In hello walkthrough, you run your custom .NET activities using Azure Batch as a compute resource.</span></span> <span data-ttu-id="4cdd1-138">**Azure Batch** büyük ölçekli paralel çalıştırmak için hizmet ve yüksek performanslı bilgi işlem (HPC) uygulamalarında verimli bir şekilde hello bulut platformudur.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-138">**Azure Batch** is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="4cdd1-139">Azure toplu işlem yoğunluklu iş toorun yönetilen üzerinde zamanlar **sanal makineler koleksiyonunda**, ve ölçek kaynakları toomeet hello işleriniz ihtiyaçlarını işlem otomatik olarak.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-139">Azure Batch schedules compute-intensive work toorun on a managed **collection of virtual machines**, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span> <span data-ttu-id="4cdd1-140">Bkz: [Azure Batch temel bilgileri] [ batch-technical-overview] hello Azure Batch hizmeti için ayrıntılı bir genel bakış makalesi.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-140">See [Azure Batch basics][batch-technical-overview] article for a detailed overview of hello Azure Batch service.</span></span>

<span data-ttu-id="4cdd1-141">Merhaba öğretici için VM'ler havuzuyla Azure Batch hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-141">For hello tutorial, create an Azure Batch account with a pool of VMs.</span></span> <span data-ttu-id="4cdd1-142">Merhaba adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-142">Here are hello steps:</span></span>

1. <span data-ttu-id="4cdd1-143">Oluşturma bir **Azure Batch hesabı** hello kullanarak [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4cdd1-143">Create an **Azure Batch account** using hello [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="4cdd1-144">Bkz: [oluşturma ve bir Azure Batch hesabını yönetmek] [ batch-create-account] makale yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-144">See [Create and manage an Azure Batch account][batch-create-account] article for instructions.</span></span>
2. <span data-ttu-id="4cdd1-145">Hello Azure toplu işlem hesabı adı, hesap anahtarı, URI ve havuz adı unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-145">Note down hello Azure Batch account name, account key, URI, and pool name.</span></span> <span data-ttu-id="4cdd1-146">Bunları toocreate bir Azure Batch bağlantılı hizmeti gerekir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-146">You need them toocreate an Azure Batch linked service.</span></span>
    1. <span data-ttu-id="4cdd1-147">Gördüğünüz Hello giriş sayfasında Azure toplu işlem hesabı için bir **URL** biçimini izleyen hello içinde: `https://myaccount.westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-147">On hello home page for Azure Batch account, you see a **URL** in hello following format: `https://myaccount.westus.batch.azure.com`.</span></span> <span data-ttu-id="4cdd1-148">Bu örnekte, **myaccount** hello Azure Batch hesabı hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-148">In this example, **myaccount** is hello name of hello Azure Batch account.</span></span> <span data-ttu-id="4cdd1-149">Merhaba bağlantılı hizmet tanımında kullandığınız URI hello hesabının hello adı olmadan hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-149">URI you use in hello linked service definition is hello URL without hello name of hello account.</span></span> <span data-ttu-id="4cdd1-150">Örneğin: `https://<region>.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-150">For example: `https://<region>.batch.azure.com`.</span></span>
    2. <span data-ttu-id="4cdd1-151">Tıklatın **anahtarları** hello soldaki menüden ve kopyalama hello **birincil erişim ANAHTARINI**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-151">Click **Keys** on hello left menu, and copy hello **PRIMARY ACCESS KEY**.</span></span>
    3. <span data-ttu-id="4cdd1-152">toouse var olan bir havuzu tıklatın **havuzları** hello menü ve hello Not **kimliği** hello havuzunun.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-152">toouse an existing pool, click **Pools** on hello menu, and note down hello **ID** of hello pool.</span></span> <span data-ttu-id="4cdd1-153">Var olan bir havuzu sahip değilseniz, sonraki adıma toohello taşıyın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-153">If you don't have an existing pool, move toohello next step.</span></span>     
2. <span data-ttu-id="4cdd1-154">Oluşturma bir **Azure Batch havuzu**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-154">Create an **Azure Batch pool**.</span></span>

   1. <span data-ttu-id="4cdd1-155">Merhaba, [Azure portal](https://portal.azure.com), tıklatın **Gözat** hello soldaki menüden ve'ı tıklatın **toplu işlem hesaplarını**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-155">In hello [Azure portal](https://portal.azure.com), click **Browse** in hello left menu, and click **Batch Accounts**.</span></span>
   2. <span data-ttu-id="4cdd1-156">Azure Batch hesabı tooopen hello seçin **toplu işlem hesabı** dikey.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-156">Select your Azure Batch account tooopen hello **Batch Account** blade.</span></span>
   3. <span data-ttu-id="4cdd1-157">Tıklatın **havuzları** döşeme.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-157">Click **Pools** tile.</span></span>
   4. <span data-ttu-id="4cdd1-158">Merhaba, **havuzları** dikey penceresinde hello araç tooadd bir havuzu Ekle düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-158">In hello **Pools** blade, click Add button on hello toolbar tooadd a pool.</span></span>
      1. <span data-ttu-id="4cdd1-159">Bir kimlik hello havuzu (havuzu kimliği) girin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-159">Enter an ID for hello pool (Pool ID).</span></span> <span data-ttu-id="4cdd1-160">Not hello **hello havuzun kimliği**; hello Data Factory çözüm oluşturulurken gerekir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-160">Note hello **ID of hello pool**; you need it when creating hello Data Factory solution.</span></span>
      2. <span data-ttu-id="4cdd1-161">Belirtin **Windows Server 2012 R2** hello işletim sistemi ailesi ayarı için.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-161">Specify **Windows Server 2012 R2** for hello Operating System Family setting.</span></span>
      3. <span data-ttu-id="4cdd1-162">Seçin bir **düğüm fiyatlandırma katmanı**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-162">Select a **node pricing tier**.</span></span>
      4. <span data-ttu-id="4cdd1-163">Girin **2** hello için değer olarak **hedef ayrılmış** ayarı.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-163">Enter **2** as value for hello **Target Dedicated** setting.</span></span>
      5. <span data-ttu-id="4cdd1-164">Girin **2** hello için değer olarak **en fazla düğüm başına görevleri** ayarı.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-164">Enter **2** as value for hello **Max tasks per node** setting.</span></span>
   5. <span data-ttu-id="4cdd1-165">Tıklatın **Tamam** toocreate hello havuzu.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-165">Click **OK** toocreate hello pool.</span></span>
   6. <span data-ttu-id="4cdd1-166">Merhaba Not **kimliği** hello havuzunun.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-166">Note down hello **ID** of hello pool.</span></span> 



### <a name="high-level-steps"></a><span data-ttu-id="4cdd1-167">Üst düzey adımlar</span><span class="sxs-lookup"><span data-stu-id="4cdd1-167">High-level steps</span></span>
<span data-ttu-id="4cdd1-168">Bu kılavuz kapsamında gerçekleştirme hello iki üst düzey adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-168">Here are hello two high-level steps you perform as part of this walkthrough:</span></span> 

1. <span data-ttu-id="4cdd1-169">Basit veri dönüştürme/işleme mantığı içeren özel bir aktivite oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-169">Create a custom activity that contains simple data transformation/processing logic.</span></span>
2. <span data-ttu-id="4cdd1-170">Bir Azure data factory hello özel etkinlik kullanan bir sahip işlem hattı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-170">Create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

### <a name="create-a-custom-activity"></a><span data-ttu-id="4cdd1-171">Özel etkinlik oluşturma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-171">Create a custom activity</span></span>
<span data-ttu-id="4cdd1-172">toocreate .NET özel etkinlik oluşturmak bir **.NET sınıf kitaplığı** uygulayan bir sınıf projeyle **IDotNetActivity** arabirimi.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-172">toocreate a .NET custom activity, create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="4cdd1-173">Bu arabirim yalnızca bir yöntemi vardır: [yürütme](https://msdn.microsoft.com/library/azure/mt603945.aspx) ve imzası:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-173">This interface has only one method: [Execute](https://msdn.microsoft.com/library/azure/mt603945.aspx) and its signature is:</span></span>

```csharp
public IDictionary<string, string> Execute(
        IEnumerable<LinkedService> linkedServices,
        IEnumerable<Dataset> datasets,
        Activity activity,
        IActivityLogger logger)
```


<span data-ttu-id="4cdd1-174">Merhaba yöntemi dört parametreleri alır:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-174">hello method takes four parameters:</span></span>

- <span data-ttu-id="4cdd1-175">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-175">**linkedServices**.</span></span> <span data-ttu-id="4cdd1-176">Bu özellik, veri deposu bağlı Hizmetleri hello etkinlik için giriş/çıkış veri kümesi tarafından başvurulan numaralandırılabilir listesidir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-176">This property is an enumerable list of Data Store linked services referenced by input/output datasets for hello activity.</span></span>   
- <span data-ttu-id="4cdd1-177">**veri kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-177">**datasets**.</span></span> <span data-ttu-id="4cdd1-178">Bu özellik hello etkinlik için giriş/çıkış veri kümesi numaralandırılabilir bir listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-178">This property is an enumerable list of input/output datasets for hello activity.</span></span> <span data-ttu-id="4cdd1-179">Bu parametre tooget hello konumları ve girdi ve çıktı veri kümeleri tarafından tanımlanan şemaları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-179">You can use this parameter tooget hello locations and schemas defined by input and output datasets.</span></span>
- <span data-ttu-id="4cdd1-180">**Etkinlik**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-180">**activity**.</span></span> <span data-ttu-id="4cdd1-181">Bu özellik hello geçerli etkinliği temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-181">This property represents hello current activity.</span></span> <span data-ttu-id="4cdd1-182">Kullanılan tooaccess genişletilmiş özellikler hello özel etkinlik ile ilişkili olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-182">It can be used tooaccess extended properties associated with hello custom activity.</span></span> <span data-ttu-id="4cdd1-183">Bkz: [genişletilmiş özellikler erişim](#access-extended-properties) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-183">See [Access extended properties](#access-extended-properties) for details.</span></span>
- <span data-ttu-id="4cdd1-184">**Günlükçü**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-184">**logger**.</span></span> <span data-ttu-id="4cdd1-185">Bu nesne hello ardışık düzeni için başlangıç kullanıcı günlüğünde bu yüzeyini hata ayıklama açıklamaları yazmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-185">This object lets you write debug comments that surface in hello user log for hello pipeline.</span></span>

<span data-ttu-id="4cdd1-186">Merhaba yöntemi kullanılan toochain özel etkinlikler birlikte hello gelecekte olabilir bir sözlüğü döndürür.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-186">hello method returns a dictionary that can be used toochain custom activities together in hello future.</span></span> <span data-ttu-id="4cdd1-187">Bu özellik henüz uygulanmadı, bu nedenle boş bir sözlük hello döndürme.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-187">This feature is not implemented yet, so return an empty dictionary from hello method.</span></span>  

### <a name="procedure"></a><span data-ttu-id="4cdd1-188">Yordam</span><span class="sxs-lookup"><span data-stu-id="4cdd1-188">Procedure</span></span>
1. <span data-ttu-id="4cdd1-189">Oluşturma bir **.NET sınıf kitaplığı** projesi.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-189">Create a **.NET Class Library** project.</span></span>
   <ol type="a">
     <li><span data-ttu-id="4cdd1-190">Başlatma <b>Visual Studio 2017</b> veya <b>Visual Studio 2015</b> veya <b>Visual Studio 2013'ün</b> veya <b>Visual Studio 2012</b>.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-190">Launch <b>Visual Studio 2017</b> or <b>Visual Studio 2015</b> or <b>Visual Studio 2013</b> or <b>Visual Studio 2012</b>.</span></span></li>
     <li><span data-ttu-id="4cdd1-191">Tıklatın <b>dosya</b>, çok noktası<b>yeni</b>, tıklatıp <b>proje</b>.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-191">Click <b>File</b>, point too<b>New</b>, and click <b>Project</b>.</span></span></li>
     <li><span data-ttu-id="4cdd1-192"><b>Şablonlar</b>’ı genişletin ve <b>Visual C#</b> seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-192">Expand <b>Templates</b>, and select <b>Visual C#</b>.</span></span> <span data-ttu-id="4cdd1-193">Bu kılavuzda, C# kullanın, ancak .NET dil toodevelop hello özel etkinlik kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-193">In this walkthrough, you use C#, but you can use any .NET language toodevelop hello custom activity.</span></span></li>
     <li><span data-ttu-id="4cdd1-194">Seçin <b>sınıf kitaplığı</b> hello sağ proje türlerinde hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-194">Select <b>Class Library</b> from hello list of project types on hello right.</span></span> <span data-ttu-id="4cdd1-195">VS 2017 ' seçin <b>sınıf kitaplığı (.NET Framework)</b> </span><span class="sxs-lookup"><span data-stu-id="4cdd1-195">In VS 2017, choose <b>Class Library (.NET Framework)</b> </span></span></li>
     <li><span data-ttu-id="4cdd1-196">Girin <b>MyDotNetActivity</b> hello için <b>adı</b>.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-196">Enter <b>MyDotNetActivity</b> for hello <b>Name</b>.</span></span></li>
     <li><span data-ttu-id="4cdd1-197">Seçin <b>C:\ADFGetStarted</b> hello için <b>konumu</b>.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-197">Select <b>C:\ADFGetStarted</b> for hello <b>Location</b>.</span></span></li>
     <li><span data-ttu-id="4cdd1-198">Tıklatın <b>Tamam</b> toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-198">Click <b>OK</b> toocreate hello project.</span></span></li>
   </ol><span data-ttu-id="4cdd1-199">
2.Tıklatın **Araçları**, çok noktası**NuGet Paket Yöneticisi**, tıklatıp **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-199">
2. Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
<span data-ttu-id="4cdd1-200">3.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-200">3.</span></span> <span data-ttu-id="4cdd1-201">Komut tooimport aşağıdaki hello Hello Paket Yöneticisi konsolu, yürütme **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-201">In hello Package Manager Console, execute hello following command tooimport **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```PowerShell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="4cdd1-202">İçeri aktarma hello **Azure Storage** toohello projesinde NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-202">Import hello **Azure Storage** NuGet package in toohello project.</span></span>

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="4cdd1-203">Veri Fabrikası Başlatıcı WindowsAzure.Storage hello 4.3 sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-203">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="4cdd1-204">Bir başvuru tooa eklerseniz, sonraki bir sürümünü özel etkinlik projenizdeki Azure Storage derlemenin hata hello etkinlik yürüttüğünde bakın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-204">If you add a reference tooa later version of Azure Storage assembly in your custom activity project, you see an error when hello activity executes.</span></span> <span data-ttu-id="4cdd1-205">tooresolve hello hata bkz [Appdomain yalıtım](#appdomain-isolation) bölümü.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-205">tooresolve hello error, see [Appdomain isolation](#appdomain-isolation) section.</span></span> 
5. <span data-ttu-id="4cdd1-206">Merhaba aşağıdakileri ekleyin **kullanarak** deyimleri toohello kaynak hello proje dosyasında.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-206">Add hello following **using** statements toohello source file in hello project.</span></span>

    ```csharp

    // Comment these lines if using VS 2017
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    // --------------------

    // Comment these lines if using <= VS 2015
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    // ---------------------

    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;

    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
6. <span data-ttu-id="4cdd1-207">Değişiklik hello hello adını **ad alanı** çok**MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-207">Change hello name of hello **namespace** too**MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="4cdd1-208">Merhaba sınıfı Hello adı çok değiştirmek**MyDotNetActivity** ve hello türetilen **IDotNetActivity** arabirim hello aşağıdaki kod parçacığında gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-208">Change hello name of hello class too**MyDotNetActivity** and derive it from hello **IDotNetActivity** interface as shown in hello following code snippet:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="4cdd1-209">Uygulama (Ekle) hello **yürütme** hello yöntemi **IDotNetActivity** toohello arabirim **MyDotNetActivity** örnek kodu toohello yöntemi aşağıdaki sınıf ve kopyalama hello.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-209">Implement (Add) hello **Execute** method of hello **IDotNetActivity** interface toohello **MyDotNetActivity** class and copy hello following sample code toohello method.</span></span>

    <span data-ttu-id="4cdd1-210">Merhaba aşağıdaki örnek hello hello arama terimi ("Microsoft") oluşumları veri dilimi ile ilişkili her bir blob içinde sayar.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-210">hello following sample counts hello number of occurrences of hello search term (“Microsoft”) in each blob associated with a data slice.</span></span>

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
        // get extended properties defined in activity JSON definition
        // (for example: SliceStart)
        DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
        string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];
    
        // toolog information, use hello logger object
        // log all extended properties            
        IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
        logger.Write("Logging extended properties if any...");
        foreach (KeyValuePair<string, string> entry in extendedProperties)
        {
            logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
        }
    
        // linked service for input and output data stores
        // in this example, same storage is used for both input/output
        AzureStorageLinkedService inputLinkedService;

        // get hello input dataset
        Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
        // declare variables toohold type properties of input/output datasets
        AzureBlobDataset inputTypeProperties, outputTypeProperties;
        
        // get type properties from hello dataset object
        inputTypeProperties = inputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // log linked services passed in linkedServices parameter
        // you will see two linked services of type: AzureStorage
        // one for input dataset and hello other for output dataset 
        foreach (LinkedService ls in linkedServices)
            logger.Write("linkedService.Name {0}", ls.Name);
    
        // get hello first Azure Storate linked service from linkedServices object
        // using First method instead of Single since we are using hello same
        // Azure Storage linked service for input and output.
        inputLinkedService = linkedServices.First(
            linkedService =>
            linkedService.Name ==
            inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
            as AzureStorageLinkedService;
    
        // get hello connection string in hello linked service
        string connectionString = inputLinkedService.ConnectionString;
    
        // get hello folder path from hello input dataset definition
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
               // with hello data slice. definition of hello method is shown in hello next step.
    
            output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
        } while (continuationToken != null);
    
        // get hello output dataset using hello name of hello dataset matched tooa name in hello Activity output collection.
        Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);

        // get type properties for hello output dataset
        outputTypeProperties = outputDataset.Properties.TypeProperties as AzureBlobDataset;
    
        // get hello folder path from hello output dataset definition
        folderPath = GetFolderPath(outputDataset);

        // log hello output folder path 
        logger.Write("Writing blob toohello folder: {0}", folderPath);
    
        // create a storage object for hello output blob.
        CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
        // write hello name of hello file.
        Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
        // log hello output file name
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
9. <span data-ttu-id="4cdd1-211">Yardımcı yöntemler aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-211">Add hello following helper methods:</span></span> 

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

        // get type properties of hello dataset 
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello folder path found in hello type properties
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
    
        // get type properties of hello dataset
        AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
        if (blobDataset == null)
        {
            return null;
        }
    
        // return hello blob/file name in hello type properties
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

    <span data-ttu-id="4cdd1-212">dataset hello hello GetFolderPath yöntemi döndürür hello yolu toohello klasörü tooand hello GetFileName yöntemi döndürür hello hello blob/dataset noktalarına hello dosyasının adını işaret eder.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-212">hello GetFolderPath method returns hello path toohello folder that hello dataset points tooand hello GetFileName method returns hello name of hello blob/file that hello dataset points to.</span></span> <span data-ttu-id="4cdd1-213">{Year} gibi değişkenler kullanarak, havefolderPath tanımlıyorsa {Month}, {Day} vb., hello yöntemi döndürür hello dizesi çalışma zamanı değerlerle değiştirmeden olduğu gibi.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-213">If you havefolderPath defines using variables such as {Year}, {Month}, {Day} etc., hello method returns hello string as it is without replacing them with runtime values.</span></span> <span data-ttu-id="4cdd1-214">Bkz: [genişletilmiş özellikler erişim](#access-extended-properties) erişme SliceStart, SliceEnd, vb. ile ilgili ayrıntılar için bölüm.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-214">See [Access extended properties](#access-extended-properties) section for details on accessing SliceStart, SliceEnd, etc.</span></span>    

    ```JSON
    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "adftutorial/inputfolder/",
    ```

    <span data-ttu-id="4cdd1-215">Merhaba hesapla yöntemi hello anahtar sözcüğü hello giriş dosyaları (BLOB hello klasöründe) Microsoft örneklerinin sayısını hesaplar.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-215">hello Calculate method calculates hello number of instances of keyword Microsoft in hello input files (blobs in hello folder).</span></span> <span data-ttu-id="4cdd1-216">Merhaba kodda sabit kodlanmış Hello arama terimi ("Microsoft").</span><span class="sxs-lookup"><span data-stu-id="4cdd1-216">hello search term (“Microsoft”) is hard-coded in hello code.</span></span>
10. <span data-ttu-id="4cdd1-217">Merhaba projeyi derleyin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-217">Compile hello project.</span></span> <span data-ttu-id="4cdd1-218">Tıklatın **yapı** hello menüsüne ve ardından gelen **yapı çözümü**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-218">Click **Build** from hello menu and click **Build Solution**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4cdd1-219">Projeniz için hello hedef çerçeve olarak .NET Framework 4.5.2 kümesi sürümü: hello projesine sağ tıklayın ve **özellikleri** tooset hello hedef çerçevesi.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-219">Set 4.5.2 version of .NET Framework as hello target framework for your project: right-click hello project, and click **Properties** tooset hello target framework.</span></span> <span data-ttu-id="4cdd1-220">Veri Fabrikası karşı .NET Framework sürüm 4.5.2 daha sonra derlenmiş özel etkinlikler desteklemez.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-220">Data Factory does not support custom activities compiled against .NET Framework versions later than 4.5.2.</span></span>

11. <span data-ttu-id="4cdd1-221">Başlatma **Windows Explorer**, giderek çok**bin\debug** veya **bin\release** klasör yapısının hello türüne bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-221">Launch **Windows Explorer**, and navigate too**bin\debug** or **bin\release** folder depending on hello type of build.</span></span>
12. <span data-ttu-id="4cdd1-222">Zip dosyası oluşturma **MyDotNetActivity.zip** hello içindeki tüm hello ikili dosyaları içeren <project folder>\bin\Debug klasörünü.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-222">Create a zip file **MyDotNetActivity.zip** that contains all hello binaries in hello <project folder>\bin\Debug folder.</span></span> <span data-ttu-id="4cdd1-223">Merhaba dahil **MyDotNetActivity.pdb** başarısız olduysa, hello soruna neden hello kaynak kodunda satır numarası gibi ek ayrıntıları almak için dosya.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-223">Include hello **MyDotNetActivity.pdb** file so that you get additional details such as line number in hello source code that caused hello issue if there was a failure.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="4cdd1-224">Merhaba özel etkinlik hello olmalıdır tüm dosyaları hello zip dosyasında hello **üst düzey** hiçbir alt klasörler ile.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-224">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>

    ![İkili çıktı dosyaları](./media/data-factory-use-custom-activities/Binaries.png)
14. <span data-ttu-id="4cdd1-226">Adlı bir blob kapsayıcı oluşturun **customactivitycontainer** zaten yoksa.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-226">Create a blob container named **customactivitycontainer** if it does not already exist.</span></span> 
15. <span data-ttu-id="4cdd1-227">İçinde bir blob toohello customactivitycontainer olarak MyDotNetActivity.zip karşıya bir **genel amaçlı** AzureStorageLinkedService tarafından başvurulan Azure blob storage (değil seyrek/cool Blob Depolama).</span><span class="sxs-lookup"><span data-stu-id="4cdd1-227">Upload MyDotNetActivity.zip as a blob toohello customactivitycontainer in a **general-purpose** Azure blob storage (not hot/cool Blob storage) that is referred by AzureStorageLinkedService.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="4cdd1-228">Visual Studio'da bir Data Factory projesi içeren bu .NET etkinliği proje tooa çözümü ekleyin ve bir başvuru too.NET etkinlik proje hello Data Factory uygulama projeden eklerseniz, el ile oluşturma tooperform hello son iki adımı gerekmez Merhaba zip dosyası ve toohello genel amaçlı Azure blob depolama karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-228">If you add this .NET activity project tooa solution in Visual Studio that contains a Data Factory project, and add a reference too.NET activity project from hello Data Factory application project, you do not need tooperform hello last two steps of manually creating hello zip file and uploading it toohello general-purpose Azure blob storage.</span></span> <span data-ttu-id="4cdd1-229">Visual Studio kullanarak Data Factory varlıklarını yayımladığınızda, şu adımları yayımlama hello işlem tarafından otomatik olarak yapılır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-229">When you publish Data Factory entities using Visual Studio, these steps are automatically done by hello publishing process.</span></span> <span data-ttu-id="4cdd1-230">Daha fazla bilgi için bkz: [Visual Studio Data Factory projesindeki](#data-factory-project-in-visual-studio) bölümü.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-230">For more information, see [Data Factory project in Visual Studio](#data-factory-project-in-visual-studio) section.</span></span>

## <a name="create-a-pipeline-with-custom-activity"></a><span data-ttu-id="4cdd1-231">Özel etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-231">Create a pipeline with custom activity</span></span>
<span data-ttu-id="4cdd1-232">Özel bir aktivite oluşturulur ve hello ZIP dosyasının ikilileri tooa blob kapsayıcısında ile karşıya bir **genel amaçlı** Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-232">You have created a custom activity and uploaded hello zip file with binaries tooa blob container in a **general-purpose** Azure Storage Account.</span></span> <span data-ttu-id="4cdd1-233">Bu bölümde, bir Azure data factory hello özel etkinlik kullanan sahip işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-233">In this section, you create an Azure data factory with a pipeline that uses hello custom activity.</span></span>

<span data-ttu-id="4cdd1-234">Merhaba hello özel etkinlik için giriş veri kümesi hello blob depolamada adftutorial kapsayıcısının hello customactivityinput klasöründeki BLOB'lar (dosyaları) temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-234">hello input dataset for hello custom activity represents blobs (files) in hello customactivityinput folder of adftutorial container in hello blob storage.</span></span> <span data-ttu-id="4cdd1-235">Merhaba çıktı veri kümesi hello etkinliğinin çıkış BLOB'lar hello blob depolamada adftutorial kapsayıcısının hello customactivityoutput klasöründeki temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-235">hello output dataset for hello activity represents output blobs in hello customactivityoutput folder of adftutorial container in hello blob storage.</span></span>

<span data-ttu-id="4cdd1-236">Oluşturma **dosya.txt'yi** aşağıdaki içerik ve çok karşıya hello dosyasıyla**customactivityinput** hello klasörünü **adftutorial** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-236">Create **file.txt** file with hello following content and upload it too**customactivityinput** folder of hello **adftutorial** container.</span></span> <span data-ttu-id="4cdd1-237">Zaten yoksa hello adftutorial kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-237">Create hello adftutorial container if it does not exist already.</span></span> 

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="4cdd1-238">Başlangıç klasörü iki veya daha fazla dosya olsa bile hello giriş klasörü Azure Data Factory tooa dilimi karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-238">hello input folder corresponds tooa slice in Azure Data Factory even if hello folder has two or more files.</span></span> <span data-ttu-id="4cdd1-239">Her dilim hello ardışık düzen tarafından işlendiğinde hello özel etkinlik bu dilim için hello giriş klasöründeki tüm hello BLOB'lar dolaşır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-239">When each slice is processed by hello pipeline, hello custom activity iterates through all hello blobs in hello input folder for that slice.</span></span>

<span data-ttu-id="4cdd1-240">Bir veya daha fazla satırlara sahip (Merhaba giriş klasörü blobları sayısı ile aynı) dosyası ile Merhaba adftutorial\customactivityoutput klasöründe bir çıkış bakın:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-240">You see one output file with in hello adftutorial\customactivityoutput folder with one or more lines (same as number of blobs in hello input folder):</span></span>

```
2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
```


<span data-ttu-id="4cdd1-241">Bu bölümde gerçekleştirmek hello adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-241">Here are hello steps you perform in this section:</span></span>

1. <span data-ttu-id="4cdd1-242">Oluşturma bir **veri fabrikası**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-242">Create a **data factory**.</span></span>
2. <span data-ttu-id="4cdd1-243">Oluşturma **bağlantılı Hizmetleri** hello Azure Batch havuzu Hangi hello özel etkinlik çalıştırır ve giriş/çıkış BLOB'lar hello tutan Azure Storage hello VM'ler için.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-243">Create **Linked services** for hello Azure Batch pool of VMs on which hello custom activity runs and hello Azure Storage that holds hello input/output blobs.</span></span>
3. <span data-ttu-id="4cdd1-244">Giriş ve çıkış oluşturma **veri kümeleri** giriş ve çıkış hello özel etkinliği temsil eden.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-244">Create input and output **datasets** that represent input and output of hello custom activity.</span></span>
4. <span data-ttu-id="4cdd1-245">Oluşturma bir **ardışık düzen** hello özel etkinlik kullanır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-245">Create a **pipeline** that uses hello custom activity.</span></span>

> [!NOTE]
> <span data-ttu-id="4cdd1-246">Merhaba oluşturma **dosya.txt'yi** ve zaten yapmadıysanız tooa blob kapsayıcısı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-246">Create hello **file.txt** and upload it tooa blob container if you haven't already done so.</span></span> <span data-ttu-id="4cdd1-247">Önceki bölümde hello bulunan yönergelere bakın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-247">See instructions in hello preceding section.</span></span>   

### <a name="step-1-create-hello-data-factory"></a><span data-ttu-id="4cdd1-248">1. adım: hello veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-248">Step 1: Create hello data factory</span></span>
1. <span data-ttu-id="4cdd1-249">Azure portalı içinde toohello oturum sonra aşağıdaki adımları hello:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-249">After logging in toohello Azure portal, do hello following steps:</span></span>
   1. <span data-ttu-id="4cdd1-250">Tıklatın **yeni** hello sol menüdeki.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-250">Click **NEW** on hello left menu.</span></span>
   2. <span data-ttu-id="4cdd1-251">Tıklatın **veri + analiz** hello içinde **yeni** dikey.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-251">Click **Data + Analytics** in hello **New** blade.</span></span>
   3. <span data-ttu-id="4cdd1-252">Tıklatın **Data Factory** hello üzerinde **veri analizi** dikey.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-252">Click **Data Factory** on hello **Data analytics** blade.</span></span>
   
    ![Yeni Azure Data Factory menüsü](media/data-factory-use-custom-activities/new-azure-data-factory-menu.png)
2. <span data-ttu-id="4cdd1-254">Merhaba, **yeni data factory** dikey penceresinde girin **CustomActivityFactory** hello adı için.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-254">In hello **New data factory** blade, enter **CustomActivityFactory** for hello Name.</span></span> <span data-ttu-id="4cdd1-255">Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-255">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="4cdd1-256">Merhaba hatayı alırsanız: **veri fabrikası adı "CustomActivityFactory" kullanılabilir değil**, hello veri fabrikası hello adını değiştirin (örneğin, **yournameCustomActivityFactory**) ve oluşturmayı deneyin yeniden.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-256">If you receive hello error: **Data factory name “CustomActivityFactory” is not available**, change hello name of hello data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>

    ![Yeni Azure Data Factory dikey penceresi](media/data-factory-use-custom-activities/new-azure-data-factory-blade.png)
3. <span data-ttu-id="4cdd1-258">Tıklatın **kaynak grubu adı**, varolan bir kaynak grubu seçin veya bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-258">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="4cdd1-259">Merhaba doğru kullandığınızdan emin olun **abonelik** ve **bölge** oluşturulan hello veri fabrikası toobe istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-259">Verify that you are using hello correct **subscription** and **region** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="4cdd1-260">Tıklatın **oluşturma** hello üzerinde **yeni data factory** dikey.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-260">Click **Create** on hello **New data factory** blade.</span></span>
6. <span data-ttu-id="4cdd1-261">Hello oluşturulmakta hello veri fabrikası gördüğünüz **Pano** hello Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-261">You see hello data factory being created in hello **Dashboard** of hello Azure portal.</span></span>
7. <span data-ttu-id="4cdd1-262">Merhaba veri fabrikası başarıyla oluşturulduktan sonra gösterir hello Data Factory dikey bkz hello hello data Factory içeriği.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-262">After hello data factory has been created successfully, you see hello Data Factory blade, which shows you hello contents of hello data factory.</span></span>
    
    ![Data Factory dikey penceresi](media/data-factory-use-custom-activities/data-factory-blade.png)

### <a name="step-2-create-linked-services"></a><span data-ttu-id="4cdd1-264">2. adım: bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-264">Step 2: Create linked services</span></span>
<span data-ttu-id="4cdd1-265">Bağlı hizmetler veri depolarını veya hizmetleri tooan Azure data factory işlem.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-265">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="4cdd1-266">Bu adımda, Azure Storage hesabını ve Azure Batch hesabı tooyour veri fabrikası bağlayın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-266">In this step, you link your Azure Storage account and Azure Batch account tooyour data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="4cdd1-267">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-267">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="4cdd1-268">Merhaba tıklatın **yazar ve dağıtma** döşeme hello üzerinde **DATA FACTORY** dikey **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-268">Click hello **Author and deploy** tile on hello **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="4cdd1-269">Merhaba Data Factory Düzenleyici bakın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-269">You see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="4cdd1-270">Tıklatın **yeni veri deposu** hello komut çubuğu ve seçin **Azure depolama**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-270">Click **New data store** on hello command bar and choose **Azure storage**.</span></span> <span data-ttu-id="4cdd1-271">Görmeniz gerekir hello Azure depolama alanı oluşturmak için JSON betiği bağlantılı hizmeti hello düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-271">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>
    
    ![Yeni veri deposu - Azure depolama](media/data-factory-use-custom-activities/new-data-store-menu.png)
3. <span data-ttu-id="4cdd1-273">Değiştir `<accountname>` Azure depolama hesabınızın adıyla ve `<accountkey>` hello Azure depolama hesabı erişim anahtarı ile.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-273">Replace `<accountname>` with name of your Azure storage account and `<accountkey>` with access key of hello Azure storage account.</span></span> <span data-ttu-id="4cdd1-274">toolearn tooget depolama alanınızın nasıl erişim anahtar, bkz: [erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma depolama](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4cdd1-274">toolearn how tooget your storage access key, see [View, copy and regenerate storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

    ![Azure depolama hizmeti beğendiğinizi](media/data-factory-use-custom-activities/azure-storage-linked-service.png)
4. <span data-ttu-id="4cdd1-276">Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-276">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="4cdd1-277">Azure Batch bağlı hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-277">Create Azure Batch linked service</span></span>
1. <span data-ttu-id="4cdd1-278">Hello Data Factory Düzenleyici'de, tıklatın **... Daha fazla** hello komut çubuğunda **yeni işlem**ve ardından **Azure Batch** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-278">In hello Data Factory Editor, click **... More** on hello command bar, click **New compute**, and then select **Azure Batch** from hello menu.</span></span>

    ![Yeni işlem - Azure toplu işlem](media/data-factory-use-custom-activities/new-azure-compute-batch.png)
2. <span data-ttu-id="4cdd1-280">Değişiklikleri toohello JSON betiği aşağıdaki hello olun:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-280">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="4cdd1-281">Hello için Azure Batch hesabı adı belirtin **accountName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-281">Specify Azure Batch account name for hello **accountName** property.</span></span> <span data-ttu-id="4cdd1-282">Merhaba **URL** hello gelen **Azure Batch hesabı dikey** biçimini izleyen hello olduğu: `http://accountname.region.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-282">hello **URL** from hello **Azure Batch account blade** is in hello following format: `http://accountname.region.batch.azure.com`.</span></span> <span data-ttu-id="4cdd1-283">Hello için **batchUri** özelliğinde hello JSON, tooremove gerek `accountname.` hello URL ve kullanım hello gelen `accountname` hello için `accountName` JSON özelliği.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-283">For hello **batchUri** property in hello JSON, you need tooremove `accountname.` from hello URL and use hello `accountname` for hello `accountName` JSON property.</span></span>
   2. <span data-ttu-id="4cdd1-284">Merhaba Hello Azure Batch hesabı anahtar belirtmeniz **accessKey** özelliği.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-284">Specify hello Azure Batch account key for hello **accessKey** property.</span></span>
   3. <span data-ttu-id="4cdd1-285">Merhaba önkoşulları bir parçası olarak oluşturduğunuz hello havuzunu Hello adını belirtin **poolName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-285">Specify hello name of hello pool you created as part of prerequisites for hello **poolName** property.</span></span> <span data-ttu-id="4cdd1-286">Hello hello havuzu hello havuzunun hello adı yerine Kimliğini de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-286">You can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>
   4. <span data-ttu-id="4cdd1-287">Azure Batch URI Merhaba belirtin **batchUri** özelliği.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-287">Specify Azure Batch URI for hello **batchUri** property.</span></span> <span data-ttu-id="4cdd1-288">Örnek: `https://westus.batch.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-288">Example: `https://westus.batch.azure.com`.</span></span>  
   5. <span data-ttu-id="4cdd1-289">Merhaba belirtin **AzureStorageLinkedService** hello için **linkedServiceName** özelliği.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-289">Specify hello **AzureStorageLinkedService** for hello **linkedServiceName** property.</span></span>

        ```json
        {
         "name": "AzureBatchLinkedService",
         "properties": {
           "type": "AzureBatch",
           "typeProperties": {
             "accountName": "myazurebatchaccount",
             "batchUri": "https://westus.batch.azure.com",
             "accessKey": "<yourbatchaccountkey>",
             "poolName": "myazurebatchpool",
             "linkedServiceName": "AzureStorageLinkedService"
           }
         }
        }
        ```

       <span data-ttu-id="4cdd1-290">Hello için **poolName** özelliği, hello hello havuzu hello havuzunun hello adı yerine Kimliğini de belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-290">For hello **poolName** property, you can also specify hello ID of hello pool instead of hello name of hello pool.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="4cdd1-291">Hdınsight için yaptığı gibi hello Data Factory hizmeti Azure toplu işlem için bir isteğe bağlı seçeneği desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-291">hello Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="4cdd1-292">Bu gibi durumlarda, kendi Azure Batch havuzu yalnızca bir Azure data factory kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-292">You can only use your own Azure Batch pool in an Azure data factory.</span></span>   
    

### <a name="step-3-create-datasets"></a><span data-ttu-id="4cdd1-293">3. adım: veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-293">Step 3: Create datasets</span></span>
<span data-ttu-id="4cdd1-294">Bu adımda, veri kümeleri toorepresent girişi oluşturun ve çıktı verilerini.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-294">In this step, you create datasets toorepresent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="4cdd1-295">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-295">Create input dataset</span></span>
1. <span data-ttu-id="4cdd1-296">Merhaba, **Düzenleyicisi** hello Data Factory tıklatın **... Daha fazla** hello komut çubuğunda **yeni veri kümesi**ve ardından **Azure Blob Depolama** hello açılan menüsünden.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-296">In hello **Editor** for hello Data Factory, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage** from hello drop-down menu.</span></span>
2. <span data-ttu-id="4cdd1-297">Merhaba JSON hello sağ bölmedeki JSON parçacığı aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-297">Replace hello JSON in hello right pane with hello following JSON snippet:</span></span>

    ```json
    {
     "name": "InputDataset",
     "properties": {
         "type": "AzureBlob",
         "linkedServiceName": "AzureStorageLinkedService",
         "typeProperties": {
             "folderPath": "adftutorial/customactivityinput/",
             "format": {
                 "type": "TextFormat"
             }
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

   <span data-ttu-id="4cdd1-298">Başlangıç saati ile bu kılavuzda daha sonra bir işlem hattı oluşturma: 2016-11-16T00:00:00Z ve bitiş zamanı: 2016-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-298">You create a pipeline later in this walkthrough with start time: 2016-11-16T00:00:00Z and end time: 2016-11-16T05:00:00Z.</span></span> <span data-ttu-id="4cdd1-299">Beş giriş/çıkış dilimler olduklarından, zamanlanmış tooproduce saatlik, verilerdir (arasında **00**: 00:00 -> **05**: 00:00).</span><span class="sxs-lookup"><span data-stu-id="4cdd1-299">It is scheduled tooproduce data hourly, so there are five input/output slices (between **00**:00:00 -> **05**:00:00).</span></span>

   <span data-ttu-id="4cdd1-300">Merhaba **sıklığı** ve **aralığı** hello girdi veri kümesi çok ayarlamak için**saat** ve **1**, o hello başka bir deyişle, dilim kullanılabilir giriş saatlik.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-300">hello **frequency** and **interval** for hello input dataset is set too**Hour** and **1**, which means that hello input slice is available hourly.</span></span> <span data-ttu-id="4cdd1-301">Bu örnekte, aynı hello olduğu hello intputfolder (dosya.txt'yi) dosyasında.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-301">In this sample, it is hello same file (file.txt) in hello intputfolder.</span></span>

   <span data-ttu-id="4cdd1-302">Burada, JSON parçacığı yukarıda hello SliceStart sistem değişkeni tarafından temsil edilen her dilim için hello başlangıç zamanlarını bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-302">Here are hello start times for each slice, which is represented by SliceStart system variable in hello above JSON snippet.</span></span>
3. <span data-ttu-id="4cdd1-303">Tıklatın **dağıtma** araç toocreate hello ve hello dağıtmak **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-303">Click **Deploy** on hello toolbar toocreate and deploy hello **InputDataset**.</span></span> <span data-ttu-id="4cdd1-304">Merhaba gördüğünüzü onaylayın **tablo başarıyla oluşturuldu** hello başlık çubuğundaki hello Düzenleyicisi ileti.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-304">Confirm that you see hello **TABLE CREATED SUCCESSFULLY** message on hello title bar of hello Editor.</span></span>

#### <a name="create-an-output-dataset"></a><span data-ttu-id="4cdd1-305">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-305">Create an output dataset</span></span>
1. <span data-ttu-id="4cdd1-306">Merhaba, **Data Factory düzenleyici**, tıklatın **... Daha fazla** hello komut çubuğunda **yeni veri kümesi**ve ardından **Azure Blob Depolama**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-306">In hello **Data Factory editor**, click **... More** on hello command bar, click **New dataset**, and then select **Azure Blob storage**.</span></span>
2. <span data-ttu-id="4cdd1-307">Merhaba JSON betiği hello sağ bölmedeki JSON betiği aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-307">Replace hello JSON script in hello right pane with hello following JSON script:</span></span>

    ```JSON
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "{slice}.txt",
                "folderPath": "adftutorial/customactivityoutput/",
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

     <span data-ttu-id="4cdd1-308">Çıktı konumu **adftutorial/customactivityoutput/** ve çıktı dosyası adını yyyy-aa-gg-HH.txt yyyy-aa-gg-HH hello yıl, ay, tarih ve saat üretilen hello dilimin olduğu.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-308">Output location is **adftutorial/customactivityoutput/** and output file name is yyyy-MM-dd-HH.txt where yyyy-MM-dd-HH is hello year, month, date, and hour of hello slice being produced.</span></span> <span data-ttu-id="4cdd1-309">Bkz: [Geliştirici Başvurusu] [ adf-developer-reference] Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-309">See [Developer Reference][adf-developer-reference] for details.</span></span>

    <span data-ttu-id="4cdd1-310">Bir çıkış blob/dosyası, her girdi dilimi için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-310">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="4cdd1-311">İşte bir çıktı dosyası için her dilimi nasıl adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-311">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="4cdd1-312">Bir çıkış klasöründe oluşturulan tüm hello çıktı dosyaları: **adftutorial\customactivityoutput**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-312">All hello output files are generated in one output folder: **adftutorial\customactivityoutput**.</span></span>

   | <span data-ttu-id="4cdd1-313">Dilim</span><span class="sxs-lookup"><span data-stu-id="4cdd1-313">Slice</span></span> | <span data-ttu-id="4cdd1-314">Başlangıç zamanı</span><span class="sxs-lookup"><span data-stu-id="4cdd1-314">Start time</span></span> | <span data-ttu-id="4cdd1-315">Çıkış dosyası</span><span class="sxs-lookup"><span data-stu-id="4cdd1-315">Output file</span></span> |
   |:--- |:--- |:--- |
   | <span data-ttu-id="4cdd1-316">1</span><span class="sxs-lookup"><span data-stu-id="4cdd1-316">1</span></span> |<span data-ttu-id="4cdd1-317">2016-11-16T00:00:00</span><span class="sxs-lookup"><span data-stu-id="4cdd1-317">2016-11-16T00:00:00</span></span> |<span data-ttu-id="4cdd1-318">2016-11-16-00.txt</span><span class="sxs-lookup"><span data-stu-id="4cdd1-318">2016-11-16-00.txt</span></span> |
   | <span data-ttu-id="4cdd1-319">2</span><span class="sxs-lookup"><span data-stu-id="4cdd1-319">2</span></span> |<span data-ttu-id="4cdd1-320">2016-11-16T01:00:00</span><span class="sxs-lookup"><span data-stu-id="4cdd1-320">2016-11-16T01:00:00</span></span> |<span data-ttu-id="4cdd1-321">2016-11-16-01.txt</span><span class="sxs-lookup"><span data-stu-id="4cdd1-321">2016-11-16-01.txt</span></span> |
   | <span data-ttu-id="4cdd1-322">3</span><span class="sxs-lookup"><span data-stu-id="4cdd1-322">3</span></span> |<span data-ttu-id="4cdd1-323">2016-11-16T02:00:00</span><span class="sxs-lookup"><span data-stu-id="4cdd1-323">2016-11-16T02:00:00</span></span> |<span data-ttu-id="4cdd1-324">2016-11-16-02.txt</span><span class="sxs-lookup"><span data-stu-id="4cdd1-324">2016-11-16-02.txt</span></span> |
   | <span data-ttu-id="4cdd1-325">4</span><span class="sxs-lookup"><span data-stu-id="4cdd1-325">4</span></span> |<span data-ttu-id="4cdd1-326">2016-11-16T03:00:00</span><span class="sxs-lookup"><span data-stu-id="4cdd1-326">2016-11-16T03:00:00</span></span> |<span data-ttu-id="4cdd1-327">2016-11-16-03.txt</span><span class="sxs-lookup"><span data-stu-id="4cdd1-327">2016-11-16-03.txt</span></span> |
   | <span data-ttu-id="4cdd1-328">5</span><span class="sxs-lookup"><span data-stu-id="4cdd1-328">5</span></span> |<span data-ttu-id="4cdd1-329">2016-11-16T04:00:00</span><span class="sxs-lookup"><span data-stu-id="4cdd1-329">2016-11-16T04:00:00</span></span> |<span data-ttu-id="4cdd1-330">2016-11-16-04.txt</span><span class="sxs-lookup"><span data-stu-id="4cdd1-330">2016-11-16-04.txt</span></span> |

    <span data-ttu-id="4cdd1-331">Giriş bir klasördeki tüm hello dosyaları hello başlangıç zamanlarını yukarıda belirtilen dilimle parçası olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-331">Remember that all hello files in an input folder are part of a slice with hello start times mentioned above.</span></span> <span data-ttu-id="4cdd1-332">Bu dilim işlendiğinde hello özel etkinlik her dosyası aracılığıyla tarar ve arama terimi ("Microsoft") oluşumları hello sayısıyla hello çıkış dosyasındaki bir satır üretir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-332">When this slice is processed, hello custom activity scans through each file and produces a line in hello output file with hello number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="4cdd1-333">Merhaba inputfolder üç dosya varsa vardır üç satır hello çıktı dosyasında her saat dilimi: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, vs.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-333">If there are three files in hello inputfolder, there are three lines in hello output file for each hourly slice: 2016-11-16-00.txt, 2016-11-16:01:00:00.txt, etc.</span></span>
3. <span data-ttu-id="4cdd1-334">toodeploy hello **OutputDataset**, tıklatın **dağıtma** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-334">toodeploy hello **OutputDataset**, click **Deploy** on hello command bar.</span></span>

### <a name="create-and-run-a-pipeline-that-uses-hello-custom-activity"></a><span data-ttu-id="4cdd1-335">Oluşturma ve hello özel etkinlik kullanan bir ardışık düzen çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-335">Create and run a pipeline that uses hello custom activity</span></span>
1. <span data-ttu-id="4cdd1-336">Hello Data Factory Düzenleyici'de, tıklatın **... Daha fazla**ve ardından **yeni işlem hattı** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-336">In hello Data Factory Editor, click **... More**, and then select **New pipeline** on hello command bar.</span></span> 
2. <span data-ttu-id="4cdd1-337">Merhaba JSON hello sağ bölmedeki JSON betiği aşağıdaki hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-337">Replace hello JSON in hello right pane with hello following JSON script:</span></span>

    ```JSON
    {
      "name": "ADFTutorialPipelineCustom",
      "properties": {
        "description": "Use custom activity",
        "activities": [
          {
            "Name": "MyDotNetActivity",
            "Type": "DotNetActivity",
            "Inputs": [
              {
                "Name": "InputDataset"
              }
            ],
            "Outputs": [
              {
                "Name": "OutputDataset"
              }
            ],
            "LinkedServiceName": "AzureBatchLinkedService",
            "typeProperties": {
              "AssemblyName": "MyDotNetActivity.dll",
              "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
              "PackageLinkedService": "AzureStorageLinkedService",
              "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
              "extendedProperties": {
                "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
              }
            },
            "Policy": {
              "Concurrency": 2,
              "ExecutionPriorityOrder": "OldestFirst",
              "Retry": 3,
              "Timeout": "00:30:00",
              "Delay": "00:00:00"
            }
          }
        ],
        "start": "2016-11-16T00:00:00Z",
        "end": "2016-11-16T05:00:00Z",
        "isPaused": false
      }
    }
    ```

    <span data-ttu-id="4cdd1-338">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-338">Note hello following points:</span></span>

   * <span data-ttu-id="4cdd1-339">**Eşzamanlılık** çok ayarlanır**2** böylece iki dilimler hello Azure Batch havuzunda 2 VM tarafından paralel olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-339">**Concurrency** is set too**2** so that two slices are processed in parallel by 2 VMs in hello Azure Batch pool.</span></span>
   * <span data-ttu-id="4cdd1-340">Merhaba etkinlikler bölümünde bir etkinlik olduğunu ve türü: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-340">There is one activity in hello activities section and it is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="4cdd1-341">**AssemblyName** hello DLL toohello adına ayarlanır: **MyDotnetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-341">**AssemblyName** is set toohello name of hello DLL: **MyDotnetActivity.dll**.</span></span>
   * <span data-ttu-id="4cdd1-342">**EntryPoint** çok ayarlanır**MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-342">**EntryPoint** is set too**MyDotNetActivityNS.MyDotNetActivity**.</span></span>
   * <span data-ttu-id="4cdd1-343">**PackageLinkedService** çok ayarlanır**AzureStorageLinkedService** hello özel etkinlik zip dosyasını içeren toohello blob depolama işaret eder.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-343">**PackageLinkedService** is set too**AzureStorageLinkedService** that points toohello blob storage that contains hello custom activity zip file.</span></span> <span data-ttu-id="4cdd1-344">Kullanıyorsanız farklı Azure depolama hesapları için giriş/çıkış dosyalarını ve hello özel etkinlik zip dosyası, başka bir Azure depolama bağlantılı hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-344">If you are using different Azure Storage accounts for input/output files and hello custom activity zip file, you create another Azure Storage linked service.</span></span> <span data-ttu-id="4cdd1-345">Bu makalede, kullanmakta olduğunuz varsayılmaktadır hello aynı Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-345">This article assumes that you are using hello same Azure Storage account.</span></span>
   * <span data-ttu-id="4cdd1-346">**PackageFile** çok ayarlanır**customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-346">**PackageFile** is set too**customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="4cdd1-347">Merhaba biçimdedir: containerforthezip/nameofthezip.zip.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-347">It is in hello format: containerforthezip/nameofthezip.zip.</span></span>
   * <span data-ttu-id="4cdd1-348">Merhaba özel etkinlik alır **InputDataset** giriş olarak ve **OutputDataset** çıktı olarak.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-348">hello custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="4cdd1-349">Merhaba linkedServiceName hello özel etkinlik özelliğinin işaret toohello **AzureBatchLinkedService**, o hello özel etkinliği Azure Data Factory söyleyen Azure toplu işlemi vm'lerinde toorun gerekir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-349">hello linkedServiceName property of hello custom activity points toohello **AzureBatchLinkedService**, which tells Azure Data Factory that hello custom activity needs toorun on Azure Batch VMs.</span></span>
   * <span data-ttu-id="4cdd1-350">**isPaused** özelliği çok ayarlanmış**false** varsayılan olarak.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-350">**isPaused** property is set too**false** by default.</span></span> <span data-ttu-id="4cdd1-351">Hello dilimler hello geçmiş başlatmak için hello ardışık düzen hemen bu örnekte çalışır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-351">hello pipeline runs immediately in this example because hello slices start in hello past.</span></span> <span data-ttu-id="4cdd1-352">Bu özellik tootrue toopause hello ardışık düzen ve geri toofalse toorestart ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-352">You can set this property tootrue toopause hello pipeline and set it back toofalse toorestart.</span></span>
   * <span data-ttu-id="4cdd1-353">Merhaba **Başlat** zaman ve **son** sürelerinin **beş** hello ardışık düzen tarafından beş dilimlerinin şekilde birbirinden saatleri ve dilimler saatlik, üretilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-353">hello **start** time and **end** times are **five** hours apart and slices are produced hourly, so five slices are produced by hello pipeline.</span></span>
3. <span data-ttu-id="4cdd1-354">toodeploy hello ardışık tıklatın **dağıtma** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-354">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-hello-pipeline"></a><span data-ttu-id="4cdd1-355">Merhaba işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="4cdd1-355">Monitor hello pipeline</span></span>
1. <span data-ttu-id="4cdd1-356">Hello Azure portal'ın Hello Data Factory dikey penceresinde tıklayın **diyagramı**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-356">In hello Data Factory blade in hello Azure portal, click **Diagram**.</span></span>

    ![Diyagram kutucuğu](./media/data-factory-use-custom-activities/DataFactoryBlade.png)
2. <span data-ttu-id="4cdd1-358">Hello diyagram Görünümü'da, artık hello OutputDataset'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-358">In hello Diagram View, now click hello OutputDataset.</span></span>

    ![Diyagram görünümü](./media/data-factory-use-custom-activities/diagram.png)
3. <span data-ttu-id="4cdd1-360">Merhaba beş çıkış dilimler hello hazır durumda olduğunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-360">You should see that hello five output slices are in hello Ready state.</span></span> <span data-ttu-id="4cdd1-361">Bunlar hello hazır durumda değilse, bunlar henüz üretilmiş henüz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-361">If they are not in hello Ready state, they haven't been produced yet.</span></span> 

   ![Çıktı dilimleri](./media/data-factory-use-custom-activities/OutputSlices.png)
4. <span data-ttu-id="4cdd1-363">Merhaba çıktı dosyaları hello hello blob depolamada oluşturulan doğrulayın **adftutorial** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-363">Verify that hello output files are generated in hello blob storage in hello **adftutorial** container.</span></span>

   ![Özel etkinliğinden çıktı][image-data-factory-ouput-from-custom-activity]
5. <span data-ttu-id="4cdd1-365">Merhaba çıktı dosyası açarsanız, çıktı aşağıdaki benzer toohello hello çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-365">If you open hello output file, you should see hello output similar toohello following output:</span></span>

    ```
    2 occurrences(s) of hello search term "Microsoft" were found in hello file inputfolder/2016-11-16-00/file.txt.
    ```
6. <span data-ttu-id="4cdd1-366">Kullanım hello [Azure portal] [ azure-preview-portal] ya da Azure PowerShell cmdlet'leri toomonitor veri fabrikası, ardışık düzen ve veri kümeleri.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-366">Use hello [Azure portal][azure-preview-portal] or Azure PowerShell cmdlets toomonitor your data factory, pipelines, and data sets.</span></span> <span data-ttu-id="4cdd1-367">Merhaba gelen iletileri görebilirsiniz **ActivityLogger** ' hello kodunda hello özel etkinlik hello portal veya cmdlet'ler kullanarak indirebilir hello günlüklerinde (özellikle kullanıcı-0.log).</span><span class="sxs-lookup"><span data-stu-id="4cdd1-367">You can see messages from hello **ActivityLogger** in hello code for hello custom activity in hello logs (specifically user-0.log) that you can download from hello portal or using cmdlets.</span></span>

   ![Özel etkinliğinden günlüklerini indirin][image-data-factory-download-logs-from-custom-activity]

<span data-ttu-id="4cdd1-369">Bkz: [izleme ve yönetme ardışık düzen](data-factory-monitor-manage-pipelines.md) veri kümelerini ve işlem hatlarını izleme için ayrıntılı adımlar için.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-369">See [Monitor and Manage Pipelines](data-factory-monitor-manage-pipelines.md) for detailed steps for monitoring datasets and pipelines.</span></span>      

## <a name="data-factory-project-in-visual-studio"></a><span data-ttu-id="4cdd1-370">Visual Studio Data Factory projesi</span><span class="sxs-lookup"><span data-stu-id="4cdd1-370">Data Factory project in Visual Studio</span></span>  
<span data-ttu-id="4cdd1-371">Oluşturma ve Azure portalını kullanarak yerine Visual Studio kullanarak Data Factory varlıklarını yayımlama.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-371">You can create and publish Data Factory entities by using Visual Studio instead of using Azure portal.</span></span> <span data-ttu-id="4cdd1-372">Visual Studio kullanarak Data Factory varlıklarını yayımlama, bakın ve ayrıntılı oluşturma hakkında daha fazla bilgi için [Visual Studio kullanarak ilk işlem hattınızı oluşturma](data-factory-build-your-first-pipeline-using-vs.md) ve [SQL Azure Blob tooAzure veri kopyalama](data-factory-copy-activity-tutorial-using-visual-studio.md) makaleler.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-372">For detailed information about creating and publishing Data Factory entities by using Visual Studio, See [Build your first pipeline using Visual Studio](data-factory-build-your-first-pipeline-using-vs.md) and [Copy data from Azure Blob tooAzure SQL](data-factory-copy-activity-tutorial-using-visual-studio.md) articles.</span></span>

<span data-ttu-id="4cdd1-373">Visual Studio'da veri fabrikası proje oluşturuyorsanız, aşağıdaki ek adımları hello:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-373">Do hello following additional steps if you are creating Data Factory project in Visual Studio:</span></span>
 
1. <span data-ttu-id="4cdd1-374">Merhaba Data Factory projesi toohello hello özel etkinlik projeyi içeren Visual Studio çözümü ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-374">Add hello Data Factory project toohello Visual Studio solution that contains hello custom activity project.</span></span> 
2. <span data-ttu-id="4cdd1-375">Bir başvuru toohello .NET etkinliği proje hello Data Factory projeden ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-375">Add a reference toohello .NET activity project from hello Data Factory project.</span></span> <span data-ttu-id="4cdd1-376">Data Factory projesine sağ tıklayın, çok noktası**Ekle**ve ardından **başvuru**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-376">Right-click Data Factory project, point too**Add**, and then click **Reference**.</span></span> 
3. <span data-ttu-id="4cdd1-377">Merhaba, **Başvuru Ekle** iletişim kutusu, select hello **MyDotNetActivity** proje öğesini tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-377">In hello **Add Reference** dialog box, select hello **MyDotNetActivity** project, and click **OK**.</span></span>
4. <span data-ttu-id="4cdd1-378">Derleme ve hello çözüm yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-378">Build and publish hello solution.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4cdd1-379">Data Factory varlıklarını yayımladığınızda, ZIP dosyası sizin için otomatik olarak oluşturulur ve karşıya yüklenen toohello blob kapsayıcı: customactivitycontainer.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-379">When you publish Data Factory entities, a zip file is automatically created for you and is uploaded toohello blob container: customactivitycontainer.</span></span> <span data-ttu-id="4cdd1-380">Merhaba blob kapsayıcısı mevcut değilse otomatik olarak çok oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-380">If hello blob container does not exist, it is automatically created too.</span></span>  


## <a name="data-factory-and-batch-integration"></a><span data-ttu-id="4cdd1-381">Veri Fabrikası ve toplu tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="4cdd1-381">Data Factory and Batch integration</span></span>
<span data-ttu-id="4cdd1-382">Hello Data Factory hizmetinin hello adı ile Azure toplu işleminde bir işi oluşturur: **adf poolname: iş xxx**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-382">hello Data Factory service creates a job in Azure Batch with hello name: **adf-poolname: job-xxx**.</span></span> <span data-ttu-id="4cdd1-383">Tıklatın **işleri** hello sol menüden.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-383">Click **Jobs** from hello left menu.</span></span> 

![Azure Data Factory - toplu işler](media/data-factory-use-custom-activities/data-factory-batch-jobs.png)

<span data-ttu-id="4cdd1-385">Bir görev, her bir dilim etkinlik çalıştırması için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-385">A task is created for each activity run of a slice.</span></span> <span data-ttu-id="4cdd1-386">İşlenen beş dilim hazır toobe varsa, beş görev alanında bu işin oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-386">If there are five slices ready toobe processed, five tasks are created in this job.</span></span> <span data-ttu-id="4cdd1-387">Merhaba Batch havuzu birden çok işlem düğümleri varsa, iki veya daha fazla dilim paralel olarak çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-387">If there are multiple compute nodes in hello Batch pool, two or more slices can run in parallel.</span></span> <span data-ttu-id="4cdd1-388">İşlem başına en fazla görevlerini Hello düğüm kümesi varsa çok > 1, ayrıca hello üzerinde çalışan birden fazla dilim sağlayabilirsiniz aynı işlem.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-388">If hello maximum tasks per compute node is set too> 1, you can also have more than one slice running on hello same compute.</span></span>

![Azure Data Factory - toplu iş görevleri](media/data-factory-use-custom-activities/data-factory-batch-job-tasks.png)

<span data-ttu-id="4cdd1-390">Diyagram aşağıdaki hello hello Azure Data Factory ve toplu işlem görevlerini arasındaki ilişki gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-390">hello following diagram illustrates hello relationship between Azure Data Factory and Batch tasks.</span></span>

![Veri Fabrikası & toplu işlem](./media/data-factory-use-custom-activities/DataFactoryAndBatch.png)

## <a name="troubleshoot-failures"></a><span data-ttu-id="4cdd1-392">Hatalarını giderme</span><span class="sxs-lookup"><span data-stu-id="4cdd1-392">Troubleshoot failures</span></span>
<span data-ttu-id="4cdd1-393">Sorun giderme birkaç temel teknikleri oluşur:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-393">Troubleshooting consists of a few basic techniques:</span></span>

1. <span data-ttu-id="4cdd1-394">Aşağıdaki hata hello görürseniz, bir etkin/Cool blob depolama genel amaçlı Azure blob storage kullanarak yerine kullanıyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-394">If you see hello following error, you may be using a Hot/Cool blob storage instead of using a general-purpose Azure blob storage.</span></span> <span data-ttu-id="4cdd1-395">Merhaba zip dosyası tooa karşıya **genel amaçlı Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-395">Upload hello zip file tooa **general-purpose Azure Storage Account**.</span></span> 
 
    ```
    Error in Activity: Job encountered scheduling error. Code: BlobDownloadMiscError Category: ServerError Message: Miscellaneous error encountered while downloading one of hello specified Azure Blob(s).
    ``` 
2. <span data-ttu-id="4cdd1-396">Aşağıdaki hata hello görürseniz, bu hello adını hello CS dosya eşleşen hello adı hello için belirttiğiniz hello sınıfının onaylayın **EntryPoint** JSON hello düzenindeki özelliği.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-396">If you see hello following error, confirm that hello name of hello class in hello CS file matches hello name you specified for hello **EntryPoint** property in hello pipeline JSON.</span></span> <span data-ttu-id="4cdd1-397">Merhaba kılavuzda hello sınıfı adıdır: MyDotNetActivity ve hello JSON hello EntryPoint: MyDotNetActivityNS. **MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-397">In hello walkthrough, name of hello class is: MyDotNetActivity, and hello EntryPoint in hello JSON is: MyDotNetActivityNS.**MyDotNetActivity**.</span></span>

    ```
    MyDotNetActivity assembly does not exist or doesn't implement hello type Microsoft.DataFactories.Runtime.IDotNetActivity properly
    ```

   <span data-ttu-id="4cdd1-398">Merhaba adları eşleşiyorsa, bu tüm hello ikili dosyaları hello doğrulayın **kök klasörü** hello ZIP dosyasının.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-398">If hello names do match, confirm that all hello binaries are in hello **root folder** of hello zip file.</span></span> <span data-ttu-id="4cdd1-399">Diğer bir deyişle, hello zip dosyası açtığınızda, tüm hello dosyaları hello kök klasöründe, tüm alt klasörlerde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-399">That is, when you open hello zip file, you should see all hello files in hello root folder, not in any sub folders.</span></span>   
3. <span data-ttu-id="4cdd1-400">Merhaba girdi dilimi çok ayarlanmamışsa**hazır**, hello giriş klasör yapısı doğru olduğunu onaylayın ve **dosya.txt'yi** hello giriş klasörlerde bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-400">If hello input slice is not set too**Ready**, confirm that hello input folder structure is correct and **file.txt** exists in hello input folders.</span></span>
3. <span data-ttu-id="4cdd1-401">Merhaba, **yürütme** özel etkinliklerinizi, kullanım hello yöntemi **IActivityLogger** yardımcı olan nesne toolog bilgileri sorunları giderme.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-401">In hello **Execute** method of your custom activity, use hello **IActivityLogger** object toolog information that helps you troubleshoot issues.</span></span> <span data-ttu-id="4cdd1-402">oturum hello iletileri göster hello kullanıcı günlük dosyalarında (adlı bir veya daha fazla: kullanıcı 0.log, kullanıcı 1.log, kullanıcı 2.log vb..).</span><span class="sxs-lookup"><span data-stu-id="4cdd1-402">hello logged messages show up in hello user log files (one or more files named: user-0.log, user-1.log, user-2.log, etc.).</span></span>

   <span data-ttu-id="4cdd1-403">Merhaba, **OutputDataset** dikey penceresinde hello dilim toosee hello tıklatın **veri DİLİMİ** dikey penceresinde, dilim için.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-403">In hello **OutputDataset** blade, click hello slice toosee hello **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="4cdd1-404">Gördüğünüz **etkinlik çalışması** bu dilim için.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-404">You see **activity runs** for that slice.</span></span> <span data-ttu-id="4cdd1-405">Merhaba dilim için bir etkinlik görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-405">You should see one activity run for hello slice.</span></span> <span data-ttu-id="4cdd1-406">Merhaba komut çubuğunda Çalıştır'ı tıklatın, hello için başka bir etkinlik başlatabilirsiniz aynı dilim.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-406">If you click Run in hello command bar, you can start another activity run for hello same slice.</span></span>

   <span data-ttu-id="4cdd1-407">Merhaba etkinlik tıklattığınızda hello bkz **etkinlik çalışma ayrıntıları** günlük dosyalarının listesini içeren dikey.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-407">When you click hello activity run, you see hello **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="4cdd1-408">Merhaba user_0.log dosyasında günlüğe kaydedilen iletilere bakın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-408">You see logged messages in hello user_0.log file.</span></span> <span data-ttu-id="4cdd1-409">Hata oluştuğunda hello yeniden deneme sayısı hello ardışık düzen/JSON etkinliğinde too3 ayarlandığından üç Etkinlik çalışması bakın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-409">When an error occurs, you see three activity runs because hello retry count is set too3 in hello pipeline/activity JSON.</span></span> <span data-ttu-id="4cdd1-410">Merhaba etkinlik tıklattığınızda tootroubleshoot hello hata inceleyebilirsiniz hello günlük dosyalarına bakın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-410">When you click hello activity run, you see hello log files that you can review tootroubleshoot hello error.</span></span>

   <span data-ttu-id="4cdd1-411">Günlük dosyaları Hello listesinde hello tıklayın **kullanıcı 0.log**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-411">In hello list of log files, click hello **user-0.log**.</span></span> <span data-ttu-id="4cdd1-412">Merhaba sağ panelde hello kullanarak hello sonucu olan **IActivityLogger.Write** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-412">In hello right panel are hello results of using hello **IActivityLogger.Write** method.</span></span> <span data-ttu-id="4cdd1-413">Tüm iletileri görmüyorsanız adlı daha fazla günlük dosyaları olup olmadığını denetleyin: user_1.log, user_2.log vs. Son oturum açan ileti Hello sonra Aksi takdirde hello kod başarısız olmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-413">If you don't see all messages, check if you have more log files named: user_1.log, user_2.log etc. Otherwise, hello code may have failed after hello last logged message.</span></span>

   <span data-ttu-id="4cdd1-414">Ayrıca, denetleme **sistem 0.log** sistem hata iletileri ve özel durumlar için.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-414">In addition, check **system-0.log** for any system error messages and exceptions.</span></span>
4. <span data-ttu-id="4cdd1-415">Merhaba dahil **PDB** hello hata ayrıntıları bilgileri gibi böylece hello zip dosyasında dosya **çağrı yığını** bir hata oluştuğunda.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-415">Include hello **PDB** file in hello zip file so that hello error details have information such as **call stack** when an error occurs.</span></span>
5. <span data-ttu-id="4cdd1-416">Merhaba özel etkinlik hello olmalıdır tüm dosyaları hello zip dosyasında hello **üst düzey** hiçbir alt klasörler ile.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-416">All hello files in hello zip file for hello custom activity must be at hello **top level** with no sub folders.</span></span>
6. <span data-ttu-id="4cdd1-417">Bu hello olun **assemblyName** (MyDotNetActivity.dll) **entryPoint**(MyDotNetActivityNS.MyDotNetActivity) **packageFile** (customactivitycontainer / MyDotNetActivity.zip) ve **packageLinkedService** (toohello işaret etmelidir **genel amaçlı**hello zip dosyasını içeren Azure blob depolama) toocorrect değerlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-417">Ensure that hello **assemblyName** (MyDotNetActivity.dll), **entryPoint**(MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point toohello **general-purpose**Azure blob storage that contains hello zip file) are set toocorrect values.</span></span>
7. <span data-ttu-id="4cdd1-418">Bir hata ve istediğiniz tooreprocess hello dilim sabit, hello hello dilimi sağ **OutputDataset** tıklayın ve dikey **çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-418">If you fixed an error and want tooreprocess hello slice, right-click hello slice in hello **OutputDataset** blade and click **Run**.</span></span>
8. <span data-ttu-id="4cdd1-419">Aşağıdaki hata hello görürseniz, hello Azure Storage paketi sürümü > 4.3.0 kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-419">If you see hello following error, you are using hello Azure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="4cdd1-420">Veri Fabrikası Başlatıcı WindowsAzure.Storage hello 4.3 sürümünü gerektirir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-420">Data Factory service launcher requires hello 4.3 version of WindowsAzure.Storage.</span></span> <span data-ttu-id="4cdd1-421">Bkz: [Appdomain yalıtım](#appdomain-isolation) bölümünde bir iş-geçici bir çözüm için hello kullanmanız gerekiyorsa Azure Storage derlemenin sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-421">See [Appdomain isolation](#appdomain-isolation) section for a work-around if you must use hello later version of Azure Storage assembly.</span></span> 

    ```
    Error in Activity: Unknown error in module: System.Reflection.TargetInvocationException: Exception has been thrown by hello target of an invocation. ---> System.TypeLoadException: Could not load type 'Microsoft.WindowsAzure.Storage.Blob.CloudBlob' from assembly 'Microsoft.WindowsAzure.Storage, Version=4.3.0.0, Culture=neutral, 
    ```

    <span data-ttu-id="4cdd1-422">Azure Storage paket hello 4.3.0 sürümünü kullanabilirsiniz, hello varolan başvuru tooAzure depolama paketi sürümü > 4.3.0 kaldırın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-422">If you can use hello 4.3.0 version of Azure Storage package, remove hello existing reference tooAzure Storage package of version > 4.3.0.</span></span> <span data-ttu-id="4cdd1-423">Ardından, NuGet Paket Yöneticisi Konsolu'ndan komutu aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-423">Then, run hello following command from NuGet Package Manager Console.</span></span> 

    ```PowerShell
    Install-Package WindowsAzure.Storage -Version 4.3.0
    ```

    <span data-ttu-id="4cdd1-424">Merhaba projeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-424">Build hello project.</span></span> <span data-ttu-id="4cdd1-425">Sürüm > 4.3.0 Azure.Storage bütünleştirilmiş hello klasörüne silin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-425">Delete Azure.Storage assembly of version > 4.3.0 from hello bin\Debug folder.</span></span> <span data-ttu-id="4cdd1-426">Bir zip dosyası ikili dosyaları ve hello PDB dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-426">Create a zip file with binaries and hello PDB file.</span></span> <span data-ttu-id="4cdd1-427">Bu bir hello blob kapsayıcısında (customactivitycontainer) Hello eski zip dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-427">Replace hello old zip file with this one in hello blob container (customactivitycontainer).</span></span> <span data-ttu-id="4cdd1-428">Yeniden çalıştırılan hello başarısız olan dilimler (dilim sağ tıklatın ve Çalıştır'ı tıklatın).</span><span class="sxs-lookup"><span data-stu-id="4cdd1-428">Rerun hello slices that failed (right-click slice, and click Run).</span></span>   
8. <span data-ttu-id="4cdd1-429">Merhaba özel etkinlik hello kullanmaz **app.config** paketinizi dosyasından.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-429">hello custom activity does not use hello **app.config** file from your package.</span></span> <span data-ttu-id="4cdd1-430">Bu nedenle, kodunuzu hello yapılandırma dosyasından bağlantı dizelerini yazıyorsa, çalışma zamanında çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-430">Therefore, if your code reads any connection strings from hello configuration file, it does not work at runtime.</span></span> <span data-ttu-id="4cdd1-431">Azure Batch kullanarak toohold olduğunda en iyi yöntem herhangi parolalarında hello bir **Azure KeyVault**, sertifika tabanlı hizmet asıl tooprotect hello kullan **keyvault**ve hello sertifika dağıtın tooAzure Batch havuzu.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-431">hello best practice when using Azure Batch is toohold any secrets in an **Azure KeyVault**, use a certificate-based service principal tooprotect hello **keyvault**, and distribute hello certificate tooAzure Batch pool.</span></span> <span data-ttu-id="4cdd1-432">.NET özel etkinlik hello sonra gizli hello KeyVault çalışma zamanında erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-432">hello .NET custom activity then can access secrets from hello KeyVault at runtime.</span></span> <span data-ttu-id="4cdd1-433">Bu çözüm genel bir çözümdür ve gizli anahtarı, yalnızca bağlantı dizesi tooany türü ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-433">This solution is a generic solution and can scale tooany type of secret, not just connection string.</span></span>

   <span data-ttu-id="4cdd1-434">Daha kolay bir çözüm (ancak en iyi yöntem değildir): oluşturabileceğiniz bir **Azure SQL bağlı hizmeti** bağlantı dizesi ayarlarıyla kullanır bağlantılı hizmet ve sahte bir giriş veri kümesi olarak zinciri hello dataset hello bir veri kümesi oluşturma toohello özel .NET etkinlik.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-434">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses hello linked service, and chain hello dataset as a dummy input dataset toohello custom .NET activity.</span></span> <span data-ttu-id="4cdd1-435">Hizmetin bağlantı dizesi hello özel etkinlik kodda erişim hello bağlı sonra kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-435">You can then access hello linked service's connection string in hello custom activity code.</span></span>  

## <a name="update-custom-activity"></a><span data-ttu-id="4cdd1-436">Özel Etkinlik güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="4cdd1-436">Update custom activity</span></span>
<span data-ttu-id="4cdd1-437">Merhaba özel etkinlik hello kodunu güncelleştirirseniz, onu oluşturmak ve yeni ikili dosyaları toohello blob depolama içeren hello zip dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-437">If you update hello code for hello custom activity, build it, and upload hello zip file that contains new binaries toohello blob storage.</span></span>

## <a name="appdomain-isolation"></a><span data-ttu-id="4cdd1-438">Uygulama etki alanı yalıtımı</span><span class="sxs-lookup"><span data-stu-id="4cdd1-438">Appdomain isolation</span></span>
<span data-ttu-id="4cdd1-439">Bkz: [arası AppDomain örnek](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) , nasıl toocreate değil özel bir aktivite hello Data Factory başlatıcısı tarafından kullanılan tooassembly sürümleri kısıtlı gösterir (örnek: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x vb..).</span><span class="sxs-lookup"><span data-stu-id="4cdd1-439">See [Cross AppDomain Sample](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) that shows you how toocreate a custom activity that is not constrained tooassembly versions used by hello Data Factory launcher (example: WindowsAzure.Storage v4.3.0, Newtonsoft.Json v6.0.x, etc.).</span></span>

## <a name="access-extended-properties"></a><span data-ttu-id="4cdd1-440">Genişletilmiş özellikler erişim</span><span class="sxs-lookup"><span data-stu-id="4cdd1-440">Access extended properties</span></span>
<span data-ttu-id="4cdd1-441">Hello örnek aşağıdaki gösterildiği gibi JSON hello etkinliğinde genişletilmiş özellikler bildirimini yapabilir:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-441">You can declare extended properties in hello activity JSON as shown in hello following sample:</span></span>

```JSON
"typeProperties": {
  "AssemblyName": "MyDotNetActivity.dll",
  "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
  "PackageLinkedService": "AzureStorageLinkedService",
  "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
  "extendedProperties": {
    "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))",
    "DataFactoryName": "CustomActivityFactory"
  }
},
```


<span data-ttu-id="4cdd1-442">Merhaba örnekte iki genişletilmiş özelliği vardır: **SliceStart** ve **DataFactoryName**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-442">In hello example, there are two extended properties: **SliceStart** and **DataFactoryName**.</span></span> <span data-ttu-id="4cdd1-443">Merhaba değer SliceStart için hello SliceStart sistem değişkeni temel alır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-443">hello value for SliceStart is based on hello SliceStart system variable.</span></span> <span data-ttu-id="4cdd1-444">Bkz: [sistem değişkenleri](data-factory-functions-variables.md) desteklenen sistem değişkenleri listesi.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-444">See [System Variables](data-factory-functions-variables.md) for a list of supported system variables.</span></span> <span data-ttu-id="4cdd1-445">Merhaba DataFactoryName sabit kodlanmış tooCustomActivityFactory değeridir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-445">hello value for DataFactoryName is hard-coded tooCustomActivityFactory.</span></span>

<span data-ttu-id="4cdd1-446">tooaccess, bu genişletilmiş hello özelliklerinde **yürütme** yöntemi, kullanım kodunu benzer toohello koddan:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-446">tooaccess these extended properties in hello **Execute** method, use code similar toohello following code:</span></span>

```csharp
// tooget extended properties (for example: SliceStart)
DotNetActivity dotNetActivity = (DotNetActivity)activity.TypeProperties;
string sliceStartString = dotNetActivity.ExtendedProperties["SliceStart"];

// toolog all extended properties                               
IDictionary<string, string> extendedProperties = dotNetActivity.ExtendedProperties;
logger.Write("Logging extended properties if any...");
foreach (KeyValuePair<string, string> entry in extendedProperties)
{
    logger.Write("<key:{0}> <value:{1}>", entry.Key, entry.Value);
}
```

## <a name="auto-scaling-of-azure-batch"></a><span data-ttu-id="4cdd1-447">Azure batch otomatik olarak ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="4cdd1-447">Auto-scaling of Azure Batch</span></span>
<span data-ttu-id="4cdd1-448">Bir Azure Batch havuzuyla oluşturabilirsiniz **otomatik ölçeklendirme** özelliği.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-448">You can also create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="4cdd1-449">Örneğin, 0 özel VM'ler ve bekleyen görevler, hello sayısına dayalı bir otomatik ölçeklendirme formülü ile bir azure batch havuzu oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-449">For example, you could create an azure batch pool with 0 dedicated VMs and an autoscale formula based on hello number of pending tasks.</span></span> 

<span data-ttu-id="4cdd1-450">Merhaba formül örneği burada başarır davranış aşağıdaki hello: hello havuzu başlangıçta oluşturulduğunda 1 VM ile başlar.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-450">hello sample formula here achieves hello following behavior: When hello pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="4cdd1-451">Çalışan + (kuyruğa alınmış) etkin $PendingTasks ölçüm tanımlar hello sayıda görev durumu.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-451">$PendingTasks metric defines hello number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="4cdd1-452">Merhaba formül hello ortalama sayısı Bekleyen Görevler hello Son 180 saniye bulur ve TargetDedicated uygun şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-452">hello formula finds hello average number of pending tasks in hello last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="4cdd1-453">TargetDedicated hiçbir zaman 25 VM'ler gider sağlar.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-453">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="4cdd1-454">Bu nedenle, yeni görevler gönderildiği haliyle havuzu otomatik olarak büyür ve görevler tamamlanınca VM'ler boş bir birer birer hale ve bu VM'lerin hello otomatik ölçeklendirmeyi küçültür.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-454">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and hello autoscaling shrinks those VMs.</span></span> <span data-ttu-id="4cdd1-455">startingNumberOfVMs ve maxNumberofVMs ayarlanmış tooyour gereksinimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-455">startingNumberOfVMs and maxNumberofVMs can be adjusted tooyour needs.</span></span>

<span data-ttu-id="4cdd1-456">Otomatik ölçeklendirme formülü:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-456">Autoscale formula:</span></span>

``` 
startingNumberOfVMs = 1;
maxNumberofVMs = 25;
pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
$TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
```

<span data-ttu-id="4cdd1-457">Bkz: [ölçek işlem düğümlerini Azure Batch havuzunda otomatik olarak](../batch/batch-automatic-scaling.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-457">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

<span data-ttu-id="4cdd1-458">Merhaba havuzu hello varsayılan kullanıyorsanız [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch hizmeti, 15-30 dakika tooprepare hello VM hello özel etkinlik çalıştırmadan önce sürebilir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-458">If hello pool is using hello default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), hello Batch service could take 15-30 minutes tooprepare hello VM before running hello custom activity.</span></span>  <span data-ttu-id="4cdd1-459">Merhaba havuzu farklı autoScaleEvaluationInterval kullanıyorsanız, hello Batch hizmeti autoScaleEvaluationInterval + 10 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-459">If hello pool is using a different autoScaleEvaluationInterval, hello Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>

## <a name="use-hdinsight-compute-service"></a><span data-ttu-id="4cdd1-460">Hdınsight işlem hizmeti kullanın</span><span class="sxs-lookup"><span data-stu-id="4cdd1-460">Use HDInsight compute service</span></span>
<span data-ttu-id="4cdd1-461">Merhaba kılavuzda Azure toplu işlem toorun hello özel etkinlik kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-461">In hello walkthrough, you used Azure Batch compute toorun hello custom activity.</span></span> <span data-ttu-id="4cdd1-462">Ayrıca, kendi Windows tabanlı Hdınsight kümesi kullanın veya hello özel etkinlik hello Hdınsight kümesi üzerinde çalışan bir isteğe bağlı Windows tabanlı Hdınsight kümesi oluşturursanız ve veri fabrikası sahip.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-462">You can also use your own Windows-based HDInsight cluster or have Data Factory create an on-demand Windows-based HDInsight cluster and have hello custom activity run on hello HDInsight cluster.</span></span> <span data-ttu-id="4cdd1-463">Hdınsight kümesi kullanma için hello üst düzey adımları şunlardır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-463">Here are hello high-level steps for using an HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4cdd1-464">Merhaba özel .NET etkinlikler yalnızca Windows tabanlı Hdınsight kümelerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-464">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="4cdd1-465">Bu sınırlama aşağıdaki haller için geçici çözüm toouse hello harita azaltmak etkinlik toorun özel Java kod Linux tabanlı Hdınsight kümesi üzerinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-465">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4cdd1-466">Toouse VM'ler toorun özel etkinlikler bir Hdınsight kümesi yerine bir Azure Batch havuzu başka bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-466">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>
 

1. <span data-ttu-id="4cdd1-467">Bir Azure Hdınsight bağlı hizmeti oluşturma.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-467">Create an Azure HDInsight linked service.</span></span>   
2. <span data-ttu-id="4cdd1-468">Kullanım Hdınsight bağlantılı hizmeti yerine **AzureBatchLinkedService** hello JSON kanalı.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-468">Use HDInsight linked service in place of **AzureBatchLinkedService** in hello pipeline JSON.</span></span>

<span data-ttu-id="4cdd1-469">Tootest istiyorsanız bunu hello kılavuza, değişiklik **Başlat** ve **son** böylece hello Azure Hdınsight hizmeti ile Merhaba senaryosu test hello ardışık düzeni için zaman.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-469">If you want tootest it with hello walkthrough, change **start** and **end** times for hello pipeline so that you can test hello scenario with hello Azure HDInsight service.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="4cdd1-470">Azure HDInsight bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-470">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="4cdd1-471">Hello Azure Data Factory hizmetine bir istek üzerine küme oluşturmayı destekler ve tooprocess giriş tooproduce çıktı verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-471">hello Azure Data Factory service supports creation of an on-demand cluster and use it tooprocess input tooproduce output data.</span></span> <span data-ttu-id="4cdd1-472">Ayrıca kendi kümenizi kullanabilirsiniz tooperform hello aynı.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-472">You can also use your own cluster tooperform hello same.</span></span> <span data-ttu-id="4cdd1-473">İsteğe bağlı Hdınsight kümesi kullandığınızda, bir küme için her bir dilim oluşturulan.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-473">When you use on-demand HDInsight cluster, a cluster gets created for each slice.</span></span> <span data-ttu-id="4cdd1-474">Kendi Hdınsight kümenizi kullanırsanız, hello küme hazır iken tooprocess dilim hemen hello.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-474">Whereas, if you use your own HDInsight cluster, hello cluster is ready tooprocess hello slice immediately.</span></span> <span data-ttu-id="4cdd1-475">İsteğe bağlı küme kullandığınızda, bu nedenle, hello çıktı verilerini kendi kümenizi kullandığınızda, olabildiğince çabuk göremeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-475">Therefore, when you use on-demand cluster, you may not see hello output data as quickly as when you use your own cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="4cdd1-476">Çalışma zamanında .NET etkinliği bir örneği yalnızca bir çalışan düğümünde hello Hdınsight kümesi çalıştırılır; birden çok düğümde ölçeklendirilmiş toorun olamaz.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-476">At runtime, an instance of a .NET activity runs only on one worker node in hello HDInsight cluster; it cannot be scaled toorun on multiple nodes.</span></span> <span data-ttu-id="4cdd1-477">.NET etkinliği birden çok örneğini farklı hello Hdınsight küme düğümlerinde paralel olarak çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-477">Multiple instances of .NET activity can run in parallel on different nodes of hello HDInsight cluster.</span></span>
>
>

##### <a name="toouse-an-on-demand-hdinsight-cluster"></a><span data-ttu-id="4cdd1-478">toouse isteğe bağlı Hdınsight kümesi</span><span class="sxs-lookup"><span data-stu-id="4cdd1-478">toouse an on-demand HDInsight cluster</span></span>
1. <span data-ttu-id="4cdd1-479">Merhaba, **Azure portal**, tıklatın **geliştir ve Dağıt** hello Data Factory giriş sayfasında.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-479">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="4cdd1-480">Hello Data Factory Düzenleyici'de, tıklatın **yeni işlem** hello komut çubuğu ve select **isteğe bağlı Hdınsight kümesi** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-480">In hello Data Factory Editor, click **New compute** from hello command bar and select **On-demand HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="4cdd1-481">Değişiklikleri toohello JSON betiği aşağıdaki hello olun:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-481">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="4cdd1-482">Hello için **clusterSize** özelliği, hello hello Hdınsight küme boyutunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-482">For hello **clusterSize** property, specify hello size of hello HDInsight cluster.</span></span>
   2. <span data-ttu-id="4cdd1-483">Hello için **timeToLive** özelliği, silinmeden önce ne kadar süreyle hello müşteri süreyle boşta kalabileceğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-483">For hello **timeToLive** property, specify how long hello customer can be idle before it is deleted.</span></span>
   3. <span data-ttu-id="4cdd1-484">Hello için **sürüm** özelliği, toouse istediğiniz hello Hdınsight sürüm belirtin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-484">For hello **version** property, specify hello HDInsight version you want toouse.</span></span> <span data-ttu-id="4cdd1-485">Bu özellik bıraksanız hello en son sürümü kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-485">If you exclude this property, hello latest version is used.</span></span>  
   4. <span data-ttu-id="4cdd1-486">Hello için **linkedServiceName**, belirtin **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-486">For hello **linkedServiceName**, specify **AzureStorageLinkedService**.</span></span>

        ```JSON
        {
           "name": "HDInsightOnDemandLinkedService",
           "properties": {
               "type": "HDInsightOnDemand",
               "typeProperties": {
                   "clusterSize": 4,
                   "timeToLive": "00:05:00",
                   "osType": "Windows",
                   "linkedServiceName": "AzureStorageLinkedService",
               }
           }
        }
        ```

    > [!IMPORTANT]
    > <span data-ttu-id="4cdd1-487">Merhaba özel .NET etkinlikler yalnızca Windows tabanlı Hdınsight kümelerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-487">hello custom .NET activities run only on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="4cdd1-488">Bu sınırlama aşağıdaki haller için geçici çözüm toouse hello harita azaltmak etkinlik toorun özel Java kod Linux tabanlı Hdınsight kümesi üzerinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-488">A workaround for this limitation is toouse hello Map Reduce Activity toorun custom Java code on a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4cdd1-489">Toouse VM'ler toorun özel etkinlikler bir Hdınsight kümesi yerine bir Azure Batch havuzu başka bir seçenektir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-489">Another option is toouse an Azure Batch pool of VMs toorun custom activities instead of using a HDInsight cluster.</span></span>

4. <span data-ttu-id="4cdd1-490">Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-490">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

##### <a name="toouse-your-own-hdinsight-cluster"></a><span data-ttu-id="4cdd1-491">toouse kendi Hdınsight kümenizi:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-491">toouse your own HDInsight cluster:</span></span>
1. <span data-ttu-id="4cdd1-492">Merhaba, **Azure portal**, tıklatın **geliştir ve Dağıt** hello Data Factory giriş sayfasında.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-492">In hello **Azure portal**, click **Author and Deploy** in hello Data Factory home page.</span></span>
2. <span data-ttu-id="4cdd1-493">Merhaba, **Data Factory düzenleyici**, tıklatın **yeni işlem** hello komut çubuğu seçin ve **Hdınsight kümesi** hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-493">In hello **Data Factory Editor**, click **New compute** from hello command bar and select **HDInsight cluster** from hello menu.</span></span>
3. <span data-ttu-id="4cdd1-494">Değişiklikleri toohello JSON betiği aşağıdaki hello olun:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-494">Make hello following changes toohello JSON script:</span></span>

   1. <span data-ttu-id="4cdd1-495">Hello için **clusterUri** özelliği, Hdınsight için hello URL'sini girin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-495">For hello **clusterUri** property, enter hello URL for your HDInsight.</span></span> <span data-ttu-id="4cdd1-496">Örneğin: https://<clustername>.azurehdinsight.net/</span><span class="sxs-lookup"><span data-stu-id="4cdd1-496">For example: https://<clustername>.azurehdinsight.net/</span></span>     
   2. <span data-ttu-id="4cdd1-497">Hello için **kullanıcıadı** özelliği, erişim toohello Hdınsight kümesine sahip hello kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-497">For hello **UserName** property, enter hello user name who has access toohello HDInsight cluster.</span></span>
   3. <span data-ttu-id="4cdd1-498">Hello için **parola** özelliği, hello kullanıcı için hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-498">For hello **Password** property, enter hello password for hello user.</span></span>
   4. <span data-ttu-id="4cdd1-499">Hello için **LinkedServiceName** özelliği girin **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-499">For hello **LinkedServiceName** property, enter **AzureStorageLinkedService**.</span></span>
4. <span data-ttu-id="4cdd1-500">Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-500">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

<span data-ttu-id="4cdd1-501">Bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md) Ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-501">See [Compute linked services](data-factory-compute-linked-services.md) for details.</span></span>

<span data-ttu-id="4cdd1-502">Merhaba, **JSON kanal**, Hdınsight kullanma (isteğe bağlı veya kendi) bağlantılı hizmeti:</span><span class="sxs-lookup"><span data-stu-id="4cdd1-502">In hello **pipeline JSON**, use HDInsight (on-demand or your own) linked service:</span></span>

```JSON
{
  "name": "ADFTutorialPipelineCustom",
  "properties": {
    "description": "Use custom activity",
    "activities": [
      {
        "Name": "MyDotNetActivity",
        "Type": "DotNetActivity",
        "Inputs": [
          {
            "Name": "InputDataset"
          }
        ],
        "Outputs": [
          {
            "Name": "OutputDataset"
          }
        ],
        "LinkedServiceName": "HDInsightOnDemandLinkedService",
        "typeProperties": {
          "AssemblyName": "MyDotNetActivity.dll",
          "EntryPoint": "MyDotNetActivityNS.MyDotNetActivity",
          "PackageLinkedService": "AzureStorageLinkedService",
          "PackageFile": "customactivitycontainer/MyDotNetActivity.zip",
          "extendedProperties": {
            "SliceStart": "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"
          }
        },
        "Policy": {
          "Concurrency": 2,
          "ExecutionPriorityOrder": "OldestFirst",
          "Retry": 3,
          "Timeout": "00:30:00",
          "Delay": "00:00:00"
        }
      }
    ],
    "start": "2016-11-16T00:00:00Z",
    "end": "2016-11-16T05:00:00Z",
    "isPaused": false
  }
}
```

## <a name="create-a-custom-activity-by-using-net-sdk"></a><span data-ttu-id="4cdd1-503">.NET SDK kullanarak bir özel etkinlik oluşturma</span><span class="sxs-lookup"><span data-stu-id="4cdd1-503">Create a custom activity by using .NET SDK</span></span>
<span data-ttu-id="4cdd1-504">Bu makalede Hello kılavuzda hello Azure portal kullanarak hello özel etkinlik kullanan bir ardışık düzen ile bir veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-504">In hello walkthrough in this article, you create a data factory with a pipeline that uses hello custom activity by using hello Azure portal.</span></span> <span data-ttu-id="4cdd1-505">koddan hello nasıl toocreate hello veri fabrikası .NET SDK kullanarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-505">hello following code shows you how toocreate hello data factory by using .NET SDK instead.</span></span> <span data-ttu-id="4cdd1-506">SDK tooprogrammatically kullanma hakkında daha fazla ayrıntı hello işlem hatlarını oluşturmak bulabilirsiniz [.NET API kullanarak kopyalama etkinliği ile işlem hattı oluşturma](data-factory-copy-activity-tutorial-using-dotnet-api.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-506">You can find more details about using SDK tooprogrammatically create pipelines in hello [create a pipeline with copy activity by using .NET API](data-factory-copy-activity-tutorial-using-dotnet-api.md) article.</span></span> 

```csharp
using System;
using System.Configuration;
using System.Collections.ObjectModel;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.Azure;
using Microsoft.Azure.Management.DataFactories;
using Microsoft.Azure.Management.DataFactories.Models;
using Microsoft.Azure.Management.DataFactories.Common.Models;

using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Collections.Generic;

namespace DataFactoryAPITestApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // create data factory management client

            // TODO: replace ADFTutorialResourceGroup with hello name of your resource group.
            string resourceGroupName = "ADFTutorialResourceGroup";

            // TODO: replace APITutorialFactory with a name that is globally unique. For example: APITutorialFactory04212017
            string dataFactoryName = "APITutorialFactory";

            TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
                ConfigurationManager.AppSettings["SubscriptionId"],
                GetAuthorizationHeader().Result);

            Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

            DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);

            Console.WriteLine("Creating a data factory");
            client.DataFactories.CreateOrUpdate(resourceGroupName,
                new DataFactoryCreateOrUpdateParameters()
                {
                    DataFactory = new DataFactory()
                    {
                        Name = dataFactoryName,
                        Location = "westus",
                        Properties = new DataFactoryProperties()
                    }
                }
            );

            // create a linked service for input data store: Azure Storage
            Console.WriteLine("Creating Azure Storage linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureStorageLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: Replace <accountname> and <accountkey> with name and key of your Azure Storage account.
                            new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>")
                        )
                    }
                }
            );

            // create a linked service for output data store: Azure SQL Database
            Console.WriteLine("Creating Azure Batch linked service");
            client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new LinkedServiceCreateOrUpdateParameters()
                {
                    LinkedService = new LinkedService()
                    {
                        Name = "AzureBatchLinkedService",
                        Properties = new LinkedServiceProperties
                        (
                            // TODO: replace <batchaccountname> and <yourbatchaccountkey> with name and key of your Azure Batch account
                            new AzureBatchLinkedService("<batchaccountname>", "https://westus.batch.azure.com", "<yourbatchaccountkey>", "myazurebatchpool", "AzureStorageLinkedService")
                        )
                    }
                }
            );

            // create input and output datasets
            Console.WriteLine("Creating input and output datasets");
            string Dataset_Source = "InputDataset";
            string Dataset_Destination = "OutputDataset";

            Console.WriteLine("Creating input dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Source,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FolderPath = "adftutorial/customactivityinput/",
                                Format = new TextFormat()
                            },
                            External = true,
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },

                            Policy = new Policy() { }
                        }
                    }
                });

            Console.WriteLine("Creating output dataset of type: Azure Blob");
            client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new DatasetCreateOrUpdateParameters()
                {
                    Dataset = new Dataset()
                    {
                        Name = Dataset_Destination,
                        Properties = new DatasetProperties()
                        {
                            LinkedServiceName = "AzureStorageLinkedService",
                            TypeProperties = new AzureBlobDataset()
                            {
                                FileName = "{slice}.txt",
                                FolderPath = "adftutorial/customactivityoutput/",
                                PartitionedBy = new List<Partition>()
                                {
                                    new Partition()
                                    {
                                        Name = "slice",
                                        Value = new DateTimePartitionValue()
                                        {
                                            Date = "SliceStart",
                                            Format = "yyyy-MM-dd-HH"
                                        }
                                    }
                                }
                            },
                            Availability = new Availability()
                            {
                                Frequency = SchedulePeriod.Hour,
                                Interval = 1,
                            },
                        }
                    }
                });

            Console.WriteLine("Creating a custom activity pipeline");
            DateTime PipelineActivePeriodStartTime = new DateTime(2017, 3, 9, 0, 0, 0, 0, DateTimeKind.Utc);
            DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
            string PipelineName = "ADFTutorialPipelineCustom";

            client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
                new PipelineCreateOrUpdateParameters()
                {
                    Pipeline = new Pipeline()
                    {
                        Name = PipelineName,
                        Properties = new PipelineProperties()
                        {
                            Description = "Use custom activity",

                            // Initial value for pipeline's active period. With this, you won't need tooset slice status
                            Start = PipelineActivePeriodStartTime,
                            End = PipelineActivePeriodEndTime,
                            IsPaused = false,

                            Activities = new List<Activity>()
                            {
                                new Activity()
                                {
                                    Name = "MyDotNetActivity",
                                    Inputs = new List<ActivityInput>()
                                    {
                                        new ActivityInput() {
                                            Name = Dataset_Source
                                        }
                                    },
                                    Outputs = new List<ActivityOutput>()
                                    {
                                        new ActivityOutput()
                                        {
                                            Name = Dataset_Destination
                                        }
                                    },
                                    LinkedServiceName = "AzureBatchLinkedService",
                                    TypeProperties = new DotNetActivity()
                                    {
                                        AssemblyName = "MyDotNetActivity.dll",
                                        EntryPoint = "MyDotNetActivityNS.MyDotNetActivity",
                                        PackageLinkedService = "AzureStorageLinkedService",
                                        PackageFile = "customactivitycontainer/MyDotNetActivity.zip",
                                        ExtendedProperties = new Dictionary<string, string>()
                                        {
                                            { "SliceStart", "$$Text.Format('{0:yyyyMMddHH-mm}', Time.AddMinutes(SliceStart, 0))"}
                                        }
                                    },
                                    Policy = new ActivityPolicy()
                                    {
                                        Concurrency = 2,
                                        ExecutionPriorityOrder = "OldestFirst",
                                        Retry = 3,
                                        Timeout = new TimeSpan(0,0,30,0),
                                        Delay = new TimeSpan()
                                    }
                                }
                            }
                        }
                    }
                });
        }

        public static async Task<string> GetAuthorizationHeader()
        {
            AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
            ClientCredential credential = new ClientCredential(
                ConfigurationManager.AppSettings["ApplicationId"],
                ConfigurationManager.AppSettings["Password"]);
            AuthenticationResult result = await context.AcquireTokenAsync(
                resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
                clientCredential: credential);

            if (result != null)
                return result.AccessToken;

            throw new InvalidOperationException("Failed tooacquire token");
        }
    }
}
```

## <a name="debug-custom-activity-in-visual-studio"></a><span data-ttu-id="4cdd1-507">Özel Etkinlik Visual Studio'da hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="4cdd1-507">Debug custom activity in Visual Studio</span></span>
<span data-ttu-id="4cdd1-508">Merhaba [Azure Data Factory - yerel ortamınıza](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) örneği github'daki toodebug özel .NET etkinlikler Visual Studio içinde sağlayan bir araç içerir.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-508">hello [Azure Data Factory - local environment](https://github.com/gbrueckl/Azure.DataFactory.LocalEnvironment) sample on GitHub includes a tool that allows you toodebug custom .NET activities within Visual Studio.</span></span>  


## <a name="sample-custom-activities-on-github"></a><span data-ttu-id="4cdd1-509">Github'da örnek özel etkinlikler</span><span class="sxs-lookup"><span data-stu-id="4cdd1-509">Sample custom activities on GitHub</span></span>
| <span data-ttu-id="4cdd1-510">Örnek</span><span class="sxs-lookup"><span data-stu-id="4cdd1-510">Sample</span></span> | <span data-ttu-id="4cdd1-511">Hangi özel etkinlik mu</span><span class="sxs-lookup"><span data-stu-id="4cdd1-511">What custom activity does</span></span> |
| --- | --- |
| <span data-ttu-id="4cdd1-512">[HTTP veri yükleyici](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span><span class="sxs-lookup"><span data-stu-id="4cdd1-512">[HTTP Data Downloader](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/HttpDataDownloaderSample).</span></span> |<span data-ttu-id="4cdd1-513">Bir HTTP uç noktası tooAzure veri fabrikasında özel C# etkinlik kullanarak Blob depolama alanından veri yükler.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-513">Downloads data from an HTTP Endpoint tooAzure Blob Storage using custom C# Activity in Data Factory.</span></span> |
| [<span data-ttu-id="4cdd1-514">Twitter düşünceleri çözümleme örneği</span><span class="sxs-lookup"><span data-stu-id="4cdd1-514">Twitter Sentiment Analysis sample</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/TwitterAnalysisSample-CustomC%23Activity) |<span data-ttu-id="4cdd1-515">Bir Azure ML model ve düşünceleri analiz, Puanlama, tahmin vb. çağırır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-515">Invokes an Azure ML model and do sentiment analysis, scoring, prediction etc.</span></span> |
| <span data-ttu-id="4cdd1-516">[R betiği Çalıştır](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span><span class="sxs-lookup"><span data-stu-id="4cdd1-516">[Run R Script](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample).</span></span> |<span data-ttu-id="4cdd1-517">R betiği Hdınsight kümenize zaten R yüklü üzerinde olan RScript.exe çalıştırarak çağırır.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-517">Invokes R script by running RScript.exe on your HDInsight cluster that already has R Installed on it.</span></span> |
| [<span data-ttu-id="4cdd1-518">AppDomain .NET etkinliği arası</span><span class="sxs-lookup"><span data-stu-id="4cdd1-518">Cross AppDomain .NET Activity</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/CrossAppDomainDotNetActivitySample) |<span data-ttu-id="4cdd1-519">Olanları hello Data Factory başlatıcısı tarafından kullanılan farklı derleme sürümlerini kullanır</span><span class="sxs-lookup"><span data-stu-id="4cdd1-519">Uses different assembly versions from ones used by hello Data Factory launcher</span></span> |
| [<span data-ttu-id="4cdd1-520">Azure Analysis Services modelinde yeniden işleyin</span><span class="sxs-lookup"><span data-stu-id="4cdd1-520">Reprocess a model in Azure Analysis Services</span></span>](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/AzureAnalysisServicesProcessSample) |  <span data-ttu-id="4cdd1-521">Azure Analysis Services modelinde yeniden işler.</span><span class="sxs-lookup"><span data-stu-id="4cdd1-521">Reprocesses a model in Azure Analysis Services.</span></span> |

[batch-net-library]: ../batch/batch-dotnet-get-started.md
[batch-create-account]: ../batch/batch-account-create-portal.md
[batch-technical-overview]: ../batch/batch-technical-overview.md
[batch-get-started]: ../batch/batch-dotnet-get-started.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[data-factory-introduction]: data-factory-introduction.md
[azure-powershell-install]: https://github.com/Azure/azure-sdk-tools/releases


[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456

[new-azure-batch-account]: https://msdn.microsoft.com/library/mt125880.aspx
[new-azure-batch-pool]: https://msdn.microsoft.com/library/mt125936.aspx
[azure-batch-blog]: http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx

[nuget-package]: http://go.microsoft.com/fwlink/?LinkId=517478
[adf-developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[azure-preview-portal]: https://portal.azure.com/

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[hivewalkthrough]: data-factory-data-transformation-activities.md

[image-data-factory-ouput-from-custom-activity]: ./media/data-factory-use-custom-activities/OutputFilesFromCustomActivity.png

[image-data-factory-download-logs-from-custom-activity]: ./media/data-factory-use-custom-activities/DownloadLogsFromCustomActivity.png
