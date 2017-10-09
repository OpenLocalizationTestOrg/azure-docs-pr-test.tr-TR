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
## <a name="create-an-application-express"></a><span data-ttu-id="11e6e-103">(Hızlı) uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="11e6e-103">Create an application (Express)</span></span>
<span data-ttu-id="11e6e-104">Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="11e6e-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="11e6e-105">Merhaba aracılığıyla uygulamanızı kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="11e6e-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="11e6e-106">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="11e6e-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="11e6e-107">Kurulum destekli Hello seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="11e6e-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="11e6e-108">Merhaba yönergeleri tooobtain hello uygulama kimliği izleyin ve kodunuza yapıştırın</span><span class="sxs-lookup"><span data-stu-id="11e6e-108">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="11e6e-109">Uygulama kayıt bilgileri tooyour çözümünüz (Gelişmiş) ekleyin</span><span class="sxs-lookup"><span data-stu-id="11e6e-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="11e6e-110">Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="11e6e-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="11e6e-111">Toohello Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app) tooregister uygulama</span><span class="sxs-lookup"><span data-stu-id="11e6e-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="11e6e-112">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="11e6e-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="11e6e-113">Destekli kurulumu için Hello seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="11e6e-113">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="11e6e-114">Tıklatın `Add Platform`seçeneğini belirleyip `Native Application` ve kaydetme ulaştı.</span><span class="sxs-lookup"><span data-stu-id="11e6e-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="11e6e-115">Açık `MainActivity` (altında `app`  >  `java`  >   *`{host}.{namespace}`* )</span><span class="sxs-lookup"><span data-stu-id="11e6e-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="11e6e-116">Hello yerine *[hello uygulama kodu buraya girin]* başlayarak hello satırdaki `final static String CLIENT_ID` yalnızca kayıtlı hello uygulama kimliği:</span><span class="sxs-lookup"><span data-stu-id="11e6e-116">Replace hello *[Enter hello application Id here]* in hello line starting with `final static String CLIENT_ID` with hello application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter hello application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="11e6e-117">Açık `AndroidManifest.xml` (altında `app`  >  `manifests`) etkinlik çok aşağıdaki Ekle hello`manifest\application` düğümü.</span><span class="sxs-lookup"><span data-stu-id="11e6e-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add hello following activity too`manifest\application` node.</span></span> <span data-ttu-id="11e6e-118">Bu kayıtları bir `BrowserTabActivity` tooallow hello kimlik doğrulama işlemini tamamladıktan sonra uygulamanız işletim sistemi tooresume hello:</span><span class="sxs-lookup"><span data-stu-id="11e6e-118">This registers a `BrowserTabActivity` tooallow hello OS tooresume your application after completing hello authentication:</span></span>
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
<span data-ttu-id="11e6e-119">Merhaba, `BrowserTabActivity`, yerine `[Enter hello application Id here]` hello uygulama kimliğiyle</span><span class="sxs-lookup"><span data-stu-id="11e6e-119">In hello `BrowserTabActivity`, replace `[Enter hello application Id here]` with hello application ID.</span></span>
</li>
</ol>
