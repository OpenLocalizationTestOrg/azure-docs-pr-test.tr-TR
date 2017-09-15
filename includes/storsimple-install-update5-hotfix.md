<!--author=alkohli last changed: 08/21/17-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="569d3-101">Düzeltmeleri indirmek için</span><span class="sxs-lookup"><span data-stu-id="569d3-101">To download hotfixes</span></span>

<span data-ttu-id="569d3-102">Microsoft Update Kataloğu'ndan yazılım güncelleştirmesi indirmek için aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="569d3-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="569d3-103">Internet Explorer'ı başlatın ve [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com) adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="569d3-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="569d3-104">Microsoft Update Kataloğu’nu bu bilgisayarda ilk kez kullanıyorsanız, sorulduğunda **Yükle**’ye tıklayarak Microsoft Update Kataloğu eklentisini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="569d3-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

    ![Katalog yükleme](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="569d3-106">Microsoft Update Kataloğu arama kutusuna, örneğin, yüklemek istediğiniz düzeltme Bilgi Bankası (KB) sayısını girin **4037264**ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="569d3-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4037264**, and then click **Search**.</span></span>
   
    <span data-ttu-id="569d3-107">Düzeltme listesi göründüğünde, örneğin, **StorSimple 8000 serisi için toplu yazılım paketini güncelleştirme 5.0**.</span><span class="sxs-lookup"><span data-stu-id="569d3-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 5.0 for StorSimple 8000 Series**.</span></span>
   
    ![Katalogda arama](./media/storsimple-install-update5-hotfix/update-catalog-search.png)

4. <span data-ttu-id="569d3-109">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="569d3-109">Click **Download**.</span></span> <span data-ttu-id="569d3-110">İndirilen öğelerin görünmesini istediğiniz yerel konumu belirtin veya **Gözat** seçeneğiyle konumu bulun.</span><span class="sxs-lookup"><span data-stu-id="569d3-110">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="569d3-111">Belirtilen konum ve klasöre yüklemek için dosyalar'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="569d3-111">Click the files to download to the specified location and folder.</span></span> <span data-ttu-id="569d3-112">Klasör, cihazdan erişilebilen bir ağ paylaşımına da kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="569d3-112">The folder can also be copied to a network share that is reachable from the device.</span></span>
5. <span data-ttu-id="569d3-113">Ek düzeltmeleri arayın yukarıdaki tabloda listelenen (**4037266**) ve yukarıdaki tabloda listelenen gibi belirli klasörlere karşılık gelen dosyalarını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="569d3-113">Search for any additional hotfixes listed in the table above (**4037266**), and download the corresponding files to the specific folders as listed in the preceding table.</span></span>

> [!NOTE]
> <span data-ttu-id="569d3-114">Düzeltmeleri tüm olası hata iletilerini eş denetleyicisinden algılamak için her iki denetleyicilerinden erişilebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="569d3-114">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
>
> <span data-ttu-id="569d3-115">Düzeltmeler 3 ayrı klasöre kopyalanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="569d3-115">The hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="569d3-116">Örneğin, aygıt CIS/software/MDS aracı güncelleştirmesi içinde kopyalanabilir _FirstOrderUpdate_ klasörü, diğer tüm benzer güncelleştirmeleri kopyalanmasına içinde _SecondOrderUpdate_ klasörünü ve Bakım modu güncelleştirmeleri içinde kopyalanan _ThirdOrderUpdate_ klasör.</span><span class="sxs-lookup"><span data-stu-id="569d3-116">For example, the device software/Cis/MDS agent update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="569d3-117">Normal mod düzeltmelerini yüklemek ve doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="569d3-117">To install and verify regular mode hotfixes</span></span>

<span data-ttu-id="569d3-118">Normal mod düzeltmelerini yüklemek ve doğrulamak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="569d3-118">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="569d3-119">İçin bunları Azure Portalı'nı kullanarak zaten yüklü değilse,'ın İleri atlayabilirsiniz [yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="569d3-119">If you already installed them using the Azure portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="569d3-120">Düzeltmeleri yüklemek için StorSimple cihazı seri konsolunuzdaki Windows PowerShell arabirimine erişin.</span><span class="sxs-lookup"><span data-stu-id="569d3-120">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="569d3-121">[Seri konsola bağlanmak için PuTTy kullanma](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console) bölümündeki ayrıntılı yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="569d3-121">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-8000-deployment-walkthrough-u2.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="569d3-122">Komut isteminde **Enter** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="569d3-122">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="569d3-123">Cihazda tam erişimle oturum açmak için **Seçenek 1**’i belirleyin.</span><span class="sxs-lookup"><span data-stu-id="569d3-123">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="569d3-124">Düzeltmeyi ilk olarak edilgen denetleyiciye yüklemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="569d3-124">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="569d3-125">Düzeltmeyi yüklemek için komut istemine şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="569d3-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="569d3-126">Yukarıdaki komuttaki paylaşım yolunda DNS yerine IP kullanın.</span><span class="sxs-lookup"><span data-stu-id="569d3-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="569d3-127">Kimlik bilgisi parametresi yalnızca kimliği doğrulanmış bir paylaşımdan erişiyorsanız kullanılır.</span><span class="sxs-lookup"><span data-stu-id="569d3-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="569d3-128">Paylaşımlara erişmek için kimlik bilgisi parametresini kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="569d3-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="569d3-129">“Herkese” açık paylaşımlar bile genellikle kimliği doğrulanmamış kullanıcılara açık değildir.</span><span class="sxs-lookup"><span data-stu-id="569d3-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
4. <span data-ttu-id="569d3-130">İstendiğinde parolayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="569d3-130">Supply the password when prompted.</span></span> <span data-ttu-id="569d3-131">Birinci sipariş güncelleştirmelerini yüklemeye ilişkin örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="569d3-131">A sample output for installing the first order updates is shown below.</span></span> <span data-ttu-id="569d3-132">İlk sipariş güncelleştirmesi için belirli bir dosyaya işaret edecek şekilde gerekir.</span><span class="sxs-lookup"><span data-stu-id="569d3-132">For the first order update, you need to point to the specific file.</span></span>

    >[!NOTE] 
    > <span data-ttu-id="569d3-133">Yüklemeniz gerekir _HcsSoftwareUpdate.exe_ ilk.</span><span class="sxs-lookup"><span data-stu-id="569d3-133">You should install the _HcsSoftwareUpdate.exe_ first.</span></span> <span data-ttu-id="569d3-134">Bu yükleme tamamlandıktan sonra daha sonra yüklemek _CisMdsAgentUpdate.exe_.</span><span class="sxs-lookup"><span data-stu-id="569d3-134">After this install has completed, then install _CisMdsAgentUpdate.exe_.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
5. <span data-ttu-id="569d3-135">Düzeltme yüklemesini onaylamak için sorulduğunda **Y** yazın.</span><span class="sxs-lookup"><span data-stu-id="569d3-135">Type **Y** when prompted to confirm the hotfix installation.</span></span>
6. <span data-ttu-id="569d3-136">`Get-HcsUpdateStatus` cmdlet'ini kullanarak güncelleştirmeyi izleyin.</span><span class="sxs-lookup"><span data-stu-id="569d3-136">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="569d3-137">Güncelleştirme ilk olarak edilgen denetleyicide tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="569d3-137">The update will first complete on the passive controller.</span></span> <span data-ttu-id="569d3-138">Edilgen denetleyici güncelleştirildikten sonra yük devretme gerçekleştirilir ve bundan sonra güncelleştirme diğer denetleyiciye uygulanır.</span><span class="sxs-lookup"><span data-stu-id="569d3-138">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="569d3-139">Her iki denetleyici de güncelleştirildiğinde güncelleştirme tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="569d3-139">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="569d3-140">Devam etmekte olan güncelleştirme aşağıdaki örnek çıktıda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="569d3-140">The following sample output shows the update in progress.</span></span> <span data-ttu-id="569d3-141">`RunInprogress` Olan `True` zaman güncelleştirme devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="569d3-141">The `RunInprogress` is `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 07/28/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="569d3-142">Aşağıdaki örnek çıktıda güncelleştirmenin tamamlandığı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="569d3-142">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="569d3-143">`RunInProgress` Olan `False` güncelleştirme tamamlandığında.</span><span class="sxs-lookup"><span data-stu-id="569d3-143">The `RunInProgress` is `False` when the update is complete.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 07/28/2017 9:15:55 AM
    LastUpdateTimestamp : 07/28/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="569d3-144">Bazı durumlarda cmdlet, güncelleştirme hala devam ediyorsa `False` raporu gönderir.</span><span class="sxs-lookup"><span data-stu-id="569d3-144">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="569d3-145">Düzeltmenin tamamlandığından emin olmak için birkaç dakika bekleyin, bu komutu yeniden çalıştırın ve `RunInProgress` değerinin `False` olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="569d3-145">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="569d3-146">Değer değiştiyse düzeltme tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="569d3-146">If it is, then the hotfix has completed.</span></span>

7. <span data-ttu-id="569d3-147">Yazılım güncelleştirmesi tamamlandıktan sonra sistem yazılımı sürümlerini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="569d3-147">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="569d3-148">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="569d3-148">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="569d3-149">Aşağıdaki sürümleri görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="569d3-149">You should see the following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 5.0`
   *  `HcsSoftwareVersion: 6.3.9600.17845`
   
    <span data-ttu-id="569d3-150">Güncelleştirme uygulandıktan sonra sürüm numarası değişmezse, düzeltmenin uygulanamadığı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="569d3-150">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="569d3-151">Bunu görmeniz durumunda daha fazla yardım için lütfen [Microsoft Desteği](../articles/storsimple/storsimple-8000-contact-microsoft-support.md)’ne başvurun.</span><span class="sxs-lookup"><span data-stu-id="569d3-151">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-8000-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="569d3-152">Etkin denetleyicisi aracılığıyla yeniden başlatmanız gerekir `Restart-HcsController` sonraki güncelleştirmeyi uygulamadan önce cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="569d3-152">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the next update.</span></span>
     
8. <span data-ttu-id="569d3-153">Yüklemek için 3 ile 6 arasındaki adımları yineleyin _CisMDSAgentupdate.exe_ Aracısı indirdiğiniz, _FirstOrderUpdate_ klasör.</span><span class="sxs-lookup"><span data-stu-id="569d3-153">Repeat steps 3-6 to install the _CisMDSAgentupdate.exe_ agent downloaded to your _FirstOrderUpdate_ folder.</span></span>
8. <span data-ttu-id="569d3-154">İkinci sipariş güncelleştirmeleri yüklemek için 3-6 adımlarını yineleyin.</span><span class="sxs-lookup"><span data-stu-id="569d3-154">Repeat steps 3-6 to install the second order updates.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="569d3-155">İkinci sipariş güncelleştirmeleri yalnızca çalıştırarak birden çok güncelleştirme yüklenebilir `Start-HcsHotfix cmdlet` ve ikinci sipariş güncelleştirmeleri bulunduğu klasöre işaret ediyor.</span><span class="sxs-lookup"><span data-stu-id="569d3-155">For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located.</span></span> <span data-ttu-id="569d3-156">Cmdlet, klasörde bulunan tüm güncelleştirmeleri yürütür.</span><span class="sxs-lookup"><span data-stu-id="569d3-156">The cmdlet will execute all the updates available in the folder.</span></span> <span data-ttu-id="569d3-157">Bir güncelleştirme zaten yüklüyse, güncelleştirme mantığı bunu saptar ve ilgili güncelleştirmeyi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="569d3-157">If an update is already installed, the update logic will detect that and not apply that update.</span></span>

    <span data-ttu-id="569d3-158">Tüm düzeltmeler yüklendikten sonra `Get-HcsSystem` cmdlet'ini kullanın.</span><span class="sxs-lookup"><span data-stu-id="569d3-158">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="569d3-159">Sürümler şunlar olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="569d3-159">The versions should be:</span></span>
    
    * `CisAgentVersion:  1.0.9724.0`
    * `MdsAgentVersion: 35.2.2.0`
    * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="569d3-160">Bakım modu düzeltmelerini yüklemek ve doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="569d3-160">To install and verify maintenance mode hotfixes</span></span>

<span data-ttu-id="569d3-161">Disk Bellenim güncelleştirmeleri yüklemek için KB4037263 kullanın.</span><span class="sxs-lookup"><span data-stu-id="569d3-161">Use KB4037263 to install disk firmware updates.</span></span> <span data-ttu-id="569d3-162">Bunlar kesintiye uğratan güncelleştirmelerdir ve tamamlanması yaklaşık 30 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="569d3-162">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="569d3-163">Bunları cihaz seri konsoluna bağlanarak planlı bakım penceresinde yüklemeyi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="569d3-163">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

> [!NOTE] 
> <span data-ttu-id="569d3-164">Disk bellenim zaten güncel ise, bu güncelleştirmeleri yüklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="569d3-164">If your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="569d3-165">Güncelleştirmelerin mevcut olup olmadığını ve güncelleştirmelerin kesintiye uğratıp (bakım modu) uğratmayacağını (normal mod) denetlemek için cihaz seri konsolundan `Get-HcsUpdateAvailability` cmdlet’ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="569d3-165">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="569d3-166">Disk üretici yazılımı güncelleştirmelerini yüklemek için aşağıdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="569d3-166">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="569d3-167">Cihazı bakım moduna alın.</span><span class="sxs-lookup"><span data-stu-id="569d3-167">Place the device in the maintenance mode.</span></span> 

    > [!NOTE] 
    > <span data-ttu-id="569d3-168">Windows PowerShell uzaktan iletişimini bakım modundaki bir aygıta bağlanırken kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="569d3-168">Do not use Windows PowerShell remoting when connecting to a device in maintenance mode.</span></span> <span data-ttu-id="569d3-169">Bunun yerine bu cmdlet'i cihaz seri konsol üzerinden bağlandığında aygıt denetleyicisinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="569d3-169">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span>

    <span data-ttu-id="569d3-170">Bakım moduna denetleyicisi için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="569d3-170">To place the controller in maintenance mode, type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="569d3-171">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="569d3-171">A sample output is shown below.</span></span>
   
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
   
    <span data-ttu-id="569d3-172">Bu durumda her iki denetleyici de bakım modunda yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="569d3-172">Both the controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="569d3-173">Disk üretici yazılımı güncelleştirmesini yüklemek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="569d3-173">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="569d3-174">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="569d3-174">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="569d3-175">`Get-HcsUpdateStatus` komutunu kullanarak yükleme ilerleme durumunu izleyin.</span><span class="sxs-lookup"><span data-stu-id="569d3-175">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="569d3-176">`RunInProgress` değeri `False` olarak değiştiğinde güncelleştirme tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="569d3-176">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="569d3-177">Yükleme tamamlandıktan sonra, bakım modu düzeltmesinin yüklendiği denetleyici yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="569d3-177">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="569d3-178">Tam erişimle seçenek 1 olarak oturum açın ve disk üretici yazılımı sürümünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="569d3-178">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="569d3-179">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="569d3-179">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="569d3-180">Beklenen disk üretici yazılımı sürümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="569d3-180">The expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N003, 0107`
   
   <span data-ttu-id="569d3-181">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="569d3-181">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17845
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
   
    <span data-ttu-id="569d3-182">Yazılım sürümünün güncelleştirildiğinden emin olmak için ikinci denetleyicide `Get-HcsFirmwareVersion` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="569d3-182">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="569d3-183">Bundan sonra bakım modundan çıkabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="569d3-183">You can then exit the maintenance mode.</span></span> <span data-ttu-id="569d3-184">Bunu yapmak için, her bir cihaz denetleyicisi için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="569d3-184">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="569d3-185">Bakım modundan çıktığınızda denetleyiciler yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="569d3-185">The controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="569d3-186">Sonra disk Bellenim güncelleştirmeleri başarıyla uygulandıktan ve cihaz Bakım modu, Azure portalında dönüş çıkıldı.</span><span class="sxs-lookup"><span data-stu-id="569d3-186">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure portal.</span></span> <span data-ttu-id="569d3-187">Yüklediğiniz bakım modu güncelleştirmeleri, 24 saat boyunca portalda gösterilmeyebilir.</span><span class="sxs-lookup"><span data-stu-id="569d3-187">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span></span>

