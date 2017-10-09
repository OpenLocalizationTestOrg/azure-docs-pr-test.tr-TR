---
title: "aaaUpdate StorSimple Cihazınızı | Microsoft Docs"
description: "Toouse hello StorSimple güncelleştirme nasıl özelliği tooinstall normal ve Bakım modu güncelleştirmeleri ve düzeltmeleri açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 786059f5-2a38-4105-941d-0860ce4ac515
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/18/2016
ms.author: v-sharos
ms.openlocfilehash: 05acf05c8fc89bbb4343f67ad103235bbe3dba0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="update-your-storsimple-8000-series-device"></a>StorSimple 8000 serisi Cihazınızı güncelleştirin
## <a name="overview"></a>Genel Bakış
Merhaba StorSimple güncelleştirmeleri özellikleri izin tooeasily StorSimple cihazınız güncel tutun. Merhaba güncelleştirme türüne bağlı olarak, güncelleştirmeleri toohello aygıt hello Windows PowerShell arabirimi üzerinden veya hello Klasik Azure Portalı aracılığıyla uygulayabilirsiniz. Bu öğretici hello güncelleştirme türlerini açıklar ve nasıl tooinstall her biri.

Cihaz güncelleştirmeleri iki tür uygulayabilirsiniz: 

* Normal (veya Normal modda) güncelleştirmeleri
* Bakım modu güncelleştirmeleri

Merhaba Klasik Azure portalı veya Windows PowerShell aracılığıyla düzenli olarak güncelleştirmeleri yükleyebilirsiniz; Ancak, Windows PowerShell tooinstall Bakım modu güncelleştirmeleri kullanmanız gerekir. 

Ayrıca, aşağıda açıklanan her güncelleştirme türüdür.

### <a name="regular-updates"></a>Düzenli olarak güncelleştirmeleri
Normal hello cihaz Normal modda olduğunda, yüklenebilen benzer güncelleştirmelerdir. Bu güncelleştirmeler hello Microsoft Update Web sitesini tooeach aygıt denetleyicisi uygulanır. 

> [!IMPORTANT]
> Denetleyici yük devretmesi hello güncelleştirme işlemi sırasında ortaya çıkabilir. Ancak, bu sistem kullanılabilirliğini veya işlem etkilemez.
> 
> 

* Nasıl tooinstall normal hello Klasik Azure portalı güncelleştirmeleri hakkında daha fazla bilgi için bkz: [hello Klasik Azure Portalı aracılığıyla normal güncelleştirmelerini yükleme](#install-regular-updates-via-the-azure-classic-portal).
* StorSimple için Windows PowerShell aracılığıyla düzenli olarak güncelleştirmeleri de yükleyebilirsiniz. Ayrıntılar için bkz [StorSimple için Windows PowerShell aracılığıyla normal güncelleştirmelerini yükleme](#install-regular-updates-via-windows-powershell-for-storsimple).

### <a name="maintenance-mode-updates"></a>Bakım modu güncelleştirmeleri
Bakım modu kesintiye uğratan disk bellenim yükseltmeleri gibi güncelleştirmelerdir. Bu güncelleştirmeler bakım moduna hello aygıt toobe gerektirir. Ayrıntılar için bkz [2. adım: girin Bakım modu](#step2). Hello Azure Klasik portalı tooinstall Bakım modu güncelleştirmelerini kullanamazsınız. Bunun yerine, StorSimple için Windows PowerShell kullanmanız gerekir. 

Güncelleştirme biçimini tooinstall Bakım modu hakkında daha fazla bilgi için bkz [yükleme Bakım modu güncelleştirmeleri StorSimple için Windows PowerShell aracılığıyla](#install-maintenance-mode-updates-via-windows-powershell-for-storsimple).

> [!IMPORTANT]
> Bakım modu güncelleştirmeleri olmalıdır tooeach denetleyicisi ayrı olarak uygulanır. 
> 
> 

## <a name="install-regular-updates-via-hello-azure-classic-portal"></a>Merhaba Klasik Azure Portalı aracılığıyla düzenli olarak güncelleştirmeleri yükle
Hello Azure Klasik portalı tooapply güncelleştirmeleri tooyour StorSimple cihazı kullanabilirsiniz.

[!INCLUDE [storsimple-install-updates-manually](../../includes/storsimple-install-updates-manually.md)]

## <a name="install-regular-updates-via-windows-powershell-for-storsimple"></a>StorSimple için Windows PowerShell aracılığıyla düzenli olarak güncelleştirmeleri yükle
Alternatif olarak, StorSimple tooapply normal (Normal modda) güncelleştirmeleri için Windows PowerShell'i kullanabilirsiniz.

> [!IMPORTANT]
> StorSimple için Windows PowerShell kullanarak düzenli olarak güncelleştirmeleri yükleyebilirsiniz, ancak düzenli olarak güncelleştirmeleri hello Klasik Azure Portalı aracılığıyla yüklemenizi öneririz. Güncelleştirme 1'den başlayarak, ön denetimleri gerçekleştirilen önceki tooinstalling güncelleştirmeleri hello portalından olacaktır. Bu ön denetimleri hatalarını önüne geçer ve daha sorunsuz bir deneyim emin olun. 
> 
> 

[!INCLUDE [storsimple-install-regular-updates-powershell](../../includes/storsimple-install-regular-updates-powershell.md)]

## <a name="install-maintenance-mode-updates-via-windows-powershell-for-storsimple"></a>StorSimple için Windows PowerShell aracılığıyla Bakım modu güncelleştirmeleri yükle
StorSimple tooapply Bakım modu güncelleştirmeleri tooyour StorSimple cihazı için Windows PowerShell kullanın. Tüm g/ç istekleri bu modda duraklatıldı. Geçici olmayan rasgele erişim belleği (NVRAM) veya hizmet kümeleme hello gibi hizmetleri de durdurulur. Girin ya da bu modundan çıkmak hem denetleyicileri yeniden başlatılır. Bu mod çıktığınızda, tüm hello Hizmetleri devam eder ve iyi durumda olmalıdır. (Bu işlem birkaç dakika sürebilir.)

Tooapply Bakım modu güncelleştirmeleri gerekiyorsa, yüklenmesi gereken güncelleştirmelerin yüklü olduğundan hello Klasik Azure Portalı aracılığıyla bir uyarı alırsınız. Bu uyarı StorSimple tooinstall hello güncelleştirmeleri için Windows PowerShell kullanma yönergeleri içerir. Cihazınızı güncelleştirmeden sonra kullanım hello aynı yordamı toochange hello aygıt tooRegular modu. Adım adım yönergeler için bkz: [4. adım: çıkış Bakım modu](#step4).

> [!IMPORTANT]
> * Bakım modu girmeden önce hello denetleyerek hem de cihaz denetleyicilerinin sağlıklı olduğunu doğrula **donanım durumu** hello üzerinde **Bakım** hello Klasik Azure portalı sayfasında. Merhaba denetleyicisi iyi durumda değil, Microsoft Support hello sonraki adımlar için başvurun. Daha fazla bilgi için Microsoft Support tooContact gidin. 
> * Bakım modunda olduğunda tooapply gereken bir denetleyicisine ilk güncelleştirme hello ve ardından üzerindeki diğer denetleyicisi hello.
> 
> 

### <a name="step-1-connect-toohello-serial-console-a-namestep1"></a>1. adım: toohello seri konsol bağlantısı<a name="step1">
İlk olarak, seri konsol PuTTY tooaccess hello gibi bir uygulama kullanın. Merhaba aşağıdaki yordam açıklanmaktadır nasıl toouse PuTTY tooconnect toohello seri konsol.

[!INCLUDE [storsimple-use-putty](../../includes/storsimple-use-putty.md)]

### <a name="step-2-enter-maintenance-mode-a-namestep2"></a>2. adım: Bakım modu girin<a name="step2">
Toohello konsol bağlandıktan sonra güncelleştirmelerinin tooinstall olup olmadığını belirlemek ve Bakım modu tooinstall girin bunları.

[!INCLUDE [storsimple-enter-maintenance-mode](../../includes/storsimple-enter-maintenance-mode.md)]

### <a name="step-3-install-your-updates-a-namestep3"></a>3. adım: güncellemelerinizi yükleme<a name="step3">
Ardından, güncelleştirmelerinizi yükleyin.

[!INCLUDE [storsimple-install-maintenance-mode-updates](../../includes/storsimple-install-maintenance-mode-updates.md)]

### <a name="step-4-exit-maintenance-mode-a-namestep4"></a>4. adım: Çıkış Bakım modu<a name="step4">
Son olarak, bakım modundan çıkın.

[!INCLUDE [storsimple-exit-maintenance-mode](../../includes/storsimple-exit-maintenance-mode.md)]

## <a name="install-hotfixes-via-windows-powershell-for-storsimple"></a>StorSimple için Windows PowerShell aracılığıyla düzeltmeleri yükleme
Microsoft Azure StorSimple güncelleştirmeleri, paylaşılan bir klasörden düzeltmeleri yüklenir. Güncelleştirmelerinde olduğu gibi düzeltmeler iki tür vardır: 

* Normal düzeltmeleri 
* Bakım modu düzeltmeleri  

Merhaba aşağıdaki yordamlar açıklamaktadır nasıl toouse Windows PowerShell StorSimple tooinstall normal ve Bakım modu düzeltmeler.

[!INCLUDE [storsimple-install-regular-hotfixes](../../includes/storsimple-install-regular-hotfixes.md)]

[!INCLUDE [storsimple-install-maintenance-mode-hotfixes](../../includes/storsimple-install-maintenance-mode-hotfixes.md)]

## <a name="what-happens-tooupdates-if-you-perform-a-factory-reset-of-hello-device"></a>Merhaba aygıtın bir Fabrika gerçekleştirirseniz tooupdates sıfırlama ne olur?
Bir aygıt toofactory ayarlarını sıfırla ise, tüm hello güncelleştirmeleri kaybolur. Merhaba Fabrika sıfırlaması cihaz kayıtlı yapılandırıldıktan sonra StorSimple için toomanually hello Klasik Azure portalı ve/veya Windows PowerShell aracılığıyla güncelleştirmeleri yükleme gerekir. Fabrika sıfırlaması hakkında daha fazla bilgi için bkz: [hello aygıt toofactory varsayılan ayarlara](storsimple-manage-device-controller.md#reset-the-device-to-factory-default-settings).

## <a name="next-steps"></a>Sonraki adımlar
* Daha fazla bilgi edinmek [StorSimple Cihazınızı StorSimple tooadminister için Windows PowerShell kullanarak](storsimple-windows-powershell-administration.md).
* Daha fazla bilgi edinmek [kullanarak, StorSimple Cihazınızı StorSimple Yöneticisi hizmet tooadminister hello](storsimple-manager-service-administration.md).

