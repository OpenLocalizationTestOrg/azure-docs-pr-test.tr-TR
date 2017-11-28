---
title: "Azure AD uygulama proxy'si için SSO aaaManage | Microsoft Docs"
description: "Merhaba temelleri uygulama proxy'si ile çoklu oturum açma hakkında bilgi edinin"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: a278751a5cb1bf98c970a4e5d2eb3edc3b784096
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a><span data-ttu-id="02c74-103">Azure AD uygulama proxy'si nasıl çoklu oturum açma sağlar?</span><span class="sxs-lookup"><span data-stu-id="02c74-103">How does Azure AD Application Proxy provide single sign-on?</span></span>

<span data-ttu-id="02c74-104">Çoklu oturum açma bir anahtar Azure AD uygulama proxy'si öğesidir.</span><span class="sxs-lookup"><span data-stu-id="02c74-104">Single sign-on is a key element of Azure AD Application Proxy.</span></span>  <span data-ttu-id="02c74-105">Kullanıcılarınız yalnızca toosign tooAzure hello bulutta Active Directory içinde olduğundan hello en iyi kullanıcı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="02c74-105">It provides hello best user experience because your users only have toosign in tooAzure Active Directory in hello cloud.</span></span> <span data-ttu-id="02c74-106">TooAzure Active Directory kimlik doğrulaması sonra hello uygulama ara sunucusu Bağlayıcısı hello kimlik doğrulama toohello şirket içi uygulama işler.</span><span class="sxs-lookup"><span data-stu-id="02c74-106">Once they authenticate tooAzure Active Directory, hello Application Proxy connector handles hello authentication toohello on-premises application.</span></span> <span data-ttu-id="02c74-107">Merhaba arka uç uygulaması uzak bir kullanıcı uygulama proxy'si ve etki alanına katılmış bir cihazda normal kullanım aracılığıyla oturum açmayı hello birbirinden bildiremez.</span><span class="sxs-lookup"><span data-stu-id="02c74-107">hello backend application can't tell hello difference between a remote user signing in through Application Proxy and a regular use on a domain-joined device.</span></span> 

<span data-ttu-id="02c74-108">Azure Active Directory toouse tek oturum açma tooyour uygulamalar için gereksinim duyduğunuz tooselect **Azure Active Directory** hello ön kimlik doğrulama yöntemi olarak.</span><span class="sxs-lookup"><span data-stu-id="02c74-108">toouse Azure Active Directory for single sign-on tooyour applications, you need tooselect **Azure Active Directory** as hello pre-authentication method.</span></span> <span data-ttu-id="02c74-109">Seçerseniz **geçiş** kullanıcılarınızın tooAzure Active Directory hiç kimlik doğrulaması yok ancak yönlendirilmiş düz toohello uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="02c74-109">If you select **Passthrough** then your users don't authenticate tooAzure Active Directory at all, but are directed straight toohello application.</span></span> <span data-ttu-id="02c74-110">Bu ayar, önce bir uygulama yayımlamak veya tooyour uygulamada hello Azure portalına gidin ve hello uygulama Proxy ayarlarını düzenleyin yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="02c74-110">You can configure this setting when you first publish an application, or navigate tooyour application in hello Azure portal and edit hello Application Proxy settings.</span></span> 

<span data-ttu-id="02c74-111">toosee, çoklu oturum açma seçenekleri, şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="02c74-111">toosee your single sign-on options, follow these steps:</span></span>

1. <span data-ttu-id="02c74-112">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="02c74-112">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="02c74-113">Çok gidin**Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="02c74-113">Navigate too**Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="02c74-114">Çoklu oturum açma seçeneklerini seçin hello uygulama toomanage istiyor.</span><span class="sxs-lookup"><span data-stu-id="02c74-114">Select hello app whose single sign-on options you want toomanage.</span></span>
4. <span data-ttu-id="02c74-115">Seçin **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="02c74-115">Select **Single sign-on**.</span></span>

   ![SSO açılır menü](./media/application-proxy-sso-overview/single-sign-on-mode.png)

<span data-ttu-id="02c74-117">Merhaba açılır menüsünde, tek oturum açma tooyour uygulama için beş seçenekleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="02c74-117">hello dropdown menu shows five options for single sign-on tooyour application:</span></span>

* <span data-ttu-id="02c74-118">Azure AD çoklu oturum açma devre dışı özelliğini</span><span class="sxs-lookup"><span data-stu-id="02c74-118">Azure AD single sign-on disabled</span></span>
* <span data-ttu-id="02c74-119">Parola tabanlı oturum açma</span><span class="sxs-lookup"><span data-stu-id="02c74-119">Password-based sign-on</span></span>
* <span data-ttu-id="02c74-120">Bağlantılı oturum açma</span><span class="sxs-lookup"><span data-stu-id="02c74-120">Linked sign-on</span></span>
* <span data-ttu-id="02c74-121">Tümleşik Windows kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="02c74-121">Integrated Windows Authentication</span></span>
* <span data-ttu-id="02c74-122">Üstbilgi tabanlı oturum açma</span><span class="sxs-lookup"><span data-stu-id="02c74-122">Header-based sign-on</span></span>

## <a name="azure-ad-single-sign-on-disabled"></a><span data-ttu-id="02c74-123">Azure AD çoklu oturum açma devre dışı özelliğini</span><span class="sxs-lookup"><span data-stu-id="02c74-123">Azure AD single sign-on disabled</span></span>

<span data-ttu-id="02c74-124">Çoklu oturum açma tooyour uygulaması için Azure Active Directory Tümleştirme toouse istemiyorsanız seçin **Azure AD çoklu oturum açma devre dışı özelliğini**.</span><span class="sxs-lookup"><span data-stu-id="02c74-124">If you don't want toouse Azure Active Directory integration for single sign-on tooyour application, choose **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="02c74-125">Bu seçenek ile kullanıcılarınızın iki kez doğrulanabilir.</span><span class="sxs-lookup"><span data-stu-id="02c74-125">With this option selected, your users may authenticate twice.</span></span> <span data-ttu-id="02c74-126">İlk olarak, tooAzure Active Directory kimlik doğrulaması ve toohello uygulamada oturum açın.</span><span class="sxs-lookup"><span data-stu-id="02c74-126">First, they authenticate tooAzure Active Directory and then sign in toohello application itself.</span></span> 

<span data-ttu-id="02c74-127">Bu seçenek iyi bir şirket içi uygulamanız kullanıcıların tooauthenticate gerektirmez, ancak uzaktan erişim için bir güvenlik katmanı Azure Active Directory tooadd istediğiniz seçimdir.</span><span class="sxs-lookup"><span data-stu-id="02c74-127">This option is a good choice if your on-premises application doesn't require users tooauthenticate, but you want tooadd Azure Active Directory as a layer of security for remote access.</span></span> 

## <a name="password-based-sign-on"></a><span data-ttu-id="02c74-128">Parola tabanlı oturum açma</span><span class="sxs-lookup"><span data-stu-id="02c74-128">Password-based sign-on</span></span>

<span data-ttu-id="02c74-129">Şirket içi uygulamalarınız için parola kasası olarak toouse Azure Active Directory istiyorsanız, tercih **parola tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="02c74-129">If you want toouse Azure Active Directory as a password vault for your on-premises applications, choose **Password-based sign-on**.</span></span> <span data-ttu-id="02c74-130">Uygulamanızı erişim belirteçleri veya üstbilgileri yerine bir kullanıcı adı/parola bileşik kimlik doğrulamasını, bu seçenek iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="02c74-130">This option is a good choice if your application authenticates with a username/password combo instead of access tokens or headers.</span></span> <span data-ttu-id="02c74-131">Parola tabanlı ile oturum açma, kullanıcılarınızın toohello uygulama hello toosign erişen ilk kez gerekir.</span><span class="sxs-lookup"><span data-stu-id="02c74-131">With password-based sign-on, your users need toosign in toohello application hello first time they access it.</span></span> <span data-ttu-id="02c74-132">Bundan sonra Azure Active Directory hello kullanıcı adı ve parola hello kullanıcı adına sağlar.</span><span class="sxs-lookup"><span data-stu-id="02c74-132">After that, Azure Active Directory supplies hello username and password on behalf of hello user.</span></span> 

<span data-ttu-id="02c74-133">Parola tabanlı oturum açmayı ayarlama hakkında daha fazla bilgi için bkz: [tek oturum açma için uygulama proxy'si ile vaulting parola](application-proxy-sso-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="02c74-133">For information about setting up password-based sign-on, see [Password vaulting for single sign-on with Application Proxy](application-proxy-sso-azure-portal.md).</span></span>

## <a name="linked-sign-on"></a><span data-ttu-id="02c74-134">Bağlantılı oturum açma</span><span class="sxs-lookup"><span data-stu-id="02c74-134">Linked sign-on</span></span>

<span data-ttu-id="02c74-135">Şirket içi kimliklerinizi için ayarlanmış bir tek oturum açma çözümü zaten varsa, seçin **bağlantılı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="02c74-135">If you already have a single sign-on solution set up for your on-premises identities, choose **Linked sign-on**.</span></span> <span data-ttu-id="02c74-136">Bu seçenek, Azure Active Directory tooleverage varolan SSO çözümleri sağlar, ancak hala kullanıcılarınızın uzaktan erişim toohello uygulamaya sunar.</span><span class="sxs-lookup"><span data-stu-id="02c74-136">This option enables Azure Active Directory tooleverage existing SSO solutions, but still gives your users remote access toohello application.</span></span> 

<span data-ttu-id="02c74-137">Bağlantılı oturum açma (varolan çoklu oturum açma resmi olarak bilinir) özelliğini hakkında daha fazla bilgi için bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="02c74-137">For information about linked sign-on (formally known as existing single sign-on), see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="integrated-windows-authentication"></a><span data-ttu-id="02c74-138">Tümleşik Windows kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="02c74-138">Integrated Windows Authentication</span></span>

<span data-ttu-id="02c74-139">Şirket içi uygulamalarınız tümleşik Windows Authentication(IWA) kullanıyorsa ya da çoklu oturum açma için toouse Kerberos Kısıtlı temsilci (KCD) istiyorsanız seçin **tümleşik Windows kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="02c74-139">If your on-premises applications use Integrated Windows Authentication(IWA) or if you want toouse Kerberos Constrained Delegation (KCD) for single sign-on, choose **Integrated Windows Authentication**.</span></span> <span data-ttu-id="02c74-140">Bu seçenek ile kullanıcılarınız tooauthenticate tooAzure Active Directory yeterlidir ve hello kullanıcı tooget bir Kerberos belirteci ve toohello uygulamada oturum hello uygulama ara sunucusu Bağlayıcısı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="02c74-140">With this option, your users only need tooauthenticate tooAzure Active Directory, and then hello Application Proxy connector impersonates hello user tooget a Kerberos token and sign in toohello application.</span></span> 

<span data-ttu-id="02c74-141">Tümleşik Windows kimlik doğrulaması ayarlama hakkında daha fazla bilgi için bkz: [Kerberos Kısıtlı temsilci çoklu oturum açma için uygulama proxy'si ile](active-directory-application-proxy-sso-using-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="02c74-141">For information about setting up Integrated Windows Authentication, see [Kerberos Constrained Delegation for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md).</span></span>

## <a name="header-based-sign-on"></a><span data-ttu-id="02c74-142">Üstbilgi tabanlı oturum açma</span><span class="sxs-lookup"><span data-stu-id="02c74-142">Header-based sign-on</span></span> 

<span data-ttu-id="02c74-143">Uygulamalarınız için kimlik doğrulama üstbilgileri kullanıyorsa seçin **üstbilgi tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="02c74-143">If your applications use headers for authentication, choose **Header-based sign-on**.</span></span> <span data-ttu-id="02c74-144">Bu seçenek ile kullanıcılarınız tooauthentication hello Azure Active Directory yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="02c74-144">With this option, your users only need tooauthentication hello Azure Active Directory.</span></span> <span data-ttu-id="02c74-145">Microsoft iş ortaklarının bir üçüncü taraf kimlik doğrulama hizmeti ile Merhaba uygulaması için bir üstbilgi biçime hello Azure Active Directory'ye erişim belirteci çevrilen PingAccess çağrılır.</span><span class="sxs-lookup"><span data-stu-id="02c74-145">Microsoft partners with a third-party authentication service called PingAccess, which translated hello Azure Active Directory access token into a header format for hello application.</span></span> 

<span data-ttu-id="02c74-146">Üstbilgi tabanlı kimlik doğrulaması ayarlama hakkında daha fazla bilgi için bkz: [üstbilgi tabanlı kimlik doğrulaması için çoklu oturum açma uygulama proxy'si ile](application-proxy-ping-access.md).</span><span class="sxs-lookup"><span data-stu-id="02c74-146">For information about setting up header-based authentication, see [Header-based authentication for single sign-on with Application Proxy](application-proxy-ping-access.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="02c74-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="02c74-147">Next steps</span></span>

- [<span data-ttu-id="02c74-148">Çoklu oturum açma için uygulama proxy'si ile vaulting parola</span><span class="sxs-lookup"><span data-stu-id="02c74-148">Password vaulting for single sign-on with Application Proxy</span></span>](application-proxy-sso-azure-portal.md)
- [<span data-ttu-id="02c74-149">Kerberos Kısıtlı temsilci çoklu oturum açma için uygulama proxy'si ile uygulama</span><span class="sxs-lookup"><span data-stu-id="02c74-149">Kerberos Constrained Delegation for single sign-on with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="02c74-150">Uygulama proxy'si ile çoklu oturum açma için üstbilgi tabanlı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="02c74-150">Header-based authentication for single sign-on with Application Proxy</span></span>](application-proxy-ping-access.md) 
