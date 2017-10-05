---
title: "SMTP Bağlayıcısı Azure Logic Apps içinde | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. E-posta göndermek için SMTP'ye bağlanın."
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
ms.openlocfilehash: 1cf96bbf8bd215d7ddb3c99860a5cb4e668be3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-smtp-connector"></a><span data-ttu-id="32579-104">SMTP Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="32579-104">Get started with the SMTP connector</span></span>
<span data-ttu-id="32579-105">E-posta göndermek için SMTP'ye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="32579-105">Connect to SMTP to send email.</span></span>

<span data-ttu-id="32579-106">Kullanılacak [tüm bağlayıcıların](apis-list.md), ilk mantıksal uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="32579-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="32579-107">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="32579-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-smtp"></a><span data-ttu-id="32579-108">SMTP Bağlan</span><span class="sxs-lookup"><span data-stu-id="32579-108">Connect to SMTP</span></span>
<span data-ttu-id="32579-109">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce ilk önce oluşturmanız gerekir bir *bağlantı* hizmet.</span><span class="sxs-lookup"><span data-stu-id="32579-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="32579-110">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="32579-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="32579-111">Örneğin, SMTP bağlanmak için önce bir SMTP gerekir *bağlantı*.</span><span class="sxs-lookup"><span data-stu-id="32579-111">For example, to connect to SMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="32579-112">Bir bağlantı oluşturmak için normalde, bağlandığınız hizmete erişmek için kullandığınız kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="32579-112">To create a connection, enter the credentials you normally use to access the service you connect to.</span></span> <span data-ttu-id="32579-113">Bu nedenle, SMTP örnekte, bağlantı adı, SMTP sunucu adresi ve SMTP bağlantı oluşturmak için kullanıcı oturum açma bilgileri için kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="32579-113">So, in the SMTP example, enter the credentials to your connection name, SMTP server address, and user login information to create the connection to SMTP.</span></span>  

### <a name="create-a-connection-to-smtp"></a><span data-ttu-id="32579-114">SMTP bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="32579-114">Create a connection to SMTP</span></span>
> [!INCLUDE [Steps to create a connection to SMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="32579-115">Bir SMTP tetikleyicisi kullanın</span><span class="sxs-lookup"><span data-stu-id="32579-115">Use an SMTP trigger</span></span>
<span data-ttu-id="32579-116">Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="32579-116">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="32579-117">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="32579-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="32579-118">Bu örnekte, SMTP kendi, tetikleyici olmadığından kullanacağız **bir nesne oluşturulduğunda Salesforce -** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="32579-118">In this example, because SMTP does not have a trigger of its own, we'll use the **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="32579-119">Salesforce'ta yeni bir nesne oluşturulduğunda, bu tetikleyici etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="32579-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="32579-120">Sağlayacak şekilde her bir yeni sağlama Salesforce içinde oluşturulur Bizim örneğimizde, bunu yaparız bir *e-posta Gönder* eylem oluşur oluşturulan yeni müşteri adayına ilişkin bir bildirim ile SMTP bağlayıcısı aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="32579-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via the SMTP connector with a notification of the new lead being created.</span></span>

1. <span data-ttu-id="32579-121">Girin *salesforce* arama kutusuna logic apps tasarımcısında seçip **bir nesne oluşturulduğunda Salesforce -** tetikleyici.</span><span class="sxs-lookup"><span data-stu-id="32579-121">Enter *salesforce* in the search box on the logic apps designer then select the **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="32579-122">**Bir nesne oluşturulduğunda** denetim görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="32579-122">The **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="32579-123">Seçin **nesne türü** seçip *neden* nesneleri listesinde.</span><span class="sxs-lookup"><span data-stu-id="32579-123">Select the **Object Type** then select *Lead* from the list of objects.</span></span> <span data-ttu-id="32579-124">Bu adımda, her bir yeni sağlama Salesforce'ta oluşturulduğunda, mantıksal uygulamanızı uyarır tetikleyici oluşturmakta olduğunuz belirten.</span><span class="sxs-lookup"><span data-stu-id="32579-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="32579-125">Tetikleyici oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="32579-125">The trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="32579-126">SMTP eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="32579-126">Use an SMTP action</span></span>
<span data-ttu-id="32579-127">Bir eylem, bir mantıksal uygulama içinde tanımlanan iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="32579-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="32579-128">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="32579-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="32579-129">Tetikleyici eklenen, yeni sağlama Salesforce'ta oluşturulduğunda gerçekleşir bir SMTP eylem eklemek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="32579-129">Now that the trigger has been added, follow these steps to add an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="32579-130">Seçin **+ yeni adım** yeni bir sağlama oluşturulduğunda, almak istediğiniz eylem eklemek için.</span><span class="sxs-lookup"><span data-stu-id="32579-130">Select **+ New Step** to add the action you would like to take when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="32579-131">Seçin **Eylem Ekle**.</span><span class="sxs-lookup"><span data-stu-id="32579-131">Select **Add an action**.</span></span> <span data-ttu-id="32579-132">Bu açılır, herhangi bir işlem arayabileceğiniz arama kutusu yapmak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="32579-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="32579-133">Girin *smtp* SMTP ilgili eylemler için aranacak.</span><span class="sxs-lookup"><span data-stu-id="32579-133">Enter *smtp* to search for actions related to SMTP.</span></span>  
4. <span data-ttu-id="32579-134">Seçin **SMTP - e-posta Gönder** ne zaman gerçekleştirilecek eylemi yeni sağlama oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="32579-134">Select **SMTP - Send Email** as the action to take when the new lead is created.</span></span> <span data-ttu-id="32579-135">Eylem denetim bloğu açılır.</span><span class="sxs-lookup"><span data-stu-id="32579-135">The action control block opens.</span></span> <span data-ttu-id="32579-136">Bunu daha önceden yapmadıysanız, smtp Tasarımcı bloğu içindeki bağlantı gerekir.</span><span class="sxs-lookup"><span data-stu-id="32579-136">You will have to establish your smtp connection in the designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="32579-137">İstenen e-posta bilgilerinizi giriş **SMTP - e-posta Gönder** bloğu.</span><span class="sxs-lookup"><span data-stu-id="32579-137">Input your desired email information in the **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="32579-138">İş akışınızı etkinleştirmek için çalışmanızı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="32579-138">Save your work in order to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="32579-139">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="32579-139">Connector-specific details</span></span>

<span data-ttu-id="32579-140">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="32579-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="32579-141">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="32579-141">More connectors</span></span>
<span data-ttu-id="32579-142">Geri dönerek [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="32579-142">Go back to the [APIs list](apis-list.md).</span></span>