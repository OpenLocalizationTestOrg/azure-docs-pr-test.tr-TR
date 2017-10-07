---
title: "aaaUse hello Logic Apps içinde SharePoint sunucusu Bağlayıcısı | Microsoft Docs"
description: "Merhaba hello SharePoint sunucusu Bağlayıcısı Logic apps kullanmaya başlama"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a><span data-ttu-id="6b8e1-103">Merhaba SharePoint Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6b8e1-103">Get started with hello SharePoint connector</span></span>
<span data-ttu-id="6b8e1-104">Merhaba SharePoint bağlayıcı SharePoint'te bir şekilde toowork listeleriyle sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b8e1-104">hello SharePoint Connector provides an way toowork with Lists on SharePoint.</span></span>

<span data-ttu-id="6b8e1-105">Bir mantıksal uygulama oluşturarak başlama; bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="6b8e1-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toosharepoint"></a><span data-ttu-id="6b8e1-106">Bir bağlantı tooSharePoint oluşturma</span><span class="sxs-lookup"><span data-stu-id="6b8e1-106">Create a connection tooSharePoint</span></span>
<span data-ttu-id="6b8e1-107">toouse Merhaba SharePoint bağlayıcı, önce oluşturduğunuz bir **bağlantı** sonra hello Ayrıntılar için bu özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="6b8e1-107">toouse hello SharePoint Connector , you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="6b8e1-108">Özellik</span><span class="sxs-lookup"><span data-stu-id="6b8e1-108">Property</span></span> | <span data-ttu-id="6b8e1-109">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6b8e1-109">Required</span></span> | <span data-ttu-id="6b8e1-110">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6b8e1-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="6b8e1-111">Belirteç</span><span class="sxs-lookup"><span data-stu-id="6b8e1-111">Token</span></span> |<span data-ttu-id="6b8e1-112">Evet</span><span class="sxs-lookup"><span data-stu-id="6b8e1-112">Yes</span></span> |<span data-ttu-id="6b8e1-113">SharePoint kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="6b8e1-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="6b8e1-114">tooconnect çok**SharePoint**, kimlik (kullanıcı adı ve parola, akıllı kart kimlik bilgileri, vb.) tooSharePoint girin.</span><span class="sxs-lookup"><span data-stu-id="6b8e1-114">tooconnect too**SharePoint**, enter your identity (username and password, smart card credentials, etc.) tooSharePoint.</span></span> <span data-ttu-id="6b8e1-115">Kimlik doğruladınız sonra mantıksal uygulamanızı toouse hello SharePoint bağlayıcı devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b8e1-115">Once you've been authenticated, you can proceed toouse hello SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="6b8e1-116">Merhaba Tasarımcısı mantıksal uygulamanızı karşın, bu adımları toosign SharePoint toocreate hello bağlantısına takip **bağlantı** mantıksal uygulamanızı kullanmak için:</span><span class="sxs-lookup"><span data-stu-id="6b8e1-116">While on hello designer of your logic app, follow these steps toosign into SharePoint toocreate hello connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="6b8e1-117">SharePoint hello arama kutusuna girin ve SharePoint ile tüm girişleri hello adında hello arama tooreturn için bekleyin:</span><span class="sxs-lookup"><span data-stu-id="6b8e1-117">Enter SharePoint in hello search box and wait for hello search tooreturn all entries with SharePoint in hello name:</span></span>   
   ![SharePoint'i yapılandırma][1]  
2. <span data-ttu-id="6b8e1-119">Seçin **bir dosya oluşturulduğunda SharePoint -**</span><span class="sxs-lookup"><span data-stu-id="6b8e1-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="6b8e1-120">Seçin **tooSharePoint içinde oturum**:</span><span class="sxs-lookup"><span data-stu-id="6b8e1-120">Select **Sign in tooSharePoint**:</span></span>   
   <span data-ttu-id="6b8e1-121">![SharePoint'i yapılandırma][2]</span><span class="sxs-lookup"><span data-stu-id="6b8e1-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="6b8e1-122">SharePoint ile SharePoint kimlik bilgileri toosign tooauthenticate içinde sağlayın</span><span class="sxs-lookup"><span data-stu-id="6b8e1-122">Provide your SharePoint credentials toosign in tooauthenticate with SharePoint</span></span>   
   ![SharePoint'i yapılandırma][3]     
5. <span data-ttu-id="6b8e1-124">Merhaba kimlik doğrulama tamamlandıktan sonra yeniden yönlendirilen tooyour mantığı uygulama toocomplete olacaktır, SharePoint yapılandırarak **bir dosya oluşturulduğunda** iletişim.</span><span class="sxs-lookup"><span data-stu-id="6b8e1-124">After hello authentication completes you'll be redirected tooyour logic app toocomplete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="6b8e1-125">![SharePoint'i yapılandırma][4]</span><span class="sxs-lookup"><span data-stu-id="6b8e1-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="6b8e1-126">Daha sonra diğer tetikleyiciler ve Eylemler mantıksal uygulamanızı toocomplete gerektiğini de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b8e1-126">You can then add other triggers and actions that you need toocomplete your logic app.</span></span>   
7. <span data-ttu-id="6b8e1-127">Seçerek çalışmanızı kaydedin **kaydetmek** hello menü çubuğunda yukarıdaki.</span><span class="sxs-lookup"><span data-stu-id="6b8e1-127">Save your work by selecting **Save** on hello menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="6b8e1-128">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="6b8e1-128">Connector-specific details</span></span>

<span data-ttu-id="6b8e1-129">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="6b8e1-129">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="6b8e1-130">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="6b8e1-130">More connectors</span></span>
<span data-ttu-id="6b8e1-131">Toohello dönün [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="6b8e1-131">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
