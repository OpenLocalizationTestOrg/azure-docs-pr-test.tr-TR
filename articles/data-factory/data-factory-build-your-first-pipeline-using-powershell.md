---
title: "İlk data factory’nizi derleme (PowerShell) | Microsoft Belgeleri"
description: "Bu öğreticide Azure PowerShell kullanarak örnek bir Azure Data Factory işlem hattı oluşturursunuz."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 22ec1236-ea86-4eb7-b903-0e79a58b90c7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 40a63339be90d0c5d972605c7f6fa029ca1e2ba4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="db91b-103">Öğretici: Azure PowerShell kullanarak ilk Azure data factory’nizi derleme</span><span class="sxs-lookup"><span data-stu-id="db91b-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="db91b-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="db91b-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="db91b-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="db91b-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="db91b-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="db91b-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="db91b-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="db91b-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="db91b-108">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="db91b-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="db91b-109">REST API</span><span class="sxs-lookup"><span data-stu-id="db91b-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="db91b-110">Bu makalede, ilk Azure data factory’nizi oluşturmak için Azure PowerShell kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="db91b-110">In this article, you use Azure PowerShell to create your first Azure data factory.</span></span> <span data-ttu-id="db91b-111">Diğer araçları/SDK’ları kullanarak öğreticiyi uygulamak için açılır listedeki seçeneklerden birini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="db91b-111">To do the tutorial using other tools/SDKs, select one of the options from the drop-down list.</span></span>

<span data-ttu-id="db91b-112">Bu öğreticideki işlem hattı bir etkinlik içerir: **HDInsight Hive etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="db91b-112">The pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="db91b-113">Bu etkinlik, Azure HDInsight kümesi üzerinde çıkış verileri üretmek üzere giriş verilerini dönüştüren bir hive betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="db91b-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data to produce output data.</span></span> <span data-ttu-id="db91b-114">İşlem hattı, belirtilen başlangıç ve bitiş saatleri arasında ayda bir kez çalışacak şekilde zamanlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="db91b-114">The pipeline is scheduled to run once a month between the specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="db91b-115">Bu öğreticideki veri işlem hattı, çıkış verileri üretmek üzere giriş verilerini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="db91b-115">The data pipeline in this tutorial transforms input data to produce output data.</span></span> <span data-ttu-id="db91b-116">Bir kaynak veri deposundan hedef veri deposuna verileri kopyalamaz.</span><span class="sxs-lookup"><span data-stu-id="db91b-116">It does not copy data from a source data store to a destination data store.</span></span> <span data-ttu-id="db91b-117">Azure Data Factory kullanarak verileri kopyalama öğreticisi için bkz. [Öğretici: Blob Depolama’dan SQL Veritabanı’na veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="db91b-117">For a tutorial on how to copy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage to SQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="db91b-118">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="db91b-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="db91b-119">Bir etkinliğin çıkış veri kümesini diğer etkinliğin giriş veri kümesi olarak ayarlayarak iki etkinliği zincirleyebilir, yani bir etkinliğin diğerinden sonra çalıştırılmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db91b-119">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="db91b-120">Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="db91b-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="db91b-121">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="db91b-121">Prerequisites</span></span>
* <span data-ttu-id="db91b-122">[Öğreticiye Genel Bakış](data-factory-build-your-first-pipeline.md) makalesinin tamamını okuyun ve **ön koşul** adımlarını tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="db91b-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="db91b-123">Bilgisayarınıza Azure PowerShell’in en son sürümünü yüklemek için [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azure/overview) makalesindeki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="db91b-123">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="db91b-124">(isteğe bağlı) Bu makalede, tüm Data Factory cmdlet'lerini kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="db91b-124">(optional) This article does not cover all the Data Factory cmdlets.</span></span> <span data-ttu-id="db91b-125">Data Factory cmdlet’leri hakkında kapsamlı bilgi için bkz. [Data Factory Cmdlet Başvurusu](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="db91b-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="db91b-126">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="db91b-126">Create data factory</span></span>
<span data-ttu-id="db91b-127">Bu adımda **FirstDataFactoryPSH** adlı bir Azure Data Factory oluşturmak için Azure PowerShell’i kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="db91b-127">In this step, you use Azure PowerShell to create an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="db91b-128">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="db91b-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="db91b-129">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="db91b-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="db91b-130">Örneğin, bir kaynaktan hedef veri deposuna veri kopyalama amaçlı bir Kopyalama Etkinliği ve giriş verilerini dönüştürmek üzere Hive betiği çalıştırma amaçlı bir HDInsight Hive etkinliği.</span><span class="sxs-lookup"><span data-stu-id="db91b-130">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data.</span></span> <span data-ttu-id="db91b-131">Bu adımda data factory oluşturmayla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="db91b-131">Let's start with creating the data factory in this step.</span></span>

1. <span data-ttu-id="db91b-132">Azure PowerShell’i başlatın ve aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="db91b-132">Start Azure PowerShell and run the following command.</span></span> <span data-ttu-id="db91b-133">Bu öğreticide sonuna kadar Azure PowerShell’i açık tutun.</span><span class="sxs-lookup"><span data-stu-id="db91b-133">Keep Azure PowerShell open until the end of this tutorial.</span></span> <span data-ttu-id="db91b-134">Kapatıp yeniden açarsanız, bu komutları yeniden çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="db91b-134">If you close and reopen, you need to run these commands again.</span></span>
   * <span data-ttu-id="db91b-135">Aşağıdaki komutu çalıştırın ve Azure portalda oturum açmak için kullandığınız kullanıcı adı ve parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="db91b-135">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="db91b-136">Bu hesapla ilgili tüm abonelikleri görmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="db91b-136">Run the following command to view all the subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="db91b-137">Çalışmak isteğiniz aboneliği seçmek için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="db91b-137">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="db91b-138">Bu abonelik Azure portalında kullanılanla aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="db91b-138">This subscription should be the same as the one you used in the Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="db91b-139">Aşağıdaki komutu kullanarak **ADFTutorialResourceGroup** adlı bir Azure kaynak grubu oluşturun:</span><span class="sxs-lookup"><span data-stu-id="db91b-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="db91b-140">Bu öğreticideki adımlardan bazıları ADFTutorialResourceGroup adlı kaynak grubunu kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="db91b-140">Some of the steps in this tutorial assume that you use the resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="db91b-141">Farklı bir kaynak grubu kullanıyorsanız, bu öğreticide ADFTutorialResourceGroup yerine onu kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="db91b-141">If you use a different resource group, you need to use it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="db91b-142">**FirstDataFactoryPSH** adında bir data factory oluşturan **New-AzureRmDataFactory** cmdlet’ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="db91b-142">Run the **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="db91b-143">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="db91b-143">Note the following points:</span></span>

* <span data-ttu-id="db91b-144">Azure Data Factory adı küresel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="db91b-144">The name of the Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="db91b-145">Şu hatayı alırsanız: **“FirstDataFactoryPSH” veri fabrikası adı yok**, adı değiştirin (örneğin, yournameFirstDataFactoryPSH).</span><span class="sxs-lookup"><span data-stu-id="db91b-145">If you receive the error **Data factory name “FirstDataFactoryPSH” is not available**, change the name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="db91b-146">Bu öğreticide adımları uygularken ADFTutorialFactoryPSH yerine bu adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="db91b-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="db91b-147">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="db91b-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="db91b-148">Data Factory örnekleri oluşturmak için, Azure aboneliğinde katılımcı/yönetici rolünüz olmalıdır</span><span class="sxs-lookup"><span data-stu-id="db91b-148">To create Data Factory instances, you need to be a contributor/administrator of the Azure subscription</span></span>
* <span data-ttu-id="db91b-149">Data factory adı gelecekte bir DNS adı olarak kaydedilmiş olabilir; bu nedenle herkese görünür hale gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="db91b-149">The name of the data factory may be registered as a DNS name in the future and hence become publically visible.</span></span>
* <span data-ttu-id="db91b-150">Şu hatayı alırsanız: "**Abonelik, Microsoft.DataFactory ad alanını kullanacak şekilde kaydedilmemiş**", aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:</span><span class="sxs-lookup"><span data-stu-id="db91b-150">If you receive the error: "**This subscription is not registered to use namespace Microsoft.DataFactory**", do one of the following and try publishing again:</span></span>

  * <span data-ttu-id="db91b-151">Azure PowerShell’de Data Factory sağlayıcısını kaydetmek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="db91b-151">In Azure PowerShell, run the following command to register the Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="db91b-152">Data Factory sağlayıcısının kayıtlı olduğunu onaylamak için aşağıdaki komutu çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="db91b-152">You can run the following command to confirm that the Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="db91b-153">Azure aboneliğini kullanarak [Azure portalında](https://portal.azure.com) oturum açın ve Data Factory dikey penceresine gidin (ya da) Azure portalında bir data factory oluşturun.</span><span class="sxs-lookup"><span data-stu-id="db91b-153">Login using the Azure subscription into the [Azure portal](https://portal.azure.com) and navigate to a Data Factory blade (or) create a data factory in the Azure portal.</span></span> <span data-ttu-id="db91b-154">Bu eylem sağlayıcıyı sizin için otomatik olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="db91b-154">This action automatically registers the provider for you.</span></span>

<span data-ttu-id="db91b-155">İşlem hattı oluşturmadan önce, öncelikle birkaç Data Factory varlığı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="db91b-155">Before creating a pipeline, you need to create a few Data Factory entities first.</span></span> <span data-ttu-id="db91b-156">Önce veri depolarını/işlemleri veri deponuza bağlamak için bağlı hizmetler oluşturun, bağlı veri depolarında giriş/çıkış verilerini temsil etmek üzere giriş ve çıkış veri kümeleri tanımlayın, sonra da bu veri kümelerini kullanan bir etkinlikle işlem hattını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="db91b-156">You first create linked services to link data stores/computes to your data store, define input and output datasets to represent input/output data in linked data stores, and then create the pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="db91b-157">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="db91b-157">Create linked services</span></span>
<span data-ttu-id="db91b-158">Bu adımda, Azure Depolama hesabınızı ve isteğe bağlı Azure HDInsight kümesini data factory’nize bağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="db91b-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster to your data factory.</span></span> <span data-ttu-id="db91b-159">Azure Depolama hesabı, bu örnekteki işlem hattı için girdi ve çıktı verilerini tutar.</span><span class="sxs-lookup"><span data-stu-id="db91b-159">The Azure Storage account holds the input and output data for the pipeline in this sample.</span></span> <span data-ttu-id="db91b-160">HDInsight bağlı hizmeti, bu örnekteki işlem hattının etkinliğinde belirtilen Hive betiğini çalıştırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="db91b-160">The HDInsight linked service is used to run a Hive script specified in the activity of the pipeline in this sample.</span></span> <span data-ttu-id="db91b-161">Senaryonuzda hangi veri deposu/işlem hizmetlerinin kullanılacağını belirleyin ve bağlı hizmetler oluşturarak bu hizmetleri data factory’ye bağlayın.</span><span class="sxs-lookup"><span data-stu-id="db91b-161">Identify what data store/compute services are used in your scenario and link those services to the data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="db91b-162">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="db91b-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="db91b-163">Bu adımda, Azure Depolama hesabınızı veri fabrikanıza bağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="db91b-163">In this step, you link your Azure Storage account to your data factory.</span></span> <span data-ttu-id="db91b-164">Giriş/çıkış verilerini ve HQL betik dosyasını depolamak için aynı Azure Depolama hesabını kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="db91b-164">You use the same Azure Storage account to store input/output data and the HQL script file.</span></span>

1. <span data-ttu-id="db91b-165">C:\ADFGetStarted klasöründe aşağıdaki içeriğe sahip StorageLinkedService.json adlı bir JSON dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="db91b-165">Create a JSON file named StorageLinkedService.json in the C:\ADFGetStarted folder with the following content.</span></span> <span data-ttu-id="db91b-166">Henüz yoksa ADFGetStarted klasörünü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="db91b-166">Create the folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="db91b-167">**accountname** sözcüğünü Azure depolama hesabınızın adıyla, **accountkey** sözcüğünü de Azure depolama hesabının erişim anahtarıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="db91b-167">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="db91b-168">Depolama erişim anahtarınızı nasıl alabileceğinizi öğrenmek için [Depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account) sayfasındaki depolama erişim anahtarlarını görüntüleme, kopyalama ve yeniden oluşturma bilgilerine bakın.</span><span class="sxs-lookup"><span data-stu-id="db91b-168">To learn how to get your storage access key, see the information about how to view, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="db91b-169">Azure PowerShell’de ADFGetStarted klasörüne geçin.</span><span class="sxs-lookup"><span data-stu-id="db91b-169">In Azure PowerShell, switch to the ADFGetStarted folder.</span></span>
3. <span data-ttu-id="db91b-170">Bağlı bir hizmet oluşturan **New-AzureRmDataFactoryLinkedService** cmdlet’ini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db91b-170">You can use the **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="db91b-171">Bu öğreticide kullandığınız bu cmdlet ve diğer Data Factory cmdlet’lerini *ResourceGroupName* ve *DataFactoryName* parametreleri için değerleri geçirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="db91b-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you to pass values for the *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="db91b-172">Alternatif olarak, **DataFactory** nesnesini almak ve cmdlet’i her çalıştırdığınızda *ResourceGroupName* ve *DataFactoryName* yazmadan nesneyi geçirmek için **Get-AzureRmDataFactory** kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db91b-172">Alternatively, you can use **Get-AzureRmDataFactory** to get a **DataFactory** object and pass the object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="db91b-173">**Get-AzureRmDataFactory** cmdlet’inin çıktısını **$df** değişkenine atamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="db91b-173">Run the following command to assign the output of the **Get-AzureRmDataFactory** cmdlet to a **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="db91b-174">Şimdi de, **StorageLinkedService** bağlı hizmetini oluşturan **New-AzureRmDataFactoryLinkedService** cmdlet’ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="db91b-174">Now, run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="db91b-175">**Get-AzureRmDataFactory** cmdlet’ini çalıştırmadıysanız ve çıktıyı **$df** değişkenine atamadıysanız, *ResourceGroupName* ve *DataFactoryName* parametreleri için değerleri aşağıdaki gibi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="db91b-175">If you hadn't run the **Get-AzureRmDataFactory** cmdlet and assigned the output to the **$df** variable, you would have to specify values for the *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="db91b-176">Öğreticinin ortasında Azure PowerShell’i kapatırsanız, öğreticiyi tamamlamak için Azure PowerShell’i sonraki başlatışınızda **Get-AzureRmDataFactory** cmdlet’ini çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="db91b-176">If you close Azure PowerShell in the middle of the tutorial, you have to run the **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell to complete the tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="db91b-177">Azure HDInsight bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="db91b-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="db91b-178">Bu adımda, isteğe bağlı HDInsight kümesini data factory’nize bağlarsınız.</span><span class="sxs-lookup"><span data-stu-id="db91b-178">In this step, you link an on-demand HDInsight cluster to your data factory.</span></span> <span data-ttu-id="db91b-179">HDInsight kümesi çalışma zamanında otomatik olarak oluşturulur ve işlenmesi bittiğinde ve belirtilen sürede boşta kalırsa silinir.</span><span class="sxs-lookup"><span data-stu-id="db91b-179">The HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for the specified amount of time.</span></span> <span data-ttu-id="db91b-180">İsteğe bağlı HDInsight kümesi yerine kendi HDInsight kümenizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db91b-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="db91b-181">Ayrıntılar için bkz. [İşlem Bağlı Hizmetleri](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="db91b-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="db91b-182">**C:\ADFGetStarted** klasöründe aşağıdaki içeriğe sahip **HDInsightOnDemandLinkedService**.json adlı bir JSON dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="db91b-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in the **C:\ADFGetStarted** folder with the following content.</span></span>

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
                "linkedServiceName": "StorageLinkedService"
            }
        }
    }
    ```
    <span data-ttu-id="db91b-183">Aşağıdaki tabloda, kod parçacığında kullanılan JSON özellikleri için açıklamalar verilmektedir:</span><span class="sxs-lookup"><span data-stu-id="db91b-183">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="db91b-184">Özellik</span><span class="sxs-lookup"><span data-stu-id="db91b-184">Property</span></span> | <span data-ttu-id="db91b-185">Açıklama</span><span class="sxs-lookup"><span data-stu-id="db91b-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="db91b-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="db91b-186">ClusterSize</span></span> |<span data-ttu-id="db91b-187">HDInsight kümesi boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="db91b-187">Specifies the size of the HDInsight cluster.</span></span> |
   | <span data-ttu-id="db91b-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="db91b-188">TimeToLive</span></span> |<span data-ttu-id="db91b-189">Silinmeden önce HDInsight kümesinin boşta kalma süresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="db91b-189">Specifies that the idle time for the HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="db91b-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="db91b-190">linkedServiceName</span></span> |<span data-ttu-id="db91b-191">HDInsight tarafından oluşturulan günlükleri depolamak için kullanılan depolama hesabını belirtir.</span><span class="sxs-lookup"><span data-stu-id="db91b-191">Specifies the storage account that is used to store the logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="db91b-192">Aşağıdaki noktalara dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="db91b-192">Note the following points:</span></span>

   * <span data-ttu-id="db91b-193">Data Factory, sizin için JSON ile **Linux tabanlı** bir HDInsight kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="db91b-193">The Data Factory creates a **Linux-based** HDInsight cluster for you with the JSON.</span></span> <span data-ttu-id="db91b-194">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="db91b-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="db91b-195">İsteğe bağlı HDInsight kümesi yerine **kendi HDInsight kümenizi** kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db91b-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="db91b-196">Ayrıntılar için bkz. [HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="db91b-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="db91b-197">HDInsight kümesi JSON’da belirttiğiniz blob depolamada (**linkedServiceName**) bir **varsayılan kapsayıcı** oluşturur.</span><span class="sxs-lookup"><span data-stu-id="db91b-197">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="db91b-198">HDInsight, küme silindiğinde bu kapsayıcıyı silmez.</span><span class="sxs-lookup"><span data-stu-id="db91b-198">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="db91b-199">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="db91b-199">This behavior is by design.</span></span> <span data-ttu-id="db91b-200">İsteğe bağlı HDInsight bağlı hizmeti kullanıldığında, mevcut canlı bir küme olmadığı sürece bir dilim her işlendiğinde bir HDInsight kümesi oluşturulur (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="db91b-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="db91b-201">Küme, işlem tamamlandığında otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="db91b-201">The cluster is automatically deleted when the processing is done.</span></span>

       <span data-ttu-id="db91b-202">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="db91b-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="db91b-203">İşlerin sorunları giderilmesi için bunlara gerek yoksa, depolama maliyetini azaltmak için bunları silmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db91b-203">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="db91b-204">Bu kapsayıcıların adları şu deseni izler: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="db91b-204">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="db91b-205">Azure blob depolamada kapsayıcı silmek için [Microsoft Storage Gezgini](http://storageexplorer.com/) gibi araçları kullanın.</span><span class="sxs-lookup"><span data-stu-id="db91b-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="db91b-206">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="db91b-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="db91b-207">HDInsightOnDemandLinkedService adlı bağlı hizmeti oluşturan **New-AzureRmDataFactoryLinkedService** cmdlet’ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="db91b-207">Run the **New-AzureRmDataFactoryLinkedService** cmdlet that creates the linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="db91b-208">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="db91b-208">Create datasets</span></span>
<span data-ttu-id="db91b-209">Bu adımda, Hive işlenmesi için girdi ve çıktı verilerini temsil edecek veri kümeleri oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="db91b-209">In this step, you create datasets to represent the input and output data for Hive processing.</span></span> <span data-ttu-id="db91b-210">Bu veri kümeleri, bu öğreticide daha önce oluşturduğunuz **StorageLinkedService** öğesine başvurur.</span><span class="sxs-lookup"><span data-stu-id="db91b-210">These datasets refer to the **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="db91b-211">Bağlı hizmet Azure Storage hesabını belirtirken, veri kümeleri de girdi ve çıktı verilerini tutan depolama biriminde kapsayıcı, klasör, dosya adı belirtir.</span><span class="sxs-lookup"><span data-stu-id="db91b-211">The linked service points to an Azure Storage account and datasets specify container, folder, file name in the storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="db91b-212">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="db91b-212">Create input dataset</span></span>
1. <span data-ttu-id="db91b-213">**C:\ADFGetStarted** klasöründe aşağıdaki içeriğe sahip **InputTable.json** adlı bir JSON dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="db91b-213">Create a JSON file named **InputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span></span>

    ```json
    {
        "name": "AzureBlobInput",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="db91b-214">Bu JSON, işlem hattındaki bir etkinliğin girdi verilerini temsil eden **AzureBlobInput** adlı veri kümesini tanımlamaktadır.</span><span class="sxs-lookup"><span data-stu-id="db91b-214">The JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in the pipeline.</span></span> <span data-ttu-id="db91b-215">Ek olarak, girdi verilerinin **adfgetstarted** adlı blob kapsayıcısında ve **inputdata** adlı klasörde bulunduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="db91b-215">In addition, it specifies that the input data is located in the blob container called **adfgetstarted** and the folder called **inputdata**.</span></span>

    <span data-ttu-id="db91b-216">Aşağıdaki tabloda, kod parçacığında kullanılan JSON özellikleri için açıklamalar verilmektedir:</span><span class="sxs-lookup"><span data-stu-id="db91b-216">The following table provides descriptions for the JSON properties used in the snippet:</span></span>

   | <span data-ttu-id="db91b-217">Özellik</span><span class="sxs-lookup"><span data-stu-id="db91b-217">Property</span></span> | <span data-ttu-id="db91b-218">Açıklama</span><span class="sxs-lookup"><span data-stu-id="db91b-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="db91b-219">type</span><span class="sxs-lookup"><span data-stu-id="db91b-219">type</span></span> |<span data-ttu-id="db91b-220">Veriler Azure blob depolamada yer aldığından type özelliği AzureBlob olarak ayarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="db91b-220">The type property is set to AzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="db91b-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="db91b-221">linkedServiceName</span></span> |<span data-ttu-id="db91b-222">daha önce oluşturduğunuz StorageLinkedService’e başvurur.</span><span class="sxs-lookup"><span data-stu-id="db91b-222">refers to the StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="db91b-223">fileName</span><span class="sxs-lookup"><span data-stu-id="db91b-223">fileName</span></span> |<span data-ttu-id="db91b-224">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="db91b-224">This property is optional.</span></span> <span data-ttu-id="db91b-225">Bu özelliği atarsanız, tüm folderPath dosyaları alınır.</span><span class="sxs-lookup"><span data-stu-id="db91b-225">If you omit this property, all the files from the folderPath are picked.</span></span> <span data-ttu-id="db91b-226">Bu durumda, yalnızca input.log işlenir.</span><span class="sxs-lookup"><span data-stu-id="db91b-226">In this case, only the input.log is processed.</span></span> |
   | <span data-ttu-id="db91b-227">type</span><span class="sxs-lookup"><span data-stu-id="db91b-227">type</span></span> |<span data-ttu-id="db91b-228">Günlük dosyaları metin biçiminde olduğundan TextFormat kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="db91b-228">The log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="db91b-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="db91b-229">columnDelimiter</span></span> |<span data-ttu-id="db91b-230">Günlük dosyalarındaki sütunlar virgül (,) ile ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="db91b-230">columns in the log files are delimited by the comma character (,).</span></span> |
   | <span data-ttu-id="db91b-231">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="db91b-231">frequency/interval</span></span> |<span data-ttu-id="db91b-232">frequency Ay, interval de 1 olarak ayarlanmıştır; girdi dilimlerinin aylık olarak kullanılabileceğini belirtir.</span><span class="sxs-lookup"><span data-stu-id="db91b-232">frequency set to Month and interval is 1, which means that the input slices are available monthly.</span></span> |
   | <span data-ttu-id="db91b-233">external</span><span class="sxs-lookup"><span data-stu-id="db91b-233">external</span></span> |<span data-ttu-id="db91b-234">bu özellik, girdi verileri Data Factory hizmetiyle oluşturulmadıysa true olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="db91b-234">this property is set to true if the input data is not generated by the Data Factory service.</span></span> |
2. <span data-ttu-id="db91b-235">Data Factory veri kümesi oluşturmak için Azure PowerShell’de şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="db91b-235">Run the following command in Azure PowerShell to create the Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="db91b-236">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="db91b-236">Create output dataset</span></span>
<span data-ttu-id="db91b-237">Şimdi, Azure Blob depolamada depolanan çıktı verilerini göstermek için çıktı veri kümesi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="db91b-237">Now, you create the output dataset to represent the output data stored in the Azure Blob storage.</span></span>

1. <span data-ttu-id="db91b-238">**C:\ADFGetStarted** klasöründe aşağıdaki içeriğe sahip **OutputTable.json** adlı bir JSON dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="db91b-238">Create a JSON file named **OutputTable.json** in the **C:\ADFGetStarted** folder with the following content:</span></span>

    ```json
    {
      "name": "AzureBlobOutput",
      "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
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
    <span data-ttu-id="db91b-239">Bu JSON, işlem hattındaki bir etkinliğin çıktı verilerini temsil eden **AzureBlobOutput** adlı veri kümesini tanımlamaktadır.</span><span class="sxs-lookup"><span data-stu-id="db91b-239">The JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in the pipeline.</span></span> <span data-ttu-id="db91b-240">Ek olarak, sonuçların **adfgetstarted** adlı blob kapsayıcısında ve **partitioneddata** adlı klasörde depolandığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="db91b-240">In addition, it specifies that the results are stored in the blob container called **adfgetstarted** and the folder called **partitioneddata**.</span></span> <span data-ttu-id="db91b-241">Burada, **availability** bölümü çıktı veri kümesinin aylık tabanda oluşturulduğunu belirtiyor.</span><span class="sxs-lookup"><span data-stu-id="db91b-241">The **availability** section specifies that the output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="db91b-242">Data Factory veri kümesi oluşturmak için Azure PowerShell’de şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="db91b-242">Run the following command in Azure PowerShell to create the Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="db91b-243">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="db91b-243">Create pipeline</span></span>
<span data-ttu-id="db91b-244">Bu adımda, **HDInsightHive** etkinliğiyle ilk işlem hattınızı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="db91b-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="db91b-245">Girdi diliminin ayda bir (frequency: Month, interval: 1) kullanılabilir, çıktı dilimi ayda bir oluşturulur ve etkinlik zamanlayıcı özelliği de ayda bir olacak şekilde ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="db91b-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and the scheduler property for the activity is also set to monthly.</span></span> <span data-ttu-id="db91b-246">Çıktı veri kümesi ve etkinlik zamanlayıcı ayarlarının eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="db91b-246">The settings for the output dataset and the activity scheduler must match.</span></span> <span data-ttu-id="db91b-247">Şu anda, çıktı veri kümesi zamanlamayı yönetendir; bu nedenle etkinlik hiçbir çıktı oluşturmasa bile sizin bir çıktı veri kümesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="db91b-247">Currently, output dataset is what drives the schedule, so you must create an output dataset even if the activity does not produce any output.</span></span> <span data-ttu-id="db91b-248">Etkinlik herhangi bir girdi almazsa, girdi veri kümesi oluşturma işlemini atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db91b-248">If the activity doesn't take any input, you can skip creating the input dataset.</span></span> <span data-ttu-id="db91b-249">Aşağıdaki JSON’da kullanılan özellikler bu bölümün sonunda anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="db91b-249">The properties used in the following JSON are explained at the end of this section.</span></span>

1. <span data-ttu-id="db91b-250">C:\ADFGetStarted klasöründe aşağıdaki içeriğe sahip MyFirstPipelinePSH.json adlı bir JSON dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="db91b-250">Create a JSON file named MyFirstPipelinePSH.json in the C:\ADFGetStarted folder with the following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="db91b-251">**storageaccountname**’i JSON’daki depolama adınızla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="db91b-251">Replace **storageaccountname** with the name of your storage account in the JSON.</span></span>
   >
   >

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
                        "scriptLinkedService": "StorageLinkedService",
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
    <span data-ttu-id="db91b-252">JSON parçacığında, HDInsight kümesinde Veri işleyecek Hive’ı kullanan etkinlikten oluşmuş bir işlem hattı oluşturuyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="db91b-252">In the JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive to process Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="db91b-253">**partitionweblogs.hql** Hive betik dosyası Azure depolama hesabında (scriptLinkedService tarafından belirtilen **StorageLinkedService** adıyla) ve **adfgetstarted** kapsayıcısındaki **betik** klasöründe depolanır.</span><span class="sxs-lookup"><span data-stu-id="db91b-253">The Hive script file, **partitionweblogs.hql**, is stored in the Azure storage account (specified by the scriptLinkedService, called **StorageLinkedService**), and in **script** folder in the container **adfgetstarted**.</span></span>

    <span data-ttu-id="db91b-254">Burada, **defines** bölümü hive betiğine Hive yapılandırma değerleri olarak (örn., ${hiveconf:inputtable}, ${hiveconf:partitionedtable}) geçirilecek çalışma zamanı ayarlarını belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="db91b-254">The **defines** section is used to specify the runtime settings that be passed to the hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="db91b-255">İşlem hattının **start** ve **end** özellikleri işlem hattının etkin dönemini belirtir.</span><span class="sxs-lookup"><span data-stu-id="db91b-255">The **start** and **end** properties of the pipeline specifies the active period of the pipeline.</span></span>

    <span data-ttu-id="db91b-256">JSON etkinliğinde, Hive betiğinin **linkedServiceName** – **HDInsightOnDemandLinkedService** tarafından belirtilen işlemde çalışacağını belirtirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db91b-256">In the activity JSON, you specify that the Hive script runs on the compute specified by the **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="db91b-257">Örnekte kullanılan JSON özellikleri hakkında ayrıntılı bilgi için [Azure Data Factory'deki işlem hatları ve etkinlikler](data-factory-create-pipelines.md) sayfasındaki "JSON İşlem Hatları" bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="db91b-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in the example.</span></span>

2. <span data-ttu-id="db91b-258">Azure blob depolamada **adfgetstarted/inputdata** klasöründeki **input.log** dosyasını gördüğünüzü doğrulayın ve işlem hattına dağıtmak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="db91b-258">Confirm that you see the **input.log** file in the **adfgetstarted/inputdata** folder in the Azure blob storage, and run the following command to deploy the pipeline.</span></span> <span data-ttu-id="db91b-259">**start** ve **end** zamanları geçmişe ayarlanmış ve **isPaused** yanlış olarak ayarlanmış olduğundan işlem hattı (işlem hattında etkinlik) dağıtıldıktan hemen sonra çalışır.</span><span class="sxs-lookup"><span data-stu-id="db91b-259">Since the **start** and **end** times are set in the past and **isPaused** is set to false, the pipeline (activity in the pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="db91b-260">Tebrikler, Azure PowerShell kullanarak ilk işlem hattınızı başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="db91b-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="db91b-261">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="db91b-261">Monitor pipeline</span></span>
<span data-ttu-id="db91b-262">Bu adımda, Azure data factory’de neler olduğunu izlemek için Azure PowerShell kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="db91b-262">In this step, you use Azure PowerShell to monitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="db91b-263">**Get-AzureRmDataFactory** komutunu çalıştırın ve çıktıyı **$df** değişkenine atayın.</span><span class="sxs-lookup"><span data-stu-id="db91b-263">Run **Get-AzureRmDataFactory** and assign the output to a **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="db91b-264">İşlem hattının çıktı tablosu olan **EmpSQLTable** tablosunun tüm dilimleri hakkında bilgi almak için **Get-AzureRmDataFactorySlice** komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="db91b-264">Run **Get-AzureRmDataFactorySlice** to get details about all slices of the **EmpSQLTable**, which is the output table of the pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="db91b-265">Burada belirttiğiniz StartDateTime ile JSON işlem hattında belirtilen başlangıç zamanıyla aynı olmasına özen gösterin.</span><span class="sxs-lookup"><span data-stu-id="db91b-265">Notice that the StartDateTime you specify here is the same start time specified in the pipeline JSON.</span></span> <span data-ttu-id="db91b-266">Örnek çıktı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="db91b-266">Here is the sample output:</span></span>

    ```PowerShell
    ResourceGroupName : ADFTutorialResourceGroup
    DataFactoryName   : FirstDataFactoryPSH
    DatasetName       : AzureBlobOutput
    Start             : 7/1/2017 12:00:00 AM
    End               : 7/2/2017 12:00:00 AM
    RetryCount        : 0
    State             : InProgress
    SubState          :
    LatencyStatus     :
    LongRetryCount    : 0
    ```
3. <span data-ttu-id="db91b-267">Belirli bir dilimle ilgili etkinlik çalıştırmalarının ayrıntılarını almak için **Get-AzureRmDataFactoryRun** komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="db91b-267">Run **Get-AzureRmDataFactoryRun** to get the details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="db91b-268">Örnek çıktı aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="db91b-268">Here is the sample output:</span></span> 

    ```PowerShell
    Id                  : 0f6334f2-d56c-4d48-b427-d4f0fb4ef883_635268096000000000_635292288000000000_AzureBlobOutput
    ResourceGroupName   : ADFTutorialResourceGroup
    DataFactoryName     : FirstDataFactoryPSH
    DatasetName         : AzureBlobOutput
    ProcessingStartTime : 12/18/2015 4:50:33 AM
    ProcessingEndTime   : 12/31/9999 11:59:59 PM
    PercentComplete     : 0
    DataSliceStart      : 7/1/2017 12:00:00 AM
    DataSliceEnd        : 7/2/2017 12:00:00 AM
    Status              : AllocatingResources
    Timestamp           : 12/18/2015 4:50:33 AM
    RetryAttempt        : 0
    Properties          : {}
    ErrorMessage        :
    ActivityName        : RunSampleHiveActivity
    PipelineName        : MyFirstPipeline
    Type                : Script
    ```
    <span data-ttu-id="db91b-269">Dilimi **Hazır** durumunda veya **Başarısız** durumunda görene kadar bu cmdlet’i çalışır halde tutun.</span><span class="sxs-lookup"><span data-stu-id="db91b-269">You can keep running this cmdlet until you see the slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="db91b-270">Dilim Hazır durumunda olduğunda, çıktı verileri için blob depolamanızın **adfgetstarted** klasöründe **partitioneddata** klasörünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="db91b-270">When the slice is in Ready state, check the **partitioneddata** folder in the **adfgetstarted** container in your blob storage for the output data.</span></span>  <span data-ttu-id="db91b-271">İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır.</span><span class="sxs-lookup"><span data-stu-id="db91b-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![çıktı verileri](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="db91b-273">İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika).</span><span class="sxs-lookup"><span data-stu-id="db91b-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="db91b-274">Bu nedenle, işlem hattının dilimi işlemesi için **yaklaşık 30 dakika** bekleyin.</span><span class="sxs-lookup"><span data-stu-id="db91b-274">Therefore, expect the pipeline to take **approximately 30 minutes** to process the slice.</span></span>
>
> <span data-ttu-id="db91b-275">Dilim başarıyla işlendiğinde girdi dosyası silinir.</span><span class="sxs-lookup"><span data-stu-id="db91b-275">The input file gets deleted when the slice is processed successfully.</span></span> <span data-ttu-id="db91b-276">Bu nedenle, dilimi yeniden çalıştırmak veya öğreticiyi yeniden uygulamak isterseniz girdi dosyasını (input.log) adfgetstarted kapsayıcısının inputdata klasörüne yükleyin.</span><span class="sxs-lookup"><span data-stu-id="db91b-276">Therefore, if you want to rerun the slice or do the tutorial again, upload the input file (input.log) to the inputdata folder of the adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="db91b-277">Özet</span><span class="sxs-lookup"><span data-stu-id="db91b-277">Summary</span></span>
<span data-ttu-id="db91b-278">Bu öğreticide, HDInsight hadoop kümesindeki Hive betiği çalıştırılarak verileri işlemek için bir Azure data factory oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="db91b-278">In this tutorial, you created an Azure data factory to process data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="db91b-279">Aşağıdaki adımları uygulamak için Azure Portal’da Data Factory Düzenleyici’yi kullandınız:</span><span class="sxs-lookup"><span data-stu-id="db91b-279">You used the Data Factory Editor in the Azure portal to do the following steps:</span></span>

1. <span data-ttu-id="db91b-280">Oluşturulan Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="db91b-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="db91b-281">Oluşturulan iki **bağlı hizmet**:</span><span class="sxs-lookup"><span data-stu-id="db91b-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="db91b-282">Girdi/çıktı dosyalarını tutan Azure blob depolamanızı data factory’ye bağlamak için **Azure Storage** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="db91b-282">**Azure Storage** linked service to link your Azure blob storage that holds input/output files to the data factory.</span></span>
   2. <span data-ttu-id="db91b-283">İsteğe bağlı HDInsight Hadoop kümesini data factory’ye bağlamak için isteğe bağlı **Azure HDInsight** bağlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="db91b-283">**Azure HDInsight** on-demand linked service to link an on-demand HDInsight Hadoop cluster to the data factory.</span></span> <span data-ttu-id="db91b-284">Azure Data Factory, girdi verilerini işlemek, çıktı verilerini de oluşturmak için tam zamanında HDInsight Hadoop kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="db91b-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time to process input data and produce output data.</span></span>
3. <span data-ttu-id="db91b-285">İşlem hattındaki HDInsight Hive etkinliğiyle ilgili girdi ve çıktı verilerini açıklayan oluşturulan iki **veri kümesi**.</span><span class="sxs-lookup"><span data-stu-id="db91b-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in the pipeline.</span></span>
4. <span data-ttu-id="db91b-286">**HDInsight Hive** etkinliğine sahip oluşturulan bir **işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="db91b-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db91b-287">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db91b-287">Next steps</span></span>
<span data-ttu-id="db91b-288">Bu makalede, isteğe bağlı Azure HDInsight kümesinde bir Hive betiği çalıştıran dönüştürme etkinliğine (HDInsight Etkinliği) sahip işlem hattı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="db91b-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="db91b-289">Verileri Azure Blob’tan Azure SQL’e kopyalamak için Kopyalama Etkinliği’nin kullanılması hakkında bilgi için bkz. [Öğretici: Verileri Azure Blob’dan Azure SQL’e kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="db91b-289">To see how to use a Copy Activity to copy data from an Azure Blob to Azure SQL, see [Tutorial: Copy data from an Azure Blob to Azure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="db91b-290">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="db91b-290">See Also</span></span>
| <span data-ttu-id="db91b-291">Konu</span><span class="sxs-lookup"><span data-stu-id="db91b-291">Topic</span></span> | <span data-ttu-id="db91b-292">Açıklama</span><span class="sxs-lookup"><span data-stu-id="db91b-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="db91b-293">Data Factory Cmdlet Başvurusu</span><span class="sxs-lookup"><span data-stu-id="db91b-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="db91b-294">Data Factory cmdlet'leri hakkında kapsamlı belgelere bakma</span><span class="sxs-lookup"><span data-stu-id="db91b-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="db91b-295">İşlem hatları</span><span class="sxs-lookup"><span data-stu-id="db91b-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="db91b-296">Bu makale, Azure Data Factory’de işlem hatlarının ve etkinliklerini anlamanıza ve senaryonuz ya da işletmeniz için uçtan uca veri odaklı iş akışları oluşturmak amacıyla bunları nasıl kullanacağınızı anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="db91b-296">This article helps you understand pipelines and activities in Azure Data Factory and how to use them to construct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="db91b-297">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="db91b-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="db91b-298">Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="db91b-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="db91b-299">Zamanlama ve Yürütme</span><span class="sxs-lookup"><span data-stu-id="db91b-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="db91b-300">Bu makalede Azure Data Factory uygulama modelinin zamanlama ve yürütme yönleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="db91b-300">This article explains the scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="db91b-301">İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="db91b-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="db91b-302">Bu makalede İzleme ve Yönetim Uygulaması kullanılarak işlem hatlarını izleme, yönetme ve hatalarını ayıklama işlemleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="db91b-302">This article describes how to monitor, manage, and debug pipelines using the Monitoring & Management App.</span></span> |
