---
title: "StorSimple Cihazınızda aaaInstall güncelleştirme 2 | Microsoft Docs"
description: "Açıklar nasıl StorSimple 8000 serisi aygıtınızda tooinstall StorSimple 8000 serisi güncelleştirme 2."
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
ms.openlocfilehash: 33a0bea4358c944644563192f686af332d2ad7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-2-on-your-storsimple-device"></a>StorSimple Cihazınızda güncelleştirme 2'yi yükleme
## <a name="overview"></a>Genel Bakış
Bu öğretici tooinstall güncelleştirme 2 hello Klasik Azure portalı önceki bir yazılım sürümünü çalıştıran bir StorSimple cihazda nasıl açıklanmaktadır. Başlangıç Öğreticisi de bir ağ arabiriminde hello StorSimple cihazı veri 0 dışında bir ağ geçidi yapılandırıldığında ve bir güncelleştirme öncesi 1 yazılımı sürümünden tooupdate çalıştığınız hello güncelleştirmesi gerekli hello adımlar kapsanmaktadır.

Güncelleştirme 2 cihaz yazılım güncelleştirmeleri, LSI sürücü güncelleştirmelerini ve disk Bellenim güncelleştirmeleri içerir. Merhaba aygıt yazılımı ve LSI güncelleştirmeleri benzer güncelleştirmeleri ve hello Klasik Azure portalı uygulanabilir. Merhaba disk Bellenim güncelleştirmeleri kesintiye uğratan güncelleştirmelerin ve yalnızca hello cihazın hello Windows PowerShell arabirimi uygulanabilir.

> [!IMPORTANT]
> * Güncelleştirme 2 göremeyebilirsiniz hemen biz aşamalı hello güncelleştirmelerinin olmadığından. Yeniden birkaç gün içinde güncelleştirmeleri taramak üzere bu güncelleştirmeyi gibi yakında kullanılabilir hale gelecektir.
> * Elle ve otomatik ön denetimleri kümesini önceki toohello yükleme toodetermine hello cihaz durumunu donanım durumu ve ağ bağlantısı bakımından yapılır. Klasik Azure portalı hello hello güncelleştirmeleri uygularsanız, bu ön denetimleri gerçekleştirilir.
> * Merhaba yazılım yüklemek ve klasik Azure Portalı aracılığıyla sürücü güncelleştirmelerini hello öneririz. Merhaba Portalı'nda Hello güncelleştirme öncesi ağ geçidi denetimi başarısız olursa yalnızca toohello Windows PowerShell arabirimi hello aygıtının (tooinstall güncelleştirmeleri) gitmeniz gerekir. Merhaba güncelleştirmeleri (Merhaba Windows güncelleştirmeleri de dahil olmak üzere) 4-7 saat tooinstall sürebilir. Merhaba Bakım modu güncelleştirmeleri hello cihazın hello Windows PowerShell arabirimi yüklenmesi gerekir. Bakım modu kesintiye uğratan güncelleştirmelerdir gibi bunlar, cihazınız için aşağı zaman neden olur.
> * İsteğe bağlı StorSimple Snapshot Manager çalışan Merhaba, anlık görüntü Yöneticisi sürüm 2 tooUpdate önceki tooupdating hello Cihazınızı yükselttikten emin olun.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-2-via-hello-azure-classic-portal"></a>Merhaba Klasik Azure portalı güncelleştirme 2'yi yükleme
Aşağıdaki adımları tooupdate hello Cihazınızı çok gerçekleştirmek[güncelleştirme 2](storsimple-update2-release-notes.md).

> [!NOTE]
> Güncelleştirme 2 Microsoft toopull ek tanılama bilgilerinin hello aygıttan sağlar. Sonuç olarak, operations ekibimiz sorunlarınız aygıtları belirlediğinde, biz hello aygıttan daha iyi donanımlı toocollect bilgileri sorunlarını tanılamak ve. Güncelleştirme 2 kabul ederek, bize tooprovide izin bu öngörülü desteği.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Cihazınızı çalıştığından emin olun **StorSimple 8000 serisi güncelleştirme 2 (6.3.9600.17673)**. Merhaba **son tarih güncelleştirme** değiştirilmeleri. Bakım modu güncelleştirmelerin kullanılabilir olduğunu görürsünüz (Bu ileti too24 saat yüklemeden sonra güncelleştirmeler hello için görüntülenen toobe devam edebilir).
   
   Bakım modu aygıt kapalı kalma sürelerine neden ve yalnızca aygıtınızın hello Windows PowerShell arabirimi uygulanabilir kesintiye uğratan güncelleştirmelerdir. Bazı durumlarda Güncelleştirme 1.2 çalıştırırken, disk bellenim zaten güncel olabilir, tooinstall gerekmez; bu durumda herhangi bir Bakım modu güncelleştirir.
2. Listelenen hello adımları kullanarak Hello Bakım modu güncelleştirmeleri karşıdan [toodownload düzeltmeleri](#to-download-hotfixes) için toosearch ve disk Bellenim güncelleştirmeleri yükler KB3121899 indirin (Merhaba diğer güncelleştirmeleri artık yüklü olması).
3. Listelenen hello adımları [yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello Bakım modu güncelleştirmeler.

## <a name="install-update-2-as-a-hotfix"></a>Bir düzeltme olarak güncelleştirme 2'yi yükleme
Merhaba ağ geçidi onay hello Klasik Azure Portalı aracılığıyla tooinstall hello güncelleştirmeleri çalışırken başarısız olursa bu yordamı kullanın. Merhaba denetimi tooa olmayan DATA 0 ağ arabirimindeki atanmış bir ağ geçidine sahip ve Cihazınızı bir yazılım sürüm önceki tooUpdate 1 çalıştığından başarısız olur.

Merhaba düzeltme yöntemi kullanılarak yükseltilen hello yazılım güncelleştirme 0.1, güncelleştirme 0.2 ve güncelleştirme 0.3, Update 1, güncelleştirme 1.1 ve güncelleştirme 1.2 sürümleridir. Merhaba düzeltme yöntemi hello aşağıdaki üç adımları içerir:

* Merhaba düzeltmeleri hello Microsoft Update Kataloğu ' indirin.
* Yükleyin ve hello normal modu düzeltmeleri doğrulayın.
* Yükleyin ve hello Bakım modu düzeltme doğrulayın.

Güncelleştirme 2 bir düzeltme olarak tooinstall, indirin ve düzeltmeleri aşağıdaki hello yükleyin:

| Sırası | KB | Açıklama | Güncelleştirme türü |
| --- | --- | --- | --- |
| 1 |KB3121901 |Yazılım güncelleştirmesi |Normal |
| 2 |KB3121900 |LSI sürücüsü |Normal |
| 3 |KB3080728 |Storport düzeltme </br> Windows Server 2012 R2 |Normal |
| 4 |KB3090322 |Spaceport düzeltme </br> Windows Server 2012 R2 |Normal |
| 5 |KB3121899 |Disk bellenim |Bakım |

> [!IMPORTANT]
> * Cihazınızı sürüm (GA) sürümünü çalıştırıyorsa, temasa [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist hello ile güncelleştirin.
> * Bu yordam gereksinimlerini toobe tooapply güncelleştirme 2 yalnızca bir kez gerçekleştirilir. Hello Azure Klasik portalı tooapply sonraki güncelleştirmeler kullanabilirsiniz.
> * Her düzeltme yüklemesi toocomplete yaklaşık 20 dakika sürebilir. Toplam yükleme saatini Kapat too2 saattir.
> * Bu yordam tooapply hello kullanmadan önce güncelleştirme, her iki aygıt denetleyicileri çevrimiçi olduğundan ve tüm hello donanım bileşenleri sağlıklı olduğundan emin olun.
> 
> 

Aşağıdaki adımları tooapply hello Bu güncelleştirme düzeltme olarak gerçekleştirin.

[!INCLUDE [storsimple-install-update2-hotfix](../../includes/storsimple-install-update2-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [güncelleştirme 2 sürümünün](storsimple-update2-release-notes.md).

