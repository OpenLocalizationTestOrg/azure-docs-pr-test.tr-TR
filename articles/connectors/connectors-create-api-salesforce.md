---
title: "Logic apps içinde Salesforce Bağlayıcısı'nı kullanmayı öğrenin | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. Salesforce Bağlayıcısı bir API'nin Salesforce nesneleriyle birlikte çalışmasını sağlar."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/05/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c2e2efd356382df9404f5c4ed54f24758b2cd22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-salesforce-connector"></a><span data-ttu-id="9dd44-104">Salesforce bağlayıcısıyla kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9dd44-104">Get started with the Salesforce connector</span></span>
<span data-ttu-id="9dd44-105">Salesforce Bağlayıcısı bir API'nin Salesforce nesneleriyle birlikte çalışmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9dd44-105">The Salesforce Connector provides an API to work with Salesforce objects.</span></span>

<span data-ttu-id="9dd44-106">Kullanılacak [tüm bağlayıcıların](apis-list.md), ilk mantıksal uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9dd44-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="9dd44-107">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9dd44-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-salesforce-connector"></a><span data-ttu-id="9dd44-108">Salesforce bağlayıcı bağlanma</span><span class="sxs-lookup"><span data-stu-id="9dd44-108">Connect to Salesforce connector</span></span>
<span data-ttu-id="9dd44-109">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce ilk önce oluşturmanız gerekir bir *bağlantı* hizmet.</span><span class="sxs-lookup"><span data-stu-id="9dd44-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="9dd44-110">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="9dd44-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-salesforce-connector"></a><span data-ttu-id="9dd44-111">Salesforce Bağlayıcısı bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9dd44-111">Create a connection to Salesforce connector</span></span>
> [!INCLUDE [Steps to create a connection to Salesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="9dd44-112">Salesforce bağlayıcı tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="9dd44-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="9dd44-113">Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="9dd44-113">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="9dd44-114">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9dd44-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="9dd44-115">Koşul ekle</span><span class="sxs-lookup"><span data-stu-id="9dd44-115">Add a condition</span></span>
> [!INCLUDE [Steps to create a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="9dd44-116">Bir Salesforce bağlayıcı eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="9dd44-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="9dd44-117">Bir eylem, bir mantıksal uygulama içinde tanımlanan iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="9dd44-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="9dd44-118">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="9dd44-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="9dd44-119">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="9dd44-119">Connector-specific details</span></span>

<span data-ttu-id="9dd44-120">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="9dd44-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="9dd44-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9dd44-121">Next steps</span></span>
[<span data-ttu-id="9dd44-122">Mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9dd44-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

