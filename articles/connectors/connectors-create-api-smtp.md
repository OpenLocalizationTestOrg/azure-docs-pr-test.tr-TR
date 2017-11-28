---
title: "Azure mantıksal uygulamaları aaaSMTP Bağlayıcısı | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. TooSMTP toosend e-posta bağlayın."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a><span data-ttu-id="d437f-104">Merhaba SMTP Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="d437f-104">Get started with hello SMTP connector</span></span>
<span data-ttu-id="d437f-105">TooSMTP toosend e-posta bağlayın.</span><span class="sxs-lookup"><span data-stu-id="d437f-105">Connect tooSMTP toosend email.</span></span>

<span data-ttu-id="d437f-106">toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir.</span><span class="sxs-lookup"><span data-stu-id="d437f-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="d437f-107">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d437f-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosmtp"></a><span data-ttu-id="d437f-108">TooSMTP Bağlan</span><span class="sxs-lookup"><span data-stu-id="d437f-108">Connect tooSMTP</span></span>
<span data-ttu-id="d437f-109">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce toocreate ilk gerekiyor bir *bağlantı* toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="d437f-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="d437f-110">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="d437f-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="d437f-111">Örneğin, tooconnect tooSMTP önce bir SMTP gerekir *bağlantı*.</span><span class="sxs-lookup"><span data-stu-id="d437f-111">For example, tooconnect tooSMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="d437f-112">toocreate bir bağlantı için connect tooaccess hello hizmeti normalde kullandığınız hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="d437f-112">toocreate a connection, enter hello credentials you normally use tooaccess hello service you connect to.</span></span> <span data-ttu-id="d437f-113">Bu nedenle, hello SMTP örnekte hello kimlik bilgilerini tooyour bağlantı adı, SMTP sunucu adresleri ve kullanıcı oturum açma bilgileri toocreate hello bağlantı tooSMTP girin.</span><span class="sxs-lookup"><span data-stu-id="d437f-113">So, in hello SMTP example, enter hello credentials tooyour connection name, SMTP server address, and user login information toocreate hello connection tooSMTP.</span></span>  

### <a name="create-a-connection-toosmtp"></a><span data-ttu-id="d437f-114">Bir bağlantı tooSMTP oluşturma</span><span class="sxs-lookup"><span data-stu-id="d437f-114">Create a connection tooSMTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="d437f-115">Bir SMTP tetikleyicisi kullanın</span><span class="sxs-lookup"><span data-stu-id="d437f-115">Use an SMTP trigger</span></span>
<span data-ttu-id="d437f-116">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="d437f-116">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="d437f-117">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d437f-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="d437f-118">SMTP kendi, tetikleyici olmadığından bu örnekte, hello kullanacağız **bir nesne oluşturulduğunda Salesforce -** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="d437f-118">In this example, because SMTP does not have a trigger of its own, we'll use hello **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="d437f-119">Salesforce'ta yeni bir nesne oluşturulduğunda, bu tetikleyici etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="d437f-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="d437f-120">Sağlayacak şekilde her bir yeni sağlama Salesforce içinde oluşturulur Bizim örneğimizde, bunu yaparız bir *e-posta Gönder* eylem oluşur oluşturulmakta hello yeni müşteri adayına ilişkin bir bildirim ile Merhaba SMTP bağlayıcısı aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="d437f-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via hello SMTP connector with a notification of hello new lead being created.</span></span>

1. <span data-ttu-id="d437f-121">Girin *salesforce* hello arama kutusuna hello logic apps tasarımcısında hello seçip **bir nesne oluşturulduğunda Salesforce -** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="d437f-121">Enter *salesforce* in hello search box on hello logic apps designer then select hello **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="d437f-122">Merhaba **bir nesne oluşturulduğunda** denetim görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="d437f-122">hello **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="d437f-123">Select hello **nesne türü** seçip *neden* nesneleri hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="d437f-123">Select hello **Object Type** then select *Lead* from hello list of objects.</span></span> <span data-ttu-id="d437f-124">Bu adımda, her bir yeni sağlama Salesforce'ta oluşturulduğunda, mantıksal uygulamanızı uyarır tetikleyici oluşturmakta olduğunuz belirten.</span><span class="sxs-lookup"><span data-stu-id="d437f-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="d437f-125">Merhaba tetikleyici oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="d437f-125">hello trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="d437f-126">SMTP eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="d437f-126">Use an SMTP action</span></span>
<span data-ttu-id="d437f-127">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="d437f-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="d437f-128">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="d437f-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="d437f-129">Merhaba tetikleyici eklendi, yeni sağlama Salesforce'ta oluşturulduğunda gerçekleşir bu adımları tooadd SMTP eylemi izleyin.</span><span class="sxs-lookup"><span data-stu-id="d437f-129">Now that hello trigger has been added, follow these steps tooadd an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="d437f-130">Seçin **+ yeni adım** tooadd hello eylem istediğinizi tootake yeni bir sağlama oluşturulduğunda.</span><span class="sxs-lookup"><span data-stu-id="d437f-130">Select **+ New Step** tooadd hello action you would like tootake when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="d437f-131">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="d437f-131">Select **Add an action**.</span></span> <span data-ttu-id="d437f-132">Bu açılır hello arama kutusu için herhangi bir işlem, arayabileceğiniz tootake ister.</span><span class="sxs-lookup"><span data-stu-id="d437f-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="d437f-133">Girin *smtp* Eylemler ilgili tooSMTP toosearch.</span><span class="sxs-lookup"><span data-stu-id="d437f-133">Enter *smtp* toosearch for actions related tooSMTP.</span></span>  
4. <span data-ttu-id="d437f-134">Seçin **SMTP - e-posta Gönder** hello yeni sağlama oluşturulduğunda eylem tootake hello gibi.</span><span class="sxs-lookup"><span data-stu-id="d437f-134">Select **SMTP - Send Email** as hello action tootake when hello new lead is created.</span></span> <span data-ttu-id="d437f-135">Merhaba eylem denetim bloğu açılır.</span><span class="sxs-lookup"><span data-stu-id="d437f-135">hello action control block opens.</span></span> <span data-ttu-id="d437f-136">Daha önce yapmadıysanız seçerseniz, smtp bağlantı tooestablish hello Tasarımcı bloğunda gerekir.</span><span class="sxs-lookup"><span data-stu-id="d437f-136">You will have tooestablish your smtp connection in hello designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="d437f-137">İstenen e-posta bilgilerinizi hello giriş **SMTP - e-posta Gönder** bloğu.</span><span class="sxs-lookup"><span data-stu-id="d437f-137">Input your desired email information in hello **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="d437f-138">İş akışınızı sipariş tooactivate kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d437f-138">Save your work in order tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="d437f-139">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="d437f-139">Connector-specific details</span></span>

<span data-ttu-id="d437f-140">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="d437f-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="d437f-141">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="d437f-141">More connectors</span></span>
<span data-ttu-id="d437f-142">Toohello dönün [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="d437f-142">Go back toohello [APIs list](apis-list.md).</span></span>
