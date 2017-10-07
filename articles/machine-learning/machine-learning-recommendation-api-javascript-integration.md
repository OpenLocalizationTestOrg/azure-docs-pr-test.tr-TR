---
title: "Machine Learning öneriler: JavaScript tümleştirme | Microsoft Docs"
description: "Azure Machine Learning önerileri - JavaScript tümleştirmesi - belgeleri"
services: machine-learning
documentationcenter: 
author: LuisCabrer
manager: jhubbard
editor: cgronlun
ms.assetid: bbbb5bb6-489d-4a62-a2ae-f36237e9e2e1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 03/31/2017
ms.author: luisca
ROBOTS: NOINDEX
redirect_url: machine-learning-datamarket-deprecation
redirect_document_id: True
ms.openlocfilehash: 4c5f0eee4aa04ce823321d52985374c52850f0d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="4a1e1-103">Azure Machine Learning Önerileri - JavaScript Tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="4a1e1-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="4a1e1-104">Merhaba önerileri API Bilişsel hizmeti yerine bu sürümünü kullanarak başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-104">You should start using hello Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="4a1e1-105">Merhaba önerileri Bilişsel hizmet bu hizmeti koyacağınız ve tüm hello yeni özellikler vardır geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-105">hello Recommendations Cognitive Service will be replacing this service, and all hello new features will be developed there.</span></span> <span data-ttu-id="4a1e1-106">Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="4a1e1-107">Daha fazla bilgi edinmek [geçiş toohello yeni Bilişsel hizmeti](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="4a1e1-107">Learn more about [Migrating toohello new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="4a1e1-108">Bu belge tarif nasıl toointegrate, sitenizi JavaScript kullanarak.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-108">This document depict how toointegrate your site using JavaScript.</span></span> <span data-ttu-id="4a1e1-109">bir öneri modeli yapı sonra hello JavaScript toosend veri alım olayları ve tooconsume öneriler sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-109">hello JavaScript enables you toosend Data Acquisition events and tooconsume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="4a1e1-110">JS yapılan tüm işlemler de sunucu tarafındaki yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="4a1e1-111">1. Genel bakış</span><span class="sxs-lookup"><span data-stu-id="4a1e1-111">1. General Overview</span></span>
<span data-ttu-id="4a1e1-112">Azure ML önerileri sitenizi tümleştirme 2 aşamalara oluşur:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="4a1e1-113">Olayları Azure ML önerileri gönderin.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="4a1e1-114">Bu toobuild bir öneri modeli olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-114">This will enable toobuild a recommendation model.</span></span>
2. <span data-ttu-id="4a1e1-115">Merhaba önerileri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-115">Consume hello recommendations.</span></span> <span data-ttu-id="4a1e1-116">Merhaba model oluşturulduktan sonra Başlangıç önerileri kullanmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-116">After hello model is built you can consume hello recommendations.</span></span> <span data-ttu-id="4a1e1-117">(Bu belgede, nasıl okuma toobuild bir model hello Hızlı Başlangıç Kılavuzu tooget hakkında daha fazla bilgi açıklamaz).</span><span class="sxs-lookup"><span data-stu-id="4a1e1-117">(This document does not explain how toobuild a model, read hello quick start guide tooget more information on how).</span></span>

<span data-ttu-id="4a1e1-118"><ins>Aşama ı</ins></span><span class="sxs-lookup"><span data-stu-id="4a1e1-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="4a1e1-119">Azure ML önerileri sunucularına (aracılığıyla veri Pazar) hello html sayfasında oluşurken hello sağlayan küçük bir JavaScript kitaplığı html sayfalarınıza ekleme Birinci aşama sayfa toosend olaylarının hello:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-119">In hello first phase you insert into your html pages a small JavaScript library that enables hello page toosend events as they occur on hello html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Drawing1][1]

<span data-ttu-id="4a1e1-121"><ins>Aşama II</ins></span><span class="sxs-lookup"><span data-stu-id="4a1e1-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="4a1e1-122">Hello tooshow hello önerileri hello sayfasında istediğinizde İkinci aşama, aşağıdaki seçenekleri şu hello birini seçin:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-122">In hello second phase when you want tooshow hello recommendations on hello page you select one of hello following options:</span></span>

<span data-ttu-id="4a1e1-123">1. sunucunuzda (sayfa işleme aşamasında hello) Azure ML önerileri Server (aracılığıyla veri Pazar) tooget önerileri çağırır.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-123">1.Your server (on hello phase of page rendering) calls Azure ML Recommendations Server (via Data Market) tooget recommendations.</span></span> <span data-ttu-id="4a1e1-124">Merhaba sonuçları öğeleri kimliği listesini içerir. Sunucunuz tooenrich hello sonuçları Meta veriler (örn. görüntüler, açıklama) hello öğelerle gerekir ve sayfa toohello tarayıcı oluşturulan hello gönderin.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-124">hello results include a list of items id. Your server needs tooenrich hello results with hello items Meta data (e.g. images, description) and send hello created page toohello browser.</span></span>

![Drawing2][2]

<span data-ttu-id="4a1e1-126">2. hello diğer seçenek toouse hello küçük JavaScript aşaması bir tooget basit önerilen öğelerin listesini dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-126">2.hello other option is toouse hello small JavaScript file from phase one tooget a simple list of recommended items.</span></span> <span data-ttu-id="4a1e1-127">Burada alınan hello hello ilk seçeneğinde hello'den daha yalın verilerdir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-127">hello data received here is leaner than hello one in hello first option.</span></span>

![Drawing3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="4a1e1-129">2. Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4a1e1-129">2. Prerequisites</span></span>
1. <span data-ttu-id="4a1e1-130">Merhaba API'lerini kullanarak yeni bir model oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-130">Create a new model using hello APIs.</span></span> <span data-ttu-id="4a1e1-131">Merhaba Hızlı Başlangıç Kılavuzu nasıl toodo onu.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-131">See hello Quick start guide on how toodo it.</span></span>
2. <span data-ttu-id="4a1e1-132">Kodlama, &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; base64 ile.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-132">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="4a1e1-133">(Bu hello temel kimlik doğrulaması tooenable hello JS kod toocall hello API'leri kullanılır).</span><span class="sxs-lookup"><span data-stu-id="4a1e1-133">(This will be used for hello basic authentication tooenable hello JS code toocall hello APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="4a1e1-134">3. JavaScript kullanarak veri alım olayları Gönder</span><span class="sxs-lookup"><span data-stu-id="4a1e1-134">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="4a1e1-135">Aşağıdaki adımları hello gönderen olaylar kolaylaştırır:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-135">hello following steps facilitate sending events:</span></span>

1. <span data-ttu-id="4a1e1-136">JQuery kitaplığı kodunuzda içerir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-136">Include JQuery library in your code.</span></span> <span data-ttu-id="4a1e1-137">URL aşağıdaki hello nuget'nden indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-137">You can download it from nuget in hello following URL.</span></span>
   
     <span data-ttu-id="4a1e1-138">http://www.nuget.org/Packages/JQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="4a1e1-138">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="4a1e1-139">URL aşağıdaki hello Hello önerileri Java betiği kitaplığından içerir: http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="4a1e1-139">Include hello Recommendations Java Script library from hello following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="4a1e1-140">Merhaba uygun parametrelerle Azure ML önerileri kitaplığı başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-140">Initialize Azure ML Recommendations library with hello appropriate parameters.</span></span>
   
     <span data-ttu-id="4a1e1-141"><script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Gönderme hello uygun olayı.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-141"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send hello appropriate event.</span></span> <span data-ttu-id="4a1e1-142">Tüm olayları türüne aşağıda ayrıntılı bölümüne bakın (örnek olarak, olay tıklayın) <script> varsa (typeof AzureMLRecommendationsEvent "undefined" ==) {</span><span class="sxs-lookup"><span data-stu-id="4a1e1-142">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="4a1e1-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({event: "click", item: "18321116"});</script></span><span class="sxs-lookup"><span data-stu-id="4a1e1-143">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="4a1e1-144">3.1.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-144">3.1.</span></span>    <span data-ttu-id="4a1e1-145">Sınırlamalar ve tarayıcı desteği</span><span class="sxs-lookup"><span data-stu-id="4a1e1-145">Limitations and Browser Support</span></span>
<span data-ttu-id="4a1e1-146">Bu bir başvuru uygulamasıdır ve olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-146">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="4a1e1-147">Önde gelen tüm tarayıcılar desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-147">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="4a1e1-148">3.2.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-148">3.2.</span></span>    <span data-ttu-id="4a1e1-149">Olay türü</span><span class="sxs-lookup"><span data-stu-id="4a1e1-149">Type of Events</span></span>
<span data-ttu-id="4a1e1-150">Kitaplık destekler hello 5 olay türü vardır: tıklatın, öneri tıklayın, tooShop Sepeti, Ekle, Kaldır alışveriş sepeti ve satın alma.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-150">There are 5 types of event that hello library supports: Click, Recommendation Click, Add tooShop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="4a1e1-151">Oturum açma adı verilen kullanılan tooset hello kullanıcı bağlamı ek bir olay yok.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-151">There is an additional event that is used tooset hello user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="4a1e1-152">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-152">3.2.1.</span></span> <span data-ttu-id="4a1e1-153">Tıklama olayı</span><span class="sxs-lookup"><span data-stu-id="4a1e1-153">Click Event</span></span>
<span data-ttu-id="4a1e1-154">Bu olay, bir kullanıcının bir öğe üzerinde tıkladığınız dilediğiniz zaman kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-154">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="4a1e1-155">Genellikle kullanıcı bir öğeyi tıklattığında yeni bir sayfa hello öğe ayrıntıları açıldıktan; Bu sayfada, bu olay tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-155">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="4a1e1-156">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-156">Parameters:</span></span>

* <span data-ttu-id="4a1e1-157">"olayı (dize, zorunlu) - tıklayın"</span><span class="sxs-lookup"><span data-stu-id="4a1e1-157">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="4a1e1-158">öğe (dize, zorunlu) - hello öğesinin benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="4a1e1-158">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="4a1e1-159">ItemName (dize, isteğe bağlı) - hello öğesinin hello adı</span><span class="sxs-lookup"><span data-stu-id="4a1e1-159">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="4a1e1-160">itemDescription (dize, isteğe bağlı) - hello öğenin hello açıklaması</span><span class="sxs-lookup"><span data-stu-id="4a1e1-160">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="4a1e1-161">itemCategory (dize, isteğe bağlı) - hello öğesinin hello kategorisi</span><span class="sxs-lookup"><span data-stu-id="4a1e1-161">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="4a1e1-162">Veya isteğe bağlı verileri olan:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-162">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="4a1e1-163">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-163">3.2.2.</span></span> <span data-ttu-id="4a1e1-164">Öneri, olay'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="4a1e1-164">Recommendation Click Event</span></span>
<span data-ttu-id="4a1e1-165">Bu olay, bir kullanıcının önerilen bir öğe olarak Azure ML önerilerden alındı bir öğe üzerinde tıkladığınız dilediğiniz zaman kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-165">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="4a1e1-166">Genellikle kullanıcı bir öğeyi tıklattığında yeni bir sayfa hello öğe ayrıntıları açıldıktan; Bu sayfada, bu olay tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-166">Usually when user clicks on an item a new page is opened with hello item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="4a1e1-167">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-167">Parameters:</span></span>

* <span data-ttu-id="4a1e1-168">Olay (dize, zorunlu) - "recommendationclick"</span><span class="sxs-lookup"><span data-stu-id="4a1e1-168">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="4a1e1-169">öğe (dize, zorunlu) - hello öğesinin benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="4a1e1-169">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="4a1e1-170">ItemName (dize, isteğe bağlı) - hello öğesinin hello adı</span><span class="sxs-lookup"><span data-stu-id="4a1e1-170">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="4a1e1-171">itemDescription (dize, isteğe bağlı) - hello öğenin hello açıklaması</span><span class="sxs-lookup"><span data-stu-id="4a1e1-171">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="4a1e1-172">itemCategory (dize, isteğe bağlı) - hello öğesinin hello kategorisi</span><span class="sxs-lookup"><span data-stu-id="4a1e1-172">itemCategory (string, optional) - hello category of hello item</span></span>
* <span data-ttu-id="4a1e1-173">oluştururken Çekirdeği (dize dizisi, isteğe bağlı) - hello öneri sorgu oluşturulan oluştururken çekirdeği hello.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-173">seeds (string array, optional) - hello seeds that generated hello recommendation query.</span></span>
* <span data-ttu-id="4a1e1-174">recoList (dize dizisi, isteğe bağlı) - tıklandığını hello maddeden hello öneri isteğinin sonucunu hello.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-174">recoList (string array, optional) - hello result of hello recommendation request that generated hello item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="4a1e1-175">Veya isteğe bağlı verileri olan:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-175">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="4a1e1-176">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-176">3.2.3.</span></span> <span data-ttu-id="4a1e1-177">Alışveriş sepeti olay Ekle</span><span class="sxs-lookup"><span data-stu-id="4a1e1-177">Add Shopping Cart Event</span></span>
<span data-ttu-id="4a1e1-178">Bu olay kullanılmalıdır hello kullanıcı alışveriş sepeti öğesi toohello eklediğinizde.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-178">This event should be used when hello user add an item toohello shopping cart.</span></span>
<span data-ttu-id="4a1e1-179">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-179">Parameters:</span></span>

* <span data-ttu-id="4a1e1-180">Olay (dize, zorunlu) - "addshopcart"</span><span class="sxs-lookup"><span data-stu-id="4a1e1-180">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="4a1e1-181">öğe (dize, zorunlu) - hello öğesinin benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="4a1e1-181">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="4a1e1-182">ItemName (dize, isteğe bağlı) - hello öğesinin hello adı</span><span class="sxs-lookup"><span data-stu-id="4a1e1-182">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="4a1e1-183">itemDescription (dize, isteğe bağlı) - hello öğenin hello açıklaması</span><span class="sxs-lookup"><span data-stu-id="4a1e1-183">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="4a1e1-184">itemCategory (dize, isteğe bağlı) - hello öğesinin hello kategorisi</span><span class="sxs-lookup"><span data-stu-id="4a1e1-184">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="4a1e1-185">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-185">3.2.4.</span></span> <span data-ttu-id="4a1e1-186">Alışveriş sepeti olay Kaldır</span><span class="sxs-lookup"><span data-stu-id="4a1e1-186">Remove Shopping Cart Event</span></span>
<span data-ttu-id="4a1e1-187">Bu olay Hello kullanıcı bir öğeyi toohello alışveriş sepeti kaldırdığında kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-187">This event should be used when hello user removes an item toohello shopping cart.</span></span>

<span data-ttu-id="4a1e1-188">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-188">Parameters:</span></span>

* <span data-ttu-id="4a1e1-189">Olay (dize, zorunlu) - "removeshopcart"</span><span class="sxs-lookup"><span data-stu-id="4a1e1-189">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="4a1e1-190">öğe (dize, zorunlu) - hello öğesinin benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="4a1e1-190">item (string, mandatory) - Unique identifier of hello item</span></span>
* <span data-ttu-id="4a1e1-191">ItemName (dize, isteğe bağlı) - hello öğesinin hello adı</span><span class="sxs-lookup"><span data-stu-id="4a1e1-191">itemName (string, optional) - hello name of hello item</span></span>
* <span data-ttu-id="4a1e1-192">itemDescription (dize, isteğe bağlı) - hello öğenin hello açıklaması</span><span class="sxs-lookup"><span data-stu-id="4a1e1-192">itemDescription (string, optional) - hello description of hello item</span></span>
* <span data-ttu-id="4a1e1-193">itemCategory (dize, isteğe bağlı) - hello öğesinin hello kategorisi</span><span class="sxs-lookup"><span data-stu-id="4a1e1-193">itemCategory (string, optional) - hello category of hello item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="4a1e1-194">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-194">3.2.5.</span></span> <span data-ttu-id="4a1e1-195">Satın alma olayı</span><span class="sxs-lookup"><span data-stu-id="4a1e1-195">Purchase Event</span></span>
<span data-ttu-id="4a1e1-196">Bu olay Hello kullanıcı kendi alışveriş sepeti satın aldığınızda kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-196">This event should be used when hello user purchased his shopping cart.</span></span>

<span data-ttu-id="4a1e1-197">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-197">Parameters:</span></span>

* <span data-ttu-id="4a1e1-198">Olay (dize) - "satın"</span><span class="sxs-lookup"><span data-stu-id="4a1e1-198">event (string) - “purchase”</span></span>
* <span data-ttu-id="4a1e1-199">öğeleri - (satın []) bir giriş her biri için madde satın bulunduran dizi.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-199">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="4a1e1-200">Satın alınan biçimi:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-200">Purchased format:</span></span>
  * <span data-ttu-id="4a1e1-201">öğe (dize) - hello öğesinin benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-201">item (string) - Unique identifier of hello item.</span></span>
  * <span data-ttu-id="4a1e1-202">Count (int veya dize) - satın alınan öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-202">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="4a1e1-203">Fiyat (kayan noktalı sayı veya dize) - isteğe bağlı alan - hello fiyatı hello öğesi.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-203">price (float or string) - optional field - hello price of hello item.</span></span>

<span data-ttu-id="4a1e1-204">Merhaba örnekte gösterilir 3 satın öğeleri (33 34, 35), iki doldurulmuş tüm alanlar (öğe sayısı, Fiyat) ve biri (öğesi 34) olmadan bir fiyat.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-204">hello example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="4a1e1-205">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-205">3.2.6.</span></span> <span data-ttu-id="4a1e1-206">Kullanıcı oturum açma olayı</span><span class="sxs-lookup"><span data-stu-id="4a1e1-206">User Login Event</span></span>
<span data-ttu-id="4a1e1-207">Azure ML önerileri olay kitaplığı oluşturur ve kullanım bir tanımlama bilgisinde nereden geldiğini sipariş tooidentify olayları aynı tarayıcı hello.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-207">Azure ML Recommendations Event library creates and use a cookie in order tooidentify events that came from hello same browser.</span></span> <span data-ttu-id="4a1e1-208">Sipariş tooimprove hello modelinde tooset hello tanımlama bilgisi kullanımı geçersiz kılacak olan kullanıcı için benzersiz bir kimlik sonuçları Azure ML önerileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-208">In order tooimprove hello model results Azure ML Recommendations enables tooset a user unique identification that will override hello cookie usage.</span></span>

<span data-ttu-id="4a1e1-209">Bu olay hello kullanıcı oturum açma tooyour site sonra kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-209">This event should be used after hello user login tooyour site.</span></span>

<span data-ttu-id="4a1e1-210">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-210">Parameters:</span></span>

* <span data-ttu-id="4a1e1-211">Olay (dize) - "userlogin"</span><span class="sxs-lookup"><span data-stu-id="4a1e1-211">event (string) - “userlogin”</span></span>
* <span data-ttu-id="4a1e1-212">Kullanıcı (dize) - hello kullanıcının benzersiz kimliği.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-212">user (string) - unique identification of hello user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="4a1e1-213">4. JavaScript aracılığıyla önerileri kullanma</span><span class="sxs-lookup"><span data-stu-id="4a1e1-213">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="4a1e1-214">Merhaba öneri tüketir hello kod bazı JavaScript olayı tarafından hello istemcinin Web sayfası tarafından tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-214">hello code that consumes hello recommendation is triggered by some JavaScript event by hello client’s webpage.</span></span> <span data-ttu-id="4a1e1-215">Merhaba öneri yanıt önerilen öğeleri kimlikleri, adlarını ve derecelendirmelerine hello içeriyor.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-215">hello recommendation response includes hello recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="4a1e1-216">Bu seçeneği yalnızca bir listesini görüntülemek için önerilen öğelerin - (Merhaba öğesi'nin meta verilerin eklenmesi gibi) işleme daha karmaşık hello hello sunucu tarafı tümleştirme üzerinde yapılmalıdır en iyi toouse olur.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-216">It’s best toouse this option only for a list display of hello recommended items - more complex handling (such as adding hello item’s metadata) should be done on hello server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="4a1e1-217">4.1 önerileri kullanma</span><span class="sxs-lookup"><span data-stu-id="4a1e1-217">4.1 Consume Recommendations</span></span>
<span data-ttu-id="4a1e1-218">tooinclude hello gereksinim tooconsume öneriler sayfası ve toocall AzureMLRecommendationsStart JavaScript kitaplıkları gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-218">tooconsume recommendations you need tooinclude hello required JavaScript libraries in your page and toocall AzureMLRecommendationsStart.</span></span> <span data-ttu-id="4a1e1-219">2 bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-219">See section 2.</span></span>

<span data-ttu-id="4a1e1-220">tooconsume önerileri bir veya daha fazla öğe için bir yöntem olarak adlandırılan toocall gerekir: AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-220">tooconsume recommendations for one or more items you need toocall a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="4a1e1-221">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-221">Parameters:</span></span>

* <span data-ttu-id="4a1e1-222">(bir dizeler dizisi) - bir veya daha fazla öğe tooget önerileri için öğeleri.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-222">items (array of strings) - One or more items tooget recommendations for.</span></span> <span data-ttu-id="4a1e1-223">Bir Fbt yapı kullanmak, yalnızca bir öğe burada ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-223">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="4a1e1-224">numberOfResults (int) - gerekli sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-224">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="4a1e1-225">includeMetadata (boolean, isteğe bağlı) - varsa too'true ayarlamak ' hello sonucunda o hello meta veri alanı doldurulur gösterir.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-225">includeMetadata (boolean, optional) - if set too‘true’ indicates that hello metadata field must be populated in hello result.</span></span>
* <span data-ttu-id="4a1e1-226">İşleme işlevi - hello önerileri işleyecek bir işlev döndürdü.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-226">Processing function - a function that will handle hello recommendations returned.</span></span> <span data-ttu-id="4a1e1-227">Merhaba veri bir dizi döndürdü:</span><span class="sxs-lookup"><span data-stu-id="4a1e1-227">hello data is returned as an array of:</span></span>
  * <span data-ttu-id="4a1e1-228">Madde - öğesi benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="4a1e1-228">Item - item unique id</span></span>
  * <span data-ttu-id="4a1e1-229">ad - öğesi adına (varsa kataloğunda var)</span><span class="sxs-lookup"><span data-stu-id="4a1e1-229">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="4a1e1-230">Derecelendirme - öneri derecelendirme</span><span class="sxs-lookup"><span data-stu-id="4a1e1-230">rating - recommendation rating</span></span>
  * <span data-ttu-id="4a1e1-231">Meta veriler - hello öğesinin hello meta verileri temsil eden bir dize</span><span class="sxs-lookup"><span data-stu-id="4a1e1-231">metadata - a string that represents hello metadata of hello item</span></span>

<span data-ttu-id="4a1e1-232">Örnek: "64f6eb0d-947a-4c18-a16c-888da9e228ba" öğesi için 8 önerileri koddan hello istekleri (değil belirleyerek includeMetadata - diyor örtük olarak meta veri gereklidir), bunu daha sonra birleştirme hello sonuçları bir arabelleğe.</span><span class="sxs-lookup"><span data-stu-id="4a1e1-232">Example: hello following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate hello results into a buffer.</span></span>

        <script>
             var reco = AzureMLRecommendationsGetI2IRecommendation(["64f6eb0d-947a-4c18-a16c-888da9e228ba"], 8, false, function (reco) {
                 var buff = "";
                 for (var ii = 0; ii < reco.length; ii++) {
                       buff += reco[ii].item + "," + reco[ii].name + "," + reco[ii].rating + "\n";
                 }
                 alert(buff);
            });
        </script>


[1]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing1.png
[2]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing2.png
[3]: ./media/machine-learning-recommendation-api-javascript-integration/Drawing3.png
