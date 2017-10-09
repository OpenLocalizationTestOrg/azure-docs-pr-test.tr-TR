---
title: "aaaStorSimple anlık görüntü Yöneticisi kullanıcı arabirimi | Microsoft Docs"
description: "Merhaba StorSimple Snapshot Manager kullanıcı arabirimini tanımlar ve açıklar nasıl toouse, toomanage yedekleme işleri ve hello yedekleme kataloğu."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: c7d91892-2881-41a2-a7a2-908dc3646493
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.custom: 
ms.openlocfilehash: 865520fdaf1b559714b52b428ad136b084d65c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-user-interface-toomanage-backup-jobs-and-backup-catalog"></a>StorSimple anlık görüntü Yöneticisi'ni kullanın kullanıcı arabirimi toomanage yedekleme işleri ve yedekleme kataloğu

## <a name="overview"></a>Genel Bakış
Merhaba StorSimple Snapshot Manager tootake kullanma ve yedeklemeleri yönetme bir sezgisel bir kullanıcı arabirimine sahiptir. Bu öğretici bir giriş toohello kullanıcı arabirimi sağlar ve ardından açıklar nasıl toouse her hello bileşenlerinin. Merhaba StorSimple Snapshot Manager ayrıntılı bir açıklaması için bkz: [StorSimple anlık görüntü Yöneticisi nedir?](storsimple-what-is-snapshot-manager.md)

### <a name="console-description"></a>Konsol açıklaması
tooview hello kullanıcı arabirimi, masaüstünüzü hello StorSimple Snapshot Manager simgesine tıklayın. hello aşağıdaki çizimde gösterildiği gibi Hello konsol penceresi görünür.

![StorSimple Snapshot Manager bölmeleri](./media/storsimple-use-snapshot-manager/HCS_SSM_gui_panes.png)

Merhaba konsol penceresi beş temel öğe var. Her öğe eksiksiz bir açıklaması için Hello uygun bağlantıyı tıklatın.

* [Menü çubuğu](#menu-bar) 
* [Araç çubuğu](#tool-bar) 
* [Kapsam bölmesi](#scope-pane) 
* [Sonuçlar Bölmesi](#results-pane) 
* [Eylemler bölmesi](#actions-pane) 

Ayrıca, StorSimple Snapshot Manager destekleyen hello [klavye gezinti ve bir dizi kısayol](#keyboard-navigation-and-shortcuts).

### <a name="console-accessibility"></a>Konsolu erişilebilirlik
Merhaba StorSimple Snapshot Manager kullanıcı arabirimini hello Windows işletim sistemi ve hello Microsoft Yönetim Konsolu (MMC), yanı sıra tarafından bazı StorSimple Snapshot Manager – özel klavye kısayolları sağlanan hello erişilebilirlik özellikleri destekler. 

* Merhaba Windows erişilebilirlik özellikleri açıklaması için çok Git[Windows için klavye kısayolları](https://support.microsoft.com/kb/126449). 
* Merhaba MMC erişilebilirlik özellikleri açıklaması için çok Git[MMC 3.0 için erişilebilirlik](https://technet.microsoft.com/library/cc766075.aspx)
* Merhaba StorSimple Snapshot Manager erişilebilirlik özellikleri açıklaması için çok Git[klavye gezinme ve kısayollar](#keyboard-navigation-and-shortcuts).

## <a name="menu-bar"></a>Menü çubuğu
Merhaba menü çubuğu hello konsol penceresinde hello üstündeki içerir [dosya](#file-menu), [eylem](#action-menu), [Görünüm](#view-menu), [Sık Kullanılanlar](#favorites-menu), [penceresi ](#window-menu), ve [yardımcı](#help-menu) menüleri.

Bu menüdeki kullanılabilir komutların hello menü çubuğu toosee listesini üzerinde herhangi bir öğeyi tıklatın. Merhaba aşağıdaki örnekte gösterilir hello **Görünüm** hello menü çubuğunda seçilen menüsü.

![Seçili Görünüm menüsü](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png)

### <a name="file-menu"></a>Dosya menüsü
Merhaba **dosya** menüsü, standart Microsoft Yönetim Konsolu (MMC) komutlarını içerir.

#### <a name="menu-access"></a>Menü erişimi
tooview hello **dosya** menüsünde tıklatın **dosya** hello menü çubuğunda. menü aşağıdaki hello görüntülenir.

![StorSimple Snapshot Manager Dosya menüsü](./media/storsimple-use-snapshot-manager/HCS_SSM_FileMenu.png) 

#### <a name="menu-description"></a>Menü açıklaması
Merhaba aşağıdaki tabloda görünen öğeler üzerinde hello açıklanmaktadır **dosya** menüsü.

| Menü öğesi | Açıklama |
|:--- |:--- |
| Yeni |Tıklatın **yeni** yeni bir konsol tabanlı StorSimple Snapshot Manager hello üzerinde toocreate. |
| Açık |Tıklatın **açık** tooopen varolan bir konsolu. |
| Kaydet |Tıklatın **kaydetmek** toosave hello geçerli konsol. |
| Farklı kaydet |Tıklatın **Kaydet** toocreate hello geçerli konsol yeni, yeniden adlandırılmış bir örneği. Kullanım hello **Kaydet** seçeneği toocustomize bir görünüm ve sonraki alımını kaydedin. Örneğin, bu nokta toospecific sunucuları StorSimple Snapshot Manager ek bileşenleri oluşturabilirsiniz. |
| Ekleyin veya ek bileşenini Kaldır |Tıklatın **Ekle/Kaldır ek bileşenini** tooadd veya ek bileşenleri ve tooorganize kaldırma hello düğümler **kapsam** bölmesi. Daha fazla bilgi için çok Git[Ekle, Kaldır ve Düzenle eklentileri ve Uzantıları MMC 3.0](https://technet.microsoft.com/library/cc722035.aspx). |
| Seçenekler |Tıklatın **seçenekleri** toochange hello konsol simgesi, kullanıcı erişim modları ve izinleri belirtin veya konsol dosyaları tooincrease kullanılabilir disk alanını silin. |
| Dosya yolları listesi |Merhaba numaralı liste tooreopen en son açtığınız bir dosya yolunda tıklatın. |
| Çıkış |Tıklatın **çıkış** tooclose hello **dosya** menüsü. |

### <a name="action-menu"></a>Eylem menüsü
Kullanım hello **eylem** kullanılabilir eylemlerine menü tooselect. Merhaba öğeler kullanılabilir tooyou bağlı hello seçim hello yap **kapsam** bölmesinde veya **sonuçları** bölmesi.

#### <a name="menu-access"></a>Menü erişimi
tooview hello **eylem** menüsü, hello aşağıdakilerden birini yapın:

* Bir öğeyi hello sağ **kapsam** bölmesinde veya **sonuçları** bölmesi.
* Hello bir öğe seçin **kapsam** bölmesinde veya **sonuçları** bölmesi ve ardından **eylem** hello menü çubuğunda. 

Örneğin hello hello en üstteki düğümü seçin, **kapsam** bölmesinde ve ardından sağ tıklayın veya **eylem** hello menü çubuğunda, hello aşağıdaki menüsü görüntülenir.

![StorSimple Snapshot Manager eylem menüsü](./media/storsimple-use-snapshot-manager/HCS_SSM_Action_menu.png)

Merhaba **Eylemler** bölmesinde (Merhaba hello konsol sağında) içeren hello Eylemler aynı listesi hello olarak **eylem** menüsü. Ayrıca, hello **Eylemler** bölmesidir hello **Görünüm** toocreate hello özel görünüm etkinleştirmek menü seçeneklerini **sonuçları** bölmesi.

![Görünüm menüsü açık eylemler bölmesi](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

#### <a name="menu-description"></a>Menü açıklaması
Aşağıdaki tablonun hello StorSimple Snapshot Manager Eylemler alfabetik bir listesini içerir. 

* Merhaba **eylem** sütunu, düğümleri ve sonuçları üzerinde gerçekleştirebileceğiniz eylemleri listeler. 
* Merhaba **Gezinti** sütun açıklar nasıl toodisplay hello uygun **eylem** menü hello eylem seçebilmeniz için. Bazı eylemler birden çok görünür **eylem** menüleri. Bu Eylemler, seçin **Gezinti** hello madde işaretli listede seçeneği. 
* Merhaba **açıklama** sütunu tanımlar nasıl toouse hello her eylem **eylem** menüsü veya Eylemler bölmesinde ve ne yaptığını açıklar.

> [!NOTE]
> Merhaba **Eylemler** bölmesinde ve **eylem** menüleri içeren ek seçenekler gibi **Görünüm**, **buradan yeni pencere**,  **Yenileme**, **verme listesi**, ve **yardımcı**. Bu seçenekler hello MMC bir parçası olarak kullanılabilir ve belirli tooStorSimple anlık görüntü Yöneticisi değildir. Merhaba tabloda bu seçeneklerin açıklamaları içerir.
> 
> 

| Eylem | Gezinme | Açıklama |
|:--- |:--- |:--- |
| Kimlik doğrulaması |Merhaba tıklatın **aygıtları** düğümü ve sağ hello bir aygıt **sonuçları** bölmesi. |Tıklatın **kimlik doğrulama** hello aygıt için yapılandırılmış tooenter hello parola. |
| Kopyala |Genişletme **yedekleme kataloğu**, genişletin **bulut anlık görüntüleri**tarihli backup'ı tıklatın ve ardından hello bir birim seçin **sonuçları** bölmesi. |Tıklatın **kopya** toocreate bir kopyasını bir bulut anlık görüntü ve belirlediğiniz bir yerde saklayın. |
| Bir aygıt yapılandırma |Sağ hello **aygıtları** düğümü. |Tıklatın **bir aygıt yapılandırma** tooconfigure tek veya birden çok aygıtları tooconnect toohello Windows ana bilgisayarı. |
| Yedekleme ilkesi oluşturma |Merhaba aşağıdakilerden birini yapın:<ul><li>Sağ **yedekleme ilkeleri**.</li><li>' I tıklatın veya genişletme **birim grupları**ve bir birim grubunu sağ tıklatın.</li><li>' I tıklatın veya genişletme **yedekleme kataloğu**ve bir birim grubunu sağ tıklatın.</li></ul> |Tıklatın **yedekleme İlkesi Oluştur** tooconfigure bir birim grubu için zamanlanmış bir yedekleme. |
| Birim grubu oluştur |Merhaba aşağıdakilerden birini yapın:<ul><li>Merhaba tıklatın **birimleri** düğümünü ve ardından sağ hello biriminde **sonuçları** bölmesi.</li><li>Sağ hello **birim grupları** düğümü.</li></ul> |Tıklatın **birim grubu oluştur** tooassign birimleri tooa birim grubu. |
| Sil |Bir düğüm veya sonucu tıklayın (Bu öğe birçok görünür **eylem** menüleri ve **Eylemler** bölmeleri.) |Tıklatın **silmek** toodelete hello düğüm veya seçtiğiniz sonucu. Merhaba onay iletişim kutusu göründüğünde, onaylayın veya hello silme işlemi iptal edin. |
| Ayrıntılar |Merhaba tıklatın **aygıtları** düğümünü ve ardından sağ tıklayarak bir aygıt hello **sonuçları** bölmesi. |Tıklatın **ayrıntıları** toosee hello yapılandırma ayrıntılarını bir aygıt için. |
| Düzenle |Tıklatın **yedekleme ilkeleri**, hello ilkesinde sağ tıklatın **sonuçları** bölmesi. |Tıklatın **Düzenle** toochange hello yedekleme zamanlamasını bir birim grubu. |
| Listeyi dışarı aktar |Herhangi bir düğüm veya sonuç tıklatın (tüm bu öğe görünür **eylem** menüleri ve **Eylemler** bölmeleri.) |Tıklatın **Liste Ver** toosave bir virgülle ayrılmış değer (CSV) dosyasına bir listesi. Çözümleme için bir elektronik tablo uygulamaya sonra bu dosyayı içeri aktarabilirsiniz. |
| Yardım |Bir düğüm veya sonucu'ı tıklatın. (Tüm bu öğe görünür **eylem** menüleri ve **Eylemler** bölmeleri.) |Tıklatın **yardımcı** tooopen ayrı bir tarayıcı penceresinde'çevrimiçi Yardım. |
| Buradan yeni pencere |Herhangi bir düğüm veya sonuç tıklatın (tüm bu öğe görünür **eylem** menüleri ve **Eylemler** bölmeleri.) |Tıklatın **buradan yeni pencere** tooopen yeni bir StorSimple Snapshot Manager penceresi. |
| Yenileme |Herhangi bir düğüm veya sonuç tıklatın (tüm bu öğe görünür **eylem** menüleri ve **Eylemler** bölmeleri.) |Tıklatın **yenileme** tooupdate görüntülenmekte hello StorSimple Snapshot Manager penceresi. |
| Cihaz Yenile |Merhaba tıklatın **aygıtları** düğümü ve sağ hello bir aygıt **sonuçları** bölmesi. |Tıklatın **yenileme aygıt** toosynchronize belirli bir bağlı aygıt ile StorSimple Snapshot Manager. |
| Cihazlarını Yenile |Sağ hello **aygıtları** düğümü. |Tıklatın **yenileme aygıtları** toosynchronize bağlı cihazı ile StorSimple Snapshot Manager listesi. |
| Birimleri yeniden tara |Sağ hello **birimleri** düğümü. |Tıklatın **birimleri yeniden tara** tooupdate hello hello görünür birimlerin listesini **sonuçları** bölmesi. |
| Geri Yükleme |Genişletme **yedekleme kataloğu**, bir birim grubu genişletin, **yerel anlık görüntüleri** veya **bulut anlık görüntüleri**ve bir yedek sağ tıklatın. |Tıklatın **geri** tooreplace hello geçerli birim grubu verileri hello seçili yedekleme hello verilerle. |
| Yedekleyin |Merhaba aşağıdakilerden birini yapın:<ul><li>Genişletme **birim grupları**ve bir birim grubunu sağ tıklatın.</li><li>Genişletme **yedekleme kataloğu**ve bir birim grubunu sağ tıklatın.</li></ul> |Tıklatın **ele yedekleme** toostart bir yedekleme işi hemen. |
| İçeri aktarmalar ekranını Değiştir |Sağ hello üst düğümü hello **kapsam** bölmesinde (Merhaba **StorSimple Snapshot Manager** hello örnekler düğümünde). |Tıklatın **içeri aktarmalar ekranını Değiştir** tooshow veya gizleme hello birim grupları ve alındığı ilişkili yedeklemelerinizi hello StorSimple Aygıt Yöneticisi'ni hizmet panosunu. |

### <a name="view-menu"></a>Görünüm menüsü
Kullanım hello **Görünüm** menü toocreate hello Özel Görünüm **sonuçları** bölmesinde içeriği. Merhaba **Görünüm** menüsü içerir **Sütun Ekle/Kaldır** ve **Özelleştir** seçenekleri.

#### <a name="menu-access"></a>Menü erişimi
Merhaba erişebilirsiniz **Görünüm** menü hello menü çubuğunda veya hello **Eylemler** bölmesi.

![StorSimple Snapshot Manager Görünüm menüsü](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png) 

#### <a name="menu-description"></a>Menü açıklaması
Merhaba aşağıdaki tabloda görünen öğeler üzerinde hello açıklanmaktadır **Görünüm** menüsü.

| Menü öğesi | Açıklama |
|:--- |:--- |
| Sütun Ekle/Kaldır |Tıklatın **Sütun Ekle/Kaldır** hello tooadd veya kaldırma sütunlarında **sonuçları** bölmesi. |
| Özelleştirme |Tıklatın **Özelleştir** hello StorSimple Snapshot Manager konsol penceresinde tooshow veya gizleme öğeleri. |

### <a name="favorites-menu"></a>Sık Kullanılanlar menüsü
Merhaba kullanmak **Sık Kullanılanlar** menü tooadd kaldırın ve sayfa görünümleri ve sık kullandığınız görevleri düzenleyin. 

#### <a name="menu-access"></a>Menü erişimi
Merhaba erişebilirsiniz **Sık Kullanılanlar** hello menü çubuğundaki menüsü.

![StorSimple Snapshot Manager Sık Kullanılanlar menüsü](./media/storsimple-use-snapshot-manager/HCS_SSM_FavoritesMenu.png)

#### <a name="menu-description"></a>Menü açıklaması
Merhaba aşağıdaki tabloda görünen öğeler üzerinde hello açıklanmaktadır **Sık Kullanılanlar** menüsü.

| Menü öğesi | Açıklama |
|:--- |:--- |
| TooFavorites Ekle |Tıklatın **tooFavorites ekleme** tooadd hello geçerli görünümü tooyour Sık Kullanılanlar listesi. |
| Sık kullanılanları düzenleme |Tıklatın **kullanılanları** Sık Kullanılanlar klasörünüze tooorganize Merhaba içeriğine. |

### <a name="window-menu"></a>Pencere menüsü
Kullanım hello **penceresi** menü tooadd ve sıralama StorSimple Snapshot Manager konsol penceresi.

#### <a name="menu-access"></a>Menü erişimi
Merhaba erişebilirsiniz **penceresi** hello menü çubuğundaki menüsü.

![StorSimple Snapshot Manager Pencere menüsü](./media/storsimple-use-snapshot-manager/HCS_SSM_WindowMenu.png)

şu anda hello windows açmak Hello numaralı liste hello menü hello sonundaki gösterir. Bu liste toobring hello penceresi herhangi penceresinde hello ön alana tıklayın. 

#### <a name="menu-description"></a>Menü açıklaması
Merhaba aşağıdaki tablo görünür hello öğeleri hello Pencere menüsünden açıklar.

| Menü öğesi | Açıklama |
|:--- |:--- |
| Yeni Pencere |Tıklatın **yeni pencere** tooopen yeni bir konsol penceresi (penceresinde toplama toohello var). |
| CASCADE |Tıklatın **Cascade** toodisplay hello açık Konsolu windows geçişli stil. |
| Yatay Döşe |Tıklatın **yatay döşeme** toodisplay hello açık Konsolu windows bir kutucuk (veya kılavuz) biçiminde. |
| Simgeleri Düzenle |Windows açın ve bunları en aza indirmek ve ardından masaüstünüzü dağılmış birden çok konsol varsa **Düzenle simgeleri** tooarrange hello ekranınızın yatay bir satırda bunları. |

### <a name="help-menu"></a>Yardım menüsü
Kullanım hello **yardımcı** tooview kullanılabilir çevrimiçi Yardım menüsü StorSimple Snapshot Manager ve hello MMC için. Sisteminizde yüklü olan hello MMC ve StorSimple Snapshot Manager yazılımı sürümleri hakkında bilgi de görüntüleyebilirsiniz. 

Merhaba erişebilirsiniz **yardımcı** hello menü çubuğundaki menüsü. StorSimple Snapshot Manager Yardım konuları hello erişebilirsiniz **Eylemler** bölmesi.

![StorSimple Snapshot Manager Yardım menüsünü](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpMenu.png)

#### <a name="menu-description"></a>Menü açıklaması
Aşağıdaki tablonun hello hello Yardım menü görünen öğeleri açıklar.

| Menü öğesi | Açıklama |
|:--- |:--- |
| StorSimple Snapshot Manager Yardımı |Tıklatın **yardımcı StorSimple Snapshot Manager** tooopen ayrı bir pencerede StorSimple Snapshot Manager Yardım. |
| Yardım konuları |Tıklatın **Yardım konuları** ayrı bir pencerede tooopen MMC çevrimiçi Yardım. |
| TechCenter Web sitesi |Tıklatın **TechCenter Web sitesi** tooopen hello Microsoft TechNet Tech Center giriş sayfası ayrı bir pencerede. |
| Microsoft Yönetim Konsolu hakkında |Tıklatın **Microsoft Yönetim Konsolu hakkında** hangi sürümünün hello Microsoft Yönetim Konsolu toosee sisteminizde yüklü. |
| StorSimple Snapshot Manager hakkında |Tıklatın **hakkında StorSimple Snapshot Manager** toosee hello ek bileşenini hangi sürümünün sisteminizde yüklü. |

## <a name="tool-bar"></a>Araç çubuğu
Merhaba menü çubuğunun altında bulunan hello araç çubuğu gezinti ve görev simgeleri içerir. Her simge kısayol tooa belirli bir görevdir.

### <a name="icon-descriptions"></a>Simge açıklamaları
Hello aşağıdaki tablo görünür hello simgeler hello araç çubuğundaki açıklar. 

| Simgesi | Açıklama |
|:--- |:--- |
| ![Sol Ok](./media/storsimple-use-snapshot-manager/HCS_SSM_LeftArrow.png) |Merhaba sol ok simgesine tooreturn toohello önceki sayfasına tıklayın. |
| ![Sağ ok](./media/storsimple-use-snapshot-manager/HCS_SSM_RightArrow.png) |Merhaba sağ ok toogo toohello sonraki sayfaya tıklayın (Merhaba ok gri ise, hello eylemi kullanılamaz). |
| ![Yukarı simgesi](./media/storsimple-use-snapshot-manager/HCS_SSM_Up.png) |Simge toogo hello konsol ağacında bir düzey yukarı Hello tıklayın (Merhaba **kapsam** bölmesi). |
| ![Konsol Ağacını Göster/Gizle](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowConsoleTree.png) |Merhaba Göster/Gizle Konsol ağacında simgesi tooshow'ı tıklatın veya hello gizleme **kapsam** bölmesi. |
| ![Listeyi dışarı aktar](./media/storsimple-use-snapshot-manager/HCS_SSM_ExportListIcon.png) |Merhaba verme listesi simgesi tooexport belirttiğiniz bir listesi tooa CSV dosyası'ı tıklatın. |
| ![Yardım simgesi](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpIcon.png) |Merhaba Yardım simgesine tooopen bir MMC Yardım konusunun'ı tıklatın. |
| ![Eylemler Bölmesini Göster/Gizle](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowAction.png) |Merhaba Göster/Gizle'yi **Eylemler** bölmesinde simgesi tooshow veya gizleme hello **Eylemler** bölmesi. |

## <a name="scope-pane"></a>Kapsam bölmesi
Merhaba **kapsam** bölmesidir hello StorSimple Snapshot Manager UI soldaki bölmede hello. Merhaba console (veya düğüm) ağacı içerir ve hello birincil gezinti için StorSimple Snapshot Manager mekanizmadır. 

### <a name="scope-pane-structure"></a>Kapsam bölmesi yapısı
Merhaba **kapsam** bölmesi, bir ağaç yapısı olarak düzenlenmiş bir dizi tıklanabilir nesneleri (düğümler) içerir. 

![Kapsam bölmesi](./media/storsimple-use-snapshot-manager/HCS_SSM_Scope_pane.png) 

* tooexpand veya bir düğümü Daralt hello ok simgesine sonraki toohello düğüm adı'ı tıklatın.
* tooview hello durumu veya bir düğümün içeriğini hello düğüm adı tıklatın. Merhaba bilgileri görünür hello **sonuçları** bölmesi. 

Merhaba **kapsam** bölmesinde düğümler aşağıdaki hello içerir: 

* [Cihazlar düğümü](#devices-node) 
* [Birimleri düğümü](#volumes-node) 
* [Birim grupları düğümü](#volume-groups-node) 
* [Yedekleme ilkeleri düğümü](#backup-policies-node) 
* [Yedekleme kataloğu düğümü](#backup-catalog-node) 
* [İşlerini düğümü](#jobs-node) 

### <a name="scope-pane-tasks"></a>Kapsam bölmesi görevleri
Merhaba kullanabilirsiniz **kapsam** bölmesinde toocomplete belirli bir düğümde bir eylem. bir görev tooselect hello aşağıdakilerden birini yapın:

* Merhaba düğümünü sağ tıklatın ve ardından görüntülenen hello menüsünden hello görevini seçin.
* Merhaba düğümünü tıklatın ve ardından **eylem** hello menü çubuğunda. Başlangıç görevi görüntülenen hello menüsünden seçin.
* Hello seçip hello eylemde tıklatıp Hello düğümü **Eylemler** bölmesi.

Bir düğüm seçin ve görev listesi bu yöntemleri toosee birini kullanın, bu düğüm üzerinde gerçekleştirilen eylemler gösterilmektedir.

### <a name="devices-node"></a>Cihazlar düğümü
Merhaba **aygıtları** hello StorSimple cihazları ve bağlı tooStorSimple anlık görüntü Yöneticisi'ni StorSimple sanal cihazlar düğümünü temsil eder. Bu düğüm tooconnect seçin ve bir aygıtı yapılandırmak ve ilişkili birimler, birimler grupları ve varolan yedek kopyaları alma. Birden çok cihazı tek bir ana bilgisayara bağlı tooa olabilir.

* tooexpand hello düğümü hello ok simgesini tıklatın ardından çok**aygıtları**.
* toosee kullanılabilir Eylemler menüsü sağ hello **aygıtları** düğüm veya sağ hello görünür hello düğümün herhangi birinden Genişletilmiş Görünüm.
* toosee yapılandırılmış aygıtların listesini tıklatın **aygıtları** hello içinde **kapsam** bölmesi. Her bir cihaz hakkında bilgi ile birlikte cihazların Merhaba listesi görünür hello **sonuçları** bölmesi.

### <a name="volumes-node"></a>Birimleri düğümü
Merhaba **birimleri** düğümü hello ana bilgisayarı, iSCSI ve bu aygıt üzerinden bulunan yoluyla bulunan dahil olmak üzere tarafından bağlı toohello birimlerin karşılık hello sürücüleri temsil eder. Bu düğüm tooview hello listesinden kullanılabilir birimlerin kullanabilir ve ayrı birimleri toovolume grupları atayabilirsiniz.

* tooexpand hello düğümü hello ok simgesini tıklatın ardından çok**birimleri**.
* toosee kullanılabilir Eylemler menüsü sağ hello **birimleri** düğüm ya da sağ tıklatma hello görünür hello düğümün herhangi birinden Genişletilmiş Görünüm.
* toosee birimlerin listesini tıklatın **birimleri** hello içinde **kapsam** bölmesi. her birim hakkında bilgi ile birlikte birimleri Hello listesi görünür hello **sonuçları** bölmesi.

### <a name="volume-groups-node"></a>Birim grupları düğümü
Birim grupları olarak da bilinen tutarlılık gruplarıdır. Her birim grubu tooensure uygulama tutarlılığı yedekleme işlemleri sırasında yardımcı olan bir uygulama ile ilgili birimlerin havuzudur. Kullanım hello **birim grupları** düğümü tooconfigure bu grupların ve tootake etkileşimli yedekleri veya yedekleme zamanlamaları oluşturun. 

* tooexpand hello düğümü hello ok simgesini tıklatın ardından çok**birim grupları**.
* toosee kullanılabilir Eylemler menüsü sağ hello **birim grupları** düğüm ya da sağ tıklatma hello görünür hello düğümün herhangi birinden Genişletilmiş Görünüm.
* toosee birim gruplarının bir listesini tıklatın **birim grupları** hello içinde **kapsam** bölmesi. her birim grubu hakkında bilgi ile birlikte toplu gruplarının Hello listesi görüntülenir hello **sonuçları** bölmesi.

### <a name="backup-policies-node"></a>Yedekleme ilkeleri düğümü
Yedekleme ilkelerdir iş zamanlamalarını, yerel ve bulut anlık görüntüleri. Kullanım hello **yedekleme ilkeleri** düğüm toospecify bir yedekleme ne sıklıkta oluşturulur ve bir yedek ne kadar süreyle olmalıdır korunur. 

* tooexpand hello düğümü hello ok simgesini tıklatın ardından çok**yedekleme ilkeleri**.
* toosee kullanılabilir Eylemler menüsü sağ hello **yedekleme ilkeleri** düğüm ya da sağ tıklatma hello görünür hello düğümün herhangi birinden Genişletilmiş Görünüm.
* toosee yedekleme ilkelerinin bir listesini tıklatın **yedekleme ilkeleri** hello içinde **kapsam** bölmesi. Her İlkesi hakkında bilgi ile birlikte yedekleme ilkeleri Hello listesi görünür hello **sonuçları** bölmesi.

> [!NOTE]
> En fazla 64 yedeklemeleri tutabilirsiniz.


### <a name="backup-catalog-node"></a>Yedekleme kataloğu düğümü
Merhaba **yedekleme kataloğu** düğümü yerinde ve şirket dışı birimlerin yedekleri, Azure StorSimple listesini içerir. Bu düğüm birim grubu tarafından düzenlenir ve yerel anlık görüntüler için ayrı yapıları her birim grubu kapsayıcısı içerir (Merhaba **yerel anlık görüntü**s düğüm) ve bulut anlık görüntüleri (Merhaba **bulut anlık görüntüleri** düğümü ). Her birim grubu kapsayıcısı genişletildiğinde, etkileşimli olarak veya yapılandırılmış bir ilke tarafından gerçekleştirilen tüm hello başarılı yedeklemeler listelenir.

* tooexpand hello düğümü hello ok simgesini tıklatın ardından çok**yedekleme kataloğu**.
* toosee kullanılabilir Eylemler menüsü sağ hello **yedekleme kataloğu** düğüm ya da sağ tıklatma hello görünür hello düğümün herhangi birinden Genişletilmiş Görünüm.
* toosee yedekleme anlık görüntülerinin listesini tıklatın **yedekleme kataloğu** hello içinde **kapsam** bölmesi. Her anlık görüntü hakkında bilgi ile birlikte anlık görüntüleri Hello listesi görünür hello **sonuçları** bölmesi.

### <a name="local-snapshots-node"></a>Yerel anlık görüntüleri düğümü
Merhaba **yerel anlık görüntüleri** düğümü bir özel birim grubu yerel anlık görüntüleri listeler. Merhaba düğümü hello altında bulunan **yedekleme kataloğu** hello düğümünde **kapsam** bölmesi. Yerel anlık görüntüleri zaman içinde nokta hello Azure StorSimple cihazında depolanmış birim verilerini kopyalarıdır. Genellikle, bu yedekleme türü oluşturulabilir ve hızlı bir şekilde geri. Yerel bir yedek kopya gibi yerel bir anlık görüntü kullanabilirsiniz.

* tooexpand hello düğümü hello ok simgesini tıklatın ardından çok**yerel anlık görüntüleri**.
* toosee kullanılabilir Eylemler menüsü sağ hello **yerel anlık görüntüleri** düğüm veya sağ hello görünür hello düğümün herhangi birinden Genişletilmiş Görünüm.
* toosee yerel anlık görüntüler, listesini tıklatın **yerel anlık görüntüleri** hello içinde **kapsam** bölmesi. Her anlık görüntü hakkında bilgi ile birlikte anlık görüntüleri Hello listesi görünür hello **sonuçları** bölmesi.

### <a name="cloud-snapshots-node"></a>Bulut anlık görüntüleri düğümü
Merhaba **bulut anlık görüntüleri** düğümü bir özel birim grubu için bulut anlık görüntüleri listeler. Merhaba düğümü hello altında bulunan **yedekleme kataloğu** hello düğümünde **kapsam** bölmesi. Bulut anlık görüntüleri zaman içinde nokta hello bulutta depolanan birim verilerini kopyalarıdır. Bir bulut anlık görüntüsü eşdeğerdir farklı, şirket dışı depolama sisteminizde çoğaltılan tooa anlık görüntü. Bulut anlık görüntüleri olağanüstü durum kurtarma senaryolarında özellikle kullanışlıdır.

* tooexpand hello düğümü hello ok simgesini tıklatın ardından çok**bulut anlık görüntüleri**.
* toosee kullanılabilir Eylemler menüsü sağ hello **bulut anlık görüntüleri** düğüm ya da sağ tıklatma hello görünür hello düğümün herhangi birinden Genişletilmiş Görünüm.
* toosee bulut anlık görüntüleri, listesini tıklatın **bulut anlık görüntüleri** hello içinde **kapsam** bölmesi. Her anlık görüntü hakkında bilgi ile birlikte anlık görüntüleri Hello listesi görünür hello **sonuçları** bölmesi.

### <a name="jobs-node"></a>İşlerini düğümü
Merhaba **işleri** düğümü zamanlanmış, çalışan ve son tamamlanan yedekleme işleri hakkında bilgiler içerir. 

* tooexpand hello düğümü hello ok simgesini tıklatın ardından çok**işleri**.
* toosee kullanılabilir Eylemler menüsü sağ hello **işleri** düğüm ya da sağ tıklatma hello görünür hello düğümün herhangi birinden Genişletilmiş Görünüm.
* toosee zamanlanmış işlerin bir listesini genişletin hello **işleri** düğümünü ve ardından **zamanlanmış**. Merhaba önceden yapılandırılmış işler ve her bir iş hakkında bilgi listesi görünür hello **sonuçları** bölmesi. 
* toosee tamamlanmış işlerin bir listesini genişletin hello **işleri** düğümünü ve ardından **son 24 saat**. Son 24 saat hello tamamlanmış işlerin bir listesini hello görünür **sonuçları** bölmesi. Merhaba **sonuçları** bölmesinde her tamamlanmış bir iş hakkında bilgiler de içerir.
* toosee çalışmakta olan, işlerin bir listesini genişletin hello **işleri** düğümünü ve ardından **çalıştıran**. işler ve her işle ilgili bilgileri şu anda çalışan hello listesi görünür hello **sonuçları** bölmesi.

## <a name="results-pane"></a>Sonuçlar Bölmesi
Merhaba **sonuçları** bölmesidir hello Orta bölmede hello StorSimple anlık görüntü Yöneticisi kullanıcı Arabirimi. Listeler ve hello Seçtiğiniz hello düğümü için ayrıntılı durum bilgilerini içeren **kapsam** bölmesi.

### <a name="example"></a>Örnek
Örneğin, aşağıdaki toosee hello hello tıklatın **birim grupları** hello düğümünde **kapsam** bölmesi. Merhaba **sonuçları** bölmesi her grup hakkında ayrıntılarla birim gruplarının bir listesini görüntüler.

![Sonuçlar Bölmesi](./media/storsimple-use-snapshot-manager/HCS_SSM_Results_pane.png) 

Hello gösterilen hello ayrıntıları yapılandırabilirsiniz **sonuçları** bölmesinde: hello bir düğümüne sağ tıklayın **kapsam** bölmesinde tıklatın **Görünüm**ve ardından **Ekle/Kaldır Sütunları**.

## <a name="actions-pane"></a>Eylemler bölmesi
Merhaba **Eylemler** bölmesidir hello StorSimple Snapshot Manager UI sağ bölmede hello. Başlangıç düğümü, görünümü veya hello Seçtiğiniz veri gerçekleştirebileceğiniz işlemler menüsüne içeren **kapsam** bölmesinde veya **sonuçları** bölmesi. Merhaba **Eylemler** bölmesidir aynı komutları hello hello **eylem** hello öğelerinde kullanılabilir menüleri **kapsam** bölmesinde ve **sonuçları**bölmesi. İçin bir açıklama her eylemin hello hello tabloya bakın **eylem** menü bölümü.

### <a name="examples"></a>Örnekler
Aşağıdaki örnekte hello toosee hello **kapsam** bölmesinde hello genişletin **işleri** düğümü ve tıklatın **zamanlanmış**. Merhaba **Eylemler** bölmesi hello hello kullanılabilir eylemleri görüntüler **zamanlanmış** düğümü.

![Eylemler bölmesi zamanlanmış işler örneği](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane.png) 

toosee daha seçenekleri, hello **kapsam** bölmesinde, hello genişletin **işleri** düğümü, tıklatın **zamanlanmış**ve ardından hello zamanlanmış bir işi **sonuçları**bölmesi. Merhaba **Eylemler** bölmesi hello aşağıdaki örnekte gösterildiği gibi hello kullanılabilir eylemler hello zamanlanmış işi için görüntüler.

![Eylemler bölmesi iş eylemleri örneği](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

## <a name="keyboard-navigation-and-shortcuts"></a>Klavye gezinme ve kısayollar
StorSimple Snapshot Manager hello erişilebilirlik özelliklerini hello Windows işletim sistemi ve hello Microsoft Yönetim Konsolu (MMC) sağlar. Ayrıca bazı klavye gezinti özellikleri ve belirli toohello StorSimple Snapshot Manager kısayolları hello aşağıdaki bölümlerde açıklandığı gibi içerir.

* [Klavye gezinti tuşları](#keyboard-navigation-keys) 
* [Menü çubuğu kısayol tuşları](#menu-bar-shortcut-keys) 
* [Kapsam bölmesi kısayol tuşları](#scope-pane-shortcut-keys) 

### <a name="keyboard-navigation-keys"></a>Klavye gezinti tuşları
Merhaba aşağıdaki tabloda toonavigate hello StorSimple Snapshot Manager kullanıcı arabirimini kullanabilirsiniz hello anahtarları açıklanmaktadır. 

| Gezinti anahtarı | Eylem |
|:--- |:--- |
| Aşağı ok tuşu |Aşağı ok anahtar toomove Hello dikey kullanmak menüsü veya bölmesindeki toohello sonraki öğe. |
| Girin |Merhaba Enter anahtar toocomplete bir eylem tuşuna basın ve toohello sonraki adıma devam edin. Örneğin, Enter tooselect basabilirsiniz **sonraki**, **Tamam**, veya **oluşturma**, ve bir Sihirbazı'nda toohello sonraki adıma gidin. |
| ESC |Merhaba Esc anahtar tooclose menü veya toocancel tuşuna basın ve bir sayfasını kapatın. |
| F1 |Merhaba F1 anahtar tooview Yardım konusunun hello şu anda etkin penceresini tuşuna basın. |
| F5 |Merhaba F5 anahtar toorefresh bir düğüm tuşuna basın. |
| F6 |Merhaba F6 anahtar toomove hello gelen basın **kapsam** bölmesinde toohello **sonuçları** bölmesi. |
| F10 |Merhaba F10 anahtar toogo toohello menü çubuğu tuşlarına basın. |
| Sol Ok tuşu |Ok anahtar toomove yatay bir menü çubuğu seçeneği toohello önceki seçeneğinden sol hello kullanın. Önceki toohello taşıdığınızda hello önceki öğesi için öğe hello menü çubuğunda, hello eylemi (veya içerik) menüsü görüntülenir. |
| Sağ ok tuşu |Merhaba sağ ok anahtar toomove yatay menüsünden bir seçenek toohello çubuğu sonraki kullanın. Taşıdığınızda toohello sonraki hello menü çubuğunda, hello eylemi (veya içerik) öğesi menüsü hello yeni öğe için görüntülenir. |
| SEKME tuşu |Merhaba konsolu veya toohello sonraki seçimi veya metin kutusunda bir sayfa üzerinde Hello sekmesini anahtar toomove toohello sonraki bölmesini kullanın. |
| Yukarı Ok tuşu |Yukarı Ok anahtar toomove Hello dikey kullanmak toohello önceki öğede menüsü veya bölmesi. |

### <a name="menu-bar-shortcut-keys"></a>Menü çubuğu kısayol tuşları
Merhaba aşağıdaki tabloda hello kısayol tuş birleşimleri hello menü çubuğu için açıklanmaktadır. Merhaba kısayol tuşlarına basın ve hello menüsü açılır sonra menü kısayol tuşları (altı çizili anahtarları hello menüsünde hello) kullanabilirsiniz. Merhaba menü çubuğu hakkında daha fazla bilgi için çok Git[menü çubuğu](#menu-bar).

| Kısayol | Sonuç | Menü kısayol tuşu | Sonuç |
|:--- |:--- |:--- |:--- |
| ALT + F |Açılır hello **dosya** menüsü. |N |Yeni bir konsol örneğini açar. |
|  |O |Açılır hello **Yönetimsel Araçlar** sayfası. | |
|  |S |Merhaba StorSimple Snapshot Manager konsolunu kaydeder. | |
|  |A |Açılır hello **Kaydet** sayfası. | |
|  |M |Açılır hello **Ekle/Kaldır ek bileşenini** sayfası. | |
|  |P |Açılır hello **seçenekleri** sayfası. | |
|  |H |Çevrimiçi Yardım'ı açar. | |
| ALT + A |Açılır hello **eylem** menüsü. |I |Merhaba alma görüntüleme seçeneği açar ve kapatır. |
|  |W |Yeni bir StorSimple Snapshot Manager konsolu açılır. | |
|  |F |Merhaba StorSimple Snapshot Manager konsol güncelleştirir. | |
|  |L |Açılır hello **Liste Ver** sayfası. | |
|  |H |Çevrimiçi Yardım'ı açar. | |
| ALT + V |Açılır hello **Görünüm** menüsü. |A |Açılır hello **Sütun Ekle/Kaldır** sayfası. |
|  |U |Açılır hello **Görünümü Özelleştir** sayfası. | |
| ALT + O |Açılır hello **Sık Kullanılanlar** menüsü. |A |Açılır hello **tooFavorites ekleme** sayfası. |
|  |O |Açılır hello **kullanılanları** sayfası. | |
| ALT + W |Açılır hello **penceresi** menüsü. |N |Başka bir StorSimple Snapshot Manager penceresi açılır. |
|  |C |Tüm açık konsol pencerelerinin geçişli stil içinde görüntüler. | |
|  |T |Tüm açık konsol pencerelerinin bir kılavuz düzeni görüntüler. | |
|  |I |Merhaba ekranınızın yatay bir satırda simgeleri yerleştirir. | |
| ALT + H |Açılır hello **yardımcı** menüsü. |H |Çevrimiçi Yardım'ı açar. |
|  |T |Merhaba Microsoft TechNet Tech Center web sayfasını açar. | |
|  |A |Açılır hello **Microsoft Yönetim Konsolu hakkında** sayfası. | |

### <a name="scope-pane-shortcut-keys"></a>Kapsam bölmesi kısayol tuşları
Merhaba aşağıdaki tablolarda hello kısayol tuş bileşimlerini her düğüm için hello Göster **kapsam** bölmesi. 

* [Cihazlar düğümü kısayol tuşları](#devices-node-shortcut-keys)
* [Birimleri düğümü kısayol tuşları](#volumes-node-shortcut-keys)
* [Birim grupları düğümü kısayol tuşları](#volume-groups-node-shortcut-keys)
* [Yedekleme ilkeleri düğümü kısayol tuşları](#backup-policies-node-shortcut-keys)
* [Yedekleme kataloğu düğümü kısayol tuşları](#backup-catalog-node-shortcut-keys)
* [İşlerini düğümü kısayol tuşları](#jobs-node-shortcut-keys)

#### <a name="devices-node-shortcut-keys"></a>Cihazlar düğümü kısayol tuşları
| Menü kısayolu | Sonuç |
|:--- |:--- |
| C |Açılır hello **bir aygıt yapılandırma** sayfası. |
| D |Cihazları ve cihaz ayrıntılarını Hello listesini yeniler. |
| V |Açılır hello **Görünüm** menüsü. |
| W |Yeni bir StorSimple Snapshot Manager konsol odaklanmış hello üzerinde açılır **ayrıntıları** düğümü. |
| F |Merhaba StorSimple Snapshot Manager konsol güncelleştirir. |
| L |Açılır hello **Liste Ver** sayfası. |
| H |Çevrimiçi Yardım'ı açar. |

#### <a name="volumes-node-shortcut-keys"></a>Birimleri düğümü kısayol tuşları
| Menü kısayolu | Sonuç |
|:--- |:--- |
| V |Birimleri güncelleştirmeleri hello listesi. |
| V (iki kez basın) |Açılır hello **Görünüm** menüsü. |
| W |Yeni bir StorSimple Snapshot Manager konsol odaklanmış hello üzerinde açılır **birimleri** düğümü. |
| F |Merhaba StorSimple Snapshot Manager konsol güncelleştirir. |
| L |Açılır hello **Liste Ver** sayfası. |
| H |Çevrimiçi Yardım'ı açar. |

#### <a name="volume-groups-node-shortcut-keys"></a>Birim grupları düğümü kısayol tuşları
| Menü kısayolu | Sonuç |
|:--- |:--- |
| G |Açılır hello **bir birim grubu oluşturun** sayfası. |
| V |Açılır hello **Görünüm** menüsü. |
| W |Yeni bir StorSimple Snapshot Manager konsol odaklanmış hello üzerinde açılır **birim grupları** düğümü. |
| F |Merhaba StorSimple Snapshot Manager konsol güncelleştirir. |
| L |Açılır hello **Liste Ver** sayfası. |
| H |Çevrimiçi Yardım'ı açar. |

#### <a name="backup-policies-node-shortcut-keys"></a>Yedekleme ilkeleri düğümü kısayol tuşları
| Menü kısayolu | Sonuç |
|:--- |:--- |
| B |Açılır hello **bir ilke oluşturmak** sayfası. |
| V |Açılır hello **Görünüm** menüsü. |
| W |Yeni bir StorSimple Snapshot Manager konsol odaklanmış hello üzerinde açılır **birim grupları** düğümü. |
| F |Merhaba StorSimple Snapshot Manager konsol güncelleştirir. |
| L |Açılır hello ** Liste Ver ** sayfası. |
| H |Çevrimiçi Yardım'ı açar. |

#### <a name="backup-catalog-node-shortcut-keys"></a>Yedekleme kataloğu düğümü kısayol tuşları
| Menü kısayolu | Sonuç |
|:--- |:--- |
| W |Yeni bir StorSimple Snapshot Manager konsol odaklanmış hello üzerinde açılır **birim grupları** düğümü. |
| F |Merhaba StorSimple Snapshot Manager konsol güncelleştirir. |
| H |Çevrimiçi Yardım'ı açar. |

#### <a name="jobs-node-shortcut-keys"></a>İşlerini düğümü kısayol tuşları
| Menü kısayolu | Sonuç |
|:--- |:--- |
| V |Açılır hello **Görünüm** menüsü. |
| W |Yeni bir StorSimple Snapshot Manager konsol odaklanmış hello üzerinde açılır **işleri** düğümü. |
| F |Merhaba StorSimple Snapshot Manager konsol güncelleştirir. |
| L |Açılır hello **Liste Ver** sayfası. |
| H |Çevrimiçi Yardım'ı açar |

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[StorSimple Snapshot Manager tooadminister StorSimple çözümünüzün kullanmak](storsimple-snapshot-manager-admin.md).
* Nasıl çok öğrenin[StorSimple Snapshot Manager tooconnect kullanın ve cihazları yönetmek](storsimple-snapshot-manager-manage-devices.md).

