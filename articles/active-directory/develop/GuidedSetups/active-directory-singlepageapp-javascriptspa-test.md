---
title: aaaAzure AD v2 JS SPA destekli Kurulumu - Test | Microsoft Docs
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
ms.openlocfilehash: b2339431a070b5c4ad4058e6c1a9b19b83c84c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Kodunuzu test

> ### <a name="testing-with-visual-studio"></a>Visual Studio ile test etme
> Visual Studio kullanıyorsanız, basın `F5` toorun projenizi: hello tarayıcı açılır ve çok yönlendirir*http://localhost: {port}* hello gördüğünüz *Microsoft Graph API çağrısı* düğmesi.

<p/><!-- -->

> ### <a name="testing-with-python-or-another-web-server"></a>Python veya başka bir web sunucusu ile test etme
> Visual Studio kullanmıyorsanız, web sunucunuz başlatılır ve yapılandırıldığından emin olun toolisten tooa TCP bağlantı noktası tabanlı hello içeren klasör, *index.html* dosya. Python için dinleme başlatabilirsiniz çalıştırarak toohello bağlantı noktası hello hello uygulamanın klasöründen hello komut istemi / terminal, içinde:
> 
> ```bash
> python -m http.server 8080
> ```
>  Ardından, hello tarayıcı açıp *http://localhost: 8080* veya *http://localhost: {port}* - hello burada *bağlantı noktası* web sunucunuz toohello bağlantı noktası karşılık gelen dinleme. İndex.html sayfanızı hello ile Merhaba içeriğine görmelisiniz *Microsoft Graph API çağrısı* düğmesi.

## <a name="test-your-application"></a>Uygulamanızı test edin

Sonra Hello tarayıcı yükler, *index.html*, hello tıklatın *Microsoft Graph API çağrısı* düğmesi. Bu hello ilk kez kullanıyorsanız, hello tarayıcı yeniden yönlendirmeleri olduğunuz, toohello Microsoft Azure Active Directory v2 uç noktası, toosign içinde istenir.
 
![Örnek ekran görüntüsü](media/active-directory-singlepageapp-javascriptspa-test/javascriptspascreenshot1.png)


### <a name="consent"></a>Onay
Merhaba tooyour uygulamada oturum çok ilk kez, bir onay ekranı benzer toohello aşağıdakileri ile tooaccept ihtiyaç duyacağınız sunulur:

 ![Onay ekranı](media/active-directory-singlepageapp-javascriptspa-test/javascriptspaconsent.png)


### <a name="expected-results"></a>Beklenen sonuçları
Kullanıcı profili bilgilerini Microsoft Graph API çağrısı yanıt hello tarafından döndürülen görmeniz gerekir.
 
 ![Sonuçlar](media/active-directory-singlepageapp-javascriptspa-test/javascriptsparesults.png)

Hello edinilen hello belirteci hakkındaki temel bilgileri de görebilirsiniz *erişim belirteci* ve *belirteç talep kimliği* kutuları.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Kapsamlar ve temsilci izinleri hakkında daha fazla bilgi

Merhaba Microsoft Graph API gerektirir hello `user.read` tooread hello kullanıcının profilini kapsam. Bu kapsam, varsayılan olarak, kayıt portal Kaydedilmekte her uygulama otomatik olarak eklenir. Microsoft Graph için diğer bazı API'leri ve aynı zamanda, arka uç sunucusu için özel API'leri ek kapsamlar gerektirebilir. Örneğin, Microsoft Graph için kapsam hello `Calendars.Read` gerekli toolist hello kullanıcının takvimleri değil. Sırada bir uygulama hello bağlamında kullanıcının Takvim tooaccess Merhaba, tooadd hello gerek `Calendars.Read` izin toohello uygulama kayıt ait bilgileri temsilcisi ve hello ekleyin `Calendars.Read` kapsam toohello `acquireTokenSilent` çağırın. Kapsam hello sayısı arttıkça hello kullanıcı için ek onayları istenebilir.

Arka uç API'si (önerilmez) bir kapsam gerektirmiyorsa hello kullanabilirsiniz `clientId` hello hello kapsamda olarak `acquireTokenSilent` ve/veya `acquireTokenRedirect` çağrıları.

<!--end-collapse-->
