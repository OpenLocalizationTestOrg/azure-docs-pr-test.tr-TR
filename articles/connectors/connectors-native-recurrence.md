---
title: "Logic apps içinde yineleme tetikleyici ekleme | Microsoft Docs"
description: "Yineleme tetikleyici ve bir Azure mantıksal uygulama ile kullanmak nasıl genel bakış."
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
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a><span data-ttu-id="0dd9c-103">Yineleme tetikleyici ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0dd9c-103">Get started with the recurrence trigger</span></span>
<span data-ttu-id="0dd9c-104">Yineleme tetikleyici kullanarak bulutta güçlü iş akışları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-104">By using the recurrence trigger, you can create powerful workflows in the cloud.</span></span>

<span data-ttu-id="0dd9c-105">Örneğin, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0dd9c-105">For example, you can:</span></span>

* <span data-ttu-id="0dd9c-106">Bir iş akışı SQL saklı yordamı her gün çalışacak şekilde zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-106">Schedule a workflow to run a SQL stored procedure every day.</span></span>
* <span data-ttu-id="0dd9c-107">Belirli bir hashtag hakkında geçen hafta içinde tüm tweet'leri özetini e-posta.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-107">Email a summary of all tweets within the last week about a certain hashtag.</span></span>

<span data-ttu-id="0dd9c-108">Yineleme tetikleyici bir mantıksal uygulama kullanmaya başlamak için bkz: [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0dd9c-108">To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="0dd9c-109">Bir yineleme tetikleyici kullanın</span><span class="sxs-lookup"><span data-stu-id="0dd9c-109">Use a recurrence trigger</span></span>
<span data-ttu-id="0dd9c-110">Bir tetikleyici bir mantıksal uygulama tanımlı iş akışını başlatmak için kullanılan bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="0dd9c-111">[Tetikleyiciler hakkında daha fazla bilgi](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0dd9c-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="0dd9c-112">Bir mantıksal uygulama yinelenme tetikleyici ayarlama konusunda bir örnek sırası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="0dd9c-112">Here’s an example sequence of how to set up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="0dd9c-113">Ekleme **yineleme** tetikleyici bir mantıksal uygulama ilk adımı olarak.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-113">Add the **Recurrence** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="0dd9c-114">Parametrelerde yineleme aralığını doldurun.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-114">Fill in the parameters for the recurrence interval.</span></span>

<span data-ttu-id="0dd9c-115">Mantıksal uygulama artık çalışma sonrasında her zaman aralığı başlatır.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-115">The logic app now starts a run after each interval of time.</span></span>

![HTTP tetikleyicisi](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="0dd9c-117">Tetikleyici ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="0dd9c-117">Trigger details</span></span>
<span data-ttu-id="0dd9c-118">Yineleme tetikleyici yapılandırabilirsiniz aşağıdaki özelliklere sahip.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-118">The recurrence trigger has the following properties that you can configure.</span></span>

<span data-ttu-id="0dd9c-119">Bu mantıksal uygulama belirtilen bir süre sonra ateşlenir.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="0dd9c-120">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="0dd9c-121">Görünen ad</span><span class="sxs-lookup"><span data-stu-id="0dd9c-121">Display name</span></span> | <span data-ttu-id="0dd9c-122">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="0dd9c-122">Property name</span></span> | <span data-ttu-id="0dd9c-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0dd9c-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0dd9c-124">Sıklık *</span><span class="sxs-lookup"><span data-stu-id="0dd9c-124">Frequency*</span></span> |<span data-ttu-id="0dd9c-125">Sıklık</span><span class="sxs-lookup"><span data-stu-id="0dd9c-125">frequency</span></span> |<span data-ttu-id="0dd9c-126">Zaman birimi: `Second`, `Minute`, `Hour`, `Day`, veya `Year`.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-126">The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="0dd9c-127">Aralık *</span><span class="sxs-lookup"><span data-stu-id="0dd9c-127">Interval*</span></span> |<span data-ttu-id="0dd9c-128">aralığı</span><span class="sxs-lookup"><span data-stu-id="0dd9c-128">interval</span></span> |<span data-ttu-id="0dd9c-129">Verilen sıklığı aralığını yineleme için.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-129">The interval of the given frequency for the recurrence.</span></span> |
| <span data-ttu-id="0dd9c-130">Saat Dilimi</span><span class="sxs-lookup"><span data-stu-id="0dd9c-130">Time Zone</span></span> |<span data-ttu-id="0dd9c-131">saat dilimi</span><span class="sxs-lookup"><span data-stu-id="0dd9c-131">timeZone</span></span> |<span data-ttu-id="0dd9c-132">Bir başlangıç saati UTC uzaklığı sağlanırsa, bu saat dilimi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0dd9c-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="0dd9c-133">Başlangıç zamanı</span><span class="sxs-lookup"><span data-stu-id="0dd9c-133">Start time</span></span> |<span data-ttu-id="0dd9c-134">startTime</span><span class="sxs-lookup"><span data-stu-id="0dd9c-134">startTime</span></span> |<span data-ttu-id="0dd9c-135">Başlangıç saati [ISO 8601 biçim](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="0dd9c-135">The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="0dd9c-136">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0dd9c-136">Next steps</span></span>
<span data-ttu-id="0dd9c-137">Şimdi, platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="0dd9c-137">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="0dd9c-138">Logic apps diğer kullanılabilir bağlayıcılar bakarak keşfedebilirsiniz bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="0dd9c-138">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

