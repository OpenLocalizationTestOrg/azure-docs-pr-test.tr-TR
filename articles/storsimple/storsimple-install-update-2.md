---
title: "StorSimple Cihazınızda güncelleştirme 2'yi yükleme | Microsoft Docs"
description: "StorSimple 8000 serisi güncelleştirme 2 StorSimple 8000 serisi cihazınıza yüklediğiniz açıklanmaktadır."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 8c8981df-75d9-4d19-b137-d6c6ba39dcfb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/21/2016
ms.author: alkohli
ms.openlocfilehash: e788439608b7122f2bca6b99b832baa5258e472d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>StorSimple Cihazınızda güncelleştirme 2'yi yükleme
## <a name="overview"></a>Genel Bakış
Bu öğretici, Klasik Azure portalı önceki yazılım sürümleri çalıştıran StorSimple cihazını güncelleştirme 2 yükleyin açıklanmaktadır. Öğretici da bir ağ arabiriminde StorSimple cihaz veri 0 dışında bir ağ geçidi yapılandırıldığında ve bir güncelleştirme öncesi 1 yazılımı sürümü güncelleştirmeye çalıştığınız güncelleştirme için gerekli olan adımları kapsar.

Güncelleştirme 2 cihaz yazılım güncelleştirmeleri, LSI sürücü güncelleştirmelerini ve disk Bellenim güncelleştirmeleri içerir. Aygıt yazılımı ve LSI güncelleştirmeleri benzer güncelleştirmeleri ve klasik Azure portalı uygulanabilir. Disk Bellenim güncelleştirmeleri kesintiye uğratan güncelleştirmelerin ve yalnızca aygıt Windows PowerShell arabirimi uygulanabilir.

> [!IMPORTANT]
> * Güncelleştirme 2 göremeyebilirsiniz hemen biz aşamalı güncelleştirmeler yapmak için. Yeniden birkaç gün içinde güncelleştirmeleri taramak üzere bu güncelleştirmeyi gibi yakında kullanılabilir hale gelecektir.
> * Elle ve otomatik ön denetimleri kümesini donanım durumu ve ağ bağlantısı bakımından cihaz durumunu belirlemek için yükleme öncesinde gerçekleştirilir. Klasik Azure portalından güncelleştirmeleri uygularsanız, bu ön denetimleri gerçekleştirilir.
> * Klasik Azure Portalı aracılığıyla yazılım ve sürücü güncelleştirmelerini yüklemenizi öneririz. Portalda güncelleştirme öncesi ağ geçidi denetimi başarısız olursa (güncelleştirmeleri yüklemek için) cihazın Windows PowerShell arabirimine yalnızca gitmeniz gerekir. Güncelleştirmeler (Windows güncelleştirmeleri dahil) yüklemek için 4-7 saat sürebilir. Bakım modu güncelleştirmeleri aygıtı Windows PowerShell arabirimi yüklenmesi gerekir. Bakım modu kesintiye uğratan güncelleştirmelerdir gibi bunlar, cihazınız için aşağı zaman neden olur.
> * İsteğe bağlı StorSimple Snapshot Manager çalışıyorsa, anlık görüntü Yöneticisi'ni sürümü güncelleştirme 2'ye aygıtı güncelleştirme önce yükselttikten emin olun.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-the-azure-classic-portal"></a>Azure Klasik portalı üzerinden güncelleştirme 2'yi yükleme
İçin Cihazınızı güncelleştirmek için aşağıdaki adımları gerçekleştirin [güncelleştirme 2](storsimple-update2-release-notes.md).

> [!NOTE]
> Güncelleştirme 2 aygıttan ek tanılama bilgilerini Microsoft'a sağlar. Sorunlarınız aygıtları operations ekibimiz belirlediğinde, sonuç olarak, daha iyi aygıttan bilgi toplamak ve sorunları tanılamak donanımlı duyuyoruz. Güncelleştirme 2 kabul ederek, bize bu öngörülü desteği sağlamak izin verir.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Cihazınızı çalıştığından emin olun **StorSimple 8000 serisi güncelleştirme 2 (6.3.9600.17673)**. **Son tarih güncelleştirme** değiştirilmeleri. Bakım modu güncelleştirmelerin kullanılabilir olduğunu görürsünüz (Bu ileti 24 güncelleştirmeleri yükledikten sonra saate kadar gösterilmeye devam).
   
   Bakım modu aygıt kapalı kalma sürelerine neden ve Cihazınızı Windows PowerShell arabirimi yalnızca uygulanabilir kesintiye uğratan güncelleştirmelerdir. Bazı durumlarda Güncelleştirme 1.2 çalıştırırken, disk bellenim zaten güncel herhangi bir Bakım modu güncelleştirme yüklemeniz gerekmez; bu durumda olabilir.
2. Bakım modu listelenen adımları kullanarak güncelleştirmeler [düzeltmeleri indirmek için](#to-download-hotfixes) aramak ve KB3121899, (diğer güncelleştirmeleri zaten yüklenmesi gerekir artık) hangi yükler disk Bellenim güncelleştirmeleri karşıdan yüklemek için.
3. Listelenen adımları izleyin [yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes) Bakım modu yüklemek için güncelleştirir.

## <a name="install-update-2-as-a-hotfix"></a>Bir düzeltme olarak güncelleştirme 2'yi yükleme
Ağ geçidi onay Klasik Azure Portalı aracılığıyla güncelleştirmeleri yüklenmeye çalışırken başarısız olursa bu yordamı kullanın. Bir veri dışı 0 ağ arabirimine atanmış bir ağ geçidine sahip ve Cihazınızı yazılım sürümü güncelleştirme 1 önce çalışan denetimi başarısız olur.

Düzeltme yöntemi kullanılarak yükseltilen yazılım güncelleştirme 0.1, güncelleştirme 0.2 ve güncelleştirme 0.3, Update 1, güncelleştirme 1.1 ve güncelleştirme 1.2 sürümleridir. Düzeltme yöntemi aşağıdaki üç adımdan oluşur:

* Düzeltmeleri Microsoft Update Kataloğu'ndan indirin.
* Yükleyin ve normal modu düzeltmeleri doğrulayın.
* Yükleme ve Bakım modu düzeltme doğrulayın.

Güncelleştirme 2 bir düzeltme olarak yüklemek için aşağıdaki düzeltmeleri yükleyip gerekir:

| Sırası | KB | Açıklama | Güncelleştirme türü |
| --- | --- | --- | --- |
| 1 |KB3121901 |Yazılım güncelleştirmesi |Normal |
| 2 |KB3121900 |LSI sürücüsü |Normal |
| 3 |KB3080728 |Storport düzeltme </br> Windows Server 2012 R2 |Normal |
| 4 |KB3090322 |Spaceport düzeltme </br> Windows Server 2012 R2 |Normal |
| 5 |KB3121899 |Disk bellenim |Bakım |

> [!IMPORTANT]
> * Cihazınızı sürüm (GA) sürümünü çalıştırıyorsa, temasa [Microsoft Support](storsimple-contact-microsoft-support.md) güncelleştirmeyle yardımcı olmak için.
> * Bu yordamı güncelleştirme 2 uygulamak için yalnızca bir kez gerçekleştirilmesi gerekir. Sonraki güncelleştirmeleri uygulamak için Klasik Azure portalını kullanabilirsiniz.
> * Her düzeltme yüklemesini tamamlamak için yaklaşık 20 dakika sürebilir. Toplam yükleme süresi dolmak üzere 2 saattir.
> * Güncelleştirmeyi uygulamak için bu yordamı kullanmadan önce hem aygıt denetleyicileri çevrimiçi olduğundan ve tüm donanım bileşenleri sağlıklı olduğundan emin olun.
> 
> 

Bir düzeltme olarak bu güncelleştirmeyi uygulamak için aşağıdaki adımları gerçekleştirin.

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [güncelleştirme 2 sürümünün](storsimple-update2-release-notes.md).

