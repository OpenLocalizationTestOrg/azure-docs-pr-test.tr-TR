<!--author=alkohli last changed: 05/19/16-->

#### <a name="toodownload-hotfixes"></a><span data-ttu-id="1ed16-101">toodownload düzeltmeleri</span><span class="sxs-lookup"><span data-stu-id="1ed16-101">toodownload hotfixes</span></span>
<span data-ttu-id="1ed16-102">Hello Microsoft Update Kataloğu ' adımları toodownload hello yazılım güncelleştirmesi aşağıdaki hello gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="1ed16-102">Perform hello following steps toodownload hello software update from hello Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="1ed16-103">Internet Explorer'ı başlatın ve çok gidin[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="1ed16-103">Start Internet Explorer and navigate too[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="1ed16-104">Bu bilgisayarda Microsoft Update Kataloğu hello kullanarak ilk kez olursa **yükleme** zaman istendiğinde tooinstall hello Microsoft Update Kataloğu eklentisi.</span><span class="sxs-lookup"><span data-stu-id="1ed16-104">If this is your first time using hello Microsoft Update Catalog on this computer, click **Install** when prompted tooinstall hello Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="1ed16-105">![Katalog yükleyin](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="1ed16-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="1ed16-106">Merhaba arama kutusuna hello Microsoft Update Kataloğu hello Bilgi Bankası (KB) numarasını girin hello düzeltme toodownload, örneğin istediğiniz **3179904**ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="1ed16-106">In hello search box of hello Microsoft Update Catalog, enter hello Knowledge Base (KB) number of hello hotfix you want toodownload, for example **3179904**, and then click **Search**.</span></span>
   
    <span data-ttu-id="1ed16-107">Merhaba düzeltme listesi, örneğin, göründüğünde **StorSimple 8000 serisi için toplu yazılım paketini güncelleştirme 2.2**.</span><span class="sxs-lookup"><span data-stu-id="1ed16-107">hello hotfix listing appears, for example, **Cumulative Software Bundle Update 2.2 for StorSimple 8000 Series**.</span></span>
   
    ![Katalogda arama](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="1ed16-109">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-109">Click **Add**.</span></span> <span data-ttu-id="1ed16-110">Merhaba güncelleştirme toohello Sepeti eklenir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-110">hello update is added toohello basket.</span></span>
5. <span data-ttu-id="1ed16-111">Ek düzeltmeleri arayın hello yukarıdaki tabloda listelenen (**3103616**, **3146621**) ve her toohello Sepeti ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1ed16-111">Search for any additional hotfixes listed in hello table above (**3103616**, **3146621**), and add each toohello basket.</span></span>
6. <span data-ttu-id="1ed16-112">**Sepeti Görüntüle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="1ed16-113">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-113">Click **Download**.</span></span> <span data-ttu-id="1ed16-114">Belirtin veya **Gözat** tooa yerel konum istediğiniz hello tooappear indirir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-114">Specify or **Browse** tooa local location where you want hello downloads tooappear.</span></span> <span data-ttu-id="1ed16-115">Merhaba güncelleştirmelerin yükleneceği toohello konumu belirtilen ve alt klasör ile aynı adı hello güncelleştirme olarak hello yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-115">hello updates are downloaded toohello specified location and placed in a sub-folder with hello same name as hello update.</span></span> <span data-ttu-id="1ed16-116">Merhaba klasör de hello aygıttan ulaşılabilir kopyalanan tooa ağ paylaşımı olabilir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-116">hello folder can also be copied tooa network share that is reachable from hello device.</span></span>

> [!NOTE]
> <span data-ttu-id="1ed16-117">Merhaba düzeltmeleri hello eş denetleyicisinden olası tüm hata iletilerini hem denetleyicileri toodetect erişilebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-117">hello hotfixes must be accessible from both controllers toodetect any potential error messages from hello peer controller.</span></span>
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="1ed16-118">tooinstall ve normal modu düzeltmeleri doğrulayın</span><span class="sxs-lookup"><span data-stu-id="1ed16-118">tooinstall and verify regular mode hotfixes</span></span>
<span data-ttu-id="1ed16-119">Aşağıdaki adımları tooinstall hello gerçekleştirmek ve normal modu düzeltmeleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-119">Perform hello following steps tooinstall and verify regular-mode hotfixes.</span></span> <span data-ttu-id="1ed16-120">Bunları zaten yüklü değilse Azure Portal hello kullanarak İleri çok atlayabilirsiniz[yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="1ed16-120">If you already installed them using hello Azure Portal, skip ahead too[install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="1ed16-121">tooinstall hello düzeltmeleri, StorSimple cihaz seri konsoluna erişim hello Windows PowerShell arabiriminde.</span><span class="sxs-lookup"><span data-stu-id="1ed16-121">tooinstall hello hotfixes, access hello Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="1ed16-122">İzleyin hello ayrıntılı yönergeleri [kullanım PuTTy tooconnect toohello seri konsol](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="1ed16-122">Follow hello detailed instructions in [Use PuTTy tooconnect toohello serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="1ed16-123">Merhaba komut isteminde basın **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1ed16-123">At hello command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="1ed16-124">Seçin **seçeneği 1** toolog toohello aygıtta tam erişime sahip.</span><span class="sxs-lookup"><span data-stu-id="1ed16-124">Select **Option 1** toolog on toohello device with full access.</span></span> <span data-ttu-id="1ed16-125">Hello düzeltmeyi hello pasif denetleyicisinde ilk yüklemenizi öneririz.</span><span class="sxs-lookup"><span data-stu-id="1ed16-125">We recommend that you install hello hotfix on hello passive controller first.</span></span>
3. <span data-ttu-id="1ed16-126">Merhaba komut isteminde türü tooinstall hello düzeltme:</span><span class="sxs-lookup"><span data-stu-id="1ed16-126">tooinstall hello hotfix, at hello command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="1ed16-127">Yukarıdaki komut hello paylaşım yolunda DNS yerine IP kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-127">Use IP rather than DNS in share path in hello above command.</span></span> <span data-ttu-id="1ed16-128">yalnızca kimliği doğrulanmış bir paylaşım erişiyorsanız hello kimlik bilgisi parametresi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1ed16-128">hello credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="1ed16-129">Merhaba kimlik bilgisi parametresi tooaccess paylaşımları kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="1ed16-129">We recommend that you use hello credential parameter tooaccess shares.</span></span> <span data-ttu-id="1ed16-130">Çok "herkes" genellikle açık edilen bile paylaşımları toounauthenticated kullanıcılar açabilir değil.</span><span class="sxs-lookup"><span data-stu-id="1ed16-130">Even shares that are open too“everyone” are typically not open toounauthenticated users.</span></span>
   
    <span data-ttu-id="1ed16-131">İstendiğinde hello parolasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-131">Supply hello password when prompted.</span></span>
   
    <span data-ttu-id="1ed16-132">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-132">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="1ed16-133">Tür **Y** zaman istendiğinde tooconfirm hello düzeltme yükleme.</span><span class="sxs-lookup"><span data-stu-id="1ed16-133">Type **Y** when prompted tooconfirm hello hotfix installation.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="1ed16-134">Güncelleştirme 2.2 yüklüyorsanız, yalnızca 'tüm-hcsmdssoftwareudpate' ile başlayan hello ikili dosya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="1ed16-134">If installing Update 2.2, only install hello binary file prefaced with 'all-hcsmdssoftwareudpate'.</span></span> <span data-ttu-id="1ed16-135">İle tüm cismdsagentupdatebundle başında hello CIS ve hello MDS aracı güncelleştirmesi yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="1ed16-135">Do not install hello Cis and hello MDS agent update prefaced with all-cismdsagentupdatebundle.</span></span> <span data-ttu-id="1ed16-136">Hata toodo şekilde bir hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="1ed16-136">Failure toodo so will result in an error.</span></span> 

5. <span data-ttu-id="1ed16-137">Hello kullanarak hello güncelleştirme izleyin `Get-HcsUpdateStatus` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="1ed16-137">Monitor hello update by using hello `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="1ed16-138">Hello güncelleştirme hello pasif denetleyicisinde önce tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="1ed16-138">hello update will first complete on hello passive controller.</span></span> <span data-ttu-id="1ed16-139">Merhaba pasif denetleyici güncelleştirildikten sonra bir yük devretme olacaktır ve hello güncelleştirme sonra üzerinde uygulanacağını diğer denetleyicisi hello.</span><span class="sxs-lookup"><span data-stu-id="1ed16-139">Once hello passive controller is updated, there will be a failover and hello update will then get applied on hello other controller.</span></span> <span data-ttu-id="1ed16-140">hem hello denetleyicileri güncelleştirildiğinde hello güncelleştirme tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="1ed16-140">hello update is complete when both hello controllers are updated.</span></span>
   
    <span data-ttu-id="1ed16-141">Merhaba aşağıdaki örnek çıkış hello güncelleştirme göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-141">hello following sample output shows hello update in progress.</span></span> <span data-ttu-id="1ed16-142">Merhaba `RunInprogress` olacaktır `True` zaman hello güncelleştirme devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="1ed16-142">hello `RunInprogress` will be `True` when hello update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 5/5/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="1ed16-143">örnek çıktı aşağıdaki hello bu hello güncelleştirme tamamlandığında gösterir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-143">hello following sample output indicates that hello update is finished.</span></span> <span data-ttu-id="1ed16-144">Merhaba `RunInProgress` olacaktır `False` zaman hello güncelleştirmesi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="1ed16-144">hello `RunInProgress` will be `False` when hello update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 5/17/2016 9:15:55 AM
    LastUpdateTimestamp : 5/17/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="1ed16-145">Bazen, cmdlet raporları'nı hello `False` hello güncelleştirme devam ederken olduğunda.</span><span class="sxs-lookup"><span data-stu-id="1ed16-145">Occasionally, hello cmdlet reports `False` when hello update is still in progress.</span></span> <span data-ttu-id="1ed16-146">Düzeltme hello tooensure tamamlandığında, birkaç dakika bekleyin, bu komutu yeniden çalıştırın ve bu hello doğrulayın `RunInProgress` olan `False`.</span><span class="sxs-lookup"><span data-stu-id="1ed16-146">tooensure that hello hotfix is complete, wait for a few minutes, rerun this command and verify that hello `RunInProgress` is `False`.</span></span> <span data-ttu-id="1ed16-147">İse, hello düzeltme tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="1ed16-147">If it is, then hello hotfix has completed.</span></span>

1. <span data-ttu-id="1ed16-148">Merhaba yazılım güncelleştirmesi tamamlandıktan sonra hello sistem yazılım sürümleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-148">After hello software update is complete, verify hello system software versions.</span></span> <span data-ttu-id="1ed16-149">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="1ed16-149">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="1ed16-150">Sürümleri aşağıdaki hello görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="1ed16-150">You should see hello following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17708`
   * `CisAgentVersion: 1.0.9299.0`
   * `MdsAgentVersion: 30.0.4698.16` 
     
     <span data-ttu-id="1ed16-151">Merhaba sürüm numaralarını hello güncelleştirmeyi uyguladıktan sonra değiştirmezseniz bu hello düzeltme tooapply başarısız oldu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-151">If hello version numbers do not change after applying hello update, it indicates that hello hotfix has failed tooapply.</span></span> <span data-ttu-id="1ed16-152">Bunu görmeniz durumunda daha fazla yardım için lütfen [Microsoft Desteği](../articles/storsimple/storsimple-contact-microsoft-support.md)’ne başvurun.</span><span class="sxs-lookup"><span data-stu-id="1ed16-152">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="1ed16-153">Merhaba etkin denetleyicisi hello aracılığıyla yeniden başlatmanız gerekir `Restart-HcsController` güncelleştirmeleri kalan hello uygulamadan önce cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="1ed16-153">You must restart hello active controller via hello `Restart-HcsController` cmdlet before applying hello remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="1ed16-154">3-5 tooinstall hello normal modu düzeltmeleri kalan adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="1ed16-154">Repeat steps 3-5 tooinstall hello remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="1ed16-155">Merhaba iSCSI güncelleştirme KB3146621</span><span class="sxs-lookup"><span data-stu-id="1ed16-155">hello iSCSI update KB3146621</span></span>
   * <span data-ttu-id="1ed16-156">Merhaba WMI güncelleştirme KB3103616</span><span class="sxs-lookup"><span data-stu-id="1ed16-156">hello WMI update KB3103616</span></span>
3. <span data-ttu-id="1ed16-157">Güncelleştirme 2'den güncelleştiriyorsanız bu adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-157">Skip this step if you are updating from Update 2.</span></span> <span data-ttu-id="1ed16-158">Bir sürüm önceki tooUpdate 2 güncelleştiriyorsanız toodownload de gerekir:</span><span class="sxs-lookup"><span data-stu-id="1ed16-158">If you are updating from a version prior tooUpdate 2, you will also need toodownload:</span></span>

    - <span data-ttu-id="1ed16-159">Merhaba LSI sürücü KB3121900</span><span class="sxs-lookup"><span data-stu-id="1ed16-159">hello LSI driver KB3121900</span></span>

    - <span data-ttu-id="1ed16-160">Merhaba Spaceport güncelleştirme KB3090322</span><span class="sxs-lookup"><span data-stu-id="1ed16-160">hello Spaceport update KB3090322</span></span>

    - <span data-ttu-id="1ed16-161">Merhaba Storport güncelleştirme KB3080728</span><span class="sxs-lookup"><span data-stu-id="1ed16-161">hello Storport update KB3080728</span></span>

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="1ed16-162">tooinstall ve Bakım modu düzeltmeleri doğrulayın</span><span class="sxs-lookup"><span data-stu-id="1ed16-162">tooinstall and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="1ed16-163">KB3121899 tooinstall disk Bellenim güncelleştirmeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-163">Use KB3121899 tooinstall disk firmware updates.</span></span> <span data-ttu-id="1ed16-164">Bunlar kesintiye uğratan güncelleştirmeleri ve yaklaşık 30 dakika toocomplete alın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-164">These are disruptive updates and take around 30 minutes toocomplete.</span></span> <span data-ttu-id="1ed16-165">Bağlantı toohello cihaz seri Konsolu tarafından bu planlı bakım penceresinde tooinstall seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ed16-165">You can choose tooinstall these in a planned maintenance window by connecting toohello device serial console.</span></span>

<span data-ttu-id="1ed16-166">Disk bellenim zaten güncel ise, bu güncelleştirmeleri tooinstall gerek kalmaz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-166">Note that if your disk firmware is already up-to-date, you won't need tooinstall these updates.</span></span> <span data-ttu-id="1ed16-167">Merhaba çalıştırmak `Get-HcsUpdateAvailability` güncelleştirmeleri kullanılabilir ve olup hello hello cihaz seri konsoluna toocheck cmdlet'inden güncelleştirmeleri olan kesintiye uğratan (Bakım modu) veya benzer (normal modu) güncelleştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="1ed16-167">Run hello `Get-HcsUpdateAvailability` cmdlet from hello device serial console toocheck if updates are available and whether hello updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="1ed16-168">tooinstall hello disk Bellenim güncelleştirmeleri aşağıdaki hello yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="1ed16-168">tooinstall hello disk firmware updates, follow hello instructions below.</span></span>

1. <span data-ttu-id="1ed16-169">Merhaba aygıt hello bakım moduna.</span><span class="sxs-lookup"><span data-stu-id="1ed16-169">Place hello device in hello Maintenance mode.</span></span> <span data-ttu-id="1ed16-170">Windows PowerShell uzaktan iletişimini tooa aygıt, Bakım modunda bağlanırken kullanmaması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-170">Note that you should not use Windows PowerShell remoting when connecting tooa device in Maintenance mode.</span></span> <span data-ttu-id="1ed16-171">Bunun yerine bu cmdlet'i hello cihaz seri konsol üzerinden bağlandığında hello aygıt denetleyicisi çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-171">Instead run this cmdlet on hello device controller when connected through hello device serial console.</span></span> <span data-ttu-id="1ed16-172">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="1ed16-172">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="1ed16-173">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-173">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from hello Microsoft Azure StorSimple Manager service. Entering maintenance mode will end hello current session and reboot both controllers, which takes a few minutes toocomplete. Are you sure you want tooenter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected tooController0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="1ed16-174">Hem hello denetleyicileri bakım moduna ardından yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-174">Both hello controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="1ed16-175">tooinstall hello disk üretici yazılımı güncelleştirmesi, türü:</span><span class="sxs-lookup"><span data-stu-id="1ed16-175">tooinstall hello disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="1ed16-176">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-176">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. <span data-ttu-id="1ed16-177">İzleyici hello yükleme ilerleme durumu kullanarak `Get-HcsUpdateStatus` komutu.</span><span class="sxs-lookup"><span data-stu-id="1ed16-177">Monitor hello install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="1ed16-178">Merhaba güncelleştirme hello zaman tamamlandıktan `RunInProgress` çok değişiklikleri`False`.</span><span class="sxs-lookup"><span data-stu-id="1ed16-178">hello update is complete when hello `RunInProgress` changes too`False`.</span></span>
4. <span data-ttu-id="1ed16-179">Merhaba yüklemesi tamamlandıktan sonra hangi hello üzerinde Bakım modu düzeltme yüklü hello denetleyicisi yeniden başlatır.</span><span class="sxs-lookup"><span data-stu-id="1ed16-179">After hello installation is complete, hello controller on which hello maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="1ed16-180">Seçenek 1 tam erişime sahip olarak oturum açın ve hello disk bellenim sürümü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-180">Log in as option 1 with full access and verify hello disk firmware version.</span></span> <span data-ttu-id="1ed16-181">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="1ed16-181">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="1ed16-182">Merhaba beklenen disk bellenim sürümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1ed16-182">hello expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="1ed16-183">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-183">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected tooController1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    <span data-ttu-id="1ed16-184">Merhaba çalıştırmak `Get-HcsFirmwareVersion` , yazılım sürümü hello hello ikinci denetleyicisi tooverify komutunda güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1ed16-184">Run hello `Get-HcsFirmwareVersion` command on hello second controller tooverify that hello software version has been updated.</span></span> <span data-ttu-id="1ed16-185">Ardından hello Bakım modu çıkabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ed16-185">You can then exit hello maintenance mode.</span></span> <span data-ttu-id="1ed16-186">toodo, bu nedenle, her cihaz denetleyicisi için komutu aşağıdaki hello yazın:</span><span class="sxs-lookup"><span data-stu-id="1ed16-186">toodo so, type hello following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="1ed16-187">Bakım modu çıktığınızda hello denetleyicilerini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-187">hello controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="1ed16-188">Sonra Hello disk Bellenim güncelleştirmeleri başarıyla uygulandıktan ve hello aygıt Bakım modu, dönüş toohello Klasik Azure portalı çıkıldı.</span><span class="sxs-lookup"><span data-stu-id="1ed16-188">After hello disk firmware updates are successfully applied and hello device has exited maintenance mode, return toohello Azure classic portal.</span></span> <span data-ttu-id="1ed16-189">Merhaba portalınız hello Bakım modu güncelleştirmeleri 24 saat için yüklü gösterilmeyebilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1ed16-189">Note that hello portal might not show that you installed hello Maintenance mode updates for 24 hours.</span></span>

