---
title: "bir StorSimple sanal dizisinde aaaInstall güncelleştirmeleri | Microsoft Docs"
description: "Toouse hello StorSimple sanal dizinin web kullanıcı Arabirimi tooapply hello portal ve düzeltme yöntemi kullanılarak nasıl güncelleştirdiği açıklar"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a>StorSimple sanal dizinizi üzerinde güncelleştirmeleri yükle
## <a name="overview"></a>Genel Bakış
Bu makalede, StorSimple sanal dizisindeki hello yerel web kullanıcı Arabirimi aracılığıyla ve hello Klasik Azure Portalı aracılığıyla hello adımları gerekli tooinstall güncelleştirmeleri anlatılmaktadır. Tooapply yazılım güncelleştirmeleri veya düzeltmeleri tookeep StorSimple sanal dizinizi güncel gerekir. 

Bir güncelleştirme veya düzeltme yükleme, aygıt yeniden unutmayın. Verilen Hello StorSimple sanal dizinin bir tek düğümlü aygıt olduğundan, devam eden tüm g/ç kesintiye ve kapalı kalma süresi Cihazınızı karşılaştığında. 

Bir güncelleştirmeyi uygulamadan önce hello birimlerinin almak veya paylaşımlarında çevrimdışı hello ilk ana bilgisayar ve aygıt hello öneririz. Bu veri bozulması olasılığını en aza indirir.

> [!IMPORTANT]
> Güncelleştirme 0.1 veya GA yazılım sürümleri çalıştırıyorsanız, hello düzeltme hello yerel web kullanıcı Arabirimi tooinstall güncelleştirme 0.3 yöntemiyle kullanmanız gerekir. Güncelleştirme 0.2 çalıştırıyorsanız, hello Klasik Azure Portalı aracılığıyla hello güncelleştirmeleri yüklemenizi öneririz.
> 
> 

## <a name="use-hello-local-web-ui"></a>Merhaba yerel web kullanıcı arabirimini kullanın
Merhaba yerel web kullanıcı arabirimini kullanırken iki adımı vardır:

* Merhaba update veya hello düzeltmeyi yükleyin
* Merhaba güncelleştirme veya hello düzeltmeyi yükleyin

### <a name="download-hello-update-or-hello-hotfix"></a>Merhaba update veya hello düzeltmeyi yükleyin
Hello Microsoft Update Kataloğu ' adımları toodownload hello yazılım güncelleştirmesi aşağıdaki hello gerçekleştirin.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>toodownload hello güncelleştirme veya hello düzeltme
1. Internet Explorer'ı başlatın ve çok gidin[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Bu bilgisayarda Microsoft Update Kataloğu hello kullanarak ilk kez olursa **yükleme** zaman istendiğinde tooinstall hello Microsoft Update Kataloğu eklentisi.
3. Merhaba arama kutusuna hello Microsoft Update Kataloğu hello Bilgi Bankası (KB) numarasını girin hello düzeltme toodownload istiyor. Girin **3182061** Update 0.3 ve ardından **arama**.
   
    Merhaba düzeltme listesi, örneğin, göründüğünde **StorSimple sanal dizinin güncelleştirme 0.3**.
   
    ![Katalogda arama](./media/storsimple-ova-install-update-01/download1.png)
4. **Ekle**'ye tıklayın. Merhaba güncelleştirme toohello Sepeti eklenir.
5. **Sepeti Görüntüle**’ye tıklayın.
6. **İndir**’e tıklayın. Belirtin veya **Gözat** tooa yerel konum istediğiniz hello tooappear indirir. Merhaba güncelleştirmelerin yükleneceği toohello konumu belirtilen ve alt hello hello update ile aynı ad ile yerleştirilir. Merhaba klasör de hello aygıttan ulaşılabilir kopyalanan tooa ağ paylaşımı olabilir.
7. Açık hello kopyaladığınız klasörü, Microsoft Update tek başına paket dosyası görmelisiniz `WindowsTH-KB3011067-x64`. Bu, kullanılan tooinstall hello güncelleştirme veya düzeltme dosyasıdır.

### <a name="install-hello-update-or-hello-hotfix"></a>Merhaba güncelleştirme veya hello düzeltmeyi yükleyin
Önceki toohello güncelleştirme veya düzeltme yükleme, bir ağ paylaşımı üzerinden erişilebilir veya hello güncelleştirmeye sahip veya hello düzeltmeyi indirdiğiniz, ana bilgisayarda yerel olarak ya da emin olun. 

Bu yöntem tooinstall güncelleştirmeleri GA çalıştıran bir cihazda kullanmayı veya 0,1 yazılım sürümleri güncelleştirin. Bu yordamı 2 dakika toocomplete değerinden alır. Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>tooinstall hello güncelleştirme veya hello düzeltme
1. Merhaba yerel web kullanıcı Arabirimi, çok Git**Bakım** > **yazılım güncelleştirmesi**.
   
    ![cihaz güncelleştirme](./media/storsimple-ova-install-update-01/update1m.png)
2. İçinde **güncelleştirme dosya yolu**, hello güncelleştirmesi hello dosya adı girin veya düzeltme hello. Ayrıca, bir ağ paylaşımında girdiyseniz toohello güncelleştirme veya düzeltme yükleme dosyası göz atabilirsiniz. **Uygula**'ya tıklayın.
   
    ![cihaz güncelleştirme](./media/storsimple-ova-install-update-01/update2m.png)
3. Bir uyarı görüntülenir. Bir tek düğümlü aygıt hello güncelleştirme uygulanana, hello aygıt yeniden başladıktan sonra kapalı kalma süresi budur. Merhaba onay simgesine tıklayın.
   
   ![cihaz güncelleştirme](./media/storsimple-ova-install-update-01/update3m.png)
4. Merhaba güncelleştirme başlatır. Merhaba cihaz başarıyla güncelleştirildikten sonra yeniden başlatır. Merhaba yerel UI bu süre içinde erişilebilir durumda değil.
   
    ![cihaz güncelleştirme](./media/storsimple-ova-install-update-01/update5m.png)
5. Merhaba yeniden başlatma tamamlandıktan sonra toohello gerçekleştirilen **oturum** sayfası. Merhaba aygıt yazılımı güncelleştirdi, hello yerel web kullanıcı Arabirimi, tooverify Git çok**Bakım** > **yazılım güncelleştirmesi**. Görüntülenen hello yazılım sürüm olmalıdır **10.0.0.0.0.10288.0** güncelleştirme 0.3 için.
   
   > [!NOTE]
   > Biz hello yerel web kullanıcı Arabirimi biraz farklı bir yolla hello yazılım sürümleri rapor ve klasik Azure portalı hello. Örneğin, yerel web kullanıcı Arabirimi raporları'nı hello **10.0.0.0.0.10288** ve Azure Klasik portalı raporları hello **10.0.10288.0** hello için aynı sürüm. 
   > 
   > 
   
    ![cihaz güncelleştirme](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a>Merhaba Klasik Azure portalını kullanın
Güncelleştirme 0.2 çalıştırılıyorsa hello Klasik Azure Portalı aracılığıyla güncelleştirmeleri yüklemenizi öneririz. Merhaba kullanıcı tooscan Hello portal yordamı gerektirir, indirin ve ardından hello güncelleştirmeleri yükleyin. Bu yordamı yaklaşık 7 dakika toocomplete alır. Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

Merhaba sonra yükleme (% 100 İş durumu belirtildiği gibi) tamamlandığında, çok Git**cihazlar > bakım > yazılım güncelleştirmelerini**. Görüntülenen hello yazılım sürümü 10.0.10288.0 olmalıdır.

![cihaz güncelleştirme](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).

