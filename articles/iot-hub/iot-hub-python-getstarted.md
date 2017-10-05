---
title: "Azure IoT Hub'ı (Python) kullanmaya başlama | Microsoft Belgeleri"
description: "Python için IoT SDK’larını kullanarak Azure IoT Hub’a cihazdan buluta ileti göndermeyi öğrenin. IoT hub’a cihazınızı kaydetmek, ileti göndermek ve ileti okumak için sanal cihaz ve hizmet uygulamaları oluşturun."
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
ms.openlocfilehash: 7ebbac4464d793717f68a4cb7905c53d1f5c051a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-python"></a><span data-ttu-id="f3883-104">Python kullanarak sanal cihazınızı IoT hub’ınıza bağlama</span><span class="sxs-lookup"><span data-stu-id="f3883-104">Connect your simulated device to your IoT hub using Python</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="f3883-105">Bu öğreticinin sonunda iki Python uygulamanız olacaktır:</span><span class="sxs-lookup"><span data-stu-id="f3883-105">At the end of this tutorial, you will have two Python apps:</span></span>

* <span data-ttu-id="f3883-106">Bir cihaz kimliği ve sanal cihaz uygulamanızı bağlamak için ilişkili güvenlik anahtarı oluşturan **CreateDeviceIdentity.py**.</span><span class="sxs-lookup"><span data-stu-id="f3883-106">**CreateDeviceIdentity.py**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="f3883-107">Daha önce oluşturulan cihaz kimliğiyle IoT hub'ınızı bağlayan ve MQTT protokolünü kullanarak düzenli aralıklarla telemetri iletisi gönderen **SimulatedDevice.py**.</span><span class="sxs-lookup"><span data-stu-id="f3883-107">**SimulatedDevice.py**, which connects to your IoT hub with the device identity created earlier, and periodically sends a telemetry message using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="f3883-108">[IoT Hub SDK'ları][lnk-hub-sdks] makalesi, hem cihazlarınızda hem de çözüm arka ucunuzda çalıştırılacak uygulamalar oluşturmak için kullanabileceğiniz Azure IoT SDK’ları hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="f3883-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="f3883-109">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="f3883-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="f3883-110">[Python 2.x veya 3.x][lnk-python-download].</span><span class="sxs-lookup"><span data-stu-id="f3883-110">[Python 2.x or 3.x][lnk-python-download].</span></span> <span data-ttu-id="f3883-111">Kurulumunuzun gereksinimine uygun olarak 32 bit veya 64 bit yüklemeyi kullanmaya dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f3883-111">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="f3883-112">Yükleme sırasında istendiğinde, platforma özgü ortam değişkeninize Python’u eklediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f3883-112">When prompted during the installation, make sure to add Python to your platform-specific environment variable.</span></span> <span data-ttu-id="f3883-113">Python 2.x kullanıyorsanız, [Python paket yönetim sistemi *pip*’yi yüklemeniz veya yükseltmeniz][lnk-install-pip] gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f3883-113">If you are using Python 2.x, you may need to [install or upgrade *pip*, the Python package management system][lnk-install-pip].</span></span>
* <span data-ttu-id="f3883-114">Windows işletim sistemi kullanıyorsanız, Python’dan yerel DLL’lerin kullanımına olanak tanımak için [Visual C++ yeniden dağıtılabilir paketi][lnk-visual-c-redist].</span><span class="sxs-lookup"><span data-stu-id="f3883-114">If you are using Windows OS, then [Visual C++ redistributable package][lnk-visual-c-redist] to allow the use of native DLLs from Python.</span></span>
* <span data-ttu-id="f3883-115">[Node.js 4.0 veya üstü][lnk-node-download].</span><span class="sxs-lookup"><span data-stu-id="f3883-115">[Node.js 4.0 or later][lnk-node-download].</span></span> <span data-ttu-id="f3883-116">Kurulumunuzun gereksinimine uygun olarak 32 bit veya 64 bit yüklemeyi kullanmaya dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="f3883-116">Make sure to use the 32-bit or 64-bit installation as required by your setup.</span></span> <span data-ttu-id="f3883-117">Bu, [IoT Hub Gezgini aracını][lnk-iot-hub-explorer] yüklemek için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f3883-117">This is needed to install the [IoT Hub Explorer tool][lnk-iot-hub-explorer].</span></span>
* <span data-ttu-id="f3883-118">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="f3883-118">An active Azure account.</span></span> <span data-ttu-id="f3883-119">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3883-119">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

> [!NOTE]
> <span data-ttu-id="f3883-120">`azure-iothub-service-client` ve `azure-iothub-device-client` için *PIP* paketleri şu anda yalnızca Windows İşletim Sistemi için mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="f3883-120">The *pip* packages for `azure-iothub-service-client` and `azure-iothub-device-client` are currently available only for Windows OS.</span></span> <span data-ttu-id="f3883-121">Linux/macOS için lütfen [Python için geliştirme ortamınızı hazırlayın][lnk-python-devbox] makalesindeki Linux ve macOS ile ilgili bölümlere bakın.</span><span class="sxs-lookup"><span data-stu-id="f3883-121">For Linux/Mac OS, please refer to the Linux and Mac OS-specific sections on the [Prepare your development environment for Python][lnk-python-devbox] post.</span></span>
> 

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="f3883-122">IoT Hub’ınızı oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="f3883-122">You have now created your IoT hub.</span></span> <span data-ttu-id="f3883-123">Bu öğreticinin kalan bölümünde IoT Hub konak adını ve IoT Hub bağlantı dizesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f3883-123">Use the IoT Hub host name and the IoT Hub connection string in the rest of this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="f3883-124">Ayrıca, komut satırında Python veya Node.js tabanlı Azure CLI’yi kullanarak kolayca IoT hub’ınızı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3883-124">You can also easily create your IoT hub on a command line, using the Python or Node.js based Azure CLI.</span></span> <span data-ttu-id="f3883-125">[Azure CLI 2.0 kullanarak IoT hub’ı oluşturma][lnk-azure-cli-hub] makalesinde bunu yapmanın hızlı adımları gösterilir.</span><span class="sxs-lookup"><span data-stu-id="f3883-125">The article [Create an IoT hub using the Azure CLI 2.0][lnk-azure-cli-hub] shows you the quick steps to do so.</span></span> 
> 

## <a name="create-a-device-identity"></a><span data-ttu-id="f3883-126">Cihaz kimliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="f3883-126">Create a device identity</span></span>
<span data-ttu-id="f3883-127">Bu bölümde, IoT hub'ınızdaki kimlik kayıt defterinde cihaz kimliği oluşturan bir Python konsol uygulaması oluşturma adımları listelenir.</span><span class="sxs-lookup"><span data-stu-id="f3883-127">This section lists the steps to create a Python console app, that creates a device identity in the identity registry of your IoT hub.</span></span> <span data-ttu-id="f3883-128">Yalnızca kimlik kayıt defterinde girişi olan cihazlar IoT Hub'ına bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="f3883-128">A device can only connect to IoT Hub if it has an entry in the identity registry.</span></span> <span data-ttu-id="f3883-129">Daha fazla bilgi için [IoT Hub Geliştirici Kılavuzu][lnk-devguide-identity]'nun **Kimlik Kayıt Defteri** bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="f3883-129">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="f3883-130">Bu konsol uygulamasını çalıştırdığınızda, cihazınızın IoT Hub'a cihaz-bulut iletileri gönderdiğinde kendisini tanımlamak için kullanabileceği benzersiz bir cihaz kimliği ve anahtarı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f3883-130">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="f3883-131">Komut istemini açın ve **Python için Azure IoT Hub Hizmeti SDK’sını** aşağıda gösterildiği gibi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f3883-131">Open a command prompt and install the **Azure IoT Hub Service SDK for Python**.</span></span> <span data-ttu-id="f3883-132">SDK’yı yükledikten sonra komut istemini kapatın.</span><span class="sxs-lookup"><span data-stu-id="f3883-132">Close the command prompt after you install the SDK.</span></span>

    ```
    pip install azure-iothub-service-client
    ```

2. <span data-ttu-id="f3883-133">**CreateDeviceIdentity.py** adlı bir Python dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f3883-133">Create a Python file named **CreateDeviceIdentity.py**.</span></span> <span data-ttu-id="f3883-134">Bu dosyayı, [kendi seçiminize bağlı olarak Python düzenleyicisinde/IDE’de][lnk-python-ide-list], (örneğin, varsayılan [IDLE][lnk-idle]) açın.</span><span class="sxs-lookup"><span data-stu-id="f3883-134">Open it in [a Python editor/IDE of your choice][lnk-python-ide-list], for example, the default [IDLE][lnk-idle].</span></span>

3. <span data-ttu-id="f3883-135">Hizmet SDK’sından gerekli modülleri içeri aktarmak için aşağıdaki kodu ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f3883-135">Add the following code to import the required modules from the service SDK:</span></span>

    ```python
    import sys
    import iothub_service_client
    from iothub_service_client import IoTHubRegistryManager, IoTHubRegistryManagerAuthMethod
    from iothub_service_client import IoTHubDeviceStatus, IoTHubError
    ```
2. <span data-ttu-id="f3883-136">Aşağıdaki kodu ekleyerek `[IoTHub Connection String]` yer tutucusunu önceki bölümde oluşturduğunuz IoT hub'ının bağlantı dizesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f3883-136">Add the following code, replacing the placeholder for `[IoTHub Connection String]` with the connection string for the IoT hub you created in the previous section.</span></span> <span data-ttu-id="f3883-137">`DEVICE_ID` olarak herhangi bir ad kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3883-137">You can use any name as the `DEVICE_ID`.</span></span>
   
    ```python
    CONNECTION_STRING = "[IoTHub Connection String]"
    DEVICE_ID = "MyFirstPythonDevice"
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

3. <span data-ttu-id="f3883-138">Cihaz bilgilerinden bir bölümünü yazdırmak için aşağıdaki işlevi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3883-138">Add the following function to print some of the device information.</span></span>

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
3. <span data-ttu-id="f3883-139">Kayıt Defteri Yöneticisi’ni kullanarak cihaz kimliği oluşturmak için aşağıdaki işlevi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3883-139">Add the following function to create the device identification using the Registry Manager.</span></span> 

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
4. <span data-ttu-id="f3883-140">Son olarak, aşağıda gösterildiği gibi ana işlevi ekleyin ve dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="f3883-140">Finally, add the main function as follows and save the file.</span></span>

    ```python
    if __name__ == '__main__':
        print ( "" )
        print ( "Python {0}".format(sys.version) )
        print ( "Creating device using the Azure IoT Hub Service SDK for Python" )
        print ( "" )
        print ( "    Connection string = {0}".format(CONNECTION_STRING) )
        print ( "    Device ID         = {0}".format(DEVICE_ID) )

        iothub_createdevice()
    ```
5. <span data-ttu-id="f3883-141">Komut isteminde, aşağıda gösterildiği gibi **CreateDeviceIdentity.py** komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f3883-141">On the command prompt, run the **CreateDeviceIdentity.py** as follows:</span></span>

    ```python
    python CreateDeviceIdentity.py
    ```
6. <span data-ttu-id="f3883-142">Oluşturulmakta olan sanal cihazı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3883-142">You should see the simulated device getting created.</span></span> <span data-ttu-id="f3883-143">Cihazın **deviceId** ve **primaryKey** değerlerini not alın.</span><span class="sxs-lookup"><span data-stu-id="f3883-143">Note down the **deviceId** and the **primaryKey** of this device.</span></span> <span data-ttu-id="f3883-144">İleride IoT Hub'a bir cihaz olarak bağlanan bir uygulama oluşturduğunuzda bu değerlere ihtiyacınız olur.</span><span class="sxs-lookup"><span data-stu-id="f3883-144">You need these values later when you create an application that connects to IoT Hub as a device.</span></span>

    ![Cihaz başarısı oluşturma][1]

> [!NOTE]
> <span data-ttu-id="f3883-146">IoT Hub kimlik kayıt defteri, yalnızca IoT hub'ına güvenli erişim sağlamak amacıyla cihaz kimliklerini depolar.</span><span class="sxs-lookup"><span data-stu-id="f3883-146">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="f3883-147">Güvenlik kimlik bilgileri olarak kullanılmak üzere cihaz kimliklerini ve anahtarlarını ve tek bir cihaza erişimi devre dışı bırakmak için kullanabileceğiniz etkin/devre dışı bayrağını depolar.</span><span class="sxs-lookup"><span data-stu-id="f3883-147">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="f3883-148">Uygulamanızın cihaza özgü diğer meta verileri depolaması gerekiyorsa uygulamaya özgü bir depo kullanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3883-148">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="f3883-149">Daha fazla bilgi için bkz. [IoT Hub geliştirici kılavuzu][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="f3883-149">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="f3883-150">Sanal cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="f3883-150">Create a simulated device app</span></span>
<span data-ttu-id="f3883-151">Bu bölümde, IoT hub'ınızda cihazdan buluta iletiler gönderen ve cihaz benzetimi yapan bir Python konsol uygulaması oluşturma adımları listelenir.</span><span class="sxs-lookup"><span data-stu-id="f3883-151">This section lists the steps to create a Python console app, that simulates a device and sends device-to-cloud messages to your IoT hub.</span></span>

1. <span data-ttu-id="f3883-152">Yeni bir komut istemi açın ve Python için Azure IoT Hub Cihazı SDK’sını aşağıda gösterildiği gibi yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f3883-152">Open a new command prompt and install the Azure IoT Hub Device SDK for Python as follows.</span></span> <span data-ttu-id="f3883-153">Yükleme bittikten sonra komut istemini kapatın.</span><span class="sxs-lookup"><span data-stu-id="f3883-153">Close the command prompt after the installation.</span></span>

    ```
    pip install azure-iothub-device-client
    ```
2. <span data-ttu-id="f3883-154">**SimulatedDevice.py** adlı bir dosya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f3883-154">Create a file named **SimulatedDevice.py**.</span></span> <span data-ttu-id="f3883-155">Bu dosyayı, kendi seçiminize bağlı olarak Python düzenleyicisinde/IDE’de açın (örneğin, IDLE).</span><span class="sxs-lookup"><span data-stu-id="f3883-155">Open this file in a Python editor/IDE of your choice (for example, IDLE).</span></span>

3. <span data-ttu-id="f3883-156">Cihaz SDK’sından gerekli modülleri içeri aktarmak için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3883-156">Add the following code to import the required modules from the device SDK.</span></span>

    ```python
    import random
    import time
    import sys
    import iothub_client
    from iothub_client import IoTHubClient, IoTHubClientError, IoTHubTransportProvider, IoTHubClientResult
    from iothub_client import IoTHubMessage, IoTHubMessageDispositionResult, IoTHubError, DeviceMethodReturnValue
    ```
4. <span data-ttu-id="f3883-157">Aşağıdaki kodu ekleyin `[IoTHub Device Connection String]` yer tutucusunu cihazınızın bağlantı dizesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f3883-157">Add the following code and replace the placeholder for `[IoTHub Device Connection String]` with the connection string for your device.</span></span> <span data-ttu-id="f3883-158">Cihaz bağlantı dizesi çoğunlukla `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>` biçimindedir.</span><span class="sxs-lookup"><span data-stu-id="f3883-158">The device connection string is usually in the format of `HostName=<hostName>;DeviceId=<deviceId>;SharedAccessKey=<primaryKey>`.</span></span> <span data-ttu-id="f3883-159">`<deviceId>` ve `<primaryKey>` değerlerini sırasıyla önceki bölümde oluşturduğunuz cihazın **deviceId** ve **primaryKey** değerleriyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f3883-159">Use the **deviceId** and **primaryKey** of the device you created in the previous section to replace the `<deviceId>` and `<primaryKey>` respectively.</span></span> <span data-ttu-id="f3883-160">`<hostName>` değerini IoT hub'ınızın konak adıyla (çoğunlukla `<IoT hub name>.azure-devices.net` gibi) değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f3883-160">Replace `<hostName>` with your IoT hub's host name, usually as `<IoT hub name>.azure-devices.net`.</span></span>

    ```python
    # String containing Hostname, Device Id & Device Key in the format
    CONNECTION_STRING = "[IoTHub Device Connection String]"
    # choose HTTP, AMQP or MQTT as transport protocol
    PROTOCOL = IoTHubTransportProvider.MQTT
    MESSAGE_TIMEOUT = 10000
    AVG_WIND_SPEED = 10.0
    SEND_CALLBACKS = 0
    MSG_TXT = "{\"deviceId\": \"MyFirstPythonDevice\",\"windSpeed\": %.2f}"    
    ```
5. <span data-ttu-id="f3883-161">Gönderme onayı geri çevirmeyi tanımlamak için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3883-161">Add the following code to define a send confirmation callback.</span></span> 

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
6. <span data-ttu-id="f3883-162">Cihaz istemcisini başlatmak için aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3883-162">Add the following code to initialize the device client.</span></span>

    ```python
    def iothub_client_init():
        # prepare iothub client
        client = IoTHubClient(CONNECTION_STRING, PROTOCOL)
        # set the time until a message times out
        client.set_option("messageTimeout", MESSAGE_TIMEOUT)
        client.set_option("logtrace", 0)
        return client
    ```
7. <span data-ttu-id="f3883-163">Sanal cihazınızdan IoT hub’ınıza bir ileti biçimlendirmek ve göndermek için aşağıdaki işlevi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3883-163">Add the following function to format and send a message from your simulated device to your IoT hub.</span></span>

    ```python
    def iothub_client_telemetry_sample_run():

        try:
            client = iothub_client_init()
            print ( "IoT Hub device sending periodic messages, press Ctrl-C to exit" )
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
                print ( "IoTHubClient.send_event_async accepted message [%d] for transmission to IoT Hub." % message_counter )

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
8. <span data-ttu-id="f3883-164">Son olarak, ana işlevi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f3883-164">Finally, add the main function.</span></span> 

    ```python
    if __name__ == '__main__':
        print ( "Simulating a device using the Azure IoT Hub Device SDK for Python" )
        print ( "    Protocol %s" % PROTOCOL )
        print ( "    Connection string=%s" % CONNECTION_STRING )

        iothub_client_telemetry_sample_run()
    ```
9. <span data-ttu-id="f3883-165">**SimulatedDevice.py** dosyasını kaydedin ve kapatın.</span><span class="sxs-lookup"><span data-stu-id="f3883-165">Save and close the **SimulatedDevice.py** file.</span></span> <span data-ttu-id="f3883-166">Şimdi bu uygulamayı çalıştırmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="f3883-166">You are now ready to run this app.</span></span>

> [!NOTE]
> <span data-ttu-id="f3883-167">Sade ve basit bir anlatım gözetildiği için bu öğretici herhangi bir yeniden deneme ilkesi uygulamaz.</span><span class="sxs-lookup"><span data-stu-id="f3883-167">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="f3883-168">[Geçici Hata İşleme][lnk-transient-faults] adlı MSDN makalesinde önerildiği üzere, üretim kodunda yeniden deneme ilkelerini (üstel geri alma gibi) uygulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3883-168">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="receive-messages-from-your-simulated-device"></a><span data-ttu-id="f3883-169">Sanal cihazınızdan ileti alma</span><span class="sxs-lookup"><span data-stu-id="f3883-169">Receive messages from your simulated device</span></span>
<span data-ttu-id="f3883-170">Cihazınızdan telemetri iletilerini almak için, cihazdan buluta giden iletileri okuyan IoT Hub tarafından ortaya konan [Event Hubs][lnk-event-hubs-overview] ile uyumlu bir uç nokta kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f3883-170">To receive telemetry messages from your device, you need to use an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint exposed by the IoT Hub, which reads the device-to-cloud messages.</span></span> <span data-ttu-id="f3883-171">Event Hubs’tan IoT hub’ınızın Event Hub uyumlu uç noktasına gelen iletilerin nasıl işleneceği hakkında bilgi edinmek için, [Event Hubs ile Çalışmaya Başlama][lnk-eventhubs-tutorial] öğreticisini okuyun.</span><span class="sxs-lookup"><span data-stu-id="f3883-171">Read the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial for information on how to process messages from Event Hubs for your IoT hub's Event Hub-compatible endpoint.</span></span> <span data-ttu-id="f3883-172">Event Hubs henüz Python’da telemetriyi desteklememektedir, dolayısıyla IoT Hub’dan cihazdan buluta gelen iletileri okumak için [Node.js](iot-hub-node-node-getstarted.md#D2C_node) veya [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs tabanlı bir konsol uygulaması oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3883-172">Event Hubs does not support telemetry in Python yet, so you can either create a [Node.js](iot-hub-node-node-getstarted.md#D2C_node) or a [.NET](iot-hub-csharp-csharp-getstarted.md#D2C_csharp) Event Hubs-based console app to read the device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="f3883-173">Bu öğretici, bu cihaz iletilerini okumak için [IoT Hub Gezgini aracını][lnk-iot-hub-explorer] nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="f3883-173">This tutorial shows how you can use the [IoT Hub Explorer tool][lnk-iot-hub-explorer] to read these device messages.</span></span>

1. <span data-ttu-id="f3883-174">Komut istemini açın ve IoT Hub Gezgini’ni yükleyin.</span><span class="sxs-lookup"><span data-stu-id="f3883-174">Open a command prompt and install the IoT Hub Explorer.</span></span> 

    ```
    npm install -g iothub-explorer
    ```

2. <span data-ttu-id="f3883-175">Cihazdan buluta gelen iletileri cihazınızdan izlemeye başlamak için, komut isteminde aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f3883-175">Run the following command on the command prompt, to begin monitoring the device-to-cloud messages from your device.</span></span> <span data-ttu-id="f3883-176">Yer tutucuda `--login` öğesinden sonra IoT hub’ınızın bağlantı dizesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f3883-176">Use your IoT hub's connection string in the placeholder after `--login`.</span></span>

    ```
    iothub-explorer monitor-events MyFirstPythonDevice --login "[IoTHub connection string]"
    ```

3. <span data-ttu-id="f3883-177">Yeni bir komut istemi açın ve **SimulatedDevice.py** dosyasını içeren dizine gidin.</span><span class="sxs-lookup"><span data-stu-id="f3883-177">Open a new command prompt and navigate to the directory containing the **SimulatedDevice.py** file.</span></span>

4. <span data-ttu-id="f3883-178">IoT hub’ınıza düzenli aralıklarla telemetri verileri gönderen **SimulatedDevice.py** dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f3883-178">Run the **SimulatedDevice.py** file, which periodically sends telemetry data to your IoT hub.</span></span> 
   
    ```
    python SimulatedDevice.py
    ```
5. <span data-ttu-id="f3883-179">Önceki bölümde IoT Hub Gezgini’ni çalıştırarak komut isteminde cihaz iletilerini gözlemleyin.</span><span class="sxs-lookup"><span data-stu-id="f3883-179">Observe the device messages on the command prompt running the IoT Hub Explorer from the previous section.</span></span> 

    ![Python cihazdan buluta iletiler][2]

## <a name="next-steps"></a><span data-ttu-id="f3883-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f3883-181">Next steps</span></span>
<span data-ttu-id="f3883-182">Bu öğreticide, Azure portalında yeni bir IoT hub'ı yapılandırdınız ve ardından IoT hub'ının kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="f3883-182">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="f3883-183">Bu cihaz kimliğini, sanal cihaz uygulamasının, IoT hub'ına cihazdan buluta iletileri göndermesini sağlamak için kullandınız.</span><span class="sxs-lookup"><span data-stu-id="f3883-183">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="f3883-184">IoT Hub Gezgini aracının yardımıyla IoT hub’ı tarafından alınan iletileri gözlemlediniz.</span><span class="sxs-lookup"><span data-stu-id="f3883-184">You observed the messages received by the IoT hub with the help of the IoT Hub Explorer tool.</span></span> 

<span data-ttu-id="f3883-185">Azure IoT Hub için Python SDK’sının kullanımını derinlemesine incelemek için [bu Git Hub deposunu][lnk-python-github] ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="f3883-185">To explore the Python SDK for Azure IoT Hub usage in depth, visit [this Git Hub repo][lnk-python-github].</span></span> <span data-ttu-id="f3883-186">Azure IoT Hub Hizmeti SDK’sının ileti özelliklerini gözden geçirmek için, [iothub_messaging_sample.py][lnk-messaging-sample] dosyasını indirebilir ve çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3883-186">To review the messaging capabilities of the Azure IoT Hub Service SDK for Python, you can download and run [iothub_messaging_sample.py][lnk-messaging-sample].</span></span> <span data-ttu-id="f3883-187">Python için Azure IoT Hub Cihazı SDK’sını kullanan cihaz tarafı benzetimi için, [iothub_client_sample.py][lnk-client-sample] dosyasını indirebilir ve çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f3883-187">For device side simulation using the Azure IoT Hub Device SDK for Python, you can download and run the [iothub_client_sample.py][lnk-client-sample].</span></span>

<span data-ttu-id="f3883-188">IoT Hub’ı kullanmaya başlamak ve diğer IoT senaryolarını keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="f3883-188">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="f3883-189">[Cihazınızı bağlama][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="f3883-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="f3883-190">[Cihaz yönetimini kullanmaya başlama][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="f3883-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="f3883-191">[Azure IoT Edge’i kullanmaya başlama][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="f3883-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="f3883-192">IoT çözümünüzün nasıl genişletileceğini ve cihazdan buluta iletilerin doğru ölçekte nasıl işleneceğini öğrenmek için [Cihazdan buluta iletileri işleme][lnk-process-d2c-tutorial] öğreticisine bakın.</span><span class="sxs-lookup"><span data-stu-id="f3883-192">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
