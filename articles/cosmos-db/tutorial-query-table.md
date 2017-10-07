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
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a>Azure Cosmos DB: Kullanarak tooquery tablo verileri tablo API (Önizleme) nasıl hello?

Hello Azure Cosmos DB [tablo API](table-introduction.md) (Önizleme) destekleyen OData ve [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) anahtar/değer (tablo) verileri sorgular.  

Bu makalede görevleri aşağıdaki hello yer almaktadır: 

> [!div class="checklist"]
> * Merhaba tablo API ile verileri Sorgulama

Merhaba bu makalede sorgularda kullanılan örnek aşağıdaki hello `People` tablosu:

| PartitionKey | RowKey | E-posta | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jeff | Jeff@contoso.com| 425-555-0104 | 

Azure Cosmos DB hello Azure Table depolama API'leri ile uyumlu olduğundan [sorgulama tabloları ve varlıkları] bakın (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) kullanarak tooquery nasıl hello ile ilgili ayrıntılar için Tablo API. 

Azure Cosmos DB sunar hello premium özellikleri hakkında daha fazla bilgi için bkz: [Azure Cosmos DB: Tablo API](table-introduction.md) ve [hello .NET tablo API ile geliştirme](tutorial-develop-table-dotnet.md). 

## <a name="prerequisites"></a>Ön koşullar

Bu sorguları toowork için bir Azure Cosmos DB hesabınız varsa ve hello kapsayıcısında varlık verilere sahip. Bu yok? Tam hello [beş dakikalık quickstart](https://aka.ms/acdbtnetqs) veya hello [Geliştirici öğretici](https://aka.ms/acdbtabletut) toocreate bir hesap ve veritabanınızı doldurmak.

## <a name="query-on-partitionkey-and-rowkey"></a>Sorgu PartitionKey ve RowKey
Bir varlığın birincil anahtarının Hello PartitionKey ve RowKey özellikler form için özel bir sözdizimi tooidentify hello varlık aşağıdaki hello kullanabilirsiniz: 

**Sorgu**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**Sonuçları**

| PartitionKey | RowKey | E-posta | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

Alternatif olarak, bu özellikleri hello bir parçası olarak belirtebilirsiniz `$filter` hello bölümü aşağıdaki gösterildiği gibi seçeneği. Merhaba anahtar özellik adlarının ve sabit değerleri büyük küçük harfe duyarlı olduğunu unutmayın. Merhaba PartitionKey ve RowKey özellikleri dize türüdür. 

## <a name="query-by-using-an-odata-filter"></a>OData filtresini kullanarak sorgulama
Bu kurallar, bir filtre dizesi oluşturulurken göz önünde bulundurun: 

* OData protokolü belirtimi toocompare bir özellik tooa değeri Hello tarafından tanımlanan hello mantıksal işleçler kullanın. Bir özellik tooa dinamik değeri karşılaştırılamıyor unutmayın. Sütunlardan biri hello ifade bir sabit olmalıdır. 
* Merhaba özellik adı, işleç ve sabit değer URL kodlanmış boşluklarla ayrılmış olması gerekir. URL kodlu olarak bir boşluk `%20`. 
* Tüm parçalarını hello filtre dizesi büyük/küçük harfe duyarlıdır. 
* Merhaba sabit değer hello olmalıdır aynı veri türü hello filtre tooreturn geçerli sonuçları düzenini hello özelliği olarak. Desteklenen özellik türleri hakkında daha fazla bilgi için bkz: [anlama hello tablo hizmeti veri modelini](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model). 

Nasıl toofilter tarafından hello PartitionKey gösteren örnek bir sorgu işte ve e-posta özellikleri bir OData kullanarak `$filter`.

**Sorgu**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

Nasıl tooconstruct filtre ifadelerinde çeşitli veri türleri için daha fazla bilgi için bkz: [sorgulama tabloları ve varlıkları](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).

**Sonuçları**

| PartitionKey | RowKey | E-posta | PhoneNumber |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>LINQ kullanarak sorgulama 
Toohello karşılık gelen OData sorgu ifadeleri çevirir LINQ kullanarak da sorgulayabilirsiniz. .NET SDK kullanarak toobuild sorguları nasıl hello örneği şöyledir:

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

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, hello aşağıdakileri yaptığınızdan:

> [!div class="checklist"]
> * Tablo API (Önizleme) kullanarak tooquery hello nasıl öğrendiniz 

Toohello sonraki öğretici toolearn nasıl şimdi devam toodistribute verilerinizi genel.

> [!div class="nextstepaction"]
> [Verilerinizi genel Dağıt](tutorial-global-distribution-documentdb.md)
