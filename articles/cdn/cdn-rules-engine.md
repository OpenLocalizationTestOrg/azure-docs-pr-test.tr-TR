---
title: "Azure CDN kurallar altyapısı kullanarak HTTP davranışı geçersiz kılma | Microsoft Docs"
description: "Kurallar altyapısı, belirli türde bir içerik teslim engelleme gibi HTTP isteklerini Azure CDN tarafından nasıl işleneceğini özelleştirme, önbellek ilkesi tanımlayın ve HTTP üstbilgileri değiştirmenize olanak sağlar."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 625a912b-91f2-485d-8991-128cc194ee71
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: abfe283476206b181018d187675b47112dc5ad2f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="override-http-behavior-using-the-azure-cdn-rules-engine"></a><span data-ttu-id="720e2-103">Azure CDN kurallar altyapısı kullanarak HTTP davranışı geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="720e2-103">Override HTTP behavior using the Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="720e2-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="720e2-104">Overview</span></span>
<span data-ttu-id="720e2-105">Kurallar altyapısı HTTP isteklerini, belirli türde bir içerik teslim engelleme, önbellek ilkesi tanımlama ve HTTP üstbilgileri değiştirme gibi işlenme özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="720e2-105">The rules engine allows you to customize how HTTP requests are handled, such as blocking the delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="720e2-106">Bu öğretici bir kural oluşturma CDN varlıklar önbelleğe alma davranışını değiştirir gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="720e2-106">This tutorial will demonstrate creating a rule that will change the caching behavior of CDN assets.</span></span>  <span data-ttu-id="720e2-107">Ayrıca video içeriği bulunmamaktadır kullanılabilir "[Ayrıca bkz.](#see-also)" bölümü.</span><span class="sxs-lookup"><span data-stu-id="720e2-107">There's also video content available in the "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="720e2-108">Ayrıntılı sözdizimi başvuru için bkz: [kuralları altyapısı başvurusu](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="720e2-108">For a reference to the syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="720e2-109">Öğretici</span><span class="sxs-lookup"><span data-stu-id="720e2-109">Tutorial</span></span>
1. <span data-ttu-id="720e2-110">CDN profili dikey penceresinden tıklayın **Yönet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="720e2-110">From the CDN profile blade, click the **Manage** button.</span></span>
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="720e2-112">CDN Yönetim Portalı'nı açar.</span><span class="sxs-lookup"><span data-stu-id="720e2-112">The CDN management portal opens.</span></span>
2. <span data-ttu-id="720e2-113">Tıklayın **HTTP büyük** sekmesini ve ardından, **kurallar altyapısı**.</span><span class="sxs-lookup"><span data-stu-id="720e2-113">Click on the **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="720e2-114">Yeni bir kural için seçenekler görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="720e2-114">Options for a new rule are displayed.</span></span>
   
    ![CDN yeni kural seçenekleri](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="720e2-116">Birden çok kural listelenmiş görevlerin sırası nasıl işlendiğini etkiler.</span><span class="sxs-lookup"><span data-stu-id="720e2-116">The order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="720e2-117">Bir sonraki kural önceki bir kural tarafından belirtilen eylemleri geçersiz kılabilir.</span><span class="sxs-lookup"><span data-stu-id="720e2-117">A subsequent rule may override the actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="720e2-118">Bir ad girin **adı / açıklaması** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="720e2-118">Enter a name in the **Name / Description** textbox.</span></span>
4. <span data-ttu-id="720e2-119">Kuralın uygulanacağı istekleri türünü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="720e2-119">Identify the type of requests the rule will apply to.</span></span>  <span data-ttu-id="720e2-120">Varsayılan olarak, **her zaman** eşleşme koşul seçilidir.</span><span class="sxs-lookup"><span data-stu-id="720e2-120">By default, the **Always** match condition is selected.</span></span>  <span data-ttu-id="720e2-121">Kullanacağınız **her zaman** Bu öğretici için bu nedenle, seçili bırakın.</span><span class="sxs-lookup"><span data-stu-id="720e2-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![CDN eşleşme koşulu](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="720e2-123">Açılır listede kullanılabilen koşullar türlerde eşleşme vardır.</span><span class="sxs-lookup"><span data-stu-id="720e2-123">There are many types of match conditions available in the dropdown.</span></span>  <span data-ttu-id="720e2-124">Eşleşme koşul solundaki mavi bilgi simgesine tıklayarak şu anda seçili koşul ayrıntılı olarak anlatılmıştır.</span><span class="sxs-lookup"><span data-stu-id="720e2-124">Clicking on the blue informational icon to the left of the match condition will explain the currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="720e2-125">Ayrıntılı koşullu ifadeler tam listesi için bkz: [kurallar altyapısı koşullu ifadeler](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="720e2-125">For the full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="720e2-126">Eşleşme koşullar ayrıntılı tam listesi için bkz [kurallar altyapısı eşleşen koşullar](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="720e2-126">For the full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="720e2-127">Tıklatın  **+**  düğmesine **özellikleri** yeni bir özellik eklemek için.</span><span class="sxs-lookup"><span data-stu-id="720e2-127">Click the **+** button next to **Features** to add a new feature.</span></span>  <span data-ttu-id="720e2-128">Sol taraftaki açılır menüde seçin **zorla iç Max-Age**.</span><span class="sxs-lookup"><span data-stu-id="720e2-128">In the dropdown on the left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="720e2-129">Görüntülenen metin kutusuna girin **300**.</span><span class="sxs-lookup"><span data-stu-id="720e2-129">In the textbox that appears, enter **300**.</span></span>  <span data-ttu-id="720e2-130">Geri kalan varsayılan değerler bırakın.</span><span class="sxs-lookup"><span data-stu-id="720e2-130">Leave the remaining default values.</span></span>
   
   ![CDN özelliği](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="720e2-132">Olarak eşleşme koşullarla yeni özellik solundaki mavi bilgi simgesine tıklayarak bu özellik hakkındaki ayrıntıları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="720e2-132">As with match conditions, clicking the blue informational icon to the left of the new feature will display details about this feature.</span></span>  <span data-ttu-id="720e2-133">Durumunda **zorla iç Max-Age**, biz varlığın geçersiz kılma **Cache-Control** ve **Expires** CDN kenar düğümüne kaynaktan varlık zaman yenilenecek denetlemek için üstbilgiler.</span><span class="sxs-lookup"><span data-stu-id="720e2-133">In the case of **Force Internal Max-Age**, we are overriding the asset's **Cache-Control** and **Expires** headers to control when the CDN edge node will refresh the asset from the origin.</span></span>  <span data-ttu-id="720e2-134">Bizim örneğimizde, 300 saniye CDN kenar düğümüne varlık kendi kaynaktan varlık yenileme önce 5 dakika için önbelleğe anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="720e2-134">Our example of 300 seconds means the CDN edge node will cache the asset for 5 minutes before refreshing the asset from its origin.</span></span>
   > 
   > <span data-ttu-id="720e2-135">Ayrıntılı özelliklerin tam listesi için bkz: [kurallar altyapısı özellik ayrıntıları](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="720e2-135">For the full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="720e2-136">Tıklatın **Ekle** yeni kuralını kaydetmek için düğmesi.</span><span class="sxs-lookup"><span data-stu-id="720e2-136">Click the **Add** button to save the new rule.</span></span>  <span data-ttu-id="720e2-137">Yeni Kural artık onayını bekliyor.</span><span class="sxs-lookup"><span data-stu-id="720e2-137">The new rule is now awaiting approval.</span></span> <span data-ttu-id="720e2-138">Bunu onaylandıktan sonra durumu değiştirilecek **bekleyen XML** için **etkin XML**.</span><span class="sxs-lookup"><span data-stu-id="720e2-138">Once it has been approved, the status will change from **Pending XML** to **Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="720e2-139">Kuralları değişiklikleri yayılması 90 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="720e2-139">Rules changes may take up to 90 minutes to propagate through the CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="720e2-140">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="720e2-140">See also</span></span>
* [<span data-ttu-id="720e2-141">Azure CDN'ye genel bakış</span><span class="sxs-lookup"><span data-stu-id="720e2-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="720e2-142">Kuralları altyapısı başvurusu</span><span class="sxs-lookup"><span data-stu-id="720e2-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="720e2-143">Kurallar altyapısı eşleşme koşulları</span><span class="sxs-lookup"><span data-stu-id="720e2-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="720e2-144">Kurallar altyapısı koşullu ifadeler</span><span class="sxs-lookup"><span data-stu-id="720e2-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="720e2-145">Kurallar altyapısı özellikleri</span><span class="sxs-lookup"><span data-stu-id="720e2-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="720e2-146">Kurallar altyapısı kullanarak varsayılan HTTP davranışı geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="720e2-146">Overriding default HTTP behavior using the rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="720e2-147">[Azure Cuma: Azure CDN's güçlü yeni Premium özellikleri](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span><span class="sxs-lookup"><span data-stu-id="720e2-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>