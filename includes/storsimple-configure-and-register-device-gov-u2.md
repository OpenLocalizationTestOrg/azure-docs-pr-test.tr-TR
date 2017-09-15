<!--author=SharS last changed: 02/22/2016-->

### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="c4ff9-101">Cihazı yapılandırmak ve kaydetmek için</span><span class="sxs-lookup"><span data-stu-id="c4ff9-101">To configure and register the device</span></span>
1. <span data-ttu-id="c4ff9-102">StorSimple cihazı seri konsolunuzdaki Windows PowerShell arabirimine erişin.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="c4ff9-103">Talimatlar için bkz. [Cihaz seri konsoluna bağlanmak için PuTTY kullanma](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="c4ff9-103">See [Use PuTTY to connect to the device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="c4ff9-104">**Yordamı hatasız takip ettiğinizden emin olun; aksi taktirde konsola erişemezsiniz.**</span><span class="sxs-lookup"><span data-stu-id="c4ff9-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>
2. <span data-ttu-id="c4ff9-105">Açılan oturumda komut istemi almak için bir kez Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-105">In the session that opens up, press Enter one time to get a command prompt.</span></span>
3. <span data-ttu-id="c4ff9-106">Cihazınızda ayarlamak istediğiniz dili seçmeniz istenecektir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="c4ff9-107">Dili belirtip Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-107">Specify the language, and then press Enter.</span></span>
   
    ![StorSimple cihazı yapılandırma ve kaydetme 1](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="c4ff9-109">Verilen seri konsol menüsünde tam erişimle oturum açmak için 1 seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-109">In the serial console menu that is presented, choose option 1 to log on with full access.</span></span>
   
    ![StorSimple kayıt cihazı 2](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="c4ff9-111">Cihazınız için en düşük gerekli ağ ayarlarını yapılandırmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-111">Perform the following steps to configure the minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="c4ff9-112">Bu yapılandırma adımları, cihazın etkin denetleyicisinde gerçekleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-112">These configuration steps need to be performed on the active controller of the device.</span></span> <span data-ttu-id="c4ff9-113">Seri konsol menüsü, bant iletisindeki denetleyici durumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-113">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="c4ff9-114">Olan değil bağlanırsanız etkin denetleyiciye kesin ve etkin denetleyiciye bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-114">If you are not connect to the active controller, disconnect and then connect to the active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="c4ff9-115">Komut istemine parolanızı yazın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-115">At the command prompt, type your password.</span></span> <span data-ttu-id="c4ff9-116">Varsayılan cihaz parolası **Password1**’dir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-116">The default device password is **Password1**.</span></span>
   2. <span data-ttu-id="c4ff9-117">Aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="c4ff9-117">Type the following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="c4ff9-118">Cihazın ağ ayarlarını yapılandırmanıza yardımcı olacak bir kurulum sihirbazı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-118">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="c4ff9-119">Aşağıdaki bilgileri sağlayın:</span><span class="sxs-lookup"><span data-stu-id="c4ff9-119">Supply the following information:</span></span>
      
      * <span data-ttu-id="c4ff9-120">Veri 0 ağ arabirimi için IP adresi</span><span class="sxs-lookup"><span data-stu-id="c4ff9-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="c4ff9-121">Alt ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="c4ff9-121">Subnet mask</span></span>
      * <span data-ttu-id="c4ff9-122">Ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="c4ff9-122">Gateway</span></span>
      * <span data-ttu-id="c4ff9-123">Birincil DNS sunucusu için IP adresi</span><span class="sxs-lookup"><span data-stu-id="c4ff9-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="c4ff9-124">Birincil NTP sunucusu için IP adresi</span><span class="sxs-lookup"><span data-stu-id="c4ff9-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="c4ff9-125">Alt ağ maskesi ve DNS ayarlarının uygulanması için birkaç dakika beklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-125">You may have to wait for a few minutes for the subnet mask and DNS settings to be applied.</span></span>
      > 
      > 
   4. <span data-ttu-id="c4ff9-126">İsteğe bağlı olarak, web proxy sunucunuzu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="c4ff9-127">Web proxy yapılandırması isteğe bağlı olsa da, bir web proxy kullanıyorsanız, yalnızca burada yapılandırabilirsiniz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="c4ff9-128">Daha fazla bilgi için [Cihazınız için web ara sunucusunu yapılandırma](../articles/storsimple/storsimple-configure-web-proxy.md)’ya gidin.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
      > 
      > 
6. <span data-ttu-id="c4ff9-129">Kurulum sihirbazından çıkmak için Ctrl + C tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-129">Press Ctrl + C to exit the setup wizard.</span></span>
7. <span data-ttu-id="c4ff9-130">Güncelleştirmeleri gibi yükleyin:</span><span class="sxs-lookup"><span data-stu-id="c4ff9-130">Install the updates as follows:</span></span>
   
   1. <span data-ttu-id="c4ff9-131">Her iki denetleyicilerinde IP'leri ayarlamak için aşağıdaki cmdlet'i kullanın:</span><span class="sxs-lookup"><span data-stu-id="c4ff9-131">Use the following cmdlet to set IPs on both the controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="c4ff9-132">Komut istemine `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-132">At the command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="c4ff9-133">Güncelleştirmelerinin kullanılabilir olduğunu bildirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="c4ff9-134">`Start-HcsUpdate` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="c4ff9-135">Herhangi bir düğümde bu komutu çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-135">You can run this command on any node.</span></span> <span data-ttu-id="c4ff9-136">Güncelleştirmeler ilk denetleyicisinde uygulanır, denetleyici üzerinden başarısız olur ve ardından diğer denetleyicisinde güncelleştirmeler uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-136">Updates will be applied on the first controller, the controller will fail over, and then the updates will be applied on the other controller.</span></span>
      
      <span data-ttu-id="c4ff9-137">Çalıştırarak güncelleştirmenin ilerleme durumunu izleyebilirsiniz `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-137">You can monitor the progress of the update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="c4ff9-138">Devam etmekte olan güncelleştirme aşağıdaki örnek çıktıda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-138">The following sample output shows the update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      <span data-ttu-id="c4ff9-139">Aşağıdaki örnek çıktıda güncelleştirmenin tamamlandığı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-139">The following sample output indicates that the update is finished.</span></span>
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      <span data-ttu-id="c4ff9-140">Windows güncelleştirmeleri de dahil olmak üzere tüm güncelleştirmeleri uygulamanızı 11 saate kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-140">It may take up to 11 hours to apply all the updates, including the Windows Updates.</span></span>
8. <span data-ttu-id="c4ff9-141">(Bu ortak Azure Klasik portalında varsayılan işaret ettiğinden) cihaz Microsoft Azure kamu Portalı'na işaret etmek için aşağıdaki cmdlet'i çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-141">Run the following cmdlet to point the device to the Microsoft Azure Government portal (because it points to the public Azure classic portal by default).</span></span> <span data-ttu-id="c4ff9-142">Bu, hem denetleyicileri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-142">This will restart both controllers.</span></span> <span data-ttu-id="c4ff9-143">Her denetleyici ne zaman yeniden görebilmeniz için aynı anda hem denetleyicileri bağlanmak için iki PuTTY oturumu kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-143">We recommend that you use two PuTTY sessions to simultaneously connect to both controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="c4ff9-144">Bir onay iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-144">You will see a confirmation message.</span></span> <span data-ttu-id="c4ff9-145">Varsayılanı kabul (**Y**).</span><span class="sxs-lookup"><span data-stu-id="c4ff9-145">Accept the default (**Y**).</span></span>
9. <span data-ttu-id="c4ff9-146">Kurulum devam etmek için aşağıdaki cmdlet'i çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c4ff9-146">Run the following cmdlet to resume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![Resume Kurulum Sihirbazı](./media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   <span data-ttu-id="c4ff9-148">Kurulum devam edince Sihirbazı'nı güncelleştirme 2 sürümü olacaktır.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-148">When you resume setup, the wizard will be the Update 2 version.</span></span>
10. <span data-ttu-id="c4ff9-149">Ağ ayarlarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-149">Accept the network settings.</span></span> <span data-ttu-id="c4ff9-150">Her ayar kabul ettikten sonra bir doğrulama iletisi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-150">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="c4ff9-151">Güvenlik nedenleriyle, cihaz yönetici parolasının süresi ilk oturumun ardından dolar; artık bunu değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-151">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="c4ff9-152">İstendiğinde cihaz yöneticisi parolasını verin.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-152">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="c4ff9-153">Geçerli bir cihaz yöneticisi parolası 8-15 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-153">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="c4ff9-154">Parolada aşağıdakilerden üçü olmalıdır: küçük harf, büyük harf, rakam ve özel karakter.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-154">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![StorSimple kayıt cihazı 5](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="c4ff9-156">Kurulum sihirbazının son adımı cihazınızı StorSimple Yöneticisi hizmetine kaydeder.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-156">The final step in the setup wizard registers your device with the StorSimple Manager service.</span></span> <span data-ttu-id="c4ff9-157">Bunun için makalesinde aldığınız hizmet kayıt anahtarı gerekir [2. adım: Hizmet kayıt anahtarını alın](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="c4ff9-157">For this, you will need the service registration key that you obtained in [Step 2: Get the service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="c4ff9-158">Kayıt anahtarını verdikten sonra cihazın kaydolması için 2-3 dakika beklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-158">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="c4ff9-159">Kurulum sihirbazından çıkmak için istediğiniz zaman Ctrl + C tuşlarına basabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-159">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="c4ff9-160">Tüm ağ ayarlarını (Data 0 için IP adresi, alt ağ maskesi ve ağ geçidi) girdiyseniz girişleriniz korunur.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-160">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![StorSimple kayıt ilerleme durumu](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="c4ff9-162">Cihaz kaydedildikten sonra Hizmet Verileri Şifreleme anahtarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-162">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="c4ff9-163">Bu anahtarı kopyalayın ve güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-163">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="c4ff9-164">**StorSimple Yöneticisi hizmetiyle ek cihazlar kaydetmek için hizmet kayıt anahtarıyla birlikte bu anahtar da gerekecektir.**</span><span class="sxs-lookup"><span data-stu-id="c4ff9-164">**This key will be required with the service registration key to register additional devices with the StorSimple Manager service.**</span></span> <span data-ttu-id="c4ff9-165">Bu anahtar hakkında daha fazla bilgi için bkz. [StorSimple güvenliği](../articles/storsimple/storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="c4ff9-165">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple kayıt cihazı 7](./media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="c4ff9-167">Seri konsol penceresinden metin kopyalamak için metni seçmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-167">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="c4ff9-168">Artık bunu panoya veya metin düzenleyicilere yapıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-168">You should then be able to paste it in the clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="c4ff9-169">Hizmet verileri şifreleme anahtarını kopyalamak için CTRL + C tuşlarını kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-169">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="c4ff9-170">Ctrl + C tuşlarının kullanılması kurulum sihirbazından çıkmanıza neden olur.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-170">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="c4ff9-171">Sonuç olarak, cihaz yöneticisi parolası değiştirilmez ve cihaz varsayılan parolasına döner.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-171">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    > 
    > 
14. <span data-ttu-id="c4ff9-172">Seri konsoldan çıkın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-172">Exit the serial console.</span></span>
15. <span data-ttu-id="c4ff9-173">Azure Kamu portalına geri dönün ve aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="c4ff9-173">Return to the Azure Government Portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="c4ff9-174">**Hızlı Başlangıç** sayfasına erişmek için StorSimple Yöneticisi hizmetinize çift tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-174">Double-click your StorSimple Manager service to access the **Quick Start** page.</span></span>
    2. <span data-ttu-id="c4ff9-175">**Bağlı cihazları görüntüle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-175">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="c4ff9-176">**Cihazlar** sayfasında, durumu arayarak cihazın hizmete sorunsuz bağlandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-176">On the **Devices** page, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="c4ff9-177">Cihazın durumu **Çevrimiçi** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-177">The device status should be **Online**.</span></span>
       
        ![StorSimple Cihazları sayfası](./media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        <span data-ttu-id="c4ff9-179">Cihazın durumu **Çevrimdışı** olduğu durumda, birkaç dakikada cihazın çevrimiçi olması bekleyin.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-179">If the device status is **Offline**, wait for a couple of minutes for the device to come online.</span></span>
       
        <span data-ttu-id="c4ff9-180">Birkaç dakika sonra cihaz yine de çevrimdışıysa, güvenlik duvarı ağınızın [StorSimple cihazınız için ağ gereksinimlerinde](../articles/storsimple/storsimple-system-requirements.md) açıklandığı şekilde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-180">If the device is still offline after a few minutes, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span>
       
        <span data-ttu-id="c4ff9-181">Bu hizmet veri yolu tarafından StorSimple Yöneticisi Hizmet - Cihaz iletişimi için hizmet veri yolu tarafından kullanıldığından, 9354 bağlantı noktasının giden iletişim için açık olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="c4ff9-181">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Manager Service-to-device communication.</span></span>

