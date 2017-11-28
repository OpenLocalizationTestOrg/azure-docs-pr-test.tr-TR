---
title: "aaaCreate etkinlik günlüğü uyarıları | Microsoft Docs"
description: "Merhaba etkinlik günlüğünde belirli olaylar meydana geldiğinde, SMS, Web kancası ve e-posta bildirilmesi."
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
ms.date: 08/03/2017
ms.author: johnkem
ms.openlocfilehash: ba0716cc12a0b3a0024ee5562a025f3f153f8982
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-activity-log-alerts"></a><span data-ttu-id="67508-103">Etkinlik günlüğü uyarı oluşturma</span><span class="sxs-lookup"><span data-stu-id="67508-103">Create activity log alerts</span></span>

## <a name="overview"></a><span data-ttu-id="67508-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="67508-104">Overview</span></span>
<span data-ttu-id="67508-105">Etkinlik günlüğü yeni bir etkinlik günlüğü olay oluştuğunda etkinleştirme uyarılar eşleşen hello uyarıda belirtilen hello koşullarına uyarılar.</span><span class="sxs-lookup"><span data-stu-id="67508-105">Activity log alerts are alerts that activate when a new activity log event occurs that matches hello conditions specified in hello alert.</span></span> <span data-ttu-id="67508-106">Bunlar Azure kaynaklarını; dolayısıyla bir Azure Resource Manager şablonu kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="67508-106">They are Azure resources, so they can be created by using an Azure Resource Manager template.</span></span> <span data-ttu-id="67508-107">Bunlar ayrıca oluşturulabilir, güncelleştirilmiş veya hello Azure portal silindi.</span><span class="sxs-lookup"><span data-stu-id="67508-107">They also can be created, updated, or deleted in hello Azure portal.</span></span> <span data-ttu-id="67508-108">Bu makalede, etkinlik günlüğü uyarıları hello kavramları tanıtır.</span><span class="sxs-lookup"><span data-stu-id="67508-108">This article introduces hello concepts behind activity log alerts.</span></span> <span data-ttu-id="67508-109">Ardından size nasıl toouse hello etkinlik günlüğü olaylarını üzerinde bir uyarı oluşturan Azure portal tooset gösterir.</span><span class="sxs-lookup"><span data-stu-id="67508-109">It then shows you how toouse hello Azure portal tooset up an alert on activity log events.</span></span>

<span data-ttu-id="67508-110">Etkinlik günlüğü uyarıları tooreceive bildirimleri normalde, oluşturduğunuz zaman:</span><span class="sxs-lookup"><span data-stu-id="67508-110">Typically, you create activity log alerts tooreceive notifications when:</span></span>

* <span data-ttu-id="67508-111">Azure aboneliği, genellikle kapsamlı tooparticular kaynak grupları veya kaynakları kaynaklardaki belirli değişiklikler gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="67508-111">Specific changes occur on resources in your Azure subscription, often scoped tooparticular resource groups or resources.</span></span> <span data-ttu-id="67508-112">Örneğin, myProductionResourceGroup herhangi bir sanal makine silindiğinde bildirim toobe isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67508-112">For example, you might want toobe notified when any virtual machine in myProductionResourceGroup is deleted.</span></span> <span data-ttu-id="67508-113">Veya herhangi bir yeni rol tooa kullanıcı aboneliğinizde atanmışsa bildirim toobe isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67508-113">Or, you might want toobe notified if any new roles are assigned tooa user in your subscription.</span></span>
* <span data-ttu-id="67508-114">Hizmet sistem durumu olayı oluşur.</span><span class="sxs-lookup"><span data-stu-id="67508-114">A service health event occurs.</span></span> <span data-ttu-id="67508-115">Hizmet sistem durumu olayları olaylar ve aboneliğinizde tooresources uygulamak bakım olayları bildirimi içerir.</span><span class="sxs-lookup"><span data-stu-id="67508-115">Service health events include notification of incidents and maintenance events that apply tooresources in your subscription.</span></span>

<span data-ttu-id="67508-116">Her iki durumda da, hello abonelik hangi hello uyarı oluşturulan olaylar için yalnızca bir etkinlik günlüğü uyarı izler.</span><span class="sxs-lookup"><span data-stu-id="67508-116">In either case, an activity log alert monitors only for events in hello subscription in which hello alert is created.</span></span>

<span data-ttu-id="67508-117">Hello JSON nesnesinde bir etkinlik günlüğü olayı için herhangi bir üst düzey özelliği bağlı bir etkinlik günlüğü uyarı yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="67508-117">You can configure an activity log alert based on any top-level property in hello JSON object for an activity log event.</span></span> <span data-ttu-id="67508-118">Ancak, hello portal hello en yaygın seçenekler gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="67508-118">However, hello portal shows hello most common options:</span></span>

- <span data-ttu-id="67508-119">**Kategori**: yönetici, hizmet sistem durumu, otomatik ölçeklendirme ve öneri.</span><span class="sxs-lookup"><span data-stu-id="67508-119">**Category**: Administrative, Service Health, Autoscale, and Recommendation.</span></span> <span data-ttu-id="67508-120">Daha fazla bilgi için bkz: [hello Azure etkinlik günlüğü'ne genel bakış](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span><span class="sxs-lookup"><span data-stu-id="67508-120">For more information, see [Overview of hello Azure activity log](./monitoring-overview-activity-logs.md#categories-in-the-activity-log).</span></span> <span data-ttu-id="67508-121">Hizmet sistem durumu olayları hakkında daha fazla toolearn bkz [etkinlik günlüğü Uyarıları hizmeti bildirimleri almak](./monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="67508-121">toolearn more about service health events, see [Receive activity log alerts on service notifications](./monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
- <span data-ttu-id="67508-122">**Kaynak grubu**</span><span class="sxs-lookup"><span data-stu-id="67508-122">**Resource group**</span></span>
- <span data-ttu-id="67508-123">**Kaynak**</span><span class="sxs-lookup"><span data-stu-id="67508-123">**Resource**</span></span>
- <span data-ttu-id="67508-124">**Kaynak türü**</span><span class="sxs-lookup"><span data-stu-id="67508-124">**Resource type**</span></span>
- <span data-ttu-id="67508-125">**İşlem adı**: hello kaynak yöneticisi rol tabanlı erişim denetimi işlem adı.</span><span class="sxs-lookup"><span data-stu-id="67508-125">**Operation name**: hello Resource Manager Role-Based Access Control operation name.</span></span>
- <span data-ttu-id="67508-126">**Düzey**: Merhaba (ayrıntılı bilgi, uyarı, hata veya kritik) hello olay önem derecesi.</span><span class="sxs-lookup"><span data-stu-id="67508-126">**Level**: hello severity level of hello event (Verbose, Informational, Warning, Error, or Critical).</span></span>
- <span data-ttu-id="67508-127">**Durum**: hello durum hello olayın genellikle başlatıldı, başarısız veya başarılı oldu.</span><span class="sxs-lookup"><span data-stu-id="67508-127">**Status**: hello status of hello event, typically Started, Failed, or Succeeded.</span></span>
- <span data-ttu-id="67508-128">**Olayı başlatan tarafından**: olarak da bilinen hello "çağırıcı."</span><span class="sxs-lookup"><span data-stu-id="67508-128">**Event initiated by**: Also known as hello "caller."</span></span> <span data-ttu-id="67508-129">Merhaba e-posta adresi veya hello işlemi gerçekleştiren hello kullanıcının Azure Active Directory tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="67508-129">hello email address or Azure Active Directory identifier of hello user who performed hello operation.</span></span>

>[!NOTE]
><span data-ttu-id="67508-130">En az iki bir olan ile uyarıdaki ölçütleri önceki hello belirtmelisiniz hello kategorisi.</span><span class="sxs-lookup"><span data-stu-id="67508-130">You must specify at least two of hello preceding criteria in your alert, with one being hello category.</span></span> <span data-ttu-id="67508-131">Merhaba etkinlik günlükleri her bir olay oluşturulduğunda etkinleştiren bir uyarı oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="67508-131">You may not create an alert that activates every time an event is created in hello activity logs.</span></span>
>
>

<span data-ttu-id="67508-132">Bir etkinlik günlüğü uyarı etkinleştirildiğinde, bir eylem kullanan Grup toogenerate eylemler veya bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="67508-132">When an activity log alert is activated, it uses an action group toogenerate actions or notifications.</span></span> <span data-ttu-id="67508-133">Bir eylem grubu yeniden kullanılabilir e-posta adresleri gibi bildirim alıcıları Web kancası URL'leri ya da SMS telefon numaralarının kümesidir.</span><span class="sxs-lookup"><span data-stu-id="67508-133">An action group is a reusable set of notification receivers, such as email addresses, webhook URLs, or SMS phone numbers.</span></span> <span data-ttu-id="67508-134">Merhaba alıcıları birden çok uyarıları toocentralize başvurulabilir ve bildirim kanallarını gruplayın.</span><span class="sxs-lookup"><span data-stu-id="67508-134">hello receivers can be referenced from multiple alerts toocentralize and group your notification channels.</span></span> <span data-ttu-id="67508-135">Etkinlik günlüğü Uyarınız tanımlamak için iki seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="67508-135">When you define your activity log alert, you have two options.</span></span> <span data-ttu-id="67508-136">Şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="67508-136">You can:</span></span>

* <span data-ttu-id="67508-137">Varolan bir eylem Grup etkinlik günlüğü Uyarınız kullanın.</span><span class="sxs-lookup"><span data-stu-id="67508-137">Use an existing action group in your activity log alert.</span></span> 
* <span data-ttu-id="67508-138">Yeni bir eylem grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="67508-138">Create a new action group.</span></span> 

<span data-ttu-id="67508-139">Eylem grupları hakkında daha fazla toolearn bkz [oluşturma ve eylem gruplarında hello Azure portalında yönetmek](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="67508-139">toolearn more about action groups, see [Create and manage action groups in hello Azure portal](monitoring-action-groups.md).</span></span>

<span data-ttu-id="67508-140">Hizmet durumu bildirimlerine hakkında daha fazla toolearn bkz [hizmet durumu bildirimlerine etkinlik günlüğü uyarılar alırsınız](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="67508-140">toolearn more about service health notifications, see [Receive activity log alerts on service health notifications](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>

## <a name="create-an-alert-on-an-activity-log-event-with-a-new-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="67508-141">Hello Azure portal kullanarak yeni bir eylem grubu ile etkinlik günlüğü olay bir uyarı oluştur</span><span class="sxs-lookup"><span data-stu-id="67508-141">Create an alert on an activity log event with a new action group by using hello Azure portal</span></span>
1. <span data-ttu-id="67508-142">Merhaba, [portal](https://portal.azure.com)seçin **İzleyici**.</span><span class="sxs-lookup"><span data-stu-id="67508-142">In hello [portal](https://portal.azure.com), select **Monitor**.</span></span>

    ![Merhaba "İzleme" hizmeti](./media/monitoring-activity-log-alerts/home-monitor.png)
2. <span data-ttu-id="67508-144">Merhaba, **etkinlik günlüğü** bölümünde, select **uyarıları**.</span><span class="sxs-lookup"><span data-stu-id="67508-144">In hello **Activity log** section, select **Alerts**.</span></span>

    ![Merhaba "Uyarılar" sekmesi](./media/monitoring-activity-log-alerts/alerts-blades.png)
3. <span data-ttu-id="67508-146">Seçin **etkinlik günlüğü uyarı Ekle**ve hello alanları doldurun.</span><span class="sxs-lookup"><span data-stu-id="67508-146">Select **Add activity log alert**, and fill in hello fields.</span></span>

4. <span data-ttu-id="67508-147">Hello bir ad girin **etkinlik günlüğü uyarı adı** kutusunda ve seçin bir **açıklama**.</span><span class="sxs-lookup"><span data-stu-id="67508-147">Enter a name in hello **Activity log alert name** box, and select a **Description**.</span></span>

    ![Merhaba "Etkinlik günlüğü uyarı Ekle" komutu](./media/monitoring-activity-log-alerts/add-activity-log-alert.png)

5. <span data-ttu-id="67508-149">Merhaba **abonelik** kutusuna geçerli aboneliğiniz ile autofills.</span><span class="sxs-lookup"><span data-stu-id="67508-149">hello **Subscription** box autofills with your current subscription.</span></span> <span data-ttu-id="67508-150">Bu abonelik, hangi hello eylem grubu kaydedildi hello bir olur.</span><span class="sxs-lookup"><span data-stu-id="67508-150">This subscription is hello one in which hello action group is saved.</span></span> <span data-ttu-id="67508-151">Merhaba uyarı dışarı dağıtılan toothis abonelik ve izleyiciler etkinlik günlüğü olaylarını kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="67508-151">hello alert resource is deployed toothis subscription and monitors activity log events from it.</span></span>

    ![Merhaba "etkinlik günlüğü uyarı Ekle" iletişim kutusu](./media/monitoring-activity-log-alerts/activity-log-alert-new-action-group.png)

6. <span data-ttu-id="67508-153">Select hello **kaynak grubu** hangi hello Uyarı kaynağı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="67508-153">Select hello **Resource group** in which hello alert resource is created.</span></span> <span data-ttu-id="67508-154">Bu hello uyarı tarafından izlenen hello kaynak grubu değil.</span><span class="sxs-lookup"><span data-stu-id="67508-154">This is not hello resource group that's monitored by hello alert.</span></span> <span data-ttu-id="67508-155">Bunun yerine, hello uyarı kaynağın bulunduğu hello kaynak grubu değil.</span><span class="sxs-lookup"><span data-stu-id="67508-155">Instead, it's hello resource group where hello alert resource is located.</span></span>

7. <span data-ttu-id="67508-156">İsteğe bağlı olarak, seçin bir **olay kategorisi** toomodify hello gösterilen ek filtreler.</span><span class="sxs-lookup"><span data-stu-id="67508-156">Optionally, select an **Event category** toomodify hello additional filters that are shown.</span></span> <span data-ttu-id="67508-157">Yönetim olaylar için hello filtreleri içeren **kaynak grubu**, **kaynak**, **kaynak türü**, **işlem adı**, **Düzeyi**, **durum**, ve **olayı başlatan tarafından**.</span><span class="sxs-lookup"><span data-stu-id="67508-157">For Administrative events, hello filters include **Resource group**, **Resource**, **Resource type**, **Operation name**, **Level**, **Status**, and **Event initiated by**.</span></span> <span data-ttu-id="67508-158">Bu değerleri bu uyarı izlemelidir hangi olayların tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="67508-158">These values identify which events this alert should monitor.</span></span>

    >[!NOTE]
    ><span data-ttu-id="67508-159">Merhaba, Uyarı ölçütleri önceki en az birini belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="67508-159">You must specify at least one of hello preceding criteria in your alert.</span></span> <span data-ttu-id="67508-160">Merhaba etkinlik günlükleri her bir olay oluşturulduğunda etkinleştiren bir uyarı oluşturamazsınız.</span><span class="sxs-lookup"><span data-stu-id="67508-160">You may not create an alert that activates every time an event is created in hello activity logs.</span></span>
    >
    >

8. <span data-ttu-id="67508-161">Hello bir ad girin **eylem grup adı** kutusunda ve hello bir ad girin **kısa ad** kutusu.</span><span class="sxs-lookup"><span data-stu-id="67508-161">Enter a name in hello **Action group name** box, and enter a name in hello **Short name** box.</span></span> <span data-ttu-id="67508-162">Bu grubun kullanarak bildirimler gönderildiğinde hello kısa adı yerine bir tam eylem grup adı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="67508-162">hello short name is used in place of a full action group name when notifications are sent using this group.</span></span>

9.  <span data-ttu-id="67508-163">Eylemin hello sağlayarak eylemlerin bir listesini tanımlar:</span><span class="sxs-lookup"><span data-stu-id="67508-163">Define a list of actions by providing hello action’s:</span></span>

    <span data-ttu-id="67508-164">a.</span><span class="sxs-lookup"><span data-stu-id="67508-164">a.</span></span> <span data-ttu-id="67508-165">**Ad**: hello eylemin adı, diğer ad veya tanımlayıcı girin.</span><span class="sxs-lookup"><span data-stu-id="67508-165">**Name**: Enter hello action’s name, alias, or identifier.</span></span>

    <span data-ttu-id="67508-166">b.</span><span class="sxs-lookup"><span data-stu-id="67508-166">b.</span></span> <span data-ttu-id="67508-167">**Eylem türü**: SMS seçin, e-posta veya Web kancası.</span><span class="sxs-lookup"><span data-stu-id="67508-167">**Action Type**: Select SMS, email, or webhook.</span></span>

    <span data-ttu-id="67508-168">c.</span><span class="sxs-lookup"><span data-stu-id="67508-168">c.</span></span> <span data-ttu-id="67508-169">**Ayrıntılar**: hello eylem türüne bağlı olarak, bir telefon numarası, e-posta adresi veya Web kancası URI girin.</span><span class="sxs-lookup"><span data-stu-id="67508-169">**Details**: Based on hello action type, enter a phone number, email address, or webhook URI.</span></span>

10. <span data-ttu-id="67508-170">Seçin **Tamam** toocreate hello uyarı.</span><span class="sxs-lookup"><span data-stu-id="67508-170">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="67508-171">Merhaba uyarı toofully yaymak ve etkin hale birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="67508-171">hello alert takes a few minutes toofully propagate and then become active.</span></span> <span data-ttu-id="67508-172">Yeni olaylar hello uyarının ölçütleri eşleştiğinde tetikler.</span><span class="sxs-lookup"><span data-stu-id="67508-172">It triggers when new events match hello alert's criteria.</span></span>

<span data-ttu-id="67508-173">Daha fazla bilgi için bkz: [etkinlik günlüğü uyarıları kullanılan anlayın hello Web kancası şema](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="67508-173">For more information, see [Understand hello webhook schema used in activity log alerts](monitoring-activity-log-alerts-webhook.md).</span></span>

>[!NOTE]
><span data-ttu-id="67508-174">Bu adımlarda tanımlanan hello eylem tüm gelecekteki uyarı tanımları için var olan bir eylem grubu olarak yeniden kullanılabilir grubudur.</span><span class="sxs-lookup"><span data-stu-id="67508-174">hello action group defined in these steps is reusable as an existing action group for all future alert definitions.</span></span>
>
>

## <a name="create-an-alert-on-an-activity-log-event-for-an-existing-action-group-by-using-hello-azure-portal"></a><span data-ttu-id="67508-175">Hello Azure portal kullanarak bir uyarı varolan bir eylem grup için bir etkinlik günlüğü olay oluşturma</span><span class="sxs-lookup"><span data-stu-id="67508-175">Create an alert on an activity log event for an existing action group by using hello Azure portal</span></span>
1. <span data-ttu-id="67508-176">1 ile 7'de hello önceki bölümde toocreate etkinlik günlüğü Uyarınız adımları.</span><span class="sxs-lookup"><span data-stu-id="67508-176">Follow steps 1 through 7 in hello previous section toocreate your activity log alert.</span></span>

2. <span data-ttu-id="67508-177">Altında **aracılığıyla bildir**seçin hello **varolan** eylem Grup düğmesi.</span><span class="sxs-lookup"><span data-stu-id="67508-177">Under **Notify via**, select hello **Existing** action group button.</span></span> <span data-ttu-id="67508-178">Var olan bir eylem grubunu hello listeden seçin.</span><span class="sxs-lookup"><span data-stu-id="67508-178">Select an existing action group from hello list.</span></span>

3. <span data-ttu-id="67508-179">Seçin **Tamam** toocreate hello uyarı.</span><span class="sxs-lookup"><span data-stu-id="67508-179">Select **OK** toocreate hello alert.</span></span>

<span data-ttu-id="67508-180">Merhaba uyarı toofully yaymak ve etkin hale birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="67508-180">hello alert takes a few minutes toofully propagate and then become active.</span></span> <span data-ttu-id="67508-181">Yeni olaylar hello uyarının ölçütleri eşleştiğinde tetikler.</span><span class="sxs-lookup"><span data-stu-id="67508-181">It triggers when new events match hello alert's criteria.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="67508-182">Uyarılarınızı yönetme</span><span class="sxs-lookup"><span data-stu-id="67508-182">Manage your alerts</span></span>

<span data-ttu-id="67508-183">Bir uyarı oluşturduktan sonra hello uyarıları bölümünde hello İzleyici dikey penceresinde görünür olur.</span><span class="sxs-lookup"><span data-stu-id="67508-183">After you create an alert, it's visible in hello Alerts section of hello Monitor blade.</span></span> <span data-ttu-id="67508-184">Toomanage için istediğiniz hello uyarıyı seçin:</span><span class="sxs-lookup"><span data-stu-id="67508-184">Select hello alert you want toomanage to:</span></span>

* <span data-ttu-id="67508-185">Düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="67508-185">Edit it.</span></span>
* <span data-ttu-id="67508-186">Dosyayı silin.</span><span class="sxs-lookup"><span data-stu-id="67508-186">Delete it.</span></span>
* <span data-ttu-id="67508-187">Tootemporarily durdurma veya hello uyarı bildirimleri almaya devam etmek istiyorsanız, etkinleştirmek veya devre dışı.</span><span class="sxs-lookup"><span data-stu-id="67508-187">Disable or enable it, if you want tootemporarily stop or resume receiving notifications for hello alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67508-188">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="67508-188">Next steps</span></span>
- <span data-ttu-id="67508-189">Alma bir [uyarılar genel bakış](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="67508-189">Get an [overview of alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="67508-190">Hakkında bilgi edinin [bildirim hız sınırlaması](monitoring-alerts-rate-limiting.md).</span><span class="sxs-lookup"><span data-stu-id="67508-190">Learn about [notification rate limiting](monitoring-alerts-rate-limiting.md).</span></span>
- <span data-ttu-id="67508-191">Gözden geçirme hello [etkinlik günlüğü uyarı Web kancası şeması](monitoring-activity-log-alerts-webhook.md).</span><span class="sxs-lookup"><span data-stu-id="67508-191">Review hello [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md).</span></span>
- <span data-ttu-id="67508-192">Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="67508-192">Learn more about [action groups](monitoring-action-groups.md).</span></span>  
- <span data-ttu-id="67508-193">Hakkında bilgi edinin [hizmet durumu bildirimlerine](monitoring-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="67508-193">Learn about [service health notifications](monitoring-service-notifications.md).</span></span>
- <span data-ttu-id="67508-194">Oluşturma bir [etkinliğini günlüğe uyarı toomonitor aboneliğinizi tüm otomatik ölçeklendirme altyapısı işlemler](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="67508-194">Create an [activity log alert toomonitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="67508-195">Oluşturma bir [etkinliğini günlüğe uyarı toomonitor aboneliğinizi tüm başarısız otomatik ölçeklendirme ölçek/genişletme işlemler](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="67508-195">Create an [activity log alert toomonitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
