---
title: "Azure Data Factory Spark programlardan çağırma | Microsoft Docs"
description: "MapReduce etkinliği kullanarak Azure data factory Spark programlardan çağırma öğrenin."
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
ms.openlocfilehash: 57894bbdd9208f8c32eb65e29f04e2ae723780ca
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="invoke-spark-programs-from-azure-data-factory-pipelines"></a><span data-ttu-id="ee3e8-103">Azure Data Factory işlem hatlarını Spark programlardan çağırma</span><span class="sxs-lookup"><span data-stu-id="ee3e8-103">Invoke Spark programs from Azure Data Factory pipelines</span></span>

> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="ee3e8-104">Hive etkinliği</span><span class="sxs-lookup"><span data-stu-id="ee3e8-104">Hive Activity</span></span>](data-factory-hive-activity.md)
> * [<span data-ttu-id="ee3e8-105">Pig etkinliği</span><span class="sxs-lookup"><span data-stu-id="ee3e8-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="ee3e8-106">MapReduce etkinliği</span><span class="sxs-lookup"><span data-stu-id="ee3e8-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="ee3e8-107">Hadoop akış etkinliği</span><span class="sxs-lookup"><span data-stu-id="ee3e8-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="ee3e8-108">Spark etkinliği</span><span class="sxs-lookup"><span data-stu-id="ee3e8-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="ee3e8-109">Machine Learning Batch Yürütme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="ee3e8-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="ee3e8-110">Machine Learning Kaynak Güncelleştirme Etkinliği</span><span class="sxs-lookup"><span data-stu-id="ee3e8-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="ee3e8-111">Saklı Yordam Etkinliği</span><span class="sxs-lookup"><span data-stu-id="ee3e8-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="ee3e8-112">Data Lake Analytics U-SQL Etkinliği</span><span class="sxs-lookup"><span data-stu-id="ee3e8-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="ee3e8-113">.NET özel etkinlik</span><span class="sxs-lookup"><span data-stu-id="ee3e8-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

## <a name="introduction"></a><span data-ttu-id="ee3e8-114">Giriş</span><span class="sxs-lookup"><span data-stu-id="ee3e8-114">Introduction</span></span>
<span data-ttu-id="ee3e8-115">Spark etkinlik biridir [veri dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) Azure Data Factory tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-115">Spark Activity is one of the [data transformation activities](data-factory-data-transformation-activities.md) supported by Azure Data Factory.</span></span> <span data-ttu-id="ee3e8-116">Bu etkinlik, Azure hdınsight'ta Apache Spark kümenizde belirtilen Spark programı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-116">This activity runs the specified Spark program on your Apache Spark cluster in Azure HDInsight.</span></span>    

> [!IMPORTANT]
> - <span data-ttu-id="ee3e8-117">Spark etkinliği Azure Data Lake Store birincil depolama alanı olarak kullanın Hdınsight Spark kümeleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-117">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
> - <span data-ttu-id="ee3e8-118">Spark etkinlik (kendi) Hdınsight Spark kümeleri yalnızca varolan destekler.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-118">Spark Activity supports only existing (your own) HDInsight Spark clusters.</span></span> <span data-ttu-id="ee3e8-119">Bir isteğe bağlı Hdınsight bağlı hizmeti desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-119">It does not support an on-demand HDInsight linked service.</span></span>

## <a name="walkthrough-create-a-pipeline-with-spark-activity"></a><span data-ttu-id="ee3e8-120">İzlenecek yol: Spark etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee3e8-120">Walkthrough: create a pipeline with Spark activity</span></span>
<span data-ttu-id="ee3e8-121">Spark etkinliği ile bir Data Factory işlem hattı oluşturmak için genel adımlar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-121">Here are the typical steps to create a Data Factory pipeline with a Spark activity.</span></span>  

1. <span data-ttu-id="ee3e8-122">Veri Fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-122">Create a data factory.</span></span>
2. <span data-ttu-id="ee3e8-123">Hdınsight Spark kümenize data factory ile ilişkili Azure depolama alanınızı bağlamak için bir Azure depolama bağlantılı hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-123">Create an Azure Storage linked service to link your Azure storage that is associated with your HDInsight Spark cluster to the data factory.</span></span>     
2. <span data-ttu-id="ee3e8-124">Azure hdınsight'ta Apache Spark kümenizin data factory'ye bağlamak için bir Azure Hdınsight bağlı hizmeti oluşturma.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-124">Create an Azure HDInsight linked service to link your Apache Spark cluster in Azure HDInsight to the data factory.</span></span>
3. <span data-ttu-id="ee3e8-125">Azure Storage bağlı hizmeti başvuran bir veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-125">Create a dataset that refers to the Azure Storage linked service.</span></span> <span data-ttu-id="ee3e8-126">Şu anda, üretilen hiçbir çıktı olsa bile bir çıkış veri kümesi bir etkinlik için belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-126">Currently, you must specify an output dataset for an activity even if there is no output being produced.</span></span>  
4. <span data-ttu-id="ee3e8-127">#2'de oluşturulan Hdınsight bağlı hizmeti başvurduğu Spark etkinliği ile işlem hattı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-127">Create a pipeline with Spark activity that refers to the HDInsight linked service created in #2.</span></span> <span data-ttu-id="ee3e8-128">Etkinlik, bir çıkış veri kümesi önceki adımda oluşturduğunuz veri kümesi ile yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-128">The activity is configured with the dataset you created in the previous step as an output dataset.</span></span> <span data-ttu-id="ee3e8-129">Çıktı veri kümesi ne zamanlama (saatlik, günlük, vs.) sürücüleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-129">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="ee3e8-130">Bu nedenle, etkinlik gerçekten bir çıktı üretmez olsa da, çıktı veri kümesi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-130">Therefore, you must specify the output dataset even though the activity does not really produce an output.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="ee3e8-131">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ee3e8-131">Prerequisites</span></span>
1. <span data-ttu-id="ee3e8-132">Create bir **genel amaçlı Azure depolama hesabı** Kılavuzu'ndaki yönergeleri izleyen tarafından: [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="ee3e8-132">Create a **general-purpose Azure Storage Account** by following instructions in the walkthrough: [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>  
2. <span data-ttu-id="ee3e8-133">Create bir **Azure hdınsight'ta Apache Spark kümesi** öğreticideki yönergeler aşağıdaki tarafından: [Azure hdınsight'ta Apache Spark oluşturma küme](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="ee3e8-133">Create an **Apache Spark cluster in Azure HDInsight** by following instructions in the tutorial: [Create Apache Spark cluster in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="ee3e8-134">Bu kümeyle #1. adımda oluşturduğunuz Azure depolama hesabı ilişkilendirin.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-134">Associate the Azure storage account you created in step #1 with this cluster.</span></span>  
3. <span data-ttu-id="ee3e8-135">Karşıdan yükle ve python komut dosyasını gözden **test.py** konumunda bulunan: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span><span class="sxs-lookup"><span data-stu-id="ee3e8-135">Download and review the python script file **test.py** located at: [https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py](https://adftutorialfiles.blob.core.windows.net/sparktutorial/test.py).</span></span>  
3.  <span data-ttu-id="ee3e8-136">Karşıya yükleme **test.py** için **pyFiles** klasöründe **adfspark** , Azure Blob depolamada kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-136">Upload **test.py** to the **pyFiles** folder in the **adfspark** container in your Azure Blob storage.</span></span> <span data-ttu-id="ee3e8-137">Bunlar yoksa kapsayıcıyı ve klasör oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-137">Create the container and the folder if they do not exist.</span></span>

### <a name="create-data-factory"></a><span data-ttu-id="ee3e8-138">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee3e8-138">Create data factory</span></span>
<span data-ttu-id="ee3e8-139">Bu adımda data factory oluşturmayla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-139">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="ee3e8-140">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-140">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ee3e8-141">Soldaki menüde **YENİ**, **Veri + Analiz** ve **Data Factory** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-141">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="ee3e8-142">İçinde **yeni data factory** dikey penceresinde girin **SparkDF** adı.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-142">In the **New data factory** blade, enter **SparkDF** for the Name.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ee3e8-143">Azure data factory adı **küresel olarak benzersiz** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-143">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="ee3e8-144">Hata görürseniz: **veri fabrikası adı "SparkDF" kullanılabilir değil**.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-144">If you see the error: **Data factory name “SparkDF” is not available**.</span></span> <span data-ttu-id="ee3e8-145">(Örneğin, yournameSparkDFdate ve oluşturmayı yeniden deneyin. veri fabrikasının adını değiştirin</span><span class="sxs-lookup"><span data-stu-id="ee3e8-145">Change the name of the data factory (for example, yournameSparkDFdate, and try creating again.</span></span> <span data-ttu-id="ee3e8-146">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-146">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
4. <span data-ttu-id="ee3e8-147">Data factory’yi oluşturmak istediğiniz **Azure aboneliği**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-147">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="ee3e8-148">Var olan seçin **kaynak grubu** veya bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-148">Select an existing **resource group** or create an Azure resource group.</span></span>
6. <span data-ttu-id="ee3e8-149">Seçin **panoya Sabitle** seçeneği.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-149">Select **Pin to dashboard** option.</span></span>  
6. <span data-ttu-id="ee3e8-150">**Yeni data factory** dikey penceresinde **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-150">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ee3e8-151">Data Factory örnekleri oluşturmak için abonelik/kaynak grubu düzeyinde [Data Factory Katılımcısı](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rolünün üyesi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-151">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
7. <span data-ttu-id="ee3e8-152">Oluşturulmakta veri fabrikası gördüğünüz **Pano** şekilde Azure portalının:</span><span class="sxs-lookup"><span data-stu-id="ee3e8-152">You see the data factory being created in the **dashboard** of the Azure portal as follows:</span></span>   
8. <span data-ttu-id="ee3e8-153">Data factory sorunsuz oluşturulduktan sonra data factory sayfasını görürsünüz, burada size data factory içeriği gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-153">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span> <span data-ttu-id="ee3e8-154">Data factory sayfasını görmüyorsanız Panoda veri fabrikanızın kutucuğa tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-154">If you do not see the data factory page, click the tile for your data factory on the dashboard.</span></span>

    ![Data Factory dikey penceresi](./media/data-factory-spark/data-factory-blade.png)

### <a name="create-linked-services"></a><span data-ttu-id="ee3e8-156">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee3e8-156">Create linked services</span></span>
<span data-ttu-id="ee3e8-157">Bu adımda, veri fabrikası ve diğer Azure depolama alanınızı veri fabrikanıza bağlamak için Spark kümenizin bağlamak için iki bağlı hizmet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-157">In this step, you create two linked services, one to link your Spark cluster to your data factory, and the other to link your Azure storage to your data factory.</span></span>  

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="ee3e8-158">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee3e8-158">Create Azure Storage linked service</span></span>
<span data-ttu-id="ee3e8-159">Bu adımda, Azure Depolama hesabınızı veri fabrikanıza bağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-159">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="ee3e8-160">Bu kılavuzda daha sonra bir adımda oluşturduğunuz bir veri kümesi bu bağlı hizmete başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-160">A dataset you create in a step later in this walkthrough refers to this linked service.</span></span> <span data-ttu-id="ee3e8-161">Sonraki adımda tanımladığınız Hdınsight bağlı hizmeti bu bağlantılı hizmeti çok ifade eder.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-161">The HDInsight linked service that you define in the next step refers to this linked service too.</span></span>  

1. <span data-ttu-id="ee3e8-162">Tıklatın **yazar ve dağıtma** üzerinde **Data Factory** veri fabrikanızın dikey.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-162">Click **Author and deploy** on the **Data Factory** blade for your data factory.</span></span> <span data-ttu-id="ee3e8-163">Data Factory Düzenleyicisi’ni görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-163">You should see the Data Factory Editor.</span></span>
2. <span data-ttu-id="ee3e8-164">**Yeni data store**’a tıklayın ve **Azure depolama**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-164">Click **New data store** and choose **Azure storage**.</span></span>

   ![Yeni veri deposu - Azure Depolama - menü](./media/data-factory-spark/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="ee3e8-166">Görmeniz gerekir **JSON betiği** bağlantılı hizmetinin Düzenleyicisi'nde bir Azure depolama alanı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-166">You should see the **JSON script** for creating an Azure Storage linked service in the editor.</span></span>

   ![Azure Storage bağlı hizmeti](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="ee3e8-168">Değiştir **hesap adı** ve **hesap anahtarı** Azure depolama hesabınızın adını ve erişim anahtarına sahip.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-168">Replace **account name** and **account key** with the name and access key of your Azure storage account.</span></span> <span data-ttu-id="ee3e8-169">Depolama erişim anahtarınızı nasıl alabileceğinizi öğrenmek için [Depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account) sayfasındaki depolama erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma bilgilerine bakın.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-169">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="ee3e8-170">Bağlantılı hizmet dağıtmak için **dağıtma** komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-170">To deploy the linked service, click **Deploy** on the command bar.</span></span> <span data-ttu-id="ee3e8-171">Bağlı hizmet sorunsuz dağıtıldıktan sonra **Taslak-1** penceresi artık görünmemelidir; soldaki ağaç görünümünde **AzureStorageLinkedService** görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-171">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

#### <a name="create-hdinsight-linked-service"></a><span data-ttu-id="ee3e8-172">Hdınsight bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee3e8-172">Create HDInsight linked service</span></span>
<span data-ttu-id="ee3e8-173">Bu adımda, Hdınsight Spark kümenizin data factory'ye bağlamak için Azure Hdınsight bağlı hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-173">In this step, you create Azure HDInsight linked service to link your HDInsight Spark cluster to the data factory.</span></span> <span data-ttu-id="ee3e8-174">Hdınsight kümesi, bu örnekteki ardışık Spark etkinliğinde belirtilen Spark programı çalıştırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-174">The HDInsight cluster is used to run the Spark program specified in the Spark activity of the pipeline in this sample.</span></span>  

1. <span data-ttu-id="ee3e8-175">Düğmeyi görmüyorsanız araç çubuğunda **... Daha fazla** araç çubuğunda tıklatın **yeni işlem**ve ardından **Hdınsight kümesi**.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-175">Click **... More** on the toolbar, click **New compute**, and then click **HDInsight cluster**.</span></span>

    ![Hdınsight bağlı hizmeti oluşturma](media/data-factory-spark/new-hdinsight-linked-service.png)
2. <span data-ttu-id="ee3e8-177">Aşağıdaki kod parçacığını kopyalayıp **Taslak-1** penceresine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-177">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="ee3e8-178">JSON Düzenleyicisi'nde, aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="ee3e8-178">In the JSON editor, do the following steps:</span></span>
    1. <span data-ttu-id="ee3e8-179">Belirtin **URI** Hdınsight Spark kümesi için.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-179">Specify the **URI** for the HDInsight Spark cluster.</span></span> <span data-ttu-id="ee3e8-180">Örneğin: `https://<sparkclustername>.azurehdinsight.net/`.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-180">For example: `https://<sparkclustername>.azurehdinsight.net/`.</span></span>
    2. <span data-ttu-id="ee3e8-181">Adını belirtin **kullanıcı** Spark küme erişimine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-181">Specify the name of the **user** who has access to the Spark cluster.</span></span>
    3. <span data-ttu-id="ee3e8-182">Belirtin **parola** kullanıcı için.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-182">Specify the **password** for user.</span></span>
    4. <span data-ttu-id="ee3e8-183">Belirtin **Azure depolama bağlantılı hizmeti** Hdınsight Spark kümesi ile ilişkili.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-183">Specify the **Azure Storage linked service** that is associated with the HDInsight Spark cluster.</span></span> <span data-ttu-id="ee3e8-184">Bu örnek,: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-184">In this example, it is: **AzureStorageLinkedService**.</span></span>

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
    > - <span data-ttu-id="ee3e8-185">Spark etkinliği Azure Data Lake Store birincil depolama alanı olarak kullanın Hdınsight Spark kümeleri desteklemez.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-185">Spark Activity does not support HDInsight Spark clusters that use an Azure Data Lake Store as primary storage.</span></span>
    > - <span data-ttu-id="ee3e8-186">Yalnızca (kendi) Hdınsight Spark kümesinde varolan Spark etkinlik destekler.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-186">Spark Activity supports only existing (your own) HDInsight Spark cluster.</span></span> <span data-ttu-id="ee3e8-187">Bir isteğe bağlı Hdınsight bağlı hizmeti desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-187">It does not support an on-demand HDInsight linked service.</span></span>

    <span data-ttu-id="ee3e8-188">Bkz: [Hdınsight bağlı hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) Hdınsight hakkında ayrıntılı bilgi için bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-188">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details about the HDInsight linked service.</span></span>
3.  <span data-ttu-id="ee3e8-189">Bağlantılı hizmet dağıtmak için **dağıtma** komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-189">To deploy the linked service, click **Deploy** on the command bar.</span></span>  

### <a name="create-output-dataset"></a><span data-ttu-id="ee3e8-190">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee3e8-190">Create output dataset</span></span>
<span data-ttu-id="ee3e8-191">Çıktı veri kümesi ne zamanlama (saatlik, günlük, vs.) sürücüleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-191">The output dataset is what drives the schedule (hourly, daily, etc.).</span></span> <span data-ttu-id="ee3e8-192">Bu nedenle, etkinlik gerçekten herhangi bir çıktı üretmez olsa da ardışık düzeninde bir çıkış veri kümesi için spark etkinlik belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-192">Therefore, you must specify an output dataset for the spark activity in the pipeline even though the activity does not really produce any output.</span></span> <span data-ttu-id="ee3e8-193">Bir giriş veri kümesi etkinliğin belirlenmesi isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-193">Specifying an input dataset for the activity is optional.</span></span>

1. <span data-ttu-id="ee3e8-194">**Data Factory Düzenleyicisi**’nde komut çubuğundaki **... Diğer**, **Yeni veri kümesi** öğelerine tıklayın ve **Azure Blob depolama** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-194">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="ee3e8-195">Aşağıdaki kod parçacığını kopyalayıp Taslak-1 penceresine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-195">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="ee3e8-196">JSON parçacığı adlı veri kümesini tanımlamaktadır **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-196">The JSON snippet defines a dataset called **OutputDataset**.</span></span> <span data-ttu-id="ee3e8-197">Ayrıca, sonuçlar adlı blob kapsayıcısında depolanır belirttiğiniz **adfspark** ve adlı klasörde **pyFiles/çıkış**.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-197">In addition, you specify that the results are stored in the blob container called **adfspark** and the folder called **pyFiles/output**.</span></span> <span data-ttu-id="ee3e8-198">Daha önce belirtildiği gibi bu veri kümesi kukla bir veri kümesi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-198">As mentioned earlier, this dataset is a dummy dataset.</span></span> <span data-ttu-id="ee3e8-199">Bu örnekte Spark program herhangi bir çıktı üretmez.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-199">The Spark program in this example does not produce any output.</span></span> <span data-ttu-id="ee3e8-200">**Kullanılabilirlik** bölümü belirtiyor çıktı veri kümesi günlük üretilir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-200">The **availability** section specifies that the output dataset is produced daily.</span></span>  

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
3. <span data-ttu-id="ee3e8-201">Veri kümesi dağıtmak için **dağıtma** komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-201">To deploy the dataset, click **Deploy** on the command bar.</span></span>


### <a name="create-pipeline"></a><span data-ttu-id="ee3e8-202">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ee3e8-202">Create pipeline</span></span>
<span data-ttu-id="ee3e8-203">Bu adımda oluşturduğunuz sahip işlem hattı bir **HDInsightSpark** etkinlik.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-203">In this step, you create a pipeline with a **HDInsightSpark** activity.</span></span> <span data-ttu-id="ee3e8-204">Şu anda, çıktı veri kümesi zamanlamayı yönetendir; bu nedenle etkinlik hiçbir çıktı oluşturmasa bile sizin bir çıktı veri kümesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-204">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="ee3e8-205">Etkinlik herhangi bir girdi almazsa, girdi veri kümesi oluşturma işlemini atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-205">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="ee3e8-206">Bu nedenle, hiçbir girdi veri kümesi bu örnekte belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-206">Therefore, no input dataset is specified in this example.</span></span>

1. <span data-ttu-id="ee3e8-207">İçinde **Data Factory düzenleyici**, tıklatın **... Daha fazla** komut çubuğu ve ardından **yeni işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-207">In the **Data Factory Editor**, click **… More** on the command bar, and then click **New pipeline**.</span></span>
2. <span data-ttu-id="ee3e8-208">Taslak-1 penceresine betiği aşağıdaki kod ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="ee3e8-208">Replace the script in the Draft-1 window with the following script:</span></span>

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
    <span data-ttu-id="ee3e8-209">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="ee3e8-209">Note the following points:</span></span>
    - <span data-ttu-id="ee3e8-210">**Türü** özelliği ayarlanmış **HDInsightSpark**.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-210">The **type** property is set to **HDInsightSpark**.</span></span>
    - <span data-ttu-id="ee3e8-211">**RootPath** ayarlanır **adfspark\\pyFiles** burada adfspark, Azure Blob kapsayıcısında ve pyFiles kapsayıcıdaki ince klasördür.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-211">The **rootPath** is set to **adfspark\\pyFiles** where adfspark is the Azure Blob container and pyFiles is fine folder in that container.</span></span> <span data-ttu-id="ee3e8-212">Bu örnekte, Azure Blob Storage Spark kümesi ile ilişkili adrestir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-212">In this example, the Azure Blob Storage is the one that is associated with the Spark cluster.</span></span> <span data-ttu-id="ee3e8-213">Farklı bir Azure depolama dosyayı karşıya yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-213">You can upload the file to a different Azure Storage.</span></span> <span data-ttu-id="ee3e8-214">Bunu yaparsanız, bu depolama hesabı data factory'ye bağlamak için bir Azure depolama bağlantılı hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-214">If you do so, create an Azure Storage linked service to link that storage account to the data factory.</span></span> <span data-ttu-id="ee3e8-215">Ardından, bağlı hizmetin adı için bir değer olarak belirtin **sparkJobLinkedService** özelliği.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-215">Then, specify the name of the linked service as a value for the **sparkJobLinkedService** property.</span></span> <span data-ttu-id="ee3e8-216">Bkz: [Spark etkinlik özellikleri](#spark-activity-properties) bu özellik ve Spark etkinlik tarafından desteklenen diğer özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-216">See [Spark Activity properties](#spark-activity-properties) for details about this property and other properties supported by the Spark Activity.</span></span>  
    - <span data-ttu-id="ee3e8-217">**EntryFilePath** ayarlanır **test.py**, python dosyası değil.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-217">The **entryFilePath** is set to the **test.py**, which is the python file.</span></span>
    - <span data-ttu-id="ee3e8-218">**Getdebugınfo** özelliği ayarlanmış **her zaman**, günlük dosyaları her zaman anlamına gelir (başarılı veya başarısız) oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-218">The **getDebugInfo** property is set to **Always**, which means the log files are always generated (success or failure).</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="ee3e8-219">Bu özelliği ayarlamak değil, öneririz `Always` bir üretim ortamında bir sorunu gidermeye çalışıyor değilseniz.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-219">We recommend that you do not set this property to `Always` in a production environment unless you are troubleshooting an issue.</span></span>
    - <span data-ttu-id="ee3e8-220">**Çıkarır** bölümü bir çıkış veri kümesi yok.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-220">The **outputs** section has one output dataset.</span></span> <span data-ttu-id="ee3e8-221">Spark program herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-221">You must specify an output dataset even if the spark program does not produce any output.</span></span> <span data-ttu-id="ee3e8-222">Çıktı veri kümesi, ardışık düzen (saatlik, günlük, vs.) için zamanlamayı sürücüleri.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-222">The output dataset drives the schedule for the pipeline (hourly, daily, etc.).</span></span>  

        <span data-ttu-id="ee3e8-223">Spark etkinliği tarafından desteklenen özellikler hakkında daha fazla ayrıntı için bkz: [Spark etkinlik özellikleri](#spark-activity-properties) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-223">For details about the properties supported by Spark activity, see [Spark activity properties](#spark-activity-properties) section.</span></span>
3. <span data-ttu-id="ee3e8-224">İşlem hattını dağıtmak için **dağıtma** komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-224">To deploy the pipeline, click **Deploy** on the command bar.</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="ee3e8-225">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="ee3e8-225">Monitor pipeline</span></span>
1. <span data-ttu-id="ee3e8-226">Tıklatın **X** Data Factory Düzenleyici dikey penceresini kapatmak ve Data Factory giriş sayfasına geri gidin.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-226">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory home page.</span></span> <span data-ttu-id="ee3e8-227">Tıklatın **izleme ve yönetme** başka bir sekmede izleme uygulamayı başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-227">Click **Monitor and Manage** to launch the monitoring application in another tab.</span></span>

    ![İzleme ve yönetme bölmesi](media/data-factory-spark/monitor-and-manage-tile.png)
2. <span data-ttu-id="ee3e8-229">Değişiklik **başlangıç zamanı** en üstte filtre **1/2/2017**, tıklatıp **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-229">Change the **Start time** filter at the top to **2/1/2017**, and click **Apply**.</span></span>
3. <span data-ttu-id="ee3e8-230">Yalnızca bir gününü (2017-02-01) başlangıç ve bitiş zamanları (2017-02-02) ardışık arasında olarak yalnızca bir etkinlik penceresini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-230">You should see only one activity window as there is only one day between the start (2017-02-01) and end times (2017-02-02) of the pipeline.</span></span> <span data-ttu-id="ee3e8-231">Veri dilimi olduğunu onaylayın **hazır** durumu.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-231">Confirm that the data slice is in **ready** state.</span></span>

    ![İşlem hattını izleme](media/data-factory-spark/monitor-and-manage-app.png)    
4. <span data-ttu-id="ee3e8-233">Seçin **etkinlik penceresini** Çalıştır etkinliği hakkındaki ayrıntıları görmek için.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-233">Select the **activity window** to see details about the activity run.</span></span> <span data-ttu-id="ee3e8-234">Bir hata varsa, sağ bölmede hakkındaki ayrıntıları bakın.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-234">If there is an error, you see details about it in the right pane.</span></span>

### <a name="verify-the-results"></a><span data-ttu-id="ee3e8-235">Sonuçları doğrulayın</span><span class="sxs-lookup"><span data-stu-id="ee3e8-235">Verify the results</span></span>

1. <span data-ttu-id="ee3e8-236">Başlatma **Jupyter not defteri** giderek Hdınsight Spark kümenizin: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-236">Launch **Jupyter notebook** for your HDInsight Spark cluster by navigating to: https://CLUSTERNAME.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="ee3e8-237">Ayrıca, Hdınsight Spark kümeniz için küme Panosu başlatın ve sonra başlatın **Jupyter not defteri**.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-237">You can also launch cluster dashboard for your HDInsight Spark cluster, and then launch **Jupyter Notebook**.</span></span>
2. <span data-ttu-id="ee3e8-238">Tıklatın **yeni** -> **PySpark** yeni bir not defteri başlatmak için.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-238">Click **New** -> **PySpark** to start a new notebook.</span></span>

    ![Yeni Jupyter not defteri](media/data-factory-spark/jupyter-new-book.png)
3. <span data-ttu-id="ee3e8-240">Metin kopyalama/yapıştırma ve tuşuna basarak aşağıdaki komutu çalıştırın **SHIFT + ENTER** ikinci ifade sonunda.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-240">Run the following command by copy/pasting the text and pressing **SHIFT + ENTER** at the end of the second statement.</span></span>  

    ```sql
    %%sql

    SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"
    ```
4. <span data-ttu-id="ee3e8-241">Hvac tablodan veri gördüğünüzü onaylayın:</span><span class="sxs-lookup"><span data-stu-id="ee3e8-241">Confirm that you see the data from the hvac table:</span></span>  

    ![Jupyter sorgu sonuçları](media/data-factory-spark/jupyter-notebook-results.png)

<span data-ttu-id="ee3e8-243">Bkz: [bir Spark SQL sorgusu çalıştırmanız](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) bölüm ayrıntılı yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-243">See [Run a Spark SQL query](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md#run-a-hive-query-using-spark-sql) section for detailed instructions.</span></span> 

### <a name="troubleshooting"></a><span data-ttu-id="ee3e8-244">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ee3e8-244">Troubleshooting</span></span>
<span data-ttu-id="ee3e8-245">Ayarladığınız bu yana **Getdebugınfo** için **her zaman**, gördüğünüz bir **günlük** alt klasöründe **pyFiles** klasörü, Azure Blob kapsayıcısında.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-245">Since you set **getDebugInfo** to **Always**, you see a **log** subfolder in the **pyFiles** folder in your Azure Blob container.</span></span> <span data-ttu-id="ee3e8-246">Günlük dosyası günlük klasöründeki ek ayrıntılar sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-246">The log file in the log folder provides additional details.</span></span> <span data-ttu-id="ee3e8-247">Bu günlük dosyası bir hata olduğunda özellikle yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-247">This log file is especially useful when there is an error.</span></span> <span data-ttu-id="ee3e8-248">Bir üretim ortamında ayarlamak isteyebilirsiniz **hatası**.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-248">In a production environment, you may want to set it to **Failure**.</span></span>

<span data-ttu-id="ee3e8-249">Daha fazla sorun giderme için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="ee3e8-249">For further troubleshooting, do the following steps:</span></span>


1. <span data-ttu-id="ee3e8-250">Gidin `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-250">Navigate to `https://<CLUSTERNAME>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

    ![YARN kullanıcı arabirimini uygulama](media/data-factory-spark/yarnui-application.png)  
2. <span data-ttu-id="ee3e8-252">Tıklatın **günlükleri** Çalıştır biri için çalışır.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-252">Click **Logs** for one of the run attempts.</span></span>

    ![Uygulama sayfası](media/data-factory-spark/yarn-applications.png)
3. <span data-ttu-id="ee3e8-254">Günlük sayfasındaki ek hata bilgileri görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-254">You should see additional error information in the log page.</span></span>

    ![Günlük hatası](media/data-factory-spark/yarnui-application-error.png)

<span data-ttu-id="ee3e8-256">Aşağıdaki bölümlerde, veri fabrikası Apache Spark kümesi ve Spark etkinliği kullanmak için Data Factory varlıklarını hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-256">The following sections provide information about Data Factory entities to use Apache Spark cluster and Spark Activity in your data factory.</span></span>

## <a name="spark-activity-properties"></a><span data-ttu-id="ee3e8-257">Spark etkinlik özellikleri</span><span class="sxs-lookup"><span data-stu-id="ee3e8-257">Spark activity properties</span></span>
<span data-ttu-id="ee3e8-258">Spark etkinliği ile işlem hattı örnek JSON tanımını şöyledir:</span><span class="sxs-lookup"><span data-stu-id="ee3e8-258">Here is the sample JSON definition of a pipeline with Spark Activity:</span></span>    

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
                "description": "This activity invokes the Spark program",
                "linkedServiceName": "HDInsightLinkedService"
            }
        ],
        "start": "2017-02-01T00:00:00Z",
        "end": "2017-02-02T00:00:00Z"
    }
}
```

<span data-ttu-id="ee3e8-259">Aşağıdaki tabloda JSON tanımında kullanılan JSON özellikleri açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="ee3e8-259">The following table describes the JSON properties used in the JSON definition:</span></span>

| <span data-ttu-id="ee3e8-260">Özellik</span><span class="sxs-lookup"><span data-stu-id="ee3e8-260">Property</span></span> | <span data-ttu-id="ee3e8-261">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee3e8-261">Description</span></span> | <span data-ttu-id="ee3e8-262">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ee3e8-262">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="ee3e8-263">ad</span><span class="sxs-lookup"><span data-stu-id="ee3e8-263">name</span></span> | <span data-ttu-id="ee3e8-264">İşlem hattında etkinlik adı.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-264">Name of the activity in the pipeline.</span></span> | <span data-ttu-id="ee3e8-265">Evet</span><span class="sxs-lookup"><span data-stu-id="ee3e8-265">Yes</span></span> |
| <span data-ttu-id="ee3e8-266">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee3e8-266">description</span></span> | <span data-ttu-id="ee3e8-267">Etkinlik yaptığı açıklayan metin.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-267">Text describing what the activity does.</span></span> | <span data-ttu-id="ee3e8-268">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee3e8-268">No</span></span> |
| <span data-ttu-id="ee3e8-269">type</span><span class="sxs-lookup"><span data-stu-id="ee3e8-269">type</span></span> | <span data-ttu-id="ee3e8-270">Bu özellik için HDInsightSpark ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-270">This property must be set to HDInsightSpark.</span></span> | <span data-ttu-id="ee3e8-271">Evet</span><span class="sxs-lookup"><span data-stu-id="ee3e8-271">Yes</span></span> |
| <span data-ttu-id="ee3e8-272">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="ee3e8-272">linkedServiceName</span></span> | <span data-ttu-id="ee3e8-273">Spark programın çalıştığı Hdınsight bağlı hizmetin adı.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-273">Name of the HDInsight linked service on which the Spark program runs.</span></span> | <span data-ttu-id="ee3e8-274">Evet</span><span class="sxs-lookup"><span data-stu-id="ee3e8-274">Yes</span></span> |
| <span data-ttu-id="ee3e8-275">rootPath</span><span class="sxs-lookup"><span data-stu-id="ee3e8-275">rootPath</span></span> | <span data-ttu-id="ee3e8-276">Azure Blob kapsayıcısı ve Spark dosyasını içeren klasör.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-276">The Azure Blob container and folder that contains the Spark file.</span></span> <span data-ttu-id="ee3e8-277">Dosya adı büyük/küçük harf duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-277">The file name is case-sensitive.</span></span> | <span data-ttu-id="ee3e8-278">Evet</span><span class="sxs-lookup"><span data-stu-id="ee3e8-278">Yes</span></span> |
| <span data-ttu-id="ee3e8-279">entryFilePath</span><span class="sxs-lookup"><span data-stu-id="ee3e8-279">entryFilePath</span></span> | <span data-ttu-id="ee3e8-280">Spark kod/paketi kök klasörüne göreli yolu.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-280">Relative path to the root folder of the Spark code/package.</span></span> | <span data-ttu-id="ee3e8-281">Evet</span><span class="sxs-lookup"><span data-stu-id="ee3e8-281">Yes</span></span> |
| <span data-ttu-id="ee3e8-282">className</span><span class="sxs-lookup"><span data-stu-id="ee3e8-282">className</span></span> | <span data-ttu-id="ee3e8-283">Uygulamanın Java/Spark ana sınıfı</span><span class="sxs-lookup"><span data-stu-id="ee3e8-283">Application's Java/Spark main class</span></span> | <span data-ttu-id="ee3e8-284">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee3e8-284">No</span></span> |
| <span data-ttu-id="ee3e8-285">Bağımsız değişkenler</span><span class="sxs-lookup"><span data-stu-id="ee3e8-285">arguments</span></span> | <span data-ttu-id="ee3e8-286">Spark programın komut satırı bağımsız değişkenleri listesi.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-286">A list of command-line arguments to the Spark program.</span></span> | <span data-ttu-id="ee3e8-287">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee3e8-287">No</span></span> |
| <span data-ttu-id="ee3e8-288">proxyUser</span><span class="sxs-lookup"><span data-stu-id="ee3e8-288">proxyUser</span></span> | <span data-ttu-id="ee3e8-289">Spark program yürütülmeye kimliğine bürünmek için kullanıcı hesabı</span><span class="sxs-lookup"><span data-stu-id="ee3e8-289">The user account to impersonate to execute the Spark program</span></span> | <span data-ttu-id="ee3e8-290">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee3e8-290">No</span></span> |
| <span data-ttu-id="ee3e8-291">sparkConfig</span><span class="sxs-lookup"><span data-stu-id="ee3e8-291">sparkConfig</span></span> | <span data-ttu-id="ee3e8-292">Konu başlığı altında listelenen Spark yapılandırma özellikleri için değerleri belirtin: [Spark yapılandırması - uygulama özellikleri](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span><span class="sxs-lookup"><span data-stu-id="ee3e8-292">Specify values for Spark configuration properties listed in the topic: [Spark Configuration - Application properties](https://spark.apache.org/docs/latest/configuration.html#available-properties).</span></span> | <span data-ttu-id="ee3e8-293">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee3e8-293">No</span></span> |
| <span data-ttu-id="ee3e8-294">Getdebugınfo</span><span class="sxs-lookup"><span data-stu-id="ee3e8-294">getDebugInfo</span></span> | <span data-ttu-id="ee3e8-295">Hdınsight küme tarafından kullanılan Azure depolama Spark günlük dosyalarının ne zaman kopyalanır belirtir (veya) sparkJobLinkedService tarafından belirtilen.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-295">Specifies when the Spark log files are copied to the Azure storage used by HDInsight cluster (or) specified by sparkJobLinkedService.</span></span> <span data-ttu-id="ee3e8-296">İzin verilen değerler: None, her zaman veya hata.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-296">Allowed values: None, Always, or Failure.</span></span> <span data-ttu-id="ee3e8-297">Varsayılan değer: yok.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-297">Default value: None.</span></span> | <span data-ttu-id="ee3e8-298">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee3e8-298">No</span></span> |
| <span data-ttu-id="ee3e8-299">sparkJobLinkedService</span><span class="sxs-lookup"><span data-stu-id="ee3e8-299">sparkJobLinkedService</span></span> | <span data-ttu-id="ee3e8-300">Azure Storage bağlı Spark iş dosyası, bağımlılıklar ve günlükleri tutan hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-300">The Azure Storage linked service that holds the Spark job file, dependencies, and logs.</span></span>  <span data-ttu-id="ee3e8-301">Bu özellik için bir değer belirtmezseniz, Hdınsight kümesi ile ilişkili depolama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-301">If you do not specify a value for this property, the storage associated with HDInsight cluster is used.</span></span> | <span data-ttu-id="ee3e8-302">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee3e8-302">No</span></span> |

## <a name="folder-structure"></a><span data-ttu-id="ee3e8-303">Klasör yapısı</span><span class="sxs-lookup"><span data-stu-id="ee3e8-303">Folder structure</span></span>
<span data-ttu-id="ee3e8-304">Spark etkinliği bir satır içi komut dosyası Pig olarak desteklemez ve Hive etkinlikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-304">The Spark activity does not support an in-line script as Pig and Hive activities do.</span></span> <span data-ttu-id="ee3e8-305">Spark işleri de Pig/Hive işleri daha fazla genişletilebilir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-305">Spark jobs are also more extensible than Pig/Hive jobs.</span></span> <span data-ttu-id="ee3e8-306">Spark işleri, birden çok bağımlılıkları gibi sağlayabilirsiniz jar (java sınıf yerleştirilen) paketleri, python dosyaları (PYTHONPATH yerleştirilmiş) ve diğer dosyaları.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-306">For Spark jobs, you can provide multiple dependencies such as jar packages (placed in the java CLASSPATH), python files (placed on the PYTHONPATH), and any other files.</span></span>

<span data-ttu-id="ee3e8-307">Hdınsight bağlı hizmeti tarafından başvurulan Azure Blob Depolama alanında aşağıdaki klasör yapısını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-307">Create the following folder structure in the Azure Blob storage referenced by the HDInsight linked service.</span></span> <span data-ttu-id="ee3e8-308">Ardından, bağımlı dosyaları tarafından temsil edilen kök klasöründe uygun alt klasörlerdeki karşıya **entryFilePath**.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-308">Then, upload dependent files to the appropriate sub folders in the root folder represented by **entryFilePath**.</span></span> <span data-ttu-id="ee3e8-309">Örneğin, python dosyalarını pyFiles alt klasöre ve jar dosyalarını kök klasörünün Kavanoz alt karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-309">For example, upload python files to the pyFiles subfolder and jar files to the jars subfolder of the root folder.</span></span> <span data-ttu-id="ee3e8-310">Çalışma zamanında Data Factory hizmeti Azure Blob depolama alanına aşağıdaki klasör yapısını bekler:</span><span class="sxs-lookup"><span data-stu-id="ee3e8-310">At runtime, Data Factory service expects the following folder structure in the Azure Blob storage:</span></span>     

| <span data-ttu-id="ee3e8-311">Yol</span><span class="sxs-lookup"><span data-stu-id="ee3e8-311">Path</span></span> | <span data-ttu-id="ee3e8-312">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ee3e8-312">Description</span></span> | <span data-ttu-id="ee3e8-313">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ee3e8-313">Required</span></span> | <span data-ttu-id="ee3e8-314">Tür</span><span class="sxs-lookup"><span data-stu-id="ee3e8-314">Type</span></span> |
| ---- | ----------- | -------- | ---- |
| <span data-ttu-id="ee3e8-315">.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-315">.</span></span> | <span data-ttu-id="ee3e8-316">Depolama bağlantılı hizmeti Spark işinde kök yolu</span><span class="sxs-lookup"><span data-stu-id="ee3e8-316">The root path of the Spark job in the storage linked service</span></span>  | <span data-ttu-id="ee3e8-317">Evet</span><span class="sxs-lookup"><span data-stu-id="ee3e8-317">Yes</span></span> | <span data-ttu-id="ee3e8-318">Klasör</span><span class="sxs-lookup"><span data-stu-id="ee3e8-318">Folder</span></span> |
| <span data-ttu-id="ee3e8-319">&lt;Kullanıcı tanımlı&gt;</span><span class="sxs-lookup"><span data-stu-id="ee3e8-319">&lt;user defined &gt;</span></span> | <span data-ttu-id="ee3e8-320">Spark iş girişi dosyasına işaret eden yolu</span><span class="sxs-lookup"><span data-stu-id="ee3e8-320">The path pointing to the entry file of the Spark job</span></span> | <span data-ttu-id="ee3e8-321">Evet</span><span class="sxs-lookup"><span data-stu-id="ee3e8-321">Yes</span></span> | <span data-ttu-id="ee3e8-322">Dosya</span><span class="sxs-lookup"><span data-stu-id="ee3e8-322">File</span></span> |
| <span data-ttu-id="ee3e8-323">. / jar'lar</span><span class="sxs-lookup"><span data-stu-id="ee3e8-323">./jars</span></span> | <span data-ttu-id="ee3e8-324">Bu klasörü altındaki tüm dosyaları karşıya ve küme java sınıf yolu yerleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="ee3e8-324">All files under this folder are uploaded and placed on the java classpath of the cluster</span></span> | <span data-ttu-id="ee3e8-325">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee3e8-325">No</span></span> | <span data-ttu-id="ee3e8-326">Klasör</span><span class="sxs-lookup"><span data-stu-id="ee3e8-326">Folder</span></span> |
| <span data-ttu-id="ee3e8-327">. / pyFiles</span><span class="sxs-lookup"><span data-stu-id="ee3e8-327">./pyFiles</span></span> | <span data-ttu-id="ee3e8-328">Bu klasörü altındaki tüm dosyaları karşıya ve küme PYTHONPATH yerleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="ee3e8-328">All files under this folder are uploaded and placed on the PYTHONPATH of the cluster</span></span> | <span data-ttu-id="ee3e8-329">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee3e8-329">No</span></span> | <span data-ttu-id="ee3e8-330">Klasör</span><span class="sxs-lookup"><span data-stu-id="ee3e8-330">Folder</span></span> |
| <span data-ttu-id="ee3e8-331">. / dosyaları</span><span class="sxs-lookup"><span data-stu-id="ee3e8-331">./files</span></span> | <span data-ttu-id="ee3e8-332">Bu klasörü altındaki tüm dosyaları karşıya ve yürütücü çalışma dizini yerleştirilmiş</span><span class="sxs-lookup"><span data-stu-id="ee3e8-332">All files under this folder are uploaded and placed on executor working directory</span></span> | <span data-ttu-id="ee3e8-333">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee3e8-333">No</span></span> | <span data-ttu-id="ee3e8-334">Klasör</span><span class="sxs-lookup"><span data-stu-id="ee3e8-334">Folder</span></span> |
| <span data-ttu-id="ee3e8-335">. / arşivler</span><span class="sxs-lookup"><span data-stu-id="ee3e8-335">./archives</span></span> | <span data-ttu-id="ee3e8-336">Bu klasörü altındaki tüm dosyaları sıkıştırılmamış</span><span class="sxs-lookup"><span data-stu-id="ee3e8-336">All files under this folder are uncompressed</span></span> | <span data-ttu-id="ee3e8-337">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee3e8-337">No</span></span> | <span data-ttu-id="ee3e8-338">Klasör</span><span class="sxs-lookup"><span data-stu-id="ee3e8-338">Folder</span></span> |
| <span data-ttu-id="ee3e8-339">. / günlükleri</span><span class="sxs-lookup"><span data-stu-id="ee3e8-339">./logs</span></span> | <span data-ttu-id="ee3e8-340">Spark kümesi günlüklerinden depolandığı klasörü.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-340">The folder where logs from the Spark cluster are stored.</span></span>| <span data-ttu-id="ee3e8-341">Hayır</span><span class="sxs-lookup"><span data-stu-id="ee3e8-341">No</span></span> | <span data-ttu-id="ee3e8-342">Klasör</span><span class="sxs-lookup"><span data-stu-id="ee3e8-342">Folder</span></span> |

<span data-ttu-id="ee3e8-343">Burada, Azure Blob Depolama Hdınsight bağlı hizmeti tarafından başvurulan iki Spark iş dosyalarını içeren bir depolama alanı için bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ee3e8-343">Here is an example for a storage containing two Spark job files in the Azure Blob Storage referenced by the HDInsight linked service.</span></span>

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
