---
title: "aaaAdd koşulları ve iş akışları - Azure Logic Apps başlatın | Microsoft Docs"
description: "İş akışları Azure Logic Apps içinde koşullu mantık, Tetikleyiciler, Eylemler ve parametreleri ekleyerek çalışma şeklini denetler."
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: e4e24de4-049a-4b3a-a14c-3bf3163287a8
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/28/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: 76d5e44590ffa14cf70d7a93b99a241d286d555b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="88558-103">Logic Apps özelliklerini kullanma</span><span class="sxs-lookup"><span data-stu-id="88558-103">Use Logic Apps features</span></span>

<span data-ttu-id="88558-104">İçinde bir [önceki konu](../logic-apps/logic-apps-create-a-logic-app.md), ilk mantıksal uygulamanızı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="88558-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="88558-105">toocontrol mantığı uygulamanızın iş akışı için logic app toorun farklı yollarını belirtin ve nasıl çok veri dizileri, koleksiyonlar ve toplu işlem.</span><span class="sxs-lookup"><span data-stu-id="88558-105">toocontrol your logic app's workflow, you can specify different paths for your logic app toorun and how too process data in arrays, collections, and batches.</span></span> <span data-ttu-id="88558-106">Bu öğeleri mantığı uygulama akışınızda içerebilir:</span><span class="sxs-lookup"><span data-stu-id="88558-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="88558-107">Koşullar ve [switch ifadeleri](../logic-apps/logic-apps-switch-case.md) belirli koşulların karşılanıp karşılanmadığını bağlı olarak farklı eylemler çalıştırmak mantıksal uygulamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="88558-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="88558-108">[Döngüler](../logic-apps/logic-apps-loops-and-scopes.md) adımları tekrar tekrar çalıştırmak mantıksal uygulamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="88558-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="88558-109">Kullandığınızda Örneğin, Eylemler bir dizi yineleyebilirsiniz bir **For_each** döngü.</span><span class="sxs-lookup"><span data-stu-id="88558-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="88558-110">Ya da kullanırken bir koşul yerine getirilene kadar Eylemler yineleyebilirsiniz bir **kadar** döngü.</span><span class="sxs-lookup"><span data-stu-id="88558-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="88558-111">[Kapsamları](../logic-apps/logic-apps-loops-and-scopes.md) let gruplandırma Eylemler dizisi birlikte, örneğin, tooimplement özel durum işleme.</span><span class="sxs-lookup"><span data-stu-id="88558-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, tooimplement exception handling.</span></span>

* <span data-ttu-id="88558-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) hello kullandığınızda bir dizi öğeleri için ayrı iş akışlarını başlatmak mantıksal uygulamanızı sağlar **SplitOn** komutu.</span><span class="sxs-lookup"><span data-stu-id="88558-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use hello **SplitOn** command.</span></span>

<span data-ttu-id="88558-113">Bu konu, mantıksal uygulamanızı oluşturmaya yönelik diğer kavramları sunar:</span><span class="sxs-lookup"><span data-stu-id="88558-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="88558-114">Görünüm tooedit var olan bir mantıksal uygulama kodu</span><span class="sxs-lookup"><span data-stu-id="88558-114">Code view tooedit an existing logic app</span></span>
* <span data-ttu-id="88558-115">Bir iş akışı başlatma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="88558-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="88558-116">Koşullar: yalnızca bir koşul yerine getirdikten sonra adımları çalıştırın</span><span class="sxs-lookup"><span data-stu-id="88558-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="88558-117">toohave adımları yalnızca veri belirli ölçütleri karşıladığında Çalıştır mantıksal uygulamanızı belirli alanlar veya değerler karşı hello akışındaki verileri karşılaştıran bir koşulu ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88558-117">toohave your logic app run steps only when data meets specific criteria, you can add a condition that compares data in hello workflow against specific fields or values.</span></span>

<span data-ttu-id="88558-118">Örneğin, bir Web sitesinin RSS akışı gönderileri için çok fazla e-posta gönderen bir mantıksal uygulama olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="88558-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="88558-119">Yalnızca yeni hello duyurduğumuzda mantıksal uygulamanızı e-posta gönderir. böylece bir koşul tooa belirli kategori ait ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88558-119">You can add a condition so that your logic app sends email only when hello new post belongs tooa specific category.</span></span>

1. <span data-ttu-id="88558-120">Merhaba, [Azure portal](https://portal.azure.com), bulma ve mantığı Uygulama Tasarımcısı'nda mantıksal uygulamanızı açın.</span><span class="sxs-lookup"><span data-stu-id="88558-120">In hello [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="88558-121">İstediğiniz koşulu toohello iş akışı konum ekleyin.</span><span class="sxs-lookup"><span data-stu-id="88558-121">Add a condition toohello workflow location that you want.</span></span> 

   <span data-ttu-id="88558-122">Merhaba mantığı uygulama iş akışında, var olan adımları arasında tooadd hello koşul işaretçisini hello hello ok tooadd hello koşul istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="88558-122">tooadd hello condition between existing steps in hello logic app workflow, move hello pointer over hello arrow where you want tooadd hello condition.</span></span> 
   <span data-ttu-id="88558-123">Merhaba seçin **artı** (**+**), ardından **bir koşul eklemek**.</span><span class="sxs-lookup"><span data-stu-id="88558-123">Choose hello **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="88558-124">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="88558-124">For example:</span></span>

   ![Koşul toologic uygulama Ekle](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="88558-126">Merhaba, geçerli iş akışınızı sonunda tooadd bir koşul istiyorsanız, mantıksal uygulamanızı toohello sonuna gidin ve seçin **+ yeni adım**.</span><span class="sxs-lookup"><span data-stu-id="88558-126">If you want tooadd a condition at hello end of your current workflow, go toohello bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="88558-127">Şimdi hello koşul tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="88558-127">Now define hello condition.</span></span> <span data-ttu-id="88558-128">Merhaba kaynak alan tooevaluate, hello işlemi tooperform ve hello hedef değer veya alan istediğinizi belirtin.</span><span class="sxs-lookup"><span data-stu-id="88558-128">Specify hello source field that you want tooevaluate, hello operation tooperform, and hello target value or field.</span></span> <span data-ttu-id="88558-129">tooadd var olan alanları tooyour koşul hello seçin **Ekle dinamik içerik listesi**.</span><span class="sxs-lookup"><span data-stu-id="88558-129">tooadd existing fields tooyour condition, choose from hello **Add dynamic content list**.</span></span>

   <span data-ttu-id="88558-130">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="88558-130">For example:</span></span>

   ![Koşul temel modunda düzenleme](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="88558-132">Merhaba tam koşul şöyledir:</span><span class="sxs-lookup"><span data-stu-id="88558-132">Here's hello complete condition:</span></span>

   ![Tam koşul](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="88558-134">kodda, toodefine hello koşulu seçin **Gelişmiş modda Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="88558-134">toodefine hello condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="88558-135">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="88558-135">For example:</span></span>
   > 
   > ![Kod koşulunda Düzenle](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="88558-137">Altında **Evet IF** ve **IF Hayır**, hello koşula uyulup uyulmadığını dayalı hello adımları tooperform ekleyin.</span><span class="sxs-lookup"><span data-stu-id="88558-137">Under **IF YES** and **IF NO**, add hello steps tooperform based on whether hello condition is met.</span></span>

   <span data-ttu-id="88558-138">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="88558-138">For example:</span></span>

   ![Evet ve hiçbir yol koşulu](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="88558-140">Var olan eylemler hello sürükleyin **Evet IF** ve **IF Hayır** yolları.</span><span class="sxs-lookup"><span data-stu-id="88558-140">You can drag existing actions into hello **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="88558-141">İşiniz bittiğinde, mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="88558-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="88558-142">Şimdi yalnızca hello gönderileri koşulunuz karşıladığında e-postaları alın.</span><span class="sxs-lookup"><span data-stu-id="88558-142">Now you get emails only when hello posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="88558-143">Eylemler forEach ile bir liste üzerinden yineleme</span><span class="sxs-lookup"><span data-stu-id="88558-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="88558-144">Merhaba forEach döngüsü üzerinde bir dizi toorepeat bir eylem belirtir.</span><span class="sxs-lookup"><span data-stu-id="88558-144">hello forEach loop specifies an array toorepeat an action over.</span></span> <span data-ttu-id="88558-145">Bir dizi değil hello akış başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="88558-145">If it is not an array, hello flow fails.</span></span> <span data-ttu-id="88558-146">Örneğin, iletileri dizisini çıkarır action1 varsa ve her iletinin toosend istiyorsanız, eylemin hello özelliklerinde bu forEach deyimi içerebilir:`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="88558-146">For example, if you have action1 that outputs an array of messages, and you want toosend each message, you can include this forEach statement in hello properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-hello-code-definition-for-a-logic-app"></a><span data-ttu-id="88558-147">Bir mantıksal uygulama için Hello kodu tanımını düzenleme</span><span class="sxs-lookup"><span data-stu-id="88558-147">Edit hello code definition for a logic app</span></span>

<span data-ttu-id="88558-148">Merhaba mantığı Uygulama Tasarımcısı sahip olsa da, bir mantıksal uygulama tanımlayan hello kodu doğrudan düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88558-148">Although you have hello Logic App Designer, you can directly edit hello code that defines a logic app.</span></span>

1. <span data-ttu-id="88558-149">Merhaba komut çubuğunda seçin **kod görünümü**.</span><span class="sxs-lookup"><span data-stu-id="88558-149">On hello command bar, choose **Code view**.</span></span>

    <span data-ttu-id="88558-150">Bir tam Düzenleyicisi'ni açar ve düzenlediğiniz hello tanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="88558-150">A full editor opens and shows hello definition you edited.</span></span>

    ![Kod Görünümü](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="88558-152">Merhaba Metin Düzenleyicisi'nde kopyalayın ve herhangi bir sayıda hello içinde eylemler yapıştırın aynı mantıksal uygulama ya da mantıksal uygulamalar arasında.</span><span class="sxs-lookup"><span data-stu-id="88558-152">In hello text editor, you can copy and paste any number of actions within hello same logic app or between logic apps.</span></span> 
    <span data-ttu-id="88558-153">Ayrıca kolayca eklemenize veya tüm bölümleri hello tanımından kaldırın ve ayrıca tanımları başkalarıyla paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88558-153">You can also easily add or remove entire sections from hello definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="88558-154">Yaptığınız düzenlemeleri toosave seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="88558-154">toosave your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="88558-155">Parametreler</span><span class="sxs-lookup"><span data-stu-id="88558-155">Parameters</span></span>

<span data-ttu-id="88558-156">Bazı Logic Apps özellikleri yalnızca kod görünümünde, örneğin, parametreleri sağlanır.</span><span class="sxs-lookup"><span data-stu-id="88558-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="88558-157">Parametreleri kolay tooreuse değerleri mantıksal uygulamanızı boyunca kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="88558-157">Parameters make it easy tooreuse values throughout your logic app.</span></span> <span data-ttu-id="88558-158">Örneğin, çeşitli eylemler kullanmak istediğiniz bir e-posta adresi varsa, bu e-posta adresi parametre olarak tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="88558-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="88558-159">Büyük olasılıkla toochange çok olmayan değerler çekmek için iyi parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="88558-159">Parameters are good for pulling out values that you are likely toochange a lot.</span></span> <span data-ttu-id="88558-160">Bunlar, özellikle farklı ortamlarda toooverride parametreleri gerektiğinde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="88558-160">They are especially useful when you need toooverride parameters in different environments.</span></span> <span data-ttu-id="88558-161">ortamında, temel toooverride parametreleri nasıl görürüm toolearn [Yazar mantıksal uygulama tanımları](../logic-apps/logic-apps-author-definitions.md) ve [REST API belgeleri](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="88558-161">toolearn how toooverride parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="88558-162">Bu örnekte gösterilir nasıl tooupdate var olan mantıksal uygulamanızı böylece hello sorgu dönem için parametreleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88558-162">This example shows how tooupdate your existing logic app so that you can use parameters for hello query term.</span></span>

1. <span data-ttu-id="88558-163">Kod Görünümü'nde hello bulur `parameters : {}` nesne ve ekleme bir `currentFeedUrl` nesnesi:</span><span class="sxs-lookup"><span data-stu-id="88558-163">In code view, find hello `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="88558-164">Toohello Git `When_a_feed-item_is_published` eylem, Bul hello `queries` bölümünde ve hello sorgu değerle değiştirin:`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="88558-164">Go toohello `When_a_feed-item_is_published` action, find hello `queries` section, and replace hello query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="88558-165">toojoin iki veya daha fazla dizeleri hello de kullanabilirsiniz `concat` işlevi.</span><span class="sxs-lookup"><span data-stu-id="88558-165">toojoin two or more strings, you can also use hello `concat` function.</span></span> 
    <span data-ttu-id="88558-166">Örneğin, `"@concat('#',parameters('currentFeedUrl'))"` works hello aynı hello yukarıdaki.</span><span class="sxs-lookup"><span data-stu-id="88558-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works hello same as hello above.</span></span>

3.  <span data-ttu-id="88558-167">İşiniz bittiğinde seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="88558-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="88558-168">Merhaba Web sitesinin RSS hello yoluyla farklı bir URL geçirerek akışı değiştirebileceğiniz artık `currentFeedURL` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="88558-168">Now you can change hello website's RSS feed by passing a different URL through hello `currentFeedURL` object.</span></span>

<span data-ttu-id="88558-169">Daha fazla bilgi edinmek [nasıl tooauthor mantıksal uygulama tanımları](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="88558-169">Learn more about [how tooauthor logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="88558-170">Mantıksal uygulama iş akışlarını başlatmak</span><span class="sxs-lookup"><span data-stu-id="88558-170">Start logic app workflows</span></span>

<span data-ttu-id="88558-171">Mantıksal uygulamanızı tanımlanan hello iş akışını başlatmak için farklı seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="88558-171">You have different options for starting hello workflow defined in your logic app.</span></span> <span data-ttu-id="88558-172">Her zaman bir iş akışı isteğe bağlı hello başlatabilirsiniz [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="88558-172">You can always start a workflow on-demand in hello [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="88558-173">Yineleme Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="88558-173">Recurrence triggers</span></span>

<span data-ttu-id="88558-174">Bir yineleme tetikleyici, belirttiğiniz bir zaman aralığında çalışır.</span><span class="sxs-lookup"><span data-stu-id="88558-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="88558-175">Koşullu mantık Hello tetikleyicisine sahip olduğunda hello tetikleyici hello iş akışı toorun gerekip gerekmediğini belirler.</span><span class="sxs-lookup"><span data-stu-id="88558-175">When hello trigger has conditional logic, hello trigger determines whether hello workflow needs toorun.</span></span> <span data-ttu-id="88558-176">Tetikleyici hello iş akışı döndürerek çalışmalı gösteren bir `200` durum kodu.</span><span class="sxs-lookup"><span data-stu-id="88558-176">A trigger indicates hello workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="88558-177">Merhaba tetikleyici döndürür Hello iş akışı toorun gerek yoktur, bir `202` durum kodu.</span><span class="sxs-lookup"><span data-stu-id="88558-177">When hello workflow doesn't need toorun, hello trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="88558-178">REST API'lerini kullanarak geri çağırma</span><span class="sxs-lookup"><span data-stu-id="88558-178">Callback using REST APIs</span></span>

<span data-ttu-id="88558-179">toostart bir iş akışı, bir mantıksal uygulama uç noktası Hizmetleri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="88558-179">toostart a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="88558-180">Bu tür bir mantıksal uygulama isteğe bağlı, toostart seçin **Şimdi Çalıştır** hello komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="88558-180">toostart this kind of logic app on-demand, choose **Run now** on hello command bar.</span></span> <span data-ttu-id="88558-181">Bkz: [Tetikleyiciler olarak uygulama uç noktaları mantığı çağırarak iş akışlarını başlatmak](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="88558-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
[Azure portal]: https://portal.azure.com

## <a name="next-steps"></a><span data-ttu-id="88558-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="88558-183">Next steps</span></span>

* [<span data-ttu-id="88558-184">Switch deyimleri</span><span class="sxs-lookup"><span data-stu-id="88558-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="88558-185">Döngüler, kapsamlar ve ayırma</span><span class="sxs-lookup"><span data-stu-id="88558-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="88558-186">Mantıksal uygulama tanımları yazma</span><span class="sxs-lookup"><span data-stu-id="88558-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)