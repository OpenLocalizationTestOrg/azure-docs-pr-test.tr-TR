---
title: "Azure yedekleme: Sistem durumunu geri yükle tooa Windows Server | Microsoft Docs"
description: "Windows Server sistem durumu azure'da bir yedekten geri yüklemek için adım açıklama tarafından adım."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/18/2017
ms.author: saurse;trinadhk;markgal;
ms.openlocfilehash: a45506507f53e2744350d3b6b2e52f1db415de4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-system-state-toowindows-server"></a>Sistem durumunu geri yükle tooWindows sunucu

Bu makalede nasıl toorestore Windows Server sistem durumu yedeklemeleri Azure kurtarma Hizmetleri kasası açıklanmaktadır. toorestore sistem durumu, bir sistem durumu yedeklemesi olması gerekir (Merhaba yönergelerinde kullanılarak oluşturulan [sistem durumu yedekleme](backup-azure-system-state.md#back-up-windows-server-system-state-preview)) ve hello yüklediğinizden emin olun [hello Microsoft Azure Recovery en son sürümü Hizmetleri (MARS) aracısı](http://aka.ms/azurebackup_agent). Azure kurtarma Hizmetleri Kasası'nı Windows Server Sistem Durumu verilerini kurtarma iki adımlı bir işlemdir:

1. Sistem durumu, Azure yedekleme dosyalarını farklı geri yükle. Azure yedekleme dosyalarından olarak sistem durum geri yüklerken şunlardan birini yapabilirsiniz:
  * Sistem durumunu geri yükle toohello burada hello yedeklemeleri gerçekleştirilecek, aynı sunucuya veya
  * Sistem durumunu geri yükle dosya tooan alternatif sunucusu.

2. Geri hello sistem durumu dosyaları tooa Windows Server uygulayın.


## <a name="recover-system-state-files-toohello-same-server"></a>Sistem durumunu kurtarma dosyaları toohello aynı sunucu
Aşağıdaki adımları hello nasıl tooroll, Windows Server yapılandırması tooa önceki durumuna geri açıklanmaktadır. Sunucunuz, kararlı durum bilinen yapılandırma geri tooa çalışırken çok yararlı olabilir. Kurtarma Hizmetleri Kasası'nı adımları geri yükleme hello sunucunun sistem durumunu izleyen hello. 

1. Açık hello **Microsoft Azure yedekleme** ek bileşenini. Merhaba ek bileşenini yüklendiği bilmiyorsanız, hello bilgisayar veya sunucu için arama **Microsoft Azure yedekleme**.

    Merhaba masaüstü uygulaması hello arama sonuçlarında görüntülenmesi gerekir.

2. Tıklatın **verileri kurtarabilirsiniz** toostart hello Sihirbazı.

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server/recover.png)

3. Merhaba üzerinde **Başlarken** bölmesi, toorestore hello veri toohello aynı sunucu bilgisayar seçin veya **bu sunucu (`<server name>`)** tıklatıp **sonraki**.

    ![Bu sunucu seçeneği toorestore hello veri toohello seçin aynı makine](./media/backup-azure-restore-system-state/samemachine.png)

4. Merhaba üzerinde **seçin kurtarma moduna** bölmesinde seçin **sistem durumu** ve ardından **sonraki**.

    ![Gözatma dosyaları](./media/backup-azure-restore-system-state/recover-type-selection.png)

5. Merhaba takvimde **birim seçin ve tarih** bölmesinde seçin kurtarma noktası. 

    Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz. İçinde tarihleri **kalın** hello en az bir kurtarma noktası kullanılabilirliğini gösterir. Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra hello hello belirli bir kurtarma noktası seçin **zaman** açılır menü.

    ![Birimi ve tarih](./media/backup-azure-restore-system-state/select-date.png)

6. Merhaba kurtarma noktası toorestore seçtikten sonra tıklatın **sonraki**.

    Azure yedekleme hello yerel kurtarma noktası bağlar ve kurtarma birimi olarak kullanır.

7. Merhaba sonraki bölme hello hedef hello için sistem durumu dosyaları kurtarılan belirtin ve tıklatın **Gözat** tooopen Windows Gezgini, Bul hello dosya ve klasörleri istiyor. Merhaba seçeneği **böylece her iki sürümünü de sahip kopya oluşturma**, hello tüm sistem durumu arşiv hello kopyasını oluşturmak yerine var olan bir sistem durumu Dosya arşiv tek tek dosyaların kopyalarını oluşturur.

    ![Kurtarma Seçenekleri](./media/backup-azure-restore-system-state/recover-as-files.png)

8. Merhaba kurtarma Hello ayrıntılarını doğrulayın **onay** bölmesinde ve tıklatın **kurtarmak**.

   ![Kurtarma tooacknowledge hello kurtarma eylemini tıklatın](./media/backup-azure-restore-system-state/confirm-recovery.png)

9. Kopya hello *WindowsImageBackup* hello kurtarma hedef tooa kritik olmayan birim hello sunucusunun dizin. Genellikle, Windows işletim sistemi birimi hello hello kritik birim değil.

10. Merhaba kurtarma başarılı olduktan sonra hello hello bölümdeki adımları [Uygula geri sistem durumu dosyaları toohello Windows Server](backup-azure-restore-system-state.md#apply-restored-system-state-files-to-the-windows-server), toocomplete hello sistem durumu kurtarma işlemi.

## <a name="recover-system-state-files-tooan-alternate-server"></a>Sistem durumunu kurtarma dosyaları tooan diğer sunucu

Windows Server'ınızın bozuk veya erişilemez durumda ve toorestore istiyorsanız, Windows Server sistem durumu kurtarma tarafından tooa kararlı durum Merhaba, başka bir sunucudan hello bozuk sunucunun sistem durumu geri yükleyebilirsiniz. Adımları toohello geri yükleme Sistem Durumu'nu ayrı bir sunucu üzerinde aşağıdaki hello kullanın.  

Bu adımlarda kullanılan hello terminolojisi içerir:

- *Kaynak makine* – hello özgün makine hangi hello yedekten alındığı ve hangi şu anda kullanılamıyor.
- *Hedef makine* – hello makine toowhich hello verilerin kurtarıldığı.
- *Örnek kasa* – hello kurtarma Hizmetleri kasası toowhich hello *kaynak makine* ve *hedef makine* kaydedilir. <br/>

> [!NOTE]
> Bir makineden alınan yedekleri geri yüklenen tooa makine hello işletim sisteminin önceki bir sürümünü çalıştıran olamaz. Örneğin, bir Windows Server makine olamaz 2016'dan alınan yedeklemeler tooWindows Server 2012 R2 geri. Ancak, hello ters mümkündür. Windows Server 2012 R2 toorestore Windows Server 2016 yedeklemelerden kullanabilirsiniz.
>

1. Açık hello **Microsoft Azure yedekleme** ek bileşenini hello *hedef makine*.
2. Bu hello olun *hedef makine* ve hello *kaynak makine* aynı kurtarma Hizmetleri kasası kayıtlı toohello şunlardır.
3. Tıklatın **verileri kurtarabilirsiniz** tooinitiate hello iş akışı.

    ![Verileri kurtarma](./media/backup-azure-restore-windows-server-classic/recover.png)

4. Seçin **başka bir sunucu**

    ![Başka bir sunucu](./media/backup-azure-restore-system-state/anotherserver.png)

5. Toohello karşılık gelen hello kasa kimlik bilgilerini sağlayın *örnek kasa*. Merhaba kasa kimlik bilgilerini geçersiz (veya süresi dolmuş) varsa, yeni bir kasa kimlik bilgilerini hello indirin *örnek kasa* hello Azure Portalı'nda. Merhaba kasa kimlik bilgilerini sağlanan sonra hello kasa kimlik bilgileri dosyasıyla ilişkili hello kurtarma Hizmetleri kasası görünür.

6. Merhaba Hello yedekleme sunucusu seçin bölmesinde seçin *kaynak makine* görüntülenmesini makineler hello listesinden.

    ![Makineler listesi](./media/backup-azure-restore-windows-server-classic/machinelist.png)

7. Merhaba seçin kurtarma moduna bölmesinde seçin **sistem durumu** tıklatıp **sonraki**. 

    ![Arama](./media/backup-azure-restore-system-state/recover-type-selection.png)

8. Merhaba hello Takvim üzerinde **birim seçin ve tarih** bölmesinde seçin kurtarma noktası. Zaman içinde herhangi bir kurtarma noktasından geri yükleyebilirsiniz. İçinde tarihleri **kalın** hello en az bir kurtarma noktası kullanılabilirliğini gösterir. Birden fazla kurtarma noktası mevcutsa, bir tarih seçtikten sonra hello hello belirli bir kurtarma noktası seçin **zaman** açılır menü. 

    ![Arama öğeleri](./media/backup-azure-restore-system-state/select-date.png)

9. Merhaba kurtarma noktası toorestore seçtikten sonra tıklatın **sonraki**.

10. Merhaba üzerinde **sistem durumu kurtarma modunu seçin** bölmesinde istediğiniz sistem durumu dosyaları kurtarılan toobe hello hedefini belirtin ve ardından **sonraki**.

    ![Şifreleme](./media/backup-azure-restore-system-state/recover-as-files.png)

    Merhaba seçeneği **böylece her iki sürümünü de sahip kopya oluşturma**, hello tüm sistem durumu arşiv hello kopyasını oluşturmak yerine var olan bir sistem durumu Dosya arşiv tek tek dosyaların kopyalarını oluşturur.

11. Kurtarma hello onay bölmesinde Hello ayrıntılarını doğrulayın ve tıklatın **kurtarmak**. 

    ![Merhaba Kurtar düğmesi tooconfirm hello kurtarma işlemi'ı tıklatın](./media/backup-azure-restore-system-state/confirm-recovery.png)

12. Kopya hello *WindowsImageBackup* directory tooa kritik olmayan birim hello sunucusunun (örneğin D:\). Genellikle Windows işletim sistemi birimi hello hello kritik birim değil.

13. toocomplete hello kurtarma işlemi, kullanım hello aşağıdaki bölümü çok[geri hello sistem durumu dosyaları bir Windows sunucusu üzerindeki geçerli](backup-azure-restore-system-state.md#apply-restored-system-state-on-a-windows-server).




## <a name="apply-restored-system-state-on-a-windows-server"></a>Bir Windows sunucusuna geri yüklenen sistem durumu Uygula

Azure kurtarma Hizmetleri aracısını kullanarak dosyaları olarak sistem durumu kurtardı sonra kullanım hello Windows Server Yedekleme yardımcı programı tooapply hello sistem durumu tooWindows sunucu kurtarıldı. Windows Server Yedekleme yardımcı programı Hello hello sunucuda zaten var. Aşağıdaki adımları hello tooapply hello sistem durumu nasıl kurtarılır açıklanmaktadır.

1. Sunucunuzun kullanım hello aşağıdaki komutları tooreboot *dizin hizmetleri onarım modunda*. Yükseltilmiş bir komut istemi'nde:

    ```
    PS C:\> Bcdedit /set safeboot dsrepair
    PS C:\> Shutdown /r /t 0
    ```

2. Merhaba yeniden başlatıldıktan sonra hello Windows Server Yedekleme ek bileşenini açın. Merhaba ek bileşenini yüklendiği bilmiyorsanız, hello bilgisayar veya sunucu için arama **Windows Server Yedekleme**.

    Merhaba Masaüstü uygulama hello arama sonuçlarında görünür.

3. Merhaba ek bileşeninde, seçin **yerel yedekleme**.

    ![Yerel yedekleme toorestore buradan seçin](./media/backup-azure-restore-system-state/win-server-backup-local-backup.png)

4. Merhaba de hello yerel yedekleme konsolunda üzerinde **Eylemler bölmesinde**, tıklatın **kurtarmak** tooopen hello Kurtarma Sihirbazı.

5. Merhaba seçeneğini **başka bir konumda depolanan bir yedek**, tıklatıp **sonraki**.

   ![toorecover tooa farklı bir sunucu seçin](./media/backup-azure-restore-system-state/backup-stored-in-diff-location.png)

6. Merhaba konum türü belirtirken seçin **uzaktan paylaşılan klasörünü** , sistem durumu yedeklemesi kurtarılan tooanother sunucusuysa. Sistem durumu yerel olarak yapılıyorsa, ardından **yerel sürücüler**. 

    ![seçin olup olmadığını yerel sunucu ya da başka bir toorecovery](./media/backup-azure-restore-system-state/ss-recovery-remote-shared-folder.png)

7. Merhaba yolu toohello girin *WindowsImageBackup* dizin veya hello sistem durumu dosyaları kurtarma Azure Kurtarma'yı kullanarak bir parçası olarak kurtarılan bu dizin (örneğin, D:\WindowsImageBackup) içeren hello yerel sürücüyü seçin Aracı ve tıklatın Hizmetleri **sonraki**.

    ![yol toohello paylaşılan dosya](./media/backup-azure-restore-system-state/ss-recovery-remote-folder.png)

8. Toorestore istediğiniz ve tıklatın select hello sistem durumu sürüm **sonraki**.

9. Merhaba kurtarma türünü seçin bölmesinde seçin **sistem durumu** tıklatıp **sonraki**.

10. Merhaba sistem durumu kurtarma konumunu Hello için seçin **özgün konumuna**, tıklatıp **sonraki**.

11. Hello onayı ayrıntıları gözden geçirin, hello yeniden başlatma ayarlarını doğrulayın ve tıklatın **kurtarmak** tooapplly hello geri sistem durumu dosyaları.

    ![başlatma hello sistem durumu dosyaları geri yükle](./media/backup-azure-restore-system-state/launch-ss-recovery.png)

## <a name="special-considerations-for-system-state-recovery-on-active-directory-server"></a>Active Directory sunucuda sistem durumu kurtarma için özel hususlar

Sistem durumu yedeklemesi Active Directory verilerini içerir. Adımları toorestore Active Directory etki alanı hizmeti (AD DS) geçerli durumu tooa önceki durumunu izleyen hello kullanın.

1. Merhaba etki alanı denetleyicisi Dizin Hizmetleri geri yükleme modu (DSRM) yeniden başlatın.
2. Merhaba adımları [burada](https://technet.microsoft.com/en-us/library/cc794755(v=ws.10).aspx) toouse Windows Server Yedekleme cmdlet'leri toorecover AD DS.


## <a name="troubleshoot-failed-system-state-restore"></a>Başarısız sistem durumu geri yükleme sorunlarını giderme

Sistem durumu uygulama hello önceki işlem başarıyla tamamlanmazsa, Windows Server'ınızın hello Windows Kurtarma Ortamı'nı (Win RE) toorecover kullanın. Merhaba aşağıdaki adımlarda açıklanmaktadır nasıl toorecover Win yeniden kullanma. Yalnızca Windows Server normalde bir sistem durumu geri yüklendikten sonra önyükleme yapmaz, bu seçeneği kullanın. işlemi aşağıdaki hello sistem dışı verileri, dikkatli siler. 

1. Windows Server'ınızın Windows Kurtarma Ortamı'nı (Win RE) hello önyükleyin.

2. Sorun giderme hello üç kullanılabilir seçenekleri seçin.

    ![Açılış menüsü](./media/backup-azure-restore-system-state/winre-1.png)

3. Merhaba gelen **Gelişmiş Seçenekler** ekran, select **komut istemi** hello server yönetici kullanıcı adı ve parolasını girin.

   ![Açılış menüsü](./media/backup-azure-restore-system-state/winre-2.png)

4. Merhaba server yönetici kullanıcı adı ve parola belirtin.

    ![Açılış menüsü](./media/backup-azure-restore-system-state/winre-3.png)

5. Yönetici modunda hello komut istemi açın, aşağıdaki komut tooget hello sistem durumu yedekleme sürümlerini çalıştırın.

    ```
    Wbadmin get versions -backuptarget:<Volume where WindowsImageBackup folder is copied>:
    ```
    ![Sistem Durumu yedekleme sürümlerini alma](./media/backup-azure-restore-system-state/winre-4.png)

6. Komut tooget aşağıdaki hello hello yedeklemeye kullanılabilir tüm birimleri çalıştırın.

    ```
    Wbadmin get items -version:<copy version from above step> -backuptarget:<Backup volume>
    ```

    ![Sistem Durumu yedekleme sürümlerini alma](./media/backup-azure-restore-system-state/winre-5.png)

7. Merhaba aşağıdaki komutu hello sistem durumu yedeklemesi parçası olan tüm birimleri kurtarır. Bu adım yalnızca hello sistem durumu parçası olan hello kritik birimler kurtarır unutmayın. Tüm sistem dışı veriler silinir.

    ```
    Wbadmin start recovery -items:C: -itemtype:Volume -version:<Backupversion> -backuptarget:<backup target volume>
    ```
     ![Sistem Durumu yedekleme sürümlerini alma](./media/backup-azure-restore-system-state/winre-6.png)



## <a name="next-steps"></a>Sonraki adımlar
* Dosya ve klasörleri kurtarma yaptıktan, yapabilecekleriniz [Yedeklemelerinizin yönetmek](backup-azure-manage-windows-server.md).
