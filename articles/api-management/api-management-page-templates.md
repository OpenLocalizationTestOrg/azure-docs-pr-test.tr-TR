---
title: "Sayfa Şablonları Azure API Management | Microsoft Docs"
description: "Azure API Management'te şablonları kümesi kullanılarak Geliştirici portal sayfalarına içeriğini özelleştirmeyi öğrenin."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: e57df269-1019-4b74-b74d-53155b809d59
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7f9ef37a694bce786b6acaa428df83f0cb23c2dc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="28988-103">Azure API Management sayfası şablonları</span><span class="sxs-lookup"><span data-stu-id="28988-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="28988-104">Azure API Management Geliştirici portal sayfalarına içeriklerini yapılandırma şablonları kümesini kullanarak içeriği özelleştirme yeteneği sağlar.</span><span class="sxs-lookup"><span data-stu-id="28988-104">Azure API Management provides you the ability to customize the content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="28988-105">Kullanarak [DotLiquid](http://dotliquidmarkup.org/) sözdizimi ve düzenleyiciyi, gibi [DotLiquid tasarımcıları için](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ve sağlanan bir dizi yerelleştirilmiş [dize kaynakları](api-management-template-resources.md#strings), [karakter kaynakları](api-management-template-resources.md#glyphs), ve [sayfa denetimleri](api-management-page-controls.md), bu şablonları kullanarak uygun gördüğünüz şekilde sayfaların yapılandırmak için büyük esneklik vardır.</span><span class="sxs-lookup"><span data-stu-id="28988-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and the editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility to configure the content of the pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="28988-106">Bu bölümdeki şablonları, oturum açma, oturum içeriğini yukarı özelleştirmenize olanak tanır ve sayfa sayfaları Geliştirici Portalı'nda bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="28988-106">The templates in this section allow you to customize the content of the sign in, sign up, and page not found pages in the developer portal.</span></span>  
  
-   [<span data-ttu-id="28988-107">Oturum Aç</span><span class="sxs-lookup"><span data-stu-id="28988-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="28988-108">Kaydol</span><span class="sxs-lookup"><span data-stu-id="28988-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="28988-109">Sayfa bulunamadı</span><span class="sxs-lookup"><span data-stu-id="28988-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="28988-110">Örnek varsayılan şablonları aşağıdaki belgelerde yer alır ancak değişikliği sürekli geliştirmeler nedeniyle tabidir.</span><span class="sxs-lookup"><span data-stu-id="28988-110">Sample default templates are included in the following documentation, but are subject to change due to continuous improvements.</span></span> <span data-ttu-id="28988-111">İstenen tek tek şablonları giderek Geliştirici Portalı'nda Canlı varsayılan şablonları görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="28988-111">You can view the live default templates in the developer portal by navigating to the desired individual templates.</span></span> <span data-ttu-id="28988-112">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [şablonları kullanarak API Management Geliştirici Portalı nasıl özelleştireceğinizi](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="28988-112">For more information about working with templates, see [How to customize the API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="28988-113"><a name="SignIn"></a>Oturum Aç</span><span class="sxs-lookup"><span data-stu-id="28988-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="28988-114">**Oturum** şablonu oturum açma sayfasında Geliştirici portalında özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="28988-114">The **sign in** template allows you to customize the sign in page in the developer portal.</span></span>  
  
 <span data-ttu-id="28988-115">![Oturum açma sayfası](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM oturum açma sayfasında Geliştirici Portalı şablonları")</span><span class="sxs-lookup"><span data-stu-id="28988-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="28988-116">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="28988-116">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SigninStrings|WebAuthenticationSigninTitle" %}</h2>  
{% if registrationEnabled == true %}  
<p class="text-center">{% localized "SigninStrings|WebAuthenticationNotAMember" %}</p>  
{% endif %}  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    {% if registrationEnabled == true %}  
        <p>{% localized "SigninStrings|WebAuthenticationSigininWithPassword" %}</p>  
    <basic-SignIn></basic-SignIn>  
    {% endif %}  
  </div>  
  
    {% if registrationEnabled != true and providers.size == 0 %}  
        {% localized "ProviderInfoStrings|TextboxExternalIdentitiesDisabled" %}  
  {% else %}  
        {% if providers.size > 0 %}  
      <div class="col-md-6">  
            <div class="providers-list">  
                <p class="text-left">  
                {% if registrationEnabled == true %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitation" %}  
                {% else %}  
                    {% localized "ProviderInfoStrings|TextboxExternalIdentitiesSigninInvitationPrimary" %}  
                {% endif %}  
                </p>  
        <providers></providers>  
            </div>  
    </div>  
        {% endif %}  
    {% endif %}  
  
  {% if userRegistrationTermsEnabled == true %}  
    <div class="col-md-6">  
        <div id="terms" class="modal" role="dialog" tabindex="-1">  
            <div class="modal-dialog">  
                <div class="modal-content">  
                    <div class="modal-header">  
                        <h4 class="modal-title">{% localized "SigninResources|DialogHeadingTermsOfUse" %}</h4>  
                    </div>  
                    <div class="modal-body break-all">{{userRegistrationTerms}}</div>  
                    <div class="modal-footer">  
                        <button type="button" class="btn btn-default" data-dismiss="modal">{% localized "CommonStrings|ButtonLabelClose" %}</button>  
                    </div>  
                </div>  
            </div>  
        </div>  
        <p>{% localized "SigninResources|TextblockUserRegistrationTermsProvided" %}</p>  
    </div>  
    {% endif %}  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="28988-117">Denetimler</span><span class="sxs-lookup"><span data-stu-id="28988-117">Controls</span></span>  
 <span data-ttu-id="28988-118">Bu şablon aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="28988-118">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="28988-119">temel oturum açma</span><span class="sxs-lookup"><span data-stu-id="28988-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="28988-120">sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="28988-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="28988-121">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="28988-121">Data model</span></span>  
 <span data-ttu-id="28988-122">[Kullanıcı oturum açma](api-management-template-data-model-reference.md#UseSignIn) varlık.</span><span class="sxs-lookup"><span data-stu-id="28988-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="28988-123">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="28988-123">Sample template data</span></span>  
  
```json  
{  
    "Email": null,  
    "Password": null,  
    "ReturnUrl": null,  
    "RememberMe": false,  
    "RegistrationEnabled": true,  
    "DelegationEnabled": false,  
    "DelegationUrl": null,  
    "SsoSignUpUrl": null,  
    "AuxServiceUrl": "https://manage.windowsazure.com/#Workspaces/ApiManagementExtension/service/contoso5/dashboard",  
    "Providers": [  
        {  
            "Properties": {  
                "AuthenticationType": "Aad",  
                "Caption": "Azure Active Directory"  
            },  
            "AuthenticationType": "Aad",  
            "Caption": "Azure Active Directory"  
        }  
    ],  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsEnabled": false  
}  
```  
  
##  <span data-ttu-id="28988-124"><a name="SignUp"></a>Kaydol</span><span class="sxs-lookup"><span data-stu-id="28988-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="28988-125">**Kaydolun** şablonu kayıt sayfasını Geliştirici portalında özelleştirmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="28988-125">The **sign up** template allows you to customize the sign up page in the developer portal.</span></span>  
  
 <span data-ttu-id="28988-126">![Oturum açma sayfasına](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "sayfasında Geliştirici Portalı şablonları APIM kaydolma")</span><span class="sxs-lookup"><span data-stu-id="28988-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="28988-127">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="28988-127">Default template</span></span>  
  
```xml  
<h2 class="text-center">{% localized "SignupStrings|PageTitleSignup" %}</h2>  
<p class="text-center">  
  {% localized "SignupStrings|WebAuthenticationAlreadyAMember" %} <a href="/signin">{% localized "SignupStrings|WebAuthenticationSigninNow" %}</a>  
</p>  
  
<div class="row center-block ap-idp-container">  
  <div class="col-md-6">  
    <p>{% localized "SignupStrings|WebAuthenticationCreateNewAccount" %}</p>  
    <sign-up></sign-up>  
  </div>  
</div>  
```  
  
### <a name="controls"></a><span data-ttu-id="28988-128">Denetimler</span><span class="sxs-lookup"><span data-stu-id="28988-128">Controls</span></span>  
 <span data-ttu-id="28988-129">Bu şablon aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="28988-129">This template may  use the following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="28988-130">Kaydolma</span><span class="sxs-lookup"><span data-stu-id="28988-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="28988-131">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="28988-131">Data model</span></span>  
 <span data-ttu-id="28988-132">[Kullanıcı Kaydolma](api-management-template-data-model-reference.md#UserSignUp) varlık.</span><span class="sxs-lookup"><span data-stu-id="28988-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="28988-133">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="28988-133">Sample template data</span></span>  
  
```json  
{  
    "PasswordConfirm": null,  
    "Password": null,  
    "PasswordVerdictLevel": 0,  
    "UserRegistrationTerms": null,  
    "UserRegistrationTermsOptions": 0,  
    "ConsentAccepted": false,  
    "Email": null,  
    "FirstName": null,  
    "LastName": null,  
    "UserData": null,  
    "NameIdentifier": null,  
    "ProviderName": null  
}  
```  
  
##  <span data-ttu-id="28988-134"><a name="PageNotFound"></a>Sayfa bulunamadı</span><span class="sxs-lookup"><span data-stu-id="28988-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="28988-135">**Sayfa bulunamadı** şablon sayfa Geliştirici Portalı'nda bulunamadı sayfayı özelleştirmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="28988-135">The **page not found** template allows you to customize the page not found page in the developer portal.</span></span>  
  
 <span data-ttu-id="28988-136">![Sayfa bulunamadı](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Portal şablonları sayfasında Geliştirici bulunamadı")</span><span class="sxs-lookup"><span data-stu-id="28988-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="28988-137">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="28988-137">Default template</span></span>  
  
```xml  
<h2>{% localized "NotFoundStrings|PageTitleNotFound" %}</h2>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialCause" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseOldLink" %}</li>  
  <li>{% localized "NotFoundStrings|TextblockPotentialCauseMisspelledUrl" %}</li>  
</ul>  
  
<h3>{% localized "NotFoundStrings|TitlePotentialSolution" %}</h3>  
<ul>  
  <li>{% localized "NotFoundStrings|TextblockPotentialSolutionRetype" %}</li>  
  <li>  
    {% capture textPotentialSolutionStartOver %}{% localized "NotFoundStrings|TextblockPotentialSolutionStartOver" %}{% endcapture %}  
    {% capture homeLink %}<a href="/">{% localized "NotFoundStrings|LinkLabelHomePage" %}</a>{% endcapture %}  
    {% assign replaceString = '{0}' %}  
  
    {{ textPotentialSolutionStartOver | replace : replaceString, homeLink }}  
  </li>  
</ul>  
  
<p>  
  {% capture textReportProblem %}{% localized "NotFoundStrings|TextReportProblem" %}{% endcapture %}  
  {% capture emailLink %}<a href="mailto:apimgmt@microsoft.com" target="_self" title="API Management Support">{% localized "NotFoundStrings|LinkLabelSendUsEmail" %}</a>{% endcapture %}  
  {% assign replaceString = '{0}' %}  
  
  {{ textReportProblem | replace : replaceString, emailLink }}  
</p>  
```  
  
### <a name="controls"></a><span data-ttu-id="28988-138">Denetimler</span><span class="sxs-lookup"><span data-stu-id="28988-138">Controls</span></span>  
 <span data-ttu-id="28988-139">Bu şablon herhangi kullanamazsınız [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="28988-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="28988-140">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="28988-140">Data model</span></span>  
  
|<span data-ttu-id="28988-141">Özellik</span><span class="sxs-lookup"><span data-stu-id="28988-141">Property</span></span>|<span data-ttu-id="28988-142">Tür</span><span class="sxs-lookup"><span data-stu-id="28988-142">Type</span></span>|<span data-ttu-id="28988-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="28988-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="28988-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="28988-144">referenceCode</span></span>|<span data-ttu-id="28988-145">Dize</span><span class="sxs-lookup"><span data-stu-id="28988-145">string</span></span>|<span data-ttu-id="28988-146">Bu sayfa bir iç hata sonucunda görüntüleniyorsa oluşturulan kod.</span><span class="sxs-lookup"><span data-stu-id="28988-146">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="28988-147">hata kodu</span><span class="sxs-lookup"><span data-stu-id="28988-147">errorCode</span></span>|<span data-ttu-id="28988-148">Dize</span><span class="sxs-lookup"><span data-stu-id="28988-148">string</span></span>|<span data-ttu-id="28988-149">Bu sayfa bir iç hata sonucunda görüntüleniyorsa oluşturulan kod.</span><span class="sxs-lookup"><span data-stu-id="28988-149">Code generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="28988-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="28988-150">emailBody</span></span>|<span data-ttu-id="28988-151">Dize</span><span class="sxs-lookup"><span data-stu-id="28988-151">string</span></span>|<span data-ttu-id="28988-152">Bu sayfa bir iç hata sonucunda görüntüleniyorsa oluşturulan gövde e-posta.</span><span class="sxs-lookup"><span data-stu-id="28988-152">Email body generated if this page was displayed as the result of an internal error.</span></span>|  
|<span data-ttu-id="28988-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="28988-153">requestedUrl</span></span>|<span data-ttu-id="28988-154">Dize</span><span class="sxs-lookup"><span data-stu-id="28988-154">string</span></span>|<span data-ttu-id="28988-155">Sayfa bulunamadı, istenen URL.</span><span class="sxs-lookup"><span data-stu-id="28988-155">The URL requested when the page was not found.</span></span>|  
|<span data-ttu-id="28988-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="28988-156">referrerUrl</span></span>|<span data-ttu-id="28988-157">Dize</span><span class="sxs-lookup"><span data-stu-id="28988-157">string</span></span>|<span data-ttu-id="28988-158">İstenen URL başvuran URL.</span><span class="sxs-lookup"><span data-stu-id="28988-158">The referrer URL to the requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="28988-159">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="28988-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="28988-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="28988-160">Next steps</span></span>
<span data-ttu-id="28988-161">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [şablonları kullanarak API Management Geliştirici Portalı nasıl özelleştireceğinizi](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="28988-161">For more information about working with templates, see [How to customize the API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>