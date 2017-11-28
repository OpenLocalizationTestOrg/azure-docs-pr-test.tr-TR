---
title: "aaaAzure AD v2 JS SPA destekli Kurulumu - yapılandırın (ARP) | Microsoft Docs"
description: "JavaScript SPA uygulamaları Azure Active Directory v2 bitiş noktası tarafından (ARP) erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
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
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="0d55c-103">Merhaba uygulamanın kayıt bilgileri tooyour uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="0d55c-103">Add hello application’s registration information tooyour App</span></span>

<span data-ttu-id="0d55c-104">Bu adımda, uygulama kayıt bilgilerinizi tooconfigure hello yeniden yönlendirme URL'si gerekir ve ardından hello uygulama kimliği tooyour JavaScript SPA uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0d55c-104">In this step, you need tooconfigure hello Redirect URL of your application registration information and then add hello Application Id tooyour JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="0d55c-105">Yeniden yönlendirme URL'sini yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0d55c-105">Configure redirect URL</span></span>

<span data-ttu-id="0d55c-106">Merhaba yapılandırma `Redirect URL` alan yukarıda index.html sayfanızın web sunucunuzda hello URL'siyle ve ardından *güncelleştirme*.</span><span class="sxs-lookup"><span data-stu-id="0d55c-106">Configure hello `Redirect URL` field above with hello URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="0d55c-107">Visual Studio yönergeleri almak için yeniden yönlendirme URL'si</span><span class="sxs-lookup"><span data-stu-id="0d55c-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="0d55c-108">tooobtain, yeniden yönlendirme URL'si aşağıdaki hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="0d55c-108">tooobtain your redirect URL, follow hello instructions below:</span></span>
> 1.    <span data-ttu-id="0d55c-109">İçinde *Çözüm Gezgini*, hello proje seçip hello arayın `Properties` penceresi (Özellikler penceresi görmüyorsanız, basın `F4`)</span><span class="sxs-lookup"><span data-stu-id="0d55c-109">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="0d55c-110">Merhaba değerinden kopyalama `URL` toohello Pano:</span><span class="sxs-lookup"><span data-stu-id="0d55c-110">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="0d55c-111">![Proje Özellikleri](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="0d55c-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="0d55c-112">Yapıştırma hello değeri olarak bir `Redirect URL` bu sayfayı hello üstte'ye tıklayın`Update`</span><span class="sxs-lookup"><span data-stu-id="0d55c-112">Paste hello value as a `Redirect URL` on hello top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="0d55c-113">Python için ayar yeniden yönlendirme URL'si</span><span class="sxs-lookup"><span data-stu-id="0d55c-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="0d55c-114">Python için komut satırı aracılığıyla hello web sunucusu bağlantı noktası ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d55c-114">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="0d55c-115">Bu Destekli Kurulum başlangıç bağlantı noktası 8080 başvurusunu kullanır, ancak tüm diğer bağlantı kullanılabilir boş toouse eşitleyerek.</span><span class="sxs-lookup"><span data-stu-id="0d55c-115">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="0d55c-116">Her iki durumda da hello uygulama kayıt bilgileri yönlendirme URL'SİNDE yukarı tooset aşağıda hello yönergeleri izleyin:</span><span class="sxs-lookup"><span data-stu-id="0d55c-116">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> <span data-ttu-id="0d55c-117">Ayarlama `http://localhost:8080/` olarak bir `Redirect URL` hello bu sayfanın üst kısmında, veya kullanmak `http://localhost:[port]/` özel bir TCP bağlantı noktası kullanıyorsanız, (burada *[bağlantı noktası]* hello özel TCP bağlantı noktası numarası), 'Update' i tıklatın</span><span class="sxs-lookup"><span data-stu-id="0d55c-117">Set `http://localhost:8080/` as a `Redirect URL` on hello top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="0d55c-118">JavaScript SPA uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="0d55c-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="0d55c-119">Adlı bir dosya oluşturun `msalconfig.js` hello uygulama kayıt bilgilerini içeren.</span><span class="sxs-lookup"><span data-stu-id="0d55c-119">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="0d55c-120">Visual Studio, select hello proje (Proje kök klasöründe) kullanıyorsanız, sağ tıklatın ve seçin: `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="0d55c-120">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="0d55c-121">Adlandırın`msalconfig.js`</span><span class="sxs-lookup"><span data-stu-id="0d55c-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="0d55c-122">Aşağıdaki kodu tooyour hello eklemek `msalconfig.js` dosyası:</span><span class="sxs-lookup"><span data-stu-id="0d55c-122">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
