1. <span data-ttu-id="532f5-101">Android Studio’nun araç çubuğundaki simgeye tıklayarak ya da menüde **Araçlar** -> **Android** -> **SDK Manager** ’a tıklayarak Android SDK Manager’ı açın.</span><span class="sxs-lookup"><span data-stu-id="532f5-101">Open the Android SDK Manager by clicking the icon on the toolbar of Android Studio or by clicking **Tools** -> **Android** -> **SDK Manager** on the menu.</span></span> <span data-ttu-id="532f5-102">Projenizde kullanılan hedef Android SDK sürümünü bulup, **Paket Ayrıntılarını Göster** ’e tıklayarak bunu açın ve henüz yüklenmemişse **Google API'ler** ’i seçin.</span><span class="sxs-lookup"><span data-stu-id="532f5-102">Locate the target version of the Android SDK that is used in your project , open it by clicking **Show Package Details**, and choose **Google APIs**, if it is not already installed.</span></span>
2. <span data-ttu-id="532f5-103">**SDK Araçları** sekmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="532f5-103">Click the **SDK Tools** tab.</span></span> <span data-ttu-id="532f5-104">Google Play Hizmeti’ni zaten yüklemediyseniz **Google Play Hizmetleri** ’ne, aşağıda gösterildiği gibi tıklayın.</span><span class="sxs-lookup"><span data-stu-id="532f5-104">If you haven't already installed Google Play Service, click **Google Play Services** as shown below.</span></span> <span data-ttu-id="532f5-105">Ardından, yüklemek için **Uygula** ’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="532f5-105">Then click **Apply** to install.</span></span> 
   
    <span data-ttu-id="532f5-106">SDK yolunun sonraki bir adım için olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="532f5-106">Note the SDK path, for use in a later step.</span></span> 
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-sdk-manager.png)
3. <span data-ttu-id="532f5-107">Uygulama dizinindeki **build.gradle** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="532f5-107">Open the **build.gradle** file in the app directory.</span></span>
   
    ![](./media/notification-hubs-android-studio-add-google-play-services/notification-hubs-android-studio-add-google-play-dependency.png)
4. <span data-ttu-id="532f5-108">*Bağımlılıklar* ’ın altına bu satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="532f5-108">Add this line under *dependencies*:</span></span> 
   
           compile 'com.google.android.gms:play-services-gcm:9.2.0'
5. <span data-ttu-id="532f5-109">Araç çubuğundaki **Projeyi Gradle Dosyalarıyla Eşitle** simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="532f5-109">Click the **Sync Project with Gradle Files** icon in the tool bar.</span></span>
6. <span data-ttu-id="532f5-110">**AndroidManifest.xml** dosyasını açın ve bu etiketi *uygulama* etiketine ekleyin.</span><span class="sxs-lookup"><span data-stu-id="532f5-110">Open **AndroidManifest.xml** and add this tag to the *application* tag.</span></span>
   
        <meta-data android:name="com.google.android.gms.version"
            android:value="@integer/google_play_services_version" />

