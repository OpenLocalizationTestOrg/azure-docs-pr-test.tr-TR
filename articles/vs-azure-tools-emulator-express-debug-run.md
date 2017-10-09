---
title: "aaaUsing Emulator Express toorun ve hata ayıklama Azure bulut hizmeti yerel makinede | Microsoft Docs"
description: "Yerel makinede emulator Express toorun ve hata ayıklama bir bulut hizmeti kullanma"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a>Öykünücü Express kullanarak toorun ve hata ayıklama Azure bulut hizmeti yerel makinede
Öykünücü Express kullanarak, test ve yönetici olarak Visual Studio çalıştırmadan bir bulut hizmetinde hata ayıklama. Proje ayarları toouse Emulator Express ayarlayabilir veya Bulut hizmetiniz hello gereksinimlerine bağlı olarak tam öykünücü hello. Merhaba tam öykünücü hakkında daha fazla bilgi için bkz: [hello işlem öykünücüsü bir Azure uygulaması çalıştırmasına](storage/common/storage-use-emulator.md).

## <a name="using-emulator-express-in-visual-studio"></a>Visual Studio öykünücüsü kullanarak
Azure SDK 2.3 veya daha sonra bir Azure projesi oluşturduğunuzda, Emulator Express otomatik olarak kullanılır. Önceki bir sürümünü hello Azure SDK'sı ile oluşturulan mevcut projeleri için aşağıdaki adımları tooselect Emulator Express hello kullanın:

1. Oluşturun veya bir Azure bulut hizmeti projesini Visual Studio'da açın.

1. İçinde **Çözüm Gezgini**hello projesine sağ tıklayın ve, hello bağlam menüsünden seçin **özellikleri**.

1. Başlangıç projeleri özellikler sayfalarında hello seçin **Web** sekmesi.

    ![Bir Azure bulut hizmeti projesi özellikleri](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. Altında **yerel geliştirme sunucusu**seçin **IIS Express kullan seçeneği**.

1. Altında **öykünücüsü**seçin **öykünücü kullan Express**.
   
1. komutu bir komut isteminde aşağıdaki hello çalıştırmak toolaunch hello Emulator Express: 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Öykünücü Express sınırlamaları
Aşağıdaki sorunlar hello Emulator Express sınırlamaları bilinmektedir: 

- Öykünücü Express IIS Web sunucusu ile uyumlu değil.
- Bulut hizmetinizi birden çok rol içerebilir, ancak her rol sınırlı tooone örneğidir.
- Bağlantı noktası numaralarını 1000 aşağıda erişemiyor. Normalde 1000 aşağıda bağlantı noktası kullanan bir kimlik doğrulama sağlayıcısı kullanırsanız, 1000'dir bu değeri tooa bağlantı noktası numarası toochange gerekebilir.
- Toohello Azure işlem öykünücüsü geçerli sınırlamalar tooEmulator Express de geçerlidir. Örneğin, dağıtım başına 50'den fazla rol örneği sahip olamaz. Hello Azure işlem öykünücüsü hakkında daha fazla bilgi için bkz: [hello işlem öykünücüsü bir Azure uygulaması çalıştırmasına](http://go.microsoft.com/fwlink/p/?LinkId=623050).

## <a name="next-steps"></a>Sonraki adımlar
[Hata ayıklama Azure bulut Hizmetleri](https://msdn.microsoft.com/library/azure/ee405479.aspx)
