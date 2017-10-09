---
title: "aaaStorSimple anlık görüntü Yöneticisi Yedekleme kataloğu | Microsoft Docs"
description: "Toouse StorSimple Snapshot Manager MMC ek bileşenini tooview hello ve hello yedekleme kataloğunu yönetme nasıl açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 6abdbfd2-22ce-45a5-aa15-38fae4c8f4ec
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 173410095bcec7948d780d7fc258d2e3670bde8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toomanage-hello-backup-catalog"></a>StorSimple anlık görüntü Yöneticisi'ni kullanın toomanage hello yedekleme kataloğu

## <a name="overview"></a>Genel Bakış
Merhaba birincil StorSimple anlık görüntü Yöneticisi'nin, toocreate uygulama tutarlı yedekleme kopyalar tooallow StorSimple birimlerin anlık görüntüleri hello formunda işlevdir. Anlık görüntüler sonra adlı bir XML dosyasında listelenen bir *yedekleme kataloğu*. Merhaba yedekleme kataloğu anlık görüntüler birim grubu ve ardından yerel anlık görüntü veya Bulut anlık görüntüsü göre düzenler.

Bu öğretici hello nasıl kullanabileceğinizi açıklar **yedekleme kataloğu** görevleri aşağıdaki düğüm toocomplete hello:

* Bir birime geri yükleme
* Bir birim veya birim grubu kopyalama
* Yedek Sil
* Bir dosya kurtarma
* Merhaba Storsimple Snapshot Manager veritabanını geri yükle

Merhaba genişleterek hello yedekleme kataloğu görüntüleyebilirsiniz **yedekleme kataloğu** hello düğümünde **kapsam** bölmesinde ve hello birim grubu genişletme.

* Merhaba birim grubu adı tıklatırsanız hello **sonuçları** bölmesi yerel anlık görüntüler ve bulut anlık görüntüleri hello birim grubu için kullanılabilir hello sayısını gösterir. 
* Tıklatırsanız **yerel anlık görüntü** veya **bulut anlık görüntüsü**, hello **sonuçları** bölmesinde her yedekleme anlık görüntüsünü hakkında bilgi aşağıdaki hello gösterir (bağlı olarak, **Görünüm** ayarları):
  
  * **Ad** – hello hello anlık görüntü alındığı.
  * **Tür** – bu yerel bir anlık görüntüsü veya bir bulut anlık görüntüsü olsun.
  * **Sahibi** – hello içerik sahibi. 
  * **Kullanılabilir** – hello anlık görüntüsü şu anda kullanılabilir durumda olup olmadığını. **Doğru** bu hello anlık görüntü kullanılabilir olduğunu ve geri yüklenebilir; gösterir. **False** bu hello anlık görüntü artık kullanılabilir gösterir. 
  * **İçeri aktarılan** – hello yedekleme içeri aktarılmış olup olmadığını. **Doğru** hello yedekleme hello hello zaman hello aygıt hizmeti StorSimple anlık görüntü Yöneticisi'nde; yapılandırıldığından StorSimple cihaz Yöneticisi'nden alındı gösterir **False** alınmadığından, ancak StorSimple Snapshot Manager tarafından oluşturulmuş olduğunu gösterir. (Bir sonek hello birim grubu içeri aktarılmış hello aygıtı tanımlayan eklendiği bir içe aktarılan birim grubu kolayca tanıyacak.)
    
    ![Yedekleme kataloğu](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Backup_catalog.png)
* Genişletirseniz **yerel anlık görüntü** veya **bulut anlık görüntüsü**, ardından bir tek tek anlık görüntü adı hello **sonuçları** bölmesi hello hakkında bilgi aşağıdaki hello gösterir Seçtiğiniz anlık görüntüsü:
  
  * **Ad** – hello birimin sürücü harfiyle tanımlanır. 
  * **Yerel ad** – hello yerel ad hello sürücüsünün (varsa). 
  * **Aygıt** – hello birim üzerinde hangi hello bulunduğu hello aygıt adı. 
  * **Kullanılabilir** – hello anlık görüntüsü şu anda kullanılabilir durumda olup olmadığını. **Doğru** bu hello anlık görüntü kullanılabilir olduğunu ve geri yüklenebilir; gösterir. **False** bu hello anlık görüntü artık kullanılabilir gösterir. 

## <a name="restore-a-volume"></a>Bir birime geri yükleme
Yordam toorestore bir birim yedekten aşağıdaki hello kullanın.

#### <a name="prerequisites"></a>Ön koşullar
Zaten yapmadıysanız, bir birim ve birim grubu oluşturun ve hello birim silin. Varsayılan olarak, StorSimple Snapshot Manager silinmiş toobe sorgulamasına önce bir birim yedekler. Bu önlem veri kaybı hello birim yanlışlıkla silinirse veya hello veri herhangi bir nedenle kurtarılan toobe gerekiyorsa engelleyebilirsiniz. 

StorSimple Snapshot Manager hello önlem yedekleme oluşturduğu sırada iletiden hello görüntüler.

![Otomatik anlık görüntü iletisi](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Automatic_snap.png) 

> [!IMPORTANT]
> Bir birim grubunun parçası olan bir birimi silemezsiniz. Merhaba Sil seçeneği kullanılamaz. <br>
> 
> 

#### <a name="toorestore-a-volume"></a>toorestore bir birim
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın. 
2. Merhaba, **kapsam** bölmesinde hello genişletin **yedekleme kataloğu** düğümü, bir birim grubunu genişletin ve ardından **yerel anlık görüntüleri** veya **bulut anlık görüntüleri**. Hello yedekleme anlık görüntülerinin listesi görüntülenir **sonuçları** bölmesi.
3. Toorestore, sağ tıklatın ve ardından istediğiniz Bul hello yedekleme **geri**.
   
    ![Yedekleme kataloğunu geri yükle](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_BU_catalog.png) 
4. Hello onay sayfasında, gözden geçirme hello ayrıntılarını yazın **Onayla**ve ardından **Tamam**. StorSimple Snapshot Manager hello yedekleme toorestore hello birim kullanır.
   
    ![Geri yükle onay iletisi](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Restore_volume_msg.png) 
5. Çalışan hello geri yükleme eylemini izleyebilirsiniz. Merhaba, **kapsam** bölmesinde hello genişletin **işleri** düğümünü ve ardından **çalıştıran**. Merhaba iş ayrıntılarını görünür hello **sonuçları** bölmesi. Merhaba geri yükleme işi bittiğinde hello iş ayrıntılarını aktarılan toohello olan **son 24 saat** listesi.

## <a name="clone-a-volume-or-volume-group"></a>Bir birim veya birim grubu kopyalama
Aşağıdaki yordam toocreate tekrarı (kopya) bir birim veya birim grubu hello kullanın.

#### <a name="tooclone-a-volume-or-volume-group"></a>tooclone bir birim veya birim grubu
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde hello genişletin **yedekleme kataloğu** düğümü, bir birim grubunu genişletin ve ardından **bulut anlık görüntüleri**. Hello yedeklemeleri listesi görüntülenir **sonuçları** bölmesi.
3. Merhaba birim veya tooclone, sağ hello birim veya birim grubu adı ve'ı tıklatın birim grubu bulma **kopya**. Merhaba **kopyalama bulut anlık görüntü** iletişim kutusu görüntülenir.
   
    ![Bir bulut anlık görüntüsü kopyalayın](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Tam hello **kopyalama bulut anlık görüntü** aşağıdaki gibi iletişim kutusunda: 
   
   1. Merhaba, **adı** klonlanmış birim metin kutusuna hello için bir ad yazın. Bu ad hello görünür **birimleri** düğümü. 
   2. (İsteğe bağlı) seçin **sürücü**ve ardından bir sürücü harfi hello aşağı açılan listeden seçin.
   3. (İsteğe bağlı) seçin **klasörü (NTFS)**, bir klasör yolunu yazın veya Gözat'ı tıklatın ve hello klasörü için bir konum seçin. 
   4. **Oluştur**'a tıklayın.
5. Kopyalama işlemini hello bittiğinde klonlanmış hello birim başlatması gerekir. Sunucu Yöneticisi'ni başlatın ve ardından Disk Yönetimi'ni başlatın. Ayrıntılı yönergeler için bkz: [bağlama birimleri](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Başlatıldıktan sonra hello birim hello altında listelenir **birimleri** hello düğümünde **kapsam** bölmesi. Hello birim listede görmüyorsanız hello birimlerin listesini yenile (sağ hello **birimleri** düğümünü ve ardından **yenileme**).

## <a name="delete-a-backup"></a>Yedek Sil
Yordam toodelete bir anlık görüntü hello yedekleme Kataloğu'ndan aşağıdaki hello kullanın. 

> [!NOTE]
> Bir anlık görüntüyü sildiğinizde hello anlık görüntü ile ilişkili veriler yedeklenen hello siler. Ancak, hello hello bulut verilerini temizleme işlemi biraz zaman alabilir.<br>


#### <a name="toodelete-a-backup"></a>toodelete bir yedekleme
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde hello genişletin **yedekleme kataloğu** düğümü, bir birim grubunu genişletin ve ardından **yerel anlık görüntüleri** veya **bulut anlık görüntüleri**. Anlık görüntü listesi hello görüntülenir **sonuçları** bölmesi.
3. Toodelete istediğiniz ve ardından sağ hello anlık görüntü **silmek**.
4. Merhaba onaylama iletisi göründüğünde tıklayın **Tamam**.

## <a name="recover-a-file"></a>Bir dosya kurtarma
Bir dosyayı bir birimden yanlışlıkla silinirse hello silme hello anlık görüntü toocreate kullanarak, önceden tarihleri bir anlık görüntü hello birimin bir kopyasını alarak hello dosya kurtarabilir ve hello dosyasından kopyalama hello kopyalanan birim toohello özgün birim.

#### <a name="prerequisites"></a>Ön koşullar
Başlamadan önce geçerli yedekleme hello birim grubunun olduğundan emin olun. Ardından, birim grubundaki hello birimlerden biri üzerinde depolanan bir dosyayı silin. Son olarak, aşağıdaki adımları toorestore silinmiş hello dosyasına yedekleme hello kullanın. 

#### <a name="toorecover-a-deleted-file"></a>Silinmiş bir dosyayı toorecover
1. Masaüstünüzde Hello StorSimple Snapshot Manager simgesine tıklayın. Merhaba StorSimple Snapshot Manager konsol penceresi görünür. 
2. Merhaba, **kapsam** bölmesinde hello genişletin **yedekleme kataloğu** düğümü ve Silinen hello dosyasını içeren Gözat tooa anlık görüntü. Genellikle, yalnızca hello silme işleminden önce oluşturulmuş bir anlık görüntü seçmelisiniz.
3. Bul hello birim tooclone, sağ tıklatın ve tıklatın istediğiniz **kopya**. Merhaba **kopyalama bulut anlık görüntü** iletişim kutusu görüntülenir.
   
    ![Bir bulut anlık görüntüsü kopyalayın](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_Clone.png) 
4. Tam hello **kopyalama bulut anlık görüntü** aşağıdaki gibi iletişim kutusunda: 
   
   1. Merhaba, **adı** klonlanmış birim metin kutusuna hello için bir ad yazın. Bu ad hello görünür **birimleri** düğümü. 
   2. (İsteğe bağlı) Seçin **sürücü**ve ardından bir sürücü harfi hello aşağı açılan listeden seçin. 
   3. (İsteğe bağlı) Seçin **klasörü (NTFS)**ve bir klasör yolunu yazın veya **Gözat** ve başlangıç klasörü için bir konum seçin. 
   4. **Oluştur**'a tıklayın. 
5. Kopyalama işlemini hello bittiğinde klonlanmış hello birim başlatması gerekir. Sunucu Yöneticisi'ni başlatın ve ardından Disk Yönetimi'ni başlatın. Ayrıntılı yönergeler için bkz: [bağlama birimleri](storsimple-snapshot-manager-manage-volumes.md#mount-volumes). Başlatıldıktan sonra hello birim hello altında listelenir **birimleri** hello düğümünde **kapsam** bölmesi. 
   
    Hello birim listede görmüyorsanız hello birimlerin listesini yenile (sağ hello **birimleri** düğümünü ve ardından **yenileme**).
6. Kopyalanmış hello birimi içeren açık hello NTFS klasörünü genişletin hello **birimleri** düğümünü ve ardından açık hello klonlanmış birim. Toorecover istediğiniz ve toohello birincil toplu kopyalama hello dosyasını bulun.
7. Merhaba dosyasını geri yükledikten sonra hello NTFS klonlanmış hello birim içeren bir klasörü silebilirsiniz.

## <a name="restore-hello-storsimple-snapshot-manager-database"></a>Merhaba StorSimple Snapshot Manager veritabanını geri yükle
Merhaba StorSimple Snapshot Manager veritabanı hello ana bilgisayarda düzenli olarak yedeklemeniz gerekir. Bir olağanüstü durum oluştuğunda veya hello ana bilgisayar için herhangi bir nedenle başarısız olursa, ardından hello yedekten geri yükleyebilirsiniz. Oluşturma hello veritabanı yedeklemesi elle yapılan bir işlemdir.

#### <a name="tooback-up-and-restore-hello-database"></a>tooback yedeklemek ve geri yükleme hello veritabanı
1. Merhaba Microsoft StorSimple Yöneticisi Hizmeti Durdur:
   
   1. Sunucu Yöneticisi'ni başlatın.
   2. Merhaba de hello Sunucu Yöneticisi panosunda üzerinde **Araçları** menüsünde, select **Hizmetleri**.
   3. Merhaba üzerinde **Hizmetleri** penceresinde, select hello **Microsoft StorSimple Yöneticisi hizmeti**.
   4. Hello bölmesini altında sağ **Microsoft StorSimple Yöneticisi hizmeti**, tıklatın **hello hizmetini durdurun**.
2. Merhaba ana bilgisayarda tooC:\ProgramData\Microsoft\StorSimple\BACatalog göz atın. 
   
   > [!NOTE]
   > ProgramData gizli bir klasördür.
   > 
   > 
3. Merhaba katalog XML dosyası, hello dosya kopyala ve depola hello Kopyala güvenli bir konumda veya hello bulutta bulun. Hello ana bilgisayar başarısız olursa, StorSimple Snapshot Manager'da oluşturduğunuz bu yedek dosya toohelp Kurtar hello yedekleme ilkeleri kullanabilirsiniz.
   
    ![Azure StorSimple yedekleme kataloğu dosyası](./media/storsimple-snapshot-manager-manage-backup-catalog/HCS_SSM_bacatalog.png)
4. Merhaba Microsoft StorSimple Yöneticisi hizmeti yeniden başlatın: 
   
   1. Merhaba de hello Sunucu Yöneticisi panosunda üzerinde **Araçları** menüsünde, select **Hizmetleri**.
   2. Merhaba üzerinde **Hizmetleri** penceresinde, select hello **Microsoft StorSimple Yöneticisi hizmeti**.
   3. Hello bölmesini altında sağ **Microsoft StorSimple Yöneticisi hizmeti**, tıklatın **hello hizmetini yeniden başlatın**.
5. Merhaba ana bilgisayarda tooC:\ProgramData\Microsoft\StorSimple\BACatalog göz atın. 
6. Başlangıç kataloğu XML dosyasını silin ve oluşturduğunuz hello yedekleme sürümle değiştirin. 
7. Merhaba Masaüstü StorSimple Snapshot Manager simgesi toostart StorSimple Snapshot Manager'ı tıklatın. 

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [StorSimple Snapshot Manager tooadminister StorSimple çözümünüzün kullanarak](storsimple-snapshot-manager-admin.md).
* Daha fazla bilgi edinmek [StorSimple Snapshot Manager görevleri ve iş akışları](storsimple-snapshot-manager-admin.md#storsimple-snapshot-manager-tasks-and-workflows).

