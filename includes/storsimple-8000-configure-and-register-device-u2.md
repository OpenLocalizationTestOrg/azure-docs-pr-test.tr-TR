<!--author=alkohli last changed: 01/18/2017-->


#### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="35ed6-101">Merhaba aygıt tooconfigure ve kaydetme</span><span class="sxs-lookup"><span data-stu-id="35ed6-101">tooconfigure and register hello device</span></span>

1. <span data-ttu-id="35ed6-102">StorSimple cihaz seri konsoluna Hello Windows PowerShell arabirimine erişin.</span><span class="sxs-lookup"><span data-stu-id="35ed6-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="35ed6-103">Bkz: [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](#use-putty-to-connect-to-the-device-serial-console) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="35ed6-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="35ed6-104">**Emin toofollow hello yordamı tamamen olması veya mümkün tooaccess hello konsol olmaz.**</span><span class="sxs-lookup"><span data-stu-id="35ed6-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>

2. <span data-ttu-id="35ed6-105">Açılan hello oturumunda basın **Enter** bir saat tooget bir komut istemi.</span><span class="sxs-lookup"><span data-stu-id="35ed6-105">In hello session that opens up, press **Enter** one time tooget a command prompt.</span></span>

3. <span data-ttu-id="35ed6-106">Cihazınız için tooset istediğiniz istendiğinde toochoose hello dil olacaktır.</span><span class="sxs-lookup"><span data-stu-id="35ed6-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="35ed6-107">Merhaba dil belirtin ve sonra basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="35ed6-107">Specify hello language, and then press **Enter**.</span></span>

4. <span data-ttu-id="35ed6-108">Sunulan hello seri konsol menüsünde 1 çok seçeneğini**oturum oturum tam erişim**.</span><span class="sxs-lookup"><span data-stu-id="35ed6-108">In hello serial console menu that is presented, choose option 1 too**log in with full access**.</span></span>
     <span data-ttu-id="35ed6-109">Adım 5-12 tooconfigure hello minimum gerekli ağ ayarlarını, cihazınız için tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="35ed6-109">Complete steps 5-12 tooconfigure hello minimum required network settings for your device.</span></span> <span data-ttu-id="35ed6-110">**Bu yapılandırma adımları hello etkin hello aygıt denetleyicisinde gerçekleştirilen toobe gerekir.**</span><span class="sxs-lookup"><span data-stu-id="35ed6-110">**These configuration steps need toobe performed on hello active controller of hello device.**</span></span> <span data-ttu-id="35ed6-111">Merhaba seri konsol menüsünde hello başlık iletisi hello denetleyicisi durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="35ed6-111">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="35ed6-112">Değil bağlıysanız toohello active denetleyicisi kesin ve toohello etkin denetleyicisi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="35ed6-112">If you are not connected toohello active controller, disconnect and then connect toohello active controller.</span></span>

5. <span data-ttu-id="35ed6-113">Merhaba komut istemine parolanızı yazın.</span><span class="sxs-lookup"><span data-stu-id="35ed6-113">At hello command prompt, type your password.</span></span> <span data-ttu-id="35ed6-114">Merhaba varsayılan cihaz parolası **Parola1**.</span><span class="sxs-lookup"><span data-stu-id="35ed6-114">hello default device password is **Password1**.</span></span>

6. <span data-ttu-id="35ed6-115">Komutu aşağıdaki türü hello: `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="35ed6-115">Type hello following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="35ed6-116">Kurulum Sihirbazı'nı hello cihaz için hello ağ ayarlarını yapılandırmak toohelp görünür.</span><span class="sxs-lookup"><span data-stu-id="35ed6-116">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="35ed6-117">Aşağıdaki bilgilerle hello hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="35ed6-117">Supply hello hello following information:</span></span>
   
   * <span data-ttu-id="35ed6-118">Merhaba veri 0 ağ arabirimi için IP adresi</span><span class="sxs-lookup"><span data-stu-id="35ed6-118">IP address for hello DATA 0 network interface</span></span>
   * <span data-ttu-id="35ed6-119">Alt ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="35ed6-119">Subnet mask</span></span>
   * <span data-ttu-id="35ed6-120">Ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="35ed6-120">Gateway</span></span>
   * <span data-ttu-id="35ed6-121">Birincil DNS sunucusu için IP adresi</span><span class="sxs-lookup"><span data-stu-id="35ed6-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="35ed6-122">Aşağıda örnek bir çıktı sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="35ed6-122">A sample output is presented below.</span></span>

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
    <span data-ttu-id="35ed6-123">Örnek çıktı önceki hello hello sistem hello işlemin her adımından sonra ağ ayarlarını doğrulama görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35ed6-123">In hello preceding sample output, you can see that hello system is validating network settings after each step in hello process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="35ed6-124">Birkaç dakika boyunca hello alt ağ maskesi ve uygulanan hello DNS ayarları toobe toowait olabilir.</span><span class="sxs-lookup"><span data-stu-id="35ed6-124">You may have toowait for a few minutes for hello subnet mask and hello DNS settings toobe applied.</span></span> <span data-ttu-id="35ed6-125">"Onay hello ağ bağlantısı tooData 0" hata iletisi alırsanız, etkin denetleyicinizin DATA 0 ağ arabirimindeki hello hello fiziksel ağ bağlantısını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="35ed6-125">If you get a "Check hello network connectivity tooData 0" error message, check hello physical network connection on hello DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="35ed6-126">(İsteğe bağlı), web ara sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="35ed6-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="35ed6-127">Web ara sunucusunun yapılandırması isteğe bağlı olsa **bir web ara sunucu kullanıyorsanız, burada yalnızca bunu yapılandırabileceğinizi unutmayın**.</span><span class="sxs-lookup"><span data-stu-id="35ed6-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="35ed6-128">Daha fazla bilgi için çok Git[cihazınız için web Proxy'yi Yapılandır](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="35ed6-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="35ed6-129">Cihazınız için Birincil NTP sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="35ed6-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="35ed6-130">Bulut hizmeti sağlayıcılarıyla doğrulanabileceği şekilde cihazınızı saati eşitlemesi gerektiğinden NTP sunucuları gereklidir.</span><span class="sxs-lookup"><span data-stu-id="35ed6-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="35ed6-131">Ağınızın, NTP trafiğini toopass, veri merkezi toohello Internet gelen verdiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="35ed6-131">Ensure that your network allows NTP traffic toopass from your datacenter toohello Internet.</span></span> <span data-ttu-id="35ed6-132">Bu yapılamıyorsa dahili bir NTP sunucusu belirtin.</span><span class="sxs-lookup"><span data-stu-id="35ed6-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="35ed6-133">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="35ed6-133">A sample output is shown below.</span></span>

    ```
        Would you like tooconfigure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="35ed6-134">Güvenlik nedenleriyle hello cihaz Yöneticisi parolası ilk oturumun hello sonra süresi dolar ve toochange gerekir artık BT.</span><span class="sxs-lookup"><span data-stu-id="35ed6-134">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="35ed6-135">İstendiğinde cihaz yöneticisi parolasını verin.</span><span class="sxs-lookup"><span data-stu-id="35ed6-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="35ed6-136">Geçerli bir cihaz yöneticisi parolası 8-15 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="35ed6-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="35ed6-137">Merhaba parola üç hello şunları içermelidir: küçük harfler, büyük harf, sayısal ve özel karakter.</span><span class="sxs-lookup"><span data-stu-id="35ed6-137">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        hello device administrator password must be between 8 and 15 characters. hello password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="35ed6-138">hello Kurulum Sihirbazı'nı Hello son adımı Cihazınızı StorSimple cihaz Yöneticisi hizmeti hello ile kaydeder.</span><span class="sxs-lookup"><span data-stu-id="35ed6-138">hello final step in hello setup wizard registers your device with hello StorSimple Device Manager service.</span></span> <span data-ttu-id="35ed6-139">Bunun için 2. adımda elde ettiğiniz hello hizmet kayıt anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="35ed6-139">For this, you will need hello service registration key that you obtained in step 2.</span></span> <span data-ttu-id="35ed6-140">Merhaba kayıt anahtarını verdikten sonra 2-3 hello cihazın kaydolması dakika toowait gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="35ed6-140">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="35ed6-141">Hiçbir zaman tooexit hello Kurulum Sihirbazı sırasında Ctrl + C tuşlarına basabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="35ed6-141">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="35ed6-142">Tüm hello ağ ayarlarını (Data 0, alt ağ maskesi ve ağ geçidi için IP adresi) girdiyseniz girişleriniz korunur.</span><span class="sxs-lookup"><span data-stu-id="35ed6-142">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="35ed6-143">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="35ed6-143">A sample output is shown below.</span></span>

    ```
        hello service registration key is available in hello StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="35ed6-144">Merhaba cihaz kaydedildikten sonra hizmet verileri şifreleme anahtarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="35ed6-144">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="35ed6-145">Bu anahtarı kopyalayın ve güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="35ed6-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="35ed6-146">**Bu anahtar aygıtlarla hello hizmet kayıt anahtarı tooregister ek hello StorSimple cihaz Yöneticisi hizmeti ile gerekli olacaktır.**</span><span class="sxs-lookup"><span data-stu-id="35ed6-146">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Device Manager service.**</span></span> <span data-ttu-id="35ed6-147">Çok başvuran[StorSimple güvenlik](../articles/storsimple/storsimple-security.md) bu anahtarı hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="35ed6-147">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple kayıt cihazı 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="35ed6-149">Merhaba seri konsol penceresinden toocopy hello metin yalnızca hello metni seçin.</span><span class="sxs-lookup"><span data-stu-id="35ed6-149">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="35ed6-150">Ardından mümkün toopaste olmalıdır hello Pano veya başka bir metin düzenleyicisi içine.</span><span class="sxs-lookup"><span data-stu-id="35ed6-150">You should then be able toopaste it in hello clipboard or any text editor.</span></span> <span data-ttu-id="35ed6-151">CTRL kullanmayın + C toocopy hello hizmet verileri şifreleme anahtarı.</span><span class="sxs-lookup"><span data-stu-id="35ed6-151">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="35ed6-152">Ctrl + C kullanarak, tooexit hello Kurulum Sihirbazı neden olur.</span><span class="sxs-lookup"><span data-stu-id="35ed6-152">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="35ed6-153">Sonuç olarak, hello cihaz Yöneticisi parolası değiştirilmez ve hello cihaz toohello varsayılan parola döner.</span><span class="sxs-lookup"><span data-stu-id="35ed6-153">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    
13. <span data-ttu-id="35ed6-154">Çıkış hello seri Konsolu.</span><span class="sxs-lookup"><span data-stu-id="35ed6-154">Exit hello serial console.</span></span>
14. <span data-ttu-id="35ed6-155">Toohello Azure portalına dönün ve hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="35ed6-155">Return toohello Azure portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="35ed6-156">Tooyour StorSimple cihaz Yöneticisi hizmeti gidin.</span><span class="sxs-lookup"><span data-stu-id="35ed6-156">Go tooyour StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="35ed6-157">**Cihazlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="35ed6-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="35ed6-158">Hello aygıtları listeleme tablo, bu hello aygıt başarıyla toohello hizmeti hello durumu arayarak bağlandı doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="35ed6-158">In hello tabular listing of devices, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="35ed6-159">Merhaba Aygıt durumu olmalıdır **yukarı tooset hazır**.</span><span class="sxs-lookup"><span data-stu-id="35ed6-159">hello device status should be **Ready tooset up**.</span></span>
       
        ![StorSimple Cihazları sayfası](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="35ed6-161">Toowait birkaç dakika hello aygıt durum toochange için çok ihtiyacınız**yukarı tooset hazır**.</span><span class="sxs-lookup"><span data-stu-id="35ed6-161">You may need toowait for a couple of minutes for hello device status toochange too**Ready tooset up**.</span></span>
       
        <span data-ttu-id="35ed6-162">Merhaba aygıt göstermiyor bu listede sonra güvenlik duvarı ağınızın açıklandığı şekilde yapılandırıldığından emin toomake ihtiyacınız [ağ gereksinimleri, StorSimple cihazınız için](../articles/storsimple/storsimple-8000-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="35ed6-162">If hello device does not show up in this list, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="35ed6-163">Bu hello hizmet veri yolu tarafından StorSimple cihaz Yöneticisi hizmet-cihaz iletişimi için kullanılan gibi 9354 bağlantı noktasının giden iletişim için açık olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="35ed6-163">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Device Manager service-to-device communication.</span></span>

