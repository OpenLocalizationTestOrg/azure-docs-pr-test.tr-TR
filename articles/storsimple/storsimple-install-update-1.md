---
title: "StorSimple Cihazınızda aaaInstall güncelleştirme 1.2 | Microsoft Docs"
description: "Açıklar nasıl tooinstall StorSimple 8000 serisi güncelleştirme 1.2, StorSimple 8000 serisi Cihazınızda."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 7a513923-eb77-4078-b0ab-f8e90183796a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0a7601dc0b1ce60eb854227243ecb02d6fb2c678
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-12-on-your-storsimple-8000-series-device"></a>StorSimple 8000 serisi aygıtınızda güncelleştirme 1.2 yükleme
## <a name="overview"></a>Genel Bakış
Bu öğretici, bir yazılım sürüm önceki tooUpdate 1 çalıştıran bir StorSimple cihazda 1.2 tooinstall güncelleştirme nasıl açıklanmaktadır. Başlangıç Öğreticisi hello StorSimple cihazı veri 0 dışında bir ağ arabiriminde bir ağ geçidi yapılandırıldığında hello güncelleştirmesi gerekli hello ek adımlar da kapsar.

Güncelleştirme 1.2 cihaz yazılım güncelleştirmeleri, LSI sürücü güncelleştirmelerini ve disk Bellenim güncelleştirmeleri içerir. Merhaba yazılım LSI sürücü güncelleştirmelerini benzer güncelleştirmeler ve hello Klasik Azure portalı uygulanabilir. Merhaba disk Bellenim güncelleştirmeleri kesintiye uğratan güncelleştirmelerin ve yalnızca hello cihazın hello Windows PowerShell arabirimi uygulanabilir.

Cihazınızı hangi sürümüne bağlı olarak çalışan, güncelleştirme 1.2 uygulanmış olmadığını belirleyebilirsiniz. Cihazınızı hello yazılımı sürümü toohello giderek denetleyebilirsiniz **Hızlı Bakış** Cihazınızı bölümünü **Pano**.

</br>

| Yazılım sürüm çalıştırılıyorsa... | Merhaba Portalı'nda ne olur? |
| --- | --- |
| Sürüm - GA |Yayın sürümüne (GA) çalıştırıyorsanız, bu güncelleştirme geçerli değildir. Lütfen [Microsoft Support başvurun](storsimple-contact-microsoft-support.md) tooupdate Cihazınızı. |
| Güncelleştirme 0.1 |Portal güncelleştirme 1.2 geçerlidir. |
| Güncelleştirme 0.2 |Portal güncelleştirme 1.2 geçerlidir. |
| Güncelleştirme 0.3 |Portal güncelleştirme 1.2 geçerlidir. |
| Güncelleştirme 1 |Bu güncelleştirme kullanılabilir olmaz. |
| Güncelleştirme 1.1 |Bu güncelleştirme kullanılabilir olmaz. |

</br>

> [!IMPORTANT]
> * Güncelleştirme 1.2 göremeyebilirsiniz hemen biz aşamalı hello güncelleştirmelerinin olmadığından. Yeniden birkaç gün içinde güncelleştirmeleri taramak üzere bu güncelleştirmeyi gibi yakında kullanılabilir hale gelecektir.
> * Bu güncelleştirme, donanım durumunu ve ağ bağlantısı bakımından elle ve otomatik ön denetimleri toodetermine hello cihaz sistem durumu kümesi içerir. Klasik Azure portalı hello hello güncelleştirmeleri uygularsanız, bu ön denetimleri gerçekleştirilir.
> * Merhaba yazılım yüklemek ve klasik Azure Portalı aracılığıyla sürücü güncelleştirmelerini hello öneririz. Merhaba Portalı'nda Hello güncelleştirme öncesi ağ geçidi denetimi başarısız olursa yalnızca toohello Windows PowerShell arabirimi hello aygıtının (tooinstall güncelleştirmeleri) gitmeniz gerekir. Merhaba güncelleştirmeleri (Merhaba Windows güncelleştirmeleri de dahil olmak üzere) 5-10 saat tooinstall sürebilir. Merhaba Bakım modu güncelleştirmeleri hello cihazın hello Windows PowerShell arabirimi yüklenmesi gerekir. Bakım modu kesintiye uğratan güncelleştirmelerdir gibi bunlar, cihazınız için aşağı zaman neden olur.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-12-via-hello-azure-classic-portal"></a>Güncelleştirme 1.2 hello Klasik Azure portalı yükleme
Aşağıdaki adımları tooupdate hello Cihazınızı çok gerçekleştirmek[güncelleştirme 1.2](storsimple-update1-release-notes.md). Veri 0 ağ arabirimindeki aygıtınızda yapılandırılmış bir ağ geçidi, bu yordamı kullanın.

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Cihazınızı çalıştığından emin olun **StorSimple 8000 serisi güncelleştirme 1.2 (6.3.9600.17584)**. Merhaba **son tarih güncelleştirme** değiştirilmeleri. Bakım modu güncelleştirmelerin kullanılabilir olduğunu görürsünüz (Bu ileti too24 saat yüklemeden sonra güncelleştirmeler hello için görüntülenen toobe devam edebilir).
   
   Bakım modu aygıt kapalı kalma sürelerine neden ve yalnızca aygıtınızın hello Windows PowerShell arabirimi uygulanabilir kesintiye uğratan güncelleştirmelerdir.
   
   ![Bakım Sayfası](./media/storsimple-install-update-1/InstallUpdate12_10M.png "Bakım Sayfası")
2. Listelenen hello adımları kullanarak Hello Bakım modu güncelleştirmeleri karşıdan [toodownload düzeltmeleri](#to-download-hotfixes) için toosearch ve disk Bellenim güncelleştirmeleri yükler KB3063416 indirin (Merhaba diğer güncelleştirmeleri artık yüklü olması).
3. Listelenen hello adımları [yükleme ve Bakım modu düzeltmeleri doğrulayın](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello Bakım modu güncelleştirmeler.
4. Buna Klasik Azure portalı Merhaba, toohello gidin **Bakım** sayfasında ve başlangıç sayfasının hello altında tıklayın **Güncelleştirmeleri tara** toocheck tüm Windows güncelleştirmeleri ve ardından **güncelleştirmeleri yükle** . Sonuçta hello başarıyla güncelleştirmelerin tamamlandı.

## <a name="install-update-12-on-a-device-that-has-a-gateway-configured-for-a-non-data-0-network-interface"></a>Güncelleştirme 1.2 olmayan veri 0 ağ arabirimi için yapılandırılmış bir ağ geçidi cihaza yükleyin
Merhaba Klasik Azure Portalı aracılığıyla tooinstall hello güncelleştirmeleri çalışırken hello ağ geçidi onay yalnızca başarısız olursa bu yordamı kullanmanız gerekir. Merhaba denetimi tooa olmayan DATA 0 ağ arabirimindeki atanmış bir ağ geçidine sahip ve Cihazınızı bir yazılım sürüm önceki tooUpdate 1 çalıştığından başarısız olur. Cihazınızı bir harici veri 0 ağ arabiriminde bir ağ geçidi yoksa, Cihazınızı doğrudan hello Klasik Azure portalı güncelleştirebilirsiniz. Bkz: [hello Klasik Azure Portalı aracılığıyla 1.2 güncelleştirme](#install-update-1.2-via-the-azure-classic-portal).

Bu yöntem kullanılarak yükseltilen hello yazılım güncelleştirme 0.1, güncelleştirme 0.2 ve Update 0.3 sürümleridir.

> [!IMPORTANT]
> * Cihazınızı sürüm (GA) sürümünü çalıştırıyorsa, temasa [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist hello ile güncelleştirin.
> * Bu yordam gereksinimlerini toobe tooapply güncelleştirme 1.2 yalnızca bir kez gerçekleştirilir. Hello Azure Klasik portalı tooapply sonraki güncelleştirmeler kullanabilirsiniz.
> 
> 

Cihazınızı güncelleştirme 1 yazılımı öncesini çalıştıran ve veri 0 dışında bir ağ arabirimi için ayarlanmış bir ağ geçidi varsa, aşağıdaki iki şekilde hello güncelleştirme 1.2 uygulayabilirsiniz:

* **Seçenek 1**: hello güncelleştirmesi ve hello kullanarak uygulamak `Start-HcsHotfix` hello cihazın hello Windows PowerShell arabiriminden cmdlet'i. Merhaba yöntemi önerilen budur. **Cihazınızı güncelleştirme 1.0 veya güncelleştirme 1.1 çalışıyorsa, bu yöntem tooapply güncelleştirme 1.2 kullanmayın.**
* **Seçenek 2**: Kaldır hello ağ geçidi yapılandırma ve yükleme hello doğrudan hello Klasik Azure Portalı ' güncelleştirin.

Aşağıdaki bölümlerde hello bunların her biri için ayrıntılı yönergeler sağlanır.

## <a name="option-1-use-windows-powershell-for-storsimple-tooapply-update-12-as-a-hotfix"></a>Seçenek 1: Bir düzeltme olarak StorSimple tooapply güncelleştirme 1.2 için Windows PowerShell'i kullanın
Güncelleştirme 0.1, 0.2, 0.3 ve ağ geçidi onay hello Klasik Azure Portalı'ndan tooinstall güncelleştirmelerini çalışırken başarısız oldu, yalnızca çalıştırıyorsanız, bu yordamı kullanmanız gerekir. Yayın (GA) yazılımı çalıştırıyorsanız, lütfen [Microsoft Support](storsimple-contact-microsoft-support.md) tooupdate Cihazınızı.

Güncelleştirme 1.2 bir düzeltme olarak tooinstall, indirin ve düzeltmeleri aşağıdaki hello yükleyin:

| Sırası | KB | Açıklama | Güncelleştirme türü |
| --- | --- | --- | --- |
| 1 |KB3063418 |Yazılım güncelleştirmesi |Normal |
| 2 |KB3043005 |LSI SAS denetleyicisi güncelleştirme |Normal |
| 3 |KB3063416 |Disk bellenim |Bakım |

Bu yordam tooapply hello kullanmadan önce güncelleştirmesi, olduğundan emin olun:

* Her iki aygıt denetleyicileri çevrimiçidir.

Aşağıdaki adımları tooapply güncelleştirme 1.2 hello gerçekleştirin. **Merhaba güncelleştirmeleri yaklaşık 2 saat toocomplete (yaklaşık 30 dakika yazılım, 30 dakika sürücüsünün disk bellenim 45 dakika) ele geçirebilir.**

[!INCLUDE [storsimple-install-update-option1](../../includes/storsimple-install-update-option1.md)]

## <a name="option-2-use-hello-azure-classic-portal-tooapply-update-12-after-removing-hello-gateway-configuration"></a>Seçenek 2: hello ağ geçidi yapılandırması kaldırdıktan sonra hello Azure Klasik portalı tooapply güncelleştirme 1.2 kullanın.
Bu yordam, bir yazılım sürüm önceki tooUpdate 1 çalıştırıyorsanız ve bir ağ arabiriminde veri 0 dışında ayarlanmış bir ağ geçidi tooStorSimple aygıtları uygulanır. Tooclear hello ağ geçidi ayarı önceki tooapplying hello güncelleştirmesi gerekir.

Merhaba güncelleştirme birkaç saat toocomplete sürebilir. Farklı alt ağlarda ana bilgisayarlarınız varsa hello iSCSI arabirimleri hello ağ geçidi yapılandırması kaldırılıyor kapalı kalma sürelerine neden olabilir. Veri 0 iSCSI trafiği tooreduce hello için kapalı kalma süresi yapılandırmanızı öneririz.

Aşağıdaki adımları toodisable hello ağ arabirimi hello ağ geçidi ile Merhaba gerçekleştirmek ve hello güncelleştirmeyi uygulayın.

[!INCLUDE [storsimple-install-update-option2](../../includes/storsimple-install-update-option2.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [güncelleştirme 1.2 sürümü](storsimple-update1-release-notes.md).

