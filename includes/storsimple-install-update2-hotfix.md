<!--author=alkohli last changed: 03/17/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="fb5aa-101">Düzeltmeleri indirmek için</span><span class="sxs-lookup"><span data-stu-id="fb5aa-101">To download hotfixes</span></span>
<span data-ttu-id="fb5aa-102">Microsoft Update Kataloğu'ndan yazılım güncelleştirmesi indirmek için aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="fb5aa-103">Internet Explorer'ı başlatın ve [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com) adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="fb5aa-104">Microsoft Update Kataloğu’nu bu bilgisayarda ilk kez kullanıyorsanız, sorulduğunda **Yükle**’ye tıklayarak Microsoft Update Kataloğu eklentisini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="fb5aa-105">![Katalog yükleyin](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="fb5aa-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="fb5aa-106">Microsoft Update Kataloğu arama kutusuna, örneğin, yüklemek istediğiniz düzeltme Bilgi Bankası (KB) sayısını girin **3121901**ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3121901**, and then click **Search**.</span></span>
   
    <span data-ttu-id="fb5aa-107">Düzeltme listesi göründüğünde, örneğin, **StorSimple 8000 serisi için toplu yazılım paketini güncelleştirme 2.0**.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.0 for StorSimple 8000 Series**.</span></span>
   
    ![Katalogda arama](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="fb5aa-109">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-109">Click **Add**.</span></span> <span data-ttu-id="fb5aa-110">Güncelleştirme sepete eklenir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="fb5aa-111">Ek düzeltmeleri arayın yukarıdaki tabloda listelenen (**3121900**, **3080728**, **3090322**, ve **3121899**) ve her ekleyin Sepeti.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-111">Search for any additional hotfixes listed in the table above (**3121900**, **3080728**, **3090322**, and **3121899**), and add each the basket.</span></span>
6. <span data-ttu-id="fb5aa-112">**Sepeti Görüntüle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="fb5aa-113">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-113">Click **Download**.</span></span> <span data-ttu-id="fb5aa-114">İndirilen öğelerin görünmesini istediğiniz yerel konumu belirtin veya **Gözat** seçeneğiyle konumu bulun.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="fb5aa-115">Güncelleştirmeler belirtilen konuma indirilir ve güncelleştirme ile aynı adı taşıyan alt klasöre yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="fb5aa-116">Klasör, cihazdan erişilebilen bir ağ paylaşımına da kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="fb5aa-117">Düzeltmeleri tüm olası hata iletilerini eş denetleyicisinden algılamak için her iki denetleyicilerinden erişilebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="fb5aa-118">Normal mod düzeltmelerini yüklemek ve doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="fb5aa-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="fb5aa-119">Normal mod düzeltmelerini yüklemek ve doğrulamak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="fb5aa-120">İçin bunları Azure Portalı'nı kullanarak zaten yüklü değilse,'ın İleri atlayabilirsiniz [yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="fb5aa-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="fb5aa-121">Düzeltmeleri yüklemek için StorSimple cihazı seri konsolunuzdaki Windows PowerShell arabirimine erişin.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="fb5aa-122">[Seri konsola bağlanmak için PuTTy kullanma](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console) bölümündeki ayrıntılı yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="fb5aa-123">Komut isteminde **Enter** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="fb5aa-124">Cihazda tam erişimle oturum açmak için **Seçenek 1**’i belirleyin.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-124">Select **Option 1** to log on to the device with full access.</span></span>
3. <span data-ttu-id="fb5aa-125">Düzeltmeyi yüklemek için komut istemine şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="fb5aa-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="fb5aa-126">Yukarıdaki komuttaki paylaşım yolunda DNS yerine IP kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="fb5aa-127">Kimlik bilgisi parametresi yalnızca kimliği doğrulanmış bir paylaşımdan erişiyorsanız kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="fb5aa-128">Paylaşımlara erişmek için kimlik bilgisi parametresini kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="fb5aa-129">“Herkese” açık paylaşımlar bile genellikle kimliği doğrulanmamış kullanıcılara açık değildir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="fb5aa-130">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```
4. <span data-ttu-id="fb5aa-131">Düzeltme yüklemesini onaylamak için sorulduğunda **Y** yazın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-131">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="fb5aa-132">`Get-HcsUpdateStatus` cmdlet'ini kullanarak güncelleştirmeyi izleyin.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="fb5aa-133">Devam etmekte olan güncelleştirme aşağıdaki örnek çıktıda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-133">The following sample output shows the update in progress.</span></span> <span data-ttu-id="fb5aa-134">Güncelleştirme devam ederken `RunInprogress` değeri `True` olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-134">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 12/21/2015 10:36:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="fb5aa-135">Aşağıdaki örnek çıktıda güncelleştirmenin tamamlandığı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-135">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="fb5aa-136">Güncelleştirme tamamlandığında `RunInProgress` değeri `False` olacaktır.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-136">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 12/21/2015 10:59:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="fb5aa-137">Bazı durumlarda cmdlet, güncelleştirme hala devam ediyorsa `False` raporu gönderir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="fb5aa-138">Düzeltmenin tamamlandığından emin olmak için birkaç dakika bekleyin, bu komutu yeniden çalıştırın ve `RunInProgress` değerinin `False` olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="fb5aa-139">Değer değiştiyse düzeltme tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-139">If it is, then the hotfix has completed.</span></span>

6. <span data-ttu-id="fb5aa-140">Yazılım güncelleştirmesi tamamlandıktan sonra adım 3-5, yüklemek ve SaaS aracısı ve MDS Aracısı izlemek için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-140">After the software update is complete, repeat steps 3-5 to install and monitor the SaaS agent and MDS agent .</span></span> <span data-ttu-id="fb5aa-141">Emin `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` önce yüklü `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-141">Ensure that `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is installed before `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span></span>
7. <span data-ttu-id="fb5aa-142">Sistem yazılım sürümleri doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-142">Verify the system software versions.</span></span> <span data-ttu-id="fb5aa-143">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="fb5aa-143">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="fb5aa-144">Aşağıdaki sürümleri görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="fb5aa-144">You should see the following versions:</span></span>
   
   * <span data-ttu-id="fb5aa-145">HcsSoftwareVersion: 6.3.9600.17673</span><span class="sxs-lookup"><span data-stu-id="fb5aa-145">HcsSoftwareVersion: 6.3.9600.17673</span></span>
   * <span data-ttu-id="fb5aa-146">CisAgentVersion: 1.0.9150.0</span><span class="sxs-lookup"><span data-stu-id="fb5aa-146">CisAgentVersion: 1.0.9150.0</span></span>
   * <span data-ttu-id="fb5aa-147">MdsAgentVersion: 30.0.4698.13</span><span class="sxs-lookup"><span data-stu-id="fb5aa-147">MdsAgentVersion: 30.0.4698.13</span></span>
     
     <span data-ttu-id="fb5aa-148">Sürüm numaraları güncelleştirmeyi uyguladıktan sonra değiştirmezseniz düzeltmeyi uygulamak başarısız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-148">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="fb5aa-149">Bunu görmeniz durumunda daha fazla yardım için lütfen [Microsoft Desteği](../articles/storsimple/storsimple-contact-microsoft-support.md)’ne başvurun.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
8. <span data-ttu-id="fb5aa-150">Kalan normal modu düzeltmeleri yüklemek için 3-5 adımlarını tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-150">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="fb5aa-151">LSI sürücüsü - KB3121900</span><span class="sxs-lookup"><span data-stu-id="fb5aa-151">The LSI driver - KB3121900</span></span>
   * <span data-ttu-id="fb5aa-152">Storport güncelleştirmesi - KB3080728</span><span class="sxs-lookup"><span data-stu-id="fb5aa-152">The Storport update - KB3080728</span></span>
   * <span data-ttu-id="fb5aa-153">Spaceport güncelleştirmesi - KB3090322</span><span class="sxs-lookup"><span data-stu-id="fb5aa-153">The Spaceport update - KB3090322</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="fb5aa-154">Bakım modu düzeltmelerini yüklemek ve doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="fb5aa-154">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="fb5aa-155">Disk Bellenim güncelleştirmeleri yüklemek için KB3121899 kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-155">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="fb5aa-156">Bunlar kesintiye uğratan güncelleştirmelerdir ve tamamlanması yaklaşık 30 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-156">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="fb5aa-157">Bunları cihaz seri konsoluna bağlanarak planlı bakım penceresinde yüklemeyi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-157">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="fb5aa-158">Disk üretici yazılımınız zaten güncelse bu güncelleştirmeleri yüklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-158">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="fb5aa-159">Güncelleştirmelerin mevcut olup olmadığını ve güncelleştirmelerin kesintiye uğratıp (bakım modu) uğratmayacağını (normal mod) denetlemek için cihaz seri konsolundan `Get-HcsUpdateAvailability` cmdlet’ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-159">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="fb5aa-160">Disk üretici yazılımı güncelleştirmelerini yüklemek için aşağıdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-160">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="fb5aa-161">Cihazın bakım moduna.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-161">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="fb5aa-162">Windows PowerShell uzaktan iletişimini bakım modundaki bir aygıta bağlanırken kullanmaması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-162">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="fb5aa-163">Bunun yerine bu cmdlet'i cihaz seri konsol üzerinden bağlandığında aygıt denetleyicisinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-163">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="fb5aa-164">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="fb5aa-164">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="fb5aa-165">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-165">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17664
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="fb5aa-166">İki denetleyiciye bakım moduna ardından yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-166">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="fb5aa-167">Disk üretici yazılımı güncelleştirmesini yüklemek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="fb5aa-167">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="fb5aa-168">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-168">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="fb5aa-169">`Get-HcsUpdateStatus` komutunu kullanarak yükleme ilerleme durumunu izleyin.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-169">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="fb5aa-170">`RunInProgress` değeri `False` olarak değiştiğinde güncelleştirme tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-170">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="fb5aa-171">Yükleme tamamlandıktan sonra, bakım modu düzeltmesinin yüklendiği denetleyici yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-171">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="fb5aa-172">Tam erişimle seçenek 1 olarak oturum açın ve disk üretici yazılımı sürümünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-172">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="fb5aa-173">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="fb5aa-173">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="fb5aa-174">Beklenen disk üretici yazılımı sürümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="fb5aa-174">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="fb5aa-175">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-175">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17664
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
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
   
    <span data-ttu-id="fb5aa-176">Yazılım sürümünün güncelleştirildiğinden emin olmak için ikinci denetleyicide `Get-HcsFirmwareVersion` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-176">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="fb5aa-177">Bundan sonra bakım modundan çıkabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-177">You can then exit the maintenance mode.</span></span> <span data-ttu-id="fb5aa-178">Bunu yapmak için, her bir cihaz denetleyicisi için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="fb5aa-178">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="fb5aa-179">Bakım modu çıktığınızda denetleyicilerini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-179">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="fb5aa-180">Disk üretici yazılımı güncelleştirmeleri başarıyla uygulanıp cihaz bakım modundan çıktıktan sonra, klasik Azure portalına geri dönün.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-180">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="fb5aa-181">Portal 24 saat için Bakım modu güncelleştirmeleri yüklü gösterilmeyebilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fb5aa-181">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

