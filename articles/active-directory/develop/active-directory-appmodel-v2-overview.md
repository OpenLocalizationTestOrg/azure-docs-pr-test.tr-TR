---
title: "aaaAzure Active Directory v2.0 uç | Microsoft Docs"
description: "Bir giriş toobuilding uygulamalarla Microsoft Account ve Azure Active Directory oturum açma."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="7b20c-103">Oturum açma Microsoft Account & Azure AD kullanıcıların tek bir uygulamada</span><span class="sxs-lookup"><span data-stu-id="7b20c-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="7b20c-104">Merhaba geçmiş, hem kişisel Microsoft hesaplarını toosupport isteyen bir uygulama geliştiricisi olarak ve Azure Active Directory iş hesaplarından iki ayrı sistemleriyle gerekli toointegrate.</span><span class="sxs-lookup"><span data-stu-id="7b20c-104">In hello past, an app developer who wanted toosupport both personal Microsoft accounts and work accounts from Azure Active Directory was required toointegrate with two separate systems.</span></span>  <span data-ttu-id="7b20c-105">Merhaba **Azure AD v2.0 uç** her iki türdeki bir basit tümleştirmesi kullanılarak hesaba toosign sağlayan yeni bir kimlik doğrulaması API Sürüm tanıtır.</span><span class="sxs-lookup"><span data-stu-id="7b20c-105">hello **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you toosign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="7b20c-106">Merhaba v2.0 uç noktası kullanan uygulamalar hello REST API'lerini de tüketebileceği [Microsoft Graph](https://graph.microsoft.io) ya da türde bir hesabı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7b20c-106">Apps that use hello v2.0 endpoint can also consume REST APIs from hello [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="7b20c-107">Başlarken</span><span class="sxs-lookup"><span data-stu-id="7b20c-107">Getting Started</span></span>
<span data-ttu-id="7b20c-108">En sevdiğiniz platformu listesi toobuild aşağıdaki hello bizim açık kaynak kitaplıkları ve çerçevelerini kullanarak bir uygulama seçin.</span><span class="sxs-lookup"><span data-stu-id="7b20c-108">Choose your favorite platform from hello following list toobuild an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="7b20c-109">Alternatif olarak, bizim OAuth 2.0 & Openıd Connect Protokolü belgeleri toosend kullanmak & protokol iletilerini doğrudan bir kimlik doğrulama kitaplığı kullanmadan alırsınız.</span><span class="sxs-lookup"><span data-stu-id="7b20c-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation toosend & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="7b20c-110">Yenilikler</span><span class="sxs-lookup"><span data-stu-id="7b20c-110">What's New</span></span>
<span data-ttu-id="7b20c-111">Buraya Hello bilgileri nedir ve ne hello v2.0 uç noktası ile mümkün olmayan anlamak yararlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7b20c-111">hello information here will be useful in understanding what is & what isn't possible with hello v2.0 endpoint.</span></span>

* <span data-ttu-id="7b20c-112">Merhaba hakkında bilgi edinin [yapı hello v2.0 uç noktası ile uygulama türleri](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="7b20c-112">Learn about hello [types of apps you can build with hello v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="7b20c-113">Merhaba anlamak [sınırlamalar, sınırlamaları ve kısıtlamaları](active-directory-v2-limitations.md) hello v2.0 uç noktası ile.</span><span class="sxs-lookup"><span data-stu-id="7b20c-113">Understand hello [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with hello v2.0 endpoint.</span></span>
* <span data-ttu-id="7b20c-114">Bu genel bakış videosu hello v2.0 uç noktası için gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="7b20c-114">Check out this overview video for hello v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="7b20c-115">Başvuru</span><span class="sxs-lookup"><span data-stu-id="7b20c-115">Reference</span></span>
<span data-ttu-id="7b20c-116">Bu bağlantılar hello platform derinlemesine keşfetmek için kullanışlıdır:</span><span class="sxs-lookup"><span data-stu-id="7b20c-116">These links will be useful for exploring hello platform in depth:</span></span>

* [<span data-ttu-id="7b20c-117">v2.0 protokol başvurusu</span><span class="sxs-lookup"><span data-stu-id="7b20c-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="7b20c-118">v2.0 belirteç başvurusu</span><span class="sxs-lookup"><span data-stu-id="7b20c-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="7b20c-119">v2.0 Kitaplığı Başvurusu</span><span class="sxs-lookup"><span data-stu-id="7b20c-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="7b20c-120">Kapsamlar ve hello v2.0 uç onayı</span><span class="sxs-lookup"><span data-stu-id="7b20c-120">Scopes and Consent in hello v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="7b20c-121">Merhaba Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="7b20c-121">hello Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="7b20c-122">Yardım ve Destek</span><span class="sxs-lookup"><span data-stu-id="7b20c-122">Help & Support</span></span>
<span data-ttu-id="7b20c-123">Azure Active Directory üzerinde geliştirme hello en iyi yerler tooget Yardım bunlar.</span><span class="sxs-lookup"><span data-stu-id="7b20c-123">These are hello best places tooget help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="7b20c-124">Stack Overflow’da `azure-active-directory` ve `adal` etiketleri</span><span class="sxs-lookup"><span data-stu-id="7b20c-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="7b20c-125">Azure Active Directory geri bildirimleri</span><span class="sxs-lookup"><span data-stu-id="7b20c-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="7b20c-126">Yalnızca iş ve Okul hesapları Azure Active Directory'den toosign gereksiniminiz varsa, ile başlamalı bizim [Azure AD Geliştirici Kılavuzu](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="7b20c-126">If you only need toosign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="7b20c-127">Merhaba v2.0 uç toosign Microsoft Kişisel hesaplarında açıkça isteyen geliştiriciler tarafından kullanılmaya yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="7b20c-127">hello v2.0 endpoint is intended for use by developers who explicitly need toosign in Microsoft personal accounts.</span></span>

