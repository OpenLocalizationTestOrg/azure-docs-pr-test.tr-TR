---
title: "Azure AD v2 Android alma başlatıldı - yapılandırma | Microsoft Docs"
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
ms.openlocfilehash: 945b09ccdb7537987da33d32d94a3ccacd829ffd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="601f3-103">(Hızlı) uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="601f3-103">Create an application (Express)</span></span>
<span data-ttu-id="601f3-104">Uygulamanızı kaydetmeniz gerekir artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="601f3-104">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="601f3-105">Uygulamanızı aracılığıyla kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span><span class="sxs-lookup"><span data-stu-id="601f3-105">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=android&step=configure)</span></span>
2.  <span data-ttu-id="601f3-106">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="601f3-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="601f3-107">Kurulum destekli seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="601f3-107">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="601f3-108">Uygulama Kimliğini almak ve kodunuza yapıştırmak için yönergeleri izleyin</span><span class="sxs-lookup"><span data-stu-id="601f3-108">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="601f3-109">Uygulama kayıt bilgilerinizi çözümünüze (Gelişmiş) ekleyin</span><span class="sxs-lookup"><span data-stu-id="601f3-109">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="601f3-110">Uygulamanızı kaydetmeniz gerekir artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="601f3-110">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="601f3-111">Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app) bir uygulamayı kaydetmek için</span><span class="sxs-lookup"><span data-stu-id="601f3-111">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="601f3-112">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="601f3-112">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="601f3-113">Destekli kurulumu için seçeneğinin işaretli olduğundan emin olun</span><span class="sxs-lookup"><span data-stu-id="601f3-113">Make sure the option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="601f3-114">Tıklatın `Add Platform`seçeneğini belirleyip `Native Application` ve kaydetme ulaştı.</span><span class="sxs-lookup"><span data-stu-id="601f3-114">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5.  <span data-ttu-id="601f3-115">Açık `MainActivity` (altında `app`  >  `java`  >   *`{host}.{namespace}`* )</span><span class="sxs-lookup"><span data-stu-id="601f3-115">Open `MainActivity` (under `app` > `java` > *`{host}.{namespace}`*)</span></span>
6.  <span data-ttu-id="601f3-116">Değiştir *[uygulama kimliği buraya girin]* başlayarak satırında `final static String CLIENT_ID` yalnızca kayıtlı uygulama kimliği:</span><span class="sxs-lookup"><span data-stu-id="601f3-116">Replace the *[Enter the application Id here]* in the line starting with `final static String CLIENT_ID` with the application ID you just registered:</span></span>

```java
final static String CLIENT_ID = "[Enter the application Id here]";
```
<!-- Workaround for Docs conversion bug -->
<ol start="7">
<li>
<span data-ttu-id="601f3-117">Açık `AndroidManifest.xml` (altında `app`  >  `manifests`) aşağıdaki etkinlik eklemek `manifest\application` düğümü.</span><span class="sxs-lookup"><span data-stu-id="601f3-117">Open `AndroidManifest.xml` (under `app` > `manifests`) Add the following activity to `manifest\application` node.</span></span> <span data-ttu-id="601f3-118">Bu kayıtları bir `BrowserTabActivity` uygulamanızın kimlik doğrulamasını tamamladıktan sonra devam etmek işletim sistemi izin vermek için:</span><span class="sxs-lookup"><span data-stu-id="601f3-118">This registers a `BrowserTabActivity` to allow the OS to resume your application after completing the authentication:</span></span>
</li>
</ol>

```xml
<!--Intent filter to capture System Browser calling back to our app after Sign In-->
<activity
    android:name="com.microsoft.identity.client.BrowserTabActivity">
    <intent-filter>
        <action android:name="android.intent.action.VIEW" />
        <category android:name="android.intent.category.DEFAULT" />
        <category android:name="android.intent.category.BROWSABLE" />
        
        <!--Add in your scheme/host from registered redirect URI-->
        <!--By default, the scheme should be similar to 'msal[appId]' -->
        <data android:scheme="msal[Enter the application Id here]"
            android:host="auth" />
    </intent-filter>
</activity>
```
<!-- Workaround for Docs conversion bug -->
<ol start="8">
<li>
<span data-ttu-id="601f3-119">İçinde `BrowserTabActivity`, yerine `[Enter the application Id here]` uygulama kimliğiyle</span><span class="sxs-lookup"><span data-stu-id="601f3-119">In the `BrowserTabActivity`, replace `[Enter the application Id here]` with the application ID.</span></span>
</li>
</ol>
