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
# <a name="how-toouse-hello-engagement-api-on-ios"></a><span data-ttu-id="c004f-103">Nasıl tooUse hello katılım API iOS</span><span class="sxs-lookup"><span data-stu-id="c004f-103">How tooUse hello Engagement API on iOS</span></span>
<span data-ttu-id="c004f-104">Bu belge bir eklenti toohello nasıl belgesidir tooIntegrate Engagement iOS: nasıl toouse hello katılım API tooreport uygulama istatistikleri hakkında derinliği ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="c004f-104">This document is an add-on toohello document How tooIntegrate Engagement on iOS: it provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="c004f-105">Yalnızca katılım tooreport uygulamanızın oturumları, etkinlikleri, kilitlenme ve teknik bilgi istiyorsanız, ardından hello basit unutmayın şekilde toomake tüm özel olan `UIViewController` nesneleri devralır hello karşılık gelen `EngagementViewController` sınıfı .</span><span class="sxs-lookup"><span data-stu-id="c004f-105">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your custom `UIViewController` objects inherit from hello corresponding `EngagementViewController` class.</span></span>

<span data-ttu-id="c004f-106">Daha fazla tooreport uygulama belirli olaylar, hatalar ve işleri gerekiyorsa örneğin toodo istiyorsanız veya tooreport uygulamanızın etkinlikleri farklı bir şekilde bir hello uygulanan hello daha varsa `EngagementViewController` sınıfları yeniden toouse hello gerekiyor Katılım API.</span><span class="sxs-lookup"><span data-stu-id="c004f-106">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementViewController` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="c004f-107">Merhaba katılım API hello tarafından sağlanan `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="c004f-107">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="c004f-108">Bu sınıfın bir örneği tarafından arama hello alınabilir `[EngagementAgent shared]` statik yöntemi (Bu hello Not `EngagementAgent` döndürülen tek nesnesidir).</span><span class="sxs-lookup"><span data-stu-id="c004f-108">An instance of this class can be retrieved by calling hello `[EngagementAgent shared]` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

<span data-ttu-id="c004f-109">Herhangi bir API'yi, hello çağırmadan önce `EngagementAgent` nesne hello yöntemini çağırarak başlatılmalı`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span><span class="sxs-lookup"><span data-stu-id="c004f-109">Before any API calls, hello `EngagementAgent` object must be initialized by calling hello method `[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="c004f-110">Engagement kavramları</span><span class="sxs-lookup"><span data-stu-id="c004f-110">Engagement concepts</span></span>
<span data-ttu-id="c004f-111">Merhaba aşağıdaki bölümleri İyileştir hello ortak [Mobile Engagement kavramları](mobile-engagement-concepts.md) hello iOS platformu için.</span><span class="sxs-lookup"><span data-stu-id="c004f-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md) for hello iOS platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="c004f-112">`Session` ve `Activity`</span><span class="sxs-lookup"><span data-stu-id="c004f-112">`Session` and `Activity`</span></span>
<span data-ttu-id="c004f-113">Bir *etkinlik* toosay hello hello uygulama, bir ekran ile genellikle ilişkili *etkinlik* Merhaba ekranında görüntülenir ve Merhaba ekranında kapatıldığında durdurduğunda başlatır: hello budur ne zaman durumda Merhaba Engagement SDK'sı hello kullanarak tümleşik `EngagementViewController` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="c004f-113">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementViewController` classes.</span></span>

<span data-ttu-id="c004f-114">Ancak *etkinlikleri* de el ile Merhaba katılım API kullanılarak denetlenebilir.</span><span class="sxs-lookup"><span data-stu-id="c004f-114">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="c004f-115">Bu toosplit belirli bir ekran hakkında daha fazla ayrıntı (örneğin tooknown ne sıklıkta ve ne kadar süreyle iletişim kutuları içinde bu ekran kullanılır) bu ekran kullanımını hello birkaç alt bölümleri tooget sağlar.</span><span class="sxs-lookup"><span data-stu-id="c004f-115">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="c004f-116">Raporlama etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="c004f-116">Reporting Activities</span></span>
### <a name="user-starts-a-new-activity"></a><span data-ttu-id="c004f-117">Kullanıcı yeni bir etkinlik başlatır</span><span class="sxs-lookup"><span data-stu-id="c004f-117">User starts a new Activity</span></span>
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

<span data-ttu-id="c004f-118">Toocall gerek `startActivity()` her zaman hello kullanıcı etkinliği değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c004f-118">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="c004f-119">Merhaba ilk çağrı toothis işlevi yeni bir kullanıcı oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="c004f-119">hello first call toothis function starts a new user session.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="c004f-120">Kullanıcı kendi geçerli etkinliği sona erer</span><span class="sxs-lookup"><span data-stu-id="c004f-120">User ends his current Activity</span></span>
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> <span data-ttu-id="c004f-121">Yapmanız gerekenler **hiçbir zaman** birkaç oturumları uygulamanıza bir kullanımını toosplit istiyorsanız, bu işlev tarafından dışında çağrısını kendiniz: end toothis function çağrı hello hemen geçerli oturumun bunu, bir sonraki çağrı çok`startActivity()`yeni bir oturum açmaları.</span><span class="sxs-lookup"><span data-stu-id="c004f-121">You should **NEVER** call this function by yourself, except if you want toosplit one use of your application into several sessions: a call toothis function would end hello current session immediately, so, a subsequent call too`startActivity()` would start a new session.</span></span> <span data-ttu-id="c004f-122">Uygulamanızı kapalı olduğunda bu işlev hello SDK'sı tarafından otomatik olarak çağrılır.</span><span class="sxs-lookup"><span data-stu-id="c004f-122">This function is automatically called by hello SDK when your application is closed.</span></span>
> 
> 

## <a name="reporting-events"></a><span data-ttu-id="c004f-123">Raporlama olayları</span><span class="sxs-lookup"><span data-stu-id="c004f-123">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="c004f-124">Oturum olayları</span><span class="sxs-lookup"><span data-stu-id="c004f-124">Session events</span></span>
<span data-ttu-id="c004f-125">Oturum, kendi oturumunda bir kullanıcı tarafından gerçekleştirilen genellikle kullanılan tooreport hello Eylemler olaylardır.</span><span class="sxs-lookup"><span data-stu-id="c004f-125">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="c004f-126">**Ek veriler olmadan örneği:**</span><span class="sxs-lookup"><span data-stu-id="c004f-126">**Example without extra data:**</span></span>

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

<span data-ttu-id="c004f-127">**Örnek ek veriler ile:**</span><span class="sxs-lookup"><span data-stu-id="c004f-127">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="c004f-128">Tek başına olayları</span><span class="sxs-lookup"><span data-stu-id="c004f-128">Standalone events</span></span>
<span data-ttu-id="c004f-129">Bir oturum Merhaba içeriğine dışında bulmadýðýný toosession olayları, tek başına olayları kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c004f-129">Contrary toosession events, standalone events can be used outside of hello context of a session.</span></span>

<span data-ttu-id="c004f-130">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="c004f-130">**Example:**</span></span>

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a><span data-ttu-id="c004f-131">Hata Raporlama</span><span class="sxs-lookup"><span data-stu-id="c004f-131">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="c004f-132">Oturum hataları</span><span class="sxs-lookup"><span data-stu-id="c004f-132">Session errors</span></span>
<span data-ttu-id="c004f-133">Oturum hatalar hello kullanıcı kendi oturumunda etkileyen genellikle kullanılan tooreport hello hatalardır.</span><span class="sxs-lookup"><span data-stu-id="c004f-133">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="c004f-134">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="c004f-134">**Example:**</span></span>

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

### <a name="standalone-errors"></a><span data-ttu-id="c004f-135">Tek başına hataları</span><span class="sxs-lookup"><span data-stu-id="c004f-135">Standalone errors</span></span>
<span data-ttu-id="c004f-136">Bulmadýðýný toosession hataları, tek başına hata bir oturum Merhaba içeriğine dışında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c004f-136">Contrary toosession errors, standalone errors can be used outside of hello context of a session.</span></span>

<span data-ttu-id="c004f-137">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="c004f-137">**Example:**</span></span>

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a><span data-ttu-id="c004f-138">Raporlama işleri</span><span class="sxs-lookup"><span data-stu-id="c004f-138">Reporting Jobs</span></span>
<span data-ttu-id="c004f-139">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="c004f-139">**Example:**</span></span>

<span data-ttu-id="c004f-140">Oturum açma işleminiz tooreport hello süresi istediğinizi varsayalım:</span><span class="sxs-lookup"><span data-stu-id="c004f-140">Suppose you want tooreport hello duration of your login process:</span></span>

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

### <a name="report-errors-during-a-job"></a><span data-ttu-id="c004f-141">Bir işi sırasında hatalarını raporla</span><span class="sxs-lookup"><span data-stu-id="c004f-141">Report Errors during a Job</span></span>
<span data-ttu-id="c004f-142">Hataları olan yerine işi ilgili tooa olabilir ilgili toohello geçerli kullanıcı oturumunun.</span><span class="sxs-lookup"><span data-stu-id="c004f-142">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="c004f-143">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="c004f-143">**Example:**</span></span>

<span data-ttu-id="c004f-144">Oturum açma işleminiz sırasında bir hata tooreport istediğinizi varsayalım:</span><span class="sxs-lookup"><span data-stu-id="c004f-144">Suppose you want tooreport an error during your login process:</span></span>

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

### <a name="events-during-a-job"></a><span data-ttu-id="c004f-145">Bir işi sırasında olayları</span><span class="sxs-lookup"><span data-stu-id="c004f-145">Events during a job</span></span>
<span data-ttu-id="c004f-146">Olaylar, ilgili tooa olmak yerine işi çalıştırmayı olabilir ilgili toohello geçerli kullanıcı oturumunun.</span><span class="sxs-lookup"><span data-stu-id="c004f-146">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="c004f-147">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="c004f-147">**Example:**</span></span>

<span data-ttu-id="c004f-148">Sosyal ağ sahibiz ve hangi hello sırasında kullanıcı bağlı toohello sunucusudur bir iş tooreport hello toplam süre kullanırız varsayalım.</span><span class="sxs-lookup"><span data-stu-id="c004f-148">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="c004f-149">Merhaba kullanıcı kendi arkadaşlarınızdan ileti alabilir, bu proje bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="c004f-149">hello user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="c004f-150">Ek parametreler</span><span class="sxs-lookup"><span data-stu-id="c004f-150">Extra parameters</span></span>
<span data-ttu-id="c004f-151">Rastgele veriler ekli tooevents, hatalar, etkinlikler ve işler olabilir.</span><span class="sxs-lookup"><span data-stu-id="c004f-151">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="c004f-152">Bu verileri yapılandırılmış, iOS'ın NSDictionary sınıfını kullanır.</span><span class="sxs-lookup"><span data-stu-id="c004f-152">This data can be structured, it uses iOS's NSDictionary class.</span></span>

<span data-ttu-id="c004f-153">Ek özellikler içerebileceğini unutmayın `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` veya diğer `NSDictionary` örnekleri.</span><span class="sxs-lookup"><span data-stu-id="c004f-153">Note that extras can contain `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` or other `NSDictionary` instances.</span></span>

> [!NOTE]
> <span data-ttu-id="c004f-154">Merhaba ek parametre JSON'de serileştirilir.</span><span class="sxs-lookup"><span data-stu-id="c004f-154">hello extra parameter is serialized in JSON.</span></span> <span data-ttu-id="c004f-155">Toopass farklı nesneleri hello yukarıda açıklanan olanları daha istiyorsanız yöntemi sınıfınızda aşağıdaki hello uygulamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="c004f-155">If you want toopass different objects than hello ones described above, you must implement hello following method in your class:</span></span>
> 
> <span data-ttu-id="c004f-156">-(NSString*) JSONRepresentation;</span><span class="sxs-lookup"><span data-stu-id="c004f-156">-(NSString*)JSONRepresentation;</span></span>
> 
> <span data-ttu-id="c004f-157">Merhaba yöntemi bir JSON temsili nesnenizin döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="c004f-157">hello method should return a JSON representation of your object.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="c004f-158">Örnek</span><span class="sxs-lookup"><span data-stu-id="c004f-158">Example</span></span>
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a><span data-ttu-id="c004f-159">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="c004f-159">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="c004f-160">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="c004f-160">Keys</span></span>
<span data-ttu-id="c004f-161">Merhaba her anahtarında `NSDictionary` normal ifade aşağıdaki hello eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c004f-161">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="c004f-162">Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).</span><span class="sxs-lookup"><span data-stu-id="c004f-162">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="c004f-163">Boyut</span><span class="sxs-lookup"><span data-stu-id="c004f-163">Size</span></span>
<span data-ttu-id="c004f-164">Ek özellikler sınırlı çok**1024** (kez JSON'de hello katılım aracısı tarafından kodlanmış) çağrı başına karakter.</span><span class="sxs-lookup"><span data-stu-id="c004f-164">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="c004f-165">Hello önceki hello toohello sunucu gönderilen JSON 58 karakter uzunluğunda örnektir:</span><span class="sxs-lookup"><span data-stu-id="c004f-165">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="c004f-166">Uygulama bilgilerini raporlama</span><span class="sxs-lookup"><span data-stu-id="c004f-166">Reporting Application Information</span></span>
<span data-ttu-id="c004f-167">İzleme hello kullanarak bilgi (veya diğer uygulama belirli bilgileri) el ile raporlayabilirsiniz `sendAppInfo:` işlevi.</span><span class="sxs-lookup"><span data-stu-id="c004f-167">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo:` function.</span></span>

<span data-ttu-id="c004f-168">Bu bilgi artımlı olarak gönderilebilir Not: yalnızca hello son değer belirli bir anahtar için belirli bir aygıt için korunur.</span><span class="sxs-lookup"><span data-stu-id="c004f-168">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="c004f-169">Gibi olay ek özellikler, hello `NSDictionary` sınıfı kullanılan tooabstract uygulama bilgileri, dizi not ya da alt sözlükleri (JSON serileştirmesi kullanan) düz dize olarak işleneceğini.</span><span class="sxs-lookup"><span data-stu-id="c004f-169">Like event extras, hello `NSDictionary` class is used tooabstract application information, note that arrays or sub-dictionaries will be treated as flat strings (using JSON serialization).</span></span>

<span data-ttu-id="c004f-170">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="c004f-170">**Example:**</span></span>

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a><span data-ttu-id="c004f-171">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="c004f-171">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="c004f-172">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="c004f-172">Keys</span></span>
<span data-ttu-id="c004f-173">Merhaba her anahtarında `NSDictionary` normal ifade aşağıdaki hello eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="c004f-173">Each key in hello `NSDictionary` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="c004f-174">Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).</span><span class="sxs-lookup"><span data-stu-id="c004f-174">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="c004f-175">Boyut</span><span class="sxs-lookup"><span data-stu-id="c004f-175">Size</span></span>
<span data-ttu-id="c004f-176">Uygulama bilgilerini sınırlı çok**1024** (kez JSON'de hello katılım aracısı tarafından kodlanmış) çağrı başına karakter.</span><span class="sxs-lookup"><span data-stu-id="c004f-176">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement agent).</span></span>

<span data-ttu-id="c004f-177">Hello önceki hello toohello sunucu gönderilen JSON 44 karakter uzunluğunda örnektir:</span><span class="sxs-lookup"><span data-stu-id="c004f-177">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

    {"birthdate":"1983-12-07","gender":"female"}
