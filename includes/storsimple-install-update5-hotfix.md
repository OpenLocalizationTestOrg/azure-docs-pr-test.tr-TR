<!--author=alkohli last changed: 08/21/17-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="bedec-101">toodownload düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="bedec-101">toodownload hotfixes</span></span>

<span data-ttu-id="bedec-102">Hello Microsoft Update Kataloğu ' adımları toodownload hello yazılım güncelleştirmesi aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="bedec-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="bedec-103">Internet Explorer'ı başlatın ve çok gidin[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="bedec-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="bedec-104">Bu bilgisayarda Microsoft Update Kataloğu hello kullanarak ilk kez olursa **yükleme** zaman istendiğinde tooinstall hello Microsoft Update Kataloğu eklentisi.</span><span class="sxs-lookup"><span data-stu-id="bedec-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>

    ![Katalog yükleme](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="bedec-106">Merhaba arama kutusuna hello Microsoft Update Kataloğu hello Bilgi Bankası (KB) numarasını girin hello düzeltme toodownload, örneğin istediğiniz **4037264**ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="bedec-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="bedec-107">Merhaba düzeltme listesi, örneğin, göründüğünde **StorSimple 8000 serisi için toplu yazılım paketini güncelleştirme 5.0**.</span><span class="sxs-lookup"><span data-stu-id="bedec-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![Katalogda arama](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="bedec-109">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bedec-109">Click **Download**.</span></span> <span data-ttu-id="bedec-110">Belirtin veya **Gözat** tooa yerel konum istediğiniz hello tooappear indirir.</span><span class="sxs-lookup"><span data-stu-id="bedec-110">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="bedec-111">Merhaba dosyaları toodownload toohello belirtilen konuma ve klasör.</span><span class="sxs-lookup"><span data-stu-id="bedec-111">Click hello files toodownload toohello specified location and folder.</span></span> <span data-ttu-id="bedec-112">Merhaba klasör de hello aygıttan ulaşılabilir kopyalanan tooa ağ paylaşımı olabilir.</span><span class="sxs-lookup"><span data-stu-id="bedec-112">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>
5. <span data-ttu-id="bedec-113">Ek düzeltmeleri arayın hello yukarıdaki tabloda listelenen (**4037266**), ve indirme hello karşılık gelen dosyaları belirli klasörleri toohello tablo önceki hello listelendiği gibi.</span><span class="sxs-lookup"><span data-stu-id="bedec-113">Search for any additional hotfixes listed in hello table above (**4037266**), and download hello corresponding files toohello specific folders as listed in hello preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="bedec-114">Merhaba düzeltmeleri hello eş denetleyicisinden olası tüm hata iletilerini hem denetleyicileri toodetect erişilebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="bedec-114">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
>
> <span data-ttu-id="bedec-115">Merhaba düzeltmeleri 3 ayrı klasörlerde kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="bedec-115">hello hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="bedec-116">Örneğin, hello aygıt CIS/software/MDS aracı güncelleştirmesi içinde kopyalanabilir _FirstOrderUpdate_ klasörü, tüm hello benzer diğer güncelleştirmeleri hello kopyalanamadı _SecondOrderUpdate_ klasörü, ve Bakım modu güncelleştirmeleri içinde kopyalanan _ThirdOrderUpdate_ klasör.</span><span class="sxs-lookup"><span data-stu-id="bedec-116">For example, hello device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all hello other non-disruptive updates could be copied in hello _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="bedec-117">tooinstall ve normal modu düzeltmeleri doğrulayın</span><span class="sxs-lookup"><span data-stu-id="bedec-117">tooinstall and verify regular mode hotfixes</span></span>

<span data-ttu-id="bedec-118">Aşağıdaki adımları tooinstall hello gerçekleştirmek ve normal modu düzeltmeleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bedec-118">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="bedec-119">Bunları zaten yüklü değilse Azure portal hello kullanarak İleri çok atlayabilirsiniz[yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="bedec-119">If you already installed them using hello Azure portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="bedec-120">tooinstall hello düzeltmeleri, StorSimple cihaz seri konsoluna erişim hello Windows PowerShell arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="bedec-120">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="bedec-121">İzleyin hello ayrıntılı yönergeleri [kullanım PuTTy tooconnect toohello seri konsol](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="bedec-121">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="bedec-122">Merhaba komut isteminde basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="bedec-122">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="bedec-123">Seçin **seçeneği 1** toolog toohello aygıtta tam erişime sahip.</span><span class="sxs-lookup"><span data-stu-id="bedec-123">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="bedec-124">Hello düzeltmeyi hello pasif denetleyicisinde ilk yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="bedec-124">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="bedec-125">Merhaba komut isteminde türü tooinstall hello düzeltme:</span><span class="sxs-lookup"><span data-stu-id="bedec-125">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="bedec-126">Yukarıdaki komut hello paylaşım yolunda DNS yerine IP kullanın.</span><span class="sxs-lookup"><span data-stu-id="bedec-126">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="bedec-127">yalnızca kimliği doğrulanmış bir paylaşım erişiyorsanız hello kimlik bilgisi parametresi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bedec-127">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="bedec-128">Merhaba kimlik bilgisi parametresi tooaccess paylaşımları kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="bedec-128">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="bedec-129">Çok "herkes" genellikle açık edilen bile paylaşımları toounauthenticated kullanıcılar açabilir değil.</span><span class="sxs-lookup"><span data-stu-id="bedec-129">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
4. <span data-ttu-id="bedec-130">İstendiğinde hello parolasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="bedec-130">Supply hello password when prompted.</span></span> <span data-ttu-id="bedec-131">Merhaba ilk sipariş güncelleştirmeleri yüklemek için örnek bir çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bedec-131">A sample output for installing hello first order updates is shown below.</span></span> <span data-ttu-id="bedec-132">Merhaba ilk sipariş güncelleştirmesi toopoint toohello belirli dosya gerekir.</span><span class="sxs-lookup"><span data-stu-id="bedec-132">For hello first order update, you need toopoint toohello specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="bedec-133">Merhaba yüklemelidir _HcsSoftwareUpdate.exe_ ilk.</span><span class="sxs-lookup"><span data-stu-id="bedec-133">You should install hello _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="bedec-134">Bu yükleme tamamlandıktan sonra daha sonra yüklemek _CisMdsAgentUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="bedec-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="bedec-135">Tür **Y** zaman istendiğinde tooconfirm hello düzeltme yükleme.</span><span class="sxs-lookup"><span data-stu-id="bedec-135">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
6. <span data-ttu-id="bedec-136">Hello kullanarak hello güncelleştirme izleyin `Get-HcsUpdateStatus` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bedec-136">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="bedec-137">Hello güncelleştirme hello pasif denetleyicisinde önce tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="bedec-137">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="bedec-138">Merhaba pasif denetleyici güncelleştirildikten sonra bir yük devretme olacaktır ve hello güncelleştirme sonra üzerinde uygulanacağını diğer denetleyicisi hello.</span><span class="sxs-lookup"><span data-stu-id="bedec-138">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="bedec-139">hem hello denetleyicileri güncelleştirildiğinde hello güncelleştirme tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="bedec-139">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="bedec-140">Merhaba aşağıdaki örnek çıkış hello güncelleştirme göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="bedec-140">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="bedec-141">Merhaba `RunInprogress` olan `True` zaman hello güncelleştirme devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="bedec-141">hello `RunInprogress` is `True` when hello update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="bedec-142">örnek çıktı aşağıdaki hello bu hello güncelleştirme tamamlandığında gösterir.</span><span class="sxs-lookup"><span data-stu-id="bedec-142">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="bedec-143">Merhaba `RunInProgress` olan `False` hello güncelleştirme tamamlandığında.</span><span class="sxs-lookup"><span data-stu-id="bedec-143">hello `RunInProgress` is `False` when hello update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="bedec-144">Bazen, cmdlet raporları'nı hello `False` hello güncelleştirme devam ederken olduğunda.</span><span class="sxs-lookup"><span data-stu-id="bedec-144">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="bedec-145">Düzeltme hello tooensure tamamlandığında, birkaç dakika bekleyin, bu komutu yeniden çalıştırın ve bu hello doğrulayın `RunInProgress` olan `False`.</span><span class="sxs-lookup"><span data-stu-id="bedec-145">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="bedec-146">İse, hello düzeltme tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="bedec-146">If it is, then hello hotfix has completed.</span></span>

7. <span data-ttu-id="bedec-147">Merhaba yazılım güncelleştirmesi tamamlandıktan sonra hello sistem yazılım sürümleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bedec-147">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="bedec-148">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="bedec-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="bedec-149">Sürümleri aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="bedec-149">You should see hello following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="bedec-150">Merhaba sürüm numarası değişmez hello güncelleştirmeyi uyguladıktan sonra o hello düzeltme tooapply başarısız oldu gösterir.</span><span class="sxs-lookup"><span data-stu-id="bedec-150">If hello version number does not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="bedec-151">Bunu görmeniz durumunda daha fazla yardım için lütfen [Microsoft Desteği](../articles/storsimple/storsimple-8000-contact-microsoft-support.md)’ne başvurun.</span><span class="sxs-lookup"><span data-stu-id="bedec-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="bedec-152">Merhaba etkin denetleyicisi hello aracılığıyla yeniden başlatmanız gerekir `Restart-HcsController` uygulamadan önce cmdlet hello sonraki güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="bedec-152">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello next update.</span></span>
     
8. <span data-ttu-id="bedec-153">Tooinstall hello 3 ile 6 arasındaki adımları yineleyin _CisMDSAgentupdate.exe_ Aracısı indirilen tooyour _FirstOrderUpdate_ klasör.</span><span class="sxs-lookup"><span data-stu-id="bedec-153">Repeat steps 3-6 tooinstall hello _CisMDSAgentupdate.exe_ agent downloaded tooyour _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="bedec-154">Adım 3-6 tooinstall hello ikinci sipariş güncelleştirmeleri yineleyin.</span><span class="sxs-lookup"><span data-stu-id="bedec-154">Repeat steps 3-6 tooinstall hello second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="bedec-155">İkinci sipariş güncelleştirmeleri hello çalıştırarak birden çok güncelleştirme yüklenebilir `Start-HcsHotfix cmdlet` ve ikinci sipariş güncelleştirmeleri bulunduğu toohello klasörünü işaret.</span><span class="sxs-lookup"><span data-stu-id="bedec-155">For second order updates, multiple updates can be installed by just running hello `Start-HcsHotfix cmdlet` and pointing toohello folder where second order updates are located.</span></span> <span data-ttu-id="bedec-156">Merhaba cmdlet'i tüm hello güncelleştirmelere hello klasöründe yürütülür.</span><span class="sxs-lookup"><span data-stu-id="bedec-156">hello cmdlet will execute all hello updates available in hello folder.</span></span> <span data-ttu-id="bedec-157">Bir güncelleştirmeyi zaten yüklediyseniz, hello güncelleştirme mantığı algılayan ve bu güncelleştirmenin geçerli değil.</span><span class="sxs-lookup"><span data-stu-id="bedec-157">If an update is already installed, hello update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="bedec-158">Tüm hello düzeltmeleri yüklendikten sonra hello kullanılacak `Get-HcsSystem` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="bedec-158">After all hello hotfixes are installed, use hello `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="bedec-159">Merhaba sürümleri olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="bedec-159">hello versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="bedec-160">tooinstall ve Bakım modu düzeltmeleri doğrulayın</span><span class="sxs-lookup"><span data-stu-id="bedec-160">tooinstall and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="bedec-161">KB4037263 tooinstall disk Bellenim güncelleştirmeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="bedec-161">Use KB4037263 tooinstall disk firmware updates.</span></span> <span data-ttu-id="bedec-162">Bunlar kesintiye uğratan güncelleştirmeleri ve yaklaşık 30 dakika toocomplete alın.</span><span class="sxs-lookup"><span data-stu-id="bedec-162">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="bedec-163">Bağlantı toohello cihaz seri Konsolu tarafından bu planlı bakım penceresinde tooinstall seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bedec-163">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="bedec-164">Disk bellenim zaten güncel ise, bu güncelleştirmeleri tooinstall gerekmez.</span><span class="sxs-lookup"><span data-stu-id="bedec-164">If your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="bedec-165">Merhaba çalıştırmak `Get-HcsUpdateAvailability` güncelleştirmeleri kullanılabilir ve olup hello hello cihaz seri konsoluna toocheck cmdlet'inden güncelleştirmeleri olan kesintiye uğratan (Bakım modu) veya benzer (normal modu) güncelleştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="bedec-165">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="bedec-166">tooinstall hello disk Bellenim güncelleştirmeleri aşağıdaki hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="bedec-166">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="bedec-167">Merhaba aygıt hello bakım moduna.</span><span class="sxs-lookup"><span data-stu-id="bedec-167">Place hello device in hello maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="bedec-168">Windows PowerShell uzaktan iletişimini tooa aygıt, Bakım modunda bağlanırken kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="bedec-168">Do not use Windows PowerShell remoting when connecting tooa device in maintenance mode.</span></span> <span data-ttu-id="bedec-169">Bunun yerine bu cmdlet'i hello cihaz seri konsol üzerinden bağlandığında hello aygıt denetleyicisi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bedec-169">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span>

    <span data-ttu-id="bedec-170">Bakım modunda tooplace hello denetleyicisi yazın:</span><span class="sxs-lookup"><span data-stu-id="bedec-170">tooplace hello controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="bedec-171">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bedec-171">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="bedec-172">Hem hello denetleyicileri bakım moduna ardından yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="bedec-172">Both hello controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="bedec-173">tooinstall hello disk üretici yazılımı güncelleştirmesi, türü:</span><span class="sxs-lookup"><span data-stu-id="bedec-173">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="bedec-174">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bedec-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="bedec-175">İzleyici hello yükleme ilerleme durumu kullanarak `Get-HcsUpdateStatus` komutu.</span><span class="sxs-lookup"><span data-stu-id="bedec-175">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="bedec-176">Merhaba güncelleştirme hello zaman tamamlandıktan `RunInProgress` çok değişiklikleri`False`.</span><span class="sxs-lookup"><span data-stu-id="bedec-176">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="bedec-177">Merhaba yüklemesi tamamlandıktan sonra hangi hello üzerinde Bakım modu düzeltme yüklü hello denetleyicisi yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="bedec-177">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="bedec-178">Seçenek 1 tam erişime sahip olarak oturum açın ve hello disk bellenim sürümü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="bedec-178">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="bedec-179">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="bedec-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="bedec-180">Merhaba beklenen disk bellenim sürümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="bedec-180">hello expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="bedec-181">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bedec-181">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    <span data-ttu-id="bedec-182">Merhaba çalıştırmak `Get-HcsFirmwareVersion` , yazılım sürümü hello hello ikinci denetleyicisi tooverify komutunda güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bedec-182">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="bedec-183">Ardından hello Bakım modu çıkabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bedec-183">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="bedec-184">toodo, bu nedenle, her cihaz denetleyicisi için komutu aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="bedec-184">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="bedec-185">Bakım modu çıktığınızda hello denetleyicilerini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="bedec-185">hello controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="bedec-186">Sonra Hello disk Bellenim güncelleştirmeleri başarıyla uygulandıktan ve hello aygıt Bakım modu, dönüş toohello Azure portal çıkıldı.</span><span class="sxs-lookup"><span data-stu-id="bedec-186">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure portal.</span></span> <span data-ttu-id="bedec-187">Merhaba portalınız hello Bakım modu güncelleştirmeleri 24 saat için yüklü gösterilmeyebilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bedec-187">Note that hello portal might not show that you installed hello maintenance mode updates for 24 hours.</span></span>

