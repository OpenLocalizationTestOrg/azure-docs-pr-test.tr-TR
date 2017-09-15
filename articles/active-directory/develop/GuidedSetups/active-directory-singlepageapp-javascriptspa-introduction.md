---
title: "Azure AD v2 JS SPA destekli Kurulumu - giriş | Microsoft Docs"
description: "JavaScript SPA uygulamaları Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 3d195d0d67f8f82c9450ffd93767917698addee3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="call-the-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="9166a-103">Bir JavaScript tek sayfa uygulama (SPA) Microsoft Graph API çağrısı</span><span class="sxs-lookup"><span data-stu-id="9166a-103">Call the Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="9166a-104">Bu kılavuz bir JavaScript tek sayfa uygulama (SPA) kişisel, iş ne kaydolabilirsiniz gösterir ve Okul hesapları, erişim belirteci almak ve Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren diğer API'leri çağırın.</span><span class="sxs-lookup"><span data-stu-id="9166a-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call the Microsoft Graph API or other APIs that require access tokens from the Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="9166a-105">Bu kılavuz nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="9166a-105">How this guide works</span></span>

![Bu kılavuz tarafından oluşturulan örnek uygulaması nasıl çalışır](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="9166a-107">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="9166a-107">More Information</span></span>

<span data-ttu-id="9166a-108">Bu kılavuz tarafından oluşturulan örnek uygulamayı Microsoft Graph API veya Azure Active Directory v2 uç noktasından belirteçleri kabul eder bir Web API sorgulamak bir JavaScript SPA sağlar.</span><span class="sxs-lookup"><span data-stu-id="9166a-108">The sample application created by this guide enables a JavaScript SPA to query the Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="9166a-109">Bir kullanıcı oturum açtığında, sonra bu senaryo için bir erişim belirteci istenen ve HTTP isteklerini authorization üstbilgisi yoluyla eklenir.</span><span class="sxs-lookup"><span data-stu-id="9166a-109">For this scenario, after a user signs-in, an access token is requested and added to HTTP requests via the authorization header.</span></span> <span data-ttu-id="9166a-110">Belirteç edinme ve yenileme Microsoft kimlik doğrulama kitaplığı (MSAL) tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="9166a-110">Token acquisition and renewal are handled by the Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="9166a-111">Kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="9166a-111">Libraries</span></span>

<span data-ttu-id="9166a-112">Bu kılavuz aşağıdaki kitaplığı kullanır:</span><span class="sxs-lookup"><span data-stu-id="9166a-112">This guide uses the following library:</span></span>

|<span data-ttu-id="9166a-113">Kitaplık</span><span class="sxs-lookup"><span data-stu-id="9166a-113">Library</span></span>|<span data-ttu-id="9166a-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9166a-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="9166a-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="9166a-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="9166a-116">JavaScript Önizleme için Microsoft kimlik doğrulama kitaplığı</span><span class="sxs-lookup"><span data-stu-id="9166a-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="9166a-117">*msal.js* hedefleri *Azure Active Directory v2 endpoint* -oturum açmak ve belirteçleri almak kişisel ve iş, okul hesapları sağlar.</span><span class="sxs-lookup"><span data-stu-id="9166a-117">*msal.js* targets the *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts to sign in and acquire tokens.</span></span> <span data-ttu-id="9166a-118">*Azure Active Directory v2 endpoint* sahip [bazı sınırlamalar](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="9166a-118">The *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="9166a-119">Yalnızca iş ve Okul hesapları ilgileniyorsanız kullanmak *adal.js* ve *V1 endpoint*.</span><span class="sxs-lookup"><span data-stu-id="9166a-119">If you are interested only in school and work accounts, use *adal.js* and the *V1 endpoint*.</span></span> <span data-ttu-id="9166a-120">Okuma v1 ve v2 uç noktaları arasındaki farkları anlamak için [v1 v2 karşılaştırma](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="9166a-120">To understand differences between the v1 and v2 endpoints read the [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
