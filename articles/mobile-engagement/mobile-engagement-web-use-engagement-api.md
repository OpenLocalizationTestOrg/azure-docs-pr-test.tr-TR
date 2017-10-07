---
title: Mobile Engagement Web SDK API'leri aaaAzure | Microsoft Docs
description: "en son güncelleştirmeler ve yordamlar hello Web SDK'sı için Azure Mobile Engagement için hello"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a>Bir web uygulaması Hello Azure Mobile Engagement API kullanın
Bu belge nasıl çok belirten bir toplama toohello belgesidir[Mobile Engagement bir web uygulaması tümleştirme](mobile-engagement-web-integrate-engagement.md). Bu, uygulama istatistikleri nasıl toouse hello Azure Mobile Engagement API tooreport hakkında kapsamlı bilgi sağlar.

Merhaba Mobile Engagement API hello tarafından sağlanan `engagement.agent` nesnesi. Merhaba varsayılan Azure Mobile Engagement Web SDK diğer `engagement`. Bu diğer adı hello SDK yapılandırmasından tanımlayabilirsiniz.

## <a name="mobile-engagement-concepts"></a>Mobile Engagement kavramları
Merhaba aşağıdaki bölümleri ortak İyileştir [Mobile Engagement kavramları](mobile-engagement-concepts.md) hello web platformu için.

### <a name="session-and-activity"></a>`Session` ve `Activity`
Merhaba kullanıcı iki etkinlik arasında birden fazla birkaç saniye boyunca boşta kalırsa, hello kullanıcının etkinlikler dizisini iki ayrı oturumlara ayrılır. Bu birkaç saniye hello oturum zaman aşımı denir.

Web uygulamanız kullanıcı etkinlikleri hello sonuna tek başına bildirme değil ise (arama hello tarafından `engagement.agent.endActivity` işlevi), hello Mobile Engagement sunucu otomatik olarak sona hello üç hello uygulama sayfası kapatıldıktan sonra dakika içinde kullanıcı oturumu. Bu hello sunucu oturum zaman aşımı çağrılır.

### `Crash`
Yakalanmayan JavaScript özel durumlarının otomatik raporları varsayılan olarak oluşturulmaz. Kilitlenme ancak rapor hello kullanarak el ile `sendCrash` (kilitlenme bildirimi hello bölümüne bakın) işlev.

## <a name="reporting-activities"></a>Raporlama etkinlikleri
Kullanıcı etkinliğini raporlama, bir kullanıcı yeni bir etkinlik başladığında ve hello kullanıcı hello geçerli etkinliği sona erdiğinde içerir.

### <a name="user-starts-a-new-activity"></a>Kullanıcı yeni bir etkinlik başlatır
    engagement.agent.startActivity("MyUserActivity");

Toocall gerek `startActivity()` her zaman kullanıcı etkinliği değiştirir. Merhaba ilk çağrı toothis işlevi yeni bir kullanıcı oturumu başlatır.

### <a name="user-ends-hello-current-activity"></a>Kullanıcı hello geçerli etkinliği sona erer
    engagement.agent.endActivity();

Toocall gerek `endActivity()` en az bir kez hello kullanıcı tamamlandığında son etkinliklerini. Bu hello Mobile Engagement Web SDK hello kullanıcı şu anda boşta kalır ve hello kullanıcı oturumu toobe gerektiğini hello oturum zaman aşımı süresi dolduktan sonra kapalı bildirir. Çağırırsanız `startActivity()` hello oturum, yalnızca hello oturum zaman aşımı süresi dolmadan önce devam ettirilir.

Merhaba Gezgini penceresi kapatıldığında için güvenilir bir çağrı yok olduğundan genellikle web ortamı içindeki kullanıcı etkinlikleri zor veya olanaksız toocatch hello sonuna değildir. Olduğu neden hello Mobile Engagement sunucu otomatik olarak sona hello kullanıcı oturumunu üç hello uygulama sayfası kapatıldıktan sonra dakika içinde.

## <a name="reporting-events"></a>Raporlama olayları
Raporlama olayları üzerinde oturum olayları ve tek başına olayları ele alınmaktadır.

### <a name="session-events"></a>Oturum olayları
Oturum genellikle kullanılan tooreport hello Eylemler hello kullanıcının oturumu sırasında bir kullanıcı tarafından gerçekleştirilen olaylardır.

**Ek veriler olmadan örneği:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

**Örnek ek veriler ile:**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a>Tek başına olayları
Oturum olayları, bir oturum hello bağlamı dışında tek başına olaylar gerçekleşebilir.

Bunun için kullanmak ``engagement.agent.sendEvent`` yerine ``engagement.agent.sendSessionEvent``.

## <a name="reporting-errors"></a>Hata Raporlama
Hata raporlama, oturum hataları ve tek başına hataları ele alınmaktadır.

### <a name="session-errors"></a>Oturum hataları
Oturum hatalar genellikle bir etkisi hello kullanıcının oturumu sırasında hello kullanıcı kullanılan tooreport hello hatalardır.

**Ek veriler olmadan örneği:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

**Örnek ek veriler ile:**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a>Tek başına hataları
Oturum hatalarının aksine, bir oturum hello bağlamı dışında tek başına hatalar oluşabilir.

Bunun için kullanmak `engagement.agent.sendError` yerine `engagement.agent.sendSessionError`.

## <a name="reporting-jobs"></a>Raporlama işleri
Raporlama, hataları ve bir işi sırasında meydana gelen olayları raporlama ve kilitlenme raporlama işleri kapsar.

**Örnek:**

Toomonitor bir AJAX isteği istiyorsanız hello aşağıdaki kullanırsınız:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a>Bir işi sırasında hata raporlama
Hataları toohello geçerli kullanıcı oturumunun yerine işi ilgili tooa olabilir.

**Örnek:**

Tooreport bir AJAX isteği varsa bir hata istiyorsanız başarısız olur:

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a>Raporlama işi sırasında olayları
Olaylar, ilgili tooa toohello geçerli kullanıcı oturumunun yerine thanks toohello işi olabilir `engagement.agent.sendJobEvent` işlevi.

Bu işlev tıpkı `engagement.agent.sendJobError`.

### <a name="reporting-crashes"></a>Kilitlenme raporlama
Kullanım hello `sendCrash` işlevi tooreport çöküyor el ile.

Merhaba `crashid` değişkendir hello kilitlenme türünü tanımlayan bir dize.
Merhaba `crash` genellikle olmayan bağımsız değişken bir dize olarak hello kilitlenme hello yığın izlemesi.

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a>Ek parametreler
Rastgele veri tooan olayı, hata, etkinlik veya iş ekleyebilirsiniz.

Merhaba veriler herhangi bir JSON nesnesi (ancak bir dizi veya ilkel tür) olabilir.

**Örnek:**

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a>Sınırlar
Tooextra parametreleri geçerli anahtarları, değer türleri ve boyutu için normal ifadeler hello alanlarında kısıtlamalardır.

#### <a name="keys"></a>Anahtarlar
Merhaba nesnesindeki her anahtar normal ifade aşağıdaki hello eşleşmesi gerekir:

    ^[a-zA-Z][a-zA-Z_0-9]*

Anahtarları en az bir harf ile başlamalıdır Bunun anlamı arkasından harf, rakam veya alt çizgi ile (\_).

#### <a name="values"></a>Değerler
Sınırlı toostring, sayı ve Boolean türleri değerlerdir.

#### <a name="size"></a>Boyut
Ek özellikler sınırlı too1, (Merhaba Mobile Engagement Web SDK'sı, JSON'da kodlar sonra) çağrı başına 024 karakterler var.

## <a name="reporting-application-information"></a>Uygulama bilgilerini raporlama
El ile (veya başka bir uygulamaya özgü bilgileri) izleme hello kullanarak raporlayabilirsiniz `sendAppInfo()` işlevi.

Bu bilgi artımlı olarak gönderilebilir unutmayın. Belirli bir aygıt için yalnızca en son değerini belirli bir anahtarın hello tutulacak.

Olay ek özellikler gibi herhangi bir JSON nesnesi tooabstract uygulama bilgi kullanabilirsiniz. Diziler veya alt nesneler (JSON serileştirmesi kullanan) düz dize olarak davranılır unutmayın.

**Örnek:**

Gönderen hello kullanıcının cinsiyeti ve doğum tarihi bir kod örneği şöyledir:

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a>Sınırlar
Anahtarları ve boyutu için normal ifadeler hello alanlarında tooapplication bilgiler geçerli sınırı mevcuttur.

#### <a name="keys"></a>Anahtarlar
Merhaba nesnesindeki her anahtar normal ifade aşağıdaki hello eşleşmesi gerekir:

    ^[a-zA-Z][a-zA-Z_0-9]*

Anahtarları en az bir harf ile başlamalıdır Bunun anlamı arkasından harf, rakam veya alt çizgi ile (\_).

#### <a name="size"></a>Boyut
Uygulama, sınırlı too1, 024 karakterleri (Merhaba Mobile Engagement Web SDK'sı, JSON'da kodlar sonra) çağrı başına bilgilerdir.

Örnek önceki hello hello JSON toohello sunucu 44 karakter uzunluğunda gönderilir:

    {"birthdate":"1983-12-07","gender":"female"}
