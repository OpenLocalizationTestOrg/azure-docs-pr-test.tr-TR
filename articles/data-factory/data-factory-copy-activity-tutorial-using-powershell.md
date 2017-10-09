---
title: "Öğretici: Azure PowerShell kullanarak bir ardışık düzen toomove veri oluşturma | Microsoft Docs"
description: "Bu öğreticide, Azure PowerShell kullanarak Kopyalama Etkinliği ile bir Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 71087349-9365-4e95-9847-170658216ed8
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 21406d7dfaa0c555b2538fbb52839d761c140fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-data-factory-pipeline-that-moves-data-by-using-azure-powershell"></a><span data-ttu-id="4e04c-103">Öğretici: Azure PowerShell kullanarak verileri taşıyan bir Data Factory işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e04c-103">Tutorial: Create a Data Factory pipeline that moves data by using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4e04c-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4e04c-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="4e04c-105">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="4e04c-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="4e04c-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4e04c-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="4e04c-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4e04c-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="4e04c-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e04c-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="4e04c-109">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="4e04c-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="4e04c-110">REST API</span><span class="sxs-lookup"><span data-stu-id="4e04c-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="4e04c-111">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="4e04c-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
>
>

<span data-ttu-id="4e04c-112">Bu makalede, bilgi nasıl toouse PowerShell toocreate data factory Azure blob depolama tooan Azure SQL veritabanına verileri kopyalayan bir işlem hattı ile.</span><span class="sxs-lookup"><span data-stu-id="4e04c-112">In this article, you learn how toouse PowerShell toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="4e04c-113">Yeni tooAzure Data Factory varsa, hello okuma [giriş tooAzure Data Factory](data-factory-introduction.md) Bu öğretici yapmadan önce makalesi.</span><span class="sxs-lookup"><span data-stu-id="4e04c-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="4e04c-114">Bu öğreticide, içinde bir etkinlik olan işlem hattı oluşturursunuz: Kopyalama Etkinliği.</span><span class="sxs-lookup"><span data-stu-id="4e04c-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="4e04c-115">Merhaba kopyalama etkinliği bir desteklenen veri deposu tooa desteklenen havuz veri deposundan verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="4e04c-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="4e04c-116">Kaynak ve havuz olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="4e04c-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="4e04c-117">Merhaba etkinlik verileri güvenli, güvenilir ve ölçeklenebilir bir şekilde çeşitli veri depolamaları arasında kopyalayabilirsiniz genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="4e04c-118">Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="4e04c-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="4e04c-119">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="4e04c-120">Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="4e04c-121">Daha fazla bilgi için bkz. [bir işlem hattında birden fazla etkinlik](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="4e04c-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

> [!NOTE]
> <span data-ttu-id="4e04c-122">Bu makalede, tüm hello Data Factory cmdlet'lerini kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-122">This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="4e04c-123">Bu cmdlet’leri hakkında kapsamlı bilgi için bkz. [Data Factory Cmdlet Başvurusu](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="4e04c-123">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on these cmdlets.</span></span>
> 
> <span data-ttu-id="4e04c-124">Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="4e04c-124">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="4e04c-125">Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak bir ardışık düzen tootransform veri derleme](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="4e04c-125">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e04c-126">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4e04c-126">Prerequisites</span></span>
- <span data-ttu-id="4e04c-127">Hello listelenen önkoşulları tamamlamanız [öğretici önkoşulları](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="4e04c-127">Complete prerequisites listed in hello [tutorial prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article.</span></span>
- <span data-ttu-id="4e04c-128">**Azure PowerShell**'i yükleyin.</span><span class="sxs-lookup"><span data-stu-id="4e04c-128">Install **Azure PowerShell**.</span></span> <span data-ttu-id="4e04c-129">Merhaba yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](../powershell-install-configure.md).</span><span class="sxs-lookup"><span data-stu-id="4e04c-129">Follow hello instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md).</span></span>

## <a name="steps"></a><span data-ttu-id="4e04c-130">Adımlar</span><span class="sxs-lookup"><span data-stu-id="4e04c-130">Steps</span></span>
<span data-ttu-id="4e04c-131">Bu öğretici bir parçası olarak gerçekleştirdiğiniz hello adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4e04c-131">Here are hello steps you perform as part of this tutorial:</span></span>

1. <span data-ttu-id="4e04c-132">Azure **veri fabrikası** oluşturma.</span><span class="sxs-lookup"><span data-stu-id="4e04c-132">Create an Azure **data factory**.</span></span> <span data-ttu-id="4e04c-133">Bu adımda, ADFTutorialDataFactoryPSH adlı bir veri fabrikası oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-133">In this step, you create a data factory named ADFTutorialDataFactoryPSH.</span></span> 
2. <span data-ttu-id="4e04c-134">Oluşturma **bağlantılı Hizmetleri** hello veri fabrikası'nda.</span><span class="sxs-lookup"><span data-stu-id="4e04c-134">Create **linked services** in hello data factory.</span></span> <span data-ttu-id="4e04c-135">Bu adımda Azure Depolama ve Azure SQL Veritabanı türünde iki bağlı hizmet oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-135">In this step, you create two linked services of types: Azure Storage and Azure SQL Database.</span></span> 
    
    <span data-ttu-id="4e04c-136">Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="4e04c-136">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="4e04c-137">Bir kapsayıcı oluşturulur ve veri toothis depolama hesabı bir parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4e04c-137">You created a container and uploaded data toothis storage account as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

    <span data-ttu-id="4e04c-138">AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="4e04c-138">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="4e04c-139">Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="4e04c-139">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="4e04c-140">Bu veritabanındaki SQL tablosunu, [ön koşulların](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) parçası olarak oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-140">You created a SQL table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   
3. <span data-ttu-id="4e04c-141">Giriş ve çıkış oluşturma **veri kümeleri** hello veri fabrikası'nda.</span><span class="sxs-lookup"><span data-stu-id="4e04c-141">Create input and output **datasets** in hello data factory.</span></span>  
    
    <span data-ttu-id="4e04c-142">Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-142">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="4e04c-143">Ve hello giriş blob dataset hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-143">And, hello input blob dataset specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="4e04c-144">Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-144">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="4e04c-145">Ve hello veritabanı toowhich hello verileri hello blob depolama biriminden hello tabloda kopyalanır hello çıktı SQL tablosu veri kümesi belirtir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-145">And, hello output SQL table dataset specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>
4. <span data-ttu-id="4e04c-146">Oluşturma bir **ardışık düzen** hello veri fabrikası'nda.</span><span class="sxs-lookup"><span data-stu-id="4e04c-146">Create a **pipeline** in hello data factory.</span></span> <span data-ttu-id="4e04c-147">Bu adımda, kopyalama etkinliği ile bir işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-147">In this step, you create a pipeline with a copy activity.</span></span>   
    
    <span data-ttu-id="4e04c-148">Merhaba kopyalama etkinliği hello Azure blob depolama tooa hello Azure SQL veritabanı tablosunda bir blob veri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="4e04c-148">hello copy activity copies data from a blob in hello Azure blob storage tooa table in hello Azure SQL database.</span></span> <span data-ttu-id="4e04c-149">Kopyalama etkinliği herhangi bir desteklenen kaynak desteklenen tooany hedefin bir ardışık düzen toocopy verileri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-149">You can use a copy activity in a pipeline toocopy data from any supported source tooany supported destination.</span></span> <span data-ttu-id="4e04c-150">Desteklenen veri depolarının bir listesi için [veri taşıma etkinlikleri](data-factory-data-movement-activities.md#supported-data-stores-and-formats) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-150">For a list of supported data stores, see [data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> 
5. <span data-ttu-id="4e04c-151">Merhaba işlem hattını izleme.</span><span class="sxs-lookup"><span data-stu-id="4e04c-151">Monitor hello pipeline.</span></span> <span data-ttu-id="4e04c-152">Bu adımda, **İzleyici** hello girdi ve çıktı veri kümeleri dilimleri PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4e04c-152">In this step, you **monitor** hello slices of input and output datasets by using PowerShell.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="4e04c-153">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e04c-153">Create a data factory</span></span>
> [!IMPORTANT]
> <span data-ttu-id="4e04c-154">Tam [hello öğreticisi için Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) zaten yapmadıysanız.</span><span class="sxs-lookup"><span data-stu-id="4e04c-154">Complete [prerequisites for hello tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) if you haven't already done so.</span></span>   

<span data-ttu-id="4e04c-155">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-155">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="4e04c-156">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-156">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="4e04c-157">Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform veri tooproduct çıktı verileri girin.</span><span class="sxs-lookup"><span data-stu-id="4e04c-157">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="4e04c-158">Bu adımda hello data factory oluşturmayla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="4e04c-158">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="4e04c-159">**PowerShell**’i başlatın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-159">Launch **PowerShell**.</span></span> <span data-ttu-id="4e04c-160">Bu öğreticide hello sonuna kadar Azure PowerShell'i açık tutun.</span><span class="sxs-lookup"><span data-stu-id="4e04c-160">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="4e04c-161">Kapatıp yeniden açın, toorun hello komutları yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-161">If you close and reopen, you need toorun hello commands again.</span></span>

    <span data-ttu-id="4e04c-162">Hello aşağıdaki komutu çalıştırın ve hello kullanıcı adı ve parola toosign toohello Azure portalını kullanın girin:</span><span class="sxs-lookup"><span data-stu-id="4e04c-162">Run hello following command, and enter hello user name and password that you use toosign in toohello Azure portal:</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```   
   
    <span data-ttu-id="4e04c-163">Komut tooview aşağıdaki hello hello abonelikler bu hesap için çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4e04c-163">Run hello following command tooview all hello subscriptions for this account:</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```

    <span data-ttu-id="4e04c-164">Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu.</span><span class="sxs-lookup"><span data-stu-id="4e04c-164">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="4e04c-165">Değiştir  **&lt;NameOfAzureSubscription** &gt; , Azure aboneliğinizin hello adı:</span><span class="sxs-lookup"><span data-stu-id="4e04c-165">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription:</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
2. <span data-ttu-id="4e04c-166">Adlı bir Azure kaynak grubu oluşturma **ADFTutorialResourceGroup** hello aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="4e04c-166">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    
    <span data-ttu-id="4e04c-167">Bu öğreticideki hello adımlardan bazıları adlı hello kaynak grubunu kullandığınızı varsayar **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="4e04c-167">Some of hello steps in this tutorial assume that you use hello resource group named **ADFTutorialResourceGroup**.</span></span> <span data-ttu-id="4e04c-168">Farklı bir kaynak grubu kullanıyorsanız, toouse gerekir, bu öğreticide ADFTutorialResourceGroup yerine.</span><span class="sxs-lookup"><span data-stu-id="4e04c-168">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="4e04c-169">Merhaba çalıştırmak **New-AzureRmDataFactory** cmdlet toocreate adlı bir veri fabrikası **ADFTutorialDataFactoryPSH**:</span><span class="sxs-lookup"><span data-stu-id="4e04c-169">Run hello **New-AzureRmDataFactory** cmdlet toocreate a data factory named **ADFTutorialDataFactoryPSH**:</span></span>  

    ```PowerShell
    $df=New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH –Location "West US"
    ```
    <span data-ttu-id="4e04c-170">Bu ad zaten alınmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-170">This name may already have been taken.</span></span> <span data-ttu-id="4e04c-171">Bu nedenle, hello veri fabrikasının hello adı benzersiz bir önek veya sonek ekleyerek olun (örneğin: ADFTutorialDataFactoryPSH05152017) ve hello komutunu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-171">Therefore, make hello name of hello data factory unique by adding a prefix or suffix (for example: ADFTutorialDataFactoryPSH05152017) and run hello command again.</span></span>  

<span data-ttu-id="4e04c-172">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="4e04c-172">Note hello following points:</span></span>

* <span data-ttu-id="4e04c-173">Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-173">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="4e04c-174">Merhaba aşağıdaki hata alırsanız, hello adını (örneğin, yournameADFTutorialDataFactoryPSH) değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4e04c-174">If you receive hello following error, change hello name (for example, yournameADFTutorialDataFactoryPSH).</span></span> <span data-ttu-id="4e04c-175">Bu öğreticide adımları uygularken ADFTutorialFactoryPSH yerine bu adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-175">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="4e04c-176">Data Factory yapıtları için bkz. [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="4e04c-176">See [Data Factory - Naming Rules](data-factory-naming-rules.md) for Data Factory artifacts.</span></span>

    ```
    Data factory name “ADFTutorialDataFactoryPSH” is not available
    ```
* <span data-ttu-id="4e04c-177">toocreate Data Factory örnekleri, katkıda bulunan veya hello Azure abonelik yöneticisi olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-177">toocreate Data Factory instances, you must be a contributor or administrator of hello Azure subscription.</span></span>
* <span data-ttu-id="4e04c-178">hello veri fabrikasının Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-178">hello name of hello data factory may be registered as a DNS name in hello future, and hence become publicly visible.</span></span>
* <span data-ttu-id="4e04c-179">Aşağıdaki hata hello alabilirsiniz: "**Bu abonelik, Microsoft.DataFactory kayıtlı toouse ad değil.**"</span><span class="sxs-lookup"><span data-stu-id="4e04c-179">You may receive hello following error: "**This subscription is not registered toouse namespace Microsoft.DataFactory.**"</span></span> <span data-ttu-id="4e04c-180">Merhaba aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:</span><span class="sxs-lookup"><span data-stu-id="4e04c-180">Do one of hello following, and try publishing again:</span></span>

  * <span data-ttu-id="4e04c-181">Azure PowerShell'de komut tooregister hello Data Factory sağlayıcısının aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4e04c-181">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

    <span data-ttu-id="4e04c-182">Data Factory sağlayıcısını hello komutu tooconfirm aşağıdaki çalışma hello kaydedilir:</span><span class="sxs-lookup"><span data-stu-id="4e04c-182">Run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="4e04c-183">Azure aboneliği toohello hello kullanarak oturum açma [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4e04c-183">Sign in by using hello Azure subscription toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="4e04c-184">Tooa Data Factory dikey penceresine gidin veya hello Azure portalında bir data factory oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4e04c-184">Go tooa Data Factory blade, or create a data factory in hello Azure portal.</span></span> <span data-ttu-id="4e04c-185">Bu eylemin hello sağlayıcıyı sizin için otomatik olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="4e04c-185">This action automatically registers hello provider for you.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="4e04c-186">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e04c-186">Create linked services</span></span>
<span data-ttu-id="4e04c-187">Verilerinizi depolayan ve Hizmetleri toohello veri fabrikası işlem bir veri fabrikası toolink bağlı hizmetler oluşturma.</span><span class="sxs-lookup"><span data-stu-id="4e04c-187">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="4e04c-188">Bu öğreticide, Azure HDInsight veya Azure Data Lake Analytics gibi herhangi bir işlem hizmeti kullanmazsınız.</span><span class="sxs-lookup"><span data-stu-id="4e04c-188">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="4e04c-189">Azure Depolama (kaynak) ve Azure SQL Veritabanı (hedef) türünde iki veri deposu kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="4e04c-189">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

<span data-ttu-id="4e04c-190">Bu nedenle, AzureStorage ve AzureSqlDatabase türlerinde AzureStorageLinkedService ve AzureSqlLinkedService adlı iki bağlı hizmet oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-190">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

<span data-ttu-id="4e04c-191">Merhaba AzureStorageLinkedService Azure depolama hesabı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="4e04c-191">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="4e04c-192">Bu depolama hesap hello biri, hangi, kapsayıcı oluşturuldu ve hello veri parçası olarak yüklenen [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4e04c-192">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>   

<span data-ttu-id="4e04c-193">AzureSqlLinkedService Azure SQL veritabanı toohello veri fabrikanıza bağlar.</span><span class="sxs-lookup"><span data-stu-id="4e04c-193">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="4e04c-194">Merhaba blob depolama biriminden kopyalanan hello veriler bu veritabanında depolanır.</span><span class="sxs-lookup"><span data-stu-id="4e04c-194">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="4e04c-195">Bu veritabanında hello emp tablosunda bir parçası olarak oluşturulan [Önkoşullar](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4e04c-195">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

### <a name="create-a-linked-service-for-an-azure-storage-account"></a><span data-ttu-id="4e04c-196">Azure depolama hesabı için bağlı hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e04c-196">Create a linked service for an Azure storage account</span></span>
<span data-ttu-id="4e04c-197">Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-197">In this step, you link your Azure storage account tooyour data factory.</span></span>

1. <span data-ttu-id="4e04c-198">Adlı bir JSON dosyası oluşturun **AzureStorageLinkedService.json** içinde **C:\ADFGetStartedPSH** içeriği aşağıdaki hello klasörüyle: (oluşturma hello zaten yoksa ADFGetStartedPSH klasörünü.)</span><span class="sxs-lookup"><span data-stu-id="4e04c-198">Create a JSON file named **AzureStorageLinkedService.json** in **C:\ADFGetStartedPSH** folder with hello following content: (Create hello folder ADFGetStartedPSH if it does not already exist.)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4e04c-199">Değiştir &lt;accountname&gt; ve &lt;accountkey&gt; adı ve anahtar hello dosyayı kaydetmeden önce Azure depolama hesabınızın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-199">Replace &lt;accountname&gt; and &lt;accountkey&gt; with name and key of your Azure storage account before saving hello file.</span></span> 

    ```json
    {
        "name": "AzureStorageLinkedService",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        }
     }
    ``` 
2. <span data-ttu-id="4e04c-200">İçinde **Azure PowerShell**, toohello geçiş **ADFGetStartedPSH** klasör.</span><span class="sxs-lookup"><span data-stu-id="4e04c-200">In **Azure PowerShell**, switch toohello **ADFGetStartedPSH** folder.</span></span>
4. <span data-ttu-id="4e04c-201">Merhaba çalıştırmak **New-AzureRmDataFactoryLinkedService** cmdlet toocreate hello bağlantılı hizmeti: **AzureStorageLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4e04c-201">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet toocreate hello linked service: **AzureStorageLinkedService**.</span></span> <span data-ttu-id="4e04c-202">Bu cmdlet ve diğer Data Factory cmdlet'leri Bu öğreticide kullandığınız gerektirir toopass değerleri Merhaba **ResourceGroupName** ve **DataFactoryName** parametreleri.</span><span class="sxs-lookup"><span data-stu-id="4e04c-202">This cmdlet, and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello **ResourceGroupName** and **DataFactoryName** parameters.</span></span> <span data-ttu-id="4e04c-203">Alternatif olarak, bir cmdlet'i her çalıştırdığınızda ResourceGroupName ve DataFactoryName yazmadan hello New-AzureRmDataFactory cmdlet tarafından döndürülen hello DataFactory nesnesini geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-203">Alternatively, you can pass hello DataFactory object returned by hello New-AzureRmDataFactory cmdlet without typing ResourceGroupName and DataFactoryName each time you run a cmdlet.</span></span> 

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureStorageLinkedService.json
    ```
    <span data-ttu-id="4e04c-204">Merhaba örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4e04c-204">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureStorageLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ``` 

    <span data-ttu-id="4e04c-205">Bu bağlı hizmeti oluşturma diğer toospecify kaynak grubu adı ve hello DataFactory nesnesini belirtme yerine veri fabrikası adı yoludur.</span><span class="sxs-lookup"><span data-stu-id="4e04c-205">Other way of creating this linked service is toospecify resource group name and data factory name instead of specifying hello DataFactory object.</span></span>  

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName <Name of your data factory> -File .\AzureStorageLinkedService.json
    ```

### <a name="create-a-linked-service-for-an-azure-sql-database"></a><span data-ttu-id="4e04c-206">Azure SQL veritabanı için bağlı hizmet oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e04c-206">Create a linked service for an Azure SQL database</span></span>
<span data-ttu-id="4e04c-207">Bu adımda, Azure SQL veritabanı tooyour veri fabrikanıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-207">In this step, you link your Azure SQL database tooyour data factory.</span></span>

1. <span data-ttu-id="4e04c-208">İçerik aşağıdaki hello ile C:\ADFGetStartedPSH klasöründe AzureSqlLinkedService.json adlı bir JSON dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="4e04c-208">Create a JSON file named AzureSqlLinkedService.json in C:\ADFGetStartedPSH folder with hello following content:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4e04c-209">&lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt; ve &lt;password&gt; sözcüklerini Azure SQL sunucunuzun, veritabanınızın, kullanıcı hesabınızın adlarıyla ve parolasıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="4e04c-209">Replace &lt;servername&gt;, &lt;databasename&gt;, &lt;username@servername&gt;, and &lt;password&gt; with names of your Azure SQL server, database, user account, and password.</span></span>
    
    ```json
    {
        "name": "AzureSqlLinkedService",
        "properties": {
            "type": "AzureSqlDatabase",
            "typeProperties": {
                "connectionString": "Server=tcp:<server>.database.windows.net,1433;Database=<databasename>;User ID=<user>@<server>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
            }
        }
     }
    ```
2. <span data-ttu-id="4e04c-210">Komut toocreate aşağıdaki hello bağlı hizmet çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4e04c-210">Run hello following command toocreate a linked service:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\AzureSqlLinkedService.json
    ```
    
    <span data-ttu-id="4e04c-211">Merhaba örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4e04c-211">Here is hello sample output:</span></span>

    ```
    LinkedServiceName : AzureSqlLinkedService
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.LinkedServiceProperties
    ProvisioningState : Succeeded
    ```

   <span data-ttu-id="4e04c-212">Onaylayın **tooAzure Hizmetleri erişimine izin** ayarının açık SQL veritabanı sunucunuz için.</span><span class="sxs-lookup"><span data-stu-id="4e04c-212">Confirm that **Allow access tooAzure services** setting is turned on for your SQL database server.</span></span> <span data-ttu-id="4e04c-213">tooverify ve açın, adımları hello:</span><span class="sxs-lookup"><span data-stu-id="4e04c-213">tooverify and turn it on, do hello following steps:</span></span>

    1. <span data-ttu-id="4e04c-214">İçinde toohello oturum [Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="4e04c-214">Log in toohello [Azure portal](https://portal.azure.com)</span></span>
    2. <span data-ttu-id="4e04c-215">Tıklatın **daha fazla hizmet >** hello solda ve tıklatın **SQL sunucuları** hello içinde **veritabanları** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="4e04c-215">Click **More services >** on hello left, and click **SQL servers** in hello **DATABASES** category.</span></span>
    3. <span data-ttu-id="4e04c-216">Sunucunuzu hello SQL Server listesinde seçin.</span><span class="sxs-lookup"><span data-stu-id="4e04c-216">Select your server in hello list of SQL servers.</span></span>
    4. <span data-ttu-id="4e04c-217">Merhaba SQL server dikey penceresinde **güvenlik duvarı ayarlarını göster** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="4e04c-217">On hello SQL server blade, click **Show firewall settings** link.</span></span>
    5. <span data-ttu-id="4e04c-218">Merhaba, **Güvenlik Duvarı ayarları** dikey penceresinde tıklatın **ON** için **tooAzure Hizmetleri erişimine izin**.</span><span class="sxs-lookup"><span data-stu-id="4e04c-218">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
    6. <span data-ttu-id="4e04c-219">Tıklatın **kaydetmek** hello araç.</span><span class="sxs-lookup"><span data-stu-id="4e04c-219">Click **Save** on hello toolbar.</span></span> 

## <a name="create-datasets"></a><span data-ttu-id="4e04c-220">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e04c-220">Create datasets</span></span>
<span data-ttu-id="4e04c-221">Merhaba önceki adımda, Azure Storage hesabını ve Azure SQL veritabanı tooyour veri fabrikası bağlı hizmetler toolink oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="4e04c-221">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="4e04c-222">Bu adımda, iki veri kümesi InputDataset ve giriş temsil OutputDataset ve sırasıyla AzureStorageLinkedService ve Azuresqllinkedservice'in başvurduğu hello veri depolarında depolanan çıktı verilerini adlı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-222">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

<span data-ttu-id="4e04c-223">Hello Azure depolama bağlı hizmeti çalışma zamanı tooconnect tooyour Azure depolama hesabı Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-223">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="4e04c-224">Ve hello giriş blob veri kümesi (InputDataset) hello kapsayıcı ve hello giriş verisi içeren hello klasörü belirtir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-224">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

<span data-ttu-id="4e04c-225">Benzer şekilde, hello Azure SQL veritabanı bağlantılı hizmet çalışma zamanı tooconnect tooyour Azure SQL veritabanını Data Factory hizmetinin kullandığı hello bağlantı dizesini belirtir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-225">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="4e04c-226">Ve kopyalanan verileri hello blob depolama biriminden hello veritabanı toowhich hello SQL tablosu veri kümesi (OututDataset) hello tabloda hello çıktı.</span><span class="sxs-lookup"><span data-stu-id="4e04c-226">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span> 

### <a name="create-an-input-dataset"></a><span data-ttu-id="4e04c-227">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e04c-227">Create an input dataset</span></span>
<span data-ttu-id="4e04c-228">Bu adımda, tooa blob dosya (emp.txt) işaret InputDataset adlı bir veri hello kök klasöründe bir blob kapsayıcısını (adftutorial) hello Azure hello AzureStorageLinkedService bağlı hizmeti tarafından temsil edilen depolama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4e04c-228">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="4e04c-229">Verme hello dosya adı için bir değer belirtin (veya atlayın) hello giriş klasöründeki tüm blob'lara ait veriler kopyalanan toohello hedef demektir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-229">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="4e04c-230">Bu öğreticide, hello dosya adı için bir değer belirtin.</span><span class="sxs-lookup"><span data-stu-id="4e04c-230">In this tutorial, you specify a value for hello fileName.</span></span>  

1. <span data-ttu-id="4e04c-231">Adlı bir JSON dosyası oluşturun **Inputdataset.JSON** hello içinde **C:\ADFGetStartedPSH** klasörüyle içeriği aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="4e04c-231">Create a JSON file named **InputDataset.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
                "fileName": "emp.txt",
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

    <span data-ttu-id="4e04c-232">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="4e04c-232">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="4e04c-233">Özellik</span><span class="sxs-lookup"><span data-stu-id="4e04c-233">Property</span></span> | <span data-ttu-id="4e04c-234">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e04c-234">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="4e04c-235">type</span><span class="sxs-lookup"><span data-stu-id="4e04c-235">type</span></span> | <span data-ttu-id="4e04c-236">Merhaba type özelliği çok ayarlamak**AzureBlob** verileri Azure blob depolama alanında bulunduğundan.</span><span class="sxs-lookup"><span data-stu-id="4e04c-236">hello type property is set too**AzureBlob** because data resides in an Azure blob storage.</span></span> |
    | <span data-ttu-id="4e04c-237">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4e04c-237">linkedServiceName</span></span> | <span data-ttu-id="4e04c-238">Toohello başvuruyor **AzureStorageLinkedService** daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-238">Refers toohello **AzureStorageLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="4e04c-239">folderPath</span><span class="sxs-lookup"><span data-stu-id="4e04c-239">folderPath</span></span> | <span data-ttu-id="4e04c-240">Merhaba blob belirtir **kapsayıcı** ve hello **klasörü** giriş BLOB'ları içerir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-240">Specifies hello blob **container** and hello **folder** that contains input blobs.</span></span> <span data-ttu-id="4e04c-241">Bu öğreticide adftutorial hello blob kapsayıcı ve hello kök klasör.</span><span class="sxs-lookup"><span data-stu-id="4e04c-241">In this tutorial, adftutorial is hello blob container and folder is hello root folder.</span></span> | 
    | <span data-ttu-id="4e04c-242">fileName</span><span class="sxs-lookup"><span data-stu-id="4e04c-242">fileName</span></span> | <span data-ttu-id="4e04c-243">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="4e04c-243">This property is optional.</span></span> <span data-ttu-id="4e04c-244">Bu özelliği atarsanız, tüm dosyaları hello folderPath çekilir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-244">If you omit this property, all files from hello folderPath are picked.</span></span> <span data-ttu-id="4e04c-245">Bu öğreticide **emp.txt** hello fileName, böylece yalnızca bu dosyanın işleme için kayıt için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-245">In this tutorial, **emp.txt** is specified for hello fileName, so only that file is picked up for processing.</span></span> |
    | <span data-ttu-id="4e04c-246">format -> type</span><span class="sxs-lookup"><span data-stu-id="4e04c-246">format -> type</span></span> |<span data-ttu-id="4e04c-247">Merhaba giriş dosyası kullanırız hello metin biçiminde olduğundan **TextFormat**.</span><span class="sxs-lookup"><span data-stu-id="4e04c-247">hello input file is in hello text format, so we use **TextFormat**.</span></span> |
    | <span data-ttu-id="4e04c-248">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="4e04c-248">columnDelimiter</span></span> | <span data-ttu-id="4e04c-249">Merhaba giriş dosyası Hello sütunlarında tarafından ayrılmış **virgül karakteriyle (`,`)**.</span><span class="sxs-lookup"><span data-stu-id="4e04c-249">hello columns in hello input file are delimited by **comma character (`,`)**.</span></span> |
    | <span data-ttu-id="4e04c-250">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="4e04c-250">frequency/interval</span></span> | <span data-ttu-id="4e04c-251">Merhaba sıklığını çok ayarlamak**saat** ve aralığı çok ayarlamak**1**, o hello yani dilimler kullanılabilir giriş **saatlik**.</span><span class="sxs-lookup"><span data-stu-id="4e04c-251">hello frequency is set too**Hour** and interval is  set too**1**, which means that hello input slices are available **hourly**.</span></span> <span data-ttu-id="4e04c-252">Hello Data Factory hizmeti için giriş verileri saatte hello kök klasöründe blob kapsayıcısının diğer bir deyişle, görünüyor (**adftutorial**), belirtilen.</span><span class="sxs-lookup"><span data-stu-id="4e04c-252">In other words, hello Data Factory service looks for input data every hour in hello root folder of blob container (**adftutorial**) you specified.</span></span> <span data-ttu-id="4e04c-253">Merhaba veri hello ardışık düzen başlangıç ve bitiş zamanları, değil önce veya sonra bu kez içinde arar.</span><span class="sxs-lookup"><span data-stu-id="4e04c-253">It looks for hello data within hello pipeline start and end times, not before or after these times.</span></span>  |
    | <span data-ttu-id="4e04c-254">external</span><span class="sxs-lookup"><span data-stu-id="4e04c-254">external</span></span> | <span data-ttu-id="4e04c-255">Bu özellik çok ayarlanır**true** hello verileri bu ardışık düzen tarafından oluşturulmamış olması durumunda.</span><span class="sxs-lookup"><span data-stu-id="4e04c-255">This property is set too**true** if hello data is not generated by this pipeline.</span></span> <span data-ttu-id="4e04c-256">Bu öğreticide girdi verileri Hello Biz bu özellik tootrue ayarlamak için bu ardışık düzen tarafından oluşturulmayan hello emp.txt, dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="4e04c-256">hello input data in this tutorial is in hello emp.txt file, which is not generated by this pipeline, so we set this property tootrue.</span></span> |

    <span data-ttu-id="4e04c-257">Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4e04c-257">For more information about these JSON properties, see [Azure Blob connector article](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="4e04c-258">Komut toocreate hello Data Factory veri kümesi aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-258">Run hello following command toocreate hello Data Factory dataset.</span></span>

    ```PowerShell  
    New-AzureRmDataFactoryDataset $df -File .\InputDataset.json
    ```
    <span data-ttu-id="4e04c-259">Merhaba örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4e04c-259">Here is hello sample output:</span></span>

    ```
    DatasetName       : InputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureBlobDataset
    Policy            : Microsoft.Azure.Management.DataFactories.Common.Models.Policy
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

### <a name="create-an-output-dataset"></a><span data-ttu-id="4e04c-260">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e04c-260">Create an output dataset</span></span>
<span data-ttu-id="4e04c-261">Adlı bir çıktı veri kümesi oluşturma hello adımın bu bölümünde **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="4e04c-261">In this part of hello step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="4e04c-262">Bu veri kümesi tarafından temsil edilen hello Azure SQL veritabanındaki tooa SQL tablosunu işaret **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="4e04c-262">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span> 

1. <span data-ttu-id="4e04c-263">Adlı bir JSON dosyası oluşturun **OutputDataset.json** hello içinde **C:\ADFGetStartedPSH** içeriği aşağıdaki hello klasörüyle:</span><span class="sxs-lookup"><span data-stu-id="4e04c-263">Create a JSON file named **OutputDataset.json** in hello **C:\ADFGetStartedPSH** folder with hello following content:</span></span>

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

    <span data-ttu-id="4e04c-264">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="4e04c-264">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

    | <span data-ttu-id="4e04c-265">Özellik</span><span class="sxs-lookup"><span data-stu-id="4e04c-265">Property</span></span> | <span data-ttu-id="4e04c-266">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e04c-266">Description</span></span> |
    |:--- |:--- |
    | <span data-ttu-id="4e04c-267">type</span><span class="sxs-lookup"><span data-stu-id="4e04c-267">type</span></span> | <span data-ttu-id="4e04c-268">Merhaba type özelliği çok ayarlamak**AzureSqlTable** verileri bir Azure SQL veritabanı tablosunda kopyalanan tooa olduğundan.</span><span class="sxs-lookup"><span data-stu-id="4e04c-268">hello type property is set too**AzureSqlTable** because data is copied tooa table in an Azure SQL database.</span></span> |
    | <span data-ttu-id="4e04c-269">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="4e04c-269">linkedServiceName</span></span> | <span data-ttu-id="4e04c-270">Toohello başvuruyor **AzureSqlLinkedService** daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-270">Refers toohello **AzureSqlLinkedService** that you created earlier.</span></span> |
    | <span data-ttu-id="4e04c-271">tableName</span><span class="sxs-lookup"><span data-stu-id="4e04c-271">tableName</span></span> | <span data-ttu-id="4e04c-272">Belirtilen hello **tablo** toowhich hello veri kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="4e04c-272">Specified hello **table** toowhich hello data is copied.</span></span> | 
    | <span data-ttu-id="4e04c-273">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="4e04c-273">frequency/interval</span></span> | <span data-ttu-id="4e04c-274">Merhaba sıklığı çok ayarlı**saat** ve aralığı **1**, hello çıkış dilimler üretilir anlamına gelir **saatlik** hello ardışık düzen başlangıç ve bitiş zamanları, önce değil arasında veya Bu kez sonra.</span><span class="sxs-lookup"><span data-stu-id="4e04c-274">hello frequency is set too**Hour** and interval is **1**, which means that hello output slices are produced **hourly** between hello pipeline start and end times, not before or after these times.</span></span>  |

    <span data-ttu-id="4e04c-275">Üç sütun – **kimliği**, **FirstName**, ve **LastName** – hello veritabanındaki emp tablosunda hello.</span><span class="sxs-lookup"><span data-stu-id="4e04c-275">There are three columns – **ID**, **FirstName**, and **LastName** – in hello emp table in hello database.</span></span> <span data-ttu-id="4e04c-276">Kimliktir bir kimlik sütunu yalnızca toospecify gereken şekilde **FirstName** ve **LastName** burada.</span><span class="sxs-lookup"><span data-stu-id="4e04c-276">ID is an identity column, so you need toospecify only **FirstName** and **LastName** here.</span></span>

    <span data-ttu-id="4e04c-277">Bu JSON özellikleri hakkında daha fazla bilgi için bkz. [Azure SQL bağlayıcısı makalesi](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4e04c-277">For more information about these JSON properties, see [Azure SQL connector article](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
2. <span data-ttu-id="4e04c-278">Çalışma hello aşağıdaki toocreate hello data factory veri kümesi komutu.</span><span class="sxs-lookup"><span data-stu-id="4e04c-278">Run hello following command toocreate hello data factory dataset.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryDataset $df -File .\OutputDataset.json
    ```

    <span data-ttu-id="4e04c-279">Merhaba örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4e04c-279">Here is hello sample output:</span></span>

    ```
    DatasetName       : OutputDataset
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Availability      : Microsoft.Azure.Management.DataFactories.Common.Models.Availability
    Location          : Microsoft.Azure.Management.DataFactories.Models.AzureSqlTableDataset
    Policy            :
    Structure         : {FirstName, LastName}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DatasetProperties
    ProvisioningState : Succeeded
    ```

## <a name="create-a-pipeline"></a><span data-ttu-id="4e04c-280">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e04c-280">Create a pipeline</span></span>
<span data-ttu-id="4e04c-281">Bu adımda, girdi olarak **InputDataset** ve çıktı olarak **OutputDataset** kullanan **kopyalama etkinliğine** sahip bir işlem hattı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-281">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

<span data-ttu-id="4e04c-282">Şu anda, hangi sürücü zamanlama hello çıktı veri kümesi değil.</span><span class="sxs-lookup"><span data-stu-id="4e04c-282">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="4e04c-283">Bu öğreticide, çıktı veri kümesi yapılandırılmış tooproduce bir dilim saate birdir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-283">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="4e04c-284">bir başlangıç saati ve bir 24 saat olan günü birbirinden, bitiş zamanı Hello ardışık düzen vardır.</span><span class="sxs-lookup"><span data-stu-id="4e04c-284">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="4e04c-285">Bu nedenle, çıktı veri kümesinin 24 dilim hello ardışık düzen tarafından oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4e04c-285">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span> 


1. <span data-ttu-id="4e04c-286">Adlı bir JSON dosyası oluşturun **C:\adfgetstartedpsh** hello içinde **C:\ADFGetStartedPSH** klasörüyle içeriği aşağıdaki hello:</span><span class="sxs-lookup"><span data-stu-id="4e04c-286">Create a JSON file named **ADFTutorialPipeline.json** in hello **C:\ADFGetStartedPSH** folder, with hello following content:</span></span>

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
    <span data-ttu-id="4e04c-287">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="4e04c-287">Note hello following points:</span></span>
   
    - <span data-ttu-id="4e04c-288">Merhaba etkinlikler bölümünde, yalnızca bir etkinlik olduğundan, **türü** çok ayarlanır**kopya**.</span><span class="sxs-lookup"><span data-stu-id="4e04c-288">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="4e04c-289">Merhaba kopyalama etkinliği hakkında daha fazla bilgi için bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="4e04c-289">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="4e04c-290">Data Factory çözümlerinde, [veri dönüştürme etkinliklerini](data-factory-data-transformation-activities.md) de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-290">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="4e04c-291">Merhaba etkinlik çok kümesi için giriş**InputDataset** ve hello etkinlik çok kümesi için çıkış**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="4e04c-291">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="4e04c-292">Merhaba, **typeProperties** bölümünde **BlobSource** hello kaynak türü olarak belirtilir ve **SqlSink** hello Havuz türü olarak belirtilir.</span><span class="sxs-lookup"><span data-stu-id="4e04c-292">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="4e04c-293">Kaynakları ve havuzlarını olarak hello kopyalama etkinliği tarafından desteklenen veri depoları tam bir listesi için bkz: [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="4e04c-293">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="4e04c-294">nasıl toouse belirli bir desteklenen veri depolayan bir kaynak/havuz toolearn hello tablosundaki hello bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-294">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
     
    <span data-ttu-id="4e04c-295">Merhaba Hello değerini değiştirin **Başlat** hello geçerli gün özelliğiyle ve **son** hello sonraki gün değeri.</span><span class="sxs-lookup"><span data-stu-id="4e04c-295">Replace hello value of hello **start** property with hello current day and **end** value with hello next day.</span></span> <span data-ttu-id="4e04c-296">Yalnızca hello tarih bölümünü belirtip tarih saat hello hello saat bölümünü atlayın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-296">You can specify only hello date part and skip hello time part of hello date time.</span></span> <span data-ttu-id="4e04c-297">Örneğin, "2016-02-çok eşdeğeri olan 03", "2016-02-03T00:00:00Z"</span><span class="sxs-lookup"><span data-stu-id="4e04c-297">For example, "2016-02-03", which is equivalent too"2016-02-03T00:00:00Z"</span></span>
     
    <span data-ttu-id="4e04c-298">Başlangıç ve bitiş tarih saatleri [ISO biçiminde](http://en.wikipedia.org/wiki/ISO_8601) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4e04c-298">Both start and end datetimes must be in [ISO format](http://en.wikipedia.org/wiki/ISO_8601).</span></span> <span data-ttu-id="4e04c-299">Örneğin: 2016-10-14T16:32:41Z.</span><span class="sxs-lookup"><span data-stu-id="4e04c-299">For example: 2016-10-14T16:32:41Z.</span></span> <span data-ttu-id="4e04c-300">Merhaba **son** saati isteğe bağlıdır ancak biz Bu öğreticide kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-300">hello **end** time is optional, but we use it in this tutorial.</span></span> 
     
    <span data-ttu-id="4e04c-301">Hello için değer belirtmezseniz, **son** özelliği olarak hesaplanır "**start + 48 saat**".</span><span class="sxs-lookup"><span data-stu-id="4e04c-301">If you do not specify value for hello **end** property, it is calculated as "**start + 48 hours**".</span></span> <span data-ttu-id="4e04c-302">toorun hello ardışık kalıcı olarak belirtmek **9999-09-09** hello hello değeri olarak **son** özelliği.</span><span class="sxs-lookup"><span data-stu-id="4e04c-302">toorun hello pipeline indefinitely, specify **9999-09-09** as hello value for hello **end** property.</span></span>
     
    <span data-ttu-id="4e04c-303">Örnek önceki hello vardır 24 veri dilimi her veri dilimi saatlik oluşturulduğundan.</span><span class="sxs-lookup"><span data-stu-id="4e04c-303">In hello preceding example, there are 24 data slices as each data slice is produced hourly.</span></span>

    <span data-ttu-id="4e04c-304">İşlem hattı tanımındaki JSON özelliklerinin açıklamaları için [işlem hatları oluşturma](data-factory-create-pipelines.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-304">For descriptions of JSON properties in a pipeline definition, see [create pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4e04c-305">Kopyalama etkinliği tanımındaki JSON özelliklerinin açıklamaları için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="4e04c-305">For descriptions of JSON properties in a copy activity definition, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="4e04c-306">BlobSource tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure Blob bağlayıcısı makalesi](data-factory-azure-blob-connector.md).</span><span class="sxs-lookup"><span data-stu-id="4e04c-306">For descriptions of JSON properties supported by BlobSource, see [Azure Blob connector article](data-factory-azure-blob-connector.md).</span></span> <span data-ttu-id="4e04c-307">SqlSink tarafından desteklenen JSON özelliklerinin açıklamaları için bkz. [Azure SQL Veritabanı bağlayıcısı makalesi](data-factory-azure-sql-connector.md).</span><span class="sxs-lookup"><span data-stu-id="4e04c-307">For descriptions of JSON properties supported by SqlSink, see [Azure SQL Database connector article](data-factory-azure-sql-connector.md).</span></span>
2. <span data-ttu-id="4e04c-308">Aşağıdaki komut toocreate hello veri fabrikası tablonun hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-308">Run hello following command toocreate hello data factory table.</span></span>

    ```PowerShell   
    New-AzureRmDataFactoryPipeline $df -File .\ADFTutorialPipeline.json
    ```

    <span data-ttu-id="4e04c-309">Merhaba örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4e04c-309">Here is hello sample output:</span></span> 

    ```
    PipelineName      : ADFTutorialPipeline
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    Properties        : Microsoft.Azure.Management.DataFactories.Models.PipelinePropertie
    ProvisioningState : Succeeded
    ```

<span data-ttu-id="4e04c-310">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="4e04c-310">**Congratulations!**</span></span> <span data-ttu-id="4e04c-311">Bir Azure data factory, ardışık düzen toocopy verilerle bir Azure blob depolama tooan Azure SQL veritabanı başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="4e04c-311">You have successfully created an Azure data factory with a pipeline toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

## <a name="monitor-hello-pipeline"></a><span data-ttu-id="4e04c-312">Merhaba işlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="4e04c-312">Monitor hello pipeline</span></span>
<span data-ttu-id="4e04c-313">Bu adımda, bir Azure data factory'de neler olduğunu Azure PowerShell toomonitor kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-313">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="4e04c-314">Değiştir &lt;DataFactoryName&gt; veri fabrikası ve Çalıştır hello adıyla **Get-AzureRmDataFactory**ve değişken $df hello çıktı tooa atayın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-314">Replace &lt;DataFactoryName&gt; with hello name of your data factory and run **Get-AzureRmDataFactory**, and assign hello output tooa variable $df.</span></span>

    ```PowerShell  
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name <DataFactoryName>
    ```

    <span data-ttu-id="4e04c-315">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="4e04c-315">For example:</span></span>
    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name ADFTutorialDataFactoryPSH0516
    ```
    
    <span data-ttu-id="4e04c-316">Ardından, çıktı aşağıdaki $df toosee hello yazdırma hello içeriğini çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="4e04c-316">Then, run print hello contents of $df toosee hello following output:</span></span> 
    
    ```
    PS C:\ADFGetStartedPSH> $df
    
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DataFactoryId     : 6f194b34-03b3-49ab-8f03-9f8a7b9d3e30
    ResourceGroupName : ADFTutorialResourceGroup
    Location          : West US
    Tags              : {}
    Properties        : Microsoft.Azure.Management.DataFactories.Models.DataFactoryProperties
    ProvisioningState : Succeeded
    ```
2. <span data-ttu-id="4e04c-317">Çalıştırma **Get-AzureRmDataFactorySlice** hello tüm dilimleri hakkında bilgi tooget **OutputDataset**, hello çıktı veri kümesi hello ardışık olduğu.</span><span class="sxs-lookup"><span data-stu-id="4e04c-317">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **OutputDataset**, which is hello output dataset of hello pipeline.</span></span>  

    ```PowerShell   
    Get-AzureRmDataFactorySlice $df -DatasetName OutputDataset -StartDateTime 2017-05-11T00:00:00Z
    ```

   <span data-ttu-id="4e04c-318">Bu ayar hello eşleşmelidir **Başlat** hello ardışık düzen JSON değeri.</span><span class="sxs-lookup"><span data-stu-id="4e04c-318">This setting should match hello **Start** value in hello pipeline JSON.</span></span> <span data-ttu-id="4e04c-319">24 dilim görmeniz gerekir ertesi gün 00: 00 hello geçerli gün too12, her saat için bir tane 'M Merhaba.</span><span class="sxs-lookup"><span data-stu-id="4e04c-319">You should see 24 slices, one for each hour from 12 AM of hello current day too12 AM of hello next day.</span></span>

   <span data-ttu-id="4e04c-320">Üç örnek dilimler hello çıktısından şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4e04c-320">Here are three sample slices from hello output:</span></span> 

    ``` 
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 11:00:00 PM
    End               : 5/12/2017 12:00:00 AM
    RetryCount        : 0
    State             : Ready
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 9:00:00 PM
    End               : 5/11/2017 10:00:00 PM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0   

    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : ADFTutorialDataFactoryPSH0516
    DatasetName       : OutputDataset
    Start             : 5/11/2017 8:00:00 PM
    End               : 5/11/2017 9:00:00 PM
    RetryCount        : 0
    State             : Waiting
    SubState          : ConcurrencyLimit
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="4e04c-321">Çalıştırma **Get-AzureRmDataFactoryRun** tooget hello etkinliğinin ayrıntılarını çalıştıran bir **belirli** dilim.</span><span class="sxs-lookup"><span data-stu-id="4e04c-321">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a **specific** slice.</span></span> <span data-ttu-id="4e04c-322">Merhaba tarih-saat değeri hello önceki komutu toospecify hello hello StartDateTime parametresinin değeri hello çıktısını kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-322">Copy hello date-time value from hello output of hello previous command toospecify hello value for hello StartDateTime parameter.</span></span> 

    ```PowerShell  
    Get-AzureRmDataFactoryRun $df -DatasetName OutputDataset -StartDateTime "5/11/2017 09:00:00 PM"
    ```

   <span data-ttu-id="4e04c-323">Merhaba örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4e04c-323">Here is hello sample output:</span></span> 

    ```
    Id                  : c0ddbd75-d0c7-4816-a775-704bbd7c7eab_636301332000000000_636301368000000000_OutputDataset
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : ADFTutorialDataFactoryPSH0516
    DatasetName         : OutputDataset
    ProcessingStartTime : 5/16/2017 8:00:33 PM
    ProcessingEndTime   : 5/16/2017 8:01:36 PM
    PercentComplete     : 100
    DataSliceStart      : 5/11/2017 9:00:00 PM
    DataSliceEnd        : 5/11/2017 10:00:00 PM
    Status              : Succeeded
    Timestamp           : 5/16/2017 8:00:33 PM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : CopyFromBlobToSQL
    PipelineName        : ADFTutorialPipeline
    Type                : Copy  
    ```

<span data-ttu-id="4e04c-324">Data Factory cmdlet’leri hakkında kapsamlı bilgi için bkz. [Data Factory Cmdlet Başvurusu](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="4e04c-324">For comprehensive documentation on Data Factory cmdlets, see [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories).</span></span>

## <a name="summary"></a><span data-ttu-id="4e04c-325">Özet</span><span class="sxs-lookup"><span data-stu-id="4e04c-325">Summary</span></span>
<span data-ttu-id="4e04c-326">Bu öğreticide, bir Azure veri fabrikası toocopy verileri Azure blob tooan Azure SQL veritabanından oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="4e04c-326">In this tutorial, you created an Azure data factory toocopy data from an Azure blob tooan Azure SQL database.</span></span> <span data-ttu-id="4e04c-327">PowerShell toocreate hello veri fabrikası, bağlı hizmetler, veri kümeleri ve işlem hattı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="4e04c-327">You used PowerShell toocreate hello data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="4e04c-328">Bu öğreticide gerçekleştirilen hello üst düzey adımlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4e04c-328">Here are hello high-level steps you performed in this tutorial:</span></span>  

1. <span data-ttu-id="4e04c-329">Oluşturulan Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="4e04c-329">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="4e04c-330">**Bağlı hizmetler** oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="4e04c-330">Created **linked services**:</span></span>

   <span data-ttu-id="4e04c-331">a.</span><span class="sxs-lookup"><span data-stu-id="4e04c-331">a.</span></span> <span data-ttu-id="4e04c-332">Bir **Azure Storage** hizmet toolink girdi verilerini tutan Azure depolama hesabınıza bağlı.</span><span class="sxs-lookup"><span data-stu-id="4e04c-332">An **Azure Storage** linked service toolink your Azure storage account that holds input data.</span></span>     
   <span data-ttu-id="4e04c-333">b.</span><span class="sxs-lookup"><span data-stu-id="4e04c-333">b.</span></span> <span data-ttu-id="4e04c-334">Bir **Azure SQL** hizmet toolink hello çıktı verilerini tutan SQL veritabanınız bağlı.</span><span class="sxs-lookup"><span data-stu-id="4e04c-334">An **Azure SQL** linked service toolink your SQL database that holds hello output data.</span></span>
3. <span data-ttu-id="4e04c-335">İşlem hatları için girdi verilerini ve çıktı verilerini açıklayan oluşturulan **veri kümeleri**.</span><span class="sxs-lookup"><span data-stu-id="4e04c-335">Created **datasets** that describe input data and output data for pipelines.</span></span>
4. <span data-ttu-id="4e04c-336">Oluşturulan bir **ardışık düzen** ile **kopyalama etkinliği**, ile **BlobSource** hello kaynağı olarak ve **SqlSink** hello havuz olarak.</span><span class="sxs-lookup"><span data-stu-id="4e04c-336">Created a **pipeline** with **Copy Activity**, with **BlobSource** as hello source and **SqlSink** as hello sink.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e04c-337">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4e04c-337">Next steps</span></span>
<span data-ttu-id="4e04c-338">Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız.</span><span class="sxs-lookup"><span data-stu-id="4e04c-338">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="4e04c-339">Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4e04c-339">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="4e04c-340">nasıl bir veri öğesine/öğesinden toocopy veri deposu hakkında toolearn hello veri deposu hello tablosundaki hello bağlantısını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="4e04c-340">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span> 

