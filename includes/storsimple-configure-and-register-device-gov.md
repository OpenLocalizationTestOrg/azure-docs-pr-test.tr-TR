<!--author=SharS last changed: 02/22/16-->

### <a name="tooconfigure-and-register-hello-device"></a><span data-ttu-id="3bdff-101">Merhaba aygıt tooconfigure ve kaydetme</span><span class="sxs-lookup"><span data-stu-id="3bdff-101">tooconfigure and register hello device</span></span>
1. <span data-ttu-id="3bdff-102">StorSimple cihaz seri konsoluna Hello Windows PowerShell arabirimine erişin.</span><span class="sxs-lookup"><span data-stu-id="3bdff-102">Access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="3bdff-103">Bkz: [kullanım PuTTY tooconnect toohello cihaz seri konsoluna](#use-putty-to-connect-to-the-device-serial-console) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="3bdff-103">See [Use PuTTY tooconnect toohello device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="3bdff-104">**Emin toofollow hello yordamı tamamen olması veya mümkün tooaccess hello konsol olmaz.**</span><span class="sxs-lookup"><span data-stu-id="3bdff-104">**Be sure toofollow hello procedure exactly or you will not be able tooaccess hello console.**</span></span>
2. <span data-ttu-id="3bdff-105">Açılan hello oturumunda Enter bir zaman tooget bir komut istemi tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="3bdff-105">In hello session that opens up, press Enter one time tooget a command prompt.</span></span> 
3. <span data-ttu-id="3bdff-106">Cihazınız için tooset istediğiniz istendiğinde toochoose hello dil olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3bdff-106">You will be prompted toochoose hello language that you would like tooset for your device.</span></span> <span data-ttu-id="3bdff-107">Merhaba dili belirtin ve ardından Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="3bdff-107">Specify hello language, and then press Enter.</span></span> 
   
    ![StorSimple cihazı yapılandırma ve kaydetme 1](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="3bdff-109">Sunulan hello seri konsol menüsünde seçeneği 1 toolog tam erişimle seçin.</span><span class="sxs-lookup"><span data-stu-id="3bdff-109">In hello serial console menu that is presented, choose option 1 toolog on with full access.</span></span> 
   
    ![StorSimple kayıt cihazı 2](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="3bdff-111">Cihazınız için adımları tooconfigure hello minimum gerekli ağ ayarlarını aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="3bdff-111">Perform hello following steps tooconfigure hello minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="3bdff-112">Bu yapılandırma adımları hello etkin hello aygıt denetleyicisinde gerçekleştirilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bdff-112">These configuration steps need toobe performed on hello active controller of hello device.</span></span> <span data-ttu-id="3bdff-113">Merhaba seri konsol menüsünde hello başlık iletisi hello denetleyicisi durumunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="3bdff-113">hello serial console menu indicates hello controller state in hello banner message.</span></span> <span data-ttu-id="3bdff-114">Olan değil bağlanırsanız toohello etkin denetleyicisi kesin ve toohello etkin denetleyicisi bağlayın.</span><span class="sxs-lookup"><span data-stu-id="3bdff-114">If you are not connect toohello active controller, disconnect and then connect toohello active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="3bdff-115">Merhaba komut istemine parolanızı yazın.</span><span class="sxs-lookup"><span data-stu-id="3bdff-115">At hello command prompt, type your password.</span></span> <span data-ttu-id="3bdff-116">Merhaba varsayılan cihaz parolası **Parola1**.</span><span class="sxs-lookup"><span data-stu-id="3bdff-116">hello default device password is **Password1**.</span></span>
   2. <span data-ttu-id="3bdff-117">Merhaba aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="3bdff-117">Type hello following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="3bdff-118">Kurulum Sihirbazı'nı hello cihaz için hello ağ ayarlarını yapılandırmak toohelp görünür.</span><span class="sxs-lookup"><span data-stu-id="3bdff-118">A setup wizard will appear toohelp you configure hello network settings for hello device.</span></span> <span data-ttu-id="3bdff-119">Aşağıdaki bilgilerle hello sağlayın:</span><span class="sxs-lookup"><span data-stu-id="3bdff-119">Supply hello following information:</span></span> 
      
      * <span data-ttu-id="3bdff-120">Veri 0 ağ arabirimi için IP adresi</span><span class="sxs-lookup"><span data-stu-id="3bdff-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="3bdff-121">Alt ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="3bdff-121">Subnet mask</span></span>
      * <span data-ttu-id="3bdff-122">Ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="3bdff-122">Gateway</span></span>
      * <span data-ttu-id="3bdff-123">Birincil DNS sunucusu için IP adresi</span><span class="sxs-lookup"><span data-stu-id="3bdff-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="3bdff-124">Birincil NTP sunucusu için IP adresi</span><span class="sxs-lookup"><span data-stu-id="3bdff-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="3bdff-125">Birkaç dakika boyunca hello alt ağ maskesi ve DNS ayarları toobe uygulanan toowait olabilir.</span><span class="sxs-lookup"><span data-stu-id="3bdff-125">You may have toowait for a few minutes for hello subnet mask and DNS settings toobe applied.</span></span> 
      > 
      > 
   4. <span data-ttu-id="3bdff-126">İsteğe bağlı olarak, web proxy sunucunuzu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="3bdff-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="3bdff-127">Web proxy yapılandırması isteğe bağlı olsa da, bir web proxy kullanıyorsanız, yalnızca burada yapılandırabilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="3bdff-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="3bdff-128">Daha fazla bilgi için çok Git[cihazınız için web Proxy'yi Yapılandır](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="3bdff-128">For more information, go too[Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span> 
      > 
      > 
6. <span data-ttu-id="3bdff-129">Ctrl + C tuşlarına basın tooexit hello Kurulum Sihirbazı'nı.</span><span class="sxs-lookup"><span data-stu-id="3bdff-129">Press Ctrl + C tooexit hello setup wizard.</span></span>
7. <span data-ttu-id="3bdff-130">Merhaba güncelleştirmeleri gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="3bdff-130">Install hello updates as follows:</span></span>
   
   1. <span data-ttu-id="3bdff-131">Her iki hello denetleyicilerinde cmdlet tooset IP'leri aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="3bdff-131">Use hello following cmdlet tooset IPs on both hello controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="3bdff-132">Merhaba komut isteminde çalıştırmak `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="3bdff-132">At hello command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="3bdff-133">Güncelleştirmelerinin kullanılabilir olduğunu bildirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="3bdff-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="3bdff-134">`Start-HcsUpdate` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3bdff-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="3bdff-135">Herhangi bir düğümde bu komutu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bdff-135">You can run this command on any node.</span></span> <span data-ttu-id="3bdff-136">Güncelleştirmeler hello ilk denetleyicisinde uygulanır, hello denetleyicisi üzerinden başarısız olur ve ardından diğer denetleyicisi hello hello güncelleştirmeler üzerinde uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3bdff-136">Updates will be applied on hello first controller, hello controller will fail over, and then hello updates will be applied on hello other controller.</span></span>
      
      <span data-ttu-id="3bdff-137">Çalıştırarak hello güncelleştirme hello ilerlemesini izleyebilirsiniz `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="3bdff-137">You can monitor hello progress of hello update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="3bdff-138">Merhaba aşağıdaki örnek çıkış hello güncelleştirme göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="3bdff-138">hello following sample output shows hello update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      <span data-ttu-id="3bdff-139">örnek çıktı aşağıdaki hello bu hello güncelleştirme tamamlandığında gösterir.</span><span class="sxs-lookup"><span data-stu-id="3bdff-139">hello following sample output indicates that hello update is finished.</span></span>
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      <span data-ttu-id="3bdff-140">Tüm güncelleştirmeleri de dahil olmak üzere, hello tooapply hello Windows güncelleştirmelerini too11 saat sürebilir.</span><span class="sxs-lookup"><span data-stu-id="3bdff-140">It may take up too11 hours tooapply all hello updates, including hello Windows Updates.</span></span>

8. <span data-ttu-id="3bdff-141">Tüm hello yazılım güncelleştirmeleri doğru şekilde uygulanıp uygulanmadığını hello başarıyla yüklenen, çalışma hello aşağıdaki cmdlet'i tooconfirm güncelleştirmelerin:</span><span class="sxs-lookup"><span data-stu-id="3bdff-141">After all hello updates are successfully installed, run hello following cmdlet tooconfirm that hello software updates were applied correctly:</span></span>
   
     `Get-HcsSystem`
   
    <span data-ttu-id="3bdff-142">Sürümleri aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="3bdff-142">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="3bdff-143">HcsSoftwareVersion: 6.3.9600.17491</span><span class="sxs-lookup"><span data-stu-id="3bdff-143">HcsSoftwareVersion: 6.3.9600.17491</span></span>
   * <span data-ttu-id="3bdff-144">CisAgentVersion: 1.0.9037.0</span><span class="sxs-lookup"><span data-stu-id="3bdff-144">CisAgentVersion: 1.0.9037.0</span></span>
   * <span data-ttu-id="3bdff-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="3bdff-145">MdsAgentVersion: 26.0.4696.1433</span></span>
9. <span data-ttu-id="3bdff-146">Bellenim güncelleştirme hello cmdlet tooconfirm aşağıdaki çalışma hello başarıyla uygulandı:</span><span class="sxs-lookup"><span data-stu-id="3bdff-146">Run hello following cmdlet tooconfirm that hello firmware update was applied correctly:</span></span>
   
    <span data-ttu-id="3bdff-147">`Start-HcsFirmwareCheck`.</span><span class="sxs-lookup"><span data-stu-id="3bdff-147">`Start-HcsFirmwareCheck`.</span></span>
   
     <span data-ttu-id="3bdff-148">Merhaba bellenim durum olmalıdır **UpToDate**.</span><span class="sxs-lookup"><span data-stu-id="3bdff-148">hello firmware status should be **UpToDate**.</span></span>
10. <span data-ttu-id="3bdff-149">(Bunu toohello ortak Klasik Azure portalı varsayılan işaret ettiğinden) cmdlet toopoint hello cihaz toohello Microsoft Azure kamu portalı aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="3bdff-149">Run hello following cmdlet toopoint hello device toohello Microsoft Azure Government portal (because it points toohello public Azure classic portal by default).</span></span> <span data-ttu-id="3bdff-150">Bu, hem denetleyicileri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="3bdff-150">This will restart both controllers.</span></span> <span data-ttu-id="3bdff-151">Toosimultaneously bağlanmak tooboth denetleyicileri her denetleyici ne zaman yeniden görebilmeniz için iki PuTTY oturumu kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="3bdff-151">We recommend that you use two PuTTY sessions toosimultaneously connect tooboth controllers so that you can see when each controller is restarted.</span></span>
    
     `Set-CloudPlatform -AzureGovt_US`
    
    <span data-ttu-id="3bdff-152">Bir onay iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3bdff-152">You will see a confirmation message.</span></span> <span data-ttu-id="3bdff-153">Merhaba varsayılanı kabul edin (**Y**).</span><span class="sxs-lookup"><span data-stu-id="3bdff-153">Accept hello default (**Y**).</span></span>
11. <span data-ttu-id="3bdff-154">Cmdlet tooresume kurulumdan sonraki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="3bdff-154">Run hello following cmdlet tooresume setup:</span></span>
    
     `Invoke-HcsSetupWizard`
    
     ![Resume Kurulum Sihirbazı](./media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    <span data-ttu-id="3bdff-156">Kurulum devam hello Sihirbazı'nı (hangi tooversion 17469 karşılık gelir) hello güncelleştirme 1 sürüm olacaktır.</span><span class="sxs-lookup"><span data-stu-id="3bdff-156">When you resume setup, hello wizard will be hello Update 1 version (which corresponds tooversion 17469).</span></span> 
12. <span data-ttu-id="3bdff-157">Merhaba ağ ayarlarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="3bdff-157">Accept hello network settings.</span></span> <span data-ttu-id="3bdff-158">Her ayar kabul ettikten sonra bir doğrulama iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3bdff-158">You will see a validation message after you accept each setting.</span></span>
13. <span data-ttu-id="3bdff-159">Güvenlik nedenleriyle hello cihaz Yöneticisi parolası ilk oturumun hello sonra süresi dolar ve toochange gerekir artık BT.</span><span class="sxs-lookup"><span data-stu-id="3bdff-159">For security reasons, hello device administrator password expires after hello first session, and you will need toochange it now.</span></span> <span data-ttu-id="3bdff-160">İstendiğinde cihaz yöneticisi parolasını verin.</span><span class="sxs-lookup"><span data-stu-id="3bdff-160">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="3bdff-161">Geçerli bir cihaz yöneticisi parolası 8-15 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="3bdff-161">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="3bdff-162">Merhaba parola üç hello şunları içermelidir: küçük harfler, büyük harf, sayısal ve özel karakter.</span><span class="sxs-lookup"><span data-stu-id="3bdff-162">hello password must contain three of hello following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![StorSimple kayıt cihazı 5](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. <span data-ttu-id="3bdff-164">hello Kurulum Sihirbazı'nı Hello son adımı Cihazınızı StorSimple Yöneticisi hizmeti hello ile kaydeder.</span><span class="sxs-lookup"><span data-stu-id="3bdff-164">hello final step in hello setup wizard registers your device with hello StorSimple Manager service.</span></span> <span data-ttu-id="3bdff-165">Bunun için makalesinde aldığınız hizmet kayıt anahtarını hello [2. adım: hello hizmet kayıt anahtarını Al](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="3bdff-165">For this, you will need hello service registration key that you obtained in [Step 2: Get hello service registration key](#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="3bdff-166">Merhaba kayıt anahtarını verdikten sonra 2-3 hello cihazın kaydolması dakika toowait gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="3bdff-166">After you supply hello registration key, you may need toowait for 2-3 minutes before hello device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="3bdff-167">Hiçbir zaman tooexit hello Kurulum Sihirbazı sırasında Ctrl + C tuşlarına basabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3bdff-167">You can press Ctrl + C at any time tooexit hello setup wizard.</span></span> <span data-ttu-id="3bdff-168">Tüm hello ağ ayarlarını (Data 0, alt ağ maskesi ve ağ geçidi için IP adresi) girdiyseniz girişleriniz korunur.</span><span class="sxs-lookup"><span data-stu-id="3bdff-168">If you have entered all hello network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![StorSimple kayıt ilerleme durumu](./media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. <span data-ttu-id="3bdff-170">Merhaba cihaz kaydedildikten sonra hizmet verileri şifreleme anahtarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="3bdff-170">After hello device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="3bdff-171">Bu anahtarı kopyalayın ve güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3bdff-171">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="3bdff-172">**Bu anahtar aygıtlarla hello hizmet kayıt anahtarı tooregister ek hello StorSimple Yöneticisi hizmeti ile gerekli olacaktır.**</span><span class="sxs-lookup"><span data-stu-id="3bdff-172">**This key will be required with hello service registration key tooregister additional devices with hello StorSimple Manager service.**</span></span> <span data-ttu-id="3bdff-173">Çok başvuran[StorSimple güvenlik](../articles/storsimple/storsimple-security.md) bu anahtarı hakkında daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="3bdff-173">Refer too[StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple kayıt cihazı 7](./media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="3bdff-175">Merhaba seri konsol penceresinden toocopy hello metin yalnızca hello metni seçin.</span><span class="sxs-lookup"><span data-stu-id="3bdff-175">toocopy hello text from hello serial console window, simply select hello text.</span></span> <span data-ttu-id="3bdff-176">Ardından mümkün toopaste olmalıdır hello Pano veya başka bir metin düzenleyicisi içine.</span><span class="sxs-lookup"><span data-stu-id="3bdff-176">You should then be able toopaste it in hello clipboard or any text editor.</span></span> 
    > 
    > <span data-ttu-id="3bdff-177">CTRL kullanmayın + C toocopy hello hizmet verileri şifreleme anahtarı.</span><span class="sxs-lookup"><span data-stu-id="3bdff-177">DO NOT use Ctrl + C toocopy hello service data encryption key.</span></span> <span data-ttu-id="3bdff-178">Ctrl + C kullanarak, tooexit hello Kurulum Sihirbazı neden olur.</span><span class="sxs-lookup"><span data-stu-id="3bdff-178">Using Ctrl + C will cause you tooexit hello setup wizard.</span></span> <span data-ttu-id="3bdff-179">Sonuç olarak, hello cihaz Yöneticisi parolası değiştirilmez ve hello cihaz toohello varsayılan parola döner.</span><span class="sxs-lookup"><span data-stu-id="3bdff-179">As a result, hello device administrator password will not be changed and hello device will revert toohello default password.</span></span>
    > 
    > 
16. <span data-ttu-id="3bdff-180">Çıkış hello seri Konsolu.</span><span class="sxs-lookup"><span data-stu-id="3bdff-180">Exit hello serial console.</span></span>
17. <span data-ttu-id="3bdff-181">Toohello Azure Kamu portalına dönün ve hello aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="3bdff-181">Return toohello Azure Government Portal, and complete hello following steps:</span></span>
    
    1. <span data-ttu-id="3bdff-182">StorSimple Yöneticisi hizmet tooaccess hello çift **Hızlı Başlangıç** sayfası.</span><span class="sxs-lookup"><span data-stu-id="3bdff-182">Double-click your StorSimple Manager service tooaccess hello **Quick Start** page.</span></span>
    2. <span data-ttu-id="3bdff-183">**Bağlı cihazları görüntüle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="3bdff-183">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="3bdff-184">Merhaba üzerinde **aygıtları** sayfasında, bu hello cihaz başarıyla bağlandı toohello hizmet hello durumu arayarak doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3bdff-184">On hello **Devices** page, verify that hello device has successfully connected toohello service by looking up hello status.</span></span> <span data-ttu-id="3bdff-185">Merhaba Aygıt durumu olmalıdır **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="3bdff-185">hello device status should be **Online**.</span></span>
       
        ![StorSimple Cihazları sayfası](./media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        <span data-ttu-id="3bdff-187">Merhaba cihaz durumu ise **çevrimdışı**, birkaç dakika hello cihaz çevrimiçi toocome için bekleyin.</span><span class="sxs-lookup"><span data-stu-id="3bdff-187">If hello device status is **Offline**, wait for a couple of minutes for hello device toocome online.</span></span> 
       
        <span data-ttu-id="3bdff-188">Hello aygıt hala çevrimdışı sonra birkaç dakika sonra toomake güvenlik duvarı ağınızın açıklandığı şekilde yapılandırıldığından emin ihtiyacınız [ağ gereksinimleri, StorSimple cihazınız için](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="3bdff-188">If hello device is still offline after a few minutes, then you need toomake sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span> 
       
        <span data-ttu-id="3bdff-189">Bu hello hizmet veri yolu tarafından StorSimple Yöneticisi hizmet-cihaz iletişimi için kullanılan gibi 9354 bağlantı noktasının giden iletişim için açık olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="3bdff-189">Verify that port 9354 is open for outbound communication as this is used by hello service bus for StorSimple Manager service-to-device communication.</span></span>

