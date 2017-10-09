<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a>Merhaba aygıt tooconfigure ve kaydetme

1. StorSimple cihaz seri konsoluna Hello Windows PowerShell arabirimine erişin. Bkz: [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](#use-putty-to-connect-to-the-device-serial-console) yönergeler için. **Emin toofollow hello yordamı tamamen olması veya mümkün tooaccess hello konsol olmaz.**

2. Açılan hello oturumunda basın **Enter** bir saat tooget bir komut istemi.

3. Cihazınız için tooset istediğiniz istendiğinde toochoose hello dil olacaktır. Merhaba dil belirtin ve sonra basın **Enter**.

4. Sunulan hello seri konsol menüsünde 1 çok seçeneğini**oturum oturum tam erişim**.
     Adım 5-12 tooconfigure hello minimum gerekli ağ ayarlarını, cihazınız için tamamlayın. **Bu yapılandırma adımları hello etkin hello aygıt denetleyicisinde gerçekleştirilen toobe gerekir.** Merhaba seri konsol menüsünde hello başlık iletisi hello denetleyicisi durumunu gösterir. Değil bağlıysanız toohello active denetleyicisi kesin ve toohello etkin denetleyicisi bağlayın.

5. Merhaba komut istemine parolanızı yazın. Merhaba varsayılan cihaz parolası **Parola1**.

6. Komutu aşağıdaki türü hello: `Invoke-HcsSetupWizard`.

7. Kurulum Sihirbazı'nı hello cihaz için hello ağ ayarlarını yapılandırmak toohelp görünür. Aşağıdaki bilgilerle hello hello sağlayın:
   
   * Merhaba veri 0 ağ arabirimi için IP adresi
   * Alt ağ maskesi
   * Ağ geçidi
   * Birincil DNS sunucusu için IP adresi

   Aşağıda örnek bir çıktı sunulmuştur.

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Active
        ---------------------------------------------------------------

        Your device needs toobe registered with hello Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' tooset up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like tooconfigure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    Örnek çıktı önceki hello hello sistem hello işlemin her adımından sonra ağ ayarlarını doğrulama görebilirsiniz.

     > [!NOTE]
     > Birkaç dakika boyunca hello alt ağ maskesi ve uygulanan hello DNS ayarları toobe toowait olabilir. "Onay hello ağ bağlantısı tooData 0" hata iletisi alırsanız, etkin denetleyicinizin DATA 0 ağ arabirimindeki hello hello fiziksel ağ bağlantısını denetleyin.

8. (İsteğe bağlı), web ara sunucusunu yapılandırın. Web ara sunucusunun yapılandırması isteğe bağlı olsa **bir web ara sunucu kullanıyorsanız, burada yalnızca bunu yapılandırabileceğinizi unutmayın**. Daha fazla bilgi için çok Git[cihazınız için web Proxy'yi Yapılandır](../articles/storsimple/storsimple-8000-configure-web-proxy.md).
9. Cihazınız için Birincil NTP sunucusunu yapılandırın. Bulut hizmeti sağlayıcılarıyla doğrulanabileceği şekilde cihazınızı saati eşitlemesi gerektiğinden NTP sunucuları gereklidir. Ağınızın, NTP trafiğini toopass, veri merkezi toohello Internet gelen verdiğinden emin olun. Bu yapılamıyorsa dahili bir NTP sunucusu belirtin.

    Örnek çıktı aşağıda gösterilmiştir.

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. Güvenlik nedenleriyle hello cihaz Yöneticisi parolası ilk oturumun hello sonra süresi dolar ve toochange gerekir artık BT. İstendiğinde cihaz yöneticisi parolasını verin. Geçerli bir cihaz yöneticisi parolası 8-15 karakter arasında olmalıdır. Merhaba parola üç hello şunları içermelidir: küçük harfler, büyük harf, sayısal ve özel karakter.

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. hello Kurulum Sihirbazı'nı Hello son adımı Cihazınızı StorSimple cihaz Yöneticisi hizmeti hello ile kaydeder. Bunun için 2. adımda elde ettiğiniz hello hizmet kayıt anahtarı gerekir. Merhaba kayıt anahtarını verdikten sonra 2-3 hello cihazın kaydolması dakika toowait gerekebilir.
    
    > [!NOTE]
    > Hiçbir zaman tooexit hello Kurulum Sihirbazı sırasında Ctrl + C tuşlarına basabilirsiniz. Tüm hello ağ ayarlarını (Data 0, alt ağ maskesi ve ağ geçidi için IP adresi) girdiyseniz girişleriniz korunur.
    
    Örnek çıktı aşağıda gösterilmiştir.

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. Merhaba cihaz kaydedildikten sonra hizmet verileri şifreleme anahtarı görüntülenir. Bu anahtarı kopyalayın ve güvenli bir konuma kaydedin. **Bu anahtar aygıtlarla hello hizmet kayıt anahtarı tooregister ek hello StorSimple cihaz Yöneticisi hizmeti ile gerekli olacaktır.** Çok başvuran[StorSimple güvenlik](../articles/storsimple/storsimple-security.md) bu anahtarı hakkında daha fazla bilgi için.
    
    ![StorSimple kayıt cihazı 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > Merhaba seri konsol penceresinden toocopy hello metin yalnızca hello metni seçin. Ardından mümkün toopaste olmalıdır hello Pano veya başka bir metin düzenleyicisi içine. CTRL kullanmayın + C toocopy hello hizmet verileri şifreleme anahtarı. Ctrl + C kullanarak, tooexit hello Kurulum Sihirbazı neden olur. Sonuç olarak, hello cihaz Yöneticisi parolası değiştirilmez ve hello cihaz toohello varsayılan parola döner.
    
13. Çıkış hello seri Konsolu.
14. Toohello Azure portalına dönün ve hello aşağıdaki adımları tamamlayın:
    
    1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin.
    2. **Cihazlar**’a tıklayın.
    3. Hello aygıtları listeleme tablo, bu hello aygıt başarıyla toohello hizmeti hello durumu arayarak bağlandı doğrulayın. Merhaba Aygıt durumu olmalıdır **yukarı tooset hazır**.
       
        ![StorSimple Cihazları sayfası](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        Toowait birkaç dakika hello aygıt durum toochange için çok ihtiyacınız**yukarı tooset hazır**.
       
        Merhaba aygıt göstermiyor bu listede sonra güvenlik duvarı ağınızın açıklandığı şekilde yapılandırıldığından emin toomake ihtiyacınız [ağ gereksinimleri, StorSimple cihazınız için](../articles/storsimple/storsimple-8000-system-requirements.md). Bu hello hizmet veri yolu tarafından StorSimple cihaz Yöneticisi hizmet-cihaz iletişimi için kullanılan gibi 9354 bağlantı noktasının giden iletişim için açık olduğunu doğrulayın.

