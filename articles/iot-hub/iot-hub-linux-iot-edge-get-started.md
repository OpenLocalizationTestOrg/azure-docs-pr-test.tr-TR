---
title: "aaaGet başlatılan Azure IOT kenar (Linux) | Microsoft Docs"
description: "Nasıl toobuild bir Linux üzerinde bir ağ geçidi makinesi ve modülleri ve JSON yapılandırma dosyaları gibi Azure IOT edge'de temel kavramları hakkında bilgi edinin."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: cf537bdd-2352-4bb1-96cd-a283fcd3d6cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 40aa9c8ddca6a974c361cbb0b453c7d0ddc71b8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a>Linux üzerinde Azure IoT Edge mimarisini keşfedin

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>Nasıl toorun hello örnek

Merhaba **build.sh** betik hello çıktısını oluşturur **yapı** hello yerel kopyasını klasöründe **IOT kenar** deposu. Bu çıktı hello Bu örnekte kullanılan iki IOT kenar modüller içerir.

Merhaba yapı betik yerler **liblogger.so** hello içinde **modülleri/yapı/Günlükçü/** klasör ve **libhello\_world.so** hello içinde **yapı / modülleri/hello_world/** klasörü. Bu yolları Merhaba kullanma **modül yolu** değerleri aşağıdaki örnek JSON ayarları dosyasına hello gösterildiği gibi.

Merhaba hello\_world\_örnek işlemi, bir komut satırı bağımsız değişkeni hello yol tooa JSON yapılandırma dosyası kullanır. Merhaba aşağıdaki örnek JSON dosyası hello SDK deposu sırasında sağlanan **örnekleri/hello\_world/src/hello\_world\_lin.json**. Merhaba değiştirmediğiniz sürece olduğundan bu yapılandırma dosyası works betik tooplace hello IOT kenar modülleri oluşturabilir veya yürütülebilir dosyalar varsayılan olmayan konumlarda örnek.

> [!NOTE]
> Merhaba modülü göreli toohello geçerli çalışma dizini nerede yollardır hello hello\_world\_örnek yürütülebilir başlatıldığında, hello yürütülebilir bulunduğu dizin hello değil. Merhaba örnek JSON yapılandırma dosyası Varsayılanları toowriting 'log.txt', geçerli çalışma dizininde.

```json
{
    "modules" :
    [
        {
            "name" : "logger",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args" : {"filename":"log.txt"}
        },
        {
            "name" : "hello_world",
            "loader": {
            "name": "native",
            "entrypoint": {
                "module.path": "./modules/hello_world/libhello_world.so"
            }
            },
            "args" : null
        }
    ],
    "links":
    [
        {
            "source": "hello_world",
            "sink": "logger"
        }
    ]
}
```

1. Toohello gidin **yapı** hello yerel kopyasını hello kök klasöründe **IOT kenar** deposu.

1. Merhaba aşağıdaki komutu çalıştırın:

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

