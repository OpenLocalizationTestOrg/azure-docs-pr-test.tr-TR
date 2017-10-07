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
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-python"></a><span data-ttu-id="7de16-104">Python kullanarak sanal cihaz tooyour IOT hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="7de16-104">Connect your simulated device tooyour IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="7de16-105">Bu öğreticinin Hello sonunda, iki Python uygulamaları olacaktır:</span><span class="sxs-lookup"><span data-stu-id="7de16-105">At hello end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="7de16-106">**CreateDeviceIdentity.py**ilişkili güvenlik anahtarı tooconnect sanal cihaz uygulamanız ve bir cihaz kimliği oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7de16-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="7de16-107">**SimulatedDevice.py**daha önce oluşturulan hello cihaz kimliğiyle IOT hub'ı tooyour bağlanır ve düzenli aralıklarla bir telemetri iletisi hello MQTT protokolünü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="7de16-107">**SimulatedDevice.py**, which connects tooyour IoT hub with hello device identity created earlier, and periodically sends a telemetry message using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="7de16-108">Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] aygıtlar ve çözüm arka ucunuz hem uygulamalar toorun toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="7de16-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="7de16-109">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="7de16-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="7de16-110">[Python 2.x veya 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="7de16-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="7de16-111">Emin toouse hello 32 bit veya 64 bit yükleme kurulumunuzu gerektirdiği olun.</span><span class="sxs-lookup"><span data-stu-id="7de16-111">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="7de16-112">Merhaba yükleme sırasında istendiğinde emin tooadd Python tooyour platforma özgü ortam değişkeni olun.</span><span class="sxs-lookup"><span data-stu-id="7de16-112">When prompted during hello installation, make sure tooadd Python tooyour platform-specific environment variable.</span></span> <span data-ttu-id="7de16-113">Python kullanılıyorsa 2.x ihtiyacınız olabilecek çok[yüklemek veya yükseltmek *PIP*, hello Python paket yönetim sistemi][lnk-install-pip].</span><span class="sxs-lookup"><span data-stu-id="7de16-113">If you are using Python 2.x, you may need too[install or upgrade *pip*, hello Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="7de16-114">Windows işletim sistemi, ardından kullanıyorsanız [Visual C++ yeniden dağıtılabilir paketi] [ lnk-visual-c-redist] python'dan Yerel DLL'leri tooallow hello kullanımı.</span><span class="sxs-lookup"><span data-stu-id="7de16-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] tooallow hello use of native DLLs from Python.</span></span>
* <span data-ttu-id="7de16-115">[Node.js 4.0 veya üstü][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="7de16-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="7de16-116">Emin toouse hello 32 bit veya 64 bit yükleme kurulumunuzu gerektirdiği olun.</span><span class="sxs-lookup"><span data-stu-id="7de16-116">Make sure toouse hello 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="7de16-117">Gerekli tooinstall hello budur [IOT Hub Explorer aracı][lnk-iot-hub-explorer].</span><span class="sxs-lookup"><span data-stu-id="7de16-117">This is needed tooinstall hello [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="7de16-118">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="7de16-118">An active Azure account.</span></span> <span data-ttu-id="7de16-119">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7de16-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="7de16-120">Merhaba *PIP* için paketler `azure-iothub-service-client` ve `azure-iothub-device-client` şu anda yalnızca Windows işletim sistemi için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7de16-120">hello *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="7de16-121">Linux/Mac OS için lütfen hello toohello Linux ve Mac OS özgü bölümlere bakın [için Python geliştirme ortamınızı hazırlama] [ lnk-python-devbox] gönderin.</span><span class="sxs-lookup"><span data-stu-id="7de16-121">For Linux/Mac OS, please refer toohello Linux and Mac OS-specific sections on hello [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="7de16-122">IoT Hub’ınızı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="7de16-122">You have now created your IoT hub.</span></span> <span data-ttu-id="7de16-123">Merhaba IOT Hub ana bilgisayar adı ve hello IOT Hub bağlantı dizesine Bu öğreticinin hello kalan kullanın.</span><span class="sxs-lookup"><span data-stu-id="7de16-123">Use hello IoT Hub host name and hello IoT Hub connection string in hello rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="7de16-124">Azure CLI Node.js tabanlı veya hello Python kullanarak IOT hub'ınızı komut satırında, ayrıca kolayca oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7de16-124">You can also easily create your IoT hub on a command line, using hello Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="7de16-125">Merhaba makale [hello Azure CLI 2.0 kullanarak IOT hub oluşturma] [ lnk-azure-cli-hub] , hello hızlı adımlar toodo şekilde gösterir.</span><span class="sxs-lookup"><span data-stu-id="7de16-125">hello article [Create an IoT hub using hello Azure CLI 2.0][lnk-azure-cli-hub] shows you hello quick steps toodo so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="7de16-126">Cihaz kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="7de16-126">Create a device identity</span></span>
<span data-ttu-id="7de16-127">Bu bölümde hello adımları toocreate IOT hub'ınızın hello kimlik kayıt defterinde bir cihaz kimliği oluşturan bir Python konsol uygulaması listelenir.</span><span class="sxs-lookup"><span data-stu-id="7de16-127">This section lists hello steps toocreate a Python console app, that creates a device identity in hello identity registry of your IoT hub.</span></span> <span data-ttu-id="7de16-128">Bir aygıt tooIoT Hub hello kimlik kayıt defterinde girişi olmayan yalnızca bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7de16-128">A device can only connect tooIoT Hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="7de16-129">Daha fazla bilgi için bkz: Merhaba **kimlik kayıt defteri** hello bölümünü [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="7de16-129">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="7de16-130">Bu konsol uygulamasını çalıştırdığınızda, benzersiz cihaz kimliği oluşturur ve cihaz bulut gönderdiğinde Cihazınızı tooidentify kendisini kullanabileceğiniz anahtar tooIoT Hub iletileri.</span><span class="sxs-lookup"><span data-stu-id="7de16-130">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="7de16-131">Bir komut istemi açın ve hello yükleme **Python için Azure IOT Hub hizmeti SDK**.</span><span class="sxs-lookup"><span data-stu-id="7de16-131">Open a command prompt and install hello **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="7de16-132">Merhaba SDK yükledikten sonra hello komut istemini kapatın.</span><span class="sxs-lookup"><span data-stu-id="7de16-132">Close hello command prompt after you install hello SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="7de16-133">**CreateDeviceIdentity.py** adlı bir Python dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7de16-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="7de16-134">İçinde açmak [tercih ettiğiniz Python Düzenleyicisi/IDE][lnk-python-ide-list], örneğin, varsayılan hello [boşta][lnk-idle].</span><span class="sxs-lookup"><span data-stu-id="7de16-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, hello default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="7de16-135">Kod tooimport gerekli hello modülleri SDK hello hizmetinden aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7de16-135">Add hello following code tooimport hello required modules from hello service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="7de16-136">Aşağıdaki kod, hello yer tutucu değiştirme hello eklemek `[IoTHub Connection String]` hello IOT hub'ı hello önceki bölümde oluşturduğunuz için hello bağlantı dizesiyle.</span><span class="sxs-lookup"><span data-stu-id="7de16-136">Add hello following code, replacing hello placeholder for `[IoTHub Connection String]` with hello connection string for hello IoT hub you created in hello previous section.</span></span> <span data-ttu-id="7de16-137">Herhangi bir ad hello kullanabilirsiniz `DEVICE_ID`.</span><span class="sxs-lookup"><span data-stu-id="7de16-137">You can use any name as hello `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="7de16-138">Add işlevi tooprint bazı hello aygıt bilgileri hello.</span><span class="sxs-lookup"><span data-stu-id="7de16-138">Add hello following function tooprint some of hello device information.</span></span>

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
3. <span data-ttu-id="7de16-139">İşlev toocreate hello cihaz kimliği Hello kayıt Yöneticisi'ni kullanarak aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7de16-139">Add hello following function toocreate hello device identification using hello Registry Manager.</span></span> 

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
4. <span data-ttu-id="7de16-140">Son olarak, hello main işlevi aşağıdaki şekilde ekleyin ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7de16-140">Finally, add hello main function as follows and save hello file.</span></span>

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
5. <span data-ttu-id="7de16-141">Merhaba Hello komut isteminde, çalıştırmak **CreateDeviceIdentity.py** gibi:</span><span class="sxs-lookup"><span data-stu-id="7de16-141">On hello command prompt, run hello **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="7de16-142">Oluşturulan hello sanal cihaz görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7de16-142">You should see hello simulated device getting created.</span></span> <span data-ttu-id="7de16-143">Merhaba Not **DeviceID** ve hello **primaryKey** bu aygıtın.</span><span class="sxs-lookup"><span data-stu-id="7de16-143">Note down hello **deviceId** and hello **primaryKey** of this device.</span></span> <span data-ttu-id="7de16-144">TooIoT hub'a bir cihaz olarak bağlanan bir uygulama oluşturduğunuzda, bu değerleri daha sonra gerekir.</span><span class="sxs-lookup"><span data-stu-id="7de16-144">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

    ![Cihaz başarısı oluşturma][1]

> [!NOTE]
> <span data-ttu-id="7de16-146">Merhaba IOT Hub kimlik kayıt defteri, yalnızca cihaz kimlikleri tooenable güvenli erişim toohello IOT hub'ı depolar.</span><span class="sxs-lookup"><span data-stu-id="7de16-146">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="7de16-147">Cihaz kimliklerini ve anahtarlarını toouse güvenlik kimlik bilgileri ve toodisable erişim için tek bir cihaza kullanabilirsiniz bir etkin/devre dışı bayrağını depolar.</span><span class="sxs-lookup"><span data-stu-id="7de16-147">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="7de16-148">Uygulamanızın cihaza özgü diğer meta verileri toostore gerekiyorsa, bir uygulamaya özgü depo kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7de16-148">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="7de16-149">Daha fazla bilgi için bkz: Merhaba [IOT Hub Geliştirici Kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="7de16-149">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="7de16-150">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7de16-150">Create a simulated device app</span></span>
<span data-ttu-id="7de16-151">Bu bölümde hello adımları toocreate bir cihaza benzetim ve tooyour IOT hub'ı cihaz-bulut iletileri gönderen bir Python konsol uygulaması listelenir.</span><span class="sxs-lookup"><span data-stu-id="7de16-151">This section lists hello steps toocreate a Python console app, that simulates a device and sends device-to-cloud messages tooyour IoT hub.</span></span>

1. <span data-ttu-id="7de16-152">Yeni bir komut istemi açın ve Python gibi hello Azure IOT Hub cihaz SDK'sı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7de16-152">Open a new command prompt and install hello Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="7de16-153">Merhaba yüklendikten sonra Hello komut istemini kapatın.</span><span class="sxs-lookup"><span data-stu-id="7de16-153">Close hello command prompt after hello installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="7de16-154">**SimulatedDevice.py** adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7de16-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="7de16-155">Bu dosyayı, kendi seçiminize bağlı olarak Python düzenleyicisinde/IDE’de açın (örneğin, IDLE).</span><span class="sxs-lookup"><span data-stu-id="7de16-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="7de16-156">Kod tooimport gerekli hello modülleri SDK hello aygıttan aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7de16-156">Add hello following code tooimport hello required modules from hello device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="7de16-157">Hello aşağıdaki kod ve değiştirmek için hello yer tutucu eklemek `[IoTHub Device Connection String]` cihazınız için başlangıç bağlantı dizesiyle.</span><span class="sxs-lookup"><span data-stu-id="7de16-157">Add hello following code and replace hello placeholder for `[IoTHub Device Connection String]` with hello connection string for your device.</span></span> <span data-ttu-id="7de16-158">Merhaba cihaz bağlantı dizesidir genellikle hello biçiminde `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span><span class="sxs-lookup"><span data-stu-id="7de16-158">hello device connection string is usually in hello format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="7de16-159">Kullanım hello **DeviceID** ve **primaryKey** önceki bölümde tooreplace hello hello oluşturduğunuz hello cihazın `<deviceId>` ve `<primaryKey>` sırasıyla.</span><span class="sxs-lookup"><span data-stu-id="7de16-159">Use hello **deviceId** and **primaryKey** of hello device you created in hello previous section tooreplace hello `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="7de16-160">`<hostName>` değerini IoT hub'ınızın konak adıyla (çoğunlukla `<IoT hub name>.azure-devices.net` gibi) değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7de16-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

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
5. <span data-ttu-id="7de16-161">Aşağıdaki kod toodefine gönderme onayı geri çağırma hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7de16-161">Add hello following code toodefine a send confirmation callback.</span></span> 

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
6. <span data-ttu-id="7de16-162">Kod tooinitialize hello aygıt istemcisi aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7de16-162">Add hello following code tooinitialize hello device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set hello time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="7de16-163">Merhaba aşağıdaki tooformat işlev ve sanal cihaz tooyour IOT hub'dan ileti gönderme ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7de16-163">Add hello following function tooformat and send a message from your simulated device tooyour IoT hub.</span></span>

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
8. <span data-ttu-id="7de16-164">Son olarak, hello main işlevi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="7de16-164">Finally, add hello main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using hello Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="7de16-165">Kaydet ve Kapat hello **SimulatedDevice.py** dosya.</span><span class="sxs-lookup"><span data-stu-id="7de16-165">Save and close hello **SimulatedDevice.py** file.</span></span> <span data-ttu-id="7de16-166">Bu uygulama artık hazır toorun şunlardır.</span><span class="sxs-lookup"><span data-stu-id="7de16-166">You are now ready toorun this app.</span></span>

> [!NOTE]
> <span data-ttu-id="7de16-167">tookeep şeyler basit, Bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="7de16-167">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="7de16-168">Üretim kodunda yeniden deneme ilkelerini (üstel geri alma), önerilen hello MSDN makalesinde uygulamalıdır [geçici hata işleme][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="7de16-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="7de16-169">Sanal cihazınızdan ileti alma</span><span class="sxs-lookup"><span data-stu-id="7de16-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="7de16-170">tooreceive telemetri iletilerini cihazınızdan toouse gereken bir [Event Hubs][lnk-event-hubs-overview]-hello hello cihaz bulut iletilerini okuyan IOT Hub tarafından kullanıma sunulan uyumlu bir uç noktasını.</span><span class="sxs-lookup"><span data-stu-id="7de16-170">tooreceive telemetry messages from your device, you need toouse an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by hello IoT Hub, which reads hello device-to-cloud messages.</span></span> <span data-ttu-id="7de16-171">Okuma hello [Event Hubs ile çalışmaya başlama] [ lnk-eventhubs-tutorial] nasıl tooprocess, IOT hub'ın Event Hub ile uyumlu uç noktası için olay hub'larından iletileri hakkında bilgi için Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7de16-171">Read hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how tooprocess messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="7de16-172">Olay hub'ları desteklemez telemetri Python içinde henüz oluşturabilir ya da şekilde bir [Node.js](iot-hub-node-node-getstarted.md#D2C_node) veya [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) olay hub'ları tabanlı bir konsol uygulama tooread hello cihaz bulut iletilerini IOT hub'dan.</span><span class="sxs-lookup"><span data-stu-id="7de16-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app tooread hello device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="7de16-173">Bu öğretici hello nasıl kullanabileceğinizi gösterir [IOT Hub Explorer aracı] [ lnk-iot-hub-explorer] tooread bu cihaz iletiler.</span><span class="sxs-lookup"><span data-stu-id="7de16-173">This tutorial shows how you can use hello [IoT Hub Explorer tool][lnk-iot-hub-explorer] tooread these device messages.</span></span>

1. <span data-ttu-id="7de16-174">Bir komut istemi açın ve hello IOT Hub Explorer yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7de16-174">Open a command prompt and install hello IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="7de16-175">Merhaba komut istemi komutu aşağıdaki hello çalıştırmak, toobegin izleme hello cihaz bulut iletilerini cihazınızdan.</span><span class="sxs-lookup"><span data-stu-id="7de16-175">Run hello following command on hello command prompt, toobegin monitoring hello device-to-cloud messages from your device.</span></span> <span data-ttu-id="7de16-176">Merhaba yer tutucu sonra IOT hub'ın bağlantı dizesi kullanmak `--login`.</span><span class="sxs-lookup"><span data-stu-id="7de16-176">Use your IoT hub's connection string in hello placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="7de16-177">Yeni bir komut istemi açın ve hello içeren toohello dizinine gidin **SimulatedDevice.py** dosya.</span><span class="sxs-lookup"><span data-stu-id="7de16-177">Open a new command prompt and navigate toohello directory containing hello **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="7de16-178">Merhaba çalıştırmak **SimulatedDevice.py** telemetri verileri tooyour IOT hub'ı düzenli aralıklarla gönderir dosya.</span><span class="sxs-lookup"><span data-stu-id="7de16-178">Run hello **SimulatedDevice.py** file, which periodically sends telemetry data tooyour IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="7de16-179">Merhaba komut istemi hello IOT Hub Explorer hello önceki bölümden çalıştıran Hello aygıt iletileri gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="7de16-179">Observe hello device messages on hello command prompt running hello IoT Hub Explorer from hello previous section.</span></span> 

    ![Python cihazdan buluta iletiler][2]

## <a name="next-steps"></a><span data-ttu-id="7de16-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7de16-181">Next steps</span></span>
<span data-ttu-id="7de16-182">Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="7de16-182">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="7de16-183">Bu cihaz kimliğini tooenable benzetimli hello cihaz uygulama toosend cihaz bulut iletilerini toohello IOT hub kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7de16-183">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="7de16-184">Merhaba IOT Hub Explorer Aracı'nın hello Yardım hello IOT hub tarafından alınan karışılama iletileri gözlenen.</span><span class="sxs-lookup"><span data-stu-id="7de16-184">You observed hello messages received by hello IoT hub with hello help of hello IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="7de16-185">derinlemesine, Azure IOT Hub kullanım için tooexplore hello Python SDK ziyaret [bu Git Hub depodaki][lnk-python-github].</span><span class="sxs-lookup"><span data-stu-id="7de16-185">tooexplore hello Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="7de16-186">tooreview hello ileti özelliklerini hello Python için Azure IOT Hub hizmeti SDK, indirme ve çalıştırma [iothub_messaging_sample.py][lnk-messaging-sample].</span><span class="sxs-lookup"><span data-stu-id="7de16-186">tooreview hello messaging capabilities of hello Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="7de16-187">Python için Azure IOT Hub cihaz SDK'sı Hello kullanarak aygıt yan benzetimi için karşıdan yükleme ve hello çalıştırma [iothub_client_sample.py][lnk-client-sample].</span><span class="sxs-lookup"><span data-stu-id="7de16-187">For device side simulation using hello Azure IoT Hub Device SDK for Python, you can download and run hello [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="7de16-188">Başlarken toocontinue IOT Hub ve tooexplore diğer IOT senaryolarını bakın:</span><span class="sxs-lookup"><span data-stu-id="7de16-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="7de16-189">[Cihazınızı bağlama][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="7de16-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="7de16-190">[Cihaz yönetimini kullanmaya başlama][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="7de16-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="7de16-191">[Azure IoT Edge’i kullanmaya başlama][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="7de16-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="7de16-192">toolearn tooextend, IOT çözümü ve işlem cihaz bulut iletilerini ölçekli olarak nasıl görürüm hello [cihaz-bulut iletileri] [ lnk-process-d2c-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="7de16-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
