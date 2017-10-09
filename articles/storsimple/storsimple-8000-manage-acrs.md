---
title: "StorSimple aaaManage erişim denetimi kayıtları | Microsoft Docs"
description: "Hangi ana bilgisayarların hello StorSimple cihazı tooa birimde bağlanabilir (ACRs) toodetermine toouse erişim denetimi kayıtları nasıl açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: alkohli
ms.openlocfilehash: cf532206e2c0bc49da853663ba34ae993ec2981d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Merhaba StorSimple Yöneticisi hizmet toomanage erişim denetimi kayıtları kullanın

## <a name="overview"></a>Genel Bakış
Erişim denetimi kayıtları (ACRs) hangi ana bilgisayarların hello StorSimple cihazı tooa birimde bağlanabilir toospecify izin verin. ACRs tooa belirli birimi ayarlayın ve hello iSCSI içeren hello konakların nitelikli adlar (IQN'ler). Bir konak tooconnect tooa birim çalıştığında hello aygıt hello IQN adı ve bir eşleşmesi durumunda hello bağlantı kurulur bu birimde ACR ilişkili hello denetler. Merhaba hello erişim denetimi kayıtları **yapılandırma** StorSimple cihaz Yöneticisi hizmeti dikey pencerenize bölümünü hello ana IQN'ler karşılık gelen hello ile tüm hello erişim denetimi kayıtları görüntülemek.

Bu öğretici ortak ACR ilgili görevleri aşağıdaki hello açıklanmaktadır:

* Bir erişim denetimi kaydı ekleme
* Bir erişim denetimi kaydı Düzenle
* Bir erişim denetimi kaydını sil

> [!IMPORTANT]
> * ACR tooa birim atarken bu hello birim bozuk olabilir çünkü hello birim aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişmediğinden dikkatli olun.
> * Bir ACR bir birimden silerken okuma-yazma kesilme hello silinmesine neden çünkü hello karşılık gelen barındıran hello birime erişimde değil emin olun.

## <a name="get-hello-iqn"></a>Merhaba IQN'sini Al

Aşağıdaki adımları tooget hello Windows Server 2012 çalıştıran bir Windows konağının IQN'sini hello gerçekleştirin.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]


## <a name="add-an-access-control-record"></a>Bir erişim denetimi kaydı ekleme
Merhaba kullandığınız **yapılandırma** hello StorSimple cihaz Yöneticisi hizmeti dikey tooadd ACRs bölümünde. Genellikle, bir birimle bir ACR ilişkilendireceğiniz.

Aşağıdaki adımları tooadd bir ACR hello gerçekleştirin.

#### <a name="tooadd-an-acr"></a>tooadd bir ACR

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin, hello hizmet adını ve ardından içinde hello çift **yapılandırma** 'yi tıklatın **erişim denetimi kayıtları**.
2. Merhaba, **erişim denetimi kayıtları** dikey penceresinde tıklatın **+ ACR eklemek**.

    ![ACR Ekle'yi tıklatın](./media/storsimple-8000-manage-acrs/createacr1.png)

3. Merhaba, **eklemek ACR** dikey penceresinde, adımları hello:

    1. Bir ad verin sağlayın.
    
    2. Windows Server konağınızda altında Hello IQN adını sağlayın **iSCSI başlatıcısı adı (IQN)**.

    3. Tıklatın **Ekle** toocreate hello ACR.

        ![ACR Ekle'yi tıklatın](./media/storsimple-8000-manage-acrs/createacr2.png)

4.  Merhaba, yeni ACR hello tablo ACRs listesinde görüntülenir eklendi.

    ![ACR Ekle'yi tıklatın](./media/storsimple-8000-manage-acrs/createacr5.png)


## <a name="edit-an-access-control-record"></a>Bir erişim denetimi kaydı Düzenle
Merhaba kullandığınız **yapılandırma** hello StorSimple cihaz Yöneticisi hizmeti dikey tooedit ACRs bölümünde.

> [!NOTE]
> Şu anda kullanımda olmayan ACRs değiştirmeniz önerilir. şu anda kullanımda olan bir birime bir ACR ilişkili tooedit, ilk hello birim çevrimdışı duruma getirmeniz gerekir.

Aşağıdaki adımları tooedit bir ACR hello gerçekleştirin.

#### <a name="tooedit-an-access-control-record"></a>tooedit bir erişim denetimi kaydı
1.  Tooyour StorSimple cihaz Yöneticisi hizmeti gidin, hello hizmet adını ve ardından içinde hello çift **yapılandırma** 'yi tıklatın **erişim denetimi kayıtları**.

    ![Tooaccess denetim kayıtları gidin](./media/storsimple-8000-manage-acrs/createacr1.png)

2. Hello tablo hello erişim denetimi kayıtları listesi,'ı tıklatın ve hello toomodify istediğiniz ACR seçin.

    ![Erişim denetimi kayıtları düzenleme](./media/storsimple-8000-manage-acrs/editacr1.png)

3. Merhaba, **düzenleme erişim denetimi kaydı** dikey penceresinde, farklı bir IQN karşılık gelen tooanother konak sağlayın.

    ![Erişim denetimi kayıtları düzenleme](./media/storsimple-8000-manage-acrs/editacr2.png)

4. **Kaydet** düğmesine tıklayın. Onayınız istendiğinde **Evet**’e tıklayın. 

    ![Erişim denetimi kayıtları düzenleme](./media/storsimple-8000-manage-acrs/editacr3.png)

5. Merhaba ACR güncelleştirildiğinde size bildirilir. Merhaba sekmeli liste tooreflect hello değişiklik de güncelleştirir.

   
## <a name="delete-an-access-control-record"></a>Bir erişim denetimi kaydını sil
Merhaba kullandığınız **yapılandırma** hello StorSimple cihaz Yöneticisi hizmeti dikey toodelete ACRs bölümünde.

> [!NOTE]
> Şu anda kullanımda olmayan ACRs silebilirsiniz. şu anda kullanımda olan bir birime bir ACR ilişkili toodelete, ilk hello birim çevrimdışı duruma getirmeniz gerekir.

Aşağıdaki adımları toodelete bir erişim denetimi kaydı hello gerçekleştirin.

#### <a name="toodelete-an-access-control-record"></a>toodelete bir erişim denetimi kaydı
1.  Tooyour StorSimple cihaz Yöneticisi hizmeti gidin, hello hizmet adını ve ardından içinde hello çift **yapılandırma** 'yi tıklatın **erişim denetimi kayıtları**.

    ![Tooaccess denetim kayıtları gidin](./media/storsimple-8000-manage-acrs/createacr1.png)

2. Hello tablo hello erişim denetimi kayıtları listesi,'ı tıklatın ve hello toodelete istediğiniz ACR seçin.

    ![Tooaccess denetim kayıtları gidin](./media/storsimple-8000-manage-acrs/deleteacr1.png)

3. Tooinvoke hello bağlam menüsü sağ tıklatıp **silmek**.

    ![Tooaccess denetim kayıtları gidin](./media/storsimple-8000-manage-acrs/deleteacr2.png)

4. Onayınız istendiğinde hello bilgileri gözden geçirin ve ardından **silmek**.

    ![Tooaccess denetim kayıtları gidin](./media/storsimple-8000-manage-acrs/deleteacr3.png)

5. Merhaba silme işlemi tamamlandığında size bildirilir. Merhaba tablo güncelleştirilmiş tooreflect hello silme listedir.

    ![Tooaccess denetim kayıtları gidin](./media/storsimple-8000-manage-acrs/deleteacr5.png)

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [StorSimple birimlerini yönetme](storsimple-8000-manage-volumes-u2.md).
* Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-8000-manager-service-administration.md).

