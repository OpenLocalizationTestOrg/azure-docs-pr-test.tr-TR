---
title: "Azure SQL veri ambarı – Data Factory aaaLoad verisine | Microsoft Docs"
description: "Bu öğreticide Azure Data Factory kullanarak Azure SQL Data Warehouse'a veri yükler ve hello veri kaynağı olarak bir SQL Server veritabanını kullanır."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="728df-103">Data Factory ile SQL veri ambarına veri yükleme</span><span class="sxs-lookup"><span data-stu-id="728df-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="728df-104">Azure SQL veri ambarında herhangi birinden hello Azure Data Factory tooload verileri kullanabilirsiniz [desteklenen kaynak veri depoları](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="728df-104">You can use Azure Data Factory tooload data into Azure SQL Data Warehouse from any of hello [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="728df-105">Örneğin, verileri Azure SQL veritabanına veya bir Oracle veritabanından bir SQL data warehouse'a veri fabrikası kullanarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="728df-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="728df-106">Bu makalede öğreticide SQL data warehouse'a nasıl tooload verilerden bir şirket içi SQL Server veritabanı gösterir.</span><span class="sxs-lookup"><span data-stu-id="728df-106">Tutorial in this article shows you how tooload data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="728df-107">**Zaman tahmin**: hello Önkoşullar sağlandığında, Bu öğretici hakkında 10-15 dakika toocomplete gösterir.</span><span class="sxs-lookup"><span data-stu-id="728df-107">**Time estimate**: This tutorial takes about 10-15 minutes toocomplete once hello prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="728df-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="728df-108">Prerequisites</span></span>

- <span data-ttu-id="728df-109">Gereksinim duyduğunuz bir **SQL Server veritabanı** hello verileri içeren tablolarla toobe toohello SQL veri ambarı kopyalanır.</span><span class="sxs-lookup"><span data-stu-id="728df-109">You need a **SQL Server database** with tables that contain hello data toobe copied over toohello SQL data warehouse.</span></span>  

- <span data-ttu-id="728df-110">Çevrimiçi ihtiyacınız **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="728df-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="728df-111">Veri ambarı zaten yoksa, nasıl çok öğrenin[bir Azure SQL Data Warehouse oluşturma](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="728df-111">If you do not already have a data warehouse, learn how too[Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="728df-112">Gereksinim duyduğunuz bir **Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="728df-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="728df-113">Bir depolama hesabı zaten yoksa, nasıl çok öğrenin[depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="728df-113">If you do not already have a storage account, learn how too[Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="728df-114">En iyi performans için hello depolama hesabını bulun ve hello veri ambarı hello aynı Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="728df-114">For best performance, locate hello storage account and hello data warehouse in hello same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="728df-115">Data factory Yapılandır</span><span class="sxs-lookup"><span data-stu-id="728df-115">Configure a data factory</span></span>
1. <span data-ttu-id="728df-116">İçinde toohello oturum [Azure portal][].</span><span class="sxs-lookup"><span data-stu-id="728df-116">Log in toohello [Azure portal][].</span></span>
2. <span data-ttu-id="728df-117">Veri ambarınız bulun ve tooopen tıklatın.</span><span class="sxs-lookup"><span data-stu-id="728df-117">Locate your data warehouse and click tooopen it.</span></span>
3. <span data-ttu-id="728df-118">Merhaba ana dikey penceresinde tıklayın **veri yükleme** > **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="728df-118">In hello main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Veri Yükleme Sihirbazını Başlat](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="728df-120">Azure aboneliğinizde bir veri fabrikası yoksa gördüğünüz bir **yeni Data Factory** hello tarayıcısının ayrı bir sekmede iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="728df-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of hello browser.</span></span> <span data-ttu-id="728df-121">Merhaba doldurun istenen bilgilerin öğesini tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="728df-121">Fill in hello requested information, and click **Create**.</span></span> <span data-ttu-id="728df-122">Merhaba veri fabrikası oluşturulduktan sonra hello **yeni Data Factory** iletişim kutusunu kapatır ve hello bkz **seçin Data Factory** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="728df-122">After hello data factory is created, hello **New Data Factory** dialog box closes, and you see hello **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="728df-123">Bir veya daha fazla data factory'leri zaten hello Azure aboneliği varsa hello bkz **seçin Data Factory** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="728df-123">If you have one or more data factories already in hello Azure subscription, you see hello **Select Data Factory** dialog box.</span></span> <span data-ttu-id="728df-124">Bu iletişim kutusunda, mevcut bir veri fabrikasını seçin veya tıklatın **oluştur yeni data factory** toocreate yeni bir tane.</span><span class="sxs-lookup"><span data-stu-id="728df-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** toocreate a new one.</span></span>

    ![Veri Fabrikası yapılandırın](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="728df-126">Merhaba, **seçin Data Factory** iletişim kutusu, hello **veri yükleme** seçeneği, varsayılan olarak seçilidir.</span><span class="sxs-lookup"><span data-stu-id="728df-126">In hello **Select Data Factory** dialog box, hello **Load data** option is selected by default.</span></span> <span data-ttu-id="728df-127">Tıklatın **sonraki** toostart veri görev yükleme oluşturma.</span><span class="sxs-lookup"><span data-stu-id="728df-127">Click **Next** toostart creating a data loading task.</span></span>

## <a name="configure-hello-data-factory-properties"></a><span data-ttu-id="728df-128">Merhaba veri fabrikası özelliklerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="728df-128">Configure hello data factory properties</span></span>
<span data-ttu-id="728df-129">Veri Fabrikası oluşturduğunuza göre hello sonraki adıma Zamanlama yüklenirken tooconfigure hello verilerdir.</span><span class="sxs-lookup"><span data-stu-id="728df-129">Now that you have created a data factory, hello next step is tooconfigure hello data loading schedule.</span></span>

1. <span data-ttu-id="728df-130">İçin **görev adı**, girin **DWLoadData fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="728df-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="728df-131">Merhaba varsayılan kullanmak **kez Şimdi Çalıştır** seçeneği, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="728df-131">Use hello default **Run once now** option, click **Next**.</span></span>

    ![Yükleme zamanlamasını yapılandırın](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a><span data-ttu-id="728df-133">Merhaba kaynak veri deposu ve ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="728df-133">Configure hello source data store and gateway</span></span>
<span data-ttu-id="728df-134">Şimdi veri fabrikası hello şirket içi SQL Server veritabanı tooload veri istediğiniz hakkında söyleyin.</span><span class="sxs-lookup"><span data-stu-id="728df-134">Now you tell Data Factory about hello on-premises SQL Server database from which you want tooload data.</span></span>

1. <span data-ttu-id="728df-135">Seçin **SQL Server** desteklenen hello kaynak verilerinden katalog depolamak ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="728df-135">Choose **SQL Server** from hello supported source data store catalog, and click **Next**.</span></span>

    ![SQL Server kaynak seçin](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="728df-137">A **belirt hello şirket içi SQL Server veritabanı** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="728df-137">A **Specify hello on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="728df-138">ilk hello **bağlantı adı** doldurulmuş otomatik bir alandır.</span><span class="sxs-lookup"><span data-stu-id="728df-138">hello first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="728df-139">Merhaba ikinci alan ister hello hello adını **ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="728df-139">hello second field asks for hello name of hello **Gateway**.</span></span> <span data-ttu-id="728df-140">Bir ağ geçidi zaten mevcut bir veri fabrikasını kullanıyorsanız, hello aşağı açılan listeden seçerek hello ağ geçidi yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="728df-140">If you are using an existing data factory that already has a gateway, you can reuse hello gateway by selecting it from hello drop-down list.</span></span> <span data-ttu-id="728df-141">Merhaba tıklatın **ağ geçidi Oluştur** toocreate veri yönetimi ağ geçidi bağlantı.</span><span class="sxs-lookup"><span data-stu-id="728df-141">Click hello **Create Gateway** link toocreate a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="728df-142">Merhaba kaynak veri deposu, şirket içi veya bir Azure Iaas sanal makinesi veri yönetimi ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="728df-142">If hello source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="728df-143">Bir ağ geçidi, veri fabrikası bir 1-1 ilişkisi yok.</span><span class="sxs-lookup"><span data-stu-id="728df-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="728df-144">Başka bir veri fabrikası'ndan kullanılamaz, ancak birden çok veri hello görevlerle yükleme tarafından kullanılabilir aynı veri fabrikası.</span><span class="sxs-lookup"><span data-stu-id="728df-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in hello same data factory.</span></span> <span data-ttu-id="728df-145">Bir ağ geçidi, veri görevleri yükleme çalıştırırken kullanılan tooconnect toomultiple veri depolarına olabilir.</span><span class="sxs-lookup"><span data-stu-id="728df-145">A gateway can be used tooconnect toomultiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="728df-146">Merhaba ağ geçidi hakkında ayrıntılı bilgi için bkz: [veri yönetimi ağ geçidi](../data-factory/data-factory-data-management-gateway.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="728df-146">For detailed information about hello gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="728df-147">A **ağ geçidi Oluştur** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="728df-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="728df-148">Adı **GatewayForDWLoading**, tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="728df-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="728df-149">A **yapılandırma ağ geçidi** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="728df-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="728df-150">Tıklatın **başlatma hızlı kurulum bu bilgisayarda** tooautomatically indirme, yükleme ve veri yönetimi ağ geçidi geçerli makinenize kaydedin.</span><span class="sxs-lookup"><span data-stu-id="728df-150">Click **Launch express setup on this computer** tooautomatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="728df-151">Merhaba ilerleme açılır pencerede gösterilir.</span><span class="sxs-lookup"><span data-stu-id="728df-151">hello progress is shown in a pop-up window.</span></span> <span data-ttu-id="728df-152">Merhaba makine toohello veri deposuna bağlanamazsa, el ile denetleyebilirsiniz [hello ağ geçidi yükleyip](https://www.microsoft.com/download/details.aspx?id=39717) toohello veri bağlanabilir bir makinede depolayın ve sonra hello anahtar tooregister kullanın.</span><span class="sxs-lookup"><span data-stu-id="728df-152">If hello machine cannot connect toohello data store, you can manually [download and install hello gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect toohello data store, and then use hello key tooregister.</span></span>
    > [!NOTE]
    > <span data-ttu-id="728df-153">Merhaba hızlı kurulumu, Microsoft Edge ve Internet Explorer ile yerel olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="728df-153">hello express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="728df-154">İlk Google Chrome kullanıyorsanız, hello ClickOnce uzantı Chrome web Mağazası'ndan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="728df-154">If you are using Google Chrome, first install hello ClickOnce extension from Chrome web store.</span></span>

    ![Hızlı Kurulum başlatma](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="728df-156">Merhaba ağ geçidi Kurulum toocomplete bekleyin.</span><span class="sxs-lookup"><span data-stu-id="728df-156">Wait for hello gateway setup toocomplete.</span></span> <span data-ttu-id="728df-157">Merhaba ağ geçidi başarıyla kaydedildi ve çevrimiçi sonra hello açılır penceresi kapanır ve hello yeni ağ geçidi hello ağ geçidi alanında görünür.</span><span class="sxs-lookup"><span data-stu-id="728df-157">Once hello gateway is successfully registered and is online, hello pop-up window closes and hello new gateway appears in hello gateway field.</span></span> <span data-ttu-id="728df-158">Ardından hello rest doldurun gibi gerekli alanları, ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="728df-158">Then fill in hello rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="728df-159">**Sunucu adı**: hello adını şirket içi SQL Server.</span><span class="sxs-lookup"><span data-stu-id="728df-159">**Server name**: Name of hello on-premises SQL Server.</span></span>
    - <span data-ttu-id="728df-160">**Veritabanı adı**: SQL Server veritabanı.</span><span class="sxs-lookup"><span data-stu-id="728df-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="728df-161">**Kimlik bilgisi şifreleme**: "web tarayıcısı tarafından" Merhaba varsayılan kullanın.</span><span class="sxs-lookup"><span data-stu-id="728df-161">**Credential encryption**: Use hello default "By web browser".</span></span>
    - <span data-ttu-id="728df-162">**Kimlik doğrulama türü**: hello kullanmakta olduğunuz kimlik doğrulama türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="728df-162">**Authentication type**: Choose hello type of authentication you are using.</span></span>
    - <span data-ttu-id="728df-163">**Kullanıcı adı** ve **parola**: izni toocopy hello veri sahip bir kullanıcı için hello kullanıcı adını ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="728df-163">**User name** and **password**: Enter hello user name and password for a user who has permission toocopy hello data.</span></span>

    ![Hızlı Kurulum başlatma](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="728df-165">Merhaba sonraki toochoose hello toocopy hello veri tablolarından adımdır.</span><span class="sxs-lookup"><span data-stu-id="728df-165">hello next step is toochoose hello tables from which toocopy hello data.</span></span> <span data-ttu-id="728df-166">Anahtar sözcükler kullanarak hello tabloları filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="728df-166">You can filter hello tables by using keywords.</span></span> <span data-ttu-id="728df-167">Ve hello veri ve tablo şeması hello alt panelinde önizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="728df-167">And you can preview hello data and table schema in hello bottom panel.</span></span> <span data-ttu-id="728df-168">Seçiminiz tamamladıktan sonra tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="728df-168">After you finish your selection, click **Next**.</span></span>

    ![Tabloları seçme](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a><span data-ttu-id="728df-170">Merhaba hedef, SQL veri ambarı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="728df-170">Configure hello destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="728df-171">Şimdi veri fabrikası hello hedef bilgilerini söyleyin.</span><span class="sxs-lookup"><span data-stu-id="728df-171">Now you tell Data Factory about hello destination information.</span></span>

1. <span data-ttu-id="728df-172">SQL veri ambarı bağlantı bilgilerini otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="728df-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="728df-173">Merhaba parola hello kullanıcı adını girin.</span><span class="sxs-lookup"><span data-stu-id="728df-173">Enter hello password for hello user name.</span></span> <span data-ttu-id="728df-174">tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="728df-174">and click **Next**.</span></span>

    ![Hedef yapılandırma](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="728df-176">Bir akıllı tablo eşlemesi kaynak toodestination tabloları Tablo adlarına göre eşleştiren görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="728df-176">An intelligent table mapping appears that maps source toodestination tables based on table names.</span></span> <span data-ttu-id="728df-177">Merhaba tablo hello hedef mevcut değilse, varsayılan olarak ADF hello biriyle oluşturur (bu geçerlidir tooSQL sunucu ya da kaynak olarak Azure SQL veritabanı) aynı adı.</span><span class="sxs-lookup"><span data-stu-id="728df-177">If hello table does not exist in hello destination, by default ADF will create one with hello same name (this applies tooSQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="728df-178">Toomap tooan var olan tablo de seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="728df-178">You can also choose toomap tooan existing table.</span></span> <span data-ttu-id="728df-179">Gözden geçirin ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="728df-179">Review and click **Next**.</span></span>

    ![Eşleme tabloları](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="728df-181">Merhaba şema eşleme gözden geçirin ve hata veya uyarı iletilerini arayın.</span><span class="sxs-lookup"><span data-stu-id="728df-181">Review hello schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="728df-182">Akıllı Eşleme sütun adını temel alır.</span><span class="sxs-lookup"><span data-stu-id="728df-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="728df-183">Desteklenmeyen veri türü dönüştürme hello kaynak ve hedef sütun arasında ise hello ilgili tablo yanında bir hata iletisine bakın.</span><span class="sxs-lookup"><span data-stu-id="728df-183">If there is an unsupported data type conversion between hello source and destination column, you see an error message alongside hello corresponding table.</span></span> <span data-ttu-id="728df-184">Toolet Data Factory otomatik seçerseniz hello tabloları oluşturmak, kaynak ve hedef depoları arasında toofix hello uyumsuzluk gerekirse uygun veri türü dönüşümü oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="728df-184">If you choose toolet Data Factory auto create hello tables, proper data type conversion may happen if needed toofix hello incompatibility between source and destination stores.</span></span>

    ![Şema eşleme](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="728df-186">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="728df-186">Click **Next**.</span></span>

## <a name="configure-hello-performance-settings"></a><span data-ttu-id="728df-187">Merhaba performans ayarlarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="728df-187">Configure hello performance settings</span></span>
<span data-ttu-id="728df-188">SQL Data Warehouse performantly kullanarak içine yüklenmeden önce hello verileri hazırlamak için kullanılan bir Azure depolama hesabı yapılandırma Hello performans yapılandırmalarında [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="728df-188">In hello Performance configurations, you configure an Azure storage account used for staging hello data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="728df-189">Başlangıç kopyası yapıldıktan sonra depolama birimindeki hello geçici verileri otomatik olarak temizlenecek.</span><span class="sxs-lookup"><span data-stu-id="728df-189">After hello copy is done, hello interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="728df-190">Mevcut bir Azure depolama hesabını seçin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="728df-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Hazırlama blob yapılandırın](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a><span data-ttu-id="728df-192">Özet bilgileri gözden geçirin ve hello ardışık düzen dağıtın</span><span class="sxs-lookup"><span data-stu-id="728df-192">Review summary information and deploy hello pipeline</span></span>

<span data-ttu-id="728df-193">Merhaba yapılandırmasını gözden geçirin ve tıklatın **son** düğmesini toodeploy hello ardışık düzen.</span><span class="sxs-lookup"><span data-stu-id="728df-193">Review hello configuration and click **Finish** button toodeploy hello pipeline.</span></span>

![Veri Fabrikası dağıtma](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="728df-195">Yükleme ilerlemesini izleme verileri</span><span class="sxs-lookup"><span data-stu-id="728df-195">Monitor data loading progress</span></span>

<span data-ttu-id="728df-196">Merhaba dağıtımının ilerleme durumunu ve hello sonuçlarında görebilirsiniz **dağıtım** sayfası.</span><span class="sxs-lookup"><span data-stu-id="728df-196">You can see hello deployment progress and results in hello **Deployment** page.</span></span>

1. <span data-ttu-id="728df-197">Merhaba dağıtımı yapıldıktan sonra diyor hello bağlantısına tıklayın **toomonitor kopyalama işlem hattını burayı** toomonitor veri yükleme ilerleme durumu.</span><span class="sxs-lookup"><span data-stu-id="728df-197">Once hello deployment is done, click hello link that says **Click here toomonitor copy pipeline** toomonitor data loading progress.</span></span>

    ![İşlem hattını izleme](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="728df-199">Yeni oluşturulan hello **DWLoadData fromSQLServer** veri yükleme ardışık olan hello sol seçili otomatik **kaynak Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="728df-199">hello newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from hello left-hand **Resource Explorer**.</span></span>

    ![Görünüm ardışık düzen](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="728df-201">Merhaba ortasında hello ardışık düzen'yi tıklatın paneli toosee hello için ayrıntılı durum tooan etkinlik eşlemeleri her bir tablo.</span><span class="sxs-lookup"><span data-stu-id="728df-201">Click into hello pipeline in hello middle panel toosee hello detailed status for each table that maps tooan Activity.</span></span>

    ![Tablo etkinliği görüntüle](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="728df-203">Daha fazla etkinliğin içinde tıklatın ve hello veri hello sağ panelde veri boyutu, satır, işleme, vb. dahil olmak üzere ayrıntıları yükleme bakın.</span><span class="sxs-lookup"><span data-stu-id="728df-203">Further click into an activity and you see hello data loading details in hello right panel including data size, rows, throughput, etc.</span></span>

    ![Tablo Etkinlik ayrıntıları görüntüle](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="728df-205">Bu izleme görünümü daha sonra Git tooyour SQL Data Warehouse, toolaunch tıklatın **veri yükleme > Azure Data Factory**, fabrikanızı seçin ve **izleme görevleri yüklenirken varolan**.</span><span class="sxs-lookup"><span data-stu-id="728df-205">toolaunch this monitoring view later, go tooyour SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="728df-206">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="728df-206">Next steps</span></span>

<span data-ttu-id="728df-207">Veri ambarı, veritabanı tooSQL toomigrate bkz [geçişine genel bakış](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="728df-207">toomigrate your database tooSQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="728df-208">Azure Data Factory ve kendi veri taşıma özellikleri hakkında daha fazla toolearn makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="728df-208">toolearn more about Azure Data Factory and its data movement capabilities, see hello following articles:</span></span>

- [<span data-ttu-id="728df-209">Giriş tooAzure veri fabrikası</span><span class="sxs-lookup"><span data-stu-id="728df-209">Introduction tooAzure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="728df-210">Kopyalama etkinliği kullanarak veri taşıma</span><span class="sxs-lookup"><span data-stu-id="728df-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="728df-211">Azure Data Factory kullanarak Azure SQL veri ambarından veri tooand taşıma</span><span class="sxs-lookup"><span data-stu-id="728df-211">Move data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="728df-212">SQL Data Warehouse verilerinizi tooexplore bkz hello makaleler:</span><span class="sxs-lookup"><span data-stu-id="728df-212">tooexplore your data in SQL Data Warehouse, see hello following articles:</span></span>

- [<span data-ttu-id="728df-213">Visual Studio ve SSDT ile tooSQL veri ambarına bağlanma</span><span class="sxs-lookup"><span data-stu-id="728df-213">Connect tooSQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="728df-214">[Görsel verilerinizi Power BI ile](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="728df-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[Azure portal]: https://portal.azure.com
