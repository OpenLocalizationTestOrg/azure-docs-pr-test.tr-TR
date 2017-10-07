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
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Merhaba uygulamanın kayıt bilgileri tooyour uygulama Ekle

Bu adımda, uygulama kayıt bilgilerinizi tooconfigure hello yeniden yönlendirme URL'si gerekir ve ardından hello uygulama kimliği tooyour JavaScript SPA uygulama ekleyin.

### <a name="configure-redirect-url"></a>Yeniden yönlendirme URL'sini yapılandırın

Merhaba yapılandırma `Redirect URL` alan yukarıda index.html sayfanızın web sunucunuzda hello URL'siyle ve ardından *güncelleştirme*.


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>Visual Studio yönergeleri almak için yeniden yönlendirme URL'si
> tooobtain, yeniden yönlendirme URL'si aşağıdaki hello yönergeleri izleyin:
> 1.    İçinde *Çözüm Gezgini*, hello proje seçip hello arayın `Properties` penceresi (Özellikler penceresi görmüyorsanız, basın `F4`)
> 2.    Merhaba değerinden kopyalama `URL` toohello Pano:<br/> ![Proje Özellikleri](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    Yapıştırma hello değeri olarak bir `Redirect URL` bu sayfayı hello üstte'ye tıklayın`Update`

<p/>

> #### <a name="setting-redirect-url-for-python"></a>Python için ayar yeniden yönlendirme URL'si
> Python için komut satırı aracılığıyla hello web sunucusu bağlantı noktası ayarlayabilirsiniz. Bu Destekli Kurulum başlangıç bağlantı noktası 8080 başvurusunu kullanır, ancak tüm diğer bağlantı kullanılabilir boş toouse eşitleyerek. Her iki durumda da hello uygulama kayıt bilgileri yönlendirme URL'SİNDE yukarı tooset aşağıda hello yönergeleri izleyin:<br/>
> Ayarlama `http://localhost:8080/` olarak bir `Redirect URL` hello bu sayfanın üst kısmında, veya kullanmak `http://localhost:[port]/` özel bir TCP bağlantı noktası kullanıyorsanız, (burada *[bağlantı noktası]* hello özel TCP bağlantı noktası numarası), 'Update' i tıklatın

### <a name="configure-your-javascript-spa-application"></a>JavaScript SPA uygulamanızı yapılandırın

1.  Adlı bir dosya oluşturun `msalconfig.js` hello uygulama kayıt bilgilerini içeren. Visual Studio, select hello proje (Proje kök klasöründe) kullanıyorsanız, sağ tıklatın ve seçin: `Add`  >  `New Item`  >  `JavaScript File`. Adlandırın`msalconfig.js`
2.  Aşağıdaki kodu tooyour hello eklemek `msalconfig.js` dosyası:

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
