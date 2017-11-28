---
title: "Yeni bir çok kiracılı uygulama aaaHow tooconfigure | Microsoft Docs"
description: "Nasıl tooconfigure tek oturum açma için özel bir uygulama geliştirdiğiniz ve Azure AD ile kaydediliyor."
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
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a><span data-ttu-id="d6f26-103">Nasıl tooconfigure yeni bir çok kiracılı uygulama</span><span class="sxs-lookup"><span data-stu-id="d6f26-103">How tooconfigure a new multi-tenant application</span></span>

<span data-ttu-id="d6f26-104">Federasyon çoklu oturum açma (SSO) uygulamanızda etkinleştirme Openıd Connect, SAML 2.0 ve WS-Fed için Azure AD üzerinden federasyonunu olduğunda otomatik olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d6f26-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="d6f26-105">Son kullanıcılarınızın toosign zaten Azure AD varolan bir oturumla sahip olmasına rağmen karşılaşıyorsanız, uygulamanızı yanlış olasıdır.</span><span class="sxs-lookup"><span data-stu-id="d6f26-105">If your end users are having toosign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="d6f26-106">ADAL/MSAL kullanıyorsanız, olduğundan emin olun **PromptBehavior** çok ayarlamak**otomatik** yerine **her zaman**.</span><span class="sxs-lookup"><span data-stu-id="d6f26-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set too**Auto** rather than **Always**.</span></span>

* <span data-ttu-id="d6f26-107">Bir mobil uygulama oluşturuyorsanız tooenable aracılı veya aracılı olmayan SSO ek yapılandırma gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d6f26-107">If you’re building a mobile app, you may need additional configurations tooenable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="d6f26-108">Android için bkz: [etkinleştirme arası SSO'nun Android içinde](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="d6f26-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="d6f26-109">İOS için bkz: [etkinleştirme arası SSO'nun iOS içinde](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="d6f26-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6f26-110">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d6f26-110">Next steps</span></span>

[<span data-ttu-id="d6f26-111">Azure AD SSO</span><span class="sxs-lookup"><span data-stu-id="d6f26-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="d6f26-112">Uygulama SSO Android içinde çapraz etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="d6f26-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="d6f26-113">Etkinleştirme arası SSO'nun iOS içinde</span><span class="sxs-lookup"><span data-stu-id="d6f26-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="d6f26-114">Uygulamaları tooAzureAD tümleştirme</span><span class="sxs-lookup"><span data-stu-id="d6f26-114">Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="d6f26-115">İzin ve adının Azuread'i v2.0 için uygulamalar Yakınsanan</span><span class="sxs-lookup"><span data-stu-id="d6f26-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="d6f26-116">Azuread'i StackOverflow</span><span class="sxs-lookup"><span data-stu-id="d6f26-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
