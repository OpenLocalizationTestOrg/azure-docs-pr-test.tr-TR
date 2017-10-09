---
title: "Veri 0 aaaModify StorSimple 8000 serisi cihazın ayarlarının | Microsoft Docs"
description: "Bilgi nasıl StorSimple tooreconfigure için Windows PowerShell toouse hello DATA 0 ağ arabirimindeki, StorSimple Cihazınızda."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2017
ms.author: alkohli
ms.openlocfilehash: 2d3bdd3675017be86def45a81d94b6c03fc61da6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-data-0-network-interface-settings-on-your-storsimple-8000-series-device"></a>StorSimple 8000 serisi aygıtınızda Hello veri 0 ağ arabirimi ayarlarını değiştirme

## <a name="overview"></a>Genel Bakış

Microsoft Azure StorSimple Cihazınızı veri 0'dan altı ağ arabirimi bulunur tooDATA 5. Merhaba arabirimi daima hello Windows PowerShell arabirimi veya hello seri Konsolu yapılandırılır ve otomatik olarak bulut etkindir veri 0. DATA 0 ağ arabirimindeki hello Azure portal aracılığıyla yapılandıramayacağınızı unutmayın.

Merhaba DATA 0 arabirimi, ilk hello Kurulumu Sihirbazı aracılığıyla hello StorSimple cihazı ilk dağıtım sırasında yapılandırılır. Merhaba aygıt bir işlemsel modundayken tooreconfigure veri 0 gerekebilir ayarlar. Bu öğretici toomodify veri 0 ağ ayarları, StorSimple için Windows PowerShell aracılığıyla her ikisi de iki yöntem sunar.

Bu öğretici okuduktan sonra aşağıdakileri gerçekleştirebilirsiniz:

* Veri 0 değiştirme ağ ayarını hello Kurulum Sihirbazı'nı kullanarak
* Veri 0 ağ ayarları'nda hello değiştirmek `Set-HcsNetInterface` cmdlet'i

## <a name="modify-data-0-network-settings-through-setup-wizard"></a>Kurulum Sihirbazı aracılığıyla veri 0 ağ ayarlarını değiştirme
StorSimple cihazınızın toohello Windows PowerShell arabirimi bağlanma ve Kurulum Sihirbazı'nı oturumunu başlatmasını veri 0 ağ ayarlarını yapılandırabilirsiniz. Gerçekleştirme adımları toomodify veri 0 aşağıdaki hello ayarları:

#### <a name="toomodify-data-0-network-settings-through-setup-wizard"></a>Kurulum Sihirbazı aracılığıyla toomodify veri 0 ağ ayarları
1. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**. İstendiğinde hello sağlamak **cihaz Yöneticisi parolası**. Merhaba varsayılan parola `Password1`.
2. Merhaba komut satırına aşağıdakini yazın:
   
    `Invoke-HcsSetupWizard`
3. Kurulum Sihirbazı'nı toohelp görünür hello veri 0 yapılandırma aygıtınızın arabirimi. Başlangıç IP adresi, ağ geçidi ve ağ maskesi için yeni değerleri sağlayın.

> [!NOTE]
> Sabit IP'leri hello yeniden toobe gerekir denetleyicileri hello **ağ ayarlarını** hello StorSimple cihazı hello Azure portal dikey. Daha fazla bilgi için çok Git[ağ arabirimleri değiştirme](storsimple-8000-modify-device-config.md#modify-network-interfaces).

## <a name="modify-data-0-network-settings-through-set-hcsnetinterface-cmdlet"></a>Set-HcsNetInterface cmdlet'i aracılığıyla veri 0 ağ ayarlarını değiştirme
Alternatif bir yol tooreconfigure veri 0 ağ arabirimi hello hello kullanımla `Set-HcsNetInterface` cmdlet'i. Merhaba cmdlet hello Windows PowerShell arabiriminden StorSimple Cihazınızı yürütülür. Bu yordam kullanılırken hello denetleyicisi sabit IP'leri de burada yapılandırılabilir. Gerçekleştirme adımları toomodify hello veri 0 aşağıdaki hello ayarları: 

#### <a name="toomodify-data-0-network-settings-through-hello-set-hcsnetinterface-cmdlet"></a>Merhaba Set-HcsNetInterface cmdlet'i toomodify veri 0 ağ ayarları
1. Merhaba seri konsol menüsünde seçeneği 1, **oturum oturum tam erişim**. İstendiğinde hello cihaz Yöneticisi parolasını verin. Merhaba varsayılan parola `Password1`.
2. Merhaba komut satırına aşağıdakini yazın:
   
    `Set-HCSNetInterface -InterfaceAlias Data0 -IPv4Address <> -IPv4Netmask <> -IPv4Gateway <> -Controller0IPv4Address <> -Controller1IPv4Address <> -IsiScsiEnabled 1 -IsCloudEnabled 1`
   
    Merhaba açılı ayraç DATA 0 için değerleri aşağıdaki hello yazın:
   
   * IPv4 adresi
   * IPv4 ağ geçidi
   * IPv4 alt ağ maskesi
   * Denetleyici 0 sabit IPv4 adresi
   * Denetleyici 1 için sabit IPv4 adresi
     
     Bu cmdlet hello kullanımı hakkında daha fazla bilgi için çok Git[StorSimple cmdlet başvurusu için Windows PowerShell](https://technet.microsoft.com/library/dn688161.aspx).

## <a name="next-steps"></a>Sonraki adımlar
* Veri 0 dışında tooconfigure ağ arabirimleri, kullanabileceğiniz hello [hello Azure portal ağ ayarlarını yapılandırma](storsimple-8000-modify-device-config.md). 
* Ağ arabirimleri yapılandırırken herhangi bir sorunla karşılaşırsanız, çok başvuran[dağıtım sorunlarını giderme](storsimple-troubleshoot-deployment.md).

