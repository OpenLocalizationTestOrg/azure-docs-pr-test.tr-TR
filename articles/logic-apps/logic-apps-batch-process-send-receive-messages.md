---
title: "Bir grubun veya koleksiyonun - Azure mantıksal uygulamaları toplu işlem iletilerinin | Microsoft Docs"
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
ms.openlocfilehash: 480ffce5dbe7c25181bb0ba5639de884e98ff4e6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="11065-104">Gönderme, alma ve logic apps işlem iletileri toplu</span><span class="sxs-lookup"><span data-stu-id="11065-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="11065-105">Birlikte gruplarındaki iletileri işlemek için veri öğeleri ya da iletileri için gönderebilirsiniz bir *toplu*ve ardından bu öğeleri toplu iş olarak işlem.</span><span class="sxs-lookup"><span data-stu-id="11065-105">To process messages together in groups, you can send data items, or messages, to a *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="11065-106">Bu yaklaşım, veri öğelerini birlikte işlenir ve belirli bir şekilde gruplama emin olmak istediğinizde yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="11065-106">This approach is useful when you want to make sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="11065-107">Öğeleri kullanarak toplu iş olarak almayı mantıksal uygulamalar oluşturabileceğiniz **toplu** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="11065-107">You can create logic apps that receive items as a batch by using the **Batch** trigger.</span></span> <span data-ttu-id="11065-108">Daha sonra öğeleri kullanarak bir toplu iş gönderme logic apps oluşturabilirsiniz **toplu** eylem.</span><span class="sxs-lookup"><span data-stu-id="11065-108">You can then create logic apps that send items to a batch by using the **Batch** action.</span></span>

<span data-ttu-id="11065-109">Bu konu, bu görevleri gerçekleştirerek toplu bir çözümü nasıl oluşturabilirsiniz gösterir:</span><span class="sxs-lookup"><span data-stu-id="11065-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="11065-110">[Alan ve öğeleri toplu iş olarak toplayan bir mantıksal uygulama oluşturma](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="11065-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="11065-111">Bu "toplu alıcı" mantıksal uygulama alıcı mantıksal uygulama serbest bırakır ve öğelerini işler önce karşılamak için toplu ad ve sürüm ölçütlerini belirtir.</span><span class="sxs-lookup"><span data-stu-id="11065-111">This "batch receiver" logic app specifies the batch name and release criteria to meet before the receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="11065-112">[Bir toplu iş öğeleri gönderen bir mantıksal uygulama oluşturma](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="11065-112">[Create a logic app that sends items to a batch](#batch-sender).</span></span> <span data-ttu-id="11065-113">Bu "toplu gönderen" mantıksal uygulama, var olan bir toplu alıcı mantığı uygulamaya olmalıdır öğeleri göndermek konumu belirtir.</span><span class="sxs-lookup"><span data-stu-id="11065-113">This "batch sender" logic app specifies where to send items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="11065-114">Ayrıca, "Bölüm" veya bölmek, bu anahtarı temel alt kümeler halinde hedef toplu için ek olarak, müşteri numarası gibi benzersiz bir anahtar belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11065-114">You can also specify a unique key, like a customer number, to "partition", or divide, the target batch into subsets based on that key.</span></span> <span data-ttu-id="11065-115">Böylece, tüm öğeleri aynı anahtarla toplanan ve birlikte işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="11065-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="11065-116">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="11065-116">Requirements</span></span>

<span data-ttu-id="11065-117">Bu örnek takip etmek için bu öğeler gerekir:</span><span class="sxs-lookup"><span data-stu-id="11065-117">To follow this example, you need these items:</span></span>

* <span data-ttu-id="11065-118">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="11065-118">An Azure subscription.</span></span> <span data-ttu-id="11065-119">Bir aboneliğiniz yoksa [ücretsiz bir Azure hesabı ile başlayabilirsiniz](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="11065-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="11065-120">Ya da [Kullandıkça Öde aboneliğine kaydolabilirsiniz](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="11065-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="11065-121">Hakkındaki temel bilgileri [mantıksal uygulamalar oluşturma](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="11065-121">Basic knowledge about [how to create logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="11065-122">Herhangi bir e-posta hesabı [Azure mantıksal uygulamaları tarafından desteklenen e-posta sağlayıcısı](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="11065-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="11065-123">Toplu iş olarak iletilerini mantıksal uygulamalar oluşturma</span><span class="sxs-lookup"><span data-stu-id="11065-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="11065-124">Bir toplu iletileri göndermeden önce "toplu alıcı" mantıksal uygulama ile ilk oluşturmalısınız **toplu** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="11065-124">Before you can send messages to a batch, you must first create a "batch receiver" logic app with the **Batch** trigger.</span></span> <span data-ttu-id="11065-125">Gönderen mantıksal uygulama oluşturduğunuzda, bu şekilde, bu alıcı mantıksal uygulama seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11065-125">That way, you can select this receiver logic app when you create the sender logic app.</span></span> <span data-ttu-id="11065-126">Alıcı için toplu işlem adı, sürüm ölçütlerini ve diğer ayarları belirtin.</span><span class="sxs-lookup"><span data-stu-id="11065-126">For the receiver, you specify the batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="11065-127">Gönderen logic apps alıcı logic apps Gönderenler ilgili herhangi bir şey bilmek zorunda değilsiniz sırada öğeleri gönderileceği yeri bilmeniz.</span><span class="sxs-lookup"><span data-stu-id="11065-127">Sender logic apps need know where to send items, while receiver logic apps don't need to know anything about the senders.</span></span>

1. <span data-ttu-id="11065-128">İçinde [Azure portal](https://portal.azure.com), bu ada sahip bir mantıksal uygulama oluşturma: "BatchReceiver"</span><span class="sxs-lookup"><span data-stu-id="11065-128">In the [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="11065-129">Logic Apps Tasarımcısı'nda eklemek **toplu** , logic app iş akışınızı başlatır tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="11065-129">In Logic Apps Designer, add the **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="11065-130">Arama kutusuna "toplu", filtre olarak girin.</span><span class="sxs-lookup"><span data-stu-id="11065-130">In the search box, enter "batch" as your filter.</span></span> <span data-ttu-id="11065-131">Bu tetikleyici seçin: **toplu – toplu iletileri**</span><span class="sxs-lookup"><span data-stu-id="11065-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Toplu tetikleyicisi ekleyin](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="11065-133">Toplu işlem için bir ad ve toplu örneğin serbest ölçütlerini belirtin:</span><span class="sxs-lookup"><span data-stu-id="11065-133">Provide a name for the batch, and specify criteria for releasing the batch, for example:</span></span>

   * <span data-ttu-id="11065-134">**Toplu işlemi adı**: Bu örnekte "TestBatch" olan toplu tanımlamak için kullanılan ad.</span><span class="sxs-lookup"><span data-stu-id="11065-134">**Batch Name**: The name used to identify the batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="11065-135">**İleti sayısı**: Bu örnekte, "5" olan işleme serbest bırakmadan önce toplu iş olarak tutmak için ileti sayısı.</span><span class="sxs-lookup"><span data-stu-id="11065-135">**Message Count**: The number of messages to hold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Toplu iş tetikleyici ayrıntılarını sağlayın](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="11065-137">Toplu tetikleyici başlatıldığında, bir e-posta gönderen başka bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="11065-137">Add another action that sends an email when the batch trigger fires.</span></span> <span data-ttu-id="11065-138">Her zaman toplu beş öğelerine sahip mantıksal uygulama bir e-posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="11065-138">Each time the batch has five items, the logic app sends an email.</span></span>

   1. <span data-ttu-id="11065-139">Toplu tetikleyici altında seçin **+ yeni adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="11065-139">Under the batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="11065-140">Arama kutusuna "e-posta", filtre olarak girin.</span><span class="sxs-lookup"><span data-stu-id="11065-140">In the search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="11065-141">E-posta sağlayıcınız üzerinde bağlı olarak, bir e-posta Bağlayıcısı'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="11065-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="11065-142">Örneğin, bir iş veya Okul hesabınız varsa, Office 365 Outlook Bağlayıcısı'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="11065-142">For example, if you have a work or school account, select the Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="11065-143">Gmail hesabınız varsa, Gmail Bağlayıcısı'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="11065-143">If you have a Gmail account, select the Gmail connector.</span></span>

   3. <span data-ttu-id="11065-144">Bu eylem, bağlayıcı için seçin:  **{*e-posta sağlayıcısı*}-bir e-posta ** Gönder</span><span class="sxs-lookup"><span data-stu-id="11065-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="11065-145">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="11065-145">For example:</span></span>

      ![E-posta sağlayıcınız için "bir e-posta Gönder" eylemini seçin](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="11065-147">E-posta sağlayıcınız için daha önce bir bağlantı oluşturmadıysanız, istendiğinde kimlik doğrulaması için e-posta kimlik bilgilerinizi sağlayın.</span><span class="sxs-lookup"><span data-stu-id="11065-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="11065-148">Daha fazla bilgi edinmek [e-posta kimlik bilgilerinizi kimlik doğrulaması](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="11065-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="11065-149">Yeni eklediğiniz eylem özelliklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="11065-149">Set the properties for the action you just added.</span></span>

   * <span data-ttu-id="11065-150">İçinde **için** kutusuna, alıcının e-posta adresi girin.</span><span class="sxs-lookup"><span data-stu-id="11065-150">In the **To** box, enter the recipient's email address.</span></span> 
   <span data-ttu-id="11065-151">Test amacıyla, kendi e-posta adresini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11065-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="11065-152">İçinde **konu** kutusu, ne zaman **dinamik içerik** listesi görüntülenir, seçin **bölüm adı** alan.</span><span class="sxs-lookup"><span data-stu-id="11065-152">In the **Subject** box, when the **Dynamic content** list appears, select the **Partition Name** field.</span></span>

     !["Dinamik içerik" listesinden "Bölüm adı"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="11065-154">Sonraki bölümde, hedef toplu iletileri burada göndermek amacıyla mantıksal kümelerini böler benzersiz bölüm anahtarı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11065-154">In a later section, you can specify a unique partition key that divides the target batch into logical sets to where you can send messages.</span></span> 
     <span data-ttu-id="11065-155">Her küme gönderen mantıksal uygulama tarafından oluşturulan benzersiz bir numara vardır.</span><span class="sxs-lookup"><span data-stu-id="11065-155">Each set has a unique number that's generated by the sender logic app.</span></span> 
     <span data-ttu-id="11065-156">Bu özelliği tek bir toplu iş ile birden çok alt kümelerini kullanın ve her alt sağladığınız ada sahip tanımlayın olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="11065-156">This capability lets you use a single batch with multiple subsets and define each subset with the name that you provide.</span></span>

   * <span data-ttu-id="11065-157">İçinde **gövde** kutusu, ne zaman **dinamik içerik** listesi görüntülenir, seçin **ileti kimliği** alan.</span><span class="sxs-lookup"><span data-stu-id="11065-157">In the **Body** box, when the **Dynamic content** list appears, select the **Message Id** field.</span></span>

     !["Body" için "İleti kimliği" seçin](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="11065-159">Giriş gönderme e-posta eylemi için bir dizi olduğundan Tasarımcısı otomatik olarak ekler bir **her** geçici döngü **bir e-posta Gönder** eylem.</span><span class="sxs-lookup"><span data-stu-id="11065-159">Because the input for the send email action is an array, the designer automatically adds a **For each** loop around the **Send an email** action.</span></span> 
     <span data-ttu-id="11065-160">Bu döngü iç eylem her toplu iş öğesinde gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="11065-160">This loop performs the inner action on each item in the batch.</span></span> 
     <span data-ttu-id="11065-161">Toplu tetikleyici beş öğelerine ayarlamak almak için tetikleyici ateşlenir beş e-postaları her zaman.</span><span class="sxs-lookup"><span data-stu-id="11065-161">So, with the batch trigger set to five items, you get five emails each time the trigger fires.</span></span>

7.  <span data-ttu-id="11065-162">Bir toplu alıcı mantıksal uygulama oluşturduğunuza göre mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="11065-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Mantıksal uygulamanızı kaydetme](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-to-a-batch"></a><span data-ttu-id="11065-164">İleti göndermek için bir toplu iş mantığı uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="11065-164">Create logic apps that send messages to a batch</span></span>

<span data-ttu-id="11065-165">Şimdi alıcı mantıksal uygulama tarafından tanımlanan toplu iş öğeleri göndermek bir veya daha fazla mantıksal uygulamalar oluşturun.</span><span class="sxs-lookup"><span data-stu-id="11065-165">Now create one or more logic apps that send items to the batch defined by the receiver logic app.</span></span> <span data-ttu-id="11065-166">Gönderen, alıcı mantıksal uygulama ve toplu işlem adı, ileti içeriği ve diğer ayarları belirtin.</span><span class="sxs-lookup"><span data-stu-id="11065-166">For the sender, you specify the receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="11065-167">İsteğe bağlı olarak bu anahtarla öğeleri toplamak için alt kümelerini toplu bölmek için benzersiz bir bölüm anahtarı sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="11065-167">You can optionally provide a unique partition key to divide the batch into subsets to collect items with that key.</span></span>

<span data-ttu-id="11065-168">Gönderen logic apps alıcı logic apps Gönderenler ilgili herhangi bir şey bilmek zorunda değilsiniz sırada öğeleri gönderileceği yeri bilmeniz.</span><span class="sxs-lookup"><span data-stu-id="11065-168">Sender logic apps need know where to send items, while receiver logic apps don't need to know anything about the senders.</span></span>

1. <span data-ttu-id="11065-169">Bu ada sahip başka bir mantıksal uygulama oluşturma: "BatchSender"</span><span class="sxs-lookup"><span data-stu-id="11065-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="11065-170">Arama kutusuna "recurrence", filtre olarak girin.</span><span class="sxs-lookup"><span data-stu-id="11065-170">In the search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="11065-171">Bu tetikleyici seçin: **çizelgesi - yineleme**</span><span class="sxs-lookup"><span data-stu-id="11065-171">Select this trigger: **Schedule - Recurrence**</span></span>

      !["Yinelemeyi Zamanla" tetikleyicisi ekleyin](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="11065-173">Gönderenin çalıştırma aralığı ve sıklığı ayarlama mantıksal uygulama dakikada.</span><span class="sxs-lookup"><span data-stu-id="11065-173">Set the frequency and interval to run the sender logic app every minute.</span></span>

      ![Sıklık ve aralığı yinelenme tetikleyici için ayarlayın](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="11065-175">Bir toplu ileti göndermek için yeni bir adımı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="11065-175">Add a new step for sending messages to a batch.</span></span>

   1. <span data-ttu-id="11065-176">Yineleme tetikleyici altında seçin **+ yeni adım** > **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="11065-176">Under the recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="11065-177">Arama kutusuna "toplu", filtre olarak girin.</span><span class="sxs-lookup"><span data-stu-id="11065-177">In the search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="11065-178">Bu eylem seçin: **toplu – toplu tetikleyici Logic Apps akışıyla seçmek için ileti gönderme**</span><span class="sxs-lookup"><span data-stu-id="11065-178">Select this action: **Send messages to batch – Choose a Logic Apps workflow with batch trigger**</span></span>

      !["Toplu iletileri gönder"'i seçin](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="11065-180">Şimdi bir eylemi olarak artık görünen daha önce oluşturduğunuz "BatchReceiver" mantıksal uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="11065-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      !["Toplu alıcı" mantıksal uygulama seçin](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="11065-182">Liste toplu Tetikleyicileri sahip herhangi bir mantıksal uygulamalar da gösterir.</span><span class="sxs-lookup"><span data-stu-id="11065-182">The list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="11065-183">Toplu özellikleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="11065-183">Set the batch properties.</span></span>

   * <span data-ttu-id="11065-184">**Toplu işlemi adı**: "TestBatch" Bu örnekte ve çalışma zamanında doğrulanır alıcı mantıksal uygulama tarafından tanımlanan toplu işlem adı.</span><span class="sxs-lookup"><span data-stu-id="11065-184">**Batch Name**: The batch name defined by the receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="11065-185">Alıcı mantıksal uygulama tarafından belirtilen toplu işlem adı eşleşmelidir toplu işlem adı değişmez emin olun.</span><span class="sxs-lookup"><span data-stu-id="11065-185">Make sure that you don't change the batch name, which must match the batch name that's specified by the receiver logic app.</span></span>
     > <span data-ttu-id="11065-186">Toplu adının değiştirilmesi neden gönderen mantıksal uygulama başarısız.</span><span class="sxs-lookup"><span data-stu-id="11065-186">Changing the batch name causes the sender logic app to fail.</span></span>

   * <span data-ttu-id="11065-187">**İleti içeriği**: göndermek istediğiniz ileti içeriği.</span><span class="sxs-lookup"><span data-stu-id="11065-187">**Message Content**: The message content that you want to send.</span></span> 
   <span data-ttu-id="11065-188">Bu örnekte, geçerli tarih ve saat için toplu Gönder ileti içeriği ekler bu deyim ekleyin:</span><span class="sxs-lookup"><span data-stu-id="11065-188">For this example, add this expression that inserts the current date and time into the message content that you send to the batch:</span></span>

     1. <span data-ttu-id="11065-189">Zaman **dinamik içerik** listesi görüntülenir, seçin **ifade**.</span><span class="sxs-lookup"><span data-stu-id="11065-189">When the **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="11065-190">İfade girin **utcnow()**ve seçin **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="11065-190">Enter the expression **utcnow()**, and choose **OK**.</span></span> 

        !["İletisi içeriği", "İfadesi" seçin.](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="11065-193">Toplu işlem için bir bölüm şimdi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="11065-193">Now set up a partition for the batch.</span></span> <span data-ttu-id="11065-194">"BatchReceiver" eylemini seçin **Gelişmiş Seçenekleri Göster**.</span><span class="sxs-lookup"><span data-stu-id="11065-194">In the "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="11065-195">**Bölüm adı**: hedef toplu bölme için kullanılacak bir isteğe bağlı benzersiz bir bölüm anahtarı.</span><span class="sxs-lookup"><span data-stu-id="11065-195">**Partition Name**: An optional unique partition key to use for dividing the target batch.</span></span> <span data-ttu-id="11065-196">Bu örnekte, bir ile beş arasında rastgele bir sayı oluşturan bir deyim ekleyin.</span><span class="sxs-lookup"><span data-stu-id="11065-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="11065-197">Zaman **dinamik içerik** listesi görüntülenir, seçin **ifade**.</span><span class="sxs-lookup"><span data-stu-id="11065-197">When the **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="11065-198">Bu ifade girin: **rand(1,6)**</span><span class="sxs-lookup"><span data-stu-id="11065-198">Enter this expression: **rand(1,6)**</span></span>

        ![Hedef toplu işlemi için bir bölüm ayarlama](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="11065-200">Bu **rand** işlevi bir ile beş arasında bir sayı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="11065-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="11065-201">Bu nedenle, bu toplu Bu ifade dinamik olarak ayarlayan beş numaralı, bölümlemesinde.</span><span class="sxs-lookup"><span data-stu-id="11065-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="11065-202">**İleti kimliği**: isteğe bağlı ileti tanımlayıcısı ve boş olduğunda oluşturulan bir GUID.</span><span class="sxs-lookup"><span data-stu-id="11065-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="11065-203">Bu örnekte, bu kutuyu boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="11065-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="11065-204">Mantıksal uygulamanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="11065-204">Save your logic app.</span></span> <span data-ttu-id="11065-205">Gönderen mantıksal uygulamanızı şimdi bu örneğe benzer görünür:</span><span class="sxs-lookup"><span data-stu-id="11065-205">Your sender logic app now looks similar to this example:</span></span>

   ![Gönderen mantıksal uygulamanızı kaydetme](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="11065-207">Mantıksal uygulamalarınızı test etme</span><span class="sxs-lookup"><span data-stu-id="11065-207">Test your logic apps</span></span>

<span data-ttu-id="11065-208">Toplu çözümünüzü test etmek için bir kaç dakika çalıştıran logic apps bırakın.</span><span class="sxs-lookup"><span data-stu-id="11065-208">To test your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="11065-209">Bir süre sonra aynı bölüm anahtarına sahip tüm beş gruplarındaki e-postaları almaya başlayın.</span><span class="sxs-lookup"><span data-stu-id="11065-209">Soon, you start getting emails in groups of five, all with the same partition key.</span></span>

<span data-ttu-id="11065-210">BatchSender mantıksal uygulamanızı dakikada çalışır, bir ile beş arasında rastgele bir sayı oluşturur ve iletileri gönderildiği hedef toplu bölüm anahtarı olarak oluşturulan bu numarayı kullanır.</span><span class="sxs-lookup"><span data-stu-id="11065-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as the partition key for the target batch where messages are sent.</span></span> <span data-ttu-id="11065-211">Toplu işlem aynı bölüm anahtarına sahip beş öğelerine sahip her zaman BatchReceiver mantıksal uygulamanızı başlatılır ve her ileti için posta gönderir.</span><span class="sxs-lookup"><span data-stu-id="11065-211">Each time the batch has five items with the same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11065-212">Bitirdiğinizde test, ileti gönderilmesini durdurmak ve gelen aşırı önlemek için BatchSender mantıksal uygulama devre dışı bırakıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="11065-212">When you're done testing, make sure that you disable the BatchSender logic app to stop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11065-213">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="11065-213">Next steps</span></span>

* [<span data-ttu-id="11065-214">JSON kullanarak mantıksal uygulama tanımları oluşturma</span><span class="sxs-lookup"><span data-stu-id="11065-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="11065-215">Visual Studio'da Azure Logic Apps ve işlevleri ile sunucusuz bir uygulama oluşturun</span><span class="sxs-lookup"><span data-stu-id="11065-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="11065-216">Özel durum işleme ve logic apps için hata günlüğü</span><span class="sxs-lookup"><span data-stu-id="11065-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
