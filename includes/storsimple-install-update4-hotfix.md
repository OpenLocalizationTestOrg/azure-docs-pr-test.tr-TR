<!--author=alkohli last changed: 02/10/17-->

#### <a name="toodownload-hotfixes"></a>toodownload düzeltmeleri

Hello Microsoft Update Kataloğu ' adımları toodownload hello yazılım güncelleştirmesi aşağıdaki hello gerçekleştirin.

1. Internet Explorer'ı başlatın ve çok gidin[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Bu bilgisayarda Microsoft Update Kataloğu hello kullanarak ilk kez olursa **yükleme** zaman istendiğinde tooinstall hello Microsoft Update Kataloğu eklentisi.

    ![Katalog yükleme](./media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. Merhaba arama kutusuna hello Microsoft Update Kataloğu hello Bilgi Bankası (KB) numarasını girin hello düzeltme toodownload, örneğin istediğiniz **4011839**ve ardından **arama**.
   
    Merhaba düzeltme listesi, örneğin, göründüğünde **StorSimple 8000 serisi için toplu yazılım paketini güncelleştirme 4.0**.
   
    ![Katalogda arama](./media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)

4. **İndir**’e tıklayın. Belirtin veya **Gözat** tooa yerel konum istediğiniz hello tooappear indirir. Merhaba dosyaları toodownload toohello belirtilen konuma ve klasör. Merhaba klasör de hello aygıttan ulaşılabilir kopyalanan tooa ağ paylaşımı olabilir.
5. Ek düzeltmeleri arayın hello yukarıdaki tabloda listelenen (**4011841**), ve indirme hello karşılık gelen dosyaları belirli klasörleri toohello tablo önceki hello listelendiği gibi.

> [!NOTE]
> Merhaba düzeltmeleri hello eş denetleyicisinden olası tüm hata iletilerini hem denetleyicileri toodetect erişilebilir olması gerekir.
>
> Merhaba düzeltmeleri 3 ayrı klasörlerde kopyalanmalıdır. Örneğin, hello aygıt CIS/software/MDS aracı güncelleştirmesi içinde kopyalanabilir _FirstOrderUpdate_ klasörü, tüm hello benzer diğer güncelleştirmeleri hello kopyalanamadı _SecondOrderUpdate_ klasörü, ve Bakım modu güncelleştirmeleri içinde kopyalanan _ThirdOrderUpdate_ klasör.

#### <a name="tooinstall-and-verify-regular-mode-hotfixes"></a>tooinstall ve normal modu düzeltmeleri doğrulayın

Aşağıdaki adımları tooinstall hello gerçekleştirmek ve normal modu düzeltmeleri doğrulayın. Bunları zaten yüklediyseniz, Klasik Azure portalı hello kullanarak İleri çok atlayabilirsiniz[yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes).

1. tooinstall hello düzeltmeleri, StorSimple cihaz seri konsoluna erişim hello Windows PowerShell arabiriminde. İzleyin hello ayrıntılı yönergeleri [kullanım PuTTy tooconnect toohello seri konsol](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console). Merhaba komut isteminde basın **Enter**.
2. Seçin **seçeneği 1** toolog toohello aygıtta tam erişime sahip. Hello düzeltmeyi hello pasif denetleyicisinde ilk yüklemenizi öneririz.
3. Merhaba komut isteminde türü tooinstall hello düzeltme:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Yukarıdaki komut hello paylaşım yolunda DNS yerine IP kullanın. yalnızca kimliği doğrulanmış bir paylaşım erişiyorsanız hello kimlik bilgisi parametresi kullanılır.
   
    Merhaba kimlik bilgisi parametresi tooaccess paylaşımları kullanmanızı öneririz. Çok "herkes" genellikle açık edilen bile paylaşımları toounauthenticated kullanıcılar açabilir değil.
   
    İstendiğinde hello parolasını sağlayın.
   
    Merhaba ilk sipariş güncelleştirmeleri yüklemek için örnek bir çıktı aşağıda gösterilmiştir. Merhaba ilk sipariş güncelleştirmesi toopoint toohello belirli dosya gerekir.
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts hello hotfix installation and could reboot one or
        both of hello controllers. If hello device is serving I/Os, these will not
        be disrupted. Are you sure you want toocontinue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. Tür **Y** zaman istendiğinde tooconfirm hello düzeltme yükleme.
5. Hello kullanarak hello güncelleştirme izleyin `Get-HcsUpdateStatus` cmdlet'i. Hello güncelleştirme hello pasif denetleyicisinde önce tamamlanır. Merhaba pasif denetleyici güncelleştirildikten sonra bir yük devretme olacaktır ve hello güncelleştirme sonra üzerinde uygulanacağını diğer denetleyicisi hello. hem hello denetleyicileri güncelleştirildiğinde hello güncelleştirme tamamlanır.
   
    Merhaba aşağıdaki örnek çıkış hello güncelleştirme göstermektedir. Merhaba `RunInprogress` olacaktır `True` zaman hello güncelleştirme devam ediyor.

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     örnek çıktı aşağıdaki hello bu hello güncelleştirme tamamlandığında gösterir. Merhaba `RunInProgress` olacaktır `False` zaman hello güncelleştirmesi tamamlandı.
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > Bazen, cmdlet raporları'nı hello `False` hello güncelleştirme devam ederken olduğunda. Düzeltme hello tooensure tamamlandığında, birkaç dakika bekleyin, bu komutu yeniden çalıştırın ve bu hello doğrulayın `RunInProgress` olan `False`. İse, hello düzeltme tamamlandı.

6. Merhaba yazılım güncelleştirmesi tamamlandıktan sonra hello sistem yazılım sürümleri doğrulayın. Şunu yazın:
   
    `Get-HcsSystem`
   
    Sürümleri aşağıdaki hello görmeniz gerekir:
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    Merhaba sürüm numarası değişmez hello güncelleştirmeyi uyguladıktan sonra o hello düzeltme tooapply başarısız oldu gösterir. Bunu görmeniz durumunda daha fazla yardım için lütfen [Microsoft Desteği](../articles/storsimple/storsimple-contact-microsoft-support.md)’ne başvurun.
     
    > [!IMPORTANT]
    > Merhaba etkin denetleyicisi hello aracılığıyla yeniden başlatmanız gerekir `Restart-HcsController` uygulamadan önce cmdlet hello sonraki güncelleştirme.
     
7. 3-5 tooinstall hello CIS/MDS indirilen Aracısı tooyour arasındaki adımları yineleyin _FirstOrderUpdate_ klasör. 
8. Adım 3-5 tooinstall hello ikinci sipariş güncelleştirmeleri yineleyin. **İkinci sipariş güncelleştirmeleri hello çalıştırarak birden çok güncelleştirme yüklenebilir `Start-HcsHotfix cmdlet` ve ikinci sipariş güncelleştirmeleri bulunduğu işaret toohello klasör. hello cmdlet hello klasöründe kullanılabilir tüm hello güncelleştirmeleri yürütülecek.** Bir güncelleştirmeyi zaten yüklediyseniz, hello güncelleştirme mantığı algılayan ve bu güncelleştirmenin geçerli değil. 

Tüm hello düzeltmeleri yüklendikten sonra hello kullanılacak `Get-HcsSystem` cmdlet'i. Merhaba sürümleri olmalıdır:

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="tooinstall-and-verify-maintenance-mode-hotfixes"></a>tooinstall ve Bakım modu düzeltmeleri doğrulayın
KB4011837 tooinstall disk Bellenim güncelleştirmeleri kullanın. Bunlar kesintiye uğratan güncelleştirmeleri ve yaklaşık 30 dakika toocomplete alın. Bağlantı toohello cihaz seri Konsolu tarafından bu planlı bakım penceresinde tooinstall seçebilirsiniz.

Disk bellenim zaten güncel ise, bu güncelleştirmeleri tooinstall gerek kalmaz unutmayın. Merhaba çalıştırmak `Get-HcsUpdateAvailability` güncelleştirmeleri kullanılabilir ve olup hello hello cihaz seri konsoluna toocheck cmdlet'inden güncelleştirmeleri olan kesintiye uğratan (Bakım modu) veya benzer (normal modu) güncelleştirmeleri.

tooinstall hello disk Bellenim güncelleştirmeleri aşağıdaki hello yönergeleri izleyin.

1. Merhaba aygıt hello bakım moduna. **Windows PowerShell uzaktan iletişimini tooa aygıt, Bakım modunda bağlanırken kullanmaması gerektiğini unutmayın. Bunun yerine bu cmdlet'i hello cihaz seri konsol üzerinden bağlandığında hello aygıt denetleyicisi çalıştırın.** Şunu yazın:
   
    `Enter-HcsMaintenanceMode`
   
    Örnek çıktı aşağıda gösterilmiştir.
   
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
   
    Hem hello denetleyicileri bakım moduna ardından yeniden başlatın.
2. tooinstall hello disk üretici yazılımı güncelleştirmesi, türü:
   
    `Start-HcsHotfix -Path <path tooupdate file> -Credential <credentials in domain\username format>`
   
    Örnek çıktı aşağıda gösterilmiştir.
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After hello hotfix is installed on this controller, install it on hello peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of hello controllers. By installing new updates you agree to, and accept any additional terms associated with, hello new functionality listed in hello release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want toocontinue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes toocomplete.
3. İzleyici hello yükleme ilerleme durumu kullanarak `Get-HcsUpdateStatus` komutu. Merhaba güncelleştirme hello zaman tamamlandıktan `RunInProgress` çok değişiklikleri`False`.
4. Merhaba yüklemesi tamamlandıktan sonra hangi hello üzerinde Bakım modu düzeltme yüklü hello denetleyicisi yeniden başlatır. Seçenek 1 tam erişime sahip olarak oturum açın ve hello disk bellenim sürümü doğrulayın. Şunu yazın:
   
   `Get-HcsFirmwareVersion`
   
   Merhaba beklenen disk bellenim sürümleri şunlardır:
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   Örnek çıktı aşağıda gösterilmiştir.
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17820
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
   
    Merhaba çalıştırmak `Get-HcsFirmwareVersion` , yazılım sürümü hello hello ikinci denetleyicisi tooverify komutunda güncelleştirilmiştir. Ardından hello Bakım modu çıkabilirsiniz. toodo, bu nedenle, her cihaz denetleyicisi için komutu aşağıdaki hello yazın:
   
   `Exit-HcsMaintenanceMode`

5. Bakım modu çıktığınızda hello denetleyicilerini yeniden başlatın. Sonra Hello disk Bellenim güncelleştirmeleri başarıyla uygulandıktan ve hello aygıt Bakım modu, dönüş toohello Klasik Azure portalı çıkıldı. Merhaba portalınız hello Bakım modu güncelleştirmeleri 24 saat için yüklü gösterilmeyebilir unutmayın.

