---
title: "aaaGet başlatılan Azure IOT Hub (Python) | Microsoft Docs"
description: "Nasıl tooAzure IOT Hub'ın IOT SDK'ları için Python kullanarak toosend cihaz-bulut iletileri öğrenin. Sanal cihazı ve hizmet uygulamaları tooregister Cihazınızı oluşturmak, iletileri gönderir ve IOT hub'ından iletileri okur."
services: iot-hub
author: dsk-2015
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: python
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: dkshir
ms.custom: na
ms.openlocfilehash: aa23e792fb144202e121274723bcfaeae0c04723
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a>Python kullanarak sanal cihaz tooyour IOT hub'ınıza bağlanın
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Bu öğreticinin Hello sonunda, iki Python uygulamaları olacaktır:

* **CreateDeviceIdentity.py**ilişkili güvenlik anahtarı tooconnect sanal cihaz uygulamanız ve bir cihaz kimliği oluşturur.
* **SimulatedDevice.py**daha önce oluşturulan hello cihaz kimliğiyle IOT hub'ı tooyour bağlanır ve düzenli aralıklarla bir telemetri iletisi hello MQTT protokolünü kullanarak.

> [!NOTE]
> Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] aygıtlar ve çözüm arka ucunuz hem uygulamalar toorun toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlar.
> 
> 

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* [Python 2.x veya 3.x][lnk-python-download]. Emin toouse hello 32 bit veya 64 bit yükleme kurulumunuzu gerektirdiği olun. Merhaba yükleme sırasında istendiğinde emin tooadd Python tooyour platforma özgü ortam değişkeni olun. Python kullanılıyorsa 2.x ihtiyacınız olabilecek çok[yüklemek veya yükseltmek *PIP*, hello Python paket yönetim sistemi][lnk-install-pip].
* Windows işletim sistemi, ardından kullanıyorsanız [Visual C++ yeniden dağıtılabilir paketi] [ lnk-visual-c-redist] python'dan Yerel DLL'leri tooallow hello kullanımı.
* [Node.js 4.0 veya üstü][lnk-node-download]. Emin toouse hello 32 bit veya 64 bit yükleme kurulumunuzu gerektirdiği olun. Gerekli tooinstall hello budur [IOT Hub Explorer aracı][lnk-iot-hub-explorer].
* Etkin bir Azure hesabı. Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.

> [!NOTE]
> Merhaba *PIP* için paketler `azure-iothub-service-client` ve `azure-iothub-device-client` şu anda yalnızca Windows işletim sistemi için kullanılabilir. Linux/Mac OS için lütfen hello toohello Linux ve Mac OS özgü bölümlere bakın [için Python geliştirme ortamınızı hazırlama] [ lnk-python-devbox] gönderin.
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

IoT Hub’ınızı oluşturdunuz. Merhaba IOT Hub ana bilgisayar adı ve hello IOT Hub bağlantı dizesine Bu öğreticinin hello kalan kullanın.

> [!NOTE]
> Azure CLI Node.js tabanlı veya hello Python kullanarak IOT hub'ınızı komut satırında, ayrıca kolayca oluşturabilirsiniz. Merhaba makale [hello Azure CLI 2.0 kullanarak IOT hub oluşturma] [ lnk-azure-cli-hub] , hello hızlı adımlar toodo şekilde gösterir. 
> 

## <a name="create-a-device-identity"></a>Cihaz kimliği oluşturma
Bu bölümde hello adımları toocreate IOT hub'ınızın hello kimlik kayıt defterinde bir cihaz kimliği oluşturan bir Python konsol uygulaması listelenir. Bir aygıt tooIoT Hub hello kimlik kayıt defterinde girişi olmayan yalnızca bağlayabilirsiniz. Daha fazla bilgi için bkz: Merhaba **kimlik kayıt defteri** hello bölümünü [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity]. Bu konsol uygulamasını çalıştırdığınızda, benzersiz cihaz kimliği oluşturur ve cihaz bulut gönderdiğinde Cihazınızı tooidentify kendisini kullanabileceğiniz anahtar tooIoT Hub iletileri.

1. Bir komut istemi açın ve hello yükleme **Python için Azure IOT Hub hizmeti SDK**. Merhaba SDK yükledikten sonra hello komut istemini kapatın.

    ```
    pip install azure-iothub-service-client
    ```

2. **CreateDeviceIdentity.py** adlı bir Python dosyası oluşturun. İçinde açmak [tercih ettiğiniz Python Düzenleyicisi/IDE][lnk-python-ide-list], örneğin, varsayılan hello [boşta][lnk-idle].

3. Kod tooimport gerekli hello modülleri SDK hello hizmetinden aşağıdaki hello ekleyin:

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. Aşağıdaki kod, hello yer tutucu değiştirme hello eklemek `[IoTHub Connection String]` hello IOT hub'ı hello önceki bölümde oluşturduğunuz için hello bağlantı dizesiyle. Herhangi bir ad hello kullanabilirsiniz `DEVICE_ID`.
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. Add işlevi tooprint bazı hello aygıt bilgileri hello.

    ```python
    def print_device_info(title, iothub_device):
        print ( title + ":" )
        print ( "iothubDevice.deviceId                    = {0}".format(iothub_device.deviceId) )
        print ( "iothubDevice.primaryKey                  = {0}".format(iothub_device.primaryKey) )
        print ( "iothubDevice.secondaryKey                = {0}".format(iothub_device.secondaryKey) )
        print ( "iothubDevice.connectionState             = {0}".format(iothub_device.connectionState) )
        print ( "iothubDevice.status                      = {0}".format(iothub_device.status) )
        print ( "iothubDevice.lastActivityTime            = {0}".format(iothub_device.lastActivityTime) )
        print ( "iothubDevice.cloudToDeviceMessageCount   = {0}".format(iothub_device.cloudToDeviceMessageCount) )
        print ( "iothubDevice.isManaged                   = {0}".format(iothub_device.isManaged) )
        print ( "iothubDevice.authMethod                  = {0}".format(iothub_device.authMethod) )
        print ( "" )
    ```
3. İşlev toocreate hello cihaz kimliği Hello kayıt Yöneticisi'ni kullanarak aşağıdaki hello ekleyin. 

    ```python
    def iothub_createdevice():
        try:
            iothub_registry_manager = IoTHubRegistryManager(CONNECTION_STRING)
            auth_method = IoTHubRegistryManagerAuthMethod.SHARED_PRIVATE_KEY
            new_device = iothub_registry_manager.create_device(DEVICE_ID, "", "", auth_method)
            print_device_info("CreateDevice", new_device)

        except IoTHubError as iothub_error:
            print ( "Unexpected error {0}".format(iothub_error) )
            return
        except KeyboardInterrupt:
            print ( "iothub_createdevice stopped" )
    ```
4. Son olarak, hello main işlevi aşağıdaki şekilde ekleyin ve hello dosyasını kaydedin.

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using hello Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. Merhaba Hello komut isteminde, çalıştırmak **CreateDeviceIdentity.py** gibi:

    ```python
    python CreateDeviceIdentity.py
    ```
6. Oluşturulan hello sanal cihaz görmeniz gerekir. Merhaba Not **DeviceID** ve hello **primaryKey** bu aygıtın. TooIoT hub'a bir cihaz olarak bağlanan bir uygulama oluşturduğunuzda, bu değerleri daha sonra gerekir.

    ![Cihaz başarısı oluşturma][1]

> [!NOTE]
> Merhaba IOT Hub kimlik kayıt defteri, yalnızca cihaz kimlikleri tooenable güvenli erişim toohello IOT hub'ı depolar. Cihaz kimliklerini ve anahtarlarını toouse güvenlik kimlik bilgileri ve toodisable erişim için tek bir cihaza kullanabilirsiniz bir etkin/devre dışı bayrağını depolar. Uygulamanızın cihaza özgü diğer meta verileri toostore gerekiyorsa, bir uygulamaya özgü depo kullanması gerekir. Daha fazla bilgi için bkz: Merhaba [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity].
> 
> 


## <a name="create-a-simulated-device-app"></a>Sanal cihaz uygulaması oluşturma
Bu bölümde hello adımları toocreate bir cihaza benzetim ve tooyour IOT hub'ı cihaz-bulut iletileri gönderen bir Python konsol uygulaması listelenir.

1. Yeni bir komut istemi açın ve Python gibi hello Azure IOT Hub cihaz SDK'sı yükleyin. Merhaba yüklendikten sonra Hello komut istemini kapatın.

    ```
    pip install azure-iothub-device-client
    ```
2. **SimulatedDevice.py** adlı bir dosya oluşturun. Bu dosyayı, kendi seçiminize bağlı olarak Python düzenleyicisinde/IDE’de açın (örneğin, IDLE).

3. Kod tooimport gerekli hello modülleri SDK hello aygıttan aşağıdaki hello ekleyin.

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. Hello aşağıdaki kod ve değiştirmek için hello yer tutucu eklemek `[IoTHub Device Connection String]` cihazınız için başlangıç bağlantı dizesiyle. Merhaba cihaz bağlantı dizesidir genellikle hello biçiminde `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`. Kullanım hello **DeviceID** ve **primaryKey** önceki bölümde tooreplace hello hello oluşturduğunuz hello cihazın `<deviceId>` ve `<primaryKey>` sırasıyla. `<hostName>` değerini IoT hub'ınızın konak adıyla (çoğunlukla `<IoT hub name>.azure-devices.net` gibi) değiştirin.

    ```python
    # String containing Hostname, Device Id & Device Key in hello format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. Aşağıdaki kod toodefine gönderme onayı geri çağırma hello ekleyin. 

    ```python
    def send_confirmation_callback(message, result, user_context):
        global SEND_CALLBACKS
        print ( "Confirmation[%d] received for message with result = %s" % (user_context, result) )
        map_properties = message.properties()
        print ( "    message_id: %s" % message.message_id )
        print ( "    correlation_id: %s" % message.correlation_id )
        key_value_pair = map_properties.get_internals()
        print ( "    Properties: %s" % key_value_pair )
        SEND_CALLBACKS += 1
        print ( "    Total calls confirmed: %d" % SEND_CALLBACKS )
    ```
6. Kod tooinitialize hello aygıt istemcisi aşağıdaki hello ekleyin.

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. Merhaba aşağıdaki tooformat işlev ve sanal cihaz tooyour IOT hub'dan ileti gönderme ekleyin.

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C tooexit" )
            message_counter = 0

            while True:
                msg_txt_formatted = MSG_TXT % (AVG_WIND_SPEED + (random.random() * 4 + 2))
                # messages can be encoded as string or bytearray
                if (message_counter & 1) == 1:
                    message = IoTHubMessage(bytearray(msg_txt_formatted, 'utf8'))
                else:
                    message = IoTHubMessage(msg_txt_formatted)
                # optional: assign ids
                message.message_id = "message_%d" % message_counter
                message.correlation_id = "correlation_%d" % message_counter
                # optional: assign properties
                prop_map = message.properties()
                prop_text = "PropMsg_%d" % message_counter
                prop_map.add("Property", prop_text)

                client.send_event_async(message, send_confirmation_callback, message_counter)
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission tooIoT Hub." % message_counter )

                status = client.get_send_status()
                print ( "Send status: %s" % status )
                time.sleep(30)

                status = client.get_send_status()
                print ( "Send status: %s" % status )

                message_counter += 1

        except IoTHubError as iothub_error:
            print ( "Unexpected error %s from IoTHub" % iothub_error )
            return
        except KeyboardInterrupt:
            print ( "IoTHubClient sample stopped" )
    ```
8. Son olarak, hello main işlevi ekleyin. 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. Kaydet ve Kapat hello **SimulatedDevice.py** dosya. Bu uygulama artık hazır toorun şunlardır.

> [!NOTE]
> tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz. Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a>Sanal cihazınızdan ileti alma
tooreceive telemetri iletilerini cihazınızdan toouse gereken bir [Event Hubs][lnk-event-hubs-overview]-hello hello cihaz bulut iletilerini okuyan IOT Hub tarafından kullanıma sunulan uyumlu bir uç noktasını. Okuma hello [Event Hubs ile çalışmaya başlama] [ lnk-eventhubs-tutorial] nasıl tooprocess, IOT hub'ın Event Hub ile uyumlu uç noktası için olay hub'larından iletileri hakkında bilgi için Öğreticisi. Olay hub'ları desteklemez telemetri Python içinde henüz oluşturabilir ya da şekilde bir [Node.js](iot-hub-node-node-getstarted.md#D2C_node) veya [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) olay hub'ları tabanlı bir konsol uygulama tooread hello cihaz bulut iletilerini IOT hub'dan. Bu öğretici hello nasıl kullanabileceğinizi gösterir [IOT Hub Explorer aracı] [ lnk-iot-hub-explorer] tooread bu cihaz iletiler.

1. Bir komut istemi açın ve hello IOT Hub Explorer yükleyin. 

    ```
    npm install -g iothub-explorer
    ```

2. Merhaba komut istemi komutu aşağıdaki hello çalıştırmak, toobegin izleme hello cihaz bulut iletilerini cihazınızdan. Merhaba yer tutucu sonra IOT hub'ın bağlantı dizesi kullanmak `--login`.

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. Yeni bir komut istemi açın ve hello içeren toohello dizinine gidin **SimulatedDevice.py** dosya.

4. Merhaba çalıştırmak **SimulatedDevice.py** telemetri verileri tooyour IOT hub'ı düzenli aralıklarla gönderir dosya. 
   
    ```
    python SimulatedDevice.py
    ```
5. Merhaba komut istemi hello IOT Hub Explorer hello önceki bölümden çalıştıran Hello aygıt iletileri gözlemleyin. 

    ![Python cihazdan buluta iletiler][2]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz. Bu cihaz kimliğini tooenable benzetimli hello cihaz uygulama toosend cihaz bulut iletilerini toohello IOT hub kullanılır. Merhaba IOT Hub Explorer Aracı'nın hello Yardım hello IOT hub tarafından alınan karışılama iletileri gözlenen. 

derinlemesine, Azure IOT Hub kullanım için tooexplore hello Python SDK ziyaret [bu Git Hub depodaki][lnk-python-github]. tooreview hello ileti özelliklerini hello Python için Azure IOT Hub hizmeti SDK, indirme ve çalıştırma [iothub_messaging_sample.py][lnk-messaging-sample]. Python için Azure IOT Hub cihaz SDK'sı Hello kullanarak aygıt yan benzetimi için karşıdan yükleme ve hello çalıştırma [iothub_client_sample.py][lnk-client-sample].

Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:

* [Cihazınızı bağlama][lnk-connect-device]
* [Cihaz yönetimini kullanmaya başlama][lnk-device-management]
* [Azure IoT Edge’i kullanmaya başlama][lnk-iot-edge]

toolearn tooextend, IOT çözümü ve işlem cihaz bulut iletilerini ölçekli olarak nasıl görürüm hello [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] Öğreticisi.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[1]: ./media/iot-hub-python-getstarted/createdevice.png
[2]: ./media/iot-hub-python-getstarted/sendd2cmessage.png

<!-- Links -->
[lnk-python-download]: https://www.python.org/downloads/
[lnk-visual-c-redist]: http://www.microsoft.com/download/confirmation.aspx?id=48145
[lnk-node-download]: https://nodejs.org/en/download/
[lnk-install-pip]: https://pip.pypa.io/en/stable/installing/
[lnk-azure-cli-hub]: https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-create-using-cli
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-idle]: https://docs.python.org/3/library/idle.html
[lnk-python-ide-list]: https://wiki.python.org/moin/IntegratedDevelopmentEnvironments
[lnk-iot-hub-explorer]: https://github.com/Azure/iothub-explorer
[lnk-python-github]: https://github.com/Azure/azure-iot-sdk-python
[lnk-messaging-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/service/samples/iothub_messaging_sample.py
[lnk-client-sample]: https://github.com/Azure/azure-iot-sdk-python/blob/master/device/samples/iothub_client_sample.py

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md
[lnk-python-devbox]: https://github.com/Azure/azure-iot-sdk-python/blob/master/doc/python-devbox-setup.md

[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
