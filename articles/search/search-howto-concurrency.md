---
title: "eşzamanlı aaaHow toomanage tooresources Azure Search'te yazar."
description: "İyimser eşzamanlılık tooavoid Orta hava çakışmaları, güncelleştirme ve silme tooAzure arama dizinlerini, dizin oluşturucular, veri kaynaklarını kullanın."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: 
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/21/2017
ms.author: heidist
ms.openlocfilehash: c061d2b5c4d2dbd0fd5633405b01ab2912fbc754
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-concurrency-in-azure-search"></a><span data-ttu-id="ac35f-103">Nasıl Azure Search'te toomanage eşzamanlılık</span><span class="sxs-lookup"><span data-stu-id="ac35f-103">How toomanage concurrency in Azure Search</span></span>

<span data-ttu-id="ac35f-104">Özellikle kaynakları uygulamanız farklı bileşenleri tarafından eşzamanlı olarak erişilen dizinler ve veri kaynakları gibi Azure Search kaynakları yönetilirken önemli tooupdate kaynaklara güvenli bir biçimde iyisidir.</span><span class="sxs-lookup"><span data-stu-id="ac35f-104">When managing Azure Search resources such as indexes and data sources, it's important tooupdate resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="ac35f-105">Yarış durumları, iki istemci aynı anda bir kaynak koordinasyon olmadan güncelleştirdiğinizde mümkündür.</span><span class="sxs-lookup"><span data-stu-id="ac35f-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="ac35f-106">tooprevent Bu, Azure Search teklifleri bir *iyimser eşzamanlılık modeli*.</span><span class="sxs-lookup"><span data-stu-id="ac35f-106">tooprevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="ac35f-107">Bir kaynak kilit yok vardır.</span><span class="sxs-lookup"><span data-stu-id="ac35f-107">There are no locks on a resource.</span></span> <span data-ttu-id="ac35f-108">Bunun yerine, üzerine yazar hello kaynak sürümü tanımlar ve böylece yanlışlıkla kaçının istekler oluşturabileceği her kaynak için bir ETag yoktur.</span><span class="sxs-lookup"><span data-stu-id="ac35f-108">Instead, there is an ETag for every resource that identifies hello resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="ac35f-109">Kavramsal kodda bir [örnek C# çözüm](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) eşzamanlılık denetimi Azure Search ile nasıl çalıştığı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ac35f-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="ac35f-110">Eşzamanlılık denetim çağırma koşullar Hello kod oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ac35f-110">hello code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="ac35f-111">Okuma hello [aşağıdaki kod parçası](#samplecode) , düzenleme appsettings.json tooadd hello hizmet adı ve yönetici api anahtarı toorun istiyorsanız ancak çoğu geliştiriciler için büyük olasılıkla yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="ac35f-111">Reading hello [code fragment below](#samplecode) is probably sufficient for most developers, but if you want toorun it, edit appsettings.json tooadd hello service name and an admin api-key.</span></span> <span data-ttu-id="ac35f-112">Hizmet URL'sini verilen `http://myservice.search.windows.net`, hello hizmet adı `myservice`.</span><span class="sxs-lookup"><span data-stu-id="ac35f-112">Given a service URL of `http://myservice.search.windows.net`, hello service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="ac35f-113">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="ac35f-113">How it works</span></span>

<span data-ttu-id="ac35f-114">Erişimi aracılığıyla iyimser eşzamanlılık uygulanan koşul tooindexes, dizin oluşturucular, veri kaynakları ve synonymMap kaynakları yazma API çağrılarında denetler.</span><span class="sxs-lookup"><span data-stu-id="ac35f-114">Optimistic concurrency is implemented through access condition checks in API calls writing tooindexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="ac35f-115">Tüm kaynaklara sahip bir [ *varlık etiketi (ETag)* ](https://en.wikipedia.org/wiki/HTTP_ETag) nesne sürüm bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ac35f-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="ac35f-116">Merhaba ETag ilk kontrol ederek, normal bir iş akışı eşzamanlı güncelleştirmeleri önleyebilirsiniz (almak, yerel olarak değiştirin, güncelleştirme) yerel kopyanızı hello kaynağın ETag eşleşmeleri sağlayarak.</span><span class="sxs-lookup"><span data-stu-id="ac35f-116">By checking hello ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring hello resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="ac35f-117">Merhaba REST API'sini kullanan bir [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) hello istek üstbilgisi üzerinde.</span><span class="sxs-lookup"><span data-stu-id="ac35f-117">hello REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello request header.</span></span>
+ <span data-ttu-id="ac35f-118">Merhaba .NET SDK'sı ayarlar hello ETag hello ayarını bir accessCondition nesnesi aracılığıyla [IF-Match | IF-Match-hiçbiri üstbilgi](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) hello kaynakta.</span><span class="sxs-lookup"><span data-stu-id="ac35f-118">hello .NET SDK sets hello ETag through an accessCondition object, setting hello [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on hello resource.</span></span> <span data-ttu-id="ac35f-119">İçinden devralma herhangi bir nesne [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) accessCondition nesneyi sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ac35f-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="ac35f-120">Bir kaynak güncelleştirme her zaman kendi ETag otomatik olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ac35f-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="ac35f-121">Eşzamanlılık yönetimini uyguladığınızda, tüm yaptığınız koyma önkoşulu hello uzak kaynak gerektirir hello güncelleştirme isteğinde toohave hello hello istemcide değiştiren hello kaynağının hello kopya olarak aynı ETag.</span><span class="sxs-lookup"><span data-stu-id="ac35f-121">When you implement concurrency management, all you're doing is putting a precondition on hello update request that requires hello remote resource toohave hello same ETag as hello copy of hello resource that you modified on hello client.</span></span> <span data-ttu-id="ac35f-122">Eşzamanlı bir işlem hello uzak kaynak zaten değiştiyse, hello ETag hello önkoşulu eşleşmez ve hello isteği HTTP 412 ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ac35f-122">If a concurrent process has changed hello remote resource already, hello ETag will not match hello precondition and hello request will fail with HTTP 412.</span></span> <span data-ttu-id="ac35f-123">Merhaba .NET SDK'sı kullanıyorsanız, olarak bu bildirimleri bir `CloudException` burada hello `IsAccessConditionFailed()` genişletme yöntemi true döndürür.</span><span class="sxs-lookup"><span data-stu-id="ac35f-123">If you're using hello .NET SDK, this manifests as a `CloudException` where hello `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="ac35f-124">Eşzamanlılık için yalnızca bir mekanizma yoktur.</span><span class="sxs-lookup"><span data-stu-id="ac35f-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="ac35f-125">Kaynak güncelleştirmeleri için kullanılan API bağımsız olarak her zaman kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ac35f-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="ac35f-126">Kullanım örnekleri ve örnek kod</span><span class="sxs-lookup"><span data-stu-id="ac35f-126">Use cases and sample code</span></span>

<span data-ttu-id="ac35f-127">koddan hello anahtar güncelleştirme işlemleri için accessCondition denetler gösterir:</span><span class="sxs-lookup"><span data-stu-id="ac35f-127">hello following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="ac35f-128">Bir güncelleştirme Hello kaynak artık yoksa başarısız</span><span class="sxs-lookup"><span data-stu-id="ac35f-128">Fail an update if hello resource no longer exists</span></span>
+ <span data-ttu-id="ac35f-129">Merhaba kaynak sürümü değişirse bir güncelleştirme başarısız</span><span class="sxs-lookup"><span data-stu-id="ac35f-129">Fail an update if hello resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="ac35f-130">Örnek koddan [DotNetETagsExplainer programı](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="ac35f-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

```
    class Program
    {
        // This sample shows how ETags work by performing conditional updates and deletes
        // on an Azure Search index.
        static void Main(string[] args)
        {
            IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
            IConfigurationRoot configuration = builder.Build();

            SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

            Console.WriteLine("Deleting index...\n");
            DeleteTestIndexIfExists(serviceClient);

            // Every top-level resource in Azure Search has an associated ETag that keeps track of which version
            // of hello resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once hello resource exists in Azure Search, its ETag will be populated. Make sure toouse hello object
            // returned by hello SearchServiceClient! Otherwise, you will still have hello old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that hello update will only
            // succeed if hello index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates toohello same resource. If another
            // client tries tooupdate hello resource, it will fail as long as all clients are using hello right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. toostart, both clients see hello same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates hello index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries tooupdate hello index, but fails, thanks toohello ETag check.
            try
            {
                indexForClient2.Fields.Add(new Field("b", DataType.Boolean));
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient2, 
                    accessCondition: AccessCondition.IfNotChanged(indexForClient2));

                Console.WriteLine("Whoops; This shouldn't happen");
                Environment.Exit(1);
            }
            catch (CloudException e) when (e.IsAccessConditionFailed())
            {
                Console.WriteLine("Client 2 failed tooupdate hello index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of hello DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using hello Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // hello resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key tooend application...\n");
            Console.ReadKey();
        }

        private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
        {
            string searchServiceName = configuration["SearchServiceName"];
            string adminApiKey = configuration["SearchServiceAdminApiKey"];

            SearchServiceClient serviceClient =
                new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
            return serviceClient;
        }

        private static void DeleteTestIndexIfExists(SearchServiceClient serviceClient)
        {
            if (serviceClient.Indexes.Exists("test"))
            {
                serviceClient.Indexes.Delete("test");
            }
        }

        private static Index DefineTestIndex() =>
            new Index()
            {
                Name = "test",
                Fields = new[] { new Field("id", DataType.String) { IsKey = true } }
            };
    }
}
```

## <a name="design-pattern"></a><span data-ttu-id="ac35f-131">Tasarım deseni</span><span class="sxs-lookup"><span data-stu-id="ac35f-131">Design pattern</span></span>

<span data-ttu-id="ac35f-132">İyimser eşzamanlılık uygulamak için bir tasarım deseni hello erişim koşul denetimi, bir test hello erişim koşulu için yeniden deneme sayısı ve isteğe bağlı olarak toore denemeden önce güncelleştirilmiş bir kaynak alır bir döngü içermelidir-hello değişiklikleri uygulayın.</span><span class="sxs-lookup"><span data-stu-id="ac35f-132">A design pattern for implementing optimistic concurrency should include a loop that retries hello access condition check, a test for hello access condition, and optionally retrieves an updated resource before attempting toore-apply hello changes.</span></span> 

<span data-ttu-id="ac35f-133">Bu kod parçacığını zaten bir synonymMap tooan dizini hello eklenmesi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ac35f-133">This code snippet illustrates hello addition of a synonymMap tooan index that already exists.</span></span> <span data-ttu-id="ac35f-134">Bu kodu hello [Azure arama için eş anlamlı (Önizleme) C# Öğreticisi](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="ac35f-134">This code is from hello [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="ac35f-135">Merhaba parçacığı hello "hotels" dizinini alır, güncelleştirme işlemi üzerinde hello nesne sürümünü denetler, hello koşulu başarısız olursa ve ardından dizin alımı ile Merhaba sunucu tooget hello son başlatma işlemi (yukarı toothree zaman), yeniden deneme hello bir özel durum oluşturur Sürüm.</span><span class="sxs-lookup"><span data-stu-id="ac35f-135">hello snippet gets hello "hotels" index, checks hello object version on an update operation, throws an exception if hello condition fails, and then retries hello operation (up toothree times), starting with index retrieval from hello server tooget hello latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // hello IfNotChanged condition ensures that hello index is updated only if hello ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated hello index successfully.\n");
                    break;
                }
                catch (CloudException e) when (e.IsAccessConditionFailed())
                {
                    Console.WriteLine($"Index update failed : {e.Message}. Attempt({i}/{MaxNumTries}).\n");
                }
            }
        }
        
        private static Index AddSynonymMapsToFields(Index index)
        {
            index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
            index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };
            return index;
        }


## <a name="next-steps"></a><span data-ttu-id="ac35f-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ac35f-136">Next steps</span></span>

<span data-ttu-id="ac35f-137">Gözden geçirme hello [anlamlıları C# örnek](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) toosafely güncelleştirme mevcut bir dizine nasıl hakkında daha fazla bağlam için.</span><span class="sxs-lookup"><span data-stu-id="ac35f-137">Review hello [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how toosafely update an existing index.</span></span>

<span data-ttu-id="ac35f-138">Merhaba aşağıdakilerden birini değiştirmeyi deneyin tooinclude Etag'ler veya AccessCondition nesne örnekleri.</span><span class="sxs-lookup"><span data-stu-id="ac35f-138">Try modifying either of hello following samples tooinclude ETags or AccessCondition objects.</span></span>

+ [<span data-ttu-id="ac35f-139">REST API örneği github'daki</span><span class="sxs-lookup"><span data-stu-id="ac35f-139">REST API sample on Github</span></span>](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ <span data-ttu-id="ac35f-140">[.NET SDK'sı örneği github'daki](https://github.com/Azure-Samples/search-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="ac35f-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="ac35f-141">Bu çözüm, bu makaledeki sunulan hello kodu içeren hello "DotNetEtagsExplainer" proje içerir.</span><span class="sxs-lookup"><span data-stu-id="ac35f-141">This solution includes hello "DotNetEtagsExplainer" project containing hello code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="ac35f-142">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="ac35f-142">See also</span></span>

  <span data-ttu-id="ac35f-143">[Ortak HTTP istek ve yanıt üstbilgileri](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span><span class="sxs-lookup"><span data-stu-id="ac35f-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="ac35f-144">[HTTP durum kodları](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [dizin işlemler (REST API'si)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span><span class="sxs-lookup"><span data-stu-id="ac35f-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>