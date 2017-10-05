---
title: "Azure IOT kenar (Linux) ile çalışmaya başlama | Microsoft Docs"
description: "Bir Linux makine üzerinde ağ geçidi oluşturmanın yanı sıra modüller ve JSON yapılandırma dosyaları gibi temel Azure IoT Edge kavramları hakkında bilgi edinin."
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
ms.openlocfilehash: b02d79fcd9cd2a2ef0041aac4e85528263c8d58a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="explore-azure-iot-edge-architecture-on-linux"></a><span data-ttu-id="02e3f-103">Linux üzerinde Azure IoT Edge mimarisini keşfedin</span><span class="sxs-lookup"><span data-stu-id="02e3f-103">Explore Azure IoT Edge architecture on Linux</span></span>

[!INCLUDE [iot-hub-iot-edge-getstarted-selector](../../includes/iot-hub-iot-edge-getstarted-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-to-run-the-sample"></a><span data-ttu-id="02e3f-104">Örneği çalıştırma</span><span class="sxs-lookup"><span data-stu-id="02e3f-104">How to run the sample</span></span>

<span data-ttu-id="02e3f-105">**build.sh** betiği, çıktısını **iot-edge** deposu yerel kopyasının **build** klasöründe oluşturur.</span><span class="sxs-lookup"><span data-stu-id="02e3f-105">The **build.sh** script generates its output in the **build** folder in your local copy of the **iot-edge** repository.</span></span> <span data-ttu-id="02e3f-106">Bu çıktı, bu örnekte kullanılan iki IOT kenar modüller içerir.</span><span class="sxs-lookup"><span data-stu-id="02e3f-106">This output includes the two IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="02e3f-107">Derleme betiği, **liblogger.so** dosyasını **build/modules/logger/** klasörüne ve **libhello\_world.so** dosyasını **build/modules/hello_world/** klasörüne yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="02e3f-107">The build script places **liblogger.so** in the **build/modules/logger/** folder and **libhello\_world.so** in the **build/modules/hello_world/** folder.</span></span> <span data-ttu-id="02e3f-108">Bu yolları için kullanma **modül yolu** değerleri aşağıdaki örnek JSON ayarları dosyasında gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="02e3f-108">Use these paths for the **module path** values as shown in the following example JSON settings file.</span></span>

<span data-ttu-id="02e3f-109">Merhaba\_dünya\_örneği işleminde JSON yapılandırma dosyasının yolu komut satırı bağımsız değişkeni olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="02e3f-109">The hello\_world\_sample process takes the path to a JSON configuration file a command-line argument.</span></span> <span data-ttu-id="02e3f-110">Aşağıdaki örnek JSON dosyası, SDK deposundaki **samples/hello\_world/src/hello\_world\_lin.json** dizininde sağlanır.</span><span class="sxs-lookup"><span data-stu-id="02e3f-110">The following example JSON file is provided in the SDK repository at **samples/hello\_world/src/hello\_world\_lin.json**.</span></span> <span data-ttu-id="02e3f-111">Bu yapılandırma dosyası IOT kenar modülleri veya örnek yürütülebilir dosyalar varsayılan olmayan konumlara yerleştirmek için yapı betik değiştirmediğiniz sürece olduğu gibi çalışır.</span><span class="sxs-lookup"><span data-stu-id="02e3f-111">This configuration file works as is unless you modify the build script to place the IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="02e3f-112">Modül yolları, geçerli çalışma dizinine göre belirlenmiştir ve hello\_world\_sample yürütülebilir dosyasının bulunduğu değil çalıştırıldığı dizini temel alır.</span><span class="sxs-lookup"><span data-stu-id="02e3f-112">The module paths are relative to the current working directory from where the hello\_world\_sample executable is launched, not the directory where the executable is located.</span></span> <span data-ttu-id="02e3f-113">Örnek JSON yapılandırma dosyası varsayılan olarak “log.txt” dosyasını geçerli çalışma dizininize yazar.</span><span class="sxs-lookup"><span data-stu-id="02e3f-113">The sample JSON configuration file defaults to writing 'log.txt' in your current working directory.</span></span>

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

1. <span data-ttu-id="02e3f-114">Gidin **yapı** yerel kopyasını kök klasöründe **IOT kenar** deposu.</span><span class="sxs-lookup"><span data-stu-id="02e3f-114">Navigate to the **build** folder in the root of your local copy of the **iot-edge** repository.</span></span>

1. <span data-ttu-id="02e3f-115">Şu komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="02e3f-115">Run the following command:</span></span>

    ```sh
    ./samples/hello_world/hello_world_sample ../samples/hello_world/src/hello_world_lin.json`
    ```

[!INCLUDE [iot-hub-iot-edge-getstarted-code](../../includes/iot-hub-iot-edge-getstarted-code.md)]

