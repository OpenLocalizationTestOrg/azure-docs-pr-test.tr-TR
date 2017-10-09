---
title: "StorSimple Cihazınızda aaaInstall güncelleştirme 3 | Microsoft Docs"
description: "Açıklar nasıl tooinstall StorSimple 8000 serisi güncelleştirme 3'ü, StorSimple 8000 serisi Cihazınızda."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c6c4634d-4f3a-4bc4-b307-a22bf18664e1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a156b8919639f1c7afb0fdef3d882d40d48f1c48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-3-on-your-storsimple-8000-series-device"></a>StorSimple 8000 serisi aygıtınızda güncelleştirme 3'ü yükleme

## <a name="overview"></a>Genel Bakış

Bu öğretici tooinstall güncelleştirme 3'ü aracılığıyla önceki bir yazılım sürümünü çalıştıran bir StorSimple cihazda nasıl hello Klasik Azure portalı ve hello düzeltme yöntemini kullanarak açıklanmaktadır. Merhaba düzeltme yöntemi, bir ağ arabiriminde hello StorSimple cihazı veri 0 dışında bir ağ geçidi yapılandırıldığında ve bir güncelleştirme öncesi 1 yazılımı sürümünden tooupdate çalıştığınız kullanılır.

Güncelleştirme 3 aygıt yazılımı, LSI sürücü ve bellenim, Storport içerir ve Spaceport güncelleştirir. Güncelleştirme 2 veya daha önceki bir sürümünden güncelleştirme varsa, ayrıca gerekli tooapply iSCSI, WMI, olması ve bellenim güncelleştirmeleri belirli durumlarda, disk. Merhaba aygıt yazılımı, WMI, iSCSI, LSI sürücü, Spaceport ve Storport düzeltmeleri benzer güncelleştirmeleri ve hello Klasik Azure portalı uygulanabilir. Merhaba disk Bellenim güncelleştirmeleri kesintiye uğratan güncelleştirmelerin ve yalnızca hello cihazın hello Windows PowerShell arabirimi uygulanabilir. 

> [!IMPORTANT]
> * Elle ve otomatik ön denetimleri kümesini önceki toohello yükleme toodetermine hello cihaz durumunu donanım durumu ve ağ bağlantısı bakımından yapılır. Klasik Azure portalı hello hello güncelleştirmeleri uygularsanız, bu ön denetimleri gerçekleştirilir.
> * Merhaba yazılım yüklemek ve klasik Azure Portalı aracılığıyla sürücü güncelleştirmelerini hello öneririz. Merhaba Portalı'nda Hello güncelleştirme öncesi ağ geçidi denetimi başarısız olursa yalnızca toohello Windows PowerShell arabirimi hello aygıtının (tooinstall güncelleştirmeleri) gitmeniz gerekir. Güncelleştirmekte olduğunuz hello sürümüne bağlı olarak, hello güncelleştirmeleri 1.5-2.5 saatleri tooinstall sürebilir. Merhaba Bakım modu güncelleştirmeleri hello cihazın hello Windows PowerShell arabirimi yüklenmesi gerekir. Bakım modu kesintiye uğratan güncelleştirmelerdir gibi bunlar, cihazınız için aşağı zaman neden olur.
> * İsteğe bağlı StorSimple Snapshot Manager çalışan Merhaba, anlık görüntü Yöneticisi sürüm 2 tooUpdate önceki tooupdating hello Cihazınızı yükselttikten emin olun.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-3-via-hello-azure-classic-portal"></a>Merhaba Klasik Azure portalı güncelleştirme 3'ü yükleme
Aşağıdaki adımları tooupdate hello Cihazınızı çok gerçekleştirmek[güncelleştirme 3'ü](storsimple-update3-release-notes.md).

> [!NOTE]
> Daha sonra (de dahil olmak üzere güncelleştirme 2.1) veya güncelleştirme 2 uyguluyorsanız Microsoft mümkün toopull ek tanılama bilgilerinin hello aygıttan olacaktır. Sonuç olarak, operations ekibimiz sorunlarınız aygıtları belirlediğinde, biz hello aygıttan daha iyi donanımlı toocollect bilgileri sorunlarını tanılamak ve. Güncelleştirme 2 veya sonrası kabul ederek, bize tooprovide izin bu öngörülü desteği.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

Cihazınızı çalıştığından emin olun **StorSimple 8000 serisi güncelleştirme 3'ü (6.3.9600.17759)**. Merhaba **son tarih güncelleştirme** değiştirilmeleri. 
   - Bir sürüm önceki tooUpdate 2 güncelleştiriyorsanız ayrıca hello Bakım modu güncelleştirmelerin kullanılabilir olduğunu göreceksiniz (Bu ileti too24 saat yüklemeden sonra güncelleştirmeler hello için görüntülenen toobe devam edebilir).
     Bakım modu aygıt kapalı kalma sürelerine neden ve yalnızca aygıtınızın hello Windows PowerShell arabirimi uygulanabilir kesintiye uğratan güncelleştirmelerdir. Bazı durumlarda Güncelleştirme 1.2 çalıştırırken, disk bellenim zaten güncel olabilir, tooinstall gerekmez; bu durumda herhangi bir Bakım modu güncelleştirir.
   - Güncelleştirme güncelleştirme 2 veya sonrası, cihazınız artık güncel olması gerekir. Merhaba sonraki adımı atlayabilirsiniz.

Listelenen hello adımları kullanarak Hello Bakım modu güncelleştirmeleri karşıdan [toodownload düzeltmeleri](#to-download-hotfixes) için toosearch ve disk Bellenim güncelleştirmeleri yükler KB3121899 indirin (Merhaba diğer güncelleştirmeleri artık yüklü olması). Listelenen hello adımları [yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello Bakım modu güncelleştirmeler. 

## <a name="install-update-3-as-a-hotfix"></a>Bir düzeltme olarak güncelleştirme 3'ü yükleme
Merhaba ağ geçidi onay hello Klasik Azure Portalı aracılığıyla tooinstall hello güncelleştirmeleri çalışırken başarısız olursa bu yordamı kullanın. Merhaba denetimi tooa olmayan DATA 0 ağ arabirimindeki atanmış bir ağ geçidine sahip ve Cihazınızı bir yazılım sürüm önceki tooUpdate 1 çalıştığından başarısız olur.

Merhaba düzeltme yöntemini kullanarak yükseltilebilir hello yazılım sürümleri şunlardır:

* Güncelleştirme 0.1, 0.2, 0.3
* 1, 1.1 ve 1.2 güncelleştirmesi
* Güncelleştirme 2, 2.1, 2.2 

> [!IMPORTANT]
> * Cihazınızı sürüm (GA) sürümünü çalıştırıyorsa, temasa [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist hello ile güncelleştirin.
> 
> 

Merhaba düzeltme yöntemi hello aşağıdaki üç adımları içerir:

1. Merhaba düzeltmeleri hello Microsoft Update Kataloğu ' indirin.
2. Yükleyin ve hello normal modu düzeltmeleri doğrulayın.
3. Yükleyin ve hello Bakım modu düzeltme (yalnızca güncelleştirme öncesi 2 yazılımlardan güncelleştirirken) doğrulayın.

#### <a name="download-updates-for-your-device"></a>Cihazınız için güncelleştirmeleri karşıdan yükle
**Cihazınızı güncelleştirme 2.1 veya 2.2 çalışıyorsa,**, sipariş belirlenen hello düzeltmeleri aşağıdaki hello yükleyip gerekir:

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |
| --- | --- | --- | --- | --- |
| 1. |KB3186843 |Yazılım güncelleştirme &#42; |Normal <br></br>Olmayan kesintiye uğratan |~ 45 dakika |
| 2. |KB3186859 |LSI sürücü ve bellenim |Normal <br></br>Olmayan kesintiye uğratan |~ 20 dakika |
| 3. |KB3121261 |Storport ve Spaceport düzeltme </br> Windows Server 2012 R2 |Normal <br></br>Olmayan kesintiye uğratan |~ 20 dakika |

&#42;  *Bu hello yazılım güncelleştirmesi oluşan iki ikili dosyaları Not: aygıt yazılım güncelleştirmesi başında ile `all-hcsmdssoftwareupdate` ve CIS hello ve Mds Aracısı başında ile `all-cismdsagentupdatebundle`. hello CIS ve Mds önce hello aygıt bir yazılım güncelleştirmesi yüklü olmalıdır Aracı. Merhaba etkin denetleyicisi hello aracılığıyla yeniden başlatmalısınız `Restart-HcsController` cmdlet hello CIS ve Mds aracı güncelleştirme uygulandıktan sonra (ve güncelleştirmeleri kalan hello uygulanmadan önce).* 

**Cihazınızı güncelleştirme 0.1, 0.2, 0.3, 1.0, 1.1, 1.2 veya 2.0 çalışıp çalışmadığını**, toplama toohello yazılım, LSI sürücü düzeltmeleri aşağıdaki hello yükleyip gerekir ve bellenim güncelleştirmeleri (gösterildiği hello tablo önceki), sipariş belirlenen hello:

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |
| --- | --- | --- | --- | --- |
| 4. |KB3146621 |iSCSI paketi |Normal <br></br>Olmayan kesintiye uğratan |~ 20 dakika |
| 5. |KB3103616 |WMI paketi |Normal <br></br>Olmayan kesintiye uğratan |~ 12 dakika |

<br></br>

**Cihazınızı sürümleri 0.2, 0.3, 1.0, 1.1 ve 1.2 çalışıyorsa,**, önceki tabloların hello gösterilen tüm hello güncelleştirmeleri üstünde tooinstall disk Bellenim güncelleştirmeleri de gerekebilir. Merhaba çalıştırarak disk Bellenim güncelleştirmeleri hello olup olmadığını doğrulayabilirsiniz `Get-HcsFirmwareVersion` cmdlet'i. Bu bellenim sürümleri çalıştırıyorsanız: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, sonra da bu güncelleştirmeler tooinstall gerekmez.

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |
| --- | --- | --- | --- | --- |
| 6. |KB3121899 |Disk bellenim |Bakım <br></br>Kesintiye uğratan |~ 30 dakika |

<br></br>

> [!IMPORTANT]
> * Bu yordam gereksinimlerini toobe tooapply güncelleştirme 3'ü yalnızca bir kez gerçekleştirilir. Hello Azure Klasik portalı tooapply sonraki güncelleştirmeler kullanabilirsiniz.
> * Güncelleştirme 2.2 güncelleştirme, hello toplam yükleme saatini Kapat too1.1 saattir.
> * Bu yordam tooapply hello kullanmadan önce güncelleştirme, hem hello aygıt denetleyicileri çevrimiçi olduğundan ve tüm hello donanım bileşenleri sağlıklı olduğundan emin olun.
> 
> 

Aşağıdaki adımları toodownload hello gerçekleştirin ve hello düzeltmeyi yükleyin.

[!INCLUDE [storsimple-install-update3-hotfix](../../includes/storsimple-install-update3-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [güncelleştirme 3 Sürüm](storsimple-update3-release-notes.md).

