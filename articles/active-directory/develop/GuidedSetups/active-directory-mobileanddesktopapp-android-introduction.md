---
title: "Azure AD v2 Android alma başlatıldı - giriş | Microsoft Docs"
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
ms.openlocfilehash: d933781713456f73aa76db557fdf35672dfb2a29
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="call-the-microsoft-graph-api-from-an-android-app"></a><span data-ttu-id="8bc4a-103">Bir Android uygulaması Microsoft Graph API çağrısı</span><span class="sxs-lookup"><span data-stu-id="8bc4a-103">Call the Microsoft Graph API from an Android app</span></span>

<span data-ttu-id="8bc4a-104">Bu kılavuz, nasıl yerel bir Android uygulaması bir erişim belirteci alın ve Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren diğer API'leri çağırmak gösterir.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-104">This guide demonstrates how a native Android application can get an access token and call Microsoft Graph API or other APIs that require access tokens from Azure Active Directory v2 endpoint.</span></span>

<span data-ttu-id="8bc4a-105">Bu kılavuzun sonunda uygulamanız (outlook.com, live.com ve diğerleri dahil) kişisel hesapları hem de iş kullanan korumalı bir API çağrısı ve Okul hesapları herhangi bir şirket veya Azure Active Directory sahip kuruluş mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-105">At the end of this guide, your application will be able to call a protected API using personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has Azure Active Directory.</span></span>  

### <a name="how-this-sample-works"></a><span data-ttu-id="8bc4a-106">Bu örnek nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="8bc4a-106">How this sample works</span></span>
![Bu örnek nasıl çalışır?](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

<span data-ttu-id="8bc4a-108">Bu kılavuz tarafından oluşturulan örnek Android uygulama Azure Active Directory v2 uç noktasından – bu durumda, Microsoft Graph API belirteçleri kabul eder bir Web API sorgulamak için kullanıldığı bir senaryo temel alır.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-108">The sample created by this guide is based on a scenario where an Android application is used to query a Web API that accepts tokens from Azure Active Directory v2 endpoint – in this case, Microsoft Graph API.</span></span> <span data-ttu-id="8bc4a-109">Bu senaryoda, HTTP isteklerini Authorization Üstbilgisi yoluyla bir belirteç eklenir.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-109">For this scenario, a token is added to HTTP requests via the Authorization header.</span></span> <span data-ttu-id="8bc4a-110">Belirteç edinme ve yenileme Microsoft kimlik doğrulama kitaplığı (MSAL) tarafından gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-110">Token acquisition and renewal is handled by the Microsoft Authentication Library (MSAL).</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="8bc4a-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="8bc4a-111">Pre-requisites</span></span>
* <span data-ttu-id="8bc4a-112">Bu Destekli Kurulum Android Studio odaklanmıştır, ancak herhangi bir Android uygulaması geliştirme ortamında da kabul edilebilir.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-112">This guided setup is focused on Android Studio, but any other Android application development environment is also acceptable.</span></span> 
* <span data-ttu-id="8bc4a-113">Android SDK 21 ya da daha yeni gereklidir (SDK 25 önerilir).</span><span class="sxs-lookup"><span data-stu-id="8bc4a-113">Android SDK 21 or newer is required (SDK 25 is recommended).</span></span>
* <span data-ttu-id="8bc4a-114">Google Chrome veya özel sekmeleri kullanarak bir web tarayıcısı Android için bu sürüm Microsoft kimlik doğrulama kitaplığı (MSAL) için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-114">Google Chrome or a web browser using Custom Tabs is required for this release of Microsoft Authentication Library (MSAL) for Android.</span></span>

> <span data-ttu-id="8bc4a-115">Not: Google Chrome Android için Visual Studio öykünücüsü bulunmaz.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-115">Note: Google Chrome is not included on Visual Studio Emulator for Android.</span></span> <span data-ttu-id="8bc4a-116">Bu kodu, Google Chrome yüklediği bir öykünücü API 25 veya bir görüntü ile API 21 ile veya test etmenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-116">We recommend you to test this code on an Emulator with API 25 or an image with API 21 or newer that has with Google Chrome installed.</span></span>


### <a name="how-to-handle-token-acquisition-to-access-a-protected-web-api"></a><span data-ttu-id="8bc4a-117">Korumalı bir Web API erişmek için belirteç edinme nasıl ele alınacağını</span><span class="sxs-lookup"><span data-stu-id="8bc4a-117">How to handle token acquisition to access a protected Web API</span></span>

<span data-ttu-id="8bc4a-118">Kullanıcı kimlik doğrulaması yaptıktan sonra örnek uygulamayı Microsoft Graph API veya Microsoft Azure Active Directory v2 ile güvenli bir Web API sorgulamak için kullanılan bir belirteç alır.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-118">After the user authenticates, the sample application receives a token that can be used to query Microsoft Graph API or a Web API secured by Microsoft Azure Active Directory v2.</span></span>

<span data-ttu-id="8bc4a-119">API Microsoft Graph gibi belirli kaynaklara – Örneğin, bir kullanıcının profilini, erişim kullanıcının Takvim okuma ya da bir e-posta göndermek erişim izin vermek için bir erişim belirteci gerektirir.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-119">APIs such as Microsoft Graph require an access token to allow accessing specific resources – for example, to read a user’s profile, access user’s calendar or send an email.</span></span> <span data-ttu-id="8bc4a-120">Uygulamanızı API kapsamları belirterek bu kaynaklara erişmek için MSAL kullanarak bir erişim belirteci isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-120">Your application can request an access token using MSAL to access these resources by specifying API scopes.</span></span> <span data-ttu-id="8bc4a-121">Bu erişim belirteci, ardından HTTP Authorization Üstbilgisi karşı korunan bir kaynağa yapılan her çağrı eklenir.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-121">This access token is then added to the HTTP Authorization header for every call made against the protected resource.</span></span> 

<span data-ttu-id="8bc4a-122">Önbelleğe alma ve böylece uygulamanız gerek olmayan erişim belirteçleri, yenileme MSAL yönetir.</span><span class="sxs-lookup"><span data-stu-id="8bc4a-122">MSAL manages caching and refreshing access tokens for you, so your application doesn't need to.</span></span>

### <a name="libraries"></a><span data-ttu-id="8bc4a-123">Kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="8bc4a-123">Libraries</span></span>

<span data-ttu-id="8bc4a-124">Bu kılavuz aşağıdaki kitaplıklarını kullanır:</span><span class="sxs-lookup"><span data-stu-id="8bc4a-124">This guide uses the following libraries:</span></span>

|<span data-ttu-id="8bc4a-125">Kitaplık</span><span class="sxs-lookup"><span data-stu-id="8bc4a-125">Library</span></span>|<span data-ttu-id="8bc4a-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8bc4a-126">Description</span></span>|
|---|---|
|[<span data-ttu-id="8bc4a-127">com.microsoft.identity.Client</span><span class="sxs-lookup"><span data-stu-id="8bc4a-127">com.microsoft.identity.client</span></span>](http://javadoc.io/doc/com.microsoft.identity.client/msal)|<span data-ttu-id="8bc4a-128">Microsoft kimlik doğrulama kitaplığı (MSAL)</span><span class="sxs-lookup"><span data-stu-id="8bc4a-128">Microsoft Authentication Library (MSAL)</span></span>|
