---
title: "Koşulları ekleme ve iş akışları - Azure Logic Apps başlatın | Microsoft Docs"
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
ms.openlocfilehash: e632c48ed31e82536db55a9c54438bece0c38fd4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-logic-apps-features"></a><span data-ttu-id="da0ff-103">Logic Apps özelliklerini kullanma</span><span class="sxs-lookup"><span data-stu-id="da0ff-103">Use Logic Apps features</span></span>

<span data-ttu-id="da0ff-104">İçinde bir [önceki konu](../logic-apps/logic-apps-create-a-logic-app.md), ilk mantıksal uygulamanızı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="da0ff-104">In a [previous topic](../logic-apps/logic-apps-create-a-logic-app.md), you created your first logic app.</span></span> <span data-ttu-id="da0ff-105">Mantığı uygulamanızın iş akışını denetlemek için mantıksal uygulamanızı çalıştırın ve Diziler, koleksiyonlar ve toplu verileri işlemek nasıl için farklı yollar belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da0ff-105">To control your logic app's workflow, you can specify different paths for your logic app to run and how to process data in arrays, collections, and batches.</span></span> <span data-ttu-id="da0ff-106">Bu öğeleri mantığı uygulama akışınızda içerebilir:</span><span class="sxs-lookup"><span data-stu-id="da0ff-106">You can include these elements in your logic app workflow:</span></span>

* <span data-ttu-id="da0ff-107">Koşullar ve [switch ifadeleri](../logic-apps/logic-apps-switch-case.md) belirli koşulların karşılanıp karşılanmadığını bağlı olarak farklı eylemler çalıştırmak mantıksal uygulamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="da0ff-107">Conditions and [switch statements](../logic-apps/logic-apps-switch-case.md) let your logic app run different actions based on whether specific conditions are met.</span></span>

* <span data-ttu-id="da0ff-108">[Döngüler](../logic-apps/logic-apps-loops-and-scopes.md) adımları tekrar tekrar çalıştırmak mantıksal uygulamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="da0ff-108">[Loops](../logic-apps/logic-apps-loops-and-scopes.md) let your logic app run steps repeatedly.</span></span> <span data-ttu-id="da0ff-109">Kullandığınızda Örneğin, Eylemler bir dizi yineleyebilirsiniz bir **For_each** döngü.</span><span class="sxs-lookup"><span data-stu-id="da0ff-109">For example, you can repeat actions over an array when you use a **For_each** loop.</span></span> <span data-ttu-id="da0ff-110">Ya da kullanırken bir koşul yerine getirilene kadar Eylemler yineleyebilirsiniz bir **kadar** döngü.</span><span class="sxs-lookup"><span data-stu-id="da0ff-110">Or you can repeat actions until a condition is met when you use an **Until** loop.</span></span>

* <span data-ttu-id="da0ff-111">[Kapsamları](../logic-apps/logic-apps-loops-and-scopes.md) let gruplandırma Eylemler dizisi birlikte, örneğin, özel durum işleme uygulamak için.</span><span class="sxs-lookup"><span data-stu-id="da0ff-111">[Scopes](../logic-apps/logic-apps-loops-and-scopes.md) let you group series of actions together, for example, to implement exception handling.</span></span>

* <span data-ttu-id="da0ff-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) kullandığınızda bir dizi öğeleri için ayrı iş akışlarını başlatmak mantıksal uygulamanızı sağlar **SplitOn** komutu.</span><span class="sxs-lookup"><span data-stu-id="da0ff-112">[Debatching](../logic-apps/logic-apps-loops-and-scopes.md) lets your logic app start separate workflows for items in an array when you use the **SplitOn** command.</span></span>

<span data-ttu-id="da0ff-113">Bu konu, mantıksal uygulamanızı oluşturmaya yönelik diğer kavramları sunar:</span><span class="sxs-lookup"><span data-stu-id="da0ff-113">This topic introduces other concepts for building your logic app:</span></span>

* <span data-ttu-id="da0ff-114">Varolan bir mantıksal uygulama düzenlemek için kod görünümü</span><span class="sxs-lookup"><span data-stu-id="da0ff-114">Code view to edit an existing logic app</span></span>
* <span data-ttu-id="da0ff-115">Bir iş akışı başlatma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="da0ff-115">Options for starting a workflow</span></span>

## <a name="conditions-run-steps-only-after-meeting-a-condition"></a><span data-ttu-id="da0ff-116">Koşullar: yalnızca bir koşul yerine getirdikten sonra adımları çalıştırın</span><span class="sxs-lookup"><span data-stu-id="da0ff-116">Conditions: Run steps only after meeting a condition</span></span>

<span data-ttu-id="da0ff-117">Mantıksal uygulamanızı yalnızca veri belirli ölçütleri karşıladığında adımlarını çalıştırmak için iş akışı içinde belirli alanlar veya değerler karşı verileri karşılaştıran bir koşul ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da0ff-117">To have your logic app run steps only when data meets specific criteria, you can add a condition that compares data in the workflow against specific fields or values.</span></span>

<span data-ttu-id="da0ff-118">Örneğin, bir Web sitesinin RSS akışı gönderileri için çok fazla e-posta gönderen bir mantıksal uygulama olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="da0ff-118">For example, suppose you have a logic app that sends you too many emails for posts on a website's RSS feed.</span></span> <span data-ttu-id="da0ff-119">Bir koşul ekleyebilirsiniz, böylece yalnızca belirli bir kategoriye yeni posta ait olduğunda mantıksal uygulamanızı e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="da0ff-119">You can add a condition so that your logic app sends email only when the new post belongs to a specific category.</span></span>

1. <span data-ttu-id="da0ff-120">İçinde [Azure portal](https://portal.azure.com), bulma ve mantığı Uygulama Tasarımcısı'nda mantıksal uygulamanızı açın.</span><span class="sxs-lookup"><span data-stu-id="da0ff-120">In the [Azure portal](https://portal.azure.com), find and open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="da0ff-121">Bir koşul istediğiniz iş akışı konumu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="da0ff-121">Add a condition to the workflow location that you want.</span></span> 

   <span data-ttu-id="da0ff-122">Mantıksal uygulama iş akışı içinde varolan adımlar arasındaki koşul eklemek için üzerinde oku koşulu eklemek istediğiniz işaretçiyi.</span><span class="sxs-lookup"><span data-stu-id="da0ff-122">To add the condition between existing steps in the logic app workflow, move the pointer over the arrow where you want to add the condition.</span></span> 
   <span data-ttu-id="da0ff-123">Seçin **artı** (**+**), ardından **bir koşul eklemek**.</span><span class="sxs-lookup"><span data-stu-id="da0ff-123">Choose the **plus sign** (**+**), then choose **Add a condition**.</span></span> <span data-ttu-id="da0ff-124">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="da0ff-124">For example:</span></span>

   ![Mantıksal uygulama koşul Ekle](./media/logic-apps-use-logic-app-features/add-condition.png)

   > [!NOTE]
   > <span data-ttu-id="da0ff-126">Geçerli iş akışınızı sonunda bir koşul eklemek istiyorsanız, mantıksal uygulamanızı alt kısmına gidin ve seçin **+ yeni adım**.</span><span class="sxs-lookup"><span data-stu-id="da0ff-126">If you want to add a condition at the end of your current workflow, go to the bottom of your logic app, and choose **+ New step**.</span></span>

3. <span data-ttu-id="da0ff-127">Şimdi koşul tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="da0ff-127">Now define the condition.</span></span> <span data-ttu-id="da0ff-128">Değerlendirme, işlemi gerçekleştirmek için ve hedef değer veya alan istediğiniz kaynak alanı belirtin.</span><span class="sxs-lookup"><span data-stu-id="da0ff-128">Specify the source field that you want to evaluate, the operation to perform, and the target value or field.</span></span> <span data-ttu-id="da0ff-129">Var olan alanları, koşulu eklemek için seçin **Ekle dinamik içerik listesi**.</span><span class="sxs-lookup"><span data-stu-id="da0ff-129">To add existing fields to your condition, choose from the **Add dynamic content list**.</span></span>

   <span data-ttu-id="da0ff-130">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="da0ff-130">For example:</span></span>

   ![Koşul temel modunda düzenleme](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode.png)

   <span data-ttu-id="da0ff-132">Tam koşul şöyledir:</span><span class="sxs-lookup"><span data-stu-id="da0ff-132">Here's the complete condition:</span></span>

   ![Tam koşul](./media/logic-apps-use-logic-app-features/edit-condition-basic-mode-2.png)

   > [!TIP]
   > <span data-ttu-id="da0ff-134">Kodda koşulu tanımlamak için tercih **Gelişmiş modda Düzenle**.</span><span class="sxs-lookup"><span data-stu-id="da0ff-134">To define the condition in code, choose **Edit in advanced mode**.</span></span> <span data-ttu-id="da0ff-135">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="da0ff-135">For example:</span></span>
   > 
   > ![Kod koşulunda Düzenle](./media/logic-apps-use-logic-app-features/edit-condition-advanced-mode.png)

4. <span data-ttu-id="da0ff-137">Altında **Evet IF** ve **IF Hayır**, gerçekleştirme adımları temel koşul karşılanır karşılanmaz ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da0ff-137">Under **IF YES** and **IF NO**, add the steps to perform based on whether the condition is met.</span></span>

   <span data-ttu-id="da0ff-138">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="da0ff-138">For example:</span></span>

   ![Evet ve hiçbir yol koşulu](./media/logic-apps-use-logic-app-features/condition-yes-no-path.png)

   > [!TIP]
   > <span data-ttu-id="da0ff-140">Varolan eylemlere sürükleyebilirsiniz **Evet IF** ve **IF Hayır** yollar.</span><span class="sxs-lookup"><span data-stu-id="da0ff-140">You can drag existing actions into the **IF YES** and **IF NO** paths.</span></span>

5. <span data-ttu-id="da0ff-141">İşiniz bittiğinde, mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="da0ff-141">When you're done, save your logic app.</span></span>

<span data-ttu-id="da0ff-142">Şimdi yalnızca gönderileri koşulunuz karşıladığında e-postaları alın.</span><span class="sxs-lookup"><span data-stu-id="da0ff-142">Now you get emails only when the posts meet your condition.</span></span>

## <a name="repeat-actions-over-a-list-with-foreach"></a><span data-ttu-id="da0ff-143">Eylemler forEach ile bir liste üzerinden yineleme</span><span class="sxs-lookup"><span data-stu-id="da0ff-143">Repeat actions over a list with forEach</span></span>

<span data-ttu-id="da0ff-144">ForEach döngüsü üzerinden bir eylem yinelenecek dizisini belirtir.</span><span class="sxs-lookup"><span data-stu-id="da0ff-144">The forEach loop specifies an array to repeat an action over.</span></span> <span data-ttu-id="da0ff-145">Bir dizi değil akış başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="da0ff-145">If it is not an array, the flow fails.</span></span> <span data-ttu-id="da0ff-146">Örneğin, bir dizi iletileri çıkarır action1 varsa ve her ileti göndermek istediğiniz eyleminizi özelliklerinde bu forEach deyimi içerebilir:`forEach : "@action('action1').outputs.messages"`</span><span class="sxs-lookup"><span data-stu-id="da0ff-146">For example, if you have action1 that outputs an array of messages, and you want to send each message, you can include this forEach statement in the properties of your action: `forEach : "@action('action1').outputs.messages"`</span></span>

## <a name="edit-the-code-definition-for-a-logic-app"></a><span data-ttu-id="da0ff-147">Bir mantıksal uygulama kodu tanımını düzenleme</span><span class="sxs-lookup"><span data-stu-id="da0ff-147">Edit the code definition for a logic app</span></span>

<span data-ttu-id="da0ff-148">Mantıksal Uygulama Tasarımcısı'nı sahip olsa da, bir mantıksal uygulama tanımlayan kodu doğrudan düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da0ff-148">Although you have the Logic App Designer, you can directly edit the code that defines a logic app.</span></span>

1. <span data-ttu-id="da0ff-149">Komut çubuğunda seçin **kod görünümü**.</span><span class="sxs-lookup"><span data-stu-id="da0ff-149">On the command bar, choose **Code view**.</span></span>

    <span data-ttu-id="da0ff-150">Bir tam Düzenleyicisi'ni açar ve düzenlediğiniz tanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="da0ff-150">A full editor opens and shows the definition you edited.</span></span>

    ![Kod Görünümü](media/logic-apps-use-logic-app-features/codeview.png)

    <span data-ttu-id="da0ff-152">Metin Düzenleyicisi'nde kopyalayın ve aynı mantıksal uygulama içinde veya arasında mantıksal uygulamalar eylemleri herhangi bir sayıda yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="da0ff-152">In the text editor, you can copy and paste any number of actions within the same logic app or between logic apps.</span></span> 
    <span data-ttu-id="da0ff-153">Ayrıca kolayca eklemenize veya tüm bölümleri tanımından kaldırın ve ayrıca tanımları başkalarıyla paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da0ff-153">You can also easily add or remove entire sections from the definition, and you can also share definitions with others.</span></span>

2. <span data-ttu-id="da0ff-154">Yaptığınız düzenlemeleri kaydetmek üzere seçim yapın **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="da0ff-154">To save your edits, choose **Save**.</span></span>

## <a name="parameters"></a><span data-ttu-id="da0ff-155">Parametreler</span><span class="sxs-lookup"><span data-stu-id="da0ff-155">Parameters</span></span>

<span data-ttu-id="da0ff-156">Bazı Logic Apps özellikleri yalnızca kod görünümünde, örneğin, parametreleri sağlanır.</span><span class="sxs-lookup"><span data-stu-id="da0ff-156">Some Logic Apps capabilities are available only in code view, for example, parameters.</span></span> <span data-ttu-id="da0ff-157">Parametre değerleri mantıksal uygulamanızı boyunca yeniden kolay hale getirir.</span><span class="sxs-lookup"><span data-stu-id="da0ff-157">Parameters make it easy to reuse values throughout your logic app.</span></span> <span data-ttu-id="da0ff-158">Örneğin, çeşitli eylemler kullanmak istediğiniz bir e-posta adresi varsa, bu e-posta adresi parametre olarak tanımlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="da0ff-158">For example, if you have an email address that you want use in several actions, you should define that email address as a parameter.</span></span>

<span data-ttu-id="da0ff-159">Çok değişmesi olasılığı olan değerler çekmek için iyi parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="da0ff-159">Parameters are good for pulling out values that you are likely to change a lot.</span></span> <span data-ttu-id="da0ff-160">Bunlar, özellikle farklı ortamlarda parametreleri geçersiz kılmak gerektiğinde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="da0ff-160">They are especially useful when you need to override parameters in different environments.</span></span> <span data-ttu-id="da0ff-161">Ortamına bağlı parametreleri geçersiz kılmak öğrenmek için bkz: [Yazar mantıksal uygulama tanımları](../logic-apps/logic-apps-author-definitions.md) ve [REST API belgeleri](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="da0ff-161">To learn how to override parameters based on environment, see [Author logic app definitions](../logic-apps/logic-apps-author-definitions.md) and [REST API documentation](https://docs.microsoft.com/rest/api/logic).</span></span>

<span data-ttu-id="da0ff-162">Bu örnek için sorgu Terime parametreleri kullanabilmesi için var olan mantıksal uygulamanızı güncelleştirme gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="da0ff-162">This example shows how to update your existing logic app so that you can use parameters for the query term.</span></span>

1. <span data-ttu-id="da0ff-163">Kod görünümünde Bul `parameters : {}` nesne ve ekleme bir `currentFeedUrl` nesnesi:</span><span class="sxs-lookup"><span data-stu-id="da0ff-163">In code view, find the `parameters : {}` object, and add a `currentFeedUrl` object:</span></span>

        "currentFeedUrl" : {
            "type" : "string",
            "defaultValue" : "http://rss.cnn.com/rss/cnn_topstories.rss"
        }

2. <span data-ttu-id="da0ff-164">Git `When_a_feed-item_is_published` eylemi bulma `queries` bölümünde ve sorgu değerle değiştirin:`"feedUrl": "#@{parameters('currentFeedUrl')}"`</span><span class="sxs-lookup"><span data-stu-id="da0ff-164">Go to the `When_a_feed-item_is_published` action, find the `queries` section, and replace the query value with : `"feedUrl": "#@{parameters('currentFeedUrl')}"`</span></span> 

    <span data-ttu-id="da0ff-165">İki veya daha fazla katılmak için de kullanabilirsiniz `concat` işlevi.</span><span class="sxs-lookup"><span data-stu-id="da0ff-165">To join two or more strings, you can also use the `concat` function.</span></span> 
    <span data-ttu-id="da0ff-166">Örneğin, `"@concat('#',parameters('currentFeedUrl'))"` yukarıdaki gibi aynı şekilde çalışır.</span><span class="sxs-lookup"><span data-stu-id="da0ff-166">For example, `"@concat('#',parameters('currentFeedUrl'))"` works the same as the above.</span></span>

3.  <span data-ttu-id="da0ff-167">İşiniz bittiğinde seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="da0ff-167">When you're done, choose **Save**.</span></span> 

    <span data-ttu-id="da0ff-168">Web sitesinin RSS yoluyla farklı bir URL geçirerek akışı değiştirebileceğiniz artık `currentFeedURL` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="da0ff-168">Now you can change the website's RSS feed by passing a different URL through the `currentFeedURL` object.</span></span>

<span data-ttu-id="da0ff-169">Daha fazla bilgi edinmek [mantıksal uygulama tanımları yazma nasıl](../logic-apps/logic-apps-author-definitions.md).</span><span class="sxs-lookup"><span data-stu-id="da0ff-169">Learn more about [how to author logic app definitions](../logic-apps/logic-apps-author-definitions.md).</span></span>

## <a name="start-logic-app-workflows"></a><span data-ttu-id="da0ff-170">Mantıksal uygulama iş akışlarını başlatmak</span><span class="sxs-lookup"><span data-stu-id="da0ff-170">Start logic app workflows</span></span>

<span data-ttu-id="da0ff-171">Mantıksal uygulamanızı tanımlanan iş akışı başlatma için farklı seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="da0ff-171">You have different options for starting the workflow defined in your logic app.</span></span> <span data-ttu-id="da0ff-172">Bir iş akışı isteğe bağlı her zaman başlayabilmeniz için [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="da0ff-172">You can always start a workflow on-demand in the [Azure portal].</span></span>

### <a name="recurrence-triggers"></a><span data-ttu-id="da0ff-173">Yineleme Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="da0ff-173">Recurrence triggers</span></span>

<span data-ttu-id="da0ff-174">Bir yineleme tetikleyici, belirttiğiniz bir zaman aralığında çalışır.</span><span class="sxs-lookup"><span data-stu-id="da0ff-174">A recurrence trigger runs at an interval that you specify.</span></span> <span data-ttu-id="da0ff-175">Tetikleyici koşullu mantık olduğunda, tetikleyici iş akışını çalıştırmak gerekip gerekmediğini belirler.</span><span class="sxs-lookup"><span data-stu-id="da0ff-175">When the trigger has conditional logic, the trigger determines whether the workflow needs to run.</span></span> <span data-ttu-id="da0ff-176">İş akışı döndürerek çalışmalı tetikleyici gösteren bir `200` durum kodu.</span><span class="sxs-lookup"><span data-stu-id="da0ff-176">A trigger indicates the workflow should run by returning a `200` status code.</span></span> <span data-ttu-id="da0ff-177">İş akışını çalıştırmak gerekmez, tetikleyici döndürür bir `202` durum kodu.</span><span class="sxs-lookup"><span data-stu-id="da0ff-177">When the workflow doesn't need to run, the trigger returns a `202` status code.</span></span>

### <a name="callback-using-rest-apis"></a><span data-ttu-id="da0ff-178">REST API'lerini kullanarak geri çağırma</span><span class="sxs-lookup"><span data-stu-id="da0ff-178">Callback using REST APIs</span></span>

<span data-ttu-id="da0ff-179">Bir iş akışını başlatmak için Hizmetler bir mantıksal uygulama uç noktası çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da0ff-179">To start a workflow, services can call a logic app endpoint.</span></span> <span data-ttu-id="da0ff-180">Bu tür bir mantıksal uygulama isteğe bağlı başlatmayı seçin **Şimdi Çalıştır** komut çubuğunda.</span><span class="sxs-lookup"><span data-stu-id="da0ff-180">To start this kind of logic app on-demand, choose **Run now** on the command bar.</span></span> <span data-ttu-id="da0ff-181">Bkz: [Tetikleyiciler olarak uygulama uç noktaları mantığı çağırarak iş akışlarını başlatmak](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="da0ff-181">See [Start workflows by calling logic app endpoints as triggers](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<!-- Shared links -->
<span data-ttu-id="da0ff-182">[Azure portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="da0ff-182">[Azure portal]: https://portal.azure.com</span></span>

## <a name="next-steps"></a><span data-ttu-id="da0ff-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="da0ff-183">Next steps</span></span>

* [<span data-ttu-id="da0ff-184">Switch deyimleri</span><span class="sxs-lookup"><span data-stu-id="da0ff-184">Switch statements</span></span>](../logic-apps/logic-apps-switch-case.md) 
* [<span data-ttu-id="da0ff-185">Döngüler, kapsamlar ve ayırma</span><span class="sxs-lookup"><span data-stu-id="da0ff-185">Loops, scopes, and debatching</span></span>](../logic-apps/logic-apps-loops-and-scopes.md)
* [<span data-ttu-id="da0ff-186">Mantıksal uygulama tanımları yazma</span><span class="sxs-lookup"><span data-stu-id="da0ff-186">Author logic app definitions</span></span>](../logic-apps/logic-apps-author-definitions.md)