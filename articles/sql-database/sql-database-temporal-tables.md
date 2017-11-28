---
title: "Zamana bağlı tablolarda Azure SQL veritabanı ile çalışmaya başlama | Microsoft Docs"
description: "Azure SQL veritabanı'nda zamana bağlı tablolarda kullanmaya başlamanıza öğrenin."
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
ms.openlocfilehash: d84db682089c65c2716d2d9bd92f7bc0ac47af27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-temporal-tables-in-azure-sql-database"></a><span data-ttu-id="34c2c-103">Zamana bağlı tablolarda Azure SQL veritabanı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="34c2c-103">Getting Started with Temporal Tables in Azure SQL Database</span></span>
<span data-ttu-id="34c2c-104">Zamana bağlı tablolarda, izlemek ve özel kodlama için gerek kalmadan, verilerde yapılan değişiklikler tam geçmişini çözümlemek izin veren Azure SQL veritabanı'nın yeni bir programlama özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-104">Temporal Tables are a new programmability feature of Azure SQL Database that allows you to track and analyze the full history of changes in your data, without the need for custom coding.</span></span> <span data-ttu-id="34c2c-105">Zamana bağlı tablolarda yalnızca belirli bir dönem içinde depolanan bulguları yorumlanabilen böylece zaman bağlamına yakından ilgili veriler geçerli olarak tutun.</span><span class="sxs-lookup"><span data-stu-id="34c2c-105">Temporal Tables keep data closely related to time context so that stored facts can be interpreted as valid only within the specific period.</span></span> <span data-ttu-id="34c2c-106">Zamana bağlı tablolarda, bu özellik etkili zamana dayalı çözümleme ve veri evrimi alma ilişkin bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="34c2c-106">This property of Temporal Tables allows for efficient time-based analysis and getting insights from data evolution.</span></span>

## <a name="temporal-scenario"></a><span data-ttu-id="34c2c-107">Zamana bağlı senaryosu</span><span class="sxs-lookup"><span data-stu-id="34c2c-107">Temporal Scenario</span></span>
<span data-ttu-id="34c2c-108">Bu makalede, zamana bağlı tablolarda bir uygulama senaryosunda kullanmak için adımları gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-108">This article illustrates the steps to utilize Temporal Tables in an application scenario.</span></span> <span data-ttu-id="34c2c-109">Sıfırdan geliştirilen yeni bir Web sitesi ya da kullanıcı etkinliği analytics ile genişletmek istediğiniz mevcut bir Web kullanıcı etkinliğini izlemek istediğinizi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="34c2c-109">Suppose that you want to track user activity on a new website that is being developed from scratch or on an existing website that you want to extend with user activity analytics.</span></span> <span data-ttu-id="34c2c-110">Bu basit örnekte, bir süre sırasında ziyaret ettiğiniz web sayfalarının sayısının yakalanan ve Azure SQL veritabanı üzerinde barındırılan Web sitesi veritabanında izlenen gerekir bir gösterge olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="34c2c-110">In this simplified example, we assume that the number of visited web pages during a period of time is an indicator that needs to be captured and monitored in the website database that is hosted on Azure SQL Database.</span></span> <span data-ttu-id="34c2c-111">Kullanıcı etkinliği geçmiş çözümleme amacı, Web sitesi yeniden tasarlama ve ziyaretçilere daha iyi deneyimi sağlamak için girişleri almaktır.</span><span class="sxs-lookup"><span data-stu-id="34c2c-111">The goal of the historical analysis of user activity is to get inputs to redesign website and provide better experience for the visitors.</span></span>

<span data-ttu-id="34c2c-112">Bu senaryo için veritabanı modeli oldukça basittir - kullanıcı etkinliği ölçüm bir tek tamsayı alanıyla temsil **PageVisited**ve kullanıcı profilini temel bilgiler birlikte yakalanır.</span><span class="sxs-lookup"><span data-stu-id="34c2c-112">The database model for this scenario is very simple - user activity metric is represented with a single integer field, **PageVisited**, and is captured along with basic information on the user profile.</span></span> <span data-ttu-id="34c2c-113">Ayrıca, temel saat analizi için her satır, belirli bir kullanıcının belirli bir dönem içinde ziyaret sayfaların sayısını temsil ettiği satırları her kullanıcı için bir dizi engelleneceği.</span><span class="sxs-lookup"><span data-stu-id="34c2c-113">Additionally, for time based analysis, you would keep a series of rows for each user, where every row represents the number of pages a particular user visited within a specific period of time.</span></span>

![Şema](./media/sql-database-temporal-tables/AzureTemporal1.png)

<span data-ttu-id="34c2c-115">Neyse ki, bu etkinlik bilgileri korumak için uygulamanızda herhangi çaba put gerekmez.</span><span class="sxs-lookup"><span data-stu-id="34c2c-115">Fortunately, you do not need to put any effort in your app to maintain this activity information.</span></span> <span data-ttu-id="34c2c-116">Zamana bağlı tablolar ile bu işlem - Web sitesi tasarımı ve daha fazla zaman veri analizi kendisini odaklanmaya sırasında tam esneklik sağlayan otomatik hale getirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-116">With Temporal Tables, this process is automated - giving you full flexibility during website design and more time to focus on the data analysis itself.</span></span> <span data-ttu-id="34c2c-117">Emin olmak için yapmanız gereken tek şey. **WebSiteInfo** tablo olarak yapılandırılmış [zamana bağlı sistem sürümlü](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="34c2c-117">The only thing you have to do is to ensure that **WebSiteInfo** table is configured as [temporal system-versioned](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_0).</span></span> <span data-ttu-id="34c2c-118">Bu senaryoda, zamana bağlı tablolarda faydalanmak için uygulanacak adımlar aşağıda açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="34c2c-118">The exact steps to utilize Temporal Tables in this scenario are described below.</span></span>

## <a name="step-1-configure-tables-as-temporal"></a><span data-ttu-id="34c2c-119">1. adım: tabloları zamana bağlı olarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="34c2c-119">Step 1: Configure tables as temporal</span></span>
<span data-ttu-id="34c2c-120">Yeni yazılım geliştirme başlangıç mı var olan uygulama yükseltme bağlı olarak, zamana bağlı tablolarda oluşturun veya var olanları zamana bağlı öznitelikleri ekleyerek değiştirin.</span><span class="sxs-lookup"><span data-stu-id="34c2c-120">Depending on whether you are starting new development or upgrading existing application, you will either create temporal tables or modify existing ones by adding temporal attributes.</span></span> <span data-ttu-id="34c2c-121">Genel durumda senaryonuz iki bu seçeneklerin bir bileşimi olabilir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-121">In general case, your scenario can be a mix of these two options.</span></span> <span data-ttu-id="34c2c-122">Bunlar gerçekleştirmek eylemini kullanarak [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS) [SQL Server veri Araçları](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) veya başka bir Transact-SQL geliştirme aracıdır.</span><span class="sxs-lookup"><span data-stu-id="34c2c-122">Perform these action using [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) (SSMS), [SQL Server Data Tools](https://msdn.microsoft.com/library/mt204009.aspx) (SSDT) or any other Transact-SQL development tool.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="34c2c-123">Microsoft Azure ve SQL Veritabanı güncelleştirmeleriyle aynı sürümde olmak için her zaman en güncel Management Studio sürümünü kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-123">It is recommended that you always use the latest version of Management Studio to remain synchronized with updates to Microsoft Azure and SQL Database.</span></span> <span data-ttu-id="34c2c-124">[SQL Server Management Studio’yu güncelleyin](https://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="34c2c-124">[Update SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx).</span></span>
> 
> 

### <a name="create-new-table"></a><span data-ttu-id="34c2c-125">Yeni Tablo Oluştur</span><span class="sxs-lookup"><span data-stu-id="34c2c-125">Create new table</span></span>
<span data-ttu-id="34c2c-126">Bağlam menüsü öğesini "Yeni sistem sürümlü tablo" SSMS nesne Gezgini'nde bir zamana bağlı tablo şablonu komut dosyasıyla sorgu Düzenleyicisi'ni açın ve şablon doldurmak için "Değerler için şablon parametrelerini belirt" (Ctrl + Shift + M) kullanmak için kullanın:</span><span class="sxs-lookup"><span data-stu-id="34c2c-126">Use context menu item “New System-Versioned Table” in SSMS Object Explorer to open the query editor with a temporal table template script and then use “Specify Values for Template Parameters” (Ctrl+Shift+M) to populate the template:</span></span>

![SSMSNewTable](./media/sql-database-temporal-tables/AzureTemporal2.png)

<span data-ttu-id="34c2c-128">Yeni öğe için veritabanı projesi eklerken SSDT içinde "(sistem sürümü tutulan) zamana bağlı tablo" Şablon seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="34c2c-128">In SSDT, chose “Temporal Table (System-Versioned)” template when adding new items to the database project.</span></span> <span data-ttu-id="34c2c-129">Bu Tablo Tasarımcısı'nı açın ve kolayca Tablo düzeni belirtmenize olanak sağlar:</span><span class="sxs-lookup"><span data-stu-id="34c2c-129">That will open table designer and enable you to easily specify the table layout:</span></span>

![SSDTNewTable](./media/sql-database-temporal-tables/AzureTemporal3.png)

<span data-ttu-id="34c2c-131">Ayrıca bir oluşturma zamana bağlı tablo Transact-SQL deyimlerini doğrudan belirterek aşağıdaki örnekte gösterildiği gibi erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34c2c-131">You can also a create temporal table by specifying the Transact-SQL statements directly, as shown in the example below.</span></span> <span data-ttu-id="34c2c-132">Her zamana bağlı tabloda zorunlu öğelerini süre tanımının ve geçmiş satır sürümlerini depolamak başka bir kullanıcı tablosu başvuru system_versıonıng yan tümcesini olduğuna dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="34c2c-132">Note that the mandatory elements of every temporal table are the PERIOD definition and the SYSTEM_VERSIONING clause with a reference to another user table that will store historical row versions:</span></span>

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

<span data-ttu-id="34c2c-133">Sistem sürümü tutulan zamana bağlı tablo oluşturduğunuzda eşlik eden geçmiş tablosu varsayılan yapılandırması otomatik olarak oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="34c2c-133">When you create system-versioned temporal table, the accompanying history table with the default configuration is automatically created.</span></span> <span data-ttu-id="34c2c-134">Varsayılan geçmiş tablosu sayfası sıkıştırmayı etkin dönem sütunlarında (end, start) bir kümelenmiş B-Ağacı dizini içerir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-134">The default history table contains a clustered B-tree index on the period columns (end, start) with page compression enabled.</span></span> <span data-ttu-id="34c2c-135">Bu yapılandırma en iyi zamana bağlı tablolarda kullanılan senaryoları çoğunluğu için özellikle de [verileri denetleme](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span><span class="sxs-lookup"><span data-stu-id="34c2c-135">This configuration is optimal for the majority of scenarios in which temporal tables are used, especially for [data auditing](https://msdn.microsoft.com/library/mt631669.aspx#Anchor_0).</span></span> 

<span data-ttu-id="34c2c-136">Bu özel durumda biz depolama için geçmiş tablosu kümelenmiş columnstore dizini seçimdir şekilde zamana dayalı eğilim analizi üzerinden uzun bir veri geçmişini ve büyük veri kümeleriyle gerçekleştirmek için hedefleyin.</span><span class="sxs-lookup"><span data-stu-id="34c2c-136">In this particular case, we aim to perform time-based trend analysis over a longer data history and with bigger data sets, so the storage choice for the history table is a clustered columnstore index.</span></span> <span data-ttu-id="34c2c-137">Kümelenmiş columnstore çok iyi sıkıştırma ve analitik sorguları için performans sağlar.</span><span class="sxs-lookup"><span data-stu-id="34c2c-137">A clustered columnstore provides very good compression and performance for analytical queries.</span></span> <span data-ttu-id="34c2c-138">Zamana bağlı tablolarda geçerli ve zamana bağlı tablolarda tamamen bağımsız olarak Dizinleri'ni esnekliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="34c2c-138">Temporal Tables give you the flexibility to configure indexes on the current and temporal tables completely independently.</span></span> 

> [!NOTE]
> <span data-ttu-id="34c2c-139">Columnstore dizinleri yalnızca premium hizmet katmanında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-139">Columnstore indexes are only available in the premium service tier.</span></span>
>

<span data-ttu-id="34c2c-140">Aşağıdaki komut dosyasında varsayılan dizini geçmiş tablosu kümelenmiş columnstore nasıl değiştirilebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="34c2c-140">The following script shows how default index on history table can be changed to the clustered columnstore:</span></span>

````
CREATE CLUSTERED COLUMNSTORE INDEX IX_WebsiteUserInfoHistory
ON dbo.WebsiteUserInfoHistory
WITH (DROP_EXISTING = ON); 
````

<span data-ttu-id="34c2c-141">Geçmiş tablosu bir alt düğüm olarak görüntülendiği sırada zamana bağlı tablolarda daha kolay tanımlama için belirli simgesiyle nesne Gezgini'nde temsil edilir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-141">Temporal Tables are represented in the Object Explorer with the specific icon for easier identification, while its history table is displayed as a child node.</span></span>

![AlterTable](./media/sql-database-temporal-tables/AzureTemporal4.png)

### <a name="alter-existing-table-to-temporal"></a><span data-ttu-id="34c2c-143">Zamana bağlı için var olan tablo değiştirme</span><span class="sxs-lookup"><span data-stu-id="34c2c-143">Alter existing table to temporal</span></span>
<span data-ttu-id="34c2c-144">Şimdi, WebsiteUserInfo tablo zaten var, ancak değişikliklerin geçmişini tutmak için tasarlanmamıştır alternatif senaryo kapsar.</span><span class="sxs-lookup"><span data-stu-id="34c2c-144">Let’s cover the alternative scenario in which the WebsiteUserInfo table already exists, but was not designed to keep a history of changes.</span></span> <span data-ttu-id="34c2c-145">Bu durumda, aşağıdaki örnekte gösterildiği gibi zamana bağlı, olmasını varolan tablonun yalnızca genişletebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34c2c-145">In this case, you can simply extend the existing table to become temporal, as shown in the following example:</span></span>

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

## <a name="step-2-run-your-workload-regularly"></a><span data-ttu-id="34c2c-146">2. adım: İş yükünüzün düzenli olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="34c2c-146">Step 2: Run your workload regularly</span></span>
<span data-ttu-id="34c2c-147">Zamana bağlı tablolarda ana avantajı, Web sitenizi değişiklik izlemeyi gerçekleştirmek için herhangi bir şekilde ayarlamak veya değiştirmek gerekmez ' dir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-147">The main advantage of Temporal Tables is that you do not need to change or adjust your website in any way to perform change tracking.</span></span> <span data-ttu-id="34c2c-148">Değişiklikler, verilerinizde gerçekleştirilecek her zaman oluşturduktan sonra zamana bağlı tablolarda saydam önceki satır sürümleri kalıcı olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="34c2c-148">Once created, Temporal Tables transparently persist previous row versions every time you perform modifications on your data.</span></span> 

<span data-ttu-id="34c2c-149">Otomatik değişiklik izleme bu belirli bir senaryo için kullanılabilmesi için şirketinizdeki yalnızca sütun güncelleştirme **PagesVisited** kullanıcı Web sitesinde her/his oturumu sona erdiğinde her zaman:</span><span class="sxs-lookup"><span data-stu-id="34c2c-149">In order to leverage automatic change tracking for this particular scenario, let’s just update column **PagesVisited** every time when user ends her/his session on the website:</span></span>

````
UPDATE WebsiteUserInfo  SET [PagesVisited] = 5 
WHERE [UserID] = 1;
````

<span data-ttu-id="34c2c-150">Güncelleştirme sorgusu tam zaman gerçek işlemi oluştuğunda veya geçmiş verileri gelecekteki analize korunacak nasıl bilmesi gerekmez fark önemlidir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-150">It is important to notice that the update query doesn’t need to know the exact time when the actual operation occurred nor how historical data will be preserved for future analysis.</span></span> <span data-ttu-id="34c2c-151">Her iki yönlerini otomatik olarak Azure SQL veritabanı tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-151">Both aspects are automatically handled by the Azure SQL Database.</span></span> <span data-ttu-id="34c2c-152">Aşağıdaki diyagram, geçmiş verileri üzerindeki her bir güncelleştirme oluşturulan nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-152">The following diagram illustrates how history data is being generated on every update.</span></span>

![TemporalArchitecture](./media/sql-database-temporal-tables/AzureTemporal5.png)

## <a name="step-3-perform-historical-data-analysis"></a><span data-ttu-id="34c2c-154">3. adım: geçmiş veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="34c2c-154">Step 3: Perform historical data analysis</span></span>
<span data-ttu-id="34c2c-155">Zamana bağlı sistem sürümü oluşturma etkin olduğunda, geçmiş verileri çözümleme, uzakta yalnızca bir sorgu sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="34c2c-155">Now when temporal system-versioning is enabled, historical data analysis is just one query away from you.</span></span> <span data-ttu-id="34c2c-156">Bu makalede, söz tüm ayrıntıları öğrenmek için çeşitli seçenekler ile sunulan keşfedin ortak analiz - senaryosu birkaç örnek sağlarız [FOR system_tıme](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) yan tümcesi.</span><span class="sxs-lookup"><span data-stu-id="34c2c-156">In this article, we will provide a few examples that address common analysis scenarios - to learn all details, explore various options introduced with the [FOR SYSTEM_TIME](https://msdn.microsoft.com/library/dn935015.aspx#Anchor_3) clause.</span></span>

<span data-ttu-id="34c2c-157">Bir saatten önce itibariyle ziyaret edilen web sayfalarının sayısı bazında ilk 10 kullanıcılar görmek için bu sorguyu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="34c2c-157">To see the top 10 users ordered by the number of visited web pages as of an hour ago, run this query:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
SELECT TOP 10 * FROM dbo.WebsiteUserInfo FOR SYSTEM_TIME AS OF @hourAgo
ORDER BY PagesVisited DESC
````

<span data-ttu-id="34c2c-158">Geçmişteki herhangi bir noktada, istediğiniz veya bir ay önce bir gün önce itibariyle site ziyaret çözümlemek için bu sorguyu kolayca değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34c2c-158">You can easily modify this query to analyze the site visits as of a day ago, a month ago or at any point in the past you wish.</span></span>

<span data-ttu-id="34c2c-159">Önceki gün için temel istatistiksel analizler yapmak için aşağıdaki örneği kullanın:</span><span class="sxs-lookup"><span data-stu-id="34c2c-159">To perform basic statistical analysis for the previous day, use the following example:</span></span>

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

<span data-ttu-id="34c2c-160">Bir süre sonunda süresi, belirli bir kullanıcı etkinlikleri için aranacak bulunan yan tümcesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="34c2c-160">To search for activities of a specific user, within a period of time, use the CONTAINED IN clause:</span></span>

````
DECLARE @hourAgo datetime2 = DATEADD(HOUR, -1, SYSUTCDATETIME());
DECLARE @twoHoursAgo datetime2 = DATEADD(HOUR, -2, SYSUTCDATETIME());
SELECT * FROM dbo.WebsiteUserInfo 
FOR SYSTEM_TIME CONTAINED IN (@twoHoursAgo, @hourAgo)
WHERE [UserID] = 1;
````

<span data-ttu-id="34c2c-161">Eğilimleri ve kullanım düzenlerini sezgisel bir yolla kolayca gösterebilirsiniz gibi grafik görselleştirme zamana bağlı sorguları için özellikle kullanışlıdır:</span><span class="sxs-lookup"><span data-stu-id="34c2c-161">Graphic visualization is especially convenient for temporal queries as you can show trends and usage patterns in an intuitive way very easily:</span></span>

![TemporalGraph](./media/sql-database-temporal-tables/AzureTemporal6.png)

## <a name="evolving-table-schema"></a><span data-ttu-id="34c2c-163">Tablo şemasını gelişen</span><span class="sxs-lookup"><span data-stu-id="34c2c-163">Evolving table schema</span></span>
<span data-ttu-id="34c2c-164">Genellikle, uygulama geliştirme yaparken zamana bağlı tablo şemasını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-164">Typically, you will need to change the temporal table schema while you are doing app development.</span></span> <span data-ttu-id="34c2c-165">Bunun için çalıştırmanız yeterlidir normal ALTER TABLE deyimleri ve Azure SQL veritabanı uygun şekilde geçmiş tablosu değişiklikleri yayılır.</span><span class="sxs-lookup"><span data-stu-id="34c2c-165">For that, simply run regular ALTER TABLE statements and Azure SQL Database will appropriately propagate changes to the history table.</span></span> <span data-ttu-id="34c2c-166">Aşağıdaki komut dosyası, izleme için ek öznitelik nasıl ekleyebileceğiniz gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="34c2c-166">The following script shows how you can add additional attribute for tracking:</span></span>

````
/*Add new column for tracking source IP address*/
ALTER TABLE dbo.WebsiteUserInfo 
ADD  [IPAddress] varchar(128) NOT NULL CONSTRAINT DF_Address DEFAULT 'N/A';
````

<span data-ttu-id="34c2c-167">Benzer şekilde, iş yükünüzü etkinken sütun tanımı değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="34c2c-167">Similarly, you can change column definition while your workload is active:</span></span>

````
/*Increase the length of name column*/
ALTER TABLE dbo.WebsiteUserInfo 
    ALTER COLUMN  UserName nvarchar(256) NOT NULL;
````

<span data-ttu-id="34c2c-168">Son olarak, artık ihtiyacınız olmayan bir sütun kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34c2c-168">Finally, you can remove a column that you do not need anymore.</span></span>

````
/*Drop unnecessary column */
ALTER TABLE dbo.WebsiteUserInfo 
    DROP COLUMN TemporaryColumn; 
````

<span data-ttu-id="34c2c-169">Alternatif olarak, en son kullanın [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) (çevrimiçi mod) veritabanı veya veritabanı projesi (Çevrimdışı mod) bir parçası olarak bağlıyken zamana bağlı tablo şemasını değiştirmek için.</span><span class="sxs-lookup"><span data-stu-id="34c2c-169">Alternatively, use latest [SSDT](https://msdn.microsoft.com/library/mt204009.aspx) to change temporal table schema while you are connected to the database (online mode) or as part of the database project (offline mode).</span></span>

## <a name="controlling-retention-of-historical-data"></a><span data-ttu-id="34c2c-170">Geçmiş verilerin bekletilmesini denetleme</span><span class="sxs-lookup"><span data-stu-id="34c2c-170">Controlling retention of historical data</span></span>
<span data-ttu-id="34c2c-171">Sistem sürümü tutulan zamana bağlı tablolarda ile geçmiş tablosu normal tablolardaki birden çok veritabanı boyutunu artırabilir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-171">With system-versioned temporal tables, the history table may increase the database size more than regular tables.</span></span> <span data-ttu-id="34c2c-172">Büyük ve sürekli büyüyen geçmiş tablosu, hem saf depolama maliyetleri yanı sıra bir performans etkileyici nedeniyle zamana bağlı sorgulama vergi bir sorun olabilir.</span><span class="sxs-lookup"><span data-stu-id="34c2c-172">A large and ever-growing history table can become an issue both due to pure storage costs as well as imposing a performance tax on temporal querying.</span></span> <span data-ttu-id="34c2c-173">Bu nedenle, geçmiş tablosundaki verileri yönetmek için bir veri bekletme ilkesi geliştirme planlama ve her zamana bağlı tablo yaşam döngüsü yönetiminden önemli bir özelliği olan.</span><span class="sxs-lookup"><span data-stu-id="34c2c-173">Hence, developing a data retention policy for managing data in the history table is an important aspect of planning and managing the lifecycle of every temporal table.</span></span> <span data-ttu-id="34c2c-174">Azure SQL veritabanı ile zamana bağlı tabloda geçmiş verileri yönetmek için aşağıdaki yaklaşımlardan vardır:</span><span class="sxs-lookup"><span data-stu-id="34c2c-174">With Azure SQL Database, you have the following approaches for managing historical data in the temporal table:</span></span>

* [<span data-ttu-id="34c2c-175">Tablo bölümleme</span><span class="sxs-lookup"><span data-stu-id="34c2c-175">Table Partitioning</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_2)
* [<span data-ttu-id="34c2c-176">Özel temizleme betiğini</span><span class="sxs-lookup"><span data-stu-id="34c2c-176">Custom Cleanup Script</span></span>](https://msdn.microsoft.com/library/mt637341.aspx#Anchor_3)

## <a name="next-steps"></a><span data-ttu-id="34c2c-177">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34c2c-177">Next steps</span></span>
<span data-ttu-id="34c2c-178">Zamana bağlı tablolarda hakkında ayrıntılı bilgi için kullanıma [MSDN belgelerine](https://msdn.microsoft.com/library/dn935015.aspx).</span><span class="sxs-lookup"><span data-stu-id="34c2c-178">For detailed information on Temporal Tables, check out [MSDN documentation](https://msdn.microsoft.com/library/dn935015.aspx).</span></span>
<span data-ttu-id="34c2c-179">Dinlemek için kanal 9 ziyaret bir [gerçek müşteri zamana bağlı implemenation başarı Öykü](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) ve izleme bir [zamana bağlı tanıtım canlı](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span><span class="sxs-lookup"><span data-stu-id="34c2c-179">Visit Channel 9 to hear a [real customer temporal implemenation success story](https://channel9.msdn.com/Blogs/jsturtevant/Azure-SQL-Temporal-Tables-with-RockStep-Solutions) and watch a [live temporal demonstration](https://channel9.msdn.com/Shows/Data-Exposed/Temporal-in-SQL-Server-2016).</span></span>

