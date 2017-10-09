---
title: "AD v2 JS SPA aaaAzure destekli kurulum - yapılandırma | Microsoft Docs"
description: "JavaScript SPA uygulamaları Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a><span data-ttu-id="77915-103">Uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="77915-103">Register your application</span></span>

<span data-ttu-id="77915-104">Birden çok yol toocreate bir uygulama, Lütfen bunlardan birini seçin:</span><span class="sxs-lookup"><span data-stu-id="77915-104">There are multiple ways toocreate an application, please select one of them:</span></span>

### <a name="option-1-register-your-application-express-mode"></a><span data-ttu-id="77915-105">Seçenek 1: Kayıt uygulamanız (hızlı mod)</span><span class="sxs-lookup"><span data-stu-id="77915-105">Option 1: Register your application (Express mode)</span></span>
<span data-ttu-id="77915-106">Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:</span><span class="sxs-lookup"><span data-stu-id="77915-106">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>

1.  <span data-ttu-id="77915-107">Merhaba aracılığıyla uygulamanızı kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span><span class="sxs-lookup"><span data-stu-id="77915-107">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)</span></span>
2.  <span data-ttu-id="77915-108">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="77915-108">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="77915-109">Merhaba seçeneği emin olmak *destekli Kurulum* denetlenir</span><span class="sxs-lookup"><span data-stu-id="77915-109">Make sure hello option for *Guided Setup* is checked</span></span>
4.  <span data-ttu-id="77915-110">Merhaba yönergeleri tooobtain hello uygulama kimliği izleyin ve kodunuza yapıştırın</span><span class="sxs-lookup"><span data-stu-id="77915-110">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="option-2-register-your-application-advanced-mode"></a><span data-ttu-id="77915-111">Seçenek 2: uygulamanızı (Gelişmiş mod) kaydetme</span><span class="sxs-lookup"><span data-stu-id="77915-111">Option 2: Register your application (Advanced mode)</span></span>

1. <span data-ttu-id="77915-112">Toohello Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app) tooregister uygulama</span><span class="sxs-lookup"><span data-stu-id="77915-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="77915-113">Uygulamanız ve e-posta için bir ad girin</span><span class="sxs-lookup"><span data-stu-id="77915-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="77915-114">Merhaba seçeneği emin olmak *destekli Kurulum* işaretli değil</span><span class="sxs-lookup"><span data-stu-id="77915-114">Make sure hello option for *Guided Setup* is unchecked</span></span>
4.  <span data-ttu-id="77915-115">Tıklatın `Add Platform`sonra seçin`Web`</span><span class="sxs-lookup"><span data-stu-id="77915-115">Click `Add Platform`, then select `Web`</span></span>
5. <span data-ttu-id="77915-116">Merhaba eklemek `Redirect URL` web sunucunuz üzerinde bağlı toohello uygulamanın URL karşılık gelir.</span><span class="sxs-lookup"><span data-stu-id="77915-116">Add hello `Redirect URL` that correspond toohello application's URL based on your web server.</span></span> <span data-ttu-id="77915-117">Hakkında yönergeler için aşağıda Hello bölümlerine bakın tooset / Visual Studio ve Python hello yeniden yönlendirme URL'si edinin.</span><span class="sxs-lookup"><span data-stu-id="77915-117">See hello sections below for instructions on how tooset/ obtain hello redirect URL in Visual Studio and Python.</span></span>
6. <span data-ttu-id="77915-118">Tıklatın *Kaydet*</span><span class="sxs-lookup"><span data-stu-id="77915-118">Click *Save*</span></span>

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="77915-119">Visual Studio yönergeleri almak için yeniden yönlendirme URL'si</span><span class="sxs-lookup"><span data-stu-id="77915-119">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="77915-120">Merhaba yönergeleri tooobtain, yeniden yönlendirme URL'si izleyin:</span><span class="sxs-lookup"><span data-stu-id="77915-120">Follow hello instructions tooobtain your redirect URL:</span></span>
> 1.    <span data-ttu-id="77915-121">İçinde *Çözüm Gezgini*, hello proje seçip hello arayın `Properties` penceresi (Özellikler penceresi görmüyorsanız, basın `F4`)</span><span class="sxs-lookup"><span data-stu-id="77915-121">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="77915-122">Merhaba değerinden kopyalama `URL` toohello Pano:</span><span class="sxs-lookup"><span data-stu-id="77915-122">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="77915-123">![Proje Özellikleri](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="77915-123">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="77915-124">Geçiş geri toohello *uygulama kayıt portalı* hello değeri olarak Yapıştır bir `Redirect URL` ve 'Kaydet' düğmesini tıklatın</span><span class="sxs-lookup"><span data-stu-id="77915-124">Switch back toohello *Application Registration Portal* and paste hello value as a `Redirect URL` and click 'Save'</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="77915-125">Python için ayar yeniden yönlendirme URL'si</span><span class="sxs-lookup"><span data-stu-id="77915-125">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="77915-126">Python için komut satırı aracılığıyla hello web sunucusu bağlantı noktası ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="77915-126">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="77915-127">Bu Destekli Kurulum başlangıç bağlantı noktası 8080 başvurusunu kullanır, ancak tüm diğer bağlantı kullanılabilir boş toouse eşitleyerek.</span><span class="sxs-lookup"><span data-stu-id="77915-127">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="77915-128">Her iki durumda da hello uygulama kayıt bilgileri yönlendirme URL'SİNDE yukarı tooset aşağıda hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="77915-128">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> - <span data-ttu-id="77915-129">Geçiş geri toohello *uygulama kayıt portalı* ve `http://localhost:8080/` olarak bir `Redirect URL`, veya kullanmak `http://localhost:[port]/` özel bir TCP bağlantı noktası kullanıyorsanız, (burada *[bağlantı noktası]* hello özel TCP bağlantı noktası sayı) ve 'Kaydet' düğmesini tıklatın</span><span class="sxs-lookup"><span data-stu-id="77915-129">Switch back toohello *Application Registration Portal* and set `http://localhost:8080/` as a `Redirect URL`, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number) and click 'Save'</span></span>


#### <a name="configure-your-javascript-spa"></a><span data-ttu-id="77915-130">JavaScript SPA yapılandırın</span><span class="sxs-lookup"><span data-stu-id="77915-130">Configure your JavaScript SPA</span></span>

1.  <span data-ttu-id="77915-131">Adlı bir dosya oluşturun `msalconfig.js` hello uygulama kayıt bilgilerini içeren.</span><span class="sxs-lookup"><span data-stu-id="77915-131">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="77915-132">Visual Studio, select hello proje (Proje kök klasöründe) kullanıyorsanız, sağ tıklatın ve seçin: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="77915-132">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="77915-133">Adlandırın`msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="77915-133">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="77915-134">Aşağıdaki kodu tooyour hello eklemek `msalconfig.js` dosyası:</span><span class="sxs-lookup"><span data-stu-id="77915-134">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
<span data-ttu-id="77915-135">Değiştir <code>Enter_the_Application_Id_here</code> hello uygulama kimliği yalnızca kayıtlı sahip</span><span class="sxs-lookup"><span data-stu-id="77915-135">Replace <code>Enter_the_Application_Id_here</code> with hello Application Id you just registered</span></span>
</li>
</ol>
