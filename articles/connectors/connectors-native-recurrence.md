---
title: logic apps aaaAdd hello yinelenme tetikleyici | Microsoft Docs
description: "Merhaba yinelenme tetikleyici, genel bakış ve nasıl toouse bir Azure mantıksal uygulama ile."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a><span data-ttu-id="b4df4-103">Merhaba yinelenme tetikleyici ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="b4df4-103">Get started with hello recurrence trigger</span></span>
<span data-ttu-id="b4df4-104">Merhaba yinelenme tetikleyicisini kullanarak hello bulutta güçlü iş akışları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b4df4-104">By using hello recurrence trigger, you can create powerful workflows in hello cloud.</span></span>

<span data-ttu-id="b4df4-105">Örneğin, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b4df4-105">For example, you can:</span></span>

* <span data-ttu-id="b4df4-106">İş akışı toorun SQL saklı yordamı her gün zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="b4df4-106">Schedule a workflow toorun a SQL stored procedure every day.</span></span>
* <span data-ttu-id="b4df4-107">Merhaba belirli bir hashtag hakkında geçen hafta içinde tüm tweet'leri özetini e-posta.</span><span class="sxs-lookup"><span data-stu-id="b4df4-107">Email a summary of all tweets within hello last week about a certain hashtag.</span></span>

<span data-ttu-id="b4df4-108">bir mantıksal uygulama Hello yinelenme tetikleyici kullanmaya tooget bkz [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b4df4-108">tooget started using hello recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="b4df4-109">Bir yineleme tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="b4df4-109">Use a recurrence trigger</span></span>
<span data-ttu-id="b4df4-110">Bir tetikleyici bir mantıksal uygulama tanımlı kullanılan toostart hello iş akışı olabilecek bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="b4df4-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="b4df4-111">[Tetikleyiciler hakkında daha fazla bilgi](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b4df4-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="b4df4-112">Nasıl bir yinelenme yukarı tooset tetikleyen bir mantıksal uygulama bir örnek sırası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="b4df4-112">Here’s an example sequence of how tooset up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="b4df4-113">Merhaba eklemek **yineleme** tetikleyici hello bir mantıksal uygulama ilk adımı olarak.</span><span class="sxs-lookup"><span data-stu-id="b4df4-113">Add hello **Recurrence** trigger as hello first step in a logic app.</span></span>
2. <span data-ttu-id="b4df4-114">Merhaba parametrelerinde hello yineleme aralığını doldurun.</span><span class="sxs-lookup"><span data-stu-id="b4df4-114">Fill in hello parameters for hello recurrence interval.</span></span>

<span data-ttu-id="b4df4-115">Merhaba mantıksal uygulama artık çalışma sonrasında her zaman aralığı başlatır.</span><span class="sxs-lookup"><span data-stu-id="b4df4-115">hello logic app now starts a run after each interval of time.</span></span>

![HTTP tetikleyicisi](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="b4df4-117">Tetikleyici ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="b4df4-117">Trigger details</span></span>
<span data-ttu-id="b4df4-118">Merhaba yinelenme tetikleyici hello aşağıdaki yapılandırabileceğiniz özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="b4df4-118">hello recurrence trigger has hello following properties that you can configure.</span></span>

<span data-ttu-id="b4df4-119">Bu mantıksal uygulama belirtilen bir süre sonra ateşlenir.</span><span class="sxs-lookup"><span data-stu-id="b4df4-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="b4df4-120">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="b4df4-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="b4df4-121">Görünen ad</span><span class="sxs-lookup"><span data-stu-id="b4df4-121">Display name</span></span> | <span data-ttu-id="b4df4-122">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="b4df4-122">Property name</span></span> | <span data-ttu-id="b4df4-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b4df4-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b4df4-124">Sıklık *</span><span class="sxs-lookup"><span data-stu-id="b4df4-124">Frequency*</span></span> |<span data-ttu-id="b4df4-125">frequency</span><span class="sxs-lookup"><span data-stu-id="b4df4-125">frequency</span></span> |<span data-ttu-id="b4df4-126">zaman birimi Hello: `Second`, `Minute`, `Hour`, `Day`, veya `Year`.</span><span class="sxs-lookup"><span data-stu-id="b4df4-126">hello unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="b4df4-127">Aralık *</span><span class="sxs-lookup"><span data-stu-id="b4df4-127">Interval*</span></span> |<span data-ttu-id="b4df4-128">interval</span><span class="sxs-lookup"><span data-stu-id="b4df4-128">interval</span></span> |<span data-ttu-id="b4df4-129">Merhaba yinelemesi sıklığı verilen hello Hello aralığı.</span><span class="sxs-lookup"><span data-stu-id="b4df4-129">hello interval of hello given frequency for hello recurrence.</span></span> |
| <span data-ttu-id="b4df4-130">Saat Dilimi</span><span class="sxs-lookup"><span data-stu-id="b4df4-130">Time Zone</span></span> |<span data-ttu-id="b4df4-131">saat dilimi</span><span class="sxs-lookup"><span data-stu-id="b4df4-131">timeZone</span></span> |<span data-ttu-id="b4df4-132">Bir başlangıç saati UTC uzaklığı sağlanırsa, bu saat dilimi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b4df4-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="b4df4-133">Başlangıç zamanı</span><span class="sxs-lookup"><span data-stu-id="b4df4-133">Start time</span></span> |<span data-ttu-id="b4df4-134">startTime</span><span class="sxs-lookup"><span data-stu-id="b4df4-134">startTime</span></span> |<span data-ttu-id="b4df4-135">Merhaba başlangıç saati [ISO 8601 biçim](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="b4df4-135">hello start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="b4df4-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b4df4-136">Next steps</span></span>
<span data-ttu-id="b4df4-137">Şimdi, hello platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="b4df4-137">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="b4df4-138">Keşfedebilirsiniz bakarak logic apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b4df4-138">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

