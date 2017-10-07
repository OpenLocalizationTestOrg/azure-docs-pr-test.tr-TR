---
title: aaaBuild ilk data factory'nizi (PowerShell) | Microsoft Docs
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
ms.openlocfilehash: 626260798b56d590577b3c4b24f7cf52873c9f80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-build-your-first-azure-data-factory-using-azure-powershell"></a><span data-ttu-id="1ca29-103">Öğretici: Azure PowerShell kullanarak ilk Azure data factory’nizi derleme</span><span class="sxs-lookup"><span data-stu-id="1ca29-103">Tutorial: Build your first Azure data factory using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ca29-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1ca29-104">Overview and prerequisites</span></span>](data-factory-build-your-first-pipeline.md)
> * [<span data-ttu-id="1ca29-105">Azure portal</span><span class="sxs-lookup"><span data-stu-id="1ca29-105">Azure portal</span></span>](data-factory-build-your-first-pipeline-using-editor.md)
> * [<span data-ttu-id="1ca29-106">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1ca29-106">Visual Studio</span></span>](data-factory-build-your-first-pipeline-using-vs.md)
> * [<span data-ttu-id="1ca29-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ca29-107">PowerShell</span></span>](data-factory-build-your-first-pipeline-using-powershell.md)
> * [<span data-ttu-id="1ca29-108">Resource Manager Şablonu</span><span class="sxs-lookup"><span data-stu-id="1ca29-108">Resource Manager Template</span></span>](data-factory-build-your-first-pipeline-using-arm.md)
> * [<span data-ttu-id="1ca29-109">REST API</span><span class="sxs-lookup"><span data-stu-id="1ca29-109">REST API</span></span>](data-factory-build-your-first-pipeline-using-rest-api.md)
>
>

<span data-ttu-id="1ca29-110">Bu makalede, ilk Azure data factory'nizi Azure PowerShell toocreate kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ca29-110">In this article, you use Azure PowerShell toocreate your first Azure data factory.</span></span> <span data-ttu-id="1ca29-111">diğer araçlar/SDK, kullanarak toodo hello öğretici seçin hello seçeneklerden birini hello aşağı açılan listeden.</span><span class="sxs-lookup"><span data-stu-id="1ca29-111">toodo hello tutorial using other tools/SDKs, select one of hello options from hello drop-down list.</span></span>

<span data-ttu-id="1ca29-112">Bu öğreticide Hello ardışık bir etkinlik vardır: **Hdınsight Hive etkinliği**.</span><span class="sxs-lookup"><span data-stu-id="1ca29-112">hello pipeline in this tutorial has one activity: **HDInsight Hive activity**.</span></span> <span data-ttu-id="1ca29-113">Bu etkinlik dönüşümler veri tooproduce çıkış veri girişi bir Azure Hdınsight kümesinde bir hive betiği çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="1ca29-113">This activity runs a hive script on an Azure HDInsight cluster that transforms input data tooproduce output data.</span></span> <span data-ttu-id="1ca29-114">Başlangıç ve bitiş zamanlarını hello arasında bir ay belirtilen sonra hello ardışık düzen zamanlanmış toorun ' dir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-114">hello pipeline is scheduled toorun once a month between hello specified start and end times.</span></span> 

> [!NOTE]
> <span data-ttu-id="1ca29-115">Bu öğreticide Hello veri ardışık giriş verisi tooproduce çıktı verilerini dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="1ca29-115">hello data pipeline in this tutorial transforms input data tooproduce output data.</span></span> <span data-ttu-id="1ca29-116">Bir kaynak veri deposu tooa hedef veri deposundan veri kopyalamaz.</span><span class="sxs-lookup"><span data-stu-id="1ca29-116">It does not copy data from a source data store tooa destination data store.</span></span> <span data-ttu-id="1ca29-117">Nasıl bir öğretici için Azure Data Factory kullanarak toocopy verileri görmek [Öğreticisi: Blob Storage tooSQL veritabanı ' veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1ca29-117">For a tutorial on how toocopy data using Azure Data Factory, see [Tutorial: Copy data from Blob Storage tooSQL Database](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
> 
> <span data-ttu-id="1ca29-118">Bir işlem hattında birden fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-118">A pipeline can have more than one activity.</span></span> <span data-ttu-id="1ca29-119">Ve hello çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-119">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="1ca29-120">Daha fazla bilgi için bkz. [Data Factory'de zamanlama ve yürütme](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="1ca29-120">For more information, see [scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ca29-121">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1ca29-121">Prerequisites</span></span>
* <span data-ttu-id="1ca29-122">Okuyun [öğreticiye genel bakış](data-factory-build-your-first-pipeline.md) makale ve tam hello **önkoşul** adımları.</span><span class="sxs-lookup"><span data-stu-id="1ca29-122">Read through [Tutorial Overview](data-factory-build-your-first-pipeline.md) article and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="1ca29-123">' Ndaki yönergeleri izleyin [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) makale tooinstall en son sürümü Azure PowerShell, bilgisayarınızda.</span><span class="sxs-lookup"><span data-stu-id="1ca29-123">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall latest version of Azure PowerShell on your computer.</span></span>
* <span data-ttu-id="1ca29-124">(isteğe bağlı) Bu makalede, tüm hello Data Factory cmdlet'lerini kapsamaz.</span><span class="sxs-lookup"><span data-stu-id="1ca29-124">(optional) This article does not cover all hello Data Factory cmdlets.</span></span> <span data-ttu-id="1ca29-125">Data Factory cmdlet’leri hakkında kapsamlı bilgi için bkz. [Data Factory Cmdlet Başvurusu](/powershell/module/azurerm.datafactories).</span><span class="sxs-lookup"><span data-stu-id="1ca29-125">See [Data Factory Cmdlet Reference](/powershell/module/azurerm.datafactories) for comprehensive documentation on Data Factory cmdlets.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="1ca29-126">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca29-126">Create data factory</span></span>
<span data-ttu-id="1ca29-127">Bu adımda, Azure PowerShell toocreate adlı bir Azure Data Factory kullandığınız **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="1ca29-127">In this step, you use Azure PowerShell toocreate an Azure Data Factory named **FirstDataFactoryPSH**.</span></span> <span data-ttu-id="1ca29-128">Bir veri fabrikasında bir veya daha fazla işlem hattı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-128">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="1ca29-129">İşlem hattında bir veya daha fazla etkinlik olabilir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-129">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="1ca29-130">Örneğin, bir kopyalama etkinliği toocopy verilerinden bir kaynak tooa hedef veri deposu ve Hdınsight Hive etkinliği toorun bir Hive betiği tootransform verileri girin.</span><span class="sxs-lookup"><span data-stu-id="1ca29-130">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data.</span></span> <span data-ttu-id="1ca29-131">Bu adımda hello data factory oluşturmayla başlayalım.</span><span class="sxs-lookup"><span data-stu-id="1ca29-131">Let's start with creating hello data factory in this step.</span></span>

1. <span data-ttu-id="1ca29-132">Azure PowerShell'i başlatın ve hello aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1ca29-132">Start Azure PowerShell and run hello following command.</span></span> <span data-ttu-id="1ca29-133">Bu öğreticide hello sonuna kadar Azure PowerShell'i açık tutun.</span><span class="sxs-lookup"><span data-stu-id="1ca29-133">Keep Azure PowerShell open until hello end of this tutorial.</span></span> <span data-ttu-id="1ca29-134">Kapatıp yeniden açın, toorun bu komutları yeniden gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-134">If you close and reopen, you need toorun these commands again.</span></span>
   * <span data-ttu-id="1ca29-135">Merhaba aşağıdaki komutu çalıştırın ve hello kullanıcı adı ve parola toosign toohello Azure portal kullanın girin.</span><span class="sxs-lookup"><span data-stu-id="1ca29-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>
    ```PowerShell
    Login-AzureRmAccount
    ```    
   * <span data-ttu-id="1ca29-136">Bu hesap için tüm hello abonelikleri komutu tooview aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1ca29-136">Run hello following command tooview all hello subscriptions for this account.</span></span>
    ```PowerShell
    Get-AzureRmSubscription 
    ```
   * <span data-ttu-id="1ca29-137">Çalışma hello aşağıdaki toowork ile istediğiniz tooselect hello abonelik komutu.</span><span class="sxs-lookup"><span data-stu-id="1ca29-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="1ca29-138">Bu abonelik olması hello hello Azure portalında kullanılanla hello gibi aynı.</span><span class="sxs-lookup"><span data-stu-id="1ca29-138">This subscription should be hello same as hello one you used in hello Azure portal.</span></span>
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <SUBSCRIPTION NAME> | Set-AzureRmContext
    ```     
2. <span data-ttu-id="1ca29-139">Adlı bir Azure kaynak grubu oluşturma **ADFTutorialResourceGroup** hello aşağıdaki komutu çalıştırarak:</span><span class="sxs-lookup"><span data-stu-id="1ca29-139">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command:</span></span>
    
    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
    <span data-ttu-id="1ca29-140">Merhaba bu öğreticideki adımlardan bazıları ADFTutorialResourceGroup adlı hello kaynak grubunu kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="1ca29-140">Some of hello steps in this tutorial assume that you use hello resource group named ADFTutorialResourceGroup.</span></span> <span data-ttu-id="1ca29-141">Farklı bir kaynak grubu kullanıyorsanız, toouse gerekir, bu öğreticide ADFTutorialResourceGroup yerine.</span><span class="sxs-lookup"><span data-stu-id="1ca29-141">If you use a different resource group, you need toouse it in place of ADFTutorialResourceGroup in this tutorial.</span></span>
3. <span data-ttu-id="1ca29-142">Merhaba çalıştırmak **New-AzureRmDataFactory** adlı bir veri fabrikası oluşturur cmdlet **FirstDataFactoryPSH**.</span><span class="sxs-lookup"><span data-stu-id="1ca29-142">Run hello **New-AzureRmDataFactory** cmdlet that creates a data factory named **FirstDataFactoryPSH**.</span></span>

    ```PowerShell
    New-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH –Location "West US"
    ```
<span data-ttu-id="1ca29-143">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="1ca29-143">Note hello following points:</span></span>

* <span data-ttu-id="1ca29-144">Merhaba hello Azure Data Factory adı küresel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1ca29-144">hello name of hello Azure Data Factory must be globally unique.</span></span> <span data-ttu-id="1ca29-145">Merhaba hata alırsanız **veri fabrikası adı "FirstDataFactoryPSH" kullanılabilir değil**, hello adını (örneğin, yournameFirstDataFactoryPSH) değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1ca29-145">If you receive hello error **Data factory name “FirstDataFactoryPSH” is not available**, change hello name (for example, yournameFirstDataFactoryPSH).</span></span> <span data-ttu-id="1ca29-146">Bu öğreticide adımları uygularken ADFTutorialFactoryPSH yerine bu adı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ca29-146">Use this name in place of ADFTutorialFactoryPSH while performing steps in this tutorial.</span></span> <span data-ttu-id="1ca29-147">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="1ca29-147">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
* <span data-ttu-id="1ca29-148">toocreate Data Factory örnekleri toobe katılımcı/yönetici rolünüz hello Azure aboneliği gerekir</span><span class="sxs-lookup"><span data-stu-id="1ca29-148">toocreate Data Factory instances, you need toobe a contributor/administrator of hello Azure subscription</span></span>
* <span data-ttu-id="1ca29-149">Merhaba veri fabrikasının Hello adı hello gelecekte bir DNS adı olarak kayıtlı ve bu nedenle herkese görünür hale gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-149">hello name of hello data factory may be registered as a DNS name in hello future and hence become publically visible.</span></span>
* <span data-ttu-id="1ca29-150">Merhaba hatayı alırsanız: "**Bu abonelik, Microsoft.DataFactory kayıtlı toouse ad değil**" Merhaba aşağıdakilerden birini yapın ve yeniden yayımlamayı deneyin:</span><span class="sxs-lookup"><span data-stu-id="1ca29-150">If you receive hello error: "**This subscription is not registered toouse namespace Microsoft.DataFactory**", do one of hello following and try publishing again:</span></span>

  * <span data-ttu-id="1ca29-151">Azure PowerShell'de komut tooregister hello Data Factory sağlayıcısının aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1ca29-151">In Azure PowerShell, run hello following command tooregister hello Data Factory provider:</span></span>

    ```PowerShell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
      <span data-ttu-id="1ca29-152">Bu Data Factory sağlayıcısının kayıtlı hello komutu tooconfirm aşağıdaki hello çalıştırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1ca29-152">You can run hello following command tooconfirm that hello Data Factory provider is registered:</span></span>

    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * <span data-ttu-id="1ca29-153">Oturum açma kullanılarak hello hello Azure aboneliğinize [Azure portal](https://portal.azure.com) ve tooa Data Factory dikey penceresine gidin (veya) hello Azure portalında bir data factory oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ca29-153">Login using hello Azure subscription into hello [Azure portal](https://portal.azure.com) and navigate tooa Data Factory blade (or) create a data factory in hello Azure portal.</span></span> <span data-ttu-id="1ca29-154">Bu eylemin hello sağlayıcıyı sizin için otomatik olarak kaydeder.</span><span class="sxs-lookup"><span data-stu-id="1ca29-154">This action automatically registers hello provider for you.</span></span>

<span data-ttu-id="1ca29-155">Bir işlem hattı oluşturmadan önce toocreate birkaç Data Factory varlıklarını önce gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-155">Before creating a pipeline, you need toocreate a few Data Factory entities first.</span></span> <span data-ttu-id="1ca29-156">Bağlı hizmetler toolink veri depolarını/işlemlerini tooyour veri depolamak, giriş tanımlayın ve çıktı veri kümeleri toorepresent girdi/çıktı verilerini bağlı veri depolarında ve ardından bu veri kümeleri kullanan bir etkinlik hello işlem hattı oluşturma ilk oluşturduğunuzda.</span><span class="sxs-lookup"><span data-stu-id="1ca29-156">You first create linked services toolink data stores/computes tooyour data store, define input and output datasets toorepresent input/output data in linked data stores, and then create hello pipeline with an activity that uses these datasets.</span></span>

## <a name="create-linked-services"></a><span data-ttu-id="1ca29-157">Bağlı hizmetler oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca29-157">Create linked services</span></span>
<span data-ttu-id="1ca29-158">Bu adımda, Azure Storage hesabınızı ve bir isteğe bağlı Azure Hdınsight küme tooyour data factory bağlayın.</span><span class="sxs-lookup"><span data-stu-id="1ca29-158">In this step, you link your Azure Storage account and an on-demand Azure HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="1ca29-159">Azure depolama hesabı bu örnekteki hello ardışık düzeni için girdi ve çıktı verilerini ayrı tutma hello hello.</span><span class="sxs-lookup"><span data-stu-id="1ca29-159">hello Azure Storage account holds hello input and output data for hello pipeline in this sample.</span></span> <span data-ttu-id="1ca29-160">Merhaba Hdınsight bağlı hizmeti kullanılan toorun hello ardışık bu örnekteki hello etkinliğinde belirtilen Hive betiği ' dir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-160">hello HDInsight linked service is used toorun a Hive script specified in hello activity of hello pipeline in this sample.</span></span> <span data-ttu-id="1ca29-161">Hangi veri deposu/işlem Hizmetleri senaryonuzda kullanılır ve bağlı hizmetler oluşturarak bu hizmetleri toohello veri fabrikası bağlantı.</span><span class="sxs-lookup"><span data-stu-id="1ca29-161">Identify what data store/compute services are used in your scenario and link those services toohello data factory by creating linked services.</span></span>

### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="1ca29-162">Azure Storage bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca29-162">Create Azure Storage linked service</span></span>
<span data-ttu-id="1ca29-163">Bu adımda, Azure depolama hesabı tooyour veri fabrikanıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="1ca29-163">In this step, you link your Azure Storage account tooyour data factory.</span></span> <span data-ttu-id="1ca29-164">Merhaba kullandığınız aynı Azure Storage hesabı toostore girdi/çıktı verilerin ve HQL hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="1ca29-164">You use hello same Azure Storage account toostore input/output data and hello HQL script file.</span></span>

1. <span data-ttu-id="1ca29-165">İçerik C:\adfgetstartedpsh hello C:\ADFGetStarted klasöründe aşağıdaki hello ile adlı bir JSON dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ca29-165">Create a JSON file named StorageLinkedService.json in hello C:\ADFGetStarted folder with hello following content.</span></span> <span data-ttu-id="1ca29-166">Zaten yoksa ADFGetStarted hello klasörünü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ca29-166">Create hello folder ADFGetStarted if it does not already exist.</span></span>

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
    <span data-ttu-id="1ca29-167">Değiştir **hesap adı** hello Azure depolama hesabınızın adını içeren ve **hesap anahtarı** hello erişim anahtarı hello Azure depolama hesabı olan.</span><span class="sxs-lookup"><span data-stu-id="1ca29-167">Replace **account name** with hello name of your Azure storage account and **account key** with hello access key of hello Azure storage account.</span></span> <span data-ttu-id="1ca29-168">toolearn tooget depolama alanınızın erişim nasıl anahtar, hello bilgi nasıl tooview, kopyalama ve yeniden oluşturma depolama erişim anahtarları içinde hakkında [depolama hesabınızı yönetme](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="1ca29-168">toolearn how tooget your storage access key, see hello information about how tooview, copy, and regenerate storage access keys in [Manage your storage account](../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>
2. <span data-ttu-id="1ca29-169">Azure PowerShell'de toohello ADFGetStarted klasörüne geçin.</span><span class="sxs-lookup"><span data-stu-id="1ca29-169">In Azure PowerShell, switch toohello ADFGetStarted folder.</span></span>
3. <span data-ttu-id="1ca29-170">Merhaba kullanabilirsiniz **New-AzureRmDataFactoryLinkedService** bağlı hizmet oluşturur cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="1ca29-170">You can use hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates a linked service.</span></span> <span data-ttu-id="1ca29-171">Bu cmdlet ve diğer Data Factory cmdlet'leri Bu öğreticide kullandığınız gerektirir toopass değerleri Merhaba *ResourceGroupName* ve *DataFactoryName* parametreleri.</span><span class="sxs-lookup"><span data-stu-id="1ca29-171">This cmdlet and other Data Factory cmdlets you use in this tutorial requires you toopass values for hello *ResourceGroupName* and *DataFactoryName* parameters.</span></span> <span data-ttu-id="1ca29-172">Alternatif olarak, kullanabileceğiniz **Get-AzureRmDataFactory** tooget bir **DataFactory** nesne ve hello nesne yazmadan nesneyi geçirmek *ResourceGroupName* ve  *DataFactoryName* her bir cmdlet'i çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1ca29-172">Alternatively, you can use **Get-AzureRmDataFactory** tooget a **DataFactory** object and pass hello object without typing *ResourceGroupName* and *DataFactoryName* each time you run a cmdlet.</span></span> <span data-ttu-id="1ca29-173">Çalışma hello şu komutu tooassign hello hello çıktısını **Get-AzureRmDataFactory** cmdlet tooa **$df** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="1ca29-173">Run hello following command tooassign hello output of hello **Get-AzureRmDataFactory** cmdlet tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
4. <span data-ttu-id="1ca29-174">Şimdi, hello çalıştırın **New-AzureRmDataFactoryLinkedService** hello oluşturur cmdlet bağlı **StorageLinkedService** hizmet.</span><span class="sxs-lookup"><span data-stu-id="1ca29-174">Now, run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked **StorageLinkedService** service.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="1ca29-175">Merhaba çalıştırırsanız çalıştırmadıysanız **Get-AzureRmDataFactory** cmdlet'i ve atanan hello çıkış toohello **$df** hello toospecify değerlerini olurdu değişken, *ResourceGroupName*ve *DataFactoryName* aşağıdaki gibi parametreleri.</span><span class="sxs-lookup"><span data-stu-id="1ca29-175">If you hadn't run hello **Get-AzureRmDataFactory** cmdlet and assigned hello output toohello **$df** variable, you would have toospecify values for hello *ResourceGroupName* and *DataFactoryName* parameters as follows.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryLinkedService -ResourceGroupName ADFTutorialResourceGroup -DataFactoryName FirstDataFactoryPSH -File .\StorageLinkedService.json
    ```
    <span data-ttu-id="1ca29-176">Başlangıç Öğreticisi hello ortadaki Azure PowerShell'i kapatırsanız, toorun hello sahip **Get-AzureRmDataFactory** cmdlet, Azure PowerShell toocomplete hello öğreticinin sonraki başlatışınızda.</span><span class="sxs-lookup"><span data-stu-id="1ca29-176">If you close Azure PowerShell in hello middle of hello tutorial, you have toorun hello **Get-AzureRmDataFactory** cmdlet next time you start Azure PowerShell toocomplete hello tutorial.</span></span>

### <a name="create-azure-hdinsight-linked-service"></a><span data-ttu-id="1ca29-177">Azure HDInsight bağlı hizmeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca29-177">Create Azure HDInsight linked service</span></span>
<span data-ttu-id="1ca29-178">Bu adımda, bir isteğe bağlı Hdınsight kümesi tooyour data factory bağlayın.</span><span class="sxs-lookup"><span data-stu-id="1ca29-178">In this step, you link an on-demand HDInsight cluster tooyour data factory.</span></span> <span data-ttu-id="1ca29-179">Merhaba Hdınsight küme otomatik olarak çalışma zamanında oluşturulur ve hello belirtilen süre boyunca işlem yapma ve boşta bittikten sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-179">hello HDInsight cluster is automatically created at runtime and deleted after it is done processing and idle for hello specified amount of time.</span></span> <span data-ttu-id="1ca29-180">İsteğe bağlı HDInsight kümesi yerine kendi HDInsight kümenizi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ca29-180">You could use your own HDInsight cluster instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="1ca29-181">Ayrıntılar için bkz. [İşlem Bağlı Hizmetleri](data-factory-compute-linked-services.md).</span><span class="sxs-lookup"><span data-stu-id="1ca29-181">See [Compute Linked Services](data-factory-compute-linked-services.md) for details.</span></span>

1. <span data-ttu-id="1ca29-182">Adlı bir JSON dosyası oluşturun **Hdınsightondemandlinkedservice**hello .json **C:\ADFGetStarted** içeriği aşağıdaki hello klasörüyle.</span><span class="sxs-lookup"><span data-stu-id="1ca29-182">Create a JSON file named **HDInsightOnDemandLinkedService**.json in hello **C:\ADFGetStarted** folder with hello following content.</span></span>

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
    <span data-ttu-id="1ca29-183">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="1ca29-183">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="1ca29-184">Özellik</span><span class="sxs-lookup"><span data-stu-id="1ca29-184">Property</span></span> | <span data-ttu-id="1ca29-185">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1ca29-185">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="1ca29-186">ClusterSize</span><span class="sxs-lookup"><span data-stu-id="1ca29-186">ClusterSize</span></span> |<span data-ttu-id="1ca29-187">Merhaba Hdınsight kümesi Hello boyutunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-187">Specifies hello size of hello HDInsight cluster.</span></span> |
   | <span data-ttu-id="1ca29-188">TimeToLive</span><span class="sxs-lookup"><span data-stu-id="1ca29-188">TimeToLive</span></span> |<span data-ttu-id="1ca29-189">Silinmeden önce hello Hdınsight kümesi, o hello boşta kalma süresini belirtir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-189">Specifies that hello idle time for hello HDInsight cluster, before it is deleted.</span></span> |
   | <span data-ttu-id="1ca29-190">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1ca29-190">linkedServiceName</span></span> |<span data-ttu-id="1ca29-191">Hdınsight tarafından oluşturulan kullanılan toostore hello günlükleri olan hello depolama hesabını belirtir</span><span class="sxs-lookup"><span data-stu-id="1ca29-191">Specifies hello storage account that is used toostore hello logs that are generated by HDInsight</span></span> |

    <span data-ttu-id="1ca29-192">Hello aşağıdaki noktaları göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="1ca29-192">Note hello following points:</span></span>

   * <span data-ttu-id="1ca29-193">Merhaba Data Factory oluşturur bir **Linux tabanlı** hello JSON ile sizin için Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="1ca29-193">hello Data Factory creates a **Linux-based** HDInsight cluster for you with hello JSON.</span></span> <span data-ttu-id="1ca29-194">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="1ca29-194">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
   * <span data-ttu-id="1ca29-195">İsteğe bağlı HDInsight kümesi yerine **kendi HDInsight kümenizi** kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ca29-195">You could use **your own HDInsight cluster** instead of using an on-demand HDInsight cluster.</span></span> <span data-ttu-id="1ca29-196">Ayrıntılar için bkz. [HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-linked-service).</span><span class="sxs-lookup"><span data-stu-id="1ca29-196">See [HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-linked-service) for details.</span></span>
   * <span data-ttu-id="1ca29-197">Merhaba Hdınsight kümesi oluşturur bir **varsayılan kapsayıcı** hello JSON belirtilen hello blob depolamada (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="1ca29-197">hello HDInsight cluster creates a **default container** in hello blob storage you specified in hello JSON (**linkedServiceName**).</span></span> <span data-ttu-id="1ca29-198">Hdınsight Hello küme silindiğinde bu kapsayıcıyı silmez.</span><span class="sxs-lookup"><span data-stu-id="1ca29-198">HDInsight does not delete this container when hello cluster is deleted.</span></span> <span data-ttu-id="1ca29-199">Bu davranış tasarım gereğidir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-199">This behavior is by design.</span></span> <span data-ttu-id="1ca29-200">İsteğe bağlı HDInsight bağlı hizmeti kullanıldığında, mevcut canlı bir küme olmadığı sürece bir dilim her işlendiğinde bir HDInsight kümesi oluşturulur (**timeToLive**).</span><span class="sxs-lookup"><span data-stu-id="1ca29-200">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice is processed unless there is an existing live cluster (**timeToLive**).</span></span> <span data-ttu-id="1ca29-201">Merhaba işlem bittiğinde hello küme otomatik olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-201">hello cluster is automatically deleted when hello processing is done.</span></span>

       <span data-ttu-id="1ca29-202">Daha fazla dilim işlendikçe, Azure blob depolamanızda çok sayıda kapsayıcı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1ca29-202">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="1ca29-203">Bunları hello işlerin sorunları giderilmesi için ihtiyacınız yoksa, toodelete isteyebilirsiniz bunları tooreduce hello depolama maliyeti.</span><span class="sxs-lookup"><span data-stu-id="1ca29-203">If you do not need them for troubleshooting of hello jobs, you may want toodelete them tooreduce hello storage cost.</span></span> <span data-ttu-id="1ca29-204">Bu kapsayıcıların Hello adları izleyen bir desen: "adf**yourdatafactoryname**-**linkedservicename**- datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="1ca29-204">hello names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="1ca29-205">Gibi araçlar kullanın [Microsoft Storage Gezgini](http://storageexplorer.com/) toodelete kapsayıcılarında Azure blob depolama.</span><span class="sxs-lookup"><span data-stu-id="1ca29-205">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) toodelete containers in your Azure blob storage.</span></span>

     <span data-ttu-id="1ca29-206">Ayrıntılar için bkz. [İsteğe Bağlı HDInsight Bağlı Hizmeti](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service).</span><span class="sxs-lookup"><span data-stu-id="1ca29-206">See [On-demand HDInsight Linked Service](data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>
2. <span data-ttu-id="1ca29-207">Merhaba çalıştırmak **New-AzureRmDataFactoryLinkedService** hello oluşturur cmdlet bağlantılı Hdınsightondemandlinkedservice adlı hizmeti.</span><span class="sxs-lookup"><span data-stu-id="1ca29-207">Run hello **New-AzureRmDataFactoryLinkedService** cmdlet that creates hello linked service called HDInsightOnDemandLinkedService.</span></span>
    
    ```PowerShell
    New-AzureRmDataFactoryLinkedService $df -File .\HDInsightOnDemandLinkedService.json
    ```

## <a name="create-datasets"></a><span data-ttu-id="1ca29-208">Veri kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca29-208">Create datasets</span></span>
<span data-ttu-id="1ca29-209">Bu adımda, veri kümeleri toorepresent hello girişi oluşturun ve Hive işlenmesi için verileri çıktı.</span><span class="sxs-lookup"><span data-stu-id="1ca29-209">In this step, you create datasets toorepresent hello input and output data for Hive processing.</span></span> <span data-ttu-id="1ca29-210">Bu veri kümeleri toohello başvuran **StorageLinkedService** Bu öğreticide daha önce oluşturduğunuz.</span><span class="sxs-lookup"><span data-stu-id="1ca29-210">These datasets refer toohello **StorageLinkedService** you have created earlier in this tutorial.</span></span> <span data-ttu-id="1ca29-211">bağlantılı hizmet noktaları tooan Azure depolama hesabı hello ve veri kümeleri, giriş tutan hello depolamada kapsayıcı, klasör, dosya adı belirtin ve çıktı verilerini.</span><span class="sxs-lookup"><span data-stu-id="1ca29-211">hello linked service points tooan Azure Storage account and datasets specify container, folder, file name in hello storage that holds input and output data.</span></span>

### <a name="create-input-dataset"></a><span data-ttu-id="1ca29-212">Girdi veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca29-212">Create input dataset</span></span>
1. <span data-ttu-id="1ca29-213">Adlı bir JSON dosyası oluşturun **C:\adfgetstarted** hello içinde **C:\ADFGetStarted** içeriği aşağıdaki hello klasörüyle:</span><span class="sxs-lookup"><span data-stu-id="1ca29-213">Create a JSON file named **InputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

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
    <span data-ttu-id="1ca29-214">Merhaba JSON adlı veri kümesini tanımlayan **Azureblobınput**, hello ardışık düzeninde bir etkinliğin girdi verilerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1ca29-214">hello JSON defines a dataset named **AzureBlobInput**, which represents input data for an activity in hello pipeline.</span></span> <span data-ttu-id="1ca29-215">Ayrıca, hello giriş verisi adlı hello blob kapsayıcısında bulunur belirtir **adfgetstarted** ve adlı hello klasör **inputdata**.</span><span class="sxs-lookup"><span data-stu-id="1ca29-215">In addition, it specifies that hello input data is located in hello blob container called **adfgetstarted** and hello folder called **inputdata**.</span></span>

    <span data-ttu-id="1ca29-216">Merhaba aşağıdaki tabloda hello parçacığında kullanılan hello JSON özellikleri için açıklamalar sağlanır:</span><span class="sxs-lookup"><span data-stu-id="1ca29-216">hello following table provides descriptions for hello JSON properties used in hello snippet:</span></span>

   | <span data-ttu-id="1ca29-217">Özellik</span><span class="sxs-lookup"><span data-stu-id="1ca29-217">Property</span></span> | <span data-ttu-id="1ca29-218">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1ca29-218">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="1ca29-219">type</span><span class="sxs-lookup"><span data-stu-id="1ca29-219">type</span></span> |<span data-ttu-id="1ca29-220">verileri Azure blob depolamada yer aldığından hello type özelliği tooAzureBlob ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1ca29-220">hello type property is set tooAzureBlob because data resides in Azure blob storage.</span></span> |
   | <span data-ttu-id="1ca29-221">linkedServiceName</span><span class="sxs-lookup"><span data-stu-id="1ca29-221">linkedServiceName</span></span> |<span data-ttu-id="1ca29-222">daha önce oluşturduğunuz StorageLinkedService toohello başvuruyor.</span><span class="sxs-lookup"><span data-stu-id="1ca29-222">refers toohello StorageLinkedService you created earlier.</span></span> |
   | <span data-ttu-id="1ca29-223">fileName</span><span class="sxs-lookup"><span data-stu-id="1ca29-223">fileName</span></span> |<span data-ttu-id="1ca29-224">Bu özellik isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="1ca29-224">This property is optional.</span></span> <span data-ttu-id="1ca29-225">Bu özelliği atarsanız, hello folderPath tüm hello dosyalarından çekilir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-225">If you omit this property, all hello files from hello folderPath are picked.</span></span> <span data-ttu-id="1ca29-226">Bu durumda, yalnızca hello input.log işlenir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-226">In this case, only hello input.log is processed.</span></span> |
   | <span data-ttu-id="1ca29-227">type</span><span class="sxs-lookup"><span data-stu-id="1ca29-227">type</span></span> |<span data-ttu-id="1ca29-228">Merhaba günlük dosyaları metin biçiminde olduğundan TextFormat kullanacağız.</span><span class="sxs-lookup"><span data-stu-id="1ca29-228">hello log files are in text format, so we use TextFormat.</span></span> |
   | <span data-ttu-id="1ca29-229">columnDelimiter</span><span class="sxs-lookup"><span data-stu-id="1ca29-229">columnDelimiter</span></span> |<span data-ttu-id="1ca29-230">Merhaba günlük dosyalarındaki sütunlar hello virgül karakteriyle (,) sınırlandırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1ca29-230">columns in hello log files are delimited by hello comma character (,).</span></span> |
   | <span data-ttu-id="1ca29-231">frequency/interval</span><span class="sxs-lookup"><span data-stu-id="1ca29-231">frequency/interval</span></span> |<span data-ttu-id="1ca29-232">tooMonth sıklığını ve aralığı hello girdi dilimlerinin aylık olarak kullanılabileceğini 1.</span><span class="sxs-lookup"><span data-stu-id="1ca29-232">frequency set tooMonth and interval is 1, which means that hello input slices are available monthly.</span></span> |
   | <span data-ttu-id="1ca29-233">external</span><span class="sxs-lookup"><span data-stu-id="1ca29-233">external</span></span> |<span data-ttu-id="1ca29-234">Merhaba giriş verisi hello Data Factory hizmetiyle oluşturulmadıysa, bu özellik tootrue ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1ca29-234">this property is set tootrue if hello input data is not generated by hello Data Factory service.</span></span> |
2. <span data-ttu-id="1ca29-235">Azure PowerShell toocreate hello Data Factory veri kümesi komutunda aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1ca29-235">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\InputTable.json
    ```

### <a name="create-output-dataset"></a><span data-ttu-id="1ca29-236">Çıktı veri kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca29-236">Create output dataset</span></span>
<span data-ttu-id="1ca29-237">Şimdi, hello çıkış veri kümesi toorepresent hello çıktı verilerini hello Azure Blob Depolama depolanan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ca29-237">Now, you create hello output dataset toorepresent hello output data stored in hello Azure Blob storage.</span></span>

1. <span data-ttu-id="1ca29-238">Adlı bir JSON dosyası oluşturun **C:\adfgetstarted** hello içinde **C:\ADFGetStarted** içeriği aşağıdaki hello klasörüyle:</span><span class="sxs-lookup"><span data-stu-id="1ca29-238">Create a JSON file named **OutputTable.json** in hello **C:\ADFGetStarted** folder with hello following content:</span></span>

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
    <span data-ttu-id="1ca29-239">Merhaba JSON adlı veri kümesini tanımlayan **AzureBlobOutput**, hello ardışık düzeninde bir etkinliğin çıktı verilerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="1ca29-239">hello JSON defines a dataset named **AzureBlobOutput**, which represents output data for an activity in hello pipeline.</span></span> <span data-ttu-id="1ca29-240">Ayrıca, hello sonuçları adlı hello blob kapsayıcısında depolanır belirtir **adfgetstarted** ve adlı hello klasör **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="1ca29-240">In addition, it specifies that hello results are stored in hello blob container called **adfgetstarted** and hello folder called **partitioneddata**.</span></span> <span data-ttu-id="1ca29-241">Merhaba **kullanılabilirlik** bölümü belirtiyor bu hello çıktı veri kümesi, aylık olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1ca29-241">hello **availability** section specifies that hello output dataset is produced on a monthly basis.</span></span>
2. <span data-ttu-id="1ca29-242">Azure PowerShell toocreate hello Data Factory veri kümesi komutunda aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="1ca29-242">Run hello following command in Azure PowerShell toocreate hello Data Factory dataset:</span></span>

    ```PowerShell
    New-AzureRmDataFactoryDataset $df -File .\OutputTable.json
    ```

## <a name="create-pipeline"></a><span data-ttu-id="1ca29-243">İşlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca29-243">Create pipeline</span></span>
<span data-ttu-id="1ca29-244">Bu adımda, **HDInsightHive** etkinliğiyle ilk işlem hattınızı oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="1ca29-244">In this step, you create your first pipeline with a **HDInsightHive** activity.</span></span> <span data-ttu-id="1ca29-245">Girdi dilimi kullanılabilir aylık (sıklığı: Month, interval: 1), çıktı diliminin ayda bir oluşturulduğunu ve hello etkinlik hello Zamanlayıcı özelliğinin de toomonthly ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1ca29-245">Input slice is available monthly (frequency: Month, interval: 1), output slice is produced monthly, and hello scheduler property for hello activity is also set toomonthly.</span></span> <span data-ttu-id="1ca29-246">Merhaba çıktı veri kümesi ve hello etkinlik Zamanlayıcı Hello ayarlarının eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-246">hello settings for hello output dataset and hello activity scheduler must match.</span></span> <span data-ttu-id="1ca29-247">Şu anda, çıktı veri kümesi hello etkinlik herhangi bir çıktı üretmez olsa bile bir çıkış veri kümesi oluşturmanız gerekir böylece hangi sürücüleri zamanlama, hello değil.</span><span class="sxs-lookup"><span data-stu-id="1ca29-247">Currently, output dataset is what drives hello schedule, so you must create an output dataset even if hello activity does not produce any output.</span></span> <span data-ttu-id="1ca29-248">Merhaba etkinlik herhangi bir girdi almazsa oluşturma hello girdi veri kümesi atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ca29-248">If hello activity doesn't take any input, you can skip creating hello input dataset.</span></span> <span data-ttu-id="1ca29-249">JSON aşağıdaki hello kullanılan hello özellikleri hello bu bölümün sonuna açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1ca29-249">hello properties used in hello following JSON are explained at hello end of this section.</span></span>

1. <span data-ttu-id="1ca29-250">İçerik aşağıdaki hello ile Merhaba C:\ADFGetStarted klasöründe MyFirstPipelinePSH.json adlı bir JSON dosyası oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1ca29-250">Create a JSON file named MyFirstPipelinePSH.json in hello C:\ADFGetStarted folder with hello following content:</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="1ca29-251">Değiştir **storageaccountname** depolama hesabınızdaki hello JSON hello adı.</span><span class="sxs-lookup"><span data-stu-id="1ca29-251">Replace **storageaccountname** with hello name of your storage account in hello JSON.</span></span>
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
    <span data-ttu-id="1ca29-252">Merhaba JSON parçacığında, Hdınsight kümesinde Hive tooprocess veri kullanan tek bir etkinlik oluşan bir işlem hattı oluşturuyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="1ca29-252">In hello JSON snippet, you are creating a pipeline that consists of a single activity that uses Hive tooprocess Data on an HDInsight cluster.</span></span>

    <span data-ttu-id="1ca29-253">Merhaba Hive betik dosyası **partitionweblogs.hql**, hello Azure depolama hesabı depolanır (adlı hello scriptLinkedService tarafından belirtilen **StorageLinkedService**) ve **komut dosyası**  hello kapsayıcı klasöründe **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="1ca29-253">hello Hive script file, **partitionweblogs.hql**, is stored in hello Azure storage account (specified by hello scriptLinkedService, called **StorageLinkedService**), and in **script** folder in hello container **adfgetstarted**.</span></span>

    <span data-ttu-id="1ca29-254">Merhaba **tanımlar** bölümdür olması kullanılan toospecify hello çalışma zamanı ayarları toohello hive betiğini Hive yapılandırma değerleri olarak geçirilen (örn., ${hiveconf: inputtable}, ${hiveconf}).</span><span class="sxs-lookup"><span data-stu-id="1ca29-254">hello **defines** section is used toospecify hello runtime settings that be passed toohello hive script as Hive configuration values (e.g ${hiveconf:inputtable}, ${hiveconf:partitionedtable}).</span></span>

    <span data-ttu-id="1ca29-255">Merhaba **Başlat** ve **son** hello ardışık düzen özelliklerini hello etkin dönem hello ardışık belirtir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-255">hello **start** and **end** properties of hello pipeline specifies hello active period of hello pipeline.</span></span>

    <span data-ttu-id="1ca29-256">Bu hello Hive betiğini hello tarafından belirtilen hello işlem üzerinde çalıştığı belirtin Hello JSON etkinliğinde **linkedServiceName** – **Hdınsightondemandlinkedservice**.</span><span class="sxs-lookup"><span data-stu-id="1ca29-256">In hello activity JSON, you specify that hello Hive script runs on hello compute specified by hello **linkedServiceName** – **HDInsightOnDemandLinkedService**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1ca29-257">"Ardışık düzen JSON" bölümüne bakın [işlem hatlarının ve etkinliklerin Azure Data Factory](data-factory-create-pipelines.md) hello örnekte kullanılan JSON özellikleri hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="1ca29-257">See "Pipeline JSON" in [Pipelines and activities in Azure Data Factory](data-factory-create-pipelines.md) for details about JSON properties that are used in hello example.</span></span>

2. <span data-ttu-id="1ca29-258">Merhaba gördüğünüzü onaylayın **input.log** hello dosyasında **adfgetstarted/inputdata** hello Azure blob depolama ve komut toodeploy hello ardışık aşağıdaki çalışma hello klasöründe.</span><span class="sxs-lookup"><span data-stu-id="1ca29-258">Confirm that you see hello **input.log** file in hello **adfgetstarted/inputdata** folder in hello Azure blob storage, and run hello following command toodeploy hello pipeline.</span></span> <span data-ttu-id="1ca29-259">Merhaba itibaren **Başlat** ve **son** hello son kez ayarlanır ve **isPaused** dağıtıldıktan hemen sonra kümesi toofalse, hello ardışık düzen (Merhaba ardışık düzeninde etkinlik) çalışması olduğu.</span><span class="sxs-lookup"><span data-stu-id="1ca29-259">Since hello **start** and **end** times are set in hello past and **isPaused** is set toofalse, hello pipeline (activity in hello pipeline) runs immediately after you deploy.</span></span>

    ```PowerShell
    New-AzureRmDataFactoryPipeline $df -File .\MyFirstPipelinePSH.json
    ```
3. <span data-ttu-id="1ca29-260">Tebrikler, Azure PowerShell kullanarak ilk işlem hattınızı başarıyla oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="1ca29-260">Congratulations, you have successfully created your first pipeline using Azure PowerShell!</span></span>

## <a name="monitor-pipeline"></a><span data-ttu-id="1ca29-261">İşlem hattını izleme</span><span class="sxs-lookup"><span data-stu-id="1ca29-261">Monitor pipeline</span></span>
<span data-ttu-id="1ca29-262">Bu adımda, bir Azure data factory'de neler olduğunu Azure PowerShell toomonitor kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ca29-262">In this step, you use Azure PowerShell toomonitor what’s going on in an Azure data factory.</span></span>

1. <span data-ttu-id="1ca29-263">Çalıştırma **Get-AzureRmDataFactory** ve hello çıktı tooa Ata **$df** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="1ca29-263">Run **Get-AzureRmDataFactory** and assign hello output tooa **$df** variable.</span></span>

    ```PowerShell
    $df=Get-AzureRmDataFactory -ResourceGroupName ADFTutorialResourceGroup -Name FirstDataFactoryPSH
    ```
2. <span data-ttu-id="1ca29-264">Çalıştırma **Get-AzureRmDataFactorySlice** hello tüm dilimleri hakkında bilgi tooget **EmpSQLTable**, hello ardışık hello çıktı tablosu.</span><span class="sxs-lookup"><span data-stu-id="1ca29-264">Run **Get-AzureRmDataFactorySlice** tooget details about all slices of hello **EmpSQLTable**, which is hello output table of hello pipeline.</span></span>

    ```PowerShell
    Get-AzureRmDataFactorySlice $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```
    <span data-ttu-id="1ca29-265">Bu hello burada belirttiğiniz StartDateTime aynı hello ile JSON işlem hattında belirtilen başlangıç zamanıyla hello olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="1ca29-265">Notice that hello StartDateTime you specify here is hello same start time specified in hello pipeline JSON.</span></span> <span data-ttu-id="1ca29-266">Merhaba örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1ca29-266">Here is hello sample output:</span></span>

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
3. <span data-ttu-id="1ca29-267">Çalıştırma **Get-AzureRmDataFactoryRun** tooget hello etkinliğinin ayrıntılarını belirli bir dilimle ilgili çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="1ca29-267">Run **Get-AzureRmDataFactoryRun** tooget hello details of activity runs for a specific slice.</span></span>

    ```PowerShell
    Get-AzureRmDataFactoryRun $df -DatasetName AzureBlobOutput -StartDateTime 2017-07-01
    ```

    <span data-ttu-id="1ca29-268">Merhaba örnek çıktı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1ca29-268">Here is hello sample output:</span></span> 

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
    <span data-ttu-id="1ca29-269">Merhaba dilimi görene kadar bu cmdlet çalışmaya devam **hazır** durumu veya **başarısız** durumu.</span><span class="sxs-lookup"><span data-stu-id="1ca29-269">You can keep running this cmdlet until you see hello slice in **Ready** state or **Failed** state.</span></span> <span data-ttu-id="1ca29-270">Merhaba dilim hazır durumunda olduğunda hello denetleyin **partitioneddata** hello klasöründe **adfgetstarted** hello için blob depolama alanınızın kapsayıcısında çıkış verileri.</span><span class="sxs-lookup"><span data-stu-id="1ca29-270">When hello slice is in Ready state, check hello **partitioneddata** folder in hello **adfgetstarted** container in your blob storage for hello output data.</span></span>  <span data-ttu-id="1ca29-271">İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır.</span><span class="sxs-lookup"><span data-stu-id="1ca29-271">Creation of an on-demand HDInsight cluster usually takes some time.</span></span>

    ![çıktı verileri](./media/data-factory-build-your-first-pipeline-using-powershell/three-ouptut-files.png)

> [!IMPORTANT]
> <span data-ttu-id="1ca29-273">İsteğe bağlı HDInsight kümesinin oluşturulması genellikle biraz zaman alır (yaklaşık 20 dakika).</span><span class="sxs-lookup"><span data-stu-id="1ca29-273">Creation of an on-demand HDInsight cluster usually takes sometime (approximately 20 minutes).</span></span> <span data-ttu-id="1ca29-274">Bu nedenle, hello ardışık düzen tootake beklediğiniz **yaklaşık olarak 30 dakika** tooprocess hello dilim.</span><span class="sxs-lookup"><span data-stu-id="1ca29-274">Therefore, expect hello pipeline tootake **approximately 30 minutes** tooprocess hello slice.</span></span>
>
> <span data-ttu-id="1ca29-275">Merhaba dilim başarıyla işlendiğinde hello girdi dosyası silinir.</span><span class="sxs-lookup"><span data-stu-id="1ca29-275">hello input file gets deleted when hello slice is processed successfully.</span></span> <span data-ttu-id="1ca29-276">Bu nedenle, toorerun hello dilim istediğiniz veya öğreticiyi yeniden Merhaba, hello adfgetstarted kapsayıcısının hello girdi dosyasını (input.log) toohello inputdata klasörüne yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1ca29-276">Therefore, if you want toorerun hello slice or do hello tutorial again, upload hello input file (input.log) toohello inputdata folder of hello adfgetstarted container.</span></span>
>
>

## <a name="summary"></a><span data-ttu-id="1ca29-277">Özet</span><span class="sxs-lookup"><span data-stu-id="1ca29-277">Summary</span></span>
<span data-ttu-id="1ca29-278">Bu öğreticide, bir Hdınsight hadoop kümesindeki Hive betiği çalıştıran bir Azure data factory tooprocess veri oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="1ca29-278">In this tutorial, you created an Azure data factory tooprocess data by running Hive script on a HDInsight hadoop cluster.</span></span> <span data-ttu-id="1ca29-279">Hello Data Factory Düzenleyici'hello Azure portal toodo hello aşağıdaki adımları kullanılır:</span><span class="sxs-lookup"><span data-stu-id="1ca29-279">You used hello Data Factory Editor in hello Azure portal toodo hello following steps:</span></span>

1. <span data-ttu-id="1ca29-280">Oluşturulan Azure **data factory**.</span><span class="sxs-lookup"><span data-stu-id="1ca29-280">Created an Azure **data factory**.</span></span>
2. <span data-ttu-id="1ca29-281">Oluşturulan iki **bağlı hizmet**:</span><span class="sxs-lookup"><span data-stu-id="1ca29-281">Created two **linked services**:</span></span>
   1. <span data-ttu-id="1ca29-282">**Azure depolama** hizmet toolink toohello veri fabrikası girdi/çıktı dosyalarını tutan Azure blob depolama alanınızın bağlı.</span><span class="sxs-lookup"><span data-stu-id="1ca29-282">**Azure Storage** linked service toolink your Azure blob storage that holds input/output files toohello data factory.</span></span>
   2. <span data-ttu-id="1ca29-283">**Azure Hdınsight** isteğe bağlı bir isteğe bağlı Hdınsight Hadoop küme toohello data factory hizmeti toolink bağlı.</span><span class="sxs-lookup"><span data-stu-id="1ca29-283">**Azure HDInsight** on-demand linked service toolink an on-demand HDInsight Hadoop cluster toohello data factory.</span></span> <span data-ttu-id="1ca29-284">Azure Data Factory Hdınsight Hadoop küme yalnızca zaman tooprocess giriş verileri hem de üretim çıktı verilerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ca29-284">Azure Data Factory creates a HDInsight Hadoop cluster just-in-time tooprocess input data and produce output data.</span></span>
3. <span data-ttu-id="1ca29-285">Oluşturulan iki **veri kümeleri**, hello ardışık düzende Hdınsight Hive etkinliğiyle ilgili girdi ve çıktı verilerini açıklayan.</span><span class="sxs-lookup"><span data-stu-id="1ca29-285">Created two **datasets**, which describe input and output data for HDInsight Hive activity in hello pipeline.</span></span>
4. <span data-ttu-id="1ca29-286">**HDInsight Hive** etkinliğine sahip oluşturulan bir **işlem hattı**.</span><span class="sxs-lookup"><span data-stu-id="1ca29-286">Created a **pipeline** with a **HDInsight Hive** activity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ca29-287">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ca29-287">Next steps</span></span>
<span data-ttu-id="1ca29-288">Bu makalede, isteğe bağlı Azure HDInsight kümesinde bir Hive betiği çalıştıran dönüştürme etkinliğine (HDInsight Etkinliği) sahip işlem hattı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="1ca29-288">In this article, you have created a pipeline with a transformation activity (HDInsight Activity) that runs a Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="1ca29-289">toouse Azure Blob tooAzure SQL, bir kopyalama etkinliği toocopy verileri nasıl görürüm toosee [öğretici: bir Azure Blob tooAzure SQL veri kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="1ca29-289">toosee how toouse a Copy Activity toocopy data from an Azure Blob tooAzure SQL, see [Tutorial: Copy data from an Azure Blob tooAzure SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1ca29-290">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="1ca29-290">See Also</span></span>
| <span data-ttu-id="1ca29-291">Konu</span><span class="sxs-lookup"><span data-stu-id="1ca29-291">Topic</span></span> | <span data-ttu-id="1ca29-292">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1ca29-292">Description</span></span> |
|:--- |:--- |
| [<span data-ttu-id="1ca29-293">Data Factory Cmdlet Başvurusu</span><span class="sxs-lookup"><span data-stu-id="1ca29-293">Data Factory Cmdlet Reference</span></span>](/powershell/module/azurerm.datafactories) |<span data-ttu-id="1ca29-294">Data Factory cmdlet'leri hakkında kapsamlı belgelere bakma</span><span class="sxs-lookup"><span data-stu-id="1ca29-294">See comprehensive documentation on Data Factory cmdlets</span></span> |
| [<span data-ttu-id="1ca29-295">İşlem hatları</span><span class="sxs-lookup"><span data-stu-id="1ca29-295">Pipelines</span></span>](data-factory-create-pipelines.md) |<span data-ttu-id="1ca29-296">Bu makalede, işlem hatlarının ve etkinliklerin Azure Data Factory anlamanıza yardımcı olur ve nasıl toouse bunları tooconstruct uçtan uca veri odaklı iş akışlarının senaryo veya iş.</span><span class="sxs-lookup"><span data-stu-id="1ca29-296">This article helps you understand pipelines and activities in Azure Data Factory and how toouse them tooconstruct end-to-end data-driven workflows for your scenario or business.</span></span> |
| [<span data-ttu-id="1ca29-297">Veri kümeleri</span><span class="sxs-lookup"><span data-stu-id="1ca29-297">Datasets</span></span>](data-factory-create-datasets.md) |<span data-ttu-id="1ca29-298">Bu makale, Azure Data Factory’deki veri kümelerini anlamanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1ca29-298">This article helps you understand datasets in Azure Data Factory.</span></span> |
| [<span data-ttu-id="1ca29-299">Zamanlama ve Yürütme</span><span class="sxs-lookup"><span data-stu-id="1ca29-299">Scheduling and Execution</span></span>](data-factory-scheduling-and-execution.md) |<span data-ttu-id="1ca29-300">Bu makalede Azure Data Factory uygulama modelinin hello zamanlama ve yürütme yönleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1ca29-300">This article explains hello scheduling and execution aspects of Azure Data Factory application model.</span></span> |
| [<span data-ttu-id="1ca29-301">İzleme Uygulaması kullanılarak işlem hatlarını izleme ve yönetme</span><span class="sxs-lookup"><span data-stu-id="1ca29-301">Monitor and manage pipelines using Monitoring App</span></span>](data-factory-monitor-manage-app.md) |<span data-ttu-id="1ca29-302">Bu makalede nasıl toomonitor, yönetme ve hatalarını ayıklama işlem hatlarını izleme ve yönetim uygulaması hello kullanarak.</span><span class="sxs-lookup"><span data-stu-id="1ca29-302">This article describes how toomonitor, manage, and debug pipelines using hello Monitoring & Management App.</span></span> |
