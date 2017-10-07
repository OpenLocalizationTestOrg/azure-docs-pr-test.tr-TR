---
title: "aaaAzure Active Directory oturum açma etkinliği raporu API Başvurusu | Microsoft Docs"
description: "Hello Azure Active Directory oturum açma etkinliği raporu API Başvurusu"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="5384b-103">Azure Active Directory oturum açma etkinliği raporu API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="5384b-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="5384b-104">Bu konu hello Azure Active Directory ilgili konulara koleksiyonu parçasıdır raporlama API'si.</span><span class="sxs-lookup"><span data-stu-id="5384b-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="5384b-105">Azure AD raporlama kodu veya ilgili araçları kullanarak tooaccess oturum açma etkinliği raporu veri sağlayan bir API ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="5384b-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="5384b-106">Bu konunun Hello kapsamı olan tooprovide hello hakkında başvuru bilgileri sizinle **oturum açma etkinliği raporu API işleminde**.</span><span class="sxs-lookup"><span data-stu-id="5384b-106">hello scope of this topic is tooprovide you with reference information about hello **sign-in activity report API**.</span></span>

<span data-ttu-id="5384b-107">Bkz.:</span><span class="sxs-lookup"><span data-stu-id="5384b-107">See:</span></span>

* <span data-ttu-id="5384b-108">[Oturum açma etkinliklerini](active-directory-reporting-azure-portal.md#activity-reports) daha fazla kavramsal bilgi için</span><span class="sxs-lookup"><span data-stu-id="5384b-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="5384b-109">[Hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) hello raporlama API'si hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="5384b-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="who-can-access-hello-api-data"></a><span data-ttu-id="5384b-110">Merhaba API veri erişebilecek mi?</span><span class="sxs-lookup"><span data-stu-id="5384b-110">Who can access hello API data?</span></span>
* <span data-ttu-id="5384b-111">Kullanıcı ve hizmet asıl adı hello Güvenlik Yöneticisi veya güvenlik okuyucu rolü</span><span class="sxs-lookup"><span data-stu-id="5384b-111">Users and Service Principals in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="5384b-112">Genel Yöneticiler</span><span class="sxs-lookup"><span data-stu-id="5384b-112">Global Admins</span></span>
* <span data-ttu-id="5384b-113">Yetkilendirme tooaccess hello API sahip herhangi bir uygulama (app yetkilendirme olabilir Kurulum genel yöneticinin iznine dayanılarak yalnızca)</span><span class="sxs-lookup"><span data-stu-id="5384b-113">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="5384b-114">bir uygulama tooaccess API'leri gibi güvenlik oturum açma olayları, PowerShell tooadd hello uygulamaları hizmet sorumlusu hello güvenlik okuyucu rolüne aşağıdaki kullanım hello tooconfigure erişim</span><span class="sxs-lookup"><span data-stu-id="5384b-114">tooconfigure access for an application tooaccess security APIs such as signin events, use hello following PowerShell tooadd hello applications Service Principal into hello Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="5384b-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5384b-115">Prerequisites</span></span>
<span data-ttu-id="5384b-116">Bu rapor aracılığıyla tooaccess raporlama API Merhaba, sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="5384b-116">tooaccess this report through hello reporting API, you must have:</span></span>

* <span data-ttu-id="5384b-117">Bir [Azure Active Directory Premium P1 veya P2 edition](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="5384b-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="5384b-118">Tamamlanan hello [Önkoşullar tooaccess hello Azure AD raporlama API'si](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="5384b-118">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="5384b-119">Merhaba API'sine erişim</span><span class="sxs-lookup"><span data-stu-id="5384b-119">Accessing hello API</span></span>
<span data-ttu-id="5384b-120">Bu API hello erişebilirsiniz [Graph Explorer'a](https://graphexplorer2.cloudapp.net) veya program aracılığıyla, örneğin, PowerShell kullanarak.</span><span class="sxs-lookup"><span data-stu-id="5384b-120">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="5384b-121">Sırayla PowerShell toocorrectly yorumlamak için AAD grafik REST çağrılarında kullanılan hello OData filtresi sözdizimi hello backtick kullanmanız gerekir (diğer adıyla: Vurgu) çok "kaçış karakteri" Merhaba $ karakteri.</span><span class="sxs-lookup"><span data-stu-id="5384b-121">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="5384b-122">Merhaba backtick karakter görür [PowerShell'in kaçış karakteri](https://technet.microsoft.com/library/hh847755.aspx)PowerShell toodo hello $ karakteri değişmez değer yorumu izin verme ve PowerShell değişken adı olarak kafa karıştırıcı kaçının (IE: $filter).</span><span class="sxs-lookup"><span data-stu-id="5384b-122">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="5384b-123">Bu konunun Hello odak Graph Explorer'a hello üzerinde noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="5384b-123">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="5384b-124">Bu PowerShell örnek için bkz [PowerShell Betiği](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="5384b-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="5384b-125">API uç noktası</span><span class="sxs-lookup"><span data-stu-id="5384b-125">API Endpoint</span></span>
<span data-ttu-id="5384b-126">Bu API taban URI aşağıdaki hello kullanarak erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5384b-126">You can access this API using hello following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="5384b-127">Veri hacmi toohello, bu API bir milyon kayıtları döndürülen bir sınıra sahiptir.</span><span class="sxs-lookup"><span data-stu-id="5384b-127">Due toohello volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="5384b-128">Bu çağrı hello verileri toplu olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="5384b-128">This call returns hello data in batches.</span></span> <span data-ttu-id="5384b-129">Her toplu işlem en fazla 1000 kaydı var.</span><span class="sxs-lookup"><span data-stu-id="5384b-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="5384b-130">tooget hello sonraki toplu kayıt, kullanım hello sonraki bağlantı.</span><span class="sxs-lookup"><span data-stu-id="5384b-130">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="5384b-131">Merhaba alma [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) hello ilk döndürülen kayıt kümesi bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5384b-131">Get hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from hello first set of returned records.</span></span> <span data-ttu-id="5384b-132">Merhaba Atla belirteci hello hello sonuç kümesinin sonunda olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5384b-132">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="5384b-133">Desteklenen filtreler</span><span class="sxs-lookup"><span data-stu-id="5384b-133">Supported filters</span></span>
<span data-ttu-id="5384b-134">Bir API tarafından döndürülen kayıt sayısını hello daraltabilirsiniz bir filtre formda çağırın.</span><span class="sxs-lookup"><span data-stu-id="5384b-134">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="5384b-135">Oturum açma için API ilgili veriler, filtreleri aşağıdaki hello desteklenir:</span><span class="sxs-lookup"><span data-stu-id="5384b-135">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="5384b-136">**$top =\<döndürülen kayıt toobe sayısı\>**  -toolimit hello döndürülen kayıt sayısı.</span><span class="sxs-lookup"><span data-stu-id="5384b-136">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="5384b-137">Bu pahalı bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="5384b-137">This is an expensive operation.</span></span> <span data-ttu-id="5384b-138">Nesnelerin tooreturn binlerce istiyorsanız bu filtre kullanmamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5384b-138">You should not use this filter if you want tooreturn thousands of objects.</span></span>  
* <span data-ttu-id="5384b-139">**$filter =\<filtre ifadesi\>**  -desteklenen filtre alanlarının önem verdiğiniz kayıtların hello türünü hello temelinde toospecify</span><span class="sxs-lookup"><span data-stu-id="5384b-139">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="5384b-140">Desteklenen filtre alanları ve işleçleri</span><span class="sxs-lookup"><span data-stu-id="5384b-140">Supported filter fields and operators</span></span>
<span data-ttu-id="5384b-141">İlgilendiğiniz kayıtları toospecify hello türü, bir veya filtre alanları aşağıdaki hello bir birleşimini içerebilir bir filtre ifadesi oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5384b-141">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="5384b-142">[signinDateTime](#signindatetime) -bir tarih veya tarih aralığı tanımlar</span><span class="sxs-lookup"><span data-stu-id="5384b-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="5384b-143">[UserId](#userid) -belirli kullanıcı tabanlı hello kullanıcının kimliği tanımlar</span><span class="sxs-lookup"><span data-stu-id="5384b-143">[userId](#userid) - defines a specific user based hello user's ID.</span></span>
* <span data-ttu-id="5384b-144">[userPrincipalName](#userprincipalname) -belirli kullanıcı tabanlı hello kullanıcının kullanıcı asıl adı (UPN) tanımlar</span><span class="sxs-lookup"><span data-stu-id="5384b-144">[userPrincipalName](#userprincipalname) - defines a specific user based hello user's user principal name (UPN)</span></span>
* <span data-ttu-id="5384b-145">[AppID](#appid) -göre belirli uygulama hello uygulamanın Kimliğini tanımlar</span><span class="sxs-lookup"><span data-stu-id="5384b-145">[appId](#appid) - defines a specific app based hello app's ID</span></span>
* <span data-ttu-id="5384b-146">[appDisplayName](#appdisplayname) -göre belirli uygulama hello uygulamanın görünen adı tanımlar</span><span class="sxs-lookup"><span data-stu-id="5384b-146">[appDisplayName](#appdisplayname) - defines a specific app based hello app's display name</span></span>
* <span data-ttu-id="5384b-147">[loginStatus](#loginStatus) -hello oturumları hello durumunu tanımlar (başarı / hata)</span><span class="sxs-lookup"><span data-stu-id="5384b-147">[loginStatus](#loginStatus) - defines hello status of hello logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="5384b-148">Grafik Gezgini'ni kullanırken, hello toouse hello filtre alanlarınızı durumdur her harfi için doğru gerekir.</span><span class="sxs-lookup"><span data-stu-id="5384b-148">When using Graph Explorer, you hello need toouse hello correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="5384b-149">toonarrow döndürülen veriler hello hello kapsamını aşağı desteklenen hello filtreleri ve filtre alanları birleşimlerini oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5384b-149">toonarrow down hello scope of hello returned data, you can build combinations of hello supported filters and filter fields.</span></span> <span data-ttu-id="5384b-150">Örneğin, hello aşağıdaki ifadeyi hello 1 Temmuz 2016 Temmuz 6 2016 arasındaki üst 10 kayıtları döndürür:</span><span class="sxs-lookup"><span data-stu-id="5384b-150">For example, hello following statement returns hello top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="5384b-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="5384b-151">signinDateTime</span></span>
<span data-ttu-id="5384b-152">**İşleçler desteklenen**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="5384b-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="5384b-153">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5384b-153">**Example**:</span></span>

<span data-ttu-id="5384b-154">Belirli bir tarih kullanma</span><span class="sxs-lookup"><span data-stu-id="5384b-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="5384b-155">Bir tarih aralığı kullanma</span><span class="sxs-lookup"><span data-stu-id="5384b-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="5384b-156">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="5384b-156">**Notes**:</span></span>

<span data-ttu-id="5384b-157">Merhaba datetime parametresi hello UTC biçiminde olmalıdır</span><span class="sxs-lookup"><span data-stu-id="5384b-157">hello datetime parameter should be in hello UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="5384b-158">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="5384b-158">userId</span></span>
<span data-ttu-id="5384b-159">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="5384b-159">**Supported operators**: eq</span></span>

<span data-ttu-id="5384b-160">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5384b-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="5384b-161">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="5384b-161">**Notes**:</span></span>

<span data-ttu-id="5384b-162">UserId Hello değeri bir dize değeridir</span><span class="sxs-lookup"><span data-stu-id="5384b-162">hello value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="5384b-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="5384b-163">userPrincipalName</span></span>
<span data-ttu-id="5384b-164">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="5384b-164">**Supported operators**: eq</span></span>

<span data-ttu-id="5384b-165">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5384b-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="5384b-166">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="5384b-166">**Notes**:</span></span>

<span data-ttu-id="5384b-167">userPrincipalName Hello değeri bir dize değeridir</span><span class="sxs-lookup"><span data-stu-id="5384b-167">hello value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="5384b-168">AppID</span><span class="sxs-lookup"><span data-stu-id="5384b-168">appId</span></span>
<span data-ttu-id="5384b-169">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="5384b-169">**Supported operators**: eq</span></span>

<span data-ttu-id="5384b-170">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5384b-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="5384b-171">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="5384b-171">**Notes**:</span></span>

<span data-ttu-id="5384b-172">AppID Hello değeri bir dize değeridir</span><span class="sxs-lookup"><span data-stu-id="5384b-172">hello value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="5384b-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="5384b-173">appDisplayName</span></span>
<span data-ttu-id="5384b-174">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="5384b-174">**Supported operators**: eq</span></span>

<span data-ttu-id="5384b-175">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5384b-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="5384b-176">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="5384b-176">**Notes**:</span></span>

<span data-ttu-id="5384b-177">appDisplayName Hello değeri bir dize değeridir</span><span class="sxs-lookup"><span data-stu-id="5384b-177">hello value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="5384b-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="5384b-178">loginStatus</span></span>
<span data-ttu-id="5384b-179">**İşleçler desteklenen**: eq</span><span class="sxs-lookup"><span data-stu-id="5384b-179">**Supported operators**: eq</span></span>

<span data-ttu-id="5384b-180">**Örnek**:</span><span class="sxs-lookup"><span data-stu-id="5384b-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="5384b-181">**Notlar**:</span><span class="sxs-lookup"><span data-stu-id="5384b-181">**Notes**:</span></span>

<span data-ttu-id="5384b-182">Merhaba loginStatus için iki seçenek vardır: 0 - başarılı, 1 - hata</span><span class="sxs-lookup"><span data-stu-id="5384b-182">There are two options for hello loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="5384b-183">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5384b-183">Next steps</span></span>
* <span data-ttu-id="5384b-184">Oturum açma filtrelenmiş etkinlikler için toosee örnekler istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="5384b-184">Do you want toosee examples for filtered sign-in activities?</span></span> <span data-ttu-id="5384b-185">Merhaba denetleyin [Azure Active Directory oturum açma etkinliği raporu API örnekleri](active-directory-reporting-api-sign-in-activity-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5384b-185">Check out hello [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="5384b-186">Tooknow hello Azure AD raporlama API'si hakkında daha fazla istiyor musunuz?</span><span class="sxs-lookup"><span data-stu-id="5384b-186">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="5384b-187">Bkz: [hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5384b-187">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

