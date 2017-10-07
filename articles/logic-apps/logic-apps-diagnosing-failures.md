---
title: "aaaDiagnose hataları - Azure Logic Apps | Microsoft Docs"
description: "Ortak yolları toounderstand logic apps nerede başarısız oluyor"
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
ms.openlocfilehash: 46d318625820034c95e6df3a71ab84c58f076dd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-logic-app-failures"></a><span data-ttu-id="f80e9-103">Mantıksal uygulama hatalarını tanılama</span><span class="sxs-lookup"><span data-stu-id="f80e9-103">Diagnose logic app failures</span></span>
<span data-ttu-id="f80e9-104">Sorunları veya hatalar logic apps ile karşılaşırsanız, var olan birkaç yaklaşımlar burada hello hataları'ten gelen daha iyi anlamanıza yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f80e9-104">If you experience issues or failures with your logic apps, there are a few approaches can help you better understand where hello failures are coming from.</span></span>  

## <a name="azure-portal-tools"></a><span data-ttu-id="f80e9-105">Azure portal araçları</span><span class="sxs-lookup"><span data-stu-id="f80e9-105">Azure portal tools</span></span>
<span data-ttu-id="f80e9-106">Hello Azure portal birçok araçları toodiagnose her mantıksal uygulama her adımında sağlar.</span><span class="sxs-lookup"><span data-stu-id="f80e9-106">hello Azure portal provides many tools toodiagnose each logic app at each step.</span></span>

### <a name="trigger-history"></a><span data-ttu-id="f80e9-107">Tetikleyici geçmişi</span><span class="sxs-lookup"><span data-stu-id="f80e9-107">Trigger history</span></span>

<span data-ttu-id="f80e9-108">Her mantıksal uygulama en az bir tetikleyici sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f80e9-108">Each logic app has at least one trigger.</span></span> <span data-ttu-id="f80e9-109">Uygulamaları tetikleme olmayan fark ederseniz hello tetikleyici geçmişi daha fazla bilgi için ilk arayın.</span><span class="sxs-lookup"><span data-stu-id="f80e9-109">If you notice that apps aren't firing, look first at hello trigger history for more information.</span></span> <span data-ttu-id="f80e9-110">Merhaba mantığı app'ss ana dikey penceresinde hello tetikleyici geçmişi erişebilir.</span><span class="sxs-lookup"><span data-stu-id="f80e9-110">You can access hello trigger history on hello logic app'ss main blade.</span></span>

![Merhaba tetikleyici geçmişi bulma][1]

<span data-ttu-id="f80e9-112">Merhaba tetikleyici geçmişi mantıksal uygulamanızı yapılan tüm tetikleyici girişimleri listeler.</span><span class="sxs-lookup"><span data-stu-id="f80e9-112">hello trigger history lists all trigger attempts that your logic app made.</span></span> <span data-ttu-id="f80e9-113">Merhaba ayrıntılara, özellikle her tetikleyici girişimi toodrill tıklatabilirsiniz, herhangi bir girdi veya tetikleyici girişimi hello çıkışları oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="f80e9-113">You can click each trigger attempt toodrill into hello details, specifically, any inputs or outputs that hello trigger attempt generated.</span></span> <span data-ttu-id="f80e9-114">Başarısız Tetikleyicileri bulursanız, hello tetikleyici girişimi seçip hello **çıkışları** oluşturulan tüm hata iletilerini, örneğin, geçerli olmayan FTP için kimlik bilgilerini tooreview bağlantı.</span><span class="sxs-lookup"><span data-stu-id="f80e9-114">If you find failed triggers, select hello trigger attempt and choose hello **Outputs** link tooreview any generated error messages, for example, for FTP credentials that aren't valid.</span></span>

<span data-ttu-id="f80e9-115">Merhaba farklı durumlarını görebilirsiniz şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f80e9-115">hello different statuses you might see are:</span></span>

* <span data-ttu-id="f80e9-116">**Atlanan**.</span><span class="sxs-lookup"><span data-stu-id="f80e9-116">**Skipped**.</span></span> <span data-ttu-id="f80e9-117">Merhaba uç noktası sorgulu toocheck verileri için olan ve hiçbir veri yoktu bir yanıt aldı.</span><span class="sxs-lookup"><span data-stu-id="f80e9-117">hello endpoint was polled toocheck for data and received a response that no data was available.</span></span>
* <span data-ttu-id="f80e9-118">**Başarılı bir şekilde**.</span><span class="sxs-lookup"><span data-stu-id="f80e9-118">**Succeeded**.</span></span> <span data-ttu-id="f80e9-119">Merhaba tetikleyici verileri kullanılabilir bir yanıt aldı.</span><span class="sxs-lookup"><span data-stu-id="f80e9-119">hello trigger received a response that data was available.</span></span> <span data-ttu-id="f80e9-120">Bu durum, el ile bir tetikleyici, yineleme tetikleyici ya da bir yoklama tetikleyici neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f80e9-120">This status might result from a manual trigger, a recurrence trigger, or a polling trigger.</span></span> <span data-ttu-id="f80e9-121">Bu durum genellikle tarafından hello eşlik **Fired** durumu, bir koşul veya SplitOn komutu memnun değildi kod görünümünde olup olmadığını olmayabilir ancak.</span><span class="sxs-lookup"><span data-stu-id="f80e9-121">This status is usually accompanied by hello **Fired** status, but might not be if you have a condition or SplitOn command in code view that wasn't satisfied.</span></span>
* <span data-ttu-id="f80e9-122">**Başarısız**.</span><span class="sxs-lookup"><span data-stu-id="f80e9-122">**Failed**.</span></span> <span data-ttu-id="f80e9-123">Bir hata oluştu.</span><span class="sxs-lookup"><span data-stu-id="f80e9-123">An error was generated.</span></span>

#### <a name="start-a-trigger-manually"></a><span data-ttu-id="f80e9-124">Bir tetikleyici el ile başlatın</span><span class="sxs-lookup"><span data-stu-id="f80e9-124">Start a trigger manually</span></span>

<span data-ttu-id="f80e9-125">Kullanılabilir bir tetikleyicinin hemen hello sonraki yinelemesi beklemeden hello mantığı uygulama toocheck istiyorsanız, **Tetik Seç** hello ana dikey tooforce onay üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f80e9-125">If you want hello logic app toocheck for an available trigger immediately without waiting for hello next recurrence, click **Select Trigger** on hello main blade tooforce a check.</span></span> <span data-ttu-id="f80e9-126">Örneğin, Dropbox tetikleyiciyle bu bağlantıyı tıklatarak yeni dosyalarda hello iş akışı tooimmediately yoklama Dropbox neden olur.</span><span class="sxs-lookup"><span data-stu-id="f80e9-126">For example, clicking this link with a Dropbox trigger causes hello workflow tooimmediately poll Dropbox for new files.</span></span>

### <a name="run-history"></a><span data-ttu-id="f80e9-127">çalıştırma geçmişi</span><span class="sxs-lookup"><span data-stu-id="f80e9-127">Run history</span></span>

<span data-ttu-id="f80e9-128">Her Mazotlu tetikleyici çalıştırılmasıyla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="f80e9-128">Every fired trigger results in a run.</span></span> <span data-ttu-id="f80e9-129">Merhaba iş akışı sırasında neler olduğunu anlamanıza yardımcı olabilecek birçok ayrıntılarını içeren hello ana dikey penceresinden çalışma bilgilere erişebilir.</span><span class="sxs-lookup"><span data-stu-id="f80e9-129">You can access run information from hello main blade, which contains many details that can help you understand what happened during hello workflow.</span></span>

![Merhaba çalıştırma geçmişi bulma][2]

<span data-ttu-id="f80e9-131">Bir çalışma durumlarını izleyen hello birini görüntüler:</span><span class="sxs-lookup"><span data-stu-id="f80e9-131">A run displays one of hello following statuses:</span></span>

* <span data-ttu-id="f80e9-132">**Başarılı bir şekilde**.</span><span class="sxs-lookup"><span data-stu-id="f80e9-132">**Succeeded**.</span></span> <span data-ttu-id="f80e9-133">Tüm eylemleri başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="f80e9-133">All actions succeeded.</span></span> <span data-ttu-id="f80e9-134">Bir hata oluştu, bu hata oluştu. daha sonra hello iş akışında bir eylem tarafından işlendi.</span><span class="sxs-lookup"><span data-stu-id="f80e9-134">If a failure happened, that failure was handled by an action that occurred later in hello workflow.</span></span> <span data-ttu-id="f80e9-135">Diğer bir deyişle, hello hatası toorun başarısız eylemden sonra ayarlanmış bir eylem yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="f80e9-135">That is, hello failure was handled by an action that was set toorun after a failed action.</span></span>
* <span data-ttu-id="f80e9-136">**Başarısız**.</span><span class="sxs-lookup"><span data-stu-id="f80e9-136">**Failed**.</span></span> <span data-ttu-id="f80e9-137">En az bir eylemin hello iş akışı daha sonra bir eylemi tarafından işlenmedi bir hata vardı.</span><span class="sxs-lookup"><span data-stu-id="f80e9-137">At least one action had a failure that was not handled by an action later in hello workflow.</span></span>
* <span data-ttu-id="f80e9-138">**İptal**.</span><span class="sxs-lookup"><span data-stu-id="f80e9-138">**Cancelled**.</span></span> <span data-ttu-id="f80e9-139">Merhaba iş akışının çalıştığı ancak iptal isteği aldı.</span><span class="sxs-lookup"><span data-stu-id="f80e9-139">hello workflow was running but received a cancel request.</span></span>
* <span data-ttu-id="f80e9-140">**Çalışan**.</span><span class="sxs-lookup"><span data-stu-id="f80e9-140">**Running**.</span></span> <span data-ttu-id="f80e9-141">Merhaba iş akışı şu anda çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="f80e9-141">hello workflow is currently running.</span></span> <span data-ttu-id="f80e9-142">Bu durum, daraltılmış iş akışları için ya da hello planı fiyatlandırma geçerli nedeniyle oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="f80e9-142">This status might occur for throttled workflows, or because of hello current pricing plan.</span></span> <span data-ttu-id="f80e9-143">Ayrıntılar için bkz [fiyatlandırma sayfası hello eylem sınırları](https://azure.microsoft.com/pricing/details/app-service/plans/).</span><span class="sxs-lookup"><span data-stu-id="f80e9-143">For details, see [action limits on hello pricing page](https://azure.microsoft.com/pricing/details/app-service/plans/).</span></span> <span data-ttu-id="f80e9-144">Tanılama (çalıştırma geçmişi hello altında görünür hello grafikleri) yapılandırma gerçekleşecek herhangi bir kısıtlama olayı hakkında bilgi de sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f80e9-144">Configuring diagnostics (hello charts that appear under hello run history) also can provide information about any throttle events that happen.</span></span>

<span data-ttu-id="f80e9-145">Çalışma geçmişinize bakıldığında, daha fazla ayrıntı için ayrıntıya inebilir.</span><span class="sxs-lookup"><span data-stu-id="f80e9-145">When you are looking at a run history, you can drill in for more details.</span></span>  

#### <a name="trigger-outputs"></a><span data-ttu-id="f80e9-146">Tetikleyici çıkarır</span><span class="sxs-lookup"><span data-stu-id="f80e9-146">Trigger outputs</span></span>

<span data-ttu-id="f80e9-147">Tetikleyici hello tetikleyiciyle gelen hello verileri göster çıkarır.</span><span class="sxs-lookup"><span data-stu-id="f80e9-147">Trigger outputs show hello data that came from hello trigger.</span></span> <span data-ttu-id="f80e9-148">Bu çıktılar tüm özellikleri beklendiği gibi döndürülen olup olmadığını belirlemenize yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f80e9-148">These outputs can help you determine whether all properties returned as expected.</span></span>

> [!NOTE]
> <span data-ttu-id="f80e9-149">Anlamadığınız herhangi bir içerik görürseniz, nasıl Azure Logic Apps öğrenin [farklı içerik türlerini işleme](../logic-apps/logic-apps-content-type.md).</span><span class="sxs-lookup"><span data-stu-id="f80e9-149">If you see any content that you don't understand, learn how Azure Logic Apps [handles different content types](../logic-apps/logic-apps-content-type.md).</span></span>
> 

![Tetikleyici çıkışı örnekleri][3]

#### <a name="action-inputs-and-outputs"></a><span data-ttu-id="f80e9-151">Eylem girişleri ve çıkışları</span><span class="sxs-lookup"><span data-stu-id="f80e9-151">Action inputs and outputs</span></span>

<span data-ttu-id="f80e9-152">Merhaba giriş ve bir eylem alınan çıkış inebilir.</span><span class="sxs-lookup"><span data-stu-id="f80e9-152">You can drill into hello inputs and outputs that an action received.</span></span> <span data-ttu-id="f80e9-153">Bu verilerin hello boyutu ve şekli ilgili hello çıktıların anlamak için ve ayrıca oluşturulmuş olabilir herhangi bir hata iletisi bulmak için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="f80e9-153">This data is useful for understanding hello size and shape of hello outputs, and also for finding any error messages that might have been generated.</span></span>

![Eylem girişleri ve çıkışları][4]

## <a name="debug-workflow-runtime"></a><span data-ttu-id="f80e9-155">İş akışı çalışma zamanı hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="f80e9-155">Debug workflow runtime</span></span>

<span data-ttu-id="f80e9-156">Hello girişleri, çıkış ve bir çalışma Tetikleyicileri izleme ile birlikte hata ayıklamaya yardımcı bazı adımları tooa iş akışı ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f80e9-156">Along with monitoring hello inputs, outputs, and triggers of a run, you could add some steps tooa workflow that help with debugging.</span></span> 
<span data-ttu-id="f80e9-157">[RequestBin](http://requestb.in) bir iş akışında bir adım olarak ekleyebileceğiniz güçlü bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="f80e9-157">[RequestBin](http://requestb.in) is a powerful tool that you can add as a step in a workflow.</span></span> <span data-ttu-id="f80e9-158">RequestBin kullanarak, bir HTTP isteği denetçisi toodetermine hello tam boyutunu, Şekil ve bir HTTP istek biçimini ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f80e9-158">By using RequestBin, you can set up an HTTP request inspector toodetermine hello exact size, shape, and format of an HTTP request.</span></span> <span data-ttu-id="f80e9-159">Bir RequestBin oluşturun ve bir mantıksal uygulama HTTP POST eylemiyle tootest, örneğin istediğiniz gövdesi içeriği, bir ifade veya başka bir adım çıkış hello URL yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="f80e9-159">You can create a RequestBin and paste hello URL in a logic app HTTP POST action with body content that you want tootest, for example, an expression or another step output.</span></span> <span data-ttu-id="f80e9-160">Merhaba mantıksal uygulama çalıştırmak sonra hello isteği hello Logic Apps altyapısı, oluşturulan zaman nasıl oluşturulduğu, RequestBin toosee yenileyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f80e9-160">After you run hello logic app, you can refresh your RequestBin toosee how hello request was formed when generated from hello Logic Apps engine.</span></span>

<!-- image references -->
[1]: ./media/logic-apps-diagnosing-failures/triggerhistory.png
[2]: ./media/logic-apps-diagnosing-failures/runhistory.png
[3]: ./media/logic-apps-diagnosing-failures/triggeroutputslink.png
[4]: ./media/logic-apps-diagnosing-failures/actionoutputs.png
