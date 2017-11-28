---
title: "aaaGet başlatılan Azure IOT Hub cihaz çiftlerini (düğüm) | Microsoft Docs"
description: "Nasıl toouse Azure IOT Hub cihaz çiftlerini tooadd etiketleri ve IOT Hub sorgusuyla kullanın. Node.js tooimplement hello sanal cihaz uygulaması için Azure IOT SDK'ları hello ve hello etiketleri ekler ve hello IOT hub'ı sorgu çalışan bir hizmet uygulaması kullanın."
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
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="84678-104">Cihaz çiftlerini (düğüm) ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="84678-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="84678-105">Bu öğreticinin Hello sonunda, iki Node.js konsol uygulamaları olacaktır:</span><span class="sxs-lookup"><span data-stu-id="84678-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="84678-106">**AddTagsAndQuery.js**, etiketleri ekler ve cihaz çiftlerini sorgular bir Node.js arka uç uygulaması.</span><span class="sxs-lookup"><span data-stu-id="84678-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="84678-107">**TwinSimulatedDevice.js**, bir cihaza benzetim yapan tooyour IOT hub'ı daha önce oluşturduğunuz hello cihaz kimliği bağlanır ve kendi bağlantı koşulu raporları bir Node.js uygulaması.</span><span class="sxs-lookup"><span data-stu-id="84678-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="84678-108">Merhaba makale [Azure IOT SDK'ları] [ lnk-hub-sdks] toobuild kullanabileceğiniz hello Azure IOT SDK'ları hakkında bilgi sağlayan cihaz ve arka uç uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="84678-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="84678-109">toocomplete hello aşağıdaki gereksinim Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="84678-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="84678-110">Node.js 0.10.x sürümü veya sonraki bir sürüm.</span><span class="sxs-lookup"><span data-stu-id="84678-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="84678-111">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="84678-111">An active Azure account.</span></span> <span data-ttu-id="84678-112">(Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="84678-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="84678-113">Merhaba service uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="84678-113">Create hello service app</span></span>
<span data-ttu-id="84678-114">Bu bölümde, konum meta veri toohello cihaz çifti ile ilişkili ekler bir Node.js konsol uygulaması oluşturma **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="84678-114">In this section, you create a Node.js console app that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="84678-115">Ardından hello cihaz çiftlerini hello IOT hub'ı hello bulunan hello aygıtları seçerek BİZE depolanır ve bir cep telefonu bağlantı raporlama olanları hello sorgular.</span><span class="sxs-lookup"><span data-stu-id="84678-115">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="84678-116">Adlı yeni bir boş klasör oluşturun **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="84678-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="84678-117">Merhaba, **addtagsandqueryapp** klasörü, komut, komut isteminde aşağıdaki hello kullanarak yeni bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84678-117">In hello **addtagsandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="84678-118">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="84678-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="84678-119">Merhaba, komut isteminde **addtagsandqueryapp** klasörüne, komut tooinstall hello aşağıdaki hello **azure-iothub** paketi:</span><span class="sxs-lookup"><span data-stu-id="84678-119">At your command prompt in hello **addtagsandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="84678-120">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **AddTagsAndQuery.js** hello dosyasında **addtagsandqueryapp** klasör.</span><span class="sxs-lookup"><span data-stu-id="84678-120">Using a text editor, create a new **AddTagsAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="84678-121">Aşağıdaki kodu toohello hello eklemek **AddTagsAndQuery.js** dosya ve hello yerine **{IOT hub bağlantı dizesine}** yer tutucu hello hub'ınızı oluşturduğunuzda kopyaladığınız IOT Hub bağlantı dizesine sahip:</span><span class="sxs-lookup"><span data-stu-id="84678-121">Add hello following code toohello **AddTagsAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
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
   
    <span data-ttu-id="84678-122">Merhaba **kayıt defteri** nesne cihaz çiftlerini hello hizmetinden ile tüm hello yöntemleri gerekli toointeract kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="84678-122">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="84678-123">Merhaba önceki kod ilk hello başlatır **kayıt defteri** nesnesi alır cihaz çiftinin hello sonra **myDeviceId**ve son olarak, etiketleri istenen hello konumu bilgilerle güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="84678-123">hello previous code first initializes hello **Registry** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="84678-124">Merhaba sonra hello güncelleştirme onu çağrıları hello etiketler **queryTwins** işlevi.</span><span class="sxs-lookup"><span data-stu-id="84678-124">After hello updating hello tags it calls hello **queryTwins** function.</span></span>
5. <span data-ttu-id="84678-125">Merhaba ucunda koddan hello eklemek **AddTagsAndQuery.js** tooimplement hello **queryTwins** işlevi:</span><span class="sxs-lookup"><span data-stu-id="84678-125">Add hello following code at hello end of  **AddTagsAndQuery.js** tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="84678-126">Merhaba önceki kod iki sorguları çalıştırır: hello ilk yalnızca hello cihaz çiftlerini hello bulunan aygıtların seçer **Redmond43** tesis ve ayrıca üzerinden bağlanan hello ikinci iyileştirir hello sorgu tooselect yalnızca hello cihazları cep telefonu şebekesi.</span><span class="sxs-lookup"><span data-stu-id="84678-126">hello previous code executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="84678-127">Merhaba oluşturduğunda bu hello önceki kod Not **sorgu** nesne, döndürülen belgelerin en fazla sayısını belirtir.</span><span class="sxs-lookup"><span data-stu-id="84678-127">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="84678-128">Merhaba **sorgu** nesnesini içeren bir **hasMoreResults** tooinvoke hello kullanabileceğiniz boolean özelliği **nextAsTwin** yöntemleri tooretrieve tüm sonuçları birden çok kez.</span><span class="sxs-lookup"><span data-stu-id="84678-128">hello **query** object contains a **hasMoreResults** boolean property that you can use tooinvoke hello **nextAsTwin** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="84678-129">Bir yöntem olarak adlandırılan **sonraki** Örneğin, cihaz çiftlerini toplama sorguların sonuçlarını olmayan sonuçlar için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="84678-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="84678-130">Merhaba uygulaması ile çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="84678-130">Run hello application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="84678-131">Bulunan tüm cihazlar için sorgu hello soran bir cihazda hello sonuçlarında görmelisiniz **Redmond43** ve hiçbiri hello kısıtlayan hello sorgu için bir cep telefonu şebekesi kullanmak toodevices sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="84678-131">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="84678-132">Merhaba sonraki bölümde hello bağlantı bilgilerini raporları bir cihaz uygulaması oluşturma ve değişiklikleri hello önceki bölümdeki hello sorgusunun sonucu hello.</span><span class="sxs-lookup"><span data-stu-id="84678-132">In hello next section you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="84678-133">Merhaba cihaz uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="84678-133">Create hello device app</span></span>
<span data-ttu-id="84678-134">Bu bölümde, tooyour hub olarak bağlanan bir Node.js konsol uygulaması oluşturma **myDeviceId**ve ardından, cihaz çifti bir cep telefonu şebekesi kullanarak bağlı özellikler toocontain hello bilgilerini bildirilen güncelleştirmeler.</span><span class="sxs-lookup"><span data-stu-id="84678-134">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its device twin's reported properties toocontain hello information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="84678-135">Şu anda cihaz çiftlerini tooIoT hub'a bağlanan aygıtlardan erişilebilir hello MQTT protokolünü kullanarak.</span><span class="sxs-lookup"><span data-stu-id="84678-135">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="84678-136">Lütfen toohello bakın [MQTT Destek] [ lnk-devguide-mqtt] hakkında yönergeler için makalenin tooconvert mevcut aygıt uygulama toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="84678-136">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

1. <span data-ttu-id="84678-137">Adlı yeni bir boş klasör oluşturun **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="84678-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="84678-138">Merhaba, **reportconnectivity** klasörü, komut, komut isteminde aşağıdaki hello kullanarak yeni bir package.json dosyası oluşturun.</span><span class="sxs-lookup"><span data-stu-id="84678-138">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="84678-139">Tüm hello Varsayılanları kabul edin:</span><span class="sxs-lookup"><span data-stu-id="84678-139">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="84678-140">Merhaba, komut isteminde **reportconnectivity** klasörüne, komut tooinstall hello aşağıdaki hello **azure IOT cihaz**, ve **azure-IOT-cihaz-mqtt** paketi :</span><span class="sxs-lookup"><span data-stu-id="84678-140">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="84678-141">Bir metin düzenleyicisi kullanarak yeni bir oluşturma **ReportConnectivity.js** hello dosyasında **reportconnectivity** klasör.</span><span class="sxs-lookup"><span data-stu-id="84678-141">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="84678-142">Kod toohello aşağıdaki hello eklemek **ReportConnectivity.js** dosya ve hello yerine **{cihaz bağlantı dizesi}** hello oluşturduğunuzda kopyaladığınız hello cihaz bağlantı dizesiyle yer tutucusu **myDeviceId** cihaz kimliği:</span><span class="sxs-lookup"><span data-stu-id="84678-142">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="84678-143">Merhaba **istemci** nesne cihaz çiftlerini hello aygıttan ile toointeract duyduğunuz tüm hello yöntemler sunar.</span><span class="sxs-lookup"><span data-stu-id="84678-143">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="84678-144">Merhaba başlatır sonra önceki kod Hello **istemci** nesnesi alır, cihaz çiftinin hello **myDeviceId** ve kendi bildirilen özelliği hello bağlantı bilgileriyle güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="84678-144">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
5. <span data-ttu-id="84678-145">Merhaba cihaz uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="84678-145">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="84678-146">Merhaba iletiyi görmeniz gerekir `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="84678-146">You should see hello message `twin state reported`.</span></span>
6. <span data-ttu-id="84678-147">Merhaba aygıt bildirilen bağlantı bilgilerini, her iki sorgularda görüntülenmelidir.</span><span class="sxs-lookup"><span data-stu-id="84678-147">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="84678-148">Merhaba edilene gidin **addtagsandqueryapp** klasörü ve Çalıştır hello sorgular yeniden:</span><span class="sxs-lookup"><span data-stu-id="84678-148">Go back in hello **addtagsandqueryapp** folder and run hello queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="84678-149">Bu süre **myDeviceId** hem sorgu sonuçlarında görüntülenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="84678-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="84678-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="84678-150">Next steps</span></span>
<span data-ttu-id="84678-151">Bu öğreticide hello Azure portalında yeni bir IOT hub yapılandırılmış ve ardından hello IOT hub'ın kimlik kayıt defterinde bir cihaz kimliği oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="84678-151">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="84678-152">Cihaz meta verilerini bir arka uç uygulamadan etiketler eklendi ve bir sanal cihaz uygulaması tooreport aygıt bağlantı bilgilerini hello cihaz çiftine yazıldı.</span><span class="sxs-lookup"><span data-stu-id="84678-152">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="84678-153">Ayrıca nasıl öğrenilen tooquery hello SQL benzeri IOT hub'ı sorgu dili kullanarak bu bilgileri.</span><span class="sxs-lookup"><span data-stu-id="84678-153">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="84678-154">Kaynakları toolearn nasıl aşağıdaki kullanım hello için:</span><span class="sxs-lookup"><span data-stu-id="84678-154">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="84678-155">Merhaba aygıtlarla telemetri gönderen [IOT Hub ile çalışmaya başlama] [ lnk-iothub-getstarted] öğretici</span><span class="sxs-lookup"><span data-stu-id="84678-155">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="84678-156">cihaz çifti'nın istenen özellikleri ile hello kullanarak cihazları yapılandırma [kullanım istenen özellikleri tooconfigure aygıtları] [ lnk-twin-how-to-configure] öğretici,</span><span class="sxs-lookup"><span data-stu-id="84678-156">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="84678-157">Merhaba ile etkileşimli olarak (örneğin, kullanıcı tarafından denetlenen bir uygulamadan fan etkinleştirdikten), cihazları denetleme [doğrudan yöntemleri kullanın] [ lnk-methods-tutorial] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="84678-157">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
