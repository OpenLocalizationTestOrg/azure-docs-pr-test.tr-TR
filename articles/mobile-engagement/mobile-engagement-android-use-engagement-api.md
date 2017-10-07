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
# <a name="how-toouse-hello-engagement-api-on-android"></a><span data-ttu-id="cee61-103">Nasıl tooUse hello Android katılım API</span><span class="sxs-lookup"><span data-stu-id="cee61-103">How tooUse hello Engagement API on Android</span></span>
<span data-ttu-id="cee61-104">Bu belge bir eklenti toohello belgesidir [Android Mobile Engagement SDK'sı için Gelişmiş raporlama seçenekleri](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="cee61-104">This document is an add-on toohello document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="cee61-105">Nasıl toouse hello katılım API tooreport uygulama istatistikleri hakkında ayrıntılar derinliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="cee61-105">It provides in depth details about how toouse hello Engagement API tooreport your application statistics.</span></span>

<span data-ttu-id="cee61-106">Yalnızca katılım tooreport uygulamanızın oturumları, etkinlikleri, kilitlenme ve teknik bilgi istiyorsanız, ardından hello en basit yolu toomake tüm olduğunu aklınızda bulundurun, `Activity` alt sınıfları devral hello karşılık gelen `EngagementActivity` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="cee61-106">Keep in mind that if you only want Engagement tooreport your application's sessions, activities, crashes and technical information, then hello simplest way is toomake all your `Activity` sub-classes inherit from hello corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="cee61-107">Daha fazla tooreport uygulama belirli olaylar, hatalar ve işleri gerekiyorsa örneğin toodo istiyorsanız veya tooreport uygulamanızın etkinlikleri farklı bir şekilde bir hello uygulanan hello daha varsa `EngagementActivity` sınıfları yeniden toouse hello gerekiyor Katılım API.</span><span class="sxs-lookup"><span data-stu-id="cee61-107">If you want toodo more, for example if you need tooreport application specific events, errors and jobs, or if you have tooreport your application's activities in a different way than hello one implemented in hello `EngagementActivity` classes, then you need toouse hello Engagement API.</span></span>

<span data-ttu-id="cee61-108">Merhaba katılım API hello tarafından sağlanan `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="cee61-108">hello Engagement API is provided by hello `EngagementAgent` class.</span></span> <span data-ttu-id="cee61-109">Bu sınıfın bir örneği tarafından arama hello alınabilir `EngagementAgent.getInstance(Context)` statik yöntemi (Bu hello Not `EngagementAgent` döndürülen tek nesnesidir).</span><span class="sxs-lookup"><span data-stu-id="cee61-109">An instance of this class can be retrieved by calling hello `EngagementAgent.getInstance(Context)` static method (note that hello `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="cee61-110">Engagement kavramları</span><span class="sxs-lookup"><span data-stu-id="cee61-110">Engagement concepts</span></span>
<span data-ttu-id="cee61-111">Merhaba aşağıdaki bölümleri İyileştir hello ortak [Mobile Engagement kavramları](mobile-engagement-concepts.md), hello Android platformu için.</span><span class="sxs-lookup"><span data-stu-id="cee61-111">hello following parts refine hello common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for hello Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="cee61-112">`Session` ve `Activity`</span><span class="sxs-lookup"><span data-stu-id="cee61-112">`Session` and `Activity`</span></span>
<span data-ttu-id="cee61-113">Hello kullanıcı birden fazla birkaç saniye arasında iki boşta kalırsa *etkinlikleri*, daha sonra kendi dizisini *etkinlikleri* iki ayrı bölünen *oturumları*.</span><span class="sxs-lookup"><span data-stu-id="cee61-113">If hello user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="cee61-114">Bu birkaç saniye hello "oturum zaman aşımı" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="cee61-114">These few seconds are called hello "session timeout".</span></span>

<span data-ttu-id="cee61-115">Bir *etkinlik* toosay hello hello uygulama, bir ekran ile genellikle ilişkili *etkinlik* Merhaba ekranında görüntülenir ve Merhaba ekranında kapatıldığında durdurduğunda başlatır: hello budur ne zaman durumda Merhaba Engagement SDK'sı hello kullanarak tümleşik `EngagementActivity` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="cee61-115">An *activity* is usually associated with one screen of hello application, that is toosay hello *activity* starts when hello screen is displayed and stops when hello screen is closed: this is hello case when hello Engagement SDK is integrated by using hello `EngagementActivity` classes.</span></span>

<span data-ttu-id="cee61-116">Ancak *etkinlikleri* de el ile Merhaba katılım API kullanılarak denetlenebilir.</span><span class="sxs-lookup"><span data-stu-id="cee61-116">But *activities* can also be controlled manually by using hello Engagement API.</span></span> <span data-ttu-id="cee61-117">Bu toosplit belirli bir ekran hakkında daha fazla ayrıntı (örneğin tooknown ne sıklıkta ve ne kadar süreyle iletişim kutuları içinde bu ekran kullanılır) bu ekran kullanımını hello birkaç alt bölümleri tooget sağlar.</span><span class="sxs-lookup"><span data-stu-id="cee61-117">This allows toosplit a given screen in several sub parts tooget more details about hello usage of this screen (for example tooknown how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="cee61-118">Raporlama etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="cee61-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="cee61-119">Merhaba kullanıyorsanız, bu bölümde açıklandığı gibi tooreport etkinlikler gerekmeyen `EngagementActivity` sınıfı ve türevleri hello nasıl açıklandığı gibi Android belgesinde tooIntegrate katılım.</span><span class="sxs-lookup"><span data-stu-id="cee61-119">You don't need tooreport activities like described in this section if you are using hello `EngagementActivity` class and its variants as explained in hello How tooIntegrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="cee61-120">Kullanıcı yeni bir etkinlik başlatır</span><span class="sxs-lookup"><span data-stu-id="cee61-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="cee61-121">Toocall gerek `startActivity()` her zaman hello kullanıcı etkinliği değiştirir.</span><span class="sxs-lookup"><span data-stu-id="cee61-121">You need toocall `startActivity()` each time hello user activity changes.</span></span> <span data-ttu-id="cee61-122">Merhaba ilk çağrı toothis işlevi yeni bir kullanıcı oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="cee61-122">hello first call toothis function starts a new user session.</span></span>

<span data-ttu-id="cee61-123">Bu işlev, her etkinlik üzerinde kullanılır en iyi yeri toocall hello `onResume` geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="cee61-123">hello best place toocall this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="cee61-124">Kullanıcı kendi geçerli etkinliği sona erer</span><span class="sxs-lookup"><span data-stu-id="cee61-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="cee61-125">Toocall gerek `endActivity()` en az bir kez hello kullanıcı tamamlandığında son etkinliğini.</span><span class="sxs-lookup"><span data-stu-id="cee61-125">You need toocall `endActivity()` at least once when hello user finishes his last activity.</span></span> <span data-ttu-id="cee61-126">Bu Engagement SDK'sı hello kullanıcı şu anda boşta ve hello kullanıcı oturumu toobe gerektiğini bildiren bir kez hello oturum zaman aşımı kapalı dolacak hello bildirir (çağırırsanız `startActivity()` hello oturum yalnızca hello oturum zaman aşımı süresi dolmadan önce sürdürüldü).</span><span class="sxs-lookup"><span data-stu-id="cee61-126">This informs hello Engagement SDK that hello user is currently idle, and that hello user session need toobe closed once hello session timeout will expire (if you call `startActivity()` before hello session timeout expires, hello session is simply resumed).</span></span>

<span data-ttu-id="cee61-127">Bu işlev, her etkinlik üzerinde kullanılır en iyi yeri toocall hello `onPause` geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="cee61-127">hello best place toocall this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="cee61-128">Raporlama olayları</span><span class="sxs-lookup"><span data-stu-id="cee61-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="cee61-129">Oturum olayları</span><span class="sxs-lookup"><span data-stu-id="cee61-129">Session events</span></span>
<span data-ttu-id="cee61-130">Oturum, kendi oturumunda bir kullanıcı tarafından gerçekleştirilen genellikle kullanılan tooreport hello Eylemler olaylardır.</span><span class="sxs-lookup"><span data-stu-id="cee61-130">Session events are usually used tooreport hello actions performed by a user during his session.</span></span>

<span data-ttu-id="cee61-131">**Ek veriler olmadan örneği:**</span><span class="sxs-lookup"><span data-stu-id="cee61-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="cee61-132">**Örnek ek veriler ile:**</span><span class="sxs-lookup"><span data-stu-id="cee61-132">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="cee61-133">Tek başına olayları</span><span class="sxs-lookup"><span data-stu-id="cee61-133">Standalone Events</span></span>
<span data-ttu-id="cee61-134">Bulmadýðýný toosession olayları, bir oturum Merhaba içeriğine dışında tek başına olaylar gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="cee61-134">Contrary toosession events, standalone events can occur outside of hello context of a session.</span></span>

<span data-ttu-id="cee61-135">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="cee61-135">**Example:**</span></span>

<span data-ttu-id="cee61-136">Bir yayın alıcı tetiklendiğinde tooreport olayların istediğinizi varsayalım:</span><span class="sxs-lookup"><span data-stu-id="cee61-136">Suppose you want tooreport events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="cee61-137">Hata Raporlama</span><span class="sxs-lookup"><span data-stu-id="cee61-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="cee61-138">Oturum hataları</span><span class="sxs-lookup"><span data-stu-id="cee61-138">Session errors</span></span>
<span data-ttu-id="cee61-139">Oturum hatalar hello kullanıcı kendi oturumunda etkileyen genellikle kullanılan tooreport hello hatalardır.</span><span class="sxs-lookup"><span data-stu-id="cee61-139">Session errors are usually used tooreport hello errors impacting hello user during his session.</span></span>

<span data-ttu-id="cee61-140">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="cee61-140">**Example:**</span></span>

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

### <a name="standalone-errors"></a><span data-ttu-id="cee61-141">Tek başına hataları</span><span class="sxs-lookup"><span data-stu-id="cee61-141">Standalone errors</span></span>
<span data-ttu-id="cee61-142">Bulmadýðýný toosession hataları, bir oturum Merhaba içeriğine dışında tek başına hatalar oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="cee61-142">Contrary toosession errors, standalone errors can occur outside of hello context of a session.</span></span>

<span data-ttu-id="cee61-143">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="cee61-143">**Example:**</span></span>

<span data-ttu-id="cee61-144">Merhaba aşağıdaki örnekte tooreport uygulama işlemi sırasında hello telefonda hello bellek azaldığında her bir hata nasıl çalıştığı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="cee61-144">hello following example shows how tooreport an error whenever hello memory becomes low on hello phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="cee61-145">Raporlama işleri</span><span class="sxs-lookup"><span data-stu-id="cee61-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="cee61-146">Örnek</span><span class="sxs-lookup"><span data-stu-id="cee61-146">Example</span></span>
<span data-ttu-id="cee61-147">Oturum açma işleminiz tooreport hello süresi istediğinizi varsayalım:</span><span class="sxs-lookup"><span data-stu-id="cee61-147">Suppose you want tooreport hello duration of your login process:</span></span>

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

### <a name="report-errors-during-a-job"></a><span data-ttu-id="cee61-148">Bir işi sırasında hatalarını raporla</span><span class="sxs-lookup"><span data-stu-id="cee61-148">Report Errors during a Job</span></span>
<span data-ttu-id="cee61-149">Hataları olan yerine işi ilgili tooa olabilir ilgili toohello geçerli kullanıcı oturumunun.</span><span class="sxs-lookup"><span data-stu-id="cee61-149">Errors can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="cee61-150">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="cee61-150">**Example:**</span></span>

<span data-ttu-id="cee61-151">Tooreport istediğinizi düşünelim, sırasında bir hata işlem oturum açma:</span><span class="sxs-lookup"><span data-stu-id="cee61-151">Suppose you want tooreport an error during you login process:</span></span>

<span data-ttu-id="cee61-152">[...] Ortak void Signın (bağlam bağlamı,...) {</span><span class="sxs-lookup"><span data-stu-id="cee61-152">[...] public void signIn(Context context, ...) {</span></span>

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

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="cee61-153">Raporlama işi sırasında olayları</span><span class="sxs-lookup"><span data-stu-id="cee61-153">Reporting Events during a job</span></span>
<span data-ttu-id="cee61-154">Olaylar, ilgili tooa olmak yerine işi çalıştırmayı olabilir ilgili toohello geçerli kullanıcı oturumunun.</span><span class="sxs-lookup"><span data-stu-id="cee61-154">Events can be related tooa running job instead of being related toohello current user session.</span></span>

<span data-ttu-id="cee61-155">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="cee61-155">**Example:**</span></span>

<span data-ttu-id="cee61-156">Sosyal ağ sahibiz ve hangi hello sırasında kullanıcı bağlı toohello sunucusudur bir iş tooreport hello toplam süre kullanırız varsayalım.</span><span class="sxs-lookup"><span data-stu-id="cee61-156">Suppose we have a social network, and we use a job tooreport hello total time during which hello user is connected toohello server.</span></span> <span data-ttu-id="cee61-157">Bu yüzden hiçbir oturum hello kullanıcı bile kendisinin başka bir uygulama kullanıyorsa veya hello telefon Uyuma arka planda bağlı kalabilir.</span><span class="sxs-lookup"><span data-stu-id="cee61-157">hello user can stay connected in background even when he's using another application or when hello phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="cee61-158">Merhaba kullanıcı kendi arkadaşlarınızdan ileti alabilir, bu proje bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="cee61-158">hello user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="cee61-159">Ek parametreler</span><span class="sxs-lookup"><span data-stu-id="cee61-159">Extra parameters</span></span>
<span data-ttu-id="cee61-160">Rastgele veriler ekli tooevents, hatalar, etkinlikler ve işler olabilir.</span><span class="sxs-lookup"><span data-stu-id="cee61-160">Arbitrary data can be attached tooevents, errors, activities and jobs.</span></span>

<span data-ttu-id="cee61-161">Bu verileri yapılandırılmış, Android'ın paket sınıfı kullanır (aslında, Android hedefleri ek parametreleri gibi çalışır).</span><span class="sxs-lookup"><span data-stu-id="cee61-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="cee61-162">Bir paket dizileri veya başka bir paket örneklerini içerebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="cee61-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cee61-163">Parcelable veya seri hale getirilebilir parametrelerinde yerleştirirseniz emin olun, `toString()` uygulanan tooreturn okunabilir dize bir yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="cee61-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented tooreturn a human-readable string.</span></span> <span data-ttu-id="cee61-164">Çağıracaksınız sırasında serileştirilebilir olmayan geçici olmayan alanlar içeriyor serileştirilebilir sınıflardan Android kilitlenme yapar`bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="cee61-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="cee61-165">Ek parametreler seyrek dizilerde desteklenmez, diğer bir deyişle, bir dizi olarak seri hale getirilmesi olmaz.</span><span class="sxs-lookup"><span data-stu-id="cee61-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="cee61-166">Bunları standart diziye ek parametreler kullanmadan önce dönüştürmeniz.</span><span class="sxs-lookup"><span data-stu-id="cee61-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="cee61-167">Örnek</span><span class="sxs-lookup"><span data-stu-id="cee61-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="cee61-168">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="cee61-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="cee61-169">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="cee61-169">Keys</span></span>
<span data-ttu-id="cee61-170">Merhaba her anahtarında `Bundle` normal ifade aşağıdaki hello eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="cee61-170">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="cee61-171">Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).</span><span class="sxs-lookup"><span data-stu-id="cee61-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="cee61-172">Boyut</span><span class="sxs-lookup"><span data-stu-id="cee61-172">Size</span></span>
<span data-ttu-id="cee61-173">Ek özellikler sınırlı çok**1024** (kez JSON'de hello katılım hizmeti tarafından kodlanmış) çağrı başına karakter.</span><span class="sxs-lookup"><span data-stu-id="cee61-173">Extras are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="cee61-174">Hello önceki hello toohello sunucu gönderilen JSON 58 karakter uzunluğunda örnektir:</span><span class="sxs-lookup"><span data-stu-id="cee61-174">In hello previous example, hello JSON sent toohello server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="cee61-175">Uygulama bilgilerini raporlama</span><span class="sxs-lookup"><span data-stu-id="cee61-175">Reporting Application Information</span></span>
<span data-ttu-id="cee61-176">İzleme hello kullanarak bilgi (veya diğer uygulama belirli bilgileri) el ile raporlayabilirsiniz `sendAppInfo()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="cee61-176">You can manually report tracking information (or any other application specific information) using hello `sendAppInfo()` function.</span></span>

<span data-ttu-id="cee61-177">Bu bilgi artımlı olarak gönderilebilir Not: yalnızca hello son değer belirli bir anahtar için belirli bir aygıt için korunur.</span><span class="sxs-lookup"><span data-stu-id="cee61-177">Note that these information can be sent incrementally: only hello latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="cee61-178">Olay ek özellikler gibi hello paket sınıfı kullanılan tooabstract uygulama bilgileri, dizi veya alt sunmaktadır unutmayın (JSON serileştirmesi kullanan) düz dize olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="cee61-178">Like event extras, hello Bundle class is used tooabstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="cee61-179">Örnek</span><span class="sxs-lookup"><span data-stu-id="cee61-179">Example</span></span>
<span data-ttu-id="cee61-180">İşte, kod örnek toosend kullanıcı cinsiyeti ve doğum tarihi:</span><span class="sxs-lookup"><span data-stu-id="cee61-180">Here is a code sample toosend user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="cee61-181">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="cee61-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="cee61-182">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="cee61-182">Keys</span></span>
<span data-ttu-id="cee61-183">Merhaba her anahtarında `Bundle` normal ifade aşağıdaki hello eşleşmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="cee61-183">Each key in hello `Bundle` must match hello following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="cee61-184">Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).</span><span class="sxs-lookup"><span data-stu-id="cee61-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="cee61-185">Boyut</span><span class="sxs-lookup"><span data-stu-id="cee61-185">Size</span></span>
<span data-ttu-id="cee61-186">Uygulama bilgilerini sınırlı çok**1024** (kez JSON'de hello katılım hizmeti tarafından kodlanmış) çağrı başına karakter.</span><span class="sxs-lookup"><span data-stu-id="cee61-186">Application information are limited too**1024** characters per call (once encoded in JSON by hello Engagement service).</span></span>

<span data-ttu-id="cee61-187">Hello önceki hello toohello sunucu gönderilen JSON 44 karakter uzunluğunda örnektir:</span><span class="sxs-lookup"><span data-stu-id="cee61-187">In hello previous example, hello JSON sent toohello server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
