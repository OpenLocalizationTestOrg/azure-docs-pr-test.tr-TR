---
title: "Azure Active Directory B2C: Kullanım raporlama API örnekleri ve tanımları | Microsoft Docs"
description: "Kılavuzu ve kullanıcıları, kimlik doğrulamaları ve çok faktörlü kimlik doğrulamaları Azure AD B2C kiracısı üzerinde raporları almayı örnekleri"
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: f01f0d1d12464e38f892f1fdd5c7408a3b4cd1aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a><span data-ttu-id="d8773-103">Azure AD B2C kullanım raporlarında hello raporlama API'si aracılığıyla erişme</span><span class="sxs-lookup"><span data-stu-id="d8773-103">Accessing usage reports in Azure AD B2C via hello reporting API</span></span>

<span data-ttu-id="d8773-104">Azure Active Directory B2C (Azure AD B2C) kullanıcı oturum açma ve Azure multi-Factor Authentication göre kimlik doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="d8773-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="d8773-105">Kimlik doğrulaması uygulama ailenizin son kullanıcılar için kimlik sağlayıcıları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="d8773-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="d8773-106">Merhaba sayısı, kullanıcı türüne göre hello Kiracı, tooregister ve kimlik doğrulama hello sayısını kullanılan hello sağlayıcıları kayıtlı bildiğinizde gibi sorulara cevap verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8773-106">When you know hello number of users registered in hello tenant, hello providers they used tooregister, and hello number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="d8773-107">Kimlik sağlayıcısı (örneğin, bir Microsoft ya da LinkedIn hesabı) her tür kaç kullanıcı hello son 10 gün kaydettiniz?</span><span class="sxs-lookup"><span data-stu-id="d8773-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in hello last 10 days?</span></span>
* <span data-ttu-id="d8773-108">Çok faktörlü kimlik doğrulaması kullanarak kaç kimlik doğrulamaları hello geçen ay başarıyla tamamladınız mı?</span><span class="sxs-lookup"><span data-stu-id="d8773-108">How many authentications using Multi-Factor Authentication have completed successfully in hello last month?</span></span>
* <span data-ttu-id="d8773-109">Kaç tane oturum bileşen tabanlı kimlik doğrulamaları bu ay tamamlandığını?</span><span class="sxs-lookup"><span data-stu-id="d8773-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="d8773-110">Gün başına?</span><span class="sxs-lookup"><span data-stu-id="d8773-110">Per day?</span></span> <span data-ttu-id="d8773-111">Uygulama başına?</span><span class="sxs-lookup"><span data-stu-id="d8773-111">Per application?</span></span>
* <span data-ttu-id="d8773-112">Azure AD B2C Kiracı etkinlik aylık maliyeti hello beklenen nasıl tahmin edebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="d8773-112">How can I estimate hello expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="d8773-113">Bu makalede, kullanıcılar, Faturalanabilir oturum bileşen tabanlı kimlik doğrulamaları ve çok faktörlü kimlik doğrulamaları hello numarasına göre bağlı raporları toobilling etkinlik odaklanır.</span><span class="sxs-lookup"><span data-stu-id="d8773-113">This article focuses on reports tied toobilling activity, which is based on hello number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d8773-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d8773-114">Prerequisites</span></span>
<span data-ttu-id="d8773-115">Başlamadan önce toocomplete hello adımlarda gereksinim [Önkoşullar tooaccess hello Azure AD raporlama API'leri](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="d8773-115">Before you get started, you need toocomplete hello steps in [Prerequisites tooaccess hello Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="d8773-116">Bir uygulama oluşturmak, bir gizlilik elde ve tooyour Azure AD B2C kiracının raporları, erişim hakları.</span><span class="sxs-lookup"><span data-stu-id="d8773-116">Create an application, obtain a secret for it, and grant it access rights tooyour Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="d8773-117">*Komut dosyası bash* ve *Python betiği* örnekler da sağlanmıştır burada.</span><span class="sxs-lookup"><span data-stu-id="d8773-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="d8773-118">PowerShell betiği</span><span class="sxs-lookup"><span data-stu-id="d8773-118">PowerShell script</span></span>
<span data-ttu-id="d8773-119">Bu komut dosyası hello kullanarak dört kullanım raporları hello oluşturulmasını gösterir `TimeStamp` parametre ve hello `ApplicationId` Filtresi.</span><span class="sxs-lookup"><span data-stu-id="d8773-119">This script demonstrates hello creation of four usage reports by using hello `TimeStamp` parameter and hello `ApplicationId` filter.</span></span>

```powershell
# This script will require hello Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from hello tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for hello report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for hello " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="d8773-120">Kullanım Raporu tanımları</span><span class="sxs-lookup"><span data-stu-id="d8773-120">Usage report definitions</span></span>
* <span data-ttu-id="d8773-121">**tenantUserCount**: son 30 gün hello Kiracı hello günde kimlik sağlayıcısı türü tarafından kullanıcıların sayısı hello.</span><span class="sxs-lookup"><span data-stu-id="d8773-121">**tenantUserCount**: hello number of users in hello tenant by type of identity provider, per day in hello last 30 days.</span></span> <span data-ttu-id="d8773-122">(İsteğe bağlı olarak, bir `TimeStamp` filtre kullanıcı sayısına geçerli tarih belirtilen tarih toohello gelen sağlar).</span><span class="sxs-lookup"><span data-stu-id="d8773-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date toohello current date).</span></span> <span data-ttu-id="d8773-123">Merhaba rapor sağlar:</span><span class="sxs-lookup"><span data-stu-id="d8773-123">hello report provides:</span></span>
  * <span data-ttu-id="d8773-124">**TotalUserCount**: Merhaba tüm kullanıcı nesnelerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="d8773-124">**TotalUserCount**: hello number of all user objects.</span></span>
  * <span data-ttu-id="d8773-125">**OtherUserCount**: hello Azure Active Directory Kullanıcıları (Azure AD B2C kullanıcılara değil) sayısı.</span><span class="sxs-lookup"><span data-stu-id="d8773-125">**OtherUserCount**: hello number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="d8773-126">**LocalUserCount**: Merhaba kimlik bilgilerini yerel toohello Azure AD B2C kiracısı ile oluşturulan Azure AD B2C kullanıcı hesaplarının sayısı.</span><span class="sxs-lookup"><span data-stu-id="d8773-126">**LocalUserCount**: hello number of Azure AD B2C user accounts created with credentials local toohello Azure AD B2C tenant.</span></span>

* <span data-ttu-id="d8773-127">**AlternateIdUserCount**: hello sayısı, Azure AD B2C kullanıcı kayıtlı olan dış kimlik sağlayıcısı (örneğin, Facebook, bir Microsoft hesabı veya başka bir Azure Active Directory Kiracı da tooas adlandırılan bir `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="d8773-127">**AlternateIdUserCount**: hello number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred tooas an `OrgId`).</span></span>

* <span data-ttu-id="d8773-128">**b2cAuthenticationCountSummary**: hello günlük Faturalanabilir kimlik doğrulamalarının gün ve kimlik doğrulama akışı türü tarafından son 30 gün hello üzerinden sayısını özeti.</span><span class="sxs-lookup"><span data-stu-id="d8773-128">**b2cAuthenticationCountSummary**: Summary of hello daily number of billable authentications over hello last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="d8773-129">**b2cAuthenticationCount**: bir süre içinde kimlik doğrulama sayısını hello.</span><span class="sxs-lookup"><span data-stu-id="d8773-129">**b2cAuthenticationCount**: hello number of authentications within a time period.</span></span> <span data-ttu-id="d8773-130">Merhaba hello son 30 gün varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="d8773-130">hello default is hello last 30 days.</span></span>  <span data-ttu-id="d8773-131">(İsteğe bağlı: Başlangıç ve bitiş hello `TimeStamp` parametreleri tanımlayan bir belirli bir zaman süresi.) hello çıktı içerir `StartTimeStamp` (Bu Kiracı için etkinliğin en erken tarihi) ve `EndTimeStamp` (son güncelleştirme).</span><span class="sxs-lookup"><span data-stu-id="d8773-131">(Optional: hello beginning and ending `TimeStamp` parameters define a specific time period.) hello output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="d8773-132">**b2cMfaRequestCountSummary**: hello günlük gün ve (SMS veya sesli) türüne göre çok faktörlü kimlik doğrulama sayısını özeti.</span><span class="sxs-lookup"><span data-stu-id="d8773-132">**b2cMfaRequestCountSummary**: Summary of hello daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="d8773-133">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="d8773-133">Limitations</span></span>
<span data-ttu-id="d8773-134">Kullanıcı sayısı verileri 24 too48 saatte bir yenilenir.</span><span class="sxs-lookup"><span data-stu-id="d8773-134">User count data is refreshed every 24 too48 hours.</span></span> <span data-ttu-id="d8773-135">Kimlik doğrulamaları günde birkaç kez güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d8773-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="d8773-136">Merhaba kullanırken `ApplicationId` filtre, bir boş rapor yanıt olabilir son tooone aşağıdaki koşullardan biri:</span><span class="sxs-lookup"><span data-stu-id="d8773-136">When using hello `ApplicationId` filter, an empty report response can be due tooone of following conditions:</span></span>
  * <span data-ttu-id="d8773-137">Merhaba uygulama kimliği hello Kiracı içinde yok.</span><span class="sxs-lookup"><span data-stu-id="d8773-137">hello application ID does not exist in hello tenant.</span></span> <span data-ttu-id="d8773-138">Doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="d8773-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="d8773-139">Merhaba uygulama kimliği var, ancak hiçbir veri raporlama dönemi hello bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="d8773-139">hello application ID exists, but no data was found in hello reporting period.</span></span> <span data-ttu-id="d8773-140">Tarih/saat parametrelerinizi inceleyin.</span><span class="sxs-lookup"><span data-stu-id="d8773-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d8773-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d8773-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="d8773-142">Azure AD için aylık faturanızı tahmin eder</span><span class="sxs-lookup"><span data-stu-id="d8773-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="d8773-143">İle birleştirildiğinde [en güncel Azure AD B2C kullanılabilir fiyatlandırma hello](https://azure.microsoft.com/pricing/details/active-directory-b2c/), günlük, haftalık ve aylık Azure tüketim tahmin edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8773-143">When combined with [hello most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="d8773-144">Genel maliyeti etkileyebilecek Kiracı davranış değişiklikleri planlarken tahmini özellikle yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="d8773-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="d8773-145">Gerçek maliyetlerini gözden geçirebilirsiniz, [Azure aboneliğine bağlı](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="d8773-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="d8773-146">Diğer çıkış biçimleri için seçenekleri</span><span class="sxs-lookup"><span data-stu-id="d8773-146">Options for other output formats</span></span>
<span data-ttu-id="d8773-147">Merhaba aşağıdaki kodu çıkış tooJSON, bir ad değeri listesi ve XML gönderme örnekler gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d8773-147">hello following code shows examples of sending output tooJSON, a name value list, and XML:</span></span>
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
