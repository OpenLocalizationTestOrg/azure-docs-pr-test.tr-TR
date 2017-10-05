---
title: "Azure CDN kuralları altyapısı koşullu ifadeler | Microsoft Docs"
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
ms.openlocfilehash: 57e56c38e003cb83dcf44f455c4451d159db8a59
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a><span data-ttu-id="5f25d-103">Azure CDN kuralları koşullu ifadeler altyapısı</span><span class="sxs-lookup"><span data-stu-id="5f25d-103">Azure CDN rules engine conditional expressions</span></span>
<span data-ttu-id="5f25d-104">Bu konu ayrıntılı açıklamaları koşullu ifadeler Azure içerik teslim ağı (CDN) için listeler [kurallar altyapısı](cdn-rules-engine.md).</span><span class="sxs-lookup"><span data-stu-id="5f25d-104">This topic lists detailed descriptions of the Conditional Expressions for Azure Content Delivery Network (CDN) [Rules Engine](cdn-rules-engine.md).</span></span>

<span data-ttu-id="5f25d-105">İlk kural koşullu ifade parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="5f25d-105">The first part of a rule is the Conditional Expression.</span></span>

<span data-ttu-id="5f25d-106">Koşullu ifade</span><span class="sxs-lookup"><span data-stu-id="5f25d-106">Conditional Expression</span></span> | <span data-ttu-id="5f25d-107">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5f25d-107">Description</span></span>
-----------------------|-------------
<span data-ttu-id="5f25d-108">EĞER</span><span class="sxs-lookup"><span data-stu-id="5f25d-108">IF</span></span> | <span data-ttu-id="5f25d-109">Bir IF ifadesi her zaman bir kural ilk deyiminde parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="5f25d-109">An IF expression is always a part of the first statement in a rule.</span></span> <span data-ttu-id="5f25d-110">Tüm diğer koşullu ifadeler gibi bu IF deyimi bir eşleşme ile ilişkilendirilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5f25d-110">Like all other conditional expressions, this IF statement must be associated with a match.</span></span> <span data-ttu-id="5f25d-111">Hiçbir ek koşullu ifadeler tanımlanmışsa, bu eşleşen bir özellik kümesi için bir istek uygulanabilir önce karşılanması gereken ölçütü belirler.</span><span class="sxs-lookup"><span data-stu-id="5f25d-111">If no additional conditional expressions are defined, then this match determines the criterion that must be met before a set of features may be applied to a request.</span></span>
<span data-ttu-id="5f25d-112">VE</span><span class="sxs-lookup"><span data-stu-id="5f25d-112">AND IF</span></span> | <span data-ttu-id="5f25d-113">VE IF ifadesi yalnızca koşullu ifadeler: IF, ve eğer aşağıdaki türden sonra eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="5f25d-113">An AND IF expression may only be added after the following types of conditional expressions:IF,AND IF.</span></span> <span data-ttu-id="5f25d-114">Bu, ilk IF deyimi için karşılanması gereken başka bir koşul olduğunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f25d-114">It indicates that there is another condition that must be met for the initial IF statement.</span></span>
<span data-ttu-id="5f25d-115">ELSE IF</span><span class="sxs-lookup"><span data-stu-id="5f25d-115">ELSE IF</span></span>| <span data-ttu-id="5f25d-116">ELSE IF ifadesi bu ELSE IF deyimi belirli özellikler kümesi gerçekleşmeden önce karşılanması gereken alternatif bir koşulu belirtir.</span><span class="sxs-lookup"><span data-stu-id="5f25d-116">An ELSE IF expression specifies an alternative condition that must be met before a set of features specific to this ELSE IF statement takes place.</span></span> <span data-ttu-id="5f25d-117">ELSE IF deyimi varlığını önceki deyimin sonuna gösterir.</span><span class="sxs-lookup"><span data-stu-id="5f25d-117">The presence of an ELSE IF statement indicates the end of the previous statement.</span></span> <span data-ttu-id="5f25d-118">ELSE IF deyimi başka bir ELSE IF deyimi sonra yerleştirilebilir yalnızca koşullu ifade.</span><span class="sxs-lookup"><span data-stu-id="5f25d-118">The only conditional expression that may be placed after an ELSE IF statement is another ELSE IF statement.</span></span> <span data-ttu-id="5f25d-119">Başka bir deyişle, bir ELSE IF deyimi yalnızca karşılanması gereken tek bir ek koşulu belirtmek için kullanılan.</span><span class="sxs-lookup"><span data-stu-id="5f25d-119">This means that an ELSE IF statement may only be used to specify a single additional condition that has to be met.</span></span>

<span data-ttu-id="5f25d-120">**Örnek**: ![CDN eşleşen koşulu](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span><span class="sxs-lookup"><span data-stu-id="5f25d-120">**Example**: ![CDN match condition](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)</span></span>

 > [!TIP]
   > <span data-ttu-id="5f25d-121">Bir sonraki kural önceki bir kural tarafından belirtilen eylemleri geçersiz kılabilir.</span><span class="sxs-lookup"><span data-stu-id="5f25d-121">A subsequent rule may override the actions specified by a previous rule.</span></span> <span data-ttu-id="5f25d-122">Örnek: Bir catch tüm kural belirteç tabanlı kimlik doğrulaması aracılığıyla tüm istekleri güvenliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="5f25d-122">Example: A catch-all rule secures all requests via Token-Based Authentication.</span></span> <span data-ttu-id="5f25d-123">Başka bir kural doğrudan, bir özel durum istek türlerini belirli yapma oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="5f25d-123">Another rule may be created directly below it to make an exception for certain types of requests.</span></span>

### <a name="next-steps"></a><span data-ttu-id="5f25d-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5f25d-124">Next steps</span></span>
* [<span data-ttu-id="5f25d-125">Azure CDN'ye genel bakış</span><span class="sxs-lookup"><span data-stu-id="5f25d-125">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="5f25d-126">Kuralları altyapısı başvurusu</span><span class="sxs-lookup"><span data-stu-id="5f25d-126">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="5f25d-127">Kurallar altyapısı eşleşme koşulları</span><span class="sxs-lookup"><span data-stu-id="5f25d-127">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="5f25d-128">Kurallar altyapısı özellikleri</span><span class="sxs-lookup"><span data-stu-id="5f25d-128">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="5f25d-129">Kurallar altyapısı kullanarak varsayılan HTTP davranışı geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="5f25d-129">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
