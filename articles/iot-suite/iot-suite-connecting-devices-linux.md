---
title: "Linux'ta C kullanarak cihazı aaaConnect | Microsoft Docs"
description: "Nasıl tooconnect aygıt toohello Azure IOT paketi Uzaktan izleme çözümü Linux üzerinde çalışan C yazılmış bir uygulama kullanarak önceden yapılandırılmış açıklar."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 0c7c8039-0bbf-4bb5-9e79-ed8cff433629
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 57393817d40d3555177956a01fa71058bc256988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a><span data-ttu-id="40b98-103">Uzaktan izleme çözümü (Linux), cihaz toohello Bağlan</span><span class="sxs-lookup"><span data-stu-id="40b98-103">Connect your device toohello remote monitoring preconfigured solution (Linux)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a><span data-ttu-id="40b98-104">Derleme ve örnek C istemcisi Linux çalıştırın</span><span class="sxs-lookup"><span data-stu-id="40b98-104">Build and run a sample C client Linux</span></span>
<span data-ttu-id="40b98-105">Aşağıdaki adımları hello nasıl toocreate hello Uzaktan izleme ile iletişim kuran bir istemci uygulaması çözüm önceden yapılandırılmış gösterir.</span><span class="sxs-lookup"><span data-stu-id="40b98-105">hello following steps show you how toocreate a client application that communicates with hello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="40b98-106">Bu uygulama C'de yazılmış ve yerleşik ve Ubuntu Linux üzerinde çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="40b98-106">This application is written in C and built and run on Ubuntu Linux.</span></span>

<span data-ttu-id="40b98-107">Aşağıdaki adımları toocomplete, Ubuntu 15.04 veya 15.10 sürümünü çalıştıran bir cihazda gerekir.</span><span class="sxs-lookup"><span data-stu-id="40b98-107">toocomplete these steps, you need a device running Ubuntu version 15.04 or 15.10.</span></span> <span data-ttu-id="40b98-108">Devam etmeden önce komutu aşağıdaki hello kullanarak Ubuntu aygıtınızda hello önkoşul yükleyin:</span><span class="sxs-lookup"><span data-stu-id="40b98-108">Before proceeding, install hello prerequisite packages on your Ubuntu device using hello following command:</span></span>

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a><span data-ttu-id="40b98-109">Cihazınızda Hello istemci kitaplıkları yükleme</span><span class="sxs-lookup"><span data-stu-id="40b98-109">Install hello client libraries on your device</span></span>
<span data-ttu-id="40b98-110">Hello Azure IOT Hub istemci kitaplıkları hello kullanarak Ubuntu aygıtınızda yükleyebilirsiniz bir paketi olarak kullanılabilir **get apt** komutu.</span><span class="sxs-lookup"><span data-stu-id="40b98-110">hello Azure IoT Hub client libraries are available as a package you can install on your Ubuntu device using hello **apt-get** command.</span></span> <span data-ttu-id="40b98-111">Merhaba IOT Hub istemci kitaplığı ve Ubuntu bilgisayarınızdaki üstbilgi dosyaları içeren adımları tooinstall hello paket aşağıdaki hello tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="40b98-111">Complete hello following steps tooinstall hello package that contains hello IoT Hub client library and header files on your Ubuntu computer:</span></span>

1. <span data-ttu-id="40b98-112">Bir Kabuğu'nda hello AzureIoT depo tooyour bilgisayar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="40b98-112">In a shell, add hello AzureIoT repository tooyour computer:</span></span>
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. <span data-ttu-id="40b98-113">Hello azure-IOT-sdk-c-dev paketini yükle</span><span class="sxs-lookup"><span data-stu-id="40b98-113">Install hello azure-iot-sdk-c-dev package</span></span>
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a><span data-ttu-id="40b98-114">Merhaba Parson JSON ayrıştırıcı yükleyin</span><span class="sxs-lookup"><span data-stu-id="40b98-114">Install hello Parson JSON parser</span></span>
<span data-ttu-id="40b98-115">Merhaba Parson JSON ayrıştırıcı tooparse ileti yükü Hello IOT Hub istemci kitaplıkları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40b98-115">hello IoT Hub client libraries use hello Parson JSON parser tooparse message payloads.</span></span> <span data-ttu-id="40b98-116">Bilgisayarınızda uygun bir klasörde komutu aşağıdaki hello kullanarak hello Parson GitHub deposunu kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="40b98-116">In a suitable folder on your computer, clone hello Parson GitHub repository using hello following command:</span></span>

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a><span data-ttu-id="40b98-117">Projenizi hazırlama</span><span class="sxs-lookup"><span data-stu-id="40b98-117">Prepare your project</span></span>
<span data-ttu-id="40b98-118">Ubuntu makinenizde adlı bir klasör oluşturun **uzak\_izleme**.</span><span class="sxs-lookup"><span data-stu-id="40b98-118">On your Ubuntu machine, create a folder called **remote\_monitoring**.</span></span> <span data-ttu-id="40b98-119">Merhaba, **uzak\_izleme** klasörü:</span><span class="sxs-lookup"><span data-stu-id="40b98-119">In hello **remote\_monitoring** folder:</span></span>

- <span data-ttu-id="40b98-120">Merhaba dört dosyaları oluşturma **main.c**, **uzak\_monitoring.c**, **uzak\_monitoring.h**, ve **CMakeLists.txt**.</span><span class="sxs-lookup"><span data-stu-id="40b98-120">Create hello four files **main.c**, **remote\_monitoring.c**, **remote\_monitoring.h**, and **CMakeLists.txt**.</span></span>
- <span data-ttu-id="40b98-121">Adlı bir klasör oluşturun **parson**.</span><span class="sxs-lookup"><span data-stu-id="40b98-121">Create folder called **parson**.</span></span>

<span data-ttu-id="40b98-122">Merhaba dosyaları kopyalama **parson.c** ve **parson.h** kopyasından yerel hello Parson depo hello içine **uzak\_izleme parson** klasör.</span><span class="sxs-lookup"><span data-stu-id="40b98-122">Copy hello files **parson.c** and **parson.h** from your local copy of hello Parson repository into hello **remote\_monitoring/parson** folder.</span></span>

<span data-ttu-id="40b98-123">Merhaba bir metin düzenleyicisinde açın **uzak\_monitoring.c** dosya.</span><span class="sxs-lookup"><span data-stu-id="40b98-123">In a text editor, open hello **remote\_monitoring.c** file.</span></span> <span data-ttu-id="40b98-124">Merhaba aşağıdakileri ekleyin `#include` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="40b98-124">Add hello following `#include` statements:</span></span>
   
```
#include "iothubtransportmqtt.h"
#include "schemalib.h"
#include "iothub_client.h"
#include "serializer_devicetwin.h"
#include "schemaserializer.h"
#include "azure_c_shared_utility/threadapi.h"
#include "azure_c_shared_utility/platform.h"
#include "parson.h"
```

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="call-hello-remotemonitoringrun-function"></a><span data-ttu-id="40b98-125">Merhaba uzaktan çağrısı\_izleme\_işlevini çalıştırma</span><span class="sxs-lookup"><span data-stu-id="40b98-125">Call hello remote\_monitoring\_run function</span></span>
<span data-ttu-id="40b98-126">Merhaba bir metin düzenleyicisinde açın **remote_monitoring.h** dosya.</span><span class="sxs-lookup"><span data-stu-id="40b98-126">In a text editor, open hello **remote_monitoring.h** file.</span></span> <span data-ttu-id="40b98-127">Hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="40b98-127">Add hello following code:</span></span>

```
void remote_monitoring_run(void);
```

<span data-ttu-id="40b98-128">Merhaba bir metin düzenleyicisinde açın **main.c** dosya.</span><span class="sxs-lookup"><span data-stu-id="40b98-128">In a text editor, open hello **main.c** file.</span></span> <span data-ttu-id="40b98-129">Hello aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="40b98-129">Add hello following code:</span></span>

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a><span data-ttu-id="40b98-130">Derleme ve Merhaba uygulaması çalıştırma</span><span class="sxs-lookup"><span data-stu-id="40b98-130">Build and run hello application</span></span>
<span data-ttu-id="40b98-131">Merhaba aşağıdaki adımlarda açıklanmaktadır nasıl toouse *CMake* toobuild istemci uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="40b98-131">hello following steps describe how toouse *CMake* toobuild your client application.</span></span>

1. <span data-ttu-id="40b98-132">Merhaba bir metin düzenleyicisinde açın **CMakeLists.txt** hello dosyasında **remote_monitoring** klasör.</span><span class="sxs-lookup"><span data-stu-id="40b98-132">In a text editor, open hello **CMakeLists.txt** file in hello **remote_monitoring** folder.</span></span>

1. <span data-ttu-id="40b98-133">Yönergeler toodefine nasıl aşağıdaki hello eklemek toobuild istemci uygulamanızı:</span><span class="sxs-lookup"><span data-stu-id="40b98-133">Add hello following instructions toodefine how toobuild your client application:</span></span>
   
    ```
    macro(compileAsC99)
      if (CMAKE_VERSION VERSION_LESS "3.1")
        if (CMAKE_C_COMPILER_ID STREQUAL "GNU")
          set (CMAKE_C_FLAGS "--std=c99 ${CMAKE_C_FLAGS}")
          set (CMAKE_CXX_FLAGS "--std=c++11 ${CMAKE_CXX_FLAGS}")
        endif()
      else()
        set (CMAKE_C_STANDARD 99)
        set (CMAKE_CXX_STANDARD 11)
      endif()
    endmacro(compileAsC99)

    cmake_minimum_required(VERSION 2.8.11)
    compileAsC99()

    set(AZUREIOT_INC_FOLDER "${CMAKE_SOURCE_DIR}" "${CMAKE_SOURCE_DIR}/parson" "/usr/include/azureiot" "/usr/include/azureiot/inc")

    include_directories(${AZUREIOT_INC_FOLDER})

    set(sample_application_c_files
        ./parson/parson.c
        ./remote_monitoring.c
        ./main.c
    )

    set(sample_application_h_files
        ./parson/parson.h
        ./remote_monitoring.h
    )

    add_executable(sample_app ${sample_application_c_files} ${sample_application_h_files})

    target_link_libraries(sample_app
        serializer
        iothub_client
        iothub_client_mqtt_transport
        aziotsharedutil
        umqtt
        pthread
        curl
        ssl
        crypto
        m
    )
    ```
1. <span data-ttu-id="40b98-134">Merhaba, **remote_monitoring** klasörü, bir klasör toostore hello oluşturma *olun* dosyaları bu CMake oluşturur ve ardından hello çalıştırın **cmake** ve **olun** gibi komutlar:</span><span class="sxs-lookup"><span data-stu-id="40b98-134">In hello **remote_monitoring** folder, create a folder toostore hello *make* files that CMake generates and then run hello **cmake** and **make** commands as follows:</span></span>
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. <span data-ttu-id="40b98-135">Merhaba istemci uygulaması çalıştırın ve telemetri tooIoT Hub gönder:</span><span class="sxs-lookup"><span data-stu-id="40b98-135">Run hello client application and send telemetry tooIoT Hub:</span></span>
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

