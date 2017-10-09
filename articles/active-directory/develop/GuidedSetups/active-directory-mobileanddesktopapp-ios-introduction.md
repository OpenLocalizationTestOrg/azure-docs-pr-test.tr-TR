---
title: "aaaAzure AD v2 iOS Başlarken - giriş | Microsoft Docs"
description: "İOS (Swift) uygulamaları, Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
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
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: f40aebbb75490912e533aecc7eedfb2b2dcd8c6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a><span data-ttu-id="07f2c-103">Bir iOS uygulamasından Hello Microsoft Graph API çağırma</span><span class="sxs-lookup"><span data-stu-id="07f2c-103">Call hello Microsoft Graph API from an iOS app</span></span>

<span data-ttu-id="07f2c-104">Bu kılavuz, nasıl bir yerel iOS uygulaması (Swift) bir erişim belirteci almak ve hello Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren diğer API'leri çağırmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="07f2c-104">This guide demonstrates how a native iOS application (Swift) can get an access token and call hello Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="07f2c-105">Bu kılavuzun Hello sonunda, uygulamanız (outlook.com, live.com ve diğerleri dahil) kişisel hesapları kullanan korumalı bir API mümkün toocall olması yanı sıra iş ve Okul hesapları herhangi bir şirket veya Azure Active Directory sahip kuruluş.</span><span class="sxs-lookup"><span data-stu-id="07f2c-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>

> ### <a name="pre-requisites"></a><span data-ttu-id="07f2c-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="07f2c-106">Pre-requisites</span></span>
> - <span data-ttu-id="07f2c-107">XCode 8.x bu kılavuzu için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="07f2c-107">XCode 8.x is required for this guide.</span></span> <span data-ttu-id="07f2c-108">XCode indirebilirsiniz [buradan](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode yükleme URL'si").</span><span class="sxs-lookup"><span data-stu-id="07f2c-108">You can download XCode [from here](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode Download URL").</span></span>
> - <span data-ttu-id="07f2c-109">[Carthage](https://github.com/Carthage/Carthage) paket Yönetimi</span><span class="sxs-lookup"><span data-stu-id="07f2c-109">[Carthage](https://github.com/Carthage/Carthage) for package management</span></span>

### <a name="how-this-guide-works"></a><span data-ttu-id="07f2c-110">Bu kılavuz nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="07f2c-110">How this guide works</span></span>

![Bu kılavuz nasıl çalışır?](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

<span data-ttu-id="07f2c-112">Bu kılavuz tarafından oluşturulan hello örnek uygulamanın bir iOS uygulaması tooquery hello Microsoft Graph API veya Azure Active Directory v2 uç noktasından belirteçleri kabul eder bir Web API sağlar.</span><span class="sxs-lookup"><span data-stu-id="07f2c-112">hello sample application created by this guide enables an iOS application tooquery hello Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="07f2c-113">Bu senaryo için bir belirteç hello Authorization Üstbilgisi tooHTTP keşfi eklenir.</span><span class="sxs-lookup"><span data-stu-id="07f2c-113">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="07f2c-114">Belirteç edinme ve yenileme hello Microsoft kimlik doğrulama kitaplığı (MSAL) tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="07f2c-114">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="07f2c-115">Korumalı Web API'lerine erişmek için belirteç edinme işleme</span><span class="sxs-lookup"><span data-stu-id="07f2c-115">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="07f2c-116">Merhaba kullanıcı kimlik doğrulaması yaptıktan sonra Merhaba örnek uygulaması kullanılan tooquery hello Microsoft Graph API ya da Microsoft Azure Active Directory v2 ile güvenli bir Web API bir belirteç alır.</span><span class="sxs-lookup"><span data-stu-id="07f2c-116">After hello user authenticates, hello sample application receives a token that can be used tooquery hello Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="07f2c-117">API Microsoft Graph gerektiren gibi belirli kaynaklara – Örneğin, tooread erişme bir erişim belirteci tooallow bir kullanıcının profilini kullanıcının Takvim erişmek veya bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="07f2c-117">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="07f2c-118">Uygulamanızı API kapsamları belirterek MSAL kullanarak bir erişim belirteci isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07f2c-118">Your application can request an access token using MSAL by specifying API scopes.</span></span> <span data-ttu-id="07f2c-119">Eklenen toohello HTTP Authorization Üstbilgisi hello karşı yapılan her çağrı korumalı kaynak sonra bu erişim belirteci değil.</span><span class="sxs-lookup"><span data-stu-id="07f2c-119">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span>

<span data-ttu-id="07f2c-120">Önbelleğe alma ve böylece uygulamanız gerek olmayan erişim belirteçleri, yenileme MSAL yönetir.</span><span class="sxs-lookup"><span data-stu-id="07f2c-120">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="07f2c-121">NuGet paketleri</span><span class="sxs-lookup"><span data-stu-id="07f2c-121">NuGet packages</span></span>

<span data-ttu-id="07f2c-122">Bu kılavuz aşağıdaki NuGet paketlerini hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="07f2c-122">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="07f2c-123">Kitaplık</span><span class="sxs-lookup"><span data-stu-id="07f2c-123">Library</span></span>|<span data-ttu-id="07f2c-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="07f2c-124">Description</span></span>|
|---|---|
|[<span data-ttu-id="07f2c-125">MSAL.framework</span><span class="sxs-lookup"><span data-stu-id="07f2c-125">MSAL.framework</span></span>](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|<span data-ttu-id="07f2c-126">İOS için Microsoft kimlik doğrulama kitaplığı Önizleme</span><span class="sxs-lookup"><span data-stu-id="07f2c-126">Microsoft Authentication Library Preview for iOS</span></span>|

