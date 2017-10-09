<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="a630b-101">toodownload düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="a630b-101">toodownload hotfixes</span></span>
<span data-ttu-id="a630b-102">Adımları toodownload hello yazılım güncelleştirmesi aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="a630b-102">Perform hello following steps toodownload hello software update.</span></span>

1. <span data-ttu-id="a630b-103">Internet Explorer'ı başlatın ve çok gidin[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a630b-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="a630b-104">Bu bilgisayarda Microsoft Update Kataloğu hello kullanarak ilk kez olursa **yükleme** zaman istendiğinde tooinstall hello Microsoft Update Kataloğu eklentisi.</span><span class="sxs-lookup"><span data-stu-id="a630b-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="a630b-105">![Katalog yükleyin](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="a630b-105">![Install catalog](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="a630b-106">Merhaba arama kutusuna hello Microsoft Update Kataloğu hello Bilgi Bankası (KB) numarasını girin hello düzeltme toodownload, örneğin istediğiniz **3063418**ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="a630b-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3063418**, and then click **Search**.</span></span>
4. <span data-ttu-id="a630b-107">Merhaba görürsünüz **StorSimple güncelleştirme 1.2 Gereci güncelleştirme** paket.</span><span class="sxs-lookup"><span data-stu-id="a630b-107">You will see hello **StorSimple Update 1.2 Appliance Update** bundle.</span></span> <span data-ttu-id="a630b-108">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a630b-108">Click **Add**.</span></span> <span data-ttu-id="a630b-109">Merhaba güncelleştirme toohello Sepeti eklenir.</span><span class="sxs-lookup"><span data-stu-id="a630b-109">hello update will be added toohello basket.</span></span>
5. <span data-ttu-id="a630b-110">Ek düzeltmeleri arayın hello yukarıdaki tabloda listelenen (**3043005** ve **3063416**) ve her hello Sepeti ekleyin.</span><span class="sxs-lookup"><span data-stu-id="a630b-110">Search for any additional hotfixes listed in hello table above (**3043005** and **3063416**), and add each hello basket.</span></span>
6. <span data-ttu-id="a630b-111">**Sepeti Görüntüle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a630b-111">Click **View Basket**.</span></span>
   
    ![Sepeti görüntüle](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. <span data-ttu-id="a630b-113">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a630b-113">Click **Download**.</span></span> <span data-ttu-id="a630b-114">Belirtin veya **Gözat** tooa yerel konum istediğiniz hello tooappear indirir.</span><span class="sxs-lookup"><span data-stu-id="a630b-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="a630b-115">Merhaba güncelleştirmelerin yükleneceği toohello konumu belirtilen ve alt hello hello update ile aynı ad ile yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a630b-115">hello updates are downloaded toohello specified location and placed in a subfolder with hello same name as hello update.</span></span> <span data-ttu-id="a630b-116">Merhaba klasör de hello aygıttan ulaşılabilir kopyalanan tooa ağ paylaşımı olabilir.</span><span class="sxs-lookup"><span data-stu-id="a630b-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="a630b-117">Merhaba düzeltmeleri hello eş denetleyicisinden olası tüm hata iletilerini hem denetleyicileri toodetect erişilebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a630b-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="a630b-118">tooinstall ve normal modu düzeltmeleri doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a630b-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="a630b-119">Aşağıdaki adımları tooinstall hello gerçekleştirmek ve hello normal modu düzeltmeleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a630b-119">Perform hello following steps tooinstall and verify hello regular-mode hotfixes.</span></span> <span data-ttu-id="a630b-120">Bunları zaten yüklü değilse Azure Portal hello kullanarak İleri çok atlayabilirsiniz[yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="a630b-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="a630b-121">StorSimple cihaz seri konsoluna erişim hello Windows PowerShell arabiriminde tooinstall hello yazılım güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="a630b-121">tooinstall hello software update, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="a630b-122">İzleyin hello ayrıntılı yönergeleri [kullanım PuTTy tooconnect toohello seri konsol](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="a630b-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="a630b-123">Merhaba komut isteminde basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="a630b-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="a630b-124">Seçin **seçeneği 1** toolog toohello aygıtta tam erişime sahip.</span><span class="sxs-lookup"><span data-stu-id="a630b-124">Select **Option 1** toolog on toohello device with full access.</span></span>
3. <span data-ttu-id="a630b-125">tooinstall hello güncelleştirme paketi, hello komut istemine yazın:</span><span class="sxs-lookup"><span data-stu-id="a630b-125">tooinstall hello update package, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="a630b-126">Yukarıdaki komut hello paylaşım yolunda DNS yerine IP kullanın.</span><span class="sxs-lookup"><span data-stu-id="a630b-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="a630b-127">yalnızca kimliği doğrulanmış bir paylaşım erişiyorsanız hello kimlik bilgisi parametresi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a630b-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="a630b-128">Merhaba kimlik bilgisi parametresi tooaccess paylaşımları kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="a630b-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="a630b-129">Çok "herkes" genellikle açık edilen bile paylaşımları toounauthenticated kullanıcılar açabilir değil.</span><span class="sxs-lookup"><span data-stu-id="a630b-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="a630b-130">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a630b-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="a630b-131">Tür **Y** zaman istendiğinde tooconfirm hello düzeltme yükleme.</span><span class="sxs-lookup"><span data-stu-id="a630b-131">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
5. <span data-ttu-id="a630b-132">Hello kullanarak hello güncelleştirme izleyin `Get-HcsUpdateStatus` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a630b-132">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="a630b-133">Merhaba aşağıdaki örnek çıkış hello güncelleştirme göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="a630b-133">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="a630b-134">Merhaba `RunInprogress` olacaktır `True` zaman hello güncelleştirme devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="a630b-134">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="a630b-135">örnek çıktı aşağıdaki hello bu hello güncelleştirme tamamlandığında gösterir.</span><span class="sxs-lookup"><span data-stu-id="a630b-135">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="a630b-136">Merhaba `RunInProgress` olacaktır `False` zaman hello güncelleştirmesi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="a630b-136">hello `RunInProgress` will be `False` when hello update has completed.</span></span>

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a630b-137">Bazen, cmdlet raporları'nı hello `False` hello güncelleştirme devam ederken olduğunda.</span><span class="sxs-lookup"><span data-stu-id="a630b-137">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="a630b-138">Düzeltme hello tooensure tamamlandığında, birkaç dakika bekleyin, bu komutu yeniden çalıştırın ve bu hello doğrulayın `RunInProgress` olan `False`.</span><span class="sxs-lookup"><span data-stu-id="a630b-138">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="a630b-139">İse, hello düzeltme tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="a630b-139">If it is, then hello hotfix has completed.</span></span>
   > 
   > 
6. <span data-ttu-id="a630b-140">Merhaba yazılım güncelleştirmesi tamamlandıktan sonra hello sistem yazılım sürümleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a630b-140">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="a630b-141">Merhaba aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="a630b-141">Type hello following command:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="a630b-142">Sürümleri aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="a630b-142">You should see hello following versions:</span></span>
   
   * <span data-ttu-id="a630b-143">HcsSoftwareVersion: 6.3.9600.17584</span><span class="sxs-lookup"><span data-stu-id="a630b-143">HcsSoftwareVersion: 6.3.9600.17584</span></span>
   * <span data-ttu-id="a630b-144">CisAgentVersion: 1.0.9049.0</span><span class="sxs-lookup"><span data-stu-id="a630b-144">CisAgentVersion: 1.0.9049.0</span></span>
   * <span data-ttu-id="a630b-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="a630b-145">MdsAgentVersion: 26.0.4696.1433</span></span>
     
     <span data-ttu-id="a630b-146">Merhaba sürüm numaralarını hello güncelleştirmeyi uyguladıktan sonra değiştirmezseniz bu hello düzeltme tooapply başarısız oldu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a630b-146">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="a630b-147">Bunu görmeniz durumunda daha fazla yardım için lütfen [Microsoft Desteği](../articles/storsimple/storsimple-contact-microsoft-support.md)’ne başvurun.</span><span class="sxs-lookup"><span data-stu-id="a630b-147">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
7. <span data-ttu-id="a630b-148">3-5 tooinstall hello normal modu düzeltme (KB3043005) kalan adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="a630b-148">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfix (KB3043005).</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="a630b-149">tooinstall ve Bakım modu düzeltmeleri doğrulayın</span><span class="sxs-lookup"><span data-stu-id="a630b-149">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="a630b-150">KB3063416 tooinstall disk Bellenim güncelleştirmeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="a630b-150">Use KB3063416 tooinstall disk firmware updates.</span></span> <span data-ttu-id="a630b-151">Bunlar kesintiye uğratan güncelleştirmeleri ve 30-45 dakika toocomplete alın.</span><span class="sxs-lookup"><span data-stu-id="a630b-151">These are disruptive updates and take around 30-45 minutes toocomplete.</span></span> <span data-ttu-id="a630b-152">Bağlantı toohello cihaz seri Konsolu tarafından bu planlı bakım penceresinde tooinstall seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a630b-152">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="a630b-153">tooinstall hello disk Bellenim güncelleştirmeleri aşağıdaki hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="a630b-153">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="a630b-154">Merhaba aygıt bakım moduna.</span><span class="sxs-lookup"><span data-stu-id="a630b-154">Place hello device in Maintenance mode.</span></span> <span data-ttu-id="a630b-155">Windows PowerShell uzaktan iletişimini tooa aygıt, Bakım modunda bağlanırken kullanmaması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a630b-155">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="a630b-156">Bu cmdlet hello cihaz seri konsol üzerinden bağlandığında hello aygıt denetleyicisinde toorun gerekir.</span><span class="sxs-lookup"><span data-stu-id="a630b-156">You will need toorun this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="a630b-157">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="a630b-157">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="a630b-158">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a630b-158">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="a630b-159">Hem hello denetleyicileri bakım moduna ardından yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="a630b-159">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="a630b-160">tooinstall hello disk üretici yazılımı güncelleştirmesi, türü:</span><span class="sxs-lookup"><span data-stu-id="a630b-160">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="a630b-161">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a630b-161">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="a630b-162">İzleyici hello yükleme ilerleme durumu kullanarak `Get-HcsUpdateStatus` komutu.</span><span class="sxs-lookup"><span data-stu-id="a630b-162">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="a630b-163">Merhaba güncelleştirme hello zaman tamamlandıktan `RunInProgress` çok değişiklikleri`False`.</span><span class="sxs-lookup"><span data-stu-id="a630b-163">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="a630b-164">Merhaba yüklemesi tamamlandıktan sonra hello Bakım modu düzeltme yüklü olduğu hello denetleyicisi yeniden başlatılacak.</span><span class="sxs-lookup"><span data-stu-id="a630b-164">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed will be rebooted.</span></span> <span data-ttu-id="a630b-165">Seçenek 1 tam erişime sahip olarak oturum açın ve hello disk bellenim sürümü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="a630b-165">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="a630b-166">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="a630b-166">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="a630b-167">Merhaba beklenen disk bellenim sürümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a630b-167">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   <span data-ttu-id="a630b-168">Merhaba çalıştırmak `Get-HcsFirmwareVersion` , yazılım sürümü hello hello ikinci denetleyicisi tooverify komutunda güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a630b-168">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="a630b-169">Ardından hello Bakım modu çıkabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a630b-169">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="a630b-170">Merhaba komutu her aygıt denetleyicisi için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="a630b-170">Type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="a630b-171">Bakım modu çıktığınızda hello denetleyicilerini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="a630b-171">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="a630b-172">Sonra Hello disk Bellenim güncelleştirmeleri başarıyla uygulandıktan ve hello aygıt Bakım modu, dönüş toohello Klasik Azure portalı çıkıldı.</span><span class="sxs-lookup"><span data-stu-id="a630b-172">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="a630b-173">Merhaba portalınız hello Bakım modu güncelleştirmeleri 24 saat için yüklü gösterilmeyebilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="a630b-173">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

