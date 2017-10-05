---
title: "SSO için Azure AD uygulama proxy'si yönetme | Microsoft Docs"
description: "Çoklu oturum açma uygulama proxy'si ile uygulama temelleri hakkında bilgi edinin"
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
ms.openlocfilehash: 1deb3d91049d45fe26791783e13bd23e0a7d9f95
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-does-azure-ad-application-proxy-provide-single-sign-on"></a><span data-ttu-id="31942-103">Azure AD uygulama proxy'si nasıl çoklu oturum açma sağlar?</span><span class="sxs-lookup"><span data-stu-id="31942-103">How does Azure AD Application Proxy provide single sign-on?</span></span>

<span data-ttu-id="31942-104">Çoklu oturum açma bir anahtar Azure AD uygulama proxy'si öğesidir.</span><span class="sxs-lookup"><span data-stu-id="31942-104">Single sign-on is a key element of Azure AD Application Proxy.</span></span>  <span data-ttu-id="31942-105">Kullanıcılarınız yalnızca bulut Azure Active Directory'de oturum açmak zorunda olduğu için en iyi kullanıcı deneyimi sağlar.</span><span class="sxs-lookup"><span data-stu-id="31942-105">It provides the best user experience because your users only have to sign in to Azure Active Directory in the cloud.</span></span> <span data-ttu-id="31942-106">Azure Active Directory kimlik doğrulaması sonra uygulama ara sunucusu Bağlayıcısı'nı şirket içi uygulama için kimlik doğrulaması gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="31942-106">Once they authenticate to Azure Active Directory, the Application Proxy connector handles the authentication to the on-premises application.</span></span> <span data-ttu-id="31942-107">Arka uç uygulaması uzak bir kullanıcı uygulama proxy'si ve etki alanına katılmış bir cihazda normal kullanım aracılığıyla oturum açmayı arasındaki farkı bildiremez.</span><span class="sxs-lookup"><span data-stu-id="31942-107">The backend application can't tell the difference between a remote user signing in through Application Proxy and a regular use on a domain-joined device.</span></span> 

<span data-ttu-id="31942-108">Çoklu oturum açma uygulamalarınızda Azure Active Directory kullanmak için seçmeniz gerekir **Azure Active Directory** ön kimlik doğrulama yöntemi olarak.</span><span class="sxs-lookup"><span data-stu-id="31942-108">To use Azure Active Directory for single sign-on to your applications, you need to select **Azure Active Directory** as the pre-authentication method.</span></span> <span data-ttu-id="31942-109">Seçerseniz **geçiş** kullanıcılarınızın Azure Active Directory'ye hiç kimlik doğrulaması yok ancak düz uygulamaya yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="31942-109">If you select **Passthrough** then your users don't authenticate to Azure Active Directory at all, but are directed straight to the application.</span></span> <span data-ttu-id="31942-110">Bu ayar, önce bir uygulama yayımlamak veya Azure portalında uygulamanıza gidin ve uygulama Proxy ayarlarını düzenleyin yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="31942-110">You can configure this setting when you first publish an application, or navigate to your application in the Azure portal and edit the Application Proxy settings.</span></span> 

<span data-ttu-id="31942-111">Çoklu oturum açma seçenekleri görmek için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="31942-111">To see your single sign-on options, follow these steps:</span></span>

1. <span data-ttu-id="31942-112">[Azure Portal](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="31942-112">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="31942-113">Gidin **Azure Active Directory** > **kurumsal uygulamalar** > **tüm uygulamaları**.</span><span class="sxs-lookup"><span data-stu-id="31942-113">Navigate to **Azure Active Directory** > **Enterprise applications** > **All applications**.</span></span>
3. <span data-ttu-id="31942-114">Çoklu oturum açma seçenekleri yönetmek istediğiniz uygulamayı seçin.</span><span class="sxs-lookup"><span data-stu-id="31942-114">Select the app whose single sign-on options you want to manage.</span></span>
4. <span data-ttu-id="31942-115">Seçin **çoklu oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="31942-115">Select **Single sign-on**.</span></span>

   ![SSO açılır menü](./media/application-proxy-sso-overview/single-sign-on-mode.png)

<span data-ttu-id="31942-117">Açılır menüsünde, uygulamanız için çoklu oturum açma için beş seçenekleri gösterir:</span><span class="sxs-lookup"><span data-stu-id="31942-117">The dropdown menu shows five options for single sign-on to your application:</span></span>

* <span data-ttu-id="31942-118">Azure AD çoklu oturum açma devre dışı özelliğini</span><span class="sxs-lookup"><span data-stu-id="31942-118">Azure AD single sign-on disabled</span></span>
* <span data-ttu-id="31942-119">Parola tabanlı oturum açma</span><span class="sxs-lookup"><span data-stu-id="31942-119">Password-based sign-on</span></span>
* <span data-ttu-id="31942-120">Bağlantılı oturum açma</span><span class="sxs-lookup"><span data-stu-id="31942-120">Linked sign-on</span></span>
* <span data-ttu-id="31942-121">Tümleşik Windows kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="31942-121">Integrated Windows Authentication</span></span>
* <span data-ttu-id="31942-122">Üstbilgi tabanlı oturum açma</span><span class="sxs-lookup"><span data-stu-id="31942-122">Header-based sign-on</span></span>

## <a name="azure-ad-single-sign-on-disabled"></a><span data-ttu-id="31942-123">Azure AD çoklu oturum açma devre dışı özelliğini</span><span class="sxs-lookup"><span data-stu-id="31942-123">Azure AD single sign-on disabled</span></span>

<span data-ttu-id="31942-124">Çoklu oturum açma uygulamanız için Azure Active Directory Tümleştirme kullanmak istemiyorsanız, seçin **Azure AD çoklu oturum açma devre dışı özelliğini**.</span><span class="sxs-lookup"><span data-stu-id="31942-124">If you don't want to use Azure Active Directory integration for single sign-on to your application, choose **Azure AD single sign-on disabled**.</span></span> <span data-ttu-id="31942-125">Bu seçenek ile kullanıcılarınızın iki kez doğrulanabilir.</span><span class="sxs-lookup"><span data-stu-id="31942-125">With this option selected, your users may authenticate twice.</span></span> <span data-ttu-id="31942-126">İlk olarak, Azure Active Directory kimlik doğrulaması ve uygulama için oturum açın.</span><span class="sxs-lookup"><span data-stu-id="31942-126">First, they authenticate to Azure Active Directory and then sign in to the application itself.</span></span> 

<span data-ttu-id="31942-127">Bu seçenek iyi bir şirket içi uygulamanız kullanıcıların kimlik doğrulaması yapmasına gerektirmez, ancak bir uzaktan erişim için güvenlik katmanı olarak Azure Active Directory eklemek istediğiniz seçimdir.</span><span class="sxs-lookup"><span data-stu-id="31942-127">This option is a good choice if your on-premises application doesn't require users to authenticate, but you want to add Azure Active Directory as a layer of security for remote access.</span></span> 

## <a name="password-based-sign-on"></a><span data-ttu-id="31942-128">Parola tabanlı oturum açma</span><span class="sxs-lookup"><span data-stu-id="31942-128">Password-based sign-on</span></span>

<span data-ttu-id="31942-129">Azure Active Directory parola kasası olarak şirket içi uygulamalarınız için kullanmak istiyorsanız, tercih **parola tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="31942-129">If you want to use Azure Active Directory as a password vault for your on-premises applications, choose **Password-based sign-on**.</span></span> <span data-ttu-id="31942-130">Uygulamanızı erişim belirteçleri veya üstbilgileri yerine bir kullanıcı adı/parola bileşik kimlik doğrulamasını, bu seçenek iyi bir seçimdir.</span><span class="sxs-lookup"><span data-stu-id="31942-130">This option is a good choice if your application authenticates with a username/password combo instead of access tokens or headers.</span></span> <span data-ttu-id="31942-131">Parola tabanlı ile oturum açma, kullanıcılarınızın erişen uygulama ilk zaman oturum açmanız.</span><span class="sxs-lookup"><span data-stu-id="31942-131">With password-based sign-on, your users need to sign in to the application the first time they access it.</span></span> <span data-ttu-id="31942-132">Bundan sonra Azure Active Directory kullanıcı adı ve parola kullanıcı adına sağlar.</span><span class="sxs-lookup"><span data-stu-id="31942-132">After that, Azure Active Directory supplies the username and password on behalf of the user.</span></span> 

<span data-ttu-id="31942-133">Parola tabanlı oturum açmayı ayarlama hakkında daha fazla bilgi için bkz: [tek oturum açma için uygulama proxy'si ile vaulting parola](application-proxy-sso-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="31942-133">For information about setting up password-based sign-on, see [Password vaulting for single sign-on with Application Proxy](application-proxy-sso-azure-portal.md).</span></span>

## <a name="linked-sign-on"></a><span data-ttu-id="31942-134">Bağlantılı oturum açma</span><span class="sxs-lookup"><span data-stu-id="31942-134">Linked sign-on</span></span>

<span data-ttu-id="31942-135">Şirket içi kimliklerinizi için ayarlanmış bir tek oturum açma çözümü zaten varsa, seçin **bağlantılı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="31942-135">If you already have a single sign-on solution set up for your on-premises identities, choose **Linked sign-on**.</span></span> <span data-ttu-id="31942-136">Bu seçenek varolan SSO çözümleri yararlanmak Azure Active Directory sağlar, ancak hala kullanıcılarınızın uygulamaya uzaktan erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="31942-136">This option enables Azure Active Directory to leverage existing SSO solutions, but still gives your users remote access to the application.</span></span> 

<span data-ttu-id="31942-137">Bağlantılı oturum açma (varolan çoklu oturum açma resmi olarak bilinir) özelliğini hakkında daha fazla bilgi için bkz: [uygulama erişimi ve çoklu oturum açma ile Azure Active Directory nedir?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span><span class="sxs-lookup"><span data-stu-id="31942-137">For information about linked sign-on (formally known as existing single sign-on), see [What is application access and single sign-on with Azure Active Directory?](active-directory-appssoaccess-whatis.md#how-does-single-sign-on-with-azure-active-directory-work).</span></span>

## <a name="integrated-windows-authentication"></a><span data-ttu-id="31942-138">Tümleşik Windows kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="31942-138">Integrated Windows Authentication</span></span>

<span data-ttu-id="31942-139">Çoklu oturum açma için Kerberos Kısıtlı temsilci (KCD) kullanmak istiyorsanız seçin veya tümleşik Windows Authentication(IWA) kullanıyorsanız, şirket içi uygulamalarınızı **tümleşik Windows kimlik doğrulaması**.</span><span class="sxs-lookup"><span data-stu-id="31942-139">If your on-premises applications use Integrated Windows Authentication(IWA) or if you want to use Kerberos Constrained Delegation (KCD) for single sign-on, choose **Integrated Windows Authentication**.</span></span> <span data-ttu-id="31942-140">Bu seçenek ile kullanıcılarınız yalnızca Azure Active Directory kimlik doğrulaması yapmanız ve kullanıcının Kerberos belirteci almak ve uygulamada oturum açmak için uygulama ara sunucusu Bağlayıcısı'nı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="31942-140">With this option, your users only need to authenticate to Azure Active Directory, and then the Application Proxy connector impersonates the user to get a Kerberos token and sign in to the application.</span></span> 

<span data-ttu-id="31942-141">Tümleşik Windows kimlik doğrulaması ayarlama hakkında daha fazla bilgi için bkz: [Kerberos Kısıtlı temsilci çoklu oturum açma için uygulama proxy'si ile](active-directory-application-proxy-sso-using-kcd.md).</span><span class="sxs-lookup"><span data-stu-id="31942-141">For information about setting up Integrated Windows Authentication, see [Kerberos Constrained Delegation for single sign-on with Application Proxy](active-directory-application-proxy-sso-using-kcd.md).</span></span>

## <a name="header-based-sign-on"></a><span data-ttu-id="31942-142">Üstbilgi tabanlı oturum açma</span><span class="sxs-lookup"><span data-stu-id="31942-142">Header-based sign-on</span></span> 

<span data-ttu-id="31942-143">Uygulamalarınız için kimlik doğrulama üstbilgileri kullanıyorsa seçin **üstbilgi tabanlı oturum açma**.</span><span class="sxs-lookup"><span data-stu-id="31942-143">If your applications use headers for authentication, choose **Header-based sign-on**.</span></span> <span data-ttu-id="31942-144">Bu seçenek ile kullanıcılarınız için kimlik doğrulaması yalnızca Azure Active Directory gerekir.</span><span class="sxs-lookup"><span data-stu-id="31942-144">With this option, your users only need to authentication the Azure Active Directory.</span></span> <span data-ttu-id="31942-145">Bir üçüncü taraf kimlik doğrulama hizmetiyle Microsoft iş ortakları, uygulama için bir üstbilgi biçime Azure Active Directory'ye erişim belirteci çevrilen PingAccess çağrılır.</span><span class="sxs-lookup"><span data-stu-id="31942-145">Microsoft partners with a third-party authentication service called PingAccess, which translated the Azure Active Directory access token into a header format for the application.</span></span> 

<span data-ttu-id="31942-146">Üstbilgi tabanlı kimlik doğrulaması ayarlama hakkında daha fazla bilgi için bkz: [üstbilgi tabanlı kimlik doğrulaması için çoklu oturum açma uygulama proxy'si ile](application-proxy-ping-access.md).</span><span class="sxs-lookup"><span data-stu-id="31942-146">For information about setting up header-based authentication, see [Header-based authentication for single sign-on with Application Proxy](application-proxy-ping-access.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31942-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="31942-147">Next steps</span></span>

- [<span data-ttu-id="31942-148">Çoklu oturum açma için uygulama proxy'si ile vaulting parola</span><span class="sxs-lookup"><span data-stu-id="31942-148">Password vaulting for single sign-on with Application Proxy</span></span>](application-proxy-sso-azure-portal.md)
- [<span data-ttu-id="31942-149">Kerberos Kısıtlı temsilci çoklu oturum açma için uygulama proxy'si ile uygulama</span><span class="sxs-lookup"><span data-stu-id="31942-149">Kerberos Constrained Delegation for single sign-on with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)
- [<span data-ttu-id="31942-150">Uygulama proxy'si ile çoklu oturum açma için üstbilgi tabanlı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="31942-150">Header-based authentication for single sign-on with Application Proxy</span></span>](application-proxy-ping-access.md) 
