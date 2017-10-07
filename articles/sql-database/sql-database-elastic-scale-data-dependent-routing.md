---
title: "Azure SQL veritabanı ile yönlendirme bağımlı aaaData | Microsoft Docs"
description: "Nasıl toouse hello veri bağımlı yönlendirme, Azure SQL veritabanında parçalı veritabanlarının bir özellik için .NET uygulamalarında ShardMapManager sınıfı"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: cad09e15-5561-4448-aa18-b38f54cda004
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ddove
ms.openlocfilehash: 34014508ae01905686791fe096bb275cb84f53b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-dependent-routing"></a>Verilere bağımlı yönlendirme
**Veri bağımlı yönlendirme** hello özelliği toouse hello veritabanında bir sorgu tooroute hello isteği tooan uygun verilerdir. Bu temel düzeni parçalı veritabanları ile çalışırken. özellikle hello parçalama anahtar hello sorgu parçası değilse hello istek bağlamı kullanılan tooroute hello isteği de olabilir. Her özel bir sorgu veya işlem veri bağımlı yönlendirme kullanarak bir uygulama içinde kısıtlı tooaccessing istek başına tek bir veritabanı değil. Hello Azure SQL veritabanı esnek araçlar bu üretim hello ile gerçekleştirilir  **[ShardMapManager sınıfı](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager.aspx)**  ADO.NET uygulamalarında.

Merhaba uygulaması, çeşitli bağlantı dizeleri veya hello parçalı ortamında verileri farklı dilimleri ilişkili DB konumları tootrack gerekmez. Bunun yerine, hello [parça eşleme Yöneticisi](sql-database-elastic-scale-shard-map-management.md) hello parça eşleme ve hello hello uygulamanın isteği hello hedefidir hello parçalama anahtarının değerini hello veriler temelinde gerekli olduğunda, açılır bağlantıları toohello doğru veritabanları. Merhaba anahtarıdır genellikle hello *customer_id*, *tenant_id*, *date_key*, veya temel parametresi hello veritabanı isteğinin bazı bir belirli tanıtıcı). 

Daha fazla bilgi için bkz: [ölçeklendirme çıkışı SQL Server ile veri bağımlı yönlendirme](https://technet.microsoft.com/library/cc966448.aspx).

## <a name="download-hello-client-library"></a>Merhaba istemci kitaplığı indirin
tooget hello sınıfı, yükleme hello [esnek veritabanı istemci Kitaplığı](http://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). 

## <a name="using-a-shardmapmanager-in-a-data-dependent-routing-application"></a>Bir ShardMapManager bir veri bağımlı yönlendirme uygulamasında kullanma
Uygulamaları hello örneği **ShardMapManager** hello fabrikada çağrısı kullanarak başlatma sırasında  **[GetSQLShardMapManager](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager.aspx)**. Bu örnekte, hem bir **ShardMapManager** ve belirli bir **ShardMap** içerdiği başlatılır. Gösterir hello GetSqlShardMapManager Bu örnek ve [GetRangeShardMap](https://msdn.microsoft.com/library/azure/dn824173.aspx) yöntemleri.

    ShardMapManager smm = ShardMapManagerFactory.GetSqlShardMapManager(smmConnnectionString, 
                      ShardMapManagerLoadPolicy.Lazy);
    RangeShardMap<int> customerShardMap = smm.GetRangeShardMap<int>("customerMap"); 

### <a name="use-lowest-privilege-credentials-possible-for-getting-hello-shard-map"></a>Merhaba parça eşleme için olası en düşük ayrıcalıklı kimlik bilgileri kullanın
Bir uygulama hello parça eşleme kendisini düzenleme değil, hello Fabrika yönteminde kullanılan hello kimlik hello üzerinde salt okunur yalnızca izinleri olmalıdır **genel parça eşleme** veritabanı. Bu kimlik bilgileri kullanılan kimlik bilgileri tooopen bağlantıları toohello parça eşleme yöneticisinden genellikle farklıdır. Ayrıca bkz. [kimlik bilgileri kullanılan tooaccess hello esnek veritabanı istemci Kitaplığı](sql-database-elastic-scale-manage-credentials.md). 

## <a name="call-hello-openconnectionforkey-method"></a>Merhaba OpenConnectionForKey yöntemini çağırın
Merhaba  **[ShardMap.OpenConnectionForKey yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey.aspx)**  bir ADO.Net bağlantı komutları toohello uygun veritabanı hello değerine göre hello verme için hazır döndürür **anahtar**parametresi. Parça bilgileri tarafından hello hello uygulamada önbelleğe **ShardMapManager**, bu istekleri genellikle bir veritabanı araması hello karşı içermeyen **genel parça eşleme** veritabanı. 

    // Syntax: 
    public SqlConnection OpenConnectionForKey<TKey>(
        TKey key,
        string connectionString,
        ConnectionOptions options
    )


* Merhaba **anahtar** parametresi kullanılır arama anahtarı olarak hello parça eşleme toodetermine hello uygun veritabanına hello talebi. 
* Merhaba **connectionString** kullanılan toopass istenen hello bağlantı için yalnızca hello kullanıcı kimlik bilgileri olan. Hiçbir veritabanı adı veya sunucu adı bu dahil edilen *connectionString* hello yöntemi hello veritabanı ve sunucu hello kullanarak belirlediğinden **ShardMap**. 
* Merhaba  **[connectionOptions](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.connectionoptions.aspx)**  çok ayarlanmalıdır**ConnectionOptions.Validate** burada parça eşleyen bir ortam değiştirebilir ve satırlar tooother veritabanları taşındığında bir bölme ve birleştirme işlemleri sonucu. Bu kısa sorgu toohello yerel parça eşleme içerir hello bağlantı önce hello hedef veritabanında (toohello genel parça eşleme değil) toohello uygulama teslim edilir. 

(Merhaba önbellek yanlış olduğunu belirten) hello yerel parça eşleme karşı Hello doğrulama başarısız olursa, hello parça eşleme Yöneticisi hello genel parça eşleme tooobtain hello yeni doğru değeri sorgu hello arama için güncelleştirme hello önbellek ve edinmeli ve dönüş hello uygun veritabanı bağlantısı. 

Kullanım **ConnectionOptions.None** uygulamanın çevrimiçi durumdayken yalnızca zaman parça eşleme değişiklikleri beklenmez. Bu durumda, önbelleğe alınmış hello değerleri tooalways doğru ve hello çok gidiş dönüş doğrulama çağrısı toohello hedef veritabanı güvenle atlanabilir varsayılabilir. Veritabanı trafiğini azaltır. Merhaba **connectionOptions** ayrıca bir yapılandırma dosyası tooindicate değerinde aracılığıyla parçalama değişiklikleri beklenen olup olmadığını veya bir zaman aralığında değil sırasında ayarlanabilir.  

Bu örnek bir tamsayı anahtarı hello değerini kullanır **CustomerID**kullanarak bir **ShardMap** adlı nesne **customerShardMap**.  

    int customerId = 12345; 
    int newPersonId = 4321; 

    // Connect toohello shard for that customer ID. No need toocall a SqlConnection 
    // constructor followed by hello Open method.
    using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId, 
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
    { 
        // Execute a simple command. 
        SqlCommand cmd = conn.CreateCommand(); 
        cmd.CommandText = @"UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID"; 

        cmd.Parameters.AddWithValue("@customerID", customerId); 
        cmd.Parameters.AddWithValue("@newPersonID", newPersonId); 
        cmd.ExecuteNonQuery(); 
    }  

Merhaba **OpenConnectionForKey** yöntemi yeni bir bağlantı zaten açık toohello doğru veritabanı döndürür. Bu şekilde kullanılan bağlantılar hala ADO.Net bağlantı havuzu tam avantajından yararlanmak. İşlemler ve istekleri tarafından bir parça aynı anda karşılanabilir sürece bu hello yalnızca değişikliği zaten ADO.Net kullanarak bir uygulama gerekli olmalıdır. 

Merhaba  **[OpenConnectionForKeyAsync yöntemi](https://msdn.microsoft.com/library/azure/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkeyasync.aspx)**  da uygulamanızı ADO.Net ile zaman uyumsuz programlama kullanım yaparsa kullanılabilir. Davranışını hello ADO eşdeğer yönlendirme bağımlı verilerdir. NET'in  **[Connection.OpenAsync](https://msdn.microsoft.com/library/hh223688\(v=vs.110\).aspx)**  yöntemi.

## <a name="integrating-with-transient-fault-handling"></a>Geçici hata işleme ile tümleştirme
Geçici hataları hello uygulama tarafından yakalanan ve bir hata atmadan önce birkaç kez yeniden hello işlemleri tooensure veri erişimi uygulamaları hello bulutta geliştirilmesi konusunda en iyi bir uygulamadır. Geçici hata bulut uygulamaları için işleme sırasında ele alınmıştır [geçici hata işleme](https://msdn.microsoft.com/library/dn440719\(v=pandp.60\).aspx). 

Geçici hata işleme hello veri bağımlı yönlendirme desenle doğal olarak bulunabilir. Merhaba anahtar tooretry hello tüm veri erişim isteği hello dahil olmak üzere gereksinimdir **kullanarak** hello veri bağımlı yönlendirme bağlantısı elde bloğu. Yukarıdaki örnekte Hello (vurgulanan değişiklik unutmayın) aşağıdaki gibi yeniden yazılmıştır. 

### <a name="example---data-dependent-routing-with-transient-fault-handling"></a>Örnek - veri geçici hata işleme ile yönlendirme bağımlı
<pre><code>int customerId = 12345; 
int newPersonId = 4321; 

<span style="background-color:  #FFFF00">Configuration.SqlRetryPolicy.ExecuteAction(() =&gt; </span> 
<span style="background-color:  #FFFF00">    { </span>
        // Connect toohello shard for a customer ID. 
        using (SqlConnection conn = customerShardMap.OpenConnectionForKey(customerId,  
        Configuration.GetCredentialsConnectionString(), ConnectionOptions.Validate)) 
        { 
            // Execute a simple command 
            SqlCommand cmd = conn.CreateCommand(); 

            cmd.CommandText = @&quot;UPDATE Sales.Customer 
                            SET PersonID = @newPersonID 
                            WHERE CustomerID = @customerID&quot;; 

            cmd.Parameters.AddWithValue(&quot;@customerID&quot;, customerId); 
            cmd.Parameters.AddWithValue(&quot;@newPersonID&quot;, newPersonId); 
            cmd.ExecuteNonQuery(); 

            Console.WriteLine(&quot;Update completed&quot;); 
        } 
<span style="background-color:  #FFFF00">    }); </span> 
</code></pre>


Gerekli tooimplement geçici hata işleme olan paketler Merhaba esnek veritabanı örnek uygulaması oluşturduğunuzda otomatik olarak yüklenir. Paketleri de edinilebilir ayrı olarak [Kurumsal Library - geçici hata işleme uygulama blok](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/). Sürüm 6.0 veya üstü kullanın. 

## <a name="transactional-consistency"></a>İşlem tutarlılığı
İşlem özellikleri için tüm işlemleri yerel tooa parça sağlanır. Örneğin, veri bağımlı yönlendirme üzerinden gönderilen işlemleri hello kapsamını hello hedef parça hello bağlantı içinde yürütün. Şu anda bir işlem içinde birden çok bağlantı kaydetme için sağlanan özelliği yoktur ve bu nedenle parça üzerinde gerçekleştirilen işlemler için işlem garanti vardır.

## <a name="next-steps"></a>Sonraki adımlar
toodetach bir parça ya da tooreattach bir parça bakın [hello RecoveryManager sınıfı toofix parça eşlemesi sorunlarının kullanma](sql-database-elastic-database-recovery-manager.md)

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

