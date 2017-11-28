---
title: "mantıksal uygulamalarınızı aaaLearn toouse hello Azure Service Bus Bağlayıcısı | Microsoft Docs"
description: "Logic apps ile Azure uygulama hizmeti oluşturun. TooAzure Service Bus toosend bağlanmak ve iletileri alabilirsiniz. Gönderme tooqueue gibi eylemleri, tootopic göndermek, kuyruktan alma ve abonelikten alırsınız."
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
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a><span data-ttu-id="367cb-105">Hello Azure Service Bus Bağlayıcısı ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="367cb-105">Get started with hello Azure Service Bus connector</span></span>
<span data-ttu-id="367cb-106">TooAzure Service Bus toosend bağlanmak ve iletileri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="367cb-106">Connect tooAzure Service Bus toosend and receive messages.</span></span> <span data-ttu-id="367cb-107">Gönderme tooqueue gibi eylemleri, tootopic göndermek, kuyruktan alma ve abonelikten alırsınız.</span><span class="sxs-lookup"><span data-stu-id="367cb-107">You can perform actions such as send tooqueue, send tootopic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="367cb-108">toouse [tüm bağlayıcıların](apis-list.md), toocreate bir mantıksal uygulama ilk gerekir.</span><span class="sxs-lookup"><span data-stu-id="367cb-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="367cb-109">Tarafından başlayabiliriz [şimdi mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="367cb-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooservice-bus"></a><span data-ttu-id="367cb-110">TooService Bus Bağlan</span><span class="sxs-lookup"><span data-stu-id="367cb-110">Connect tooService Bus</span></span>
<span data-ttu-id="367cb-111">Mantıksal uygulamanızı herhangi bir hizmet erişebilmeniz için önce ilk toocreate bağlantı toohello hizmeti gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="367cb-111">Before your logic app can access any service, you first need toocreate a connection toohello service.</span></span> <span data-ttu-id="367cb-112">A [bağlantı](connectors-overview.md) bir mantıksal uygulama ile başka bir hizmet arasında bağlantı sağlar.</span><span class="sxs-lookup"><span data-stu-id="367cb-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="367cb-113">Hizmet veri yolu tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="367cb-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="367cb-114">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="367cb-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="367cb-115">[Tetikleyiciler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="367cb-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="367cb-116">Bir hizmet veri yolu eylemi kullanın</span><span class="sxs-lookup"><span data-stu-id="367cb-116">Use a Service Bus action</span></span>
<span data-ttu-id="367cb-117">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="367cb-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="367cb-118">[Eylemler hakkında daha fazla bilgi](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="367cb-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="367cb-119">Bağlayıcı özgü ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="367cb-119">Connector-specific details</span></span>

<span data-ttu-id="367cb-120">Tüm tetikleyiciler ve Eylemler hello swagger içinde tanımlanan görüntüleyebilir ve ayrıca hello herhangi bir sınır bkz. [Bağlayıcısı ayrıntıları](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="367cb-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="367cb-121">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="367cb-121">Next steps</span></span>
<span data-ttu-id="367cb-122">[Mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="367cb-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

