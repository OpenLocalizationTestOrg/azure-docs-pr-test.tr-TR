---
title: "Logic Apps içinde OneDrive bağlayıcısını ekleyin | Microsoft Docs"
description: "REST API parametreleri OneDrive bağlayıcısıyla genel bakış"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 63bd33bf4e09b98aa53dcfec9fcc4a0109204952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-onedrive-connector"></a><span data-ttu-id="b14e2-103">OneDrive Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b14e2-103">Get started with the OneDrive connector</span></span>
<span data-ttu-id="b14e2-104">Karşıya yükleme de dahil olmak üzere dosyalarınızı yönetmek için OneDrive bağlanmak, almak için dosyaları ve diğer silin.</span><span class="sxs-lookup"><span data-stu-id="b14e2-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="b14e2-105">OneDrive ile:</span><span class="sxs-lookup"><span data-stu-id="b14e2-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="b14e2-106">Onedrive'daki dosyaları depolayarak, iş akışı oluşturma veya varolan dosyaları OneDrive güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="b14e2-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="b14e2-107">Bir dosya oluşturulduğunda veya OneDrive'ınıza içinde güncelleştirildiğinde iş akışını başlatmak için Tetikleyiciler kullanın.</span><span class="sxs-lookup"><span data-stu-id="b14e2-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="b14e2-108">Eylemler bir dosya oluşturun ve bir dosyayı silmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="b14e2-108">Use actions to create a file, delete a file, and more.</span></span> <span data-ttu-id="b14e2-109">Örneğin, yeni Office 365 e-posta eki (tetikleyici) alındığında, OneDrive (bir eylem) yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b14e2-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="b14e2-110">Bu konuda, bir mantıksal uygulama OneDrive Bağlayıcısı'nı kullanmayı gösterir ve ayrıca tetikleyiciler ve eylemler listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="b14e2-110">This topic shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span></span>

<span data-ttu-id="b14e2-111">Logic Apps hakkında daha fazla bilgi için bkz: [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b14e2-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-onedrive"></a><span data-ttu-id="b14e2-112">OneDrive Bağlan</span><span class="sxs-lookup"><span data-stu-id="b14e2-112">Connect to OneDrive</span></span>
<span data-ttu-id="b14e2-113">Mantıksal uygulamanızı herhangi bir hizmete erişebilmesi için önce oluşturduğunuz bir *bağlantı* hizmet.</span><span class="sxs-lookup"><span data-stu-id="b14e2-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="b14e2-114">Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b14e2-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="b14e2-115">Örneğin, OneDrive bağlanmak için önce bir OneDrive gerekir *bağlantı*.</span><span class="sxs-lookup"><span data-stu-id="b14e2-115">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="b14e2-116">Bir bağlantı oluşturmak için normalde bağlanmak istediğiniz hizmete erişmek için kullandığınız kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="b14e2-116">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="b14e2-117">Bu nedenle, OneDrive ile bağlantı oluşturmak için OneDrive hesabınıza kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="b14e2-117">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="b14e2-118">Bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b14e2-118">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to OneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="b14e2-119">Bir tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="b14e2-119">Use a trigger</span></span>
<span data-ttu-id="b14e2-120">Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="b14e2-120">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="b14e2-121">Tetikleyiciler "hizmet bir aralığı ve istediğiniz sıklığı yoklama".</span><span class="sxs-lookup"><span data-stu-id="b14e2-121">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="b14e2-122">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b14e2-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="b14e2-123">Mantıksal uygulama "onedrive" Tetikleyiciler listesini almak için aşağıdakileri yazın:</span><span class="sxs-lookup"><span data-stu-id="b14e2-123">In the logic app, type "onedrive" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="b14e2-124">Seçin **bir dosya değiştirildiği**.</span><span class="sxs-lookup"><span data-stu-id="b14e2-124">Select **When a file is modified**.</span></span> <span data-ttu-id="b14e2-125">Bir bağlantı zaten varsa, bir klasör seçmek için seçiciyi Göster düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b14e2-125">If a connection already exists, then select the Show Picker button to select a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="b14e2-126">Oturum açmak için istenirse, oturum bağlantısı oluşturmak için Ayrıntılar girin.</span><span class="sxs-lookup"><span data-stu-id="b14e2-126">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="b14e2-127">[Bağlantı oluşturmak](connectors-create-api-onedrive.md#create-the-connection) bu konudaki adımları listeler.</span><span class="sxs-lookup"><span data-stu-id="b14e2-127">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b14e2-128">Bu örnekte, mantıksal uygulama güncelleştirilir seçtiğiniz klasöründe bir dosya açıldığında çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="b14e2-128">In this example, the logic app runs when a file in the folder you choose is updated.</span></span> <span data-ttu-id="b14e2-129">Bu tetikleyici sonuçlarını görmek için bir e-posta gönderir başka bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b14e2-129">To see the results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="b14e2-130">Örneğin, Office 365 Outlook ekleme *bir e-posta Gönder* bir dosya güncelleştirildiğinde, e-postalar eylem.</span><span class="sxs-lookup"><span data-stu-id="b14e2-130">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="b14e2-131">Seçin **Düzenle** düğmesine tıklayın ve ayarlama **sıklığı** ve **aralığı** değerleri.</span><span class="sxs-lookup"><span data-stu-id="b14e2-131">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="b14e2-132">Örneğin, 15 dakikada bir yoklamak için tetikleyicinin isterseniz, daha sonra ayarlamak **sıklığı** için **dakika**ve **aralığı** için **15**.</span><span class="sxs-lookup"><span data-stu-id="b14e2-132">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="b14e2-133">**Kaydet** değişikliklerinizi (sol üst köşesindeki araç).</span><span class="sxs-lookup"><span data-stu-id="b14e2-133">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="b14e2-134">Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b14e2-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="b14e2-135">Bir eylem kullanın</span><span class="sxs-lookup"><span data-stu-id="b14e2-135">Use an action</span></span>
<span data-ttu-id="b14e2-136">Bir eylem, bir mantıksal uygulama içinde tanımlanan iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="b14e2-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="b14e2-137">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b14e2-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="b14e2-138">Artı işaretini seçin.</span><span class="sxs-lookup"><span data-stu-id="b14e2-138">Select the plus sign.</span></span> <span data-ttu-id="b14e2-139">Birkaç seçeneğiniz bkz: **Eylem Ekle**, **bir koşul eklemek**, veya biri **daha fazla** seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="b14e2-139">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="b14e2-140">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="b14e2-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="b14e2-141">Metin kutusuna, kullanılabilir tüm eylemlerin bir listesini almak için "onedrive" yazın.</span><span class="sxs-lookup"><span data-stu-id="b14e2-141">In the text box, type “onedrive” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="b14e2-142">Bizim örneğimizde seçin **OneDrive - dosyası oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="b14e2-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="b14e2-143">Bir bağlantı zaten varsa, ardından **klasör yolu** dosya yerleştirilecek girin **dosya adı**ve seçin **dosya içeriği** istediğiniz:</span><span class="sxs-lookup"><span data-stu-id="b14e2-143">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="b14e2-144">Bağlantı bilgilerini istenirse, bağlantı oluşturmak için ayrıntılarını girin.</span><span class="sxs-lookup"><span data-stu-id="b14e2-144">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="b14e2-145">[Bağlantı oluşturmak](connectors-create-api-onedrive.md#create-the-connection) bu konuda bu özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="b14e2-145">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="b14e2-146">Bu örnekte, OneDrive klasöründe yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b14e2-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="b14e2-147">Başka bir tetikleyici çıktısını OneDrive dosyası oluşturmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b14e2-147">You can use output from another trigger to create the OneDrive file.</span></span> <span data-ttu-id="b14e2-148">Örneğin, Office 365 Outlook ekleme *yeni bir e-posta geldiğinde* tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="b14e2-148">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="b14e2-149">OneDrive ekleme *dosyası oluştur* Content-Type ve ekleri kullandığı eylem Onedrive'da yeni dosyası oluşturmak için bir ForEach içindeki alanları.</span><span class="sxs-lookup"><span data-stu-id="b14e2-149">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="b14e2-150">**Kaydet** değişikliklerinizi (sol üst köşesindeki araç).</span><span class="sxs-lookup"><span data-stu-id="b14e2-150">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="b14e2-151">Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b14e2-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="b14e2-152">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="b14e2-152">Connector-specific details</span></span>

<span data-ttu-id="b14e2-153">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="b14e2-153">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="b14e2-154">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="b14e2-154">More connectors</span></span>
<span data-ttu-id="b14e2-155">Geri dönerek [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b14e2-155">Go back to the [APIs list](apis-list.md).</span></span>