---
title: "aaaManage, StorSimple birim kapsayıcıları hello StorSimple 8000 serisi aygıtta | Microsoft Docs"
description: "Merhaba hizmet birim kapsayıcıları tooadd sayfasında, değiştirmek veya birim kapsayıcısı silmek Aygıt Yöneticisi'ni StorSimple nasıl kullanabileceğinizi açıklar."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 07/19/2017
ms.author: alkohli
ms.openlocfilehash: 7374d4ab9aecd6280ae1d93a29f17d12d28c9362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-storsimple-volume-containers"></a>Merhaba StorSimple cihaz Yöneticisi hizmeti toomanage StorSimple birim kapsayıcıları kullanma

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl toouse StorSimple cihaz Yöneticisi hizmeti toocreate hello ve StorSimple birim kapsayıcıları yönetmek açıklanmaktadır.

Microsoft Azure StorSimple aygıtta bir birim kapsayıcısı depolama hesabı, şifreleme ve bant genişliği tüketimi ayarları paylaşan bir veya daha fazla birimleri içerir. Bir aygıt tüm birimlerde için birden çok birim kapsayıcıları olabilir. 

Birim kapsayıcısı öznitelikleri aşağıdaki hello sahiptir:

* **Birimleri** – hello katmanlı veya hello birim kapsayıcı içinde bulunan StorSimple birimlerini'yerel olarak sabitlenmiş. 
* **Şifreleme** – her birim kapsayıcısı için tanımlanabilen bir şifreleme anahtarı. Bu anahtar StorSimple cihaz toohello buluttan gönderilen hello verileri şifrelemek için kullanılır. Askeri düzeyde AES 256 bit anahtar hello kullanıcı tarafından girilen anahtarla kullanılır. toosecure, verilerinizin her zaman bulut depolama şifrelemesini etkinleştir olan öneririz.
* **Depolama hesabı** – kullanılan toostore hello veriler Azure depolama hesabı hello. Birim kapsayıcısı içinde bulunan tüm hello birimleri bu depolama hesabını paylaşır. Varolan bir listesinden bir depolama hesabını seçin veya hello birim kapsayıcısı oluşturduğunuzda ve bu hesabın hello erişim kimlik bilgilerini belirtin yeni bir hesap oluşturun.
* **Bulut bant genişliği** – hello cihazdaki hello verileri toohello bulut gönderildiğinde hello aygıt tarafından kullanılan bant genişliği hello. Bu kapsayıcı oluşturduğunuzda, 1 MB/sn ile 1000 MB/sn arasında bir değer belirterek bant genişliği denetimini uygulayabilirsiniz. Kullanılabilir tüm bant genişliği hello aygıt tooconsume istiyorsanız, bu alan çok ayarlayın**sınırsız**. Ayrıca, oluşturmak ve bant genişliği şablonu tooallocate bant zamanlamaya göre uygulayabilirsiniz.

Merhaba aşağıdaki yordamlar nasıl toouse hello StorSimple açıklamaktadır **birim kapsayıcıları** ortak işlemleri aşağıdaki dikey toocomplete hello:

* Birim kapsayıcısı Ekle
* Birim kapsayıcısı değiştirme
* Birim kapsayıcısı Sil

## <a name="add-a-volume-container"></a>Birim kapsayıcısı Ekle
Aşağıdaki adımları tooadd birim kapsayıcısı hello gerçekleştirin.

[!INCLUDE [storsimple-8000-add-volume-container](../../includes/storsimple-8000-create-volume-container.md)]

## <a name="modify-a-volume-container"></a>Birim kapsayıcısı değiştirme
Aşağıdaki adımları toomodify birim kapsayıcısı hello gerçekleştirin.

[!INCLUDE [storsimple-8000-modify-volume-container](../../includes/storsimple-8000-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Birim kapsayıcısı Sil
Birim kapsayıcısı içindeki birimi vardır. Yalnızca kapsadığı tüm hello birimler ilk silindiğinde silinebilir. Aşağıdaki adımları toodelete birim kapsayıcısı hello gerçekleştirin.

[!INCLUDE [storsimple-8000-delete-volume-container](../../includes/storsimple-8000-delete-volume-container.md)]

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [StorSimple birimlerini yönetme](storsimple-8000-manage-volumes-u2.md). 
* Daha fazla bilgi edinmek [StorSimple Cihazınızı hello StorSimple cihaz Yöneticisi hizmeti tooadminister kullanarak](storsimple-8000-manager-service-administration.md).

