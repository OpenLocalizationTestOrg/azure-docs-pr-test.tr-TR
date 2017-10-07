---
title: "aaaAzure iothub-explorer ile IOT cihaz Yönetimi | Microsoft Docs"
description: "Merhaba ıothub explorer CLI aracı hello doğrudan yöntemleri ve hello Twin'ın istenen özellikleri yönetim seçenekleri özelliklerine sahip Azure IOT Hub cihaz yönetimi için kullanın."
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
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="25377-104">Azure IOT Hub cihaz yönetimi için ıothub explorer'ı kullanın</span><span class="sxs-lookup"><span data-stu-id="25377-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![Uçtan uca diyagramı](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="25377-106">[ıothub explorer](https://github.com/azure/iothub-explorer) IOT hub kayıt defterinizde bir ana bilgisayar toomanage cihaz kimliklerini çalıştırdığınız bir CLI aracıdır.</span><span class="sxs-lookup"><span data-stu-id="25377-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer toomanage device identities in your IoT hub registry.</span></span> <span data-ttu-id="25377-107">Çeşitli görevleri tooperform kullanabileceğiniz yönetim seçenekleri ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="25377-107">It comes with management options that you can use tooperform various tasks.</span></span>

| <span data-ttu-id="25377-108">Yönetim seçeneği</span><span class="sxs-lookup"><span data-stu-id="25377-108">Management option</span></span>          | <span data-ttu-id="25377-109">Görev</span><span class="sxs-lookup"><span data-stu-id="25377-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="25377-110">Doğrudan yöntemler</span><span class="sxs-lookup"><span data-stu-id="25377-110">Direct methods</span></span>             | <span data-ttu-id="25377-111">Başlatma veya ileti gönderme veya hello cihaz yeniden başlatıldığı durdurma gibi davranacak bir aygıtı olun.</span><span class="sxs-lookup"><span data-stu-id="25377-111">Make a device act such as starting or stopping sending messages or rebooting hello device.</span></span>                                        |
| <span data-ttu-id="25377-112">İstenen twin özellikleri</span><span class="sxs-lookup"><span data-stu-id="25377-112">Twin desired properties</span></span>    | <span data-ttu-id="25377-113">Bir aygıt LED toogreen ayarlama gibi bazı durumların yerleştirin veya hello telemetri ayarı aralığı too30 dakika gönderin.</span><span class="sxs-lookup"><span data-stu-id="25377-113">Put a device into certain states, such as setting an LED toogreen or setting hello telemetry send interval too30 minutes.</span></span>         |
| <span data-ttu-id="25377-114">Özellikler Twin bildirdi</span><span class="sxs-lookup"><span data-stu-id="25377-114">Twin reported properties</span></span>   | <span data-ttu-id="25377-115">Alma hello aygıtın durumunu bildirdi.</span><span class="sxs-lookup"><span data-stu-id="25377-115">Get hello reported state of a device.</span></span> <span data-ttu-id="25377-116">Örneğin, hello aygıt LED şimdi yanıp sönen hello bildirir.</span><span class="sxs-lookup"><span data-stu-id="25377-116">For example, hello device reports hello LED is blinking now.</span></span>                                    |
| <span data-ttu-id="25377-117">Twin etiketleri</span><span class="sxs-lookup"><span data-stu-id="25377-117">Twin tags</span></span>                  | <span data-ttu-id="25377-118">Aygıta özgü meta veriler hello bulutta depolayın.</span><span class="sxs-lookup"><span data-stu-id="25377-118">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="25377-119">Örneğin, bir satış makinenin dağıtım konumu hello.</span><span class="sxs-lookup"><span data-stu-id="25377-119">For example, hello deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="25377-120">Bulut-cihaz iletilerini</span><span class="sxs-lookup"><span data-stu-id="25377-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="25377-121">Bildirimleri tooa aygıt gönderin.</span><span class="sxs-lookup"><span data-stu-id="25377-121">Send notifications tooa device.</span></span> <span data-ttu-id="25377-122">Örneğin, "Bu büyük olasılıkla toorain bugün olur.</span><span class="sxs-lookup"><span data-stu-id="25377-122">For example, "It is very likely toorain today.</span></span> <span data-ttu-id="25377-123">Toobring bir şemsiyesi unutmayın."</span><span class="sxs-lookup"><span data-stu-id="25377-123">Don't forget toobring an umbrella."</span></span>              |
| <span data-ttu-id="25377-124">Cihaz çifti sorguları</span><span class="sxs-lookup"><span data-stu-id="25377-124">Device twin queries</span></span>        | <span data-ttu-id="25377-125">Tüm cihaz çiftlerini tooretrieve olanlar gibi kullanılabilir hello aygıtlarını tanımlayan rasgele koşullarla sorgu.</span><span class="sxs-lookup"><span data-stu-id="25377-125">Query all device twins tooretrieve those with arbitrary conditions, such as identifying hello devices that are available for use.</span></span> |

<span data-ttu-id="25377-126">Daha ayrıntılı açıklama hello farklar hakkında ve bu seçenekleri kullanma konusunda yönergeler için bkz: [cihaz bulut iletişimi Kılavuzu](iot-hub-devguide-d2c-guidance.md) ve [bulut-cihaz iletişimi Kılavuzu](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="25377-126">For more detailed explanation on hello differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="25377-127">Cihaz çiftleri, cihaz durumu bilgilerini (meta veriler, yapılandırmalar ve koşullar) depolayan JSON belgelerdir.</span><span class="sxs-lookup"><span data-stu-id="25377-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="25377-128">IOT Hub cihaz çifti tooit bağlanan her aygıt için devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="25377-128">IoT Hub persists a device twin for each device that connects tooit.</span></span> <span data-ttu-id="25377-129">Cihaz çiftlerini hakkında daha fazla bilgi için bkz: [cihaz çiftlerini ile çalışmaya başlama](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="25377-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="25377-130">Öğrenecekleriniz</span><span class="sxs-lookup"><span data-stu-id="25377-130">What you learn</span></span>

<span data-ttu-id="25377-131">Geliştirme makinenizde çeşitli yönetim seçenekleri ile ıothub explorer'ı kullanarak öğrenin.</span><span class="sxs-lookup"><span data-stu-id="25377-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="25377-132">Neler</span><span class="sxs-lookup"><span data-stu-id="25377-132">What you do</span></span>

<span data-ttu-id="25377-133">Iothub explorer çeşitli yönetim seçenekleri ile çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="25377-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="25377-134">Ne gerekiyor</span><span class="sxs-lookup"><span data-stu-id="25377-134">What you need</span></span>

- <span data-ttu-id="25377-135">Öğretici [Cihazınızı](iot-hub-raspberry-pi-kit-node-get-started.md) hangi hello gereksinimleri aşağıdaki kapsayan tamamlandı:</span><span class="sxs-lookup"><span data-stu-id="25377-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="25377-136">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="25377-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="25377-137">Azure IOT hub'ı aboneliğinizdeki.</span><span class="sxs-lookup"><span data-stu-id="25377-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="25377-138">Tooyour Azure IOT hub'ı iletileri gönderir bir istemci uygulaması.</span><span class="sxs-lookup"><span data-stu-id="25377-138">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="25377-139">Cihazınızı Merhaba istemci uygulaması Bu öğretici sırasında çalıştırdığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="25377-139">Make sure your device is running with hello client application during this tutorial.</span></span>
- <span data-ttu-id="25377-140">iothub-explorer [yükleme ıothub explorer](https://github.com/azure/iothub-explorer) geliştirme makinenizde.</span><span class="sxs-lookup"><span data-stu-id="25377-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-tooyour-iot-hub"></a><span data-ttu-id="25377-141">Tooyour IOT hub'ı Bağlan</span><span class="sxs-lookup"><span data-stu-id="25377-141">Connect tooyour IoT hub</span></span>

<span data-ttu-id="25377-142">Tooyour IOT hub'ı hello aşağıdaki komutu çalıştırarak Bağlan:</span><span class="sxs-lookup"><span data-stu-id="25377-142">Connect tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="25377-143">Doğrudan yöntemleriyle ıothub Gezgini'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="25377-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="25377-144">Merhaba çağırma `start` hello aşağıdaki komutu çalıştırarak hello cihaz uygulama toosend iletileri tooyour IOT hub yöntemi:</span><span class="sxs-lookup"><span data-stu-id="25377-144">Invoke hello `start` method in hello device app toosend messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="25377-145">Merhaba çağırma `stop` hello cihaz uygulama toostop gönderme yöntemi hello aşağıdaki komutu çalıştırarak tooyour IOT hub'ı iletileri:</span><span class="sxs-lookup"><span data-stu-id="25377-145">Invoke hello `stop` method in hello device app toostop sending messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="25377-146">Twin'ın istenen özelliklere sahip ıothub Gezgini'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="25377-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="25377-147">İstenen özellik aralığı ayarlamak hello aşağıdaki komutu çalıştırarak 3000 =:</span><span class="sxs-lookup"><span data-stu-id="25377-147">Set a desired property interval = 3000 by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="25377-148">Bu özellik, cihazınız tarafından okunabilir.</span><span class="sxs-lookup"><span data-stu-id="25377-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="25377-149">Twin'ın bildirilen özelliklerle ıothub Gezgini'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="25377-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="25377-150">Merhaba bildirilen hello çalıştırarak hello cihazın komutu aşağıdaki özelliklere alın:</span><span class="sxs-lookup"><span data-stu-id="25377-150">Get hello reported properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="25377-151">$Metadata hello özellikleri biridir. hangi gösterir, bu aygıtın son zamanı hello $lastUpdated gönderir veya bir ileti alır.</span><span class="sxs-lookup"><span data-stu-id="25377-151">One of hello properties is $metadata.$lastUpdated which shows hello last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="25377-152">Twin'ın etiketleriyle ıothub Gezgini'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="25377-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="25377-153">Başlangıç etiketleri ve hello cihaz özelliklerini hello aşağıdaki komutu çalıştırarak görüntüler:</span><span class="sxs-lookup"><span data-stu-id="25377-153">Display hello tags and properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="25377-154">Bir alan rolü eklemek hello aşağıdaki komutu çalıştırarak = sıcaklık ve nem toohello cihazın:</span><span class="sxs-lookup"><span data-stu-id="25377-154">Add a field role = temperature&humidity toohello device by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="25377-155">Bulut cihaza iletileriyle ıothub Gezgini'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="25377-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="25377-156">"Hello World" iletisini toohello aygıt hello aşağıdaki komutu çalıştırarak gönder:</span><span class="sxs-lookup"><span data-stu-id="25377-156">Send a "Hello World" message toohello device by running hello following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="25377-157">Bkz: [iothub-explorer toosend kullanıyorsanız ve cihaz ve IOT hub'ı arasında iletileri alırsanız](iot-hub-explorer-cloud-device-messaging.md) bu komutu kullanarak, gerçek bir senaryo için.</span><span class="sxs-lookup"><span data-stu-id="25377-157">See [Use iothub-explorer toosend and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="25377-158">Cihaz çiftlerini sorgularıyla ıothub Gezgini'ni kullanın</span><span class="sxs-lookup"><span data-stu-id="25377-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="25377-159">Sorgu bir etiket rolünün aygıtlarla 'sıcaklık ve nem' hello aşağıdaki komutu çalıştırarak =:</span><span class="sxs-lookup"><span data-stu-id="25377-159">Query devices with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="25377-160">Bir etiketi rolünün olanlar dışında tüm cihazlar sorgu 'sıcaklık ve nem' hello aşağıdaki komutu çalıştırarak =:</span><span class="sxs-lookup"><span data-stu-id="25377-160">Query all devices except those with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="25377-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="25377-161">Next steps</span></span>

<span data-ttu-id="25377-162">Öğrendiğinize nasıl toouse iothub-Gezgini çeşitli yönetim seçenekleri ile.</span><span class="sxs-lookup"><span data-stu-id="25377-162">You've learned how toouse iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
