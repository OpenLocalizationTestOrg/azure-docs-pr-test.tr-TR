---
title: "aaaListing hello Azure Active Directory Uygulama galerisinde uygulamanızı"
description: "Nasıl toolist çoklu oturum açma içinde destekleyen bir uygulama hello Azure Active Directory galeri | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: bryanla
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/27/2017
ms.author: bryanla
ms.custom: aaddev
ms.openlocfilehash: 09ccd3b4645a180059b9a9d502e39f1b8933c988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="listing-your-application-in-hello-azure-active-directory-application-gallery"></a><span data-ttu-id="77b63-103">Hello Azure Active Directory Uygulama galerisinde uygulamanızı listeleme</span><span class="sxs-lookup"><span data-stu-id="77b63-103">Listing your application in hello Azure Active Directory application gallery</span></span>
<span data-ttu-id="77b63-104">Çoklu oturum açma Azure Active Directory ile hello destekleyen bir uygulama toolist [Azure AD galeri](https://azure.microsoft.com/marketplace/active-directory/all/), hello uygulamanın ilk tümleştirme modları aşağıdaki Merhaba, tooimplement gerekir:</span><span class="sxs-lookup"><span data-stu-id="77b63-104">toolist an application that supports single sign-on with Azure Active Directory in hello [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), hello application first needs tooimplement one of hello following integration modes:</span></span>

* <span data-ttu-id="77b63-105">**Openıd Connect** - Openıd Connect kimlik doğrulamasını kullanan Azure AD ile tümleştirme doğrudan ve yapılandırması için Azure AD onay API hello.</span><span class="sxs-lookup"><span data-stu-id="77b63-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="77b63-106">Uygulamanızı SAML desteklemez ve yalnızca bir tümleştirme başlıyorsanız, ardından hello öneri modu budur.</span><span class="sxs-lookup"><span data-stu-id="77b63-106">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
* <span data-ttu-id="77b63-107">**SAML** – hello özelliği tooconfigure üçüncü taraf kimlik sağlayıcıları hello SAML protokolü kullanarak uygulamanızı zaten sahiptir.</span><span class="sxs-lookup"><span data-stu-id="77b63-107">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="77b63-108">Her iki modda listeleme gereksinimleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="77b63-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="77b63-109">Openıd Connect tümleştirme</span><span class="sxs-lookup"><span data-stu-id="77b63-109">OpenID Connect Integration</span></span>
<span data-ttu-id="77b63-110">toointegrate aşağıdaki hello Azure AD ile uygulamanızı [Geliştirici yönergeleri](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="77b63-110">toointegrate your application with Azure AD, following hello [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="77b63-111">Daha sonra tamamlamak aşağıdaki hello sorular ve göndermek toowaadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="77b63-111">Then complete hello questions below and send toowaadpartners@microsoft.com.</span></span>

* <span data-ttu-id="77b63-112">Uygulamanızla Azure AD team tootest hello tümleştirmesi hello tarafından kullanılan bir test Kiracı ya da hesabı için kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="77b63-112">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="77b63-113">Nasıl hello Azure AD team oturum açabilir ve Azure AD tooyour uygulaması hello kullanarak bir örneğine bağlanmak üzerinde yönergelerinizi [Azure AD onay framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="77b63-113">Provide instructions on how hello Azure AD team can sign in and connect an instance of Azure AD tooyour application using hello [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="77b63-114">Azure AD Hello için gerekli tüm ek yönergeler tootest çoklu oturum açma uygulamanız ile ekip sağlar.</span><span class="sxs-lookup"><span data-stu-id="77b63-114">Provide any further instructions required for hello Azure AD team tootest single sign-on with your application.</span></span> 
* <span data-ttu-id="77b63-115">Merhaba aşağıdaki bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="77b63-115">Provide hello info below:</span></span>

> <span data-ttu-id="77b63-116">Şirket adı:</span><span class="sxs-lookup"><span data-stu-id="77b63-116">Company Name:</span></span>
> 
> <span data-ttu-id="77b63-117">Şirket Web sitesi:</span><span class="sxs-lookup"><span data-stu-id="77b63-117">Company Website:</span></span>
> 
> <span data-ttu-id="77b63-118">Uygulama adı:</span><span class="sxs-lookup"><span data-stu-id="77b63-118">Application Name:</span></span>
> 
> <span data-ttu-id="77b63-119">Uygulama açıklaması (200 karakter sınırı):</span><span class="sxs-lookup"><span data-stu-id="77b63-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="77b63-120">Uygulama Web sitesi (bilgilendirme):</span><span class="sxs-lookup"><span data-stu-id="77b63-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="77b63-121">Uygulamanın teknik destek Web sitesi veya kişi bilgileri:</span><span class="sxs-lookup"><span data-stu-id="77b63-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="77b63-122">Https://portal.azure.com hello uygulama ayrıntıları gösterildiği gibi hello uygulamanın uygulama Kimliğini:</span><span class="sxs-lookup"><span data-stu-id="77b63-122">Application  ID of hello application, as shown in hello application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="77b63-123">Ya da uygulama kayıt müşteriler için toosign nereye URL hello uygulama satın alın:</span><span class="sxs-lookup"><span data-stu-id="77b63-123">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="77b63-124">(Hello Azure Active Directory Marketi kullanılabilir kategorilerini görmek için) altında listelenen, uygulama toobe toothree kategorileri seçin:</span><span class="sxs-lookup"><span data-stu-id="77b63-124">Choose up toothree categories for your application toobe listed under (for available categories see hello Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="77b63-125">Uygulama küçük simgesi (PNG dosyası, 45px, düz bir arka plan rengi tarafından 45px) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="77b63-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="77b63-126">Uygulama büyük simge (PNG dosyası, 215px, düz bir arka plan rengi tarafından 215px) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="77b63-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="77b63-127">Uygulama Logo (PNG dosyası, 122px, saydam arka plan rengi tarafından 150px) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="77b63-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="77b63-128">SAML tümleştirme</span><span class="sxs-lookup"><span data-stu-id="77b63-128">SAML Integration</span></span>
<span data-ttu-id="77b63-129">SAML 2.0 destekleyen herhangi bir uygulama kullanarak doğrudan bir Azure AD kiracısı ile tümleştirilebilir [bu yönergeleri tooadd özel bir uygulama](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="77b63-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions tooadd a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="77b63-130">Uygulama tümleştirmesi Azure AD ile çalışıp çalışmadığını test ettikten sonra aşağıdaki bilgilerle çok hello Gönder<mailto:waadpartners@microsoft.com>.</span><span class="sxs-lookup"><span data-stu-id="77b63-130">Once you have tested that your application integration works with Azure AD, send hello following information too<mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="77b63-131">Uygulamanızla Azure AD team tootest hello tümleştirmesi hello tarafından kullanılan bir test Kiracı ya da hesabı için kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="77b63-131">Provide credentials for a test tenant or account with your application that can be used by hello Azure AD team tootest hello integration.</span></span>  
* <span data-ttu-id="77b63-132">SAML oturum açma URL'si, veren URL'si (varlık kimliği) hello ve yanıt URL'si (onaylama tüketici hizmeti), uygulamanız için değerleri açıklandığı gibi sağlamak [burada](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="77b63-132">Provide hello SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="77b63-133">SAML meta veri dosyasının bir parçası olarak bu değer genellikle sağlarsanız, sonra Lütfen, de gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="77b63-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="77b63-134">Nasıl kısa bir açıklama sağlayın tooconfigure Azure AD kimlik sağlayıcısı SAML 2.0 kullanarak uygulamanızdaki.</span><span class="sxs-lookup"><span data-stu-id="77b63-134">Provide a brief description of how tooconfigure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="77b63-135">Uygulamanızı yapılandırma Azure AD kimlik sağlayıcısı Self Servis Yönetim Portalı üzerinden destekliyorsa, sonra lütfen yukarıda verilen hello kimlik hello özelliği tooset buna yukarı dahil emin olun.</span><span class="sxs-lookup"><span data-stu-id="77b63-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure hello credentials provided above include hello ability tooset this up.</span></span>
* <span data-ttu-id="77b63-136">Merhaba aşağıdaki bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="77b63-136">Provide hello info below:</span></span>

> <span data-ttu-id="77b63-137">Şirket adı:</span><span class="sxs-lookup"><span data-stu-id="77b63-137">Company Name:</span></span>
> 
> <span data-ttu-id="77b63-138">Şirket Web sitesi:</span><span class="sxs-lookup"><span data-stu-id="77b63-138">Company Website:</span></span>
> 
> <span data-ttu-id="77b63-139">Uygulama adı:</span><span class="sxs-lookup"><span data-stu-id="77b63-139">Application Name:</span></span>
> 
> <span data-ttu-id="77b63-140">Uygulama açıklaması (200 karakter sınırı):</span><span class="sxs-lookup"><span data-stu-id="77b63-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="77b63-141">Uygulama Web sitesi (bilgilendirme):</span><span class="sxs-lookup"><span data-stu-id="77b63-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="77b63-142">Uygulamanın teknik destek Web sitesi veya kişi bilgileri:</span><span class="sxs-lookup"><span data-stu-id="77b63-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="77b63-143">Ya da uygulama kayıt müşteriler için toosign nereye URL hello uygulama satın alın:</span><span class="sxs-lookup"><span data-stu-id="77b63-143">Application Sign-Up URL where customers go toosign up for and /or purchase hello application:</span></span>
> 
> <span data-ttu-id="77b63-144">Altında listelenen, uygulama toobe toothree kategorileri seçin (Merhaba kullanılabilir kategorilerini görmek için [Azure Active Directory Marketi](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="77b63-144">Choose up toothree categories for your application toobe listed under (for available categories see hello [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="77b63-145">Uygulama küçük simgesi (PNG dosyası, 45px, düz bir arka plan rengi tarafından 45px) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="77b63-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="77b63-146">Uygulama büyük simge (PNG dosyası, 215px, düz bir arka plan rengi tarafından 215px) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="77b63-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="77b63-147">Uygulama Logo (PNG dosyası, 122px, saydam arka plan rengi tarafından 150px) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="77b63-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

