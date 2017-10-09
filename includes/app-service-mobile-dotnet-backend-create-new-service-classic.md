1. Merhaba oturum açma [Azure Portal].
2. **+YENİ** > **Web + Mobil** > **Mobil Uygulama**’ya tıklayıp Mobile Uygulama arka ucu için bir ad verin.
3. Hello için **kaynak grubu**, varolan bir kaynak grubu seçin veya yeni bir tane oluşturun (kullanarak Merhaba, uygulamanızın adıyla aynı.) 
   
    Başka bir App Service planı seçin veya yeni bir tane oluşturun. Uygulama Hizmetleri planları ve nasıl toocreate farklı fiyatlandırma içinde yeni bir plan katmanı ve tercih ettiğiniz konumda bkz hakkında daha fazla bilgi için [Azure App Service planlarına ayrıntılı genel bakış](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).
4. Hello için **uygulama hizmeti planı**, hello varsayılan plan (Merhaba içinde [standart katmanı](https://azure.microsoft.com/pricing/details/app-service/)) seçilidir. Ayrıca, farklı bir plan seçebilirsiniz veya [yeni bir tane oluşturun](../articles/app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md#create-an-app-service-plan). Merhaba uygulama hizmeti planının ayarları belirlemek hello [konumu, özellikleri, maliyeti ve işlem kaynaklarını](https://azure.microsoft.com/pricing/details/app-service/) uygulamanızla ilişkili. 
   
    Merhaba planla ilgili kararı verdikten sonra tıklayın **oluşturma**. Merhaba mobil uygulama arka ucu oluşturur. 
5. Merhaba, **ayarları** hello yeni mobil uygulama arka ucu, dikey tıklayın **Hızlı Başlangıç** > istemci uygulaması platformunuz > **bir veritabanına bağlanmak**. 
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-data-connection.png)
6. Merhaba, **veri bağlantısı Ekle** dikey penceresinde tıklatın **SQL veritabanı** > **yeni bir veritabanı oluşturmak**, türü hello veritabanı **adı**, bir fiyatlandırma katmanı seçin ve ardından **Server**.  Bu yeni veritabanını yeniden kullanabilirsiniz. Hello bir veritabanı zaten varsa, aynı konumda, bunun yerine seçebilirsiniz **varolan veritabanını kullan**. bir veritabanı farklı bir konumda Hello kullanımını toobandwidth maliyetleri ve daha yüksek gecikme önerilmez.
   
    ![](./media/app-service-mobile-dotnet-backend-create-new-service/dotnet-backend-create-db.png)
7. Merhaba, **yeni sunucu** dikey penceresinde hello benzersiz sunucu adını yazın **sunucu adı** alanında, bir oturum açma ve parola, denetleme sağlayın **izin azure Hizmetleri tooaccess sunucusu**ve'ı tıklatın **Tamam**. Merhaba yeni bir veritabanı oluşturur.
8. Merhaba edilene **veri bağlantısı Ekle** dikey penceresinde tıklatın **bağlantı dizesi**, veritabanınızı hello oturum açma ve parola değerlerini yazın ve'ı tıklatın **Tamam**. Devam etmeden önce başarıyla dağıtılan hello veritabanı toobe birkaç dakika bekleyin.

<!-- URLs. -->
[Azure Portal]: https://portal.azure.com/
