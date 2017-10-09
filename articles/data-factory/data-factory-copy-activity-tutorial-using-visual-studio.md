---
title: "Öğretici: Visual Studio kullanarak Kopyalama Etkinliği ile işlem hattı oluşturma | Microsoft Belgeleri"
description: "Bu öğreticide, Visual Studio kullanarak Kopyalama Etkinliği ile bir Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1751185b-ce0a-4ab2-a9c3-e37b4d149ca3
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: d99d8875807bab41f5122ab95a09f83f82923529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-visual-studio"></a><span data-ttu-id="7c9ea-103">Öğretici: Visual Studio kullanarak Kopyalama Etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-103">Tutorial: Create a pipeline with Copy Activity using Visual Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7c9ea-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7c9ea-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="7c9ea-105">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="7c9ea-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="7c9ea-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7c9ea-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="7c9ea-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c9ea-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="7c9ea-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c9ea-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="7c9ea-109">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="7c9ea-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="7c9ea-110">REST API</span><span class="sxs-lookup"><span data-stu-id="7c9ea-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="7c9ea-111">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="7c9ea-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="7c9ea-112">Bu makalede, nasıl toouse hello Microsoft Visual Studio toocreate data factory Azure blob depolama tooan Azure SQL veritabanına verileri kopyalayan bir işlem hattı ile bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-112">In this article, you learn how toouse hello Microsoft Visual Studio toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="7c9ea-113">Yeni tooAzure Data Factory varsa, hello okuma [giriş tooAzure Data Factory](data-factory-introduction.md) Bu öğretici yapmadan önce makalesi.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="7c9ea-114">Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="7c9ea-115">Merhaba kopyalama etkinliği bir desteklenen veri deposu tooa desteklenen havuz veri deposundan verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="7c9ea-116">Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="7c9ea-117">Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="7c9ea-118">Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="7c9ea-119">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="7c9ea-120">Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="7c9ea-121">Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE] 
> <span data-ttu-id="7c9ea-122">Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-122">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="7c9ea-123">Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-123">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7c9ea-124">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7c9ea-124">Prerequisites</span></span>
1. <span data-ttu-id="7c9ea-125">Okuyun [öğreticiye genel bakış](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) makale ve tam hello **önkoşul** adımları.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-125">Read through [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article and complete hello **prerequisite** steps.</span></span>       
2. <span data-ttu-id="7c9ea-126">toocreate Data Factory örnekleri hello üyesi olmalıdır [veri fabrikası katkıda bulunan](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) hello abonelik/kaynak grubu düzeyinde rol.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-126">toocreate Data Factory instances, you must be a member of hello [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at hello subscription/resource group level.</span></span>
3. <span data-ttu-id="7c9ea-127">Merhaba aşağıdakilerin yüklü olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-127">You must have hello following installed on your computer:</span></span> 
   * <span data-ttu-id="7c9ea-128">Visual Studio 2013 veya Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="7c9ea-128">Visual Studio 2013 or Visual Studio 2015</span></span>
   * <span data-ttu-id="7c9ea-129">Visual Studio 2013 veya Visual Studio 2015 için Azure SDK’sını indirin.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-129">Download Azure SDK for Visual Studio 2013 or Visual Studio 2015.</span></span> <span data-ttu-id="7c9ea-130">Çok gidin[Azure indirme sayfası](https://azure.microsoft.com/downloads/) tıklatıp **VS 2013** veya **VS 2015** hello içinde **.NET** bölümü.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-130">Navigate too[Azure Download Page](https://azure.microsoft.com/downloads/) and click **VS 2013** or **VS 2015** in hello **.NET** section.</span></span>
   * <span data-ttu-id="7c9ea-131">Visual Studio için Hello en son Azure Data Factory eklentisini indirin: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) veya [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-131">Download hello latest Azure Data Factory plugin for Visual Studio: [VS 2013](https://visualstudiogallery.msdn.microsoft.com/754d998c-8f92-4aa7-835b-e89c8c954aa5) or [VS 2015](https://visualstudiogallery.msdn.microsoft.com/371a4cf9-0093-40fa-b7dd-be3c74f49005).</span></span> <span data-ttu-id="7c9ea-132">Aşağıdaki adımları hello yaparak hello eklentisi güncelleştirebilirsiniz: hello menüsünde **Araçları** -> **Uzantılar ve güncelleştirmeler** -> **çevrimiçi**  ->  **Visual Studio Galerisi** -> **Visual Studio için Microsoft Azure Data Factory Araçları** -> **güncelleştirme**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-132">You can also update hello plugin by doing hello following steps: On hello menu, click **Tools** -> **Extensions and Updates** -> **Online** -> **Visual Studio Gallery** -> **Microsoft Azure Data Factory Tools for Visual Studio** -> **Update**.</span></span>

## <a name="steps"></a><span data-ttu-id="7c9ea-133">Adımlar</span><span class="sxs-lookup"><span data-stu-id="7c9ea-133">Steps</span></span>
<span data-ttu-id="7c9ea-134">Bu öğretici bir parçası olarak gerçekleştirdiğiniz hello adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-134">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="7c9ea-135">Oluşturma **bağlantılı Hizmetleri** hello veri fabrikası'nda.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-135">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="7c9ea-136">Bu adımda Azure Depolama ve Azure SQL Veritabanı türünde iki bağlı hizmet oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-136">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="7c9ea-137">Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-137">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="7c9ea-138">Bir kapsayıcı oluşturulur ve veri toothis depolama hesabı bir parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-138">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="7c9ea-139">AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-139">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="7c9ea-140">Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-140">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="7c9ea-141">Bu veritabanındaki SQL tablosunu, [ön koşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-141">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>     
2. <span data-ttu-id="7c9ea-142">Giriş ve çıkış oluşturma **veri kümeleri** hello veri fabrikası'nda.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-142">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="7c9ea-143">Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-143">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="7c9ea-144">Ve hello giriş blob dataset hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-144">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="7c9ea-145">Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-145">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="7c9ea-146">Ve hello veritabanı toowhich hello verileri hello blob depolama biriminden hello tabloda kopyalanır hello çıktı SQL tablosu veri kümesi belirtir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-146">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
3. <span data-ttu-id="7c9ea-147">Oluşturma bir **ardışık düzen** hello veri fabrikası'nda.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-147">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="7c9ea-148">Bu adımda, kopyalama etkinliği ile bir işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-148">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="7c9ea-149">Merhaba kopyalama etkinliği hello Azure blob depolama tooa hello Azure SQL veritabanı tablosunda bir blob veri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-149">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="7c9ea-150">Kopyalama etkinliği herhangi bir desteklenen kaynak desteklenen tooany hedefin bir ardışık düzen toocopy verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-150">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="7c9ea-151">Desteklenen veri depolarının bir listesi için [veri taşıma etkinlikleri](data-factory-data-movement-activities.md#supported-data-stores-and-formats) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-151">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
4. <span data-ttu-id="7c9ea-152">Data Factory varlıklarını (bağlı hizmetler, veri kümeleri/tabloları ve işlem hatları) dağıtırken bir Azure **veri fabrikası** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-152">Create an Azure **data factory** when deploying Data Factory entities (linked services, datasets/tables, and pipelines).</span></span> 

## <a name="create-visual-studio-project"></a><span data-ttu-id="7c9ea-153">Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-153">Create Visual Studio project</span></span>
1. <span data-ttu-id="7c9ea-154">**Visual Studio 2015**’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-154">Launch **Visual Studio 2015**.</span></span> <span data-ttu-id="7c9ea-155">Tıklatın **dosya**, çok noktası**yeni**, tıklatıp **proje**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-155">Click **File**, point too**New**, and click **Project**.</span></span> <span data-ttu-id="7c9ea-156">Merhaba görmelisiniz **yeni proje** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-156">You should see hello **New Project** dialog box.</span></span>  
2. <span data-ttu-id="7c9ea-157">Merhaba, **yeni proje** iletişim, select hello **DataFactory** şablonu ve tıklatın **boş Data Factory projesi**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-157">In hello **New Project** dialog, select hello **DataFactory** template, and click **Empty Data Factory Project**.</span></span>  
   
    ![Yeni proje iletişim kutusu](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-project-dialog.png)
3. <span data-ttu-id="7c9ea-159">Merhaba adını hello proje hello çözüm için konum ve hello çözüm adını belirtin ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-159">Specify hello name of hello project, location for hello solution, and name of hello solution, and then click **OK**.</span></span>
   
    ![Çözüm Gezgini](./media/data-factory-copy-activity-tutorial-using-visual-studio/solution-explorer.png)    

## <a name="create-linked-services"></a><span data-ttu-id="7c9ea-161">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-161">Create linked services</span></span>
<span data-ttu-id="7c9ea-162">Verilerinizi depolayan ve Hizmetleri toohello veri fabrikası işlem bir veri fabrikası toolink bağlı hizmetler oluşturma.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-162">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="7c9ea-163">Bu öğreticide, Azure HDInsight veya Azure Data Lake Analytics gibi herhangi bir işlem hizmeti kullanmazsınız.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-163">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="7c9ea-164">Azure Depolama (kaynak) ve Azure SQL Veritabanı (hedef) türünde iki veri deposu kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-164">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="7c9ea-165">Bu nedenle, AzureStorage ve AzureSqlDatabase türünde iki bağlı hizmet oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-165">Therefore, you create two linked services of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="7c9ea-166">Hello Azure depolama hizmeti Azure depolama hesabı toohello data factory'nizi bağlı.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-166">hello Azure Storage linked service links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="7c9ea-167">Bu depolama hesap hello biri, hangi, kapsayıcı oluşturuldu ve hello veri parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-167">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="7c9ea-168">Azure SQL Hizmeti Azure SQL veritabanı toohello data factory'nizi bağlı.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-168">Azure SQL linked service links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="7c9ea-169">Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-169">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="7c9ea-170">Bu veritabanında hello emp tablosunda bir parçası olarak oluşturulan [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-170">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="7c9ea-171">Bağlı hizmetler veri depolarını veya hizmetleri tooan Azure data factory işlem.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-171">Linked services link data stores or compute services tooan Azure data factory.</span></span> <span data-ttu-id="7c9ea-172">Bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tüm kaynakları ve kopyalama etkinliği hello tarafından desteklenen havuzlarını hello için.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-172">See [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) for all hello sources and sinks supported by hello Copy Activity.</span></span> <span data-ttu-id="7c9ea-173">Bkz: [işlem bağlı Hizmetleri](data-factory-compute-linked-services.md) Data Factory ile desteklenen işlem Hizmetleri hello listesi.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-173">See [compute linked services](data-factory-compute-linked-services.md) for hello list of compute services supported by Data Factory.</span></span> <span data-ttu-id="7c9ea-174">Bu öğreticide herhangi bir işlem hizmeti kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-174">In this tutorial, you do not use any compute service.</span></span> 

### <a name="create-hello-azure-storage-linked-service"></a><span data-ttu-id="7c9ea-175">Hello Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-175">Create hello Azure Storage linked service</span></span>
1. <span data-ttu-id="7c9ea-176">İçinde **Çözüm Gezgini**, sağ **bağlı hizmetler**, çok noktası**Ekle**, tıklatıp **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-176">In **Solution Explorer**, right-click **Linked Services**, point too**Add**, and click **New Item**.</span></span>      
2. <span data-ttu-id="7c9ea-177">Merhaba, **Yeni Öğe Ekle** iletişim kutusunda **Azure depolama bağlı hizmeti** hello listesi ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-177">In hello **Add New Item** dialog box, select **Azure Storage Linked Service** from hello list, and click **Add**.</span></span> 
   
    ![Yeni Bağlı Hizmet](./media/data-factory-copy-activity-tutorial-using-visual-studio/new-linked-service-dialog.png)
3. <span data-ttu-id="7c9ea-179">Değiştir `<accountname>` ve `<accountkey>`* Azure storage hesabınızı ve anahtarını hello adı.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-179">Replace `<accountname>` and `<accountkey>`* with hello name of your Azure storage account and its key.</span></span> 
   
    ![Azure Storage Bağlı Hizmeti](./media/data-factory-copy-activity-tutorial-using-visual-studio/azure-storage-linked-service.png)
4. <span data-ttu-id="7c9ea-181">Merhaba Kaydet **AzureStorageLinkedService1.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-181">Save hello **AzureStorageLinkedService1.json** file.</span></span>

    <span data-ttu-id="7c9ea-182">Merhaba bağlantılı hizmet tanımında JSON özellikleri hakkında daha fazla bilgi için bkz: [Azure Blob Storage bağlayıcı](data-factory-azure-blob-connector.md#linked-service-properties) makalesi.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-182">For more information about JSON properties in hello linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-hello-azure-sql-linked-service"></a><span data-ttu-id="7c9ea-183">Hello Azure SQL bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-183">Create hello Azure SQL linked service</span></span>
1. <span data-ttu-id="7c9ea-184">Sağ tıklayın **bağlı hizmetler** hello düğümünde **Çözüm Gezgini** yeniden çok noktası**Ekle**, tıklatıp **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-184">Right-click on **Linked Services** node in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span> 
2. <span data-ttu-id="7c9ea-185">Bu sefer, **Azure SQL Bağlı Hizmeti**’ni seçin ve **Ekle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-185">This time, select **Azure SQL Linked Service**, and click **Add**.</span></span> 
3. <span data-ttu-id="7c9ea-186">Merhaba, **AzureSqlLinkedService1.json dosyasında**, Değiştir `<servername>`, `<databasename>`, `<username@servername>`, ve `<password>` adlarıyla Azure SQL sunucunuza, veritabanı, kullanıcı hesabı ve parolası.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-186">In hello **AzureSqlLinkedService1.json file**, replace `<servername>`, `<databasename>`, `<username@servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span>    
4. <span data-ttu-id="7c9ea-187">Merhaba Kaydet **AzureSqlLinkedService1.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-187">Save hello **AzureSqlLinkedService1.json** file.</span></span> 
    
    <span data-ttu-id="7c9ea-188">Bu JSON özellikleri hakkında daha fazla bilgi için [Azure SQL Veritabanı bağlayıcısı](data-factory-azure-sql-connector.md#linked-service-properties) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-188">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>


## <a name="create-datasets"></a><span data-ttu-id="7c9ea-189">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-189">Create datasets</span></span>
<span data-ttu-id="7c9ea-190">Merhaba önceki adımda, Azure Storage hesabını ve Azure SQL veritabanı tooyour veri fabrikası bağlı hizmetler toolink oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-190">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="7c9ea-191">Bu adımda, iki veri kümesi InputDataset ve giriş temsil OutputDataset ve sırasıyla AzureStorageLinkedService1 ve AzureSqlLinkedService1 başvurduğu hello veri depolarında depolanan çıktı verilerini adlı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-191">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService1 and AzureSqlLinkedService1 respectively.</span></span>

<span data-ttu-id="7c9ea-192">Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-192">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="7c9ea-193">Ve hello giriş blob veri kümesi (InputDataset) hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-193">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="7c9ea-194">Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-194">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="7c9ea-195">Ve kopyalanan verileri hello blob depolama biriminden hello veritabanı toowhich hello SQL tablosu veri kümesi (OututDataset) hello tabloda hello çıktı.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-195">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="7c9ea-196">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-196">Create input dataset</span></span>
<span data-ttu-id="7c9ea-197">Bu adımda, tooa blob dosya (emp.txt) işaret InputDataset adlı bir veri hello kök klasöründe bir blob kapsayıcısını (adftutorial) hello Azure hello AzureStorageLinkedService1 bağlı hizmeti tarafından temsil edilen depolama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-197">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService1 linked service.</span></span> <span data-ttu-id="7c9ea-198">Verme hello dosya adı için bir değer belirtin (veya atlayın) hello giriş klasöründeki tüm blob'lara ait veriler kopyalanan toohello hedef demektir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-198">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="7c9ea-199">Bu öğreticide, hello dosya adı için bir değer belirtin.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-199">In this tutorial, you specify a value for hello fileName.</span></span> 

<span data-ttu-id="7c9ea-200">Burada, "yerine"veri kümelerini hello terimi "Tablo" kullanın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-200">Here, you use hello term "tables" rather than "datasets".</span></span> <span data-ttu-id="7c9ea-201">Tablo dikdörtgen bir veri kümesidir ve hello yalnızca şu anda desteklenen veri kümesi türüdür.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-201">A table is a rectangular dataset and is hello only type of dataset supported right now.</span></span> 

1. <span data-ttu-id="7c9ea-202">Sağ **tabloları** hello içinde **Çözüm Gezgini**, çok noktası**Ekle**, tıklatıp **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-202">Right-click **Tables** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="7c9ea-203">Merhaba, **Yeni Öğe Ekle** iletişim kutusunda **Azure Blob**, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-203">In hello **Add New Item** dialog box, select **Azure Blob**, and click **Add**.</span></span>   
3. <span data-ttu-id="7c9ea-204">Hello JSON metnini aşağıdaki metin hello ile değiştirin ve hello Kaydet **AzureBlobLocation1.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-204">Replace hello JSON text with hello following text and save hello **AzureBlobLocation1.json** file.</span></span> 

  ```json   
  {
    "name": "InputDataset",
    "properties": {
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
      "type": "AzureBlob",
      "linkedServiceName": "AzureStorageLinkedService1",
      "typeProperties": {
        "folderPath": "adftutorial/",
        "format": {
          "type": "TextFormat",
          "columnDelimiter": ","
        }
      },
      "external": true,
      "availability": {
        "frequency": "Hour",
        "interval": 1
      }
    }
  }
  ``` 
    <span data-ttu-id="7c9ea-205">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-205">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="7c9ea-206">Özellik</span><span class="sxs-lookup"><span data-stu-id="7c9ea-206">Property</span></span> | <span data-ttu-id="7c9ea-207">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c9ea-207">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="7c9ea-208">type</span><span class="sxs-lookup"><span data-stu-id="7c9ea-208">type</span></span> | <span data-ttu-id="7c9ea-209">Merhaba type özelliği çok ayarlamak**AzureBlob** verileri Azure blob depolama alanında bulunduğundan.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-209">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="7c9ea-210">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7c9ea-210">linkedServiceName</span></span> | <span data-ttu-id="7c9ea-211">Toohello başvuruyor **AzureStorageLinkedService** daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-211">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="7c9ea-212">folderPath</span><span class="sxs-lookup"><span data-stu-id="7c9ea-212">folderPath</span></span> | <span data-ttu-id="7c9ea-213">Merhaba blob belirtir **kapsayıcı** ve hello **klasörü** giriş BLOB'ları içerir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-213">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="7c9ea-214">Bu öğreticide adftutorial hello blob kapsayıcı ve hello kök klasör.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-214">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="7c9ea-215">fileName</span><span class="sxs-lookup"><span data-stu-id="7c9ea-215">fileName</span></span> | <span data-ttu-id="7c9ea-216">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-216">This property is optional.</span></span> <span data-ttu-id="7c9ea-217">Bu özelliği atarsanız, tüm dosyaları hello folderPath çekilir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-217">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="7c9ea-218">Bu öğreticide **emp.txt** hello fileName, böylece yalnızca bu dosyanın işleme için kayıt için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-218">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="7c9ea-219">format -> type</span><span class="sxs-lookup"><span data-stu-id="7c9ea-219">format -> type</span></span> |<span data-ttu-id="7c9ea-220">Merhaba giriş dosyası kullanırız hello metin biçiminde olduğundan **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-220">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="7c9ea-221">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="7c9ea-221">columnDelimiter</span></span> | <span data-ttu-id="7c9ea-222">Merhaba giriş dosyası Hello sütunlarında tarafından ayrılmış **virgül karakteriyle (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-222">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="7c9ea-223">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="7c9ea-223">frequency/interval</span></span> | <span data-ttu-id="7c9ea-224">Merhaba sıklığını çok ayarlamak**saat** ve aralığı çok ayarlamak**1**, o hello yani dilimler kullanılabilir giriş **saatlik**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-224">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="7c9ea-225">Hello Data Factory hizmeti için giriş verileri saatte hello kök klasöründe blob kapsayıcısının diğer bir deyişle, görünüyor (**adftutorial**), belirtilen.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-225">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="7c9ea-226">Merhaba veri hello ardışık düzen başlangıç ve bitiş zamanları, değil önce veya sonra bu kez içinde arar.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-226">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="7c9ea-227">external</span><span class="sxs-lookup"><span data-stu-id="7c9ea-227">external</span></span> | <span data-ttu-id="7c9ea-228">Bu özellik çok ayarlanır**true** hello verileri bu ardışık düzen tarafından oluşturulmamış olması durumunda.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-228">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="7c9ea-229">Bu öğreticide girdi verileri Hello Biz bu özellik tootrue ayarlamak için bu ardışık düzen tarafından oluşturulmayan hello emp.txt, dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-229">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="7c9ea-230">Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-230">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>   

### <a name="create-output-dataset"></a><span data-ttu-id="7c9ea-231">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-231">Create output dataset</span></span>
<span data-ttu-id="7c9ea-232">Bu adımda **OutputDataset** adlı bir çıktı veri kümesi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-232">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="7c9ea-233">Bu veri kümesi tarafından temsil edilen hello Azure SQL veritabanındaki tooa SQL tablosunu işaret **AzureSqlLinkedService1**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-233">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService1**.</span></span> 

1. <span data-ttu-id="7c9ea-234">Sağ **tabloları** hello içinde **Çözüm Gezgini** yeniden çok noktası**Ekle**, tıklatıp **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-234">Right-click **Tables** in hello **Solution Explorer** again, point too**Add**, and click **New Item**.</span></span>
2. <span data-ttu-id="7c9ea-235">Merhaba, **Yeni Öğe Ekle** iletişim kutusunda **Azure SQL**, tıklatıp **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-235">In hello **Add New Item** dialog box, select **Azure SQL**, and click **Add**.</span></span> 
3. <span data-ttu-id="7c9ea-236">Merhaba JSON metnini aşağıdaki JSON hello ile değiştirin ve hello Kaydet **AzureSqlTableLocation1.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-236">Replace hello JSON text with hello following JSON and save hello **AzureSqlTableLocation1.json** file.</span></span>

  ```json
    {
     "name": "OutputDataset",
     "properties": {
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
       "type": "AzureSqlTable",
       "linkedServiceName": "AzureSqlLinkedService1",
       "typeProperties": {
         "tableName": "emp"
       },
       "availability": {
         "frequency": "Hour",
         "interval": 1
       }
     }
    }
    ```
    <span data-ttu-id="7c9ea-237">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-237">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="7c9ea-238">Özellik</span><span class="sxs-lookup"><span data-stu-id="7c9ea-238">Property</span></span> | <span data-ttu-id="7c9ea-239">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7c9ea-239">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="7c9ea-240">type</span><span class="sxs-lookup"><span data-stu-id="7c9ea-240">type</span></span> | <span data-ttu-id="7c9ea-241">Merhaba type özelliği çok ayarlamak**AzureSqlTable** verileri bir Azure SQL veritabanı tablosunda kopyalanan tooa olduğundan.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-241">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="7c9ea-242">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="7c9ea-242">linkedServiceName</span></span> | <span data-ttu-id="7c9ea-243">Toohello başvuruyor **AzureSqlLinkedService** daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-243">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="7c9ea-244">tableName</span><span class="sxs-lookup"><span data-stu-id="7c9ea-244">tableName</span></span> | <span data-ttu-id="7c9ea-245">Belirtilen hello **tablo** toowhich hello veri kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-245">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="7c9ea-246">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="7c9ea-246">frequency/interval</span></span> | <span data-ttu-id="7c9ea-247">Merhaba sıklığı çok ayarlı**saat** ve aralığı **1**, hello çıkış dilimler üretilir anlamına gelir **saatlik** hello ardışık düzen başlangıç ve bitiş zamanları, önce değil arasında veya Bu kez sonra.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-247">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="7c9ea-248">Üç sütun – **kimliği**, **FirstName**, ve **LastName** – hello veritabanındaki emp tablosunda hello.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-248">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="7c9ea-249">Kimliktir bir kimlik sütunu yalnızca toospecify gereken şekilde **FirstName** ve **LastName** burada.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-249">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="7c9ea-250">Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure SQL bağlayıcısı makalesi](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-250">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>

## <a name="create-pipeline"></a><span data-ttu-id="7c9ea-251">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-251">Create pipeline</span></span>
<span data-ttu-id="7c9ea-252">Bu adımda, girdi olarak **InputDataset** ve çıktı olarak **OutputDataset** kullanan **kopyalama etkinliğine** sahip bir işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-252">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="7c9ea-253">Şu anda, hangi sürücü zamanlama hello çıktı veri kümesi değil.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-253">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="7c9ea-254">Bu öğreticide, çıktı veri kümesi yapılandırılmış tooproduce bir dilim saate birdir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-254">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="7c9ea-255">bir başlangıç saati ve bir 24 saat olan günü birbirinden, bitiş zamanı Hello ardışık düzen vardır.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-255">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="7c9ea-256">Bu nedenle, çıktı veri kümesinin 24 dilim hello ardışık düzen tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-256">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 

1. <span data-ttu-id="7c9ea-257">Sağ **ardışık düzen** hello içinde **Çözüm Gezgini**, çok noktası**Ekle**, tıklatıp **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-257">Right-click **Pipelines** in hello **Solution Explorer**, point too**Add**, and click **New Item**.</span></span>  
2. <span data-ttu-id="7c9ea-258">Seçin **veri işlem hattı Kopyala** hello içinde **Yeni Öğe Ekle** iletişim kutusu ve tıklatın **Ekle**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-258">Select **Copy Data Pipeline** in hello **Add New Item** dialog box and click **Add**.</span></span> 
3. <span data-ttu-id="7c9ea-259">Merhaba JSON hello aşağıdaki JSON ile değiştirin ve hello kaydedin **CopyActivity1.json** dosya.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-259">Replace hello JSON with hello following JSON and save hello **CopyActivity1.json** file.</span></span>

  ```json   
    {
     "name": "ADFTutorialPipeline",
     "properties": {
       "description": "Copy data from a blob tooAzure SQL table",
       "activities": [
         {
           "name": "CopyFromBlobToSQL",
           "type": "Copy",
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
           "typeProperties": {
             "source": {
               "type": "BlobSource"
             },
             "sink": {
               "type": "SqlSink",
               "writeBatchSize": 10000,
               "writeBatchTimeout": "60:00:00"
             }
           },
           "Policy": {
             "concurrency": 1,
             "executionPriorityOrder": "NewestFirst",
             "style": "StartOfInterval",
             "retry": 0,
             "timeout": "01:00:00"
           }
         }
       ],
       "start": "2017-05-11T00:00:00Z",
       "end": "2017-05-12T00:00:00Z",
       "isPaused": false
     }
    }
    ```   
    - <span data-ttu-id="7c9ea-260">Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**kopya**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-260">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="7c9ea-261">Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-261">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="7c9ea-262">Data Factory çözümlerinde, [veri dönüştürme etkinliklerini](data-factory-data-transformation-activities.md) de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-262">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="7c9ea-263">Merhaba etkinlik çok kümesi için giriş**InputDataset** ve hello etkinlik çok kümesi için çıkış**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-263">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="7c9ea-264">Merhaba, **typeProperties** bölümünde **BlobSource** hello kaynak türü olarak belirtilir ve **SqlSink** hello Havuz türü olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-264">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="7c9ea-265">Kaynakları ve havuzlarını olarak hello kopyalama etkinliği tarafından desteklenen veri depoları tam bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-265">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="7c9ea-266">nasıl toouse belirli bir desteklenen veri depolayan bir kaynak/havuz toolearn hello tablosundaki hello bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-266">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="7c9ea-267">Merhaba Hello değerini değiştirin **Başlat** hello geçerli gün özelliğiyle ve **son** hello sonraki gün değeri.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-267">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="7c9ea-268">Yalnızca hello tarih bölümünü belirtip tarih saat hello hello saat bölümünü atlayın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-268">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="7c9ea-269">Örneğin, "2016-02-çok eşdeğeri olan 03", "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="7c9ea-269">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="7c9ea-270">Başlangıç ve bitiş tarih saatleri [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-270">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="7c9ea-271">Örneğin: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-271">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="7c9ea-272">Merhaba **son** saati isteğe bağlıdır ancak biz Bu öğreticide kullanın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-272">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="7c9ea-273">Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 saat**".</span><span class="sxs-lookup"><span data-stu-id="7c9ea-273">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="7c9ea-274">toorun hello ardışık kalıcı olarak belirtmek **9999-09-09** hello hello değeri olarak **son** özelliği.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-274">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="7c9ea-275">Örnek önceki hello vardır 24 veri dilimi her veri dilimi saatlik oluşturulduğundan.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-275">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="7c9ea-276">İşlem hattı tanımındaki JSON özelliklerinin açıklamaları için [işlem hatları oluşturma](data-factory-create-pipelines.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-276">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="7c9ea-277">Kopyalama etkinliği tanımındaki JSON özelliklerinin açıklamaları için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-277">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="7c9ea-278">BlobSource tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-278">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="7c9ea-279">SqlSink tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure SQL Veritabanı bağlayıcısı makalesi](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-279">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>

## <a name="publishdeploy-data-factory-entities"></a><span data-ttu-id="7c9ea-280">Data Factory varlıklarını yayımlama/dağıtma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-280">Publish/deploy Data Factory entities</span></span>
<span data-ttu-id="7c9ea-281">Bu adımda daha önce oluşturduğunuz Data Factory varlıklarını (bağlı hizmetler, veri kümeleri ve işlem hattı) yayımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-281">In this step, you publish Data Factory entities (linked services, datasets, and pipeline) you created earlier.</span></span> <span data-ttu-id="7c9ea-282">Ayrıca, bu varlıkları toohold hello yeni veri fabrikası toobe hello adını oluşturulan belirtin.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-282">You also specify hello name of hello new data factory toobe created toohold these entities.</span></span>  

1. <span data-ttu-id="7c9ea-283">Merhaba Çözüm Gezgini'nde projeye sağ tıklayın ve **Yayımla**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-283">Right-click project in hello Solution Explorer, and click **Publish**.</span></span> 
2. <span data-ttu-id="7c9ea-284">Görürseniz **tooyour Microsoft hesabı oturum** iletişim kutusunda, Azure aboneliği olan hello hesabı için kimlik bilgilerinizi girin ve tıklayın **oturum**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-284">If you see **Sign in tooyour Microsoft account** dialog box, enter your credentials for hello account that has Azure subscription, and click **sign in**.</span></span>
3. <span data-ttu-id="7c9ea-285">İletişim kutusu aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-285">You should see hello following dialog box:</span></span>
   
   ![Yayımla iletişim kutusu](./media/data-factory-copy-activity-tutorial-using-visual-studio/publish.png)
4. <span data-ttu-id="7c9ea-287">Merhaba data factory yapılandırma sayfasında içinde adımları hello:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-287">In hello Configure data factory page, do hello following steps:</span></span> 
   
   1. <span data-ttu-id="7c9ea-288">**Yeni Data Factory Oluştur** seçeneğini seçin.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-288">select **Create New Data Factory** option.</span></span>
   2. <span data-ttu-id="7c9ea-289">**Ad** için **VSTutorialFactory** girin.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-289">Enter **VSTutorialFactory** for **Name**.</span></span>  
      
      > [!IMPORTANT]
      > <span data-ttu-id="7c9ea-290">Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-290">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="7c9ea-291">Yayımlama sırasında veri fabrikasının hello adı hakkında bir hata alırsanız, hello veri fabrikası (örneğin, yournameVSTutorialFactory) yayımlamayı yeniden deneyin ve hello adını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-291">If you receive an error about hello name of data factory when publishing, change hello name of hello data factory (for example, yournameVSTutorialFactory) and try publishing again.</span></span> <span data-ttu-id="7c9ea-292">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-292">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>        
      > 
      > 
   3. <span data-ttu-id="7c9ea-293">Azure aboneliğiniz için hello seçin **abonelik** alan.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-293">Select your Azure subscription for hello **Subscription** field.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="7c9ea-294">Herhangi bir abonelik görmüyorsanız, bir yönetici veya hello aboneliğin ortak yöneticisi olan bir hesabı kullanarak oturum emin olun.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-294">If you do not see any subscription, ensure that you logged in using an account that is an admin or co-admin of hello subscription.</span></span>  
      > 
      > 
   4. <span data-ttu-id="7c9ea-295">Select hello **kaynak grubu** oluşturulan hello veri fabrikası toobe için.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-295">Select hello **resource group** for hello data factory toobe created.</span></span> 
   5. <span data-ttu-id="7c9ea-296">Select hello **bölge** hello veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-296">Select hello **region** for hello data factory.</span></span> <span data-ttu-id="7c9ea-297">Yalnızca Hello Data Factory hizmeti tarafından desteklenen bölgeler hello aşağı açılan listesinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-297">Only regions supported by hello Data Factory service are shown in hello drop-down list.</span></span>
   6. <span data-ttu-id="7c9ea-298">Tıklatın **sonraki** tooswitch toohello **öğeleri Yayımla** sayfası.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-298">Click **Next** tooswitch toohello **Publish Items** page.</span></span>
      
       ![Veri fabrikası yapılandırma sayfası](media/data-factory-copy-activity-tutorial-using-visual-studio/configure-data-factory-page.png)   
5. <span data-ttu-id="7c9ea-300">Merhaba, **öğeleri Yayımla** sayfasında, tüm veri varlıkları seçilir ve tıklatın fabrikaları hello olun **sonraki** tooswitch toohello **Özet** sayfası.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-300">In hello **Publish Items** page, ensure that all hello Data Factories entities are selected, and click **Next** tooswitch toohello **Summary** page.</span></span>
   
   ![Öğe yayımlama sayfası](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-items-page.png)     
6. <span data-ttu-id="7c9ea-302">Merhaba özeti gözden geçirin ve tıklatın **sonraki** toostart, hello dağıtım işlemi ve görünüm hello **dağıtım durumu**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-302">Review hello summary and click **Next** toostart hello deployment process and view hello **Deployment Status**.</span></span>
   
   ![Özet yayımlama sayfası](media/data-factory-copy-activity-tutorial-using-visual-studio/publish-summary-page.png)
7. <span data-ttu-id="7c9ea-304">Merhaba, **dağıtım durumu** sayfasında hello hello dağıtım işleminin durumunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-304">In hello **Deployment Status** page, you should see hello status of hello deployment process.</span></span> <span data-ttu-id="7c9ea-305">Merhaba dağıtımını gerçekleştirdikten sonra Son'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-305">Click Finish after hello deployment is done.</span></span>
 
   ![Dağıtım durumu sayfası](media/data-factory-copy-activity-tutorial-using-visual-studio/deployment-status.png)

<span data-ttu-id="7c9ea-307">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-307">Note hello following points:</span></span> 

* <span data-ttu-id="7c9ea-308">Merhaba hatayı alırsanız: "Bu aboneliği değil Microsoft.DataFactory kayıtlı toouse ad", hello aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-308">If you receive hello error: "This subscription is not registered toouse namespace Microsoft.DataFactory", do one of hello following and try publishing again:</span></span> 
  
  * <span data-ttu-id="7c9ea-309">Azure PowerShell'de komut tooregister hello Data Factory sağlayıcısının aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-309">In Azure PowerShell, run hello following command tooregister hello Data Factory provider.</span></span> 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    <span data-ttu-id="7c9ea-310">Bu Data Factory sağlayıcısının kayıtlı hello komutu tooconfirm aşağıdaki hello çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-310">You can run hello following command tooconfirm that hello Data Factory provider is registered.</span></span> 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="7c9ea-311">Oturum açma kullanılarak hello hello Azure aboneliğinize [Azure portal](https://portal.azure.com) ve tooa Data Factory dikey penceresine gidin (veya) hello Azure portalında bir data factory oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-311">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="7c9ea-312">Bu eylemin hello sağlayıcıyı sizin için otomatik olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-312">This action automatically registers hello provider for you.</span></span>
* <span data-ttu-id="7c9ea-313">Merhaba veri fabrikasının Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-313">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c9ea-314">toocreate Data Factory örnekleri toobe bir yönetici/ortak yöneticisi olan hello Azure aboneliği gerekir</span><span class="sxs-lookup"><span data-stu-id="7c9ea-314">toocreate Data Factory instances, you need toobe a admin/co-admin of hello Azure subscription</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="7c9ea-315">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="7c9ea-315">Monitor pipeline</span></span>
<span data-ttu-id="7c9ea-316">Veri fabrikanızın toohello giriş sayfasına gidin:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-316">Navigate toohello home page for your data factory:</span></span>

1. <span data-ttu-id="7c9ea-317">Çok oturum[Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-317">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7c9ea-318">Tıklatın **daha fazla hizmet** üzerinde hello sol menü öğesini tıklatıp **veri fabrikaları**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-318">Click **More services** on hello left menu, and click **Data factories**.</span></span>

    ![Data factory’lere göz atma](media/data-factory-copy-activity-tutorial-using-visual-studio/browse-data-factories.png)
3. <span data-ttu-id="7c9ea-320">Veri fabrikanızın Hello adını yazmaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-320">Start typing hello name of your data factory.</span></span>

    ![Veri fabrikasının adı](media/data-factory-copy-activity-tutorial-using-visual-studio/enter-data-factory-name.png) 
4. <span data-ttu-id="7c9ea-322">Veri fabrikanızın hello sonuçları listesi toosee hello giriş sayfasında, veri fabrikası'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-322">Click your data factory in hello results list toosee hello home page for your data factory.</span></span>

    ![Data factory giriş sayfası](media/data-factory-copy-activity-tutorial-using-visual-studio/data-factory-home-page.png)
5. <span data-ttu-id="7c9ea-324">Makalesindeki yönergeleri izleyin [veri kümelerini ve ardışık düzen izleme](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello ardışık düzen ve veri kümeleri Bu öğreticide oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-324">Follow instructions from [Monitor datasets and pipeline](data-factory-copy-activity-tutorial-using-azure-portal.md#monitor-pipeline) toomonitor hello pipeline and datasets you have created in this tutorial.</span></span> <span data-ttu-id="7c9ea-325">Visual Studio şu anda Data Factory işlem hatlarını izlemeyi desteklememektedir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-325">Currently, Visual Studio does not support monitoring Data Factory pipelines.</span></span> 

## <a name="summary"></a><span data-ttu-id="7c9ea-326">Özet</span><span class="sxs-lookup"><span data-stu-id="7c9ea-326">Summary</span></span>
<span data-ttu-id="7c9ea-327">Bu öğreticide, bir Azure veri fabrikası toocopy verileri Azure blob tooan Azure SQL veritabanından oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-327">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="7c9ea-328">Visual Studio toocreate hello veri fabrikası, bağlı hizmetler, veri kümeleri ve işlem hattı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-328">You used Visual Studio toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="7c9ea-329">Bu öğreticide gerçekleştirilen hello üst düzey adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-329">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="7c9ea-330">Oluşturulan Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-330">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="7c9ea-331">Oluşturulan **bağlı hizmetler**:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-331">Created **linked services**:</span></span>
   1. <span data-ttu-id="7c9ea-332">Bir **Azure Storage** hizmet toolink girdi verilerini tutan Azure Storage hesabınıza bağlı.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-332">An **Azure Storage** linked service toolink your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="7c9ea-333">Bir **Azure SQL** hizmet toolink hello çıktı verilerini tutan Azure SQL veritabanınızı bağlı.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-333">An **Azure SQL** linked service toolink your Azure SQL database that holds hello output data.</span></span> 
3. <span data-ttu-id="7c9ea-334">İşlem hatları için girdi ve çıktı verilerini açıklayan **veri kümeleri** oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-334">Created **datasets**, which describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="7c9ea-335">Kaynak olarak **BlobSource**’u, havuz olarak da **SqlSink**’i kapsayan **Kopyalama Etkinliği**’ne sahip oluşturulan **işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-335">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span> 

<span data-ttu-id="7c9ea-336">toouse Azure Hdınsight kümesi kullanarak bir Hdınsight Hive etkinliği tootransform veri nasıl görürüm toosee [ Öğreticisi: Hadoop kümesi kullanarak ilk ardışık düzen tootransform verilerinizi yapı](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-336">toosee how toouse a HDInsight Hive Activity tootransform data by using Azure HDInsight cluster, see [ Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

<span data-ttu-id="7c9ea-337">Merhaba çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-337">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="7c9ea-338">Ayrıntılı bilgi için bkz. [Data Factory’de zamanlama ve yürütme](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-338">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 

## <a name="view-all-data-factories-in-server-explorer"></a><span data-ttu-id="7c9ea-339">Sunucu Gezgini’nde tüm veri fabrikalarını görüntüleme</span><span class="sxs-lookup"><span data-stu-id="7c9ea-339">View all data factories in Server Explorer</span></span>
<span data-ttu-id="7c9ea-340">Bu bölümde, nasıl toouse Sunucu Gezgini, Azure aboneliğinizin tüm hello data factory'leri Visual Studio tooview hello ve mevcut bir data factory'ye dayandırılan Visual Studio projesi oluşturma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-340">This section describes how toouse hello Server Explorer in Visual Studio tooview all hello data factories in your Azure subscription and create a Visual Studio project based on an existing data factory.</span></span> 

1. <span data-ttu-id="7c9ea-341">İçinde **Visual Studio**, tıklatın **Görünüm** üzerinde hello menü öğesini tıklatıp **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-341">In **Visual Studio**, click **View** on hello menu, and click **Server Explorer**.</span></span>
2. <span data-ttu-id="7c9ea-342">Merhaba Sunucu Gezgini penceresinde **Azure** ve genişletin **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-342">In hello Server Explorer window, expand **Azure** and expand **Data Factory**.</span></span> <span data-ttu-id="7c9ea-343">Görürseniz **tooVisual Studio oturum**, hello girin **hesap** tıklatın ve Azure aboneliği ile ilişkili **devam**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-343">If you see **Sign in tooVisual Studio**, enter hello **account** associated with your Azure subscription and click **Continue**.</span></span> <span data-ttu-id="7c9ea-344">**parola** girip **Oturum aç**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-344">Enter **password**, and click **Sign in**.</span></span> <span data-ttu-id="7c9ea-345">Visual Studio, aboneliğinizdeki tüm Azure data factory'leri hakkında bilgi tooget çalışır.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-345">Visual Studio tries tooget information about all Azure data factories in your subscription.</span></span> <span data-ttu-id="7c9ea-346">Bu işlemde hello hello durumunu görmek **Data Factoy görev listesi** penceresi.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-346">You see hello status of this operation in hello **Data Factory Task List** window.</span></span>

    ![Sunucu Gezgini](./media/data-factory-copy-activity-tutorial-using-visual-studio/server-explorer.png)

## <a name="create-a-visual-studio-project-for-an-existing-data-factory"></a><span data-ttu-id="7c9ea-348">Var olan bir veri fabrikası için Visual Studio projesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-348">Create a Visual Studio project for an existing data factory</span></span>

- <span data-ttu-id="7c9ea-349">Sunucu Gezgininde veri fabrikası sağ tıklatın ve seçin **dışarı veri fabrikası tooNew proje** Visual Studio projesi dayalı mevcut bir data factory'ye toocreate.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-349">Right-click a data factory in Server Explorer, and select **Export Data Factory tooNew Project** toocreate a Visual Studio project based on an existing data factory.</span></span>

    ![Veri Fabrikası tooa VS projesinde dışarı aktarma](./media/data-factory-copy-activity-tutorial-using-visual-studio/export-data-factory-menu.png)  

## <a name="update-data-factory-tools-for-visual-studio"></a><span data-ttu-id="7c9ea-351">Visual Studio için Data Factory araçlarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7c9ea-351">Update Data Factory tools for Visual Studio</span></span>
<span data-ttu-id="7c9ea-352">Visual Studio için tooupdate Azure Data Factory araçları hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-352">tooupdate Azure Data Factory tools for Visual Studio, do hello following steps:</span></span>

1. <span data-ttu-id="7c9ea-353">Tıklatın **Araçları** hello menü ve seçim **Uzantılar ve güncelleştirmeler**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-353">Click **Tools** on hello menu and select **Extensions and Updates**.</span></span> 
2. <span data-ttu-id="7c9ea-354">Seçin **güncelleştirmeleri** hello sol bölmesinde ve ardından **Visual Studio Galerisi**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-354">Select **Updates** in hello left pane and then select **Visual Studio Gallery**.</span></span>
3. <span data-ttu-id="7c9ea-355">**Visual Studio için Azure Data Factory araçları**’nı seçin ve **Güncelleştir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-355">Select **Azure Data Factory tools for Visual Studio** and click **Update**.</span></span> <span data-ttu-id="7c9ea-356">Bu girişi görmüyorsanız hello hello Araçları'nın en son sürümü zaten sahip.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-356">If you do not see this entry, you already have hello latest version of hello tools.</span></span> 

## <a name="use-configuration-files"></a><span data-ttu-id="7c9ea-357">Yapılandırma dosyalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-357">Use configuration files</span></span>
<span data-ttu-id="7c9ea-358">Bağlı hizmetler/tablolar/işlem hatları için her ortamda farklı için Visual Studio tooconfigure özelliklerinde yapılandırma dosyalarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-358">You can use configuration files in Visual Studio tooconfigure properties for linked services/tables/pipelines differently for each environment.</span></span>

<span data-ttu-id="7c9ea-359">Azure depolama bağlı hizmeti için JSON tanımı aşağıdaki hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-359">Consider hello following JSON definition for an Azure Storage linked service.</span></span> <span data-ttu-id="7c9ea-360">toospecify **connectionString** accountname ve accountkey hello ortam (Dev/Test/Production) toowhich üzerinde göre farklı değerleri olan Data Factory varlıklarını dağıttığınız.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-360">toospecify **connectionString** with different values for accountname and accountkey based on hello environment (Dev/Test/Production) toowhich you are deploying Data Factory entities.</span></span> <span data-ttu-id="7c9ea-361">Her ortam için ayrı bir yapılandırma dosyası kullanarak bu davranışı elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-361">You can achieve this behavior by using separate configuration file for each environment.</span></span>

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

### <a name="add-a-configuration-file"></a><span data-ttu-id="7c9ea-362">Yapılandırma dosyası ekleme</span><span class="sxs-lookup"><span data-stu-id="7c9ea-362">Add a configuration file</span></span>
<span data-ttu-id="7c9ea-363">Merhaba aşağıdaki adımları uygulayarak her ortam için bir yapılandırma dosyası ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-363">Add a configuration file for each environment by performing hello following steps:</span></span>   

1. <span data-ttu-id="7c9ea-364">Visual Studio çözümünüzü Hello Data Factory projenize sağ tıklayın, çok gelin**Ekle**, tıklatıp **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-364">Right-click hello Data Factory project in your Visual Studio solution, point too**Add**, and click **New item**.</span></span>
2. <span data-ttu-id="7c9ea-365">Seçin **Config** hello soldaki yüklenmiş şablonlar hello listeden seçin **yapılandırma dosyası**, girin bir **adı** hello yapılandırması için dosya ve tıklatın**Eklemek**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-365">Select **Config** from hello list of installed templates on hello left, select **Configuration File**, enter a **name** for hello configuration file, and click **Add**.</span></span>

    ![Yapılandırma dosyasını ekleme](./media/data-factory-build-your-first-pipeline-using-vs/add-config-file.png)
3. <span data-ttu-id="7c9ea-367">Biçim aşağıdaki hello yapılandırma parametrelerini ve değerlerini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-367">Add configuration parameters and their values in hello following format:</span></span>

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

    <span data-ttu-id="7c9ea-368">Bu örnek, Azure Storage bağlı hizmetinin ve Azure SQL bağlı hizmetinin connectionString özelliğini yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-368">This example configures connectionString property of an Azure Storage linked service and an Azure SQL linked service.</span></span> <span data-ttu-id="7c9ea-369">Adı belirtmek için hello sözdizimi olduğuna dikkat edin [JsonPath](http://goessner.net/articles/JsonPath/).</span><span class="sxs-lookup"><span data-stu-id="7c9ea-369">Notice that hello syntax for specifying name is [JsonPath](http://goessner.net/articles/JsonPath/).</span></span>   

    <span data-ttu-id="7c9ea-370">JSON hello kod aşağıdaki gösterildiği gibi bir dizi değere sahip özellik varsa:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-370">If JSON has a property that has an array of values as shown in hello following code:</span></span>  

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

    <span data-ttu-id="7c9ea-371">Özellikler, aşağıdaki yapılandırma dosyasına (kullanımı sıfır tabanlı dizin) hello gösterildiği gibi yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-371">Configure properties as shown in hello following configuration file (use zero-based indexing):</span></span>

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

### <a name="property-names-with-spaces"></a><span data-ttu-id="7c9ea-372">Boşluklu özellik adları</span><span class="sxs-lookup"><span data-stu-id="7c9ea-372">Property names with spaces</span></span>
<span data-ttu-id="7c9ea-373">Özellik adında boşluklar varsa, hello aşağıdaki örneğine (veritabanı sunucu adı) gösterildiği gibi köşeli ayraç kullanın:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-373">If a property name has spaces in it, use square brackets as shown in hello following example (Database server name):</span></span>

```json
 {
     "name": "$.properties.activities[1].typeProperties.webServiceParameters.['Database server name']",
     "value": "MyAsqlServer.database.windows.net"
 }
```

### <a name="deploy-solution-using-a-configuration"></a><span data-ttu-id="7c9ea-374">Yapılandırma kullanarak çözümü dağıtma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-374">Deploy solution using a configuration</span></span>
<span data-ttu-id="7c9ea-375">Azure Data Factory varlıklarını vs'de toouse Bu yayımlama işlemi için istediğiniz hello yapılandırma belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-375">When you are publishing Azure Data Factory entities in VS, you can specify hello configuration that you want toouse for that publishing operation.</span></span>

<span data-ttu-id="7c9ea-376">yapılandırma dosyası kullanarak Azure Data Factory projesindeki varlıkları toopublish:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-376">toopublish entities in an Azure Data Factory project using configuration file:</span></span>   

1. <span data-ttu-id="7c9ea-377">Data Factory projesine sağ tıklatın ve **Yayımla** toosee hello **öğeleri Yayımla** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-377">Right-click Data Factory project and click **Publish** toosee hello **Publish Items** dialog box.</span></span>
2. <span data-ttu-id="7c9ea-378">Mevcut bir veri fabrikasını seçin veya üzerinde hello data factory oluşturmak için değerleri belirtin **data factory Yapılandır** sayfasında ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-378">Select an existing data factory or specify values for creating a data factory on hello **Configure data factory** page, and click **Next**.</span></span>   
3. <span data-ttu-id="7c9ea-379">Merhaba üzerinde **öğeleri Yayımla** sayfa: hello için kullanılabilir yapılandırmaların açılan listesini görmek **Dağıtım Yapılandırması Seç** alan.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-379">On hello **Publish Items** page: you see a drop-down list with available configurations for hello **Select Deployment Config** field.</span></span>

    ![Yapılandırma dosyası seçme](./media/data-factory-build-your-first-pipeline-using-vs/select-config-file.png)
4. <span data-ttu-id="7c9ea-381">Select hello **yapılandırma dosyası** , gibi toouse ve'ı tıklatın, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-381">Select hello **configuration file** that you would like toouse and click **Next**.</span></span>
5. <span data-ttu-id="7c9ea-382">Merhaba hello JSON dosyasının adını gördüğünüzü onaylayın **Özet** sayfasında ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-382">Confirm that you see hello name of JSON file in hello **Summary** page and click **Next**.</span></span>
6. <span data-ttu-id="7c9ea-383">Tıklatın **son** hello dağıtım işlemi tamamlandıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-383">Click **Finish** after hello deployment operation is finished.</span></span>

<span data-ttu-id="7c9ea-384">Dağıttığınızda, dağıtılan tooAzure Data Factory hizmetinin hello varlıklardır önce hello hello yapılandırma dosyasından hello JSON dosyalarında özellikler için kullanılan tooset değerler değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-384">When you deploy, hello values from hello configuration file are used tooset values for properties in hello JSON files before hello entities are deployed tooAzure Data Factory service.</span></span>   

## <a name="use-azure-key-vault"></a><span data-ttu-id="7c9ea-385">Azure Key Vault kullanma</span><span class="sxs-lookup"><span data-stu-id="7c9ea-385">Use Azure Key Vault</span></span>
<span data-ttu-id="7c9ea-386">Şu önerilir ve genellikle karşı güvenlik ilkesi toocommit bağlantı dizeleri toohello kod deposu gibi hassas verileri değil.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-386">It is not advisable and often against security policy toocommit sensitive data such as connection strings toohello code repository.</span></span> <span data-ttu-id="7c9ea-387">Bkz: [ADF güvenli yayımlama](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) Azure anahtar kasası hassas bilgilerini depolamak ve Data Factory varlıklarını yayımlanırken kullanmayla ilgili GitHub toolearn üzerinde örnek.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-387">See [ADF Secure Publish](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/ADFSecurePublish) sample on GitHub toolearn about storing sensitive information in Azure Key Vault and using it while publishing Data Factory entities.</span></span> <span data-ttu-id="7c9ea-388">Visual Studio uzantısı güvenli yayımlama Hello anahtar kasasında depolanan hello gizli toobe sağlar ve yalnızca başvuruları toothem bağlantılı Hizmetleri belirtilen / dağıtım yapılandırmaları.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-388">hello Secure Publish extension for Visual Studio allows hello secrets toobe stored in Key Vault and only references toothem are specified in linked services/ deployment configurations.</span></span> <span data-ttu-id="7c9ea-389">Data Factory varlıkları tooAzure yayımladığınızda, bu başvuruları çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-389">These references are resolved when you publish Data Factory entities tooAzure.</span></span> <span data-ttu-id="7c9ea-390">Bu dosyalar ardından tüm gizli gösterme olmadan kaydedilmiş toosource deposu olabilir.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-390">These files can then be committed toosource repository without exposing any secrets.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7c9ea-391">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7c9ea-391">Next steps</span></span>
<span data-ttu-id="7c9ea-392">Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-392">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="7c9ea-393">Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7c9ea-393">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="7c9ea-394">nasıl bir veri öğesine/öğesinden toocopy veri deposu hakkında toolearn hello veri deposu hello tablosundaki hello bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="7c9ea-394">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>
