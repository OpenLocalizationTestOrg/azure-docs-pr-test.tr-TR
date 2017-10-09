---
title: aaaAzure AD v2 Android Getting Started - Test | Microsoft Docs
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Kodunuzu test

1. Kod tooyour Aygıt/Öykünücüsü dağıtın.
2. Tootest hazır olduğunuzda, bir Microsoft Azure Active Directory (kuruluş hesabı) veya bir Microsoft Account (live.com, outlook.com) hesabı toosign içinde kullanın. 

![Örnek ekran görüntüsü](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
<br/><br/>
![Oturum açma](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)

### <a name="consent"></a>Onay
Merhaba tooyour uygulamada bir kullanıcı oturum açtığında ilk kez bunlar bir onay ekranı benzer toohello ile aşağıdaki sunulur, gereksinim duydukları burada tooexplicitly kabul edin: 

![Onay](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a>Beklenen sonuçları
'Me' hello çağrısı tooMicrosoft grafik API'si sonuçlarını görmeniz gerekir uç nokta kullanılan tootooobtain hello kullanıcı profili - https://graph.microsoft.com/v1.0/me. Genel Microsoft Graph uç noktaları listesi için lütfen bu bakın [makale](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries).

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Kapsamlar ve temsilci izinleri hakkında daha fazla bilgi

Merhaba Microsoft Graph API gerektirir hello `user.read` tooread hello kullanıcının profilini kapsam. Bu kapsam, varsayılan olarak, kayıt portal Kaydedilmekte her uygulama otomatik olarak eklenir. Microsoft Graph için diğer bazı API'leri ve aynı zamanda, arka uç sunucusu için özel API'leri ek kapsamlar gerektirebilir. Örneğin, Microsoft Graph için kapsam hello `Calendars.Read` gerekli toolist hello kullanıcının takvimleri değil. Sırada bir uygulama bağlamında kullanıcının Takvim tooaccess Merhaba, tooadd hello gerek `Calendars.Read` izin toohello uygulama kayıt ait bilgileri temsilcisi ve hello ekleyin `Calendars.Read` kapsam toohello `acquireTokenSilentAsync` çağırın. Kapsam hello sayısı arttıkça hello kullanıcı için ek onayları istenebilir.

<!--end-collapse-->
