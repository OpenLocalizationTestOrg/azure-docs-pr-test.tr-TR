> [!IMPORTANT]
> tooreceive Mobile Engagement anında iletme bildirimleri, gereksinim duyduğunuz tooenable `Silent Remote Notifications` uygulamanızda. Info.plist dosyanızdaki tooadd hello uzaktan bildirim değeri toohello Uıbackgroundmodes dizisine gerekir.
> 
> 

1. Açık `info.plist` hello proje dosyasında
2. Merhaba listesindeki hello üst öğeyi sağ tıklayın (`Information Property List`) ve yeni satır Ekle
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push1.png)
3. Yeni satır Hello girin`Required background modes`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push2.png)
4. Merhaba sol ok tooexpand hello satırına tıklayın
5. Değer toohello öğeyi 0 izleyen hello ekleme`App downloads content in response toopush notifications`
   
    ![](./media/mobile-engagement-ios-silent-push/xcode-plist-add-silent-push3.png)
6. Merhaba değişiklik yaptıktan sonra XML aşağıdaki hello içermelidir hello info.plist anahtar ve değer:
   
        <key>UIBackgroundModes</key>
        <array>
        <string>remote-notification</string>
        </array>
7. **Xcode 7 +** ve **iOS 9 +** kullanıyorsanız:
   
   * **Anında İletme Bildirimleri**’ni Hedefler > Hedef Adınız > Özellikler’de etkinleştirin.

