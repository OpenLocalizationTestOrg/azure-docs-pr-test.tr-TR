---
title: "aaaStorSimple anlık görüntü Yöneticisi birim grupları | Microsoft Docs"
description: "Toouse StorSimple Snapshot Manager MMC ek bileşenini toocreate hello ve birim gruplarını yönetme nasıl açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a>StorSimple Snapshot Manager toocreate kullanma ve birim grupları yönetme
## <a name="overview"></a>Genel Bakış
Merhaba kullanabilirsiniz **birim grupları** hello düğümde **kapsam** bölmesi tooassign birimleri toovolume grupları, bir birim grubu hakkındaki bilgileri görüntüleyin yedeklemeleri zamanlamak ve birim grupları düzenleyin.

Birim, yedeklemelerin uygulama tutarlı olduğunu kullanılan ilgili birimleri tooensure havuzları gruplarıdır. Daha fazla bilgi için bkz: [birim ve birim grupları](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) ve [Windows birim gölge kopyası hizmeti ile tümleştirme](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).

> [!IMPORTANT]
> * Bir birim grubundaki tüm birimleri, bir tek bulut hizmeti sağlayıcısını gelmesi gerekir.
> * Birim grupları yapılandırdığınızda, Küme Paylaşılan birimleri (CSV) ve CSV olmayan hello içinde karıştırmamanızı aynı birim grubu. StorSimple Snapshot Manager csv bir karışımını desteklemez ve aynı anlık görüntü olmayan-csv hello.

![Birim grupları düğümü](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

**Şekil 1: StorSimple anlık görüntü Yöneticisi birim grupları düğümü** 

Bu öğretici, StorSimple Snapshot Manager için nasıl kullanabileceğiniz açıklanır:

* Birim grupları hakkındaki bilgileri görüntüleme
* Birim grubu oluştur
* Bir birim grubunu yedekleyin
* Bir birim grubu Düzenle
* Bir birim grubu Sil

Tüm bu eylemleri de hello üzerinde kullanılabilir **Eylemler** bölmesi.

## <a name="view-volume-groups"></a>Birim grupları görüntüle
Merhaba tıklatırsanız **birim grupları** düğümü, hello **sonuçları** bölmesinde her bir birim grubu hakkında bilgi aşağıdaki hello gösterir, yaptığınız hello sütun seçimlerini bağlı olarak. (Merhaba hello sütunlarında **sonuçları** bölmesinde yapılandırılabilir. Sağ hello **birimleri** düğümü, select **Görünüm**ve ardından **Sütun Ekle/Kaldır**.)

| Sonuçları sütun | Açıklama |
|:--- |:--- |
| Ad |Merhaba **adı** sütun hello birim grubu hello adını içerir. |
| Uygulama |Merhaba **uygulamaları** hello Windows ana bilgisayar üzerinde çalışan ve sütun şu anda yüklü VSS yazıcılarının hello sayısı gösterir. |
| Seçildi |Merhaba **seçili** sütun hello birim grubunda bulunan birimleri hello sayısını gösterir. Sıfır (0), uygulama hello birimleri hello birim grubu ile ilişkili olduğunu gösterir. |
| İçeri aktarılan |Merhaba **Imported** sütun alınan birimler hello sayısını gösterir. Ayarlandığında çok**doğru**, bu sütun bir birim grubu hello Azure portal ' alınan ve StorSimple Snapshot Manager'da oluşturulmadı belirtir. |

> [!NOTE]
> StorSimple Snapshot Manager birim grupları ayrıca hello üzerinde görüntülenen **yedekleme ilkeleri** hello Azure portal sekmesindedir.
> 
> 

## <a name="create-a-volume-group"></a>Birim grubu oluştur
Aşağıdaki yordam toocreate bir birim grubu hello kullanın.

#### <a name="toocreate-a-volume-group"></a>toocreate bir birim grubu
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde sağ **birim grupları**ve ardından **birim grubu oluştur**.
   
    ![Birim grubu oluştur](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    Merhaba **bir birim grubu oluşturun** iletişim kutusu görüntülenir.
   
    ![Bir birim grubu iletişim kutusu oluşturma](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. Aşağıdaki bilgilerle hello girin:
   
   1. Merhaba, **adı** hello yeni birim grubu için benzersiz bir ad yazın.
   2. Merhaba, **uygulamaları** kutusunda, toohello birim grubu alacağınız hello birimleri ile ilişkili uygulama.
      
       Merhaba **uygulamaları** VSS yazıcılarının olan ve StorSimple birimlerini kullanan uygulamalar için bunları etkin kutusunu listeler. Tüm birimlerin hello hello yazıcının farkında ise yalnızca bir VSS yazıcının etkin olduğu StorSimple birimler. Merhaba uygulamaları kutusu boş ise, VSS yazıcılarının desteklenen ve Azure StorSimple birimlerini kullanan bir uygulama yüklenmez. (Şu anda Azure StorSimple Microsoft Exchange ve SQL Server destekler.) VSS yazıcılarının hakkında daha fazla bilgi için bkz: [Windows birim gölge kopyası hizmeti ile tümleştirme](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).
      
       Bir uygulama seçerseniz, kendisiyle ilişkilendirilmiş tüm birimleri otomatik olarak seçilir. Belirli bir uygulama ile ilişkili birimler seçerseniz, buna karşılık, hello uygulama otomatik olarak hello seçilen **uygulamaları** kutusu. 
   3. Merhaba, **birimleri** kutusunda, StorSimple birimlerini tooadd toohello birim grubu seçin. 
      
      * Tek veya birden çok bölüm birimlerle içerebilir. (Birden çok bölüm birim dinamik diskleri veya temel diskleri birden çok bölüm olabilir.) Birden çok bölüm içeren bir birimdeki tek bir birim olarak kabul edilir. Sonuç olarak, yalnızca bir hello bölümleri tooa birim grubu, tüm hello diğer bölümler eklerseniz, olan otomatik olarak eklenen toothat birim grubu hello aynı saat. Birden çok bölüm birim tooa birim Grup ekledikten sonra hello birden çok bölüm birim tek bir birim olarak kabul toobe devam eder.
      * Tüm birimlerin toothem atayarak değil boş birim grupları oluşturabilirsiniz. 
      * Küme Paylaşılan birimleri (CSV) ve CSV olmayan hello içinde karıştırmamanızı aynı birim grubu. StorSimple Snapshot Manager CSV birimleri karışımını desteklemez ve aynı anlık görüntü CSV olmayan birimlerin hello.
4. Tıklatın **Tamam** toosave hello birim grubu.

## <a name="back-up-a-volume-group"></a>Bir birim grubunu yedekleyin
Bir birim grubu yordamı tooback aşağıdaki hello kullanın.

#### <a name="tooback-up-a-volume-group"></a>bir birim grubu tooback
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde hello genişletin **birim grupları** düğümü, bir birim grubu adını sağ tıklatın ve ardından **ele yedekleme**.
   
    ![Birim grubunu hemen yedekleyin](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. Merhaba, **ele yedekleme** iletişim kutusunda **yerel anlık görüntü** veya **bulut anlık görüntüsü**ve ardından **oluşturma**.
   
    ![Yedekleme iletişim alın](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. Yedekleme hello tooconfirm çalıştığından, hello genişletin **işleri** düğümünü ve ardından **çalıştıran**. Merhaba yedekleme listelenmelidir.
5. Tamamlanan tooview hello hello genişletin anlık görüntü, **yedekleme kataloğu** düğümü hello birim grup adını genişletin ve ardından **yerel anlık görüntü** veya **bulut anlık görüntüsü**. başarıyla tamamlandı, hello yedekleme listelenir.

## <a name="edit-a-volume-group"></a>Bir birim grubu Düzenle
Aşağıdaki yordam tooedit bir birim grubu hello kullanın.

#### <a name="tooedit-a-volume-group"></a>tooedit bir birim grubu
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde hello genişletin **birim grupları** düğümü, bir birim grubu adını sağ tıklatın ve ardından **Düzenle**.
3. Merhaba ** bir birim grubu oluşturun ** iletişim kutusu görüntülenir. Merhaba değiştirebileceğiniz **adı**, **uygulamaları**, ve **birimleri** girişleri.
4. Tıklatın **Tamam** toosave değişikliklerinizi.

## <a name="delete-a-volume-group"></a>Bir birim grubu Sil
Aşağıdaki yordam toodelete bir birim grubu hello kullanın. 

> [!WARNING]
> Bu da hello birim grubu ile ilişkili tüm hello yedeklerini siler.
> 
> 

#### <a name="toodelete-a-volume-group"></a>toodelete bir birim grubu
1. Merhaba Masaüstü simgesi toostart StorSimple Snapshot Manager'ı tıklatın.
2. Merhaba, **kapsam** bölmesinde hello genişletin **birim grupları** düğümü, bir birim grubu adını sağ tıklatın ve ardından **silmek**.
3. Merhaba **birim grubunu Sil** iletişim kutusu görüntülenir. Tür **Onayla** hello metin kutusuna ve ardından **Tamam**.
   
    Silinen hello birim grubu kaybolduktan hello hello listesinden **sonuçları** bölmesinde ve o birimi grubuyla ilişkili olan tüm yedeklemeler hello yedekleme Kataloğu'ndan silinir.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[StorSimple Snapshot Manager tooadminister StorSimple çözümünüzün kullanmak](storsimple-snapshot-manager-admin.md).
* Nasıl çok öğrenin[StorSimple Snapshot Manager toocreate kullanın ve yedekleme ilkelerini yönetme](storsimple-snapshot-manager-manage-backup-policies.md).

