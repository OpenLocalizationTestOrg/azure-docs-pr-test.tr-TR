---
title: "Mantıksal uygulamalarınızı aaaAdd hello Office 365 Outlook connector | Microsoft Docs"
description: "Office 365 ile Office 365 Bağlayıcısı tooenable etkileşimi ile mantıksal uygulamalar oluşturun. Örneğin: oluşturma, düzenleme ve kişiler ve takvim öğeleri güncelleştirme."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a><span data-ttu-id="42468-104">Merhaba Office 365 Outlook Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="42468-104">Get started with hello Office 365 Outlook connector</span></span>
<span data-ttu-id="42468-105">Merhaba Office 365 Outlook Bağlayıcısı, Office 365'te Outlook ile etkileşim sağlar.</span><span class="sxs-lookup"><span data-stu-id="42468-105">hello Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="42468-106">Bu bağlayıcı toocreate, düzenleme, güncelleştirme kişiler ve takvim öğeleri kullanın ve ayrıca almak, Gönder ve tooemail yanıt.</span><span class="sxs-lookup"><span data-stu-id="42468-106">Use this connector toocreate, edit, and update contacts and calendar items, and also get, send, and reply tooemail.</span></span>

<span data-ttu-id="42468-107">Office 365 Outlook ile:</span><span class="sxs-lookup"><span data-stu-id="42468-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="42468-108">Office 365 içinde Hello e-posta ve Takvim özellikleri kullanarak, iş akışı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="42468-108">Build your workflow using hello email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="42468-109">Kullanım toostart olduğunda yeni e-posta, Takvim öğesi güncelleştirildiğinde, iş akışınızı ve daha fazlasını tetikler.</span><span class="sxs-lookup"><span data-stu-id="42468-109">Use triggers toostart your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="42468-110">Eylemler toosend bir e-posta kullanın, yeni bir takvim olayı ve daha fazlasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="42468-110">Use actions toosend an email, create a new calendar event, and more.</span></span> <span data-ttu-id="42468-111">Salesforce (tetikleyici) yeni bir nesne olduğunda, örneğin, bir e-posta Gönder tooyour Office 365 Outlook (bir eylem).</span><span class="sxs-lookup"><span data-stu-id="42468-111">For example, when there is a new object in Salesforce (a trigger), send an email tooyour Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="42468-112">Bu konuda nasıl toouse hello bir mantıksal uygulama Office 365 Outlook connector gösterir ve ayrıca listeleri tetikleyiciler ve Eylemler hello.</span><span class="sxs-lookup"><span data-stu-id="42468-112">This topic shows you how toouse hello Office 365 Outlook connector in a logic app, and also lists hello triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="42468-113">Merhaba makalenin bu sürümü tooLogic uygulamaları genel kullanılabilirlik (GA) uygulanır.</span><span class="sxs-lookup"><span data-stu-id="42468-113">This version of hello article applies tooLogic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="42468-114">Logic Apps hakkında daha fazla toolearn bkz [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="42468-114">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="42468-115">TooOffice 365 Bağlan</span><span class="sxs-lookup"><span data-stu-id="42468-115">Connect tooOffice 365</span></span>
<span data-ttu-id="42468-116">Mantıksal uygulamanızı herhangi bir hizmete erişebilmesi için önce oluşturduğunuz bir *bağlantı* toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="42468-116">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="42468-117">Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="42468-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="42468-118">Örneğin, tooconnect tooOffice 365 Outlook, ilk ihtiyacınız bir Office 365 *bağlantı*.</span><span class="sxs-lookup"><span data-stu-id="42468-118">For example, tooconnect tooOffice 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="42468-119">toocreate bir bağlantı için tooconnect istediğiniz tooaccess hello hizmet normalde kullandığınız hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="42468-119">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="42468-120">Bu nedenle Office 365 Outlook ile Merhaba kimlik bilgilerini tooyour Office 365 hesabı toocreate hello bağlantısı girin.</span><span class="sxs-lookup"><span data-stu-id="42468-120">So with Office 365 Outlook, enter hello credentials tooyour Office 365 account toocreate hello connection.</span></span>

## <a name="create-hello-connection"></a><span data-ttu-id="42468-121">Merhaba bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="42468-121">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="42468-122">Bir tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="42468-122">Use a trigger</span></span>
<span data-ttu-id="42468-123">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="42468-123">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="42468-124">Tetikleyiciler "Merhaba hizmet bir aralığı ve istediğiniz sıklığı yoklama".</span><span class="sxs-lookup"><span data-stu-id="42468-124">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="42468-125">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="42468-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="42468-126">Merhaba mantıksal uygulama içinde "office 365" tooget hello Tetikleyicileri listesini yazın:</span><span class="sxs-lookup"><span data-stu-id="42468-126">In hello logic app, type "office 365" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="42468-127">Seçin **Office 365 yaklaşan bir olay yakında başlatırken Outlook -**.</span><span class="sxs-lookup"><span data-stu-id="42468-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="42468-128">Bir bağlantı zaten varsa, bir takvim hello aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="42468-128">If a connection already exists, then select a calendar from hello drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="42468-129">İçinde istendiğinde toosign varsa, hello oturum ayrıntıları toocreate hello bağlantısında girin.</span><span class="sxs-lookup"><span data-stu-id="42468-129">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="42468-130">[Merhaba bağlantı oluşturmak](connectors-create-api-office365-outlook.md#create-the-connection) bu konudaki hello adımlar listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="42468-130">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="42468-131">Bu örnekte, bir takvim olay güncelleştirildiğinde hello mantıksal uygulama çalışır.</span><span class="sxs-lookup"><span data-stu-id="42468-131">In this example, hello logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="42468-132">Bu tetikleyici toosee hello sonuçlarını bir kısa mesaj gönderir başka bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="42468-132">toosee hello results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="42468-133">Örneğin, hello Twilio ekleyin *ileti gönder* hello olduğunda Takvim olay metinleri 15 dakika içinde başlangıç eylem.</span><span class="sxs-lookup"><span data-stu-id="42468-133">For example, add hello Twilio *Send message* action that texts you when hello calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="42468-134">Select hello **Düzenle** düğmesine tıklayın ve ayarlama hello **sıklığı** ve **aralığı** değerleri.</span><span class="sxs-lookup"><span data-stu-id="42468-134">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="42468-135">Örneğin, 15 dakikada bir hello tetikleyici toopoll istiyorsanız, ardından hello ayarlayın **sıklığı** çok**Minute**ve kümesi hello **aralığı** çok**15**.</span><span class="sxs-lookup"><span data-stu-id="42468-135">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="42468-136">**Kaydet** değişikliklerinizi (sol üst köşesindeki hello araç).</span><span class="sxs-lookup"><span data-stu-id="42468-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="42468-137">Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="42468-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="42468-138">Bir eylem kullanın</span><span class="sxs-lookup"><span data-stu-id="42468-138">Use an action</span></span>
<span data-ttu-id="42468-139">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="42468-139">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="42468-140">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="42468-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="42468-141">Merhaba artı işaretini seçin.</span><span class="sxs-lookup"><span data-stu-id="42468-141">Select hello plus sign.</span></span> <span data-ttu-id="42468-142">Birkaç seçeneğiniz bkz: **Eylem Ekle**, **bir koşul eklemek**, veya hello **daha fazla** seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="42468-142">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="42468-143">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="42468-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="42468-144">Merhaba metin kutusuna "office 365" tooget tüm hello kullanılabilir eylemlerin bir listesini yazın.</span><span class="sxs-lookup"><span data-stu-id="42468-144">In hello text box, type “office 365” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="42468-145">Bizim örneğimizde seçin **Office 365 Outlook - kişi oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="42468-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="42468-146">Bir bağlantı zaten varsa, hello seçin **klasörü kimliği**, **verilen ad**ve diğer özellikleri:</span><span class="sxs-lookup"><span data-stu-id="42468-146">If a connection already exists, then choose hello **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="42468-147">Merhaba bağlantı bilgilerini istenirse, hello ayrıntıları toocreate hello bağlantısı girin.</span><span class="sxs-lookup"><span data-stu-id="42468-147">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="42468-148">[Merhaba bağlantı oluşturmak](connectors-create-api-office365-outlook.md#create-the-connection) bu konuda bu özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="42468-148">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="42468-149">Bu örnekte, Office 365 Outlook içinde yeni bir kişi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="42468-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="42468-150">Başka bir tetikleyici toocreate hello kişi çıktısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="42468-150">You can use output from another trigger toocreate hello contact.</span></span> <span data-ttu-id="42468-151">Örneğin, SalesForce hello ekleyin *bir nesne oluşturulduğunda* tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="42468-151">For example, add hello SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="42468-152">Merhaba Office 365 Outlook eklemek *kişi oluşturma* hello SalesForce kullandığı eylem toocreate hello yeni yeni kişi Office 365'te alanları.</span><span class="sxs-lookup"><span data-stu-id="42468-152">Then add hello Office 365 Outlook *Create contact* action that uses hello SalesForce fields toocreate hello new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="42468-153">**Kaydet** değişikliklerinizi (sol üst köşesindeki hello araç).</span><span class="sxs-lookup"><span data-stu-id="42468-153">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="42468-154">Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="42468-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="42468-155">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="42468-155">Connector-specific details</span></span>

<span data-ttu-id="42468-156">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="42468-156">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="42468-157">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="42468-157">Next Steps</span></span>
<span data-ttu-id="42468-158">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="42468-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="42468-159">Araştır Logic Apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="42468-159">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

