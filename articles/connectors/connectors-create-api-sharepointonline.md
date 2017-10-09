---
title: "aaaLearn nasıl toouse hello logic apps içinde SharePoint Online bağlayıcısını | Microsoft Docs"
description: "Logic apps hello SharePoint Online bağlayıcısıyla SharePoint'te toomange listeleri oluşturun."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e0ec3149-507a-409d-8e7b-d5fbded006ce
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: fc2f2745f0d174eae6165e84fd8b6656b0aac44b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-online-connector"></a><span data-ttu-id="a4ed5-103">Merhaba SharePoint Online Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="a4ed5-103">Get started with hello SharePoint Online connector</span></span>
<span data-ttu-id="a4ed5-104">SharePoint listeleri hello SharePoint Online bağlayıcısını toomanage kullanın.</span><span class="sxs-lookup"><span data-stu-id="a4ed5-104">Use hello SharePoint Online connector toomanage SharePoint lists.</span></span>  

<span data-ttu-id="a4ed5-105">toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4ed5-105">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="a4ed5-106">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a4ed5-106">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosharepoint-online"></a><span data-ttu-id="a4ed5-107">Çevrimiçi tooSharePoint Bağlan</span><span class="sxs-lookup"><span data-stu-id="a4ed5-107">Connect tooSharePoint Online</span></span>
<span data-ttu-id="a4ed5-108">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce toocreate ilk gerekiyor bir *bağlantı* toohello hizmet.</span><span class="sxs-lookup"><span data-stu-id="a4ed5-108">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="a4ed5-109">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4ed5-109">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosharepoint-online"></a><span data-ttu-id="a4ed5-110">Bağlantı tooSharePoint çevrimiçi oluşturma</span><span class="sxs-lookup"><span data-stu-id="a4ed5-110">Create a connection tooSharePoint Online</span></span>
> [!INCLUDE [Steps toocreate a connection tooSharePoint](../../includes/connectors-create-api-sharepointonline.md)]


## <a name="use-a-sharepoint-online-trigger"></a><span data-ttu-id="a4ed5-111">SharePoint Online tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="a4ed5-111">Use a SharePoint Online trigger</span></span>
<span data-ttu-id="a4ed5-112">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="a4ed5-112">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="a4ed5-113">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="a4ed5-113">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a SharePoint Online trigger](../../includes/connectors-create-api-sharepointonline-trigger.md)]


## <a name="use-a-sharepoint-online-action"></a><span data-ttu-id="a4ed5-114">Bir SharePoint Online eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="a4ed5-114">Use a SharePoint Online action</span></span>
<span data-ttu-id="a4ed5-115">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="a4ed5-115">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="a4ed5-116">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="a4ed5-116">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a SharePoint Online action](../../includes/connectors-create-api-sharepointonline-action.md)]


## <a name="connector-specific-details"></a><span data-ttu-id="a4ed5-117">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="a4ed5-117">Connector-specific details</span></span>

<span data-ttu-id="a4ed5-118">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="a4ed5-118">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sharepoint/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4ed5-119">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="a4ed5-119">Next Steps</span></span>
[<span data-ttu-id="a4ed5-120">Mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a4ed5-120">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

