---
title: aaaBuild ilk data factory'nizi (Visual Studio) | Microsoft Docs
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
ms.openlocfilehash: 0c5eb01b685d978d80916da0293cc2d3701b2d57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-by-using-visual-studio"></a><span data-ttu-id="e658c-103">Öğretici: Visual Studio kullanarak veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="e658c-103">Tutorial: Create a data factory by using Visual Studio</span></span>
> [!div class="op_single_selector" title="Tools/SDKs"]
> * [<span data-ttu-id="e658c-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e658c-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="e658c-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="e658c-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="e658c-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e658c-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="e658c-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e658c-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="e658c-108">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="e658c-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="e658c-109">REST API</span><span class="sxs-lookup"><span data-stu-id="e658c-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)

<span data-ttu-id="e658c-110">Bu öğretici şunların nasıl yapıldığını gösterir toocreate Visual Studio kullanarak Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="e658c-110">This tutorial shows you how toocreate an Azure data factory by using Visual Studio.</span></span> <span data-ttu-id="e658c-111">Hello Data Factory proje şablonunu kullanarak bir Visual Studio projesi oluşturmak, Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) JSON biçiminde tanımlayın ve yayımlama/bu varlıkları toohello bulut dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="e658c-111">You create a Visual Studio project using hello Data Factory project template, define Data Factory entities (linked services, datasets, and pipeline) in JSON format, and then publish/deploy these entities toohello cloud.</span></span> 

<span data-ttu-id="e658c-112">Bu öğreticide Hello ardışık bir etkinlik vardır: **Hdınsight Hive etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="e658c-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="e658c-113">Bu etkinlik dönüşümler veri tooproduce çıkış veri girişi bir Azure Hdınsight kümesinde bir hive betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="e658c-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="e658c-114">Başlangıç ve bitiş zamanlarını hello arasında bir ay belirtilen sonra hello ardışık düzen zamanlanmış toorun ' dir.</span><span class="sxs-lookup"><span data-stu-id="e658c-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="e658c-115">Bu öğreticide, Azure Data Factory kullanarak verilerin nasıl kopyalanacağı gösterilmemektedir.</span><span class="sxs-lookup"><span data-stu-id="e658c-115">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="e658c-116">Nasıl bir öğretici için Azure Data Factory kullanarak toocopy verileri görmek [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="e658c-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="e658c-117">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="e658c-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="e658c-118">Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="e658c-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="e658c-119">Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="e658c-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>


## <a name="walkthrough-create-and-publish-data-factory-entities"></a><span data-ttu-id="e658c-120">İzlenecek Yol: Data Factory varlıkları oluşturma ve yayımlama</span><span class="sxs-lookup"><span data-stu-id="e658c-120">Walkthrough: Create and publish Data Factory entities</span></span>
<span data-ttu-id="e658c-121">Bu kılavuz kapsamında gerçekleştirme hello adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="e658c-121">Here are hello steps you perform as part of this walkthrough:</span></span>

1. <span data-ttu-id="e658c-122">İki bağlı hizmet oluşturun: **AzureStorageLinkedService1** ve **HDInsightOnDemandLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="e658c-122">Create two linked services: **AzureStorageLinkedService1** and **HDInsightOnDemandLinkedService1**.</span></span> 
   
    <span data-ttu-id="e658c-123">Bu öğreticide, Hello hive etkinliği içinde için girdi ve çıktı verilerini aynı Azure Blob Storage hello.</span><span class="sxs-lookup"><span data-stu-id="e658c-123">In this tutorial, both input and output data for hello hive activity are in hello same Azure Blob Storage.</span></span> <span data-ttu-id="e658c-124">Bir isteğe bağlı Hdınsight kümesi tooprocess varolan giriş verisi tooproduce çıktı verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="e658c-124">You use an on-demand HDInsight cluster tooprocess existing input data tooproduce output data.</span></span> <span data-ttu-id="e658c-125">Merhaba isteğe bağlı Hdınsight kümesi otomatik olarak sizin için Azure Data Factory'nin hello giriş verisi işlenen hazır toobe olduğunda çalışma zamanında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e658c-125">hello on-demand HDInsight cluster is automatically created for you by Azure Data Factory at run time when hello input data is ready toobe processed.</span></span> <span data-ttu-id="e658c-126">Verilerinizi depolayan veya hello Data Factory hizmeti çalışma zamanında toothem bağlanabilmesi tooyour veri fabrikası hesaplar toolink gerekir.</span><span class="sxs-lookup"><span data-stu-id="e658c-126">You need toolink your data stores or computes tooyour data factory so that hello Data Factory service can connect toothem at runtime.</span></span> <span data-ttu-id="e658c-127">Bu nedenle, hello AzureStorageLinkedService1 kullanarak Azure depolama hesabı toohello veri fabrikanıza bağlamak ve isteğe bağlı Hdınsight kümesi hello HDInsightOnDemandLinkedService1 kullanarak bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e658c-127">Therefore, you link your Azure Storage Account toohello data factory by using hello AzureStorageLinkedService1, and link an on-demand HDInsight cluster by using hello HDInsightOnDemandLinkedService1.</span></span> <span data-ttu-id="e658c-128">Yayımlama sırasında oluşturulan hello veri fabrikası toobe hello adı veya mevcut bir veri fabrikasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="e658c-128">When publishing, you specify hello name for hello data factory toobe created or an existing data factory.</span></span>  
2. <span data-ttu-id="e658c-129">İki veri kümesi oluşturma: **InputDataset** ve **OutputDataset**, hello Azure blob depolamada depolanan hello girdi/çıktı verilerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e658c-129">Create two datasets: **InputDataset** and **OutputDataset**, which represent hello input/output data that is stored in hello Azure blob storage.</span></span> 
   
    <span data-ttu-id="e658c-130">Bu veri kümesi tanımları hello önceki adımda oluşturduğunuz toohello Azure Storage bağlı hizmeti bakın.</span><span class="sxs-lookup"><span data-stu-id="e658c-130">These dataset definitions refer toohello Azure Storage linked service you created in hello previous step.</span></span> <span data-ttu-id="e658c-131">Hello InputDataset için hello blob kapsayıcıda (adfgetstarted) belirtin ve bir blob hello giriş verisi içeren klasörü (inptutdata) hello.</span><span class="sxs-lookup"><span data-stu-id="e658c-131">For hello InputDataset, you specify hello blob container (adfgetstarted) and hello folder (inptutdata) that contains a blob with hello input data.</span></span> <span data-ttu-id="e658c-132">Hello OutputDataset, hello blob kapsayıcıda (adfgetstarted) belirtin ve hello çıktı verilerini tutan hello klasörü (adfgetstarted).</span><span class="sxs-lookup"><span data-stu-id="e658c-132">For hello OutputDataset, you specify hello blob container (adfgetstarted) and hello folder (partitioneddata) that holds hello output data.</span></span> <span data-ttu-id="e658c-133">Yapı, kullanılabilirlik ve ilke gibi diğer özellikleri de belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e658c-133">You also specify other properties such as structure, availability, and policy.</span></span>
3. <span data-ttu-id="e658c-134">**MyFirstPipeline** adlı bir işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e658c-134">Create a pipeline named **MyFirstPipeline**.</span></span> 
  
    <span data-ttu-id="e658c-135">Bu kılavuzda, yalnızca bir etkinlik hello ardışık düzen vardır: **Hdınsight Hive etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="e658c-135">In this walkthrough, hello pipeline has only one activity: **HDInsight Hive Activity**.</span></span> <span data-ttu-id="e658c-136">Bu etkinlik dönüştürme, bir isteğe bağlı Hdınsight kümesinde bir hive betiği çalıştırarak veri tooproduce çıktı verileri girin.</span><span class="sxs-lookup"><span data-stu-id="e658c-136">This activity transform input data tooproduce output data by running a hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="e658c-137">toolearn hive etkinliği hakkında daha fazla bilgi görmek [Hive etkinliği](data-factory-hive-activity.md)</span><span class="sxs-lookup"><span data-stu-id="e658c-137">toolearn more about hive activity, see [Hive Activity](data-factory-hive-activity.md)</span></span> 
4. <span data-ttu-id="e658c-138">**DataFactoryUsingVS** adlı bir veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e658c-138">Create a data factory named **DataFactoryUsingVS**.</span></span> <span data-ttu-id="e658c-139">Merhaba veri fabrikası ve tüm Data Factory varlıkları (bağlı hizmetler, tablolar ve hello ardışık düzeni) dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e658c-139">Deploy hello data factory and all Data Factory entities (linked services, tables, and hello pipeline).</span></span>
5. <span data-ttu-id="e658c-140">Yayımladığınızda, Azure portal dikey penceresi ve izleme ve yönetim uygulaması toomonitor hello ardışık düzen kullanın.</span><span class="sxs-lookup"><span data-stu-id="e658c-140">After you publish, you use Azure portal blades and Monitoring & Management App toomonitor hello pipeline.</span></span> 
  
### <a name="prerequisites"></a><span data-ttu-id="e658c-141">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e658c-141">Prerequisites</span></span>
1. <span data-ttu-id="e658c-142">Okuyun [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md) makale ve tam hello **önkoşul** adımları.</span><span class="sxs-lookup"><span data-stu-id="e658c-142">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span> <span data-ttu-id="e658c-143">Merhaba öğesini de seçebilirsiniz **genel bakış ve önkoşulları** hello üst tooswitch toohello makale hello aşağı açılan listesinde seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e658c-143">You can also select hello **Overview and prerequisites** option in hello drop-down list at hello top tooswitch toohello article.</span></span> <span data-ttu-id="e658c-144">Seçerek geri toothis makale hello önkoşulları tamamladıktan sonra geçiş **Visual Studio** hello aşağı açılan listesinden seçeneği.</span><span class="sxs-lookup"><span data-stu-id="e658c-144">After you complete hello prerequisites, switch back toothis article by selecting **Visual Studio** option in hello drop-down list.</span></span>
2. <span data-ttu-id="e658c-145">toocreate Data Factory örnekleri hello üyesi olmalıdır [veri fabrikası katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello abonelik/kaynak grubu düzeyinde rol.</span><span class="sxs-lookup"><span data-stu-id="e658c-145">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>  
3. <span data-ttu-id="e658c-146">Merhaba aşağıdakilerin yüklü olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="e658c-146">You must have hello following installed on your computer:</span></span>
   * <span data-ttu-id="e658c-147">Visual Studio 2013 veya Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e658c-147">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="e658c-148">Visual Studio 2013 veya Visual Studio 2015 için Azure SDK’sını indirin.</span><span class="sxs-lookup"><span data-stu-id="e658c-148">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="e658c-149">Çok gidin[Azure indirme sayfası](https://azure.microsoft.com/downloads/) tıklatıp **VS 2013** veya **VS 2015** hello içinde **.NET** bölümü.</span><span class="sxs-lookup"><span data-stu-id="e658c-149">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="e658c-150">Visual Studio için Hello en son Azure Data Factory eklentisini indirin: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) veya [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="e658c-150">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="e658c-151">Aşağıdaki adımları hello yaparak hello eklentisi güncelleştirebilirsiniz: hello menüsünde **Araçları** -> **Uzantılar ve güncelleştirmeler** -> **çevrimiçi**  ->  **Visual Studio Galerisi** -> **Visual Studio için Microsoft Azure Data Factory Araçları** -> **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="e658c-151">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

<span data-ttu-id="e658c-152">Şimdi, Visual Studio toocreate bir Azure data factory kullanalım.</span><span class="sxs-lookup"><span data-stu-id="e658c-152">Now, let's use Visual Studio toocreate an Azure data factory.</span></span>

### <a name="create-visual-studio-project"></a><span data-ttu-id="e658c-153">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e658c-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="e658c-154">**Visual Studio 2013** veya **Visual Studio 2015**’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="e658c-154">Launch **Visual Studio 2013** or **Visual Studio 2015**.</span></span> <span data-ttu-id="e658c-155">Tıklatın **dosya**, çok noktası**yeni**, tıklatıp **proje**.</span><span class="sxs-lookup"><span data-stu-id="e658c-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="e658c-156">Merhaba görmelisiniz **yeni proje** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="e658c-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="e658c-157">Merhaba, **yeni proje** iletişim, select hello **DataFactory** şablonu ve tıklatın **boş Data Factory projesi**.</span><span class="sxs-lookup"><span data-stu-id="e658c-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>   

    ![Yeni proje iletişim kutusu](./media/data-factory-build-your-first-pipeline-using-vs/new-project-dialog.png)
3. <span data-ttu-id="e658c-159">Girin bir **adı** hello projesi için **konumu**ve hello için bir ad **çözüm**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="e658c-159">Enter a **name** for hello project, **location**, and a name for hello **solution**, and click **OK**.</span></span>

    ![Çözüm Gezgini](./media/data-factory-build-your-first-pipeline-using-vs/solution-explorer.png)

### <a name="create-linked-services"></a><span data-ttu-id="e658c-161">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="e658c-161">Create linked services</span></span>
<span data-ttu-id="e658c-162">Bu adımda iki bağlı hizmet oluşturursunuz: **Azure Depolama** ve **İsteğe bağlı HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="e658c-162">In this step, you create two linked services: **Azure Storage** and **HDInsight on-demand**.</span></span> 

<span data-ttu-id="e658c-163">Hello Azure depolama hizmeti bağlantıları hello bağlantı bilgilerini sağlayarak Azure depolama hesabı toohello data factory'nizi bağlı.</span><span class="sxs-lookup"><span data-stu-id="e658c-163">hello Azure Storage linked service links your Azure Storage account toohello data factory by providing hello connection information.</span></span> <span data-ttu-id="e658c-164">Veri Fabrikası hizmetine bağlı hello hizmet ayarı tooconnect toohello Azure depolama bağlantı dizesinden hello çalışma zamanında kullanır.</span><span class="sxs-lookup"><span data-stu-id="e658c-164">Data Factory service uses hello connection string from hello linked service setting tooconnect toohello Azure storage at runtime.</span></span> <span data-ttu-id="e658c-165">Bu depolama giriş tutar ve çıktı verilerini hello ardışık düzen ve hello için komut dosyası hello hive etkinlik tarafından kullanılan hive.</span><span class="sxs-lookup"><span data-stu-id="e658c-165">This storage holds input and output data for hello pipeline, and hello hive script file used by hello hive activity.</span></span> 

<span data-ttu-id="e658c-166">İsteğe bağlı Hdınsight bağlı hizmeti ile Merhaba giriş verisi hazır tooprocessed olduğunda hello Hdınsight kümesi çalışma zamanında otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e658c-166">With on-demand HDInsight linked service, hello HDInsight cluster is automatically created at runtime when hello input data is ready tooprocessed.</span></span> <span data-ttu-id="e658c-167">Merhaba küme hello belirtilen süre boyunca işlem yapma ve boşta bittikten sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="e658c-167">hello cluster is deleted after it is done processing and idle for hello specified amount of time.</span></span> 

> [!NOTE]
> <span data-ttu-id="e658c-168">Veri Fabrikası adı ve ayarları Data Factory çözümünüzü yayımlama hello zamanında belirterek oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e658c-168">You create a data factory by specifying its name and settings at hello time of publishing your Data Factory solution.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="e658c-169">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="e658c-169">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="e658c-170">Sağ **bağlı hizmetler** hello Çözüm Gezgini'nde çok noktası**Ekle**, tıklatıp **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="e658c-170">Right-click **Linked Services** in hello solution explorer, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="e658c-171">Merhaba, **Yeni Öğe Ekle** iletişim kutusunda **Azure depolama bağlı hizmeti** hello listesi ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e658c-171">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span>
    <span data-ttu-id="e658c-172">![Azure Storage Bağlı Hizmeti](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="e658c-172">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/new-azure-storage-linked-service.png)</span></span>
3. <span data-ttu-id="e658c-173">Değiştir `<accountname>` ve `<accountkey>` Azure storage hesabınızı ve anahtarını hello adı.</span><span class="sxs-lookup"><span data-stu-id="e658c-173">Replace `<accountname>` and `<accountkey>` with hello name of your Azure storage account and its key.</span></span> <span data-ttu-id="e658c-174">toolearn tooget depolama alanınızın erişim nasıl anahtar, hello bilgi nasıl tooview, kopyalama ve yeniden oluşturma depolama erişim anahtarları içinde hakkında [depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="e658c-174">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
    <span data-ttu-id="e658c-175">![Azure Storage Bağlı Hizmeti](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span><span class="sxs-lookup"><span data-stu-id="e658c-175">![Azure Storage Linked Service](./media/data-factory-build-your-first-pipeline-using-vs/azure-storage-linked-service.png)</span></span>
4. <span data-ttu-id="e658c-176">Merhaba Kaydet **AzureStorageLinkedService1.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="e658c-176">Save hello **AzureStorageLinkedService1.json** file.</span></span>

#### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="e658c-177">Azure HDInsight bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="e658c-177">Create Azure HDInsight linked service</span></span>
1. <span data-ttu-id="e658c-178">Merhaba, **Çözüm Gezgini**, sağ **bağlı hizmetler**, çok noktası**Ekle**, tıklatıp **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="e658c-178">In hello **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="e658c-179">**İsteğe Bağlı HDInsight Bağlı Hizmeti**’ni seçin ve **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e658c-179">Select **HDInsight On Demand Linked Service**, and click **Add**.</span></span>
3. <span data-ttu-id="e658c-180">Hello yerine **JSON** JSON aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="e658c-180">Replace hello **JSON** with hello following JSON:</span></span>

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

    <span data-ttu-id="e658c-181">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="e658c-181">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    <span data-ttu-id="e658c-182">Özellik</span><span class="sxs-lookup"><span data-stu-id="e658c-182">Property</span></span> | <span data-ttu-id="e658c-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e658c-183">Description</span></span>
    -------- | ----------- 
    <span data-ttu-id="e658c-184">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="e658c-184">ClusterSize</span></span> | <span data-ttu-id="e658c-185">Merhaba Hdınsight Hadoop kümesi Hello boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="e658c-185">Specifies hello size of hello HDInsight Hadoop cluster.</span></span>
    <span data-ttu-id="e658c-186">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="e658c-186">TimeToLive</span></span> | <span data-ttu-id="e658c-187">Silinmeden önce hello Hdınsight kümesi, o hello boşta kalma süresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="e658c-187">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span>
    <span data-ttu-id="e658c-188">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e658c-188">linkedServiceName</span></span> | <span data-ttu-id="e658c-189">Hdınsight Hadoop kümesi tarafından oluşturulan kullanılan toostore hello günlükleri olan hello depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e658c-189">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight Hadoop cluster.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="e658c-190">Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello blob depolamada hello JSON (linkedServiceName) belirtildi.</span><span class="sxs-lookup"><span data-stu-id="e658c-190">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (linkedServiceName).</span></span> <span data-ttu-id="e658c-191">Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez.</span><span class="sxs-lookup"><span data-stu-id="e658c-191">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="e658c-192">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="e658c-192">This behavior is by design.</span></span> <span data-ttu-id="e658c-193">İsteğe bağlı HDInsight bağlı hizmeti kullanıldığında, mevcut canlı bir küme olmadığı sürece bir dilim her işlendiğinde bir HDInsight kümesi oluşturulur (timeToLive).</span><span class="sxs-lookup"><span data-stu-id="e658c-193">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="e658c-194">Merhaba işlem bittiğinde hello küme otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="e658c-194">hello cluster is automatically deleted when hello processing is done.</span></span>
    > 
    > <span data-ttu-id="e658c-195">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e658c-195">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="e658c-196">Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti.</span><span class="sxs-lookup"><span data-stu-id="e658c-196">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="e658c-197">Bu kapsayıcıların Hello adları izleyen bir desen: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="e658c-197">hello names of these containers follow a pattern: `adf<yourdatafactoryname>-<linkedservicename>-datetimestamp`.</span></span> <span data-ttu-id="e658c-198">Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.</span><span class="sxs-lookup"><span data-stu-id="e658c-198">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

    <span data-ttu-id="e658c-199">JSON özellikleri hakkında daha fazla bilgi için [İşlem bağlı hizmetleri](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="e658c-199">For more information about JSON properties, see [Compute linked services](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article.</span></span> 
4. <span data-ttu-id="e658c-200">Merhaba Kaydet **Hdınsightondemandlinkedservice1.JSON** dosya.</span><span class="sxs-lookup"><span data-stu-id="e658c-200">Save hello **HDInsightOnDemandLinkedService1.json** file.</span></span>

### <a name="create-datasets"></a><span data-ttu-id="e658c-201">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="e658c-201">Create datasets</span></span>
<span data-ttu-id="e658c-202">Bu adımda, veri kümeleri toorepresent hello girişi oluşturun ve Hive işlenmesi için verileri çıktı.</span><span class="sxs-lookup"><span data-stu-id="e658c-202">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="e658c-203">Bu veri kümeleri toohello başvuran **AzureStorageLinkedService1** Bu öğreticide daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="e658c-203">These datasets refer toohello **AzureStorageLinkedService1** you have created earlier in this tutorial.</span></span> <span data-ttu-id="e658c-204">bağlantılı hizmet noktaları tooan Azure depolama hesabı hello ve veri kümeleri, giriş tutan hello depolamada kapsayıcı, klasör, dosya adı belirtin ve çıktı verilerini.</span><span class="sxs-lookup"><span data-stu-id="e658c-204">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

#### <a name="create-input-dataset"></a><span data-ttu-id="e658c-205">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e658c-205">Create input dataset</span></span>
1. <span data-ttu-id="e658c-206">Merhaba, **Çözüm Gezgini**, sağ **tabloları**, çok noktası**Ekle**, tıklatıp **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="e658c-206">In hello **Solution Explorer**, right-click **Tables**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="e658c-207">Seçin **Azure Blob** hello listeden hello hello dosyasının adını çok değiştirme**Inputdataset.JSON**, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e658c-207">Select **Azure Blob** from hello list, change hello name of hello file too**InputDataSet.json**, and click **Add**.</span></span>
3. <span data-ttu-id="e658c-208">Hello yerine **JSON** hello düzenleyicisinde JSON parçacığı aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="e658c-208">Replace hello **JSON** in hello editor with hello following JSON snippet:</span></span>

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
    <span data-ttu-id="e658c-209">Bu JSON parçacığı adlı veri kümesini tanımlamaktadır **Azureblobınput** hello ardışık düzen hello hive etkinliğin girdi verilerini temsil eden.</span><span class="sxs-lookup"><span data-stu-id="e658c-209">This JSON snippet defines a dataset called **AzureBlobInput** that represents input data for hello hive activity in hello pipeline.</span></span> <span data-ttu-id="e658c-210">Merhaba giriş verisi adlı hello blob kapsayıcısında bulunur belirttiğiniz `adfgetstarted` ve adlı hello klasör `inputdata`.</span><span class="sxs-lookup"><span data-stu-id="e658c-210">You specify that hello input data is located in hello blob container called `adfgetstarted` and hello folder called `inputdata`.</span></span>

    <span data-ttu-id="e658c-211">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="e658c-211">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    <span data-ttu-id="e658c-212">Özellik</span><span class="sxs-lookup"><span data-stu-id="e658c-212">Property</span></span> | <span data-ttu-id="e658c-213">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e658c-213">Description</span></span> |
    -------- | ----------- |
    <span data-ttu-id="e658c-214">type</span><span class="sxs-lookup"><span data-stu-id="e658c-214">type</span></span> |<span data-ttu-id="e658c-215">Merhaba type özelliği çok ayarlamak**AzureBlob** verileri Azure Blob depolamada yer aldığından.</span><span class="sxs-lookup"><span data-stu-id="e658c-215">hello type property is set too**AzureBlob** because data resides in Azure Blob Storage.</span></span>
    <span data-ttu-id="e658c-216">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="e658c-216">linkedServiceName</span></span> | <span data-ttu-id="e658c-217">Daha önce oluşturduğunuz AzureStorageLinkedService1 toohello başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="e658c-217">Refers toohello AzureStorageLinkedService1 you created earlier.</span></span>
    <span data-ttu-id="e658c-218">fileName</span><span class="sxs-lookup"><span data-stu-id="e658c-218">fileName</span></span> |<span data-ttu-id="e658c-219">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e658c-219">This property is optional.</span></span> <span data-ttu-id="e658c-220">Bu özelliği atarsanız, hello folderPath tüm hello dosyalarından çekilir.</span><span class="sxs-lookup"><span data-stu-id="e658c-220">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="e658c-221">Bu durumda, yalnızca hello input.log işlenir.</span><span class="sxs-lookup"><span data-stu-id="e658c-221">In this case, only hello input.log is processed.</span></span>
    <span data-ttu-id="e658c-222">type</span><span class="sxs-lookup"><span data-stu-id="e658c-222">type</span></span> | <span data-ttu-id="e658c-223">Merhaba günlük dosyaları metin biçiminde olduğundan TextFormat kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="e658c-223">hello log files are in text format, so we use TextFormat.</span></span> |
    <span data-ttu-id="e658c-224">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="e658c-224">columnDelimiter</span></span> | <span data-ttu-id="e658c-225">Merhaba günlük dosyalarındaki sütunlar hello virgül karakteriyle ayrılmış (`,`)</span><span class="sxs-lookup"><span data-stu-id="e658c-225">columns in hello log files are delimited by hello comma character (`,`)</span></span>
    <span data-ttu-id="e658c-226">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="e658c-226">frequency/interval</span></span> | <span data-ttu-id="e658c-227">tooMonth sıklığını ve aralığı hello girdi dilimlerinin aylık olarak kullanılabileceğini 1.</span><span class="sxs-lookup"><span data-stu-id="e658c-227">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span>
    <span data-ttu-id="e658c-228">external</span><span class="sxs-lookup"><span data-stu-id="e658c-228">external</span></span> | <span data-ttu-id="e658c-229">Hello etkinlik için giriş verileri Hello hello ardışık düzen tarafından oluşturulmadıysa, bu özellik tootrue ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="e658c-229">This property is set tootrue if hello input data for hello activity is not generated by hello pipeline.</span></span> <span data-ttu-id="e658c-230">Bu özellik yalnızca giriş veri kümelerinde belirtilir.</span><span class="sxs-lookup"><span data-stu-id="e658c-230">This property is only specified on input datasets.</span></span> <span data-ttu-id="e658c-231">Merhaba girdi veri kümesi hello ilk etkinlik için her zaman tootrue ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e658c-231">For hello input dataset of hello first activity, always set it tootrue.</span></span>
4. <span data-ttu-id="e658c-232">Merhaba Kaydet **Inputdataset.JSON** dosya.</span><span class="sxs-lookup"><span data-stu-id="e658c-232">Save hello **InputDataset.json** file.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="e658c-233">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="e658c-233">Create output dataset</span></span>
<span data-ttu-id="e658c-234">Şimdi, hello Azure Blob Depolama depolanan hello çıkış veri kümesi toorepresent çıktı verileri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e658c-234">Now, you create hello output dataset toorepresent output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="e658c-235">Merhaba, **Çözüm Gezgini**, sağ **tabloları**, çok noktası**Ekle**, tıklatıp **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="e658c-235">In hello **Solution Explorer**, right-click **tables**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="e658c-236">Seçin **Azure Blob** hello listeden hello hello dosyasının adını çok değiştirme**OutputDataset.json**, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e658c-236">Select **Azure Blob** from hello list, change hello name of hello file too**OutputDataset.json**, and click **Add**.</span></span>
3. <span data-ttu-id="e658c-237">Hello yerine **JSON** hello düzenleyicisinde JSON aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="e658c-237">Replace hello **JSON** in hello editor with hello following JSON:</span></span>
    
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
    <span data-ttu-id="e658c-238">Merhaba JSON parçacığı tanımlar adlı bir veri kümesi **AzureBlobOutput** çıktı hello hive etkinliğiyle hello ardışık düzen tarafından üretilen verilerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="e658c-238">hello JSON snippet defines a dataset called **AzureBlobOutput** that represents output data produced by hello hive activity in hello pipeline.</span></span> <span data-ttu-id="e658c-239">Merhaba çıktı hello hive etkinliği tarafından üretilen veriler adlı hello blob kapsayıcısında yerleştirilir belirttiğiniz `adfgetstarted` ve adlı hello klasör `partitioneddata`.</span><span class="sxs-lookup"><span data-stu-id="e658c-239">You specify that hello output data is produced by hello hive activity is placed in hello blob container called `adfgetstarted` and hello folder called `partitioneddata`.</span></span> 
    
    <span data-ttu-id="e658c-240">Merhaba **kullanılabilirlik** bölümü belirtiyor bu hello çıktı veri kümesi, aylık olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e658c-240">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span> <span data-ttu-id="e658c-241">Merhaba ardışık Hello çıkış veri kümesi sürücüleri hello zamanlama.</span><span class="sxs-lookup"><span data-stu-id="e658c-241">hello output dataset drives hello schedule of hello pipeline.</span></span> <span data-ttu-id="e658c-242">Merhaba ardışık düzen aylık, başlangıç ve bitiş zamanları arasında çalışır.</span><span class="sxs-lookup"><span data-stu-id="e658c-242">hello pipeline runs monthly between its start and end times.</span></span> 

    <span data-ttu-id="e658c-243">Bkz: **hello girdi veri kümesi oluşturma** bu özelliklerin açıklamaları için bölüm.</span><span class="sxs-lookup"><span data-stu-id="e658c-243">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="e658c-244">Merhaba dataset hello ardışık düzen tarafından oluşturulduğundan çıktı veri hello dış özelliği ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="e658c-244">You do not set hello external property on an output dataset as hello dataset is produced by hello pipeline.</span></span>
4. <span data-ttu-id="e658c-245">Merhaba Kaydet **OutputDataset.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="e658c-245">Save hello **OutputDataset.json** file.</span></span>

### <a name="create-pipeline"></a><span data-ttu-id="e658c-246">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e658c-246">Create pipeline</span></span>
<span data-ttu-id="e658c-247">Hello Azure Storage bağlı hizmeti ve girdi ve çıktı veri kümelerini kadarki oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="e658c-247">You have created hello Azure Storage linked service, and input and output datasets so far.</span></span> <span data-ttu-id="e658c-248">Şimdi, **HDInsightHive** etkinliğiyle bir işlem hattı oluşturacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e658c-248">Now, you create a pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="e658c-249">Merhaba **giriş** hello hive etkinliği çok ayarlanır**Azureblobınput** ve **çıkış** çok ayarlanır**AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="e658c-249">hello **input** for hello hive activity is set too**AzureBlobInput** and **output** is set too**AzureBlobOutput**.</span></span> <span data-ttu-id="e658c-250">Bir dilim bir giriş veri kümesinin aylık kullanılabilir (sıklığı: Month, interval: 1), ve hello çıktı diliminin ayda bir oluşturulduğunu çok.</span><span class="sxs-lookup"><span data-stu-id="e658c-250">A slice of an input dataset is available monthly (frequency: Month, interval: 1), and hello output slice is produced monthly too.</span></span> 

1. <span data-ttu-id="e658c-251">Merhaba, **Çözüm Gezgini**, sağ **ardışık düzen**, çok noktası**Ekle**, tıklatıp **yeni öğe.**</span><span class="sxs-lookup"><span data-stu-id="e658c-251">In hello **Solution Explorer**, right-click **Pipelines**, point too**Add**, and click **New Item.**</span></span>
2. <span data-ttu-id="e658c-252">Seçin **Hive dönüşüm işlem hattı** hello listesi ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e658c-252">Select **Hive Transformation Pipeline** from hello list, and click **Add**.</span></span>
3. <span data-ttu-id="e658c-253">Hello yerine **JSON** parçacığını aşağıdaki hello ile:</span><span class="sxs-lookup"><span data-stu-id="e658c-253">Replace hello **JSON** with hello following snippet:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e658c-254">Değiştir `<storageaccountname>` depolama hesabınızın hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="e658c-254">Replace `<storageaccountname>` with hello name of your storage account.</span></span>

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
    > <span data-ttu-id="e658c-255">Değiştir `<storageaccountname>` depolama hesabınızın hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="e658c-255">Replace `<storageaccountname>` with hello name of your storage account.</span></span>

    <span data-ttu-id="e658c-256">Merhaba JSON parçacığı tek bir etkinliğin (Hive etkinliği) oluşan bir ardışık düzen tanımlar.</span><span class="sxs-lookup"><span data-stu-id="e658c-256">hello JSON snippet defines a pipeline that consists of a single activity (Hive Activity).</span></span> <span data-ttu-id="e658c-257">Bu etkinlik bir Hive betiği tooprocess giriş verilerini bir isteğe bağlı Hdınsight kümesi tooproduce çıktı verileri üzerinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="e658c-257">This activity runs a Hive script tooprocess input data on an on-demand HDInsight cluster tooproduce output data.</span></span> <span data-ttu-id="e658c-258">Merhaba etkinlikler bölümünde hello ardışık JSON, çok kümesi türü ile yalnızca bir etkinlik hello dizisindeki bkz**Hdınsighthive**.</span><span class="sxs-lookup"><span data-stu-id="e658c-258">In hello activities section of hello pipeline JSON, you see only one activity in hello array with type set too**HDInsightHive**.</span></span> 

    <span data-ttu-id="e658c-259">Belirli tooHDInsight Hive etkinliği olan hello türü özelliklerinde, hangi Azure Storage bağlı hizmeti hello hive betik dosyası, hello yolu toohello komut dosyası ve parametreleri toohello komut dosyasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="e658c-259">In hello type properties that are specific tooHDInsight Hive activity, you specify what Azure Storage linked service has hello hive script file, hello path toohello script file, and parameters toohello script file.</span></span> 

    <span data-ttu-id="e658c-260">Merhaba Hive betik dosyası **partitionweblogs.hql**, (Merhaba scriptLinkedService tarafından belirtilen) hello Azure depolama hesabı ve hello depolanan `script` hello kapsayıcı klasöründe `adfgetstarted`.</span><span class="sxs-lookup"><span data-stu-id="e658c-260">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService), and in hello `script` folder in hello container `adfgetstarted`.</span></span>

    <span data-ttu-id="e658c-261">Merhaba `defines` bölümdür toohello hive betiğini Hive yapılandırma değerleri olarak geçirilir kullanılan toospecify hello çalışma zamanı ayarları (örneğin `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span><span class="sxs-lookup"><span data-stu-id="e658c-261">hello `defines` section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g `${hiveconf:inputtable}`, `${hiveconf:partitionedtable})`.</span></span>

    <span data-ttu-id="e658c-262">Merhaba **Başlat** ve **son** hello ardışık düzen özelliklerini hello etkin dönem hello ardışık belirtir.</span><span class="sxs-lookup"><span data-stu-id="e658c-262">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span> <span data-ttu-id="e658c-263">Merhaba dataset toobe (Merhaba ay başlangıç ve bitiş tarihleri aynı olduğu için) yalnızca dilim hello ardışık düzen tarafından üretilen sonra aylık, bu nedenle, üretilen yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="e658c-263">You configured hello dataset toobe produced monthly, therefore, only once slice is produced by hello pipeline (because hello month is same in start and end dates).</span></span>

    <span data-ttu-id="e658c-264">Bu hello Hive betiğini hello tarafından belirtilen hello işlem üzerinde çalıştığı belirtin Hello JSON etkinliğinde **linkedServiceName** – **Hdınsightondemandlinkedservice**.</span><span class="sxs-lookup"><span data-stu-id="e658c-264">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>
4. <span data-ttu-id="e658c-265">Merhaba Kaydet **HiveActivity1.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="e658c-265">Save hello **HiveActivity1.json** file.</span></span>

### <a name="add-partitionweblogshql-and-inputlog-as-a-dependency"></a><span data-ttu-id="e658c-266">partitionweblogs.hql ve input.log dosyalarını bağımlılık olarak ekleme</span><span class="sxs-lookup"><span data-stu-id="e658c-266">Add partitionweblogs.hql and input.log as a dependency</span></span>
1. <span data-ttu-id="e658c-267">Sağ **bağımlılıkları** hello içinde **Çözüm Gezgini** penceresinde, çok noktası**Ekle**, tıklatıp **varolan öğeyi**.</span><span class="sxs-lookup"><span data-stu-id="e658c-267">Right-click **Dependencies** in hello **Solution Explorer** window, point too**Add**, and click **Existing Item**.</span></span>  
2. <span data-ttu-id="e658c-268">Toohello gidin **C:\ADFGettingStarted** seçip **partitionweblogs.hql**, **input.log** dosyaları ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="e658c-268">Navigate toohello **C:\ADFGettingStarted** and select **partitionweblogs.hql**, **input.log** files, and click **Add**.</span></span> <span data-ttu-id="e658c-269">Bu iki dosyayı hello önkoşulları bir parçası olarak oluşturulan [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="e658c-269">You created these two files as part of prerequisites from hello [Tutorial Overview](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="e658c-270">Merhaba sonraki adımda hello çözümü yayımladığınızda hello **partitionweblogs.hql** dosyasıdır karşıya yüklenen toohello **betik** hello klasöründe `adfgetstarted` blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="e658c-270">When you publish hello solution in hello next step, hello **partitionweblogs.hql** file is uploaded toohello **script** folder in hello `adfgetstarted` blob container.</span></span>   

### <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="e658c-271">Data Factory varlıklarını yayımlama/dağıtma</span><span class="sxs-lookup"><span data-stu-id="e658c-271">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="e658c-272">Bu adımda, proje toohello Azure Data Factory hizmetine hello Data Factory varlıkları (bağlı hizmetler, veri kümeleri ve işlem hattı) yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e658c-272">In this step, you publish hello Data Factory entities (linked services, datasets, and pipeline) in your project toohello Azure Data Factory service.</span></span> <span data-ttu-id="e658c-273">Yayımlama Hello işleminde veri fabrikanızın hello adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="e658c-273">In hello process of publishing, you specify hello name for your data factory.</span></span> 

1. <span data-ttu-id="e658c-274">Merhaba Çözüm Gezgini'nde projeye sağ tıklayın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="e658c-274">Right-click project in hello Solution Explorer, and click **Publish**.</span></span>
2. <span data-ttu-id="e658c-275">Görürseniz **tooyour Microsoft hesabı oturum** iletişim kutusunda, Azure aboneliği olan hello hesabı için kimlik bilgilerinizi girin ve tıklayın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="e658c-275">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="e658c-276">İletişim kutusu aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="e658c-276">You should see hello following dialog box:</span></span>

   ![Yayımla iletişim kutusu](./media/data-factory-build-your-first-pipeline-using-vs/publish.png)
4. <span data-ttu-id="e658c-278">Merhaba, **data factory Yapılandır** sayfasında, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="e658c-278">In hello **Configure data factory** page, do hello following steps:</span></span>

    ![Yayımlama - Yeni veri fabrikası ayarları](media/data-factory-build-your-first-pipeline-using-vs/publish-new-data-factory.png)

   1. <span data-ttu-id="e658c-280">**Yeni Data Factory Oluştur** seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="e658c-280">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="e658c-281">Benzersiz bir girin **adı** hello veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="e658c-281">Enter a unique **name** for hello data factory.</span></span> <span data-ttu-id="e658c-282">Örneğin: **DataFactoryUsingVS09152016**.</span><span class="sxs-lookup"><span data-stu-id="e658c-282">For example: **DataFactoryUsingVS09152016**.</span></span> <span data-ttu-id="e658c-283">Merhaba adı genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e658c-283">hello name must be globally unique.</span></span>
   3. <span data-ttu-id="e658c-284">Merhaba hello için doğru abonelik seçin **abonelik** alan.</span><span class="sxs-lookup"><span data-stu-id="e658c-284">Select hello right subscription for hello **Subscription** field.</span></span> 
        > [!IMPORTANT]
        > <span data-ttu-id="e658c-285">Herhangi bir abonelik görmüyorsanız, bir yönetici veya hello aboneliğin ortak yöneticisi olan bir hesabı kullanarak oturum emin olun.</span><span class="sxs-lookup"><span data-stu-id="e658c-285">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>
   4. <span data-ttu-id="e658c-286">Select hello **kaynak grubu** oluşturulan hello veri fabrikası toobe için.</span><span class="sxs-lookup"><span data-stu-id="e658c-286">Select hello **resource group** for hello data factory toobe created.</span></span>
   5. <span data-ttu-id="e658c-287">Select hello **bölge** hello veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="e658c-287">Select hello **region** for hello data factory.</span></span>
   6. <span data-ttu-id="e658c-288">Tıklatın **sonraki** tooswitch toohello **öğeleri Yayımla** sayfası.</span><span class="sxs-lookup"><span data-stu-id="e658c-288">Click **Next** tooswitch toohello **Publish Items** page.</span></span> <span data-ttu-id="e658c-289">(Tuşuna **sekmesini** hello ad alanı tooif hello dışında toomove **sonraki** düğmesi devre dışıdır.)</span><span class="sxs-lookup"><span data-stu-id="e658c-289">(Press **TAB** toomove out of hello Name field tooif hello **Next** button is disabled.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e658c-290">Merhaba hata alırsanız **veri fabrikası adı "DataFactoryUsingVS" kullanılabilir değil** yayımlarken hello adını (örneğin, yournameDataFactoryUsingVS) değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e658c-290">If you receive hello error **Data factory name “DataFactoryUsingVS” is not available** when publishing, change hello name (for example, yournameDataFactoryUsingVS).</span></span> <span data-ttu-id="e658c-291">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="e658c-291">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>   
1. <span data-ttu-id="e658c-292">Merhaba, **öğeleri Yayımla** sayfasında, tüm veri varlıkları seçilir ve tıklatın fabrikaları hello olun **sonraki** tooswitch toohello **Özet** sayfası.</span><span class="sxs-lookup"><span data-stu-id="e658c-292">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>

    ![Öğe yayımlama sayfası](media/data-factory-build-your-first-pipeline-using-vs/publish-items-page.png)     
2. <span data-ttu-id="e658c-294">Merhaba özeti gözden geçirin ve tıklatın **sonraki** toostart, hello dağıtım işlemi ve görünüm hello **dağıtım durumu**.</span><span class="sxs-lookup"><span data-stu-id="e658c-294">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>

    ![Özet sayfası](media/data-factory-build-your-first-pipeline-using-vs/summary-page.png)
3. <span data-ttu-id="e658c-296">Merhaba, **dağıtım durumu** sayfasında hello hello dağıtım işleminin durumunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e658c-296">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="e658c-297">Merhaba dağıtımını gerçekleştirdikten sonra Son'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e658c-297">Click Finish after hello deployment is done.</span></span>

<span data-ttu-id="e658c-298">Önemli noktaları toonote:</span><span class="sxs-lookup"><span data-stu-id="e658c-298">Important points toonote:</span></span>

- <span data-ttu-id="e658c-299">Merhaba hatayı alırsanız: **Bu abonelik, Microsoft.DataFactory kayıtlı toouse ad değil**hello aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:</span><span class="sxs-lookup"><span data-stu-id="e658c-299">If you receive hello error: **This subscription is not registered toouse namespace Microsoft.DataFactory**, do one of hello following and try publishing again:</span></span>
    - <span data-ttu-id="e658c-300">Azure PowerShell'de komut tooregister hello Data Factory sağlayıcısının aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e658c-300">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span>
        ```PowerShell   
        Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
        ```
        <span data-ttu-id="e658c-301">Bu Data Factory sağlayıcısının kayıtlı hello komutu tooconfirm aşağıdaki hello çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e658c-301">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span>

        ```PowerShell
        Get-AzureRmResourceProvider
        ```
    - <span data-ttu-id="e658c-302">Merhaba toohello Azure aboneliğinizde oturum açma kullanılarak [Azure portal](https://portal.azure.com) ve tooa Data Factory dikey penceresine gidin (veya) hello Azure portalında bir data factory oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e658c-302">Login using hello Azure subscription in toohello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="e658c-303">Bu eylemin hello sağlayıcıyı sizin için otomatik olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="e658c-303">This action automatically registers hello provider for you.</span></span>
- <span data-ttu-id="e658c-304">Merhaba veri fabrikasının Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="e658c-304">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
- <span data-ttu-id="e658c-305">toocreate Data Factory örnekleri, toobe bir yönetici veya ortak yöneticisi olan hello Azure aboneliği gerekir</span><span class="sxs-lookup"><span data-stu-id="e658c-305">toocreate Data Factory instances, you need toobe an admin or co-admin of hello Azure subscription</span></span>

### <a name="monitor-pipeline"></a><span data-ttu-id="e658c-306">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="e658c-306">Monitor pipeline</span></span>
<span data-ttu-id="e658c-307">Bu adımda, diyagram görünümü hello data Factory kullanarak hello ardışık izleyin.</span><span class="sxs-lookup"><span data-stu-id="e658c-307">In this step, you monitor hello pipeline using Diagram View of hello data factory.</span></span> 

#### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="e658c-308">Diyagram Görünümünü kullanarak işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="e658c-308">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="e658c-309">İçinde toohello oturum [Azure portal](https://portal.azure.com/), adımları hello:</span><span class="sxs-lookup"><span data-stu-id="e658c-309">Log in toohello [Azure portal](https://portal.azure.com/), do hello following steps:</span></span>
   1. <span data-ttu-id="e658c-310">**Diğer hizmetler** ve **Data factory’ler** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e658c-310">Click **More services** and click **Data factories**.</span></span>
       
        ![Data factory’lere göz atma](./media/data-factory-build-your-first-pipeline-using-vs/browse-datafactories.png)
   2. <span data-ttu-id="e658c-312">Veri fabrikanızın SELECT hello adı (örneğin: **DataFactoryUsingVS09152016**) veri fabrikaları hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="e658c-312">Select hello name of your data factory (for example: **DataFactoryUsingVS09152016**) from hello list of data factories.</span></span>
   
       ![Data factory’nizi seçme](./media/data-factory-build-your-first-pipeline-using-vs/select-first-data-factory.png)
2. <span data-ttu-id="e658c-314">Merhaba giriş sayfasında veri fabrikanızın tıklatın **diyagramı**.</span><span class="sxs-lookup"><span data-stu-id="e658c-314">In hello home page for your data factory, click **Diagram**.</span></span>

    ![Diyagram kutucuğu](./media/data-factory-build-your-first-pipeline-using-vs/diagram-tile.png)
3. <span data-ttu-id="e658c-316">Hello diyagram görünümü, hello ardışık düzen ve Bu öğreticide kullanılan veri kümelerine genel bakış konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="e658c-316">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Diyagram Görünümü](./media/data-factory-build-your-first-pipeline-using-vs/diagram-view-2.png)
4. <span data-ttu-id="e658c-318">tooview hello düzenindeki hello sağ kanaldaki tüm etkinlikleri Diyagram ve ardışık düzeni Aç'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e658c-318">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![İşlem hattı menüsünü açma](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-menu.png)
5. <span data-ttu-id="e658c-320">Merhaba ardışık düzeninde hello Hdınsighthive etkinliğini gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="e658c-320">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![İşlem hattı görünümünü açma](./media/data-factory-build-your-first-pipeline-using-vs/open-pipeline-view.png)

    <span data-ttu-id="e658c-322">toonavigate toohello önceki görünüme geri tıklatın **veri fabrikası** hello içerik haritası menüsünde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="e658c-322">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
6. <span data-ttu-id="e658c-323">Merhaba, **diyagram görünümü**, hello dataset çift **Azureblobınput**.</span><span class="sxs-lookup"><span data-stu-id="e658c-323">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="e658c-324">Bu hello dilim onaylayın **hazır** durumu.</span><span class="sxs-lookup"><span data-stu-id="e658c-324">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="e658c-325">Bu işlem birkaç dakika hello dilim tooshow için hazır durumda kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="e658c-325">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="e658c-326">Bir süre bekledikten sonra gerçekleştirilmez, hello doğru kapsayıcıda yerleştirilen hello girdi dosyasının (input.log) yüklü olup olmadığına bakın (`adfgetstarted`) ve klasör (`inputdata`).</span><span class="sxs-lookup"><span data-stu-id="e658c-326">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (`adfgetstarted`) and folder (`inputdata`).</span></span> <span data-ttu-id="e658c-327">Ve o hello emin olun **dış** özelliği hello giriş veri kümesi üzerinde çok ayarlanmış**doğru**.</span><span class="sxs-lookup"><span data-stu-id="e658c-327">And, make sure that hello **external** property on hello input dataset is set too**true**.</span></span> 

   ![Girdi dilimi hazır durumda](./media/data-factory-build-your-first-pipeline-using-vs/input-slice-ready.png)
7. <span data-ttu-id="e658c-329">Tıklatın **X** tooclose **Azureblobınput** dikey.</span><span class="sxs-lookup"><span data-stu-id="e658c-329">Click **X** tooclose **AzureBlobInput** blade.</span></span>
8. <span data-ttu-id="e658c-330">Merhaba, **diyagram görünümü**, hello dataset çift **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="e658c-330">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="e658c-331">İşlenmekte olan bu hello dilim bakın.</span><span class="sxs-lookup"><span data-stu-id="e658c-331">You see that hello slice that is currently being processed.</span></span>

   ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-vs/dataset-blade.png)
9. <span data-ttu-id="e658c-333">İşlem bittiğinde hello dilimi bkz **hazır** durumu.</span><span class="sxs-lookup"><span data-stu-id="e658c-333">When processing is done, you see hello slice in **Ready** state.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e658c-334">İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika).</span><span class="sxs-lookup"><span data-stu-id="e658c-334">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="e658c-335">Bu nedenle, hello ardışık düzen tootake beklediğiniz **yaklaşık olarak 30 dakika** tooprocess hello dilim.</span><span class="sxs-lookup"><span data-stu-id="e658c-335">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>  
   
    ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-vs/dataset-slice-ready.png)    
10. <span data-ttu-id="e658c-337">Merhaba dilim olduğunda **hazır** durum, hello denetleyin `partitioneddata` hello klasöründe `adfgetstarted` hello için blob depolama alanınızın kapsayıcısında çıkış verileri.</span><span class="sxs-lookup"><span data-stu-id="e658c-337">When hello slice is in **Ready** state, check hello `partitioneddata` folder in hello `adfgetstarted` container in your blob storage for hello output data.</span></span>  

    ![çıktı verileri](./media/data-factory-build-your-first-pipeline-using-vs/three-ouptut-files.png)
11. <span data-ttu-id="e658c-339">Merhaba dilim toosee ayrıntılarını içinde tıklatın bir **veri dilimi** dikey.</span><span class="sxs-lookup"><span data-stu-id="e658c-339">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

    ![Veri dilimi ayrıntıları](./media/data-factory-build-your-first-pipeline-using-vs/data-slice-details.png)  
12. <span data-ttu-id="e658c-341">Hello çalıştırmak bir etkinliği **etkinlik çalışır listesi** toosee etkinliği hakkında ayrıntılı bir çalıştır (Senaryomuzda Hive etkinliğiyle) bir **etkinlik çalışma ayrıntıları** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e658c-341">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span> 
  
    ![Etkinlik çalışma ayrıntıları](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-blade.png)    

    <span data-ttu-id="e658c-343">Merhaba günlük dosyalarından yürütüldü hello Hive sorgusu ve durum bilgileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e658c-343">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="e658c-344">Bu günlükler her türlü sorunu gidermek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="e658c-344">These logs are useful for troubleshooting any issues.</span></span>  

<span data-ttu-id="e658c-345">Bkz: [veri kümelerini ve ardışık düzen izleme](data-factory-monitor-manage-pipelines.md) nasıl toouse hello Azure portal toomonitor hello ardışık düzen ve veri kümeleri, bu öğreticide oluşturduğunuz hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="e658c-345">See [Monitor datasets and pipeline](data-factory-monitor-manage-pipelines.md) for instructions on how toouse hello Azure portal toomonitor hello pipeline and datasets you have created in this tutorial.</span></span>

#### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="e658c-346">İzleme ve Yönetme Uygulamasını kullanarak işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="e658c-346">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="e658c-347">İzleyicisi'ni kullanın ve uygulama toomonitor hatlarınızı yönetme.</span><span class="sxs-lookup"><span data-stu-id="e658c-347">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="e658c-348">Bu uygulamanın kullanımına ilişkin ayrıntılı bilgi için bkz. [İzleme ve Yönetme Uygulamasını kullanarak Azure Data Factory işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="e658c-348">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="e658c-349">İzleme ve Yönetme kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e658c-349">Click Monitor & Manage tile.</span></span>

    ![İzleme ve Yönetme kutucuğu](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-tile.png)
2. <span data-ttu-id="e658c-351">İzleme ve Yönetme uygulamasını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e658c-351">You should see Monitor & Manage application.</span></span> <span data-ttu-id="e658c-352">Değişiklik hello **başlangıç zamanı** ve **bitiş saati** toomatch başlangıç (04 01 2016 12: 00'da) ve bitiş zamanları (04-02-2016 12: 00'da) ardışık düzen ve tıklatın **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="e658c-352">Change hello **Start time** and **End time** toomatch start (04-01-2016 12:00 AM) and end times (04-02-2016 12:00 AM) of your pipeline, and click **Apply**.</span></span>

    ![İzleme ve Yönetme Uygulaması](./media/data-factory-build-your-first-pipeline-using-vs/monitor-and-manage-app.png)
3. <span data-ttu-id="e658c-354">bir etkinlik penceresi toosee ayrıntılarını seçin, hello **etkinlik Windows listesi** toosee ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="e658c-354">toosee details about an activity window, select it in hello **Activity Windows list** toosee details about it.</span></span>
    <span data-ttu-id="e658c-355">![Etkinlik penceresi ayrıntıları](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="e658c-355">![Activity window details](./media/data-factory-build-your-first-pipeline-using-vs/activity-window-details.png)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e658c-356">Merhaba dilim başarıyla işlendiğinde hello girdi dosyası silinir.</span><span class="sxs-lookup"><span data-stu-id="e658c-356">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="e658c-357">Merhaba girdi dosyasını (input.log) toohello toorerun hello dilim istediğiniz veya öğreticiyi yeniden Merhaba, bu nedenle, karşıya `inputdata` hello klasörünü `adfgetstarted` kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="e658c-357">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello `inputdata` folder of hello `adfgetstarted` container.</span></span>

### <a name="additional-notes"></a><span data-ttu-id="e658c-358">Ek notlar</span><span class="sxs-lookup"><span data-stu-id="e658c-358">Additional notes</span></span>
- <span data-ttu-id="e658c-359">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="e658c-359">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="e658c-360">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="e658c-360">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="e658c-361">Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform verileri girin.</span><span class="sxs-lookup"><span data-stu-id="e658c-361">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="e658c-362">Bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tüm kaynakları ve kopyalama etkinliği hello tarafından desteklenen havuzlarını hello için.</span><span class="sxs-lookup"><span data-stu-id="e658c-362">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="e658c-363">Bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md) Data Factory ile desteklenen işlem Hizmetleri hello listesi.</span><span class="sxs-lookup"><span data-stu-id="e658c-363">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span>
- <span data-ttu-id="e658c-364">Bağlı hizmetler veri depolarını veya hizmetleri tooan Azure data factory işlem.</span><span class="sxs-lookup"><span data-stu-id="e658c-364">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="e658c-365">Bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tüm kaynakları ve kopyalama etkinliği hello tarafından desteklenen havuzlarını hello için.</span><span class="sxs-lookup"><span data-stu-id="e658c-365">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="e658c-366">Bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md) Data Factory ile desteklenen işlem Hizmetleri hello listesi için ve [dönüştürme etkinlikleri](data-factory-data-transformation-activities.md) , çalıştırabilirsiniz üzerlerinde.</span><span class="sxs-lookup"><span data-stu-id="e658c-366">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory and [transformation activities](data-factory-data-transformation-activities.md) that can run on them.</span></span>
- <span data-ttu-id="e658c-367">Bkz: [taşıma verilerden / tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) hello kullanılan JSON özellikleri hakkında ayrıntılı bilgi için Azure depolama bağlantılı hizmet tanımı.</span><span class="sxs-lookup"><span data-stu-id="e658c-367">See [Move data from/tooAzure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used in hello Azure Storage linked service definition.</span></span>
- <span data-ttu-id="e658c-368">İsteğe bağlı HDInsight kümesi yerine kendi HDInsight kümenizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e658c-368">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="e658c-369">Ayrıntılar için bkz. [İşlem Bağlı Hizmetleri](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="e658c-369">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>
-  <span data-ttu-id="e658c-370">Merhaba Data Factory oluşturur bir **Linux tabanlı** JSON önceki hello ile Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="e658c-370">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello preceding JSON.</span></span> <span data-ttu-id="e658c-371">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="e658c-371">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
- <span data-ttu-id="e658c-372">Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello blob depolamada hello JSON (linkedServiceName) belirtildi.</span><span class="sxs-lookup"><span data-stu-id="e658c-372">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (linkedServiceName).</span></span> <span data-ttu-id="e658c-373">Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez.</span><span class="sxs-lookup"><span data-stu-id="e658c-373">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="e658c-374">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="e658c-374">This behavior is by design.</span></span> <span data-ttu-id="e658c-375">İsteğe bağlı HDInsight bağlı hizmeti kullanıldığında, mevcut canlı bir küme olmadığı sürece bir dilim her işlendiğinde bir HDInsight kümesi oluşturulur (timeToLive).</span><span class="sxs-lookup"><span data-stu-id="e658c-375">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (timeToLive).</span></span> <span data-ttu-id="e658c-376">Merhaba işlem bittiğinde hello küme otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="e658c-376">hello cluster is automatically deleted when hello processing is done.</span></span>
    
    <span data-ttu-id="e658c-377">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="e658c-377">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="e658c-378">Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti.</span><span class="sxs-lookup"><span data-stu-id="e658c-378">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="e658c-379">Bu kapsayıcıların Hello adları izleyen bir desen: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="e658c-379">hello names of these containers follow a pattern: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`.</span></span> <span data-ttu-id="e658c-380">Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.</span><span class="sxs-lookup"><span data-stu-id="e658c-380">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>
- <span data-ttu-id="e658c-381">Şu anda, çıktı veri kümesi hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir böylece hangi sürücüleri zamanlama, hello değil.</span><span class="sxs-lookup"><span data-stu-id="e658c-381">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="e658c-382">Merhaba etkinlik herhangi bir girdi almazsa oluşturma hello girdi veri kümesi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e658c-382">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> 
- <span data-ttu-id="e658c-383">Bu öğreticide, Azure Data Factory kullanarak verilerin nasıl kopyalanacağı gösterilmemektedir.</span><span class="sxs-lookup"><span data-stu-id="e658c-383">This tutorial does not show how copy data by using Azure Data Factory.</span></span> <span data-ttu-id="e658c-384">Nasıl bir öğretici için Azure Data Factory kullanarak toocopy verileri görmek [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="e658c-384">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>


## <a name="use-server-explorer-tooview-data-factories"></a><span data-ttu-id="e658c-385">Sunucu Gezgini tooview veri fabrikaları kullanın</span><span class="sxs-lookup"><span data-stu-id="e658c-385">Use Server Explorer tooview data factories</span></span>
1. <span data-ttu-id="e658c-386">İçinde **Visual Studio**, tıklatın **Görünüm** üzerinde hello menü öğesini tıklatıp **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="e658c-386">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="e658c-387">Merhaba Sunucu Gezgini penceresinde **Azure** ve genişletin **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="e658c-387">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="e658c-388">Görürseniz **tooVisual Studio oturum**, hello girin **hesap** tıklatın ve Azure aboneliği ile ilişkili **devam**.</span><span class="sxs-lookup"><span data-stu-id="e658c-388">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="e658c-389">**parola** girip **Oturum aç**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e658c-389">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="e658c-390">Visual Studio, aboneliğinizdeki tüm Azure data factory'leri hakkında bilgi tooget çalışır.</span><span class="sxs-lookup"><span data-stu-id="e658c-390">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="e658c-391">Bu işlemde hello hello durumunu görmek **Data Factoy görev listesi** penceresi.</span><span class="sxs-lookup"><span data-stu-id="e658c-391">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Sunucu Gezgini](./media/data-factory-build-your-first-pipeline-using-vs/server-explorer.png)
3. <span data-ttu-id="e658c-393">Veri Fabrikası sağ tıklatın ve seçin **dışarı veri fabrikası tooNew proje** Visual Studio projesi dayalı mevcut bir data factory'ye toocreate.</span><span class="sxs-lookup"><span data-stu-id="e658c-393">You can right-click a data factory, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![Data factory’yi dışarı aktarma](./media/data-factory-build-your-first-pipeline-using-vs/export-data-factory-menu.png)

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="e658c-395">Visual Studio için Data Factory araçlarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e658c-395">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="e658c-396">Visual Studio için tooupdate Azure Data Factory araçları hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="e658c-396">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="e658c-397">Tıklatın **Araçları** hello menü ve seçim **Uzantılar ve güncelleştirmeler**.</span><span class="sxs-lookup"><span data-stu-id="e658c-397">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span>
2. <span data-ttu-id="e658c-398">Seçin **güncelleştirmeleri** hello sol bölmesinde ve ardından **Visual Studio Galerisi**.</span><span class="sxs-lookup"><span data-stu-id="e658c-398">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="e658c-399">**Visual Studio için Azure Data Factory araçları**’nı seçin ve **Güncelleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e658c-399">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="e658c-400">Bu girişi görmüyorsanız hello hello Araçları'nın en son sürümü zaten sahip.</span><span class="sxs-lookup"><span data-stu-id="e658c-400">If you do not see this entry, you already have hello latest version of hello tools.</span></span>

## <a name="use-configuration-files"></a><span data-ttu-id="e658c-401">Yapılandırma dosyalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="e658c-401">Use configuration files</span></span>
<span data-ttu-id="e658c-402">Bağlı hizmetler/tablolar/işlem hatları için her ortamda farklı için Visual Studio tooconfigure özelliklerinde yapılandırma dosyalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e658c-402">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="e658c-403">Azure depolama bağlı hizmeti için JSON tanımı aşağıdaki hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="e658c-403">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="e658c-404">toospecify **connectionString** accountname ve accountkey hello ortam (Dev/Test/Production) toowhich üzerinde göre farklı değerleri olan Data Factory varlıklarını dağıttığınız.</span><span class="sxs-lookup"><span data-stu-id="e658c-404">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="e658c-405">Her ortam için ayrı bir yapılandırma dosyası kullanarak bu davranışı elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e658c-405">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="e658c-406">Yapılandırma dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="e658c-406">Add a configuration file</span></span>
<span data-ttu-id="e658c-407">Merhaba aşağıdaki adımları uygulayarak her ortam için bir yapılandırma dosyası ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e658c-407">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="e658c-408">Visual Studio çözümünüzü Hello Data Factory projenize sağ tıklayın, çok gelin**Ekle**, tıklatıp **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="e658c-408">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="e658c-409">Seçin **Config** hello soldaki yüklenmiş şablonlar hello listeden seçin **yapılandırma dosyası**, girin bir **adı** hello yapılandırması için dosya ve tıklatın**Eklemek**.</span><span class="sxs-lookup"><span data-stu-id="e658c-409">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![Yapılandırma dosyasını ekleme](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="e658c-411">Biçim aşağıdaki hello yapılandırma parametrelerini ve değerlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="e658c-411">Add configuration parameters and their values in hello following format:</span></span>

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

    <span data-ttu-id="e658c-412">Bu örnek, Azure Storage bağlı hizmetinin ve Azure SQL bağlı hizmetinin connectionString özelliğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="e658c-412">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="e658c-413">Adı belirtmek için hello sözdizimi olduğuna dikkat edin [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="e658c-413">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="e658c-414">JSON hello kod aşağıdaki gösterildiği gibi bir dizi değere sahip özellik varsa:</span><span class="sxs-lookup"><span data-stu-id="e658c-414">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

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

    <span data-ttu-id="e658c-415">Özellikler, aşağıdaki yapılandırma dosyasına (kullanımı sıfır tabanlı dizin) hello gösterildiği gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="e658c-415">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="e658c-416">Boşluklu özellik adları</span><span class="sxs-lookup"><span data-stu-id="e658c-416">Property names with spaces</span></span>
<span data-ttu-id="e658c-417">Özellik adında boşluklar varsa, hello aşağıdaki örneğine (veritabanı sunucu adı) gösterildiği gibi köşeli ayraç kullanın:</span><span class="sxs-lookup"><span data-stu-id="e658c-417">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="e658c-418">Yapılandırma kullanarak çözümü dağıtma</span><span class="sxs-lookup"><span data-stu-id="e658c-418">Deploy solution using a configuration</span></span>
<span data-ttu-id="e658c-419">Azure Data Factory varlıklarını vs'de toouse Bu yayımlama işlemi için istediğiniz hello yapılandırma belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e658c-419">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="e658c-420">yapılandırma dosyası kullanarak Azure Data Factory projesindeki varlıkları toopublish:</span><span class="sxs-lookup"><span data-stu-id="e658c-420">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="e658c-421">Data Factory projesine sağ tıklatın ve **Yayımla** toosee hello **öğeleri Yayımla** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="e658c-421">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="e658c-422">Mevcut bir veri fabrikasını seçin veya üzerinde hello data factory oluşturmak için değerleri belirtin **data factory Yapılandır** sayfasında ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e658c-422">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="e658c-423">Merhaba üzerinde **öğeleri Yayımla** sayfa: hello için kullanılabilir yapılandırmaların açılan listesini görmek **Dağıtım Yapılandırması Seç** alan.</span><span class="sxs-lookup"><span data-stu-id="e658c-423">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![Yapılandırma dosyası seçme](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="e658c-425">Select hello **yapılandırma dosyası** , gibi toouse ve'ı tıklatın, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e658c-425">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="e658c-426">Merhaba hello JSON dosyasının adını gördüğünüzü onaylayın **Özet** sayfasında ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="e658c-426">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="e658c-427">Tıklatın **son** hello dağıtım işlemi tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="e658c-427">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="e658c-428">Dağıttığınızda, dağıtılan tooAzure Data Factory hizmetinin hello varlıklardır önce hello hello yapılandırma dosyasından hello JSON dosyalarında özellikler için kullanılan tooset değerler değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="e658c-428">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="e658c-429">Azure Key Vault kullanma</span><span class="sxs-lookup"><span data-stu-id="e658c-429">Use Azure Key Vault</span></span>
<span data-ttu-id="e658c-430">Şu önerilir ve genellikle karşı güvenlik ilkesi toocommit bağlantı dizeleri toohello kod deposu gibi hassas verileri değil.</span><span class="sxs-lookup"><span data-stu-id="e658c-430">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="e658c-431">Bkz: [ADF güvenli yayımlama](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) Azure anahtar kasası hassas bilgilerini depolamak ve Data Factory varlıklarını yayımlanırken kullanmayla ilgili GitHub toolearn üzerinde örnek.</span><span class="sxs-lookup"><span data-stu-id="e658c-431">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="e658c-432">Visual Studio uzantısı güvenli yayımlama Hello anahtar kasasında depolanan hello gizli toobe sağlar ve yalnızca başvuruları toothem bağlantılı Hizmetleri belirtilen / dağıtım yapılandırmaları.</span><span class="sxs-lookup"><span data-stu-id="e658c-432">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="e658c-433">Data Factory varlıkları tooAzure yayımladığınızda, bu başvuruları çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="e658c-433">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="e658c-434">Bu dosyalar ardından tüm gizli gösterme olmadan kaydedilmiş toosource deposu olabilir.</span><span class="sxs-lookup"><span data-stu-id="e658c-434">These files can then be committed toosource repository without exposing any secrets.</span></span>

## <a name="summary"></a><span data-ttu-id="e658c-435">Özet</span><span class="sxs-lookup"><span data-stu-id="e658c-435">Summary</span></span>
<span data-ttu-id="e658c-436">Bu öğreticide, bir Hdınsight hadoop kümesindeki Hive betiği çalıştıran bir Azure data factory tooprocess veri oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="e658c-436">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="e658c-437">Hello Data Factory Düzenleyici'hello Azure portal toodo hello aşağıdaki adımları kullanılır:</span><span class="sxs-lookup"><span data-stu-id="e658c-437">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="e658c-438">Oluşturulan Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="e658c-438">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="e658c-439">Oluşturulan iki **bağlı hizmet**:</span><span class="sxs-lookup"><span data-stu-id="e658c-439">Created two **linked services**:</span></span>
   1. <span data-ttu-id="e658c-440">**Azure depolama** hizmet toolink toohello veri fabrikası girdi/çıktı dosyalarını tutan Azure blob depolama alanınızın bağlı.</span><span class="sxs-lookup"><span data-stu-id="e658c-440">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="e658c-441">**Azure Hdınsight** isteğe bağlı bir isteğe bağlı Hdınsight Hadoop küme toohello data factory hizmeti toolink bağlı.</span><span class="sxs-lookup"><span data-stu-id="e658c-441">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="e658c-442">Azure Data Factory Hdınsight Hadoop küme yalnızca zaman tooprocess giriş verileri hem de üretim çıktı verilerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e658c-442">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="e658c-443">Oluşturulan iki **veri kümeleri**, hello ardışık düzende Hdınsight Hive etkinliğiyle ilgili girdi ve çıktı verilerini açıklayan.</span><span class="sxs-lookup"><span data-stu-id="e658c-443">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="e658c-444">**HDInsight Hive** etkinliğine sahip oluşturulan bir **işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="e658c-444">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e658c-445">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="e658c-445">Next Steps</span></span>
<span data-ttu-id="e658c-446">Bu makalede, isteğe bağlı HDInsight kümesinde bir Hive betiği çalıştıran dönüştürme etkinliğine (HDInsight Etkinliği) sahip işlem hattı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="e658c-446">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="e658c-447">toouse Azure Blob tooAzure SQL, bir kopyalama etkinliği toocopy verileri nasıl görürüm toosee [öğretici: bir Azure blob tooAzure SQL veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="e658c-447">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="e658c-448">Merhaba çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="e658c-448">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="e658c-449">Ayrıntılı bilgi için bkz. [Data Factory’de zamanlama ve yürütme](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="e658c-449">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 


## <a name="see-also"></a><span data-ttu-id="e658c-450">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e658c-450">See Also</span></span>
| <span data-ttu-id="e658c-451">Konu</span><span class="sxs-lookup"><span data-stu-id="e658c-451">Topic</span></span> | <span data-ttu-id="e658c-452">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e658c-452">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="e658c-453">İşlem hatları</span><span class="sxs-lookup"><span data-stu-id="e658c-453">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="e658c-454">Bu makalede, işlem hatlarının ve etkinliklerin Azure Data Factory anlamanıza yardımcı olur ve nasıl toouse bunları tooconstruct veri odaklı iş akışlarının senaryo veya iş.</span><span class="sxs-lookup"><span data-stu-id="e658c-454">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="e658c-455">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="e658c-455">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="e658c-456">Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="e658c-456">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="e658c-457">Veri Dönüştürme Etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="e658c-457">Data Transformation Activities</span></span>](data-factory-data-transformation-activities.md) |<span data-ttu-id="e658c-458">Bu makalede, Azure Data Factory’nin desteklediği veri dönüştürme etkinliklerinin (bu öğreticide kullandığınız HDInsight Hive dönüştürmesi gibi) bir listesi sağlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e658c-458">This article provides a list of data transformation activities (such as HDInsight Hive transformation you used in this tutorial) supported by Azure Data Factory.</span></span> |
| [<span data-ttu-id="e658c-459">Zamanlama ve yürütme</span><span class="sxs-lookup"><span data-stu-id="e658c-459">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="e658c-460">Bu makalede Azure Data Factory uygulama modelinin hello zamanlama ve yürütme yönleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e658c-460">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="e658c-461">İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="e658c-461">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="e658c-462">Bu makalede nasıl toomonitor, yönetme ve hatalarını ayıklama işlem hatlarını izleme ve yönetim uygulaması hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="e658c-462">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
