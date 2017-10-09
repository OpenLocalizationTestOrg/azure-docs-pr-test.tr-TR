---
title: "aaaAzure AD v2 Windows Masaüstü Getting Started - Test | Microsoft Docs"
description: "Windows Masaüstü .NET (XAML) uygulamaları, Azure Active Directory v2 bitiş noktası tarafından erişim belirteçleri gerektiren bir API nasıl çağırabilirsiniz"
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
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>Kodunuzu test

İçinde uygulamanızın tuşuna tootest sipariş `F5` toorun projenizi Visual Studio'da. Ana penceresi görünmelidir:

![Örnek ekran görüntüsü](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

Hazır tootest olduğunuzda tıklatın *Microsoft Graph API çağrısı* ve bir Microsoft Azure Active Directory (kuruluş hesabı) veya bir Microsoft Account (live.com, outlook.com) hesap toosign de kullanabilirsiniz. Bu ilk kez hello ise, kullanıcı toosign isteyen bir pencere görürsünüz:

![oturum açma](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a>Onay
Merhaba tooyour uygulamada oturum ilk kez, bir onay ekranı benzer toohello ile aşağıdaki sunulur, ihtiyacınız olduğunda tooexplicitly kabul edin:

![Onay ekranı](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a>Beklenen sonuçları
Kullanıcı profili bilgilerini hello API çağrısı sonuçları ekranda hello Microsoft Graph API çağrısı tarafından döndürülen görmeniz gerekir.

Merhaba belirteci aracılığıyla edinilen hakkında temel bilgiler görmeniz gerekir `AcquireTokenAsync` veya `AcquireTokenSilentAsync` hello belirteci bilgisi kutusunda:

|Özellik  |Biçimi  |Açıklama |
|---------|---------|---------|
|Ad | {Tam} kullanıcı adı |Merhaba kullanıcı adı ve Soyadı|
|Kullanıcı adı |<span>user@domain.com</span> |kullanılan tooidentify hello kullanıcı Hello kullanıcı adı|
|Belirtecinin süresi |{DateTime}         |hangi hello üzerinde belirteci hello ne kadar süre. MSAL hello sona erme tarihi sizin için hello belirteci gerektiğinde yenileyerek uzatır|
|erişim belirteci |{Dize}         |bir yetkilendirme üst bilgisi gerektiren tooHTTP istekleri gönderilecek Hello belirteç dizesini gönderilen|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>Kapsamlar ve temsilci izinleri hakkında daha fazla bilgi
Grafik API'si gerektirir hello `user.read` kapsam tooread kullanıcı profili. Bu kapsam, varsayılan olarak, kayıt portal Kaydedilmekte her uygulama otomatik olarak eklenir. Bazı diğer grafik API'leri yanı sıra, arka uç sunucusu için özel API'leri ek kapsamlar gerektirir. Örneğin, bir grafik `Calendars.Read` gerekli toolist kullanıcının takvimleri değil. Sırada bir uygulama bağlamında kullanıcının Takvim tooaccess Merhaba, tooadd gerek `Calendars.Read` uygulama kaydı'nın bilgi temsilci ve ardından ekleyin `Calendars.Read` toohello `AcquireTokenAsync` çağırın. Kapsam hello sayısı arttıkça, kullanıcı için ek onayları istenebilir.

<!--end-collapse-->



