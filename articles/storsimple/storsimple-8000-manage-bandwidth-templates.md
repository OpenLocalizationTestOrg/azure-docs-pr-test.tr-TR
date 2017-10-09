---
title: "StorSimple 8000 serisi için aaaManage bant genişliği şablonları | Microsoft Docs"
description: "Açıklar nasıl toocontrol bant genişliği kullanılmasına izin ver toomanage StorSimple bant genişliği şablonları."
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
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: ebcd1824d7bb9e4c235194c04edbfe8001a3e794
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-bandwidth-templates"></a>Merhaba StorSimple cihaz Yöneticisi hizmeti toomanage StorSimple bant genişliği şablonları kullanın.

## <a name="overview"></a>Genel Bakış

Bant genişliği şablonları birden çok gün saat zamanlamaları tootier hello verilerden hello StorSimple cihaz toohello bulut üzerinden tooconfigure ağ bant genişliği kullanımı sağlar.

Bant genişliği zamanlamaları azaltma ile şunları yapabilirsiniz:

* Özelleştirilmiş bant genişliği zamanlamaları hello iş yükü ağ kullanımları bağlı olarak belirtin.
* Yönetim merkezileştirmek ve hello zamanlamaları birçok cihaz arasında kolay ve sorunsuz bir şekilde yeniden kullanabilirsiniz.

> [!NOTE]
> Bu özellik yalnızca StorSimple fiziksel cihazlar (modeller 8100 ve 8600) için ve StorSimple bulut cihazları (modeller 8010 hem de 8020) için kullanılabilir.


## <a name="hello-bandwidth-templates-blade"></a>Merhaba bant genişliği şablonları dikey penceresi

Merhaba **bant genişliği şablonları** dikey tablo biçiminde tüm hello bant genişliği şablonları hizmetiniz için sahip ve aşağıdaki bilgilerle hello içeren:

* **Ad** – oluşturulduğunda atanan benzersiz bir ad toohello bant genişliği şablonu.
* **Zamanlama** – hello verilen bant genişliği şablonundaki zamanlamaları sayısı.
* **Tarafından kullanılan** – hello hello bant genişliği şablonları kullanarak birimlerin sayısı.

Ek bilgi toohelp bant genişliği şablonları yapılandırmak da bulabilirsiniz içinde:

* [Bant genişliği şablonları hakkında sorular ve yanıtlar](#questions-and-answers-about-bandwidth-templates)
* [Bant genişliği şablonları için en iyi yöntemler](#best-practices-for-bandwidth-templates)

## <a name="add-a-bandwidth-template"></a>Bant genişliği şablonu ekleyin

Aşağıdaki adımları toocreate yeni bant genişliği şablonu hello gerçekleştirin.

#### <a name="tooadd-a-bandwidth-template"></a>tooadd bant genişliği şablonu

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin, tıklatın **bant genişliği şablonları** ve ardından **+ Ekle bant genişliği şablonu**.

    ![Bant genişliği şablonu ekleyin + tıklayın](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp1.png)

2. Merhaba, **bant genişliği şablonu Ekle** dikey penceresinde, adımları hello:
   
    1. Bant genişliği şablonu için benzersiz bir ad belirtin.
    2. Bir bant genişliği zamanlama tanımlayın. bir zamanlama toocreate:
   
        1. Merhaba Hello aşağı açılan listeden seçin **gün** hello hafta Merhaba zamanlama için yapılandırılır. Birden fazla gün seçebilirsiniz.        
        
        2. Girin bir **başlangıç saati** içinde _ss: dd_ biçimi. Merhaba zamanlama başlar, bu olur.

        3. Girin bir **bitiş saati** içinde _ss: dd_ biçimi. Merhaba zamanlama durdurur durumdur.
      
           > [!NOTE]
           > Çakışan zamanlamaları izin verilmiyor. Merhaba başlangıç ve bitiş zamanlarını çakışan bir zamanlamada neden olacak bir hata iletisi toothat efekti görürsünüz.

        4. Merhaba belirtin **bant genişliği Hızı**. Merhaba bant genişliği megabit / saniye (Mbps) StorSimple Cihazınızı hello bulut (karşıya ve karşıdan yüklemeleri) ilgili işlemler tarafından kullanılan budur. 1 ve bu alan için 1000 arasında bir sayı girin.

            ![Bant genişliği zamanlamayı tanımlayın](./media/storsimple-8000-manage-bandwidth-templates/addbwtemp2.png)
         
            Tümü tamamlanıncaya kadar yukarıdaki adımları toodefine hello birden çok zamanlama şablonunuz için yineleyin.

        5. Tıklatın **Ekle** toostart bant genişliği şablonu oluşturma. Şablon oluşturulan hello toohello bant genişliği şablonları listesi eklenir.
      

## <a name="edit-a-bandwidth-template"></a>Bant genişliği Şablonu Düzenle

Aşağıdaki adımları tooedit bant genişliği şablonu hello gerçekleştirin.

### <a name="tooedit-a-bandwidth-template"></a>tooedit bant genişliği şablonu

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **bant genişliği şablonları**.
2. Bant genişliği şablonları Hello listesinde toodelete istediğiniz hello şablonu seçin. Sağ tıklayın ve hello bağlam menüsünden seçin **silmek**.
3. Onayınız istendiğinde tıklatın **Tamam**. Bu hello bant genişliği şablonu silmeniz gerekir. 
4. bant genişliği şablonları listesi Hello tooreflect hello silme güncelleştirir.

> [!NOTE]
> Merhaba zamanlama çakışmalar değiştirdiğiniz hello bant genişliği şablonu mevcut bir zamanlamayı ile düzenlerseniz, değişiklikler kaydedilemiyor.

## <a name="delete-a-bandwidth-template"></a>Bant genişliği Şablonu Sil

Aşağıdaki adımları toodelete bant genişliği şablonu hello gerçekleştirin.

#### <a name="toodelete-a-bandwidth-template"></a>toodelete bant genişliği şablonu

1. Tooyour StorSimple cihaz Yöneticisi hizmeti gidin ve tıklayın **bant genişliği şablonları**.
2. Bant genişliği şablonları Hello listesinde toodelete istediğiniz hello şablonu seçin. Sağ tıklayın ve Delete hello bağlam menüsünden seçin.
3. Onayınız istendiğinde tıklatın **Tamam**. Bu hello bant genişliği şablonu silmeniz gerekir.
4. bant genişliği şablonları listesi Hello tooreflect hello silme güncelleştirir.

Tüm birimlerin kullanımında Hello şablonu ise, toodelete izin verilmez. Merhaba şablon kullanımda belirten bir hata iletisi görürsünüz. Tüm hello başvuruları toohello şablonu kaldırılması gerektiğini bildiren bir hata iletisi iletişim kutusu görünür.

Merhaba erişerek tüm hello başvuruları toohello şablonunu silebilirsiniz **birim kapsayıcıları** sayfasında ve böylece başka bir şablon kullanın veya bir özel veya sınırsız bant genişliği kullanın, bu şablonu kullanan hello birim kapsayıcıları değiştirme ayar. Tüm hello başvuruları kaldırıldıktan sonra hello şablonunu silebilirsiniz.

## <a name="use-a-default-bandwidth-template"></a>Varsayılan bant genişliği şablonu kullanın

Varsayılan bant genişliği şablonu sağlanır ve birim kapsayıcıları tarafından hello bulut erişirken varsayılan tooenforce bant genişliği denetimleri tarafından kullanılır. Hello varsayılan şablonu, ayrıca kullanıcılar kendi şablonlarını oluşturmak için hazır bir başvuru olarak görev yapar. Bu varsayılan şablon Hello ayrıntılarını şunlardır:

* **Ad** – sınırsız gece ve hafta sonları
* **Zamanlama** – 8: 00 ve 17: 00 saatleri aygıt saat arasındaki 1 MB/sn bant genişliği oranını geçerlidir Pazartesi tooFriday tek bir zamanlamadan. Merhaba bant genişliği tooUnlimited hello hafta hello kalanı için ayarlanır.

Merhaba varsayılan şablonu düzenlenebilir. (düzenlenen sürümleri de dahil olmak üzere) bu şablonu Hello kullanımı izlenir.

## <a name="create-an-all-day-bandwidth-template-that-starts-at-a-specified-time"></a>Belirli bir zamanda başlatır süren bir bant genişliği şablonu oluştur

Bu yordam toocreate belirli bir zamanda başlatır ve tüm gün çalışan bir zamanlama izleyin. Merhaba örnekte hello zamanlama hello sabah içinde 09: 00'dan başlar ve sonraki sabah 09: 00 hello kadar çalıştırır. Başlangıç hello önemli toonote olduğundan ve bitiş zamanları belirli bir zamanlama için her ikisini de aynı 24 saatlik zamanlama ve birden fazla gün yayılamaz hello üzerinde yer almalıdır. Birden çok gün span bant genişliği şablonlarını tooset ihtiyacınız varsa, (Merhaba örnekte gösterildiği gibi) birden çok zamanlama toouse gerekir.

#### <a name="toocreate-an-all-day-bandwidth-template"></a>toocreate süren bir bant genişliği şablonu

1. Merhaba sabah içinde 09: 00'dan başlar ve kadar gece yarısı çalışan bir zamanlama oluşturun.
2. Başka bir zamanlama ekleyin. 09: 00 hello sabah içinde kadar Hello ikinci zamanlama toorun gece yarısına yapılandırın.
3. Merhaba bant genişliği şablonu kaydedin.

Merhaba bileşik zamanlama sonra bir zamanda başlatmak ve günlük çalıştırın.

## <a name="questions-and-answers-about-bandwidth-templates"></a>Bant genişliği şablonları hakkında sorular ve yanıtlar

**Q**. Between hello zamanlama toobandwidth denetimleri ne olur? (Bir zamanlama sona erdi ve başka bir henüz başlatılmadı.)

**A**. Böyle durumlarda, bant genişliği denetimleri işe. Bu, hello aygıt sınırsız bant genişliği veri toohello bulut katmanlandırma olduğunda kullanabileceğiniz anlamına gelir.

**Q**. Bant genişliği şablonları çevrimdışı cihazında değişiklik yapabilirsiniz?

**A**. Merhaba karşılık gelen cihaz çevrimdışı ise mümkün toomodify bant genişliği şablonları birimleri kapsayıcılarında olmaz.

**Q**. İlişkili hello birimlerinin çevrimdışı olduğunda bir birim kapsayıcısı ile ilişkili bir bant genişliği şablonu düzenleyebilirsiniz.

**A**. Birimleri çevrimdışı bir birim kapsayıcısı ile ilişkili bir bant genişliği şablonu değiştirebilirsiniz. Hiçbir veri birimlerinin çevrimdışı olduğunda hello aygıt toohello buluttan katmanlı olduğunu unutmayın.

**Q**. Varsayılan bir şablon silebilirsiniz?

**A**. Varsayılan bir şablon silebilirsiniz rağmen iyi bir fikir toodo şekilde değil. düzenlenen sürümleri de dahil olmak üzere varsayılan bir şablon Hello kullanımı izlenir. izleme verilerini hello analiz edilir ve zaman hello süresince kullanılan tooimprove hello varsayılan şablonudur.

**Q**. Bant genişliği şablonlarınızı değiştiren toobe gerektiğini nasıl belirlediğiniz?

**A**. Merhaba başlattığınızda işaretlerini toomodify hello bant genişliği şablonlar ihtiyacınız olan biri hello ağ görmesini yavaşlaması veya bir gün içinde birden çok kez boğma. Bu durumda, hello depolama ve kullanım ağ hello g/ç performans ve ağ üretilen grafikleri bakarak izleyin.

Merhaba ağ verimliliği verilerden başlangıç saati belirleyin ve hangi hello ağ sorununu oluşur birim kapsayıcıları hello. Veri Katmanlı toohello bulut yüklenirken bu ortaya çıkarsa (aygıt toocloud için g/ç performans tüm birim kapsayıcıları için bu bilgileri almak,), birim kapsayıcıları ile ilişkili toomodify hello bant genişliği şablonları gerekir.

Merhaba değiştiren sonra şablonları kullanılıyor, toomonitor hello ağ için önemli gecikmeleri yeniden gerekir. Ardından bu hala yoksa, bant genişliği şablonlarınızı toorevisit gerekir.

**Q**. Bu çakışma zamanlar cihazımı üzerinde birden çok birim kapsayıcıları varsa ne olur ancak tooeach farklı sınırlar uygulanır?

**A**. 3 birim kapsayıcıları aygıtla olduğunu varsayalım. Merhaba tamamen Bu kapsayıcılar ile ilişkilendirilmiş zamanlamaları çakışıyor. Her bu kapsayıcıların kullanılan hello bant genişliği 5, 10 ve 15 Mbps sırasıyla kısıtlamalardır. Ne zaman g/ç oluşan tüm bu kapsayıcıların aynı zamanda, hello minimum hello 3 bant genişliği sınırlarının uygulanabilir hello adresindeki: Bu durumda, bu g/ç istekleri paylaşımına giden olarak 5 MB/sn aynı sıra hello.

## <a name="best-practices-for-bandwidth-templates"></a>Bant genişliği şablonları için en iyi yöntemler

StorSimple cihazınız için bu en iyi uygulamaları izleyin:

* Bant genişliği şablonları, aygıt tooenable değişken hello ağ verimliliği hello aygıt tarafından hello günün farklı zamanlarda azaltma üzerinde yapılandırın. Yedekleme zamanlamaları ile kullanıldığında bu bant genişliği şablonları, yoğun olmayan saatlerde ek ağ bant genişliği bulut işlemleri için etkili bir şekilde yararlanabilirsiniz.
* Hello boyutuna hello dağıtım ve hello gerekli kurtarma süresi hedefi (RTO) göre belirli bir dağıtım için gereken gerçek bant hello hesaplayın.

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).

