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
ms.openlocfilehash: 52180b760046d273c5a75720df0a73532d0343ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-the-reporting-api"></a><span data-ttu-id="cb992-103">Raporlama API'si aracılığıyla Azure AD B2C kullanım raporlarında erişme</span><span class="sxs-lookup"><span data-stu-id="cb992-103">Accessing usage reports in Azure AD B2C via the reporting API</span></span>

<span data-ttu-id="cb992-104">Azure Active Directory B2C (Azure AD B2C) kullanıcı oturum açma ve Azure multi-Factor Authentication göre kimlik doğrulaması sağlar.</span><span class="sxs-lookup"><span data-stu-id="cb992-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="cb992-105">Kimlik doğrulaması uygulama ailenizin son kullanıcılar için kimlik sağlayıcıları sağlanır.</span><span class="sxs-lookup"><span data-stu-id="cb992-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="cb992-106">Kiracı, kaydettirmek için kullanılan sağlayıcıları ve kimlik doğrulama sayısını türüne göre kayıtlı kullanıcıların sayısını bildiğinizde gibi sorulara cevap verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb992-106">When you know the number of users registered in the tenant, the providers they used to register, and the number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="cb992-107">Kimlik sağlayıcısı (örneğin, bir Microsoft ya da LinkedIn hesabı) her tür kaç kullanıcının son 10 gün içinde kayıtlı?</span><span class="sxs-lookup"><span data-stu-id="cb992-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in the last 10 days?</span></span>
* <span data-ttu-id="cb992-108">Çok faktörlü kimlik doğrulaması kullanarak kaç kimlik doğrulamaları son bir ayda başarıyla tamamladınız mı?</span><span class="sxs-lookup"><span data-stu-id="cb992-108">How many authentications using Multi-Factor Authentication have completed successfully in the last month?</span></span>
* <span data-ttu-id="cb992-109">Kaç tane oturum bileşen tabanlı kimlik doğrulamaları bu ay tamamlandığını?</span><span class="sxs-lookup"><span data-stu-id="cb992-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="cb992-110">Gün başına?</span><span class="sxs-lookup"><span data-stu-id="cb992-110">Per day?</span></span> <span data-ttu-id="cb992-111">Uygulama başına?</span><span class="sxs-lookup"><span data-stu-id="cb992-111">Per application?</span></span>
* <span data-ttu-id="cb992-112">Azure AD B2C Kiracı etkinlik beklenen aylık maliyetini nasıl tahmin edebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="cb992-112">How can I estimate the expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="cb992-113">Bu makalede, kullanıcılar, Faturalanabilir oturum bileşen tabanlı kimlik doğrulamaları ve çok faktörlü kimlik doğrulamaları sayısına göre fatura etkinliğine bağlı raporları odaklanır.</span><span class="sxs-lookup"><span data-stu-id="cb992-113">This article focuses on reports tied to billing activity, which is based on the number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="cb992-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="cb992-114">Prerequisites</span></span>
<span data-ttu-id="cb992-115">Başlamadan önce bölümündeki adımları tamamlamanız gerekir [Azure AD API'leri raporlama erişmek için Önkoşullar](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="cb992-115">Before you get started, you need to complete the steps in [Prerequisites to access the Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="cb992-116">Bir uygulama oluşturmak, bir gizlilik elde ve erişim izni Azure AD B2C kiracınızın raporları hakkı.</span><span class="sxs-lookup"><span data-stu-id="cb992-116">Create an application, obtain a secret for it, and grant it access rights to your Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="cb992-117">*Komut dosyası bash* ve *Python betiği* örnekler da sağlanmıştır burada.</span><span class="sxs-lookup"><span data-stu-id="cb992-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="cb992-118">PowerShell betiği</span><span class="sxs-lookup"><span data-stu-id="cb992-118">PowerShell script</span></span>
<span data-ttu-id="cb992-119">Bu komut dosyasını kullanarak dört kullanım raporları oluşturulmasını gösterir `TimeStamp` parametre ve `ApplicationId` Filtresi.</span><span class="sxs-lookup"><span data-stu-id="cb992-119">This script demonstrates the creation of four usage reports by using the `TimeStamp` parameter and the `ApplicationId` filter.</span></span>

```powershell
# This script will require the Web Application and permissions setup in Azure Active Directory

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

    Write-host Data from the tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for the report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for the " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="cb992-120">Kullanım Raporu tanımları</span><span class="sxs-lookup"><span data-stu-id="cb992-120">Usage report definitions</span></span>
* <span data-ttu-id="cb992-121">**tenantUserCount**: Kiracı son 30 gün içinde gün başına kimlik sağlayıcısı türü tarafından kullanıcıların sayısı.</span><span class="sxs-lookup"><span data-stu-id="cb992-121">**tenantUserCount**: The number of users in the tenant by type of identity provider, per day in the last 30 days.</span></span> <span data-ttu-id="cb992-122">(İsteğe bağlı olarak, bir `TimeStamp` filtre geçerli tarih için belirtilen bir tarihten itibaren kullanıcı sayısına sağlar).</span><span class="sxs-lookup"><span data-stu-id="cb992-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date to the current date).</span></span> <span data-ttu-id="cb992-123">Rapor sağlar:</span><span class="sxs-lookup"><span data-stu-id="cb992-123">The report provides:</span></span>
  * <span data-ttu-id="cb992-124">**TotalUserCount**: tüm kullanıcı nesnelerinin sayısı.</span><span class="sxs-lookup"><span data-stu-id="cb992-124">**TotalUserCount**: The number of all user objects.</span></span>
  * <span data-ttu-id="cb992-125">**OtherUserCount**: Azure Active Directory Kullanıcıları (Azure AD B2C kullanıcılara değil) sayısı.</span><span class="sxs-lookup"><span data-stu-id="cb992-125">**OtherUserCount**: The number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="cb992-126">**LocalUserCount**: Azure AD B2C kullanıcı hesaplarının sayısı kimlik bilgileriyle Azure AD B2C kiracısı yerel oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="cb992-126">**LocalUserCount**: The number of Azure AD B2C user accounts created with credentials local to the Azure AD B2C tenant.</span></span>

* <span data-ttu-id="cb992-127">**AlternateIdUserCount**: Azure AD B2C kullanıcı sayısını kayıtlı olan dış kimlik sağlayıcısı (örneğin, Facebook, bir Microsoft hesabı veya başka bir Azure Active Directory Kiracı da denir bir `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="cb992-127">**AlternateIdUserCount**: The number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred to as an `OrgId`).</span></span>

* <span data-ttu-id="cb992-128">**b2cAuthenticationCountSummary**: Özet Faturalanabilir kimlik doğrulamaları gün ve kimlik doğrulama akışı türü tarafından son 30 gün boyunca günlük sayısı.</span><span class="sxs-lookup"><span data-stu-id="cb992-128">**b2cAuthenticationCountSummary**: Summary of the daily number of billable authentications over the last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="cb992-129">**b2cAuthenticationCount**: kimlik doğrulamaları bir süre içinde sayısı.</span><span class="sxs-lookup"><span data-stu-id="cb992-129">**b2cAuthenticationCount**: The number of authentications within a time period.</span></span> <span data-ttu-id="cb992-130">Son 30 gün varsayılandır.</span><span class="sxs-lookup"><span data-stu-id="cb992-130">The default is the last 30 days.</span></span>  <span data-ttu-id="cb992-131">(İsteğe bağlı: Başlangıç ve bitiş `TimeStamp` parametreleri tanımlayan belirli bir zaman dilimi.) Çıktı içerir `StartTimeStamp` (Bu Kiracı için etkinliğin en erken tarihi) ve `EndTimeStamp` (son güncelleştirme).</span><span class="sxs-lookup"><span data-stu-id="cb992-131">(Optional: The beginning and ending `TimeStamp` parameters define a specific time period.) The output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="cb992-132">**b2cMfaRequestCountSummary**: gün ve türüne (SMS veya sesli) göre çok faktörlü kimlik doğrulama günlük sayısını özeti.</span><span class="sxs-lookup"><span data-stu-id="cb992-132">**b2cMfaRequestCountSummary**: Summary of the daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="cb992-133">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="cb992-133">Limitations</span></span>
<span data-ttu-id="cb992-134">Kullanıcı sayısı verileri 48 için 24 saatte bir yenilenir.</span><span class="sxs-lookup"><span data-stu-id="cb992-134">User count data is refreshed every 24 to 48 hours.</span></span> <span data-ttu-id="cb992-135">Kimlik doğrulamaları günde birkaç kez güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cb992-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="cb992-136">Kullanırken `ApplicationId` filtre, bir boş rapor yanıt olabilir aşağıdaki koşullardan biri nedeniyle:</span><span class="sxs-lookup"><span data-stu-id="cb992-136">When using the `ApplicationId` filter, an empty report response can be due to one of following conditions:</span></span>
  * <span data-ttu-id="cb992-137">Uygulama Kimliği Kiracı içinde yok.</span><span class="sxs-lookup"><span data-stu-id="cb992-137">The application ID does not exist in the tenant.</span></span> <span data-ttu-id="cb992-138">Doğru olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="cb992-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="cb992-139">Uygulama kimliği var, ancak hiçbir veri raporlama döneminde bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="cb992-139">The application ID exists, but no data was found in the reporting period.</span></span> <span data-ttu-id="cb992-140">Tarih/saat parametrelerinizi inceleyin.</span><span class="sxs-lookup"><span data-stu-id="cb992-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="cb992-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cb992-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="cb992-142">Azure AD için aylık faturanızı tahmin eder</span><span class="sxs-lookup"><span data-stu-id="cb992-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="cb992-143">İle birleştirildiğinde [en güncel Azure AD B2C kullanılabilir fiyatlandırma](https://azure.microsoft.com/pricing/details/active-directory-b2c/), günlük, haftalık ve aylık Azure tüketim tahmin edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cb992-143">When combined with [the most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="cb992-144">Genel maliyeti etkileyebilecek Kiracı davranış değişiklikleri planlarken tahmini özellikle yararlı olur.</span><span class="sxs-lookup"><span data-stu-id="cb992-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="cb992-145">Gerçek maliyetlerini gözden geçirebilirsiniz, [Azure aboneliğine bağlı](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="cb992-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="cb992-146">Diğer çıkış biçimleri için seçenekleri</span><span class="sxs-lookup"><span data-stu-id="cb992-146">Options for other output formats</span></span>
<span data-ttu-id="cb992-147">Aşağıdaki kod örnekleri JSON, bir ad değeri listesi ve XML Çıkış göndermeyi gösterir:</span><span class="sxs-lookup"><span data-stu-id="cb992-147">The following code shows examples of sending output to JSON, a name value list, and XML:</span></span>
```powershell
# to output to JSON use following line in the PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# to output the content to a name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# to output the content in XML use the following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
