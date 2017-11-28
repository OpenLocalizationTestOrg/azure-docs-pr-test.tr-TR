---
title: aaaCreate B2B solutions - Azure Logic Apps | Microsoft Docs
description: "Merhaba Enterprise Integration Pack Merhaba B2B özelliklerini kullanarak logic apps içinde veri alma"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 20fc3722-6f8b-402f-b391-b84e9df6fcff
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8f01318a0415d81c37b216f9b991c060edec2053
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-data-in-logic-apps-with-hello-b2b-features-in-hello-enterprise-integration-pack"></a><span data-ttu-id="45c80-103">Logic apps hello Enterprise Integration Pack Merhaba B2B özellikleri ile veri alma</span><span class="sxs-lookup"><span data-stu-id="45c80-103">Receive data in logic apps with hello B2B features in hello Enterprise Integration Pack</span></span>

<span data-ttu-id="45c80-104">İş ortakları ve anlaşmaları olan bir tümleştirme hesap oluşturduktan sonra hazır toocreate iş toobusiness (B2B) iş akışı mantığı uygulamanızla hello için olduğunuz [Kurumsal tümleştirme paketi](logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="45c80-104">After you create an integration account that has partners and agreements, you are ready toocreate a business toobusiness (B2B) workflow for your logic app with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45c80-105">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="45c80-105">Prerequisites</span></span>

<span data-ttu-id="45c80-106">toouse hello AS2 ve X12 Eylemler, bir kurumsal tümleştirme hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="45c80-106">toouse hello AS2 and X12 actions, you must have an Enterprise Integration Account.</span></span> <span data-ttu-id="45c80-107">Bilgi [nasıl toocreate bir kurumsal tümleştirme hesap](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="45c80-107">Learn [how toocreate an Enterprise Integration Account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

## <a name="create-a-logic-app-with-b2b-connectors"></a><span data-ttu-id="45c80-108">İle B2B bağlayıcılar mantıksal uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="45c80-108">Create a logic app with B2B connectors</span></span>

<span data-ttu-id="45c80-109">Merhaba AS2 ve X12 kullanan bu adımları toocreate bir B2B mantıksal uygulama izleyin ticari ortak Eylemler tooreceive verileri:</span><span class="sxs-lookup"><span data-stu-id="45c80-109">Follow these steps toocreate a B2B logic app that uses hello AS2 and X12 actions tooreceive data from a trading partner:</span></span>

1. <span data-ttu-id="45c80-110">Ardından bir mantıksal uygulama oluşturma [uygulama tooyour tümleştirme hesabınızı bağlama](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="45c80-110">Create a logic app, then [link your app tooyour integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md).</span></span>

2. <span data-ttu-id="45c80-111">Ekleme bir **isteği - olduğunda bir HTTP isteği alındığında** tetikleyici tooyour mantıksal uygulama.</span><span class="sxs-lookup"><span data-stu-id="45c80-111">Add a **Request - When an HTTP request is received** trigger tooyour logic app.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/flatfile-1.png)

3. <span data-ttu-id="45c80-112">tooadd hello **kod çözme AS2** eylem, select **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="45c80-112">tooadd hello **Decode AS2** action, select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-2.png)

4. <span data-ttu-id="45c80-113">toofilter tüm eylemler toohello istediğiniz birini girin hello word **as2** hello arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="45c80-113">toofilter all actions toohello one that you want, enter hello word **as2** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-5.png)

5. <span data-ttu-id="45c80-114">Select hello **AS2 - kod çözme AS2 ileti** eylem.</span><span class="sxs-lookup"><span data-stu-id="45c80-114">Select hello **AS2 - Decode AS2 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-6.png)

6. <span data-ttu-id="45c80-115">Merhaba eklemek **gövde** giriş olarak toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="45c80-115">Add hello **Body** that you want toouse as input.</span></span> <span data-ttu-id="45c80-116">Bu örnekte, hello Tetikleyicileri mantıksal uygulama hello hello HTTP istek gövdesi seçin.</span><span class="sxs-lookup"><span data-stu-id="45c80-116">In this example, select hello body of hello HTTP request that triggers hello logic app.</span></span> <span data-ttu-id="45c80-117">Merhaba hello üstbilgilerinde girdi bir ifade girin veya **ÜSTBİLGİLERİ** alan:</span><span class="sxs-lookup"><span data-stu-id="45c80-117">Or enter an expression that inputs hello headers in hello **HEADERS** field:</span></span>

    <span data-ttu-id="45c80-118">@triggerOutputs() ['üst bilgileri']</span><span class="sxs-lookup"><span data-stu-id="45c80-118">@triggerOutputs()['headers']</span></span>

7. <span data-ttu-id="45c80-119">Gerekli hello eklemek **üstbilgileri** hello HTTP istek üst bilgilerinde bulabilirsiniz AS2 için.</span><span class="sxs-lookup"><span data-stu-id="45c80-119">Add hello required **Headers** for AS2, which you can find in hello HTTP request headers.</span></span> <span data-ttu-id="45c80-120">Bu örnekte, bu tetikleyici hello mantıksal uygulama hello üstbilgilerini hello HTTP isteğini seçin.</span><span class="sxs-lookup"><span data-stu-id="45c80-120">In this example, select hello headers of hello HTTP request that trigger hello logic app.</span></span>

8. <span data-ttu-id="45c80-121">Şimdi hello kod çözme X12 ileti eylemi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="45c80-121">Now add hello Decode X12 message action.</span></span> <span data-ttu-id="45c80-122">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="45c80-122">Select **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-9.png)

9. <span data-ttu-id="45c80-123">toofilter tüm eylemler toohello istediğiniz birini girin hello word **x12** hello arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="45c80-123">toofilter all actions toohello one that you want, enter hello word **x12** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-10.png)

10. <span data-ttu-id="45c80-124">Select hello **X12-X12 kod çözme ileti** eylem.</span><span class="sxs-lookup"><span data-stu-id="45c80-124">Select hello **X12 - Decode X12 message** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-as2message.png)

11. <span data-ttu-id="45c80-125">Şimdi hello giriş toothis eylem belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="45c80-125">Now you must specify hello input toothis action.</span></span> <span data-ttu-id="45c80-126">Bu giriş hello önceki AS2 eylemin hello çıktısını olabilir.</span><span class="sxs-lookup"><span data-stu-id="45c80-126">This input is hello output from hello previous AS2 action.</span></span>

    <span data-ttu-id="45c80-127">Merhaba gerçek ileti içerik bir JSON nesnesinde ve base64 ile kodlanmış, olduğundan, bir ifade hello giriş olarak belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="45c80-127">hello actual message content is in a JSON object and is base64 encoded, so you must specify an expression as hello input.</span></span> 
    <span data-ttu-id="45c80-128">Merhaba ifadesinde aşağıdaki hello girin **X12 DÜZ dosya iletisi tooDECODE** giriş alanı:</span><span class="sxs-lookup"><span data-stu-id="45c80-128">Enter hello following expression in hello **X12 FLAT FILE MESSAGE tooDECODE** input field:</span></span>
    
    <span data-ttu-id="45c80-129">@base64ToString(body('Decode_AS2_message')? ['AS2Message']? ['Content'])</span><span class="sxs-lookup"><span data-stu-id="45c80-129">@base64ToString(body('Decode_AS2_message')?['AS2Message']?['Content'])</span></span>

    <span data-ttu-id="45c80-130">Şimdi toodecode hello X12 veri öğeleri bir JSON nesnesinde çıkış ve iş ortağı ticaret hello alınan adımlar ekleyin.</span><span class="sxs-lookup"><span data-stu-id="45c80-130">Now add steps toodecode hello X12 data received from hello trading partner and output items in a JSON object.</span></span> 
    <span data-ttu-id="45c80-131">Veri hello toonotify hello iş ortağı alındı, hello bir HTTP yanıt uygulamada AS2 ileti değerlendirme bildirim (MDN) içeren bir yanıtı geri gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45c80-131">toonotify hello partner that hello data was received, you can send back a response containing hello AS2 Message Disposition Notification (MDN) in an HTTP Response Action.</span></span>

12. <span data-ttu-id="45c80-132">tooadd hello **yanıt** eylemi seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="45c80-132">tooadd hello **Response** action, choose **Add an action**.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-14.png)

13. <span data-ttu-id="45c80-133">toofilter tüm eylemler toohello istediğiniz birini girin hello word **yanıt** hello arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="45c80-133">toofilter all actions toohello one that you want, enter hello word **response** in hello search box.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-15.png)

14. <span data-ttu-id="45c80-134">Select hello **yanıt** eylem.</span><span class="sxs-lookup"><span data-stu-id="45c80-134">Select hello **Response** action.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-16.png)

15. <span data-ttu-id="45c80-135">tooaccess hello MDN hello hello çıktısından **kod çözme X12 ileti** eylem, kümesi hello yanıt **gövde** Bu ifade ile alan:</span><span class="sxs-lookup"><span data-stu-id="45c80-135">tooaccess hello MDN from hello output of hello **Decode X12 message** action, set hello response **BODY** field with this expression:</span></span>

    <span data-ttu-id="45c80-136">@base64ToString(body('Decode_AS2_message')? ['OutgoingMdn']? ['Content'])</span><span class="sxs-lookup"><span data-stu-id="45c80-136">@base64ToString(body('Decode_AS2_message')?['OutgoingMdn']?['Content'])</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/b2b-17.png)  

16. <span data-ttu-id="45c80-137">Çalışmanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="45c80-137">Save your work.</span></span>

    ![](./media/logic-apps-enterprise-integration-b2b/transform-5.png)  

<span data-ttu-id="45c80-138">Şimdi yapılır B2B mantıksal uygulamanızı ayarlama.</span><span class="sxs-lookup"><span data-stu-id="45c80-138">You are now done setting up your B2B logic app.</span></span> <span data-ttu-id="45c80-139">Gerçek dünya uygulamada toostore hello kodunu çözdü X12 isteyebilirsiniz satır iş kolu (LOB) uygulaması veya veri deposuna verileri.</span><span class="sxs-lookup"><span data-stu-id="45c80-139">In a real world application, you might want toostore hello decoded X12 data in a line-of-business (LOB) app or data store.</span></span> <span data-ttu-id="45c80-140">tooconnect kendi iş KOLU uygulamalarınızı ve mantıksal uygulamanızı bu API'leri kullanın, daha fazla eylemler ekleyebilir veya özel API'ları yazma.</span><span class="sxs-lookup"><span data-stu-id="45c80-140">tooconnect your own LOB apps and use these APIs in your logic app, you can add further actions or write custom APIs.</span></span>

## <a name="features-and-use-cases"></a><span data-ttu-id="45c80-141">Özellikleri ve kullanım örnekleri</span><span class="sxs-lookup"><span data-stu-id="45c80-141">Features and use cases</span></span>

* <span data-ttu-id="45c80-142">Merhaba AS2 ve X12 Eylemler kodlanacağını ve logic apps içinde endüstri standardı protokoller kullanarak ticaret ortakları arasında veri değişimi bırakın.</span><span class="sxs-lookup"><span data-stu-id="45c80-142">hello AS2 and X12 decode and encode actions let you exchange data between trading partners by using industry standard protocols in logic apps.</span></span>
* <span data-ttu-id="45c80-143">Ticari ortaklar tooexchange veriler ile veya olmadan birbirine AS2 ve X12 kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45c80-143">tooexchange data with trading partners, you can use AS2 and X12 with or without each other.</span></span>
* <span data-ttu-id="45c80-144">Hello B2B Eylemler iş ortakları ve anlaşmaları tümleştirme hesabınızı kolayca oluşturun ve bir mantıksal uygulama kullanmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="45c80-144">hello B2B actions help you create partners and agreements easily in your integration account and consume them in a logic app.</span></span>
* <span data-ttu-id="45c80-145">Mantıksal uygulamanızı diğer eylemler ile genişlettiğinizde, gönderebilir ve diğer uygulamalarla SalesForce gibi hizmetler arasında veri alırsınız.</span><span class="sxs-lookup"><span data-stu-id="45c80-145">When you extend your logic app with other actions, you can send and receive data between other apps and services like SalesForce.</span></span>

## <a name="learn-more"></a><span data-ttu-id="45c80-146">Daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="45c80-146">Learn more</span></span>
[<span data-ttu-id="45c80-147">Merhaba Enterprise Integration Pack hakkında daha fazla bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="45c80-147">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md)
