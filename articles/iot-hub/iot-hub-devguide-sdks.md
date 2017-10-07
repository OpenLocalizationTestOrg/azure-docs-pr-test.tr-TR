---
title: "aaaUnderstand hello Azure IOT SDK'ları | Microsoft Docs"
description: "Geliştirici Kılavuzu - hakkında bilgi ve bağlantılar toohello toobuild aygıt uygulamalar ve arka uç uygulamalar kullanabilirsiniz çeşitli Azure IOT cihaz ve hizmet SDK'ları."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e319451ca97876666e1c011ee0e1a73d0a0f1ed1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a>Anlamak ve Azure IOT SDK'ları kullanın

IOT Hub ile çalışmaya yönelik SDK'ın üç kategoriye ayrılır:

* **Cihaz SDK'ları** IOT cihazlarınızı üzerinde çalışan toobuild uygulamalar etkinleştirin. Bu uygulamaları tooyour IOT hub'ı telemetri gönderebilir ve isteğe bağlı olarak, IOT hub'ından iletileri alacak.

* **Hizmet SDK'ları** , toomanage IOT hub'ınızı etkinleştir ve isteğe bağlı olarak tooyour IOT cihazları iletileri gönder.

* **Azure IOT kenar** , kullanmama desteklenen hello protokollerden birini ya da hello kenar tooprocess iletileri gerektiğinde toobuild ağ geçitleri tooenable aygıtları etkinleştirir.

SDK'ları olan birden fazla programlama dili toosupport sağlanan.

## <a name="azure-iot-device-sdks"></a>Azure IOT cihaz SDK'ları

Merhaba Microsoft Azure IOT cihaz SDK'ları içeren yapı aygıtları kolaylaştıran kod ve tooand bağlanan uygulamaları Azure IOT Hub Hizmetleri tarafından yönetilir.

Merhaba aşağıdaki Azure IOT cihaz SDK'ları github'dan kullanılabilir toodownload şunlardır:

* [C için Azure IOT cihaz SDK'sı] [ lnk-c-device-sdk] taşınabilirlik ve geniş platform uyumluluğu için ANSI C (C99) yazılır. İki aygıt istemci kitaplığı yok c hello alt düzey **iothub_client** ve hello **seri hale getirici**.
* [.NET için Azure IOT cihaz SDK'sı][lnk-dotnet-device-sdk]
* [Java için Azure IOT cihaz SDK'sı][lnk-java-device-sdk]
* [Node.js için Azure IOT cihaz SDK'sı][lnk-node-device-sdk]
* [Python için Azure IOT cihaz SDK'sı][lnk-python-device-sdk]

> [!NOTE]
> Merhaba readme dosyalarında hello GitHub depolarının dili ve platforma özgü paket yöneticileri tooinstall ikili dosyaları ve bağımlılıkları geliştirme makinenizde kullanma hakkında bilgi için bkz.
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a>İşletim sistemi platformu ve donanım uyumluluğu

Merhaba belirli donanım aygıtları ile SDK uyumluluğu hakkında daha fazla bilgi için bkz: [Azure IOT cihaz katalog için onaylanmıştır][lnk-certified].

## <a name="azure-iot-service-sdks"></a>Azure IOT hizmeti SDK'ları

Hello Azure IOT hizmeti SDK'ları doğrudan IOT Hub toomanage cihazları ve güvenlik etkileşime uygulamaları derleme kodu toofacilitate içerir.

Merhaba aşağıdaki Azure IOT hizmeti SDK'ları github'dan kullanılabilir toodownload şunlardır:

* [.NET için Azure IOT hizmeti SDK'sı][lnk-dotnet-service-sdk]
* [Node.js için Azure IOT hizmeti SDK'sı][lnk-node-service-sdk]
* [Java için Azure IOT hizmeti SDK'sı][lnk-java-service-sdk]
* [Python için Azure IOT hizmeti SDK'sı][lnk-python-service-sdk]
* [C için Azure IOT hizmeti SDK'sı][lnk-c-service-sdk]

> [!NOTE]
> Merhaba readme dosyalarında hello GitHub depolarının dili ve platforma özgü paket yöneticileri tooinstall ikili dosyaları ve bağımlılıkları geliştirme makinenizde kullanma hakkında bilgi için bkz.

## <a name="azure-iot-edge"></a>Azure IoT Edge

Azure IOT kenar hello altyapı ve modülleri toocreate IOT ağ geçidi çözümleri içerir. IOT kenar toocreate ağ geçitleri uyarlanmış tooany uçtan uca senaryoyu da genişletebilirsiniz.

İndirebilirsiniz [Azure IOT kenar] [ lnk-iot-edge] github'dan.

## <a name="online-api-reference-documentation"></a>Çevrimiçi API başvuru belgeleri

Merhaba aşağıdaki listede bağlantılar tooonline API başvuru belgeleri Azure IOT cihaz, hizmet ve ağ geçidi kitaplıkları içerir:

* [Nesnelerin interneti (IOT) .NET][lnk-dotnet-ref]
* [IOT hub'ı REST][lnk-rest-ref]
* [C için Azure IOT cihaz SDK'sı][lnk-c-ref]
* [Java için Azure IOT cihaz SDK'sı][lnk-java-ref]
* [Java için Azure IOT hizmeti SDK'sı][lnk-java-service-ref]
* [Node.js için Azure IOT cihaz SDK'sı][lnk-node-ref]
* [Node.js için Azure IOT hizmeti SDK'sı][lnk-node-service-ref]
* [Azure IOT kenar][lnk-gateway-ref]

## <a name="next-steps"></a>Sonraki adımlar

Bu IOT Hub Geliştirici Kılavuzu'ndaki diğer başvuru konuları içerir:

* [IOT Hub uç noktaları][lnk-devguide-endpoints]
* [Cihaz çiftlerini, işler ve ileti yönlendirme için IOT hub'ı sorgulama dili][lnk-devguide-query]
* [Kotalar ve azaltma][lnk-devguide-quotas]
* [IOT Hub MQTT desteği][lnk-devguide-mqtt]

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-c-service-sdk]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_service_client
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-iot-edge]: https://github.com/Azure/iot-edge

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-gateway-ref]: http://azure.github.io/iot-edge/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
