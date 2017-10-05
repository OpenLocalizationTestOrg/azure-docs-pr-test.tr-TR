---
title: "Azure IOT cihaz SDK'sı c - seri hale getirici | Microsoft Docs"
description: "Azure IOT cihaz SDK'sı C için seri hale getirici kitaplıkta bir IOT hub ile iletişim cihaz uygulamaları oluşturmak için nasıl kullanılacağını."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: defbed34-de73-429c-8592-cd863a38e4dd
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/06/2016
ms.author: obloch
ms.openlocfilehash: aa03c29c54d75538b1fdf987cac5f09d5d344f73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="04865-103">Azure IOT cihaz SDK'sı için C – seri hale getirici hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="04865-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="04865-104">[İlk makale](iot-hub-device-sdk-c-intro.md) sunulan bu serideki **C için Azure IOT cihaz SDK'sı**. Daha ayrıntılı bir açıklaması sonraki makalede sağlanan [ **IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="04865-104">The [first article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C**. The next article provided a more detailed description of the [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="04865-105">Bu makalede daha ayrıntılı bir açıklama kalan bileşeninin sağlayarak SDK'ın kapsamı tamamlar: **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="04865-105">This article completes coverage of the SDK by providing a more detailed description of the remaining component: the **serializer** library.</span></span>

<span data-ttu-id="04865-106">Giriş makalesi nasıl kullanılacağını açıklanan **seri hale getirici** olayları göndermek ve IOT Hub'ından iletileri almak için kitaplık.</span><span class="sxs-lookup"><span data-stu-id="04865-106">The introductory article described how to use the **serializer** library to send events to and receive messages from IoT Hub.</span></span> <span data-ttu-id="04865-107">Bu makalede, biz bu tartışma verilerinizle modellemek nasıl daha eksiksiz bir açıklaması sağlayarak genişletmek **seri hale getirici** makro dili.</span><span class="sxs-lookup"><span data-stu-id="04865-107">In this article, we extend that discussion by providing a more complete explanation of how to model your data with the **serializer** macro language.</span></span> <span data-ttu-id="04865-108">Makale ayrıca nasıl kitaplığı iletileri serileştiren hakkında daha fazla ayrıntı içerir (ve bazı durumlarda serileştirme davranışı nasıl kontrol edebilir).</span><span class="sxs-lookup"><span data-stu-id="04865-108">The article also includes more detail about how the library serializes messages (and in some cases how you can control the serialization behavior).</span></span> <span data-ttu-id="04865-109">Biz de oluşturduğunuz modelleri boyutunu belirleyen değiştirebileceğiniz bazı parametreleri açıklayan.</span><span class="sxs-lookup"><span data-stu-id="04865-109">We'll also describe some parameters you can modify that determine the size of the models you create.</span></span>

<span data-ttu-id="04865-110">Son olarak, makaleyi ileti ve özellik işleme gibi önceki makalelerinde kapsanan bazı konular revisits.</span><span class="sxs-lookup"><span data-stu-id="04865-110">Finally, the article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="04865-111">Biz bulma, bu özellikler iş aynı şekilde kullanarak **seri hale getirici** kitaplığı ile göründükleri **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="04865-111">As we'll find out, those features work in the same way using the **serializer** library as they do with the **IoTHubClient** library.</span></span>

<span data-ttu-id="04865-112">Bu makalede açıklanan her şeyi dayanır **seri hale getirici** SDK örnekleri.</span><span class="sxs-lookup"><span data-stu-id="04865-112">Everything described in this article is based on the **serializer** SDK samples.</span></span> <span data-ttu-id="04865-113">İzlemek istiyorsanız, bkz: **simplesample\_amqp** ve **simplesample\_http** c için Azure IOT cihaz SDK'sı eklenmiş olan uygulamalar</span><span class="sxs-lookup"><span data-stu-id="04865-113">If you want to follow along, see the **simplesample\_amqp** and **simplesample\_http** applications included in the Azure IoT device SDK for C.</span></span>

<span data-ttu-id="04865-114">Bulabileceğiniz [ **C için Azure IOT cihaz SDK'sı** ](https://github.com/Azure/azure-iot-sdk-c) GitHub depo ve görünüm ayrıntılarını API [C API Başvurusu](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="04865-114">You can find the [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of the API in the [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="the-modeling-language"></a><span data-ttu-id="04865-115">Modelleme Dili</span><span class="sxs-lookup"><span data-stu-id="04865-115">The modeling language</span></span>
<span data-ttu-id="04865-116">[Giriş makalesi](iot-hub-device-sdk-c-intro.md) sunulan bu serideki **C için Azure IOT cihaz SDK'sı** sağlanan örnek aracılığıyla dil modelleme **simplesample\_amqp** uygulama:</span><span class="sxs-lookup"><span data-stu-id="04865-116">The [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced the **Azure IoT device SDK for C** modeling language through the example provided in the **simplesample\_amqp** application:</span></span>

```
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(double, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

<span data-ttu-id="04865-117">Gördüğünüz gibi modelleme dil C makroları temel alır.</span><span class="sxs-lookup"><span data-stu-id="04865-117">As you can see, the modeling language is based on C macros.</span></span> <span data-ttu-id="04865-118">Her zaman tanımınız ile başlayan **başlangıç\_ad alanı** ve her zaman bittiğini **son\_ad alanı**.</span><span class="sxs-lookup"><span data-stu-id="04865-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="04865-119">Şirketinizde veya bu örnekte, üzerinde çalıştığınız proje olduğu gibi ad alanı adı için yaygın bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="04865-119">It's common to name the namespace for your company or, as in this example, the project that you're working on.</span></span>

<span data-ttu-id="04865-120">Ad alanı içinde unsurları olan model tanımları.</span><span class="sxs-lookup"><span data-stu-id="04865-120">What goes inside the namespace are model definitions.</span></span> <span data-ttu-id="04865-121">Bu durumda, tek bir model için bir anemometer yoktur.</span><span class="sxs-lookup"><span data-stu-id="04865-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="04865-122">Bir kez daha, model bir şey adlandırılabilir, ancak bu aygıt veya IOT Hub ile değiştirmek istediğiniz veri türü için tipik olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="04865-122">Once again, the model can be named anything, but typically this is named for the device or type of data you want to exchange with IoT Hub.</span></span>  

<span data-ttu-id="04865-123">Modelleri içeren bir tanımı olaylarını IOT Hub'ına giriş olabilir ( *veri*) IOT Hub'ından alabilir iletileri yanı sıra ( *Eylemler*).</span><span class="sxs-lookup"><span data-stu-id="04865-123">Models contain a definition of the events you can ingress to IoT Hub (the *data*) as well as the messages you can receive from IoT Hub (the *actions*).</span></span> <span data-ttu-id="04865-124">Örnekte görebildiğiniz gibi olayları bir türü ve bir ada sahip; Eylemler, bir ad ve isteğe bağlı parametreler (her bir türüyle) sahip.</span><span class="sxs-lookup"><span data-stu-id="04865-124">As you can see from the example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="04865-125">SDK'sı tarafından desteklenen ek veri türleri olan ne Bu örnekte gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="04865-125">What’s not demonstrated in this sample are additional data types that are supported by the SDK.</span></span> <span data-ttu-id="04865-126">Biz bu sonraki ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="04865-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="04865-127">IOT hub'ı, bir cihazın gönderdiği olarak veri başvurduğu *olayları*olarak Modelleme Dili başvurduğu yaparken *veri* (kullanılarak tanımlanan **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="04865-127">IoT Hub refers to the data a device sends to it as *events*, while the modeling language refers to it as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="04865-128">Benzer şekilde, IOT hub'ı veri Gönder aygıtlara başvurduğu *iletileri*olarak Modelleme Dili başvurduğu yaparken *Eylemler* (kullanılarak tanımlanan **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="04865-128">Likewise, IoT Hub refers to the data you send to devices as *messages*, while the modeling language refers to it as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="04865-129">Bu makalede birbirinin yerine kullanılabilir bu koşulları unutmayın.</span><span class="sxs-lookup"><span data-stu-id="04865-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="04865-130">Desteklenen veri türleri</span><span class="sxs-lookup"><span data-stu-id="04865-130">Supported data types</span></span>
<span data-ttu-id="04865-131">Aşağıdaki veri türleri ile oluşturulan modellerinde desteklenir **seri hale getirici** kitaplığı:</span><span class="sxs-lookup"><span data-stu-id="04865-131">The following data types are supported in models created with the **serializer** library:</span></span>

| <span data-ttu-id="04865-132">Tür</span><span class="sxs-lookup"><span data-stu-id="04865-132">Type</span></span> | <span data-ttu-id="04865-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="04865-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04865-134">Çift</span><span class="sxs-lookup"><span data-stu-id="04865-134">double</span></span> |<span data-ttu-id="04865-135">çift duyarlıklı kayan nokta sayısı</span><span class="sxs-lookup"><span data-stu-id="04865-135">double precision floating point number</span></span> |
| <span data-ttu-id="04865-136">Int</span><span class="sxs-lookup"><span data-stu-id="04865-136">int</span></span> |<span data-ttu-id="04865-137">32 bit tamsayı</span><span class="sxs-lookup"><span data-stu-id="04865-137">32 bit integer</span></span> |
| <span data-ttu-id="04865-138">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="04865-138">float</span></span> |<span data-ttu-id="04865-139">tek duyarlıklı kayan nokta sayısı</span><span class="sxs-lookup"><span data-stu-id="04865-139">single precision floating point number</span></span> |
| <span data-ttu-id="04865-140">uzun</span><span class="sxs-lookup"><span data-stu-id="04865-140">long</span></span> |<span data-ttu-id="04865-141">uzun tamsayı</span><span class="sxs-lookup"><span data-stu-id="04865-141">long integer</span></span> |
| <span data-ttu-id="04865-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="04865-142">int8\_t</span></span> |<span data-ttu-id="04865-143">8 bit tam sayı</span><span class="sxs-lookup"><span data-stu-id="04865-143">8 bit integer</span></span> |
| <span data-ttu-id="04865-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="04865-144">int16\_t</span></span> |<span data-ttu-id="04865-145">16 bit tam sayı</span><span class="sxs-lookup"><span data-stu-id="04865-145">16 bit integer</span></span> |
| <span data-ttu-id="04865-146">Int32\_t</span><span class="sxs-lookup"><span data-stu-id="04865-146">int32\_t</span></span> |<span data-ttu-id="04865-147">32 bit tamsayı</span><span class="sxs-lookup"><span data-stu-id="04865-147">32 bit integer</span></span> |
| <span data-ttu-id="04865-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="04865-148">int64\_t</span></span> |<span data-ttu-id="04865-149">64 bit tamsayı</span><span class="sxs-lookup"><span data-stu-id="04865-149">64 bit integer</span></span> |
| <span data-ttu-id="04865-150">bool</span><span class="sxs-lookup"><span data-stu-id="04865-150">bool</span></span> |<span data-ttu-id="04865-151">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="04865-151">boolean</span></span> |
| <span data-ttu-id="04865-152">ASCII\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="04865-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="04865-153">ASCII dizesi</span><span class="sxs-lookup"><span data-stu-id="04865-153">ASCII string</span></span> |
| <span data-ttu-id="04865-154">EDM\_TARİH\_ZAMAN\_UZAKLIĞI</span><span class="sxs-lookup"><span data-stu-id="04865-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="04865-155">Tarih Saat farkı</span><span class="sxs-lookup"><span data-stu-id="04865-155">date time offset</span></span> |
| <span data-ttu-id="04865-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="04865-156">EDM\_GUID</span></span> |<span data-ttu-id="04865-157">GUID</span><span class="sxs-lookup"><span data-stu-id="04865-157">GUID</span></span> |
| <span data-ttu-id="04865-158">EDM\_İKİLİ</span><span class="sxs-lookup"><span data-stu-id="04865-158">EDM\_BINARY</span></span> |<span data-ttu-id="04865-159">İkili</span><span class="sxs-lookup"><span data-stu-id="04865-159">binary</span></span> |
| <span data-ttu-id="04865-160">BİLDİRME\_YAPISI</span><span class="sxs-lookup"><span data-stu-id="04865-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="04865-161">karmaşık veri türü</span><span class="sxs-lookup"><span data-stu-id="04865-161">complex data type</span></span> |

<span data-ttu-id="04865-162">Son veri türüyle başlayalım.</span><span class="sxs-lookup"><span data-stu-id="04865-162">Let’s start with the last data type.</span></span> <span data-ttu-id="04865-163">**DECLARE\_YAPISI** gruplandırmaları başka ilkel türleri olan karmaşık veri türlerini tanımlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="04865-163">The **DECLARE\_STRUCT** allows you to define complex data types, which are groupings of the other primitive types.</span></span> <span data-ttu-id="04865-164">Bu gruplandırmalar bize şuna benzer bir modeli tanımlamak izin ver:</span><span class="sxs-lookup"><span data-stu-id="04865-164">These groupings allow us to define a model that looks like this:</span></span>

```
DECLARE_STRUCT(TestType,
double, aDouble,
int, aInt,
float, aFloat,
long, aLong,
int8_t, aInt8,
uint8_t, auInt8,
int16_t, aInt16,
int32_t, aInt32,
int64_t, aInt64,
bool, aBool,
ascii_char_ptr, aAsciiCharPtr,
EDM_DATE_TIME_OFFSET, aDateTimeOffset,
EDM_GUID, aGuid,
EDM_BINARY, aBinary
);

DECLARE_MODEL(TestModel,
WITH_DATA(TestType, Test)
);
```

<span data-ttu-id="04865-165">Bir tek veri olayı türü modelimizi içeriyor **TestType**.</span><span class="sxs-lookup"><span data-stu-id="04865-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="04865-166">**TestType** topluca tarafından desteklenen ilkel türler gösteren birkaç üyeleri içeren karmaşık bir tür **seri hale getirici** model oluşturma dili.</span><span class="sxs-lookup"><span data-stu-id="04865-166">**TestType** is a complex type that includes several members, which collectively demonstrate the primitive types supported by the **serializer** modeling language.</span></span>

<span data-ttu-id="04865-167">Bir modelin bu şekilde size aşağıdaki gibi görünen IOT Hub veri göndermek için kod yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="04865-167">With a model like this, we can write code to send data to IoT Hub that appears as follows:</span></span>

```
TestModel* testModel = CREATE_MODEL_INSTANCE(MyThermostat, TestModel);

testModel->Test.aDouble = 1.1;
testModel->Test.aInt = 2;
testModel->Test.aFloat = 3.0f;
testModel->Test.aLong = 4;
testModel->Test.aInt8 = 5;
testModel->Test.auInt8 = 6;
testModel->Test.aInt16 = 7;
testModel->Test.aInt32 = 8;
testModel->Test.aInt64 = 9;
testModel->Test.aBool = true;
testModel->Test.aAsciiCharPtr = "ascii string 1";

time_t now;
time(&now);
testModel->Test.aDateTimeOffset = GetDateTimeOffset(now);

EDM_GUID guid = { { 0x00, 0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F } };
testModel->Test.aGuid = guid;

unsigned char binaryArray[3] = { 0x01, 0x02, 0x03 };
EDM_BINARY binaryData = { sizeof(binaryArray), &binaryArray };
testModel->Test.aBinary = binaryData;

SendAsync(iotHubClientHandle, (const void*)&(testModel->Test));
```

<span data-ttu-id="04865-168">Temel olarak, size bir değer her üyesine atama **Test** yapısı ve ardından çağırma **SendAsync** göndermek için **Test** buluta veri olayı.</span><span class="sxs-lookup"><span data-stu-id="04865-168">Basically, we’re assigning a value to every member of the **Test** structure and then calling **SendAsync** to send the **Test** data event to the cloud.</span></span> <span data-ttu-id="04865-169">**SendAsync** tek bir veri olayı, IOT Hub'ına gönderir yardımcı işlevdir:</span><span class="sxs-lookup"><span data-stu-id="04865-169">**SendAsync** is a helper function that sends a single data event to IoT Hub:</span></span>

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate the string
        char* destinationAsString = (char*)malloc(destinationSize + 1);
        if (destinationAsString != NULL)
        {
            memcpy(destinationAsString, destination, destinationSize);
            destinationAsString[destinationSize] = '\0';
            IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromString(destinationAsString);
            if (messageHandle != NULL)
            {
                IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)0);

                IoTHubMessage_Destroy(messageHandle);
            }
            free(destinationAsString);
        }
        free(destination);
    }
}
```

<span data-ttu-id="04865-170">Bu işlev, verilen veri olay serileştirir ve IOT kullanarak Hub'ına gönderir **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="04865-170">This function serializes the given data event and sends it to IoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="04865-171">Önceki makalede ele alınan aynı kodu budur (**SendAsync** mantığı kullanışlı bir işlevdeki yalıtır).</span><span class="sxs-lookup"><span data-stu-id="04865-171">This is the same code discussed in previous articles (**SendAsync** encapsulates the logic into a convenient function).</span></span>

<span data-ttu-id="04865-172">Önceki kod içinde kullanılan bir diğer yardımcı işlevdir **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="04865-172">One other helper function used in the previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="04865-173">Bu işlev belirli bir zaman türünde bir değer dönüşümler **EDM\_tarih\_zaman\_UZAKLIĞI**:</span><span class="sxs-lookup"><span data-stu-id="04865-173">This function transforms the given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

```
EDM_DATE_TIME_OFFSET GetDateTimeOffset(time_t time)
{
    struct tm newTime;
    gmtime_s(&newTime, &time);
    EDM_DATE_TIME_OFFSET dateTimeOffset;
    dateTimeOffset.dateTime = newTime;
    dateTimeOffset.fractionalSecond = 0;
    dateTimeOffset.hasFractionalSecond = 0;
    dateTimeOffset.hasTimeZone = 0;
    dateTimeOffset.timeZoneHour = 0;
    dateTimeOffset.timeZoneMinute = 0;
    return dateTimeOffset;
}
```

<span data-ttu-id="04865-174">Bu kodu çalıştırmak, şu iletiyi IOT Hub'ına gönderilir:</span><span class="sxs-lookup"><span data-stu-id="04865-174">If you run this code, the following message is sent to IoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="04865-175">Oluşturulan biçimi JSON seri hale getirme unutmayın tarafından **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="04865-175">Note that the serialization is JSON, which is the format generated by the **serializer** library.</span></span> <span data-ttu-id="04865-176">Ayrıca her üyenin seri hale getirilmiş JSON nesnesinin üyelerini eşleştiğini unutmayın **TestType** biz bizim modelde tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="04865-176">Also note that each member of the serialized JSON object matches the members of the **TestType** that we defined in our model.</span></span> <span data-ttu-id="04865-177">Değerleri de tam olarak kod içinde kullanılan eşleştiğinden.</span><span class="sxs-lookup"><span data-stu-id="04865-177">The values also exactly match those used in the code.</span></span> <span data-ttu-id="04865-178">Ancak, ikili verileri base64 ile kodlanmış olduğuna dikkat edin: "AQID" olan base64 kodlamasını {0x01, 0x02, 0x03}.</span><span class="sxs-lookup"><span data-stu-id="04865-178">However, note that the binary data is base64-encoded: "AQID" is the base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="04865-179">Bu örnek kullanmanın avantajı gösterir **seri hale getirici** kitaplığı--etkinleştirir JSON seri hale getirme uygulamamızdaki açıkça uğraşmanız gerek kalmadan buluta göndermemizi.</span><span class="sxs-lookup"><span data-stu-id="04865-179">This example demonstrates the advantage of using the **serializer** library -- it enables us to send JSON to the cloud, without having to explicitly deal with serialization in our application.</span></span> <span data-ttu-id="04865-180">Tüm hakkında endişelenmeye gerek sahibiz ayarlanması veri olaylarını değerlerini bizim modeli ve buluta olayları göndermek için basit API'ler çağırma.</span><span class="sxs-lookup"><span data-stu-id="04865-180">All we have to worry about is setting the values of the data events in our model and then calling simple APIs to send those events to the cloud.</span></span>

<span data-ttu-id="04865-181">Bu bilgi ile biz desteklenen veri türleri, (sizi bile başka karmaşık türler içindeki karmaşık tür dahil olabilir) karmaşık türleri dahil olmak üzere çeşitli içeren modellerinin tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04865-181">With this information, we can define models that include the range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="04865-182">Ancak, kullanıcı tarafından oluşturulan JSON seri hale getirilmiş yukarıdaki örnekte önemli noktanız getirir.</span><span class="sxs-lookup"><span data-stu-id="04865-182">However, he serialized JSON generated by the example above brings up an important point.</span></span> <span data-ttu-id="04865-183">*Nasıl* size verilerle göndereceğiz **seri hale getirici** kitaplığı belirler tam olarak nasıl JSON biçimi.</span><span class="sxs-lookup"><span data-stu-id="04865-183">*How* we send data with the **serializer** library determines exactly how the JSON is formed.</span></span> <span data-ttu-id="04865-184">Bu belirli ne şu sonraki konulara değineceğiz noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="04865-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="04865-185">Seri hale getirme hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="04865-185">More about serialization</span></span>
<span data-ttu-id="04865-186">Önceki bölümde tarafından oluşturulan çıkış vurgular **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="04865-186">The previous section highlights an example of the output generated by the **serializer** library.</span></span> <span data-ttu-id="04865-187">Bu bölümde, nasıl kitaplığı veri serileştirir ve seri hale getirme API'leri kullanılarak bu davranışı nasıl kontrol edebilir açıklayacağız.</span><span class="sxs-lookup"><span data-stu-id="04865-187">In this section, we'll explain how the library serializes data and how you can control that behavior using the serialization APIs.</span></span>

<span data-ttu-id="04865-188">Seri hale getirme tartışma ilerletmek için biz thermostat üzerinde temel alan yeni bir modeli çalışmak.</span><span class="sxs-lookup"><span data-stu-id="04865-188">In order to advance the discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="04865-189">İlk olarak, şimdi biz adresine çalıştığınız senaryoya bazı arka plan sağlayın.</span><span class="sxs-lookup"><span data-stu-id="04865-189">First, let's provide some background on the scenario we're trying to address.</span></span>

<span data-ttu-id="04865-190">Sıcaklık ve nem ölçer thermostat model istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="04865-190">We want to model a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="04865-191">IOT Hub'ına farklı gönderilmek üzere her veri parçası geçiyor.</span><span class="sxs-lookup"><span data-stu-id="04865-191">Each piece of data is going to be sent to IoT Hub differently.</span></span> <span data-ttu-id="04865-192">Varsayılan olarak, thermostat ingresses sıcaklık olay 2 dakikada; bir nem her 15 dakikada ingressed olayıdır.</span><span class="sxs-lookup"><span data-stu-id="04865-192">By default, the thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="04865-193">Her iki olay ingressed olduğunda karşılık gelen sıcaklık veya nem ölçülen süreyi gösterir bir zaman damgası dahil etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="04865-193">When either event is ingressed, it must include a timestamp that shows the time that the corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="04865-194">Bu senaryo verildiğinde, veri modeli için iki farklı yol göstermek ve etkisi açıklayacağız modelleme serileştirilmiş çıktı sahiptir.</span><span class="sxs-lookup"><span data-stu-id="04865-194">Given this scenario, we'll demonstrate two different ways to model the data, and we'll explain the effect that modeling has on the serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="04865-195">Model 1</span><span class="sxs-lookup"><span data-stu-id="04865-195">Model 1</span></span>
<span data-ttu-id="04865-196">Önceki senaryoda destekleyen bir model ilk sürümü şöyledir:</span><span class="sxs-lookup"><span data-stu-id="04865-196">Here's the first version of a model that supports the previous scenario:</span></span>

```
BEGIN_NAMESPACE(Contoso);

DECLARE_STRUCT(TemperatureEvent,
int, Temperature,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_STRUCT(HumidityEvent,
int, Humidity,
EDM_DATE_TIME_OFFSET, Time);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureEvent, Temperature),
WITH_DATA(HumidityEvent, Humidity)
);

END_NAMESPACE(Contoso);
```

<span data-ttu-id="04865-197">Model iki veri olaylarını içerdiğini unutmayın: **sıcaklık** ve **nem**.</span><span class="sxs-lookup"><span data-stu-id="04865-197">Note that the model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="04865-198">Önceki örneklerde farklı olarak, her olay kullanılarak tanımlanmış bir yapı türünde **DECLARE\_YAPISI**.</span><span class="sxs-lookup"><span data-stu-id="04865-198">Unlike previous examples, the type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="04865-199">**TemperatureEvent** ısı ölçümü ve zaman damgası; içerir **HumidityEvent** nem ölçümü ve zaman damgası içeriyor.</span><span class="sxs-lookup"><span data-stu-id="04865-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="04865-200">Bu model bize yukarıda açıklanan senaryo için veri modeli için doğal bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="04865-200">This model gives us a natural way to model the data for the scenario described above.</span></span> <span data-ttu-id="04865-201">Bir olay buluta gönderirken ya da sıcaklık/zaman damgası veya bir nem/zaman damgası çifti göndereceğiz.</span><span class="sxs-lookup"><span data-stu-id="04865-201">When we send an event to the cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="04865-202">Aşağıdaki gibi kod kullanarak buluta sıcaklık olay gönderebiliriz:</span><span class="sxs-lookup"><span data-stu-id="04865-202">We can send a temperature event to the cloud using code such as the following:</span></span>

```
time_t now;
time(&now);
thermostat->Temperature.Temperature = 75;
thermostat->Temperature.Time = GetDateTimeOffset(now);

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="04865-203">Biz sabit kodlanmış değerler sıcaklık ve nem örnek kodda kullanır, ancak biz aslında bu değerleri thermostat üzerinde karşılık gelen algılayıcı örnekleyerek alma olduğunu düşünün.</span><span class="sxs-lookup"><span data-stu-id="04865-203">We'll use hard-coded values for temperature and humidity in the sample code, but imagine that we’re actually retrieving these values by sampling the corresponding sensors on the thermostat.</span></span>

<span data-ttu-id="04865-204">Yukarıdaki kullanan kodu **GetDateTimeOffset** önceden sunulan Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="04865-204">The code above uses the **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="04865-205">Clear sonraki olacak nedeniyle, bu kod açıkça seri hale getirme ve olay gönderme görevi ayırır.</span><span class="sxs-lookup"><span data-stu-id="04865-205">For reasons that will become clear later, this code explicitly separates the task of serializing and sending the event.</span></span> <span data-ttu-id="04865-206">Önceki kod sıcaklık olay bir arabelleğe serileştirir.</span><span class="sxs-lookup"><span data-stu-id="04865-206">The previous code serializes the temperature event into a buffer.</span></span> <span data-ttu-id="04865-207">Ardından, **sendMessage** yardımcı işlevi (dahil **simplesample\_amqp**), IOT Hub'ına olay gönderir:</span><span class="sxs-lookup"><span data-stu-id="04865-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends the event to IoT Hub:</span></span>

```
static void sendMessage(IOTHUB_CLIENT_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle != NULL)
    {
        IoTHubClient_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId);

        IoTHubMessage_Destroy(messageHandle);
    }
    free((void*)buffer);
}
```

<span data-ttu-id="04865-208">Bu kod bir alt kümesidir **SendAsync** biz üzerine yeniden buraya gidin olmaz şekilde önceki bölümde açıklanan Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="04865-208">This code is a subset of the **SendAsync** helper described in the previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="04865-209">Biz sıcaklık olay göndermek için önceki kod çalıştırdığınızda, olayın serileştirilmiş bu formu IOT Hub'ına gönderilir:</span><span class="sxs-lookup"><span data-stu-id="04865-209">When we run the previous code to send the Temperature event, this serialized form of the event is sent to IoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="04865-210">Biz türü olan bir sıcaklık gönderiyorsanız **TemperatureEvent** ve bu yapı içeren bir **sıcaklık** ve **zaman** üyesi.</span><span class="sxs-lookup"><span data-stu-id="04865-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="04865-211">Bu, doğrudan seri duruma getirilmiş verilerde yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="04865-211">This is directly reflected in the serialized data.</span></span>

<span data-ttu-id="04865-212">Benzer şekilde, biz bu kodu nem olayla gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="04865-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="04865-213">IOT Hub'ına gönderilen serileştirilmiş form aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="04865-213">The serialized form that’s sent to IoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="04865-214">Yeniden, bu beklenen biçimde değil.</span><span class="sxs-lookup"><span data-stu-id="04865-214">Again, this is as expected.</span></span>

<span data-ttu-id="04865-215">Bu model ile nasıl ek olaylar hayal edebildiğiniz kolayca eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="04865-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="04865-216">Kullanarak daha fazla yapıları tanımladığınız **DECLARE\_YAPISI**ve karşılık gelen olay kullanarak modeli dahil **ile\_veri**.</span><span class="sxs-lookup"><span data-stu-id="04865-216">You define more structures using **DECLARE\_STRUCT**, and include the corresponding event in the model using **WITH\_DATA**.</span></span>

<span data-ttu-id="04865-217">Şimdi, model böylece aynı verileri içerir, ancak farklı bir yapıya sahip değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="04865-217">Now, let’s modify the model so that it includes the same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="04865-218">Model 2</span><span class="sxs-lookup"><span data-stu-id="04865-218">Model 2</span></span>
<span data-ttu-id="04865-219">Bu alternatif model yukarıdakine göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="04865-219">Consider this alternative model to the one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="04865-220">Bu durumda biz olmadığı anlaşılmış olur **DECLARE\_YAPISI** makroları ve Senaryomuzda basit türler Modelleme Dili kullanarak veri öğelerinden yalnızca tanımlama.</span><span class="sxs-lookup"><span data-stu-id="04865-220">In this case we've eliminated the **DECLARE\_STRUCT** macros and are simply defining the data items from our scenario using simple types from the modeling language.</span></span>

<span data-ttu-id="04865-221">Yalnızca şu anda şirketinizdeki Yoksay **zaman** olay.</span><span class="sxs-lookup"><span data-stu-id="04865-221">Just for the moment let’s ignore the **Time** event.</span></span> <span data-ttu-id="04865-222">Bu aralık ile giriş koda işte **sıcaklık**:</span><span class="sxs-lookup"><span data-stu-id="04865-222">With that aside, here’s the code to ingress **Temperature**:</span></span>

```
time_t now;
time(&now);
thermostat->Temperature = 75;

unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="04865-223">Bu kod, IOT Hub'ına aşağıdaki serileştirilmiş olay gönderir:</span><span class="sxs-lookup"><span data-stu-id="04865-223">This code sends the following serialized event to IoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="04865-224">Ve nem olay göndermek için kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="04865-224">And the code for sending the Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="04865-225">Bu kod bu IOT Hub'ına gönderir:</span><span class="sxs-lookup"><span data-stu-id="04865-225">This code sends this to IoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="04865-226">Şu ana kadar var. yine de hiçbir beklenmeyen durumları.</span><span class="sxs-lookup"><span data-stu-id="04865-226">So far there are still no surprises.</span></span> <span data-ttu-id="04865-227">Şimdi SERİLEŞTİRME makrosu nasıl kullanırız değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="04865-227">Now let's change how we use the SERIALIZE macro.</span></span>

<span data-ttu-id="04865-228">**SERİLEŞTİRME** makrosu bağımsız değişken birden çok veri olaylarını alabilir.</span><span class="sxs-lookup"><span data-stu-id="04865-228">The **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="04865-229">Bu seri hale getirmemize sağlar **sıcaklık** ve **nem** birlikte olay ve tek çağrıda IOT Hub'ına gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="04865-229">This enables us to serialize the **Temperature** and **Humidity** event together and send them to IoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="04865-230">Bu kodun sonucunda iki veri olayları IOT Hub'ına gönderilir olduğunu tahmin:</span><span class="sxs-lookup"><span data-stu-id="04865-230">You might guess that the result of this code is that two data events are sent to IoT Hub:</span></span>

<span data-ttu-id="04865-231">[</span><span class="sxs-lookup"><span data-stu-id="04865-231">[</span></span>

<span data-ttu-id="04865-232">{"Sıcaklık": 75},</span><span class="sxs-lookup"><span data-stu-id="04865-232">{"Temperature":75},</span></span>

<span data-ttu-id="04865-233">{"Nem": 45}</span><span class="sxs-lookup"><span data-stu-id="04865-233">{"Humidity":45}</span></span>

<span data-ttu-id="04865-234">]</span><span class="sxs-lookup"><span data-stu-id="04865-234">]</span></span>

<span data-ttu-id="04865-235">Diğer bir deyişle, bu kod gönderme ile aynı olduğunu bekleyebilirsiniz **sıcaklık** ve **nem** ayrı olarak.</span><span class="sxs-lookup"><span data-stu-id="04865-235">In other words, you might expect that this code is the same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="04865-236">Her iki olayları iletmek için yalnızca kolaylık sağlamak olan **SERİLEŞTİRME** aynı çağrısında.</span><span class="sxs-lookup"><span data-stu-id="04865-236">It’s just a convenience to pass both events to **SERIALIZE** in the same call.</span></span> <span data-ttu-id="04865-237">Ancak, bu durumda değil.</span><span class="sxs-lookup"><span data-stu-id="04865-237">However, that’s not the case.</span></span> <span data-ttu-id="04865-238">Bunun yerine, yukarıdaki kod bu tek bir veri olayı, IOT Hub'ına gönderir:</span><span class="sxs-lookup"><span data-stu-id="04865-238">Instead, the code above sends this single data event to IoT Hub:</span></span>

<span data-ttu-id="04865-239">{"Sıcaklık": 75 "nem": 45}</span><span class="sxs-lookup"><span data-stu-id="04865-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="04865-240">Modelimizi tanımladığından Bu tuhaf görünebilir **sıcaklık** ve **nem** iki olarak *ayrı* olayları:</span><span class="sxs-lookup"><span data-stu-id="04865-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="04865-241">Daha noktasına Biz bu olayları modelini alamadık nerede **sıcaklık** ve **nem** aynı yapısında şunlardır:</span><span class="sxs-lookup"><span data-stu-id="04865-241">More to the point, we didn’t model these events where **Temperature** and **Humidity** are in the same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="04865-242">Bu model kullansaydık anlamak daha kolay olacaktır nasıl **sıcaklık** ve **nem** aynı serileştirilmiş iletisinde gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="04865-242">If we used this model, it would be easier to understand how **Temperature** and **Humidity** would be sent in the same serialized message.</span></span> <span data-ttu-id="04865-243">Her iki veri olaylarını geçirdiğinizde bu şekilde çalıştığını neden ancak onu Temizle olmayabilir **SERİLEŞTİRME** kullanarak modeli 2.</span><span class="sxs-lookup"><span data-stu-id="04865-243">However it may not be clear why it works that way when you pass both data events to **SERIALIZE** using model 2.</span></span>

<span data-ttu-id="04865-244">Bu davranış, varsayımlar, biliyorsanız anlamak daha kolay **seri hale getirici** kitaplığı yapma.</span><span class="sxs-lookup"><span data-stu-id="04865-244">This behavior is easier to understand if you know the assumptions that the **serializer** library is making.</span></span> <span data-ttu-id="04865-245">Bu bizim modele geri edelim anlamlı için:</span><span class="sxs-lookup"><span data-stu-id="04865-245">To make sense of this let’s go back to our model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="04865-246">Bu model nesne yönelimli koşullarında düşünün.</span><span class="sxs-lookup"><span data-stu-id="04865-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="04865-247">Bu durumda biz fiziksel bir aygıtı (thermostat) modelleme ve o aygıtı gibi özniteliklerini içerir **sıcaklık** ve **nem**.</span><span class="sxs-lookup"><span data-stu-id="04865-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="04865-248">Modelimizi aşağıdaki gibi kod ile tüm durumunu gönderebiliriz:</span><span class="sxs-lookup"><span data-stu-id="04865-248">We can send the entire state of our model with code such as the following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="04865-249">Sıcaklık değerlerini varsayıldığında, nem ve saatini ayarlayın, biz bu IOT Hub'ına gönderilen gibi bir olay görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="04865-249">Assuming the values of Temperature, Humidity and Time are set, we would see an event like this sent to IoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="04865-250">Bazı durumlarda, yalnızca göndermek isteyebilirsiniz *bazı* (Bu, çok sayıda veri olaylarını modelinizi içeriyorsa, özellikle true) buluta modelin özellikleri.</span><span class="sxs-lookup"><span data-stu-id="04865-250">Sometimes you may only want to send *some* properties of the model to the cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="04865-251">Önceki örneğimizde gibi yalnızca bir alt veri olayların göndermek yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="04865-251">It’s useful to send only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="04865-252">Tanımlanan olarak, bu tam olarak aynı serileştirilmiş olay oluşturur bir **TemperatureEvent** ile bir **sıcaklık** ve **zaman** üye, biz ile 1 model gibi.</span><span class="sxs-lookup"><span data-stu-id="04865-252">This generates exactly the same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="04865-253">Bu durumda biz adlı olduğundan farklı bir model (model 2) kullanarak tam olarak aynı serileştirilmiş olayı Oluştur bulduk **SERİLEŞTİRME** farklı bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="04865-253">In this case we were able to generate exactly the same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="04865-254">Birden çok veri olaylarını geçirirseniz olan en önemli nokta **SERİLEŞTİRME,** sonra her olay tek bir JSON nesnesi özelliğinde olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="04865-254">The important point is that if you pass multiple data events to **SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="04865-255">En iyi yaklaşımı, ve modelinizi hakkında nasıl düşündüğünüz bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="04865-255">The best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="04865-256">Buluta "olayları" gönderiyorsanız ve her olay tanımlanmış bir özellik kümesi içeriyorsa, ilk yaklaşım çok algılama hale getirir.</span><span class="sxs-lookup"><span data-stu-id="04865-256">If you’re sending "events" to the cloud and each event contains a defined set of properties, then the first approach makes a lot of sense.</span></span> <span data-ttu-id="04865-257">Bu durumda kullanacağınız **DECLARE\_YAPISI** her olay yapısını tanımlar ve bunları modelinizi dahil **ile\_veri** makrosu.</span><span class="sxs-lookup"><span data-stu-id="04865-257">In that case you would use **DECLARE\_STRUCT** to define the structure of each event and then include them in your model with the **WITH\_DATA** macro.</span></span> <span data-ttu-id="04865-258">Daha sonra ilk yukarıdaki örnekte yaptığımız gibi her olay gönderin.</span><span class="sxs-lookup"><span data-stu-id="04865-258">Then you send each event as we did in the first example above.</span></span> <span data-ttu-id="04865-259">Bu yaklaşım, yalnızca bir tek veri olayı geçip geçmeyeceğini **seri hale GETİRİCİ**.</span><span class="sxs-lookup"><span data-stu-id="04865-259">In this approach you would only pass a single data event to **SERIALIZER**.</span></span>

<span data-ttu-id="04865-260">Nesne odaklı bir şekilde modelinizde hakkında düşünüyorsanız, ikinci yaklaşımın size uygun.</span><span class="sxs-lookup"><span data-stu-id="04865-260">If you think about your model in an object-oriented fashion, then the second approach may suit you.</span></span> <span data-ttu-id="04865-261">Bu durumda, öğeleri tanımlanan kullanarak **ile\_veri** nesnenizin "Özellikler".</span><span class="sxs-lookup"><span data-stu-id="04865-261">In this case, the elements defined using **WITH\_DATA** are the "properties" of your object.</span></span> <span data-ttu-id="04865-262">Her alt olayların geçirdiğiniz **SERİLEŞTİRME** , bağlı olarak, istediğiniz buluta göndermek için "nesnenin" durumu ne kadarının ister.</span><span class="sxs-lookup"><span data-stu-id="04865-262">You pass whatever subset of events to **SERIALIZE** that you like, depending on how much of your "object’s" state you want to send to the cloud.</span></span>

<span data-ttu-id="04865-263">Doğru veya yanlış bir bağlanamadı yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="04865-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="04865-264">Yalnızca, nasıl unutmayın **seri hale getirici** kitaplığı çalışır ve çekme gereksinimlerine en uygun modelleme yaklaşım.</span><span class="sxs-lookup"><span data-stu-id="04865-264">Just be aware of how the **serializer** library works, and pick the modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="04865-265">İleti işleme</span><span class="sxs-lookup"><span data-stu-id="04865-265">Message handling</span></span>
<span data-ttu-id="04865-266">Şu ana kadar bu makalede, IOT Hub'ına gönderen olayları ele alınan yalnızca ve iletileri alma ele kurmadı.</span><span class="sxs-lookup"><span data-stu-id="04865-266">So far this article has only discussed sending events to IoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="04865-267">Bu, biz iletileri alma hakkında bilmeniz gerekenler için nedeni büyük ölçüde içinde ele alınmış bir [önceki makalesi](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="04865-267">The reason for this is that what we need to know about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="04865-268">Bu makaleden bir ileti geri çağırma işlevini kaydederek iletileri işleme geri çağırma:</span><span class="sxs-lookup"><span data-stu-id="04865-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="04865-269">Ardından, bir ileti alındığında çağrılan geri çağırma işlevi de yazın:</span><span class="sxs-lookup"><span data-stu-id="04865-269">You then write the callback function that’s invoked when a message is received:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable to IoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed to malloc\r\n");
            result = EXECUTE_COMMAND_ERROR;
        }
        else
        {
            memcpy(temp, buffer, size);
            temp[size] = '\0';
            EXECUTE_COMMAND_RESULT executeCommandResult = EXECUTE_COMMAND(userContextCallback, temp);
            result =
                (executeCommandResult == EXECUTE_COMMAND_ERROR) ? IOTHUBMESSAGE_ABANDONED :
                (executeCommandResult == EXECUTE_COMMAND_SUCCESS) ? IOTHUBMESSAGE_ACCEPTED :
                IOTHUBMESSAGE_REJECTED;
            free(temp);
        }
    }
    return result;
}
```

<span data-ttu-id="04865-270">Bu uygulaması, **IoTHubMessage** modelinizdeki her eylem için belirli bir işlevi çağırır.</span><span class="sxs-lookup"><span data-stu-id="04865-270">This implementation of **IoTHubMessage** calls the specific function for each action in your model.</span></span> <span data-ttu-id="04865-271">Örneğin bu eylemi modelinizi tanımlar:</span><span class="sxs-lookup"><span data-stu-id="04865-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="04865-272">Bu imza işleviyle tanımlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="04865-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position to %d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="04865-273">**SetAirResistance** aygıtınıza ileti gönderildiğinde daha sonra çağrılır.</span><span class="sxs-lookup"><span data-stu-id="04865-273">**SetAirResistance** is then called when that message is sent to your device.</span></span>

<span data-ttu-id="04865-274">Ne biz açıklandığı henüz henüz iletisinin seri duruma getirilmiş sürüm ne aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="04865-274">What we haven't explained yet is what the serialized version of message looks like.</span></span> <span data-ttu-id="04865-275">Diğer bir deyişle, göndermek istiyorsanız bir **SetAirResistance** Cihazınızı iletiye, ne görünüm ister?</span><span class="sxs-lookup"><span data-stu-id="04865-275">In other words, if you want to send a **SetAirResistance** message to your device, what does that look like?</span></span>

<span data-ttu-id="04865-276">Bir cihaza bir ileti gönderiyorsanız, Azure IOT hizmeti SDK bunu.</span><span class="sxs-lookup"><span data-stu-id="04865-276">If you're sending a message to a device, you would do so through the Azure IoT service SDK.</span></span> <span data-ttu-id="04865-277">Hala belirli bir eylemi çağırmak göndermek için hangi dize bilmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="04865-277">You still need to know what string to send to invoke a particular action.</span></span> <span data-ttu-id="04865-278">Bir ileti göndermek için genel biçim şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="04865-278">The general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="04865-279">Serileştirilmiş bir JSON nesnesi iki özellikleriyle gönderiyorsanız: **adı** (ileti) eylem adı ve **parametreleri** Bu eylem parametrelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="04865-279">You're sending a serialized JSON object with two properties: **Name** is the name of the action (message) and **Parameters** contains the parameters of that action.</span></span>

<span data-ttu-id="04865-280">Örneğin, çağrılacak **SetAirResistance** bu iletiyi bir cihaza gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="04865-280">For example, to invoke **SetAirResistance** you can send this message to a device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="04865-281">Eylem adı, modelde tanımlanan bir eylem tam olarak eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="04865-281">The action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="04865-282">Parametre adları de eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="04865-282">The parameter names must match as well.</span></span> <span data-ttu-id="04865-283">Ayrıca, büyük küçük harfe duyarlılığın unutmayın.</span><span class="sxs-lookup"><span data-stu-id="04865-283">Also note case sensitivity.</span></span> <span data-ttu-id="04865-284">**Ad** ve **parametreleri** her zaman büyük harfle yazılır.</span><span class="sxs-lookup"><span data-stu-id="04865-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="04865-285">Eylem adı ve modelinizdeki parametreleri büyük küçük harf duyarlı emin olun.</span><span class="sxs-lookup"><span data-stu-id="04865-285">Make sure to match the case of your action name and parameters in your model.</span></span> <span data-ttu-id="04865-286">Bu örnekte, eylem adı "SetAirResistance" değil "setairresistance" ise.</span><span class="sxs-lookup"><span data-stu-id="04865-286">In this example, the action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="04865-287">İki diğer eylemler **TurnFanOn** ve **TurnFanOff** bir aygıta bu iletiler göndererek çağrılır:</span><span class="sxs-lookup"><span data-stu-id="04865-287">The two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages to a device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="04865-288">Bu bölümde alma ve gönderme olayları zaman iletileri ile bilmeniz gereken her şeyi açıklanan **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="04865-288">This section described everything you need to know when sending events and receiving messages with the **serializer** library.</span></span> <span data-ttu-id="04865-289">Devam etmeden önce şimdi ne kadar büyük modelinizi denetleyebilir yapılandırabileceğiniz bazı parametreler kapsar.</span><span class="sxs-lookup"><span data-stu-id="04865-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="04865-290">Makro yapılandırma</span><span class="sxs-lookup"><span data-stu-id="04865-290">Macro configuration</span></span>
<span data-ttu-id="04865-291">Kullanıyorsanız, **seri hale getirici** SDK'sı dikkat edilmesi gereken önemli bir kısmını azure-c-paylaşılan-yardımcı programı Kitaplığı'nda bulunan kitaplık.</span><span class="sxs-lookup"><span data-stu-id="04865-291">If you’re using the **Serializer** library an important part of the SDK to be aware of is found in the azure-c-shared-utility library.</span></span>
<span data-ttu-id="04865-292">GitHub--özyinelemeli seçeneğini kullanarak Azure-IOT-sdk-c depodan klonlanmış varsa, bu paylaşılan yardımcı kitaplık yer alır:</span><span class="sxs-lookup"><span data-stu-id="04865-292">If you have cloned the Azure-iot-sdk-c repository from GitHub using the --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="04865-293">Kitaplık klonlanmış değil, bulabilirsiniz [burada](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="04865-293">If you have not cloned the library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="04865-294">Paylaşılan yardımcı kitaplıkta şu klasörü bulacaksınız:</span><span class="sxs-lookup"><span data-stu-id="04865-294">Within the shared utility library, you will find the following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="04865-295">Adlı bir Visual Studio çözümü bu klasörde **makrosu\_yardımcı programları\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="04865-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="04865-296">Bu çözümdeki programın oluşturduğu **makrosu\_utils.h** dosya.</span><span class="sxs-lookup"><span data-stu-id="04865-296">The program in this solution generates the **macro\_utils.h** file.</span></span> <span data-ttu-id="04865-297">Varsayılan makrosu yoktur\_SDK ile birlikte bulunan utils.h dosyası.</span><span class="sxs-lookup"><span data-stu-id="04865-297">There’s a default macro\_utils.h file included with the SDK.</span></span> <span data-ttu-id="04865-298">Bu çözüm, bu parametrelere göre üst bilgi dosyasını yeniden oluşturun ve bazı parametreler değiştirmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="04865-298">This solution allows you to modify some parameters and then recreate the header file based on these parameters.</span></span>

<span data-ttu-id="04865-299">İle ilgili olarak iki anahtar parametreleri **nArithmetic** ve **nMacroParameters** makro içinde bulunan bu iki satır içinde tanımlanan\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="04865-299">The two key parameters to be concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="04865-300">Bu değerler SDK ile birlikte dahil varsayılan parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="04865-300">These values are the default parameters included with the SDK.</span></span> <span data-ttu-id="04865-301">Her bir parametreyi şu anlama sahiptir:</span><span class="sxs-lookup"><span data-stu-id="04865-301">Each parameter has the following meaning:</span></span>

* <span data-ttu-id="04865-302">nMacroParameters – denetimleri içinde bir DECLARE olabilir kaç parametreleri\_modeli makro tanımı.</span><span class="sxs-lookup"><span data-stu-id="04865-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="04865-303">nArithmetic – üyeleri bir model izin verilen toplam sayısını denetler.</span><span class="sxs-lookup"><span data-stu-id="04865-303">nArithmetic – Controls the total number of members allowed in a model.</span></span>

<span data-ttu-id="04865-304">Bunlar denetlemek için bu parametreler önemli modelinizi ne kadar büyük olabilir nedenidir.</span><span class="sxs-lookup"><span data-stu-id="04865-304">The reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="04865-305">Örneğin, bu model tanımı göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="04865-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="04865-306">Daha önce belirtildiği gibi **DECLARE\_MODEL** yalnızca C makro.</span><span class="sxs-lookup"><span data-stu-id="04865-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="04865-307">Model adını ve **ile\_veri** deyimi (henüz başka bir makrosu) olan parametrelerinin **DECLARE\_modeli**.</span><span class="sxs-lookup"><span data-stu-id="04865-307">The names of the model and the **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="04865-308">**nMacroParameters** kaç parametreleri eklenebilir tanımlar **DECLARE\_modeli**.</span><span class="sxs-lookup"><span data-stu-id="04865-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="04865-309">Etkili bir şekilde sağlayabilirsiniz kaç tane veri olay ve eylem bildirimleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="04865-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="04865-310">Bu nedenle, 124 varsayılan sınır ile bu 60 eylemleri ve veri olayları birleşimi ile bir model tanımlayabilirsiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="04865-310">As such, with the default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="04865-311">Bu sınırı aşarsanız çalışırsanız, aşağıdakine benzer derleyici hataları alırsınız:</span><span class="sxs-lookup"><span data-stu-id="04865-311">If you try to exceed this limit, you'll receive compiler errors that look similar to this:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="04865-312">**NArithmetic** parametredir uygulamanızı'den daha fazla Internet'in iç makro dili hakkında.</span><span class="sxs-lookup"><span data-stu-id="04865-312">The **nArithmetic** parameter is more about the internal workings of the macro language than your application.</span></span>  <span data-ttu-id="04865-313">Modelinizde, olabilir üyeleri toplam sayısını denetlediği de dahil olmak üzere **DECLARE_STRUCT** makroları.</span><span class="sxs-lookup"><span data-stu-id="04865-313">It controls the total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="04865-314">Bu gibi derleyici hataları görmeye başlayacaksınız sonra artırmayı denemelisiniz **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="04865-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="04865-315">Bu parametreleri değiştirmek istiyorsanız, makrosu değiştirin\_utils.tt dosya, makrosu derlenir\_yardımcı programları\_h\_generator.sln çözüm ve derlenmiş programını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="04865-315">If you want to change these parameters, modify the values in the macro\_utils.tt file, recompile the macro\_utils\_h\_generator.sln solution, and run the compiled program.</span></span> <span data-ttu-id="04865-316">Bunu yaptığınızda bunu yeni bir makro\_utils.h dosya oluşturulur ve yerleştirilir.\\ Ortak\\Inc dizini.</span><span class="sxs-lookup"><span data-stu-id="04865-316">When you do so, a new macro\_utils.h file is generated and placed in the .\\common\\inc directory.</span></span>

<span data-ttu-id="04865-317">Makro yeni sürümü kullanmak için\_utils.h, kaldırma **seri hale getirici** NuGet paketi çözümünüzden ve onun yerine dahil **seri hale getirici** Visual Studio projesi.</span><span class="sxs-lookup"><span data-stu-id="04865-317">In order to use the new version of macro\_utils.h, remove the **serializer** NuGet package from your solution and in its place include the **serializer** Visual Studio project.</span></span> <span data-ttu-id="04865-318">Bu seri hale getirici kitaplığı karşı Kaynak Kodu derlemek kodunuzu sağlar.</span><span class="sxs-lookup"><span data-stu-id="04865-318">This enables your code to compile against the source code of the serializer library.</span></span> <span data-ttu-id="04865-319">Bu güncelleştirilmiş makrosu içerir\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="04865-319">This includes the updated macro\_utils.h.</span></span> <span data-ttu-id="04865-320">Bunu yapmak istiyorsanız, **simplesample\_amqp**, seri hale getirici kitaplığı NuGet paketi çözümden kaldırarak Başlat:</span><span class="sxs-lookup"><span data-stu-id="04865-320">If you want to do this for **simplesample\_amqp**, start by removing the NuGet package for the serializer library from the solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="04865-321">Daha sonra bu projeyi Visual Studio çözümünüzü ekleyin:</span><span class="sxs-lookup"><span data-stu-id="04865-321">Then add this project to your Visual Studio solution:</span></span>

> <span data-ttu-id="04865-322">. \\c\\seri hale getirici\\yapı\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="04865-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="04865-323">İşiniz bittiğinde, çözümünüzün aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="04865-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="04865-324">Şimdi ne zaman, derleme güncelleştirilmiş makrosu çözümünüzü\_utils.h ikili dosyanız yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="04865-324">Now when you compile your solution, the updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="04865-325">Bu değerleri yeterince artırma derleyici sınırları aşabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="04865-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="04865-326">Bu noktaya **nMacroParameters** endişelenmeniz kullanılacak ana parametresidir.</span><span class="sxs-lookup"><span data-stu-id="04865-326">To this point, the **nMacroParameters** is the main parameter with which to be concerned.</span></span> <span data-ttu-id="04865-327">En az 127 parametrelerden biri izin verilen bir makro tanımı'nda C99 spec belirtir.</span><span class="sxs-lookup"><span data-stu-id="04865-327">The C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="04865-328">Microsoft derleyici spec tam olarak aşağıdaki (ve 127 sınırı), artırmak mümkün olmayacaktır **nMacroParameters** varsayılan ötesinde.</span><span class="sxs-lookup"><span data-stu-id="04865-328">The Microsoft compiler follows the spec exactly (and has a limit of 127), so you won't be able to increase **nMacroParameters** beyond the default.</span></span> <span data-ttu-id="04865-329">Diğer derleyiciler, bunu yapmak izin verebilir (örneğin, GNU derleyici daha yüksek bir sınır destekler).</span><span class="sxs-lookup"><span data-stu-id="04865-329">Other compilers might allow you to do so (for example, the GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="04865-330">Şu ana kadar biz neredeyse koduyla yazma hakkında bilmeniz gereken her şeyi kapsamdaki **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="04865-330">So far we've covered just about everything you need to know about how to write code with the **serializer** library.</span></span> <span data-ttu-id="04865-331">Tamamlanırken önce şimdi bazı konular hakkında merak ediyor önceki makalelerden yeniden ziyaret.</span><span class="sxs-lookup"><span data-stu-id="04865-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="the-lower-level-apis"></a><span data-ttu-id="04865-332">Alt düzey API'ları</span><span class="sxs-lookup"><span data-stu-id="04865-332">The lower-level APIs</span></span>
<span data-ttu-id="04865-333">Bu makale üzerinde odaklanmış örnek uygulama **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="04865-333">The sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="04865-334">Bu örnek daha üst düzey (olmayan-"tümü") kullanan iletileri olayları göndermek ve almak için API'ler.</span><span class="sxs-lookup"><span data-stu-id="04865-334">This sample uses the higher-level (the non-"LL") APIs to send events and receive messages.</span></span> <span data-ttu-id="04865-335">Bu API'leri kullanırsanız, hem olayları ileti gönderme ve alma, mvc'deki bir arka plan iş parçacığı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="04865-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="04865-336">Ancak, bu arka plan iş parçacığı ortadan kaldırmak ve açık denetim olayları gönderirken veya buluttan iletilerini almak için alt düzey (Tümü) API'ları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04865-336">However, you can use the lower-level (LL) APIs to eliminate this background thread and take explicit control over when you send events or receive messages from the cloud.</span></span>

<span data-ttu-id="04865-337">Bölümünde açıklandığı gibi bir [önceki makale](iot-hub-device-sdk-c-iothubclient.md), üst düzey API'lerinin oluşan bir dizi işlevleri vardır:</span><span class="sxs-lookup"><span data-stu-id="04865-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of the higher-level APIs:</span></span>

* <span data-ttu-id="04865-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="04865-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="04865-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="04865-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="04865-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="04865-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="04865-341">IoTHubClient\_yok</span><span class="sxs-lookup"><span data-stu-id="04865-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="04865-342">Bu API'leri örneklerde gösterildiği **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="04865-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="04865-343">Ayrıca vardır benzer bir alt düzey API kümesi.</span><span class="sxs-lookup"><span data-stu-id="04865-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="04865-344">IoTHubClient\_ÜM\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="04865-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="04865-345">IoTHubClient\_ÜM\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="04865-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="04865-346">IoTHubClient\_ÜM\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="04865-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="04865-347">IoTHubClient\_ÜM\_yok</span><span class="sxs-lookup"><span data-stu-id="04865-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="04865-348">Alt düzey API'ları önceki makalelerinde açıklandığı gibi tamamen aynı şekilde çalıştığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="04865-348">Note that the lower-level APIs work exactly the same way as described in the previous articles.</span></span> <span data-ttu-id="04865-349">Gönderen olaylar ve alıcı iletileri işlemek için bir arka plan iş parçacığı isterseniz ilk dizi API kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04865-349">You can use the first set of APIs if you want a background thread to handle sending events and receiving messages.</span></span> <span data-ttu-id="04865-350">Açık denetim zaman göndermek ve IOT Hub'ından veri almak istiyorsanız, ikinci dizi API kullanın.</span><span class="sxs-lookup"><span data-stu-id="04865-350">You use the second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="04865-351">API iş ayarlayın ya da eşit ile yanı sıra **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="04865-351">Either set of APIs work equally well with the **serializer** library.</span></span>

<span data-ttu-id="04865-352">Alt düzey API'ları ile nasıl kullanıldığı bir örnek için **seri hale getirici** kitaplığı bkz **simplesample\_http** uygulama.</span><span class="sxs-lookup"><span data-stu-id="04865-352">For an example of how the lower-level APIs are used with the **serializer** library, see the **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="04865-353">Ek konu başlıkları</span><span class="sxs-lookup"><span data-stu-id="04865-353">Additional topics</span></span>
<span data-ttu-id="04865-354">Söz değerinde birkaç diğer yeniden işleme, diğer aygıt kimlik bilgisi ve yapılandırma seçeneklerini kullanarak özellik konulardır.</span><span class="sxs-lookup"><span data-stu-id="04865-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="04865-355">Tüm konuları ele bunlar bir [önceki makalede](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="04865-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="04865-356">Bu özelliklerin tümü, ile aynı şekilde çalıştığını ana nokta olan **seri hale getirici** kitaplığı ile göründükleri **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="04865-356">The main point is that all of these features work in the same way with the **serializer** library as they do with the **IoTHubClient** library.</span></span> <span data-ttu-id="04865-357">Örneğin, Özellikler modelinizin dışında bir olaya bağlamak istiyorsanız, kullandığınız **IoTHubMessage\_özellikleri** ve **harita**\_**örnek**, daha önce açıklanan aynı şekilde:</span><span class="sxs-lookup"><span data-stu-id="04865-357">For example, if you want to attach properties to an event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, the same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="04865-358">Gelen olay oluşturulup oluşturulmadığını **seri hale getirici** kitaplığı veya el ile kullanılarak oluşturulan **IoTHubClient** kitaplığı önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="04865-358">Whether the event was generated from the **serializer** library or created manually using the **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="04865-359">Kullanarak alternatif aygıt kimlik bilgisi için **IoTHubClient\_ÜM\_oluşturma** da çalışır olarak **IoTHubClient\_CreateFromConnectionString** için ayrılırken bir **IOTHUB\_istemci\_İŞLEMEK**.</span><span class="sxs-lookup"><span data-stu-id="04865-359">For the alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="04865-360">Son olarak, kullanıyorsanız, **seri hale getirici** kitaplığı ile yapılandırma seçeneklerini ayarlayabilirsiniz **IoTHubClient\_ÜM\_SetOption** kullanırkenyaptığınızgibi**IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="04865-360">Finally, if you're using the **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using the **IoTHubClient** library.</span></span>

<span data-ttu-id="04865-361">İçin benzersiz bir özelliğini **seri hale getirici** kitaplığı olan API'leri başlatma.</span><span class="sxs-lookup"><span data-stu-id="04865-361">A feature that is unique to the **serializer** library are the initialization APIs.</span></span> <span data-ttu-id="04865-362">Kitaplığı ile çalışmaya başlamadan önce çağırmalısınız **seri hale getirici\_init**:</span><span class="sxs-lookup"><span data-stu-id="04865-362">Before you can start working with the library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="04865-363">Yalnızca arama yapmadan önce bu yapılır **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="04865-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="04865-364">Benzer şekilde, bitirdiğinizde kullanmaktır yaptığınız son çağrının kitaplıkla çalışırken, **seri hale getirici\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="04865-364">Similarly, when you're done working with the library, the last call you’ll make is to **serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="04865-365">Aksi takdirde, yukarıda listelenen diğer özelliklerin tümü aynı iş **seri hale getirici** kitaplığı göründükleri **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="04865-365">Otherwise, all of the other features listed above work the same in the **serializer** library as they do in the **IoTHubClient** library.</span></span> <span data-ttu-id="04865-366">Bu konular hakkında daha fazla bilgi için bkz: [önceki makalede](iot-hub-device-sdk-c-iothubclient.md) bu serideki.</span><span class="sxs-lookup"><span data-stu-id="04865-366">For more information about any of these topics, see the [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04865-367">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="04865-367">Next steps</span></span>
<span data-ttu-id="04865-368">Bu makalede benzersiz yönleri ayrıntılı olarak **seri hale getirici** bulunan kitaplık **C için Azure IOT cihaz SDK'sı**. Modelleri IOT Hub'ından ileti alıp olayları göndermek için nasıl kullanılacağını bir iyi anlamış olmanız gerekir bilgi ile sağlanan.</span><span class="sxs-lookup"><span data-stu-id="04865-368">This article describes in detail the unique aspects of the **serializer** library contained in the **Azure IoT device SDK for C**. With the information provided you should have a good understanding of how to use models to send events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="04865-369">Bu üç bölümlük ile uygulamalar geliştirme konusunda da sonucuna **C için Azure IOT cihaz SDK'sı**. Bu, yalnızca başlamanıza ancak nasıl API'leri işe kapsamlı olarak anlamayı vermek için yeterli bilgi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="04865-369">This also concludes the three-part series on how to develop applications with the **Azure IoT device SDK for C**. This should be enough information to not only get you started but give you a thorough understanding of how the APIs work.</span></span> <span data-ttu-id="04865-370">Ek bilgi için burada kapsanmayan SDK'ın bazı örnekler vardır.</span><span class="sxs-lookup"><span data-stu-id="04865-370">For additional information, there are a few samples in the SDK not covered here.</span></span> <span data-ttu-id="04865-371">Aksi takdirde, [SDK Belgeleri](https://github.com/Azure/azure-iot-sdk-c) ek bilgi için iyi bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="04865-371">Otherwise, the [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="04865-372">IOT Hub için geliştirme hakkında daha fazla bilgi için bkz: [Azure IOT SDK'ları][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="04865-372">To learn more about developing for IoT Hub, see the [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="04865-373">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="04865-373">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="04865-374">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="04865-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
