---
title: "aaaAzure CDN kurallar altyapısı koşullu ifadeler | Microsoft Docs"
description: "Azure CDN başvuru belgelerine altyapısı eşleşme koşulları ve özellikleri kuralları."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a>Azure CDN kuralları koşullu ifadeler altyapısı
Bu konu ayrıntılı açıklamaları hello koşullu ifadeler Azure içerik teslim ağı (CDN) için listeler [kurallar altyapısı](cdn-rules-engine.md).

Merhaba ilk kural hello koşullu ifade parçasıdır.

Koşullu ifade | Açıklama
-----------------------|-------------
EĞER | Bir IF ifadesi her zaman bir kural ilk deyiminde hello parçasıdır. Tüm diğer koşullu ifadeler gibi bu IF deyimi bir eşleşme ile ilişkilendirilmiş olması gerekir. Hiçbir ek koşullu ifadeler tanımlanmışsa, bu eşleşen bir özellik kümesi uygulanan tooa isteği olabilir önce karşılanması gereken hello ölçütü belirler.
VE | VE IF ifadesi yalnızca şu koşullu ifadeler: if, ve eğer türlerini hello sonra eklenebilir. Merhaba ilk IF deyimi için karşılanması gereken başka bir koşul olduğunu belirtir.
ELSE IF| ELSE IF ifadesi bir dizi özellikler belirli toothis ELSE IF deyimi gerçekleşmeden önce karşılanması gereken alternatif bir koşulu belirtir. ELSE IF deyimi Hello varlığını hello önceki deyimi hello sonunu gösterir. ELSE IF deyimi başka bir ELSE IF deyimi sonra yerleştirilebilir hello yalnızca koşullu ifade. Başka bir deyişle, bir ELSE IF deyimi yalnızca kullanılan toospecify karşılanır toobe sahip tek bir ek koşul olabilir.

**Örnek**: ![CDN eşleşen koşulu](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)

 > [!TIP]
   > Bir sonraki kural önceki bir kural tarafından belirtilen hello Eylemler geçersiz kılabilir. Örnek: Bir catch tüm kural belirteç tabanlı kimlik doğrulaması aracılığıyla tüm istekleri güvenliğini sağlar. Başka bir kural doğrudan o oluşturulabilir toomake belirli türde bir istekleri için bir özel durum.

### <a name="next-steps"></a>Sonraki adımlar
* [Azure CDN'ye genel bakış](cdn-overview.md)
* [Kuralları altyapısı başvurusu](cdn-rules-engine-reference.md)
* [Kurallar altyapısı eşleşme koşulları](cdn-rules-engine-reference-match-conditions.md)
* [Kurallar altyapısı özellikleri](cdn-rules-engine-reference-features.md)
* [Merhaba kurallar altyapısı kullanarak varsayılan HTTP davranışı geçersiz kılma](cdn-rules-engine.md)
