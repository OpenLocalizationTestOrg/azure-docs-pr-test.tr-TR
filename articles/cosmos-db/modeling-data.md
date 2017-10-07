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
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="41949-104">Belge verileri NoSQL veritabanları için modelleme</span><span class="sxs-lookup"><span data-stu-id="41949-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="41949-105">Azure Cosmos DB gibi şemasız veritabanı Süper kolaylaştırmak sırada tooembrace değişiklikleri tooyour veri modeli harcamanız bazı zaman verileriniz hakkında düşünmeye.</span><span class="sxs-lookup"><span data-stu-id="41949-105">While schema-free databases, like Azure Cosmos DB, make it super easy tooembrace changes tooyour data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="41949-106">Veri depolanan toobe nasıl geçiyor?</span><span class="sxs-lookup"><span data-stu-id="41949-106">How is data going toobe stored?</span></span> <span data-ttu-id="41949-107">Uygulama giderek tooretrieve ve sorgu verilerinizi nasıl mi?</span><span class="sxs-lookup"><span data-stu-id="41949-107">How is your application going tooretrieve and query data?</span></span> <span data-ttu-id="41949-108">Uygulamanızı koyu okuma veya yazma ağır mi?</span><span class="sxs-lookup"><span data-stu-id="41949-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="41949-109">Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="41949-109">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="41949-110">Nasıl bir belge veritabanı belgede dikkat etmeniz?</span><span class="sxs-lookup"><span data-stu-id="41949-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="41949-111">Veri modellemesi nedir ve neden ı dikkat etmelisiniz?</span><span class="sxs-lookup"><span data-stu-id="41949-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="41949-112">Nasıl modelleme verileri ilişkisel bir veritabanındaki belge veritabanı farklı tooa mi?</span><span class="sxs-lookup"><span data-stu-id="41949-112">How is modeling data in a document database different tooa relational database?</span></span>
* <span data-ttu-id="41949-113">Veri ilişkileri ilişkisel olmayan bir veritabanında nasıl express?</span><span class="sxs-lookup"><span data-stu-id="41949-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="41949-114">Ne zaman ı verileri katıştır ve ne zaman toodata bağlamayın?</span><span class="sxs-lookup"><span data-stu-id="41949-114">When do I embed data and when do I link toodata?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="41949-115">Veri katıştırma</span><span class="sxs-lookup"><span data-stu-id="41949-115">Embedding data</span></span>
<span data-ttu-id="41949-116">Azure Cosmos DB gibi bir belge deposundaki verileri modelleme başlattığınızda tootreat varlıklarınızı olarak deneyin **kendi içinde bulunan belgeleri** JSON'da temsil.</span><span class="sxs-lookup"><span data-stu-id="41949-116">When you start modeling data in a document store, such as Azure Cosmos DB, try tootreat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="41949-117">Biz daha yakından inceleyin önce çok daha çok, bize birkaç adımı yeniden alın ve nasıl biz bize çoğunu bilginiz konu ilişkisel bir veritabanındaki bir şey model bir göz gerekir.</span><span class="sxs-lookup"><span data-stu-id="41949-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="41949-118">Merhaba aşağıdaki örnek bir kişi ilişkisel bir veritabanına nasıl depolanabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="41949-118">hello following example shows how a person might be stored in a relational database.</span></span> 

![İlişkisel veritabanı modeli](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="41949-120">Biz yıl toonormalize için öğrettin ilişkisel veritabanları ile çalışırken, normalleştirin, normalleştirin.</span><span class="sxs-lookup"><span data-stu-id="41949-120">When working with relational databases, we've been taught for years toonormalize, normalize, normalize.</span></span>

<span data-ttu-id="41949-121">Verilerinizi genellikle normalleştirme bir kişi gibi bir varlık alma ve veri toodiscrete parçalarını çiğnemekten içerir.</span><span class="sxs-lookup"><span data-stu-id="41949-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in toodiscrete pieces of data.</span></span> <span data-ttu-id="41949-122">Hello yukarıdaki örnekte, bir kişi, birden çok kişi ayrıntı kaydı gibi birden çok adres kaydı olabilir.</span><span class="sxs-lookup"><span data-stu-id="41949-122">In hello example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="41949-123">Biz bile bir adım daha fazla gidin ve başka çıkartarak kişi ayrıntılarını ortak bölün alanları ister bir türü.</span><span class="sxs-lookup"><span data-stu-id="41949-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="41949-124">Aynı adresi için burada her kaydı gibi bir türe sahip *giriş* veya *iş*</span><span class="sxs-lookup"><span data-stu-id="41949-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="41949-125">Şirket içi veri normalleştirme çok olduğunda yönlendirmede hello**yedek verileri depolamak kaçının** her kaydedin ve bunun yerine toodata bakın.</span><span class="sxs-lookup"><span data-stu-id="41949-125">hello guiding premise when normalizing data is too**avoid storing redundant data** on each record and rather refer toodata.</span></span> <span data-ttu-id="41949-126">Bu örnekte, tooread kendi ilgili kişi ayrıntıları ve adresleri olan bir kişi verilerinizi çalışma zamanı toouse BİRLEŞTİRMELER tooeffectively toplama gerekir.</span><span class="sxs-lookup"><span data-stu-id="41949-126">In this example, tooread a person, with all their contact details and addresses, you need toouse JOINS tooeffectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="41949-127">Tek bir kişinin kendi ilgili kişi ayrıntıları ve adreslerinin güncelleştirme yazma işlemleri, birçok tek tek tablolar arasında gerektirir.</span><span class="sxs-lookup"><span data-stu-id="41949-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="41949-128">Şimdi Al biz nasıl saptayacaktır bir göz hello artık aynı veri bir belge veritabanında kendi içinde bulunan bir varlık olarak.</span><span class="sxs-lookup"><span data-stu-id="41949-128">Now let's take a look at how we would model hello same data as a self-contained entity in a document database.</span></span>

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

<span data-ttu-id="41949-129">Yukarıdaki şimdi sahibiz hello yaklaşımı kullanarak **Normalleştirilmemiş** hello kişi kaydı burada biz **katıştırılmış** tüm toothis kişinin, kendi ilgili kişi ayrıntıları ve adresleri tooa tek gibi ilgili bilgileri hello JSON belgesi.</span><span class="sxs-lookup"><span data-stu-id="41949-129">Using hello approach above we have now **denormalized** hello person record where we **embedded** all hello information relating toothis person, such as their contact details and addresses, in tooa single JSON document.</span></span>
<span data-ttu-id="41949-130">Ayrıca, biz değil sınırlı çünkü tooa sahibiz şema farklı şekillerdeki kişi ayrıntılarını tamamen olması gibi hello esneklik toodo şeyler sabit.</span><span class="sxs-lookup"><span data-stu-id="41949-130">In addition, because we're not confined tooa fixed schema we have hello flexibility toodo things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="41949-131">Tam kişi kaydı hello veritabanından alma işlemi tek bir koleksiyon ve tek bir belgenin okuma tek bir sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="41949-131">Retrieving a complete person record from hello database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="41949-132">Bir kişi kaydı, iletişim ayrıntılarını ve adresleri güncelleştirmek tek bir belgenin karşı tek bir yazma işlemi de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="41949-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="41949-133">Uygulamanızın veri denormalizing göre daha az sorgular ve güncelleştirmeleri toocomplete ortak işlemleri tooissue gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="41949-133">By denormalizing data, your application may need tooissue fewer queries and updates toocomplete common operations.</span></span> 

### <a name="when-tooembed"></a><span data-ttu-id="41949-134">Zaman tooembed</span><span class="sxs-lookup"><span data-stu-id="41949-134">When tooembed</span></span>
<span data-ttu-id="41949-135">Genel olarak, katıştırılmış veri kullanmak ne zaman modelleri:</span><span class="sxs-lookup"><span data-stu-id="41949-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="41949-136">Vardır **içeren** varlıklar arasındaki ilişkiler.</span><span class="sxs-lookup"><span data-stu-id="41949-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="41949-137">Vardır **bir birkaç** varlıklar arasındaki ilişkiler.</span><span class="sxs-lookup"><span data-stu-id="41949-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="41949-138">Katıştırılmış veri, **değişmeyen**.</span><span class="sxs-lookup"><span data-stu-id="41949-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="41949-139">Var. katıştırılmış veri olmaz büyümesine **bağlı olmadan**.</span><span class="sxs-lookup"><span data-stu-id="41949-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="41949-140">Ekli veriler var. **tam sayı** belgede toodata.</span><span class="sxs-lookup"><span data-stu-id="41949-140">There is embedded data that is **integral** toodata in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="41949-141">Veri modelleri sağlayan daha iyi normal genellikle dışı **okuma** performans.</span><span class="sxs-lookup"><span data-stu-id="41949-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-tooembed"></a><span data-ttu-id="41949-142">Değil tooembed zaman</span><span class="sxs-lookup"><span data-stu-id="41949-142">When not tooembed</span></span>
<span data-ttu-id="41949-143">Merhaba altın kural bir belge veritabanında toodenormalize gereken her şey vardır ve tüm veri tooa tek belgede embed olsa da, bu kaçınılmalıdır toosome durumlarda neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="41949-143">While hello rule of thumb in a document database is toodenormalize everything and embed all data in tooa single document, this can lead toosome situations that should be avoided.</span></span>

<span data-ttu-id="41949-144">Bu JSON parçacığı alın.</span><span class="sxs-lookup"><span data-stu-id="41949-144">Take this JSON snippet.</span></span>

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

<span data-ttu-id="41949-145">Bu, biz tipik bir blog veya CMS, sistem modelleme varsa gibi ne katıştırılmış açıklamaları post varlıkla görünür olabilir.</span><span class="sxs-lookup"><span data-stu-id="41949-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="41949-146">Hello Bu örnek ile ilgili sorun olduğunu açıklamaları dizisi bu hello **sınırsız**, hiçbir (pratik) toohello sayısı sınırı tek bir post olabilir açıklamaları olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="41949-146">hello problem with this example is that hello comments array is **unbounded**, meaning that there is no (practical) limit toohello number of comments any single post can have.</span></span> <span data-ttu-id="41949-147">Merhaba belgenin Hello boyutu önemli ölçüde büyüdükçe bu bir sorun olacaktır.</span><span class="sxs-lookup"><span data-stu-id="41949-147">This will become a problem as hello size of hello document could grow significantly.</span></span>

<span data-ttu-id="41949-148">Belge hello özelliği tootransmit hello veri okuma yanı sıra hello kablo hello Hello boyutu olarak büyür ve Ölçekle güncelleştirme hello belge etkilenir.</span><span class="sxs-lookup"><span data-stu-id="41949-148">As hello size of hello document grows hello ability tootransmit hello data over hello wire as well as reading and updating hello document, at scale, will be impacted.</span></span>

<span data-ttu-id="41949-149">Bu durumda bu model aşağıdaki daha iyi tooconsider hello olacaktır.</span><span class="sxs-lookup"><span data-stu-id="41949-149">In this case it would be better tooconsider hello following model.</span></span>

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

<span data-ttu-id="41949-150">Bu model kendisine ait bir sabit sınır sahip olan bir dizi bu sonrası üzerinde hello katıştırılmış hello üç en son açıklamaları olan zaman.</span><span class="sxs-lookup"><span data-stu-id="41949-150">This model has hello three most recent comments embedded on hello post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="41949-151">Hello diğer açıklamalar 100 açıklamaları toobatches içinde gruplandırılır ve ayrı belgelerde depolanır.</span><span class="sxs-lookup"><span data-stu-id="41949-151">hello other comments are grouped in toobatches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="41949-152">kurgusal uygulamamız hello kullanıcı tooload 100 yorumları aynı anda izin verdiğinden hello hello toplu iş boyutu 100 olarak seçildi.</span><span class="sxs-lookup"><span data-stu-id="41949-152">hello size of hello batch was chosen as 100 because our fictitious application allows hello user tooload 100 comments at a time.</span></span>  

<span data-ttu-id="41949-153">Merhaba katıştırılmış katıştırma veri iyi bir fikir olduğu başka bir veri belgeler arasında genellikle kullanılır ve sık sık değişiklik yapacağınız bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="41949-153">Another case where embedding data is not a good idea is when hello embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="41949-154">Bu JSON parçacığı alın.</span><span class="sxs-lookup"><span data-stu-id="41949-154">Take this JSON snippet.</span></span>

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

<span data-ttu-id="41949-155">Bu kişinin stok Portföy temsil eder.</span><span class="sxs-lookup"><span data-stu-id="41949-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="41949-156">Biz tooembed hello hisse bilgilerini tooeach Portföy belgede seçtiniz.</span><span class="sxs-lookup"><span data-stu-id="41949-156">We have chosen tooembed hello stock information in tooeach portfolio document.</span></span> <span data-ttu-id="41949-157">İlgili verileri uygulama, ticari bir stok gibi sık, burada değişen bir ortamda sık sık değişen verileri katıştırma bir hisse senedi ticareti her zaman her Portföy belge sürekli güncelleştirdiğiniz toomean geçiyor.</span><span class="sxs-lookup"><span data-stu-id="41949-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going toomean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="41949-158">Hisse senedi *zaza* tek bir kez yüzlerce ticareti gün ve binlerce kullanıcıyı sahip olabilir *zaza* kendi Portföy üzerinde.</span><span class="sxs-lookup"><span data-stu-id="41949-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="41949-159">Yukarıdaki hello gibi bir veri modeli ile biz tooupdate binlerce Portföy belgeleri birçok kez çok iyi ölçeklendirme olmaz tooa sistem önde gelen her gün gerekir.</span><span class="sxs-lookup"><span data-stu-id="41949-159">With a data model like hello above we would have tooupdate many thousands of portfolio documents many times every day leading tooa system that won't scale very well.</span></span> 

## <span data-ttu-id="41949-160"><a id="Refer"></a>Veri başvurma</span><span class="sxs-lookup"><span data-stu-id="41949-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="41949-161">Bu nedenle, veri katıştırma sorunsuz şekilde için çoğu zaman çalışır ancak verilerinizi denormalizing değerinde olandan daha fazla sorunlara neden olduğunda senaryoları olduğunu işaretlenmemiştir.</span><span class="sxs-lookup"><span data-stu-id="41949-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="41949-162">Bu nedenle ne şimdi yapmak istersiniz?</span><span class="sxs-lookup"><span data-stu-id="41949-162">So what do we do now?</span></span> 

<span data-ttu-id="41949-163">İlişkisel veritabanları varlıklar arasındaki ilişkiler oluşturabileceğiniz hello tek yer değildir.</span><span class="sxs-lookup"><span data-stu-id="41949-163">Relational databases are not hello only place where you can create relationships between entities.</span></span> <span data-ttu-id="41949-164">Bir belge veritabanında gerçekten başka belgelerde toodata ilişkili bir belgedeki bilgi olabilir.</span><span class="sxs-lookup"><span data-stu-id="41949-164">In a document database you can have information in one document that actually relates toodata in other documents.</span></span> <span data-ttu-id="41949-165">Şimdi, ı bile bir dakika boyunca size daha iyi uygun tooa ilişkisel veritabanı Azure Cosmos veritabanı veya başka bir belge veritabanında sistemler oluşturabilir, ancak basit ilişkileri ince ve çok kullanışlı olabilir advocating değil.</span><span class="sxs-lookup"><span data-stu-id="41949-165">Now, I am not advocating for even one minute that we build systems that would be better suited tooa relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="41949-166">Merhaba aşağıdaki JSON stok Portföy ancak biz toohello stok katıştırmak yerine hello Portföy öğede başvuran olarak daha önce bu kez toouse hello örneği seçtik.</span><span class="sxs-lookup"><span data-stu-id="41949-166">In hello JSON below we chose toouse hello example of a stock portfolio from earlier but this time we refer toohello stock item on hello portfolio instead of embedding it.</span></span> <span data-ttu-id="41949-167">Bu şekilde hello stok öğesi sık güncelleştirilen toobe gereken hello gün hello yalnızca belge değiştiğinde hello tek stok belge olur.</span><span class="sxs-lookup"><span data-stu-id="41949-167">This way, when hello stock item changes frequently throughout hello day hello only document that needs toobe updated is hello single stock document.</span></span> 

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


<span data-ttu-id="41949-168">Bir hemen dezavantajı toothis yine de uygulamanız bir kişinin Portföy görüntülenirken tutulan her hisse senedi hakkında gerekli tooshow bilgi olup olmadığını yaklaşımdır; Bu durumda toomake stok her belge için birden çok dönüşleri toohello veritabanı tooload hello bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="41949-168">An immediate downside toothis approach though is if your application is required tooshow information about each stock that is held when displaying a person's portfolio; in this case you would need toomake multiple trips toohello database tooload hello information for each stock document.</span></span> <span data-ttu-id="41949-169">Sık hello gün boyunca gerçekleşir, ancak bu belirli bir sistemi hello performansını büyük olasılıkla daha az etkisi olan işlemleri okuma hello üzerinde sırayla tehlikeye yazma işlemleri karar tooimprove hello verimliliğini burada yaptık.</span><span class="sxs-lookup"><span data-stu-id="41949-169">Here we've made a decision tooimprove hello efficiency of write operations, which happen frequently throughout hello day, but in turn compromised on hello read operations that potentially have less impact on hello performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="41949-170">Normalleştirilmiş veri modelleri **daha fazla gidiş dönüş gerektiren** toohello sunucu.</span><span class="sxs-lookup"><span data-stu-id="41949-170">Normalized data models **can require more round trips** toohello server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="41949-171">Yabancı anahtarlar nasıldır?</span><span class="sxs-lookup"><span data-stu-id="41949-171">What about foreign keys?</span></span>
<span data-ttu-id="41949-172">Şu anda bir kısıtlama kavramına olduğundan, yabancı anahtar veya aksi takdirde belgelerde sahip herhangi bir arası belge ilişki etkili bir şekilde "zayıf bağlantılar" ve hello veritabanının tarafından doğrulanmaz.</span><span class="sxs-lookup"><span data-stu-id="41949-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by hello database itself.</span></span> <span data-ttu-id="41949-173">Bir belge başvuran veri hello tooensure isterseniz tooactually var. sonra toodo bu uygulamanızda veya sunucu tarafı Tetikleyicileri ya da Azure Cosmos DB saklı yordamları hello kullanımı aracılığıyla ihtiyacınız.</span><span class="sxs-lookup"><span data-stu-id="41949-173">If you want tooensure that hello data a document is referring tooactually exists, then you need toodo this in your application, or through hello use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-tooreference"></a><span data-ttu-id="41949-174">Zaman tooreference</span><span class="sxs-lookup"><span data-stu-id="41949-174">When tooreference</span></span>
<span data-ttu-id="41949-175">Genel olarak, normalleştirilmiş verileri kullanmak ne zaman modelleri:</span><span class="sxs-lookup"><span data-stu-id="41949-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="41949-176">Temsil eden **bir çok** ilişkiler.</span><span class="sxs-lookup"><span data-stu-id="41949-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="41949-177">Temsil eden **çok-** ilişkiler.</span><span class="sxs-lookup"><span data-stu-id="41949-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="41949-178">İlgili verileri **sık sık değişen**.</span><span class="sxs-lookup"><span data-stu-id="41949-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="41949-179">Başvurulan veri olabilir **sınırsız**.</span><span class="sxs-lookup"><span data-stu-id="41949-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="41949-180">Genellikle normalleştirme sağlar daha iyi **yazma** performans.</span><span class="sxs-lookup"><span data-stu-id="41949-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-hello-relationship"></a><span data-ttu-id="41949-181">Merhaba ilişkisi burada put?</span><span class="sxs-lookup"><span data-stu-id="41949-181">Where do I put hello relationship?</span></span>
<span data-ttu-id="41949-182">Merhaba büyüme hello ilişkinin hangi belge toostore hello başvurusunda belirlemenize yardımcı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="41949-182">hello growth of hello relationship will help determine in which document toostore hello reference.</span></span>

<span data-ttu-id="41949-183">Biz Yayımcılar ve books modeller aşağıdaki JSON hello bakarsanız.</span><span class="sxs-lookup"><span data-stu-id="41949-183">If we look at hello JSON below that models publishers and books.</span></span>

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

<span data-ttu-id="41949-184">Yayımcı başına hello books Hello sayısı sınırlı büyümesiyle küçükse hello kitap başvuru hello yayımcı belgesinin içindeki depolama yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="41949-184">If hello number of hello books per publisher is small with limited growth, then storing hello book reference inside hello publisher document may be useful.</span></span> <span data-ttu-id="41949-185">Ancak, yayımcı başına books Hello sayısı sınırsız ise, bu veri modeli hello örnek publisher belgesi yukarıdaki olduğu gibi diziler büyüyen toomutable yol açar.</span><span class="sxs-lookup"><span data-stu-id="41949-185">However, if hello number of books per publisher is unbounded, then this data model would lead toomutable, growing arrays, as in hello example publisher document above.</span></span> 

<span data-ttu-id="41949-186">Şeyler biraz geçici geçiş hala temsil aynı veri ancak şimdi hello bir modeldeki sonuç önler bu büyük değişebilir koleksiyonları.</span><span class="sxs-lookup"><span data-stu-id="41949-186">Switching things around a bit would result in a model that still represents hello same data but now avoids these large mutable collections.</span></span>

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

<span data-ttu-id="41949-187">Yukarıdaki örnek Hello biz yoksaymış hello yayımcı belgesinde sınırsız koleksiyonu hello.</span><span class="sxs-lookup"><span data-stu-id="41949-187">In hello above example, we have dropped hello unbounded collection on hello publisher document.</span></span> <span data-ttu-id="41949-188">Bunun yerine yalnızca sahip olduğumuz bir başvuru toohello yayımcı her kitap belgesinde.</span><span class="sxs-lookup"><span data-stu-id="41949-188">Instead we just have a a reference toohello publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="41949-189">Çok: ilişkileri nasıl model?</span><span class="sxs-lookup"><span data-stu-id="41949-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="41949-190">İlişkisel bir veritabanındaki *çok:* ilişkileri genellikle yalnızca diğer tablolardan kayıtları birlikte katılma birleştirme tablolarla modellenir.</span><span class="sxs-lookup"><span data-stu-id="41949-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Tabloları birleştirme](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="41949-192">Belgeler ve benzer toohello şu görünen bir veri modeli üretmek kullanarak aynı şeyi isteği tooreplicate hello olabilir.</span><span class="sxs-lookup"><span data-stu-id="41949-192">You might be tempted tooreplicate hello same thing using documents and produce a data model that looks similar toohello following.</span></span>

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

<span data-ttu-id="41949-193">Bu çalışır.</span><span class="sxs-lookup"><span data-stu-id="41949-193">This would work.</span></span> <span data-ttu-id="41949-194">Ancak, bir ya da yazar kendi kitaplarıyla yüklenirken veya kitap yazarı ile yükleme her zaman en az iki ek hello veritabanı sorguları gerektirir.</span><span class="sxs-lookup"><span data-stu-id="41949-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against hello database.</span></span> <span data-ttu-id="41949-195">Bir sorgu toohello belge ve birleştirilen başka bir sorgu toofetch hello gerçek belge birleştirme.</span><span class="sxs-lookup"><span data-stu-id="41949-195">One query toohello joining document and then another query toofetch hello actual document being joined.</span></span> 

<span data-ttu-id="41949-196">Tüm bu birleştirme tablo yaptığını yapıştırma, birlikte veri iki parça sonra neden tamamen kaldırın?</span><span class="sxs-lookup"><span data-stu-id="41949-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="41949-197">Merhaba aşağıdakileri göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="41949-197">Consider hello following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="41949-198">Artık bir yaz güncelleştirmeniz varsa hemen yazılmış hangi books bilebilirim ve yüklenen bir kitap belge sahipse, buna karşılık hello yazarları hello kimliklerini bilebilirim.</span><span class="sxs-lookup"><span data-stu-id="41949-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know hello ids of hello author(s).</span></span> <span data-ttu-id="41949-199">Bu Ara sorgulayan sunucu hello sayısının azaltılması hello birleşim tablosundan karşı kaydeder gidiş dönüş uygulamanızı toomake sahiptir.</span><span class="sxs-lookup"><span data-stu-id="41949-199">This saves that intermediary query against hello join table reducing hello number of server round trips your application has toomake.</span></span> 

## <span data-ttu-id="41949-200"><a id="WrapUp"></a>Karma veri modelleri</span><span class="sxs-lookup"><span data-stu-id="41949-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="41949-201">Biz şimdi inceledik katıştırma (veya denormalizing) ve başvuru (veya normalleştirme) veri her varsa bunların upsides ve her güvenlik ihlalleri anlatıldığı gibi.</span><span class="sxs-lookup"><span data-stu-id="41949-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="41949-202">Bunu değil her zaman toobe ya da vardır veya yoktur biraz Korkmuş toomix şeyler yukarı olabilir.</span><span class="sxs-lookup"><span data-stu-id="41949-202">It doesn't always have toobe either or, don't be scared toomix things up a little.</span></span> 

<span data-ttu-id="41949-203">Uygulamanızın belirli kullanım desenlerini ve burada karıştırma katıştırılmış durumlar olabilir iş yükleri göre ve başvurulan veri mantıklı ve hala iyi düzeyde performans korurken dönüşleri sağlama toosimpler uygulama mantığını daha az sunucusuyla yuvarlamak .</span><span class="sxs-lookup"><span data-stu-id="41949-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead toosimpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="41949-204">JSON aşağıdaki hello göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="41949-204">Consider hello following JSON.</span></span> 

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

<span data-ttu-id="41949-205">Burada burada diğer varlıklar verilerden hello en üst düzey belgede gömülü, ancak diğer veri başvurulan hello katıştırılmış modeli, (çoğunlukla) izlenen.</span><span class="sxs-lookup"><span data-stu-id="41949-205">Here we've (mostly) followed hello embedded model, where data from other entities are embedded in hello top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="41949-206">Merhaba kitap belge bakarsanız, birkaç görebiliriz biz yazarlar hello dizisi baktığınızda alanları ilginç.</span><span class="sxs-lookup"><span data-stu-id="41949-206">If you look at hello book document, we can see a few interesting fields when we look at hello array of authors.</span></span> <span data-ttu-id="41949-207">Var. bir *kimliği* kullanırız toorefer geri tooan Yazar belge, standart uygulamada normalleştirilmiş bir model, ancak daha sonra da hello alanı olan alanı *adı* ve *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="41949-207">There is an *id* field which is hello field we use toorefer back tooan author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="41949-208">Biz yalnızca ile takılmış *kimliği* ve hello uygulama tooget gerekli ek bilgileri hello "bağlantı" kullanarak hello ilgili Yazar belgeden sol ancak uygulamamız hello yazar adı görüntülediğinden ve bir görüntülenen her defteri ile küçük resim biz kaydedebilir kitap gidiş dönüş toohello Sunucu'yu bir listede denormalizing tarafından **bazı** verileri hello yazar.</span><span class="sxs-lookup"><span data-stu-id="41949-208">We could've just stuck with *id* and left hello application tooget any additional information it needed from hello respective author document using hello "link", but because our application displays hello author's name and a thumbnail picture with every book displayed we can save a round trip toohello server per book in a list by denormalizing **some** data from hello author.</span></span>

<span data-ttu-id="41949-209">Emin hello yazar adı değiştirilmiş ya da kendi photo tooupdate istedikleri biz toogo bir güncelleştirme olurdu her kitap hiç yayımlanmadan ancak yazarlar adlarını sıklıkla, değişmeyen hello duymadığını uygulamamız için bu kabul edilebilir bir tasarım karar.</span><span class="sxs-lookup"><span data-stu-id="41949-209">Sure, if hello author's name changed or they wanted tooupdate their photo we'd have toogo an update every book they ever published but for our application, based on hello assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="41949-210">Merhaba örnekte vardır **toplamalar'önceden hesaplanan** toosave üzerinde okuma işlem pahalı değerleri.</span><span class="sxs-lookup"><span data-stu-id="41949-210">In hello example there are **pre-calculated aggregates** values toosave expensive processing on a read operation.</span></span> <span data-ttu-id="41949-211">Merhaba örnekte hello Yazar belgede gömülü hello verilerin bazıları olduğundan çalışma zamanında hesaplanan veri.</span><span class="sxs-lookup"><span data-stu-id="41949-211">In hello example, some of hello data embedded in hello author document is data that is calculated at run-time.</span></span> <span data-ttu-id="41949-212">Yeni bir rehberi yayımlanan her zaman bir kitap belge oluşturulur **ve** hello countOfBooks alanını için belirli bir yazarın mevcut Kitap belgelerini hello sayısına dayalı tooa hesaplanan değer ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="41949-212">Every time a new book is published, a book document is created **and** hello countOfBooks field is set tooa calculated value based on hello number of book documents that exist for a particular author.</span></span> <span data-ttu-id="41949-213">Bu iyileştirme biz sipariş toooptimize okuma yazma toodo hesaplamalar burada destekleyebilir okuma ağır sistemlerinde iyi olacaktır.</span><span class="sxs-lookup"><span data-stu-id="41949-213">This optimization would be good in read heavy systems where we can afford toodo computations on writes in order toooptimize reads.</span></span>

<span data-ttu-id="41949-214">Azure Cosmos DB desteklediği için önceden hesaplanan alanları ile bir model olası yapıldığında özelliği toohave hello **Çoklu belge işlemler**.</span><span class="sxs-lookup"><span data-stu-id="41949-214">hello ability toohave a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="41949-215">Birçok NoSQL depoları belgeler arasında işlemleri yapın ve bu nedenle "her zaman her şeyi, toothis sınırlaması katıştırmak" gibi tasarım kararları advocate.</span><span class="sxs-lookup"><span data-stu-id="41949-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due toothis limitation.</span></span> <span data-ttu-id="41949-216">Azure Cosmos DB ile sunucu tarafı Tetikleyicileri ya da books ekleyebileceğiniz ve yazarlar ACID işlemi içinde tüm güncelleştirme saklı yordamları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41949-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="41949-217">Sizin artık **sahip** tooembed, her şeyi tooone belge yalnızca toobe verilerinizi tutarlı kalmasını.</span><span class="sxs-lookup"><span data-stu-id="41949-217">Now you don't **have** tooembed everything in tooone document just toobe sure that your data remains consistent.</span></span>

## <span data-ttu-id="41949-218"><a name="NextSteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41949-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="41949-219">Bu makaledeki Hello büyük paketler şemasız bir dünyada modelleme verileri olarak şimdiye kadar önemli olduğu toounderstand olur.</span><span class="sxs-lookup"><span data-stu-id="41949-219">hello biggest takeaways from this article is toounderstand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="41949-220">Hiçbir tek bir yolu toorepresent ekranda verileri bir parçasını yalnızca yok olarak verilerinizi tek bir yolu toomodel yoktur.</span><span class="sxs-lookup"><span data-stu-id="41949-220">Just as there is no single way toorepresent a piece of data on a screen, there is no single way toomodel your data.</span></span> <span data-ttu-id="41949-221">Toounderstand uygulamanız gerekir ve onu oluşturan nasıl kullanmak ve hello verileri işleme.</span><span class="sxs-lookup"><span data-stu-id="41949-221">You need toounderstand your application and how it will produce, consume, and process hello data.</span></span> <span data-ttu-id="41949-222">Ardından, bazı hello uygulayarak Burada sunulan yönergeleri uygulamanızın hello hemen gereksinimlerine yönelik bir model oluşturma hakkında ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41949-222">Then, by applying some of hello guidelines presented here you can set about creating a model that addresses hello immediate needs of your application.</span></span> <span data-ttu-id="41949-223">Uygulamalarınızı toochange gerektiğinde, şemasız veritabanı tooembrace hello esnekliğini değiştirmek ve veri modelinizi kolayca gelişmesi yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="41949-223">When your applications need toochange, you can leverage hello flexibility of a schema-free database tooembrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="41949-224">Azure Cosmos DB hakkında daha fazla toolearn başvuran toohello hizmetin [belgelerine](https://azure.microsoft.com/documentation/services/cosmos-db/) sayfası.</span><span class="sxs-lookup"><span data-stu-id="41949-224">toolearn more about Azure Cosmos DB, refer toohello service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="41949-225">toounderstand nasıl tooshard verilerinizi birden çok bölüm arasında başvurmak çok[bölümleme veri Azure Cosmos veritabanı](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="41949-225">toounderstand how tooshard your data across multiple partitions, refer too[Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
