---
title: "Azure Search'te aaaHow toomodel karmaşık veri türleri | Microsoft Docs"
description: "İç içe geçmiş veya hiyerarşik veri yapılarını düzleştirilmiş satır kümesi ve koleksiyonları veri türünü kullanarak Azure Search dizini içinde modellenebilir."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a><span data-ttu-id="ad494-103">Azure Search'te nasıl toomodel karmaşık veri türleri</span><span class="sxs-lookup"><span data-stu-id="ad494-103">How toomodel complex data types in Azure Search</span></span>
<span data-ttu-id="ad494-104">Dış veri kümeleri, Azure Search dizini bazen düzgünce tablo satır kümesine bozmadığını hiyerarşik veya iç içe substructures dahil toopopulate kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ad494-104">External datasets used toopopulate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="ad494-105">Bu tür yapıları örnekleri birden çok konumda ve telefon numaraları, tek bir rehberi birden çok yazar gibi tek bir SKU için tek bir müşteri, birden çok renkleri ve boyutları içerir ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="ad494-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="ad494-106">Koşulları modelleme içinde bu yapıları başvurulan tooas görebilirsiniz *karmaşık veri türlerini*, *bileşik veri türleri*, *bileşik veri türleri*, veya *toplama veri türleri*, az bir tooname.</span><span class="sxs-lookup"><span data-stu-id="ad494-106">In modeling terms, you might see these structures referred tooas *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, tooname a few.</span></span>

<span data-ttu-id="ad494-107">Karmaşık veri türleri yerel olarak Azure arama desteklenmez, ancak kanıtlanmış bir geçici çözüm hello yapısı düzleştirme ve ardından kullanarak iki adımlı bir işlem içerir bir **koleksiyonu** veri türü tooreconstitute hello iç yapısı.</span><span class="sxs-lookup"><span data-stu-id="ad494-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening hello structure and then using a **Collection** data type tooreconstitute hello interior structure.</span></span> <span data-ttu-id="ad494-108">Bu makalede açıklanan hello tekniği aşağıdaki hello içerik toobe Aranan, modellenmiş, filtre ve sıralanmış sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad494-108">Following hello technique described in this article allows hello content toobe searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="ad494-109">Karmaşık veri yapısı örneği</span><span class="sxs-lookup"><span data-stu-id="ad494-109">Example of a complex data structure</span></span>
<span data-ttu-id="ad494-110">Genellikle, söz konusu hello veri JSON veya XML belgeleri kümesi olarak ya da Azure Cosmos DB gibi bir NoSQL deposundaki öğeleri olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="ad494-110">Typically, hello data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="ad494-111">Yapısal olarak, arama ve filtre toobe gereken birden çok alt öğe olmaktan hello sınama kaynaklandığını.</span><span class="sxs-lookup"><span data-stu-id="ad494-111">Structurally, hello challenge stems from having multiple child items that need toobe searched and filtered.</span></span>  <span data-ttu-id="ad494-112">Merhaba geçici çözüm gösteren için başlangıç noktası olarak kişiler bir dizi örnek olarak listeler JSON belgesi aşağıdaki hello alın:</span><span class="sxs-lookup"><span data-stu-id="ad494-112">As a starting point for illustrating hello workaround, take hello following JSON document that lists a set of contacts as an example:</span></span>

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

<span data-ttu-id="ad494-113">'ID' Hello alanları adlı olsa da, 'name' ve 'şirket' kolayca bire bir Azure Search dizini içinde alanlar olarak eşlenebilir, hem bir dizi konumu açıklamaları yanı sıra konumu kimlikleri sahip konumları, bir dizi hello 'konumları' alan içerir.</span><span class="sxs-lookup"><span data-stu-id="ad494-113">While hello fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, hello ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="ad494-114">Azure Search bu destekleyen bir veri türü yok koşuluyla, farklı bir şekilde toomodel Azure Search'te gerekli.</span><span class="sxs-lookup"><span data-stu-id="ad494-114">Given that Azure Search does not have a data type that supports this, we need a different way toomodel this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="ad494-115">Bu teknik de blog postasına Kirk Evans tarafından açıklanan [Azure Search dizini oluşturma DocumentDB](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), "yapabildiği sahip olduğunuz adlı bir alan düzleştirme hello verilerin", adında bir teknik gösterir `locationsID` ve `locationsDescription` her ikisi de olan [koleksiyonları](https://msdn.microsoft.com/library/azure/dn798938.aspx) (veya bir dizeler dizisi).</span><span class="sxs-lookup"><span data-stu-id="ad494-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening hello data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a><span data-ttu-id="ad494-116">1. Kısım: hello dizi tek tek alanlarına düzleştirmek</span><span class="sxs-lookup"><span data-stu-id="ad494-116">Part 1: Flatten hello array into individual fields</span></span>
<span data-ttu-id="ad494-117">toocreate bu veri kümesi düzenler bir Azure Search dizini oluşturma hello iç içe geçmiş düzeltilebilmenize alanları tek tek: `locationsID` ve `locationsDescription` veri türüne sahip [koleksiyonları](https://msdn.microsoft.com/library/azure/dn798938.aspx) (veya bir dizeler dizisi).</span><span class="sxs-lookup"><span data-stu-id="ad494-117">toocreate an Azure Search index that accommodates this dataset, create individual fields for hello nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="ad494-118">Bu alanları hello '1' ve '2' hello değerlerini dizin `locationsID` alanında Hasan Aydın ve başlangıç değerleri '3' & '4' hello içine `locationsID` Jen Campbell için alan.</span><span class="sxs-lookup"><span data-stu-id="ad494-118">In these fields you would index hello values ‘1’ and ‘2’ into hello `locationsID` field for John Smith and hello values ‘3’ & ‘4’ into hello `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="ad494-119">Verilerinizi Azure Search içinde şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="ad494-119">Your data within Azure Search would look like this:</span></span> 

![Örnek veriler, 2 satır](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a><span data-ttu-id="ad494-121">2. Bölüm: Merhaba dizin tanımında koleksiyonu alan ekleme</span><span class="sxs-lookup"><span data-stu-id="ad494-121">Part 2: Add a collection field in hello index definition</span></span>
<span data-ttu-id="ad494-122">Merhaba dizin şemasında benzer toothis örnek hello alan başvuruları görünebilir.</span><span class="sxs-lookup"><span data-stu-id="ad494-122">In hello index schema, hello field definitions might look similar toothis example.</span></span>

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a><span data-ttu-id="ad494-123">Arama davranışlarını doğrulamak ve isteğe bağlı olarak hello dizin genişletme</span><span class="sxs-lookup"><span data-stu-id="ad494-123">Validate search behaviors and optionally extend hello index</span></span>
<span data-ttu-id="ad494-124">Oluşturulan hello dizin ve yüklenen hello veri varsayıldığında, artık hello çözüm tooverify arama sorgusu yürütme hello dataset karşı test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad494-124">Assuming you created hello index and loaded hello data, you can now test hello solution tooverify search query execution against hello dataset.</span></span> <span data-ttu-id="ad494-125">Her **koleksiyonu** alan olmalıdır **aranabilir**, **filtrelenebilir** ve **modellenebilir**.</span><span class="sxs-lookup"><span data-stu-id="ad494-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="ad494-126">Mümkün toorun sorguları gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="ad494-126">You should be able toorun queries like:</span></span>

* <span data-ttu-id="ad494-127">'Adventureworks Genel merkez' hello sırasında çalışan tüm kişilerin bulun.</span><span class="sxs-lookup"><span data-stu-id="ad494-127">Find all people who work at hello ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="ad494-128">'Giriş Office' çalışan kişilerin hello sayısı sayısını alır.</span><span class="sxs-lookup"><span data-stu-id="ad494-128">Get a count of hello number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="ad494-129">Çalışan bir 'giriş ofiste' hello kişiler her yerde hello kişi sayısı ile birlikte çalıştıkları diğer ofislerdeki gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad494-129">Of hello people who work at a ‘Home Office’, show what other offices they work along with a count of hello people in each location.</span></span>  

<span data-ttu-id="ad494-130">Toodo hem hello konum kimliği, hem de hello konum açıklaması birleştiren bir arama gerektiğinde burada bu yöntem parçalayın döner ' dir.</span><span class="sxs-lookup"><span data-stu-id="ad494-130">Where this technique falls apart is when you need toodo a search that combines both hello location id as well as hello location description.</span></span> <span data-ttu-id="ad494-131">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ad494-131">For example:</span></span>

* <span data-ttu-id="ad494-132">Bir giriş Office sahip oldukları tüm kişileri Bul ve 4'ün bir konum kimliği vardır.</span><span class="sxs-lookup"><span data-stu-id="ad494-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="ad494-133">Aşağıdaki gibi görünen hello özgün içerik geri çağırma varsa:</span><span class="sxs-lookup"><span data-stu-id="ad494-133">If you recall hello original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="ad494-134">Biz hello veri farklı alanlara ayrılmış, ancak hiçbir şekilde bilinmesiyle hello Jen Campbell için giriş Office çok ile ilişkili ise sahibiz`locationsID 3` veya `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="ad494-134">However, now that we have separated hello data into separate fields, we have no way of knowing if hello Home Office for Jen Campbell relates too`locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="ad494-135">Bu durumda toohandle hello verilerin tümü tek bir koleksiyona birleştirir hello dizindeki başka bir alan tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="ad494-135">toohandle this case, define another field in hello index that combines all of hello data into a single collection.</span></span>  <span data-ttu-id="ad494-136">Bizim örneğimizde, biz Bu alan çağıracak `locationsCombined` ve biz hello içerikle ayıracak bir `||` düşündüğünüz ayırıcı karakter içeriğiniz için benzersiz bir dizi olacaktır seçebilmenize rağmen.</span><span class="sxs-lookup"><span data-stu-id="ad494-136">For our example, we will call this field `locationsCombined` and we will separate hello content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="ad494-137">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ad494-137">For example:</span></span> 

![Örnek veriler, 2 satır ayırıcı ile](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="ad494-139">Bu kullanarak `locationsCombined` alan, biz şimdi uyum sağlayacak daha da fazla sorguları gibi:</span><span class="sxs-lookup"><span data-stu-id="ad494-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="ad494-140">Bir 'giriş ofiste' konum kimliği ile '4' ın çalışan kişilerin sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ad494-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="ad494-141">Kimliği '4' konumu ile bir 'giriş ofiste' çalışan kişilerin arayın.</span><span class="sxs-lookup"><span data-stu-id="ad494-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="ad494-142">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="ad494-142">Limitations</span></span>
<span data-ttu-id="ad494-143">Bu teknik senaryolar sayısı için yararlıdır, ancak her durumda geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="ad494-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="ad494-144">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="ad494-144">For example:</span></span>

1. <span data-ttu-id="ad494-145">Karmaşık veri türünüz alanları statik kümesine sahip değil ve hiçbir şekilde toomap vardı tüm hello olası tooa tek alan türleri.</span><span class="sxs-lookup"><span data-stu-id="ad494-145">If you do not have a static set of fields in your complex data type and there was no way toomap all hello possible types tooa single field.</span></span> 
2. <span data-ttu-id="ad494-146">İç içe geçmiş hello nesnelerini güncelleştirme bazı ek çalışmalar toodetermine tam olarak ne hello Azure Search dizinine güncelleştirilmiş toobe gerektiğini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ad494-146">Updating hello nested objects requires some extra work toodetermine exactly what needs toobe updated in hello Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="ad494-147">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="ad494-147">Sample code</span></span>
<span data-ttu-id="ad494-148">Nasıl tooindex karmaşık bir JSON verilerini Azure Search ayarlandığında örneği görmek ve bu veri kümesi bu üzerinden sorguları bir dizi yerine [GitHub deposuna](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="ad494-148">You can see an example on how tooindex a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="ad494-149">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="ad494-149">Next step</span></span>
<span data-ttu-id="ad494-150">[Karmaşık veri türleri için yerel destek için oy](https://feedback.azure.com/forums/263029-azure-search) hello Azure arama UserVoice üzerinde sayfasında ve herhangi bir ek giriş sağlamak göndermemizi istediğinizi tooconsider özellik uygulama ile ilgili.</span><span class="sxs-lookup"><span data-stu-id="ad494-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on hello Azure Search UserVoice page and provide any additional input that you’d like us tooconsider regarding feature implementation.</span></span> <span data-ttu-id="ad494-151">Doğrudan Twitter'da toome çıkışı de ulaşabilir @liamca.</span><span class="sxs-lookup"><span data-stu-id="ad494-151">You can also reach out toome directly on Twitter at @liamca.</span></span>

