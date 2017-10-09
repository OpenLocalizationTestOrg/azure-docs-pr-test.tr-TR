
1. Merhaba tıklatın **uygulama hizmetleri** düğmesi, Mobile Apps arka ucunuz seçin, **Hızlı Başlangıç**ve ardından, istemci Platformu (iOS, Android, Xamarin, Cordova) seçin.

    ![Mobile Apps Hızlı Başlangıcın vurgulandığı Azure Portal][quickstart]

2. Bir veritabanı bağlantısı yapılandırılmamışsa, hello aşağıdakileri yaparak oluşturun:

    ![Azure portalı ile mobil uygulamaları bağlamak toodatabase][connect]

    a. Yeni bir SQL veritabanı ve sunucusu oluşturun.

    ![Mobile Apps ile Azure Portal, yeni veritabanı ve sunucu oluşturma][server]

    b. Merhaba veri bağlantısı başarıyla oluşturulana kadar bekleyin.

    ![Veri bağlantısının başarıyla oluşturulduğunu gösteren Azure Portal bildirimi][notification]

    c. Veri bağlantısının başarılı olması gerekir.

    ![Azure Portal bildirimi, "Bir veri bağlantınız zaten var"][already-connection]

3. **2. Tablo API'si oluştur**'un altında **Arka uç dili** olarak Node.js seçeneğini belirleyin. 
 
4. Merhaba bildirimi kabul edin ve ardından **Todoıtem tablosu oluştur**.  
    Böylece veritabanınızda yeni bir yapılacaklar tablosu oluşturulur. 

    >[!IMPORTANT]
    > Var olan bir arka uç tooNode.js geçiş tüm içeriğinin üzerine yazar. Bunun yerine, bir .NET arka uç bkz toocreate [hello .NET arka uç sunucusu SDK ile Mobile Apps için iş][instructions].

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png
[connect]: ./media/app-service-mobile-configure-new-backend/connect-to-bd.png
[notification]: ./media/app-service-mobile-configure-new-backend/notification-data-connection-create.png
[server]: ./media/app-service-mobile-configure-new-backend/create-new-server.png
[already-connection]: ./media/app-service-mobile-configure-new-backend/already-connection.png

<!-- URLs -->
[instructions]: ../articles/app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#create-app
