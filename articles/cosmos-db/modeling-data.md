---
title: "bir NoSQL veritabanı için aaaModeling belge verileri | Microsoft Docs"
description: "NoSQL veritabanları için veriler modelleme hakkında bilgi edinin"
keywords: Veri modelleme
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a>Belge verileri NoSQL veritabanları için modelleme
Azure Cosmos DB gibi şemasız veritabanı Süper kolaylaştırmak sırada tooembrace değişiklikleri tooyour veri modeli harcamanız bazı zaman verileriniz hakkında düşünmeye. 

Veri depolanan toobe nasıl geçiyor? Uygulama giderek tooretrieve ve sorgu verilerinizi nasıl mi? Uygulamanızı koyu okuma veya yazma ağır mi? 

Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olacaktır:

* Nasıl bir belge veritabanı belgede dikkat etmeniz?
* Veri modellemesi nedir ve neden ı dikkat etmelisiniz? 
* Nasıl modelleme verileri ilişkisel bir veritabanındaki belge veritabanı farklı tooa mi?
* Veri ilişkileri ilişkisel olmayan bir veritabanında nasıl express?
* Ne zaman ı verileri katıştır ve ne zaman toodata bağlamayın?

## <a name="embedding-data"></a>Veri katıştırma
Azure Cosmos DB gibi bir belge deposundaki verileri modelleme başlattığınızda tootreat varlıklarınızı olarak deneyin **kendi içinde bulunan belgeleri** JSON'da temsil.

Biz daha yakından inceleyin önce çok daha çok, bize birkaç adımı yeniden alın ve nasıl biz bize çoğunu bilginiz konu ilişkisel bir veritabanındaki bir şey model bir göz gerekir. Merhaba aşağıdaki örnek bir kişi ilişkisel bir veritabanına nasıl depolanabilir gösterir. 

![İlişkisel veritabanı modeli](./media/documentdb-modeling-data/relational-data-model.png)

Biz yıl toonormalize için öğrettin ilişkisel veritabanları ile çalışırken, normalleştirin, normalleştirin.

Verilerinizi genellikle normalleştirme bir kişi gibi bir varlık alma ve veri toodiscrete parçalarını çiğnemekten içerir. Hello yukarıdaki örnekte, bir kişi, birden çok kişi ayrıntı kaydı gibi birden çok adres kaydı olabilir. Biz bile bir adım daha fazla gidin ve başka çıkartarak kişi ayrıntılarını ortak bölün alanları ister bir türü. Aynı adresi için burada her kaydı gibi bir türe sahip *giriş* veya *iş* 

Şirket içi veri normalleştirme çok olduğunda yönlendirmede hello**yedek verileri depolamak kaçının** her kaydedin ve bunun yerine toodata bakın. Bu örnekte, tooread kendi ilgili kişi ayrıntıları ve adresleri olan bir kişi verilerinizi çalışma zamanı toouse BİRLEŞTİRMELER tooeffectively toplama gerekir.

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

Tek bir kişinin kendi ilgili kişi ayrıntıları ve adreslerinin güncelleştirme yazma işlemleri, birçok tek tek tablolar arasında gerektirir. 

Şimdi Al biz nasıl saptayacaktır bir göz hello artık aynı veri bir belge veritabanında kendi içinde bulunan bir varlık olarak.

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

Yukarıdaki şimdi sahibiz hello yaklaşımı kullanarak **Normalleştirilmemiş** hello kişi kaydı burada biz **katıştırılmış** tüm toothis kişinin, kendi ilgili kişi ayrıntıları ve adresleri tooa tek gibi ilgili bilgileri hello JSON belgesi.
Ayrıca, biz değil sınırlı çünkü tooa sahibiz şema farklı şekillerdeki kişi ayrıntılarını tamamen olması gibi hello esneklik toodo şeyler sabit. 

Tam kişi kaydı hello veritabanından alma işlemi tek bir koleksiyon ve tek bir belgenin okuma tek bir sunulmuştur. Bir kişi kaydı, iletişim ayrıntılarını ve adresleri güncelleştirmek tek bir belgenin karşı tek bir yazma işlemi de kullanılır.

Uygulamanızın veri denormalizing göre daha az sorgular ve güncelleştirmeleri toocomplete ortak işlemleri tooissue gerekebilir. 

### <a name="when-tooembed"></a>Zaman tooembed
Genel olarak, katıştırılmış veri kullanmak ne zaman modelleri:

* Vardır **içeren** varlıklar arasındaki ilişkiler.
* Vardır **bir birkaç** varlıklar arasındaki ilişkiler.
* Katıştırılmış veri, **değişmeyen**.
* Var. katıştırılmış veri olmaz büyümesine **bağlı olmadan**.
* Ekli veriler var. **tam sayı** belgede toodata.

> [!NOTE]
> Veri modelleri sağlayan daha iyi normal genellikle dışı **okuma** performans.
> 
> 

### <a name="when-not-tooembed"></a>Değil tooembed zaman
Merhaba altın kural bir belge veritabanında toodenormalize gereken her şey vardır ve tüm veri tooa tek belgede embed olsa da, bu kaçınılmalıdır toosome durumlarda neden olabilir.

Bu JSON parçacığı alın.

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

Bu, biz tipik bir blog veya CMS, sistem modelleme varsa gibi ne katıştırılmış açıklamaları post varlıkla görünür olabilir. Hello Bu örnek ile ilgili sorun olduğunu açıklamaları dizisi bu hello **sınırsız**, hiçbir (pratik) toohello sayısı sınırı tek bir post olabilir açıklamaları olduğu anlamına gelir. Merhaba belgenin Hello boyutu önemli ölçüde büyüdükçe bu bir sorun olacaktır.

Belge hello özelliği tootransmit hello veri okuma yanı sıra hello kablo hello Hello boyutu olarak büyür ve Ölçekle güncelleştirme hello belge etkilenir.

Bu durumda bu model aşağıdaki daha iyi tooconsider hello olacaktır.

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

Bu model kendisine ait bir sabit sınır sahip olan bir dizi bu sonrası üzerinde hello katıştırılmış hello üç en son açıklamaları olan zaman. Hello diğer açıklamalar 100 açıklamaları toobatches içinde gruplandırılır ve ayrı belgelerde depolanır. kurgusal uygulamamız hello kullanıcı tooload 100 yorumları aynı anda izin verdiğinden hello hello toplu iş boyutu 100 olarak seçildi.  

Merhaba katıştırılmış katıştırma veri iyi bir fikir olduğu başka bir veri belgeler arasında genellikle kullanılır ve sık sık değişiklik yapacağınız bir durumdur. 

Bu JSON parçacığı alın.

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

Bu kişinin stok Portföy temsil eder. Biz tooembed hello hisse bilgilerini tooeach Portföy belgede seçtiniz. İlgili verileri uygulama, ticari bir stok gibi sık, burada değişen bir ortamda sık sık değişen verileri katıştırma bir hisse senedi ticareti her zaman her Portföy belge sürekli güncelleştirdiğiniz toomean geçiyor.

Hisse senedi *zaza* tek bir kez yüzlerce ticareti gün ve binlerce kullanıcıyı sahip olabilir *zaza* kendi Portföy üzerinde. Yukarıdaki hello gibi bir veri modeli ile biz tooupdate binlerce Portföy belgeleri birçok kez çok iyi ölçeklendirme olmaz tooa sistem önde gelen her gün gerekir. 

## <a id="Refer"></a>Veri başvurma
Bu nedenle, veri katıştırma sorunsuz şekilde için çoğu zaman çalışır ancak verilerinizi denormalizing değerinde olandan daha fazla sorunlara neden olduğunda senaryoları olduğunu işaretlenmemiştir. Bu nedenle ne şimdi yapmak istersiniz? 

İlişkisel veritabanları varlıklar arasındaki ilişkiler oluşturabileceğiniz hello tek yer değildir. Bir belge veritabanında gerçekten başka belgelerde toodata ilişkili bir belgedeki bilgi olabilir. Şimdi, ı bile bir dakika boyunca size daha iyi uygun tooa ilişkisel veritabanı Azure Cosmos veritabanı veya başka bir belge veritabanında sistemler oluşturabilir, ancak basit ilişkileri ince ve çok kullanışlı olabilir advocating değil. 

Merhaba aşağıdaki JSON stok Portföy ancak biz toohello stok katıştırmak yerine hello Portföy öğede başvuran olarak daha önce bu kez toouse hello örneği seçtik. Bu şekilde hello stok öğesi sık güncelleştirilen toobe gereken hello gün hello yalnızca belge değiştiğinde hello tek stok belge olur. 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


Bir hemen dezavantajı toothis yine de uygulamanız bir kişinin Portföy görüntülenirken tutulan her hisse senedi hakkında gerekli tooshow bilgi olup olmadığını yaklaşımdır; Bu durumda toomake stok her belge için birden çok dönüşleri toohello veritabanı tooload hello bilgileri gerekir. Sık hello gün boyunca gerçekleşir, ancak bu belirli bir sistemi hello performansını büyük olasılıkla daha az etkisi olan işlemleri okuma hello üzerinde sırayla tehlikeye yazma işlemleri karar tooimprove hello verimliliğini burada yaptık.

> [!NOTE]
> Normalleştirilmiş veri modelleri **daha fazla gidiş dönüş gerektiren** toohello sunucu.
> 
> 

### <a name="what-about-foreign-keys"></a>Yabancı anahtarlar nasıldır?
Şu anda bir kısıtlama kavramına olduğundan, yabancı anahtar veya aksi takdirde belgelerde sahip herhangi bir arası belge ilişki etkili bir şekilde "zayıf bağlantılar" ve hello veritabanının tarafından doğrulanmaz. Bir belge başvuran veri hello tooensure isterseniz tooactually var. sonra toodo bu uygulamanızda veya sunucu tarafı Tetikleyicileri ya da Azure Cosmos DB saklı yordamları hello kullanımı aracılığıyla ihtiyacınız.

### <a name="when-tooreference"></a>Zaman tooreference
Genel olarak, normalleştirilmiş verileri kullanmak ne zaman modelleri:

* Temsil eden **bir çok** ilişkiler.
* Temsil eden **çok-** ilişkiler.
* İlgili verileri **sık sık değişen**.
* Başvurulan veri olabilir **sınırsız**.

> [!NOTE]
> Genellikle normalleştirme sağlar daha iyi **yazma** performans.
> 
> 

### <a name="where-do-i-put-hello-relationship"></a>Merhaba ilişkisi burada put?
Merhaba büyüme hello ilişkinin hangi belge toostore hello başvurusunda belirlemenize yardımcı olacaktır.

Biz Yayımcılar ve books modeller aşağıdaki JSON hello bakarsanız.

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

Yayımcı başına hello books Hello sayısı sınırlı büyümesiyle küçükse hello kitap başvuru hello yayımcı belgesinin içindeki depolama yararlı olabilir. Ancak, yayımcı başına books Hello sayısı sınırsız ise, bu veri modeli hello örnek publisher belgesi yukarıdaki olduğu gibi diziler büyüyen toomutable yol açar. 

Şeyler biraz geçici geçiş hala temsil aynı veri ancak şimdi hello bir modeldeki sonuç önler bu büyük değişebilir koleksiyonları.

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

Yukarıdaki örnek Hello biz yoksaymış hello yayımcı belgesinde sınırsız koleksiyonu hello. Bunun yerine yalnızca sahip olduğumuz bir başvuru toohello yayımcı her kitap belgesinde.

### <a name="how-do-i-model-manymany-relationships"></a>Çok: ilişkileri nasıl model?
İlişkisel bir veritabanındaki *çok:* ilişkileri genellikle yalnızca diğer tablolardan kayıtları birlikte katılma birleştirme tablolarla modellenir. 

![Tabloları birleştirme](./media/documentdb-modeling-data/join-table.png)

Belgeler ve benzer toohello şu görünen bir veri modeli üretmek kullanarak aynı şeyi isteği tooreplicate hello olabilir.

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

Bu çalışır. Ancak, bir ya da yazar kendi kitaplarıyla yüklenirken veya kitap yazarı ile yükleme her zaman en az iki ek hello veritabanı sorguları gerektirir. Bir sorgu toohello belge ve birleştirilen başka bir sorgu toofetch hello gerçek belge birleştirme. 

Tüm bu birleştirme tablo yaptığını yapıştırma, birlikte veri iki parça sonra neden tamamen kaldırın?
Merhaba aşağıdakileri göz önünde bulundurun.

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

Artık bir yaz güncelleştirmeniz varsa hemen yazılmış hangi books bilebilirim ve yüklenen bir kitap belge sahipse, buna karşılık hello yazarları hello kimliklerini bilebilirim. Bu Ara sorgulayan sunucu hello sayısının azaltılması hello birleşim tablosundan karşı kaydeder gidiş dönüş uygulamanızı toomake sahiptir. 

## <a id="WrapUp"></a>Karma veri modelleri
Biz şimdi inceledik katıştırma (veya denormalizing) ve başvuru (veya normalleştirme) veri her varsa bunların upsides ve her güvenlik ihlalleri anlatıldığı gibi. 

Bunu değil her zaman toobe ya da vardır veya yoktur biraz Korkmuş toomix şeyler yukarı olabilir. 

Uygulamanızın belirli kullanım desenlerini ve burada karıştırma katıştırılmış durumlar olabilir iş yükleri göre ve başvurulan veri mantıklı ve hala iyi düzeyde performans korurken dönüşleri sağlama toosimpler uygulama mantığını daha az sunucusuyla yuvarlamak .

JSON aşağıdaki hello göz önünde bulundurun. 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

Burada burada diğer varlıklar verilerden hello en üst düzey belgede gömülü, ancak diğer veri başvurulan hello katıştırılmış modeli, (çoğunlukla) izlenen. 

Merhaba kitap belge bakarsanız, birkaç görebiliriz biz yazarlar hello dizisi baktığınızda alanları ilginç. Var. bir *kimliği* kullanırız toorefer geri tooan Yazar belge, standart uygulamada normalleştirilmiş bir model, ancak daha sonra da hello alanı olan alanı *adı* ve *thumbnailUrl*. Biz yalnızca ile takılmış *kimliği* ve hello uygulama tooget gerekli ek bilgileri hello "bağlantı" kullanarak hello ilgili Yazar belgeden sol ancak uygulamamız hello yazar adı görüntülediğinden ve bir görüntülenen her defteri ile küçük resim biz kaydedebilir kitap gidiş dönüş toohello Sunucu'yu bir listede denormalizing tarafından **bazı** verileri hello yazar.

Emin hello yazar adı değiştirilmiş ya da kendi photo tooupdate istedikleri biz toogo bir güncelleştirme olurdu her kitap hiç yayımlanmadan ancak yazarlar adlarını sıklıkla, değişmeyen hello duymadığını uygulamamız için bu kabul edilebilir bir tasarım karar.  

Merhaba örnekte vardır **toplamalar'önceden hesaplanan** toosave üzerinde okuma işlem pahalı değerleri. Merhaba örnekte hello Yazar belgede gömülü hello verilerin bazıları olduğundan çalışma zamanında hesaplanan veri. Yeni bir rehberi yayımlanan her zaman bir kitap belge oluşturulur **ve** hello countOfBooks alanını için belirli bir yazarın mevcut Kitap belgelerini hello sayısına dayalı tooa hesaplanan değer ayarlayın. Bu iyileştirme biz sipariş toooptimize okuma yazma toodo hesaplamalar burada destekleyebilir okuma ağır sistemlerinde iyi olacaktır.

Azure Cosmos DB desteklediği için önceden hesaplanan alanları ile bir model olası yapıldığında özelliği toohave hello **Çoklu belge işlemler**. Birçok NoSQL depoları belgeler arasında işlemleri yapın ve bu nedenle "her zaman her şeyi, toothis sınırlaması katıştırmak" gibi tasarım kararları advocate. Azure Cosmos DB ile sunucu tarafı Tetikleyicileri ya da books ekleyebileceğiniz ve yazarlar ACID işlemi içinde tüm güncelleştirme saklı yordamları kullanabilirsiniz. Sizin artık **sahip** tooembed, her şeyi tooone belge yalnızca toobe verilerinizi tutarlı kalmasını.

## <a name="NextSteps"></a>Sonraki adımlar
Bu makaledeki Hello büyük paketler şemasız bir dünyada modelleme verileri olarak şimdiye kadar önemli olduğu toounderstand olur. 

Hiçbir tek bir yolu toorepresent ekranda verileri bir parçasını yalnızca yok olarak verilerinizi tek bir yolu toomodel yoktur. Toounderstand uygulamanız gerekir ve onu oluşturan nasıl kullanmak ve hello verileri işleme. Ardından, bazı hello uygulayarak Burada sunulan yönergeleri uygulamanızın hello hemen gereksinimlerine yönelik bir model oluşturma hakkında ayarlayabilirsiniz. Uygulamalarınızı toochange gerektiğinde, şemasız veritabanı tooembrace hello esnekliğini değiştirmek ve veri modelinizi kolayca gelişmesi yararlanabilirsiniz. 

Azure Cosmos DB hakkında daha fazla toolearn başvuran toohello hizmetin [belgelerine](https://azure.microsoft.com/documentation/services/cosmos-db/) sayfası. 

toounderstand nasıl tooshard verilerinizi birden çok bölüm arasında başvurmak çok[bölümleme veri Azure Cosmos veritabanı](documentdb-partition-data.md). 
