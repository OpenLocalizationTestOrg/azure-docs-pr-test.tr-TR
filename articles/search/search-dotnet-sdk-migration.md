---
title: "Azure Search .NET SDK sürüm 1.1 yükseltme | Microsoft Docs"
description: "Azure Search .NET SDK sürüm 1.1 yükseltme"
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
ms.openlocfilehash: 9782454e3bfc697b63cde8aa28a14be0c393c36b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-net-sdk-version-3"></a><span data-ttu-id="1b3bf-103">Azure Search .NET SDK sürüm 3 yükseltme</span><span class="sxs-lookup"><span data-stu-id="1b3bf-103">Upgrading to the Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="1b3bf-104">2.0-Önizleme veya, daha eski bir sürümü kullanıyorsanız [Azure Search .NET SDK'sı](https://aka.ms/search-sdk), bu makalede, uygulamanızı sürüm 3'ü kullanacak şekilde yükseltmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-104">If you're using version 2.0-preview or older of the [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application to use version 3.</span></span>

<span data-ttu-id="1b3bf-105">Örnekler dahil olmak üzere SDK'ın daha genel bir kılavuz için bkz: [bir .NET uygulamasından Azure Search kullanmayı](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="1b3bf-105">For a more general walkthrough of the SDK including examples, see [How to use Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="1b3bf-106">Azure Search .NET SDK'sı 3 sürümünü önceki sürümlerinden bazı değişiklikler içerir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-106">Version 3 of the Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="1b3bf-107">Kodunuzu değiştirmeden yalnızca en az çaba gerektirmelidir şekilde çoğunlukla ikincil, bunlar.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="1b3bf-108">Bkz: [yükseltme adımları](#UpgradeSteps) yeni SDK sürümü kullanmak kodunuzu değiştirmek konusunda yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-108">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="1b3bf-109">Sürüm 1.0.2-preview kullanıyorsanız veya daha eski, sürüm 1.1 ilk ve ardından yükseltme 3 sürümüne yükseltmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-109">If you're using version 1.0.2-preview or older, you should upgrade to version 1.1 first, and then upgrade to version 3.</span></span> <span data-ttu-id="1b3bf-110">Bkz: [ek: sürüm 1.1 yükseltme adımları](#UpgradeStepsV1) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-110">See [Appendix: Steps to upgrade to version 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="1b3bf-111">Azure Search Hizmeti örneğinizi son de dahil olmak üzere birkaç REST API sürümlerini destekler.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-111">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="1b3bf-112">En son artık değildir, ancak en yeni sürümü kullanmak için kodunuzu geçirmek öneririz bir sürümünü kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-112">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span> <span data-ttu-id="1b3bf-113">REST API kullanırken, api-version parametresi aracılığıyla her istekte API sürümü belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-113">When using the REST API, you must specify the API version in every request via the api-version parameter.</span></span> <span data-ttu-id="1b3bf-114">.NET SDK kullanarak, kullanmakta olduğunuz SDK sürümü karşılık gelen REST API sürümü belirler.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-114">When using the .NET SDK, the version of the SDK you’re using determines the corresponding version of the REST API.</span></span> <span data-ttu-id="1b3bf-115">Eski bir SDK kullanıyorsanız, hizmet daha yeni bir API sürümü desteklemek için yükseltilir olsa bile bu kodu ile herhangi bir değişiklik çalıştırmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-115">If you are using an older SDK, you can continue to run that code with no changes even if the service is upgraded to support a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="1b3bf-116">Sürüm 3 yenilikler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="1b3bf-116">What's new in version 3</span></span>
<span data-ttu-id="1b3bf-117">Azure Search .NET SDK'sı 3 sürümünü hedefleyen en son Azure Search REST API'sini özellikle 2016-09-01 genel olarak kullanılabilir sürümü.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-117">Version 3 of the Azure Search .NET SDK targets the latest generally available version of the Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="1b3bf-118">Aşağıdakiler de dahil olmak üzere, bir .NET uygulamasından Azure Search'ün birçok yeni özellik kullanmayı mümkün kılar:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-118">This makes it possible to use many new features of Azure Search from a .NET application, including the following:</span></span>

* [<span data-ttu-id="1b3bf-119">Özel çözümleyiciler</span><span class="sxs-lookup"><span data-stu-id="1b3bf-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="1b3bf-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) ve [Azure Table Storage](search-howto-indexing-azure-tables.md) dizin oluşturucu desteği</span><span class="sxs-lookup"><span data-stu-id="1b3bf-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="1b3bf-121">Dizin Oluşturucu özelleştirme aracılığıyla [alan eşlemeleri](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="1b3bf-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="1b3bf-122">Güvenli eşzamanlı dizin tanımları, dizin oluşturucular ve veri kaynaklarını güncelleştirme etkinleştirmek için Etag'ler desteği</span><span class="sxs-lookup"><span data-stu-id="1b3bf-122">ETags support to enable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="1b3bf-123">Dizin alan tanımları bildirimli olarak model sınıfınız dekorasyon ve yeni kullanarak oluşturmak için destek `FieldBuilder` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-123">Support for building index field definitions declaratively by decorating your model class and using the new `FieldBuilder` class.</span></span>
* <span data-ttu-id="1b3bf-124">.NET Core ve .NET taşınabilir profil 111 desteği</span><span class="sxs-lookup"><span data-stu-id="1b3bf-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="1b3bf-125">Yükseltme adımları</span><span class="sxs-lookup"><span data-stu-id="1b3bf-125">Steps to upgrade</span></span>
<span data-ttu-id="1b3bf-126">İlk olarak, NuGet başvuru için güncelleştirme `Microsoft.Azure.Search` NuGet Paket Yöneticisi konsolu kullanılarak veya göre proje başvuruları sağ tıklayıp Visual Studio'da "NuGet paketleri...'ı Yönet" seçerek.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="1b3bf-127">NuGet yeni paketleri ve bunların bağımlılıklarını indirdikten sonra projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-127">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="1b3bf-128">Kodunuzu nasıl yapılandırıldığını bağlı olarak başarılı bir şekilde yeniden oluşturmak.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="1b3bf-129">Bu durumda, başlamaya hazırsınız!</span><span class="sxs-lookup"><span data-stu-id="1b3bf-129">If so, you're ready to go!</span></span>

<span data-ttu-id="1b3bf-130">Derleme başarısız olursa, bir derleme hatası aşağıdaki gibi görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-130">If your build fails, you should see a build error like the following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' to 'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="1b3bf-131">Bu yapı hatayı düzeltmek için sonraki adım olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-131">The next step is to fix this build error.</span></span> <span data-ttu-id="1b3bf-132">Bkz: [önemli değişiklikler sürüm 3](#ListOfChanges) hatanın nedeni nedir ve nasıl düzeltileceği hakkında ayrıntılar için.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes the error and how to fix it.</span></span>

<span data-ttu-id="1b3bf-133">Artık kullanılmayan yöntemleri ya da özellikleri ilgili ek derleme uyarıları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-133">You may see additional build warnings related to obsolete methods or properties.</span></span> <span data-ttu-id="1b3bf-134">Uyarıları ne yerine kullanım dışı özelliği kullanmak yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-134">The warnings will include instructions on what to use instead of the deprecated feature.</span></span> <span data-ttu-id="1b3bf-135">Örneğin, uygulamanızın kullandığı `IndexingParameters.Base64EncodeKeys` özelliği bildiren bir uyarı almak`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="1b3bf-135">For example, if your application uses the `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="1b3bf-136">Derleme hataları düzelttik sonra isterseniz yeni işlevsellikten yararlanmak için uygulamanızı değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-136">Once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span> <span data-ttu-id="1b3bf-137">SDK'sındaki yeni özellikleri ayrıntılı olarak [sürüm 3 yenilikler](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="1b3bf-137">New features in the SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="1b3bf-138">Sürüm 3'de yeni değişiklikler</span><span class="sxs-lookup"><span data-stu-id="1b3bf-138">Breaking changes in version 3</span></span>
<span data-ttu-id="1b3bf-139">Var. Yeni kod gerektirebilecek sürümünde 3 değişiklikler, küçük bir sayı, uygulamanızın yeniden ek olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-139">There a small number of breaking changes in version 3 that may require code changes in addition to rebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="1b3bf-140">Indexes.GetClient dönüş türü</span><span class="sxs-lookup"><span data-stu-id="1b3bf-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="1b3bf-141">`Indexes.GetClient` Yöntemi yeni bir dönüş türüne sahip.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-141">The `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="1b3bf-142">Daha önce döndürülen `SearchIndexClient`, ancak bu şekilde değiştirilmiştir `ISearchIndexClient` sürüm 2.0-Önizleme ve bu değişiklik sürüm 3 taşır.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-142">Previously, it returned `SearchIndexClient`, but this was changed to `ISearchIndexClient` in version 2.0-preview, and that change carries over to version 3.</span></span> <span data-ttu-id="1b3bf-143">Bu mock isteyen müşteriler desteklemektir `GetClient` yöntemi, sahte bir uygulama döndürerek birim testleri için `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-143">This is to support customers that wish to mock the `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="1b3bf-144">Örnek</span><span class="sxs-lookup"><span data-stu-id="1b3bf-144">Example</span></span>
<span data-ttu-id="1b3bf-145">Kodunuzu şöyle ise:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="1b3bf-146">Bu yapı hataları düzeltmek için bunu değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-146">You can change it to this to fix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-to-strings"></a><span data-ttu-id="1b3bf-147">AnalyzerName, veri türü ve diğerleri artık dizelere örtük olarak dönüştürülebilir</span><span class="sxs-lookup"><span data-stu-id="1b3bf-147">AnalyzerName, DataType, and others are no longer implicitly convertible to strings</span></span>
<span data-ttu-id="1b3bf-148">Öğesinden türetilen Azure Search .NET SDK'sı birçok türlerinde vardır `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-148">There are many types in the Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="1b3bf-149">Bu tür daha önce tüm türüne örtük olarak dönüştürülebilir `string`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-149">Previously these types were all implicitly convertible to type `string`.</span></span> <span data-ttu-id="1b3bf-150">Ancak, bir hata bulunması `Object.Equals` bu sınıfların ve bu örtük dönüştürme devre dışı bırakılması gereken hatayı düzeltmek için uygulama.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-150">However, a bug was discovered in the `Object.Equals` implementation for these classes, and fixing the bug required disabling this implicit conversion.</span></span> <span data-ttu-id="1b3bf-151">Açık dönüşüm `string` hala izin verilir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-151">Explicit conversion to `string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="1b3bf-152">Örnek</span><span class="sxs-lookup"><span data-stu-id="1b3bf-152">Example</span></span>
<span data-ttu-id="1b3bf-153">Kodunuzu şöyle ise:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-153">If your code looks like this:</span></span>

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

<span data-ttu-id="1b3bf-154">Bu yapı hataları düzeltmek için bunu değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-154">You can change it to this to fix any build errors:</span></span>

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

### <a name="removed-obsolete-members"></a><span data-ttu-id="1b3bf-155">Eski üyeler kaldırıldı</span><span class="sxs-lookup"><span data-stu-id="1b3bf-155">Removed obsolete members</span></span>

<span data-ttu-id="1b3bf-156">Derleme hataları ile ilgili görebilirsiniz yöntemleri ya da geçersiz sürüm olarak 2.0 Önizleme ve daha sonra kaldırılan sürüm 3 işaretlenen özellikleri.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-156">You may see build errors related to methods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="1b3bf-157">Bu tür hatalarla karşılaşırsanız, bunların nasıl çözüleceği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-157">If you encounter such errors, here is how to resolve them:</span></span>

- <span data-ttu-id="1b3bf-158">Bu oluşturucu kullanıyorsanız: `ScoringParameter(string name, string value)`, bunun yerine bunu kullanın:`ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="1b3bf-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="1b3bf-159">Kullanmakta olduğunuz varsa `ScoringParameter.Value` özelliği, kullanım `ScoringParameter.Values` özelliği veya `ToString` yöntemi yerine.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-159">If you were using the `ScoringParameter.Value` property, use the `ScoringParameter.Values` property or the `ToString` method instead.</span></span>
- <span data-ttu-id="1b3bf-160">Kullanmakta olduğunuz varsa `SearchRequestOptions.RequestId` özelliği, kullanım `ClientRequestId` özelliği yerine.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-160">If you were using the `SearchRequestOptions.RequestId` property, use the `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="1b3bf-161">Kaldırılan Önizleme özellikleri</span><span class="sxs-lookup"><span data-stu-id="1b3bf-161">Removed preview features</span></span>

<span data-ttu-id="1b3bf-162">Sürüm 3 sürüm 2.0-Önizlemesi'nden yükseltiyorsanız, JSON ve Blob dizin oluşturucular için destek ayrıştırma CSV kaldırıldı, bu özellikler hala önizlemede olduğundan unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-162">If you are upgrading from version 2.0-preview to version 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="1b3bf-163">Özellikle, aşağıdaki yöntemlerden birini `IndexingParametersExtensions` sınıfı kaldırıldı:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-163">Specifically, the following methods of the `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="1b3bf-164">Uygulamanız bu özelliklere sıkı bir bağımlılık varsa, Azure Search .NET SDK'sı 3 sürümüne yükseltmeniz mümkün olmaz.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-164">If your application has a hard dependency on these features, you will not be able to upgrade to version 3 of the Azure Search .NET SDK.</span></span> <span data-ttu-id="1b3bf-165">Sürüm 2.0-Önizleme kullanmaya devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-165">You can continue to use version 2.0-preview.</span></span> <span data-ttu-id="1b3bf-166">Bununla birlikte, lütfen aklınızda **üretim uygulamaları SDK'ları önizlemede kullanmanızı önermiyoruz**.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="1b3bf-167">Önizleme özellikleri yalnızca değerlendirme ve değişiklik.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="1b3bf-168">Sonuç</span><span class="sxs-lookup"><span data-stu-id="1b3bf-168">Conclusion</span></span>
<span data-ttu-id="1b3bf-169">Azure Search .NET SDK'sını kullanma hakkında daha fazla ayrıntı gereksinim duyarsanız, yeni güncelleştirilen bakın [nasıl yapılır](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="1b3bf-169">If you need more details on using the Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="1b3bf-170">SDK'bildiriminiz bizim.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-170">We welcome your feedback on the SDK.</span></span> <span data-ttu-id="1b3bf-171">Sorunlarla karşılaşırsanız, bize yardım isteyin çekinmeyin [Azure arama MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="1b3bf-171">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="1b3bf-172">Bir hata bulursanız, bir sorunun dosya [Azure .NET SDK GitHub deposunu](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="1b3bf-172">If you find a bug, you can file an issue in the [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="1b3bf-173">Sorunu başlıkla önek emin olun "arama SDK:".</span><span class="sxs-lookup"><span data-stu-id="1b3bf-173">Make sure to prefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="1b3bf-174">Azure Search kullandığınız için teşekkür ederiz!</span><span class="sxs-lookup"><span data-stu-id="1b3bf-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-to-upgrade-to-version-11"></a><span data-ttu-id="1b3bf-175">Ek: 1.1 sürümüne yükseltmek için adımlar</span><span class="sxs-lookup"><span data-stu-id="1b3bf-175">Appendix: Steps to upgrade to version 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="1b3bf-176">Bu bölüm, yalnızca Azure Search .NET SDK sürüm 1.0.2-preview ve kullanıcıları eski için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-176">This section applies only to users of the Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="1b3bf-177">İlk olarak, NuGet başvuru için güncelleştirme `Microsoft.Azure.Search` NuGet Paket Yöneticisi konsolu kullanılarak veya göre proje başvuruları sağ tıklayıp Visual Studio'da "NuGet paketleri...'ı Yönet" seçerek.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="1b3bf-178">NuGet yeni paketleri ve bunların bağımlılıklarını indirdikten sonra projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-178">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="1b3bf-179">Daha önce sürüm 1.0.0-preview, 1.0.1-preview veya 1.0.2-preview kullanıyorsanız, derleme başarısız olması ve başlamaya hazırsınız!</span><span class="sxs-lookup"><span data-stu-id="1b3bf-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, the build should succeed and you're ready to go!</span></span>

<span data-ttu-id="1b3bf-180">Daha önce sürüm 0.13.0-preview kullanıyorsanız veya daha eski, görmeniz gerekir derleme hataları aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-180">If you were previously using version 0.13.0-preview or older, you should see build errors like the following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: The type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="1b3bf-181">Tek tek derleme hataları düzeltmek için sonraki adım olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-181">The next step is to fix the build errors one by one.</span></span> <span data-ttu-id="1b3bf-182">Çoğu SDK'ın yeniden adlandırıldığı bazı sınıfı ve yöntemi adlarını değiştirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-182">Most will require changing some class and method names that have been renamed in the SDK.</span></span> <span data-ttu-id="1b3bf-183">[Yeni sürüm 1.1 değişiklikler listesi](#ListOfChangesV1) adı değişikliklerin listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="1b3bf-184">Belgelerinizi modellemek için özel sınıflar kullanıyorsanız ve bu sınıfların null ilkel türler özelliklerini sahip (örneğin, `int` veya `bool` C#), hangisinin olmanız gerekir kullanan SDK 1.1 sürümünde hata düzeltmesi yoktur.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-184">If you're using custom classes to model your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in the 1.1 version of the SDK of which you should be aware.</span></span> <span data-ttu-id="1b3bf-185">Bkz: [hata düzeltmeleri sürüm 1.1](#BugFixesV1) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="1b3bf-186">Derleme hataları düzelttik sonra son olarak, isterseniz yeni işlevsellikten yararlanmak için uygulamanızı değişiklik yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-186">Finally, once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="1b3bf-187">Yeni sürüm 1.1 değişiklikler listesi</span><span class="sxs-lookup"><span data-stu-id="1b3bf-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="1b3bf-188">Aşağıdaki listede değişiklik uygulama kodunuz etkileyecek olasılığını göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-188">The following list is ordered by the likelihood that the change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="1b3bf-189">IndexBatch ve IndexAction değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="1b3bf-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="1b3bf-190">`IndexBatch.Create`adlandırıldı `IndexBatch.New` ve artık sahip bir `params` bağımsız değişkeni.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-190">`IndexBatch.Create` has been renamed to `IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="1b3bf-191">Kullanabileceğiniz `IndexBatch.New` Eylemler (birleştirme, silme, vb.) farklı türlerde karışık toplu işlemler için.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="1b3bf-192">Ayrıca, toplu işleri oluşturmak için yeni statik yöntemler vardır tüm eylemleri nerede aynı: `Delete`, `Merge`, `MergeOrUpload`, ve `Upload`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-192">In addition, there are new static methods for creating batches where all the actions are the same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="1b3bf-193">`IndexAction`Genel oluşturucular artık sahiptir ve özelliklerini şimdi değişmez.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="1b3bf-194">Farklı amaçlar için Eylemler oluşturmak için yeni statik yöntemler kullanmalısınız: `Delete`, `Merge`, `MergeOrUpload`, ve `Upload`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-194">You should use the new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="1b3bf-195">`IndexAction.Create`kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="1b3bf-196">Yalnızca bir belge alan aşırı kullandıysanız, kullandığınızdan emin olun `Upload` yerine.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-196">If you used the overload that takes only a document, make sure to use `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="1b3bf-197">Örnek</span><span class="sxs-lookup"><span data-stu-id="1b3bf-197">Example</span></span>
<span data-ttu-id="1b3bf-198">Kodunuzu şöyle ise:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="1b3bf-199">Bu yapı hataları düzeltmek için bunu değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-199">You can change it to this to fix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="1b3bf-200">İsterseniz, daha fazla için basitleştirin:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-200">If you want, you can further simplify it to this:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="1b3bf-201">IndexBatchException değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="1b3bf-201">IndexBatchException changes</span></span>
<span data-ttu-id="1b3bf-202">`IndexBatchException.IndexResponse` Özelliği adlandırılmıştır `IndexingResults`, ve türünü şimdi `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-202">The `IndexBatchException.IndexResponse` property has been renamed to `IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="1b3bf-203">Örnek</span><span class="sxs-lookup"><span data-stu-id="1b3bf-203">Example</span></span>
<span data-ttu-id="1b3bf-204">Kodunuzu şöyle ise:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="1b3bf-205">Bu yapı hataları düzeltmek için bunu değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-205">You can change it to this to fix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="1b3bf-206">Operasyon yöntemi değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="1b3bf-206">Operation method changes</span></span>
<span data-ttu-id="1b3bf-207">Azure Search .NET SDK'sı her işlem için zaman uyumlu ve zaman uyumsuz arayanlar yöntemi aşırı bir dizi açıktır.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-207">Each operation in the Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="1b3bf-208">İmzalar ve bu yöntem aşırı Finansman sürüm 1.1 değişti.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-208">The signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="1b3bf-209">Örneğin, "Dizin istatistikleri Al" işlemi SDK'ın eski sürümlerinde bu imzaları kullanıma sunulan:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-209">For example, the "Get Index Statistics" operation in older versions of the SDK exposed these signatures:</span></span>

<span data-ttu-id="1b3bf-210">İçinde `IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="1b3bf-211">İçinde `IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="1b3bf-212">Aynı işlem içinde sürüm 1.1 yöntemi imzaları şöyle görünür:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-212">The method signatures for the same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="1b3bf-213">İçinde `IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="1b3bf-214">İçinde `IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-214">In `IndexesOperationsExtensions`:</span></span>

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

<span data-ttu-id="1b3bf-215">Sürüm 1.1 ile başlayarak, Azure Search .NET SDK'sı farklı işlemi yöntemleri düzenler:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-215">Starting with version 1.1, the Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="1b3bf-216">Parametreleri bunun yerine varsayılan olarak, isteğe bağlı parametreler Modellenen artık ek yöntemi aşırı daha.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="1b3bf-217">Bu yöntem aşırı yüklemeleri, bazen önemli ölçüde azaltır.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-217">This reduces the number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="1b3bf-218">Genişletme yöntemleri şimdi ayrıntılarını yabancı HTTP çağrıyı yapandan çok gizleyin.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-218">The extension methods now hide a lot of the extraneous details of HTTP from the caller.</span></span> <span data-ttu-id="1b3bf-219">Örneğin, SDK'ın eski sürümleri işlemi yöntemleri throw çünkü denetlemek için genellikle ihtiyacım kalmadı bir HTTP durum kodu ile bir yanıt nesnesi döndürülen `CloudException` bir hata gösterir herhangi bir durum kodu için.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-219">For example, older versions of the SDK returned a response object with an HTTP status code, which you often didn't need to check because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="1b3bf-220">Yeni Uzantı yöntemleri, yalnızca model nesneleri, kodunuzda açılacak sahip olmanın zahmetinden kurtarır döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-220">The new extension methods just return model objects, saving you the trouble of having to unwrap them in your code.</span></span>
* <span data-ttu-id="1b3bf-221">Buna karşılık, çekirdek artık ihtiyacınız olursa, HTTP düzeyinde daha fazla denetime sunmaya yöntemleri arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-221">Conversely, the core interfaces now expose methods that give you more control at the HTTP level if you need it.</span></span> <span data-ttu-id="1b3bf-222">Şimdi istekleri ve yeni dahil edilecek özel HTTP üst bilgilerinde geçirebilirsiniz `AzureOperationResponse<T>` dönüş türü, doğrudan erişim verir `HttpRequestMessage` ve `HttpResponseMessage` işlemi için.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-222">You can now pass in custom HTTP headers to be included in requests, and the new `AzureOperationResponse<T>` return type gives you direct access to the `HttpRequestMessage` and `HttpResponseMessage` for the operation.</span></span> <span data-ttu-id="1b3bf-223">`AzureOperationResponse`tanımlanan `Microsoft.Rest.Azure` ad alanı ve değiştirir `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-223">`AzureOperationResponse` is defined in the `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="1b3bf-224">ScoringParameters değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="1b3bf-224">ScoringParameters changes</span></span>
<span data-ttu-id="1b3bf-225">Adlı yeni bir sınıf `ScoringParameter` bir arama sorgusu profilleri Puanlama için parametreleri sağlayın kolaylaştırmak için en son SDK eklendi.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-225">A new class named `ScoringParameter` has been added in the latest SDK to make it easier to provide parameters to scoring profiles in a search query.</span></span> <span data-ttu-id="1b3bf-226">Daha önce `ScoringProfiles` özelliği `SearchParameters` sınıfı olarak yazıldığından `IList<string>`; Olarak yazılan artık `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-226">Previously the `ScoringProfiles` property of the `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="1b3bf-227">Örnek</span><span class="sxs-lookup"><span data-stu-id="1b3bf-227">Example</span></span>
<span data-ttu-id="1b3bf-228">Kodunuzu şöyle ise:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="1b3bf-229">Bu yapı hataları düzeltmek için bunu değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-229">You can change it to this to fix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="1b3bf-230">Model sınıfı değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="1b3bf-230">Model class changes</span></span>
<span data-ttu-id="1b3bf-231">Açıklanan imza değişiklikler nedeniyle [işlemi yöntemi değişiklikleri](#OperationMethodChanges), birçok sınıflarda `Microsoft.Azure.Search.Models` ad alanı yeniden adlandırılmış veya kaldırılmış.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-231">Due to the signature changes described in [Operation method changes](#OperationMethodChanges), many classes in the `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="1b3bf-232">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-232">For example:</span></span>

* <span data-ttu-id="1b3bf-233">`IndexDefinitionResponse`ile değiştirilmiştir`AzureOperationResponse<Index>`</span><span class="sxs-lookup"><span data-stu-id="1b3bf-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="1b3bf-234">`DocumentSearchResponse`, `DocumentSearchResult` olarak yeniden adlandırıldı</span><span class="sxs-lookup"><span data-stu-id="1b3bf-234">`DocumentSearchResponse` has been renamed to `DocumentSearchResult`</span></span>
* <span data-ttu-id="1b3bf-235">`IndexResult`, `IndexingResult` olarak yeniden adlandırıldı</span><span class="sxs-lookup"><span data-stu-id="1b3bf-235">`IndexResult` has been renamed to `IndexingResult`</span></span>
* <span data-ttu-id="1b3bf-236">`Documents.Count()`Şimdi döndüren bir `long` ile belge sayısı yerine bir`DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="1b3bf-236">`Documents.Count()` now returns a `long` with the document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="1b3bf-237">`IndexGetStatisticsResponse`, `IndexGetStatisticsResult` olarak yeniden adlandırıldı</span><span class="sxs-lookup"><span data-stu-id="1b3bf-237">`IndexGetStatisticsResponse` has been renamed to `IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="1b3bf-238">`IndexListResponse`, `IndexListResult` olarak yeniden adlandırıldı</span><span class="sxs-lookup"><span data-stu-id="1b3bf-238">`IndexListResponse` has been renamed to `IndexListResult`</span></span>

<span data-ttu-id="1b3bf-239">Özetlemek için `OperationResponse`-türetilmiş sarmalamak için bir model nesnesi kaldırılmış yalnızca var olan sınıfları.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-239">To summarize, `OperationResponse`-derived classes that existed only to wrap a model object have been removed.</span></span> <span data-ttu-id="1b3bf-240">Kalan sınıfları değiştirildi kendi soneki beklendiğinden `Response` için `Result`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-240">The remaining classes have had their suffix changed from `Response` to `Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="1b3bf-241">Örnek</span><span class="sxs-lookup"><span data-stu-id="1b3bf-241">Example</span></span>
<span data-ttu-id="1b3bf-242">Kodunuzu şöyle ise:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-242">If your code looks like this:</span></span>

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

<span data-ttu-id="1b3bf-243">Bu yapı hataları düzeltmek için bunu değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-243">You can change it to this to fix any build errors:</span></span>

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

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="1b3bf-244">Yanıt sınıfları ve IEnumerable</span><span class="sxs-lookup"><span data-stu-id="1b3bf-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="1b3bf-245">Koleksiyonları tutun yanıt sınıfları artık uygulama kodunuz etkileyebilecek ek bir değişiklik olduğunu `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="1b3bf-246">Bunun yerine, koleksiyon özelliği doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-246">Instead, you can access the collection property directly.</span></span> <span data-ttu-id="1b3bf-247">Örneğin, kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="1b3bf-248">Bu yapı hataları düzeltmek için bunu değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-248">You can change it to this to fix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="1b3bf-249">Web uygulamaları için özel durum</span><span class="sxs-lookup"><span data-stu-id="1b3bf-249">Special case for web applications</span></span>
<span data-ttu-id="1b3bf-250">Serileştiren bir web uygulaması varsa `DocumentSearchResponse` doğrudan arama sonuçları tarayıcıya göndermek için kodunu değiştirmeniz gerekir veya sonuçları doğru seri değildir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-250">If you have a web application that serializes `DocumentSearchResponse` directly to send search results to the browser, you will need to change your code or the results will not serialize correctly.</span></span> <span data-ttu-id="1b3bf-251">Örneğin, kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="1b3bf-252">Alarak değiştirebilirsiniz `.Results` arama sonucu işleme düzeltmek için arama yanıtının özelliği:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-252">You can change it by getting the `.Results` property of the search response to fix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="1b3bf-253">Böyle durumlarda, kodunuzda kendiniz Ara gerekir; **Derleyici sizi uyarır değil** çünkü `JsonResult.Data` türü `object`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-253">You will have to look for such cases in your code yourself; **The compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="1b3bf-254">CloudException değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="1b3bf-254">CloudException changes</span></span>
<span data-ttu-id="1b3bf-255">`CloudException` Sınıfı taşınmış `Hyak.Common` ad alanına `Microsoft.Rest.Azure` ad alanı.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-255">The `CloudException` class has moved from the `Hyak.Common` namespace to the `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="1b3bf-256">Ayrıca, kendi `Error` özelliği adlandırılmıştır `Body`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-256">Also, its `Error` property has been renamed to `Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="1b3bf-257">SearchServiceClient ve Searchındexclient değişiklikleri</span><span class="sxs-lookup"><span data-stu-id="1b3bf-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="1b3bf-258">Türü `Credentials` özelliği değiştiğini `SearchCredentials` için temel sınıfı olan `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-258">The type of the `Credentials` property has changed from `SearchCredentials` to its base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="1b3bf-259">Erişmeniz gerekiyorsa `SearchCredentials` , bir `SearchIndexClient` veya `SearchServiceClient`, Lütfen yeni kullanın `SearchCredentials` özelliği.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-259">If you need to access the `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use the new `SearchCredentials` property.</span></span>

<span data-ttu-id="1b3bf-260">SDK ' nın eski sürümlerinde `SearchServiceClient` ve `SearchIndexClient` sürdü oluşturucular sahip bir `HttpClient` parametresi.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-260">In older versions of the SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="1b3bf-261">Bu alan Oluşturucuları ile değiştirilmiştir bir `HttpClientHandler` ve bir dizi `DelegatingHandler` nesneleri.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="1b3bf-262">Bu, HTTP isteklerini gerekirse önceden işlemek için özel işleyicileri yüklemek kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-262">This makes it easier to install custom handlers to pre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="1b3bf-263">Son olarak, sürdü oluşturucular bir `Uri` ve `SearchCredentials` değiştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-263">Finally, the constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="1b3bf-264">Örneğin, şöyle bir kodunuz varsa:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="1b3bf-265">Bu yapı hataları düzeltmek için bunu değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-265">You can change it to this to fix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="1b3bf-266">Ayrıca kimlik bilgileri parametresinin türü için değiştirildiğine dikkat edin `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-266">Also note that the type of the credentials parameter has changed to `ServiceClientCredentials`.</span></span> <span data-ttu-id="1b3bf-267">Bu yana kodunuzu etkilemek düşüktür `SearchCredentials` türetildiği `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-267">This is unlikely to affect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="1b3bf-268">İstek Kimliği geçirme</span><span class="sxs-lookup"><span data-stu-id="1b3bf-268">Passing a request ID</span></span>
<span data-ttu-id="1b3bf-269">SDK eski sürümleri üzerinde bir istek kimliği ayarlayabilirsiniz `SearchServiceClient` veya `SearchIndexClient` ve her istek için REST API dahil.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-269">In older versions of the SDK, you could set a request ID on the `SearchServiceClient` or `SearchIndexClient` and it would be included in every request to the REST API.</span></span> <span data-ttu-id="1b3bf-270">Bu, destek ile iletişime geçmeniz gerekiyorsa arama hizmetinizi sorunlarını gidermek için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-270">This is useful for troubleshooting issues with your search service if you need to contact support.</span></span> <span data-ttu-id="1b3bf-271">Bununla birlikte, her işlem için bir benzersiz istek kimliği ayarlamak için yerine tüm işlemler için aynı kimlik kullanmak için daha yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-271">However, it is more useful to set a unique request ID for every operation rather than to use the same ID for all operations.</span></span> <span data-ttu-id="1b3bf-272">Bu nedenle, `SetClientRequestId` yöntemlerinin `SearchServiceClient` ve `SearchIndexClient` kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-272">For this reason, the `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="1b3bf-273">Bunun yerine, bir istek kimliği her işlemi yöntemi isteğe bağlı geçirebilirsiniz `SearchRequestOptions` parametresi.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-273">Instead, you can pass a request ID to each operation method via the optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="1b3bf-274">Gelecekteki bir SDK sürümünde, diğer Azure SDK tarafından kullanılan bir yaklaşım ile tutarlı olan bir istek kimliği nesneler genel istemcide ayarlamak için yeni bir yöntem ekleyeceğiz.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-274">In a future release of the SDK, we will add a new mechanism for setting a request ID globally on the client objects that is consistent with the approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="1b3bf-275">Örnek</span><span class="sxs-lookup"><span data-stu-id="1b3bf-275">Example</span></span>
<span data-ttu-id="1b3bf-276">Şuna benzer bir kod varsa:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="1b3bf-277">Bu yapı hataları düzeltmek için bunu değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-277">You can change it to this to fix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="1b3bf-278">Arabirim adı değişikliği</span><span class="sxs-lookup"><span data-stu-id="1b3bf-278">Interface name changes</span></span>
<span data-ttu-id="1b3bf-279">İşlem grubu arabirimi adları tüm karşılık gelen özellik adları ile tutarlı olacak şekilde değiştirilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-279">The operation group interface names have all changed to be consistent with their corresponding property names:</span></span>

* <span data-ttu-id="1b3bf-280">Türü `ISearchServiceClient.Indexes` adlandırılmıştır `IIndexOperations` için `IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-280">The type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` to `IIndexesOperations`.</span></span>
* <span data-ttu-id="1b3bf-281">Türü `ISearchServiceClient.Indexers` adlandırılmıştır `IIndexerOperations` için `IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-281">The type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` to `IIndexersOperations`.</span></span>
* <span data-ttu-id="1b3bf-282">Türü `ISearchServiceClient.DataSources` adlandırılmıştır `IDataSourceOperations` için `IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-282">The type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` to `IDataSourcesOperations`.</span></span>
* <span data-ttu-id="1b3bf-283">Türü `ISearchIndexClient.Documents` adlandırılmıştır `IDocumentOperations` için `IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-283">The type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` to `IDocumentsOperations`.</span></span>

<span data-ttu-id="1b3bf-284">Bu değişiklik, test amacıyla bu arabirimleri mocks oluşturduğunuz sürece kodunuzu etkilemek olası değil.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-284">This change is unlikely to affect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="1b3bf-285">Hata düzeltmeleri sürüm 1.1</span><span class="sxs-lookup"><span data-stu-id="1b3bf-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="1b3bf-286">Eski sürümleri, Azure Search .NET SDK özel model sınıfları serileştirmek için ilgili bir hata vardı.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-286">There was a bug in older versions of the Azure Search .NET SDK relating to serialization of custom model classes.</span></span> <span data-ttu-id="1b3bf-287">Bir null değer türünde bir özellik özel model sınıfı oluşturduysanız, bu hata oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-287">The bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-to-reproduce"></a><span data-ttu-id="1b3bf-288">Yeniden oluşturma adımları</span><span class="sxs-lookup"><span data-stu-id="1b3bf-288">Steps to reproduce</span></span>
<span data-ttu-id="1b3bf-289">Bir özel model sınıfı null değer türünde bir özellik oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="1b3bf-290">Örneğin, bir ortak ekleyin `UnitCount` türündeki özelliği `int` yerine `int?`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="1b3bf-291">Varsayılan değer bu tür bir belgeyle sıralıyorsanız (örneğin, 0 `int`), alanın Azure Search'te null olur.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-291">If you index a document with the default value of that type (for example, 0 for `int`), the field will be null in Azure Search.</span></span> <span data-ttu-id="1b3bf-292">Daha sonra bu belge için arama yaparsanız `Search` çağrısı throw `JsonSerializationException` , onu dönüştürülemiyor şikayetçi `null` için `int`.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-292">If you subsequently search for that document, the `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` to `int`.</span></span>

<span data-ttu-id="1b3bf-293">Ayrıca, filtreleri null amaçlanan değer yerine dizine yazıldı beri beklendiği gibi çalışmayabilir.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-293">Also, filters may not work as expected since null was written to the index instead of the intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="1b3bf-294">Ayrıntılar Düzelt</span><span class="sxs-lookup"><span data-stu-id="1b3bf-294">Fix details</span></span>
<span data-ttu-id="1b3bf-295">Sürüm SDK 1.1 Biz bu sorunu düzelttik.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-295">We have fixed this issue in version 1.1 of the SDK.</span></span> <span data-ttu-id="1b3bf-296">Şimdi, böyle bir model sınıfı varsa:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="1b3bf-297">ve ayarladığınız `IntValue` 0 olarak bu değer şimdi doğru hattaki 0 olarak serileştirilmiş ve dizindeki 0 olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-297">and you set `IntValue` to 0, that value is now correctly serialized as 0 on the wire and stored as 0 in the index.</span></span> <span data-ttu-id="1b3bf-298">Yuvarlak tripping de beklendiği gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="1b3bf-299">Bu yaklaşımda farkında olması için bir olası sorun: bir model türü ile atanamayan bir özellik kullanırsanız, için sahip **garanti** hiçbir belgeleri dizininize karşılık gelen alan için bir null değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-299">There is one potential issue to be aware of with this approach: If you use a model type with a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="1b3bf-300">Bunu zorlamanıza ne SDK ne de Azure Search REST API'sini yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-300">Neither the SDK nor the Azure Search REST API will help you to enforce this.</span></span>

<span data-ttu-id="1b3bf-301">Bu yalnızca kuramsal bir sorun değildir: Var olan `Edm.Int32` türünde bir dizine yeni bir alan eklediğiniz bir senaryoyu düşünün.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="1b3bf-302">Dizin tanımını güncelleştirdikten sonra, tüm belgelerin bu yeni alan için boş bir değeri olur (bunun nedeni, Azure Search'te tüm türlerin boş değer atanabilir olmasıdır).</span><span class="sxs-lookup"><span data-stu-id="1b3bf-302">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="1b3bf-303">Ardından bu alan için boş değer atanamayan bir `int` özelliğiyle bir model sınıfı kullanırsanız belgeleri almaya çalışırken bunun gibi bir `JsonSerializationException` alırsınız:</span><span class="sxs-lookup"><span data-stu-id="1b3bf-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="1b3bf-304">Bu nedenle, hala bir en iyi uygulama olarak model sınıflarınızda boş değer atanabilir türler kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="1b3bf-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="1b3bf-305">Bu hatayı ve düzeltme hakkında daha fazla ayrıntı için lütfen bkz. [github'daki bu sorunu](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="1b3bf-305">For more details on this bug and the fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

