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
## <a name="create-an-application-express"></a><span data-ttu-id="b0931-103">(Hızlı) uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="b0931-103">Create an application (Express)</span></span>
<span data-ttu-id="b0931-104">Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="b0931-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="b0931-105">Merhaba aracılığıyla uygulamanızı kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="b0931-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="b0931-106">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="b0931-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="b0931-107">Kurulum destekli Hello seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="b0931-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="b0931-108">Merhaba yönergeleri tooobtain hello uygulama kimliği izleyin ve kodunuza yapıştırın</span><span class="sxs-lookup"><span data-stu-id="b0931-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="b0931-109">Uygulama kayıt bilgileri tooyour çözümünüz (Gelişmiş) ekleyin</span><span class="sxs-lookup"><span data-stu-id="b0931-109">Add your application registration information tooyour solution (Advanced)</span></span>

1.  <span data-ttu-id="b0931-110">Çok Git[Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="b0931-110">Go too[Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="b0931-111">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="b0931-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="b0931-112">Destekli kurulumu için Hello seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="b0931-112">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="b0931-113">Tıklatın `Add Platform`seçeneğini belirleyip `Native Application` ve'ı tıklatın`Save`</span><span class="sxs-lookup"><span data-stu-id="b0931-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="b0931-114">TooXcode geri dönün.</span><span class="sxs-lookup"><span data-stu-id="b0931-114">Go back tooXcode.</span></span> <span data-ttu-id="b0931-115">İçinde `ViewController.swift`, hello çizgi ile başlayan Değiştir '`let kClientID`' hello uygulama kimliği ile yalnızca kayıtlı:</span><span class="sxs-lookup"><span data-stu-id="b0931-115">In `ViewController.swift`, replace hello line starting with '`let kClientID`' with hello application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="b0931-116">Control + tıklatın <code>Info.plist</code> toobring yukarı hello bağlamsal menü ve ardından: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="b0931-116">Control+click <code>Info.plist</code> toobring up hello contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="b0931-117">Merhaba altında <code>dict</code> kök düğümü, hello aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b0931-117">Under hello <code>dict</code> root node, add hello following:</span></span>
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
<span data-ttu-id="b0931-118">Değiştir <i> <code>[Your_Application_Id_Here]</code> </i> hello uygulama kimliği yalnızca kayıtlı sahip</span><span class="sxs-lookup"><span data-stu-id="b0931-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with hello Application Id you just registered</span></span>
</li>
</ol>
