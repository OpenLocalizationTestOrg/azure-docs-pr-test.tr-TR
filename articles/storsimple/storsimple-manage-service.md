---
title: "aaaDeploy hello StorSimple Yöneticisi hizmeti | Microsoft Docs"
description: "Merhaba Klasik Azure portalı, StorSimple Yöneticisi hizmeti toocreate ve delete nasıl hello açıklar ve nasıl toomanage hello hizmet kayıt anahtarını açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: bc1d5650-275c-42ed-bc77-cdb596f85943
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/14/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f49b647d91b03bb89ebd0e5cce196e50e3c00296
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-storsimple-manager-service-in-hello-azure-classic-portal"></a>Merhaba Klasik Azure portalı Hello StorSimple Yöneticisi hizmeti dağıtma

## <a name="overview"></a>Genel Bakış
Merhaba StorSimple Yöneticisi hizmeti Microsoft Azure üzerinde çalışır ve toomultiple StorSimple cihazları bağlanır. Merhaba hizmeti oluşturduktan sonra hello Microsoft Azure Klasik portalı bir tarayıcıda çalışan toomanage hello cihazların kullanabilirsiniz. Bu, böylece yönetici yükünü en aza bir tek, merkezi konumdan bağlı toohello StorSimple Yöneticisi tüm hello cihazlar hizmet toomonitor sağlar.

Merhaba StorSimple Yöneticisi giriş sayfası, StorSimple depolama aygıtları toomanage kullanabileceğiniz tüm hello StorSimple Yöneticisi hizmetleri listeler. Her bir StorSimple Yöneticisi hizmeti için aşağıdaki bilgilerle hello hello StorSimple Yöneticisi sayfasında sunulur:

* **Ad** – oluşturulduğunda tooyour StorSimple Yöneticisi hizmeti atandı hello adı. **Merhaba hizmet adı Hello hizmeti oluşturulduktan sonra değiştirilemez. Bu, aynı zamanda cihazları, birimler, birim kapsayıcıları ve hello Klasik Azure portalında yeniden adlandırılamaz yedekleme ilkeleri gibi diğer varlıklar için de geçerlidir.**
* **Durum** – hello olabilir hello hizmetinin durumunu **etkin**, **oluşturma**, veya **çevrimiçi**.
* **Konum** – hello hello StorSimple cihaz dağıtılacak coğrafi konum.
* **Abonelik** – hello hizmetiniz ile ilişkili abonelik faturalama.

Merhaba StorSimple Yöneticisi sayfası gerçekleştirilebilir hello ortak görevler şunlardır:

* Hizmet oluşturma
* Bir hizmeti silin
* Merhaba hizmet kayıt anahtarını alın
* Merhaba hizmet kayıt anahtarını yeniden oluşturma

Bu öğretici açıklar nasıl tooperform her bu görevlerin.

## <a name="create-a-service"></a>Hizmet oluşturma
Kullanım hello **hızlı Oluştur** StorSimple Cihazınızı toodeploy istiyorsanız toocreate bir StorSimple Yöneticisi hizmeti seçeneği. bir hizmet toocreate, toohave gerekir:

* Bir aboneliği bir kurumsal anlaşma ile
* Etkin bir Microsoft Azure depolama hesabı
* Merhaba, erişim yönetimi için kullanılan bilgileri faturalama

Merhaba hizmeti oluşturduğunuzda, toogenerate varsayılan depolama hesabı seçebilirsiniz.

Tek bir hizmet birden çok cihazları yönetebilirsiniz. Ancak, bir aygıt birden fazla hizmet yayılamaz. Büyük bir kuruluş birden çok hizmet örnekleri toowork farklı Aboneliklerde, kuruluşlar veya bile dağıtım konumlarında olabilir. StorSimple Yöneticisi hizmet toomanage StorSimple 8000 serisi cihazlar ve StorSimple sanal diziler örnekleri ayrı unutmayın.

> [!IMPORTANT] 
> Oluşturulan kullanılmayan hizmete (aygıt gerçekleştirilen Bu kaynakta işlemler) varsa, önceki tooAugust 2016, Azure portalından veya Klasik Azure portalı yönetilemez. Hello Azure portalında yeni bir hizmet oluşturmanızı öneririz.

Aşağıdaki adımları toocreate hizmet hello gerçekleştirin.

[!INCLUDE [storsimple-create-new-service](../../includes/storsimple-create-new-service.md)]

## <a name="delete-a-service"></a>Bir hizmeti silin
Bir hizmet silmeden önce hiçbir bağlı aygıtlar, kullandığınızdan emin olun. Merhaba hizmet kullanımdaysa hello bağlı aygıtları devre dışı bırakın. Merhaba, işlemi devre dışı bırakma hello bağlantı hello hizmeti ile Merhaba aygıt arasında sever ancak hello bulutta hello aygıt verilerini korumak.

> [!IMPORTANT] 
> Hizmet silindikten sonra hello işlem geri alınamaz. Merhaba hizmeti tarafından kullanılan herhangi bir aygıt toobe ihtiyacınız olacak başka bir hizmetle kullanılabilmesi için önce Fabrika. Bu senaryoda, hello yapılandırma yanı sıra hello aygıt hello yerel veriler kaybolacak.

Aşağıdaki adımları toodelete hizmet hello gerçekleştirin.

### <a name="toodelete-a-service"></a>toodelete bir hizmeti
1. Merhaba üzerinde **StorSimple Yöneticisi hizmeti** sayfası, select hello hizmet toodelete istiyor.
2. Tıklatın **silmek** hello sayfanın hello sonundaki.
3. Tıklatın **Evet** hello onay bildirim. Silinen hello hizmet toobe birkaç dakika sürebilir.

## <a name="get-hello-service-registration-key"></a>Merhaba hizmet kayıt anahtarını alın
Bir hizmeti başarıyla oluşturduktan sonra StorSimple cihazınızla hello hizmet tooregister gerekir. tooregister ilk StorSimple Cihazınızı hizmet kayıt anahtarını hello. tooregister ek cihazların mevcut bir StorSimple hizmeti ile Merhaba kayıt anahtarını ve (Merhaba ilk cihazda kayıt sırasında oluşturulan) hello hizmet verileri şifreleme anahtarı gerekir. Merhaba hizmet verileri şifreleme anahtarı hakkında daha fazla bilgi için bkz: [StorSimple güvenlik](storsimple-security.md). Erişerek hello kayıt anahtarını elde edebilirsiniz **kayıt anahtarı** hello üzerinde **Hizmetleri** sayfası.

Aşağıdaki adımları tooget hello hizmet kayıt anahtarını hello gerçekleştirin.

[!INCLUDE [storsimple-get-service-registration-key](../../includes/storsimple-get-service-registration-key.md)]

Merhaba hizmet kayıt anahtarı güvenli bir yerde tutun. Bu anahtar, yanı sıra hello hizmet verileri şifreleme anahtarı, bu hizmetiyle ek cihazlar tooregister gerekir. Merhaba hizmet kayıt anahtarı aldıktan sonra StorSimple arabirimi hello Windows PowerShell aracılığıyla cihazınızın tooconfigure gerekir.

Ayrıntılar için toouse bu kayıt anahtarı, bkz: [adım 3: yapılandırmak ve storsimple için Windows PowerShell üzerinden hello cihazı](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple).

## <a name="regenerate-hello-service-registration-key"></a>Merhaba hizmet kayıt anahtarını yeniden oluşturma
Gerekli tooperform anahtar döndürme veya hizmet yöneticilerinin listesini hello değişip değişmediğini varsa tooregenerate hizmet kayıt anahtarı gerekir. Başlangıç anahtarı yeniden oluşturmak zaman hello yeni anahtar yalnızca sonraki cihazları kaydetmek için kullanılır. Bu işlem tarafından zaten kayıtlı olan hello aygıtları etkilenmez.

Aşağıdaki adımları tooregenerate hizmet kayıt anahtarını hello gerçekleştirin.

### <a name="tooregenerate-hello-service-registration-key"></a>tooregenerate hello hizmet kayıt anahtarı
1. Merhaba üzerinde **StorSimple Yöneticisi hizmeti** sayfasında, **kayıt anahtarı**.
2. Merhaba, **hizmet kayıt anahtarını** iletişim kutusu, tıklatın **yeniden**.
3. Bir onay iletisi görürsünüz. Tıklatın **Tamam** toocontinue ile Merhaba yeniden oluşturma.
4. Yeni bir hizmet kayıt anahtarı görüntülenir.
5. Bu anahtarı kopyalayın ve bu hizmeti ile yeni aygıtları kaydetme için kaydedin.
6. Merhaba onay simgesine tıklayın ![Onay simgesi](./media/storsimple-manage-service/HCS_CheckIcon.png) tooclose bu iletişim kutusu.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba hakkında daha fazla bilgi [StorSimple dağıtım işlemi](storsimple-deployment-walkthrough-u2.md).
* Daha fazla bilgi edinmek [StorSimple depolama hesabınızı yönetme](storsimple-manage-storage-accounts.md).
* Hakkında daha fazla çok bilgi[kullanım StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).
