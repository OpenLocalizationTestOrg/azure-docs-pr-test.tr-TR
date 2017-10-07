---
title: "aaaHow tooquery grafik verileri Azure Cosmos veritabanı? | Microsoft Belgeleri"
description: "Tooquery grafik verileri Azure Cosmos veritabanı öğrenin"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
tags: 
ms.assetid: 8bde5c80-581c-4f70-acb4-9578873c92fa
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: denlee
ms.openlocfilehash: fdde881edd6c488e2fea51e5c9665e1d736009fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-with-hello-graph-api-preview"></a>Azure Cosmos DB: Nasıl tooquery ile Merhaba grafik API'si (Önizleme)?

Hello Azure Cosmos DB [grafik API'si](graph-introduction.md) (Önizleme) destekleyen [Gremlin](https://docs.mongodb.com/manual/tutorial/query-documents/) sorgular. Bu makalede örnek belgeler sağlar ve başlattığınız tooget sorgular. Ayrıntılı Gremlin başvuru hello sağlanan [Gremlin Destek](gremlin-support.md) makalesi.

Bu makalede görevleri aşağıdaki hello yer almaktadır: 

> [!div class="checklist"]
> * Gremlin verilerle sorgulama

## <a name="prerequisites"></a>Ön koşullar

Bu sorguları toowork için bir Azure Cosmos DB hesabınız varsa ve grafik verileri hello kapsayıcısında sahip. Bu yok? Tam hello [5 dakikalık quickstart](create-graph-dotnet.md) veya hello [Geliştirici öğretici](tutorial-query-graph.md) toocreate bir hesap ve veritabanınızı doldurmak. Hello kullanarak sorguları aşağıdaki hello çalıştırabilirsiniz [Azure Cosmos DB .NET grafik Kitaplığı](graph-sdk-dotnet.md), [Gremlin konsol](https://tinkerpop.apache.org/docs/current/reference/#gremlin-console), veya sık kullanılan Gremlin sürücünüzü.

## <a name="count-vertices-in-hello-graph"></a>Merhaba grafik tepe sayısı

Aşağıdaki kod parçacığında hello nasıl toocount hello hello grafik tepe sayısı gösterir:

```
g.V().count()
```

## <a name="filters"></a>Filtreler

Gremlin'ın kullanarak filtreler gerçekleştirebilirsiniz `has` ve `hasLabel` adımları ve bunları birleştirmek kullanarak `and`, `or`, ve `not` toobuild daha karmaşık filtreler. Azure Cosmos DB köşeleri ve derece hızlı sorgular için içindeki tüm özelliklerinin şema belirsiz dizin oluşturma sağlar:

```
g.V().hasLabel('person').has('age', gt(40))
```

## <a name="projection"></a>Yansıtma

Belirli özellikler hello sorgu sonuçlarındaki hello kullanarak proje `values` . adım:

```
g.V().hasLabel('person').values('firstName')
```

## <a name="find-related-edges-and-vertices"></a>İlgili kenarları ve köşeleri Bul

Şu ana kadar yalnızca tüm veritabanındaki iş sorgu işleçleri gördük. Toonavigate toorelated kenarları ve köşeleri gerektiğinde grafikleri hızlı ve verimli çapraz geçiş işlemleri için. Şimdi tüm arkadaşların Thomas bulun. Biz Gremlin'ın kullanarak bunu `outE` tüm hello dışarı Thomas kenarları toofind adım sonra içinde köşe için toohello Gremlin'ın kullanarak bu kenarlarından çapraz geçiş yapan `inV` . adım:

```cs
g.V('thomas').outE('knows').inV().hasLabel('person')
```

Merhaba sonraki sorgu gerçekleştirir iki atlama toofind tüm "çağırarak Thomas arkadaş arkadaş", `outE` ve `inV` iki kez. 

```cs
g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')
```

Daha karmaşık sorgular derlemek ve Gremlin, kullanarak döngü gerçekleştirme ifadeleri hello dahil olmak üzere karıştırma filtre kullanan güçlü grafik geçişi mantığı uygulamanıza `loop` adım ve hello kullanarak uygulama koşullu Gezinti `choose` adım. İle yapabilecekleriniz hakkında daha fazla bilgi [Gremlin Destek](gremlin-support.md)!

## <a name="next-steps"></a>Sonraki adımlar

Bu öğreticide, hello aşağıdakileri yaptığınızdan:

> [!div class="checklist"]
> * Nasıl öğrenilen grafiğini kullanarak tooquery 

Toohello sonraki öğretici toolearn nasıl şimdi devam toodistribute verilerinizi genel.

> [!div class="nextstepaction"]
> [Verilerinizi genel Dağıt](tutorial-global-distribution-documentdb.md)