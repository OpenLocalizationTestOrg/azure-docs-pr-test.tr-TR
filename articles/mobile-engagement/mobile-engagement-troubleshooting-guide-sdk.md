---
title: "aaaAzure Mobile Engagement sorun giderme kılavuzu - SDK"
description: "Azure Mobile Engagement SDK tümleştirmesi sorunlarını giderme"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a>SDK tümleştirme sorunları için sorun giderme kılavuzu
Merhaba, nasıl Azure Mobile Engagement uygulamanıza ile tümleşir karşılaşabileceğiniz olası sorunlar şunlardır.

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a>Bir hata, uygulamanızın başka bir alan keşfedilen SDK sorunları
### <a name="issue"></a>Sorun
* UI veri toplama hatası (Analytics, izleme, Segment veya panolar).
* Hataları gönderme (uygulama ya da her ikisini de dışında uygulamasında iter çalışmıyor).
* Özellik hataları (izleme, coğrafi konuma veya belirli iter çalışmıyor platform) Gelişmiş.
* API hataları (API'leri başarısız genellikle hata iletileri olmadan sessizce).
* Hizmet hataları (hiçbiri Azure Mobile Engagement uygulamanız için çalışır).

### <a name="causes"></a>Neden olur.
* Hello Azure Mobile Engagement SDK'sı ile çözümlenen toobe gereken çoğu sorunlar uygulamanız (örneğin, bir kullanıcı Arabirimi veri toplama hatası, gönderme hatası, gelişmiş özellik hatası, API hatası, uygulama kilitlenmelerine veya görünen hizmet bir hata bulunan Kesinti).  
* Azure Mobile Engagement, belirli bir özellik, hiçbir zaman uygulamanızda önce çalıştıysa toocomplete hello tümleştirme gerekir. 
* Azure Mobile Engagement, belirli bir özellik çalıştığı ve durdurulmuş, tooupgrade toohello son sürümü hello Azure Mobile Engagement SDK'sı ile gerekebilir. Hello Azure Mobile Engagement SDK'sı (Android, iOS, Windows ve Windows Phone) Azure Mobile Engagement tarafından desteklenen her platform için farklı bir sürümü olduğunu unutmayın.

#### <a name="sdk-integration"></a>SDK Tümleştirmesi
* Azure Mobile Engagement SDK'yı (Analytics) doğru biçimde tümleşik.
* SDK (uygulama içinde ve dışında uygulama iter) doğru biçimde tümleşik ulaşabilirsiniz.
* Süresi dolmuş veya hatalı ürün vs sertifika. Geliştirme (yalnızca iOS).
* GCM veya ADM SDK'da tümleşik doğru biçimde (Android yalnızca - hizmet belirli iter).
* Doğru biçimde izleme SDK (yükleme deposu izleme) tümleşiktir.
* Yavaş veya GPS yerleşimine SDK (hedefleme coğrafi konuma göre) doğru biçimde tümleşik.

**Ayrıca bkz.:**

* [SDK Belgeleri - tümleştirme kılavuzları][Link 5] 
* [Sorun giderme kılavuzu - gönderme][Link 23]

#### <a name="sdk-upgrade"></a>SDK yükseltme
* Tooupgrade SDK tooresolve sorunlarının hello SDK'sı (Merhaba aygıt işletim sistemi sürümleri genellikle ilgili toonewer) daha eski sürümleriyle gerekir.
* Aygıtınızdan uygulamanızı önceki tüm sürümlerini kaldırın ve hello uygulamanızı en yeni sürümünü yükleyin, hello hello Azure Mobile Engagement UI tooconfirm Cihazınızı hello en yeni sürümü, uygulamanızın kullanıyor, cihaz kimliği yeniden kaydedin.

**Ayrıca bkz.:**

* [SDK Belgeleri - sürüm notları](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [SDK Belgeleri - yükseltme kılavuzları](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a>SDK diğer
* Azure Mobile Engagement uygulama bildirimi "AndroidManifest.xml" hatalara neden olabilir toowork (yalnızca Android).
* SDK tümleştirmesi ve API kullanımı ile yaygın bir sorun tooconfuse hello SDK anahtarı olan ve API anahtarını hello.

**Ayrıca bkz.:**

* [Kavramlar - sözlüğü][Link 6]

## <a name="advanced-coding-issues"></a>Sorunları kodlama Gelişmiş
### <a name="issue"></a>Sorun
* Platform özel kod doğrudan Mobile Engagement, iOS, Android ve Windows Phone sorunlara neden olabilir tooAzure ilgili.

### <a name="causes"></a>Neden olur.
* Birçok Azure Mobile Engagement kodlama sorunları Gelişmiş nedeni yanlış yazılan platformu tarafından belirli bir kod tooAzure Mobile Engagement doğrudan ilgili. Tooconsult belgeleri belirli toohello platform için ayrıca tooAzure Mobile Engagement belgeleri (Android, iOS, Web, Windows ve Windows Phone) geliştirdiğinize gerekir.
* Doğru biçimde "Kategoriler" yapılandırma, bir bildirim tooanother konumdan içinde veya dışında hello uygulaması (yalnızca Android) bağlama engeller. 
* "UIKit.framework" çok "isteğe bağlı" "simgesi bulunamadı hatası" gösterir, iOS kodunuzda ayarı bulunamadı ve/veya eski iOS cihazlarda (yalnızca iOS) çöküyor.
* Süresi dolan sertifikaları veya doğru biçimde hello geliştirme veya üretim hello cert sürümünü kullanarak, nedenleri itme (yalnızca iOS) verir.
* (Merhaba system center için uygulamanın oturumunu işleyişi Android ve iOS iter gibi), Azure Mobile Engagement denetleyemezsiniz bazı sınırlamalar devralınan tooa platformu vardır.
* Azure Mobile Engagement tam başvuru için iOS ve Android için Azure Mobile Engagement tarafından kullanılan hello iç paketlerin listesini yayımlar. Azure Mobile Engagement özelliklerinden bazıları belirli toohello platform (Android, iOS, Web, Windows ve Windows Phone) olduğunu unutmayın.

### <a name="see-also"></a>Ayrıca bkz.
* [Sorun giderme kılavuzu - gönderme][Link 23] 
* [SDK Belgeleri - sürüm notları][Link 5]
* [SDK Belgeleri - yükseltme kılavuzları][Link 5]

## <a name="application-crashes"></a>Uygulama çökme (Crash)
### <a name="issue"></a>Sorun
* Uygulamanızı hello son kullanıcıların cihazda çöküyor.

### <a name="causes"></a>Neden olur.
* Kilitlenme bilgi hello görüntülenebilir *Analytics UI* veya hello *Analytics API*
* Cihaz kimliği test aygıtınızın hello ve hello ele bulabilir bir son kullanıcı toohelp için uygulama toocrash neden aynı eylemi, kilitlenme hello nedenini tanımlayın.
* Uygulamaları toocrash neden ile ilgili bilinen sorunlar hello Azure Mobile Engagement SDK'sı bazen toohello hello SDK en son sürümüne yükseltme tarafından çözümlenir. Platformunuz hakkında emin toocheck hello sürüm notları, kilitlenme araştırırken olun.

### <a name="see-also"></a>Ayrıca bkz.
* [SDK Belgeleri - sürüm notları][Link 5]
* [SDK Belgeleri - yükseltme kılavuzları][Link 5]

## <a name="app-store-upload-failures"></a>Uygulama mağazası karşıya yükleme hataları
### <a name="issue"></a>Sorun
* Toouploading hello en son sürümünü uygulama tooApple, Google veya hello Windows uygulama mağazası ilgili hatalarla ilgili.

### <a name="causes"></a>Neden olur.
* Uygulama mağazaları bazen belirli özellikleri etkin blok uygulamalar (örneğin hello Apple Store hello kullanımında IDFV hello Mağazası'ndaki uygulamaların ve hello GooglePlay deposu engeller uygulamalar arasında uygulama bilgilerinin hello paylaşımı). 
* Bir uygulama toohello deposu karşıya güçlük çekiyorsanız hello sürüm notları platform ve hello SDK geçerli sürümü hakkında denetlediğinizden emin olun.

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
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

