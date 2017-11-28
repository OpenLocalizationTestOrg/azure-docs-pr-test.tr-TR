---
title: "logic apps içinde aaaLearn toouse hello Salesforce bağlayıcı | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. Merhaba Salesforce bağlayıcı Salesforce nesnelerle bir API toowork sağlar."
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
ms.openlocfilehash: b14b41fa8a4648b4f0090472dc0f9575bf13a2ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-salesforce-connector"></a><span data-ttu-id="4c518-104">Merhaba Salesforce bağlayıcısıyla kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="4c518-104">Get started with hello Salesforce connector</span></span>
<span data-ttu-id="4c518-105">Merhaba Salesforce bağlayıcı Salesforce nesnelerle bir API toowork sağlar.</span><span class="sxs-lookup"><span data-stu-id="4c518-105">hello Salesforce Connector provides an API toowork with Salesforce objects.</span></span>

<span data-ttu-id="4c518-106">toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c518-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="4c518-107">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4c518-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosalesforce-connector"></a><span data-ttu-id="4c518-108">TooSalesforce bağlayıcı bağlanma</span><span class="sxs-lookup"><span data-stu-id="4c518-108">Connect tooSalesforce connector</span></span>
<span data-ttu-id="4c518-109">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce toocreate ilk gerekiyor bir *bağlantı* toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="4c518-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="4c518-110">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4c518-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosalesforce-connector"></a><span data-ttu-id="4c518-111">Bir bağlantı tooSalesforce bağlayıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="4c518-111">Create a connection tooSalesforce connector</span></span>
> [!INCLUDE [Steps toocreate a connection tooSalesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="4c518-112">Salesforce bağlayıcı tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="4c518-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="4c518-113">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="4c518-113">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="4c518-114">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="4c518-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="4c518-115">Koşul ekle</span><span class="sxs-lookup"><span data-stu-id="4c518-115">Add a condition</span></span>
> [!INCLUDE [Steps toocreate a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="4c518-116">Bir Salesforce bağlayıcı eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="4c518-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="4c518-117">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="4c518-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="4c518-118">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="4c518-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="4c518-119">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="4c518-119">Connector-specific details</span></span>

<span data-ttu-id="4c518-120">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="4c518-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4c518-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c518-121">Next steps</span></span>
[<span data-ttu-id="4c518-122">Mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c518-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

