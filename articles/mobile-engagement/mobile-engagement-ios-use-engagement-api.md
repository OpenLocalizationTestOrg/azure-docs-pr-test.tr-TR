---
title: "iOS aaaHow tooUse hello katılım API"
description: "En son iOS SDK - nasıl tooUse hello katılım API iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a>Nasıl tooUse hello katılım API iOS
Bu belge bir eklenti toohello nasıl belgesidir tooIntegrate Engagement iOS: nasıl toouse hello katılım API tooreport uygulama istatistikleri hakkında derinliği ayrıntıları sağlar.

Yalnızca katılım tooreport uygulamanızın oturumları, etkinlikleri, kilitlenme ve teknik bilgi istiyorsanız, ardından hello basit unutmayın şekilde toomake tüm özel olan `UIViewController` nesneleri devralır hello karşılık gelen `EngagementViewController` sınıfı .

Daha fazla tooreport uygulama belirli olaylar, hatalar ve işleri gerekiyorsa örneğin toodo istiyorsanız veya tooreport uygulamanızın etkinlikleri farklı bir şekilde bir hello uygulanan hello daha varsa `EngagementViewController` sınıfları yeniden toouse hello gerekiyor Katılım API.

Merhaba katılım API hello tarafından sağlanan `EngagementAgent` sınıfı. Bu sınıfın bir örneği tarafından arama hello alınabilir `[EngagementAgent shared]` statik yöntemi (Bu hello Not `EngagementAgent` döndürülen tek nesnesidir).

Herhangi bir API'yi, hello çağırmadan önce `EngagementAgent` nesne hello yöntemini çağırarak başlatılmalı`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`

## <a name="engagement-concepts"></a>Engagement kavramları
Merhaba aşağıdaki bölümleri İyileştir hello ortak [Mobile Engagement kavramları](mobile-engagement-concepts.md) hello iOS platformu için.

### <a name="session-and-activity"></a>`Session` ve `Activity`
Bir *etkinlik* toosay hello hello uygulama, bir ekran ile genellikle ilişkili *etkinlik* Merhaba ekranında görüntülenir ve Merhaba ekranında kapatıldığında durdurduğunda başlatır: hello budur ne zaman durumda Merhaba Engagement SDK'sı hello kullanarak tümleşik `EngagementViewController` sınıfları.

Ancak *etkinlikleri* de el ile Merhaba katılım API kullanılarak denetlenebilir. Bu toosplit belirli bir ekran hakkında daha fazla ayrıntı (örneğin tooknown ne sıklıkta ve ne kadar süreyle iletişim kutuları içinde bu ekran kullanılır) bu ekran kullanımını hello birkaç alt bölümleri tooget sağlar.

## <a name="reporting-activities"></a>Raporlama etkinlikleri
### <a name="user-starts-a-new-activity"></a>Kullanıcı yeni bir etkinlik başlatır
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

Toocall gerek `startActivity()` her zaman hello kullanıcı etkinliği değiştirir. Merhaba ilk çağrı toothis işlevi yeni bir kullanıcı oturumu başlatır.

### <a name="user-ends-his-current-activity"></a>Kullanıcı kendi geçerli etkinliği sona erer
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> Yapmanız gerekenler **hiçbir zaman** birkaç oturumları uygulamanıza bir kullanımını toosplit istiyorsanız, bu işlev tarafından dışında çağrısını kendiniz: end toothis function çağrı hello hemen geçerli oturumun bunu, bir sonraki çağrı çok`startActivity()`yeni bir oturum açmaları. Uygulamanızı kapalı olduğunda bu işlev hello SDK'sı tarafından otomatik olarak çağrılır.
> 
> 

## <a name="reporting-events"></a>Raporlama olayları
### <a name="session-events"></a>Oturum olayları
Oturum, kendi oturumunda bir kullanıcı tarafından gerçekleştirilen genellikle kullanılan tooreport hello Eylemler olaylardır.

**Ek veriler olmadan örneği:**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

**Örnek ek veriler ile:**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a>Tek başına olayları
Bir oturum Merhaba içeriğine dışında bulmadýðýný toosession olayları, tek başına olayları kullanılabilir.

**Örnek:**

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a>Hata Raporlama
### <a name="session-errors"></a>Oturum hataları
Oturum hatalar hello kullanıcı kendi oturumunda etkileyen genellikle kullanılan tooreport hello hatalardır.

**Örnek:**

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a>Tek başına hataları
Bulmadýðýný toosession hataları, tek başına hata bir oturum Merhaba içeriğine dışında kullanılabilir.

**Örnek:**

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a>Raporlama işleri
**Örnek:**

Oturum açma işleminiz tooreport hello süresi istediğinizi varsayalım:

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a>Bir işi sırasında hatalarını raporla
Hataları olan yerine işi ilgili tooa olabilir ilgili toohello geçerli kullanıcı oturumunun.

**Örnek:**

Oturum açma işleminiz sırasında bir hata tooreport istediğinizi varsayalım:

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a>Bir işi sırasında olayları
Olaylar, ilgili tooa olmak yerine işi çalıştırmayı olabilir ilgili toohello geçerli kullanıcı oturumunun.

**Örnek:**

Sosyal ağ sahibiz ve hangi hello sırasında kullanıcı bağlı toohello sunucusudur bir iş tooreport hello toplam süre kullanırız varsayalım. Merhaba kullanıcı kendi arkadaşlarınızdan ileti alabilir, bu proje bir olaydır.

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a>Ek parametreler
Rastgele veriler ekli tooevents, hatalar, etkinlikler ve işler olabilir.

Bu verileri yapılandırılmış, iOS'ın NSDictionary sınıfını kullanır.

Ek özellikler içerebileceğini unutmayın `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` veya diğer `NSDictionary` örnekleri.

> [!NOTE]
> Merhaba ek parametre JSON'de serileştirilir. Toopass farklı nesneleri hello yukarıda açıklanan olanları daha istiyorsanız yöntemi sınıfınızda aşağıdaki hello uygulamanız gerekir:
> 
> -(NSString*) JSONRepresentation;
> 
> Merhaba yöntemi bir JSON temsili nesnenizin döndürmelidir.
> 
> 

### <a name="example"></a>Örnek
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a>Sınırlar
#### <a name="keys"></a>Anahtarlar
Merhaba her anahtarında `NSDictionary` normal ifade aşağıdaki hello eşleşmesi gerekir:

`^[a-zA-Z][a-zA-Z_0-9]*`

Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).

#### <a name="size"></a>Boyut
Ek özellikler sınırlı çok**1024** (kez JSON'de hello katılım aracısı tarafından kodlanmış) çağrı başına karakter.

Hello önceki hello toohello sunucu gönderilen JSON 58 karakter uzunluğunda örnektir:

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Uygulama bilgilerini raporlama
İzleme hello kullanarak bilgi (veya diğer uygulama belirli bilgileri) el ile raporlayabilirsiniz `sendAppInfo:` işlevi.

Bu bilgi artımlı olarak gönderilebilir Not: yalnızca hello son değer belirli bir anahtar için belirli bir aygıt için korunur.

Gibi olay ek özellikler, hello `NSDictionary` sınıfı kullanılan tooabstract uygulama bilgileri, dizi not ya da alt sözlükleri (JSON serileştirmesi kullanan) düz dize olarak işleneceğini.

**Örnek:**

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a>Sınırlar
#### <a name="keys"></a>Anahtarlar
Merhaba her anahtarında `NSDictionary` normal ifade aşağıdaki hello eşleşmesi gerekir:

`^[a-zA-Z][a-zA-Z_0-9]*`

Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).

#### <a name="size"></a>Boyut
Uygulama bilgilerini sınırlı çok**1024** (kez JSON'de hello katılım aracısı tarafından kodlanmış) çağrı başına karakter.

Hello önceki hello toohello sunucu gönderilen JSON 44 karakter uzunluğunda örnektir:

    {"birthdate":"1983-12-07","gender":"female"}
