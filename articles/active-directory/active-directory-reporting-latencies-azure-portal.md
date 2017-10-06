---
title: aaaAzure Active Directory raporlama gecikmeleri | Microsoft Docs
description: "Merhaba, olayları tooshow ayarlama, Azure portalında raporlama için geçen süreyi hakkında bilgi edinin"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="03008-103">Gecikme raporlama Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="03008-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="03008-104">İle [raporlama](active-directory-preview-explainer.md) hello Azure Active Directory, toodetermine ortamınızı nasıl yapılması gereken tüm hello bilgileri alın.</span><span class="sxs-lookup"><span data-stu-id="03008-104">With [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, you get all hello information you need toodetermine how your environment is doing.</span></span> <span data-ttu-id="03008-105">Merhaba hello Azure portal'ın veri tooshow yukarı olarak da bilinen gecikme raporlama için geçen süre miktarı.</span><span class="sxs-lookup"><span data-stu-id="03008-105">hello amount of time it takes for reporting data tooshow up in hello Azure portal is also known as latency.</span></span> 

<span data-ttu-id="03008-106">Bu konuda hello hello gecikme bilgileri hello Azure portal tüm raporlama kategorilerini listeler.</span><span class="sxs-lookup"><span data-stu-id="03008-106">This topic lists hello latency information for hello all reporting categories in hello Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="03008-107">Etkinlik raporları</span><span class="sxs-lookup"><span data-stu-id="03008-107">Activity reports</span></span>

<span data-ttu-id="03008-108">Etkinlik Raporlama iki alan vardır:</span><span class="sxs-lookup"><span data-stu-id="03008-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="03008-109">**Oturum açma etkinliklerini** – yönetilen uygulamalar ve kullanıcı oturum açma etkinliklerini hello kullanımı hakkında bilgi</span><span class="sxs-lookup"><span data-stu-id="03008-109">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="03008-110">**Denetim günlükleri** - Kullanıcılar ve grup yönetimi, yönetilen uygulamalarınız ve dizin etkinlikleriniz hakkında sistem etkinliği bilgileri</span><span class="sxs-lookup"><span data-stu-id="03008-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="03008-111">Aşağıdaki tablonun hello hello gecikme bilgileri etkinlik raporları listeler.</span><span class="sxs-lookup"><span data-stu-id="03008-111">hello following table lists hello latency information for activity reports.</span></span>

| <span data-ttu-id="03008-112">Rapor</span><span class="sxs-lookup"><span data-stu-id="03008-112">Report</span></span> | <span data-ttu-id="03008-113">Minimum</span><span class="sxs-lookup"><span data-stu-id="03008-113">Minimum</span></span> | <span data-ttu-id="03008-114">Ortalama</span><span class="sxs-lookup"><span data-stu-id="03008-114">Average</span></span> | <span data-ttu-id="03008-115">Maksimum</span><span class="sxs-lookup"><span data-stu-id="03008-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="03008-116">Denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="03008-116">Audit logs</span></span>             | <span data-ttu-id="03008-117">30 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-117">30 minutes</span></span>  | <span data-ttu-id="03008-118">45 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-118">45 Minutes</span></span> | <span data-ttu-id="03008-119">1 saat</span><span class="sxs-lookup"><span data-stu-id="03008-119">1 hour</span></span>     |
| <span data-ttu-id="03008-120">Oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="03008-120">Sign-ins</span></span>               | <span data-ttu-id="03008-121">15 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-121">15 minutes</span></span>  | <span data-ttu-id="03008-122">15 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-122">15 minutes</span></span> | <span data-ttu-id="03008-123">2 saat *</span><span class="sxs-lookup"><span data-stu-id="03008-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="03008-124">Eski office uygulamalarından gelen gerçekleştirilen oturum açma etkinliği için bazı veriler, veri tooshow yukarı raporlama hello too8 saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="03008-124">For some sign-ins activity data coming from legacy office applications, it can take too8 hours for hello reporting data tooshow up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="03008-125">Güvenlik raporları</span><span class="sxs-lookup"><span data-stu-id="03008-125">Security reports</span></span>

<span data-ttu-id="03008-126">Raporlama güvenliği, iki alan vardır:</span><span class="sxs-lookup"><span data-stu-id="03008-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="03008-127">**Riskli oturum açma işlemleri** -bir riskli oturum açma bir hello meşru bir kullanıcı hesabının sahibi olmayan kişi tarafından gerçekleştirilmiş olabilecek bir oturum açma girişimi için göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="03008-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 
- <span data-ttu-id="03008-128">**Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="03008-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="03008-129">Aşağıdaki tablonun hello hello gecikme bilgileri güvenlik raporları listeler.</span><span class="sxs-lookup"><span data-stu-id="03008-129">hello following table lists hello latency information for security reports.</span></span>

| <span data-ttu-id="03008-130">Rapor</span><span class="sxs-lookup"><span data-stu-id="03008-130">Report</span></span> | <span data-ttu-id="03008-131">Minimum</span><span class="sxs-lookup"><span data-stu-id="03008-131">Minimum</span></span> | <span data-ttu-id="03008-132">Ortalama</span><span class="sxs-lookup"><span data-stu-id="03008-132">Average</span></span> | <span data-ttu-id="03008-133">Maksimum</span><span class="sxs-lookup"><span data-stu-id="03008-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="03008-134">Risk altındaki kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="03008-134">Users at risk</span></span>          | <span data-ttu-id="03008-135">5 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-135">5 minutes</span></span>   | <span data-ttu-id="03008-136">15 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-136">15 minutes</span></span>  | <span data-ttu-id="03008-137">2 saat</span><span class="sxs-lookup"><span data-stu-id="03008-137">2 hours</span></span>  |
| <span data-ttu-id="03008-138">Riskli oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="03008-138">Risky sign-ins</span></span>         | <span data-ttu-id="03008-139">5 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-139">5 minutes</span></span>   | <span data-ttu-id="03008-140">15 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-140">15 minutes</span></span>  | <span data-ttu-id="03008-141">2 saat</span><span class="sxs-lookup"><span data-stu-id="03008-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="03008-142">Risk olayı</span><span class="sxs-lookup"><span data-stu-id="03008-142">Risk events</span></span>

<span data-ttu-id="03008-143">Azure Active Directory Uyarlamalı machine learning, ilgili tooyour kullanıcı hesapları olan algoritmalar ve buluşsal yöntemler toodetect şüpheli eylemleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="03008-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="03008-144">Her kuşkulu eylem bir kayıt çağrılan risk olayı depolanan algıladı.</span><span class="sxs-lookup"><span data-stu-id="03008-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="03008-145">Aşağıdaki tablonun hello hello gecikme bilgileri risk olaylarını listeler.</span><span class="sxs-lookup"><span data-stu-id="03008-145">hello following table lists hello latency information for risk events.</span></span>

| <span data-ttu-id="03008-146">Rapor</span><span class="sxs-lookup"><span data-stu-id="03008-146">Report</span></span> | <span data-ttu-id="03008-147">Minimum</span><span class="sxs-lookup"><span data-stu-id="03008-147">Minimum</span></span> | <span data-ttu-id="03008-148">Ortalama</span><span class="sxs-lookup"><span data-stu-id="03008-148">Average</span></span> | <span data-ttu-id="03008-149">Maksimum</span><span class="sxs-lookup"><span data-stu-id="03008-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="03008-150">Anonim IP adreslerinden oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="03008-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="03008-151">5 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-151">5 minutes</span></span> |<span data-ttu-id="03008-152">15 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-152">15 Minutes</span></span> |<span data-ttu-id="03008-153">2 saat</span><span class="sxs-lookup"><span data-stu-id="03008-153">2 hours</span></span> |
| <span data-ttu-id="03008-154">Alışılmadık konumlardan oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="03008-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="03008-155">5 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-155">5 minutes</span></span> |<span data-ttu-id="03008-156">15 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-156">15 Minutes</span></span> |<span data-ttu-id="03008-157">2 saat</span><span class="sxs-lookup"><span data-stu-id="03008-157">2 hours</span></span> |
| <span data-ttu-id="03008-158">Sızan kimlik bilgilerine sahip kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="03008-158">Users with leaked credentials</span></span> |<span data-ttu-id="03008-159">2 saat</span><span class="sxs-lookup"><span data-stu-id="03008-159">2 hours</span></span> |<span data-ttu-id="03008-160">4 saat</span><span class="sxs-lookup"><span data-stu-id="03008-160">4 hours</span></span> |<span data-ttu-id="03008-161">8 saat</span><span class="sxs-lookup"><span data-stu-id="03008-161">8 hours</span></span> |
| <span data-ttu-id="03008-162">Mümkün olmayan seyahat tooatypical konumları</span><span class="sxs-lookup"><span data-stu-id="03008-162">Impossible travel tooatypical locations</span></span> |<span data-ttu-id="03008-163">5 dakika</span><span class="sxs-lookup"><span data-stu-id="03008-163">5 minutes</span></span> |<span data-ttu-id="03008-164">1 saat</span><span class="sxs-lookup"><span data-stu-id="03008-164">1 hour</span></span> |<span data-ttu-id="03008-165">8 saat</span><span class="sxs-lookup"><span data-stu-id="03008-165">8 hours</span></span>  |
| <span data-ttu-id="03008-166">Virüs bulaşmış cihazlardan oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="03008-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="03008-167">2 saat</span><span class="sxs-lookup"><span data-stu-id="03008-167">2 hours</span></span> |<span data-ttu-id="03008-168">4 saat</span><span class="sxs-lookup"><span data-stu-id="03008-168">4 hours</span></span> |<span data-ttu-id="03008-169">8 saat</span><span class="sxs-lookup"><span data-stu-id="03008-169">8 hours</span></span>  |
| <span data-ttu-id="03008-170">Şüpheli etkinlik gösteren IP adreslerinden gerçekleştirilen oturum açma işlemleri</span><span class="sxs-lookup"><span data-stu-id="03008-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="03008-171">2 saat</span><span class="sxs-lookup"><span data-stu-id="03008-171">2 hours</span></span> |<span data-ttu-id="03008-172">4 saat</span><span class="sxs-lookup"><span data-stu-id="03008-172">4 hours</span></span> |<span data-ttu-id="03008-173">8 saat</span><span class="sxs-lookup"><span data-stu-id="03008-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="03008-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="03008-174">Next steps</span></span>

<span data-ttu-id="03008-175">Tooknow hello Azure portal'ın hello etkinlik raporları hakkında daha fazla bilgi istiyorsanız, bkz:</span><span class="sxs-lookup"><span data-stu-id="03008-175">If you want tooknow more about hello activity reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="03008-176">Hello Azure Active Directory portalında oturum açma etkinliği raporları</span><span class="sxs-lookup"><span data-stu-id="03008-176">Sign-in activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="03008-177">Etkinlik raporları hello Azure Active Directory portalında denetleme</span><span class="sxs-lookup"><span data-stu-id="03008-177">Audit activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="03008-178">Tooknow hello Azure portal'ın hello güvenlik raporları hakkında daha fazla bilgi istiyorsanız, bkz:</span><span class="sxs-lookup"><span data-stu-id="03008-178">If you want tooknow more about hello security reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="03008-179">Risk güvenlik raporu hello Azure Active Directory portalında kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="03008-179">Users at risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="03008-180">Hello Azure Active Directory portalında riskli oturum açma işlemleri raporu</span><span class="sxs-lookup"><span data-stu-id="03008-180">Risky sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="03008-181">Tooknow risk olaylar hakkında daha fazla bilgi istiyorsanız, bkz: [Azure Active Directory risk olaylarını](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="03008-181">If you want tooknow more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
