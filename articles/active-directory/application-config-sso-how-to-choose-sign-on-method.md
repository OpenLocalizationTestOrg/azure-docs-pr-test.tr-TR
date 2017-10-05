---
title: "Hangi çoklu oturum açma yönteminin kullanılacağını belirleme | Microsoft Docs"
description: "Azure AD tarafından desteklenen tek oturum açma modu anlamak ve hangisinin ilgilendiğiniz uygulama seçmek için seçin."
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
ms.openlocfilehash: 80f4a965920fec9cb578c1bee235c7857f37431e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-determine-what-single-sign-on-method-to-use"></a><span data-ttu-id="cfbe8-103">Hangi çoklu oturum açma yönteminin kullanılacağını belirleme</span><span class="sxs-lookup"><span data-stu-id="cfbe8-103">How to determine what single-sign on method to use</span></span>

<span data-ttu-id="cfbe8-104">Bu makalede, Azure AD tarafından desteklenen tek oturum açma modu anlamanıza yardımcı olmak ve hangisinin ilgilendiğiniz uygulama seçmek için seçin.</span><span class="sxs-lookup"><span data-stu-id="cfbe8-104">This article help you to understand the single sign-on modes supported by Azure AD and how to pick which one to choose for the application you are interested in.</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="cfbe8-105">Çoklu oturum açma ve belirli bir uygulama türleri tarafından desteklenen modları sağlama</span><span class="sxs-lookup"><span data-stu-id="cfbe8-105">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="cfbe8-106">Aşağıdaki tabloda, farklı çoklu oturum açma ve türlerinin her biri yukarıdaki uygulama tarafından desteklenen sağlama modu açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="cfbe8-106">The table below describes the different single sign-on and provisioning modes supported by each of the above application types.</span></span> <span data-ttu-id="cfbe8-107">Belirli bir amaca desteklemek üzere eklemenize gerek hangi uygulamanın anlamanıza yardımcı olması için bu tabloyu kullanın.</span><span class="sxs-lookup"><span data-stu-id="cfbe8-107">You can use this table to help you to understand which application you need to add to support a specific goal.</span></span>

  ![AP türleri tablosu](./media/application-tables/table1.png)

## <a name="how-to-choose-a-single-sign-on-mode"></a><span data-ttu-id="cfbe8-109">Tek bir oturum açma modu seçme</span><span class="sxs-lookup"><span data-stu-id="cfbe8-109">How to choose a single sign-on mode</span></span>

<span data-ttu-id="cfbe8-110">Desteklenen **çoklu oturum açma** modları Azure AD uygulamaları için aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="cfbe8-110">The supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="cfbe8-111">**Azure AD çoklu oturum açma devre dışı özelliğini** – Azure AD çoklu oturum açma devre dışı özelliğini seçin **tek oturum açma modu** , henüz bu uygulama tek oturum açma ile Azure AD ile tümleştirmek hazır değil veya onu yalnızca sınama</span><span class="sxs-lookup"><span data-stu-id="cfbe8-111">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready to integrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="cfbe8-112">**Bağlantılı oturum açma** – seçin [bağlantılı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tek oturum açma modu** mevcut tek oturum açma çözümüyle zaten bağlı olan bir uygulamanız varsa ya da yalnızca basit bir bağlantı, kullanıcılarınızın yayımlamak isterseniz kendi [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) veya [Office 365 uygulama Başlatıcı](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="cfbe8-112">**Linked Sign-on** – choose the [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want to publish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="cfbe8-113">**Parola tabanlı oturum açma** – seçin [parola tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tek oturum açma modu** uygulamanız bir HTML kullanıcı adı ve parola alanı oluşturur ve bu kullanıcı adı ve parola güvenli bir şekilde uygulamayı daha sonra yeniden yürütülmesi depolamak istediğiniz</span><span class="sxs-lookup"><span data-stu-id="cfbe8-113">**Password-based Sign-on** – choose the [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want to store that username and password securely to be replayed to the application later</span></span>

-   <span data-ttu-id="cfbe8-114">**SAML tabanlı oturum açma** – seçin [SAML tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) çoklu oturum açma, uygulamanızın SAML veya Openıd Connect protokollerini destekler veya SAML Taleplerde tanımladığınız kurallar temel alınarak belirli uygulama rollere kullanıcıları eşlemek istiyorsanız modu *(**Not:** uygulama proxy'si bir uygulama için yapılandırıldığında, bu seçenek kullanılamaz) *</span><span class="sxs-lookup"><span data-stu-id="cfbe8-114">**SAML-based Sign-on** – choose the [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports the SAML or OpenID Connect protocols, or you want to be able to map users to specific application roles based on rules you define in your SAML claims *(**Note:** this option is not available when the application proxy is configured for an application)*</span></span>

-   <span data-ttu-id="cfbe8-115">**Üstbilgi tabanlı oturum açma** – bu seçin [üstbilgi tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) HTTP üstbilgisi destekleyen PingAccess kullanan bir uygulamanız varsa, tek oturum açma modu, çoklu oturum açmayı gerçekleştirmek istediğiniz kimlik doğrulaması tabanlı *(**Not:** bu seçenek yalnızca uygulama proxy'si ve PingAccess yapılandırıldığında bir uygulama için kullanılabilir) *</span><span class="sxs-lookup"><span data-stu-id="cfbe8-115">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish to perform single-sign on to *(**Note:** this option is only available when the application proxy and PingAccess is configured for an application)*</span></span>

-   <span data-ttu-id="cfbe8-116">**Tümleşik Windows kimlik doğrulaması** – seçin [tümleşik Windows kimlik doğrulaması](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) çoklu oturum açma çoklu oturum açmayı gerçekleştirmek istediğiniz şirket içi WIA uygulamanın gösterme zaman modu *(**Not:** bu seçenek yalnızca uygulama proxy'si bir uygulama için yapılandırıldığında kullanılabilir) *</span><span class="sxs-lookup"><span data-stu-id="cfbe8-116">**Integrated Windows Authentication** – choose the [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish to perform single-sign on to *(**Note:** this option is only available when the application proxy is configured for an application)*</span></span>

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="cfbe8-117">Özel geliştirilmiş uygulamalar için çoklu oturum açma modları</span><span class="sxs-lookup"><span data-stu-id="cfbe8-117">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="cfbe8-118">Uygulamaları aracılığıyla geliştirilen özel sahip [özel geliştirilmiş uygulama](#_Custom-Developed_Applications) deneyimi de Yukarıda listelenmeyen ek tek oturum açma modunu destekler.</span><span class="sxs-lookup"><span data-stu-id="cfbe8-118">Applications you have custom developed through the [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="cfbe8-119">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="cfbe8-119">These include:</span></span>

-   <span data-ttu-id="cfbe8-120">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) oturum açma tabanlı</span><span class="sxs-lookup"><span data-stu-id="cfbe8-120">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="cfbe8-121">[Openıd Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) oturum açma tabanlı</span><span class="sxs-lookup"><span data-stu-id="cfbe8-121">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="cfbe8-122">[WS-Federasyon 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) oturum açma tabanlı</span><span class="sxs-lookup"><span data-stu-id="cfbe8-122">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="cfbe8-123">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) oturum açma tabanlı</span><span class="sxs-lookup"><span data-stu-id="cfbe8-123">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="cfbe8-124">Okuma [Azure Active Directory Geliştirici Kılavuzu](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) , bu tek oturum açma modunu destekler ve özel geliştirilmiş bir uygulama oluşturma hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="cfbe8-124">Read the [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) to learn more about how to create a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-to-set-an-applications-single-sign-on-mode"></a><span data-ttu-id="cfbe8-125">Oturum açma uygulamanın tek modunu ayarlama</span><span class="sxs-lookup"><span data-stu-id="cfbe8-125">How to set an application’s single sign-on mode</span></span>

<span data-ttu-id="cfbe8-126">Bir uygulamanın ayarlamak için **çoklu oturum açma** modu, aşağıdaki yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="cfbe8-126">To set an application’s **single sign-on** mode, follow the instructions below:</span></span>

1.  <span data-ttu-id="cfbe8-127">Açık [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="cfbe8-127">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="cfbe8-128">Açık **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** ana sol taraftaki gezinti menüsünde sonundaki.</span><span class="sxs-lookup"><span data-stu-id="cfbe8-128">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="cfbe8-129">Yazın **"Azure Active Directory**" Filtre Arama kutusuna seçip **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="cfbe8-129">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="cfbe8-130">tıklatın **kurumsal uygulamalar** Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="cfbe8-130">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="cfbe8-131">tıklatın **tüm uygulamaları** tüm uygulamaların bir listesini görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="cfbe8-131">click **All Applications** to view a list of all your applications.</span></span>

   * <span data-ttu-id="cfbe8-132">Burada gösterisini istediğiniz uygulama görmüyorsanız kullanın **filtre** üst kısmındaki denetim **tüm uygulamalar listesini** ve **Göster** için seçenek **tüm uygulamaları.**</span><span class="sxs-lookup"><span data-stu-id="cfbe8-132">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="cfbe8-133">Çoklu oturum açma yapılandırmak istediğiniz uygulamayı seçin</span><span class="sxs-lookup"><span data-stu-id="cfbe8-133">Select the application you want to configure single sign-on</span></span>

7.  <span data-ttu-id="cfbe8-134">Uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="cfbe8-134">Once the application loads, click **Single sign-on** from the application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfbe8-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cfbe8-135">Next steps</span></span>
[<span data-ttu-id="cfbe8-136">Çoklu oturum açma uygulamalarınızı uygulama proxy'si ile sağlayın.</span><span class="sxs-lookup"><span data-stu-id="cfbe8-136">Provide single sign-on to your apps with Application Proxy</span></span>](active-directory-application-proxy-sso-using-kcd.md)

