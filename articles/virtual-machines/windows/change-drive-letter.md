---
title: "VM bir veri diski D: sürücü hello olun | Microsoft Docs"
description: "Bir veri sürücüsü olarak hello D: sürücü kullanabilmesi için bir Windows VM nasıl toochange sürücü harfleri açıklar."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a>Bir Windows VM üzerinde bir veri sürücüsü olarak Hello D: sürücü kullanın
Uygulamanızı toouse hello D sürücü toostore veri gerekiyorsa, bu yönergeler toouse hello geçici disk için farklı bir sürücü harfi izleyin. Hiçbir zaman tookeep gereksinim hello geçici disk toostore verileri kullanın.

Yeniden boyutlandırma varsa veya **Dur (Deallocate)** bir sanal makine, bu hello sanal makine tooa yeni hiper yerleşimini tetikleyebilir. Bir planlı veya plansız bir bakım olayı de bu yerleştirme tetikleyebilir. Bu senaryoda, hello geçici disk yeniden atanan toohello ilk kullanılabilir sürücü harfini olacaktır. Özellikle hello D: sürücü gerektiren bir uygulama varsa, bu yeni bir veri diski ekleyin ve hello Harf D atamak adımları tootemporarily taşıma hello pagefile.sys ve ardından toohello geçici sürücü geri taşıma hello pagefile.sys toofollow gerekir. Merhaba VM tooa farklı hiper yönetici taşınırsa tamamlandıktan sonra Azure geri hello D: olmayacaktır.

Azure hello geçici disk nasıl kullandığı hakkında daha fazla bilgi için bkz: [hello geçici sürücü Microsoft Azure sanal makineler üzerinde anlama](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="attach-hello-data-disk"></a>Merhaba veri diski Ekle
İlk olarak, tooattach hello veri diski toohello sanal makine gerekir. toodo bu hello portal'ı kullanarak, bkz: [nasıl tooattach yönetilen bir veri diski hello Azure portal](attach-managed-disk-portal.md).

## <a name="temporarily-move-pagefilesys-tooc-drive"></a>Geçici olarak pagefile.sys tooC sürücüye taşıyın
1. Toohello sanal makineye bağlanın. 
2. Sağ hello **Başlat** menü ve select **sistem**.
3. Merhaba sol menüde seçin **Gelişmiş Sistem ayarları**.
4. Merhaba, **performans** bölümünde, select **ayarları**.
5. Select hello **Gelişmiş** sekmesi.
6. Merhaba, **sanal bellek** bölümünde, select **değişiklik**.
7. Select hello **C** sürücü ve ardından **sistem yönetilen boyutu** ve ardından **ayarlamak**.
8. Select hello **D** sürücü ve ardından **herhangi bir disk belleği dosyası** ve ardından **ayarlamak**.
9. Uygula'yı tıklatın. Bu hello bilgisayarın hello değişiklikleri tootake etkileyen için yeniden toobe gerekiyor bir uyarı alırsınız.
10. Merhaba sanal makineyi yeniden başlatın.

## <a name="change-hello-drive-letters"></a>Merhaba sürücü harflerini Değiştir
1. Bir kez hello VM yeniden başlatma geri toohello üzerinde VM oturum.
2. Merhaba tıklatın **Başlat** menü ve türü **diskmgmt.msc** ve Enter tuşuna basın. Disk Yönetimi başlar.
3. Sağ **D**hello geçici depolama sürücüsü ve seçin **değişiklik sürücü harfi ve yolları**.
4. Sürücü harfi altında yeni bir sürücü gibi seçin **T** ve ardından **Tamam**. 
5. Merhaba veri disk üzerinde sağ tıklatın ve seçin **değişiklik sürücü harfi ve yolları**.
6. Sürücü harfi altında seçin **D** ve ardından **Tamam**. 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a>Pagefile.sys geri toohello geçici depolama sürücüsü taşıma
1. Sağ hello **Başlat** menü ve select **sistem**
2. Merhaba sol menüde seçin **Gelişmiş Sistem ayarları**.
3. Merhaba, **performans** bölümünde, select **ayarları**.
4. Select hello **Gelişmiş** sekmesi.
5. Merhaba, **sanal bellek** bölümünde, select **değişiklik**.
6. Merhaba işletim sistemi sürücüsünü seçin **C** tıklatıp **herhangi bir disk belleği dosyası** ve ardından **ayarlamak**.
7. Merhaba geçici depolama sürücüsünü seçin **T** ve ardından **sistem yönetilen boyutu** ve ardından **ayarlamak**.
8. **Uygula**'ya tıklayın. Bu hello bilgisayarın hello değişiklikleri tootake etkileyen için yeniden toobe gerekiyor bir uyarı alırsınız.
9. Merhaba sanal makineyi yeniden başlatın.

## <a name="next-steps"></a>Sonraki adımlar
* Merhaba depolama kullanılabilir tooyour sanal makine tarafından artırabilirsiniz [bir ek veri diski eklemeyi](attach-managed-disk-portal.md).

