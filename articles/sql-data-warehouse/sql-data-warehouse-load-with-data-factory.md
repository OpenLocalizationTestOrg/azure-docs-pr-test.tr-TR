---
title: "Azure SQL Data Warehouse'a – Data Factory veri yükleme | Microsoft Docs"
description: "Bu öğreticide Azure Data Factory kullanarak Azure SQL Data Warehouse'a veri yükler ve veri kaynağı olarak bir SQL Server veritabanını kullanır."
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
ms.openlocfilehash: 12a35213e07ff16bdc1c27be106792bcc032ac80
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a><span data-ttu-id="0f9da-103">Data Factory ile SQL veri ambarına veri yükleme</span><span class="sxs-lookup"><span data-stu-id="0f9da-103">Load data into SQL Data Warehouse with Data Factory</span></span>

<span data-ttu-id="0f9da-104">Azure Data Factory herhangi birini Azure SQL Data Warehouse'a veri yüklemek için kullanabileceğiniz [desteklenen kaynak veri depoları](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="0f9da-104">You can use Azure Data Factory to load data into Azure SQL Data Warehouse from any of the [supported source data stores](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="0f9da-105">Örneğin, verileri Azure SQL veritabanına veya bir Oracle veritabanından bir SQL data warehouse'a veri fabrikası kullanarak yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f9da-105">For example, you can load data from an Azure SQL database or an Oracle database into a SQL data warehouse by using Data Factory.</span></span> <span data-ttu-id="0f9da-106">Bu makalede öğreticide bir şirket içi SQL Server veritabanından SQL data warehouse'a veri yükleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="0f9da-106">Tutorial in this article shows you how to load data from an on-premises SQL Server database into a SQL data warehouse.</span></span>

<span data-ttu-id="0f9da-107">**Zaman tahmin**: Bu öğreticide Önkoşullar sağlandığında tamamlamak için yaklaşık 10-15 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="0f9da-107">**Time estimate**: This tutorial takes about 10-15 minutes to complete once the prerequisites are met.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f9da-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0f9da-108">Prerequisites</span></span>

- <span data-ttu-id="0f9da-109">Gereksinim duyduğunuz bir **SQL Server veritabanı** SQL veri ambarı'na üzerinden kopyalanacak verileri içeren tablolar ile.</span><span class="sxs-lookup"><span data-stu-id="0f9da-109">You need a **SQL Server database** with tables that contain the data to be copied over to the SQL data warehouse.</span></span>  

- <span data-ttu-id="0f9da-110">Çevrimiçi ihtiyacınız **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-110">You need an online **SQL Data Warehouse**.</span></span> <span data-ttu-id="0f9da-111">Veri ambarı zaten yoksa öğrenin nasıl [bir Azure SQL Data Warehouse oluşturma](sql-data-warehouse-get-started-provision.md).</span><span class="sxs-lookup"><span data-stu-id="0f9da-111">If you do not already have a data warehouse, learn how to [Create an Azure SQL Data Warehouse](sql-data-warehouse-get-started-provision.md).</span></span>

- <span data-ttu-id="0f9da-112">Gereksinim duyduğunuz bir **Azure depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-112">You need an **Azure Storage Account**.</span></span> <span data-ttu-id="0f9da-113">Bir depolama hesabı zaten yoksa öğrenin nasıl [depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="0f9da-113">If you do not already have a storage account, learn how to [Create a storage account](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="0f9da-114">En iyi performans için depolama hesabı ve veri ambarı aynı Azure bölgesinde bulun.</span><span class="sxs-lookup"><span data-stu-id="0f9da-114">For best performance, locate the storage account and the data warehouse in the same Azure region.</span></span>

## <a name="configure-a-data-factory"></a><span data-ttu-id="0f9da-115">Data factory Yapılandır</span><span class="sxs-lookup"><span data-stu-id="0f9da-115">Configure a data factory</span></span>
1. <span data-ttu-id="0f9da-116">[Azure Portal][]’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="0f9da-116">Log in to the [Azure portal][].</span></span>
2. <span data-ttu-id="0f9da-117">Veri ambarınız bulun ve açmak için tıklatın.</span><span class="sxs-lookup"><span data-stu-id="0f9da-117">Locate your data warehouse and click to open it.</span></span>
3. <span data-ttu-id="0f9da-118">Ana dikey penceresinde tıklayın **veri yükleme** > **Azure Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-118">In the main blade, click **Load Data** > **Azure Data Factory**.</span></span>

    ![Veri Yükleme Sihirbazını Başlat](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. <span data-ttu-id="0f9da-120">Azure aboneliğinizde bir veri fabrikası yoksa gördüğünüz bir **yeni Data Factory** ayrı bir sekmesinde iletişim kutusunda tarayıcının.</span><span class="sxs-lookup"><span data-stu-id="0f9da-120">If you do not have a data factory in your Azure subscription, you see a **New Data Factory** dialog box in a separate tab of the browser.</span></span> <span data-ttu-id="0f9da-121">İstenen bilgileri girin ve tıklayın **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-121">Fill in the requested information, and click **Create**.</span></span> <span data-ttu-id="0f9da-122">Veri Fabrikası oluşturulduktan sonra **yeni Data Factory** iletişim kutusunu kapatır ve gördüğünüz **seçin Data Factory** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="0f9da-122">After the data factory is created, the **New Data Factory** dialog box closes, and you see the **Select Data Factory** dialog box.</span></span>

    <span data-ttu-id="0f9da-123">Zaten Azure Abonelikteki bir veya daha fazla veri fabrikaları varsa, gördüğünüz **seçin Data Factory** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="0f9da-123">If you have one or more data factories already in the Azure subscription, you see the **Select Data Factory** dialog box.</span></span> <span data-ttu-id="0f9da-124">Bu iletişim kutusunda, mevcut bir veri fabrikasını seçin veya tıklatın **oluştur yeni data factory** yeni bir tane oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="0f9da-124">In this dialog box, you can either select an existing data factory or click **Create new data factory** to create a new one.</span></span>

    ![Veri Fabrikası yapılandırın](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. <span data-ttu-id="0f9da-126">İçinde **seçin Data Factory** iletişim kutusu, **veri yükleme** seçeneği, varsayılan olarak seçilidir.</span><span class="sxs-lookup"><span data-stu-id="0f9da-126">In the **Select Data Factory** dialog box, the **Load data** option is selected by default.</span></span> <span data-ttu-id="0f9da-127">Tıklatın **sonraki** veri görev yükleme oluşturmaya başlamak için.</span><span class="sxs-lookup"><span data-stu-id="0f9da-127">Click **Next** to start creating a data loading task.</span></span>

## <a name="configure-the-data-factory-properties"></a><span data-ttu-id="0f9da-128">Veri Fabrikası özelliklerini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0f9da-128">Configure the data factory properties</span></span>
<span data-ttu-id="0f9da-129">Veri Fabrikası oluşturduğunuza göre sonraki adıma Zamanlama yüklenirken veri yapılandırmaktır.</span><span class="sxs-lookup"><span data-stu-id="0f9da-129">Now that you have created a data factory, the next step is to configure the data loading schedule.</span></span>

1. <span data-ttu-id="0f9da-130">İçin **görev adı**, girin **DWLoadData fromSQLServer**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-130">For **Task name**, enter **DWLoadData-fromSQLServer**.</span></span>
2. <span data-ttu-id="0f9da-131">Varsayılan kullanmak **kez Şimdi Çalıştır** seçeneği, tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-131">Use the default **Run once now** option, click **Next**.</span></span>

    ![Yükleme zamanlamasını yapılandırın](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-the-source-data-store-and-gateway"></a><span data-ttu-id="0f9da-133">Ağ geçidi ve kaynak veri deposu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0f9da-133">Configure the source data store and gateway</span></span>
<span data-ttu-id="0f9da-134">Şimdi veri yüklemek istediğiniz şirket içi SQL Server veritabanı hakkında veri fabrikası söyleyin.</span><span class="sxs-lookup"><span data-stu-id="0f9da-134">Now you tell Data Factory about the on-premises SQL Server database from which you want to load data.</span></span>

1. <span data-ttu-id="0f9da-135">Seçin **SQL Server** desteklenen kaynak verilerden katalog depolamak ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-135">Choose **SQL Server** from the supported source data store catalog, and click **Next**.</span></span>

    ![SQL Server kaynak seçin](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. <span data-ttu-id="0f9da-137">A **şirket içi SQL Server veritabanını belirtin** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0f9da-137">A **Specify the on-premises SQL Server database** dialog appears.</span></span> <span data-ttu-id="0f9da-138">İlk **bağlantı adı** doldurulmuş otomatik bir alandır.</span><span class="sxs-lookup"><span data-stu-id="0f9da-138">The first  **Connection name** field is auto filled in.</span></span> <span data-ttu-id="0f9da-139">İkinci alan adını ister **ağ geçidi**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-139">The second field asks for the name of the **Gateway**.</span></span> <span data-ttu-id="0f9da-140">Bir ağ geçidi zaten mevcut bir veri fabrikasını kullanıyorsanız, aşağı açılan listeden seçerek ağ geçidini yeniden kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f9da-140">If you are using an existing data factory that already has a gateway, you can reuse the gateway by selecting it from the drop-down list.</span></span> <span data-ttu-id="0f9da-141">Tıklatın **ağ geçidi Oluştur** veri yönetimi ağ geçidi oluşturmak için bağlantı.</span><span class="sxs-lookup"><span data-stu-id="0f9da-141">Click the **Create Gateway** link to create a Data Management Gateway.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="0f9da-142">Kaynak veri deposu, şirket içi veya bir Azure Iaas sanal makinesi veri yönetimi ağ geçidi gereklidir.</span><span class="sxs-lookup"><span data-stu-id="0f9da-142">If the source data store is on-premises or in an Azure IaaS virtual machine, a Data Management Gateway is required.</span></span> <span data-ttu-id="0f9da-143">Bir ağ geçidi, veri fabrikası bir 1-1 ilişkisi yok.</span><span class="sxs-lookup"><span data-stu-id="0f9da-143">A gateway has a 1-1 relationship with a data factory.</span></span> <span data-ttu-id="0f9da-144">Başka bir veri fabrikası'ndan kullanılamaz, ancak birden çok veri yükleme ile aynı veri fabrikasında görevleri tarafından kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0f9da-144">It cannot be used from another data factory, but it can be used by multiple data loading tasks with in the same data factory.</span></span> <span data-ttu-id="0f9da-145">Bir ağ geçidi, veri görevleri yükleme çalışırken birden çok veri depolarına bağlanmak için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="0f9da-145">A gateway can be used to connect to multiple data stores when running data loading tasks.</span></span>
    >
    > <span data-ttu-id="0f9da-146">Ağ geçidi hakkında ayrıntılı bilgi için bkz: [veri yönetimi ağ geçidi](../data-factory/data-factory-data-management-gateway.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="0f9da-146">For detailed information about the gateway, see [Data Management Gateway](../data-factory/data-factory-data-management-gateway.md) article.</span></span>

3. <span data-ttu-id="0f9da-147">A **ağ geçidi Oluştur** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0f9da-147">A **Create Gateway** dialog box appears.</span></span> <span data-ttu-id="0f9da-148">Adı **GatewayForDWLoading**, tıklatıp **oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-148">For Name, enter **GatewayForDWLoading**, and click **Create**.</span></span>

4. <span data-ttu-id="0f9da-149">A **yapılandırma ağ geçidi** iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0f9da-149">A **Configure Gateway** dialog box appears.</span></span> <span data-ttu-id="0f9da-150">Tıklatın **başlatma hızlı kurulum bu bilgisayarda** otomatik olarak indirmek için yüklemek ve veri yönetimi ağ geçidi geçerli makinenize kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0f9da-150">Click **Launch express setup on this computer** to automatically download, install, and register Data Management Gateway on your current machine.</span></span> <span data-ttu-id="0f9da-151">İlerleme açılır pencerede gösterilir.</span><span class="sxs-lookup"><span data-stu-id="0f9da-151">The progress is shown in a pop-up window.</span></span> <span data-ttu-id="0f9da-152">Makine veri deposuna bağlanamazsa, el ile denetleyebilirsiniz [ağ geçidi yükleyip](https://www.microsoft.com/download/details.aspx?id=39717) verilere bağlayabilirsiniz bir makinede depolamak ve kaydetmek için kayıt anahtarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f9da-152">If the machine cannot connect to the data store, you can manually [download and install the gateway](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect to the data store, and then use the key to register.</span></span>
    > [!NOTE]
    > <span data-ttu-id="0f9da-153">Hızlı Kurulum, Microsoft Edge ve Internet Explorer ile yerel olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="0f9da-153">The express setup works natively with Microsoft Edge and Internet Explorer.</span></span> <span data-ttu-id="0f9da-154">İlk Google Chrome kullanıyorsanız, ClickOnce uzantı Chrome web Mağazası'ndan yükleyin.</span><span class="sxs-lookup"><span data-stu-id="0f9da-154">If you are using Google Chrome, first install the ClickOnce extension from Chrome web store.</span></span>

    ![Hızlı Kurulum başlatma](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. <span data-ttu-id="0f9da-156">Ağ geçidi kurulumun tamamlanması için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="0f9da-156">Wait for the gateway setup to complete.</span></span> <span data-ttu-id="0f9da-157">Ağ geçidi başarıyla kaydedildi ve çevrimiçi sonra açılır penceresi kapanır ve yeni ağ geçidi ağ geçidi alanında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="0f9da-157">Once the gateway is successfully registered and is online, the pop-up window closes and the new gateway appears in the gateway field.</span></span> <span data-ttu-id="0f9da-158">Ardından kalan doldurun gibi gerekli alanları, ardından **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-158">Then fill in the rest required fields as follows, then click **Next**.</span></span>
    - <span data-ttu-id="0f9da-159">**Sunucu adı**: şirket içi SQL Server'ın adı.</span><span class="sxs-lookup"><span data-stu-id="0f9da-159">**Server name**: Name of the on-premises SQL Server.</span></span>
    - <span data-ttu-id="0f9da-160">**Veritabanı adı**: SQL Server veritabanı.</span><span class="sxs-lookup"><span data-stu-id="0f9da-160">**Database name**: SQL Server database.</span></span>
    - <span data-ttu-id="0f9da-161">**Kimlik bilgisi şifreleme**: "web tarayıcısı tarafından" varsayılan kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f9da-161">**Credential encryption**: Use the default "By web browser".</span></span>
    - <span data-ttu-id="0f9da-162">**Kimlik doğrulama türü**: kullanmakta olduğunuz kimlik doğrulama türünü seçin.</span><span class="sxs-lookup"><span data-stu-id="0f9da-162">**Authentication type**: Choose the type of authentication you are using.</span></span>
    - <span data-ttu-id="0f9da-163">**Kullanıcı adı** ve **parola**: veri kopyalamak için izni olan bir kullanıcı için kullanıcı adını ve parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="0f9da-163">**User name** and **password**: Enter the user name and password for a user who has permission to copy the data.</span></span>

    ![Hızlı Kurulum başlatma](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. <span data-ttu-id="0f9da-165">Sonraki adım, verileri kopyalamak tablolardan seçmektir.</span><span class="sxs-lookup"><span data-stu-id="0f9da-165">The next step is to choose the tables from which to copy the data.</span></span> <span data-ttu-id="0f9da-166">Anahtar sözcükler kullanarak tabloları filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f9da-166">You can filter the tables by using keywords.</span></span> <span data-ttu-id="0f9da-167">Ve veri ve tablo şeması alt panelinde önizleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f9da-167">And you can preview the data and table schema in the bottom panel.</span></span> <span data-ttu-id="0f9da-168">Seçiminiz tamamladıktan sonra tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-168">After you finish your selection, click **Next**.</span></span>

    ![Tabloları seçme](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-the-destination-your-sql-data-warehouse"></a><span data-ttu-id="0f9da-170">Hedef, SQL veri ambarı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0f9da-170">Configure the destination, your SQL Data Warehouse</span></span>

<span data-ttu-id="0f9da-171">Şimdi veri fabrikası hedef bilgilerini söyleyin.</span><span class="sxs-lookup"><span data-stu-id="0f9da-171">Now you tell Data Factory about the destination information.</span></span>

1. <span data-ttu-id="0f9da-172">SQL veri ambarı bağlantı bilgilerini otomatik olarak doldurulur.</span><span class="sxs-lookup"><span data-stu-id="0f9da-172">Your SQL Data Warehouse connection information is filled in automatically.</span></span> <span data-ttu-id="0f9da-173">Kullanıcı adı için parola girin.</span><span class="sxs-lookup"><span data-stu-id="0f9da-173">Enter the password for the user name.</span></span> <span data-ttu-id="0f9da-174">tıklatıp **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-174">and click **Next**.</span></span>

    ![Hedef yapılandırma](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. <span data-ttu-id="0f9da-176">Bir akıllı tablo eşlemesi eşlemeleri tablo adlarına göre hedef tabloları için kaynak görünür.</span><span class="sxs-lookup"><span data-stu-id="0f9da-176">An intelligent table mapping appears that maps source to destination tables based on table names.</span></span> <span data-ttu-id="0f9da-177">Hedef Tablo mevcut değilse, varsayılan olarak (Bu bu SQL Server ya da kaynak olarak Azure SQL veritabanı için geçerlidir) aynı ada sahip bir ADF oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0f9da-177">If the table does not exist in the destination, by default ADF will create one with the same name (this applies to SQL Server or Azure SQL Database as source).</span></span> <span data-ttu-id="0f9da-178">Var olan bir tabloya eşlemek seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f9da-178">You can also choose to map to an existing table.</span></span> <span data-ttu-id="0f9da-179">Gözden geçirin ve tıklatın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-179">Review and click **Next**.</span></span>

    ![Eşleme tabloları](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. <span data-ttu-id="0f9da-181">Şema eşleme gözden geçirin ve hata veya uyarı iletilerini arayın.</span><span class="sxs-lookup"><span data-stu-id="0f9da-181">Review the schema mapping and look for error or warning messages.</span></span> <span data-ttu-id="0f9da-182">Akıllı Eşleme sütun adını temel alır.</span><span class="sxs-lookup"><span data-stu-id="0f9da-182">Intelligent mapping is based on column name.</span></span> <span data-ttu-id="0f9da-183">Kaynak ve hedef sütun arasında bir desteklenmeyen veri türü dönüştürme ise, ilgili tablo yanında bir hata iletisine bakın.</span><span class="sxs-lookup"><span data-stu-id="0f9da-183">If there is an unsupported data type conversion between the source and destination column, you see an error message alongside the corresponding table.</span></span> <span data-ttu-id="0f9da-184">Veri Fabrikası otomatik tabloları oluşturma olanak seçerseniz, uygun veri türü dönüşümü kaynak ve hedef depoları arasında uyumsuzluk sorunu düzeltmek için gerekirse ortaya çıkabilir.</span><span class="sxs-lookup"><span data-stu-id="0f9da-184">If you choose to let Data Factory auto create the tables, proper data type conversion may happen if needed to fix the incompatibility between source and destination stores.</span></span>

    ![Şema eşleme](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. <span data-ttu-id="0f9da-186">**İleri**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0f9da-186">Click **Next**.</span></span>

## <a name="configure-the-performance-settings"></a><span data-ttu-id="0f9da-187">Performans ayarlarını yapılandır</span><span class="sxs-lookup"><span data-stu-id="0f9da-187">Configure the performance settings</span></span>
<span data-ttu-id="0f9da-188">SQL veri ambarı performantly kullanarak içine yüklenmeden önce verileri hazırlamak için kullanılan bir Azure depolama hesabı yapılandırma performans yapılandırmalarında [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span><span class="sxs-lookup"><span data-stu-id="0f9da-188">In the Performance configurations, you configure an Azure storage account used for staging the data before it loads into SQL Data Warehouse performantly using [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly).</span></span> <span data-ttu-id="0f9da-189">Kopyalama tamamlandıktan sonra depolama birimindeki geçici verileri otomatik olarak temizlenecek.</span><span class="sxs-lookup"><span data-stu-id="0f9da-189">After the copy is done, the interim data in storage will be cleaned up automatically.</span></span>

<span data-ttu-id="0f9da-190">Mevcut bir Azure depolama hesabını seçin ve tıklayın **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-190">Select an existing Azure Storage account, and click **Next**.</span></span>

![Hazırlama blob yapılandırın](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-the-pipeline"></a><span data-ttu-id="0f9da-192">Özet bilgileri gözden geçirin ve ardışık düzen dağıtın</span><span class="sxs-lookup"><span data-stu-id="0f9da-192">Review summary information and deploy the pipeline</span></span>

<span data-ttu-id="0f9da-193">Yapılandırmasını gözden geçirmek ve tıklayın **son** düğmesi ardışık düzen dağıtın.</span><span class="sxs-lookup"><span data-stu-id="0f9da-193">Review the configuration and click **Finish** button to deploy the pipeline.</span></span>

![Veri Fabrikası dağıtma](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a><span data-ttu-id="0f9da-195">Yükleme ilerlemesini izleme verileri</span><span class="sxs-lookup"><span data-stu-id="0f9da-195">Monitor data loading progress</span></span>

<span data-ttu-id="0f9da-196">Sonuçları ve dağıtımının ilerleme durumunu görebilirsiniz **dağıtım** sayfası.</span><span class="sxs-lookup"><span data-stu-id="0f9da-196">You can see the deployment progress and results in the **Deployment** page.</span></span>

1. <span data-ttu-id="0f9da-197">Dağıtım tamamlandığında bağlantısını tıklatın **kopyalama işlem hattını izlemek için burayı tıklatın** veri yükleme ilerlemesini izlemek için.</span><span class="sxs-lookup"><span data-stu-id="0f9da-197">Once the deployment is done, click the link that says **Click here to monitor copy pipeline** to monitor data loading progress.</span></span>

    ![İşlem hattını izleme](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. <span data-ttu-id="0f9da-199">Yeni oluşturulan **DWLoadData fromSQLServer** veri yükleme ardışık olan sol seçili otomatik **kaynak Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-199">The newly created **DWLoadData-fromSQLServer** data loading pipeline is auto selected from the left-hand **Resource Explorer**.</span></span>

    ![Görünüm ardışık düzen](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. <span data-ttu-id="0f9da-201">Ardışık Düzen Orta panelinde bir etkinliğe eşlemeleri her tablo için ayrıntılı durum görmek için tıklayın.</span><span class="sxs-lookup"><span data-stu-id="0f9da-201">Click into the pipeline in the middle panel to see the detailed status for each table that maps to an Activity.</span></span>

    ![Tablo etkinliği görüntüle](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. <span data-ttu-id="0f9da-203">Daha fazla etkinliğin içinde tıklatın ve veri boyutu, satır, işleme, vb. dahil olmak üzere sağ bölmede ayrıntıları yükleniyor veri bakın.</span><span class="sxs-lookup"><span data-stu-id="0f9da-203">Further click into an activity and you see the data loading details in the right panel including data size, rows, throughput, etc.</span></span>

    ![Tablo Etkinlik ayrıntıları görüntüle](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. <span data-ttu-id="0f9da-205">Bu izleme görünümü daha sonra SQL veri ambarı gidin başlatmak için tıklatın **veri yükleme > Azure Data Factory**, fabrikanızı seçin ve **izleme görevleri yüklenirken varolan**.</span><span class="sxs-lookup"><span data-stu-id="0f9da-205">To launch this monitoring view later, go to your SQL Data Warehouse, click **Load Data > Azure Data Factory**, select your factory, and choose **Monitor existing loading tasks**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f9da-206">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0f9da-206">Next steps</span></span>

<span data-ttu-id="0f9da-207">SQL Data Warehouse veritabanınızı geçirmek için bkz [geçişine genel bakış](sql-data-warehouse-overview-migrate.md).</span><span class="sxs-lookup"><span data-stu-id="0f9da-207">To migrate your database to SQL Data Warehouse, see [Migration overview](sql-data-warehouse-overview-migrate.md).</span></span>

<span data-ttu-id="0f9da-208">Azure Data Factory ve veri taşıma özelliklerini hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="0f9da-208">To learn more about Azure Data Factory and its data movement capabilities, see the following articles:</span></span>

- [<span data-ttu-id="0f9da-209">Azure Data Factory'ye giriş</span><span class="sxs-lookup"><span data-stu-id="0f9da-209">Introduction to Azure Data Factory</span></span>](../data-factory/data-factory-introduction.md)
- [<span data-ttu-id="0f9da-210">Kopyalama etkinliği kullanarak veri taşıma</span><span class="sxs-lookup"><span data-stu-id="0f9da-210">Move data by using Copy Activity</span></span>](../data-factory/data-factory-data-movement-activities.md)
- [<span data-ttu-id="0f9da-211">Azure Data Factory kullanarak Azure'a/Azure'dan veri taşıma</span><span class="sxs-lookup"><span data-stu-id="0f9da-211">Move data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

<span data-ttu-id="0f9da-212">SQL Data Warehouse verilerinizi keşfetmek için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="0f9da-212">To explore your data in SQL Data Warehouse, see the following articles:</span></span>

- [<span data-ttu-id="0f9da-213">Visual Studio ve SSDT ile SQL Data Warehouse'a bağlanma</span><span class="sxs-lookup"><span data-stu-id="0f9da-213">Connect to SQL Data Warehouse with Visual Studio and SSDT</span></span>](sql-data-warehouse-query-visual-studio.md)
- <span data-ttu-id="0f9da-214">[Görsel verilerinizi Power BI ile](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="0f9da-214">[Visual data with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

<!-- Azure references -->
[Azure Portal]: https://portal.azure.com
