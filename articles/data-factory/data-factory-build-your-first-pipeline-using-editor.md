---
title: "İlk data factory’nizi derleme (Azure portalı) | Microsoft Belgeleri"
description: "Bu öğreticide, Azure Portal'daki Data Factory Düzenleyiciyi kullanarak örnek bir Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d5b14e9e-e358-45be-943c-5297435d402d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 9c958aecb841fa02349c6b9e5e1984f6ba4fb611
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="b920f-103">Öğretici: Azure portal kullanarak ilk Azure data factory’nizi derleme</span><span class="sxs-lookup"><span data-stu-id="b920f-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b920f-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="b920f-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="b920f-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="b920f-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="b920f-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b920f-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="b920f-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b920f-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="b920f-108">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="b920f-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="b920f-109">REST API</span><span class="sxs-lookup"><span data-stu-id="b920f-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="b920f-110">Bu makalede, ilk Azure veri fabrikanızı oluşturmak için [Azure portalını](https://portal.azure.com/) nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="b920f-110">In this article, you learn how to use [Azure portal](https://portal.azure.com/) to create your first Azure data factory.</span></span> <span data-ttu-id="b920f-111">Diğer araçları/SDK’ları kullanarak öğreticiyi uygulamak için açılır listedeki seçeneklerden birini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="b920f-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span> 

<span data-ttu-id="b920f-112">Bu öğreticideki işlem hattı bir etkinlik içerir: **HDInsight Hive etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="b920f-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="b920f-113">Bu etkinlik, Azure HDInsight kümesi üzerinde çıkış verileri üretmek üzere giriş verilerini dönüştüren bir hive betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="b920f-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="b920f-114">İşlem hattı, belirtilen başlangıç ve bitiş saatleri arasında ayda bir kez çalışacak şekilde zamanlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b920f-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="b920f-115">Bu öğreticideki veri işlem hattı, çıkış verileri üretmek üzere giriş verilerini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="b920f-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="b920f-116">Azure Data Factory kullanarak verileri kopyalama öğreticisi için bkz. [Öğretici: Blob Depolama’dan SQL Veritabanı’na veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b920f-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="b920f-117">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="b920f-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="b920f-118">Bir etkinliğin çıkış veri kümesini diğer etkinliğin giriş veri kümesi olarak ayarlayarak iki etkinliği zincirleyebilir, yani bir etkinliğin diğerinden sonra çalıştırılmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b920f-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="b920f-119">Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="b920f-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b920f-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b920f-120">Prerequisites</span></span>
1. <span data-ttu-id="b920f-121">[Öğreticiye Genel Bakış](data-factory-build-your-first-pipeline.md) makalesinin tamamını okuyun ve **ön koşul** adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
2. <span data-ttu-id="b920f-122">Bu makale, Azure Data Factory hizmetine kavramsal bir genel bakış sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="b920f-122">This article does not provide a conceptual overview of the Azure Data Factory service.</span></span> <span data-ttu-id="b920f-123">Hizmet hakkında ayrıntılı bir genel bakış için [Azure Data Factory'ye giriş](data-factory-introduction.md) makalesine gitmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="b920f-123">We recommend that you go through [Introduction to Azure Data Factory](data-factory-introduction.md) article for a detailed overview of the service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="b920f-124">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="b920f-124">Create data factory</span></span>
<span data-ttu-id="b920f-125">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="b920f-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="b920f-126">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="b920f-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="b920f-127">Örneğin, verileri bir kaynaktan bir hedef veri deposuna kopyalamak için Kopyalama Etkinliği, giriş verilerini ürün çıkış verilerine dönüştürecek Hive betiğini çalıştırmak için de HDInsight Hive etkinliği.</span><span class="sxs-lookup"><span data-stu-id="b920f-127">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="b920f-128">Bu adımda data factory oluşturmayla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="b920f-128">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="b920f-129">[Azure Portal](https://portal.azure.com/)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b920f-129">Log in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="b920f-130">Soldaki menüde **YENİ**, **Veri + Analiz** ve **Data Factory** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-130">Click **NEW** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Dikey pencere oluşturma](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="b920f-132">**Yeni data factory** dikey penceresinde, Ad olarak **GetStartedDF** girin.</span><span class="sxs-lookup"><span data-stu-id="b920f-132">In the **New data factory** blade, enter **GetStartedDF** for the Name.</span></span>

   ![Yeni veri fabrikası dikey penceresi](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="b920f-134">Azure data factory adı **küresel olarak benzersiz** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b920f-134">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="b920f-135">**Veri fabrikası adı "GetStartedDF" kullanılamıyor** hatasını alırsanız.</span><span class="sxs-lookup"><span data-stu-id="b920f-135">If you receive the error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="b920f-136">Veri fabrikasının adını (örneğin adınızBaşlarkenVF) değiştirin ve yeniden oluşturmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="b920f-136">Change the name of the data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="b920f-137">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="b920f-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="b920f-138">Data factory adı gelecekte bir **DNS** adı olarak kaydedilmiş olabilir; bu nedenle herkese görünür hale gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="b920f-138">The name of the data factory may be registered as a **DNS** name in the future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="b920f-139">Data factory’yi oluşturmak istediğiniz **Azure aboneliği**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="b920f-139">Select the **Azure subscription** where you want the data factory to be created.</span></span>
5. <span data-ttu-id="b920f-140">Mevcut bir **kaynak grubu** seçin ya da bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b920f-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="b920f-141">Öğreticide kullanmak için şu adla bir kaynak grubu oluşturun: **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="b920f-141">For the tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="b920f-142">Data factory için **konum** seçin.</span><span class="sxs-lookup"><span data-stu-id="b920f-142">Select the **location** for the data factory.</span></span> <span data-ttu-id="b920f-143">Açılır listede yalnızca Data Factory hizmeti tarafından desteklenen bölgeler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b920f-143">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
7. <span data-ttu-id="b920f-144">**Panoya sabitle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b920f-144">Select **Pin to dashboard**.</span></span> 
8. <span data-ttu-id="b920f-145">**Yeni data factory** dikey penceresinde **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-145">Click **Create** on the **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b920f-146">Data Factory örnekleri oluşturmak için abonelik/kaynak grubu düzeyinde [Data Factory Katılımcısı](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rolünün üyesi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b920f-146">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="b920f-147">Panoda, şu duruma sahip aşağıdaki kutucuğu görürsünüz: Veri fabrikası dağıtılıyor.</span><span class="sxs-lookup"><span data-stu-id="b920f-147">On the dashboard, you see the following tile with status: Deploying data factory.</span></span>    

   ![Data factory durumu oluşturma](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="b920f-149">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="b920f-149">Congratulations!</span></span> <span data-ttu-id="b920f-150">İlk data factory’nizi başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="b920f-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="b920f-151">Data factory sorunsuz oluşturulduktan sonra data factory sayfasını görürsünüz, burada size data factory içeriği gösterilir.</span><span class="sxs-lookup"><span data-stu-id="b920f-151">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>     

    ![Data Factory dikey penceresi](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="b920f-153">Data factory içinde bir işlem hattı oluşturmadan önce birkaç Data Factory varlığı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b920f-153">Before creating a pipeline in the data factory, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="b920f-154">Önce veri depolarını/işlemleri veri deponuza bağlamak için bağlı hizmetler oluşturun, bağlı veri depolarında giriş/çıkış verilerini temsil etmek üzere giriş ve çıkış veri kümeleri tanımlayın, sonra da bu veri kümelerini kullanan bir etkinlikle işlem hattını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b920f-154">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="b920f-155">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="b920f-155">Create linked services</span></span>
<span data-ttu-id="b920f-156">Bu adımda, Azure Depolama hesabınızı ve isteğe bağlı Azure HDInsight kümesini data factory’nize bağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="b920f-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="b920f-157">Azure Depolama hesabı, bu örnekteki işlem hattı için girdi ve çıktı verilerini tutar.</span><span class="sxs-lookup"><span data-stu-id="b920f-157">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="b920f-158">HDInsight bağlı hizmeti, bu örnekteki işlem hattının etkinliğinde belirtilen Hive betiğini çalıştırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b920f-158">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="b920f-159">Senaryonuzda hangi [veri deposu](data-factory-data-movement-activities.md)/[işlem hizmetlerinin](data-factory-compute-linked-services.md) kullanılacağını belirleyin ve bağlı hizmetler oluşturarak bu hizmetleri data factory’ye bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services to the data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="b920f-160">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="b920f-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="b920f-161">Bu adımda, Azure Depolama hesabınızı veri fabrikanıza bağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="b920f-161">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="b920f-162">Bu öğreticide, giriş/çıkış verilerini ve HQL betik dosyasını depolamak için aynı Azure Depolama hesabını kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="b920f-162">In this tutorial, you use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="b920f-163">**GetStartedDF** için **DATA FACTORY** dikey penceresinde **Geliştir ve dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-163">Click **Author and deploy** on the **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="b920f-164">Data Factory Düzenleyicisi’ni görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b920f-164">You should see the Data Factory Editor.</span></span>

   ![Geliştir ve dağıt kutucuğu](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="b920f-166">**Yeni data store**’a tıklayın ve **Azure depolama**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="b920f-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Yeni veri deposu - Azure Depolama - menü](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="b920f-168">Düzenleyicide Azure Storage bağlı hizmeti oluşturmak için JSON betiğini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b920f-168">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![Azure Storage bağlı hizmeti](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="b920f-170">**accountname** sözcüğünü Azure depolama hesabınızın adıyla, **accountkey** sözcüğünü de Azure depolama hesabının erişim anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b920f-170">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="b920f-171">Depolama erişim anahtarınızı nasıl alabileceğinizi öğrenmek için [Depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account) sayfasındaki depolama erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma bilgilerine bakın.</span><span class="sxs-lookup"><span data-stu-id="b920f-171">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="b920f-172">Bağlı hizmeti dağıtmak için komut çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-172">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![Dağıt düğmesi](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="b920f-174">Bağlı hizmet sorunsuz dağıtıldıktan sonra **Taslak-1** penceresi artık görünmemelidir; soldaki ağaç görünümünde **AzureStorageLinkedService** görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b920f-174">After the linked service is deployed successfully, the **Draft-1** window should disappear and you see **AzureStorageLinkedService** in the tree view on the left.</span></span>

    ![Menüde Storage Bağlı Hizmeti](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="b920f-176">Azure HDInsight bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="b920f-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="b920f-177">Bu adımda, isteğe bağlı HDInsight kümesini data factory’nize bağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="b920f-177">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="b920f-178">HDInsight kümesi çalışma zamanında otomatik olarak oluşturulur ve işlenmesi bittiğinde ve belirtilen sürede boşta kalırsa silinir.</span><span class="sxs-lookup"><span data-stu-id="b920f-178">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span>

1. <span data-ttu-id="b920f-179">**Data Factory Düzenleyicisi**’nde komut çubuğundaki **... Diğer**, **Yeni işlem** öğelerine tıklayın ve **İsteğe bağlı HDInsight kümesi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="b920f-179">In the **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Yeni işlem](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="b920f-181">Aşağıdaki kod parçacığını kopyalayıp **Taslak-1** penceresine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b920f-181">Copy and paste the following snippet to the **Draft-1** window.</span></span> <span data-ttu-id="b920f-182">JSON parçacığı, istek üzerine HDInsight kümesi oluşturmak için kullanılan özellikleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="b920f-182">The JSON snippet describes the properties that are used to create the HDInsight cluster on-demand.</span></span>

    ```JSON
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService"
            }
        }
    }
    ```

    <span data-ttu-id="b920f-183">Aşağıdaki tabloda, kod parçacığında kullanılan JSON özellikleri için açıklamalar verilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b920f-183">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="b920f-184">Özellik</span><span class="sxs-lookup"><span data-stu-id="b920f-184">Property</span></span> | <span data-ttu-id="b920f-185">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b920f-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b920f-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="b920f-186">ClusterSize</span></span> |<span data-ttu-id="b920f-187">HDInsight kümesi boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="b920f-187">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="b920f-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="b920f-188">TimeToLive</span></span> | <span data-ttu-id="b920f-189">Silinmeden önce HDInsight kümesinin boşta kalma süresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b920f-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="b920f-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="b920f-190">linkedServiceName</span></span> | <span data-ttu-id="b920f-191">HDInsight tarafından oluşturulan günlükleri depolamak için kullanılan depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="b920f-191">Specifies the storage account that is used to store the logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="b920f-192">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="b920f-192">Note the following points:</span></span>

   * <span data-ttu-id="b920f-193">Data Factory, sizin için JSON ile **Linux tabanlı** bir HDInsight kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b920f-193">The Data Factory creates a **Linux-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="b920f-194">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="b920f-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="b920f-195">İsteğe bağlı HDInsight kümesi yerine **kendi HDInsight kümenizi** kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b920f-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="b920f-196">Ayrıntılar için bkz. [HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="b920f-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="b920f-197">HDInsight kümesi JSON’da belirttiğiniz blob depolamada (**linkedServiceName**) bir **varsayılan kapsayıcı** oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b920f-197">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="b920f-198">HDInsight, küme silindiğinde bu kapsayıcıyı silmez.</span><span class="sxs-lookup"><span data-stu-id="b920f-198">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="b920f-199">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="b920f-199">This behavior is by design.</span></span> <span data-ttu-id="b920f-200">İsteğe bağlı HDInsight bağlı hizmeti kullanıldığında, mevcut canlı bir küme olmadığı sürece bir dilim her işlendiğinde bir HDInsight kümesi oluşturulur (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="b920f-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="b920f-201">Küme, işlem tamamlandığında otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="b920f-201">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="b920f-202">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b920f-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="b920f-203">İşlerin sorunları giderilmesi için bunlara gerek yoksa, depolama maliyetini azaltmak için bunları silmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b920f-203">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="b920f-204">Bu kapsayıcıların adları şu deseni izler: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="b920f-204">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="b920f-205">Azure blob depolamada kapsayıcı silmek için [Microsoft Storage Gezgini](http://storageexplorer.com/) gibi araçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="b920f-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="b920f-206">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="b920f-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="b920f-207">Bağlı hizmeti dağıtmak için komut çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-207">Click **Deploy** on the command bar to deploy the linked service.</span></span>

    ![İsteğe bağlı HDInsight bağlı hizmetini dağıtma](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="b920f-209">Hem **AzureStorageLinkedService**, hem de **HDInsightOnDemandLinkedService** öğesinin soldaki ağaç görünümünde olduğunu onaylayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in the tree view on the left.</span></span>

    ![Bağlı hizmetlerin bulunduğu ağaç görünümü](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="b920f-211">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="b920f-211">Create datasets</span></span>
<span data-ttu-id="b920f-212">Bu adımda, Hive işlenmesi için girdi ve çıktı verilerini temsil edecek veri kümeleri oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="b920f-212">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="b920f-213">Bu veri kümeleri, bu öğreticide daha önce oluşturduğunuz **AzureStorageLinkedService** öğesine başvurur.</span><span class="sxs-lookup"><span data-stu-id="b920f-213">These datasets refer to the **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="b920f-214">Bağlı hizmet Azure Storage hesabını belirtirken, veri kümeleri de girdi ve çıktı verilerini tutan depolama biriminde kapsayıcı, klasör, dosya adı belirtir.</span><span class="sxs-lookup"><span data-stu-id="b920f-214">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="b920f-215">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b920f-215">Create input dataset</span></span>
1. <span data-ttu-id="b920f-216">**Data Factory Düzenleyicisi**’nde komut çubuğundaki **... Diğer**, **Yeni veri kümesi** öğelerine tıklayın ve **Azure Blob depolama** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b920f-216">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Yeni veri kümesi](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="b920f-218">Aşağıdaki kod parçacığını kopyalayıp Taslak-1 penceresine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b920f-218">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="b920f-219">JSON parçacığında, işlem hattındaki etkinliğin girdi verilerini temsil eden **AzureBlobInput** adlı bir veri kümesi oluşturmaktasınız.</span><span class="sxs-lookup"><span data-stu-id="b920f-219">In the JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="b920f-220">Ek olarak, girdi verilerinin **adfgetstarted** adlı blob kapsayıcısında ve **inputdata** adlı klasörde bulunduğunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="b920f-220">In addition, you specify that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

    ```JSON
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "fileName": "input.log",
                "folderPath": "adfgetstarted/inputdata",
                "format": {
                    "type": "TextFormat",
                    "columnDelimiter": ","
                }
            },
            "availability": {
                "frequency": "Month",
                "interval": 1
            },
            "external": true,
            "policy": {}
        }
    }
    ```
    <span data-ttu-id="b920f-221">Aşağıdaki tabloda, kod parçacığında kullanılan JSON özellikleri için açıklamalar verilmektedir:</span><span class="sxs-lookup"><span data-stu-id="b920f-221">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="b920f-222">Özellik</span><span class="sxs-lookup"><span data-stu-id="b920f-222">Property</span></span> | <span data-ttu-id="b920f-223">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b920f-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="b920f-224">type</span><span class="sxs-lookup"><span data-stu-id="b920f-224">type</span></span> |<span data-ttu-id="b920f-225">Veriler Azure blob depolama alanında yer aldığından type özelliği **AzureBlob** olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="b920f-225">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="b920f-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="b920f-226">linkedServiceName</span></span> |<span data-ttu-id="b920f-227">Daha önce oluşturduğunuz **AzureStorageLinkedService**'e başvurur.</span><span class="sxs-lookup"><span data-stu-id="b920f-227">Refers to the **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="b920f-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="b920f-228">folderPath</span></span> | <span data-ttu-id="b920f-229">Blob **kapsayıcısını** ve giriş bloblarını içeren **klasörü** belirtir.</span><span class="sxs-lookup"><span data-stu-id="b920f-229">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="b920f-230">fileName</span><span class="sxs-lookup"><span data-stu-id="b920f-230">fileName</span></span> |<span data-ttu-id="b920f-231">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b920f-231">This property is optional.</span></span> <span data-ttu-id="b920f-232">Bu özelliği atarsanız, tüm folderPath dosyaları alınır.</span><span class="sxs-lookup"><span data-stu-id="b920f-232">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="b920f-233">Bu öğreticide yalnızca **input.log** işlenir.</span><span class="sxs-lookup"><span data-stu-id="b920f-233">In this tutorial, only the **input.log** is processed.</span></span> |
   | <span data-ttu-id="b920f-234">type</span><span class="sxs-lookup"><span data-stu-id="b920f-234">type</span></span> |<span data-ttu-id="b920f-235">Günlük dosyaları metin biçiminde olduğundan **TextFormat**'i kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="b920f-235">The log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="b920f-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="b920f-236">columnDelimiter</span></span> |<span data-ttu-id="b920f-237">Günlük dosyalarındaki sütunlar **virgül karakteri (`,`)** ile ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="b920f-237">columns in the log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="b920f-238">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="b920f-238">frequency/interval</span></span> |<span data-ttu-id="b920f-239">frequency **Ay**, interval ise **1** olarak ayarlanmıştır. Bu, giriş dilimlerinin aylık olarak kullanılabileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b920f-239">frequency set to **Month** and interval is **1**, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="b920f-240">external</span><span class="sxs-lookup"><span data-stu-id="b920f-240">external</span></span> | <span data-ttu-id="b920f-241">Bu özellik, giriş verileri bu işlem hattı tarafından oluşturulmadıysa **true** olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b920f-241">This property is set to **true** if the input data is not generated by this pipeline.</span></span> <span data-ttu-id="b920f-242">Bu öğreticide, input.log dosyası bu işlem hattı tarafından oluşturulmamıştır, bu nedenle özelliği true olarak ayarlayacağız.</span><span class="sxs-lookup"><span data-stu-id="b920f-242">In this tutorial, the input.log file is not generated by this pipeline, so we set the property to true.</span></span> |

    <span data-ttu-id="b920f-243">Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="b920f-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="b920f-244">Yeni oluşturulan veri kümesini dağıtmak için komut çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-244">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span> <span data-ttu-id="b920f-245">Veri kümesini soldaki ağaç görünümünde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b920f-245">You should see the dataset in the tree view on the left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="b920f-246">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="b920f-246">Create output dataset</span></span>
<span data-ttu-id="b920f-247">Şimdi, Azure Blob depolamada depolanan çıktı verilerini göstermek için çıktı veri kümesi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="b920f-247">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="b920f-248">**Data Factory Düzenleyicisi**’nde komut çubuğundaki **... Diğer**, **Yeni veri kümesi** öğelerine tıklayın ve **Azure Blob depolama** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b920f-248">In the **Data Factory Editor**, click **... More** on the command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="b920f-249">Aşağıdaki kod parçacığını kopyalayıp Taslak-1 penceresine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b920f-249">Copy and paste the following snippet to the Draft-1 window.</span></span> <span data-ttu-id="b920f-250">JSON parçacığında, **AzureBlobOutput** adlı bir veri kümesi oluşturur ve Hive betiğinin oluşturacağı verilerin yapısını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b920f-250">In the JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying the structure of the data that is produced by the Hive script.</span></span> <span data-ttu-id="b920f-251">Ek olarak, sonuçların **adfgetstarted** adlı blob kapsayıcısında ve **partitioneddata** adlı klasörde depolandığını belirtin.</span><span class="sxs-lookup"><span data-stu-id="b920f-251">In addition, you specify that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="b920f-252">Burada, **availability** bölümü çıktı veri kümesinin aylık tabanda oluşturulduğunu belirtiyor.</span><span class="sxs-lookup"><span data-stu-id="b920f-252">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>

    ```JSON
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adfgetstarted/partitioneddata",
          "format": {
            "type": "TextFormat",
            "columnDelimiter": ","
          }
        },
        "availability": {
          "frequency": "Month",
          "interval": 1
        }
      }
    }
    ```
    <span data-ttu-id="b920f-253">Bu özelliklerin açıklamaları için **Girdi veri kümesi oluşturma** bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b920f-253">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="b920f-254">Veri kümesi Data Factory hizmeti tarafından oluşturulduğundan çıktı veri kümesinde dış özellik ayarlamazsınız.</span><span class="sxs-lookup"><span data-stu-id="b920f-254">You do not set the external property on an output dataset as the dataset is produced by the Data Factory service.</span></span>
3. <span data-ttu-id="b920f-255">Yeni oluşturulan veri kümesini dağıtmak için komut çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-255">Click **Deploy** on the command bar to deploy the newly created dataset.</span></span>
4. <span data-ttu-id="b920f-256">Veri kümesinin başarıyla oluşturulduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-256">Verify that the dataset is created successfully.</span></span>

    ![Bağlı hizmetlerin bulunduğu ağaç görünümü](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="b920f-258">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b920f-258">Create pipeline</span></span>
<span data-ttu-id="b920f-259">Bu adımda, **HDInsightHive** etkinliğiyle ilk işlem hattınızı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="b920f-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="b920f-260">Girdi diliminin ayda bir (frequency: Month, interval: 1) kullanılabilir, çıktı dilimi ayda bir oluşturulur ve etkinlik zamanlayıcı özelliği de ayda bir olacak şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="b920f-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="b920f-261">Çıktı veri kümesi ve etkinlik zamanlayıcı ayarlarının eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b920f-261">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="b920f-262">Şu anda, çıktı veri kümesi zamanlamayı yönetendir; bu nedenle etkinlik hiçbir çıktı oluşturmasa bile sizin bir çıktı veri kümesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b920f-262">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="b920f-263">Etkinlik herhangi bir girdi almazsa, girdi veri kümesi oluşturma işlemini atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b920f-263">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="b920f-264">Aşağıdaki JSON’da kullanılan özellikler bu bölümün sonunda anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b920f-264">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="b920f-265">**Data Factory Düzenleyicisi**’nde, **Ellipsis (…) More commands**’e (Üç nokta (…) Daha fazla komut’a) sonra da **Yeni işlem hattı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-265">In the **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![yeni işlem hattı düğmesi](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="b920f-267">Aşağıdaki kod parçacığını kopyalayıp Taslak-1 penceresine yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="b920f-267">Copy and paste the following snippet to the Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b920f-268">**storageaccountname**’i JSON’daki depolama adınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b920f-268">Replace **storageaccountname** with the name of your storage account in the JSON.</span></span>
   >
   >

    ```JSON
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService",
                        "defines": {
                            "inputtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/inputdata",
                            "partitionedtable": "wasb://adfgetstarted@<storageaccountname>.blob.core.windows.net/partitioneddata"
                        }
                    },
                    "inputs": [
                        {
                            "name": "AzureBlobInput"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobOutput"
                        }
                    ],
                    "policy": {
                        "concurrency": 1,
                        "retry": 3
                    },
                    "scheduler": {
                        "frequency": "Month",
                        "interval": 1
                    },
                    "name": "RunSampleHiveActivity",
                    "linkedServiceName": "HDInsightOnDemandLinkedService"
                }
            ],
            "start": "2017-07-01T00:00:00Z",
            "end": "2017-07-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    <span data-ttu-id="b920f-269">JSON parçacığında, HDInsight kümesinde Veri işleyecek Hive’ı kullanan etkinlikten oluşmuş bir işlem hattı oluşturuyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="b920f-269">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="b920f-270">**partitionweblogs.hql** Hive betik dosyası Azure depolama hesabında (scriptLinkedService tarafından belirtilen **AzureStorageLinkedService** adıyla) ve **adfgetstarted** kapsayıcısındaki **betik** klasöründe depolanır.</span><span class="sxs-lookup"><span data-stu-id="b920f-270">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="b920f-271">Burada, **defines** bölümü hive betiğine Hive yapılandırma değerleri olarak (örn., ${hiveconf:inputtable}, ${hiveconf:partitionedtable}) geçirilecek çalışma zamanı ayarlarını belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b920f-271">The **defines** section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="b920f-272">İşlem hattının **start** ve **end** özellikleri işlem hattının etkin dönemini belirtir.</span><span class="sxs-lookup"><span data-stu-id="b920f-272">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="b920f-273">JSON etkinliğinde, Hive betiğinin **linkedServiceName** – **HDInsightOnDemandLinkedService** tarafından belirtilen işlemde çalışacağını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b920f-273">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b920f-274">Örnekte kullanılan JSON özellikleri hakkında ayrıntılı bilgi için [Azure Data Factory’deki işlem hatları ve etkinlikler](data-factory-create-pipelines.md) sayfasındaki “JSON İşlem Hatları” bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="b920f-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in the example.</span></span>
   >
   >
3. <span data-ttu-id="b920f-275">Şunları onaylayın:</span><span class="sxs-lookup"><span data-stu-id="b920f-275">Confirm the following:</span></span>

   1. <span data-ttu-id="b920f-276">Azure blob depolamada **adfgetstarted** kapsayıcısının **inputdata** klasöründe **input.log** dosyasının olduğunu</span><span class="sxs-lookup"><span data-stu-id="b920f-276">**input.log** file exists in the **inputdata** folder of the **adfgetstarted** container in the Azure blob storage</span></span>
   2. <span data-ttu-id="b920f-277">Azure blob depolamada **adfgetstarted** kapsayıcısının **script** klasöründe **partitionweblogs.hql** dosyasının olduğunu.</span><span class="sxs-lookup"><span data-stu-id="b920f-277">**partitionweblogs.hql** file exists in the **script** folder of the **adfgetstarted** container in the Azure blob storage.</span></span> <span data-ttu-id="b920f-278">Bu dosyaları görmüyorsanız lütfen [Öğreticiye Genel Bakış](data-factory-build-your-first-pipeline.md)’taki önkoşul adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-278">Complete the prerequisite steps in the [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="b920f-279">**storageaccountname**’i JSON işlem hattındaki depolama adınızla değiştirdiğinizi onaylayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-279">Confirm that you replaced **storageaccountname** with the name of your storage account in the pipeline JSON.</span></span>
4. <span data-ttu-id="b920f-280">İşlem hattını dağıtmak için komut çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-280">Click **Deploy** on the command bar to deploy the pipeline.</span></span> <span data-ttu-id="b920f-281">**start** ve **end** zamanları geçmişe ayarlanmış ve **isPaused** yanlış olarak ayarlanmış olduğundan işlem hattı (işlem hattında etkinlik) dağıtıldıktan hemen sonra çalışır.</span><span class="sxs-lookup"><span data-stu-id="b920f-281">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="b920f-282">İşlem hattını ağaç görünümünde gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-282">Confirm that you see the pipeline in the tree view.</span></span>

    ![İşlem hattının bulunduğu ağaç görünümü](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="b920f-284">Tebrikler, ilk işlem hattınızı başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="b920f-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="b920f-285">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="b920f-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="b920f-286">Diyagram Görünümünü kullanarak işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="b920f-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="b920f-287">Data Factory Düzenleyici dikey penceresini kapatmak ve Data Factory dikey penceresine dönmek için **X** işaretine, sonra da **Diyagram**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-287">Click **X** to close Data Factory Editor blades and to navigate back to the Data Factory blade, and click **Diagram**.</span></span>

    ![Diyagram kutucuğu](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="b920f-289">Diyagram Görünümü’nde, işlem hatlarına ve bu öğreticide kullanılan veri kümelerine bir genel bakış görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b920f-289">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Diyagram Görünümü](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="b920f-291">İşlem hattındaki tüm etkinlikleri görüntülemek için diyagramdaki işlem hattına sağ tıklayın ve Açık İşlem Hattı’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-291">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![İşlem hattı menüsünü açma](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="b920f-293">İşlem hattında HDInsightHive etkinliğini gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-293">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![İşlem hattı görünümünü açma](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="b920f-295">Önceki görünüme dönmek için en üstteki içerik haritası menüsünde **Data factory**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-295">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
5. <span data-ttu-id="b920f-296">**Diyagram Görünümü**’nde **AzureBlobInput** veri kümesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-296">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="b920f-297">Dilimin **Hazır** durumunda olduğunu onaylayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-297">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="b920f-298">Dilimin Hazır durumda gösterilmesi birkaç dakika alabilir.</span><span class="sxs-lookup"><span data-stu-id="b920f-298">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="b920f-299">Bir süre bekledikten sonra bu gerçekleşmiyorsa, girdi dosyasının (input.log) doğru kapsayıcıda (adfgetstarted) ve klasörde (inputdata) olup olmadığına bakın.</span><span class="sxs-lookup"><span data-stu-id="b920f-299">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Girdi dilimi hazır durumda](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="b920f-301">**AzureBlobInput** dikey penceresini kapatmak için **X** işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-301">Click **X** to close **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="b920f-302">**Diyagram Görünümü**’nde **AzureBlobOutput** veri kümesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-302">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="b920f-303">Dilimin işlenmekte olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b920f-303">You see that the slice that is currently being processed.</span></span>

   ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="b920f-305">İşlem tamamlandığında dilimi **Hazır** durumunda görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="b920f-305">When processing is done, you see the slice in **Ready** state.</span></span>

   ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="b920f-307">İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika).</span><span class="sxs-lookup"><span data-stu-id="b920f-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="b920f-308">Bu nedenle, işlem hattının dilimi işlemesi için **yaklaşık 30 dakika** bekleyin.</span><span class="sxs-lookup"><span data-stu-id="b920f-308">Therefore, expect the pipeline to       take **approximately 30 minutes** to process the slice.</span></span>
   >
   >

9. <span data-ttu-id="b920f-309">Dilim **Hazır** durumunda olduğunda çıktı verileri için blob depolama alanınızın **adfgetstarted** kapsayıcısında **partitioneddata** klasörünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="b920f-309">When the slice is in **Ready** state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  

   ![çıktı verileri](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="b920f-311">Dilimin ayrıntılarını bir **Veri dilimi** dikey penceresinde görmek için dilime tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-311">Click the slice to see details about it in a **Data slice** blade.</span></span>

   ![Veri dilimi ayrıntıları](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="b920f-313">Bir etkinlik çalışmasına ilişkin ayrıntıları (bu senaryoda Hive etkinliği) bir **Etkinlik çalışma ayrıntıları** penceresinde görmek için **Etkinlik çalışma listesi** içinden bir etkinlik çalışmasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-313">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Etkinlik çalışma ayrıntıları](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="b920f-315">Yürütülen Hive sorgusunu ve durum bilgilerini günlük dosyalarında görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b920f-315">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="b920f-316">Bu günlükler her türlü sorunu gidermek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="b920f-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="b920f-317">Daha fazla ayrıntı için [Azure portal dikey penceresi kullanılarak işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-pipelines.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="b920f-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b920f-318">Dilim başarıyla işlendiğinde girdi dosyası silinir.</span><span class="sxs-lookup"><span data-stu-id="b920f-318">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="b920f-319">Bu nedenle, dilimi yeniden çalıştırmak veya öğreticiyi yeniden uygulamak isterseniz girdi dosyasını (input.log) adfgetstarted kapsayıcısının inputdata klasörüne yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b920f-319">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="b920f-320">İzleme ve Yönetme Uygulamasını kullanarak işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="b920f-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="b920f-321">İşlem hatlarınızı izlemek için İzleme ve Yönetme uygulamasını da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b920f-321">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="b920f-322">Bu uygulamanın kullanımına ilişkin ayrıntılı bilgi için bkz. [İzleme ve Yönetme Uygulamasını kullanarak Azure Data Factory işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="b920f-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="b920f-323">Data factory’nin giriş sayfasındaki **İzleme ve Yönetme** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-323">Click **Monitor & Manage** tile on the home page for your data factory.</span></span>

    ![İzleme ve Yönetme kutucuğu](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="b920f-325">**İzleme ve Yönetme uygulaması**’nı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b920f-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="b920f-326">**Başlangıç saati** ve **Bitiş saati** değerlerini işlem hattınızın başlangıç ve bitiş saatleriyle eşleşecek şekilde değiştirin ve **Uygula**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b920f-326">Change the **Start time** and **End time** to match start and end times of your pipeline, and click **Apply**.</span></span>

    ![İzleme ve Yönetme Uygulaması](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="b920f-328">Ayrıntılarını görmek için **Etkinlik Pencereleri** listesinden bir etkinlik penceresi seçin.</span><span class="sxs-lookup"><span data-stu-id="b920f-328">Select an activity window in the **Activity Windows** list to see details about it.</span></span>

    ![Etkinlik penceresi ayrıntıları](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="b920f-330">Özet</span><span class="sxs-lookup"><span data-stu-id="b920f-330">Summary</span></span>
<span data-ttu-id="b920f-331">Bu öğreticide, HDInsight hadoop kümesindeki Hive betiği çalıştırılarak verileri işlemek için bir Azure data factory oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="b920f-331">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="b920f-332">Aşağıdaki adımları uygulamak için Azure Portal’da Data Factory Düzenleyici’yi kullandınız:</span><span class="sxs-lookup"><span data-stu-id="b920f-332">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="b920f-333">Oluşturulan Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="b920f-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="b920f-334">Oluşturulan iki **bağlı hizmet**:</span><span class="sxs-lookup"><span data-stu-id="b920f-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="b920f-335">Girdi/çıktı dosyalarını tutan Azure blob depolamanızı data factory’ye bağlamak için **Azure Storage** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="b920f-335">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="b920f-336">İsteğe bağlı HDInsight Hadoop kümesini data factory’ye bağlamak için isteğe bağlı **Azure HDInsight** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="b920f-336">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="b920f-337">Azure Data Factory, girdi verilerini işlemek, çıktı verilerini de oluşturmak için tam zamanında HDInsight Hadoop kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="b920f-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="b920f-338">İşlem hattındaki HDInsight Hive etkinliğiyle ilgili girdi ve çıktı verilerini açıklayan oluşturulan iki **veri kümesi**.</span><span class="sxs-lookup"><span data-stu-id="b920f-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="b920f-339">**HDInsight Hive** etkinliğine sahip oluşturulan bir **işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="b920f-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b920f-340">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="b920f-340">Next Steps</span></span>
<span data-ttu-id="b920f-341">Bu makalede, isteğe bağlı HDInsight kümesinde bir Hive betiği çalıştıran dönüştürme etkinliğine (HDInsight Etkinliği) sahip işlem hattı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="b920f-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="b920f-342">Verileri Azure Blob’tan Azure SQL’e kopyalamak için Kopyalama Etkinliği’nin kullanılması hakkında bilgi için bkz. [Öğretici: Verileri Azure blob’tan Azure SQL’e kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b920f-342">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b920f-343">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="b920f-343">See Also</span></span>
| <span data-ttu-id="b920f-344">Konu</span><span class="sxs-lookup"><span data-stu-id="b920f-344">Topic</span></span> | <span data-ttu-id="b920f-345">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b920f-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="b920f-346">İşlem hatları</span><span class="sxs-lookup"><span data-stu-id="b920f-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="b920f-347">Bu makale, Azure Data Factory’de işlem hatlarının ve etkinliklerini anlamanıza ve senaryonuz ya da işletmeniz için uçtan uca veri odaklı iş akışları oluşturmak amacıyla bunları nasıl kullanacağınızı anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b920f-347">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="b920f-348">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="b920f-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="b920f-349">Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="b920f-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="b920f-350">Zamanlama ve yürütme</span><span class="sxs-lookup"><span data-stu-id="b920f-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="b920f-351">Bu makalede Azure Data Factory uygulama modelinin zamanlama ve yürütme yönleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b920f-351">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="b920f-352">İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="b920f-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="b920f-353">Bu makalede İzleme ve Yönetim Uygulaması kullanılarak işlem hatlarını izleme, yönetme ve hatalarını ayıklama işlemleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b920f-353">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
