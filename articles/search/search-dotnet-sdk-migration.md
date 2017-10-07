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
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a><span data-ttu-id="31ae3-103">Azure Search .NET SDK sürüm 3 toohello yükseltme</span><span class="sxs-lookup"><span data-stu-id="31ae3-103">Upgrading toohello Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="31ae3-104">2.0-Önizleme veya Merhaba, daha eski bir sürümü kullanıyorsanız [Azure Search .NET SDK'sı](https://aka.ms/search-sdk), bu makalede, uygulama toouse sürüm 3 yükseltmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="31ae3-104">If you're using version 2.0-preview or older of hello [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application toouse version 3.</span></span>

<span data-ttu-id="31ae3-105">Merhaba SDK daha genel bir kılavuz için de dahil olmak üzere örneklere bakın [toouse Azure arama nasıl bir .NET uygulamasından](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="31ae3-105">For a more general walkthrough of hello SDK including examples, see [How toouse Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="31ae3-106">Hello Azure Search .NET SDK 3 sürümünü önceki sürümlerinden bazı değişiklikler içerir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-106">Version 3 of hello Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="31ae3-107">Kodunuzu değiştirmeden yalnızca en az çaba gerektirmelidir şekilde çoğunlukla ikincil, bunlar.</span><span class="sxs-lookup"><span data-stu-id="31ae3-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="31ae3-108">Bkz: [adımları tooupgrade](#UpgradeSteps) yönelik yönergeler toochange, kod toouse hello yeni SDK sürümü.</span><span class="sxs-lookup"><span data-stu-id="31ae3-108">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="31ae3-109">Sürüm 1.0.2-preview kullanıyorsanız veya daha eski, tooversion 1.1 yükseltmeniz ve ardından tooversion 3 yükseltmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-109">If you're using version 1.0.2-preview or older, you should upgrade tooversion 1.1 first, and then upgrade tooversion 3.</span></span> <span data-ttu-id="31ae3-110">Bkz: [ek: adımları tooupgrade tooversion 1.1](#UpgradeStepsV1) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="31ae3-110">See [Appendix: Steps tooupgrade tooversion 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="31ae3-111">Azure Search Hizmeti örneğinizi hello en son dahil olmak üzere birkaç REST API sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="31ae3-111">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="31ae3-112">En son Merhaba, ancak, kod toouse hello en yeni sürüme geçirmek öneririz artık olduğunda toouse bir sürüm devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31ae3-112">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span> <span data-ttu-id="31ae3-113">Merhaba REST API kullanırken, her istek hello api-version parametresi aracılığıyla hello API sürümü belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-113">When using hello REST API, you must specify hello API version in every request via hello api-version parameter.</span></span> <span data-ttu-id="31ae3-114">Merhaba .NET SDK kullanarak olduğunda hello hello kullanmakta olduğunuz SDK sürümü hello ilgili hello REST API sürümü belirler.</span><span class="sxs-lookup"><span data-stu-id="31ae3-114">When using hello .NET SDK, hello version of hello SDK you’re using determines hello corresponding version of hello REST API.</span></span> <span data-ttu-id="31ae3-115">Eski bir SDK kullanıyorsanız, hello hizmet yükseltilmiş toosupport daha yeni bir API sürümü olsa bile, hiçbir değişiklik kodla toorun devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31ae3-115">If you are using an older SDK, you can continue toorun that code with no changes even if hello service is upgraded toosupport a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="31ae3-116">Sürüm 3 yenilikler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="31ae3-116">What's new in version 3</span></span>
<span data-ttu-id="31ae3-117">Hello Azure Search .NET SDK'sı hedefleri hello son 3 sürümünü hello Azure Search REST API'si, özellikle 2016-09-01 genel olarak kullanılabilir sürümü.</span><span class="sxs-lookup"><span data-stu-id="31ae3-117">Version 3 of hello Azure Search .NET SDK targets hello latest generally available version of hello Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="31ae3-118">Bu, olası toouse kolaylaştırır hello aşağıdakiler dahil, bir .NET uygulamasından Azure Search'ün birçok yeni özellik:</span><span class="sxs-lookup"><span data-stu-id="31ae3-118">This makes it possible toouse many new features of Azure Search from a .NET application, including hello following:</span></span>

* [<span data-ttu-id="31ae3-119">Özel çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="31ae3-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="31ae3-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) ve [Azure Table Storage](search-howto-indexing-azure-tables.md) dizin oluşturucu desteği</span><span class="sxs-lookup"><span data-stu-id="31ae3-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="31ae3-121">Dizin Oluşturucu özelleştirme aracılığıyla [alan eşlemeleri](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="31ae3-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="31ae3-122">Etag'ler tooenable güvenli eşzamanlı dizin tanımları, dizin oluşturucular ve veri kaynaklarını güncelleştirme desteği</span><span class="sxs-lookup"><span data-stu-id="31ae3-122">ETags support tooenable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="31ae3-123">Dizin alan tanımları bildirimli olarak model sınıfınız dekorasyon ve hello kullanarak yeni oluşturmak için destek `FieldBuilder` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="31ae3-123">Support for building index field definitions declaratively by decorating your model class and using hello new `FieldBuilder` class.</span></span>
* <span data-ttu-id="31ae3-124">.NET Core ve .NET taşınabilir profil 111 desteği</span><span class="sxs-lookup"><span data-stu-id="31ae3-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="31ae3-125">Adımları tooupgrade</span><span class="sxs-lookup"><span data-stu-id="31ae3-125">Steps tooupgrade</span></span>
<span data-ttu-id="31ae3-126">İlk olarak, NuGet başvuru için güncelleştirme `Microsoft.Azure.Search` ya da hello NuGet Paket Yöneticisi konsolu kullanılarak veya göre proje başvuruları sağ tıklayıp Visual Studio'da "NuGet paketleri...'ı Yönet" seçerek.</span><span class="sxs-lookup"><span data-stu-id="31ae3-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="31ae3-127">NuGet hello yeni paketleri ve bunların bağımlılıklarını indirdikten sonra projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="31ae3-127">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="31ae3-128">Kodunuzu nasıl yapılandırıldığını bağlı olarak başarılı bir şekilde yeniden oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="31ae3-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="31ae3-129">Bu durumda, hazır toogo dileriz!</span><span class="sxs-lookup"><span data-stu-id="31ae3-129">If so, you're ready toogo!</span></span>

<span data-ttu-id="31ae3-130">Derleme başarısız olursa, bir derleme hatası hello aşağıdaki gibi görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="31ae3-130">If your build fails, you should see a build error like hello following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="31ae3-131">Merhaba sonraki adıma toofix bu yapı hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="31ae3-131">hello next step is toofix this build error.</span></span> <span data-ttu-id="31ae3-132">Bkz: [önemli değişiklikler sürüm 3](#ListOfChanges) ne hello hatasına neden oluyor ile ilgili ayrıntılar için ve nasıl toofix onu.</span><span class="sxs-lookup"><span data-stu-id="31ae3-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes hello error and how toofix it.</span></span>

<span data-ttu-id="31ae3-133">Ek yapı görebilirsiniz uyarılarla ilgili tooobsolete yöntemleri veya özellikleri.</span><span class="sxs-lookup"><span data-stu-id="31ae3-133">You may see additional build warnings related tooobsolete methods or properties.</span></span> <span data-ttu-id="31ae3-134">Merhaba uyarıları ne toouse, Merhaba bunun yerine özelliği kullanım dışı. ilgili yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-134">hello warnings will include instructions on what toouse instead of hello deprecated feature.</span></span> <span data-ttu-id="31ae3-135">Örneğin, uygulamanız hello kullanıyorsa `IndexingParameters.Base64EncodeKeys` özelliği bildiren bir uyarı almak`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="31ae3-135">For example, if your application uses hello `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="31ae3-136">Derleme hataları düzelttik sonra isterseniz tooyour uygulama tootake yeni işlevsellik avantajlarından değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31ae3-136">Once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span> <span data-ttu-id="31ae3-137">Merhaba SDK yeni özellikleri ayrıntılı olarak [sürüm 3 yenilikler](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="31ae3-137">New features in hello SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="31ae3-138">Sürüm 3'de yeni değişiklikler</span><span class="sxs-lookup"><span data-stu-id="31ae3-138">Breaking changes in version 3</span></span>
<span data-ttu-id="31ae3-139">Var. kod gerektirebilecek önemli değişiklikler 3 sürümündeki az sayıda ek olarak, uygulamanızın toorebuilding değiştirir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-139">There a small number of breaking changes in version 3 that may require code changes in addition toorebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="31ae3-140">Indexes.GetClient dönüş türü</span><span class="sxs-lookup"><span data-stu-id="31ae3-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="31ae3-141">Merhaba `Indexes.GetClient` yöntemi yeni bir dönüş türüne sahip.</span><span class="sxs-lookup"><span data-stu-id="31ae3-141">hello `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="31ae3-142">Daha önce döndürülen `SearchIndexClient`, ancak bu çok değiştirildi`ISearchIndexClient` sürüm 2.0-Önizleme ve bu değişiklik 3 tooversion yürütür.</span><span class="sxs-lookup"><span data-stu-id="31ae3-142">Previously, it returned `SearchIndexClient`, but this was changed too`ISearchIndexClient` in version 2.0-preview, and that change carries over tooversion 3.</span></span> <span data-ttu-id="31ae3-143">Bu toomock hello istiyor toosupport müşterileri içindir `GetClient` yöntemi, sahte bir uygulama döndürerek birim testleri için `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-143">This is toosupport customers that wish toomock hello `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="31ae3-144">Örnek</span><span class="sxs-lookup"><span data-stu-id="31ae3-144">Example</span></span>
<span data-ttu-id="31ae3-145">Kodunuzu şöyle ise:</span><span class="sxs-lookup"><span data-stu-id="31ae3-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="31ae3-146">Toothis toofix değiştirmek herhangi bir derleme hataları:</span><span class="sxs-lookup"><span data-stu-id="31ae3-146">You can change it toothis toofix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a><span data-ttu-id="31ae3-147">Örtük olarak dönüştürülebilir toostrings AnalyzerName, veri türü ve diğerleri artık olmayan</span><span class="sxs-lookup"><span data-stu-id="31ae3-147">AnalyzerName, DataType, and others are no longer implicitly convertible toostrings</span></span>
<span data-ttu-id="31ae3-148">Hello Azure Search .NET SDK'sı, türetilen birçok türlerinde vardır `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-148">There are many types in hello Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="31ae3-149">Daha önce bu türleri tüm dolaylı olarak dönüştürülebilir tootype olan `string`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-149">Previously these types were all implicitly convertible tootype `string`.</span></span> <span data-ttu-id="31ae3-150">Ancak, bir hata hello bulunan `Object.Equals` uygulaması bu sınıfları ve bu örtük dönüştürme devre dışı bırakılması gereken giderilmesi hello hata.</span><span class="sxs-lookup"><span data-stu-id="31ae3-150">However, a bug was discovered in hello `Object.Equals` implementation for these classes, and fixing hello bug required disabling this implicit conversion.</span></span> <span data-ttu-id="31ae3-151">Açık dönüşüm çok`string` hala izin verilir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-151">Explicit conversion too`string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="31ae3-152">Örnek</span><span class="sxs-lookup"><span data-stu-id="31ae3-152">Example</span></span>
<span data-ttu-id="31ae3-153">Kodunuzu şöyle ise:</span><span class="sxs-lookup"><span data-stu-id="31ae3-153">If your code looks like this:</span></span>

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

<span data-ttu-id="31ae3-154">Toothis toofix değiştirmek herhangi bir derleme hataları:</span><span class="sxs-lookup"><span data-stu-id="31ae3-154">You can change it toothis toofix any build errors:</span></span>

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

### <a name="removed-obsolete-members"></a><span data-ttu-id="31ae3-155">Eski üyeler kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="31ae3-155">Removed obsolete members</span></span>

<span data-ttu-id="31ae3-156">Derleme hataları ilgili toomethods veya sürüm 2.0-Önizleme'te eski olarak işaretlenen ve daha sonra sürüm 3 kaldırılan özellikler görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31ae3-156">You may see build errors related toomethods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="31ae3-157">Bu tür hatalarla karşılaşırsanız, işte nasıl tooresolve bunları:</span><span class="sxs-lookup"><span data-stu-id="31ae3-157">If you encounter such errors, here is how tooresolve them:</span></span>

- <span data-ttu-id="31ae3-158">Bu oluşturucu kullanıyorsanız: `ScoringParameter(string name, string value)`, bunun yerine bunu kullanın:`ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="31ae3-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="31ae3-159">Merhaba kullanıyorsanız `ScoringParameter.Value` özelliği, kullanım hello `ScoringParameter.Values` özelliği veya hello `ToString` yöntemi yerine.</span><span class="sxs-lookup"><span data-stu-id="31ae3-159">If you were using hello `ScoringParameter.Value` property, use hello `ScoringParameter.Values` property or hello `ToString` method instead.</span></span>
- <span data-ttu-id="31ae3-160">Merhaba kullanıyorsanız `SearchRequestOptions.RequestId` özelliği, kullanım hello `ClientRequestId` özelliği yerine.</span><span class="sxs-lookup"><span data-stu-id="31ae3-160">If you were using hello `SearchRequestOptions.RequestId` property, use hello `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="31ae3-161">Kaldırılan Önizleme özellikleri</span><span class="sxs-lookup"><span data-stu-id="31ae3-161">Removed preview features</span></span>

<span data-ttu-id="31ae3-162">Sürüm 2.0-Önizleme tooversion 3 ' yükseltiyorsanız, JSON ve Blob dizin oluşturucular için destek ayrıştırma CSV kaldırıldı, bu özellikler hala önizlemede olduğundan unutmayın.</span><span class="sxs-lookup"><span data-stu-id="31ae3-162">If you are upgrading from version 2.0-preview tooversion 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="31ae3-163">Özellikle, hello yöntemlerinin aşağıdaki hello `IndexingParametersExtensions` sınıfı kaldırıldı:</span><span class="sxs-lookup"><span data-stu-id="31ae3-163">Specifically, hello following methods of hello `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="31ae3-164">Uygulamanız bu özelliklere sıkı bir bağımlılık varsa, hello Azure Search .NET SDK'sı, mümkün tooupgrade tooversion 3 olmaz.</span><span class="sxs-lookup"><span data-stu-id="31ae3-164">If your application has a hard dependency on these features, you will not be able tooupgrade tooversion 3 of hello Azure Search .NET SDK.</span></span> <span data-ttu-id="31ae3-165">Toouse sürüm 2.0-Önizleme devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31ae3-165">You can continue toouse version 2.0-preview.</span></span> <span data-ttu-id="31ae3-166">Bununla birlikte, lütfen aklınızda **üretim uygulamaları SDK'ları önizlemede kullanmanızı önermiyoruz**.</span><span class="sxs-lookup"><span data-stu-id="31ae3-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="31ae3-167">Önizleme özellikleri yalnızca değerlendirme ve değişiklik.</span><span class="sxs-lookup"><span data-stu-id="31ae3-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="31ae3-168">Sonuç</span><span class="sxs-lookup"><span data-stu-id="31ae3-168">Conclusion</span></span>
<span data-ttu-id="31ae3-169">Hello Azure Search .NET SDK'sını kullanma hakkında daha fazla ayrıntı gereksinim duyarsanız, yeni güncelleştirilen bakın [nasıl yapılır](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="31ae3-169">If you need more details on using hello Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="31ae3-170">SDK hello üzerinde bildiriminiz bizim.</span><span class="sxs-lookup"><span data-stu-id="31ae3-170">We welcome your feedback on hello SDK.</span></span> <span data-ttu-id="31ae3-171">Sorunlarla karşılaşırsanız, ücretsiz tooask bize hello hakkında Yardım için eşitleyerek [Azure arama MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="31ae3-171">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="31ae3-172">Bir hata bulursanız, hello sorunu dosya [Azure .NET SDK GitHub deposunu](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="31ae3-172">If you find a bug, you can file an issue in hello [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="31ae3-173">Sorunu başlıkla emin tooprefix olun "arama SDK:".</span><span class="sxs-lookup"><span data-stu-id="31ae3-173">Make sure tooprefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="31ae3-174">Azure Search kullandığınız için teşekkür ederiz!</span><span class="sxs-lookup"><span data-stu-id="31ae3-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a><span data-ttu-id="31ae3-175">Ek: Adımları tooupgrade tooversion 1.1</span><span class="sxs-lookup"><span data-stu-id="31ae3-175">Appendix: Steps tooupgrade tooversion 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="31ae3-176">Bu bölüm, yalnızca toousers hello Azure Search .NET SDK sürüm 1.0.2-preview ve eski geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-176">This section applies only toousers of hello Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="31ae3-177">İlk olarak, NuGet başvuru için güncelleştirme `Microsoft.Azure.Search` ya da hello NuGet Paket Yöneticisi konsolu kullanılarak veya göre proje başvuruları sağ tıklayıp Visual Studio'da "NuGet paketleri...'ı Yönet" seçerek.</span><span class="sxs-lookup"><span data-stu-id="31ae3-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="31ae3-178">NuGet hello yeni paketleri ve bunların bağımlılıklarını indirdikten sonra projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="31ae3-178">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="31ae3-179">Varsa, daha önce sürüm 1.0.0-preview, 1.0.1-preview veya 1.0.2-preview, hello yapı kullanarak başarılı olması gerekir ve hazır toogo demektir!</span><span class="sxs-lookup"><span data-stu-id="31ae3-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, hello build should succeed and you're ready toogo!</span></span>

<span data-ttu-id="31ae3-180">Daha önce sürüm 0.13.0-preview kullanıyorsanız veya daha eski, görmeniz gerekir derleme hataları hello aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="31ae3-180">If you were previously using version 0.13.0-preview or older, you should see build errors like hello following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="31ae3-181">Merhaba sonraki toofix hello derleme hataları tek tek bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="31ae3-181">hello next step is toofix hello build errors one by one.</span></span> <span data-ttu-id="31ae3-182">Çoğu hello SDK yeniden adlandırıldığı bazı sınıfı ve yöntemi adlarını değiştirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-182">Most will require changing some class and method names that have been renamed in hello SDK.</span></span> <span data-ttu-id="31ae3-183">[Yeni sürüm 1.1 değişiklikler listesi](#ListOfChangesV1) adı değişikliklerin listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="31ae3-184">Belgelerinizi özel sınıflar toomodel kullanıyorsanız ve bu sınıfların null ilkel türler özelliklerini varsa (örneğin, `int` veya `bool` C#), hello 1.1 hangisinin olmanız gerekir kullanan hello SDK sürümünde hata düzeltmesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="31ae3-184">If you're using custom classes toomodel your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in hello 1.1 version of hello SDK of which you should be aware.</span></span> <span data-ttu-id="31ae3-185">Bkz: [hata düzeltmeleri sürüm 1.1](#BugFixesV1) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="31ae3-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="31ae3-186">Derleme hataları düzelttik sonra istiyorsanız son olarak, yeni işlevsellik tooyour uygulama tootake avantajlarından değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31ae3-186">Finally, once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="31ae3-187">Yeni sürüm 1.1 değişiklikler listesi</span><span class="sxs-lookup"><span data-stu-id="31ae3-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="31ae3-188">Merhaba aşağıdaki listede hello olasılığını tarafından hello değişiklik uygulama kodunuz etkileyecek sıralanır.</span><span class="sxs-lookup"><span data-stu-id="31ae3-188">hello following list is ordered by hello likelihood that hello change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="31ae3-189">IndexBatch ve IndexAction değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="31ae3-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="31ae3-190">`IndexBatch.Create`çok adlandırıldı`IndexBatch.New` ve artık sahip bir `params` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="31ae3-190">`IndexBatch.Create` has been renamed too`IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="31ae3-191">Kullanabileceğiniz `IndexBatch.New` Eylemler (birleştirme, silme, vb.) farklı türlerde karışık toplu işlemler için.</span><span class="sxs-lookup"><span data-stu-id="31ae3-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="31ae3-192">Ayrıca, toplu işleri oluşturmak için yeni statik yöntemler vardır burada tüm hello eylemleri olan hello aynı: `Delete`, `Merge`, `MergeOrUpload`, ve `Upload`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-192">In addition, there are new static methods for creating batches where all hello actions are hello same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="31ae3-193">`IndexAction`Genel oluşturucular artık sahiptir ve özelliklerini şimdi değişmez.</span><span class="sxs-lookup"><span data-stu-id="31ae3-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="31ae3-194">Farklı amaçlar için Eylemler oluşturmak için hello yeni statik yöntemler kullanmalısınız: `Delete`, `Merge`, `MergeOrUpload`, ve `Upload`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-194">You should use hello new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="31ae3-195">`IndexAction.Create`kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="31ae3-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="31ae3-196">Yalnızca bir belge alır hello aşırı kullanılan emin toouse olun `Upload` yerine.</span><span class="sxs-lookup"><span data-stu-id="31ae3-196">If you used hello overload that takes only a document, make sure toouse `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="31ae3-197">Örnek</span><span class="sxs-lookup"><span data-stu-id="31ae3-197">Example</span></span>
<span data-ttu-id="31ae3-198">Kodunuzu şöyle ise:</span><span class="sxs-lookup"><span data-stu-id="31ae3-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="31ae3-199">Toothis toofix değiştirmek herhangi bir derleme hataları:</span><span class="sxs-lookup"><span data-stu-id="31ae3-199">You can change it toothis toofix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="31ae3-200">İsterseniz, daha fazla toothis basitleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="31ae3-200">If you want, you can further simplify it toothis:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="31ae3-201">IndexBatchException değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="31ae3-201">IndexBatchException changes</span></span>
<span data-ttu-id="31ae3-202">Merhaba `IndexBatchException.IndexResponse` özelliği çok adlandırılmıştır`IndexingResults`, ve türünü şimdi `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-202">hello `IndexBatchException.IndexResponse` property has been renamed too`IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="31ae3-203">Örnek</span><span class="sxs-lookup"><span data-stu-id="31ae3-203">Example</span></span>
<span data-ttu-id="31ae3-204">Kodunuzu şöyle ise:</span><span class="sxs-lookup"><span data-stu-id="31ae3-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="31ae3-205">Toothis toofix değiştirmek herhangi bir derleme hataları:</span><span class="sxs-lookup"><span data-stu-id="31ae3-205">You can change it toothis toofix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="31ae3-206">Operasyon yöntemi değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="31ae3-206">Operation method changes</span></span>
<span data-ttu-id="31ae3-207">Her bir işlemde hello Azure Search .NET SDK'sı için zaman uyumlu ve zaman uyumsuz arayanlar yöntemi aşırı bir dizi açıktır.</span><span class="sxs-lookup"><span data-stu-id="31ae3-207">Each operation in hello Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="31ae3-208">Merhaba imzalar ve bu yöntem aşırı Finansman değiştirdi. sürüm 1.1</span><span class="sxs-lookup"><span data-stu-id="31ae3-208">hello signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="31ae3-209">Örneğin, bu imzaları hello "Dizin istatistikleri Al" işlemi hello SDK eski sürümlerinde sunulan:</span><span class="sxs-lookup"><span data-stu-id="31ae3-209">For example, hello "Get Index Statistics" operation in older versions of hello SDK exposed these signatures:</span></span>

<span data-ttu-id="31ae3-210">İçinde `IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="31ae3-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="31ae3-211">İçinde `IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="31ae3-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="31ae3-212">Bu sürüm 1.1 görünümlü aynı işlemde Hello yöntemi imzaları hello:</span><span class="sxs-lookup"><span data-stu-id="31ae3-212">hello method signatures for hello same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="31ae3-213">İçinde `IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="31ae3-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="31ae3-214">İçinde `IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="31ae3-214">In `IndexesOperationsExtensions`:</span></span>

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

<span data-ttu-id="31ae3-215">Sürüm 1.1 ile başlayarak, hello Azure Search .NET SDK'sı farklı işlemi yöntemleri düzenler:</span><span class="sxs-lookup"><span data-stu-id="31ae3-215">Starting with version 1.1, hello Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="31ae3-216">Parametreleri bunun yerine varsayılan olarak, isteğe bağlı parametreler Modellenen artık ek yöntemi aşırı daha.</span><span class="sxs-lookup"><span data-stu-id="31ae3-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="31ae3-217">Bu yöntemi aşırı yüklemelerinden hello sayısını bazen önemli ölçüde azaltır.</span><span class="sxs-lookup"><span data-stu-id="31ae3-217">This reduces hello number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="31ae3-218">Merhaba genişletme yöntemleri şimdi hello yabancı ayrıntılarının HTTP hello çağıran çok gizleyin.</span><span class="sxs-lookup"><span data-stu-id="31ae3-218">hello extension methods now hide a lot of hello extraneous details of HTTP from hello caller.</span></span> <span data-ttu-id="31ae3-219">İşlem yöntemleri throw olduğundan SDK döndürülen yanıt nesnesi, genellikle bir HTTP durum kodu ile Merhaba eski sürümleri toocheck örneğin ihtiyacım kalmadı `CloudException` bir hata gösterir herhangi bir durum kodu için.</span><span class="sxs-lookup"><span data-stu-id="31ae3-219">For example, older versions of hello SDK returned a response object with an HTTP status code, which you often didn't need toocheck because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="31ae3-220">Yeni Uzantı yöntemleri yalnızca dönüş model nesneleri Merhaba,, toounwrap sahip olmanın sorun hello kodunuzu bunları.</span><span class="sxs-lookup"><span data-stu-id="31ae3-220">hello new extension methods just return model objects, saving you hello trouble of having toounwrap them in your code.</span></span>
* <span data-ttu-id="31ae3-221">Buna karşılık, hello çekirdek arabirimleri artık ihtiyacınız olursa hello HTTP düzeyinde daha fazla denetime yöntemleri kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="31ae3-221">Conversely, hello core interfaces now expose methods that give you more control at hello HTTP level if you need it.</span></span> <span data-ttu-id="31ae3-222">Özel HTTP üstbilgileri toobe istekleri ve yeni hello dahil şimdi geçirebilirsiniz `AzureOperationResponse<T>` türü doğrudan erişim toohello size dönüş `HttpRequestMessage` ve `HttpResponseMessage` hello işlemi için.</span><span class="sxs-lookup"><span data-stu-id="31ae3-222">You can now pass in custom HTTP headers toobe included in requests, and hello new `AzureOperationResponse<T>` return type gives you direct access toohello `HttpRequestMessage` and `HttpResponseMessage` for hello operation.</span></span> <span data-ttu-id="31ae3-223">`AzureOperationResponse`Hello tanımlanan `Microsoft.Rest.Azure` ad alanı ve değiştirir `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-223">`AzureOperationResponse` is defined in hello `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="31ae3-224">ScoringParameters değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="31ae3-224">ScoringParameters changes</span></span>
<span data-ttu-id="31ae3-225">Adlı yeni bir sınıf `ScoringParameter` bırakıldı isteğe bağlı olarak hello son SDK toomake daha kolay tooprovide parametreleri tooscoring profillerinde arama sorgusu eklendi.</span><span class="sxs-lookup"><span data-stu-id="31ae3-225">A new class named `ScoringParameter` has been added in hello latest SDK toomake it easier tooprovide parameters tooscoring profiles in a search query.</span></span> <span data-ttu-id="31ae3-226">Daha önce hello `ScoringProfiles` hello özelliğinin `SearchParameters` sınıfı olarak yazıldığından `IList<string>`; Olarak yazılan artık `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-226">Previously hello `ScoringProfiles` property of hello `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="31ae3-227">Örnek</span><span class="sxs-lookup"><span data-stu-id="31ae3-227">Example</span></span>
<span data-ttu-id="31ae3-228">Kodunuzu şöyle ise:</span><span class="sxs-lookup"><span data-stu-id="31ae3-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="31ae3-229">Toothis toofix değiştirmek herhangi bir derleme hataları:</span><span class="sxs-lookup"><span data-stu-id="31ae3-229">You can change it toothis toofix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="31ae3-230">Model sınıfı değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="31ae3-230">Model class changes</span></span>
<span data-ttu-id="31ae3-231">Açıklanan toohello imza değişiklikler nedeniyle [işlemi yöntemi değişiklikleri](#OperationMethodChanges), birçok sınıflarda hello `Microsoft.Azure.Search.Models` ad alanı yeniden adlandırılmış veya kaldırılmış.</span><span class="sxs-lookup"><span data-stu-id="31ae3-231">Due toohello signature changes described in [Operation method changes](#OperationMethodChanges), many classes in hello `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="31ae3-232">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="31ae3-232">For example:</span></span>

* <span data-ttu-id="31ae3-233">`IndexDefinitionResponse`ile değiştirilmiştir`AzureOperationResponse<Index>`</span><span class="sxs-lookup"><span data-stu-id="31ae3-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="31ae3-234">`DocumentSearchResponse`çok yeniden adlandırıldı`DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="31ae3-234">`DocumentSearchResponse` has been renamed too`DocumentSearchResult`</span></span>
* <span data-ttu-id="31ae3-235">`IndexResult`çok yeniden adlandırıldı`IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="31ae3-235">`IndexResult` has been renamed too`IndexingResult`</span></span>
* <span data-ttu-id="31ae3-236">`Documents.Count()`Şimdi döndüren bir `long` ile Merhaba belge sayısı yerine bir`DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="31ae3-236">`Documents.Count()` now returns a `long` with hello document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="31ae3-237">`IndexGetStatisticsResponse`çok yeniden adlandırıldı`IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="31ae3-237">`IndexGetStatisticsResponse` has been renamed too`IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="31ae3-238">`IndexListResponse`çok yeniden adlandırıldı`IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="31ae3-238">`IndexListResponse` has been renamed too`IndexListResult`</span></span>

<span data-ttu-id="31ae3-239">toosummarize, `OperationResponse`-türetilmiş sınıfları yalnızca bir model nesnesi kaldırılmış toowrap vardı.</span><span class="sxs-lookup"><span data-stu-id="31ae3-239">toosummarize, `OperationResponse`-derived classes that existed only toowrap a model object have been removed.</span></span> <span data-ttu-id="31ae3-240">Merhaba kalan sınıfları değiştirildi kendi soneki beklendiğinden `Response` çok`Result`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-240">hello remaining classes have had their suffix changed from `Response` too`Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="31ae3-241">Örnek</span><span class="sxs-lookup"><span data-stu-id="31ae3-241">Example</span></span>
<span data-ttu-id="31ae3-242">Kodunuzu şöyle ise:</span><span class="sxs-lookup"><span data-stu-id="31ae3-242">If your code looks like this:</span></span>

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

<span data-ttu-id="31ae3-243">Toothis toofix değiştirmek herhangi bir derleme hataları:</span><span class="sxs-lookup"><span data-stu-id="31ae3-243">You can change it toothis toofix any build errors:</span></span>

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

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="31ae3-244">Yanıt sınıfları ve IEnumerable</span><span class="sxs-lookup"><span data-stu-id="31ae3-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="31ae3-245">Koleksiyonları tutun yanıt sınıfları artık uygulama kodunuz etkileyebilecek ek bir değişiklik olduğunu `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="31ae3-246">Bunun yerine, hello koleksiyon özelliği doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31ae3-246">Instead, you can access hello collection property directly.</span></span> <span data-ttu-id="31ae3-247">Örneğin, kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="31ae3-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="31ae3-248">Toothis toofix değiştirmek herhangi bir derleme hataları:</span><span class="sxs-lookup"><span data-stu-id="31ae3-248">You can change it toothis toofix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="31ae3-249">Web uygulamaları için özel durum</span><span class="sxs-lookup"><span data-stu-id="31ae3-249">Special case for web applications</span></span>
<span data-ttu-id="31ae3-250">Serileştiren bir web uygulaması varsa `DocumentSearchResponse` toohello tarayıcı toosend arama sonuçları doğrudan kodunuzu toochange gerekir veya hello sonuçları değil seri doğru.</span><span class="sxs-lookup"><span data-stu-id="31ae3-250">If you have a web application that serializes `DocumentSearchResponse` directly toosend search results toohello browser, you will need toochange your code or hello results will not serialize correctly.</span></span> <span data-ttu-id="31ae3-251">Örneğin, kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="31ae3-251">For example, if your code looks like this:</span></span>

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

<span data-ttu-id="31ae3-252">Merhaba alarak değiştirebilirsiniz `.Results` hello arama yanıt toofix arama sonucu işleme özelliği:</span><span class="sxs-lookup"><span data-stu-id="31ae3-252">You can change it by getting hello `.Results` property of hello search response toofix search result rendering:</span></span>

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

<span data-ttu-id="31ae3-253">Bu gibi durumlarda toolook kendiniz bir kodunuzda olur; **hello derleyici değil sizi uyaracaktır** çünkü `JsonResult.Data` türü `object`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-253">You will have toolook for such cases in your code yourself; **hello compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="31ae3-254">CloudException değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="31ae3-254">CloudException changes</span></span>
<span data-ttu-id="31ae3-255">Merhaba `CloudException` sınıfı hello taşımıştır `Hyak.Common` ad alanı toohello `Microsoft.Rest.Azure` ad alanı.</span><span class="sxs-lookup"><span data-stu-id="31ae3-255">hello `CloudException` class has moved from hello `Hyak.Common` namespace toohello `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="31ae3-256">Ayrıca, kendi `Error` özelliği çok adlandırılmıştır`Body`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-256">Also, its `Error` property has been renamed too`Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="31ae3-257">SearchServiceClient ve Searchındexclient değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="31ae3-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="31ae3-258">Merhaba hello türünü `Credentials` özelliği değiştiğini `SearchCredentials` tooits temel sınıfı, `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-258">hello type of hello `Credentials` property has changed from `SearchCredentials` tooits base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="31ae3-259">Tooaccess hello gerekiyorsa `SearchCredentials` , bir `SearchIndexClient` veya `SearchServiceClient`, lütfen hello yeni kullanın `SearchCredentials` özelliği.</span><span class="sxs-lookup"><span data-stu-id="31ae3-259">If you need tooaccess hello `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use hello new `SearchCredentials` property.</span></span>

<span data-ttu-id="31ae3-260">Merhaba SDK, eski sürümlerinde `SearchServiceClient` ve `SearchIndexClient` sürdü oluşturucular sahip bir `HttpClient` parametresi.</span><span class="sxs-lookup"><span data-stu-id="31ae3-260">In older versions of hello SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="31ae3-261">Bu alan Oluşturucuları ile değiştirilmiştir bir `HttpClientHandler` ve bir dizi `DelegatingHandler` nesneleri.</span><span class="sxs-lookup"><span data-stu-id="31ae3-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="31ae3-262">Bu, daha kolay tooinstall özel işleyicileri toopre-HTTP isteklerini işleyen gerekirse kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="31ae3-262">This makes it easier tooinstall custom handlers toopre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="31ae3-263">Son olarak, sürdü oluşturucular hello bir `Uri` ve `SearchCredentials` değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-263">Finally, hello constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="31ae3-264">Örneğin, şöyle bir kodunuz varsa:</span><span class="sxs-lookup"><span data-stu-id="31ae3-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="31ae3-265">Toothis toofix değiştirmek herhangi bir derleme hataları:</span><span class="sxs-lookup"><span data-stu-id="31ae3-265">You can change it toothis toofix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="31ae3-266">Ayrıca hello hello tür parametresi kimlik bilgilerini not çok değişti`ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-266">Also note that hello type of hello credentials parameter has changed too`ServiceClientCredentials`.</span></span> <span data-ttu-id="31ae3-267">Bu olası tooaffect bu yana kodunuz: `SearchCredentials` türetildiği `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-267">This is unlikely tooaffect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="31ae3-268">İstek Kimliği geçirme</span><span class="sxs-lookup"><span data-stu-id="31ae3-268">Passing a request ID</span></span>
<span data-ttu-id="31ae3-269">Merhaba SDK eski sürümleri, bir istek kimliği üzerinde hello ayarlayabilirsiniz `SearchServiceClient` veya `SearchIndexClient` ve her isteği toohello REST API dahil edilmesi.</span><span class="sxs-lookup"><span data-stu-id="31ae3-269">In older versions of hello SDK, you could set a request ID on hello `SearchServiceClient` or `SearchIndexClient` and it would be included in every request toohello REST API.</span></span> <span data-ttu-id="31ae3-270">Bu, toocontact destek gerekiyorsa arama hizmetinizi sorunlarını gidermek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="31ae3-270">This is useful for troubleshooting issues with your search service if you need toocontact support.</span></span> <span data-ttu-id="31ae3-271">Ancak, tüm işlemleri için aynı kimliği toouse hello yerine her işlem için daha kullanışlı tooset benzersiz istek kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-271">However, it is more useful tooset a unique request ID for every operation rather than toouse hello same ID for all operations.</span></span> <span data-ttu-id="31ae3-272">Bu nedenle, hello `SetClientRequestId` yöntemlerinin `SearchServiceClient` ve `SearchIndexClient` kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="31ae3-272">For this reason, hello `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="31ae3-273">Bunun yerine, bir istek kimliği tooeach işlemi yöntemi hello isteğe bağlı geçirebilirsiniz `SearchRequestOptions` parametresi.</span><span class="sxs-lookup"><span data-stu-id="31ae3-273">Instead, you can pass a request ID tooeach operation method via hello optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="31ae3-274">Gelecekteki bir hello SDK sürümünde, diğer Azure SDK tarafından kullanılan hello yaklaşım ile tutarlı olan bir istek kimliği nesneler genel hello istemcide ayarlamak için yeni bir yöntem ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="31ae3-274">In a future release of hello SDK, we will add a new mechanism for setting a request ID globally on hello client objects that is consistent with hello approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="31ae3-275">Örnek</span><span class="sxs-lookup"><span data-stu-id="31ae3-275">Example</span></span>
<span data-ttu-id="31ae3-276">Şuna benzer bir kod varsa:</span><span class="sxs-lookup"><span data-stu-id="31ae3-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="31ae3-277">Toothis toofix değiştirmek herhangi bir derleme hataları:</span><span class="sxs-lookup"><span data-stu-id="31ae3-277">You can change it toothis toofix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="31ae3-278">Arabirim adı değişikliği</span><span class="sxs-lookup"><span data-stu-id="31ae3-278">Interface name changes</span></span>
<span data-ttu-id="31ae3-279">Merhaba işlemi Grup arabirimi adları tüm değiştirilen toobe karşılık gelen özellik adları ile tutarlı vardır:</span><span class="sxs-lookup"><span data-stu-id="31ae3-279">hello operation group interface names have all changed toobe consistent with their corresponding property names:</span></span>

* <span data-ttu-id="31ae3-280">Merhaba türü `ISearchServiceClient.Indexes` adlandırılmıştır `IIndexOperations` çok`IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-280">hello type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` too`IIndexesOperations`.</span></span>
* <span data-ttu-id="31ae3-281">Merhaba türü `ISearchServiceClient.Indexers` adlandırılmıştır `IIndexerOperations` çok`IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-281">hello type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` too`IIndexersOperations`.</span></span>
* <span data-ttu-id="31ae3-282">Merhaba türü `ISearchServiceClient.DataSources` adlandırılmıştır `IDataSourceOperations` çok`IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-282">hello type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` too`IDataSourcesOperations`.</span></span>
* <span data-ttu-id="31ae3-283">Merhaba türü `ISearchIndexClient.Documents` adlandırılmıştır `IDocumentOperations` çok`IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-283">hello type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` too`IDocumentsOperations`.</span></span>

<span data-ttu-id="31ae3-284">Bu değişiklik, test amacıyla bu arabirimleri mocks oluşturduğunuz sürece olası tooaffect kodunuz:.</span><span class="sxs-lookup"><span data-stu-id="31ae3-284">This change is unlikely tooaffect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="31ae3-285">Hata düzeltmeleri sürüm 1.1</span><span class="sxs-lookup"><span data-stu-id="31ae3-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="31ae3-286">Hello Azure Search .NET SDK'sı ile ilgili tooserialization özel model sınıfların eski sürümleri bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="31ae3-286">There was a bug in older versions of hello Azure Search .NET SDK relating tooserialization of custom model classes.</span></span> <span data-ttu-id="31ae3-287">bir null değer türünde bir özelliği bir özel model sınıfı oluşturduysanız hello hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-287">hello bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-tooreproduce"></a><span data-ttu-id="31ae3-288">Adımları tooreproduce</span><span class="sxs-lookup"><span data-stu-id="31ae3-288">Steps tooreproduce</span></span>
<span data-ttu-id="31ae3-289">Bir özel model sınıfı null değer türünde bir özellik oluşturun.</span><span class="sxs-lookup"><span data-stu-id="31ae3-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="31ae3-290">Örneğin, bir ortak ekleyin `UnitCount` türündeki özelliği `int` yerine `int?`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="31ae3-291">Bu tür hello varsayılan değere sahip bir belge sıralıyorsanız (örneğin, 0 `int`), hello alan Azure Search'te boş olacaktır.</span><span class="sxs-lookup"><span data-stu-id="31ae3-291">If you index a document with hello default value of that type (for example, 0 for `int`), hello field will be null in Azure Search.</span></span> <span data-ttu-id="31ae3-292">Daha sonra bu belge için arama yaparsanız hello `Search` çağrısı throw `JsonSerializationException` , onu dönüştürülemiyor şikayetçi `null` çok`int`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-292">If you subsequently search for that document, hello `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` too`int`.</span></span>

<span data-ttu-id="31ae3-293">Ayrıca, filtreleri null toohello dizin hedeflenen hello değeri yerine yazıldı beri beklendiği gibi çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="31ae3-293">Also, filters may not work as expected since null was written toohello index instead of hello intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="31ae3-294">Ayrıntılar Düzelt</span><span class="sxs-lookup"><span data-stu-id="31ae3-294">Fix details</span></span>
<span data-ttu-id="31ae3-295">Sürüm hello SDK 1.1 Biz bu sorunu düzelttik.</span><span class="sxs-lookup"><span data-stu-id="31ae3-295">We have fixed this issue in version 1.1 of hello SDK.</span></span> <span data-ttu-id="31ae3-296">Şimdi, böyle bir model sınıfı varsa:</span><span class="sxs-lookup"><span data-stu-id="31ae3-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="31ae3-297">ve ayarladığınız `IntValue` değer artık doğru hello kablo 0 olarak serileştirilmiş ve hello dizin 0 olarak depolanan olduğunu too0.</span><span class="sxs-lookup"><span data-stu-id="31ae3-297">and you set `IntValue` too0, that value is now correctly serialized as 0 on hello wire and stored as 0 in hello index.</span></span> <span data-ttu-id="31ae3-298">Yuvarlak tripping de beklendiği gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="31ae3-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="31ae3-299">Olası bir sorunu toobe Bu yaklaşımda farkında: atanamayan bir özellik ile bir model türünü kullanan çok varsa**garanti** hiçbir belgeleri dizininize hello karşılık gelen alan için bir null değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="31ae3-299">There is one potential issue toobe aware of with this approach: If you use a model type with a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="31ae3-300">Merhaba SDK ne hello Azure Search REST API'si, tooenforce bu yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="31ae3-300">Neither hello SDK nor hello Azure Search REST API will help you tooenforce this.</span></span>

<span data-ttu-id="31ae3-301">Bu yalnızca kuramsal bir sorun değildir: türü olan yeni bir alan tooan mevcut dizin eklediğiniz bir senaryoyu düşünün `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="31ae3-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="31ae3-302">(Tüm türleri Azure Search'te boş değer atanabilir olmasıdır) hello dizin tanımını güncelleştirdikten sonra bu yeni alan için bir null değer tüm belgeler olacaktır.</span><span class="sxs-lookup"><span data-stu-id="31ae3-302">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="31ae3-303">Ardından bir model sınıfı bir null ile kullanırsanız `int` özelliği bu alan için elde edersiniz bir `JsonSerializationException` şöyle tooretrieve belgeleri çalışırken:</span><span class="sxs-lookup"><span data-stu-id="31ae3-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="31ae3-304">Bu nedenle, hala bir en iyi uygulama olarak model sınıflarınızda boş değer atanabilir türler kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="31ae3-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="31ae3-305">Bu hatayı ve hello düzeltme hakkında daha fazla ayrıntı için lütfen bkz. [github'daki bu sorunu](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="31ae3-305">For more details on this bug and hello fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

