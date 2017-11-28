---
title: "Uygulamanız Azure Active Directory Uygulama galerisinde listeleme"
description: "Çoklu oturum açma Azure Active Directory Galerisi'nde destekleyen bir uygulama listelemek nasıl | Microsoft Azure"
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
ms.openlocfilehash: cf25772bd9d92b59401aa5da76e6bbd5fa5ee3e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="listing-your-application-in-the-azure-active-directory-application-gallery"></a><span data-ttu-id="9d958-103">Uygulamanız Azure Active Directory Uygulama galerisinde listeleme</span><span class="sxs-lookup"><span data-stu-id="9d958-103">Listing your application in the Azure Active Directory application gallery</span></span>
<span data-ttu-id="9d958-104">Çoklu oturum açma Azure Active Directory ile destekleyen bir uygulama listelemek için [Azure AD galeri](https://azure.microsoft.com/marketplace/active-directory/all/), uygulamanın önce aşağıdaki tümleştirme modlarından birini uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9d958-104">To list an application that supports single sign-on with Azure Active Directory in the [Azure AD gallery](https://azure.microsoft.com/marketplace/active-directory/all/), the application first needs to implement one of the following integration modes:</span></span>

* <span data-ttu-id="9d958-105">**Openıd Connect** -Openıd Connect kimlik doğrulaması ve Azure AD API yapılandırmasını onayı için kullanarak Azure AD ile doğrudan tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="9d958-105">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="9d958-106">Uygulamanızı SAML desteklemez ve yalnızca bir tümleştirme başlıyorsanız, ardından öneri modu budur.</span><span class="sxs-lookup"><span data-stu-id="9d958-106">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
* <span data-ttu-id="9d958-107">**SAML** – üçüncü taraf kimlik sağlayıcıları SAML protokolü kullanarak yapılandırma yeteneğini uygulamanız zaten sahip.</span><span class="sxs-lookup"><span data-stu-id="9d958-107">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="9d958-108">Her iki modda listeleme gereksinimleri aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9d958-108">Listing requirements for each mode are below.</span></span>

## <a name="openid-connect-integration"></a><span data-ttu-id="9d958-109">Openıd Connect tümleştirme</span><span class="sxs-lookup"><span data-stu-id="9d958-109">OpenID Connect Integration</span></span>
<span data-ttu-id="9d958-110">Uygulamanızı aşağıdaki Azure AD ile tümleştirmek için [Geliştirici yönergeleri](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="9d958-110">To integrate your application with Azure AD, following the [developer instructions](active-directory-authentication-scenarios.md).</span></span> <span data-ttu-id="9d958-111">Ardından aşağıdaki sorular tamamlamak ve göndermek waadpartners@microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="9d958-111">Then complete the questions below and send to waadpartners@microsoft.com.</span></span>

* <span data-ttu-id="9d958-112">Uygulamanızla Azure AD ekibi tarafından tümleştirme test etmek için kullanılan bir test Kiracı ya da hesabı için kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9d958-112">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="9d958-113">Azure AD ekibi nasıl oturum açabilir ve kullanarak uygulamanızı örneğini Azure ad connect üzerinde yönergelerinizi [Azure AD onay framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span><span class="sxs-lookup"><span data-stu-id="9d958-113">Provide instructions on how the Azure AD team can sign in and connect an instance of Azure AD to your application using the [Azure AD consent framework](active-directory-integrating-applications.md#overview-of-the-consent-framework).</span></span> 
* <span data-ttu-id="9d958-114">Çoklu oturum açma ile uygulamanızı test etmek Azure AD ekibi için gerekli tüm ek yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d958-114">Provide any further instructions required for the Azure AD team to test single sign-on with your application.</span></span> 
* <span data-ttu-id="9d958-115">Aşağıdaki bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="9d958-115">Provide the info below:</span></span>

> <span data-ttu-id="9d958-116">Şirket adı:</span><span class="sxs-lookup"><span data-stu-id="9d958-116">Company Name:</span></span>
> 
> <span data-ttu-id="9d958-117">Şirket Web sitesi:</span><span class="sxs-lookup"><span data-stu-id="9d958-117">Company Website:</span></span>
> 
> <span data-ttu-id="9d958-118">Uygulama adı:</span><span class="sxs-lookup"><span data-stu-id="9d958-118">Application Name:</span></span>
> 
> <span data-ttu-id="9d958-119">Uygulama açıklaması (200 karakter sınırı):</span><span class="sxs-lookup"><span data-stu-id="9d958-119">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="9d958-120">Uygulama Web sitesi (bilgilendirme):</span><span class="sxs-lookup"><span data-stu-id="9d958-120">Application Website (informational):</span></span>
> 
> <span data-ttu-id="9d958-121">Uygulamanın teknik destek Web sitesi veya kişi bilgileri:</span><span class="sxs-lookup"><span data-stu-id="9d958-121">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="9d958-122">Uygulama Ayrıntıları https://portal.azure.com gösterildiği gibi uygulamanın uygulama Kimliğini:</span><span class="sxs-lookup"><span data-stu-id="9d958-122">Application  ID of the application, as shown in the application details at https://portal.azure.com:</span></span>
> 
> <span data-ttu-id="9d958-123">Uygulama kaydolma müşteriler için kaydolun nereye URL'si ve/ya da uygulama satın alın:</span><span class="sxs-lookup"><span data-stu-id="9d958-123">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="9d958-124">Uygulamanızın (kullanılabilir kategoriler için bkz. Azure Active Directory Marketi) altında listelenecek en çok üç kategorileri seçin:</span><span class="sxs-lookup"><span data-stu-id="9d958-124">Choose up to three categories for your application to be listed under (for available categories see the Azure Active Directory Marketplace):</span></span>
> 
> <span data-ttu-id="9d958-125">Uygulama küçük simgesi (PNG dosyası, 45px, düz bir arka plan rengi tarafından 45px) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9d958-125">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="9d958-126">Uygulama büyük simge (PNG dosyası, 215px, düz bir arka plan rengi tarafından 215px) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9d958-126">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="9d958-127">Uygulama Logo (PNG dosyası, 122px, saydam arka plan rengi tarafından 150px) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9d958-127">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

## <a name="saml-integration"></a><span data-ttu-id="9d958-128">SAML tümleştirme</span><span class="sxs-lookup"><span data-stu-id="9d958-128">SAML Integration</span></span>
<span data-ttu-id="9d958-129">SAML 2.0 destekleyen herhangi bir uygulama kullanarak doğrudan bir Azure AD kiracısı ile tümleştirilebilir [özel bir uygulama eklemek için bu yönergeleri](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="9d958-129">Any app that supports SAML 2.0 can be integrated directly with an Azure AD tenant using [these instructions to add a custom application](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="9d958-130">Uygulama tümleştirmesi Azure AD ile çalışıp çalışmadığını test ettikten sonra aşağıdaki bilgileri göndermek < mailto:waadpartners@microsoft.com >.</span><span class="sxs-lookup"><span data-stu-id="9d958-130">Once you have tested that your application integration works with Azure AD, send the following information to <mailto:waadpartners@microsoft.com>.</span></span>

* <span data-ttu-id="9d958-131">Uygulamanızla Azure AD ekibi tarafından tümleştirme test etmek için kullanılan bir test Kiracı ya da hesabı için kimlik bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9d958-131">Provide credentials for a test tenant or account with your application that can be used by the Azure AD team to test the integration.</span></span>  
* <span data-ttu-id="9d958-132">SAML oturum açma URL'si, veren URL'si (varlık kimliği) ve yanıt URL'si (onaylama tüketici hizmeti) değerleri, uygulamanız için açıklandığı gibi sağlamak [burada](../active-directory-saas-custom-apps.md).</span><span class="sxs-lookup"><span data-stu-id="9d958-132">Provide the SAML Sign-On URL, Issuer URL (entity ID), and Reply URL (assertion consumer service) values for your application, as described [here](../active-directory-saas-custom-apps.md).</span></span> <span data-ttu-id="9d958-133">SAML meta veri dosyasının bir parçası olarak bu değer genellikle sağlarsanız, sonra Lütfen, de gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9d958-133">If you typically provide these values as part of a SAML metadata file, then please send that as well.</span></span>
* <span data-ttu-id="9d958-134">Azure AD kimlik sağlayıcısı SAML 2.0 kullanarak uygulamanızdaki yapılandırma kısa bir açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="9d958-134">Provide a brief description of how to configure Azure AD as an identity provider in your application using SAML 2.0.</span></span> <span data-ttu-id="9d958-135">Uygulamanızı yapılandırma Azure AD kimlik sağlayıcısı Self Servis Yönetim Portalı üzerinden destekliyorsa, sonra lütfen yukarıda verilen kimlik bilgileri bu ayarlamanıza olanak içerir emin olun.</span><span class="sxs-lookup"><span data-stu-id="9d958-135">If your application supports configuring Azure AD as an identity provider through a self-service administrative portal, then please ensure the credentials provided above include the ability to set this up.</span></span>
* <span data-ttu-id="9d958-136">Aşağıdaki bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="9d958-136">Provide the info below:</span></span>

> <span data-ttu-id="9d958-137">Şirket adı:</span><span class="sxs-lookup"><span data-stu-id="9d958-137">Company Name:</span></span>
> 
> <span data-ttu-id="9d958-138">Şirket Web sitesi:</span><span class="sxs-lookup"><span data-stu-id="9d958-138">Company Website:</span></span>
> 
> <span data-ttu-id="9d958-139">Uygulama adı:</span><span class="sxs-lookup"><span data-stu-id="9d958-139">Application Name:</span></span>
> 
> <span data-ttu-id="9d958-140">Uygulama açıklaması (200 karakter sınırı):</span><span class="sxs-lookup"><span data-stu-id="9d958-140">Application Description (200 character limit):</span></span>
> 
> <span data-ttu-id="9d958-141">Uygulama Web sitesi (bilgilendirme):</span><span class="sxs-lookup"><span data-stu-id="9d958-141">Application Website (informational):</span></span>
> 
> <span data-ttu-id="9d958-142">Uygulamanın teknik destek Web sitesi veya kişi bilgileri:</span><span class="sxs-lookup"><span data-stu-id="9d958-142">Application Technical Support Website or Contact Info:</span></span>
> 
> <span data-ttu-id="9d958-143">Uygulama kaydolma müşteriler için kaydolun nereye URL'si ve/ya da uygulama satın alın:</span><span class="sxs-lookup"><span data-stu-id="9d958-143">Application Sign-Up URL where customers go to sign up for and /or purchase the application:</span></span>
> 
> <span data-ttu-id="9d958-144">Altında listelenen uygulamanız için en çok üç kategorileri seçin (kullanılabilir kategorilerini görmek için [Azure Active Directory Marketi](https://azure.microsoft.com/marketplace/active-directory/))):</span><span class="sxs-lookup"><span data-stu-id="9d958-144">Choose up to three categories for your application to be listed under (for available categories see the [Azure Active Directory Marketplace](https://azure.microsoft.com/marketplace/active-directory/))):</span></span>
> 
> <span data-ttu-id="9d958-145">Uygulama küçük simgesi (PNG dosyası, 45px, düz bir arka plan rengi tarafından 45px) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9d958-145">Attach Application Small Icon (PNG file, 45px by 45px, solid background color):</span></span>
> 
> <span data-ttu-id="9d958-146">Uygulama büyük simge (PNG dosyası, 215px, düz bir arka plan rengi tarafından 215px) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9d958-146">Attach Application Large Icon (PNG file, 215px by 215px, solid background color):</span></span>
> 
> <span data-ttu-id="9d958-147">Uygulama Logo (PNG dosyası, 122px, saydam arka plan rengi tarafından 150px) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9d958-147">Attach Application Logo (PNG file, 150px by 122px, transparent background color):</span></span>
> 
> 

