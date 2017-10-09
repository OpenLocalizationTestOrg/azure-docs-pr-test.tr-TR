

## <a name="generate-hello-certificate-signing-request-file"></a><span data-ttu-id="fbe37-101">Merhaba sertifika imzalama isteği dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="fbe37-101">Generate hello Certificate Signing Request file</span></span>
<span data-ttu-id="fbe37-102">Merhaba Apple anında bildirim hizmeti (APNS), anında iletme bildirimleri sertifikaları tooauthenticate kullanır.</span><span class="sxs-lookup"><span data-stu-id="fbe37-102">hello Apple Push Notification Service (APNS) uses certificates tooauthenticate your push notifications.</span></span> <span data-ttu-id="fbe37-103">Bu yönergeler toocreate hello gereken bildirim sertifikasını toosend izleyin ve bildirimleri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fbe37-103">Follow these instructions toocreate hello necessary push certificate toosend and receive notifications.</span></span> <span data-ttu-id="fbe37-104">Bu kavramlarla ilgili daha fazla bilgi için bkz: hello resmi [Apple anında iletilen bildirim servisi](http://go.microsoft.com/fwlink/p/?LinkId=272584) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="fbe37-104">For more information on these concepts see hello official [Apple Push Notification Service](http://go.microsoft.com/fwlink/p/?LinkId=272584) documentation.</span></span>

<span data-ttu-id="fbe37-105">Merhaba sertifika imzalama isteği (CSR) dosyasını oluşturmak Apple toogenerate tarafından imzalı bir bildirim sertifikası kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fbe37-105">Generate hello Certificate Signing Request (CSR) file, which is used by Apple toogenerate a signed push certificate.</span></span>

1. <span data-ttu-id="fbe37-106">Mac'inizde hello anahtar zinciri erişimi aracını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fbe37-106">On your Mac, run hello Keychain Access tool.</span></span> <span data-ttu-id="fbe37-107">Hello açılabilir **yardımcı programları** klasör veya hello **diğer** hello başlatma panelindeki klasör.</span><span class="sxs-lookup"><span data-stu-id="fbe37-107">It can be opened from hello **Utilities** folder or hello **Other** folder on hello launch pad.</span></span>
2. <span data-ttu-id="fbe37-108">**Anahtar Zinciri Erişimi**’ne tıklayın, **Sertifika Yardımcısı**’nı genişletin ve **Sertifika Yetkilisinden Sertifika İste...** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbe37-108">Click **Keychain Access**, expand **Certificate Assistant**, then click **Request a Certificate from a Certificate Authority...**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. <span data-ttu-id="fbe37-109">Seçin, **kullanıcı e-posta adresi** ve **ortak ad** , olduğundan emin olun **toodisk kaydedilen** seçilir ve ardından **devam**.</span><span class="sxs-lookup"><span data-stu-id="fbe37-109">Select your **User Email Address** and **Common Name** , make sure that **Saved toodisk** is selected, and then click **Continue**.</span></span> <span data-ttu-id="fbe37-110">Merhaba bırakın **CA e-posta adresi** alanı gerekli olmadığı boş.</span><span class="sxs-lookup"><span data-stu-id="fbe37-110">Leave hello **CA Email Address** field blank as it is not required.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. <span data-ttu-id="fbe37-111">Hello sertifika imzalama isteği (CSR) dosyası için bir ad yazın **Kaydet**, seçin hello konumda **nerede**, ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="fbe37-111">Type a name for hello Certificate Signing Request (CSR) file in **Save As**, select hello location in **Where**, then click **Save**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      <span data-ttu-id="fbe37-112">Bu hello CSR dosyasını hello seçili konuma kaydeder; Merhaba Masaüstü Hello varsayılan konumdur.</span><span class="sxs-lookup"><span data-stu-id="fbe37-112">This saves hello CSR file in hello selected location; hello default location is in hello Desktop.</span></span> <span data-ttu-id="fbe37-113">Bu dosya için seçilen hello konumu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fbe37-113">Remember hello location chosen for this file.</span></span>

<span data-ttu-id="fbe37-114">Ardından, uygulamanızı Apple'a kaydedeceksiniz anında iletme bildirimlerini etkinleştirin ve dışarı aktarılan Bu CSR toocreate bildirim sertifikası karşıya.</span><span class="sxs-lookup"><span data-stu-id="fbe37-114">Next, you will register your app with Apple, enable push notifications, and upload this exported CSR toocreate a push certificate.</span></span>

## <a name="register-your-app-for-push-notifications"></a><span data-ttu-id="fbe37-115">Anında iletme bildirimleri için uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="fbe37-115">Register your app for push notifications</span></span>
<span data-ttu-id="fbe37-116">toobe mümkün toosend anında iletme bildirimleri tooan iOS uygulaması, Apple ve aynı zamanda kayıt anında iletme bildirimleri için uygulamanızı kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fbe37-116">toobe able toosend push notifications tooan iOS app, you must register your application with Apple and also register for push notifications.</span></span>  

1. <span data-ttu-id="fbe37-117">Uygulamanızı zaten kaydolmadıysanız toohello gidin <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS sağlama portalı</a> hello Apple Geliştirici Merkezi'ndeki, Apple kimliğinizle oturum açma tıklatın **tanımlayıcıları**, ardından **uygulama kimlikleri** ve son olarak hello üzerinde tıklatın  **+**  tooregister yeni bir uygulama oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fbe37-117">If you have not already registered your app, navigate toohello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a> at hello Apple Developer Center, log on with your Apple ID, click **Identifiers**, then click **App IDs**, and finally click on hello **+** sign tooregister a new app.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. <span data-ttu-id="fbe37-118">Yeni uygulamanız için üç alanları izleyen hello güncelleştirin ve ardından **devam**:</span><span class="sxs-lookup"><span data-stu-id="fbe37-118">Update hello following three fields for your new app and then click **Continue**:</span></span>
   
   * <span data-ttu-id="fbe37-119">**Ad**: hello uygulamanız için açıklayıcı bir ad yazın **adı** hello alanındaki **uygulama kimliği açıklaması** bölümü.</span><span class="sxs-lookup"><span data-stu-id="fbe37-119">**Name**: Type a descriptive name for your app in hello **Name** field in hello **App ID Description** section.</span></span>
   * <span data-ttu-id="fbe37-120">**Paket tanımlayıcı**: hello altında **açık uygulama kimliği** bölümünde, girin bir **paket tanımlayıcı** hello formunda `<Organization Identifier>.<Product Name>` hello belirtildiği gibi [uygulama dağıtımı Kılavuzu](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span><span class="sxs-lookup"><span data-stu-id="fbe37-120">**Bundle Identifier**: Under hello **Explicit App ID** section, enter a **Bundle Identifier** in hello form `<Organization Identifier>.<Product Name>` as mentioned in hello [App Distribution Guide](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8).</span></span> <span data-ttu-id="fbe37-121">Merhaba *kuruluş tanımlayıcı* ve *ürün adı* gereken kullandığınız eşleşen hello kuruluş tanımlayıcısı ve ürün adı, XCode projenizi oluşturduğunuzda kullanacağınız.</span><span class="sxs-lookup"><span data-stu-id="fbe37-121">hello *Organization Identifier* and *Product Name* you use must match hello organization identifier and product name you will use when you create your XCode project.</span></span> <span data-ttu-id="fbe37-122">Aşağıdaki hello ekran görüntüsünde, *NotificationHubs* kuruluş tanımlayıcısı kullanılır ve *GetStarted* hello ürün adı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fbe37-122">In hello screeshot below *NotificationHubs* is used as a organization idenitifier and *GetStarted* is used as hello product name.</span></span> <span data-ttu-id="fbe37-123">Bu, XCode projenizde kullanacağınız hello değerlerle eşleştiğinden emin olunması, toouse hello doğru yayımlama profili ile XCode izin verir.</span><span class="sxs-lookup"><span data-stu-id="fbe37-123">Making sure this matches hello values you will use in your XCode project will allow you toouse hello correct publishing profile with XCode.</span></span> 
   * <span data-ttu-id="fbe37-124">**Anında iletme bildirimleri**: onay hello **anında iletme bildirimleri** hello seçeneğinde **uygulama hizmetleri** bölümü.</span><span class="sxs-lookup"><span data-stu-id="fbe37-124">**Push Notifications**: Check hello **Push Notifications** option in hello **App Services** section, .</span></span>
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      <span data-ttu-id="fbe37-125">Bu, uygulama Kimliğiniz oluşturulur ve tooconfirm hello bilgi ister.</span><span class="sxs-lookup"><span data-stu-id="fbe37-125">This generates your App ID and requests you tooconfirm hello information.</span></span> <span data-ttu-id="fbe37-126">Tıklatın **kaydetmek** tooconfirm hello yeni bir uygulama kimliği</span><span class="sxs-lookup"><span data-stu-id="fbe37-126">Click **Register** tooconfirm hello new App ID.</span></span>
     
      <span data-ttu-id="fbe37-127">Tıkladığınızda **kaydetmek**, hello görürsünüz **kayıt işlemini tamamlamak** ekranını aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="fbe37-127">Once you click **Register**, you will see hello **Registration complete** screen, as shown below.</span></span> <span data-ttu-id="fbe37-128">**Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbe37-128">Click **Done**.</span></span>
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. <span data-ttu-id="fbe37-129">Merhaba Geliştirici Merkezi'nde, uygulama kimlikleri altında az önce oluşturduğunuz ve satırına tıklayın hello uygulama Kimliğini bulun.</span><span class="sxs-lookup"><span data-stu-id="fbe37-129">In hello Developer Center, under App IDs, locate hello app ID that you just created, and click on its row.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      <span data-ttu-id="fbe37-130">Merhaba uygulama Kimliğinin tıklatılması hello uygulama ayrıntılarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="fbe37-130">Clicking on hello app ID will display hello app details.</span></span> <span data-ttu-id="fbe37-131">Merhaba tıklatın **Düzenle** hello altındaki düğmesi.</span><span class="sxs-lookup"><span data-stu-id="fbe37-131">Click hello **Edit** button at hello bottom.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. <span data-ttu-id="fbe37-132">Merhaba ekranın toohello'e gidin ve hello tıklatın **sertifika oluştur...**  düğmesi hello bölümü altında **geliştirme bildirimi SSL sertifikası**.</span><span class="sxs-lookup"><span data-stu-id="fbe37-132">Scroll toohello bottom of hello screen, and click hello **Create Certificate...** button under hello section **Development Push SSL Certificate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      <span data-ttu-id="fbe37-133">Bu hello "iOS sertifikası Ekle" Yardımcısı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="fbe37-133">This displays hello "Add iOS Certificate" assistant.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fbe37-134">Bu öğretici geliştirme sertifikası kullanır.</span><span class="sxs-lookup"><span data-stu-id="fbe37-134">This tutorial uses a development certificate.</span></span> <span data-ttu-id="fbe37-135">Merhaba aynı işlem üretim sertifika kaydedildiğinde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fbe37-135">hello same process is used when registering a production certificate.</span></span> <span data-ttu-id="fbe37-136">Yalnızca hello kullandığınızdan emin olun aynı sertifika türü Bildirimleri gönderirken.</span><span class="sxs-lookup"><span data-stu-id="fbe37-136">Just make sure that you use hello same certificate type when sending notifications.</span></span>
   > 
   > 
3. <span data-ttu-id="fbe37-137">Tıklatın **Dosya Seç**, hello ilk görevde oluşturduğunuz hello CSR dosyasını kaydettiğiniz toohello konumunu bulun ve ardından **Generate**.</span><span class="sxs-lookup"><span data-stu-id="fbe37-137">Click **Choose File**, browse toohello location where you saved hello CSR file that you created in hello first task, then click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. <span data-ttu-id="fbe37-138">Merhaba sertifika hello portal tarafından oluşturulduktan sonra hello tıklatın **karşıdan** düğmesine tıklayın ve **Bitti**.</span><span class="sxs-lookup"><span data-stu-id="fbe37-138">After hello certificate is created by hello portal, click hello **Download** button, and click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      <span data-ttu-id="fbe37-139">Bu hello sertifika indirmeleri ve yüklemeleri klasörünüzdeki tooyour bilgisayar kaydeder.</span><span class="sxs-lookup"><span data-stu-id="fbe37-139">This downloads hello certificate and saves it tooyour computer in your Downloads folder.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > <span data-ttu-id="fbe37-140">Varsayılan olarak, hello indirilen geliştirme sertifikası adlandırılan dosya **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="fbe37-140">By default, hello downloaded file a development certificate is named **aps_development.cer**.</span></span>
   > 
   > 
5. <span data-ttu-id="fbe37-141">Merhaba indirilen sertifikasına çift tıklayın **aps_development.cer**.</span><span class="sxs-lookup"><span data-stu-id="fbe37-141">Double-click hello downloaded push certificate **aps_development.cer**.</span></span>
   
      <span data-ttu-id="fbe37-142">Bu hello yeni sertifika hello Anahtarlık, aşağıda gösterildiği gibi yüklenir:</span><span class="sxs-lookup"><span data-stu-id="fbe37-142">This installs hello new certificate in hello Keychain, as shown below:</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > <span data-ttu-id="fbe37-143">Merhaba ad farklı olabilir, ancak ile önek alacaktır **Apple geliştirme iOS Bildirim Hizmetleri:**.</span><span class="sxs-lookup"><span data-stu-id="fbe37-143">hello name in your certificate might be different, but it will be prefixed with **Apple Development iOS Push Services:**.</span></span>
   > 
   > 
6. <span data-ttu-id="fbe37-144">Anahtarlık erişimi'nde hello oluşturduğunuz hello yeni bildirim sertifikasına sağ tıklayın **sertifikaları** kategorisi.</span><span class="sxs-lookup"><span data-stu-id="fbe37-144">In Keychain Access, right-click hello new push certificate that you created in hello **Certificates** category.</span></span> <span data-ttu-id="fbe37-145">Tıklatın **verme**, hello dosya adı, seçin hello **.p12** biçimlendirmek ve ardından **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="fbe37-145">Click **Export**, name hello file, select hello **.p12** format, and then click **Save**.</span></span>
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    <span data-ttu-id="fbe37-146">Merhaba dosya adını not ve hello dışarı aktarılan .p12 sertifikanın konumunu yapın.</span><span class="sxs-lookup"><span data-stu-id="fbe37-146">Make a note of hello file name and location of hello exported .p12 certificate.</span></span> <span data-ttu-id="fbe37-147">APNS ile kimlik doğrulaması kullanılan tooenable olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fbe37-147">It will be used tooenable authentication with APNS.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="fbe37-148">Bu öğretici bir QuickStart.p12 dosyası oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fbe37-148">This tutorial creates a QuickStart.p12 file.</span></span> <span data-ttu-id="fbe37-149">Dosyanızın adı ve konumu farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="fbe37-149">Your file name and location might be different.</span></span>
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a><span data-ttu-id="fbe37-150">Merhaba uygulama için bir sağlama profili oluşturun</span><span class="sxs-lookup"><span data-stu-id="fbe37-150">Create a provisioning profile for hello app</span></span>
1. <span data-ttu-id="fbe37-151">Merhaba edilene <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS sağlama portalı</a>seçin **sağlama profilleri**seçin **tüm**ve ardından hello  **+**  Düğme toocreate yeni bir profil.</span><span class="sxs-lookup"><span data-stu-id="fbe37-151">Back in hello <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS Provisioning Portal</a>, select **Provisioning Profiles**, select **All**, and then click hello **+** button toocreate a new profile.</span></span> <span data-ttu-id="fbe37-152">Bu hello başlatır **iOS hazırlama profili** Sihirbazı</span><span class="sxs-lookup"><span data-stu-id="fbe37-152">This launches hello **Add iOS Provisiong Profile** Wizard</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. <span data-ttu-id="fbe37-153">Seçin **iOS uygulaması geliştirme** altında **geliştirme** hello hazırlama profili türü ve tıklatın olarak **devam**.</span><span class="sxs-lookup"><span data-stu-id="fbe37-153">Select **iOS App Development** under **Development** as hello provisiong profile type, and click **Continue**.</span></span> 
3. <span data-ttu-id="fbe37-154">Ardından, yeni oluşturduğunuz hello hello uygulama Kimliğini seçin **uygulama kimliği** aşağı açılan liste ve tıklatın **devam et**</span><span class="sxs-lookup"><span data-stu-id="fbe37-154">Next, select hello app ID you just created from hello **App ID** drop-down list, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. <span data-ttu-id="fbe37-155">Merhaba, **sertifikaları Seç** ekranında, kod imzalama için kullanılan normal geliştirme sertifikanızı seçin ve tıklatın **devam**.</span><span class="sxs-lookup"><span data-stu-id="fbe37-155">In hello **Select certificates** screen, select your usual development certificate used for code signing, and click **Continue**.</span></span> <span data-ttu-id="fbe37-156">Bu, yeni oluşturduğunuz hello bildirim sertifikası değildir.</span><span class="sxs-lookup"><span data-stu-id="fbe37-156">This is not hello push certificate you just created.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. <span data-ttu-id="fbe37-157">Ardından, hello'ı seçin **aygıtları** toouse test etme ve tıklatın **devam et**</span><span class="sxs-lookup"><span data-stu-id="fbe37-157">Next, select hello **Devices** toouse for testing, and click **Continue**</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. <span data-ttu-id="fbe37-158">Son olarak, hello profili için bir ad seçin **profil adı**, tıklatın **Generate**.</span><span class="sxs-lookup"><span data-stu-id="fbe37-158">Finally, pick a name for hello profile in **Profile Name**, click **Generate**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. <span data-ttu-id="fbe37-159">Merhaba yeni sağlama profili oluşturulduğunda toodownload, yükleme tıklayın ve Xcode geliştirme makinenizde.</span><span class="sxs-lookup"><span data-stu-id="fbe37-159">When hello new provisioning profile is created click toodownload it and install it on your Xcode development machine.</span></span> <span data-ttu-id="fbe37-160">Sonra da **Bitti**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fbe37-160">Then click **Done**.</span></span>
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
