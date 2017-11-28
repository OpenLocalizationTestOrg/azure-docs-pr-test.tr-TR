---
title: "İlk data factory’nizi derleme (Visual Studio) | Microsoft Belgeleri"
description: "Bu öğreticide Visual Studio kullanarak örnek bir Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 7398c0c9-7a03-4628-94b3-f2aaef4a72c5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 77042219cbe698a33ab9447aa952586772897241
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a><span data-ttu-id="1df04-103">Öğretici: Visual Studio kullanarak veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="1df04-103">Tutorial: Create a data factory by using Visual Studio</span></span>
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [<span data-ttu-id="1df04-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1df04-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="1df04-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="1df04-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="1df04-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1df04-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="1df04-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1df04-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="1df04-108">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="1df04-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="1df04-109">REST API</span><span class="sxs-lookup"><span data-stu-id="1df04-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="1df04-110">Bu öğreticide Visual Studio kullanarak bir Azure veri fabrikası oluşturma ve izleme işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1df04-110">This tutorial shows you how to create an Azure data factory by using Visual Studio.</span></span> <span data-ttu-id="1df04-111">Data Factory proje şablonunu kullanarak bir Visual Studio projesi oluşturacak, JSON biçiminde Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) tanımlayacak ve ardından bu varlıkları bulutta yayımlayacak/dağıtacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1df04-111">You create a Visual Studio project using the Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities to the cloud.</span></span> 

<span data-ttu-id="1df04-112">Bu öğreticideki işlem hattı bir etkinlik içerir: **HDInsight Hive etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="1df04-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="1df04-113">Bu etkinlik, Azure HDInsight kümesi üzerinde çıkış verileri üretmek üzere giriş verilerini dönüştüren bir hive betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="1df04-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="1df04-114">İşlem hattı, belirtilen başlangıç ve bitiş saatleri arasında ayda bir kez çalışacak şekilde zamanlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1df04-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="1df04-115">Bu öğreticide, Azure Data Factory kullanarak verilerin nasıl kopyalanacağı gösterilmemektedir.</span><span class="sxs-lookup"><span data-stu-id="1df04-115">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="1df04-116">Azure Data Factory kullanarak verileri kopyalama öğreticisi için bkz. [Öğretici: Blob Depolama’dan SQL Veritabanı’na veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1df04-116">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="1df04-117">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="1df04-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="1df04-118">Bir etkinliğin çıkış veri kümesini diğer etkinliğin giriş veri kümesi olarak ayarlayarak iki etkinliği zincirleyebilir, yani bir etkinliğin diğerinden sonra çalıştırılmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-118">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="1df04-119">Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="1df04-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="walkthrough-create-and-publish-data-factory-entities"></a><span data-ttu-id="1df04-120">İzlenecek Yol: Data Factory varlıkları oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="1df04-120">Walkthrough: Create and publish Data Factory entities</span></span>
<span data-ttu-id="1df04-121">Bu izlenecek yolun bir parçası olarak gerçekleştireceğiniz adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1df04-121">Here are the steps you perform as part of this walkthrough:</span></span>

1. <span data-ttu-id="1df04-122">İki bağlı hizmet oluşturun: **AzureStorageLinkedService1** ve **HDInsightOnDemandLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="1df04-122">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span></span> 
   
    <span data-ttu-id="1df04-123">Bu öğreticide, hive etkinliği için giriş ve çıkış verileri aynı Azure Blob Depolama içindedir.</span><span class="sxs-lookup"><span data-stu-id="1df04-123">In this tutorial, both input and output data for the hive activity are in the same Azure Blob Storage.</span></span> <span data-ttu-id="1df04-124">İsteğe bağlı HDInsight kümesini kullanarak, çıkış verileri üretmek üzere mevcut giriş verilerini işleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-124">You use an on-demand HDInsight cluster to process existing input data to produce output data.</span></span> <span data-ttu-id="1df04-125">İsteğe bağlı HDInsight kümesi, giriş verileri işlenmeye hazır olduğunda Azure Data Factory tarafından çalışma zamanında otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1df04-125">The on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when the input data is ready to be processed.</span></span> <span data-ttu-id="1df04-126">Çalışma zamanında Data Factory hizmetinin veri depolarınıza veya işlemlerinize bağlanabilmesi için, bunları veri fabrikanıza bağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1df04-126">You need to link your data stores or computes to your data factory so that the Data Factory service can connect to them at runtime.</span></span> <span data-ttu-id="1df04-127">Bu nedenle, AzureStorageLinkedService1 kullanarak Azure Depolama Hesabınızı veri fabrikasına bağlarsınız ve HDInsightOnDemandLinkedService1 kullanarak isteğe bağlı HDInsight kümesini bağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="1df04-127">Therefore, you link your Azure Storage Account to the data factory by using the AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using the HDInsightOnDemandLinkedService1.</span></span> <span data-ttu-id="1df04-128">Yayımlama sırasında, oluşturulacak veri fabrikasının adını veya mevcut bir veri fabrikasını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-128">When publishing, you specify the name for the data factory to be created or an existing data factory.</span></span>  
2. <span data-ttu-id="1df04-129">Azure blob depolama alanında depolanan giriş/çıkış verilerini temsil eden iki veri kümesi oluşturun: **InputDataset** ve **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="1df04-129">Create two datasets: **InputDataset** and **OutputDataset**, which represent the input/output data that is stored in the Azure blob storage.</span></span> 
   
    <span data-ttu-id="1df04-130">Bu veri kümesi tanımları, önceki adımda oluşturduğunuz bağlı Azure Depolama hizmetini ifade eder.</span><span class="sxs-lookup"><span data-stu-id="1df04-130">These dataset definitions refer to the Azure Storage linked service you created in the previous step.</span></span> <span data-ttu-id="1df04-131">InputDataset için blob kapsayıcısını (adfgetstarted) ve giriş verileriyle birlikte blob içeren klasörü (inptutdata) belirtin.</span><span class="sxs-lookup"><span data-stu-id="1df04-131">For the InputDataset, you specify the blob container (adfgetstarted) and the folder (inptutdata) that contains a blob with the input data.</span></span> <span data-ttu-id="1df04-132">OutputDataset için blob kapsayıcısını (adfgetstarted) ve çıkış verilerini içeren klasörü (partitioneddata) belirtin.</span><span class="sxs-lookup"><span data-stu-id="1df04-132">For the OutputDataset, you specify the blob container (adfgetstarted) and the folder (partitioneddata) that holds the output data.</span></span> <span data-ttu-id="1df04-133">Yapı, kullanılabilirlik ve ilke gibi diğer özellikleri de belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-133">You also specify other properties such as structure, availability, and policy.</span></span>
3. <span data-ttu-id="1df04-134">**MyFirstPipeline** adlı bir işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1df04-134">Create a pipeline named **MyFirstPipeline**.</span></span> 
  
    <span data-ttu-id="1df04-135">Bu kılavuzdaki işlem hattı yalnızca bir etkinlik içerir: **HDInsight Hive Etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="1df04-135">In this walkthrough, the pipeline has only one activity: **HDInsight Hive Activity**.</span></span> <span data-ttu-id="1df04-136">Bu etkinlik, isteğe bağlı bir HDInsight kümesi üzerinde hive betiği çalıştırarak çıkış verileri üretmek üzere giriş verilerini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1df04-136">This activity transform input data to produce output data by running a hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="1df04-137">Hive etkinliği hakkında daha fazla bilgi edinmek için bkz. [Hive Etkinliği](data-factory-hive-activity.md)</span><span class="sxs-lookup"><span data-stu-id="1df04-137">To learn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span></span> 
4. <span data-ttu-id="1df04-138">**DataFactoryUsingVS** adlı bir veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1df04-138">Create a data factory named **DataFactoryUsingVS**.</span></span> <span data-ttu-id="1df04-139">Veri fabrikasını ve tüm Data Factory varlıklarını (bağlı hizmetler, tablolar ve işlem hattı) dağıtın.</span><span class="sxs-lookup"><span data-stu-id="1df04-139">Deploy the data factory and all Data Factory entities (linked services, tables, and the pipeline).</span></span>
5. <span data-ttu-id="1df04-140">Yayımladıktan sonra, işlem hattını izlemek için Azure portalı dikey pencereleri ile İzleme ve Yönetim Uygulamasını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-140">After you publish, you use Azure portal blades and Monitoring & Management App to monitor the pipeline.</span></span> 
  
### <a name="prerequisites"></a><span data-ttu-id="1df04-141">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1df04-141">Prerequisites</span></span>
1. <span data-ttu-id="1df04-142">[Öğreticiye Genel Bakış](data-factory-build-your-first-pipeline.md) makalesinin tamamını okuyun ve **ön koşul** adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-142">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span> <span data-ttu-id="1df04-143">Ayrıca, üst kısımdaki açılır listede bulunan **Genel bakış ve önkoşullar** seçeneğini belirleyerek makaleye geçiş yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-143">You can also select the **Overview and prerequisites** option in the drop-down list at the top to switch to the article.</span></span> <span data-ttu-id="1df04-144">Önkoşulları tamamladıktan sonra, açılır listeden **Visual Studio** seçeneğini belirleyerek bu makaleye geri dönün.</span><span class="sxs-lookup"><span data-stu-id="1df04-144">After you complete the prerequisites, switch back to this article by selecting **Visual Studio** option in the drop-down list.</span></span>
2. <span data-ttu-id="1df04-145">Data Factory örnekleri oluşturmak için abonelik/kaynak grubu düzeyinde [Data Factory Katılımcısı](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rolünün üyesi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1df04-145">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>  
3. <span data-ttu-id="1df04-146">Bilgisayarınızda şunların yüklü olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="1df04-146">You must have the following installed on your computer:</span></span>
   * <span data-ttu-id="1df04-147">Visual Studio 2013 veya Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="1df04-147">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="1df04-148">Visual Studio 2013 veya Visual Studio 2015 için Azure SDK’sını indirin.</span><span class="sxs-lookup"><span data-stu-id="1df04-148">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="1df04-149">[Azure İndirme Sayfası](https://azure.microsoft.com/downloads/)’na gidin ve **.NET** bölümündeki **VS 2013** veya **VS 2015**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-149">Navigate to [Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in the **.NET** section.</span></span>
   * <span data-ttu-id="1df04-150">Visual Studio için en son Azure Data Factory eklentisini indirin: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) veya [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="1df04-150">Download the latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="1df04-151">Aşağıdaki adımları uygulayarak eklentiyi güncelleştirebilirsiniz: Menüde **Araçlar** -> **Uzantılar ve Güncelleştirmeler** -> **Çevrimiçi** -> **Visual Studio Galerisi** -> **Visual Studio için Microsoft Azure Data Factory Araçları** -> **Güncelleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-151">You can also update the plugin by doing the following steps: On the menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

<span data-ttu-id="1df04-152">Şimdi bir Azure data factory oluşturmak için Visual Studio kullanalım.</span><span class="sxs-lookup"><span data-stu-id="1df04-152">Now, let's use Visual Studio to create an Azure data factory.</span></span>

### <a name="create-visual-studio-project"></a><span data-ttu-id="1df04-153">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1df04-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="1df04-154">**Visual Studio 2013** veya **Visual Studio 2015**’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="1df04-154">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span></span> <span data-ttu-id="1df04-155">**Dosya**’ya tıklayın, **Yeni**’nin üzerine gelin ve **Proje**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-155">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="1df04-156">**Yeni Proje** iletişim kutusu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1df04-156">You should see the **New Project** dialog box.</span></span>  
2. <span data-ttu-id="1df04-157">**Yeni Proje** iletişim kutusunda **DataFactory** şablonunu seçip **Boş Data Factory Projesi**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-157">In the **New Project** dialog, select the **DataFactory** template, and click **Empty Data Factory Project**.</span></span>   

    ![Yeni proje iletişim kutusu](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. <span data-ttu-id="1df04-159">Proje için bir **ad**, **konum** ve **çözüm** için ad girip **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-159">Enter a **name** for the project, **location**, and a name for the **solution**, and click **OK**.</span></span>

    ![Çözüm Gezgini](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a><span data-ttu-id="1df04-161">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="1df04-161">Create linked services</span></span>
<span data-ttu-id="1df04-162">Bu adımda iki bağlı hizmet oluşturursunuz: **Azure Depolama** ve **İsteğe bağlı HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1df04-162">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span></span> 

<span data-ttu-id="1df04-163">Azure Depolama bağlı hizmeti, bağlantı bilgilerini sağlayarak Azure Depolama hesabınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="1df04-163">The Azure Storage linked service links your Azure Storage account to the data factory by providing the connection information.</span></span> <span data-ttu-id="1df04-164">Data Factory hizmeti, çalışma zamanında Azure depolamaya bağlanmak için bağlı hizmet ayarındaki bağlantı dizesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="1df04-164">Data Factory service uses the connection string from the linked service setting to connect to the Azure storage at runtime.</span></span> <span data-ttu-id="1df04-165">Bu depolama alanı, işlem hattının giriş ve çıkış verilerinin yanı sıra hive etkinliği tarafından kullanılan hive betik dosyasını içerir.</span><span class="sxs-lookup"><span data-stu-id="1df04-165">This storage holds input and output data for the pipeline, and the hive script file used by the hive activity.</span></span> 

<span data-ttu-id="1df04-166">İsteğe bağlı HDInsight bağlı hizmeti ile, giriş verileri işlenmeye hazır olduğunda HDInsight kümesi çalışma zamanında otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1df04-166">With on-demand HDInsight linked service, The HDInsight cluster is automatically created at runtime when the input data is ready to processed.</span></span> <span data-ttu-id="1df04-167">Kümenin işlenmesi tamamlandıktan sonra küme belirtilen süre boyunca boşta kalırsa, küme silinir.</span><span class="sxs-lookup"><span data-stu-id="1df04-167">The cluster is deleted after it is done processing and idle for the specified amount of time.</span></span> 

> [!NOTE]
> <span data-ttu-id="1df04-168">Data Factory çözümünüzü yayımlarken, ad ve ayarlarını belirterek bir veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1df04-168">You create a data factory by specifying its name and settings at the time of publishing your Data Factory solution.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="1df04-169">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="1df04-169">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="1df04-170">Çözüm gezgininde **Bağlı Hizmetler**’e sağ tıklayın, **Ekle**’nin üzerine gelip **Yeni Öğe**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-170">Right-click **Linked Services** in the solution explorer, point to **Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="1df04-171">**Yeni Öğe Ekle** iletişim kutusunda **Azure Storage Bağlı Hizmeti**’ni listeden seçip **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-171">In the **Add New Item** dialog box, select **Azure Storage Linked Service** from the list, and click **Add**.</span></span>
    <span data-ttu-id="1df04-172">![Azure Storage Bağlı Hizmeti](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="1df04-172">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span></span>
3. <span data-ttu-id="1df04-173">`<accountname>` ve `<accountkey>` değerlerini Azure depolama hesabınızın adı ve anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1df04-173">Replace `<accountname>` and `<accountkey>` with the name of your Azure storage account and its key.</span></span> <span data-ttu-id="1df04-174">Depolama erişim anahtarınızı nasıl alabileceğinizi öğrenmek için [Depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account) sayfasındaki depolama erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma bilgilerine bakın.</span><span class="sxs-lookup"><span data-stu-id="1df04-174">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
    <span data-ttu-id="1df04-175">![Azure Storage Bağlı Hizmeti](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="1df04-175">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span></span>
4. <span data-ttu-id="1df04-176">**AzureStorageLinkedService1.json** dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1df04-176">Save the **AzureStorageLinkedService1.json** file.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="1df04-177">Azure HDInsight bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="1df04-177">Create Azure HDInsight linked service</span></span>
1. <span data-ttu-id="1df04-178">**Çözüm Gezgini**’nde **Bağlı Hizmetler**’e sağ tıklayın, **Ekle**’nin üzerine gelip Y**eni Öğe**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-178">In the **Solution Explorer**, right-click **Linked Services**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="1df04-179">**İsteğe Bağlı HDInsight Bağlı Hizmeti**’ni seçin ve **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-179">Select **HDInsight On Demand Linked Service**, and click **Add**.</span></span>
3. <span data-ttu-id="1df04-180">**JSON** değerini aşağıdaki JSON ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1df04-180">Replace the **JSON** with the following JSON:</span></span>

     ```json
    {
        "name": "HDInsightOnDemandLinkedService",
        "properties": {
        "type": "HDInsightOnDemand",
            "typeProperties": {
                "version": "3.5",
                "clusterSize": 1,
                "timeToLive": "00:05:00",
                "osType": "Linux",
                "linkedServiceName": "AzureStorageLinkedService1"
            }
        }
    }
    ```

    <span data-ttu-id="1df04-181">Aşağıdaki tabloda, kod parçacığında kullanılan JSON özellikleri için açıklamalar verilmektedir:</span><span class="sxs-lookup"><span data-stu-id="1df04-181">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    <span data-ttu-id="1df04-182">Özellik</span><span class="sxs-lookup"><span data-stu-id="1df04-182">Property</span></span> | <span data-ttu-id="1df04-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1df04-183">Description</span></span>
    -------- | ----------- 
    <span data-ttu-id="1df04-184">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="1df04-184">ClusterSize</span></span> | <span data-ttu-id="1df04-185">HDInsight Hadoop kümesinin boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="1df04-185">Specifies the size of the HDInsight Hadoop cluster.</span></span>
    <span data-ttu-id="1df04-186">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="1df04-186">TimeToLive</span></span> | <span data-ttu-id="1df04-187">Silinmeden önce HDInsight kümesinin boşta kalma süresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1df04-187">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span>
    <span data-ttu-id="1df04-188">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1df04-188">linkedServiceName</span></span> | <span data-ttu-id="1df04-189">HDInsight Hadoop kümesi tarafından oluşturulan günlükleri depolamak için kullanılan depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="1df04-189">Specifies the storage account that is used to store the logs that are generated by HDInsight Hadoop cluster.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="1df04-190">HDInsight kümesi JSON’da belirttiğiniz blob depolamada (linkedServiceName) bir **varsayılan kapsayıcı** oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1df04-190">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName).</span></span> <span data-ttu-id="1df04-191">HDInsight, küme silindiğinde bu kapsayıcıyı silmez.</span><span class="sxs-lookup"><span data-stu-id="1df04-191">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="1df04-192">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="1df04-192">This behavior is by design.</span></span> <span data-ttu-id="1df04-193">İsteğe bağlı HDInsight bağlı hizmeti kullanıldığında, mevcut canlı bir küme olmadığı sürece bir dilim her işlendiğinde bir HDInsight kümesi oluşturulur (timeToLive).</span><span class="sxs-lookup"><span data-stu-id="1df04-193">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="1df04-194">Küme, işlem tamamlandığında otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="1df04-194">The cluster is automatically deleted when the processing is done.</span></span>
    > 
    > <span data-ttu-id="1df04-195">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1df04-195">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="1df04-196">İşlerin sorunları giderilmesi için bunlara gerek yoksa, depolama maliyetini azaltmak için bunları silmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-196">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="1df04-197">Bu kapsayıcı adları bir düzene sahiptir: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="1df04-197">The names of these containers follow a pattern: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span></span> <span data-ttu-id="1df04-198">Azure blob depolamada kapsayıcı silmek için [Microsoft Storage Gezgini](http://storageexplorer.com/) gibi araçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="1df04-198">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

    <span data-ttu-id="1df04-199">JSON özellikleri hakkında daha fazla bilgi için [İşlem bağlı hizmetleri](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="1df04-199">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span></span> 
4. <span data-ttu-id="1df04-200">**HDInsightOnDemandLinkedService1.json** dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1df04-200">Save the **HDInsightOnDemandLinkedService1.json** file.</span></span>

### <a name="create-datasets"></a><span data-ttu-id="1df04-201">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="1df04-201">Create datasets</span></span>
<span data-ttu-id="1df04-202">Bu adımda, Hive işlenmesi için girdi ve çıktı verilerini temsil edecek veri kümeleri oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1df04-202">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="1df04-203">Bu veri kümeleri, bu öğreticide daha önce oluşturduğunuz **AzureStorageLinkedService1** öğesine başvurur.</span><span class="sxs-lookup"><span data-stu-id="1df04-203">These datasets refer to the **AzureStorageLinkedService1** you have created earlier in this tutorial.</span></span> <span data-ttu-id="1df04-204">Bağlı hizmet Azure Storage hesabını belirtirken, veri kümeleri de girdi ve çıktı verilerini tutan depolama biriminde kapsayıcı, klasör, dosya adı belirtir.</span><span class="sxs-lookup"><span data-stu-id="1df04-204">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>   

#### <a name="create-input-dataset"></a><span data-ttu-id="1df04-205">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1df04-205">Create input dataset</span></span>
1. <span data-ttu-id="1df04-206">**Çözüm Gezgini**’nde **Tablolar**’a sağ tıklayın, **Ekle**’nin üzerine gelip **Yeni Öğe**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-206">In the **Solution Explorer**, right-click **Tables**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="1df04-207">Listeden **Azure Blob**’u seçin, dosya adını **InputDataSet.json** olarak değiştirin ve **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-207">Select **Azure Blob** from the list, change the name of the file to **InputDataSet.json**, and click **Add**.</span></span>
3. <span data-ttu-id="1df04-208">Düzenleyicide **JSON** değerini aşağıdaki JSON kod parçacığıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1df04-208">Replace the **JSON** in the editor with the following JSON snippet:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    <span data-ttu-id="1df04-209">Bu JSON parçacığı, işlem hattındaki hive etkinliğinin giriş verilerini temsil eden **AzureBlobInput** adlı bir veri kümesi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1df04-209">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for the hive activity in the pipeline.</span></span> <span data-ttu-id="1df04-210">Giriş verilerinin `adfgetstarted` adlı blob kapsayıcısında ve `inputdata` adlı klasörde bulunduğunu belirtin.</span><span class="sxs-lookup"><span data-stu-id="1df04-210">You specify that the input data is located in the blob container called `adfgetstarted` and the folder called `inputdata`.</span></span>

    <span data-ttu-id="1df04-211">Aşağıdaki tabloda, kod parçacığında kullanılan JSON özellikleri için açıklamalar verilmektedir:</span><span class="sxs-lookup"><span data-stu-id="1df04-211">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    <span data-ttu-id="1df04-212">Özellik</span><span class="sxs-lookup"><span data-stu-id="1df04-212">Property</span></span> | <span data-ttu-id="1df04-213">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1df04-213">Description</span></span> |
    -------- | ----------- |
    <span data-ttu-id="1df04-214">type</span><span class="sxs-lookup"><span data-stu-id="1df04-214">type</span></span> |<span data-ttu-id="1df04-215">Veriler Azure Blob Depolamada yer aldığından type özelliği **AzureBlob** olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1df04-215">The type property is set to **AzureBlob** because data resides in Azure Blob Storage.</span></span>
    <span data-ttu-id="1df04-216">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1df04-216">linkedServiceName</span></span> | <span data-ttu-id="1df04-217">Daha önce oluşturduğunuz AzureStorageLinkedService1’i ifade eder.</span><span class="sxs-lookup"><span data-stu-id="1df04-217">Refers to the AzureStorageLinkedService1 you created earlier.</span></span>
    <span data-ttu-id="1df04-218">fileName</span><span class="sxs-lookup"><span data-stu-id="1df04-218">fileName</span></span> |<span data-ttu-id="1df04-219">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1df04-219">This property is optional.</span></span> <span data-ttu-id="1df04-220">Bu özelliği atarsanız, tüm folderPath dosyaları alınır.</span><span class="sxs-lookup"><span data-stu-id="1df04-220">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="1df04-221">Bu durumda, yalnızca input.log işlenir.</span><span class="sxs-lookup"><span data-stu-id="1df04-221">In this case, only the input.log is processed.</span></span>
    <span data-ttu-id="1df04-222">type</span><span class="sxs-lookup"><span data-stu-id="1df04-222">type</span></span> | <span data-ttu-id="1df04-223">Günlük dosyaları metin biçiminde olduğundan TextFormat kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="1df04-223">The log files are in text format, so we use TextFormat.</span></span> |
    <span data-ttu-id="1df04-224">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="1df04-224">columnDelimiter</span></span> | <span data-ttu-id="1df04-225">Günlük dosyalarındaki sütunlar virgül (`,`) ile ayrılmıştır</span><span class="sxs-lookup"><span data-stu-id="1df04-225">columns in the log files are delimited by the comma character (`,`)</span></span>
    <span data-ttu-id="1df04-226">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="1df04-226">frequency/interval</span></span> | <span data-ttu-id="1df04-227">frequency Ay, interval de 1 olarak ayarlanmıştır; girdi dilimlerinin aylık olarak kullanılabileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1df04-227">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span>
    <span data-ttu-id="1df04-228">external</span><span class="sxs-lookup"><span data-stu-id="1df04-228">external</span></span> | <span data-ttu-id="1df04-229">Bu özellik, etkinliğin giriş verileri işlem hattı tarafından oluşturulmadıysa true olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1df04-229">This property is set to true if the input data for the activity is not generated by the pipeline.</span></span> <span data-ttu-id="1df04-230">Bu özellik yalnızca giriş veri kümelerinde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="1df04-230">This property is only specified on input datasets.</span></span> <span data-ttu-id="1df04-231">Birinci etkinliğin giriş veri kümesi için her zaman true olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-231">For the input dataset of the first activity, always set it to true.</span></span>
4. <span data-ttu-id="1df04-232">**InputDataset.json** dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1df04-232">Save the **InputDataset.json** file.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="1df04-233">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1df04-233">Create output dataset</span></span>
<span data-ttu-id="1df04-234">Şimdi, Azure Blob depolamada depolanan çıkış verilerini göstermek için çıkış veri kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1df04-234">Now, you create the output dataset to represent output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="1df04-235">**Çözüm Gezgini**’nde **tablolar**’a sağ tıklayın, **Ekle**’nin üzerine gelip **Yeni Öğe**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-235">In the **Solution Explorer**, right-click **tables**, point to **Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="1df04-236">Listeden **Azure Blob**’u seçin, dosya adını **OutputDataset.json** olarak değiştirin ve **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-236">Select **Azure Blob** from the list, change the name of the file to **OutputDataset.json**, and click **Add**.</span></span>
3. <span data-ttu-id="1df04-237">Düzenleyicide **JSON**’u aşağıdaki JSON ile değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1df04-237">Replace the **JSON** in the editor with the following JSON:</span></span>
    
    ```json
    {
        "name": "AzureBlobOutput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService1",
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
    <span data-ttu-id="1df04-238">JSON parçacığı, işlem hattındaki hive etkinliği tarafından oluşturulan çıkış verilerini temsil eden **AzureBlobOutput** adlı bir veri kümesi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1df04-238">The JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by the hive activity in the pipeline.</span></span> <span data-ttu-id="1df04-239">Hive etkinliği tarafından oluşturulan çıkış verilerinin `adfgetstarted` adlı blob kapsayıcısına ve `partitioneddata` adlı klasöre yerleştirileceğini belirtin.</span><span class="sxs-lookup"><span data-stu-id="1df04-239">You specify that the output data is produced by the hive activity is placed in the blob container called `adfgetstarted` and the folder called `partitioneddata`.</span></span> 
    
    <span data-ttu-id="1df04-240">Burada, **availability** bölümü çıktı veri kümesinin aylık tabanda oluşturulduğunu belirtiyor.</span><span class="sxs-lookup"><span data-stu-id="1df04-240">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span> <span data-ttu-id="1df04-241">Çıkış veri kümesi, işlem hattının zamanlamasını belirler.</span><span class="sxs-lookup"><span data-stu-id="1df04-241">The output dataset drives the schedule of the pipeline.</span></span> <span data-ttu-id="1df04-242">İşlem hattı, ayda bir kez başlangıç ve bitiş saatleri arasında çalışır.</span><span class="sxs-lookup"><span data-stu-id="1df04-242">The pipeline runs monthly between its start and end times.</span></span> 

    <span data-ttu-id="1df04-243">Bu özelliklerin açıklamaları için **Girdi veri kümesi oluşturma** bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="1df04-243">See **Create the input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="1df04-244">Veri kümesi işlem hattı tarafından oluşturulduğundan çıkış veri kümesinde dış özellik ayarlamayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-244">You do not set the external property on an output dataset as the dataset is produced by the pipeline.</span></span>
4. <span data-ttu-id="1df04-245">**OutputDataset.json** dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1df04-245">Save the **OutputDataset.json** file.</span></span>

### <a name="create-pipeline"></a><span data-ttu-id="1df04-246">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1df04-246">Create pipeline</span></span>
<span data-ttu-id="1df04-247">Şimdiye kadar, Azure Depolama bağlı hizmetinin yanı sıra giriş ve çıkış veri kümelerini oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="1df04-247">You have created the Azure Storage linked service, and input and output datasets so far.</span></span> <span data-ttu-id="1df04-248">Şimdi, **HDInsightHive** etkinliğiyle bir işlem hattı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1df04-248">Now, you create a pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="1df04-249">Hive etkinliğinin **input** değeri **AzureBlobInput**, **output** değeri ise **AzureBlobOutput** olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1df04-249">The **input** for the hive activity is set to **AzureBlobInput** and **output** is set to **AzureBlobOutput**.</span></span> <span data-ttu-id="1df04-250">Giriş veri kümesinin bir dilimi ayda bir kez kullanılabilir (sıklık: Ay, aralık: 1), çıkış dilimi de ayda bir kez üretilir.</span><span class="sxs-lookup"><span data-stu-id="1df04-250">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and the output slice is produced monthly too.</span></span> 

1. <span data-ttu-id="1df04-251">**Çözüm Gezgini**’nde **İşlem Hatları**’na sağ tıklayın, **Ekle**’nin üzerine gelip **Yeni Öğe**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-251">In the **Solution Explorer**, right-click **Pipelines**, point to **Add**, and click **New Item.**</span></span>
2. <span data-ttu-id="1df04-252">Listeden **Hive Dönüşüm İşlem Hattı**’nı seçin ve **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-252">Select **Hive Transformation Pipeline** from the list, and click **Add**.</span></span>
3. <span data-ttu-id="1df04-253">**JSON**’u aşağıdaki kod parçacığıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1df04-253">Replace the **JSON** with the following snippet:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1df04-254">`<storageaccountname>` değerini depolama hesabınızın adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1df04-254">Replace `<storageaccountname>` with the name of your storage account.</span></span>

    ```json
    {
        "name": "MyFirstPipeline",
        "properties": {
            "description": "My first Azure Data Factory pipeline",
            "activities": [
                {
                    "type": "HDInsightHive",
                    "typeProperties": {
                        "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                        "scriptLinkedService": "AzureStorageLinkedService1",
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
            "start": "2016-04-01T00:00:00Z",
            "end": "2016-04-02T00:00:00Z",
            "isPaused": false
        }
    }
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="1df04-255">`<storageaccountname>` değerini depolama hesabınızın adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1df04-255">Replace `<storageaccountname>` with the name of your storage account.</span></span>

    <span data-ttu-id="1df04-256">JSON parçacığı, tek etkinlikten (Hive Etkinliği) oluşan bir işlem hattı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="1df04-256">The JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span></span> <span data-ttu-id="1df04-257">Bu etkinlik, isteğe bağlı bir HDInsight kümesi üzerinde çıkış verileri üretmek üzere giriş verilerini işleyen bir Hive betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="1df04-257">This activity runs a Hive script to process input data on an on-demand HDInsight cluster to produce output data.</span></span> <span data-ttu-id="1df04-258">İşlem hattı JSON etkinlikler bölümünde, dizi içinde türü **HDInsightHive** olarak ayarlanmış yalnızca bir etkinlik görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1df04-258">In the activities section of the pipeline JSON, you see only one activity in the array with type set to **HDInsightHive**.</span></span> 

    <span data-ttu-id="1df04-259">HDInsight Hive etkinliğine özel type özelliklerinde, hangi Azure Depolama bağlı hizmetinin hive betik dosyasına sahip olduğunu, betik dosyasının yolunu ve betik dosyasının parametrelerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="1df04-259">In the type properties that are specific to HDInsight Hive activity, you specify what Azure Storage linked service has the hive script file, the path to the script file, and parameters to the script file.</span></span> 

    <span data-ttu-id="1df04-260">**partitionweblogs.hql** Hive betik dosyası Azure depolama hesabında (scriptLinkedService tarafından belirtilir) ve `adfgetstarted` kapsayıcısındaki `script` klasöründe depolanır.</span><span class="sxs-lookup"><span data-stu-id="1df04-260">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService), and in the `script` folder in the container `adfgetstarted`.</span></span>

    <span data-ttu-id="1df04-261">`defines` bölümü, hive betiğine Hive yapılandırma değerleri olarak (örn `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`) geçirilen çalışma zamanı ayarlarını belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1df04-261">The `defines` section is used to specify the runtime settings that are passed to the hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span></span>

    <span data-ttu-id="1df04-262">İşlem hattının **start** ve **end** özellikleri işlem hattının etkin dönemini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1df04-262">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span> <span data-ttu-id="1df04-263">Aylık olarak üretilecek veri kümesini yapılandırdınız; bu nedenle, (başlangıç ve bitiş tarihleri aynı ayda olduğu için) işlem hattı tarafından yalnızca bir dilim üretilir.</span><span class="sxs-lookup"><span data-stu-id="1df04-263">You configured the dataset to be produced monthly, therefore, only once slice is produced by the pipeline (because the month is same in start and end dates).</span></span>

    <span data-ttu-id="1df04-264">JSON etkinliğinde, Hive betiğinin **linkedServiceName** – **HDInsightOnDemandLinkedService** tarafından belirtilen işlemde çalışacağını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-264">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>
4. <span data-ttu-id="1df04-265">**HiveActivity1.json** dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="1df04-265">Save the **HiveActivity1.json** file.</span></span>

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a><span data-ttu-id="1df04-266">partitionweblogs.hql ve input.log dosyalarını bağımlılık olarak ekleme</span><span class="sxs-lookup"><span data-stu-id="1df04-266">Add partitionweblogs.hql and input.log as a dependency</span></span>
1. <span data-ttu-id="1df04-267">**Çözüm Gezgini** penceresinde **Bağımlılıklar**’a sağ tıklayın, **Ekle**’nin üzerine gelip **Mevcut Öğe**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-267">Right-click **Dependencies** in the **Solution Explorer** window, point to **Add**, and click **Existing Item**.</span></span>  
2. <span data-ttu-id="1df04-268">**C:\ADFGettingStarted** yoluna gidin ve **partitionweblogs.hql**, **input.log** dosyalarını seçip **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-268">Navigate to the **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span></span> <span data-ttu-id="1df04-269">Bu iki dosyayı [Öğreticiye Genel Bakış](data-factory-build-your-first-pipeline.md)’taki ön koşulların bir parçası olarak oluşturmuştunuz.</span><span class="sxs-lookup"><span data-stu-id="1df04-269">You created these two files as part of prerequisites from the [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="1df04-270">Sonraki adımda çözümü yayımladığınızda, **partitionweblogs.hql** dosyası `adfgetstarted` blob kapsayıcısındaki **script** klasörüne yüklenir.</span><span class="sxs-lookup"><span data-stu-id="1df04-270">When you publish the solution in the next step, the **partitionweblogs.hql** file is uploaded to the **script** folder in the `adfgetstarted` blob container.</span></span>   

### <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="1df04-271">Data Factory varlıklarını yayımlama/dağıtma</span><span class="sxs-lookup"><span data-stu-id="1df04-271">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="1df04-272">Bu adımda, projenizdeki Data Factory varlıklarını (bağlı hizmetler, veri kümeleri ve işlem hattı) Azure Data Factory hizmetinde yayımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1df04-272">In this step, you publish the Data Factory entities (linked services, datasets, and pipeline) in your project to the Azure Data Factory service.</span></span> <span data-ttu-id="1df04-273">Yayımlama sürecinde, veri fabrikanızın adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="1df04-273">In the process of publishing, you specify the name for your data factory.</span></span> 

1. <span data-ttu-id="1df04-274">Çözüm Gezgini’nde projeye sağ tıklayın ve ardından **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-274">Right-click project in the Solution Explorer, and click **Publish**.</span></span>
2. <span data-ttu-id="1df04-275">**Microsoft hesabınızda oturum açın** iletişim kutusunu görmezseniz, Azure aboneliğindeki kimlik bilgilerini hesap için girin ve **oturum aç**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-275">If you see **Sign in to your Microsoft account** dialog box, enter your credentials for the account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="1df04-276">Aşağıdaki iletişim kutusunu göreceksiniz:</span><span class="sxs-lookup"><span data-stu-id="1df04-276">You should see the following dialog box:</span></span>

   ![Yayımla iletişim kutusu](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. <span data-ttu-id="1df04-278">**Data Factory’yi yapılandırma** sayfasında aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="1df04-278">In the **Configure data factory** page, do the following steps:</span></span>

    ![Yayımlama - Yeni veri fabrikası ayarları](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. <span data-ttu-id="1df04-280">**Yeni Data Factory Oluştur** seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="1df04-280">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="1df04-281">Data factory için benzersiz bir **ad** girin.</span><span class="sxs-lookup"><span data-stu-id="1df04-281">Enter a unique **name** for the data factory.</span></span> <span data-ttu-id="1df04-282">Örneğin: **DataFactoryUsingVS09152016**.</span><span class="sxs-lookup"><span data-stu-id="1df04-282">For example: **DataFactoryUsingVS09152016**.</span></span> <span data-ttu-id="1df04-283">Adın genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1df04-283">The name must be globally unique.</span></span>
   3. <span data-ttu-id="1df04-284">**Abonelik** alanı için doğru abonelik seçin.</span><span class="sxs-lookup"><span data-stu-id="1df04-284">Select the right subscription for the **Subscription** field.</span></span> 
        > [!IMPORTANT]
        > <span data-ttu-id="1df04-285">Herhangi bir abonelik görmüyorsanız aboneliğin yöneticisi veya ortak yöneticisi olan bir hesapla oturum açtığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1df04-285">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of the subscription.</span></span>
   4. <span data-ttu-id="1df04-286">oluşturulacak data factory için **kaynak grubu** seçin.</span><span class="sxs-lookup"><span data-stu-id="1df04-286">Select the **resource group** for the data factory to be created.</span></span>
   5. <span data-ttu-id="1df04-287">Data factory için **bölge** seçin.</span><span class="sxs-lookup"><span data-stu-id="1df04-287">Select the **region** for the data factory.</span></span>
   6. <span data-ttu-id="1df04-288">**Öğeleri Yayımla** sayfasına geçmek için **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-288">Click **Next** to switch to the **Publish Items** page.</span></span> <span data-ttu-id="1df04-289">(Ad alanından çıkmak için, **İleri** düğmesi devre dışıysa **SEKME** tuşuna basın.)</span><span class="sxs-lookup"><span data-stu-id="1df04-289">(Press **TAB** to move out of the Name field to if the **Next** button is disabled.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="1df04-290">Yayımladığınızda **“DataFactoryUsingVS” data factory adı yok** hatasını alırsanız adı değiştirin (örneğin, yournameDataFactoryUsingVS).</span><span class="sxs-lookup"><span data-stu-id="1df04-290">If you receive the error **Data factory name “DataFactoryUsingVS” is not available** when publishing, change the name (for example, yournameDataFactoryUsingVS).</span></span> <span data-ttu-id="1df04-291">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="1df04-291">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
1. <span data-ttu-id="1df04-292">**Öğeleri Yayımla** sayfasında tüm Data Factory varlıklarının işaretli olmasını sağlayın ve **Özet** sayfasına geçmek için **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-292">In the **Publish Items** page, ensure that all the Data Factories entities are selected, and click **Next** to switch to the **Summary** page.</span></span>

    ![Öğe yayımlama sayfası](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. <span data-ttu-id="1df04-294">Özeti gözden geçirin, dağıtım işlemini başlatmak ve **Dağıtım Durumu**’nu görüntülemek için **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-294">Review the summary and click **Next** to start the deployment process and view the **Deployment Status**.</span></span>

    ![Özet sayfası](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. <span data-ttu-id="1df04-296">**Dağıtım Durumu** sayfasında dağıtım sürecinin durumunu görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-296">In the **Deployment Status** page, you should see the status of the deployment process.</span></span> <span data-ttu-id="1df04-297">Dağıtımını gerçekleştirdikten sonra Son'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-297">Click Finish after the deployment is done.</span></span>

<span data-ttu-id="1df04-298">Dikkat edilmesi gereken önemli noktalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1df04-298">Important points to note:</span></span>

- <span data-ttu-id="1df04-299">**Abonelik, Microsoft.DataFactory ad alanını kullanacak şekilde kaydedilmemiş** hatasını alırsanız, aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:</span><span class="sxs-lookup"><span data-stu-id="1df04-299">If you receive the error: **This subscription is not registered to use namespace Microsoft.DataFactory**, do one of the following and try publishing again:</span></span>
    - <span data-ttu-id="1df04-300">Azure PowerShell’de Data Factory sağlayıcısını kaydetmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1df04-300">In Azure PowerShell, run the following command to register the Data Factory provider.</span></span>
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        <span data-ttu-id="1df04-301">Data Factory sağlayıcısının kayıtlı olduğunu onaylamak için aşağıdaki komutu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-301">You can run the following command to confirm that the Data Factory provider is registered.</span></span>

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - <span data-ttu-id="1df04-302">Azure aboneliğini kullanarak [Azure portalında](https://portal.azure.com) oturum açın ve Data Factory dikey penceresine gidin (ya da) Azure portalında bir data factory oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1df04-302">Login using the Azure subscription in to the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="1df04-303">Bu eylem sağlayıcıyı sizin için otomatik olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="1df04-303">This action automatically registers the provider for you.</span></span>
- <span data-ttu-id="1df04-304">Data factory adı gelecekte bir DNS adı olarak kaydedilmiş olabilir; bu nedenle herkese görünür hale gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="1df04-304">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>
- <span data-ttu-id="1df04-305">Data Factory örnekleri oluşturmak için Azure aboneliğinde yönetici veya ortak yönetici olmanız gerekir</span><span class="sxs-lookup"><span data-stu-id="1df04-305">To create Data Factory instances, you need to be an admin or co-admin of the Azure subscription</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="1df04-306">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="1df04-306">Monitor pipeline</span></span>
<span data-ttu-id="1df04-307">Bu adımda, veri fabrikasının Diyagram Görünümünü kullanarak işlem hattını izleyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-307">In this step, you monitor the pipeline using Diagram View of the data factory.</span></span> 

#### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="1df04-308">Diyagram Görünümünü kullanarak işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="1df04-308">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="1df04-309">[Azure portalında](https://portal.azure.com/) oturum açıp aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="1df04-309">Log in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>
   1. <span data-ttu-id="1df04-310">**Diğer hizmetler** ve **Data factory’ler** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-310">Click **More services** and click **Data factories**.</span></span>
       
        ![Data factory’lere göz atma](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. <span data-ttu-id="1df04-312">Veri fabrikası listesinden veri fabrikanızın adını seçin (örneğin: **DataFactoryUsingVS09152016**).</span><span class="sxs-lookup"><span data-stu-id="1df04-312">Select the name of your data factory (for example: **DataFactoryUsingVS09152016**) from the list of data factories.</span></span>
   
       ![Data factory’nizi seçme](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. <span data-ttu-id="1df04-314">Veri fabrikanızın giriş sayfasında penceresinde **Diyagram**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-314">In the home page for your data factory, click **Diagram**.</span></span>

    ![Diyagram kutucuğu](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. <span data-ttu-id="1df04-316">Diyagram Görünümü’nde, işlem hatlarına ve bu öğreticide kullanılan veri kümelerine bir genel bakış görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1df04-316">In the Diagram View, you see an overview of the pipelines, and datasets used in this tutorial.</span></span>

    ![Diyagram Görünümü](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. <span data-ttu-id="1df04-318">İşlem hattındaki tüm etkinlikleri görüntülemek için diyagramdaki işlem hattına sağ tıklayın ve Açık İşlem Hattı’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-318">To view all activities in the pipeline, right-click pipeline in the diagram and click Open Pipeline.</span></span>

    ![İşlem hattı menüsünü açma](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. <span data-ttu-id="1df04-320">İşlem hattında HDInsightHive etkinliğini gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-320">Confirm that you see the HDInsightHive activity in the pipeline.</span></span>

    ![İşlem hattı görünümünü açma](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    <span data-ttu-id="1df04-322">Önceki görünüme dönmek için en üstteki içerik haritası menüsünde **Data factory**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-322">To navigate back to the previous view, click **Data factory** in the breadcrumb menu at the top.</span></span>
6. <span data-ttu-id="1df04-323">**Diyagram Görünümü**’nde **AzureBlobInput** veri kümesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-323">In the **Diagram View**, double-click the dataset **AzureBlobInput**.</span></span> <span data-ttu-id="1df04-324">Dilimin **Hazır** durumunda olduğunu onaylayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-324">Confirm that the slice is in **Ready** state.</span></span> <span data-ttu-id="1df04-325">Dilimin Hazır durumda gösterilmesi birkaç dakika alabilir.</span><span class="sxs-lookup"><span data-stu-id="1df04-325">It may take a couple of minutes for the slice to show up in Ready state.</span></span> <span data-ttu-id="1df04-326">Bir süre bekledikten sonra bu gerçekleşmiyorsa, girdi dosyasının (input.log) doğru kapsayıcıda (`adfgetstarted`) ve klasörde (`inputdata`) olup olmadığına bakın.</span><span class="sxs-lookup"><span data-stu-id="1df04-326">If it does not happen after you wait for sometime, see if you have the input file (input.log) placed in the right container (`adfgetstarted`) and folder (`inputdata`).</span></span> <span data-ttu-id="1df04-327">Ayrıca, giriş veri kümesindeki **external** özelliğinin **true** olarak ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="1df04-327">And, make sure that the **external** property on the input dataset is set to **true**.</span></span> 

   ![Girdi dilimi hazır durumda](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. <span data-ttu-id="1df04-329">**AzureBlobInput** dikey penceresini kapatmak için **X** işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-329">Click **X** to close **AzureBlobInput** blade.</span></span>
8. <span data-ttu-id="1df04-330">**Diyagram Görünümü**’nde **AzureBlobOutput** veri kümesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-330">In the **Diagram View**, double-click the dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="1df04-331">Dilimin işlenmekte olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1df04-331">You see that the slice that is currently being processed.</span></span>

   ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. <span data-ttu-id="1df04-333">İşlem tamamlandığında dilimi **Hazır** durumunda görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1df04-333">When processing is done, you see the slice in **Ready** state.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1df04-334">İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika).</span><span class="sxs-lookup"><span data-stu-id="1df04-334">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="1df04-335">Bu nedenle, işlem hattının dilimi işlemesi için **yaklaşık 30 dakika** bekleyin.</span><span class="sxs-lookup"><span data-stu-id="1df04-335">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>  
   
    ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. <span data-ttu-id="1df04-337">Dilim **Hazır** durumunda olduğunda çıktı verileri için blob depolama alanınızın `adfgetstarted` kapsayıcısında `partitioneddata` klasörünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="1df04-337">When the slice is in **Ready** state, check the `partitioneddata` folder in the `adfgetstarted` container in your blob storage for the output data.</span></span>  

    ![çıktı verileri](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. <span data-ttu-id="1df04-339">Dilimin ayrıntılarını bir **Veri dilimi** dikey penceresinde görmek için dilime tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-339">Click the slice to see details about it in a **Data slice** blade.</span></span>

    ![Veri dilimi ayrıntıları](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. <span data-ttu-id="1df04-341">Bir etkinlik çalışmasına ilişkin ayrıntıları (bu senaryoda Hive etkinliği) bir **Etkinlik çalışma ayrıntıları** penceresinde görmek için **Etkinlik çalışma listesi** içinden bir etkinlik çalışmasına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-341">Click an activity run in the **Activity runs list** to see details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span> 
  
    ![Etkinlik çalışma ayrıntıları](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    <span data-ttu-id="1df04-343">Yürütülen Hive sorgusunu ve durum bilgilerini günlük dosyalarında görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-343">From the log files, you can see the Hive query that was executed and status information.</span></span> <span data-ttu-id="1df04-344">Bu günlükler her türlü sorunu gidermek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="1df04-344">These logs are useful for troubleshooting any issues.</span></span>  

<span data-ttu-id="1df04-345">Bu öğreticide oluşturduğunuz işlem hattını ve veri kümelerini izlemek üzere Azure Portal’ın ilişkin yönergeler için bkz. [Veri kümelerini ve işlem hatlarını izleme](data-factory-monitor-manage-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="1df04-345">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how to use the Azure portal to monitor the pipeline and datasets you have created in this tutorial.</span></span>

#### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="1df04-346">İzleme ve Yönetme Uygulamasını kullanarak işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="1df04-346">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="1df04-347">İşlem hatlarınızı izlemek için İzleme ve Yönetme uygulamasını da kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-347">You can also use Monitor & Manage application to monitor your pipelines.</span></span> <span data-ttu-id="1df04-348">Bu uygulamanın kullanımına ilişkin ayrıntılı bilgi için bkz. [İzleme ve Yönetme Uygulamasını kullanarak Azure Data Factory işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="1df04-348">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="1df04-349">İzleme ve Yönetme kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-349">Click Monitor & Manage tile.</span></span>

    ![İzleme ve Yönetme kutucuğu](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. <span data-ttu-id="1df04-351">İzleme ve Yönetme uygulamasını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1df04-351">You should see Monitor & Manage application.</span></span> <span data-ttu-id="1df04-352">**Başlangıç saati** ve **Bitiş saati** değerlerini işlem hattınızın başlangıç (04-01-2016 12:00 AM) ve bitiş saatleri (04-02-2016 12:00 AM) ile eşleşecek şekilde değiştirin ve **Uygula**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-352">Change the **Start time** and **End time** to match start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span></span>

    ![İzleme ve Yönetme Uygulaması](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. <span data-ttu-id="1df04-354">Bir etkinlik penceresinin ayrıntılarını görmek için **Etkinlik Pencereleri listesinden** seçim yapın.</span><span class="sxs-lookup"><span data-stu-id="1df04-354">To see details about an activity window, select it in the **Activity Windows list** to see details about it.</span></span>
    <span data-ttu-id="1df04-355">![Etkinlik penceresi ayrıntıları](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="1df04-355">![Activity window details](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1df04-356">Dilim başarıyla işlendiğinde girdi dosyası silinir.</span><span class="sxs-lookup"><span data-stu-id="1df04-356">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="1df04-357">Bu nedenle, dilimi yeniden çalıştırmak veya öğreticiyi yeniden uygulamak isterseniz girdi dosyasını (input.log) `adfgetstarted` kapsayıcısının `inputdata` klasörüne yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1df04-357">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the `inputdata` folder of the `adfgetstarted` container.</span></span>

### <a name="additional-notes"></a><span data-ttu-id="1df04-358">Ek notlar</span><span class="sxs-lookup"><span data-stu-id="1df04-358">Additional notes</span></span>
- <span data-ttu-id="1df04-359">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1df04-359">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="1df04-360">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="1df04-360">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="1df04-361">Örneğin, bir kaynaktan hedef veri deposuna veri kopyalama amaçlı bir Kopyalama Etkinliği ve giriş verilerini dönüştürmek üzere Hive betiği çalıştırma amaçlı bir HDInsight Hive etkinliği.</span><span class="sxs-lookup"><span data-stu-id="1df04-361">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data.</span></span> <span data-ttu-id="1df04-362">Kopyalama Etkinliği tarafından desteklenen tüm kaynaklar ve havuzlar için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1df04-362">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="1df04-363">Data Factory tarafından desteklenen işlem hizmetlerinin listesi için bkz. [bağlantılı işlem hizmetleri](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="1df04-363">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory.</span></span>
- <span data-ttu-id="1df04-364">Bağlı hizmetler veri depolarını veya işlem hizmetlerini Azure data factory’ye bağlar.</span><span class="sxs-lookup"><span data-stu-id="1df04-364">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="1df04-365">Kopyalama Etkinliği tarafından desteklenen tüm kaynaklar ve havuzlar için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1df04-365">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all the sources and sinks supported by the Copy Activity.</span></span> <span data-ttu-id="1df04-366">Data Factory tarafından desteklenen işlem hizmetlerinin listesi ve bunlar üzerinde çalışabilecek [dönüşüm etkinlikleri](data-factory-data-transformation-activities.md) için [işlem bağlı hizmetleri](data-factory-compute-linked-services.md) bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="1df04-366">See [compute linked services](data-factory-compute-linked-services.md) for the list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span></span>
- <span data-ttu-id="1df04-367">Azure Depolama bağlı hizmet tanımında kullanılan JSON özellikleri hakkında ayrıntılı bilgi için bkz. [Azure Blob’a/Blob’dan veri taşıma](data-factory-azure-blob-connector.md#azure-storage-linked-service).</span><span class="sxs-lookup"><span data-stu-id="1df04-367">See [Move data from/to Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in the Azure Storage linked service definition.</span></span>
- <span data-ttu-id="1df04-368">İsteğe bağlı HDInsight kümesi yerine kendi HDInsight kümenizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-368">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="1df04-369">Ayrıntılar için bkz. [İşlem Bağlı Hizmetleri](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="1df04-369">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>
-  <span data-ttu-id="1df04-370">Data Factory, sizin için önceki JSON ile **Linux tabanlı** bir HDInsight kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1df04-370">The Data Factory creates a **Linux-based** HDInsight cluster for you with the preceding JSON.</span></span> <span data-ttu-id="1df04-371">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="1df04-371">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
- <span data-ttu-id="1df04-372">HDInsight kümesi JSON’da belirttiğiniz blob depolamada (linkedServiceName) bir **varsayılan kapsayıcı** oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1df04-372">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (linkedServiceName).</span></span> <span data-ttu-id="1df04-373">HDInsight, küme silindiğinde bu kapsayıcıyı silmez.</span><span class="sxs-lookup"><span data-stu-id="1df04-373">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="1df04-374">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="1df04-374">This behavior is by design.</span></span> <span data-ttu-id="1df04-375">İsteğe bağlı HDInsight bağlı hizmeti kullanıldığında, mevcut canlı bir küme olmadığı sürece bir dilim her işlendiğinde bir HDInsight kümesi oluşturulur (timeToLive).</span><span class="sxs-lookup"><span data-stu-id="1df04-375">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="1df04-376">Küme, işlem tamamlandığında otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="1df04-376">The cluster is automatically deleted when the processing is done.</span></span>
    
    <span data-ttu-id="1df04-377">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1df04-377">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="1df04-378">İşlerin sorunları giderilmesi için bunlara gerek yoksa, depolama maliyetini azaltmak için bunları silmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-378">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="1df04-379">Bu kapsayıcı adları bir düzene sahiptir: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="1df04-379">The names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="1df04-380">Azure blob depolamada kapsayıcı silmek için [Microsoft Storage Gezgini](http://storageexplorer.com/) gibi araçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="1df04-380">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>
- <span data-ttu-id="1df04-381">Şu anda, çıktı veri kümesi zamanlamayı yönetendir; bu nedenle etkinlik hiçbir çıktı oluşturmasa bile sizin bir çıktı veri kümesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1df04-381">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="1df04-382">Etkinlik herhangi bir girdi almazsa, girdi veri kümesi oluşturma işlemini atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-382">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> 
- <span data-ttu-id="1df04-383">Bu öğreticide, Azure Data Factory kullanarak verilerin nasıl kopyalanacağı gösterilmemektedir.</span><span class="sxs-lookup"><span data-stu-id="1df04-383">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="1df04-384">Azure Data Factory kullanarak verileri kopyalama öğreticisi için bkz. [Öğretici: Blob Depolama’dan SQL Veritabanı’na veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1df04-384">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>


## <a name="use-server-explorer-to-view-data-factories"></a><span data-ttu-id="1df04-385">Data factory’leri görüntülemek için Sunucu Gezgini’ni kullanın</span><span class="sxs-lookup"><span data-stu-id="1df04-385">Use Server Explorer to view data factories</span></span>
1. <span data-ttu-id="1df04-386">**Visual Studio**’nun menüsünde **Görünüm**’e ve **Sunucu Gezgini**’ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-386">In **Visual Studio**, click **View** on the menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="1df04-387">Sunucu Gezgini penceresinde, **Azure**’ü ve **Data Factory**’yi genişletin.</span><span class="sxs-lookup"><span data-stu-id="1df04-387">In the Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="1df04-388">**Visual Studio'da oturum açın**’ı görürseniz Azure aboneliğiyle ilişkili **hesabı** girin ve **Devam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-388">If you see **Sign in to Visual Studio**, enter the **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="1df04-389">**parola** girip **Oturum aç**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-389">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="1df04-390">Visual Studio, aboneliğinizdeki tüm Azure data factory’leri hakkında bilgi almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="1df04-390">Visual Studio tries to get information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="1df04-391">Bu işlemin durumunu **Data Factory Görev Listesi** penceresinde görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1df04-391">You see the status of this operation in the **Data Factory Task List** window.</span></span>

    ![Sunucu Gezgini](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. <span data-ttu-id="1df04-393">İstediğiniz data factory’ye sağ tıklayıp, mevcut bir data factory’ye dayandırılan Visual Studio projesi oluşturmak için **Data Factory’yi Yeni Projeye Aktar**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="1df04-393">You can right-click a data factory, and select **Export Data Factory to New Project** to create a Visual Studio project based on an existing data factory.</span></span>

    ![Data factory’yi dışarı aktarma](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="1df04-395">Visual Studio için Data Factory araçlarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="1df04-395">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="1df04-396">Visual Studio için Azure Data Factory araçlarını güncelleştirmek üzere aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="1df04-396">To update Azure Data Factory tools for Visual Studio, do the following steps:</span></span>

1. <span data-ttu-id="1df04-397">Menüde **Araçlar**’a tıklayın ve **Uzantılar ve Güncelleştirmeler**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="1df04-397">Click **Tools** on the menu and select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="1df04-398">Sol bölmede **Güncelleştirmeler**’i, sonra da **Visual Studio Galerisi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="1df04-398">Select **Updates** in the left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="1df04-399">**Visual Studio için Azure Data Factory araçları**’nı seçin ve **Güncelleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-399">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="1df04-400">Bu girişi görmüyorsanız araçların en son sürümü zaten yüklüdür.</span><span class="sxs-lookup"><span data-stu-id="1df04-400">If you do not see this entry, you already have the latest version of the tools.</span></span>

## <a name="use-configuration-files"></a><span data-ttu-id="1df04-401">Yapılandırma dosyalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="1df04-401">Use configuration files</span></span>
<span data-ttu-id="1df04-402">Visual Studio'da bağlı hizmetler/tablolar/işlem hatları için her ortamda farklı özellik yapılandırmak amacıyla yapılandırma dosyalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-402">You can use configuration files in Visual Studio to configure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="1df04-403">Azure Storage bağlı hizmeti için aşağıdaki JSON tanımını dikkate alın.</span><span class="sxs-lookup"><span data-stu-id="1df04-403">Consider the following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="1df04-404">Data Factory varlıklarını dağıttığınız ortama dayanan accountname ve accountkey farklı değerlerini (Dev/Test/Production) **connectionString** olarak belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="1df04-404">To specify **connectionString** with different values for accountname and accountkey based on the environment (Dev/Test/Production) to which you are deploying Data Factory entities.</span></span> <span data-ttu-id="1df04-405">Her ortam için ayrı bir yapılandırma dosyası kullanarak bu davranışı elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-405">You can achieve this behavior by using separate configuration file for each environment.</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "description": "",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

### <a name="add-a-configuration-file"></a><span data-ttu-id="1df04-406">Yapılandırma dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="1df04-406">Add a configuration file</span></span>
<span data-ttu-id="1df04-407">Aşağıdaki adımları uygulayarak her ortam için bir yapılandırma dosyası ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1df04-407">Add a configuration file for each environment by performing the following steps:</span></span>   

1. <span data-ttu-id="1df04-408">Visual Studio çözümünüzde Data Factory projenize sağ tıklayın, **Ekle**’nin üzerine gelin ve **Yeni öğe**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-408">Right-click the Data Factory project in your Visual Studio solution, point to **Add**, and click **New item**.</span></span>
2. <span data-ttu-id="1df04-409">Soldaki yüklenmiş şablonlar listesinden **Config**’i ve **Yapılandırma Dosyası**’nı seçin ve yapılandırma dosyası için bir **ad** girip **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-409">Select **Config** from the list of installed templates on the left, select **Configuration File**, enter a **name** for the configuration file, and click **Add**.</span></span>

    ![Yapılandırma dosyasını ekleme](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="1df04-411">Yapılandırma parametrelerini ve değerlerini aşağıda gösterilen biçimde ekleyin:</span><span class="sxs-lookup"><span data-stu-id="1df04-411">Add configuration parameters and their values in the following format:</span></span>

    ```json
    {
        "$schema": "http://datafactories.schema.management.azure.com/vsschemas/V1/Microsoft.DataFactory.Config.json",
        "AzureStorageLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        ],
        "AzureSqlLinkedService1": [
            {
                "name": "$.properties.typeProperties.connectionString",
                "value":  "Server=tcp:spsqlserver.database.windows.net,1433;Database=spsqldb;User ID=spelluru;Password=Sowmya123;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        ]
    }
    ```

    <span data-ttu-id="1df04-412">Bu örnek, Azure Storage bağlı hizmetinin ve Azure SQL bağlı hizmetinin connectionString özelliğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="1df04-412">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="1df04-413">Belirtilen adın sözdiziminin [JsonPath](http://goessner.net/articles/JsonPath/) olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="1df04-413">Notice that the syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="1df04-414">JSON’un aşağıdaki kodda gösterilen şekilde bir dizi değere sahip bir özelliği varsa:</span><span class="sxs-lookup"><span data-stu-id="1df04-414">If JSON has a property that has an array of values as shown in the following code:</span></span>  

    ```json
    "structure": [
          {
              "name": "FirstName",
            "type": "String"
          },
          {
            "name": "LastName",
            "type": "String"
        }
    ],
    ```

    <span data-ttu-id="1df04-415">Özellikleri, aşağıdaki yapılandırma dosyasında gösterildiği gibi (sıfır tabanlı dizin oluşturma kullanın) yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="1df04-415">Configure properties as shown in the following configuration file (use zero-based indexing):</span></span>

    ```json
    {
        "name": "$.properties.structure[0].name",
        "value": "FirstName"
    }
    {
        "name": "$.properties.structure[0].type",
        "value": "String"
    }
    {
        "name": "$.properties.structure[1].name",
        "value": "LastName"
    }
    {
        "name": "$.properties.structure[1].type",
        "value": "String"
    }
    ```

### <a name="property-names-with-spaces"></a><span data-ttu-id="1df04-416">Boşluklu özellik adları</span><span class="sxs-lookup"><span data-stu-id="1df04-416">Property names with spaces</span></span>
<span data-ttu-id="1df04-417">Özellik adında boşluklar varsa, aşağıdaki örnekte (veritabanı sunucu adı) gösterildiği gibi köşeli ayraç kullanın:</span><span class="sxs-lookup"><span data-stu-id="1df04-417">If a property name has spaces in it, use square brackets as shown in the following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="1df04-418">Yapılandırma kullanarak çözümü dağıtma</span><span class="sxs-lookup"><span data-stu-id="1df04-418">Deploy solution using a configuration</span></span>
<span data-ttu-id="1df04-419">Azure Data Factory varlıklarını VS’de dağıttığınızda, bu yayımlama işlemi için kullanmak istediğiniz yapılandırmayı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-419">When you are publishing Azure Data Factory entities in VS, you can specify the configuration that you want to use for that publishing operation.</span></span>

<span data-ttu-id="1df04-420">Azure Data Factory projesindeki varlıkları yapılandırma dosyası kullanarak oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="1df04-420">To publish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="1df04-421">Data Factory projesine sağ tıklayıp, **Öğeleri Yayımla** iletişim kutusunu görüntülemek için **Yayımla**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-421">Right-click Data Factory project and click **Publish** to see the **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="1df04-422">Mevcut bir data factory seçip ya da **Data factory yapılandır** sayfasında bir data factory oluşturulması için değerleri belirtip **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-422">Select an existing data factory or specify values for creating a data factory on the **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="1df04-423">**Öğeleri Yayımla** sayfasında: **Dağıtım Yapılandırması seç** alanı için kullanılabilir yapılandırmaların açılan listesini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1df04-423">On the **Publish Items** page: you see a drop-down list with available configurations for the **Select Deployment Config** field.</span></span>

    ![Yapılandırma dosyası seçme](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="1df04-425">Kullanmak istediğiniz **yapılandırma dosyasını** seçip **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-425">Select the **configuration file** that you would like to use and click **Next**.</span></span>
5. <span data-ttu-id="1df04-426">**Özet** sayfasında JSON dosyasının adını gördüğünüzü doğrulayıp **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-426">Confirm that you see the name of JSON file in the **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="1df04-427">Dağıtım işlemi sona erdikten sonra **Son**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1df04-427">Click **Finish** after the deployment operation is finished.</span></span>

<span data-ttu-id="1df04-428">Dağıtımı yaptığınızda, yapılandırma dosyasındaki değerler, varlıkların Azure Data Factory hizmetine dağıtılmasından önce JSON dosyalarındaki özelliklerin değerlerini ayarlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1df04-428">When you deploy, the values from the configuration file are used to set values for properties in the JSON files before the entities are deployed to Azure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="1df04-429">Azure Key Vault kullanma</span><span class="sxs-lookup"><span data-stu-id="1df04-429">Use Azure Key Vault</span></span>
<span data-ttu-id="1df04-430">Bağlantı dizeleri gibi hassas verilerin kod deposuna işlenmesi önerilmez ve genellikle güvenlik ilkesine aykırıdır.</span><span class="sxs-lookup"><span data-stu-id="1df04-430">It is not advisable and often against security policy to commit sensitive data such as connection strings to the code repository.</span></span> <span data-ttu-id="1df04-431">Hassas bilgileri Azure Key Vault’ta depolama ve Data Factory varlıklarını yayımlarken bu bilgileri kullanma hakkında bilgi için, GitHub üzerinde [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="1df04-431">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub to learn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="1df04-432">Visual Studio için Secure Publish uzantısı, gizli anahtarların Key Vault’ta depolanmasına olanak tanır ve bağlı hizmetler/ dağıtım yapılandırmalarında bunların yalnızca başvuruları belirtilir.</span><span class="sxs-lookup"><span data-stu-id="1df04-432">The Secure Publish extension for Visual Studio allows the secrets to be stored in Key Vault and only references to them are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="1df04-433">Bu başvurular, Azure’da Data Factory varlıkları yayımladığınızda çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="1df04-433">These references are resolved when you publish Data Factory entities to Azure.</span></span> <span data-ttu-id="1df04-434">Bu dosyalar daha sonra herhangi bir gizli anahtar kullanıma sunulmadan kaynak depoya işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="1df04-434">These files can then be committed to source repository without exposing any secrets.</span></span>

## <a name="summary"></a><span data-ttu-id="1df04-435">Özet</span><span class="sxs-lookup"><span data-stu-id="1df04-435">Summary</span></span>
<span data-ttu-id="1df04-436">Bu öğreticide, HDInsight hadoop kümesindeki Hive betiği çalıştırılarak verileri işlemek için bir Azure data factory oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="1df04-436">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="1df04-437">Aşağıdaki adımları uygulamak için Azure Portal’da Data Factory Düzenleyici’yi kullandınız:</span><span class="sxs-lookup"><span data-stu-id="1df04-437">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>  

1. <span data-ttu-id="1df04-438">Oluşturulan Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="1df04-438">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="1df04-439">Oluşturulan iki **bağlı hizmet**:</span><span class="sxs-lookup"><span data-stu-id="1df04-439">Created two **linked services**:</span></span>
   1. <span data-ttu-id="1df04-440">Girdi/çıktı dosyalarını tutan Azure blob depolamanızı data factory’ye bağlamak için **Azure Storage** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="1df04-440">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="1df04-441">İsteğe bağlı HDInsight Hadoop kümesini data factory’ye bağlamak için isteğe bağlı **Azure HDInsight** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="1df04-441">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="1df04-442">Azure Data Factory, girdi verilerini işlemek, çıktı verilerini de oluşturmak için tam zamanında HDInsight Hadoop kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1df04-442">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="1df04-443">İşlem hattındaki HDInsight Hive etkinliğiyle ilgili girdi ve çıktı verilerini açıklayan oluşturulan iki **veri kümesi**.</span><span class="sxs-lookup"><span data-stu-id="1df04-443">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="1df04-444">**HDInsight Hive** etkinliğine sahip oluşturulan bir **işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="1df04-444">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1df04-445">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="1df04-445">Next Steps</span></span>
<span data-ttu-id="1df04-446">Bu makalede, isteğe bağlı HDInsight kümesinde bir Hive betiği çalıştıran dönüştürme etkinliğine (HDInsight Etkinliği) sahip işlem hattı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="1df04-446">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="1df04-447">Verileri Azure Blob’tan Azure SQL’e kopyalamak için Kopyalama Etkinliği’nin kullanılması hakkında bilgi için bkz. [Öğretici: Verileri Azure blob’tan Azure SQL’e kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1df04-447">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="1df04-448">Bir etkinliğin çıkış veri kümesini diğer etkinliğin giriş veri kümesi olarak ayarlayarak iki etkinliği zincirleyebilir, yani bir etkinliği diğerinden sonra çalıştırılmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1df04-448">You can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="1df04-449">Ayrıntılı bilgi için bkz. [Data Factory’de zamanlama ve yürütme](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="1df04-449">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 


## <a name="see-also"></a><span data-ttu-id="1df04-450">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1df04-450">See Also</span></span>
| <span data-ttu-id="1df04-451">Konu</span><span class="sxs-lookup"><span data-stu-id="1df04-451">Topic</span></span> | <span data-ttu-id="1df04-452">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1df04-452">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="1df04-453">İşlem hatları</span><span class="sxs-lookup"><span data-stu-id="1df04-453">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="1df04-454">Bu makale, Azure Data Factory’de işlem hatlarını ve etkinlikleri anlamanıza, senaryonuz ya da işletmeniz için veri odaklı iş akışları oluşturmak amacıyla bunları nasıl kullanacağınızı öğrenmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1df04-454">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="1df04-455">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="1df04-455">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="1df04-456">Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1df04-456">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="1df04-457">Veri Dönüştürme Etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="1df04-457">Data Transformation Activities</span></span>](data-factory-data-transformation-activities.md) |<span data-ttu-id="1df04-458">Bu makalede, Azure Data Factory’nin desteklediği veri dönüştürme etkinliklerinin (bu öğreticide kullandığınız HDInsight Hive dönüştürmesi gibi) bir listesi sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1df04-458">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span></span> |
| [<span data-ttu-id="1df04-459">Zamanlama ve yürütme</span><span class="sxs-lookup"><span data-stu-id="1df04-459">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="1df04-460">Bu makalede Azure Data Factory uygulama modelinin zamanlama ve yürütme yönleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1df04-460">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="1df04-461">İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="1df04-461">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="1df04-462">Bu makalede İzleme ve Yönetim Uygulaması kullanılarak işlem hatlarını izleme, yönetme ve hatalarını ayıklama işlemleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1df04-462">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
