---
title: "c - IoTHubClient aaaAzure IOT cihaz SDK'sı | Microsoft Docs"
description: "Nasıl toouse hello IoTHubClient C toocreate cihaz uygulamaları için hello Azure IOT cihaz SDK'sı kitaplıkta, bir IOT hub ile iletişim kurar."
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
ms.openlocfilehash: d1ece79e9ba6d1e5fd45cabb8fca393b24052e07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a><span data-ttu-id="5a13b-103">C – IoTHubClient hakkında daha fazla bilgi için Azure IOT cihaz SDK'sı</span><span class="sxs-lookup"><span data-stu-id="5a13b-103">Azure IoT device SDK for C – more about IoTHubClient</span></span>
<span data-ttu-id="5a13b-104">Merhaba [ilk makale](iot-hub-device-sdk-c-intro.md) bu sunulan serisi hello içinde **C için Azure IOT cihaz SDK'sı**. Bu makale, SDK içinde iki Mimari katman vardır açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-104">hello [first article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C**. That article explained that there are two architectural layers in SDK.</span></span> <span data-ttu-id="5a13b-105">Merhaba Hello temel olan **IoTHubClient** doğrudan IOT Hub ile iletişim yöneten kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="5a13b-105">At hello base is hello **IoTHubClient** library which directly manages communication with IoT Hub.</span></span> <span data-ttu-id="5a13b-106">Ayrıca hello olan **seri hale getirici** tooprovide seri hale getirme hizmetleri üzerinde üst o derlemeler kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="5a13b-106">There's also hello **serializer** library that builds on top of that tooprovide serialization services.</span></span> <span data-ttu-id="5a13b-107">Bu makalede ek ayrıntı üzerinde hello sağlarız **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="5a13b-107">In this article we'll provide additional detail on hello **IoTHubClient** library.</span></span>

<span data-ttu-id="5a13b-108">Merhaba önceki makalede açıklanan nasıl toouse hello **IoTHubClient** kitaplığı toosend olayları tooIoT Hub ve iletileri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a13b-108">hello previous article described how toouse hello **IoTHubClient** library toosend events tooIoT Hub and receive messages.</span></span> <span data-ttu-id="5a13b-109">Bu makalede bu tartışma nasıl toomore tam olarak yönetmek açıklayarak genişletir *zaman* toohello Tanıtımı veri gönderip **düşük düzeyli API'leri**.</span><span class="sxs-lookup"><span data-stu-id="5a13b-109">This article extends that discussion by explaining how toomore precisely manage *when* you send and receive data, introducing you toohello **lower-level APIs**.</span></span> <span data-ttu-id="5a13b-110">Ayrıca açıklayacağız nasıl tooattach özellikleri tooevents (ve gelen iletileri almak) hello özelliklerinde işleme hello özelliğini kullanarak **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="5a13b-110">We'll also explain how tooattach properties tooevents (and retrieve them from messages) using hello property handling features in hello **IoTHubClient** library.</span></span> <span data-ttu-id="5a13b-111">Son olarak, farklı şekillerde toohandle ek açıklaması sağlarız IOT Hub'ından alınan iletileri.</span><span class="sxs-lookup"><span data-stu-id="5a13b-111">Finally, we'll provide additional explanation of different ways toohandle messages received from IoT Hub.</span></span>

<span data-ttu-id="5a13b-112">Merhaba makale birkaç cihaz kimlik bilgileri hakkında daha fazla bilgi ve nasıl toochange hello hello davranışını dahil olmak üzere çeşitli konuları kapsayan sonucuna **IoTHubClient** yapılandırma seçenekleri üzerinden.</span><span class="sxs-lookup"><span data-stu-id="5a13b-112">hello article concludes by covering a couple of miscellaneous topics, including more about device credentials and how toochange hello behavior of hello **IoTHubClient** through configuration options.</span></span>

<span data-ttu-id="5a13b-113">Merhaba kullanacağız **IoTHubClient** SDK Bu konularda tooexplain örnekleri.</span><span class="sxs-lookup"><span data-stu-id="5a13b-113">We'll use hello **IoTHubClient** SDK samples tooexplain these topics.</span></span> <span data-ttu-id="5a13b-114">Merhaba toofollow boyunca istiyorsanız bkz **ıothub\_istemci\_örnek\_http** ve **ıothub\_istemci\_örnek\_amqp** C. hello aşağıdaki bölümlerde açıklanan her şey bu örnekleri gösterilmiştir için hello Azure IOT cihaz SDK'sı bulunan uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="5a13b-114">If you want toofollow along, see hello **iothub\_client\_sample\_http** and **iothub\_client\_sample\_amqp** applications that are included in hello Azure IoT device SDK for C. Everything described in hello following sections is demonstrated in these samples.</span></span>

<span data-ttu-id="5a13b-115">Merhaba bulabilirsiniz [ **C için Azure IOT cihaz SDK'sı** ](https://github.com/Azure/azure-iot-sdk-c) GitHub depo ve görünüm ayrıntılarını hello hello API [C API Başvurusu](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="5a13b-115">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="hello-lower-level-apis"></a><span data-ttu-id="5a13b-116">Merhaba düşük düzeyli API'leri</span><span class="sxs-lookup"><span data-stu-id="5a13b-116">hello lower-level APIs</span></span>
<span data-ttu-id="5a13b-117">Merhaba önceki makalede açıklanan hello temel hello işleyişi **IotHubClient** hello Merhaba içeriğine içinde **ıothub\_istemci\_örnek\_amqp** uygulama.</span><span class="sxs-lookup"><span data-stu-id="5a13b-117">hello previous article described hello basic operation of hello **IotHubClient** within hello context of hello **iothub\_client\_sample\_amqp** application.</span></span> <span data-ttu-id="5a13b-118">Örneğin, nasıl tooinitialize hello bu kodu kullanarak kitaplığı açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-118">For example, it explained how tooinitialize hello library using this code.</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="5a13b-119">Ayrıca, bu kullanarak toosend olayları nasıl işlev çağrısı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-119">It also described how toosend events using this function call.</span></span>

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

<span data-ttu-id="5a13b-120">Merhaba makale, bir geri çağırma işlevini kaydederek tooreceive nasıl iletileri de açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-120">hello article also described how tooreceive messages by registering a callback function.</span></span>

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

<span data-ttu-id="5a13b-121">Merhaba makale ayrıca nasıl kullanarak toofree kaynakları hello aşağıdaki gibi kod gösterdi.</span><span class="sxs-lookup"><span data-stu-id="5a13b-121">hello article also showed how toofree resources using code such as hello following.</span></span>

```
IoTHubClient_Destroy(iotHubClientHandle);
```

<span data-ttu-id="5a13b-122">Ancak bu API'lerden yardımcı işlevleri tooeach vardır:</span><span class="sxs-lookup"><span data-stu-id="5a13b-122">However there are companion functions tooeach of these APIs:</span></span>

* <span data-ttu-id="5a13b-123">IoTHubClient\_ÜM\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="5a13b-123">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="5a13b-124">IoTHubClient\_ÜM\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="5a13b-124">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="5a13b-125">IoTHubClient\_ÜM\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="5a13b-125">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="5a13b-126">IoTHubClient\_ÜM\_yok</span><span class="sxs-lookup"><span data-stu-id="5a13b-126">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="5a13b-127">Tüm bu işlevler "Tümü" Merhaba API adına dahil et.</span><span class="sxs-lookup"><span data-stu-id="5a13b-127">These functions all include “LL” in hello API name.</span></span> <span data-ttu-id="5a13b-128">Dışında bu işlevlerin her biri hello parametrelerinin aynı tootheir ÜM olmayan ortaklarınıza olan.</span><span class="sxs-lookup"><span data-stu-id="5a13b-128">Other than that, hello parameters of each of these functions are identical tootheir non-LL counterparts.</span></span> <span data-ttu-id="5a13b-129">Ancak, bu işlevler hello davranışını önemli bir şekilde farklıdır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-129">However, hello behavior of these functions is different in one important way.</span></span>

<span data-ttu-id="5a13b-130">Çağırdığınızda **IoTHubClient\_CreateFromConnectionString**, hello temel kitaplıkları hello arka planda çalışan yeni bir iş parçacığı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-130">When you call **IoTHubClient\_CreateFromConnectionString**, hello underlying libraries create a new thread that runs in hello background.</span></span> <span data-ttu-id="5a13b-131">Bu iş parçacığı olayları gönderir ve IOT Hub'ından, iletileri alır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-131">This thread sends events to, and receives messages from, IoT Hub.</span></span> <span data-ttu-id="5a13b-132">Bu tür bir iş parçacığı hello "Tümü" API'leri ile çalışırken oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="5a13b-132">No such thread is created when working with hello "LL" APIs.</span></span> <span data-ttu-id="5a13b-133">Merhaba arka plan iş parçacığı Hello oluşturulmasını kolaylık toohello geliştiricisi değildir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-133">hello creation of hello background thread is a convenience toohello developer.</span></span> <span data-ttu-id="5a13b-134">Açıkça olayları ileti gönderme ve IOT Hub'ından--hello arka planda otomatik olarak gerçekleşir alma hakkında tooworry yok.</span><span class="sxs-lookup"><span data-stu-id="5a13b-134">You don’t have tooworry about explicitly sending events and receiving messages from IoT Hub -- it happens automatically in hello background.</span></span> <span data-ttu-id="5a13b-135">Buna karşılık, hello "Tümü" API'leri size IOT Hub ile iletişim açık denetime ihtiyacınız varsa.</span><span class="sxs-lookup"><span data-stu-id="5a13b-135">In contrast, hello "LL" APIs give you explicit control over communication with IoT Hub, if you need it.</span></span>

<span data-ttu-id="5a13b-136">toounderstand bu daha iyi bir örneğe bakalım:</span><span class="sxs-lookup"><span data-stu-id="5a13b-136">toounderstand this better, let’s look at an example:</span></span>

<span data-ttu-id="5a13b-137">Çağırdığınızda **IoTHubClient\_SendEventAsync**, ne gerçekte yaptığınız hello olay arabellekte koyuyor.</span><span class="sxs-lookup"><span data-stu-id="5a13b-137">When you call **IoTHubClient\_SendEventAsync**, what you're actually doing is putting hello event in a buffer.</span></span> <span data-ttu-id="5a13b-138">Merhaba çağırdığınızda oluşturulan arka plan iş parçacığı **IoTHubClient\_CreateFromConnectionString** sürekli olarak bu arabellek izler ve herhangi bir veri gönderir tooIoT Hub içerir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-138">hello background thread created when you call **IoTHubClient\_CreateFromConnectionString** continually monitors this buffer and sends any data that it contains tooIoT Hub.</span></span> <span data-ttu-id="5a13b-139">Hello adresindeki hello arka planda bu hello aynı zaman böyle ana iş parçacığının başka işler gerçekleştirme.</span><span class="sxs-lookup"><span data-stu-id="5a13b-139">This happens in hello background at hello same time that hello main thread is performing other work.</span></span>

<span data-ttu-id="5a13b-140">Benzer şekilde, bir geri çağırma işlevini kullanarak iletileri için kaydettiğinizde **IoTHubClient\_SetMessageCallback**, hello SDK toohave hello arka plan sunuculardaki gerektiğini belirten bir ileti olduğunda iş parçacığı çağırma hello geri çağırma işlevi alınan, hello ana iş parçacığı bağımsızdır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-140">Similarly, when you register a callback function for messages using **IoTHubClient\_SetMessageCallback**, you're instructing hello SDK toohave hello background thread invoke hello callback function when a message is received, independent of hello main thread.</span></span>

<span data-ttu-id="5a13b-141">Merhaba "Tümü" API'leri arka plan iş parçacığı oluştur.</span><span class="sxs-lookup"><span data-stu-id="5a13b-141">hello "LL" APIs don’t create a background thread.</span></span> <span data-ttu-id="5a13b-142">Bunun yerine, yeni bir API tooexplicitly gönderme çağrılmalıdır ve IOT Hub'ından veri alırsınız.</span><span class="sxs-lookup"><span data-stu-id="5a13b-142">Instead, a new API must be called tooexplicitly send and receive data from IoT Hub.</span></span> <span data-ttu-id="5a13b-143">Bu örnekte aşağıdaki hello gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-143">This is demonstrated in hello following example.</span></span>

<span data-ttu-id="5a13b-144">Merhaba **ıothub\_istemci\_örnek\_http** SDK gösteren hello dahil uygulama hello düşük düzeyli API'leri.</span><span class="sxs-lookup"><span data-stu-id="5a13b-144">hello **iothub\_client\_sample\_http** application that’s included in hello SDK demonstrates hello lower-level APIs.</span></span> <span data-ttu-id="5a13b-145">Bu örnekte, hello aşağıdaki gibi kod ile olayları tooIoT Hub gönder:</span><span class="sxs-lookup"><span data-stu-id="5a13b-145">In that sample, we send events tooIoT Hub with code such as hello following:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="5a13b-146">Merhaba ilk üç satırını hello iletisi oluşturun ve hello son satırında hello olay gönderir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-146">hello first three lines create hello message, and hello last line sends hello event.</span></span> <span data-ttu-id="5a13b-147">Ancak, daha önce belirtildiği gibi "Merhaba veriler yalnızca bir arabellek yerleştirilir hello olay anlamına gelir gönderme".</span><span class="sxs-lookup"><span data-stu-id="5a13b-147">However, as mentioned previously, "sending" hello event means that hello data is simply placed in a buffer.</span></span> <span data-ttu-id="5a13b-148">Biz çağırdığınızda hiçbir şey hello ağ üzerinde aktarılan **IoTHubClient\_ÜM\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="5a13b-148">Nothing is transmitted on hello network when we call **IoTHubClient\_LL\_SendEventAsync**.</span></span> <span data-ttu-id="5a13b-149">Sipariş tooactually giriş hello veri tooIoT içinde Hub, çağırmalısınız **IoTHubClient\_ÜM\_DoWork**, bu örnekteki gibi:</span><span class="sxs-lookup"><span data-stu-id="5a13b-149">In order tooactually ingress hello data tooIoT Hub, you must call **IoTHubClient\_LL\_DoWork**, as in this example:</span></span>

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="5a13b-150">Bu kod (Merhaba gelen **ıothub\_istemci\_örnek\_http** uygulama) art arda çağırır **IoTHubClient\_ÜM\_DoWork** .</span><span class="sxs-lookup"><span data-stu-id="5a13b-150">This code (from hello **iothub\_client\_sample\_http** application) repeatedly calls **IoTHubClient\_LL\_DoWork**.</span></span> <span data-ttu-id="5a13b-151">Her zaman **IoTHubClient\_ÜM\_DoWork** olan çağrılır, hello arabellek tooIoT Hub bazı olayların gönderir ve toohello aygıt gönderilen sıraya alınmış bir iletiyi alır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-151">Each time **IoTHubClient\_LL\_DoWork** is called, it sends some events from hello buffer tooIoT Hub and it retrieves a queued message being sent toohello device.</span></span> <span data-ttu-id="5a13b-152">Biz iletiler için bir geri çağırma işlevini kaydolduysanız hello geri çağırma (herhangi bir ileti kuyruğa varsayılarak) çağrıldıktan sonra hello ikinci durumda anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-152">hello latter case means that if we registered a callback function for messages, then hello callback is invoked (assuming any messages are queued up).</span></span> <span data-ttu-id="5a13b-153">Biz bu tür bir geri çağırma işlevi hello aşağıdaki gibi kod ile kayıtlı:</span><span class="sxs-lookup"><span data-stu-id="5a13b-153">We would have registered such a callback function with code such as hello following:</span></span>

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

<span data-ttu-id="5a13b-154">Hello neden **IoTHubClient\_ÜM\_DoWork** genellikle adlandırılır bir döngü değil, her kez çağırıldığında, gönderir *bazı* arabelleğe alınmış olayları tooIoT Hub ve alır *hello sonraki* iletisi sıraya hello aygıt için.</span><span class="sxs-lookup"><span data-stu-id="5a13b-154">hello reason that **IoTHubClient\_LL\_DoWork** is often called in a loop is that each time it’s called, it sends *some* buffered events tooIoT Hub and retrieves *hello next* message queued up for hello device.</span></span> <span data-ttu-id="5a13b-155">Her çağrı toosend tüm arabelleğe alınmış olayları garantisi yoktur veya tooretrieve tüm kuyruğa alınan iletileri.</span><span class="sxs-lookup"><span data-stu-id="5a13b-155">Each call isn’t guaranteed toosend all buffered events or tooretrieve all queued messages.</span></span> <span data-ttu-id="5a13b-156">Tüm olaylar hello arabellek ve ardından başka bir işlem devam toosend istiyorsanız hello aşağıdaki gibi kod ile bu döngü değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5a13b-156">If you want toosend all events in hello buffer and then continue on with other processing you can replace this loop with code such as hello following:</span></span>

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

<span data-ttu-id="5a13b-157">Bu kod çağırır **IoTHubClient\_ÜM\_DoWork** hello arabelleği tüm olayları tooIoT Hub gönderilen kadar.</span><span class="sxs-lookup"><span data-stu-id="5a13b-157">This code calls **IoTHubClient\_LL\_DoWork** until all events in hello buffer have been sent tooIoT Hub.</span></span> <span data-ttu-id="5a13b-158">Bu ayrıca tüm sıraya alınan iletileri alınmış olan anlamına gelmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5a13b-158">Note this does not also imply that all queued messages have been received.</span></span> <span data-ttu-id="5a13b-159">Bunun nedeni hello parçası "tümü" iletileri denetleme gibi belirleyici bir eylem olmadığından emin olur.</span><span class="sxs-lookup"><span data-stu-id="5a13b-159">Part of hello reason for this is that checking for "all" messages isn’t as deterministic an action.</span></span> <span data-ttu-id="5a13b-160">"Tüm" Merhaba iletileri almak, ancak başka bir toohello aygıt gönderilir ne olur hemen sonra?</span><span class="sxs-lookup"><span data-stu-id="5a13b-160">What happens if you retrieve "all" of hello messages, but then another one is sent toohello device immediately after?</span></span> <span data-ttu-id="5a13b-161">Daha iyi bir şekilde toodeal, ile programlı bir zaman aşımı ile olur.</span><span class="sxs-lookup"><span data-stu-id="5a13b-161">A better way toodeal with that is with a programmed timeout.</span></span> <span data-ttu-id="5a13b-162">Örneğin, çağrılması her zaman hello ileti geri çağırma işlevi bir süreölçer sıfırlanamadı.</span><span class="sxs-lookup"><span data-stu-id="5a13b-162">For example, hello message callback function could reset a timer every time it’s invoked.</span></span> <span data-ttu-id="5a13b-163">Örneğin, hiçbir hello en son alınan ileti yok, ardından mantığı toocontinue işleme yazabilirsiniz *X* saniye.</span><span class="sxs-lookup"><span data-stu-id="5a13b-163">You can then write logic toocontinue processing if, for example, no messages have been received in hello last *X* seconds.</span></span>

<span data-ttu-id="5a13b-164">Ne zaman tamamlanmış ingressing olayları olduğunuz ve iletilerini alma emin toocall hello karşılık gelen işlevi tooclean kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-164">When you’re finished ingressing events and receiving messages, be sure toocall hello corresponding function tooclean up resources.</span></span>

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

<span data-ttu-id="5a13b-165">Temel olarak yalnızca bir dizi API toosend yoktur ve arka plan iş parçacığı ve başka bir dizi hello arka plan iş parçacığı olmadan aynı şeyi hello API ile verilerini alma.</span><span class="sxs-lookup"><span data-stu-id="5a13b-165">Basically there’s only one set of APIs toosend and receive data with a background thread and another set of APIs that does hello same thing without hello background thread.</span></span> <span data-ttu-id="5a13b-166">Geliştiricilerin çok hello olmayan - ÜM API'leri tercih edebilirsiniz, ancak hello Geliştirici ağ aktarımları üzerinde açık denetim istediğinde hello düşük düzeyli API'leri yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-166">A lot of developers may prefer hello non-LL APIs, but hello lower-level APIs are useful when hello developer wants explicit control over network transmissions.</span></span> <span data-ttu-id="5a13b-167">Örneğin, bazı aygıtlar veri zaman ve yalnızca giriş olayları belirtilen aralıklarla (örneğin, saatte bir kez veya günde bir kez) toplar.</span><span class="sxs-lookup"><span data-stu-id="5a13b-167">For example, some devices collect data over time and only ingress events at specified intervals (for example, once an hour or once a day).</span></span> <span data-ttu-id="5a13b-168">Merhaba IOT Hub'ından veri gönderip alırken özelliği tooexplicitly denetim hello alt düzey API'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a13b-168">hello lower-level APIs give you hello ability tooexplicitly control when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="5a13b-169">Başkalarının yalnızca hello Basitlik alt düzey API'ler sağlar, hello tercih eder.</span><span class="sxs-lookup"><span data-stu-id="5a13b-169">Others will simply prefer hello simplicity that hello lower-level APIs provide.</span></span> <span data-ttu-id="5a13b-170">Bazı iş oluşmasını hello arka planda yerine hello ana iş parçacığı her şeyi olur.</span><span class="sxs-lookup"><span data-stu-id="5a13b-170">Everything happens on hello main thread rather than some work happening in hello background.</span></span>

<span data-ttu-id="5a13b-171">Seçtiğiniz hangi modeli olması emin toobe tutarlı hangi API'leri kullanın.</span><span class="sxs-lookup"><span data-stu-id="5a13b-171">Whichever model you choose, be sure toobe consistent in which APIs you use.</span></span> <span data-ttu-id="5a13b-172">Çağırarak başlatırsanız **IoTHubClient\_ÜM\_CreateFromConnectionString**, herhangi bir izleme iş için alt düzey API'leri karşılık gelen hello yalnızca kullandığınızdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="5a13b-172">If you start by calling **IoTHubClient\_LL\_CreateFromConnectionString**, be sure you only use hello corresponding lower-level APIs for any follow-up work:</span></span>

* <span data-ttu-id="5a13b-173">IoTHubClient\_ÜM\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="5a13b-173">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="5a13b-174">IoTHubClient\_ÜM\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="5a13b-174">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="5a13b-175">IoTHubClient\_ÜM\_yok</span><span class="sxs-lookup"><span data-stu-id="5a13b-175">IoTHubClient\_LL\_Destroy</span></span>
* <span data-ttu-id="5a13b-176">IoTHubClient\_ÜM\_DoWork</span><span class="sxs-lookup"><span data-stu-id="5a13b-176">IoTHubClient\_LL\_DoWork</span></span>

<span data-ttu-id="5a13b-177">Merhaba ters de geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-177">hello opposite is true as well.</span></span> <span data-ttu-id="5a13b-178">İle başlatırsanız, **IoTHubClient\_CreateFromConnectionString**, kullanım hello sonra ÜM olmayan API'ler herhangi bir ek işlem için.</span><span class="sxs-lookup"><span data-stu-id="5a13b-178">If you start with **IoTHubClient\_CreateFromConnectionString**, then use hello non-LL APIs for any additional processing.</span></span>

<span data-ttu-id="5a13b-179">Merhaba Hello Azure IOT cihazı SDK C için bkz: **ıothub\_istemci\_örnek\_http** uygulama hello tam bir örnek için alt düzey API'leri.</span><span class="sxs-lookup"><span data-stu-id="5a13b-179">In hello Azure IoT device SDK for C, see hello **iothub\_client\_sample\_http** application for a complete example of hello lower-level APIs.</span></span> <span data-ttu-id="5a13b-180">Merhaba **ıothub\_istemci\_örnek\_amqp** uygulama tam bir örnek için hello olmayan - ÜM API'leri başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-180">hello **iothub\_client\_sample\_amqp** application can be referenced for a full example of hello non-LL APIs.</span></span>

## <a name="property-handling"></a><span data-ttu-id="5a13b-181">Özellik işleme</span><span class="sxs-lookup"><span data-stu-id="5a13b-181">Property handling</span></span>
<span data-ttu-id="5a13b-182">Verileri gönderilirken açıklanan zaman kadarki biz toohello hello ileti gövdesi başvuran.</span><span class="sxs-lookup"><span data-stu-id="5a13b-182">So far when we've described sending data, we've been referring toohello body of hello message.</span></span> <span data-ttu-id="5a13b-183">Örneğin, bu kod göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="5a13b-183">For example, consider this code:</span></span>

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

<span data-ttu-id="5a13b-184">Bu örnekte, "Hello World." Merhaba metinle ileti tooIoT Hub gönderilir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-184">This example sends a message tooIoT Hub with hello text "Hello World."</span></span> <span data-ttu-id="5a13b-185">Ancak, IOT Hub ayrıca özellikleri toobe ekli tooeach ileti imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-185">However, IoT Hub also allows properties toobe attached tooeach message.</span></span> <span data-ttu-id="5a13b-186">Ekli toohello ileti olabilir ad/değer çiftleri özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-186">Properties are name/value pairs that can be attached toohello message.</span></span> <span data-ttu-id="5a13b-187">Örneğin, biz hello önceki kod tooattach özellik toohello iletisi değiştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5a13b-187">For example, we can modify hello previous code tooattach a property toohello message:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="5a13b-188">Arayarak Başlat **IoTHubMessage\_özellikleri** ve onu bizim ileti hello tanıtıcısı.</span><span class="sxs-lookup"><span data-stu-id="5a13b-188">We start by calling **IoTHubMessage\_Properties** and passing it hello handle of our message.</span></span> <span data-ttu-id="5a13b-189">Ne biz geri alırsınız bir **harita\_İŞLEMEK** bize Özellikler ekleme toostart etkinleştirir başvuru.</span><span class="sxs-lookup"><span data-stu-id="5a13b-189">What we get back is a **MAP\_HANDLE** reference that enables us toostart adding properties.</span></span> <span data-ttu-id="5a13b-190">Merhaba ikinci çağırarak gerçekleştirilir **harita\_örnek**, başvuru tooa harita aldığı\_TANITICISI, hello özellik adı ve Başlangıç özellik değeri.</span><span class="sxs-lookup"><span data-stu-id="5a13b-190">hello latter is accomplished by calling **Map\_AddOrUpdate**, which takes a reference tooa MAP\_HANDLE, hello property name, and hello property value.</span></span> <span data-ttu-id="5a13b-191">Bu API ile biz istediğiniz sayıda özellik ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="5a13b-191">With this API we can add as many properties as we like.</span></span>

<span data-ttu-id="5a13b-192">Ne zaman hello olay okunur gelen **olay hub'ları**, hello alıcı hello özellikler numaralandırılmaya ve bunlara karşılık gelen değerler alır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-192">When hello event is read from **Event Hubs**, hello receiver can enumerate hello properties and retrieve their corresponding values.</span></span> <span data-ttu-id="5a13b-193">Örneğin, .NET içinde bu hello erişerek gerçekleştirilmesi [hello EventData nesne üzerindeki özellikleri koleksiyonu](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span><span class="sxs-lookup"><span data-stu-id="5a13b-193">For example, in .NET this would be accomplished by accessing hello [Properties collection on hello EventData object](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).</span></span>

<span data-ttu-id="5a13b-194">Merhaba önceki örnekte, biz özellikleri tooan olayı biz tooIoT Hub Gönder ekleniyor.</span><span class="sxs-lookup"><span data-stu-id="5a13b-194">In hello previous example, we’re attaching properties tooan event that we send tooIoT Hub.</span></span> <span data-ttu-id="5a13b-195">Özellikler, IOT Hub'ından alınan ekli toomessages de olabilir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-195">Properties can also be attached toomessages received from IoT Hub.</span></span> <span data-ttu-id="5a13b-196">Bir ileti tooretrieve özelliklerinden istiyoruz, hello aşağıdaki gibi kod bizim ileti geri çağırma işlevini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5a13b-196">If we want tooretrieve properties from a message, we can use code such as hello following in our message callback function:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .

    // Retrieve properties from hello message
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

<span data-ttu-id="5a13b-197">Çağrı çok hello**IoTHubMessage\_özellikleri** döndürür hello **harita\_İŞLEMEK** başvuru.</span><span class="sxs-lookup"><span data-stu-id="5a13b-197">hello call too**IoTHubMessage\_Properties** returns hello **MAP\_HANDLE** reference.</span></span> <span data-ttu-id="5a13b-198">Biz daha sonra bu başvuruyu çok geçirin**harita\_GetInternals** tooobtain başvuru tooan dizisi hello ad/değer çiftleri (bir sayım hello özelliklerinin yanı sıra).</span><span class="sxs-lookup"><span data-stu-id="5a13b-198">We then pass that reference too**Map\_GetInternals** tooobtain a reference tooan array of hello name/value pairs (as well as a count of hello properties).</span></span> <span data-ttu-id="5a13b-199">Bu noktada hello özellikleri tooget toohello değerleri istiyoruz numaralandırma, atmaktan değil.</span><span class="sxs-lookup"><span data-stu-id="5a13b-199">At that point it's a simple matter of enumerating hello properties tooget toohello values we want.</span></span>

<span data-ttu-id="5a13b-200">Uygulamanızda toouse özellikleri yok.</span><span class="sxs-lookup"><span data-stu-id="5a13b-200">You don't have toouse properties in your application.</span></span> <span data-ttu-id="5a13b-201">Ancak, tooset ihtiyacınız varsa bunları olaylarına veya bunları gelen iletileri, hello almak **IoTHubClient** kitaplığı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-201">However, if you need tooset them on events or retrieve them from messages, hello **IoTHubClient** library makes it easy.</span></span>

## <a name="message-handling"></a><span data-ttu-id="5a13b-202">İleti işleme</span><span class="sxs-lookup"><span data-stu-id="5a13b-202">Message handling</span></span>
<span data-ttu-id="5a13b-203">Daha önce belirtildiği gibi iletiler geldiğinde IOT hub'ı hello **IoTHubClient** kitaplığı yanıt kayıtlı geri çağırma işlevini çağırarak.</span><span class="sxs-lookup"><span data-stu-id="5a13b-203">As stated previously, when messages arrive from IoT Hub hello **IoTHubClient** library responds by invoking a registered callback function.</span></span> <span data-ttu-id="5a13b-204">Bazı ek açıklama hak bu işlevin dönüş parametresi yok.</span><span class="sxs-lookup"><span data-stu-id="5a13b-204">There is a return parameter of this function that deserves some additional explanation.</span></span> <span data-ttu-id="5a13b-205">Merhaba hello geri çağırma işlevinin bir alıntı işte **ıothub\_istemci\_örnek\_http** örnek uygulama:</span><span class="sxs-lookup"><span data-stu-id="5a13b-205">Here’s an excerpt of hello callback function in hello **iothub\_client\_sample\_http** sample application:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

<span data-ttu-id="5a13b-206">Merhaba dönüş türü olduğuna dikkat edin **IOTHUBMESSAGE\_değerlendirme\_sonuç** ve bu belirli durumda döndürürüz **IOTHUBMESSAGE\_kabul edilen**.</span><span class="sxs-lookup"><span data-stu-id="5a13b-206">Note that hello return type is **IOTHUBMESSAGE\_DISPOSITION\_RESULT** and in this particular case we return **IOTHUBMESSAGE\_ACCEPTED**.</span></span> <span data-ttu-id="5a13b-207">Biz dönebilirsiniz bu işlevden değişiklik nasıl hello diğer değerler **IoTHubClient** kitaplığı tepki verdiğini toohello ileti geri çağırma.</span><span class="sxs-lookup"><span data-stu-id="5a13b-207">There are other values we can return from this function that change how hello **IoTHubClient** library reacts toohello message callback.</span></span> <span data-ttu-id="5a13b-208">Merhaba seçenekler aşağıda belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-208">Here are hello options.</span></span>

* <span data-ttu-id="5a13b-209">**IOTHUBMESSAGE\_kabul edilen** – selamlama iletisine başarıyla işlendiğinden.</span><span class="sxs-lookup"><span data-stu-id="5a13b-209">**IOTHUBMESSAGE\_ACCEPTED** – hello message has been processed successfully.</span></span> <span data-ttu-id="5a13b-210">Merhaba **IoTHubClient** kitaplığı değil hello'yla yeniden hello geri çağırma işlevi çağırma aynı ileti.</span><span class="sxs-lookup"><span data-stu-id="5a13b-210">hello **IoTHubClient** library will not invoke hello callback function again with hello same message.</span></span>
* <span data-ttu-id="5a13b-211">**IOTHUBMESSAGE\_reddedildi** – selamlama iletisine değil işlendiği ve yoktur hiçbir desire toodo bu nedenle de hello gelecekteki.</span><span class="sxs-lookup"><span data-stu-id="5a13b-211">**IOTHUBMESSAGE\_REJECTED** – hello message was not processed and there is no desire toodo so in hello future.</span></span> <span data-ttu-id="5a13b-212">Merhaba **IoTHubClient** kitaplığı çağrılamadı hello geri çağırma işlevi yeniden hello ile aynı ileti.</span><span class="sxs-lookup"><span data-stu-id="5a13b-212">hello **IoTHubClient** library should not invoke hello callback function again with hello same message.</span></span>
* <span data-ttu-id="5a13b-213">**IOTHUBMESSAGE\_ABANDONED** – selamlama iletisine değil işlendiği başarıyla ancak hello **IoTHubClient** kitaplığı hello'yla yeniden hello geri çağırma işlevi çağırma aynı ileti.</span><span class="sxs-lookup"><span data-stu-id="5a13b-213">**IOTHUBMESSAGE\_ABANDONED** – hello message was not processed successfully, but hello **IoTHubClient** library should invoke hello callback function again with hello same message.</span></span>

<span data-ttu-id="5a13b-214">Merhaba ilk iki, hello dönüş kodları **IoTHubClient** kitaplığı hello ileti belirten Hub hello aygıt sıradan silinir ve gerekir yeniden teslim edilmedi ileti tooIoT gönderir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-214">For hello first two return codes, hello **IoTHubClient** library sends a message tooIoT Hub indicating that hello message should be deleted from hello device queue and not delivered again.</span></span> <span data-ttu-id="5a13b-215">Merhaba net etkisi aynı hello olduğu (selamlama iletisine hello aygıt sıradan silinir), ancak selamlama iletisine kabul edilen veya reddedilen hala kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-215">hello net effect is hello same (hello message is deleted from hello device queue), but whether hello message was accepted or rejected is still recorded.</span></span>  <span data-ttu-id="5a13b-216">Bu ayrım kaydı geri bildirim için dinleyen ve bir cihaz kabul ettiğini veya belirli bir ileti reddedildi varsa öğrenmek yararlı toosenders hello iletisinin olur.</span><span class="sxs-lookup"><span data-stu-id="5a13b-216">Recording this distinction is useful toosenders of hello message who can listen for feedback and find out if a device has accepted or rejected a particular message.</span></span>

<span data-ttu-id="5a13b-217">Merhaba son durumda tooIoT Hub ayrıca bir ileti gönderilir, ancak bu hello ileti yeniden teslim edilebilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-217">In hello last case a message is also sent tooIoT Hub, but it indicates that hello message should be redelivered.</span></span> <span data-ttu-id="5a13b-218">Genellikle bazı hatayla karşılaşırsanız, ancak tootry tooprocess ileti yeniden hello isterseniz bir ileti abandon.</span><span class="sxs-lookup"><span data-stu-id="5a13b-218">Typically you’ll abandon a message if you encounter some error but want tootry tooprocess hello message again.</span></span> <span data-ttu-id="5a13b-219">Buna karşılık, bir ileti reddetme kurtarılamaz bir hatayla karşılaştığında (veya yalnızca tooprocess selamlama iletisine istemediğinize karar verirseniz) uygundur.</span><span class="sxs-lookup"><span data-stu-id="5a13b-219">In contrast, rejecting a message is appropriate when you encounter an unrecoverable error (or if you simply decide you don’t want tooprocess hello message).</span></span>

<span data-ttu-id="5a13b-220">Böylece hello istediğiniz hello davranışı tasarlanmalıdır herhangi bir durumda, hello farklı dönüş kodları unutmayın **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="5a13b-220">In any case, be aware of hello different return codes so that you can elicit hello behavior you want from hello **IoTHubClient** library.</span></span>

## <a name="alternate-device-credentials"></a><span data-ttu-id="5a13b-221">Alternatif aygıt kimlik bilgisi</span><span class="sxs-lookup"><span data-stu-id="5a13b-221">Alternate device credentials</span></span>
<span data-ttu-id="5a13b-222">Daha önce açıklandığı gibi ilk şey toodo hello ile çalışırken hello **IoTHubClient** kitaplığıdır tooobtain bir **IOTHUB\_istemci\_İŞLEMEK** hello gibi bir çağrıyla Aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="5a13b-222">As explained previously, hello first thing toodo when working with hello **IoTHubClient** library is tooobtain a **IOTHUB\_CLIENT\_HANDLE** with a call such as hello following:</span></span>

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

<span data-ttu-id="5a13b-223">bağımsız değişkenler çok hello**IoTHubClient\_CreateFromConnectionString** hello cihaz bağlantı dizesini ve kullanırız toocommunicate IOT Hub ile Merhaba protokolü belirten bir parametre.</span><span class="sxs-lookup"><span data-stu-id="5a13b-223">hello arguments too**IoTHubClient\_CreateFromConnectionString** are hello device connection string and a parameter that indicates hello protocol we use toocommunicate with IoT Hub.</span></span> <span data-ttu-id="5a13b-224">Merhaba cihaz bağlantı dizesi şu şekilde görünen bir biçime sahiptir:</span><span class="sxs-lookup"><span data-stu-id="5a13b-224">hello device connection string has a format that appears as follows:</span></span>

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

<span data-ttu-id="5a13b-225">Bu dize bilgilerinde dört adet vardır: IOT hub'ı adı, IOT hub'ı soneki, cihaz kimliği ve paylaşılan erişim anahtarı.</span><span class="sxs-lookup"><span data-stu-id="5a13b-225">There are four pieces of information in this string: IoT Hub name, IoT Hub suffix, device ID, and shared access key.</span></span> <span data-ttu-id="5a13b-226">Hello Azure portal, IOT hub örneği oluşturduğunuzda, IOT hub'ı hello tam etki alanı adı (FQDN) elde — Bu, hello IOT hub adını (FQDN hello hello ilk bölümü) ve hello IOT hub soneki (Merhaba FQDN kalanı hello) sunar.</span><span class="sxs-lookup"><span data-stu-id="5a13b-226">You obtain hello fully qualified domain name (FQDN) of an IoT hub when you create your IoT hub instance in hello Azure portal — this gives you hello IoT hub name (hello first part of hello FQDN) and hello IoT hub suffix (hello rest of hello FQDN).</span></span> <span data-ttu-id="5a13b-227">IOT Hub ile Cihazınızı kaydederken hello cihaz kimliği ve hello paylaşılan erişim anahtarı almanız (hello açıklandığı gibi [önceki makalede](iot-hub-device-sdk-c-intro.md)).</span><span class="sxs-lookup"><span data-stu-id="5a13b-227">You get hello device ID and hello shared access key when you register your device with IoT Hub (as described in hello [previous article](iot-hub-device-sdk-c-intro.md)).</span></span>

<span data-ttu-id="5a13b-228">**IoTHubClient\_CreateFromConnectionString** tek yönlü tooinitialize hello kitaplığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a13b-228">**IoTHubClient\_CreateFromConnectionString** gives you one way tooinitialize hello library.</span></span> <span data-ttu-id="5a13b-229">İsterseniz, yeni bir oluşturabileceğiniz **IOTHUB\_istemci\_İŞLEMEK** hello cihaz bağlantı dizesi yerine bu tek tek parametreleri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="5a13b-229">If you prefer, you can create a new **IOTHUB\_CLIENT\_HANDLE** by using these individual parameters rather than hello device connection string.</span></span> <span data-ttu-id="5a13b-230">Bu kod aşağıdaki hello ile sağlanır:</span><span class="sxs-lookup"><span data-stu-id="5a13b-230">This is achieved with hello following code:</span></span>

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

<span data-ttu-id="5a13b-231">Bunu hello gerçekleştirir aynı **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="5a13b-231">This accomplishes hello same thing as **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="5a13b-232">Toouse istersiniz belirgin görünebilir **IoTHubClient\_CreateFromConnectionString** başlatma daha ayrıntılı bu yöntem yerine.</span><span class="sxs-lookup"><span data-stu-id="5a13b-232">It may seem obvious that you would want toouse **IoTHubClient\_CreateFromConnectionString** rather than this more verbose method of initialization.</span></span> <span data-ttu-id="5a13b-233">IOT Hub ' bir aygıtı kaydederken bir cihaz kimliği ve aygıt anahtarı (olmayan bir bağlantı dizesi) aldığınızdır olduğunu, ancak unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5a13b-233">Keep in mind, however, that when you register a device in IoT Hub what you get is a device ID and device key (not a connection string).</span></span> <span data-ttu-id="5a13b-234">Merhaba *aygıt explorer* hello sunulan SDK aracı [önceki makalede](iot-hub-device-sdk-c-intro.md) hello kitaplıklarında kullanır **Azure IOT hizmeti SDK'sını** toocreate hello cihaz bağlantı dizesinden Merhaba cihaz kimliği, aygıt anahtarı ve IOT Hub ana bilgisayar adı.</span><span class="sxs-lookup"><span data-stu-id="5a13b-234">hello *device explorer* SDK tool introduced in hello [previous article](iot-hub-device-sdk-c-intro.md) uses libraries in hello **Azure IoT service SDK** toocreate hello device connection string from hello device ID, device key, and IoT Hub host name.</span></span> <span data-ttu-id="5a13b-235">Bu nedenle çağırma **IoTHubClient\_ÜM\_oluşturma** , kaydettiğinden tercih olabilir hello adım bir bağlantı dizesi oluşturma.</span><span class="sxs-lookup"><span data-stu-id="5a13b-235">So calling **IoTHubClient\_LL\_Create** may be preferable because it saves you hello step of generating a connection string.</span></span> <span data-ttu-id="5a13b-236">Hangi yöntemi uygundur kullanın.</span><span class="sxs-lookup"><span data-stu-id="5a13b-236">Use whichever method is convenient.</span></span>

## <a name="configuration-options"></a><span data-ttu-id="5a13b-237">Yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="5a13b-237">Configuration options</span></span>
<span data-ttu-id="5a13b-238">Şimdiye kadar her şeyi hello şekilde hello hakkında anlatılan **IoTHubClient** kitaplığı works varsayılan davranışını yansıtır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-238">So far everything described about hello way hello **IoTHubClient** library works reflects its default behavior.</span></span> <span data-ttu-id="5a13b-239">Ancak, hello kitaplığı nasıl çalıştığını toochange ayarlayabileceğiniz birkaç seçenek vardır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-239">However, there are a few options that you can set toochange how hello library works.</span></span> <span data-ttu-id="5a13b-240">Bu hello yararlanarak gerçekleştirilir **IoTHubClient\_ÜM\_SetOption** API.</span><span class="sxs-lookup"><span data-stu-id="5a13b-240">This is accomplished by leveraging hello **IoTHubClient\_LL\_SetOption** API.</span></span> <span data-ttu-id="5a13b-241">Bu örneği göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="5a13b-241">Consider this example:</span></span>

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

<span data-ttu-id="5a13b-242">Birkaç yaygın olarak kullanılan seçenekler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5a13b-242">There are a couple of options that are commonly used:</span></span>

* <span data-ttu-id="5a13b-243">**SetBatching** (Boole) – varsa **doğru**, sonra gönderilen veriler tooIoT Hub toplu olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-243">**SetBatching** (bool) – If **true**, then data sent tooIoT Hub is sent in batches.</span></span> <span data-ttu-id="5a13b-244">Varsa **yanlış**, ayrı ayrı gönderilen iletileri sonra.</span><span class="sxs-lookup"><span data-stu-id="5a13b-244">If **false**, then messages are sent individually.</span></span> <span data-ttu-id="5a13b-245">Merhaba varsayılandır **false**.</span><span class="sxs-lookup"><span data-stu-id="5a13b-245">hello default is **false**.</span></span> <span data-ttu-id="5a13b-246">Bu hello Not **SetBatching** seçeneği yalnızca toohello HTTP protokolü ve değil toohello MQTT veya AMQP protokollerini uygulanır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-246">Note that hello **SetBatching** option only applies toohello HTTP protocol and not toohello MQTT or AMQP protocols.</span></span>
* <span data-ttu-id="5a13b-247">**Zaman aşımı** (imzasız int) – bu değer milisaniye cinsinden gösterilir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-247">**Timeout** (unsigned int) – This value is represented in milliseconds.</span></span> <span data-ttu-id="5a13b-248">Bir HTTP isteğinin ya da bir yanıt alırken bu süreden daha uzun sürer gönderme, ardından hello bağlantı zaman aşımına uğradı.</span><span class="sxs-lookup"><span data-stu-id="5a13b-248">If sending an HTTP request or receiving a response takes longer than this time, then hello connection times out.</span></span>

<span data-ttu-id="5a13b-249">seçenek toplu işleme hello önemlidir.</span><span class="sxs-lookup"><span data-stu-id="5a13b-249">hello batching option is important.</span></span> <span data-ttu-id="5a13b-250">Varsayılan olarak, kitaplık ingresses olayları ayrı ayrı hello (tek bir olay ne olursa olsun çok geçirdiğiniz olan**IoTHubClient\_ÜM\_SendEventAsync**).</span><span class="sxs-lookup"><span data-stu-id="5a13b-250">By default, hello library ingresses events individually (a single event is whatever you pass too**IoTHubClient\_LL\_SendEventAsync**).</span></span> <span data-ttu-id="5a13b-251">Seçenek toplu işleme hello ise **doğru**, hello kitaplığı hello arabellek (yukarı, IOT hub'ı kabul toohello maksimum ileti boyutu) gelen mümkün olduğunca çok olayları toplar.</span><span class="sxs-lookup"><span data-stu-id="5a13b-251">If hello batching option is **true**, hello library collects as many events as it can from hello buffer (up toohello maximum message size that IoT Hub will accept).</span></span>  <span data-ttu-id="5a13b-252">Merhaba olay toplu tooIoT Hub tek bir gönderilen HTTP çağrısıyla (Merhaba olayları tek tek paketlenmiş bir JSON dizisine).</span><span class="sxs-lookup"><span data-stu-id="5a13b-252">hello event batch is sent tooIoT Hub in a single HTTP call (hello individual events are bundled into a JSON array).</span></span> <span data-ttu-id="5a13b-253">Ağ gidiş dönüş azaltma bu yana genellikle toplu etkinleştirme büyük performans artışları sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-253">Enabling batching typically results in big performance gains since you’re reducing network round-trips.</span></span> <span data-ttu-id="5a13b-254">Tek bir olay toplu ile HTTP üstbilgi kümesi yerine tek tek her olay için üstbilgi kümesi gönderme beri bant genişliği de önemli ölçüde azaltır.</span><span class="sxs-lookup"><span data-stu-id="5a13b-254">It also significantly reduces bandwidth since you are sending one set of HTTP headers with an event batch rather than a set of headers for each individual event.</span></span> <span data-ttu-id="5a13b-255">Tipik olarak belirli bir nedenle toodo Aksi durumda olmadığı sürece tooenable toplu işleme isteyeceksiniz.</span><span class="sxs-lookup"><span data-stu-id="5a13b-255">Unless you have a specific reason toodo otherwise, typically you’ll want tooenable batching.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a13b-256">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5a13b-256">Next steps</span></span>
<span data-ttu-id="5a13b-257">Bu makalede ayrıntı hello davranışını hello içinde **IoTHubClient** kitaplığı bulunan hello **C için Azure IOT cihaz SDK'sı**. Bu bilgiyle hello hello özelliklerini iyi anlamış olmanız **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="5a13b-257">This article describes in detail hello behavior of hello **IoTHubClient** library found in hello **Azure IoT device SDK for C**. With this information, you should have a good understanding of hello capabilities of hello **IoTHubClient** library.</span></span> <span data-ttu-id="5a13b-258">Merhaba [sonraki makalede](iot-hub-device-sdk-c-serializer.md) hello üzerinde benzer ayrıntı sağlar **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="5a13b-258">hello [next article](iot-hub-device-sdk-c-serializer.md) provides similar detail on hello **serializer** library.</span></span>

<span data-ttu-id="5a13b-259">IOT hub'ı geliştirme hakkında daha fazla toolearn bkz hello [Azure IOT SDK'ları][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="5a13b-259">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="5a13b-260">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="5a13b-260">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="5a13b-261">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="5a13b-261">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
