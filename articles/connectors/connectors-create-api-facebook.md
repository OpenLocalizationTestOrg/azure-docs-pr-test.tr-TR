---
title: "Logic Apps içinde Facebook bağlayıcısını ekleyin | Microsoft Docs"
description: "REST API parametrelerle Facebook bağlayıcısını genel bakış"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f4d6f0ed-c09b-488c-be1c-8cf2b5b1d4b8
ms.service: multiple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/07/2016
ms.author: mandia; ladocs
ms.openlocfilehash: e10a30ccef3e81cb3d7749696453d82b8958d076
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-facebook-connector"></a><span data-ttu-id="f96f5-103">Facebook Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f96f5-103">Get started with the Facebook connector</span></span>
<span data-ttu-id="f96f5-104">Facebook hesabına bağlanma ve gönderi, sayfa akışı ve daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="f96f5-104">Connect to Facebook and post to a timeline, get a page feed, and more.</span></span> <span data-ttu-id="f96f5-105">Facebook ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f96f5-105">With Facebook, you can:</span></span>

* <span data-ttu-id="f96f5-106">Facebook alma verileri temel alan, iş akışınızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f96f5-106">Build your business flow based on the data you get from Facebook.</span></span> 
* <span data-ttu-id="f96f5-107">Yeni bir posta alındığında bir tetikleyici kullanın.</span><span class="sxs-lookup"><span data-stu-id="f96f5-107">Use a trigger when a new post is received.</span></span>
* <span data-ttu-id="f96f5-108">Zaman Çizelgesi'sonrası kullanım Eylemler ve sayfa akışı alın.</span><span class="sxs-lookup"><span data-stu-id="f96f5-108">Use actions that post to your timeline, get a page feed, and more.</span></span> <span data-ttu-id="f96f5-109">Bu eylemler bir yanıt ve çıkış diğer eylemler için kullanılabilir yapın.</span><span class="sxs-lookup"><span data-stu-id="f96f5-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="f96f5-110">Örneğin, kendi zaman çizelgesi üzerinde yeni bir posta olduğunda bu posta ele ve Twitter akışınıza gönderim.</span><span class="sxs-lookup"><span data-stu-id="f96f5-110">For example, when there is a new post on your timeline, you can take that post and push it to your Twitter feed.</span></span> 

<span data-ttu-id="f96f5-111">Bir mantıksal uygulama'yi şimdi oluşturmaya başlamak, bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f96f5-111">You can get started by creating a logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-facebook"></a><span data-ttu-id="f96f5-112">Facebook bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f96f5-112">Create a connection to Facebook</span></span>
<span data-ttu-id="f96f5-113">Bu bağlayıcı mantıksal uygulamalarınızı eklediğinizde, Facebook bağlanmak için logic apps yetkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f96f5-113">When you add this connector to your logic apps, you must authorize logic apps to connect to your Facebook.</span></span>

1. <span data-ttu-id="f96f5-114">Facebook hesabınızda oturum açın</span><span class="sxs-lookup"><span data-stu-id="f96f5-114">Sign in to your Facebook account</span></span>
2. <span data-ttu-id="f96f5-115">Seçin **Authorize**ve logic apps, Facebook bağlanıp izin verin.</span><span class="sxs-lookup"><span data-stu-id="f96f5-115">Select **Authorize**, and allow your logic apps to connect and use your Facebook.</span></span> 

> [!INCLUDE [Steps to create a connection to Facebook](../../includes/connectors-create-api-facebook.md)]
> 


## <a name="connector-specific-details"></a><span data-ttu-id="f96f5-116">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="f96f5-116">Connector-specific details</span></span>

<span data-ttu-id="f96f5-117">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/facebook/).</span><span class="sxs-lookup"><span data-stu-id="f96f5-117">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/facebook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="f96f5-118">Daha fazla bağlayıcılar</span><span class="sxs-lookup"><span data-stu-id="f96f5-118">More connectors</span></span>
<span data-ttu-id="f96f5-119">Geri dönerek [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f96f5-119">Go back to the [APIs list](apis-list.md).</span></span>