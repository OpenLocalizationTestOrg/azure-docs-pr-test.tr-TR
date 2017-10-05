---
title: "Android API katılım kullanma"
description: "En son Android SDK - Android API katılım kullanma"
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
ms.openlocfilehash: d353cd2fe47c54a0282cc5bb1b22b4a56e0cd82c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-the-engagement-api-on-android"></a><span data-ttu-id="d4fd9-103">Android API katılım kullanma</span><span class="sxs-lookup"><span data-stu-id="d4fd9-103">How to Use the Engagement API on Android</span></span>
<span data-ttu-id="d4fd9-104">Bu belge belgeye bir eklentidir [Android Mobile Engagement SDK'sı için Gelişmiş raporlama seçenekleri](mobile-engagement-android-advanced-reporting.md).</span><span class="sxs-lookup"><span data-stu-id="d4fd9-104">This document is an add-on to the document [Advanced Reporting options for Android Mobile Engagement SDK](mobile-engagement-android-advanced-reporting.md).</span></span> <span data-ttu-id="d4fd9-105">Katılım API uygulama istatistikleri rapor için nasıl kullanılacağı hakkındaki derinliği ayrıntıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-105">It provides in depth details about how to use the Engagement API to report your application statistics.</span></span>

<span data-ttu-id="d4fd9-106">Uygulamanızın oturumları, etkinlikleri, kilitlenme ve teknik bilgileri raporlamak için katılım yalnızca istiyorsanız, sonra en basit yolu tüm olduğunu aklınızda bulundurun, `Activity` alt sınıfları devralır denk gelen `EngagementActivity` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-106">Keep in mind that if you only want Engagement to report your application's sessions, activities, crashes and technical information, then the simplest way is to make all your `Activity` sub-classes inherit from the corresponding `EngagementActivity` class.</span></span>

<span data-ttu-id="d4fd9-107">Daha fazla bilgi için uygulama belirli olaylar, hatalar ve işleri, rapor gerekiyorsa örnek yapmak istiyorsanız veya uygulamanızın etkinlikleri uygulanan bir daha farklı bir şekilde bildirmek varsa `EngagementActivity` sınıfları yeniden katılım API'sini kullanmanız gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-107">If you want to do more, for example if you need to report application specific events, errors and jobs, or if you have to report your application's activities in a different way than the one implemented in the `EngagementActivity` classes, then you need to use the Engagement API.</span></span>

<span data-ttu-id="d4fd9-108">Katılım API'si tarafından sağlanan `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-108">The Engagement API is provided by the `EngagementAgent` class.</span></span> <span data-ttu-id="d4fd9-109">Bu sınıfın örneğini çağırarak alınabilir `EngagementAgent.getInstance(Context)` statik yöntemi (unutmayın `EngagementAgent` döndürülen tek nesnesidir).</span><span class="sxs-lookup"><span data-stu-id="d4fd9-109">An instance of this class can be retrieved by calling the `EngagementAgent.getInstance(Context)` static method (note that the `EngagementAgent` object returned is a singleton).</span></span>

## <a name="engagement-concepts"></a><span data-ttu-id="d4fd9-110">Engagement kavramları</span><span class="sxs-lookup"><span data-stu-id="d4fd9-110">Engagement concepts</span></span>
<span data-ttu-id="d4fd9-111">Aşağıdaki bölümleri yaygın İyileştir [Mobile Engagement kavramları](mobile-engagement-concepts.md), Android platformu için.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-111">The following parts refine the common [Mobile Engagement Concepts](mobile-engagement-concepts.md), for the Android platform.</span></span>

### <a name="session-and-activity"></a><span data-ttu-id="d4fd9-112">`Session` ve `Activity`</span><span class="sxs-lookup"><span data-stu-id="d4fd9-112">`Session` and `Activity`</span></span>
<span data-ttu-id="d4fd9-113">Kullanıcı birden fazla birkaç saniye arasında iki boşta kalırsa *etkinlikleri*, daha sonra kendi dizisini *etkinlikleri* iki ayrı bölünen *oturumları*.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-113">If the user stays more than a few seconds idle between two *activities*, then his sequence of *activities* is split in two distinct *sessions*.</span></span> <span data-ttu-id="d4fd9-114">Bu birkaç saniye "oturum zaman aşımı" adı verilir.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-114">These few seconds are called the "session timeout".</span></span>

<span data-ttu-id="d4fd9-115">Bir *etkinlik* yani genellikle uygulamanın bir ekran ile ilişkilendirilen *etkinlik* ekranı görüntülenir ve ekran kapatıldığında durdurduğunda başlatır: Engagement SDK'sını kullanarak tümleştirildiğinde bu durumda `EngagementActivity` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-115">An *activity* is usually associated with one screen of the application, that is to say the *activity* starts when the screen is displayed and stops when the screen is closed: this is the case when the Engagement SDK is integrated by using the `EngagementActivity` classes.</span></span>

<span data-ttu-id="d4fd9-116">Ancak *etkinlikleri* de el ile katılım API'si kullanılarak denetlenebilir.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-116">But *activities* can also be controlled manually by using the Engagement API.</span></span> <span data-ttu-id="d4fd9-117">Bu, birkaç alt bölümde bu ekrana (örneğin bilinen ne sıklıkta ve ne kadar süreyle iletişim kutuları içinde bu ekran kullanılır) kullanımı hakkında daha fazla bilgi almak için belirli bir ekran bölmek için sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-117">This allows to split a given screen in several sub parts to get more details about the usage of this screen (for example to known how often and how long dialogs are used inside this screen).</span></span>

## <a name="reporting-activities"></a><span data-ttu-id="d4fd9-118">Raporlama etkinlikleri</span><span class="sxs-lookup"><span data-stu-id="d4fd9-118">Reporting Activities</span></span>
> [!IMPORTANT]
> <span data-ttu-id="d4fd9-119">Etkinlikler gibi rapor kullanıyorsanız, bu bölümde açıklanan gerekmeyen `EngagementActivity` sınıfı ve türevleri tümleştirmek katılım nasıl Android belgede açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-119">You don't need to report activities like described in this section if you are using the `EngagementActivity` class and its variants as explained in the How to Integrate Engagement on Android document.</span></span>
> 
> 

### <a name="user-starts-a-new-activity"></a><span data-ttu-id="d4fd9-120">Kullanıcı yeni bir etkinlik başlatır</span><span class="sxs-lookup"><span data-stu-id="d4fd9-120">User starts a new Activity</span></span>
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing the current activity is required for Reach to display in-app notifications, passing null will postpone such announcements and polls.

<span data-ttu-id="d4fd9-121">Çağırmanız gerekir `startActivity()` kullanıcı etkinliği değişiklikleri her zaman.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-121">You need to call `startActivity()` each time the user activity changes.</span></span> <span data-ttu-id="d4fd9-122">Bu işlev ilk çağrıda yeni bir kullanıcı oturumu başlatır.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-122">The first call to this function starts a new user session.</span></span>

<span data-ttu-id="d4fd9-123">Bu işlevi çağırmak için en iyi her faaliyete yerdir `onResume` geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-123">The best place to call this function is on each activity `onResume` callback.</span></span>

### <a name="user-ends-his-current-activity"></a><span data-ttu-id="d4fd9-124">Kullanıcı kendi geçerli etkinliği sona erer</span><span class="sxs-lookup"><span data-stu-id="d4fd9-124">User ends his current Activity</span></span>
            EngagementAgent.getInstance(this).endActivity();

<span data-ttu-id="d4fd9-125">Çağırmanız gerekir `endActivity()` en az bir kez kullanıcı tamamlandığında son etkinliğini.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-125">You need to call `endActivity()` at least once when the user finishes his last activity.</span></span> <span data-ttu-id="d4fd9-126">Bu kullanıcı şu anda boşta kalır ve bir kez oturum zaman aşımı kapatılacak kullanıcı oturumunu gereksinim dolacak Engagement SDK'sı bildirir (çağırırsanız `startActivity()` oturumu yalnızca oturum zaman aşımı süresi dolmadan önce sürdürüldü).</span><span class="sxs-lookup"><span data-stu-id="d4fd9-126">This informs the Engagement SDK that the user is currently idle, and that the user session need to be closed once the session timeout will expire (if you call `startActivity()` before the session timeout expires, the session is simply resumed).</span></span>

<span data-ttu-id="d4fd9-127">Bu işlevi çağırmak için en iyi her faaliyete yerdir `onPause` geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-127">The best place to call this function is on each activity `onPause` callback.</span></span>

## <a name="reporting-events"></a><span data-ttu-id="d4fd9-128">Raporlama olayları</span><span class="sxs-lookup"><span data-stu-id="d4fd9-128">Reporting Events</span></span>
### <a name="session-events"></a><span data-ttu-id="d4fd9-129">Oturum olayları</span><span class="sxs-lookup"><span data-stu-id="d4fd9-129">Session events</span></span>
<span data-ttu-id="d4fd9-130">Oturum olaylar, genellikle kendi oturumu sırasında bir kullanıcı tarafından gerçekleştirilen eylemleri bildirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-130">Session events are usually used to report the actions performed by a user during his session.</span></span>

<span data-ttu-id="d4fd9-131">**Ek veriler olmadan örneği:**</span><span class="sxs-lookup"><span data-stu-id="d4fd9-131">**Example without extra data:**</span></span>

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

<span data-ttu-id="d4fd9-132">**Örnek ek veriler ile:**</span><span class="sxs-lookup"><span data-stu-id="d4fd9-132">**Example with extra data:**</span></span>

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

### <a name="standalone-events"></a><span data-ttu-id="d4fd9-133">Tek başına olayları</span><span class="sxs-lookup"><span data-stu-id="d4fd9-133">Standalone Events</span></span>
<span data-ttu-id="d4fd9-134">Oturum olayları aykırı bir oturum bağlamı dışında tek başına olaylar gerçekleşebilir.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-134">Contrary to session events, standalone events can occur outside of the context of a session.</span></span>

<span data-ttu-id="d4fd9-135">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="d4fd9-135">**Example:**</span></span>

<span data-ttu-id="d4fd9-136">Bir yayın alıcı tetiklendiğinde rapor olayların için istediğinizi varsayalım:</span><span class="sxs-lookup"><span data-stu-id="d4fd9-136">Suppose you want to report events occurring when a broadcast receiver is triggered:</span></span>

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a><span data-ttu-id="d4fd9-137">Hata Raporlama</span><span class="sxs-lookup"><span data-stu-id="d4fd9-137">Reporting Errors</span></span>
### <a name="session-errors"></a><span data-ttu-id="d4fd9-138">Oturum hataları</span><span class="sxs-lookup"><span data-stu-id="d4fd9-138">Session errors</span></span>
<span data-ttu-id="d4fd9-139">Oturum hatalar genellikle kendi oturumu sırasında kullanıcı etkileyen hatalarını bildirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-139">Session errors are usually used to report the errors impacting the user during his session.</span></span>

<span data-ttu-id="d4fd9-140">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="d4fd9-140">**Example:**</span></span>

            /** The user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* The user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a><span data-ttu-id="d4fd9-141">Tek başına hataları</span><span class="sxs-lookup"><span data-stu-id="d4fd9-141">Standalone errors</span></span>
<span data-ttu-id="d4fd9-142">Oturum hataları aykırı bir oturum bağlamı dışında tek başına hatalar oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-142">Contrary to session errors, standalone errors can occur outside of the context of a session.</span></span>

<span data-ttu-id="d4fd9-143">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="d4fd9-143">**Example:**</span></span>

<span data-ttu-id="d4fd9-144">Aşağıdaki örnek, uygulama işlemi çalışırken bellek telefonda azaldığında her bir hata raporu gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-144">The following example shows how to report an error whenever the memory becomes low on the phone while your application process is running.</span></span>

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a><span data-ttu-id="d4fd9-145">Raporlama işleri</span><span class="sxs-lookup"><span data-stu-id="d4fd9-145">Reporting Jobs</span></span>
### <a name="example"></a><span data-ttu-id="d4fd9-146">Örnek</span><span class="sxs-lookup"><span data-stu-id="d4fd9-146">Example</span></span>
<span data-ttu-id="d4fd9-147">Oturum açma işleminiz süresini rapor istediğinizi varsayalım:</span><span class="sxs-lookup"><span data-stu-id="d4fd9-147">Suppose you want to report the duration of your login process:</span></span>

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a><span data-ttu-id="d4fd9-148">Bir işi sırasında hatalarını raporla</span><span class="sxs-lookup"><span data-stu-id="d4fd9-148">Report Errors during a Job</span></span>
<span data-ttu-id="d4fd9-149">Geçerli kullanıcı oturumuyla ilgili yerine çalıştırılan bir iş hataları ile ilgili olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-149">Errors can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="d4fd9-150">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="d4fd9-150">**Example:**</span></span>

<span data-ttu-id="d4fd9-151">Raporu, sırasında bir hata oturum açma işlemi istediğinizi varsayalım:</span><span class="sxs-lookup"><span data-stu-id="d4fd9-151">Suppose you want to report an error during you login process:</span></span>

<span data-ttu-id="d4fd9-152">[...] Ortak void Signın (bağlam bağlamı,...) {</span><span class="sxs-lookup"><span data-stu-id="d4fd9-152">[...] public void signIn(Context context, ...) {</span></span>

              /* We need an Android context to call the Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try to sign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report the error to Engagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a><span data-ttu-id="d4fd9-153">Raporlama işi sırasında olayları</span><span class="sxs-lookup"><span data-stu-id="d4fd9-153">Reporting Events during a job</span></span>
<span data-ttu-id="d4fd9-154">Geçerli kullanıcı oturumuyla ilgili yerine çalıştırılan bir iş olayları ile ilgili olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-154">Events can be related to a running job instead of being related to the current user session.</span></span>

<span data-ttu-id="d4fd9-155">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="d4fd9-155">**Example:**</span></span>

<span data-ttu-id="d4fd9-156">Sosyal ağ sahibiz ve rapor için bir iş sunucusuna bağlı kullanıcı sırasında toplam süre kullanırız varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-156">Suppose we have a social network, and we use a job to report the total time during which the user is connected to the server.</span></span> <span data-ttu-id="d4fd9-157">Bu yüzden hiçbir oturum kullanıcı kendisinin başka bir uygulama kullanırken ya da telefon Uyuma arka planda bile bağlı kalabilir.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-157">The user can stay connected in background even when he's using another application or when the phone is sleeping, so there is no session.</span></span>

<span data-ttu-id="d4fd9-158">Kullanıcı kendi arkadaşlarınızdan ileti alabilir, bu proje bir olaydır.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-158">The user can receive messages from his friends, this is a job event.</span></span>

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

## <a name="extra-parameters"></a><span data-ttu-id="d4fd9-159">Ek parametreler</span><span class="sxs-lookup"><span data-stu-id="d4fd9-159">Extra parameters</span></span>
<span data-ttu-id="d4fd9-160">Rastgele veriler, olaylar, hatalar, etkinlikler ve işler eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-160">Arbitrary data can be attached to events, errors, activities and jobs.</span></span>

<span data-ttu-id="d4fd9-161">Bu verileri yapılandırılmış, Android'ın paket sınıfı kullanır (aslında, Android hedefleri ek parametreleri gibi çalışır).</span><span class="sxs-lookup"><span data-stu-id="d4fd9-161">This data can be structured, it uses Android's Bundle class (actually, it works like extra parameters in Android Intents).</span></span> <span data-ttu-id="d4fd9-162">Bir paket dizileri veya başka bir paket örneklerini içerebileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-162">Note that a Bundle can contain arrays or another Bundle instances.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4fd9-163">Parcelable veya seri hale getirilebilir parametrelerinde yerleştirirseniz emin olun, `toString()` yöntemi okunabilir dize döndürecek şekilde gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-163">If you put in parcelable or serializable parameters, make sure their `toString()` method is implemented to return a human-readable string.</span></span> <span data-ttu-id="d4fd9-164">Çağıracaksınız sırasında serileştirilebilir olmayan geçici olmayan alanlar içeriyor serileştirilebilir sınıflardan Android kilitlenme yapar`bundle.putSerializable("key",value);`</span><span class="sxs-lookup"><span data-stu-id="d4fd9-164">Serializable classes that contain non transient fields that are not serializable will make Android crash when you will call `bundle.putSerializable("key",value);`</span></span>
> 
> [!WARNING]
> <span data-ttu-id="d4fd9-165">Ek parametreler seyrek dizilerde desteklenmez, diğer bir deyişle, bir dizi olarak seri hale getirilmesi olmaz.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-165">Sparse arrays in extra parameters are not supported, that is, it won't be serialized as an array.</span></span> <span data-ttu-id="d4fd9-166">Bunları standart diziye ek parametreler kullanmadan önce dönüştürmeniz.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-166">You should convert them into standard arrays before using it in extra parameters.</span></span>
> 
> 

### <a name="example"></a><span data-ttu-id="d4fd9-167">Örnek</span><span class="sxs-lookup"><span data-stu-id="d4fd9-167">Example</span></span>
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a><span data-ttu-id="d4fd9-168">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="d4fd9-168">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="d4fd9-169">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="d4fd9-169">Keys</span></span>
<span data-ttu-id="d4fd9-170">Her anahtarında `Bundle` şu normal ifadeyle eşleşen gerekir:</span><span class="sxs-lookup"><span data-stu-id="d4fd9-170">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="d4fd9-171">Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).</span><span class="sxs-lookup"><span data-stu-id="d4fd9-171">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="d4fd9-172">Boyut</span><span class="sxs-lookup"><span data-stu-id="d4fd9-172">Size</span></span>
<span data-ttu-id="d4fd9-173">Ek özellikler sınırlı **1024** (kez JSON'de katılım hizmeti tarafından kodlanmış) çağrı başına karakter.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-173">Extras are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="d4fd9-174">Önceki örnekte, sunucuya gönderilen JSON 58 karakter olacak:</span><span class="sxs-lookup"><span data-stu-id="d4fd9-174">In the previous example, the JSON sent to the server is 58 characters long:</span></span>

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a><span data-ttu-id="d4fd9-175">Uygulama bilgilerini raporlama</span><span class="sxs-lookup"><span data-stu-id="d4fd9-175">Reporting Application Information</span></span>
<span data-ttu-id="d4fd9-176">İzleme bilgileri (veya diğer uygulama belirli bilgileri) kullanarak el ile raporlayabilirsiniz `sendAppInfo()` işlevi.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-176">You can manually report tracking information (or any other application specific information) using the `sendAppInfo()` function.</span></span>

<span data-ttu-id="d4fd9-177">Bu bilgi artımlı olarak gönderilebilir Not: belirli bir aygıt için belirli bir anahtar için yalnızca en son değeri korunur.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-177">Note that these information can be sent incrementally: only the latest value for a given key will be kept for a given device.</span></span>

<span data-ttu-id="d4fd9-178">Olay ek özellikler gibi paket sınıfı uygulama bilgilerini soyut, kullanılan diziler veya alt paketleri (JSON serileştirmesi kullanan) düz dize olarak kabul olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-178">Like event extras, the Bundle class is used to abstract application information, note that arrays or sub-bundles will be treated as flat strings (using JSON serialization).</span></span>

### <a name="example"></a><span data-ttu-id="d4fd9-179">Örnek</span><span class="sxs-lookup"><span data-stu-id="d4fd9-179">Example</span></span>
<span data-ttu-id="d4fd9-180">Kullanıcı cinsiyeti ve doğum tarihi göndermek için bir kod örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="d4fd9-180">Here is a code sample to send user gender and birthdate:</span></span>

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a><span data-ttu-id="d4fd9-181">Sınırlar</span><span class="sxs-lookup"><span data-stu-id="d4fd9-181">Limits</span></span>
#### <a name="keys"></a><span data-ttu-id="d4fd9-182">Anahtarlar</span><span class="sxs-lookup"><span data-stu-id="d4fd9-182">Keys</span></span>
<span data-ttu-id="d4fd9-183">Her anahtarında `Bundle` şu normal ifadeyle eşleşen gerekir:</span><span class="sxs-lookup"><span data-stu-id="d4fd9-183">Each key in the `Bundle` must match the following regular expression:</span></span>

`^[a-zA-Z][a-zA-Z_0-9]*`

<span data-ttu-id="d4fd9-184">Anahtarları harfler, sayılar veya alt çizgi izlemelidir en az bir harf ile başlamalıdır anlamına gelir (\_).</span><span class="sxs-lookup"><span data-stu-id="d4fd9-184">It means that keys must start with at least one letter, followed by letters, digits or underscores (\_).</span></span>

#### <a name="size"></a><span data-ttu-id="d4fd9-185">Boyut</span><span class="sxs-lookup"><span data-stu-id="d4fd9-185">Size</span></span>
<span data-ttu-id="d4fd9-186">Uygulama bilgilerini sınırlı **1024** (kez JSON'de katılım hizmeti tarafından kodlanmış) çağrı başına karakter.</span><span class="sxs-lookup"><span data-stu-id="d4fd9-186">Application information are limited to **1024** characters per call (once encoded in JSON by the Engagement service).</span></span>

<span data-ttu-id="d4fd9-187">Önceki örnekte, sunucuya gönderilen JSON 44 karakter olacak:</span><span class="sxs-lookup"><span data-stu-id="d4fd9-187">In the previous example, the JSON sent to the server is 44 characters long:</span></span>

            {"expiration":"2016-12-07","status":"premium"}
