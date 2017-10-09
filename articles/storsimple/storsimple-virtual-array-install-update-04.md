---
title: "StorSimple sanal dizisindeki aaaInstall güncelleştirmeleri | Microsoft Docs"
description: "Azure portal ve düzeltme yöntemi toouse hello StorSimple sanal dizinin web kullanıcı Arabirimi tooapply güncelleştirmeleri kullanarak nasıl hello açıklar"
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
ms.date: 02/07/2017
ms.author: alkohli
ms.openlocfilehash: 6165b305fb0d404b404cf3a11dd0ade2f2f13b2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-04-on-your-storsimple-virtual-array"></a>StorSimple sanal dizinizi üzerinde güncelleştirme 0.4 yükleyin

## <a name="overview"></a>Genel Bakış

Bu makalede, StorSimple sanal dizisindeki hello yerel web kullanıcı Arabirimi aracılığıyla ve hello Azure portal aracılığıyla hello adımları gerekli tooinstall güncelleştirme 0.4 açıklanmaktadır. Tooapply yazılım güncelleştirmeleri veya düzeltmeleri tookeep StorSimple sanal dizinizi güncel gerekir. 

Bir güncelleştirme veya düzeltme yükleme, aygıt yeniden unutmayın. Verilen Hello StorSimple sanal dizinin bir tek düğümlü aygıt olduğundan, devam eden tüm g/ç kesintiye ve kapalı kalma süresi Cihazınızı karşılaştığında. 

Bir güncelleştirmeyi uygulamadan önce hello birimlerinin almak veya paylaşımlarında çevrimdışı hello ilk ana bilgisayar ve aygıt hello öneririz. Bu veri bozulması olasılığını en aza indirir.

> [!IMPORTANT]
> Güncelleştirme 0.1 veya GA yazılım sürümleri çalıştırıyorsanız, hello düzeltme hello yerel web kullanıcı Arabirimi tooinstall güncelleştirme 0.3 yöntemiyle kullanmanız gerekir. Daha sonra öneririz veya güncelleştirme 0.2 çalıştırıyorsanız hello Azure portal aracılığıyla hello güncelleştirmeleri yükleyin.
 

## <a name="use-hello-local-web-ui"></a>Merhaba yerel web kullanıcı arabirimini kullanın

Merhaba yerel web kullanıcı arabirimini kullanırken iki adımı vardır:

* Merhaba update veya hello düzeltmeyi yükleyin
* Merhaba güncelleştirme veya hello düzeltmeyi yükleyin

### <a name="download-hello-update-or-hello-hotfix"></a>Merhaba update veya hello düzeltmeyi yükleyin

Hello Microsoft Update Kataloğu ' adımları toodownload hello yazılım güncelleştirmesi aşağıdaki hello gerçekleştirin.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>toodownload hello güncelleştirme veya hello düzeltme

1. Internet Explorer'ı başlatın ve çok gidin[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).

2. Bu bilgisayarda Microsoft Update Kataloğu hello kullanarak ilk kez olursa **yükleme** zaman istendiğinde tooinstall hello Microsoft Update Kataloğu eklentisi.

3. Merhaba arama kutusuna hello Microsoft Update Kataloğu hello Bilgi Bankası (KB) numarasını girin hello düzeltme toodownload istiyor. Girin **3216577** 0.4 güncelleştirmesi için ve ardından **arama**.
   
    Merhaba düzeltme listesi, örneğin, göründüğünde **StorSimple sanal dizinin güncelleştirme 0.4**.
   
    ![Katalogda arama](./media/storsimple-virtual-array-install-update-04/download1.png)

4. **Ekle**'ye tıklayın. Merhaba güncelleştirme toohello Sepeti eklenir.

5. **Sepeti Görüntüle**’ye tıklayın.

6. **İndir**’e tıklayın. Belirtin veya **Gözat** tooa yerel konum istediğiniz hello tooappear indirir. Merhaba güncelleştirmelerin yükleneceği toohello konumu belirtilen ve alt hello hello update ile aynı ad ile yerleştirilir. Merhaba klasör de hello aygıttan ulaşılabilir kopyalanan tooa ağ paylaşımı olabilir.

7. Açık hello kopyaladığınız klasörü, Microsoft Update tek başına paket dosyası görmelisiniz `WindowsTH-KB3011067-x64`. Bu, kullanılan tooinstall hello güncelleştirme veya düzeltme dosyasıdır.

### <a name="install-hello-update-or-hello-hotfix"></a>Merhaba güncelleştirme veya hello düzeltmeyi yükleyin

Önceki toohello güncelleştirme veya düzeltme yükleme, bir ağ paylaşımı üzerinden erişilebilir veya hello güncelleştirmeye sahip veya hello düzeltmeyi indirdiğiniz, ana bilgisayarda yerel olarak ya da emin olun. 

Bu yöntem tooinstall güncelleştirmeleri GA çalıştıran bir cihazda kullanmayı veya 0,1 yazılım sürümleri güncelleştirin. Bu yordamı 2 dakika toocomplete değerinden alır. Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>tooinstall hello güncelleştirme veya hello düzeltme

1. Merhaba yerel web kullanıcı Arabirimi, çok Git**Bakım** > **yazılım güncelleştirmesi**.
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update1m.png)

2. İçinde **güncelleştirme dosya yolu**, hello güncelleştirmesi hello dosya adı girin veya düzeltme hello. Ayrıca, bir ağ paylaşımında girdiyseniz toohello güncelleştirme veya düzeltme yükleme dosyası göz atabilirsiniz. **Uygula**'ya tıklayın.
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update2m.png)

3. Bir uyarı görüntülenir. Bir tek düğümlü aygıt hello güncelleştirme uygulanana, hello aygıt yeniden başladıktan sonra kapalı kalma süresi budur. Merhaba onay simgesine tıklayın.
   
   ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update3m.png)

4. Merhaba güncelleştirme başlatır. Merhaba cihaz başarıyla güncelleştirildikten sonra yeniden başlatır. Merhaba yerel UI bu süre içinde erişilebilir durumda değil.
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update5m.png)

5. Merhaba yeniden başlatma tamamlandıktan sonra toohello gerçekleştirilen **oturum** sayfası. Merhaba aygıt yazılımı güncelleştirdi, hello yerel web kullanıcı Arabirimi, tooverify Git çok**Bakım** > **yazılım güncelleştirmesi**. Görüntülenen hello yazılım sürüm olmalıdır **10.0.0.0.0.10289.0** 0.4 güncelleştirmesi.
   
   > [!NOTE]
   > Biz hello yerel web kullanıcı Arabirimi biraz farklı bir yolla hello yazılım sürümleri rapor ve Azure portal hello. Örneğin, yerel web kullanıcı Arabirimi raporları'nı hello **10.0.0.0.0.10289** ve Azure portal raporları hello **10.0.10289.0** hello için aynı sürüm.
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-hello-azure-portal"></a>Hello Azure portalını kullanın

Güncelleştirme 0.2 ve sonraki sürümleri çalışıyorsa hello Azure portal aracılığıyla güncelleştirmeleri yüklemenizi öneririz. Merhaba kullanıcı tooscan Hello portal yordamı gerektirir, indirin ve ardından hello güncelleştirmeleri yükleyin. Bu yordamı yaklaşık 7 dakika toocomplete alır. Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

Merhaba sonra yükleme (olarak belirttiği % 100 İş durumu), tam gidin tooyour StorSimple cihaz Yöneticisi hizmeti değildir. Seçin **aygıtları** seçin ve tooupdate aygıtlar bağlı toothis hizmeti hello listesinden istediğiniz hello aygıtı'ı tıklatın. Merhaba, **ayarları** dikey penceresinde çok Git**Yönet** bölümünde ve seçin **aygıt güncelleştirmeleri**. Görüntülenen hello yazılım sürüm olmalıdır **10.0.10289.0**.


## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).

