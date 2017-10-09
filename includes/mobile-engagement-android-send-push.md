
### <a name="update-manifest-file-tooenable-notifications"></a><span data-ttu-id="dfefd-101">Güncelleştirme bildirim dosyası tooenable bildirimleri</span><span class="sxs-lookup"><span data-stu-id="dfefd-101">Update manifest file tooenable notifications</span></span>
<span data-ttu-id="dfefd-102">Merhaba uygulama içi Mesajlaşma kaynaklarını aşağıdaki manifest.XML dosyanızda hello arasında kopyalama `<application>` ve `</application>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="dfefd-102">Copy hello in-app messaging resources below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementTextAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
              <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/plain" />
              </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementWebAnnouncementActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ANNOUNCEMENT"/>
                <category android:name="android.intent.category.DEFAULT" />
                <data android:mimeType="text/html" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementPollActivity" android:theme="@android:style/Theme.Light" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.POLL"/>
                <category android:name="android.intent.category.DEFAULT" />
            </intent-filter>
        </activity>
        <activity android:name="com.microsoft.azure.engagement.reach.activity.EngagementLoadingActivity" android:theme="@android:style/Theme.Dialog" android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.LOADING"/>
                <category android:name="android.intent.category.DEFAULT"/>
            </intent-filter>
        </activity>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachReceiver" android:exported="false">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.AGENT_CREATED"/>
                <action android:name="com.microsoft.azure.engagement.intent.action.MESSAGE"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.ACTION_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.EXIT_NOTIFICATION"/>
                <action android:name="com.microsoft.azure.engagement.reach.intent.action.DOWNLOAD_TIMEOUT"/>
            </intent-filter>
        </receiver>
        <receiver android:name="com.microsoft.azure.engagement.reach.EngagementReachDownloadReceiver">
            <intent-filter>
                <action android:name="android.intent.action.DOWNLOAD_COMPLETE"/>
            </intent-filter>
        </receiver>

### <a name="specify-an-icon-for-notifications"></a><span data-ttu-id="dfefd-103">Bildirimler için simge belirtme</span><span class="sxs-lookup"><span data-stu-id="dfefd-103">Specify an icon for notifications</span></span>
<span data-ttu-id="dfefd-104">Merhaba arasında Manifest.xml dosyanızda yer XML parçacığını aşağıdaki Yapıştır hello `<application>` ve `</application>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="dfefd-104">Paste hello following XML snippet in your Manifest.xml between hello `<application>` and `</application>` tags.</span></span>

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

<span data-ttu-id="dfefd-105">Bu, hem de sistem ve uygulama içi bildirimler görüntülenen hello simgesini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="dfefd-105">This defines hello icon that is displayed both in system and in-app notifications.</span></span> <span data-ttu-id="dfefd-106">Bu, uygulama içi bildirimler için isteğe bağlı olsa da, sistem bildirimleri için zorunludur.</span><span class="sxs-lookup"><span data-stu-id="dfefd-106">It is optional for in-app notifications however mandatory for system notifications.</span></span> <span data-ttu-id="dfefd-107">Android, geçersiz simgelere sahip sistem bildirimlerini reddeder.</span><span class="sxs-lookup"><span data-stu-id="dfefd-107">Android will rejects system notifications with invalid icons.</span></span>

<span data-ttu-id="dfefd-108">Kullanmakta olduğunuz var simge hello birinde emin olun **drawable** klasörleri (gibi ``engagement_close.png``).</span><span class="sxs-lookup"><span data-stu-id="dfefd-108">Make sure you are using an icon that exists in one of hello **drawable** folders (like ``engagement_close.png``).</span></span> <span data-ttu-id="dfefd-109">**mipmap** klasörü desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="dfefd-109">**mipmap** folder isn't supported.</span></span>

> [!NOTE]
> <span data-ttu-id="dfefd-110">Merhaba kullanmamalıdır **Başlatıcısı** simgesi.</span><span class="sxs-lookup"><span data-stu-id="dfefd-110">You should not use hello **launcher** icon.</span></span> <span data-ttu-id="dfefd-111">Farklı bir çözünürlüğü vardır ve çoğunlukla desteklemediğimiz hello mipmap klasörlerinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="dfefd-111">It has a different resolution and is usually in hello mipmap folders, which we don't support.</span></span>
> 
> 

<span data-ttu-id="dfefd-112">Gerçek uygulamalar için, her[Android tasarım yönergesi](http://developer.android.com/design/patterns/notifications.html) için bir bildirime uygun simgeleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfefd-112">For real apps, you can use an icon that is suitable for notifications per [Android design guidelines](http://developer.android.com/design/patterns/notifications.html).</span></span>

> [!TIP]
> <span data-ttu-id="dfefd-113">toobe emin toouse doğru simge çözünürlüğü göz önünde bulundurmanız adresindeki [Bu örnekler](https://www.google.com/design/icons).</span><span class="sxs-lookup"><span data-stu-id="dfefd-113">toobe sure toouse correct icon resolutions, you can look at [these examples](https://www.google.com/design/icons).</span></span>
> <span data-ttu-id="dfefd-114">Toohello aşağı **bildirim** bölümünde, bir simgesine tıklayın ve ardından `PNGS` toodownload hello simge çizilebilir kümesini.</span><span class="sxs-lookup"><span data-stu-id="dfefd-114">Scroll down toohello **Notification** section, click an icon, and then click `PNGS` toodownload hello icon drawable set.</span></span> <span data-ttu-id="dfefd-115">Hangi drawable klasörlerde hangi çözümleme toouse hello simgesi her sürümü ile görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dfefd-115">You can see what drawable folders with which resolution toouse for each version of hello icon.</span></span>
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a><span data-ttu-id="dfefd-116">Uygulama tooreceive GCM anında iletme bildirimlerini etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="dfefd-116">Enable your app tooreceive GCM push notifications</span></span>
1. <span data-ttu-id="dfefd-117">Merhaba arasında manifest.XML dosyanızda hello aşağıdaki Yapıştır `<application>` ve `</application>` hello değiştirildikten sonra etiketleri **Gönderen Kimliği** Firebase proje konsolunuzdan elde.</span><span class="sxs-lookup"><span data-stu-id="dfefd-117">Paste hello following into your Manifest.xml between hello `<application>` and `</application>` tags after replacing hello **Sender ID** obtained from your Firebase project console.</span></span> <span data-ttu-id="dfefd-118">Merhaba \n maksatlı şekilde hello proje numarasını bitirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="dfefd-118">hello \n is intentional so make sure that you end hello project number with it.</span></span>
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. <span data-ttu-id="dfefd-119">Merhaba arasında manifest.XML dosyanızda hello kodu kopyalayıp yapıştırın `<application>` ve `</application>` etiketler.</span><span class="sxs-lookup"><span data-stu-id="dfefd-119">Paste hello code below into your Manifest.xml between hello `<application>` and `</application>` tags.</span></span> <span data-ttu-id="dfefd-120">Merhaba paket adını değiştirin <Your package name>.</span><span class="sxs-lookup"><span data-stu-id="dfefd-120">Replace hello package name <Your package name>.</span></span>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMEnabler"
        android:exported="false">
            <intent-filter>
                <action android:name="com.microsoft.azure.engagement.intent.action.APPID_GOT" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.microsoft.azure.engagement.gcm.EngagementGCMReceiver" android:permission="com.google.android.c2dm.permission.SEND">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
                <action android:name="com.google.android.c2dm.intent.RECEIVE" />
                <category android:name="<Your package name>" />
            </intent-filter>
        </receiver>
3. <span data-ttu-id="dfefd-121">Merhaba son önce hello vurgulanmıştır izinler kümesini eklemek `<application>` etiketi.</span><span class="sxs-lookup"><span data-stu-id="dfefd-121">Add hello last set of permissions that are highlighted before hello `<application>` tag.</span></span> <span data-ttu-id="dfefd-122">Değiştir `<Your package name>` uygulamanızın hello asıl Paket adıyla.</span><span class="sxs-lookup"><span data-stu-id="dfefd-122">Replace `<Your package name>` by hello actual package name of your application.</span></span>
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

