1. Açık hello Android SDK Manager Android Studio hello araç çubuğundaki hello simgesini tıklatarak veya tıklayarak **Araçları** -> **Android** -> **SDK Manager**hello menüsünde. Projenizde Hello hedef hello kullanılan Android SDK sürümünü bulun, tıklayarak açın **Paket ayrıntılarını göster**ve seçin **Google API'leri**, zaten yüklü değilse.
2. Merhaba tıklatın **SDK Araçları** sekmesi. Google Play Hizmeti’ni zaten yüklemediyseniz **Google Play Hizmetleri** ’ne, aşağıda gösterildiği gibi tıklayın. Ardından **Uygula** tooinstall. 
   
    Sonraki adımda kullanmak için Hello SDK yolunu not edin. 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. Açık hello **build.gradle** hello uygulama dizinindeki dosyasını.
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. *Bağımlılıklar* ’ın altına bu satırı ekleyin: 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. Merhaba tıklatın **projeyi Gradle dosyalarıyla Eşitle** hello araç çubuğunda simge.
6. Açık **AndroidManifest.xml** ve bu etiketi toohello ekleyin *uygulama* etiketi.
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

