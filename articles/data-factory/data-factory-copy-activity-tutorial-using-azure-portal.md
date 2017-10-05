---
title: "Öğretici: Verileri kopyalamak amacıyla Azure Data Factory işlem hattı oluşturma | Microsoft Docs"
description: "Bu öğreticide, Azure blob depolama alanından Azure SQL veritabanına veri kopyalamak için Azure portalını kullanarak Kopyalama Etkinliği içeren Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: d9317652-0170-4fd3-b9b2-37711272162b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 8072a863fab0b304ccbbba639aa56b403e8f37c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-use-azure-portal-to-create-a-data-factory-pipeline-to-copy-data"></a><span data-ttu-id="1cb6c-103">Öğretici: Verileri kopyalamak amacıyla Data Factory işlem hattı oluşturmak için Azure portalını kullanma | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="1cb6c-103">Tutorial: Use Azure portal to create a Data Factory pipeline to copy data</span></span> 
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1cb6c-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1cb6c-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="1cb6c-105">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="1cb6c-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="1cb6c-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1cb6c-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="1cb6c-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1cb6c-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="1cb6c-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1cb6c-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="1cb6c-109">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="1cb6c-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="1cb6c-110">REST API</span><span class="sxs-lookup"><span data-stu-id="1cb6c-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="1cb6c-111">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="1cb6c-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

<span data-ttu-id="1cb6c-112">Bu makalede, Azure blob depolama alanından Azure SQL veritabanına veri kopyalayan bir işlem hattıyla veri fabrikası oluşturmak için [Azure portalını](https://portal.azure.com) nasıl kullanacağınızı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-112">In this article, you learn how to use [Azure portal](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="1cb6c-113">Azure Data Factory’yi ilk kez kullanıyorsanız bu öğreticiyi tamamlamadan önce [Azure Data Factory’ye Giriş](data-factory-introduction.md) makalesini okuyun.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="1cb6c-114">Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="1cb6c-115">Kopyalama etkinliği, verileri, desteklenen bir veri deposundan desteklenen bir havuz veri deposuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="1cb6c-116">Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="1cb6c-117">Etkinlik, çeşitli veri depolama alanları arasında güvenli, güvenilir ve ölçeklenebilir bir yolla veri kopyalayabilen genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="1cb6c-118">Kopyalama Etkinliği hakkında daha fazla bilgi için bkz. [Veri Taşıma Etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="1cb6c-119">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="1cb6c-120">Bir etkinliğin çıkış veri kümesini diğer etkinliğin giriş veri kümesi olarak ayarlayarak iki etkinliği zincirleyebilir, yani bir etkinliğin diğerinden sonra çalıştırılmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="1cb6c-121">Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="1cb6c-122">Bu öğreticideki veri işlem hattı, bir kaynak veri deposundaki verileri hedef veri deposuna kopyalar.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-122">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="1cb6c-123">Azure Data Factory kullanarak verileri dönüştürme hakkında bir öğretici için bkz. [Öğretici: Hadoop kümesi kullanarak verileri dönüştürmek için işlem hattı oluşturma](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-123">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1cb6c-124">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1cb6c-124">Prerequisites</span></span>
<span data-ttu-id="1cb6c-125">Bu öğreticiyi uygulamadan önce [öğretici önkoşulları](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) makalesinde listelenen önkoşulları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-125">Complete prerequisites listed in the [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="steps"></a><span data-ttu-id="1cb6c-126">Adımlar</span><span class="sxs-lookup"><span data-stu-id="1cb6c-126">Steps</span></span>
<span data-ttu-id="1cb6c-127">Bu eğitimin bir parçası olarak gerçekleştireceğiniz adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-127">Here are the steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="1cb6c-128">Azure **veri fabrikası** oluşturma.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-128">Create an Azure **data factory**.</span></span> <span data-ttu-id="1cb6c-129">Bu adımda, ADFTutorialDataFactory adlı bir veri fabrikası oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-129">In this step, you create a data factory named ADFTutorialDataFactory.</span></span> 
2. <span data-ttu-id="1cb6c-130">Veri fabrikasında **bağlı hizmetler** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-130">Create **linked services** in the data factory.</span></span> <span data-ttu-id="1cb6c-131">Bu adımda Azure Depolama ve Azure SQL Veritabanı türünde iki bağlı hizmet oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-131">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="1cb6c-132">AzureStorageLinkedService, Azure depolama hesabınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-132">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="1cb6c-133">Bir kapsayıcı oluşturup verileri [ön koşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak bu depolama hesabına yüklediniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-133">You created a container and uploaded data to this storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="1cb6c-134">AzureSqlLinkedService, Azure SQL veritabanınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-134">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="1cb6c-135">Blob depolama alanından kopyalanan veriler bu veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-135">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="1cb6c-136">Bu veritabanındaki SQL tablosunu, [ön koşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-136">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="1cb6c-137">Veri fabrikasında girdi ve çıktı **veri kümesi oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-137">Create input and output **datasets** in the data factory.</span></span>  
    
    <span data-ttu-id="1cb6c-138">Azure depolama bağlı hizmeti, Data Factory hizmetinin Azure depolama hesabınıza bağlanmak için çalışma zamanında kullandığı bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-138">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="1cb6c-139">Giriş blob veri kümesi ise kapsayıcıyı ve girdi verilerini içeren klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-139">And, the input blob dataset specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="1cb6c-140">Benzer şekilde, Azure SQL Veritabanı bağlı hizmeti, Data Factory hizmetinin Azure SQL veritabanınıza bağlanmak için çalışma zamanında kullandığı bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-140">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="1cb6c-141">Çıktı SQL tablosu veri kümesi ise blob depolama alanındaki verilerin kopyalandığı veritabanında tabloyu belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-141">And, the output SQL table dataset specifies the table in the database to which the data from the blob storage is copied.</span></span>
4. <span data-ttu-id="1cb6c-142">Veri fabrikasında **işlem hattı** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-142">Create a **pipeline** in the data factory.</span></span> <span data-ttu-id="1cb6c-143">Bu adımda, kopyalama etkinliği ile bir işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-143">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="1cb6c-144">Kopyalama etkinliği, verileri Azure blob depolama alanındaki bir blobdan Azure SQL veritabanındaki tabloya kopyalar.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-144">The copy activity copies data from a blob in the Azure blob storage to a table in the Azure SQL database.</span></span> <span data-ttu-id="1cb6c-145">Verileri desteklenen herhangi bir kaynaktan desteklenen herhangi bir hedefe kopyalamak için bir işlem hattındaki kopyalama etkinliğini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-145">You can use a copy activity in a pipeline to copy data from any supported source to any supported destination.</span></span> <span data-ttu-id="1cb6c-146">Desteklenen veri depolarının bir listesi için [veri taşıma etkinlikleri](data-factory-data-movement-activities.md#supported-data-stores-and-formats) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-146">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="1cb6c-147">İşlem hattını izleme.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-147">Monitor the pipeline.</span></span> <span data-ttu-id="1cb6c-148">Bu adımda, girdi ve çıktı veri kümelerinin dilimlerini Azure portalını kullanarak **izlersiniz**.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-148">In this step, you **monitor** the slices of input and output datasets by using Azure portal.</span></span> 

## <a name="create-data-factory"></a><span data-ttu-id="1cb6c-149">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cb6c-149">Create data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1cb6c-150">Henüz yapmadıysanız, [öğreticinin ön koşullarını](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-150">Complete [prerequisites for the tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="1cb6c-151">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-151">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="1cb6c-152">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-152">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="1cb6c-153">Örneğin, verileri bir kaynaktan bir hedef veri deposuna kopyalamak için Kopyalama Etkinliği, giriş verilerini ürün çıkış verilerine dönüştürecek Hive betiğini çalıştırmak için de HDInsight Hive etkinliği.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-153">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="1cb6c-154">Bu adımda data factory oluşturmayla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-154">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="1cb6c-155">[Azure portalında](https://portal.azure.com/) oturum açtıktan sonra sol taraftaki menüde **Yeni**'ye tıklayın, **Zeka + Analiz**'i seçin ve **Data Factory**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-155">After logging in to the [Azure portal](https://portal.azure.com/), click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 
   
   ![Yeni->DataFactory](./media/data-factory-copy-activity-tutorial-using-azure-portal/NewDataFactoryMenu.png)    
2. <span data-ttu-id="1cb6c-157">**Yeni data factory** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-157">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="1cb6c-158">**Ad** için **ADFTutorialDataFactory** girin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-158">Enter **ADFTutorialDataFactory** for the **name**.</span></span> 
      
         ![Yeni veri fabrikası dikey penceresi](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-new-data-factory.png)
      
       <span data-ttu-id="1cb6c-160">Azure data factory adı **küresel olarak benzersiz** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-160">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="1cb6c-161">Aşağıdaki hatayı alırsanız veri fabrikasının adını değiştirin (örneğin adınızADFTutorialDataFactory) ve oluşturmayı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-161">If you receive the following error, change the name of the data factory (for example, yournameADFTutorialDataFactory) and try creating again.</span></span> <span data-ttu-id="1cb6c-162">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-162">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
      
           Data factory name “ADFTutorialDataFactory” is not available  
      
       ![Data Factory adı yok](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-not-available.png)
   2. <span data-ttu-id="1cb6c-164">Veri fabrikasını oluşturmak istediğiniz Azure **aboneliğini** seçin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-164">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
   3. <span data-ttu-id="1cb6c-165">**Kaynak Grubu** için aşağıdaki adımlardan birini uygulayın:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-165">For the **Resource Group**, do one of the following steps:</span></span>
      
      - <span data-ttu-id="1cb6c-166">**Var olanı kullan**’ı seçin ve ardından açılır listeden var olan bir kaynak grubu belirleyin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-166">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
      - <span data-ttu-id="1cb6c-167">**Yeni oluştur**’u seçin ve bir kaynak grubunun adını girin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-167">Select **Create new**, and enter the name of a resource group.</span></span>   
         
          <span data-ttu-id="1cb6c-168">Bu öğreticideki adımlardan bazıları kaynak grubu için şu adı kullandığınızı varsayar: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-168">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="1cb6c-169">Kaynak grupları hakkında daha fazla bilgi için bkz. [Azure kaynaklarınızı yönetmek için kaynak gruplarını kullanma](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-169">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>  
   4. <span data-ttu-id="1cb6c-170">Data factory için **konum** seçin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-170">Select the **location** for the data factory.</span></span> <span data-ttu-id="1cb6c-171">Açılır listede yalnızca Data Factory hizmeti tarafından desteklenen bölgeler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-171">Only regions supported by the Data Factory service are shown in the drop-down list.</span></span>
   5. <span data-ttu-id="1cb6c-172">**Panoya sabitle**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-172">Select **Pin to dashboard**.</span></span>     
   6. <span data-ttu-id="1cb6c-173">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-173">Click **Create**.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="1cb6c-174">Data Factory örnekleri oluşturmak için abonelik/kaynak grubu düzeyinde [Data Factory Katılımcısı](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) rolünün üyesi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-174">To create Data Factory instances, you must be a member of the [Data Factory Contributor](../active-directory/role-based-access-built-in-roles.md#data-factory-contributor) role at the subscription/resource group level.</span></span>
      > 
      > <span data-ttu-id="1cb6c-175">Data factory adı gelecekte bir DNS adı olarak kaydedilmiş olabilir; bu nedenle herkese görünür hale gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-175">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>                
      > 
      > 
3. <span data-ttu-id="1cb6c-176">Panoda şu kutucuğu ve üzerinde şu durumu görürsünüz: **Veri fabrikası dağıtılıyor**.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-176">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![veri fabrikası dağıtılıyor kutucuğu](media/data-factory-copy-activity-tutorial-using-azure-portal/deploying-data-factory.png)
4. <span data-ttu-id="1cb6c-178">Oluşturma işlemi tamamlandıktan sonra, görüntüde gösterildiği gibi **Data Factory** dikey penceresini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-178">After the creation is complete, you see the **Data Factory** blade as shown in the image.</span></span>
   
   ![Data factory giriş sayfası](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-data-factory-home-page.png)

## <a name="create-linked-services"></a><span data-ttu-id="1cb6c-180">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cb6c-180">Create linked services</span></span>
<span data-ttu-id="1cb6c-181">Veri depolarınızı ve işlem hizmetlerinizi veri fabrikasına bağlamak için veri fabrikasında bağlı hizmetler oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-181">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="1cb6c-182">Bu öğreticide, Azure HDInsight veya Azure Data Lake Analytics gibi herhangi bir işlem hizmeti kullanmazsınız.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-182">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="1cb6c-183">Azure Depolama (kaynak) ve Azure SQL Veritabanı (hedef) türünde iki veri deposu kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-183">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="1cb6c-184">Bu nedenle, AzureStorage ve AzureSqlDatabase türlerinde AzureStorageLinkedService ve AzureSqlLinkedService adlı iki bağlı hizmet oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-184">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="1cb6c-185">AzureStorageLinkedService, Azure depolama hesabınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-185">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="1cb6c-186">Bu depolama hesabı, kapsayıcı oluşturduğunuz ve verileri [ön koşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak yüklediğiniz hesaptır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-186">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="1cb6c-187">AzureSqlLinkedService, Azure SQL veritabanınızı veri fabrikasına bağlar.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-187">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="1cb6c-188">Blob depolama alanından kopyalanan veriler bu veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-188">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="1cb6c-189">Bu veritabanındaki emp tablosunu, [ön koşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-189">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>  

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="1cb6c-190">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cb6c-190">Create Azure Storage linked service</span></span>
<span data-ttu-id="1cb6c-191">Bu adımda, Azure depolama hesabınızı veri fabrikanıza bağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-191">In this step, you link your Azure storage account to your data factory.</span></span> <span data-ttu-id="1cb6c-192">Bu bölümde Azure depolama hesabınızın adını ve anahtarını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-192">You specify the name and key of your Azure storage account in this section.</span></span>  

1. <span data-ttu-id="1cb6c-193">**Data Factory** dikey penceresinde **Geliştir ve dağıt** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-193">In the **Data Factory** blade, click **Author and deploy** tile.</span></span>
   
   ![Geliştir ve Dağıt Kutucuğu](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-author-deploy-tile.png) 
2. <span data-ttu-id="1cb6c-195">Bu resimdeki gibi **Data Factory Düzenleyicisi**'ni göreceksiniz:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-195">You see the **Data Factory Editor** as shown in the following image:</span></span> 

    ![Data Factory Düzenleyicisi](./media/data-factory-copy-activity-tutorial-using-azure-portal/data-factory-editor.png)
3. <span data-ttu-id="1cb6c-197">Düzenleyici'de, araç çubuğundaki **Yeni veri deposu** düğmesine tıklayın ve açılan menüden **Azure depolama**'yı seçin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-197">In the editor, click **New data store** button on the toolbar and select **Azure storage** from the drop-down menu.</span></span> <span data-ttu-id="1cb6c-198">Sağ bölmede Azure depolama bağlı hizmeti oluşturmak için JSON şablonunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-198">You should see the JSON template for creating an Azure storage linked service in the right pane.</span></span> 
   
    ![Düzenleyici Yeni veri deposu düğmesi](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-newdatastore-button.png)    
3. <span data-ttu-id="1cb6c-200">Burada, `<accountname>` ve `<accountkey>` sözcüklerini Azure depolama hesabınıza ait hesap adı ve hesap anahtarı değerleriyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-200">Replace `<accountname>` and `<accountkey>` with the account name and account key values for your Azure storage account.</span></span> 
   
    ![Düzenleyici Blob Storage JSON](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-json.png)    
4. <span data-ttu-id="1cb6c-202">Araç çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-202">Click **Deploy** on the toolbar.</span></span> <span data-ttu-id="1cb6c-203">Dağıtılan **AzureStorageLinkedService** öğesini şu anda ağaçta görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-203">You should see the deployed **AzureStorageLinkedService** in the tree view now.</span></span> 
   
    ![Düzenleyici Blob Storage Dağıtma](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-editor-blob-storage-deploy.png)

    <span data-ttu-id="1cb6c-205">Bağlı hizmet tanımındaki JSON özellikleri hakkında daha fazla bilgi için [Azure Blob Depolama bağlayıcısı](data-factory-azure-blob-connector.md#linked-service-properties) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-205">For more information about JSON properties in the linked service definition, see [Azure Blob Storage connector](data-factory-azure-blob-connector.md#linked-service-properties) article.</span></span>

### <a name="create-a-linked-service-for-the-azure-sql-database"></a><span data-ttu-id="1cb6c-206">Azure SQL Database için bağlı hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cb6c-206">Create a linked service for the Azure SQL Database</span></span>
<span data-ttu-id="1cb6c-207">Bu adımda, Azure SQL veritabanınızı veri fabrikanıza bağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-207">In this step, you link your Azure SQL database to your data factory.</span></span> <span data-ttu-id="1cb6c-208">Bu bölümde Azure SQL sunucu adı, veritabanı adı, kullanıcı adı ve kullanıcı parolasını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-208">You specify the Azure SQL server name, database name, user name, and user password in this section.</span></span> 

1. <span data-ttu-id="1cb6c-209">**Data Factory Düzenleyici**’de, araç çubuğundaki **Yeni veri deposu** düğmesine tıklayın ve açılan menüden **Azure SQL Veritabanı**’nı seçin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-209">In the **Data Factory Editor**, click **New data store** button on the toolbar and select **Azure SQL Database** from the drop-down menu.</span></span> <span data-ttu-id="1cb6c-210">Sağ bölmede Azure SQL bağlı hizmeti oluşturmak için JSON şablonunu görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-210">You should see the JSON template for creating the Azure SQL linked service in the right pane.</span></span>
2. <span data-ttu-id="1cb6c-211">`<servername>`, `<databasename>`, `<username>@<servername>` ve `<password>` öğesini Azure SQL sunucusu, veritabanı, kullanıcı hesabı ve parolası ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-211">Replace `<servername>`, `<databasename>`, `<username>@<servername>`, and `<password>` with names of your Azure SQL server, database, user account, and password.</span></span> 
3. <span data-ttu-id="1cb6c-212">**AzureSqlLinkedService**’i oluşturmak ve dağıtmak için araç çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-212">Click **Deploy** on the toolbar to create and deploy the **AzureSqlLinkedService**.</span></span>
4. <span data-ttu-id="1cb6c-213">Ağaç görünümünde **Bağlı hizmetler** bölümünde **AzureSqlLinkedService** öğesini gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-213">Confirm that you see **AzureSqlLinkedService** in the tree view under **Linked services**.</span></span>  

    <span data-ttu-id="1cb6c-214">Bu JSON özellikleri hakkında daha fazla bilgi için [Azure SQL Veritabanı bağlayıcısı](data-factory-azure-sql-connector.md#linked-service-properties) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-214">For more information about these JSON properties, see [Azure SQL Database connector](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>

## <a name="create-datasets"></a><span data-ttu-id="1cb6c-215">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cb6c-215">Create datasets</span></span>
<span data-ttu-id="1cb6c-216">Önceki adımda, Azure Depolama hesabınızı ve Azure SQL veritabanınızı veri fabrikanıza bağlamak için bağlı hizmetler oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-216">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="1cb6c-217">Bu adımda, sırasıyla AzureStorageLinkedService ve AzureSqlLinkedService tarafından başvurulan veri depolarında depolanan girdi ve çıktı verilerini temsil eden InputDataset ve OutputDataset adlı iki veri kümesini tanımlarsınız.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-217">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="1cb6c-218">Azure depolama bağlı hizmeti, Data Factory hizmetinin Azure depolama hesabınıza bağlanmak için çalışma zamanında kullandığı bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-218">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="1cb6c-219">Giriş blobu veri kümesi (InputDataset) ise kapsayıcıyı ve girdi verilerini içeren klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-219">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

<span data-ttu-id="1cb6c-220">Benzer şekilde, Azure SQL Veritabanı bağlı hizmeti, Data Factory hizmetinin Azure SQL veritabanınıza bağlanmak için çalışma zamanında kullandığı bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-220">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="1cb6c-221">Çıktı SQL tablosu veri kümesi (OutputDataset) ise blob depolama alanındaki verilerin kopyalandığı veritabanında tabloyu belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-221">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span> 

### <a name="create-input-dataset"></a><span data-ttu-id="1cb6c-222">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cb6c-222">Create input dataset</span></span>
<span data-ttu-id="1cb6c-223">Bu adımda, InputDataset adlı bir veri kümesi oluşturursunuz. Bu veri kümesi, AzureStorageLinkedService bağlı hizmetiyle temsil edilen Azure Depolama’daki bir blob kapsayıcısının (adftutorial) kök klasöründe bulunan blob dosyasını (emp.txt) işaret eder.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-223">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="1cb6c-224">fileName için bir değer belirtmezseniz (veya bu adımı atlarsanız) girdi klasöründe bulunan tüm blob’lardaki veriler hedefe kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-224">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="1cb6c-225">Bu öğreticide, dosya adı için bir değer belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-225">In this tutorial, you specify a value for the fileName.</span></span> 

1. <span data-ttu-id="1cb6c-226">Data Factory **Düzenleyici**’de açılır listeden **... Daha fazla**, **Yeni veri kümesi** ve **Azure Blob depolama** öğelerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-226">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure Blob storage** from the drop-down menu.</span></span> 
   
    ![Yeni veri kümesi menüsü](./media/data-factory-copy-activity-tutorial-using-azure-portal/new-dataset-menu.png)
2. <span data-ttu-id="1cb6c-228">Sağ bölmedeki JSON ifadesini aşağıdaki JSON parçacığıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-228">Replace JSON in the right pane with the following JSON snippet:</span></span> 
   
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
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
          "folderPath": "adftutorial/",
          "fileName": "emp.txt",
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

    <span data-ttu-id="1cb6c-229">Aşağıdaki tabloda, kod parçacığında kullanılan JSON özellikleri için açıklamalar verilmektedir:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-229">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="1cb6c-230">Özellik</span><span class="sxs-lookup"><span data-stu-id="1cb6c-230">Property</span></span> | <span data-ttu-id="1cb6c-231">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1cb6c-231">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="1cb6c-232">type</span><span class="sxs-lookup"><span data-stu-id="1cb6c-232">type</span></span> | <span data-ttu-id="1cb6c-233">Veriler Azure blob depolama alanında yer aldığından type özelliği **AzureBlob** olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-233">The type property is set to **AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="1cb6c-234">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1cb6c-234">linkedServiceName</span></span> | <span data-ttu-id="1cb6c-235">Daha önce oluşturduğunuz **AzureStorageLinkedService**’e başvurur.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-235">Refers to the **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="1cb6c-236">folderPath</span><span class="sxs-lookup"><span data-stu-id="1cb6c-236">folderPath</span></span> | <span data-ttu-id="1cb6c-237">blob **kapsayıcıyı** ve girdi blob’larını içeren **klasörü** belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-237">Specifies the blob **container** and the **folder** that contains input blobs.</span></span> <span data-ttu-id="1cb6c-238">Bu öğreticide adftutorial, blob kapsayıcısıdır ve klasör, kök klasördür.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-238">In this tutorial, adftutorial is the blob container and folder is the root folder.</span></span> | 
    | <span data-ttu-id="1cb6c-239">fileName</span><span class="sxs-lookup"><span data-stu-id="1cb6c-239">fileName</span></span> | <span data-ttu-id="1cb6c-240">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-240">This property is optional.</span></span> <span data-ttu-id="1cb6c-241">Bu özelliği atarsanız tüm folderPath dosyaları alınır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-241">If you omit this property, all files from the folderPath are picked.</span></span> <span data-ttu-id="1cb6c-242">Bu öğreticide fileName için **emp.txt** belirtilir, bu nedenle işlem için yalnızca bu dosya seçilir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-242">In this tutorial, **emp.txt** is specified for the fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="1cb6c-243">format -> type</span><span class="sxs-lookup"><span data-stu-id="1cb6c-243">format -> type</span></span> |<span data-ttu-id="1cb6c-244">Girdi dosyası metin biçiminde olduğundan **TextFormat**'ı kullanırız.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-244">The input file is in the text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="1cb6c-245">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="1cb6c-245">columnDelimiter</span></span> | <span data-ttu-id="1cb6c-246">Girdi dosyasındaki sütunlar, **virgül (`,`)** ile ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-246">The columns in the input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="1cb6c-247">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="1cb6c-247">frequency/interval</span></span> | <span data-ttu-id="1cb6c-248">frequency **Saat**, interval da **1** olarak ayarlanmıştır. Bu, girdi dilimlerinin **saatlik** olarak kullanılabileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-248">The frequency is set to **Hour** and interval is  set to **1**, which means that the input slices are available **hourly**.</span></span> <span data-ttu-id="1cb6c-249">Başka bir deyişle, Data Factory hizmeti belirttiğiniz blob kapsayıcısının (**adftutorial**) kök klasöründe girdi verilerini saatte bir kere arar.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-249">In other words, the Data Factory service looks for input data every hour in the root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="1cb6c-250">İşlem hattı başlangıç ve bitiş zamanlarındaki verileri arar, bu zamanlardan önceki veya sonraki verileri aramaz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-250">It looks for the data within the pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="1cb6c-251">external</span><span class="sxs-lookup"><span data-stu-id="1cb6c-251">external</span></span> | <span data-ttu-id="1cb6c-252">Bu özellik, veriler bu işlem hattı tarafından oluşturulmazsa **true** olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-252">This property is set to **true** if the data is not generated by this pipeline.</span></span> <span data-ttu-id="1cb6c-253">Bu öğreticideki girdi verileri, bu işlem hattı tarafından oluşturulmayan emp.txt dosyasında bulunur, bu nedenle bu özelliği true olarak ayarlarız.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-253">The input data in this tutorial is in the emp.txt file, which is not generated by this pipeline, so we set this property to true.</span></span> |

    <span data-ttu-id="1cb6c-254">Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-254">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>      
3. <span data-ttu-id="1cb6c-255">**InputDataset** veri kümesini oluşturmak ve dağıtmak için araç çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-255">Click **Deploy** on the toolbar to create and deploy the **InputDataset** dataset.</span></span> <span data-ttu-id="1cb6c-256">**InputDataset** öğesini ağaç görünümünde gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-256">Confirm that you see the **InputDataset** in the tree view.</span></span>

### <a name="create-output-dataset"></a><span data-ttu-id="1cb6c-257">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cb6c-257">Create output dataset</span></span>
<span data-ttu-id="1cb6c-258">Azure SQL Veritabanı bağlı hizmeti, Data Factory hizmetinin Azure SQL veritabanınıza bağlanmak için çalışma zamanında kullandığı bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-258">The Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="1cb6c-259">Bu adımda oluşturduğunuz çıktı SQL tablosu veri kümesi (OututDataset), blob depolama alanındaki verilerin kopyalandığı veritabanında tabloyu belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-259">The output SQL table dataset (OututDataset) you create in this step specifies the table in the database to which the data from the blob storage is copied.</span></span>

1. <span data-ttu-id="1cb6c-260">Data Factory **Düzenleyici**’de açılır listeden **... Daha fazla**, **Yeni veri kümesi** ve **Azure SQL** öğelerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-260">In the **Editor** for the Data Factory, click **... More**, click **New dataset**, and click **Azure SQL** from the drop-down menu.</span></span> 
2. <span data-ttu-id="1cb6c-261">Sağ bölmedeki JSON ifadesini aşağıdaki JSON parçacığıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-261">Replace JSON in the right pane with the following JSON snippet:</span></span>

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
        "linkedServiceName": "AzureSqlLinkedService",
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

    <span data-ttu-id="1cb6c-262">Aşağıdaki tabloda, kod parçacığında kullanılan JSON özellikleri için açıklamalar verilmektedir:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-262">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

    | <span data-ttu-id="1cb6c-263">Özellik</span><span class="sxs-lookup"><span data-stu-id="1cb6c-263">Property</span></span> | <span data-ttu-id="1cb6c-264">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1cb6c-264">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="1cb6c-265">type</span><span class="sxs-lookup"><span data-stu-id="1cb6c-265">type</span></span> | <span data-ttu-id="1cb6c-266">type özelliği, veriler Azure SQL veritabanındaki bir tabloya kopyalandığından **AzureSqlTable** olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-266">The type property is set to **AzureSqlTable** because data is copied to a table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="1cb6c-267">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1cb6c-267">linkedServiceName</span></span> | <span data-ttu-id="1cb6c-268">Daha önce oluşturduğunuz **AzureSqlLinkedService**’e başvurur.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-268">Refers to the **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="1cb6c-269">tableName</span><span class="sxs-lookup"><span data-stu-id="1cb6c-269">tableName</span></span> | <span data-ttu-id="1cb6c-270">Verilerin kopyalandığı **tabloyu** belirtir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-270">Specified the **table** to which the data is copied.</span></span> | 
    | <span data-ttu-id="1cb6c-271">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="1cb6c-271">frequency/interval</span></span> | <span data-ttu-id="1cb6c-272">frequency **Saatlik** ve interval **1** olarak ayarlanır. Bu durumda çıktı dilimleri, işlem hattı başlangıç ve bitiş zamanları arasında **saatlik** olarak üretilir, bu zamanlardan önce veya sonra üretilmez.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-272">The frequency is set to **Hour** and interval is **1**, which means that the output slices are produced **hourly** between the pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="1cb6c-273">Veritabanındaki emp tablosunda üç sütun vardır: **ID**, **FirstName** ve **LastName**.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-273">There are three columns – **ID**, **FirstName**, and **LastName** – in the emp table in the database.</span></span> <span data-ttu-id="1cb6c-274">ID bir kimlik sütunu olduğundan, burada yalnızca **FirstName** ve **LastName** değerlerini belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-274">ID is an identity column, so you need to specify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="1cb6c-275">Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure SQL bağlayıcısı makalesi](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-275">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="1cb6c-276">**OutputDataset** veri kümesini oluşturmak ve dağıtmak için araç çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-276">Click **Deploy** on the toolbar to create and deploy the **OutputDataset** dataset.</span></span> <span data-ttu-id="1cb6c-277">**OutputDataset** öğesini ağaç görünümünde **Veri kümeleri** altında gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-277">Confirm that you see the **OutputDataset** in the tree view under **Datasets**.</span></span> 

## <a name="create-pipeline"></a><span data-ttu-id="1cb6c-278">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1cb6c-278">Create pipeline</span></span>
<span data-ttu-id="1cb6c-279">Bu adımda, girdi olarak **InputDataset** ve çıktı olarak **OutputDataset** kullanan **kopyalama etkinliğine** sahip bir işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-279">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="1cb6c-280">Şu anda zamanlamayı çıktı veri kümesi yürütmektedir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-280">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="1cb6c-281">Bu öğreticide, çıktı veri kümesi saatte bir dilim oluşturacak şekilde yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-281">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="1cb6c-282">İşlem hattının başlangıç zamanı ve bitiş zamanı arasında bir gün, yani 24 saat vardır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-282">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="1cb6c-283">Bu nedenle, işlem hattı çıktı veri kümesinden 24 dilim oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-283">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span> 

1. <span data-ttu-id="1cb6c-284">Data Factory **Düzenleyici**’de açılır listeden **... Daha fazla** ve **Yeni işlem hattı** öğelerine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-284">In the **Editor** for the Data Factory, click **... More**, and click **New pipeline**.</span></span> <span data-ttu-id="1cb6c-285">Alternatif olarak, ağaç görünümünde **İşlem hatları**’na sağ tıklayın ve**Yeni işlem hattı**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-285">Alternatively, you can right-click **Pipelines** in the tree view and click **New pipeline**.</span></span>
2. <span data-ttu-id="1cb6c-286">Sağ bölmedeki JSON ifadesini aşağıdaki JSON parçacığıyla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-286">Replace JSON in the right pane with the following JSON snippet:</span></span> 

    ```json   
    {
      "name": "ADFTutorialPipeline",
      "properties": {
        "description": "Copy data from a blob to Azure SQL table",
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
              "retry": 0,
              "timeout": "01:00:00"
            }
          }
        ],
        "start": "2017-05-11T00:00:00Z",
        "end": "2017-05-12T00:00:00Z"
      }
    } 
    ```   
    
    <span data-ttu-id="1cb6c-287">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-287">Note the following points:</span></span>
   
    - <span data-ttu-id="1cb6c-288">Etkinlikler bölümünde, **türü** **Copy** olarak ayarlanmış yalnızca bir etkinlik vardır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-288">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="1cb6c-289">Kopyalama etkinliği hakkında daha fazla bilgi için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-289">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="1cb6c-290">Data Factory çözümlerinde, [veri dönüştürme etkinliklerini](data-factory-data-transformation-activities.md) de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="1cb6c-291">Etkinlik girdisi **InputDataset** olarak, etkinlik çıktısı ise **OutputDataset** olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-291">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="1cb6c-292">**typeProperties** bölümünde **BlobSource** kaynak türü, **SqlSink** de havuz türü olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-292">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="1cb6c-293">Kaynak ve havuz olarak kopyalama etkinliği tarafından desteklenen veri depolarının eksiksiz listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-293">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="1cb6c-294">Kaynak/havuz olarak desteklenen belirli bir veri deposunu nasıl kullanacağınızı öğrenmek için tablodaki bağlantıya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-294">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>
    - <span data-ttu-id="1cb6c-295">Başlangıç ve bitiş tarih saatleri [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-295">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="1cb6c-296">Örneğin: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-296">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="1cb6c-297">**End** zamanı isteğe bağlıdır; ancak bu öğreticide bunu kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-297">The **end** time is optional, but we use it in this tutorial.</span></span> <span data-ttu-id="1cb6c-298">**end** özelliği için değer belirtmezseniz "**start + 48 hours**" olarak hesaplanır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-298">If you do not specify value for the **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="1cb6c-299">İşlem hattını süresiz olarak çalıştırmak için **end** özelliği değerini **9999-09-09** olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-299">To run the pipeline indefinitely, specify **9999-09-09** as the value for the **end** property.</span></span>
     
    <span data-ttu-id="1cb6c-300">Önceki örnekte, her veri dilimi saatlik oluşturulduğundan 24 veri dilimi vardır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-300">In the preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="1cb6c-301">İşlem hattı tanımındaki JSON özelliklerinin açıklamaları için [işlem hatları oluşturma](data-factory-create-pipelines.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-301">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1cb6c-302">Kopyalama etkinliği tanımındaki JSON özelliklerinin açıklamaları için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-302">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="1cb6c-303">BlobSource tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-303">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="1cb6c-304">SqlSink tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure SQL Veritabanı bağlayıcısı makalesi](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-304">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
3. <span data-ttu-id="1cb6c-305">**ADFTutorialPipeline** tablosunu oluşturmak ve dağıtmak için araç çubuğunda **Dağıt**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-305">Click **Deploy** on the toolbar to create and deploy the **ADFTutorialPipeline**.</span></span> <span data-ttu-id="1cb6c-306">İşlem hattını ağaç görünümünde gördüğünüzü onaylayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-306">Confirm that you see the pipeline in the tree view.</span></span> 
4. <span data-ttu-id="1cb6c-307">Şimdi, **Düzenleyici** dikey penceresini **X** işaretine tıklayarak kapatın. **X** simgesine yeniden tıklayarak **ADFTutorialDataFactory** için **Data Factory** giriş sayfasını görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-307">Now, close the **Editor** blade by clicking **X**. Click **X** again to see the **Data Factory** home page for the **ADFTutorialDataFactory**.</span></span>

<span data-ttu-id="1cb6c-308">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="1cb6c-308">**Congratulations!**</span></span> <span data-ttu-id="1cb6c-309">Azure blob depolamadan bir Azure SQL veritabanına veri kopyalamak üzere işlem hattına sahip bir Azure veri fabrikasını başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-309">You have successfully created an Azure data factory with a pipeline to copy data from an Azure blob storage to an Azure SQL database.</span></span> 


## <a name="monitor-pipeline"></a><span data-ttu-id="1cb6c-310">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="1cb6c-310">Monitor pipeline</span></span>
<span data-ttu-id="1cb6c-311">Bu adımda, Azure data factory’de neler olduğunu izlemek için Azure Portal kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-311">In this step, you use the Azure portal to monitor what’s going on in an Azure data factory.</span></span>    

### <a name="monitor-pipeline-using-monitor--manage-app"></a><span data-ttu-id="1cb6c-312">İzleme ve Yönetme Uygulamasını kullanarak işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="1cb6c-312">Monitor pipeline using Monitor & Manage App</span></span>
<span data-ttu-id="1cb6c-313">Aşağıdaki adımlar İzleme ve Yönetme uygulamasını kullanarak veri fabrikanızdaki işlem hatlarını nasıl izleyeceğinizi göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-313">The following steps show you how to monitor pipelines in your data factory by using the Monitor & Manage application:</span></span> 

1. <span data-ttu-id="1cb6c-314">Data factory’nin giriş sayfasındaki **İzleme ve Yönetme** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-314">Click **Monitor & Manage** tile on the home page for your data factory.</span></span>
   
    ![İzleme ve Yönetme kutucuğu](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-manage-tile.png) 
2. <span data-ttu-id="1cb6c-316">**İzleme ve Yönetme uygulaması** ayrı bir sekmede açılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-316">You should see **Monitor & Manage application** in a separate tab.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="1cb6c-317">Web tarayıcısının "Yetkilendiriliyor..." durumunda takıldığını görürseniz **Üçüncü taraf tanımlama bilgilerini ve site verilerini engelle** ayarının işaretini kaldırın (ya da) **login.microsoftonline.com** için bir özel durum oluşturun ve ardından uygulamayı yeniden başlatmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-317">If you see that the web browser is stuck at "Authorizing...", do one of the following: clear the **Block third-party cookies and site data** check box (or) create an exception for **login.microsoftonline.com**, and then try to open the app again.</span></span>

    ![İzleme ve Yönetme Uygulaması](./media/data-factory-copy-activity-tutorial-using-azure-portal/monitor-and-manage-app.png)
3. <span data-ttu-id="1cb6c-319">**Başlangıç saati** ve **Bitiş saati**'ni işlem hattınızın başlangıç (2017-05-11) ve bitiş saatlerini (2017-05-12) içerecek şekilde değiştirin ve **Uygula**'ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-319">Change the **Start time** and **End time** to include start (2017-05-11) and end times (2017-05-12) of your pipeline, and click **Apply**.</span></span>       
3. <span data-ttu-id="1cb6c-320">İşlem hattı başlangıç ve bitiş saatleri arasındaki saatlerle ilişkilendirilmiş **etkinlik pencerelerini** orta bölmede görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-320">You see the **activity windows** associated with each hour between pipeline start and end times in the list in the middle pane.</span></span> 
4. <span data-ttu-id="1cb6c-321">Bir etkinlik penceresinin ayrıntılarını görmek için **Etkinlik Pencereleri** listesinde seçin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-321">To see details about an activity window, select the activity window in the **Activity Windows** list.</span></span> 
    <span data-ttu-id="1cb6c-322">![Etkinlik penceresi ayrıntıları](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span><span class="sxs-lookup"><span data-stu-id="1cb6c-322">![Activity window details](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-window-details.png)</span></span>

    <span data-ttu-id="1cb6c-323">Sağ taraftaki Etkinlik Penceresi Gezgini'nde geçerli saate (20:12) kadar olan dilimlerin işlendiğini (yeşil renkli olduğunu) göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-323">In Activity Window Explorer on the right, you see that the slices up to the current UTC time (8:12 PM) are all processed (in green color).</span></span> <span data-ttu-id="1cb6c-324">20-21, 21-22, 22-23 ve 23-00 dilimleri henüz işlenmemiştir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-324">The 8-9 PM, 9 - 10 PM, 10 - 11 PM, 11 PM - 12 AM slices are not processed yet.</span></span>

    <span data-ttu-id="1cb6c-325">Sağ bölmedeki **Denemeler**bölümünde veri dilimi için çalıştırılan etkinlik hakkında bilgiler yer alır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-325">The **Attempts** section in the right pane provides information about the activity run for the data slice.</span></span> <span data-ttu-id="1cb6c-326">Bir hata varsa onunla ilgili bilgiler de eklenir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-326">If there was an error, it provides details about the error.</span></span> <span data-ttu-id="1cb6c-327">Örneğin girdi klasörü veya kapsayıcı mevcut değilse ve dilim işleme başarısız olursa kapsayıcının veya klasörün bulunmadığını belirten bir hata iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-327">For example, if the input folder or container does not exist and the slice processing fails, you see an error message stating that the container or folder does not exist.</span></span>

    ![Etkinlik çalıştırma denemeleri](./media/data-factory-copy-activity-tutorial-using-azure-portal/activity-run-attempts.png) 
4. <span data-ttu-id="1cb6c-329">**SQL Server Management Studio**’yu başlatın, Azure SQL Veritabanı’na bağlanın ve veritabanındaki **emp** tablosuna satırların eklenmiş olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-329">Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.</span></span>
    
    ![sql sorgu sonuçları](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)

<span data-ttu-id="1cb6c-331">Bu uygulamanın kullanımına ilişkin ayrıntılı bilgi için bkz. [İzleme ve Yönetme Uygulamasını kullanarak Azure Data Factory işlem hatlarını izleme ve yönetme](data-factory-monitor-manage-app.md).</span><span class="sxs-lookup"><span data-stu-id="1cb6c-331">For detailed information about using this application, see [Monitor and manage Azure Data Factory pipelines using Monitoring and Management App](data-factory-monitor-manage-app.md).</span></span>

### <a name="monitor-pipeline-using-diagram-view"></a><span data-ttu-id="1cb6c-332">Diyagram Görünümünü kullanarak işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="1cb6c-332">Monitor pipeline using Diagram View</span></span>
<span data-ttu-id="1cb6c-333">Veri işlem hatlarını diyagram görünümüyle de izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-333">You can also monitor data pipelines by using the diagram view.</span></span>  

1. <span data-ttu-id="1cb6c-334">**Data Factory** dikey penceresinde **Diyagram**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-334">In the **Data Factory** blade, click **Diagram**.</span></span>
   
    ![Data Factory Dikey Penceresi - Diyagram Kutucuğu](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-datafactoryblade-diagramtile.png)
2. <span data-ttu-id="1cb6c-336">Aşağıdaki görüntüye benzer bir diyagram görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-336">You should see the diagram similar to the following image:</span></span> 
   
    ![Diyagram görünümü](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-diagram-blade.png)  
5. <span data-ttu-id="1cb6c-338">Diyagram görünümünde **InputDataset**'e çift tıklayarak veri kümesinin dilimlerini görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-338">In the diagram view, double-click **InputDataset** to see slices for the dataset.</span></span>  
   
    ![InputDataset seçiliyken veri kümeleri](./media/data-factory-copy-activity-tutorial-using-azure-portal/DataSetsWithInputDatasetFromBlobSelected.png)   
5. <span data-ttu-id="1cb6c-340">Tüm veri dilimlerini görmek için **Daha fazlasını gör** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-340">Click **See more** link to see all the data slices.</span></span> <span data-ttu-id="1cb6c-341">İşlem hattı başlangıç ve bitiş saatleri arasında 24 saatlik dilim göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-341">You see 24 hourly slices between pipeline start and end times.</span></span> 
   
    ![Tüm girdi veri dilimleri](./media/data-factory-copy-activity-tutorial-using-azure-portal/all-input-slices.png)  
   
    <span data-ttu-id="1cb6c-343">**emp.txt** dosyası her zaman **adftutorial\input** blob kapsayıcısında yer aldığından geçerli UTC saatine kadar olan tüm veri dilimleri **Hazır**'dır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-343">Notice that all the data slices up to the current UTC time are **Ready** because the **emp.txt** file exists all the time in the blob container: **adftutorial\input**.</span></span> <span data-ttu-id="1cb6c-344">Geleceğe yönelik dilimler hazır değil durumundadır.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-344">The slices for the future times are not in ready state yet.</span></span> <span data-ttu-id="1cb6c-345">Alttaki **En son başarısız olan dilimler** bölümünde hiç dilim gösterilmediğini onaylayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-345">Confirm that no slices show up in the **Recently failed slices** section at the bottom.</span></span>
6. <span data-ttu-id="1cb6c-346">Diyagram görünümüne ulaşana kadar dikey pencereleri kapatın veya diyagram görünümüne geçmek için sola kaydırın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-346">Close the blades until you see the diagram view (or) scroll left to see the diagram view.</span></span> <span data-ttu-id="1cb6c-347">Ardından **OutputDataset** öğesine çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-347">Then, double-click **OutputDataset**.</span></span> 
8. <span data-ttu-id="1cb6c-348">Tüm dilimleri görmek için **OutputDataset** öğesine ait **Tablo** dikey penceresinde **Daha fazlasını gör** bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-348">Click **See more** link on the **Table** blade for **OutputDataset** to see all the slices.</span></span>

    ![veri dilimleri dikey penceresi](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslices-blade.png) 
9. <span data-ttu-id="1cb6c-350">Geçerli UTC saatine kadar olan tüm dilimlerin durumunun **bekleyen yürütme** yerine => **Sürüyor** ==> **Hazır** durumuna geçtiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-350">Notice that all the slices up to the current UTC time move from **pending execution** state => **In progress** ==> **Ready** state.</span></span> <span data-ttu-id="1cb6c-351">Geçmiş dilimler (geçerli saat öncesi) varsayılan olarak en yeniden en eskiye doğru işlenir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-351">The slices from the past (before current time) are processed from latest to oldest by default.</span></span> <span data-ttu-id="1cb6c-352">Örneğin geçerli saat 20:12 UTC ise 19-20 dilimi 18-19 diliminden önce işlenir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-352">For example, if the current time is 8:12 PM UTC, the slice for 7 PM - 8 PM is processed ahead of the 6 PM - 7 PM slice.</span></span> <span data-ttu-id="1cb6c-353">20-21 dilimi varsayılan olarak zaman aralığın sonunda,yani 21 sonrasında işlenir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-353">The 8 PM - 9 PM slice is processed at the end of the time interval by default, that is after 9 PM.</span></span>  
10. <span data-ttu-id="1cb6c-354">Listeden herhangi bir veri dilimine tıklayın; **Veri dilimi** dikey penceresini görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-354">Click any data slice from the list and you should see the **Data slice** blade.</span></span> <span data-ttu-id="1cb6c-355">Bir etkinlik penceresiyle ilişkilendirilmiş veri parçasına dilim adı verilir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-355">A piece of data associated with an activity window is called a slice.</span></span> <span data-ttu-id="1cb6c-356">Bir dilim bir veya birden çok dosya olabilir.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-356">A slice can be one file or multiple files.</span></span>  
    
     ![veri dilimi dikey penceresi](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-dataslice-blade.png)
    
     <span data-ttu-id="1cb6c-358">Dilim **Hazır** durumunda değilse, Hazır olmayan ve geçerli dilimin yürütülmesini engelleyen yukarı akış dilimlerini **Hazır olmayan yukarı akış dilimleri** listesinde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-358">If the slice is not in the **Ready** state, you can see the upstream slices that are not Ready and are blocking the current slice from executing in the **Upstream slices that are not ready** list.</span></span>
11. <span data-ttu-id="1cb6c-359">**VERİ DİLİMİ** dikey penceresinde, alttaki listede tüm etkinlik çalıştırmalarını görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-359">In the **DATA SLICE** blade, you should see all activity runs in the list at the bottom.</span></span> <span data-ttu-id="1cb6c-360">**Etkinlik çalışma ayrıntıları** dikey penceresini görmek için bir **etkinlik çalışması**’na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-360">Click an **activity run** to see the **Activity run details** blade.</span></span> 
    
    ![Etkinlik Çalışma Ayrıntıları](./media/data-factory-copy-activity-tutorial-using-azure-portal/ActivityRunDetails.png)

    <span data-ttu-id="1cb6c-362">Bu dikey pencerede kopyalama işleminin ne kadar sürdüğünü, aktarım hızını, kaç bayt veri okunup yazıldığını, çalışma başlangıç zamanını, çalışma bitiş zamanını vs. görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-362">In this blade, you see how long the copy operation took, what throughput is, how many bytes of data were read and written, run start time, run end time etc.</span></span>  
12. <span data-ttu-id="1cb6c-363">**ADFTutorialDataFactory** giriş dikey penceresine dönene kadar tüm dikey pencereleri kapatmak için **X** işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-363">Click **X** to close all the blades until you get back to the home blade for the **ADFTutorialDataFactory**.</span></span>
13. <span data-ttu-id="1cb6c-364">(isteğe bağlı) Önceki adımlarda gördüğünüz dikey pencerelere ulaşmak için **Veri kümeleri** kutucuğuna veya **İşlem hatları** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-364">(optional) click the **Datasets** tile or **Pipelines** tile to get the blades you have seen the preceding steps.</span></span> 
14. <span data-ttu-id="1cb6c-365">**SQL Server Management Studio**’yu başlatın, Azure SQL Veritabanı’na bağlanın ve veritabanındaki **emp** tablosuna satırların eklenmiş olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-365">Launch **SQL Server Management Studio**, connect to the Azure SQL Database, and verify that the rows are inserted in to the **emp** table in the database.</span></span>
    
    ![sql sorgu sonuçları](./media/data-factory-copy-activity-tutorial-using-azure-portal/getstarted-sql-query-results.png)


## <a name="summary"></a><span data-ttu-id="1cb6c-367">Özet</span><span class="sxs-lookup"><span data-stu-id="1cb6c-367">Summary</span></span>
<span data-ttu-id="1cb6c-368">Bu öğreticide Azure blob’undan Azure SQL veritabanına veri kopyalamak üzere Azure data factory oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-368">In this tutorial, you created an Azure data factory to copy data from an Azure blob to an Azure SQL database.</span></span> <span data-ttu-id="1cb6c-369">Data factory, bağlı hizmetler, veri kümeleri ve işlem hattı oluşturmak için Azure Portal’ı kullandınız.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-369">You used the Azure portal to create the data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="1cb6c-370">Bu öğreticide gerçekleştirilen üst düzey adımları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-370">Here are the high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="1cb6c-371">Azure **data factory** oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-371">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="1cb6c-372">Oluşturulan **bağlı hizmetler**:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-372">Created **linked services**:</span></span>
   1. <span data-ttu-id="1cb6c-373">Girdi verilerini tutan Azure Storage hesabınıza bağlamak için **Azure Storage** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-373">An **Azure Storage** linked service to link your Azure Storage account that holds input data.</span></span>     
   2. <span data-ttu-id="1cb6c-374">Çıktı verilerini tutan Azure SQL veritabanınıza bağlamak için **Azure SQL** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-374">An **Azure SQL** linked service to link your Azure SQL database that holds the output data.</span></span> 
3. <span data-ttu-id="1cb6c-375">İşlem hatları için girdi verilerini ve çıktı verilerini açıklayan oluşturulan **veri kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-375">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="1cb6c-376">Kaynak olarak **BlobSource**’u, havuz olarak da **SqlSink**’i kapsayan **Kopyalama Etkinliği**’ne sahip oluşturulan **işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-376">Created a **pipeline** with a **Copy Activity** with **BlobSource** as source and **SqlSink** as sink.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1cb6c-377">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1cb6c-377">Next steps</span></span>
<span data-ttu-id="1cb6c-378">Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-378">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="1cb6c-379">Aşağıdaki tabloda, kopyalama etkinliği tarafından kaynak ve hedef olarak desteklenen veri depolarının listesi sağlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="1cb6c-379">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="1cb6c-380">Veri deposundan/veri deposuna veri kopyalama hakkında bilgi edinmek için tablodaki veri deposunun bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1cb6c-380">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>