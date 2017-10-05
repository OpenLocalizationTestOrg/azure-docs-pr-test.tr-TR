---
title: "Hataları - Azure Logic Apps tanılama | Microsoft Docs"
description: "Logic apps nerede başarısız olduğunu anlamak için yaygın yolları"
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: a6727ebd-39bd-4298-9e68-2ae98738576e
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: 814e6f93088cdd96b0a663d2a7494b5a11470d99
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="f9bd5-103">Mantıksal uygulama hatalarını tanılama</span><span class="sxs-lookup"><span data-stu-id="f9bd5-103">Diagnose logic app failures</span></span>
<span data-ttu-id="f9bd5-104">Sorunları veya hatalar logic apps ile karşılaşırsanız, var olan birkaç yaklaşımlar burada hataları'ten gelen daha iyi anlamanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where the failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="f9bd5-105">Azure portal araçları</span><span class="sxs-lookup"><span data-stu-id="f9bd5-105">Azure portal tools</span></span>
<span data-ttu-id="f9bd5-106">Azure portalında her mantıksal uygulama her adımında tanılamak için birçok araçlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-106">The Azure portal provides many tools to diagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="f9bd5-107">Tetikleyici geçmişi</span><span class="sxs-lookup"><span data-stu-id="f9bd5-107">Trigger history</span></span>

<span data-ttu-id="f9bd5-108">Her mantıksal uygulama en az bir tetikleyici sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="f9bd5-109">Uygulamaları tetikleme olmayan fark ederseniz, tetikleyici geçmişi daha fazla bilgi için ilk arayın.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-109">If you notice that apps aren't firing, look first at the trigger history for more information.</span></span> <span data-ttu-id="f9bd5-110">Tetikleyici geçmişi mantığı app'ss ana dikey penceresinde erişebilir.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-110">You can access the trigger history on the logic app'ss main blade.</span></span>

![Tetikleyici geçmişi bulma][1]

<span data-ttu-id="f9bd5-112">Tetikleyici geçmişi mantıksal uygulamanızı yapılan tüm tetikleyici girişimleri listeler.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-112">The trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="f9bd5-113">Ayrıntılara, özellikle incelemek için her bir tetikleyici denemesi, tüm girişleri veya tetikleyici girişimi oluşturulan çıkışları tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-113">You can click each trigger attempt to drill into the details, specifically, any inputs or outputs that the trigger attempt generated.</span></span> <span data-ttu-id="f9bd5-114">Başarısız Tetikleyicileri bulursanız, tetikleyici girişimi seçip **çıkışları** gözden için bağlantı oluşturulan hata iletileri, örneğin, geçerli olmayan FTP kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-114">If you find failed triggers, select the trigger attempt and choose the **Outputs** link to review any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="f9bd5-115">Görebilirsiniz farklı durumlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f9bd5-115">The different statuses you might see are:</span></span>

* <span data-ttu-id="f9bd5-116">**Atlanan**.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-116">**Skipped**.</span></span> <span data-ttu-id="f9bd5-117">Uç nokta verileri denetlemek için sorgulanan ve hiçbir veri yoktu bir yanıt aldı.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-117">The endpoint was polled to check for data and received a response that no data was available.</span></span>
* <span data-ttu-id="f9bd5-118">**Başarılı bir şekilde**.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-118">**Succeeded**.</span></span> <span data-ttu-id="f9bd5-119">Tetikleyici verileri kullanılabilir bir yanıt aldı.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-119">The trigger received a response that data was available.</span></span> <span data-ttu-id="f9bd5-120">Bu durum, el ile bir tetikleyici, yineleme tetikleyici ya da bir yoklama tetikleyici neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="f9bd5-121">Bu durum genellikle tarafından eşlik **Fired** durumu, bir koşul veya SplitOn komutu memnun değildi kod görünümünde olup olmadığını olmayabilir ancak.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-121">This status is usually accompanied by the **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="f9bd5-122">**Başarısız**.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-122">**Failed**.</span></span> <span data-ttu-id="f9bd5-123">Bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="f9bd5-124">Bir tetikleyici el ile başlatın</span><span class="sxs-lookup"><span data-stu-id="f9bd5-124">Start a trigger manually</span></span>

<span data-ttu-id="f9bd5-125">Hemen bir sonraki tekrarı beklemeden kullanılabilir bir tetikleyici denetlemek için mantıksal uygulama istiyorsanız, **Tetik Seç** onay zorlamak için ana dikey penceresinde.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-125">If you want the logic app to check for an available trigger immediately without waiting for the next recurrence, click **Select Trigger** on the main blade to force a check.</span></span> <span data-ttu-id="f9bd5-126">Örneğin, Dropbox tetikleyiciyle bu bağlantıya tıkladıklarında, Dropbox yeni dosyaları hemen yoklamak iş akışı neden olur.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-126">For example, clicking this link with a Dropbox trigger causes the workflow to immediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="f9bd5-127">çalıştırma geçmişi</span><span class="sxs-lookup"><span data-stu-id="f9bd5-127">Run history</span></span>

<span data-ttu-id="f9bd5-128">Her Mazotlu tetikleyici çalıştırılmasıyla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="f9bd5-129">İş akışı sırasında neler olduğunu anlamanıza yardımcı olabilecek birçok ayrıntılarını içeren ana dikey penceresinden çalışma bilgilere erişebilir.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-129">You can access run information from the main blade, which contains many details that can help you understand what happened during the workflow.</span></span>

![Çalıştırma geçmişi bulma][2]

<span data-ttu-id="f9bd5-131">Bir farklı çalıştır aşağıdaki durumlardan birini görüntüler:</span><span class="sxs-lookup"><span data-stu-id="f9bd5-131">A run displays one of the following statuses:</span></span>

* <span data-ttu-id="f9bd5-132">**Başarılı bir şekilde**.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-132">**Succeeded**.</span></span> <span data-ttu-id="f9bd5-133">Tüm eylemleri başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-133">All actions succeeded.</span></span> <span data-ttu-id="f9bd5-134">Bir hata oluştu, bu hata oluştu. daha sonra iş akışında bir eylem tarafından işlendi.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-134">If a failure happened, that failure was handled by an action that occurred later in the workflow.</span></span> <span data-ttu-id="f9bd5-135">Diğer bir deyişle, hata, başarısız bir eylemden sonra çalışacak şekilde ayarlanmış bir eylem tarafından işlendi.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-135">That is, the failure was handled by an action that was set to run after a failed action.</span></span>
* <span data-ttu-id="f9bd5-136">**Başarısız**.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-136">**Failed**.</span></span> <span data-ttu-id="f9bd5-137">En az bir eylemin daha sonra iş akışında bir eylem tarafından işlenmedi bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-137">At least one action had a failure that was not handled by an action later in the workflow.</span></span>
* <span data-ttu-id="f9bd5-138">**İptal**.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-138">**Cancelled**.</span></span> <span data-ttu-id="f9bd5-139">İş akışının çalıştığı ancak iptal isteği aldı.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-139">The workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="f9bd5-140">**Çalışan**.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-140">**Running**.</span></span> <span data-ttu-id="f9bd5-141">İş akışı şu anda çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-141">The workflow is currently running.</span></span> <span data-ttu-id="f9bd5-142">Bu durum, daraltılmış iş akışları için ya da geçerli fiyatlandırma planı nedeniyle oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-142">This status might occur for throttled workflows, or because of the current pricing plan.</span></span> <span data-ttu-id="f9bd5-143">Ayrıntılar için bkz [eylem sınırları Fiyatlandırma sayfasında](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="f9bd5-143">For details, see [action limits on the pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="f9bd5-144">Tanılama (çalıştırma geçmişi altında görüntülenen grafiklerin) yapılandırma gerçekleşecek herhangi bir kısıtlama olayı hakkında bilgi de sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-144">Configuring diagnostics (the charts that appear under the run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="f9bd5-145">Çalışma geçmişinize bakıldığında, daha fazla ayrıntı için ayrıntıya inebilir.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="f9bd5-146">Tetikleyici çıkarır</span><span class="sxs-lookup"><span data-stu-id="f9bd5-146">Trigger outputs</span></span>

<span data-ttu-id="f9bd5-147">Tetikleyici çıkışları tetikleyiciyle gelen verileri görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-147">Trigger outputs show the data that came from the trigger.</span></span> <span data-ttu-id="f9bd5-148">Bu çıktılar tüm özellikleri beklendiği gibi döndürülen olup olmadığını belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="f9bd5-149">Anlamadığınız herhangi bir içerik görürseniz, nasıl Azure Logic Apps öğrenin [farklı içerik türlerini işleme](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="f9bd5-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Tetikleyici çıkışı örnekleri][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="f9bd5-151">Eylem girişleri ve çıkışları</span><span class="sxs-lookup"><span data-stu-id="f9bd5-151">Action inputs and outputs</span></span>

<span data-ttu-id="f9bd5-152">Giriş ve bir eylem alınan çıkış inebilir.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-152">You can drill into the inputs and outputs that an action received.</span></span> <span data-ttu-id="f9bd5-153">Bu verilerin boyutunu ve çıkışları şeklini anlamak için ve ayrıca oluşturulmuş olabilir herhangi bir hata iletisi bulmak için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-153">This data is useful for understanding the size and shape of the outputs, and also for finding any error messages that might have been generated.</span></span>

![Eylem girişleri ve çıkışları][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="f9bd5-155">İş akışı çalışma zamanı hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="f9bd5-155">Debug workflow runtime</span></span>

<span data-ttu-id="f9bd5-156">Giriş, çıkış ve Tetikleyicileri bir çalışma izleme ile birlikte hata ayıklamaya yardımcı bir iş akışı için bazı adımlar ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-156">Along with monitoring the inputs, outputs, and triggers of a run, you could add some steps to a workflow that help with debugging.</span></span> 
<span data-ttu-id="f9bd5-157">[RequestBin](http://requestb.in) bir iş akışında bir adım olarak ekleyebileceğiniz güçlü bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="f9bd5-158">RequestBin kullanarak tam boyutunu, Şekil ve bir HTTP istek biçimini belirlemek için HTTP isteği Inspector ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-158">By using RequestBin, you can set up an HTTP request inspector to determine the exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="f9bd5-159">Bir RequestBin oluşturun ve bir mantıksal uygulama HTTP POST eylemiyle, örneğin test etmek istediğiniz gövde içerik, ifade veya başka bir adım çıkış URL'sini yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-159">You can create a RequestBin and paste the URL in a logic app HTTP POST action with body content that you want to test, for example, an expression or another step output.</span></span> <span data-ttu-id="f9bd5-160">Mantıksal uygulama çalıştırın sonra isteği Logic Apps altyapısı oluşturulan zaman nasıl oluşturulduğu görmek için RequestBin yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9bd5-160">After you run the logic app, you can refresh your RequestBin to see how the request was formed when generated from the Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
