---
title: "aaaAzure Active Directory oturum açma etkinliği raporu API örnekleri | Microsoft Docs"
description: "Tooget hello Azure Active Directory raporlama API'si ile çalışmaya nasıl"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: c41c1489-726b-4d3f-81d6-83beb932df9c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d4fbbea95fe0b52828673b997681ae37481e21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a>Azure Active Directory oturum açma etkinliği raporu API örnekleri
Bu konu hello Azure Active Directory ilgili konulara koleksiyonu parçasıdır raporlama API'si.  
Azure AD raporlama kodu veya ilgili araçları kullanarak tooaccess oturum açma etkinliği veri sağlayan bir API ile sağlar.  
Merhaba bu konunun kapsamı olan, örnek kod Merhaba tooprovide **etkinlik API oturum aç**.

Bkz.:

* [Denetim günlükleri](active-directory-reporting-azure-portal.md#activity-reports) daha fazla kavramsal bilgi için
* [Hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) hello raporlama API'si hakkında daha fazla bilgi.


## <a name="prerequisites"></a>Ön koşullar
Bu konudaki hello örnekleri kullanabilmeniz için önce toocomplete hello gerekir [Önkoşullar tooaccess hello Azure AD raporlama API'si](active-directory-reporting-api-prerequisites.md).  

## <a name="powershell-script"></a>PowerShell betiği
    # This script will require hello Web Application and permissions setup in Azure Active Directory
    $ClientID       = "<clientId>"             # Should be a ~35 character string insert your info here
    $ClientSecret   = "<clientSecret>"         # Should be a ~44 character string insert your info here
    $loginURL       = "https://login.microsoftonline.com/"
    $tenantdomain   = "<tenantDomain>"
    $ daterange            # For example, contoso.onmicrosoft.com

    $7daysago = "{0:s}" -f (get-date).AddDays(-7) + "Z"
    # or, AddMinutes(-5)

    Write-Output $7daysago

    # Get an Oauth 2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}

    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    if ($oauth.access_token -ne $null) {
    $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    $url = "https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&`$filter=signinDateTime ge $7daysago"

    $i=0

    Do{
        Write-Output "Fetching data using Uri: $url"
        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
        Write-Output "Save hello output tooa file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-hello-script"></a>Merhaba komut dosyası yürütme
Sonra hello betik düzenlenmesini tamamlamayı, çalıştırın ve bu hello hello denetim günlüklerini rapor verileri döndürülen beklenen doğrulayın.

Merhaba betik çıkış raporundan hello oturum açma JSON biçiminde döndürür. Ayrıca oluşturur bir `SigninActivities.json` hello ile aynı dosyayı çıktı. Diğer raporlar ve yorum ihtiyacınız olmayan hello Çıkış biçimleri çıkışı hello betik tooreturn veriler değiştirerek deneyebilirsiniz.

## <a name="next-steps"></a>Sonraki Adımlar
* Bu konudaki toocustomize hello örnekleri ister misiniz? Merhaba denetleyin [Azure Active Directory oturum açma etkinliği API Başvurusu](active-directory-reporting-api-sign-in-activity-reference.md). 
* Toosee kullanmanın eksiksiz bir genel görünüm istiyorsanız, Azure Active Directory raporlama API'si Merhaba, bkz: [hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).
* Merhaba toofind Azure Active Directory raporlama hakkında daha fazla bilgi isterseniz bkz [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).  

