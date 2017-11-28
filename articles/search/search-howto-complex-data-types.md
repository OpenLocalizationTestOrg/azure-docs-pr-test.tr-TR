---
title: "Azure Search'te karmaşık veri türlerini modellemek nasıl | Microsoft Docs"
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
ms.openlocfilehash: d576fd7bb267ae7a100589413185b595e3b2be42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-model-complex-data-types-in-azure-search"></a><span data-ttu-id="36901-103">Azure Search'te model karmaşık veri türleri hakkında</span><span class="sxs-lookup"><span data-stu-id="36901-103">How to model complex data types in Azure Search</span></span>
<span data-ttu-id="36901-104">Azure Search dizini bazen doldurmak için kullanılan dış veri kümeleri düzgünce tablo satır kümesine bozmadığını hiyerarşik veya iç içe substructures içerir.</span><span class="sxs-lookup"><span data-stu-id="36901-104">External datasets used to populate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="36901-105">Bu tür yapıları örnekleri birden çok konumda ve telefon numaraları, tek bir rehberi birden çok yazar gibi tek bir SKU için tek bir müşteri, birden çok renkleri ve boyutları içerir ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="36901-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="36901-106">Koşulları modelleme içinde olarak adlandırılan bu yapıları görebilirsiniz *karmaşık veri türlerini*, *bileşik veri türleri*, *bileşik veri türleri*, veya *veri türleri bir araya*, birkaçıdır.</span><span class="sxs-lookup"><span data-stu-id="36901-106">In modeling terms, you might see these structures referred to as *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, to name a few.</span></span>

<span data-ttu-id="36901-107">Karmaşık veri türleri yerel olarak Azure arama desteklenmez, ancak kanıtlanmış bir geçici çözüm yapısı düzleştirme ve ardından kullanarak iki adımlı bir işlem içerir bir **koleksiyonu** veri türü iç yapısı yeniden oluşturma.</span><span class="sxs-lookup"><span data-stu-id="36901-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening the structure and then using a **Collection** data type to reconstitute the interior structure.</span></span> <span data-ttu-id="36901-108">Bu makalede açıklanan teknikleri aşağıdaki aranması içerik filtre ve sıralanmış modellenmiş, sağlar.</span><span class="sxs-lookup"><span data-stu-id="36901-108">Following the technique described in this article allows the content to be searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="36901-109">Karmaşık veri yapısı örneği</span><span class="sxs-lookup"><span data-stu-id="36901-109">Example of a complex data structure</span></span>
<span data-ttu-id="36901-110">Genellikle, söz konusu veri JSON veya XML belgeleri kümesi olarak ya da Azure Cosmos DB gibi bir NoSQL deposundaki öğeleri olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="36901-110">Typically, the data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="36901-111">Yapısal olarak, arama ve filtre gereken birden çok alt öğe olmaktan challenge kaynaklandığını.</span><span class="sxs-lookup"><span data-stu-id="36901-111">Structurally, the challenge stems from having multiple child items that need to be searched and filtered.</span></span>  <span data-ttu-id="36901-112">Geçici çözüm gösteren için başlangıç noktası olarak kişiler bir dizi örnek olarak listeler aşağıdaki JSON belgesini alın:</span><span class="sxs-lookup"><span data-stu-id="36901-112">As a starting point for illustrating the workaround, take the following JSON document that lists a set of contacts as an example:</span></span>

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

<span data-ttu-id="36901-113">'ID' alanları adlı olsa da, 'name' ve 'şirket' kolayca bire bir Azure Search dizini içinde alanlar olarak eşlenebilir, hem bir dizi konumu açıklamaları yanı sıra konumu kimlikleri sahip konumları, bir dizi 'konumları' alan içerir.</span><span class="sxs-lookup"><span data-stu-id="36901-113">While the fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, the ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="36901-114">O Azure Search bu destekleyen bir veri türüne sahip değil, Azure Search'te Bu model için farklı bir şekilde ihtiyacımız var.</span><span class="sxs-lookup"><span data-stu-id="36901-114">Given that Azure Search does not have a data type that supports this, we need a different way to model this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="36901-115">Bu tekniği de blog postasına Kirk Evans tarafından açıklanan [Azure Search dizini oluşturma DocumentDB](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), "veri düzleştirme" adında bir teknik gösterir adlı bir alan olurdu aslına `locationsID` ve `locationsDescription` her ikisi de olan [koleksiyonları](https://msdn.microsoft.com/library/azure/dn798938.aspx) (veya bir dizeler dizisi).</span><span class="sxs-lookup"><span data-stu-id="36901-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening the data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-the-array-into-individual-fields"></a><span data-ttu-id="36901-116">1. Kısım: dizi tek tek alanlarına düzleştirmek</span><span class="sxs-lookup"><span data-stu-id="36901-116">Part 1: Flatten the array into individual fields</span></span>
<span data-ttu-id="36901-117">Bu veri kümesi düzenler bir Azure Search dizini oluşturmak için iç içe geçmiş düzeltilebilmenize alanları tek tek oluşturun: `locationsID` ve `locationsDescription` veri türüne sahip [koleksiyonları](https://msdn.microsoft.com/library/azure/dn798938.aspx) (veya bir dizeler dizisi).</span><span class="sxs-lookup"><span data-stu-id="36901-117">To create an Azure Search index that accommodates this dataset, create individual fields for the nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="36901-118">Bu alanları içine değerleri '1' ve '2' dizini `locationsID` alanında Hasan Aydın ve değerleri '3' & '4' için içine `locationsID` Jen Campbell için alan.</span><span class="sxs-lookup"><span data-stu-id="36901-118">In these fields you would index the values ‘1’ and ‘2’ into the `locationsID` field for John Smith and the values ‘3’ & ‘4’ into the `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="36901-119">Verilerinizi Azure Search içinde şöyle olabilir:</span><span class="sxs-lookup"><span data-stu-id="36901-119">Your data within Azure Search would look like this:</span></span> 

![Örnek veriler, 2 satır](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-the-index-definition"></a><span data-ttu-id="36901-121">2. Kısım: Dizin tanımı'nda koleksiyonu alan ekleme</span><span class="sxs-lookup"><span data-stu-id="36901-121">Part 2: Add a collection field in the index definition</span></span>
<span data-ttu-id="36901-122">Dizin şemasında alan tanımları bu örneğe benzer görünür.</span><span class="sxs-lookup"><span data-stu-id="36901-122">In the index schema, the field definitions might look similar to this example.</span></span>

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

## <a name="validate-search-behaviors-and-optionally-extend-the-index"></a><span data-ttu-id="36901-123">Arama davranışlarını doğrulamak ve isteğe bağlı olarak dizin genişletme</span><span class="sxs-lookup"><span data-stu-id="36901-123">Validate search behaviors and optionally extend the index</span></span>
<span data-ttu-id="36901-124">Dizin oluşturulur ve veriler yüklü olduğu varsayılarak, arama sorgu yürütme dataset karşı doğrulamak için çözüm artık test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="36901-124">Assuming you created the index and loaded the data, you can now test the solution to verify search query execution against the dataset.</span></span> <span data-ttu-id="36901-125">Her **koleksiyonu** alan olmalıdır **aranabilir**, **filtrelenebilir** ve **modellenebilir**.</span><span class="sxs-lookup"><span data-stu-id="36901-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="36901-126">Sorgular gibi çalışır olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="36901-126">You should be able to run queries like:</span></span>

* <span data-ttu-id="36901-127">'Adventureworks merkezde' çalışan tüm kişilerin bulun.</span><span class="sxs-lookup"><span data-stu-id="36901-127">Find all people who work at the ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="36901-128">'Giriş Office' çalışan kişilerin sayısını alır.</span><span class="sxs-lookup"><span data-stu-id="36901-128">Get a count of the number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="36901-129">Bir 'giriş ofiste' çalışan kişilerin her yerde kişiler sayısını birlikte çalıştıkları diğer ofislerdeki gösterir.</span><span class="sxs-lookup"><span data-stu-id="36901-129">Of the people who work at a ‘Home Office’, show what other offices they work along with a count of the people in each location.</span></span>  

<span data-ttu-id="36901-130">Hem konum kimliği, hem de konum açıklaması birleştiren bir arama yapmak gerektiğinde burada bu yöntem parçalayın döner olur.</span><span class="sxs-lookup"><span data-stu-id="36901-130">Where this technique falls apart is when you need to do a search that combines both the location id as well as the location description.</span></span> <span data-ttu-id="36901-131">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="36901-131">For example:</span></span>

* <span data-ttu-id="36901-132">Bir giriş Office sahip oldukları tüm kişileri Bul ve 4'ün bir konum kimliği vardır.</span><span class="sxs-lookup"><span data-stu-id="36901-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="36901-133">Özgün içerik arama şu şekilde geri çağırma varsa:</span><span class="sxs-lookup"><span data-stu-id="36901-133">If you recall the original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="36901-134">Biz verilerin farklı alanlara ayrılmış, Jen Campbell teklifiyle için ancak biz olduğunu bilerek if giriş Office zorlaması `locationsID 3` veya `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="36901-134">However, now that we have separated the data into separate fields, we have no way of knowing if the Home Office for Jen Campbell relates to `locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="36901-135">Bu durumu işlemek için tüm verileri tek bir koleksiyona birleştirir dizindeki başka bir alan tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="36901-135">To handle this case, define another field in the index that combines all of the data into a single collection.</span></span>  <span data-ttu-id="36901-136">Bizim örneğimizde, biz Bu alan çağıracak `locationsCombined` ve biz içerikle ayıracak bir `||` düşündüğünüz ayırıcı karakter içeriğiniz için benzersiz bir dizi olacaktır seçebilmenize rağmen.</span><span class="sxs-lookup"><span data-stu-id="36901-136">For our example, we will call this field `locationsCombined` and we will separate the content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="36901-137">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="36901-137">For example:</span></span> 

![Örnek veriler, 2 satır ayırıcı ile](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="36901-139">Bu kullanarak `locationsCombined` alan, biz şimdi uyum sağlayacak daha da fazla sorguları gibi:</span><span class="sxs-lookup"><span data-stu-id="36901-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="36901-140">Bir 'giriş ofiste' konum kimliği ile '4' ın çalışan kişilerin sayısını gösterir.</span><span class="sxs-lookup"><span data-stu-id="36901-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="36901-141">Kimliği '4' konumu ile bir 'giriş ofiste' çalışan kişilerin arayın.</span><span class="sxs-lookup"><span data-stu-id="36901-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="36901-142">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="36901-142">Limitations</span></span>
<span data-ttu-id="36901-143">Bu teknik senaryolar sayısı için yararlıdır, ancak her durumda geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="36901-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="36901-144">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="36901-144">For example:</span></span>

1. <span data-ttu-id="36901-145">Varsa, karmaşık veri türü statik alanları kümesine sahip değildir ve olası tüm türler için tek bir alanı eşlemek için hiçbir yolu yoktu.</span><span class="sxs-lookup"><span data-stu-id="36901-145">If you do not have a static set of fields in your complex data type and there was no way to map all the possible types to a single field.</span></span> 
2. <span data-ttu-id="36901-146">İç içe geçmiş nesnelerde Güncelleştirme ne Azure Search dizini güncelleştirilmesi gerektiğinde tam olarak belirlemek için bazı ek çalışmalar gerektirir</span><span class="sxs-lookup"><span data-stu-id="36901-146">Updating the nested objects requires some extra work to determine exactly what needs to be updated in the Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="36901-147">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="36901-147">Sample code</span></span>
<span data-ttu-id="36901-148">Karmaşık bir JSON veri kümesi Azure Search dizini oluşturmak ve bu veri kümesi bu üzerinden sorguları bir dizi yerine konusunda bir örnek görebilirsiniz [GitHub deposuna](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="36901-148">You can see an example on how to index a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="36901-149">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="36901-149">Next step</span></span>
<span data-ttu-id="36901-150">[Karmaşık veri türleri için yerel destek için oy](https://feedback.azure.com/forums/263029-azure-search) üzerinde Azure arama UserVoice sayfasında ve bize özellik uygulamasıyla ilgili dikkate alınması gereken istediğiniz herhangi bir ek giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="36901-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on the Azure Search UserVoice page and provide any additional input that you’d like us to consider regarding feature implementation.</span></span> <span data-ttu-id="36901-151">Da bana doğrudan Twitter'da ulaşabilirsiniz @liamca.</span><span class="sxs-lookup"><span data-stu-id="36901-151">You can also reach out to me directly on Twitter at @liamca.</span></span>

