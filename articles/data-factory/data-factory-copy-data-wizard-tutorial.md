---
title: "Öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma | Microsoft Belgeleri"
description: "Bu öğreticide, bir Azure Data Factory işlem hattı kopyalama etkinliği ile Merhaba Data Factory ile desteklenen Kopyalama Sihirbazı'nı kullanarak oluşturduğunuz"
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b87afb8e-53b7-4e1b-905b-0343dd096198
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 567b89e7a54c245c134cd0674690e6f3499b46d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="1b43c-103">Öğretici: Data Factory Kopyalama Sihirbazı kullanarak Kopyalama Etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1b43c-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1b43c-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1b43c-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="1b43c-105">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="1b43c-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="1b43c-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="1b43c-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="1b43c-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1b43c-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="1b43c-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b43c-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="1b43c-109">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="1b43c-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="1b43c-110">REST API</span><span class="sxs-lookup"><span data-stu-id="1b43c-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="1b43c-111">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="1b43c-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="1b43c-112">Bu öğretici şunların nasıl yapıldığını gösterir toouse hello **Kopyalama Sihirbazı'nı** bir Azure blob depolama tooan Azure SQL veritabanından toocopy veri.</span><span class="sxs-lookup"><span data-stu-id="1b43c-112">This tutorial shows you how toouse hello **Copy Wizard** toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> 

<span data-ttu-id="1b43c-113">Hello Azure Data Factory **Kopyalama Sihirbazı'nı** sağlar tooquickly bir desteklenen kaynak veri deposu desteklenen tooa hedef veri deposundan verileri kopyalayan bir veri işlem hattı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1b43c-113">hello Azure Data Factory **Copy Wizard** allows you tooquickly create a data pipeline that copies data from a supported source data store tooa supported destination data store.</span></span> <span data-ttu-id="1b43c-114">Bu nedenle, veri taşıma senaryonuz için ilk adım toocreate örnek bir işlem hattı hello Sihirbazı'nı kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="1b43c-114">Therefore, we recommend that you use hello wizard as a first step toocreate a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="1b43c-115">Kaynak ve hedef olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="1b43c-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="1b43c-116">Bu öğretici nasıl toocreate başlatma hello Kopyalama Sihirbazı, bir Azure data factory geçtikleri bir dizi adımları tooprovide veri alım/taşıma senaryonuz ayrıntılarını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1b43c-116">This tutorial shows you how toocreate an Azure data factory, launch hello Copy Wizard, go through a series of steps tooprovide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="1b43c-117">Hello sihirbazındaki adımları tamamladığınızda, Başlangıç Sihirbazı'nı bir ardışık düzen kopyalama etkinliği toocopy verilerle Azure blob depolama tooan Azure SQL veritabanını otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1b43c-117">When you finish steps in hello wizard, hello wizard automatically creates a pipeline with a Copy Activity toocopy data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="1b43c-118">Kopyalama Etkinliği hakkında daha fazla bilgi için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="1b43c-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b43c-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1b43c-119">Prerequisites</span></span>
<span data-ttu-id="1b43c-120">Hello listelenen önkoşulları tamamlamanız [öğreticiye genel bakış](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) Bu öğreticiyi gerçekleştirmeden önce makalesi.</span><span class="sxs-lookup"><span data-stu-id="1b43c-120">Complete prerequisites listed in hello [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="1b43c-121">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="1b43c-121">Create data factory</span></span>
<span data-ttu-id="1b43c-122">Bu adımda, kullandığınız hello Azure portal toocreate adlı bir Azure data factory **ADFTutorialDataFactory**.</span><span class="sxs-lookup"><span data-stu-id="1b43c-122">In this step, you use hello Azure portal toocreate an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="1b43c-123">Çok oturum[Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b43c-123">Log in too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b43c-124">Tıklatın **+ yeni** hello sol üst köşeden tıklatın **veri + analiz**, tıklatıp **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="1b43c-124">Click **+ NEW** from hello top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![Yeni->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="1b43c-126">Merhaba, **yeni data factory** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="1b43c-126">In hello **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="1b43c-127">Girin **ADFTutorialDataFactory** hello için **adı**.</span><span class="sxs-lookup"><span data-stu-id="1b43c-127">Enter **ADFTutorialDataFactory** for hello **name**.</span></span>
       <span data-ttu-id="1b43c-128">Merhaba hello Azure veri fabrikasının adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b43c-128">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="1b43c-129">Merhaba hatayı alırsanız: `Data factory name “ADFTutorialDataFactory” is not available`, hello veri fabrikası (örneğin, yournameADFTutorialDataFactoryYYYYMMDD) hello adını değiştirin ve oluşturmayı yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="1b43c-129">If you receive hello error: `Data factory name “ADFTutorialDataFactory” is not available`, change hello name of hello data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="1b43c-130">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="1b43c-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Data Factory adı yok](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="1b43c-132">Azure **aboneliğinizi** seçin.</span><span class="sxs-lookup"><span data-stu-id="1b43c-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="1b43c-133">Kaynak grubu için aşağıdaki adımları hello birini yapın:</span><span class="sxs-lookup"><span data-stu-id="1b43c-133">For Resource Group, do one of hello following steps:</span></span> 
      
      - <span data-ttu-id="1b43c-134">Seçin **var olanı kullan** tooselect varolan bir kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="1b43c-134">Select **Use existing** tooselect an existing resource group.</span></span>
      - <span data-ttu-id="1b43c-135">Seçin **Yeni Oluştur** tooenter bir kaynak grubu için bir ad.</span><span class="sxs-lookup"><span data-stu-id="1b43c-135">Select **Create new** tooenter a name for a resource group.</span></span>
          
        <span data-ttu-id="1b43c-136">Bu öğreticideki hello adımlardan bazıları hello adı kullandığınızı varsayar: **ADFTutorialResourceGroup** hello kaynak grubu için.</span><span class="sxs-lookup"><span data-stu-id="1b43c-136">Some of hello steps in this tutorial assume that you use hello name: **ADFTutorialResourceGroup** for hello resource group.</span></span> <span data-ttu-id="1b43c-137">Kaynak grupları hakkında toolearn bkz [Azure kaynaklarınızı grupları toomanage kaynağı kullanan](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1b43c-137">toolearn about resource groups, see [Using resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="1b43c-138">Seçin bir **konumu** hello veri fabrikası için.</span><span class="sxs-lookup"><span data-stu-id="1b43c-138">Select a **location** for hello data factory.</span></span>
   5. <span data-ttu-id="1b43c-139">Seçin **PIN toodashboard** hello dikey penceresinde hello altındaki onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="1b43c-139">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>  
   6. <span data-ttu-id="1b43c-140">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b43c-140">Click **Create**.</span></span>
      
       ![Yeni veri fabrikası dikey penceresi](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="1b43c-142">Merhaba oluşturma işlemi tamamlandıktan sonra hello bkz **Data Factory** dikey penceresini hello görüntü aşağıdaki gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="1b43c-142">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image:</span></span>
   
   ![Data factory giriş sayfası](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="1b43c-144">Kopyalama Sihirbazı'nı başlatma</span><span class="sxs-lookup"><span data-stu-id="1b43c-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="1b43c-145">Merhaba Data Factory dikey penceresinde **kopyalama [Önizleme] verileri** toolaunch hello **Kopyalama Sihirbazı'nı**.</span><span class="sxs-lookup"><span data-stu-id="1b43c-145">On hello Data Factory blade, click **Copy data [PREVIEW]** toolaunch hello **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="1b43c-146">Bu hello web tarayıcısının "Yetkilendiriliyor..." takılmış görürseniz, devre dışı bırakın/işaretini **üçüncü taraf tanımlama bilgilerini engelleyebilir ve site verileri** hello tarayıcı ayarlarını (veya) etkin tutma ayarlama ve oluşturmak için bir özel durum  **Login.microsoftonline.com** ve hello Sihirbazı yeniden başlatmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="1b43c-146">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in hello browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="1b43c-147">Merhaba, **özellikleri** sayfa:</span><span class="sxs-lookup"><span data-stu-id="1b43c-147">In hello **Properties** page:</span></span>
   
   1. <span data-ttu-id="1b43c-148">**Görev adı** için **CopyFromBlobToAzureSql** girin</span><span class="sxs-lookup"><span data-stu-id="1b43c-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="1b43c-149">**Açıklama** girin (isteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="1b43c-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="1b43c-150">Değişiklik hello **başlangıç tarihi ve saati** ve hello **bitiş tarihi ve saati** hello bitiş tarihi ayarla tootoday ve tarih toofive gün önce başla olmasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1b43c-150">Change hello **Start date time** and hello **End date time** so that hello end date is set tootoday and start date toofive days earlier.</span></span>  
   4. <span data-ttu-id="1b43c-151">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b43c-151">Click **Next**.</span></span>  
      
      ![Kopyalama Aracı - Özellikler sayfası](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="1b43c-153">Merhaba üzerinde **kaynak veri deposu** sayfasında, **Azure Blob Storage** döşeme.</span><span class="sxs-lookup"><span data-stu-id="1b43c-153">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="1b43c-154">Bu sayfa toospecify hello kaynak veri deposu hello kopyalama görevi için kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b43c-154">You use this page toospecify hello source data store for hello copy task.</span></span> 
   
    ![Kopyalama Aracı - Kaynak veri deposu sayfası](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="1b43c-156">Merhaba üzerinde **hello Azure Blob Depolama hesabı belirtin** sayfa:</span><span class="sxs-lookup"><span data-stu-id="1b43c-156">On hello **Specify hello Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="1b43c-157">**Bağlı hizmet adı** için **AzureStorageLinkedService** girin.</span><span class="sxs-lookup"><span data-stu-id="1b43c-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="1b43c-158">**Hesap seçme yöntemi** için **Azure aboneliklerinden** seçeneğinin belirlendiğini onaylayın.</span><span class="sxs-lookup"><span data-stu-id="1b43c-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="1b43c-159">Azure **aboneliğinizi** seçin.</span><span class="sxs-lookup"><span data-stu-id="1b43c-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="1b43c-160">Seçin bir **Azure depolama hesabı** hello hesaplarına Azure depolama listesi hello seçili abonelikte kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1b43c-160">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="1b43c-161">Ayrıca tooenter depolama hesabı ayarlarını el ile seçerek seçebilirsiniz **el ile girmeniz** hello seçeneği **hesap seçme yöntemi**ve ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="1b43c-161">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**, and then click **Next**.</span></span> 
      
      ![Kopyalama aracı - hello Azure Blob Depolama hesabı belirtin](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="1b43c-163">Üzerinde **Seç hello girdi dosyası veya klasörü** sayfa:</span><span class="sxs-lookup"><span data-stu-id="1b43c-163">On **Choose hello input file or folder** page:</span></span>
   
   1. <span data-ttu-id="1b43c-164">**adftutorial** seçeneğine (klasör) çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b43c-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="1b43c-165">**emp.txt** dosyasını seçip **Seç** öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="1b43c-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![Kopyalama aracı - hello girdi dosyası veya klasörü seçin](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="1b43c-167">Merhaba üzerinde **Seç hello girdi dosyası veya klasörü** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="1b43c-167">On hello **Choose hello input file or folder** page, click **Next**.</span></span> <span data-ttu-id="1b43c-168">**İkili kopya**’yı seçmeyin.</span><span class="sxs-lookup"><span data-stu-id="1b43c-168">Do not select **Binary copy**.</span></span> 
   
    ![Kopyalama aracı - hello girdi dosyası veya klasörü seçin](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="1b43c-170">Merhaba üzerinde **dosya biçimi ayarları** sayfasında, gördüğünüz hello sınırlayıcıları ve hello dosyası ayrıştırılırken hello Sihirbazı tarafından otomatik olarak algılanır hello şema.</span><span class="sxs-lookup"><span data-stu-id="1b43c-170">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> <span data-ttu-id="1b43c-171">Da hello sınırlayıcıları el ile Merhaba Kopyalama Sihirbazı'nı toostop otomatik-algılama veya toooverride girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b43c-171">You can also enter hello delimiters manually for hello copy wizard toostop auto-detecting or toooverride.</span></span> <span data-ttu-id="1b43c-172">Tıklatın **sonraki** hello sınırlayıcıları gözden geçirin ve Önizleme veri sonra.</span><span class="sxs-lookup"><span data-stu-id="1b43c-172">Click **Next** after you review hello delimiters and preview data.</span></span> 
   
    ![Kopyalama Aracı - Dosya biçimi ayarları](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="1b43c-174">Merhaba hedef veri deposu sayfasında, seçin **Azure SQL veritabanı**, tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="1b43c-174">On hello Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Kopyalama Aracı - Hedef depo seçme](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="1b43c-176">Üzerinde **belirt hello Azure SQL veritabanı** sayfa:</span><span class="sxs-lookup"><span data-stu-id="1b43c-176">On **Specify hello Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="1b43c-177">Girin **AzureSqlLinkedService** hello için **bağlantı adı** alan.</span><span class="sxs-lookup"><span data-stu-id="1b43c-177">Enter **AzureSqlLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="1b43c-178">**Sunucu / veritabanı seçme yöntemi** için **Azure aboneliklerinden** seçeneğinin belirlendiğini onaylayın.</span><span class="sxs-lookup"><span data-stu-id="1b43c-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="1b43c-179">Azure **aboneliğinizi** seçin.</span><span class="sxs-lookup"><span data-stu-id="1b43c-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="1b43c-180">**Sunucu adı** ve **Veritabanı** öğelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="1b43c-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="1b43c-181">**Kullanıcı Adı** ve **Parola** girin.</span><span class="sxs-lookup"><span data-stu-id="1b43c-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="1b43c-182">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b43c-182">Click **Next**.</span></span>  
      
      ![Kopyalama Aracı - Azure SQL veritabanı belirtme](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="1b43c-184">Merhaba üzerinde **tablo eşlemesi** sayfasında, **emp** hello için **hedef** alan hello aşağı açılan listeden, tıklatın **aşağı ok** (isteğe bağlı) toosee hello şema ve toopreview hello verileri.</span><span class="sxs-lookup"><span data-stu-id="1b43c-184">On hello **Table mapping** page, select **emp** for hello **Destination** field from hello drop-down list, click **down arrow** (optional) toosee hello schema and toopreview hello data.</span></span>
    
     ![Kopyalama Aracı - Tablo eşleme](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="1b43c-186">Merhaba üzerinde **şema eşleme** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="1b43c-186">On hello **Schema mapping** page, click **Next**.</span></span>
    
    ![Kopyalama Aracı - düzen eşlemesi](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="1b43c-188">Merhaba üzerinde **performans ayarlarını** sayfasında, **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="1b43c-188">On hello **Performance settings** page, click **Next**.</span></span> 
    
    ![Kopyalama Aracı - performans ayarları](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="1b43c-190">Merhaba bilgileri gözden **Özet** sayfasında ve tıklayın **son**.</span><span class="sxs-lookup"><span data-stu-id="1b43c-190">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="1b43c-191">Başlangıç Sihirbazı'nı (Başlangıç burada hello Kopyalama Sihirbazı'nı başlatılan) hello veri fabrikasında iki bağlı hizmet, iki veri kümesi (girdi ve çıktı) ve bir işlem hattı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1b43c-191">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span> 
    
    ![Kopyalama Aracı - performans ayarları](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="1b43c-193">Uygulama İzleme ve Yönetmeyi başlatma</span><span class="sxs-lookup"><span data-stu-id="1b43c-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="1b43c-194">Merhaba üzerinde **dağıtım** sayfasında, hello bağlantıyı tıklatın: `Click here toomonitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="1b43c-194">On hello **Deployment** page, click hello link: `Click here toomonitor copy pipeline`.</span></span>
   
   ![Kopyalama Aracı - Dağıtım başarılı](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="1b43c-196">Uygulama izleme hello web tarayıcınızda ayrı bir sekmede başlatılır.</span><span class="sxs-lookup"><span data-stu-id="1b43c-196">hello monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![İzleme Uygulaması](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="1b43c-198">toosee hello son durumunu saat dilimleri tıklatın **yenileme** hello düğmesini **etkinlik WINDOWS** hello altındaki listesi.</span><span class="sxs-lookup"><span data-stu-id="1b43c-198">toosee hello latest status of hourly slices, click **Refresh** button in hello **ACTIVITY WINDOWS** list at hello bottom.</span></span> <span data-ttu-id="1b43c-199">Beş etkinlik windows hello ardışık düzeni için başlangıç ve bitiş zamanları arasında beş gün boyunca bakın.</span><span class="sxs-lookup"><span data-stu-id="1b43c-199">You see five activity windows for five days between start and end times for hello pipeline.</span></span> <span data-ttu-id="1b43c-200">Merhaba listesi otomatik olarak yenilenmez, açabilmeniz için tooclick birkaç tüm hello etkinlik windows hello hazır durumda görmeden önce kaç kez yenilemeniz.</span><span class="sxs-lookup"><span data-stu-id="1b43c-200">hello list is not automatically refreshed, so you may need tooclick Refresh a couple of times before you see all hello activity windows in hello Ready state.</span></span> 
4. <span data-ttu-id="1b43c-201">Bir etkinlik penceresinde hello listesinde seçin.</span><span class="sxs-lookup"><span data-stu-id="1b43c-201">Select an activity window in hello list.</span></span> <span data-ttu-id="1b43c-202">Merhaba hakkındaki Hello ayrıntıları görmek **etkinlik penceresini Explorer** hello sağ üzerinde.</span><span class="sxs-lookup"><span data-stu-id="1b43c-202">See hello details about it in hello **Activity Window Explorer** on hello right.</span></span>

    ![Etkinlik penceresi ayrıntıları](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="1b43c-204">Merhaba tarihleri 11, 12, 13, 14 ve 15 hello günlük çıktısı dilimler bu tarihler için zaten oluşturulmuş olduğunu anlamına gelir, yeşil renkte olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="1b43c-204">Notice that hello dates 11, 12, 13, 14, and 15 are in green color, which means that hello daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="1b43c-205">Ayrıca bu renk hello ardışık kodlama bakın ve çıktı veri kümesi hello diyagram görünümünde hello.</span><span class="sxs-lookup"><span data-stu-id="1b43c-205">You also see this color coding on hello pipeline and hello output dataset in hello diagram view.</span></span> <span data-ttu-id="1b43c-206">Hello önceki adımda (Merhaba renk kodlama göre) iki dilimlerinin zaten oluşturulmuş olduğunu, bir dilim işlenmekte olan ve hello diğer iki işlenen toobe bekleyen dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="1b43c-206">In hello previous step, notice that two slices have already been produced, one slice is currently being processed, and hello other two are waiting toobe processed (based on hello color coding).</span></span> 

    <span data-ttu-id="1b43c-207">Bu uygulamayı kullanma hakkında daha fazla bilgi için [İzleme Uygulamasını kullanarak işlem hattını izleme ve yönetme](data-factory-monitor-manage-app.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="1b43c-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b43c-208">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1b43c-208">Next steps</span></span>
<span data-ttu-id="1b43c-209">Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız.</span><span class="sxs-lookup"><span data-stu-id="1b43c-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="1b43c-210">Merhaba aşağıdaki tabloda kaynakları ve hedefleri hello kopyalama etkinliği tarafından desteklenen veri depoları listesi verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1b43c-210">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="1b43c-211">Bir veri deposu hello Kopyalama Sihirbazı'nda bkz alanları/özellikleri hakkında daha fazla ayrıntı için hello tablo veri deposunda hello hello bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1b43c-211">For details about fields/properties that you see in hello copy wizard for a data store, click hello link for hello data store in hello table.</span></span> 
