---
title: "Azure Active Directory denetim API Başvurusu | Microsoft Docs"
description: "Azure Active Directory denetim API'si ile çalışmaya nasıl başlayacağınız"
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
ms.openlocfilehash: 573e940c5390e7b990d889681eb37b73c5b253d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="77ff9-103">Azure Active Directory denetim API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="77ff9-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="77ff9-104">Bu konuda, Azure Active Directory hakkındaki konuları API raporlama koleksiyonu bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="77ff9-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="77ff9-105">Azure AD raporlama kodu veya ilgili araçları kullanarak denetim veri erişmenizi sağlayan bir API ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="77ff9-105">Azure AD reporting provides you with an API that enables you to access audit data using code or related tools.</span></span>
<span data-ttu-id="77ff9-106">Hakkında başvuru bilgileri sağlamak için bu konunun kapsamı olan **API denetim**.</span><span class="sxs-lookup"><span data-stu-id="77ff9-106">The scope of this topic is to provide you with reference information about the **audit API**.</span></span>

<span data-ttu-id="77ff9-107">Bkz.:</span><span class="sxs-lookup"><span data-stu-id="77ff9-107">See:</span></span>

* <span data-ttu-id="77ff9-108">[Denetim günlükleri](active-directory-reporting-azure-portal.md#activity-reports) daha fazla kavramsal bilgi için</span><span class="sxs-lookup"><span data-stu-id="77ff9-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="77ff9-109">[Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) raporlama API'si hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="77ff9-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


<span data-ttu-id="77ff9-110">İçin:</span><span class="sxs-lookup"><span data-stu-id="77ff9-110">For:</span></span>

- <span data-ttu-id="77ff9-111">Sık sorulan sorular, okuma bizim [SSS](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="77ff9-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="77ff9-112">Sorunları, lütfen [bir destek bileti dosya](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="77ff9-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-the-data"></a><span data-ttu-id="77ff9-113">Verilere kimler erişebilir?</span><span class="sxs-lookup"><span data-stu-id="77ff9-113">Who can access the data?</span></span>
* <span data-ttu-id="77ff9-114">Güvenlik Yöneticisi veya Güvenlik Okuyucusu rolündeki kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="77ff9-114">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="77ff9-115">Genel Yöneticiler</span><span class="sxs-lookup"><span data-stu-id="77ff9-115">Global Admins</span></span>
* <span data-ttu-id="77ff9-116">API erişme yetkisi olan herhangi bir uygulama (app yetkilendirme olabilir Kurulum genel yöneticinin iznine dayanılarak yalnızca)</span><span class="sxs-lookup"><span data-stu-id="77ff9-116">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77ff9-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="77ff9-117">Prerequisites</span></span>
<span data-ttu-id="77ff9-118">Bu rapor raporlama API'si erişmek için sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="77ff9-118">In order to access this report through the Reporting API, you must have:</span></span>

* <span data-ttu-id="77ff9-119">Bir [Azure Active Directory ücretsiz ya da daha iyi edition](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="77ff9-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="77ff9-120">Tamamlanan [Azure AD raporlama API'si erişmek için Önkoşullar](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="77ff9-120">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="77ff9-121">API erişme</span><span class="sxs-lookup"><span data-stu-id="77ff9-121">Accessing the API</span></span>
<span data-ttu-id="77ff9-122">Bu API aracılığıyla da erişebilirsiniz [Graph Explorer'a](https://graphexplorer2.cloudapp.net) veya program aracılığıyla, örneğin, PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="77ff9-122">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="77ff9-123">AAD grafik REST çağrılarında kullanılan OData filtresi sözdizimi doğru şekilde yorumlamaya PowerShell sırayla backtick kullanmanız gerekir (diğer adıyla: Vurgu) "$ karakterini atlamak için" karakter.</span><span class="sxs-lookup"><span data-stu-id="77ff9-123">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="77ff9-124">Backtick karakter gören [PowerShell'in kaçış karakteri](https://technet.microsoft.com/library/hh847755.aspx), sabit bir $ karakteri yorumu yapın ve PowerShell değişken adı olarak kafa karıştırıcı önlemek PowerShell izin verme (IE: $filter).</span><span class="sxs-lookup"><span data-stu-id="77ff9-124">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="77ff9-125">Bu konunun odak Graph Explorer'a noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="77ff9-125">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="77ff9-126">Bu PowerShell örnek için bkz [PowerShell Betiği](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="77ff9-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="77ff9-127">API uç noktası</span><span class="sxs-lookup"><span data-stu-id="77ff9-127">API Endpoint</span></span>
<span data-ttu-id="77ff9-128">Bu API aşağıdaki URI'ı kullanarak erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="77ff9-128">You can access this API using the following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="77ff9-129">(OData sayfalandırma kullanarak) Azure AD denetim API'si tarafından döndürülen kayıt sayısı sınırı yoktur.</span><span class="sxs-lookup"><span data-stu-id="77ff9-129">There is no limit on the number of records returned by the Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="77ff9-130">Bekletme sınırları veri raporlama, kullanıma [raporlama bekletme ilkeleri](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="77ff9-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="77ff9-131">Bu çağrı verileri toplu olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="77ff9-131">This call returns the data in batches.</span></span> <span data-ttu-id="77ff9-132">Her toplu işlem en fazla 1000 kaydı var.</span><span class="sxs-lookup"><span data-stu-id="77ff9-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="77ff9-133">Sonraki toplu kayıt almak için sonraki bağlantıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="77ff9-133">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="77ff9-134">Döndürülen kayıtları ilk kümesinden skiptoken bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="77ff9-134">Get the skiptoken information from the first set of returned records.</span></span> <span data-ttu-id="77ff9-135">Atla belirteci sonucu sonunda ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="77ff9-135">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="77ff9-136">Desteklenen filtreler</span><span class="sxs-lookup"><span data-stu-id="77ff9-136">Supported filters</span></span>
<span data-ttu-id="77ff9-137">Bir API tarafından döndürülen kayıt sayısını daraltabilirsiniz bir filtre formda çağırın.</span><span class="sxs-lookup"><span data-stu-id="77ff9-137">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="77ff9-138">Oturum açma için API ilgili verileri, aşağıdaki filtreleri desteklenir:</span><span class="sxs-lookup"><span data-stu-id="77ff9-138">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="77ff9-139">**$top =\<döndürülecek kayıtları numara\>**  - döndürülen kayıt sayısını sınırlamak için.</span><span class="sxs-lookup"><span data-stu-id="77ff9-139">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="77ff9-140">Bu pahalı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="77ff9-140">This is an expensive operation.</span></span> <span data-ttu-id="77ff9-141">Binlerce nesneyi dönmek istiyorsanız, bu filtre kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="77ff9-141">You should not use this filter if you want to return thousands of objects.</span></span>     
* <span data-ttu-id="77ff9-142">**$filter =\<filtre ifadesi\>**  -, desteklenen filtre alanları temel alarak çok önem verdiğiniz kayıtları türünü belirtmek için</span><span class="sxs-lookup"><span data-stu-id="77ff9-142">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="77ff9-143">Desteklenen filtre alanları ve işleçleri</span><span class="sxs-lookup"><span data-stu-id="77ff9-143">Supported filter fields and operators</span></span>
<span data-ttu-id="77ff9-144">İlgilendiğiniz kayıtları türünü belirtmek için bir ya da aşağıdaki filtre alanlarını bileşimini içerebilir bir filtre ifadesi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="77ff9-144">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="77ff9-145">[Tarihi](#activitydate) -bir tarih veya tarih aralığı tanımlar</span><span class="sxs-lookup"><span data-stu-id="77ff9-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="77ff9-146">[Kategori](#category) -filtre uygulamak istediğiniz kategori tanımlar.</span><span class="sxs-lookup"><span data-stu-id="77ff9-146">[category](#category) - defines the category you want to filter on.</span></span>
* <span data-ttu-id="77ff9-147">[activityStatus](#activitystatus) -bir etkinlik durumunu tanımlar</span><span class="sxs-lookup"><span data-stu-id="77ff9-147">[activityStatus](#activitystatus) - defines the status of an activity</span></span>
* <span data-ttu-id="77ff9-148">[activityType](#activitytype) -bir etkinlik türünü tanımlar</span><span class="sxs-lookup"><span data-stu-id="77ff9-148">[activityType](#activitytype)  - defines the type of an activity</span></span>
* <span data-ttu-id="77ff9-149">[Etkinlik](#activity) -dize olarak etkinliğini tanımlar</span><span class="sxs-lookup"><span data-stu-id="77ff9-149">[activity](#activity) - defines the activity as string</span></span>  
* <span data-ttu-id="77ff9-150">[Aktör/adı](#actorname) -aktör aktör'ın adı biçiminde tanımlar</span><span class="sxs-lookup"><span data-stu-id="77ff9-150">[actor/name](#actorname) -   defines the actor in form of the actor's name</span></span>
* <span data-ttu-id="77ff9-151">[Aktör/objectID](#actorobjectid) -aktör aktör'ın kimliği formunda tanımlar</span><span class="sxs-lookup"><span data-stu-id="77ff9-151">[actor/objectid](#actorobjectid) - defines the actor in form of the actor's ID</span></span>   
* <span data-ttu-id="77ff9-152">[Aktör/upn](#actorupn) -aktör aktör'ın kullanıcı asıl adı (UPN) biçiminde tanımlar</span><span class="sxs-lookup"><span data-stu-id="77ff9-152">[actor/upn](#actorupn)  - defines the actor in form of the actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="77ff9-153">[Hedef/adı](#targetname) -hedef aktör'ın adı biçiminde tanımlar</span><span class="sxs-lookup"><span data-stu-id="77ff9-153">[target/name](#targetname)  - defines the target in form of the actor's name</span></span>
* <span data-ttu-id="77ff9-154">[Hedef/objectID](#targetobjectid) -hedef hedefin kimliği formunda tanımlar</span><span class="sxs-lookup"><span data-stu-id="77ff9-154">[target/objectid](#targetobjectid) - defines the target in form of the target's ID</span></span>  
* <span data-ttu-id="77ff9-155">[Hedef/upn](#targetupn) -aktör aktör'ın kullanıcı asıl adı (UPN) biçiminde tanımlar</span><span class="sxs-lookup"><span data-stu-id="77ff9-155">[target/upn](#targetupn) - defines the actor in form of the actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="77ff9-156">Tarihi</span><span class="sxs-lookup"><span data-stu-id="77ff9-156">activityDate</span></span>
<span data-ttu-id="77ff9-157">**İşleçler desteklenen**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="77ff9-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="77ff9-158">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="77ff9-159">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-159">**Notes**:</span></span>

<span data-ttu-id="77ff9-160">DateTime UTC biçiminde olmalıdır</span><span class="sxs-lookup"><span data-stu-id="77ff9-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="77ff9-161">category</span><span class="sxs-lookup"><span data-stu-id="77ff9-161">category</span></span>

<span data-ttu-id="77ff9-162">**Desteklenen değerler**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-162">**Supported values**:</span></span>

| <span data-ttu-id="77ff9-163">Kategori</span><span class="sxs-lookup"><span data-stu-id="77ff9-163">Category</span></span>                         | <span data-ttu-id="77ff9-164">Değer</span><span class="sxs-lookup"><span data-stu-id="77ff9-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="77ff9-165">Çekirdek Dizin</span><span class="sxs-lookup"><span data-stu-id="77ff9-165">Core Directory</span></span>                   | <span data-ttu-id="77ff9-166">Dizin</span><span class="sxs-lookup"><span data-stu-id="77ff9-166">Directory</span></span> |
| <span data-ttu-id="77ff9-167">Self Servis Parola Yönetimi</span><span class="sxs-lookup"><span data-stu-id="77ff9-167">Self-service Password Management</span></span> | <span data-ttu-id="77ff9-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="77ff9-168">SSPR</span></span>      |
| <span data-ttu-id="77ff9-169">Self Servis Grup Yönetimi</span><span class="sxs-lookup"><span data-stu-id="77ff9-169">Self-service Group Management</span></span>    | <span data-ttu-id="77ff9-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="77ff9-170">SSGM</span></span>      |
| <span data-ttu-id="77ff9-171">Hesap Sağlama</span><span class="sxs-lookup"><span data-stu-id="77ff9-171">Account Provisioning</span></span>             | <span data-ttu-id="77ff9-172">Sync</span><span class="sxs-lookup"><span data-stu-id="77ff9-172">Sync</span></span>      |
| <span data-ttu-id="77ff9-173">Otomatik Parola Geçişi</span><span class="sxs-lookup"><span data-stu-id="77ff9-173">Automated Password Rollover</span></span>      | <span data-ttu-id="77ff9-174">Otomatik Parola Geçişi</span><span class="sxs-lookup"><span data-stu-id="77ff9-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="77ff9-175">Kimlik Koruması</span><span class="sxs-lookup"><span data-stu-id="77ff9-175">Identity Protection</span></span>              | <span data-ttu-id="77ff9-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="77ff9-176">IdentityProtection</span></span> |
| <span data-ttu-id="77ff9-177">Davetli Kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="77ff9-177">Invited Users</span></span>                    | <span data-ttu-id="77ff9-178">Davetli Kullanıcılar</span><span class="sxs-lookup"><span data-stu-id="77ff9-178">Invited Users</span></span> |
| <span data-ttu-id="77ff9-179">MIM Hizmeti</span><span class="sxs-lookup"><span data-stu-id="77ff9-179">MIM Service</span></span>                      | <span data-ttu-id="77ff9-180">MIM Hizmeti</span><span class="sxs-lookup"><span data-stu-id="77ff9-180">MIM Service</span></span> |



<span data-ttu-id="77ff9-181">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="77ff9-181">**Supported operators**: eq</span></span>

<span data-ttu-id="77ff9-182">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="77ff9-183">ActivityStatus</span><span class="sxs-lookup"><span data-stu-id="77ff9-183">activityStatus</span></span>

<span data-ttu-id="77ff9-184">**Desteklenen değerler**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-184">**Supported values**:</span></span>

| <span data-ttu-id="77ff9-185">Etkinlik durumu</span><span class="sxs-lookup"><span data-stu-id="77ff9-185">Activity Status</span></span> | <span data-ttu-id="77ff9-186">Değer</span><span class="sxs-lookup"><span data-stu-id="77ff9-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="77ff9-187">Başarılı</span><span class="sxs-lookup"><span data-stu-id="77ff9-187">Success</span></span>         | <span data-ttu-id="77ff9-188">0</span><span class="sxs-lookup"><span data-stu-id="77ff9-188">0</span></span>     |
| <span data-ttu-id="77ff9-189">Hata</span><span class="sxs-lookup"><span data-stu-id="77ff9-189">Failure</span></span>         | <span data-ttu-id="77ff9-190">- 1</span><span class="sxs-lookup"><span data-stu-id="77ff9-190">- 1</span></span>   |

<span data-ttu-id="77ff9-191">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="77ff9-191">**Supported operators**: eq</span></span>

<span data-ttu-id="77ff9-192">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="77ff9-193">activityType</span><span class="sxs-lookup"><span data-stu-id="77ff9-193">activityType</span></span>
<span data-ttu-id="77ff9-194">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="77ff9-194">**Supported operators**: eq</span></span>

<span data-ttu-id="77ff9-195">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="77ff9-196">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-196">**Notes**:</span></span>

<span data-ttu-id="77ff9-197">büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="77ff9-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="77ff9-198">Etkinlik</span><span class="sxs-lookup"><span data-stu-id="77ff9-198">activity</span></span>
<span data-ttu-id="77ff9-199">**İşleçler desteklenen**: eq, içerir, startsWith</span><span class="sxs-lookup"><span data-stu-id="77ff9-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="77ff9-200">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="77ff9-201">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-201">**Notes**:</span></span>

<span data-ttu-id="77ff9-202">büyük küçük harfe duyarlı</span><span class="sxs-lookup"><span data-stu-id="77ff9-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="77ff9-203">Aktör/adı</span><span class="sxs-lookup"><span data-stu-id="77ff9-203">actor/name</span></span>
<span data-ttu-id="77ff9-204">**İşleçler desteklenen**: eq, içerir, startsWith</span><span class="sxs-lookup"><span data-stu-id="77ff9-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="77ff9-205">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="77ff9-206">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-206">**Notes**:</span></span>

<span data-ttu-id="77ff9-207">Büyük küçük harfe duyarsızdır</span><span class="sxs-lookup"><span data-stu-id="77ff9-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="77ff9-208">Aktör/objectID</span><span class="sxs-lookup"><span data-stu-id="77ff9-208">actor/objectId</span></span>
<span data-ttu-id="77ff9-209">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="77ff9-209">**Supported operators**: eq</span></span>

<span data-ttu-id="77ff9-210">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="77ff9-211">Hedef/adı</span><span class="sxs-lookup"><span data-stu-id="77ff9-211">target/name</span></span>
<span data-ttu-id="77ff9-212">**İşleçler desteklenen**: eq, içerir, startsWith</span><span class="sxs-lookup"><span data-stu-id="77ff9-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="77ff9-213">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="77ff9-214">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-214">**Notes**:</span></span>

<span data-ttu-id="77ff9-215">Büyük küçük harfe duyarsızdır</span><span class="sxs-lookup"><span data-stu-id="77ff9-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="77ff9-216">Hedef/upn</span><span class="sxs-lookup"><span data-stu-id="77ff9-216">target/upn</span></span>
<span data-ttu-id="77ff9-217">**İşleçler desteklenen**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="77ff9-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="77ff9-218">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="77ff9-219">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-219">**Notes**:</span></span>

* <span data-ttu-id="77ff9-220">Büyük küçük harfe duyarsızdır</span><span class="sxs-lookup"><span data-stu-id="77ff9-220">Case-insensitive</span></span>
* <span data-ttu-id="77ff9-221">Tam ad alanını Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity sorgulanırken eklemeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="77ff9-221">You need to add the full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="77ff9-222">Hedef/objectID</span><span class="sxs-lookup"><span data-stu-id="77ff9-222">target/objectId</span></span>
<span data-ttu-id="77ff9-223">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="77ff9-223">**Supported operators**: eq</span></span>

<span data-ttu-id="77ff9-224">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="77ff9-225">Aktör/upn</span><span class="sxs-lookup"><span data-stu-id="77ff9-225">actor/upn</span></span>
<span data-ttu-id="77ff9-226">**İşleçler desteklenen**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="77ff9-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="77ff9-227">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="77ff9-228">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="77ff9-228">**Notes**:</span></span>

* <span data-ttu-id="77ff9-229">Büyük küçük harfe duyarsızdır</span><span class="sxs-lookup"><span data-stu-id="77ff9-229">Case-insensitive</span></span> 
* <span data-ttu-id="77ff9-230">Tam ad alanını Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity sorgulanırken eklemeniz gerekir</span><span class="sxs-lookup"><span data-stu-id="77ff9-230">You need to add the full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="77ff9-231">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="77ff9-231">Next Steps</span></span>
* <span data-ttu-id="77ff9-232">Filtrelenmiş sistem faaliyetleri örneklerini görmek istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="77ff9-232">Do you want to see examples for filtered system activities?</span></span> <span data-ttu-id="77ff9-233">Kullanıma [Azure Active Directory denetim API'si örnekleri](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="77ff9-233">Check out the [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="77ff9-234">Azure AD raporlama API'si hakkında daha fazla bilgi istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="77ff9-234">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="77ff9-235">Bkz: [Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="77ff9-235">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

