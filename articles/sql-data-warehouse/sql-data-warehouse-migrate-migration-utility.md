---
title: "Geçir: Veri ambarı geçiş yardımcı programı | Microsoft Docs"
description: "SQL veri ambarı'na geçirin."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 4d7ad981-ef31-4513-b337-50bdc4709c09
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: 2466e823c448ada4dc7bc5769b1b7f10bbb5dc7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="data-warehouse-migration-utility-preview"></a><span data-ttu-id="1fa0f-103">Veri ambarı geçiş yardımcı programı (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="1fa0f-103">Data Warehouse Migration Utility (Preview)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="1fa0f-104">[Geçiş yardımcı programı indir][Download Migration Utility]</span><span class="sxs-lookup"><span data-stu-id="1fa0f-104">[Download Migration Utility][Download Migration Utility]</span></span>
> 
> 

<span data-ttu-id="1fa0f-105">Veri ambarı geçiş yardımcı programı'nı SQL Server ve Azure SQL veritabanı şeması ve verisi için Azure SQL Data Warehouse geçirmek için tasarlanmış bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-105">The Data Warehouse Migration Utility is a tool designed to migrate schema and data from SQL Server and Azure SQL Database to Azure SQL Data Warehouse.</span></span> <span data-ttu-id="1fa0f-106">Şema geçiş sırasında aracı hedef karşılık gelen şemaya kaynağından otomatik olarak eşler.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-106">During schema migration, the tool automatically maps the corresponding schema from source to destination.</span></span> <span data-ttu-id="1fa0f-107">Şema geçirildikten sonra araçları otomatik olarak oluşturulan komut ile veri taşımak için bir seçenek sağlar.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-107">After the schema has been migrated, the tools provides the option to move data with automatically generated scripts.</span></span>

<span data-ttu-id="1fa0f-108">Şeması ve verisi geçişe ek olarak, bu aracı kolaylaştırılmış geçiş önleyen hedef ve kaynak örnekleri arasında uyumsuzluk özetlemek uyumluluk raporları oluşturmak için seçeneği sunar.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-108">In addition to schema and data migration, this tool gives you the option to generate compatibility reports which summarize incompatibilities between the target and source instances which would prevent streamlined migration.</span></span>

## <a name="get-started"></a><span data-ttu-id="1fa0f-109">başlarken</span><span class="sxs-lookup"><span data-stu-id="1fa0f-109">Get started</span></span>
<span data-ttu-id="1fa0f-110">Yükleme için bir önkoşul olarak geçiş betikleri ve uyumluluk raporu görüntülemek üzere Office çalıştırmak için BCP komut satırı yardımcı programı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-110">As a prerequisite for installation, you will need the BCP command-line utility to run migration scripts and Office to view the compatibility report.</span></span> <span data-ttu-id="1fa0f-111">İndirilen yürütülebilir başlattıktan sonra aracı yüklenmeden önce standart EULA kabul etmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-111">After launching the executable that is downloaded you will be prompted to accept a standard EULA before the tool will be installed.</span></span>

<span data-ttu-id="1fa0f-112">Ayrıca, geçiş Utiliy çalıştırmak için bir gerekir geçirmeye bakıyorsanız veritabanında aşağıdaki izinleri: veritabanı oluşturma, ALTER ANY DATABASE veya Görünüm herhangi TANIMI.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-112">In addition, to run the Migration Utiliy, you will need the one following permissions on the database that you are looking to migrate: CREATE DATABASE, ALTER ANY DATABASE or VIEW ANY DEFINITION.</span></span>

### <a name="launching-the-tool-and-connecting"></a><span data-ttu-id="1fa0f-113">Aracı'nı başlatarak ve bağlanma</span><span class="sxs-lookup"><span data-stu-id="1fa0f-113">Launching the tool and connecting</span></span>
<span data-ttu-id="1fa0f-114">Aracı yükleme sonrası görünen masaüstü simgesini tıklatarak başlatın.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-114">Launch the tool by clicking on the desktop icon which appears post install.</span></span> <span data-ttu-id="1fa0f-115">Aracı açıldığında, kaynak ve hedef geçiş aracı için seçebileceğiniz bir ilk bağlantı sayfasıyla istenir.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-115">Upon opening the tool, you will be prompted with an initial connection page where you can choose your source and destination for the migration tool.</span></span> <span data-ttu-id="1fa0f-116">Bu aşamada, SQL Server ve Azure SQL veritabanı kaynakları ve SQL Data Warehouse hedef olarak olarak destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-116">At this time, we support SQL Server and Azure SQL Database as sources and SQL Data Warehouse as a destination.</span></span> <span data-ttu-id="1fa0f-117">Bu seçtikten sonra sunucu adını doldurma ve kimlik doğrulaması ve 'Bağlan' a tıklayarak kaynak sunucunuza bağlanmak istenir.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-117">After selecting this you will be asked to connect to your source server by filling in server name and authenticating and then clicking ‘Connect’.</span></span>

<span data-ttu-id="1fa0f-118">Kimlik doğrulandıktan sonra aracı, bağlandığınız sunucudaki var olan veritabanlarının listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-118">After authenticating, the tool will show a list of databases that are present in the server which you are connected to.</span></span> <span data-ttu-id="1fa0f-119">Geçirmek istediğiniz veritabanını seçtikten ve 'seçili geçirme' üzerinde tıklatarak geçişe başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-119">You can begin the migration by selecting a database that you would like to migrate and then clicking on ‘Migrate selected’.</span></span>

## <a name="migration-report"></a><span data-ttu-id="1fa0f-120">Geçiş raporu</span><span class="sxs-lookup"><span data-stu-id="1fa0f-120">Migration report</span></span>
<span data-ttu-id="1fa0f-121">'Veritabanı uyumluluğu denetle' aracı seçme geçirmek için istenen veritabanındaki tüm nesne uyumsuzlukları özetleyen bir rapor oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-121">Selecting ‘Check Database Compatibility’ in the tool will generate a report summarizing all object incompatibilities in the database you requested to migrate.</span></span> <span data-ttu-id="1fa0f-122">SQL veri ambarı'nda mevcut değil SQL Server işlevsellik daha geniş bir listesi bulunabilir bizim [geçiş belgeleri][migration documentation].</span><span class="sxs-lookup"><span data-stu-id="1fa0f-122">A broader list of some of the SQL Server functionality that is not present in SQL Data Warehouse can be found in our [migration documentation][migration documentation].</span></span> <span data-ttu-id="1fa0f-123">Raporun oluşturulduğu sonra kaydedin ve rapor Excel'de açın.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-123">After the report is generated you will be able to save and open the report in Excel.</span></span>

<span data-ttu-id="1fa0f-124">Lütfen geçiş şeması, 'Object' bu verilerin hemen geçiş izin vermek üzere ayarlanmış olarak tanımlanan çoğu sorunların oluştururken unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-124">Please note that when generating the migration schema, most issues identified as ‘Object’ will be adjusted in order to allow immediate migration of that data.</span></span> <span data-ttu-id="1fa0f-125">Lütfen şemayı uygulamadan önce ek ayarlamalar yapmak istiyor musunuz emin olmak için değişiklikleri gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-125">Please review the changes to ensure you do not want to make additional adjustments before applying the schema.</span></span>

## <a name="migrate-schema"></a><span data-ttu-id="1fa0f-126">Geçiş şeması</span><span class="sxs-lookup"><span data-stu-id="1fa0f-126">Migrate schema</span></span>
<span data-ttu-id="1fa0f-127">Bağlandıktan sonra geçirme'Schema ' seçerek seçili tablo için şema geçiş komut dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-127">After connecting, selecting ‘Migrate Schema’ will generate a schema migration script for the selected tables.</span></span> <span data-ttu-id="1fa0f-128">Bu komut dosyası bağlantı noktalarını eşlemeleri uyumsuz veri tablosunun yapısı daha uyumlu formlara türleri ve bu geçiş ayarları kullanıcı tarafından belirtilirse, güvenlik kimlik bilgileri ve şema oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-128">This script ports the structure of the table, maps incompatible data types to more compatible forms, and creates security credentials and schema if this is indicated by the user in the migration settings.</span></span> <span data-ttu-id="1fa0f-129">Bu kod hedeflenen SQL Data Warehouse örneğine karşı çalıştırabilirsiniz, bir dosyaya kaydedilir, panonuza kopyaladığınız veya daha fazla eylemi gerçekleştirmeden önce satır içi bile düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-129">This code can be run against the targeted SQL Data Warehouse instance, saved to a file, copied to your clipboard, or even edited in-line before taking further action.</span></span>  

<span data-ttu-id="1fa0f-130">Geçirme şema gözden geçirme, değiştiğinde olarak yukarıda belirtildiği, aracı emin olmak için yaptığı tam olarak bunları anladığınızdan.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-130">As noted above, when migrating schema review the migration changes that the tool has made in order to ensure that that you fully understand them.</span></span>  

## <a name="migrate-data"></a><span data-ttu-id="1fa0f-131">Geçiş verileri</span><span class="sxs-lookup"><span data-stu-id="1fa0f-131">Migrate data</span></span>
<span data-ttu-id="1fa0f-132">'Verileri geçirmek' seçeneğini tıklatarak, verilerinizi ilk sunucunuzda, düz dosyalar taşır BCP komut dosyaları oluşturabilir ve ardından SQL veri ambarı doğrudan.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-132">By clicking the ‘Migrate Data’ option you can generate BCP scripts that will move your data first to flat files on your server, and then directly into your SQL Data Warehouse.</span></span> <span data-ttu-id="1fa0f-133">Küçük miktarda veri ve yeniden deneme olarak taşımak için bu işlemi yerleşik olmayan ve hataları ağ bağlantı kaybı oluşabilir öneririz.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-133">We recommend this process for moving small amounts of data and, as retries are not built-in and failures may occur if there is a loss of the network connection.</span></span> <span data-ttu-id="1fa0f-134">Bunu çalıştırmak için BCP komut satırı yardımcı programının yüklü olması gerekir ve veriler için şema zaten oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-134">In order to run this, you will need to have the BCP command-line utility installed and the schema for the data must already have been created.</span></span>

<span data-ttu-id="1fa0f-135">Parametreleri yukarıdaki doldurduktan sonra çalışma geçiş tıklamanız yeterlidir ve iki paket kümesini belirtilen konuma oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-135">After you have filled out the parameters above you simply need to click run migration and a set of two packages will be generated to your specified location.</span></span> <span data-ttu-id="1fa0f-136">Veri geçiş kaynağınızdan düz dosyasına dışarı aktarma için dışarı aktarma dosyasını çalıştırın ve verilerinizi SQL Data Warehouse'a almak için içeri aktarma dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1fa0f-136">Run the export file in order to export data from your migration source into flat files, and run the import file in order to import your data into SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1fa0f-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1fa0f-137">Next steps</span></span>
<span data-ttu-id="1fa0f-138">Nasıl yapılır bazı verileri geçirdikten, kullanıma [geliştirmek][develop].</span><span class="sxs-lookup"><span data-stu-id="1fa0f-138">Now that you've migrated some data, check out how to [develop][develop].</span></span>

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
