---
title: StorSimple sanal dizinin aaaManage birimlerde | Microsoft Docs
description: "Merhaba StorSimple Aygıt Yöneticisi'ni tanımlar ve açıklar nasıl toouse, StorSimple sanal dizinizi toomanage birimlerde."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: caa6a26b-b7ba-4a05-b092-1a79450225cf
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 46aa6d7508b3e62f75a3b78ed73302b88320a0f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-service-toomanage-volumes-on-hello-storsimple-virtual-array"></a>Aygıt Yöneticisi'ni StorSimple hizmet toomanage hello StorSimple sanal dizinin birimlerde

## <a name="overview"></a>Genel Bakış

Bu öğretici nasıl toouse StorSimple cihaz Yöneticisi hizmeti toocreate hello ve StorSimple sanal dizinizi birimlerde yönetmek açıklanmaktadır.

Merhaba StorSimple cihaz Yöneticisi hizmeti hello StorSimple çözümünüzün bir tek web arabiriminden yönetmenizi sağlayan Azure portalı bir uzantıdır. Toplama toomanaging paylaşımları ve birimler, hello StorSimple cihaz Yöneticisi hizmeti tooview kullanın ve cihazları yönetmek, uyarıları görüntülemek ve görüntüleyebilir ve yedekleme ilkeleri ve hello yedekleme kataloğu yönetin.

## <a name="volume-types"></a>Birim türleri

StorSimple birimlerini olabilir:

* **Yerel olarak sabitlenmiş**: Bu birimlerdeki veriler her zaman hello dizisinde kalır ve toohello buluta dağıtılmamasını.
* **Katmanlı**: Bu birimlerdeki veriler toohello bulut sığdırmaya. Katmanlı birim oluşturduğunuzda, hello alanın % 10'yaklaşık hello yerel katmanında sağlanır ve % 90'hello alanı hello bulutta sağlanır. Örneğin, 1 TB birim sağlanan, 100 GB hello yerel alan bulunması ve 900 GB hello bulutta kullanılacak ne zaman veri katmanlarını hello. Bu, sırayla hello cihazda tüm hello yerel alana çalıştırırsanız (Merhaba % 10 hello yerel katmanı kullanılamaz gerektirdiğinden), katmanlı birim sağlayamazsınız olduğunu gösterir.

### <a name="provisioned-capacity"></a>Sağlanan kapasite
Aşağıdaki tabloda her bir birim türü için en fazla sağlanan kapasite toohello bakın.

| **Sınır tanımlayıcısı**                                       | **Sınırı**     |
|------------------------------------------------------------|---------------|
| Katmanlı birim en küçük boyut                            | 500 GB        |
| Katmanlı birim en büyük boyutu                            | 5 TB          |
| Yerel olarak sabitlenmiş bir birim en küçük boyut                    | 50 GB         |
| Yerel olarak sabitlenmiş bir birim en büyük boyutu                    | 500 GB        |

## <a name="hello-volumes-blade"></a>Merhaba birimleri dikey penceresi
Merhaba **birimleri** StorSimple hizmeti Özet dikey menüsünde belirli bir StorSimple dizi depolama birimleri hello listesini görüntüler ve toomanage sağlayan bunları.

![Birimleri dikey penceresi](./media/storsimple-virtual-array-manage-volumes/volumes-blade.png)

Bir birim öznitelikleri bir dizi oluşur:

* **Birim adı** – benzersiz olmalı ve hello birim tanımlamanıza yardımcı olan açıklayıcı bir ad.
* **Durum** – çevrimiçi veya çevrimdışı olabilir. Bir birim çevrimdışıysa, erişim toouse hello birim izin görünür tooinitiators (sunucu) değil.
* **Tür** – hello birim olup olmadığını belirten **katmanlı** (Merhaba varsayılan) veya **yerel olarak sabitlenmiş**.
* **Kapasite** – hello karşılaştırılan toohello toplam hello Başlatıcı (sunucu) tarafından depolanan veri miktarını olarak kullanılan veri miktarını belirtir.
* **Yedekleme** – durumda hello StorSimple sanal dizinin tüm birimleri otomatik olarak yedekleme için etkinleştirilir.
* **Bağlı Konaklar** – erişim toothis birim izin hello başlatıcıları (Sunucuları) belirtir.

![Birimleri ayrıntıları](./media/storsimple-virtual-array-manage-volumes/volume-details.png)

Bu öğretici tooperform hello görevleri aşağıdaki Hello yönergeleri kullanın:

* Birim Ekle
* Bir birim değiştirme
* Bir birim çevrimdışı duruma getirin
* Bir birim Sil

## <a name="add-a-volume"></a>Birim Ekle

1. Merhaba StorSimple hizmeti Özet dikey penceresinden, tıklayın **+ Add birim** hello komut çubuğundan. Merhaba açılır **birim ekleme** dikey.
   
    ![Birim ekle](./media/storsimple-virtual-array-manage-volumes/add-volume.png)
2. Merhaba, **birim ekleme** dikey penceresinde, aşağıdaki hello:
   
   * Merhaba, **birim adı** alanında, biriminiz için benzersiz bir ad girin. Merhaba adı 3 too127 karakter içeren bir dize olmalıdır.
   * Merhaba, **türü** açılır listesinde, belirleyin olup olmadığını toocreate bir **katmanlı** veya **yerel olarak sabitlenmiş** birim. Yerel GARANTİLERİN, düşük gecikme ve yüksek performansın gerektiği iş yükleri için seçin **birim'yerel olarak sabitlenmiş**. Diğer tüm veriler için seçin **katmanlı** birim.
   * Merhaba, **kapasite** alanında, hello hello birimin boyutunu belirtin. Katmanlı birim 500 GB ile 5 TB arasında olmalıdır ve yerel olarak sabitlenmiş bir birim 50 GB ve 500 GB arasında olması gerekir.
   * * Tıklatın **bağlı Konaklar**, tooconnect toothis birim istediğiniz ve ardından bir erişim denetimi kaydı (ACR) karşılık gelen toohello iSCSI başlatıcısı seçin **seçin**.
3. Yeni bir bağlı konak tooadd tıklatın **yeni Ekle**, hello ana bilgisayarı ve onun iSCSI için bir ad girin tam adını (IQN) ve ardından **Ekle**.
   
    ![Birim ekle](./media/storsimple-virtual-array-manage-volumes/volume-add-acr.png)
4. Biriminiz yapılandırma tamamladığınızda tıklatın **oluşturma**. Bir birim belirtilen hello ile oluşturulacak ayarlar ve aynı hello hello başarılı oluşturulmasını bir bildirim görürsünüz. Varsayılan olarak yedekleme hello birim için etkin.
5. Birim hello tooconfirm edildi başarıyla oluşturuldu, Git toohello **birimleri** dikey. Listelenen hello birim görmeniz gerekir.
   
    ![Birim oluşturma başarılı](./media/storsimple-virtual-array-manage-volumes/volume-success.png)

## <a name="modify-a-volume"></a>Bir birim değiştirme

Merhaba birime erişmek toochange hello konakları gerektiğinde bir birim değiştirin. Merhaba birim oluşturulduktan sonra hello biriminin diğer öznitelikleri değiştirilemez.

#### <a name="toomodify-a-volume"></a>toomodify bir birim

1. Merhaba gelen **birimleri** seçin istediğinizden, toomodify birim üzerinde hangi hello bulunduğu sanal dizinin hello hello StorSimple hizmeti Özet dikey ayarı.
2. **Seçin** hello birimi ve'ı tıklatın **bağlı Konaklar** tooview hello şu anda bağlı ana bilgisayar ve tooa farklı sunucu değiştirin.
   
    ![Toplu düzenleme](./media/storsimple-virtual-array-manage-volumes/volume-edit-acr.png)
3. Merhaba tıklayarak yaptığınız değişiklikleri kaydetmek **kaydetmek** komut çubuğu. Belirtilen ayarlarınızı uygulanır ve bir bildirim görürsünüz.

## <a name="take-a-volume-offline"></a>Bir birim çevrimdışı duruma getirin

Toomodify veya delete planlarken tootake çevrimdışı bir birim gerekebilir. Bir birim çevrimdışı olduğunda okuma-yazma erişimi için kullanılabilir değildir. Tootake hello birim çevrimdışı hello aygıt yanı sıra hello ana bilgisayar gerekir.

#### <a name="tootake-a-volume-offline"></a>tootake çevrimdışı bir birim

1. Söz konusu Hello birim çevrimdışı duruma getirmeden önce kullanımda olmadığından emin olun.
2. Çevrimdışı Hello birim hello konakta ilk alın. Bu, olası tüm hello birimdeki veri bozulması riskini ortadan kaldırır. Belirli adımlar için işletim sistemi için toohello yönergeler bakın.
3. Hello konak Hello birimde çevrimdışıysa, hello birim çevrimdışı hello dizisinde hello aşağıdaki adımları gerçekleştirerek başlatıldıktan sonra:
   
   * Merhaba gelen **birimleri** seçin istediğinizden, çevrimdışı tootake birim üzerinde hangi hello bulunduğu sanal dizinin hello hello StorSimple hizmeti Özet dikey ayarı.
   * **Seçin** hello birim ve tıklayın **...**  (Alternatif olarak bu satırı sağ) ve hello bağlam menüsünden seçin **çevrimdışına**.
     
        ![Çevrimdışı birim](./media/storsimple-virtual-array-manage-volumes/volume-offline.png)
   * Merhaba hello bilgileri gözden **çevrimdışına** dikey ve hello işleminin onaylamış olursunuz. Tıklatın **çevrimdışına** tootake hello çevrimdışı birim. Merhaba işlem devam ettiğinden, bir bildirim görürsünüz.
   * Merhaba birimi başarıyla çevrimdışı duruma tooconfirm Git toohello **birimleri** dikey. Merhaba birimin hello durumu çevrimdışı olarak görmeniz gerekir.
     
       ![Çevrimdışı birim onayı](./media/storsimple-virtual-array-manage-volumes/volume-offline-confirm.png)

## <a name="delete-a-volume"></a>Bir birim Sil

> [!IMPORTANT]
> Yalnızca çevrimdışı ise, bir birim silebilirsiniz.
> 
> 

Aşağıdaki adımları toodelete bir birim hello tamamlayın.

#### <a name="toodelete-a-volume"></a>toodelete bir birim

1. Merhaba gelen **birimleri** seçin istediğinizden, toodelete birim üzerinde hangi hello bulunduğu sanal dizinin hello hello StorSimple hizmeti Özet dikey ayarı.
2. **Seçin** hello birim ve tıklayın **...**  (Alternatif olarak bu satırı sağ) ve hello bağlam menüsünden seçin **silmek**.
   
    ![Birim Sil](./media/storsimple-virtual-array-manage-volumes/volume-delete.png)
3. Merhaba durumunu denetlemek hello hacmi toodelete istiyor. Merhaba birim toodelete istediğiniz çevrimdışı durumda değilse, bunu çevrimdışı ilk, aşağıdaki hello adımlar [bir birim çevrimdışına](#take-a-volume-offline).
4. Merhaba onaylamanız istendiğinde **silmek** dikey penceresinde hello onay kabul edin ve tıklatın **silmek**. Merhaba birim artık silinecek ve hello **birimleri** dikey penceresinde hello sanal dizi birimlerin hello güncelleştirilmiş listesini gösterir.

## <a name="next-steps"></a>Sonraki adımlar

Nasıl çok öğrenin[bir StorSimple biriminin kopyalama](storsimple-virtual-array-clone.md).

