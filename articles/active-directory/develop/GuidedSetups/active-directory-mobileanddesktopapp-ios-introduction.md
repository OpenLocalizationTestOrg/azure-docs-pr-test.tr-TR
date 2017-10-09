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
# <a name="call-hello-microsoft-graph-api-from-an-ios-app"></a>Bir iOS uygulamasından Hello Microsoft Graph API çağırma

Bu kılavuz, nasıl bir yerel iOS uygulaması (Swift) bir erişim belirteci almak ve hello Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren diğer API'leri çağırmak gösterir.

Bu kılavuzun Hello sonunda, uygulamanız (outlook.com, live.com ve diğerleri dahil) kişisel hesapları kullanan korumalı bir API mümkün toocall olması yanı sıra iş ve Okul hesapları herhangi bir şirket veya Azure Active Directory sahip kuruluş.

> ### <a name="pre-requisites"></a>Ön koşullar
> - XCode 8.x bu kılavuzu için gereklidir. XCode indirebilirsiniz [buradan](https://geo.itunes.apple.com/us/app/xcode/id497799835?mt=12 "XCode yükleme URL'si").
> - [Carthage](https://github.com/Carthage/Carthage) paket Yönetimi

### <a name="how-this-guide-works"></a>Bu kılavuz nasıl çalışır?

![Bu kılavuz nasıl çalışır?](media/active-directory-mobileanddesktopapp-ios-introduction/iosintro.png)

Bu kılavuz tarafından oluşturulan hello örnek uygulamanın bir iOS uygulaması tooquery hello Microsoft Graph API veya Azure Active Directory v2 uç noktasından belirteçleri kabul eder bir Web API sağlar. Bu senaryo için bir belirteç hello Authorization Üstbilgisi tooHTTP keşfi eklenir. Belirteç edinme ve yenileme hello Microsoft kimlik doğrulama kitaplığı (MSAL) tarafından gerçekleştirilir.


### <a name="handling-token-acquisition-for-accessing-protected-web-apis"></a>Korumalı Web API'lerine erişmek için belirteç edinme işleme

Merhaba kullanıcı kimlik doğrulaması yaptıktan sonra Merhaba örnek uygulaması kullanılan tooquery hello Microsoft Graph API ya da Microsoft Azure Active Directory v2 ile güvenli bir Web API bir belirteç alır.

API Microsoft Graph gerektiren gibi belirli kaynaklara – Örneğin, tooread erişme bir erişim belirteci tooallow bir kullanıcının profilini kullanıcının Takvim erişmek veya bir e-posta gönderin. Uygulamanızı API kapsamları belirterek MSAL kullanarak bir erişim belirteci isteyebilirsiniz. Eklenen toohello HTTP Authorization Üstbilgisi hello karşı yapılan her çağrı korumalı kaynak sonra bu erişim belirteci değil.

Önbelleğe alma ve böylece uygulamanız gerek olmayan erişim belirteçleri, yenileme MSAL yönetir.


### <a name="nuget-packages"></a>NuGet paketleri

Bu kılavuz aşağıdaki NuGet paketlerini hello kullanır:

|Kitaplık|Açıklama|
|---|---|
|[MSAL.framework](https://github.com/AzureAD/microsoft-authentication-library-for-objc)|İOS için Microsoft kimlik doğrulama kitaplığı Önizleme|

