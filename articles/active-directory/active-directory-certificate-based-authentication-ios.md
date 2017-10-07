---
title: "aaaAzure Active Directory Sertifika tabanlı kimlik doğrulaması iOS | Microsoft Docs"
description: "Merhaba desteklenen senaryolar ve sertifika tabanlı kimlik doğrulaması ile iOS cihazları çözümlerinde yapılandırma hello gereksinimleri hakkında bilgi edinin"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 4486ff5239c2897b3bc187053f31d74807430301
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="391ad-103">Azure Active Directory Sertifika tabanlı kimlik doğrulaması iOS</span><span class="sxs-lookup"><span data-stu-id="391ad-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="391ad-104">Sertifika tabanlı kimlik doğrulaması (CBA) Azure Active Directory tarafından Windows, Android veya iOS aygıtında bir istemci sertifikası ile Exchange online hesabınızı bağlanırken kimlik doğrulaması toobe sağlar:</span><span class="sxs-lookup"><span data-stu-id="391ad-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="391ad-105">Microsoft Outlook ve Microsoft Word gibi Office mobil uygulamaları</span><span class="sxs-lookup"><span data-stu-id="391ad-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="391ad-106">Exchange ActiveSync (EAS) istemcileri</span><span class="sxs-lookup"><span data-stu-id="391ad-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="391ad-107">Bu özelliği yapılandıran hello gerek tooenter bir kullanıcı adı ve parola birleşimi belirli mail ve Microsoft Office uygulamaları, mobil Cihazınızda içine ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="391ad-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="391ad-108">Bu konu, hello gereksinimleri ve desteklenen hello senaryoları ile Office 365 Kurumsal, iş, eğitim, ABD devlet kurumları, Çin kiracılar kullanıcılarının iOS(Android) cihazında CBA yapılandırmak için sağlar ve Almanya planları.</span><span class="sxs-lookup"><span data-stu-id="391ad-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="391ad-109">Bu özellik, Office 365 US Government savunma ve Federal planlarda Önizleme'de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="391ad-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="391ad-110">Office mobil uygulamaları desteği</span><span class="sxs-lookup"><span data-stu-id="391ad-110">Office mobile applications support</span></span>

| <span data-ttu-id="391ad-111">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="391ad-111">Apps</span></span> | <span data-ttu-id="391ad-112">Destek</span><span class="sxs-lookup"><span data-stu-id="391ad-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="391ad-113">Azure Information Protection uygulama</span><span class="sxs-lookup"><span data-stu-id="391ad-113">Azure Information Protection app</span></span> |![İşaretli][1] |
| <span data-ttu-id="391ad-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="391ad-115">Microsoft Teams</span></span> |![İşaretli][1] |
| <span data-ttu-id="391ad-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="391ad-117">OneNote</span></span> |![İşaretli][1] |
| <span data-ttu-id="391ad-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="391ad-119">OneDrive</span></span> |![İşaretli][1] |
| <span data-ttu-id="391ad-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="391ad-121">Outlook</span></span> |![İşaretli][1] |
| <span data-ttu-id="391ad-123">Power BI mobil uygulamaları</span><span class="sxs-lookup"><span data-stu-id="391ad-123">Power BI mobile apps</span></span> |![İşaretli][1] |
| <span data-ttu-id="391ad-125">Skype Kurumsal</span><span class="sxs-lookup"><span data-stu-id="391ad-125">Skype for Business</span></span> |![İşaretli][1] |
| <span data-ttu-id="391ad-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="391ad-127">Word / Excel / PowerPoint</span></span> |![İşaretli][1] |
| <span data-ttu-id="391ad-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="391ad-129">Yammer</span></span> |![İşaretli][1] |


## <a name="requirements"></a><span data-ttu-id="391ad-131">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="391ad-131">Requirements</span></span> 

<span data-ttu-id="391ad-132">Merhaba aygıt işletim sistemi sürümü iOS 9 olmalıdır ve üstü</span><span class="sxs-lookup"><span data-stu-id="391ad-132">hello device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="391ad-133">Bir federasyon sunucusunun yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="391ad-133">A federation server must be configured.</span></span>  

<span data-ttu-id="391ad-134">Office uygulamaları iOS için Microsoft Authenticator gereklidir.</span><span class="sxs-lookup"><span data-stu-id="391ad-134">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="391ad-135">Azure Active Directory toorevoke bir istemci sertifikası hello ADFS belirteç talep aşağıdaki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="391ad-135">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="391ad-136">(Merhaba sertifikanın seri numarası hello istemci)</span><span class="sxs-lookup"><span data-stu-id="391ad-136">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="391ad-137">(Merhaba veren hello istemci sertifikasının hello dize)</span><span class="sxs-lookup"><span data-stu-id="391ad-137">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="391ad-138">Merhaba ADFS belirteç (veya başka bir SAML belirteci) kullanılabilir olmaları durumunda azure Active Directory bu talep toohello yenileme belirteci ekler.</span><span class="sxs-lookup"><span data-stu-id="391ad-138">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="391ad-139">Merhaba yenileme belirteci doğrulanmış toobe gerektiğinde, bu bilgiler kullanılan toocheck hello iptal olur.</span><span class="sxs-lookup"><span data-stu-id="391ad-139">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="391ad-140">En iyi uygulama, hello aşağıdakilerle hello ADFS hata sayfaları güncelleştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="391ad-140">As a best practice, you should update hello ADFS error pages with hello following:</span></span>

* <span data-ttu-id="391ad-141">Merhaba gereksinim İos'ta hello Microsoft Authenticator yüklemek için</span><span class="sxs-lookup"><span data-stu-id="391ad-141">hello requirement for installing hello Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="391ad-142">Yönergeler tooget bir kullanıcı sertifikası.</span><span class="sxs-lookup"><span data-stu-id="391ad-142">Instructions on how tooget a user certificate.</span></span> 

<span data-ttu-id="391ad-143">Daha fazla ayrıntı için bkz: [hello AD FS oturum açma sayfalarını özelleştirme](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="391ad-143">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="391ad-144">Bazı Office uygulamaları (modern kimlik doğrulaması etkin ile) Gönder '*oturum açma istemini =*' tooAzure AD kendi isteği.</span><span class="sxs-lookup"><span data-stu-id="391ad-144">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="391ad-145">Varsayılan olarak, Azure AD bu hello isteği tooADFS çok dönüşür '*wauth usernamepassworduri =*' (ADFS toodo U/P auth ister) ve '*wfresh = 0*' (ADFS tooignore SSO durumu ister ve yeni bir kimlik doğrulaması yapın) .</span><span class="sxs-lookup"><span data-stu-id="391ad-145">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="391ad-146">Bu uygulamalar için sertifika tabanlı kimlik doğrulaması tooenable istiyorsanız toomodify hello varsayılan Azure AD davranışını gerekir.</span><span class="sxs-lookup"><span data-stu-id="391ad-146">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="391ad-147">Yalnızca kümesi hello '*PromptLoginBehavior*' federasyon etki alanını ayarlarınızda çok '*devre dışı*'.</span><span class="sxs-lookup"><span data-stu-id="391ad-147">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="391ad-148">Merhaba kullanabilirsiniz [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform bu görevi:</span><span class="sxs-lookup"><span data-stu-id="391ad-148">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="391ad-149">Exchange ActiveSync istemcileri desteği</span><span class="sxs-lookup"><span data-stu-id="391ad-149">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="391ad-150">İOS 9 veya sonrası, hello yerel iOS posta istemcisi desteklenir.</span><span class="sxs-lookup"><span data-stu-id="391ad-150">On iOS 9 or later, hello native iOS mail client is supported.</span></span> <span data-ttu-id="391ad-151">Diğer tüm Exchange ActiveSync uygulamaları için toodetermine bu özellik destekleniyorsa, kişi, uygulama geliştiricisi.</span><span class="sxs-lookup"><span data-stu-id="391ad-151">For all other Exchange ActiveSync applications, toodetermine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="391ad-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="391ad-152">Next steps</span></span>

<span data-ttu-id="391ad-153">Ortamınızda tooconfigure sertifika tabanlı kimlik doğrulaması istiyorsanız, bkz: [Android sertifika tabanlı kimlik doğrulamasını kullanmaya başlama](active-directory-certificate-based-authentication-get-started.md) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="391ad-153">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
