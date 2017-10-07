---
title: "bir grubun veya koleksiyonun - Azure mantıksal uygulamaları olarak aaaBatch işlem iletilerinin | Microsoft Docs"
description: "Toplu işleme logic apps içinde ileti gönderme ve alma"
keywords: "Batch, toplu işlem"
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="a1d3f-104">Gönderme, alma ve logic apps işlem iletileri toplu</span><span class="sxs-lookup"><span data-stu-id="a1d3f-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="a1d3f-105">tooprocess iletileri gruplarında birlikte, veri öğeleri ya da iletileri tooa gönderebilir *toplu*ve ardından bu öğeleri toplu iş olarak işlem.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-105">tooprocess messages together in groups, you can send data items, or messages, tooa *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="a1d3f-106">Bu yaklaşım, toomake emin veri öğelerini birlikte işlenir ve belirli bir şekilde gruplama istediğinizde yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-106">This approach is useful when you want toomake sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="a1d3f-107">Hello kullanarak toplu iş olarak öğeleri alma mantıksal uygulamalar oluşturabileceğiniz **toplu** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-107">You can create logic apps that receive items as a batch by using hello **Batch** trigger.</span></span> <span data-ttu-id="a1d3f-108">Daha sonra hello kullanarak öğeleri tooa toplu iş gönderme logic apps oluşturabilirsiniz **toplu** eylem.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-108">You can then create logic apps that send items tooa batch by using hello **Batch** action.</span></span>

<span data-ttu-id="a1d3f-109">Bu konu, bu görevleri gerçekleştirerek toplu bir çözümü nasıl oluşturabilirsiniz gösterir:</span><span class="sxs-lookup"><span data-stu-id="a1d3f-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="a1d3f-110">[Alan ve öğeleri toplu iş olarak toplayan bir mantıksal uygulama oluşturma](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="a1d3f-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="a1d3f-111">Merhaba alıcı mantıksal uygulama serbest bırakır ve öğelerini işler önce bu "toplu alıcı" mantıksal uygulama hello toplu ad ve sürüm ölçütlerini toomeet belirtir.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-111">This "batch receiver" logic app specifies hello batch name and release criteria toomeet before hello receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="a1d3f-112">[Öğeleri tooa toplu gönderen bir mantıksal uygulama oluşturma](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="a1d3f-112">[Create a logic app that sends items tooa batch](#batch-sender).</span></span> <span data-ttu-id="a1d3f-113">Bu "toplu gönderen" mantıksal uygulama yeri belirtir var olan bir toplu alıcı mantığı uygulamaya olmalıdır toosend öğeleri.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-113">This "batch sender" logic app specifies where toosend items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="a1d3f-114">Ayrıca, bir müşteri numarası gibi benzersiz bir anahtar belirtin, çok "Bölüm" veya bölmek, bu anahtarı temel alt kümeler halinde hello hedef toplu.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-114">You can also specify a unique key, like a customer number, too"partition", or divide, hello target batch into subsets based on that key.</span></span> <span data-ttu-id="a1d3f-115">Böylece, tüm öğeleri aynı anahtarla toplanan ve birlikte işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="a1d3f-116">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="a1d3f-116">Requirements</span></span>

<span data-ttu-id="a1d3f-117">toofollow Bu örnekte, bu öğeler gerekir:</span><span class="sxs-lookup"><span data-stu-id="a1d3f-117">toofollow this example, you need these items:</span></span>

* <span data-ttu-id="a1d3f-118">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-118">An Azure subscription.</span></span> <span data-ttu-id="a1d3f-119">Bir aboneliğiniz yoksa [ücretsiz bir Azure hesabı ile başlayabilirsiniz](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="a1d3f-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="a1d3f-120">Ya da [Kullandıkça Öde aboneliğine kaydolabilirsiniz](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="a1d3f-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="a1d3f-121">Hakkındaki temel bilgileri [nasıl toocreate mantıksal uygulamalar](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="a1d3f-121">Basic knowledge about [how toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="a1d3f-122">Herhangi bir e-posta hesabı [Azure mantıksal uygulamaları tarafından desteklenen e-posta sağlayıcısı](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="a1d3f-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="a1d3f-123">Toplu iş olarak iletilerini mantıksal uygulamalar oluşturma</span><span class="sxs-lookup"><span data-stu-id="a1d3f-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="a1d3f-124">İletileri tooa toplu göndermeden önce hello ile bir "toplu alıcı" mantıksal uygulama oluşturmanız gerekir **toplu** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-124">Before you can send messages tooa batch, you must first create a "batch receiver" logic app with hello **Batch** trigger.</span></span> <span data-ttu-id="a1d3f-125">Bu şekilde hello gönderen mantıksal uygulama oluşturduğunuzda, bu alıcı mantıksal uygulama seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-125">That way, you can select this receiver logic app when you create hello sender logic app.</span></span> <span data-ttu-id="a1d3f-126">Merhaba alıcısı için hello toplu işlem adı, sürüm ölçütlerini ve diğer ayarları belirtin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-126">For hello receiver, you specify hello batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="a1d3f-127">Gönderen logic apps alıcı logic apps tooknow hello Gönderenler hakkında herhangi bir şey gerekmez ancak burada toosend öğe, bilmeniz.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-127">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="a1d3f-128">Merhaba, [Azure portal](https://portal.azure.com), bu ada sahip bir mantıksal uygulama oluşturma: "BatchReceiver"</span><span class="sxs-lookup"><span data-stu-id="a1d3f-128">In hello [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="a1d3f-129">Logic Apps Tasarımcısı'nda hello eklemek **toplu** , logic app iş akışınızı başlatır tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-129">In Logic Apps Designer, add hello **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="a1d3f-130">Merhaba arama kutusuna "toplu", filtre olarak girin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-130">In hello search box, enter "batch" as your filter.</span></span> <span data-ttu-id="a1d3f-131">Bu tetikleyici seçin: **toplu – toplu iletileri**</span><span class="sxs-lookup"><span data-stu-id="a1d3f-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Toplu tetikleyicisi ekleyin](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="a1d3f-133">Merhaba toplu işlem için bir ad sağlayın ve hello toplu, örneğin serbest ölçütlerini belirtin:</span><span class="sxs-lookup"><span data-stu-id="a1d3f-133">Provide a name for hello batch, and specify criteria for releasing hello batch, for example:</span></span>

   * <span data-ttu-id="a1d3f-134">**Toplu işlemi adı**: Bu örnekte "TestBatch" olan hello kullanılan ad tooidentify hello toplu işlem.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-134">**Batch Name**: hello name used tooidentify hello batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="a1d3f-135">**İleti sayısı**: Merhaba iletileri toohold sayısı toplu iş olarak bu örnekte, "5" olan işlenmek üzere serbest bırakmadan önce.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-135">**Message Count**: hello number of messages toohold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Toplu iş tetikleyici ayrıntılarını sağlayın](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="a1d3f-137">Merhaba toplu tetikleyici başlatıldığında, bir e-posta gönderen başka bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-137">Add another action that sends an email when hello batch trigger fires.</span></span> <span data-ttu-id="a1d3f-138">Her zaman hello toplu beş öğelerine sahip, hello mantıksal uygulama bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-138">Each time hello batch has five items, hello logic app sends an email.</span></span>

   1. <span data-ttu-id="a1d3f-139">Merhaba toplu tetikleyici altında seçin **+ yeni adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-139">Under hello batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="a1d3f-140">Merhaba arama kutusuna "e-posta", filtre olarak girin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-140">In hello search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="a1d3f-141">E-posta sağlayıcınız üzerinde bağlı olarak, bir e-posta Bağlayıcısı'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="a1d3f-142">Örneğin, bir iş veya Okul hesabınız varsa, hello Office 365 Outlook bağlayıcıyı seçin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-142">For example, if you have a work or school account, select hello Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="a1d3f-143">Gmail hesabınız varsa, hello Gmail Bağlayıcısı'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-143">If you have a Gmail account, select hello Gmail connector.</span></span>

   3. <span data-ttu-id="a1d3f-144">Bu eylem, bağlayıcı için seçin:  **{*e-posta sağlayıcısı*}-bir e-posta ** Gönder</span><span class="sxs-lookup"><span data-stu-id="a1d3f-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="a1d3f-145">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="a1d3f-145">For example:</span></span>

      ![E-posta sağlayıcınız için "bir e-posta Gönder" eylemini seçin](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="a1d3f-147">E-posta sağlayıcınız için daha önce bir bağlantı oluşturmadıysanız, istendiğinde kimlik doğrulaması için e-posta kimlik bilgilerinizi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="a1d3f-148">Daha fazla bilgi edinmek [e-posta kimlik bilgilerinizi kimlik doğrulaması](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a1d3f-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="a1d3f-149">Yeni eklediğiniz hello eylemin Hello özellikleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-149">Set hello properties for hello action you just added.</span></span>

   * <span data-ttu-id="a1d3f-150">Merhaba, **için** kutusuna, hello alıcının e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-150">In hello **To** box, enter hello recipient's email address.</span></span> 
   <span data-ttu-id="a1d3f-151">Test amacıyla, kendi e-posta adresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="a1d3f-152">Merhaba, **konu** kutusunda, hello zaman **dinamik içerik** seçin hello listesi görüntülenir, **bölüm adı** alan.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-152">In hello **Subject** box, when hello **Dynamic content** list appears, select hello **Partition Name** field.</span></span>

     !["Bölüm adı" Hello "Dinamik içerik" listeden seçin](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="a1d3f-154">Bir sonraki bölümde böler hedef toplu içine mantıksal hello benzersiz bölüm anahtarı iletiler gönderebilir toowhere ayarlar belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-154">In a later section, you can specify a unique partition key that divides hello target batch into logical sets toowhere you can send messages.</span></span> 
     <span data-ttu-id="a1d3f-155">Her küme hello gönderen mantıksal uygulama tarafından oluşturulan benzersiz bir numara vardır.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-155">Each set has a unique number that's generated by hello sender logic app.</span></span> 
     <span data-ttu-id="a1d3f-156">Bu özelliği, tek bir toplu iş ile birden çok alt kümelerini kullanın ve her alt sağladığınız hello adıyla tanımlamak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-156">This capability lets you use a single batch with multiple subsets and define each subset with hello name that you provide.</span></span>

   * <span data-ttu-id="a1d3f-157">Merhaba, **gövde** kutusunda, hello zaman **dinamik içerik** seçin hello listesi görüntülenir, **ileti kimliği** alan.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-157">In hello **Body** box, when hello **Dynamic content** list appears, select hello **Message Id** field.</span></span>

     !["Body" için "İleti kimliği" seçin](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="a1d3f-159">Merhaba giriş hello gönderme e-posta eylemi için bir dizi olduğundan hello Tasarımcısı otomatik olarak ekler bir **her** döngü hello geçici **bir e-posta Gönder** eylem.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-159">Because hello input for hello send email action is an array, hello designer automatically adds a **For each** loop around hello **Send an email** action.</span></span> 
     <span data-ttu-id="a1d3f-160">Bu döngü hello toplu işteki her öğe hello iç eylemi gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-160">This loop performs hello inner action on each item in hello batch.</span></span> 
     <span data-ttu-id="a1d3f-161">Bu nedenle, hello toplu tetikleyici kümesi toofive öğeleri ile her zaman hello tetikleyici harekete beş e-postaları alır.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-161">So, with hello batch trigger set toofive items, you get five emails each time hello trigger fires.</span></span>

7.  <span data-ttu-id="a1d3f-162">Bir toplu alıcı mantıksal uygulama oluşturduğunuza göre mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Mantıksal uygulamanızı kaydetme](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a><span data-ttu-id="a1d3f-164">İletileri tooa yığını gönderme mantıksal uygulamalar oluşturma</span><span class="sxs-lookup"><span data-stu-id="a1d3f-164">Create logic apps that send messages tooa batch</span></span>

<span data-ttu-id="a1d3f-165">Şimdi hello alıcı mantıksal uygulama tarafından tanımlanan öğeleri toohello yığını gönderme bir veya daha fazla mantıksal uygulamalar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-165">Now create one or more logic apps that send items toohello batch defined by hello receiver logic app.</span></span> <span data-ttu-id="a1d3f-166">Merhaba gönderen için hello alıcı mantıksal uygulama ve toplu işlem adı, ileti içeriği ve diğer ayarları belirtin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-166">For hello sender, you specify hello receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="a1d3f-167">İsteğe bağlı olarak bu anahtarla alt kümelerini toocollect öğeleri benzersiz bir bölüm anahtarı toodivide hello toplu sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-167">You can optionally provide a unique partition key toodivide hello batch into subsets toocollect items with that key.</span></span>

<span data-ttu-id="a1d3f-168">Gönderen logic apps alıcı logic apps tooknow hello Gönderenler hakkında herhangi bir şey gerekmez ancak burada toosend öğe, bilmeniz.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-168">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="a1d3f-169">Bu ada sahip başka bir mantıksal uygulama oluşturma: "BatchSender"</span><span class="sxs-lookup"><span data-stu-id="a1d3f-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="a1d3f-170">Merhaba arama kutusuna "recurrence", filtre olarak girin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-170">In hello search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="a1d3f-171">Bu tetikleyici seçin: **çizelgesi - yineleme**</span><span class="sxs-lookup"><span data-stu-id="a1d3f-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![Merhaba "Yinelemeyi Zamanla" tetikleyicisi ekleyin](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="a1d3f-173">Merhaba sıklık ve aralığı toorun hello gönderen mantıksal uygulama dakikada ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-173">Set hello frequency and interval toorun hello sender logic app every minute.</span></span>

      ![Sıklık ve aralığı yinelenme tetikleyici için ayarlayın](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="a1d3f-175">İletileri tooa toplu göndermek için yeni bir adımı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-175">Add a new step for sending messages tooa batch.</span></span>

   1. <span data-ttu-id="a1d3f-176">Merhaba yinelenme tetikleyici altında seçin **+ yeni adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-176">Under hello recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="a1d3f-177">Merhaba arama kutusuna "toplu", filtre olarak girin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-177">In hello search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="a1d3f-178">Bu eylem seçin: **Gönder iletileri toobatch – toplu tetikleyici Logic Apps akışıyla seçin**</span><span class="sxs-lookup"><span data-stu-id="a1d3f-178">Select this action: **Send messages toobatch – Choose a Logic Apps workflow with batch trigger**</span></span>

      !["İletileri toobatch Gönder"'i seçin](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="a1d3f-180">Şimdi bir eylemi olarak artık görünen daha önce oluşturduğunuz "BatchReceiver" mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      !["Toplu alıcı" mantıksal uygulama seçin](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="a1d3f-182">Merhaba liste toplu Tetikleyicileri sahip herhangi bir mantıksal uygulamalar da gösterir.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-182">hello list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="a1d3f-183">Merhaba toplu özellikleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-183">Set hello batch properties.</span></span>

   * <span data-ttu-id="a1d3f-184">**Toplu işlemi adı**: "TestBatch" Bu örnekte ve çalışma zamanında doğrulanır hello alıcı mantıksal uygulama tarafından tanımlanan hello toplu işlem adı.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-184">**Batch Name**: hello batch name defined by hello receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="a1d3f-185">Merhaba alıcı mantıksal uygulama tarafından belirtilen hello toplu adıyla eşleşmelidir hello toplu adı değiştirmemeniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-185">Make sure that you don't change hello batch name, which must match hello batch name that's specified by hello receiver logic app.</span></span>
     > <span data-ttu-id="a1d3f-186">Değişen hello Tpl hello gönderen mantığı uygulama toofail neden olur.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-186">Changing hello batch name causes hello sender logic app toofail.</span></span>

   * <span data-ttu-id="a1d3f-187">**İleti içeriği**: Merhaba toosend istediğiniz ileti içeriği.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-187">**Message Content**: hello message content that you want toosend.</span></span> 
   <span data-ttu-id="a1d3f-188">Bu örnekte, eklemeleri iletisine hello toohello toplu iş gönderme içerik geçerli tarih ve saat hello bu deyim ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a1d3f-188">For this example, add this expression that inserts hello current date and time into hello message content that you send toohello batch:</span></span>

     1. <span data-ttu-id="a1d3f-189">Ne zaman hello **dinamik içerik** listesi görüntülenir, seçin **ifade**.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-189">When hello **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="a1d3f-190">Merhaba ifade girin **utcnow()**ve seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-190">Enter hello expression **utcnow()**, and choose **OK**.</span></span> 

        !["İletisi içeriği", "İfadesi" seçin.](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="a1d3f-193">Şimdi hello toplu işlemi için bir bölüm ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-193">Now set up a partition for hello batch.</span></span> <span data-ttu-id="a1d3f-194">Hello "BatchReceiver" eylemini seçin **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-194">In hello "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="a1d3f-195">**Bölüm adı**: hello hedef toplu bölme için bir isteğe bağlı benzersiz bir bölüm anahtarı toouse.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-195">**Partition Name**: An optional unique partition key toouse for dividing hello target batch.</span></span> <span data-ttu-id="a1d3f-196">Bu örnekte, bir ile beş arasında rastgele bir sayı oluşturan bir deyim ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="a1d3f-197">Ne zaman hello **dinamik içerik** listesi görüntülenir, seçin **ifade**.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-197">When hello **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="a1d3f-198">Bu ifade girin: **rand(1,6)**</span><span class="sxs-lookup"><span data-stu-id="a1d3f-198">Enter this expression: **rand(1,6)**</span></span>

        ![Hedef toplu işlemi için bir bölüm ayarlama](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="a1d3f-200">Bu **rand** işlevi bir ile beş arasında bir sayı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="a1d3f-201">Bu nedenle, bu toplu Bu ifade dinamik olarak ayarlayan beş numaralı, bölümlemesinde.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="a1d3f-202">**İleti kimliği**: isteğe bağlı ileti tanımlayıcısı ve boş olduğunda oluşturulan bir GUID.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="a1d3f-203">Bu örnekte, bu kutuyu boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="a1d3f-204">Mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-204">Save your logic app.</span></span> <span data-ttu-id="a1d3f-205">Gönderen mantıksal uygulamanızı şimdi benzer toothis örnek görünür:</span><span class="sxs-lookup"><span data-stu-id="a1d3f-205">Your sender logic app now looks similar toothis example:</span></span>

   ![Gönderen mantıksal uygulamanızı kaydetme](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="a1d3f-207">Mantıksal uygulamalarınızı test etme</span><span class="sxs-lookup"><span data-stu-id="a1d3f-207">Test your logic apps</span></span>

<span data-ttu-id="a1d3f-208">tootest, çözüm, toplu işleme için bir kaç dakika çalıştıran logic apps bırakın.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-208">tootest your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="a1d3f-209">Bir süre sonra grupları beş e-postaları almaya başlayın, tüm hello ile aynı anahtar bölüm.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-209">Soon, you start getting emails in groups of five, all with hello same partition key.</span></span>

<span data-ttu-id="a1d3f-210">BatchSender mantıksal uygulamanızı dakikada çalışır, bir ile beş arasında rastgele bir sayı oluşturur ve iletileri gönderildiği hello bölüm anahtarı hello hedef toplu olarak oluşturulan bu numarayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as hello partition key for hello target batch where messages are sent.</span></span> <span data-ttu-id="a1d3f-211">Merhaba toplu hello ile beş öğelerine sahip her zaman aynı bölüm anahtarı, BatchReceiver mantıksal uygulamanızı başlatılır ve her ileti için posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-211">Each time hello batch has five items with hello same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a1d3f-212">Bitirdiğinizde test, hello BatchSender mantığı uygulama toostop iletileri gönderme devre dışı bırakın ve gelen aşırı kaçının emin olun.</span><span class="sxs-lookup"><span data-stu-id="a1d3f-212">When you're done testing, make sure that you disable hello BatchSender logic app toostop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1d3f-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a1d3f-213">Next steps</span></span>

* [<span data-ttu-id="a1d3f-214">JSON kullanarak mantıksal uygulama tanımları oluşturma</span><span class="sxs-lookup"><span data-stu-id="a1d3f-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="a1d3f-215">Visual Studio'da Azure Logic Apps ve işlevleri ile sunucusuz bir uygulama oluşturun</span><span class="sxs-lookup"><span data-stu-id="a1d3f-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="a1d3f-216">Özel durum işleme ve logic apps için hata günlüğü</span><span class="sxs-lookup"><span data-stu-id="a1d3f-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
