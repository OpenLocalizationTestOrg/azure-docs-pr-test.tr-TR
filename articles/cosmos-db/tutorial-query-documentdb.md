---
title: "SQL Azure Cosmos veritabanı ile aaaHow tooquery? | Microsoft Belgeleri"
description: "SQL Azure Cosmos veritabanı ile DocumentDB verilerle tooquery öğrenin"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: tutorial-develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: d3dc51acf92cb78d4f4d9dbac7ec54b1382431cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-using-sql"></a>Azure Cosmos DB: Nasıl SQL kullanarak tooquery?

Hello Azure Cosmos DB [DocumentDB API](documentdb-introduction.md) belgeleri SQL kullanarak sorgulama destekler. Bu makalede, örnek bir belge ve iki örnek SQL sorguları ve sonuçları sağlar.

Bu makalede görevleri aşağıdaki hello yer almaktadır: 

> [!div class="checklist"]
> * SQL ile veri sorgulama

## <a name="sample-document"></a>Örnek bir belge

Merhaba SQL sorgularını bu makaledeki örnek bir belge aşağıdaki hello kullanın.

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```
## <a name="where-can-i-run-sql-queries"></a>SQL sorguları yeri çalıştırabilir miyim?

Hello Veri Gezgini hello hello aracılığıyla Azure portal kullanarak sorguları çalıştırabilirsiniz [REST API ve SDK](documentdb-sdk-dotnet.md)ve hatta hello [Query playground](https://www.documentdb.com/sql/demo), var olan bir örnek veri kümesini temel sorguları çalıştırır.

SQL sorguları hakkında daha fazla bilgi için bkz:
* [SQL sorgusu ve SQL söz dizimi](documentdb-sql-query.md)

## <a name="prerequisites"></a>Ön koşullar

Bu öğretici bir Azure Cosmos DB hesap ve koleksiyon olduğunu varsayar. Bu yok? Tam hello [5 dakikalık quickstart](create-mongodb-nodejs.md) veya hello [Geliştirici öğretici](tutorial-develop-mongodb.md) toocreate bir hesap ve koleksiyonu.

## <a name="example-query-1"></a>Örnek sorgu 1

Merhaba örnek ailesi belge yukarıda verilen, SQL sorgusu aşağıdaki hello belgeleri hello Kimliği alanı eşleştiği döndürür `WakefieldFamily`. Olduğundan bir `SELECT *` ifadesi, hello sorgu hello çıktısını hello tam JSON belgesi şöyledir:

**Sorgu**

    SELECT * 
    FROM Families f 
    WHERE f.id = "WakefieldFamily"

**Sonuçları**

```json
{
  "id": "WakefieldFamily",
  "parents": [
      { "familyName": "Wakefield", "givenName": "Robin" },
      { "familyName": "Miller", "givenName": "Ben" }
  ],
  "children": [
      {
        "familyName": "Merriam", 
        "givenName": "Jesse", 
        "gender": "female", "grade": 1,
        "pets": [
            { "givenName": "Goofy" },
            { "givenName": "Shadow" }
        ]
      },
      { 
        "familyName": "Miller", 
         "givenName": "Lisa", 
         "gender": "female", 
         "grade": 8 }
  ],
  "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
  "creationDate": 1431620462,
  "isRegistered": false
}
```

## <a name="example-query-2"></a>Örnek Sorgu 2

Merhaba sonraki sorgunun döndürdüğü tüm hello verilen adları alt kimliğine eşleşen hello ailesinde `WakefieldFamily` kendi sınıf tarafından sıralanan.

**Sorgu**

    SELECT c.givenName 
    FROM Families f 
    JOIN c IN f.children 
    WHERE f.id = 'WakefieldFamily'
    ORDER BY f.children.grade ASC

**Sonuçları**

    [
      { "givenName": "Jesse" }, 
      { "givenName": "Lisa"}
    ]


## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, hello aşağıdakileri yaptığınızdan:

> [!div class="checklist"]
> * Nasıl öğrenilen SQL kullanarak tooquery  

Toohello sonraki öğretici toolearn nasıl şimdi devam toodistribute verilerinizi genel.

> [!div class="nextstepaction"]
> [Verilerinizi genel Dağıt](tutorial-global-distribution-documentdb.md)

