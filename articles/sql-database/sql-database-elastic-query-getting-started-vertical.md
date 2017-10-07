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
# <a name="get-started-with-cross-database-queries-vertical-partitioning-preview"></a>Veritabanları arası sorgular (dikey bölümleme) ile çalışmaya başlama (Önizleme)
Esnek veritabanı sorgu (Önizleme) Azure SQL veritabanı için bir tek bağlantı noktası kullanarak birden çok veritabanı span toorun T-SQL sorgularını sağlar. Bu konu, çok geçerlidir[veritabanları'dikey olarak bölümlenmiş](sql-database-elastic-query-vertical-partitioning.md).  

Tamamlandığında, şunları yapacaksınız: nasıl tooconfigure ve kullanım bir Azure SQL veritabanı tooperform sorgular bu aralık birden çok ilişkili veritabanlarını öğrenin. 

Merhaba esnek veritabanı sorgu özelliği hakkında daha fazla bilgi için lütfen bkz [Azure SQL Database esnek veritabanı sorgu genel bakış](sql-database-elastic-query-overview.md). 

## <a name="prerequisites"></a>Ön koşullar

ALTER ANY dış veri KAYNAĞINA iznine sahip olması gerekir. Bu izni hello ALTER DATABASE iznine dahil edilir. ALTER ANY dış veri kaynağı, veri kaynağı arka plandaki gerekli toorefer toohello izinlerdir.

## <a name="create-hello-sample-databases"></a>Örnek veritabanları Hello oluşturma
toostart ile ihtiyacımız toocreate iki veritabanı, **müşteriler** ve **siparişleri**, aynı veya farklı bir mantıksal sunucu ya da hello.   

Sorguları hello üzerinde aşağıdaki hello yürütme **siparişleri** veritabanı toocreate hello **OrderInformation** tablo ve giriş hello örnek verileri. 

    CREATE TABLE [dbo].[OrderInformation]( 
        [OrderID] [int] NOT NULL, 
        [CustomerID] [int] NOT NULL 
        ) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (123, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (149, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (857, 2) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (321, 1) 
    INSERT INTO [dbo].[OrderInformation] ([OrderID], [CustomerID]) VALUES (564, 8) 

Merhaba bir sorguyu aşağıdaki şimdi, yürütme **müşteriler** veritabanı toocreate hello **CustomerInformation** tablo ve giriş hello örnek verileri. 

    CREATE TABLE [dbo].[CustomerInformation]( 
        [CustomerID] [int] NOT NULL, 
        [CustomerName] [varchar](50) NULL, 
        [Company] [varchar](50) NULL 
        CONSTRAINT [CustID] PRIMARY KEY CLUSTERED ([CustomerID] ASC) 
    ) 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (1, 'Jack', 'ABC') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (2, 'Steve', 'XYZ') 
    INSERT INTO [dbo].[CustomerInformation] ([CustomerID], [CustomerName], [Company]) VALUES (3, 'Lylla', 'MNO') 

## <a name="create-database-objects"></a>Veritabanı nesneleri oluşturma
### <a name="database-scoped-master-key-and-credentials"></a>Veritabanı kapsamlı ana anahtar ve kimlik bilgileri
1. SQL Server Management Studio veya SQL Server veri araçları Visual Studio'da açın.
2. Toohello siparişleri veritabanına bağlanmak ve aşağıdaki T-SQL komutlarıyla hello yürütün:
   
        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>'; 
        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred 
        WITH IDENTITY = '<username>', 
        SECRET = '<password>';  
   
    hello müşteriler veritabanına toologin kullanılan parolayı ve Hello "username" ve "parola" hello kullanıcı adı olması gerekir.
    Esnek sorgularıyla Azure Active Directory'yi kullanarak kimlik doğrulaması şu anda desteklenmiyor.

### <a name="external-data-sources"></a>Dış veri kaynakları
bir dış veri kaynağına toocreate komutu hello siparişleri veritabanında aşağıdaki hello yürütün: 

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH 
        (TYPE = RDBMS, 
        LOCATION = '<server_name>.database.windows.net', 
        DATABASE_NAME = 'Customers', 
        CREDENTIAL = ElasticDBQueryCred, 
    ) ;

### <a name="external-tables"></a>Dış tablolar
Bir dış tablo hello CustomerInformation tablosunun hello tanımı eşleşen hello siparişleri veritabanı üzerinde oluşturun:

    CREATE EXTERNAL TABLE [dbo].[CustomerInformation] 
    ( [CustomerID] [int] NOT NULL, 
      [CustomerName] [varchar](50) NOT NULL, 
      [Company] [varchar](50) NOT NULL) 
    WITH 
    ( DATA_SOURCE = MyElasticDBQueryDataSrc) 

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Bir örnek esnek veritabanı T-SQL sorgusu yürütme
Dış veri kaynağınızda ve dış tablolarınızı tanımladıktan sonra dış tablolara T-SQL tooquery artık kullanabilirsiniz. Bu sorgu hello siparişleri veritabanında yürütün: 

    SELECT OrderInformation.CustomerID, OrderInformation.OrderId, CustomerInformation.CustomerName, CustomerInformation.Company 
    FROM OrderInformation 
    INNER JOIN CustomerInformation 
    ON CustomerInformation.CustomerID = OrderInformation.CustomerID 

## <a name="cost"></a>Maliyet
Şu anda hello esnek veritabanı sorgu Özelliği Azure SQL veritabanınıza hello maliyetini dahil edilir.  

Fiyatlandırma bilgileri için bkz: [SQL Database fiyatlandırması](https://azure.microsoft.com/pricing/details/sql-database). 

## <a name="next-steps"></a>Sonraki adımlar

* Esnek sorgu genel bakış için bkz: [esnek sorgu genel bakış](sql-database-elastic-query-overview.md).
* Dikey olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [dikey sorgulama bölümlenmiş veri)](sql-database-elastic-query-vertical-partitioning.md)
* Yatay bölümleme (parçalama) bir öğretici için bkz: [yatay (parçalama) bölümleme için esnek sorgu ile çalışmaya başlama](sql-database-elastic-query-getting-started.md).
* Yatay olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [yatay sorgulama bölümlenmiş veri)](sql-database-elastic-query-horizontal-partitioning.md)
* Bkz: [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) tek uzaktan Azure SQL veritabanı ya da yatay bölümleme düzenindeki parça olarak hizmet veren bir veritabanları kümesi üzerinde bir Transact-SQL deyimini yürütür bir saklı yordam için.