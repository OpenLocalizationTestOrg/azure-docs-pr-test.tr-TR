---
title: "aaaGet başlatıldı (dikey bölümleme) veritabanları arası sorgularıyla | Microsoft Docs"
description: "nasıl toouse esnek veritabanı sorgusu ile veritabanları dikey olarak bölümlenmiş"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: e5b44b10-c432-4f96-b20e-08615ff4d5dd
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: torsteng
ms.openlocfilehash: 9e6183268e8bf87e3ac28f502711fcc05a7a3f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="9d72d-103">Veritabanları arası sorgular (dikey bölümleme) ile çalışmaya başlama (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="9d72d-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="9d72d-104">Esnek veritabanı sorgu (Önizleme) Azure SQL veritabanı için bir tek bağlantı noktası kullanarak birden çok veritabanı span toorun T-SQL sorgularını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d72d-104">Elastic database query (preview) for Azure SQL Database allows you toorun T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="9d72d-105">Bu konu, çok geçerlidir[veritabanları'dikey olarak bölümlenmiş](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="9d72d-105">This topic applies too[vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="9d72d-106">Tamamlandığında, şunları yapacaksınız: nasıl tooconfigure ve kullanım bir Azure SQL veritabanı tooperform sorgular bu aralık birden çok ilişkili veritabanlarını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9d72d-106">When completed, you will: learn how tooconfigure and use an Azure SQL Database tooperform queries that span multiple related databases.</span></span> 

<span data-ttu-id="9d72d-107">Merhaba esnek veritabanı sorgu özelliği hakkında daha fazla bilgi için lütfen bkz [Azure SQL Database esnek veritabanı sorgu genel bakış](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9d72d-107">For more information about hello elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9d72d-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9d72d-108">Prerequisites</span></span>

<span data-ttu-id="9d72d-109">ALTER ANY dış veri KAYNAĞINA iznine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d72d-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="9d72d-110">Bu izni hello ALTER DATABASE iznine dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="9d72d-110">This permission is included with hello ALTER DATABASE permission.</span></span> <span data-ttu-id="9d72d-111">ALTER ANY dış veri kaynağı, veri kaynağı arka plandaki gerekli toorefer toohello izinlerdir.</span><span class="sxs-lookup"><span data-stu-id="9d72d-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed toorefer toohello underlying data source.</span></span>

## <a name="create-hello-sample-databases"></a><span data-ttu-id="9d72d-112">Örnek veritabanları Hello oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d72d-112">Create hello sample databases</span></span>
<span data-ttu-id="9d72d-113">toostart ile ihtiyacımız toocreate iki veritabanı, **müşteriler** ve **siparişleri**, aynı veya farklı bir mantıksal sunucu ya da hello.</span><span class="sxs-lookup"><span data-stu-id="9d72d-113">toostart with, we need toocreate two databases, **Customers** and **Orders**, either in hello same or different logical servers.</span></span>   

<span data-ttu-id="9d72d-114">Sorguları hello üzerinde aşağıdaki hello yürütme **siparişleri** veritabanı toocreate hello **OrderInformation** tablo ve giriş hello örnek verileri.</span><span class="sxs-lookup"><span data-stu-id="9d72d-114">Execute hello following queries on hello **Orders** database toocreate hello **OrderInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="9d72d-115">Merhaba bir sorguyu aşağıdaki şimdi, yürütme **müşteriler** veritabanı toocreate hello **CustomerInformation** tablo ve giriş hello örnek verileri.</span><span class="sxs-lookup"><span data-stu-id="9d72d-115">Now, execute following query on hello **Customers** database toocreate hello **CustomerInformation** table and input hello sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="9d72d-116">Veritabanı nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="9d72d-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="9d72d-117">Veritabanı kapsamlı ana anahtar ve kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="9d72d-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="9d72d-118">SQL Server Management Studio veya SQL Server veri araçları Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="9d72d-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="9d72d-119">Toohello siparişleri veritabanına bağlanmak ve aşağıdaki T-SQL komutlarıyla hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="9d72d-119">Connect toohello Orders database and execute hello following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="9d72d-120">hello müşteriler veritabanına toologin kullanılan parolayı ve Hello "username" ve "parola" hello kullanıcı adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9d72d-120">hello "username" and "password" should be hello username and password used toologin into hello Customers database.</span></span>
    <span data-ttu-id="9d72d-121">Esnek sorgularıyla Azure Active Directory'yi kullanarak kimlik doğrulaması şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="9d72d-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="9d72d-122">Dış veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="9d72d-122">External data sources</span></span>
<span data-ttu-id="9d72d-123">bir dış veri kaynağına toocreate komutu hello siparişleri veritabanında aşağıdaki hello yürütün:</span><span class="sxs-lookup"><span data-stu-id="9d72d-123">toocreate an external data source, execute hello following command on hello Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="9d72d-124">Dış tablolar</span><span class="sxs-lookup"><span data-stu-id="9d72d-124">External tables</span></span>
<span data-ttu-id="9d72d-125">Bir dış tablo hello CustomerInformation tablosunun hello tanımı eşleşen hello siparişleri veritabanı üzerinde oluşturun:</span><span class="sxs-lookup"><span data-stu-id="9d72d-125">Create an external table on hello Orders database, which matches hello definition of hello CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="9d72d-126">Bir örnek esnek veritabanı T-SQL sorgusu yürütme</span><span class="sxs-lookup"><span data-stu-id="9d72d-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="9d72d-127">Dış veri kaynağınızda ve dış tablolarınızı tanımladıktan sonra dış tablolara T-SQL tooquery artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d72d-127">Once you have defined your external data source and your external tables you can now use T-SQL tooquery your external tables.</span></span> <span data-ttu-id="9d72d-128">Bu sorgu hello siparişleri veritabanında yürütün:</span><span class="sxs-lookup"><span data-stu-id="9d72d-128">Execute this query on hello Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="9d72d-129">Maliyet</span><span class="sxs-lookup"><span data-stu-id="9d72d-129">Cost</span></span>
<span data-ttu-id="9d72d-130">Şu anda hello esnek veritabanı sorgu Özelliği Azure SQL veritabanınıza hello maliyetini dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="9d72d-130">Currently, hello elastic database query feature is included into hello cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="9d72d-131">Fiyatlandırma bilgileri için bkz: [SQL Database fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="9d72d-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9d72d-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9d72d-132">Next steps</span></span>

* <span data-ttu-id="9d72d-133">Esnek sorgu genel bakış için bkz: [esnek sorgu genel bakış](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9d72d-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="9d72d-134">Dikey olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [dikey sorgulama bölümlenmiş veri)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="9d72d-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="9d72d-135">Yatay bölümleme (parçalama) bir öğretici için bkz: [yatay (parçalama) bölümleme için esnek sorgu ile çalışmaya başlama](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="9d72d-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="9d72d-136">Yatay olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [yatay sorgulama bölümlenmiş veri)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="9d72d-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="9d72d-137">Bkz: [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) tek uzaktan Azure SQL veritabanı ya da yatay bölümleme düzenindeki parça olarak hizmet veren bir veritabanları kümesi üzerinde bir Transact-SQL deyimini yürütür bir saklı yordam için.</span><span class="sxs-lookup"><span data-stu-id="9d72d-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>