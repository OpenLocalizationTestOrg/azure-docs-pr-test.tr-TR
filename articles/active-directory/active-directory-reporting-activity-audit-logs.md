---
title: "aaaAudit etkinlik raporları hello Azure Active Directory portalında | Microsoft Docs"
description: "Giriş toohello denetim hello Azure Active Directory portalında etkinlik raporları"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="63ae3-103">Etkinlik raporları hello Azure Active Directory portalında denetleme</span><span class="sxs-lookup"><span data-stu-id="63ae3-103">Audit activity reports in hello Azure Active Directory portal</span></span> 

<span data-ttu-id="63ae3-104">Azure Active Directory (Azure AD) raporlama ile ortamınızı nasıl çalıştığını toodetermine gereksinim hello bilgileri elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63ae3-104">With reporting in Azure Active Directory (Azure AD), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="63ae3-105">Azure AD raporlama mimarisi hello bileşenleri aşağıdaki Merhaba oluşur:</span><span class="sxs-lookup"><span data-stu-id="63ae3-105">hello reporting architecture in Azure AD consists of hello following components:</span></span>

- <span data-ttu-id="63ae3-106">**Etkinlik**</span><span class="sxs-lookup"><span data-stu-id="63ae3-106">**Activity**</span></span> 
    - <span data-ttu-id="63ae3-107">**Oturum açma etkinliklerini** – yönetilen uygulamalar ve kullanıcı oturum açma etkinliklerini hello kullanımı hakkında bilgi</span><span class="sxs-lookup"><span data-stu-id="63ae3-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="63ae3-108">**Denetim günlükleri**: Kullanıcılar ve grup yönetimi, yönetilen uygulamalarınız ve dizin etkinlikleriniz hakkında sistem etkinliği bilgileri.</span><span class="sxs-lookup"><span data-stu-id="63ae3-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="63ae3-109">**Güvenlik**</span><span class="sxs-lookup"><span data-stu-id="63ae3-109">**Security**</span></span> 
    - <span data-ttu-id="63ae3-110">**Riskli oturum açma işlemleri** -bir riskli oturum açma bir hello meşru bir kullanıcı hesabının sahibi olmayan kişi tarafından gerçekleştirilmiş olabilecek bir oturum açma girişimi için göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="63ae3-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="63ae3-111">Daha fazla bilgi için bkz. Riskli oturum açma işlemleri.</span><span class="sxs-lookup"><span data-stu-id="63ae3-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="63ae3-112">**Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="63ae3-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="63ae3-113">Daha fazla bilgi için bkz. Riskli oldukları belirlenen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="63ae3-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="63ae3-114">Bu konuda hello denetim etkinlikleri genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="63ae3-114">This topic gives you an overview of hello audit activities.</span></span>
 
## <a name="who-can-access-hello-data"></a><span data-ttu-id="63ae3-115">Merhaba veri erişebilecek mi?</span><span class="sxs-lookup"><span data-stu-id="63ae3-115">Who can access hello data?</span></span>
* <span data-ttu-id="63ae3-116">Merhaba Güvenlik Yöneticisi veya güvenlik okuyucu roldeki kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="63ae3-116">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="63ae3-117">Genel Yöneticiler</span><span class="sxs-lookup"><span data-stu-id="63ae3-117">Global Admins</span></span>
* <span data-ttu-id="63ae3-118">Bireysel kullanıcılar (yönetici olmayanlar) kendi etkinliklerini görebilir</span><span class="sxs-lookup"><span data-stu-id="63ae3-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="63ae3-119">Denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="63ae3-119">Audit logs</span></span>

<span data-ttu-id="63ae3-120">Azure Active Directory'de Hello denetim günlüklerini kayıtları sistem etkinliklerin uyumluluk sağlar.</span><span class="sxs-lookup"><span data-stu-id="63ae3-120">hello audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="63ae3-121">İlk giriş noktası verileri denetleme tooall olan **denetim günlüklerini** hello içinde **etkinlik** bölümünü **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="63ae3-121">Your first entry point tooall auditing data is **Audit logs** in hello **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="63ae3-122">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/61.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="63ae3-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="63ae3-123">Denetim günlüklerinin aşağıdakileri gösteren bir varsayılan liste görünümü vardır:</span><span class="sxs-lookup"><span data-stu-id="63ae3-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="63ae3-124">Başlangıç tarihi ve saati hello oluşum</span><span class="sxs-lookup"><span data-stu-id="63ae3-124">hello date and time of hello occurrence</span></span>
- <span data-ttu-id="63ae3-125">Başlatıcı hello / aktör (*kimin*) etkinliğin</span><span class="sxs-lookup"><span data-stu-id="63ae3-125">hello initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="63ae3-126">Merhaba etkinliği (*ne*)</span><span class="sxs-lookup"><span data-stu-id="63ae3-126">hello activity (*what*)</span></span> 
- <span data-ttu-id="63ae3-127">Merhaba hedef</span><span class="sxs-lookup"><span data-stu-id="63ae3-127">hello target</span></span>

<span data-ttu-id="63ae3-128">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/18.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="63ae3-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="63ae3-129">Tıklatarak hello liste görünümü özelleştirebilirsiniz **sütunları** hello araç.</span><span class="sxs-lookup"><span data-stu-id="63ae3-129">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="63ae3-130">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/19.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="63ae3-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="63ae3-131">Bu toodisplay ek alanlar etkinleştirir veya zaten görüntülenen alanları kaldırın.</span><span class="sxs-lookup"><span data-stu-id="63ae3-131">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="63ae3-132">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/21.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="63ae3-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="63ae3-133">Merhaba liste görünümünde bir öğeyi tıklatarak bunu hakkında tüm kullanılabilir ayrıntıları alın.</span><span class="sxs-lookup"><span data-stu-id="63ae3-133">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="63ae3-134">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/22.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="63ae3-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="63ae3-135">Denetim günlüklerini filtreleme</span><span class="sxs-lookup"><span data-stu-id="63ae3-135">Filtering audit logs</span></span>

<span data-ttu-id="63ae3-136">Merhaba aşağı toonarrow veri tooa düzeyinde çalışır, alanları izleyen hello kullanarak hello denetim verileri filtreleyebilirsiniz bildirdi:</span><span class="sxs-lookup"><span data-stu-id="63ae3-136">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="63ae3-137">Tarih aralığı</span><span class="sxs-lookup"><span data-stu-id="63ae3-137">Date range</span></span>
- <span data-ttu-id="63ae3-138">Başlatan (Aktör)</span><span class="sxs-lookup"><span data-stu-id="63ae3-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="63ae3-139">Kategori</span><span class="sxs-lookup"><span data-stu-id="63ae3-139">Category</span></span>
- <span data-ttu-id="63ae3-140">Etkinlik kaynak türü</span><span class="sxs-lookup"><span data-stu-id="63ae3-140">Activity resource type</span></span>
- <span data-ttu-id="63ae3-141">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="63ae3-141">Activity</span></span>

<span data-ttu-id="63ae3-142">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/23.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="63ae3-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="63ae3-143">Merhaba **tarih aralığı** filtre etkinleştirir tooyou toodefine hello için bir zaman çerçevesi veri döndürdü.</span><span class="sxs-lookup"><span data-stu-id="63ae3-143">hello **date range** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="63ae3-144">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="63ae3-144">Possible values are:</span></span>

- <span data-ttu-id="63ae3-145">1 ay</span><span class="sxs-lookup"><span data-stu-id="63ae3-145">1 month</span></span>
- <span data-ttu-id="63ae3-146">7 gün</span><span class="sxs-lookup"><span data-stu-id="63ae3-146">7 days</span></span>
- <span data-ttu-id="63ae3-147">24 saat</span><span class="sxs-lookup"><span data-stu-id="63ae3-147">24 hours</span></span>
- <span data-ttu-id="63ae3-148">Özel</span><span class="sxs-lookup"><span data-stu-id="63ae3-148">Custom</span></span>

<span data-ttu-id="63ae3-149">Özel bir zaman çerçevesi seçerken başlangıç ve bitiş zamanını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63ae3-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="63ae3-150">Merhaba **tarafından başlatılan** filtre, toodefine bir aktör'ın adı veya evrensel asıl adı (UPN) sağlar.</span><span class="sxs-lookup"><span data-stu-id="63ae3-150">hello **initiated by** filter enables you toodefine an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="63ae3-151">Merhaba **kategori** filtre filtre aşağıdaki Merhaba, tooselect sağlar:</span><span class="sxs-lookup"><span data-stu-id="63ae3-151">hello **category** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="63ae3-152">Tümü</span><span class="sxs-lookup"><span data-stu-id="63ae3-152">All</span></span>
- <span data-ttu-id="63ae3-153">Çekirdek kategori</span><span class="sxs-lookup"><span data-stu-id="63ae3-153">Core category</span></span>
- <span data-ttu-id="63ae3-154">Çekirdek dizin</span><span class="sxs-lookup"><span data-stu-id="63ae3-154">Core directory</span></span>
- <span data-ttu-id="63ae3-155">Self servis parola yönetimi</span><span class="sxs-lookup"><span data-stu-id="63ae3-155">Self-service password management</span></span>
- <span data-ttu-id="63ae3-156">Self servis grup yönetimi</span><span class="sxs-lookup"><span data-stu-id="63ae3-156">Self-service group management</span></span>
- <span data-ttu-id="63ae3-157">Hesap sağlama - Otomatik parola geçişi</span><span class="sxs-lookup"><span data-stu-id="63ae3-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="63ae3-158">Davetli kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="63ae3-158">Invited users</span></span>
- <span data-ttu-id="63ae3-159">MIM hizmeti</span><span class="sxs-lookup"><span data-stu-id="63ae3-159">MIM service</span></span>
- <span data-ttu-id="63ae3-160">Kimlik Koruması</span><span class="sxs-lookup"><span data-stu-id="63ae3-160">Identity Protection</span></span>
- <span data-ttu-id="63ae3-161">B2C</span><span class="sxs-lookup"><span data-stu-id="63ae3-161">B2C</span></span>

<span data-ttu-id="63ae3-162">Merhaba **etkinlik kaynak türü** filtre hello aşağıdakilerden birini filtreler tooselect sağlar:</span><span class="sxs-lookup"><span data-stu-id="63ae3-162">hello **activity resource type** filter enables you tooselect one of hello following filters:</span></span>

- <span data-ttu-id="63ae3-163">Tümü</span><span class="sxs-lookup"><span data-stu-id="63ae3-163">All</span></span> 
- <span data-ttu-id="63ae3-164">Grup</span><span class="sxs-lookup"><span data-stu-id="63ae3-164">Group</span></span>
- <span data-ttu-id="63ae3-165">Dizin</span><span class="sxs-lookup"><span data-stu-id="63ae3-165">Directory</span></span>
- <span data-ttu-id="63ae3-166">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="63ae3-166">User</span></span>
- <span data-ttu-id="63ae3-167">Uygulama</span><span class="sxs-lookup"><span data-stu-id="63ae3-167">Application</span></span>
- <span data-ttu-id="63ae3-168">İlke</span><span class="sxs-lookup"><span data-stu-id="63ae3-168">Policy</span></span>
- <span data-ttu-id="63ae3-169">Cihaz</span><span class="sxs-lookup"><span data-stu-id="63ae3-169">Device</span></span>
- <span data-ttu-id="63ae3-170">Diğer</span><span class="sxs-lookup"><span data-stu-id="63ae3-170">Other</span></span>

<span data-ttu-id="63ae3-171">Seçtiğinizde, **grup** olarak **etkinlik kaynak türü**, tooalso sağlayan bir ek filtre kategorisi alma sağlayan bir **kaynak**:</span><span class="sxs-lookup"><span data-stu-id="63ae3-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you tooalso provide a **Source**:</span></span>

- <span data-ttu-id="63ae3-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="63ae3-172">Azure AD</span></span>
- <span data-ttu-id="63ae3-173">O365</span><span class="sxs-lookup"><span data-stu-id="63ae3-173">O365</span></span>


<span data-ttu-id="63ae3-174">Merhaba **etkinlik** filtre hello kategori ve etkinlik kaynak türü seçimi yaptığınız dayanır.</span><span class="sxs-lookup"><span data-stu-id="63ae3-174">hello **activity** filter is based on hello category and Activity resource type selection you make.</span></span> <span data-ttu-id="63ae3-175">Belirli bir etkinliğe toosee istediğiniz ya da Tümünü Seç seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="63ae3-175">You can select a specific activity you want toosee or choose all.</span></span> 

<span data-ttu-id="63ae3-176">Merhaba grafik API'si https://graph.windows.net/$ tenantdomain/etkinlikleri/auditActivityTypes kullanarak tüm denetim etkinlikleri hello listesini elde edebilirsiniz? api sürümü beta = nerede $tenantdomain = etki alanı adı veya toohello makalesine başvurun [denetleme raporu olayları](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="63ae3-176">You can get hello list of all Audit Activities using hello Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer toohello article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="63ae3-177">Denetim günlükleri kısayolları</span><span class="sxs-lookup"><span data-stu-id="63ae3-177">Audit logs shortcuts</span></span>

<span data-ttu-id="63ae3-178">Ayrıca çok**Azure Active Directory**, hello Azure portal, iki ek giriş noktaları ile tooaudit verileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="63ae3-178">In addition too**Azure Active Directory**, hello Azure portal provides you with two additional entry points tooaudit data:</span></span>

- <span data-ttu-id="63ae3-179">Kullanıcılar ve gruplar</span><span class="sxs-lookup"><span data-stu-id="63ae3-179">Users and groups</span></span>
- <span data-ttu-id="63ae3-180">Kurumsal uygulamalar</span><span class="sxs-lookup"><span data-stu-id="63ae3-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="63ae3-181">Kullanıcı ve gruplara yönelik denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="63ae3-181">Users and groups audit logs</span></span>

<span data-ttu-id="63ae3-182">Kullanıcı ve grup tabanlı denetim raporları ile yanıtlar tooquestions gibi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="63ae3-182">With user and group-based audit reports, you can get answers tooquestions such as:</span></span>

- <span data-ttu-id="63ae3-183">Hangi güncelleştirme türlerini uygulanan hello kullanıcılar silinmiş?</span><span class="sxs-lookup"><span data-stu-id="63ae3-183">What types of updates have been applied hello users?</span></span>

- <span data-ttu-id="63ae3-184">Kaç adet kullanıcı değiştirildi?</span><span class="sxs-lookup"><span data-stu-id="63ae3-184">How many users were changed?</span></span>

- <span data-ttu-id="63ae3-185">Kaç adet parola değiştirildi?</span><span class="sxs-lookup"><span data-stu-id="63ae3-185">How many passwords were changed?</span></span>

- <span data-ttu-id="63ae3-186">Bir yönetici bir dizinde neler yaptı?</span><span class="sxs-lookup"><span data-stu-id="63ae3-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="63ae3-187">Eklenen hello grupları nelerdir?</span><span class="sxs-lookup"><span data-stu-id="63ae3-187">What are hello groups that have been added?</span></span>

- <span data-ttu-id="63ae3-188">Üyelik değişiklikleri olan gruplar var mı?</span><span class="sxs-lookup"><span data-stu-id="63ae3-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="63ae3-189">Grubun sahiplerini Hello değişti mi?</span><span class="sxs-lookup"><span data-stu-id="63ae3-189">Have hello owners of group been changed?</span></span>

- <span data-ttu-id="63ae3-190">Hangi lisansları tooa grup veya kullanıcı atanmış?</span><span class="sxs-lookup"><span data-stu-id="63ae3-190">What licenses have been assigned tooa group or a user?</span></span>

<span data-ttu-id="63ae3-191">Yalnızca ilgili toousers ve gruplar verileri denetleme tooreview istiyorsanız, filtre uygulanmış bir görünüm altında bulabilirsiniz **denetim günlüklerini** hello içinde **etkinlik** hello bölümünü **kullanıcılar ve gruplar**.</span><span class="sxs-lookup"><span data-stu-id="63ae3-191">If you just want tooreview auditing data that is related toousers and groups, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Users and Groups**.</span></span> <span data-ttu-id="63ae3-192">Bu giriş noktasında, **Etkinlik Kaynağı Türü** olarak **Kullanıcılar ve gruplar** önceden seçilidir.</span><span class="sxs-lookup"><span data-stu-id="63ae3-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="63ae3-193">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/93.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="63ae3-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="63ae3-194">Kurumsal uygulamaların denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="63ae3-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="63ae3-195">Uygulama tabanlı denetim raporları, yanıtları tooquestions gibi alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="63ae3-195">With application-based audit reports, you can get answers tooquestions such as:</span></span>

* <span data-ttu-id="63ae3-196">Eklenen veya güncelleştirilen hello uygulamalar nelerdir?</span><span class="sxs-lookup"><span data-stu-id="63ae3-196">What are hello applications that have been added or updated?</span></span>
* <span data-ttu-id="63ae3-197">Kaldırılan hello uygulamalar nelerdir?</span><span class="sxs-lookup"><span data-stu-id="63ae3-197">What are hello applications that have been removed?</span></span>
* <span data-ttu-id="63ae3-198">Belirli bir uygulamaya ait bir hizmet ilkesi değiştirildi mi?</span><span class="sxs-lookup"><span data-stu-id="63ae3-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="63ae3-199">Uygulamaları Hello adlarını değişti mi?</span><span class="sxs-lookup"><span data-stu-id="63ae3-199">Have hello names of applications been changed?</span></span>
* <span data-ttu-id="63ae3-200">Kimin onayı tooan uygulamasını vermiş?</span><span class="sxs-lookup"><span data-stu-id="63ae3-200">Who gave consent tooan application?</span></span>

<span data-ttu-id="63ae3-201">Yalnızca ilgili tooyour uygulamalar verileri denetleme tooreview istiyorsanız, filtre uygulanmış bir görünüm altında bulabilirsiniz **denetim günlüklerini** hello içinde **etkinlik** hello bölümünü **kurumsal uygulamalar**  dikey.</span><span class="sxs-lookup"><span data-stu-id="63ae3-201">If you just want tooreview auditing data that is related tooyour applications, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Enterprise applications** blade.</span></span> <span data-ttu-id="63ae3-202">Bu giriş noktasında, **Etkinlik Kaynağı Türü** olarak **Kurumsal uygulamalar** önceden seçilidir.</span><span class="sxs-lookup"><span data-stu-id="63ae3-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="63ae3-203">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/134.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="63ae3-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="63ae3-204">Bu görünümü daha fazla toojust aşağı filtreleyebilirsiniz **grupları** veya yalnızca **kullanıcılar**.</span><span class="sxs-lookup"><span data-stu-id="63ae3-204">You can filter this view further down toojust **groups** or just **users**.</span></span>

<span data-ttu-id="63ae3-205">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/25.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="63ae3-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="63ae3-206">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="63ae3-206">Next steps</span></span>

<span data-ttu-id="63ae3-207">Merhaba raporlama genel bakış için bkz: [Azure Active Directory raporlama](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="63ae3-207">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

