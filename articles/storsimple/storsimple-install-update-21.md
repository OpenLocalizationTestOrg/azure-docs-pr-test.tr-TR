---
title: "StorSimple Cihazınızda güncelleştirme 2.2 yükleme | Microsoft Docs"
description: "StorSimple 8000 serisi güncelleştirme 2.2 StorSimple 8000 serisi cihazınıza yüklediğiniz açıklanmaktadır."
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
ms.openlocfilehash: c60b4de88d60f0373d69fe2f3cee5ccf888b8d8c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-update-22-on-your-storsimple-device"></a>StorSimple Cihazınızda güncelleştirme 2.2 yükleyin
## <a name="overview"></a>Genel Bakış
Bu öğretici, Klasik Azure portalı önceki yazılım sürümleri çalıştıran ve düzeltme yöntemini kullanarak bir StorSimple cihazında güncelleştirme 2.2 yüklemeye açıklanmaktadır. Düzeltme yöntemi, bir ağ arabiriminde StorSimple cihaz veri 0 dışında bir ağ geçidi yapılandırıldığında ve bir güncelleştirme öncesi 1 yazılımı sürümü güncelleştirmeye çalıştığınız kullanılır.

Güncelleştirme 2.2 aygıt yazılımı, WMI ve iSCSI güncelleştirmeleri içerir. Sürüm 2.1 güncelleştirme, yalnızca cihaz yazılım güncelleştirme uygulanması gerekir. Bir güncelleştirme öncesi 2 sürümden güncelleştirme varsa, aynı zamanda LSI sürücü, Spaceport, Storport ve disk Bellenim güncelleştirmeleri uygulamak için gerekir. Aygıt yazılımı, WMI, iSCSI, LSI sürücü, Spaceport ve Storport düzeltmeleri benzer güncelleştirmeleri ve klasik Azure portalı uygulanabilir. Disk Bellenim güncelleştirmeleri kesintiye uğratan güncelleştirmelerin ve yalnızca aygıt Windows PowerShell arabirimi uygulanabilir. 

> [!IMPORTANT]
> * Elle ve otomatik ön denetimleri kümesini donanım durumu ve ağ bağlantısı bakımından cihaz durumunu belirlemek için yükleme öncesinde gerçekleştirilir. Klasik Azure portalından güncelleştirmeleri uygularsanız, bu ön denetimleri gerçekleştirilir.
> * Klasik Azure Portalı aracılığıyla yazılım ve sürücü güncelleştirmelerini yüklemenizi öneririz. Portalda güncelleştirme öncesi ağ geçidi denetimi başarısız olursa (güncelleştirmeleri yüklemek için) cihazın Windows PowerShell arabirimine yalnızca gitmeniz gerekir. Güncelleştirmekte olduğunuz sürümüne bağlı olarak, güncelleştirmeleri yüklemek için 1.5-2.5 saat sürebilir. Bakım modu güncelleştirmeleri aygıtı Windows PowerShell arabirimi yüklenmesi gerekir. Bakım modu kesintiye uğratan güncelleştirmelerdir gibi bunlar, cihazınız için aşağı zaman neden olur.
> * İsteğe bağlı StorSimple Snapshot Manager çalışıyorsa, anlık görüntü Yöneticisi'ni sürümünüz için güncelleştirme 2.2 aygıtı güncelleştirme önce yükselttikten emin olun.
> 
> 

[!INCLUDE [storsimple-preparing-for-update](../../includes/storsimple-preparing-for-updates.md)]

## <a name="install-update-22-via-the-azure-classic-portal"></a>Güncelleştirme 2.2 Azure Klasik portalı üzerinden yükleyin
İçin Cihazınızı güncelleştirmek için aşağıdaki adımları gerçekleştirin [güncelleştirme 2.2](storsimple-update21-release-notes.md).

> [!NOTE]
> Daha sonra (de dahil olmak üzere güncelleştirme 2.1) veya güncelleştirme 2 uyguluyorsanız Microsoft aygıttan ek tanılama bilgilerini mümkün olacaktır. Sorunlarınız aygıtları operations ekibimiz belirlediğinde, sonuç olarak, daha iyi aygıttan bilgi toplamak ve sorunları tanılamak donanımlı duyuyoruz. Güncelleştirme 2 veya sonrası kabul ederek, bize bu öngörülü desteği sağlamak izin verir.
> 
> 

[!INCLUDE [storsimple-install-update2-via-portal](../../includes/storsimple-install-update2-via-portal.md)]

1. Cihazınızı çalıştığından emin olun **StorSimple 8000 serisi güncelleştirme 2.2 (6.3.9600.17708)**. **Son tarih güncelleştirme** değiştirilmeleri. 
   
   Güncelleştirme 2 önce bir sürümünden güncelleştiriyorsanız, ayrıca Bakım modu güncelleştirmelerinin kullanılabilir olduğunu göreceksiniz (Bu ileti 24 güncelleştirmeleri yükledikten sonra saate kadar gösterilmeye devam).
   
   Bakım modu aygıt kapalı kalma sürelerine neden ve Cihazınızı Windows PowerShell arabirimi yalnızca uygulanabilir kesintiye uğratan güncelleştirmelerdir. Bazı durumlarda Güncelleştirme 1.2 çalıştırırken, disk bellenim zaten güncel herhangi bir Bakım modu güncelleştirme yüklemeniz gerekmez; bu durumda olabilir.
   
   Güncelleştirme 2'den güncelleştiriyorsanız, cihazınız artık güncel olması gerekir. Geri kalan adımları atlayabilirsiniz.
2. Bakım modu listelenen adımları kullanarak güncelleştirmeler [düzeltmeleri indirmek için](#to-download-hotfixes) aramak ve KB3121899, (diğer güncelleştirmeleri zaten yüklenmesi gerekir artık) hangi yükler disk Bellenim güncelleştirmeleri karşıdan yüklemek için.
3. Listelenen adımları izleyin [yükleme ve Bakım modu düzeltmeleri doğrulama](#to-install-and-verify-maintenance-mode-hotfixes) Bakım modu yüklemek için güncelleştirir. 

## <a name="install-update-22-as-a-hotfix"></a>Güncelleştirme 2.2 bir düzeltmenin yüklenmesi
Ağ geçidi onay Klasik Azure Portalı aracılığıyla güncelleştirmeleri yüklenmeye çalışırken başarısız olursa bu yordamı kullanın. Bir veri dışı 0 ağ arabirimine atanmış bir ağ geçidine sahip ve Cihazınızı yazılım sürümü güncelleştirme 1 önce çalışan denetimi başarısız olur.

Düzeltme yöntemini kullanarak yükseltilebilir yazılım sürümleri şunlardır:

* Güncelleştirme 0.1, 0.2, 0.3
* 1, 1.1 ve 1.2 güncelleştirmesi
* Güncelleştirme 2, 2.1 

> [!IMPORTANT]
> * Cihazınızı sürüm (GA) sürümünü çalıştırıyorsa, temasa [Microsoft Support](storsimple-contact-microsoft-support.md) güncelleştirmeyle yardımcı olmak için.
> 
> 

Düzeltme yöntemi aşağıdaki üç adımdan oluşur:

* Düzeltmeleri Microsoft Update Kataloğu'ndan indirin.
* Yükleyin ve normal modu düzeltmeleri doğrulayın.
* Yükleme ve Bakım modu düzeltme (yalnızca güncelleştirme öncesi 2 yazılımlardan güncelleştirirken) doğrulayın.

#### <a name="download-updates-for-a-device-running-update-21-software"></a>Güncelleştirme 2.1 yazılımı çalıştıran bir aygıt için güncelleştirmeleri karşıdan yükle
**Cihazınızı güncelleştirme 2.1 çalışıyorsa,**, yalnızca cihaz yazılım güncelleştirmesi KB3179904 indirmeniz gerekir. Yalnızca 'tüm-hcsmdssoftwareudpate' ile başlayan ikili dosya yükleyin. CI yüklemeyin ve MDS aracı güncelleştirmesi başında `all-cismdsagentupdatebundle`. Bunun Sağlanamaması bir hatayla sonuçlanır. Bu benzer bir güncelleştirmedir, GÇ değil kesintiye ve cihaz kapalı kalma süresi sahip değil.

#### <a name="download-updates-for-a-device-running-update-2-software"></a>Yazılım güncelleştirme 2 çalıştıran bir cihazda güncelleştirmeleri yükle
**Cihazınızı güncelleştirme 2 çalışıyorsa,**, indirin ve belirtilen sırayla aşağıdaki düzeltmeleri yüklemeniz gerekir:

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |
| --- | --- | --- | --- | --- |
| 1. |KB3179904 |Yazılım güncelleştirme &#42; |Normal <br></br>Olmayan kesintiye uğratan |~ 45 dakika |
| 2. |KB3146621 |iSCSI paketi |Normal <br></br>Olmayan kesintiye uğratan |~ 20 dakika |
| 3. |KB3103616 |WMI paketi |Normal <br></br>Olmayan kesintiye uğratan |~ 12 dakika |

 &#42;  *Not, yazılım güncelleştirmesi iki ikili dosyaları oluşur: aygıt yazılım güncelleştirmesi başında ile `all-hcsmdssoftwareupdate` ve ile başlayan CIS ve Mds Aracısı `all-cismdsagentupdatebundle`. Aygıt yazılım güncelleştirmesi önce CIS ve Mds aracısı yüklü olmalıdır. Etkin denetleyicisi aracılığıyla yeniden başlatmalısınız `Restart-HcsController` CIS ve MDS Aracısı uyguladıktan sonra cmdlet güncelleştirme (ve bir kalan uygulama güncelleştirmeleri önce).* 

#### <a name="download-updates-for-a-device-running-pre-update-2-software"></a>Güncelleştirme öncesi 2 yazılımı çalıştıran bir aygıt için güncelleştirmeleri karşıdan yükle
**Cihazınızı 0.2, 0.3, 1.0 ve 1.1 sürümleri çalışıyorsa**karşıdan yüklemeniz gerekir ve yükleme LSI sürücü ve bellenim güncelleştirmeleri güncelleştirme yazılım, iSCSI ve WMI yanı sıra. Güncelleştirme 1.2 veya 2 çalıştırıyorsanız bu güncelleştirme zaten yüklü. 

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |
| --- | --- | --- | --- | --- |
| 4. |KB3121900 |LSI sürücü ve bellenim |Normal <br></br>Olmayan kesintiye uğratan |~ 20 dakika |

<br></br>
**Cihazınızı sürümleri 0.2, 0.3, 1.0, 1.1 ve 1.2 çalışıyorsa,**, indirin ve Spaceport ve Storport düzeltmeyi yüklemeniz gerekir. Güncelleştirme 2 çalıştırıyorsanız, bunlar zaten yüklü.

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |
| --- | --- | --- | --- | --- |
| 5. |KB3090322 |Spaceport düzeltme </br> Windows Server 2012 R2 |Normal <br></br>Olmayan kesintiye uğratan |~ 20 dakika |
| 6. |KB3080728 |Storport düzeltme </br> Windows Server 2012 R2 |Normal <br></br>Olmayan kesintiye uğratan |~ 20 dakika |

<br></br>
Disk Bellenim güncelleştirmeleri yüklemeniz gerekebilir. Disk Bellenim güncelleştirmeleri çalıştırarak gerekmediğini doğrulayabilirsiniz `Get-HcsFirmwareVersion` cmdlet'i. Bu bellenim sürümleri çalıştırıyorsanız: `XMGG`, `XGEG`, `KZ50`, `F6C2`, `VR08`, sonra da bu güncelleştirmeleri yüklemek gerekmez.

| Sırası | KB | Açıklama | Güncelleştirme türü | Yükleme saati |
| --- | --- | --- | --- | --- |
| 7. |KB3121899 |Disk bellenim |Bakım <br></br>Kesintiye uğratan |~ 30 dakika |

<br></br>

> [!IMPORTANT]
> * Bu yordamı güncelleştirme 2.2 uygulamak için yalnızca bir kez gerçekleştirilmesi gerekir. Sonraki güncelleştirmeleri uygulamak için Klasik Azure portalını kullanabilirsiniz.
> * Toplam yükleme saatini güncelleştirme 2'den güncelleştirme, yakın 1,5 saattir.
> * Güncelleştirmeyi uygulamak için bu yordamı kullanmadan önce hem aygıt denetleyicileri çevrimiçi olduğundan ve tüm donanım bileşenleri sağlıklı olduğundan emin olun.
> 
> 

Karşıdan yüklemek ve düzeltmeleri yüklemek için aşağıdaki adımları gerçekleştirin.

[!INCLUDE [storsimple-install-update21-hotfix](../../includes/storsimple-install-update21-hotfix.md)]

[!INCLUDE [storsimple-install-troubleshooting](../../includes/storsimple-install-troubleshooting.md)]

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [güncelleştirme 2.1 yayın](storsimple-update21-release-notes.md).

