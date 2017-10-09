---
title: "(yatay bölümleme) ölçeklendirilmiş bulut veritabanları arasında aaaReport | Microsoft Docs"
description: "nasıl toouse arası veritabanı veritabanı sorguları"
services: sql-database
documentationcenter: 
manager: jhubbard
author: MladjoA
ms.assetid: c81ef5e3-41e9-4fd2-8631-868f2e168147
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2016
ms.author: mlandzic
ms.openlocfilehash: e34f398f8d408cffd91a70fc2cfbda73daec3550
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="report-across-scaled-out-cloud-databases-preview"></a>Ölçeklendirilen bulut veritabanları arasında (Önizleme) raporu
Tek bir bağlantı noktası kullanarak birden çok Azure SQL veritabanından raporlar oluşturmak bir [esnek sorgu](sql-database-elastic-query-overview.md). Merhaba veritabanları yatay (aynı zamanda "parçalı" olarak da bilinir) bölümlenmiş olması gerekir.

Var olan bir veritabanı varsa, bkz: [veritabanları tooscaled kullanıma veritabanlarını taşıma varolan](sql-database-elastic-convert-to-use-elastic-tools.md).

toounderstand hello SQL nesneleri tooquery gerektiği için bkz: [sorgu yatay olarak bölümlenmiş veritabanları arasında](sql-database-elastic-query-horizontal-partitioning.md).

## <a name="prerequisites"></a>Ön koşullar
İndirme ve çalıştırma hello [esnek veritabanı araçlarını örneği ile çalışmaya başlama](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Merhaba örnek uygulaması kullanarak Yöneticisi bir parça eşlemesi oluşturma
Burada Yöneticisi birlikte hello parça veri ekleme tarafından izlenen birkaç parça parça eşleme oluşturur. Tooalready görülüyorsa parçalı veriler parça Kurulum'a olması, hello aşağıdaki adımları atlayın ve toohello sonraki bölümde taşıyın.

1. Derleme ve çalıştırma hello **esnek veritabanı araçlarını kullanmaya başlama** örnek uygulama. Adım 7 hello bölümünde kadar Hello adımları [hello örnek uygulamasını indirme ve çalıştırma](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). Adım 7 Hello sonunda, komut istemine aşağıdaki hello görürsünüz:

    ![Komut İstemi][1]
2. Merhaba komut penceresinde "1" yazın ve tuşuna basın **Enter**. Bu hello parça eşleme Yöneticisi oluşturur ve iki parça toohello sunucu ekler. Daha sonra "3" yazın ve basın **Enter**; hello eylem dört kez yineler. Bu örnek verileri satır, parça ekler.
3. Merhaba [Azure portal](https://portal.azure.com) üç yeni veritabanları sunucunuzun göstermesi gerekir:

   ![Visual Studio onayı][2]

   Bu noktada, veritabanları arası sorguları hello esnek veritabanı istemci kitaplıkları desteklenir. Örneğin, hello komut penceresinde 4 seçeneğini kullanın. bir çok parça sorgudan Hello sonuçlar her zaman bir **UNION ALL** tüm parça hello sonuçları.

   Merhaba sonraki bölümde, daha zengin hello verilerin parça sorgulama destekleyen bir örnek veritabanı uç noktası oluşturun.

## <a name="create-an-elastic-query-database"></a>Esnek sorgu veritabanı oluşturma
1. Açık hello [Azure portal](https://portal.azure.com) ve oturum açın.
2. Hello yeni Azure SQL veritabanı oluşturma parça kurulumunuzu aynı sunucu. Ad hello veritabanını "ElasticDBQuery."

    ![Azure portalı ve fiyatlandırma katmanı][3]

    > [!NOTE]
    > Varolan bir veritabanını kullanabilirsiniz. Bunu yapabilirsiniz tooexecute istediğiniz hello parça biri olması gerekir değil sorgularınızı üzerinde. Bu veritabanı, esnek veritabanı sorgusu için meta veri nesnelerinin hello oluşturmak için kullanılır.
    >

## <a name="create-database-objects"></a>Veritabanı nesneleri oluşturma
### <a name="database-scoped-master-key-and-credentials"></a>Veritabanı kapsamlı ana anahtar ve kimlik bilgileri
Kullanılan tooconnect toohello parça eşleme Yöneticisi ve hello parça şunlardır:

1. SQL Server Management Studio veya SQL Server veri araçları Visual Studio'da açın.
2. TooElasticDBQuery veritabanına bağlanmak ve aşağıdaki T-SQL komutlarıyla hello yürütün:

        CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<password>';

        CREATE DATABASE SCOPED CREDENTIAL ElasticDBQueryCred
        WITH IDENTITY = '<username>',
        SECRET = '<password>';

    "username" ve "parola" olması hello aynı yordamının 6. adımında kullanılan oturum açma bilgileri olarak [hello örnek uygulamasını indirme ve çalıştırma](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app) içinde [esnek veritabanı araçlarını kullanmaya başlama](sql-database-elastic-scale-get-started.md).

### <a name="external-data-sources"></a>Dış veri kaynakları
bir dış veri kaynağına toocreate komutu hello ElasticDBQuery veritabanında aşağıdaki hello yürütün:

    CREATE EXTERNAL DATA SOURCE MyElasticDBQueryDataSrc WITH
      (TYPE = SHARD_MAP_MANAGER,
      LOCATION = '<server_name>.database.windows.net',
      DATABASE_NAME = 'ElasticScaleStarterKit_ShardMapManagerDb',
      CREDENTIAL = ElasticDBQueryCred,
       SHARD_MAP_NAME = 'CustomerIDShardMap'
    ) ;

 Merhaba esnek veritabanı araçlarını örneğini kullanarak Yöneticisi hello parça eşleme ve parça eşleme oluşturduysanız "CustomerIDShardMap" Merhaba hello parça eşleme adıdır. Ancak, bu örnek için özel kurulum kullandıysanız, uygulamanızda seçtiğiniz hello parça eşleme adı olması gerekir.

### <a name="external-tables"></a>Dış tablolar
Komut ElasticDBQuery veritabanında aşağıdaki hello yürüterek hello parça hello Müşteriler tablosunda eşleşen bir dış tablo oluşturun:

    CREATE EXTERNAL TABLE [dbo].[Customers]
    ( [CustomerId] [int] NOT NULL,
      [Name] [nvarchar](256) NOT NULL,
      [RegionId] [int] NOT NULL)
    WITH
    ( DATA_SOURCE = MyElasticDBQueryDataSrc,
      DISTRIBUTION = SHARDED([CustomerId])
    ) ;

## <a name="execute-a-sample-elastic-database-t-sql-query"></a>Bir örnek esnek veritabanı T-SQL sorgusu yürütme
Dış veri kaynağınızda ve dış tablolarınızı tanımladıktan sonra dış tablolar üzerindeki tam T-SQL artık kullanabilirsiniz.

Bu sorgu hello ElasticDBQuery veritabanında yürütün:

    select count(CustomerId) from [dbo].[Customers]

Merhaba sorgulayan tüm hello parça sonuçları toplar ve çıktı aşağıdaki hello verir görürsünüz:

![Çıkış Ayrıntıları][4]

## <a name="import-elastic-database-query-results-tooexcel"></a>Esnek veritabanı sorgu sonuçları tooExcel alma
 Merhaba sonuçlarını bir sorgu tooan Excel dosyasını içeri aktarabilirsiniz.

1. Excel 2013'ü başlatın.
2. Toohello gidin **veri** Şerit.
3. Tıklatın **diğer kaynaklardan** tıklatıp **SQL Server'dan**.

   ![Excel Import diğer kaynaklardan][5]
4. Merhaba, **Veri Bağlantı Sihirbazı** hello sunucu adını ve oturum açma kimlik bilgilerini yazın. Ardından **İleri**'ye tıklayın.
5. Merhaba iletişim kutusunda **hello verileri içeren Select hello veritabanı**seçin hello **ElasticDBQuery** veritabanı.
6. Select hello **müşteriler** tablo hello liste görünümünde ve tıklayın **sonraki**. Ardından **son**.
7. Merhaba, **veri içeri aktarma** formunda, altında **nasıl bu verileri tooview çalışma kitabınızı istediğinizi seçin**seçin **tablo** tıklatıp **Tamam**.

Tüm satırları hello **müşteriler** tablo, farklı parça içinde depolanan doldurmak hello Excel sayfası.

Şimdi, Excel'in güçlü veri görselleştirme işlevlerini kullanabilirsiniz. Tooconnect BI ve veri tümleştirme araçları toohello esnek sorgu veritabanınızı kimlik bilgileri ve hello bağlantı dizesi, sunucu adı, veritabanı adı kullanabilirsiniz. SQL Server, aracı için bir veri kaynağı olarak desteklendiğinden emin olun. Toohello esnek sorgu veritabanını ve herhangi bir SQL Server veritabanı gibi dış tablolara ve SQL Server tablolarını aracınızı toowith bağlamak başvurabilir.

### <a name="cost"></a>Maliyet
Merhaba esnek veritabanı sorgusu özelliğini kullanmak için ek ücret yoktur.

Fiyatlandırma bilgileri için bkz: [SQL veritabanı fiyatlandırma ayrıntıları](https://azure.microsoft.com/pricing/details/sql-database/).

## <a name="next-steps"></a>Sonraki adımlar

* Esnek sorgu genel bakış için bkz: [esnek sorgu genel bakış](sql-database-elastic-query-overview.md).
* Dikey bölümleme öğretici için bkz: [(dikey bölümleme) veritabanları arası sorgusu ile çalışmaya başlama](sql-database-elastic-query-getting-started-vertical.md).
* Dikey olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [dikey sorgulama bölümlenmiş veri)](sql-database-elastic-query-vertical-partitioning.md)
* Yatay olarak bölümlenmiş verilere ilişkin söz dizimi ve örnek sorgular için bkz: [yatay sorgulama bölümlenmiş veri)](sql-database-elastic-query-horizontal-partitioning.md)
* Bkz: [sp\_yürütme \_uzak](https://msdn.microsoft.com/library/mt703714) tek uzaktan Azure SQL veritabanı ya da yatay bölümleme düzenindeki parça olarak hizmet veren bir veritabanları kümesi üzerinde bir Transact-SQL deyimini yürütür bir saklı yordam için.


<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
