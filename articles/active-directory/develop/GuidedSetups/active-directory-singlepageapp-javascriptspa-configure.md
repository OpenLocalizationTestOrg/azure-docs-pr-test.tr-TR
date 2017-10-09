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
## <a name="register-your-application"></a>Uygulamanızı kaydetme

Birden çok yol toocreate bir uygulama, Lütfen bunlardan birini seçin:

### <a name="option-1-register-your-application-express-mode"></a>Seçenek 1: Kayıt uygulamanız (hızlı mod)
Merhaba uygulamanızda tooregister gereksinim artık *Microsoft uygulama kayıt portalı*:

1.  Merhaba aracılığıyla uygulamanızı kaydetme [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)
2.  Uygulamanız ve e-posta için bir ad girin
3.  Merhaba seçeneği emin olmak *destekli Kurulum* denetlenir
4.  Merhaba yönergeleri tooobtain hello uygulama kimliği izleyin ve kodunuza yapıştırın

### <a name="option-2-register-your-application-advanced-mode"></a>Seçenek 2: uygulamanızı (Gelişmiş mod) kaydetme

1. Toohello Git [Microsoft uygulama kayıt portalı](https://apps.dev.microsoft.com/portal/register-app) tooregister uygulama
2. Uygulamanız ve e-posta için bir ad girin 
3. Merhaba seçeneği emin olmak *destekli Kurulum* işaretli değil
4.  Tıklatın `Add Platform`sonra seçin`Web`
5. Merhaba eklemek `Redirect URL` web sunucunuz üzerinde bağlı toohello uygulamanın URL karşılık gelir. Hakkında yönergeler için aşağıda Hello bölümlerine bakın tooset / Visual Studio ve Python hello yeniden yönlendirme URL'si edinin.
6. Tıklatın *Kaydet*

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Visual Studio yönergeleri almak için yeniden yönlendirme URL'si
> Merhaba yönergeleri tooobtain, yeniden yönlendirme URL'si izleyin:
> 1.    İçinde *Çözüm Gezgini*, hello proje seçip hello arayın `Properties` penceresi (Özellikler penceresi görmüyorsanız, basın `F4`)
> 2.    Merhaba değerinden kopyalama `URL` toohello Pano:<br/> ![Proje Özellikleri](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Geçiş geri toohello *uygulama kayıt portalı* hello değeri olarak Yapıştır bir `Redirect URL` ve 'Kaydet' düğmesini tıklatın

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Python için ayar yeniden yönlendirme URL'si
> Python için komut satırı aracılığıyla hello web sunucusu bağlantı noktası ayarlayabilirsiniz. Bu Destekli Kurulum başlangıç bağlantı noktası 8080 başvurusunu kullanır, ancak tüm diğer bağlantı kullanılabilir boş toouse eşitleyerek. Her iki durumda da hello uygulama kayıt bilgileri yönlendirme URL'SİNDE yukarı tooset aşağıda hello yönergeleri izleyin:<br/>
> - Geçiş geri toohello *uygulama kayıt portalı* ve `http://localhost:8080/` olarak bir `Redirect URL`, veya kullanmak `http://localhost:[port]/` özel bir TCP bağlantı noktası kullanıyorsanız, (burada *[bağlantı noktası]* hello özel TCP bağlantı noktası sayı) ve 'Kaydet' düğmesini tıklatın


#### <a name="configure-your-javascript-spa"></a>JavaScript SPA yapılandırın

1.  Adlı bir dosya oluşturun `msalconfig.js` hello uygulama kayıt bilgilerini içeren. Visual Studio, select hello proje (Proje kök klasöründe) kullanıyorsanız, sağ tıklatın ve seçin: `Add`  >  `New Item`  >  `JavaScript File`. Adlandırın`msalconfig.js`
2.  Aşağıdaki kodu tooyour hello eklemek `msalconfig.js` dosyası:

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
Değiştir <code>Enter_the_Application_Id_here</code> hello uygulama kimliği yalnızca kayıtlı sahip
</li>
</ol>
