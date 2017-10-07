---
title: "aaaConnect uzaktan tooyour StorSimple cihazı | Microsoft Docs"
description: "Açıklar nasıl tooconfigure Cihazınızı uzaktan yönetimi için nasıl ve ne tooconnect tooWindows HTTP veya HTTPS aracılığıyla StorSimple için PowerShell."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 55ed8fcdd997901301e0adc164a302216cde0332
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-remotely-tooyour-storsimple-8000-series-device"></a>Uzaktan tooyour StorSimple 8000 serisi aygıtı bağlayın

## <a name="overview"></a>Genel Bakış
Windows PowerShell uzaktan iletişim tooconnect tooyour StorSimple cihazı kullanabilirsiniz. Bu şekilde bağlandığınızda, menü görmezsiniz. (Yalnızca hello seri konsol hello aygıt tooconnect üzerinde kullanıyorsanız, bir menü bakın.) Windows PowerShell uzaktan iletişimini ile tooa belirli çalışma bağlayın. Merhaba görüntüleme dili de belirtebilirsiniz. 

Windows PowerShell uzaktan iletişim toomanage Cihazınızı kullanma hakkında daha fazla bilgi için çok Git[StorSimple tooadminister için Windows PowerShell'i kullanın StorSimple Cihazınızı](storsimple-windows-powershell-administration.md).

Bu öğretici açıklar nasıl tooconfigure cihazınız için uzaktan yönetim ve ardından nasıl tooconnect tooWindows StorSimple için PowerShell. Windows PowerShell uzaktan iletişimini aracılığıyla HTTP veya HTTPS tooconnect kullanabilirsiniz. Ancak, ne zaman karar tooconnect tooWindows StorSimple, PowerShell hello aşağıdaki nasıl dikkate alın: 

* Doğrudan toohello bağlanma cihaz seri konsoluna güvenlidir, ancak ağ anahtarları üzerinden bağlanan toohello seri konsol değil. Toohello cihaz seri konsoluna ağ anahtarları bağlanırken hello güvenlik riskini dikkatli olun. 
* Bir HTTP oturumu aracılığıyla bağlanma hello ağ üzerinden hello seri konsol üzerinden bağlanma daha fazla güvenlik sunar. Bu en güvenli yöntemi hello olmamasına karşın, güvenilen ağlarda kabul edilebilir. 
* Kendinden imzalı bir sertifika ile HTTPS oturumu aracılığıyla bağlanma hello en güvenli ve önerilen seçenek hello olur.

Toohello Windows PowerShell arabirimi uzaktan bağlanabilirsiniz. Ancak, uzaktan erişim tooyour StorSimple cihazı hello Windows PowerShell arabirimi üzerinden varsayılan olarak etkin değildir. Hello cihazda uzaktan yönetimi tooenable önce gerekir ve ardından üzerinde Cihazınızı kullanılan tooaccess istemcisi hello.

Bu makalede açıklanan başlangıç adımları Windows Server 2012 R2 çalıştıran bir konak sisteminde gerçekleştirilmiştir.

## <a name="connect-through-http"></a>HTTP bağlanma
TooWindows PowerShell StorSimple için bir HTTP oturumu aracılığıyla bağlanma hello seri konsol StorSimple cihazınızın üzerinden bağlanma daha fazla güvenlik sunar. Bu en güvenli yöntemi hello olmamasına karşın, güvenilen ağlarda kabul edilebilir.

Merhaba Klasik Azure portalı veya hello seri konsol tooconfigure uzaktan yönetimi kullanabilirsiniz. Yordamları izleyerek hello seçin:

* [HTTP üzerinden Hello Azure Klasik portalı tooenable Uzaktan Yönetimi'ni kullanın](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [HTTP üzerinden Hello seri konsol tooenable Uzaktan Yönetimi'ni kullanın](#use-the-serial-console-to-enable-remote-management-over-http)

Uzaktan Yönetimi etkinleştirdikten sonra uzak bağlantı için yordamı tooprepare hello istemcisi aşağıdaki hello kullanın.

* [İçin Uzak bağlantı Hello istemcisini hazırla](#prepare-the-client-for-remote-connection)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-http"></a>HTTP üzerinden Hello Azure Klasik portalı tooenable Uzaktan Yönetimi'ni kullanın
HTTP üzerinden adımlara hello Azure Klasik portalı tooenable Uzaktan Yönetimi'nde hello gerçekleştirin.

#### <a name="tooenable-remote-management-through-hello-azure-classic-portal"></a>Merhaba Klasik Azure portalı üzerinden tooenable uzaktan yönetim
1. Erişim **aygıtları** > **yapılandırma** cihazınız için.
2. Toohello aşağı **uzaktan yönetimi** bölümü.
3. Ayarlama **uzaktan yönetimini etkinleştirme** çok**Evet**.
4. Artık HTTP kullanarak tooconnect seçebilirsiniz. (Merhaba tooconnect HTTPS üzerinden varsayılandır.) HTTP seçili olduğundan emin olun.
   
   > [!NOTE]
   > HTTP üzerinden bağlanma yalnızca güvenilen ağlarda kabul edilebilir.
   > 
   > 
5. Tıklatın **kaydetmek** hello sayfanın hello sonundaki.

### <a name="use-hello-serial-console-tooenable-remote-management-over-http"></a>HTTP üzerinden Hello seri konsol tooenable Uzaktan Yönetimi'ni kullanın
Aşağıdaki adımları hello cihaz seri konsoluna tooenable uzaktan yönetimi hello gerçekleştirin.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>tooenable hello cihaz seri Konsolu aracılığıyla uzaktan yönetim
1. Merhaba seri konsol menüsünde 1 seçeneğini belirleyin. Hello aygıtta hello seri Konsolu kullanma hakkında daha fazla bilgi için çok Git[tooWindows PowerShell StorSimple için cihaz seri konsoluna bağlanmak](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Merhaba istemine yazın:`Enable-HcsRemoteManagement –AllowHttp`
3. HTTP tooconnect toohello cihaz kullanımının hello güvenlik açıkları hakkında size bildirilecek. İstendiğinde, yazarak onaylayın **Y**.
4. HTTP yazarak etkin olduğunu doğrulayın:`Get-HcsSystem`
5. Bu hello doğrulayın **RemoteManagementMode** alan gösterir **HttpsAndHttpEnabled**çizim aşağıdaki .hello PuTTY bu ayarları gösterir.
   
     ![Seri HTTPS ve HTTP Etkin](./media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-hello-client-for-remote-connection"></a>İçin Uzak bağlantı Hello istemcisini hazırla
Aşağıdaki adımları hello istemci tooenable uzaktan yönetimi hello gerçekleştirin.

#### <a name="tooprepare-hello-client-for-remote-connection"></a>Uzak bağlantı için tooprepare hello istemcisi
1. Bir Windows PowerShell oturumu yönetici olarak başlatın.
2. Merhaba komutu tooadd hello IP adresini hello StorSimple cihaz toohello istemcinin güvenilir konaklar listesine aşağıdaki komutu yazın: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     Değiştir <*device_ip*> merhaba IP adresiyle Cihazınızı; örneğin: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Bir değişken komutu toosave hello aygıt kimlik bilgilerini aşağıdaki hello yazın: 
   
    ```
    $cred = Get-Credential
    ```
    
4. Merhaba iletişim kutusu görüntülenir:
   
   1. Tür hello kullanıcı adı şu biçimde: *device_ip\SSAdmin*.
   2. Hello aygıt hello Kurulum Sihirbazı ile yapılandırıldığında bu ayarlanan hello cihaz Yöneticisi parolasını yazın. Merhaba varsayılan parola *Parola1*.
5. Bir Windows PowerShell oturumunda aşağıdaki komutu yazarak hello cihazda başlatın:
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > toocreate hello StorSimple sanal cihazı ile kullanmak için Windows PowerShell oturumu sona hello `–Port` parametre ve Remoting StorSimple sanal Gereci için yapılandırılan hello genel bağlantı noktası belirtin.
   > 
   > 
   
     Bu noktada, bir etkin uzaktan Windows PowerShell oturumu toohello cihaz olması gerekir.
   
    ![HTTP kullanarak PowerShell uzaktan iletişim](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a>HTTPS bağlanır
TooWindows PowerShell StorSimple için bir HTTPS oturumu aracılığıyla bağlanma hello en güvenli olduğundan ve uzaktan bağlanan tooyour Microsoft Azure StorSimple cihaz yöntemi önerilir. yordamları izleyerek hello nasıl tooset yukarı hello seri konsol ve istemci bilgisayarları için StorSimple HTTPS tooconnect tooWindows PowerShell kullanabilmesi açıklanmaktadır.

Merhaba Klasik Azure portalı veya hello seri konsol tooconfigure uzaktan yönetimi kullanabilirsiniz. Yordamları izleyerek hello seçin:

* [HTTPS üzerinden Hello Azure Klasik portalı tooenable Uzaktan Yönetimi'ni kullanın](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [HTTPS üzerinden Hello seri konsol tooenable Uzaktan Yönetimi'ni kullanın](#use-the-serial-console-to-enable-remote-management-over-https)

Uzaktan Yönetimi etkinleştirdikten sonra Uzaktan Yönetim için yordamlar tooprepare hello konak aşağıdaki hello kullanın ve toohello aygıt hello uzak ana bilgisayara bağlanın.

* [Merhaba konak uzaktan yönetimi için hazırlama](#prepare-the-host-for-remote-management)
* [Toohello aygıt hello uzak ana bilgisayara bağlanın](#connect-to-the-device-from-the-remote-host)

### <a name="use-hello-azure-classic-portal-tooenable-remote-management-over-https"></a>HTTPS üzerinden Hello Azure Klasik portalı tooenable Uzaktan Yönetimi'ni kullanın
HTTPS üzerinden adımlara hello Azure Klasik portalı tooenable Uzaktan Yönetimi'nde hello gerçekleştirin.

#### <a name="tooenable-remote-management-over-https-from-hello-azure-classic-portal"></a>tooenable hello Klasik Azure Portalı'den HTTPS üzerinden uzaktan yönetim
1. Erişim **aygıtları** > **yapılandırma** cihazınız için.
2. Toohello aşağı **uzaktan yönetimi** bölümü.
3. Ayarlama **uzaktan yönetimini etkinleştirme** çok**Evet**.
4. Artık HTTPS kullanarak tooconnect seçebilirsiniz. (Merhaba tooconnect HTTPS üzerinden varsayılandır.) HTTPS seçili olduğundan emin olun. 
5. Tıklatın **uzak yönetim sertifikası indir**. Konum toosave bu dosyayı belirtin. Bu sertifika tooconnect toohello aygıtını kullanacak hello istemci veya konak bilgisayarda tooinstall gerekir.
6. Tıklatın **kaydetmek** hello sayfanın hello sonundaki.

### <a name="use-hello-serial-console-tooenable-remote-management-over-https"></a>HTTPS üzerinden Hello seri konsol tooenable Uzaktan Yönetimi'ni kullanın
Aşağıdaki adımları hello cihaz seri konsoluna tooenable uzaktan yönetimi hello gerçekleştirin.

#### <a name="tooenable-remote-management-through-hello-device-serial-console"></a>tooenable hello cihaz seri Konsolu aracılığıyla uzaktan yönetim
1. Merhaba seri konsol menüsünde 1 seçeneğini belirleyin. Hello aygıtta hello seri Konsolu kullanma hakkında daha fazla bilgi için çok Git[tooWindows PowerShell StorSimple için cihaz seri konsoluna bağlanmak](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).
2. Merhaba istemine yazın: 
   
     `Enable-HcsRemoteManagement`
   
    Bu, Cihazınızda HTTPS etkinleştirmeniz gerekir.
3. Yazarak HTTPS etkin olduğunu doğrulayın: 
   
     `Get-HcsSystem`
   
    Bu hello emin olun **RemoteManagementMode** alan gösterir **HttpsEnabled**çizim aşağıdaki .hello PuTTY bu ayarları gösterir.
   
     ![Seri HTTPS etkin](./media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. Hello çıktısından `Get-HcsSystem`, kopyalama hello aygıtının hello seri numarasını ve daha sonra kullanmak üzere kaydedin.
   
   > [!NOTE]
   > Merhaba seri numarası toohello CN adı hello sertifikasında eşler.
   > 
   > 
5. Uzak Yönetim sertifikası yazarak alın: 
   
     `Get-HcsRemoteManagementCert`
   
    Sertifika benzer toohello aşağıdaki görünür.
   
    ![Uzaktan Yönetim sertifikası alma](./media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. Hello bilgi hello sertifikadan kopyalayın **---başlangıç sertifika---** çok**---son SERTİFİKAYI---** .cer dosyası olarak bir metin düzenleyicisine Not Defteri gibi ve kaydedin. (Merhaba konak hazırlarken bu dosya tooyour uzak ana kopyalayacak.)
   
   > [!NOTE]
   > toogenerate yeni bir sertifika kullanmak hello `Set-HcsRemoteManagementCert` cmdlet'i.
   > 
   > 

### <a name="prepare-hello-host-for-remote-management"></a>Merhaba konak uzaktan yönetimi için hazırlama
tooprepare hello ana bilgisayar kullanan bir HTTPS oturumu uzaktan bağlantı hello yordamları gerçekleştirin:

* [İçeri aktarma hello .cer dosyası hello istemci ya da uzak ana hello kök deposuna](#to-import-the-certificate-on-the-remote-host).
* [Merhaba cihaz seri numaraları toohello hosts dosyasını uzak ana bilgisayarınızda eklemek](#to-add-device-serial-numbers-to-the-remote-host).

Bu yordamların her biri aşağıda açıklanmıştır.

#### <a name="tooimport-hello-certificate-on-hello-remote-host"></a>Merhaba uzak ana bilgisayarda tooimport hello sertifika
1. Merhaba .cer dosyasını sağ tıklatın ve seçin **yükleme sertifika**. Bu hello Sertifika Alma Sihirbazı'nı başlatır.
   
    ![Sertifika Alma Sihirbazı 1](./media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. İçin **depo konumuna**seçin **yerel makine**ve ardından **sonraki**.
3. Seçin **tüm sertifikaları deposu aşağıdaki hello Yerleştir**ve ardından **Gözat**. Uzak ana bilgisayarınız toohello bir kök depoya gidin ve ardından **sonraki**.
   
    ![Sertifika Alma Sihirbazı'nı 2](./media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. **Son**'a tıklayın. Merhaba alma işleminin başarılı olduğunu bildiren bir ileti görüntülenir.
   
    ![Sertifika Alma Sihirbazı'nı 3](./media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="tooadd-device-serial-numbers-toohello-remote-host"></a>tooadd cihaz seri numaraları toohello uzak ana bilgisayar
1. Not Defteri'ni yönetici olarak başlatın ve sonra \Windows\System32\Drivers\etc bulunan hello hosts dosyasını açın.
2. Aşağıdaki üç girişleri tooyour hosts dosyasına hello ekleyin: **veri 0 IP adresi**, **denetleyici 0 sabit IP adresi**, ve **Denetleyici 1 sabit IP adresi**.
3. Daha önce kaydettiğiniz Hello cihaz seri numarasını girin. Bu toohello IP adresini hello görüntü aşağıdaki gösterildiği gibi eşleyin. Denetleyici 0 ve denetleyici 1 için sona **Controller0** ve **Controller1** hello sonunda hello seri numarası (CN adı).
   
    ![CN adı toohosts dosyası ekleme](./media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. Kaydet hello hosts dosyasını.

### <a name="connect-toohello-device-from-hello-remote-host"></a>Toohello aygıt hello uzak ana bilgisayara bağlanın
Windows PowerShell ve SSL kullanmak SSAdmin oturum bir uzak ana bilgisayara veya istemci, Cihazınızda bir tooenter. Merhaba SSAdmin oturum eşlemeleri toooption 1 hello içinde [seri konsol](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) Cihazınızı menüsü.

Aşağıdaki yordamı toomake hello uzaktan Windows PowerShell bağlantı istediğiniz hello bilgisayarda hello gerçekleştirin.

#### <a name="tooenter-an-ssadmin-session-on-hello-device-by-using-windows-powershell-and-ssl"></a>bir Windows PowerShell ve SSL kullanarak hello aygıt SSAdmin oturum tooenter
1. Bir Windows PowerShell oturumu yönetici olarak başlatın.
2. Merhaba aygıt IP adresi toohello istemcinin güvenilir konaklar yazarak ekleyin:
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    Burada <*device_ip*> Cihazınızı hello IP adresidir; örneğin: 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. Yeni bir kimlik bilgisi yazarak oluşturun: 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    Burada <*hedef aygıtın IP*> hello IP adresi veri 0 aygıtınızın; Örneğin, **10.126.173.90** hello hosts dosyasını görüntüsü önceki hello gösterildiği gibi. Ayrıca, Cihazınızı hello yönetici parolasını sağlayın.
4. Bir oturum yazarak oluşturun:
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    Merhaba - ComputerName parametresi için Merhaba, hello sağlayın <*hedef cihaz seri numarasını*>. Bu seri numarasına eşlendi veri uzak ana bilgisayarınızda; hello hosts dosyasında 0 toohello IP adresi Örneğin, **SHX0991003G44MT** hello görüntü aşağıdaki gösterildiği gibi.
5. Şunu yazın: 
   
     `Enter-PSSession $session`
6. Birkaç dakika toowait gerekir ve ardından HTTPS üzerinden bağlı tooyour aygıt SSL üzerinden olacaktır. Bağlı tooyour aygıt olduğunuz belirten bir ileti görürsünüz.
   
    ![PowerShell uzaktan iletişimini HTTPS ve SSL kullanma](./media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [Windows PowerShell tooadminister StorSimple Cihazınızı kullanarak](storsimple-windows-powershell-administration.md).
* Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

