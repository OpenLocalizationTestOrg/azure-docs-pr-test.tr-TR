---
title: "StorSimple sanal dizini aaaManage erişim denetimi kayıtları | Microsoft Docs"
description: "Hangi ana bilgisayarların hello StorSimple sanal dizinin tooa birimde bağlanabilir (ACRs) toodetermine toomanage erişim denetimi kayıtları nasıl açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: e154bb4f-faab-4d92-a593-900c3ddc9595
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 608fdf72413761ce3c9c4bf297a748489c415685
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-device-manager-toomanage-access-control-records-for-storsimple-virtual-array"></a>StorSimple sanal dizisi için Aygıt Yöneticisi'ni StorSimple toomanage erişim denetimi kayıtları

## <a name="overview"></a>Genel Bakış

Erişim denetimi kayıtları (ACRs) hangi ana bilgisayarların hello StorSimple sanal dizinin (olarak da bilinen hello StorSimple şirket içi sanal cihaz) tooa birimde bağlanabilir toospecify izin verin. ACRs tooa belirli birimi ayarlayın ve hello iSCSI içeren hello konakların nitelikli adlar (IQN'ler). Bir konak tooconnect tooa birim çalıştığında, hello aygıt hello hello IQN adının bu birimde ilişkili ACR denetler ve bir eşleşme varsa, ardından hello bağlantı kurulur. Merhaba **erişim denetimi kayıtları** dikey penceresinde hello içinde **yapılandırma** Aygıt Yöneticisi'ni hizmetinizi bölümünü hello ana IQN'ler karşılık gelen hello ile tüm hello erişim denetimi kayıtları görüntüler.

![Erişim denetimi kayıtlarını yönetme](./media/storsimple-virtual-array-manage-acrs/ova-manage-acrs.png)

Bu öğretici ortak ACR ilgili görevleri aşağıdaki hello açıklanmaktadır:

* Merhaba IQN'sini Al
* Bir erişim denetimi kaydı ekleme
* Bir erişim denetimi kaydı Düzenle
* Bir erişim denetimi kaydını sil

> [!IMPORTANT]
> 
> * ACR tooa birim atarken bu hello birim bozuk olabilir çünkü hello birim aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişmediğinden dikkatli olun.
> * Bir ACR bir birimden silerken okuma-yazma kesilme hello silinmesine neden çünkü hello karşılık gelen barındıran hello birime erişimde değil emin olun.


## <a name="get-hello-iqn"></a>Merhaba IQN'sini Al

Aşağıdaki adımları tooget hello Windows Server 2012 çalıştıran bir Windows konağının IQN'sini hello gerçekleştirin.

[!INCLUDE [storsimple-get-iqn](../../includes/storsimple-get-iqn.md)]

## <a name="add-an-acr"></a>Bir ACR ekleme

Kullandığınız **erişim denetimi kayıtları** dikey penceresinde hello içinde **yapılandırma** StorSimple cihaz Yöneticisi hizmeti tooadd ACRs bölümü. Genellikle, bir ACR tek bir birim ile ilişkilendirin.

Bir birim bir ACR ilişkilendirme hakkında daha fazla bilgi için çok Git[birim Ekle](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

> [!IMPORTANT]
> ACR tooa birim atarken bu hello birim bozuk olabilir çünkü hello birim aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişmediğinden dikkatli olun.


Aşağıdaki adımları tooadd bir ACR hello gerçekleştirin.

#### <a name="tooadd-an-acr"></a>tooadd bir ACR

1. Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adını ve ardından içinde hello çift **yapılandırma** 'yi tıklatın **erişim denetimi kayıtları**.
2. Merhaba, **erişim denetimi kayıtları** dikey penceresinde tıklatın **Ekle**.
3. Merhaba, **eklemek ACR** dikey penceresinde, aşağıdaki hello:
   
    1. ACR’nize bir **Ad** verin.
    
    2. Altında **iSCSI başlatıcısı adı**, Windows ana bilgisayarınız hello IQN adını sağlayın. tooget Merhaba, Windows Server konağının IQN'ini hello aşağıdaki:
   
    3. Merhaba Microsoft iSCSI başlatıcısını Windows konağında başlatın. Merhaba iSCSI başlatıcısı Özellikleri penceresinde hello **yapılandırma** sekmesinde seçin ve hello hello dize kopyalama **Başlatıcı adı** alan.
    Bu dize hello Yapıştır **IQN** hello alanındaki **eklemek ACR** dikey.
   
    6. Tıklatın **Ekle** tooadd hello ACR.  
   
        ![Erişim denetimi kayıtları ekleyin](./media/storsimple-virtual-array-manage-acrs/ova-add-acrs.png)
4. Sekmeli liste hello güncelleştirilmiş tooreflect bu ektir.

## <a name="edit-an-acr"></a>Bir ACR Düzenle

Merhaba kullandığınız **erişim denetimi kayıtları** dikey penceresinde hello içinde **yapılandırma** Aygıt Yöneticisi'ni hizmetinizi hello Azure portal tooedit ACRs bölümü.

> [!NOTE]
> Şu anda kullanımda bir ACR değiştirmemeniz gerekir. şu anda kullanımda olan bir birime bir ACR ilişkili tooedit, ilk hello birim çevrimdışı duruma.


Aşağıdaki adımları tooedit bir ACR hello gerçekleştirin.

#### <a name="tooedit-an-acr"></a>tooedit bir ACR

1. Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adını ve ardından içinde hello çift **yapılandırma** bölümünde **erişim denetimi kayıtları**.
2. Merhaba, **erişim denetimi kayıtları** dikey penceresinde, hello erişim denetimi kayıtları, Tablo listesini hello hello toomodify istediğiniz ACR çift tıklayın.
3. Merhaba, **düzenleme erişim denetimi kayıtları** dikey penceresinde, aşağıdaki hello:
   
    1. Merhaba IQN hello ACR sağlayın.
   
    2. Tıklatın **kaydetmek** hello dikey toosave hello üstünde hello ACR değiştirdi. Onay iletisi aşağıdaki hello bakın:
   
        ![Erişim denetimi kayıtları düzenleme](./media/storsimple-virtual-array-manage-acrs/ova-edit-acrs.png)

## <a name="delete-an-access-control-record"></a>Bir erişim denetimi kaydını sil

Merhaba kullandığınız **yapılandırma** hello Azure portal toodelete ACRs sayfasında.

> [!NOTE]
> 
> * Şu anda kullanımda bir ACR silmemelisiniz. şu anda kullanımda olan bir birime bir ACR ilişkili toodelete, ilk hello birim çevrimdışı duruma.
> * Bir ACR bir birimden silerken okuma-yazma kesilme hello silinmesine neden çünkü hello karşılık gelen barındıran hello birime erişimde değil emin olun.


Aşağıdaki adımları toodelete bir erişim denetimi kaydı hello gerçekleştirin.

#### <a name="toodelete-an-access-control-record"></a>toodelete bir erişim denetimi kaydı

1. Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adını ve ardından içinde hello çift **yapılandırma** bölümünde **erişim denetimi kayıtları**.

2. Merhaba, **erişim denetimi kayıtları** dikey penceresinde, hello erişim denetimi kayıtları, Tablo listesini hello hello toodelete istediğiniz ACR çift tıklayın.

3. Merhaba düzenleme erişim denetimi kayıtları dikey penceresinde tıklayın **silmek**.
   
    ![ACRS Sil](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs.png)

4. Onayınız istendiğinde tıklatın **silmek** toocontinue hello silme işlemi ile. Merhaba tablo güncelleştirilmiş tooreflect hello silme listedir.
   
   ![Uyarı iletisi](./media/storsimple-virtual-array-manage-acrs/ova-del-acrs-warning.png)

## <a name="next-steps"></a>Sonraki adımlar

* Daha fazla bilgi edinmek [birimleri ekleme ve ACRs yapılandırma](storsimple-virtual-array-deploy3-iscsi-setup.md#step-3-add-a-volume).

