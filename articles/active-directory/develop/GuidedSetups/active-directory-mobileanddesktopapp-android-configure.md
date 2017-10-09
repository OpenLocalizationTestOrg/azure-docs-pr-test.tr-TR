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
ms.openlocfilehash: e14796c37ab0c30d948b6f783dac80059375afa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>(Hızlı) uygulama oluşturma
Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:
1. Merhaba aracılığıyla uygulamanızı kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)
2.  Uygulamanız ve e-posta için bir ad girin
3.  Kurulum destekli Hello seçeneğinin işaretli olduğundan emin olun
4.  Merhaba yönergeleri tooobtain hello uygulama kimliği izleyin ve kodunuza yapıştırın

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Uygulama kayıt bilgileri tooyour çözümünüz (Gelişmiş) ekleyin
Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:
1. Toohello Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app) tooregister uygulama
2. Uygulamanız ve e-posta için bir ad girin 
3. Destekli kurulumu için Hello seçeneğinin işaretli olduğundan emin olun
4. Tıklatın `Add Platform`seçeneğini belirleyip `Native Application` ve kaydetme ulaştı.
5.  Açık `MainActivity` (altında `app`  >  `java`  >   *`{host}.{namespace}`* )
6.  Hello yerine *[hello uygulama kodu buraya girin]* başlayarak hello satırdaki `final static String CLIENT_ID` yalnızca kayıtlı hello uygulama kimliği:

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
Açık `AndroidManifest.xml` (altında `app`  >  `manifests`) etkinlik çok aşağıdaki Ekle hello`manifest\application` düğümü. Bu kayıtları bir `BrowserTabActivity` tooallow hello kimlik doğrulama işlemini tamamladıktan sonra uygulamanız işletim sistemi tooresume hello:
</li>
</ol>

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
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
Merhaba, `BrowserTabActivity`, yerine `[Enter hello application Id here]` hello uygulama kimliğiyle
</li>
</ol>
