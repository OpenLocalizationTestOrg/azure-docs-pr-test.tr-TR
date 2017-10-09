### <a name="grant-mobile-engagement-access-tooyour-gcm-api-key"></a>GRANT Mobile Engagement erişimi tooyour GCM API anahtarı
tooallow Mobile Engagement toosend anında iletme bildirimleri sizin adınıza tooyour API anahtarı erişim toogrant gerekir. Bu, yapılandırarak ve anahtarınızı hello Mobile Engagement portalına girilerek gerçekleştirilir.

1. Biz bu proje için kullanmakta olduğunuz ve hello ardından hello uygulamada olduğunuzdan, Azure Klasik portalından olun **Katıl** hello altındaki düğmesi:
   
    ![](./media/mobile-engagement-android-send-push/engage-button.png)
2. Merhaba ardından **ayarları** -> **yerel gönderim** tooenter GCM anahtarınızı bölümünde:
   
    ![](./media/mobile-engagement-android-send-push/engagement-portal.png)
3. Merhaba tıklatın **Düzenle** önüne simgesi **API anahtarı** hello içinde **GCM ayarları** bölümünde aşağıda gösterildiği gibi:
   
    ![](./media/mobile-engagement-android-send-push/native-push-settings.png)
4. Merhaba açılır hello önce aldığınız GCM Server anahtarını yapıştırın ve ardından **Tamam**.
   
    ![](./media/mobile-engagement-android-send-push/api-key.png)

## <a id="send"></a>Bir bildirim tooyour uygulaması Gönder
Şimdi bir anında iletme bildirimi tooour uygulaması gönderir basit anında iletme bildirimi kampanyası oluşturacağız.

1. Toohello gidin **ULAŞMAK** Mobile Engagement portalınıza sekmesindedir.
2. Tıklatın **Yeni duyuru** toocreate anında iletme bildirimi kampanyanızı.
   
    ![](./media/mobile-engagement-android-send-push/new-announcement.png)
3. Aşağıdaki adımları hello kampanyanızın ilk alan hello ayarlayın:
   
    ![](./media/mobile-engagement-android-send-push/campaign-first-params.png)
   
    a. Kampanyanızı adlandırın.
   
    b. Select hello **teslimat türü** olarak *sistem bildirimi -> basit*: bir başlık ve küçük bir metin satırının özellikleri hello basit Android anında iletme bildirimi türü budur.
   
    c. Seçin **teslim saati** olarak *dilediğiniz zaman* hello uygulama veya başlatılıp başlatılmadığını tooallow hello uygulama tooreceive bir bildirim.
   
    d. Merhaba bildirim metin türü hello içinde **başlık** olacak hello itme kalın.
   
    e. Ardından, **İleti**’yi yazın.
4. Kaydırma aşağı ve hello **içerik** bölümünde, select **yalnızca bildirim**.
   
    ![](./media/mobile-engagement-android-send-push/campaign-content.png)
5. Ayar hello en temel kampanya olası bitirdiniz. Şimdi kaydırarak yeniden aşağı gidin ve hello tıklatın **oluşturma** toosave kampanyanızı düğmesine tıklayın.
6. Son adım: tıklatın **etkinleştirme** tooactivate kampanya toosend anında iletme bildirimleri.
   
    ![](./media/mobile-engagement-android-send-push/campaign-activate.png)

