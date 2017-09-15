

## <a name="generate-the-certificate-signing-request-file"></a><span data-ttu-id="78834-101">Sertifika İmzalama İsteği dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="78834-101">Generate the Certificate Signing Request file</span></span>
<span data-ttu-id="78834-102">Apple Anında İletilen Bildirim Servisi (APNS), anında iletme bildirimlerinizi doğrulamak için sertifikaları kullanır.</span><span class="sxs-lookup"><span data-stu-id="78834-102">The Apple Push Notification Service (APNS) uses certificates to authenticate your push notifications.</span></span> <span data-ttu-id="78834-103">Bildirim gönderip almak için gereken bildirim sertifikasını oluşturacak bu talimatları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="78834-103">Follow these instructions to create the necessary push certificate to send and receive notifications.</span></span> <span data-ttu-id="78834-104">Bu kavramlarla ilgili daha fazla bilgi için resmi [Apple Anında İletilen Bildirim Servisi](http://go.microsoft.com/fwlink/p/?LinkId=272584) belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="78834-104">For more information on these concepts see the official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="78834-105">İmzalı bir bildirim sertifikası oluşturmak için Apple tarafından kullanılan Sertifika İmzalama İsteği (CSR) dosyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="78834-105">Generate the Certificate Signing Request (CSR) file, which is used by Apple to generate a signed push certificate.</span></span>

1. <span data-ttu-id="78834-106">Mac’inizde Anahtar Zinciri Erişimi aracını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="78834-106">On your Mac, run the Keychain Access tool.</span></span> <span data-ttu-id="78834-107">**Yardımcı Programlar** klasöründen veya başlatma panelindeki **Diğer** klasöründen açılabilir.</span><span class="sxs-lookup"><span data-stu-id="78834-107">It can be opened from the **Utilities** folder or the **Other** folder on the launch pad.</span></span>
2. <span data-ttu-id="78834-108">**Anahtar Zinciri Erişimi**’ne tıklayın, **Sertifika Yardımcısı**’nı genişletin ve **Sertifika Yetkilisinden Sertifika İste...** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="78834-109">**Kullanıcı E-posta Adresi**’nizi ve **Ortak Ad**’ı seçin, **Diske kaydedilmiş**’in seçili olduğundan emin olun ve ardından **Devam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-109">Select your **User Email Address** and **Common Name** , make sure that **Saved to disk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="78834-110">Gerekmediğinden **CA E-posta Adresi**’ni boş bırakın.</span><span class="sxs-lookup"><span data-stu-id="78834-110">Leave the **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="78834-111">Sertifika İmzalama İsteği (CSR) dosyası için **Farklı Kaydet**’e bir ad yazın, **Nerede**’de konum seçin ve ardından **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-111">Type a name for the Certificate Signing Request (CSR) file in **Save As**, select the location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="78834-112">Böylece CSR dosyası istediğiniz konuma kaydedilir; varsayılan konum Masaüstü’dür.</span><span class="sxs-lookup"><span data-stu-id="78834-112">This saves the CSR file in the selected location; the default location is in the Desktop.</span></span> <span data-ttu-id="78834-113">Bu dosya için seçilen konumu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="78834-113">Remember the location chosen for this file.</span></span>

<span data-ttu-id="78834-114">Bundan sonra, uygulamanızı Apple’a kaydedeceksiniz; anında iletme bildirimini etkinleştirip bildirim sertifikası oluşturmak için dışarı aktarılan bu CSR dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="78834-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR to create a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="78834-115">Anında iletme bildirimleri için uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="78834-115">Register your app for push notifications</span></span>
<span data-ttu-id="78834-116">iOS uygulamasına anında iletme bildirimleri gönderebilmek için uygulamanızı Apple’a kaydetmenin yanı sıra anında iletme bildirimlerini de kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="78834-116">To be able to send push notifications to an iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="78834-117">Uygulamanızı henüz kaydetmediyseniz, Apple Geliştirici Merkezi’ndeki <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Sağlama Portalı</a>’na gidin, Apple kimliğinizle oturum açın, **Tanımlayıcılar**’a, **Uygulama kimlikleri**’ne ve son olarak da **+** işaretine tıklayarak yeni uygulamayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="78834-117">If you have not already registered your app, navigate to the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at the Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on the **+** sign to register a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="78834-118">Yeni uygulamanız için aşağıdaki üç alanı güncelleştirin ve ardından **Devam**’a tıklayın:</span><span class="sxs-lookup"><span data-stu-id="78834-118">Update the following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="78834-119">**Ad**: Uygulamanızı için **Uygulama Kimliği Açıklaması** bölümündeki **Ad** alanına açıklayıcı bir ad yazın.</span><span class="sxs-lookup"><span data-stu-id="78834-119">**Name**: Type a descriptive name for your app in the **Name** field in the **App ID Description** section.</span></span>
   * <span data-ttu-id="78834-120">**Paket Tanımlayıcı** : **Açık Uygulama Kimliği** bölümünün altında, **Paket Tanımlayıcı** öğesini `<Organization Identifier>.<Product Name>` biçiminde, [Uygulama Dağıtım Kılavuzu](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8)’nda söz edildiği gibi girin.</span><span class="sxs-lookup"><span data-stu-id="78834-120">**Bundle Identifier**: Under the **Explicit App ID** section, enter a **Bundle Identifier** in the form `<Organization Identifier>.<Product Name>` as mentioned in the [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="78834-121">*Kuruluş Tanımlayıcı* ve kullandığınız *Ürün Adı*, XCode projenizi oluşturduğunuzda kullanacağınız kuruluş tanımlayıcısı ve ürün adıyla eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="78834-121">The *Organization Identifier* and *Product Name* you use must match the organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="78834-122">Aşağıdaki ekran görüntüsünde *NotificationHubs* kuruluş tanımlayıcısı, *GetStarted* da ürün adı olarak kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="78834-122">In the screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as the product name.</span></span> <span data-ttu-id="78834-123">Bunun, XCode projenizde kullanacağınız değerlerle eşleştiğinden emin olunması XCode ile doğru yayımlama profili kullanmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="78834-123">Making sure this matches the values you will use in your XCode project will allow you to use the correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="78834-124">**Anında İletme Bildirimleri**: **Anında İletme Bildirimleri**’ni **Uygulama Hizmetleri** bölümünde denetleyin.</span><span class="sxs-lookup"><span data-stu-id="78834-124">**Push Notifications**: Check the **Push Notifications** option in the **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="78834-125">Böylece, Uygulama Kimliğiniz oluşturulur ve bilgiyi onaylamanız istenir.</span><span class="sxs-lookup"><span data-stu-id="78834-125">This generates your App ID and requests you to confirm the information.</span></span> <span data-ttu-id="78834-126">Yeni Uygulama Kimliğini onaylamak için **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-126">Click **Register** to confirm the new App ID.</span></span>
     
      <span data-ttu-id="78834-127">**Kaydet**’e tıkladıktan sonra **Kayıt tamamlandı** ekranını aşağıda gösterildiği gibi göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="78834-127">Once you click **Register**, you will see the **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="78834-128">**Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="78834-129">Geliştirici Merkezi’nde, Uygulama Kimlikleri altında henüz yeni oluşturmuş olduğunuz , uygulama kimliğini bulup satırına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-129">In the Developer Center, under App IDs, locate the app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="78834-130">Uygulama kimliğinin tıklatılması uygulama ayrıntılarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="78834-130">Clicking on the app ID will display the app details.</span></span> <span data-ttu-id="78834-131">Alttaki **Düzenle** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-131">Click the **Edit** button at the bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="78834-132">Ekranın altına gidin ve **Geliştirme bildirimi SSL Sertifikası** altındaki **sertifika Oluştur...** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-132">Scroll to the bottom of the screen, and click the **Create Certificate...** button under the section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="78834-133">"iOS Sertifikası Ekle" yardımcısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="78834-133">This displays the "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="78834-134">Bu öğretici geliştirme sertifikası kullanır.</span><span class="sxs-lookup"><span data-stu-id="78834-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="78834-135">Aynı işlem üretim sertifika kaydedildiğinde de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="78834-135">The same process is used when registering a production certificate.</span></span> <span data-ttu-id="78834-136">Bildirimleri gönderirken aynı sertifika türünü kullandığınızdan kesinlikle emin olun.</span><span class="sxs-lookup"><span data-stu-id="78834-136">Just make sure that you use the same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="78834-137">**Dosya Seç**’e tıklayın, ilk görevde oluşturduğunuz CSR dosyasını kaydettiğiniz konuma göz atın ve **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-137">Click **Choose File**, browse to the location where you saved the CSR file that you created in the first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="78834-138">Portal tarafından sertifika oluşturulduktan sonra **İndir** düğmesine ve **Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-138">After the certificate is created by the portal, click the **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="78834-139">Böylece sertifika indirilir ve bilgisayarınızın İndirmeler klasörüne kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="78834-139">This downloads the certificate and saves it to your computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="78834-140">Varsayılan olarak, indirilen geliştirme sertifikası dosyası **aps_development.cer** olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="78834-140">By default, the downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="78834-141">İndirilen **aps_development.cer** bildirim sertifikasına çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-141">Double-click the downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="78834-142">Yeni sertifika Anahtar Zinciri’ne aşağıda gösterildiği gibi yüklenir:</span><span class="sxs-lookup"><span data-stu-id="78834-142">This installs the new certificate in the Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="78834-143">Sertifikanızdaki ad farklı olabilir, ancak **Apple Geliştirme iOS Bildirim Hizmetleri:** ile önek alacaktır.</span><span class="sxs-lookup"><span data-stu-id="78834-143">The name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="78834-144">Anahtar Zinciri Erişimi’nde **Sertifikalar** kategorisinde oluşturduğunuz yeni bildirim sertifikasına sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-144">In Keychain Access, right-click the new push certificate that you created in the **Certificates** category.</span></span> <span data-ttu-id="78834-145">**Dışarı Aktar**’a tıklayın, dosyaya ad verin, **.p12** biçimini seçin ve **Kaydet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-145">Click **Export**, name the file, select the **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="78834-146">Dışarı aktarılan .p12 sertifikanın dosya adını ve konumunu not edin.</span><span class="sxs-lookup"><span data-stu-id="78834-146">Make a note of the file name and location of the exported .p12 certificate.</span></span> <span data-ttu-id="78834-147">APNS kimlik doğrulamasını etkinleştirmek için kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="78834-147">It will be used to enable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="78834-148">Bu öğretici bir QuickStart.p12 dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="78834-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="78834-149">Dosyanızın adı ve konumu farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="78834-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-the-app"></a><span data-ttu-id="78834-150">Uygulama için bir sağlama profili oluşturun</span><span class="sxs-lookup"><span data-stu-id="78834-150">Create a provisioning profile for the app</span></span>
1. <span data-ttu-id="78834-151"><a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Sağlama Portalı</a>’na geri dönün, **Sağlama Profilleri**’ni ve **Tümü**’nü seçin, ardından da yeni profil oluşturmak için **+** düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-151">Back in the <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click the **+** button to create a new profile.</span></span> <span data-ttu-id="78834-152">Böylece, **iOS Hazırlama Profili** Sihirbazı başlatılır</span><span class="sxs-lookup"><span data-stu-id="78834-152">This launches the **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="78834-153">**iOS Uygulaması Geliştirme**’yi, **Geliştirme** altında hazırlama profili türü olarak seçin ve **Devam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-153">Select **iOS App Development** under **Development** as the provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="78834-154">Daha sonra, az önce **Uygulama Kimliği** açılan listesinden oluşturduğunuz uygulama kimliğini seçin ve **Devam**’a tıklayın</span><span class="sxs-lookup"><span data-stu-id="78834-154">Next, select the app ID you just created from the **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="78834-155">**Sertifikaları Seç** ekranında, kod imzalama için kullanılan normal geliştirme sertifikanızı seçin ve **Devam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-155">In the **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="78834-156">Bu, yeni oluşturduğunuz bildirim sertifikası değildir.</span><span class="sxs-lookup"><span data-stu-id="78834-156">This is not the push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="78834-157">Sonra da, testte kullanmak üzere **Cihazlar**’a ve **Devam**’a tıklayın</span><span class="sxs-lookup"><span data-stu-id="78834-157">Next, select the **Devices** to use for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="78834-158">Son olarak, profil için **Profil Adı**’nda bir ad seçin, **Oluştur**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-158">Finally, pick a name for the profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="78834-159">Yeni sağlama profili oluşturulduğunda indirmek için buna tıklayın ve Xcode geliştirme makinesine yükleyin.</span><span class="sxs-lookup"><span data-stu-id="78834-159">When the new provisioning profile is created click to download it and install it on your Xcode development machine.</span></span> <span data-ttu-id="78834-160">Sonra da **Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78834-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
