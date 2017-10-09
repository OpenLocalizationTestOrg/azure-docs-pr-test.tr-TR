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
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="13f2f-103">Linux üzerinde Azure IoT Edge mimarisini keşfedin</span><span class="sxs-lookup"><span data-stu-id="13f2f-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="13f2f-104">Nasıl toorun hello örnek</span><span class="sxs-lookup"><span data-stu-id="13f2f-104">How toorun hello sample</span></span>

<span data-ttu-id="13f2f-105">Merhaba **build.sh** betik hello çıktısını oluşturur **yapı** hello yerel kopyasını klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="13f2f-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="13f2f-106">Bu çıktı hello Bu örnekte kullanılan iki IOT kenar modüller içerir.</span><span class="sxs-lookup"><span data-stu-id="13f2f-106">This output includes hello two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="13f2f-107">Merhaba yapı betik yerler **liblogger.so** hello içinde **modülleri/yapı/Günlükçü/** klasör ve **libhello\_world.so** hello içinde **yapı / modülleri/hello_world/** klasörü.</span><span class="sxs-lookup"><span data-stu-id="13f2f-107">hello build script places **liblogger.so** in hello **build/modules/logger/** folder and **libhello\_world.so** in hello **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="13f2f-108">Bu yolları Merhaba kullanma **modül yolu** değerleri aşağıdaki örnek JSON ayarları dosyasına hello gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="13f2f-108">Use these paths for hello **module path** values as shown in hello following example JSON settings file.</span></span>

<span data-ttu-id="13f2f-109">Merhaba hello\_world\_örnek işlemi, bir komut satırı bağımsız değişkeni hello yol tooa JSON yapılandırma dosyası kullanır.</span><span class="sxs-lookup"><span data-stu-id="13f2f-109">hello hello\_world\_sample process takes hello path tooa JSON configuration file a command-line argument.</span></span> <span data-ttu-id="13f2f-110">Merhaba aşağıdaki örnek JSON dosyası hello SDK deposu sırasında sağlanan **örnekleri/hello\_world/src/hello\_world\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="13f2f-110">hello following example JSON file is provided in hello SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="13f2f-111">Merhaba değiştirmediğiniz sürece olduğundan bu yapılandırma dosyası works betik tooplace hello IOT kenar modülleri oluşturabilir veya yürütülebilir dosyalar varsayılan olmayan konumlarda örnek.</span><span class="sxs-lookup"><span data-stu-id="13f2f-111">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="13f2f-112">Merhaba modülü göreli toohello geçerli çalışma dizini nerede yollardır hello hello\_world\_örnek yürütülebilir başlatıldığında, hello yürütülebilir bulunduğu dizin hello değil.</span><span class="sxs-lookup"><span data-stu-id="13f2f-112">hello module paths are relative toohello current working directory from where hello hello\_world\_sample executable is launched, not hello directory where hello executable is located.</span></span> <span data-ttu-id="13f2f-113">Merhaba örnek JSON yapılandırma dosyası Varsayılanları toowriting 'log.txt', geçerli çalışma dizininde.</span><span class="sxs-lookup"><span data-stu-id="13f2f-113">hello sample JSON configuration file defaults toowriting 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="13f2f-114">Toohello gidin **yapı** hello yerel kopyasını hello kök klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="13f2f-114">Navigate toohello **build** folder in hello root of your local copy of hello **iot-edge** repository.</span></span>

1. <span data-ttu-id="13f2f-115">Merhaba aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="13f2f-115">Run hello following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

