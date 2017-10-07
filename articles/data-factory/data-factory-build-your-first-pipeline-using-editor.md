---
title: "aaaBuild ilk data factory'nizi (Azure portalı) | Microsoft Docs"
description: "Bu öğreticide Data Factory Düzenleyici'hello Azure portal kullanarak örnek bir Azure Data Factory işlem hattı oluşturacaksınız."
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
ms.openlocfilehash: fc80776001b181a59c04d80d2e05c20b107a63f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-portal"></a><span data-ttu-id="4b00b-103">Öğretici: Azure portal kullanarak ilk Azure data factory’nizi derleme</span><span class="sxs-lookup"><span data-stu-id="4b00b-103">Tutorial: Build your first Azure data factory using Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4b00b-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4b00b-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="4b00b-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="4b00b-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="4b00b-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4b00b-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="4b00b-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4b00b-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="4b00b-108">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="4b00b-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="4b00b-109">REST API</span><span class="sxs-lookup"><span data-stu-id="4b00b-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)


<span data-ttu-id="4b00b-110">Bu makalede, bilgi nasıl toouse [Azure portal](https://portal.azure.com/) toocreate ilk Azure data factory'nizi.</span><span class="sxs-lookup"><span data-stu-id="4b00b-110">In this article, you learn how toouse [Azure portal](https://portal.azure.com/) toocreate your first Azure data factory.</span></span> <span data-ttu-id="4b00b-111">diğer araçlar/SDK, kullanarak toodo hello öğretici seçin hello seçeneklerden birini hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="4b00b-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span> 

<span data-ttu-id="4b00b-112">Bu öğreticide Hello ardışık bir etkinlik vardır: **Hdınsight Hive etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="4b00b-113">Bu etkinlik dönüşümler veri tooproduce çıkış veri girişi bir Azure Hdınsight kümesinde bir hive betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="4b00b-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="4b00b-114">Başlangıç ve bitiş zamanlarını hello arasında bir ay belirtilen sonra hello ardışık düzen zamanlanmış toorun ' dir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="4b00b-115">Bu öğreticide Hello veri ardışık giriş verisi tooproduce çıktı verilerini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="4b00b-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="4b00b-116">Nasıl bir öğretici için Azure Data Factory kullanarak toocopy verileri görmek [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4b00b-116">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="4b00b-117">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-117">A pipeline can have more than one activity.</span></span> <span data-ttu-id="4b00b-118">Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-118">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="4b00b-119">Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="4b00b-119">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b00b-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4b00b-120">Prerequisites</span></span>
1. <span data-ttu-id="4b00b-121">Okuyun [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md) makale ve tam hello **önkoşul** adımları.</span><span class="sxs-lookup"><span data-stu-id="4b00b-121">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
2. <span data-ttu-id="4b00b-122">Bu makalede hello Azure Data Factory hizmetine kavramsal bir genel bakış sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-122">This article does not provide a conceptual overview of hello Azure Data Factory service.</span></span> <span data-ttu-id="4b00b-123">Gitmenizi öneririz [giriş tooAzure Data Factory](data-factory-introduction.md) hello hizmetinin makale için ayrıntılı bir genel bakış.</span><span class="sxs-lookup"><span data-stu-id="4b00b-123">We recommend that you go through [Introduction tooAzure Data Factory](data-factory-introduction.md) article for a detailed overview of hello service.</span></span>  

## <a name="create-data-factory"></a><span data-ttu-id="4b00b-124">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b00b-124">Create data factory</span></span>
<span data-ttu-id="4b00b-125">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-125">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="4b00b-126">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-126">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="4b00b-127">Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform veri tooproduct çıktı verileri girin.</span><span class="sxs-lookup"><span data-stu-id="4b00b-127">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="4b00b-128">Bu adımda hello data factory oluşturmayla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="4b00b-128">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="4b00b-129">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4b00b-129">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="4b00b-130">Tıklatın **yeni** hello sol menüsünde **veri + analiz**, tıklatıp **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-130">Click **NEW** on hello left menu, click **Data + Analytics**, and click **Data Factory**.</span></span>

   ![Dikey pencere oluşturma](./media/data-factory-build-your-first-pipeline-using-editor/create-blade.png)
3. <span data-ttu-id="4b00b-132">Merhaba, **yeni data factory** dikey penceresinde girin **GetStartedDF** hello adı için.</span><span class="sxs-lookup"><span data-stu-id="4b00b-132">In hello **New data factory** blade, enter **GetStartedDF** for hello Name.</span></span>

   ![Yeni veri fabrikası dikey penceresi](./media/data-factory-build-your-first-pipeline-using-editor/new-data-factory-blade.png)

   > [!IMPORTANT]
   > <span data-ttu-id="4b00b-134">Merhaba adı'hello Azure data Factory olması **genel benzersiz**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-134">hello name of hello Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="4b00b-135">Merhaba hatayı alırsanız: **veri fabrikası adı "GetStartedDF" kullanılabilir değil**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-135">If you receive hello error: **Data factory name “GetStartedDF” is not available**.</span></span> <span data-ttu-id="4b00b-136">Hello veri fabrikası (örneğin, yournameGetStartedDF) Hello adını değiştirin ve oluşturmayı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="4b00b-136">Change hello name of hello data factory (for example, yournameGetStartedDF) and try creating again.</span></span> <span data-ttu-id="4b00b-137">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-137">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
   >
   > <span data-ttu-id="4b00b-138">Merhaba veri fabrikasının Hello adı olarak kaydedilmesi bir **DNS** hello gelecekte olarak adlandırın ve bu nedenle herkese görünür hale gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-138">hello name of hello data factory may be registered as a **DNS** name in hello future and hence become publically visible.</span></span>
   >
   >
4. <span data-ttu-id="4b00b-139">Select hello **Azure aboneliği** oluşturulan hello veri fabrikası toobe istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-139">Select hello **Azure subscription** where you want hello data factory toobe created.</span></span>
5. <span data-ttu-id="4b00b-140">Mevcut bir **kaynak grubu** seçin ya da bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4b00b-140">Select existing **resource group** or create a resource group.</span></span> <span data-ttu-id="4b00b-141">Merhaba öğretici için adlı bir kaynak grubu oluşturun: **ADFGetStartedRG**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-141">For hello tutorial, create a resource group named: **ADFGetStartedRG**.</span></span>
6. <span data-ttu-id="4b00b-142">Select hello **konumu** hello veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="4b00b-142">Select hello **location** for hello data factory.</span></span> <span data-ttu-id="4b00b-143">Yalnızca Hello Data Factory hizmeti tarafından desteklenen bölgeler hello aşağı açılan listesinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-143">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
7. <span data-ttu-id="4b00b-144">Seçin **PIN toodashboard**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-144">Select **Pin toodashboard**.</span></span> 
8. <span data-ttu-id="4b00b-145">Tıklatın **oluşturma** hello üzerinde **yeni data factory** dikey.</span><span class="sxs-lookup"><span data-stu-id="4b00b-145">Click **Create** on hello **New data factory** blade.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4b00b-146">toocreate Data Factory örnekleri hello üyesi olmalıdır [veri fabrikası katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello abonelik/kaynak grubu düzeyinde rol.</span><span class="sxs-lookup"><span data-stu-id="4b00b-146">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
   >
   >
7. <span data-ttu-id="4b00b-147">Merhaba Panoda durumuyla döşeme hello aşağıdakilere bakın: dağıtma veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="4b00b-147">On hello dashboard, you see hello following tile with status: Deploying data factory.</span></span>    

   ![Data factory durumu oluşturma](./media/data-factory-build-your-first-pipeline-using-editor/creating-data-factory-image.png)
8. <span data-ttu-id="4b00b-149">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="4b00b-149">Congratulations!</span></span> <span data-ttu-id="4b00b-150">İlk data factory’nizi başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-150">You have successfully created your first data factory.</span></span> <span data-ttu-id="4b00b-151">Merhaba veri fabrikası başarıyla oluşturulduktan sonra gösterir hello veri fabrikası sayfasına bakın hello hello data Factory içeriği.</span><span class="sxs-lookup"><span data-stu-id="4b00b-151">After hello data factory has been created successfully, you see hello data factory page, which shows you hello contents of hello data factory.</span></span>     

    ![Data Factory dikey penceresi](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-blade.png)

<span data-ttu-id="4b00b-153">Merhaba data factory'de işlem hattı oluşturmadan önce toocreate birkaç Data Factory varlıklarını önce gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-153">Before creating a pipeline in hello data factory, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="4b00b-154">Bağlı hizmetler toolink veri depolarını/işlemlerini tooyour veri depolamak, giriş tanımlayın ve çıktı veri kümeleri toorepresent girdi/çıktı verilerini bağlı veri depolarında ve ardından bu veri kümeleri kullanan bir etkinlik hello işlem hattı oluşturma ilk oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="4b00b-154">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="4b00b-155">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b00b-155">Create linked services</span></span>
<span data-ttu-id="4b00b-156">Bu adımda, Azure Storage hesabınızı ve bir isteğe bağlı Azure Hdınsight küme tooyour data factory bağlayın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-156">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="4b00b-157">Azure depolama hesabı bu örnekteki hello ardışık düzeni için girdi ve çıktı verilerini ayrı tutma hello hello.</span><span class="sxs-lookup"><span data-stu-id="4b00b-157">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="4b00b-158">Merhaba Hdınsight bağlı hizmeti kullanılan toorun hello ardışık bu örnekteki hello etkinliğinde belirtilen Hive betiği ' dir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-158">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="4b00b-159">Ne tanımlamak [veri deposu](data-factory-data-movement-activities.md)/[işlem Hizmetleri](data-factory-compute-linked-services.md) senaryonuzda kullanılır ve bağlı hizmetler oluşturarak bu hizmetleri toohello veri fabrikası bağlayın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-159">Identify what [data store](data-factory-data-movement-activities.md)/[compute services](data-factory-compute-linked-services.md) are used in your scenario and link those services toohello data factory by creating linked services.</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="4b00b-160">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b00b-160">Create Azure Storage linked service</span></span>
<span data-ttu-id="4b00b-161">Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-161">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="4b00b-162">Bu öğreticide kullandığınız hello toostore girdi/çıktı verilerin ve HQL hello komut dosyasını aynı Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="4b00b-162">In this tutorial, you use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="4b00b-163">Tıklatın **yazar ve dağıtma** hello üzerinde **DATA FACTORY** dikey **GetStartedDF**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-163">Click **Author and deploy** on hello **DATA FACTORY** blade for **GetStartedDF**.</span></span> <span data-ttu-id="4b00b-164">Merhaba Data Factory Düzenleyici görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-164">You should see hello Data Factory Editor.</span></span>

   ![Geliştir ve dağıt kutucuğu](./media/data-factory-build-your-first-pipeline-using-editor/data-factory-author-deploy.png)
2. <span data-ttu-id="4b00b-166">**Yeni data store**’a tıklayın ve **Azure depolama**’yı seçin.</span><span class="sxs-lookup"><span data-stu-id="4b00b-166">Click **New data store** and choose **Azure storage**.</span></span>

   ![Yeni veri deposu - Azure Depolama - menü](./media/data-factory-build-your-first-pipeline-using-editor/new-data-store-azure-storage-menu.png)
3. <span data-ttu-id="4b00b-168">Görmeniz gerekir hello Azure depolama alanı oluşturmak için JSON betiği bağlantılı hizmeti hello düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="4b00b-168">You should see hello JSON script for creating an Azure Storage linked service in hello editor.</span></span>

   ![Azure Storage bağlı hizmeti](./media/data-factory-build-your-first-pipeline-using-editor/azure-storage-linked-service.png)
4. <span data-ttu-id="4b00b-170">Değiştir **hesap adı** hello Azure depolama hesabınızın adını içeren ve **hesap anahtarı** hello erişim anahtarı hello Azure depolama hesabı olan.</span><span class="sxs-lookup"><span data-stu-id="4b00b-170">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="4b00b-171">toolearn tooget depolama alanınızın erişim nasıl anahtar, hello bilgi nasıl tooview, kopyalama ve yeniden oluşturma depolama erişim anahtarları içinde hakkında [depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4b00b-171">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
5. <span data-ttu-id="4b00b-172">Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="4b00b-172">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![Dağıt düğmesi](./media/data-factory-build-your-first-pipeline-using-editor/deploy-button.png)

   <span data-ttu-id="4b00b-174">Merhaba bağlı hizmet başarıyla dağıtıldıktan sonra hello **taslak-1** penceresi görünmemelidir; gördüğünüz **AzureStorageLinkedService** hello hello soldaki ağaç görünümünde.</span><span class="sxs-lookup"><span data-stu-id="4b00b-174">After hello linked service is deployed successfully, hello **Draft-1** window should disappear and you see **AzureStorageLinkedService** in hello tree view on hello left.</span></span>

    ![Menüde Storage Bağlı Hizmeti](./media/data-factory-build-your-first-pipeline-using-editor/StorageLinkedServiceInTree.png)    

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="4b00b-176">Azure HDInsight bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b00b-176">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="4b00b-177">Bu adımda, bir isteğe bağlı Hdınsight kümesi tooyour data factory bağlayın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-177">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="4b00b-178">Merhaba Hdınsight küme otomatik olarak çalışma zamanında oluşturulur ve hello belirtilen süre boyunca işlem yapma ve boşta bittikten sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-178">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span>

1. <span data-ttu-id="4b00b-179">Merhaba, **Data Factory düzenleyici**, tıklatın **... Diğer**, **Yeni işlem** öğelerine tıklayın ve **İsteğe bağlı HDInsight kümesi**’ni seçin.</span><span class="sxs-lookup"><span data-stu-id="4b00b-179">In hello **Data Factory Editor**, click **... More**, click **New compute**, and select **On-demand HDInsight cluster**.</span></span>

    ![Yeni işlem](./media/data-factory-build-your-first-pipeline-using-editor/new-compute-menu.png)
2. <span data-ttu-id="4b00b-181">Aşağıdaki kod parçacığında toohello hello kopyalayıp **taslak-1** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4b00b-181">Copy and paste hello following snippet toohello **Draft-1** window.</span></span> <span data-ttu-id="4b00b-182">Merhaba JSON parçacığında kullanılan toocreate hello Hdınsight küme isteğe bağlı hello özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="4b00b-182">hello JSON snippet describes hello properties that are used toocreate hello HDInsight cluster on-demand.</span></span>

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

    <span data-ttu-id="4b00b-183">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="4b00b-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="4b00b-184">Özellik</span><span class="sxs-lookup"><span data-stu-id="4b00b-184">Property</span></span> | <span data-ttu-id="4b00b-185">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4b00b-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="4b00b-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="4b00b-186">ClusterSize</span></span> |<span data-ttu-id="4b00b-187">Merhaba Hdınsight kümesi Hello boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="4b00b-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="4b00b-188">TimeToLive</span></span> | <span data-ttu-id="4b00b-189">Silinmeden önce hello Hdınsight kümesi, o hello boşta kalma süresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="4b00b-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4b00b-190">linkedServiceName</span></span> | <span data-ttu-id="4b00b-191">Hdınsight tarafından oluşturulan kullanılan toostore hello günlükleri olan hello depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight.</span></span> |

    <span data-ttu-id="4b00b-192">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="4b00b-192">Note hello following points:</span></span>

   * <span data-ttu-id="4b00b-193">Merhaba Data Factory oluşturur bir **Linux tabanlı** hello JSON ile sizin için Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="4b00b-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="4b00b-194">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="4b00b-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="4b00b-195">İsteğe bağlı HDInsight kümesi yerine **kendi HDInsight kümenizi** kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="4b00b-196">Ayrıntılar için bkz. [HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="4b00b-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="4b00b-197">Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello JSON belirtilen hello blob depolamada (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="4b00b-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="4b00b-198">Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez.</span><span class="sxs-lookup"><span data-stu-id="4b00b-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="4b00b-199">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-199">This behavior is by design.</span></span> <span data-ttu-id="4b00b-200">İsteğe bağlı HDInsight bağlı hizmeti kullanıldığında, mevcut canlı bir küme olmadığı sürece bir dilim her işlendiğinde bir HDInsight kümesi oluşturulur (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="4b00b-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="4b00b-201">Merhaba işlem bittiğinde hello küme otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="4b00b-202">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="4b00b-203">Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti.</span><span class="sxs-lookup"><span data-stu-id="4b00b-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="4b00b-204">Bu kapsayıcıların Hello adları izleyen bir desen: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="4b00b-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="4b00b-205">Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.</span><span class="sxs-lookup"><span data-stu-id="4b00b-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="4b00b-206">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="4b00b-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
3. <span data-ttu-id="4b00b-207">Tıklatın **dağıtma** toodeploy hello bağlantılı hizmet çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="4b00b-207">Click **Deploy** on hello command bar toodeploy hello linked service.</span></span>

    ![İsteğe bağlı HDInsight bağlı hizmetini dağıtma](./media/data-factory-build-your-first-pipeline-using-editor/ondemand-hdinsight-deploy.png)
4. <span data-ttu-id="4b00b-209">Her ikisi de gördüğünüzü onaylayın **AzureStorageLinkedService** ve **Hdınsightondemandlinkedservice** hello hello soldaki ağaç görünümünde.</span><span class="sxs-lookup"><span data-stu-id="4b00b-209">Confirm that you see both **AzureStorageLinkedService** and **HDInsightOnDemandLinkedService** in hello tree view on hello left.</span></span>

    ![Bağlı hizmetlerin bulunduğu ağaç görünümü](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-linked-services.png)

## <a name="create-datasets"></a><span data-ttu-id="4b00b-211">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b00b-211">Create datasets</span></span>
<span data-ttu-id="4b00b-212">Bu adımda, veri kümeleri toorepresent hello girişi oluşturun ve Hive işlenmesi için verileri çıktı.</span><span class="sxs-lookup"><span data-stu-id="4b00b-212">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="4b00b-213">Bu veri kümeleri toohello başvuran **AzureStorageLinkedService** Bu öğreticide daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-213">These datasets refer toohello **AzureStorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="4b00b-214">bağlantılı hizmet noktaları tooan Azure depolama hesabı hello ve veri kümeleri, giriş tutan hello depolamada kapsayıcı, klasör, dosya adı belirtin ve çıktı verilerini.</span><span class="sxs-lookup"><span data-stu-id="4b00b-214">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>   

### <a name="create-input-dataset"></a><span data-ttu-id="4b00b-215">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b00b-215">Create input dataset</span></span>
1. <span data-ttu-id="4b00b-216">Merhaba, **Data Factory düzenleyici**, tıklatın **... Daha fazla** hello komut çubuğunda **yeni veri kümesi**seçip **Azure Blob Depolama**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-216">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>

    ![Yeni veri kümesi](./media/data-factory-build-your-first-pipeline-using-editor/new-data-set.png)
2. <span data-ttu-id="4b00b-218">Aşağıdaki kod parçacığında toohello taslak-1 penceresinde hello kopyalayıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-218">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="4b00b-219">Merhaba JSON parçacığında adlı bir veri kümesi oluşturmakta olduğunuz **Azureblobınput** hello ardışık düzeninde bir etkinliğin girdi verilerini temsil eden.</span><span class="sxs-lookup"><span data-stu-id="4b00b-219">In hello JSON snippet, you are creating a dataset called **AzureBlobInput** that represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="4b00b-220">Ayrıca, hello giriş verisi adlı hello blob kapsayıcısında bulunur belirttiğiniz **adfgetstarted** ve adlı hello klasör **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-220">In addition, you specify that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

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
    <span data-ttu-id="4b00b-221">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="4b00b-221">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="4b00b-222">Özellik</span><span class="sxs-lookup"><span data-stu-id="4b00b-222">Property</span></span> | <span data-ttu-id="4b00b-223">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4b00b-223">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="4b00b-224">type</span><span class="sxs-lookup"><span data-stu-id="4b00b-224">type</span></span> |<span data-ttu-id="4b00b-225">Merhaba type özelliği çok ayarlamak**AzureBlob** verileri Azure blob depolama alanında bulunduğundan.</span><span class="sxs-lookup"><span data-stu-id="4b00b-225">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
   | <span data-ttu-id="4b00b-226">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4b00b-226">linkedServiceName</span></span> |<span data-ttu-id="4b00b-227">Toohello başvuruyor **AzureStorageLinkedService** daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-227">Refers toohello **AzureStorageLinkedService** you created earlier.</span></span> |
   | <span data-ttu-id="4b00b-228">folderPath</span><span class="sxs-lookup"><span data-stu-id="4b00b-228">folderPath</span></span> | <span data-ttu-id="4b00b-229">Merhaba blob belirtir **kapsayıcı** ve hello **klasörü** giriş BLOB'ları içerir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-229">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> | 
   | <span data-ttu-id="4b00b-230">fileName</span><span class="sxs-lookup"><span data-stu-id="4b00b-230">fileName</span></span> |<span data-ttu-id="4b00b-231">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4b00b-231">This property is optional.</span></span> <span data-ttu-id="4b00b-232">Bu özelliği atarsanız, hello folderPath tüm hello dosyalarından çekilir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-232">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="4b00b-233">Bu öğreticide, yalnızca hello **input.log** işlenir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-233">In this tutorial, only hello **input.log** is processed.</span></span> |
   | <span data-ttu-id="4b00b-234">type</span><span class="sxs-lookup"><span data-stu-id="4b00b-234">type</span></span> |<span data-ttu-id="4b00b-235">Merhaba günlük dosyaları metin biçiminde kullandığımız için olan **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-235">hello log files are in text format, so we use **TextFormat**.</span></span> |
   | <span data-ttu-id="4b00b-236">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="4b00b-236">columnDelimiter</span></span> |<span data-ttu-id="4b00b-237">Merhaba günlük dosyalarındaki sütunlar tarafından ayrılmış **virgül karakteriyle (`,`)**</span><span class="sxs-lookup"><span data-stu-id="4b00b-237">columns in hello log files are delimited by **comma character (`,`)**</span></span> |
   | <span data-ttu-id="4b00b-238">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="4b00b-238">frequency/interval</span></span> |<span data-ttu-id="4b00b-239">sıklığını çok**ay** ve aralığı **1**, kullanılabilir aylık olan dilimler giriş o hello anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-239">frequency set too**Month** and interval is **1**, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="4b00b-240">external</span><span class="sxs-lookup"><span data-stu-id="4b00b-240">external</span></span> | <span data-ttu-id="4b00b-241">Bu özellik çok ayarlanır**true** hello giriş verileri bu ardışık düzen tarafından oluşturulmamış olması durumunda.</span><span class="sxs-lookup"><span data-stu-id="4b00b-241">This property is set too**true** if hello input data is not generated by this pipeline.</span></span> <span data-ttu-id="4b00b-242">Bu öğreticide, hello özelliği tootrue ayarlarız şekilde hello input.log dosyası bu ardışık düzen tarafından oluşturulmaz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-242">In this tutorial, hello input.log file is not generated by this pipeline, so we set hello property tootrue.</span></span> |

    <span data-ttu-id="4b00b-243">Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4b00b-243">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="4b00b-244">Tıklatın **dağıtma** toodeploy yeni oluşturulan hello dataset çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="4b00b-244">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span> <span data-ttu-id="4b00b-245">Merhaba dataset hello hello soldaki ağaç görünümünde görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-245">You should see hello dataset in hello tree view on hello left.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="4b00b-246">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b00b-246">Create output dataset</span></span>
<span data-ttu-id="4b00b-247">Şimdi, hello çıkış veri kümesi toorepresent hello çıktı verilerini hello Azure Blob Depolama depolanan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4b00b-247">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="4b00b-248">Merhaba, **Data Factory düzenleyici**, tıklatın **... Daha fazla** hello komut çubuğunda **yeni veri kümesi**seçip **Azure Blob Depolama**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-248">In hello **Data Factory Editor**, click **... More** on hello command bar, click **New dataset**, and select **Azure Blob storage**.</span></span>  
2. <span data-ttu-id="4b00b-249">Aşağıdaki kod parçacığında toohello taslak-1 penceresinde hello kopyalayıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-249">Copy and paste hello following snippet toohello Draft-1 window.</span></span> <span data-ttu-id="4b00b-250">Merhaba JSON parçacığında adlı bir veri kümesi oluşturmakta olduğunuz **AzureBlobOutput**ve hello Hive betiği tarafından üretilen hello verilerin hello yapısını belirtme.</span><span class="sxs-lookup"><span data-stu-id="4b00b-250">In hello JSON snippet, you are creating a dataset called **AzureBlobOutput**, and specifying hello structure of hello data that is produced by hello Hive script.</span></span> <span data-ttu-id="4b00b-251">Ayrıca, hello sonuçları adlı hello blob kapsayıcısında depolanır belirttiğiniz **adfgetstarted** ve adlı hello klasör **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-251">In addition, you specify that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="4b00b-252">Merhaba **kullanılabilirlik** bölümü belirtiyor bu hello çıktı veri kümesi, aylık olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4b00b-252">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>

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
    <span data-ttu-id="4b00b-253">Bkz: **hello girdi veri kümesi oluşturma** bu özelliklerin açıklamaları için bölüm.</span><span class="sxs-lookup"><span data-stu-id="4b00b-253">See **Create hello input dataset** section for descriptions of these properties.</span></span> <span data-ttu-id="4b00b-254">Merhaba dataset hello Data Factory hizmeti tarafından oluşturulduğundan çıktı veri hello dış özelliği ayarlı değil.</span><span class="sxs-lookup"><span data-stu-id="4b00b-254">You do not set hello external property on an output dataset as hello dataset is produced by hello Data Factory service.</span></span>
3. <span data-ttu-id="4b00b-255">Tıklatın **dağıtma** toodeploy yeni oluşturulan hello dataset çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="4b00b-255">Click **Deploy** on hello command bar toodeploy hello newly created dataset.</span></span>
4. <span data-ttu-id="4b00b-256">Bu hello veri kümesi başarıyla oluşturuldu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-256">Verify that hello dataset is created successfully.</span></span>

    ![Bağlı hizmetlerin bulunduğu ağaç görünümü](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-data-set.png)

## <a name="create-pipeline"></a><span data-ttu-id="4b00b-258">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4b00b-258">Create pipeline</span></span>
<span data-ttu-id="4b00b-259">Bu adımda, **HDInsightHive** etkinliğiyle ilk işlem hattınızı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-259">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="4b00b-260">Girdi dilimi kullanılabilir aylık (sıklığı: Month, interval: 1), çıktı diliminin ayda bir oluşturulduğunu ve hello etkinlik hello Zamanlayıcı özelliğinin de toomonthly ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-260">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="4b00b-261">Merhaba çıktı veri kümesi ve hello etkinlik Zamanlayıcı Hello ayarlarının eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-261">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="4b00b-262">Şu anda, çıktı veri kümesi hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir böylece hangi sürücüleri zamanlama, hello değil.</span><span class="sxs-lookup"><span data-stu-id="4b00b-262">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="4b00b-263">Merhaba etkinlik herhangi bir girdi almazsa oluşturma hello girdi veri kümesi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-263">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="4b00b-264">JSON aşağıdaki hello kullanılan hello özellikleri hello bu bölümün sonuna açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="4b00b-264">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="4b00b-265">Merhaba, **Data Factory düzenleyici**, tıklatın **üç nokta (...) Daha fazla komut** ve ardından **yeni işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-265">In hello **Data Factory Editor**, click **Ellipsis (…) More commands** and then click **New pipeline**.</span></span>

    ![yeni işlem hattı düğmesi](./media/data-factory-build-your-first-pipeline-using-editor/new-pipeline-button.png)
2. <span data-ttu-id="4b00b-267">Aşağıdaki kod parçacığında toohello taslak-1 penceresinde hello kopyalayıp yeniden açın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-267">Copy and paste hello following snippet toohello Draft-1 window.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="4b00b-268">Değiştir **storageaccountname** depolama hesabınızdaki hello JSON hello adı.</span><span class="sxs-lookup"><span data-stu-id="4b00b-268">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
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

    <span data-ttu-id="4b00b-269">Merhaba JSON parçacığında, Hdınsight kümesinde Hive tooprocess veri kullanan tek bir etkinlik oluşan bir işlem hattı oluşturuyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-269">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="4b00b-270">Merhaba Hive betik dosyası **partitionweblogs.hql**, hello Azure depolama hesabı depolanır (adlı hello scriptLinkedService tarafından belirtilen **AzureStorageLinkedService**) ve  **komut dosyası** hello kapsayıcı klasöründe **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-270">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **AzureStorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="4b00b-271">Merhaba **tanımlar** bölümdür toohello hive betiğini Hive yapılandırma değerleri olarak geçirilir kullanılan toospecify hello çalışma zamanı ayarları (örn., ${hiveconf: inputtable}, ${hiveconf}).</span><span class="sxs-lookup"><span data-stu-id="4b00b-271">hello **defines** section is used toospecify hello runtime settings that are passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="4b00b-272">Merhaba **Başlat** ve **son** hello ardışık düzen özelliklerini hello etkin dönem hello ardışık belirtir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-272">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="4b00b-273">Bu hello Hive betiğini hello tarafından belirtilen hello işlem üzerinde çalıştığı belirtin Hello JSON etkinliğinde **linkedServiceName** – **Hdınsightondemandlinkedservice**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-273">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4b00b-274">"Ardışık düzen JSON" bölümüne bakın [işlem hatlarının ve etkinliklerin Azure Data Factory](data-factory-create-pipelines.md) hello örnekte kullanılan JSON özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4b00b-274">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties used in hello example.</span></span>
   >
   >
3. <span data-ttu-id="4b00b-275">Merhaba aşağıdakileri doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="4b00b-275">Confirm hello following:</span></span>

   1. <span data-ttu-id="4b00b-276">**input.log** dosyasından hello **inputdata** hello klasörünü **adfgetstarted** hello Azure blob depolama kapsayıcısında</span><span class="sxs-lookup"><span data-stu-id="4b00b-276">**input.log** file exists in hello **inputdata** folder of hello **adfgetstarted** container in hello Azure blob storage</span></span>
   2. <span data-ttu-id="4b00b-277">**partitionweblogs.hql** dosyasından hello **betik** hello klasörünü **adfgetstarted** hello Azure blob depolama kapsayıcısında.</span><span class="sxs-lookup"><span data-stu-id="4b00b-277">**partitionweblogs.hql** file exists in hello **script** folder of hello **adfgetstarted** container in hello Azure blob storage.</span></span> <span data-ttu-id="4b00b-278">Tam hello önkoşul adımları hello [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md) bu dosyaları görmüyorsanız.</span><span class="sxs-lookup"><span data-stu-id="4b00b-278">Complete hello prerequisite steps in hello [Tutorial Overview](data-factory-build-your-first-pipeline.md) if you don't see these files.</span></span>
   3. <span data-ttu-id="4b00b-279">Değiştirdiğinizi onaylayın **storageaccountname** depolama hesabınızdaki hello hello adıyla JSON kanalı.</span><span class="sxs-lookup"><span data-stu-id="4b00b-279">Confirm that you replaced **storageaccountname** with hello name of your storage account in hello pipeline JSON.</span></span>
4. <span data-ttu-id="4b00b-280">Tıklatın **dağıtma** toodeploy hello ardışık çubuğu hello komutu.</span><span class="sxs-lookup"><span data-stu-id="4b00b-280">Click **Deploy** on hello command bar toodeploy hello pipeline.</span></span> <span data-ttu-id="4b00b-281">Merhaba itibaren **Başlat** ve **son** hello son kez ayarlanır ve **isPaused** dağıtıldıktan hemen sonra kümesi toofalse, hello ardışık düzen (Merhaba ardışık düzeninde etkinlik) çalışması olduğu.</span><span class="sxs-lookup"><span data-stu-id="4b00b-281">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>
5. <span data-ttu-id="4b00b-282">Merhaba ardışık hello ağaç görünümünde gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-282">Confirm that you see hello pipeline in hello tree view.</span></span>

    ![İşlem hattının bulunduğu ağaç görünümü](./media/data-factory-build-your-first-pipeline-using-editor/tree-view-pipeline.png)
6. <span data-ttu-id="4b00b-284">Tebrikler, ilk işlem hattınızı başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-284">Congratulations, you have successfully created your first pipeline!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="4b00b-285">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="4b00b-285">Monitor pipeline</span></span>
### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="4b00b-286">Diyagram Görünümünü kullanarak işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="4b00b-286">Monitor pipeline using Diagram View</span></span>
1. <span data-ttu-id="4b00b-287">Tıklatın **X** tooclose Data Factory Düzenleyici dikey toonavigate toohello Data Factory dikey penceresine geri tıklatın ve **diyagramı**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-287">Click **X** tooclose Data Factory Editor blades and toonavigate back toohello Data Factory blade, and click **Diagram**.</span></span>

    ![Diyagram kutucuğu](./media/data-factory-build-your-first-pipeline-using-editor/diagram-tile.png)
2. <span data-ttu-id="4b00b-289">Hello diyagram görünümü, hello ardışık düzen ve Bu öğreticide kullanılan veri kümelerine genel bakış konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-289">In hello Diagram View, you see an overview of hello pipelines, and datasets used in this tutorial.</span></span>

    ![Diyagram Görünümü](./media/data-factory-build-your-first-pipeline-using-editor/diagram-view-2.png)
3. <span data-ttu-id="4b00b-291">tooview hello düzenindeki hello sağ kanaldaki tüm etkinlikleri Diyagram ve ardışık düzeni Aç'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-291">tooview all activities in hello pipeline, right-click pipeline in hello diagram and click Open Pipeline.</span></span>

    ![İşlem hattı menüsünü açma](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-menu.png)
4. <span data-ttu-id="4b00b-293">Merhaba ardışık düzeninde hello Hdınsighthive etkinliğini gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-293">Confirm that you see hello HDInsightHive activity in hello pipeline.</span></span>

    ![İşlem hattı görünümünü açma](./media/data-factory-build-your-first-pipeline-using-editor/open-pipeline-view.png)

    <span data-ttu-id="4b00b-295">toonavigate toohello önceki görünüme geri tıklatın **veri fabrikası** hello içerik haritası menüsünde hello üstünde.</span><span class="sxs-lookup"><span data-stu-id="4b00b-295">toonavigate back toohello previous view, click **Data factory** in hello breadcrumb menu at hello top.</span></span>
5. <span data-ttu-id="4b00b-296">Merhaba, **diyagram görünümü**, hello dataset çift **Azureblobınput**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-296">In hello **Diagram View**, double-click hello dataset **AzureBlobInput**.</span></span> <span data-ttu-id="4b00b-297">Bu hello dilim onaylayın **hazır** durumu.</span><span class="sxs-lookup"><span data-stu-id="4b00b-297">Confirm that hello slice is in **Ready** state.</span></span> <span data-ttu-id="4b00b-298">Bu işlem birkaç dakika hello dilim tooshow için hazır durumda kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-298">It may take a couple of minutes for hello slice tooshow up in Ready state.</span></span> <span data-ttu-id="4b00b-299">Bir süre bekledikten sonra gerçekleşmez hello doğru kapsayıcıda (adfgetstarted) ve klasörde (inputdata) yerleştirilen hello girdi dosyasının (input.log) yüklü olup olmadığına bakın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-299">If it does not happen after you wait for sometime, see if you have hello input file (input.log) placed in hello right container (adfgetstarted) and folder (inputdata).</span></span>

   ![Girdi dilimi hazır durumda](./media/data-factory-build-your-first-pipeline-using-editor/input-slice-ready.png)
6. <span data-ttu-id="4b00b-301">Tıklatın **X** tooclose **Azureblobınput** dikey.</span><span class="sxs-lookup"><span data-stu-id="4b00b-301">Click **X** tooclose **AzureBlobInput** blade.</span></span>
7. <span data-ttu-id="4b00b-302">Merhaba, **diyagram görünümü**, hello dataset çift **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-302">In hello **Diagram View**, double-click hello dataset **AzureBlobOutput**.</span></span> <span data-ttu-id="4b00b-303">İşlenmekte olan bu hello dilim bakın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-303">You see that hello slice that is currently being processed.</span></span>

   ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-editor/dataset-blade.png)
8. <span data-ttu-id="4b00b-305">İşlem bittiğinde hello dilimi bkz **hazır** durumu.</span><span class="sxs-lookup"><span data-stu-id="4b00b-305">When processing is done, you see hello slice in **Ready** state.</span></span>

   ![Veri kümesi](./media/data-factory-build-your-first-pipeline-using-editor/dataset-slice-ready.png)  

   > [!IMPORTANT]
   > <span data-ttu-id="4b00b-307">İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika).</span><span class="sxs-lookup"><span data-stu-id="4b00b-307">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="4b00b-308">Bu nedenle, hello ardışık düzen beklediğiniz çok ele **yaklaşık olarak 30 dakika** tooprocess hello dilim.</span><span class="sxs-lookup"><span data-stu-id="4b00b-308">Therefore, expect hello pipeline too      take **approximately 30 minutes** tooprocess hello slice.</span></span>
   >
   >

9. <span data-ttu-id="4b00b-309">Merhaba dilim olduğunda **hazır** durum, hello denetleyin **partitioneddata** hello klasöründe **adfgetstarted** hello için blob depolama alanınızın kapsayıcısında çıkış verileri.</span><span class="sxs-lookup"><span data-stu-id="4b00b-309">When hello slice is in **Ready** state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  

   ![çıktı verileri](./media/data-factory-build-your-first-pipeline-using-editor/three-ouptut-files.png)
10. <span data-ttu-id="4b00b-311">Merhaba dilim toosee ayrıntılarını içinde tıklatın bir **veri dilimi** dikey.</span><span class="sxs-lookup"><span data-stu-id="4b00b-311">Click hello slice toosee details about it in a **Data slice** blade.</span></span>

   ![Veri dilimi ayrıntıları](./media/data-factory-build-your-first-pipeline-using-editor/data-slice-details.png)  
11. <span data-ttu-id="4b00b-313">Hello çalıştırmak bir etkinliği **etkinlik çalışır listesi** toosee etkinliği hakkında ayrıntılı bir çalıştır (Senaryomuzda Hive etkinliğiyle) bir **etkinlik çalışma ayrıntıları** penceresi.</span><span class="sxs-lookup"><span data-stu-id="4b00b-313">Click an activity run in hello **Activity runs list** toosee details about an activity run (Hive activity in our scenario) in an **Activity run details** window.</span></span>   

   ![Etkinlik çalışma ayrıntıları](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-blade.png)    

   <span data-ttu-id="4b00b-315">Merhaba günlük dosyalarından yürütüldü hello Hive sorgusu ve durum bilgileri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-315">From hello log files, you can see hello Hive query that was executed and status information.</span></span> <span data-ttu-id="4b00b-316">Bu günlükler her türlü sorunu gidermek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="4b00b-316">These logs are useful for troubleshooting any issues.</span></span>
   <span data-ttu-id="4b00b-317">Daha fazla ayrıntı için [Azure portal dikey penceresi kullanılarak işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-pipelines.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="4b00b-317">See [Monitor and manage pipelines using Azure portal blades](data-factory-monitor-manage-pipelines.md) article for more details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b00b-318">Merhaba dilim başarıyla işlendiğinde hello girdi dosyası silinir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-318">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="4b00b-319">Bu nedenle, toorerun hello dilim istediğiniz veya öğreticiyi yeniden Merhaba, hello adfgetstarted kapsayıcısının hello girdi dosyasını (input.log) toohello inputdata klasörüne yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4b00b-319">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="4b00b-320">İzleme ve Yönetme Uygulamasını kullanarak işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="4b00b-320">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="4b00b-321">İzleyicisi'ni kullanın ve uygulama toomonitor hatlarınızı yönetme.</span><span class="sxs-lookup"><span data-stu-id="4b00b-321">You can also use Monitor & Manage application toomonitor your pipelines.</span></span> <span data-ttu-id="4b00b-322">Bu uygulamanın kullanımına ilişkin ayrıntılı bilgi için bkz. [İzleme ve Yönetme Uygulamasını kullanarak Azure Data Factory işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="4b00b-322">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

1. <span data-ttu-id="4b00b-323">Tıklatın **İzleyici & Yönet** döşeme hello veri fabrikanızın giriş sayfasında.</span><span class="sxs-lookup"><span data-stu-id="4b00b-323">Click **Monitor & Manage** tile on hello home page for your data factory.</span></span>

    ![İzleme ve Yönetme kutucuğu](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-tile.png)
2. <span data-ttu-id="4b00b-325">**İzleme ve Yönetme uygulaması**’nı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="4b00b-325">You should see **Monitor & Manage application**.</span></span> <span data-ttu-id="4b00b-326">Değişiklik hello **başlangıç zamanı** ve **bitiş saati** toomatch başlangıç ve bitiş zamanları, ardışık ve tıklatın **Uygula**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-326">Change hello **Start time** and **End time** toomatch start and end times of your pipeline, and click **Apply**.</span></span>

    ![İzleme ve Yönetme Uygulaması](./media/data-factory-build-your-first-pipeline-using-editor/monitor-and-manage-app.png)
3. <span data-ttu-id="4b00b-328">Bir etkinlik penceresinde hello seçin **etkinlik Windows** toosee ayrıntılarını listeler.</span><span class="sxs-lookup"><span data-stu-id="4b00b-328">Select an activity window in hello **Activity Windows** list toosee details about it.</span></span>

    ![Etkinlik penceresi ayrıntıları](./media/data-factory-build-your-first-pipeline-using-editor/activity-window-details.png)

## <a name="summary"></a><span data-ttu-id="4b00b-330">Özet</span><span class="sxs-lookup"><span data-stu-id="4b00b-330">Summary</span></span>
<span data-ttu-id="4b00b-331">Bu öğreticide, bir Hdınsight hadoop kümesindeki Hive betiği çalıştıran bir Azure data factory tooprocess veri oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="4b00b-331">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="4b00b-332">Hello Data Factory Düzenleyici'hello Azure portal toodo hello aşağıdaki adımları kullanılır:</span><span class="sxs-lookup"><span data-stu-id="4b00b-332">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>  

1. <span data-ttu-id="4b00b-333">Oluşturulan Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-333">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="4b00b-334">Oluşturulan iki **bağlı hizmet**:</span><span class="sxs-lookup"><span data-stu-id="4b00b-334">Created two **linked services**:</span></span>
   1. <span data-ttu-id="4b00b-335">**Azure depolama** hizmet toolink toohello veri fabrikası girdi/çıktı dosyalarını tutan Azure blob depolama alanınızın bağlı.</span><span class="sxs-lookup"><span data-stu-id="4b00b-335">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="4b00b-336">**Azure Hdınsight** isteğe bağlı bir isteğe bağlı Hdınsight Hadoop küme toohello data factory hizmeti toolink bağlı.</span><span class="sxs-lookup"><span data-stu-id="4b00b-336">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="4b00b-337">Azure Data Factory Hdınsight Hadoop küme yalnızca zaman tooprocess giriş verileri hem de üretim çıktı verilerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="4b00b-337">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="4b00b-338">Oluşturulan iki **veri kümeleri**, hello ardışık düzende Hdınsight Hive etkinliğiyle ilgili girdi ve çıktı verilerini açıklayan.</span><span class="sxs-lookup"><span data-stu-id="4b00b-338">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="4b00b-339">**HDInsight Hive** etkinliğine sahip oluşturulan bir **işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="4b00b-339">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b00b-340">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="4b00b-340">Next Steps</span></span>
<span data-ttu-id="4b00b-341">Bu makalede, isteğe bağlı HDInsight kümesinde bir Hive betiği çalıştıran dönüştürme etkinliğine (HDInsight Etkinliği) sahip işlem hattı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-341">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand HDInsight cluster.</span></span> <span data-ttu-id="4b00b-342">toouse Azure Blob tooAzure SQL, bir kopyalama etkinliği toocopy verileri nasıl görürüm toosee [öğretici: bir Azure blob tooAzure SQL veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4b00b-342">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="4b00b-343">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="4b00b-343">See Also</span></span>
| <span data-ttu-id="4b00b-344">Konu</span><span class="sxs-lookup"><span data-stu-id="4b00b-344">Topic</span></span> | <span data-ttu-id="4b00b-345">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4b00b-345">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="4b00b-346">İşlem hatları</span><span class="sxs-lookup"><span data-stu-id="4b00b-346">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="4b00b-347">Bu makalede, işlem hatlarının ve etkinliklerin Azure Data Factory anlamanıza yardımcı olur ve nasıl toouse bunları tooconstruct uçtan uca veri odaklı iş akışlarının senaryo veya iş.</span><span class="sxs-lookup"><span data-stu-id="4b00b-347">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="4b00b-348">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="4b00b-348">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="4b00b-349">Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4b00b-349">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="4b00b-350">Zamanlama ve yürütme</span><span class="sxs-lookup"><span data-stu-id="4b00b-350">Scheduling and execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="4b00b-351">Bu makalede Azure Data Factory uygulama modelinin hello zamanlama ve yürütme yönleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4b00b-351">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="4b00b-352">İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="4b00b-352">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="4b00b-353">Bu makalede nasıl toomonitor, yönetme ve hatalarını ayıklama işlem hatlarını izleme ve yönetim uygulaması hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4b00b-353">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
