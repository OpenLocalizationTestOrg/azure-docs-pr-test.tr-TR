<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="95919-101">Düzeltmeleri indirmek için</span><span class="sxs-lookup"><span data-stu-id="95919-101">To download hotfixes</span></span>

<span data-ttu-id="95919-102">Microsoft Update Kataloğu'ndan yazılım güncelleştirmesi indirmek için aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="95919-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="95919-103">Internet Explorer'ı başlatın ve [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com) adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="95919-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="95919-104">Microsoft Update Kataloğu’nu bu bilgisayarda ilk kez kullanıyorsanız, sorulduğunda **Yükle**’ye tıklayarak Microsoft Update Kataloğu eklentisini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="95919-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

    ![Katalog yükleme](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="95919-106">Microsoft Update Kataloğu arama kutusuna, indirmek istediğiniz düzeltmenin Bilgi Bankası (KB) numarasını girin (örneğin, **4011839**) ve ardından **Ara**’ya tıklayın.</span><span class="sxs-lookup"><span data-stu-id="95919-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4011839**, and then click **Search**.</span></span>
   
    <span data-ttu-id="95919-107">Düzeltme listesi görüntülenir, örneğin **StorSimple 8000 Serisi için Toplu Yazılım Paketi Güncelleştirmesi 4.0**.</span><span class="sxs-lookup"><span data-stu-id="95919-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 4.0 for StorSimple 8000 Series**.</span></span>
   
    ![Katalogda arama](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)

4. <span data-ttu-id="95919-109">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="95919-109">Click **Download**.</span></span> <span data-ttu-id="95919-110">İndirilen öğelerin görünmesini istediğiniz yerel konumu belirtin veya **Gözat** seçeneğiyle konumu bulun.</span><span class="sxs-lookup"><span data-stu-id="95919-110">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="95919-111">Belirtilen konum ve klasöre yüklemek için dosyalar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="95919-111">Click the files to download to the specified location and folder.</span></span> <span data-ttu-id="95919-112">Klasör, cihazdan erişilebilen bir ağ paylaşımına da kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="95919-112">The folder can also be copied to a network share that is reachable from the device.</span></span>
5. <span data-ttu-id="95919-113">Ek düzeltmeleri arayın yukarıdaki tabloda listelenen (**4011841**) ve yukarıdaki tabloda listelenen gibi belirli klasörlere karşılık gelen dosyalarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="95919-113">Search for any additional hotfixes listed in the table above (**4011841**), and download the corresponding files to the specific folders as listed in the preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="95919-114">Düzeltmeleri tüm olası hata iletilerini eş denetleyicisinden algılamak için her iki denetleyicilerinden erişilebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="95919-114">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
>
> <span data-ttu-id="95919-115">Düzeltmeler 3 ayrı klasöre kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="95919-115">The hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="95919-116">Örneğin, aygıt CIS/software/MDS aracı güncelleştirmesi içinde kopyalanabilir _FirstOrderUpdate_ klasörü, diğer tüm benzer güncelleştirmeleri kopyalanmasına içinde _SecondOrderUpdate_ klasörünü ve Bakım modu güncelleştirmeleri içinde kopyalanan _ThirdOrderUpdate_ klasör.</span><span class="sxs-lookup"><span data-stu-id="95919-116">For example, the device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="95919-117">Normal mod düzeltmelerini yüklemek ve doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="95919-117">To install and verify regular mode hotfixes</span></span>

<span data-ttu-id="95919-118">Normal mod düzeltmelerini yüklemek ve doğrulamak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="95919-118">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="95919-119">Bu düzeltmeleri klasik Azure portalını kullanarak yüklediyseniz, [bakım modu düzeltmelerini yükleme ve doğrulama](#to-install-and-verify-maintenance-mode-hotfixes) bölümüne atlayın.</span><span class="sxs-lookup"><span data-stu-id="95919-119">If you already installed them using the Azure classic portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="95919-120">Düzeltmeleri yüklemek için StorSimple cihazı seri konsolunuzdaki Windows PowerShell arabirimine erişin.</span><span class="sxs-lookup"><span data-stu-id="95919-120">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="95919-121">[Seri konsola bağlanmak için PuTTy kullanma](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console) bölümündeki ayrıntılı yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="95919-121">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="95919-122">Komut isteminde **Enter** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="95919-122">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="95919-123">Cihazda tam erişimle oturum açmak için **Seçenek 1**’i belirleyin.</span><span class="sxs-lookup"><span data-stu-id="95919-123">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="95919-124">Düzeltmeyi ilk olarak edilgen denetleyiciye yüklemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="95919-124">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="95919-125">Düzeltmeyi yüklemek için komut istemine şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="95919-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="95919-126">Yukarıdaki komuttaki paylaşım yolunda DNS yerine IP kullanın.</span><span class="sxs-lookup"><span data-stu-id="95919-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="95919-127">Kimlik bilgisi parametresi yalnızca kimliği doğrulanmış bir paylaşımdan erişiyorsanız kullanılır.</span><span class="sxs-lookup"><span data-stu-id="95919-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="95919-128">Paylaşımlara erişmek için kimlik bilgisi parametresini kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="95919-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="95919-129">“Herkese” açık paylaşımlar bile genellikle kimliği doğrulanmamış kullanıcılara açık değildir.</span><span class="sxs-lookup"><span data-stu-id="95919-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="95919-130">İstendiğinde parolayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="95919-130">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="95919-131">Birinci sipariş güncelleştirmelerini yüklemeye ilişkin örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="95919-131">A sample output for installing the first order updates is shown below.</span></span> <span data-ttu-id="95919-132">İlk sipariş güncelleştirmesi için belirli bir dosyaya işaret edecek şekilde gerekir.</span><span class="sxs-lookup"><span data-stu-id="95919-132">For the first order update, you need to point to the specific file.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="95919-133">Düzeltme yüklemesini onaylamak için sorulduğunda **Y** yazın.</span><span class="sxs-lookup"><span data-stu-id="95919-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="95919-134">`Get-HcsUpdateStatus` cmdlet'ini kullanarak güncelleştirmeyi izleyin.</span><span class="sxs-lookup"><span data-stu-id="95919-134">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="95919-135">Güncelleştirme ilk olarak edilgen denetleyicide tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="95919-135">The update will first complete on the passive controller.</span></span> <span data-ttu-id="95919-136">Edilgen denetleyici güncelleştirildikten sonra yük devretme gerçekleştirilir ve bundan sonra güncelleştirme diğer denetleyiciye uygulanır.</span><span class="sxs-lookup"><span data-stu-id="95919-136">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="95919-137">Her iki denetleyici de güncelleştirildiğinde güncelleştirme tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="95919-137">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="95919-138">Devam etmekte olan güncelleştirme aşağıdaki örnek çıktıda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="95919-138">The following sample output shows the update in progress.</span></span> <span data-ttu-id="95919-139">Güncelleştirme devam ederken `RunInprogress` değeri `True` olacaktır.</span><span class="sxs-lookup"><span data-stu-id="95919-139">The `RunInprogress` will be `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="95919-140">Aşağıdaki örnek çıktıda güncelleştirmenin tamamlandığı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="95919-140">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="95919-141">Güncelleştirme tamamlandığında `RunInProgress` değeri `False` olacaktır.</span><span class="sxs-lookup"><span data-stu-id="95919-141">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="95919-142">Bazı durumlarda cmdlet, güncelleştirme hala devam ediyorsa `False` raporu gönderir.</span><span class="sxs-lookup"><span data-stu-id="95919-142">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="95919-143">Düzeltmenin tamamlandığından emin olmak için birkaç dakika bekleyin, bu komutu yeniden çalıştırın ve `RunInProgress` değerinin `False` olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="95919-143">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="95919-144">Değer değiştiyse düzeltme tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="95919-144">If it is, then the hotfix has completed.</span></span>

6. <span data-ttu-id="95919-145">Yazılım güncelleştirmesi tamamlandıktan sonra sistem yazılımı sürümlerini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="95919-145">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="95919-146">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="95919-146">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="95919-147">Aşağıdaki sürümleri görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="95919-147">You should see the following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    <span data-ttu-id="95919-148">Güncelleştirme uygulandıktan sonra sürüm numarası değişmezse, düzeltmenin uygulanamadığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="95919-148">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="95919-149">Bunu görmeniz durumunda daha fazla yardım için lütfen [Microsoft Desteği](../articles/storsimple/storsimple-contact-microsoft-support.md)’ne başvurun.</span><span class="sxs-lookup"><span data-stu-id="95919-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="95919-150">Etkin denetleyicisi aracılığıyla yeniden başlatmanız gerekir `Restart-HcsController` sonraki güncelleştirmeyi uygulamadan önce cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="95919-150">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the next update.</span></span>
     
7. <span data-ttu-id="95919-151">Karşıdan CIS/MDS aracısı yüklemek için 3 ile 5 arasındaki adımları yineleyin, _FirstOrderUpdate_ klasör.</span><span class="sxs-lookup"><span data-stu-id="95919-151">Repeat steps 3-5 to install the Cis/MDS agent downloaded to your _FirstOrderUpdate_ folder.</span></span> 
8. <span data-ttu-id="95919-152">İkinci sipariş güncelleştirmelerini yüklemek için 3-5 aralığındaki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="95919-152">Repeat steps 3-5 to install the second order updates.</span></span> <span data-ttu-id="95919-153">**İkinci sipariş güncelleştirmeleri yalnızca çalıştırarak birden çok güncelleştirme yüklenebilir `Start-HcsHotfix cmdlet` ve ikinci sipariş güncelleştirmeleri bulunduğu klasöre işaret ediyor. Cmdlet kullanılabilir tüm güncelleştirmeleri klasöründe yürütülür.**</span><span class="sxs-lookup"><span data-stu-id="95919-153">**For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located. The cmdlet will execute all the updates available in the folder.**</span></span> <span data-ttu-id="95919-154">Bir güncelleştirme zaten yüklüyse, güncelleştirme mantığı bunu saptar ve ilgili güncelleştirmeyi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="95919-154">If an update is already installed, the update logic will detect that and not apply that update.</span></span> 

<span data-ttu-id="95919-155">Tüm düzeltmeler yüklendikten sonra `Get-HcsSystem` cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="95919-155">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="95919-156">Sürümler şunlar olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="95919-156">The versions should be:</span></span>

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="95919-157">Bakım modu düzeltmelerini yüklemek ve doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="95919-157">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="95919-158">Disk üretici yazılımı güncelleştirmelerini yüklemek için KB4011837’yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="95919-158">Use KB4011837 to install disk firmware updates.</span></span> <span data-ttu-id="95919-159">Bunlar kesintiye uğratan güncelleştirmelerdir ve tamamlanması yaklaşık 30 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="95919-159">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="95919-160">Bunları cihaz seri konsoluna bağlanarak planlı bakım penceresinde yüklemeyi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95919-160">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="95919-161">Disk üretici yazılımınız zaten güncelse bu güncelleştirmeleri yüklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="95919-161">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="95919-162">Güncelleştirmelerin mevcut olup olmadığını ve güncelleştirmelerin kesintiye uğratıp (bakım modu) uğratmayacağını (normal mod) denetlemek için cihaz seri konsolundan `Get-HcsUpdateAvailability` cmdlet’ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="95919-162">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="95919-163">Disk üretici yazılımı güncelleştirmelerini yüklemek için aşağıdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="95919-163">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="95919-164">Cihazı bakım moduna alın.</span><span class="sxs-lookup"><span data-stu-id="95919-164">Place the device in the maintenance mode.</span></span> <span data-ttu-id="95919-165">**Bakım modunda bir cihaza bağlanırken Windows PowerShell uzaktan iletişimini kullanmamanız gerekir. Bunun yerine, cihaz seri konsolu üzerinden bağlanırken bu cmdlet’i cihaz denetleyicisinde çalıştırın.**</span><span class="sxs-lookup"><span data-stu-id="95919-165">**Note that you should not use Windows PowerShell remoting when connecting to a device in maintenance mode. Instead run this cmdlet on the device controller when connected through the device serial console.**</span></span> <span data-ttu-id="95919-166">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="95919-166">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="95919-167">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="95919-167">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="95919-168">Bu durumda her iki denetleyici de bakım modunda yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="95919-168">Both the controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="95919-169">Disk üretici yazılımı güncelleştirmesini yüklemek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="95919-169">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="95919-170">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="95919-170">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="95919-171">`Get-HcsUpdateStatus` komutunu kullanarak yükleme ilerleme durumunu izleyin.</span><span class="sxs-lookup"><span data-stu-id="95919-171">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="95919-172">`RunInProgress` değeri `False` olarak değiştiğinde güncelleştirme tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="95919-172">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="95919-173">Yükleme tamamlandıktan sonra, bakım modu düzeltmesinin yüklendiği denetleyici yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="95919-173">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="95919-174">Tam erişimle seçenek 1 olarak oturum açın ve disk üretici yazılımı sürümünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="95919-174">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="95919-175">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="95919-175">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="95919-176">Beklenen disk üretici yazılımı sürümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="95919-176">The expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   <span data-ttu-id="95919-177">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="95919-177">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17820
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    <span data-ttu-id="95919-178">Yazılım sürümünün güncelleştirildiğinden emin olmak için ikinci denetleyicide `Get-HcsFirmwareVersion` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="95919-178">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="95919-179">Bundan sonra bakım modundan çıkabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95919-179">You can then exit the maintenance mode.</span></span> <span data-ttu-id="95919-180">Bunu yapmak için, her bir cihaz denetleyicisi için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="95919-180">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="95919-181">Bakım modundan çıktığınızda denetleyiciler yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="95919-181">The controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="95919-182">Disk üretici yazılımı güncelleştirmeleri başarıyla uygulanıp cihaz bakım modundan çıktıktan sonra, klasik Azure portalına geri dönün.</span><span class="sxs-lookup"><span data-stu-id="95919-182">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="95919-183">Yüklediğiniz bakım modu güncelleştirmeleri, 24 saat boyunca portalda gösterilmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="95919-183">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span></span>

