<!--author=alkohli last changed: 05/19/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="f6a2e-101">Düzeltmeleri indirmek için</span><span class="sxs-lookup"><span data-stu-id="f6a2e-101">To download hotfixes</span></span>
<span data-ttu-id="f6a2e-102">Microsoft Update Kataloğu'ndan yazılım güncelleştirmesi indirmek için aşağıdaki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="f6a2e-103">Internet Explorer'ı başlatın ve [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com) adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="f6a2e-104">Microsoft Update Kataloğu’nu bu bilgisayarda ilk kez kullanıyorsanız, sorulduğunda **Yükle**’ye tıklayarak Microsoft Update Kataloğu eklentisini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="f6a2e-105">![Katalog yükleyin](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="f6a2e-105">![Install catalog](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="f6a2e-106">Microsoft Update Kataloğu arama kutusuna, örneğin, yüklemek istediğiniz düzeltme Bilgi Bankası (KB) sayısını girin **3179904**ve ardından **arama**.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3179904**, and then click **Search**.</span></span>
   
    <span data-ttu-id="f6a2e-107">Düzeltme listesi göründüğünde, örneğin, **StorSimple 8000 serisi için toplu yazılım paketini güncelleştirme 2.2**.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.2 for StorSimple 8000 Series**.</span></span>
   
    ![Katalogda arama](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="f6a2e-109">**Ekle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-109">Click **Add**.</span></span> <span data-ttu-id="f6a2e-110">Güncelleştirme sepete eklenir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="f6a2e-111">Ek düzeltmeleri arayın yukarıdaki tabloda listelenen (**3103616**, **3146621**) ve her Sepete ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-111">Search for any additional hotfixes listed in the table above (**3103616**, **3146621**), and add each to the basket.</span></span>
6. <span data-ttu-id="f6a2e-112">**Sepeti Görüntüle**’ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="f6a2e-113">**İndir**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-113">Click **Download**.</span></span> <span data-ttu-id="f6a2e-114">İndirilen öğelerin görünmesini istediğiniz yerel konumu belirtin veya **Gözat** seçeneğiyle konumu bulun.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="f6a2e-115">Güncelleştirmeleri belirtilen konuma indirilir ve güncelleştirme aynı ada sahip bir alt klasöre yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-115">The updates are downloaded to the specified location and placed in a sub-folder with the same name as the update.</span></span> <span data-ttu-id="f6a2e-116">Klasör, cihazdan erişilebilen bir ağ paylaşımına da kopyalanabilir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="f6a2e-117">Düzeltmeleri tüm olası hata iletilerini eş denetleyicisinden algılamak için her iki denetleyicilerinden erişilebilir olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="f6a2e-118">Normal mod düzeltmelerini yüklemek ve doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="f6a2e-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="f6a2e-119">Normal mod düzeltmelerini yüklemek ve doğrulamak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="f6a2e-120">İçin bunları Azure Portalı'nı kullanarak zaten yüklü değilse,'ın İleri atlayabilirsiniz [yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="f6a2e-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="f6a2e-121">Düzeltmeleri yüklemek için StorSimple cihazı seri konsolunuzdaki Windows PowerShell arabirimine erişin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="f6a2e-122">[Seri konsola bağlanmak için PuTTy kullanma](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console) bölümündeki ayrıntılı yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="f6a2e-123">Komut isteminde **Enter** tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="f6a2e-124">Cihazda tam erişimle oturum açmak için **Seçenek 1**’i belirleyin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-124">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="f6a2e-125">Düzeltmeyi ilk olarak edilgen denetleyiciye yüklemeniz önerilir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-125">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="f6a2e-126">Düzeltmeyi yüklemek için komut istemine şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="f6a2e-126">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="f6a2e-127">Yukarıdaki komuttaki paylaşım yolunda DNS yerine IP kullanın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-127">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="f6a2e-128">Kimlik bilgisi parametresi yalnızca kimliği doğrulanmış bir paylaşımdan erişiyorsanız kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-128">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="f6a2e-129">Paylaşımlara erişmek için kimlik bilgisi parametresini kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-129">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="f6a2e-130">“Herkese” açık paylaşımlar bile genellikle kimliği doğrulanmamış kullanıcılara açık değildir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-130">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="f6a2e-131">İstendiğinde parolayı belirtin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-131">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="f6a2e-132">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-132">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="f6a2e-133">Düzeltme yüklemesini onaylamak için sorulduğunda **Y** yazın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="f6a2e-134">Güncelleştirme 2.2 yüklüyorsanız, yalnızca 'tüm-hcsmdssoftwareudpate' ile başlayan ikili dosya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-134">If installing Update 2.2, only install the binary file prefaced with 'all-hcsmdssoftwareudpate'.</span></span> <span data-ttu-id="f6a2e-135">CI ve tüm cismdsagentupdatebundle ile başlayan MDS aracı güncelleştirmesi yüklemeyin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-135">Do not install the Cis and the MDS agent update prefaced with all-cismdsagentupdatebundle.</span></span> <span data-ttu-id="f6a2e-136">Bunun Sağlanamaması bir hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-136">Failure to do so will result in an error.</span></span> 

5. <span data-ttu-id="f6a2e-137">`Get-HcsUpdateStatus` cmdlet'ini kullanarak güncelleştirmeyi izleyin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-137">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="f6a2e-138">Güncelleştirme ilk olarak edilgen denetleyicide tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-138">The update will first complete on the passive controller.</span></span> <span data-ttu-id="f6a2e-139">Edilgen denetleyici güncelleştirildikten sonra yük devretme gerçekleştirilir ve bundan sonra güncelleştirme diğer denetleyiciye uygulanır.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-139">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="f6a2e-140">Her iki denetleyici de güncelleştirildiğinde güncelleştirme tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-140">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="f6a2e-141">Devam etmekte olan güncelleştirme aşağıdaki örnek çıktıda gösterilir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-141">The following sample output shows the update in progress.</span></span> <span data-ttu-id="f6a2e-142">Güncelleştirme devam ederken `RunInprogress` değeri `True` olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-142">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 5/5/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="f6a2e-143">Aşağıdaki örnek çıktıda güncelleştirmenin tamamlandığı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-143">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="f6a2e-144">Güncelleştirme tamamlandığında `RunInProgress` değeri `False` olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-144">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 5/17/2016 9:15:55 AM
    LastUpdateTimestamp : 5/17/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="f6a2e-145">Bazı durumlarda cmdlet, güncelleştirme hala devam ediyorsa `False` raporu gönderir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-145">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="f6a2e-146">Düzeltmenin tamamlandığından emin olmak için birkaç dakika bekleyin, bu komutu yeniden çalıştırın ve `RunInProgress` değerinin `False` olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-146">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="f6a2e-147">Değer değiştiyse düzeltme tamamlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-147">If it is, then the hotfix has completed.</span></span>

1. <span data-ttu-id="f6a2e-148">Yazılım güncelleştirmesi tamamlandıktan sonra sistem yazılımı sürümlerini doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-148">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="f6a2e-149">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="f6a2e-149">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="f6a2e-150">Aşağıdaki sürümleri görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f6a2e-150">You should see the following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17708`
   * `CisAgentVersion: 1.0.9299.0`
   * `MdsAgentVersion: 30.0.4698.16` 
     
     <span data-ttu-id="f6a2e-151">Sürüm numaraları güncelleştirmeyi uyguladıktan sonra değiştirmezseniz düzeltmeyi uygulamak başarısız olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-151">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="f6a2e-152">Bunu görmeniz durumunda daha fazla yardım için lütfen [Microsoft Desteği](../articles/storsimple/storsimple-contact-microsoft-support.md)’ne başvurun.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-152">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="f6a2e-153">Kalan güncelleştirmeleri uygulamadan önce etkin denetleyiciyi `Restart-HcsController` cmdlet’i ile yeniden başlatmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-153">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="f6a2e-154">Kalan normal modu düzeltmeleri yüklemek için 3-5 adımlarını tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-154">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="f6a2e-155">İSCSI güncelleştirme KB3146621</span><span class="sxs-lookup"><span data-stu-id="f6a2e-155">The iSCSI update KB3146621</span></span>
   * <span data-ttu-id="f6a2e-156">WMI güncelleştirme KB3103616</span><span class="sxs-lookup"><span data-stu-id="f6a2e-156">The WMI update KB3103616</span></span>
3. <span data-ttu-id="f6a2e-157">Güncelleştirme 2'den güncelleştiriyorsanız bu adımı atlayın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-157">Skip this step if you are updating from Update 2.</span></span> <span data-ttu-id="f6a2e-158">Güncelleştirme 2 önce bir sürümünden güncelleştiriyorsanız indirmek gerekir:</span><span class="sxs-lookup"><span data-stu-id="f6a2e-158">If you are updating from a version prior to Update 2, you will also need to download:</span></span>

    - <span data-ttu-id="f6a2e-159">LSI sürücü KB3121900</span><span class="sxs-lookup"><span data-stu-id="f6a2e-159">The LSI driver KB3121900</span></span>

    - <span data-ttu-id="f6a2e-160">KB3090322 Spaceport güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f6a2e-160">The Spaceport update KB3090322</span></span>

    - <span data-ttu-id="f6a2e-161">Storport güncelleştirme KB3080728</span><span class="sxs-lookup"><span data-stu-id="f6a2e-161">The Storport update KB3080728</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="f6a2e-162">Bakım modu düzeltmelerini yüklemek ve doğrulamak için</span><span class="sxs-lookup"><span data-stu-id="f6a2e-162">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="f6a2e-163">Disk Bellenim güncelleştirmeleri yüklemek için KB3121899 kullanın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-163">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="f6a2e-164">Bunlar kesintiye uğratan güncelleştirmelerdir ve tamamlanması yaklaşık 30 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-164">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="f6a2e-165">Bunları cihaz seri konsoluna bağlanarak planlı bakım penceresinde yüklemeyi seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-165">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="f6a2e-166">Disk üretici yazılımınız zaten güncelse bu güncelleştirmeleri yüklemeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-166">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="f6a2e-167">Güncelleştirmelerin mevcut olup olmadığını ve güncelleştirmelerin kesintiye uğratıp (bakım modu) uğratmayacağını (normal mod) denetlemek için cihaz seri konsolundan `Get-HcsUpdateAvailability` cmdlet’ini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-167">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="f6a2e-168">Disk üretici yazılımı güncelleştirmelerini yüklemek için aşağıdaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-168">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="f6a2e-169">Cihazın bakım moduna.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-169">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="f6a2e-170">Windows PowerShell uzaktan iletişimini bakım modundaki bir aygıta bağlanırken kullanmaması gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-170">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="f6a2e-171">Bunun yerine bu cmdlet'i cihaz seri konsol üzerinden bağlandığında aygıt denetleyicisinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-171">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="f6a2e-172">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="f6a2e-172">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="f6a2e-173">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-173">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="f6a2e-174">İki denetleyiciye bakım moduna ardından yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-174">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="f6a2e-175">Disk üretici yazılımı güncelleştirmesini yüklemek için şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="f6a2e-175">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="f6a2e-176">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-176">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="f6a2e-177">`Get-HcsUpdateStatus` komutunu kullanarak yükleme ilerleme durumunu izleyin.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-177">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="f6a2e-178">`RunInProgress` değeri `False` olarak değiştiğinde güncelleştirme tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-178">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="f6a2e-179">Yükleme tamamlandıktan sonra, bakım modu düzeltmesinin yüklendiği denetleyici yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-179">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="f6a2e-180">Tam erişimle seçenek 1 olarak oturum açın ve disk üretici yazılımı sürümünü doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-180">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="f6a2e-181">Şunu yazın:</span><span class="sxs-lookup"><span data-stu-id="f6a2e-181">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="f6a2e-182">Beklenen disk üretici yazılımı sürümleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f6a2e-182">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="f6a2e-183">Örnek çıktı aşağıda gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-183">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
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
   
    <span data-ttu-id="f6a2e-184">Yazılım sürümünün güncelleştirildiğinden emin olmak için ikinci denetleyicide `Get-HcsFirmwareVersion` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-184">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="f6a2e-185">Bundan sonra bakım modundan çıkabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-185">You can then exit the maintenance mode.</span></span> <span data-ttu-id="f6a2e-186">Bunu yapmak için, her bir cihaz denetleyicisi için aşağıdaki komutu yazın:</span><span class="sxs-lookup"><span data-stu-id="f6a2e-186">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="f6a2e-187">Bakım modu çıktığınızda denetleyicilerini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-187">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="f6a2e-188">Disk üretici yazılımı güncelleştirmeleri başarıyla uygulanıp cihaz bakım modundan çıktıktan sonra, klasik Azure portalına geri dönün.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-188">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="f6a2e-189">Portal 24 saat için Bakım modu güncelleştirmeleri yüklü gösterilmeyebilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f6a2e-189">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>

