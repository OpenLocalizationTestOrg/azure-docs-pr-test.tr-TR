---
title: "Azure AD için aaaDevelop uygulamalar | Microsoft Docs"
description: "Hello BT Uzmanı yazılmış, Azure uygulamalarını Active Directory ile tümleştirme için bu makaleyi kılavuz bilgiler verilmektedir."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: 
ms.assetid: dd69f2bc-37c5-457c-857d-27acb84267fb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/07/2017
ms.author: kgremban
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d2924be752af0be2843b1d9b74d9ec446d3fe1ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-line-of-business-apps-for-azure-active-directory"></a><span data-ttu-id="50a54-103">Azure Active Directory için satır iş kolu uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="50a54-103">Develop line-of-business apps for Azure Active Directory</span></span>
<span data-ttu-id="50a54-104">Bu kılavuz, Azure Active Directory (AD) .hello için satır iş kolu (LoB) uygulamaları geliştirme genel bir bakış İzleyici Active Directory/Office 365 genel Yöneticiler amaçlanmıştır sağlar.</span><span class="sxs-lookup"><span data-stu-id="50a54-104">This guide provides an overview of developing line-of-business (LoB) applications for Azure Active Directory (AD).hello intended audience is Active Directory/Office 365 global administrators.</span></span>

## <a name="overview"></a><span data-ttu-id="50a54-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="50a54-105">Overview</span></span>
<span data-ttu-id="50a54-106">Azure AD ile tümleşik uygulamaları oluşturmak, kuruluş çoklu oturum açma Office 365 ile kullanıcılara sağlar.</span><span class="sxs-lookup"><span data-stu-id="50a54-106">Building applications integrated with Azure AD gives users in your organization single sign-on with Office 365.</span></span> <span data-ttu-id="50a54-107">Merhaba uygulaması hello Merhaba uygulaması için kimlik doğrulama ilkesini üzerinden denetim Azure AD sağlar bulundurmak.</span><span class="sxs-lookup"><span data-stu-id="50a54-107">Having hello application in Azure AD gives you control over hello authentication policy for hello application.</span></span> <span data-ttu-id="50a54-108">koşullu erişim ve çok faktörlü kimlik doğrulaması (MFA) tooprotect uygulamalarla nasıl görürüm hakkında daha fazla toolearn [yapılandırma erişim kuralları](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="50a54-108">toolearn more about conditional access and how tooprotect apps with multi-factor authentication (MFA) see [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

<span data-ttu-id="50a54-109">Uygulama toouse Azure Active Directory'ye kaydedin.</span><span class="sxs-lookup"><span data-stu-id="50a54-109">Register your application toouse Azure Active Directory.</span></span> <span data-ttu-id="50a54-110">Merhaba Uygulaması kaydettirilirken, geliştiricilerin Azure AD tooauthenticate kullanıcıları kullanın ve e-posta, Takvim ve belgeler gibi erişim toouser kaynakları isteği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="50a54-110">Registering hello application means that your developers can use Azure AD tooauthenticate users and request access toouser resources such as email, calendar, and documents.</span></span>

<span data-ttu-id="50a54-111">Aksi takdirde olarak bilinen bir uygulama dizininize (Konuklar değil) herhangi bir üyenin kaydedebilirsiniz *uygulama nesnesi oluşturma*.</span><span class="sxs-lookup"><span data-stu-id="50a54-111">Any member of your directory (not guests) can register an application, otherwise known as *creating an application object*.</span></span>

<span data-ttu-id="50a54-112">Uygulama kaydetme hiçbir kullanıcı toodo hello aşağıdakileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="50a54-112">Registering an application allows any user toodo hello following:</span></span>

* <span data-ttu-id="50a54-113">Azure AD tanıdığı kendi uygulama için bir kimlik alma</span><span class="sxs-lookup"><span data-stu-id="50a54-113">Get an identity for their application that Azure AD recognizes</span></span>
* <span data-ttu-id="50a54-114">Edinebileceğinizi veya daha fazla gizli/uygulama hello anahtarları tooAD tooauthenticate kendisini kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="50a54-114">Get one or more secrets/keys that hello application can use tooauthenticate itself tooAD</span></span>
* <span data-ttu-id="50a54-115">Merhaba uygulamada hello Azure portalı özel adı, logosu, vb. ile marka.</span><span class="sxs-lookup"><span data-stu-id="50a54-115">Brand hello application in hello Azure portal with a custom name, logo, etc.</span></span>
* <span data-ttu-id="50a54-116">Azure AD yetkilendirme özellikleri tootheir uygulama geçerli dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="50a54-116">Apply Azure AD authorization features tootheir app, including:</span></span>

  * <span data-ttu-id="50a54-117">Rol Tabanlı Erişim Denetimi (RBAC)</span><span class="sxs-lookup"><span data-stu-id="50a54-117">Role-Based Access Control (RBAC)</span></span>
  * <span data-ttu-id="50a54-118">OAuth yetkilendirme sunucusu olarak Azure Active Directory (Merhaba uygulaması tarafından sunulan bir API güvenli)</span><span class="sxs-lookup"><span data-stu-id="50a54-118">Azure Active Directory as oAuth authorization server (secure an API exposed by hello application)</span></span>
* <span data-ttu-id="50a54-119">Gerekli izinleri hello uygulama toofunction için gerekli dahil olmak üzere, beklendiği gibi bildirin:</span><span class="sxs-lookup"><span data-stu-id="50a54-119">Declare required permissions necessary for hello application toofunction as expected, including:</span></span>

      - <span data-ttu-id="50a54-120">Uygulama izinleri (yalnızca genel Yöneticiler).</span><span class="sxs-lookup"><span data-stu-id="50a54-120">App permissions (global administrators only).</span></span> <span data-ttu-id="50a54-121">Örneğin: başka bir Azure AD uygulama veya rol üyeliğini göreli tooan Azure kaynak, kaynak grubu, rol üyeliğini veya abonelik</span><span class="sxs-lookup"><span data-stu-id="50a54-121">For example: Role membership in another Azure AD application or role membership relative tooan Azure Resource, Resource Group, or Subscription</span></span>
      - <span data-ttu-id="50a54-122">Temsilci izinleri (herhangi bir kullanıcı).</span><span class="sxs-lookup"><span data-stu-id="50a54-122">Delegated permissions (any user).</span></span> <span data-ttu-id="50a54-123">Örneğin: Azure AD oturum açma ve okuma profili</span><span class="sxs-lookup"><span data-stu-id="50a54-123">For example: Azure AD, Sign-in, and Read Profile</span></span>

> [!NOTE]
> <span data-ttu-id="50a54-124">Varsayılan olarak, bir uygulama herhangi bir üyenin kaydedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50a54-124">By default, any member can register an application.</span></span> <span data-ttu-id="50a54-125">uygulamaları toospecific üyeleri kaydettirmek için toorestrict izinleri nasıl görürüm toolearn [tooAzure AD uygulamaları nasıl eklenir](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span><span class="sxs-lookup"><span data-stu-id="50a54-125">toolearn how toorestrict permissions for registering applications toospecific members, see [How applications are added tooAzure AD](develop/active-directory-how-applications-are-added.md#who-has-permission-to-add-applications-to-my-azure-ad-instance).</span></span>
>
>

<span data-ttu-id="50a54-126">Burada hangi, hello genel yönetici, kendi uygulama toodo toohelp geliştiriciler üretime hazır olun:</span><span class="sxs-lookup"><span data-stu-id="50a54-126">Here’s what you, hello global administrator, need toodo toohelp developers make their application ready for production:</span></span>

* <span data-ttu-id="50a54-127">Erişim kuralları (erişim ilkesi/MFA) yapılandırma</span><span class="sxs-lookup"><span data-stu-id="50a54-127">Configure access rules (access policy/MFA)</span></span>
* <span data-ttu-id="50a54-128">Merhaba uygulama toorequire kullanıcı ataması yapılandırın ve kullanıcılar atayın</span><span class="sxs-lookup"><span data-stu-id="50a54-128">Configure hello app toorequire user assignment and assign users</span></span>
* <span data-ttu-id="50a54-129">Merhaba varsayılan kullanıcı onayı deneyimi gösterme</span><span class="sxs-lookup"><span data-stu-id="50a54-129">Suppress hello default user consent experience</span></span>

## <a name="configure-access-rules"></a><span data-ttu-id="50a54-130">Erişim kuralları yapılandırın</span><span class="sxs-lookup"><span data-stu-id="50a54-130">Configure access rules</span></span>
<span data-ttu-id="50a54-131">Uygulama başına erişim kuralları tooyour SaaS uygulamalarını yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="50a54-131">Configure per-application access rules tooyour SaaS apps.</span></span> <span data-ttu-id="50a54-132">Örneğin, MFA gerektirecek veya yalnızca güvenilen ağlarda erişim toousers izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50a54-132">For example, you can require MFA or only allow access toousers on trusted networks.</span></span> <span data-ttu-id="50a54-133">Bu Hello ayrıntılarını hello belgede kullanılabilir [yapılandırma erişim kuralları](active-directory-conditional-access-azuread-connected-apps.md).</span><span class="sxs-lookup"><span data-stu-id="50a54-133">hello details for this are available in hello document [Configuring access rules](active-directory-conditional-access-azuread-connected-apps.md).</span></span>

## <a name="configure-hello-app-toorequire-user-assignment-and-assign-users"></a><span data-ttu-id="50a54-134">Merhaba uygulama toorequire kullanıcı ataması yapılandırın ve kullanıcılar atayın</span><span class="sxs-lookup"><span data-stu-id="50a54-134">Configure hello app toorequire user assignment and assign users</span></span>
<span data-ttu-id="50a54-135">Varsayılan olarak, kullanıcılar atanmadan uygulamalarına erişebilir.</span><span class="sxs-lookup"><span data-stu-id="50a54-135">By default, users can access applications without being assigned.</span></span> <span data-ttu-id="50a54-136">Ancak, hello uygulama rolleri gösterir veya bir kullanıcının erişim panelinde hello uygulama tooappear istiyorsanız, kullanıcı ataması istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="50a54-136">However, if hello application exposes roles or if you want hello application tooappear on a user’s access panel, you should require user assignment.</span></span>

[<span data-ttu-id="50a54-137">Kullanıcı ataması gerektirme</span><span class="sxs-lookup"><span data-stu-id="50a54-137">Requiring user assignment</span></span>](active-directory-applications-guiding-developers-requiring-user-assignment.md)

<span data-ttu-id="50a54-138">Bir Azure AD Premium veya Enterprise Mobility Suite (EMS) abone değilseniz, grupları kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="50a54-138">If you’re an Azure AD Premium or Enterprise Mobility Suite (EMS) subscriber, we strongly recommend using groups.</span></span> <span data-ttu-id="50a54-139">Toohello uygulama grupları atama toodelegate sürekli erişim yönetimi toohello hello grubun sahibi sağlar.</span><span class="sxs-lookup"><span data-stu-id="50a54-139">Assigning groups toohello application allows you toodelegate ongoing access management toohello owner of hello group.</span></span> <span data-ttu-id="50a54-140">Merhaba grubu oluşturun veya Grup Yönetimi özelliğini kullanarak kuruluş toocreate hello grubunuzdaki hello sorumlu taraf isteyin.</span><span class="sxs-lookup"><span data-stu-id="50a54-140">You can create hello group or ask hello responsible party in your organization toocreate hello group using your group management facility.</span></span>

[<span data-ttu-id="50a54-141">Kullanıcıları tooan uygulama atama</span><span class="sxs-lookup"><span data-stu-id="50a54-141">Assigning users tooan application</span></span>](active-directory-applications-guiding-developers-assigning-users.md)  
[<span data-ttu-id="50a54-142">Tooan uygulama grupları atama</span><span class="sxs-lookup"><span data-stu-id="50a54-142">Assigning groups tooan application</span></span>](active-directory-applications-guiding-developers-assigning-groups.md)

## <a name="suppress-user-consent"></a><span data-ttu-id="50a54-143">Kullanıcı izni gösterme</span><span class="sxs-lookup"><span data-stu-id="50a54-143">Suppress user consent</span></span>
<span data-ttu-id="50a54-144">Varsayılan olarak, her kullanıcı onayı deneyimi toosign geçer.</span><span class="sxs-lookup"><span data-stu-id="50a54-144">By default, each user goes through a consent experience toosign in.</span></span> <span data-ttu-id="50a54-145">tooan uygulaması, kullanıcıların toogrant izinleri isteyen hello onayı deneyimi böyle kararları ile ilgili bilginiz kullanıcılar için disconcerting olabilir.</span><span class="sxs-lookup"><span data-stu-id="50a54-145">hello consent experience, asking users toogrant permissions tooan application, can be disconcerting for users who are unfamiliar with making such decisions.</span></span>

<span data-ttu-id="50a54-146">Güvendiğiniz uygulamalar için kuruluşunuz adına onaylıyorsunuz toohello uygulama tarafından hello kullanıcı deneyimi basitleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="50a54-146">For applications that you trust, you can simplify hello user experience by consenting toohello application on behalf of your organization.</span></span>

<span data-ttu-id="50a54-147">Kullanıcı izni ve hello izin hakkında daha fazla bilgi için Azure'da deneyimi, bkz: [Azure Active Directory Tümleştirme uygulamalarla](active-directory-integrating-applications.md).</span><span class="sxs-lookup"><span data-stu-id="50a54-147">For more information about user consent and hello consent experience in Azure, see [Integrating Applications with Azure Active Directory](active-directory-integrating-applications.md).</span></span>

## <a name="related-articles"></a><span data-ttu-id="50a54-148">İlgili makaleler</span><span class="sxs-lookup"><span data-stu-id="50a54-148">Related Articles</span></span>
* [<span data-ttu-id="50a54-149">Azure AD uygulama proxy'si tooon içi uygulamalara güvenli uzaktan erişim etkinleştir</span><span class="sxs-lookup"><span data-stu-id="50a54-149">Enable secure remote access tooon-premises applications with Azure AD Application Proxy</span></span>](active-directory-application-proxy-get-started.md)
* [<span data-ttu-id="50a54-150">SaaS uygulamaları için Azure koşullu erişim önizlemesi</span><span class="sxs-lookup"><span data-stu-id="50a54-150">Azure Conditional Access Preview for SaaS Apps</span></span>](active-directory-conditional-access-azuread-connected-apps.md)
* [<span data-ttu-id="50a54-151">Azure AD ile erişim tooapps yönetme</span><span class="sxs-lookup"><span data-stu-id="50a54-151">Managing access tooapps with Azure AD</span></span>](active-directory-managing-access-to-apps.md)
* [<span data-ttu-id="50a54-152">Azure Active Directory'de Uygulama Yönetimi için Makale Dizini</span><span class="sxs-lookup"><span data-stu-id="50a54-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
