#### <a name="configure-hello-ios-project-in-xamarin-studio"></a>Xamarin Studio'da Hello iOS projesi yapılandırın
1. Xamarin.Studio içinde açmak **Info.plist**ve güncelleştirme hello **paket tanımlayıcısı** yeni uygulama kimliğiniz ile daha önce oluşturduğunuz kimliği ile Merhaba paketini

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-21.png)
2. Çok ilerleyin**arka plan modları**. Select hello **arka plan modlarını etkinleştir** kutusu ve hello **uzak bildirimler** kutusu.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-22.png)
3. Merhaba çözüm paneli tooopen projenizde çift **proje seçenekleri**.
4. Altında **yapı**, seçin **iOS paket imzalama**, select hello karşılık gelen kimliği ve sağlama profiliniz, yalnızca bu proje için ayarlanmış.

   ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-20.png)

   Bu kod imzalama için hello proje hello yeni profili kullanan sağlar. Belge hello resmi Xamarin cihaz sağlama için bkz: [Xamarin cihaz sağlamayı].

#### <a name="configure-hello-ios-project-in-visual-studio"></a>Visual Studio'da Hello iOS projesi yapılandırın
1. Visual Studio'da hello projesine sağ tıklayın ve ardından **özellikleri**.
2. Merhaba özellikler sayfalarında hello tıklatın **iOS uygulama** sekmesi ve güncelleştirme hello **tanımlayıcısı** daha önce oluşturduğunuz hello Kimliğine sahip.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-23.png)
3. Merhaba, **iOS paket imzalama** sekmesinde, select hello karşılık gelen kimliği ve sağlama profili, ayarladığınız yukarı bu proje için.

    ![](./media/app-service-mobile-xamarin-ios-configure-project/mobile-services-ios-push-24.png)

    Bu kod imzalama için hello proje hello yeni profili kullanan sağlar. Belge hello resmi Xamarin cihaz sağlama için bkz: [Xamarin cihaz sağlamayı].
4. Info.plist tooopen çift tıklayın ve ardından Etkinleştir **RemoteNotifications** altında **arka plan modları**.

[Xamarin cihaz sağlamayı]: http://developer.xamarin.com/guides/ios/getting_started/installation/device_provisioning/
