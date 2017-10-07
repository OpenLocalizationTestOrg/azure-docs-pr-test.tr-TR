---
title: "StorSimple aaaManage erişim denetimi kayıtları | Microsoft Docs"
description: "Hangi ana bilgisayarların hello StorSimple cihazı tooa birimde bağlanabilir (ACRs) toodetermine toouse erişim denetimi kayıtları nasıl açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 2f1475d8-36a5-4cc4-84b9-adf8a310b60c
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: a1e718c2679301b34221a233557a1eaae869a94f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-access-control-records"></a>Merhaba StorSimple Yöneticisi hizmet toomanage erişim denetimi kayıtları kullanın
## <a name="overview"></a>Genel Bakış
Erişim denetimi kayıtları (ACRs) hangi ana bilgisayarların hello StorSimple cihazı tooa birimde bağlanabilir toospecify izin verin. ACRs tooa belirli birimi ayarlayın ve hello iSCSI içeren hello konakların nitelikli adlar (IQN'ler). Bir konak tooconnect tooa birim çalıştığında hello aygıt hello IQN adı ve bir eşleşmesi durumunda hello bağlantı kurulur bu birimde ACR ilişkili hello denetler. Merhaba erişim denetimi kayıtları hello bölüm **yapılandırma** sayfası ile Merhaba hello ana IQN'ler karşılık gelen tüm hello erişim denetimi kayıtları görüntüler.

Bu öğretici ortak ACR ilgili görevleri aşağıdaki hello açıklanmaktadır:

* Bir erişim denetimi kaydı ekleme 
* Bir erişim denetimi kaydı Düzenle 
* Bir erişim denetimi kaydını sil 

> [!IMPORTANT]
> * ACR tooa birim atarken bu hello birim bozuk olabilir çünkü hello birim aynı anda birden fazla kümelenmemiş ana bilgisayar tarafından erişmediğinden dikkatli olun. 
> * Bir ACR bir birimden silerken okuma-yazma kesilme hello silinmesine neden çünkü hello karşılık gelen barındıran hello birime erişimde değil emin olun.
> 
> 

## <a name="add-an-access-control-record"></a>Bir erişim denetimi kaydı ekleme
Merhaba StorSimple Yöneticisi hizmetini kullanma **yapılandırma** tooadd ACRs sayfa. Genellikle, bir birimle bir ACR ilişkilendireceğiniz.

Aşağıdaki adımları tooadd bir ACR hello gerçekleştirin.

#### <a name="tooadd-an-access-control-record"></a>tooadd bir erişim denetimi kaydı
1. Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adına çift tıklayın ve hello ardından **yapılandırma** sekmesi.
2. Merhaba altında listeleme tablo içinde **erişim denetimi kayıtları**, sağlar bir **adı** verin.
3. Merhaba IQN altında Windows ana bilgisayar adını sağlayın **iSCSI başlatıcısı adı**. tooget Merhaba, Windows Server konağının IQN'ini hello aşağıdaki:
   
   * Merhaba Microsoft iSCSI başlatıcısını Windows konağında başlatın.
   * Merhaba, **iSCSI başlatıcısı özellikleri** penceresinde hello **yapılandırma** sekmesinde seçin ve hello hello dize kopyalama **Başlatıcı adı** alan.
   * Bu dize hello Yapıştır **iSCSI başlatıcısı adı** ' hello Azure Klasik portalı de hello ACRs tabloda alan.
4. Tıklatın **kaydetmek** toosave hello ACR yeni oluşturulmuş. Merhaba tablo olacak listeleme güncelleştirilmiş tooreflect bu toplama olabilir.

## <a name="edit-an-access-control-record"></a>Bir erişim denetimi kaydı Düzenle
Merhaba kullandığınız **yapılandırma** hello Azure Klasik portalı tooedit ACRs sayfasında. 

> [!NOTE]
> Şu anda kullanımda olmayan ACRs değiştirebilirsiniz. şu anda kullanımda olan bir birime bir ACR ilişkili tooedit, ilk hello birim çevrimdışı duruma getirmeniz gerekir.
> 
> 

Aşağıdaki adımları tooedit bir ACR hello gerçekleştirin.

#### <a name="tooedit-an-access-control-record"></a>tooedit bir erişim denetimi kaydı
1. Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adına çift tıklayın ve hello ardından **yapılandırma** sekmesi.
2. Merhaba Tablo listesindeki hello erişim denetimi kayıtları, toomodify istediğiniz ACR hello gelin.
3. Yeni bir ad ve/veya IQN Merhaba ACR sağlayın.
4. Tıklatın **kaydetmek** toosave hello ACR değiştirdi. Merhaba tablo olacak listeleme güncelleştirilmiş tooreflect bu değişikliği olabilir.

## <a name="delete-an-access-control-record"></a>Bir erişim denetimi kaydını sil
Merhaba kullandığınız **yapılandırma** hello Azure Klasik portalı toodelete ACRs sayfasında. 

> [!NOTE]
> Şu anda kullanımda olmayan ACRs silebilirsiniz. şu anda kullanımda olan bir birime bir ACR ilişkili toodelete, ilk hello birim çevrimdışı duruma getirmeniz gerekir.
> 
> 

Aşağıdaki adımları toodelete bir erişim denetimi kaydı hello gerçekleştirin.

#### <a name="toodelete-an-access-control-record"></a>toodelete bir erişim denetimi kaydı
1. Merhaba hizmet giriş sayfasında hizmetinizi seçin, hello hizmet adına çift tıklayın ve hello ardından **yapılandırma** sekmesi.
2. Merhaba Tablo listesindeki hello erişim denetim kayıtlarının (ACRs), toodelete istediğiniz ACR hello gelin.
3. Sil simgesini (**x**) hello aşırı sağ sütundaki hello Seçtiğiniz ACR için görünür. Merhaba tıklatın **x** simgesi toodelete hello ACR.
4. Onayınız istendiğinde tıklatın **Evet** toocontinue hello silme işlemi ile. Merhaba sekmeli liste güncelleştirilmiş tooreflect hello silme olacaktır.

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [StorSimple birimlerini yönetme](storsimple-manage-volumes.md).
* Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

