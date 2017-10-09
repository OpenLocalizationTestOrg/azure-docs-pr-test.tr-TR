---
title: "aaaUse Redgate tooload veri tooyour Azure veri ambarı | Microsoft Docs"
description: "Bilgi nasıl toouse Redgate'nın veri platformu Studio veri depolama senaryolarında için."
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
ms.openlocfilehash: 6082390c07c8ffa73ebd8ab272ace00ba8bb1897
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-redgate-data-platform-studio"></a><span data-ttu-id="21f82-103">Redgate Data Platform Studio ile veri yükleme</span><span class="sxs-lookup"><span data-stu-id="21f82-103">Load data with Redgate Data Platform Studio</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="21f82-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="21f82-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)
> * [<span data-ttu-id="21f82-105">Data Factory</span><span class="sxs-lookup"><span data-stu-id="21f82-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)
> * [<span data-ttu-id="21f82-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="21f82-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)
> * [<span data-ttu-id="21f82-107">BCP</span><span class="sxs-lookup"><span data-stu-id="21f82-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="21f82-108">Bu öğretici şunların nasıl yapıldığını gösterir toouse [Redgate'nın veri platformu Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) bir şirket içi SQL Server tooAzure SQL veri ambarı (DPS) toomove verileri.</span><span class="sxs-lookup"><span data-stu-id="21f82-108">This tutorial shows you how toouse [Redgate's Data Platform Studio](http://www.red-gate.com/products/azure-development/data-platform-studio/) (DPS) toomove data from an on-premises SQL Server tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="21f82-109">Veri Platformu Studio hello en uygun uyumluluk düzeltmeleri uygular ve bu nedenle en iyi duruma getirme, hello hızlı şekilde tooget SQL Data Warehouse ile başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="21f82-109">Data Platform Studio applies hello most appropriate compatibility fixes and optimizations, so it's hello quickest way tooget started with SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="21f82-110">[Redgate](http://www.red-gate.com) çeşitli SQL Server araçları sunan uzun süreli bir Microsoft ortağıdır.</span><span class="sxs-lookup"><span data-stu-id="21f82-110">[Redgate](http://www.red-gate.com) is a long-time Microsoft partner that delivers various SQL Server tools.</span></span> <span data-ttu-id="21f82-111">Data Platform Studio’daki bu özellik hem ticari hem de ticari olmayan kullanımlar için ücretsiz olarak sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="21f82-111">This feature in Data Platform Studio has been made available freely for both commercial and non-commercial use.</span></span>
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="21f82-112">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="21f82-112">Before you begin</span></span>
### <a name="create-or-identify-resources"></a><span data-ttu-id="21f82-113">Kaynak oluşturma veya tanımlama</span><span class="sxs-lookup"><span data-stu-id="21f82-113">Create or identify resources</span></span>
<span data-ttu-id="21f82-114">Bu öğreticiye başlamadan önce toohave gerekir:</span><span class="sxs-lookup"><span data-stu-id="21f82-114">Before starting this tutorial, you need toohave:</span></span>

* <span data-ttu-id="21f82-115">**Şirket içi SQL Server veritabanı**: Merhaba tooimport tooSQL veri ambarı gereken bir şirket içi SQL Server'dan toocome istediğiniz verileri (sürüm 2008R2 veya üstü).</span><span class="sxs-lookup"><span data-stu-id="21f82-115">**on-premises SQL Server Database**: hello data you want tooimport tooSQL Data Warehouse needs toocome from an on-premises SQL Server (version 2008R2 or above).</span></span> <span data-ttu-id="21f82-116">Data Platform Studio, verileri bir Azure SQL Veritabanından veya metin dosyalarından doğrudan aktaramaz.</span><span class="sxs-lookup"><span data-stu-id="21f82-116">Data Platform Studio cannot import data directly from an Azure SQL Database or from text files.</span></span>
* <span data-ttu-id="21f82-117">**Azure depolama hesabı**: SQL Data Warehouse'a yüklemeden önce veri platformu Studio hello verileri Azure Blob Depolama aşamaları.</span><span class="sxs-lookup"><span data-stu-id="21f82-117">**Azure Storage Account**: Data Platform Studio stages hello data in Azure Blob Storage before loading it into SQL Data Warehouse.</span></span> <span data-ttu-id="21f82-118">Merhaba depolama hesabı hello "Klasik" dağıtım modeli yerine hello "Resource Manager" dağıtım modeli (Merhaba varsayılan) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f82-118">hello storage account must be using hello “Resource Manager” deployment model (hello default) rather than hello “Classic” deployment model.</span></span> <span data-ttu-id="21f82-119">Depolama hesabınız yoksa, bilgi nasıl tooCreate bir depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="21f82-119">If you don't have a storage account, learn how tooCreate a storage account.</span></span> 
* <span data-ttu-id="21f82-120">**SQL veri ambarı**: toohave gerekir böylece Bu öğretici hello verileri şirket içi SQL Server tooSQL veri ambarı, çevrimiçi bir veri ambarı taşır.</span><span class="sxs-lookup"><span data-stu-id="21f82-120">**SQL Data Warehouse**: This tutorial moves hello data from on-premises SQL Server tooSQL Data Warehouse, so you need toohave a data warehouse online.</span></span> <span data-ttu-id="21f82-121">Veri ambarı zaten yoksa öğrenin nasıl tooCreate Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="21f82-121">If you do not already have a data warehouse, learn how tooCreate an Azure SQL Data Warehouse.</span></span>

> [!NOTE]
> <span data-ttu-id="21f82-122">Merhaba depolama hesabı ve hello veri ambarı hello aynı oluşturulmuş olması durumunda performans geliştirildi bölgesi.</span><span class="sxs-lookup"><span data-stu-id="21f82-122">Performance is improved if hello storage account and hello data warehouse are created in hello same region.</span></span>
> 
> 

## <a name="step-1-sign-in-toodata-platform-studio-with-your-azure-account"></a><span data-ttu-id="21f82-123">1. adım: tooData Platform Studio Azure hesabınızla oturum</span><span class="sxs-lookup"><span data-stu-id="21f82-123">Step 1: Sign in tooData Platform Studio with your Azure account</span></span>
<span data-ttu-id="21f82-124">Web tarayıcınızı açın ve toohello gidin [veri platformu Studio](https://www.dataplatformstudio.com/) Web sitesi.</span><span class="sxs-lookup"><span data-stu-id="21f82-124">Open your web browser and navigate toohello [Data Platform Studio](https://www.dataplatformstudio.com/) website.</span></span> <span data-ttu-id="21f82-125">Oturum açma ile aynı Azure hesabı bu, kullanılan toocreate hello depolama hesabı ve veri ambarı hello.</span><span class="sxs-lookup"><span data-stu-id="21f82-125">Sign in with hello same Azure account that you used toocreate hello storage account and data warehouse.</span></span> <span data-ttu-id="21f82-126">E-posta adresinizi bir iş veya Okul hesabı ve bir Microsoft hesabı ile ilişkili ise, erişim tooyour kaynaklara sahip emin toochoose hello hesabı olması.</span><span class="sxs-lookup"><span data-stu-id="21f82-126">If your email address is associated with both a work or school account and a Microsoft account, be sure toochoose hello account that has access tooyour resources.</span></span>

> [!NOTE]
> <span data-ttu-id="21f82-127">Bu veri platformu Studio kullanarak ilk kez ise olduğunuz Azure kaynaklarınızı toogrant hello uygulama izni toomanage istedi.</span><span class="sxs-lookup"><span data-stu-id="21f82-127">If this is your first time using Data Platform Studio, you are asked toogrant hello application permission toomanage your Azure resources.</span></span>
> 
> 

## <a name="step-2-start-hello-import-wizard"></a><span data-ttu-id="21f82-128">2. adım: hello İçeri Aktarma Sihirbazı'nı Başlat</span><span class="sxs-lookup"><span data-stu-id="21f82-128">Step 2: Start hello Import Wizard</span></span>
<span data-ttu-id="21f82-129">Merhaba DPS ana ekranından, hello alma tooAzure SQL veri ambarı bağlantı toostart hello İçeri Aktarma Sihirbazı seçin.</span><span class="sxs-lookup"><span data-stu-id="21f82-129">From hello DPS main screen, select hello Import tooAzure SQL Data Warehouse link toostart hello import wizard.</span></span>

![][1]

## <a name="step-3-install-hello-data-platform-studio-gateway"></a><span data-ttu-id="21f82-130">3. adım: hello veri platformu Studio ağ geçidi yükleme</span><span class="sxs-lookup"><span data-stu-id="21f82-130">Step 3: Install hello Data Platform Studio Gateway</span></span>
<span data-ttu-id="21f82-131">tooconnect tooyour şirket içi SQL Server veritabanı tooinstall hello DPS ağ geçidi gerekir.</span><span class="sxs-lookup"><span data-stu-id="21f82-131">tooconnect tooyour on-premises SQL Server database, you need tooinstall hello DPS Gateway.</span></span> <span data-ttu-id="21f82-132">Merhaba ağ geçidi erişim tooyour şirket içi ortamına hello verileri ayıklar ve tooyour depolama hesabı yükler sağlayan bir istemci aracısıdır.</span><span class="sxs-lookup"><span data-stu-id="21f82-132">hello gateway is a client agent that provides access tooyour on-premises environment, extracts hello data, and uploads it tooyour storage account.</span></span> <span data-ttu-id="21f82-133">Verileriniz hiçbir zaman Redgate sunucularından geçmez.</span><span class="sxs-lookup"><span data-stu-id="21f82-133">Your data never passes through Redgate’s servers.</span></span> <span data-ttu-id="21f82-134">tooinstall hello ağ geçidi:</span><span class="sxs-lookup"><span data-stu-id="21f82-134">tooinstall hello Gateway:</span></span>

1. <span data-ttu-id="21f82-135">Merhaba tıklatın **ağ geçidi Oluştur** bağlantı</span><span class="sxs-lookup"><span data-stu-id="21f82-135">Click hello **Create Gateway** link</span></span>
2. <span data-ttu-id="21f82-136">İndirme ve yükleme hello ağ geçidini kullanarak sağlanan yükleyici hello</span><span class="sxs-lookup"><span data-stu-id="21f82-136">Download and install hello Gateway using hello provided installer</span></span>

![][2]

> [!NOTE]
> <span data-ttu-id="21f82-137">Merhaba ağ geçidi, ağ erişim toohello kaynak SQL Server veritabanı ile herhangi bir makinede yüklenebilir.</span><span class="sxs-lookup"><span data-stu-id="21f82-137">hello Gateway can be installed on any machine with network access toohello source SQL Server database.</span></span> <span data-ttu-id="21f82-138">Merhaba hello geçerli kullanıcı kimlik bilgileriyle Windows kimlik doğrulaması kullanarak hello SQL Server veritabanına erişir.</span><span class="sxs-lookup"><span data-stu-id="21f82-138">It accesses hello SQL Server database using Windows authentication with hello credentials of hello current user.</span></span>
> 
> 

<span data-ttu-id="21f82-139">Yüklendikten sonra ağ geçidi durumu değişiklikleri tooConnected hello ve sonraki seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21f82-139">Once installed, hello Gateway status changes tooConnected and you can select Next.</span></span>

## <a name="step-4-identify-hello-source-database"></a><span data-ttu-id="21f82-140">4. adım: hello kaynak veritabanı tanımlayın</span><span class="sxs-lookup"><span data-stu-id="21f82-140">Step 4: Identify hello source database</span></span>
<span data-ttu-id="21f82-141">Merhaba, *sunucu adı girin* metin kutusuna, hello veritabanınızı barındıran hello sunucu adını girin ve **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="21f82-141">In hello *Enter Server Name* textbox, enter hello name of hello server that hosts your database and select **Next**.</span></span> <span data-ttu-id="21f82-142">Ardından, hello açılır menüsünden tooimport verileri istediğiniz hello veritabanını seçin.</span><span class="sxs-lookup"><span data-stu-id="21f82-142">Then, from hello drop-down menu, select hello database you want tooimport data from.</span></span>

![][3]

<span data-ttu-id="21f82-143">DPS hello seçili veritabanı tabloları tooimport için olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="21f82-143">DPS inspects hello selected database for tables tooimport.</span></span> <span data-ttu-id="21f82-144">Varsayılan olarak, dağıtım noktaları hello veritabanındaki tüm hello tabloların alır.</span><span class="sxs-lookup"><span data-stu-id="21f82-144">By default, DPS imports all hello tables in hello database.</span></span> <span data-ttu-id="21f82-145">Tüm tabloları bağlantı hello genişleterek tabloları seçimini kaldırın veya seçin.</span><span class="sxs-lookup"><span data-stu-id="21f82-145">You can select or deselect tables by expanding hello All Tables link.</span></span> <span data-ttu-id="21f82-146">Merhaba İleri düğmesi toomove İleri seçin.</span><span class="sxs-lookup"><span data-stu-id="21f82-146">Select hello Next button toomove forward.</span></span>

## <a name="step-5-choose-a-storage-account-toostage-hello-data"></a><span data-ttu-id="21f82-147">5. adım: depolama hesabı toostage hello veri seçin</span><span class="sxs-lookup"><span data-stu-id="21f82-147">Step 5: Choose a storage account toostage hello data</span></span>
<span data-ttu-id="21f82-148">Dağıtım noktaları için konum toostage hello verileri ister.</span><span class="sxs-lookup"><span data-stu-id="21f82-148">DPS prompts you for a location toostage hello data.</span></span> <span data-ttu-id="21f82-149">Aboneliğinizde var olan bir depolama hesabı seçin ve **İleri**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="21f82-149">Choose an existing storage account from your subscription and select **Next**.</span></span>

> [!NOTE]
> <span data-ttu-id="21f82-150">DPS depolama hesabı seçilen hello yeni blob kapsayıcı oluşturun ve her alma için ayrı bir klasör kullanın.</span><span class="sxs-lookup"><span data-stu-id="21f82-150">DPS will create a new blob container in hello chosen storage account and use a distinct folder for each import.</span></span>
> 
> 

![][4]

## <a name="step-6-select-a-data-warehouse"></a><span data-ttu-id="21f82-151">6. Adım: Veri ambarı seçin</span><span class="sxs-lookup"><span data-stu-id="21f82-151">Step 6: Select a data warehouse</span></span>
<span data-ttu-id="21f82-152">Ardından, bir çevrimiçi seçtiğiniz [Azure SQL Data Warehouse](http://aka.ms/sqldw) veritabanı tooimport hello verileri.</span><span class="sxs-lookup"><span data-stu-id="21f82-152">Next, you select an online [Azure SQL Data Warehouse](http://aka.ms/sqldw) database tooimport hello data into.</span></span> <span data-ttu-id="21f82-153">Veritabanınızı seçtikten sonra tooenter hello kimlik bilgilerini tooconnect toohello gereken veritabanı ve seçin **sonraki**.</span><span class="sxs-lookup"><span data-stu-id="21f82-153">Once you've selected your database, you need tooenter hello credentials tooconnect toohello database and select **Next**.</span></span>

![][5]

> [!NOTE]
> <span data-ttu-id="21f82-154">DPS hello kaynak veri tabloları hello veri ambarına birleştirir.</span><span class="sxs-lookup"><span data-stu-id="21f82-154">DPS merges hello source data tables into hello data warehouse.</span></span> <span data-ttu-id="21f82-155">Dağıtım noktaları, hello tablo adı, var olan tabloları hello veri ambarı toooverwrite gerektirip gerektirmediğini sizi uyarır.</span><span class="sxs-lookup"><span data-stu-id="21f82-155">DPS warns you if hello table name requires it toooverwrite existing tables in hello data warehouse.</span></span> <span data-ttu-id="21f82-156">İsteğe bağlı olarak hello veri ambarındaki mevcut tüm nesneleri silme ticking tarafından içe aktarma işleminden önce varolan tüm nesneler silebilir.</span><span class="sxs-lookup"><span data-stu-id="21f82-156">You may optionally delete any existing objects in hello data warehouse by ticking Delete all existing objects before import.</span></span>
> 
> 

## <a name="step-7-import-hello-data"></a><span data-ttu-id="21f82-157">7. adım: Hello Veri Al</span><span class="sxs-lookup"><span data-stu-id="21f82-157">Step 7: Import hello data</span></span>
<span data-ttu-id="21f82-158">DPS tooimport hello veri istediğiniz onaylar.</span><span class="sxs-lookup"><span data-stu-id="21f82-158">DPS confirms that you would like tooimport hello data.</span></span> <span data-ttu-id="21f82-159">Merhaba başlangıç İçe Aktar düğmesi toobegin hello veri alma tıklamanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="21f82-159">Simply click hello Start import button toobegin hello data import.</span></span>

![][6]

<span data-ttu-id="21f82-160">DPS ayıklanması ve hello şirket içi SQL Server ve hello ilerlemesini SQL Data Warehouse hello içe hello verileri karşıya hello ilerleme durumunu gösteren bir görsel öğe görüntüler.</span><span class="sxs-lookup"><span data-stu-id="21f82-160">DPS displays a visualization that shows hello progress of extracting and uploading hello data from hello on-premises SQL Server and hello progress of hello import into SQL Data Warehouse.</span></span>

![][7]

<span data-ttu-id="21f82-161">Merhaba alma işlemi tamamlandıktan sonra dağıtım noktaları hello veri alma özetini ve gerçekleştirilmiş hello uyumluluk düzeltmeleri değişiklik raporunu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="21f82-161">Once hello import is complete, DPS displays a summary of hello data import and a change report of hello compatibility fixes that have been performed.</span></span>

![][8]

## <a name="next-steps"></a><span data-ttu-id="21f82-162">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21f82-162">Next steps</span></span>
<span data-ttu-id="21f82-163">Verilerinizi SQL Data warehouse'da tooexplore görüntüleyerek başlatın:</span><span class="sxs-lookup"><span data-stu-id="21f82-163">tooexplore your data within SQL Data Warehouse, start by viewing:</span></span>

* <span data-ttu-id="21f82-164">[Azure SQL Veri Ambarı'nı (Visual Studio) Sorgulama][Query Azure SQL Data Warehouse (Visual Studio)]</span><span class="sxs-lookup"><span data-stu-id="21f82-164">[Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)]</span></span>
* <span data-ttu-id="21f82-165">[Power BI ile verileri görselleştirme][Visualize data with Power BI]</span><span class="sxs-lookup"><span data-stu-id="21f82-165">[Visualize data with Power BI][Visualize data with Power BI]</span></span>

<span data-ttu-id="21f82-166">toolearn Redgate'nın veri platformu Studio hakkında daha fazla bilgi:</span><span class="sxs-lookup"><span data-stu-id="21f82-166">toolearn more about Redgate’s Data Platform Studio:</span></span>

* [<span data-ttu-id="21f82-167">Merhaba DPS giriş sayfasını ziyaret edin</span><span class="sxs-lookup"><span data-stu-id="21f82-167">Visit hello DPS homepage</span></span>](http://www.dataplatformstudio.com/)
* [<span data-ttu-id="21f82-168">DPS Channel9 gösterimini izleyin</span><span class="sxs-lookup"><span data-stu-id="21f82-168">Watch a demo of DPS on Channel9</span></span>](https://channel9.msdn.com/Blogs/cloud-with-a-silver-lining/Loading-data-into-Azure-SQL-Datawarehouse-with-Redgate-Data-Platform-Studio)

<span data-ttu-id="21f82-169">Diğer yolları toomigrate ve Yük genel bakış için SQL Data Warehouse verilerinizi bakın:</span><span class="sxs-lookup"><span data-stu-id="21f82-169">For an overview of other ways toomigrate and load your data in SQL Data Warehouse see:</span></span>

* <span data-ttu-id="21f82-170">[Çözüm tooSQL veri ambarına geçirme][Migrate your solution tooSQL Data Warehouse]</span><span class="sxs-lookup"><span data-stu-id="21f82-170">[Migrate your solution tooSQL Data Warehouse][Migrate your solution tooSQL Data Warehouse]</span></span>
* [<span data-ttu-id="21f82-171">Azure SQL Veri Ambarı’na veri yükleme</span><span class="sxs-lookup"><span data-stu-id="21f82-171">Load data into Azure SQL Data Warehouse</span></span>](sql-data-warehouse-overview-load.md)

<span data-ttu-id="21f82-172">Daha fazla geliştirme ipuçları için bkz: Merhaba [SQL Data Warehouse geliştirmeye genel bakış](sql-data-warehouse-overview-develop.md).</span><span class="sxs-lookup"><span data-stu-id="21f82-172">For more development tips, see hello [SQL Data Warehouse development overview](sql-data-warehouse-overview-develop.md).</span></span>

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
[Migrate your solution tooSQL Data Warehouse]: ./sql-data-warehouse-overview-migrate.md
[Load data into Azure SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
