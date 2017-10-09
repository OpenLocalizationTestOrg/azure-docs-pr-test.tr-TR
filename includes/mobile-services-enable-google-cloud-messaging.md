
1. Toohello gidin [Google Cloud Console](https://console.developers.google.com/project), Google hesabı kimlik bilgilerinizle oturum açın. 
2. **Proje Oluştur**’a tıklayıp bir proje adı yazın ve sonra **Oluştur**’a tıklayın. İstenirse, SMS doğrulamasını hello taşımak ve tıklatın **oluşturma** yeniden.
   
    ![Yeni proje oluşturma](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-new-project.png)   
   
     Yeni **Proje adı**’nızı yazıp **Proje oluştur**’a tıklayın.
3. Merhaba tıklatın **yardımcı programlar ve diğerleri** düğmesine tıklayın ve ardından **proje bilgileri**. Merhaba Not **proje numarası**. Bu değer hello olarak tooset gerekir `SenderId` hello istemci uygulamasında değişken.
   
    ![Yardımcı programlar ve daha fazlası](./media/mobile-services-enable-google-cloud-messaging/notification-hubs-utilities-and-more.png)
4. Hello panoyu altında proje **mobil API'leri**, tıklatın **Google Cloud Messaging**, hello sonraki sayfada'ye tıklayın **API etkinleştir** ve hizmet hello koşullarını kabul edin. 
   
    ![GCM etkinleştirme](./media/mobile-services-enable-google-cloud-messaging/enable-GCM.png)
   
    ![GCM etkinleştirme](./media/mobile-services-enable-google-cloud-messaging/enable-gcm-2.png) 
5. Merhaba proje panosunda tıklatın **kimlik bilgileri** > **kimlik bilgisi Oluştur** > **API anahtarı**. 
   
    ![](./media/mobile-services-enable-google-cloud-messaging/mobile-services-google-create-server-key.png)
6. **Yeni anahtar oluştur**’da **Sunucu anahtarı**’na tıklayın, anahtarınız için bir ad yazın ve **Oluştur**’a tıklayın.
7. Merhaba Not **API anahtarı** değeri.
   
    Bu API anahtar değeri tooenable Azure tooauthenticate GCM ile birlikte kullanabilir ve uygulamanız adına anında iletme bildirimleri göndermek.

