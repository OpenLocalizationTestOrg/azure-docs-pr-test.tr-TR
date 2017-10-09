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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-linux"></a>Uzaktan izleme çözümü (Linux), cihaz toohello Bağlan
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="build-and-run-a-sample-c-client-linux"></a>Derleme ve örnek C istemcisi Linux çalıştırın
Aşağıdaki adımları hello nasıl toocreate hello Uzaktan izleme ile iletişim kuran bir istemci uygulaması çözüm önceden yapılandırılmış gösterir. Bu uygulama C'de yazılmış ve yerleşik ve Ubuntu Linux üzerinde çalıştırın.

Aşağıdaki adımları toocomplete, Ubuntu 15.04 veya 15.10 sürümünü çalıştıran bir cihazda gerekir. Devam etmeden önce komutu aşağıdaki hello kullanarak Ubuntu aygıtınızda hello önkoşul yükleyin:

```
sudo apt-get install cmake gcc g++
```

## <a name="install-hello-client-libraries-on-your-device"></a>Cihazınızda Hello istemci kitaplıkları yükleme
Hello Azure IOT Hub istemci kitaplıkları hello kullanarak Ubuntu aygıtınızda yükleyebilirsiniz bir paketi olarak kullanılabilir **get apt** komutu. Merhaba IOT Hub istemci kitaplığı ve Ubuntu bilgisayarınızdaki üstbilgi dosyaları içeren adımları tooinstall hello paket aşağıdaki hello tamamlayın:

1. Bir Kabuğu'nda hello AzureIoT depo tooyour bilgisayar ekleyin:
   
    ```
    sudo add-apt-repository ppa:aziotsdklinux/ppa-azureiot
    sudo apt-get update
    ```
2. Hello azure-IOT-sdk-c-dev paketini yükle
   
    ```
    sudo apt-get install -y azure-iot-sdk-c-dev
    ```

## <a name="install-hello-parson-json-parser"></a>Merhaba Parson JSON ayrıştırıcı yükleyin
Merhaba Parson JSON ayrıştırıcı tooparse ileti yükü Hello IOT Hub istemci kitaplıkları kullanabilirsiniz. Bilgisayarınızda uygun bir klasörde komutu aşağıdaki hello kullanarak hello Parson GitHub deposunu kopyalayın:

```
git clone https://github.com/kgabis/parson.git
```

## <a name="prepare-your-project"></a>Projenizi hazırlama
Ubuntu makinenizde adlı bir klasör oluşturun **uzak\_izleme**. Merhaba, **uzak\_izleme** klasörü:

- Merhaba dört dosyaları oluşturma **main.c**, **uzak\_monitoring.c**, **uzak\_monitoring.h**, ve **CMakeLists.txt**.
- Adlı bir klasör oluşturun **parson**.

Merhaba dosyaları kopyalama **parson.c** ve **parson.h** kopyasından yerel hello Parson depo hello içine **uzak\_izleme parson** klasör.

Merhaba bir metin düzenleyicisinde açın **uzak\_monitoring.c** dosya. Merhaba aşağıdakileri ekleyin `#include` deyimleri:
   
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

## <a name="call-hello-remotemonitoringrun-function"></a>Merhaba uzaktan çağrısı\_izleme\_işlevini çalıştırma
Merhaba bir metin düzenleyicisinde açın **remote_monitoring.h** dosya. Hello aşağıdaki kodu ekleyin:

```
void remote_monitoring_run(void);
```

Merhaba bir metin düzenleyicisinde açın **main.c** dosya. Hello aşağıdaki kodu ekleyin:

```
#include "remote_monitoring.h"

int main(void)
{
    remote_monitoring_run();

    return 0;
}
```

## <a name="build-and-run-hello-application"></a>Derleme ve Merhaba uygulaması çalıştırma
Merhaba aşağıdaki adımlarda açıklanmaktadır nasıl toouse *CMake* toobuild istemci uygulamanızı.

1. Merhaba bir metin düzenleyicisinde açın **CMakeLists.txt** hello dosyasında **remote_monitoring** klasör.

1. Yönergeler toodefine nasıl aşağıdaki hello eklemek toobuild istemci uygulamanızı:
   
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
1. Merhaba, **remote_monitoring** klasörü, bir klasör toostore hello oluşturma *olun* dosyaları bu CMake oluşturur ve ardından hello çalıştırın **cmake** ve **olun** gibi komutlar:
   
    ```
    mkdir cmake
    cd cmake
    cmake ../
    make
    ```

1. Merhaba istemci uygulaması çalıştırın ve telemetri tooIoT Hub gönder:
   
    ```
    ./sample_app
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

