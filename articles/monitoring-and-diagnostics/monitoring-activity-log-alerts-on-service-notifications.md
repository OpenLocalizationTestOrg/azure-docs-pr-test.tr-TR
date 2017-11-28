---
title: "aaaReceive etkinlik günlüğü Uyarıları hizmeti bildirimleri | Microsoft Docs"
description: "Azure hizmet ortaya çıktığında, SMS, e-posta veya Web kancası aracılığıyla bilgi edinin."
author: johnkemnetz
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
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: dd35e8f39d2a522efdae4dfed20779c992c1dd27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts-on-service-notifications"></a><span data-ttu-id="82214-103">Etkinlik günlüğü Uyarıları hizmeti bildirimlerinin oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82214-103">Create activity log alerts on service notifications</span></span>
## <a name="overview"></a><span data-ttu-id="82214-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="82214-104">Overview</span></span>
<span data-ttu-id="82214-105">Bu makale size nasıl hello Azure portal kullanarak tooset etkinlik günlüğü yedeklemek için hizmet durumu bildirimlerine uyarıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="82214-105">This article shows you how tooset up activity log alerts for service health notifications by using hello Azure portal.</span></span>  

<span data-ttu-id="82214-106">Azure hizmet durumu bildirimleri tooyour Azure aboneliği gönderdiğinde bir uyarı alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="82214-106">You can receive an alert when Azure sends service health notifications tooyour Azure subscription.</span></span> <span data-ttu-id="82214-107">Temel hello uyarı yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="82214-107">You can configure hello alert based on:</span></span>

- <span data-ttu-id="82214-108">hizmeti sistem durumu bildirimi (olay, bakım, bilgi, vb.) Hello sınıfı.</span><span class="sxs-lookup"><span data-stu-id="82214-108">hello class of service health notification (incident, maintenance, information, etc.).</span></span>
- <span data-ttu-id="82214-109">Etkilenen hello hizmetlere.</span><span class="sxs-lookup"><span data-stu-id="82214-109">hello service(s) affected.</span></span>
- <span data-ttu-id="82214-110">Etkilenen hello bilgiler.</span><span class="sxs-lookup"><span data-stu-id="82214-110">hello region(s) affected.</span></span>
- <span data-ttu-id="82214-111">Merhaba bildirim (karşılaştırması çözümlenen etkin) Hello durumu.</span><span class="sxs-lookup"><span data-stu-id="82214-111">hello status of hello notification (active vs. resolved).</span></span>
- <span data-ttu-id="82214-112">Merhaba düzeyi hello bildirimler (bilgi, uyarı, hatası).</span><span class="sxs-lookup"><span data-stu-id="82214-112">hello level of hello notifications (informational, warning, error).</span></span>

<span data-ttu-id="82214-113">Kimin hello uyarı göndermesi gerektiğini de yapılandırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="82214-113">You also can configure who hello alert should be sent to:</span></span>

- <span data-ttu-id="82214-114">Var olan bir eylem grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="82214-114">Select an existing action group.</span></span>
- <span data-ttu-id="82214-115">(Bu uyarılar için kullanılabilir) yeni bir eylem grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="82214-115">Create a new action group (that can be used for future alerts).</span></span>

<span data-ttu-id="82214-116">Eylem grupları hakkında daha fazla toolearn bkz [oluşturma ve eylem gruplarını yönetme](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="82214-116">toolearn more about action groups, see [Create and manage action groups](monitoring-action-groups.md).</span></span>

<span data-ttu-id="82214-117">Azure Resource Manager şablonları kullanarak nasıl uyarılar tooconfigure hizmet sistem durumu bildirimi hakkında daha fazla bilgi için bkz: [Resource Manager şablonları](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="82214-117">For information on how tooconfigure service health notification alerts by using Azure Resource Manager templates, see [Resource Manager templates](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>

## <a name="create-an-alert-on-a-service-health-notification-for-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="82214-118">Hello Azure portal kullanarak bir uyarı yeni bir eylem grubu için bir hizmet sistem durumu bildirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="82214-118">Create an alert on a service health notification for a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="82214-119">Merhaba, [portal](https://portal.azure.com)seçin **İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="82214-119">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Merhaba "İzleme" hizmeti](./media/monitoring-activity-log-alerts-on-service-notifications/home-monitor.png)

2. <span data-ttu-id="82214-121">Merhaba, **etkinlik günlüğü** bölümünde, select **uyarıları**.</span><span class="sxs-lookup"><span data-stu-id="82214-121">In hello **Activity log** section, select **Alerts**.</span></span>

    ![Merhaba "Uyarılar" sekmesi](./media/monitoring-activity-log-alerts-on-service-notifications/alerts-blades.png)

3. <span data-ttu-id="82214-123">Seçin **etkinlik günlüğü uyarı Ekle**ve hello alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="82214-123">Select **Add activity log alert**, and fill in hello fields.</span></span>

    ![Merhaba "Etkinlik günlüğü uyarı Ekle" komutu](./media/monitoring-activity-log-alerts-on-service-notifications/add-activity-log-alert.png)

4. <span data-ttu-id="82214-125">Hello bir ad girin **etkinlik günlüğü uyarı adı** kutusuna ve sağlayan bir **açıklama**.</span><span class="sxs-lookup"><span data-stu-id="82214-125">Enter a name in hello **Activity log alert name** box, and provide a **Description**.</span></span>

    ![Merhaba "etkinlik günlüğü uyarı Ekle" iletişim kutusu](./media/monitoring-activity-log-alerts-on-service-notifications/activity-log-alert-service-notification-new-action-group.png)

5. <span data-ttu-id="82214-127">Merhaba **abonelik** kutusuna geçerli aboneliğiniz ile autofills.</span><span class="sxs-lookup"><span data-stu-id="82214-127">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="82214-128">Bu abonelik kullanılan toosave hello etkinlik günlüğü uyarı belirtir.</span><span class="sxs-lookup"><span data-stu-id="82214-128">This subscription is used toosave hello activity log alert.</span></span> <span data-ttu-id="82214-129">Merhaba uyarı hello etkinlik günlüğü için bu dağıtılan toothis abonelik ve izleyiciler olayları kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="82214-129">hello alert resource is deployed toothis subscription and monitors events in hello activity log for it.</span></span>

6. <span data-ttu-id="82214-130">Select hello **kaynak grubu** hangi hello Uyarı kaynağı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="82214-130">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="82214-131">Merhaba uyarı tarafından izlenen hello kaynak grubu değil.</span><span class="sxs-lookup"><span data-stu-id="82214-131">This isn't hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="82214-132">Bunun yerine, hello uyarı kaynağın bulunduğu hello kaynak grubu değil.</span><span class="sxs-lookup"><span data-stu-id="82214-132">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="82214-133">Merhaba, **olay kategorisi** kutusunda **hizmet durumu**.</span><span class="sxs-lookup"><span data-stu-id="82214-133">In hello **Event category** box, select **Service Health**.</span></span> <span data-ttu-id="82214-134">İsteğe bağlı olarak, hello seçin **hizmet**, **bölge**, **türü**, **durum**, ve **düzeyi** hizmeti Sistem durumu bildirimleri tooreceive istiyor.</span><span class="sxs-lookup"><span data-stu-id="82214-134">Optionally, select hello **Service**, **Region**, **Type**, **Status**, and **Level** of service health notifications that you want tooreceive.</span></span>

8. <span data-ttu-id="82214-135">Altında **aracılığıyla uyarı**seçin hello **yeni** eylem Grup düğmesi.</span><span class="sxs-lookup"><span data-stu-id="82214-135">Under **Alert via**, select hello **New** action group button.</span></span> <span data-ttu-id="82214-136">Hello bir ad girin **eylem grup adı** kutusunda ve hello bir ad girin **kısa ad** kutusu.</span><span class="sxs-lookup"><span data-stu-id="82214-136">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="82214-137">Bu uyarı oluşturulduğunda, gönderilen hello bildirimleri Hello kısa ad başvuruluyor.</span><span class="sxs-lookup"><span data-stu-id="82214-137">hello short name is referenced in hello notifications that are sent when this alert fires.</span></span>

9. <span data-ttu-id="82214-138">Alıcıları listesini hello alıcının sağlayarak tanımlayın:</span><span class="sxs-lookup"><span data-stu-id="82214-138">Define a list of receivers by providing hello receiver's:</span></span>

    <span data-ttu-id="82214-139">a.</span><span class="sxs-lookup"><span data-stu-id="82214-139">a.</span></span> <span data-ttu-id="82214-140">**Ad**: hello alıcının adını, diğer ad veya tanımlayıcı girin.</span><span class="sxs-lookup"><span data-stu-id="82214-140">**Name**: Enter hello receiver’s name, alias, or identifier.</span></span>

    <span data-ttu-id="82214-141">b.</span><span class="sxs-lookup"><span data-stu-id="82214-141">b.</span></span> <span data-ttu-id="82214-142">**Eylem türü**: SMS seçin, e-posta veya Web kancası.</span><span class="sxs-lookup"><span data-stu-id="82214-142">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="82214-143">c.</span><span class="sxs-lookup"><span data-stu-id="82214-143">c.</span></span> <span data-ttu-id="82214-144">**Ayrıntılar**: seçilen hello eylem türüne bağlı olarak, bir telefon numarası, e-posta adresi veya Web kancası URI girin.</span><span class="sxs-lookup"><span data-stu-id="82214-144">**Details**: Based on hello action type chosen, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="82214-145">Seçin **Tamam** toocreate hello uyarı.</span><span class="sxs-lookup"><span data-stu-id="82214-145">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="82214-146">Birkaç dakika içinde hello etkindir ve uyarı oluşturma sırasında belirtilen hello koşullarına göre tootrigger başlar.</span><span class="sxs-lookup"><span data-stu-id="82214-146">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

<span data-ttu-id="82214-147">Etkinlik günlüğü uyarıları için hello Web kancası şeması hakkında daha fazla bilgi için bkz: [Azure etkinlik için Web kancası oturum uyarıları](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="82214-147">For information on hello webhook schema for activity log alerts, see [Webhooks for Azure activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="82214-148">Bu adımlarda tanımlanan hello eylem tüm gelecekteki uyarı tanımları için var olan bir eylem grubu olarak yeniden kullanılabilir grubudur.</span><span class="sxs-lookup"><span data-stu-id="82214-148">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-a-service-health-notification-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="82214-149">Hello Azure portal kullanarak bir uyarı varolan bir eylem grup için bir hizmet sistem durumu bildirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="82214-149">Create an alert on a service health notification for an existing action group by using hello Azure portal</span></span>

1. <span data-ttu-id="82214-150">1 ile 7'de hello önceki bölümde toocreate hizmeti sistem durumu bildirimi adımları.</span><span class="sxs-lookup"><span data-stu-id="82214-150">Follow steps 1 through 7 in hello previous section toocreate your service health notification.</span></span> 

2. <span data-ttu-id="82214-151">Altında **aracılığıyla uyarı**seçin hello **varolan** eylem Grup düğmesi.</span><span class="sxs-lookup"><span data-stu-id="82214-151">Under **Alert via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="82214-152">Merhaba uygun eylemi grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="82214-152">Select hello appropriate action group.</span></span>

3. <span data-ttu-id="82214-153">Seçin **Tamam** toocreate hello uyarı.</span><span class="sxs-lookup"><span data-stu-id="82214-153">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="82214-154">Birkaç dakika içinde hello etkindir ve uyarı oluşturma sırasında belirtilen hello koşullarına göre tootrigger başlar.</span><span class="sxs-lookup"><span data-stu-id="82214-154">Within a few minutes, hello alert is active and begins tootrigger based on hello conditions you specified during creation.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="82214-155">Uyarılarınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="82214-155">Manage your alerts</span></span>

<span data-ttu-id="82214-156">Bir uyarı oluşturduktan sonra hello görünür **uyarıları** hello bölümünü **İzleyici** dikey.</span><span class="sxs-lookup"><span data-stu-id="82214-156">After you create an alert, it's visible in hello **Alerts** section of hello **Monitor** blade.</span></span> <span data-ttu-id="82214-157">Toomanage için istediğiniz hello uyarıyı seçin:</span><span class="sxs-lookup"><span data-stu-id="82214-157">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="82214-158">Düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="82214-158">Edit it.</span></span>
* <span data-ttu-id="82214-159">Dosyayı silin.</span><span class="sxs-lookup"><span data-stu-id="82214-159">Delete it.</span></span>
* <span data-ttu-id="82214-160">Tootemporarily durdurma veya hello uyarı bildirimleri almaya devam etmek istiyorsanız, etkinleştirmek veya devre dışı.</span><span class="sxs-lookup"><span data-stu-id="82214-160">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82214-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="82214-161">Next steps</span></span>
- <span data-ttu-id="82214-162">Hakkında bilgi edinin [hizmet durumu bildirimlerine](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="82214-162">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="82214-163">Hakkında bilgi edinin [bildirim hız sınırlaması](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="82214-163">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="82214-164">Gözden geçirme hello [etkinlik günlüğü uyarı Web kancası şeması](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="82214-164">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="82214-165">Alma bir [etkinlik günlüğü uyarıları genel bakış](monitoring-overview-alerts.md)ve öğrenin nasıl tooreceive uyarıları.</span><span class="sxs-lookup"><span data-stu-id="82214-165">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span> 
- <span data-ttu-id="82214-166">Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="82214-166">Learn more about [action groups](monitoring-action-groups.md).</span></span>
