---
title: "aaaInstall güncelleştirme 0,6 StorSimple sanal dizisindeki | Microsoft Docs"
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
ms.date: 05/18/2017
ms.author: alkohli
ms.openlocfilehash: 2ccd1b5fc1957c35ebec35aa947d331b3ff05464
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-06-on-your-storsimple-virtual-array"></a>StorSimple sanal dizinizi üzerinde güncelleştirme 0,6 yükleyin

## <a name="overview"></a>Genel Bakış

Bu makalede, StorSimple sanal dizisindeki hello yerel web kullanıcı Arabirimi aracılığıyla ve hello Azure portal aracılığıyla hello adımları gerekli tooinstall güncelleştirme 0,6 açıklanmaktadır. StorSimple sanal dizinizi güncel hello yazılım güncelleştirmeleri veya düzeltmeleri tookeep uygulayın.

Bir güncelleştirmeyi uygulamadan önce hello birimlerinin almak veya paylaşımlarında çevrimdışı hello ilk ana bilgisayar ve aygıt hello öneririz. Bu veri bozulması olasılığını en aza indirir. Merhaba birimler veya paylaşımlar çevrimdışı olduktan sonra aynı zamanda el ile Merhaba aygıtına yedekleme almalıdır.

> [!IMPORTANT]
> - Güncelleştirme 0,6 karşılık gelen çok**10.0.10293.0** Cihazınızda yazılımı sürümü. Bu güncelleştirmede yenilikler hakkında daha fazla bilgi için çok gidin[0,6 güncelleştirmesi sürüm notları](storsimple-virtual-array-update-06-release-notes.md).
>
> - Daha sonra öneririz veya güncelleştirme 0.2 çalıştırıyorsanız hello Azure portal aracılığıyla hello güncelleştirmeleri yükleyin. Güncelleştirme 0.1 veya GA yazılım sürümleri çalıştırıyorsanız, hello düzeltme hello yerel web kullanıcı Arabirimi tooinstall güncelleştirme 0,6 yöntemiyle kullanmanız gerekir.
>
> - Bir güncelleştirme veya düzeltme yükleme, aygıt yeniden unutmayın. Verilen Hello StorSimple sanal dizinin bir tek düğümlü aygıt olduğundan, devam eden tüm g/ç kesintiye ve kapalı kalma süresi Cihazınızı karşılaştığında.

## <a name="use-hello-azure-portal"></a>Hello Azure portalını kullanın

Güncelleştirme 0.2 ve sonraki sürümleri çalışıyorsa hello Azure portal aracılığıyla güncelleştirmeleri yüklemenizi öneririz. Merhaba kullanıcı tooscan Hello portal yordamı gerektirir, indirin ve ardından hello güncelleştirmeleri yükleyin. Bu yordamı yaklaşık 7 dakika toocomplete alır. Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

Merhaba sonra tam, Git tooyour StorSimple cihaz Yöneticisi hizmeti bir yüklemedir. Seçin **aygıtları** seçin ve güncelleştirdiğiniz hello cihaz seçeneğine tıklayın. Çok Git**ayarlar > Yönet > aygıt güncelleştirmeleri**. Görüntülenen hello yazılım sürüm olmalıdır **10.0.10293.0**.

## <a name="use-hello-local-web-ui"></a>Merhaba yerel web kullanıcı arabirimini kullanın

Merhaba yerel web kullanıcı arabirimini kullanırken iki adımı vardır:

* Merhaba update veya hello düzeltmeyi yükleyin
* Merhaba güncelleştirme veya hello düzeltmeyi yükleyin

### <a name="download-hello-update-or-hello-hotfix"></a>Merhaba update veya hello düzeltmeyi yükleyin

Hello Microsoft Update Kataloğu ' adımları toodownload hello yazılım güncelleştirmesi aşağıdaki hello gerçekleştirin.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>toodownload hello güncelleştirme veya hello düzeltme

1. Internet Explorer'ı başlatın ve çok gidin[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).

2. Merhaba Microsoft Update Kataloğu hello için bu bilgisayarda ilk kez kullanıyorsanız **yükleme** zaman istendiğinde tooinstall hello Microsoft Update Kataloğu eklentisi.

3. Merhaba arama kutusuna hello Microsoft Update Kataloğu hello Bilgi Bankası (KB) numarasını girin hello düzeltme toodownload istiyor. Girin **4023268** 0,6 güncelleştirmesi için ve ardından **arama**.
   
    Merhaba düzeltme listesi, örneğin, göründüğünde **StorSimple sanal dizinin güncelleştirme 0,6**.
   
    ![Katalogda arama](./media/storsimple-virtual-array-install-update-06/download1.png)

4. **İndir**’e tıklayın.

5. Beş dosyaları toodownload görmeniz gerekir. Her bu dosyaları tooa klasörünün indirin. Merhaba klasör de hello aygıttan ulaşılabilir kopyalanan tooa ağ paylaşımı olabilir.

6. Merhaba dosyalarının bulunduğu hello klasörünü açın.
    ![Merhaba paket dosyaları](./media/storsimple-virtual-array-install-update-06/update06folder.png)

    Görürsünüz:
    -  Microsoft Update tek başına paket dosyası `WindowsTH-KB3011067-x64`. Bu dosya kullanılan tooupdate hello aygıt yazılımdır.
    - Geneva İzleme Aracısı paket dosyası `GenevaMonitoringAgentPackageInstaller`. Kullanılan tooupdate hello izleme ve Tanılama Hizmeti (MDS) aracısı dosyasıdır. Merhaba cab dosyasını çift tıklatın. A _.msi_ görüntülenir. Select hello dosyasını sağ tıklatın ve ardından **ayıklamak** hello dosya. Merhaba kullandığınız _.msi_ dosya tooupdate hello Aracısı.

        ![MDS aracı güncelleştirme dosyasını ayıklayın](./media/storsimple-virtual-array-install-update-06/extract-geneva-monitoring-agent-installer.png)

        > [!IMPORTANT]
        > StorSimple güncelleştirme 0,5 (0.0.10293.0) çalıştırıyorsanız, tooupdate hello MDS Aracısı gerekmez.

    - Kritik Windows Güvenlik güncelleştirmeleri içeren üç dosyaları `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, ve `windows8.1-kb4019213-x64`.


### <a name="install-hello-update-or-hello-hotfix"></a>Merhaba güncelleştirme veya hello düzeltmeyi yükleyin

Önceki toohello güncelleştirme veya düzeltme yükleme, bir ağ paylaşımı üzerinden erişilebilir veya hello güncelleştirmeye sahip veya hello düzeltmeyi indirdiğiniz, ana bilgisayarda yerel olarak ya da emin olun.

Bu yöntem tooinstall güncelleştirmeleri GA çalıştıran bir cihazda kullanmayı veya 0,1 yazılım sürümleri güncelleştirin. Bu yordam, yaklaşık olarak 12 dakika toocomplete alır. Hello aşağıdaki gerçekleştirme adımları tooinstall hello güncelleştirme veya düzeltme.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>tooinstall hello güncelleştirme veya hello düzeltme

1. Merhaba yerel web kullanıcı Arabirimi, çok Git**Bakım** > **yazılım güncelleştirmesi**. Çalıştırmakta olduğunuz hello yazılım sürümü not edin. Çalıştırıyorsanız, **10.0.10290.0**, adım 6 tooupdate hello MDS Aracısı gerekli değildir.
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. İçinde **güncelleştirme dosya yolu**, hello güncelleştirmesi hello dosya adı girin veya düzeltme hello. Ayrıca, bir ağ paylaşımında girdiyseniz toohello güncelleştirme veya düzeltme yükleme dosyası göz atabilirsiniz. **Uygula**'ya tıklayın.
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. Bir uyarı görüntülenir. Hello sanal bir tek düğümlü aygıt hello güncelleştirme uygulanana, hello aygıt yeniden başladıktan sonra kapalı kalma süresi dizisidir. Merhaba onay simgesine tıklayın.
   
   ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. Merhaba güncelleştirme başlatır. Merhaba cihaz başarıyla güncelleştirildikten sonra yeniden başlatır. Merhaba yerel UI bu süre içinde erişilebilir durumda değil.
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. Merhaba yeniden başlatma tamamlandıktan sonra toohello gerçekleştirilen **oturum** sayfası. Merhaba aygıt yazılımı güncelleştirdi, hello yerel web kullanıcı Arabirimi, tooverify Git çok**Bakım** > **yazılım güncelleştirmesi**. Görüntülenen hello yazılım sürüm olmalıdır **10.0.0.0.0.10293** 0,6 güncelleştirmesi.
   
   > [!NOTE]
   > Biz hello yerel web kullanıcı Arabirimi biraz farklı bir yolla hello yazılım sürümleri rapor ve Azure portal hello. Örneğin, yerel web kullanıcı Arabirimi raporları'nı hello **10.0.0.0.0.10293** ve Azure portal raporları hello **10.0.10293.0** hello için aynı sürüm.
   
    ![cihaz güncelleştirme](./media/storsimple-virtual-array-install-update-06/update6m.png)

6. StorSimple sanal dizinin güncelleştirme 0,5 çalışıyormuş bu adımı atla (**10.0.10290.0**) bu güncelleştirmeyi uygulamadan önce. Tooupdate başlamadan önce 1. adımda not hello yazılım sürümü yaptığınız. Güncelleştirme 0,5 çalışıyormuş MDS aracı zaten güncel.

    Bir yazılım sürüm önceki tooUpdate 0,5 çalıştırıyorsanız, hello sonraki adımda, tooupdate hello MDS aracısıdır. Merhaba, **yazılım güncelleştirmesi** sayfasında, Git toohello **güncelleştirme dosya yolu** ve toohello Gözat `GenevaMonitoringAgentPackageInstaller.msi` dosya. 2-4 arası adımları yineleyin. Merhaba sanal dizinin yeniden başlatıldıktan sonra hello yerel web kullanıcı Arabirimi ile oturum açın.

7. 2-4 tooinstall hello Windows güvenlik düzeltmelerini dosyalarını kullanarak adımı yineleyin `windows8.1-kb4012213-x64`,`windows8.1-kb3205400-x64`, ve `windows8.1-kb4019213-x64`. Merhaba sanal dizinin her yüklendikten sonra yeniden başlatılır ve hello yerel web kullanıcı Arabirimi toosign gerekir.

## <a name="next-steps"></a>Sonraki adımlar

Daha fazla bilgi edinmek [StorSimple sanal dizinizi yönetme](storsimple-ova-web-ui-admin.md).

