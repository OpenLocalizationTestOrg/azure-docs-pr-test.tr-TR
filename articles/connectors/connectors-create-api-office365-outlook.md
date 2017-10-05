---
title: "Office 365 Outlook Bağlayıcısı Logic Apps içinde ekleme | Microsoft Docs"
description: "Office 365 ile etkileşimi etkinleştirmek için Office 365 Bağlayıcısı ile mantıksal uygulamalar oluşturun. Örneğin: oluşturma, düzenleme ve kişiler ve takvim öğeleri güncelleştirme."
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
ms.openlocfilehash: 5335dae62e61659b68e8befb4ed0d404dffb800c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-outlook-connector"></a><span data-ttu-id="91762-104">Office 365 Outlook Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="91762-104">Get started with the Office 365 Outlook connector</span></span>
<span data-ttu-id="91762-105">Office 365 Outlook Bağlayıcısı, Office 365'te Outlook ile etkileşim sağlar.</span><span class="sxs-lookup"><span data-stu-id="91762-105">The Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="91762-106">Bu Bağlayıcıyı oluşturmak, düzenlemek ve kişiler ve takvim öğeleri, güncelleştirme ve ayrıca almak, Gönder ve e-posta için için kullanın.</span><span class="sxs-lookup"><span data-stu-id="91762-106">Use this connector to create, edit, and update contacts and calendar items, and also get, send, and reply to email.</span></span>

<span data-ttu-id="91762-107">Office 365 Outlook ile:</span><span class="sxs-lookup"><span data-stu-id="91762-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="91762-108">Office 365 e-posta ve Takvim özeliklerin kullanarak, iş akışı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="91762-108">Build your workflow using the email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="91762-109">Tetikleyiciler, bir Takvim öğesi güncelleştirildiğinde bir yeni e-posta ve daha fazla olduğunda, iş akışını başlatmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="91762-109">Use triggers to start your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="91762-110">Eylemler bir e-posta Gönder, yeni bir takvim olayı ve daha fazlasını oluşturmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="91762-110">Use actions to send an email, create a new calendar event, and more.</span></span> <span data-ttu-id="91762-111">Örneğin, Salesforce (tetikleyici) yeni bir nesne olduğunda, Office 365 Outlook (bir eylem) bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="91762-111">For example, when there is a new object in Salesforce (a trigger), send an email to your Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="91762-112">Bu konuda, bir mantıksal uygulama Office 365 Outlook Bağlayıcısı'nı kullanmayı gösterir ve ayrıca tetikleyiciler ve eylemler listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="91762-112">This topic shows you how to use the Office 365 Outlook connector in a logic app, and also lists the triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="91762-113">Makalenin bu sürümü Logic Apps genel kullanılabilirlik (GA) için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="91762-113">This version of the article applies to Logic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="91762-114">Logic Apps hakkında daha fazla bilgi için bkz: [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="91762-114">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="91762-115">Office 365’e bağlanın</span><span class="sxs-lookup"><span data-stu-id="91762-115">Connect to Office 365</span></span>
<span data-ttu-id="91762-116">Mantıksal uygulamanızı herhangi bir hizmete erişebilmesi için önce oluşturduğunuz bir *bağlantı* hizmet.</span><span class="sxs-lookup"><span data-stu-id="91762-116">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="91762-117">Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="91762-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="91762-118">Örneğin, Office 365 Outlook'a bağlanmak için önce bir Office 365 gerekir *bağlantı*.</span><span class="sxs-lookup"><span data-stu-id="91762-118">For example, to connect to Office 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="91762-119">Bir bağlantı oluşturmak için normalde bağlanmak istediğiniz hizmete erişmek için kullandığınız kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="91762-119">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="91762-120">Bu nedenle Office 365 Outlook ile bağlantı oluşturmak için Office 365 hesabınıza kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="91762-120">So with Office 365 Outlook, enter the credentials to your Office 365 account to create the connection.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="91762-121">Bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="91762-121">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to Office 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="91762-122">Bir tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="91762-122">Use a trigger</span></span>
<span data-ttu-id="91762-123">Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="91762-123">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="91762-124">Tetikleyiciler "hizmet bir aralığı ve istediğiniz sıklığı yoklama".</span><span class="sxs-lookup"><span data-stu-id="91762-124">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="91762-125">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="91762-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="91762-126">Mantıksal uygulama "Tetikleyiciler listesini almak için office 365" yazın:</span><span class="sxs-lookup"><span data-stu-id="91762-126">In the logic app, type "office 365" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="91762-127">Seçin **Office 365 yaklaşan bir olay yakında başlatırken Outlook -**.</span><span class="sxs-lookup"><span data-stu-id="91762-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="91762-128">Bir bağlantı zaten varsa, bir takvim aşağı açılan listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="91762-128">If a connection already exists, then select a calendar from the drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="91762-129">Oturum açmak için istenirse, oturum bağlantısı oluşturmak için Ayrıntılar girin.</span><span class="sxs-lookup"><span data-stu-id="91762-129">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="91762-130">[Bağlantı oluşturmak](connectors-create-api-office365-outlook.md#create-the-connection) bu konudaki adımları listeler.</span><span class="sxs-lookup"><span data-stu-id="91762-130">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="91762-131">Takvim olay güncelleştirildiğinde bu örnekte, mantıksal uygulama çalışır.</span><span class="sxs-lookup"><span data-stu-id="91762-131">In this example, the logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="91762-132">Bu tetikleyici sonuçlarını görmek için bir kısa mesaj gönderir başka bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="91762-132">To see the results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="91762-133">Örneğin, Twilio ekleyin *ileti gönder* eylem bu metinleri, takvim olayının 15 dakika içinde başlatırken.</span><span class="sxs-lookup"><span data-stu-id="91762-133">For example, add the Twilio *Send message* action that texts you when the calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="91762-134">Seçin **Düzenle** düğmesine tıklayın ve ayarlama **sıklığı** ve **aralığı** değerleri.</span><span class="sxs-lookup"><span data-stu-id="91762-134">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="91762-135">Örneğin, 15 dakikada bir yoklamak için tetikleyicinin isterseniz, daha sonra ayarlamak **sıklığı** için **dakika**ve **aralığı** için **15**.</span><span class="sxs-lookup"><span data-stu-id="91762-135">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="91762-136">**Kaydet** değişikliklerinizi (sol üst köşesindeki araç).</span><span class="sxs-lookup"><span data-stu-id="91762-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="91762-137">Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="91762-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="91762-138">Bir eylem kullanın</span><span class="sxs-lookup"><span data-stu-id="91762-138">Use an action</span></span>
<span data-ttu-id="91762-139">Bir eylem, bir mantıksal uygulama içinde tanımlanan iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="91762-139">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="91762-140">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="91762-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="91762-141">Artı işaretini seçin.</span><span class="sxs-lookup"><span data-stu-id="91762-141">Select the plus sign.</span></span> <span data-ttu-id="91762-142">Birkaç seçeneğiniz bkz: **Eylem Ekle**, **bir koşul eklemek**, veya biri **daha fazla** seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="91762-142">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="91762-143">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="91762-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="91762-144">Metin kutusuna "kullanılabilir tüm eylemlerin bir listesini almak için office 365" yazın.</span><span class="sxs-lookup"><span data-stu-id="91762-144">In the text box, type “office 365” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="91762-145">Bizim örneğimizde seçin **Office 365 Outlook - kişi oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="91762-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="91762-146">Bir bağlantı zaten varsa, ardından **klasörü kimliği**, **verilen ad**ve diğer özellikleri:</span><span class="sxs-lookup"><span data-stu-id="91762-146">If a connection already exists, then choose the **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="91762-147">Bağlantı bilgilerini istenirse, bağlantı oluşturmak için ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="91762-147">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="91762-148">[Bağlantı oluşturmak](connectors-create-api-office365-outlook.md#create-the-connection) bu konuda bu özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="91762-148">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="91762-149">Bu örnekte, Office 365 Outlook içinde yeni bir kişi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="91762-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="91762-150">İlgili kişi oluşturmanız için başka bir tetikleyici çıktısını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="91762-150">You can use output from another trigger to create the contact.</span></span> <span data-ttu-id="91762-151">Örneğin, SalesForce ekleyin *bir nesne oluşturulduğunda* tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="91762-151">For example, add the SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="91762-152">Office 365 Outlook eklemek *kişi oluşturma* SalesForce alanları Office 365'te yeni yeni kişi oluşturmak için kullandığı eylem.</span><span class="sxs-lookup"><span data-stu-id="91762-152">Then add the Office 365 Outlook *Create contact* action that uses the SalesForce fields to create the new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="91762-153">**Kaydet** değişikliklerinizi (sol üst köşesindeki araç).</span><span class="sxs-lookup"><span data-stu-id="91762-153">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="91762-154">Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="91762-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="91762-155">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="91762-155">Connector-specific details</span></span>

<span data-ttu-id="91762-156">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="91762-156">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="91762-157">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="91762-157">Next Steps</span></span>
<span data-ttu-id="91762-158">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="91762-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="91762-159">Logic Apps diğer kullanılabilir bağlayıcılar keşfedin bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="91762-159">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

