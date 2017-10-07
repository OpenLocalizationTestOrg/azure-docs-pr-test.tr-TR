---
title: "aaaHow tooUse hello Android katılım API"
description: "En son Android SDK - nasıl tooUse hello Android katılım API"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a>Nasıl tooUse hello Android katılım API
Bu belge bir eklenti toohello belgesidir [Android Mobile Engagement SDK'sı için Gelişmiş raporlama seçenekleri](mobile-engagement-android-advanced-reporting.md). Nasıl toouse hello katılım API tooreport uygulama istatistikleri hakkında ayrıntılar derinliği sağlar.

Yalnızca katılım tooreport uygulamanızın oturumları, etkinlikleri, kilitlenme ve teknik bilgi istiyorsanız, ardından hello en basit yolu toomake tüm olduğunu aklınızda bulundurun, `Activity` alt sınıfları devral hello karşılık gelen `EngagementActivity` sınıfı.

Daha fazla tooreport uygulama belirli olaylar, hatalar ve işleri gerekiyorsa örneğin toodo istiyorsanız veya tooreport uygulamanızın etkinlikleri farklı bir şekilde bir hello uygulanan hello daha varsa `EngagementActivity` sınıfları yeniden toouse hello gerekiyor Katılım API.

Merhaba katılım API hello tarafından sağlanan `EngagementAgent` sınıfı. Bu sınıfın bir örneği tarafından arama hello alınabilir `EngagementAgent.getInstance(Context)` statik yöntemi (Bu hello Not `EngagementAgent` döndürülen tek nesnesidir).

## <a name="engagement-concepts"></a>Engagement kavramları
Merhaba aşağıdaki bölümleri İyileştir hello ortak [Mobile Engagement kavramları](mobile-engagement-concepts.md), hello Android platformu için.

### <a name="session-and-activity"></a>`Session` ve `Activity`
Hello kullanıcı birden fazla birkaç saniye arasında iki boşta kalırsa *etkinlikleri*, daha sonra kendi dizisini *etkinlikleri* iki ayrı bölünen *oturumları*. Bu birkaç saniye hello "oturum zaman aşımı" adı verilir.

Bir *etkinlik* toosay hello hello uygulama, bir ekran ile genellikle ilişkili *etkinlik* Merhaba ekranında görüntülenir ve Merhaba ekranında kapatıldığında durdurduğunda başlatır: hello budur ne zaman durumda Merhaba Engagement SDK'sı hello kullanarak tümleşik `EngagementActivity` sınıfları.

Ancak *etkinlikleri* de el ile Merhaba katılım API kullanılarak denetlenebilir. Bu toosplit belirli bir ekran hakkında daha fazla ayrıntı (örneğin tooknown ne sıklıkta ve ne kadar süreyle iletişim kutuları içinde bu ekran kullanılır) bu ekran kullanımını hello birkaç alt bölümleri tooget sağlar.

## <a name="reporting-activities"></a>Raporlama etkinlikleri
> [!IMPORTANT]
> Merhaba kullanıyorsanız, bu bölümde açıklandığı gibi tooreport etkinlikler gerekmeyen `EngagementActivity` sınıfı ve türevleri hello nasıl açıklandığı gibi Android belgesinde tooIntegrate katılım.
> 
> 

### <a name="user-starts-a-new-activity"></a>Kullanıcı yeni bir etkinlik başlatır
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

Toocall gerek `startActivity()` her zaman hello kullanıcı etkinliği değiştirir. Merhaba ilk çağrı toothis işlevi yeni bir kullanıcı oturumu başlatır.

Bu işlev, her etkinlik üzerinde kullanılır en iyi yeri toocall hello `onResume` geri çağırma.

### <a name="user-ends-his-current-activity"></a>Kullanıcı kendi geçerli etkinliği sona erer
            EngagementAgent.getInstance(this).endActivity();

Toocall gerek `endActivity()` en az bir kez hello kullanıcı tamamlandığında son etkinliğini. Bu Engagement SDK'sı hello kullanıcı şu anda boşta ve hello kullanıcı oturumu toobe gerektiğini bildiren bir kez hello oturum zaman aşımı kapalı dolacak hello bildirir (çağırırsanız `startActivity()` hello oturum yalnızca hello oturum zaman aşımı süresi dolmadan önce sürdürüldü).

Bu işlev, her etkinlik üzerinde kullanılır en iyi yeri toocall hello `onPause` geri çağırma.

## <a name="reporting-events"></a>Raporlama olayları
### <a name="session-events"></a>Oturum olayları
Oturum, kendi oturumunda bir kullanıcı tarafından gerçekleştirilen genellikle kullanılan tooreport hello Eylemler olaylardır.

**Ek veriler olmadan örneği:**

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

**Örnek ek veriler ile:**

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a>Tek başına olayları
Bulmadýðýný toosession olayları, bir oturum Merhaba içeriğine dışında tek başına olaylar gerçekleşebilir.

**Örnek:**

Bir yayın alıcı tetiklendiğinde tooreport olayların istediğinizi varsayalım:

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a>Hata Raporlama
### <a name="session-errors"></a>Oturum hataları
Oturum hatalar hello kullanıcı kendi oturumunda etkileyen genellikle kullanılan tooreport hello hatalardır.

**Örnek:**

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a>Tek başına hataları
Bulmadýðýný toosession hataları, bir oturum Merhaba içeriğine dışında tek başına hatalar oluşabilir.

**Örnek:**

Merhaba aşağıdaki örnekte tooreport uygulama işlemi sırasında hello telefonda hello bellek azaldığında her bir hata nasıl çalıştığı gösterilmektedir.

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a>Raporlama işleri
### <a name="example"></a>Örnek
Oturum açma işleminiz tooreport hello süresi istediğinizi varsayalım:

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a>Bir işi sırasında hatalarını raporla
Hataları olan yerine işi ilgili tooa olabilir ilgili toohello geçerli kullanıcı oturumunun.

**Örnek:**

Tooreport istediğinizi düşünelim, sırasında bir hata işlem oturum açma:

[...] Ortak void Signın (bağlam bağlamı,...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a>Raporlama işi sırasında olayları
Olaylar, ilgili tooa olmak yerine işi çalıştırmayı olabilir ilgili toohello geçerli kullanıcı oturumunun.

**Örnek:**

Sosyal ağ sahibiz ve hangi hello sırasında kullanıcı bağlı toohello sunucusudur bir iş tooreport hello toplam süre kullanırız varsayalım. Bu yüzden hiçbir oturum hello kullanıcı bile kendisinin başka bir uygulama kullanıyorsa veya hello telefon Uyuma arka planda bağlı kalabilir.

Merhaba kullanıcı kendi arkadaşlarınızdan ileti alabilir, bu proje bir olaydır.

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a>Ek parametreler
Rastgele veriler ekli tooevents, hatalar, etkinlikler ve işler olabilir.

Bu verileri yapılandırılmış, Android'ın paket sınıfı kullanır (aslında, Android hedefleri ek parametreleri gibi çalışır). Bir paket dizileri veya başka bir paket örneklerini içerebileceğini unutmayın.

> [!IMPORTANT]
> Parcelable veya seri hale getirilebilir parametrelerinde yerleştirirseniz emin olun, `toString()` uygulanan tooreturn okunabilir dize bir yöntemdir. Çağıracaksınız sırasında serileştirilebilir olmayan geçici olmayan alanlar içeriyor serileştirilebilir sınıflardan Android kilitlenme yapar`bundle.putSerializable("key",value);`
> 
> [!WARNING]
> Ek parametreler seyrek dizilerde desteklenmez, diğer bir deyişle, bir dizi olarak seri hale getirilmesi olmaz. Bunları standart diziye ek parametreler kullanmadan önce dönüştürmeniz.
> 
> 

### <a name="example"></a>Örnek
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a>Sınırlar
#### <a name="keys"></a>Anahtarlar
Merhaba her anahtarında `Bundle` normal ifade aşağıdaki hello eşleşmesi gerekir:

`^[a-zA-Z][a-zA-Z_0-9]*`

Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).

#### <a name="size"></a>Boyut
Ek özellikler sınırlı çok**1024** (kez JSON'de hello katılım hizmeti tarafından kodlanmış) çağrı başına karakter.

Hello önceki hello toohello sunucu gönderilen JSON 58 karakter uzunluğunda örnektir:

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Uygulama bilgilerini raporlama
İzleme hello kullanarak bilgi (veya diğer uygulama belirli bilgileri) el ile raporlayabilirsiniz `sendAppInfo()` işlevi.

Bu bilgi artımlı olarak gönderilebilir Not: yalnızca hello son değer belirli bir anahtar için belirli bir aygıt için korunur.

Olay ek özellikler gibi hello paket sınıfı kullanılan tooabstract uygulama bilgileri, dizi veya alt sunmaktadır unutmayın (JSON serileştirmesi kullanan) düz dize olarak kabul edilir.

### <a name="example"></a>Örnek
İşte, kod örnek toosend kullanıcı cinsiyeti ve doğum tarihi:

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a>Sınırlar
#### <a name="keys"></a>Anahtarlar
Merhaba her anahtarında `Bundle` normal ifade aşağıdaki hello eşleşmesi gerekir:

`^[a-zA-Z][a-zA-Z_0-9]*`

Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).

#### <a name="size"></a>Boyut
Uygulama bilgilerini sınırlı çok**1024** (kez JSON'de hello katılım hizmeti tarafından kodlanmış) çağrı başına karakter.

Hello önceki hello toohello sunucu gönderilen JSON 44 karakter uzunluğunda örnektir:

            {"expiration":"2016-12-07","status":"premium"}
