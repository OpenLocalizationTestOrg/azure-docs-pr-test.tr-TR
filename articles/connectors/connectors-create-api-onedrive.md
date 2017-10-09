---
title: "Mantıksal uygulamalarınızı aaaAdd hello OneDrive Bağlayıcısı | Microsoft Docs"
description: "REST API parametrelerle hello OneDrive bağlayıcı genel bakış"
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
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a><span data-ttu-id="6ba46-103">Merhaba OneDrive Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6ba46-103">Get started with hello OneDrive connector</span></span>
<span data-ttu-id="6ba46-104">TooOneDrive toomanage karşıya yükleme, get, dosyaları silin ve daha fazlası da dahil olmak üzere dosyalarınızı bağlayın.</span><span class="sxs-lookup"><span data-stu-id="6ba46-104">Connect tooOneDrive toomanage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="6ba46-105">OneDrive ile:</span><span class="sxs-lookup"><span data-stu-id="6ba46-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="6ba46-106">Onedrive'daki dosyaları depolayarak, iş akışı oluşturma veya varolan dosyaları OneDrive güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6ba46-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="6ba46-107">Bir dosya oluşturulduğunda veya OneDrive'ınıza içinde güncelleştirildiğinde kullanım toostart, iş akışını tetikler.</span><span class="sxs-lookup"><span data-stu-id="6ba46-107">Use triggers toostart your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="6ba46-108">Eylemler toocreate bir dosyası kullanmak, bir dosya ve daha fazlasını silin.</span><span class="sxs-lookup"><span data-stu-id="6ba46-108">Use actions toocreate a file, delete a file, and more.</span></span> <span data-ttu-id="6ba46-109">Örneğin, yeni Office 365 e-posta eki (tetikleyici) alındığında, OneDrive (bir eylem) yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6ba46-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="6ba46-110">Bu konuda nasıl toouse hello bir mantıksal uygulama OneDrive Bağlayıcısı gösterir ve ayrıca listeleri tetikleyiciler ve Eylemler hello.</span><span class="sxs-lookup"><span data-stu-id="6ba46-110">This topic shows you how toouse hello OneDrive connector in a logic app, and also lists hello triggers and actions.</span></span>

<span data-ttu-id="6ba46-111">Logic Apps hakkında daha fazla toolearn bkz [logic apps nedir](../logic-apps/logic-apps-what-are-logic-apps.md) ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6ba46-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooonedrive"></a><span data-ttu-id="6ba46-112">TooOneDrive Bağlan</span><span class="sxs-lookup"><span data-stu-id="6ba46-112">Connect tooOneDrive</span></span>
<span data-ttu-id="6ba46-113">Mantıksal uygulamanızı herhangi bir hizmete erişebilmesi için önce oluşturduğunuz bir *bağlantı* toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="6ba46-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="6ba46-114">Bağlantı bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ba46-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="6ba46-115">Örneğin, tooconnect tooOneDrive önce bir OneDrive gerekir *bağlantı*.</span><span class="sxs-lookup"><span data-stu-id="6ba46-115">For example, tooconnect tooOneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="6ba46-116">toocreate bir bağlantı için tooconnect istediğiniz tooaccess hello hizmet normalde kullandığınız hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="6ba46-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="6ba46-117">Bu nedenle, OneDrive ile Merhaba kimlik bilgilerini tooyour OneDrive hesabı toocreate hello bağlantısı girin.</span><span class="sxs-lookup"><span data-stu-id="6ba46-117">So, with OneDrive, enter hello credentials tooyour OneDrive account  toocreate hello connection.</span></span>

### <a name="create-hello-connection"></a><span data-ttu-id="6ba46-118">Merhaba bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="6ba46-118">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="6ba46-119">Bir tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="6ba46-119">Use a trigger</span></span>
<span data-ttu-id="6ba46-120">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="6ba46-120">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="6ba46-121">Tetikleyiciler "Merhaba hizmet bir aralığı ve istediğiniz sıklığı yoklama".</span><span class="sxs-lookup"><span data-stu-id="6ba46-121">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="6ba46-122">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="6ba46-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="6ba46-123">Merhaba mantıksal uygulama içinde "onedrive" tooget hello Tetikleyicileri listesini yazın:</span><span class="sxs-lookup"><span data-stu-id="6ba46-123">In hello logic app, type "onedrive" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="6ba46-124">Seçin **bir dosya değiştirildiği**.</span><span class="sxs-lookup"><span data-stu-id="6ba46-124">Select **When a file is modified**.</span></span> <span data-ttu-id="6ba46-125">Bir bağlantı zaten varsa, hello Seçici Göster düğmesini tooselect bir klasör seçin.</span><span class="sxs-lookup"><span data-stu-id="6ba46-125">If a connection already exists, then select hello Show Picker button tooselect a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="6ba46-126">İçinde istendiğinde toosign varsa, hello oturum ayrıntıları toocreate hello bağlantısında girin.</span><span class="sxs-lookup"><span data-stu-id="6ba46-126">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="6ba46-127">[Merhaba bağlantı oluşturmak](connectors-create-api-onedrive.md#create-the-connection) bu konudaki hello adımlar listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="6ba46-127">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="6ba46-128">Bu örnekte, hello mantıksal uygulama güncelleştirilir seçtiğiniz hello klasöründe bir dosya açıldığında çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="6ba46-128">In this example, hello logic app runs when a file in hello folder you choose is updated.</span></span> <span data-ttu-id="6ba46-129">Bu tetikleyici toosee hello sonuçlarını bir e-posta gönderir başka bir eylem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6ba46-129">toosee hello results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="6ba46-130">Örneğin, Office 365 Outlook hello ekleyin *bir e-posta Gönder* bir dosya güncelleştirildiğinde, e-postalar eylem.</span><span class="sxs-lookup"><span data-stu-id="6ba46-130">For example, add hello Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="6ba46-131">Select hello **Düzenle** düğmesine tıklayın ve ayarlama hello **sıklığı** ve **aralığı** değerleri.</span><span class="sxs-lookup"><span data-stu-id="6ba46-131">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="6ba46-132">Örneğin, 15 dakikada bir hello tetikleyici toopoll istiyorsanız, ardından hello ayarlayın **sıklığı** çok**Minute**ve kümesi hello **aralığı** çok**15**.</span><span class="sxs-lookup"><span data-stu-id="6ba46-132">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="6ba46-133">**Kaydet** değişikliklerinizi (sol üst köşesindeki hello araç).</span><span class="sxs-lookup"><span data-stu-id="6ba46-133">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="6ba46-134">Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="6ba46-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="6ba46-135">Bir eylem kullanın</span><span class="sxs-lookup"><span data-stu-id="6ba46-135">Use an action</span></span>
<span data-ttu-id="6ba46-136">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="6ba46-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="6ba46-137">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="6ba46-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="6ba46-138">Merhaba artı işaretini seçin.</span><span class="sxs-lookup"><span data-stu-id="6ba46-138">Select hello plus sign.</span></span> <span data-ttu-id="6ba46-139">Birkaç seçeneğiniz bkz: **Eylem Ekle**, **bir koşul eklemek**, veya hello **daha fazla** seçenekleri.</span><span class="sxs-lookup"><span data-stu-id="6ba46-139">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="6ba46-140">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="6ba46-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="6ba46-141">Merhaba metin kutusuna "onedrive" tooget tüm hello kullanılabilir eylemlerin bir listesini yazın.</span><span class="sxs-lookup"><span data-stu-id="6ba46-141">In hello text box, type “onedrive” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="6ba46-142">Bizim örneğimizde seçin **OneDrive - dosyası oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="6ba46-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="6ba46-143">Bir bağlantı zaten varsa, hello seçin **klasör yolu** tooput hello dosya, hello girin **dosya adı**ve hello seçin **dosya içeriği** istediğiniz:</span><span class="sxs-lookup"><span data-stu-id="6ba46-143">If a connection already exists, then select hello **Folder Path** tooput hello file, enter hello **File Name**, and choose hello **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="6ba46-144">Merhaba bağlantı bilgilerini istenirse, hello ayrıntıları toocreate hello bağlantısı girin.</span><span class="sxs-lookup"><span data-stu-id="6ba46-144">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="6ba46-145">[Merhaba bağlantı oluşturmak](connectors-create-api-onedrive.md#create-the-connection) bu konuda bu özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="6ba46-145">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="6ba46-146">Bu örnekte, OneDrive klasöründe yeni bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6ba46-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="6ba46-147">Başka bir tetikleyici toocreate hello OneDrive dosyasından çıkış kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ba46-147">You can use output from another trigger toocreate hello OneDrive file.</span></span> <span data-ttu-id="6ba46-148">Örneğin, Office 365 Outlook hello ekleyin *yeni bir e-posta geldiğinde* tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="6ba46-148">For example, add hello Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="6ba46-149">Merhaba OneDrive ekleme *dosyası oluştur* ForEach toocreate hello yeni bir dosyada OneDrive içinde hello ekler ve Content-Type alanları kullanan eylem.</span><span class="sxs-lookup"><span data-stu-id="6ba46-149">Then add hello OneDrive *Create file* action that uses hello Attachments and Content-Type fields within a ForEach toocreate hello new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="6ba46-150">**Kaydet** değişikliklerinizi (sol üst köşesindeki hello araç).</span><span class="sxs-lookup"><span data-stu-id="6ba46-150">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="6ba46-151">Mantıksal uygulamanızı kaydedilir ve otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="6ba46-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="6ba46-152">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="6ba46-152">Connector-specific details</span></span>

<span data-ttu-id="6ba46-153">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="6ba46-153">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="6ba46-154">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="6ba46-154">More connectors</span></span>
<span data-ttu-id="6ba46-155">Toohello dönün [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="6ba46-155">Go back toohello [APIs list](apis-list.md).</span></span>
