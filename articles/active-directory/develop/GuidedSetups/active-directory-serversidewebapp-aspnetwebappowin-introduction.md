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
# <a name="add-sign-in-with-microsoft-tooan-aspnet-web-app"></a>Microsoft tooan ASP.NET web uygulaması ile oturum açma ekleme

Bu kılavuz, nasıl tooimplement ile oturum açma Openıd Connect kullanarak geleneksel web tarayıcı tabanlı bir uygulama ile ASP.NET MVC çözümünü kullanarak Microsoft gösterir. 

Bu kılavuzun Hello sonunda, uygulamanız kişisel bileşenleri (outlook.com, live.com ve diğerleri dahil) hesaplarının yanı sıra iş mümkün tooaccept oturum olması ve Okul hesapları herhangi bir şirket veya Azure Active Directory ile tümleşik olan kuruluş. 

> Bu kılavuz, Visual Studio 2015 güncelleştirme 3'ü veya Visual Studio 2017 gerektirir.  Sahip değilseniz?  [Visual Studio 2017 ücretsiz indirme](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a>Bu kılavuz nasıl çalışır?

![Bu kılavuz nasıl çalışır?](media/active-directory-serversidewebapp-aspnetwebappowin-intro/aspnetbrowsergeneral.png)

Bu kılavuz, bir oturum açma düğmesi aracılığıyla kullanıcı tooauthenticate isteyen hello senaryosunda burada bir tarayıcı bir ASP.NET web sitesine erişen temel alır. Bu senaryoda, çoğu hello iş toorender hello web sayfasının hello sunucu tarafında gerçekleşir.

## <a name="libraries"></a>Kitaplıkları

Bu kılavuz kitaplıkları aşağıdaki hello kullanır:

|Kitaplık|Açıklama|
|---|---|
|[Microsoft.Owin.Security.OpenIdConnect](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|Kimlik doğrulaması için bir uygulama toouse Openıdconnect sağlayan Ara|
|[Microsoft.Owin.Security.Cookies](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|Tanımlama bilgilerini kullanarak bir uygulama toomaintain kullanıcı oturumu etkinleştirir Ara|
|[Microsoft.Owin.Host.SystemWeb](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|OWIN tabanlı uygulamalar toorun hello ASP.NET isteği ardışık düzeni kullanılarak IIS'de sağlar|

