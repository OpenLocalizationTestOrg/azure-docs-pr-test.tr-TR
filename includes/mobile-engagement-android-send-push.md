
### <a name="update-manifest-file-tooenable-notifications"></a>Güncelleştirme bildirim dosyası tooenable bildirimleri
Merhaba uygulama içi Mesajlaşma kaynaklarını aşağıdaki manifest.XML dosyanızda hello arasında kopyalama `<application>` ve `</application>` etiketler.

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

### <a name="specify-an-icon-for-notifications"></a>Bildirimler için simge belirtme
Merhaba arasında Manifest.xml dosyanızda yer XML parçacığını aşağıdaki Yapıştır hello `<application>` ve `</application>` etiketler.

        <meta-data android:name="engagement:reach:notification:icon" android:value="engagement_close"/>

Bu, hem de sistem ve uygulama içi bildirimler görüntülenen hello simgesini tanımlar. Bu, uygulama içi bildirimler için isteğe bağlı olsa da, sistem bildirimleri için zorunludur. Android, geçersiz simgelere sahip sistem bildirimlerini reddeder.

Kullanmakta olduğunuz var simge hello birinde emin olun **drawable** klasörleri (gibi ``engagement_close.png``). **mipmap** klasörü desteklenmez.

> [!NOTE]
> Merhaba kullanmamalıdır **Başlatıcısı** simgesi. Farklı bir çözünürlüğü vardır ve çoğunlukla desteklemediğimiz hello mipmap klasörlerinde yer alır.
> 
> 

Gerçek uygulamalar için, her[Android tasarım yönergesi](http://developer.android.com/design/patterns/notifications.html) için bir bildirime uygun simgeleri kullanabilirsiniz.

> [!TIP]
> toobe emin toouse doğru simge çözünürlüğü göz önünde bulundurmanız adresindeki [Bu örnekler](https://www.google.com/design/icons).
> Toohello aşağı **bildirim** bölümünde, bir simgesine tıklayın ve ardından `PNGS` toodownload hello simge çizilebilir kümesini. Hangi drawable klasörlerde hangi çözümleme toouse hello simgesi her sürümü ile görebilirsiniz.
> 
> 

### <a name="enable-your-app-tooreceive-gcm-push-notifications"></a>Uygulama tooreceive GCM anında iletme bildirimlerini etkinleştirin
1. Merhaba arasında manifest.XML dosyanızda hello aşağıdaki Yapıştır `<application>` ve `</application>` hello değiştirildikten sonra etiketleri **Gönderen Kimliği** Firebase proje konsolunuzdan elde. Merhaba \n maksatlı şekilde hello proje numarasını bitirdiğinizden emin olun.
   
        <meta-data android:name="engagement:gcm:sender" android:value="************\n" />
2. Merhaba arasında manifest.XML dosyanızda hello kodu kopyalayıp yapıştırın `<application>` ve `</application>` etiketler. Merhaba paket adını değiştirin <Your package name>.
   
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
3. Merhaba son önce hello vurgulanmıştır izinler kümesini eklemek `<application>` etiketi. Değiştir `<Your package name>` uygulamanızın hello asıl Paket adıyla.
   
        <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE" />
        <uses-permission android:name="<Your package name>.permission.C2D_MESSAGE" />
        <permission android:name="<Your package name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />

