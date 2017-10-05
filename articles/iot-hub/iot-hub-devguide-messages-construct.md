---
title: "Azure IOT Hub ileti biçimi anlama | Microsoft Docs"
description: "Geliştirici Kılavuzu - descibes biçimi ve IOT hub'ı iletilerinin beklenen içerik."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: e6eafb1a0030b022da2b5d0b787e092f3067c99f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-and-read-iot-hub-messages"></a><span data-ttu-id="ea28d-103">Oluşturun ve IOT hub'ı iletileri okur</span><span class="sxs-lookup"><span data-stu-id="ea28d-103">Create and read IoT Hub messages</span></span>

<span data-ttu-id="ea28d-104">Protokoller kullanılarak sorunsuz birlikte çalışabilirlik desteklemek için tüm cihaz dönük protokoller için ortak bir ileti biçimi IOT hub'ı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ea28d-104">To support seamless interoperability across protocols, IoT Hub defines a common message format for all device-facing protocols.</span></span> <span data-ttu-id="ea28d-105">Bu ileti biçimi her ikisi için kullanılan [cihaz bulut] [ lnk-d2c] ve [bulut cihaz] [ lnk-c2d] iletileri.</span><span class="sxs-lookup"><span data-stu-id="ea28d-105">This message format is used for both [device-to-cloud][lnk-d2c] and [cloud-to-device][lnk-c2d] messages.</span></span> <span data-ttu-id="ea28d-106">Bir [IOT hub'ı ileti] [ lnk-messaging] oluşur:</span><span class="sxs-lookup"><span data-stu-id="ea28d-106">An [IoT Hub message][lnk-messaging] consists of:</span></span>

* <span data-ttu-id="ea28d-107">Bir dizi *Sistem Özellikleri*.</span><span class="sxs-lookup"><span data-stu-id="ea28d-107">A set of *system properties*.</span></span> <span data-ttu-id="ea28d-108">IOT hub'ı yorumlar veya ayarlayan özellikleri.</span><span class="sxs-lookup"><span data-stu-id="ea28d-108">Properties that IoT Hub interprets or sets.</span></span> <span data-ttu-id="ea28d-109">Bu önceden belirlenmiş kümesidir.</span><span class="sxs-lookup"><span data-stu-id="ea28d-109">This set is predetermined.</span></span>
* <span data-ttu-id="ea28d-110">Bir dizi *uygulama özellikleri*.</span><span class="sxs-lookup"><span data-stu-id="ea28d-110">A set of *application properties*.</span></span> <span data-ttu-id="ea28d-111">Uygulama tanımlayabilirsiniz dize özellikleri ve ileti gövdesi seri durumdan gerek olmadan erişim, sözlüğü.</span><span class="sxs-lookup"><span data-stu-id="ea28d-111">A dictionary of string properties that the application can define and access, without needing to deserialize the message body.</span></span> <span data-ttu-id="ea28d-112">IOT hub'ı hiçbir zaman bu özellikleri değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ea28d-112">IoT Hub never modifies these properties.</span></span>
* <span data-ttu-id="ea28d-113">Donuk bir ikili gövdesi.</span><span class="sxs-lookup"><span data-stu-id="ea28d-113">An opaque binary body.</span></span>

<span data-ttu-id="ea28d-114">Özellik adları ve değerleri yalnızca ASCII alfasayısal karakterler içerebilirler, artı ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`\` olduğunda:</span><span class="sxs-lookup"><span data-stu-id="ea28d-114">Property names and values can only contain ASCII alphanumeric characters, plus ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`\` when you:</span></span>

* <span data-ttu-id="ea28d-115">HTTP protokolünü kullanarak cihaz-bulut iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="ea28d-115">Send device-to-cloud messages using the HTTP protocol.</span></span>
* <span data-ttu-id="ea28d-116">Bulut cihaz iletileri gönderir.</span><span class="sxs-lookup"><span data-stu-id="ea28d-116">Send cloud-to-device messages.</span></span>

<span data-ttu-id="ea28d-117">Kodlamak ve farklı protokoller kullanılarak gönderilen iletileri kod çözme hakkında daha fazla bilgi için bkz: [Azure IOT SDK'ları][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="ea28d-117">For more information about how to encode and decode messages sent using different protocols, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="ea28d-118">Aşağıdaki tabloda, IOT hub'ı iletileri Sistem özelliklerinde kümesini listeler.</span><span class="sxs-lookup"><span data-stu-id="ea28d-118">The following table lists the set of system properties in IoT Hub messages.</span></span>

| <span data-ttu-id="ea28d-119">Özellik</span><span class="sxs-lookup"><span data-stu-id="ea28d-119">Property</span></span> | <span data-ttu-id="ea28d-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ea28d-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ea28d-121">MessageID</span><span class="sxs-lookup"><span data-stu-id="ea28d-121">MessageId</span></span> |<span data-ttu-id="ea28d-122">İstek-yanıt desenler için kullanılan ileti için kullanıcı ayarlanabilir bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="ea28d-122">A user-settable identifier for the message used for request-reply patterns.</span></span> <span data-ttu-id="ea28d-123">Biçimi: Büyük küçük harfe duyarlı dizesi (en fazla 128 karakter uzunluğunda) ASCII 7 bit alfasayısal karakter + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`.</span><span class="sxs-lookup"><span data-stu-id="ea28d-123">Format: A case-sensitive string (up to 128 characters long) of ASCII 7-bit alphanumeric characters + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`.</span></span> |
| <span data-ttu-id="ea28d-124">Sıra numarası</span><span class="sxs-lookup"><span data-stu-id="ea28d-124">Sequence number</span></span> |<span data-ttu-id="ea28d-125">Her bulut cihaz iletiye IOT Hub tarafından atanan bir sayı (aygıt sırası benzersiz).</span><span class="sxs-lookup"><span data-stu-id="ea28d-125">A number (unique per device-queue) assigned by IoT Hub to each cloud-to-device message.</span></span> |
| <span data-ttu-id="ea28d-126">Bitiş</span><span class="sxs-lookup"><span data-stu-id="ea28d-126">To</span></span> |<span data-ttu-id="ea28d-127">Belirtilen bir hedef [bulut cihaz] [ lnk-c2d] iletileri.</span><span class="sxs-lookup"><span data-stu-id="ea28d-127">A destination specified in [Cloud-to-Device][lnk-c2d] messages.</span></span> |
| <span data-ttu-id="ea28d-128">ExpiryTimeUtc</span><span class="sxs-lookup"><span data-stu-id="ea28d-128">ExpiryTimeUtc</span></span> |<span data-ttu-id="ea28d-129">Tarih ve saat iletisi süre sonu.</span><span class="sxs-lookup"><span data-stu-id="ea28d-129">Date and time of message expiration.</span></span> |
| <span data-ttu-id="ea28d-130">EnqueuedTime</span><span class="sxs-lookup"><span data-stu-id="ea28d-130">EnqueuedTime</span></span> |<span data-ttu-id="ea28d-131">Tarih ve saat [bulut cihaz] [ lnk-c2d] ileti IOT Hub tarafından alındı.</span><span class="sxs-lookup"><span data-stu-id="ea28d-131">Date and time the [Cloud-to-Device][lnk-c2d] message was received by IoT Hub.</span></span> |
| <span data-ttu-id="ea28d-132">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="ea28d-132">CorrelationId</span></span> |<span data-ttu-id="ea28d-133">Bir dize özelliği genellikle istek, istek-yanıt desenleri MessageID içeren bir yanıt iletisi.</span><span class="sxs-lookup"><span data-stu-id="ea28d-133">A string property in a response message that typically contains the MessageId of the request, in request-reply patterns.</span></span> |
| <span data-ttu-id="ea28d-134">Kullanıcı Kimliği</span><span class="sxs-lookup"><span data-stu-id="ea28d-134">UserId</span></span> |<span data-ttu-id="ea28d-135">İletileri kökeni belirtmek için kullanılan bir kimliği.</span><span class="sxs-lookup"><span data-stu-id="ea28d-135">An ID used to specify the origin of messages.</span></span> <span data-ttu-id="ea28d-136">IOT Hub tarafından iletileri oluşturulduğunda ayarlanır `{iot hub name}`.</span><span class="sxs-lookup"><span data-stu-id="ea28d-136">When messages are generated by IoT Hub, it is set to `{iot hub name}`.</span></span> |
| <span data-ttu-id="ea28d-137">ACK</span><span class="sxs-lookup"><span data-stu-id="ea28d-137">Ack</span></span> |<span data-ttu-id="ea28d-138">Geri bildirim iletisi üreteci.</span><span class="sxs-lookup"><span data-stu-id="ea28d-138">A feedback message generator.</span></span> <span data-ttu-id="ea28d-139">Bu özellik bulut cihaz iletilerinde aygıt tarafından tüketilen iletinin sonucunda geri bildirim iletileri oluşturmak için IOT Hub istemek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ea28d-139">This property is used in cloud-to-device messages to request IoT Hub to generate feedback messages as a result of the consumption of the message by the device.</span></span> <span data-ttu-id="ea28d-140">Olası değerler: **hiçbiri** (varsayılan): hiçbir geri bildirim iletisi oluşturulur, **pozitif**: ileti tamamlanmışsa bir geri bildirim iletisi **negatif**: alma bir iletinin zaman aşımına (veya en yüksek teslimat sayısı ulaşıldı varsa) aygıtıyla tamamlandığı olmadan geri bildirim iletisi veya **tam**: pozitif ve negatif.</span><span class="sxs-lookup"><span data-stu-id="ea28d-140">Possible values: **none** (default): no feedback message is generated, **positive**: receive a feedback message if the message was completed, **negative**: receive a feedback message if the message expired (or maximum delivery count was reached) without being completed by the device, or **full**: both positive and negative.</span></span> <span data-ttu-id="ea28d-141">Daha fazla bilgi için bkz: [ileti geri bildirim][lnk-feedback].</span><span class="sxs-lookup"><span data-stu-id="ea28d-141">For more information, see [Message feedback][lnk-feedback].</span></span> |
| <span data-ttu-id="ea28d-142">ConnectionDeviceId</span><span class="sxs-lookup"><span data-stu-id="ea28d-142">ConnectionDeviceId</span></span> |<span data-ttu-id="ea28d-143">IOT Hub tarafından cihaz bulut iletilerini üzerinde ayarlanmış bir kimliği.</span><span class="sxs-lookup"><span data-stu-id="ea28d-143">An ID set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="ea28d-144">İçerdiği **DeviceID** iletiyi gönderen cihaz.</span><span class="sxs-lookup"><span data-stu-id="ea28d-144">It contains the **deviceId** of the device that sent the message.</span></span> |
| <span data-ttu-id="ea28d-145">ConnectionDeviceGenerationId</span><span class="sxs-lookup"><span data-stu-id="ea28d-145">ConnectionDeviceGenerationId</span></span> |<span data-ttu-id="ea28d-146">IOT Hub tarafından cihaz bulut iletilerini üzerinde ayarlanmış bir kimliği.</span><span class="sxs-lookup"><span data-stu-id="ea28d-146">An ID set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="ea28d-147">İçerdiği **Generationıd** (göre [aygıt kimlik özellikleri][lnk-device-properties]) iletiyi gönderen cihaz.</span><span class="sxs-lookup"><span data-stu-id="ea28d-147">It contains the **generationId** (as per [Device identity properties][lnk-device-properties]) of the device that sent the message.</span></span> |
| <span data-ttu-id="ea28d-148">ConnectionAuthMethod</span><span class="sxs-lookup"><span data-stu-id="ea28d-148">ConnectionAuthMethod</span></span> |<span data-ttu-id="ea28d-149">IOT Hub tarafından cihaz bulut iletilerini üzerinde ayarlanmış bir kimlik doğrulama yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ea28d-149">An authentication method set by IoT Hub on device-to-cloud messages.</span></span> <span data-ttu-id="ea28d-150">Bu özellik, iletiyi göndermeyi cihazın kimliğini doğrulamak için kullanılan kimlik doğrulama yöntemi hakkında bilgi içerir.</span><span class="sxs-lookup"><span data-stu-id="ea28d-150">This property contains information about the authentication method used to authenticate the device sending the message.</span></span> <span data-ttu-id="ea28d-151">Daha fazla bilgi için bkz: [yanıltma bulut aygıta][lnk-antispoofing].</span><span class="sxs-lookup"><span data-stu-id="ea28d-151">For more information, see [Device to cloud anti-spoofing][lnk-antispoofing].</span></span> |

## <a name="message-size"></a><span data-ttu-id="ea28d-152">İleti boyutu</span><span class="sxs-lookup"><span data-stu-id="ea28d-152">Message size</span></span>

<span data-ttu-id="ea28d-153">IOT hub'ı yalnızca gerçek yükü dikkate Protokolü belirsiz şekilde, ileti boyutu ölçer.</span><span class="sxs-lookup"><span data-stu-id="ea28d-153">IoT Hub measures message size in a protocol-agnostic way, considering only the actual payload.</span></span> <span data-ttu-id="ea28d-154">Bayt cinsinden boyutu toplamı aşağıdaki olarak hesaplanır:</span><span class="sxs-lookup"><span data-stu-id="ea28d-154">The size in bytes is calculated as the sum of the following:</span></span>

* <span data-ttu-id="ea28d-155">Gövde boyutu bayt.</span><span class="sxs-lookup"><span data-stu-id="ea28d-155">The body size in bytes.</span></span>
* <span data-ttu-id="ea28d-156">İleti sistemi özelliklerini tüm değerlerin bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="ea28d-156">The size in bytes of all the values of the message system properties.</span></span>
* <span data-ttu-id="ea28d-157">Tüm kullanıcı özellik adları ve değerleri bayt cinsinden boyutu.</span><span class="sxs-lookup"><span data-stu-id="ea28d-157">The size in bytes of all user property names and values.</span></span>

<span data-ttu-id="ea28d-158">Dolayısıyla bayt cinsinden boyutu dize uzunluğu eşittir özellik adları ve değerleri ASCII karakter ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="ea28d-158">Property names and values are limited to ASCII characters, so the length of the strings equals the size in bytes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea28d-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea28d-159">Next steps</span></span>

<span data-ttu-id="ea28d-160">IOT Hub'ındaki ileti boyutu sınırları hakkında daha fazla bilgi için bkz: [IOT hub'ı kotalar ve azaltma][lnk-quotas].</span><span class="sxs-lookup"><span data-stu-id="ea28d-160">For information about message size limits in IoT Hub, see [IoT Hub quotas and throttling][lnk-quotas].</span></span>

<span data-ttu-id="ea28d-161">Oluşturun ve IOT hub'ı çeşitli programlama dillerinde iletileri okumak öğrenmek için bkz: [başlama] [ lnk-get-started] öğreticileri.</span><span class="sxs-lookup"><span data-stu-id="ea28d-161">To learn how to create and read IoT Hub messages in various programming languages, see the [Get started][lnk-get-started] tutorials.</span></span>

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
