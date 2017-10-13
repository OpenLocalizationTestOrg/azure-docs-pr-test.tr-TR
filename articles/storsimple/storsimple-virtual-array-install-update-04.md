---
title: "StorSimple sanal dizisinde güncelleştirmeleri yükle | Microsoft Docs"
description: "StorSimple sanal dizinin web kullanıcı Arabirimi Azure portal ve düzeltme yöntemini kullanarak güncelleştirmeleri uygulamak için nasıl kullanılacağını açıklar"
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
ms.openlocfilehash: 3fb246b1515e7a637e6cff6499bf324c3f80dd45
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-04-on-your-storsimple-virtual-array"></a>StorSimple sanal dizinizi üzerinde güncelleştirme 0.4 yükleyin

## <a name="overview"></a>Genel Bakış

Bu makalede, yerel web kullanıcı Arabirimi aracılığıyla ve Azure portalı üzerinden, StorSimple sanal dizisindeki 0.4 güncelleştirmeyi yüklemek için gereken adımlar açıklanır. Yazılım güncelleştirmelerini veya düzeltmeleri StorSimple sanal dizinizi güncel tutmak için uygulamanız gerekir. 

Bir güncelleştirme veya düzeltme yükleme, aygıt yeniden unutmayın. Bir tek düğümlü cihaz StorSimple sanal dizinin olması koşuluyla, devam eden tüm g/ç kesintiye ve kapalı kalma süresi Cihazınızı karşılaştığında. 

Bir güncelleştirmeyi uygulamadan önce birimler veya paylaşımlar çevrimdışı konakta ilk almanızı öneririz ve ardından cihaz. Bu veri bozulması olasılığını en aza indirir.

> [!IMPORTANT]
> Güncelleştirme 0.1 veya GA yazılım sürümleri çalıştırıyorsanız, update 0.3 yüklemek için yerel web kullanıcı Arabirimi aracılığıyla düzeltme yöntemini kullanmanız gerekir. Daha sonra öneririz veya güncelleştirme 0.2 çalıştırıyorsanız Azure Portalı aracılığıyla güncelleştirmeleri yükleyin.
 

## <a name="use-the-local-web-ui"></a>Yerel web kullanıcı arabirimini kullanın

Yerel web kullanıcı arabirimini kullanırken iki adımı vardır:

* Güncelleştirmeyi veya düzeltmeyi indirin
* Güncelleştirmeyi veya düzeltmeyi yükleyin

### <a name="download-the-update-or-the-hotfix"></a>Güncelleştirmeyi veya düzeltmeyi indirin

Microsoft Update Kataloğu'ndan yazılım güncelleştirmesi indirmek için aşağıdaki adımları uygulayın.

#### <a name="to-download-the-update-or-the-hotfix"></a>Güncelleştirmeyi veya düzeltmeyi indirmek için

1. Internet Explorer'ı başlatın ve [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com) adresine gidin.

2. Microsoft Update Kataloğu’nu bu bilgisayarda ilk kez kullanıyorsanız, sorulduğunda **Yükle**’ye tıklayarak Microsoft Update Kataloğu eklentisini yükleyin.

3. Microsoft Update Kataloğu arama kutusuna, yüklemek istediğiniz düzeltme Bilgi Bankası (KB) sayısını girin. Girin **3216577** 0.4 güncelleştirmesi için ve ardından **arama**.
   
    Düzeltme listesi göründüğünde, örneğin, **StorSimple sanal dizinin güncelleştirme 0.4**.
   
    ![Katalogda arama](./media/storsimple-virtual-array-install-update-04/download1.png)

4. **Ekle**'ye tıklayın. Güncelleştirme sepete eklenir.

5. **Sepeti Görüntüle**’ye tıklayın.

6. **İndir**’e tıklayın. İndirilen öğelerin görünmesini istediğiniz yerel konumu belirtin veya **Gözat** seçeneğiyle konumu bulun. Güncelleştirmeler belirtilen konuma indirilir ve güncelleştirme ile aynı adı taşıyan alt klasöre yerleştirilir. Klasör, cihazdan erişilebilen bir ağ paylaşımına da kopyalanabilir.

7. Kopyalanan klasörünü açın, bir Microsoft Update tek başına paket dosyası görmelisiniz `WindowsTH-KB3011067-x64`. Bu dosya, güncelleştirme veya düzeltme yüklemek için kullanılır.

### <a name="install-the-update-or-the-hotfix"></a>Güncelleştirmeyi veya düzeltmeyi yükleyin

Güncelleştirme veya düzeltme yükleme önce bir ağ paylaşımı üzerinden erişilebilir veya güncelleştirmeye sahip veya ana bilgisayarınız yerel olarak ya da düzeltmeyi indirdiğiniz olduğundan emin olun. 

GA çalıştıran bir cihazda güncelleştirmeleri yüklemek veya 0,1 yazılım sürümleri güncelleştirmek için bu yöntemi kullanın. Bu yordamı tamamlamak için değerinden 2 dakika sürer. Güncelleştirme veya düzeltme yüklemek için aşağıdaki adımları gerçekleştirin.

#### <a name="to-install-the-update-or-the-hotfix"></a>Güncelleştirme veya düzeltme yüklemek için

1. Yerel web kullanıcı Arabirimi, Git **Bakım** > **yazılım güncelleştirmesi**.
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update1m.png)

2. İçinde **güncelleştirme dosya yolu**, güncelleştirme veya düzeltme için dosya adı girin. Ayrıca, bir ağ paylaşımında girdiyseniz güncelleştirme veya düzeltme yükleme dosyasına göz atabilirsiniz. **Uygula**'ya tıklayın.
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update2m.png)

3. Bir uyarı görüntülenir. Bir tek düğümlü aygıt güncelleştirme uygulanana, aygıt yeniden başladıktan sonra kapalı kalma süresi budur. Onay simgesine tıklayın.
   
   ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update3m.png)

4. Güncelleştirme başlatır. Cihaz başarıyla güncelleştirildikten sonra yeniden başlatır. Yerel kullanıcı arabirimini bu süre içinde erişilebilir durumda değil.
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update5m.png)

5. Yeniden başlatma tamamlandıktan sonra gittiğiniz **oturum** sayfası. Aygıt yazılımı, yerel web kullanıcı Arabirimi, güncelleştirilmiş olduğunu doğrulamak için Git **Bakım** > **yazılım güncelleştirmesi**. Görüntülenen yazılım sürümü olmalıdır **10.0.0.0.0.10289.0** 0.4 güncelleştirmesi.
   
   > [!NOTE]
   > Yazılım sürümlerini yerel web kullanıcı Arabirimi biraz farklı bir şekilde hem de Azure portalında bildirin. Örneğin, yerel web kullanıcı Arabirimi raporları **10.0.0.0.0.10289** ve Azure portal raporları **10.0.10289.0** aynı sürüm için.
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update/update6m.png)

## <a name="use-the-azure-portal"></a>Azure portalı kullanma

Güncelleştirme 0.2 ve sonraki sürümleri çalışıyorsa, Azure portal aracılığıyla güncelleştirmeleri yüklemenizi öneririz. Portal yordamı tarama, indirme ve güncelleştirmeleri yüklemek kullanıcının gerektirir. Bu yordamı tamamlamak için yaklaşık 7 dakika sürer. Güncelleştirme veya düzeltme yüklemek için aşağıdaki adımları gerçekleştirin.

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

(Olarak % 100 İş durumu tarafından gösterilen) yükleme tamamlandıktan sonra StorSimple cihaz Yöneticisi hizmetinize gidin. Seçin **aygıtları** seçin ve bu hizmete bağlı aygıtlar listesinde güncelleştirmek istediğiniz cihaza tıklayın. İçinde **ayarları** dikey penceresinde, Git **Yönet** bölümünde ve seçin **aygıt güncelleştirmeleri**. Görüntülenen yazılım sürümü olmalıdır **10.0.10289.0**.


## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).

