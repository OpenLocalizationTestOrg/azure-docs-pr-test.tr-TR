---
title: "Azure Search'te kaynaklarına eşzamanlı yazma yönetme"
description: "İyimser eşzamanlılık güncelleştirmeleri veya Azure Search dizinlerini, dizin oluşturucular, veri kaynaklarını siler Orta hava çakışmalarını önlemek için kullanın."
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
ms.openlocfilehash: aee1b7376d4829e3e2f5a232525e3c3cb4df9d8e
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/29/2017
---
# <a name="how-to-manage-concurrency-in-azure-search"></a><span data-ttu-id="f029a-103">Azure Search'te eşzamanlılık yönetme</span><span class="sxs-lookup"><span data-stu-id="f029a-103">How to manage concurrency in Azure Search</span></span>

<span data-ttu-id="f029a-104">Özellikle kaynakları uygulamanız farklı bileşenleri tarafından eşzamanlı olarak erişilen, dizinler ve veri kaynakları gibi Azure Search kaynakları yönetirken, kaynaklara güvenli bir biçimde güncelleştirmek önemlidir.</span><span class="sxs-lookup"><span data-stu-id="f029a-104">When managing Azure Search resources such as indexes and data sources, it's important to update resources safely, especially if resources are accessed concurrently by different components of your application.</span></span> <span data-ttu-id="f029a-105">Yarış durumları, iki istemci aynı anda bir kaynak koordinasyon olmadan güncelleştirdiğinizde mümkündür.</span><span class="sxs-lookup"><span data-stu-id="f029a-105">When two clients concurrently update a resource without coordination, race conditions are possible.</span></span> <span data-ttu-id="f029a-106">Bunu önlemek için Azure Search sunan bir *iyimser eşzamanlılık modeli*.</span><span class="sxs-lookup"><span data-stu-id="f029a-106">To prevent this, Azure Search offers an *optimistic concurrency model*.</span></span> <span data-ttu-id="f029a-107">Bir kaynak kilit yok vardır.</span><span class="sxs-lookup"><span data-stu-id="f029a-107">There are no locks on a resource.</span></span> <span data-ttu-id="f029a-108">Bunun yerine, kaynak sürümü tanımlar ve böylece yanlışlıkla kaçının istekler oluşturabileceği tüm kaynakların üzerine yazar için ETag yoktur.</span><span class="sxs-lookup"><span data-stu-id="f029a-108">Instead, there is an ETag for every resource that identifies the resource version so that you can craft requests that avoid accidental overwrites.</span></span>

> [!Tip]
> <span data-ttu-id="f029a-109">Kavramsal kodda bir [örnek C# çözüm](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) eşzamanlılık denetimi Azure Search ile nasıl çalıştığı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f029a-109">Conceptual code in a [sample C# solution](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) explains how concurrency control works in Azure Search.</span></span> <span data-ttu-id="f029a-110">Kod eşzamanlılık denetim çağırma koşullar oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f029a-110">The code creates conditions that invoke concurrency control.</span></span> <span data-ttu-id="f029a-111">Okuma [aşağıdaki kod parçası](#samplecode) çalıştırmak istiyor ancak çoğu geliştirici, hizmet adı ve yönetici api anahtarı eklemek için appsettings.json düzenlemek için büyük olasılıkla yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="f029a-111">Reading the [code fragment below](#samplecode) is probably sufficient for most developers, but if you want to run it, edit appsettings.json to add the service name and an admin api-key.</span></span> <span data-ttu-id="f029a-112">Hizmet URL'sini verilen `http://myservice.search.windows.net`, hizmet adı `myservice`.</span><span class="sxs-lookup"><span data-stu-id="f029a-112">Given a service URL of `http://myservice.search.windows.net`, the service name is `myservice`.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="f029a-113">Nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="f029a-113">How it works</span></span>

<span data-ttu-id="f029a-114">İyimser eşzamanlılık uygulanan aracılığıyla erişimi koşul dizinler, dizin oluşturucular, veri kaynakları ve synonymMap kaynaklara yazma API çağrılarında denetler.</span><span class="sxs-lookup"><span data-stu-id="f029a-114">Optimistic concurrency is implemented through access condition checks in API calls writing to indexes, indexers, datasources, and synonymMap resources.</span></span> 

<span data-ttu-id="f029a-115">Tüm kaynaklara sahip bir [ *varlık etiketi (ETag)* ](https://en.wikipedia.org/wiki/HTTP_ETag) nesne sürüm bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f029a-115">All resources have an [*entity tag (ETag)*](https://en.wikipedia.org/wiki/HTTP_ETag) that provides object version information.</span></span> <span data-ttu-id="f029a-116">ETag ilk kontrol ederek, normal bir iş akışı eşzamanlı güncelleştirmeleri önleyebilirsiniz (almak, yerel olarak değiştirin, güncelleştirme) yerel kopyanızı kaynağın ETag eşleşmeleri sağlayarak.</span><span class="sxs-lookup"><span data-stu-id="f029a-116">By checking the ETag first, you can avoid concurrent updates in a typical workflow (get, modify locally, update) by ensuring the resource's ETag matches your local copy.</span></span> 

+ <span data-ttu-id="f029a-117">REST API'sini kullanan bir [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) istek üstbilgisi üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f029a-117">The REST API uses an [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on the request header.</span></span>
+ <span data-ttu-id="f029a-118">.NET SDK'sı ayarlama bir accessCondition nesnesi aracılığıyla ETag ayarlar [IF-Match | IF-Match-hiçbiri üstbilgi](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) kaynağı.</span><span class="sxs-lookup"><span data-stu-id="f029a-118">The .NET SDK sets the ETag through an accessCondition object, setting the [If-Match | If-Match-None header](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) on the resource.</span></span> <span data-ttu-id="f029a-119">İçinden devralma herhangi bir nesne [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) accessCondition nesneyi sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f029a-119">Any object inheriting from [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) has an accessCondition object.</span></span>

<span data-ttu-id="f029a-120">Bir kaynak güncelleştirme her zaman kendi ETag otomatik olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="f029a-120">Every time you update a resource, its ETag changes automatically.</span></span> <span data-ttu-id="f029a-121">Eşzamanlılık yönetimini uyguladığınızda, tüm yaptığınız koyma önkoşulu güncelleştirme isteğinde uzak kaynak kopya olarak istemci üzerinde değişiklik kaynağın aynı ETag olmasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f029a-121">When you implement concurrency management, all you're doing is putting a precondition on the update request that requires the remote resource to have the same ETag as the copy of the resource that you modified on the client.</span></span> <span data-ttu-id="f029a-122">Eşzamanlı bir işlem uzak kaynak zaten değiştiyse, ETag önkoşulu eşleşmez ve İstek HTTP 412 ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f029a-122">If a concurrent process has changed the remote resource already, the ETag will not match the precondition and the request will fail with HTTP 412.</span></span> <span data-ttu-id="f029a-123">.NET SDK'sı kullanıyorsanız, olarak bu bildirimleri bir `CloudException` burada `IsAccessConditionFailed()` genişletme yöntemi true döndürür.</span><span class="sxs-lookup"><span data-stu-id="f029a-123">If you're using the .NET SDK, this manifests as a `CloudException` where the `IsAccessConditionFailed()` extension method returns true.</span></span>

> [!Note]
> <span data-ttu-id="f029a-124">Eşzamanlılık için yalnızca bir mekanizma yoktur.</span><span class="sxs-lookup"><span data-stu-id="f029a-124">There is only one mechanism for concurrency.</span></span> <span data-ttu-id="f029a-125">Kaynak güncelleştirmeleri için kullanılan API bağımsız olarak her zaman kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f029a-125">It's always used regardless of which API is used for resource updates.</span></span> 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a><span data-ttu-id="f029a-126">Kullanım örnekleri ve örnek kod</span><span class="sxs-lookup"><span data-stu-id="f029a-126">Use cases and sample code</span></span>

<span data-ttu-id="f029a-127">Aşağıdaki kod, anahtar güncelleştirme işlemleri için accessCondition denetler gösterir:</span><span class="sxs-lookup"><span data-stu-id="f029a-127">The following code demonstrates accessCondition checks for key update operations:</span></span>

+ <span data-ttu-id="f029a-128">Bir güncelleştirme kaynağı artık yoksa başarısız</span><span class="sxs-lookup"><span data-stu-id="f029a-128">Fail an update if the resource no longer exists</span></span>
+ <span data-ttu-id="f029a-129">Kaynak sürümü değişirse bir güncelleştirme başarısız</span><span class="sxs-lookup"><span data-stu-id="f029a-129">Fail an update if the resource version changes</span></span>

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a><span data-ttu-id="f029a-130">Örnek koddan [DotNetETagsExplainer programı](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span><span class="sxs-lookup"><span data-stu-id="f029a-130">Sample code from [DotNetETagsExplainer program](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)</span></span>

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
            // of the resource you're working on. When you first create a resource such as an index, its ETag is
            // empty.
            Index index = DefineTestIndex();
            Console.WriteLine(
                $"Test index hasn't been created yet, so its ETag should be blank. ETag: '{index.ETag}'");

            // Once the resource exists in Azure Search, its ETag will be populated. Make sure to use the object
            // returned by the SearchServiceClient! Otherwise, you will still have the old object with the
            // blank ETag.
            Console.WriteLine("Creating index...\n");
            index = serviceClient.Indexes.Create(index);
            
            Console.WriteLine($"Test index created; Its ETag should be populated. ETag: '{index.ETag}'");

            // ETags let you do some useful things you couldn't do otherwise. For example, by using an If-Match
            // condition, we can update an index using CreateOrUpdate and be guaranteed that the update will only
            // succeed if the index already exists.
            index.Fields.Add(new Field("name", AnalyzerName.EnMicrosoft));
            index =
                serviceClient.Indexes.CreateOrUpdate(
                    index,
                    accessCondition: AccessCondition.GenerateIfExistsCondition());

            Console.WriteLine(
                $"Test index updated; Its ETag should have changed since it was created. ETag: '{index.ETag}'");

            // More importantly, ETags protect you from concurrent updates to the same resource. If another
            // client tries to update the resource, it will fail as long as all clients are using the right
            // access conditions.
            Index indexForClient1 = index;
            Index indexForClient2 = serviceClient.Indexes.Get("test");

            Console.WriteLine("Simulating concurrent update. To start, both clients see the same ETag.");
            Console.WriteLine($"Client 1 ETag: '{indexForClient1.ETag}' Client 2 ETag: '{indexForClient2.ETag}'");

            // Client 1 successfully updates the index.
            indexForClient1.Fields.Add(new Field("a", DataType.Int32));
            indexForClient1 =
                serviceClient.Indexes.CreateOrUpdate(
                    indexForClient1,
                    accessCondition: AccessCondition.IfNotChanged(indexForClient1));

            Console.WriteLine($"Test index updated by client 1; ETag: '{indexForClient1.ETag}'");

            // Client 2 tries to update the index, but fails, thanks to the ETag check.
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
                Console.WriteLine("Client 2 failed to update the index, as expected.");
            }

            // You can also use access conditions with Delete operations. For example, you can implement an
            // atomic version of the DeleteTestIndexIfExists method from this sample like this:
            Console.WriteLine("Deleting index...\n");
            serviceClient.Indexes.Delete("test", accessCondition: AccessCondition.GenerateIfExistsCondition());

            // This is slightly better than using the Exists method since it makes only one round trip to
            // Azure Search instead of potentially two. It also avoids an extra Delete request in cases where
            // the resource is deleted concurrently, but this doesn't matter much since resource deletion in
            // Azure Search is idempotent.

            // And we're done! Bye!
            Console.WriteLine("Complete.  Press any key to end application...\n");
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

## <a name="design-pattern"></a><span data-ttu-id="f029a-131">Tasarım deseni</span><span class="sxs-lookup"><span data-stu-id="f029a-131">Design pattern</span></span>

<span data-ttu-id="f029a-132">Uygulamak için bir tasarım deseni iyimser eşzamanlılık erişim koşulu yeniden deneme döngüsü içermelidir, erişim koşulu için bir sınama denetleyin ve değişiklikleri yeniden uygulamak denemeden önce güncelleştirilmiş bir kaynak isteğe bağlı olarak alır.</span><span class="sxs-lookup"><span data-stu-id="f029a-132">A design pattern for implementing optimistic concurrency should include a loop that retries the access condition check, a test for the access condition, and optionally retrieves an updated resource before attempting to re-apply the changes.</span></span> 

<span data-ttu-id="f029a-133">Bu kod parçacığını bir synonymMap zaten bir dizine eklenmesi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f029a-133">This code snippet illustrates the addition of a synonymMap to an index that already exists.</span></span> <span data-ttu-id="f029a-134">Bu kod arasındadır [Azure arama için eş anlamlı (Önizleme) C# Öğreticisi](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span><span class="sxs-lookup"><span data-stu-id="f029a-134">This code is from the [Synonym (preview) C# tutorial for Azure Search](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk).</span></span> 

<span data-ttu-id="f029a-135">Kod parçacığını "hotels" dizinini alır, bir güncelleştirme işlemi nesne sürümünde denetler, koşul başarısız olursa, bir özel durum oluşturur ve sonra işlemi (en fazla üç kez), en son sürümü edinmek için sunucudan dizin alma başlayarak yeniden dener.</span><span class="sxs-lookup"><span data-stu-id="f029a-135">The snippet gets the "hotels" index, checks the object version on an update operation, throws an exception if the condition fails, and then retries the operation (up to three times), starting with index retrieval from the server to get the latest version.</span></span>

        private static void EnableSynonymsInHotelsIndexSafely(SearchServiceClient serviceClient)
        {
            int MaxNumTries = 3;

            for (int i = 0; i < MaxNumTries; ++i)
            {
                try
                {
                    Index index = serviceClient.Indexes.Get("hotels");
                    index = AddSynonymMapsToFields(index);

                    // The IfNotChanged condition ensures that the index is updated only if the ETags match.
                    serviceClient.Indexes.CreateOrUpdate(index, accessCondition: AccessCondition.IfNotChanged(index));

                    Console.WriteLine("Updated the index successfully.\n");
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


## <a name="next-steps"></a><span data-ttu-id="f029a-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f029a-136">Next steps</span></span>

<span data-ttu-id="f029a-137">Gözden geçirme [anlamlıları C# örnek](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) güvenle varolan bir dizini güncelleştirme hakkında daha fazla bağlam için.</span><span class="sxs-lookup"><span data-stu-id="f029a-137">Review the [synonyms C# sample](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) for more context on how to safely update an existing index.</span></span>

<span data-ttu-id="f029a-138">Aşağıdaki örnekleri Etag'ler veya AccessCondition nesneleri içerecek şekilde ya da değiştirmeyi deneyin.</span><span class="sxs-lookup"><span data-stu-id="f029a-138">Try modifying either of the following samples to include ETags or AccessCondition objects.</span></span>

+ [<span data-ttu-id="f029a-139">REST API örneği github'daki</span><span class="sxs-lookup"><span data-stu-id="f029a-139">REST API sample on Github</span></span>](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ <span data-ttu-id="f029a-140">[.NET SDK'sı örneği github'daki](https://github.com/Azure-Samples/search-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="f029a-140">[.NET SDK sample on Github](https://github.com/Azure-Samples/search-dotnet-getting-started).</span></span> <span data-ttu-id="f029a-141">Bu çözüm, bu makaledeki sunulan kodu içeren "DotNetEtagsExplainer" projeyi içerir.</span><span class="sxs-lookup"><span data-stu-id="f029a-141">This solution includes the "DotNetEtagsExplainer" project containing the code presented in this article.</span></span>

## <a name="see-also"></a><span data-ttu-id="f029a-142">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f029a-142">See also</span></span>

  <span data-ttu-id="f029a-143">[Ortak HTTP istek ve yanıt üstbilgileri](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span><span class="sxs-lookup"><span data-stu-id="f029a-143">[Common HTTP request and response headers](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)  </span></span>  
  <span data-ttu-id="f029a-144">[HTTP durum kodları](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [dizin işlemler (REST API'si)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span><span class="sxs-lookup"><span data-stu-id="f029a-144">[HTTP status codes](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [Index operations (REST API)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)</span></span>