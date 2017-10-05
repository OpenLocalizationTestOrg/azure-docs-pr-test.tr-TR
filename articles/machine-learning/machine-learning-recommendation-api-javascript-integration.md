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
redirect_document_id: TRUE
ms.openlocfilehash: 8f27962d097bffc2a03de80244ae41d6573a4bf3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-machine-learning-recommendations---javascript-integration"></a><span data-ttu-id="555be-103">Azure Machine Learning Önerileri - JavaScript Tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="555be-103">Azure Machine Learning Recommendations - JavaScript Integration</span></span>
> [!NOTE]
> <span data-ttu-id="555be-104">Öneriler API Bilişsel hizmeti yerine bu sürümünü kullanarak başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="555be-104">You should start using the Recommendations API Cognitive Service instead of this version.</span></span> <span data-ttu-id="555be-105">Öneriler Bilişsel hizmet bu hizmeti koyacağınız ve tüm yeni özellikler vardır geliştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="555be-105">The Recommendations Cognitive Service will be replacing this service, and all the new features will be developed there.</span></span> <span data-ttu-id="555be-106">Toplu işlem desteği, daha iyi API'si Gezgini, bir temizleyici API yüzeyi, daha tutarlı kaydolma/faturalandırma deneyimi, vb. gibi yeni özellikler vardır.</span><span class="sxs-lookup"><span data-stu-id="555be-106">It has new capabilities like batching support, a better API Explorer, a cleaner API surface, more consistent signup/billing experience, etc.</span></span>
> <span data-ttu-id="555be-107">Daha fazla bilgi edinmek [yeni Bilişsel Service'e geçirme](http://aka.ms/recomigrate)</span><span class="sxs-lookup"><span data-stu-id="555be-107">Learn more about [Migrating to the new Cognitive Service](http://aka.ms/recomigrate)</span></span>
> 
> 

<span data-ttu-id="555be-108">Bu belge, sitenizi JavaScript kullanarak tümleştirme tarif.</span><span class="sxs-lookup"><span data-stu-id="555be-108">This document depict how to integrate your site using JavaScript.</span></span> <span data-ttu-id="555be-109">JavaScript, veri alım olayları göndermek için ve bir öneri modeli yapı sonra öneriler tüketmeye sağlar.</span><span class="sxs-lookup"><span data-stu-id="555be-109">The JavaScript enables you to send Data Acquisition events and to consume recommendations once you build a recommendation model.</span></span> <span data-ttu-id="555be-110">JS yapılan tüm işlemler de sunucu tarafındaki yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="555be-110">All operations done via JS can be also done from server side.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="1-general-overview"></a><span data-ttu-id="555be-111">1. Genel bakış</span><span class="sxs-lookup"><span data-stu-id="555be-111">1. General Overview</span></span>
<span data-ttu-id="555be-112">Azure ML önerileri sitenizi tümleştirme 2 aşamalara oluşur:</span><span class="sxs-lookup"><span data-stu-id="555be-112">Integrating your site with Azure ML Recommendations consist on 2 Phases:</span></span>

1. <span data-ttu-id="555be-113">Olayları Azure ML önerileri gönderin.</span><span class="sxs-lookup"><span data-stu-id="555be-113">Send Events into Azure ML Recommendations.</span></span> <span data-ttu-id="555be-114">Bu öneri modeli oluşturmaya olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="555be-114">This will enable to build a recommendation model.</span></span>
2. <span data-ttu-id="555be-115">Öneriler kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="555be-115">Consume the recommendations.</span></span> <span data-ttu-id="555be-116">Model oluşturulduktan sonra öneriler kullanmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="555be-116">After the model is built you can consume the recommendations.</span></span> <span data-ttu-id="555be-117">(Bu belgede bir model oluşturmak nasıl açıklamaz okuma hakkında daha fazla bilgi almak için Hızlı Başlangıç Kılavuzu).</span><span class="sxs-lookup"><span data-stu-id="555be-117">(This document does not explain how to build a model, read the quick start guide to get more information on how).</span></span>

<span data-ttu-id="555be-118"><ins>Aşama ı</ins></span><span class="sxs-lookup"><span data-stu-id="555be-118"><ins>Phase I</ins></span></span>

<span data-ttu-id="555be-119">İlk aşamada, bunlar html sayfasında Azure ML önerileri sunucularına (aracılığıyla veri Pazar) ortaya çıktığında olayları göndermek için sayfadaki sağlayan küçük bir JavaScript kitaplığı html sayfalarınıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="555be-119">In the first phase you insert into your html pages a small JavaScript library that enables the page to send events as they occur on the html page into Azure ML Recommendations servers (via Data Market):</span></span>

![Drawing1][1]

<span data-ttu-id="555be-121"><ins>Aşama II</ins></span><span class="sxs-lookup"><span data-stu-id="555be-121"><ins>Phase II</ins></span></span>

<span data-ttu-id="555be-122">Sayfada önerileri göstermek istediğiniz zaman ikinci aşamasında aşağıdaki seçeneklerden birini seçin:</span><span class="sxs-lookup"><span data-stu-id="555be-122">In the second phase when you want to show the recommendations on the page you select one of the following options:</span></span>

<span data-ttu-id="555be-123">1. sunucunuzda (sayfa işleme aşama) Azure ML önerileri sunucusu önerileri almak için (veri Pazar) çağırır.</span><span class="sxs-lookup"><span data-stu-id="555be-123">1.Your server (on the phase of page rendering) calls Azure ML Recommendations Server (via Data Market) to get recommendations.</span></span> <span data-ttu-id="555be-124">Sonuçlar öğeleri kimliği listesini içerir.</span><span class="sxs-lookup"><span data-stu-id="555be-124">The results include a list of items id.</span></span> <span data-ttu-id="555be-125">Meta veriler (örn. görüntüler, açıklama) öğeleri sonuçlardan zenginleştirmek ve oluşturulan sayfa tarayıcıya göndermek sunucunuzu gerekir.</span><span class="sxs-lookup"><span data-stu-id="555be-125">Your server needs to enrich the results with the items Meta data (e.g. images, description) and send the created page to the browser.</span></span>

![Drawing2][2]

<span data-ttu-id="555be-127">2. diğer seçenek önerilen öğeler basit bir listesini almak için birinci aşaması küçük JavaScript dosyasından kullanmaktır.</span><span class="sxs-lookup"><span data-stu-id="555be-127">2.The other option is to use the small JavaScript file from phase one to get a simple list of recommended items.</span></span> <span data-ttu-id="555be-128">Burada alınan ilk seçeneğinde olandan daha yalın veridir.</span><span class="sxs-lookup"><span data-stu-id="555be-128">The data received here is leaner than the one in the first option.</span></span>

![Drawing3][3]

## <a name="2-prerequisites"></a><span data-ttu-id="555be-130">2. Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="555be-130">2. Prerequisites</span></span>
1. <span data-ttu-id="555be-131">API'lerini kullanarak yeni bir model oluşturun.</span><span class="sxs-lookup"><span data-stu-id="555be-131">Create a new model using the APIs.</span></span> <span data-ttu-id="555be-132">Yapmak Hızlı Başlangıç Kılavuzu bakın.</span><span class="sxs-lookup"><span data-stu-id="555be-132">See the Quick start guide on how to do it.</span></span>
2. <span data-ttu-id="555be-133">Kodlama, &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; base64 ile.</span><span class="sxs-lookup"><span data-stu-id="555be-133">Encode your &lt;dataMarketUser&gt;:&lt;dataMarketKey&gt; with base64.</span></span> <span data-ttu-id="555be-134">(Bunun için temel kimlik doğrulaması API'leri çağırmak JS kodu etkinleştirmek için kullanılır).</span><span class="sxs-lookup"><span data-stu-id="555be-134">(This will be used for the basic authentication to enable the JS code to call the APIs).</span></span>

## <a name="3-send-data-acquisition-events-using-javascript"></a><span data-ttu-id="555be-135">3. JavaScript kullanarak veri alım olayları Gönder</span><span class="sxs-lookup"><span data-stu-id="555be-135">3. Send Data Acquisition events using JavaScript</span></span>
<span data-ttu-id="555be-136">Aşağıdaki adımları gönderen olaylar kolaylaştırır:</span><span class="sxs-lookup"><span data-stu-id="555be-136">The following steps facilitate sending events:</span></span>

1. <span data-ttu-id="555be-137">JQuery kitaplığı kodunuzda içerir.</span><span class="sxs-lookup"><span data-stu-id="555be-137">Include JQuery library in your code.</span></span> <span data-ttu-id="555be-138">Nuget aşağıdaki URL'de'nden indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="555be-138">You can download it from nuget in the following URL.</span></span>
   
     <span data-ttu-id="555be-139">http://www.nuget.org/Packages/JQuery/1.8.2</span><span class="sxs-lookup"><span data-stu-id="555be-139">http://www.nuget.org/packages/jQuery/1.8.2</span></span>
2. <span data-ttu-id="555be-140">Aşağıdaki URL'yi önerileri Java betiği kitaplığından içerir: http://aka.ms/RecoJSLib1</span><span class="sxs-lookup"><span data-stu-id="555be-140">Include the Recommendations Java Script library from the following URL: http://aka.ms/RecoJSLib1</span></span>
3. <span data-ttu-id="555be-141">Uygun parametrelerle Azure ML önerileri kitaplığı başlatılamıyor.</span><span class="sxs-lookup"><span data-stu-id="555be-141">Initialize Azure ML Recommendations library with the appropriate parameters.</span></span>
   
     <span data-ttu-id="555be-142"><script>AzureMLRecommendationsStart ("<base64encoding of username:key>", "< model_id >"); </script> 
4. Uygun olay gönderin.</span><span class="sxs-lookup"><span data-stu-id="555be-142"><script> AzureMLRecommendationsStart("<base64encoding of username:key>", "<model_id>"); </script>
4. Send the appropriate event.</span></span> <span data-ttu-id="555be-143">Tüm olayları türüne aşağıda ayrıntılı bölümüne bakın (örnek olarak, olay tıklayın) <script> varsa (typeof AzureMLRecommendationsEvent "undefined" ==) {</span><span class="sxs-lookup"><span data-stu-id="555be-143">See detailed section below on all type of events (example of click event)  <script> if (typeof AzureMLRecommendationsEvent=="undefined") {</span></span>         
                     <span data-ttu-id="555be-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({event: "click", item: "18321116"});</script></span><span class="sxs-lookup"><span data-stu-id="555be-144">AzureMLRecommendationsEvent = []; } AzureMLRecommendationsEvent.push({ event: "click", item: "18321116" }); </script></span></span>

### <a name="31----limitations-and-browser-support"></a><span data-ttu-id="555be-145">3.1.</span><span class="sxs-lookup"><span data-stu-id="555be-145">3.1.</span></span>    <span data-ttu-id="555be-146">Sınırlamalar ve tarayıcı desteği</span><span class="sxs-lookup"><span data-stu-id="555be-146">Limitations and Browser Support</span></span>
<span data-ttu-id="555be-147">Bu bir başvuru uygulamasıdır ve olarak verilir.</span><span class="sxs-lookup"><span data-stu-id="555be-147">This is a reference implementation and it is given as is.</span></span> <span data-ttu-id="555be-148">Önde gelen tüm tarayıcılar desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="555be-148">It should support all major browsers.</span></span>

### <a name="32----type-of-events"></a><span data-ttu-id="555be-149">3.2.</span><span class="sxs-lookup"><span data-stu-id="555be-149">3.2.</span></span>    <span data-ttu-id="555be-150">Olay türü</span><span class="sxs-lookup"><span data-stu-id="555be-150">Type of Events</span></span>
<span data-ttu-id="555be-151">Kitaplık destekleyen olay 5 türü vardır:, öneri'ı tıklatın, Ekle'yi tıklatın alışveriş sepetine alışveriş sepeti ve satın alma kaldırın.</span><span class="sxs-lookup"><span data-stu-id="555be-151">There are 5 types of event that the library supports: Click, Recommendation Click, Add to Shop Cart, Remove from Shop Cart and Purchase.</span></span> <span data-ttu-id="555be-152">Oturum açma adı verilen kullanıcı bağlamı ayarlamak için kullanılan ek bir olay yok.</span><span class="sxs-lookup"><span data-stu-id="555be-152">There is an additional event that is used to set the user context called Login.</span></span>

#### <a name="321-click-event"></a><span data-ttu-id="555be-153">3.2.1.</span><span class="sxs-lookup"><span data-stu-id="555be-153">3.2.1.</span></span> <span data-ttu-id="555be-154">Tıklama olayı</span><span class="sxs-lookup"><span data-stu-id="555be-154">Click Event</span></span>
<span data-ttu-id="555be-155">Bu olay, bir kullanıcının bir öğe üzerinde tıkladığınız dilediğiniz zaman kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="555be-155">This event should be used any time a user clicked on an item.</span></span> <span data-ttu-id="555be-156">Genellikle kullanıcı bir öğeyi tıklattığında yeni bir sayfa öğesi ayrıntılarla açıldığında; Bu sayfada, bu olay tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="555be-156">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="555be-157">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="555be-157">Parameters:</span></span>

* <span data-ttu-id="555be-158">"olayı (dize, zorunlu) - tıklayın"</span><span class="sxs-lookup"><span data-stu-id="555be-158">event (string, mandatory) - “click”</span></span>
* <span data-ttu-id="555be-159">öğe (dize, zorunlu) - öğesinin benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="555be-159">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="555be-160">ItemName (dize, isteğe bağlı) - öğesinin adı</span><span class="sxs-lookup"><span data-stu-id="555be-160">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="555be-161">itemDescription (dize, isteğe bağlı) - öğenin açıklaması</span><span class="sxs-lookup"><span data-stu-id="555be-161">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="555be-162">itemCategory (dize, isteğe bağlı) - kategori öğesi</span><span class="sxs-lookup"><span data-stu-id="555be-162">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "click", item: "3111718" });
        </script>

<span data-ttu-id="555be-163">Veya isteğe bağlı verileri olan:</span><span class="sxs-lookup"><span data-stu-id="555be-163">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent === "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "click", item: "3111718", itemName: "Plane", itemDescription: "It is a big plane", itemCategory: "Aviation"});
        </script>


#### <a name="322-recommendation-click-event"></a><span data-ttu-id="555be-164">3.2.2.</span><span class="sxs-lookup"><span data-stu-id="555be-164">3.2.2.</span></span> <span data-ttu-id="555be-165">Öneri, olay'ı tıklatın</span><span class="sxs-lookup"><span data-stu-id="555be-165">Recommendation Click Event</span></span>
<span data-ttu-id="555be-166">Bu olay, bir kullanıcının önerilen bir öğe olarak Azure ML önerilerden alındı bir öğe üzerinde tıkladığınız dilediğiniz zaman kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="555be-166">This event should be used any time a user clicked on an item that was received from Azure ML Recommendations as a recommended item.</span></span> <span data-ttu-id="555be-167">Genellikle kullanıcı bir öğeyi tıklattığında yeni bir sayfa öğesi ayrıntılarla açıldığında; Bu sayfada, bu olay tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="555be-167">Usually when user clicks on an item a new page is opened with the item details; in this page this event should be triggered.</span></span>

<span data-ttu-id="555be-168">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="555be-168">Parameters:</span></span>

* <span data-ttu-id="555be-169">Olay (dize, zorunlu) - "recommendationclick"</span><span class="sxs-lookup"><span data-stu-id="555be-169">event (string, mandatory) - “recommendationclick”</span></span>
* <span data-ttu-id="555be-170">öğe (dize, zorunlu) - öğesinin benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="555be-170">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="555be-171">ItemName (dize, isteğe bağlı) - öğesinin adı</span><span class="sxs-lookup"><span data-stu-id="555be-171">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="555be-172">itemDescription (dize, isteğe bağlı) - öğenin açıklaması</span><span class="sxs-lookup"><span data-stu-id="555be-172">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="555be-173">itemCategory (dize, isteğe bağlı) - kategori öğesi</span><span class="sxs-lookup"><span data-stu-id="555be-173">itemCategory (string, optional) - the category of the item</span></span>
* <span data-ttu-id="555be-174">(dize dizisi, isteğe bağlı) - öneri sorgu oluşturulan oluştururken çekirdeği çekirdeğini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="555be-174">seeds (string array, optional) - the seeds that generated the recommendation query.</span></span>
* <span data-ttu-id="555be-175">recoList (dize dizisi, isteğe bağlı) - tıklandığını maddeden öneri isteğin sonucu.</span><span class="sxs-lookup"><span data-stu-id="555be-175">recoList (string array, optional) - the result of the recommendation request that generated the item that was clicked.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "recommendationclick", item: "18899918" });
        </script>

<span data-ttu-id="555be-176">Veya isteğe bağlı verileri olan:</span><span class="sxs-lookup"><span data-stu-id="555be-176">Or with optional data:</span></span>

        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: eventName, item: "198", itemName: "Plane2", itemDescription: "It is a big plane2", itemCategory: "Default2", seeds: ["Seed1", "Seed2"], recoList: ["199", "198", "197"]                 });
        </script>


#### <a name="323-add-shopping-cart-event"></a><span data-ttu-id="555be-177">3.2.3.</span><span class="sxs-lookup"><span data-stu-id="555be-177">3.2.3.</span></span> <span data-ttu-id="555be-178">Alışveriş sepeti olay Ekle</span><span class="sxs-lookup"><span data-stu-id="555be-178">Add Shopping Cart Event</span></span>
<span data-ttu-id="555be-179">Bu olay kullanılması gereken kullanıcı alışveriş sepetine bir öğe eklediğinizde.</span><span class="sxs-lookup"><span data-stu-id="555be-179">This event should be used when the user add an item to the shopping cart.</span></span>
<span data-ttu-id="555be-180">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="555be-180">Parameters:</span></span>

* <span data-ttu-id="555be-181">Olay (dize, zorunlu) - "addshopcart"</span><span class="sxs-lookup"><span data-stu-id="555be-181">event (string, mandatory) - “addshopcart”</span></span>
* <span data-ttu-id="555be-182">öğe (dize, zorunlu) - öğesinin benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="555be-182">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="555be-183">ItemName (dize, isteğe bağlı) - öğesinin adı</span><span class="sxs-lookup"><span data-stu-id="555be-183">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="555be-184">itemDescription (dize, isteğe bağlı) - öğenin açıklaması</span><span class="sxs-lookup"><span data-stu-id="555be-184">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="555be-185">itemCategory (dize, isteğe bağlı) - kategori öğesi</span><span class="sxs-lookup"><span data-stu-id="555be-185">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent == "undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "addshopcart", item: "13221118" });
        </script>

#### <a name="324-remove-shopping-cart-event"></a><span data-ttu-id="555be-186">3.2.4.</span><span class="sxs-lookup"><span data-stu-id="555be-186">3.2.4.</span></span> <span data-ttu-id="555be-187">Alışveriş sepeti olay Kaldır</span><span class="sxs-lookup"><span data-stu-id="555be-187">Remove Shopping Cart Event</span></span>
<span data-ttu-id="555be-188">Bu olay, kullanıcı bir öğeyi alışveriş sepetine kaldırdığında kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="555be-188">This event should be used when the user removes an item to the shopping cart.</span></span>

<span data-ttu-id="555be-189">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="555be-189">Parameters:</span></span>

* <span data-ttu-id="555be-190">Olay (dize, zorunlu) - "removeshopcart"</span><span class="sxs-lookup"><span data-stu-id="555be-190">event (string, mandatory) - “removeshopcart”</span></span>
* <span data-ttu-id="555be-191">öğe (dize, zorunlu) - öğesinin benzersiz tanıtıcısı</span><span class="sxs-lookup"><span data-stu-id="555be-191">item (string, mandatory) - Unique identifier of the item</span></span>
* <span data-ttu-id="555be-192">ItemName (dize, isteğe bağlı) - öğesinin adı</span><span class="sxs-lookup"><span data-stu-id="555be-192">itemName (string, optional) - the name of the item</span></span>
* <span data-ttu-id="555be-193">itemDescription (dize, isteğe bağlı) - öğenin açıklaması</span><span class="sxs-lookup"><span data-stu-id="555be-193">itemDescription (string, optional) - the description of the item</span></span>
* <span data-ttu-id="555be-194">itemCategory (dize, isteğe bağlı) - kategori öğesi</span><span class="sxs-lookup"><span data-stu-id="555be-194">itemCategory (string, optional) - the category of the item</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "removeshopcart", item: "111118" });
        </script>

#### <a name="325-purchase-event"></a><span data-ttu-id="555be-195">3.2.5.</span><span class="sxs-lookup"><span data-stu-id="555be-195">3.2.5.</span></span> <span data-ttu-id="555be-196">Satın alma olayı</span><span class="sxs-lookup"><span data-stu-id="555be-196">Purchase Event</span></span>
<span data-ttu-id="555be-197">Bu olay, kullanıcının kendi alışveriş sepeti satın aldığınızda kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="555be-197">This event should be used when the user purchased his shopping cart.</span></span>

<span data-ttu-id="555be-198">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="555be-198">Parameters:</span></span>

* <span data-ttu-id="555be-199">Olay (dize) - "satın"</span><span class="sxs-lookup"><span data-stu-id="555be-199">event (string) - “purchase”</span></span>
* <span data-ttu-id="555be-200">öğeleri - (satın []) bir giriş her biri için madde satın bulunduran dizi.</span><span class="sxs-lookup"><span data-stu-id="555be-200">items ( Purchased[] ) - Array holding an entry for each item purchased.</span></span><br><br>
  <span data-ttu-id="555be-201">Satın alınan biçimi:</span><span class="sxs-lookup"><span data-stu-id="555be-201">Purchased format:</span></span>
  * <span data-ttu-id="555be-202">öğe (dize) - öğesinin benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="555be-202">item (string) - Unique identifier of the item.</span></span>
  * <span data-ttu-id="555be-203">Count (int veya dize) - satın alınan öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="555be-203">count (int or string) - number of items that were purchased.</span></span>
  * <span data-ttu-id="555be-204">Fiyat (kayan noktalı sayı veya dize) - isteğe bağlı alan - öğenin fiyat.</span><span class="sxs-lookup"><span data-stu-id="555be-204">price (float or string) - optional field - the price of the item.</span></span>

<span data-ttu-id="555be-205">Aşağıdaki örnek, satın alma 3 gösterir (33, 34, 35) öğeleri iki doldurulmuş tüm alanlar (öğe sayısı, Fiyat) ve biri (öğesi 34) olmadan bir fiyat.</span><span class="sxs-lookup"><span data-stu-id="555be-205">The example below shows purchase of 3 items (33, 34, 35), two with all fields populated (item, count, price) and one (item 34) without a price.</span></span>

        <script>
            if ( typeof AzureMLRecommendationsEvent == "undefined"){ AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({ event: "purchase", items: [{ item: "33", count: "1", price: "10" }, { item: "34", count: "2" }, { item: "35", count: "1", price: "210" }] });
        </script>

#### <a name="326-user-login-event"></a><span data-ttu-id="555be-206">3.2.6.</span><span class="sxs-lookup"><span data-stu-id="555be-206">3.2.6.</span></span> <span data-ttu-id="555be-207">Kullanıcı oturum açma olayı</span><span class="sxs-lookup"><span data-stu-id="555be-207">User Login Event</span></span>
<span data-ttu-id="555be-208">Azure ML önerileri olay kitaplığı oluşturur ve aynı tarayıcıdan gelen olayları belirlemek amacıyla bir tanımlama bilgisi kullanın.</span><span class="sxs-lookup"><span data-stu-id="555be-208">Azure ML Recommendations Event library creates and use a cookie in order to identify events that came from the same browser.</span></span> <span data-ttu-id="555be-209">Model sonuçları Azure ML önerileri geliştirmek için tanımlama bilgisi kullanımı geçersiz kılacak olan kullanıcı için benzersiz bir kimlik ayarlamak için etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="555be-209">In order to improve the model results Azure ML Recommendations enables to set a user unique identification that will override the cookie usage.</span></span>

<span data-ttu-id="555be-210">Bu olay, kullanıcı oturum açma Web sitenize sonra kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="555be-210">This event should be used after the user login to your site.</span></span>

<span data-ttu-id="555be-211">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="555be-211">Parameters:</span></span>

* <span data-ttu-id="555be-212">Olay (dize) - "userlogin"</span><span class="sxs-lookup"><span data-stu-id="555be-212">event (string) - “userlogin”</span></span>
* <span data-ttu-id="555be-213">Kullanıcı (dize) - kullanıcının benzersiz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="555be-213">user (string) - unique identification of the user.</span></span>
  
        <script>
            if (typeof AzureMLRecommendationsEvent=="undefined") { AzureMLRecommendationsEvent = []; }
            AzureMLRecommendationsEvent.push({event: "userlogin", user: “ABCD10AA” });
        </script>

## <a name="4-consume-recommendations-via-javascript"></a><span data-ttu-id="555be-214">4. JavaScript aracılığıyla önerileri kullanma</span><span class="sxs-lookup"><span data-stu-id="555be-214">4. Consume Recommendations via JavaScript</span></span>
<span data-ttu-id="555be-215">Öneri tüketir kod bazı JavaScript olayı tarafından istemci Web sayfası tarafından tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="555be-215">The code that consumes the recommendation is triggered by some JavaScript event by the client’s webpage.</span></span> <span data-ttu-id="555be-216">Öneri yanıt önerilen öğeler kimlikleri, adlarını ve derecelendirmeleri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="555be-216">The recommendation response includes the recommended items Ids, their names and their ratings.</span></span> <span data-ttu-id="555be-217">Yalnızca bir liste görünümünü önerilen öğeler için bu seçeneği kullanmak en iyisidir - sunucu tarafı tümleştirmeye (öğesi'nin meta veri ekleme gibi) daha karmaşık işleme yapılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="555be-217">It’s best to use this option only for a list display of the recommended items - more complex handling (such as adding the item’s metadata) should be done on the server side integration.</span></span>

### <a name="41-consume-recommendations"></a><span data-ttu-id="555be-218">4.1 önerileri kullanma</span><span class="sxs-lookup"><span data-stu-id="555be-218">4.1 Consume Recommendations</span></span>
<span data-ttu-id="555be-219">Kullanmak için sayfanızı ve AzureMLRecommendationsStart çağırmak için gerekli JavaScript kitaplıklarını yapmanız önerileri içerir.</span><span class="sxs-lookup"><span data-stu-id="555be-219">To consume recommendations you need to include the required JavaScript libraries in your page and to call AzureMLRecommendationsStart.</span></span> <span data-ttu-id="555be-220">2 bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="555be-220">See section 2.</span></span>

<span data-ttu-id="555be-221">Bir veya daha fazla öğe için gereken adlı bir yöntemi çağırmak öneriler kullanmak için: AzureMLRecommendationsGetI2IRecommendation.</span><span class="sxs-lookup"><span data-stu-id="555be-221">To consume recommendations for one or more items you need to call a method called: AzureMLRecommendationsGetI2IRecommendation.</span></span>

<span data-ttu-id="555be-222">Parametreler:</span><span class="sxs-lookup"><span data-stu-id="555be-222">Parameters:</span></span>

* <span data-ttu-id="555be-223">(bir dizeler dizisi) - için önerileri almak için bir veya daha fazla öğe öğeleri.</span><span class="sxs-lookup"><span data-stu-id="555be-223">items (array of strings) - One or more items to get recommendations for.</span></span> <span data-ttu-id="555be-224">Bir Fbt yapı kullanmak, yalnızca bir öğe burada ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="555be-224">If you consume an Fbt build then you can set here only one item.</span></span>
* <span data-ttu-id="555be-225">numberOfResults (int) - gerekli sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="555be-225">numberOfResults (int) - number of required results.</span></span>
* <span data-ttu-id="555be-226">includeMetadata (boolean, isteğe bağlı) - meta verileri alan sonucunda doldurulmalıdır 'true' olarak ayarlandığında gösterir.</span><span class="sxs-lookup"><span data-stu-id="555be-226">includeMetadata (boolean, optional) - if set to ‘true’ indicates that the metadata field must be populated in the result.</span></span>
* <span data-ttu-id="555be-227">İşleme işlevi - önerileri işleyecek bir işlev döndürdü.</span><span class="sxs-lookup"><span data-stu-id="555be-227">Processing function - a function that will handle the recommendations returned.</span></span> <span data-ttu-id="555be-228">Bir dizisi olarak döndürülen veriler:</span><span class="sxs-lookup"><span data-stu-id="555be-228">The data is returned as an array of:</span></span>
  * <span data-ttu-id="555be-229">Madde - öğesi benzersiz kimliği</span><span class="sxs-lookup"><span data-stu-id="555be-229">Item - item unique id</span></span>
  * <span data-ttu-id="555be-230">ad - öğesi adına (varsa kataloğunda var)</span><span class="sxs-lookup"><span data-stu-id="555be-230">name - item name (if exist in catalog)</span></span>
  * <span data-ttu-id="555be-231">Derecelendirme - öneri derecelendirme</span><span class="sxs-lookup"><span data-stu-id="555be-231">rating - recommendation rating</span></span>
  * <span data-ttu-id="555be-232">Meta veriler - öğe meta verileri temsil eden bir dize</span><span class="sxs-lookup"><span data-stu-id="555be-232">metadata - a string that represents the metadata of the item</span></span>

<span data-ttu-id="555be-233">Örnek: 8 önerileri öğesi "64f6eb0d-947a-4c18-a16c-888da9e228ba" için aşağıdaki kodu istekleri (değil belirleyerek includeMetadata - diyor örtük olarak meta veri gereklidir), bunu daha sonra birleştirme sonuçları bir arabelleğe.</span><span class="sxs-lookup"><span data-stu-id="555be-233">Example: The following code requests 8 recommendations for item "64f6eb0d-947a-4c18-a16c-888da9e228ba" (and by not specifying includeMetadata - it implicitly says that no metadata is required), it then concatenate the results into a buffer.</span></span>

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
