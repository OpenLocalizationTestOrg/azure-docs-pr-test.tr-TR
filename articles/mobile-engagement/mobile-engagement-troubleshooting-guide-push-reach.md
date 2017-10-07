---
title: "aaaAzure Mobile Engagement sorun giderme kılavuzu - itme/ulaşma"
description: "Azure Mobile Engagement'de kullanıcı etkileşimi ve bildirim sorunlarını giderme"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3f1886b7-1fdd-47f4-b6b0-d79f158d5ef3
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4ee0b34b9b753a98ccf24863acb28a5dc76bfb95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-push-and-reach-issues"></a>İletme ve Erişim sorunları için sorun giderme kılavuzu
Merhaba, Azure Mobile Engagement'ın bilgi tooyour kullanıcıların nasıl göndereceğini karşılaşabileceğiniz olası sorunlar şunlardır.

## <a name="push-failures"></a>Hataları gönderme
### <a name="issue"></a>Sorun
* Gönderim (uygulamasında, uygulama veya her ikisi de dışında) çalışmıyor.

### <a name="causes"></a>Neden olur.
* Birçok kez gönderme hatası Azure Mobile Engagement, Reach veya başka bir gelişmiş özellik Azure Mobile Engagement'ın doğru şekilde entegre, göstergesidir veya yükseltme olduğunu hello SDK toofix yeni bir işletim sistemi veya cihaz platformu bilinen bir sorun gereklidir.
* Bir şey bir uygulama içinde veya dışında uygulama sorun ise yalnızca bir uygulama içinde anında iletme ve yalnızca bir uygulama dışı itme toodetermine sınayın.
* Hangi ek hata bilgileri kullanılabilir sorun giderme adım toosee hello UI hem hello API test her iki yerde.
* Azure Mobile Engagement ve Reach hello SDK'sı tümleşiktir sürece uygulamanın oturumunu iter çalışmaz.
* Sertifika geçerli değil veya üretim vs kullanıyorsanız iter çalışmaz. Geliştirme doğru (yalnızca iOS). (**Not:** "uygulama oturumunu" anında iletme bildirimleri tooiOS, her iki hello geliştirme (Geliştirme) varsa ve uygulamanızı üretim (üretim) sürümlerinin yüklü hello üzerinde aynı dağıtılmamış olabilir ilişkili hello güvenlik belirteci bu yana aygıt sertifikanızla Apple tarafından geçersiz kılınan. tooresolve bu sorunu hello geliştirme ve uygulamanızın üretim sürümünü kaldırın ve yalnızca hello bir sürümünü yeniden yükleyin.)
* Uygulamanın oturumunu itme sayıları farklı platformlarda (IOS Android daha az bilgi yerel gönderim devre dışı olmadığını bir cihazda, API itme istatistikleri üzerinde hello UI daha fazla bilgi sağlayabilir hello gösterir) farklı şekilde işlenir.
* Uygulamanın oturumunu iter, işletim sistemi düzeyinde (iOS ve Android) müşteriler tarafından engellenebilir.
* Uygulamanın oturumunu iter doğru tümleşik değildir ancak API hello sessiz bir şekilde çalışmayabilir hello Azure Mobile Engagement UI devre dışı olarak gösterilir.
* Azure Mobile Engagement ve Reach hello SDK'sı tümleşiktir sürece uygulamada iter çalışmaz.
* Azure Mobile Engagement ve hello belirli sunucu hello SDK'sı (yalnızca Android) tümleşiktir sürece GCM ve ADM iter çalışmaz.
* Ayrı ayrı bir itme veya Reach sorunu ise, uygulama ve uygulamanın iter olmalıdır dışarı toodetermine test.
* Uygulama bildirim bu hello uygulama alınan açık toobe olması gerekir.
* Uygulamasında iter çoğunlukla bir katılımı veya vazgeçme uygulama bilgisi etikete göre filtrelenmiş Kurulum toobe olur.
* Özel bir kategori ulaşma toodisplay uygulama içi Bildirimlerde kullanın, toofollow hello doğru yaşam döngüsünü hello bildirim gerekir, aksi takdirde, hello bildirim Temizlenmemiş zaman hello kullanıcı yok sayın.
* El ile Merhaba Kampanya bitiş olsa bile bir kampanya ile Bitiş tarihi yok başlatın ve bir cihaz uygulama bildiriminde hello alır ancak henüz görüntülemez, hello kullanıcı hala hello bildirim hello hello uygulamaya oturum sonraki açışlarında alır.
* Merhaba itme API ile sorunları için (Merhaba Reach API'sini daha sık kullanıldığından) hello Reach API'sini yerine toouse hello itme API gerçekten istemiyorsanız ve değil kafa karıştırıcı hello "yükü" ve "bildirim" parametreleri olan onaylayın.
* Anında iletme kampanyanızı aygıtıyla WIFI ve 3 G tooeliminate hello ağ bağlantı sorunlarının olası bir kaynak olarak üzerinden bağlanan her iki test edin.

## <a name="push-testing"></a>Sınama bildirme
### <a name="issue"></a>Sorun
* Bir cihaz kimliği temel tooa belirli cihaz iter gönderilebilir

### <a name="causes"></a>Neden olur.
* Test cihazlarını her platform için farklı kurulum olsa da bir test cihazda uygulamanızda olaya neden ve cihaz Kimliğinizi hello portalında arayan toofind tüm platformlar için cihaz Kimliğinizi çalışması gerekir.
* Test cihazlarını farklı IDFA vs ile çalışır. IDFV (yalnızca iOS).

## <a name="push-customization"></a>Anında iletme özelleştirme
### <a name="issue"></a>Sorun
* Anında iletme öğesi çalışmayacak içerik Gelişmiş (göstergeye, halka, Titret, resim, vb.).
* Gönderim bağlantılarından (uygulama dışında uygulama, tooa Web sitesi, uygulama tooa konumda) çalışmıyor.
* Push değildi itme istatistikleri göster tooas beklenen olarak birçok kişi (çok fazla sayıda veya yeterli) gönderilir.
* Yinelenen ve iki kez alınan iletin.
* Test cihazı Azure Mobile Engagement iter için (kendi üretim ya da geliştirme uygulamayla) kaydedilemiyor.

### <a name="causes"></a>Neden olur.
* toolink tooa uygulamasında belirli bir konuma "Kategoriler" (yalnızca Android) gerektirir.
* Anında iletme bildirimi tıkladıktan sonra tooredirect kullanıcılar tooan alternatif bir konum gerekir içinde oluşturulur ve uygulama ve hello Cihazınızı işletim sistemi tarafından Mobile Engagement tarafından doğrudan yönetilir toobe derin düzenleri bağlama. (**Not:** ile Android olabildiğince uygulamanın oturumunu bildirimleri doğrudan tooin uygulama konumları iOS ile bağlayamazsınız.)
* Harici bir görüntü sunucunuz toobe mümkün toouse HTTP "GET" ve "toowork (yalnızca Android) büyük resmi iter için HEAD".
* Kodunuzda da hello klavye açıldığında hello Azure Mobile Engagement aracısını devre dışı ve böylece hello klavye hello görünümünü etkilemez hello klavye kapatıldıktan sonra hello Azure Mobile Engagement aracısı yeniden etkinleştirmeleri kodunuzu, Bildirim (yalnızca iOS).
* Bazı öğeler test benzetimleri, ancak yalnızca gerçek kampanyaları çalışmıyor (göstergeye, halka, Titret, resim, vb.).
* "Test" Merhaba düğmesini kullandığınızda veriler günlüğe kaydedilir hiçbir sunucu tarafı çok iter. Veriler yalnızca gerçek anında iletme kampanyalarını için günlüğe kaydedilir.
* toohelp sorununuzu ayırmak, ile ilgili sorunları giderme: benzetimini, test ve bunlar her biraz farklı şekilde çalışır olduğundan gerçek bir kampanya.
* Merhaba, "uygulama" ve "dilediğiniz zaman" Kampanyalar zamanlanmış toorun olan süreyi teslim numaraları bir kampanya yalnızca "uygulama" Merhaba kampanya çalışırken olan toousers teslim edilecek (ve cihaz ayarlarına sahip kullanıcılar tooreceive ayarlamak efekt bildirimler "uygulama dışında").
* nasıl Android ve iOS tanıtıcı uygulama bildirimleri dışında zor toodirectly kolaylaştırır arasındaki farklar hello hello Android ve iOS uygulamanızın sürümünü arasında itme istatistikleri karşılaştırın. Android, iOS daha daha fazla işletim sistemi düzeyinde bildirim bilgi sağlar. Yerel bir bildirim alındığında, tıklattınız veya hello bildirim merkezi aracılığıyla silindi ancak iOS hello bildirim tıklandığında sürece bu bilgiler bildirmez Android bildirir. 
* "verilen" numaraları "teslim" numaraları için Kampanyalar ulaşması daha farklı "uygulama" ve "uygulama dışında" bildirimleri farklı sayılır olandan farklı hello ana nedeni. "Uygulama" bildirimler Mobile Engagement tarafından işlenen, ancak "uygulama dışında" bildirimleri hello bildirim merkezi aracılığıyla cihazınızın hello işletim sistemi tarafından işlenir.

## <a name="push-targeting"></a>Hedefleme bildirme
### <a name="issue"></a>Sorun
* Yerleşik hedefleme işe yaramazsa beklendiği gibi.
* Uygulama bilgileri etiketi hedefleme beklendiği gibi çalışmıyor.
* Coğrafi konum hedefleme beklendiği gibi çalışmıyor.
* Dil Seçenekleri beklendiği gibi çalışmıyor.

### <a name="causes"></a>Neden olur.
* Uygulama bilgileri etiketleri hello Azure Mobile Engagement UI veya API aracılığıyla karşıya yüklediğiniz emin olun.
* Azaltma hello anında iletme hız ya da anında iletme kota hello uygulama düzeyinde veya sınırlama hello İzleyici hello kampanya düzeyinde bir kişi diğer hedefleme ölçütlerinize uyan olsa bile belirli bir itme almasını engelleyebilirsiniz. 
* "Language" ayarı hedefleme ülkeye göre tabanlı veya coğrafi konuma göre de hedefleme daha farklı olan yerel bir telefon konumu veya GPS konumuna göre farklıdır.
* Merhaba "varsayılan dili" Merhaba iletisinde cihazlarını, belirttiğiniz hello diğer diller tooone ayarlayın sahip olmayan tooany müşteri gönderilir.

## <a name="push-scheduling"></a>Zamanlama bildirme
### <a name="issue"></a>Sorun
* Anında iletme zamanlama beklendiği gibi (çok erken veya Gecikmeli gönderilen) çalışmıyor.

### <a name="causes"></a>Neden olur.
* Saat dilimleri özellikle hello son kullanıcıların saat dilimi kullanırken zamanlama, sorunlar olabilir.
* Gelişmiş gönderme özellikleri iter gecikmeye yol açabilir.
* Azure Mobile Engagement hello telefon gerçek zamanlı toorequest verilerden bir itme göndermeden önce sağlanmış olabileceği (yerine uygulama bilgisi etiketleri) ayarları geciktirebilir telefonla üzerinde hedefleme iter.
* Bitiş tarihi oluşturulan Kampanyalar hello itme hello cihazda yerel olarak depolamak ve hello kampanya el ile sona erdi olsa bile hello uygulama açıldığında hello göster.
* Birden fazla kampanya başlangıç hello aynı anda daha uzun bir süre tooscan kullanıcı tabanınızı alabilir (aynı anda en fazla dört tooonly başlangıç bir kampanya deneyin, böylece eski kullanıcılar taranan toobe yok yalnızca tooyour etkin kullanıcıları de hedeflemek).
* Merhaba kampanya otomatik olarak göndermez, hello seçeneği "Yoksay İzleyici toousers hello API aracılığıyla bir gönderim" hello "Kampanya" bölümünde Reach kampanya kullanırsanız toosend gerekir, hello Reach API'sini kullanarak el ile.
* Özel bir kategori ulaşma toodisplay uygulama içi Bildirimlerde kullanın, toofollow hello doğru yaşam döngüsünü bir bildirim gerekir, aksi takdirde, hello bildirim Temizlenmemiş zaman hello kullanıcı yok sayın.

