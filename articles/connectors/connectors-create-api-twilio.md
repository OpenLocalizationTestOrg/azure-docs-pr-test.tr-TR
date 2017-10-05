---
title: "Twilio bağlayıcı Azure Logic apps içinde ekleme | Microsoft Docs"
description: "REST API parametreleri Twilio bağlayıcısıyla genel bakış"
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
ms.openlocfilehash: a790ac51b0fea7e3fa379d20e0e094e7ce0d7696
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twilio-connector"></a><span data-ttu-id="dd2aa-103">Twilio Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="dd2aa-103">Get started with the Twilio connector</span></span>
<span data-ttu-id="dd2aa-104">Genel IP SMS ve MMS ileti gönderme ve alma için Twilio için bağlayın.</span><span class="sxs-lookup"><span data-stu-id="dd2aa-104">Connect to Twilio to send and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="dd2aa-105">Twilio ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dd2aa-105">With Twilio, you can:</span></span>

* <span data-ttu-id="dd2aa-106">İş akışınız Twilio alma verileri temel alan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd2aa-106">Build your business flow based on the data you get from Twilio.</span></span> 
* <span data-ttu-id="dd2aa-107">Bir ileti, liste iletiler ve daha fazlasını alma eylemlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="dd2aa-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="dd2aa-108">Bu eylemler bir yanıt ve çıkış diğer eylemler için kullanılabilir yapın.</span><span class="sxs-lookup"><span data-stu-id="dd2aa-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="dd2aa-109">Örneğin, yeni bir Twilio ileti aldığınızda, bu ileti almak ve bir hizmet veri yolu iş akışı kullanın.</span><span class="sxs-lookup"><span data-stu-id="dd2aa-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="dd2aa-110">Bir mantıksal uygulama oluşturarak başlama; bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="dd2aa-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-twilio"></a><span data-ttu-id="dd2aa-111">Twilio bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd2aa-111">Create a connection to Twilio</span></span>
<span data-ttu-id="dd2aa-112">Bu bağlayıcı mantıksal uygulamalarınızı eklediğinizde, aşağıdaki Twilio değerleri girin:</span><span class="sxs-lookup"><span data-stu-id="dd2aa-112">When you add this Connector to your logic apps, enter the following Twilio values:</span></span>

| <span data-ttu-id="dd2aa-113">Özellik</span><span class="sxs-lookup"><span data-stu-id="dd2aa-113">Property</span></span> | <span data-ttu-id="dd2aa-114">Gerekli</span><span class="sxs-lookup"><span data-stu-id="dd2aa-114">Required</span></span> | <span data-ttu-id="dd2aa-115">Açıklama</span><span class="sxs-lookup"><span data-stu-id="dd2aa-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd2aa-116">Hesap Kimliği</span><span class="sxs-lookup"><span data-stu-id="dd2aa-116">Account ID</span></span> |<span data-ttu-id="dd2aa-117">Evet</span><span class="sxs-lookup"><span data-stu-id="dd2aa-117">Yes</span></span> |<span data-ttu-id="dd2aa-118">Twilio hesabı Kimliğinizi girin</span><span class="sxs-lookup"><span data-stu-id="dd2aa-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="dd2aa-119">Erişim belirteci</span><span class="sxs-lookup"><span data-stu-id="dd2aa-119">Access Token</span></span> |<span data-ttu-id="dd2aa-120">Evet</span><span class="sxs-lookup"><span data-stu-id="dd2aa-120">Yes</span></span> |<span data-ttu-id="dd2aa-121">Twilio erişim belirtecinizi girin</span><span class="sxs-lookup"><span data-stu-id="dd2aa-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps to create a connection to Twilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="dd2aa-122">Twilio erişim belirteci sahip değilseniz, bkz: [kullanıcı kimliği ve erişim belirteçleri](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="dd2aa-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="dd2aa-123">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="dd2aa-123">Connector-specific details</span></span>

<span data-ttu-id="dd2aa-124">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="dd2aa-124">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="dd2aa-125">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="dd2aa-125">More connectors</span></span>
<span data-ttu-id="dd2aa-126">Geri dönerek [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="dd2aa-126">Go back to the [APIs list](apis-list.md).</span></span>