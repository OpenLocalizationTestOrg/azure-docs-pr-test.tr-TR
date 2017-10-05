---
title: "Öğretici: Kopyalama Sihirbazı'nı kullanarak bir işlem hattı oluşturma | Microsoft Belgeleri"
description: "Bu öğreticide, Data Factory ile desteklenen Kopyalama Sihirbazı’nı kullanarak Kopyalama Etkinlikli bir Azure Data Factory işlem hattı oluşturursunuz"
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
ms.openlocfilehash: 5922c050cc09236ba5fdec885a70d11da20135cd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-data-factory-copy-wizard"></a><span data-ttu-id="97c2f-103">Öğretici: Data Factory Kopyalama Sihirbazı kullanarak Kopyalama Etkinliği ile işlem hattı oluşturma</span><span class="sxs-lookup"><span data-stu-id="97c2f-103">Tutorial: Create a pipeline with Copy Activity using Data Factory Copy Wizard</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="97c2f-104">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="97c2f-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="97c2f-105">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="97c2f-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="97c2f-106">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="97c2f-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="97c2f-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="97c2f-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="97c2f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="97c2f-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="97c2f-109">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="97c2f-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="97c2f-110">REST API</span><span class="sxs-lookup"><span data-stu-id="97c2f-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="97c2f-111">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="97c2f-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="97c2f-112">Bu öğretici, verileri bir Azure blob depolamadan Azure SQL veritabanına kopyalamak için **Kopyalama Sihirbazı**’nın nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="97c2f-112">This tutorial shows you how to use the **Copy Wizard** to copy data from an Azure blob storage to an Azure SQL database.</span></span> 

<span data-ttu-id="97c2f-113">Azure Data Factory **Kopyalama Sihirbazı**, verileri desteklenen kaynak veri deposundan desteklenen bir hedef veri deposuna kopyalayan veri işlem hattını hızlıca oluşturmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="97c2f-113">The Azure Data Factory **Copy Wizard** allows you to quickly create a data pipeline that copies data from a supported source data store to a supported destination data store.</span></span> <span data-ttu-id="97c2f-114">Bu nedenle, veri taşıma senaryonuza yönelik bir örnek işlem hattı oluşturmanın ilk adımı olarak sihirbazı kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="97c2f-114">Therefore, we recommend that you use the wizard as a first step to create a sample pipeline for your data movement scenario.</span></span> <span data-ttu-id="97c2f-115">Kaynak ve hedef olarak desteklenen veri depolarının listesi için bkz. [desteklenen veri depoları](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="97c2f-115">For a list of data stores supported as sources and as destinations, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span>  

<span data-ttu-id="97c2f-116">Bu öğretici bir Azure veri fabrikası oluşturma ve Kopyalama Sihirbazı’nı başlatma işlemlerini göstermesinin yanı sıra veri alma/taşıma senaryonuza ilişkin ayrıntılar sağlayan bir dizi adım uygular.</span><span class="sxs-lookup"><span data-stu-id="97c2f-116">This tutorial shows you how to create an Azure data factory, launch the Copy Wizard, go through a series of steps to provide details about your data ingestion/movement scenario.</span></span> <span data-ttu-id="97c2f-117">Sihirbazdaki adımları tamamladığınızda sihirbaz bir Azure blob depolama alanından Azure SQL veritabanına veri kopyalamak için Kopyalama Etkinliği içeren bir işlem hattını otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="97c2f-117">When you finish steps in the wizard, the wizard automatically creates a pipeline with a Copy Activity to copy data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="97c2f-118">Kopyalama Etkinliği hakkında daha fazla bilgi için bkz. [veri taşıma etkinlikleri](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="97c2f-118">For more information about Copy Activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97c2f-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="97c2f-119">Prerequisites</span></span>
<span data-ttu-id="97c2f-120">Bu öğreticiyi uygulamadan önce [Öğreticiye Genel Bakış](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) makalesinde listelenen önkoşulları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-120">Complete prerequisites listed in the [Tutorial Overview](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) article before performing this tutorial.</span></span>

## <a name="create-data-factory"></a><span data-ttu-id="97c2f-121">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="97c2f-121">Create data factory</span></span>
<span data-ttu-id="97c2f-122">Bu adımda **ADFTutorialDataFactory** adlı bir Azure data factory oluşturmak için Azure Portal’ı kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="97c2f-122">In this step, you use the Azure portal to create an Azure data factory named **ADFTutorialDataFactory**.</span></span>

1. <span data-ttu-id="97c2f-123">[Azure portalı](https://portal.azure.com)’nda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-123">Log in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="97c2f-124">Sol üst köşedeki **+YENİ** öğesine **Veri + analiz**’e ve **Data Factory** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-124">Click **+ NEW** from the top-left corner, click **Data + analytics**, and click **Data Factory**.</span></span> 
   
   ![Yeni->DataFactory](./media/data-factory-copy-data-wizard-tutorial/new-data-factory-menu.png)
2. <span data-ttu-id="97c2f-126">**Yeni data factory** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="97c2f-126">In the **New data factory** blade:</span></span>
   
   1. <span data-ttu-id="97c2f-127">**Ad** için **ADFTutorialDataFactory** girin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-127">Enter **ADFTutorialDataFactory** for the **name**.</span></span>
       <span data-ttu-id="97c2f-128">Azure veri fabrikasının adı genel olarak benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="97c2f-128">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="97c2f-129">`Data factory name “ADFTutorialDataFactory” is not available` hatasını alırsanız veri fabrikasının adını değiştirin (örneğin, yournameADFTutorialDataFactoryYYYYMMDD) ve yeniden oluşturmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-129">If you receive the error: `Data factory name “ADFTutorialDataFactory” is not available`, change the name of the data factory (for example, yournameADFTutorialDataFactoryYYYYMMDD) and try creating again.</span></span> <span data-ttu-id="97c2f-130">Data Factory yapıtlarının adlandırma kuralları için [Data Factory - Adlandırma Kuralları](data-factory-naming-rules.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-130">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>  
      
       ![Data Factory adı yok](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-not-available.png)    
   2. <span data-ttu-id="97c2f-132">Azure **aboneliğinizi** seçin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-132">Select your Azure **subscription**.</span></span>
   3. <span data-ttu-id="97c2f-133">Kaynak Grubu için aşağıdaki adımlardan birini uygulayın:</span><span class="sxs-lookup"><span data-stu-id="97c2f-133">For Resource Group, do one of the following steps:</span></span> 
      
      - <span data-ttu-id="97c2f-134">Var olan bir kaynak grubu seçmek için **Var olanı kullan**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-134">Select **Use existing** to select an existing resource group.</span></span>
      - <span data-ttu-id="97c2f-135">Bir kaynak grubunun adını girmek için **Yeni oluştur**’u seçin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-135">Select **Create new** to enter a name for a resource group.</span></span>
          
        <span data-ttu-id="97c2f-136">Bu öğreticideki adımlardan bazıları kaynak grubu için şu adı kullandığınızı varsayar: **ADFTutorialResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="97c2f-136">Some of the steps in this tutorial assume that you use the name: **ADFTutorialResourceGroup** for the resource group.</span></span> <span data-ttu-id="97c2f-137">Kaynak grupları hakkında daha fazla bilgi için bkz. [Azure kaynaklarınızı yönetmek için kaynak gruplarını kullanma](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="97c2f-137">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span>
   4. <span data-ttu-id="97c2f-138">Veri fabrikası için bir **konum** seçin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-138">Select a **location** for the data factory.</span></span>
   5. <span data-ttu-id="97c2f-139">Dikey pencerenin alt kısmındaki **Panoya sabitle** onay kutusunu seçin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-139">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>  
   6. <span data-ttu-id="97c2f-140">**Oluştur**’ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-140">Click **Create**.</span></span>
      
       ![Yeni veri fabrikası dikey penceresi](media/data-factory-copy-data-wizard-tutorial/new-data-factory-blade.png)            
3. <span data-ttu-id="97c2f-142">Oluşturma işlemi tamamlandıktan sonra, aşağıdaki görüntüde gösterildiği gibi **Data Factory** dikey penceresini görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="97c2f-142">After the creation is complete, you see the **Data Factory** blade as shown in the following image:</span></span>
   
   ![Data factory giriş sayfası](./media/data-factory-copy-data-wizard-tutorial/getstarted-data-factory-home-page.png)

## <a name="launch-copy-wizard"></a><span data-ttu-id="97c2f-144">Kopyalama Sihirbazı'nı başlatma</span><span class="sxs-lookup"><span data-stu-id="97c2f-144">Launch Copy Wizard</span></span>
1. <span data-ttu-id="97c2f-145">Data Factory dikey penceresinde **Veri kopyala [ÖNİZLEME]** öğesine tıklayarak **Kopyalama Sihirbazı**’nı başlatın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-145">On the Data Factory blade, click **Copy data [PREVIEW]** to launch the **Copy Wizard**.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="97c2f-146">Web tarayıcısının "Yetkilendiriliyor..." durumunda takıldığını görürseniz, tarayıcı ayarlarından **Üçüncü taraf tanımlama bilgilerini ve site verilerini engelle** ayarını devre dışı bırakın/ayarının işaretini kaldırın (veya) etkin durumda bırakıp **login.microsoftonline.com** için bir özel durum oluşturun ve ardından sihirbazı yeniden başlatmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-146">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting in the browser settings (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="97c2f-147">**Özellikler** sayfasında:</span><span class="sxs-lookup"><span data-stu-id="97c2f-147">In the **Properties** page:</span></span>
   
   1. <span data-ttu-id="97c2f-148">**Görev adı** için **CopyFromBlobToAzureSql** girin</span><span class="sxs-lookup"><span data-stu-id="97c2f-148">Enter **CopyFromBlobToAzureSql** for **Task name**</span></span>
   2. <span data-ttu-id="97c2f-149">**Açıklama** girin (isteğe bağlı).</span><span class="sxs-lookup"><span data-stu-id="97c2f-149">Enter **description** (optional).</span></span>
   3. <span data-ttu-id="97c2f-150">Bitiş tarihini bugüne, başlangıç tarihini ise beş gün öncesine ayarlayacak şekilde **Başlangıç tarihi ve saati** ile **Bitiş tarihi ve saati** değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-150">Change the **Start date time** and the **End date time** so that the end date is set to today and start date to five days earlier.</span></span>  
   4. <span data-ttu-id="97c2f-151">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-151">Click **Next**.</span></span>  
      
      ![Kopyalama Aracı - Özellikler sayfası](./media/data-factory-copy-data-wizard-tutorial/copy-tool-properties-page.png) 
3. <span data-ttu-id="97c2f-153">**Kaynak veri deposu** sayfasında **Azure Blob Storage** kutucuğuna tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-153">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="97c2f-154">Kopyalama görevine yönelik kaynak veri deposunu belirtmek için bu sayfayı kullanın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-154">You use this page to specify the source data store for the copy task.</span></span> 
   
    ![Kopyalama Aracı - Kaynak veri deposu sayfası](./media/data-factory-copy-data-wizard-tutorial/copy-tool-source-data-store-page.png)
4. <span data-ttu-id="97c2f-156">**Azure Blob depolama hesabı belirtin** sayfasında:</span><span class="sxs-lookup"><span data-stu-id="97c2f-156">On the **Specify the Azure Blob storage account** page:</span></span>
   
   1. <span data-ttu-id="97c2f-157">**Bağlı hizmet adı** için **AzureStorageLinkedService** girin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-157">Enter **AzureStorageLinkedService** for **Linked service name**.</span></span>
   2. <span data-ttu-id="97c2f-158">**Hesap seçme yöntemi** için **Azure aboneliklerinden** seçeneğinin belirlendiğini onaylayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-158">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="97c2f-159">Azure **aboneliğinizi** seçin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-159">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="97c2f-160">Seçili abonelikte bulunan Azure depolama hesapları listesinden bir **Azure depolama hesabı** seçin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-160">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="97c2f-161">Ayrıca **Hesap seçme yöntemi** için **El ile gir** öğesini seçip **İleri**’ye tıklayarak depolama hesabı ayarlarını el ile girmeyi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97c2f-161">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**, and then click **Next**.</span></span> 
      
      ![Kopyalama Aracı - Azure Blob depolama hesabı belirtin](./media/data-factory-copy-data-wizard-tutorial/copy-tool-specify-azure-blob-storage-account.png)
5. <span data-ttu-id="97c2f-163">**Girdi dosyası veya klasörü seçin** sayfasında:</span><span class="sxs-lookup"><span data-stu-id="97c2f-163">On **Choose the input file or folder** page:</span></span>
   
   1. <span data-ttu-id="97c2f-164">**adftutorial** seçeneğine (klasör) çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-164">Double-click **adftutorial** (folder).</span></span>
   2. <span data-ttu-id="97c2f-165">**emp.txt** dosyasını seçip **Seç** öğesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="97c2f-165">Select **emp.txt**, and click **Choose**</span></span>
      
      ![Kopyalama Aracı - Girdi dosyası veya klasörü seçin](./media/data-factory-copy-data-wizard-tutorial/copy-tool-choose-input-file-or-folder.png)
6. <span data-ttu-id="97c2f-167">**Girdi dosyası veya klasörü seçin** sayfasında **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-167">On the **Choose the input file or folder** page, click **Next**.</span></span> <span data-ttu-id="97c2f-168">**İkili kopya**’yı seçmeyin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-168">Do not select **Binary copy**.</span></span> 
   
    ![Kopyalama Aracı - Girdi dosyası veya klasörü seçin](./media/data-factory-copy-data-wizard-tutorial/chose-input-file-folder.png) 
7. <span data-ttu-id="97c2f-170">**Dosya biçimi ayarları** sayfasında sınırlayıcıları ve sihirbaz tarafından dosya ayrıştırılarak otomatik olarak algılanan düzeni görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="97c2f-170">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> <span data-ttu-id="97c2f-171">Kopyalama sihirbazının otomatik algılamasını durdurmak veya geçersiz kılmak için sınırlayıcıları el ile de girebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97c2f-171">You can also enter the delimiters manually for the copy wizard to stop auto-detecting or to override.</span></span> <span data-ttu-id="97c2f-172">Sınırlayıcıları gözden geçirin verilerin önizlemesini gördükten sonra **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-172">Click **Next** after you review the delimiters and preview data.</span></span> 
   
    ![Kopyalama Aracı - Dosya biçimi ayarları](./media/data-factory-copy-data-wizard-tutorial/copy-tool-file-format-settings.png)  
8. <span data-ttu-id="97c2f-174">Hedef veri deposu sayfasında **Azure SQL Veritabanı** öğesini ve **İleri**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-174">On the Destination data store page, select **Azure SQL Database**, and click **Next**.</span></span>
   
    ![Kopyalama Aracı - Hedef depo seçme](./media/data-factory-copy-data-wizard-tutorial/choose-destination-store.png)
9. <span data-ttu-id="97c2f-176">**Azure SQL veritabanı belirtin** sayfasında:</span><span class="sxs-lookup"><span data-stu-id="97c2f-176">On **Specify the Azure SQL database** page:</span></span>
   
   1. <span data-ttu-id="97c2f-177">**Bağlantı adı** için **AzureSqlLinkedService** girin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-177">Enter **AzureSqlLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="97c2f-178">**Sunucu / veritabanı seçme yöntemi** için **Azure aboneliklerinden** seçeneğinin belirlendiğini onaylayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-178">Confirm that **From Azure subscriptions** option is selected for **Server / database selection method**.</span></span>
   3. <span data-ttu-id="97c2f-179">Azure **aboneliğinizi** seçin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-179">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="97c2f-180">**Sunucu adı** ve **Veritabanı** öğelerini seçin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-180">Select **Server name** and **Database**.</span></span>
   5. <span data-ttu-id="97c2f-181">**Kullanıcı Adı** ve **Parola** girin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-181">Enter **User name** and **Password**.</span></span>
   6. <span data-ttu-id="97c2f-182">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-182">Click **Next**.</span></span>  
      
      ![Kopyalama Aracı - Azure SQL veritabanı belirtme](./media/data-factory-copy-data-wizard-tutorial/specify-azure-sql-database.png)
10. <span data-ttu-id="97c2f-184">**Tablo eşleme** sayfasında **Hedef** alanı için aşağı açılan listeden **emp** öğesini seçin, **aşağı oka** tıklayarak (isteğe bağlı) şemayı ve verilerin önizlemesini görün.</span><span class="sxs-lookup"><span data-stu-id="97c2f-184">On the **Table mapping** page, select **emp** for the **Destination** field from the drop-down list, click **down arrow** (optional) to see the schema and to preview the data.</span></span>
    
     ![Kopyalama Aracı - Tablo eşleme](./media/data-factory-copy-data-wizard-tutorial/copy-tool-table-mapping-page.png) 
11. <span data-ttu-id="97c2f-186">**Şema eşleme** sayfasında **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-186">On the **Schema mapping** page, click **Next**.</span></span>
    
    ![Kopyalama Aracı - düzen eşlemesi](./media/data-factory-copy-data-wizard-tutorial/schema-mapping-page.png)
12. <span data-ttu-id="97c2f-188">**Performans ayarları** sayfasında **İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-188">On the **Performance settings** page, click **Next**.</span></span> 
    
    ![Kopyalama Aracı - performans ayarları](./media/data-factory-copy-data-wizard-tutorial/performance-settings.png)
13. <span data-ttu-id="97c2f-190">**Özet** sayfasındaki bilgileri gözden geçirin ve **Son**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-190">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="97c2f-191">Sihirbaz, veri fabrikasında (Kopyalama Sihirbazı’nı başlattığınız yer) iki bağlı hizmet, iki veri kümesi (girdi ve çıktı) ve bir işlem hattı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="97c2f-191">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span> 
    
    ![Kopyalama Aracı - performans ayarları](./media/data-factory-copy-data-wizard-tutorial/summary-page.png)

## <a name="launch-monitor-and-manage-application"></a><span data-ttu-id="97c2f-193">Uygulama İzleme ve Yönetmeyi başlatma</span><span class="sxs-lookup"><span data-stu-id="97c2f-193">Launch Monitor and Manage application</span></span>
1. <span data-ttu-id="97c2f-194">**Dağıtım** sayfasında, şu bağlantıya tıklayın: `Click here to monitor copy pipeline`.</span><span class="sxs-lookup"><span data-stu-id="97c2f-194">On the **Deployment** page, click the link: `Click here to monitor copy pipeline`.</span></span>
   
   ![Kopyalama Aracı - Dağıtım başarılı](./media/data-factory-copy-data-wizard-tutorial/copy-tool-deployment-succeeded.png)  
2. <span data-ttu-id="97c2f-196">İzleme uygulaması, web tarayıcınızdaki ayrı bir sekmede başlatılır.</span><span class="sxs-lookup"><span data-stu-id="97c2f-196">The monitoring application is launched in a separate tab in your web browser.</span></span>   
   
   ![İzleme Uygulaması](./media/data-factory-copy-data-wizard-tutorial/monitoring-app.png)   
3. <span data-ttu-id="97c2f-198">Saatlik dilimlerin en son durumu görmek için alt kısımdaki **ETKİNLİK PENCERELERİ** listesinde **Yenile** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-198">To see the latest status of hourly slices, click **Refresh** button in the **ACTIVITY WINDOWS** list at the bottom.</span></span> <span data-ttu-id="97c2f-199">İşlem hattının başlangıç ve bitiş saatleri arasındaki beş gün için beş etkinlik görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="97c2f-199">You see five activity windows for five days between start and end times for the pipeline.</span></span> <span data-ttu-id="97c2f-200">Liste otomatik olarak yenilenmez. Bu nedenle, tüm etkinlik pencerelerini Hazır durumunda görebilmeniz için Yenile düğmesine birkaç kez tıklamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="97c2f-200">The list is not automatically refreshed, so you may need to click Refresh a couple of times before you see all the activity windows in the Ready state.</span></span> 
4. <span data-ttu-id="97c2f-201">Listeden bir etkinlik penceresi seçin.</span><span class="sxs-lookup"><span data-stu-id="97c2f-201">Select an activity window in the list.</span></span> <span data-ttu-id="97c2f-202">Ayrıntılarını sağ taraftaki **Etkinlik Penceresi Gezgini**’nde görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97c2f-202">See the details about it in the **Activity Window Explorer** on the right.</span></span>

    ![Etkinlik penceresi ayrıntıları](media/data-factory-copy-data-wizard-tutorial/activity-window-details.png)    

    <span data-ttu-id="97c2f-204">11, 12, 13, 14 ve 15 tarihlerinin yeşil renkli olduğuna dikkat edin; yeşil renk, bu tarihlerin günlük çıktı dilimlerinin zaten oluşturulduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="97c2f-204">Notice that the dates 11, 12, 13, 14, and 15 are in green color, which means that the daily output slices for these dates have already been produced.</span></span> <span data-ttu-id="97c2f-205">Bu renk kodlamasını, diyagram görünümünde işlem hattı ve çıktı veri kümesinde de görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="97c2f-205">You also see this color coding on the pipeline and the output dataset in the diagram view.</span></span> <span data-ttu-id="97c2f-206">Önceki adımda, iki dilimin zaten oluşturulduğuna, bir dilimin o anda işlenmekte olduğuna ve diğer ikisinin işlenmeyi beklediğine dikkat edin (renk kodlamasına göre).</span><span class="sxs-lookup"><span data-stu-id="97c2f-206">In the previous step, notice that two slices have already been produced, one slice is currently being processed, and the other two are waiting to be processed (based on the color coding).</span></span> 

    <span data-ttu-id="97c2f-207">Bu uygulamayı kullanma hakkında daha fazla bilgi için [İzleme Uygulamasını kullanarak işlem hattını izleme ve yönetme](data-factory-monitor-manage-app.md) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-207">For more information on using this application, see [Monitor and manage pipeline using Monitoring App](data-factory-monitor-manage-app.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97c2f-208">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="97c2f-208">Next steps</span></span>
<span data-ttu-id="97c2f-209">Bu öğreticide, bir kopyalama işleminde kaynak veri deposu olarak Azure blob depolama alanını ve hedef veri deposu olarak Azure SQL veritabanını kullandınız.</span><span class="sxs-lookup"><span data-stu-id="97c2f-209">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="97c2f-210">Aşağıdaki tabloda, kopyalama etkinliği tarafından kaynaklar ve hedefler olarak desteklenen veri depolarının listesi sağlanmıştır:</span><span class="sxs-lookup"><span data-stu-id="97c2f-210">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="97c2f-211">Bir veri deposu için kopyalama sihirbazında gördüğünüz alanlar/özellikler hakkında bilgi için tablodaki veri deposu bağlantısına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="97c2f-211">For details about fields/properties that you see in the copy wizard for a data store, click the link for the data store in the table.</span></span> 