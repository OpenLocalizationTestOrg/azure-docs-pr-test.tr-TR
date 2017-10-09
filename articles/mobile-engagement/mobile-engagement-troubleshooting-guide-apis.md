---
title: "aaaAzure Mobile Engagement sorun giderme kılavuzu - API'leri"
description: "Azure Mobile Engagement - API'leri için kılavuzları sorunlarını giderme"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3efc8a52-2b74-4917-b887-815ae8277474
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 10/04/2016
ms.author: piyushjo
ms.openlocfilehash: 5656b6f0f1aaf3e496a168c7cf09b307b9ab2a4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-api-issues"></a>API sorunları için sorun giderme kılavuzu
Merhaba, nasıl yöneticileri Azure Mobile Engagement ile Merhaba API'leri etkileşimde karşılaşabileceğiniz olası sorunlar şunlardır.

## <a name="syntax-issues"></a>Sözdizimi sorunları
### <a name="issue"></a>Sorun
* Merhaba API (ya da beklenmeyen davranışlarla) kullanarak söz dizimi hataları.

### <a name="causes"></a>Neden olur.
* Sözdizimi sorunlar:
  * Emin toocheck hello hello belirli API kullandığınız sözdizimi olun seçeneği hello tooconfirm kullanılabilir.
  * Bir ortak API kullanımı tooconfuse hello Reach API'sini ve hello (görevlerin çoğunu hello Reach API'sini hello itme API yerine ile yapılmalıdır) API anında konudur. 
  * SDK tümleştirmesi ve API kullanımı ile başka bir yaygın sorun tooconfuse hello SDK anahtarı olan ve API anahtarını hello.
  * Toohello API'leri bağlanmak betikleri toosend veri her en az 10 dakika ya da (verilerini dinleme İzleyici API komut ortak özellikle) zaman aşımına uğrar hello bağlantı gerekir. tooprevent zaman aşımları, komut dosyası gönderme XMPP ping her 10 dakikada tookeep hello oturumuna hello sunucuyla Canlı vardır.

### <a name="see-also"></a>Ayrıca bkz.
* [API belgeleri][Link 4]
* [XMPP protokol bilgileri](http://xmpp.org/extensions/xep-0199.html)

## <a name="unable-toouse-hello-api-tooperform-hello-same-action-available-in-hello-azure-mobile-engagement-ui"></a>%S toouse hello API tooperform hello aynı eylemin hello Azure Mobile Engagement UI kullanılabilir
### <a name="issue"></a>Sorun
* Azure Mobile Engagement UI hello işe yaramazsa hello gelen çalışır bir eylem Azure Mobile Engagement API ilgili.

### <a name="causes"></a>Neden olur.
* Aynı hello Azure Mobile Engagement UI eyleminden gösterir ile Azure Mobile Engagement'ın bu özelliği doğru bir şekilde tümleştirilmiş hello gerçekleştirebilirsiniz onaylayan hello SDK.

### <a name="see-also"></a>Ayrıca bkz.
* [UI belgeleri][Link 1]

## <a name="error-messages"></a>Hata iletileri
### <a name="issue"></a>Sorun
* Hata kodları çalışma zamanında ya da günlükleri görüntülenen hello API'yi kullanma.

### <a name="causes"></a>Neden olur.
* Başvuru ve ön sorun giderme için ortak API durum kodları numaraları bileşik listesi aşağıdadır:
  
        200        Success.
        200        Account updated: device registered, associated, updated, or removed from hello current account.
        200        Returns a list of projects as a JSON object or an authentication token generated and returned in hello response’s body.
        201        Account created.
        400        Invalid parameter or validation exception (check payload for details). hello parameters provided toohello API or service are invalid. In this case, hello HTTP response will embed more details. Make sure tootest for hello MIME type of hello response as hello payload can either be plain text or a JSON object.
        401        Authentication error. No user is currently authenticated or connected (check hello AppID and SDK key).
        402        Billing lock. hello application is either off its quotas or is currently in a bad billing state.
        403        hello application is not enabled or hello specific API is disabled for this application.
        403        Unauthorized access toohello project or application, invalid access key (hello key must match hello one provided when created).
        403        Campaign specific errors: campaign must be finished (or has already been activated), hello suspend action can only be performed on an scheduled campaign, cannot finish a campaign that is not currently “in progress”, campaign must be “in progress” and hello campaign’s property named, manual Push must be set tootrue.
        403        hello email address is already associated tooanother account (a super user for instance). No authentication token will be generated.
        404        Application, device, campaign, or project identifier not found.
        404        Query parameter is invalid JSON or has a field with an unexpected value.
        404        hello email address is not associated with an account. Please create or update hello account first.
        405        Invalid HTTP method (GET, POST, etc.) or trying tooedit a read only segment (i.e. add or update or delete a criterion). A segment becomes read only after it has been computed for hello first time.
        409        Name already associated tooa different device ID or campaign.
        413        Too many device identifiers (current limit is 1,000), POST URL encoded entity is over 2MB, or hello period is too large toobe displayed (hello server didn’t retrieve hello analytics because hello user request is for a period that is too large).
        503        Analytics not available yet (hello requested information is not computed yet for an application).
        504        hello server was not able toohandle your request in a reasonable time (if you make multiple calls tooan API very quickly, try toomake one call at a time and spread hello calls out over time).

### <a name="see-also"></a>Ayrıca bkz.
* [-Her belirli API ayrıntılı hataları için API belgeleri][Link 4]

## <a name="silent-failures"></a>Sessiz hataları
### <a name="issue"></a>Sorun
* API Eylem günlükleri ya da çalışma zamanında görüntülenen hiçbir hata iletisiyle başarısız olur.

### <a name="causes"></a>Neden olur.
* Çok sayıda öğe doğru tümleşik değildir ancak API, hello sessizce başarısız olur, Azure Mobile Engagement UI şekilde anımsa hello devre dışı bırakılacak tootest hello hello UI toosee aynı işlevinden çalışırsa.
* Azure Mobile Engagement ve birçok gelişmiş özelliklerini Azure Mobile Engagement toouse, gerek toobe kullanabilmek için önce ayrı ayrı ayrı adımlardan hello SDK'sı ile uygulamanızı içine tümleştirilmiştir çalışıyorsunuz.

### <a name="see-also"></a>Ayrıca bkz.
* [Sorun giderme kılavuzu - SDK][Link 25]

<!--Link references-->
[Link 1]: mobile-engagement-user-interface-home.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

