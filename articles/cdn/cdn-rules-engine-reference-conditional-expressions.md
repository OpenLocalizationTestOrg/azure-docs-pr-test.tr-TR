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
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="d924e-103">Azure CDN kuralları koşullu ifadeler altyapısı</span><span class="sxs-lookup"><span data-stu-id="d924e-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="d924e-104">Bu konu ayrıntılı açıklamaları hello koşullu ifadeler Azure içerik teslim ağı (CDN) için listeler [kurallar altyapısı](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="d924e-104">This topic lists detailed descriptions of hello Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="d924e-105">Merhaba ilk kural hello koşullu ifade parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="d924e-105">hello first part of a rule is hello Conditional Expression.</span></span>

<span data-ttu-id="d924e-106">Koşullu ifade</span><span class="sxs-lookup"><span data-stu-id="d924e-106">Conditional Expression</span></span> | <span data-ttu-id="d924e-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d924e-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="d924e-108">EĞER</span><span class="sxs-lookup"><span data-stu-id="d924e-108">IF</span></span> | <span data-ttu-id="d924e-109">Bir IF ifadesi her zaman bir kural ilk deyiminde hello parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="d924e-109">An IF expression is always a part of hello first statement in a rule.</span></span> <span data-ttu-id="d924e-110">Tüm diğer koşullu ifadeler gibi bu IF deyimi bir eşleşme ile ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d924e-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="d924e-111">Hiçbir ek koşullu ifadeler tanımlanmışsa, bu eşleşen bir özellik kümesi uygulanan tooa isteği olabilir önce karşılanması gereken hello ölçütü belirler.</span><span class="sxs-lookup"><span data-stu-id="d924e-111">If no additional conditional expressions are defined, then this match determines hello criterion that must be met before a set of features may be applied tooa request.</span></span>
<span data-ttu-id="d924e-112">VE</span><span class="sxs-lookup"><span data-stu-id="d924e-112">AND IF</span></span> | <span data-ttu-id="d924e-113">VE IF ifadesi yalnızca şu koşullu ifadeler: if, ve eğer türlerini hello sonra eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="d924e-113">An AND IF expression may only be added after hello following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="d924e-114">Merhaba ilk IF deyimi için karşılanması gereken başka bir koşul olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="d924e-114">It indicates that there is another condition that must be met for hello initial IF statement.</span></span>
<span data-ttu-id="d924e-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="d924e-115">ELSE IF</span></span>| <span data-ttu-id="d924e-116">ELSE IF ifadesi bir dizi özellikler belirli toothis ELSE IF deyimi gerçekleşmeden önce karşılanması gereken alternatif bir koşulu belirtir.</span><span class="sxs-lookup"><span data-stu-id="d924e-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific toothis ELSE IF statement takes place.</span></span> <span data-ttu-id="d924e-117">ELSE IF deyimi Hello varlığını hello önceki deyimi hello sonunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d924e-117">hello presence of an ELSE IF statement indicates hello end of hello previous statement.</span></span> <span data-ttu-id="d924e-118">ELSE IF deyimi başka bir ELSE IF deyimi sonra yerleştirilebilir hello yalnızca koşullu ifade.</span><span class="sxs-lookup"><span data-stu-id="d924e-118">hello only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="d924e-119">Başka bir deyişle, bir ELSE IF deyimi yalnızca kullanılan toospecify karşılanır toobe sahip tek bir ek koşul olabilir.</span><span class="sxs-lookup"><span data-stu-id="d924e-119">This means that an ELSE IF statement may only be used toospecify a single additional condition that has toobe met.</span></span>

<span data-ttu-id="d924e-120">**Örnek**: ![CDN eşleşen koşulu](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="d924e-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="d924e-121">Bir sonraki kural önceki bir kural tarafından belirtilen hello Eylemler geçersiz kılabilir.</span><span class="sxs-lookup"><span data-stu-id="d924e-121">A subsequent rule may override hello actions specified by a previous rule.</span></span> <span data-ttu-id="d924e-122">Örnek: Bir catch tüm kural belirteç tabanlı kimlik doğrulaması aracılığıyla tüm istekleri güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="d924e-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="d924e-123">Başka bir kural doğrudan o oluşturulabilir toomake belirli türde bir istekleri için bir özel durum.</span><span class="sxs-lookup"><span data-stu-id="d924e-123">Another rule may be created directly below it toomake an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="d924e-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d924e-124">Next steps</span></span>
* [<span data-ttu-id="d924e-125">Azure CDN'ye genel bakış</span><span class="sxs-lookup"><span data-stu-id="d924e-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="d924e-126">Kuralları altyapısı başvurusu</span><span class="sxs-lookup"><span data-stu-id="d924e-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="d924e-127">Kurallar altyapısı eşleşme koşulları</span><span class="sxs-lookup"><span data-stu-id="d924e-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="d924e-128">Kurallar altyapısı özellikleri</span><span class="sxs-lookup"><span data-stu-id="d924e-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="d924e-129">Merhaba kurallar altyapısı kullanarak varsayılan HTTP davranışı geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="d924e-129">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
