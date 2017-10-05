---
title: "Azure Logic Apps içinde Yammer bağlayıcısını ekleyin | Microsoft Docs"
description: "REST API parametreleri Yammer bağlayıcısıyla genel bakış"
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
ms.openlocfilehash: c7a213343b4fb2b5a89a5052a459061b404a431c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-yammer-connector"></a><span data-ttu-id="5a6f8-103">Yammer Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="5a6f8-103">Get started with the Yammer connector</span></span>
<span data-ttu-id="5a6f8-104">Erişim görüşmeleri Kurumsal ağınızda Yammer'a bağlanır.</span><span class="sxs-lookup"><span data-stu-id="5a6f8-104">Connect to Yammer to access conversations in your enterprise network.</span></span> <span data-ttu-id="5a6f8-105">Yammer ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5a6f8-105">With Yammer, you can:</span></span>

* <span data-ttu-id="5a6f8-106">İş akışınız Yammer alma verileri temel alan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5a6f8-106">Build your business flow based on the data you get from Yammer.</span></span> 
* <span data-ttu-id="5a6f8-107">Aşağıdaki Grup ya da bir akışı yeni bir ileti olduğunda kullanmak için tetikler.</span><span class="sxs-lookup"><span data-stu-id="5a6f8-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="5a6f8-108">Eylemler bir ileti gönderme, tüm iletileri ve daha fazla bilgi almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="5a6f8-108">Use actions to post a message, get all messages, and more.</span></span> <span data-ttu-id="5a6f8-109">Bu eylemler bir yanıt ve çıkış diğer eylemler için kullanılabilir yapın.</span><span class="sxs-lookup"><span data-stu-id="5a6f8-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="5a6f8-110">Örneğin, yeni bir ileti görüntülendiğinde, Office 365 kullanılarak bir e-posta gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a6f8-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="5a6f8-111">Bir mantıksal uygulama artık oluşturarak başlama; bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5a6f8-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-yammer"></a><span data-ttu-id="5a6f8-112">Yammer bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5a6f8-112">Create a connection to Yammer</span></span>
<span data-ttu-id="5a6f8-113">Yammer Bağlayıcısı'nı kullanmak için önce oluşturduğunuz bir **bağlantı** ardından ayrıntılar için bu özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="5a6f8-113">To use the Yammer connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="5a6f8-114">Özellik</span><span class="sxs-lookup"><span data-stu-id="5a6f8-114">Property</span></span> | <span data-ttu-id="5a6f8-115">Gerekli</span><span class="sxs-lookup"><span data-stu-id="5a6f8-115">Required</span></span> | <span data-ttu-id="5a6f8-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5a6f8-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a6f8-117">Belirteç</span><span class="sxs-lookup"><span data-stu-id="5a6f8-117">Token</span></span> |<span data-ttu-id="5a6f8-118">Evet</span><span class="sxs-lookup"><span data-stu-id="5a6f8-118">Yes</span></span> |<span data-ttu-id="5a6f8-119">Yammer kimlik bilgilerini sağlayın</span><span class="sxs-lookup"><span data-stu-id="5a6f8-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps to create a connection to Yammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="5a6f8-120">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="5a6f8-120">Connector-specific details</span></span>

<span data-ttu-id="5a6f8-121">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/yammer/).</span><span class="sxs-lookup"><span data-stu-id="5a6f8-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="5a6f8-122">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="5a6f8-122">More connectors</span></span>
<span data-ttu-id="5a6f8-123">Geri dönerek [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5a6f8-123">Go back to the [APIs list](apis-list.md).</span></span>