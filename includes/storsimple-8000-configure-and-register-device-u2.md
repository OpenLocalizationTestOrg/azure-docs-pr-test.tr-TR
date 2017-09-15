<!--author=alkohli last changed: 01/18/2017-->


#### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="b75b0-101">Cihazı yapılandırmak ve kaydetmek için</span><span class="sxs-lookup"><span data-stu-id="b75b0-101">To configure and register the device</span></span>

1. <span data-ttu-id="b75b0-102">StorSimple cihazı seri konsolunuzdaki Windows PowerShell arabirimine erişin.</span><span class="sxs-lookup"><span data-stu-id="b75b0-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="b75b0-103">Talimatlar için bkz. [Cihaz seri konsoluna bağlanmak için PuTTY kullanma](#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="b75b0-103">See [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="b75b0-104">**Yordamı hatasız takip ettiğinizden emin olun; aksi taktirde konsola erişemezsiniz.**</span><span class="sxs-lookup"><span data-stu-id="b75b0-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>

2. <span data-ttu-id="b75b0-105">Açılan oturumda komut istemi almak için bir kez **Enter** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-105">In the session that opens up, press **Enter** one time to get a command prompt.</span></span>

3. <span data-ttu-id="b75b0-106">Cihazınızda ayarlamak istediğiniz dili seçmeniz istenecektir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="b75b0-107">Dili belirtip **Enter** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-107">Specify the language, and then press **Enter**.</span></span>

4. <span data-ttu-id="b75b0-108">Verilen seri konsol menüsünde **tam erişimle oturum açmak** için 1 seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="b75b0-108">In the serial console menu that is presented, choose option 1 to **log in with full access**.</span></span>
     <span data-ttu-id="b75b0-109">Cihazınız için en düşük gerekli ağ ayarlarını yapılandırmak için 5-12 arası adımları tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-109">Complete steps 5-12 to configure the minimum required network settings for your device.</span></span> <span data-ttu-id="b75b0-110">**Bu yapılandırma adımları, cihazın etkin denetleyicisinde gerçekleştirilmelidir.**</span><span class="sxs-lookup"><span data-stu-id="b75b0-110">**These configuration steps need to be performed on the active controller of the device.**</span></span> <span data-ttu-id="b75b0-111">Seri konsol menüsü, bant iletisindeki denetleyici durumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-111">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="b75b0-112">Etkin denetleyiciye bağlı değilseniz, bağlantıyı kesip etkin denetleyiciye bağlayın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-112">If you are not connected to the active controller, disconnect and then connect to the active controller.</span></span>

5. <span data-ttu-id="b75b0-113">Komut istemine parolanızı yazın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-113">At the command prompt, type your password.</span></span> <span data-ttu-id="b75b0-114">Varsayılan cihaz parolası **Password1**’dir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-114">The default device password is **Password1**.</span></span>

6. <span data-ttu-id="b75b0-115">Şu komutu yazın: `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="b75b0-115">Type the following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="b75b0-116">Cihazın ağ ayarlarını yapılandırmanıza yardımcı olacak bir kurulum sihirbazı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-116">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="b75b0-117">Aşağıdaki bilgileri verin:</span><span class="sxs-lookup"><span data-stu-id="b75b0-117">Supply the the following information:</span></span>
   
   * <span data-ttu-id="b75b0-118">DATA 0 ağ arabirimi için IP adresi</span><span class="sxs-lookup"><span data-stu-id="b75b0-118">IP address for the DATA 0 network interface</span></span>
   * <span data-ttu-id="b75b0-119">Alt ağ maskesi</span><span class="sxs-lookup"><span data-stu-id="b75b0-119">Subnet mask</span></span>
   * <span data-ttu-id="b75b0-120">Ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="b75b0-120">Gateway</span></span>
   * <span data-ttu-id="b75b0-121">Birincil DNS sunucusu için IP adresi</span><span class="sxs-lookup"><span data-stu-id="b75b0-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="b75b0-122">Aşağıda örnek bir çıktı sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="b75b0-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Active
        ---------------------------------------------------------------

        Your device needs to be registered with the Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' to set up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like to configure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="b75b0-123">Yukarıdaki örnek çıktıda, işlemin her adımından sonra sistemin ağ ayarlarını doğruladığını görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b75b0-123">In the preceding sample output, you can see that the system is validating network settings after each step in the process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b75b0-124">Uygulanacak alt ağ maskesi ve DNS ayarları için dakika beklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-124">You may have to wait for a few minutes for the subnet mask and the DNS settings to be applied.</span></span> <span data-ttu-id="b75b0-125">“Data 0 ağ bağlantısını denetleyin” hata iletisi alırsanız, etkin denetleyicinizin DATA 0 ağ arabirimindeki fiziksel ağ bağlantısını işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="b75b0-125">If you get a "Check the network connectivity to Data 0" error message, check the physical network connection on the DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="b75b0-126">(İsteğe bağlı), web ara sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="b75b0-127">Web ara sunucusunun yapılandırması isteğe bağlı olsa **bir web ara sunucu kullanıyorsanız, burada yalnızca bunu yapılandırabileceğinizi unutmayın**.</span><span class="sxs-lookup"><span data-stu-id="b75b0-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="b75b0-128">Daha fazla bilgi için [Cihazınız için web ara sunucusunu yapılandırma](../articles/storsimple/storsimple-8000-configure-web-proxy.md)’ya gidin.</span><span class="sxs-lookup"><span data-stu-id="b75b0-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="b75b0-129">Cihazınız için Birincil NTP sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="b75b0-130">Bulut hizmeti sağlayıcılarıyla doğrulanabileceği şekilde cihazınızı saati eşitlemesi gerektiğinden NTP sunucuları gereklidir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="b75b0-131">Ağınızın, NTP trafiğini veri merkezinizden İnternete geçirilmesine izin vermesini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-131">Ensure that your network allows NTP traffic to pass from your datacenter to the Internet.</span></span> <span data-ttu-id="b75b0-132">Bu yapılamıyorsa dahili bir NTP sunucusu belirtin.</span><span class="sxs-lookup"><span data-stu-id="b75b0-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="b75b0-133">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-133">A sample output is shown below.</span></span>

    ```
        Would you like to configure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="b75b0-134">Güvenlik nedenleriyle, cihaz yönetici parolasının süresi ilk oturumun ardından dolar; artık bunu değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-134">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="b75b0-135">İstendiğinde cihaz yöneticisi parolasını verin.</span><span class="sxs-lookup"><span data-stu-id="b75b0-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="b75b0-136">Geçerli bir cihaz yöneticisi parolası 8-15 karakter arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b75b0-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="b75b0-137">Parolada aşağıdakilerden üçü olmalıdır: küçük harf, büyük harf, rakam ve özel karakter.</span><span class="sxs-lookup"><span data-stu-id="b75b0-137">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        The device administrator password must be between 8 and 15 characters. The password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="b75b0-138">Kurulum sihirbazının son adımı cihazınızı StorSimple Cihaz Yöneticisi hizmetine kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b75b0-138">The final step in the setup wizard registers your device with the StorSimple Device Manager service.</span></span> <span data-ttu-id="b75b0-139">Bunun için, 2. adımda aldığınız hizmet kayıt anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-139">For this, you will need the service registration key that you obtained in step 2.</span></span> <span data-ttu-id="b75b0-140">Kayıt anahtarını verdikten sonra cihazın kaydolması için 2-3 dakika beklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-140">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="b75b0-141">Kurulum sihirbazından çıkmak için istediğiniz zaman Ctrl + C tuşlarına basabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b75b0-141">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="b75b0-142">Tüm ağ ayarlarını (Data 0 için IP adresi, alt ağ maskesi ve ağ geçidi) girdiyseniz girişleriniz korunur.</span><span class="sxs-lookup"><span data-stu-id="b75b0-142">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="b75b0-143">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-143">A sample output is shown below.</span></span>

    ```
        The service registration key is available in the StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="b75b0-144">Cihaz kaydedildikten sonra Hizmet Verileri Şifreleme anahtarı görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-144">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="b75b0-145">Bu anahtarı kopyalayın ve güvenli bir konuma kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b75b0-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="b75b0-146">**StorSimple Cihaz Yöneticisi hizmetiyle ek cihazlar kaydetmek için hizmet kayıt anahtarıyla birlikte bu anahtar da gerekecektir.**</span><span class="sxs-lookup"><span data-stu-id="b75b0-146">**This key will be required with the service registration key to register additional devices with the StorSimple Device Manager service.**</span></span> <span data-ttu-id="b75b0-147">Bu anahtar hakkında daha fazla bilgi için bkz. [StorSimple güvenliği](../articles/storsimple/storsimple-security.md).</span><span class="sxs-lookup"><span data-stu-id="b75b0-147">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple kayıt cihazı 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="b75b0-149">Seri konsol penceresinden metin kopyalamak için metni seçmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-149">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="b75b0-150">Artık bunu panoya veya metin düzenleyicilere yapıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b75b0-150">You should then be able to paste it in the clipboard or any text editor.</span></span> <span data-ttu-id="b75b0-151">Hizmet verileri şifreleme anahtarını kopyalamak için CTRL + C tuşlarını kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-151">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="b75b0-152">Ctrl + C tuşlarının kullanılması kurulum sihirbazından çıkmanıza neden olur.</span><span class="sxs-lookup"><span data-stu-id="b75b0-152">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="b75b0-153">Sonuç olarak, cihaz yöneticisi parolası değiştirilmez ve cihaz varsayılan parolasına döner.</span><span class="sxs-lookup"><span data-stu-id="b75b0-153">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    
13. <span data-ttu-id="b75b0-154">Seri konsoldan çıkın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-154">Exit the serial console.</span></span>
14. <span data-ttu-id="b75b0-155">Azure portalına dönün ve aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="b75b0-155">Return to the Azure portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="b75b0-156">StorSimple Cihaz Yöneticisi hizmetinize gidin.</span><span class="sxs-lookup"><span data-stu-id="b75b0-156">Go to your StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="b75b0-157">**Cihazlar**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="b75b0-158">Cihazların tablosal listesinde cihazın durumunu arayarak cihazın hizmete sorunsuz bir şekilde bağlandığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-158">In the tabular listing of devices, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="b75b0-159">Cihazın durumu **Kuruluma hazır** olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b75b0-159">The device status should be **Ready to set up**.</span></span>
       
        ![StorSimple Cihazları sayfası](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="b75b0-161">Cihaz durumunun **Kuruluma hazır** hale gelmesi için birkaç dakika beklemeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="b75b0-161">You may need to wait for a couple of minutes for the device status to change to **Ready to set up**.</span></span>
       
        <span data-ttu-id="b75b0-162">Cihaz bu listede görünmüyorsa, güvenlik duvarı ağınızın [StorSimple cihazınız için ağ gereksinimlerinde](../articles/storsimple/storsimple-8000-system-requirements.md) açıklandığı şekilde yapılandırıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="b75b0-162">If the device does not show up in this list, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="b75b0-163">StorSimple Cihaz Yöneticisi hizmeti ile cihazlar arasındaki iletişim için hizmet veri yolu tarafından kullanılan 9354 bağlantı noktasının giden iletişim için açık olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="b75b0-163">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Device Manager service-to-device communication.</span></span>

