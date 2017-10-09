---
title: "aaaManage StorSimple birim kapsayıcıları | Microsoft Docs"
description: "Merhaba StorSimple hizmeti birim kapsayıcıları tooadd sayfasında, değiştirmek veya birim kapsayıcısı silmek Yöneticisi nasıl kullanabileceğinizi açıklar."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 1c64ce75-1fd3-4d3b-9304-d4dc0fc2b069
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/24/2016
ms.author: v-sharos
ms.openlocfilehash: 9b29536e0072306e53ac92bacca78a13d932c2b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomanage-storsimple-volume-containers"></a>Merhaba StorSimple Yöneticisi hizmet toomanage StorSimple birim kapsayıcıları kullanma
## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl toouse StorSimple Yöneticisi hizmet toocreate hello ve StorSimple birim kapsayıcıları yönetmek açıklanmaktadır.

Microsoft Azure StorSimple aygıtta bir birim kapsayıcısı depolama hesabı, şifreleme ve bant genişliği tüketimi ayarları paylaşan bir veya daha fazla birimleri içerir. Bir aygıt tüm birimlerde için birden çok birim kapsayıcıları olabilir. 

Birim kapsayıcısı öznitelikleri aşağıdaki hello sahiptir:

* **Birimleri** – hello katmanlı veya hello birim kapsayıcı içinde bulunan StorSimple birimlerini'yerel olarak sabitlenmiş. Birim kapsayıcısı too256 StorSimple birimleri içerebilir.
* **Şifreleme** – her birim kapsayıcısı için tanımlanabilen bir şifreleme anahtarı. Bu anahtar StorSimple cihaz toohello buluttan gönderilen hello verileri şifrelemek için kullanılır. Askeri düzeyde AES 256 bit anahtar hello kullanıcı tarafından girilen anahtarla kullanılır. toosecure, verilerinizin her zaman bulut depolama şifrelemesini etkinleştir olan öneririz.
* **Depolama hesabı** – hello bağlantılı tooyour bulut depolama hizmeti sağlayıcısıdır depolama hesabı. Birim kapsayıcısı içinde bulunan tüm hello birimleri bu depolama hesabını paylaşır. Varolan bir listesinden bir depolama hesabını seçin veya hello birim kapsayıcısı oluşturduğunuzda ve bu hesabın hello erişim kimlik bilgilerini belirtin yeni bir hesap oluşturun.
* **Bulut bant genişliği** – hello cihazdaki hello verileri toohello bulut gönderildiğinde hello aygıt tarafından kullanılan bant genişliği hello. Bu kapsayıcı tanımlarken 1 ile 1000 MB/sn arasında bir değer belirterek bir bant genişliği denetimini uygulayabilirsiniz. Kullanılabilir tüm bant genişliği hello aygıt tooconsume istiyorsanız bu alanı tooUnlimited ayarlayın. Ayrıca, oluşturmak ve bant genişliği şablonu tooallocate bant zamanlamaya göre uygulayabilirsiniz.

![Birim kapsayıcıları sayfası](./media/storsimple-manage-volume-containers/HCS_VolumeContainersPage.png)

Bu aşağıdaki yordamlarda, nasıl toouse hello StorSimple açıklanmaktadır **birim kapsayıcıları** ortak işlemleri aşağıdaki sayfayı toocomplete hello:

* Birim kapsayıcısı Ekle 
* Birim kapsayıcısı değiştirme 
* Birim kapsayıcısı Sil 

## <a name="add-a-volume-container"></a>Birim kapsayıcısı Ekle
Aşağıdaki adımları tooadd birim kapsayıcısı hello gerçekleştirin.

[!INCLUDE [storsimple-add-volume-container](../../includes/storsimple-add-volume-container.md)]

## <a name="modify-a-volume-container"></a>Birim kapsayıcısı değiştirme
Aşağıdaki adımları toomodify birim kapsayıcısı hello gerçekleştirin.

[!INCLUDE [storsimple-modify-volume-container](../../includes/storsimple-modify-volume-container.md)]

## <a name="delete-a-volume-container"></a>Birim kapsayıcısı Sil
Birim kapsayıcısı içindeki birimi vardır. Yalnızca kapsadığı tüm hello birimler ilk silindiğinde silinebilir. Aşağıdaki adımları toodelete birim kapsayıcısı hello gerçekleştirin.

[!INCLUDE [storsimple-delete-volume-container](../../includes/storsimple-delete-volume-container.md)]

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [StorSimple birimlerini yönetme](storsimple-manage-volumes.md). 
* Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

