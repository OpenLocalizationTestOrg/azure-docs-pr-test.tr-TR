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
# <a name="call-hello-microsoft-graph-api-from-an-android-app"></a>Bir Android uygulaması Hello Microsoft Graph API çağrısı

Bu kılavuz, nasıl yerel bir Android uygulaması bir erişim belirteci alın ve Microsoft Graph API veya Azure Active Directory v2 uç noktasından erişim belirteçleri gerektiren diğer API'leri çağırmak gösterir.

Bu kılavuzun Hello sonunda, uygulamanız (outlook.com, live.com ve diğerleri dahil) kişisel hesapları kullanan korumalı bir API mümkün toocall olması yanı sıra iş ve Okul hesapları herhangi bir şirket veya Azure Active Directory sahip kuruluş.  

### <a name="how-this-sample-works"></a>Bu örnek nasıl çalışır?
![Bu örnek nasıl çalışır?](media/active-directory-mobileanddesktopapp-android-intro/android-intro.png)

Bu kılavuz tarafından oluşturulan hello örnek Android uygulama kullanılan tooquery Azure Active Directory v2 uç noktasından – bu durumda, Microsoft Graph API belirteçleri kabul eder bir Web API olduğu bir senaryo temel alır. Bu senaryo için bir belirteç hello Authorization Üstbilgisi tooHTTP keşfi eklenir. Belirteç edinme ve yenileme hello Microsoft kimlik doğrulama kitaplığı (MSAL) tarafından gerçekleştirilir.

### <a name="pre-requisites"></a>Ön koşullar
* Bu Destekli Kurulum Android Studio odaklanmıştır, ancak herhangi bir Android uygulaması geliştirme ortamında da kabul edilebilir. 
* Android SDK 21 ya da daha yeni gereklidir (SDK 25 önerilir).
* Google Chrome veya özel sekmeleri kullanarak bir web tarayıcısı Android için bu sürüm Microsoft kimlik doğrulama kitaplığı (MSAL) için gereklidir.

> Not: Google Chrome Android için Visual Studio öykünücüsü bulunmaz. Tootest öneririz, Google Chrome yüklediği bu API 21 veya daha yeni bir öykünücü API 25 veya bir görüntü ile kodu.


### <a name="how-toohandle-token-acquisition-tooaccess-a-protected-web-api"></a>Nasıl toohandle belirteci edinme tooaccess korumalı bir Web API

Merhaba kullanıcı kimlik doğrulaması yaptıktan sonra Merhaba örnek uygulaması kullanılan tooquery Microsoft Graph API veya Microsoft Azure Active Directory v2 ile güvenli bir Web API olabilir bir belirteç alır.

API Microsoft Graph gerektiren gibi belirli kaynaklara – Örneğin, tooread erişme bir erişim belirteci tooallow bir kullanıcının profilini kullanıcının Takvim erişmek veya bir e-posta gönderin. Uygulamanızı API kapsamları belirterek bu kaynakları MSAL tooaccess kullanarak bir erişim belirteci isteyebilirsiniz. Eklenen toohello HTTP Authorization Üstbilgisi hello karşı yapılan her çağrı korumalı kaynak sonra bu erişim belirteci değil. 

Önbelleğe alma ve böylece uygulamanız gerek olmayan erişim belirteçleri, yenileme MSAL yönetir.

### <a name="libraries"></a>Kitaplıkları

Bu kılavuz kitaplıkları aşağıdaki hello kullanır:

|Kitaplık|Açıklama|
|---|---|
|[com.microsoft.identity.Client](http://javadoc.io/doc/com.microsoft.identity.client/msal)|Microsoft kimlik doğrulama kitaplığı (MSAL)|
