1. <span data-ttu-id="161ab-101">Açık hello Android SDK Manager Android Studio hello araç çubuğundaki hello simgesini tıklatarak veya tıklayarak **Araçları** -> **Android** -> **SDK Manager**hello menüsünde.</span><span class="sxs-lookup"><span data-stu-id="161ab-101">Open hello Android SDK Manager by clicking hello icon on hello toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on hello menu.</span></span> <span data-ttu-id="161ab-102">Projenizde Hello hedef hello kullanılan Android SDK sürümünü bulun, tıklayarak açın **Paket ayrıntılarını göster**ve seçin **Google API'leri**, zaten yüklü değilse.</span><span class="sxs-lookup"><span data-stu-id="161ab-102">Locate hello target version of hello Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="161ab-103">Merhaba tıklatın **SDK Araçları** sekmesi. Google Play Hizmeti’ni zaten yüklemediyseniz **Google Play Hizmetleri** ’ne, aşağıda gösterildiği gibi tıklayın.</span><span class="sxs-lookup"><span data-stu-id="161ab-103">Click hello **SDK Tools** tab. If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="161ab-104">Ardından **Uygula** tooinstall.</span><span class="sxs-lookup"><span data-stu-id="161ab-104">Then click **Apply** tooinstall.</span></span> 
   
    <span data-ttu-id="161ab-105">Sonraki adımda kullanmak için Hello SDK yolunu not edin.</span><span class="sxs-lookup"><span data-stu-id="161ab-105">Note hello SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="161ab-106">Açık hello **build.gradle** hello uygulama dizinindeki dosyasını.</span><span class="sxs-lookup"><span data-stu-id="161ab-106">Open hello **build.gradle** file in hello app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="161ab-107">*Bağımlılıklar* ’ın altına bu satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="161ab-107">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="161ab-108">Merhaba tıklatın **projeyi Gradle dosyalarıyla Eşitle** hello araç çubuğunda simge.</span><span class="sxs-lookup"><span data-stu-id="161ab-108">Click hello **Sync Project with Gradle Files** icon in hello tool bar.</span></span>
6. <span data-ttu-id="161ab-109">Açık **AndroidManifest.xml** ve bu etiketi toohello ekleyin *uygulama* etiketi.</span><span class="sxs-lookup"><span data-stu-id="161ab-109">Open **AndroidManifest.xml** and add this tag toohello *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

