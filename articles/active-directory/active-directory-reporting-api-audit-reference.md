---
title: "aaaAzure Active Directory denetim API Başvurusu | Microsoft Docs"
description: "Tooget hello Azure Active Directory denetim API'si ile çalışmaya nasıl"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="03c41-103">Azure Active Directory denetim API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="03c41-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="03c41-104">Bu konu hello Azure Active Directory ilgili konulara koleksiyonu parçasıdır raporlama API'si.</span><span class="sxs-lookup"><span data-stu-id="03c41-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="03c41-105">Azure AD raporlama kodu veya ilgili araçları kullanarak tooaccess denetim veri sağlayan bir API ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="03c41-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="03c41-106">Bu konunun Hello kapsamı olan tooprovide hello hakkında başvuru bilgileri sizinle **API denetim**.</span><span class="sxs-lookup"><span data-stu-id="03c41-106">hello scope of this topic is tooprovide you with reference information about hello **audit API**.</span></span>

<span data-ttu-id="03c41-107">Bkz.:</span><span class="sxs-lookup"><span data-stu-id="03c41-107">See:</span></span>

* <span data-ttu-id="03c41-108">[Denetim günlükleri](active-directory-reporting-azure-portal.md#activity-reports) daha fazla kavramsal bilgi için</span><span class="sxs-lookup"><span data-stu-id="03c41-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="03c41-109">[Hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) hello raporlama API'si hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="03c41-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


<span data-ttu-id="03c41-110">İçin:</span><span class="sxs-lookup"><span data-stu-id="03c41-110">For:</span></span>

- <span data-ttu-id="03c41-111">Sık sorulan sorular, okuma bizim [SSS](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="03c41-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="03c41-112">Sorunları, lütfen [bir destek bileti dosya](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="03c41-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-hello-data"></a><span data-ttu-id="03c41-113">Merhaba veri erişebilecek mi?</span><span class="sxs-lookup"><span data-stu-id="03c41-113">Who can access hello data?</span></span>
* <span data-ttu-id="03c41-114">Merhaba Güvenlik Yöneticisi veya güvenlik okuyucu roldeki kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="03c41-114">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="03c41-115">Genel Yöneticiler</span><span class="sxs-lookup"><span data-stu-id="03c41-115">Global Admins</span></span>
* <span data-ttu-id="03c41-116">Yetkilendirme tooaccess hello API sahip herhangi bir uygulama (app yetkilendirme olabilir Kurulum genel yöneticinin iznine dayanılarak yalnızca)</span><span class="sxs-lookup"><span data-stu-id="03c41-116">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03c41-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="03c41-117">Prerequisites</span></span>
<span data-ttu-id="03c41-118">Bu rapor aracılığıyla sipariş tooaccess içinde raporlama API'si Merhaba, sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="03c41-118">In order tooaccess this report through hello Reporting API, you must have:</span></span>

* <span data-ttu-id="03c41-119">Bir [Azure Active Directory ücretsiz ya da daha iyi edition](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="03c41-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="03c41-120">Tamamlanan hello [Önkoşullar tooaccess hello Azure AD raporlama API'si](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="03c41-120">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="03c41-121">Merhaba API'sine erişim</span><span class="sxs-lookup"><span data-stu-id="03c41-121">Accessing hello API</span></span>
<span data-ttu-id="03c41-122">Bu API hello erişebilirsiniz [Graph Explorer'a](https://graphexplorer2.cloudapp.net) veya program aracılığıyla, örneğin, PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="03c41-122">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="03c41-123">Sırayla PowerShell toocorrectly yorumlamak için AAD grafik REST çağrılarında kullanılan hello OData filtresi sözdizimi hello backtick kullanmanız gerekir (diğer adıyla: Vurgu) çok "kaçış karakteri" Merhaba $ karakteri.</span><span class="sxs-lookup"><span data-stu-id="03c41-123">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="03c41-124">Merhaba backtick karakter görür [PowerShell'in kaçış karakteri](https://technet.microsoft.com/library/hh847755.aspx)PowerShell toodo hello $ karakteri değişmez değer yorumu izin verme ve PowerShell değişken adı olarak kafa karıştırıcı kaçının (IE: $filter).</span><span class="sxs-lookup"><span data-stu-id="03c41-124">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="03c41-125">Bu konunun Hello odak Graph Explorer'a hello üzerinde noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="03c41-125">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="03c41-126">Bu PowerShell örnek için bkz [PowerShell Betiği](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="03c41-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="03c41-127">API uç noktası</span><span class="sxs-lookup"><span data-stu-id="03c41-127">API Endpoint</span></span>
<span data-ttu-id="03c41-128">Bu API URI aşağıdaki hello kullanarak erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="03c41-128">You can access this API using hello following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="03c41-129">(OData sayfalandırma kullanarak) hello Azure AD denetim API'si tarafından döndürülen kayıt hello sayısına bir sınır yoktur.</span><span class="sxs-lookup"><span data-stu-id="03c41-129">There is no limit on hello number of records returned by hello Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="03c41-130">Bekletme sınırları veri raporlama, kullanıma [raporlama bekletme ilkeleri](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="03c41-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="03c41-131">Bu çağrı hello verileri toplu olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="03c41-131">This call returns hello data in batches.</span></span> <span data-ttu-id="03c41-132">Her toplu işlem en fazla 1000 kaydı var.</span><span class="sxs-lookup"><span data-stu-id="03c41-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="03c41-133">tooget hello sonraki toplu kayıt, kullanım hello sonraki bağlantı.</span><span class="sxs-lookup"><span data-stu-id="03c41-133">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="03c41-134">Merhaba skiptoken bilgi hello ilk döndürülen kayıt kümesinden alın.</span><span class="sxs-lookup"><span data-stu-id="03c41-134">Get hello skiptoken information from hello first set of returned records.</span></span> <span data-ttu-id="03c41-135">Merhaba Atla belirteci hello hello sonuç kümesinin sonunda olacaktır.</span><span class="sxs-lookup"><span data-stu-id="03c41-135">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="03c41-136">Desteklenen filtreler</span><span class="sxs-lookup"><span data-stu-id="03c41-136">Supported filters</span></span>
<span data-ttu-id="03c41-137">Bir API tarafından döndürülen kayıt sayısını hello daraltabilirsiniz bir filtre formda çağırın.</span><span class="sxs-lookup"><span data-stu-id="03c41-137">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="03c41-138">Oturum açma için API ilgili veriler, filtreleri aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="03c41-138">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="03c41-139">**$top =\<döndürülen kayıt toobe sayısı\>**  -toolimit hello döndürülen kayıt sayısı.</span><span class="sxs-lookup"><span data-stu-id="03c41-139">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="03c41-140">Bu pahalı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="03c41-140">This is an expensive operation.</span></span> <span data-ttu-id="03c41-141">Nesnelerin tooreturn binlerce istiyorsanız bu filtre kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="03c41-141">You should not use this filter if you want tooreturn thousands of objects.</span></span>     
* <span data-ttu-id="03c41-142">**$filter =\<filtre ifadesi\>**  -desteklenen filtre alanlarının önem verdiğiniz kayıtların hello türünü hello temelinde toospecify</span><span class="sxs-lookup"><span data-stu-id="03c41-142">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="03c41-143">Desteklenen filtre alanları ve işleçleri</span><span class="sxs-lookup"><span data-stu-id="03c41-143">Supported filter fields and operators</span></span>
<span data-ttu-id="03c41-144">İlgilendiğiniz kayıtları toospecify hello türü, bir veya filtre alanları aşağıdaki hello bir birleşimini içerebilir bir filtre ifadesi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="03c41-144">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="03c41-145">[Tarihi](#activitydate) -bir tarih veya tarih aralığı tanımlar</span><span class="sxs-lookup"><span data-stu-id="03c41-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="03c41-146">[Kategori](#category) -üzerinde toofilter istediğiniz hello kategorisini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="03c41-146">[category](#category) - defines hello category you want toofilter on.</span></span>
* <span data-ttu-id="03c41-147">[activityStatus](#activitystatus) -bir etkinlik hello durumunu tanımlar</span><span class="sxs-lookup"><span data-stu-id="03c41-147">[activityStatus](#activitystatus) - defines hello status of an activity</span></span>
* <span data-ttu-id="03c41-148">[activityType](#activitytype) -bir etkinlik hello türünü tanımlar</span><span class="sxs-lookup"><span data-stu-id="03c41-148">[activityType](#activitytype)  - defines hello type of an activity</span></span>
* <span data-ttu-id="03c41-149">[Etkinlik](#activity) -dize olarak hello etkinlik tanımlar</span><span class="sxs-lookup"><span data-stu-id="03c41-149">[activity](#activity) - defines hello activity as string</span></span>  
* <span data-ttu-id="03c41-150">[Aktör/adı](#actorname) -hello aktör'ın adı biçiminde hello aktör tanımlar</span><span class="sxs-lookup"><span data-stu-id="03c41-150">[actor/name](#actorname) -   defines hello actor in form of hello actor's name</span></span>
* <span data-ttu-id="03c41-151">[Aktör/objectID](#actorobjectid) -hello aktör'ın kimliği biçiminde hello aktör tanımlar</span><span class="sxs-lookup"><span data-stu-id="03c41-151">[actor/objectid](#actorobjectid) - defines hello actor in form of hello actor's ID</span></span>   
* <span data-ttu-id="03c41-152">[Aktör/upn](#actorupn) -hello aktör'ın kullanıcı asıl adı (UPN) biçiminde hello aktör tanımlar</span><span class="sxs-lookup"><span data-stu-id="03c41-152">[actor/upn](#actorupn)  - defines hello actor in form of hello actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="03c41-153">[Hedef/adı](#targetname) -hello aktör'ın adı biçiminde hello hedef tanımlar</span><span class="sxs-lookup"><span data-stu-id="03c41-153">[target/name](#targetname)  - defines hello target in form of hello actor's name</span></span>
* <span data-ttu-id="03c41-154">[Hedef/objectID](#targetobjectid) -hello hedefin kimliği biçiminde hello hedef tanımlar</span><span class="sxs-lookup"><span data-stu-id="03c41-154">[target/objectid](#targetobjectid) - defines hello target in form of hello target's ID</span></span>  
* <span data-ttu-id="03c41-155">[Hedef/upn](#targetupn) -hello aktör'ın kullanıcı asıl adı (UPN) biçiminde hello aktör tanımlar</span><span class="sxs-lookup"><span data-stu-id="03c41-155">[target/upn](#targetupn) - defines hello actor in form of hello actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="03c41-156">Tarihi</span><span class="sxs-lookup"><span data-stu-id="03c41-156">activityDate</span></span>
<span data-ttu-id="03c41-157">**İşleçler desteklenen**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="03c41-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="03c41-158">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="03c41-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="03c41-159">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="03c41-159">**Notes**:</span></span>

<span data-ttu-id="03c41-160">DateTime UTC biçiminde olmalıdır</span><span class="sxs-lookup"><span data-stu-id="03c41-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="03c41-161">category</span><span class="sxs-lookup"><span data-stu-id="03c41-161">category</span></span>

<span data-ttu-id="03c41-162">**Desteklenen değerler**:</span><span class="sxs-lookup"><span data-stu-id="03c41-162">**Supported values**:</span></span>

| <span data-ttu-id="03c41-163">Kategori</span><span class="sxs-lookup"><span data-stu-id="03c41-163">Category</span></span>                         | <span data-ttu-id="03c41-164">Değer</span><span class="sxs-lookup"><span data-stu-id="03c41-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="03c41-165">Çekirdek Dizin</span><span class="sxs-lookup"><span data-stu-id="03c41-165">Core Directory</span></span>                   | <span data-ttu-id="03c41-166">Dizin</span><span class="sxs-lookup"><span data-stu-id="03c41-166">Directory</span></span> |
| <span data-ttu-id="03c41-167">Self Servis Parola Yönetimi</span><span class="sxs-lookup"><span data-stu-id="03c41-167">Self-service Password Management</span></span> | <span data-ttu-id="03c41-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="03c41-168">SSPR</span></span>      |
| <span data-ttu-id="03c41-169">Self Servis Grup Yönetimi</span><span class="sxs-lookup"><span data-stu-id="03c41-169">Self-service Group Management</span></span>    | <span data-ttu-id="03c41-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="03c41-170">SSGM</span></span>      |
| <span data-ttu-id="03c41-171">Hesap Sağlama</span><span class="sxs-lookup"><span data-stu-id="03c41-171">Account Provisioning</span></span>             | <span data-ttu-id="03c41-172">Sync</span><span class="sxs-lookup"><span data-stu-id="03c41-172">Sync</span></span>      |
| <span data-ttu-id="03c41-173">Otomatik Parola Geçişi</span><span class="sxs-lookup"><span data-stu-id="03c41-173">Automated Password Rollover</span></span>      | <span data-ttu-id="03c41-174">Otomatik Parola Geçişi</span><span class="sxs-lookup"><span data-stu-id="03c41-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="03c41-175">Kimlik Koruması</span><span class="sxs-lookup"><span data-stu-id="03c41-175">Identity Protection</span></span>              | <span data-ttu-id="03c41-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="03c41-176">IdentityProtection</span></span> |
| <span data-ttu-id="03c41-177">Davetli Kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="03c41-177">Invited Users</span></span>                    | <span data-ttu-id="03c41-178">Davetli Kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="03c41-178">Invited Users</span></span> |
| <span data-ttu-id="03c41-179">MIM Hizmeti</span><span class="sxs-lookup"><span data-stu-id="03c41-179">MIM Service</span></span>                      | <span data-ttu-id="03c41-180">MIM Hizmeti</span><span class="sxs-lookup"><span data-stu-id="03c41-180">MIM Service</span></span> |



<span data-ttu-id="03c41-181">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="03c41-181">**Supported operators**: eq</span></span>

<span data-ttu-id="03c41-182">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="03c41-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="03c41-183">ActivityStatus</span><span class="sxs-lookup"><span data-stu-id="03c41-183">activityStatus</span></span>

<span data-ttu-id="03c41-184">**Desteklenen değerler**:</span><span class="sxs-lookup"><span data-stu-id="03c41-184">**Supported values**:</span></span>

| <span data-ttu-id="03c41-185">Etkinlik durumu</span><span class="sxs-lookup"><span data-stu-id="03c41-185">Activity Status</span></span> | <span data-ttu-id="03c41-186">Değer</span><span class="sxs-lookup"><span data-stu-id="03c41-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="03c41-187">Başarılı</span><span class="sxs-lookup"><span data-stu-id="03c41-187">Success</span></span>         | <span data-ttu-id="03c41-188">0</span><span class="sxs-lookup"><span data-stu-id="03c41-188">0</span></span>     |
| <span data-ttu-id="03c41-189">Hata</span><span class="sxs-lookup"><span data-stu-id="03c41-189">Failure</span></span>         | <span data-ttu-id="03c41-190">- 1</span><span class="sxs-lookup"><span data-stu-id="03c41-190">- 1</span></span>   |

<span data-ttu-id="03c41-191">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="03c41-191">**Supported operators**: eq</span></span>

<span data-ttu-id="03c41-192">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="03c41-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="03c41-193">activityType</span><span class="sxs-lookup"><span data-stu-id="03c41-193">activityType</span></span>
<span data-ttu-id="03c41-194">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="03c41-194">**Supported operators**: eq</span></span>

<span data-ttu-id="03c41-195">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="03c41-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="03c41-196">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="03c41-196">**Notes**:</span></span>

<span data-ttu-id="03c41-197">büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="03c41-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="03c41-198">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="03c41-198">activity</span></span>
<span data-ttu-id="03c41-199">**İşleçler desteklenen**: eq, içerir, startsWith</span><span class="sxs-lookup"><span data-stu-id="03c41-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="03c41-200">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="03c41-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="03c41-201">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="03c41-201">**Notes**:</span></span>

<span data-ttu-id="03c41-202">büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="03c41-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="03c41-203">Aktör/adı</span><span class="sxs-lookup"><span data-stu-id="03c41-203">actor/name</span></span>
<span data-ttu-id="03c41-204">**İşleçler desteklenen**: eq, içerir, startsWith</span><span class="sxs-lookup"><span data-stu-id="03c41-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="03c41-205">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="03c41-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="03c41-206">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="03c41-206">**Notes**:</span></span>

<span data-ttu-id="03c41-207">Büyük küçük harfe duyarsızdır</span><span class="sxs-lookup"><span data-stu-id="03c41-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="03c41-208">Aktör/objectID</span><span class="sxs-lookup"><span data-stu-id="03c41-208">actor/objectId</span></span>
<span data-ttu-id="03c41-209">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="03c41-209">**Supported operators**: eq</span></span>

<span data-ttu-id="03c41-210">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="03c41-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="03c41-211">Hedef/adı</span><span class="sxs-lookup"><span data-stu-id="03c41-211">target/name</span></span>
<span data-ttu-id="03c41-212">**İşleçler desteklenen**: eq, içerir, startsWith</span><span class="sxs-lookup"><span data-stu-id="03c41-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="03c41-213">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="03c41-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="03c41-214">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="03c41-214">**Notes**:</span></span>

<span data-ttu-id="03c41-215">Büyük küçük harfe duyarsızdır</span><span class="sxs-lookup"><span data-stu-id="03c41-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="03c41-216">Hedef/upn</span><span class="sxs-lookup"><span data-stu-id="03c41-216">target/upn</span></span>
<span data-ttu-id="03c41-217">**İşleçler desteklenen**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="03c41-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="03c41-218">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="03c41-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="03c41-219">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="03c41-219">**Notes**:</span></span>

* <span data-ttu-id="03c41-220">Büyük küçük harfe duyarsızdır</span><span class="sxs-lookup"><span data-stu-id="03c41-220">Case-insensitive</span></span>
* <span data-ttu-id="03c41-221">Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity sorgulanırken tooadd hello tam ad alanı gerekir</span><span class="sxs-lookup"><span data-stu-id="03c41-221">You need tooadd hello full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="03c41-222">Hedef/objectID</span><span class="sxs-lookup"><span data-stu-id="03c41-222">target/objectId</span></span>
<span data-ttu-id="03c41-223">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="03c41-223">**Supported operators**: eq</span></span>

<span data-ttu-id="03c41-224">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="03c41-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="03c41-225">Aktör/upn</span><span class="sxs-lookup"><span data-stu-id="03c41-225">actor/upn</span></span>
<span data-ttu-id="03c41-226">**İşleçler desteklenen**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="03c41-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="03c41-227">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="03c41-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="03c41-228">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="03c41-228">**Notes**:</span></span>

* <span data-ttu-id="03c41-229">Büyük küçük harfe duyarsızdır</span><span class="sxs-lookup"><span data-stu-id="03c41-229">Case-insensitive</span></span> 
* <span data-ttu-id="03c41-230">Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity sorgulanırken tooadd hello tam ad alanı gerekir</span><span class="sxs-lookup"><span data-stu-id="03c41-230">You need tooadd hello full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="03c41-231">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="03c41-231">Next Steps</span></span>
* <span data-ttu-id="03c41-232">Filtrelenmiş sistem etkinlikler için toosee örnekler istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="03c41-232">Do you want toosee examples for filtered system activities?</span></span> <span data-ttu-id="03c41-233">Merhaba denetleyin [Azure Active Directory denetim API'si örnekleri](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="03c41-233">Check out hello [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="03c41-234">Tooknow hello Azure AD raporlama API'si hakkında daha fazla istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="03c41-234">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="03c41-235">Bkz: [hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="03c41-235">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

