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
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="8a6fb-103">Azure Active Directory oturum açma etkinliği raporu API örnekleri</span><span class="sxs-lookup"><span data-stu-id="8a6fb-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="8a6fb-104">Bu konu hello Azure Active Directory ilgili konulara koleksiyonu parçasıdır raporlama API'si.</span><span class="sxs-lookup"><span data-stu-id="8a6fb-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="8a6fb-105">Azure AD raporlama kodu veya ilgili araçları kullanarak tooaccess oturum açma etkinliği veri sağlayan bir API ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="8a6fb-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="8a6fb-106">Merhaba bu konunun kapsamı olan, örnek kod Merhaba tooprovide **etkinlik API oturum aç**.</span><span class="sxs-lookup"><span data-stu-id="8a6fb-106">hello scope of this topic is tooprovide you with sample code for hello **sign-in activity API**.</span></span>

<span data-ttu-id="8a6fb-107">Bkz.:</span><span class="sxs-lookup"><span data-stu-id="8a6fb-107">See:</span></span>

* <span data-ttu-id="8a6fb-108">[Denetim günlükleri](active-directory-reporting-azure-portal.md#activity-reports) daha fazla kavramsal bilgi için</span><span class="sxs-lookup"><span data-stu-id="8a6fb-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="8a6fb-109">[Hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) hello raporlama API'si hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="8a6fb-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="8a6fb-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8a6fb-110">Prerequisites</span></span>
<span data-ttu-id="8a6fb-111">Bu konudaki hello örnekleri kullanabilmeniz için önce toocomplete hello gerekir [Önkoşullar tooaccess hello Azure AD raporlama API'si](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="8a6fb-111">Before you can use hello samples in this topic, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="8a6fb-112">PowerShell betiği</span><span class="sxs-lookup"><span data-stu-id="8a6fb-112">PowerShell script</span></span>
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




## <a name="executing-hello-script"></a><span data-ttu-id="8a6fb-113">Merhaba komut dosyası yürütme</span><span class="sxs-lookup"><span data-stu-id="8a6fb-113">Executing hello script</span></span>
<span data-ttu-id="8a6fb-114">Sonra hello betik düzenlenmesini tamamlamayı, çalıştırın ve bu hello hello denetim günlüklerini rapor verileri döndürülen beklenen doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="8a6fb-114">Once you finish editing hello script, run it and verify that hello expected data from hello Audit logs report is returned.</span></span>

<span data-ttu-id="8a6fb-115">Merhaba betik çıkış raporundan hello oturum açma JSON biçiminde döndürür.</span><span class="sxs-lookup"><span data-stu-id="8a6fb-115">hello script returns output from hello sign-in report in JSON format.</span></span> <span data-ttu-id="8a6fb-116">Ayrıca oluşturur bir `SigninActivities.json` hello ile aynı dosyayı çıktı.</span><span class="sxs-lookup"><span data-stu-id="8a6fb-116">It also creates an `SigninActivities.json` file with hello same output.</span></span> <span data-ttu-id="8a6fb-117">Diğer raporlar ve yorum ihtiyacınız olmayan hello Çıkış biçimleri çıkışı hello betik tooreturn veriler değiştirerek deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8a6fb-117">You can experiment by modifying hello script tooreturn data from other reports, and comment out hello output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8a6fb-118">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="8a6fb-118">Next Steps</span></span>
* <span data-ttu-id="8a6fb-119">Bu konudaki toocustomize hello örnekleri ister misiniz?</span><span class="sxs-lookup"><span data-stu-id="8a6fb-119">Would you like toocustomize hello samples in this topic?</span></span> <span data-ttu-id="8a6fb-120">Merhaba denetleyin [Azure Active Directory oturum açma etkinliği API Başvurusu](active-directory-reporting-api-sign-in-activity-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8a6fb-120">Check out hello [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="8a6fb-121">Toosee kullanmanın eksiksiz bir genel görünüm istiyorsanız, Azure Active Directory raporlama API'si Merhaba, bkz: [hello Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="8a6fb-121">If you want toosee a complete overview of using hello Azure Active Directory reporting API, see [Getting started with hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="8a6fb-122">Merhaba toofind Azure Active Directory raporlama hakkında daha fazla bilgi isterseniz bkz [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="8a6fb-122">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

