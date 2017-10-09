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
# <a name="azure-iot-device-sdk-for-c--more-about-serializer"></a>Azure IOT cihaz SDK'sı için C – seri hale getirici hakkında daha fazla bilgi
Merhaba [ilk makale](iot-hub-device-sdk-c-intro.md) bu sunulan serisi hello içinde **C için Azure IOT cihaz SDK'sı**. hello sonraki makalede sağlanan hello daha ayrıntılı bir açıklaması [ **IoTHubClient** ](iot-hub-device-sdk-c-iothubclient.md). Bu makalede bileşen kalan hello daha ayrıntılı bir açıklaması sağlayarak hello SDK kapsamını tamamlandıktan: Merhaba **seri hale getirici** kitaplığı.

Merhaba giriş makalesi nasıl açıklanan toouse hello **seri hale getirici** kitaplığı toosend olayları tooand IOT Hub'ından iletileri alırsınız. Bu makalede, biz bu tartışma nasıl daha eksiksiz bir açıklaması sağlayarak genişletmek toomodel hello verilerinizle **seri hale getirici** makro dili. Merhaba makale ayrıca nasıl hello kitaplığı iletileri serileştiren hakkında daha fazla ayrıntı içerir (ve bazı durumlarda nasıl hello serileştirme davranışını denetleyebileceğiniz). Biz de oluşturduğunuz hello modelleri hello boyutunu belirleyen değiştirebileceğiniz bazı parametreleri açıklayan.

Son olarak, ileti ve özellik işleme gibi önceki makalelerinde kapsanan bazı konular hello makale revisits. Çıkışı, bu özellikleri işlerinde bulacaksınız gibi aynı şekilde hello kullanarak hello **seri hale getirici** kitaplığı ile Merhaba göründükleri **IoTHubClient** kitaplığı.

Bu makalede açıklanan her şeyi hello üzerinde temel **seri hale getirici** SDK örnekleri. Merhaba toofollow boyunca istiyorsanız bkz **simplesample\_amqp** ve **simplesample\_http** hello Azure IOT cihaz SDK'sı C. eklenmiş olan uygulamalar

Merhaba bulabilirsiniz [ **C için Azure IOT cihaz SDK'sı** ](https://github.com/Azure/azure-iot-sdk-c) GitHub depo ve görünüm ayrıntılarını hello hello API [C API Başvurusu](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-modeling-language"></a>Merhaba Modelleme Dili
Merhaba [giriş makalesi](iot-hub-device-sdk-c-intro.md) bu sunulan serisi hello içinde **C için Azure IOT cihaz SDK'sı** hello sağlanan hello örneğin aracılığıyla dil modelleme **simplesample\_amqp**  uygulama:

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

Gördüğünüz gibi dil modelleme hello C makroları temel alır. Her zaman tanımınız ile başlayan **başlangıç\_ad alanı** ve her zaman bittiğini **son\_ad alanı**. Şirketinizde veya bu örnekte, üzerinde çalıştığınız hello proje olduğu gibi'de ortak tooname hello ad alanıdır.

Ne hello ad alanı içinde aygıtlardır modelini tanımlar. Bu durumda, tek bir model için bir anemometer yoktur. Bir kez daha, hello modeli adlı bir şey, ancak bu genelde adlı hello aygıt veya veri türü için IOT Hub ile tooexchange istiyor.  

Modelleri içeren bir tanımı hello olayları giriş tooIoT Hub olabilir (hello *veri*) IOT Hub'ından alabilir Merhaba iletileri yanı sıra (Merhaba *Eylemler*). Merhaba örnekte görebildiğiniz gibi olayları bir türü ve bir ada sahip; Eylemler, bir ad ve isteğe bağlı parametreler (her bir türüyle) sahip.

Merhaba SDK tarafından desteklenen ek veri türleri olan ne Bu örnekte gösterilmez. Biz bu sonraki ele alacağız.

> [!NOTE]
> IOT hub'ı başvuran bir aygıt olarak tooit gönderdiği toohello veri *olayları*tooit olarak dil modelleme hello başvuruyor yaparken *veri* (kullanılarak tanımlanan **WITH_DATA**). Benzer şekilde, IOT hub'ı toohello veri toodevices olarak gönder başvuruyor *iletileri*tooit olarak dil modelleme hello başvuruyor yaparken *Eylemler* (kullanılarak tanımlanan **WITH_ACTION**). Bu makalede birbirinin yerine kullanılabilir bu koşulları unutmayın.
> 
> 

### <a name="supported-data-types"></a>Desteklenen veri türleri
veri türleri aşağıdaki hello hello ile oluşturulan modellerinde desteklenir **seri hale getirici** kitaplığı:

| Tür | Açıklama |
| --- | --- |
| Çift |çift duyarlıklı kayan nokta sayısı |
| Int |32 bit tamsayı |
| Kayan nokta |tek duyarlıklı kayan nokta sayısı |
| uzun |uzun tamsayı |
| int8\_t |8 bit tam sayı |
| int16\_t |16 bit tam sayı |
| Int32\_t |32 bit tamsayı |
| int64\_t |64 bit tamsayı |
| bool |Boole değeri |
| ASCII\_char\_ptr |ASCII dizesi |
| EDM\_TARİH\_ZAMAN\_UZAKLIĞI |Tarih Saat farkı |
| EDM\_GUID |GUID |
| EDM\_İKİLİ |İkili |
| BİLDİRME\_YAPISI |karmaşık veri türü |

Merhaba son veri türüyle başlayalım. Merhaba **DECLARE\_YAPISI** hello gruplandırmaları olan toodefine karmaşık veri türlerini başka ilkel türler sağlar. Bu gruplandırmalar bize toodefine şuna benzer bir model izin ver:

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

Bir tek veri olayı türü modelimizi içeriyor **TestType**. **TestType** topluca hello ilkel türler hello tarafından desteklenen gösteren birkaç üyeleri içeren karmaşık bir tür **seri hale getirici** model oluşturma dili.

Bir modelin bu şekilde size kod toosend veri tooIoT aşağıdaki gibi görünür Hub yazabilirsiniz:

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

Temel olarak, biz hello değeri tooevery üyesi atama **Test** yapısı ve ardından çağırma **SendAsync** toosend hello **Test** veri olay toohello bulut. **SendAsync** bir tek veri olay tooIoT Hub gönderir yardımcı işlevdir:

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

Bu işlev veri olayı verilen hello serileştirir ve tooIoT Hub gönderir kullanarak **IoTHubClient\_SendEventAsync**. Aynı kodu önceki makalelerinde açıklanan hello budur (**SendAsync** hello mantığı kullanışlı bir işlevdeki yalıtır).

Merhaba önceki kod içinde kullanılan bir diğer yardımcı işlevdir **GetDateTimeOffset**. Bu işlev saat türünde bir değer verilen hello dönüştüren **EDM\_tarih\_zaman\_UZAKLIĞI**:

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

Bu kodu çalıştırmak, iletiden hello tooIoT Hub gönderilir:

```
{"aDouble":1.100000000000000, "aInt":2, "aFloat":3.000000, "aLong":4, "aInt8":5, "auInt8":6, "aInt16":7, "aInt32":8, "aInt64":9, "aBool":true, "aAsciiCharPtr":"ascii string 1", "aDateTimeOffset":"2015-09-14T21:18:21Z", "aGuid":"00010203-0405-0607-0809-0A0B0C0D0E0F", "aBinary":"AQID"}
```

Merhaba serileştirme hello tarafından oluşturulan hello biçimi JSON olduğuna dikkat edin **seri hale getirici** kitaplığı. Ayrıca her bir üyesi hello JSON nesnesi seri Not hello hello üyeleri eşleşen **TestType** biz bizim modelde tanımlanmış. Merhaba değerleri de tam olarak hello kod içinde kullanılan eşleştiğinden. Ancak, hello ikili veriler base64 ile kodlanmış olduğuna dikkat edin: olan "AQID" hello, base64 kodlaması {0x01, 0x02, 0x03}.

Bu örnek hello kullanarak hello avantajı gösterir **seri hale getirici** kitaplığı--bize toosend JSON toohello bulut uygulamamız serileştirmede uğraşmanız tooexplicitly gerek kalmadan etkinleştirir. Tüm ilgili tooworry sahip olduğumuz ayarlanması hello başlangıç değerleri veri olaylarını modelimizi ve ardından bu olayları toohello bulut basit API'ler toosend çağırma.

Bu bilgi ile biz hello aralığı (biz bile başka karmaşık türler içindeki karmaşık tür dahil olabilir) karmaşık türleri dahil olmak üzere desteklenen veri türlerini içeren modellerinin tanımlayabilirsiniz. Ancak, kendisinin oluşturulan JSON seri hale getirilmiş tarafından hello yukarıdaki örnekte önemli noktanız getirir. *Nasıl* size hello verilerle göndereceğiz **seri hale getirici** kitaplığı belirler tam olarak nasıl hello JSON biçimi. Bu belirli ne şu sonraki konulara değineceğiz noktasıdır.

## <a name="more-about-serialization"></a>Seri hale getirme hakkında daha fazla bilgi
Merhaba önceki bölümde vurgular hello tarafından oluşturulan bir hello çıkış **seri hale getirici** kitaplığı. Bu bölümde, nasıl hello kitaplığı veri serileştirir ve hello serileştirme API'leri kullanılarak bu davranışı nasıl kontrol edebilir açıklayacağız.

Sipariş tooadvance hello tartışmada üzerinde seri hale getirme, biz thermostat üzerinde temel alan yeni bir modeli çalışmak. İlk olarak, şimdi bazı arka plan sağlamak hello senaryosunda biz tooaddress çalıştığınız.

Toomodel sıcaklık ve nem ölçer thermostat istiyoruz. Her veri parçası tooIoT Hub farklı gönderilen toobe geçiyor. Varsayılan olarak, her iki dakikada bir sıcaklık olay thermostat ingresses hello; bir nem her 15 dakikada ingressed olayıdır. Ya da olay ingressed olduğunda, o hello karşılık gelen sıcaklık hello saati gösteren bir zaman damgası içermelidir veya nem ölçülür.

Bu senaryo verildiğinde, şu iki farklı şekilde toomodel hello veri göstermek ve modelleme çıktı hello üzerinde serileştirilmiş hello etkisi açıklayacağız.

### <a name="model-1"></a>Model 1
Merhaba ilk sürüm destekler önceki senaryoda hello bir modelin şöyledir:

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

Not hello modelin iki veri olaylarını içerir: **sıcaklık** ve **nem**. Önceki örneklerde farklı olarak, her olayın hello türü kullanılarak tanımlanan bir yapıdır **DECLARE\_YAPISI**. **TemperatureEvent** ısı ölçümü ve zaman damgası; içerir **HumidityEvent** nem ölçümü ve zaman damgası içeriyor. Bu model, bize yukarıda açıklanan hello senaryosu için doğal şekilde toomodel hello veri sağlar. Biz bir olay toohello bulut gönderdiğinizde, ya da sıcaklık/zaman damgası veya bir nem/zaman damgası çifti göndereceğiz.

Merhaba aşağıdaki gibi kod kullanarak bir sıcaklık olay toohello bulut gönderebiliriz:

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

Biz sabit kodlanmış değerler sıcaklık ve nem hello örnek kodda kullanır, ancak biz aslında bu değerleri hello karşılık gelen algılayıcı hello thermostat üzerinde örnekleyerek alma olduğunu düşünün.

Yukarıdaki Hello kod kullanan hello **GetDateTimeOffset** önceden sunulan Yardımcısı. Clear sonraki olacak nedeniyle, bu kod açıkça seri hale getirme ve hello olay gönderme hello görevi ayırır. Merhaba önceki kod hello sıcaklık olay bir arabelleğe serileştirir. Ardından, **sendMessage** yardımcı işlevi (dahil **simplesample\_amqp**) gönderir olay tooIoT Hub hello:

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

Bu kod hello alt kümesidir **SendAsync** biz üzerine yeniden buraya gidin olmaz şekilde hello önceki bölümde açıklanan Yardımcısı.

Biz hello önceki kod toosend hello sıcaklık olay çalıştırdığınızda, bu serileştirilmiş formu hello olayın tooIoT Hub gönderilir:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Biz türü olan bir sıcaklık gönderiyorsanız **TemperatureEvent** ve bu yapı içeren bir **sıcaklık** ve **zaman** üyesi. Bu, doğrudan serileştirilmiş hello verilerde yansıtılır.

Benzer şekilde, biz bu kodu nem olayla gönderebilirsiniz:

```
thermostat->Humidity.Humidity = 45;
thermostat->Humidity.Time = GetDateTimeOffset(now);
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

tooIoT Hub gönderdi serileştirilmiş hello form aşağıdaki gibi görünür:

```
{"Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Yeniden, bu beklenen biçimde değil.

Bu model ile nasıl ek olaylar hayal edebildiğiniz kolayca eklenebilir. Kullanarak daha fazla yapıları tanımladığınız **DECLARE\_YAPISI**ve hello modelinde hello karşılık gelen olay dahil **ile\_veri**.

Şimdi, hello içeren hello modeli değiştirelim aynı veri ancak farklı bir yapıya sahip.

### <a name="model-2"></a>Model 2
Bu alternatif modeli toohello biri yukarıdaki göz önünde bulundurun:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Bu durumda biz hello olmadığı anlaşılmış olur **DECLARE\_YAPISI** makroları ve yalnızca basit türler dil modelleme hello kullanarak senaryomuz hello veri öğeleri tanımlama.

Yalnızca hello şu anda şirketinizdeki hello Yoksay **zaman** olay. Bu aralık ile Merhaba kod tooingress işte **sıcaklık**:

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

Bu kod, olay tooIoT Hub hello aşağıdaki serileştirilmiş gönderir:

```
{"Temperature":75}
```

Ve hello nem olay gönderme hello kod aşağıdaki gibidir:

```
thermostat->Humidity = 45;
if (SERIALIZE(&destination, &destinationSize, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Bu kod, bu tooIoT Hub gönderir:

```
{"Humidity":45}
```

Şu ana kadar var. yine de hiçbir beklenmeyen durumları. Şimdi hello SERİLEŞTİRME makrosu nasıl kullanırız değiştirelim.

Merhaba **SERİLEŞTİRME** makrosu bağımsız değişken birden çok veri olaylarını alabilir. Bu bize tooserialize hello sağlar **sıcaklık** ve **nem** birlikte olay ve tek çağrıda tooIoT Hub gönderin:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Bu kodun hello sonucunda iki veri olayları tooIoT Hub gönderilir olduğunu tahmin:

[

{"Sıcaklık": 75},

{"Nem": 45}

]

Diğer bir deyişle, bu kod olduğu Merhaba, aynı göndermek bekleyebilirsiniz **sıcaklık** ve **nem** ayrı olarak. Yalnızca kolaylık toopass olan iki olayları çok**SERİLEŞTİRME** hello aynı çağrı. Ancak, bu hello durumda değil. Bunun yerine, yukarıdaki hello kod bu tek veri olay tooIoT Hub gönderir:

{"Sıcaklık": 75 "nem": 45}

Modelimizi tanımladığından Bu tuhaf görünebilir **sıcaklık** ve **nem** iki olarak *ayrı* olayları:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Daha fazla toohello noktası, biz bu olayları modelini alamadık nerede **sıcaklık** ve **nem** hello olan aynı yapısı:

```
DECLARE_STRUCT(TemperatureAndHumidityEvent,
int, Temperature,
int, Humidity,
);

DECLARE_MODEL(Thermostat,
WITH_DATA(TemperatureAndHumidityEvent, TemperatureAndHumidity),
);
```

Bu model kullansaydık, bunu daha kolay toounderstand nasıl olacaktır **sıcaklık** ve **nem** hello aynı serileştirilmiş ileti gönderilir. Her iki veri olaylarını çok geçirdiğinizde bu şekilde çalıştığını neden ancak onu Temizle olmayabilir**SERİLEŞTİRME** kullanarak modeli 2.

Bu hello hello varsayımlar biliyorsanız, bu daha kolay toounderstand davranıştır **seri hale getirici** kitaplığı yapma. Bu toomake duygusu geri tooour modeli edelim:

```
DECLARE_MODEL(Thermostat,
WITH_DATA(int, Temperature),
WITH_DATA(int, Humidity),
WITH_DATA(EDM_DATE_TIME_OFFSET, Time)
);
```

Bu model nesne yönelimli koşullarında düşünün. Bu durumda biz fiziksel bir aygıtı (thermostat) modelleme ve o aygıtı gibi özniteliklerini içerir **sıcaklık** ve **nem**.

Merhaba tüm modelimizi hello aşağıdaki gibi kod ile durumunu gönderebiliriz:

```
if (SERIALIZE(&destination, &destinationSize, thermostat->Temperature, thermostat->Humidity, thermostat->Time) == IOT_AGENT_OK)
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
}
```

Sıcaklık ve nem zaman Hello değerlerini ayarlamak varsayıldığında, bu gönderilen tooIoT Hub gibi bir olay görür:

```
{"Temperature":75, "Humidity":45, "Time":"2015-09-17T18:45:56Z"}
```

Bazen yalnızca toosend isteyebilirsiniz *bazı* (Bu, çok sayıda veri olaylarını modelinizi içeriyorsa, özellikle true) hello modeli toohello bulutun özelliklerini. Yararlı toosend yalnızca bir alt veri olayların gibi önceki örneğimizde olmasından:

```
{"Temperature":75, "Time":"2015-09-17T18:45:56Z"}
```

Bu tam olarak hello oluşturur biz olarak tanımlanmışsa aynı olay serileştirilmiş bir **TemperatureEvent** ile bir **sıcaklık** ve **zaman** üye, biz ile 1 model gibi. Bu durumda tam olarak hello aynı serileştirilmiş olay biz adlı olduğundan farklı bir model (model 2) kullanarak mümkün toogenerate bulamadığımız **SERİLEŞTİRME** farklı bir şekilde.

birden çok veri olaylarını çok geçirirseniz hello önemli nokta olan**SERİLEŞTİRME,** sonra her olay tek bir JSON nesnesi özelliğinde olduğunu varsayar.

Merhaba en iyi yaklaşımı, ve modelinizi hakkında nasıl düşündüğünüz bağlıdır. "Olayları" toohello bulut gönderiyorsanız ve her olay tanımlanmış bir özellik kümesi içeriyorsa, hello ilk yaklaşımı algılama çok hale getirir. Bu durumda kullanacağınız **DECLARE\_YAPISI** toodefine hello her olay yapısını ve bunları modelinizi hello dahil **ile\_veri** makrosu. Merhaba ilk yukarıdaki örnekte yaptığımız gibi her olay gönderirsiniz. Bu yaklaşım, yalnızca bir tek veri olayı çok geçip geçmeyeceğini**seri hale GETİRİCİ**.

Nesne odaklı bir şekilde modelinizde hakkında düşünüyorsanız, hello ikinci yaklaşımın size uygun. Bu durumda, öğeleri kullanarak tanımlanan hello **ile\_veri** hello "" nesnenizin özelliklerdir. Hangi olayların alt kümesini çok geçirdiğiniz**SERİLEŞTİRME** istediğiniz, ne kadar "nesnesinin" durumuna bağlı olarak toosend toohello bulut istiyor.

Doğru veya yanlış bir bağlanamadı yaklaşımdır. Yalnızca nasıl ele aldığını da hello **seri hale getirici** kitaplığı çalışır ve gereksinimlerine en uygun çekme hello modelleme yaklaşım.

## <a name="message-handling"></a>İleti işleme
Şu ana kadar bu makalede, gönderen olaylar tooIoT Hub ele alınan yalnızca ve iletileri alma ele kurmadı. Merhaba neden bu ne ihtiyacımız olan için ileti alma hakkında tooknow büyük ölçüde içinde ele alınmış bir [önceki makalesi](iot-hub-device-sdk-c-intro.md). Bu makaleden bir ileti geri çağırma işlevini kaydederek iletileri işleme geri çağırma:

```
IoTHubClient_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather)
```

Ardından, bir ileti alındığında çağrılan hello geri çağırma işlevi de yazın:

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

Bu uygulaması, **IoTHubMessage** çağrıları hello modelinizdeki her eylem için belirli bir işlev. Örneğin bu eylemi modelinizi tanımlar:

```
WITH_ACTION(SetAirResistance, int, Position)
```

Bu imza işleviyle tanımlamanız gerekir:

```
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

**SetAirResistance** tooyour cihaz bu ileti gönderildiğinde daha sonra çağrılır.

Ne biz açıklandığı henüz henüz hangi hello serileştirilmiş ileti görülüyor sürümüdür. Diğer bir deyişle, toosend istiyorsanız bir **SetAirResistance** ileti tooyour aygıt, ne görünüm ister?

Bir ileti tooa aygıt gönderiyorsanız hello Azure IOT hizmeti SDK aracılığıyla bunu. Hala ne toosend tooinvoke belirli bir eylem dize tooknow gerekir. ileti gönderme için hello genel biçimi şu şekilde görünür:

```
{"Name" : "", "Parameters" : "" }
```

Serileştirilmiş bir JSON nesnesi iki özellikleriyle gönderiyorsanız: **adı** hello eylemi (ileti) hello adıdır ve **parametreleri** bu eylemin hello parametrelerini içerir.

Örneğin, tooinvoke **SetAirResistance** bu ileti tooa aygıt gönderebilirsiniz:

```
{"Name" : "SetAirResistance", "Parameters" : { "Position" : 5 }}
```

Merhaba eylem adı, modelde tanımlanan bir eylem tam olarak eşleşmelidir. Merhaba parametre adları de eşleşmelidir. Ayrıca, büyük küçük harfe duyarlılığın unutmayın. **Ad** ve **parametreleri** her zaman büyük harfle yazılır. Eylem adı ve parametreleri emin toomatch hello durumunda modelinizde olun. Bu örnekte, hello eylem adı "SetAirResistance" değil "setairresistance" ise.

diğer iki eylem hello **TurnFanOn** ve **TurnFanOff** bu iletileri tooa aygıt göndererek çağrılır:

```
{"Name" : "TurnFanOn", "Parameters" : {}}
{"Name" : "TurnFanOff", "Parameters" : {}}
```

Gereksinim duyduğunuz her şeyi tooknow iletileri ile olayları gönderme ve alma Merhaba, bu bölümde açıklanan **seri hale getirici** kitaplığı. Devam etmeden önce şimdi ne kadar büyük modelinizi denetleyebilir yapılandırabileceğiniz bazı parametreler kapsar.

## <a name="macro-configuration"></a>Makro yapılandırma
Merhaba kullanıyorsanız **seri hale getirici** hello SDK toobe farkında önemli bir kısmını hello azure-c-paylaşılan-yardımcı programı Kitaplığı'nda bulunan kitaplık.
Merhaba--özyinelemeli seçeneği kullanılarak GitHub hello Azure-IOT-sdk-c depodan klonlanmış varsa, bu paylaşılan yardımcı kitaplık yer alır:

```
.\\c-utility
```

Merhaba kitaplığı klonlanmış değil, bulabilirsiniz [burada](https://github.com/Azure/azure-c-shared-utility).

Merhaba paylaşılan yardımcı kitaplıkta klasörü aşağıdaki hello bulacaksınız:

```
azure-c-shared-utility\\macro\_utils\_h\_generator.
```

Adlı bir Visual Studio çözümü bu klasörde **makrosu\_yardımcı programları\_h\_generator.sln**:

  ![](media/iot-hub-device-sdk-c-serializer/01-macro_utils_h_generator.PNG)

Bu çözümdeki Hello programın oluşturduğu hello **makrosu\_utils.h** dosya. Varsayılan makrosu yoktur\_hello SDK ile bulunan utils.h dosyası. Bu çözüm bazı parametreler ve sonra yeniden oluşturun üstbilgi dosyası bu parametrelere göre hello toomodify sağlar.

Merhaba iki anahtar parametreleri toobe endişe ile **nArithmetic** ve **nMacroParameters** makro içinde bulunan bu iki satır içinde tanımlanan\_utils.tt:

```
<#int nArithmetic=1024;#>
<#int nMacroParameters=124;/*127 parameters in one macro deﬁnition in C99 in chapter 5.2.4.1 Translation limits*/#>

```

Bu değerleri hello SDK ile dahil hello varsayılan parametreleridir. Her bir parametreyi anlamı aşağıdaki hello sahiptir:

* nMacroParameters – denetimleri içinde bir DECLARE olabilir kaç parametreleri\_modeli makro tanımı.
* nArithmetic – denetimleri hello toplam bir model izin üye sayısı.

Bunlar denetlemek için bu parametreler önemli hello modelinizi ne kadar büyük olabilir nedenidir. Örneğin, bu model tanımı göz önünde bulundurun:

```
DECLARE_MODEL(MyModel,
WITH_DATA(int, MyData)
);
```

Daha önce belirtildiği gibi **DECLARE\_MODEL** yalnızca C makro. Merhaba hello modeli ve hello adları **ile\_veri** deyimi (henüz başka bir makrosu) olan parametrelerinin **DECLARE\_modeli**. **nMacroParameters** kaç parametreleri eklenebilir tanımlar **DECLARE\_modeli**. Etkili bir şekilde sağlayabilirsiniz kaç tane veri olay ve eylem bildirimleri tanımlar. Bu nedenle, hello varsayılan sınırının 124 ile bu 60 eylemleri ve veri olayları birleşimi ile bir model tanımlayabilirsiniz anlamına gelir. Bu sınır tooexceed çalışırsanız, benzer toothis Ara derleyici hataları alırsınız:

  ![](media/iot-hub-device-sdk-c-serializer/02-nMacroParametersCompilerErrors.PNG)

Merhaba **nArithmetic** parametredir uygulamanızı'den daha fazla hello iç işleyişini hello makro dili hakkında.  Merhaba toplam modelinizde, olabilir üye sayısı denetimleri de dahil olmak üzere **DECLARE_STRUCT** makroları. Bu gibi derleyici hataları görmeye başlayacaksınız sonra artırmayı denemelisiniz **nArithmetic**:

   ![](media/iot-hub-device-sdk-c-serializer/03-nArithmeticCompilerErrors.PNG)

Bu parametreler toochange istiyorsanız, hello makrosu hello değerleri değiştirin\_utils.tt dosyası, yeniden derleyebilirsiniz hello makrosu\_yardımcı programları\_h\_generator.sln çözüm ve çalışma hello derlenmiş program. Bunu yaptığınızda bunu yeni bir makro\_utils.h dosya oluşturulur ve hello yerleştirilir.\\ Ortak\\Inc dizini.

Sipariş toouse hello yeni sürümünde makrosu\_utils.h, Kaldır hello **seri hale getirici** NuGet paketi çözümünüzden ve onun yerine dahil hello **seri hale getirici** Visual Studio projesi. Bu, kod toocompile hello kaynak kodu hello seri hale getirici kitaplığının karşı sağlar. Bu güncelleştirilmiş hello makrosu içerir\_utils.h. Bunun için toodo istiyorsanız **simplesample\_amqp**, hello çözümden hello NuGet paketi hello seri hale getirici kitaplığı kaldırarak Başlat:

   ![](media/iot-hub-device-sdk-c-serializer/04-serializer-github-package.PNG)

Daha sonra bu proje tooyour Visual Studio çözümü ekleyin:

> . \\c\\seri hale getirici\\yapı\\windows\\serializer.vcxproj
> 
> 

İşiniz bittiğinde, çözümünüzün aşağıdaki gibi görünmelidir:

   ![](media/iot-hub-device-sdk-c-serializer/05-serializer-project.PNG)

Ne zaman, çözümünüz hello derleme makro güncelleştirilmiş artık\_utils.h ikili dosyanız yer almaktadır.

Bu değerleri yeterince artırma derleyici sınırları aşabilir unutmayın. toothis noktası hello **nMacroParameters** ilgilenen hangi toobe ile Merhaba ana parametresidir. Merhaba C99 spec 127 parametreleri en az bir makro tanımı'nda verilir belirtir. Merhaba Microsoft derleyici hello spec tam olarak aşağıdaki (ve 127 sınırı) mümkün tooincrease olmayacaktır **nMacroParameters** hello varsayılan ötesinde. Diğer derleyiciler toodo şekilde izin vermiyor olabilir (örneğin, daha yüksek bir sınır hello GNU derleyici destekler).

Şu ana kadar biz neredeyse tooknow nasıl toowrite kod hello ile ilgili ihtiyaç duyduğunuz her şeyi kapsamdaki **seri hale getirici** kitaplığı. Tamamlanırken önce şimdi bazı konular hakkında merak ediyor önceki makalelerden yeniden ziyaret.

## <a name="hello-lower-level-apis"></a>Merhaba düşük düzeyli API'leri
Bu makale üzerinde odaklanmış hello örnek uygulama **simplesample\_amqp**. Bu örnek hello üst düzey (Merhaba olmayan-"tümü") API'leri toosend olayları kullanır ve iletileri alabilirsiniz. Bu API'leri kullanırsanız, hem olayları ileti gönderme ve alma, mvc'deki bir arka plan iş parçacığı çalıştırır. Ancak, bu arka plan iş parçacığı hello alt düzey (Tümü) API'leri tooeliminate kullanın ve açık denetim olayları gönderirken veya hello buluttan iletilerini gerçekleştirin.

Bölümünde açıklandığı gibi bir [önceki makale](iot-hub-device-sdk-c-iothubclient.md), Merhaba oluşan bir dizi işlevleri yoktur üst düzey API'leri:

* IoTHubClient\_CreateFromConnectionString
* IoTHubClient\_SendEventAsync
* IoTHubClient\_SetMessageCallback
* IoTHubClient\_yok

Bu API'leri örneklerde gösterildiği **simplesample\_amqp**.

Ayrıca vardır benzer bir alt düzey API kümesi.

* IoTHubClient\_ÜM\_CreateFromConnectionString
* IoTHubClient\_ÜM\_SendEventAsync
* IoTHubClient\_ÜM\_SetMessageCallback
* IoTHubClient\_ÜM\_yok

Merhaba düşük düzeyli API'leri iş tam olarak aynı şekilde hello önceki makalelerinde açıklandığı gibi hello olduğunu unutmayın. İleti olayları gönderme ve alma bir arka plan iş parçacığı toohandle istiyorsanız hello ilk API kümesi kullanabilirsiniz. Açık denetim zaman göndermek ve IOT Hub'ından veri almak istiyorsanız, hello ikinci API kümesi kullanın. API iş ayarlayın ya da eşit ile Merhaba yanı sıra **seri hale getirici** kitaplığı.

Nasıl bir örneği için hello düşük düzeyli API'leri ile Merhaba kullanılan **seri hale getirici** kitaplığı hello bkz **simplesample\_http** uygulama.

## <a name="additional-topics"></a>Ek konu başlıkları
Söz değerinde birkaç diğer yeniden işleme, diğer aygıt kimlik bilgisi ve yapılandırma seçeneklerini kullanarak özellik konulardır. Tüm konuları ele bunlar bir [önceki makalede](iot-hub-device-sdk-c-iothubclient.md). Merhaba ana bu özelliklerin tümü, hello aynı çalıştığını noktasıdır hello işlemleriyle **seri hale getirici** kitaplığı ile Merhaba göründükleri **IoTHubClient** kitaplığı. Örneğin, modelinizin dışında tooattach özellikleri tooan olay istiyorsanız, kullandığınız **IoTHubMessage\_özellikleri** ve **harita**\_**örnek**, aynı şekilde daha önce açıklandığı gibi hello:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Merhaba olay hello olup oluşturulan **seri hale getirici** kitaplığı veya hello kullanarak el ile oluşturulan **IoTHubClient** kitaplığı önemli değildir.

Merhaba farklı aygıt kimlik bilgileri kullanarak, **IoTHubClient\_ÜM\_oluşturma** da çalışır olarak **IoTHubClient\_CreateFromConnectionString** için ayrılırken bir **IOTHUB\_istemci\_İŞLEMEK**.

Son olarak, hello kullanıyorsanız **seri hale getirici** kitaplığı ile yapılandırma seçeneklerini ayarlayabilirsiniz **IoTHubClient\_ÜM\_SetOption** hello kullanırkenyaptığınızgibi**IoTHubClient** kitaplığı.

Benzersiz toohello özelliği **seri hale getirici** kitaplığı olan hello başlatma API'leri. Merhaba kitaplığı ile çalışmaya başlamadan önce çağırmalısınız **seri hale getirici\_init**:

```
serializer_init(NULL);
```

Yalnızca arama yapmadan önce bu yapılır **IoTHubClient\_CreateFromConnectionString**.

Benzer şekilde, bitirdiğinizde hello kitaplıkla çalışırken, yaptığınız hello son çok çağrıdır**seri hale getirici\_deinit**:

```
serializer_deinit();
```

Aksi takdirde, tüm yukarıda listelenen diğer özellikleri hello iş hello aynı hello **seri hale getirici** kitaplığı hello göründükleri **IoTHubClient** kitaplığı. Bu konular hakkında daha fazla bilgi için bkz: Merhaba [önceki makalede](iot-hub-device-sdk-c-iothubclient.md) bu serideki.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede ayrıntı hello benzersiz yönleri hello içinde **seri hale getirici** hello bulunan kitaplık **C için Azure IOT cihaz SDK'sı**. Sağlanan hello bilgilerle IOT Hub'ından iletileri almasına ve nasıl toouse toosend olayları modeller, iyi anlamış olmanız gerekir.

Bu ayrıca nasıl toodevelop uygulamalarla hello üzerinde hello üç bölümlük sonucuna **C için Azure IOT cihaz SDK'sı**. Bu, yeterli bilgi toonot yalnızca Başlarken olabilir ancak nasıl hello API'leri işe kapsamlı olarak anlamayı size gerekir. Ek bilgi için SDK burada kapsanmayan hello birkaç örneği vardır. Aksi takdirde hello [SDK Belgeleri](https://github.com/Azure/azure-iot-sdk-c) ek bilgi için iyi bir kaynaktır.

IOT hub'ı geliştirme hakkında daha fazla toolearn bkz hello [Azure IOT SDK'ları][lnk-sdks].

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
