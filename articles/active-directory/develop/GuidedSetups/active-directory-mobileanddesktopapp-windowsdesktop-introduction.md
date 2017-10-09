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
# <a name="call-hello-microsoft-graph-api-from-a-windows-desktop-app"></a>Windows Masaüstü uygulamasından Hello Microsoft Graph API çağırma

Bu kılavuz, nasıl bir yerel Windows Masaüstü .NET (XAML) uygulama erişim belirteci almak ve Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren diğer API'leri çağırmak gösterir.

Bu kılavuzun Hello sonunda, uygulamanız (outlook.com, live.com ve diğerleri dahil) kişisel hesapları kullanan korumalı bir API mümkün toocall olması yanı sıra iş ve Okul hesapları herhangi bir şirket veya Azure Active Directory sahip kuruluş.  

> Bu kılavuz, Visual Studio 2015 güncelleştirme 3'ü veya Visual Studio 2017 gerektirir.  Sahip değilseniz? [Visual Studio 2017 ücretsiz indirme](https://www.visualstudio.com/downloads/)

### <a name="how-this-guide-works"></a>Bu kılavuz nasıl çalışır?

![Bu kılavuz nasıl çalışır?](media/active-directory-mobileanddesktopapp-windowsdesktop-intro/windesktophowitworks.png)

Bu kılavuzu tarafından oluşturulan Merhaba örnek uygulaması, Windows masaüstü uygulaması tooquery Microsoft Graph API veya Azure Active Directory v2 uç noktasından belirteçleri kabul eder bir Web API sağlar. Bu senaryo için bir belirteç hello Authorization Üstbilgisi tooHTTP keşfi eklenir. Belirteç edinme ve yenileme hello Microsoft kimlik doğrulama kitaplığı (MSAL) tarafından gerçekleştirilir.


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Korumalı Web API'lerine erişmek için belirteç edinme işleme

Merhaba kullanıcı kimlik doğrulaması yaptıktan sonra Merhaba örnek uygulaması kullanılan tooquery Microsoft Graph API veya Microsoft Azure Active Directory v2 ile güvenli bir Web API olabilir bir belirteç alır.

API Microsoft Graph gerektiren gibi belirli kaynaklara – Örneğin, tooread erişme bir erişim belirteci tooallow bir kullanıcının profilini kullanıcının Takvim erişmek veya bir e-posta gönderin. Uygulamanızı API kapsamları belirterek bu kaynakları MSAL tooaccess kullanarak bir erişim belirteci isteyebilirsiniz. Eklenen toohello HTTP Authorization Üstbilgisi hello karşı yapılan her çağrı korumalı kaynak sonra bu erişim belirteci değil. 

Önbelleğe alma ve böylece uygulamanız gerek olmayan erişim belirteçleri, yenileme MSAL yönetir.


### <a name="nuget-packages"></a>NuGet paketleri

Bu kılavuz aşağıdaki NuGet paketlerini hello kullanır:

|Kitaplık|Açıklama|
|---|---|
|[Microsoft.Identity.Client](https://www.nuget.org/packages/Microsoft.Identity.Client)|Microsoft kimlik doğrulama kitaplığı (MSAL)|

