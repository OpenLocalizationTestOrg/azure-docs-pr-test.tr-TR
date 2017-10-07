---
title: "Azure mantıksal uygulamalarınızı aaaUse hello kayma bağlayıcı | Microsoft Docs"
description: "Mantıksal uygulamalarınızı tooSlack Bağlan"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a><span data-ttu-id="458fd-103">Merhaba Slack Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="458fd-103">Get started with hello Slack connector</span></span>
<span data-ttu-id="458fd-104">Slack, ekibinizin tüm yazışmalarını anında aranabilecek ve gittiğiniz her yerden ulaşılabilecek bir yerde toplayan bir ekip iletişim aracıdır.</span><span class="sxs-lookup"><span data-stu-id="458fd-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="458fd-105">Bir mantıksal uygulama artık oluşturarak başlama; bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="458fd-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooslack"></a><span data-ttu-id="458fd-106">Bir bağlantı tooSlack oluşturma</span><span class="sxs-lookup"><span data-stu-id="458fd-106">Create a connection tooSlack</span></span>
<span data-ttu-id="458fd-107">toouse hello Slack bağlayıcı, önce oluşturduğunuz bir **bağlantı** sonra hello Ayrıntılar için bu özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="458fd-107">toouse hello Slack connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="458fd-108">Özellik</span><span class="sxs-lookup"><span data-stu-id="458fd-108">Property</span></span> | <span data-ttu-id="458fd-109">Gerekli</span><span class="sxs-lookup"><span data-stu-id="458fd-109">Required</span></span> | <span data-ttu-id="458fd-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="458fd-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="458fd-111">Belirteç</span><span class="sxs-lookup"><span data-stu-id="458fd-111">Token</span></span> |<span data-ttu-id="458fd-112">Evet</span><span class="sxs-lookup"><span data-stu-id="458fd-112">Yes</span></span> |<span data-ttu-id="458fd-113">Slack kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="458fd-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="458fd-114">Bu adımları toosign kayma ve hello kayma tam hello yapılandırmasını izleyin **bağlantı** mantığı uygulamanıza:</span><span class="sxs-lookup"><span data-stu-id="458fd-114">Follow these steps toosign into Slack, and complete hello configuration of hello Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="458fd-115">Seçin **yineleme**</span><span class="sxs-lookup"><span data-stu-id="458fd-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="458fd-116">Seçin bir **sıklığı** ve girin bir **aralığı**</span><span class="sxs-lookup"><span data-stu-id="458fd-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="458fd-117">Seçin **Eylem Ekle**</span><span class="sxs-lookup"><span data-stu-id="458fd-117">Select **Add an action**</span></span>  
   <span data-ttu-id="458fd-118">![Kayma yapılandırın][1]</span><span class="sxs-lookup"><span data-stu-id="458fd-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="458fd-119">Kayma hello arama kutusuna girin ve hello adında boşluk içeren tüm girişleri için hello arama tooreturn bekleyin</span><span class="sxs-lookup"><span data-stu-id="458fd-119">Enter Slack in hello search box and wait for hello search tooreturn all entries with Slack in hello name</span></span>
5. <span data-ttu-id="458fd-120">Seçin **Slack'e - posta iletisi**</span><span class="sxs-lookup"><span data-stu-id="458fd-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="458fd-121">Seçin **tooSlack içinde oturum**:</span><span class="sxs-lookup"><span data-stu-id="458fd-121">Select **Sign in tooSlack**:</span></span>  
   <span data-ttu-id="458fd-122">![Kayma yapılandırın][2]</span><span class="sxs-lookup"><span data-stu-id="458fd-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="458fd-123">Slack kimlik bilgileri toosign tooauthorize hello uygulamada sağlayın</span><span class="sxs-lookup"><span data-stu-id="458fd-123">Provide your Slack credentials toosign in tooauthorize hello  application</span></span>    
   ![Kayma yapılandırın][3]  
8. <span data-ttu-id="458fd-125">Yeniden yönlendirilen tooyour kuruluşunuzun oturum açma sayfasında olması.</span><span class="sxs-lookup"><span data-stu-id="458fd-125">You'll be redirected tooyour organization's Log in page.</span></span> <span data-ttu-id="458fd-126">**Yetki** Slack toointeract mantıksal uygulamanızı ile:</span><span class="sxs-lookup"><span data-stu-id="458fd-126">**Authorize** Slack toointeract with your logic app:</span></span>      
   <span data-ttu-id="458fd-127">![Kayma yapılandırın][5]</span><span class="sxs-lookup"><span data-stu-id="458fd-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="458fd-128">Hello yetkilendirme tamamlandıktan sonra yeniden yönlendirilen tooyour mantığı uygulama toocomplete olması, hello yapılandırarak **Slack - tüm iletileri Al** bölüm.</span><span class="sxs-lookup"><span data-stu-id="458fd-128">After hello authorization completes you'll be redirected tooyour logic app toocomplete it by configuring hello **Slack - Get all messages** section.</span></span> <span data-ttu-id="458fd-129">Diğer tetikleyiciler ve gereken eylemleri ekleyin.</span><span class="sxs-lookup"><span data-stu-id="458fd-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="458fd-130">![Kayma yapılandırın][6]</span><span class="sxs-lookup"><span data-stu-id="458fd-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="458fd-131">Seçerek çalışmanızı kaydedin **kaydetmek** hello menü çubuğunda yukarıdaki.</span><span class="sxs-lookup"><span data-stu-id="458fd-131">Save your work by selecting **Save** on hello menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="458fd-132">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="458fd-132">Connector-specific details</span></span>

<span data-ttu-id="458fd-133">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="458fd-133">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="458fd-134">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="458fd-134">More connectors</span></span>
<span data-ttu-id="458fd-135">Toohello dönün [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="458fd-135">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
