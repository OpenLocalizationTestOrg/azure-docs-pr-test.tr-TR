---
title: "aaaAdd hello Twilio bağlayıcı Azure Logic apps içinde | Microsoft Docs"
description: "REST API parametrelerle hello Twilio bağlayıcı genel bakış"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a><span data-ttu-id="0de25-103">Merhaba Twilio Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0de25-103">Get started with hello Twilio connector</span></span>
<span data-ttu-id="0de25-104">TooTwilio toosend bağlanmak ve genel IP SMS ve MMS iletileri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0de25-104">Connect tooTwilio toosend and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="0de25-105">Twilio ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0de25-105">With Twilio, you can:</span></span>

* <span data-ttu-id="0de25-106">İş akışınız hello verileri Twilio Al esas oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0de25-106">Build your business flow based on hello data you get from Twilio.</span></span> 
* <span data-ttu-id="0de25-107">Bir ileti, liste iletiler ve daha fazlasını alma eylemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0de25-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="0de25-108">Bu eylemler bir yanıt ve hello çıkış diğer eylemler için kullanılabilir yapın.</span><span class="sxs-lookup"><span data-stu-id="0de25-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="0de25-109">Örneğin, yeni bir Twilio ileti aldığınızda, bu ileti almak ve bir hizmet veri yolu iş akışı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0de25-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="0de25-110">Bir mantıksal uygulama oluşturarak başlama; bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0de25-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tootwilio"></a><span data-ttu-id="0de25-111">Bir bağlantı tooTwilio oluşturma</span><span class="sxs-lookup"><span data-stu-id="0de25-111">Create a connection tooTwilio</span></span>
<span data-ttu-id="0de25-112">Bu bağlayıcı tooyour logic apps eklediğinizde, Twilio değerleri aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="0de25-112">When you add this Connector tooyour logic apps, enter hello following Twilio values:</span></span>

| <span data-ttu-id="0de25-113">Özellik</span><span class="sxs-lookup"><span data-stu-id="0de25-113">Property</span></span> | <span data-ttu-id="0de25-114">Gerekli</span><span class="sxs-lookup"><span data-stu-id="0de25-114">Required</span></span> | <span data-ttu-id="0de25-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0de25-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0de25-116">Hesap Kimliği</span><span class="sxs-lookup"><span data-stu-id="0de25-116">Account ID</span></span> |<span data-ttu-id="0de25-117">Evet</span><span class="sxs-lookup"><span data-stu-id="0de25-117">Yes</span></span> |<span data-ttu-id="0de25-118">Twilio hesabı Kimliğinizi girin</span><span class="sxs-lookup"><span data-stu-id="0de25-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="0de25-119">Erişim belirteci</span><span class="sxs-lookup"><span data-stu-id="0de25-119">Access Token</span></span> |<span data-ttu-id="0de25-120">Evet</span><span class="sxs-lookup"><span data-stu-id="0de25-120">Yes</span></span> |<span data-ttu-id="0de25-121">Twilio erişim belirtecinizi girin</span><span class="sxs-lookup"><span data-stu-id="0de25-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="0de25-122">Twilio erişim belirteci sahip değilseniz, bkz: [kullanıcı kimliği ve erişim belirteçleri](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="0de25-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="0de25-123">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="0de25-123">Connector-specific details</span></span>

<span data-ttu-id="0de25-124">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="0de25-124">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="0de25-125">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="0de25-125">More connectors</span></span>
<span data-ttu-id="0de25-126">Toohello dönün [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="0de25-126">Go back toohello [APIs list](apis-list.md).</span></span>
