<!--author=alkohli last changed: 02/22/2016-->


### <a name="tooconfigure-and-register-hello-device"></a>Merhaba aygıt tooconfigure ve kaydetme
1. StorSimple cihaz seri konsoluna Hello Windows PowerShell arabirimine erişin. Bkz: [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](#use-putty-to-connect-to-the-device-serial-console) yönergeler için. **Emin toofollow hello yordamı tamamen olması veya mümkün tooaccess hello konsol olmaz.**
2. Açılan hello oturumunda Enter bir zaman tooget bir komut istemi tuşuna basın. 
3. Cihazınız için tooset istediğiniz istendiğinde toochoose hello dil olacaktır. Merhaba dili belirtin ve ardından Enter tuşuna basın. 
   
    ![StorSimple cihazı yapılandırma ve kaydetme 1](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice1-U1-include.png)
4. Sunulan hello seri konsol menüsünde seçeneği 1 toolog tam erişimle seçin. 
   
    ![StorSimple kayıt cihazı 2](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice2_U1-include.png)
   
     Adım 5-12 tooconfigure hello minimum gerekli ağ ayarlarını, cihazınız için tamamlayın. **Bu yapılandırma adımları hello etkin hello aygıt denetleyicisinde gerçekleştirilen toobe gerekir.** Merhaba seri konsol menüsünde hello başlık iletisi hello denetleyicisi durumunu gösterir. Değil bağlıysanız toohello active denetleyicisi kesin ve toohello etkin denetleyicisi bağlayın.
5. Merhaba komut istemine parolanızı yazın. Merhaba varsayılan cihaz parolası **Parola1**.
6. Komutu aşağıdaki türü hello: `Invoke-HcsSetupWizard`. 
7. Kurulum Sihirbazı'nı hello cihaz için hello ağ ayarlarını yapılandırmak toohelp görünür. Aşağıdaki bilgilerle hello hello sağlayın: 
   
   * Merhaba veri 0 ağ arabirimi için IP adresi
   * Alt ağ maskesi
   * Ağ geçidi
   * Birincil DNS sunucusu için IP adresi
     
        Merhaba sistem ağ ayarlarını hello işlemin her adımından sonra doğruladığını unutmayın.
     
     > [!NOTE]
     > Birkaç dakika boyunca hello alt ağ maskesi ve uygulanan hello DNS ayarları toobe toowait olabilir. "Onay hello ağ bağlantısı tooData 0" hata iletisi alırsanız, etkin denetleyicinizin DATA 0 ağ arabirimindeki hello hello fiziksel ağ bağlantısını denetleyin.
     > 
     > 
8. (İsteğe bağlı), web ara sunucusunu yapılandırın. Web ara sunucusunun yapılandırması isteğe bağlı olsa **bir web ara sunucu kullanıyorsanız, burada yalnızca bunu yapılandırabileceğinizi unutmayın**. Daha fazla bilgi için çok Git[cihazınız için web Proxy'yi Yapılandır](../articles/storsimple/storsimple-configure-web-proxy.md).
9. Cihazınız için Birincil NTP sunucusunu yapılandırın. Bulut hizmeti sağlayıcılarıyla doğrulanabileceği şekilde cihazınızı saati eşitlemesi gerektiğinden NTP sunucuları gereklidir. Ağınızın, NTP trafiğini toopass, veri merkezi toohello Internet gelen verdiğinden emin olun. Bu yapılamıyorsa dahili bir NTP sunucusu belirtin. 
10. Güvenlik nedenleriyle hello cihaz Yöneticisi parolası ilk oturumun hello sonra süresi dolar ve toochange gerekir artık BT. İstendiğinde cihaz yöneticisi parolasını verin. Geçerli bir cihaz yöneticisi parolası 8-15 karakter arasında olmalıdır. Merhaba parola üç hello şunları içermelidir: küçük harfler, büyük harf, sayısal ve özel karakter.
    
    <br/>![StorSimple kayıt cihazı 5](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice5_U1-include.png)
11. hello Kurulum Sihirbazı'nı Hello son adımı Cihazınızı StorSimple Yöneticisi hizmeti hello ile kaydeder. Bunun için 2. adımda elde ettiğiniz hello hizmet kayıt anahtarı gerekir. Merhaba kayıt anahtarını verdikten sonra 2-3 hello cihazın kaydolması dakika toowait gerekebilir.
    
    > [!NOTE]
    > Hiçbir zaman tooexit hello Kurulum Sihirbazı sırasında Ctrl + C tuşlarına basabilirsiniz. Tüm hello ağ ayarlarını (Data 0, alt ağ maskesi ve ağ geçidi için IP adresi) girdiyseniz girişleriniz korunur.
    > 
    > 
    
    ![StorSimple kayıt cihazı 6](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice6_U1-include.png)
12. Merhaba cihaz kaydedildikten sonra hizmet verileri şifreleme anahtarı görüntülenir. Bu anahtarı kopyalayın ve güvenli bir konuma kaydedin. **Bu anahtar aygıtlarla hello hizmet kayıt anahtarı tooregister ek hello StorSimple Yöneticisi hizmeti ile gerekli olacaktır.** Çok başvuran[StorSimple güvenlik](../articles/storsimple/storsimple-security.md) bu anahtarı hakkında daha fazla bilgi için.
    
    ![StorSimple kayıt cihazı 7](./media/storsimple-configure-and-register-device-u1/HCS_RegisterYourDevice7_U1-include.png)    
    
    > [!NOTE]
    > Merhaba seri konsol penceresinden toocopy hello metin yalnızca hello metni seçin. Ardından mümkün toopaste olmalıdır hello Pano veya başka bir metin düzenleyicisi içine. CTRL kullanmayın + C toocopy hello hizmet verileri şifreleme anahtarı. Ctrl + C kullanarak, tooexit hello Kurulum Sihirbazı neden olur. Sonuç olarak, hello cihaz Yöneticisi parolası değiştirilmez ve hello cihaz toohello varsayılan parola döner.
    > 
    > 
13. Çıkış hello seri Konsolu.
14. Toohello Klasik Azure portalına dönün ve hello aşağıdaki adımları tamamlayın:
    
    1. StorSimple Yöneticisi hizmet tooaccess hello çift **Hızlı Başlangıç** sayfası.
    2. **Bağlı cihazları görüntüle**’ye tıklayın.
    3. Merhaba üzerinde **aygıtları** sayfasında, bu hello cihaz başarıyla bağlandı toohello hizmet hello durumu arayarak doğrulayın. Merhaba Aygıt durumu olmalıdır **çevrimiçi**.
       
        ![StorSimple Cihazları sayfası](./media/storsimple-configure-and-register-device-u1/HCS_DevicesPageM_U1-include.png) 
       
        Merhaba cihaz durumu ise **çevrimdışı**, birkaç dakika hello cihaz çevrimiçi toocome için bekleyin. 
       
        Hello aygıt hala çevrimdışı sonra birkaç dakika sonra toomake güvenlik duvarı ağınızın açıklandığı şekilde yapılandırıldığından emin ihtiyacınız [ağ gereksinimleri, StorSimple cihazınız için](../articles/storsimple/storsimple-system-requirements.md). 
       
        Bu hello hizmet veri yolu tarafından StorSimple Yöneticisi hizmet-cihaz iletişimi için kullanılan gibi 9354 bağlantı noktasının giden iletişim için açık olduğunu doğrulayın.

