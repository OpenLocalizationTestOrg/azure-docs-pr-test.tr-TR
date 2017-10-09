---
title: "aaaAzure AD v2 iOS Başlarken - Test | Microsoft Docs"
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
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a>Test iOS uygulamanızdan Microsoft Graph API Hello sorgulama

Tuşuna `Command`  +  `R` toorun hello hello simulator kodda.

![Örnek ekran görüntüsü](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

Tootest hazır olduğunuzda, dokunun *'Microsoft Graph API çağrısı'* ve kullanıcı adı ve parola istendiğinde tootype olacaktır.

### <a name="consent"></a>Onay
Merhaba tooyour uygulamada oturum ilk kez, bir onay ekranı benzer toohello ile aşağıdaki sunulur, ihtiyacınız olduğunda tooexplicitly kabul edin:

![Onay ekranı](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a>Beklenen sonuçları
Kullanıcı profili bilgilerini hello hello Microsoft Graph API çağrısında tarafından döndürülen görmelisiniz *günlüğü* bölümü.

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Kapsamlar ve temsilci izinleri hakkında daha fazla bilgi

Merhaba Microsoft Graph API gerektirir hello `user.read` tooread hello kullanıcının profilini kapsam. Bu kapsam, varsayılan olarak, kayıt portal Kaydedilmekte her uygulama otomatik olarak eklenir. Microsoft Graph için diğer bazı API'leri ve aynı zamanda, arka uç sunucusu için özel API'leri ek kapsamlar gerektirebilir. Örneğin, Microsoft Graph için kapsam hello `Calendars.Read` gerekli toolist hello kullanıcının takvimleri değil. Sırada bir uygulama bağlamında kullanıcının Takvim tooaccess Merhaba, tooadd hello gerek `Calendars.Read` izin toohello uygulama kayıt ait bilgileri temsilcisi ve hello ekleyin `Calendars.Read` kapsam toohello `acquireTokenSilent` çağırın. Kapsam hello sayısı arttıkça hello kullanıcı için ek onayları istenebilir.

<!--end-collapse-->



