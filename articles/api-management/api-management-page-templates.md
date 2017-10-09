---
title: "Azure API Management'te aaaPage şablonları | Microsoft Docs"
description: "Nasıl toocustomize hello Azure API Management'te şablonları kümesi kullanılarak Geliştirici portal sayfalarına içeriğini öğrenin."
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
ms.openlocfilehash: 84bd971ad4bcacfdd36c2ebbe05b16063f2a547b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="page-templates-in-azure-api-management"></a><span data-ttu-id="7332a-103">Azure API Management sayfası şablonları</span><span class="sxs-lookup"><span data-stu-id="7332a-103">Page templates in Azure API Management</span></span>
<span data-ttu-id="7332a-104">Azure API Management yeteneği toocustomize hello Geliştirici portal sayfalarına içeriklerini yapılandırma şablonları kümesini kullanarak içeriğini hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="7332a-104">Azure API Management provides you hello ability toocustomize hello content of developer portal pages using a set of templates that configure their content.</span></span> <span data-ttu-id="7332a-105">Kullanarak [DotLiquid](http://dotliquidmarkup.org/) sözdizimi ve hello düzenleyiciyi, gibi [tasarımcıları için DotLiquid](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), ve sağlanan bir dizi yerelleştirilmiş [dize kaynakları](api-management-template-resources.md#strings), [ Karakter kaynakları](api-management-template-resources.md#glyphs), ve [sayfasında denetimleri](api-management-page-controls.md), bu şablonları kullanarak uygun gördüğünüz şekilde hello sayfaların büyük esneklik tooconfigure hello içeriğe sahip.</span><span class="sxs-lookup"><span data-stu-id="7332a-105">Using [DotLiquid](http://dotliquidmarkup.org/) syntax and hello editor of your choice, such as [DotLiquid for Designers](https://github.com/dotliquid/dotliquid/wiki/DotLiquid-for-Designers), and a provided set of localized [String resources](api-management-template-resources.md#strings), [Glyph resources](api-management-template-resources.md#glyphs), and [Page controls](api-management-page-controls.md), you have great flexibility tooconfigure hello content of hello pages as you see fit using these templates.</span></span>  
  
 <span data-ttu-id="7332a-106">Bu bölümdeki Hello şablonları yukarı hello oturum açma, oturum toocustomize Merhaba içeriğine izin ve sayfa sayfaları hello Geliştirici Portalı'nda bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="7332a-106">hello templates in this section allow you toocustomize hello content of hello sign in, sign up, and page not found pages in hello developer portal.</span></span>  
  
-   [<span data-ttu-id="7332a-107">Oturum Aç</span><span class="sxs-lookup"><span data-stu-id="7332a-107">Sign in</span></span>](#SignIn)  
  
-   [<span data-ttu-id="7332a-108">Kaydol</span><span class="sxs-lookup"><span data-stu-id="7332a-108">Sign up</span></span>](#SignUp)  
  
-   [<span data-ttu-id="7332a-109">Sayfa bulunamadı</span><span class="sxs-lookup"><span data-stu-id="7332a-109">Page not found</span></span>](#PageNotFound)  
  
> [!NOTE]
>  <span data-ttu-id="7332a-110">Örnek varsayılan şablonları belgelerine aşağıdaki hello dahil olan, ancak konu toochange toocontinuous geliştirmeler nedeniyle.</span><span class="sxs-lookup"><span data-stu-id="7332a-110">Sample default templates are included in hello following documentation, but are subject toochange due toocontinuous improvements.</span></span> <span data-ttu-id="7332a-111">İstenen toohello tek tek şablonları giderek hello Canlı varsayılan şablonları hello Geliştirici Portalı'nda görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7332a-111">You can view hello live default templates in hello developer portal by navigating toohello desired individual templates.</span></span> <span data-ttu-id="7332a-112">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span><span class="sxs-lookup"><span data-stu-id="7332a-112">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/).</span></span>  
  
##  <span data-ttu-id="7332a-113"><a name="SignIn"></a>Oturum Aç</span><span class="sxs-lookup"><span data-stu-id="7332a-113"><a name="SignIn"></a> Sign in</span></span>  
 <span data-ttu-id="7332a-114">Merhaba **oturum** şablon sağlar, toocustomize hello oturum hello Geliştirici Portalı'ndaki sayfasında.</span><span class="sxs-lookup"><span data-stu-id="7332a-114">hello **sign in** template allows you toocustomize hello sign in page in hello developer portal.</span></span>  
  
 <span data-ttu-id="7332a-115">![Oturum açma sayfası](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM oturum açma sayfasında Geliştirici Portalı şablonları")</span><span class="sxs-lookup"><span data-stu-id="7332a-115">![Sign In Page](./media/api-management-page-templates/APIM-Sign-In-Page-Developer-Portal-Templates.png "APIM Sign In Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="7332a-116">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="7332a-116">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="7332a-117">Denetimler</span><span class="sxs-lookup"><span data-stu-id="7332a-117">Controls</span></span>  
 <span data-ttu-id="7332a-118">Bu şablon hello aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="7332a-118">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="7332a-119">temel oturum açma</span><span class="sxs-lookup"><span data-stu-id="7332a-119">basic-signin</span></span>](api-management-page-controls.md#basic-signin)  
  
-   [<span data-ttu-id="7332a-120">sağlayıcıları</span><span class="sxs-lookup"><span data-stu-id="7332a-120">providers</span></span>](api-management-page-controls.md#providers)  
  
### <a name="data-model"></a><span data-ttu-id="7332a-121">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="7332a-121">Data model</span></span>  
 <span data-ttu-id="7332a-122">[Kullanıcı oturum açma](api-management-template-data-model-reference.md#UseSignIn) varlık.</span><span class="sxs-lookup"><span data-stu-id="7332a-122">[User sign in](api-management-template-data-model-reference.md#UseSignIn) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="7332a-123">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="7332a-123">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="7332a-124"><a name="SignUp"></a>Kaydol</span><span class="sxs-lookup"><span data-stu-id="7332a-124"><a name="SignUp"></a> Sign up</span></span>  
 <span data-ttu-id="7332a-125">Merhaba **kaydolun** şablonu verir toocustomize hello kayıt sayfasını hello Geliştirici Portalı'nda.</span><span class="sxs-lookup"><span data-stu-id="7332a-125">hello **sign up** template allows you toocustomize hello sign up page in hello developer portal.</span></span>  
  
 <span data-ttu-id="7332a-126">![Oturum açma sayfasına](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "sayfasında Geliştirici Portalı şablonları APIM kaydolma")</span><span class="sxs-lookup"><span data-stu-id="7332a-126">![Sign Up Page](./media/api-management-page-templates/APIM-Sign-Up-Page-Developer-Portal-Templates.png "APIM Sign Up Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="7332a-127">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="7332a-127">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="7332a-128">Denetimler</span><span class="sxs-lookup"><span data-stu-id="7332a-128">Controls</span></span>  
 <span data-ttu-id="7332a-129">Bu şablon hello aşağıdaki kullanabilir [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="7332a-129">This template may  use hello following [page controls](api-management-page-controls.md).</span></span>  
  
-   [<span data-ttu-id="7332a-130">Kaydolma</span><span class="sxs-lookup"><span data-stu-id="7332a-130">sign-up</span></span>](api-management-page-controls.md#sign-up)  
  
### <a name="data-model"></a><span data-ttu-id="7332a-131">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="7332a-131">Data model</span></span>  
 <span data-ttu-id="7332a-132">[Kullanıcı Kaydolma](api-management-template-data-model-reference.md#UserSignUp) varlık.</span><span class="sxs-lookup"><span data-stu-id="7332a-132">[User sign up](api-management-template-data-model-reference.md#UserSignUp) entity.</span></span>  
  
### <a name="sample-template-data"></a><span data-ttu-id="7332a-133">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="7332a-133">Sample template data</span></span>  
  
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
  
##  <span data-ttu-id="7332a-134"><a name="PageNotFound"></a>Sayfa bulunamadı</span><span class="sxs-lookup"><span data-stu-id="7332a-134"><a name="PageNotFound"></a> Page not found</span></span>  
 <span data-ttu-id="7332a-135">Merhaba **sayfa bulunamadı** şablon sayfa hello Geliştirici Portalı'nda bulunamadı toocustomize hello sayfa sağlar.</span><span class="sxs-lookup"><span data-stu-id="7332a-135">hello **page not found** template allows you toocustomize hello page not found page in hello developer portal.</span></span>  
  
 <span data-ttu-id="7332a-136">![Sayfa bulunamadı](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Portal şablonları sayfasında Geliştirici bulunamadı")</span><span class="sxs-lookup"><span data-stu-id="7332a-136">![Not Found Page](./media/api-management-page-templates/APIM-Not-Found-Page-Developer-Portal-Templates.png "APIM Not Found Page Developer Portal Templates")</span></span>  
  
### <a name="default-template"></a><span data-ttu-id="7332a-137">Varsayılan şablonu</span><span class="sxs-lookup"><span data-stu-id="7332a-137">Default template</span></span>  
  
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
  
### <a name="controls"></a><span data-ttu-id="7332a-138">Denetimler</span><span class="sxs-lookup"><span data-stu-id="7332a-138">Controls</span></span>  
 <span data-ttu-id="7332a-139">Bu şablon herhangi kullanamazsınız [sayfasında denetimleri](api-management-page-controls.md).</span><span class="sxs-lookup"><span data-stu-id="7332a-139">This template may  not use any [page controls](api-management-page-controls.md).</span></span>  
  
### <a name="data-model"></a><span data-ttu-id="7332a-140">Veri modeli</span><span class="sxs-lookup"><span data-stu-id="7332a-140">Data model</span></span>  
  
|<span data-ttu-id="7332a-141">Özellik</span><span class="sxs-lookup"><span data-stu-id="7332a-141">Property</span></span>|<span data-ttu-id="7332a-142">Tür</span><span class="sxs-lookup"><span data-stu-id="7332a-142">Type</span></span>|<span data-ttu-id="7332a-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7332a-143">Description</span></span>|  
|--------------|----------|-----------------|  
|<span data-ttu-id="7332a-144">referenceCode</span><span class="sxs-lookup"><span data-stu-id="7332a-144">referenceCode</span></span>|<span data-ttu-id="7332a-145">Dize</span><span class="sxs-lookup"><span data-stu-id="7332a-145">string</span></span>|<span data-ttu-id="7332a-146">Bu sayfayı hello bir iç hata sonucunda görüntüleniyorsa oluşturulan kod.</span><span class="sxs-lookup"><span data-stu-id="7332a-146">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="7332a-147">hata kodu</span><span class="sxs-lookup"><span data-stu-id="7332a-147">errorCode</span></span>|<span data-ttu-id="7332a-148">Dize</span><span class="sxs-lookup"><span data-stu-id="7332a-148">string</span></span>|<span data-ttu-id="7332a-149">Bu sayfayı hello bir iç hata sonucunda görüntüleniyorsa oluşturulan kod.</span><span class="sxs-lookup"><span data-stu-id="7332a-149">Code generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="7332a-150">emailBody</span><span class="sxs-lookup"><span data-stu-id="7332a-150">emailBody</span></span>|<span data-ttu-id="7332a-151">Dize</span><span class="sxs-lookup"><span data-stu-id="7332a-151">string</span></span>|<span data-ttu-id="7332a-152">Bu sayfayı hello bir iç hata sonucunda görüntüleniyorsa oluşturulan gövde e-posta.</span><span class="sxs-lookup"><span data-stu-id="7332a-152">Email body generated if this page was displayed as hello result of an internal error.</span></span>|  
|<span data-ttu-id="7332a-153">requestedUrl</span><span class="sxs-lookup"><span data-stu-id="7332a-153">requestedUrl</span></span>|<span data-ttu-id="7332a-154">Dize</span><span class="sxs-lookup"><span data-stu-id="7332a-154">string</span></span>|<span data-ttu-id="7332a-155">Merhaba sayfa bulunamadı, istenen hello URL'si.</span><span class="sxs-lookup"><span data-stu-id="7332a-155">hello URL requested when hello page was not found.</span></span>|  
|<span data-ttu-id="7332a-156">referrerUrl</span><span class="sxs-lookup"><span data-stu-id="7332a-156">referrerUrl</span></span>|<span data-ttu-id="7332a-157">Dize</span><span class="sxs-lookup"><span data-stu-id="7332a-157">string</span></span>|<span data-ttu-id="7332a-158">Merhaba başvuran URL toohello URL istendi.</span><span class="sxs-lookup"><span data-stu-id="7332a-158">hello referrer URL toohello requested URL.</span></span>|  
  
### <a name="sample-template-data"></a><span data-ttu-id="7332a-159">Örnek şablon verileri</span><span class="sxs-lookup"><span data-stu-id="7332a-159">Sample template data</span></span>  
  
```json  
{  
    "referenceCode": null,  
    "errorCode": null,  
    "emailBody": null,  
    "requestedUrl": "https://contoso5.portal.azure-api.net:443/NotFoundPage?startEditTemplate=NotFoundPage",  
    "referrerUrl": "https://contoso5.portal.azure-api.net/signup?startEditTemplate=SignUpTemplate"  
}  
```

## <a name="next-steps"></a><span data-ttu-id="7332a-160">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7332a-160">Next steps</span></span>
<span data-ttu-id="7332a-161">Şablonları ile çalışma hakkında daha fazla bilgi için bkz: [nasıl toocustomize hello şablonları kullanarak API Management Geliştirici Portalı](api-management-developer-portal-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7332a-161">For more information about working with templates, see [How toocustomize hello API Management developer portal using templates](api-management-developer-portal-templates.md).</span></span>
