---
title: "Azure Cosmos DB tasarım deseni: sosyal medya uygulamalar | Microsoft Docs"
description: "Bir tasarım deseni hakkında hello depolama esnekliğini Azure Cosmos DB ve diğer Azure hizmetleriyle yararlanarak sosyal ağlar için öğrenin."
keywords: Sosyal medya uygulamalar
services: cosmos-db
author: ealsur
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 2dbf83a7-512a-4993-bf1b-ea7d72e095d9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: mimig
ms.openlocfilehash: 47a22f2c5762d62b176921c8052e7bd75d8cf6ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="going-social-with-azure-cosmos-db"></a>Azure Cosmos DB ile sosyal gitme
Yüksek düzeyde birbirine topluluğu içinde yaşayan anlamına gelir hayatta bir noktada, bir parçası haline gelir, bir **sosyal ağ**. Sosyal ağlar tookeep arkadaşlarınız, iş arkadaşlarınızı, Aile veya bazen tooshare iletişim bizim tutku ortak ilgi alanlarına sahip kişilerle kullanırız.

Mühendisleri veya geliştiriciler, biz nasıl bu ağlar depolamak ve verilerimizi birbirine hiç merak ettiniz, veya sahip bile edilmiş görevli toocreate veya belirli bir sayıda için yeni bir sosyal ağ Mimarı Pazar yourselves. Ne zaman olan hello büyük soruyu ortaya çıkar: nasıl tüm bu verileri depolanır?

Şimdi kullanıcılarımızın ilgili medya gibi resim, video ya da hatta müzik makalelerle burada nakledebilirsiniz yeni ve parlak sosyal ağ, oluşturuyoruz varsayalım. Kullanıcıların gönderilerine yorum ve derecelendirmeleri noktaları verin. Kullanıcıların görebileceği ve hello ana Web sitesi giriş sayfasında ile mümkün toointeract olması posta akışı olacaktır. Bu gerçekten karmaşık ses değil (başta), ancak Basitlik hello artırmak amacıyla için şimdi var. Durdur (biz ilişkileriyle etkilenen özel kullanıcı akışları içine inceleyin, ancak bu makalenin hello hedef aşıyor).

Bu nedenle, nasıl depolarız bu ve nerede?

Birçoğu deneyimi olan SQL veritabanlarına sahip olabilir veya en azından kavramı [ilişkisel veri modelleme](https://en.wikipedia.org/wiki/Relational_model) ve şöyle bir şey çizim isteği toostart olabilir:

![Göreli bir ilişkisel modeli gösteren diyagram](./media/social-media-apps/social-media-apps-sql.png) 

Mükemmel normalleştirilmiş ve asıl veri yapısı... ölçeklendirilmediğini. 

Me, my hayatta SQL veritabanları ile çalıştığınız, harika, ancak her düzeni, uygulama ve yazılım platformu gibi her senaryo için mükemmel değil yanlış olmaz.

Bu senaryoda SQL hello en iyi seçenek neden yok? Şimdi tek bir posta hello yapısına bakmak, bir Web sitesi veya Uygulama sonrası tooshow istediyseniz, t toodo içeren bir sorgu olurdu... 8 tablo birleşimler (!) yalnızca tooshow tek tek post, artık, resim dinamik olarak yükleme ve başlangıç ekranı ve, görünen gönderileri akışı yapacağım burada görebilirsiniz.

Elbette, bir bellek bilgisayar'ın SQL örneği yeterli güç toosolve binlerce sorguların çoğu bu birleştirmeler tooserve ile birlikte bizim içerik ancak gerçekten kullanırız olabilir, neden biz daha basit bir çözüm olduğunda var?

## <a name="hello-nosql-road"></a>Merhaba NoSQL yol
Bu makalede Azure'nın NoSQL veritabanı sosyal platformun verilerle modelleme içine yönlendirecek [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) hello gibi diğer Azure Cosmos DB özellikleri yararlanarak sırasında uygun maliyetli bir şekilde [Gremlin grafik API'si ](../cosmos-db/graph-introduction.md). Kullanarak bir [NoSQL](https://en.wikipedia.org/wiki/NoSQL) JSON biçiminde veri depolamak ve uygulama yaklaşımı [denormalization](https://en.wikipedia.org/wiki/Denormalization), daha önce karmaşık bizim post tek bir dönüştürülebilir [belge](https://en.wikipedia.org/wiki/Document-oriented_database):


    {
        "id":"ew12-res2-234e-544f",
        "title":"post title",
        "date":"2016-01-01",
        "body":"this is an awesome post stored on NoSQL",
        "createdBy":User,
        "images":["http://myfirstimage.png","http://mysecondimage.png"],
        "videos":[
            {"url":"http://myfirstvideo.mp4", "title":"hello first video"},
            {"url":"http://mysecondvideo.mp4", "title":"hello second video"}
        ],
        "audios":[
            {"url":"http://myfirstaudio.mp3", "title":"hello first audio"},
            {"url":"http://mysecondaudio.mp3", "title":"hello second audio"}
        ]
    }

Ve tek bir sorgu ile ve hiçbir birleştirmeleri edinilebilir. Bu çok daha basit ve kolay ve budget-wise, daha az kaynak tooachieve daha iyi sonuç gerektirir.

Azure Cosmos DB yapar tüm hello özellikleri kendi otomatik dizin oluşturma ile hatta olabilen dizinlenir olduğundan emin [özelleştirilmiş](indexing-policies.md). hiçbir ek özniteliklerle Hello yaklaşım bize belgeleri farklı depolamak sağlar ve kategorilere veya diyez etiketlerini, Cosmos DB ilişkili listesini işleyecek gönderileri toohave istiyoruz dinamik yapıları, belki de yarın yeni belgeler hello ile Merhaba şemasız eklendi İş tarafımızca gerekli.

Yalnızca diğer gönderileri (bizim nesne eşleme basitleştirir) üst özelliğe sahip olarak bir post açıklamaları işlenebilir. 

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":User2,
        "parent":"ew12-res2-234e-544f"
    }

    {
        "id":"asd2-fee4-23gc-jh67",
        "title":"Ditto!",
        "date":"2016-01-03",
        "createdBy":User3,
        "parent":"ew12-res2-234e-544f"
    }

Ve tüm sosyal etkileşimler sayaçları ayrı bir nesne üzerinde depolanabilir:

    {
        "id":"dfe3-thf5-232s-dse4",
        "post":"ew12-res2-234e-544f",
        "comments":2,
        "likes":10,
        "points":200
    }

Akışlar oluşturma verilen ilgi sırasıyla post kimlikleri listesini tutabilir belgeler oluşturma yalnızca bir konudur:

    [
        {"relevance":9, "post":"ew12-res2-234e-544f"},
        {"relevance":8, "post":"fer7-mnb6-fgh9-2344"},
        {"relevance":7, "post":"w34r-qeg6-ref6-8565"}
    ]

Biz "en son" akış oluşturma tarihine göre sıralanmış gönderileri sahip, daha fazla yöntemlerine hello içinde ile son 24 saat olanla "sıcak" bir akış gönderir, biz followers ve ilgi alanları gibi mantığı göre her bir kullanıcı için özel bir akış bile uygulamak ve hala listesini olacaktır  gönderir. Bunu nasıl toobuild listeler, bir konudur ancak hello okuma performans unhindered kalır. Biz bu listelerden birine elde sonra biz tek bir sorgu tooCosmos DB sorun hello kullanarak [İŞLECİNDE](documentdb-sql-query.md#WhereClause) birer birer gönderileri tooobtain sayfaları.

Akışlar akış hello kullanarak oluşturulur [Azure App Services](https://azure.microsoft.com/services/app-service/) arka plan işlemleri: [Webjobs](../app-service-web/web-sites-create-web-jobs.md). Bir post oluşturulduktan sonra arka plan işleme kullanarak tetiklenebilir [Azure Storage](https://azure.microsoft.com/services/storage/) [sıraları](../storage/queues/storage-dotnet-how-to-use-queues.md) ve hello kullanarak tetiklenen Webjobs [Azure Webjobs SDK](../app-service-web/websites-dotnet-webjobs-sdk.md), uygulama Merhaba, kendi özel mantığına göre akışları içinde yayma gönderin. 

Noktaları ve yöntemlerine bir post üzerinden aynı Bu teknik toocreate sonuçta tutarlı bir ortam kullanarak ertelenmiş bir şekilde işlenebilir.

Followers daha. Cosmos DB en fazla belge boyut sınırı vardır ve büyük belgeleri okuma/yazma uygulamanızı hello ölçeklenebilirliğini etkileyebilir. Bu nedenle bu yapısına sahip bir belge olarak followers depolama düşünebilirsiniz:

    {
        "id":"234d-sd23-rrf2-552d",
        "followersOf": "dse4-qwe2-ert4-aad2",
        "followers":[
            "ewr5-232d-tyrg-iuo2",
            "qejh-2345-sdf1-ytg5",
            //...
            "uie0-4tyg-3456-rwjh"
        ]
    }

Bu birkaç binlerce sahip bir kullanıcı için çalışabilir followers, ancak bazı ünlülerle bizim sıralar birleştirir bu yaklaşım tooa büyük belge boyutu götürür ve sonunda isabet hello belge boyutu cap.

toosolve bunu, karma bir yaklaşım kullanırız. Followers hello sayısı hello kullanıcı istatistikleri belge bir parçası olarak depolarız:

    {
        "id":"234d-sd23-rrf2-552d",
        "user": "dse4-qwe2-ert4-aad2",
        "followers":55230,
        "totalPosts":452,
        "totalPoints":11342
    }

Ve Azure Cosmos DB kullanarak followers gerçek grafiği hello depolanabilir [Gremlin grafik API'si](../cosmos-db/graph-introduction.md), toocreate [köşeleri](http://mathworld.wolfram.com/GraphVertex.html) her kullanıcı için ve [kenarları](http://mathworld.wolfram.com/GraphEdge.html) hello korumak " A-aşağıdaki-B"ilişkiler. Hello grafik API'si şimdi, yalnızca belirli bir kullanıcının hello followers elde ancak tooeven önermek kişiler ortak daha karmaşık sorgular oluşturabilirsiniz. Biz toohello grafik hello eklerseniz, içerik kategorileri kişilerin keyfini çıkarın veya gibi biz Akıllı İçerik bulma dahil deneyimleri weaving içerik öneren bu olanlar gibi biz izleyin veya takımı biz çok ortak olabilir kişi bulma başlatabilirsiniz.

Merhaba kullanıcı istatistikleri belge hala kullanılan toocreate kartları hello UI veya hızlı profili önizlemeleri olabilir.

## <a name="hello-ladder-pattern-and-data-duplication"></a>"Merdiveni" düzeni ve veri çoğaltma hello
Bir post başvuran hello JSON belgede fark etmiş olabileceğiniz gibi bir kullanıcı birden fazla oluşumu vardır. Ve, sağ, yani bu denormalization verilen bir kullanıcıyı temsil eden hello bilgi birden fazla yerde mevcut olabilir tahmin.

Daha hızlı sorgular için sipariş tooallow içinde veri çoğaltma doğurur. Bu yan etkiyi Hello sorun bazı eylem tarafından bir kullanıcının veri değişiklikleri, biz toofind gerekiyorsa tüm hello etkinlikleri kendisine herhangi bir zamanda vermedi ve Tümünü Güncelleştir olmasıdır. Ses çok pratik, doğru değil mi?

Devam eden toosolve biz uygulamamızı her etkinlik için gösterilecek bir kullanıcı anahtarı özniteliklerini tanımlayan tarafından hello duyuyoruz. Neden biz görsel olarak bir post bizim uygulamada Göster ve yalnızca hello Oluşturanın adı ve resim Göster, tümünü hello kullanıcının verileri hello "tarafından oluşturuldu" özniteliği depolamak? Her açıklamasını yalnızca hello kullanıcının resim gösteriyoruz, kendi bilgilerinin hello rest gerçekten gerekli değil. Burada bir şey hello "Merdiveni düzeni" çağrısı oyuna gelen olmasıdır.

Kullanıcı bilgilerini bir örnek olarak atalım:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "address":"742 Evergreen Terrace",
        "birthday":"1983-05-07",
        "email":"john@doe.com",
        "twitterHandle":"@john",
        "username":"johndoe",
        "password":"some_encrypted_phrase",
        "totalPoints":100,
        "totalPosts":24
    }

Bu bilgileri bakarak, biz kritik bilgilerin olduğu ve hangi "Merdiveni" böylece oluşturma değil hızlı bir şekilde tespit edebilirsiniz:

![Merdiveni düzeni diyagramı](./media/social-media-apps/social-media-apps-ladder.png)

Merhaba en küçük adım adlı UserChunk, hello en az bir kullanıcıyı tanımlar bilgi parçasını ve veri çoğaltma için kullanılır. Yinelenen hello veri tooonly hello bilgileri "göstereceğiz" Merhaba boyutunu azaltarak biz yoğun güncelleştirmeleri hello olasılığını azaltmak.

Merhaba Orta adım hello kullanıcı adında, Cosmos DB performans bağımlı sorguların çoğu üzerinde kullanılan hello tam veri hello en erişilen ve kritik. UserChunk tarafından temsil edilen hello bilgiler içerir.

en büyük Hello hello genişletilmiş kullanıcı olur. Kendi kullanımı (Merhaba oturum açma işlemi gibi) nihai veya tüm hello kritik kullanıcı bilgilerini artı gerçekten toobe okuma hızla gerektirmeyen diğer veri içerir. Bu veriler, Azure SQL Database veya Azure depolama tablolarında Cosmos DB dışında depolanabilir.

Neden biz hello kullanıcı bölme bile bu bilgileri ve farklı yerlerde depolamak? Bir performans açısından bakıldığında, hello büyük hello belgeleri hello çünkü costlier hello sorgular. Belgeleri hello ile ince bilgi toodo tüm, performans bağımlı sosyal ağınız için sorgular ve deposu hello diğer ek bilgileri gibi son senaryoları, tam profil düzenleme, oturum açma bilgileri doğru tutun, kullanım analizi ve büyük veri madenciliği bile Veri girişimleri. Azure SQL veritabanı üzerinde çalıştığından hello veri toplama için veri madenciliği yavaş ise, biz gerçekten umursamaz, biz sahip ilgilendiren ancak kullanıcılarımızın hızlı ve ince bir deneyim sahibi olduğunuzu. Cosmos DB üzerinde depolanan, bir kullanıcı şöyle olabilir:

    {
        "id":"dse4-qwe2-ert4-aad2",
        "name":"John",
        "surname":"Doe",
        "username":"johndoe"
        "email":"john@doe.com",
        "twitterHandle":"@john"
    }

Ve bir Post aşağıdaki gibidir:

    {
        "id":"1234-asd3-54ts-199a",
        "title":"Awesome post!",
        "date":"2016-01-02",
        "createdBy":{
            "id":"dse4-qwe2-ert4-aad2",
            "username":"johndoe"
        }
    }

Ve bir düzen hello öbek hello özniteliklerini birini burada etkilenir duyduğunuzda dizine toohello öznitelikleri noktası sorgularını kullanarak kolay toofind etkilenen hello belgeleri ise (seçin * FROM yazılarını p NEREYE p.createdBy.id "edited_user_id" ==) ve ardından güncelleştirme Merhaba öbekleri.

## <a name="hello-search-box"></a>Merhaba arama kutusu
Kullanıcılar, çok miktarda içerik oluşturur. Biz mümkün tooprovide hello özelliği toosearch olması ve hello oluşturucuları uygulayın yoktur çünkü doğrudan kendi içerik akış, belki de olmayabilir içeriği bulmak ve belki de numaralı yalnızca toofind 6 ay önce yaptığımız bu eski post çalışıyoruz.

Thankfully, ve Azure Cosmos DB de kullandığınızdan, biz kolayca bir arama motoru kullanarak uygulayabileceğiniz [Azure Search](https://azure.microsoft.com/services/search/) birkaç dakika ve tek satırlık bir kod yazmaya olmadan (tabii ki hello dışında arama işlemi ve kullanıcı Arabirimi).

Neden bu kadar kolay mi?

Azure arama uygulayan bunlar unsur [dizin oluşturucular](https://msdn.microsoft.com/library/azure/dn946891.aspx), arka plan, veri depoları içindeki bu kanca işler ve automagically ekleme, güncelleştirme veya nesnelerinizi hello dizinlerde kaldırma. Desteklenen bir [Azure SQL veritabanı dizin oluşturucular](https://blogs.msdn.microsoft.com/kaevans/2015/03/06/indexing-azure-sql-database-with-azure-search/), [Azure BLOB'ları dizin oluşturucular](../search/search-howto-indexing-azure-blob-storage.md) ve thankfully, [Azure Cosmos DB dizin oluşturucular](../search/search-howto-index-documentdb.md). Merhaba Cosmos DB tooAzure arama bilgilerinden geçişini, her iki depolama bilgileri JSON biçiminde olarak basittir, yalnızca çok ihtiyacımız[bizim dizin oluşturma](../search/search-create-index-portal.md) ve hangi özniteliklerin bizim belgelerden dizinli istiyoruz ve bunu eşleyin birkaç dakika içinde (Merhaba bizim veri boyutuna bağlıdır), bazı içeriklerin hello en iyi hizmet olarak arama çözümü bulut altyapısı tarafından bağlı aranır kullanılabilir toobe olacaktır. 

Azure Search hakkında daha fazla bilgi için hello ziyaret edebilirsiniz [Hitchhiker'ın Kılavuzu tooSearch](https://blogs.msdn.microsoft.com/mvpawardprogram/2016/02/02/a-hitchhikers-guide-to-search/).

## <a name="hello-underlying-knowledge"></a>Merhaba temel bilgi
Büyür ve her gün büyür tüm bu içeriği depolamak sonra biz kendisini düşünüyorum bulabilirsiniz: tüm bu bilgilerin olan akış my kullanıcılardan ne yapabilirim?

Merhaba yanıt basit: toowork yerleştirin ve ondan öğrenin.

Ancak, ne biz öğrenebilirsiniz? Birkaç kolay örnekler [düşünceleri analiz](https://en.wikipedia.org/wiki/Sentiment_analysis), önerilerine dayalı bir kullanıcının tercihlerini üzerinde veya tüm bizim sosyal ağ tarafından yayımlanan içerik hello sağlayan bile bir otomatik içerik denetleyici Merhaba güvenlidir içeriği ailesi.

Sayfaya var, büyük olasılıkla bu desenleri ve basit veritabanları ve dosyaları bilgilerini matematik Bilim tooextract içinde bazı Doktora gerekir, ancak yanlış olacaktır düşündüğünüz.

[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/), hello parçası [Cortana Intelligence Suite](https://www.microsoft.com/en/server-cloud/cortana-analytics-suite/overview.aspx), hello algoritmalar basit bir Sürükle ve bırak arabirimi kullanarak iş akışları oluşturmak, kendi algoritmaları kodu olanak sağlayan bir tam olarak yönetilen bir bulut hizmetidir içinde [R](https://en.wikipedia.org/wiki/R_\(programming_language\)) veya daha önce oluşturulan hello bazıları kullanın ve toouse API'leri gibi hazır: [metin analizi](https://gallery.cortanaanalytics.com/MachineLearningAPI/Text-Analytics-2), [içerik denetleyici](https://www.microsoft.com/moderator) veya [önerileri](https://gallery.cortanaanalytics.com/MachineLearningAPI/Recommendations-2).

tooachieve tüm bu Machine Learning senaryoları, kullandığımız [Azure Data Lake](https://azure.microsoft.com/services/data-lake-store/) tooingest hello farklı kaynaklardan bilgi ve kullanmak [U-SQL](https://azure.microsoft.com/documentation/videos/data-lake-u-sql-query-execution/) tooprocess hello bilgi ve bir çıktı oluşturmak Azure Machine Learning tarafından işlenebilir.

Başka bir kullanılabilir toouse seçenektir [Microsoft Bilişsel Hizmetler](https://www.microsoft.com/cognitive-services) tooanalyze kullanıcılarımızın içerik; yalnızca ki anlamak bunları daha iyi (ile bunların yazma çözümleme aracılığıyla [metin Analytics API](https://www.microsoft.com/cognitive-services/en-us/text-analytics-api)), ancak Biz ayrıca istenmeyen veya olgun içerikleri algılama ve buna göre hareket ile [bilgisayar görme API](https://www.microsoft.com/cognitive-services/en-us/computer-vision-api). Bilişsel hizmetler çok Machine Learning bilgi toouse her türlü gerektirmeyen Giden kutusu çözümleri içerir.

## <a name="a-planet-scale-social-experience"></a>Planet ölçekli sosyal deneyimi
Bir son yoktur, ancak önemli konu t, adres gerekir: **ölçeklenebilirlik**. Daha fazla veri tooprocess ihtiyacımız çünkü her bileşen, kendi, ya da genişletilebileceğini önemlidir bir mimari tasarlarken veya daha büyük bir coğrafi kapsamı (veya her ikisi de!) toohave istemiyor. Thankfully, karmaşık bir görev elde olan bir **anahtar teslimi deneyimi** Cosmos DB ile.

Cosmos DB destekleyen [dinamik bölümleme](https://azure.microsoft.com/blog/10-things-to-know-about-documentdb-partitioned-collections/) out-of--box bölümleri göre otomatik olarak oluşturarak bir verilen **bölüm anahtarı** (belgelerinizi hello öznitelikleri biri olarak tanımlanır). Merhaba bölüm anahtarı tasarım zamanında yapılmalıdır doğru tanımlama ve göz hello tutma [en iyi uygulamalar](../cosmos-db/partition-data.md#designing-for-partitioning) kullanılabilir; sosyal deneyimi hello durumda bölümleme stratejinizi (okuma sorgu hello işlemleriyle hizalanmalıdır. Merhaba içinde aynı bölüme arzu) ve yazma ("etkin nokta" birden çok bölüm üzerinde yazma yayarak kaçının). Bazı seçenekler şunlardır: kullanıcı tarafından; coğrafi bölgeye göre içerik kategoriye göre zamana bağlı bir anahtarı (gün/ay/hafta), temel bölümleri Tüm gerçekten nasıl hello verileri sorgulamak ve sosyal deneyiminizi göster bağımlı. 

Bir söz değerinde ilginç noktasıdır Cosmos DB sorgularınızı çalıştırın (de dahil olmak üzere [toplamalar](https://azure.microsoft.com/blog/planet-scale-aggregates-with-azure-documentdb/)) verilerinizi büyüdükçe, tüm bölümler saydam, tooadd herhangi bir mantık gerekmeyen.

Saat ile sonunda trafik ve kaynak tüketimini büyüyecektir (cinsinden [RUs](request-units.md), veya istek birimleri) artmasına neden olur. Okuma ve daha sık, userbase büyüdükçe ve oluşturma ve daha fazla içerik okuma başlayacak şekilde yazma; Merhaba yeteneklerini **, üretilen iş ölçeklendirme** önemlidir. Bizim RUs artırma çok kolay, biz hello Azure Portal veya tarafından birkaç tıklama ile yapabilirsiniz [hello API aracılığıyla komutlar veren](https://docs.microsoft.com/rest/api/documentdb/replace-an-offer).

![Yükseltme ve bölüm anahtarı tanımlama](./media/social-media-apps/social-media-apps-scaling.png)

Şeyleri daha iyi almaya devam ederseniz olanlar başka bir bölge, ülke veya kıtada, platformunuz dikkat edin ve kullanıcıları, bir harika aniden kullanmaya başlayın!

Ancak bekleyin... yakında deneyimlerini platformunuz ile en iyi; değil unutmayın şu ana kadar işletimsel bölgenizi çıktığınızda hello gecikme korkunç ve bunları açıkça tooquit istemiyorsanız oldukları. Oluştu, kolay bir yol yalnızca **genel elinizin genişletme**... yoktur ancak!

Cosmos DB olanak tanır [verilerinizi genel çoğaltmak](../cosmos-db/tutorial-global-distribution-documentdb.md) ve saydam bir birkaç tıklama ve otomatik olarak hello kullanılabilir bölgelerden arasından, [istemci kodu](../cosmos-db/tutorial-global-distribution-documentdb.md). Bu aynı zamanda, olabilir gelir [birden çok yük devretme bölgeleri](regional-failover.md). 

Verilerinizi genel çoğalttığınızda, istemcilerinizin bunu yararlanabilir emin toomake gerekir. Bir web ön uç veya belirtilmemelidir API'leri mobil istemcilerden kullanıyorsanız, dağıtabileceğiniz [Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager/) ve tüm istenen hello bölgeler, Azure App kullanarak hizmet kopyalama bir [performans Yapılandırması](../app-service-web/web-sites-traffic-manager.md)toosupport Genişletilmiş genel kapsama. İstemcilerinizi ön uç veya API'ler eriştiğinizde, yönlendirilmiş toohello olacaktır toohello yerel Cosmos DB çoğaltma sırayla bağlanacak en yakın uygulama hizmeti.

![Genel kapsam tooyour sosyal platform ekleme](./media/social-media-apps/social-media-apps-global-replicate.png)

## <a name="conclusion"></a>Sonuç
Bu makalede bazı sosyal ağlar düşük maliyetli Hizmetleri ile tamamen Azure üzerinde oluşturma ve mükemmel sonuçlar görünümü teşvik eder hello kullanarak "Merdiveni" adlı bir çok katmanlı depolama çözümü ve veri dağıtım sağlama hello alternatifleri içine açık tooshed çalışır.

![Sosyal ağ için Azure services arasındaki etkileşim diyagramı](./media/social-media-apps/social-media-apps-azure-solution.png)

Merhaba gerçekte Gümüş hiçbir madde işareti bu tür bir senaryo için sahip olduğu hello bize toobuild harika deneyimleri sağlayan harika Hizmetleri birleşimiyle oluşturulan synergy hello: Merhaba hızı ve Azure Cosmos DB tooprovide harika bir sosyal uygulaması özgürlüğünü ilk sınıf arama çözümü arkasında Hello Intelligence ister Azure Search, Azure App Services toohost hello esnekliğini dilden bağımsız uygulamalar güçlü arka plan işlemleri ancak bile ve Genişletilebilir Azure Storage ve Azure SQL veritabanı için hello Azure Machine Learning toocreate veri ve hello analitik gücünü oldukça büyük miktardaki depolama bilgi ve tooour işlemleri geri bildirim sağlamak ve bize yardımcı Intelligence sağ içerik toohello doğru kullanıcılar hello sunar.

## <a name="next-steps"></a>Sonraki adımlar
toolearn Cosmos DB kullanım durumları hakkında daha fazla bilgi görmek [ortak Cosmos DB kullanım](use-cases.md).
