---
title: "aaaAzure AD v2 Android Başlarken - yapılandırma | Microsoft Docs"
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
ms.openlocfilehash: eaa41805c92212154ee8d51d3eb3aee1202eef1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Merhaba uygulamanın kayıt bilgileri tooyour uygulama Ekle

Bu adımda, tooadd hello istemci kimliği tooyour proje gerekir.

1.  Açık `MainActivity` (altında `app`  >  `java`  >   *`{host}.{namespace}`* )
2.  İle başlayan hello satırı değiştirin `final static String CLIENT_ID` ile:
```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
3. Aç:`app` > `manifests` > `AndroidManifest.xml`
4. Etkinlik çok aşağıdaki hello eklemek`manifest\application` düğümü. Bu kayıt bir `BrowserTabActivity` tooallow hello kimlik doğrulama işlemini tamamladıktan sonra uygulamanız işletim sistemi tooresume hello:

```xml
<!--Intent filter toocapture System Browser calling back tooour app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />

        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, hello scheme should be similar too'msal[appId]' -->
        <data android:scheme="msal[Enter hello application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```

### <a name="what-is-next"></a>Sonraki nedir

[Test ve doğrulama](active-directory-mobileanddesktopapp-android-test.md)
