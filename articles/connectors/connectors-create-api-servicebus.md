---
title: "Mantıksal uygulamalarınızı Azure Service Bus Bağlayıcısı'nı kullanmayı öğrenin | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. İleti gönderme ve alma için Azure Service Bus hizmetine bağlanın. Kuyruk, konu başlığına göndermek, kuyruktan alma ve abonelikten almak için gönderme gibi eylemleri gerçekleştirebilirsiniz."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1e2ce06f5993280dbdb67121849591e67f7979e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-service-bus-connector"></a><span data-ttu-id="b4ecb-105">Azure Service Bus Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b4ecb-105">Get started with the Azure Service Bus connector</span></span>
<span data-ttu-id="b4ecb-106">İleti gönderme ve alma için Azure Service Bus hizmetine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="b4ecb-106">Connect to Azure Service Bus to send and receive messages.</span></span> <span data-ttu-id="b4ecb-107">Kuyruk, konu başlığına göndermek, kuyruktan alma ve abonelikten almak için gönderme gibi eylemleri gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4ecb-107">You can perform actions such as send to queue, send to topic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="b4ecb-108">Kullanılacak [tüm bağlayıcıların](apis-list.md), ilk mantıksal uygulama oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4ecb-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="b4ecb-109">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b4ecb-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-service-bus"></a><span data-ttu-id="b4ecb-110">Hizmet veri yoluna bağlayın</span><span class="sxs-lookup"><span data-stu-id="b4ecb-110">Connect to Service Bus</span></span>
<span data-ttu-id="b4ecb-111">Mantıksal uygulamanızı herhangi bir hizmet erişmeden önce ilk hizmetine bir bağlantı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b4ecb-111">Before your logic app can access any service, you first need to create a connection to the service.</span></span> <span data-ttu-id="b4ecb-112">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b4ecb-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps to create a connection to Azure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="b4ecb-113">Hizmet veri yolu tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="b4ecb-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="b4ecb-114">Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="b4ecb-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="b4ecb-115">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b4ecb-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="b4ecb-116">Bir hizmet veri yolu eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="b4ecb-116">Use a Service Bus action</span></span>
<span data-ttu-id="b4ecb-117">Bir eylem, bir mantıksal uygulama içinde tanımlanan iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="b4ecb-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="b4ecb-118">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="b4ecb-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps to create a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="b4ecb-119">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="b4ecb-119">Connector-specific details</span></span>

<span data-ttu-id="b4ecb-120">Tüm tetikleyiciler ve Eylemler swagger tanımlanan görüntüleyebilir ve ayrıca herhangi bir sınır bkz [Bağlayıcısı ayrıntıları](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="b4ecb-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="b4ecb-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4ecb-121">Next steps</span></span>
<span data-ttu-id="b4ecb-122">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b4ecb-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

