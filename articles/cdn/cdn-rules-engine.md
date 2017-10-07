---
title: "Hello Azure CDN kurallar altyapısı kullanarak aaaOverride HTTP davranışı | Microsoft Docs"
description: "HTTP üstbilgileri değiştirmek ve önbellek ilkesi tanımlayın veya Hello kurallar altyapısı belirli içerik türlerini hello teslimini engelleme gibi HTTP isteklerini Azure CDN tarafından nasıl işleneceğini toocustomize sağlar."
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
ms.openlocfilehash: dd7194be9dbda43180c64568d3e1f52c5c513a7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="override-http-behavior-using-hello-azure-cdn-rules-engine"></a><span data-ttu-id="97d35-103">Hello Azure CDN kurallar altyapısı kullanarak HTTP davranışı geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="97d35-103">Override HTTP behavior using hello Azure CDN rules engine</span></span>
[!INCLUDE [cdn-premium-feature](../../includes/cdn-premium-feature.md)]

## <a name="overview"></a><span data-ttu-id="97d35-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="97d35-104">Overview</span></span>
<span data-ttu-id="97d35-105">Merhaba kurallar altyapısı HTTP isteklerini, belirli türde bir içerik hello teslimini engelleme, önbellek ilkesi tanımlama ve HTTP üstbilgileri değiştirme gibi işlenme toocustomize sağlar.</span><span class="sxs-lookup"><span data-stu-id="97d35-105">hello rules engine allows you toocustomize how HTTP requests are handled, such as blocking hello delivery of certain types of content, defining a caching policy, and modifying HTTP headers.</span></span>  <span data-ttu-id="97d35-106">Bu öğretici bir kural oluşturma önbelleğe alma davranışı CDN varlıklarını hello değiştirecek gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="97d35-106">This tutorial will demonstrate creating a rule that will change hello caching behavior of CDN assets.</span></span>  <span data-ttu-id="97d35-107">Ayrıca video içeriği hello kullanılabilir yok "[Ayrıca bkz.](#see-also)" bölümü.</span><span class="sxs-lookup"><span data-stu-id="97d35-107">There's also video content available in hello "[See also](#see-also)" section.</span></span>

   > [!TIP] 
   > <span data-ttu-id="97d35-108">Ayrıntılı bir başvuru toohello sözdizimi için bkz: [kuralları altyapısı başvurusu](cdn-rules-engine-reference.md).</span><span class="sxs-lookup"><span data-stu-id="97d35-108">For a reference toohello syntax in detail, see [Rules Engine Reference](cdn-rules-engine-reference.md).</span></span>
   > 


## <a name="tutorial"></a><span data-ttu-id="97d35-109">Öğretici</span><span class="sxs-lookup"><span data-stu-id="97d35-109">Tutorial</span></span>
1. <span data-ttu-id="97d35-110">Merhaba CDN profili dikey penceresinden hello tıklayın **Yönet** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="97d35-110">From hello CDN profile blade, click hello **Manage** button.</span></span>
   
    ![CDN profili dikey penceresi yönetmek düğmesi](./media/cdn-rules-engine/cdn-manage-btn.png)
   
    <span data-ttu-id="97d35-112">Merhaba CDN Yönetim Portalı açar.</span><span class="sxs-lookup"><span data-stu-id="97d35-112">hello CDN management portal opens.</span></span>
2. <span data-ttu-id="97d35-113">Tıklatın hello üzerinde **HTTP büyük** sekmesini ve ardından, **kurallar altyapısı**.</span><span class="sxs-lookup"><span data-stu-id="97d35-113">Click on hello **HTTP Large** tab, followed by **Rules Engine**.</span></span>
   
    <span data-ttu-id="97d35-114">Yeni bir kural için seçenekler görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="97d35-114">Options for a new rule are displayed.</span></span>
   
    ![CDN yeni kural seçenekleri](./media/cdn-rules-engine/cdn-new-rule.png)
   
   > [!IMPORTANT]
   > <span data-ttu-id="97d35-116">içinde birden çok kural listelenen hello sırasını nasıl işlendiğini etkiler.</span><span class="sxs-lookup"><span data-stu-id="97d35-116">hello order in which multiple rules are listed affects how they are handled.</span></span> <span data-ttu-id="97d35-117">Bir sonraki kural önceki bir kural tarafından belirtilen hello Eylemler geçersiz kılabilir.</span><span class="sxs-lookup"><span data-stu-id="97d35-117">A subsequent rule may override hello actions specified by a previous rule.</span></span>
   > 
   > 
3. <span data-ttu-id="97d35-118">Hello bir ad girin **adı / açıklaması** metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="97d35-118">Enter a name in hello **Name / Description** textbox.</span></span>
4. <span data-ttu-id="97d35-119">Merhaba kuralın uygulanacağı istekleri Hello türünü tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="97d35-119">Identify hello type of requests hello rule will apply to.</span></span>  <span data-ttu-id="97d35-120">Varsayılan olarak, hello **her zaman** eşleşme koşul seçilidir.</span><span class="sxs-lookup"><span data-stu-id="97d35-120">By default, hello **Always** match condition is selected.</span></span>  <span data-ttu-id="97d35-121">Kullanacağınız **her zaman** Bu öğretici için bu nedenle, seçili bırakın.</span><span class="sxs-lookup"><span data-stu-id="97d35-121">You'll use **Always** for this tutorial, so leave that selected.</span></span>
   
   ![CDN eşleşme koşulu](./media/cdn-rules-engine/cdn-request-type.png)
   
   > [!TIP]
   > <span data-ttu-id="97d35-123">Koşullar hello açılır menüde kullanılabilir türlerde eşleşme vardır.</span><span class="sxs-lookup"><span data-stu-id="97d35-123">There are many types of match conditions available in hello dropdown.</span></span>  <span data-ttu-id="97d35-124">Merhaba mavi Bilgi simgesi toohello üzerinde tıklatarak hello eşleşme koşul solundaki şu anda seçili hello koşul ayrıntılı anlatılmıştır.</span><span class="sxs-lookup"><span data-stu-id="97d35-124">Clicking on hello blue informational icon toohello left of hello match condition will explain hello currently selected condition in detail.</span></span>
   > 
   >  <span data-ttu-id="97d35-125">Merhaba tam listesi için ayrıntılı koşullu ifadeler için bkz [kurallar altyapısı koşullu ifadeler](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="97d35-125">For hello full list of conditional expressions in detail, see [Rules Engine Conditional Expressions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   >  
   > <span data-ttu-id="97d35-126">Hello tam listesi ayrıntılı eşleşme koşulları için bkz: [kurallar altyapısı eşleşen koşullar](cdn-rules-engine-reference-match-conditions.md).</span><span class="sxs-lookup"><span data-stu-id="97d35-126">For hello full list of match conditions in detail, see [Rules Engine Match Conditions](cdn-rules-engine-reference-match-conditions.md).</span></span>
   > 
   > 
5. <span data-ttu-id="97d35-127">Merhaba tıklatın  **+**  sonraki çok düğmesini**özellikleri** tooadd yeni bir özellik.</span><span class="sxs-lookup"><span data-stu-id="97d35-127">Click hello **+** button next too**Features** tooadd a new feature.</span></span>  <span data-ttu-id="97d35-128">Merhaba soldaki Hello açılır menüde seçin **zorla iç Max-Age**.</span><span class="sxs-lookup"><span data-stu-id="97d35-128">In hello dropdown on hello left, select **Force Internal Max-Age**.</span></span>  <span data-ttu-id="97d35-129">Görüntülenen hello metin kutusuna girin **300**.</span><span class="sxs-lookup"><span data-stu-id="97d35-129">In hello textbox that appears, enter **300**.</span></span>  <span data-ttu-id="97d35-130">Varsayılan değerleri kalan hello bırakın.</span><span class="sxs-lookup"><span data-stu-id="97d35-130">Leave hello remaining default values.</span></span>
   
   ![CDN özelliği](./media/cdn-rules-engine/cdn-new-feature.png)
   
   > [!NOTE]
   > <span data-ttu-id="97d35-132">Eşleşme koşullarla hello mavi Bilgi simgesi toohello tıklatarak Merhaba yeni bıraktığınız özelliği bu özellik hakkındaki ayrıntıları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="97d35-132">As with match conditions, clicking hello blue informational icon toohello left of hello new feature will display details about this feature.</span></span>  <span data-ttu-id="97d35-133">Merhaba durumda **zorla iç Max-Age**, biz hello varlığın geçersiz kılma **Cache-Control** ve **Expires** hello CDN kenar düğümüne hello yenilediğinizde üstbilgileri toocontrol Varlık hello kaynaktan.</span><span class="sxs-lookup"><span data-stu-id="97d35-133">In hello case of **Force Internal Max-Age**, we are overriding hello asset's **Cache-Control** and **Expires** headers toocontrol when hello CDN edge node will refresh hello asset from hello origin.</span></span>  <span data-ttu-id="97d35-134">Bizim örneğimizde, 300 saniye hello CDN kenar düğümüne hello varlık hello varlık kendi kaynaktan yenileme önce 5 dakika için önbelleğe anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="97d35-134">Our example of 300 seconds means hello CDN edge node will cache hello asset for 5 minutes before refreshing hello asset from its origin.</span></span>
   > 
   > <span data-ttu-id="97d35-135">Merhaba özelliklerin tam listesini ayrıntılı için bkz: [kurallar altyapısı özellik ayrıntıları](cdn-rules-engine-reference-features.md).</span><span class="sxs-lookup"><span data-stu-id="97d35-135">For hello full list of features in detail, see [Rules Engine Feature Details](cdn-rules-engine-reference-features.md).</span></span>
   > 
   > 
6. <span data-ttu-id="97d35-136">Merhaba tıklatın **Ekle** düğmesini toosave hello yeni kural.</span><span class="sxs-lookup"><span data-stu-id="97d35-136">Click hello **Add** button toosave hello new rule.</span></span>  <span data-ttu-id="97d35-137">Merhaba yeni kural artık onayını bekliyor.</span><span class="sxs-lookup"><span data-stu-id="97d35-137">hello new rule is now awaiting approval.</span></span> <span data-ttu-id="97d35-138">Bunu onaylandıktan sonra hello durum değiştirilecek **bekleyen XML** çok**etkin XML**.</span><span class="sxs-lookup"><span data-stu-id="97d35-138">Once it has been approved, hello status will change from **Pending XML** too**Active XML**.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="97d35-139">Kuralları değişikliklerin too90 dakika toopropagate hello CDN aracılığıyla yukarı alabilir.</span><span class="sxs-lookup"><span data-stu-id="97d35-139">Rules changes may take up too90 minutes toopropagate through hello CDN.</span></span>
   > 
   > 

## <a name="see-also"></a><span data-ttu-id="97d35-140">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="97d35-140">See also</span></span>
* [<span data-ttu-id="97d35-141">Azure CDN'ye genel bakış</span><span class="sxs-lookup"><span data-stu-id="97d35-141">Azure CDN Overview</span></span>](cdn-overview.md)
* [<span data-ttu-id="97d35-142">Kuralları altyapısı başvurusu</span><span class="sxs-lookup"><span data-stu-id="97d35-142">Rules Engine Reference</span></span>](cdn-rules-engine-reference.md)
* [<span data-ttu-id="97d35-143">Kurallar altyapısı eşleşme koşulları</span><span class="sxs-lookup"><span data-stu-id="97d35-143">Rules Engine Match Conditions</span></span>](cdn-rules-engine-reference-match-conditions.md)
* [<span data-ttu-id="97d35-144">Kurallar altyapısı koşullu ifadeler</span><span class="sxs-lookup"><span data-stu-id="97d35-144">Rules Engine Conditional Expressions</span></span>](cdn-rules-engine-reference-conditional-expressions.md)
* [<span data-ttu-id="97d35-145">Kurallar altyapısı özellikleri</span><span class="sxs-lookup"><span data-stu-id="97d35-145">Rules Engine Features</span></span>](cdn-rules-engine-reference-features.md)
* [<span data-ttu-id="97d35-146">Merhaba kurallar altyapısı kullanarak varsayılan HTTP davranışı geçersiz kılma</span><span class="sxs-lookup"><span data-stu-id="97d35-146">Overriding default HTTP behavior using hello rules engine</span></span>](cdn-rules-engine.md)
* <span data-ttu-id="97d35-147">[Azure Cuma: Azure CDN's güçlü yeni Premium özellikleri](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span><span class="sxs-lookup"><span data-stu-id="97d35-147">[Azure Fridays: Azure CDN's powerful new Premium Features](https://azure.microsoft.com/documentation/videos/azure-cdns-powerful-new-premium-features/) (video)</span></span>