---
title: "Veritabanları arası sorgular (dikey bölümleme) ile çalışmaya başlama | Microsoft Docs"
description: "Esnek veritabanı sorgusu dikey olarak bölümlenmiş veritabanları ile nasıl kullanılır"
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
ms.openlocfilehash: 17158c4960e9ba9251524659c90af9aec1316774
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a><span data-ttu-id="85bce-103">Veritabanları arası sorgular (dikey bölümleme) ile çalışmaya başlama (Önizleme)</span><span class="sxs-lookup"><span data-stu-id="85bce-103">Get started with cross-database queries (vertical partitioning) (preview)</span></span>
<span data-ttu-id="85bce-104">Esnek veritabanı sorgu (Önizleme) Azure SQL veritabanı için bir tek bağlantı noktası kullanarak birden çok veritabanı span T-SQL sorguları çalıştırmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="85bce-104">Elastic database query (preview) for Azure SQL Database allows you to run T-SQL queries that span multiple databases using a single connection point.</span></span> <span data-ttu-id="85bce-105">Bu konuda uygulandığı [veritabanları'dikey olarak bölümlenmiş](sql-database-elastic-query-vertical-partitioning.md).</span><span class="sxs-lookup"><span data-stu-id="85bce-105">This topic applies to [vertically partitioned databases](sql-database-elastic-query-vertical-partitioning.md).</span></span>  

<span data-ttu-id="85bce-106">Tamamlandığında, şunları yapacaksınız: yapılandırmak ve birden çok ilişkili veritabanlarını span sorguları gerçekleştirmek için bir Azure SQL veritabanını kullan öğrenin.</span><span class="sxs-lookup"><span data-stu-id="85bce-106">When completed, you will: learn how to configure and use an Azure SQL Database to perform queries that span multiple related databases.</span></span> 

<span data-ttu-id="85bce-107">Esnek veritabanı sorgu özelliği hakkında daha fazla bilgi için lütfen bkz [Azure SQL Database esnek veritabanı sorgu genel bakış](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85bce-107">For more information about the elastic database query feature, please see  [Azure SQL Database elastic database query overview](sql-database-elastic-query-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="85bce-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="85bce-108">Prerequisites</span></span>

<span data-ttu-id="85bce-109">ALTER ANY dış veri KAYNAĞINA iznine sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="85bce-109">You must possess ALTER ANY EXTERNAL DATA SOURCE permission.</span></span> <span data-ttu-id="85bce-110">Bu izin ALTER DATABASE izniyle dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="85bce-110">This permission is included with the ALTER DATABASE permission.</span></span> <span data-ttu-id="85bce-111">Temel alınan veri kaynağına başvurmak için ALTER ANY dış veri kaynağı izinleri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="85bce-111">ALTER ANY EXTERNAL DATA SOURCE permissions are needed to refer to the underlying data source.</span></span>

## <a name="create-the-sample-databases"></a><span data-ttu-id="85bce-112">Örnek veritabanları oluşturma</span><span class="sxs-lookup"><span data-stu-id="85bce-112">Create the sample databases</span></span>
<span data-ttu-id="85bce-113">İle başlamak iki veritabanı oluşturmak ihtiyacımız **müşteriler** ve **siparişleri**, aynı veya farklı bir mantıksal sunucuya ya da.</span><span class="sxs-lookup"><span data-stu-id="85bce-113">To start with, we need to create two databases, **Customers** and **Orders**, either in the same or different logical servers.</span></span>   

<span data-ttu-id="85bce-114">Üzerinde aşağıdaki sorguları yürütün **siparişleri** oluşturmak için veritabanında **OrderInformation** tablo ve örnek verileri girdi.</span><span class="sxs-lookup"><span data-stu-id="85bce-114">Execute the following queries on the **Orders** database to create the **OrderInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

<span data-ttu-id="85bce-115">Sorgu şimdi yürütmek **müşteriler** oluşturmak için veritabanında **CustomerInformation** tablo ve örnek verileri girdi.</span><span class="sxs-lookup"><span data-stu-id="85bce-115">Now, execute following query on the **Customers** database to create the **CustomerInformation** table and input the sample data.</span></span> 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a><span data-ttu-id="85bce-116">Veritabanı nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="85bce-116">Create database objects</span></span>
### <a name="database-scoped-master-key-and-credentials"></a><span data-ttu-id="85bce-117">Veritabanı kapsamlı ana anahtar ve kimlik bilgileri</span><span class="sxs-lookup"><span data-stu-id="85bce-117">Database scoped master key and credentials</span></span>
1. <span data-ttu-id="85bce-118">SQL Server Management Studio veya SQL Server veri araçları Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="85bce-118">Open SQL Server Management Studio or SQL Server Data Tools in Visual Studio.</span></span>
2. <span data-ttu-id="85bce-119">Siparişleri veritabanına bağlanmak ve aşağıdaki T-SQL komutları yürütün:</span><span class="sxs-lookup"><span data-stu-id="85bce-119">Connect to the Orders database and execute the following T-SQL commands:</span></span>
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    <span data-ttu-id="85bce-120">"Parola" ve "username" kullanıcı adı ve parola kullanılan olmalıdır müşteriler veritabanına oturum açmak için.</span><span class="sxs-lookup"><span data-stu-id="85bce-120">The "username" and "password" should be the username and password used to login into the Customers database.</span></span>
    <span data-ttu-id="85bce-121">Esnek sorgularıyla Azure Active Directory'yi kullanarak kimlik doğrulaması şu anda desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="85bce-121">Authentication using Azure Active Directory with elastic queries is not currently supported.</span></span>

### <a name="external-data-sources"></a><span data-ttu-id="85bce-122">Dış veri kaynakları</span><span class="sxs-lookup"><span data-stu-id="85bce-122">External data sources</span></span>
<span data-ttu-id="85bce-123">Dış veri kaynağı oluşturmak için siparişler veritabanı üzerinde şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="85bce-123">To create an external data source, execute the following command on the Orders database:</span></span> 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a><span data-ttu-id="85bce-124">Dış tablolar</span><span class="sxs-lookup"><span data-stu-id="85bce-124">External tables</span></span>
<span data-ttu-id="85bce-125">Bir dış tablo CustomerInformation tablosunun tanımını eşleşen siparişleri veritabanı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="85bce-125">Create an external table on the Orders database, which matches the definition of the CustomerInformation table:</span></span>

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a><span data-ttu-id="85bce-126">Bir örnek esnek veritabanı T-SQL sorgusu yürütme</span><span class="sxs-lookup"><span data-stu-id="85bce-126">Execute a sample elastic database T-SQL query</span></span>
<span data-ttu-id="85bce-127">Dış veri kaynağınızda ve dış tablolarınızı tanımladıktan sonra dış tablolara sorgulamak için T-SQL artık kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85bce-127">Once you have defined your external data source and your external tables you can now use T-SQL to query your external tables.</span></span> <span data-ttu-id="85bce-128">Bu sorgu siparişler veritabanında yürütün:</span><span class="sxs-lookup"><span data-stu-id="85bce-128">Execute this query on the Orders database:</span></span> 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a><span data-ttu-id="85bce-129">Maliyet</span><span class="sxs-lookup"><span data-stu-id="85bce-129">Cost</span></span>
<span data-ttu-id="85bce-130">Şu anda, esnek veritabanı sorgu Özelliği Azure SQL veritabanınıza maliyet dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="85bce-130">Currently, the elastic database query feature is included into the cost of your Azure SQL Database.</span></span>  

<span data-ttu-id="85bce-131">Fiyatlandırma bilgileri için bkz: [SQL Database fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-database).</span><span class="sxs-lookup"><span data-stu-id="85bce-131">For pricing information see [SQL Database Pricing](https://azure.microsoft.com/pricing/details/sql-database).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="85bce-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="85bce-132">Next steps</span></span>

* <span data-ttu-id="85bce-133">Esnek sorgu genel bakış için bkz: [esnek sorgu genel bakış](sql-database-elastic-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85bce-133">For an overview of elastic query, see [Elastic query overview](sql-database-elastic-query-overview.md).</span></span>
* <span data-ttu-id="85bce-134">Dikey olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [dikey sorgulama bölümlenmiş veri)](sql-database-elastic-query-vertical-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="85bce-134">For syntax and sample queries for vertically partitioned data, see [Querying vertically partitioned data)](sql-database-elastic-query-vertical-partitioning.md)</span></span>
* <span data-ttu-id="85bce-135">Yatay bölümleme (parçalama) bir öğretici için bkz: [yatay (parçalama) bölümleme için esnek sorgu ile çalışmaya başlama](sql-database-elastic-query-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="85bce-135">For a horizontal partitioning (sharding) tutorial, see [Getting started with elastic query for horizontal partitioning (sharding)](sql-database-elastic-query-getting-started.md).</span></span>
* <span data-ttu-id="85bce-136">Yatay olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [yatay sorgulama bölümlenmiş veri)](sql-database-elastic-query-horizontal-partitioning.md)</span><span class="sxs-lookup"><span data-stu-id="85bce-136">For syntax and sample queries for horizontally partitioned data, see [Querying horizontally partitioned data)](sql-database-elastic-query-horizontal-partitioning.md)</span></span>
* <span data-ttu-id="85bce-137">Bkz: [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) tek uzaktan Azure SQL veritabanı ya da yatay bölümleme düzenindeki parça olarak hizmet veren bir veritabanları kümesi üzerinde bir Transact-SQL deyimini yürütür bir saklı yordam için.</span><span class="sxs-lookup"><span data-stu-id="85bce-137">See [sp\_execute \_remote](https://msdn.microsoft.com/library/mt703714) for a stored procedure that executes a Transact-SQL statement on a single remote Azure SQL Database or set of databases serving as shards in a horizontal partitioning scheme.</span></span>