---
title: "aaaAzure AD v2 Windows Masaüstü Getting Started - giriş | Microsoft Docs"
description: "Windows Masaüstü .NET (XAML) uygulamaları, Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 89d98fc46190ba9e47b7c3095f91e32eca455fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a><span data-ttu-id="55b12-103">Windows Masaüstü uygulamasından Hello Microsoft Graph API çağırma</span><span class="sxs-lookup"><span data-stu-id="55b12-103">Call hello Microsoft Graph API from a Windows Desktop app</span></span>

<span data-ttu-id="55b12-104">Bu kılavuz, nasıl bir yerel Windows Masaüstü .NET (XAML) uygulama erişim belirteci almak ve Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren diğer API'leri çağırmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="55b12-104">This guide demonstrates how a native Windows Desktop .NET (XAML) application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="55b12-105">Bu kılavuzun Hello sonunda, uygulamanız (outlook.com, live.com ve diğerleri dahil) kişisel hesapları kullanan korumalı bir API mümkün toocall olması yanı sıra iş ve Okul hesapları herhangi bir şirket veya Azure Active Directory sahip kuruluş.</span><span class="sxs-lookup"><span data-stu-id="55b12-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

> <span data-ttu-id="55b12-106">Bu kılavuz, Visual Studio 2015 güncelleştirme 3'ü veya Visual Studio 2017 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="55b12-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="55b12-107">Sahip değilseniz?</span><span class="sxs-lookup"><span data-stu-id="55b12-107">Don’t have it?</span></span> [<span data-ttu-id="55b12-108">Visual Studio 2017 ücretsiz indirme</span><span class="sxs-lookup"><span data-stu-id="55b12-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a><span data-ttu-id="55b12-109">Bu kılavuz nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="55b12-109">How this guide works</span></span>

![Bu kılavuz nasıl çalışır?](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

<span data-ttu-id="55b12-111">Bu kılavuzu tarafından oluşturulan Merhaba örnek uygulaması, Windows masaüstü uygulaması tooquery Microsoft Graph API veya Azure Active Directory v2 uç noktasından belirteçleri kabul eder bir Web API sağlar.</span><span class="sxs-lookup"><span data-stu-id="55b12-111">hello sample application created by this guide enables a Windows Desktop Application tooquery Microsoft Graph API or a Web API that accepts tokens from Azure Active Directory v2 endpoint.</span></span> <span data-ttu-id="55b12-112">Bu senaryo için bir belirteç hello Authorization Üstbilgisi tooHTTP keşfi eklenir.</span><span class="sxs-lookup"><span data-stu-id="55b12-112">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="55b12-113">Belirteç edinme ve yenileme hello Microsoft kimlik doğrulama kitaplığı (MSAL) tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="55b12-113">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a><span data-ttu-id="55b12-114">Korumalı Web API'lerine erişmek için belirteç edinme işleme</span><span class="sxs-lookup"><span data-stu-id="55b12-114">Handling token acquisition for accessing protected Web APIs</span></span>

<span data-ttu-id="55b12-115">Merhaba kullanıcı kimlik doğrulaması yaptıktan sonra Merhaba örnek uygulaması kullanılan tooquery Microsoft Graph API veya Microsoft Azure Active Directory v2 ile güvenli bir Web API olabilir bir belirteç alır.</span><span class="sxs-lookup"><span data-stu-id="55b12-115">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="55b12-116">API Microsoft Graph gerektiren gibi belirli kaynaklara – Örneğin, tooread erişme bir erişim belirteci tooallow bir kullanıcının profilini kullanıcının Takvim erişmek veya bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="55b12-116">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="55b12-117">Uygulamanızı API kapsamları belirterek bu kaynakları MSAL tooaccess kullanarak bir erişim belirteci isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55b12-117">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="55b12-118">Eklenen toohello HTTP Authorization Üstbilgisi hello karşı yapılan her çağrı korumalı kaynak sonra bu erişim belirteci değil.</span><span class="sxs-lookup"><span data-stu-id="55b12-118">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="55b12-119">Önbelleğe alma ve böylece uygulamanız gerek olmayan erişim belirteçleri, yenileme MSAL yönetir.</span><span class="sxs-lookup"><span data-stu-id="55b12-119">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>


### <a name="nuget-packages"></a><span data-ttu-id="55b12-120">NuGet paketleri</span><span class="sxs-lookup"><span data-stu-id="55b12-120">NuGet Packages</span></span>

<span data-ttu-id="55b12-121">Bu kılavuz aşağıdaki NuGet paketlerini hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="55b12-121">This guide uses hello following NuGet packages:</span></span>

|<span data-ttu-id="55b12-122">Kitaplık</span><span class="sxs-lookup"><span data-stu-id="55b12-122">Library</span></span>|<span data-ttu-id="55b12-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="55b12-123">Description</span></span>|
|---|---|
|[<span data-ttu-id="55b12-124">Microsoft.Identity.Client</span><span class="sxs-lookup"><span data-stu-id="55b12-124">Microsoft.Identity.Client</span></span>](https://www.nuget.org/packages/Microsoft.Identity.Client)|<span data-ttu-id="55b12-125">Microsoft kimlik doğrulama kitaplığı (MSAL)</span><span class="sxs-lookup"><span data-stu-id="55b12-125">Microsoft Authentication Library (MSAL)</span></span>|

