---
title: "aaaAzure AD v2 Android Getting Started - giriş | Microsoft Docs"
description: "Nasıl bir Android uygulaması bir erişim belirteci alın ve Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren API'larını çağırma"
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
ms.openlocfilehash: 7c76ab8bbf1a6c934ab672cccf85ae82f03f601a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="8c592-103">Bir Android uygulaması Hello Microsoft Graph API çağrısı</span><span class="sxs-lookup"><span data-stu-id="8c592-103">Call hello Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="8c592-104">Bu kılavuz, nasıl yerel bir Android uygulaması bir erişim belirteci alın ve Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren diğer API'leri çağırmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="8c592-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="8c592-105">Bu kılavuzun Hello sonunda, uygulamanız (outlook.com, live.com ve diğerleri dahil) kişisel hesapları kullanan korumalı bir API mümkün toocall olması yanı sıra iş ve Okul hesapları herhangi bir şirket veya Azure Active Directory sahip kuruluş.</span><span class="sxs-lookup"><span data-stu-id="8c592-105">At hello end of this guide, your application will be able toocall a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="8c592-106">Bu örnek nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="8c592-106">How this sample works</span></span>
![Bu örnek nasıl çalışır?](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="8c592-108">Bu kılavuz tarafından oluşturulan hello örnek Android uygulama kullanılan tooquery Azure Active Directory v2 uç noktasından – bu durumda, Microsoft Graph API belirteçleri kabul eder bir Web API olduğu bir senaryo temel alır.</span><span class="sxs-lookup"><span data-stu-id="8c592-108">hello sample created by this guide is based on a scenario where an Android application is used tooquery a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="8c592-109">Bu senaryo için bir belirteç hello Authorization Üstbilgisi tooHTTP keşfi eklenir.</span><span class="sxs-lookup"><span data-stu-id="8c592-109">For this scenario, a token is added tooHTTP requests via hello Authorization header.</span></span> <span data-ttu-id="8c592-110">Belirteç edinme ve yenileme hello Microsoft kimlik doğrulama kitaplığı (MSAL) tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8c592-110">Token acquisition and renewal is handled by hello Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="8c592-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8c592-111">Pre-requisites</span></span>
* <span data-ttu-id="8c592-112">Bu Destekli Kurulum Android Studio odaklanmıştır, ancak herhangi bir Android uygulaması geliştirme ortamında da kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="8c592-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="8c592-113">Android SDK 21 ya da daha yeni gereklidir (SDK 25 önerilir).</span><span class="sxs-lookup"><span data-stu-id="8c592-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="8c592-114">Google Chrome veya özel sekmeleri kullanarak bir web tarayıcısı Android için bu sürüm Microsoft kimlik doğrulama kitaplığı (MSAL) için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8c592-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="8c592-115">Not: Google Chrome Android için Visual Studio öykünücüsü bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="8c592-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="8c592-116">Tootest öneririz, Google Chrome yüklediği bu API 21 veya daha yeni bir öykünücü API 25 veya bir görüntü ile kodu.</span><span class="sxs-lookup"><span data-stu-id="8c592-116">We recommend you tootest this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a><span data-ttu-id="8c592-117">Nasıl toohandle belirteci edinme tooaccess korumalı bir Web API</span><span class="sxs-lookup"><span data-stu-id="8c592-117">How toohandle token acquisition tooaccess a protected Web API</span></span>

<span data-ttu-id="8c592-118">Merhaba kullanıcı kimlik doğrulaması yaptıktan sonra Merhaba örnek uygulaması kullanılan tooquery Microsoft Graph API veya Microsoft Azure Active Directory v2 ile güvenli bir Web API olabilir bir belirteç alır.</span><span class="sxs-lookup"><span data-stu-id="8c592-118">After hello user authenticates, hello sample application receives a token that can be used tooquery Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="8c592-119">API Microsoft Graph gerektiren gibi belirli kaynaklara – Örneğin, tooread erişme bir erişim belirteci tooallow bir kullanıcının profilini kullanıcının Takvim erişmek veya bir e-posta gönderin.</span><span class="sxs-lookup"><span data-stu-id="8c592-119">APIs such as Microsoft Graph require an access token tooallow accessing specific resources – for example, tooread a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="8c592-120">Uygulamanızı API kapsamları belirterek bu kaynakları MSAL tooaccess kullanarak bir erişim belirteci isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c592-120">Your application can request an access token using MSAL tooaccess these resources by specifying API scopes.</span></span> <span data-ttu-id="8c592-121">Eklenen toohello HTTP Authorization Üstbilgisi hello karşı yapılan her çağrı korumalı kaynak sonra bu erişim belirteci değil.</span><span class="sxs-lookup"><span data-stu-id="8c592-121">This access token is then added toohello HTTP Authorization header for every call made against hello protected resource.</span></span> 

<span data-ttu-id="8c592-122">Önbelleğe alma ve böylece uygulamanız gerek olmayan erişim belirteçleri, yenileme MSAL yönetir.</span><span class="sxs-lookup"><span data-stu-id="8c592-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="8c592-123">Kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="8c592-123">Libraries</span></span>

<span data-ttu-id="8c592-124">Bu kılavuz kitaplıkları aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="8c592-124">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="8c592-125">Kitaplık</span><span class="sxs-lookup"><span data-stu-id="8c592-125">Library</span></span>|<span data-ttu-id="8c592-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8c592-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="8c592-127">com.microsoft.identity.Client</span><span class="sxs-lookup"><span data-stu-id="8c592-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="8c592-128">Microsoft kimlik doğrulama kitaplığı (MSAL)</span><span class="sxs-lookup"><span data-stu-id="8c592-128">Microsoft Authentication Library (MSAL)</span></span>|
