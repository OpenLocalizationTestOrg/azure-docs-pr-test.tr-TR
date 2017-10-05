---
title: "Azure AD uygulama galerisinde için çok kiracılı uygulama ekleme | Microsoft Docs"
description: "Özel geliştirilen çok kiracılı uygulamanızı Azure AD uygulama galerisinde nasıl listeleyebilirsiniz açıklar"
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
ms.openlocfilehash: 208f0d40bd7a8e8f35f16e1fcb09c305d833dbb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-add-a-multi-tenant-application-to-the-azure-ad-application-gallery"></a><span data-ttu-id="ebba9-103">Azure AD uygulama galerisinde çok kiracılı uygulamaya ekleme</span><span class="sxs-lookup"><span data-stu-id="ebba9-103">How to add a multi-tenant application to the Azure AD application gallery</span></span>

## <a name="what-is-the-azure-ad-application-gallery"></a><span data-ttu-id="ebba9-104">Azure AD uygulama galerisinde nedir?</span><span class="sxs-lookup"><span data-stu-id="ebba9-104">What is the Azure AD Application Gallery?</span></span>

<span data-ttu-id="ebba9-105">Azure AD uygulama galerisinde uygulamanızı Azure Active Directory müşterilerin etkisi genişletmek ve uygulamanızın Market'te ulaşmak için tüm milyonlarca önünde almak için harika bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="ebba9-105">The Azure AD Application Gallery is a great way to get your application in front of all the millions of Azure Active Directory customers to broaden the impact and reach of your application in the marketplace.</span></span> <span data-ttu-id="ebba9-106">Uygulamanızı Azure AD uygulama galerisinde nasıl listesinde aşağıdaki adımları açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ebba9-106">The below steps explain how you can list your application in the Azure AD Application Gallery.</span></span>

## <a name="if-your-application-supports-saml-or-openidconnect"></a><span data-ttu-id="ebba9-107">SAML veya Openıdconnect uygulamanız destekliyorsa</span><span class="sxs-lookup"><span data-stu-id="ebba9-107">If your application supports SAML or OpenIDConnect</span></span>
<span data-ttu-id="ebba9-108">Azure AD uygulama galerisinde listelemek istediğiniz bir çok kiracılı uygulamanız varsa, ilk uygulamanızı aşağıdaki tek oturum açma teknolojileri birini destekleyen emin olmalısınız:</span><span class="sxs-lookup"><span data-stu-id="ebba9-108">If you have a multi-tenant application you'd like to list in the Azure AD Application Gallery, you must first make sure that your application supports one of the following single sign-on technologies:</span></span>

1. <span data-ttu-id="ebba9-109">**Openıd Connect** -Openıd Connect kimlik doğrulaması ve Azure AD API yapılandırmasını onayı için kullanarak Azure AD ile doğrudan tümleştirme.</span><span class="sxs-lookup"><span data-stu-id="ebba9-109">**OpenID Connect** - Direct integration with Azure AD using OpenID Connect for authentication and the Azure AD consent API for configuration.</span></span> <span data-ttu-id="ebba9-110">Uygulamanızı SAML desteklemez ve yalnızca bir tümleştirme başlıyorsanız, ardından öneri modu budur.</span><span class="sxs-lookup"><span data-stu-id="ebba9-110">If you are just starting an integration and your application does not support SAML, then this is the recommend mode.</span></span>
2. <span data-ttu-id="ebba9-111">**SAML** – üçüncü taraf kimlik sağlayıcıları SAML protokolü kullanarak yapılandırma yeteneğini uygulamanız zaten sahip.</span><span class="sxs-lookup"><span data-stu-id="ebba9-111">**SAML** – Your application already has the ability to configure third-party identity providers using the SAML protocol.</span></span>

<span data-ttu-id="ebba9-112">Bu tek oturum açma modlarından birini uygulamanız destekliyorsa ve çok kiracılı uygulamanızı Azure AD uygulama galerisinde listelemek istediğiniz, belgede yer alan adımlar izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ebba9-112">If your application supports one of these single sign-on modes and you'd like to list your multi-tenant application in the Azure AD Application Gallery, you can follow the steps in the document below.</span></span> <span data-ttu-id="ebba9-113">Hızlıca başlamak için bir e-posta Gönder  **waadpartners@microsoft.com** .</span><span class="sxs-lookup"><span data-stu-id="ebba9-113">To get started quickly send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="if-your-application-does-not-support-saml-or-openidconnect"></a><span data-ttu-id="ebba9-114">Uygulamanızı SAML veya Openıdconnect desteklemiyorsa</span><span class="sxs-lookup"><span data-stu-id="ebba9-114">If your application does not support SAML or OpenIDConnect</span></span>
<span data-ttu-id="ebba9-115">Uygulamanız bu modlarından birini bile desteklemiyorsa, biz yine bizim parola çoklu oturum açma teknolojisini kullanarak bizim Galerisine tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ebba9-115">Even if your application does not support one of these modes, we can still integrate it into our gallery using our Password Single Sign-on technology.</span></span> <span data-ttu-id="ebba9-116">Bu seçenek keşfetmek isterseniz, e-posta gönderebilirsiniz  **waadpartners@microsoft.com** .</span><span class="sxs-lookup"><span data-stu-id="ebba9-116">If you'd like to explore this option, you can send an email to **waadpartners@microsoft.com**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebba9-117">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ebba9-117">Next steps</span></span>
[<span data-ttu-id="ebba9-118">Uygulamanız Azure Active Directory Uygulama galerisinde listelemek nasıl</span><span class="sxs-lookup"><span data-stu-id="ebba9-118">How to list your application in the Azure Active Directory application gallery</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-app-gallery-listing)
