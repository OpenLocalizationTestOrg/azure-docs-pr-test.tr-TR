---
title: aaaDeploy StorSimple Snapshot Manager | Microsoft Docs
description: "StorSimple veri koruma ve yedekleme özellikleri yönetmek için MMC ek bileşenini StorSimple Snapshot Manager toodownload ve yükleme nasıl hello öğrenin."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: f0128f57-519e-49ec-9187-23575809cdbe
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: dd90cca2bbb3410bb8cd459fb1a3ff3fb5f2997b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-snapshot-manager-mmc-snap-in"></a>StorSimple Snapshot Manager MMC ek bileşenini Hello dağıtma

## <a name="overview"></a>Genel Bakış
Merhaba StorSimple Snapshot Manager, veri koruma ve Microsoft Azure StorSimple ortamda yedekleme yönetimini basitleştirir Microsoft Yönetim Konsolu (MMC) ek bileşenidir. StorSimple Snapshot Manager ile Microsoft Azure StorSimple şirket içi yönetme ve tam olarak tümleşik depolama sistemi değilmiş gibi depolama böylece yedekleme ve geri yükleme işlemleri basitleştirir ve maliyetlerini azaltma bulut. 

Bu öğretici, yükleme, kaldırma ve StorSimple Snapshot Manager yükseltme yordamları yanı sıra yapılandırma gereksinimlerini açıklar.

> [!NOTE]
> * StorSimple Snapshot Manager toomanage Microsoft Azure StorSimple sanal (olarak da bilinen StorSimple sanal cihazlar şirket) diziler kullanamazsınız.
> * StorSimple Cihazınızda tooinstall StorSimple güncelleştirme 2 düşünüyorsanız, emin toodownload hello en son sürümünü StorSimple anlık görüntü Yöneticisi'nin olması ve yüklemeniz **StorSimple güncelleştirme 2 yüklemeden önce**. Merhaba en son sürümünü StorSimple anlık görüntü Yöneticisi'nin geriye dönük olarak uyumludur ve Microsoft Azure StorSimple serbest bırakılmış tüm sürümleri ile çalışır. StorSimple anlık görüntü Yöneticisi'nin hello önceki sürümü kullanıyorsanız, tooupdate gerekir (gerektirmeyen toouninstall hello önceki sürüm hello yeni sürümü yüklemeden önce) BT.


## <a name="storsimple-snapshot-manager-installation"></a>StorSimple anlık görüntü Yöneticisi'ni yükleme
StorSimple Snapshot Manager hello Windows Server 2008 R2 SP1, Windows Server 2012 veya Windows Server 2012 R2 işletim sistemi çalıştıran bilgisayarlara yüklenebilir. Windows 2008 R2 çalıştıran sunucularda, Windows Server 2008 SP1 ve Windows Management Framework 3.0 de yüklemeniz gerekir.

Yüklemeden veya hello StorSimple Snapshot Manager ek bileşenini Microsoft Yönetim Konsolu (MMC) hello yükseltmeden önce hello Microsoft Azure StorSimple cihaz emin olun ve ana bilgisayar sunucusu doğru şekilde yapılandırılır.

## <a name="configure-prerequisites"></a>Önkoşulları yapılandırma
Merhaba aşağıdaki adımlar yapılandırma görevleri üst düzey bir genel bakış hello StorSimple Snapshot Manager yüklemeden önce tamamlamanız gerekir sağlar. Microsoft Azure StorSimple yapılandırmasını tamamlamak ve sistem gereksinimleri ve adım adım yönergeler de dahil olmak üzere, kurulum bilgileri görmek için [şirket içi StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-u2.md).

> [!IMPORTANT]
> Başlamadan önce hello gözden [dağıtım yapılandırma denetim listesi](storsimple-8000-deployment-walkthrough-u2.md#deployment-configuration-checklist) ve ve [dağıtımının önkoşulları](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites) içinde [şirket içi StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-u2.md).
> <br>
> 
> 

### <a name="before-you-install-storsimple-snapshot-manager"></a>StorSimple Snapshot Manager yüklemeden önce
1. Kutusundan çıkarma, bağlama ve açıklandığı gibi hello Microsoft Azure StorSimple cihazı bağlayın [StorSimple 8100 cihazınız yüklemek](storsimple-8100-hardware-installation.md) veya [StorSimple 8600 model Cihazınızı yüklemek](storsimple-8600-hardware-installation.md).
2. Ana bilgisayar işletim sistemleri aşağıdaki hello birini çalıştığından emin olun:
   
   * Windows Server 2008 R2 (Windows 2008 R2 çalıştıran üzerinde sunucular da Windows Server 2008 SP1 ve Windows Management Framework 3.0 yüklemeniz gerekir)
   * Windows Server 2012
   * Windows Server 2012 R2
     
     StorSimple sanal cihaz için bir Microsoft Azure sanal makinesi hello konak olması gerekir.
3. Tüm hello Microsoft Azure StorSimple yapılandırma gereksinimlerini karşıladığından emin olun. Ayrıntılı bilgi için çok gidin[dağıtımının önkoşulları](storsimple-8000-deployment-walkthrough-u2.md#deployment-prerequisites).
4. Merhaba aygıt toohello ana bağlanın ve hello ilk yapılandırmasını gerçekleştirin. Ayrıntılı bilgi için çok gidin[dağıtım adımları](storsimple-8000-deployment-walkthrough-u2.md#deployment-steps).
5. Merhaba aygıtta birimler oluşturabilir, toohello ana bilgisayar atamak ve hello barındıran bağlayabilir ve bunları doğrulayın. StorSimple Snapshot Manager hello şu birimlerin türlerini destekler:
   
   * Temel birim
   * Basit birimler
   * Dinamik birimler
   * Yansıtılmış dinamik birimler (RAID 1)
   * Küme Paylaşılan Birimleri
     
     Birimleri hello StorSimple cihaz veya StorSimple sanal cihaz oluşturma hakkında daha fazla bilgi için çok Git[6. adım: birim oluşturma](storsimple-8000-deployment-walkthrough-u2.md#step-6-create-a-volume), [şirket içi StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-u2.md).

## <a name="install-a-new-storsimple-snapshot-manager"></a>Yeni bir StorSimple Snapshot Manager yükleyin
StorSimple Snapshot Manager'ı yüklemeden önce oluşturulan hello StorSimple cihazı veya StorSimple sanal cihazı hello birimler takılı, başlatılmış ve açıklandığı şekilde biçimlendirilmiş olduğunu emin olun [önkoşulları yapılandırma](#configure-prerequisites).

> [!IMPORTANT]
> * StorSimple sanal cihaz için bir Microsoft Azure sanal makinesi hello konak olması gerekir. 
> * Merhaba ana bilgisayar Windows 2008 R2, Windows Server 2012 veya Windows Server 2012 R2 çalıştırması gerekir. Sunucunuz Windows Server 2008 R2 çalıştırıyorsa, Windows Server 2008 SP1 ve Windows Management Framework 3.0 yüklemeniz gerekir.
> * Merhaba aygıt tooStorSimple anlık görüntü Yöneticisi'ni bağlanabilmesi için önce bir iSCSI bağlantısı hello konak toohello StorSimple cihazı yapılandırmanız gerekir.

Bu adımları toocomplete yüklemesidir StorSimple anlık görüntü Yöneticisi'nin izleyin. Bir yükseltme yüklüyorsanız, çok Git[yükseltme veya yeniden StorSimple Snapshot Manager](#upgrade-or-reinstall-storsimple-snapshot-manager).

* 1. adım: StorSimple anlık görüntü Yöneticisi'ni yükleyin 
* 2. adım: StorSimple Snapshot Manager tooa aygıt bağlanma 
* 3. adım: hello bağlantı toohello aygıtı doğrulayın 

### <a name="step-1-install-storsimple-snapshot-manager"></a>1. adım: StorSimple anlık görüntü Yöneticisi'ni yükleyin
Aşağıdaki adımları tooinstall StorSimple Snapshot Manager hello kullanın.

#### <a name="tooinstall-storsimple-snapshot-manager"></a>StorSimple Snapshot Manager tooinstall
1. Merhaba StorSimple Snapshot Manager yazılımı yükle (çok Git[StorSimple Snapshot Manager](https://www.microsoft.com/download/details.aspx?id=44220) hello Microsoft Download Center içinde) ve hello ana bilgisayarda yerel olarak kaydedin.
2. Dosya Gezgini'nde, hello sıkıştırılmış klasörü sağ tıklatın ve ardından **tümünü Ayıkla**.
3. Merhaba, **sıkıştırılmış ayıklamak (Zipped) klasörleri** penceresinde hello **bir hedef seçin ve dosyaları ayıklayın** kutusuna yazın veya olduğu gibi ayıklanan toofile toobe toohello yolu göz atın.
   
    > [!IMPORTANT]
    > StorSimple Snapshot Manager C: sürücüsündeki hello üzerinde yüklemeniz gerekir.
    
4. Select hello **Göster ayıklanan dosyaları tamamlandığında** onay kutusunu işaretleyin ve ardından **ayıklamak**.
   
    ![Dosyaları ayıkla iletişim kutusu](./media/storsimple-snapshot-manager-deployment/HCS_SSM_extract_files.png) 
5. Merhaba Ayıklama tamamlandığında hello hedef klasörü açılır. Merhaba hedef klasörde görünür hello Uygulama Kurulumu simgesini çift tıklatın.
6. Ne zaman hello **Kurulumu başarılı** iletisi görüntülendikten sonra **Kapat**. Masaüstünüzde hello StorSimple Snapshot Manager simgesi görmeniz gerekir.
   
    ![Masaüstü simgesi](./media/storsimple-snapshot-manager-deployment/HCS_SSM_desktop_icon.png) 

### <a name="step-2-connect-storsimple-snapshot-manager-tooa-device"></a>2. adım: StorSimple Snapshot Manager tooa aygıt bağlanma
Aşağıdaki adımları tooconnect StorSimple Snapshot Manager tooa StorSimple cihazı hello kullanın.

#### <a name="tooconnect-storsimple-snapshot-manager-tooa-device"></a>tooconnect StorSimple Snapshot Manager tooa aygıt
1. Masaüstünüzde Hello StorSimple Snapshot Manager simgesine tıklayın. Merhaba StorSimple Snapshot Manager penceresi görüntülenir. Hello penceresi içeren bir **kapsam** bölmesinde, bir **sonuçları** bölmesinde ve bir **Eylemler** bölmesi. 
   
    ![StorSimple anlık görüntü Yöneticisi kullanıcı arabirimi](./media/storsimple-snapshot-manager-deployment/HCS_SSM_gui_panes.png)
   
   * Merhaba **kapsam** bölmesinde (sol bölme hello) içeren bir ağaç yapısında düzenlenmiş düğüm listesi. Bazı düğümler tooselect bir görünüm veya belirli veri ilgili toothat düğümü genişletebilirsiniz. Merhaba ok simgesine tooexpand tıklayın veya bir düğüm daraltın. Bir öğeyi hello sağ **kapsam** bölmesinde toosee bu öğeye ilişkin kullanılabilir eylemler listesi.
   * Merhaba **sonuçları** bölmesi (Merhaba Orta bölme), başlangıç düğümü, görünümü veya hello seçili veri hakkındaki ayrıntılı durum bilgilerini içerir **kapsam** bölmesi.
   * Merhaba **Eylemler** bölmesi hello düğümü, görünümü veya hello seçili veri gerçekleştirebileceğiniz hello işlemleri listeler **kapsam** bölmesi.
     
     Merhaba StorSimple Snapshot Manager kullanıcı arabirimi tam bir açıklaması için bkz: [StorSimple Snapshot Manager kullanıcı arabirimini](storsimple-use-snapshot-manager.md).
2. Merhaba, **kapsam** bölmesi, sağ hello **aygıtları** düğümünü ve ardından **bir aygıt yapılandırma**. Merhaba **bir aygıt yapılandırma** iletişim kutusu görüntülenir.
   
    ![Bir aygıt yapılandırma](./media/storsimple-snapshot-manager-deployment/HCS_SSM_config_device.png) 
3. Merhaba, **aygıt** liste kutusu, select hello IP adresini hello Microsoft Azure StorSimple cihazı veya sanal aygıt. Merhaba, **parola** metin kutusu, hello Azure portal hello aygıt için oluşturduğunuz türü hello StorSimple Snapshot Manager parolası. **Tamam** düğmesine tıklayın.
4. StorSimple Snapshot Manager tanımladığınız hello aygıt için arar. Merhaba aygıt varsa, StorSimple Snapshot Manager bağlantı ekler. Yapabilecekleriniz [hello bağlantı toohello aygıtı doğrulayın](#to-verify-the-connection) bağlantı hello tooconfirm başarıyla eklendi.
   
    Merhaba aygıt herhangi bir nedenle kullanılamıyorsa, StorSimple Snapshot Manager bir hata iletisi döndürür. Tıklatın **Tamam** tooclose hello hata iletisi ve ardından **iptal** tooclose hello **bir aygıt yapılandırma** iletişim kutusu.
5. Hello birim grubu yedeklemeleri ilişkili koşuluyla StorSimple Snapshot Manager tooa Aygıt bağlandığında, bu cihaz için yapılandırılmış her birim grubu içeri aktarır. İlişkili yedeklemelerinizi olmayan birim grupları içeri aktarılmadı. Ayrıca, bir birim grubu için oluşturulan yedekleme ilkeleri içeri aktarılmadı. toosee Merhaba alınan grupları, hello en üstteki sağ **birim grupları** hello düğümünde **kapsam** bölmesinde ve tıklatın **alınan grupları geçiş**.

### <a name="step-3-verify-hello-connection-toohello-device"></a>3. adım: hello bağlantı toohello aygıtı doğrulayın
StorSimple Snapshot Manager bağlı toohello StorSimple cihaz olduğunu adımları tooverify aşağıdaki hello kullanın.

#### <a name="tooverify-hello-connection"></a>tooverify hello bağlantı
1. Merhaba, **kapsam** bölmesinde, hello tıklatın **aygıtları** düğümü.
   
    ![StorSimple Snapshot Manager cihaz durumu](./media/storsimple-snapshot-manager-deployment/HCS_SSM_Device_status.png) 
2. Merhaba denetleyin **sonuçları** bölmesi: 
   
   * Merhaba aygıt simgesinde yeşil bir göstergesi görünür değilse ve **kullanılabilir** hello görünür **durum** sütununda, ardından hello aygıt bağlı. 
   * Merhaba aygıt simgesinde kırmızı bir göstergesi görünür ve kullanılamaz görünüyorsa hello **durum** sütununda, ardından hello aygıt bağlı değil. 
   * Varsa **yenilemek** hello görünür **durum** sütun sonra StorSimple Snapshot Manager alma birim grupları ve ilişkili yedeklemeler bağlı bir aygıt için.

## <a name="upgrade-or-reinstall-storsimple-snapshot-manager"></a>Yükseltme veya StorSimple Snapshot Manager yeniden yükleme
Yükseltme veya hello yazılımı yeniden önce StorSimple Snapshot Manager tamamen kaldırmanız gerekir. 

StorSimple Snapshot Manager yeniden yüklemeden önce hello varolan StorSimple Snapshot Manager veritabanını hello ana bilgisayarda yedekleyin. Bu hello yedekleme ilkeleri ve yapılandırma bilgileri kaydeder, böylece bu verileri kolayca yedekten geri yükleyebilirsiniz.

Yükseltme veya yeniden yüklemeyi StorSimple Snapshot Manager, şu adımları izleyin:

* 1. adım: StorSimple anlık görüntü Yöneticisi'ni kaldırma 
* 2. adım: Merhaba StorSimple Snapshot Manager veritabanını yedekle 
* 3. adım: StorSimple anlık görüntü Yöneticisi'ni yeniden yükleyin ve hello veritabanını geri yükle 

### <a name="step-1-uninstall-storsimple-snapshot-manager"></a>1. adım: StorSimple anlık görüntü Yöneticisi'ni kaldırma
Aşağıdaki adımları toouninstall StorSimple Snapshot Manager hello kullanın.

#### <a name="toouninstall-storsimple-snapshot-manager"></a>StorSimple Snapshot Manager toouninstall
1. Merhaba Hello ana bilgisayarda açmak **Denetim Masası**, tıklatın **programları**ve ardından **programlar ve Özellikler**.
2. Merhaba sol bölmede **Kaldır veya Değiştir bir program**.
3. Sağ **StorSimple Snapshot Manager**ve ardından **kaldırma**.
4. Merhaba StorSimple Snapshot Manager Kurulum programını başlatır. Tıklatın **değiştirme kurulum**ve ardından **kaldırma**.
   
   > [!NOTE]
   > Varsa hello arka planda çalışan tüm MMC işlemleri, StorSimple Snapshot Manager veya Disk Yönetimi gibi hello kaldırma başarısız olur ve bu ileti tooclose alacak MMC, önce tüm örneklerini toouninstall hello program çalışır. Seçin **otomatik olarak uygulamaları kapatın ve bunları Kurulum tamamlandıktan sonra tamamlamanız toorestart Dene**ve ardından **Tamam**.
   > 
   > 
5. Merhaba kaldırdığınızda işlem tamamlandı, bir **Kurulumu başarılı** ileti görüntülenir. **Kapat**’a tıklayın.

### <a name="step-2-back-up-hello-storsimple-snapshot-manager-database"></a>2. adım: Merhaba StorSimple Snapshot Manager veritabanını yedekle
Aşağıdaki adımları toocreate hello kullanın ve hello StorSimple Snapshot Manager veritabanının bir kopyasını kaydedin.

#### <a name="tooback-up-hello-database"></a>Merhaba veritabanını tooback
1. Merhaba Microsoft StorSimple Yöneticisi Hizmeti Durdur:
   
   1. Sunucu Yöneticisi'ni başlatın.
   2. Merhaba üzerinde Sunucu Yöneticisi Panosu hello üzerinde **Araçları** menüsünde, select **Hizmetleri**.
   3. Merhaba üzerinde **Hizmetleri** sayfasında, **Microsoft StorSimple Yöneticisi hizmeti**.
   4. Hello bölmesini altında sağ **Microsoft StorSimple Yöneticisi hizmeti**, tıklatın **hello hizmetini durdurun**.
      
        ![Merhaba StorSimple cihaz Yöneticisi hizmetini durdurun](./media/storsimple-snapshot-manager-deployment/HCS_SSM_stop_service.png)
2. TooC:\ProgramData\Microsoft\StorSimple\BACatalog göz atın. 
   
   > [!NOTE]
   > ProgramData gizli bir klasördür.
  
3. Merhaba katalog XML dosyası, hello dosya kopyala ve depola hello Kopyala güvenli bir konumda veya hello bulutta bulun.
   
    ![StorSimple yedekleme kataloğu dosyası](./media/storsimple-snapshot-manager-deployment/HCS_SSM_bacatalog.png)
4. Merhaba Microsoft StorSimple Yöneticisi hizmeti yeniden başlatın: 
   
   1. Merhaba üzerinde Sunucu Yöneticisi Panosu hello üzerinde **Araçları** menüsünde, select **Hizmetleri**.
   2. Merhaba üzerinde **Hizmetleri** sayfası, select hello **Microsoft StorSimple Yönetim bildirimleri**e.
   3. Hello bölmesini altında sağ **Microsoft StorSimple Yöneticisi hizmeti**, tıklatın **hello hizmetini yeniden başlatın**. 

### <a name="step-3-reinstall-storsimple-snapshot-manager-and-restore-hello-database"></a>3. adım: StorSimple anlık görüntü Yöneticisi'ni yeniden yükleyin ve hello veritabanını geri yükle
StorSimple Snapshot Manager tooreinstall izleyin hello adımlarda [yeni bir StorSimple Snapshot Manager yükleme](#install-a-new-storsimple-snapshot-manager). Ardından, aşağıdaki yordamı toorestore hello StorSimple Snapshot Manager veritabanı hello kullanın.

#### <a name="toorestore-hello-database"></a>toorestore hello veritabanı
1. Merhaba Microsoft StorSimple Yöneticisi Hizmeti Durdur:
   
   1. Sunucu Yöneticisi'ni başlatın.
   2. Merhaba üzerinde Sunucu Yöneticisi Panosu hello üzerinde **Araçları** menüsünde, select **Hizmetleri**.
   3. Merhaba üzerinde **Hizmetleri** sayfasında, **Microsoft StorSimple Yöneticisi hizmeti**.
   4. Hello bölmesini altında sağ **Microsoft StorSimple Yöneticisi hizmeti**, tıklatın **hello hizmetini durdurun**.
2. TooC:\ProgramData\Microsoft\StorSimple\BACatalog göz atın.
   
   > [!NOTE]
   > ProgramData gizli bir klasördür.
   > 
   > 
3. Başlangıç kataloğu XML dosyasını silin ve daha önce kaydettiğiniz hello sürümle değiştirin.
4. Merhaba Microsoft StorSimple Yöneticisi hizmeti yeniden başlatın: 
   
   1. Merhaba üzerinde Sunucu Yöneticisi Panosu hello üzerinde **Araçları** menüsünde, select **Hizmetleri**.
   2. Merhaba üzerinde **Hizmetleri** sayfasında, **Microsoft StorSimple Yöneticisi hizmeti**.
   3. Hello bölmesini altında sağ **Microsoft StorSimple Yöneticisi hizmeti**, tıklatın **hello hizmetini yeniden başlatın**.

## <a name="next-steps"></a>Sonraki adımlar
* toolearn daha hakkında StorSimple Snapshot Manager, Git çok[StorSimple anlık görüntü Yöneticisi nedir?](storsimple-what-is-snapshot-manager.md).
* Merhaba StorSimple Snapshot Manager kullanıcı arabirimi hakkında daha fazla toolearn Git çok[StorSimple Snapshot Manager kullanıcı arabirimini](storsimple-use-snapshot-manager.md).
* StorSimple Snapshot Manager kullanma hakkında daha fazla toolearn Git çok[StorSimple anlık görüntü Yöneticisi'ni kullanın tooadminister StorSimple çözümünüzün](storsimple-snapshot-manager-admin.md).

