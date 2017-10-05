---
title: "Azure IOT cihaz SDK'sı c - IoTHubClient | Microsoft Docs"
description: "Azure IOT cihaz SDK'sı c IoTHubClient kitaplıkta bir IOT hub ile iletişim cihaz uygulamaları oluşturmak için nasıl kullanılacağını."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: 828cf2bf-999d-4b8a-8a28-c7c901629600
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: 422d89014511f0d08ba57a893570ff7b253b7bc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a><span data-ttu-id="1da4f-103">C – IoTHubClient hakkında daha fazla bilgi için Azure IOT cihaz SDK'sı</span><span class="sxs-lookup"><span data-stu-id="1da4f-103">Azure IoT device SDK for C – more about IoTHubClient</span></span>
<span data-ttu-id="1da4f-104">[İlk makale](iot-hub-device-sdk-c-intro.md) sunulan bu serideki **C için Azure IOT cihaz SDK'sı**. Bu makale, SDK içinde iki Mimari katman vardır açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. That article explained that there are two architectural layers in SDK.</span></span> <span data-ttu-id="1da4f-105">Temeli **IoTHubClient** doğrudan IOT Hub ile iletişim yöneten kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="1da4f-105">At the base is the **IoTHubClient** library which directly manages communication with IoT Hub.</span></span> <span data-ttu-id="1da4f-106">Ayrıca **seri hale getirici** serileştirme hizmetleri sağlamak için açık üst o derlemeler kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="1da4f-106">There's also the **serializer** library that builds on top of that to provide serialization services.</span></span> <span data-ttu-id="1da4f-107">Bu makalede ek ayrıntı sağlarız **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="1da4f-107">In this article we'll provide additional detail on the **IoTHubClient** library.</span></span>

<span data-ttu-id="1da4f-108">Önceki makalede açıklanan nasıl kullanılacağını **IoTHubClient** iletileri IOT Hub'ına olayları göndermek ve almak için kitaplık.</span><span class="sxs-lookup"><span data-stu-id="1da4f-108">The previous article described how to use the **IoTHubClient** library to send events to IoT Hub and receive messages.</span></span> <span data-ttu-id="1da4f-109">Bu makalede bu tartışma nasıl daha kesin olarak yönetilir açıklayarak genişletir *zaman* için giriş veri gönderip **düşük düzeyli API'leri**.</span><span class="sxs-lookup"><span data-stu-id="1da4f-109">This article extends that discussion by explaining how to more precisely manage *when* you send and receive data, introducing you to the **lower-level APIs**.</span></span> <span data-ttu-id="1da4f-110">Olayları Özellikler ekleme (ve gelen iletileri almak) nasıl ayrıca açıklayacağız özelliklerinde işleme özelliğini kullanarak **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="1da4f-110">We'll also explain how to attach properties to events (and retrieve them from messages) using the property handling features in the **IoTHubClient** library.</span></span> <span data-ttu-id="1da4f-111">Son olarak, IOT Hub'ından alınan iletileri işlemek için farklı yollar ek açıklama sağlarız.</span><span class="sxs-lookup"><span data-stu-id="1da4f-111">Finally, we'll provide additional explanation of different ways to handle messages received from IoT Hub.</span></span>

<span data-ttu-id="1da4f-112">Makaleyi birkaç aygıt kimlik bilgisi ve davranışını değiştirme hakkında daha fazla dahil çeşitli konuları kapsayan sonucuna **IoTHubClient** yapılandırma seçenekleri üzerinden.</span><span class="sxs-lookup"><span data-stu-id="1da4f-112">The article concludes by covering a couple of miscellaneous topics, including more about device credentials and how to change the behavior of the **IoTHubClient** through configuration options.</span></span>

<span data-ttu-id="1da4f-113">Kullanacağız **IoTHubClient** SDK örnekleri bu konular açıklanır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-113">We'll use the **IoTHubClient** SDK samples to explain these topics.</span></span> <span data-ttu-id="1da4f-114">İzlemek istiyorsanız, bkz: **ıothub\_istemci\_örnek\_http** ve **ıothub\_istemci\_örnek\_amqp**C. aşağıdaki bölümlerde açıklanan her şey bu örnekleri gösterilmiştir için Azure IOT cihaz SDK'sı bulunan uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="1da4f-114">If you want to follow along, see the **iothub\_client\_sample\_http** and **iothub\_client\_sample\_amqp** applications that are included in the Azure IoT device SDK for C. Everything described in the following sections is demonstrated in these samples.</span></span>

<span data-ttu-id="1da4f-115">Bulabileceğiniz [ **C için Azure IOT cihaz SDK'sı** ](https://github.com/Azure/azure-iot-sdk-c) GitHub depo ve görünüm ayrıntılarını API [C API Başvurusu](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="1da4f-115">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="1da4f-116">Alt düzey API'ları</span><span class="sxs-lookup"><span data-stu-id="1da4f-116">The lower-level APIs</span></span>
<span data-ttu-id="1da4f-117">Temel işlemi önceki makalede açıklanan **IotHubClient** bağlamında **ıothub\_istemci\_örnek\_amqp** uygulama.</span><span class="sxs-lookup"><span data-stu-id="1da4f-117">The previous article described the basic operation of the **IotHubClient** within the context of the **iothub\_client\_sample\_amqp** application.</span></span> <span data-ttu-id="1da4f-118">Örneğin, bu kodu kullanarak kitaplığı başlatılamadı nasıl açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-118">For example, it explained how to initialize the library using this code.</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="1da4f-119">Ayrıca, bu işlev çağrısı kullanarak olayları göndermek nasıl açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-119">It also described how to send events using this function call.</span></span>

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

<span data-ttu-id="1da4f-120">Makale, bir geri çağırma işlevini kaydederek ileti alma de açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-120">The article also described how to receive messages by registering a callback function.</span></span>

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

<span data-ttu-id="1da4f-121">Makale ayrıca aşağıdaki gibi kod kullanarak kaynakları serbest nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-121">The article also showed how to free resources using code such as the following.</span></span>

```
IoTHubClient_Destroy(iotHubClientHandle);
```

<span data-ttu-id="1da4f-122">Ancak bu API'leri her yardımcı işlevleri vardır:</span><span class="sxs-lookup"><span data-stu-id="1da4f-122">However there are companion functions to each of these APIs:</span></span>

* <span data-ttu-id="1da4f-123">IoTHubClient\_ÜM\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="1da4f-123">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="1da4f-124">IoTHubClient\_ÜM\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="1da4f-124">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="1da4f-125">IoTHubClient\_ÜM\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="1da4f-125">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="1da4f-126">IoTHubClient\_ÜM\_yok</span><span class="sxs-lookup"><span data-stu-id="1da4f-126">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="1da4f-127">Tüm bu işlevler "Tümü" API adını içerir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-127">These functions all include “LL” in the API name.</span></span> <span data-ttu-id="1da4f-128">İlgili dışında bu işlevlerin her biri parametrelerinin ÜM olmayan dekiler aynıdır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-128">Other than that, the parameters of each of these functions are identical to their non-LL counterparts.</span></span> <span data-ttu-id="1da4f-129">Ancak, bu işlevler davranışını önemli bir şekilde farklıdır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-129">However, the behavior of these functions is different in one important way.</span></span>

<span data-ttu-id="1da4f-130">Çağırdığınızda **IoTHubClient\_CreateFromConnectionString**, temel alınan kitaplıkları arka planda çalışan yeni bir iş parçacığı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-130">When you call **IoTHubClient\_CreateFromConnectionString**, the underlying libraries create a new thread that runs in the background.</span></span> <span data-ttu-id="1da4f-131">Bu iş parçacığı olayları gönderir ve IOT Hub'ından, iletileri alır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-131">This thread sends events to, and receives messages from, IoT Hub.</span></span> <span data-ttu-id="1da4f-132">Bu tür bir iş parçacığı "ÜM ile" API'leri çalışırken oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1da4f-132">No such thread is created when working with the "LL" APIs.</span></span> <span data-ttu-id="1da4f-133">Arka plan iş parçacığı oluşturmayı geliştiriciye kolaylık sağlamak amacıyla ' dir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-133">The creation of the background thread is a convenience to the developer.</span></span> <span data-ttu-id="1da4f-134">Açıkça olayları ileti gönderme ve IOT Hub'ından--arka planda otomatik olarak gerçekleşir alma hakkında endişelenmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1da4f-134">You don’t have to worry about explicitly sending events and receiving messages from IoT Hub -- it happens automatically in the background.</span></span> <span data-ttu-id="1da4f-135">Buna karşılık, ihtiyacınız olursa "Tümü" API'leri, IOT Hub ile iletişim üzerinde açık denetim sağlar.</span><span class="sxs-lookup"><span data-stu-id="1da4f-135">In contrast, the "LL" APIs give you explicit control over communication with IoT Hub, if you need it.</span></span>

<span data-ttu-id="1da4f-136">Bu daha iyi anlamak için bir örneğe bakalım:</span><span class="sxs-lookup"><span data-stu-id="1da4f-136">To understand this better, let’s look at an example:</span></span>

<span data-ttu-id="1da4f-137">Çağırdığınızda **IoTHubClient\_SendEventAsync**, gerçekte ne gerçekleştirmekte olduğunuz olay arabellekte koyuyor.</span><span class="sxs-lookup"><span data-stu-id="1da4f-137">When you call **IoTHubClient\_SendEventAsync**, what you're actually doing is putting the event in a buffer.</span></span> <span data-ttu-id="1da4f-138">Çağırdığınızda oluşturulan arka plan iş parçacığı **IoTHubClient\_CreateFromConnectionString** sürekli olarak bu arabellek izler ve içerdiği herhangi bir veri IOT Hub'ına gönderir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-138">The background thread created when you call **IoTHubClient\_CreateFromConnectionString** continually monitors this buffer and sends any data that it contains to IoT Hub.</span></span> <span data-ttu-id="1da4f-139">Bu, ana iş parçacığının başka işler gerçekleştiriyor aynı anda arka planda gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-139">This happens in the background at the same time that the main thread is performing other work.</span></span>

<span data-ttu-id="1da4f-140">Benzer şekilde, bir geri çağırma işlevini kullanarak iletileri için kaydettiğinizde **IoTHubClient\_SetMessageCallback**, SDK'sını bir ileti olduğunda geri çağırma işlevi çağırma arka plan iş parçacığı sahip sunuculardaki gerektiğini belirten alınan, ana iş parçacığı bağımsızdır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-140">Similarly, when you register a callback function for messages using **IoTHubClient\_SetMessageCallback**, you're instructing the SDK to have the background thread invoke the callback function when a message is received, independent of the main thread.</span></span>

<span data-ttu-id="1da4f-141">"Tümü" API'leri arka plan iş parçacığı oluşturmayın.</span><span class="sxs-lookup"><span data-stu-id="1da4f-141">The "LL" APIs don’t create a background thread.</span></span> <span data-ttu-id="1da4f-142">Bunun yerine, yeni bir API açıkça göndermek ve IOT Hub'ından veri almak için çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-142">Instead, a new API must be called to explicitly send and receive data from IoT Hub.</span></span> <span data-ttu-id="1da4f-143">Bu aşağıdaki örnekte gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-143">This is demonstrated in the following example.</span></span>

<span data-ttu-id="1da4f-144">**Iothub\_istemci\_örnek\_http** SDK'da bulunan uygulama alt düzey API'ları gösterir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-144">The **iothub\_client\_sample\_http** application that’s included in the SDK demonstrates the lower-level APIs.</span></span> <span data-ttu-id="1da4f-145">Bu örnekte, biz olayları IOT Hub'ına aşağıdaki gibi kod ile gönder:</span><span class="sxs-lookup"><span data-stu-id="1da4f-145">In that sample, we send events to IoT Hub with code such as the following:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="1da4f-146">İlk üç satırını iletisi oluşturun ve son satırında olay gönderir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-146">The first three lines create the message, and the last line sends the event.</span></span> <span data-ttu-id="1da4f-147">Ancak, daha önce belirtildiği gibi "Olay verileri yalnızca bir arabellek yerleştirilir anlamına gelir gönderme".</span><span class="sxs-lookup"><span data-stu-id="1da4f-147">However, as mentioned previously, "sending" the event means that the data is simply placed in a buffer.</span></span> <span data-ttu-id="1da4f-148">Biz çağırdığınızda hiçbir şey ağ üzerinde aktarılan **IoTHubClient\_ÜM\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="1da4f-148">Nothing is transmitted on the network when we call **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="1da4f-149">Gerçekte giriş verileri IOT Hub'ına için sırayla çağırmalısınız **IoTHubClient\_ÜM\_DoWork**, bu örnekteki gibi:</span><span class="sxs-lookup"><span data-stu-id="1da4f-149">In order to actually ingress the data to IoT Hub, you must call **IoTHubClient\_LL\_DoWork**, as in this example:</span></span>

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="1da4f-150">Bu kod (gelen **ıothub\_istemci\_örnek\_http** uygulama) art arda çağırır **IoTHubClient\_ÜM\_DoWork**.</span><span class="sxs-lookup"><span data-stu-id="1da4f-150">This code (from the **iothub\_client\_sample\_http** application) repeatedly calls **IoTHubClient\_LL\_DoWork**.</span></span> <span data-ttu-id="1da4f-151">Her zaman **IoTHubClient\_ÜM\_DoWork** olan çağrılır, bazı olaylar arabelleğinden IOT Hub'ına gönderir ve cihaza gönderilen sıraya alınmış bir iletiyi alır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-151">Each time **IoTHubClient\_LL\_DoWork** is called, it sends some events from the buffer to IoT Hub and it retrieves a queued message being sent to the device.</span></span> <span data-ttu-id="1da4f-152">İkinci durumda, biz iletiler için bir geri çağırma işlevini kaydettiyseniz, daha sonra geri çağırma (herhangi bir ileti kuyruğa varsayılarak) çağrılması anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-152">The latter case means that if we registered a callback function for messages, then the callback is invoked (assuming any messages are queued up).</span></span> <span data-ttu-id="1da4f-153">Biz bu tür bir geri çağırma işlevi aşağıdaki gibi kod ile kayıtlı:</span><span class="sxs-lookup"><span data-stu-id="1da4f-153">We would have registered such a callback function with code such as the following:</span></span>

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

<span data-ttu-id="1da4f-154">Bunun nedeni, **IoTHubClient\_ÜM\_DoWork** çoğunlukla adı verilir bir döngü değil, her kez çağırıldığında, gönderir *bazı* IOT Hub ve alır olaylarınıarabelleğe*sonraki* iletisi sıraya cihaz için.</span><span class="sxs-lookup"><span data-stu-id="1da4f-154">The reason that **IoTHubClient\_LL\_DoWork** is often called in a loop is that each time it’s called, it sends *some* buffered events to IoT Hub and retrieves *the next* message queued up for the device.</span></span> <span data-ttu-id="1da4f-155">Her çağrı tüm arabelleğe alınmış olayları göndermek için garantisi yoktur veya tüm almak için sıraya alınan iletileri.</span><span class="sxs-lookup"><span data-stu-id="1da4f-155">Each call isn’t guaranteed to send all buffered events or to retrieve all queued messages.</span></span> <span data-ttu-id="1da4f-156">Arabellekte tüm olayları göndermek ve ardından başka bir işlem ile çalışmaya devam etmek istiyorsanız, aşağıdaki gibi kod ile bu döngü değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1da4f-156">If you want to send all events in the buffer and then continue on with other processing you can replace this loop with code such as the following:</span></span>

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="1da4f-157">Bu kod çağırır **IoTHubClient\_ÜM\_DoWork** arabelleği tüm olayları IOT hub'a gönderilen kadar.</span><span class="sxs-lookup"><span data-stu-id="1da4f-157">This code calls **IoTHubClient\_LL\_DoWork** until all events in the buffer have been sent to IoT Hub.</span></span> <span data-ttu-id="1da4f-158">Bu ayrıca tüm sıraya alınan iletileri alınmış olan anlamına gelmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1da4f-158">Note this does not also imply that all queued messages have been received.</span></span> <span data-ttu-id="1da4f-159">Bunun nedeni parçası "tümü" iletileri denetleme gibi belirleyici bir eylem olmadığından emin olur.</span><span class="sxs-lookup"><span data-stu-id="1da4f-159">Part of the reason for this is that checking for "all" messages isn’t as deterministic an action.</span></span> <span data-ttu-id="1da4f-160">"Tüm" iletileri almak, ancak başka bir cihaza gönderilir ne olur hemen sonra?</span><span class="sxs-lookup"><span data-stu-id="1da4f-160">What happens if you retrieve "all" of the messages, but then another one is sent to the device immediately after?</span></span> <span data-ttu-id="1da4f-161">Programlı bir zaman aşımı ile ile mücadele etmek için daha iyi bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="1da4f-161">A better way to deal with that is with a programmed timeout.</span></span> <span data-ttu-id="1da4f-162">Örneğin, ileti geri çağırma işlevi çağrılması her zaman bir süreölçeri sıfırlanamadı.</span><span class="sxs-lookup"><span data-stu-id="1da4f-162">For example, the message callback function could reset a timer every time it’s invoked.</span></span> <span data-ttu-id="1da4f-163">Örneğin, son alınan ileti değilse, işleme devam etmek için mantığı sonra yazabilirsiniz *X* saniye.</span><span class="sxs-lookup"><span data-stu-id="1da4f-163">You can then write logic to continue processing if, for example, no messages have been received in the last *X* seconds.</span></span>

<span data-ttu-id="1da4f-164">Ne zaman tamamlanmış ingressing olayları olduğunuz ve iletilerini alma kaynakları temizlemek için karşılık gelen işlevi çağırdığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="1da4f-164">When you’re finished ingressing events and receiving messages, be sure to call the corresponding function to clean up resources.</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="1da4f-165">Temel olarak yalnızca bir dizi arka plan iş parçacığı ve başka bir dizi arka plan iş parçacığı olmadan aynı şeyi yapar API ile veri göndermek ve almak için API yoktur.</span><span class="sxs-lookup"><span data-stu-id="1da4f-165">Basically there’s only one set of APIs to send and receive data with a background thread and another set of APIs that does the same thing without the background thread.</span></span> <span data-ttu-id="1da4f-166">Geliştiricilerin çok olmayan - ÜM API'leri tercih edebilirsiniz, ancak geliştirici ağ aktarımları üzerinde açık denetim istediğinde düşük düzeyli API'leri yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-166">A lot of developers may prefer the non-LL APIs, but the lower-level APIs are useful when the developer wants explicit control over network transmissions.</span></span> <span data-ttu-id="1da4f-167">Örneğin, bazı aygıtlar veri zaman ve yalnızca giriş olayları belirtilen aralıklarla (örneğin, saatte bir kez veya günde bir kez) toplar.</span><span class="sxs-lookup"><span data-stu-id="1da4f-167">For example, some devices collect data over time and only ingress events at specified intervals (for example, once an hour or once a day).</span></span> <span data-ttu-id="1da4f-168">IOT Hub'ından veri gönderip alırken düşük düzeyli API'leri, açıkça denetimine sağlıyor.</span><span class="sxs-lookup"><span data-stu-id="1da4f-168">The lower-level APIs give you the ability to explicitly control when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="1da4f-169">Başkalarının yalnızca alt düzey API'ler sağlar basitliğini tercih eder.</span><span class="sxs-lookup"><span data-stu-id="1da4f-169">Others will simply prefer the simplicity that the lower-level APIs provide.</span></span> <span data-ttu-id="1da4f-170">Bazı iş oluşmasını arka planda yerine ana iş parçacığı her şeyi olur.</span><span class="sxs-lookup"><span data-stu-id="1da4f-170">Everything happens on the main thread rather than some work happening in the background.</span></span>

<span data-ttu-id="1da4f-171">Seçtiğiniz hangi model kullandığınız hangi API'leri tutarlı olacak şekilde emin olun.</span><span class="sxs-lookup"><span data-stu-id="1da4f-171">Whichever model you choose, be sure to be consistent in which APIs you use.</span></span> <span data-ttu-id="1da4f-172">Çağırarak başlatırsanız **IoTHubClient\_ÜM\_CreateFromConnectionString**, yalnızca kullandığınız karşılık gelen alt düzey API'ları için herhangi bir izleme iş emin olun:</span><span class="sxs-lookup"><span data-stu-id="1da4f-172">If you start by calling **IoTHubClient\_LL\_CreateFromConnectionString**, be sure you only use the corresponding lower-level APIs for any follow-up work:</span></span>

* <span data-ttu-id="1da4f-173">IoTHubClient\_ÜM\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="1da4f-173">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="1da4f-174">IoTHubClient\_ÜM\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="1da4f-174">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="1da4f-175">IoTHubClient\_ÜM\_yok</span><span class="sxs-lookup"><span data-stu-id="1da4f-175">IoTHubClient\_LL\_Destroy</span></span>
* <span data-ttu-id="1da4f-176">IoTHubClient\_ÜM\_DoWork</span><span class="sxs-lookup"><span data-stu-id="1da4f-176">IoTHubClient\_LL\_DoWork</span></span>

<span data-ttu-id="1da4f-177">Bunun tersi de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-177">The opposite is true as well.</span></span> <span data-ttu-id="1da4f-178">İle başlatırsanız, **IoTHubClient\_CreateFromConnectionString**, ardından herhangi bir ek işlem dışı - ÜM API'leri kullanın.</span><span class="sxs-lookup"><span data-stu-id="1da4f-178">If you start with **IoTHubClient\_CreateFromConnectionString**, then use the non-LL APIs for any additional processing.</span></span>

<span data-ttu-id="1da4f-179">Azure IOT cihazı SDK C için bkz: **ıothub\_istemci\_örnek\_http** düşük düzeyli API'leri tam bir örnek uygulama.</span><span class="sxs-lookup"><span data-stu-id="1da4f-179">In the Azure IoT device SDK for C, see the **iothub\_client\_sample\_http** application for a complete example of the lower-level APIs.</span></span> <span data-ttu-id="1da4f-180">**Iothub\_istemci\_örnek\_amqp** uygulama tam bir örnek için harici - ÜM API'leri başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-180">The **iothub\_client\_sample\_amqp** application can be referenced for a full example of the non-LL APIs.</span></span>

## <a name="property-handling"></a><span data-ttu-id="1da4f-181">Özellik işleme</span><span class="sxs-lookup"><span data-stu-id="1da4f-181">Property handling</span></span>
<span data-ttu-id="1da4f-182">Verileri gönderilirken açıklanan zaman kadarki biz ileti gövdesini başvuran.</span><span class="sxs-lookup"><span data-stu-id="1da4f-182">So far when we've described sending data, we've been referring to the body of the message.</span></span> <span data-ttu-id="1da4f-183">Örneğin, bu kod göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="1da4f-183">For example, consider this code:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="1da4f-184">Bu örnek ileti IOT Hub'ına metinle "Hello World." gönderir</span><span class="sxs-lookup"><span data-stu-id="1da4f-184">This example sends a message to IoT Hub with the text "Hello World."</span></span> <span data-ttu-id="1da4f-185">Ancak, IOT hub'ı her iletisine iliştirilecek özellikleri de sağlar.</span><span class="sxs-lookup"><span data-stu-id="1da4f-185">However, IoT Hub also allows properties to be attached to each message.</span></span> <span data-ttu-id="1da4f-186">İletiye eklenmiş ad/değer çiftleri özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-186">Properties are name/value pairs that can be attached to the message.</span></span> <span data-ttu-id="1da4f-187">Örneğin, biz iletiye bir özellik eklemek için önceki kod değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1da4f-187">For example, we can modify the previous code to attach a property to the message:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="1da4f-188">Arayarak Başlat **IoTHubMessage\_özellikleri** ve bizim ileti işleyicisini geçirme.</span><span class="sxs-lookup"><span data-stu-id="1da4f-188">We start by calling **IoTHubMessage\_Properties** and passing it the handle of our message.</span></span> <span data-ttu-id="1da4f-189">Ne biz geri alırsınız bir **harita\_İŞLEMEK** Özellikler ekleme başlatmak için bize etkinleştirir başvuru.</span><span class="sxs-lookup"><span data-stu-id="1da4f-189">What we get back is a **MAP\_HANDLE** reference that enables us to start adding properties.</span></span> <span data-ttu-id="1da4f-190">İkinci çağırarak gerçekleştirilir **harita\_örnek**, bir harita başvuru alır\_TANITICISI, özellik adı ve özellik değeri.</span><span class="sxs-lookup"><span data-stu-id="1da4f-190">The latter is accomplished by calling **Map\_AddOrUpdate**, which takes a reference to a MAP\_HANDLE, the property name, and the property value.</span></span> <span data-ttu-id="1da4f-191">Bu API ile biz istediğiniz sayıda özellik ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="1da4f-191">With this API we can add as many properties as we like.</span></span>

<span data-ttu-id="1da4f-192">Ne zaman olay okunur gelen **olay hub'ları**, alıcı özellikler numaralandırılmaya ve bunlara karşılık gelen değerler alır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-192">When the event is read from **Event Hubs**, the receiver can enumerate the properties and retrieve their corresponding values.</span></span> <span data-ttu-id="1da4f-193">Örneğin, .NET içinde bu erişerek gerçekleştirilmesi [EventData nesne üzerindeki özellikleri koleksiyonu](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span><span class="sxs-lookup"><span data-stu-id="1da4f-193">For example, in .NET this would be accomplished by accessing the [Properties collection on the EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span></span>

<span data-ttu-id="1da4f-194">Önceki örnekte, biz özellikleri size IOT Hub'ına göndereceğiz olaya ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="1da4f-194">In the previous example, we’re attaching properties to an event that we send to IoT Hub.</span></span> <span data-ttu-id="1da4f-195">Özellikler, IOT Hub'ından alınan iletileri da eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-195">Properties can also be attached to messages received from IoT Hub.</span></span> <span data-ttu-id="1da4f-196">Biz iletiden özelliklerini almak istiyorsanız, aşağıdaki gibi kod bizim ileti geri çağırma işlevini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1da4f-196">If we want to retrieve properties from a message, we can use code such as the following in our message callback function:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from the message
    MAP_HANDLE mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                printf("Message Properties:\r\n");
                for (size_t index = 0; index < propertyCount; index++)
                {
                    printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                printf("\r\n");
            }
        }
    }

    . . .
}
```

<span data-ttu-id="1da4f-197">Çağrı **IoTHubMessage\_özellikleri** döndürür **harita\_İŞLEMEK** başvuru.</span><span class="sxs-lookup"><span data-stu-id="1da4f-197">The call to **IoTHubMessage\_Properties** returns the **MAP\_HANDLE** reference.</span></span> <span data-ttu-id="1da4f-198">Biz sonra bu başvuruyu iletebilir **harita\_GetInternals** ad/değer çiftleri (yanı sıra özellikleri sayısı) dizisi başvuru elde edilir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-198">We then pass that reference to **Map\_GetInternals** to obtain a reference to an array of the name/value pairs (as well as a count of the properties).</span></span> <span data-ttu-id="1da4f-199">Bu noktada istiyoruz değerlerini almak için özellikleri numaralandırma, atmaktan değil.</span><span class="sxs-lookup"><span data-stu-id="1da4f-199">At that point it's a simple matter of enumerating the properties to get to the values we want.</span></span>

<span data-ttu-id="1da4f-200">Uygulamanızda özelliklerini kullanmak zorunda değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="1da4f-200">You don't have to use properties in your application.</span></span> <span data-ttu-id="1da4f-201">Ancak, olaylarına ayarlamak veya gelen iletileri almak gerekiyorsa **IoTHubClient** kitaplığı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-201">However, if you need to set them on events or retrieve them from messages, the **IoTHubClient** library makes it easy.</span></span>

## <a name="message-handling"></a><span data-ttu-id="1da4f-202">İleti işleme</span><span class="sxs-lookup"><span data-stu-id="1da4f-202">Message handling</span></span>
<span data-ttu-id="1da4f-203">Daha önce belirtildiği gibi iletiler geldiğinde IOT Hub'ından **IoTHubClient** kitaplığı yanıt kayıtlı geri çağırma işlevini çağırarak.</span><span class="sxs-lookup"><span data-stu-id="1da4f-203">As stated previously, when messages arrive from IoT Hub the **IoTHubClient** library responds by invoking a registered callback function.</span></span> <span data-ttu-id="1da4f-204">Bazı ek açıklama hak bu işlevin dönüş parametresi yok.</span><span class="sxs-lookup"><span data-stu-id="1da4f-204">There is a return parameter of this function that deserves some additional explanation.</span></span> <span data-ttu-id="1da4f-205">Geri çağırma işlevi bir alıntı işte **ıothub\_istemci\_örnek\_http** örnek uygulama:</span><span class="sxs-lookup"><span data-stu-id="1da4f-205">Here’s an excerpt of the callback function in the **iothub\_client\_sample\_http** sample application:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="1da4f-206">Dönüş türü olduğuna dikkat edin **IOTHUBMESSAGE\_değerlendirme\_sonuç** ve bu belirli durumda döndürürüz **IOTHUBMESSAGE\_kabul edilen**.</span><span class="sxs-lookup"><span data-stu-id="1da4f-206">Note that the return type is **IOTHUBMESSAGE\_DISPOSITION\_RESULT** and in this particular case we return **IOTHUBMESSAGE\_ACCEPTED**.</span></span> <span data-ttu-id="1da4f-207">Değiştirme Biz bu işlevden dönebilirsiniz diğer değerler nasıl **IoTHubClient** kitaplığı tepki verdiğini için ileti geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="1da4f-207">There are other values we can return from this function that change how the **IoTHubClient** library reacts to the message callback.</span></span> <span data-ttu-id="1da4f-208">Seçenekler aşağıda belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-208">Here are the options.</span></span>

* <span data-ttu-id="1da4f-209">**IOTHUBMESSAGE\_kabul edilen** – iletiyi başarıyla işledi.</span><span class="sxs-lookup"><span data-stu-id="1da4f-209">**IOTHUBMESSAGE\_ACCEPTED** – The message has been processed successfully.</span></span> <span data-ttu-id="1da4f-210">**IoTHubClient** kitaplığı değil aynı ileti yeniden ile geri çağırma işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-210">The **IoTHubClient** library will not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="1da4f-211">**IOTHUBMESSAGE\_reddedildi** – ileti işlenmedi ve gelecekte bunun için hiçbir desire yoktur.</span><span class="sxs-lookup"><span data-stu-id="1da4f-211">**IOTHUBMESSAGE\_REJECTED** – The message was not processed and there is no desire to do so in the future.</span></span> <span data-ttu-id="1da4f-212">**IoTHubClient** kitaplığı çağrılamadı aynı ileti yeniden ile geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="1da4f-212">The **IoTHubClient** library should not invoke the callback function again with the same message.</span></span>
* <span data-ttu-id="1da4f-213">**IOTHUBMESSAGE\_ABANDONED** – ileti başarıyla işlenmedi ancak **IoTHubClient** kitaplığı aynı ileti yeniden ile geri çağırma işlevi çağırma.</span><span class="sxs-lookup"><span data-stu-id="1da4f-213">**IOTHUBMESSAGE\_ABANDONED** – The message was not processed successfully, but the **IoTHubClient** library should invoke the callback function again with the same message.</span></span>

<span data-ttu-id="1da4f-214">İlk iki dönüş kodları, için **IoTHubClient** kitaplığı ileti gönderir IOT Hub'ına ileti aygıt sıradan silinir ve gerekir yeniden teslim edilmedi olduğunu gösteren.</span><span class="sxs-lookup"><span data-stu-id="1da4f-214">For the first two return codes, the **IoTHubClient** library sends a message to IoT Hub indicating that the message should be deleted from the device queue and not delivered again.</span></span> <span data-ttu-id="1da4f-215">Net etkisi (ileti aygıt sıradan silinir) aynıdır, ancak ileti kabul edilen veya reddedilen hala kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-215">The net effect is the same (the message is deleted from the device queue), but whether the message was accepted or rejected is still recorded.</span></span>  <span data-ttu-id="1da4f-216">Bu ayrım kaydı geri bildirim için dinleyen ve bir cihaz kabul ettiğini veya belirli bir ileti reddedildi varsa öğrenmek Gönderenler iletinin için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-216">Recording this distinction is useful to senders of the message who can listen for feedback and find out if a device has accepted or rejected a particular message.</span></span>

<span data-ttu-id="1da4f-217">Son durumda bir ileti da IOT Hub'ına gönderilir, ancak ileti yeniden teslim olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-217">In the last case a message is also sent to IoT Hub, but it indicates that the message should be redelivered.</span></span> <span data-ttu-id="1da4f-218">Genellikle bazı hatayla karşılaşırsanız, ancak iletiyi yeniden işlemek denemek istiyorsanız bir ileti abandon.</span><span class="sxs-lookup"><span data-stu-id="1da4f-218">Typically you’ll abandon a message if you encounter some error but want to try to process the message again.</span></span> <span data-ttu-id="1da4f-219">Buna karşılık, bir ileti reddetme kurtarılamaz bir hatayla karşılaştığında (veya yalnızca iletiyi işlemek istemediğinize karar verirseniz) uygundur.</span><span class="sxs-lookup"><span data-stu-id="1da4f-219">In contrast, rejecting a message is appropriate when you encounter an unrecoverable error (or if you simply decide you don’t want to process the message).</span></span>

<span data-ttu-id="1da4f-220">Böylece, istediğiniz davranışı tasarlanmalıdır herhangi bir durumda, farklı dönüş kodları unutmayın **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="1da4f-220">In any case, be aware of the different return codes so that you can elicit the behavior you want from the **IoTHubClient** library.</span></span>

## <a name="alternate-device-credentials"></a><span data-ttu-id="1da4f-221">Alternatif aygıt kimlik bilgisi</span><span class="sxs-lookup"><span data-stu-id="1da4f-221">Alternate device credentials</span></span>
<span data-ttu-id="1da4f-222">İle çalışırken yapılacak ilk şey daha önce açıklandığı gibi **IoTHubClient** kitaplığıdır elde etmek için bir **IOTHUB\_istemci\_İŞLEMEK** aşağıdaki gibi bir çağrıyla:</span><span class="sxs-lookup"><span data-stu-id="1da4f-222">As explained previously, the first thing to do when working with the **IoTHubClient** library is to obtain a **IOTHUB\_CLIENT\_HANDLE** with a call such as the following:</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="1da4f-223">Bağımsız değişkenleri **IoTHubClient\_CreateFromConnectionString** cihaz bağlantı dizesini ve IOT Hub ile iletişim kurmak için kullandığımız protokolü belirten bir parametre.</span><span class="sxs-lookup"><span data-stu-id="1da4f-223">The arguments to **IoTHubClient\_CreateFromConnectionString** are the device connection string and a parameter that indicates the protocol we use to communicate with IoT Hub.</span></span> <span data-ttu-id="1da4f-224">Cihaz bağlantı dizesi şu şekilde görünen bir biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="1da4f-224">The device connection string has a format that appears as follows:</span></span>

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

<span data-ttu-id="1da4f-225">Bu dize bilgilerinde dört adet vardır: IOT hub'ı adı, IOT hub'ı soneki, cihaz kimliği ve paylaşılan erişim anahtarı.</span><span class="sxs-lookup"><span data-stu-id="1da4f-225">There are four pieces of information in this string: IoT Hub name, IoT Hub suffix, device ID, and shared access key.</span></span> <span data-ttu-id="1da4f-226">Azure portalında, IOT hub örneği oluşturduğunuzda IOT hub'ı tam etki alanı adı (FQDN) elde — Bu, IOT hub adını (FQDN ilk parçası) ve IOT hub soneki (FQDN rest) sunar.</span><span class="sxs-lookup"><span data-stu-id="1da4f-226">You obtain the fully qualified domain name (FQDN) of an IoT hub when you create your IoT hub instance in the Azure portal — this gives you the IoT hub name (the first part of the FQDN) and the IoT hub suffix (the rest of the FQDN).</span></span> <span data-ttu-id="1da4f-227">IOT Hub ile Cihazınızı kaydederken cihaz kimliği ve paylaşılan erişim anahtarı almanız (açıklandığı gibi [önceki makalede](iot-hub-device-sdk-c-intro.md)).</span><span class="sxs-lookup"><span data-stu-id="1da4f-227">You get the device ID and the shared access key when you register your device with IoT Hub (as described in the [previous article](iot-hub-device-sdk-c-intro.md)).</span></span>

<span data-ttu-id="1da4f-228">**IoTHubClient\_CreateFromConnectionString** kitaplığı başlatmak için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="1da4f-228">**IoTHubClient\_CreateFromConnectionString** gives you one way to initialize the library.</span></span> <span data-ttu-id="1da4f-229">İsterseniz, yeni bir oluşturabileceğiniz **IOTHUB\_istemci\_İŞLEMEK** cihaz bağlantı dizesi yerine bu tek tek parametreleri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="1da4f-229">If you prefer, you can create a new **IOTHUB\_CLIENT\_HANDLE** by using these individual parameters rather than the device connection string.</span></span> <span data-ttu-id="1da4f-230">Bu, aşağıdaki kod ile sağlanır:</span><span class="sxs-lookup"><span data-stu-id="1da4f-230">This is achieved with the following code:</span></span>

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

<span data-ttu-id="1da4f-231">Bu aynı gerçekleştirir **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="1da4f-231">This accomplishes the same thing as **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="1da4f-232">Kullanmak istediğiniz belirgin görünebilir **IoTHubClient\_CreateFromConnectionString** başlatma daha ayrıntılı bu yöntem yerine.</span><span class="sxs-lookup"><span data-stu-id="1da4f-232">It may seem obvious that you would want to use **IoTHubClient\_CreateFromConnectionString** rather than this more verbose method of initialization.</span></span> <span data-ttu-id="1da4f-233">IOT Hub ' bir aygıtı kaydederken bir cihaz kimliği ve aygıt anahtarı (olmayan bir bağlantı dizesi) aldığınızdır olduğunu, ancak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="1da4f-233">Keep in mind, however, that when you register a device in IoT Hub what you get is a device ID and device key (not a connection string).</span></span> <span data-ttu-id="1da4f-234">*Aygıt explorer* SDK Aracı kullanıma sunulan [önceki makalede](iot-hub-device-sdk-c-intro.md) kitaplıklarında kullanan **Azure IOT hizmeti SDK'sını** aygıt Kimliğinden cihaz bağlantı dizesi oluşturmak için , aygıt anahtarı ve IOT Hub ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="1da4f-234">The *device explorer* SDK tool introduced in the [previous article](iot-hub-device-sdk-c-intro.md) uses libraries in the **Azure IoT service SDK** to create the device connection string from the device ID, device key, and IoT Hub host name.</span></span> <span data-ttu-id="1da4f-235">Bu nedenle çağırma **IoTHubClient\_ÜM\_oluşturma** bir bağlantı dizesi oluşturma adım ortadan kaldırdığı için tercih olabilir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-235">So calling **IoTHubClient\_LL\_Create** may be preferable because it saves you the step of generating a connection string.</span></span> <span data-ttu-id="1da4f-236">Hangi yöntemi uygundur kullanın.</span><span class="sxs-lookup"><span data-stu-id="1da4f-236">Use whichever method is convenient.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="1da4f-237">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="1da4f-237">Configuration options</span></span>
<span data-ttu-id="1da4f-238">Şimdiye kadar her şeyi şekilde anlatılan **IoTHubClient** kitaplığı works varsayılan davranışını yansıtır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-238">So far everything described about the way the **IoTHubClient** library works reflects its default behavior.</span></span> <span data-ttu-id="1da4f-239">Ancak, kitaplık çalışma şeklini değiştirmek için ayarlayabileceğiniz birkaç seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-239">However, there are a few options that you can set to change how the library works.</span></span> <span data-ttu-id="1da4f-240">Bu yararlanarak gerçekleştirilir **IoTHubClient\_ÜM\_SetOption** API.</span><span class="sxs-lookup"><span data-stu-id="1da4f-240">This is accomplished by leveraging the **IoTHubClient\_LL\_SetOption** API.</span></span> <span data-ttu-id="1da4f-241">Bu örneği göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="1da4f-241">Consider this example:</span></span>

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

<span data-ttu-id="1da4f-242">Birkaç yaygın olarak kullanılan seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1da4f-242">There are a couple of options that are commonly used:</span></span>

* <span data-ttu-id="1da4f-243">**SetBatching** (Boole) – varsa **doğru**, sonra da IOT Hub'ına gönderilen verileri toplu olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-243">**SetBatching** (bool) – If **true**, then data sent to IoT Hub is sent in batches.</span></span> <span data-ttu-id="1da4f-244">Varsa **yanlış**, ayrı ayrı gönderilen iletileri sonra.</span><span class="sxs-lookup"><span data-stu-id="1da4f-244">If **false**, then messages are sent individually.</span></span> <span data-ttu-id="1da4f-245">Varsayılan değer **false**.</span><span class="sxs-lookup"><span data-stu-id="1da4f-245">The default is **false**.</span></span> <span data-ttu-id="1da4f-246">Unutmayın **SetBatching** seçeneği yalnızca MQTT veya AMQP protokollerini değil de, HTTP protokolü için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-246">Note that the **SetBatching** option only applies to the HTTP protocol and not to the MQTT or AMQP protocols.</span></span>
* <span data-ttu-id="1da4f-247">**Zaman aşımı** (imzasız int) – bu değer milisaniye cinsinden gösterilir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-247">**Timeout** (unsigned int) – This value is represented in milliseconds.</span></span> <span data-ttu-id="1da4f-248">Bir HTTP isteğinin ya da bir yanıt alırken bu süreden daha uzun sürer gönderme, ardından bağlantı zaman aşımına uğradı.</span><span class="sxs-lookup"><span data-stu-id="1da4f-248">If sending an HTTP request or receiving a response takes longer than this time, then the connection times out.</span></span>

<span data-ttu-id="1da4f-249">Toplu işleme seçeneği önemlidir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-249">The batching option is important.</span></span> <span data-ttu-id="1da4f-250">Varsayılan olarak, kitaplık ingresses olayları ayrı ayrı (tek bir olay için ne olursa olsun, geçirdiğiniz olan **IoTHubClient\_ÜM\_SendEventAsync**).</span><span class="sxs-lookup"><span data-stu-id="1da4f-250">By default, the library ingresses events individually (a single event is whatever you pass to **IoTHubClient\_LL\_SendEventAsync**).</span></span> <span data-ttu-id="1da4f-251">Toplu işleme seçeneği ise **doğru**, kitaplık (kadar IOT hub'ı kabul edeceği maksimum ileti boyutu) arabellekteki mümkün olduğunca çok olaylarını toplar.</span><span class="sxs-lookup"><span data-stu-id="1da4f-251">If the batching option is **true**, the library collects as many events as it can from the buffer (up to the maximum message size that IoT Hub will accept).</span></span>  <span data-ttu-id="1da4f-252">Olay toplu IOT Hub'ına (olayları tek tek bir JSON dizisine paketlenmiştir) tek bir HTTP çağrısıyla gönderilir.</span><span class="sxs-lookup"><span data-stu-id="1da4f-252">The event batch is sent to IoT Hub in a single HTTP call (the individual events are bundled into a JSON array).</span></span> <span data-ttu-id="1da4f-253">Ağ gidiş dönüş azaltma bu yana genellikle toplu etkinleştirme büyük performans artışları sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-253">Enabling batching typically results in big performance gains since you’re reducing network round-trips.</span></span> <span data-ttu-id="1da4f-254">Tek bir olay toplu ile HTTP üstbilgi kümesi yerine tek tek her olay için üstbilgi kümesi gönderme beri bant genişliği de önemli ölçüde azaltır.</span><span class="sxs-lookup"><span data-stu-id="1da4f-254">It also significantly reduces bandwidth since you are sending one set of HTTP headers with an event batch rather than a set of headers for each individual event.</span></span> <span data-ttu-id="1da4f-255">Genellikle, aksi takdirde yapmak için özel bir nedeniniz yoksa, toplu etkinleştirme istersiniz.</span><span class="sxs-lookup"><span data-stu-id="1da4f-255">Unless you have a specific reason to do otherwise, typically you’ll want to enable batching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1da4f-256">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1da4f-256">Next steps</span></span>
<span data-ttu-id="1da4f-257">Bu makalede davranışını ayrıntılı olarak **IoTHubClient** kitaplığı bulunan **C için Azure IOT cihaz SDK'sı**. Bu bilgiyle özelliklerini iyi anlamış olmanız **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="1da4f-257">This article describes in detail the behavior of the **IoTHubClient** library found in the **Azure IoT device SDK for C**. With this information, you should have a good understanding of the capabilities of the **IoTHubClient** library.</span></span> <span data-ttu-id="1da4f-258">[Sonraki makalede](iot-hub-device-sdk-c-serializer.md) benzer ayrıntı sağlar **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="1da4f-258">The [next article](iot-hub-device-sdk-c-serializer.md) provides similar detail on the **serializer** library.</span></span>

<span data-ttu-id="1da4f-259">IOT Hub için geliştirme hakkında daha fazla bilgi için bkz: [Azure IOT SDK'ları][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="1da4f-259">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="1da4f-260">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="1da4f-260">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="1da4f-261">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="1da4f-261">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
