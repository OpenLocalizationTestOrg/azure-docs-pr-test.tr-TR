---
title: "aaaHow tooadd çok kiracılı uygulama toohello Azure AD uygulama Galerisi'ni | Microsoft Docs"
description: "Özel geliştirilen çok kiracılı uygulamanızda hello Azure AD uygulama galerisinde nasıl listeleyebilirsiniz açıklar"
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
ms.openlocfilehash: 2dc6e0d783835d2639a7e6dda172110ee860a977
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-a-multi-tenant-application-toohello-azure-ad-application-gallery"></a><span data-ttu-id="69fe9-103">Nasıl tooadd çok kiracılı uygulama toohello Azure AD uygulama Galerisi</span><span class="sxs-lookup"><span data-stu-id="69fe9-103">How tooadd a multi-tenant application toohello Azure AD application gallery</span></span>

## <a name="what-is-hello-azure-ad-application-gallery"></a><span data-ttu-id="69fe9-104">Hello Azure AD uygulama galerisinde nedir?</span><span class="sxs-lookup"><span data-stu-id="69fe9-104">What is hello Azure AD Application Gallery?</span></span>

<span data-ttu-id="69fe9-105">Hello Azure AD uygulama galerisinde mükemmel şekilde tooget tüm hello milyonlarca önünde uygulamanızı Azure Active Directory müşteriler toobroaden hello etkisi olan ve uygulamanızın hello Market ulaşılırsa.</span><span class="sxs-lookup"><span data-stu-id="69fe9-105">hello Azure AD Application Gallery is a great way tooget your application in front of all hello millions of Azure Active Directory customers toobroaden hello impact and reach of your application in hello marketplace.</span></span> <span data-ttu-id="69fe9-106">Aşağıdaki adımları Hello açıklayan hello Azure AD uygulama galerisinde uygulamanızı nasıl listeleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69fe9-106">hello below steps explain how you can list your application in hello Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="69fe9-107">SAML veya Openıdconnect uygulamanız destekliyorsa</span><span class="sxs-lookup"><span data-stu-id="69fe9-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="69fe9-108">Hello Azure AD uygulama galerisinde toolist istediğiniz bir çok kiracılı uygulamanız varsa, ilk uygulamanızı tek oturum açma teknolojileri aşağıdaki hello birini destekleyen emin olmalısınız:</span><span class="sxs-lookup"><span data-stu-id="69fe9-108">If you have a multi-tenant application you'd like toolist in hello Azure AD Application Gallery, you must first make sure that your application supports one of hello following single sign-on technologies:</span></span>

1. <span data-ttu-id="69fe9-109">**Openıd Connect** - Openıd Connect kimlik doğrulamasını kullanan Azure AD ile tümleştirme doğrudan ve yapılandırması için Azure AD onay API hello.</span><span class="sxs-lookup"><span data-stu-id="69fe9-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and hello Azure AD consent API for configuration.</span></span> <span data-ttu-id="69fe9-110">Uygulamanızı SAML desteklemez ve yalnızca bir tümleştirme başlıyorsanız, ardından hello öneri modu budur.</span><span class="sxs-lookup"><span data-stu-id="69fe9-110">If you are just starting an integration and your application does not support SAML, then this is hello recommend mode.</span></span>
2. <span data-ttu-id="69fe9-111">**SAML** – hello özelliği tooconfigure üçüncü taraf kimlik sağlayıcıları hello SAML protokolü kullanarak uygulamanızı zaten sahiptir.</span><span class="sxs-lookup"><span data-stu-id="69fe9-111">**SAML** – Your application already has hello ability tooconfigure third-party identity providers using hello SAML protocol.</span></span>

<span data-ttu-id="69fe9-112">Uygulamanız bu tek oturum açma modlarından birini destekler ve toolist istiyorsanız çok kiracılı uygulamanızda hello Azure AD uygulama galerisinde, hello belgedeki hello adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69fe9-112">If your application supports one of these single sign-on modes and you'd like toolist your multi-tenant application in hello Azure AD Application Gallery, you can follow hello steps in hello document below.</span></span> <span data-ttu-id="69fe9-113">hızlı şekilde kullanmaya tooget Gönder bir e-posta çok**waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="69fe9-113">tooget started quickly send an email too**waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="69fe9-114">Uygulamanızı SAML veya Openıdconnect desteklemiyorsa</span><span class="sxs-lookup"><span data-stu-id="69fe9-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="69fe9-115">Uygulamanız bu modlarından birini bile desteklemiyorsa, biz yine bizim parola çoklu oturum açma teknolojisini kullanarak bizim Galerisine tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69fe9-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="69fe9-116">Tooexplore istiyorsanız bu seçeneği, bir e-posta çok gönderebilirsiniz**waadpartners@microsoft.com**.</span><span class="sxs-lookup"><span data-stu-id="69fe9-116">If you'd like tooexplore this option, you can send an email too**waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69fe9-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="69fe9-117">Next steps</span></span>
[<span data-ttu-id="69fe9-118">Nasıl toolist hello Azure Active Directory Uygulama galerisinde uygulamanızı</span><span class="sxs-lookup"><span data-stu-id="69fe9-118">How toolist your application in hello Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
