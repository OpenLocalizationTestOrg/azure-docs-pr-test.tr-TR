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
# <a name="explore-azure-iot-edge-architecture-on-windows"></a><span data-ttu-id="a9526-103">Windows Azure IOT kenar mimarisi keşfedin</span><span class="sxs-lookup"><span data-stu-id="a9526-103">Explore Azure IoT Edge architecture on Windows</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-windows](../../includes/iot-hub-iot-edge-install-build-windows.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="a9526-104">Nasıl toorun hello örnek</span><span class="sxs-lookup"><span data-stu-id="a9526-104">How toorun hello sample</span></span>

<span data-ttu-id="a9526-105">Merhaba **build.cmd** betik hello çıktısını oluşturur **yapı** hello yerel kopyasını klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="a9526-105">hello **build.cmd** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="a9526-106">Bu çıktı hello Bu örnekte kullanılan iki IOT kenar modüller içerir.</span><span class="sxs-lookup"><span data-stu-id="a9526-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="a9526-107">Merhaba yapı betik yerler **logger.dll** hello içinde **yapı\\modülleri\\Günlükçü\\hata ayıklama** klasör ve **hello\_world.dll**  hello içinde **yapı\\modülleri\\hello_world\\hata ayıklama** klasör.</span><span class="sxs-lookup"><span data-stu-id="a9526-107">hello build script places **logger.dll** in hello **build\\modules\\logger\\Debug** folder and **hello\_world.dll** in hello **build\\modules\\hello_world\\Debug** folder.</span></span> <span data-ttu-id="a9526-108">Bu yolları Merhaba kullanma **modül yolu** değerleri aşağıdaki JSON ayarları dosyasına hello gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="a9526-108">Use these paths for hello **module path** values as shown in hello following JSON settings file.</span></span>

<span data-ttu-id="a9526-109">Merhaba hello\_world\_örnek işlemi hello yol tooa JSON yapılandırma dosyası komut satırı bağımsız değişkeni olarak alır.</span><span class="sxs-lookup"><span data-stu-id="a9526-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="a9526-110">Merhaba aşağıdaki örnek JSON dosyası hello SDK deposu sırasında sağlanan **örnekleri\\hello\_world\\src\\hello\_world\_win.json**.</span><span class="sxs-lookup"><span data-stu-id="a9526-110">hello following example JSON file is provided in hello SDK repository at **samples\\hello\_world\\src\\hello\_world\_win.json**.</span></span> <span data-ttu-id="a9526-111">Merhaba değiştirmediğiniz sürece olduğundan bu yapılandırma dosyası works betik tooplace hello IOT kenar modülleri oluşturabilir veya yürütülebilir dosyalar varsayılan olmayan konumlarda örnek.</span><span class="sxs-lookup"><span data-stu-id="a9526-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="a9526-112">Merhaba modülü yollardır göreli toohello dizin hello burada hello\_world\_sample.exe bulunduğu.</span><span class="sxs-lookup"><span data-stu-id="a9526-112">hello module paths are relative toohello directory where hello hello\_world\_sample.exe is located.</span></span> <span data-ttu-id="a9526-113">Merhaba örnek JSON yapılandırma dosyası Varsayılanları toowriting 'log.txt', geçerli çalışma dizininde.</span><span class="sxs-lookup"><span data-stu-id="a9526-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="a9526-114">Toohello gidin **yapı** hello yerel kopyasını hello kök klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="a9526-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="a9526-115">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="a9526-115">Run hello following command:</span></span>

    ```cmd
    samples\hello_world\Debug\hello_world_sample.exe ..\samples\hello_world\src\hello_world_win.json
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]
