---
title: logic apps gecikmeden aaaAdd | Microsoft Docs
description: "Merhaba genel bakış gecikmesi ve gecikme-Eylemler kadar ve nasıl toouse bunları Azure mantıksal uygulama ile."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a><span data-ttu-id="3642f-103">Merhaba ile çalışmaya başlama gecikmesi ve gecikme-Eylemler kadar</span><span class="sxs-lookup"><span data-stu-id="3642f-103">Get started with hello delay and delay-until actions</span></span>
<span data-ttu-id="3642f-104">Merhaba gecikme kullanarak ve "gecikme-kadar" Eylemler, iş akışı senaryoları tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3642f-104">By using hello delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="3642f-105">Örneğin, şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3642f-105">For example, you can:</span></span>

* <span data-ttu-id="3642f-106">Haftanın günü toosend durumu güncelleştirilene kadar e-posta bekleyin.</span><span class="sxs-lookup"><span data-stu-id="3642f-106">Wait until a weekday toosend a status update over email.</span></span>
* <span data-ttu-id="3642f-107">Bir HTTP çağrısıyla kadar gecikme hello iş akışı hello sonuç alma ve sürdürme önce zaman toofinish sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3642f-107">Delay hello workflow until an HTTP call has time toofinish before resuming and retrieving hello result.</span></span>

<span data-ttu-id="3642f-108">bir mantıksal uygulama Hello gecikme eylem kullanmaya tooget bkz [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3642f-108">tooget started using hello delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-delay-actions"></a><span data-ttu-id="3642f-109">Merhaba gecikme eylemlerini kullanın</span><span class="sxs-lookup"><span data-stu-id="3642f-109">Use hello delay actions</span></span>
<span data-ttu-id="3642f-110">Bir eylem, bir mantıksal uygulama tanımlı hello iş akışı tarafından gerçekleştirilen bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="3642f-110">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="3642f-111">[Eylemler hakkında daha fazla bilgi](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3642f-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="3642f-112">Nasıl toouse bir gecikme adım bir mantıksal uygulama bir örnek sırası şöyledir:</span><span class="sxs-lookup"><span data-stu-id="3642f-112">Here’s an example sequence of how toouse a delay step in a logic app:</span></span>

1. <span data-ttu-id="3642f-113">Bir tetikleyici ekledikten sonra tıklatın **yeni adım** tooadd bir eylem.</span><span class="sxs-lookup"><span data-stu-id="3642f-113">After adding a trigger, click **New Step** tooadd an action.</span></span>
2. <span data-ttu-id="3642f-114">Arama **gecikme** toobring hello gecikme Eylemler ayarlama.</span><span class="sxs-lookup"><span data-stu-id="3642f-114">Search for **delay** toobring up hello delay actions.</span></span> <span data-ttu-id="3642f-115">Bu örnekte, biz seçecektir **gecikme**.</span><span class="sxs-lookup"><span data-stu-id="3642f-115">In this example, we will select **Delay**.</span></span>
   
    ![Gecikme Eylemler](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="3642f-117">Merhaba eylem özellikleri tooconfigure hello gecikme tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="3642f-117">Complete any of hello action properties tooconfigure hello delay.</span></span>
   
    ![Gecikme yapılandırma](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="3642f-119">Tıklatın **kaydetmek** toopublish ve hello mantıksal uygulama etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="3642f-119">Click **Save** toopublish and activate hello logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="3642f-120">Eylem ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="3642f-120">Action details</span></span>
<span data-ttu-id="3642f-121">Merhaba yinelenme tetikleyici hello aşağıdaki yapılandırılabilir özelliklere sahiptir.</span><span class="sxs-lookup"><span data-stu-id="3642f-121">hello recurrence trigger has hello following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="3642f-122">Gecikme eylemi</span><span class="sxs-lookup"><span data-stu-id="3642f-122">Delay action</span></span>
<span data-ttu-id="3642f-123">Bu eylem gecikmeler hello belirli bir zaman aralığı için çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3642f-123">This action delays hello run for a certain time interval.</span></span>
<span data-ttu-id="3642f-124">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3642f-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="3642f-125">Görünen ad</span><span class="sxs-lookup"><span data-stu-id="3642f-125">Display name</span></span> | <span data-ttu-id="3642f-126">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="3642f-126">Property name</span></span> | <span data-ttu-id="3642f-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3642f-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3642f-128">Sayısı *</span><span class="sxs-lookup"><span data-stu-id="3642f-128">Count*</span></span> |<span data-ttu-id="3642f-129">Sayısı</span><span class="sxs-lookup"><span data-stu-id="3642f-129">count</span></span> |<span data-ttu-id="3642f-130">zaman birimleri toodelay Hello sayısı</span><span class="sxs-lookup"><span data-stu-id="3642f-130">hello number of time units toodelay</span></span> |
| <span data-ttu-id="3642f-131">Birim *</span><span class="sxs-lookup"><span data-stu-id="3642f-131">Unit*</span></span> |<span data-ttu-id="3642f-132">Birim</span><span class="sxs-lookup"><span data-stu-id="3642f-132">unit</span></span> |<span data-ttu-id="3642f-133">zaman birimi Hello: `Second`, `Minute`, `Hour`, veya`Day`</span><span class="sxs-lookup"><span data-stu-id="3642f-133">hello unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="3642f-134">Gecikme-eylem kadar</span><span class="sxs-lookup"><span data-stu-id="3642f-134">Delay-until action</span></span>
<span data-ttu-id="3642f-135">Bu eylem, belirtilen bir tarih/saat kadar çalıştırmak hello geciktirir.</span><span class="sxs-lookup"><span data-stu-id="3642f-135">This action delays hello run until a specified date/time.</span></span>
<span data-ttu-id="3642f-136">A * gerekli bir alan olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="3642f-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="3642f-137">Görünen ad</span><span class="sxs-lookup"><span data-stu-id="3642f-137">Display name</span></span> | <span data-ttu-id="3642f-138">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="3642f-138">Property name</span></span> | <span data-ttu-id="3642f-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3642f-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3642f-140">Yıl *</span><span class="sxs-lookup"><span data-stu-id="3642f-140">Year*</span></span> |<span data-ttu-id="3642f-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="3642f-141">timestamp</span></span> |<span data-ttu-id="3642f-142">(GMT) kadar Hello yıl toodelay</span><span class="sxs-lookup"><span data-stu-id="3642f-142">hello year toodelay until (GMT)</span></span> |
| <span data-ttu-id="3642f-143">Ay *</span><span class="sxs-lookup"><span data-stu-id="3642f-143">Month*</span></span> |<span data-ttu-id="3642f-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="3642f-144">timestamp</span></span> |<span data-ttu-id="3642f-145">(GMT) kadar Hello ay toodelay</span><span class="sxs-lookup"><span data-stu-id="3642f-145">hello month toodelay until (GMT)</span></span> |
| <span data-ttu-id="3642f-146">Gün *</span><span class="sxs-lookup"><span data-stu-id="3642f-146">Day*</span></span> |<span data-ttu-id="3642f-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="3642f-147">timestamp</span></span> |<span data-ttu-id="3642f-148">(GMT) kadar Hello gün toodelay</span><span class="sxs-lookup"><span data-stu-id="3642f-148">hello day toodelay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="3642f-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3642f-149">Next steps</span></span>
<span data-ttu-id="3642f-150">Şimdi, hello platform deneyin ve [mantıksal uygulama oluşturma](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3642f-150">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="3642f-151">Keşfedebilirsiniz bakarak logic apps içinde kullanılabilir diğer bağlayıcıları hello bizim [API'leri listesi](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="3642f-151">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

