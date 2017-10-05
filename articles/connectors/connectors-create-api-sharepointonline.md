---
title: "Logic apps içinde SharePoint Online Bağlayıcısı'nı kullanmayı öğrenin | Microsoft Docs"
description: "SharePoint Yönet listelerde için SharePoint Online bağlayıcısıyla mantıksal uygulamalar oluşturun."
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
ms.openlocfilehash: 96fc1347604c0c6cc2c2463a5dbd83b560183a16
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-online-connector"></a><span data-ttu-id="522e7-103">SharePoint Online Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="522e7-103">Get started with the SharePoint Online connector</span></span>
<span data-ttu-id="522e7-104">SharePoint listelerini yönetmek için SharePoint Online Bağlayıcısı'nı kullanın.</span><span class="sxs-lookup"><span data-stu-id="522e7-104">Use the SharePoint Online connector to manage SharePoint lists.</span></span>  

<span data-ttu-id="522e7-105">Kullanılacak [tüm bağlayıcıların](apis-list.md), ilk mantıksal uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="522e7-105">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="522e7-106">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="522e7-106">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sharepoint-online"></a><span data-ttu-id="522e7-107">SharePoint'e çevrimiçi Bağlan</span><span class="sxs-lookup"><span data-stu-id="522e7-107">Connect to SharePoint Online</span></span>
<span data-ttu-id="522e7-108">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce ilk önce oluşturmanız gerekir bir *bağlantı* hizmet.</span><span class="sxs-lookup"><span data-stu-id="522e7-108">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="522e7-109">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="522e7-109">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sharepoint-online"></a><span data-ttu-id="522e7-110">SharePoint Online bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="522e7-110">Create a connection to SharePoint Online</span></span>
> [!INCLUDE [Steps to create a connection to SharePoint](../../includes/connectors-create-api-sharepointonline.md)]


## <a name="use-a-sharepoint-online-trigger"></a><span data-ttu-id="522e7-111">SharePoint Online tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="522e7-111">Use a SharePoint Online trigger</span></span>
<span data-ttu-id="522e7-112">Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="522e7-112">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="522e7-113">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="522e7-113">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online trigger](../../includes/connectors-create-api-sharepointonline-trigger.md)]


## <a name="use-a-sharepoint-online-action"></a><span data-ttu-id="522e7-114">Bir SharePoint Online eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="522e7-114">Use a SharePoint Online action</span></span>
<span data-ttu-id="522e7-115">Bir eylem, bir mantıksal uygulama içinde tanımlanan iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="522e7-115">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="522e7-116">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="522e7-116">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a SharePoint Online action](../../includes/connectors-create-api-sharepointonline-action.md)]


## <a name="connector-specific-details"></a><span data-ttu-id="522e7-117">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="522e7-117">Connector-specific details</span></span>

<span data-ttu-id="522e7-118">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="522e7-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="522e7-119">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="522e7-119">Next Steps</span></span>
[<span data-ttu-id="522e7-120">Mantıksal uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="522e7-120">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

