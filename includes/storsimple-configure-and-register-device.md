<!--author=alkohli last changed: 12/01/15-->


#### <a name="tooconfigure-and-register-hello-device"></a>Merhaba aygıt tooconfigure ve kaydetme
1. StorSimple cihaz seri konsoluna Hello Windows PowerShell arabirimine erişin. Bkz: [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](#use-putty-to-connect-to-the-device-serial-console) yönergeler için. **Emin toofollow hello yordamı tamamen olması veya mümkün tooaccess hello konsol olmaz.**
2. Açılan hello oturumunda Enter bir zaman tooget bir komut istemi tuşuna basın. 
3. Cihazınız için tooset istediğiniz istendiğinde toochoose hello dil olacaktır. Merhaba dili belirtin ve ardından Enter tuşuna basın. 
   
    ![StorSimple cihazı yapılandırma ve kaydetme 1](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice1-include.png)
4. Sunulan hello seri konsol menüsünde seçeneği 1 toolog tam erişimle seçin. 
   
    ![StorSimple kayıt cihazı 2](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice2-include.png)
   
     Adım 5-12 tooconfigure hello minimum gerekli ağ ayarlarını, cihazınız için tamamlayın. **Bu yapılandırma adımları hello etkin hello aygıt denetleyicisinde gerçekleştirilen toobe gerekir.** Merhaba seri konsol menüsünde hello başlık iletisi hello denetleyicisi durumunu gösterir. Değil bağlıysanız toohello active denetleyicisi kesin ve toohello etkin denetleyicisi bağlayın.
5. Merhaba komut istemine parolanızı yazın. Merhaba varsayılan cihaz parolası **Parola1**.
6. Merhaba aşağıdaki komutu yazın:
   
     `Invoke-HcsSetupWizard` 
7. Kurulum Sihirbazı'nı hello cihaz için hello ağ ayarlarını yapılandırmak toohelp görünür. Aşağıdaki bilgilerle hello hello sağlayın: 
   
   * Merhaba veri 0 ağ arabirimi için IP adresi
   * Alt ağ maskesi
   * Ağ geçidi
   * Birincil DNS sunucusu için IP adresi
   * Birincil NTP sunucusu için IP adresi
     
     > [!NOTE]
     > Birkaç dakika boyunca hello alt ağ maskesi ve uygulanan hello DNS ayarları toobe toowait olabilir. Bir "Merhaba cihaz hazır değil." alırsanız hata iletisi, Itanium tabanlı sistemler için onay hello fiziksel ağ bağlantısı hello DATA 0 ağ arabirimindeki üzerinde etkin denetleyicinizin.
     > 
     > 
8. (İsteğe bağlı), web ara sunucusunu yapılandırın. Web ara sunucusunun yapılandırması isteğe bağlı olsa **bir web ara sunucu kullanıyorsanız, burada yalnızca bunu yapılandırabileceğinizi unutmayın**. Daha fazla bilgi için çok Git[cihazınız için web Proxy'yi Yapılandır](../articles/storsimple/storsimple-configure-web-proxy.md). Bu adım sırasında sorunları çalıştırırsanız tootroubleshooting yönergeler için bkz [web proxy yapılandırması sırasında hatalar](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-the-optional-web-proxy-settings).

     > [!NOTE]
     > Hiçbir zaman tooexit hello Kurulum Sihirbazı sırasında Ctrl + C tuşlarına basabilirsiniz. Bu komutu bildirmeden önce uyguladığınız ayarlar korunur.

1. Güvenlik nedenleriyle hello cihaz Yöneticisi parolası ilk oturumun hello sonra süresi dolar ve toochange gerekir sonraki oturumlar için. İstendiğinde cihaz yöneticisi parolasını verin. Geçerli bir cihaz yöneticisi parolası 8-15 karakter arasında olmalıdır. Merhaba parola birleşimini küçük harfler, büyük harf karakterler, sayılar ve özel karakterler içermelidir.
2. Merhaba StorSimple Snapshot Manager parolası burada da ayarlanır. StorSimple Snapshot Manager çalıştıran Windows konağınızla bir cihazın kimlik doğrulamasını yaptığınızda bu parolayı kullanın. İstendiğinde, 14 too15 karakter uzunluğunda bir parola sağlayın. Merhaba parola hello aşağıdakilerden üçünün bir birleşimi içermelidir: küçük harfler, büyük harf, sayısal ve özel karakter. 
   
   ![StorSimple kayıt cihazı 4](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice4-include.png)
   
   Merhaba StorSimple Snapshot Manager parolası hello StorSimple Yöneticisi hizmet arabirimden sıfırlayabilirsiniz. Ayrıntılı adımlar için çok Git[hello StorSimple Yöneticisi hizmetini kullanarak hello StorSimple parolalarını değiştirme](../articles/storsimple/storsimple-change-passwords.md).
   
   tootroubleshoot Bu adım sırasında sorunları başvurmak için tootroubleshooting Kılavuzu [toopasswords ilgili hatalarla ilgili](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-related-to-device-administrator-and-storsimple-snapshot-manager-passwords).
3. hello Kurulum Sihirbazı'nı Hello son adımı Cihazınızı StorSimple Yöneticisi hizmeti hello ile kaydeder. Bunun için 2. adımda elde ettiğiniz hello hizmet kayıt anahtarı gerekir. Merhaba kayıt anahtarını verdikten sonra 2-3 hello cihazın kaydolması dakika toowait gerekebilir.
   
   tootroubleshoot tüm olası cihaz kayıt sorunlarını başvurmak çok[cihaz kaydı sırasında hatalar](../articles/storsimple/storsimple-troubleshoot-deployment.md#errors-during-device-registration). Ayrıntılı sorun giderme için aynı zamanda çok başvurabilirsiniz[adım adım sorun giderme örnek](../articles/storsimple/storsimple-troubleshoot-deployment.md#step-by-step-storsimple-troubleshooting-example).
4. Merhaba cihaz kaydedildikten sonra hizmet verileri şifreleme anahtarı görüntülenir. Bu anahtarı kopyalayın ve güvenli bir konuma kaydedin.
   
   > [!WARNING]
   > Bu anahtar aygıtlarla hello hizmet kayıt anahtarı tooregister ek hello StorSimple Yöneticisi hizmeti ile gerekli olacaktır. Çok başvuran[StorSimple güvenlik](../articles/storsimple/storsimple-security.md) bu anahtarı hakkında daha fazla bilgi için.
   > 
   > 
   
    ![StorSimple kayıt cihazı 6](./media/storsimple-configure-and-register-device/HCS_RegisterYourDevice6-include.png)
   
    Merhaba seri konsol penceresinden toocopy hello metin yalnızca hello metni seçin. Ardından mümkün toopaste olmalıdır hello Pano veya başka bir metin düzenleyicisi içine. CTRL kullanmayın + C toocopy hello hizmet verileri şifreleme anahtarı. Ctrl + C kullanarak, tooexit hello Kurulum Sihirbazı neden olur. Sonuç olarak, hello cihaz Yöneticisi parolası ve hello StorSimple Snapshot Manager parolası değiştirilmez ve hello cihaz toohello varsayılan parolalarına döner.
5. Çıkış hello seri Konsolu.
6. Toohello Klasik Azure portalına dönün ve hello aşağıdaki adımları tamamlayın:
   
   1. StorSimple Yöneticisi hizmet tooaccess hello çift **Hızlı Başlangıç** sayfası.
   2. **Bağlı cihazları görüntüle**’ye tıklayın.
   3. Merhaba üzerinde **aygıtları** sayfasında, bu hello cihaz başarıyla bağlandı toohello hizmet hello durumu arayarak doğrulayın. Merhaba Aygıt durumu olmalıdır **çevrimiçi**. Merhaba cihaz durumu ise **çevrimdışı**, birkaç dakika hello cihaz çevrimiçi toocome için bekleyin.
   
   ![StorSimple Cihazları sayfası](./media/storsimple-configure-and-register-device/HCS_DevicesPageM-include.png) 
   
   > [!IMPORTANT]
   > Merhaba cihaz çevrimiçi olduktan sonra hello'den itibaren bu adımın söktüğünüz hello ağ kablolarını takın.
   > 
   > 

Merhaba cihaz sorunsuz kaydedildikten ve çevrimiçi olmadıktan sonra hello çalıştırabilirsiniz `Test-HcsmConnection -Verbose` ağ bağlantısı hello tooensure sağlam. Merhaba, cmdlet'in ayrıntılı kullanımı Git çok[Test HcsmConnection için cmdlet başvurusu](https://technet.microsoft.com/library/dn715782.aspx).

![Video var](./media/storsimple-configure-and-register-device/Video_icon.png) **Video var**

toowatch gösteren bir video tooconfigure ve kaydetme, StorSimple için Windows PowerShell aracılığıyla cihazınızın nasıl tıklatın [burada](https://azure.microsoft.com/documentation/videos/initialize-the-storsimple-appliance/).

