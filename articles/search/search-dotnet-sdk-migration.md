---
title: "Azure Search .NET SDK sürüm 1.1 aaaUpgrading toohello | Microsoft Docs"
description: "Azure Search .NET SDK sürüm 1.1 toohello yükseltme"
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a>Azure Search .NET SDK sürüm 3 toohello yükseltme
2.0-Önizleme veya Merhaba, daha eski bir sürümü kullanıyorsanız [Azure Search .NET SDK'sı](https://aka.ms/search-sdk), bu makalede, uygulama toouse sürüm 3 yükseltmenize yardımcı olur.

Merhaba SDK daha genel bir kılavuz için de dahil olmak üzere örneklere bakın [toouse Azure arama nasıl bir .NET uygulamasından](search-howto-dotnet-sdk.md).

Hello Azure Search .NET SDK 3 sürümünü önceki sürümlerinden bazı değişiklikler içerir. Kodunuzu değiştirmeden yalnızca en az çaba gerektirmelidir şekilde çoğunlukla ikincil, bunlar. Bkz: [adımları tooupgrade](#UpgradeSteps) yönelik yönergeler toochange, kod toouse hello yeni SDK sürümü.

> [!NOTE]
> Sürüm 1.0.2-preview kullanıyorsanız veya daha eski, tooversion 1.1 yükseltmeniz ve ardından tooversion 3 yükseltmeniz gerekir. Bkz: [ek: adımları tooupgrade tooversion 1.1](#UpgradeStepsV1) yönergeler için.
>
> Azure Search Hizmeti örneğinizi hello en son dahil olmak üzere birkaç REST API sürümlerini destekler. En son Merhaba, ancak, kod toouse hello en yeni sürüme geçirmek öneririz artık olduğunda toouse bir sürüm devam edebilirsiniz. Merhaba REST API kullanırken, her istek hello api-version parametresi aracılığıyla hello API sürümü belirtmeniz gerekir. Merhaba .NET SDK kullanarak olduğunda hello hello kullanmakta olduğunuz SDK sürümü hello ilgili hello REST API sürümü belirler. Eski bir SDK kullanıyorsanız, hello hizmet yükseltilmiş toosupport daha yeni bir API sürümü olsa bile, hiçbir değişiklik kodla toorun devam edebilirsiniz.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a>Sürüm 3 yenilikler nelerdir?
Hello Azure Search .NET SDK'sı hedefleri hello son 3 sürümünü hello Azure Search REST API'si, özellikle 2016-09-01 genel olarak kullanılabilir sürümü. Bu, olası toouse kolaylaştırır hello aşağıdakiler dahil, bir .NET uygulamasından Azure Search'ün birçok yeni özellik:

* [Özel çözümleyiciler](https://aka.ms/customanalyzers)
* [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) ve [Azure Table Storage](search-howto-indexing-azure-tables.md) dizin oluşturucu desteği
* Dizin Oluşturucu özelleştirme aracılığıyla [alan eşlemeleri](search-indexer-field-mappings.md)
* Etag'ler tooenable güvenli eşzamanlı dizin tanımları, dizin oluşturucular ve veri kaynaklarını güncelleştirme desteği
* Dizin alan tanımları bildirimli olarak model sınıfınız dekorasyon ve hello kullanarak yeni oluşturmak için destek `FieldBuilder` sınıfı.
* .NET Core ve .NET taşınabilir profil 111 desteği

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Adımları tooupgrade
İlk olarak, NuGet başvuru için güncelleştirme `Microsoft.Azure.Search` ya da hello NuGet Paket Yöneticisi konsolu kullanılarak veya göre proje başvuruları sağ tıklayıp Visual Studio'da "NuGet paketleri...'ı Yönet" seçerek.

NuGet hello yeni paketleri ve bunların bağımlılıklarını indirdikten sonra projenizi yeniden derleyin. Kodunuzu nasıl yapılandırıldığını bağlı olarak başarılı bir şekilde yeniden oluşturmak. Bu durumda, hazır toogo dileriz!

Derleme başarısız olursa, bir derleme hatası hello aşağıdaki gibi görmeniz gerekir:

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

Merhaba sonraki adıma toofix bu yapı hatasıdır. Bkz: [önemli değişiklikler sürüm 3](#ListOfChanges) ne hello hatasına neden oluyor ile ilgili ayrıntılar için ve nasıl toofix onu.

Ek yapı görebilirsiniz uyarılarla ilgili tooobsolete yöntemleri veya özellikleri. Merhaba uyarıları ne toouse, Merhaba bunun yerine özelliği kullanım dışı. ilgili yönergeler içerir. Örneğin, uygulamanız hello kullanıyorsa `IndexingParameters.Base64EncodeKeys` özelliği bildiren bir uyarı almak`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`

Derleme hataları düzelttik sonra isterseniz tooyour uygulama tootake yeni işlevsellik avantajlarından değişiklik yapabilirsiniz. Merhaba SDK yeni özellikleri ayrıntılı olarak [sürüm 3 yenilikler](#WhatsNew).

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a>Sürüm 3'de yeni değişiklikler
Var. kod gerektirebilecek önemli değişiklikler 3 sürümündeki az sayıda ek olarak, uygulamanızın toorebuilding değiştirir.

### <a name="indexesgetclient-return-type"></a>Indexes.GetClient dönüş türü
Merhaba `Indexes.GetClient` yöntemi yeni bir dönüş türüne sahip. Daha önce döndürülen `SearchIndexClient`, ancak bu çok değiştirildi`ISearchIndexClient` sürüm 2.0-Önizleme ve bu değişiklik 3 tooversion yürütür. Bu toomock hello istiyor toosupport müşterileri içindir `GetClient` yöntemi, sahte bir uygulama döndürerek birim testleri için `ISearchIndexClient`.

#### <a name="example"></a>Örnek
Kodunuzu şöyle ise:

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

Toothis toofix değiştirmek herhangi bir derleme hataları:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a>Örtük olarak dönüştürülebilir toostrings AnalyzerName, veri türü ve diğerleri artık olmayan
Hello Azure Search .NET SDK'sı, türetilen birçok türlerinde vardır `ExtensibleEnum`. Daha önce bu türleri tüm dolaylı olarak dönüştürülebilir tootype olan `string`. Ancak, bir hata hello bulunan `Object.Equals` uygulaması bu sınıfları ve bu örtük dönüştürme devre dışı bırakılması gereken giderilmesi hello hata. Açık dönüşüm çok`string` hala izin verilir.

#### <a name="example"></a>Örnek
Kodunuzu şöyle ise:

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

Toothis toofix değiştirmek herhangi bir derleme hataları:

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a>Eski üyeler kaldırıldı

Derleme hataları ilgili toomethods veya sürüm 2.0-Önizleme'te eski olarak işaretlenen ve daha sonra sürüm 3 kaldırılan özellikler görebilirsiniz. Bu tür hatalarla karşılaşırsanız, işte nasıl tooresolve bunları:

- Bu oluşturucu kullanıyorsanız: `ScoringParameter(string name, string value)`, bunun yerine bunu kullanın:`ScoringParameter(string name, IEnumerable<string> values)`
- Merhaba kullanıyorsanız `ScoringParameter.Value` özelliği, kullanım hello `ScoringParameter.Values` özelliği veya hello `ToString` yöntemi yerine.
- Merhaba kullanıyorsanız `SearchRequestOptions.RequestId` özelliği, kullanım hello `ClientRequestId` özelliği yerine.

### <a name="removed-preview-features"></a>Kaldırılan Önizleme özellikleri

Sürüm 2.0-Önizleme tooversion 3 ' yükseltiyorsanız, JSON ve Blob dizin oluşturucular için destek ayrıştırma CSV kaldırıldı, bu özellikler hala önizlemede olduğundan unutmayın. Özellikle, hello yöntemlerinin aşağıdaki hello `IndexingParametersExtensions` sınıfı kaldırıldı:

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

Uygulamanız bu özelliklere sıkı bir bağımlılık varsa, hello Azure Search .NET SDK'sı, mümkün tooupgrade tooversion 3 olmaz. Toouse sürüm 2.0-Önizleme devam edebilirsiniz. Bununla birlikte, lütfen aklınızda **üretim uygulamaları SDK'ları önizlemede kullanmanızı önermiyoruz**. Önizleme özellikleri yalnızca değerlendirme ve değişiklik.

## <a name="conclusion"></a>Sonuç
Hello Azure Search .NET SDK'sını kullanma hakkında daha fazla ayrıntı gereksinim duyarsanız, yeni güncelleştirilen bakın [nasıl yapılır](search-howto-dotnet-sdk.md).

SDK hello üzerinde bildiriminiz bizim. Sorunlarla karşılaşırsanız, ücretsiz tooask bize hello hakkında Yardım için eşitleyerek [Azure arama MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch). Bir hata bulursanız, hello sorunu dosya [Azure .NET SDK GitHub deposunu](https://github.com/Azure/azure-sdk-for-net/issues). Sorunu başlıkla emin tooprefix olun "arama SDK:".

Azure Search kullandığınız için teşekkür ederiz!

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a>Ek: Adımları tooupgrade tooversion 1.1
> [!NOTE]
> Bu bölüm, yalnızca toousers hello Azure Search .NET SDK sürüm 1.0.2-preview ve eski geçerlidir.
> 
> 

İlk olarak, NuGet başvuru için güncelleştirme `Microsoft.Azure.Search` ya da hello NuGet Paket Yöneticisi konsolu kullanılarak veya göre proje başvuruları sağ tıklayıp Visual Studio'da "NuGet paketleri...'ı Yönet" seçerek.

NuGet hello yeni paketleri ve bunların bağımlılıklarını indirdikten sonra projenizi yeniden derleyin.

Varsa, daha önce sürüm 1.0.0-preview, 1.0.1-preview veya 1.0.2-preview, hello yapı kullanarak başarılı olması gerekir ve hazır toogo demektir!

Daha önce sürüm 0.13.0-preview kullanıyorsanız veya daha eski, görmeniz gerekir derleme hataları hello aşağıdaki gibi:

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

Merhaba sonraki toofix hello derleme hataları tek tek bir adımdır. Çoğu hello SDK yeniden adlandırıldığı bazı sınıfı ve yöntemi adlarını değiştirme gerektirir. [Yeni sürüm 1.1 değişiklikler listesi](#ListOfChangesV1) adı değişikliklerin listesini içerir.

Belgelerinizi özel sınıflar toomodel kullanıyorsanız ve bu sınıfların null ilkel türler özelliklerini varsa (örneğin, `int` veya `bool` C#), hello 1.1 hangisinin olmanız gerekir kullanan hello SDK sürümünde hata düzeltmesi yoktur. Bkz: [hata düzeltmeleri sürüm 1.1](#BugFixesV1) daha fazla ayrıntı için.

Derleme hataları düzelttik sonra istiyorsanız son olarak, yeni işlevsellik tooyour uygulama tootake avantajlarından değişiklik yapabilirsiniz.

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a>Yeni sürüm 1.1 değişiklikler listesi
Merhaba aşağıdaki listede hello olasılığını tarafından hello değişiklik uygulama kodunuz etkileyecek sıralanır.

#### <a name="indexbatch-and-indexaction-changes"></a>IndexBatch ve IndexAction değişiklikleri
`IndexBatch.Create`çok adlandırıldı`IndexBatch.New` ve artık sahip bir `params` bağımsız değişkeni. Kullanabileceğiniz `IndexBatch.New` Eylemler (birleştirme, silme, vb.) farklı türlerde karışık toplu işlemler için. Ayrıca, toplu işleri oluşturmak için yeni statik yöntemler vardır burada tüm hello eylemleri olan hello aynı: `Delete`, `Merge`, `MergeOrUpload`, ve `Upload`.

`IndexAction`Genel oluşturucular artık sahiptir ve özelliklerini şimdi değişmez. Farklı amaçlar için Eylemler oluşturmak için hello yeni statik yöntemler kullanmalısınız: `Delete`, `Merge`, `MergeOrUpload`, ve `Upload`. `IndexAction.Create`kaldırılmıştır. Yalnızca bir belge alır hello aşırı kullanılan emin toouse olun `Upload` yerine.

##### <a name="example"></a>Örnek
Kodunuzu şöyle ise:

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

Toothis toofix değiştirmek herhangi bir derleme hataları:

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

İsterseniz, daha fazla toothis basitleştirebilirsiniz:

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a>IndexBatchException değişiklikleri
Merhaba `IndexBatchException.IndexResponse` özelliği çok adlandırılmıştır`IndexingResults`, ve türünü şimdi `IList<IndexingResult>`.

##### <a name="example"></a>Örnek
Kodunuzu şöyle ise:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

Toothis toofix değiştirmek herhangi bir derleme hataları:

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a>Operasyon yöntemi değişiklikleri
Her bir işlemde hello Azure Search .NET SDK'sı için zaman uyumlu ve zaman uyumsuz arayanlar yöntemi aşırı bir dizi açıktır. Merhaba imzalar ve bu yöntem aşırı Finansman değiştirdi. sürüm 1.1

Örneğin, bu imzaları hello "Dizin istatistikleri Al" işlemi hello SDK eski sürümlerinde sunulan:

İçinde `IIndexOperations`:

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

İçinde `IndexOperationsExtensions`:

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

Bu sürüm 1.1 görünümlü aynı işlemde Hello yöntemi imzaları hello:

İçinde `IIndexesOperations`:

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

İçinde `IndexesOperationsExtensions`:

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

Sürüm 1.1 ile başlayarak, hello Azure Search .NET SDK'sı farklı işlemi yöntemleri düzenler:

* Parametreleri bunun yerine varsayılan olarak, isteğe bağlı parametreler Modellenen artık ek yöntemi aşırı daha. Bu yöntemi aşırı yüklemelerinden hello sayısını bazen önemli ölçüde azaltır.
* Merhaba genişletme yöntemleri şimdi hello yabancı ayrıntılarının HTTP hello çağıran çok gizleyin. İşlem yöntemleri throw olduğundan SDK döndürülen yanıt nesnesi, genellikle bir HTTP durum kodu ile Merhaba eski sürümleri toocheck örneğin ihtiyacım kalmadı `CloudException` bir hata gösterir herhangi bir durum kodu için. Yeni Uzantı yöntemleri yalnızca dönüş model nesneleri Merhaba,, toounwrap sahip olmanın sorun hello kodunuzu bunları.
* Buna karşılık, hello çekirdek arabirimleri artık ihtiyacınız olursa hello HTTP düzeyinde daha fazla denetime yöntemleri kullanıma sunar. Özel HTTP üstbilgileri toobe istekleri ve yeni hello dahil şimdi geçirebilirsiniz `AzureOperationResponse<T>` türü doğrudan erişim toohello size dönüş `HttpRequestMessage` ve `HttpResponseMessage` hello işlemi için. `AzureOperationResponse`Hello tanımlanan `Microsoft.Rest.Azure` ad alanı ve değiştirir `Hyak.Common.OperationResponse`.

#### <a name="scoringparameters-changes"></a>ScoringParameters değişiklikleri
Adlı yeni bir sınıf `ScoringParameter` bırakıldı isteğe bağlı olarak hello son SDK toomake daha kolay tooprovide parametreleri tooscoring profillerinde arama sorgusu eklendi. Daha önce hello `ScoringProfiles` hello özelliğinin `SearchParameters` sınıfı olarak yazıldığından `IList<string>`; Olarak yazılan artık `IList<ScoringParameter>`.

##### <a name="example"></a>Örnek
Kodunuzu şöyle ise:

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

Toothis toofix değiştirmek herhangi bir derleme hataları: 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a>Model sınıfı değişiklikleri
Açıklanan toohello imza değişiklikler nedeniyle [işlemi yöntemi değişiklikleri](#OperationMethodChanges), birçok sınıflarda hello `Microsoft.Azure.Search.Models` ad alanı yeniden adlandırılmış veya kaldırılmış. Örneğin:

* `IndexDefinitionResponse`ile değiştirilmiştir`AzureOperationResponse<Index>`
* `DocumentSearchResponse`çok yeniden adlandırıldı`DocumentSearchResult`
* `IndexResult`çok yeniden adlandırıldı`IndexingResult`
* `Documents.Count()`Şimdi döndüren bir `long` ile Merhaba belge sayısı yerine bir`DocumentCountResponse`
* `IndexGetStatisticsResponse`çok yeniden adlandırıldı`IndexGetStatisticsResult`
* `IndexListResponse`çok yeniden adlandırıldı`IndexListResult`

toosummarize, `OperationResponse`-türetilmiş sınıfları yalnızca bir model nesnesi kaldırılmış toowrap vardı. Merhaba kalan sınıfları değiştirildi kendi soneki beklendiğinden `Response` çok`Result`.

##### <a name="example"></a>Örnek
Kodunuzu şöyle ise:

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

Toothis toofix değiştirmek herhangi bir derleme hataları:

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a>Yanıt sınıfları ve IEnumerable
Koleksiyonları tutun yanıt sınıfları artık uygulama kodunuz etkileyebilecek ek bir değişiklik olduğunu `IEnumerable<T>`. Bunun yerine, hello koleksiyon özelliği doğrudan erişebilirsiniz. Örneğin, kod aşağıdaki gibidir:

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

Toothis toofix değiştirmek herhangi bir derleme hataları:

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a>Web uygulamaları için özel durum
Serileştiren bir web uygulaması varsa `DocumentSearchResponse` toohello tarayıcı toosend arama sonuçları doğrudan kodunuzu toochange gerekir veya hello sonuçları değil seri doğru. Örneğin, kod aşağıdaki gibidir:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

Merhaba alarak değiştirebilirsiniz `.Results` hello arama yanıt toofix arama sonucu işleme özelliği:

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

Bu gibi durumlarda toolook kendiniz bir kodunuzda olur; **hello derleyici değil sizi uyaracaktır** çünkü `JsonResult.Data` türü `object`.

#### <a name="cloudexception-changes"></a>CloudException değişiklikleri
Merhaba `CloudException` sınıfı hello taşımıştır `Hyak.Common` ad alanı toohello `Microsoft.Rest.Azure` ad alanı. Ayrıca, kendi `Error` özelliği çok adlandırılmıştır`Body`.

#### <a name="searchserviceclient-and-searchindexclient-changes"></a>SearchServiceClient ve Searchındexclient değişiklikleri
Merhaba hello türünü `Credentials` özelliği değiştiğini `SearchCredentials` tooits temel sınıfı, `ServiceClientCredentials`. Tooaccess hello gerekiyorsa `SearchCredentials` , bir `SearchIndexClient` veya `SearchServiceClient`, lütfen hello yeni kullanın `SearchCredentials` özelliği.

Merhaba SDK, eski sürümlerinde `SearchServiceClient` ve `SearchIndexClient` sürdü oluşturucular sahip bir `HttpClient` parametresi. Bu alan Oluşturucuları ile değiştirilmiştir bir `HttpClientHandler` ve bir dizi `DelegatingHandler` nesneleri. Bu, daha kolay tooinstall özel işleyicileri toopre-HTTP isteklerini işleyen gerekirse kolaylaştırır.

Son olarak, sürdü oluşturucular hello bir `Uri` ve `SearchCredentials` değiştirilmiştir. Örneğin, şöyle bir kodunuz varsa:

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

Toothis toofix değiştirmek herhangi bir derleme hataları:

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

Ayrıca hello hello tür parametresi kimlik bilgilerini not çok değişti`ServiceClientCredentials`. Bu olası tooaffect bu yana kodunuz: `SearchCredentials` türetildiği `ServiceClientCredentials`.

#### <a name="passing-a-request-id"></a>İstek Kimliği geçirme
Merhaba SDK eski sürümleri, bir istek kimliği üzerinde hello ayarlayabilirsiniz `SearchServiceClient` veya `SearchIndexClient` ve her isteği toohello REST API dahil edilmesi. Bu, toocontact destek gerekiyorsa arama hizmetinizi sorunlarını gidermek için kullanışlıdır. Ancak, tüm işlemleri için aynı kimliği toouse hello yerine her işlem için daha kullanışlı tooset benzersiz istek kimliği gerekir. Bu nedenle, hello `SetClientRequestId` yöntemlerinin `SearchServiceClient` ve `SearchIndexClient` kaldırıldı. Bunun yerine, bir istek kimliği tooeach işlemi yöntemi hello isteğe bağlı geçirebilirsiniz `SearchRequestOptions` parametresi.

> [!NOTE]
> Gelecekteki bir hello SDK sürümünde, diğer Azure SDK tarafından kullanılan hello yaklaşım ile tutarlı olan bir istek kimliği nesneler genel hello istemcide ayarlamak için yeni bir yöntem ekleyeceğiz.
> 
> 

#### <a name="example"></a>Örnek
Şuna benzer bir kod varsa:

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

Toothis toofix değiştirmek herhangi bir derleme hataları:

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a>Arabirim adı değişikliği
Merhaba işlemi Grup arabirimi adları tüm değiştirilen toobe karşılık gelen özellik adları ile tutarlı vardır:

* Merhaba türü `ISearchServiceClient.Indexes` adlandırılmıştır `IIndexOperations` çok`IIndexesOperations`.
* Merhaba türü `ISearchServiceClient.Indexers` adlandırılmıştır `IIndexerOperations` çok`IIndexersOperations`.
* Merhaba türü `ISearchServiceClient.DataSources` adlandırılmıştır `IDataSourceOperations` çok`IDataSourcesOperations`.
* Merhaba türü `ISearchIndexClient.Documents` adlandırılmıştır `IDocumentOperations` çok`IDocumentsOperations`.

Bu değişiklik, test amacıyla bu arabirimleri mocks oluşturduğunuz sürece olası tooaffect kodunuz:.

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a>Hata düzeltmeleri sürüm 1.1
Hello Azure Search .NET SDK'sı ile ilgili tooserialization özel model sınıfların eski sürümleri bir hata oluştu. bir null değer türünde bir özelliği bir özel model sınıfı oluşturduysanız hello hata oluşabilir.

#### <a name="steps-tooreproduce"></a>Adımları tooreproduce
Bir özel model sınıfı null değer türünde bir özellik oluşturun. Örneğin, bir ortak ekleyin `UnitCount` türündeki özelliği `int` yerine `int?`.

Bu tür hello varsayılan değere sahip bir belge sıralıyorsanız (örneğin, 0 `int`), hello alan Azure Search'te boş olacaktır. Daha sonra bu belge için arama yaparsanız hello `Search` çağrısı throw `JsonSerializationException` , onu dönüştürülemiyor şikayetçi `null` çok`int`.

Ayrıca, filtreleri null toohello dizin hedeflenen hello değeri yerine yazıldı beri beklendiği gibi çalışmayabilir.

#### <a name="fix-details"></a>Ayrıntılar Düzelt
Sürüm hello SDK 1.1 Biz bu sorunu düzelttik. Şimdi, böyle bir model sınıfı varsa:

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

ve ayarladığınız `IntValue` değer artık doğru hello kablo 0 olarak serileştirilmiş ve hello dizin 0 olarak depolanan olduğunu too0. Yuvarlak tripping de beklendiği gibi çalışır.

Olası bir sorunu toobe Bu yaklaşımda farkında: atanamayan bir özellik ile bir model türünü kullanan çok varsa**garanti** hiçbir belgeleri dizininize hello karşılık gelen alan için bir null değer içeriyor. Merhaba SDK ne hello Azure Search REST API'si, tooenforce bu yardımcı olur.

Bu yalnızca kuramsal bir sorun değildir: türü olan yeni bir alan tooan mevcut dizin eklediğiniz bir senaryoyu düşünün `Edm.Int32`. (Tüm türleri Azure Search'te boş değer atanabilir olmasıdır) hello dizin tanımını güncelleştirdikten sonra bu yeni alan için bir null değer tüm belgeler olacaktır. Ardından bir model sınıfı bir null ile kullanırsanız `int` özelliği bu alan için elde edersiniz bir `JsonSerializationException` şöyle tooretrieve belgeleri çalışırken:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Bu nedenle, hala bir en iyi uygulama olarak model sınıflarınızda boş değer atanabilir türler kullanmanızı öneririz.

Bu hatayı ve hello düzeltme hakkında daha fazla ayrıntı için lütfen bkz. [github'daki bu sorunu](https://github.com/Azure/azure-sdk-for-net/issues/1063).

