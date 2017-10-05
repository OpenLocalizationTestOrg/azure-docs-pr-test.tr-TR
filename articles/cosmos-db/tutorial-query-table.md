---
title: "Tablo verisi Azure Cosmos veritabanı nasıl? | Microsoft Belgeleri"
description: "Sorgu tablosu veri Azure Cosmos veritabanı hakkında bilgi edinin"
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: e59cfa85c6bf584e44bdc6e88cc19d67df390041
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api-preview"></a><span data-ttu-id="5e1ef-104">Azure Cosmos DB: Tablo API (Önizleme) kullanarak tablo verileri sorgulamak nasıl?</span><span class="sxs-lookup"><span data-stu-id="5e1ef-104">Azure Cosmos DB: How to query table data by using the Table API (preview)?</span></span>

<span data-ttu-id="5e1ef-105">Azure Cosmos DB [tablo API](table-introduction.md) (Önizleme) destekleyen OData ve [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) anahtar/değer (tablo) verileri sorgular.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-105">The Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="5e1ef-106">Bu makalede aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="5e1ef-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="5e1ef-107">Tablo API ile veri sorgulama</span><span class="sxs-lookup"><span data-stu-id="5e1ef-107">Querying data with the Table API</span></span>

<span data-ttu-id="5e1ef-108">Bu makalede sorgularda aşağıdaki örneği kullanın `People` tablosu:</span><span class="sxs-lookup"><span data-stu-id="5e1ef-108">The queries in this article use the following sample `People` table:</span></span>

| <span data-ttu-id="5e1ef-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="5e1ef-109">PartitionKey</span></span> | <span data-ttu-id="5e1ef-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="5e1ef-110">RowKey</span></span> | <span data-ttu-id="5e1ef-111">E-posta</span><span class="sxs-lookup"><span data-stu-id="5e1ef-111">Email</span></span> | <span data-ttu-id="5e1ef-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="5e1ef-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e1ef-113">Harp</span><span class="sxs-lookup"><span data-stu-id="5e1ef-113">Harp</span></span> | <span data-ttu-id="5e1ef-114">Walter</span><span class="sxs-lookup"><span data-stu-id="5e1ef-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="5e1ef-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="5e1ef-115">425-555-0101</span></span> |
| <span data-ttu-id="5e1ef-116">Smith</span><span class="sxs-lookup"><span data-stu-id="5e1ef-116">Smith</span></span> | <span data-ttu-id="5e1ef-117">Ben</span><span class="sxs-lookup"><span data-stu-id="5e1ef-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="5e1ef-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="5e1ef-118">425-555-0102</span></span> |
| <span data-ttu-id="5e1ef-119">Smith</span><span class="sxs-lookup"><span data-stu-id="5e1ef-119">Smith</span></span> | <span data-ttu-id="5e1ef-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="5e1ef-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="5e1ef-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="5e1ef-121">425-555-0104</span></span> | 

<span data-ttu-id="5e1ef-122">Azure Cosmos DB Azure Table depolama API'leri ile uyumlu olduğundan [sorgulama tabloları ve varlıkları] bakın (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) tablosunu kullanarak sorguya hakkında ayrıntılar için API.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-122">Because Azure Cosmos DB is compatible with the Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how to query by using the Table API.</span></span> 

<span data-ttu-id="5e1ef-123">Azure Cosmos DB sunar premium özellikleri hakkında daha fazla bilgi için bkz: [Azure Cosmos DB: Tablo API](table-introduction.md) ve [.NET içinde tablo API ile geliştirme](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="5e1ef-123">For more information on the premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with the Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5e1ef-124">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5e1ef-124">Prerequisites</span></span>

<span data-ttu-id="5e1ef-125">Bu sorguları çalışmak bir Azure Cosmos DB hesabınız varsa ve kapsayıcısında varlık verilere sahip.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-125">For these queries to work, you must have an Azure Cosmos DB account and have entity data in the container.</span></span> <span data-ttu-id="5e1ef-126">Bu yok?</span><span class="sxs-lookup"><span data-stu-id="5e1ef-126">Don't have any of those?</span></span> <span data-ttu-id="5e1ef-127">Tamamlamak [beş dakikalık quickstart](https://aka.ms/acdbtnetqs) veya [Geliştirici öğretici](https://aka.ms/acdbtabletut) bir hesap oluşturun ve veritabanınızı doldurmak için.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-127">Complete the [five-minute quickstart](https://aka.ms/acdbtnetqs) or the [developer tutorial](https://aka.ms/acdbtabletut) to create an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="5e1ef-128">Sorgu PartitionKey ve RowKey</span><span class="sxs-lookup"><span data-stu-id="5e1ef-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="5e1ef-129">Bir varlığın birincil anahtarının PartitionKey ve RowKey özellikler form için varlık tanımlamak için aşağıdaki özel söz dizimini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5e1ef-129">Because the PartitionKey and RowKey properties form an entity's primary key, you can use the following special syntax to identify the entity:</span></span> 

<span data-ttu-id="5e1ef-130">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="5e1ef-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="5e1ef-131">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="5e1ef-131">**Results**</span></span>

| <span data-ttu-id="5e1ef-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="5e1ef-132">PartitionKey</span></span> | <span data-ttu-id="5e1ef-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="5e1ef-133">RowKey</span></span> | <span data-ttu-id="5e1ef-134">E-posta</span><span class="sxs-lookup"><span data-stu-id="5e1ef-134">Email</span></span> | <span data-ttu-id="5e1ef-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="5e1ef-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e1ef-136">Harp</span><span class="sxs-lookup"><span data-stu-id="5e1ef-136">Harp</span></span> | <span data-ttu-id="5e1ef-137">Walter</span><span class="sxs-lookup"><span data-stu-id="5e1ef-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="5e1ef-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="5e1ef-138">425-555-0104</span></span> |

<span data-ttu-id="5e1ef-139">Alternatif olarak, bir parçası olarak bu özellikleri belirtebilirsiniz `$filter` , aşağıdaki bölümde gösterildiği gibi seçeneği.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-139">Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.</span></span> <span data-ttu-id="5e1ef-140">Anahtar özellik adlarının ve sabit değerleri büyük küçük harfe duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-140">Note that the key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="5e1ef-141">PartitionKey ve RowKey dize türünde özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-141">Both the PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="5e1ef-142">OData filtresini kullanarak sorgulama</span><span class="sxs-lookup"><span data-stu-id="5e1ef-142">Query by using an OData filter</span></span>
<span data-ttu-id="5e1ef-143">Bu kurallar, bir filtre dizesi oluşturulurken göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="5e1ef-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="5e1ef-144">Bir özellik için bir değer karşılaştırmak için OData Protokolü belirtim tarafından tanımlanan mantıksal işleçler kullanın.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-144">Use the logical operators defined by the OData Protocol Specification to compare a property to a value.</span></span> <span data-ttu-id="5e1ef-145">Özelliği dinamik bir değere karşılaştırılamıyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-145">Note that you can't compare a property to a dynamic value.</span></span> <span data-ttu-id="5e1ef-146">İfade bir tarafındaki bir sabit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-146">One side of the expression must be a constant.</span></span> 
* <span data-ttu-id="5e1ef-147">Özellik adı, işleç ve sabit değer URL kodlanmış boşluklarla ayrılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-147">The property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="5e1ef-148">URL kodlu olarak bir boşluk `%20`.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="5e1ef-149">Filtre dizesi tüm parçalarını büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-149">All parts of the filter string are case-sensitive.</span></span> 
* <span data-ttu-id="5e1ef-150">Geçerli sonuçları döndürmek için aynı veri türünde filtre sırasını özelliği olarak sabit değeri olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-150">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="5e1ef-151">Desteklenen özellik türleri hakkında daha fazla bilgi için bkz: [tablo hizmeti veri modelini anlama](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="5e1ef-151">For more information about supported property types, see [Understanding the Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="5e1ef-152">Bir OData kullanarak PartitionKey ve e-posta özellikleri tarafından filtre gösteren örnek bir sorgu işte `$filter`.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-152">Here's an example query that shows how to filter by the PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="5e1ef-153">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="5e1ef-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="5e1ef-154">Çeşitli veri türleri için filtre ifadeleri oluşturma hakkında daha fazla bilgi için bkz: [sorgulama tabloları ve varlıkları](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="5e1ef-154">For more information on how to construct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="5e1ef-155">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="5e1ef-155">**Results**</span></span>

| <span data-ttu-id="5e1ef-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="5e1ef-156">PartitionKey</span></span> | <span data-ttu-id="5e1ef-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="5e1ef-157">RowKey</span></span> | <span data-ttu-id="5e1ef-158">E-posta</span><span class="sxs-lookup"><span data-stu-id="5e1ef-158">Email</span></span> | <span data-ttu-id="5e1ef-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="5e1ef-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5e1ef-160">Ben</span><span class="sxs-lookup"><span data-stu-id="5e1ef-160">Ben</span></span> |<span data-ttu-id="5e1ef-161">Smith</span><span class="sxs-lookup"><span data-stu-id="5e1ef-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="5e1ef-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="5e1ef-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="5e1ef-163">LINQ kullanarak sorgulama</span><span class="sxs-lookup"><span data-stu-id="5e1ef-163">Query by using LINQ</span></span> 
<span data-ttu-id="5e1ef-164">Karşılık gelen OData sorgu ifadeleri için çevirir LINQ kullanarak da sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-164">You can also query by using LINQ, which translates to the corresponding OData query expressions.</span></span> <span data-ttu-id="5e1ef-165">.NET SDK kullanarak sorgu oluşturma konusunda bir örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5e1ef-165">Here's an example of how to build queries by using the .NET SDK:</span></span>

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a><span data-ttu-id="5e1ef-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5e1ef-166">Next steps</span></span>

<span data-ttu-id="5e1ef-167">Bu öğreticide, aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="5e1ef-167">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5e1ef-168">Tablo API (Önizleme) kullanarak sorgulama öğrendiniz</span><span class="sxs-lookup"><span data-stu-id="5e1ef-168">Learned how to query by using the Table API (preview)</span></span> 

<span data-ttu-id="5e1ef-169">Verilerinizi Genel dağıtma konusunda bilgi almak için sonraki öğretici şimdi devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e1ef-169">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e1ef-170">Verilerinizi genel Dağıt</span><span class="sxs-lookup"><span data-stu-id="5e1ef-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
