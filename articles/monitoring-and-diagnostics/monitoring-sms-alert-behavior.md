---
title: "Eylem grupları uyarı davranışını aaaSMS | Microsoft Docs"
description: "SMS ileti biçimi ve yanıt veren tooSMS iletileri toounsubscribe resubscribe veya Yardım isteyin."
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
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="d81ab-103">SMS eylemi gruplarındaki davranışı uyar</span><span class="sxs-lookup"><span data-stu-id="d81ab-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="d81ab-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d81ab-104">Overview</span></span> ##
<span data-ttu-id="d81ab-105">Eylem grupları tooconfigure alıcıları listesini etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="d81ab-105">Action groups enable you tooconfigure a list of receivers.</span></span> <span data-ttu-id="d81ab-106">Bu gruplar daha sonra etkinlik günlüğü uyarıları tanımlarken yararlanılabilir; Hello etkinlik günlüğü uyarı tetiklendiğinde, belirli bir eylem grubu bildirim sağlama.</span><span class="sxs-lookup"><span data-stu-id="d81ab-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when hello activity log alert is triggered.</span></span> <span data-ttu-id="d81ab-107">Mekanizmaları desteklenen uyarı hello SMS biridir; Merhaba uyarıları çift yönlü iletişimi destekler.</span><span class="sxs-lookup"><span data-stu-id="d81ab-107">One of hello alerting mechanisms supported is SMS; hello alerts support bi-directional communication.</span></span> <span data-ttu-id="d81ab-108">Bir kullanıcı tooan uyarısını yanıt verebilir:</span><span class="sxs-lookup"><span data-stu-id="d81ab-108">A user can respond tooan alert to:</span></span>

- <span data-ttu-id="d81ab-109">**Uyarılardan aboneliği:** bir kullanıcı tüm Eylem grupları veya tekil eylem grubu için tüm SMS uyarılardan aboneliğinizi iptal edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d81ab-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="d81ab-110">**Tooalerts resubscribe:** tooall SMS uyarıları tüm Eylem grupları veya tekil eylem grup için bir kullanıcı resubscribe.</span><span class="sxs-lookup"><span data-stu-id="d81ab-110">**Resubscribe tooalerts:** A user can resubscribe tooall SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="d81ab-111">**Yardım isteğinde:** kullanıcı hello SMS hakkında daha fazla bilgi isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="d81ab-111">**Request help:** A user can ask for more information on hello SMS.</span></span> <span data-ttu-id="d81ab-112">Yeniden yönlendirilen toothis makale olacaktır</span><span class="sxs-lookup"><span data-stu-id="d81ab-112">They will be redirected toothis article</span></span>

<span data-ttu-id="d81ab-113">Bu makalede hello SMS uyarıları hello davranışını yer almaktadır ve hello yanıt eylemleri hello kullanıcı hello kullanıcı hello yerel ayar temel alabilir:</span><span class="sxs-lookup"><span data-stu-id="d81ab-113">This article covers hello behavior of hello SMS alerts and hello response actions hello user can take based on hello locale of hello user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="d81ab-114">ABD/Kanada SMS davranışı</span><span class="sxs-lookup"><span data-stu-id="d81ab-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="d81ab-115">SMS uyarı alma</span><span class="sxs-lookup"><span data-stu-id="d81ab-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="d81ab-116">Bir uyarı oluşturulduğunda bir eylem grubunun bir parçası yapılandırılmış bir SMS alıcı SMS alır.</span><span class="sxs-lookup"><span data-stu-id="d81ab-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="d81ab-117">Merhaba SMS bilgisinden hello yürütecek:</span><span class="sxs-lookup"><span data-stu-id="d81ab-117">hello SMS will carry hello following information:</span></span>
* <span data-ttu-id="d81ab-118">Bu uyarı gönderildiği hello eylem grubunun kısaad</span><span class="sxs-lookup"><span data-stu-id="d81ab-118">Shortname of hello action group this alert was sent to</span></span>
- <span data-ttu-id="d81ab-119">Merhaba uyarı başlığı</span><span class="sxs-lookup"><span data-stu-id="d81ab-119">Title of hello alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="d81ab-120">Aboneliğini iptal etmek için bir eylem grubu SMS uyarıları</span><span class="sxs-lookup"><span data-stu-id="d81ab-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="d81ab-121">Bir kullanıcı SMS uyarılar için bir eylem grubu için yanıt veren toohello shortcode 20873 hello sözcüklerle tarafından aboneliğinizi iptal edebilirsiniz: "devre dışı &lt;eylem grubunun kısaad&gt;".</span><span class="sxs-lookup"><span data-stu-id="d81ab-121">A user can unsubscribe from SMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="d81ab-122">Örn</span><span class="sxs-lookup"><span data-stu-id="d81ab-122">Ex.</span></span> <span data-ttu-id="d81ab-123">Merhaba kısaad "Azure" ile bir eylem grubu için uyarılardan toounsubscribe isteyen kullanıcı "Azure devre dışı bırak" diyen bir SMS toohello shortcode 20873 göndermek</span><span class="sxs-lookup"><span data-stu-id="d81ab-123">A user wishing toounsubscribe from alerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="d81ab-124">Tüm Eylem grupları için SMS uyarı aboneliğini</span><span class="sxs-lookup"><span data-stu-id="d81ab-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="d81ab-125">Bir kullanıcının tüm Eylem grupları için tüm SMS uyarılardan yanıt veren toohello shortcode anahtar sözcükler aşağıdaki hello biri tarafından 20873 herhangi biriyle aboneliğinizi iptal edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="d81ab-125">A user can unsubscribe from all SMS alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="d81ab-126">DURDUR</span><span class="sxs-lookup"><span data-stu-id="d81ab-126">STOP</span></span>

<span data-ttu-id="d81ab-127">Örn</span><span class="sxs-lookup"><span data-stu-id="d81ab-127">Ex.</span></span> <span data-ttu-id="d81ab-128">Tüm eylem gruplarında, tüm SMS uyarılardan toounsubscribe isteyen kullanıcı "Durdur" diyen bir SMS toohello shortcode 20873 göndermek</span><span class="sxs-lookup"><span data-stu-id="d81ab-128">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="d81ab-129">Bir kullanıcı iptal etti SMS uyarır, ancak daha sonra tooa yeni eylem grubu eklenir; Bunlar yeni o eylemi grubu SMS uyarı almak, ancak tüm önceki eylem gruplarından aboneliği kalır.</span><span class="sxs-lookup"><span data-stu-id="d81ab-129">If a user has unsubscribed from SMS alerts, but is then added tooa new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a><span data-ttu-id="d81ab-130">Bir eylem grubu için resubscribing tooSMS uyarıları</span><span class="sxs-lookup"><span data-stu-id="d81ab-130">Resubscribing tooSMS alerts for one action group</span></span>
<span data-ttu-id="d81ab-131">Bir kullanıcı tarafından yanıt veren toohello shortcode 20873 hello sözcüklerle tooSMS bir eylem grubu için uyarılar için resubscribe: "etkinleştirme &lt;eylem grubunun kısaad&gt;".</span><span class="sxs-lookup"><span data-stu-id="d81ab-131">A user can resubscribe tooSMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="d81ab-132">Örn</span><span class="sxs-lookup"><span data-stu-id="d81ab-132">Ex.</span></span> <span data-ttu-id="d81ab-133">Bir eylem grubu hello kısaad "Azure" ile tooresubscribe tooalerts isteyen bir kullanıcı "Azure etkinleştir" diyen bir SMS toohello shortcode 20873 göndermek</span><span class="sxs-lookup"><span data-stu-id="d81ab-133">A user wishing tooresubscribe tooalerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a><span data-ttu-id="d81ab-134">Tüm Eylem grupları için resubscribing tooSMS uyarıları</span><span class="sxs-lookup"><span data-stu-id="d81ab-134">Resubscribing tooSMS alerts for all action groups</span></span>
<span data-ttu-id="d81ab-135">Bir kullanıcı tooall SMS tüm Eylem grupları için uyarılar için yanıt veren toohello shortcode anahtar sözcükler aşağıdaki hello biri tarafından 20873 herhangi biriyle resubscribe:</span><span class="sxs-lookup"><span data-stu-id="d81ab-135">A user can resubscribe tooall SMS for alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>

* <span data-ttu-id="d81ab-136">BAŞLAT</span><span class="sxs-lookup"><span data-stu-id="d81ab-136">START</span></span>

<span data-ttu-id="d81ab-137">Örn</span><span class="sxs-lookup"><span data-stu-id="d81ab-137">Ex.</span></span> <span data-ttu-id="d81ab-138">Tüm eylem gruplarında, tüm SMS uyarılardan toounsubscribe isteyen kullanıcı "Başlat" diyen bir SMS toohello shortcode 20873 göndermek</span><span class="sxs-lookup"><span data-stu-id="d81ab-138">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="d81ab-139">SMS aracılığıyla Yardım isteme</span><span class="sxs-lookup"><span data-stu-id="d81ab-139">Requesting help via SMS</span></span>
<span data-ttu-id="d81ab-140">Bir kullanıcı herhangi bir anahtar sözcük aşağıdaki hello ile yanıt veren toohello shortcode 20873 tarafından alınan hello SMS hakkında daha fazla bilgi isteyebilir:</span><span class="sxs-lookup"><span data-stu-id="d81ab-140">A user can ask for more information about hello SMS they have received by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="d81ab-141">YARDIM</span><span class="sxs-lookup"><span data-stu-id="d81ab-141">HELP</span></span>

<span data-ttu-id="d81ab-142">Bir yanıt toohello kullanıcı ile bir bağlantı toothis makalesi gönderilir.</span><span class="sxs-lookup"><span data-stu-id="d81ab-142">A response will be sent toohello user with a link toothis article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d81ab-143">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="d81ab-143">Next Steps</span></span>
<span data-ttu-id="d81ab-144">Alma bir [etkinlik günlüğü uyarıları genel bakış](monitoring-overview-alerts.md) ve nasıl tooget uyarı öğrenin</span><span class="sxs-lookup"><span data-stu-id="d81ab-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how tooget alerted</span></span>  
<span data-ttu-id="d81ab-145">Daha fazla bilgi edinmek [SMS hız sınırı](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="d81ab-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="d81ab-146">Daha fazla bilgi edinmek [Eylem grupları](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="d81ab-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
