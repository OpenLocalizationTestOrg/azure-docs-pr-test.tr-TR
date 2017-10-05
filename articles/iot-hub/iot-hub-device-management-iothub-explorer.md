---
title: "Iothub explorer ile Azure IOT cihaz Yönetimi | Microsoft Docs"
description: "Iothub explorer CLI aracı doğrudan yöntemleri ve Twin'ın istenen özellikleri yönetim seçenekleri özelliklerine sahip Azure IOT Hub cihaz yönetimi için kullanın."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Azure IOT cihaz yönetimi, azure IOT hub cihaz yönetimi, cihaz yönetim IOT, IOT hub cihaz Yönetimi"
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: 5b7a5057bdfb5920fbb5759bed1f5561cfa1d7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="11fa4-104">Azure IOT Hub cihaz yönetimi için ıothub explorer'ı kullanın</span><span class="sxs-lookup"><span data-stu-id="11fa4-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="11fa4-106">[ıothub explorer](https://github.com/azure/iothub-explorer) bir ana bilgisayarda çalıştırmak bir CLI araçtır, IOT hub defterinde cihaz kimlikleri yönetmek için bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="11fa4-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer to manage device identities in your IoT hub registry.</span></span> <span data-ttu-id="11fa4-107">Çeşitli görevleri gerçekleştirmek için kullanabileceğiniz yönetim seçenekleri ile gelir.</span><span class="sxs-lookup"><span data-stu-id="11fa4-107">It comes with management options that you can use to perform various tasks.</span></span>

| <span data-ttu-id="11fa4-108">Yönetim seçeneği</span><span class="sxs-lookup"><span data-stu-id="11fa4-108">Management option</span></span>          | <span data-ttu-id="11fa4-109">Görev</span><span class="sxs-lookup"><span data-stu-id="11fa4-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="11fa4-110">Doğrudan yöntemler</span><span class="sxs-lookup"><span data-stu-id="11fa4-110">Direct methods</span></span>             | <span data-ttu-id="11fa4-111">Başlatma veya ileti gönderme veya cihaz yeniden başlatıldığı durdurma gibi davranacak bir aygıtı olun.</span><span class="sxs-lookup"><span data-stu-id="11fa4-111">Make a device act such as starting or stopping sending messages or rebooting the device.</span></span>                                        |
| <span data-ttu-id="11fa4-112">İstenen twin özellikleri</span><span class="sxs-lookup"><span data-stu-id="11fa4-112">Twin desired properties</span></span>    | <span data-ttu-id="11fa4-113">Bir aygıt için yeşil bir Işığı ayarlama veya telemetri gönderme aralığı 30 dakika gibi bazı durumların yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="11fa4-113">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span></span>         |
| <span data-ttu-id="11fa4-114">Özellikler Twin bildirdi</span><span class="sxs-lookup"><span data-stu-id="11fa4-114">Twin reported properties</span></span>   | <span data-ttu-id="11fa4-115">Bir aygıt bildirilen durumunu alın.</span><span class="sxs-lookup"><span data-stu-id="11fa4-115">Get the reported state of a device.</span></span> <span data-ttu-id="11fa4-116">Örneğin, aygıt LED şimdi yanıp sönen bildirir.</span><span class="sxs-lookup"><span data-stu-id="11fa4-116">For example, the device reports the LED is blinking now.</span></span>                                    |
| <span data-ttu-id="11fa4-117">Twin etiketleri</span><span class="sxs-lookup"><span data-stu-id="11fa4-117">Twin tags</span></span>                  | <span data-ttu-id="11fa4-118">Aygıta özgü meta verileri bulutta depolayın.</span><span class="sxs-lookup"><span data-stu-id="11fa4-118">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="11fa4-119">Örneğin, bir satış makinenin dağıtım konumu.</span><span class="sxs-lookup"><span data-stu-id="11fa4-119">For example, the deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="11fa4-120">Bulut-cihaz iletilerini</span><span class="sxs-lookup"><span data-stu-id="11fa4-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="11fa4-121">Bir aygıt için bildirimler Gönder.</span><span class="sxs-lookup"><span data-stu-id="11fa4-121">Send notifications to a device.</span></span> <span data-ttu-id="11fa4-122">Örneğin, ", Bugün sizi büyük olasılıktır.</span><span class="sxs-lookup"><span data-stu-id="11fa4-122">For example, "It is very likely to rain today.</span></span> <span data-ttu-id="11fa4-123">Bir şemsiyesi getirmeyi unutmayın."</span><span class="sxs-lookup"><span data-stu-id="11fa4-123">Don't forget to bring an umbrella."</span></span>              |
| <span data-ttu-id="11fa4-124">Cihaz çifti sorguları</span><span class="sxs-lookup"><span data-stu-id="11fa4-124">Device twin queries</span></span>        | <span data-ttu-id="11fa4-125">Kullanılabilir aygıtları tanımlama gibi rasgele koşullarla almak için tüm cihaz çiftlerini sorgulamak.</span><span class="sxs-lookup"><span data-stu-id="11fa4-125">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span></span> |

<span data-ttu-id="11fa4-126">Daha ayrıntılı açıklama farklara ve bu seçenekleri kullanma konusunda yönergeler için bkz: [cihaz bulut iletişimi Kılavuzu](iot-hub-devguide-d2c-guidance.md) ve [bulut-cihaz iletişimi Kılavuzu](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="11fa4-126">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="11fa4-127">Cihaz çiftleri, cihaz durumu bilgilerini (meta veriler, yapılandırmalar ve koşullar) depolayan JSON belgelerdir.</span><span class="sxs-lookup"><span data-stu-id="11fa4-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="11fa4-128">IOT Hub cihaz çifti ona bağlanan her aygıt için devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="11fa4-128">IoT Hub persists a device twin for each device that connects to it.</span></span> <span data-ttu-id="11fa4-129">Cihaz çiftlerini hakkında daha fazla bilgi için bkz: [cihaz çiftlerini ile çalışmaya başlama](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="11fa4-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="11fa4-130">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="11fa4-130">What you learn</span></span>

<span data-ttu-id="11fa4-131">Geliştirme makinenizde çeşitli yönetim seçenekleri ile ıothub explorer'ı kullanarak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="11fa4-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="11fa4-132">Neler</span><span class="sxs-lookup"><span data-stu-id="11fa4-132">What you do</span></span>

<span data-ttu-id="11fa4-133">Iothub explorer çeşitli yönetim seçenekleri ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="11fa4-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="11fa4-134">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="11fa4-134">What you need</span></span>

- <span data-ttu-id="11fa4-135">Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) , aşağıdaki gereksinimleri ele alınmaktadır tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="11fa4-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="11fa4-136">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="11fa4-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="11fa4-137">Azure IOT hub'ı aboneliğinizdeki.</span><span class="sxs-lookup"><span data-stu-id="11fa4-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="11fa4-138">Azure IOT hub'ına iletileri gönderen bir istemci uygulaması.</span><span class="sxs-lookup"><span data-stu-id="11fa4-138">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="11fa4-139">Cihazınız Bu öğretici sırasında istemci uygulaması ile çalıştığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="11fa4-139">Make sure your device is running with the client application during this tutorial.</span></span>
- <span data-ttu-id="11fa4-140">iothub-explorer [yükleme ıothub explorer](https://github.com/azure/iothub-explorer) geliştirme makinenizde.</span><span class="sxs-lookup"><span data-stu-id="11fa4-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-to-your-iot-hub"></a><span data-ttu-id="11fa4-141">IOT hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="11fa4-141">Connect to your IoT hub</span></span>

<span data-ttu-id="11fa4-142">Aşağıdaki komutu çalıştırarak IOT hub'ınıza bağlanın:</span><span class="sxs-lookup"><span data-stu-id="11fa4-142">Connect to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="11fa4-143">Doğrudan yöntemleriyle ıothub Gezgini'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="11fa4-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="11fa4-144">Çağırma `start` yöntemi aşağıdaki komutu çalıştırarak IOT hub'ınıza ileti göndermek için aygıt uygulamasında:</span><span class="sxs-lookup"><span data-stu-id="11fa4-144">Invoke the `start` method in the device app to send messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="11fa4-145">Çağırma `stop` gönderilmesini durdurmak için cihaz uygulaması yönteminde aşağıdaki komutu çalıştırarak IOT hub'ına iletileri:</span><span class="sxs-lookup"><span data-stu-id="11fa4-145">Invoke the `stop` method in the device app to stop sending messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="11fa4-146">Twin'ın istenen özelliklere sahip ıothub Gezgini'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="11fa4-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="11fa4-147">İstenen özellik aralığını ayarlayın aşağıdaki komutu çalıştırarak 3000 =:</span><span class="sxs-lookup"><span data-stu-id="11fa4-147">Set a desired property interval = 3000 by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="11fa4-148">Bu özellik, cihazınız tarafından okunabilir.</span><span class="sxs-lookup"><span data-stu-id="11fa4-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="11fa4-149">Twin'ın bildirilen özelliklerle ıothub Gezgini'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="11fa4-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="11fa4-150">Aşağıdaki komutu çalıştırarak bildirilen cihaz özelliklerini alın:</span><span class="sxs-lookup"><span data-stu-id="11fa4-150">Get the reported properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="11fa4-151">$Metadata özellikleri biridir. Bu aygıtın son zamanı gösteren $lastUpdated gönderir veya bir ileti alır.</span><span class="sxs-lookup"><span data-stu-id="11fa4-151">One of the properties is $metadata.$lastUpdated which shows the last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="11fa4-152">Twin'ın etiketleriyle ıothub Gezgini'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="11fa4-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="11fa4-153">Aşağıdaki komutu çalıştırarak etiketleri ve cihaz özelliklerini görüntüle:</span><span class="sxs-lookup"><span data-stu-id="11fa4-153">Display the tags and properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="11fa4-154">Bir alan rolünü ekleyin aşağıdaki komutu çalıştırarak sıcaklık ve nem aygıta =:</span><span class="sxs-lookup"><span data-stu-id="11fa4-154">Add a field role = temperature&humidity to the device by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="11fa4-155">Bulut cihaza iletileriyle ıothub Gezgini'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="11fa4-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="11fa4-156">"Hello World" iletisini, aşağıdaki komutu çalıştırarak cihaza gönder:</span><span class="sxs-lookup"><span data-stu-id="11fa4-156">Send a "Hello World" message to the device by running the following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="11fa4-157">Bkz: [cihaz ve IOT hub'ı arasında ileti gönderme ve alma için iothub-Gezgini'ni kullanma](iot-hub-explorer-cloud-device-messaging.md) bu komutu kullanarak, gerçek bir senaryo için.</span><span class="sxs-lookup"><span data-stu-id="11fa4-157">See [Use iothub-explorer to send and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="11fa4-158">Cihaz çiftlerini sorgularıyla ıothub Gezgini'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="11fa4-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="11fa4-159">Sorgu bir etiket rolünün aygıtlarla 'sıcaklık ve nem' aşağıdaki komutu çalıştırarak =:</span><span class="sxs-lookup"><span data-stu-id="11fa4-159">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="11fa4-160">Bir etiketi rolünün olanlar dışında tüm cihazlar sorgu aşağıdaki komutu çalıştırarak 'sıcaklık ve nem' =:</span><span class="sxs-lookup"><span data-stu-id="11fa4-160">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="11fa4-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="11fa4-161">Next steps</span></span>

<span data-ttu-id="11fa4-162">Çeşitli yönetim seçenekleri ile ıothub Gezgini'ni kullanma öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="11fa4-162">You've learned how to use iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
