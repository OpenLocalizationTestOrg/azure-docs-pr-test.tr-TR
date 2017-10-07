---
title: "Azure Cosmos DB aaaProvision verimliliğini | Microsoft Docs"
description: "Nasıl tooset, Azure Cosmos DB containsers, koleksiyonları, grafikler ve tablolar için işleme sağlanan öğrenin."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: mimig
ms.openlocfilehash: c143f4aace466b7109168a50e2eb80ddeca6400e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-throughput-for-azure-cosmos-db-containers"></a>Azure Cosmos DB kapsayıcıları için kümesi işleme

Hello Azure portal, Azure Cosmos DB kapsayıcıları için işleme ayarlayabilir veya istemci SDK'ları kullanarak hello. 

Aşağıdaki tablonun hello hello işleme için kapsayıcıları kullanılabilir listeler:

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><strong>Tek bir bölüm kapsayıcısı</strong></p></td>
            <td valign="top"><p><strong>Bölümlenmiş kapsayıcısı</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>En düşük işleme</p></td>
            <td valign="top"><p>saniye başına 400 istek birimleri</p></td>
            <td valign="top"><p>saniye başına 2.500 istek birimleri</p></td>
        </tr>
        <tr>
            <td valign="top"><p>En yüksek verimlilik</p></td>
            <td valign="top"><p>saniye başına 10.000 istek birimleri</p></td>
            <td valign="top"><p>Sınırsız</p></td>
        </tr>
    </tbody>
</table>

## <a name="tooset-hello-throughput-by-using-hello-azure-portal"></a>hello Azure portal kullanarak tooset hello işleme

1. Merhaba yeni bir pencerede açmak [Azure portal](https://portal.azure.com).
2. Merhaba sol çubuğunda **Azure Cosmos DB**, veya **daha Hizmetleri** hello kısımda, ardından çok kaydırın**veritabanları**ve ardından **Azure Cosmos DB**.
3. Cosmos DB hesabınızı seçin.
4. Merhaba yeni penceresinde **Veri Gezgini (Önizleme)** hello Gezinti menüsünde.
5. Merhaba yeni pencerede, veritabanı ve kapsayıcısını genişletin ve ardından **ölçek & ayarları**.
6. Merhaba yeni penceresinde hello hello yeni işleme değeri yazın **işleme** kutusuna ve ardından **kaydetmek**.

<a id="set-throughput-sdk"></a>

## <a name="tooset-hello-throughput-by-using-hello-documentdb-api-for-net"></a>.NET için hello DocumentDB API kullanarak tooset hello işleme

```C#
//Fetch hello resource toobe updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput toohello new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a>Üretilen iş ile ilgili SSS

**My verimlilik tooless 400 RU/s daha ayarlayabilir miyim?**

400 RU/s hello en düşük işleme Cosmos DB tek bölüm koleksiyonları (2500 RU/s hello bölümlenmiş koleksiyonlar için en düşük olduğu) üzerinde kullanılabilir değil. İstek birimleri 100 RU/s aralıklarla ayarlanmış, ancak işleme too100 RU/s veya herhangi bir değer 400 RU/s değerinden küçük olacak şekilde ayarlanamaz. İçin uygun maliyetli yöntemi toodevelop arıyorsanız ve Cosmos DB test, hello ücretsiz kullanabilirsiniz [Azure Cosmos DB öykünücüsü](local-emulator.md), hangi hiçbir ücret yerel olarak dağıtabilirsiniz. 

**Merhaba MongoDB API kullanarak througput nasıl ayarlarım?**

Hiçbir MongoDB API uzantısı tooset verimlilik yoktur. Merhaba toouse hello DocumentDB API gösterildiği gibi önerilir [tooset hello işleme için .NET hello DocumentDB API kullanarak](#set-throughput-sdk).

## <a name="next-steps"></a>Sonraki adımlar

sağlama ve devam eden planet ölçekli Cosmos DB ile hakkında daha fazla toolearn bkz [bölümleme ve Cosmos DB ile ölçeklendirme](partition-data.md).
