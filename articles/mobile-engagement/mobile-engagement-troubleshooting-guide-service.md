---
title: "aaaAzure Mobile Engagement sorun giderme kılavuzu - hizmet"
description: "Azure Mobile Engagement için kılavuzları sorunlarını giderme"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8b4275da-c0b4-4690-824a-48e9d7a1fc6e
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: cf48db323a873ccef95946f7bb26e8d7473c002f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-service-issues"></a>Hizmet sorunları için sorun giderme kılavuzu
Merhaba, nasıl Azure Mobile Engagement çalışır karşılaşabileceğiniz olası sorunlar şunlardır.

## <a name="service-outages"></a>Hizmet kesintisi
### <a name="issue"></a>Sorun
* Azure Mobile Engagement hizmet kesintileri tarafından neden toobe görünür sorunları.

### <a name="causes"></a>Neden olur.
* Azure Mobile Engagement hizmet kesintileri tarafından neden toobe görünür sorunları birkaç farklı nedenlerden kaynaklanabilir:
  * İlk olarak Azure Mobile Engagement, sistemle ilgili tooall görünür yalıtılmış sorunları
  * Bilinen sorunlar sunucu kesintileri (her zaman sunucu durumunda gösterir) nedeni:
  * Gecikmeler, hedefleme hataları, rozet güncelleştirmesini sorunları, toplama, çalışma anında durakları istatistikleri durdurma zamanlama, API'nin Dur çalışma, yeni uygulamalar veya kullanıcılar oluşturulamaz, DNS hataları ve zaman aşımı hataları hello UI, API veya uygulamaları bir cihazda.
  * Bulut bağımlılık kesintileri [Azure hizmet durumu](http://status.azure.com/)
  * Bildirim Hizmetleri (PNS) bağımlılık kesintileri bildirme
  * Uygulama mağazası kesintileri

1) Merhaba sorunun sistemle ilgili olup olmadığını tootest toosee aynı farklı bir işlevi hello test edebilirsiniz

* Azure Mobile Engagement uygulama tümleşik
* Test cihazı
* Test aygıt işletim sistemi sürümü
* Kampanya
* Yönetici kullanıcı hesabı
* Tarayıcı (IE, Firefox, Chrome, vb.)
* Bilgisayar

2) Merhaba sorun yalnızca hello UI veya hello API'nin etkilerse tootest:

* Aynı hem hello Azure Mobile Engagement UI işlev ve Azure Mobile Engagement API'nin hello hello sınayın.

3) Cep telefonu ağınızla Hello sorun olması durumunda tootest:

* Bağlı toohello Internet WIFI üzerinden ve 3 G cep telefonu ağınız bağlıyken sırasında test edin.
* Güvenlik duvarınızın hello Azure Mobile Engagement IP adresleri ya da bağlantı noktalarını herhangi birini engellemediğinden emin olun.

4) Merhaba cihazınızla sorunsa tootest:

* Cihazınızı başka bir Azure Mobile Engagement tümleşik uygulaması ile Mobile Engagement mümkün tooconnect tooAzure ise test edin.
* Hello Azure Mobile Engagement UI görülebilir telefonunuzdan gelen olayları, işler ve kilitlenme oluşturabilir sınayın. 
* Kendi cihaz Kimliği'nde dayalı hello Azure Mobile Engagement UI tooyour aygıttan anında iletme bildirimleri göndermek, test etme 

5) Merhaba, uygulamanızı sorunsa tootest:

* Yükleyin ve yerine bir öykünücü fiziksel CİHAZDAN uygulamanızı test edin:

6) işletim sistemi yükseltmeleri tooend kullanıcıyla SDK yükseltme tooresolve gerektiren cihazlar Hello sorun olması durumunda tootest:

* Uygulamanızın farklı sürümlerini hello işletim sistemi ile farklı cihazlarda sınayın.
* Merhaba hello SDK en son sürümünü kullandığınızdan emin olun.

## <a name="connectivity-and-incorrect-information-issues"></a>Bağlantısı ve yanlış bilgi sorunları
### <a name="issue"></a>Sorun
* Oturum açma sorunları Azure Mobile Engagement UI hello.
* Bağlantı hatalarını hello Azure Mobile Engagement API's ile.
* Uygulama bilgileri etiketleri hello aygıt API karşıya yükleme sorunları.
* Sorunları günlüklerini veya dışarı aktarılan verileri Azure Mobile Engagement'tan yükleniyor.
* Hello Azure Mobile Engagement UI gösterilen yanlış bilgileri.
* Azure Mobile Engagement günlüklerde gösterilen yanlış bilgileri.

### <a name="causes"></a>Neden olur.
* Kullanıcı hesabınızın yeterli izinleri tooperform hello görev sahip olduğunu doğrulayın.
* Bu hello sorunu yalıtılmış tooone bilgisayar ya da yerel ağınızda değil onaylayın.
* Bu hello Azure Mobile Engagement hizmet hiçbir rapor edilen kesintileri onaylayın.
* Uygulama bilgileri etiketi dosyalarınızı bu kuralların hepsi izleyin onaylayın:
  * Kullanım yalnızca hello UTF8 karakter kümesi (Merhaba ANSI karakter kümesini desteklenmez).
  * Virgül "," Merhaba ayırıcı karakter olarak (bir hizmet isteği toorequest toochange hello .csv ayırıcı karakter virgül açabilirsiniz "," tooanother karakter noktalı virgül gibi ";").
  * Tüm küçük Boole değerleri için "true" ve "false" kullanın.
  * Merhaba en büyük dosya boyutu 35 MB daha küçük bir dosya kullanın.

