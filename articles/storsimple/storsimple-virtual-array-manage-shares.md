---
title: "StorSimple sanal dizinin aaaManage paylaşır | Microsoft Docs"
description: "Merhaba StorSimple Aygıt Yöneticisi'ni tanımlar ve açıklar nasıl toouse, StorSimple sanal dizinizi toomanage paylaşımlarında."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: 0a799c83-fde5-4f3f-af0e-67535d1882b6
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: manuaery
ms.openlocfilehash: 9b57d7ec7c0b7de5a22e1b816daa8852d0f32a48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-shares-on-hello-storsimple-virtual-array"></a>StorSimple sanal dizinin hello üzerinde Hello StorSimple cihaz Yöneticisi hizmeti toomanage paylaşımları kullanın

## <a name="overview"></a>Genel Bakış

Bu öğretici nasıl toouse StorSimple cihaz Yöneticisi hizmeti toocreate hello ve StorSimple sanal dizinizi paylaşımlarında yönetmek açıklanmaktadır.

Merhaba StorSimple cihaz Yöneticisi hizmeti hello StorSimple çözümünüzün bir tek web arabiriminden yönetmenizi sağlayan Azure portalı bir uzantıdır. Toplama toomanaging paylaşımları ve birimler, hello StorSimple cihaz Yöneticisi hizmeti tooview kullanın ve cihazları yönetmek, uyarıları görüntüleyebilir, yedekleme ilkelerini yönetme ve hello yedekleme kataloğunu yönetir.

## <a name="share-types"></a>Paylaşım türleri

StorSimple paylaşımları olabilir:

* **Yerel olarak sabitlenmiş**: bu paylaşımlar verileri her zaman hello dizisinde kalır ve toohello buluta dağıtılmamasını.
* **Katmanlı**: bu paylaşımlar verilerde toohello bulut sığdırmaya. Katmanlı bir paylaşımı oluşturduğunuzda, hello alanın % 10'yaklaşık hello yerel katmanında sağlanır ve hello alanı % 90'ını hello bulutta sağlanır. Örneğin, 1 TB paylaşımı sağlanan, 100 GB hello yerel alan bulunması ve 900 GB hello bulutta kullanılacak ne zaman veri katmanlarını hello. Bu, sırayla hello cihazda tüm hello yerel alana çalıştırırsanız (Merhaba % 10 hello yerel katmanı kullanılamaz gerektirdiğinden), katmanlı bir paylaşım sağlayamazsınız olduğunu gösterir.

### <a name="provisioned-capacity"></a>Sağlanan kapasite

Aşağıdaki tablonun her paylaşım türü için en fazla sağlanan kapasite toohello bakın.

| **Sınır tanımlayıcısı** | **Sınırı** |
| --- | --- |
| Katmanlı bir paylaşımı en küçük boyut |500 GB |
| Katmanlı bir paylaşımı en büyük boyutu |20 TB |
| Yerel olarak sabitlenmiş bir paylaşımı en küçük boyut |50 GB |
| Yerel olarak sabitlenmiş bir paylaşımı en büyük boyutu |2 TB |

## <a name="hello-shares-blade"></a>Merhaba paylaşımları dikey penceresi

Merhaba **paylaşımları** StorSimple hizmeti Özet dikey menüsünde belirli bir StorSimple dizi depolama paylaşımları hello listesini görüntüler ve toomanage sağlayan bunları.

![Paylaşımlar dikey penceresi](./media/storsimple-virtual-array-manage-shares/shares-blade.png)

Bir paylaşım öznitelikleri bir dizi oluşur:

* **Paylaşım adı** – benzersiz olmalı ve hello paylaşımı tanımlamanıza yardımcı olan açıklayıcı bir ad.
* **Durum** – çevrimiçi veya çevrimdışı olabilir. Bir paylaşım çevrimdışı olduğunda, kullanıcılar hello paylaşımının mümkün tooaccess olmayacaktır.
* **Tür** – hello paylaşımı olup olmadığını belirten **katmanlı** (Merhaba varsayılan) veya **yerel olarak sabitlenmiş**.
* **Kapasite** – hello karşılaştırılan toohello toplam hello paylaşımında depolanan veri miktarını olarak kullanılan veri miktarını belirtir.
* **Açıklama** – hello paylaşımı açıklamak yardımcı olan isteğe bağlı bir ayar.
* **İzinleri** -Windows Explorer ile yönetilebilir hello NTFS izinleri toohello paylaşımı.
* **Yedekleme** – hello StorSimple sanal dizinin tüm paylaşımlar yedekleme için otomatik olarak etkinleştirilmiş durumda.

![Paylaşımlar ayrıntıları](./media/storsimple-virtual-array-manage-shares/share-details.png)

Bu öğretici tooperform hello görevleri aşağıdaki Hello yönergeleri kullanın:

* Paylaşım Ekle
* Bir paylaşımı değiştirme
* Bir paylaşım çevrimdışı duruma getirin
* Bir paylaşımı silme

## <a name="add-a-share"></a>Paylaşım Ekle

1. Merhaba StorSimple hizmeti Özet dikey penceresinden, tıklayın **+ Ekle paylaşımı** hello komut çubuğundan. Merhaba açılır **Ekle paylaşımı** dikey.

    ![Paylaşım Ekle](./media/storsimple-virtual-array-manage-shares/add-share.png)

2. Merhaba, **Ekle paylaşımı** dikey penceresinde, aşağıdaki hello:
   
    1. Merhaba, **paylaşım adı** alanında, paylaşımınıza için benzersiz bir ad girin. Merhaba adı 3 too127 karakter içeren bir dize olmalıdır.

    2. İsteğe bağlı bir **açıklama** hello paylaşımı için. Merhaba açıklama hello paylaşım sahiplerini tanımlamaya yardımcı olur.

    3. Merhaba, **türü** açılır listesinde, belirleyin olup olmadığını toocreate bir **katmanlı** veya **yerel olarak sabitlenmiş** paylaşın. Yerel GARANTİLERİN, düşük gecikme ve yüksek performansın gerektiği iş yükleri için seçin **Paylaşımı'yerel olarak sabitlenmiş**. Diğer tüm veriler için seçin **katmanlı** paylaşın.

    4. Merhaba, **kapasite** alanında, hello hello paylaşımı boyutunu belirtin. Katmanlı bir paylaşımı, 500 GB ile 20 TB arasında olmalıdır ve yerel olarak sabitlenmiş bir paylaşımı, 50 GB ile 2 TB arasında olmalıdır.

    5. Merhaba, **kümesine varsayılan tam izinleri** alan, hello izinleri toohello kullanıcı veya bu paylaşıma erişen hello grubuna atayın. Merhaba kullanıcı veya hello kullanıcı grubunda Hello adını belirtin  _john@contoso.com_  biçimi. Bir kullanıcı grubu (yerine tek bir kullanıcı) tooallow yönetici ayrıcalıkları tooaccess bu paylaşımları kullanmanızı öneririz. Merhaba izinlerini burada atadıktan sonra bu izinleri dosya Gezgini toomodify sonra kullanabilirsiniz.
3. Paylaşımınıza yapılandırma tamamladığınızda tıklatın **oluşturma**. Bir paylaşımı ile belirtilen hello oluşturulacak ayarları ve bir bildirim görürsünüz. Varsayılan olarak, yedekleme hello paylaşımı için etkin.
4. Paylaşım hello tooconfirm edildi başarıyla oluşturuldu, Git toohello **paylaşımları** dikey. Listelenen paylaşmak hello görmeniz gerekir.
   
    ![Paylaşımı oluşturma başarılı](./media/storsimple-virtual-array-manage-shares/share-success.png)

## <a name="modify-a-share"></a>Bir paylaşımı değiştirme

Merhaba paylaşımı toochange hello açıklama gerektiğinde bir paylaşımı değiştirin. Merhaba paylaşımı oluşturulduktan sonra başka bir paylaşım özellikleri değiştirilebilir.

#### <a name="toomodify-a-share"></a>toomodify bir paylaşımı

1. Merhaba gelen **paylaşımları** seçin istediğinizden, toomodify paylaşımı üzerinde hangi hello bulunduğu sanal dizinin hello hello StorSimple hizmeti Özet dikey ayarı.
2. **Seçin** hello paylaşımı tooview hello geçerli açıklama ve değiştirebilirsiniz.
3. Merhaba tıklayarak yaptığınız değişiklikleri kaydetmek **kaydetmek** komut çubuğu. Belirtilen ayarlarınızı uygulanır ve bir bildirim görürsünüz.
   
    ![ Paylaşım Düzenle](./media/storsimple-virtual-array-manage-shares/share-edit.png)

## <a name="take-a-share-offline"></a>Bir paylaşım çevrimdışı duruma getirin

Toomodify veya delete planlarken tootake çevrimdışı bir paylaşımı gerekebilir. Bir paylaşım çevrimdışı olduğunda okuma-yazma erişimi için kullanılabilir değildir. Tootake hello paylaşımı çevrimdışı hello aygıt yanı sıra hello ana bilgisayar gerekir.

#### <a name="tootake-a-share-offline"></a>tootake çevrimdışı bir paylaşımı

1. Söz konusu hello paylaşan çevrimdışı duruma getirmeden önce kullanımda olmadığından emin olun.
2. Merhaba paylaşımı hello aşağıdaki adımları gerçekleştirerek çevrimdışı hello dizisinde alın:
   
    1. Merhaba gelen **paylaşımları** seçin istediğinizden, çevrimdışı tootake paylaşımı üzerinde hangi hello bulunduğu sanal dizinin hello hello StorSimple hizmeti Özet dikey ayarı.

    2. **Seçin** hello paylaşım ve tıklatın **...**  (Alternatif olarak bu satırı sağ) ve hello bağlam menüsünden seçin **çevrimdışına**.
     
        ![Çevrimdışı paylaşımı](./media/storsimple-virtual-array-manage-shares/shares-offline.png)

    3. Merhaba hello bilgileri gözden **çevrimdışına** dikey ve hello işleminin onaylamış olursunuz. Tıklatın **çevrimdışına** tootake hello çevrimdışı paylaşımı. Merhaba işlem devam ettiğinden, bir bildirim görürsünüz.

    4. Paylaşım hello tooconfirm çevrimdışı, Git toohello başarıyla alındığı **paylaşımları** dikey. Çevrimdışı olarak hello paylaşımı hello durumunu görmeniz gerekir.

## <a name="delete-a-share"></a>Bir paylaşımı silme

> [!IMPORTANT]
> Yalnızca çevrimdışı ise, bir paylaşım silebilirsiniz.


Aşağıdaki adımları toodelete bir paylaşımı hello tamamlayın.

#### <a name="toodelete-a-share"></a>toodelete bir paylaşımı

1. Merhaba gelen **paylaşımları** seçin hangi hello paylaşımında istediğiniz toodelete bulunduğu sanal dizinin hello hello StorSimple hizmeti Özet dikey ayarı.
2. **Seçin** hello paylaşım ve tıklatın **...**  (Alternatif olarak bu satırı sağ) ve hello bağlam menüsünden seçin **silmek**.
   
    ![Paylaşımı silin](./media/storsimple-virtual-array-manage-shares/share-delete.png)
3. Merhaba durumunu denetlemek hello payı toodelete istiyor. Merhaba paylaşımı toodelete istediğiniz çevrimdışı durumda değilse, onu önce çevrimdışına. Merhaba adımları [bir paylaşımı çevrimdışına](#take-a-share-offline).
4. Merhaba onaylamanız istendiğinde **silmek** dikey penceresinde hello onay kabul edin ve tıklatın **silmek**. Merhaba paylaşım şimdi silinecek ve hello **paylaşımları** dikey penceresinde hello sanal dizi paylaşımlarının hello güncelleştirilmiş listesini gösterir.

## <a name="next-steps"></a>Sonraki adımlar
Nasıl çok öğrenin[bir StorSimple paylaşımı kopyalama](storsimple-virtual-array-clone.md).

