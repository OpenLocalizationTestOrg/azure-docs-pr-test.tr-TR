---
title: "aaaAzure AD v2 JS SPA destekli Kurulumu - giriş | Microsoft Docs"
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
ms.openlocfilehash: 7e4250ccca837a17489a99603da167009cc2e3d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-javascript-single-page-application-spa"></a><span data-ttu-id="def9a-103">Çağrı hello Microsoft Graph API öğesinden bir JavaScript tek sayfa uygulama (SPA)</span><span class="sxs-lookup"><span data-stu-id="def9a-103">Call hello Microsoft Graph API from a JavaScript Single Page Application (SPA)</span></span>

<span data-ttu-id="def9a-104">Bu kılavuz bir JavaScript tek sayfa uygulama (SPA) kişisel, iş ne kaydolabilirsiniz gösterir ve Okul hesapları, erişim belirteci almak ve hello Microsoft Graph API çağrısı veya Azure Active Directory v2 endpoint gelen erişim belirteçleri gerektiren diğer API'leri hello.</span><span class="sxs-lookup"><span data-stu-id="def9a-104">This guide demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call hello Microsoft Graph API or other APIs that require access tokens from hello Azure Active Directory v2 endpoint.</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="def9a-105">Bu kılavuz nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="def9a-105">How this guide works</span></span>

![Bu kılavuz tarafından oluşturulan hello örnek uygulaması nasıl çalışır](media/active-directory-singlepageapp-javascriptspa-introduction/javascriptspa-intro.png)

<!--start-collapse-->
### <a name="more-information"></a><span data-ttu-id="def9a-107">Daha Fazla Bilgi</span><span class="sxs-lookup"><span data-stu-id="def9a-107">More Information</span></span>

<span data-ttu-id="def9a-108">Bu kılavuz tarafından oluşturulan Merhaba örnek uygulaması JavaScript SPA tooquery hello Microsoft Graph API veya Azure Active Directory v2 uç noktasından belirteçleri kabul eder bir Web API sağlar.</span><span class="sxs-lookup"><span data-stu-id="def9a-108">hello sample application created by this guide enables a JavaScript SPA tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="def9a-109">Bu senaryoda, sonra bir kullanıcı oturum açtığında, bir erişim belirteci hello authorization üstbilgisi aracılığıyla istenen ve eklenen tooHTTP isteği sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="def9a-109">For this scenario, after a user signs-in, an access token is requested and added tooHTTP requests via hello authorization header.</span></span> <span data-ttu-id="def9a-110">Belirteç edinme ve yenileme hello Microsoft kimlik doğrulama kitaplığı (MSAL) tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="def9a-110">Token acquisition and renewal are handled by hello Microsoft Authentication Library (MSAL).</span></span>

<!--end-collapse-->

<!--start-collapse-->
### <a name="libraries"></a><span data-ttu-id="def9a-111">Kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="def9a-111">Libraries</span></span>

<span data-ttu-id="def9a-112">Bu kılavuz kitaplığı aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="def9a-112">This guide uses hello following library:</span></span>

|<span data-ttu-id="def9a-113">Kitaplık</span><span class="sxs-lookup"><span data-stu-id="def9a-113">Library</span></span>|<span data-ttu-id="def9a-114">Açıklama</span><span class="sxs-lookup"><span data-stu-id="def9a-114">Description</span></span>|
|---|---|
|[<span data-ttu-id="def9a-115">msal.js</span><span class="sxs-lookup"><span data-stu-id="def9a-115">msal.js</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-js)|<span data-ttu-id="def9a-116">JavaScript Önizleme için Microsoft kimlik doğrulama kitaplığı</span><span class="sxs-lookup"><span data-stu-id="def9a-116">Microsoft Authentication Library for JavaScript Preview</span></span>|

> [!NOTE]
> <span data-ttu-id="def9a-117">*msal.js* hedefleri hello *Azure Active Directory v2 endpoint* -kişisel ve iş, okul hesapları toosign sağlar ve belirteçleri almak.</span><span class="sxs-lookup"><span data-stu-id="def9a-117">*msal.js* targets hello *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts toosign in and acquire tokens.</span></span> <span data-ttu-id="def9a-118">Merhaba *Azure Active Directory v2 endpoint* sahip [bazı sınırlamalar](..\active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="def9a-118">hello *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md).</span></span> <span data-ttu-id="def9a-119">Yalnızca iş ve Okul hesapları ilgileniyorsanız kullanmak *adal.js* ve hello *V1 endpoint*.</span><span class="sxs-lookup"><span data-stu-id="def9a-119">If you are interested only in school and work accounts, use *adal.js* and hello *V1 endpoint*.</span></span> <span data-ttu-id="def9a-120">Merhaba v1 ve v2 uç noktaları arasındaki farklar toounderstand okuma hello [v1 v2 karşılaştırma](..\active-directory-v2-compare.md).</span><span class="sxs-lookup"><span data-stu-id="def9a-120">toounderstand differences between hello v1 and v2 endpoints read hello [v1-v2 comparison](..\active-directory-v2-compare.md).</span></span>

<!--end-collapse-->
