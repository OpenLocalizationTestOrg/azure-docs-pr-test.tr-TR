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
# <a name="how-toomanage-concurrency-in-azure-search"></a>Nasıl Azure Search'te toomanage eşzamanlılık

Özellikle kaynakları uygulamanız farklı bileşenleri tarafından eşzamanlı olarak erişilen dizinler ve veri kaynakları gibi Azure Search kaynakları yönetilirken önemli tooupdate kaynaklara güvenli bir biçimde iyisidir. Yarış durumları, iki istemci aynı anda bir kaynak koordinasyon olmadan güncelleştirdiğinizde mümkündür. tooprevent Bu, Azure Search teklifleri bir *iyimser eşzamanlılık modeli*. Bir kaynak kilit yok vardır. Bunun yerine, üzerine yazar hello kaynak sürümü tanımlar ve böylece yanlışlıkla kaçının istekler oluşturabileceği her kaynak için bir ETag yoktur.

> [!Tip]
> Kavramsal kodda bir [örnek C# çözüm](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer) eşzamanlılık denetimi Azure Search ile nasıl çalıştığı açıklanmaktadır. Eşzamanlılık denetim çağırma koşullar Hello kod oluşturur. Okuma hello [aşağıdaki kod parçası](#samplecode) , düzenleme appsettings.json tooadd hello hizmet adı ve yönetici api anahtarı toorun istiyorsanız ancak çoğu geliştiriciler için büyük olasılıkla yeterlidir. Hizmet URL'sini verilen `http://myservice.search.windows.net`, hello hizmet adı `myservice`.

## <a name="how-it-works"></a>Nasıl çalışır?

Erişimi aracılığıyla iyimser eşzamanlılık uygulanan koşul tooindexes, dizin oluşturucular, veri kaynakları ve synonymMap kaynakları yazma API çağrılarında denetler. 

Tüm kaynaklara sahip bir [ *varlık etiketi (ETag)* ](https://en.wikipedia.org/wiki/HTTP_ETag) nesne sürüm bilgilerini sağlar. Merhaba ETag ilk kontrol ederek, normal bir iş akışı eşzamanlı güncelleştirmeleri önleyebilirsiniz (almak, yerel olarak değiştirin, güncelleştirme) yerel kopyanızı hello kaynağın ETag eşleşmeleri sağlayarak. 

+ Merhaba REST API'sini kullanan bir [ETag](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) hello istek üstbilgisi üzerinde.
+ Merhaba .NET SDK'sı ayarlar hello ETag hello ayarını bir accessCondition nesnesi aracılığıyla [IF-Match | IF-Match-hiçbiri üstbilgi](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search) hello kaynakta. İçinden devralma herhangi bir nesne [IResourceWithETag (.NET SDK)](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.iresourcewithetag) accessCondition nesneyi sahiptir.

Bir kaynak güncelleştirme her zaman kendi ETag otomatik olarak değiştirir. Eşzamanlılık yönetimini uyguladığınızda, tüm yaptığınız koyma önkoşulu hello uzak kaynak gerektirir hello güncelleştirme isteğinde toohave hello hello istemcide değiştiren hello kaynağının hello kopya olarak aynı ETag. Eşzamanlı bir işlem hello uzak kaynak zaten değiştiyse, hello ETag hello önkoşulu eşleşmez ve hello isteği HTTP 412 ile başarısız olur. Merhaba .NET SDK'sı kullanıyorsanız, olarak bu bildirimleri bir `CloudException` burada hello `IsAccessConditionFailed()` genişletme yöntemi true döndürür.

> [!Note]
> Eşzamanlılık için yalnızca bir mekanizma yoktur. Kaynak güncelleştirmeleri için kullanılan API bağımsız olarak her zaman kullanılır. 

<a name="samplecode"></a>
## <a name="use-cases-and-sample-code"></a>Kullanım örnekleri ve örnek kod

koddan hello anahtar güncelleştirme işlemleri için accessCondition denetler gösterir:

+ Bir güncelleştirme Hello kaynak artık yoksa başarısız
+ Merhaba kaynak sürümü değişirse bir güncelleştirme başarısız

### <a name="sample-code-from-dotnetetagsexplainer-programhttpsgithubcomazure-samplessearch-dotnet-getting-startedtreemasterdotnetetagsexplainer"></a>Örnek koddan [DotNetETagsExplainer programı](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetETagsExplainer)

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

## <a name="design-pattern"></a>Tasarım deseni

İyimser eşzamanlılık uygulamak için bir tasarım deseni hello erişim koşul denetimi, bir test hello erişim koşulu için yeniden deneme sayısı ve isteğe bağlı olarak toore denemeden önce güncelleştirilmiş bir kaynak alır bir döngü içermelidir-hello değişiklikleri uygulayın. 

Bu kod parçacığını zaten bir synonymMap tooan dizini hello eklenmesi gösterilmektedir. Bu kodu hello [Azure arama için eş anlamlı (Önizleme) C# Öğreticisi](https://docs.microsoft.com/azure/search/search-synonyms-tutorial-sdk). 

Merhaba parçacığı hello "hotels" dizinini alır, güncelleştirme işlemi üzerinde hello nesne sürümünü denetler, hello koşulu başarısız olursa ve ardından dizin alımı ile Merhaba sunucu tooget hello son başlatma işlemi (yukarı toothree zaman), yeniden deneme hello bir özel durum oluşturur Sürüm.

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


## <a name="next-steps"></a>Sonraki adımlar

Gözden geçirme hello [anlamlıları C# örnek](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms) toosafely güncelleştirme mevcut bir dizine nasıl hakkında daha fazla bağlam için.

Merhaba aşağıdakilerden birini değiştirmeyi deneyin tooinclude Etag'ler veya AccessCondition nesne örnekleri.

+ [REST API örneği github'daki](https://github.com/Azure-Samples/search-rest-api-getting-started) 
+ [.NET SDK'sı örneği github'daki](https://github.com/Azure-Samples/search-dotnet-getting-started). Bu çözüm, bu makaledeki sunulan hello kodu içeren hello "DotNetEtagsExplainer" proje içerir.

## <a name="see-also"></a>Ayrıca bkz.

  [Ortak HTTP istek ve yanıt üstbilgileri](https://docs.microsoft.com/rest/api/searchservice/common-http-request-and-response-headers-used-in-azure-search)    
  [HTTP durum kodları](https://docs.microsoft.com/rest/api/searchservice/http-status-codes) [dizin işlemler (REST API'si)](https://docs.microsoft.com/\rest/api/searchservice/index-operations)