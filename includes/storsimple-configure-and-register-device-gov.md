<!--author=SharS last changed: 02/22/16-->

### <a name="tooconfigure-and-register-hello-device"></a>Merhaba aygıt tooconfigure ve kaydetme
1. StorSimple cihaz seri konsoluna Hello Windows PowerShell arabirimine erişin. Bkz: [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](#use-putty-to-connect-to-the-device-serial-console) yönergeler için. **Emin toofollow hello yordamı tamamen olması veya mümkün tooaccess hello konsol olmaz.**
2. Açılan hello oturumunda Enter bir zaman tooget bir komut istemi tuşuna basın. 
3. Cihazınız için tooset istediğiniz istendiğinde toochoose hello dil olacaktır. Merhaba dili belirtin ve ardından Enter tuşuna basın. 
   
    ![StorSimple cihazı yapılandırma ve kaydetme 1](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. Sunulan hello seri konsol menüsünde seçeneği 1 toolog tam erişimle seçin. 
   
    ![StorSimple kayıt cihazı 2](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. Cihazınız için adımları tooconfigure hello minimum gerekli ağ ayarlarını aşağıdaki hello gerçekleştirin.
   
   > [!IMPORTANT]
   > Bu yapılandırma adımları hello etkin hello aygıt denetleyicisinde gerçekleştirilen toobe gerekir. Merhaba seri konsol menüsünde hello başlık iletisi hello denetleyicisi durumunu gösterir. Olan değil bağlanırsanız toohello etkin denetleyicisi kesin ve toohello etkin denetleyicisi bağlayın.
   > 
   > 
   
   1. Merhaba komut istemine parolanızı yazın. Merhaba varsayılan cihaz parolası **Parola1**.
   2. Merhaba aşağıdaki komutu yazın:
      
        `Invoke-HcsSetupWizard`
   3. Kurulum Sihirbazı'nı hello cihaz için hello ağ ayarlarını yapılandırmak toohelp görünür. Aşağıdaki bilgilerle hello sağlayın: 
      
      * Veri 0 ağ arabirimi için IP adresi
      * Alt ağ maskesi
      * Ağ geçidi
      * Birincil DNS sunucusu için IP adresi
      * Birincil NTP sunucusu için IP adresi
      
      > [!NOTE]
      > Birkaç dakika boyunca hello alt ağ maskesi ve DNS ayarları toobe uygulanan toowait olabilir. 
      > 
      > 
   4. İsteğe bağlı olarak, web proxy sunucunuzu yapılandırın.
      
      > [!IMPORTANT]
      > Web proxy yapılandırması isteğe bağlı olsa da, bir web proxy kullanıyorsanız, yalnızca burada yapılandırabilirsiniz olduğunu unutmayın. Daha fazla bilgi için çok Git[cihazınız için web Proxy'yi Yapılandır](../articles/storsimple/storsimple-configure-web-proxy.md). 
      > 
      > 
6. Ctrl + C tuşlarına basın tooexit hello Kurulum Sihirbazı'nı.
7. Merhaba güncelleştirmeleri gibi yükleyin:
   
   1. Her iki hello denetleyicilerinde cmdlet tooset IP'leri aşağıdaki hello kullan:
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. Merhaba komut isteminde çalıştırmak `Get-HcsUpdateAvailability`. Güncelleştirmelerinin kullanılabilir olduğunu bildirilmesi gerekir.
   3. `Start-HcsUpdate` öğesini çalıştırın. Herhangi bir düğümde bu komutu çalıştırabilirsiniz. Güncelleştirmeler hello ilk denetleyicisinde uygulanır, hello denetleyicisi üzerinden başarısız olur ve ardından diğer denetleyicisi hello hello güncelleştirmeler üzerinde uygulanır.
      
      Çalıştırarak hello güncelleştirme hello ilerlemesini izleyebilirsiniz `Get-HcsUpdateStatus`.    
      
      Merhaba aşağıdaki örnek çıkış hello güncelleştirme göstermektedir.
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      örnek çıktı aşağıdaki hello bu hello güncelleştirme tamamlandığında gösterir.
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      Tüm güncelleştirmeleri de dahil olmak üzere, hello tooapply hello Windows güncelleştirmelerini too11 saat sürebilir.

8. Tüm hello yazılım güncelleştirmeleri doğru şekilde uygulanıp uygulanmadığını hello başarıyla yüklenen, çalışma hello aşağıdaki cmdlet'i tooconfirm güncelleştirmelerin:
   
     `Get-HcsSystem`
   
    Sürümleri aşağıdaki hello görmeniz gerekir:
   
   * HcsSoftwareVersion: 6.3.9600.17491
   * CisAgentVersion: 1.0.9037.0
   * MdsAgentVersion: 26.0.4696.1433
9. Bellenim güncelleştirme hello cmdlet tooconfirm aşağıdaki çalışma hello başarıyla uygulandı:
   
    `Start-HcsFirmwareCheck`.
   
     Merhaba bellenim durum olmalıdır **UpToDate**.
10. (Bunu toohello ortak Klasik Azure portalı varsayılan işaret ettiğinden) cmdlet toopoint hello cihaz toohello Microsoft Azure kamu portalı aşağıdaki hello çalıştırın. Bu, hem denetleyicileri yeniden başlatılır. Toosimultaneously bağlanmak tooboth denetleyicileri her denetleyici ne zaman yeniden görebilmeniz için iki PuTTY oturumu kullanmanızı öneririz.
    
     `Set-CloudPlatform -AzureGovt_US`
    
    Bir onay iletisi görürsünüz. Merhaba varsayılanı kabul edin (**Y**).
11. Cmdlet tooresume kurulumdan sonraki hello çalıştırın:
    
     `Invoke-HcsSetupWizard`
    
     ![Resume Kurulum Sihirbazı](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    Kurulum devam hello Sihirbazı'nı (hangi tooversion 17469 karşılık gelir) hello güncelleştirme 1 sürüm olacaktır. 
12. Merhaba ağ ayarlarını kabul edin. Her ayar kabul ettikten sonra bir doğrulama iletisi görürsünüz.
13. Güvenlik nedenleriyle hello cihaz Yöneticisi parolası ilk oturumun hello sonra süresi dolar ve toochange gerekir artık BT. İstendiğinde cihaz yöneticisi parolasını verin. Geçerli bir cihaz yöneticisi parolası 8-15 karakter arasında olmalıdır. Merhaba parola üç hello şunları içermelidir: küçük harfler, büyük harf, sayısal ve özel karakter.
    
    <br/>![StorSimple kayıt cihazı 5](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. hello Kurulum Sihirbazı'nı Hello son adımı Cihazınızı StorSimple Yöneticisi hizmeti hello ile kaydeder. Bunun için makalesinde aldığınız hizmet kayıt anahtarını hello [2. adım: hello hizmet kayıt anahtarını Al](#step-2-get-the-service-registration-key). Merhaba kayıt anahtarını verdikten sonra 2-3 hello cihazın kaydolması dakika toowait gerekebilir.
    
    > [!NOTE]
    > Hiçbir zaman tooexit hello Kurulum Sihirbazı sırasında Ctrl + C tuşlarına basabilirsiniz. Tüm hello ağ ayarlarını (Data 0, alt ağ maskesi ve ağ geçidi için IP adresi) girdiyseniz girişleriniz korunur.
    > 
    > 
    
    ![StorSimple kayıt ilerleme durumu](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. Merhaba cihaz kaydedildikten sonra hizmet verileri şifreleme anahtarı görüntülenir. Bu anahtarı kopyalayın ve güvenli bir konuma kaydedin. **Bu anahtar aygıtlarla hello hizmet kayıt anahtarı tooregister ek hello StorSimple Yöneticisi hizmeti ile gerekli olacaktır.** Çok başvuran[StorSimple güvenlik](../articles/storsimple/storsimple-security.md) bu anahtarı hakkında daha fazla bilgi için.
    
    ![StorSimple kayıt cihazı 7](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > Merhaba seri konsol penceresinden toocopy hello metin yalnızca hello metni seçin. Ardından mümkün toopaste olmalıdır hello Pano veya başka bir metin düzenleyicisi içine. 
    > 
    > CTRL kullanmayın + C toocopy hello hizmet verileri şifreleme anahtarı. Ctrl + C kullanarak, tooexit hello Kurulum Sihirbazı neden olur. Sonuç olarak, hello cihaz Yöneticisi parolası değiştirilmez ve hello cihaz toohello varsayılan parola döner.
    > 
    > 
16. Çıkış hello seri Konsolu.
17. Toohello Azure Kamu portalına dönün ve hello aşağıdaki adımları tamamlayın:
    
    1. StorSimple Yöneticisi hizmet tooaccess hello çift **Hızlı Başlangıç** sayfası.
    2. **Bağlı cihazları görüntüle**’ye tıklayın.
    3. Merhaba üzerinde **aygıtları** sayfasında, bu hello cihaz başarıyla bağlandı toohello hizmet hello durumu arayarak doğrulayın. Merhaba Aygıt durumu olmalıdır **çevrimiçi**.
       
        ![StorSimple Cihazları sayfası](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        Merhaba cihaz durumu ise **çevrimdışı**, birkaç dakika hello cihaz çevrimiçi toocome için bekleyin. 
       
        Hello aygıt hala çevrimdışı sonra birkaç dakika sonra toomake güvenlik duvarı ağınızın açıklandığı şekilde yapılandırıldığından emin ihtiyacınız [ağ gereksinimleri, StorSimple cihazınız için](../articles/storsimple/storsimple-system-requirements.md). 
       
        Bu hello hizmet veri yolu tarafından StorSimple Yöneticisi hizmet-cihaz iletişimi için kullanılan gibi 9354 bağlantı noktasının giden iletişim için açık olduğunu doğrulayın.

