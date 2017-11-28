---
title: "hangi uygulamanın uygulama eklerken toouse yazın aaaHow toochoose | Microsoft Docs"
description: "Azure AD ile tümleştirebilir uygulamaları desteklenen hello türlerini anlamanız ve bunların ilgili yapılandırma seçenekleri"
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
ms.openlocfilehash: 46e3672e7f5048b0fa54171f0fc169362c9d5ac6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toochoose-which-application-type-toouse-when-adding-an-application"></a><span data-ttu-id="1d3a2-103">Nasıl toochoose hangi uygulamanın uygulama eklerken toouse yazın</span><span class="sxs-lookup"><span data-stu-id="1d3a2-103">How toochoose which application type toouse when adding an application</span></span>

<span data-ttu-id="1d3a2-104">Bu makalede toounderstand hello dört ana Azure AD ile tümleştirebilirsiniz uygulama türlerini yardımcı:</span><span class="sxs-lookup"><span data-stu-id="1d3a2-104">This article help you toounderstand hello four main types of applications you can integrate with Azure AD:</span></span>

* <span data-ttu-id="1d3a2-105">Bunların her biri tarafından desteklenen özellikler</span><span class="sxs-lookup"><span data-stu-id="1d3a2-105">What is supported by each of them</span></span>
* <span data-ttu-id="1d3a2-106">Hangi uygulamanın neden seçebilirsiniz</span><span class="sxs-lookup"><span data-stu-id="1d3a2-106">Why you might choose which application</span></span>
* <span data-ttu-id="1d3a2-107">Bu uygulamanın çekirdek özellikleri nasıl tooconfigure ister nasıl kullanıcılardır **sağlanan**, veya ne **çoklu oturum açma** teknolojisi toouse.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-107">How tooconfigure those application’s core properties, like how users are **provisioned**, or what **single sign-on** technology toouse.</span></span>

## <a name="supported-application-types-in-azure-ad"></a><span data-ttu-id="1d3a2-108">Azure AD'de desteklenen uygulama türleri</span><span class="sxs-lookup"><span data-stu-id="1d3a2-108">Supported application types in Azure AD</span></span>

<span data-ttu-id="1d3a2-109">Kullanarak ekleyebileceğiniz azure AD destekler dört ana uygulama türleri hello **Ekle** özelliği bulunan altında **kurumsal uygulamalar**.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-109">Azure AD supports four main application types that you can add using hello **Add** feature found under **Enterprise Applications**.</span></span> <span data-ttu-id="1d3a2-110">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="1d3a2-110">These include:</span></span>

-   <span data-ttu-id="1d3a2-111">**Azure AD galeri uygulamaları** – bir tek oturum açma için Azure AD ile önceden tümleştirilmiş uygulama.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-111">**Azure AD Gallery Applications** – An application that has been pre-integrated for single sign-on with Azure AD.</span></span>

-   <span data-ttu-id="1d3a2-112">**Uygulama proxy'si uygulamalar** – tooprovide güvenli çoklu oturum açma tooexternally istediğiniz şirket içi ortamınızda çalışan bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-112">**Application Proxy Applications** – An application running in your on-premises environment that you want tooprovide secure single-sign on tooexternally.</span></span>

-   <span data-ttu-id="1d3a2-113">**Özel geliştirilmiş uygulamaları** – üzerinde toodevelop kuruluşunuz isteyen bir uygulama hello Azure AD uygulama geliştirme platformu, ancak var henüz.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-113">**Custom-developed Applications** – An application that your organization wishes toodevelop on hello Azure AD Application Development Platform, but that may not exist yet.</span></span>

-   <span data-ttu-id="1d3a2-114">**Galeri olmayan uygulamaları** – kendi uygulamalarınızı Getir!</span><span class="sxs-lookup"><span data-stu-id="1d3a2-114">**Non-Gallery Applications** – Bring your own applications!</span></span> <span data-ttu-id="1d3a2-115">İstediğiniz herhangi bir web bağlantıyı ya da bir kullanıcı adı ve parola alanı işleyen herhangi bir uygulama SAML veya Openıd Connect protokollerini destekler veya çoklu oturum açma için Azure AD ile toointegrate istediğiniz SCIM'yi destekler.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-115">Any web link you want, or any application which renders a username and password field, supports SAML or OpenID Connect protocols, or supports SCIM which you wish toointegrate for single sign-on with Azure AD.</span></span>

## <a name="features-and-capabilities-supported-by-all-hello-above-application-types"></a><span data-ttu-id="1d3a2-116">Özellik ve tüm hello uygulama türleri yukarıda tarafından desteklenen yetenekler</span><span class="sxs-lookup"><span data-stu-id="1d3a2-116">Features and capabilities supported by all hello above application types</span></span>

<span data-ttu-id="1d3a2-117">Merhaba aşağıdaki özellikleri 4 uygulama türleri yukarıda hello hiçbiri tarafından Azure AD'de desteklenir:</span><span class="sxs-lookup"><span data-stu-id="1d3a2-117">hello following features are supported by any of hello above 4 application types in Azure AD:</span></span>

-   <span data-ttu-id="1d3a2-118">**Hızlı Başlangıç** – izleyerek bir uygulama ile hızlı bir şekilde yapmalarını [basit dağıtım adımları](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span><span class="sxs-lookup"><span data-stu-id="1d3a2-118">**Quick start** – get going with an application quickly by following [simple deployment steps](https://docs.microsoft.com/azure/active-directory/active-directory-integrating-applications-getting-started)</span></span>

-   <span data-ttu-id="1d3a2-119">**Genel Özellikler Yönetim** – alma bir [doğrudan ayrıntılı bağlantı](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan uygulama [hello marka özelleştirme](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) bir uygulamanın veya [Merhaba uygulamasıdevredışıbırak](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) tüm kullanıcılar için.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-119">**General properties management** – get a [direct deeplink](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#deploying-azure-ad-integrated-applications-to-users) tooan application, [customize hello branding](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-change-app-logo-user-azure-portal) of an application, or [disable hello application](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-disable-app-azure-portal) for all users.</span></span>

-   <span data-ttu-id="1d3a2-120">**Kullanıcı ve Grup Yönetimi** – [atamak](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) veya [kaldırmak](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) kullanıcılar ve gruplar tooan uygulama ve isteğe bağlı olarak bu kullanıcılar ve gruplar erişiminiz Ata hello belirli uygulama rolleri</span><span class="sxs-lookup"><span data-stu-id="1d3a2-120">**User and group management** – [assign](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-assign-user-azure-portal) or [remove](https://docs.microsoft.com/azure/active-directory/active-directory-coreapps-remove-assignment-azure-portal) users and groups tooan application, and optionally assign hello specific application roles these users and groups have access to</span></span>

-   <span data-ttu-id="1d3a2-121">**Self Servis uygulamaya erişim** – kullanıcılar toorequest etkinleştirmek [Self Servis uygulamaya erişim](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) kendi uygulama erişimini tooan uygulamadan paneller ya da bir uygulama doğrudan ekleyerek veya [ Self Servis etkinleştirilmiş gruba katılıyor](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), isteğe bağlı olarak hello boyunca iş onay gerektiren yolu</span><span class="sxs-lookup"><span data-stu-id="1d3a2-121">**Self-service application access** – enable your users toorequest [self-service application access](https://docs.microsoft.com/azure/active-directory/active-directory-self-service-application-access) tooan application from their Application Access Panels either by adding an application directly or [joining a self-service enabled group](https://docs.microsoft.com/azure/active-directory/active-directory-accessmanagement-self-service-group-management), optionally requiring business approval along hello way</span></span>

-   <span data-ttu-id="1d3a2-122">**Oturum açma günlükleri** – bkz [tüm oturum açma işlemleri tooan uygulama hello](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), ya da tüm uygulamalarınızın</span><span class="sxs-lookup"><span data-stu-id="1d3a2-122">**Sign-in logs** – see [all hello sign-ins tooan application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-sign-ins), or all your applications</span></span>

-   <span data-ttu-id="1d3a2-123">**Denetim günlükleri** – bkz [denetim günlüklerini değişiklikler tooan uygulama hakkında ayrıntılı](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), veya tooall uygulamalarınızı</span><span class="sxs-lookup"><span data-stu-id="1d3a2-123">**Audit logs** – see [detailed audit logs about modifications tooan application](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs), or tooall your applications</span></span>

-   <span data-ttu-id="1d3a2-124">**Koşullu ve risk tabanlı erişim** – güçlü ayarlanmış [koşul tabanlı erişim kuralları](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) kullanıcılar toosign tooa belirli uygulamasında çalıştığında uygulanır</span><span class="sxs-lookup"><span data-stu-id="1d3a2-124">**Conditional and risk-based access** – set powerful [condition-based access rules](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access) that are enforced when users attempt toosign in tooa specific application</span></span>

-   <span data-ttu-id="1d3a2-125">**İzinleri Görünüm** – hello hiçbirini görüntülemek [OAuth2 izinleri](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) bir uygulama dizininize erişim tooin, tek bir yerden sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-125">**Permissions view** – view any of hello [OAuth2 permissions](https://docs.microsoft.com/azure/active-directory/active-directory-apps-permissions-consent) an application has access tooin your directory from a single place</span></span>

## <a name="single-sign-on-and-provisioning-modes-supported-by-specific-application-types"></a><span data-ttu-id="1d3a2-126">Çoklu oturum açma ve belirli bir uygulama türleri tarafından desteklenen modları sağlama</span><span class="sxs-lookup"><span data-stu-id="1d3a2-126">Single sign-on and provisioning modes supported by specific application types</span></span>

<span data-ttu-id="1d3a2-127">Merhaba farklı çoklu oturum açma ve her uygulama türleri yukarıda hello tarafından desteklenen modları sağlama Hello tabloda açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-127">hello table below describes hello different single sign-on and provisioning modes supported by each of hello above application types.</span></span> <span data-ttu-id="1d3a2-128">Bu tablo toohelp kullanabileceğiniz hangi uygulamanın gereksinim toounderstand tooadd toosupport belirli bir amaca.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-128">You can use this table toohelp you toounderstand which application you need tooadd toosupport a specific goal.</span></span>

  ![Uygulama türleri tablosu](./media/application-tables/table1.png)

## <a name="how-toochoose-a-single-sign-on-mode"></a><span data-ttu-id="1d3a2-130">Nasıl toochoose tek bir oturum açma modu</span><span class="sxs-lookup"><span data-stu-id="1d3a2-130">How toochoose a single sign-on mode</span></span>

<span data-ttu-id="1d3a2-131">desteklenen hello **çoklu oturum açma** modları Azure AD uygulamaları için aşağıda listelenmiştir.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-131">hello supported **single sign-on** modes for Azure AD applications are listed below.</span></span>

-   <span data-ttu-id="1d3a2-132">**Azure AD çoklu oturum açma devre dışı özelliğini** – Azure AD çoklu oturum açma devre dışı özelliğini seçin **tek oturum açma modu** , çoklu oturum açma ile Azure AD ile henüz hazır değil toointegrate misiniz veya onu yalnızca sınama</span><span class="sxs-lookup"><span data-stu-id="1d3a2-132">**Azure AD single sign-on disabled** – choose Azure AD single sign-on disabled **single sign-on mode** if you are not yet ready toointegrate this application with single sign-on with Azure AD, or are simply testing it out</span></span>

-   <span data-ttu-id="1d3a2-133">**Bağlantılı oturum açma** – hello seçin [bağlantılı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tek oturum açma modu** mevcut tek oturum açma çözümüyle zaten bağlı olan bir uygulamanız varsa ya da yalnızca istiyorsanız Basit bir bağlantı, kullanıcılarınızın toopublish kendi [uygulama erişim Paneli'ne](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) veya [Office 365 uygulama Başlatıcı](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span><span class="sxs-lookup"><span data-stu-id="1d3a2-133">**Linked Sign-on** – choose hello [Linked Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if you have an application that is already connected with an existing single sign-on solution, or if you just want toopublish a simple link for your users in their [Application Access Panel](https://docs.microsoft.com/azure/active-directory/active-directory-saas-access-panel-introduction) or [Office 365 application launcher](https://login.microsoftonline.com/common/oauth2/authorize?response_mode=form_post&response_type=id_token&scope=openid&nonce=d508a995-f6d6-4b8a-81b8-825c71f1be46.636253878097046923&state=https%3a%2f%2fsupport.office.com%2farticle%2fMeet-the-Office-365-app-launcher-79f12104-6fed-442f-96a0-eb089a3f476a%3fui%3den-US%26rs%3den-US%26ad%3dUS&client_id=4b233688-031c-404b-9a80-a4f3f2351f90&redirect_uri=https%3a%2f%2fsupport.office.com%2fauth%2fsignin&login_hint=asteen%40microsoft.com&prompt=none)</span></span>

-   <span data-ttu-id="1d3a2-134">**Parola tabanlı oturum açma** – hello seçin [parola tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **tek oturum açma modu** uygulamanız bir HTML kullanıcı adı ve parola alanı oluşturur ve toostore istiyorsanız, Kullanıcı adı ve parola toobe güvenli bir şekilde yeniden toohello uygulamayı daha sonra</span><span class="sxs-lookup"><span data-stu-id="1d3a2-134">**Password-based Sign-on** – choose hello [Password-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) **single sign-on mode** if your application renders an HTML username and password field and you want toostore that username and password securely toobe replayed toohello application later</span></span>

-   <span data-ttu-id="1d3a2-135">**SAML tabanlı oturum açma** – hello seçin [SAML tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) çoklu oturum açma, uygulamanızın hello SAML veya Openıd Connect protokollerini destekler veya toobe mümkün toomap kullanıcılar isterseniz modu toospecific uygulama rolleri dayalı Talep kuralları, SAML tanımladığınız *</span><span class="sxs-lookup"><span data-stu-id="1d3a2-135">**SAML-based Sign-on** – choose hello [SAML-based Sign-on](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis#how-does-single-sign-on-with-azure-active-directory-work) single-sign on mode if your application supports hello SAML or OpenID Connect protocols, or you want toobe able toomap users toospecific application roles based on rules you define in your SAML claims *</span></span>

   >[!NOTE]
   ><span data-ttu-id="1d3a2-136">Merhaba uygulama proxy'si bir uygulama için yapılandırıldığında, bu seçenek kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-136">This option is not available when hello application proxy is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="1d3a2-137">**Üstbilgi tabanlı oturum açma** – bu seçin [üstbilgi tabanlı oturum açma](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) HTTP üstbilgisi destekleyen PingAccess kullanan bir uygulamanız varsa, tek oturum açma modu temel tooperform çoklu oturum üzerinde çok istediğiniz kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="1d3a2-137">**Header-based Sign-on** – choose this [Header-based Sign-on](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access#what-is-pingaccess-for-azure-ad) single sign-on mode if you have an application using PingAccess that supports HTTP-header based authentication that you wish tooperform single-sign on too</span></span>

   >[!NOTE]
   ><span data-ttu-id="1d3a2-138">Bu seçenek, yalnızca Hello uygulama proxy'si ve PingAccess yapılandırıldığında bir uygulama için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-138">This option is only available when hello application proxy and PingAccess is configured for an application.</span></span>
   >
   >

-   <span data-ttu-id="1d3a2-139">**Tümleşik Windows kimlik doğrulaması** – hello seçin [tümleşik Windows kimlik doğrulaması](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) çoklu oturum açma tooperform çoklu oturum üzerinde çok istediğiniz şirket içi WIA uygulamanın gösterme zaman modu</span><span class="sxs-lookup"><span data-stu-id="1d3a2-139">**Integrated Windows Authentication** – choose hello [Integrated Windows Authentication](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) single-sign on mode when exposing an on-premises WIA application that you wish tooperform single-sign on too</span></span>

   >[!NOTE]
   ><span data-ttu-id="1d3a2-140">Bu seçenek, yalnızca Hello uygulama proxy'si bir uygulama için yapılandırıldığında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-140">This option is only available when hello application proxy is configured for an application.</span></span>
   >
   >

## <a name="single-sign-on-modes-for-custom-developed-applications"></a><span data-ttu-id="1d3a2-141">Özel geliştirilmiş uygulamalar için çoklu oturum açma modları</span><span class="sxs-lookup"><span data-stu-id="1d3a2-141">Single sign-on modes for custom-developed applications</span></span>

<span data-ttu-id="1d3a2-142">Uygulamaları hello geliştirilen özel sahip [özel geliştirilmiş uygulama](#_Custom-Developed_Applications) deneyimi de Yukarıda listelenmeyen ek tek oturum açma modunu destekler.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-142">Applications you have custom developed through hello [Custom-developed application](#_Custom-Developed_Applications) experience also support additional single sign-on modes not listed above.</span></span> <span data-ttu-id="1d3a2-143">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="1d3a2-143">These include:</span></span>

-   <span data-ttu-id="1d3a2-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) oturum açma tabanlı</span><span class="sxs-lookup"><span data-stu-id="1d3a2-144">[OAuth 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code) based sign-on</span></span>

-   <span data-ttu-id="1d3a2-145">[Openıd Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) oturum açma tabanlı</span><span class="sxs-lookup"><span data-stu-id="1d3a2-145">[OpenID Connect 1.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-openid-connect-code) based sign-on</span></span>

-   <span data-ttu-id="1d3a2-146">[WS-Federasyon 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) oturum açma tabanlı</span><span class="sxs-lookup"><span data-stu-id="1d3a2-146">[WS-Federation 1.2](http://docs.oasis-open.org/wsfed/federation/v1.2/os/ws-federation-1.2-spec-os.html) based sign-on</span></span>

-   <span data-ttu-id="1d3a2-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) oturum açma tabanlı</span><span class="sxs-lookup"><span data-stu-id="1d3a2-147">[SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) based sign-on</span></span>

<span data-ttu-id="1d3a2-148">Okuma hello [Azure Active Directory Geliştirici Kılavuzu](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn nasıl bunlar destekleyen toocreate özel geliştirilmiş uygulama tek oturum açma modları hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-148">Read hello [Azure Active Directory developer’s guide](https://docs.microsoft.com/azure/active-directory/develop/active-directory-developers-guide) toolearn more about how toocreate a custom-developed application which supports these single sign-on modes.</span></span>

## <a name="how-tooset-an-applications-single-sign-on-mode"></a><span data-ttu-id="1d3a2-149">Tooset bir uygulamanın nasıl tek oturum açma modu</span><span class="sxs-lookup"><span data-stu-id="1d3a2-149">How tooset an application’s single sign-on mode</span></span>

<span data-ttu-id="1d3a2-150">tooset uygulamaya ait **çoklu oturum açma** modu, aşağıdaki hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="1d3a2-150">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="1d3a2-151">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="1d3a2-151">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1d3a2-152">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-152">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d3a2-153">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-153">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d3a2-154">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-154">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1d3a2-155">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-155">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1d3a2-156">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="1d3a2-156">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1d3a2-157">Tooconfigure çoklu oturum açma istediğiniz hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-157">Select hello application for which you want tooconfigure single sign-on.</span></span>

7.  <span data-ttu-id="1d3a2-158">Merhaba uygulamanın yüklediği sonra tıklayın **çoklu oturum açma** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-158">Once hello application loads, click **Single sign-on** from hello application’s left hand navigation menu.</span></span>

## <a name="how-toochoose-a-provisioning-mode"></a><span data-ttu-id="1d3a2-159">Nasıl toochoose sağlama modu</span><span class="sxs-lookup"><span data-stu-id="1d3a2-159">How toochoose a provisioning mode</span></span>

-   <span data-ttu-id="1d3a2-160">**El ile sağlama** – hello seçin [el ile](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) hazırlama modu var olan hesapları varsa veya bu uygulamaları Azure AD dışında toomanage hesabı istiyor.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-160">**Manual Provisioning** – choose hello [Manual](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#provisioning-modes) provisioning mode if you have existing accounts, or wish toomanage accounts for this application outside of Azure AD.</span></span>

-   <span data-ttu-id="1d3a2-161">**Otomatik sağlama** – hello seçin [otomatik](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **sağlama modu** API tabanlı tooenable otomatik sağlama ve/veya XML'deki sağlanmasını istiyorsanız toothis kullanıcı hesapları Uygulama</span><span class="sxs-lookup"><span data-stu-id="1d3a2-161">**Automatic Provisioning** – choose hello [Automatic](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-provisioning#configuring-automatic-user-account-provisioning) **provisioning mode** if you want tooenable automatic API-based provisioning and/or de-provisioning of user accounts toothis application</span></span> 

   >[!NOTE]
   ><span data-ttu-id="1d3a2-162">Bu seçenek yalnızca hello içinde uygulamaları için kullanılabilir **öne çıkan** hello kategorisini [Azure AD uygulama galerisinde](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span><span class="sxs-lookup"><span data-stu-id="1d3a2-162">This option is available only for applications within hello **featured** category of hello [Azure AD Application Gallery](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-whats-new-azure-portal#the-new-and-improved-application-gallery).</span></span>
   >
   >

-   <span data-ttu-id="1d3a2-163">**Otomatik sağlama SCIM'yi tabanlı** – kullanmak [SCIM'yi tabanlı otomatik sağlamayı](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) değişiklikleri toousers ve değişiklikleri otomatik olarak gösterilen grupları algılamak için uygulamanızın hello SCIM'yi Protokolü destekliyorsa Azure AD ile tümleşik tooany uygulama</span><span class="sxs-lookup"><span data-stu-id="1d3a2-163">**SCIM-based Automatic Provisioning** – use [SCIM-based Automatic Provisioning](https://docs.microsoft.com/azure/active-directory/active-directory-scim-provisioning) if your application supports hello SCIM protocol for detecting changes toousers and groups, which are automatically emitted for changes tooany application integrated with Azure AD</span></span> 

   >[!NOTE]
   ><span data-ttu-id="1d3a2-164">Bu seçenek, belirli bir sağlama modu olarak listelenmez, ancak Azure AD ile tümleşik tüm uygulamalar için varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-164">This option is not listed as a specific provisioning mode, but is enabled by default for all applications that are integrated with Azure AD.</span></span>
   >
   >

## <a name="how-tooset-an-applications-provisioning-mode"></a><span data-ttu-id="1d3a2-165">Nasıl tooset bir uygulama sağlama modunda</span><span class="sxs-lookup"><span data-stu-id="1d3a2-165">How tooset an application’s provisioning mode</span></span>

<span data-ttu-id="1d3a2-166">tooset uygulamaya ait **sağlama** modu, aşağıdaki hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="1d3a2-166">tooset an application’s **provisioning** mode, follow hello instructions below:</span></span>

<span data-ttu-id="1d3a2-167">tooset uygulamaya ait **çoklu oturum açma** modu, aşağıdaki hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="1d3a2-167">tooset an application’s **single sign-on** mode, follow hello instructions below:</span></span>

1.  <span data-ttu-id="1d3a2-168">Açık hello [ **Azure Portal** ](https://portal.azure.com/) olarak oturum açın ve bir **genel yönetici** veya **ortak yönetici**</span><span class="sxs-lookup"><span data-stu-id="1d3a2-168">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator** or **Co-admin.**</span></span>

2.  <span data-ttu-id="1d3a2-169">Açık hello **Azure Active Directory uzantısını** tıklayarak **daha fazla hizmet** hello ana sol taraftaki gezinti menüsünde hello sonundaki.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-169">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="1d3a2-170">Yazın **"Azure Active Directory**" Merhaba filtre arama kutusunda ve select hello **Azure Active Directory** öğesi.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-170">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="1d3a2-171">Tıklatın **kurumsal uygulamalar** hello Azure Active Directory sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-171">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="1d3a2-172">Tıklatın **tüm uygulamaları** tooview tüm uygulamalarınızın listesi.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-172">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="1d3a2-173">Burada göstermek istediğiniz Merhaba uygulaması görmüyorsanız hello kullan **filtre** denetim hello hello üstündeki **tüm uygulamalar listesini** ve kümesi hello **Göster** çok seçenek **Tüm uygulamalar.**</span><span class="sxs-lookup"><span data-stu-id="1d3a2-173">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="1d3a2-174">Tooconfigure sağlama istediğiniz hello uygulaması'nı seçin.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-174">Select hello application for which you want tooconfigure provisioning.</span></span>

7.  <span data-ttu-id="1d3a2-175">Merhaba uygulamanın yüklediği sonra tıklayın **sağlama** hello uygulamanın sol taraftaki gezinti menüsünde.</span><span class="sxs-lookup"><span data-stu-id="1d3a2-175">Once hello application loads, click **Provisioning** from hello application’s left hand navigation menu.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1d3a2-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1d3a2-176">Next steps</span></span>
[<span data-ttu-id="1d3a2-177">Azure Active Directory ile uygulamaları yönetme</span><span class="sxs-lookup"><span data-stu-id="1d3a2-177">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
