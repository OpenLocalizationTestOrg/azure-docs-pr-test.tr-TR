---
title: "Azure Active Directory portalındaki denetim etkinliği raporları | Microsoft Docs"
description: "Azure Active Directory portalındaki denetim etkinliği raporlarına giriş"
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
ms.openlocfilehash: f2d0332d815c82d7d47625e020de2e9c5099deeb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="audit-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="95ea0-103">Azure Active Directory portalındaki denetim etkinliği raporları</span><span class="sxs-lookup"><span data-stu-id="95ea0-103">Audit activity reports in the Azure Active Directory portal</span></span> 

<span data-ttu-id="95ea0-104">Azure Active Directory’deki (Azure AD) raporlama özelliğiyle ortamınızın nasıl çalıştığını belirlemek için gereken bilgileri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95ea0-104">With reporting in Azure Active Directory (Azure AD), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="95ea0-105">Azure AD'nin raporlama mimarisi aşağıdaki bileşenlerden oluşur:</span><span class="sxs-lookup"><span data-stu-id="95ea0-105">The reporting architecture in Azure AD consists of the following components:</span></span>

- <span data-ttu-id="95ea0-106">**Etkinlik**</span><span class="sxs-lookup"><span data-stu-id="95ea0-106">**Activity**</span></span> 
    - <span data-ttu-id="95ea0-107">**Oturum açma etkinlikleri**: Yönetilen uygulamaların kullanımı ve kullanıcıların oturum açma etkinlikleri hakkında bilgiler</span><span class="sxs-lookup"><span data-stu-id="95ea0-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="95ea0-108">**Denetim günlükleri**: Kullanıcılar ve grup yönetimi, yönetilen uygulamalarınız ve dizin etkinlikleriniz hakkında sistem etkinliği bilgileri.</span><span class="sxs-lookup"><span data-stu-id="95ea0-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="95ea0-109">**Güvenlik**</span><span class="sxs-lookup"><span data-stu-id="95ea0-109">**Security**</span></span> 
    - <span data-ttu-id="95ea0-110">**Riskli oturum açma işlemleri** - Riskli oturum açma işlemi bir kullanıcı hesabının meşru sahibi olmayan bir kişi tarafından gerçekleştirilmiş olabilecek oturum açma girişiminin göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="95ea0-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="95ea0-111">Daha fazla bilgi için bkz. Riskli oturum açma işlemleri.</span><span class="sxs-lookup"><span data-stu-id="95ea0-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="95ea0-112">**Riskli oldukları belirlenen kullanıcılar** - Riskli kullanıcı, güvenliği tehlikeye girmiş olabilecek bir kullanıcı hesabının göstergesidir.</span><span class="sxs-lookup"><span data-stu-id="95ea0-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="95ea0-113">Daha fazla bilgi için bkz. Riskli oldukları belirlenen kullanıcılar.</span><span class="sxs-lookup"><span data-stu-id="95ea0-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="95ea0-114">Bu konu başlığı denetim etkinliklerine genel bakış sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="95ea0-114">This topic gives you an overview of the audit activities.</span></span>
 
## <a name="who-can-access-the-data"></a><span data-ttu-id="95ea0-115">Verilere kimler erişebilir?</span><span class="sxs-lookup"><span data-stu-id="95ea0-115">Who can access the data?</span></span>
* <span data-ttu-id="95ea0-116">Güvenlik Yöneticisi veya Güvenlik Okuyucusu rolündeki kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="95ea0-116">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="95ea0-117">Genel Yöneticiler</span><span class="sxs-lookup"><span data-stu-id="95ea0-117">Global Admins</span></span>
* <span data-ttu-id="95ea0-118">Bireysel kullanıcılar (yönetici olmayanlar) kendi etkinliklerini görebilir</span><span class="sxs-lookup"><span data-stu-id="95ea0-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="95ea0-119">Denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="95ea0-119">Audit logs</span></span>

<span data-ttu-id="95ea0-120">Azure Active Directory'deki denetim günlükleri uyumluluk amacıyla sistem etkinliklerinin kayıtlarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="95ea0-120">The audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="95ea0-121">Tüm denetim verilerine ilk giriş noktanız, **Azure Active Directory**’nin **Etkinlik** bölümünde bulunan **Denetim günlükleri** kısmıdır.</span><span class="sxs-lookup"><span data-stu-id="95ea0-121">Your first entry point to all auditing data is **Audit logs** in the **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="95ea0-122">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/61.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="95ea0-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="95ea0-123">Denetim günlüklerinin aşağıdakileri gösteren bir varsayılan liste görünümü vardır:</span><span class="sxs-lookup"><span data-stu-id="95ea0-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="95ea0-124">Olayın tarihi ve saati</span><span class="sxs-lookup"><span data-stu-id="95ea0-124">the date and time of the occurrence</span></span>
- <span data-ttu-id="95ea0-125">Bir etkinliğin başlatıcısı/aktörü (*kim*)</span><span class="sxs-lookup"><span data-stu-id="95ea0-125">the initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="95ea0-126">Etkinlik (*ne*)</span><span class="sxs-lookup"><span data-stu-id="95ea0-126">the activity (*what*)</span></span> 
- <span data-ttu-id="95ea0-127">Hedef</span><span class="sxs-lookup"><span data-stu-id="95ea0-127">the target</span></span>

<span data-ttu-id="95ea0-128">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/18.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="95ea0-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="95ea0-129">Araç çubuğunda **Sütunlar**’a tıklayarak liste görünümünü özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95ea0-129">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="95ea0-130">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/19.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="95ea0-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="95ea0-131">Bu sayede ek alanları görüntüleyebilir ya da zaten görüntülenen alanları kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95ea0-131">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="95ea0-132">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/21.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="95ea0-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="95ea0-133">Liste görünümündeki bir öğeye tıklayarak bu öğe hakkında mevcut olan tüm ayrıntıları öğrenebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95ea0-133">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="95ea0-134">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/22.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="95ea0-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="95ea0-135">Denetim günlüklerini filtreleme</span><span class="sxs-lookup"><span data-stu-id="95ea0-135">Filtering audit logs</span></span>

<span data-ttu-id="95ea0-136">Raporlanan verileri istediğiniz düzeye gelecek şekilde daraltmak için, aşağıdaki alanları kullanarak denetim verilerini filtreleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95ea0-136">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="95ea0-137">Tarih aralığı</span><span class="sxs-lookup"><span data-stu-id="95ea0-137">Date range</span></span>
- <span data-ttu-id="95ea0-138">Başlatan (Aktör)</span><span class="sxs-lookup"><span data-stu-id="95ea0-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="95ea0-139">Kategori</span><span class="sxs-lookup"><span data-stu-id="95ea0-139">Category</span></span>
- <span data-ttu-id="95ea0-140">Etkinlik kaynak türü</span><span class="sxs-lookup"><span data-stu-id="95ea0-140">Activity resource type</span></span>
- <span data-ttu-id="95ea0-141">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="95ea0-141">Activity</span></span>

<span data-ttu-id="95ea0-142">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/23.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="95ea0-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="95ea0-143">**Tarih aralığı** filtresi, döndürülen veriler için bir zaman çerçevesi tanımlamanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="95ea0-143">The **date range** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="95ea0-144">Olası değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="95ea0-144">Possible values are:</span></span>

- <span data-ttu-id="95ea0-145">1 ay</span><span class="sxs-lookup"><span data-stu-id="95ea0-145">1 month</span></span>
- <span data-ttu-id="95ea0-146">7 gün</span><span class="sxs-lookup"><span data-stu-id="95ea0-146">7 days</span></span>
- <span data-ttu-id="95ea0-147">24 saat</span><span class="sxs-lookup"><span data-stu-id="95ea0-147">24 hours</span></span>
- <span data-ttu-id="95ea0-148">Özel</span><span class="sxs-lookup"><span data-stu-id="95ea0-148">Custom</span></span>

<span data-ttu-id="95ea0-149">Özel bir zaman çerçevesi seçerken başlangıç ve bitiş zamanını yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95ea0-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="95ea0-150">**Başlatan** filtresi, bir aktörün adını ya da evrensel asıl adını (UPN) tanımlamanıza imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="95ea0-150">The **initiated by** filter enables you to define an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="95ea0-151">**Kategori** filtresi, aşağıdaki filtrelerden birini seçmenize imkan tanır:</span><span class="sxs-lookup"><span data-stu-id="95ea0-151">The **category** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="95ea0-152">Tümü</span><span class="sxs-lookup"><span data-stu-id="95ea0-152">All</span></span>
- <span data-ttu-id="95ea0-153">Çekirdek kategori</span><span class="sxs-lookup"><span data-stu-id="95ea0-153">Core category</span></span>
- <span data-ttu-id="95ea0-154">Çekirdek dizin</span><span class="sxs-lookup"><span data-stu-id="95ea0-154">Core directory</span></span>
- <span data-ttu-id="95ea0-155">Self servis parola yönetimi</span><span class="sxs-lookup"><span data-stu-id="95ea0-155">Self-service password management</span></span>
- <span data-ttu-id="95ea0-156">Self servis grup yönetimi</span><span class="sxs-lookup"><span data-stu-id="95ea0-156">Self-service group management</span></span>
- <span data-ttu-id="95ea0-157">Hesap sağlama - Otomatik parola geçişi</span><span class="sxs-lookup"><span data-stu-id="95ea0-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="95ea0-158">Davetli kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="95ea0-158">Invited users</span></span>
- <span data-ttu-id="95ea0-159">MIM hizmeti</span><span class="sxs-lookup"><span data-stu-id="95ea0-159">MIM service</span></span>
- <span data-ttu-id="95ea0-160">Kimlik Koruması</span><span class="sxs-lookup"><span data-stu-id="95ea0-160">Identity Protection</span></span>
- <span data-ttu-id="95ea0-161">B2C</span><span class="sxs-lookup"><span data-stu-id="95ea0-161">B2C</span></span>

<span data-ttu-id="95ea0-162">**Etkinlik kaynağı türü** filtresi, aşağıdaki filtrelerden birini seçmenize imkan tanır:</span><span class="sxs-lookup"><span data-stu-id="95ea0-162">The **activity resource type** filter enables you to select one of the following filters:</span></span>

- <span data-ttu-id="95ea0-163">Tümü</span><span class="sxs-lookup"><span data-stu-id="95ea0-163">All</span></span> 
- <span data-ttu-id="95ea0-164">Grup</span><span class="sxs-lookup"><span data-stu-id="95ea0-164">Group</span></span>
- <span data-ttu-id="95ea0-165">Dizin</span><span class="sxs-lookup"><span data-stu-id="95ea0-165">Directory</span></span>
- <span data-ttu-id="95ea0-166">Kullanıcı</span><span class="sxs-lookup"><span data-stu-id="95ea0-166">User</span></span>
- <span data-ttu-id="95ea0-167">Uygulama</span><span class="sxs-lookup"><span data-stu-id="95ea0-167">Application</span></span>
- <span data-ttu-id="95ea0-168">İlke</span><span class="sxs-lookup"><span data-stu-id="95ea0-168">Policy</span></span>
- <span data-ttu-id="95ea0-169">Cihaz</span><span class="sxs-lookup"><span data-stu-id="95ea0-169">Device</span></span>
- <span data-ttu-id="95ea0-170">Diğer</span><span class="sxs-lookup"><span data-stu-id="95ea0-170">Other</span></span>

<span data-ttu-id="95ea0-171">**Etkinlik kaynağı türü** olarak **Grup**’u seçtiğinizde, bir **Kaynak** sağlamanıza da imkan tanıyan ek bir filtre kategorisine sahip olursunuz:</span><span class="sxs-lookup"><span data-stu-id="95ea0-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you to also provide a **Source**:</span></span>

- <span data-ttu-id="95ea0-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="95ea0-172">Azure AD</span></span>
- <span data-ttu-id="95ea0-173">O365</span><span class="sxs-lookup"><span data-stu-id="95ea0-173">O365</span></span>


<span data-ttu-id="95ea0-174">**Etkinlik** filtresi, yaptığınız kategori ve Etkinlik kaynağı türü seçimine bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="95ea0-174">The **activity** filter is based on the category and Activity resource type selection you make.</span></span> <span data-ttu-id="95ea0-175">Görmek istediğiniz belirli bir etkinliği ya da tüm etkinlikleri seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95ea0-175">You can select a specific activity you want to see or choose all.</span></span> 

<span data-ttu-id="95ea0-176">Grafik API'si ($tenantdomain = etki alanı adınız olacak şekilde https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta) kullanarak tüm Denetim Etkinliklerinin listesini alabilir veya [denetim raporu olayları](active-directory-reporting-audit-events.md) makalesine bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95ea0-176">You can get the list of all Audit Activities using the Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer to the article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="95ea0-177">Denetim günlükleri kısayolları</span><span class="sxs-lookup"><span data-stu-id="95ea0-177">Audit logs shortcuts</span></span>

<span data-ttu-id="95ea0-178">Azure portalı, **Azure Active Directory**’ye ek olarak verileri denetlemeniz için fazladan iki giriş noktası sağlar:</span><span class="sxs-lookup"><span data-stu-id="95ea0-178">In addition to **Azure Active Directory**, the Azure portal provides you with two additional entry points to audit data:</span></span>

- <span data-ttu-id="95ea0-179">Kullanıcılar ve gruplar</span><span class="sxs-lookup"><span data-stu-id="95ea0-179">Users and groups</span></span>
- <span data-ttu-id="95ea0-180">Kurumsal uygulamalar</span><span class="sxs-lookup"><span data-stu-id="95ea0-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="95ea0-181">Kullanıcı ve gruplara yönelik denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="95ea0-181">Users and groups audit logs</span></span>

<span data-ttu-id="95ea0-182">Kullanıcı ve grup tabanlı denetim raporları ile aşağıdakiler gibi soruların yanıtlarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95ea0-182">With user and group-based audit reports, you can get answers to questions such as:</span></span>

- <span data-ttu-id="95ea0-183">Kullanıcılara hangi tür güncelleştirmeler uygulanmış?</span><span class="sxs-lookup"><span data-stu-id="95ea0-183">What types of updates have been applied the users?</span></span>

- <span data-ttu-id="95ea0-184">Kaç adet kullanıcı değiştirildi?</span><span class="sxs-lookup"><span data-stu-id="95ea0-184">How many users were changed?</span></span>

- <span data-ttu-id="95ea0-185">Kaç adet parola değiştirildi?</span><span class="sxs-lookup"><span data-stu-id="95ea0-185">How many passwords were changed?</span></span>

- <span data-ttu-id="95ea0-186">Bir yönetici bir dizinde neler yaptı?</span><span class="sxs-lookup"><span data-stu-id="95ea0-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="95ea0-187">Eklenmiş olan gruplar hangileridir?</span><span class="sxs-lookup"><span data-stu-id="95ea0-187">What are the groups that have been added?</span></span>

- <span data-ttu-id="95ea0-188">Üyelik değişiklikleri olan gruplar var mı?</span><span class="sxs-lookup"><span data-stu-id="95ea0-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="95ea0-189">Grubun sahipleri değişti mi?</span><span class="sxs-lookup"><span data-stu-id="95ea0-189">Have the owners of group been changed?</span></span>

- <span data-ttu-id="95ea0-190">Bir grup veya kullanıcıya hangi lisanslar atanmış?</span><span class="sxs-lookup"><span data-stu-id="95ea0-190">What licenses have been assigned to a group or a user?</span></span>

<span data-ttu-id="95ea0-191">Yalnızca kullanıcı ve gruplarla ilgili denetim verilerini gözden geçirmek istiyorsanız, **Kullanıcılar ve Gruplar**’ın **Etkinlik** bölümündeki **Denetim günlükleri** altında filtrelenmiş bir görünüm bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95ea0-191">If you just want to review auditing data that is related to users and groups, you can find a filtered view under **Audit logs** in the **Activity** section of the **Users and Groups**.</span></span> <span data-ttu-id="95ea0-192">Bu giriş noktasında, **Etkinlik Kaynağı Türü** olarak **Kullanıcılar ve gruplar** önceden seçilidir.</span><span class="sxs-lookup"><span data-stu-id="95ea0-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="95ea0-193">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/93.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="95ea0-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="95ea0-194">Kurumsal uygulamaların denetim günlükleri</span><span class="sxs-lookup"><span data-stu-id="95ea0-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="95ea0-195">Uygulama tabanlı denetim raporları ile aşağıdakiler gibi soruların yanıtlarını alabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95ea0-195">With application-based audit reports, you can get answers to questions such as:</span></span>

* <span data-ttu-id="95ea0-196">Eklenmiş veya güncelleştirilmiş olan uygulamalar hangileridir?</span><span class="sxs-lookup"><span data-stu-id="95ea0-196">What are the applications that have been added or updated?</span></span>
* <span data-ttu-id="95ea0-197">Kaldırılmış olan uygulamalar hangileridir?</span><span class="sxs-lookup"><span data-stu-id="95ea0-197">What are the applications that have been removed?</span></span>
* <span data-ttu-id="95ea0-198">Belirli bir uygulamaya ait bir hizmet ilkesi değiştirildi mi?</span><span class="sxs-lookup"><span data-stu-id="95ea0-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="95ea0-199">Uygulamaların adları değiştirildi mi?</span><span class="sxs-lookup"><span data-stu-id="95ea0-199">Have the names of applications been changed?</span></span>
* <span data-ttu-id="95ea0-200">Belirli bir uygulama için kim onay verdi?</span><span class="sxs-lookup"><span data-stu-id="95ea0-200">Who gave consent to an application?</span></span>

<span data-ttu-id="95ea0-201">Yalnızca uygulamalarınızla ilgili denetim verilerini gözden geçirmek istiyorsanız, **Kurumsal uygulamalar** dikey penceresinin **Etkinlik** bölümündeki **Denetim günlükleri** altında filtrelenmiş bir görünüm bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95ea0-201">If you just want to review auditing data that is related to your applications, you can find a filtered view under **Audit logs** in the **Activity** section of the **Enterprise applications** blade.</span></span> <span data-ttu-id="95ea0-202">Bu giriş noktasında, **Etkinlik Kaynağı Türü** olarak **Kurumsal uygulamalar** önceden seçilidir.</span><span class="sxs-lookup"><span data-stu-id="95ea0-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="95ea0-203">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/134.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="95ea0-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="95ea0-204">Bu görünümü yalnızca **grupları** veya yalnızca **kullanıcıları** içerecek şekilde filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95ea0-204">You can filter this view further down to just **groups** or just **users**.</span></span>

<span data-ttu-id="95ea0-205">![Denetim günlükleri](./media/active-directory-reporting-activity-audit-logs/25.png "Denetim günlükleri")</span><span class="sxs-lookup"><span data-stu-id="95ea0-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="95ea0-206">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="95ea0-206">Next steps</span></span>

<span data-ttu-id="95ea0-207">Raporlamaya genel bir bakış için bkz. [Azure Active Directory raporlama](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="95ea0-207">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

