---
title: "c - seri hale getirici aaaAzure IOT cihaz SDK'sı | Microsoft Docs"
description: "Nasıl toouse hello seri hale getirici C toocreate cihaz uygulamaları için hello Azure IOT cihaz SDK'sı kitaplıkta, bir IOT hub ile iletişim kurar."
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
ms.openlocfilehash: c5776e9b50ffea71df96cb2d342ea2fc045f5a0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a><span data-ttu-id="daff1-103">Azure IOT cihaz SDK'sı için C – seri hale getirici hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="daff1-103">Azure IoT device SDK for C – more about serializer</span></span>
<span data-ttu-id="daff1-104">Merhaba [ilk makale](iot-hub-device-sdk-c-intro.md) bu sunulan serisi hello içinde **C için Azure IOT cihaz SDK'sı**. hello sonraki makalede sağlanan hello daha ayrıntılı bir açıklaması [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="daff1-104">hello [first article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C**. hello next article provided a more detailed description of hello [**IoTHubClient**](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="daff1-105">Bu makalede bileşen kalan hello daha ayrıntılı bir açıklaması sağlayarak hello SDK kapsamını tamamlandıktan: Merhaba **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="daff1-105">This article completes coverage of hello SDK by providing a more detailed description of hello remaining component: hello **serializer** library.</span></span>

<span data-ttu-id="daff1-106">Merhaba giriş makalesi nasıl açıklanan toouse hello **seri hale getirici** kitaplığı toosend olayları tooand IOT Hub'ından iletileri alırsınız.</span><span class="sxs-lookup"><span data-stu-id="daff1-106">hello introductory article described how toouse hello **serializer** library toosend events tooand receive messages from IoT Hub.</span></span> <span data-ttu-id="daff1-107">Bu makalede, biz bu tartışma nasıl daha eksiksiz bir açıklaması sağlayarak genişletmek toomodel hello verilerinizle **seri hale getirici** makro dili.</span><span class="sxs-lookup"><span data-stu-id="daff1-107">In this article, we extend that discussion by providing a more complete explanation of how toomodel your data with hello **serializer** macro language.</span></span> <span data-ttu-id="daff1-108">Merhaba makale ayrıca nasıl hello kitaplığı iletileri serileştiren hakkında daha fazla ayrıntı içerir (ve bazı durumlarda nasıl hello serileştirme davranışını denetleyebileceğiniz).</span><span class="sxs-lookup"><span data-stu-id="daff1-108">hello article also includes more detail about how hello library serializes messages (and in some cases how you can control hello serialization behavior).</span></span> <span data-ttu-id="daff1-109">Biz de oluşturduğunuz hello modelleri hello boyutunu belirleyen değiştirebileceğiniz bazı parametreleri açıklayan.</span><span class="sxs-lookup"><span data-stu-id="daff1-109">We'll also describe some parameters you can modify that determine hello size of hello models you create.</span></span>

<span data-ttu-id="daff1-110">Son olarak, ileti ve özellik işleme gibi önceki makalelerinde kapsanan bazı konular hello makale revisits.</span><span class="sxs-lookup"><span data-stu-id="daff1-110">Finally, hello article revisits some topics covered in previous articles such as message and property handling.</span></span> <span data-ttu-id="daff1-111">Çıkışı, bu özellikleri işlerinde bulacaksınız gibi aynı şekilde hello kullanarak hello **seri hale getirici** kitaplığı ile Merhaba göründükleri **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="daff1-111">As we'll find out, those features work in hello same way using hello **serializer** library as they do with hello **IoTHubClient** library.</span></span>

<span data-ttu-id="daff1-112">Bu makalede açıklanan her şeyi hello üzerinde temel **seri hale getirici** SDK örnekleri.</span><span class="sxs-lookup"><span data-stu-id="daff1-112">Everything described in this article is based on hello **serializer** SDK samples.</span></span> <span data-ttu-id="daff1-113">Merhaba toofollow boyunca istiyorsanız bkz **simplesample\_amqp** ve **simplesample\_http** hello Azure IOT cihaz SDK'sı C. eklenmiş olan uygulamalar</span><span class="sxs-lookup"><span data-stu-id="daff1-113">If you want toofollow along, see hello **simplesample\_amqp** and **simplesample\_http** applications included in hello Azure IoT device SDK for C.</span></span>

<span data-ttu-id="daff1-114">Merhaba bulabilirsiniz [ **C için Azure IOT cihaz SDK'sı** ](https://github.com/Azure/azure-iot-sdk-c) GitHub depo ve görünüm ayrıntılarını hello hello API [C API Başvurusu](https://azure.github.io/azure-iot-sdk-c/index.html).</span><span class="sxs-lookup"><span data-stu-id="daff1-114">You can find hello [**Azure IoT device SDK for C**](https://github.com/Azure/azure-iot-sdk-c) GitHub repository and view details of hello API in hello [C API reference](https://azure.github.io/azure-iot-sdk-c/index.html).</span></span>

## <a name="hello-modeling-language"></a><span data-ttu-id="daff1-115">Merhaba Modelleme Dili</span><span class="sxs-lookup"><span data-stu-id="daff1-115">hello modeling language</span></span>
<span data-ttu-id="daff1-116">Merhaba [giriş makalesi](iot-hub-device-sdk-c-intro.md) bu sunulan serisi hello içinde **C için Azure IOT cihaz SDK'sı** hello sağlanan hello örneğin aracılığıyla dil modelleme **simplesample\_amqp**  uygulama:</span><span class="sxs-lookup"><span data-stu-id="daff1-116">hello [introductory article](iot-hub-device-sdk-c-intro.md) in this series introduced hello **Azure IoT device SDK for C** modeling language through hello example provided in hello **simplesample\_amqp** application:</span></span>

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

<span data-ttu-id="daff1-117">Gördüğünüz gibi dil modelleme hello C makroları temel alır.</span><span class="sxs-lookup"><span data-stu-id="daff1-117">As you can see, hello modeling language is based on C macros.</span></span> <span data-ttu-id="daff1-118">Her zaman tanımınız ile başlayan **başlangıç\_ad alanı** ve her zaman bittiğini **son\_ad alanı**.</span><span class="sxs-lookup"><span data-stu-id="daff1-118">You always begin your definition with **BEGIN\_NAMESPACE** and always end with **END\_NAMESPACE**.</span></span> <span data-ttu-id="daff1-119">Şirketinizde veya bu örnekte, üzerinde çalıştığınız hello proje olduğu gibi'de ortak tooname hello ad alanıdır.</span><span class="sxs-lookup"><span data-stu-id="daff1-119">It's common tooname hello namespace for your company or, as in this example, hello project that you're working on.</span></span>

<span data-ttu-id="daff1-120">Ne hello ad alanı içinde aygıtlardır modelini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="daff1-120">What goes inside hello namespace are model definitions.</span></span> <span data-ttu-id="daff1-121">Bu durumda, tek bir model için bir anemometer yoktur.</span><span class="sxs-lookup"><span data-stu-id="daff1-121">In this case, there is a single model for an anemometer.</span></span> <span data-ttu-id="daff1-122">Bir kez daha, hello modeli adlı bir şey, ancak bu genelde adlı hello aygıt veya veri türü için IOT Hub ile tooexchange istiyor.</span><span class="sxs-lookup"><span data-stu-id="daff1-122">Once again, hello model can be named anything, but typically this is named for hello device or type of data you want tooexchange with IoT Hub.</span></span>  

<span data-ttu-id="daff1-123">Modelleri içeren bir tanımı hello olayları giriş tooIoT Hub olabilir (hello *veri*) IOT Hub'ından alabilir Merhaba iletileri yanı sıra (Merhaba *Eylemler*).</span><span class="sxs-lookup"><span data-stu-id="daff1-123">Models contain a definition of hello events you can ingress tooIoT Hub (hello *data*) as well as hello messages you can receive from IoT Hub (hello *actions*).</span></span> <span data-ttu-id="daff1-124">Merhaba örnekte görebildiğiniz gibi olayları bir türü ve bir ada sahip; Eylemler, bir ad ve isteğe bağlı parametreler (her bir türüyle) sahip.</span><span class="sxs-lookup"><span data-stu-id="daff1-124">As you can see from hello example, events have a type and a name; actions have a name and optional parameters (each with a type).</span></span>

<span data-ttu-id="daff1-125">Merhaba SDK tarafından desteklenen ek veri türleri olan ne Bu örnekte gösterilmez.</span><span class="sxs-lookup"><span data-stu-id="daff1-125">What’s not demonstrated in this sample are additional data types that are supported by hello SDK.</span></span> <span data-ttu-id="daff1-126">Biz bu sonraki ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="daff1-126">We'll cover that next.</span></span>

> [!NOTE]
> <span data-ttu-id="daff1-127">IOT hub'ı başvuran bir aygıt olarak tooit gönderdiği toohello veri *olayları*tooit olarak dil modelleme hello başvuruyor yaparken *veri* (kullanılarak tanımlanan **WITH_DATA**).</span><span class="sxs-lookup"><span data-stu-id="daff1-127">IoT Hub refers toohello data a device sends tooit as *events*, while hello modeling language refers tooit as *data* (defined using **WITH_DATA**).</span></span> <span data-ttu-id="daff1-128">Benzer şekilde, IOT hub'ı toohello veri toodevices olarak gönder başvuruyor *iletileri*tooit olarak dil modelleme hello başvuruyor yaparken *Eylemler* (kullanılarak tanımlanan **WITH_ACTION**).</span><span class="sxs-lookup"><span data-stu-id="daff1-128">Likewise, IoT Hub refers toohello data you send toodevices as *messages*, while hello modeling language refers tooit as *actions* (defined using **WITH_ACTION**).</span></span> <span data-ttu-id="daff1-129">Bu makalede birbirinin yerine kullanılabilir bu koşulları unutmayın.</span><span class="sxs-lookup"><span data-stu-id="daff1-129">Be aware that these terms may be used interchangeably in this article.</span></span>
> 
> 

### <a name="supported-data-types"></a><span data-ttu-id="daff1-130">Desteklenen veri türleri</span><span class="sxs-lookup"><span data-stu-id="daff1-130">Supported data types</span></span>
<span data-ttu-id="daff1-131">veri türleri aşağıdaki hello hello ile oluşturulan modellerinde desteklenir **seri hale getirici** kitaplığı:</span><span class="sxs-lookup"><span data-stu-id="daff1-131">hello following data types are supported in models created with hello **serializer** library:</span></span>

| <span data-ttu-id="daff1-132">Tür</span><span class="sxs-lookup"><span data-stu-id="daff1-132">Type</span></span> | <span data-ttu-id="daff1-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="daff1-133">Description</span></span> |
| --- | --- |
| <span data-ttu-id="daff1-134">Çift</span><span class="sxs-lookup"><span data-stu-id="daff1-134">double</span></span> |<span data-ttu-id="daff1-135">çift duyarlıklı kayan nokta sayısı</span><span class="sxs-lookup"><span data-stu-id="daff1-135">double precision floating point number</span></span> |
| <span data-ttu-id="daff1-136">Int</span><span class="sxs-lookup"><span data-stu-id="daff1-136">int</span></span> |<span data-ttu-id="daff1-137">32 bit tamsayı</span><span class="sxs-lookup"><span data-stu-id="daff1-137">32 bit integer</span></span> |
| <span data-ttu-id="daff1-138">Kayan nokta</span><span class="sxs-lookup"><span data-stu-id="daff1-138">float</span></span> |<span data-ttu-id="daff1-139">tek duyarlıklı kayan nokta sayısı</span><span class="sxs-lookup"><span data-stu-id="daff1-139">single precision floating point number</span></span> |
| <span data-ttu-id="daff1-140">uzun</span><span class="sxs-lookup"><span data-stu-id="daff1-140">long</span></span> |<span data-ttu-id="daff1-141">uzun tamsayı</span><span class="sxs-lookup"><span data-stu-id="daff1-141">long integer</span></span> |
| <span data-ttu-id="daff1-142">int8\_t</span><span class="sxs-lookup"><span data-stu-id="daff1-142">int8\_t</span></span> |<span data-ttu-id="daff1-143">8 bit tam sayı</span><span class="sxs-lookup"><span data-stu-id="daff1-143">8 bit integer</span></span> |
| <span data-ttu-id="daff1-144">int16\_t</span><span class="sxs-lookup"><span data-stu-id="daff1-144">int16\_t</span></span> |<span data-ttu-id="daff1-145">16 bit tam sayı</span><span class="sxs-lookup"><span data-stu-id="daff1-145">16 bit integer</span></span> |
| <span data-ttu-id="daff1-146">Int32\_t</span><span class="sxs-lookup"><span data-stu-id="daff1-146">int32\_t</span></span> |<span data-ttu-id="daff1-147">32 bit tamsayı</span><span class="sxs-lookup"><span data-stu-id="daff1-147">32 bit integer</span></span> |
| <span data-ttu-id="daff1-148">int64\_t</span><span class="sxs-lookup"><span data-stu-id="daff1-148">int64\_t</span></span> |<span data-ttu-id="daff1-149">64 bit tamsayı</span><span class="sxs-lookup"><span data-stu-id="daff1-149">64 bit integer</span></span> |
| <span data-ttu-id="daff1-150">bool</span><span class="sxs-lookup"><span data-stu-id="daff1-150">bool</span></span> |<span data-ttu-id="daff1-151">Boole değeri</span><span class="sxs-lookup"><span data-stu-id="daff1-151">boolean</span></span> |
| <span data-ttu-id="daff1-152">ASCII\_char\_ptr</span><span class="sxs-lookup"><span data-stu-id="daff1-152">ascii\_char\_ptr</span></span> |<span data-ttu-id="daff1-153">ASCII dizesi</span><span class="sxs-lookup"><span data-stu-id="daff1-153">ASCII string</span></span> |
| <span data-ttu-id="daff1-154">EDM\_TARİH\_ZAMAN\_UZAKLIĞI</span><span class="sxs-lookup"><span data-stu-id="daff1-154">EDM\_DATE\_TIME\_OFFSET</span></span> |<span data-ttu-id="daff1-155">Tarih Saat farkı</span><span class="sxs-lookup"><span data-stu-id="daff1-155">date time offset</span></span> |
| <span data-ttu-id="daff1-156">EDM\_GUID</span><span class="sxs-lookup"><span data-stu-id="daff1-156">EDM\_GUID</span></span> |<span data-ttu-id="daff1-157">GUID</span><span class="sxs-lookup"><span data-stu-id="daff1-157">GUID</span></span> |
| <span data-ttu-id="daff1-158">EDM\_İKİLİ</span><span class="sxs-lookup"><span data-stu-id="daff1-158">EDM\_BINARY</span></span> |<span data-ttu-id="daff1-159">İkili</span><span class="sxs-lookup"><span data-stu-id="daff1-159">binary</span></span> |
| <span data-ttu-id="daff1-160">BİLDİRME\_YAPISI</span><span class="sxs-lookup"><span data-stu-id="daff1-160">DECLARE\_STRUCT</span></span> |<span data-ttu-id="daff1-161">karmaşık veri türü</span><span class="sxs-lookup"><span data-stu-id="daff1-161">complex data type</span></span> |

<span data-ttu-id="daff1-162">Merhaba son veri türüyle başlayalım.</span><span class="sxs-lookup"><span data-stu-id="daff1-162">Let’s start with hello last data type.</span></span> <span data-ttu-id="daff1-163">Merhaba **DECLARE\_YAPISI** hello gruplandırmaları olan toodefine karmaşık veri türlerini başka ilkel türler sağlar.</span><span class="sxs-lookup"><span data-stu-id="daff1-163">hello **DECLARE\_STRUCT** allows you toodefine complex data types, which are groupings of hello other primitive types.</span></span> <span data-ttu-id="daff1-164">Bu gruplandırmalar bize toodefine şuna benzer bir model izin ver:</span><span class="sxs-lookup"><span data-stu-id="daff1-164">These groupings allow us toodefine a model that looks like this:</span></span>

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

<span data-ttu-id="daff1-165">Bir tek veri olayı türü modelimizi içeriyor **TestType**.</span><span class="sxs-lookup"><span data-stu-id="daff1-165">Our model contains a single data event of type **TestType**.</span></span> <span data-ttu-id="daff1-166">**TestType** topluca hello ilkel türler hello tarafından desteklenen gösteren birkaç üyeleri içeren karmaşık bir tür **seri hale getirici** model oluşturma dili.</span><span class="sxs-lookup"><span data-stu-id="daff1-166">**TestType** is a complex type that includes several members, which collectively demonstrate hello primitive types supported by hello **serializer** modeling language.</span></span>

<span data-ttu-id="daff1-167">Bir modelin bu şekilde size kod toosend veri tooIoT aşağıdaki gibi görünür Hub yazabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="daff1-167">With a model like this, we can write code toosend data tooIoT Hub that appears as follows:</span></span>

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

<span data-ttu-id="daff1-168">Temel olarak, biz hello değeri tooevery üyesi atama **Test** yapısı ve ardından çağırma **SendAsync** toosend hello **Test** veri olay toohello bulut.</span><span class="sxs-lookup"><span data-stu-id="daff1-168">Basically, we’re assigning a value tooevery member of hello **Test** structure and then calling **SendAsync** toosend hello **Test** data event toohello cloud.</span></span> <span data-ttu-id="daff1-169">**SendAsync** bir tek veri olay tooIoT Hub gönderir yardımcı işlevdir:</span><span class="sxs-lookup"><span data-stu-id="daff1-169">**SendAsync** is a helper function that sends a single data event tooIoT Hub:</span></span>

```
void SendAsync(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const void *dataEvent)
{
    unsigned char* destination;
    size_t destinationSize;
    if (SERIALIZE(&destination, &destinationSize, *(const unsigned char*)dataEvent) ==
    {
        // null terminate hello string
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

<span data-ttu-id="daff1-170">Bu işlev veri olayı verilen hello serileştirir ve tooIoT Hub gönderir kullanarak **IoTHubClient\_SendEventAsync**.</span><span class="sxs-lookup"><span data-stu-id="daff1-170">This function serializes hello given data event and sends it tooIoT Hub using **IoTHubClient\_SendEventAsync**.</span></span> <span data-ttu-id="daff1-171">Aynı kodu önceki makalelerinde açıklanan hello budur (**SendAsync** hello mantığı kullanışlı bir işlevdeki yalıtır).</span><span class="sxs-lookup"><span data-stu-id="daff1-171">This is hello same code discussed in previous articles (**SendAsync** encapsulates hello logic into a convenient function).</span></span>

<span data-ttu-id="daff1-172">Merhaba önceki kod içinde kullanılan bir diğer yardımcı işlevdir **GetDateTimeOffset**.</span><span class="sxs-lookup"><span data-stu-id="daff1-172">One other helper function used in hello previous code is **GetDateTimeOffset**.</span></span> <span data-ttu-id="daff1-173">Bu işlev saat türünde bir değer verilen hello dönüştüren **EDM\_tarih\_zaman\_UZAKLIĞI**:</span><span class="sxs-lookup"><span data-stu-id="daff1-173">This function transforms hello given time into a value of type **EDM\_DATE\_TIME\_OFFSET**:</span></span>

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

<span data-ttu-id="daff1-174">Bu kodu çalıştırmak, iletiden hello tooIoT Hub gönderilir:</span><span class="sxs-lookup"><span data-stu-id="daff1-174">If you run this code, hello following message is sent tooIoT Hub:</span></span>

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

<span data-ttu-id="daff1-175">Merhaba serileştirme hello tarafından oluşturulan hello biçimi JSON olduğuna dikkat edin **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="daff1-175">Note that hello serialization is JSON, which is hello format generated by hello **serializer** library.</span></span> <span data-ttu-id="daff1-176">Ayrıca her bir üyesi hello JSON nesnesi seri Not hello hello üyeleri eşleşen **TestType** biz bizim modelde tanımlanmış.</span><span class="sxs-lookup"><span data-stu-id="daff1-176">Also note that each member of hello serialized JSON object matches hello members of hello **TestType** that we defined in our model.</span></span> <span data-ttu-id="daff1-177">Merhaba değerleri de tam olarak hello kod içinde kullanılan eşleştiğinden.</span><span class="sxs-lookup"><span data-stu-id="daff1-177">hello values also exactly match those used in hello code.</span></span> <span data-ttu-id="daff1-178">Ancak, hello ikili veriler base64 ile kodlanmış olduğuna dikkat edin: olan "AQID" hello, base64 kodlaması {0x01, 0x02, 0x03}.</span><span class="sxs-lookup"><span data-stu-id="daff1-178">However, note that hello binary data is base64-encoded: "AQID" is hello base64 encoding of {0x01, 0x02, 0x03}.</span></span>

<span data-ttu-id="daff1-179">Bu örnek hello kullanarak hello avantajı gösterir **seri hale getirici** kitaplığı--bize toosend JSON toohello bulut uygulamamız serileştirmede uğraşmanız tooexplicitly gerek kalmadan etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="daff1-179">This example demonstrates hello advantage of using hello **serializer** library -- it enables us toosend JSON toohello cloud, without having tooexplicitly deal with serialization in our application.</span></span> <span data-ttu-id="daff1-180">Tüm ilgili tooworry sahip olduğumuz ayarlanması hello başlangıç değerleri veri olaylarını modelimizi ve ardından bu olayları toohello bulut basit API'ler toosend çağırma.</span><span class="sxs-lookup"><span data-stu-id="daff1-180">All we have tooworry about is setting hello values of hello data events in our model and then calling simple APIs toosend those events toohello cloud.</span></span>

<span data-ttu-id="daff1-181">Bu bilgi ile biz hello aralığı (biz bile başka karmaşık türler içindeki karmaşık tür dahil olabilir) karmaşık türleri dahil olmak üzere desteklenen veri türlerini içeren modellerinin tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daff1-181">With this information, we can define models that include hello range of supported data types, including complex types (we could even include complex types within other complex types).</span></span> <span data-ttu-id="daff1-182">Ancak, kendisinin oluşturulan JSON seri hale getirilmiş tarafından hello yukarıdaki örnekte önemli noktanız getirir.</span><span class="sxs-lookup"><span data-stu-id="daff1-182">However, he serialized JSON generated by hello example above brings up an important point.</span></span> <span data-ttu-id="daff1-183">*Nasıl* size hello verilerle göndereceğiz **seri hale getirici** kitaplığı belirler tam olarak nasıl hello JSON biçimi.</span><span class="sxs-lookup"><span data-stu-id="daff1-183">*How* we send data with hello **serializer** library determines exactly how hello JSON is formed.</span></span> <span data-ttu-id="daff1-184">Bu belirli ne şu sonraki konulara değineceğiz noktasıdır.</span><span class="sxs-lookup"><span data-stu-id="daff1-184">That particular point is what we'll cover next.</span></span>

## <a name="more-about-serialization"></a><span data-ttu-id="daff1-185">Seri hale getirme hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="daff1-185">More about serialization</span></span>
<span data-ttu-id="daff1-186">Merhaba önceki bölümde vurgular hello tarafından oluşturulan bir hello çıkış **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="daff1-186">hello previous section highlights an example of hello output generated by hello **serializer** library.</span></span> <span data-ttu-id="daff1-187">Bu bölümde, nasıl hello kitaplığı veri serileştirir ve hello serileştirme API'leri kullanılarak bu davranışı nasıl kontrol edebilir açıklayacağız.</span><span class="sxs-lookup"><span data-stu-id="daff1-187">In this section, we'll explain how hello library serializes data and how you can control that behavior using hello serialization APIs.</span></span>

<span data-ttu-id="daff1-188">Sipariş tooadvance hello tartışmada üzerinde seri hale getirme, biz thermostat üzerinde temel alan yeni bir modeli çalışmak.</span><span class="sxs-lookup"><span data-stu-id="daff1-188">In order tooadvance hello discussion on serialization, we'll work with a new model based on a thermostat.</span></span> <span data-ttu-id="daff1-189">İlk olarak, şimdi bazı arka plan sağlamak hello senaryosunda biz tooaddress çalıştığınız.</span><span class="sxs-lookup"><span data-stu-id="daff1-189">First, let's provide some background on hello scenario we're trying tooaddress.</span></span>

<span data-ttu-id="daff1-190">Toomodel sıcaklık ve nem ölçer thermostat istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="daff1-190">We want toomodel a thermostat that measures temperature and humidity.</span></span> <span data-ttu-id="daff1-191">Her veri parçası tooIoT Hub farklı gönderilen toobe geçiyor.</span><span class="sxs-lookup"><span data-stu-id="daff1-191">Each piece of data is going toobe sent tooIoT Hub differently.</span></span> <span data-ttu-id="daff1-192">Varsayılan olarak, her iki dakikada bir sıcaklık olay thermostat ingresses hello; bir nem her 15 dakikada ingressed olayıdır.</span><span class="sxs-lookup"><span data-stu-id="daff1-192">By default, hello thermostat ingresses a temperature event once every 2 minutes; a humidity event is ingressed once every 15 minutes.</span></span> <span data-ttu-id="daff1-193">Ya da olay ingressed olduğunda, o hello karşılık gelen sıcaklık hello saati gösteren bir zaman damgası içermelidir veya nem ölçülür.</span><span class="sxs-lookup"><span data-stu-id="daff1-193">When either event is ingressed, it must include a timestamp that shows hello time that hello corresponding temperature or humidity was measured.</span></span>

<span data-ttu-id="daff1-194">Bu senaryo verildiğinde, şu iki farklı şekilde toomodel hello veri göstermek ve modelleme çıktı hello üzerinde serileştirilmiş hello etkisi açıklayacağız.</span><span class="sxs-lookup"><span data-stu-id="daff1-194">Given this scenario, we'll demonstrate two different ways toomodel hello data, and we'll explain hello effect that modeling has on hello serialized output.</span></span>

### <a name="model-1"></a><span data-ttu-id="daff1-195">Model 1</span><span class="sxs-lookup"><span data-stu-id="daff1-195">Model 1</span></span>
<span data-ttu-id="daff1-196">Merhaba ilk sürüm destekler önceki senaryoda hello bir modelin şöyledir:</span><span class="sxs-lookup"><span data-stu-id="daff1-196">Here's hello first version of a model that supports hello previous scenario:</span></span>

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

<span data-ttu-id="daff1-197">Not hello modelin iki veri olaylarını içerir: **sıcaklık** ve **nem**.</span><span class="sxs-lookup"><span data-stu-id="daff1-197">Note that hello model includes two data events: **Temperature** and **Humidity**.</span></span> <span data-ttu-id="daff1-198">Önceki örneklerde farklı olarak, her olayın hello türü kullanılarak tanımlanan bir yapıdır **DECLARE\_YAPISI**.</span><span class="sxs-lookup"><span data-stu-id="daff1-198">Unlike previous examples, hello type of each event is a structure defined using **DECLARE\_STRUCT**.</span></span> <span data-ttu-id="daff1-199">**TemperatureEvent** ısı ölçümü ve zaman damgası; içerir **HumidityEvent** nem ölçümü ve zaman damgası içeriyor.</span><span class="sxs-lookup"><span data-stu-id="daff1-199">**TemperatureEvent** includes a temperature measurement and a timestamp; **HumidityEvent** contains a humidity measurement and a timestamp.</span></span> <span data-ttu-id="daff1-200">Bu model, bize yukarıda açıklanan hello senaryosu için doğal şekilde toomodel hello veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="daff1-200">This model gives us a natural way toomodel hello data for hello scenario described above.</span></span> <span data-ttu-id="daff1-201">Biz bir olay toohello bulut gönderdiğinizde, ya da sıcaklık/zaman damgası veya bir nem/zaman damgası çifti göndereceğiz.</span><span class="sxs-lookup"><span data-stu-id="daff1-201">When we send an event toohello cloud, we'll either send a temperature/timestamp or a humidity/timestamp pair.</span></span>

<span data-ttu-id="daff1-202">Merhaba aşağıdaki gibi kod kullanarak bir sıcaklık olay toohello bulut gönderebiliriz:</span><span class="sxs-lookup"><span data-stu-id="daff1-202">We can send a temperature event toohello cloud using code such as hello following:</span></span>

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

<span data-ttu-id="daff1-203">Biz sabit kodlanmış değerler sıcaklık ve nem hello örnek kodda kullanır, ancak biz aslında bu değerleri hello karşılık gelen algılayıcı hello thermostat üzerinde örnekleyerek alma olduğunu düşünün.</span><span class="sxs-lookup"><span data-stu-id="daff1-203">We'll use hard-coded values for temperature and humidity in hello sample code, but imagine that we’re actually retrieving these values by sampling hello corresponding sensors on hello thermostat.</span></span>

<span data-ttu-id="daff1-204">Yukarıdaki Hello kod kullanan hello **GetDateTimeOffset** önceden sunulan Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="daff1-204">hello code above uses hello **GetDateTimeOffset** helper that was introduced previously.</span></span> <span data-ttu-id="daff1-205">Clear sonraki olacak nedeniyle, bu kod açıkça seri hale getirme ve hello olay gönderme hello görevi ayırır.</span><span class="sxs-lookup"><span data-stu-id="daff1-205">For reasons that will become clear later, this code explicitly separates hello task of serializing and sending hello event.</span></span> <span data-ttu-id="daff1-206">Merhaba önceki kod hello sıcaklık olay bir arabelleğe serileştirir.</span><span class="sxs-lookup"><span data-stu-id="daff1-206">hello previous code serializes hello temperature event into a buffer.</span></span> <span data-ttu-id="daff1-207">Ardından, **sendMessage** yardımcı işlevi (dahil **simplesample\_amqp**) gönderir olay tooIoT Hub hello:</span><span class="sxs-lookup"><span data-stu-id="daff1-207">Then, **sendMessage** is a helper function (included in **simplesample\_amqp**) that sends hello event tooIoT Hub:</span></span>

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

<span data-ttu-id="daff1-208">Bu kod hello alt kümesidir **SendAsync** biz üzerine yeniden buraya gidin olmaz şekilde hello önceki bölümde açıklanan Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="daff1-208">This code is a subset of hello **SendAsync** helper described in hello previous section, so we won’t go over it again here.</span></span>

<span data-ttu-id="daff1-209">Biz hello önceki kod toosend hello sıcaklık olay çalıştırdığınızda, bu serileştirilmiş formu hello olayın tooIoT Hub gönderilir:</span><span class="sxs-lookup"><span data-stu-id="daff1-209">When we run hello previous code toosend hello Temperature event, this serialized form of hello event is sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="daff1-210">Biz türü olan bir sıcaklık gönderiyorsanız **TemperatureEvent** ve bu yapı içeren bir **sıcaklık** ve **zaman** üyesi.</span><span class="sxs-lookup"><span data-stu-id="daff1-210">We're sending a temperature which is of type **TemperatureEvent** and that struct contains a **Temperature** and **Time** member.</span></span> <span data-ttu-id="daff1-211">Bu, doğrudan serileştirilmiş hello verilerde yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="daff1-211">This is directly reflected in hello serialized data.</span></span>

<span data-ttu-id="daff1-212">Benzer şekilde, biz bu kodu nem olayla gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="daff1-212">Similarly, we can send a humidity event with this code:</span></span>

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="daff1-213">tooIoT Hub gönderdi serileştirilmiş hello form aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="daff1-213">hello serialized form that’s sent tooIoT Hub appears as follows:</span></span>

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="daff1-214">Yeniden, bu beklenen biçimde değil.</span><span class="sxs-lookup"><span data-stu-id="daff1-214">Again, this is as expected.</span></span>

<span data-ttu-id="daff1-215">Bu model ile nasıl ek olaylar hayal edebildiğiniz kolayca eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="daff1-215">With this model, you can imagine how additional events can easily be added.</span></span> <span data-ttu-id="daff1-216">Kullanarak daha fazla yapıları tanımladığınız **DECLARE\_YAPISI**ve hello modelinde hello karşılık gelen olay dahil **ile\_veri**.</span><span class="sxs-lookup"><span data-stu-id="daff1-216">You define more structures using **DECLARE\_STRUCT**, and include hello corresponding event in hello model using **WITH\_DATA**.</span></span>

<span data-ttu-id="daff1-217">Şimdi, hello içeren hello modeli değiştirelim aynı veri ancak farklı bir yapıya sahip.</span><span class="sxs-lookup"><span data-stu-id="daff1-217">Now, let’s modify hello model so that it includes hello same data but with a different structure.</span></span>

### <a name="model-2"></a><span data-ttu-id="daff1-218">Model 2</span><span class="sxs-lookup"><span data-stu-id="daff1-218">Model 2</span></span>
<span data-ttu-id="daff1-219">Bu alternatif modeli toohello biri yukarıdaki göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="daff1-219">Consider this alternative model toohello one above:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="daff1-220">Bu durumda biz hello olmadığı anlaşılmış olur **DECLARE\_YAPISI** makroları ve yalnızca basit türler dil modelleme hello kullanarak senaryomuz hello veri öğeleri tanımlama.</span><span class="sxs-lookup"><span data-stu-id="daff1-220">In this case we've eliminated hello **DECLARE\_STRUCT** macros and are simply defining hello data items from our scenario using simple types from hello modeling language.</span></span>

<span data-ttu-id="daff1-221">Yalnızca hello şu anda şirketinizdeki hello Yoksay **zaman** olay.</span><span class="sxs-lookup"><span data-stu-id="daff1-221">Just for hello moment let’s ignore hello **Time** event.</span></span> <span data-ttu-id="daff1-222">Bu aralık ile Merhaba kod tooingress işte **sıcaklık**:</span><span class="sxs-lookup"><span data-stu-id="daff1-222">With that aside, here’s hello code tooingress **Temperature**:</span></span>

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

<span data-ttu-id="daff1-223">Bu kod, olay tooIoT Hub hello aşağıdaki serileştirilmiş gönderir:</span><span class="sxs-lookup"><span data-stu-id="daff1-223">This code sends hello following serialized event tooIoT Hub:</span></span>

```
{"Temperature":75}
```

<span data-ttu-id="daff1-224">Ve hello nem olay gönderme hello kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="daff1-224">And hello code for sending hello Humidity event appears as follows:</span></span>

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="daff1-225">Bu kod, bu tooIoT Hub gönderir:</span><span class="sxs-lookup"><span data-stu-id="daff1-225">This code sends this tooIoT Hub:</span></span>

```
{"Humidity":45}
```

<span data-ttu-id="daff1-226">Şu ana kadar var. yine de hiçbir beklenmeyen durumları.</span><span class="sxs-lookup"><span data-stu-id="daff1-226">So far there are still no surprises.</span></span> <span data-ttu-id="daff1-227">Şimdi hello SERİLEŞTİRME makrosu nasıl kullanırız değiştirelim.</span><span class="sxs-lookup"><span data-stu-id="daff1-227">Now let's change how we use hello SERIALIZE macro.</span></span>

<span data-ttu-id="daff1-228">Merhaba **SERİLEŞTİRME** makrosu bağımsız değişken birden çok veri olaylarını alabilir.</span><span class="sxs-lookup"><span data-stu-id="daff1-228">hello **SERIALIZE** macro can take multiple data events as arguments.</span></span> <span data-ttu-id="daff1-229">Bu bize tooserialize hello sağlar **sıcaklık** ve **nem** birlikte olay ve tek çağrıda tooIoT Hub gönderin:</span><span class="sxs-lookup"><span data-stu-id="daff1-229">This enables us tooserialize hello **Temperature** and **Humidity** event together and send them tooIoT Hub in one call:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="daff1-230">Bu kodun hello sonucunda iki veri olayları tooIoT Hub gönderilir olduğunu tahmin:</span><span class="sxs-lookup"><span data-stu-id="daff1-230">You might guess that hello result of this code is that two data events are sent tooIoT Hub:</span></span>

<span data-ttu-id="daff1-231">[</span><span class="sxs-lookup"><span data-stu-id="daff1-231">[</span></span>

<span data-ttu-id="daff1-232">{"Sıcaklık": 75},</span><span class="sxs-lookup"><span data-stu-id="daff1-232">{"Temperature":75},</span></span>

<span data-ttu-id="daff1-233">{"Nem": 45}</span><span class="sxs-lookup"><span data-stu-id="daff1-233">{"Humidity":45}</span></span>

<span data-ttu-id="daff1-234">]</span><span class="sxs-lookup"><span data-stu-id="daff1-234">]</span></span>

<span data-ttu-id="daff1-235">Diğer bir deyişle, bu kod olduğu Merhaba, aynı göndermek bekleyebilirsiniz **sıcaklık** ve **nem** ayrı olarak.</span><span class="sxs-lookup"><span data-stu-id="daff1-235">In other words, you might expect that this code is hello same as sending **Temperature** and **Humidity** separately.</span></span> <span data-ttu-id="daff1-236">Yalnızca kolaylık toopass olan iki olayları çok**SERİLEŞTİRME** hello aynı çağrı.</span><span class="sxs-lookup"><span data-stu-id="daff1-236">It’s just a convenience toopass both events too**SERIALIZE** in hello same call.</span></span> <span data-ttu-id="daff1-237">Ancak, bu hello durumda değil.</span><span class="sxs-lookup"><span data-stu-id="daff1-237">However, that’s not hello case.</span></span> <span data-ttu-id="daff1-238">Bunun yerine, yukarıdaki hello kod bu tek veri olay tooIoT Hub gönderir:</span><span class="sxs-lookup"><span data-stu-id="daff1-238">Instead, hello code above sends this single data event tooIoT Hub:</span></span>

<span data-ttu-id="daff1-239">{"Sıcaklık": 75 "nem": 45}</span><span class="sxs-lookup"><span data-stu-id="daff1-239">{"Temperature":75, "Humidity":45}</span></span>

<span data-ttu-id="daff1-240">Modelimizi tanımladığından Bu tuhaf görünebilir **sıcaklık** ve **nem** iki olarak *ayrı* olayları:</span><span class="sxs-lookup"><span data-stu-id="daff1-240">This may seem strange because our model defines **Temperature** and **Humidity** as two *separate* events:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="daff1-241">Daha fazla toohello noktası, biz bu olayları modelini alamadık nerede **sıcaklık** ve **nem** hello olan aynı yapısı:</span><span class="sxs-lookup"><span data-stu-id="daff1-241">More toohello point, we didn’t model these events where **Temperature** and **Humidity** are in hello same structure:</span></span>

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

<span data-ttu-id="daff1-242">Bu model kullansaydık, bunu daha kolay toounderstand nasıl olacaktır **sıcaklık** ve **nem** hello aynı serileştirilmiş ileti gönderilir.</span><span class="sxs-lookup"><span data-stu-id="daff1-242">If we used this model, it would be easier toounderstand how **Temperature** and **Humidity** would be sent in hello same serialized message.</span></span> <span data-ttu-id="daff1-243">Her iki veri olaylarını çok geçirdiğinizde bu şekilde çalıştığını neden ancak onu Temizle olmayabilir**SERİLEŞTİRME** kullanarak modeli 2.</span><span class="sxs-lookup"><span data-stu-id="daff1-243">However it may not be clear why it works that way when you pass both data events too**SERIALIZE** using model 2.</span></span>

<span data-ttu-id="daff1-244">Bu hello hello varsayımlar biliyorsanız, bu daha kolay toounderstand davranıştır **seri hale getirici** kitaplığı yapma.</span><span class="sxs-lookup"><span data-stu-id="daff1-244">This behavior is easier toounderstand if you know hello assumptions that hello **serializer** library is making.</span></span> <span data-ttu-id="daff1-245">Bu toomake duygusu geri tooour modeli edelim:</span><span class="sxs-lookup"><span data-stu-id="daff1-245">toomake sense of this let’s go back tooour model:</span></span>

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

<span data-ttu-id="daff1-246">Bu model nesne yönelimli koşullarında düşünün.</span><span class="sxs-lookup"><span data-stu-id="daff1-246">Think of this model in object-oriented terms.</span></span> <span data-ttu-id="daff1-247">Bu durumda biz fiziksel bir aygıtı (thermostat) modelleme ve o aygıtı gibi özniteliklerini içerir **sıcaklık** ve **nem**.</span><span class="sxs-lookup"><span data-stu-id="daff1-247">In this case we’re modeling a physical device (a thermostat) and that device includes attributes like **Temperature** and **Humidity**.</span></span>

<span data-ttu-id="daff1-248">Merhaba tüm modelimizi hello aşağıdaki gibi kod ile durumunu gönderebiliriz:</span><span class="sxs-lookup"><span data-stu-id="daff1-248">We can send hello entire state of our model with code such as hello following:</span></span>

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

<span data-ttu-id="daff1-249">Sıcaklık ve nem zaman Hello değerlerini ayarlamak varsayıldığında, bu gönderilen tooIoT Hub gibi bir olay görür:</span><span class="sxs-lookup"><span data-stu-id="daff1-249">Assuming hello values of Temperature, Humidity and Time are set, we would see an event like this sent tooIoT Hub:</span></span>

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="daff1-250">Bazen yalnızca toosend isteyebilirsiniz *bazı* (Bu, çok sayıda veri olaylarını modelinizi içeriyorsa, özellikle true) hello modeli toohello bulutun özelliklerini.</span><span class="sxs-lookup"><span data-stu-id="daff1-250">Sometimes you may only want toosend *some* properties of hello model toohello cloud (this is especially true if your model contains a large number of data events).</span></span> <span data-ttu-id="daff1-251">Yararlı toosend yalnızca bir alt veri olayların gibi önceki örneğimizde olmasından:</span><span class="sxs-lookup"><span data-stu-id="daff1-251">It’s useful toosend only a subset of data events, such as in our earlier example:</span></span>

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

<span data-ttu-id="daff1-252">Bu tam olarak hello oluşturur biz olarak tanımlanmışsa aynı olay serileştirilmiş bir **TemperatureEvent** ile bir **sıcaklık** ve **zaman** üye, biz ile 1 model gibi.</span><span class="sxs-lookup"><span data-stu-id="daff1-252">This generates exactly hello same serialized event as if we had defined a **TemperatureEvent** with a **Temperature** and **Time** member, just as we did with model 1.</span></span> <span data-ttu-id="daff1-253">Bu durumda tam olarak hello aynı serileştirilmiş olay biz adlı olduğundan farklı bir model (model 2) kullanarak mümkün toogenerate bulamadığımız **SERİLEŞTİRME** farklı bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="daff1-253">In this case we were able toogenerate exactly hello same serialized event by using a different model (model 2) because we called **SERIALIZE** in a different way.</span></span>

<span data-ttu-id="daff1-254">birden çok veri olaylarını çok geçirirseniz hello önemli nokta olan**SERİLEŞTİRME,** sonra her olay tek bir JSON nesnesi özelliğinde olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="daff1-254">hello important point is that if you pass multiple data events too**SERIALIZE,** then it assumes each event is a property in a single JSON object.</span></span>

<span data-ttu-id="daff1-255">Merhaba en iyi yaklaşımı, ve modelinizi hakkında nasıl düşündüğünüz bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="daff1-255">hello best approach depends on you and how you think about your model.</span></span> <span data-ttu-id="daff1-256">"Olayları" toohello bulut gönderiyorsanız ve her olay tanımlanmış bir özellik kümesi içeriyorsa, hello ilk yaklaşımı algılama çok hale getirir.</span><span class="sxs-lookup"><span data-stu-id="daff1-256">If you’re sending "events" toohello cloud and each event contains a defined set of properties, then hello first approach makes a lot of sense.</span></span> <span data-ttu-id="daff1-257">Bu durumda kullanacağınız **DECLARE\_YAPISI** toodefine hello her olay yapısını ve bunları modelinizi hello dahil **ile\_veri** makrosu.</span><span class="sxs-lookup"><span data-stu-id="daff1-257">In that case you would use **DECLARE\_STRUCT** toodefine hello structure of each event and then include them in your model with hello **WITH\_DATA** macro.</span></span> <span data-ttu-id="daff1-258">Merhaba ilk yukarıdaki örnekte yaptığımız gibi her olay gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daff1-258">Then you send each event as we did in hello first example above.</span></span> <span data-ttu-id="daff1-259">Bu yaklaşım, yalnızca bir tek veri olayı çok geçip geçmeyeceğini**seri hale GETİRİCİ**.</span><span class="sxs-lookup"><span data-stu-id="daff1-259">In this approach you would only pass a single data event too**SERIALIZER**.</span></span>

<span data-ttu-id="daff1-260">Nesne odaklı bir şekilde modelinizde hakkında düşünüyorsanız, hello ikinci yaklaşımın size uygun.</span><span class="sxs-lookup"><span data-stu-id="daff1-260">If you think about your model in an object-oriented fashion, then hello second approach may suit you.</span></span> <span data-ttu-id="daff1-261">Bu durumda, öğeleri kullanarak tanımlanan hello **ile\_veri** hello "" nesnenizin özelliklerdir.</span><span class="sxs-lookup"><span data-stu-id="daff1-261">In this case, hello elements defined using **WITH\_DATA** are hello "properties" of your object.</span></span> <span data-ttu-id="daff1-262">Hangi olayların alt kümesini çok geçirdiğiniz**SERİLEŞTİRME** istediğiniz, ne kadar "nesnesinin" durumuna bağlı olarak toosend toohello bulut istiyor.</span><span class="sxs-lookup"><span data-stu-id="daff1-262">You pass whatever subset of events too**SERIALIZE** that you like, depending on how much of your "object’s" state you want toosend toohello cloud.</span></span>

<span data-ttu-id="daff1-263">Doğru veya yanlış bir bağlanamadı yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="daff1-263">Nether approach is right or wrong.</span></span> <span data-ttu-id="daff1-264">Yalnızca nasıl ele aldığını da hello **seri hale getirici** kitaplığı çalışır ve gereksinimlerine en uygun çekme hello modelleme yaklaşım.</span><span class="sxs-lookup"><span data-stu-id="daff1-264">Just be aware of how hello **serializer** library works, and pick hello modeling approach that best fits your needs.</span></span>

## <a name="message-handling"></a><span data-ttu-id="daff1-265">İleti işleme</span><span class="sxs-lookup"><span data-stu-id="daff1-265">Message handling</span></span>
<span data-ttu-id="daff1-266">Şu ana kadar bu makalede, gönderen olaylar tooIoT Hub ele alınan yalnızca ve iletileri alma ele kurmadı.</span><span class="sxs-lookup"><span data-stu-id="daff1-266">So far this article has only discussed sending events tooIoT Hub, and hasn't addressed receiving messages.</span></span> <span data-ttu-id="daff1-267">Merhaba neden bu ne ihtiyacımız olan için ileti alma hakkında tooknow büyük ölçüde içinde ele alınmış bir [önceki makalesi](iot-hub-device-sdk-c-intro.md).</span><span class="sxs-lookup"><span data-stu-id="daff1-267">hello reason for this is that what we need tooknow about receiving messages has largely been covered in an [earlier article](iot-hub-device-sdk-c-intro.md).</span></span> <span data-ttu-id="daff1-268">Bu makaleden bir ileti geri çağırma işlevini kaydederek iletileri işleme geri çağırma:</span><span class="sxs-lookup"><span data-stu-id="daff1-268">Recall from that article that you process messages by registering a message callback function:</span></span>

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

<span data-ttu-id="daff1-269">Ardından, bir ileti alındığında çağrılan hello geri çağırma işlevi de yazın:</span><span class="sxs-lookup"><span data-stu-id="daff1-269">You then write hello callback function that’s invoked when a message is received:</span></span>

```
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = EXECUTE_COMMAND_ERROR;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
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

<span data-ttu-id="daff1-270">Bu uygulaması, **IoTHubMessage** çağrıları hello modelinizdeki her eylem için belirli bir işlev.</span><span class="sxs-lookup"><span data-stu-id="daff1-270">This implementation of **IoTHubMessage** calls hello specific function for each action in your model.</span></span> <span data-ttu-id="daff1-271">Örneğin bu eylemi modelinizi tanımlar:</span><span class="sxs-lookup"><span data-stu-id="daff1-271">For example, if your model defines this action:</span></span>

```
WITH_ACTION(SetAirResistance, int, Position)
```

<span data-ttu-id="daff1-272">Bu imza işleviyle tanımlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="daff1-272">You must define a function with this signature:</span></span>

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

<span data-ttu-id="daff1-273">**SetAirResistance** tooyour cihaz bu ileti gönderildiğinde daha sonra çağrılır.</span><span class="sxs-lookup"><span data-stu-id="daff1-273">**SetAirResistance** is then called when that message is sent tooyour device.</span></span>

<span data-ttu-id="daff1-274">Ne biz açıklandığı henüz henüz hangi hello serileştirilmiş ileti görülüyor sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="daff1-274">What we haven't explained yet is what hello serialized version of message looks like.</span></span> <span data-ttu-id="daff1-275">Diğer bir deyişle, toosend istiyorsanız bir **SetAirResistance** ileti tooyour aygıt, ne görünüm ister?</span><span class="sxs-lookup"><span data-stu-id="daff1-275">In other words, if you want toosend a **SetAirResistance** message tooyour device, what does that look like?</span></span>

<span data-ttu-id="daff1-276">Bir ileti tooa aygıt gönderiyorsanız hello Azure IOT hizmeti SDK aracılığıyla bunu.</span><span class="sxs-lookup"><span data-stu-id="daff1-276">If you're sending a message tooa device, you would do so through hello Azure IoT service SDK.</span></span> <span data-ttu-id="daff1-277">Hala ne toosend tooinvoke belirli bir eylem dize tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="daff1-277">You still need tooknow what string toosend tooinvoke a particular action.</span></span> <span data-ttu-id="daff1-278">ileti gönderme için hello genel biçimi şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="daff1-278">hello general format for sending a message appears as follows:</span></span>

```
{"Name" : "", "Parameters" : "" }
```

<span data-ttu-id="daff1-279">Serileştirilmiş bir JSON nesnesi iki özellikleriyle gönderiyorsanız: **adı** hello eylemi (ileti) hello adıdır ve **parametreleri** bu eylemin hello parametrelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="daff1-279">You're sending a serialized JSON object with two properties: **Name** is hello name of hello action (message) and **Parameters** contains hello parameters of that action.</span></span>

<span data-ttu-id="daff1-280">Örneğin, tooinvoke **SetAirResistance** bu ileti tooa aygıt gönderebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="daff1-280">For example, tooinvoke **SetAirResistance** you can send this message tooa device:</span></span>

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

<span data-ttu-id="daff1-281">Merhaba eylem adı, modelde tanımlanan bir eylem tam olarak eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="daff1-281">hello action name must exactly match an action defined in your model.</span></span> <span data-ttu-id="daff1-282">Merhaba parametre adları de eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="daff1-282">hello parameter names must match as well.</span></span> <span data-ttu-id="daff1-283">Ayrıca, büyük küçük harfe duyarlılığın unutmayın.</span><span class="sxs-lookup"><span data-stu-id="daff1-283">Also note case sensitivity.</span></span> <span data-ttu-id="daff1-284">**Ad** ve **parametreleri** her zaman büyük harfle yazılır.</span><span class="sxs-lookup"><span data-stu-id="daff1-284">**Name** and **Parameters** are always uppercase.</span></span> <span data-ttu-id="daff1-285">Eylem adı ve parametreleri emin toomatch hello durumunda modelinizde olun.</span><span class="sxs-lookup"><span data-stu-id="daff1-285">Make sure toomatch hello case of your action name and parameters in your model.</span></span> <span data-ttu-id="daff1-286">Bu örnekte, hello eylem adı "SetAirResistance" değil "setairresistance" ise.</span><span class="sxs-lookup"><span data-stu-id="daff1-286">In this example, hello action name is "SetAirResistance" and not "setairresistance".</span></span>

<span data-ttu-id="daff1-287">diğer iki eylem hello **TurnFanOn** ve **TurnFanOff** bu iletileri tooa aygıt göndererek çağrılır:</span><span class="sxs-lookup"><span data-stu-id="daff1-287">hello two other actions **TurnFanOn** and **TurnFanOff** can be invoked by sending these messages tooa device:</span></span>

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

<span data-ttu-id="daff1-288">Gereksinim duyduğunuz her şeyi tooknow iletileri ile olayları gönderme ve alma Merhaba, bu bölümde açıklanan **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="daff1-288">This section described everything you need tooknow when sending events and receiving messages with hello **serializer** library.</span></span> <span data-ttu-id="daff1-289">Devam etmeden önce şimdi ne kadar büyük modelinizi denetleyebilir yapılandırabileceğiniz bazı parametreler kapsar.</span><span class="sxs-lookup"><span data-stu-id="daff1-289">Before moving on, let's cover some parameters you can configure that control how large your model is.</span></span>

## <a name="macro-configuration"></a><span data-ttu-id="daff1-290">Makro yapılandırma</span><span class="sxs-lookup"><span data-stu-id="daff1-290">Macro configuration</span></span>
<span data-ttu-id="daff1-291">Merhaba kullanıyorsanız **seri hale getirici** hello SDK toobe farkında önemli bir kısmını hello azure-c-paylaşılan-yardımcı programı Kitaplığı'nda bulunan kitaplık.</span><span class="sxs-lookup"><span data-stu-id="daff1-291">If you’re using hello **Serializer** library an important part of hello SDK toobe aware of is found in hello azure-c-shared-utility library.</span></span>
<span data-ttu-id="daff1-292">Merhaba--özyinelemeli seçeneği kullanılarak GitHub hello Azure-IOT-sdk-c depodan klonlanmış varsa, bu paylaşılan yardımcı kitaplık yer alır:</span><span class="sxs-lookup"><span data-stu-id="daff1-292">If you have cloned hello Azure-iot-sdk-c repository from GitHub using hello --recursive option, then you will find this shared utility library here:</span></span>

```
.\\c-utility
```

<span data-ttu-id="daff1-293">Merhaba kitaplığı klonlanmış değil, bulabilirsiniz [burada](https://github.com/Azure/azure-c-shared-utility).</span><span class="sxs-lookup"><span data-stu-id="daff1-293">If you have not cloned hello library, you can find it [here](https://github.com/Azure/azure-c-shared-utility).</span></span>

<span data-ttu-id="daff1-294">Merhaba paylaşılan yardımcı kitaplıkta klasörü aşağıdaki hello bulacaksınız:</span><span class="sxs-lookup"><span data-stu-id="daff1-294">Within hello shared utility library, you will find hello following folder:</span></span>

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

<span data-ttu-id="daff1-295">Adlı bir Visual Studio çözümü bu klasörde **makrosu\_yardımcı programları\_h\_generator.sln**:</span><span class="sxs-lookup"><span data-stu-id="daff1-295">This folder contains a Visual Studio solution called **macro\_utils\_h\_generator.sln**:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

<span data-ttu-id="daff1-296">Bu çözümdeki Hello programın oluşturduğu hello **makrosu\_utils.h** dosya.</span><span class="sxs-lookup"><span data-stu-id="daff1-296">hello program in this solution generates hello **macro\_utils.h** file.</span></span> <span data-ttu-id="daff1-297">Varsayılan makrosu yoktur\_hello SDK ile bulunan utils.h dosyası.</span><span class="sxs-lookup"><span data-stu-id="daff1-297">There’s a default macro\_utils.h file included with hello SDK.</span></span> <span data-ttu-id="daff1-298">Bu çözüm bazı parametreler ve sonra yeniden oluşturun üstbilgi dosyası bu parametrelere göre hello toomodify sağlar.</span><span class="sxs-lookup"><span data-stu-id="daff1-298">This solution allows you toomodify some parameters and then recreate hello header file based on these parameters.</span></span>

<span data-ttu-id="daff1-299">Merhaba iki anahtar parametreleri toobe endişe ile **nArithmetic** ve **nMacroParameters** makro içinde bulunan bu iki satır içinde tanımlanan\_utils.tt:</span><span class="sxs-lookup"><span data-stu-id="daff1-299">hello two key parameters toobe concerned with are **nArithmetic** and **nMacroParameters** which are defined in these two lines found in macro\_utils.tt:</span></span>

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

<span data-ttu-id="daff1-300">Bu değerleri hello SDK ile dahil hello varsayılan parametreleridir.</span><span class="sxs-lookup"><span data-stu-id="daff1-300">These values are hello default parameters included with hello SDK.</span></span> <span data-ttu-id="daff1-301">Her bir parametreyi anlamı aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="daff1-301">Each parameter has hello following meaning:</span></span>

* <span data-ttu-id="daff1-302">nMacroParameters – denetimleri içinde bir DECLARE olabilir kaç parametreleri\_modeli makro tanımı.</span><span class="sxs-lookup"><span data-stu-id="daff1-302">nMacroParameters – Controls how many parameters you can have in one DECLARE\_MODEL macro definition.</span></span>
* <span data-ttu-id="daff1-303">nArithmetic – denetimleri hello toplam bir model izin üye sayısı.</span><span class="sxs-lookup"><span data-stu-id="daff1-303">nArithmetic – Controls hello total number of members allowed in a model.</span></span>

<span data-ttu-id="daff1-304">Bunlar denetlemek için bu parametreler önemli hello modelinizi ne kadar büyük olabilir nedenidir.</span><span class="sxs-lookup"><span data-stu-id="daff1-304">hello reason these parameters are important is because they control how large your model can be.</span></span> <span data-ttu-id="daff1-305">Örneğin, bu model tanımı göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="daff1-305">For example, consider this model definition:</span></span>

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

<span data-ttu-id="daff1-306">Daha önce belirtildiği gibi **DECLARE\_MODEL** yalnızca C makro.</span><span class="sxs-lookup"><span data-stu-id="daff1-306">As mentioned previously, **DECLARE\_MODEL** is just a C macro.</span></span> <span data-ttu-id="daff1-307">Merhaba hello modeli ve hello adları **ile\_veri** deyimi (henüz başka bir makrosu) olan parametrelerinin **DECLARE\_modeli**.</span><span class="sxs-lookup"><span data-stu-id="daff1-307">hello names of hello model and hello **WITH\_DATA** statement (yet another macro) are parameters of **DECLARE\_MODEL**.</span></span> <span data-ttu-id="daff1-308">**nMacroParameters** kaç parametreleri eklenebilir tanımlar **DECLARE\_modeli**.</span><span class="sxs-lookup"><span data-stu-id="daff1-308">**nMacroParameters** defines how many parameters can be included in **DECLARE\_MODEL**.</span></span> <span data-ttu-id="daff1-309">Etkili bir şekilde sağlayabilirsiniz kaç tane veri olay ve eylem bildirimleri tanımlar.</span><span class="sxs-lookup"><span data-stu-id="daff1-309">Effectively, this defines how many data event and action declarations you can have.</span></span> <span data-ttu-id="daff1-310">Bu nedenle, hello varsayılan sınırının 124 ile bu 60 eylemleri ve veri olayları birleşimi ile bir model tanımlayabilirsiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="daff1-310">As such, with hello default limit of 124 this means that you can define a model with a combination of about 60 actions and data events.</span></span> <span data-ttu-id="daff1-311">Bu sınır tooexceed çalışırsanız, benzer toothis Ara derleyici hataları alırsınız:</span><span class="sxs-lookup"><span data-stu-id="daff1-311">If you try tooexceed this limit, you'll receive compiler errors that look similar toothis:</span></span>

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

<span data-ttu-id="daff1-312">Merhaba **nArithmetic** parametredir uygulamanızı'den daha fazla hello iç işleyişini hello makro dili hakkında.</span><span class="sxs-lookup"><span data-stu-id="daff1-312">hello **nArithmetic** parameter is more about hello internal workings of hello macro language than your application.</span></span>  <span data-ttu-id="daff1-313">Merhaba toplam modelinizde, olabilir üye sayısı denetimleri de dahil olmak üzere **DECLARE_STRUCT** makroları.</span><span class="sxs-lookup"><span data-stu-id="daff1-313">It controls hello total number of members you can have in your model, including **DECLARE_STRUCT** macros.</span></span> <span data-ttu-id="daff1-314">Bu gibi derleyici hataları görmeye başlayacaksınız sonra artırmayı denemelisiniz **nArithmetic**:</span><span class="sxs-lookup"><span data-stu-id="daff1-314">If you start seeing compiler errors such as this, then you should try increasing **nArithmetic**:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

<span data-ttu-id="daff1-315">Bu parametreler toochange istiyorsanız, hello makrosu hello değerleri değiştirin\_utils.tt dosyası, yeniden derleyebilirsiniz hello makrosu\_yardımcı programları\_h\_generator.sln çözüm ve çalışma hello derlenmiş program.</span><span class="sxs-lookup"><span data-stu-id="daff1-315">If you want toochange these parameters, modify hello values in hello macro\_utils.tt file, recompile hello macro\_utils\_h\_generator.sln solution, and run hello compiled program.</span></span> <span data-ttu-id="daff1-316">Bunu yaptığınızda bunu yeni bir makro\_utils.h dosya oluşturulur ve hello yerleştirilir.\\ Ortak\\Inc dizini.</span><span class="sxs-lookup"><span data-stu-id="daff1-316">When you do so, a new macro\_utils.h file is generated and placed in hello .\\common\\inc directory.</span></span>

<span data-ttu-id="daff1-317">Sipariş toouse hello yeni sürümünde makrosu\_utils.h, Kaldır hello **seri hale getirici** NuGet paketi çözümünüzden ve onun yerine dahil hello **seri hale getirici** Visual Studio projesi.</span><span class="sxs-lookup"><span data-stu-id="daff1-317">In order toouse hello new version of macro\_utils.h, remove hello **serializer** NuGet package from your solution and in its place include hello **serializer** Visual Studio project.</span></span> <span data-ttu-id="daff1-318">Bu, kod toocompile hello kaynak kodu hello seri hale getirici kitaplığının karşı sağlar.</span><span class="sxs-lookup"><span data-stu-id="daff1-318">This enables your code toocompile against hello source code of hello serializer library.</span></span> <span data-ttu-id="daff1-319">Bu güncelleştirilmiş hello makrosu içerir\_utils.h.</span><span class="sxs-lookup"><span data-stu-id="daff1-319">This includes hello updated macro\_utils.h.</span></span> <span data-ttu-id="daff1-320">Bunun için toodo istiyorsanız **simplesample\_amqp**, hello çözümden hello NuGet paketi hello seri hale getirici kitaplığı kaldırarak Başlat:</span><span class="sxs-lookup"><span data-stu-id="daff1-320">If you want toodo this for **simplesample\_amqp**, start by removing hello NuGet package for hello serializer library from hello solution:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

<span data-ttu-id="daff1-321">Daha sonra bu proje tooyour Visual Studio çözümü ekleyin:</span><span class="sxs-lookup"><span data-stu-id="daff1-321">Then add this project tooyour Visual Studio solution:</span></span>

> <span data-ttu-id="daff1-322">. \\c\\seri hale getirici\\yapı\\windows\\serializer.vcxproj</span><span class="sxs-lookup"><span data-stu-id="daff1-322">.\\c\\serializer\\build\\windows\\serializer.vcxproj</span></span>
> 
> 

<span data-ttu-id="daff1-323">İşiniz bittiğinde, çözümünüzün aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="daff1-323">When you're done, your solution should look like this:</span></span>

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

<span data-ttu-id="daff1-324">Ne zaman, çözümünüz hello derleme makro güncelleştirilmiş artık\_utils.h ikili dosyanız yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="daff1-324">Now when you compile your solution, hello updated macro\_utils.h is included in your binary.</span></span>

<span data-ttu-id="daff1-325">Bu değerleri yeterince artırma derleyici sınırları aşabilir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="daff1-325">Note that increasing these values high enough can exceed compiler limits.</span></span> <span data-ttu-id="daff1-326">toothis noktası hello **nMacroParameters** ilgilenen hangi toobe ile Merhaba ana parametresidir.</span><span class="sxs-lookup"><span data-stu-id="daff1-326">toothis point, hello **nMacroParameters** is hello main parameter with which toobe concerned.</span></span> <span data-ttu-id="daff1-327">Merhaba C99 spec 127 parametreleri en az bir makro tanımı'nda verilir belirtir.</span><span class="sxs-lookup"><span data-stu-id="daff1-327">hello C99 spec specifies that a minimum of 127 parameters are allowed in a macro definition.</span></span> <span data-ttu-id="daff1-328">Merhaba Microsoft derleyici hello spec tam olarak aşağıdaki (ve 127 sınırı) mümkün tooincrease olmayacaktır **nMacroParameters** hello varsayılan ötesinde.</span><span class="sxs-lookup"><span data-stu-id="daff1-328">hello Microsoft compiler follows hello spec exactly (and has a limit of 127), so you won't be able tooincrease **nMacroParameters** beyond hello default.</span></span> <span data-ttu-id="daff1-329">Diğer derleyiciler toodo şekilde izin vermiyor olabilir (örneğin, daha yüksek bir sınır hello GNU derleyici destekler).</span><span class="sxs-lookup"><span data-stu-id="daff1-329">Other compilers might allow you toodo so (for example, hello GNU compiler supports a higher limit).</span></span>

<span data-ttu-id="daff1-330">Şu ana kadar biz neredeyse tooknow nasıl toowrite kod hello ile ilgili ihtiyaç duyduğunuz her şeyi kapsamdaki **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="daff1-330">So far we've covered just about everything you need tooknow about how toowrite code with hello **serializer** library.</span></span> <span data-ttu-id="daff1-331">Tamamlanırken önce şimdi bazı konular hakkında merak ediyor önceki makalelerden yeniden ziyaret.</span><span class="sxs-lookup"><span data-stu-id="daff1-331">Before concluding, let's revisit some topics from previous articles that you may be wondering about.</span></span>

## <a name="hello-lower-level-apis"></a><span data-ttu-id="daff1-332">Merhaba düşük düzeyli API'leri</span><span class="sxs-lookup"><span data-stu-id="daff1-332">hello lower-level APIs</span></span>
<span data-ttu-id="daff1-333">Bu makale üzerinde odaklanmış hello örnek uygulama **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="daff1-333">hello sample application on which this article focused is **simplesample\_amqp**.</span></span> <span data-ttu-id="daff1-334">Bu örnek hello üst düzey (Merhaba olmayan-"tümü") API'leri toosend olayları kullanır ve iletileri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daff1-334">This sample uses hello higher-level (hello non-"LL") APIs toosend events and receive messages.</span></span> <span data-ttu-id="daff1-335">Bu API'leri kullanırsanız, hem olayları ileti gönderme ve alma, mvc'deki bir arka plan iş parçacığı çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="daff1-335">If you use these APIs, a background thread runs which takes care of both sending events and receiving messages.</span></span> <span data-ttu-id="daff1-336">Ancak, bu arka plan iş parçacığı hello alt düzey (Tümü) API'leri tooeliminate kullanın ve açık denetim olayları gönderirken veya hello buluttan iletilerini gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="daff1-336">However, you can use hello lower-level (LL) APIs tooeliminate this background thread and take explicit control over when you send events or receive messages from hello cloud.</span></span>

<span data-ttu-id="daff1-337">Bölümünde açıklandığı gibi bir [önceki makale](iot-hub-device-sdk-c-iothubclient.md), Merhaba oluşan bir dizi işlevleri yoktur üst düzey API'leri:</span><span class="sxs-lookup"><span data-stu-id="daff1-337">As described in a [previous article](iot-hub-device-sdk-c-iothubclient.md), there is a set of functions that consists of hello higher-level APIs:</span></span>

* <span data-ttu-id="daff1-338">IoTHubClient\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="daff1-338">IoTHubClient\_CreateFromConnectionString</span></span>
* <span data-ttu-id="daff1-339">IoTHubClient\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="daff1-339">IoTHubClient\_SendEventAsync</span></span>
* <span data-ttu-id="daff1-340">IoTHubClient\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="daff1-340">IoTHubClient\_SetMessageCallback</span></span>
* <span data-ttu-id="daff1-341">IoTHubClient\_yok</span><span class="sxs-lookup"><span data-stu-id="daff1-341">IoTHubClient\_Destroy</span></span>

<span data-ttu-id="daff1-342">Bu API'leri örneklerde gösterildiği **simplesample\_amqp**.</span><span class="sxs-lookup"><span data-stu-id="daff1-342">These APIs are demonstrated in **simplesample\_amqp**.</span></span>

<span data-ttu-id="daff1-343">Ayrıca vardır benzer bir alt düzey API kümesi.</span><span class="sxs-lookup"><span data-stu-id="daff1-343">There is also an analogous set of lower-level APIs.</span></span>

* <span data-ttu-id="daff1-344">IoTHubClient\_ÜM\_CreateFromConnectionString</span><span class="sxs-lookup"><span data-stu-id="daff1-344">IoTHubClient\_LL\_CreateFromConnectionString</span></span>
* <span data-ttu-id="daff1-345">IoTHubClient\_ÜM\_SendEventAsync</span><span class="sxs-lookup"><span data-stu-id="daff1-345">IoTHubClient\_LL\_SendEventAsync</span></span>
* <span data-ttu-id="daff1-346">IoTHubClient\_ÜM\_SetMessageCallback</span><span class="sxs-lookup"><span data-stu-id="daff1-346">IoTHubClient\_LL\_SetMessageCallback</span></span>
* <span data-ttu-id="daff1-347">IoTHubClient\_ÜM\_yok</span><span class="sxs-lookup"><span data-stu-id="daff1-347">IoTHubClient\_LL\_Destroy</span></span>

<span data-ttu-id="daff1-348">Merhaba düşük düzeyli API'leri iş tam olarak aynı şekilde hello önceki makalelerinde açıklandığı gibi hello olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="daff1-348">Note that hello lower-level APIs work exactly hello same way as described in hello previous articles.</span></span> <span data-ttu-id="daff1-349">İleti olayları gönderme ve alma bir arka plan iş parçacığı toohandle istiyorsanız hello ilk API kümesi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daff1-349">You can use hello first set of APIs if you want a background thread toohandle sending events and receiving messages.</span></span> <span data-ttu-id="daff1-350">Açık denetim zaman göndermek ve IOT Hub'ından veri almak istiyorsanız, hello ikinci API kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="daff1-350">You use hello second set of APIs if you want explicit control over when you send and receive data from IoT Hub.</span></span> <span data-ttu-id="daff1-351">API iş ayarlayın ya da eşit ile Merhaba yanı sıra **seri hale getirici** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="daff1-351">Either set of APIs work equally well with hello **serializer** library.</span></span>

<span data-ttu-id="daff1-352">Nasıl bir örneği için hello düşük düzeyli API'leri ile Merhaba kullanılan **seri hale getirici** kitaplığı hello bkz **simplesample\_http** uygulama.</span><span class="sxs-lookup"><span data-stu-id="daff1-352">For an example of how hello lower-level APIs are used with hello **serializer** library, see hello **simplesample\_http** application.</span></span>

## <a name="additional-topics"></a><span data-ttu-id="daff1-353">Ek konu başlıkları</span><span class="sxs-lookup"><span data-stu-id="daff1-353">Additional topics</span></span>
<span data-ttu-id="daff1-354">Söz değerinde birkaç diğer yeniden işleme, diğer aygıt kimlik bilgisi ve yapılandırma seçeneklerini kullanarak özellik konulardır.</span><span class="sxs-lookup"><span data-stu-id="daff1-354">A few other topics worth mentioning again are property handling, using alternate device credentials, and configuration options.</span></span> <span data-ttu-id="daff1-355">Tüm konuları ele bunlar bir [önceki makalede](iot-hub-device-sdk-c-iothubclient.md).</span><span class="sxs-lookup"><span data-stu-id="daff1-355">These are all topics covered in a [previous article](iot-hub-device-sdk-c-iothubclient.md).</span></span> <span data-ttu-id="daff1-356">Merhaba ana bu özelliklerin tümü, hello aynı çalıştığını noktasıdır hello işlemleriyle **seri hale getirici** kitaplığı ile Merhaba göründükleri **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="daff1-356">hello main point is that all of these features work in hello same way with hello **serializer** library as they do with hello **IoTHubClient** library.</span></span> <span data-ttu-id="daff1-357">Örneğin, modelinizin dışında tooattach özellikleri tooan olay istiyorsanız, kullandığınız **IoTHubMessage\_özellikleri** ve **harita**\_**örnek**, aynı şekilde daha önce açıklandığı gibi hello:</span><span class="sxs-lookup"><span data-stu-id="daff1-357">For example, if you want tooattach properties tooan event from your model, you use **IoTHubMessage\_Properties** and **Map**\_**AddorUpdate**, hello same way as described previously:</span></span>

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

<span data-ttu-id="daff1-358">Merhaba olay hello olup oluşturulan **seri hale getirici** kitaplığı veya hello kullanarak el ile oluşturulan **IoTHubClient** kitaplığı önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="daff1-358">Whether hello event was generated from hello **serializer** library or created manually using hello **IoTHubClient** library does not matter.</span></span>

<span data-ttu-id="daff1-359">Merhaba farklı aygıt kimlik bilgileri kullanarak, **IoTHubClient\_ÜM\_oluşturma** da çalışır olarak **IoTHubClient\_CreateFromConnectionString** için ayrılırken bir **IOTHUB\_istemci\_İŞLEMEK**.</span><span class="sxs-lookup"><span data-stu-id="daff1-359">For hello alternate device credentials, using **IoTHubClient\_LL\_Create** works just as well as **IoTHubClient\_CreateFromConnectionString** for allocating an **IOTHUB\_CLIENT\_HANDLE**.</span></span>

<span data-ttu-id="daff1-360">Son olarak, hello kullanıyorsanız **seri hale getirici** kitaplığı ile yapılandırma seçeneklerini ayarlayabilirsiniz **IoTHubClient\_ÜM\_SetOption** hello kullanırkenyaptığınızgibi**IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="daff1-360">Finally, if you're using hello **serializer** library, you can set configuration options with **IoTHubClient\_LL\_SetOption** just as you did when using hello **IoTHubClient** library.</span></span>

<span data-ttu-id="daff1-361">Benzersiz toohello özelliği **seri hale getirici** kitaplığı olan hello başlatma API'leri.</span><span class="sxs-lookup"><span data-stu-id="daff1-361">A feature that is unique toohello **serializer** library are hello initialization APIs.</span></span> <span data-ttu-id="daff1-362">Merhaba kitaplığı ile çalışmaya başlamadan önce çağırmalısınız **seri hale getirici\_init**:</span><span class="sxs-lookup"><span data-stu-id="daff1-362">Before you can start working with hello library, you must call **serializer\_init**:</span></span>

```
serializer_init(NULL);
```

<span data-ttu-id="daff1-363">Yalnızca arama yapmadan önce bu yapılır **IoTHubClient\_CreateFromConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="daff1-363">This is done just before you call **IoTHubClient\_CreateFromConnectionString**.</span></span>

<span data-ttu-id="daff1-364">Benzer şekilde, bitirdiğinizde hello kitaplıkla çalışırken, yaptığınız hello son çok çağrıdır**seri hale getirici\_deinit**:</span><span class="sxs-lookup"><span data-stu-id="daff1-364">Similarly, when you're done working with hello library, hello last call you’ll make is too**serializer\_deinit**:</span></span>

```
serializer_deinit();
```

<span data-ttu-id="daff1-365">Aksi takdirde, tüm yukarıda listelenen diğer özellikleri hello iş hello aynı hello **seri hale getirici** kitaplığı hello göründükleri **IoTHubClient** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="daff1-365">Otherwise, all of hello other features listed above work hello same in hello **serializer** library as they do in hello **IoTHubClient** library.</span></span> <span data-ttu-id="daff1-366">Bu konular hakkında daha fazla bilgi için bkz: Merhaba [önceki makalede](iot-hub-device-sdk-c-iothubclient.md) bu serideki.</span><span class="sxs-lookup"><span data-stu-id="daff1-366">For more information about any of these topics, see hello [previous article](iot-hub-device-sdk-c-iothubclient.md) in this series.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daff1-367">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="daff1-367">Next steps</span></span>
<span data-ttu-id="daff1-368">Bu makalede ayrıntı hello benzersiz yönleri hello içinde **seri hale getirici** hello bulunan kitaplık **C için Azure IOT cihaz SDK'sı**. Sağlanan hello bilgilerle IOT Hub'ından iletileri almasına ve nasıl toouse toosend olayları modeller, iyi anlamış olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="daff1-368">This article describes in detail hello unique aspects of hello **serializer** library contained in hello **Azure IoT device SDK for C**. With hello information provided you should have a good understanding of how toouse models toosend events and receive messages from IoT Hub.</span></span>

<span data-ttu-id="daff1-369">Bu ayrıca nasıl toodevelop uygulamalarla hello üzerinde hello üç bölümlük sonucuna **C için Azure IOT cihaz SDK'sı**. Bu, yeterli bilgi toonot yalnızca Başlarken olabilir ancak nasıl hello API'leri işe kapsamlı olarak anlamayı size gerekir.</span><span class="sxs-lookup"><span data-stu-id="daff1-369">This also concludes hello three-part series on how toodevelop applications with hello **Azure IoT device SDK for C**. This should be enough information toonot only get you started but give you a thorough understanding of how hello APIs work.</span></span> <span data-ttu-id="daff1-370">Ek bilgi için SDK burada kapsanmayan hello birkaç örneği vardır.</span><span class="sxs-lookup"><span data-stu-id="daff1-370">For additional information, there are a few samples in hello SDK not covered here.</span></span> <span data-ttu-id="daff1-371">Aksi takdirde hello [SDK Belgeleri](https://github.com/Azure/azure-iot-sdk-c) ek bilgi için iyi bir kaynaktır.</span><span class="sxs-lookup"><span data-stu-id="daff1-371">Otherwise, hello [SDK documentation](https://github.com/Azure/azure-iot-sdk-c) is a good resource for additional information.</span></span>

<span data-ttu-id="daff1-372">IOT hub'ı geliştirme hakkında daha fazla toolearn bkz hello [Azure IOT SDK'ları][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="daff1-372">toolearn more about developing for IoT Hub, see hello [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="daff1-373">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="daff1-373">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="daff1-374">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="daff1-374">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
