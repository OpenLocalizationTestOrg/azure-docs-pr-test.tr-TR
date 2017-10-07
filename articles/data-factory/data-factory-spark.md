---
title: "aaaInvoke Spark Azure veri fabrikası'ndan programlar | Microsoft Docs"
description: "MapReduce etkinliği kullanılarak bir Azure data factory tooinvoke Spark programların nasıl hello öğrenin."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: fd98931c-cab5-4d66-97cb-4c947861255c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: f88943ece7ee3d21dedbd857609f1b2713b62741
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="4f2ed-103">Azure Data Factory işlem hatlarını Spark programlardan çağırma</span><span class="sxs-lookup"><span data-stu-id="4f2ed-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="4f2ed-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="4f2ed-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="4f2ed-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="4f2ed-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="4f2ed-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="4f2ed-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="4f2ed-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="4f2ed-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="4f2ed-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="4f2ed-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="4f2ed-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="4f2ed-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="4f2ed-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="4f2ed-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="4f2ed-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="4f2ed-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="4f2ed-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="4f2ed-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="4f2ed-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="4f2ed-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="4f2ed-114">Giriş</span><span class="sxs-lookup"><span data-stu-id="4f2ed-114">Introduction</span></span>
<span data-ttu-id="4f2ed-115">Spark etkinlik hello biridir [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) Azure Data Factory tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-115">Spark Activity is one of hello [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="4f2ed-116">Bu etkinlik belirtilen hello çalıştıran Azure hdınsight'ta Apache Spark kümenizin üzerinde Spark program.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-116">This activity runs hello specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="4f2ed-117">Spark etkinliği Azure Data Lake Store birincil depolama alanı olarak kullanın Hdınsight Spark kümeleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="4f2ed-118">Spark etkinlik (kendi) Hdınsight Spark kümeleri yalnızca varolan destekler.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="4f2ed-119">Bir isteğe bağlı Hdınsight bağlı hizmeti desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="4f2ed-120">İzlenecek yol: Spark etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f2ed-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="4f2ed-121">Merhaba tipik adımları toocreate Data Factory işlem hattı Spark aktivitesiyle şunlardır.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-121">Here are hello typical steps toocreate a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="4f2ed-122">Veri Fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-122">Create a data factory.</span></span>
2. <span data-ttu-id="4f2ed-123">Bir Azure Storage bağlı hizmeti toolink Hdınsight Spark küme toohello data factory ile ilişkili Azure depolama alanınızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-123">Create an Azure Storage linked service toolink your Azure storage that is associated with your HDInsight Spark cluster toohello data factory.</span></span>     
2. <span data-ttu-id="4f2ed-124">Azure Hdınsight bağlı hizmeti toolink Azure Hdınsight toohello veri fabrikasında Apache Spark kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-124">Create an Azure HDInsight linked service toolink your Apache Spark cluster in Azure HDInsight toohello data factory.</span></span>
3. <span data-ttu-id="4f2ed-125">Toohello Azure Storage bağlı hizmeti başvuran bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-125">Create a dataset that refers toohello Azure Storage linked service.</span></span> <span data-ttu-id="4f2ed-126">Şu anda, üretilen hiçbir çıktı olsa bile bir çıkış veri kümesi bir etkinlik için belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="4f2ed-127">#2'de oluşturduğunuz toohello Hdınsight bağlı hizmeti başvuruyor Spark etkinliği ile işlem hattı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-127">Create a pipeline with Spark activity that refers toohello HDInsight linked service created in #2.</span></span> <span data-ttu-id="4f2ed-128">Merhaba etkinliği bir çıkış veri kümesi olarak hello önceki adımda oluşturduğunuz hello veri kümesi ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-128">hello activity is configured with hello dataset you created in hello previous step as an output dataset.</span></span> <span data-ttu-id="4f2ed-129">Merhaba çıktı veri kümesi, zamanlama (saatlik, günlük, vs.) hangi sürücüleri hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-129">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="4f2ed-130">Bu nedenle, Hello etkinlik gerçekten bir çıktı üretmez olsa bile hello çıktı veri kümesi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-130">Therefore, you must specify hello output dataset even though hello activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4f2ed-131">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4f2ed-131">Prerequisites</span></span>
1. <span data-ttu-id="4f2ed-132">Create bir **genel amaçlı Azure depolama hesabı** hello gözden geçirme yönergeleri izleyerek tarafından: [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4f2ed-132">Create a **general-purpose Azure Storage Account** by following instructions in hello walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="4f2ed-133">Create bir **Azure hdınsight'ta Apache Spark kümesi** hello öğreticideki yönergeler aşağıdaki tarafından: [Azure hdınsight'ta Apache Spark oluşturma küme](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="4f2ed-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in hello tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="4f2ed-134">Bu kümeyle #1. adımda oluşturduğunuz hello Azure depolama hesabı ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-134">Associate hello Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="4f2ed-135">Karşıdan yükle ve hello python komut dosyasını gözden **test.py** konumunda bulunan: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="4f2ed-135">Download and review hello python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="4f2ed-136">Karşıya yükleme **test.py** toohello **pyFiles** hello klasöründe **adfspark** , Azure Blob depolamada kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-136">Upload **test.py** toohello **pyFiles** folder in hello **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="4f2ed-137">Bunlar yoksa hello kapsayıcı ve başlangıç klasörü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-137">Create hello container and hello folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="4f2ed-138">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f2ed-138">Create data factory</span></span>
<span data-ttu-id="4f2ed-139">Bu adımda hello data factory oluşturmayla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-139">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="4f2ed-140">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4f2ed-140">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4f2ed-141">Tıklatın **yeni** hello sol menüsünde **veri + analiz**, tıklatıp **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-141">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="4f2ed-142">Merhaba, **yeni data factory** dikey penceresinde girin **SparkDF** hello adı için.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-142">In hello **New data factory** blade, enter **SparkDF** for hello Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4f2ed-143">Merhaba adı'hello Azure data Factory olması **genel benzersiz**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-143">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="4f2ed-144">Merhaba hata görürseniz: **veri fabrikası adı "SparkDF" kullanılabilir değil**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-144">If you see hello error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="4f2ed-145">Merhaba veri fabrikası (örneğin, yournameSparkDFdate ve oluşturmayı yeniden deneyin. Hello adını değiştirin</span><span class="sxs-lookup"><span data-stu-id="4f2ed-145">Change hello name of hello data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="4f2ed-146">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="4f2ed-147">Select hello **Azure aboneliği** oluşturulan hello veri fabrikası toobe istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-147">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="4f2ed-148">Var olan seçin **kaynak grubu** veya bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="4f2ed-149">Seçin **PIN toodashboard** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-149">Select **Pin toodashboard** option.</span></span>  
6. <span data-ttu-id="4f2ed-150">Tıklatın **oluşturma** hello üzerinde **yeni data factory** dikey.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-150">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4f2ed-151">toocreate Data Factory örnekleri hello üyesi olmalıdır [veri fabrikası katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello abonelik/kaynak grubu düzeyinde rol.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-151">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
7. <span data-ttu-id="4f2ed-152">Hello oluşturulmakta hello veri fabrikası gördüğünüz **Pano** hello şekilde Azure portal'ın:</span><span class="sxs-lookup"><span data-stu-id="4f2ed-152">You see hello data factory being created in hello **dashboard** of hello Azure portal as follows:</span></span>   
8. <span data-ttu-id="4f2ed-153">Merhaba veri fabrikası başarıyla oluşturulduktan sonra gösterir hello veri fabrikası sayfasına bakın hello hello data Factory içeriği.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-153">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span> <span data-ttu-id="4f2ed-154">Merhaba data factory sayfasını görmüyorsanız hello Panoda veri fabrikanızın hello kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-154">If you do not see hello data factory page, click hello tile for your data factory on hello dashboard.</span></span>

    ![Data Factory dikey penceresi](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="4f2ed-156">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f2ed-156">Create linked services</span></span>
<span data-ttu-id="4f2ed-157">Bu adımda, iki bağlı hizmet, bir toolink Spark küme tooyour data factory'nizi oluşturmak ve diğer toolink Azure depolama tooyour data factory'nizi hello.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-157">In this step, you create two linked services, one toolink your Spark cluster tooyour data factory, and hello other toolink your Azure storage tooyour data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="4f2ed-158">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f2ed-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="4f2ed-159">Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-159">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="4f2ed-160">Bu kılavuzda daha sonra bir adımda oluşturduğunuz bir veri kümesi toothis bağlantılı hizmeti anlamına gelmektedir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-160">A dataset you create in a step later in this walkthrough refers toothis linked service.</span></span> <span data-ttu-id="4f2ed-161">Hello hello sonraki adımda tanımladığınız Hdınsight bağlı hizmeti toothis bağlantılı hizmeti çok ifade eder.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-161">hello HDInsight linked service that you define in hello next step refers toothis linked service too.</span></span>  

1. <span data-ttu-id="4f2ed-162">Tıklatın **yazar ve dağıtma** hello üzerinde **Data Factory** veri fabrikanızın dikey.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-162">Click **Author and deploy** on hello **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="4f2ed-163">Merhaba Data Factory Düzenleyici görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-163">You should see hello Data Factory Editor.</span></span>
2. <span data-ttu-id="4f2ed-164">**Yeni data store**’a tıklayın ve **Azure depolama**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Yeni veri deposu - Azure Depolama - menü](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="4f2ed-166">Merhaba görmelisiniz **JSON betiği** bağlantılı hizmetinin hello Düzenleyicisi'nde bir Azure depolama alanı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-166">You should see hello **JSON script** for creating an Azure Storage linked service in hello editor.</span></span>

   ![Azure Storage bağlı hizmeti](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="4f2ed-168">Değiştir **hesap adı** ve **hesap anahtarı** Azure depolama hesabınızın hello adı ve erişim anahtarına sahip.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-168">Replace **account name** and **account key** with hello name and access key of your Azure storage account.</span></span> <span data-ttu-id="4f2ed-169">toolearn tooget depolama alanınızın erişim nasıl anahtar, hello bilgi nasıl tooview, kopyalama ve yeniden oluşturma depolama erişim anahtarları içinde hakkında [depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4f2ed-169">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="4f2ed-170">toodeploy Merhaba bağlantılı hizmeti,'ı tıklatın **dağıtma** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-170">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span> <span data-ttu-id="4f2ed-171">Merhaba bağlı hizmet başarıyla dağıtıldıktan sonra hello **taslak-1** penceresi görünmemelidir; gördüğünüz **AzureStorageLinkedService** hello hello soldaki ağaç görünümünde.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-171">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="4f2ed-172">Hdınsight bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f2ed-172">Create HDInsight linked service</span></span>
<span data-ttu-id="4f2ed-173">Bu adımda, Hdınsight Spark küme toohello data factory'nizi Azure Hdınsight bağlı hizmeti toolink oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-173">In this step, you create Azure HDInsight linked service toolink your HDInsight Spark cluster toohello data factory.</span></span> <span data-ttu-id="4f2ed-174">Merhaba Hdınsight kümesi hello ardışık bu örnekteki hello Spark etkinliğinde belirtilen kullanılan toorun hello Spark programdır.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-174">hello HDInsight cluster is used toorun hello Spark program specified in hello Spark activity of hello pipeline in this sample.</span></span>  

1. <span data-ttu-id="4f2ed-175">Düğmeyi görmüyorsanız araç çubuğunda **... Daha fazla** hello araç çubuğundan, **yeni işlem**ve ardından **Hdınsight kümesi**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-175">Click **... More** on hello toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Hdınsight bağlı hizmeti oluşturma](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="4f2ed-177">Aşağıdaki kod parçacığında toohello hello kopyalayıp **taslak-1** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-177">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="4f2ed-178">Merhaba JSON Düzenleyicisi'nde, şu adımları hello:</span><span class="sxs-lookup"><span data-stu-id="4f2ed-178">In hello JSON editor, do hello following steps:</span></span>
    1. <span data-ttu-id="4f2ed-179">Merhaba belirtin **URI** Merhaba Hdınsight Spark küme.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-179">Specify hello **URI** for hello HDInsight Spark cluster.</span></span> <span data-ttu-id="4f2ed-180">Örneğin: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="4f2ed-181">Merhaba Hello adını belirtin **kullanıcı** erişim toohello Spark kümesi vardır.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-181">Specify hello name of hello **user** who has access toohello Spark cluster.</span></span>
    3. <span data-ttu-id="4f2ed-182">Merhaba belirtin **parola** kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-182">Specify hello **password** for user.</span></span>
    4. <span data-ttu-id="4f2ed-183">Merhaba belirtin **Azure depolama bağlantılı hizmeti** hello Hdınsight Spark kümesi ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-183">Specify hello **Azure Storage linked service** that is associated with hello HDInsight Spark cluster.</span></span> <span data-ttu-id="4f2ed-184">Bu örnek,: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

    ```json
    {
        "name": "HDInsightLinkedService",
        "properties": {
            "type": "HDInsight",
            "typeProperties": {
                "clusterUri": "https://<sparkclustername>.azurehdinsight.net/",
                "userName": "admin",
                "password": "**********",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    > [!IMPORTANT]
    > - <span data-ttu-id="4f2ed-185">Spark etkinliği Azure Data Lake Store birincil depolama alanı olarak kullanın Hdınsight Spark kümeleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="4f2ed-186">Yalnızca (kendi) Hdınsight Spark kümesinde varolan Spark etkinlik destekler.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="4f2ed-187">Bir isteğe bağlı Hdınsight bağlı hizmeti desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="4f2ed-188">Bkz: [Hdınsight bağlı hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) hello hakkındaki ayrıntılar için hizmet Hdınsight bağlı.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about hello HDInsight linked service.</span></span>
3.  <span data-ttu-id="4f2ed-189">toodeploy Merhaba bağlantılı hizmeti,'ı tıklatın **dağıtma** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-189">toodeploy hello linked service, click **Deploy** on hello command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="4f2ed-190">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f2ed-190">Create output dataset</span></span>
<span data-ttu-id="4f2ed-191">Merhaba çıktı veri kümesi, zamanlama (saatlik, günlük, vs.) hangi sürücüleri hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-191">hello output dataset is what drives hello schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="4f2ed-192">Bu nedenle, Hello etkinlik gerçekten herhangi bir çıktı üretmez olsa bile hello ardışık düzeninde bir çıkış veri kümesi hello spark etkinliğinin belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-192">Therefore, you must specify an output dataset for hello spark activity in hello pipeline even though hello activity does not really produce any output.</span></span> <span data-ttu-id="4f2ed-193">Bir giriş veri kümesi hello etkinlik için belirtme isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-193">Specifying an input dataset for hello activity is optional.</span></span>

1. <span data-ttu-id="4f2ed-194">Merhaba, **Data Factory düzenleyici**, tıklatın **... Daha fazla** hello komut çubuğunda **yeni veri kümesi**seçip **Azure Blob Depolama**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-194">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="4f2ed-195">Aşağıdaki kod parçacığında toohello taslak-1 penceresinde hello kopyalayıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-195">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="4f2ed-196">Merhaba JSON parçacığı tanımlar adlı bir veri kümesi **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-196">hello JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="4f2ed-197">Ayrıca, hello sonuçları adlı hello blob kapsayıcısında depolanır belirttiğiniz **adfspark** ve adlı hello klasör **pyFiles/çıkış**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-197">In addition, you specify that hello results are stored in hello blob container called **adfspark** and hello folder called **pyFiles/output**.</span></span> <span data-ttu-id="4f2ed-198">Daha önce belirtildiği gibi bu veri kümesi kukla bir veri kümesi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="4f2ed-199">Bu örnekte Hello Spark program herhangi bir çıktı üretmez.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-199">hello Spark program in this example does not produce any output.</span></span> <span data-ttu-id="4f2ed-200">Merhaba **kullanılabilirlik** bölümü belirtiyor bu hello çıktı veri kümesi günlük oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-200">hello **availability** section specifies that hello output dataset is produced daily.</span></span>  

    ```json
    {
        "name": "OutputDataset",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "sparkoutput.txt",
                "folderPath": "adfspark/pyFiles/output",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": "\t"
                }
            },
            "availability": {
                "frequency": "Day",
                "interval": 1
            }
        }
    }
    ```
3. <span data-ttu-id="4f2ed-201">toodeploy dataset Merhaba, tıklatın **dağıtma** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-201">toodeploy hello dataset, click **Deploy** on hello command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="4f2ed-202">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4f2ed-202">Create pipeline</span></span>
<span data-ttu-id="4f2ed-203">Bu adımda oluşturduğunuz sahip işlem hattı bir **HDInsightSpark** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="4f2ed-204">Şu anda, çıktı veri kümesi hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir böylece hangi sürücüleri zamanlama, hello değil.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-204">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="4f2ed-205">Merhaba etkinlik herhangi bir girdi almazsa oluşturma hello girdi veri kümesi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-205">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="4f2ed-206">Bu nedenle, hiçbir girdi veri kümesi bu örnekte belirtilir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="4f2ed-207">Merhaba, **Data Factory düzenleyici**, tıklatın **... Daha fazla** hello komut çubuğunda ve ardından **yeni işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-207">In hello **Data Factory Editor**, click **… More** on hello command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="4f2ed-208">Merhaba taslak-1 penceresinde Hello komut dosyası komut dosyası izleyen hello ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="4f2ed-208">Replace hello script in hello Draft-1 window with hello following script:</span></span>

    ```json
    {
        "name": "SparkPipeline",
        "properties": {
            "activities": [
                {
                    "type": "HDInsightSpark",
                    "typeProperties": {
                        "rootPath": "adfspark\\pyFiles",
                        "entryFilePath": "test.py",
                        "getDebugInfo": "Always"
                    },
                    "outputs": [
                        {
                            "name": "OutputDataset"
                        }
                    ],
                    "name": "MySparkActivity",
                    "linkedServiceName": "HDInsightLinkedService"
                }
            ],
            "start": "2017-02-05T00:00:00Z",
            "end": "2017-02-06T00:00:00Z"
        }
    }
    ```
    <span data-ttu-id="4f2ed-209">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="4f2ed-209">Note hello following points:</span></span>
    - <span data-ttu-id="4f2ed-210">Merhaba **türü** özelliği çok ayarlanmış**HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-210">hello **type** property is set too**HDInsightSpark**.</span></span>
    - <span data-ttu-id="4f2ed-211">Merhaba **rootPath** çok ayarlanır**adfspark\\pyFiles** adfspark hello Azure Blob kapsayıcısı ve pyFiles olduğu ince kapsayıcıdaki klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-211">hello **rootPath** is set too**adfspark\\pyFiles** where adfspark is hello Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="4f2ed-212">Bu örnekte, hello Azure Blob Storage hello hello Spark kümesi ile ilişkili olan bir ' dir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-212">In this example, hello Azure Blob Storage is hello one that is associated with hello Spark cluster.</span></span> <span data-ttu-id="4f2ed-213">Merhaba dosya tooa yükleyebilirsiniz farklı Azure depolama.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-213">You can upload hello file tooa different Azure Storage.</span></span> <span data-ttu-id="4f2ed-214">Bunu yaparsanız, bir Azure Storage bağlı hizmeti toolink bu depolama hesabı toohello veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-214">If you do so, create an Azure Storage linked service toolink that storage account toohello data factory.</span></span> <span data-ttu-id="4f2ed-215">Ardından, hello için bir değer olarak hello hello bağlı hizmetin adını belirtin **sparkJobLinkedService** özelliği.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-215">Then, specify hello name of hello linked service as a value for hello **sparkJobLinkedService** property.</span></span> <span data-ttu-id="4f2ed-216">Bkz: [Spark etkinlik özellikleri](#spark-activity-properties) bu özellik ve Spark etkinlik hello tarafından desteklenen diğer özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by hello Spark Activity.</span></span>  
    - <span data-ttu-id="4f2ed-217">Merhaba **entryFilePath** toohello ayarlamak **test.py**, hello python dosyası değil.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-217">hello **entryFilePath** is set toohello **test.py**, which is hello python file.</span></span>
    - <span data-ttu-id="4f2ed-218">Merhaba **Getdebugınfo** özelliği çok ayarlanmış**her zaman**, yani hello günlük dosyaları her zaman oluşturulan (başarılı veya başarısız).</span><span class="sxs-lookup"><span data-stu-id="4f2ed-218">hello **getDebugInfo** property is set too**Always**, which means hello log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="4f2ed-219">Bu özellik çok ayarlamayın öneririz`Always` bir üretim ortamında bir sorunu gidermeye çalışıyor değilseniz.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-219">We recommend that you do not set this property too`Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="4f2ed-220">Merhaba **çıkarır** bölümü bir çıkış veri kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-220">hello **outputs** section has one output dataset.</span></span> <span data-ttu-id="4f2ed-221">Merhaba spark program herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-221">You must specify an output dataset even if hello spark program does not produce any output.</span></span> <span data-ttu-id="4f2ed-222">Merhaba çıkış veri kümesi sürücüleri hello zamanlama hello ardışık düzen (saatlik, günlük, vs.).</span><span class="sxs-lookup"><span data-stu-id="4f2ed-222">hello output dataset drives hello schedule for hello pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="4f2ed-223">Spark etkinliği tarafından desteklenen hello özellikleri hakkında daha fazla ayrıntı için bkz: [Spark etkinlik özellikleri](#spark-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-223">For details about hello properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="4f2ed-224">toodeploy hello ardışık tıklatın **dağıtma** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-224">toodeploy hello pipeline, click **Deploy** on hello command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="4f2ed-225">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="4f2ed-225">Monitor pipeline</span></span>
1. <span data-ttu-id="4f2ed-226">Tıklatın **X** tooclose Data Factory Düzenleyici dikey ve toonavigate toohello Data Factory giriş sayfasında yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-226">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory home page.</span></span> <span data-ttu-id="4f2ed-227">Tıklatın **izleme ve yönetme** toolaunch hello başka bir sekmesinde uygulama izleme.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-227">Click **Monitor and Manage** toolaunch hello monitoring application in another tab.</span></span>

    ![İzleme ve yönetme bölmesi](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="4f2ed-229">Değişiklik hello **başlangıç zamanı** hello üstünde çok filtre**1/2/2017**, tıklatıp **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-229">Change hello **Start time** filter at hello top too**2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="4f2ed-230">Hello arasında yalnızca bir gününü (2017-02-01) başlangıç ve bitiş saatlerini (2017-02-02) hello ardışık olduğundan yalnızca bir etkinlik penceresini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-230">You should see only one activity window as there is only one day between hello start (2017-02-01) and end times (2017-02-02) of hello pipeline.</span></span> <span data-ttu-id="4f2ed-231">Bu hello veri dilim onaylayın **hazır** durumu.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-231">Confirm that hello data slice is in **ready** state.</span></span>

    ![Merhaba işlem hattını izleme](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="4f2ed-233">Select hello **etkinlik penceresini** toosee etkinliği hakkında ayrıntılı bilgi çalıştırmak hello.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-233">Select hello **activity window** toosee details about hello activity run.</span></span> <span data-ttu-id="4f2ed-234">Bir hata varsa, hello sağ bölmedeki hakkındaki ayrıntıları bakın.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-234">If there is an error, you see details about it in hello right pane.</span></span>

### <a name="verify-hello-results"></a><span data-ttu-id="4f2ed-235">Merhaba sonuçlarını doğrulayın</span><span class="sxs-lookup"><span data-stu-id="4f2ed-235">Verify hello results</span></span>

1. <span data-ttu-id="4f2ed-236">Başlatma **Jupyter not defteri** giderek Hdınsight Spark kümenizin: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="4f2ed-237">Ayrıca, Hdınsight Spark kümeniz için küme Panosu başlatın ve sonra başlatın **Jupyter not defteri**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="4f2ed-238">Tıklatın **yeni** -> **PySpark** toostart yeni bir not defteri.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-238">Click **New** -> **PySpark** toostart a new notebook.</span></span>

    ![Yeni Jupyter not defteri](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="4f2ed-240">Çalışma hello komutu aşağıdaki hello metin kopyalama/yapıştırma ve tuşlarına basarak **SHIFT + ENTER** hello ikinci ifade hello sonunda.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-240">Run hello following command by copy/pasting hello text and pressing **SHIFT + ENTER** at hello end of hello second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="4f2ed-241">Merhaba hvac tablodan hello veri gördüğünüzü onaylayın:</span><span class="sxs-lookup"><span data-stu-id="4f2ed-241">Confirm that you see hello data from hello hvac table:</span></span>  

    ![Jupyter sorgu sonuçları](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="4f2ed-243">Bkz: [bir Spark SQL sorgusu çalıştırmanız](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) bölüm ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="4f2ed-244">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="4f2ed-244">Troubleshooting</span></span>
<span data-ttu-id="4f2ed-245">Ayarladığınız bu yana **Getdebugınfo** çok**her zaman**, gördüğünüz bir **günlük** hello alt **pyFiles** klasörü, Azure Blob kapsayıcısında.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-245">Since you set **getDebugInfo** too**Always**, you see a **log** subfolder in hello **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="4f2ed-246">Merhaba Günlük klasörü Hello günlük dosyasına ek ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-246">hello log file in hello log folder provides additional details.</span></span> <span data-ttu-id="4f2ed-247">Bu günlük dosyası bir hata olduğunda özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="4f2ed-248">Bir üretim ortamında tooset isteyebilirsiniz, çok**hatası**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-248">In a production environment, you may want tooset it too**Failure**.</span></span>

<span data-ttu-id="4f2ed-249">Daha fazla sorun giderme için aşağıdaki adımları hello:</span><span class="sxs-lookup"><span data-stu-id="4f2ed-249">For further troubleshooting, do hello following steps:</span></span>


1. <span data-ttu-id="4f2ed-250">Çok gidin`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-250">Navigate too`https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![YARN kullanıcı arabirimini uygulama](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="4f2ed-252">Tıklatın **günlükleri** hello birini denemeleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-252">Click **Logs** for one of hello run attempts.</span></span>

    ![Uygulama sayfası](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="4f2ed-254">Merhaba günlük sayfasındaki ek hata bilgileri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-254">You should see additional error information in hello log page.</span></span>

    ![Günlük hatası](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="4f2ed-256">Aşağıdaki bölümlerde hello Data Factory varlıkları toouse Apache Spark kümesi ve data factory'nizi Spark etkinliğinde hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-256">hello following sections provide information about Data Factory entities toouse Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="4f2ed-257">Spark etkinlik özellikleri</span><span class="sxs-lookup"><span data-stu-id="4f2ed-257">Spark activity properties</span></span>
<span data-ttu-id="4f2ed-258">Spark etkinliği ile işlem hattı hello örnek JSON tanımını şöyledir:</span><span class="sxs-lookup"><span data-stu-id="4f2ed-258">Here is hello sample JSON definition of a pipeline with Spark Activity:</span></span>    

```json
{
    "name": "SparkPipeline",
    "properties": {
        "activities": [
            {
                "type": "HDInsightSpark",
                "typeProperties": {
                    "rootPath": "adfspark\\pyFiles",
                    "entryFilePath": "test.py",
                    "arguments": [ "arg1", "arg2" ],
                    "sparkConfig": {
                        "spark.python.worker.memory": "512m"
                    }
                    "getDebugInfo": "Always"
                },
                "outputs": [
                    {
                        "name": "OutputDataset"
                    }
                ],
                "name": "MySparkActivity",
                "description": "This activity invokes hello Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="4f2ed-259">Merhaba aşağıdaki tabloda hello JSON tanımını kullanılan hello JSON özellikleri açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="4f2ed-259">hello following table describes hello JSON properties used in hello JSON definition:</span></span>

| <span data-ttu-id="4f2ed-260">Özellik</span><span class="sxs-lookup"><span data-stu-id="4f2ed-260">Property</span></span> | <span data-ttu-id="4f2ed-261">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4f2ed-261">Description</span></span> | <span data-ttu-id="4f2ed-262">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4f2ed-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="4f2ed-263">ad</span><span class="sxs-lookup"><span data-stu-id="4f2ed-263">name</span></span> | <span data-ttu-id="4f2ed-264">Hello etkinliğinde hello ardışık düzen adı.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-264">Name of hello activity in hello pipeline.</span></span> | <span data-ttu-id="4f2ed-265">Evet</span><span class="sxs-lookup"><span data-stu-id="4f2ed-265">Yes</span></span> |
| <span data-ttu-id="4f2ed-266">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4f2ed-266">description</span></span> | <span data-ttu-id="4f2ed-267">Hangi hello etkinliği açıklayan metin yapar.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-267">Text describing what hello activity does.</span></span> | <span data-ttu-id="4f2ed-268">Hayır</span><span class="sxs-lookup"><span data-stu-id="4f2ed-268">No</span></span> |
| <span data-ttu-id="4f2ed-269">type</span><span class="sxs-lookup"><span data-stu-id="4f2ed-269">type</span></span> | <span data-ttu-id="4f2ed-270">Bu özellik tooHDInsightSpark ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-270">This property must be set tooHDInsightSpark.</span></span> | <span data-ttu-id="4f2ed-271">Evet</span><span class="sxs-lookup"><span data-stu-id="4f2ed-271">Yes</span></span> |
| <span data-ttu-id="4f2ed-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4f2ed-272">linkedServiceName</span></span> | <span data-ttu-id="4f2ed-273">Merhaba Hdınsight adını bağlantılı hizmetinin hangi hello Spark programı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-273">Name of hello HDInsight linked service on which hello Spark program runs.</span></span> | <span data-ttu-id="4f2ed-274">Evet</span><span class="sxs-lookup"><span data-stu-id="4f2ed-274">Yes</span></span> |
| <span data-ttu-id="4f2ed-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="4f2ed-275">rootPath</span></span> | <span data-ttu-id="4f2ed-276">Hello Azure Blob kapsayıcısı ve hello Spark dosyasını içeren klasör.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-276">hello Azure Blob container and folder that contains hello Spark file.</span></span> <span data-ttu-id="4f2ed-277">Merhaba dosya adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-277">hello file name is case-sensitive.</span></span> | <span data-ttu-id="4f2ed-278">Evet</span><span class="sxs-lookup"><span data-stu-id="4f2ed-278">Yes</span></span> |
| <span data-ttu-id="4f2ed-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="4f2ed-279">entryFilePath</span></span> | <span data-ttu-id="4f2ed-280">Göreli yol toohello kök klasöründe hello Spark kod/paketi.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-280">Relative path toohello root folder of hello Spark code/package.</span></span> | <span data-ttu-id="4f2ed-281">Evet</span><span class="sxs-lookup"><span data-stu-id="4f2ed-281">Yes</span></span> |
| <span data-ttu-id="4f2ed-282">className</span><span class="sxs-lookup"><span data-stu-id="4f2ed-282">className</span></span> | <span data-ttu-id="4f2ed-283">Uygulamanın Java/Spark ana sınıfı</span><span class="sxs-lookup"><span data-stu-id="4f2ed-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="4f2ed-284">Hayır</span><span class="sxs-lookup"><span data-stu-id="4f2ed-284">No</span></span> |
| <span data-ttu-id="4f2ed-285">Bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="4f2ed-285">arguments</span></span> | <span data-ttu-id="4f2ed-286">Komut satırı bağımsız değişkenleri toohello Spark program listesi.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-286">A list of command-line arguments toohello Spark program.</span></span> | <span data-ttu-id="4f2ed-287">Hayır</span><span class="sxs-lookup"><span data-stu-id="4f2ed-287">No</span></span> |
| <span data-ttu-id="4f2ed-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="4f2ed-288">proxyUser</span></span> | <span data-ttu-id="4f2ed-289">Merhaba kullanıcı hesabı tooimpersonate tooexecute hello Spark programı</span><span class="sxs-lookup"><span data-stu-id="4f2ed-289">hello user account tooimpersonate tooexecute hello Spark program</span></span> | <span data-ttu-id="4f2ed-290">Hayır</span><span class="sxs-lookup"><span data-stu-id="4f2ed-290">No</span></span> |
| <span data-ttu-id="4f2ed-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="4f2ed-291">sparkConfig</span></span> | <span data-ttu-id="4f2ed-292">Merhaba konu başlığı altında listelenen Spark yapılandırma özellikleri için değerleri belirtin: [Spark yapılandırması - uygulama özellikleri](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="4f2ed-292">Specify values for Spark configuration properties listed in hello topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="4f2ed-293">Hayır</span><span class="sxs-lookup"><span data-stu-id="4f2ed-293">No</span></span> |
| <span data-ttu-id="4f2ed-294">Getdebugınfo</span><span class="sxs-lookup"><span data-stu-id="4f2ed-294">getDebugInfo</span></span> | <span data-ttu-id="4f2ed-295">Merhaba Spark günlük dosyalarını kopyalanan toohello Hdınsight küme tarafından kullanılan Azure depolama olduğunda belirtir (veya) sparkJobLinkedService tarafından belirtilen.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-295">Specifies when hello Spark log files are copied toohello Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="4f2ed-296">İzin verilen değerler: None, her zaman veya hata.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="4f2ed-297">Varsayılan değer: yok.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-297">Default value: None.</span></span> | <span data-ttu-id="4f2ed-298">Hayır</span><span class="sxs-lookup"><span data-stu-id="4f2ed-298">No</span></span> |
| <span data-ttu-id="4f2ed-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="4f2ed-299">sparkJobLinkedService</span></span> | <span data-ttu-id="4f2ed-300">Merhaba hello Spark iş dosyası, bağımlılıklar ve günlükleri tutan Azure Storage bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-300">hello Azure Storage linked service that holds hello Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="4f2ed-301">Bu özellik için bir değer belirtmezseniz, Hdınsight kümesi ile ilişkili hello depolama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-301">If you do not specify a value for this property, hello storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="4f2ed-302">Hayır</span><span class="sxs-lookup"><span data-stu-id="4f2ed-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="4f2ed-303">Klasör yapısı</span><span class="sxs-lookup"><span data-stu-id="4f2ed-303">Folder structure</span></span>
<span data-ttu-id="4f2ed-304">Merhaba Spark etkinliği bir satır içi komut dosyası Pig olarak desteklemez ve Hive etkinlikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-304">hello Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="4f2ed-305">Spark işleri de Pig/Hive işleri daha fazla genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="4f2ed-306">Spark işleri, birden çok bağımlılıkları gibi sağlayabilirsiniz jar (Merhaba java sınıf yerleştirilen) paketleri, python dosyaları (PYTHONPATH hello yerleştirilmiş) ve diğer dosyaları.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in hello java CLASSPATH), python files (placed on hello PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="4f2ed-307">Merhaba hello Hdınsight bağlı hizmeti tarafından başvurulan Azure Blob Depolama Klasör yapısındaki aşağıdaki hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-307">Create hello following folder structure in hello Azure Blob storage referenced by hello HDInsight linked service.</span></span> <span data-ttu-id="4f2ed-308">Ardından, bağımlı dosyaları toohello uygun alt klasörleri tarafından temsil edilen hello kök klasöründe karşıya **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-308">Then, upload dependent files toohello appropriate sub folders in hello root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="4f2ed-309">Örneğin, python dosyalar toohello pyFiles alt ve jar dosyalarını toohello Kavanoz hello kök klasörünün alt karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-309">For example, upload python files toohello pyFiles subfolder and jar files toohello jars subfolder of hello root folder.</span></span> <span data-ttu-id="4f2ed-310">Çalışma zamanında Data Factory hizmetinin hello Azure Blob Depolama Klasör yapısındaki aşağıdaki hello bekler:</span><span class="sxs-lookup"><span data-stu-id="4f2ed-310">At runtime, Data Factory service expects hello following folder structure in hello Azure Blob storage:</span></span>     

| <span data-ttu-id="4f2ed-311">Yol</span><span class="sxs-lookup"><span data-stu-id="4f2ed-311">Path</span></span> | <span data-ttu-id="4f2ed-312">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4f2ed-312">Description</span></span> | <span data-ttu-id="4f2ed-313">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4f2ed-313">Required</span></span> | <span data-ttu-id="4f2ed-314">Tür</span><span class="sxs-lookup"><span data-stu-id="4f2ed-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="4f2ed-315">.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-315">.</span></span> | <span data-ttu-id="4f2ed-316">Merhaba Spark hello depolama bağlı hizmeti işinde Hello kök yolu</span><span class="sxs-lookup"><span data-stu-id="4f2ed-316">hello root path of hello Spark job in hello storage linked service</span></span>    | <span data-ttu-id="4f2ed-317">Evet</span><span class="sxs-lookup"><span data-stu-id="4f2ed-317">Yes</span></span> | <span data-ttu-id="4f2ed-318">Klasör</span><span class="sxs-lookup"><span data-stu-id="4f2ed-318">Folder</span></span> |
| <span data-ttu-id="4f2ed-319">&lt;Kullanıcı tanımlı&gt;</span><span class="sxs-lookup"><span data-stu-id="4f2ed-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="4f2ed-320">toohello girdi dosyası hello Spark işin işaret eden hello yolu</span><span class="sxs-lookup"><span data-stu-id="4f2ed-320">hello path pointing toohello entry file of hello Spark job</span></span> | <span data-ttu-id="4f2ed-321">Evet</span><span class="sxs-lookup"><span data-stu-id="4f2ed-321">Yes</span></span> | <span data-ttu-id="4f2ed-322">Dosya</span><span class="sxs-lookup"><span data-stu-id="4f2ed-322">File</span></span> |
| <span data-ttu-id="4f2ed-323">. / jar'lar</span><span class="sxs-lookup"><span data-stu-id="4f2ed-323">./jars</span></span> | <span data-ttu-id="4f2ed-324">Bu klasörü altındaki tüm dosyaları karşıya ve üzerinde hello kümesinin hello java sınıf yerleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="4f2ed-324">All files under this folder are uploaded and placed on hello java classpath of hello cluster</span></span> | <span data-ttu-id="4f2ed-325">Hayır</span><span class="sxs-lookup"><span data-stu-id="4f2ed-325">No</span></span> | <span data-ttu-id="4f2ed-326">Klasör</span><span class="sxs-lookup"><span data-stu-id="4f2ed-326">Folder</span></span> |
| <span data-ttu-id="4f2ed-327">. / pyFiles</span><span class="sxs-lookup"><span data-stu-id="4f2ed-327">./pyFiles</span></span> | <span data-ttu-id="4f2ed-328">Bu klasörü altındaki tüm dosyaları karşıya ve hello kümesinin PYTHONPATH hello üzerinde yerleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="4f2ed-328">All files under this folder are uploaded and placed on hello PYTHONPATH of hello cluster</span></span> | <span data-ttu-id="4f2ed-329">Hayır</span><span class="sxs-lookup"><span data-stu-id="4f2ed-329">No</span></span> | <span data-ttu-id="4f2ed-330">Klasör</span><span class="sxs-lookup"><span data-stu-id="4f2ed-330">Folder</span></span> |
| <span data-ttu-id="4f2ed-331">. / dosyaları</span><span class="sxs-lookup"><span data-stu-id="4f2ed-331">./files</span></span> | <span data-ttu-id="4f2ed-332">Bu klasörü altındaki tüm dosyaları karşıya ve yürütücü çalışma dizini yerleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="4f2ed-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="4f2ed-333">Hayır</span><span class="sxs-lookup"><span data-stu-id="4f2ed-333">No</span></span> | <span data-ttu-id="4f2ed-334">Klasör</span><span class="sxs-lookup"><span data-stu-id="4f2ed-334">Folder</span></span> |
| <span data-ttu-id="4f2ed-335">. / arşivler</span><span class="sxs-lookup"><span data-stu-id="4f2ed-335">./archives</span></span> | <span data-ttu-id="4f2ed-336">Bu klasörü altındaki tüm dosyaları sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="4f2ed-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="4f2ed-337">Hayır</span><span class="sxs-lookup"><span data-stu-id="4f2ed-337">No</span></span> | <span data-ttu-id="4f2ed-338">Klasör</span><span class="sxs-lookup"><span data-stu-id="4f2ed-338">Folder</span></span> |
| <span data-ttu-id="4f2ed-339">. / günlükleri</span><span class="sxs-lookup"><span data-stu-id="4f2ed-339">./logs</span></span> | <span data-ttu-id="4f2ed-340">Merhaba Spark kümesi günlüklerinden depolandığı hello klasör.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-340">hello folder where logs from hello Spark cluster are stored.</span></span>| <span data-ttu-id="4f2ed-341">Hayır</span><span class="sxs-lookup"><span data-stu-id="4f2ed-341">No</span></span> | <span data-ttu-id="4f2ed-342">Klasör</span><span class="sxs-lookup"><span data-stu-id="4f2ed-342">Folder</span></span> |

<span data-ttu-id="4f2ed-343">Hello Azure Blob Storage Hdınsight bağlı hizmeti hello tarafından başvurulan iki Spark iş dosyaları içeren bir depolama için örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4f2ed-343">Here is an example for a storage containing two Spark job files in hello Azure Blob Storage referenced by hello HDInsight linked service.</span></span>

```
SparkJob1
    main.jar
    files
        input1.txt
        input2.txt
    jars
        package1.jar
        package2.jar
    logs

SparkJob2
    main.py
    pyFiles
        scrip1.py
        script2.py
    logs
```
