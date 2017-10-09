### <a name="grant-access-tooyour-push-certificate-toomobile-engagement"></a>GRANT erişim tooyour anında sertifika tooMobile katılım
sizin adınıza tooallow Mobile Engagement toosend anında iletme bildirimleri, tooyour sertifika erişim toogrant gerekir. Bu, yapılandırarak ve sertifikanızı hello Mobile Engagement portalına girilerek gerçekleştirilir. [Apple belgeleri](https://developer.apple.com/library/prerelease/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html#//apple_ref/doc/uid/TP40012582-CH26-SW6)’nde açıklandığı gibi p12 sertifikanız olduğundan emin olun

1. Tooyour Mobile Engagement portalına gidin. Hello doğru olduğunuz ve üzerinde hello ardından olun **Katıl** hello altındaki düğmesi:
   
    ![](./media/mobile-engagement-ios-send-push/engage-button.png)
2. Tıklatın hello üzerinde **ayarları** Engagement portalınızın sayfası. Merhaba orada tıklayın **yerel gönderim** tooupload p12 sertifikanızı bölümünde:
   
    ![](./media/mobile-engagement-ios-send-push/engagement-portal.png)
3. p12 sertifikanızı seçin, bunu yükleyip parolanızı yazın:
   
    ![](./media/mobile-engagement-ios-send-push/native-push-settings.png)

## <a id="send"></a>Bir bildirim tooyour uygulaması Gönder
Şimdi bir itme tooour uygulaması gönderecek basit bir anında iletme bildirimi kampanyası oluşturacağız:

1. Toohello gidin **ulaşmak** Mobile Engagement portalınıza sekmesindedir.
2. Tıklatın **Yeni duyuru** toocreate anında iletme kampanyanızı
   
    ![](./media/mobile-engagement-ios-send-push/new-announcement.png)
3. Kampanyanızın ilk alanlarını Hello Kurulum:
   
    ![](./media/mobile-engagement-ios-send-push/campaign-first-params.png)
   
   * Kampanyanıza bir **Ad** verin 
   * Select hello **teslim saati** olarak **yalnızca uygulama dışında**: Bu, bazı metinleri hello basit Apple anında iletilen bildirim türüdür.
   * İlk hello Hello bildirim metni yazın **başlık** hello itme hello ilk satırı olacak.
   * Ardından, **ileti** hello ikinci satır olacak
4. Aşağı kaydırın ve içerik bölümü hello seçin **yalnızca bildirim**
   
    ![](./media/mobile-engagement-ios-send-push/campaign-content.png)
5. Merhaba en temel kampanya ayarını bitirdiniz. Şimdi aşağıya kayın ve tıklayın **oluşturma** toosave anında iletme bildirimi kampanyanızı düğmesine tıklayın. 
6. Son olarak - tıklayın **etkinleştirme** toosend anında iletme bildirimi. 
   
    ![](./media/mobile-engagement-ios-send-push/campaign-activate.png)
7. Size hello iOS Cihazınızda hello aşağıdaki gibi hello bildirim merkezi bildirimi:
   
    ![](./media/mobile-engagement-ios-send-push/iphone-notification.png)
8. Bu iOS cihazıyla eşleştirilmiş bir Apple Watch varsa, Apple Watch hello bildirim görürsünüz:
   
    ![](./media/mobile-engagement-ios-send-push/apple-watch.png)

