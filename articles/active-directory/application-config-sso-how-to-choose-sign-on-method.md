---
title: "aaaHow toodetermine hangi çoklu oturum açma yöntemi toouse | Microsoft Docs"
description: "Azure AD tarafından desteklenen hello tek oturum açma modu anlamak ve nasıl için bir hangi toochoose hello uygulama toopick ilgilendiğiniz."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 64f0bc1dc8281d1ab8222fd50eaceaf710704886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodetermine-what-single-sign-on-method-toouse"></a><span data-ttu-id="cf2df-103">Nasıl toodetermine hangi çoklu oturum açma yöntemi toouse</span><span class="sxs-lookup"><span data-stu-id="cf2df-103">How toodetermine what single-sign on method toouse</span></span>

<span data-ttu-id="cf2df-104">Bu makalede, Azure AD tarafından desteklenen toounderstand hello tek oturum açma modu Yardım ve nasıl için bir hangi toochoose hello uygulama toopick ilgilendiğiniz.</span><span class="sxs-lookup"><span data-stu-id="cf2df-104">This article help you toounderstand hello single sign-on modes supported by Azure AD and how toopick which one toochoose for hello application you are interested in.</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="cf2df-105">Çoklu oturum açma ve belirli bir uygulama türleri tarafından desteklenen modları sağlama</span><span class="sxs-lookup"><span data-stu-id="cf2df-105">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="cf2df-106">Merhaba farklı çoklu oturum açma ve her uygulama türleri yukarıda hello tarafından desteklenen modları sağlama Hello tabloda açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cf2df-106">hello table below describes hello different single sign-on and provisioning modes supported by each of hello above application types.</span></span> <span data-ttu-id="cf2df-107">Bu tablo toohelp kullanabileceğiniz hangi uygulamanın gereksinim toounderstand tooadd toosupport belirli bir amaca.</span><span class="sxs-lookup"><span data-stu-id="cf2df-107">You can use this table toohelp you toounderstand which application you need tooadd toosupport a specific goal.</span></span>

  ![AP türleri tablosu](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a><span data-ttu-id="cf2df-109">Nasıl toochoose tek bir oturum açma modu</span><span class="sxs-lookup"><span data-stu-id="cf2df-109">How toochoose a single sign-on mode</span></span>

<span data-ttu-id="cf2df-110">desteklenen hello **çoklu oturum açma** modları Azure AD uygulamaları için aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="cf2df-110">hello supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="cf2df-111">**Azure AD çoklu oturum açma devre dışı özelliğini** – Azure AD çoklu oturum açma devre dışı özelliğini seçin **tek oturum açma modu** , çoklu oturum açma ile Azure AD ile henüz hazır değil toointegrate misiniz veya onu yalnızca sınama</span><span class="sxs-lookup"><span data-stu-id="cf2df-111">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready toointegrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="cf2df-112">**Bağlantılı oturum açma** – hello seçin [bağlantılı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tek oturum açma modu** mevcut tek oturum açma çözümüyle zaten bağlı olan bir uygulamanız varsa ya da yalnızca istiyorsanız Basit bir bağlantı, kullanıcılarınızın toopublish kendi [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) veya [Office 365 uygulama Başlatıcı](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="cf2df-112">**Linked Sign-on** – choose hello [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want toopublish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="cf2df-113">**Parola tabanlı oturum açma** – hello seçin [parola tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tek oturum açma modu** uygulamanız bir HTML kullanıcı adı ve parola alanı oluşturur ve toostore istiyorsanız, Kullanıcı adı ve parola toobe güvenli bir şekilde yeniden toohello uygulamayı daha sonra</span><span class="sxs-lookup"><span data-stu-id="cf2df-113">**Password-based Sign-on** – choose hello [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want toostore that username and password securely toobe replayed toohello application later</span></span>

-   <span data-ttu-id="cf2df-114">**SAML tabanlı oturum açma** – hello seçin [SAML tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) çoklu oturum açma, uygulamanızın hello SAML veya Openıd Connect protokollerini destekler veya toobe mümkün toomap kullanıcılar isterseniz modu toospecific uygulama rolleri dayalı Talep kuralları, SAML tanımladığınız *(**Not:** hello uygulama proxy'si bir uygulama için yapılandırıldığında, bu seçenek kullanılamaz) *</span><span class="sxs-lookup"><span data-stu-id="cf2df-114">**SAML-based Sign-on** – choose hello [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports hello SAML or OpenID Connect protocols, or you want toobe able toomap users toospecific application roles based on rules you define in your SAML claims *(**Note:** this option is not available when hello application proxy is configured for an application)*</span></span>

-   <span data-ttu-id="cf2df-115">**Üstbilgi tabanlı oturum açma** – bu seçin [üstbilgi tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) HTTP üstbilgisi destekleyen PingAccess kullanan bir uygulamanız varsa, tek oturum açma modu temel tooperform çoklu oturum üzerinde çok istediğiniz kimlik doğrulaması *(**Not:** bu seçenek yalnızca hello uygulama proxy'si ve PingAccess yapılandırıldığında bir uygulama için kullanılabilir) *</span><span class="sxs-lookup"><span data-stu-id="cf2df-115">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish tooperform single-sign on too*(**Note:** this option is only available when hello application proxy and PingAccess is configured for an application)*</span></span>

-   <span data-ttu-id="cf2df-116">**Tümleşik Windows kimlik doğrulaması** – hello seçin [tümleşik Windows kimlik doğrulaması](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) çoklu oturum açma tooperform çoklu oturum üzerinde çok istediğiniz şirket içi WIA uygulamanın gösterme zaman modu*()*  *Not:** bu seçenek yalnızca hello uygulama proxy'si bir uygulama için yapılandırıldığında kullanılabilir) *</span><span class="sxs-lookup"><span data-stu-id="cf2df-116">**Integrated Windows Authentication** – choose hello [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish tooperform single-sign on too*(**Note:** this option is only available when hello application proxy is configured for an application)*</span></span>

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="cf2df-117">Özel geliştirilmiş uygulamalar için çoklu oturum açma modları</span><span class="sxs-lookup"><span data-stu-id="cf2df-117">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="cf2df-118">Uygulamaları hello geliştirilen özel sahip [özel geliştirilmiş uygulama](#_Custom-Developed_Applications) deneyimi de Yukarıda listelenmeyen ek tek oturum açma modunu destekler.</span><span class="sxs-lookup"><span data-stu-id="cf2df-118">Applications you have custom developed through hello [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="cf2df-119">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="cf2df-119">These include:</span></span>

-   <span data-ttu-id="cf2df-120">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) oturum açma tabanlı</span><span class="sxs-lookup"><span data-stu-id="cf2df-120">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="cf2df-121">[Openıd Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) oturum açma tabanlı</span><span class="sxs-lookup"><span data-stu-id="cf2df-121">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="cf2df-122">[WS-Federasyon 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) oturum açma tabanlı</span><span class="sxs-lookup"><span data-stu-id="cf2df-122">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="cf2df-123">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) oturum açma tabanlı</span><span class="sxs-lookup"><span data-stu-id="cf2df-123">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="cf2df-124">Okuma hello [Azure Active Directory Geliştirici Kılavuzu](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn nasıl bunlar destekleyen toocreate özel geliştirilmiş uygulama tek oturum açma modları hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="cf2df-124">Read hello [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn more about how toocreate a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-tooset-an-applications-single-sign-on-mode"></a><span data-ttu-id="cf2df-125">Tooset bir uygulamanın nasıl tek oturum açma modu</span><span class="sxs-lookup"><span data-stu-id="cf2df-125">How tooset an application’s single sign-on mode</span></span>

<span data-ttu-id="cf2df-126">tooset uygulamaya ait **çoklu oturum açma** modu, aşağıdaki hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="cf2df-126">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="cf2df-127">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="cf2df-127">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="cf2df-128">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="cf2df-128">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cf2df-129">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="cf2df-129">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cf2df-130">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="cf2df-130">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cf2df-131">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="cf2df-131">click **All Applications** tooview a list of all your applications.</span></span>

   * <span data-ttu-id="cf2df-132">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="cf2df-132">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="cf2df-133">Tooconfigure çoklu oturum açma hello uygulamasını seçin</span><span class="sxs-lookup"><span data-stu-id="cf2df-133">Select hello application you want tooconfigure single sign-on</span></span>

7.  <span data-ttu-id="cf2df-134">Merhaba uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="cf2df-134">Once hello application loads, click **Single sign-on** from hello application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf2df-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cf2df-135">Next steps</span></span>
[<span data-ttu-id="cf2df-136">Uygulama proxy'si ile çoklu oturum açma tooyour uygulamaları sağlayın</span><span class="sxs-lookup"><span data-stu-id="cf2df-136">Provide single sign-on tooyour apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

