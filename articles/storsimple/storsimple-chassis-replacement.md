---
title: "StorSimple 8000 serisi aygıtta aaaReplace kasa | Microsoft Docs"
description: "StorSimple birincil muhafaza veya EBOD muhafazası için kasa tooremove ve Değiştir nasıl hello açıklar."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8576d63520a6f7d3267180d2a68d4fc38fd48fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-chassis-on-your-storsimple-device"></a>StorSimple Cihazınızda Hello kasa değiştirin
## <a name="overview"></a>Genel Bakış
Bu öğretici açıklar nasıl tooremove ve StorSimple 8000 serisi aygıtta bir kasa değiştirin. Merhaba 8600 çift muhafaza aygıt (iki kasa) iken hello StorSimple 8100 model bir tek kasası (bir kasa), aygıttır. 8600 model için büyük olasılıkla hello aygıtı başarısız iki kasa vardır: Merhaba hello birincil kasası için Kasa ya da hello EBOD muhafazası hello Kasa.

Her iki durumda da, Microsoft tarafından sevk hello değiştirme kasa boştur. Hiçbir güç ve soğutma modülleri (PCMs) denetleyicisi modülleri, katı hal disk sürücüleri (SSD), sabit disk sürücülerinin (HDD'ler) ya da EBOD modülleri dahil edilir.

> [!IMPORTANT]
> Merhaba kasa, değiştirme ve kaldırma gözden önce hello güvenlik bilgileri [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="remove-hello-chassis"></a>Merhaba kasa Kaldır
StorSimple Cihazınızda adımları tooremove hello kasa aşağıdaki hello gerçekleştirin.

#### <a name="tooremove-a-chassis"></a>tooremove bir kasa
1. Merhaba StorSimple cihaz kapatılır ve tüm hello güç kaynaklardan bağlantısı kesilmiş emin olun.
2. Tüm hello ağ ve SAS kabloları varsa kaldırın.
3. Merhaba birimi hello raf kaldırın.
4. Her hello sürücüleri kaldırın ve hello yuvaları, bunlar kaldırılır unutmayın. Daha fazla bilgi için bkz: [kaldırmak hello disk sürücüsü](storsimple-disk-drive-replacement.md#remove-the-disk-drive).
5. Hello (Bu başarısız hello kasa ise) EBOD muhafazası, hello EBOD denetleyicisi modülleri kaldırın. Daha fazla bilgi için bkz: [EBOD denetleyicisi kaldırmak](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller). 
   
    Hello (Bu başarısız hello kasa ise) birincil muhafaza hello denetleyicilerini kaldırın ve hello yuvaları, bunlar kaldırılır unutmayın. Daha fazla bilgi için bkz: [bir denetleyici kaldırmak](storsimple-controller-replacement.md#remove-a-controller).

## <a name="install-hello-chassis"></a>Merhaba kasa yükleyin
StorSimple Cihazınızda adımları tooinstall hello kasa aşağıdaki hello gerçekleştirin.

#### <a name="tooinstall-a-chassis"></a>tooinstall bir kasa
1. Merhaba kasa hello dolapta bağlayın. Daha fazla bilgi için bkz: [rafa monte StorSimple 8100 aygıt](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) veya [rafa monte StorSimple 8600 aygıt](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).
2. Merhaba kasa hello rafa monte sonra hello denetleyicisi modülleri aynı daha önce de yüklendikleri konumlandırır hello yükleyin.
3. Yükleme Merhaba, daha önce de yüklendikleri aynı yerleştirir ve yuvası hello sürücüleri.
   
   > [!NOTE]
   > Merhaba SSD hello yuvalarında yüklemeniz ve ardından hello HDD yükleyin öneririz.
   > 
   > 
4. Merhaba ile cihaz hello rafa monte ve hello bileşenlerinin yüklü olması, aygıt toohello uygun güç kaynaklarınız bağlanmak ve hello aygıtı açın. Ayrıntılar için bkz [StorSimple 8100 cihazınız kablo](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) veya [StorSimple 8600 model Cihazınızı kablo](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

## <a name="next-steps"></a>Sonraki adımlar
Daha fazla bilgi edinmek [StorSimple donanım bileşeni değiştirme](storsimple-hardware-component-replacement.md).

