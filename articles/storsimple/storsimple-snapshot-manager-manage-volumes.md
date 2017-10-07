---
title: "aaaStorSimple anlık görüntü Yöneticisi'ni ve birimler | Microsoft Docs"
description: "Toouse StorSimple Snapshot Manager MMC ek bileşenini tooview hello ve birimler ve tooconfigure yedeklemeleri yönetebilir nasıl açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 78896323-e57c-431e-bbe2-0cbde1cf43a2
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: b8ce102d082b7c773d667a9d3ec747be9e1d3064
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooview-and-manage-volumes"></a>StorSimple Snapshot Manager tooview kullanın ve birimleri yönetme
## <a name="overview"></a>Genel Bakış
Merhaba StorSimple Snapshot Manager kullanabilirsiniz **birimleri** düğümü (Merhaba üzerinde **kapsam** bölmesi) tooselect birimleri ve bunlarla ilgili bilgileri görüntüleyin. Merhaba birimleri hello ana bilgisayar tarafından bağlanan toohello birimleri karşılık gelen sürücüleri olarak sunulur. Merhaba **birimleri** düğümü yerel birimleri ve StorSimple, iSCSI ve bir cihaz hello kullanarak bulunan birimler dahil tarafından desteklenen birim türleri gösterir. 

Desteklenen birimleri hakkında daha fazla bilgi için çok Git[birden çok birim türleri için destek](storsimple-what-is-snapshot-manager.md#support-for-multiple-volume-types).

![Sonuçlar bölmesinde birim listesi](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Volume_node.png)

Merhaba **birimleri** düğümü de sağlar yeniden tarayın veya StorSimple Snapshot Manager bunları bulur sonra birimleri silin. 

Bu öğretici nasıl bağlamak, başlatmak ve birimleri biçimlendirme ve StorSimple anlık görüntü Yöneticisi'ni kullanarak açıklanmaktadır:

* Birimler hakkındaki bilgileri görüntüleme 
* Birimleri silin
* Birimleri yeniden tara 
* Temel birim yapılandırmak ve yedekleyin
* Dinamik yansıtılmış birim yapılandırmak ve yedekleyin

> [!NOTE]
> Tüm hello **birim** düğümü eylemleri de edinilebilir hello **Eylemler** bölmesi.
> 
> 

## <a name="mount-volumes"></a>Bağlama birimleri
Kullanım hello yordamı toomount aşağıdaki başlatın ve StorSimple birimlerini biçimlendirin. Bu yordam, Disk Yönetimi, sabit diskleri ve hello karşılık gelen birimlere veya bölümlerini yönetmek için bir sistem hizmet kullanır. Disk Yönetimi hakkında daha fazla bilgi için çok Git[Disk Yönetimi](https://technet.microsoft.com/library/cc770943.aspx) hello Microsoft TechNet Web sitesinde.

#### <a name="toomount-volumes"></a>toomount birimleri
1. Ana bilgisayarınızda hello Microsoft iSCSI başlatıcısını başlatın.
2. Bir hello arabirimi IP adresleri hello hedef portalı olarak veya bulma IP adresi sağlayın ve toohello aygıtı bağlayın. Merhaba cihaz bağlandıktan sonra hello birimleri erişilebilir tooyour Windows sistemi olacaktır. Toohello bölüm "Bağlanıyor tooan iSCSI hedef aygıt" Merhaba Microsoft iSCSI başlatıcısını kullanma hakkında daha fazla bilgi için Git [yükleme ve yapılandırma Microsoft iSCSI başlatıcısı][1].
3. Disk Yönetimi seçenekleri toostart aşağıdaki hello birini kullanın:
   
   * Hello diskmgmt.msc yazın **çalıştırmak** kutusu.
   * Sunucu Yöneticisi'ni başlatın, hello genişletin **depolama** düğümünü ve ardından **Disk Yönetimi**.
   * Başlat **Yönetimsel Araçlar**, hello genişletin **Bilgisayar Yönetimi** düğümünü ve ardından **Disk Yönetimi**. 
     
     > [!NOTE]
     > Yönetici ayrıcalıkları toorun Disk Yönetimi kullanmanız gerekir.
     > 
     > 
4. Merhaba birimlerin çevrimiçi yap:
   
   1. İşaretlenen herhangi bir birim Disk Yönetimi'nde sağ **çevrimdışı**.
   2. Tıklatın **yeniden Disk**. Merhaba disk işaretlenmelidir **çevrimiçi** hello disk yeniden etkinleştirildikten sonra.
5. Merhaba birimlerin başlatın:
   
   1. Merhaba bulunan birimleri sağ tıklayın.
   2. Başlangıç menüsünden seçin **diski başlatma**.
   3. Merhaba, **diski başlatma** iletişim kutusu, tooinitialize istediğiniz ve ardından select hello diskleri **Tamam**.
6. Basit birimler Biçimlendir:
   
   1. Tooformat istediğiniz bir birime sağ tıklayın.
   2. Başlangıç menüsünden seçin **yeni basit birim**.
   3. Merhaba Yeni Basit Birim Sihirbazı tooformat hello birim kullanın:
      
      * Merhaba birim boyutu belirtin.
      * Bir sürücü harfi sağlayın.
      * Merhaba NTFS dosya sistemi seçin.
      * 64 KB ayırma birimi boyutu belirtin.
      * Hızlı biçimlendirme gerçekleştirin.
7. Birden çok bölüm birimleri biçimlendirme. Yönergeler için toohello bölümünde, "Bölüm ve birimleri" Git [Disk Yönetimi uygulama](https://msdn.microsoft.com/library/dd163556.aspx).

## <a name="view-information-about-your-volumes"></a>Birimlerinizi hakkındaki bilgileri görüntüleme
Aşağıdaki yordam tooview bilgilerle yerel ve Azure StorSimple birimler hakkında hello kullanın.

#### <a name="tooview-volume-information"></a>tooview birim bilgileri
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın. 
2. Merhaba, **kapsam** bölmesinde, hello tıklatın **birimleri** düğümü. Tüm Azure StorSimple birimleri de dahil olmak üzere, yerel ve bağlı birimlerin listesini hello görünür **sonuçları** bölmesi. Merhaba hello sütunlarında **sonuçları** bölmesinde yapılandırılabilir. (Sağ hello **birimleri** düğümü, select **Görünüm**ve ardından **Sütun Ekle/Kaldır**.)
   
    ![Merhaba sütunları Yapılandır](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_View_volumes.png)
   
   | Sonuçları sütun | Açıklama |
   |:--- |:--- |
   |  Ad |Merhaba **adı** sütun hello sürücü harfi atanmış bulunan tooeach birimini içerir. |
   |  Cihaz |Merhaba **aygıt** sütun hello hello aygıt bağlı toohello ana bilgisayarın IP adresini içerir. |
   |  Cihaz birim adı |Merhaba **aygıt birim adı** sütun hello aygıt birim toowhich hello seçili hello adını içerir birim ait. Bu hello belirli o birim için Azure portal tanımlanan hello birim adıdır. |
   |  Erişim yolları |Merhaba **erişim yolları** sütunu hello erişim yolu toohello birim görüntüler. Hangi hello birim hello ana bilgisayarda erişilebilir durumda hello sürücü harfi veya bağlama noktası budur. |

## <a name="delete-a-volume"></a>Bir birim Sil
StorSimple anlık görüntü Yöneticisi'nden yordamı toodelete bir birim aşağıdaki hello kullanın.

> [!NOTE]
> Herhangi bir birim grubu parçası ise, bir birim silemezsiniz. (Merhaba Sil seçeneği bir birim grubu üyesi olan birimleri için kullanılabilir değildir.) Merhaba tüm birim grubu toodelete hello birim silmeniz gerekir.

#### <a name="toodelete-a-volume"></a>toodelete bir birim
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde, hello tıklatın **birimleri** düğümü. 
3. Merhaba, **sonuçları** bölmesi, sağ hello birim toodelete istiyor.
4. Başlangıç menüsünde **silmek**. 
   
    ![Bir birim Sil](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Delete_volume.png) 
5. Merhaba **Birim Sil** iletişim kutusu görüntülenir. Tür **Onayla** hello metin kutusuna ve ardından **Tamam**.
6. Varsayılan olarak, StorSimple Snapshot Manager silmeden önce bir birim yedekler. Merhaba silme işlemi istenmeden yapıldıysa, bu önlem veri kaybına karşı koruyabilirsiniz. StorSimple Snapshot Manager görüntüler bir **otomatik anlık görüntü** hello birimi yedekler olsa ilerleme iletisi. 
   
    ![Otomatik anlık görüntü iletisi](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Automatic_snap.png) 

## <a name="rescan-volumes"></a>Birimleri yeniden tara
Hello aşağıdaki yordamı toorescan hello birimleri bağlı tooStorSimple anlık görüntü Yöneticisi'ni kullanın.

#### <a name="toorescan-hello-volumes"></a>toorescan hello birimleri
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Hello içinde **kapsam** bölmesinde sağ **birimleri**ve ardından **birimleri yeniden tara**.
   
    ![Birimleri yeniden tara](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Rescan_volumes.png)
   
    Bu yordamı hello birim listesi StorSimple Snapshot Manager ile eşitler. Yeni birimlere veya silinen birimler gibi herhangi bir değişiklik hello sonuçlarında yansıtılır.

## <a name="configure-and-back-up-a-basic-volume"></a>Yapılandırma ve temel bir birimi yedekleyin
Aşağıdaki yordam tooconfigure temel bir birim yedeğini hello kullanın ve ardından bir yedeklemeyi hemen başlatmak ya da zamanlanmış yedeklemeler için bir ilke oluşturun.

### <a name="prerequisites"></a>Ön koşullar
Başlamadan önce:

* Merhaba StorSimple cihaz ve ana bilgisayar doğru şekilde yapılandırıldığından emin olun. Daha fazla bilgi için çok Git[şirket içi StorSimple Cihazınızı dağıtma](storsimple-deployment-walkthrough-u2.md).
* Yükleyin ve StorSimple Snapshot Manager yapılandırın. Daha fazla bilgi için çok Git[dağıtmak StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).

#### <a name="tooconfigure-backup-of-a-basic-volume"></a>temel birim tooconfigure yedekleme
1. Temel birim hello StorSimple cihazında oluşturun.
2. Bağlamayı, başlatmayı ve açıklandığı gibi hello birimi biçimlendirmek [bağlama birimleri](#mount-volumes). 
3. Masaüstünüzde Hello StorSimple Snapshot Manager simgesine tıklayın. Merhaba StorSimple Snapshot Manager penceresi görüntülenir. 
4. Merhaba, **kapsam** bölmesi, sağ hello **birimleri** düğümünü ve ardından **birimleri yeniden tara**. Merhaba tarama tamamlandığında, birimlerin listesini hello görünmelidir **sonuçları** bölmesi. 
5. Merhaba, **sonuçları** bölmesinde hello birime sağ tıklayın ve ardından **birim grubu oluştur**. 
   
    ![Birim grubu oluştur](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Create_volume_group.png) 
6. Merhaba, **birim grubu oluştur** iletişim kutusu, hello birim grubu için bir ad girin, birimleri tooit atayın ve ardından **Tamam**.
7. Merhaba, **kapsam** bölmesinde hello genişletin **birim grupları** düğümü. Merhaba yeni birim grubu hello altında görünmelidir **birim grupları** düğümü. 
8. Merhaba birim grubu adını sağ tıklatın.
   
   * toostart bir etkileşimli (isteğe bağlı) yedekleme işi, tıklatın **ele yedekleme**. 
   * tooschedule bir otomatik yedekleme tıklatın **yedekleme İlkesi Oluştur**. Merhaba üzerinde **genel** sayfasında, bir birim grubu hello listeden seçin. Merhaba üzerinde **zamanlama** sayfasında, hello zamanlama ayrıntılarını girin. İşiniz bittiğinde, tıklatın **Tamam**. 
9. yedekleme işi hello tooconfirm başlatıldı, hello genişletin **işleri** hello düğümünde **kapsam** bölmesinde ve ardından hello **çalıştıran** düğümü. şu anda çalışan işi hello listesi görünür hello **sonuçları** bölmesi. 

## <a name="configure-and-back-up-a-dynamic-mirrored-volume"></a>Yapılandırma ve dinamik yansıtılmış birimi yedekleyin
Dinamik yansıtılmış birim tooconfigure yedeğini adımları izleyerek hello tamamlayın:

* 1. adım: Disk yönetimini kullanma toocreate dinamik yansıtılmış birim. 
* 2. adım: StorSimple anlık görüntü Yöneticisi'ni kullanın tooconfigure yedekleme.

### <a name="prerequisites"></a>Ön koşullar
Başlamadan önce:

* Merhaba StorSimple cihaz ve ana bilgisayar doğru şekilde yapılandırıldığından emin olun. Daha fazla bilgi için çok Git[şirket içi StorSimple Cihazınızı dağıtma](storsimple-8000-deployment-walkthrough-u2.md).
* Yükleyin ve StorSimple Snapshot Manager yapılandırın. Daha fazla bilgi için çok Git[dağıtmak StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).
* İki birimleri hello StorSimple cihazında yapılandırın. (Merhaba örneklerde hello kullanılabilir birimlerdir **Disk 1** ve **Disk 2**.) 

### <a name="step-1-use-disk-management-toocreate-a-dynamic-mirrored-volume"></a>1. adım: Disk yönetimini kullanma toocreate dinamik yansıtılmış birim
Disk Yönetimi, sabit diskleri ve hello birimleri veya içerdikleri bölümlerini yönetmek için bir sistem aracıdır. Disk Yönetimi hakkında daha fazla bilgi için çok Git[Disk Yönetimi](https://technet.microsoft.com/library/cc770943.aspx) hello Microsoft TechNet Web sitesinde.

#### <a name="toocreate-a-dynamic-mirrored-volume"></a>toocreate dinamik yansıtılmış birim
1. Disk Yönetimi seçenekleri toostart aşağıdaki hello birini kullanın: 
   
   * Açık hello **çalıştırmak** kutusuna **Diskmgmt.msc**, ve Enter tuşuna basın.
   * Sunucu Yöneticisi'ni başlatın, hello genişletin **depolama** düğümünü ve ardından **Disk Yönetimi**. 
   * Başlat **Yönetimsel Araçlar**, hello genişletin **Bilgisayar Yönetimi** düğümünü ve ardından **Disk Yönetimi**. 
2. Merhaba StorSimple cihazında iki birimler kullanılabilir olduğundan emin olun. (Merhaba örnekte hello kullanılabilir birimlerdir **Disk 1** ve **Disk 2**.) 
3. Merhaba Disk Yönetimi penceresinde hello sağ sütundaki hello alt bölme, sağ **Disk 1** seçip **Yeni Yansıtılmış birim**. 
   
    ![Yeni Yansıtılmış birim](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_New_mirrored_volume.png) 
4. Merhaba üzerinde **Yeni Yansıtılmış birim** sihirbaz sayfasında, tıklatın **sonraki**.
5. Hello üzerinde **diskleri Seç** sayfasında, seçin **Disk 2** hello içinde **seçili** bölmesinde tıklatın **Ekle**ve ardından **İleri**. 
6. Merhaba üzerinde **sürücü harfi atama veya yol** sayfasında, hello Varsayılanları kabul edin ve ardından **sonraki**. 
7. Merhaba üzerinde **birim biçimlendirmeyi** sayfasında hello **ayırma birimi boyutu** kutusunda **64K**. Select hello **hızlı biçimlendirme gerçekleştirmek** onay kutusunu işaretleyin ve ardından **sonraki**. 
8. Merhaba üzerinde **Tamamlanıyor hello Yeni Yansıtılmış birim** sayfasında, ayarlarınızı gözden geçirin ve ardından **son**. 
9. Dönüştürülen tooa dinamik disk temel disk hello tooindicate olacak bir ileti görüntülenir. **Evet**'e tıklayın.
   
    ![Dinamik disk dönüştürme iletisi](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Disk_management_msg.png) 
10. Disk Yönetimi'nde Disk 1 ve Disk 2 dinamik yansıtılmış birimler olarak gösterildiğinden emin olun. (**Dinamik** hello Durum sütununda görünür olmalıdır ve hello kapasite çubuğu rengini yansıtılmış birim belirten toored değiştirmek.) 
    
    ![Disk Yönetimi yansıtılmış dinamik diskler](./media/storsimple-snapshot-manager-manage-volumes/HCS_SSM_Verify_dynamic_disks_2.png) 

### <a name="step-2-use-storsimple-snapshot-manager-tooconfigure-backup"></a>2. adım: StorSimple anlık görüntü Yöneticisi'ni kullanın tooconfigure yedekleme
Aşağıdaki yordam tooconfigure dinamik yansıtılmış birim hello kullanın ve ardından bir yedeklemeyi hemen başlatmak ya da zamanlanmış yedeklemeler için bir ilke oluşturun.

#### <a name="tooconfigure-backup-of-a-dynamic-mirrored-volume"></a>Dinamik yansıtılmış birim tooconfigure yedeği
1. Masaüstünüzde Hello StorSimple Snapshot Manager simgesine tıklayın. Merhaba StorSimple Snapshot Manager penceresi görüntülenir. 
2. Merhaba, **kapsam** bölmesi, sağ hello **birimleri** düğümü ve seçin **birimleri yeniden tara**. Merhaba tarama tamamlandığında, birimlerin listesini hello görünmelidir **sonuçları** bölmesi. Merhaba dinamik yansıtılmış birim tek bir birim listelenir. 
3. Merhaba, **sonuçları** bölmesinde hello dinamik yansıtılmış birime sağ tıklayın ve ardından **birim grubu oluştur**. 
4. Merhaba, **birim grubu oluştur** iletişim kutusu, hello birim grubu için bir ad yazın, hello dinamik yansıtılmış birim toothis grubu atayın ve ardından **Tamam**. 
5. Merhaba, **kapsam** bölmesinde hello genişletin **birim grupları** düğümü. Merhaba yeni birim grubu hello altında görünmelidir **birim grupları** düğümü. 
6. Merhaba birim grubu adını sağ tıklatın. 
   
   * toostart bir etkileşimli (isteğe bağlı) yedekleme işi, tıklatın **ele yedekleme**. 
   * tooschedule bir otomatik yedekleme tıklatın **yedekleme İlkesi Oluştur**. Merhaba üzerinde **genel** sayfası, hello listesinden seçim hello birim grubu. Merhaba üzerinde **zamanlama** sayfasında, hello zamanlama ayrıntılarını girin. İşiniz bittiğinde, tıklatın **Tamam**. 
7. Çalışan hello yedekleme işi izleyebilirsiniz. Merhaba, **kapsam** bölmesinde hello genişletin **işleri** düğümünü ve ardından **çalıştıran**, hello iş ayrıntılarını görünür hello **sonuçları** bölmesi. Merhaba yedekleme işi tamamlandığında, hello ayrıntıları aktarılan toohello olan **son 24** saatleri proje listesi. 

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[StorSimple Snapshot Manager tooadminister StorSimple çözümünüzün kullanmak](storsimple-snapshot-manager-admin.md).
* Nasıl çok öğrenin[StorSimple Snapshot Manager toocreate kullanın ve birim gruplarını yönetme](storsimple-snapshot-manager-manage-volume-groups.md).

<!--Reference links-->
[1]: https://msdn.microsoft.com/library/ee338480(v=ws.10).aspx
