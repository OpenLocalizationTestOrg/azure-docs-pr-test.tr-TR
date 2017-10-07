---
title: "aaaHow tooquery tablo verileri Azure Cosmos veritabanı? | Microsoft Belgeleri"
description: "Tooquery tablo verileri Azure Cosmos veritabanı öğrenin"
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
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a><span data-ttu-id="df2ae-104">Azure Cosmos DB: Kullanarak tooquery tablo verileri tablo API (Önizleme) nasıl hello?</span><span class="sxs-lookup"><span data-stu-id="df2ae-104">Azure Cosmos DB: How tooquery table data by using hello Table API (preview)?</span></span>

<span data-ttu-id="df2ae-105">Hello Azure Cosmos DB [tablo API](table-introduction.md) (Önizleme) destekleyen OData ve [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) anahtar/değer (tablo) verileri sorgular.</span><span class="sxs-lookup"><span data-stu-id="df2ae-105">hello Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="df2ae-106">Bu makalede görevleri aşağıdaki hello yer almaktadır:</span><span class="sxs-lookup"><span data-stu-id="df2ae-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="df2ae-107">Merhaba tablo API ile verileri Sorgulama</span><span class="sxs-lookup"><span data-stu-id="df2ae-107">Querying data with hello Table API</span></span>

<span data-ttu-id="df2ae-108">Merhaba bu makalede sorgularda kullanılan örnek aşağıdaki hello `People` tablosu:</span><span class="sxs-lookup"><span data-stu-id="df2ae-108">hello queries in this article use hello following sample `People` table:</span></span>

| <span data-ttu-id="df2ae-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="df2ae-109">PartitionKey</span></span> | <span data-ttu-id="df2ae-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="df2ae-110">RowKey</span></span> | <span data-ttu-id="df2ae-111">E-posta</span><span class="sxs-lookup"><span data-stu-id="df2ae-111">Email</span></span> | <span data-ttu-id="df2ae-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="df2ae-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df2ae-113">Harp</span><span class="sxs-lookup"><span data-stu-id="df2ae-113">Harp</span></span> | <span data-ttu-id="df2ae-114">Walter</span><span class="sxs-lookup"><span data-stu-id="df2ae-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="df2ae-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="df2ae-115">425-555-0101</span></span> |
| <span data-ttu-id="df2ae-116">Smith</span><span class="sxs-lookup"><span data-stu-id="df2ae-116">Smith</span></span> | <span data-ttu-id="df2ae-117">Ben</span><span class="sxs-lookup"><span data-stu-id="df2ae-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="df2ae-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="df2ae-118">425-555-0102</span></span> |
| <span data-ttu-id="df2ae-119">Smith</span><span class="sxs-lookup"><span data-stu-id="df2ae-119">Smith</span></span> | <span data-ttu-id="df2ae-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="df2ae-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="df2ae-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="df2ae-121">425-555-0104</span></span> | 

<span data-ttu-id="df2ae-122">Azure Cosmos DB hello Azure Table depolama API'leri ile uyumlu olduğundan [sorgulama tabloları ve varlıkları] bakın (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) kullanarak tooquery nasıl hello ile ilgili ayrıntılar için Tablo API.</span><span class="sxs-lookup"><span data-stu-id="df2ae-122">Because Azure Cosmos DB is compatible with hello Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how tooquery by using hello Table API.</span></span> 

<span data-ttu-id="df2ae-123">Azure Cosmos DB sunar hello premium özellikleri hakkında daha fazla bilgi için bkz: [Azure Cosmos DB: Tablo API](table-introduction.md) ve [hello .NET tablo API ile geliştirme](tutorial-develop-table-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="df2ae-123">For more information on hello premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with hello Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="df2ae-124">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="df2ae-124">Prerequisites</span></span>

<span data-ttu-id="df2ae-125">Bu sorguları toowork için bir Azure Cosmos DB hesabınız varsa ve hello kapsayıcısında varlık verilere sahip.</span><span class="sxs-lookup"><span data-stu-id="df2ae-125">For these queries toowork, you must have an Azure Cosmos DB account and have entity data in hello container.</span></span> <span data-ttu-id="df2ae-126">Bu yok?</span><span class="sxs-lookup"><span data-stu-id="df2ae-126">Don't have any of those?</span></span> <span data-ttu-id="df2ae-127">Tam hello [beş dakikalık quickstart](https://aka.ms/acdbtnetqs) veya hello [Geliştirici öğretici](https://aka.ms/acdbtabletut) toocreate bir hesap ve veritabanınızı doldurmak.</span><span class="sxs-lookup"><span data-stu-id="df2ae-127">Complete hello [five-minute quickstart](https://aka.ms/acdbtnetqs) or hello [developer tutorial](https://aka.ms/acdbtabletut) toocreate an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="df2ae-128">Sorgu PartitionKey ve RowKey</span><span class="sxs-lookup"><span data-stu-id="df2ae-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="df2ae-129">Bir varlığın birincil anahtarının Hello PartitionKey ve RowKey özellikler form için özel bir sözdizimi tooidentify hello varlık aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="df2ae-129">Because hello PartitionKey and RowKey properties form an entity's primary key, you can use hello following special syntax tooidentify hello entity:</span></span> 

<span data-ttu-id="df2ae-130">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="df2ae-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="df2ae-131">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="df2ae-131">**Results**</span></span>

| <span data-ttu-id="df2ae-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="df2ae-132">PartitionKey</span></span> | <span data-ttu-id="df2ae-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="df2ae-133">RowKey</span></span> | <span data-ttu-id="df2ae-134">E-posta</span><span class="sxs-lookup"><span data-stu-id="df2ae-134">Email</span></span> | <span data-ttu-id="df2ae-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="df2ae-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df2ae-136">Harp</span><span class="sxs-lookup"><span data-stu-id="df2ae-136">Harp</span></span> | <span data-ttu-id="df2ae-137">Walter</span><span class="sxs-lookup"><span data-stu-id="df2ae-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="df2ae-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="df2ae-138">425-555-0104</span></span> |

<span data-ttu-id="df2ae-139">Alternatif olarak, bu özellikleri hello bir parçası olarak belirtebilirsiniz `$filter` hello bölümü aşağıdaki gösterildiği gibi seçeneği.</span><span class="sxs-lookup"><span data-stu-id="df2ae-139">Alternatively, you can specify these properties as part of hello `$filter` option, as shown in hello following section.</span></span> <span data-ttu-id="df2ae-140">Merhaba anahtar özellik adlarının ve sabit değerleri büyük küçük harfe duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="df2ae-140">Note that hello key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="df2ae-141">Merhaba PartitionKey ve RowKey özellikleri dize türüdür.</span><span class="sxs-lookup"><span data-stu-id="df2ae-141">Both hello PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="df2ae-142">OData filtresini kullanarak sorgulama</span><span class="sxs-lookup"><span data-stu-id="df2ae-142">Query by using an OData filter</span></span>
<span data-ttu-id="df2ae-143">Bu kurallar, bir filtre dizesi oluşturulurken göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="df2ae-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="df2ae-144">OData protokolü belirtimi toocompare bir özellik tooa değeri Hello tarafından tanımlanan hello mantıksal işleçler kullanın.</span><span class="sxs-lookup"><span data-stu-id="df2ae-144">Use hello logical operators defined by hello OData Protocol Specification toocompare a property tooa value.</span></span> <span data-ttu-id="df2ae-145">Bir özellik tooa dinamik değeri karşılaştırılamıyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="df2ae-145">Note that you can't compare a property tooa dynamic value.</span></span> <span data-ttu-id="df2ae-146">Sütunlardan biri hello ifade bir sabit olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="df2ae-146">One side of hello expression must be a constant.</span></span> 
* <span data-ttu-id="df2ae-147">Merhaba özellik adı, işleç ve sabit değer URL kodlanmış boşluklarla ayrılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="df2ae-147">hello property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="df2ae-148">URL kodlu olarak bir boşluk `%20`.</span><span class="sxs-lookup"><span data-stu-id="df2ae-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="df2ae-149">Tüm parçalarını hello filtre dizesi büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="df2ae-149">All parts of hello filter string are case-sensitive.</span></span> 
* <span data-ttu-id="df2ae-150">Merhaba sabit değer hello olmalıdır aynı veri türü hello filtre tooreturn geçerli sonuçları düzenini hello özelliği olarak.</span><span class="sxs-lookup"><span data-stu-id="df2ae-150">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="df2ae-151">Desteklenen özellik türleri hakkında daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span><span class="sxs-lookup"><span data-stu-id="df2ae-151">For more information about supported property types, see [Understanding hello Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="df2ae-152">Nasıl toofilter tarafından hello PartitionKey gösteren örnek bir sorgu işte ve e-posta özellikleri bir OData kullanarak `$filter`.</span><span class="sxs-lookup"><span data-stu-id="df2ae-152">Here's an example query that shows how toofilter by hello PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="df2ae-153">**Sorgu**</span><span class="sxs-lookup"><span data-stu-id="df2ae-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="df2ae-154">Nasıl tooconstruct filtre ifadelerinde çeşitli veri türleri için daha fazla bilgi için bkz: [sorgulama tabloları ve varlıkları](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span><span class="sxs-lookup"><span data-stu-id="df2ae-154">For more information on how tooconstruct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="df2ae-155">**Sonuçları**</span><span class="sxs-lookup"><span data-stu-id="df2ae-155">**Results**</span></span>

| <span data-ttu-id="df2ae-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="df2ae-156">PartitionKey</span></span> | <span data-ttu-id="df2ae-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="df2ae-157">RowKey</span></span> | <span data-ttu-id="df2ae-158">E-posta</span><span class="sxs-lookup"><span data-stu-id="df2ae-158">Email</span></span> | <span data-ttu-id="df2ae-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="df2ae-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="df2ae-160">Ben</span><span class="sxs-lookup"><span data-stu-id="df2ae-160">Ben</span></span> |<span data-ttu-id="df2ae-161">Smith</span><span class="sxs-lookup"><span data-stu-id="df2ae-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="df2ae-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="df2ae-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="df2ae-163">LINQ kullanarak sorgulama</span><span class="sxs-lookup"><span data-stu-id="df2ae-163">Query by using LINQ</span></span> 
<span data-ttu-id="df2ae-164">Toohello karşılık gelen OData sorgu ifadeleri çevirir LINQ kullanarak da sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df2ae-164">You can also query by using LINQ, which translates toohello corresponding OData query expressions.</span></span> <span data-ttu-id="df2ae-165">.NET SDK kullanarak toobuild sorguları nasıl hello örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="df2ae-165">Here's an example of how toobuild queries by using hello .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="df2ae-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="df2ae-166">Next steps</span></span>

<span data-ttu-id="df2ae-167">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="df2ae-167">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="df2ae-168">Tablo API (Önizleme) kullanarak tooquery hello nasıl öğrendiniz</span><span class="sxs-lookup"><span data-stu-id="df2ae-168">Learned how tooquery by using hello Table API (preview)</span></span> 

<span data-ttu-id="df2ae-169">Toohello sonraki öğretici toolearn nasıl şimdi devam toodistribute verilerinizi genel.</span><span class="sxs-lookup"><span data-stu-id="df2ae-169">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="df2ae-170">Verilerinizi genel Dağıt</span><span class="sxs-lookup"><span data-stu-id="df2ae-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
