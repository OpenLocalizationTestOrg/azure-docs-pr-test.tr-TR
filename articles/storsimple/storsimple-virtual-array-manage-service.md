---
title: "StorSimple cihaz Yöneticisi hizmeti aaaDeploy | Microsoft Docs"
description: "Nasıl toocreate ve delete hello Azure portal StorSimple Aygıt Yöneticisi'ni hizmetinde hello açıklar ve nasıl toomanage hello hizmet kayıt anahtarını açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 28499494-8c4d-4a7f-9d44-94b2b8a93c93
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: alkohli
ms.openlocfilehash: 9064053addc7b3dfcce08b47e81b38c2e0e1b559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-device-manager-service-for-storsimple-virtual-array"></a>StorSimple sanal dizini Hello StorSimple cihaz Yöneticisi hizmetini dağıtma
## <a name="overview"></a>Genel Bakış

Merhaba StorSimple cihaz Yöneticisi hizmeti Microsoft Azure üzerinde çalışır ve toomultiple StorSimple cihazları bağlanır. Merhaba hizmeti oluşturduktan sonra hello Microsoft Azure portal tarayıcıda çalışıyor toomanage hello cihazların kullanabilirsiniz. Bu, böylece yönetici yükünü en aza bir tek, merkezi konumdan bağlı toohello StorSimple Aygıt Yöneticisi'ni tüm hello cihazlar hizmet toomonitor sağlar.

Merhaba, ortak görevler, ilgili, tooa StorSimple cihaz Yöneticisi hizmeti şunlardır:

* Hizmet oluşturma
* Bir hizmeti silin
* Merhaba hizmet kayıt anahtarını alın
* Merhaba hizmet kayıt anahtarını yeniden oluşturma

Bu öğretici nasıl tooperform her birini hello önceki görevleri açıklar. Bu makalede bulunan hello yalnızca geçerli tooStorSimple sanal diziler bilgilerdir. StorSimple 8000 serisi hakkında daha fazla bilgi için çok Git[StorSimple Yöneticisi hizmet dağıtma](storsimple-manage-service.md).

## <a name="create-a-service"></a>Hizmet oluşturma

bir hizmet toocreate, toohave gerekir:

* Bir aboneliği bir kurumsal anlaşma ile
* Etkin bir Microsoft Azure depolama hesabı
* Merhaba, erişim yönetimi için kullanılan bilgileri faturalama

Merhaba hizmeti oluşturduğunuzda, toogenerate bir depolama hesabı seçebilirsiniz.

Tek bir hizmet birden çok cihazları yönetebilirsiniz. Ancak, bir aygıt birden fazla hizmet yayılamaz. Büyük bir kuruluş birden çok hizmet örnekleri toowork farklı Aboneliklerde, kuruluşlar veya bile dağıtım konumlarında olabilir.

> [!NOTE]
> StorSimple cihaz Yöneticisi hizmeti toomanage StorSimple 8000 serisi cihazlar ve StorSimple sanal diziler ayrı örnekleri gerekir.


Aşağıdaki adımları toocreate hizmet hello gerçekleştirin.

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

## <a name="delete-a-service"></a>Bir hizmeti silin

Bir hizmet silmeden önce hiçbir bağlı aygıtlar, kullandığınızdan emin olun. Merhaba hizmet kullanımdaysa hello bağlı aygıtları devre dışı bırakın. Merhaba, işlemi devre dışı bırakma hello bağlantı hello hizmeti ile Merhaba aygıt arasında sever ancak hello bulutta hello aygıt verilerini korumak.

> [!IMPORTANT]
> Hizmet silindikten sonra hello işlem geri alınamaz. Merhaba hizmeti tarafından kullanılan herhangi bir aygıt toobe ihtiyacınız olacak başka bir hizmetle kullanılabilmesi için önce Fabrika. Bu senaryoda, hello yapılandırma yanı sıra hello aygıt hello yerel veriler kaybolacak.
 

Aşağıdaki adımları toodelete hizmet hello gerçekleştirin.

#### <a name="toodelete-a-service"></a>toodelete bir hizmeti

1. Çok Git**tüm kaynakları**. StorSimple cihaz Yöneticisi hizmetiniz için arama yapın. Toodelete istediğiniz hello hizmeti seçin.
   
    ![Hizmet toodelete seçin](./media/storsimple-virtual-array-manage-service/deleteservice2.png)
2. Tooyour hizmet Pano tooensure vardır Git hiçbir aygıt bağlı toohello hizmet. Bu hizmetle kaydedilen hiçbir cihaz varsa bir başlık iletisi toohello etkisi de görürsünüz. **Sil**'e tıklayın.
   
    ![Hizmet silme](./media/storsimple-virtual-array-manage-service/deleteservice3.png)

3. Onayınız istendiğinde tıklatın **Evet** hello onay bildirim. 
   
    ![Hizmet Silmeyi Onayla](./media/storsimple-virtual-array-manage-service/deleteservice4.png)
4. Silinen hello hizmet toobe birkaç dakika sürebilir. Merhaba sonra hizmeti başarıyla, size bildirilecek silinir.
   
    ![Başarılı hizmet silme](./media/storsimple-virtual-array-manage-service/deleteservice6.png)

hizmetlerin Hello listesi yenilenecektir.

 ![Güncelleştirilmiş hizmetlerin listesi](./media/storsimple-virtual-array-manage-service/deleteservice7.png)

## <a name="get-hello-service-registration-key"></a>Merhaba hizmet kayıt anahtarını alın
Bir hizmeti başarıyla oluşturduktan sonra StorSimple cihazınızla hello hizmet tooregister gerekir. tooregister ilk StorSimple Cihazınızı hizmet kayıt anahtarını hello. tooregister ek cihazların mevcut bir StorSimple hizmeti ile Merhaba kayıt anahtarını ve (Merhaba ilk cihazda kayıt sırasında oluşturulan) hello hizmet verileri şifreleme anahtarı gerekir. Merhaba hizmet verileri şifreleme anahtarı hakkında daha fazla bilgi için bkz: [StorSimple güvenlik](storsimple-security.md). Merhaba erişerek hello kayıt anahtarını elde edebilirsiniz **anahtarları** dikey hizmetiniz için.

Aşağıdaki adımları tooget hello hizmet kayıt anahtarını hello gerçekleştirin.

#### <a name="tooget-hello-service-registration-key"></a>tooget hello hizmet kayıt anahtarı
1. Merhaba, **StorSimple Aygıt Yöneticisi'ni** dikey penceresinde çok Git**Yönetim &gt;**  **anahtarları**.
   
   ![Anahtarlar dikey penceresi](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. Merhaba, **anahtarları** hizmet kayıt anahtarını dikey penceresinde görüntülenir. Merhaba kopyalama simgesini kullanarak hello kayıt anahtarını kopyalayın. 

Merhaba hizmet kayıt anahtarı güvenli bir yerde tutun. Bu anahtar, yanı sıra hello hizmet verileri şifreleme anahtarı, bu hizmetiyle ek cihazlar tooregister gerekir. Merhaba hizmet kayıt anahtarı aldıktan sonra StorSimple arabirimi hello Windows PowerShell aracılığıyla cihazınızın tooconfigure gerekir.

## <a name="regenerate-hello-service-registration-key"></a>Merhaba hizmet kayıt anahtarını yeniden oluşturma
Gerekli tooperform anahtar döndürme veya hizmet yöneticilerinin listesini hello değişip değişmediğini varsa tooregenerate hizmet kayıt anahtarı gerekir. Başlangıç anahtarı yeniden oluşturmak zaman hello yeni anahtar yalnızca sonraki cihazları kaydetmek için kullanılır. Bu işlem tarafından zaten kayıtlı olan hello aygıtları etkilenmez.

Aşağıdaki adımları tooregenerate hizmet kayıt anahtarını hello gerçekleştirin.

#### <a name="tooregenerate-hello-service-registration-key"></a>tooregenerate hello hizmet kayıt anahtarı
1. Merhaba, **StorSimple Aygıt Yöneticisi'ni** dikey penceresinde çok Git**Yönetim &gt;**  **anahtarları**.
   
   ![Anahtarlar dikey penceresi](./media/storsimple-virtual-array-manage-service/getregkey2.png)
2. Merhaba, **anahtarları** dikey penceresinde tıklatın **yeniden**.
   
   ![Yeniden tıklatın](./media/storsimple-virtual-array-manage-service/getregkey5.png)
3. Merhaba, **üretme hizmet kayıt anahtarını** dikey penceresinde, gözden geçirme hello eylem gerekli hello zaman anahtarları yeniden oluşturuldu. Bu hizmetle kaydedilen tüm hello sonraki cihazlar hello yeni kayıt anahtarını kullanır. Tıklatın **yeniden** tooconfirm. Merhaba kayıt tamamlandıktan sonra size bildirilecek.
   
   ![Yeniden oluşturma anahtarını doğrulayın](./media/storsimple-virtual-array-manage-service/getregkey3.png)
4. Yeni bir hizmet kayıt anahtarı görüntülenir.
   
    ![Yeniden oluşturma anahtarını doğrulayın](./media/storsimple-virtual-array-manage-service/getregkey4.png)
   
   Bu anahtarı kopyalayın ve bu hizmeti ile yeni aygıtları kaydetme için kaydedin.

## <a name="next-steps"></a>Sonraki adımlar
* Nasıl çok öğrenin[başlama](storsimple-virtual-array-deploy1-portal-prep.md) bir StorSimple sanal diziye sahip.
* Nasıl çok öğrenin[StorSimple Cihazınızı yönetmek](storsimple-ova-web-ui-admin.md).

