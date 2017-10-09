---
title: "aaaAzure AD v2 ASP.NET Web sunucusu Getting Started - giriş | Microsoft Docs"
description: "Microsoft oturum açma Openıd Connect standardını kullanan geleneksel web tarayıcı tabanlı bir uygulama ile ASP.NET çözümünü uygulama"
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
ms.openlocfilehash: d6449926af2bdad24cbc8e91f74885a08f909103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a><span data-ttu-id="ebc7e-103">Microsoft tooan ASP.NET web uygulaması ile oturum açma ekleme</span><span class="sxs-lookup"><span data-stu-id="ebc7e-103">Add sign-in with Microsoft tooan ASP.NET web app</span></span>

<span data-ttu-id="ebc7e-104">Bu kılavuz, nasıl tooimplement ile oturum açma Openıd Connect kullanarak geleneksel web tarayıcı tabanlı bir uygulama ile ASP.NET MVC çözümünü kullanarak Microsoft gösterir.</span><span class="sxs-lookup"><span data-stu-id="ebc7e-104">This guide demonstrates how tooimplement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="ebc7e-105">Bu kılavuzun Hello sonunda, uygulamanız kişisel bileşenleri (outlook.com, live.com ve diğerleri dahil) hesaplarının yanı sıra iş mümkün tooaccept oturum olması ve Okul hesapları herhangi bir şirket veya Azure Active Directory ile tümleşik olan kuruluş.</span><span class="sxs-lookup"><span data-stu-id="ebc7e-105">At hello end of this guide, your application will be able tooaccept sign ins of personal accounts (including outlook.com, live.com, and others) as well as work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> 

> <span data-ttu-id="ebc7e-106">Bu kılavuz, Visual Studio 2015 güncelleştirme 3'ü veya Visual Studio 2017 gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ebc7e-106">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="ebc7e-107">Sahip değilseniz?</span><span class="sxs-lookup"><span data-stu-id="ebc7e-107">Don’t have it?</span></span>  [<span data-ttu-id="ebc7e-108">Visual Studio 2017 ücretsiz indirme</span><span class="sxs-lookup"><span data-stu-id="ebc7e-108">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="ebc7e-109">Bu kılavuz nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="ebc7e-109">How this guide works</span></span>

![Bu kılavuz nasıl çalışır?](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

<span data-ttu-id="ebc7e-111">Bu kılavuz, bir oturum açma düğmesi aracılığıyla kullanıcı tooauthenticate isteyen hello senaryosunda burada bir tarayıcı bir ASP.NET web sitesine erişen temel alır.</span><span class="sxs-lookup"><span data-stu-id="ebc7e-111">This guide is based on hello scenario where a browser accesses an ASP.NET web site, requesting a user tooauthenticate via a sign-in button.</span></span> <span data-ttu-id="ebc7e-112">Bu senaryoda, çoğu hello iş toorender hello web sayfasının hello sunucu tarafında gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="ebc7e-112">In this scenario, most of hello work toorender hello web page occurs on hello server side.</span></span>

## <a name="libraries"></a><span data-ttu-id="ebc7e-113">Kitaplıkları</span><span class="sxs-lookup"><span data-stu-id="ebc7e-113">Libraries</span></span>

<span data-ttu-id="ebc7e-114">Bu kılavuz kitaplıkları aşağıdaki hello kullanır:</span><span class="sxs-lookup"><span data-stu-id="ebc7e-114">This guide uses hello following libraries:</span></span>

|<span data-ttu-id="ebc7e-115">Kitaplık</span><span class="sxs-lookup"><span data-stu-id="ebc7e-115">Library</span></span>|<span data-ttu-id="ebc7e-116">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ebc7e-116">Description</span></span>|
|---|---|
|[<span data-ttu-id="ebc7e-117">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="ebc7e-117">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="ebc7e-118">Kimlik doğrulaması için bir uygulama toouse Openıdconnect sağlayan Ara</span><span class="sxs-lookup"><span data-stu-id="ebc7e-118">Middleware that enables an application toouse OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="ebc7e-119">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="ebc7e-119">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="ebc7e-120">Tanımlama bilgilerini kullanarak bir uygulama toomaintain kullanıcı oturumu etkinleştirir Ara</span><span class="sxs-lookup"><span data-stu-id="ebc7e-120">Middleware that enables an application toomaintain user session using cookies</span></span>|
|[<span data-ttu-id="ebc7e-121">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="ebc7e-121">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="ebc7e-122">OWIN tabanlı uygulamalar toorun hello ASP.NET isteği ardışık düzeni kullanılarak IIS'de sağlar</span><span class="sxs-lookup"><span data-stu-id="ebc7e-122">Enables OWIN-based applications toorun on IIS using hello ASP.NET request pipeline</span></span>|

