---
title: "StorSimple 8000 serisi cihazda güncelleştirme 5 aaaInstall | Microsoft Docs"
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
ms.date: 08/22/2017
ms.author: alkohli
ms.openlocfilehash: a832f9953e8e39408efeeed375e3afe8eee8d0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-5-on-your-storsimple-device"></a>StorSimple Cihazınızda güncelleştirme 5 yükleyin

## <a name="overview"></a>Genel Bakış

Bu öğretici tooinstall güncelleştirme 5 aracılığıyla önceki bir yazılım sürümünü çalıştıran bir StorSimple cihazda nasıl hello Azure portalı ve hello düzeltme yöntemini kullanarak açıklanmaktadır. Merhaba düzeltme yöntemi, bir ağ arabiriminde hello StorSimple cihazı veri 0 dışında bir ağ geçidi yapılandırıldığında ve bir güncelleştirme öncesi 1 yazılımı sürümünden tooupdate çalıştığınız kullanılır.

Güncelleştirme 5 içerir aygıt yazılımı, Storport ve Spaceport, işletim sistemi güvenlik güncelleştirmelerini ve işletim sistemi güncelleştirmelerini ve disk Bellenim güncelleştirmeleri.  Merhaba aygıt yazılımı, Spaceport, Storport, güvenlik ve diğer işletim sistemi güncelleştirmelerini benzer güncelleştirmelerdir. Merhaba benzer veya normal güncelleştirmeleri hello düzeltme yöntemle veya hello Azure portal aracılığıyla uygulanabilir. Merhaba disk Bellenim güncelleştirmeleri kesintiye uğratan güncelleştirmelerin ve hello cihaz hello cihazın hello Windows PowerShell arabirimini kullanarak hello düzeltme yöntemle bakım modunda olduğunda uygulanır.

> [!IMPORTANT]
> * Elle ve otomatik ön denetimleri kümesini önceki toohello yükleme toodetermine hello cihaz durumunu donanım durumu ve ağ bağlantısı bakımından yapılır. Azure portal hello hello güncelleştirmeleri uygularsanız, bu ön denetimleri gerçekleştirilir.
> * Merhaba yazılım ve diğer düzenli güncelleştirmeler hello Azure portal aracılığıyla yüklemenizi öneririz. Merhaba Portalı'nda Hello güncelleştirme öncesi ağ geçidi denetimi başarısız olursa yalnızca toohello Windows PowerShell arabirimi hello aygıtının (tooinstall güncelleştirmeleri) gitmeniz gerekir. Gelen güncelleştirdiğiniz hello sürüm bağlı olarak, hello güncelleştirmeleri 4 saat sürebilir (veya daha büyük) tooinstall. Merhaba Bakım modu güncelleştirmeleri hello cihazın hello Windows PowerShell arabirimi yüklenmesi gerekir. Bakım modu kesintiye uğratan güncelleştirmelerdir gibi bu cihazınız için aşağı zaman sonuçlanır.
> * İsteğe bağlı StorSimple Snapshot Manager çalışan Merhaba, anlık görüntü Yöneticisi sürüm tooUpdate 5 önceki tooupdating hello Cihazınızı yükselttikten emin olun.


[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-5-via-hello-azure-portal"></a>Güncelleştirme 5'hello Azure portal yükleyin
Aşağıdaki adımları tooupdate hello Cihazınızı çok gerçekleştirmek[güncelleştirme 5](storsimple-update5-release-notes.md).

> [!NOTE]
> Microsoft hello aygıttan ek tanılama bilgilerinin çeker. Sonuç olarak, operations ekibimiz sorunlarınız aygıtları belirlediğinde, biz hello aygıttan daha iyi donanımlı toocollect bilgileri sorunlarını tanılamak ve.

[!INCLUDE [storsimple-8000-install-update4-via-portal](../../includes/storsimple-8000-install-update5-via-portal.md)]

Cihazınızı çalıştığından emin olun **StorSimple 8000 serisi güncelleştirme 5 (6.3.9600.17845)**. Merhaba **son tarih güncelleştirme** değiştirilmemelidir.

* Şimdi hello Bakım modu güncelleştirmelerin kullanılabilir olduğunu göreceksiniz (Bu ileti too24 saat yüklemeden sonra güncelleştirmeler hello için görüntülenen toobe devam edebilir). Bakım modu aygıt kapalı kalma sürelerine neden ve yalnızca aygıtınızın hello Windows PowerShell arabirimi uygulanabilir kesintiye uğratan güncelleştirmelerdir.

* Listelenen hello adımları kullanarak Hello Bakım modu güncelleştirmeleri karşıdan [toodownload düzeltmeleri](#to-download-hotfixes) için toosearch ve disk Bellenim güncelleştirmeleri yükler KB4011837 indirin (Merhaba diğer güncelleştirmeleri artık yüklü olması). Listelenen hello adımları [yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello Bakım modu güncelleştirmeler.

## <a name="install-update-5-as-a-hotfix"></a>Güncelleştirme 5 bir düzeltmenin yüklenmesi


Merhaba düzeltme yöntemini kullanarak yükseltilebilir hello yazılım sürümleri şunlardır:

* Güncelleştirme 0.1, 0.2, 0.3
* 1, 1.1 ve 1.2 güncelleştirmesi
* Güncelleştirme 2, 2.1, 2.2
* Güncelleştirme 3, 3.1
* Güncelleştirme 4

> [!NOTE] 
> Merhaba hello Azure portal güncelleştirme 5. yöntemi tooinstall önerilir. Merhaba ağ geçidi onay hello Azure portal aracılığıyla tooinstall hello güncelleştirmeleri çalışırken başarısız olursa bu yordamı kullanın. Merhaba denetimi tooa olmayan DATA 0 ağ arabirimindeki atanmış bir ağ geçidi varsa ve Cihazınızı güncelleştirme 1'den önceki bir yazılım sürümleri çalıştıran başarısız olur.

Merhaba düzeltme yöntemi hello aşağıdaki üç adımları içerir:

1. Merhaba düzeltmeleri hello Microsoft Update Kataloğu ' indirin.
2. Yükleyin ve hello normal modu düzeltmeleri doğrulayın.
3. Yükleyin ve hello Bakım modu düzeltme doğrulayın.

#### <a name="download-updates-for-your-device"></a>Cihazınız için güncelleştirmeleri karşıdan yükle

Merhaba aşağıdaki yükleyip gerekir belirlenen hello düzeltmeleri sipariş ve hello önerilen klasörler:

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |Klasöre yükleyin|
| --- | --- | --- | --- | --- | --- |
| 1. |KB4037264 |Yazılım güncelleştirmesi<br> Her ikisi de karşıdan _HcsSfotwareUpdate.exe_ ve _CisMSDAgent.exe_ |Normal <br></br>Olmayan kesintiye uğratan |~ 25 dakika |FirstOrderUpdate|

Güncelleştirme 4 çalıştıran bir CİHAZDAN güncelleştirme, ikinci sipariş güncelleştirmeler olarak yalnızca tooinstall hello OS toplu güncelleştirmeler gerekir.

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |Klasöre yükleyin|
| --- | --- | --- | --- | --- | --- |
| 2A. |KB4025336 |İşletim sistemi toplu güncelleştirmeler paketi <br> Windows Server 2012 R2 sürümünü karşıdan yükleyin |Normal <br></br>Olmayan kesintiye uğratan |- |SecondOrderUpdate|

Güncelleştirme 3'ü çalıştıran bir aygıttan yükleme veya önceki sürümleri, ayrıca şu toohello toplu güncelleştirmeleri hello yükleyin.

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |Klasöre yükleyin|
| --- | --- | --- | --- | --- | --- |
| 2B. |KB4011841 <br> KB4011842 |LSI sürücü ve bellenim güncelleştirmeleri <br> USM bellenim güncelleştirme (sürüm 3,38) |Normal <br></br>Olmayan kesintiye uğratan |~ 3 saat <br> (2A içerir. + 2B. + 2 C.)|SecondOrderUpdate|
| 2 C |KB3139398 <br> KB3142030 <br> KB3108381 <br> KB3153704 <br> KB3174644 <br> KB3139914   |İşletim sistemi güvenlik güncelleştirmeleri paketi <br> Windows Server 2012 R2 sürümünü karşıdan yükleyin |Normal <br></br>Olmayan kesintiye uğratan |- |SecondOrderUpdate|
| 2B. |KB3146621 <br> KB3103616 <br> KB3121261 <br> KB3123538 |İşletim sistemi güncelleştirmeleri paketi <br> Windows Server 2012 R2 sürümünü karşıdan yükleyin |Normal <br></br>Olmayan kesintiye uğratan |- |SecondOrderUpdate|


Önceki tabloların hello gösterilen tüm hello güncelleştirmeleri üstünde tooinstall disk Bellenim güncelleştirmeleri de gerekebilir. Merhaba çalıştırarak disk Bellenim güncelleştirmeleri hello olup olmadığını doğrulayabilirsiniz `Get-HcsFirmwareVersion` cmdlet'i. Bu bellenim sürümleri çalıştırıyorsanız: `XMGJ`, `XGEG`, `KZ50`, `F6C2`, `VR08`, `N003`, `0107`, sonra da bu güncelleştirmeler tooinstall gerekmez.

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati | Klasöre yükleyin|
| --- | --- | --- | --- | --- | --- |
| 3. |KB4037263 |Disk bellenim |Bakım <br></br>Kesintiye uğratan |~ 30 dakika | ThirdOrderUpdate |

<br></br>

> [!IMPORTANT]
> * Güncelleştirme 4'ten güncelleştirme, hello toplam yükleme saatini Kapat too4 saattir.
> * Bu yordam tooapply hello kullanmadan önce güncelleştirme, hem hello aygıt denetleyicileri çevrimiçi olduğundan ve tüm hello donanım bileşenleri sağlıklı olduğundan emin olun.

Aşağıdaki adımları toodownload hello gerçekleştirin ve hello düzeltmeyi yükleyin.

[!INCLUDE [storsimple-install-update5-hotfix](../../includes/storsimple-install-update5-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [güncelleştirme 5 yayın](storsimple-update5-release-notes.md).

