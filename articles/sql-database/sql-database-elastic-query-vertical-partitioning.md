---
title: "Bulut üzerinden aaaQuery veritabanları farklı şemasıyla | Microsoft Docs"
description: "nasıl tooset dikey bölümleri veritabanları arası sorguları ayarlama"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 84c261f2-9edc-42f4-988c-cf2f251f5eff
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: 1134e2e608128b7a9cac47ff35a22a11e6e5bc14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="query-across-cloud-databases-with-different-schemas-preview"></a>Bulut veritabanları farklı şemaları (Önizleme) ile sorgulama
![Farklı veritabanı tablolarında sorgulama][1]

Veritabanlarını dikey olarak bölümlenmiş tabloları kümesi farklı farklı veritabanlarını kullanır. Bu hello şema farklı veritabanlarında farklı olduğu anlamına gelir. Örneğin, tüm hesap ilişkili tabloları ikinci bir veritabanı üzerinde çalışırken tüm tablolar için stok bir veritabanında ' dir. 

## <a name="prerequisites"></a>Ön koşullar
* Merhaba kullanıcı ALTER ANY dış veri KAYNAĞINA iznine sahip olması gerekir. Bu izni hello ALTER DATABASE iznine dahil edilir.
* ALTER ANY dış veri kaynağı, veri kaynağı arka plandaki gerekli toorefer toohello izinlerdir.

## <a name="overview"></a>Genel Bakış

> [!NOTE]
> Farklı yatay bölümleme bu DDL deyimleri parça eşlemesiyle hello esnek veritabanı istemci kitaplığı aracılığıyla veri katmanı tanımlama güvenmeyin.
>

1. [ANA ANAHTAR OLUŞTURMA](https://msdn.microsoft.com/library/ms174382.aspx)
2. [VERİTABANI KAPSAMLI OLUŞTURMAK KİMLİK BİLGİSİ](https://msdn.microsoft.com/library/mt270260.aspx)
3. [DIŞ VERİ KAYNAĞI OLUŞTURUN](https://msdn.microsoft.com/library/dn935022.aspx)
4. [DIŞ TABLO OLUŞTURMA](https://msdn.microsoft.com/library/dn935021.aspx) 

## <a name="create-database-scoped-master-key-and-credentials"></a>Kapsamlı veritabanı ana anahtarı ve kimlik bilgileri oluşturun
Merhaba kimlik bilgisi hello esnek sorgu tooconnect tooyour Uzak veritabanı tarafından kullanılır.  

    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'password';
    CREATE DATABASE SCOPED CREDENTIAL <credential_name>  WITH IDENTITY = '<username>',  
    SECRET = '<password>'
    [;]

> [!NOTE]
> Bu hello olun `<username>` içermez **"@servername"** soneki. 
>

## <a name="create-external-data-sources"></a>Dış veri kaynakları oluşturun
Sözdizimi:

    <External_Data_Source> ::=
    CREATE EXTERNAL DATA SOURCE <data_source_name> WITH 
               (TYPE = RDBMS,
                LOCATION = ’<fully_qualified_server_name>’,
                DATABASE_NAME = ‘<remote_database_name>’,  
                CREDENTIAL = <credential_name> 
                ) [;] 

> [!IMPORTANT]
> Merhaba tür parametresi çok ayarlanmalıdır**RDBMS**. 
>

### <a name="example"></a>Örnek
Merhaba aşağıdaki örnek hello CREATE deyimi dış veri kaynakları için hello kullanımını göstermektedir. 

    CREATE EXTERNAL DATA SOURCE RemoteReferenceData 
    WITH 
    ( 
        TYPE=RDBMS, 
        LOCATION='myserver.database.windows.net', 
        DATABASE_NAME='ReferenceData', 
        CREDENTIAL= SqlUser 
    ); 

Geçerli dış veri kaynakları tooretrieve hello listesi: 

    select * from sys.external_data_sources; 

### <a name="external-tables"></a>Dış tablolar
Sözdizimi:

    CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name . ] table_name  
    ( { <column_definition> } [ ,...n ])     
    { WITH ( <rdbms_external_table_options> ) } 
    )[;] 

    <rdbms_external_table_options> ::= 
      DATA_SOURCE = <External_Data_Source>, 
      [ SCHEMA_NAME = N'nonescaped_schema_name',] 
      [ OBJECT_NAME = N'nonescaped_object_name',] 

### <a name="example"></a>Örnek
    CREATE EXTERNAL TABLE [dbo].[customer]( 
        [c_id] int NOT NULL, 
        [c_firstname] nvarchar(256) NULL, 
        [c_lastname] nvarchar(256) NOT NULL, 
        [street] nvarchar(256) NOT NULL, 
        [city] nvarchar(256) NOT NULL, 
        [state] nvarchar(20) NULL, 
        [country] nvarchar(50) NOT NULL, 
    ) 
    WITH 
    ( 
           DATA_SOURCE = RemoteReferenceData 
    ); 

Aşağıdaki örnek hello nasıl tooretrieve hello hello geçerli veritabanından dış tablolar listesini gösterir: 

    select * from sys.external_tables; 

### <a name="remarks"></a>Açıklamalar
Esnek sorgu türü RDBMS dış veri kaynakları kullanan hello varolan dış tablo sözdizimi toodefine dış tablolara genişletir. Dikey bölümleme için bir dış tablo tanımındaki yönlerini aşağıdaki hello kapsar: 

* **Şema**: hello dış tablo DDL sorgularınızı kullanabileceğiniz bir şema tanımlar. Dış tablo tanımı'nda sağlanan hello şema hello hello gerçek verilerinin depolandığı hello Uzak veritabanı tablolarında toomatch hello şeması gerekir. 
* **Uzak veritabanı başvuru**: hello dış tablo DDL tooan dış veri kaynağına başvuruyor. Merhaba dış veri kaynağına hello mantıksal sunucu adını ve veritabanı adını hello uzak veritabanının hello gerçek tablo verilerinin nerede depolanacağını belirtir. 

Dış veri kaynağına hello önceki bölümde özetlendiği gibi kullanarak, hello sözdizimi toocreate dış tablolara şu şekildedir: 

Merhaba DATA_SOURCE tümcesi hello dış tablo için kullanılan hello dış veri kaynağı (dikey bölümleme durumunda yani hello Uzak veritabanı) tanımlar.  

Merhaba SCHEMA_NAME ve OBJECT_NAME yan tümceleri hello özelliği toomap hello dış tablo tanımı tooa tabloda farklı bir şema hello Uzak veritabanı veya farklı bir adla tooa tablo sırasıyla sağlar. Bu toodefine bir dış tablo tooa Katalog görünümü veya DMV uzak veritabanınızı - veya burada hello uzak tablo adı zaten yerel olarak alınmış diğer durum istiyorsanız kullanışlıdır.  

Merhaba aşağıdaki DDL deyimi var olan bir dış tablo tanımındaki hello yerel Kataloğu'ndan bırakır. Merhaba Uzak veritabanı etkilemez. 

    DROP EXTERNAL TABLE [ [ schema_name ] . | schema_name. ] table_name[;]  

**CREATE/DROP dış tablo izinlerini**: dış tablo aynı zamanda olan DDL toorefer toohello temel alınan veri kaynağı gerekli için ALTER ANY dış veri kaynağı izinleri gerekiyor.  

## <a name="security-considerations"></a>Güvenlikle ilgili dikkat edilmesi gerekenler
Erişim toohello dış tablo kullanıcılarla otomatik olarak toohello temel alınan uzak tablolar hello dış veri kaynağı tanımına verilen hello kimlik bilgileri altında erişin. Dikkatli bir şekilde erişim toohello dış tablosunda sipariş istenmeden tooavoid ayrıcalıkların hello kimlik bilgisi hello dış veri kaynağının aracılığıyla yönetmeniz gerekir. Yalnızca dizinindeymiş gibi olağan bir tablo normal SQL izinleri kullanılan tooGRANT veya REVOKE erişim tooan dış tablo olabilir.  

## <a name="example-querying-vertically-partitioned-databases"></a>Örnek: dikey sorgulama veritabanları bölümlenmiş
Merhaba aşağıdaki sorguyu hello siparişleri ve sipariş satırlarını için iki yerel tabloları ve hello uzak tablo arasında üç yönlü birleşim müşteriler için gerçekleştirir. Bu, hello başvuru verileri kullanım durumu için esnek sorgu örneğidir: 

    SELECT      
     c_id as customer,
     c_lastname as customer_name,
     count(*) as cnt_orderline, 
     max(ol_quantity) as max_quantity,
     avg(ol_amount) as avg_amount,
     min(ol_delivery_d) as min_deliv_date
    FROM customer 
    JOIN orders 
    ON c_id = o_c_id
    JOIN  order_line 
    ON o_id = ol_o_id and o_c_id = ol_c_id
    WHERE c_id = 100


## <a name="stored-procedure-for-remote-t-sql-execution-spexecuteremote"></a>Saklı yordamı uzaktan T-SQL yürütmesi için: sp\_execute_remote
Esnek sorgu aynı zamanda toohello parça doğrudan erişim sağlayan bir saklı yordam sunar. Merhaba saklı yordam adı verilir [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) ve kullanılan tooexecute uzak saklı yordamları veya T-SQL kodunu hello Uzak veritabanı üzerinde çalıştırılabilir. Şu parametreler hello alır: 

* Veri kaynağı adı (nvarchar): hello dış veri kaynağı türü RDBMS hello adı. 
* Sorgu (nvarchar): hello T-SQL sorgusu toobe her parça üzerinde yürütülür. 
* Parametre bildirimi (nvarchar) - isteğe bağlı: dize veri türü tanımları (gibi sp_executesql) hello Sorgu parametresinde kullanılan hello parametreler için. 
* Parametre değeri listesi - isteğe bağlı: parametre değerleri (gibi sp_executesql) virgülle ayrılmış listesi.

Merhaba sp\_yürütme\_uzak kullanır hello hello çağırma parametreleri tooexecute hello T-SQL deyimini hello uzak veritabanlarında verilen sağlanan dış veri kaynağı. Merhaba dış veri kaynağı tooconnect toohello shardmap manager veritabanı ve hello uzak veritabanlarına hello kimlik bilgisi kullanır.  

Örnek: 

    EXEC sp_execute_remote
        N'MyExtSrc',
        N'select count(w_id) as foo from warehouse' 



## <a name="connectivity-for-tools"></a>Bağlantı için araçları
Etkin Esnek sorgu ve tanımlanan dış tablolara hello SQL DB sunucusunda, BI ve veri tümleştirme araçları toodatabases normal SQL Server bağlantı dizelerini tooconnect kullanabilirsiniz. SQL Server, aracı için bir veri kaynağı olarak desteklendiğinden emin olun. Ardından toohello esnek sorgu veritabanını ve aracınızı toowith bağlamak yalnızca herhangi diğer SQL Server veritabanı gibi dış tabloları bakın. 

## <a name="best-practices"></a>En iyi uygulamalar
* Hello esnek sorgu uç veritabanı erişim toohello uzak veritabanına erişim Azure hizmetlerini SQL DB güvenlik duvarı yapılandırmasıyla etkinleştirerek verilip verilmediğini emin olun. Ayrıca hello dış veri kaynağı tanımını hello uzak veritabanına başarıyla oturum açabilir ve hello izinleri tooaccess hello uzak tablo sahip sağlanan bu hello kimlik bilgisi emin olun.  
* Esnek sorgu hello hesaplama çoğunu hello uzak veritabanlarında burada yapılabilir sorguları için en iyi şekilde çalışır. Genellikle hello en iyi sorgu performansını hello uzak veritabanları veya tamamen hello Uzak veritabanı üzerinde gerçekleştirilebilir birleştirmeler hesaplanan seçmeli filtre koşulları sahip olursunuz. Diğer sorgu desenlerine tooload büyük miktarlarda veri hello uzak veritabanından gerekebilir ve kötü gerçekleştirebilir. 

## <a name="next-steps"></a>Sonraki adımlar

* Esnek sorgu genel bakış için bkz: [esnek sorgu genel bakış](sql-database-elastic-query-overview.md).
* Dikey bölümleme öğretici için bkz: [(dikey bölümleme) veritabanları arası sorgusu ile çalışmaya başlama](sql-database-elastic-query-getting-started-vertical.md).
* Yatay bölümleme (parçalama) bir öğretici için bkz: [yatay (parçalama) bölümleme için esnek sorgu ile çalışmaya başlama](sql-database-elastic-query-getting-started.md).
* Yatay olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [yatay sorgulama bölümlenmiş veri)](sql-database-elastic-query-horizontal-partitioning.md)
* Bkz: [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) tek uzaktan Azure SQL veritabanı ya da yatay bölümleme düzenindeki parça olarak hizmet veren bir veritabanları kümesi üzerinde bir Transact-SQL deyimini yürütür bir saklı yordam için.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-vertical-partitioning/verticalpartitioning.png


<!--anchors-->
