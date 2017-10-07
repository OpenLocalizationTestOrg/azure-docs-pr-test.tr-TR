---
title: "SQL veri ambarı aaaUser tanımlı şemalarda | Microsoft Docs"
description: "Çözümleri geliştirme için Azure SQL Data Warehouse'da Transact-SQL şemalarını kullanma ipuçları."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 52af5bd5-d5d3-4f9b-8704-06829fb924e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: c411d6fed68e67c444a5871eab06182eaeb6dbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="user-defined-schemas-in-sql-data-warehouse"></a><span data-ttu-id="7695a-103">Kullanıcı tanımlı şemaları SQL veri ambarı</span><span class="sxs-lookup"><span data-stu-id="7695a-103">User-defined schemas in SQL Data Warehouse</span></span>
<span data-ttu-id="7695a-104">Geleneksel veri ambarları genellikle kullanım ayrı veritabanlarını toocreate uygulama sınırlarını iş yükü, etki alanı veya güvenlik dayanarak.</span><span class="sxs-lookup"><span data-stu-id="7695a-104">Traditional data warehouses often use separate databases toocreate application boundaries based on either workload, domain or security.</span></span> <span data-ttu-id="7695a-105">Örneğin, geleneksel SQL Server veri ambarı Hazırlama veritabanı, veri ambarı veritabanı ve bazı veri reyonu veritabanı içerebilir.</span><span class="sxs-lookup"><span data-stu-id="7695a-105">For example, a traditional SQL Server data warehouse might include a staging database, a data warehouse database, and some data mart databases.</span></span> <span data-ttu-id="7695a-106">Bu topolojide, her veritabanı iş yükü ve güvenlik sınırı hello mimarisinde olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="7695a-106">In this topology each database operates as a workload and security boundary in hello architecture.</span></span>

<span data-ttu-id="7695a-107">Bunun aksine, SQL Data Warehouse hello tüm veri ambarı iş yükü bir veritabanı içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="7695a-107">By contrast, SQL Data Warehouse runs hello entire data warehouse workload within one database.</span></span> <span data-ttu-id="7695a-108">Veritabanı birleştirmeler izin verilmez.</span><span class="sxs-lookup"><span data-stu-id="7695a-108">Cross database joins are not permitted.</span></span> <span data-ttu-id="7695a-109">Bu nedenle SQL Data Warehouse hello bir veritabanı içinde depolanan hello ambar toobe tarafından kullanılan bütün tablolar bekliyor.</span><span class="sxs-lookup"><span data-stu-id="7695a-109">Therefore SQL Data Warehouse expects all tables used by hello warehouse toobe stored within hello one database.</span></span>

> [!NOTE]
> <span data-ttu-id="7695a-110">SQL veri ambarı veritabanları arası sorguları herhangi bir türde desteklemez.</span><span class="sxs-lookup"><span data-stu-id="7695a-110">SQL Data Warehouse does not support cross database queries of any kind.</span></span> <span data-ttu-id="7695a-111">Sonuç olarak, bu deseni yararlanan veri ambarı uygulamaları düzenlendi toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7695a-111">Consequently, data warehouse implementations that leverage this pattern will need toobe revised.</span></span>
> 
> 

## <a name="recommendations"></a><span data-ttu-id="7695a-112">Öneriler</span><span class="sxs-lookup"><span data-stu-id="7695a-112">Recommendations</span></span>
<span data-ttu-id="7695a-113">Kullanıcı tanımlı şemalarını kullanarak iş yükleri, güvenlik, etki alanı ve işlevsel sınırları birleştirilmesi için öneriler bunlar</span><span class="sxs-lookup"><span data-stu-id="7695a-113">These are recommendations for consolidating workloads, security, domain and functional boundaries by using user defined schemas</span></span>

1. <span data-ttu-id="7695a-114">Bir SQL Data Warehouse veritabanı toorun, tüm veri ambarı iş yükü kullanın</span><span class="sxs-lookup"><span data-stu-id="7695a-114">Use one SQL Data Warehouse database toorun your entire data warehouse workload</span></span>
2. <span data-ttu-id="7695a-115">Var olan veri ambarı ortamında toouse bir SQL Data Warehouse veritabanınız birleştirin</span><span class="sxs-lookup"><span data-stu-id="7695a-115">Consolidate your existing data warehouse environment toouse one SQL Data Warehouse database</span></span>
3. <span data-ttu-id="7695a-116">Dengeleme **kullanıcı tanımlı şemaları** veritabanları kullanılarak daha önce uygulanan tooprovide hello sınır.</span><span class="sxs-lookup"><span data-stu-id="7695a-116">Leverage **user-defined schemas** tooprovide hello boundary previously implemented using databases.</span></span>

<span data-ttu-id="7695a-117">Kullanıcı tanımlı şemaları kullanılmadı önceden sonra temiz bir Kurşun varsa.</span><span class="sxs-lookup"><span data-stu-id="7695a-117">If user-defined schemas have not been used previously then you have a clean slate.</span></span> <span data-ttu-id="7695a-118">Yalnızca hello eski veritabanı adı, kullanıcı tanımlı şemaları hello SQL veri ambarı veritabanındaki için hello temel olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="7695a-118">Simply use hello old database name as hello basis for your user-defined schemas in hello SQL Data Warehouse database.</span></span>

<span data-ttu-id="7695a-119">Ardından şemaları zaten kullandıysanız, birkaç seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="7695a-119">If schemas have already been used then you have a few options:</span></span>

1. <span data-ttu-id="7695a-120">Merhaba eski şema adlarını kaldırın ve yeniden Başlat</span><span class="sxs-lookup"><span data-stu-id="7695a-120">Remove hello legacy schema names and start fresh</span></span>
2. <span data-ttu-id="7695a-121">Merhaba eski şema adları önceden bekleyen hello eski şema toohello tablo adı ile koruyun</span><span class="sxs-lookup"><span data-stu-id="7695a-121">Retain hello legacy schema names by pre-pending hello legacy schema name toohello table name</span></span>
3. <span data-ttu-id="7695a-122">Bir ek şema toore hello tabloda üzerinden görünümleri uygulayarak Hello eski şema adlarını korumak-hello eski şema yapısı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7695a-122">Retain hello legacy schema names by implementing views over hello table in an extra schema toore-create hello old schema structure.</span></span>

> [!NOTE]
> <span data-ttu-id="7695a-123">İlk denetimi seçenek 3 hello en cazip seçeneği gibi görünebilir.</span><span class="sxs-lookup"><span data-stu-id="7695a-123">On first inspection option 3 may seem like hello most appealing option.</span></span> <span data-ttu-id="7695a-124">Ancak, hello Şeytan hello ayrıntılı olarak vardır.</span><span class="sxs-lookup"><span data-stu-id="7695a-124">However, hello devil is in hello detail.</span></span> <span data-ttu-id="7695a-125">Görünümler, yalnızca SQL veri ambarında salt okunurdur.</span><span class="sxs-lookup"><span data-stu-id="7695a-125">Views are read only in SQL Data Warehouse.</span></span> <span data-ttu-id="7695a-126">Tüm veri veya tabloda değişiklik hello temel tablo karşı gerçekleştirilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="7695a-126">Any data or table modification would need toobe performed against hello base table.</span></span> <span data-ttu-id="7695a-127">Seçenek 3, aynı zamanda bir katman görünümlerinin sisteminize sunar.</span><span class="sxs-lookup"><span data-stu-id="7695a-127">Option 3 also introduces a layer of views into your system.</span></span> <span data-ttu-id="7695a-128">Görünümler, mimarisinde zaten kullanıyorsanız, bu bazı ek bir düşünce toogive isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7695a-128">You might want toogive this some additional thought if you are using views in your architecture already.</span></span>
> 
> 

### <a name="examples"></a><span data-ttu-id="7695a-129">Örnekler:</span><span class="sxs-lookup"><span data-stu-id="7695a-129">Examples:</span></span>
<span data-ttu-id="7695a-130">Kullanıcı tanımlı şemaları veritabanı adlarına göre uygulama</span><span class="sxs-lookup"><span data-stu-id="7695a-130">Implement user-defined schemas based on database names</span></span>

```sql
CREATE SCHEMA [stg]; -- stg previously database name for staging database
GO
CREATE SCHEMA [edw]; -- edw previously database name for hello data warehouse
GO
CREATE TABLE [stg].[customer] -- create staging tables in hello stg schema
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[customer] -- create data warehouse tables in hello edw schema
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="7695a-131">Korumak eski şema adları tarafından önceden bekleyen bunları toohello tablo adı.</span><span class="sxs-lookup"><span data-stu-id="7695a-131">Retain legacy schema names by pre-pending them toohello table name.</span></span> <span data-ttu-id="7695a-132">Şemalar hello iş yükü sınırı için kullanın.</span><span class="sxs-lookup"><span data-stu-id="7695a-132">Use schemas for hello workload boundary.</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- edw defines hello data warehouse boundary
GO
CREATE TABLE [stg].[dim_customer] --pre-pend hello old schema name toohello table and create in hello staging boundary
(       CustKey BIGINT NOT NULL
,       ...
);
GO
CREATE TABLE [edw].[dim_customer] --pre-pend hello old schema name toohello table and create in hello data warehouse boundary
(       CustKey BIGINT NOT NULL
,       ...
);
```

<span data-ttu-id="7695a-133">Görünümleri kullanarak eski şema adlarını korur</span><span class="sxs-lookup"><span data-stu-id="7695a-133">Retain legacy schema names using views</span></span>

```sql
CREATE SCHEMA [stg]; -- stg defines hello staging boundary
GO
CREATE SCHEMA [edw]; -- stg defines hello data warehouse boundary
GO
CREATE SCHEMA [dim]; -- edw defines hello legacy schema name boundary
GO
CREATE TABLE [stg].[customer] -- create hello base staging tables in hello staging boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE TABLE [edw].[customer] -- create hello base data warehouse tables in hello data warehouse boundary
(       CustKey    BIGINT NOT NULL
,       ...
)
GO
CREATE VIEW [dim].[customer] -- create a view in hello legacy schema name boundary for presentation consistency purposes only
AS
SELECT  CustKey
,       ...
FROM    [edw].customer
;
```

> [!NOTE]
> <span data-ttu-id="7695a-134">Şema stratejisi herhangi bir değişikliği hello güvenlik modeli gözden hello veritabanı için gerekir.</span><span class="sxs-lookup"><span data-stu-id="7695a-134">Any change in schema strategy needs a review of hello security model for hello database.</span></span> <span data-ttu-id="7695a-135">Çoğu durumda hello şema düzeyinde izinler atayarak mümkün toosimplify hello güvenlik modeli olabilir.</span><span class="sxs-lookup"><span data-stu-id="7695a-135">In many cases you might be able toosimplify hello security model by assigning permissions at hello schema level.</span></span> <span data-ttu-id="7695a-136">Daha ayrıntılı izinler gerekli olduğunda, veritabanı rolleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7695a-136">If more granular permissions are required then you can use database roles.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="7695a-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7695a-137">Next steps</span></span>
<span data-ttu-id="7695a-138">Daha fazla geliştirme ipuçları için bkz: [geliştirmeye genel bakış][development overview].</span><span class="sxs-lookup"><span data-stu-id="7695a-138">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
