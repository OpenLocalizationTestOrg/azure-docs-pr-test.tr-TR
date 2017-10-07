---
title: "aaaCreate ve hello Azure portal'ın eylem gruplarını yönetme | Microsoft Docs"
description: "Bilgi nasıl toocreate hello Azure portal'ın Eylem grupları ve yönetin."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: ancav
ms.openlocfilehash: 97e0b22bea7787fff6856f895a7e6256c177efd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-action-groups-in-hello-azure-portal"></a><span data-ttu-id="352e1-103">Hello Azure portal'ın eylem gruplarını oluşturma ve yönetme</span><span class="sxs-lookup"><span data-stu-id="352e1-103">Create and manage action groups in hello Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="352e1-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="352e1-104">Overview</span></span> ##
<span data-ttu-id="352e1-105">Bu makale size nasıl gösterir toocreate hello Azure portal'ın Eylem grupları ve yönetin.</span><span class="sxs-lookup"><span data-stu-id="352e1-105">This article shows you how toocreate and manage action groups in hello Azure portal.</span></span>

<span data-ttu-id="352e1-106">Eylem gruplarıyla eylemlerin bir listesini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="352e1-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="352e1-107">Etkinlik günlüğü uyarıları tanımlarken bu gruplar daha sonra kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="352e1-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="352e1-108">Bu gruplar daha sonra aynı eylemleri hello etkinlik günlüğü uyarısı her tetiklenişinde alınır, hello sağlama tanımlamak her etkinlik günlüğü uyarı tarafından yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="352e1-108">These groups can then be reused by each activity log alert you define, ensuring that hello same actions are taken each time hello activity log alert is triggered.</span></span>

<span data-ttu-id="352e1-109">Bir eylem grubu, her eylem türü too10 olabilir.</span><span class="sxs-lookup"><span data-stu-id="352e1-109">An action group can have up too10 of each action type.</span></span> <span data-ttu-id="352e1-110">Her eylem aşağıdaki özelliklere hello oluşur:</span><span class="sxs-lookup"><span data-stu-id="352e1-110">Each action is made up of hello following properties:</span></span>

* <span data-ttu-id="352e1-111">**Ad**: hello eylem grubu içinde benzersiz bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="352e1-111">**Name**: A unique identifier within hello action group.</span></span>  
* <span data-ttu-id="352e1-112">**Eylem türü**: bir SMS gönder, bir e-posta gönderme veya bir Web kancası çağırın.</span><span class="sxs-lookup"><span data-stu-id="352e1-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="352e1-113">**Ayrıntılar**: karşılık gelen telefon numarası, e-posta adresi veya Web kancası URI hello.</span><span class="sxs-lookup"><span data-stu-id="352e1-113">**Details**: hello corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="352e1-114">Hakkında bilgi için bkz: toouse Azure Resource Manager şablonları tooconfigure Eylem grupları, [eylem Grup Resource Manager şablonları](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="352e1-114">For information on how toouse Azure Resource Manager templates tooconfigure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="352e1-115">Hello Azure portal kullanarak bir eylem grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="352e1-115">Create an action group by using hello Azure portal</span></span> ##
1. <span data-ttu-id="352e1-116">Merhaba, [portal](https://portal.azure.com)seçin **İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="352e1-116">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="352e1-117">Merhaba **İzleyici** dikey penceresinde, izleme ayarları ve verileri tek bir görünümde birleştirir.</span><span class="sxs-lookup"><span data-stu-id="352e1-117">hello **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    ![Merhaba "İzleme" hizmeti](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="352e1-119">Merhaba, **etkinlik günlüğü** bölümünde, select **Eylem grupları**.</span><span class="sxs-lookup"><span data-stu-id="352e1-119">In hello **Activity log** section, select **Action groups**.</span></span>

    ![Merhaba "Eylem grupları" sekmesi](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="352e1-121">Seçin **eylem Grup Ekle**ve hello alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="352e1-121">Select **Add action group**, and fill in hello fields.</span></span>

    ![Merhaba "Eylem Grup Ekle" komutu](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="352e1-123">Hello bir ad girin **eylem grup adı** kutusunda ve hello bir ad girin **kısa ad** kutusu.</span><span class="sxs-lookup"><span data-stu-id="352e1-123">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="352e1-124">Bu grubun kullanarak bildirimler gönderildiğinde hello kısa adı yerine bir tam eylem grup adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="352e1-124">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![Merhaba eylem Grup Ekle"iletişim kutusu](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="352e1-126">Merhaba **abonelik** kutusuna geçerli aboneliğiniz ile autofills.</span><span class="sxs-lookup"><span data-stu-id="352e1-126">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="352e1-127">Bu abonelik, hangi hello eylem grubu kaydedildi hello bir olur.</span><span class="sxs-lookup"><span data-stu-id="352e1-127">This subscription is hello one in which hello action group is saved.</span></span>

6. <span data-ttu-id="352e1-128">Select hello **kaynak grubu** hangi hello eylemde Grup kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="352e1-128">Select hello **Resource group** in which hello action group is saved.</span></span>

7. <span data-ttu-id="352e1-129">Eylemlerin bir listesini, her eylemin sağlayarak tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="352e1-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="352e1-130">a.</span><span class="sxs-lookup"><span data-stu-id="352e1-130">a.</span></span> <span data-ttu-id="352e1-131">**Ad**: Bu eylem için benzersiz bir tanımlayıcı girin.</span><span class="sxs-lookup"><span data-stu-id="352e1-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="352e1-132">b.</span><span class="sxs-lookup"><span data-stu-id="352e1-132">b.</span></span> <span data-ttu-id="352e1-133">**Eylem türü**: SMS seçin, e-posta veya Web kancası.</span><span class="sxs-lookup"><span data-stu-id="352e1-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="352e1-134">c.</span><span class="sxs-lookup"><span data-stu-id="352e1-134">c.</span></span> <span data-ttu-id="352e1-135">**Ayrıntılar**: hello eylem türüne bağlı olarak, bir telefon numarası, e-posta adresi veya Web kancası URI girin.</span><span class="sxs-lookup"><span data-stu-id="352e1-135">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="352e1-136">Seçin **Tamam** toocreate hello eylem grubu.</span><span class="sxs-lookup"><span data-stu-id="352e1-136">Select **OK** toocreate hello action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="352e1-137">Eylem gruplarınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="352e1-137">Manage your action groups</span></span> ##
<span data-ttu-id="352e1-138">Bir eylem grubu oluşturduktan sonra hello görünür **Eylem grupları** hello bölümünü **İzleyici** dikey.</span><span class="sxs-lookup"><span data-stu-id="352e1-138">After you create an action group, it's visible in hello **Action groups** section of hello **Monitor** blade.</span></span> <span data-ttu-id="352e1-139">Toomanage için istediğiniz hello eylem grubunu seçin:</span><span class="sxs-lookup"><span data-stu-id="352e1-139">Select hello action group you want toomanage to:</span></span>

* <span data-ttu-id="352e1-140">Ekleme, düzenleme veya Eylemler kaldırma.</span><span class="sxs-lookup"><span data-stu-id="352e1-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="352e1-141">Merhaba eylem grubunu silin.</span><span class="sxs-lookup"><span data-stu-id="352e1-141">Delete hello action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="352e1-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="352e1-142">Next steps</span></span> ##
* <span data-ttu-id="352e1-143">Daha fazla bilgi edinmek [SMS uyarı davranış](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="352e1-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="352e1-144">Geçirmesine bir [hello etkinlik günlüğü uyarı Web kancası şeması anlama](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="352e1-144">Gain an [understanding of hello activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="352e1-145">Daha fazla bilgi edinmek [hız sınırlaması](monitoring-alerts-rate-limiting.md) uyarılar hakkında.</span><span class="sxs-lookup"><span data-stu-id="352e1-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="352e1-146">Alma bir [etkinlik günlüğü uyarıları genel bakış](monitoring-overview-alerts.md)ve öğrenin nasıl tooreceive uyarıları.</span><span class="sxs-lookup"><span data-stu-id="352e1-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="352e1-147">Nasıl çok öğrenin[hizmeti sistem durumu bildirimi gönderilen her uyarıları yapılandırmak](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="352e1-147">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
