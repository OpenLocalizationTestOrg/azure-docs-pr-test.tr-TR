

## <a name="generate-hello-certificate-signing-request-file"></a>Merhaba sertifika imzalama isteği dosyası oluşturma
Merhaba Apple anında bildirim hizmeti (APNS), anında iletme bildirimleri sertifikaları tooauthenticate kullanır. Bu yönergeler toocreate hello gereken bildirim sertifikasını toosend izleyin ve bildirimleri alabilirsiniz. Bu kavramlarla ilgili daha fazla bilgi için bkz: hello resmi [Apple anında iletilen bildirim servisi](http://go.microsoft.com/fwlink/p/?LinkId=272584) belgeleri.

Merhaba sertifika imzalama isteği (CSR) dosyasını oluşturmak Apple toogenerate tarafından imzalı bir bildirim sertifikası kullanılır.

1. Mac'inizde hello anahtar zinciri erişimi aracını çalıştırın. Hello açılabilir **yardımcı programları** klasör veya hello **diğer** hello başlatma panelindeki klasör.
2. **Anahtar Zinciri Erişimi**’ne tıklayın, **Sertifika Yardımcısı**’nı genişletin ve **Sertifika Yetkilisinden Sertifika İste...** öğesine tıklayın.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-request-cert-from-ca.png)
3. Seçin, **kullanıcı e-posta adresi** ve **ortak ad** , olduğundan emin olun **toodisk kaydedilen** seçilir ve ardından **devam**. Merhaba bırakın **CA e-posta adresi** alanı gerekli olmadığı boş.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-csr-info.png)
4. Hello sertifika imzalama isteği (CSR) dosyası için bir ad yazın **Kaydet**, seçin hello konumda **nerede**, ardından **kaydetmek**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-save-csr.png)
   
      Bu hello CSR dosyasını hello seçili konuma kaydeder; Merhaba Masaüstü Hello varsayılan konumdur. Bu dosya için seçilen hello konumu unutmayın.

Ardından, uygulamanızı Apple'a kaydedeceksiniz anında iletme bildirimlerini etkinleştirin ve dışarı aktarılan Bu CSR toocreate bildirim sertifikası karşıya.

## <a name="register-your-app-for-push-notifications"></a>Anında iletme bildirimleri için uygulamanızı kaydetme
toobe mümkün toosend anında iletme bildirimleri tooan iOS uygulaması, Apple ve aynı zamanda kayıt anında iletme bildirimleri için uygulamanızı kaydetmeniz gerekir.  

1. Uygulamanızı zaten kaydolmadıysanız toohello gidin <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS sağlama portalı</a> hello Apple Geliştirici Merkezi'ndeki, Apple kimliğinizle oturum açma tıklatın **tanımlayıcıları**, ardından **uygulama kimlikleri** ve son olarak hello üzerinde tıklatın  **+**  tooregister yeni bir uygulama oturum açın.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids.png)
      
2. Yeni uygulamanız için üç alanları izleyen hello güncelleştirin ve ardından **devam**:
   
   * **Ad**: hello uygulamanız için açıklayıcı bir ad yazın **adı** hello alanındaki **uygulama kimliği açıklaması** bölümü.
   * **Paket tanımlayıcı**: hello altında **açık uygulama kimliği** bölümünde, girin bir **paket tanımlayıcı** hello formunda `<Organization Identifier>.<Product Name>` hello belirtildiği gibi [uygulama dağıtımı Kılavuzu](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/ConfiguringYourApp/ConfiguringYourApp.html#//apple_ref/doc/uid/TP40012582-CH28-SW8). Merhaba *kuruluş tanımlayıcı* ve *ürün adı* gereken kullandığınız eşleşen hello kuruluş tanımlayıcısı ve ürün adı, XCode projenizi oluşturduğunuzda kullanacağınız. Aşağıdaki hello ekran görüntüsünde, *NotificationHubs* kuruluş tanımlayıcısı kullanılır ve *GetStarted* hello ürün adı olarak kullanılır. Bu, XCode projenizde kullanacağınız hello değerlerle eşleştiğinden emin olunması, toouse hello doğru yayımlama profili ile XCode izin verir. 
   * **Anında iletme bildirimleri**: onay hello **anında iletme bildirimleri** hello seçeneğinde **uygulama hizmetleri** bölümü.
     
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-appid-info.png)
     
      Bu, uygulama Kimliğiniz oluşturulur ve tooconfirm hello bilgi ister. Tıklatın **kaydetmek** tooconfirm hello yeni bir uygulama kimliği
     
      Tıkladığınızda **kaydetmek**, hello görürsünüz **kayıt işlemini tamamlamak** ekranını aşağıda gösterildiği gibi. **Bitti**’ye tıklayın.
      
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-registration-complete.png)


1. Merhaba Geliştirici Merkezi'nde, uygulama kimlikleri altında az önce oluşturduğunuz ve satırına tıklayın hello uygulama Kimliğini bulun.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-ios-appids2.png)
   
      Merhaba uygulama Kimliğinin tıklatılması hello uygulama ayrıntılarını görüntüler. Merhaba tıklatın **Düzenle** hello altındaki düğmesi.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-edit-appid.png)
      
2. Merhaba ekranın toohello'e gidin ve hello tıklatın **sertifika oluştur...**  düğmesi hello bölümü altında **geliştirme bildirimi SSL sertifikası**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-create-cert.png)
   
      Bu hello "iOS sertifikası Ekle" Yardımcısı görüntülenir.
   
   > [!NOTE]
   > Bu öğretici geliştirme sertifikası kullanır. Merhaba aynı işlem üretim sertifika kaydedildiğinde kullanılır. Yalnızca hello kullandığınızdan emin olun aynı sertifika türü Bildirimleri gönderirken.
   > 
   > 
3. Tıklatın **Dosya Seç**, hello ilk görevde oluşturduğunuz hello CSR dosyasını kaydettiğiniz toohello konumunu bulun ve ardından **Generate**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-cert-choose-csr.png)
4. Merhaba sertifika hello portal tarafından oluşturulduktan sonra hello tıklatın **karşıdan** düğmesine tıklayın ve **Bitti**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-appid-download-cert.png)
   
      Bu hello sertifika indirmeleri ve yüklemeleri klasörünüzdeki tooyour bilgisayar kaydeder.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-downloaded.png)
   
   > [!NOTE]
   > Varsayılan olarak, hello indirilen geliştirme sertifikası adlandırılan dosya **aps_development.cer**.
   > 
   > 
5. Merhaba indirilen sertifikasına çift tıklayın **aps_development.cer**.
   
      Bu hello yeni sertifika hello Anahtarlık, aşağıda gösterildiği gibi yüklenir:
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-cert-in-keychain.png)
   
   > [!NOTE]
   > Merhaba ad farklı olabilir, ancak ile önek alacaktır **Apple geliştirme iOS Bildirim Hizmetleri:**.
   > 
   > 
6. Anahtarlık erişimi'nde hello oluşturduğunuz hello yeni bildirim sertifikasına sağ tıklayın **sertifikaları** kategorisi. Tıklatın **verme**, hello dosya adı, seçin hello **.p12** biçimlendirmek ve ardından **kaydetmek**.
   
    ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-export-cert-p12.png)
   
    Merhaba dosya adını not ve hello dışarı aktarılan .p12 sertifikanın konumunu yapın. APNS ile kimlik doğrulaması kullanılan tooenable olacaktır.
   
   > [!NOTE]
   > Bu öğretici bir QuickStart.p12 dosyası oluşturur. Dosyanızın adı ve konumu farklı olabilir.
   > 
   > 

## <a name="create-a-provisioning-profile-for-hello-app"></a>Merhaba uygulama için bir sağlama profili oluşturun
1. Merhaba edilene <a href="http://go.microsoft.com/fwlink/p/?LinkId=272456" target="_blank">iOS sağlama portalı</a>seçin **sağlama profilleri**seçin **tüm**ve ardından hello  **+**  Düğme toocreate yeni bir profil. Bu hello başlatır **iOS hazırlama profili** Sihirbazı
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-new-provisioning-profile.png)
2. Seçin **iOS uygulaması geliştirme** altında **geliştirme** hello hazırlama profili türü ve tıklatın olarak **devam**. 
3. Ardından, yeni oluşturduğunuz hello hello uygulama Kimliğini seçin **uygulama kimliği** aşağı açılan liste ve tıklatın **devam et**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-select-appid-for-provisioning.png)
4. Merhaba, **sertifikaları Seç** ekranında, kod imzalama için kullanılan normal geliştirme sertifikanızı seçin ve tıklatın **devam**. Bu, yeni oluşturduğunuz hello bildirim sertifikası değildir.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-cert.png)
5. Ardından, hello'ı seçin **aygıtları** toouse test etme ve tıklatın **devam et**
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-select-devices.png)
6. Son olarak, hello profili için bir ad seçin **profil adı**, tıklatın **Generate**.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-name-profile.png)
7. Merhaba yeni sağlama profili oluşturulduğunda toodownload, yükleme tıklayın ve Xcode geliştirme makinenizde. Sonra da **Bitti**’ye tıklayın.
   
      ![](./media/notification-hubs-enable-apple-push-notifications/notification-hubs-provisioning-profile-ready.png)
