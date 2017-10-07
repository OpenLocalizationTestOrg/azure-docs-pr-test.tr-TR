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
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a>Azure AD B2C kullanım raporlarında hello raporlama API'si aracılığıyla erişme

Azure Active Directory B2C (Azure AD B2C) kullanıcı oturum açma ve Azure multi-Factor Authentication göre kimlik doğrulaması sağlar. Kimlik doğrulaması uygulama ailenizin son kullanıcılar için kimlik sağlayıcıları sağlanır. Merhaba sayısı, kullanıcı türüne göre hello Kiracı, tooregister ve kimlik doğrulama hello sayısını kullanılan hello sağlayıcıları kayıtlı bildiğinizde gibi sorulara cevap verebilirsiniz.
* Kimlik sağlayıcısı (örneğin, bir Microsoft ya da LinkedIn hesabı) her tür kaç kullanıcı hello son 10 gün kaydettiniz?
* Çok faktörlü kimlik doğrulaması kullanarak kaç kimlik doğrulamaları hello geçen ay başarıyla tamamladınız mı?
* Kaç tane oturum bileşen tabanlı kimlik doğrulamaları bu ay tamamlandığını? Gün başına? Uygulama başına?
* Azure AD B2C Kiracı etkinlik aylık maliyeti hello beklenen nasıl tahmin edebilirsiniz?

Bu makalede, kullanıcılar, Faturalanabilir oturum bileşen tabanlı kimlik doğrulamaları ve çok faktörlü kimlik doğrulamaları hello numarasına göre bağlı raporları toobilling etkinlik odaklanır.


## <a name="prerequisites"></a>Ön koşullar
Başlamadan önce toocomplete hello adımlarda gereksinim [Önkoşullar tooaccess hello Azure AD raporlama API'leri](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/). Bir uygulama oluşturmak, bir gizlilik elde ve tooyour Azure AD B2C kiracının raporları, erişim hakları. *Komut dosyası bash* ve *Python betiği* örnekler da sağlanmıştır burada. 

## <a name="powershell-script"></a>PowerShell betiği
Bu komut dosyası hello kullanarak dört kullanım raporları hello oluşturulmasını gösterir `TimeStamp` parametre ve hello `ApplicationId` Filtresi.

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


## <a name="usage-report-definitions"></a>Kullanım Raporu tanımları
* **tenantUserCount**: son 30 gün hello Kiracı hello günde kimlik sağlayıcısı türü tarafından kullanıcıların sayısı hello. (İsteğe bağlı olarak, bir `TimeStamp` filtre kullanıcı sayısına geçerli tarih belirtilen tarih toohello gelen sağlar). Merhaba rapor sağlar:
  * **TotalUserCount**: Merhaba tüm kullanıcı nesnelerinin sayısı.
  * **OtherUserCount**: hello Azure Active Directory Kullanıcıları (Azure AD B2C kullanıcılara değil) sayısı.
  * **LocalUserCount**: Merhaba kimlik bilgilerini yerel toohello Azure AD B2C kiracısı ile oluşturulan Azure AD B2C kullanıcı hesaplarının sayısı.

* **AlternateIdUserCount**: hello sayısı, Azure AD B2C kullanıcı kayıtlı olan dış kimlik sağlayıcısı (örneğin, Facebook, bir Microsoft hesabı veya başka bir Azure Active Directory Kiracı da tooas adlandırılan bir `OrgId`).

* **b2cAuthenticationCountSummary**: hello günlük Faturalanabilir kimlik doğrulamalarının gün ve kimlik doğrulama akışı türü tarafından son 30 gün hello üzerinden sayısını özeti.

* **b2cAuthenticationCount**: bir süre içinde kimlik doğrulama sayısını hello. Merhaba hello son 30 gün varsayılandır.  (İsteğe bağlı: Başlangıç ve bitiş hello `TimeStamp` parametreleri tanımlayan bir belirli bir zaman süresi.) hello çıktı içerir `StartTimeStamp` (Bu Kiracı için etkinliğin en erken tarihi) ve `EndTimeStamp` (son güncelleştirme).

* **b2cMfaRequestCountSummary**: hello günlük gün ve (SMS veya sesli) türüne göre çok faktörlü kimlik doğrulama sayısını özeti.


## <a name="limitations"></a>Sınırlamalar
Kullanıcı sayısı verileri 24 too48 saatte bir yenilenir. Kimlik doğrulamaları günde birkaç kez güncelleştirilir. Merhaba kullanırken `ApplicationId` filtre, bir boş rapor yanıt olabilir son tooone aşağıdaki koşullardan biri:
  * Merhaba uygulama kimliği hello Kiracı içinde yok. Doğru olduğundan emin olun.
  * Merhaba uygulama kimliği var, ancak hiçbir veri raporlama dönemi hello bulunamadı. Tarih/saat parametrelerinizi inceleyin.


## <a name="next-steps"></a>Sonraki adımlar
### <a name="monthly-bill-estimates-for-azure-ad"></a>Azure AD için aylık faturanızı tahmin eder
İle birleştirildiğinde [en güncel Azure AD B2C kullanılabilir fiyatlandırma hello](https://azure.microsoft.com/pricing/details/active-directory-b2c/), günlük, haftalık ve aylık Azure tüketim tahmin edebilirsiniz.  Genel maliyeti etkileyebilecek Kiracı davranış değişiklikleri planlarken tahmini özellikle yararlı olur. Gerçek maliyetlerini gözden geçirebilirsiniz, [Azure aboneliğine bağlı](active-directory-b2c-how-to-enable-billing.md).

### <a name="options-for-other-output-formats"></a>Diğer çıkış biçimleri için seçenekleri
Merhaba aşağıdaki kodu çıkış tooJSON, bir ad değeri listesi ve XML gönderme örnekler gösterilmektedir:
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
