---
title: "aaaGet başlatılan Azure IOT kenar (Windows) | Microsoft Docs"
description: "Nasıl toobuild bir Azure IOT sınır ağ geçidi Windows makine ve modülleri ve JSON yapılandırma dosyaları gibi Azure IOT edge'de temel kavramları hakkında bilgi edinin."
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 9aff3724-5e4e-40ec-b95a-d00df4f590c5
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/07/2017
ms.author: andbuc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5dd13cbfc02eeb55d9f2dbffca5021f2624acf14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-azure-iot-edge-architecture-on-windows"></a>Windows Azure IOT kenar mimarisi keşfedin

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a>Nasıl toorun hello örnek

Merhaba **build.cmd** betik hello çıktısını oluşturur **yapı** hello yerel kopyasını klasöründe **IOT kenar** deposu. Bu çıktı hello Bu örnekte kullanılan iki IOT kenar modüller içerir.

Merhaba yapı betik yerler **logger.dll** hello içinde **yapı\\modülleri\\Günlükçü\\hata ayıklama** klasör ve **hello\_world.dll**  hello içinde **yapı\\modülleri\\hello_world\\hata ayıklama** klasör. Bu yolları Merhaba kullanma **modül yolu** değerleri aşağıdaki JSON ayarları dosyasına hello gösterildiği gibi.

Merhaba hello\_world\_örnek işlemi hello yol tooa JSON yapılandırma dosyası komut satırı bağımsız değişkeni olarak alır. Merhaba aşağıdaki örnek JSON dosyası hello SDK deposu sırasında sağlanan **örnekleri\\hello\_world\\src\\hello\_world\_win.json**. Merhaba değiştirmediğiniz sürece olduğundan bu yapılandırma dosyası works betik tooplace hello IOT kenar modülleri oluşturabilir veya yürütülebilir dosyalar varsayılan olmayan konumlarda örnek.

> [!NOTE]
> Merhaba modülü yollardır göreli toohello dizin hello burada hello\_world\_sample.exe bulunduğu. Merhaba örnek JSON yapılandırma dosyası Varsayılanları toowriting 'log.txt', geçerli çalışma dizininde.

```json
{
  "modules": [
    {
      "name": "logger",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\logger\\Debug\\logger.dll"
        }
      },
      "args": { "filename": "log.txt" }
    },
    {
      "name": "hello_world",
      "loader": {
        "name": "native",
        "entrypoint": {
          "module.path": "..\\..\\..\\modules\\hello_world\\Debug\\hello_world.dll"
        }
      },
      "args": null
      }
  ],
  "links": [
    {
      "source": "hello_world",
      "sink": "logger"
    }
  ]
}
```

1. Toohello gidin **yapı** hello yerel kopyasını hello kök klasöründe **IOT kenar** deposu.

1. Merhaba aşağıdaki komutu çalıştırın:

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
