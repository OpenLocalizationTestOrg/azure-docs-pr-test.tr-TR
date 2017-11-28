---
title: aaaAdd hello Azure Logic Apps Yammer Connector'daki | Microsoft Docs
description: "REST API parametrelerle hello Yammer bağlayıcı genel bakış"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5ae0827-fbb3-45ec-8f45-ad1cc2e7eccc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: be75df770a8062d839926dff8c0195d2647f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-yammer-connector"></a><span data-ttu-id="b6d24-103">Merhaba Yammer Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b6d24-103">Get started with hello Yammer connector</span></span>
<span data-ttu-id="b6d24-104">TooYammer tooaccess görüşmeleri, Kurumsal ağınıza bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b6d24-104">Connect tooYammer tooaccess conversations in your enterprise network.</span></span> <span data-ttu-id="b6d24-105">Yammer ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b6d24-105">With Yammer, you can:</span></span>

* <span data-ttu-id="b6d24-106">İş akışınız hello verileri Yammer Al esas oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b6d24-106">Build your business flow based on hello data you get from Yammer.</span></span> 
* <span data-ttu-id="b6d24-107">Aşağıdaki Grup ya da bir akışı yeni bir ileti olduğunda kullanmak için tetikler.</span><span class="sxs-lookup"><span data-stu-id="b6d24-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="b6d24-108">Eylemler toopost bir ileti kullanın, tüm iletileri ve daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="b6d24-108">Use actions toopost a message, get all messages, and more.</span></span> <span data-ttu-id="b6d24-109">Bu eylemler bir yanıt ve hello çıkış diğer eylemler için kullanılabilir yapın.</span><span class="sxs-lookup"><span data-stu-id="b6d24-109">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="b6d24-110">Örneğin, yeni bir ileti görüntülendiğinde, Office 365 kullanılarak bir e-posta gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6d24-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="b6d24-111">Bir mantıksal uygulama artık oluşturarak başlama; bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b6d24-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooyammer"></a><span data-ttu-id="b6d24-112">Bir bağlantı tooYammer oluşturma</span><span class="sxs-lookup"><span data-stu-id="b6d24-112">Create a connection tooYammer</span></span>
<span data-ttu-id="b6d24-113">ilk toouse hello Yammer Bağlayıcısı oluşturmanız bir **bağlantı** sonra hello Ayrıntılar için bu özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="b6d24-113">toouse hello Yammer connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="b6d24-114">Özellik</span><span class="sxs-lookup"><span data-stu-id="b6d24-114">Property</span></span> | <span data-ttu-id="b6d24-115">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b6d24-115">Required</span></span> | <span data-ttu-id="b6d24-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b6d24-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6d24-117">Belirteç</span><span class="sxs-lookup"><span data-stu-id="b6d24-117">Token</span></span> |<span data-ttu-id="b6d24-118">Evet</span><span class="sxs-lookup"><span data-stu-id="b6d24-118">Yes</span></span> |<span data-ttu-id="b6d24-119">Yammer kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="b6d24-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps toocreate a connection tooYammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="b6d24-120">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="b6d24-120">Connector-specific details</span></span>

<span data-ttu-id="b6d24-121">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/yammer/).</span><span class="sxs-lookup"><span data-stu-id="b6d24-121">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="b6d24-122">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="b6d24-122">More connectors</span></span>
<span data-ttu-id="b6d24-123">Toohello dönün [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b6d24-123">Go back toohello [APIs list](apis-list.md).</span></span>
