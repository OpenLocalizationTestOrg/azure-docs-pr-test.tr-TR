---
title: "aaaHow tooUse hello Windows Phone Silverlight katılım API"
description: "Nasıl tooUse hello Windows Phone Silverlight katılım API"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a>Nasıl tooUse hello Windows Phone Silverlight katılım API
Bu belge bir eklenti toohello belgesidir [nasıl toointegrate Mobile Engagement Windows Phone Silverlight uygulamanızda](mobile-engagement-windows-phone-integrate-engagement.md). Nasıl toouse hello katılım API tooreport uygulama istatistikleri hakkında ayrıntılar derinliği sağlar.

Yalnızca katılım tooreport uygulamanızın oturumları, etkinlikleri, kilitlenme ve teknik bilgi istiyorsanız sonra hello en basit yolu toomake tüm olduğundan, `PhoneApplicationPage` alt sınıfları devral hello `EngagementPage` sınıfı.

Daha fazla tooreport uygulama belirli olaylar, hatalar ve işleri gerekiyorsa örneğin toodo istiyorsanız veya tooreport uygulamanızın etkinlikleri farklı bir şekilde bir hello uygulanan hello daha varsa `EngagementPage` sınıfları yeniden toouse hello gerekiyor Katılım API.

Merhaba katılım API hello tarafından sağlanan `EngagementAgent` sınıfı. Toothose yöntemlerle erişebilirsiniz `EngagementAgent.Instance`.

Merhaba aracı modülü başlatılmadı olsa bile, her çağrı toohello API ertelenir ve hello Aracısı kullanılabilir olduğunda yeniden yürütülür.

## <a name="engagement-concepts"></a>Engagement kavramları
bölümleri aşağıdaki hello hello Mobile Engagement kavramları hello Windows Phone platform için yenileyin.

### <a name="session-and-activity"></a>`Session` ve `Activity`
Bir *etkinlik* genellikle toosay hello hello uygulama, bir sayfayla ilişkili *etkinlik* hello sayfası görüntülenir ve hello sayfa kapatıldığında durdurduğunda başlatır: hello hello zaman böyledir Engagement SDK'sı tümleşik hello kullanarak `EngagementPage` sınıfı.

Ancak *etkinlikleri* de el ile Merhaba katılım API kullanılarak denetlenebilir. Bu toosplit belirli bir sayfa hakkında daha fazla ayrıntı (örneğin tooknown ne sıklıkta ve ne kadar süre içinde bu sayfa iletişim kutuları kullanılır), bu sayfanın kullanım hello birkaç alt bölümleri tooget sağlar.

## <a name="reporting-activities"></a>Raporlama etkinlikleri
### <a name="user-starts-a-new-activity"></a>Kullanıcı yeni bir etkinlik başlatır
#### <a name="reference"></a>Başvuru
            void StartActivity(string name, Dictionary<object, object> extras = null)

Toocall gerek `StartActivity()` her zaman hello kullanıcı etkinliği değiştirir. Merhaba ilk çağrı toothis işlevi yeni bir kullanıcı oturumu başlatır.

> [!IMPORTANT]
> Merhaba SDK otomatik olarak çağrı hello EndActivity yöntemi hello uygulama kapatıldığında. Bu nedenle, hello kullanıcı değiştirme ve hello EndActivity yöntemi, bu yöntemi çağırmadan itibaren hello geçerli oturum toobe zorlar tooNEVER çağrı Hello etkinliğini sona erdi her toocall hello StartActivity yöntemi KULLANMAMANIZ önerilir.
> 
> 

#### <a name="example"></a>Örnek
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>Kullanıcı kendi geçerli etkinliği sona erer
#### <a name="reference"></a>Başvuru
            void EndActivity()

Toocall gerek `EndActivity()` en az bir kez hello kullanıcı tamamlandığında son etkinliğini. Bu Engagement SDK'sı hello kullanıcı şu anda boşta ve hello kullanıcı oturumu toobe gerektiğini bildiren bir kez hello oturum zaman aşımı kapalı dolacak hello bildirir (çağırırsanız `StartActivity()` hello oturum, yalnızca hello oturum zaman aşımı süresi dolmadan önce devam ettirildiğinde).

#### <a name="example"></a>Örnek
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>Raporlama işleri
### <a name="start-a-job"></a>Bir işi Başlat
#### <a name="reference"></a>Başvuru
            void StartJob(string name, Dictionary<object, object> extras = null)

Bir süre boyunca hello iş tootrack bazı görevleri kullanabilirsiniz.

#### <a name="example"></a>Örnek
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>Bir işin bitiş
#### <a name="reference"></a>Başvuru
            void EndJob(string name)

Bir iş tarafından izlenen bir görev sonlandırıldı hemen hello iş adı sağlayarak bu proje için hello EndJob yöntemini çağırmalıdır.

#### <a name="example"></a>Örnek
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>Raporlama olayları
Üç tür olay vardır:

* Tek başına olayları
* Oturum olayları
* İş olayları

### <a name="standalone-events"></a>Tek başına olayları
#### <a name="reference"></a>Başvuru
            void SendEvent(string name, Dictionary<object, object> extras = null)

Tek başına olaylar oturumu hello bağlamı dışında gerçekleşebilir.

#### <a name="example"></a>Örnek
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>Oturum olayları
#### <a name="reference"></a>Başvuru
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

Oturum, kendi oturumunda bir kullanıcı tarafından gerçekleştirilen genellikle kullanılan tooreport hello Eylemler olaylardır.

#### <a name="example"></a>Örnek
**Veri olmadan:**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**Verilerle:**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>İş olayları
#### <a name="reference"></a>Başvuru
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

İş, bir kullanıcı tarafından gerçekleştirilen işi sırasında genellikle kullanılan tooreport hello Eylemler olaylardır.

#### <a name="example"></a>Örnek
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>Hata Raporlama
Üç tür hataları vardır:

* Tek başına hataları
* Oturum hataları
* İş hataları

### <a name="standalone-errors"></a>Tek başına hataları
#### <a name="reference"></a>Başvuru
            void SendError(string name, Dictionary<object, object> extras = null)

Bulmadýðýný toosession hataları, bir oturum Merhaba içeriğine dışında tek başına hatalar oluşabilir.

#### <a name="example"></a>Örnek
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>Oturum hataları
#### <a name="reference"></a>Başvuru
            void SendSessionError(string name, Dictionary<object, object> extras = null)

Oturum hatalar hello kullanıcı kendi oturumunda etkileyen genellikle kullanılan tooreport hello hatalardır.

#### <a name="example"></a>Örnek
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>İş hataları
#### <a name="reference"></a>Başvuru
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

Hataları olan yerine işi ilgili tooa olabilir ilgili toohello geçerli kullanıcı oturumunun.

#### <a name="example"></a>Örnek
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>Raporlama çökme (Crash)
Merhaba Aracısı çökme (Crash) ile iki yöntemleri toodeal sağlar.

### <a name="send-an-exception"></a>Bir özel durum Gönder
#### <a name="reference"></a>Başvuru
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>Örnek
Bir özel durum herhangi bir zamanda çağırarak gönderebilirsiniz:

            EngagementAgent.Instance.SendCrash(aCatchedException);

Bir isteğe bağlı bir parametre tooterminate hello katılım oturumu sırasında hello kullanabilirsiniz hello kilitlenme gönderme daha aynı anda. Bu nedenle, toodo arayın:

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

Bunu yaparsanız, hello oturum işleri hello kilitlenme gönderdikten sonra kapatılacak.

### <a name="send-an-unhandled-exception"></a>İşlenmeyen bir özel durum Gönder
#### <a name="reference"></a>Başvuru
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

Katılım yöntemi toosend işlenmeyen özel durumlar da sağlar. Merhaba silverlight UnhandledException olay işleyicisinin içinden kullanıldığında bu özellikle yararlıdır.

Bu yöntem olacak **her zaman** hello katılım oturum ve işleri adlı sonra sonlandırılacak.

#### <a name="example"></a>Örnek
Tooimplement kullanın (özellikle, hello otomatik kilitlenme raporlama katılım özelliği devre dışı bıraktıysanız) kendi UnhandledException işleyicisi. Örneğin, hello içinde `Application_UnhandledException` hello yöntemi `App.xaml.cs` dosyası:

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a>OnActivated
### <a name="reference"></a>Başvuru
            void OnActivated(ActivatedEventArgs e)

Hello devre dışı olay tetiklenir sonra hello kullanıcı İleri, bir uygulama çıktığınızda gittiğinde hello işletim sistemi tooput Merhaba uygulaması etkinliği olmayan bir duruma deneyecek. Ardından, kaldırıldı olarak işaretleme hello uygulamasıdır. Bu işlemde bir uygulama sonlandırıldı ancak hello uygulama ve her bir sayfayı hello hello uygulamadaki hello durumuyla ilgili bazı veriler korunur.

Tooinsert sahip `EngagementAgent.Instance.OnActivated(e)` hello içinde `Application_Activated` hello App.xaml.cs dosyasını tooreset hello katılım Merhaba uygulaması kaldırıldı kaldığında Aracısı yönteminden.

### <a name="example"></a>Örnek
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a>Cihaz kimliği
            String GetDeviceId()

Bu yöntemi çağrılarak hello engagement cihaz kimliğini elde edebilirsiniz.

## <a name="extras-parameters"></a>Ek özellikler parametreleri
Rastgele veriler ekli tooan olay, bir hata, bir etkinlik veya bir iş olabilir. Bu verilerin bir sözlüğünü kullanarak yapılandırılmış. Anahtarları ve değerleri herhangi bir türde olabilir.

Bu nedenle tooinsert kendi türünde ek özellikler istiyorsanız, bu tür için bir veri sözleşmesi tooadd zorunda ek özellikler veri serileştirilir.

### <a name="example"></a>Örnek
Yeni bir sınıf "Kişi" oluşturuyoruz.

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

Ardından, ekleyeceğiz bir `Person` örneği tooan ek.

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> Diğer nesne türlerini yerleştirirseniz, kendi ToString() yöntemini uygulanan tooreturn İnsan okunabilir dize olduğundan emin olun.
> 
> 

### <a name="limits"></a>Sınırlar
#### <a name="keys"></a>Anahtarlar
Merhaba nesnesindeki her anahtar normal ifade aşağıdaki hello eşleşmesi gerekir:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).

#### <a name="size"></a>Boyut
Ek özellikler sınırlı çok**1024** çağrı başına karakter.

## <a name="reporting-application-information"></a>Uygulama bilgilerini raporlama
### <a name="reference"></a>Başvuru
            void SendAppInfo(Dictionary<object, object> appInfos)

Merhaba SendAppInfo() işlevini kullanarak bilgi (veya diğer uygulama belirli bilgileri) izleme el ile bildirebilirsiniz.

Bu bilgi artımlı olarak gönderilebilir Not: yalnızca hello son değer belirli bir anahtar için belirli bir aygıt için korunur. Olay ek özellikler gibi sözlük kullanma\<nesne, nesne\> tooattach bilgiler.

### <a name="example"></a>Örnek
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>Sınırlar
#### <a name="keys"></a>Anahtarlar
Merhaba nesnesindeki her anahtar normal ifade aşağıdaki hello eşleşmesi gerekir:

`^[a-zA-Z][a-zA-Z_0-9]*$`

Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).

#### <a name="size"></a>Boyut
Uygulama bilgilerini sınırlı çok**1024** çağrı başına karakter.

Hello önceki hello toohello sunucu gönderilen JSON 44 karakter uzunluğunda örnektir:

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a>Günlüğe kaydetme
### <a name="enable-logging"></a>Günlük kaydını etkinleştir
Merhaba SDK hello IDE konsolunda yapılandırılmış tooproduce test günlüklerinin olabilir.
Bu günlükler varsayılan olarak etkinleştirilmez. toocustomize Bu, güncelleştirme hello özellik `EngagementAgent.Instance.TestLogEnabled` tooone hello kullanılabilir hello değerinin `EngagementTestLogLevel` numaralandırma, örneğin:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
