---
title: Active Directory aaaAzure raporlama | Microsoft Docs
description: "Azure Active Directory raporlamasına genel bir bakış sağlar."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="621f0-103">Azure Active Directory raporlama</span><span class="sxs-lookup"><span data-stu-id="621f0-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="621f0-104">Azure Active Directory raporlamasıyla, ortamınızın nasıl çalıştığıyla ilgili fikir edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="621f0-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="621f0-105">sağlanan hello veri sağlar:</span><span class="sxs-lookup"><span data-stu-id="621f0-105">hello provided data enables you to:</span></span>

- <span data-ttu-id="621f0-106">Uygulama ve hizmetlerinizin kullanıcılarınız tarafından nasıl kullanıldığını saptayabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="621f0-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="621f0-107">Ortamınızı Hello sağlığını etkileyen olası riskleri Algıla</span><span class="sxs-lookup"><span data-stu-id="621f0-107">Detect potential risks affecting hello health of your environment</span></span>
- <span data-ttu-id="621f0-108">Kullanıcılarınızın işlerini yapmalarını engelleyen sorunları giderebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="621f0-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="621f0-109">Merhaba raporlama mimarisi üzerinde iki ana ayaklar dayanır:</span><span class="sxs-lookup"><span data-stu-id="621f0-109">hello reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="621f0-110">Güvenlik raporları</span><span class="sxs-lookup"><span data-stu-id="621f0-110">Security reports</span></span>
- <span data-ttu-id="621f0-111">Etkinlik raporları</span><span class="sxs-lookup"><span data-stu-id="621f0-111">Activity reports</span></span>

![Raporlama](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="621f0-113">Güvenlik raporları</span><span class="sxs-lookup"><span data-stu-id="621f0-113">Security reports</span></span>

<span data-ttu-id="621f0-114">Azure Active Directory'de Hello güvenlik raporları, kuruluşunuzdaki kimlikleri, tooprotect yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="621f0-114">hello security reports in Azure Active Directory help you tooprotect your organization's identities.</span></span>  
<span data-ttu-id="621f0-115">Azure Active Directory'de iki tür güvenlik raporu vardır:</span><span class="sxs-lookup"><span data-stu-id="621f0-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="621f0-116">**Bayrak eklenen kullanıcılar için risk** - hello [bayrak eklenen kullanıcılar için risk güvenlik raporu](active-directory-reporting-security-user-at-risk.md), geçirildiğini kullanıcı hesapları özetini almak.</span><span class="sxs-lookup"><span data-stu-id="621f0-116">**Users flagged for risk** - From hello [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="621f0-117">**Riskli oturum açma işlemleri** - hello [riskli oturum açma güvenlik raporu](active-directory-reporting-security-risky-sign-ins.md), yasal sahibi bir kullanıcı hesabı olan kişi tarafından gerçekleştirilmiş olabilecek oturum açma denemeleri hello değil için bir gösterge alın.</span><span class="sxs-lookup"><span data-stu-id="621f0-117">**Risky sign-ins** - With hello [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 

<span data-ttu-id="621f0-118">**Hangi Azure AD lisans tooaccess bir güvenlik raporu gerekiyor mu?**</span><span class="sxs-lookup"><span data-stu-id="621f0-118">**What Azure AD license do you need tooaccess a security report?**</span></span>  
<span data-ttu-id="621f0-119">Azure Active Directory'nin tüm sürümlerinde size riskli oldukları belirlenen kullanıcılar ve riskli oturum açma işlemleri raporları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="621f0-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="621f0-120">Bununla birlikte, rapor ayrıntı düzeyini hello hello sürümleri arasında farklılık gösterir:</span><span class="sxs-lookup"><span data-stu-id="621f0-120">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="621f0-121">Merhaba, **Azure Active Directory ücretsiz ve Basic sürümleri**, zaten risk ve riskli oturum açma işlemleri için işaretlenen kullanıcıların bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="621f0-121">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="621f0-122">Merhaba **Azure Active Directory Premium 1** edition'ı genişletir bu modeli de tooexamine sağlayarak her rapor için algılanan risk olayı temel hello bazıları.</span><span class="sxs-lookup"><span data-stu-id="621f0-122">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="621f0-123">Merhaba **Azure Active Directory Premium 2** edition hello sizinle en hakkında ayrıntılı bilgi risk olaylarını temel hello ve ayrıca, otomatik olarak tooconfigured yanıt tooconfigure güvenlik ilkeleri sağlar sağlar risk düzeyleri.</span><span class="sxs-lookup"><span data-stu-id="621f0-123">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about hello underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="621f0-124">Etkinlik raporları</span><span class="sxs-lookup"><span data-stu-id="621f0-124">Activity reports</span></span>

<span data-ttu-id="621f0-125">Azure Active Directory'de iki tür etkinlik raporu vardır:</span><span class="sxs-lookup"><span data-stu-id="621f0-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="621f0-126">**Denetim günlükleri** - hello [denetim günlüklerini Etkinlik Raporu](active-directory-reporting-activity-audit-logs.md) kiracınızda gerçekleştirilen her görev toohello geçmişine erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="621f0-126">**Audit logs** - hello [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access toohello history of every task performed in your tenant.</span></span>

- <span data-ttu-id="621f0-127">**Oturum açma işlemleri** - hello [gerçekleştirilen oturum açma etkinliği raporu](active-directory-reporting-activity-sign-ins.md), belirleyebilirsiniz, hello denetim günlüklerini raporu tarafından bildirilen hello görevleri gerçekleştiren.</span><span class="sxs-lookup"><span data-stu-id="621f0-127">**Sign-ins** -  With hello [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed hello tasks reported by hello audit logs report.</span></span>



<span data-ttu-id="621f0-128">Merhaba **denetim günlüklerini rapor** sistem faaliyetleri kayıtlarıyla için uyumluluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="621f0-128">hello **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="621f0-129">Başkalarının arasında veri tooaddress yaygın senaryolar gibi sağlar hello sağlanan:</span><span class="sxs-lookup"><span data-stu-id="621f0-129">Amongst others, hello provided data enables you tooaddress common scenarios such as:</span></span>

- <span data-ttu-id="621f0-130">Kişi bilgilerimi Kiracı erişim tooan Yönetici grubu aldı.</span><span class="sxs-lookup"><span data-stu-id="621f0-130">Someone in my tenant got access tooan admin group.</span></span> <span data-ttu-id="621f0-131">Ona kim erişim verdi?</span><span class="sxs-lookup"><span data-stu-id="621f0-131">Who gave them access?</span></span> 

- <span data-ttu-id="621f0-132">Kullanıcıların belirli bir uygulamaya imzalama tooknow hello listesini istediğiniz ı itibaren son edildi hello uygulama ve tooknow de yapmak istiyorsanız</span><span class="sxs-lookup"><span data-stu-id="621f0-132">I want tooknow hello list of users signing into a specific app since I recently onboarded hello app and want tooknow if it’s doing well</span></span>

- <span data-ttu-id="621f0-133">Tooknow kaç parola sıfırlama gerçekleştiği my Kiracı istiyorum</span><span class="sxs-lookup"><span data-stu-id="621f0-133">I want tooknow how many password resets are happening in my tenant</span></span>


<span data-ttu-id="621f0-134">**Hangi Azure AD lisans tooaccess hello denetim günlüklerini rapor gerekiyor mu?**</span><span class="sxs-lookup"><span data-stu-id="621f0-134">**What Azure AD license do you need tooaccess hello audit logs report?**</span></span>  
<span data-ttu-id="621f0-135">Merhaba denetim günlüklerini raporu lisanslara sahip özellikler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="621f0-135">hello audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="621f0-136">Belirli bir özellik için bir lisans varsa, günlük bilgilerini Denetim erişim toohello de gerekir.</span><span class="sxs-lookup"><span data-stu-id="621f0-136">If you have a license for a specific feature, you also have access toohello audit log information for it.</span></span>

<span data-ttu-id="621f0-137">Daha fazla ayrıntı için bkz: **hello ücretsiz, temel ve Premium sürümlerinde genel olarak kullanılabilir özelliklerini karşılaştırma** içinde [Azure Active Directory özellikleri ve yetenekleri](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="621f0-137">For more details, see **Comparing generally available features of hello Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="621f0-138">Merhaba **gerçekleştirilen oturum açma etkinliği raporu** etkinleştirir tootoofind tooquestions gibi yanıt verir:</span><span class="sxs-lookup"><span data-stu-id="621f0-138">hello **sign-ins activity report** enables tootoofind answers tooquestions such as:</span></span>

- <span data-ttu-id="621f0-139">Bir kullanıcı oturum açma hello desenini nedir?</span><span class="sxs-lookup"><span data-stu-id="621f0-139">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="621f0-140">Bir hafta içerisinde kaç adet kullanıcı oturum açtı?</span><span class="sxs-lookup"><span data-stu-id="621f0-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="621f0-141">Bu oturum açma işlemleri hello durumu nedir?</span><span class="sxs-lookup"><span data-stu-id="621f0-141">What’s hello status of these sign-ins?</span></span>


<span data-ttu-id="621f0-142">**Hangi Azure AD lisans musunuz tooaccess gerçekleştirilen oturum açma etkinliği raporu hello?**</span><span class="sxs-lookup"><span data-stu-id="621f0-142">**What Azure AD license do you need tooaccess hello sign-ins activity report?**</span></span>  
<span data-ttu-id="621f0-143">gerçekleştirilen oturum açma etkinliği raporu tooaccess Merhaba, Kiracı kendisiyle ilişkili bir Azure AD Premium lisansına sahip olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="621f0-143">tooaccess hello sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="621f0-144">Programlı erişim</span><span class="sxs-lookup"><span data-stu-id="621f0-144">Programmatic access</span></span>

<span data-ttu-id="621f0-145">Toplama toohello kullanıcı arabiriminde, Azure Active Directory raporlama da sizinle sağlar [programlı erişim](active-directory-reporting-api-getting-started-azure-portal.md) raporlama verilerini toohello.</span><span class="sxs-lookup"><span data-stu-id="621f0-145">In addition toohello user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) toohello reporting data.</span></span> <span data-ttu-id="621f0-146">Bu raporların Hello veriler SIEM sistemleri, Denetim ve iş zekası araçları gibi çok kullanışlı tooyour uygulamalar olabilir.</span><span class="sxs-lookup"><span data-stu-id="621f0-146">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="621f0-147">bir dizi REST tabanlı API'ler aracılığıyla programlı erişim toohello veri API'leri sağlamak Hello Azure AD raporlama.</span><span class="sxs-lookup"><span data-stu-id="621f0-147">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="621f0-148">Çeşitli programlama dilleri ve araçlarından bu API'leri çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="621f0-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="621f0-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="621f0-149">Next steps</span></span>

<span data-ttu-id="621f0-150">Azure Active Directory'de çeşitli rapor türleri tooknow hello hakkında daha fazla bilgi istiyorsanız, bkz:</span><span class="sxs-lookup"><span data-stu-id="621f0-150">If you want tooknow more about hello various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="621f0-151">Riskli olarak işaretlenen kullanıcılar raporu</span><span class="sxs-lookup"><span data-stu-id="621f0-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="621f0-152">Riskli oturum açma işlemleri raporu</span><span class="sxs-lookup"><span data-stu-id="621f0-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="621f0-153">Denetim günlükleri raporu</span><span class="sxs-lookup"><span data-stu-id="621f0-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="621f0-154">Oturum açma günlükleri raporu</span><span class="sxs-lookup"><span data-stu-id="621f0-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="621f0-155">Tooknow API raporlama hello kullanarak verileri raporlama hello hello erişme hakkında daha fazla bilgi istiyorsanız, bkz:</span><span class="sxs-lookup"><span data-stu-id="621f0-155">If you want tooknow more about accessing hello hello reporting data using hello reporting API, see:</span></span> 

- [<span data-ttu-id="621f0-156">Hello Azure Active Directory raporlama API'si ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="621f0-156">Getting started with hello Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png