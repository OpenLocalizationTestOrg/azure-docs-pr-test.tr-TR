---
title: "Azure AD v2 iOS Başlarken - yapılandırma | Microsoft Docs"
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
ms.openlocfilehash: 0ebca65585fc87bd4a85ba092cd423fce9540f58
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="7e182-103">(Hızlı) uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e182-103">Create an application (Express)</span></span>
<span data-ttu-id="7e182-104">Uygulamanızı kaydetmeniz gerekir artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="7e182-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="7e182-105">Uygulamanızı aracılığıyla kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span><span class="sxs-lookup"><span data-stu-id="7e182-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=ios&step=configure)</span></span>
2.  <span data-ttu-id="7e182-106">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="7e182-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="7e182-107">Kurulum destekli seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="7e182-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="7e182-108">Uygulama Kimliğini almak ve kodunuza yapıştırmak için yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="7e182-108">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="7e182-109">Uygulama kayıt bilgilerinizi çözümünüze (Gelişmiş) ekleyin</span><span class="sxs-lookup"><span data-stu-id="7e182-109">Add your application registration information to your solution (Advanced)</span></span>

1.  <span data-ttu-id="7e182-110">Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app)</span><span class="sxs-lookup"><span data-stu-id="7e182-110">Go to [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app)</span></span>
2.  <span data-ttu-id="7e182-111">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="7e182-111">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="7e182-112">Destekli kurulumu için seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="7e182-112">Make sure the option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="7e182-113">Tıklatın `Add Platform`seçeneğini belirleyip `Native Application` ve'ı tıklatın`Save`</span><span class="sxs-lookup"><span data-stu-id="7e182-113">Click `Add Platform`, then select `Native Application` and click `Save`</span></span>
5.  <span data-ttu-id="7e182-114">Xcode için geri dönün.</span><span class="sxs-lookup"><span data-stu-id="7e182-114">Go back to Xcode.</span></span> <span data-ttu-id="7e182-115">İçinde `ViewController.swift`, ile başlayan satırı Değiştir '`let kClientID`' yalnızca kayıtlı uygulama kimliği:</span><span class="sxs-lookup"><span data-stu-id="7e182-115">In `ViewController.swift`, replace the line starting with '`let kClientID`' with the application ID you just registered:</span></span>

```swift
let kClientID = "Your_Application_Id_Here"
```

<!-- Workaround for Docs conversion bug -->
<ol start="6">
<li>
<span data-ttu-id="7e182-116">Control + tıklatın <code>Info.plist</code> bağlam menüsünü açmak ve ardından: <code>Open As</code>> <code>Source Code</code>
</span><span class="sxs-lookup"><span data-stu-id="7e182-116">Control+click <code>Info.plist</code> to bring up the contextual menu, and then click: <code>Open As</code> > <code>Source Code</code>
</span></span></li>
<li>
<span data-ttu-id="7e182-117">Altında <code>dict</code> kök düğümü, aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7e182-117">Under the <code>dict</code> root node, add the following:</span></span>
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
<span data-ttu-id="7e182-118">Değiştir <i> <code>[Your_Application_Id_Here]</code> </i> yalnızca kayıtlı uygulama kimliği</span><span class="sxs-lookup"><span data-stu-id="7e182-118">Replace <i><code>[Your_Application_Id_Here]</code></i> with the Application Id you just registered</span></span>
</li>
</ol>
