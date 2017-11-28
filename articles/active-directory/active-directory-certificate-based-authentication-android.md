---
title: "aaaAzure Active Directory Sertifika tabanlı kimlik doğrulamasını Android | Microsoft Docs"
description: "Merhaba desteklenen senaryolar ve sertifika tabanlı kimlik doğrulaması ile Android cihazları çözümlerinde yapılandırma hello gereksinimleri hakkında bilgi edinin"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/28/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 148275fa3da610530c278fcd57e02e907f735d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a><span data-ttu-id="f67a8-103">Azure Active Directory Sertifika tabanlı kimlik doğrulamasını Android</span><span class="sxs-lookup"><span data-stu-id="f67a8-103">Azure Active Directory certificate-based authentication on Android</span></span>


<span data-ttu-id="f67a8-104">Sertifika tabanlı kimlik doğrulaması (CBA) Azure Active Directory tarafından Windows, Android veya iOS aygıtında bir istemci sertifikası ile Exchange online hesabınızı bağlanırken kimlik doğrulaması toobe sağlar:</span><span class="sxs-lookup"><span data-stu-id="f67a8-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="f67a8-105">Microsoft Outlook ve Microsoft Word gibi Office mobil uygulamaları</span><span class="sxs-lookup"><span data-stu-id="f67a8-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="f67a8-106">Exchange ActiveSync (EAS) istemcileri</span><span class="sxs-lookup"><span data-stu-id="f67a8-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="f67a8-107">Bu özelliği yapılandıran hello gerek tooenter bir kullanıcı adı ve parola birleşimi belirli mail ve Microsoft Office uygulamaları, mobil Cihazınızda içine ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="f67a8-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="f67a8-108">Bu konu, hello gereksinimleri ve desteklenen hello senaryoları ile Office 365 Kurumsal, iş, eğitim, ABD devlet kurumları, Çin kiracılar kullanıcılarının iOS(Android) cihazında CBA yapılandırmak için sağlar ve Almanya planları.</span><span class="sxs-lookup"><span data-stu-id="f67a8-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>



<span data-ttu-id="f67a8-109">Bu özellik, Office 365 US Government savunma ve Federal planlarda Önizleme'de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="f67a8-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>


## <a name="office-mobile-applications-support"></a><span data-ttu-id="f67a8-110">Office mobil uygulamaları desteği</span><span class="sxs-lookup"><span data-stu-id="f67a8-110">Office mobile applications support</span></span>
| <span data-ttu-id="f67a8-111">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="f67a8-111">Apps</span></span> | <span data-ttu-id="f67a8-112">Destek</span><span class="sxs-lookup"><span data-stu-id="f67a8-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="f67a8-113">Azure Information Protection uygulama</span><span class="sxs-lookup"><span data-stu-id="f67a8-113">Azure Information Protection app</span></span> |![İşaretli][1] |
| <span data-ttu-id="f67a8-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="f67a8-115">Microsoft Teams</span></span> |![İşaretli][1] |
| <span data-ttu-id="f67a8-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="f67a8-117">OneNote</span></span> |![İşaretli][1] |
| <span data-ttu-id="f67a8-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="f67a8-119">OneDrive</span></span> |![İşaretli][1] |
| <span data-ttu-id="f67a8-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="f67a8-121">Outlook</span></span> |![İşaretli][1] |
| <span data-ttu-id="f67a8-123">Power BI mobil uygulamaları</span><span class="sxs-lookup"><span data-stu-id="f67a8-123">Power BI mobile apps</span></span> |![İşaretli][1] |
| <span data-ttu-id="f67a8-125">Skype Kurumsal</span><span class="sxs-lookup"><span data-stu-id="f67a8-125">Skype for Business</span></span> |![İşaretli][1] |
| <span data-ttu-id="f67a8-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="f67a8-127">Word / Excel / PowerPoint</span></span> |![İşaretli][1] |
| <span data-ttu-id="f67a8-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="f67a8-129">Yammer</span></span> |![İşaretli][1] |


### <a name="implementation-requirements"></a><span data-ttu-id="f67a8-131">Uygulama gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="f67a8-131">Implementation requirements</span></span>

<span data-ttu-id="f67a8-132">Merhaba aygıt işletim sistemi sürümü Android 5.0 (Lolipop) olmalıdır ve üstü.</span><span class="sxs-lookup"><span data-stu-id="f67a8-132">hello device OS version must be Android 5.0 (Lollipop) and above.</span></span> 

<span data-ttu-id="f67a8-133">Bir federasyon sunucusunun yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f67a8-133">A federation server must be configured.</span></span>  

<span data-ttu-id="f67a8-134">Azure Active Directory toorevoke bir istemci sertifikası hello ADFS belirteç talep aşağıdaki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="f67a8-134">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="f67a8-135">(Merhaba sertifikanın seri numarası hello istemci)</span><span class="sxs-lookup"><span data-stu-id="f67a8-135">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="f67a8-136">(Merhaba veren hello istemci sertifikasının hello dize)</span><span class="sxs-lookup"><span data-stu-id="f67a8-136">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="f67a8-137">Merhaba ADFS belirteç (veya başka bir SAML belirteci) kullanılabilir olmaları durumunda azure Active Directory bu talep toohello yenileme belirteci ekler.</span><span class="sxs-lookup"><span data-stu-id="f67a8-137">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="f67a8-138">Merhaba yenileme belirteci doğrulanmış toobe gerektiğinde, bu bilgiler kullanılan toocheck hello iptal olur.</span><span class="sxs-lookup"><span data-stu-id="f67a8-138">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="f67a8-139">En iyi uygulama, yönergelerini içeren hello ADFS hata sayfalarını güncelleştirmelidir tooget bir kullanıcı sertifikası.</span><span class="sxs-lookup"><span data-stu-id="f67a8-139">As a best practice, you should update hello ADFS error pages with instructions on how tooget a user certificate.</span></span>  
<span data-ttu-id="f67a8-140">Daha fazla ayrıntı için bkz: [hello AD FS oturum açma sayfalarını özelleştirme](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="f67a8-140">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>  

<span data-ttu-id="f67a8-141">Bazı Office uygulamaları (modern kimlik doğrulaması etkin ile) Gönder '*oturum açma istemini =*' tooAzure AD kendi isteği.</span><span class="sxs-lookup"><span data-stu-id="f67a8-141">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="f67a8-142">Varsayılan olarak, Azure AD bu hello isteği tooADFS çok dönüşür '*wauth usernamepassworduri =*' (ADFS toodo U/P auth ister) ve '*wfresh = 0*' (ADFS tooignore SSO durumu ister ve yeni bir kimlik doğrulaması yapın) .</span><span class="sxs-lookup"><span data-stu-id="f67a8-142">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="f67a8-143">Bu uygulamalar için sertifika tabanlı kimlik doğrulaması tooenable istiyorsanız toomodify hello varsayılan Azure AD davranışını gerekir.</span><span class="sxs-lookup"><span data-stu-id="f67a8-143">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="f67a8-144">Yalnızca kümesi hello '*PromptLoginBehavior*' federasyon etki alanını ayarlarınızda çok '*devre dışı*'.</span><span class="sxs-lookup"><span data-stu-id="f67a8-144">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="f67a8-145">Merhaba kullanabilirsiniz [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform bu görevi:</span><span class="sxs-lookup"><span data-stu-id="f67a8-145">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="f67a8-146">Exchange ActiveSync istemcileri desteği</span><span class="sxs-lookup"><span data-stu-id="f67a8-146">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="f67a8-147">Belirli Exchange ActiveSync uygulamaları Android 5.0 (Lolipop) veya sonraki sürümlerde desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="f67a8-147">Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported.</span></span> <span data-ttu-id="f67a8-148">toodetermine bu özellik, e-posta uygulamanızı destekliyorsa temasa geçin, uygulama geliştiricisi.</span><span class="sxs-lookup"><span data-stu-id="f67a8-148">toodetermine if your email application does support this feature, please contact your application developer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="f67a8-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f67a8-149">Next steps</span></span>

<span data-ttu-id="f67a8-150">Ortamınızda tooconfigure sertifika tabanlı kimlik doğrulaması istiyorsanız, bkz: [Android sertifika tabanlı kimlik doğrulamasını kullanmaya başlama](active-directory-certificate-based-authentication-get-started.md) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="f67a8-150">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
