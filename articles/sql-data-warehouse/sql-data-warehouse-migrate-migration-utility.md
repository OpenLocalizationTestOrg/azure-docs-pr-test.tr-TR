---
title: "Geçir: Veri ambarı geçiş yardımcı programı | Microsoft Docs"
description: "Veri ambarı tooSQL geçirin."
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
ms.openlocfilehash: c89909883fb42b0b04dd87a9973e5ee3e30d8f0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-warehouse-migration-utility-preview"></a><span data-ttu-id="f7c0b-103">Veri ambarı geçiş yardımcı programı (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="f7c0b-103">Data Warehouse Migration Utility (Preview)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="f7c0b-104">[Geçiş yardımcı programı indir][Download Migration Utility]</span><span class="sxs-lookup"><span data-stu-id="f7c0b-104">[Download Migration Utility][Download Migration Utility]</span></span>
> 
> 

<span data-ttu-id="f7c0b-105">Veri ambarı geçiş yardımcı programı Hello toomigrate şema ve SQL Server ve Azure SQL veritabanı tooAzure SQL Data Warehouse verilerini bir aracı tasarlanmış ' dir.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-105">hello Data Warehouse Migration Utility is a tool designed toomigrate schema and data from SQL Server and Azure SQL Database tooAzure SQL Data Warehouse.</span></span> <span data-ttu-id="f7c0b-106">Şema geçiş sırasında hello aracı hello karşılık gelen kaynak toodestination şemadan otomatik olarak eşlenir.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-106">During schema migration, hello tool automatically maps hello corresponding schema from source toodestination.</span></span> <span data-ttu-id="f7c0b-107">Merhaba şema geçirildikten sonra hello Araçlar otomatik olarak oluşturulan komut ile Merhaba seçeneği toomove verileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-107">After hello schema has been migrated, hello tools provides hello option toomove data with automatically generated scripts.</span></span>

<span data-ttu-id="f7c0b-108">Ayrıca tooschema ve veri geçişi, önleyen hello hedef ve kaynak örnekleri arasında uyumsuzluk özetleme seçeneği toogenerate Uyumluluk raporlarını hello aracı kazandırır geçiş hızlandırıldı.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-108">In addition tooschema and data migration, this tool gives you hello option toogenerate compatibility reports which summarize incompatibilities between hello target and source instances which would prevent streamlined migration.</span></span>

## <a name="get-started"></a><span data-ttu-id="f7c0b-109">başlarken</span><span class="sxs-lookup"><span data-stu-id="f7c0b-109">Get started</span></span>
<span data-ttu-id="f7c0b-110">Yükleme için bir önkoşul olarak hello BCP komut satırı yardımcı programını toorun geçiş betikleri ve Office tooview hello uyumluluk raporu gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-110">As a prerequisite for installation, you will need hello BCP command-line utility toorun migration scripts and Office tooview hello compatibility report.</span></span> <span data-ttu-id="f7c0b-111">Merhaba aracı yüklenmeden önce hello başlattıktan sonra istendiğinde tooaccept standart EULA karşıdan yüklediğiniz yürütülebilir olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-111">After launching hello executable that is downloaded you will be prompted tooaccept a standard EULA before hello tool will be installed.</span></span>

<span data-ttu-id="f7c0b-112">Ayrıca, toorun hello geçiş Utiliy, bir hello toomigrate aradığınız hello veritabanında aşağıdaki izinleri: veritabanı oluşturma, ALTER ANY DATABASE veya Görünüm herhangi TANIMI.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-112">In addition, toorun hello Migration Utiliy, you will need hello one following permissions on hello database that you are looking toomigrate: CREATE DATABASE, ALTER ANY DATABASE or VIEW ANY DEFINITION.</span></span>

### <a name="launching-hello-tool-and-connecting"></a><span data-ttu-id="f7c0b-113">Merhaba aracı başlatarak ve bağlanma</span><span class="sxs-lookup"><span data-stu-id="f7c0b-113">Launching hello tool and connecting</span></span>
<span data-ttu-id="f7c0b-114">Post görünen hello Masaüstü simgesine tıklayarak başlatma hello aracını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-114">Launch hello tool by clicking on hello desktop icon which appears post install.</span></span> <span data-ttu-id="f7c0b-115">Merhaba aracı açıldığında, kaynak ve hedef hello geçiş aracı için seçebileceğiniz bir ilk bağlantı sayfasıyla istenir.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-115">Upon opening hello tool, you will be prompted with an initial connection page where you can choose your source and destination for hello migration tool.</span></span> <span data-ttu-id="f7c0b-116">Bu aşamada, SQL Server ve Azure SQL veritabanı kaynakları ve SQL Data Warehouse hedef olarak olarak destekliyoruz.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-116">At this time, we support SQL Server and Azure SQL Database as sources and SQL Data Warehouse as a destination.</span></span> <span data-ttu-id="f7c0b-117">Bu seçtikten sonra tooconnect tooyour kaynak sunucunun sunucu adını doldurma ve kimlik doğrulaması ve 'Bağlan' a tıklayarak istenir.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-117">After selecting this you will be asked tooconnect tooyour source server by filling in server name and authenticating and then clicking ‘Connect’.</span></span>

<span data-ttu-id="f7c0b-118">Kimlik doğrulandıktan sonra hello aracı bağlı hello sunucusunda mevcut olan veritabanlarının bir listesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-118">After authenticating, hello tool will show a list of databases that are present in hello server which you are connected to.</span></span> <span data-ttu-id="f7c0b-119">Toomigrate ve 'seçili geçirme üzerinde' e tıklayarak istediğiniz veritabanını seçerek hello geçişe başlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-119">You can begin hello migration by selecting a database that you would like toomigrate and then clicking on ‘Migrate selected’.</span></span>

## <a name="migration-report"></a><span data-ttu-id="f7c0b-120">Geçiş raporu</span><span class="sxs-lookup"><span data-stu-id="f7c0b-120">Migration report</span></span>
<span data-ttu-id="f7c0b-121">'Veritabanı uyumluluğu denetle' hello aracında seçerek tüm nesne uyumsuzlukları özetleyen bir rapor oluşturacağını hello veritabanında toomigrate istedi.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-121">Selecting ‘Check Database Compatibility’ in hello tool will generate a report summarizing all object incompatibilities in hello database you requested toomigrate.</span></span> <span data-ttu-id="f7c0b-122">Merhaba SQL veri ambarı'nda mevcut SQL Server işlevselliği bazıları daha geniş bir listesi bulunabilir bizim [geçiş belgeleri][migration documentation].</span><span class="sxs-lookup"><span data-stu-id="f7c0b-122">A broader list of some of hello SQL Server functionality that is not present in SQL Data Warehouse can be found in our [migration documentation][migration documentation].</span></span> <span data-ttu-id="f7c0b-123">Merhaba rapor oluşturulduktan sonra mümkün toosave ve Excel'de Aç hello rapor olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-123">After hello report is generated you will be able toosave and open hello report in Excel.</span></span>

<span data-ttu-id="f7c0b-124">Lütfen hello geçiş şeması, 'Nesnesi' siparişi tooallow hemen geçişte bu verilerin ayarlanacak olarak tanımlanan çoğu sorunların oluştururken unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-124">Please note that when generating hello migration schema, most issues identified as ‘Object’ will be adjusted in order tooallow immediate migration of that data.</span></span> <span data-ttu-id="f7c0b-125">Lütfen hello şema uygulamadan önce toomake ek ayarlamalar istemediğiniz hello değişiklikleri tooensure gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-125">Please review hello changes tooensure you do not want toomake additional adjustments before applying hello schema.</span></span>

## <a name="migrate-schema"></a><span data-ttu-id="f7c0b-126">Geçiş şeması</span><span class="sxs-lookup"><span data-stu-id="f7c0b-126">Migrate schema</span></span>
<span data-ttu-id="f7c0b-127">Bağlandıktan sonra geçirme'Schema ' seçerek hello seçili tablo için şema geçiş komut dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-127">After connecting, selecting ‘Migrate Schema’ will generate a schema migration script for hello selected tables.</span></span> <span data-ttu-id="f7c0b-128">Bu komut dosyası bağlantı noktalarını hello yapı Merhaba tablonun uyumlu veri türleri toomore uyumlu formları eşler ve bu hello geçiş ayarları hello kullanıcı tarafından belirtilirse, güvenlik kimlik bilgileri ve şema oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-128">This script ports hello structure of hello table, maps incompatible data types toomore compatible forms, and creates security credentials and schema if this is indicated by hello user in hello migration settings.</span></span> <span data-ttu-id="f7c0b-129">Bu kod hedeflenen hello SQL Data Warehouse örneğine karşı çalıştırabilirsiniz tooa dosyasını kaydettiğiniz tooyour Panoya kopyalanan veya daha fazla eylemi gerçekleştirmeden önce satır içi bile düzenlenebilir.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-129">This code can be run against hello targeted SQL Data Warehouse instance, saved tooa file, copied tooyour clipboard, or even edited in-line before taking further action.</span></span>  

<span data-ttu-id="f7c0b-130">Yukarıdaki şema gözden geçirme hello geçiş bu hello değiştiğinde belirtilenlerle aracı sipariş tooensure yaptı, tam olarak bunları anladığınızdan.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-130">As noted above, when migrating schema review hello migration changes that hello tool has made in order tooensure that that you fully understand them.</span></span>  

## <a name="migrate-data"></a><span data-ttu-id="f7c0b-131">Geçiş verileri</span><span class="sxs-lookup"><span data-stu-id="f7c0b-131">Migrate data</span></span>
<span data-ttu-id="f7c0b-132">Merhaba 'Verileri geçirmek' seçeneğini tıklatarak, veri ilk tooflat dosyalarınızı sunucunuzda, taşınır BCP komut dosyaları oluşturabilir ve ardından SQL veri ambarı doğrudan.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-132">By clicking hello ‘Migrate Data’ option you can generate BCP scripts that will move your data first tooflat files on your server, and then directly into your SQL Data Warehouse.</span></span> <span data-ttu-id="f7c0b-133">Küçük miktarda veri ve yeniden deneme olarak taşımak için bu işlemi yerleşik olmayan ve hataları hello ağ bağlantı kaybı oluşabilir öneririz.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-133">We recommend this process for moving small amounts of data and, as retries are not built-in and failures may occur if there is a loss of hello network connection.</span></span> <span data-ttu-id="f7c0b-134">İçinde toorun Bu sipariş, toohave hello BCP komut satırı yardımcı programının yüklü olması gerekir ve hello veri hello şeması zaten oluşturulmuş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-134">In order toorun this, you will need toohave hello BCP command-line utility installed and hello schema for hello data must already have been created.</span></span>

<span data-ttu-id="f7c0b-135">Out Parametreleri hello doldurduktan sonra tooclick geçiş çalıştırmanız yeterlidir ve iki paket kümesini oluşturulur tooyour belirtilen konum.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-135">After you have filled out hello parameters above you simply need tooclick run migration and a set of two packages will be generated tooyour specified location.</span></span> <span data-ttu-id="f7c0b-136">Merhaba dışarı aktarma dosyası sipariş tooexport verilerde geçiş kaynağınızdan düz dosyalarıyla çalıştırın ve hello içeri aktarma dosyası sipariş tooimport verilerinizi SQL Data Warehouse'a çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f7c0b-136">Run hello export file in order tooexport data from your migration source into flat files, and run hello import file in order tooimport your data into SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7c0b-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f7c0b-137">Next steps</span></span>
<span data-ttu-id="f7c0b-138">Bazı verileri geçirdikten, nasıl çok denetleyin[geliştirmek][develop].</span><span class="sxs-lookup"><span data-stu-id="f7c0b-138">Now that you've migrated some data, check out how too[develop][develop].</span></span>

<!--Image references-->

<!--Article references-->
[migration documentation]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md

<!--Other Web references--> 
[Download Migration Utility]: https://migrhoststorage.blob.core.windows.net/sqldwsample/DataWarehouseMigrationUtility.zip
