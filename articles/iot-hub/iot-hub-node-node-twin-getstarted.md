---
title: "Azure IOT Hub cihaz çiftlerini (düğüm) ile çalışmaya başlama | Microsoft Docs"
description: "Azure IOT Hub cihaz çiftlerini etiket ekleyebilir ve IOT Hub sorgusuyla kullanmak için nasıl kullanılacağını. Sanal cihaz uygulamasının ve etiketleri ekler ve IOT hub'ı sorgu çalışan bir hizmet uygulaması uygulamak için Node.js için Azure IOT SDK'ları kullanın."
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: 633c9fd4f8a1d017d93148f8c2e860ccba14238c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="97b63-104">Cihaz çiftlerini (düğüm) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="97b63-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="97b63-105">Bu öğreticinin sonunda iki Node.js konsol uygulamaları olacaktır:</span><span class="sxs-lookup"><span data-stu-id="97b63-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="97b63-106">**AddTagsAndQuery.js**, etiketleri ekler ve cihaz çiftlerini sorgular bir Node.js arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="97b63-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="97b63-107">**TwinSimulatedDevice.js**, bir cihaza benzetim yapan daha önce oluşturulan cihaz kimliğiyle IOT hub'ınıza bağlanır ve kendi bağlantı koşulu raporları bir Node.js uygulaması.</span><span class="sxs-lookup"><span data-stu-id="97b63-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="97b63-108">Makaleyi [Azure IOT SDK'ları] [ lnk-hub-sdks] hem cihaz hem de arka uç uygulamalar oluşturmak için kullanabileceğiniz Azure IOT SDK'ları hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="97b63-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="97b63-109">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="97b63-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="97b63-110">Node.js 0.10.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="97b63-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="97b63-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="97b63-111">An active Azure account.</span></span> <span data-ttu-id="97b63-112">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="97b63-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="97b63-113">Hizmet Uygulaması Oluştur</span><span class="sxs-lookup"><span data-stu-id="97b63-113">Create the service app</span></span>
<span data-ttu-id="97b63-114">Bu bölümde, ilişkili cihaz çifti konumu meta veri ekleyen bir Node.js konsol uygulaması oluşturma **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="97b63-114">In this section, you create a Node.js console app that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="97b63-115">Ardından, IOT hub'ı ABD, ardından bir cep telefonu bağlantı raporlama olanları içinde bulunan aygıtları seçerek depolanan cihaz çiftlerini sorgular.</span><span class="sxs-lookup"><span data-stu-id="97b63-115">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="97b63-116">Adlı yeni bir boş klasör oluşturun **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="97b63-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="97b63-117">İçinde **addtagsandqueryapp** klasörü, komut isteminde aşağıdaki komutu kullanarak yeni bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="97b63-117">In the **addtagsandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="97b63-118">Tüm varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="97b63-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="97b63-119">Komut isteminizde **addtagsandqueryapp** klasörü yüklemek için aşağıdaki komutu çalıştırın, **azure-iothub** paketi:</span><span class="sxs-lookup"><span data-stu-id="97b63-119">At your command prompt in the **addtagsandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="97b63-120">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **AddTagsAndQuery.js** dosyasını **addtagsandqueryapp** klasör.</span><span class="sxs-lookup"><span data-stu-id="97b63-120">Using a text editor, create a new **AddTagsAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="97b63-121">Aşağıdaki kodu ekleyin **AddTagsAndQuery.js** dosya ve yerine **{IOT hub bağlantı dizesine}** yer tutucu hub'ınızı oluşturduğunuzda kopyaladığınız IOT Hub bağlantı dizesine sahip:</span><span class="sxs-lookup"><span data-stu-id="97b63-121">Add the following code to the **AddTagsAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    <span data-ttu-id="97b63-122">**Kayıt defteri** nesne cihaz çiftlerini hizmet ile etkileşim kurmak için gereken tüm yöntemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="97b63-122">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="97b63-123">Önceki kod ilk başlatır **kayıt defteri** nesnesi, ardından cihaz çiftinin alır **myDeviceId**ve son olarak, etiketleri istenen konumu bilgilerle güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="97b63-123">The previous code first initializes the **Registry** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="97b63-124">Etiketler güncelleştirdikten sonra çağırır **queryTwins** işlevi.</span><span class="sxs-lookup"><span data-stu-id="97b63-124">After the updating the tags it calls the **queryTwins** function.</span></span>
5. <span data-ttu-id="97b63-125">Sonuna aşağıdaki kodu ekleyin **AddTagsAndQuery.js** uygulamak için **queryTwins** işlevi:</span><span class="sxs-lookup"><span data-stu-id="97b63-125">Add the following code at the end of  **AddTagsAndQuery.js** to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="97b63-126">Önceki kod iki sorguları yürüten: yalnızca cihaz çiftlerini bulunan aygıtların ilk seçer **Redmond43** tesis ve ikinci da cep telefonu şebekesi bağlı aygıtlar seçmek için sorgu iyileştirir.</span><span class="sxs-lookup"><span data-stu-id="97b63-126">The previous code executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="97b63-127">Unutmayın, oluşturduğunda, önceki kod **sorgu** nesne, döndürülen belgelerin en fazla sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="97b63-127">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="97b63-128">**Sorgu** nesnesini içeren bir **hasMoreResults** çağırmak için kullanabileceğiniz boolean özelliği **nextAsTwin** birden çok kez tüm sonuçları almak için yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="97b63-128">The **query** object contains a **hasMoreResults** boolean property that you can use to invoke the **nextAsTwin** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="97b63-129">Bir yöntem olarak adlandırılan **sonraki** Örneğin, cihaz çiftlerini toplama sorguların sonuçlarını olmayan sonuçlar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="97b63-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="97b63-130">Uygulama ile çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="97b63-130">Run the application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="97b63-131">Bulunan tüm cihazlar için sorgu soran bir cihazda sonuçlarında görmelisiniz **Redmond43** ve sonuçları bir cep telefonu şebekesi kullanan cihazlar için sınırlar sorgu için yok.</span><span class="sxs-lookup"><span data-stu-id="97b63-131">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="97b63-132">Sonraki bölümde, önceki bölümde sorgusunun sonucu değiştirir ve bağlantı bilgilerini raporlar bir cihaz uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="97b63-132">In the next section you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="97b63-133">Cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="97b63-133">Create the device app</span></span>
<span data-ttu-id="97b63-134">Bu bölümde, hub'ınıza bağlanan bir Node.js konsol uygulaması oluşturma **myDeviceId**ve ardından, cihaz çifti bir cep telefonu şebekesi kullanarak bağlı bilgileri içerecek şekilde özellikleri bildirilen güncelleştirmeler.</span><span class="sxs-lookup"><span data-stu-id="97b63-134">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its device twin's reported properties to contain the information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="97b63-135">Şu anda cihaz çiftlerini MQTT protokolünü kullanarak IOT hub'a bağlanan cihazlar üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="97b63-135">At this time, device twins are accessible only from devices that connect to IoT Hub using the MQTT protocol.</span></span> <span data-ttu-id="97b63-136">Lütfen [MQTT Destek] [ lnk-devguide-mqtt] MQTT kullanmak mevcut cihaz uygulaması dönüştürme hakkında yönergeler için makalenin.</span><span class="sxs-lookup"><span data-stu-id="97b63-136">Please refer to the [MQTT support][lnk-devguide-mqtt] article for instructions on how to convert existing device app to use MQTT.</span></span>
> 
> 

1. <span data-ttu-id="97b63-137">Adlı yeni bir boş klasör oluşturun **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="97b63-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="97b63-138">İçinde **reportconnectivity** klasörü, komut isteminde aşağıdaki komutu kullanarak yeni bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="97b63-138">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="97b63-139">Tüm varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="97b63-139">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="97b63-140">Komut isteminizde **reportconnectivity** klasörü yüklemek için aşağıdaki komutu çalıştırın, **azure IOT cihaz**, ve **azure-IOT-cihaz-mqtt** paketi:</span><span class="sxs-lookup"><span data-stu-id="97b63-140">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="97b63-141">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **ReportConnectivity.js** dosyasını **reportconnectivity** klasör.</span><span class="sxs-lookup"><span data-stu-id="97b63-141">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="97b63-142">Aşağıdaki kodu ekleyin **ReportConnectivity.js** dosya ve yerine **{cihaz bağlantı dizesi}** yer tutucu oluşturduğunuzdakopyaladığınızcihazbağlantıdizesiyle**myDeviceId** cihaz kimliği:</span><span class="sxs-lookup"><span data-stu-id="97b63-142">Add the following code to the **ReportConnectivity.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="97b63-143">**İstemci** nesne ihtiyaç duyduğunuz etkileşim kurmak için cihaz çiftlerini aygıttan ile tüm yöntemleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="97b63-143">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="97b63-144">Bunu başlatır sonra önceki kod **istemci** nesnesi, cihaz çiftinin alır **myDeviceId** ve kendi bildirilen özelliği ile bağlantı bilgilerini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="97b63-144">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
5. <span data-ttu-id="97b63-145">Cihaz uygulama çalıştırma</span><span class="sxs-lookup"><span data-stu-id="97b63-145">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="97b63-146">Şu iletiyi görürsünüz `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="97b63-146">You should see the message `twin state reported`.</span></span>
6. <span data-ttu-id="97b63-147">Aygıt bağlantısı bilgilerini bildirdi, her iki sorgularda görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="97b63-147">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="97b63-148">Geri gidin **addtagsandqueryapp** klasörü ve sorguları yeniden çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="97b63-148">Go back in the **addtagsandqueryapp** folder and run the queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="97b63-149">Bu süre **myDeviceId** hem sorgu sonuçlarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="97b63-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="97b63-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="97b63-150">Next steps</span></span>
<span data-ttu-id="97b63-151">Bu öğreticide, Azure portalında yeni bir IoT hub'ı yapılandırdınız ve ardından IoT hub'ının kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="97b63-151">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="97b63-152">Cihaz meta verilerini bir arka uç uygulamadan etiketler eklendi ve sanal cihaz uygulaması rapor cihaz bağlantı bilgilerini cihaz çiftine yazıldı.</span><span class="sxs-lookup"><span data-stu-id="97b63-152">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="97b63-153">Ayrıca SQL benzeri IOT hub'ı sorgu dili kullanarak bu bilgileri sorgulamak öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="97b63-153">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="97b63-154">Bilgi edinmek için aşağıdaki kaynakları kullanın nasıl yapılır:</span><span class="sxs-lookup"><span data-stu-id="97b63-154">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="97b63-155">aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici</span><span class="sxs-lookup"><span data-stu-id="97b63-155">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="97b63-156">cihaz çifti'nın istenen özelliklere sahip kullanarak cihazları yapılandırma [kullanmak istediğiniz cihazları yapılandırmak için Özellikler] [ lnk-twin-how-to-configure] öğretici</span><span class="sxs-lookup"><span data-stu-id="97b63-156">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="97b63-157">ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten), cihazları denetleme [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="97b63-157">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
