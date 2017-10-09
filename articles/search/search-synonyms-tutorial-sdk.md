---
title: "aaaSynonyms Önizleme Azure Search'te Öğreticisi | Microsoft Docs"
description: "Azure Search'te Hello eş anlamlıları önizleme özelliği tooan dizin ekleyin."
services: search
manager: jhubbard
documentationcenter: 
author: HeidiSteen
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 03/31/2017
ms.author: heidist
ms.openlocfilehash: 055c1cbafb945823a3dc4da0c522db236b1d192c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="synonym-preview-c-tutorial-for-azure-search"></a><span data-ttu-id="35ad0-103">Azure Search için eş anlamlı (önizleme) C# öğreticisi</span><span class="sxs-lookup"><span data-stu-id="35ad0-103">Synonym (preview) C# tutorial for Azure Search</span></span>

<span data-ttu-id="35ad0-104">Eş anlamlıları anlam olarak eşdeğer toohello giriş terim kabul koşullarınızda eşleştirerek bir sorgu genişletin.</span><span class="sxs-lookup"><span data-stu-id="35ad0-104">Synonyms expand a query by matching on terms considered semantically equivalent toohello input term.</span></span> <span data-ttu-id="35ad0-105">Örneğin, "araba" toomatch belgeleri hello koşulları "otomobil" veya "araç" içeren isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35ad0-105">For example, you might want "car" toomatch documents containing hello terms "automobile" or "vehicle".</span></span>

<span data-ttu-id="35ad0-106">Azure Search’te, eş anlamlılar eşdeğer terimleri ilişkilendiren *eşleme kuralları* aracılığıyla bir *eş anlamlı eşleminde* tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="35ad0-106">In Azure Search, synonyms are defined in a *synonym map*, through *mapping rules* that associate equivalent terms.</span></span> <span data-ttu-id="35ad0-107">Birden çok eş eşlemesi oluşturmak, bir hizmet geneli kaynak kullanılabilir tooany dizini gönderme ve hello alan düzeyinde bir hangi toouse başvuru.</span><span class="sxs-lookup"><span data-stu-id="35ad0-107">You can create multiple synonym maps, post them as a service-wide resource available tooany index, and then reference which one toouse at hello field level.</span></span> <span data-ttu-id="35ad0-108">Merhaba sorguda kullanılan alanları belirtilmişse, sorgu zamanında toosearching dizin, Azure Search ayrıca eş eşlemesindeki bir arama yapar.</span><span class="sxs-lookup"><span data-stu-id="35ad0-108">At query time, in addition toosearching an index, Azure Search does a lookup in a synonym map, if one is specified on fields used in hello query.</span></span>

> [!NOTE]
> <span data-ttu-id="35ad0-109">Merhaba anlamlıları özelliği şu anda, Önizleme ve desteklenen yalnızca en son Önizleme API ve SDK sürümleri hello (API sürümü 2016-09-01-Önizleme, SDK sürüm 4.x-Önizleme =).</span><span class="sxs-lookup"><span data-stu-id="35ad0-109">hello synonyms feature is currently in preview and only supported in hello latest preview API and SDK versions (api-version=2016-09-01-Preview, SDK version 4.x-preview).</span></span> <span data-ttu-id="35ad0-110">Şu anda Azure portalı desteği yoktur.</span><span class="sxs-lookup"><span data-stu-id="35ad0-110">There is no Azure portal support at this time.</span></span> <span data-ttu-id="35ad0-111">Önizleme API’leri SLA kapsamında değildir ve önizleme özellikleri değişebilir; bu nedenle, üretim uygulamalarında kullanılması önerilmez.</span><span class="sxs-lookup"><span data-stu-id="35ad0-111">Preview APIs are not under SLA and preview features may change, so we do not recommend using them in production applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="35ad0-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="35ad0-112">Prerequisites</span></span>

<span data-ttu-id="35ad0-113">Eğitmen gereksinimleri hello şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="35ad0-113">Tutorial requirements include hello following:</span></span>

* [<span data-ttu-id="35ad0-114">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="35ad0-114">Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="35ad0-115">Azure Search hizmeti</span><span class="sxs-lookup"><span data-stu-id="35ad0-115">Azure Search service</span></span>](search-create-service-portal.md)
* [<span data-ttu-id="35ad0-116">Microsoft.Azure.Search .NET kitaplığının önizleme sürümü</span><span class="sxs-lookup"><span data-stu-id="35ad0-116">Preview version of Microsoft.Azure.Search .NET library</span></span>](https://aka.ms/search-sdk-preview)
* [<span data-ttu-id="35ad0-117">Bir .NET uygulamasından Azure toouse arama nasıl</span><span class="sxs-lookup"><span data-stu-id="35ad0-117">How toouse Azure Search from a .NET Application</span></span>](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk)

## <a name="overview"></a><span data-ttu-id="35ad0-118">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="35ad0-118">Overview</span></span>

<span data-ttu-id="35ad0-119">Önce ve sonra sorguları eş anlamlıları hello değerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="35ad0-119">Before-and-after queries demonstrate hello value of synonyms.</span></span> <span data-ttu-id="35ad0-120">Bu öğreticide, sorguları yürüten ve sonuçları bir örnek dizinde döndüren örnek bir uygulama kullanılır.</span><span class="sxs-lookup"><span data-stu-id="35ad0-120">In this tutorial, we use a sample application that executes queries and returns results on a sample index.</span></span> <span data-ttu-id="35ad0-121">Merhaba örnek uygulaması "iki belgelerle doldurulmuş hotels" adlı küçük bir dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="35ad0-121">hello sample application creates a small index named "hotels" populated with two documents.</span></span> <span data-ttu-id="35ad0-122">Merhaba uygulaması hüküm ve hello dizinde görünmez tümcecikleri kullanarak arama sorguları çalıştırır, sorunları aynı aramaları yeniden hello sonra hello eş anlamlıları özelliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="35ad0-122">hello application executes search queries using terms and phrases that do not appear in hello index, enables hello synonyms feature, then issues hello same searches again.</span></span> <span data-ttu-id="35ad0-123">Aşağıdaki Hello kodu gösterir hello genel akış.</span><span class="sxs-lookup"><span data-stu-id="35ad0-123">hello code below demonstrates hello overall flow.</span></span>

```csharp
  static void Main(string[] args)
  {
      SearchServiceClient serviceClient = CreateSearchServiceClient();

      Console.WriteLine("{0}", "Cleaning up resources...\n");
      CleanupResources(serviceClient);

      Console.WriteLine("{0}", "Creating index...\n");
      CreateHotelsIndex(serviceClient);

      ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

      Console.WriteLine("{0}", "Uploading documents...\n");
      UploadDocuments(indexClient);

      ISearchIndexClient indexClientForQueries = CreateSearchIndexClient();

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Adding synonyms...\n");
      UploadSynonyms(serviceClient);
      EnableSynonymsInHotelsIndex(serviceClient);
      Thread.Sleep(10000); // Wait for hello changes toopropagate

      RunQueriesWithNonExistentTermsInIndex(indexClientForQueries);

      Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");

      Console.ReadKey();
  }
```
<span data-ttu-id="35ad0-124">Merhaba adımları toocreate ve hello örnek dizinini doldurmak açıklanacak [toouse Azure arama nasıl bir .NET uygulamasından](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span><span class="sxs-lookup"><span data-stu-id="35ad0-124">hello steps toocreate and populate hello sample index are explained in [How toouse Azure Search from a .NET Application](https://docs.microsoft.com/azure/search/search-howto-dotnet-sdk).</span></span>

## <a name="before-queries"></a><span data-ttu-id="35ad0-125">"Öncesi" sorguları</span><span class="sxs-lookup"><span data-stu-id="35ad0-125">"Before" queries</span></span>

<span data-ttu-id="35ad0-126">`RunQueriesWithNonExistentTermsInIndex` içinde "beş yıldızlı", "internet" ve "ekonomik VE otel" ile arama sorguları gönderdik.</span><span class="sxs-lookup"><span data-stu-id="35ad0-126">In `RunQueriesWithNonExistentTermsInIndex`, we issue search queries with "five star", "internet", and "economy AND hotel".</span></span>
```csharp
Console.WriteLine("Search hello entire index for hello phrase \"five star\":\n");
results = indexClient.Documents.Search<Hotel>("\"five star\"", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello term 'internet':\n");
results = indexClient.Documents.Search<Hotel>("internet", parameters);
WriteDocuments(results);

Console.WriteLine("Search hello entire index for hello terms 'economy' AND 'hotel':\n");
results = indexClient.Documents.Search<Hotel>("economy AND hotel", parameters);
WriteDocuments(results);
```
<span data-ttu-id="35ad0-127">Böylece biz hello ilk çıkış hello aşağıdaki elde hello iki dizinlenmiş belgeleri hiçbiri hello terimleri içeren `RunQueriesWithNonExistentTermsInIndex`.</span><span class="sxs-lookup"><span data-stu-id="35ad0-127">Neither of hello two indexed documents contain hello terms, so we get hello following output from hello first `RunQueriesWithNonExistentTermsInIndex`.</span></span>
~~~
Search hello entire index for hello phrase "five star":

no document matched

Search hello entire index for hello term 'internet':

no document matched

Search hello entire index for hello terms 'economy' AND 'hotel':

no document matched
~~~

## <a name="enable-synonyms"></a><span data-ttu-id="35ad0-128">Eş anlamlıları etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="35ad0-128">Enable synonyms</span></span>

<span data-ttu-id="35ad0-129">Eş anlamlıların etkinleştirilmesi iki adımlı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="35ad0-129">Enabling synonyms is a two-step process.</span></span> <span data-ttu-id="35ad0-130">Biz öncelikle tanımlamanız ve eş kuralları karşıya yükleme ve alanları toouse yapılandırmak bunları.</span><span class="sxs-lookup"><span data-stu-id="35ad0-130">We first define and upload synonym rules and then configure fields toouse them.</span></span> <span data-ttu-id="35ad0-131">Merhaba işlem özetlenen içinde `UploadSynonyms` ve `EnableSynonymsInHotelsIndex`.</span><span class="sxs-lookup"><span data-stu-id="35ad0-131">hello process is outlined in `UploadSynonyms` and `EnableSynonymsInHotelsIndex`.</span></span>

1. <span data-ttu-id="35ad0-132">Bir eş anlamlı harita tooyour arama hizmeti ekleyin.</span><span class="sxs-lookup"><span data-stu-id="35ad0-132">Add a synonym map tooyour search service.</span></span> <span data-ttu-id="35ad0-133">İçinde `UploadSynonyms`, bizim eş eşlemesinde 'desc-synonymmap' dört kurallar tanımlamak ve toohello hizmet karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="35ad0-133">In `UploadSynonyms`, we define four rules in our synonym map 'desc-synonymmap' and upload toohello service.</span></span>
```csharp
    var synonymMap = new SynonymMap()
    {
        Name = "desc-synonymmap",
        Format = "solr",
        Synonyms = "hotel, motel\n
                    internet,wifi\n
                    five star=>luxury\n
                    economy,inexpensive=>budget"
    };

    serviceClient.SynonymMaps.CreateOrUpdate(synonymMap);
```
<span data-ttu-id="35ad0-134">Bir eş anlamlı harita toohello açık kaynak standart uymalıdır `solr` biçimi.</span><span class="sxs-lookup"><span data-stu-id="35ad0-134">A synonym map must conform toohello open source standard `solr` format.</span></span> <span data-ttu-id="35ad0-135">Merhaba biçimi içinde açıklanan [Azure Search eş anlamlı](search-synonyms.md) hello bölümünde `Apache Solr synonym format`.</span><span class="sxs-lookup"><span data-stu-id="35ad0-135">hello format is explained in [Synonyms in Azure Search](search-synonyms.md) under hello section `Apache Solr synonym format`.</span></span>

2. <span data-ttu-id="35ad0-136">Aranabilir alanlara toouse hello eş harita hello dizin tanımında yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="35ad0-136">Configure searchable fields toouse hello synonym map in hello index definition.</span></span> <span data-ttu-id="35ad0-137">İçinde `EnableSynonymsInHotelsIndex`, iki alanlar anlamlıları etkinleştirme `category` ve `tags` hello ayarı tarafından `synonymMaps` özellik toohello hello adını yeni karşıya eş eşleme.</span><span class="sxs-lookup"><span data-stu-id="35ad0-137">In `EnableSynonymsInHotelsIndex`, we enable synonyms on two fields `category` and `tags` by setting hello `synonymMaps` property toohello name of hello newly uploaded synonym map.</span></span>
```csharp
  Index index = serviceClient.Indexes.Get("hotels");
  index.Fields.First(f => f.Name == "category").SynonymMaps = new[] { "desc-synonymmap" };
  index.Fields.First(f => f.Name == "tags").SynonymMaps = new[] { "desc-synonymmap" };

  serviceClient.Indexes.CreateOrUpdate(index);
```
<span data-ttu-id="35ad0-138">Bir eş anlamlı eşlemi eklediğinizde, dizinin yeniden oluşturulması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="35ad0-138">When you add a synonym map, index rebuilds are not required.</span></span> <span data-ttu-id="35ad0-139">Bir eş anlamlı harita tooyour hizmet eklemek ve varolan alan tanımları eşlemindeki tüm dizin toouse hello yeni eş düzeltmek.</span><span class="sxs-lookup"><span data-stu-id="35ad0-139">You can add a synonym map tooyour service, and then amend existing field definitions in any index toouse hello new synonym map.</span></span> <span data-ttu-id="35ad0-140">Yeni öznitelikler Hello eklenmesi dizin kullanılabilirliğine hiçbir etkisi olmaz.</span><span class="sxs-lookup"><span data-stu-id="35ad0-140">hello addition of new attributes has no impact on index availability.</span></span> <span data-ttu-id="35ad0-141">Merhaba aynı devre dışı bırakılırken bir alan için eş anlamlı sözcükleri uygular.</span><span class="sxs-lookup"><span data-stu-id="35ad0-141">hello same applies in disabling synonyms for a field.</span></span> <span data-ttu-id="35ad0-142">Merhaba yalnızca ayarlayabileceğiniz `synonymMaps` özelliği tooan boş bir liste.</span><span class="sxs-lookup"><span data-stu-id="35ad0-142">You can simply set hello `synonymMaps` property tooan empty list.</span></span>
```csharp
  index.Fields.First(f => f.Name == "category").SynonymMaps = new List<string>();
```

## <a name="after-queries"></a><span data-ttu-id="35ad0-143">"Sonrası" sorguları</span><span class="sxs-lookup"><span data-stu-id="35ad0-143">"After" queries</span></span>

<span data-ttu-id="35ad0-144">Merhaba eş harita yüklendiği ve hello dizin güncelleştirilmiş toouse hello eş harita sonra ikinci hello `RunQueriesWithNonExistentTermsInIndex` çağrısı hello aşağıdaki çıkarır:</span><span class="sxs-lookup"><span data-stu-id="35ad0-144">After hello synonym map is uploaded and hello index is updated toouse hello synonym map, hello second `RunQueriesWithNonExistentTermsInIndex` call outputs hello following:</span></span>

~~~
Search hello entire index for hello phrase "five star":

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello term 'internet':

Name: Fancy Stay        Category: Luxury        Tags: [pool, view, wifi, concierge]

Search hello entire index for hello terms 'economy' AND 'hotel':

Name: Roach Motel       Category: Budget        Tags: [motel, budget]
~~~
<span data-ttu-id="35ad0-145">Merhaba ilk sorgu bulur hello hello kural belgeden `five star=>luxury`.</span><span class="sxs-lookup"><span data-stu-id="35ad0-145">hello first query finds hello document from hello rule `five star=>luxury`.</span></span> <span data-ttu-id="35ad0-146">Merhaba ikinci sorguyu genişletir hello arama'yı kullanarak `internet,wifi` ve üçüncü her ikisini de kullanarak hello `hotel, motel` ve `economy,inexpensive=>budget` hello belgeleri bulma bunlar eşleşti.</span><span class="sxs-lookup"><span data-stu-id="35ad0-146">hello second query expands hello search using `internet,wifi` and hello third using both `hotel, motel` and `economy,inexpensive=>budget` in finding hello documents they matched.</span></span>

<span data-ttu-id="35ad0-147">Eş anlamlıları tamamen ekleme hello arama deneyimi değiştirir.</span><span class="sxs-lookup"><span data-stu-id="35ad0-147">Adding synonyms completely changes hello search experience.</span></span> <span data-ttu-id="35ad0-148">Bu öğreticide, dizinimizi Hello belgelerde ilgili olsa bile hello özgün sorguları tooreturn anlamlı sonuçlar başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="35ad0-148">In this tutorial, hello original queries failed tooreturn meaningful results even though hello documents in our index were relevant.</span></span> <span data-ttu-id="35ad0-149">Eş anlamlıları etkinleştirerek, genelde, hello dizindeki değişiklikleri toounderlying veri içermeyen kullanım koşullarına bir dizin tooinclude genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35ad0-149">By enabling synonyms, we can expand an index tooinclude terms in common use, with no changes toounderlying data in hello index.</span></span>

## <a name="sample-application-source-code"></a><span data-ttu-id="35ad0-150">Örnek uygulama kaynak kodu</span><span class="sxs-lookup"><span data-stu-id="35ad0-150">Sample application source code</span></span>
<span data-ttu-id="35ad0-151">Merhaba örnek uygulaması bu ilerlemesi üzerinde kullanılan hello tam kaynak kodunu bulabilirsiniz [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span><span class="sxs-lookup"><span data-stu-id="35ad0-151">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToSynonyms).</span></span>

## <a name="next-steps"></a><span data-ttu-id="35ad0-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="35ad0-152">Next steps</span></span>

* <span data-ttu-id="35ad0-153">Gözden geçirme [nasıl Azure Search toouse eş anlamlı](search-synonyms.md)</span><span class="sxs-lookup"><span data-stu-id="35ad0-153">Review [How toouse synonyms in Azure Search](search-synonyms.md)</span></span>
* <span data-ttu-id="35ad0-154">[Eş anlamlılar REST API belgelerini](https://aka.ms/rgm6rq) gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="35ad0-154">Review [Synonyms REST API documentation](https://aka.ms/rgm6rq)</span></span>
* <span data-ttu-id="35ad0-155">Hello için Hello başvuruları Gözat [.NET SDK'sı](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) ve [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="35ad0-155">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
