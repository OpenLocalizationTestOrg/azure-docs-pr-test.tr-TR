<!--author=SharS last changed: 03/17/2016-->

#### <a name="toodownload-hotfixes"></a>toodownload düzeltmeleri
Adımları toodownload hello yazılım güncelleştirmesi aşağıdaki hello gerçekleştirin.

1. Internet Explorer'ı başlatın ve çok gidin[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Bu bilgisayarda Microsoft Update Kataloğu hello kullanarak ilk kez olursa **yükleme** zaman istendiğinde tooinstall hello Microsoft Update Kataloğu eklentisi.
    ![Katalog yükleyin](./media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)
3. Merhaba arama kutusuna hello Microsoft Update Kataloğu hello Bilgi Bankası (KB) numarasını girin hello düzeltme toodownload, örneğin istediğiniz **3063418**ve ardından **arama**.
4. Merhaba görürsünüz **StorSimple güncelleştirme 1.2 Gereci güncelleştirme** paket. **Ekle**'ye tıklayın. Merhaba güncelleştirme toohello Sepeti eklenir.
5. Ek düzeltmeleri arayın hello yukarıdaki tabloda listelenen (**3043005** ve **3063416**) ve her hello Sepeti ekleyin.
6. **Sepeti Görüntüle**’ye tıklayın.
   
    ![Sepeti görüntüle](./media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. **İndir**’e tıklayın. Belirtin veya **Gözat** tooa yerel konum istediğiniz hello tooappear indirir. Merhaba güncelleştirmelerin yükleneceği toohello konumu belirtilen ve alt hello hello update ile aynı ad ile yerleştirilir. Merhaba klasör de hello aygıttan ulaşılabilir kopyalanan tooa ağ paylaşımı olabilir.

> [!NOTE]
> Merhaba düzeltmeleri hello eş denetleyicisinden olası tüm hata iletilerini hem denetleyicileri toodetect erişilebilir olması gerekir.
> 
> 

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall ve normal modu düzeltmeleri doğrulayın
Aşağıdaki adımları tooinstall hello gerçekleştirmek ve hello normal modu düzeltmeleri doğrulayın. Bunları zaten yüklü değilse Azure Portal hello kullanarak İleri çok atlayabilirsiniz[yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes).

1. StorSimple cihaz seri konsoluna erişim hello Windows PowerShell arabiriminde tooinstall hello yazılım güncelleştirme. İzleyin hello ayrıntılı yönergeleri [kullanım PuTTy tooconnect toohello seri konsol](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Merhaba komut isteminde basın **Enter**.
2. Seçin **seçeneği 1** toolog toohello aygıtta tam erişime sahip.
3. tooinstall hello güncelleştirme paketi, hello komut istemine yazın:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Yukarıdaki komut hello paylaşım yolunda DNS yerine IP kullanın. yalnızca kimliği doğrulanmış bir paylaşım erişiyorsanız hello kimlik bilgisi parametresi kullanılır.
   
    Merhaba kimlik bilgisi parametresi tooaccess paylaşımları kullanmanızı öneririz. Çok "herkes" genellikle açık edilen bile paylaşımları toounauthenticated kullanıcılar açabilir değil.
   
    Örnek çıktı aşağıda gösterilmiştir.
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts hello hotfix installation and could reboot one or
    both of hello controllers. If hello device is serving I/Os, these will not
    be disrupted. Are you sure you want toocontinue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. Tür **Y** zaman istendiğinde tooconfirm hello düzeltme yükleme.
5. Hello kullanarak hello güncelleştirme izleyin `Get-HcsUpdateStatus` cmdlet'i.
   
    Merhaba aşağıdaki örnek çıkış hello güncelleştirme göstermektedir. Merhaba `RunInprogress` olacaktır `True` zaman hello güncelleştirme devam ediyor.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     örnek çıktı aşağıdaki hello bu hello güncelleştirme tamamlandığında gösterir. Merhaba `RunInProgress` olacaktır `False` zaman hello güncelleştirmesi tamamlandı.

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > Bazen, cmdlet raporları'nı hello `False` hello güncelleştirme devam ederken olduğunda. Düzeltme hello tooensure tamamlandığında, birkaç dakika bekleyin, bu komutu yeniden çalıştırın ve bu hello doğrulayın `RunInProgress` olan `False`. İse, hello düzeltme tamamlandı.
   > 
   > 
6. Merhaba yazılım güncelleştirmesi tamamlandıktan sonra hello sistem yazılım sürümleri doğrulayın. Merhaba aşağıdaki komutu yazın:
   
    `Get-HcsSystem`
   
    Sürümleri aşağıdaki hello görmeniz gerekir:
   
   * HcsSoftwareVersion: 6.3.9600.17584
   * CisAgentVersion: 1.0.9049.0
   * MdsAgentVersion: 26.0.4696.1433
     
     Merhaba sürüm numaralarını hello güncelleştirmeyi uyguladıktan sonra değiştirmezseniz bu hello düzeltme tooapply başarısız oldu gösterir. Bunu görmeniz durumunda daha fazla yardım için lütfen [Microsoft Desteği](../articles/storsimple/storsimple-contact-microsoft-support.md)’ne başvurun.
7. 3-5 tooinstall hello normal modu düzeltme (KB3043005) kalan adımları yineleyin.

#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall ve Bakım modu düzeltmeleri doğrulayın
KB3063416 tooinstall disk Bellenim güncelleştirmeleri kullanın. Bunlar kesintiye uğratan güncelleştirmeleri ve 30-45 dakika toocomplete alın. Bağlantı toohello cihaz seri Konsolu tarafından bu planlı bakım penceresinde tooinstall seçebilirsiniz.

tooinstall hello disk Bellenim güncelleştirmeleri aşağıdaki hello yönergeleri izleyin.

1. Merhaba aygıt bakım moduna. Windows PowerShell uzaktan iletişimini tooa aygıt, Bakım modunda bağlanırken kullanmaması gerektiğini unutmayın. Bu cmdlet hello cihaz seri konsol üzerinden bağlandığında hello aygıt denetleyicisinde toorun gerekir. Şunu yazın:
   
    `Enter-HcsMaintenanceMode`
   
    Örnek çıktı aşağıda gösterilmiştir.
   
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
   
    Hem hello denetleyicileri bakım moduna ardından yeniden başlatın.
2. tooinstall hello disk üretici yazılımı güncelleştirmesi, türü:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Örnek çıktı aşağıda gösterilmiştir.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. İzleyici hello yükleme ilerleme durumu kullanarak `Get-HcsUpdateStatus` komutu. Merhaba güncelleştirme hello zaman tamamlandıktan `RunInProgress` çok değişiklikleri`False`.
4. Merhaba yüklemesi tamamlandıktan sonra hello Bakım modu düzeltme yüklü olduğu hello denetleyicisi yeniden başlatılacak. Seçenek 1 tam erişime sahip olarak oturum açın ve hello disk bellenim sürümü doğrulayın. Şunu yazın:
   
   `Get-HcsFirmwareVersion`
   
   Merhaba beklenen disk bellenim sürümleri şunlardır:
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   Merhaba çalıştırmak `Get-HcsFirmwareVersion` , yazılım sürümü hello hello ikinci denetleyicisi tooverify komutunda güncelleştirilmiştir. Ardından hello Bakım modu çıkabilirsiniz. Merhaba komutu her aygıt denetleyicisi için aşağıdaki komutu yazın:
   
   `Exit-HcsMaintenanceMode`
5. Bakım modu çıktığınızda hello denetleyicilerini yeniden başlatın. Sonra Hello disk Bellenim güncelleştirmeleri başarıyla uygulandıktan ve hello aygıt Bakım modu, dönüş toohello Klasik Azure portalı çıkıldı. Merhaba portalınız hello Bakım modu güncelleştirmeleri 24 saat için yüklü gösterilmeyebilir unutmayın.

