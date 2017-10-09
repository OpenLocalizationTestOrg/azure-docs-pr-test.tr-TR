---
title: "Entity Framework aaaUsing esnek veritabanı istemci kitaplığı | Microsoft Docs"
description: "Esnek veritabanı istemci kitaplığı ve Entity Framework veritabanları kodlama için kullanın"
services: sql-database
documentationcenter: 
manager: jhubbard
author: torsteng
editor: 
ms.assetid: b9c3065b-cb92-41be-aa7f-deba23e7e159
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: torsteng
ms.openlocfilehash: 917f6d28d9855c0b42afe2c008613a9bbb3ec6b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="elastic-database-client-library-with-entity-framework"></a>Entity Framework ile esnek veritabanı istemci kitaplığı
Bu belge, uygulamada hello ile gerekli toointegrate olan Entity Framework hello değişiklikleri gösterir. [esnek veritabanı araçlarını](sql-database-elastic-scale-introduction.md). Merhaba odak noktasıdır oluşturma üzerinde [parça eşleme Yönetim](sql-database-elastic-scale-shard-map-management.md) ve [veri bağımlı yönlendirme](sql-database-elastic-scale-data-dependent-routing.md) hello Entity Framework ile **Code First** yaklaşım. Merhaba [ilk - yeni veritabanı kod](http://msdn.microsoft.com/data/jj193542.aspx) öğretici EF için bu belge boyunca çalışan bizim örnek olarak hizmet verir. Bu belge eşlik hello örnek kod, esnek veritabanı araçlarını hello Visual Studio kod örnekleri örnekleri kümesi parçasıdır.

## <a name="downloading-and-running-hello-sample-code"></a>Yükleme ve başlangıç örnek kodu çalıştırma
Bu makale için toodownload hello kodu:

* Visual Studio 2012 veya üzeri gereklidir. 
* Merhaba karşıdan [Azure SQL - Entity Framework tümleştirme örneği için esnek DB Araçları](https://code.msdn.microsoft.com/windowsapps/Elastic-Scale-with-Azure-bae904ba) MSDN'den. Seçtiğiniz hello örnek tooa konumu sıkıştırmasını açın.
* Visual Studio’yu çalıştırın. 
* Visual Studio'da Aç proje/çözüm dosyasını seçin ->. 
* Merhaba, **Proje Aç** iletişim kutusunda, indirdiğiniz toohello örnek gidin ve seçin **EntityFrameworkCodeFirst.sln** tooopen hello örnek. 

toorun hello örnek toocreate üç boş veritabanları, Azure SQL veritabanında gerekir:

* Parça eşleme Manager veritabanı
* Parça 1 veritabanı
* Parça 2 veritabanı

Bu veritabanları oluşturduktan sonra hello yer tutucu doldurun **Program.cs** Azure SQL veritabanı sunucunuzun adını, hello veritabanı adları ve kimlik bilgilerini tooconnect toohello veritabanlarınızı. Visual Studio'da Hello çözümü oluşturun. Visual Studio hello esnek veritabanı istemci kitaplığı, Entity Framework ve geçici hello derleme işleminin bir parçası işleme hata için gerekli hello NuGet paketlerini indirir. NuGet paketleri geri çözümünüz için etkinleştirildiğinden emin olun. Visual Studio Çözüm Gezgini hello hello çözüm dosyasında sağ tıklayarak bu ayarı etkinleştirebilirsiniz. 

## <a name="entity-framework-workflows"></a>Entity Framework iş akışları
Entity Framework geliştiriciler dört iş akışları toobuild uygulamalar ve uygulama nesneleri tooensure kalıcılığını aşağıdaki hello birini kullanır: 

* **(Yeni veritabanı) ilk kod**: hello EF Geliştirici hello uygulama kodunda hello modeli oluşturur ve ardından EF hello veritabanı ondan oluşturur. 
* **İlk (var olan veritabanı) kod**: hello Geliştirici hello uygulama kodu hello modeli için varolan bir veritabanından oluşturmak EF olanak sağlar.
* **Model ilk**: hello Geliştirici hello modeli hello EF Designer'da ve ardından EF hello veritabanı hello modelden oluşturur.
* **Veritabanı ilk**: hello Geliştirici tooinfer hello varolan bir veritabanını modelden tooling EF kullanır. 

Veritabanı bağlantılarını ve veritabanı şeması bir uygulama için tüm bu yaklaşımlar hello DbContext sınıfı tootransparently üzerinde kullanan yönetin. Merhaba belgenin ilerleyen bölümlerinde daha ayrıntılı bağlantı oluşturma üzerinde denetim farklı düzeylerde hello DbContext temel sınıf farklı oluşturucularda izin aşağıdakiler ele alınacaktır olarak önyükleme ve şema oluşturma veritabanı. Öncelikle Itanium tabanlı sistemler için hello bağlantı yönetim özellikleri, sağlanan hello veri bağımlı yönlendirme arabirimleri ile Merhaba veritabanı bağlantısı yönetimini EF tarafından sağlanan kesiştiğinden hello olgu zorluklar hello esnek veritabanı istemci kitaplığı tarafından kaynaklanır. 

## <a name="elastic-database-tools-assumptions"></a>Varsayımlar esnek veritabanı araçları
Terim tanımları için bkz: [esnek veritabanı araçlarını sözlüğü](sql-database-elastic-scale-glossary.md).

Esnek veritabanı istemci kitaplığı ile uygulama verilerinizi shardlets adlı Bölüm tanımlayın. Shardlets bir parçalama anahtar tarafından tanımlanır ve eşlenen toospecific veritabanlarıdır. Bir uygulama gerekli tüm veritabanı ve yeterli kapasitesi veya geçerli iş gereksinimlerini verilen performans hello shardlets tooprovide dağıtmak olabilirsiniz. Merhaba eşleme parçalama anahtar değerleri toohello veritabanlarının hello esnek veritabanı istemci API tarafından sağlanan bir parça eşleme tarafından depolanır. Bu özellik diyoruz **parça eşleme Yönetim**, veya kısaca SMM. Merhaba parça eşleme hello Aracısı parçalama anahtar taşımak istekleri için veritabanı bağlantılarının de görür. Biz toothis özelliği olarak başvuran **veri bağımlı yönlendirme**. 

Merhaba parça eşleme Yöneticisi kullanıcıları tutarsız görünümleri eşzamanlı shardlet yönetim işlemlerini (örneğin, bir parça tooanother verileri yeniden konumlandırma) gerçekleştiği yüklendiğinde oluşabilecek shardlet verilerini korur. toodo, bu nedenle, parça eşlemeleri hello istemci Kitaplığı Aracısı hello veritabanı bağlantıları için bir uygulama tarafından yönetilen hello. Parça yönetim işlemlerini hello bağlantı için oluşturulan hello shardlet etkileyebilir olduğunda bu bir veritabanı bağlantısı hello parça eşleme işlevselliği tooautomatically KILL izin verir. Bu yaklaşım, bazı veritabanı varlığı için varolan bir tek toocheck yeni bağlantı oluşturma gibi EF'ın işlevlerini toointegrate gerekir. Genel olarak, bizim gözlem hello standart DbContext oluşturucular yalnızca güvenilir bir şekilde güvenli bir şekilde kopyalanıp kapalı veritabanı bağlantıları için çalıştığını bırakıldı EF iş için. Merhaba tasarım esnek veritabanı yerine tooonly açılan Aracısı bağlantıları ilkesidir. Bir hello istemci kitaplığı tarafından EF DbContext toohello teslim etmeden önce aracılı bağlantı kesiliyor bu sorunu çözebilir düşünebilirsiniz. Ancak, hello bağlantı kesiliyor ve EF toore-Aç bağlı olan bir hello kitaplığı tarafından gerçekleştirilen hello doğrulama ve tutarlılık denetimleri sağlamlığın gerisinde kalır. EF, Hello geçişler işlevi ancak, bu bağlantıları toomanage hello saydam toohello uygulama şekilde veritabanı şemasını temel kullanır. İdeal olarak, biz gibi tooretain ve tüm bu özelliklere hello esnek veritabanı istemci kitaplığı ve EF hello birleştirmek aynı uygulama. Merhaba aşağıdaki bölümde bu özellikleri ve gereksinimleri daha ayrıntılı açıklanmıştır. 

## <a name="requirements"></a>Gereksinimler
Merhaba esnek veritabanı istemci kitaplığı ve Entity Framework API'leri ile çalışırken, aşağıdaki özelliklere tooretain hello istiyoruz: 

* **Genişleme**: hello veri katmanı uygulamasının hello parçalı hello kapasite talebi için gerektikçe hello uygulamasının tooadd veya kaldırma veritabanlarından. Bu hello hello oluşturulması ve veritabanları ve hello esnek veritabanı parça eşleme manager API'leri toomanage veritabanları ve shardlets eşlemelerini kullanma silinmesini üzerinde denetim anlamına gelir. 
* **Tutarlılık**: Merhaba uygulaması parçalama kullanır ve kullandığı veri bağımlı yönlendirme özellikleri hello istemci kitaplığının hello. bağlantıları aracılı tooavoid bozulma veya yanlış sorgu sonuçları, aracılığıyla hello parça eşleme Yöneticisi. Bu ayrıca doğrulama ve tutarlılık korur.
* **İlk kod**: tooretain hello EF'ın kod ilk kip kolaylığı. Code First içinde Merhaba uygulaması sınıflarda saydam eşlenen veritabanı yapılarını temel toohello. Merhaba uygulama kodu birçok yönüyle veritabanı işleme temel hello söz konusu maske DbSets ile etkileşim kurar.
* **Şema**: Entity Framework ilk veritabanı şeması oluşturma ve sonraki şema evrimi geçişleri üzerinden işler. Bu özellikler koruyarak uygulamanızı uyarlama veri dönüşmesi hello kolaydır. 

Merhaba aşağıdaki kılavuz kaldırmasını nasıl toosatisfy esnek veritabanı araçlarını kullanarak Code First uygulamalar için bu gereksinimleri. 

## <a name="data-dependent-routing-using-ef-dbcontext"></a>Veri bağımlı yönlendirme EF DbContext kullanma
Entity Framework veritabanı bağlantılarıyla genellikle alt sınıflarının yönetilen **DbContext**. Bu alt sınıflarından türetme tarafından oluşturma **DbContext**. Burada, tanımlarsınız, **DbSets** uygulamanız için CLR nesnesi hello veritabanı yedeği koleksiyonları uygulayın. Veri bağımlı yönlendirme hello bağlamında, biz diğer EF kodu ilk uygulama senaryoları için mutlaka tutmayın çeşitli yararlı özelliklerini tanımlayabilirsiniz: 

* Merhaba veritabanı zaten var ve hello esnek veritabanı parça eşlemesinde kaydedildi. 
* Merhaba uygulaması Hello şeması (aşağıda açıklanmıştır) dağıtılan toohello veritabanı zaten etkinleştirilmiş. 
* Veri bağımlı yönlendirme bağlantıları toohello veritabanı hello parça eşleme tarafından aracılı. 

toointegrate **DbContexts** veri bağımlı genişleme için Yönlendirme:

1. Merhaba parça eşleme Yöneticisi'nin hello esnek veritabanı istemci arabirimleri aracılığıyla fiziksel veritabanı bağlantıları oluşturma, 
2. Merhaba Hello bağlantıyla kaydırma **DbContext** alt sınıfı
3. Merhaba bağlantı hello geçirmek **DbContext** temel sınıfları tooensure tüm hello işleme hello EF tarafında gerçekleşir de. 

Aşağıdaki kod örneğine hello bu yaklaşımı açıklar. (Bu da Visual Studio projesi eşlik hello kodudur)

    public class ElasticScaleContext<T> : DbContext
    {
    public DbSet<Blog> Blogs { get; set; }
    …

        // C'tor for data dependent routing. This call will open a validated connection 
        // routed toohello proper shard by hello shard map manager. 
        // Note that hello base class c'tor call will fail for an open connection
        // if migrations need toobe done and SQL credentials are used. This is hello reason for hello 
        // separation of c'tors into hello data-dependent routing case (this c'tor) and hello internal c'tor for new shards.
        public ElasticScaleContext(ShardMap shardMap, T shardingKey, string connectionStr)
            : base(CreateDDRConnection(shardMap, shardingKey, connectionStr), 
            true /* contextOwnsConnection */)
        {
        }

        // Only static methods are allowed in calls into base class c'tors.
        private static DbConnection CreateDDRConnection(
        ShardMap shardMap, 
        T shardingKey, 
        string connectionStr)
        {
            // No initialization
            Database.SetInitializer<ElasticScaleContext<T>>(null);

            // Ask shard map toobroker a validated connection for hello given key
            SqlConnection conn = shardMap.OpenConnectionForKey<T>
                                (shardingKey, connectionStr, ConnectionOptions.Validate);
            return conn;
        }    

## <a name="main-points"></a>Ana noktaları
* Yeni bir oluşturucu hello varsayılan oluşturucu hello DbContext alt sınıfta değiştirir 
* Merhaba yeni Oluşturucusu veri bağımlı esnek veritabanı istemci kitaplığı yönlendirme için gerekli olan hello bağımsız değişkenleri alır:
  
  * veri bağımlı yönlendirme arabirimlerini Hello parça eşleme tooaccess hello
  * Merhaba parçalama anahtar tooidentify hello shardlet
  * Merhaba veri bağımlı yönlendirme bağlantısı toohello parça hello kimlik bilgileri ile bir bağlantı dizesi. 
* Merhaba çağrısı toohello temel sınıf oluşturucu tüm hello adımları gerçekleştirir statik bir yönteme bir detour veri bağımlı yönlendirme için gerekli alır. 
  
  * Merhaba parça eşleme tooestablish açık bir bağlantı hello OpenConnectionForKey çağrısı hello esnek veritabanı istemci arabirimlerini kullanır.
  * Merhaba parça eşlemesi parçalama anahtarı verilen hello hello shardlet tutan hello açık bağlantı toohello parça oluşturur.
  * Bu açık bağlantı geri toohello temel sınıf bu bağlantının otomatik olarak yeni bir bağlantı oluşturmak EF yapmasına izin vermek yerine EF tarafından kullanılan toobe olduğunu DbContext tooindicate oluşturucusunun geçirilir. Böylece parça eşleme yönetim işlemleri altında tutarlılığı garanti edebilir bu şekilde hello bağlantı hello esnek veritabanı istemci API tarafından etiketlendiği.

Merhaba varsayılan oluşturucu, kodunuzda yerine, bir DbContext alt için Hello yeni Oluşturucu kullanın. Örnek aşağıda verilmiştir: 

    // Create and save a new blog.

    Console.Write("Enter a name for a new blog: "); 
    var name = Console.ReadLine(); 

    using (var db = new ElasticScaleContext<int>( 
                            sharding.ShardMap,  
                            tenantId1,  
                            connStrBldr.ConnectionString)) 
    { 
        var blog = new Blog { Name = name }; 
        db.Blogs.Add(blog); 
        db.SaveChanges(); 

        // Display all Blogs for tenant 1 
        var query = from b in db.Blogs 
                    orderby b.Name 
                    select b; 
     … 
    }

Merhaba yeni Oluşturucusu açar hello değeri tarafından tanımlanan hello shardlet hello verilerini tutan hello bağlantı toohello parça **tenantid1**. Merhaba hello kodda **kullanarak** blok kalır değişmeden tooaccess hello **DbSet** EF hello parça kullanarak Web günlükleri için **tenantid1**. Tüm veritabanı işlemleri sunulmuştur gibi blok kullanarak hello Hello kodda toohello bir parça kapsamlı için bu semantiğini değiştirir nerede **tenantid1** tutulur. Örneğin, bir LINQ sorgusu hello bloglar üzerinden **DbSet** yalnızca hello geçerli parça üzerinde depolanan bloglar dönün, ancak olanları diğer parça üzerinde depolanan hello değil.  

#### <a name="transient-faults-handling"></a>Geçici hataları işleme
Merhaba Microsoft Patterns & yöntemler yayımlanan hello ekip [hello geçici hata işleme uygulama blok](https://msdn.microsoft.com/library/dn440719.aspx). Merhaba kitaplığı esnek ölçek istemci kitaplığı EF ile birlikte kullanılır. Ancak, geçici bir özel durumla burada biz böylece biz tweaked hello oluşturucuları kullanarak herhangi bir yeni bağlantı denemesi yapıldıktan sonra geçici bir hata bu hello yeni oluşturucusunun kullanıldığından emin olabilirsiniz tooa yer döndürdüğünden emin olun. Aksi takdirde, parça garanti edilmez ve hello bağlantı hiçbir garanti vermediğini olan doğru bir bağlantı toohello toohello parça eşleme oluşacak değişiklikler korunur. 

Merhaba aşağıdaki kod örneği nasıl bir SQL yeniden deneme ilkesi hello yeni kullanılabileceğini gösterir **DbContext** alt sınıf oluşturucular: 

    SqlDatabaseUtils.SqlRetryPolicy.ExecuteAction(() => 
    { 
        using (var db = new ElasticScaleContext<int>( 
                                sharding.ShardMap,  
                                tenantId1,  
                                connStrBldr.ConnectionString)) 
            { 
                    var blog = new Blog { Name = name }; 
                    db.Blogs.Add(blog); 
                    db.SaveChanges(); 
            … 
            } 
        }); 

**SqlDatabaseUtils.SqlRetryPolicy** hello Yukarıdaki kod olarak tanımlanan bir **SqlDatabaseTransientErrorDetectionStrategy** bir yeniden deneme sayısı 10 ve 5 saniye ile yeniden denemeler arasındaki süre bekleyin. Bu yaklaşım EF ve kullanıcı tarafından başlatılan işlemleri için benzer toohello kılavuzunu olur (bkz [yeniden deneniyor yürütme stratejileri (veya sonraki sürümleri EF6) kısıtlamalarla](http://msdn.microsoft.com/data/dn307226). Her iki durumlarda bu hello uygulama programı denetimleri hello kapsam toowhich hello geçici özel durum döndürür gerektirir: tooeither hello işlem yeniden veya (gösterildiği gibi) kullanımları esnek veritabanı hello hello uygun Oluşturucusu hello bağlamından yeniden İstemci Kitaplığı.

Merhaba burada geçici özel durumlar ele bize geri kapsamda gerek toocontrol de hello yerleşik hello kullanımını önleyen **SqlAzureExecutionStrategy** EF ile birlikte gelir. **SqlAzureExecutionStrategy** bir bağlantıyı yeniden, ancak kullanmaz **OpenConnectionForKey** ve bu nedenle hello bir parçası olarak gerçekleştirilen tüm hello Doğrulamayı atla **OpenConnectionForKey** çağırın. Bunun yerine, hello yerleşik hello kod örneği kullanan **DefaultExecutionStrategy** EF ile de gelir. Çok aygıtlardır**SqlAzureExecutionStrategy**, doğru geçici hata işleme hello yeniden deneme ilkesi ile birlikte çalışır. Merhaba yürütme İlkesi hello ayarlanmış **ElasticScaleDbConfiguration** sınıfı. Biz değil toouse karar Not **DefaultSqlExecutionStrategy** toouse öneren beri **SqlAzureExecutionStrategy** geçici özel durumlar oluşursa - hangi neden toowrong davranışı açıklandığı gibi. Merhaba farklı yeniden deneme ilkelerini ve EF ile ilgili daha fazla bilgi için bkz: [EF bağlantı dayanıklılığı](http://msdn.microsoft.com/data/dn456835.aspx).     

#### <a name="constructor-rewrites"></a>Oluşturucu yeniden yazmalar
Merhaba Yukarıdaki kod örnekleri göstermeye hello varsayılan sipariş toouse veri hello Entity Framework ile yönlendirme bağımlı, uygulamanız için gerekli Oluşturucusu yeniden yazar. Aşağıdaki tablonun hello bu yaklaşım tooother oluşturucular genelleştirir. 

| Geçerli Oluşturucusu | Verileri yeniden Oluşturucusu | Temel Oluşturucusu | Notlar |
| --- | --- | --- | --- |
| MyContext() |ElasticScaleContext (ShardMap, TKey) |DbContext (DbConnection, bool) |Merhaba bağlantı toobe işlevi hello parça eşleme ve hello veri bağımlı yönlendirme anahtarı gerekiyor. Bunun yerine hello parça eşleme toobroker hello bağlantı kullanın ve EF tooby geçişi otomatik bağlantı oluşturması gerekir. |
| MyContext(string) |ElasticScaleContext (ShardMap, TKey) |DbContext (DbConnection, bool) |Merhaba bağlantı hello parça eşleme ve hello veri bağımlı yönlendirme anahtarı bir işlevdir. Sabit veritabanı adı veya bağlantı dizesi çalışmazlar hello parça eşleme tarafından atlama doğrulama. |
| MyContext(DbCompiledModel) |ElasticScaleContext (ShardMap, TKey, DbCompiledModel) |DbContext (DbConnection, DbCompiledModel, Boole) |Merhaba bağlantısı için sağlanan hello modeliyle parça eşleme ve parçalama anahtarı verilen hello oluşturulur. Merhaba derlenmiş model üzerinde temel c'tor toohello geçirilir. |
| MyContext (DbConnection, bool) |ElasticScaleContext (ShardMap, TKey, Boole) |DbContext (DbConnection, bool) |Merhaba bağlantı hello parça eşleme ve başlangıç anahtarı çıkarımı yapılan toobe gerekir. (Bu girişi zaten hello parça eşleme ve başlangıç anahtarı kullanmadığı sürece) bir giriş olarak sağlanamaz. Merhaba Boolean geçirilir. |
| MyContext (dize, DbCompiledModel) |ElasticScaleContext (ShardMap, TKey, DbCompiledModel) |DbContext (DbConnection, DbCompiledModel, Boole) |Merhaba bağlantı hello parça eşleme ve başlangıç anahtarı çıkarımı yapılan toobe gerekir. (Bu giriş hello parça eşleme ve başlangıç anahtarı kullanmadığı sürece) bir giriş olarak sağlanamaz. Merhaba derlenmiş modeli geçirilir. |
| MyContext (ObjectContext, bool) |ElasticScaleContext (ShardMap, TKey, ObjectContext, bool) |DbContext (ObjectContext, bool) |Merhaba yeni Oluşturucusu herhangi bir giriş olarak ObjectContext geçirilen hello bağlantısında esnek ölçek tarafından yönetilen yeniden yönlendirilmiş tooa bağlantıdır tooensure gerekir. ObjectContexts hakkında ayrıntılı bilgi hello bu belgenin kapsamında değildir. |
| MyContext (DbConnection, DbCompiledModel, Boole) |ElasticScaleContext (ShardMap, TKey, DbCompiledModel, bool) |DbContext (DbConnection, DbCompiledModel, bool); |Merhaba bağlantı hello parça eşleme ve başlangıç anahtarı çıkarımı yapılan toobe gerekir. (Bu girişi zaten hello parça eşleme ve başlangıç anahtarı kullanmadığı sürece) bir giriş olarak hello bağlantı sağlanamaz. Model ve Boolean toohello temel sınıf oluşturucu geçirilir. |

## <a name="shard-schema-deployment-through-ef-migrations"></a>EF geçişler aracılığıyla parça şema dağıtımı
Otomatik şema, hello Entity Framework tarafından sağlanan bir kolaylık yönetimidir. Veritabanlarını toohello parçalı uygulama eklendiğinde esnek veritabanı araçlarını kullanarak uygulamaları hello bağlamda tooretain Bu yetenek tooautomatically sağlama hello şema oluşturulan toonewly parça istiyoruz. Merhaba birincil kullanım hello veri katmanı tooincrease kapasitede EF kullanan parçalı uygulamalar için bir durumdur. Şema Yönetimi için EF'in özellikleri güvenmek EF üzerinde oluşturulmuş parçalı bir uygulama ile Merhaba veritabanı yönetim çaba azaltır. 

Şema dağıtımı EF geçişler aracılığıyla en iyi şekilde çalışır **açılmamış bağlantıları**. Buna karşılık hello esnek veritabanı istemci API'si tarafından sağlanan açılan hello bağlantı dayanan veri bağımlı yönlendirme için toohello senaryo budur. Başka bir fark hello tutarlılık gereksinimdir: tüm veri bağımlı yönlendirme bağlantıları tooprotect karşı eş zamanlı parça eşleme işleme sırasında tutarlılık arzu tooensure, bu ilk şema dağıtım tooa yeni veritabanı ile ilgili bir sorun değildir Merhaba parça eşlemesinde kayıtlı değil henüz ve toohold shardlets ayrılmamış henüz sahip. Biz, bu nedenle normal veritabanı bağlantısı karşılıklı yönlendirme toodata bağlı olarak bu senaryoları için güvenebilirsiniz.  

Bu, tooan yaklaşım nerede EF geçişler aracılığıyla şema dağıtımın sıkı şekilde hello yeni veritabanının hello kaydı hello uygulamanın parça eşlemesindeki bir parça olarak bağlı yol açar. Bu Önkoşullar aşağıdaki hello üzerinde dayanır: 

* Merhaba veritabanı zaten oluşturuldu. 
* Merhaba veritabanı boş - kullanıcı şeması yok ve hiçbir kullanıcı verileri tutar.
* Merhaba veritabanı henüz veri bağımlı yönlendirme için hello esnek veritabanı istemci API erişilemiyor. 

Bu önkoşulları yerine getirilince, bir normal oluşturabilir açılmamış **SqlConnection** tookick EF geçişler şema dağıtımı için devre dışı. Aşağıdaki kod örneği hello bu yaklaşım gösterilmektedir. 

        // Enter a new shard - i.e. an empty database - toohello shard map, allocate a first tenant tooit  
        // and kick off EF intialization of hello database toodeploy schema 

        public void RegisterNewShard(string server, string database, string connStr, int key) 
        { 

            Shard shard = this.ShardMap.CreateShard(new ShardLocation(server, database)); 

            SqlConnectionStringBuilder connStrBldr = new SqlConnectionStringBuilder(connStr); 
            connStrBldr.DataSource = server; 
            connStrBldr.InitialCatalog = database; 

            // Go into a DbContext tootrigger migrations and schema deployment for hello new shard. 
            // This requires an un-opened connection. 
            using (var db = new ElasticScaleContext<int>(connStrBldr.ConnectionString)) 
            { 
                // Run a query tooengage EF migrations 
                (from b in db.Blogs 
                    select b).Count(); 
            } 

            // Register hello mapping of hello tenant toohello shard in hello shard map. 
            // After this step, data-dependent routing on hello shard map can be used 

            this.ShardMap.CreatePointMapping(key, shard); 
        } 


Bu örnek hello yöntemi gösterilir **RegisterNewShard** yazmaçlar hello parça eşlemesindeki parça hello hello şema EF geçişler aracılığıyla dağıtır ve parçalama anahtar toohello parça eşlemesi depolar. Merhaba, bir oluşturucusuna dayanır **DbContext** alt (**ElasticScaleContext** hello örnekteki), bir SQL bağlantı dizesi giriş olarak alır. Bu oluşturucu Hello kodunu düz iletme örnekte gösterildiği aşağıdaki hello, şöyledir: 

        // C'tor toodeploy schema and migrations tooa new shard 
        protected internal ElasticScaleContext(string connectionString) 
            : base(SetInitializerForConnection(connectionString)) 
        { 
        } 

        // Only static methods are allowed in calls into base class c'tors 
        private static string SetInitializerForConnection(string connnectionString) 
        { 
            // We want existence checks so that hello schema can get deployed 
            Database.SetInitializer<ElasticScaleContext<T>>( 
        new CreateDatabaseIfNotExists<ElasticScaleContext<T>>()); 

            return connnectionString; 
        } 

Bir hello taban sınıfından devralınan hello Oluşturucusu hello sürümünü kullanmış olabilirsiniz. Ancak EF varsayılan Başlatıcısı hello hello Kod gereksinimlerini tooensure bağlanırken kullanılır. Bu nedenle hello statik yöntemiyle hello temel sınıf oluşturucu hello bağlantı dizesiyle içine çağırmadan önce kısa detour hello. Parça Hello kaydı EF hello Başlatıcı ayarlarını değil çakışan bir farklı uygulama etki alanı ya da işlem tooensure içinde çalışması gerektiğini unutmayın. 

## <a name="limitations"></a>Sınırlamalar
Bu belgede özetlenen hello yaklaşımlar birkaç sınırlama oluşturulmasını gerektirir: 

* Kullanan EF uygulamaları **LocalDb** ilk gereksinim toomigrate tooa normal SQL Server veritabanının esnek veritabanı istemci kitaplığı kullanmadan önce. Esnek ölçeklendirme ile parçalama aracılığıyla bir uygulama ölçeğini mümkün değil **LocalDb**. Geliştirme hala kullanabileceğinizi unutmayın **LocalDb**. 
* Veritabanı şema değişiklikleri kapsıyor herhangi bir değişiklik toohello uygulama tüm parça EF geçişleri üzerinden toogo gerekir. Bu belge için örnek kod Hello göstermek değil nasıl toodo bu. Update-Database tüm parça ConnectionString parametresi tooiterate ile kullanmayı düşünün; veya hello - komut dosyası seçeneği ve hello T-SQL komut dosyası tooyour parça uygulamak extract hello T-SQL komut dosyası için Update-Database kullanarak geçiş bekleyen hello.  
* Bir istek göz önüne alındığında, tüm veritabanı işleme içinde yer alır, tek bir parça içinde hello isteğiyle sağlanan hello parçalama anahtarı tarafından tanımlandığı gibi varsayılır. Ancak, bu varsayım her zaman true tutmaz. Örneğin, ne zaman olası toomake parçalama anahtarına sahip değil. tooaddress Bu, hello istemci kitaplığı sağlayan hello **MultiShardQuery** birkaç parça sorgulama için bir bağlantı Özet uygulayan sınıf. Toouse hello öğrenme **MultiShardQuery** EF ile birlikte hello bu belgenin kapsamında değildir.

## <a name="conclusion"></a>Sonuç
Bu belgede özetlenen hello adımlara EF uygulamaları hello esnek veritabanı istemci kitaplığının yetenek hello oluşturucular yeniden düzenleme yönlendirme bağımlı veri kullanabilirsiniz **DbContext** hello EF kullanılan alt sınıflar uygulama. Bu sınırları hello değişiklik gerekli toothose yerleştirir nerede **DbContext** sınıflar zaten mevcut. Ayrıca, EF uygulamaları hello gerekli EF geçirilmesi hello kayıt ile yeni parça ve eşlemelerini hello parça eşlemesindeki çağırma hello adımları birleştirerek otomatik şema dağıtımından toobenefit devam edebilir. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-use-entity-framework-applications-visual-studio/sample.png
