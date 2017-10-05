---
title: "Azure Active Directory Sertifika tabanlı kimlik doğrulaması android'de | Microsoft Docs"
description: "Desteklenen senaryoları ve yapılandırma sertifika tabanlı kimlik doğrulama çözümlerinde gereksinimleri ile Android cihazları öğrenin"
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
ms.openlocfilehash: 8005bfe821fea25539c84efdccf6c49bd5f1f8ee
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a><span data-ttu-id="18741-103">Azure Active Directory Sertifika tabanlı kimlik doğrulamasını Android</span><span class="sxs-lookup"><span data-stu-id="18741-103">Azure Active Directory certificate-based authentication on Android</span></span>


<span data-ttu-id="18741-104">Sertifika tabanlı kimlik doğrulaması (CBA), Azure Active Directory tarafından Windows, Android veya iOS aygıtında bir istemci sertifikası ile Exchange online hesabınızı bağlanırken kimliğinin doğrulanmasını sağlar:</span><span class="sxs-lookup"><span data-stu-id="18741-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="18741-105">Microsoft Outlook ve Microsoft Word gibi Office mobil uygulamaları</span><span class="sxs-lookup"><span data-stu-id="18741-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="18741-106">Exchange ActiveSync (EAS) istemcileri</span><span class="sxs-lookup"><span data-stu-id="18741-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="18741-107">Bu özelliği yapılandıran bir kullanıcı adı ve parola birleşimini belirli mail ve Microsoft Office uygulamaları mobil cihazınızdan girin gereğini ortadan kaldırır.</span><span class="sxs-lookup"><span data-stu-id="18741-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="18741-108">Bu konu, gereksinimler ve desteklenen senaryoları ile Office 365 Kurumsal, iş, eğitim, ABD devlet kurumları, Çin kiracılar kullanıcılarının iOS(Android) cihazında CBA yapılandırmak için sağlar ve Almanya planları.</span><span class="sxs-lookup"><span data-stu-id="18741-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>



<span data-ttu-id="18741-109">Bu özellik, Office 365 US Government savunma ve Federal planlarda Önizleme'de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="18741-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>


## <a name="office-mobile-applications-support"></a><span data-ttu-id="18741-110">Office mobil uygulamaları desteği</span><span class="sxs-lookup"><span data-stu-id="18741-110">Office mobile applications support</span></span>
| <span data-ttu-id="18741-111">Uygulamalar</span><span class="sxs-lookup"><span data-stu-id="18741-111">Apps</span></span> | <span data-ttu-id="18741-112">Destek</span><span class="sxs-lookup"><span data-stu-id="18741-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="18741-113">Azure Information Protection uygulama</span><span class="sxs-lookup"><span data-stu-id="18741-113">Azure Information Protection app</span></span> |![İşaretli][1] |
| <span data-ttu-id="18741-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="18741-115">Microsoft Teams</span></span> |![İşaretli][1] |
| <span data-ttu-id="18741-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="18741-117">OneNote</span></span> |![İşaretli][1] |
| <span data-ttu-id="18741-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="18741-119">OneDrive</span></span> |![İşaretli][1] |
| <span data-ttu-id="18741-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="18741-121">Outlook</span></span> |![İşaretli][1] |
| <span data-ttu-id="18741-123">Power BI mobil uygulamaları</span><span class="sxs-lookup"><span data-stu-id="18741-123">Power BI mobile apps</span></span> |![İşaretli][1] |
| <span data-ttu-id="18741-125">Skype Kurumsal</span><span class="sxs-lookup"><span data-stu-id="18741-125">Skype for Business</span></span> |![İşaretli][1] |
| <span data-ttu-id="18741-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="18741-127">Word / Excel / PowerPoint</span></span> |![İşaretli][1] |
| <span data-ttu-id="18741-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="18741-129">Yammer</span></span> |![İşaretli][1] |


### <a name="implementation-requirements"></a><span data-ttu-id="18741-131">Uygulama gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="18741-131">Implementation requirements</span></span>

<span data-ttu-id="18741-132">Aygıt işletim sistemi sürümü Android 5.0 (Lolipop) olmalıdır ve üstü.</span><span class="sxs-lookup"><span data-stu-id="18741-132">The device OS version must be Android 5.0 (Lollipop) and above.</span></span> 

<span data-ttu-id="18741-133">Bir federasyon sunucusunun yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="18741-133">A federation server must be configured.</span></span>  

<span data-ttu-id="18741-134">Azure bir istemci sertifikası iptal etmek için Active Directory, ADFS belirteç aşağıdaki talep sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="18741-134">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="18741-135">(İstemci sertifikanın seri numarası)</span><span class="sxs-lookup"><span data-stu-id="18741-135">(The serial number of the client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="18741-136">(İstemci sertifikası veren dize)</span><span class="sxs-lookup"><span data-stu-id="18741-136">(The string for the issuer of the client certificate)</span></span> 

<span data-ttu-id="18741-137">ADFS belirteç (veya başka bir SAML belirteci) kullanılabilir olmaları durumunda azure Active Directory yenileme belirtecini bu talep ekler.</span><span class="sxs-lookup"><span data-stu-id="18741-137">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="18741-138">Yenileme belirteci doğrulanması gerektiğinde, bu bilgileri iptalini denetlemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="18741-138">When the refresh token needs to be validated, this information is used to check the revocation.</span></span> 

<span data-ttu-id="18741-139">En iyi uygulama, bir kullanıcı sertifikası almak yönergeler ile ADFS hata sayfaları güncelleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="18741-139">As a best practice, you should update the ADFS error pages with instructions on how to get a user certificate.</span></span>  
<span data-ttu-id="18741-140">Daha fazla ayrıntı için bkz: [AD FS oturum açma sayfalarını özelleştirme](https://technet.microsoft.com/library/dn280950.aspx).</span><span class="sxs-lookup"><span data-stu-id="18741-140">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>  

<span data-ttu-id="18741-141">Bazı Office uygulamaları (modern kimlik doğrulaması etkin ile) Gönder '*oturum açma istemini =*', istekte Azure ad.</span><span class="sxs-lookup"><span data-stu-id="18741-141">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="18741-142">Varsayılan olarak, Azure AD bu için ADFS isteğinde dönüşür '*wauth usernamepassworduri =*' (U/P kimlik doğrulama yapmak için ADFS ister) ve '*wfresh = 0*' (SSO durumu yoksay ve yeni bir kimlik doğrulaması yapmak için ADFS ister).</span><span class="sxs-lookup"><span data-stu-id="18741-142">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="18741-143">Sertifika tabanlı kimlik doğrulaması bu uygulamalar için etkinleştirmek istiyorsanız, varsayılan Azure AD davranışını değiştirmek gerekir.</span><span class="sxs-lookup"><span data-stu-id="18741-143">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="18741-144">Ayarlamanız yeterlidir '*PromptLoginBehavior*'ın Federasyon etki alanı ayarlarınızı'*devre dışı*'.</span><span class="sxs-lookup"><span data-stu-id="18741-144">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span> <span data-ttu-id="18741-145">Kullanabileceğiniz [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) bu görevi gerçekleştirmek için cmdlet:</span><span class="sxs-lookup"><span data-stu-id="18741-145">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="18741-146">Exchange ActiveSync istemcileri desteği</span><span class="sxs-lookup"><span data-stu-id="18741-146">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="18741-147">Belirli Exchange ActiveSync uygulamaları Android 5.0 (Lolipop) veya sonraki sürümlerde desteklenmektedir.</span><span class="sxs-lookup"><span data-stu-id="18741-147">Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported.</span></span> <span data-ttu-id="18741-148">E-posta uygulamanız bu özelliği destekleyen belirlemek için uygulama geliştiricisi ile temasa geçin.</span><span class="sxs-lookup"><span data-stu-id="18741-148">To determine if your email application does support this feature, please contact your application developer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="18741-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="18741-149">Next steps</span></span>

<span data-ttu-id="18741-150">Sertifika tabanlı kimlik doğrulaması, ortamınızda yapılandırmak istiyorsanız, bkz: [Android sertifika tabanlı kimlik doğrulamasını kullanmaya başlama](active-directory-certificate-based-authentication-get-started.md) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="18741-150">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
