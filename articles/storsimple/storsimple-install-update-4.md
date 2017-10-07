---
title: "StorSimple Cihazınızda aaaInstall güncelleştirme 4 | Microsoft Docs"
description: "Açıklar nasıl tooinstall StorSimple 8000 serisi güncelleştirme 4, StorSimple 8000 serisi Cihazınızda."
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
ms.date: 05/30/2017
ms.author: alkohli
ms.openlocfilehash: 62c0ae94afdbb1027d3075962afa04d49fd1f60a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-4-on-your-storsimple-device"></a>StorSimple Cihazınızda güncelleştirme 4'ü yükleyin

## <a name="overview"></a>Genel Bakış

Bu öğretici tooinstall güncelleştirme 4 aracılığıyla önceki bir yazılım sürümünü çalıştıran bir StorSimple cihazda nasıl hello Klasik Azure portalı ve hello düzeltme yöntemini kullanarak açıklanmaktadır. Merhaba düzeltme yöntemi, bir ağ arabiriminde hello StorSimple cihazı veri 0 dışında bir ağ geçidi yapılandırıldığında ve bir güncelleştirme öncesi 1 yazılımı sürümünden tooupdate çalıştığınız kullanılır.

Güncelleştirme 4 aygıt yazılımı, USM üretici yazılımı, LSI sürücü ve bellenim, Storport ve Spaceport, işletim sistemi güvenlik güncelleştirmelerini ve diğer işletim sistemi güncelleştirmelerini ana bilgisayarını içerir.  Merhaba aygıt yazılımı, USM üretici yazılımı, Spaceport, Storport ve diğer işletim sistemi güncelleştirmelerini benzer güncelleştirmelerdir. Merhaba benzer veya normal güncelleştirmeleri hello düzeltme yöntemle veya hello Klasik Azure Portalı aracılığıyla uygulanabilir. Merhaba disk Bellenim güncelleştirmeleri kesintiye uğratan güncelleştirmelerin ve hello düzeltme yöntemiyle hello cihazın hello Windows PowerShell arabirimini kullanarak yalnızca uygulanabilir. 

> [!IMPORTANT]
> * Elle ve otomatik ön denetimleri kümesini önceki toohello yükleme toodetermine hello cihaz durumunu donanım durumu ve ağ bağlantısı bakımından yapılır. Klasik Azure portalı hello hello güncelleştirmeleri uygularsanız, bu ön denetimleri gerçekleştirilir.
> * Merhaba yazılım ve diğer düzenli güncelleştirmeler hello Klasik Azure Portalı aracılığıyla yüklemenizi öneririz. Merhaba Portalı'nda Hello güncelleştirme öncesi ağ geçidi denetimi başarısız olursa yalnızca toohello Windows PowerShell arabirimi hello aygıtının (tooinstall güncelleştirmeleri) gitmeniz gerekir. Gelen güncelleştirdiğiniz hello sürüm bağlı olarak, hello güncelleştirmeleri 4 saat sürebilir (veya daha büyük) tooinstall. Merhaba Bakım modu güncelleştirmeleri hello cihazın hello Windows PowerShell arabirimi de yüklenmesi gerekir. Bakım modu kesintiye uğratan güncelleştirmelerdir gibi bunlar, cihazınız için aşağı zaman neden olur.
> * İsteğe bağlı StorSimple Snapshot Manager çalışan Merhaba, anlık görüntü Yöneticisi sürüm tooUpdate 4 önceki tooupdating hello Cihazınızı yükselttikten emin olun.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-4-via-hello-azure-classic-portal"></a>Merhaba Klasik Azure portalı güncelleştirme 4'ü yükleyin
Aşağıdaki adımları tooupdate hello Cihazınızı çok gerçekleştirmek[güncelleştirme 4](storsimple-update4-release-notes.md).

> [!NOTE]
> Daha sonra (de dahil olmak üzere güncelleştirme 2.1) veya güncelleştirme 2 uyguluyorsanız Microsoft mümkün toopull ek tanılama bilgilerinin hello aygıttan olacaktır. Sonuç olarak, operations ekibimiz sorunlarınız aygıtları belirlediğinde, biz hello aygıttan daha iyi donanımlı toocollect bilgileri sorunlarını tanılamak ve. Güncelleştirme 2 veya sonrası kabul ederek, bize tooprovide izin bu öngörülü desteği. 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

Cihazınızı çalıştığından emin olun **StorSimple 8000 serisi güncelleştirme 4 (6.3.9600.17820)**. Merhaba **son tarih güncelleştirme** değiştirilmeleri. 

* Şimdi hello Bakım modu güncelleştirmelerin kullanılabilir olduğunu göreceksiniz (Bu ileti too24 saat yüklemeden sonra güncelleştirmeler hello için görüntülenen toobe devam edebilir). Bakım modu aygıt kapalı kalma sürelerine neden ve yalnızca aygıtınızın hello Windows PowerShell arabirimi uygulanabilir kesintiye uğratan güncelleştirmelerdir.
 
* Listelenen hello adımları kullanarak Hello Bakım modu güncelleştirmeleri karşıdan [toodownload düzeltmeleri](#to-download-hotfixes) için toosearch ve disk Bellenim güncelleştirmeleri yükler KB4011837 indirin (Merhaba diğer güncelleştirmeleri artık yüklü olması). Listelenen hello adımları [yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello Bakım modu güncelleştirmeler. 

## <a name="install-update-4-as-a-hotfix"></a>Bir düzeltme olarak güncelleştirme 4'ü yükleyin
Merhaba hello Klasik Azure portalı güncelleştirme 4. yöntemi tooinstall önerilir.

Merhaba ağ geçidi onay hello Klasik Azure Portalı aracılığıyla tooinstall hello güncelleştirmeleri çalışırken başarısız olursa bu yordamı kullanın. Merhaba denetimi tooa olmayan DATA 0 ağ arabirimindeki atanmış bir ağ geçidine sahip ve Cihazınızı bir yazılım sürüm önceki tooUpdate 1 çalıştığından başarısız olur.

Merhaba düzeltme yöntemini kullanarak yükseltilebilir hello yazılım sürümleri şunlardır:

* Güncelleştirme 0.1, 0.2, 0.3
* 1, 1.1 ve 1.2 güncelleştirmesi
* Güncelleştirme 2, 2.1, 2.2
* Güncelleştirme 3, 3.1 


Merhaba düzeltme yöntemi hello aşağıdaki üç adımları içerir:

1. Merhaba düzeltmeleri hello Microsoft Update Kataloğu ' indirin.
2. Yükleyin ve hello normal modu düzeltmeleri doğrulayın.
3. Yükleyin ve hello Bakım modu düzeltme doğrulayın.

#### <a name="download-updates-for-your-device"></a>Cihazınız için güncelleştirmeleri karşıdan yükle

Merhaba aşağıdaki yükleyip gerekir belirlenen hello düzeltmeleri sipariş ve hello önerilen klasörler:

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |Klasöre yükleyin|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4011839 <br> (2 dosyaları) |Aygıt bir yazılım güncelleştirmesi <br> CIS/MDS aracı güncelleştirmesi |Normal <br></br>Olmayan kesintiye uğratan |~ 25 dakika |FirstOrderUpdate <br> _Aygıt yazılım güncelleştirmesini CIS/MDS aracı güncelleştirme öncesi_|
| 2A. |KB4011841 <br> KB4011842 |LSI sürücü ve bellenim güncelleştirmeleri <br> USM bellenim güncelleştirme (sürüm 3,38) |Normal <br></br>Olmayan kesintiye uğratan |~ 3 saat <br> (2A içerir. + 2B. + 2 C.)|SecondOrderUpdate|
| 2B. |KB3139398, KB3108381 <br> KB3205400, KB3142030 <br> KB3197873, KB3192392  <br> KB3153704, KB3174644 <br> KB3139914  |İşletim sistemi güvenlik güncelleştirmeleri paketi |Normal <br></br>Olmayan kesintiye uğratan |- |SecondOrderUpdate|
| 2 C |KB3210083, KB3103616 <br> KB3146621, KB3121261 <br> KB3123538 |İşletim sistemi güncelleştirmeleri paketi |Normal <br></br>Olmayan kesintiye uğratan |- |SecondOrderUpdate|

Önceki tabloların hello gösterilen tüm hello güncelleştirmeleri üstünde tooinstall disk Bellenim güncelleştirmeleri de gerekebilir. Merhaba çalıştırarak disk Bellenim güncelleştirmeleri hello olup olmadığını doğrulayabilirsiniz `Get-HcsFirmwareVersion` cmdlet'i. Bu bellenim sürümleri çalıştırıyorsanız: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N002`, `0106`, sonra da bu güncelleştirmeler tooinstall gerekmez.

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati | Klasöre yükleyin|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4011837 |Disk bellenim |Bakım <br></br>Kesintiye uğratan |~ 30 dakika | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Bu yordam gereksinimlerini toobe tooapply güncelleştirme 4 yalnızca bir kez gerçekleştirilir. Hello Azure Klasik portalı tooapply sonraki güncelleştirmeler kullanabilirsiniz.
> * Güncelleştirme 3'ü veya 3.1 güncelleştirmek, hello toplam yükleme saatini Kapat too4 saattir.
> * Bu yordam tooapply hello kullanmadan önce güncelleştirme, hem hello aygıt denetleyicileri çevrimiçi olduğundan ve tüm hello donanım bileşenleri sağlıklı olduğundan emin olun.

Aşağıdaki adımları toodownload hello gerçekleştirin ve hello düzeltmeyi yükleyin.

[!INCLUDE [storsimple-install-update4-hotfix](../../includes/storsimple-install-update4-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [güncelleştirme 4 yayın](storsimple-update4-release-notes.md).

