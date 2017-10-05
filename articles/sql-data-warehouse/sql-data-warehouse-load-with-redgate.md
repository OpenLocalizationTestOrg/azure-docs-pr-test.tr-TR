---
title: "Redgate kullanarak verileri Azure veri deposuna yükleme | Microsoft Docs"
description: "Redgate Data Platform Studio’nun veri ambarı senaryoları için nasıl kullanılacağı hakkında bilgi edinin."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 670aef98-31f7-4436-86c0-cc989a39fe7f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a38b237d5bfc0450c1ca79b53a5784dbb9bf8602
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="b76e7-103">Redgate Data Platform Studio ile veri yükleme</span><span class="sxs-lookup"><span data-stu-id="b76e7-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b76e7-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="b76e7-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="b76e7-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="b76e7-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="b76e7-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="b76e7-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="b76e7-107">BCP</span><span class="sxs-lookup"><span data-stu-id="b76e7-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="b76e7-108">Bu öğreticide, şirket içi SQL Server’dan Azure SQL Veri Ambarı’na veri taşımak için [Redgate Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/)’yu (DPS) kullanma işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-108">This tutorial shows you how to use [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) to move data from an on-premises SQL Server to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="b76e7-109">Data Platform Studio en uygun uyumluluk düzeltmelerini ve iyileştirmelerini uyguladığı için, SQL Veri Ambarı’nı kullanmaya başlamanın en hızlı yoludur.</span><span class="sxs-lookup"><span data-stu-id="b76e7-109">Data Platform Studio applies the most appropriate compatibility fixes and optimizations, so it's the quickest way to get started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="b76e7-110">[Redgate](http://www.red-gate.com) çeşitli SQL Server araçları sunan uzun süreli bir Microsoft ortağıdır.</span><span class="sxs-lookup"><span data-stu-id="b76e7-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="b76e7-111">Data Platform Studio’daki bu özellik hem ticari hem de ticari olmayan kullanımlar için ücretsiz olarak sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="b76e7-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="b76e7-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="b76e7-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="b76e7-113">Kaynak oluşturma veya tanımlama</span><span class="sxs-lookup"><span data-stu-id="b76e7-113">Create or identify resources</span></span>
<span data-ttu-id="b76e7-114">Bu öğreticiye başlamadan önce aşağıdakilere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="b76e7-114">Before starting this tutorial, you need to have:</span></span>

* <span data-ttu-id="b76e7-115">**Şirket içi SQL Server Veritabanı**: SQL Veri Ambarı’na aktarmak istediğiniz verilerin şirket içi SQL Server’dan (sürüm 2008R2 veya üstü) gelmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-115">**on-premises SQL Server Database**: The data you want to import to SQL Data Warehouse needs to come from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="b76e7-116">Data Platform Studio, verileri bir Azure SQL Veritabanından veya metin dosyalarından doğrudan aktaramaz.</span><span class="sxs-lookup"><span data-stu-id="b76e7-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="b76e7-117">**Azure Storage Hesabı**: Data Platform Studio, verileri SQL Veri Ambarı’na yüklemeden önce Azure Blob Depolama içinde hazırlar.</span><span class="sxs-lookup"><span data-stu-id="b76e7-117">**Azure Storage Account**: Data Platform Studio stages the data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="b76e7-118">Depolama hesabı “Klasik” dağıtım modeli yerine “Resource Manager” dağıtım modeli (varsayılan) kullanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b76e7-118">The storage account must be using the “Resource Manager” deployment model (the default) rather than the “Classic” deployment model.</span></span> <span data-ttu-id="b76e7-119">Bir depolama hesabınız Depolama hesabı oluşturma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="b76e7-119">If you don't have a storage account, learn how to Create a storage account.</span></span> 
* <span data-ttu-id="b76e7-120">**SQL Veri Ambarı**: Bu öğretici, verileri şirket içi SQL Server’dan SQL Veri Ambarı’na taşır, bu nedenle çevrimiçi bir veri ambarına sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-120">**SQL Data Warehouse**: This tutorial moves the data from on-premises SQL Server to SQL Data Warehouse, so you need to have a data warehouse online.</span></span> <span data-ttu-id="b76e7-121">Veri ambarınız yoksa Azure SQL Veri Ambarı oluşturma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="b76e7-121">If you do not already have a data warehouse, learn how to Create an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="b76e7-122">Depolama hesabı ve veri ambarı aynı bölge oluşturulursa performans geliştirilir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-122">Performance is improved if the storage account and the data warehouse are created in the same region.</span></span>
> 
> 

## <a name="step-1-sign-in-to-data-platform-studio-with-your-azure-account"></a><span data-ttu-id="b76e7-123">1. Adım: Azure hesabınızla Data Platform Studio’da oturum açın</span><span class="sxs-lookup"><span data-stu-id="b76e7-123">Step 1: Sign in to Data Platform Studio with your Azure account</span></span>
<span data-ttu-id="b76e7-124">Web tarayıcınızı açın ve [Data Platform Studio](https://www.dataplatformstudio.com/) web sitesine gidin.</span><span class="sxs-lookup"><span data-stu-id="b76e7-124">Open your web browser and navigate to the [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="b76e7-125">Depolama hesabını ve veri ambarını oluşturmak için kullandığını Azure hesabıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b76e7-125">Sign in with the same Azure account that you used to create the storage account and data warehouse.</span></span> <span data-ttu-id="b76e7-126">E-posta adresiniz bir iş veya okul hesabı ve bir Microsoft hesabıyla ilişkiliyse, kaynaklarınıza erişimi olan hesabı seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b76e7-126">If your email address is associated with both a work or school account and a Microsoft account, be sure to choose the account that has access to your resources.</span></span>

> [!NOTE]
> <span data-ttu-id="b76e7-127">Data Platform Studio’yu ilk kez kullanıyorsanız, Azure kaynaklarınızı yönetmesi için uygulamaya izin vermeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-127">If this is your first time using Data Platform Studio, you are asked to grant the application permission to manage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-the-import-wizard"></a><span data-ttu-id="b76e7-128">2. Adım: Alma Sihirbazı’nı başlatın</span><span class="sxs-lookup"><span data-stu-id="b76e7-128">Step 2: Start the Import Wizard</span></span>
<span data-ttu-id="b76e7-129">Alma sihirbazını başlatmak için DPS ana ekranında Azure SQL Veri Ambarı’na Al bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="b76e7-129">From the DPS main screen, select the Import to Azure SQL Data Warehouse link to start the import wizard.</span></span>

![][1]

## <a name="step-3-install-the-data-platform-studio-gateway"></a><span data-ttu-id="b76e7-130">3. Adım: Data Platform Studio Ağ Geçidini yükleyin</span><span class="sxs-lookup"><span data-stu-id="b76e7-130">Step 3: Install the Data Platform Studio Gateway</span></span>
<span data-ttu-id="b76e7-131">Şirket içi SQL Server veritabanınıza bağlanmak için DPS Ağ Geçidi’ni yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-131">To connect to your on-premises SQL Server database, you need to install the DPS Gateway.</span></span> <span data-ttu-id="b76e7-132">Ağ geçidi, şirket içi ortamınıza erişim sağlayan, verileri ayıklayan ve depolama hesabınıza yükleyen bir istemci aracısıdır.</span><span class="sxs-lookup"><span data-stu-id="b76e7-132">The gateway is a client agent that provides access to your on-premises environment, extracts the data, and uploads it to your storage account.</span></span> <span data-ttu-id="b76e7-133">Verileriniz hiçbir zaman Redgate sunucularından geçmez.</span><span class="sxs-lookup"><span data-stu-id="b76e7-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="b76e7-134">Ağ Geçidi’ni yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="b76e7-134">To install the Gateway:</span></span>

1. <span data-ttu-id="b76e7-135">**Ağ Geçidi Oluştur** bağlantısına tıklayın</span><span class="sxs-lookup"><span data-stu-id="b76e7-135">Click the **Create Gateway** link</span></span>
2. <span data-ttu-id="b76e7-136">Sağlanan yükleyiciyi kullanarak Ağ Geçidi’ni indirip yükleyin</span><span class="sxs-lookup"><span data-stu-id="b76e7-136">Download and install the Gateway using the provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="b76e7-137">Ağ Geçidi, kaynak SQL Server veritabanına ağ erişimi olan herhangi bir makineye yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-137">The Gateway can be installed on any machine with network access to the source SQL Server database.</span></span> <span data-ttu-id="b76e7-138">SQL Server veritabanına, geçerli kullanıcının kimlik bilgileriyle Windows kimlik doğrulaması kullanarak erişir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-138">It accesses the SQL Server database using Windows authentication with the credentials of the current user.</span></span>
> 
> 

<span data-ttu-id="b76e7-139">Yüklendikten sonra, Ağ Geçidi durumu Bağlı olarak değişir ve İleri’yi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b76e7-139">Once installed, the Gateway status changes to Connected and you can select Next.</span></span>

## <a name="step-4-identify-the-source-database"></a><span data-ttu-id="b76e7-140">4. Adım: Kaynak veritabanınızı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="b76e7-140">Step 4: Identify the source database</span></span>
<span data-ttu-id="b76e7-141">*Sunucu Adı Girin* metin kutusuna veritabanınızı barındıran sunucunun adını girin ve **İleri**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b76e7-141">In the *Enter Server Name* textbox, enter the name of the server that hosts your database and select **Next**.</span></span> <span data-ttu-id="b76e7-142">Ardından, açılır menüden verileri almak istediğiniz veritabanını seçin.</span><span class="sxs-lookup"><span data-stu-id="b76e7-142">Then, from the drop-down menu, select the database you want to import data from.</span></span>

![][3]

<span data-ttu-id="b76e7-143">DPS, seçili veritabanında içeri aktarılacak tabloları inceler.</span><span class="sxs-lookup"><span data-stu-id="b76e7-143">DPS inspects the selected database for tables to import.</span></span> <span data-ttu-id="b76e7-144">DPS varsayılan olarak veritabanındaki tüm tabloları içeri aktarır.</span><span class="sxs-lookup"><span data-stu-id="b76e7-144">By default, DPS imports all the tables in the database.</span></span> <span data-ttu-id="b76e7-145">Tüm Tablolar bağlantısını genişleterek tabloları seçebilir veya seçimini kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b76e7-145">You can select or deselect tables by expanding the All Tables link.</span></span> <span data-ttu-id="b76e7-146">İlerlemek için İleri düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b76e7-146">Select the Next button to move forward.</span></span>

## <a name="step-5-choose-a-storage-account-to-stage-the-data"></a><span data-ttu-id="b76e7-147">5. Adım: Verileri hazırlamak için bir depolama hesabı seçin</span><span class="sxs-lookup"><span data-stu-id="b76e7-147">Step 5: Choose a storage account to stage the data</span></span>
<span data-ttu-id="b76e7-148">DPS, verilerin hazırlanacağı bir konum seçmenizi ister.</span><span class="sxs-lookup"><span data-stu-id="b76e7-148">DPS prompts you for a location to stage the data.</span></span> <span data-ttu-id="b76e7-149">Aboneliğinizde var olan bir depolama hesabı seçin ve **İleri**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="b76e7-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="b76e7-150">DPS, seçilen depolama hesabında yeni bir blob kapsayıcısı oluşturur ve her içeri aktarma için ayrı bir klasör kullanır.</span><span class="sxs-lookup"><span data-stu-id="b76e7-150">DPS will create a new blob container in the chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="b76e7-151">6. Adım: Veri ambarı seçin</span><span class="sxs-lookup"><span data-stu-id="b76e7-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="b76e7-152">Ardından, verileri içine aktarmak için çevrimiçi bir [Azure SQL Veri Ambarı](http://aka.ms/sqldw) veritabanı seçin.</span><span class="sxs-lookup"><span data-stu-id="b76e7-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database to import the data into.</span></span> <span data-ttu-id="b76e7-153">Veritabanınızı seçtikten sonra veritabanına bağlanmak için kimlik bilgilerini girip **İleri**’yi seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-153">Once you've selected your database, you need to enter the credentials to connect to the database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="b76e7-154">DPS, kaynak veri tablolarını veri ambarında birleştirir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-154">DPS merges the source data tables into the data warehouse.</span></span> <span data-ttu-id="b76e7-155">Tablo adının veri ambarında var olan tabloların üzerine yazılması gerekirse DPS sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="b76e7-155">DPS warns you if the table name requires it to overwrite existing tables in the data warehouse.</span></span> <span data-ttu-id="b76e7-156">İsterseniz, İçeri aktarmadan önce var olan tüm nesneleri silin seçeneğini işaretleyerek veri ambarında var olan tüm nesneleri silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b76e7-156">You may optionally delete any existing objects in the data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-the-data"></a><span data-ttu-id="b76e7-157">7. Adım: Verileri içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="b76e7-157">Step 7: Import the data</span></span>
<span data-ttu-id="b76e7-158">DPS, verileri içeri aktarmak istediğinizi onaylar.</span><span class="sxs-lookup"><span data-stu-id="b76e7-158">DPS confirms that you would like to import the data.</span></span> <span data-ttu-id="b76e7-159">Verileri içeri aktarmaya başlamak için İçeri aktarmayı başlat düğmesine tıklamanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-159">Simply click the Start import button to begin the data import.</span></span>

![][6]

<span data-ttu-id="b76e7-160">DPS, verileri şirket içi SQL Server’dan ayıklayıp karşıya yükleme ve SQL Veri Ambarı’na aktarma işlemlerinin ilerleme durumunu gösteren bir görsel gösterir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-160">DPS displays a visualization that shows the progress of extracting and uploading the data from the on-premises SQL Server and the progress of the import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="b76e7-161">İçeri aktarma tamamlandıktan sonra DPS, verileri içeri aktarma işleminin bir özetini ve gerçekleştirilen uyumluluk düzeltmelerini içeren bir değişim raporunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="b76e7-161">Once the import is complete, DPS displays a summary of the data import and a change report of the compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="b76e7-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b76e7-162">Next steps</span></span>
<span data-ttu-id="b76e7-163">SQL Veri Ambarı’ndaki verilerinizi araştırmak için aşağıdakileri görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="b76e7-163">To explore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="b76e7-164">[Azure SQL Veri Ambarı'nı (Visual Studio) Sorgulama][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="b76e7-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="b76e7-165">[Power BI ile verileri görselleştirme][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="b76e7-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="b76e7-166">Redgate Data Platform Studio hakkında daha fazla bilgi almak için:</span><span class="sxs-lookup"><span data-stu-id="b76e7-166">To learn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="b76e7-167">DPS giriş sayfasını ziyaret edin</span><span class="sxs-lookup"><span data-stu-id="b76e7-167">Visit the DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="b76e7-168">DPS Channel9 gösterimini izleyin</span><span class="sxs-lookup"><span data-stu-id="b76e7-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="b76e7-169">Verilerinizi SQL Veri Ambarı’na geçirme ve yüklemenin diğer yollarına genel bakış için bkz.:</span><span class="sxs-lookup"><span data-stu-id="b76e7-169">For an overview of other ways to migrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="b76e7-170">[Çözümünüzü SQL Veri Ambarı'na taşıma][Migrate your solution to SQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="b76e7-170">[Migrate your solution to SQL Data Warehouse][Migrate your solution to SQL Data Warehouse]</span></span>
* [<span data-ttu-id="b76e7-171">Azure SQL Veri Ambarı’na veri yükleme</span><span class="sxs-lookup"><span data-stu-id="b76e7-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="b76e7-172">Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı geliştirmeye genel bakış](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="b76e7-172">For more development tips, see the [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-redgate/2016-10-05_15-59-56.png
[2]: media/sql-data-warehouse-redgate/2016-10-05_11-16-07.png
[3]: media/sql-data-warehouse-redgate/2016-10-05_11-17-46.png
[4]: media/sql-data-warehouse-redgate/2016-10-05_11-20-41.png
[5]: media/sql-data-warehouse-redgate/2016-10-05_11-31-24.png
[6]: media/sql-data-warehouse-redgate/2016-10-05_11-32-20.png
[7]: media/sql-data-warehouse-redgate/2016-10-05_11-49-53.png
[8]: media/sql-data-warehouse-redgate/2016-10-05_12-57-10.png

<!--Article references-->
[Query Azure SQL Data Warehouse (Visual Studio)]: ./sql-data-warehouse-query-visual-studio.md
[Visualize data with Power BI]: ./sql-data-warehouse-get-started-visualize-with-power-bi.md
[Migrate your solution to SQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
