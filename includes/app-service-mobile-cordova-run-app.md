
1. [Azure portalını] ziyaret edin.
2. **Uygulama Hizmetleri**'ne ve oluşturduğunuz arka uca tıklayın.
3. Mobil uygulama ayarlarında, **Hızlı Başlangıç** > **Cordova** öğesine tıklayın.
![Mobile Apps Hızlı Başlangıcı'nın vurgulandığı Azure Portal][quickstart]
4. **İstemci uygulamanızı yapılandırın** altında **Yeni Uygulama Oluştur**’u seçin ve **İndir**’e tıklayın.
2. İndirilen ZIP dosyasını sabit sürücünüzde bir dizine çıkarın, çözüm dosyasına (.sln) gidin ve Visual Studio'yu kullanarak dosyayı açın.
3. Visual Studio'da başlatma okunun yanındaki açılır menüden çözüm platformunu (Android, iOS veya Windows) seçin. Yeşil ok üzerindeki açılır menüye tıklayarak belirli bir dağıtım cihazı veya öykünücüyü seçin. Varsayılan Android platformunu ve Ripple öykünücüsünü kullanabilirsiniz. Daha gelişmiş öğreticilerde (anında iletme bildirimleri gibi) desteklenen bir cihazı ve öykünücüyü seçmeniz istenecek.
4. Cordova uygulamanızı derlemek ve çalıştırmak için F5'e basın veya yeşil oka tıklayın. Öykünücüde ağa erişim isteyen bir güvenlik iletişim kutusu görürseniz erişim isteğini kabul edin.
5. Cihazda veya öykünücüde uygulama başlatıldıktan sonra, **Yeni metin gir** bölümüne *Öğreticiyi tamamla* gibi anlamlı bir metin girin ve **Ekle** düğmesine tıklayın.

Arka uç, istekten alınan verileri SQL Veritabanı'ndaki TodoItem tablosuna ekler ve yeni depolanan öğeler hakkındaki bilgileri de mobil uygulamaya geri döndürür. Mobil uygulama bu verileri listede görüntüler.

Diğer platformlar için 3 ile 5 arasındaki adımları tekrarlayabilirsiniz.

<!-- Images. -->
[quickstart]: ./media/app-service-mobile-configure-new-backend/quickstart.png

<!-- URLs -->
[Azure portalını]: https://portal.azure.com/
