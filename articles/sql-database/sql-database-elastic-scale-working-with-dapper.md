---
title: "Dapper aaaUsing esnek veritabanı istemci kitaplığı | Microsoft Docs"
description: "Esnek veritabanı istemci kitaplığı ile Dapper kullanıyor."
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
ms.assetid: 463d2676-3b19-47c2-83df-f8c50492c9d2
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/27/2016
ms.author: torsteng
ms.openlocfilehash: c22ece2a977265e93850f0ad3f3ca48f0a8733ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-elastic-database-client-library-with-dapper"></a>Esnek veritabanı istemci kitaplığı Dapper ile kullanma
Bu belge, Dapper toobuild uygulamaları kullanan ancak aynı zamanda tooembrace isteyen geliştiriciler için değil [esnek veritabanı araçları](sql-database-elastic-scale-introduction.md) parçalama tooscale kullanıma kendi veri katmanı uygulama toocreate uygulamalar.  Bu belge esnek veritabanı araçları ile gerekli toointegrate olan Dapper tabanlı uygulamalarda hello değişiklikleri gösterilmektedir. Bizim odak hello esnek veritabanı parça yönetimi ve veri bağımlı oluşturma üzerinde Dapper ile gönderiyor. 

**Örnek kod**: [Azure SQL veritabanı - Dapper tümleştirme için esnek veritabanı araçlarını](https://code.msdn.microsoft.com/Elastic-Scale-with-Azure-e19fc77f).

Tümleştirme **Dapper** ve **DapperExtensions** hello ile Azure SQL veritabanı için esnek veritabanı istemci kitaplığı kolaydır. Uygulamalarınızın veri hello oluşturma değiştirme ve, yeni açarak yönlendirme bağımlı kullanabilirsiniz [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) nesneleri toouse hello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) çağrısı hello [istemci Kitaplık](http://msdn.microsoft.com/library/azure/dn765902.aspx). Bu yeni bağlantı burada oluşturulan ve açılan, uygulama tooonly değişiklikleri sınırlar. 

## <a name="dapper-overview"></a>Dapper genel bakış
**Dapper** bir nesne ilişkisel Eşleyici olduğu. .NET nesneleri uygulama tooa ilişkisel veritabanı (ve tersi) eşler. Merhaba ilk hello örnek kod parçası, nasıl Dapper tabanlı uygulamalarla hello esnek veritabanı istemci kitaplığı tümleştirebilir gösterilmektedir. Merhaba ikinci hello örnek kod parçası gösterilmektedir nasıl Dapper ve DapperExtensions kullanırken toointegrate.  

Merhaba Eşleyici Dapper işlevindeki yürütme veya sorgulanırken hello veritabanı gönderiliyor T-SQL deyimlerini basitleştirmek veritabanı bağlantılarını genişletme yöntemleri sağlar. Örneğin, Dapper .NET nesneleri ve SQL deyimlerini hello parametrelerinin arasındaki kolay toomap kolaylaştırır **yürütme** çağrıları ya da tooconsume hello sorgularınızın sonuçlarıyla ilgili SQL kullanarak .NET nesneleri içine **sorgu**Dapper gelen çağrıları. 

DapperExtensions kullanırken, artık tooprovide hello SQL deyimlerini gerekmez. Genişletme yöntemleri gibi **GetList** veya **Ekle** hello veritabanı bağlantısı üzerinden hello hello perde arkasında SQL deyimleri oluşturma.

Başka bir avantaj Dapper ve ayrıca DapperExtensions hello uygulama denetimleri hello veritabanı bağlantısı oluşturulmasını hello olmalıdır. Bu, hangi Aracıların shardlets toodatabases hello eşleşmeye göre bağlantıları veritabanı hello esnek veritabanı istemci kitaplığı ile etkileşim yardımcı olur.

tooget hello Dapper derlemeler, bkz: [Dapper dot net](http://www.nuget.org/packages/Dapper/). Merhaba Dapper uzantıları için bkz: [DapperExtensions](http://www.nuget.org/packages/DapperExtensions).

## <a name="a-quick-look-at-hello-elastic-database-client-library"></a>Merhaba esnek veritabanı istemci kitaplığı hızlı bir bakış
Adlı uygulama verilerinizi bölümlerini tanımladığınız Hello esnek veritabanı istemci kitaplığı ile *shardlets* toodatabases harita ve onlar tarafından tanımlamak *parçalama anahtarları*. Gerekir ve bu veritabanları arasında shardlets dağıtmak sayıda veritabanı olabilir. Merhaba eşleme parçalama anahtar değerleri toohello veritabanlarının hello kitaplığın API'leri tarafından sağlanan bir parça eşleme tarafından depolanır. Bu özellik adında **parça eşleme Yönetim**. Merhaba parça eşleme hello Aracısı parçalama anahtar taşımak istekleri için veritabanı bağlantılarının de görür. Bu özellik, başvurulan tooas yöneliktir **veri bağımlı yönlendirme**.

![Parça eşlemeleri ve veri bağımlı yönlendirme][1]

Merhaba parça eşleme Yöneticisi eşzamanlı shardlet yönetim işlemlerini hello veritabanlarında gerçekleştiği yüklendiğinde oluşabilecek shardlet veri tutarsız görünümleri kullanıcıları korur. toodo, bu nedenle, parça eşlemeleri Aracısı hello veritabanı bağlantılarını hello kitaplığı ile oluşturulmuş bir uygulama için hello. Parça yönetim işlemlerini hello shardlet etkileyebilir olduğunda bu bir veritabanı bağlantısı hello parça eşleme işlevselliği tooautomatically KILL izin verir. 

Merhaba geleneksel bir şekilde toocreate bağlantıları için Dapper kullanmak yerine, toouse hello ihtiyacımız [OpenConnectionForKey yöntemi](http://msdn.microsoft.com/library/azure/dn824099.aspx). Bu, tüm hello doğrulama gerçekleşir ve herhangi bir veri parça arasında taşındığında bağlantıları düzgün yönetilen sağlar.

### <a name="requirements-for-dapper-integration"></a>Dapper tümleştirme gereksinimleri
Merhaba esnek veritabanı istemci kitaplığı ve hello Dapper API'leri ile çalışırken, aşağıdaki özelliklere tooretain hello istiyoruz:

* **Genişletme**: tooadd istediğiniz veya veritabanlarını uygulamasının hello parçalı hello kapasite talebi için gerektikçe hello uygulamasının veri katmanı hello kaldırın. 
* **Tutarlılık**: uygulamamız parçalama kullanılarak ölçeklenir olduğundan, veri tooperform bağımlı yönlendirme gerekir. Toouse hello veri bağımlı yönlendirme yeteneklerine hello kitaplığı toodo şekilde istiyoruz. Özellikle, tooretain hello doğrulama istiyoruz ve sipariş tooavoid Bozulması veya yanlış sorgu sonuçları hello parça eşleme Yöneticisi aracılığıyla aracılı bağlantılar tarafından sağlanan tutarlılığı garanti altına alır. Bu, bu bağlantıları tooa shardlet verilen reddedildi veya (örneğin) hello shardlet bölünmüş/Merge API'lerini kullanarak şu anda taşınan tooa farklı parça ise durduruldu sağlar.
* **Nesne eşleme**: hello uygulamada sınıfları ve temel veritabanı yapılarını hello arasında Dapper tootranslate tarafından sağlanan hello eşlemeleri tooretain hello kolaylık istiyoruz. 

Hello aşağıdaki bölümde yönelik yönergeler dayalı uygulamalar için bu gereksinimleri sağlanmaktadır **Dapper** ve **DapperExtensions**.

## <a name="technical-guidance"></a>Teknik Kılavuzu
### <a name="data-dependent-routing-with-dapper"></a>Veri Dapper ile yönlendirme bağımlı
Dapper ile Merhaba uygulaması oluşturmak ve veritabanı arka plandaki hello bağlantıları toohello açmak için genellikle sorumludur. .NET koleksiyonları türü T. Dapper gerçekleştirirken hello eşleme hello T-SQL sonuç satırları toohello nesnelerden t türü T türü hello uygulama tarafından verilen, Dapper sorgu sonuçlarını döndürür Benzer şekilde, Dapper SQL değerleri veya veri işleme dili (DML) deyimleri parametrelerini .NET nesneleri eşler. Dapper hello normal üzerinde genişletme yöntemleri aracılığıyla bu işlevselliği sunar [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) hello ADO .NET SQL istemci kitaplıklarından nesnesi. Merhaba DDR için esnek ölçeklendirme API'leri hello tarafından döndürülen SQL bağlantısı normal de [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) nesneleri. Ayrıca basit SQL istemci bağlantısı olarak bu bize toodirectly kullanım Dapper uzantıları hello istemci kitaplığının DDR API tarafından döndürülen hello türü üzerinden sağlar.

Bu gözlemleri hello esnek veritabanı istemci kitaplığı tarafından Dapper için aracılı basit toouse bağlantıları kolaylaştırır.

Bu kod örneğindeki (Merhaba) örnek eşlik hello uygulama toohello kitaplığı toobroker hello bağlantı toohello sağ parça tarafından sağlanan hello parçalama anahtar burada hello yaklaşımı açıklar.   

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                     key: tenantId1, 
                     connectionString: connStrBldr.ConnectionString, 
                     options: ConnectionOptions.Validate))
    {
        var blog = new Blog { Name = name };
        sqlconn.Execute(@"
                      INSERT INTO
                            Blog (Name)
                            VALUES (@name)", new { name = blog.Name }
                        );
    }

Merhaba çağrısı toohello [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) API hello varsayılan oluşturma ve SQL istemci bağlantısı açılırken yerini alır. Merhaba [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) çağrısı veri bağımlı yönlendirme için gerekli olan hello bağımsız değişkenleri alır: 

* veri bağımlı yönlendirme arabirimlerini Hello parça eşleme tooaccess hello
* Merhaba parçalama anahtar tooidentify hello shardlet
* Merhaba kimlik (kullanıcı adı ve parola) tooconnect toohello parça

Merhaba shardlet parçalama anahtarı verilen hello için tutan bir bağlantı toohello parça Hello parça eşleme nesnesi oluşturur. Merhaba esnek veritabanı istemci API de etiket hello bağlantı tooimplement kendi tutarlılığı garanti altına alır. Bu yana Hello çağrı çok[OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) normal SQL istemci bağlantısı nesnesi, hello sonraki çağrı toohello verir **yürütme** Dapper aşağıdaki uzantısı yönteminden hello standart Dapper yöntem.

Sorguları iş çok hello aynı şekilde - ilk hello bağlantıyla açtığınız [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello istemciden API. Ardından .NET nesnelerini hello normal Dapper uzantı yöntemleri toomap hello SQL Sorgunuzun sonuçlarını kullanın:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId1, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate ))
    {    
           // Display all Blogs for tenant 1
           IEnumerable<Blog> result = sqlconn.Query<Blog>(@"
                                SELECT * 
                                FROM Blog
                                ORDER BY Name");

           Console.WriteLine("All blogs for tenant id {0}:", tenantId1);
           foreach (var item in result)
           {
                Console.WriteLine(item.Name);
            }
    }

Bu hello Not **kullanarak** hello DDR bağlantı kapsamlarla hello blok toohello bir parça tenantId1 nerede tutulur içindeki tüm veritabanı işlemleri engelleyin. Merhaba sorgu yalnızca hello geçerli parça ancak hello başka bir parça üzerinde depolanan olanları depolanan bloglar döndürür. 

## <a name="data-dependent-routing-with-dapper-and-dapperextensions"></a>Veri Dapper ve DapperExtensions yönlendirme bağımlı
Dapper bir daha kullanışlı ve soyutlama hello veritabanından veritabanı uygulamaları geliştirirken sağlayabilir ek uzantıları ekosistemi ile birlikte gelir. DapperExtensions bir örnektir. 

Uygulamanızda DapperExtensions kullanarak veritabanı bağlantılarını nasıl oluşturulduğunu ve yönetilen değiştirmez. Merhaba uygulamanın sorumluluk tooopen bağlantılar hala olduğunu ve normal SQL istemci bağlantısı nesneleri hello genişletme yöntemleri tarafından beklenir. Biz üzerinde hello güvenebilirsiniz [OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) yukarıda açıklandığı şekilde. Aşağıdaki kod örnekleri tarafından Göster Hello hello tek değişiklik biz artık toowrite hello T-SQL deyimleri sahip olabilir:

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           var blog = new Blog { Name = name2 };
           sqlconn.Insert(blog);
    }

Ve hello sorgu için hello kod örneği aşağıdadır: 

    using (SqlConnection sqlconn = shardingLayer.ShardMap.OpenConnectionForKey(
                    key: tenantId2, 
                    connectionString: connStrBldr.ConnectionString, 
                    options: ConnectionOptions.Validate))
    {
           // Display all Blogs for tenant 2
           IEnumerable<Blog> result = sqlconn.GetList<Blog>();
           Console.WriteLine("All blogs for tenant id {0}:", tenantId2);
           foreach (var item in result)
           {
               Console.WriteLine(item.Name);
           }
    }

### <a name="handling-transient-faults"></a>Geçici hata işleme
Merhaba Microsoft Patterns & yöntemler yayımlanan hello ekip [geçici hata işleme uygulama bloğu](http://msdn.microsoft.com/library/hh680934.aspx) toohelp uygulama geliştiricileri hello bulutta çalışan karşılaşılan yaygın geçici hata koşulları etkisini azaltır. Daha fazla bilgi için bkz: [Perseverance, tüm Triumphs gizliliği: hello geçici hata işleme uygulama bloğu kullanarak](http://msdn.microsoft.com/library/dn440719.aspx).

Merhaba geçici hata kitaplığı tooprotect geçici hataları karşı Hello kod örneği kullanır. 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() =>
    {
       using (SqlConnection sqlconn = 
          shardingLayer.ShardMap.OpenConnectionForKey(tenantId2, connStrBldr.ConnectionString, ConnectionOptions.Validate))
          {
              var blog = new Blog { Name = name2 };
              sqlconn.Insert(blog);
          }
    });

**SqlDatabaseUtils.SqlRetryPolicy** hello Yukarıdaki kod olarak tanımlanan bir **SqlDatabaseTransientErrorDetectionStrategy** bir yeniden deneme sayısı 10 ve 5 saniye ile yeniden denemeler arasındaki süre bekleyin. İşlemler kullanıyorsanız, yeniden deneme kapsamınızı geri toohello gider emin olun geçici bir hata hello durumda hello işlem başlangıcı.

## <a name="limitations"></a>Sınırlamalar
Bu belgede özetlenen hello yaklaşımlar birkaç sınırlama oluşturulmasını gerektirir:

* Bu belge için örnek kod Hello göstermek değil nasıl toomanage şema parça genelinde.
* Bir istek göz önüne alındığında, tüm veritabanı işleme hello isteğiyle sağlanan hello parçalama anahtarı tarafından tanımlandığı gibi tek bir parça içinde bulunur varsayıyoruz. Olası toomake parçalama anahtar kullanılabilir olmadığında ancak, bu varsayım her zaman, örneğin, tutmaz. tooaddress Bu, hello esnek veritabanı istemci kitaplığı içerir hello [MultiShardQuery sınıfı](http://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.query.multishardexception.aspx). Merhaba sınıfı birkaç parça sorgulama için bir bağlantı Özet uygular. MultiShardQuery Dapper birlikte kullanılması hello bu belgenin kapsamında değildir.

## <a name="conclusion"></a>Sonuç
Dapper ve DapperExtensions kullanarak uygulamaları kolayca Azure SQL veritabanı için esnek Veritabanı Araçları'ndan yararlanabilirsiniz. Bu belgede özetlenen hello adımları, hello oluşturma değiştirme ve, yeni açarak yönlendirme bağımlı veriler için hello aracın yeteneği bu uygulamaları kullanabilirsiniz [SqlConnection](http://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) nesneleri toouse hello [ OpenConnectionForKey](http://msdn.microsoft.com/library/azure/dn807226.aspx) hello esnek veritabanı istemci kitaplığı çağrısı. Bu yeni bağlantı burada oluşturulan ve açılan hello uygulama değişiklikleri gerekli toothose yerler sınırlar. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-working-with-dapper/dapperimage1.png
