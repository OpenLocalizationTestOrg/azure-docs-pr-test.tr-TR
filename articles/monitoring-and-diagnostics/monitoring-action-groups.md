---
title: "Azure portalında eylem gruplarını oluşturma ve yönetme | Microsoft Docs"
description: "Azure portalında eylem gruplarını oluşturma ve yönetme öğrenin."
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
ms.openlocfilehash: ea15705bf02d9773507c6cb59f2da4c1dd0f9d77
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-action-groups-in-the-azure-portal"></a><span data-ttu-id="31c96-103">Azure portalında eylem gruplarını oluşturma ve yönetme</span><span class="sxs-lookup"><span data-stu-id="31c96-103">Create and manage action groups in the Azure portal</span></span>
## <a name="overview"></a><span data-ttu-id="31c96-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="31c96-104">Overview</span></span> ##
<span data-ttu-id="31c96-105">Bu makalede, Azure portalında Eylem grupları oluşturmak ve yönetmek nasıl gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="31c96-105">This article shows you how to create and manage action groups in the Azure portal.</span></span>

<span data-ttu-id="31c96-106">Eylem gruplarıyla eylemlerin bir listesini yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31c96-106">You can configure a list of actions with action groups.</span></span> <span data-ttu-id="31c96-107">Etkinlik günlüğü uyarıları tanımlarken bu gruplar daha sonra kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="31c96-107">These groups then can be used when you define activity log alerts.</span></span> <span data-ttu-id="31c96-108">Bu gruplar daha sonra aynı eylemleri etkinlik günlüğü uyarısı her tetiklenişinde alınır sağlama tanımlamak her etkinlik günlüğü uyarı tarafından yeniden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="31c96-108">These groups can then be reused by each activity log alert you define, ensuring that the same actions are taken each time the activity log alert is triggered.</span></span>

<span data-ttu-id="31c96-109">Bir eylem grubu 10 her eylem türünde olabilir.</span><span class="sxs-lookup"><span data-stu-id="31c96-109">An action group can have up to 10 of each action type.</span></span> <span data-ttu-id="31c96-110">Her eylem aşağıdaki özellikleri oluşur:</span><span class="sxs-lookup"><span data-stu-id="31c96-110">Each action is made up of the following properties:</span></span>

* <span data-ttu-id="31c96-111">**Ad**: eylem grubu içinde benzersiz bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="31c96-111">**Name**: A unique identifier within the action group.</span></span>  
* <span data-ttu-id="31c96-112">**Eylem türü**: bir SMS gönder, bir e-posta gönderme veya bir Web kancası çağırın.</span><span class="sxs-lookup"><span data-stu-id="31c96-112">**Action type**: Send an SMS, send an email, or call a webhook.</span></span>  
* <span data-ttu-id="31c96-113">**Ayrıntılar**: karşılık gelen telefon numarası, e-posta adresi veya Web kancası URI.</span><span class="sxs-lookup"><span data-stu-id="31c96-113">**Details**: The corresponding phone number, email address, or webhook URI.</span></span>

<span data-ttu-id="31c96-114">Eylem grupları yapılandırmak için Azure Resource Manager şablonları kullanma hakkında daha fazla bilgi için bkz: [eylem Grup Resource Manager şablonları](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="31c96-114">For information on how to use Azure Resource Manager templates to configure action groups, see [Action group Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md).</span></span>

## <a name="create-an-action-group-by-using-the-azure-portal"></a><span data-ttu-id="31c96-115">Azure portalını kullanarak bir eylem grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="31c96-115">Create an action group by using the Azure portal</span></span> ##
1. <span data-ttu-id="31c96-116">İçinde [portal](https://portal.azure.com)seçin **İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="31c96-116">In the [portal](https://portal.azure.com), select **Monitor**.</span></span> <span data-ttu-id="31c96-117">**İzleyici** dikey penceresinde, izleme ayarları ve verileri tek bir görünümde birleştirir.</span><span class="sxs-lookup"><span data-stu-id="31c96-117">The **Monitor** blade consolidates all your monitoring settings and data in one view.</span></span>

    !["İzleme" hizmeti](./media/monitoring-action-groups/home-monitor.png)
2. <span data-ttu-id="31c96-119">İçinde **etkinlik günlüğü** bölümünde, select **Eylem grupları**.</span><span class="sxs-lookup"><span data-stu-id="31c96-119">In the **Activity log** section, select **Action groups**.</span></span>

    !["Eylem grupları" sekmesi](./media/monitoring-action-groups/action-groups-blade.png)
3. <span data-ttu-id="31c96-121">Seçin **eylem Grup Ekle**ve alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="31c96-121">Select **Add action group**, and fill in the fields.</span></span>

    !["Eylem Grup Ekle" komutu](./media/monitoring-action-groups/add-action-group.png)
4. <span data-ttu-id="31c96-123">Bir ad girin **eylem grup adı** kutu ve bir ad girin **kısa ad** kutusu.</span><span class="sxs-lookup"><span data-stu-id="31c96-123">Enter a name in the **Action group name** box, and enter a name in the **Short name** box.</span></span> <span data-ttu-id="31c96-124">Bu grubun kullanarak bildirimler gönderildiğinde kısa adı yerine bir tam eylem grup adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="31c96-124">The short name is used in place of a full action group name when notifications are sent using this group.</span></span>

      ![Eylem Grup Ekle"iletişim kutusu](./media/monitoring-action-groups/action-group-define.png)

5. <span data-ttu-id="31c96-126">**Abonelik** kutusuna geçerli aboneliğiniz ile autofills.</span><span class="sxs-lookup"><span data-stu-id="31c96-126">The **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="31c96-127">Bu abonelik eylem grubunu kaydedildiği adrestir.</span><span class="sxs-lookup"><span data-stu-id="31c96-127">This subscription is the one in which the action group is saved.</span></span>

6. <span data-ttu-id="31c96-128">Seçin **kaynak grubu** eylem grubunu kaydedildiği içinde.</span><span class="sxs-lookup"><span data-stu-id="31c96-128">Select the **Resource group** in which the action group is saved.</span></span>

7. <span data-ttu-id="31c96-129">Eylemlerin bir listesini, her eylemin sağlayarak tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="31c96-129">Define a list of actions by providing each action's:</span></span>

    <span data-ttu-id="31c96-130">a.</span><span class="sxs-lookup"><span data-stu-id="31c96-130">a.</span></span> <span data-ttu-id="31c96-131">**Ad**: Bu eylem için benzersiz bir tanımlayıcı girin.</span><span class="sxs-lookup"><span data-stu-id="31c96-131">**Name**: Enter a unique identifier for this action.</span></span>

    <span data-ttu-id="31c96-132">b.</span><span class="sxs-lookup"><span data-stu-id="31c96-132">b.</span></span> <span data-ttu-id="31c96-133">**Eylem türü**: SMS seçin, e-posta veya Web kancası.</span><span class="sxs-lookup"><span data-stu-id="31c96-133">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="31c96-134">c.</span><span class="sxs-lookup"><span data-stu-id="31c96-134">c.</span></span> <span data-ttu-id="31c96-135">**Ayrıntılar**: eylem türüne bağlı olarak, bir telefon numarası, e-posta adresi veya Web kancası URI girin.</span><span class="sxs-lookup"><span data-stu-id="31c96-135">**Details**: Based on the action type, enter a phone number, email address, or webhook URI.</span></span>

8. <span data-ttu-id="31c96-136">Seçin **Tamam** eylem grubu oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="31c96-136">Select **OK** to create the action group.</span></span>

## <a name="manage-your-action-groups"></a><span data-ttu-id="31c96-137">Eylem gruplarınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="31c96-137">Manage your action groups</span></span> ##
<span data-ttu-id="31c96-138">Bir eylem grubu oluşturduktan sonra görünür **Eylem grupları** bölümünü **İzleyici** dikey.</span><span class="sxs-lookup"><span data-stu-id="31c96-138">After you create an action group, it's visible in the **Action groups** section of the **Monitor** blade.</span></span> <span data-ttu-id="31c96-139">Yönetmek istediğiniz eylem grubunu seçin:</span><span class="sxs-lookup"><span data-stu-id="31c96-139">Select the action group you want to manage to:</span></span>

* <span data-ttu-id="31c96-140">Ekleme, düzenleme veya Eylemler kaldırma.</span><span class="sxs-lookup"><span data-stu-id="31c96-140">Add, edit, or remove actions.</span></span>
* <span data-ttu-id="31c96-141">Eylem grubunu silin.</span><span class="sxs-lookup"><span data-stu-id="31c96-141">Delete the action group.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31c96-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="31c96-142">Next steps</span></span> ##
* <span data-ttu-id="31c96-143">Daha fazla bilgi edinmek [SMS uyarı davranış](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="31c96-143">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>  
* <span data-ttu-id="31c96-144">Geçirmesine bir [etkinlik günlüğü uyarı Web kancası şeması anlama](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="31c96-144">Gain an [understanding of the activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>  
* <span data-ttu-id="31c96-145">Daha fazla bilgi edinmek [hız sınırlaması](monitoring-alerts-rate-limiting.md) uyarılar hakkında.</span><span class="sxs-lookup"><span data-stu-id="31c96-145">Learn more about [rate limiting](monitoring-alerts-rate-limiting.md) on alerts.</span></span> 
* <span data-ttu-id="31c96-146">Alma bir [etkinlik günlüğü uyarıları genel bakış](monitoring-overview-alerts.md)ve uyarıların nasıl alınacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="31c96-146">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="31c96-147">Bilgi edinmek için nasıl [hizmeti sistem durumu bildirimi gönderilen her uyarıları yapılandırmak](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="31c96-147">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
