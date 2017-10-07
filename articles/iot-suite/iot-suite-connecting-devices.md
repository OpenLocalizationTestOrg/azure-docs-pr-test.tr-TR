---
title: "Windows C kullanarak cihazı aaaConnect | Microsoft Docs"
description: "Nasıl tooconnect aygıt toohello Azure IOT paketi Uzaktan izleme çözümü Windows üzerinde çalışan C yazılmış bir uygulama kullanarak önceden yapılandırılmış açıklar."
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 34e39a58-2434-482c-b3fa-29438a0c05e8
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 51041e0cec113a5cfa006ab2276096baf928eef5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-windows"></a>Uzaktan izleme çözümü (Windows), cihaz toohello Bağlan
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-c-sample-solution-on-windows"></a>Windows C örnek bir çözüm oluşturun
Aşağıdaki adımları hello nasıl toocreate hello Uzaktan izleme ile iletişim kuran bir istemci uygulaması çözüm önceden yapılandırılmış gösterir. Bu uygulama C'de yazılmış ve yerleşik ve Windows üzerinde çalıştırın.

Visual Studio 2015 veya Visual Studio 2017 içinde bir başlangıç projesi oluşturun ve hello IOT Hub cihaz istemcisi NuGet paketleri ekleyin:

1. Visual Studio'da hello Visual C++ kullanarak C konsol uygulaması oluşturma **Win32 konsol uygulaması** şablonu. Ad hello proje **RMDevice**.
2. Merhaba üzerinde **uygulama ayarları** hello sayfasında **Win32 Uygulama Sihirbazı'nı**, emin **konsol uygulaması** seçilidir ve işaretini **önceden derlenmiş Üstbilgi** ve **güvenlik geliştirme yaşam döngüsü (SDL) denetler**.
3. İçinde **Çözüm Gezgini**, hello dosyaları stdafx.h, targetver.h ve stdafx.cpp silin.
4. İçinde **Çözüm Gezgini**, hello dosya RMDevice.cpp tooRMDevice.c yeniden adlandırın.
5. İçinde **Çözüm Gezgini**, hello üzerinde sağ **RMDevice** proje ve ardından **Manage NuGet paketleri**. Tıklatın **Gözat**, ardından aramak ve NuGet paketleri aşağıdaki hello yükleyin:
   
   * Microsoft.Azure.IoTHub.Serializer
   * Microsoft.Azure.IoTHub.IoTHubClient
   * Microsoft.Azure.IoTHub.MqttTransport
6. İçinde **Çözüm Gezgini**, hello üzerinde sağ **RMDevice** proje ve ardından **özellikleri** tooopen hello projenin **özellik sayfaları**iletişim kutusu. Ayrıntılar için bkz [Visual C++ proje özelliklerini ayarlama][lnk-c-project-properties]. 
7. Hello tıklatın **bağlayıcı** klasörü, hello ardından **giriş** özellik sayfası.
8. Ekleme **crypt32.lib** toohello **ek bağımlılıklar** özelliği. Tıklatın **Tamam** ve ardından **Tamam** yeniden toosave hello proje özellik değerleri.

Merhaba Parson JSON kitaplığı toohello ekleme **RMDevice** proje ve gerekli hello eklemek `#include` deyimleri:

1. Bilgisayarınızda uygun bir klasörde komutu aşağıdaki hello kullanarak hello Parson GitHub deposunu kopyalayın:

    ```
    git clone https://github.com/kgabis/parson.git
    ```

1. Merhaba parson.h ve parson.c dosyaları hello yerel hello Parson depo tooyour kopyadan kopyalamak **RMDevice** proje klasörü.

1. Visual Studio'da hello sağ **RMDevice** proje, tıklatın **Ekle**ve ardından **varolan öğeyi**.

1. Merhaba, **varolan öğeyi Ekle** iletişim, select hello parson.h ve parson.c dosyalarında hello **RMDevice** proje klasörü. Ardından **Ekle** tooadd bu iki dosya tooyour projesi.

1. Visual Studio'da hello RMDevice.c dosyasını açın. Merhaba varolan `#include` koddan hello ifadelerle:
   
    ```c
    #include "iothubtransportmqtt.h"
    #include "schemalib.h"
    #include "iothub_client.h"
    #include "serializer_devicetwin.h"
    #include "schemaserializer.h"
    #include "azure_c_shared_utility/threadapi.h"
    #include "azure_c_shared_utility/platform.h"
    #include "parson.h"
    ```

    > [!NOTE]
    > Şimdi projenizi derleme tarafından ayarlanan hello doğru bağımlılıkları olduğunu doğrulayabilirsiniz.

[!INCLUDE [iot-suite-connecting-code](../../includes/iot-suite-connecting-code.md)]

## <a name="build-and-run-hello-sample"></a>Derleme ve hello örnek çalıştırma

Kod tooinvoke hello eklemek **uzak\_izleme\_çalıştırmak** işlev oluşturmak ve hello cihaz uygulamayı çalıştırın.

1. Hello yerine **ana** aşağıdaki kodu tooinvoke hello işleviyle **uzak\_izleme\_çalıştırmak** işlevi:
   
    ```c
    int main()
    {
      remote_monitoring_run();
      return 0;
    }
    ```

1. Tıklatın **yapı** ve ardından **yapı çözümü** toobuild Merhaba cihaz uygulaması.

1. İçinde **Çözüm Gezgini**, sağ hello **RMDevice** proje, tıklatın **hata ayıklama**ve ardından **başlangıç yeni örnek** toorun hello örnek. Merhaba uygulama örnek telemetri toohello önceden yapılandırılmış çözüm, hello çözüm panosunda ayarlamak istediğiniz özellik değerlerini alır ve hello çözüm panodan çağrılan toomethods yanıt gönderir gibi hello konsol iletileri görüntüler.

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-c-project-properties]: https://msdn.microsoft.com/library/669zx6zc.aspx
