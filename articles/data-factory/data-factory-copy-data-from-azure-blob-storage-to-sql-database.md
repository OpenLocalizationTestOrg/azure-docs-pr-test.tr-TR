---
title: "Blob Storage tooSQL veritabanı - Azure aaaCopy verilerden | Microsoft Docs"
description: "Bu öğretici nasıl toouse bir Azure Data Factory kopyalama etkinliği kanal Blob Depolama tooSQL veritabanındaki toocopy verileri gösterir."
keywords: BLOB sql, blob depolama, veri kopyalama
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e4035060-93bf-4e8d-bf35-35e2d15c51e0
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: spelluru
ms.openlocfilehash: a2c3fb8a4ddd63b0b6b3e75903b7a7eaf188fda4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-copy-data-from-blob-storage-toosql-database-using-data-factory"></a><span data-ttu-id="a7323-104">Öğretici: Data Factory kullanarak veritabanı Blob Storage tooSQL veri kopyalama</span><span class="sxs-lookup"><span data-stu-id="a7323-104">Tutorial: Copy data from Blob Storage tooSQL Database using Data Factory</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7323-105">Genel bakış ve önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a7323-105">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="a7323-106">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="a7323-106">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="a7323-107">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a7323-107">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="a7323-108">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a7323-108">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="a7323-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7323-109">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="a7323-110">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="a7323-110">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="a7323-111">REST API</span><span class="sxs-lookup"><span data-stu-id="a7323-111">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="a7323-112">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="a7323-112">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="a7323-113">Bu öğreticide, Blob Depolama tooSQL veritabanından bir ardışık düzen toocopy verilerle bir veri fabrikası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a7323-113">In this tutorial, you create a data factory with a pipeline toocopy data from Blob storage tooSQL database.</span></span>

<span data-ttu-id="a7323-114">Merhaba kopya etkinliği Azure Data Factory'de hello veri taşımayı gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="a7323-114">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="a7323-115">Bu etkinlik, çeşitli veri depolama alanları arasında güvenli, güvenilir ve ölçeklenebilir bir yolla veri kopyalayabilen genel olarak kullanılabilir bir hizmet tarafından desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a7323-115">It is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="a7323-116">Bkz: [veri taşıma etkinlikleri](data-factory-data-movement-activities.md) makale hello kopyalama etkinliği hakkında ayrıntılı bilgi için.</span><span class="sxs-lookup"><span data-stu-id="a7323-116">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>  

> [!NOTE]
> <span data-ttu-id="a7323-117">Merhaba hello Data Factory hizmetinin ayrıntılı bir genel bakış için bkz [giriş tooAzure Data Factory](data-factory-introduction.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="a7323-117">For a detailed overview of hello Data Factory service, see hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article.</span></span>
>
>

## <a name="prerequisites-for-hello-tutorial"></a><span data-ttu-id="a7323-118">Başlangıç öğreticisi için Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a7323-118">Prerequisites for hello tutorial</span></span>
<span data-ttu-id="a7323-119">Bu öğreticiye başlamadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a7323-119">Before you begin this tutorial, you must have hello following prerequisites:</span></span>

* <span data-ttu-id="a7323-120">**Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="a7323-120">**Azure subscription**.</span></span>  <span data-ttu-id="a7323-121">Bir aboneliğiniz yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7323-121">If you don't have a subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a7323-122">Merhaba bkz [ücretsiz deneme](http://azure.microsoft.com/pricing/free-trial/) Ayrıntılar için makale.</span><span class="sxs-lookup"><span data-stu-id="a7323-122">See hello [Free Trial](http://azure.microsoft.com/pricing/free-trial/) article for details.</span></span>
* <span data-ttu-id="a7323-123">**Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="a7323-123">**Azure Storage Account**.</span></span> <span data-ttu-id="a7323-124">Merhaba blob depolama alanı olarak kullandığınız bir **kaynak** verileri depolamak Bu öğreticide.</span><span class="sxs-lookup"><span data-stu-id="a7323-124">You use hello blob storage as a **source** data store in this tutorial.</span></span> <span data-ttu-id="a7323-125">bir Azure depolama hesabınız yoksa, hello bkz [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account) adımları toocreate bir makale.</span><span class="sxs-lookup"><span data-stu-id="a7323-125">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
* <span data-ttu-id="a7323-126">**Azure SQL veritabanı**.</span><span class="sxs-lookup"><span data-stu-id="a7323-126">**Azure SQL Database**.</span></span> <span data-ttu-id="a7323-127">Bir Azure SQL veritabanı olarak kullandığınız bir **hedef** verileri depolamak Bu öğreticide.</span><span class="sxs-lookup"><span data-stu-id="a7323-127">You use an Azure SQL database as a **destination** data store in this tutorial.</span></span> <span data-ttu-id="a7323-128">Merhaba öğretici, bkz: kullanabileceğiniz bir Azure SQL veritabanı yoksa [nasıl toocreate ve bir Azure SQL veritabanı yapılandırma](../sql-database/sql-database-get-started.md) toocreate biri.</span><span class="sxs-lookup"><span data-stu-id="a7323-128">If you don't have an Azure SQL database that you can use in hello tutorial, See [How toocreate and configure an Azure SQL Database](../sql-database/sql-database-get-started.md) toocreate one.</span></span>
* <span data-ttu-id="a7323-129">**SQL Server 2012/2014 veya Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="a7323-129">**SQL Server 2012/2014 or Visual Studio 2013**.</span></span> <span data-ttu-id="a7323-130">Merhaba veritabanında SQL Server Management Studio veya Visual Studio toocreate bir örnek veritabanı ve tooview hello sonuç verileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a7323-130">You use SQL Server Management Studio or Visual Studio toocreate a sample database and tooview hello result data in hello database.</span></span>  

## <a name="collect-blob-storage-account-name-and-key"></a><span data-ttu-id="a7323-131">BLOB Depolama hesabı adı ve anahtar Topla</span><span class="sxs-lookup"><span data-stu-id="a7323-131">Collect blob storage account name and key</span></span>
<span data-ttu-id="a7323-132">Merhaba hesap adını ve hesap anahtarını, Azure depolama hesabı toodo Bu öğretici gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7323-132">You need hello account name and account key of your Azure storage account toodo this tutorial.</span></span> <span data-ttu-id="a7323-133">Aşağı Not **hesap adı** ve **hesap anahtarı** Azure depolama hesabınız için.</span><span class="sxs-lookup"><span data-stu-id="a7323-133">Note down **account name** and **account key** for your Azure storage account.</span></span>

1. <span data-ttu-id="a7323-134">İçinde toohello oturum [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a7323-134">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="a7323-135">Tıklatın **daha fazla hizmet** sol menü ve select hello üzerinde **depolama hesapları**.</span><span class="sxs-lookup"><span data-stu-id="a7323-135">Click **More services** on hello left menu and select **Storage Accounts**.</span></span>

    ![Gözat - depolama hesapları](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/browse-storage-accounts.png)
3. <span data-ttu-id="a7323-137">Merhaba, **depolama hesapları** dikey penceresinde, select hello **Azure depolama hesabı** Bu öğreticide toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="a7323-137">In hello **Storage Accounts** blade, select hello **Azure storage account** that you want toouse in this tutorial.</span></span>
4. <span data-ttu-id="a7323-138">Seçin **erişim anahtarları** altında bağlantı **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a7323-138">Select **Access keys** link under **SETTINGS**.</span></span>
5. <span data-ttu-id="a7323-139">Tıklatın **kopya** (görüntü) sonraki çok düğmesini**depolama hesabı adı** metin kutusuna ve kaydetme/bunu herhangi bir yerde Yapıştır (örneğin: bir metin dosyasındaki).</span><span class="sxs-lookup"><span data-stu-id="a7323-139">Click **copy** (image) button next too**Storage account name** text box and save/paste it somewhere (for example: in a text file).</span></span>
6. <span data-ttu-id="a7323-140">Merhaba önceki adım toocopy veya hello Not yineleyin **key1**.</span><span class="sxs-lookup"><span data-stu-id="a7323-140">Repeat hello previous step toocopy or note down hello **key1**.</span></span>

    ![Depolama erişim tuşu](media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/storage-access-key.png)
7. <span data-ttu-id="a7323-142">Tüm hello dikey tıklayarak kapatın **X**.</span><span class="sxs-lookup"><span data-stu-id="a7323-142">Close all hello blades by clicking **X**.</span></span>

## <a name="collect-sql-server-database-user-names"></a><span data-ttu-id="a7323-143">SQL server, veritabanı, kullanıcı adları Topla</span><span class="sxs-lookup"><span data-stu-id="a7323-143">Collect SQL server, database, user names</span></span>
<span data-ttu-id="a7323-144">Bu öğreticide Azure SQL server, veritabanı ve kullanıcı toodo hello adlarını gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7323-144">You need hello names of Azure SQL server, database, and user toodo this tutorial.</span></span> <span data-ttu-id="a7323-145">Adlarını Not **server**, **veritabanı**, ve **kullanıcı** Azure SQL veritabanı.</span><span class="sxs-lookup"><span data-stu-id="a7323-145">Note down names of **server**, **database**, and **user** for your Azure SQL database.</span></span>

1. <span data-ttu-id="a7323-146">Merhaba, **Azure portal**, tıklatın **daha fazla hizmet** hello seçin ve sol üzerinde **SQL veritabanları**.</span><span class="sxs-lookup"><span data-stu-id="a7323-146">In hello **Azure portal**, click **More services** on hello left and select **SQL databases**.</span></span>
2. <span data-ttu-id="a7323-147">Merhaba, **SQL veritabanları dikey**seçin hello **veritabanı** Bu öğreticide toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="a7323-147">In hello **SQL databases blade**, select hello **database** that you want toouse in this tutorial.</span></span> <span data-ttu-id="a7323-148">Merhaba Not **veritabanı adı**.</span><span class="sxs-lookup"><span data-stu-id="a7323-148">Note down hello **database name**.</span></span>  
3. <span data-ttu-id="a7323-149">Merhaba, **SQL veritabanı** dikey penceresinde tıklatın **özellikleri** altında **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a7323-149">In hello **SQL database** blade, click **Properties** under **SETTINGS**.</span></span>
4. <span data-ttu-id="a7323-150">Merhaba değerlerini Not **sunucu adı** ve **Sunucu Yöneticisi oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="a7323-150">Note down hello values for **SERVER NAME** and **SERVER ADMIN LOGIN**.</span></span>
5. <span data-ttu-id="a7323-151">Tüm hello dikey tıklayarak kapatın **X**.</span><span class="sxs-lookup"><span data-stu-id="a7323-151">Close all hello blades by clicking **X**.</span></span>

## <a name="allow-azure-services-tooaccess-sql-server"></a><span data-ttu-id="a7323-152">Azure Hizmetleri tooaccess SQL server izin ver</span><span class="sxs-lookup"><span data-stu-id="a7323-152">Allow Azure services tooaccess SQL server</span></span>
<span data-ttu-id="a7323-153">Emin **tooAzure Hizmetleri erişimine izin** açık ayarı **ON** bu hello Data Factory hizmeti Azure SQL sunucunuza erişebilmesi için Azure SQL sunucunuzun.</span><span class="sxs-lookup"><span data-stu-id="a7323-153">Ensure that **Allow access tooAzure services** setting turned **ON** for your Azure SQL server so that hello Data Factory service can access your Azure SQL server.</span></span> <span data-ttu-id="a7323-154">tooverify ve bu ayarı etkinleştirin adımları izleyerek hello:</span><span class="sxs-lookup"><span data-stu-id="a7323-154">tooverify and turn on this setting, do hello following steps:</span></span>

1. <span data-ttu-id="a7323-155">Tıklatın **daha fazla hizmet** hello solda ve tıklatın hub **SQL sunucuları**.</span><span class="sxs-lookup"><span data-stu-id="a7323-155">Click **More services** hub on hello left and click **SQL servers**.</span></span>
2. <span data-ttu-id="a7323-156">Sunucunuzu seçin ve tıklayın **Güvenlik Duvarı** altında **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a7323-156">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
3. <span data-ttu-id="a7323-157">Merhaba, **Güvenlik Duvarı ayarları** dikey penceresinde tıklatın **ON** için **tooAzure Hizmetleri erişimine izin**.</span><span class="sxs-lookup"><span data-stu-id="a7323-157">In hello **Firewall settings** blade, click **ON** for **Allow access tooAzure services**.</span></span>
4. <span data-ttu-id="a7323-158">Tüm hello dikey tıklayarak kapatın **X**.</span><span class="sxs-lookup"><span data-stu-id="a7323-158">Close all hello blades by clicking **X**.</span></span>

## <a name="prepare-blob-storage-and-sql-database"></a><span data-ttu-id="a7323-159">BLOB Storage ve SQL veritabanı hazırlayın</span><span class="sxs-lookup"><span data-stu-id="a7323-159">Prepare Blob Storage and SQL Database</span></span>
<span data-ttu-id="a7323-160">Şimdi, Azure blob depolama ve Azure SQL veritabanı için başlangıç Öğreticisi hello aşağıdaki adımları gerçekleştirerek hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="a7323-160">Now, prepare your Azure blob storage and Azure SQL database for hello tutorial by performing hello following steps:</span></span>  

1. <span data-ttu-id="a7323-161">Not Defteri'ni başlatın.</span><span class="sxs-lookup"><span data-stu-id="a7323-161">Launch Notepad.</span></span> <span data-ttu-id="a7323-162">Metin aşağıdaki hello kopyalayın ve olarak kaydedin **emp.txt** çok**C:\ADFGetStarted** sabit diskinizde klasör.</span><span class="sxs-lookup"><span data-stu-id="a7323-162">Copy hello following text and save it as **emp.txt** too**C:\ADFGetStarted** folder on your hard drive.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
2. <span data-ttu-id="a7323-163">Gibi araçlar kullanın [Azure Storage Gezgini](http://storageexplorer.com/) toocreate hello **adftutorial** kapsayıcı ve tooupload hello **emp.txt** dosya toohello kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a7323-163">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate hello **adftutorial** container and tooupload hello **emp.txt** file toohello container.</span></span>

    ![Azure Storage Gezgini.](./media/data-factory-copy-data-from-azure-blob-storage-to-sql-database/getstarted-storage-explorer.png)
3. <span data-ttu-id="a7323-166">Aşağıdaki SQL komut dosyası toocreate hello kullan hello **emp** Azure SQL veritabanı tablosunda.</span><span class="sxs-lookup"><span data-stu-id="a7323-166">Use hello following SQL script toocreate hello **emp** table in your Azure SQL Database.</span></span>  

    ```SQL
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50),
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

    <span data-ttu-id="a7323-167">**SQL Server 2012/2014 bilgisayarınızda yüklü olup olmadığını:** makalesindeki yönergeleri izleyin [Azure SQL SQL Server Management Studio'yu kullanarak veritabanı yönetme](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server ve Çalıştır hello SQL komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="a7323-167">**If you have SQL Server 2012/2014 installed on your computer:** follow instructions from [Managing Azure SQL Database using SQL Server Management Studio](../sql-database/sql-database-manage-azure-ssms.md) tooconnect tooyour Azure SQL server and run hello SQL script.</span></span> <span data-ttu-id="a7323-168">Bu makalede hello kullanan [Klasik Azure portalı](http://manage.windowsazure.com), değil hello [yeni Azure portalına](https://portal.azure.com), bir Azure SQL server için Güvenlik Duvarı'nı tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="a7323-168">This article uses hello [classic Azure portal](http://manage.windowsazure.com), not hello [new Azure portal](https://portal.azure.com), tooconfigure firewall for an Azure SQL server.</span></span>

    <span data-ttu-id="a7323-169">İstemci tooaccess hello Azure SQL server izin verilmiyorsa tooconfigure Güvenlik Duvarı'nı makinenizden (IP adresi), Azure SQL sunucusu tooallow erişimi için gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7323-169">If your client is not allowed tooaccess hello Azure SQL server, you need tooconfigure firewall for your Azure SQL server tooallow access from your machine (IP Address).</span></span> <span data-ttu-id="a7323-170">Bkz: [bu makalede](../sql-database/sql-database-configure-firewall-settings.md) adımları tooconfigure hello Azure SQL server için Güvenlik Duvarı için.</span><span class="sxs-lookup"><span data-stu-id="a7323-170">See [this article](../sql-database/sql-database-configure-firewall-settings.md) for steps tooconfigure hello firewall for your Azure SQL server.</span></span>

## <a name="create-a-data-factory"></a><span data-ttu-id="a7323-171">Veri fabrikası oluşturma</span><span class="sxs-lookup"><span data-stu-id="a7323-171">Create a data factory</span></span>
<span data-ttu-id="a7323-172">Merhaba Önkoşullar tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="a7323-172">You have completed hello prerequisites.</span></span> <span data-ttu-id="a7323-173">Aşağıdaki şekilde hello birini kullanarak bir veri fabrikası oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7323-173">You can create a data factory using one of hello following ways.</span></span> <span data-ttu-id="a7323-174">Merhaba üst veya bağlantılar tooperform hello öğreticiyi izleyerek hello hello aşağı açılan listesinde hello seçeneklerden birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a7323-174">Click one of hello options in hello drop-down list at hello top or hello following links tooperform hello tutorial.</span></span>     

* [<span data-ttu-id="a7323-175">Kopyalama Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="a7323-175">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
* [<span data-ttu-id="a7323-176">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a7323-176">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
* [<span data-ttu-id="a7323-177">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a7323-177">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
* [<span data-ttu-id="a7323-178">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7323-178">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
* [<span data-ttu-id="a7323-179">Azure Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="a7323-179">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
* [<span data-ttu-id="a7323-180">REST API</span><span class="sxs-lookup"><span data-stu-id="a7323-180">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
* [<span data-ttu-id="a7323-181">.NET API’si</span><span class="sxs-lookup"><span data-stu-id="a7323-181">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

> [!NOTE]
> <span data-ttu-id="a7323-182">Merhaba veri ardışık Bu öğreticide, bir kaynak veri deposu tooa hedef veri deposundan verileri kopyalar.</span><span class="sxs-lookup"><span data-stu-id="a7323-182">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="a7323-183">Giriş verisi tooproduce çıktı verilerini dönüştürmez.</span><span class="sxs-lookup"><span data-stu-id="a7323-183">It does not transform input data tooproduce output data.</span></span> <span data-ttu-id="a7323-184">Nasıl bir öğretici için Azure Data Factory kullanarak tootransform verileri görmek [Öğreticisi: Hadoop kümesi kullanarak ilk ardışık düzen tootransform verilerinizi yapı](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="a7323-184">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build your first pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>
> 
> <span data-ttu-id="a7323-185">Merhaba çıkış veri kümesi bir etkinlik hello hello dataset diğer etkinlik girişi olarak ayarlayarak (bir etkinlik sonra başka bir Çalıştır) iki etkinlik zincir.</span><span class="sxs-lookup"><span data-stu-id="a7323-185">You can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="a7323-186">Ayrıntılı bilgi için bkz. [Data Factory’de zamanlama ve yürütme](data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="a7323-186">See [Scheduling and execution in Data Factory](data-factory-scheduling-and-execution.md) for detailed information.</span></span> 
