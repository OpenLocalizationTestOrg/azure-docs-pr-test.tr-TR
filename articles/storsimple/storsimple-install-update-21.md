---
title: "StorSimple Cihazınızda aaaInstall güncelleştirme 2.2 | Microsoft Docs"
description: "Açıklar nasıl tooinstall StorSimple 8000 serisi güncelleştirme 2.2, StorSimple 8000 serisi Cihazınızda."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 047c7a4b-73d0-45ea-8d51-c54d71871392
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/02/2016
ms.author: alkohli
ms.openlocfilehash: cedb83ce42bc6bb81a4e43345da3f25b71036d1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-22-on-your-storsimple-device"></a>StorSimple Cihazınızda güncelleştirme 2.2 yükleyin
## <a name="overview"></a>Genel Bakış
Bu öğretici tooinstall güncelleştirme 2.2 aracılığıyla önceki bir yazılım sürümünü çalıştıran bir StorSimple cihazda nasıl hello Klasik Azure portalı ve hello düzeltme yöntemini kullanarak açıklanmaktadır. Merhaba düzeltme yöntemi, bir ağ arabiriminde hello StorSimple cihazı veri 0 dışında bir ağ geçidi yapılandırıldığında ve bir güncelleştirme öncesi 1 yazılımı sürümünden tooupdate çalıştığınız kullanılır.

Güncelleştirme 2.2 aygıt yazılımı, WMI ve iSCSI güncelleştirmeleri içerir. Sürüm 2.1 güncelleştirme, yalnızca hello aygıt yazılım güncelleştirmesi uygulanan toobe gerekir. Bir güncelleştirme öncesi 2 sürümden güncelleştirme, gerekli tooapply LSI sürücü, Spaceport, Storport ve disk Bellenim güncelleştirmeleri olacaktır. Merhaba aygıt yazılımı, WMI, iSCSI, LSI sürücü, Spaceport ve Storport düzeltmeleri benzer güncelleştirmeleri ve hello Klasik Azure portalı uygulanabilir. Merhaba disk Bellenim güncelleştirmeleri kesintiye uğratan güncelleştirmelerin ve yalnızca hello cihazın hello Windows PowerShell arabirimi uygulanabilir. 

> [!IMPORTANT]
> * Elle ve otomatik ön denetimleri kümesini önceki toohello yükleme toodetermine hello cihaz durumunu donanım durumu ve ağ bağlantısı bakımından yapılır. Klasik Azure portalı hello hello güncelleştirmeleri uygularsanız, bu ön denetimleri gerçekleştirilir.
> * Merhaba yazılım yüklemek ve klasik Azure Portalı aracılığıyla sürücü güncelleştirmelerini hello öneririz. Merhaba Portalı'nda Hello güncelleştirme öncesi ağ geçidi denetimi başarısız olursa yalnızca toohello Windows PowerShell arabirimi hello aygıtının (tooinstall güncelleştirmeleri) gitmeniz gerekir. Güncelleştirmekte olduğunuz hello sürümüne bağlı olarak, hello güncelleştirmeleri 1.5-2.5 saatleri tooinstall sürebilir. Merhaba Bakım modu güncelleştirmeleri hello cihazın hello Windows PowerShell arabirimi yüklenmesi gerekir. Bakım modu kesintiye uğratan güncelleştirmelerdir gibi bunlar, cihazınız için aşağı zaman neden olur.
> * İsteğe bağlı StorSimple Snapshot Manager çalışan Merhaba, anlık görüntü Yöneticisi sürüm tooUpdate 2.2 önceki tooupdating hello Cihazınızı yükselttikten emin olun.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-22-via-hello-azure-classic-portal"></a>Güncelleştirme 2.2 hello Klasik Azure portalı yükleyin
Aşağıdaki adımları tooupdate hello Cihazınızı çok gerçekleştirmek[güncelleştirme 2.2](storsimple-update21-release-notes.md).

> [!NOTE]
> Daha sonra (de dahil olmak üzere güncelleştirme 2.1) veya güncelleştirme 2 uyguluyorsanız Microsoft mümkün toopull ek tanılama bilgilerinin hello aygıttan olacaktır. Sonuç olarak, operations ekibimiz sorunlarınız aygıtları belirlediğinde, biz hello aygıttan daha iyi donanımlı toocollect bilgileri sorunlarını tanılamak ve. Güncelleştirme 2 veya sonrası kabul ederek, bize tooprovide izin bu öngörülü desteği.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Cihazınızı çalıştığından emin olun **StorSimple 8000 serisi güncelleştirme 2.2 (6.3.9600.17708)**. Merhaba **son tarih güncelleştirme** değiştirilmeleri. 
   
   Bir sürüm önceki tooUpdate 2 güncelleştiriyorsanız ayrıca hello Bakım modu güncelleştirmelerin kullanılabilir olduğunu göreceksiniz (Bu ileti too24 saat yüklemeden sonra güncelleştirmeler hello için görüntülenen toobe devam edebilir).
   
   Bakım modu aygıt kapalı kalma sürelerine neden ve yalnızca aygıtınızın hello Windows PowerShell arabirimi uygulanabilir kesintiye uğratan güncelleştirmelerdir. Bazı durumlarda Güncelleştirme 1.2 çalıştırırken, disk bellenim zaten güncel olabilir, tooinstall gerekmez; bu durumda herhangi bir Bakım modu güncelleştirir.
   
   Güncelleştirme 2'den güncelleştiriyorsanız, cihazınız artık güncel olması gerekir. Merhaba kalan adımları atlayabilirsiniz.
2. Listelenen hello adımları kullanarak Hello Bakım modu güncelleştirmeleri karşıdan [toodownload düzeltmeleri](#to-download-hotfixes) için toosearch ve disk Bellenim güncelleştirmeleri yükler KB3121899 indirin (Merhaba diğer güncelleştirmeleri artık yüklü olması).
3. Listelenen hello adımları [yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes) tooinstall hello Bakım modu güncelleştirmeler. 

## <a name="install-update-22-as-a-hotfix"></a>Güncelleştirme 2.2 bir düzeltmenin yüklenmesi
Merhaba ağ geçidi onay hello Klasik Azure Portalı aracılığıyla tooinstall hello güncelleştirmeleri çalışırken başarısız olursa bu yordamı kullanın. Merhaba denetimi tooa olmayan DATA 0 ağ arabirimindeki atanmış bir ağ geçidine sahip ve Cihazınızı bir yazılım sürüm önceki tooUpdate 1 çalıştığından başarısız olur.

Merhaba düzeltme yöntemini kullanarak yükseltilebilir hello yazılım sürümleri şunlardır:

* Güncelleştirme 0.1, 0.2, 0.3
* 1, 1.1 ve 1.2 güncelleştirmesi
* Güncelleştirme 2, 2.1 

> [!IMPORTANT]
> * Cihazınızı sürüm (GA) sürümünü çalıştırıyorsa, temasa [Microsoft Support](storsimple-contact-microsoft-support.md) tooassist hello ile güncelleştirin.
> 
> 

Merhaba düzeltme yöntemi hello aşağıdaki üç adımları içerir:

* Merhaba düzeltmeleri hello Microsoft Update Kataloğu ' indirin.
* Yükleyin ve hello normal modu düzeltmeleri doğrulayın.
* Yükleyin ve hello Bakım modu düzeltme (yalnızca güncelleştirme öncesi 2 yazılımlardan güncelleştirirken) doğrulayın.

#### <a name="download-updates-for-a-device-running-update-21-software"></a>Güncelleştirme 2.1 yazılımı çalıştıran bir aygıt için güncelleştirmeleri karşıdan yükle
**Cihazınızı güncelleştirme 2.1 çalışıyorsa,**, yalnızca hello aygıt yazılım güncelleştirmesi KB3179904 indirmeniz gerekir. Yalnızca 'tüm-hcsmdssoftwareudpate' ile başlayan hello ikili dosya yükleyin. Merhaba CIS yüklemeyin ve hello MDS aracı güncelleştirmesi başında ile `all-cismdsagentupdatebundle`. Hata toodo şekilde bir hatayla sonuçlanır. Bu benzer bir güncelleştirmedir, GÇ değil kesintiye ve hello aygıt kapalı kalma süresi sahip değil.

#### <a name="download-updates-for-a-device-running-update-2-software"></a>Yazılım güncelleştirme 2 çalıştıran bir cihazda güncelleştirmeleri yükle
**Cihazınızı güncelleştirme 2 çalışıyorsa,**, sipariş belirlenen hello düzeltmeleri aşağıdaki hello yükleyip gerekir:

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |
| --- | --- | --- | --- | --- |
| 1. |KB3179904 |Yazılım güncelleştirme & #42; |Normal <br></br>Olmayan kesintiye uğratan |~ 45 dakika |
| 2. |KB3146621 |iSCSI paketi |Normal <br></br>Olmayan kesintiye uğratan |~ 20 dakika |
| 3. |KB3103616 |WMI paketi |Normal <br></br>Olmayan kesintiye uğratan |~ 12 dakika |

 & #42;  *Not, yazılım güncelleştirmesi iki ikili dosyaları oluşur: aygıt yazılım güncelleştirmesi başında ile `all-hcsmdssoftwareupdate` ve CIS hello ve Mds Aracısı başında ile `all-cismdsagentupdatebundle`. hello aygıt bir yazılım güncelleştirmesi önce hello CIS ve Mds aracısı yüklü olmalıdır. Merhaba etkin denetleyicisi hello aracılığıyla yeniden başlatmalısınız `Restart-HcsController` cmdlet hello CIS ve MDS aracı güncelleştirme uygulandıktan sonra (ve güncelleştirmeleri kalan hello uygulanmadan önce).* 

#### <a name="download-updates-for-a-device-running-pre-update-2-software"></a>Güncelleştirme öncesi 2 yazılımı çalıştıran bir aygıt için güncelleştirmeleri karşıdan yükle
**Cihazınızı 0.2, 0.3, 1.0 ve 1.1 sürümleri çalışıyorsa**, karşıdan yüklemeniz gerekir ve yükleme hello LSI sürücü ve bellenim güncelleştirme ayrıca toohello yazılım, iSCSI ve WMI güncelleştirmeler. Güncelleştirme 1.2 veya 2 çalıştırıyorsanız bu güncelleştirme zaten yüklü. 

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |
| --- | --- | --- | --- | --- |
| 4. |KB3121900 |LSI sürücü ve bellenim |Normal <br></br>Olmayan kesintiye uğratan |~ 20 dakika |

<br></br>
**Cihazınızı sürümleri 0.2, 0.3, 1.0, 1.1 ve 1.2 çalışıyorsa,**, indirin ve hello Spaceport ve hello Storport düzeltme yüklemeniz gerekir. Güncelleştirme 2 çalıştırıyorsanız, bunlar zaten yüklü.

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |
| --- | --- | --- | --- | --- |
| 5. |KB3090322 |Spaceport düzeltme </br> Windows Server 2012 R2 |Normal <br></br>Olmayan kesintiye uğratan |~ 20 dakika |
| 6. |KB3080728 |Storport düzeltme </br> Windows Server 2012 R2 |Normal <br></br>Olmayan kesintiye uğratan |~ 20 dakika |

<br></br>
Tooinstall disk Bellenim güncelleştirmeleri de gerekebilir. Merhaba çalıştırarak disk Bellenim güncelleştirmeleri hello olup olmadığını doğrulayabilirsiniz `Get-HcsFirmwareVersion` cmdlet'i. Bu bellenim sürümleri çalıştırıyorsanız: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, sonra da bu güncelleştirmeler tooinstall gerekmez.

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |
| --- | --- | --- | --- | --- |
| 7. |KB3121899 |Disk bellenim |Bakım <br></br>Kesintiye uğratan |~ 30 dakika |

<br></br>

> [!IMPORTANT]
> * Bu yordam gereksinimlerini toobe tooapply güncelleştirme 2.2 yalnızca bir kez gerçekleştirilir. Hello Azure Klasik portalı tooapply sonraki güncelleştirmeler kullanabilirsiniz.
> * Güncelleştirme 2'den güncelleştirme, hello toplam yükleme saatini Kapat too1.5 saattir.
> * Bu yordam tooapply hello kullanmadan önce güncelleştirme, hem hello aygıt denetleyicileri çevrimiçi olduğundan ve tüm hello donanım bileşenleri sağlıklı olduğundan emin olun.
> 
> 

Aşağıdaki adımları toodownload hello gerçekleştirin ve hello düzeltmeyi yükleyin.

[!INCLUDE [storsimple-install-update21-hotfix](../../includes/storsimple-install-update21-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Sonraki adımlar
Merhaba hakkında daha fazla bilgi [güncelleştirme 2.1 yayın](storsimple-update21-release-notes.md).

