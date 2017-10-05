---
title: "Azure Active Directory oturum açma etkinliği raporu API örnekleri | Microsoft Docs"
description: "Azure Active Directory raporlama API'sini kullanmaya başlama"
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
ms.openlocfilehash: 7fc2b59fe37ed2ffe85925c457300ef8fd83c3c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="f66a8-103">Azure Active Directory oturum açma etkinliği raporu API örnekleri</span><span class="sxs-lookup"><span data-stu-id="f66a8-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="f66a8-104">Bu konuda, Azure Active Directory hakkındaki konuları API raporlama koleksiyonu bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="f66a8-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="f66a8-105">Azure AD raporlama kodu veya ilgili araçları kullanarak oturum açma etkinliği veri erişmenizi sağlayan bir API ile sağlar.</span><span class="sxs-lookup"><span data-stu-id="f66a8-105">Azure AD reporting provides you with an API that enables you to access sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="f66a8-106">Örnek kod için ile sağlamak için bu konunun kapsamı olan **etkinlik API oturum aç**.</span><span class="sxs-lookup"><span data-stu-id="f66a8-106">The scope of this topic is to provide you with sample code for the **sign-in activity API**.</span></span>

<span data-ttu-id="f66a8-107">Bkz.:</span><span class="sxs-lookup"><span data-stu-id="f66a8-107">See:</span></span>

* <span data-ttu-id="f66a8-108">[Denetim günlükleri](active-directory-reporting-azure-portal.md#activity-reports) daha fazla kavramsal bilgi için</span><span class="sxs-lookup"><span data-stu-id="f66a8-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="f66a8-109">[Azure Active Directory raporlama API'si ile çalışmaya başlama](active-directory-reporting-api-getting-started.md) raporlama API'si hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="f66a8-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f66a8-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f66a8-110">Prerequisites</span></span>
<span data-ttu-id="f66a8-111">Bu konudaki örnekler kullanmadan önce tamamlanması gereken [Azure AD raporlama API'si erişmek için Önkoşullar](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="f66a8-111">Before you can use the samples in this topic, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="f66a8-112">PowerShell betiği</span><span class="sxs-lookup"><span data-stu-id="f66a8-112">PowerShell script</span></span>
    # This script will require the Web Application and permissions setup in Azure Active Directory
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
        Write-Output "Save the output to a file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-the-script"></a><span data-ttu-id="f66a8-113">Komut dosyası yürütme</span><span class="sxs-lookup"><span data-stu-id="f66a8-113">Executing the script</span></span>
<span data-ttu-id="f66a8-114">Komut dosyası düzenlemeyi tamamladıktan sonra çalıştırın ve denetim beklenen verilerden rapor günlüklerini doğrulayın döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f66a8-114">Once you finish editing the script, run it and verify that the expected data from the Audit logs report is returned.</span></span>

<span data-ttu-id="f66a8-115">Komut çıktısı raporundan oturum açma JSON biçiminde döndürür.</span><span class="sxs-lookup"><span data-stu-id="f66a8-115">The script returns output from the sign-in report in JSON format.</span></span> <span data-ttu-id="f66a8-116">Ayrıca oluşturur bir `SigninActivities.json` aynı çıkış dosyası.</span><span class="sxs-lookup"><span data-stu-id="f66a8-116">It also creates an `SigninActivities.json` file with the same output.</span></span> <span data-ttu-id="f66a8-117">Veri diğer raporlar ve yorum ihtiyacınız olmayan çıkış biçimleri çıkışı döndürmek için komut dosyasını değiştirerek deneyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f66a8-117">You can experiment by modifying the script to return data from other reports, and comment out the output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f66a8-118">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="f66a8-118">Next Steps</span></span>
* <span data-ttu-id="f66a8-119">Bu konudaki örnekler özelleştirme ister misiniz?</span><span class="sxs-lookup"><span data-stu-id="f66a8-119">Would you like to customize the samples in this topic?</span></span> <span data-ttu-id="f66a8-120">Kullanıma [Azure Active Directory oturum açma etkinliği API Başvurusu](active-directory-reporting-api-sign-in-activity-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f66a8-120">Check out the [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="f66a8-121">Azure Active Directory'ı Raporlama API'si kullanan bir tam genel bakış görmek istiyorsanız bkz [Azure Active raporlama API'si Directory ile çalışmaya başlama](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="f66a8-121">If you want to see a complete overview of using the Azure Active Directory reporting API, see [Getting started with the Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="f66a8-122">Azure Active Directory raporlama hakkında daha fazla bilgi edinmek istiyorsanız, bkz: [Azure Active Directory raporlama Kılavuzu](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="f66a8-122">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

