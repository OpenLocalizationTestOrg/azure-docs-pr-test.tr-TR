---
title: "aaaGetting zamana bağlı tablolarda Azure SQL veritabanı ile Başlarken | Microsoft Docs"
description: "Nasıl tooget zamana bağlı tablolarda Azure SQL veritabanı'nda kullanmaya öğrenin."
services: sql-database
documentationcenter: 
author: bonova
manager: jhubbard
editor: 
ms.assetid: c8c0f232-0751-4a7f-a36e-67a0b29fa1b8
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: sql-database
ms.date: 01/10/2017
ms.author: bonova
ms.openlocfilehash: 54f394b51df07aa2f9bb299f207e692171d23479
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="fea43-103">Zamana bağlı tablolarda Azure SQL veritabanı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="fea43-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="fea43-104">Zamana bağlı tablolarda tootrack sağlayan bir Azure SQL veritabanı'nın yeni bir programlama özelliğidir ve özel kodlama için hello gerek kalmadan, verilerde yapılan değişiklikler tam geçmişini hello analiz edin.</span><span class="sxs-lookup"><span data-stu-id="fea43-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you tootrack and analyze hello full history of changes in your data, without hello need for custom coding.</span></span> <span data-ttu-id="fea43-105">Böylece saklı bulguları yorumlanabilen zamana bağlı tablolarda veri yakından ilgili tootime bağlamı yalnızca hello belirli bir dönem içinde geçerli olarak tutun.</span><span class="sxs-lookup"><span data-stu-id="fea43-105">Temporal Tables keep data closely related tootime context so that stored facts can be interpreted as valid only within hello specific period.</span></span> <span data-ttu-id="fea43-106">Zamana bağlı tablolarda, bu özellik etkili zamana dayalı çözümleme ve veri evrimi alma ilişkin bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="fea43-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="fea43-107">Zamana bağlı senaryosu</span><span class="sxs-lookup"><span data-stu-id="fea43-107">Temporal Scenario</span></span>
<span data-ttu-id="fea43-108">Bu makalede, bir uygulama senaryosunda başlangıç adımları tooutilize zamana bağlı tablolarda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fea43-108">This article illustrates hello steps tooutilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="fea43-109">Tootrack kullanıcı etkinliği sıfırdan geliştirilen yeni bir Web sitesi ya da kullanıcı etkinliği analytics ile tooextend istediğiniz mevcut bir Web istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="fea43-109">Suppose that you want tootrack user activity on a new website that is being developed from scratch or on an existing website that you want tooextend with user activity analytics.</span></span> <span data-ttu-id="fea43-110">Bu basit örnekte, bir süre sırasında ziyaret ettiğiniz web sayfalarının hello sayısının yakalanan ve Azure SQL veritabanı üzerinde barındırılan hello Web sitesi veritabanında izlenen toobe gerektiren bir gösterge olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="fea43-110">In this simplified example, we assume that hello number of visited web pages during a period of time is an indicator that needs toobe captured and monitored in hello website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="fea43-111">kullanıcı etkinliği hello geçmiş çözümleme Hello amacı tooget girişleri tooredesign Web sitesidir ve hello ziyaretçiler için daha iyi deneyimi sağlamak.</span><span class="sxs-lookup"><span data-stu-id="fea43-111">hello goal of hello historical analysis of user activity is tooget inputs tooredesign website and provide better experience for hello visitors.</span></span>

<span data-ttu-id="fea43-112">Bu senaryo için Hello veritabanı modeli çok basit - kullanıcı etkinliği ölçüm bir tek tamsayı alanıyla temsil **PageVisited**ve hello kullanıcı profili temel bilgiler birlikte yakalanır.</span><span class="sxs-lookup"><span data-stu-id="fea43-112">hello database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on hello user profile.</span></span> <span data-ttu-id="fea43-113">Ayrıca, temel saat analizi için her satır belirli bir kullanıcının belirli bir dönem içinde ziyaret edilen sayfalar hello sayısı temsil ettiği satırları her kullanıcı için bir dizi engelleneceği.</span><span class="sxs-lookup"><span data-stu-id="fea43-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents hello number of pages a particular user visited within a specific period of time.</span></span>

![Şema](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="fea43-115">Neyse ki, tooput herhangi çaba, uygulama toomaintain gerekmez bu etkinliği bilgileri.</span><span class="sxs-lookup"><span data-stu-id="fea43-115">Fortunately, you do not need tooput any effort in your app toomaintain this activity information.</span></span> <span data-ttu-id="fea43-116">Zamana bağlı tablolar ile bu işlem - Web sitesi tasarımı ve hello veri analizi kendisi hakkında daha fazla zaman toofocus sırasında tam esneklik sağlayan otomatik hale getirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fea43-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time toofocus on hello data analysis itself.</span></span> <span data-ttu-id="fea43-117">yalnızca bir şey toodo sahip tooensure Merhaba, **WebSiteInfo** tablo olarak yapılandırılmış [zamana bağlı sistem sürümlü](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="fea43-117">hello only thing you have toodo is tooensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="fea43-118">Bu senaryoda Hello tam adımlar tooutilize zamana bağlı tablolarda aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fea43-118">hello exact steps tooutilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="fea43-119">1. adım: tabloları zamana bağlı olarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="fea43-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="fea43-120">Yeni yazılım geliştirme başlangıç mı var olan uygulama yükseltme bağlı olarak, zamana bağlı tablolarda oluşturun veya var olanları zamana bağlı öznitelikleri ekleyerek değiştirin.</span><span class="sxs-lookup"><span data-stu-id="fea43-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="fea43-121">Genel durumda senaryonuz iki bu seçeneklerin bir bileşimi olabilir.</span><span class="sxs-lookup"><span data-stu-id="fea43-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="fea43-122">Bunlar gerçekleştirmek eylemini kullanarak [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS) [SQL Server veri Araçları](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) veya başka bir Transact-SQL geliştirme aracıdır.</span><span class="sxs-lookup"><span data-stu-id="fea43-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fea43-123">Her zaman hello kullanmanız önerilir Management Studio tooremain en son sürümünü Azure ve SQL veritabanı güncelleştirmeleri tooMicrosoft ile eşitlenir.</span><span class="sxs-lookup"><span data-stu-id="fea43-123">It is recommended that you always use hello latest version of Management Studio tooremain synchronized with updates tooMicrosoft Azure and SQL Database.</span></span> <span data-ttu-id="fea43-124">[SQL Server Management Studio’yu güncelleyin](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="fea43-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="fea43-125">Yeni Tablo Oluştur</span><span class="sxs-lookup"><span data-stu-id="fea43-125">Create new table</span></span>
<span data-ttu-id="fea43-126">SSMS Nesne Gezgini tooopen hello sorgu Düzenleyicisi'nde bağlam menüsü öğesini "Yeni sistem sürümlü tablo" ile bir zamana bağlı tablo şablonu komut dosyası kullanın ve ardından "Değerleri için şablon parametrelerini belirt" (Ctrl + Shift + M) toopopulate hello şablonu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fea43-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer tooopen hello query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) toopopulate hello template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="fea43-128">SSDT içinde yeni öğeleri toohello veritabanı projesi eklerken "(sistem sürümü tutulan) zamana bağlı tablo" Şablon seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="fea43-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items toohello database project.</span></span> <span data-ttu-id="fea43-129">Açık Tablo Tasarımcısı ve etkinleştirme, tooeasily belirtin Tablo düzeni hello olduğunu:</span><span class="sxs-lookup"><span data-stu-id="fea43-129">That will open table designer and enable you tooeasily specify hello table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="fea43-131">Ayrıca bir oluşturma zamana bağlı tablo hello Transact-SQL deyimlerini doğrudan belirterek hello aşağıdaki örnekte gösterildiği gibi erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fea43-131">You can also a create temporal table by specifying hello Transact-SQL statements directly, as shown in hello example below.</span></span> <span data-ttu-id="fea43-132">Her zamana bağlı tabloda zorunlu öğeleri Hello hello süre tanımının ve geçmiş satır sürümleri depolayacak bir başvuru tooanother kullanıcı tablosu ile Merhaba system_versıonıng yan tümcesini olduğuna dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="fea43-132">Note that hello mandatory elements of every temporal table are hello PERIOD definition and hello SYSTEM_VERSIONING clause with a reference tooanother user table that will store historical row versions:</span></span>

````
CREATE TABLE WebsiteUserInfo 
(  
    [UserID] int NOT NULL PRIMARY KEY CLUSTERED 
  , [UserName] nvarchar(100) NOT NULL
  , [PagesVisited] int NOT NULL 
  , [ValidFrom] datetime2 (0) GENERATED ALWAYS AS ROW START
  , [ValidTo] datetime2 (0) GENERATED ALWAYS AS ROW END
  , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo)
 )  
 WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
````

<span data-ttu-id="fea43-133">Sistem sürümü tutulan zamana bağlı tablo oluşturduğunuzda, geçmiş tablosu hello varsayılan yapılandırması ile birlikte gelen hello otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fea43-133">When you create system-versioned temporal table, hello accompanying history table with hello default configuration is automatically created.</span></span> <span data-ttu-id="fea43-134">Merhaba varsayılan geçmiş tablosu sayfası sıkıştırma ile Merhaba dönem sütunlarında (end, start) bir kümelenmiş B-Ağacı dizini içerir.</span><span class="sxs-lookup"><span data-stu-id="fea43-134">hello default history table contains a clustered B-tree index on hello period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="fea43-135">Bu yapılandırma en iyi zamana bağlı tablolarda kullanılan senaryoları hello çoğunluğu için özellikle de [verileri denetleme](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="fea43-135">This configuration is optimal for hello majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="fea43-136">Merhaba depolama hello geçmiş tablosu için kümelenmiş columnstore dizini seçimdir şekilde bu özel durumda biz tooperform zamana dayalı eğilim analizi üzerinden uzun bir veri geçmişini ve büyük veri kümeleriyle hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="fea43-136">In this particular case, we aim tooperform time-based trend analysis over a longer data history and with bigger data sets, so hello storage choice for hello history table is a clustered columnstore index.</span></span> <span data-ttu-id="fea43-137">Kümelenmiş columnstore çok iyi sıkıştırma ve analitik sorguları için performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="fea43-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="fea43-138">Esneklik tooconfigure dizinleri hello geçerli ve zamana bağlı tablolarda tamamen bağımsız olarak hello zamana bağlı tablolar verin.</span><span class="sxs-lookup"><span data-stu-id="fea43-138">Temporal Tables give you hello flexibility tooconfigure indexes on hello current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="fea43-139">Columnstore dizinleri yalnızca hello premium hizmet katmanında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fea43-139">Columnstore indexes are only available in hello premium service tier.</span></span>
>

<span data-ttu-id="fea43-140">komut dosyası izleyen hello varsayılan dizini geçmiş tablosu değişen toohello kümelenmiş columnstore nasıl olabilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="fea43-140">hello following script shows how default index on history table can be changed toohello clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="fea43-141">Geçmiş tablosu bir alt düğüm olarak görüntülendiği sırada zamana bağlı tablolarda hello Nesne Gezgini daha kolay tanımlama için hello belirli simgesiyle gösterilir.</span><span class="sxs-lookup"><span data-stu-id="fea43-141">Temporal Tables are represented in hello Object Explorer with hello specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-tootemporal"></a><span data-ttu-id="fea43-143">Var olan tablo tootemporal alter</span><span class="sxs-lookup"><span data-stu-id="fea43-143">Alter existing table tootemporal</span></span>
<span data-ttu-id="fea43-144">Şimdi hangi hello WebsiteUserInfo tablo zaten var, ancak tasarlanmış tookeep değişikliklerin geçmişini değildi hello alternatif senaryo kapsar.</span><span class="sxs-lookup"><span data-stu-id="fea43-144">Let’s cover hello alternative scenario in which hello WebsiteUserInfo table already exists, but was not designed tookeep a history of changes.</span></span> <span data-ttu-id="fea43-145">Bu durumda, yalnızca hello var olan tablo toobecome hello örnek aşağıdaki gösterildiği gibi zamana bağlı genişletebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fea43-145">In this case, you can simply extend hello existing table toobecome temporal, as shown in hello following example:</span></span>

````
ALTER TABLE WebsiteUserInfo 
ADD 
    ValidFrom datetime2 (0) GENERATED ALWAYS AS ROW START HIDDEN  
        constraint DF_ValidFrom DEFAULT DATEADD(SECOND, -1, SYSUTCDATETIME())
    , ValidTo datetime2 (0)  GENERATED ALWAYS AS ROW END HIDDEN   
        constraint DF_ValidTo DEFAULT '9999.12.31 23:59:59.99'
    , PERIOD FOR SYSTEM_TIME (ValidFrom, ValidTo); 

ALTER TABLE WebsiteUserInfo  
SET (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.WebsiteUserInfoHistory));
GO

CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="fea43-146">2. adım: İş yükünüzün düzenli olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="fea43-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="fea43-147">zamana bağlı tablolarda Hello ana avantajı, değil toochange gerekir veya herhangi bir şekilde tooperform değişiklik izleme, Web sitenizi ayarlama olması.</span><span class="sxs-lookup"><span data-stu-id="fea43-147">hello main advantage of Temporal Tables is that you do not need toochange or adjust your website in any way tooperform change tracking.</span></span> <span data-ttu-id="fea43-148">Değişiklikler, verilerinizde gerçekleştirilecek her zaman oluşturduktan sonra zamana bağlı tablolarda saydam önceki satır sürümleri kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="fea43-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="fea43-149">Sipariş tooleverage otomatik değişiklik izleme, bu belirli bir senaryo için şirketinizdeki yalnızca sütun güncelleştirme **PagesVisited** kullanıcı hello Web sitesinde her/his oturumu sona erdiğinde her zaman:</span><span class="sxs-lookup"><span data-stu-id="fea43-149">In order tooleverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on hello website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="fea43-150">Güncelleştirme sorgusu hello toonotice tooknow hello tam zaman hello gerçek işlemi oluştuğunda veya geçmiş verileri gelecekteki analize korunacak nasıl gerek duymaz önemlidir.</span><span class="sxs-lookup"><span data-stu-id="fea43-150">It is important toonotice that hello update query doesn’t need tooknow hello exact time when hello actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="fea43-151">Her iki yönlerini hello Azure SQL veritabanı tarafından otomatik olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="fea43-151">Both aspects are automatically handled by hello Azure SQL Database.</span></span> <span data-ttu-id="fea43-152">Merhaba Aşağıdaki diyagramda geçmiş verileri üzerindeki her bir güncelleştirme nasıl üretiliyor gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="fea43-152">hello following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="fea43-154">3. adım: geçmiş veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="fea43-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="fea43-155">Zamana bağlı sistem sürümü oluşturma etkin olduğunda, geçmiş verileri çözümleme, uzakta yalnızca bir sorgu sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="fea43-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="fea43-156">Bu makalede, biz ortak analiz - toolearn senaryosu birkaç örnek tüm ayrıntıları sağlayın, hello ile sunulan çeşitli seçenekleriniz keşfetme [FOR system_tıme](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="fea43-156">In this article, we will provide a few examples that address common analysis scenarios - toolearn all details, explore various options introduced with hello [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="fea43-157">itibariyle bir saatten önce ziyaret edilen web sayfalarını hello sayısına göre sıralanmış toosee hello ilk 10 kullanıcılar bu sorguyu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="fea43-157">toosee hello top 10 users ordered by hello number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="fea43-158">Bu sorgu kolayca değiştirebilirsiniz tooanalyze hello sitesini ziyaret gün önce itibariyle bir ay önce veya hello geçmiş herhangi bir noktada istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="fea43-158">You can easily modify this query tooanalyze hello site visits as of a day ago, a month ago or at any point in hello past you wish.</span></span>

<span data-ttu-id="fea43-159">önceki gün tooperform temel istatistiksel çözümleme hello için aşağıdaki örneğine hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="fea43-159">tooperform basic statistical analysis for hello previous day, use hello following example:</span></span>

````
DECLARE @twoDaysAgo datetime2 = DATEADD(DAY, -2, SYSUTCDATETIME());
DECLARE @aDayAgo datetime2 = DATEADD(DAY, -1, SYSUTCDATETIME());

SELECT UserID, SUM (PagesVisited) as TotalVisitedPages, AVG (PagesVisited) as AverageVisitedPages,
MAX (PagesVisited) AS MaxVisitedPages, MIN (PagesVisited) AS MinVisitedPages,
STDEV (PagesVisited) as StDevViistedPages
FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME BETWEEN @twoDaysAgo AND @aDayAgo
GROUP BY UserId
````

<span data-ttu-id="fea43-160">toosearch belirli bir kullanıcının bir süre, kullanım hello KAPSANAN yan tümcesi içindeki etkinlikler için:</span><span class="sxs-lookup"><span data-stu-id="fea43-160">toosearch for activities of a specific user, within a period of time, use hello CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="fea43-161">Eğilimleri ve kullanım düzenlerini sezgisel bir yolla kolayca gösterebilirsiniz gibi grafik görselleştirme zamana bağlı sorguları için özellikle kullanışlıdır:</span><span class="sxs-lookup"><span data-stu-id="fea43-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="fea43-163">Tablo şemasını gelişen</span><span class="sxs-lookup"><span data-stu-id="fea43-163">Evolving table schema</span></span>
<span data-ttu-id="fea43-164">Genellikle, uygulama geliştirme yaparken toochange hello zamana bağlı tablo şemasını gerekir.</span><span class="sxs-lookup"><span data-stu-id="fea43-164">Typically, you will need toochange hello temporal table schema while you are doing app development.</span></span> <span data-ttu-id="fea43-165">Yalnızca normal ALTER TABLE deyimleri çalıştırın ve Azure SQL veritabanı uygun şekilde değişiklikleri toohello geçmiş tablosu yayılır.</span><span class="sxs-lookup"><span data-stu-id="fea43-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes toohello history table.</span></span> <span data-ttu-id="fea43-166">Merhaba aşağıdaki betiği izleme için ek öznitelik nasıl ekleyebileceğiniz gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="fea43-166">hello following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="fea43-167">Benzer şekilde, iş yükünüzü etkinken sütun tanımı değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fea43-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase hello length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="fea43-168">Son olarak, artık ihtiyacınız olmayan bir sütun kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fea43-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="fea43-169">Alternatif olarak, en son kullanın [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange zamana bağlı tablo şeması bağlı toohello veritabanı (çevrimiçi mod) durumdayken veya hello veritabanı projesi (Çevrimdışı mod) bir parçası olarak.</span><span class="sxs-lookup"><span data-stu-id="fea43-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) toochange temporal table schema while you are connected toohello database (online mode) or as part of hello database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="fea43-170">Geçmiş verilerin bekletilmesini denetleme</span><span class="sxs-lookup"><span data-stu-id="fea43-170">Controlling retention of historical data</span></span>
<span data-ttu-id="fea43-171">Sistem sürümü tutulan zamana bağlı tablolarda ile Merhaba geçmiş tablosu normal tablolardaki'birden fazla hello veritabanı boyutunu artırabilir.</span><span class="sxs-lookup"><span data-stu-id="fea43-171">With system-versioned temporal tables, hello history table may increase hello database size more than regular tables.</span></span> <span data-ttu-id="fea43-172">Büyük ve sürekli büyüyen geçmiş tablosu, hem toopure depolama maliyetleri yanı sıra bir performans etkileyici son zamana bağlı sorgulama vergi bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="fea43-172">A large and ever-growing history table can become an issue both due toopure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="fea43-173">Bu nedenle, hello geçmiş tablosundaki verileri yönetmek için bir veri bekletme ilkesi geliştirme planlama ve her zamana bağlı tablo hello yaşam döngüsü yönetiminden önemli bir özelliği olan.</span><span class="sxs-lookup"><span data-stu-id="fea43-173">Hence, developing a data retention policy for managing data in hello history table is an important aspect of planning and managing hello lifecycle of every temporal table.</span></span> <span data-ttu-id="fea43-174">Azure SQL veritabanı ile yaklaşımlar hello zamana bağlı tabloda geçmiş verileri yönetmek için aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="fea43-174">With Azure SQL Database, you have hello following approaches for managing historical data in hello temporal table:</span></span>

* [<span data-ttu-id="fea43-175">Tablo bölümleme</span><span class="sxs-lookup"><span data-stu-id="fea43-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="fea43-176">Özel temizleme betiğini</span><span class="sxs-lookup"><span data-stu-id="fea43-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="fea43-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fea43-177">Next steps</span></span>
<span data-ttu-id="fea43-178">Zamana bağlı tablolarda hakkında ayrıntılı bilgi için kullanıma [MSDN belgelerine](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="fea43-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="fea43-179">Ziyaret kanal 9 toohear bir [gerçek müşteri zamana bağlı implemenation başarı Öykü](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) ve izleme bir [zamana bağlı tanıtım canlı](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="fea43-179">Visit Channel 9 toohear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

