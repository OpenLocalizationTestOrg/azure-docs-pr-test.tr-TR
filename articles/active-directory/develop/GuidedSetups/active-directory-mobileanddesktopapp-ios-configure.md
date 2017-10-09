---
title: "aaaAzure AD v2 iOS Başlarken - yapılandırma | Microsoft Docs"
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
ms.openlocfilehash: 537cc7f0de6cd947fe340566c9e93f8bb08d57a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>(Hızlı) uygulama oluşturma
Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:
1. Merhaba aracılığıyla uygulamanızı kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)
2.  Uygulamanız ve e-posta için bir ad girin
3.  Kurulum destekli Hello seçeneğinin işaretli olduğundan emin olun
4.  Merhaba yönergeleri tooobtain hello uygulama kimliği izleyin ve kodunuza yapıştırın

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Uygulama kayıt bilgileri tooyour çözümünüz (Gelişmiş) ekleyin

1.  Çok Git[Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app)
2.  Uygulamanız ve e-posta için bir ad girin
3.  Destekli kurulumu için Hello seçeneğinin işaretli olduğundan emin olun
4.  Tıklatın `Add Platform`seçeneğini belirleyip `Native Application` ve'ı tıklatın`Save`
5.  TooXcode geri dönün. İçinde `ViewController.swift`, hello çizgi ile başlayan Değiştir '`let kClientID`' hello uygulama kimliği ile yalnızca kayıtlı:

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
Control + tıklatın <code>Info.plist</code> toobring yukarı hello bağlamsal menü ve ardından: <code>Open As</code>> <code>Source Code</code>
</li>
<li>
Merhaba altında <code>dict</code> kök düğümü, hello aşağıdakileri ekleyin:
</li>
</ol>

```xml
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>$(PRODUCT_BUNDLE_IDENTIFIER)</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>msal[Your_Application_Id_Here]</string>
            <string>auth</string>
        </array>
    </dict>
</array>
```
<ol start="8">
<li>
Değiştir <i> <code>[Your_Application_Id_Here]</code> </i> hello uygulama kimliği yalnızca kayıtlı sahip
</li>
</ol>
