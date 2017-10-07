---
title: "c aaaThe Azure IOT cihaz SDK'sı | Microsoft Docs"
description: "Hello Azure IOT cihaz SDK'sı için C başlamak ve öğrenin toocreate cihaz uygulamaları, iletişim kurma biçimini bir IOT hub ile."
services: iot-hub
documentationcenter: 
author: olivierbloch
manager: timlt
editor: 
ms.assetid: e448b061-6bdd-470a-a527-15ec03cca7b9
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: obloch
ms.openlocfilehash: 9e20742e6ea513c124bfaf28f02f6fba86170daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-device-sdk-for-c"></a>C için Azure IOT cihaz SDK'sı

Merhaba **Azure IOT cihaz SDK'sı** olan bir dizi tasarlanmıştır Merhaba tooand alıcı iletileri gönderme toosimplify hello işlemi **Azure IOT Hub** hizmet. Merhaba her belirli bir platformu hedefleyen SDK, farklı çeşidi vardır, ancak bu makalede hello **C için Azure IOT cihaz SDK'sı**.

c Hello Azure IOT cihaz SDK'sı ANSI C (C99) toomaximize taşınabilirlik yazılır. Bu özellik hello kitaplıkları oldukça uygun toooperate birden çok platformlarda ve cihazlarda, özellikle disk en aza burada yapar ve bellek alanını önceliktir.

Çok çeşitli platformlar üzerinde hangi hello SDK'sı test vardır (Merhaba bkz [Azure IOT cihaz katalog için onaylanmıştır](https://catalog.azureiotsuite.com/) Ayrıntılar için). İzlenecek yollar hello Windows platformunda çalışan örnek kodu, bu makalede bulunmasına karşın, bu makalede açıklanan hello kod hello desteklenen platformlar aynı aralığıdır.

Bu makalede C. hello Azure IOT cihaz SDK'sı toohello mimarisini sunar Nasıl tooinitialize hello aygıtı kitaplığı veri tooIoT Hub, ileti gönderme ve ondan alma gösterir. Bu makaledeki Hello bilgiler hello SDK kullanmaya yeterli tooget olmalı, ancak işaretçileri tooadditional hakkında da bilgi hello kitaplıkları sağlar.

## <a name="sdk-architecture"></a>SDK mimarisi

Merhaba bulabilirsiniz [ **C için Azure IOT cihaz SDK'sı** ](https://github.com/Azure/azure-iot-sdk-c) GitHub depo ve görünüm ayrıntılarını hello hello API [C API Başvurusu](https://azure.github.io/azure-iot-sdk-c/index.html).

Merhaba kitaplıkları en son sürümünü Hello hello bulunabilir **ana** hello deponun dalı:

  ![](media/iot-hub-device-sdk-c-intro/01-MasterBranch.PNG)

* Merhaba çekirdek hello SDK hello uygulamasıdır **ıothub\_istemci** hello en düşük API katmanı hello SDK'hello uyarlamasını içeren klasörü: Merhaba **IoTHubClient** kitaplığı. Merhaba **IoTHubClient** kitaplığı IOT Hub'ından ileti alıp iletileri tooIoT Hub göndermeyi için ham Mesajlaşma uygulama API'leri içerir. Bu kitaplık kullanırken, ileti serileştirme uygulamak için sorumlu olan, ancak diğer ayrıntıları IOT Hub ile iletişim için işlenir.
* Merhaba **seri hale getirici** klasörü yardımcı işlevleri ve nasıl tooAzure IOT hub'ı kullanarak göndermeden önce tooserialize veri istemci kitaplığı hello Göster örnekleri içerir. Merhaba seri hale getirici Hello kullanımını zorunlu değildir ve kolaylık sağlanır. toouse hello **seri hale getirici** kitaplığı tooreceive dışarı beklediğiniz hello veri toosend tooIoT Hub ve hello iletileri belirten bir model tanımlayın. Merhaba modeli tanımlandığında hello SDK, sağlayan bir API yüzeyi ile tooeasily iş cihaz bulut ile sağlar ve Serileştirme ayrıntılar hakkında kaygısı olmadan bulut-cihaz iletilerini hello. Merhaba kitaplığı MQTT ve AMQP gibi protokoller kullanarak aktarım uygulayan diğer açık kaynak kitaplıkları bağlıdır.
* Merhaba **IoTHubClient** kitaplığı diğer açık kaynak kitaplıkları bağlıdır:
  * Merhaba [Azure C paylaşılan yardımcı programı](https://github.com/Azure/azure-c-shared-utility) kitaplığı çeşitli Azure ile ilgili C SDK gerekli (dizeler, liste işleme ve g/ç gibi) temel görevleri için ortak işlevsellik sağlar.
  * Merhaba [Azure uAMQP](https://github.com/Azure/azure-uamqp-c) bir istemci-tarafı uygulaması kısıtlı kaynak cihazlar için en iyi duruma getirilmiş AMQP olan kitaplığı.
  * Merhaba [Azure uMQTT](https://github.com/Azure/azure-umqtt-c) hello MQTT protokolünü uygulamaya yönelik genel amaçlı bir kitaplığı ve kısıtlı kaynak cihazlar için en iyi duruma getirilmiş kitaplığı.

Bu kitaplıklar daha kolay toounderstand örnek kodu incelemeden tarafından kullanılır. Aşağıdaki bölümlerde Merhaba, birkaç hello SDK dahil hello örnek uygulamalar size yol. Bu izlenecek iyi bir hello mimari katmanların hello SDK API'leri iş bir giriş toohow hello ve çeşitli özellikleri Merhaba eşitleyerek vermesi gerekir.

## <a name="before-you-run-hello-samples"></a>Merhaba örnekleri çalıştırmadan önce

Hello Azure IOT cihaz SDK'sı hello örnekleri için C çalıştırabilmeniz için önce şunları yapmalısınız [hello IOT hub'ı hizmet örneği oluşturma](iot-hub-create-through-portal.md) Azure aboneliğinizde. Ardından hello aşağıdaki görevleri tamamlayın:

* Geliştirme ortamınızı hazırlama
* Cihaz kimlik bilgileri edinin.

### <a name="prepare-your-development-environment"></a>Geliştirme ortamınızı hazırlama

Paketleri (örneğin, Windows için NuGet veya apt_get Debian ve Ubuntu) ortak platformlar için sağlanır ve bu paketleri kullanılabilir olduğunda hello örnekleri kullanın. Bazı durumlarda, Cihazınızda veya için toocompile hello SDK gerekir. Toocompile hello SDK gerekirse bkz [geliştirme ortamınızı hazırlama](https://github.com/Azure/azure-iot-sdk-c/blob/master/doc/devbox_setup.md) hello GitHub deposundaki.

tooobtain hello örnek uygulama kodu, bir hello SDK github'dan kopyasını indirme. Hello hello kaynak kopyanızı almak **ana** hello dalı [GitHub deposunu](https://github.com/Azure/azure-iot-sdk-c).


### <a name="obtain-hello-device-credentials"></a>Merhaba aygıt kimlik bilgilerini alma

Merhaba örnek kaynak koda sahip olduğunuza göre hello sonraki şey toodo tooget aygıt kimlik bilgileri kümesi ' dir. Bir aygıt toobe mümkün tooaccess için IOT hub'ı, öncelikle hello aygıt toohello IOT Hub kimlik kayıt eklemeniz gerekir. Cihazınızı eklediğinizde, hello aygıt toobe mümkün tooconnect toohello IOT hub için gereksinim duyduğunuz aygıt kimlik bilgisi kümesi alır. Merhaba biçiminde Hello sonraki bölümde açıklanan hello örnek uygulamaları beklediğiniz bu kimlik bilgileri bir **cihaz bağlantı dizesi**.

IOT hub'ınızı yönetmek birkaç açık kaynaklı araçları toohelp vardır.

* Adlı bir Windows uygulaması [aygıt explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).
* Platformlar arası node.js CLI aracı adlı [iothub-explorer](https://github.com/azure/iothub-explorer).

Bu öğretici hello grafik kullanır *aygıt explorer* aracı. Merhaba de kullanabilirsiniz *iothub-explorer* toouse CLI aracı tercih ederseniz, aracı.

Merhaba aygıtı explorer aracını hello Azure IOT hizmeti kitaplıkları tooperform cihaz ekleme de dahil olmak üzere IOT hub'da çeşitli işlevleri kullanır. Merhaba aygıt Gezgini aracı tooadd bir aygıtı kullanırsanız, cihazınız için bir bağlantı dizesi alın. Bu bağlantı dizesi toorun hello örnek uygulamaları gerekir.

Hello aygıt explorer aracıyla bilmiyorsanız, aşağıdaki yordamı hello açıklar nasıl toouse, tooadd bir cihaz ve cihaz bağlantı dizesini edinin.

tooinstall hello aygıtı explorer aracını bkz [nasıl toouse hello aygıt Explorer için IOT Hub cihazları](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer).

Merhaba programını çalıştırdığınızda, bu arabirim bakın:

  ![](media/iot-hub-device-sdk-c-intro/03-DeviceExplorer.PNG)

Girin, **IOT Hub bağlantı dizesine** hello ilk alan ve tıklayın **güncelleştirme**. IOT Hub ile iletişim kurabilmesi için bu adımı hello aracı yapılandırır.

Merhaba IOT Hub bağlantı dizesine yapılandırıldığında, hello tıklatın **Yönetim** sekmesi:

  ![](media/iot-hub-device-sdk-c-intro/04-ManagementTab.PNG)

Bu sekme, IOT hub'ınıza kayıtlı hello cihazları yöneteceğiniz kullanılabilir.

Merhaba tıklayarak bir cihaz oluşturma **oluşturma** düğmesi. Bir iletişim kutusu (birincil ve ikincil) önceden doldurulmuş haldedir anahtarları bir kümesini görüntüler. Girin bir **cihaz kimliği** ve ardından **oluşturma**.

  ![](media/iot-hub-device-sdk-c-intro/05-CreateDevice.PNG)

Merhaba cihaz oluşturulduğunda, hello aygıtları tek, yeni oluşturduğunuz hello dahil olmak üzere tüm kayıtlı hello aygıtlarla güncelleştirmeleri listeleyin. Yeni aygıtınızı sağ tıklatın, bu menü bakın:

  ![](media/iot-hub-device-sdk-c-intro/06-RightClickDevice.PNG)

Seçerseniz **kopyalama seçili cihaz için bağlantı dizesi**, hello cihaz bağlantı dizesidir, kopyalanan toohello Pano. Merhaba cihaz bağlantı dizesi bir kopyasını tutun. Aşağıdaki bölümlerde hello açıklanan hello örnek uygulamaları çalıştırırken gerekir.

Yukarıdaki hello adımları tamamladıktan sonra bazı kodları çalıştıran hazır toostart demektir. Her iki örnek bir sabit bir bağlantı dizesi tooenter olanak sağlayan hello ana kaynak dosyası hello üstünde vardır. Örneğin, karşılık gelen satırından hello hello **ıothub\_istemci\_örnek\_mqtt** uygulama şu şekilde görünür.

```c
static const char* connectionString = "[device connection string]";
```

## <a name="use-hello-iothubclient-library"></a>Merhaba IoTHubClient kitaplığını kullanma

Hello içinde **ıothub\_istemci** hello klasöründe [azure-IOT-sdk-c](https://github.com/azure/azure-iot-sdk-c) deposunu var. bir **örnekleri** adlıbiruygulamaiçerenklasör**ıothub\_istemci\_örnek\_mqtt**.

Merhaba Windows hello sürümü **ıothub\_istemci\_örnek\_mqtt** uygulama, Visual Studio çözümü aşağıdaki hello içerir:

  ![](media/iot-hub-device-sdk-c-intro/12-iothub-client-sample-mqtt.PNG)

> [!NOTE]
> Bu projeyi Visual Studio 2017 içinde açarsanız, hello istemleri tooretarget hello proje toohello en son sürümünü kabul edin.

Bu çözüm, tek bir proje içerir. Bu çözümde yüklü olan dört NuGet paketleri vardır:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.umqtt

Her zaman hello ihtiyacınız **Microsoft.Azure.C.SharedUtility** paketini hello SDK ile çalışırken. Bu örnek hello MQTT protokolünü kullanır, bu nedenle hello içermelidir **Microsoft.Azure.umqtt** ve **Microsoft.Azure.IoTHub.MqttTransport** (eşdeğer paketi vardır AMQP ve HTTP için paketler ). Merhaba örnek hello kullandığından **IoTHubClient** kitaplığı hello de dahil etmelisiniz **Microsoft.Azure.IoTHub.IoTHubClient** çözümünüzdeki paket.

Hello hello uygulama hello örnek uygulama için bulabilirsiniz **ıothub\_istemci\_örnek\_mqtt.c** kaynak dosyası.

Merhaba aşağıdaki adımları kullanın Bu örnek uygulama toowalk toouse hello gerekli olan size **IoTHubClient** kitaplığı.

### <a name="initialize-hello-library"></a>Merhaba kitaplığı başlatılamıyor

> [!NOTE]
> Merhaba kitaplıkları ile çalışmaya başlamadan önce bazı platforma özgü başlatma tooperform gerekebilir. Örneğin, Linux üzerinde toouse AMQP düşünüyorsanız hello OpenSSL kitaplığı başlatması gerekir. Merhaba hello örneklerinde [GitHub deposunu](https://github.com/Azure/azure-iot-sdk-c) hello yardımcı programı işlevi çağrısı **platform\_init** zaman hello istemci başlatır ve çağrı hello **platform\_deinit ** çıkmadan önce işlevi. Bu işlevler hello platform.h üstbilgi dosyasında bildirilir. Hedef platformunuzu hello için bu işlevlerin Hello tanımlarını incelemek [deposu](https://github.com/Azure/azure-iot-sdk-c) toodetermine tooinclude herhangi bir platforma özgü başlatma kod, istemci gerekmediğini.

Merhaba kitaplıklarla çalışma toostart önce bir IOT Hub istemci tanıtıcısı atayın:

```c
if ((iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol)) == NULL)
{
    (void)printf("ERROR: iotHubClientHandle is NULL!\r\n");
}
else
{
    ...
```

Merhaba aygıt Gezgini aracı toothis işlevinden elde hello cihaz bağlantı dizesi bir kopyasını geçirin. Ayrıca hello iletişim protokolü toouse belirlemeniz. Bu örnek MQTT kullanır, ancak AMQP ve HTTP ayrıca seçeneklerdir.

Geçerli bir olduğunda **IOTHUB\_istemci\_İŞLEMEK**, hello API'leri toosend çağırma başlatın ve IOT Hub'ından iletileri tooand alırsınız.

### <a name="send-messages"></a>İletileri gönder

Merhaba örnek uygulaması bir döngü toosend iletileri tooyour IOT hub ayarlar. kod parçacığında hello:

- Bir ileti oluşturur.
- Bir özellik toohello iletisi ekler.
- Bir ileti gönderir.

İlk olarak, bir ileti oluşturun:

```c
size_t iterator = 0;
do
{
    if (iterator < MESSAGE_COUNT)
    {
        sprintf_s(msgText, sizeof(msgText), "{\"deviceId\":\"myFirstDevice\",\"windSpeed\":%.2f}", avgWindSpeed + (rand() % 4 + 2));
        if ((messages[iterator].messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText))) == NULL)
        {
            (void)printf("ERROR: iotHubMessageHandle is NULL!\r\n");
        }
        else
        {
            messages[iterator].messageTrackingId = iterator;
            MAP_HANDLE propMap = IoTHubMessage_Properties(messages[iterator].messageHandle);
            (void)sprintf_s(propText, sizeof(propText), "PropMsg_%zu", iterator);
            if (Map_AddOrUpdate(propMap, "PropName", propText) != MAP_OK)
            {
                (void)printf("ERROR: Map_AddOrUpdate Failed!\r\n");
            }

            if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messages[iterator].messageHandle, SendConfirmationCallback, &messages[iterator]) != IOTHUB_CLIENT_OK)
            {
                (void)printf("ERROR: IoTHubClient_LL_SendEventAsync..........FAILED!\r\n");
            }
            else
            {
                (void)printf("IoTHubClient_LL_SendEventAsync accepted message [%d] for transmission tooIoT Hub.\r\n", (int)iterator);
            }
        }
    }
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1);

    iterator++;
} while (g_continueRunning);
```

İleti gönderme her zaman hello veriler gönderilirken çağrılan bir başvuru tooa geri çağırma işlevi belirtin. Bu örnekte, hello geri çağırma işlevini çağırdı **SendConfirmationCallback**. Aşağıdaki kod parçacığında hello bu geri çağırma işlevini gösterir:

```c
static void SendConfirmationCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    EVENT_INSTANCE* eventInstance = (EVENT_INSTANCE*)userContextCallback;
    (void)printf("Confirmation[%d] received for message tracking id = %zu with result = %s\r\n", callbackCounter, eventInstance->messageTrackingId, ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
    /* Some device specific action code goes here... */
    callbackCounter++;
    IoTHubMessage_Destroy(eventInstance->messageHandle);
}
```

Not hello çağrısı toohello **IoTHubMessage\_Destroy** hello iletisiyle bittiğinde işlev. Bu işlev, selamlama iletisine oluştururken ayrılmış hello kaynakları serbest bırakır.

### <a name="receive-messages"></a>İleti alma

Bir ileti alma zaman uyumsuz bir işlemdir. İlk olarak, Hello aygıt bir ileti aldığında hello geri çağırma tooinvoke kaydedin:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext) != IOTHUB_CLIENT_OK)
{
    (void)printf("ERROR: IoTHubClient_LL_SetMessageCallback..........FAILED!\r\n");
}
else
{
    (void)printf("IoTHubClient_LL_SetMessageCallback...successful.\r\n");
...
```

Merhaba son istediğiniz void işaretçi toowhatever parametresidir. İsteğe bağlı olarak Hello örnek bir işaretçi tooan tamsayı olan ancak bir işaretçi tooa olabilir daha karmaşık veri yapısı. Bu parametre hello geri çağırma işlevi toooperate hello çağıran paylaşılan durumuyla bu işlevin üzerinde sağlar.

Merhaba aygıt bir ileti aldığında hello kayıtlı geri çağırma işlevi çağrılır. Bu geri çağırma işlevini alır:

* Merhaba ileti kimliği ve hello iletisi bağıntı kimliği.
* Merhaba ileti içeriği.
* Tüm özel özellikler Başlangıç iletisi.

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    int* counter = (int*)userContextCallback;
    const char* buffer;
    size_t size;
    MAP_HANDLE mapProperties;
    const char* messageId;
    const char* correlationId;

    // Message properties
    if ((messageId = IoTHubMessage_GetMessageId(message)) == NULL)
    {
        messageId = "<null>";
    }

    if ((correlationId = IoTHubMessage_GetCorrelationId(message)) == NULL)
    {
        correlationId = "<null>";
    }

    // Message content
    if (IoTHubMessage_GetByteArray(message, (const unsigned char**)&buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        (void)printf("unable tooretrieve hello message data\r\n");
    }
    else
    {
        (void)printf("Received Message [%d]\r\n Message ID: %s\r\n Correlation ID: %s\r\n Data: <<<%.*s>>> & Size=%d\r\n", *counter, messageId, correlationId, (int)size, buffer, (int)size);
        // If we receive hello work 'quit' then we stop running
        if (size == (strlen("quit") * sizeof(char)) && memcmp(buffer, "quit", size) == 0)
        {
            g_continueRunning = false;
        }
    }

    // Retrieve properties from hello message
    mapProperties = IoTHubMessage_Properties(message);
    if (mapProperties != NULL)
    {
        const char*const* keys;
        const char*const* values;
        size_t propertyCount = 0;
        if (Map_GetInternals(mapProperties, &keys, &values, &propertyCount) == MAP_OK)
        {
            if (propertyCount > 0)
            {
                size_t index;

                printf(" Message Properties:\r\n");
                for (index = 0; index < propertyCount; index++)
                {
                    (void)printf("\tKey: %s Value: %s\r\n", keys[index], values[index]);
                }
                (void)printf("\r\n");
            }
        }
    }

    /* Some device specific action code goes here... */
    (*counter)++;
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Kullanım hello **IoTHubMessage\_GetByteArray** , bu örnekte bir dizedir işlev tooretrieve Başlangıç iletisi.

### <a name="uninitialize-hello-library"></a>Merhaba kitaplığı kapatması

Ne zaman gönderen olaylar işiniz bittiğinde ve iletileri alma, hello IOT kitaplığı kapatması. toodo, bu nedenle, işlev çağrısı aşağıdaki hello yürütün:

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Merhaba tarafından önceden ayrılmış hello kaynakları bu çağrıyı boşaltır **IoTHubClient\_CreateFromConnectionString** işlevi.

Gördüğünüz gibi kolay toosend olan ve hello ile iletilerini **IoTHubClient** kitaplığı. Merhaba kitaplığı hangi protokolü toouse dahil olmak üzere IOT Hub ile iletişim kurmasını hello ayrıntılarını işleyen (Merhaba Geliştirici hello açısından basit yapılandırma seçeneği budur).

Merhaba **IoTHubClient** kitaplığı da tooserialize hello verilerini Cihazınızı tooIoT Hub nasıl göndereceğini üzerinden kesin bir denetim sağlar. Bazı durumlarda bu düzeyi denetiminin bir avantajı, ancak diğer toobe ilgili istemediğiniz bir uygulama ayrıntısı şöyle. Merhaba durum söz konusuysa hello kullanarak düşünebilirsiniz **seri hale getirici** hello sonraki bölümde açıklanan kitaplığı.

## <a name="use-hello-serializer-library"></a>Merhaba seri hale getirici kitaplığını kullanma

Kavramsal olarak hello **seri hale getirici** kitaplığı hello üstünde bulunur **IoTHubClient** hello SDK'sı kitaplığı. Merhaba kullanan **IoTHubClient** IOT Hub, ancak ile iletişim için temel alınan hello kitaplığının hello yük ileti serileştirme postalarla hello geliştiriciden kaldırmak modelleme yetenekleri ekler. Nasıl bu kitaplığı works en iyi bir örnek gösterilmiştir.

İç hello **seri hale getirici** hello klasöründe [azure-IOT-sdk-c deposu](https://github.com/Azure/azure-iot-sdk-c), olan bir **örnekleri** adlı bir uygulama içeren klasörde **simplesample \_mqtt**. Merhaba Windows sürümü bu örnek, Visual Studio çözümü aşağıdaki hello içerir:

  ![](media/iot-hub-device-sdk-c-intro/14-simplesample_mqtt.PNG)

> [!NOTE]
> Bu projeyi Visual Studio 2017 içinde açarsanız, hello istemleri tooretarget hello proje toohello en son sürümünü kabul edin.

Merhaba önceki örnek olarak, bunun birkaç NuGet paketlerini içerir:

* Microsoft.Azure.C.SharedUtility
* Microsoft.Azure.IoTHub.MqttTransport
* Microsoft.Azure.IoTHub.IoTHubClient
* Microsoft.Azure.IoTHub.Serializer
* Microsoft.Azure.umqtt

Bu paketleri hello önceki örnekteki çoğunu gördünüz ancak **Microsoft.Azure.IoTHub.Serializer** yenidir. Bu paket hello kullandığınızda gereklidir **seri hale getirici** kitaplığı.

Merhaba örnek uygulaması hello uyarlamasını hello bulabilirsiniz **simplesample\_mqtt.c** dosya.

Hello aşağıdaki bölümlerde bu örnek anahtar bölümleri hello size yol gösterir.

### <a name="initialize-hello-library"></a>Merhaba kitaplığı başlatılamıyor

Merhaba ile çalışma toostart **seri hale getirici** çağrısı hello başlatma API'leri kitaplığı:

```c
if (serializer_init(NULL) != SERIALIZER_OK)
{
    (void)printf("Failed on serializer_init\r\n");
}
else
{
    IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle = IoTHubClient_LL_CreateFromConnectionString(connectionString, MQTT_Protocol);
    srand((unsigned int)time(NULL));
    int avgWindSpeed = 10;

    if (iotHubClientHandle == NULL)
    {
        (void)printf("Failed on IoTHubClient_LL_Create\r\n");
    }
    else
    {
        ContosoAnemometer* myWeather = CREATE_MODEL_INSTANCE(WeatherStation, ContosoAnemometer);
        if (myWeather == NULL)
        {
            (void)printf("Failed on CREATE_MODEL_INSTANCE\r\n");
        }
        else
        {
...
```

Merhaba çağrısı toohello **seri hale getirici\_init** işlevi tek seferlik bir çağrı ve başlatır hello temel kitaplığı. Sonra hello çağırın **IoTHubClient\_ÜM\_CreateFromConnectionString** hello olduğu gibi aynı API hello işlevi **IoTHubClient** örnek. Bu çağrı, cihaz bağlantı dizesini ayarlar (Bu da hello Protokolü burada seçtiğiniz çağrıdır toouse istediğiniz). Bu örnek hello taşıma olarak MQTT kullanır, ancak AMQP veya HTTP kullanabilirsiniz.

Son olarak, hello çağrısı **oluşturma\_modeli\_örneği** işlevi. **WeatherStation** hello modelinin hello ad alanıdır ve **ContosoAnemometer** hello modeli hello adıdır. Merhaba model örneği oluşturulduktan sonra ileti toostart gönderme ve alma kullanabilirsiniz. Ancak, önemli toounderstand hangi bir modeldir olur.

### <a name="define-hello-model"></a>Merhaba modeli tanımlayın

Merhaba modelinde **seri hale getirici** kitaplığı tanımlar Cihazınızı tooIoT olarak adlandırılan, Hub ve hello iletiler gönderebilir Merhaba iletileri *Eylemler* alabileceği dil modelleme hello içinde. C makroları hello gibi bir dizi kullanılarak bir modeli tanımlamak **simplesample\_mqtt** örnek uygulama:

```c
BEGIN_NAMESPACE(WeatherStation);

DECLARE_MODEL(ContosoAnemometer,
WITH_DATA(ascii_char_ptr, DeviceId),
WITH_DATA(int, WindSpeed),
WITH_ACTION(TurnFanOn),
WITH_ACTION(TurnFanOff),
WITH_ACTION(SetAirResistance, int, Position)
);

END_NAMESPACE(WeatherStation);
```

Merhaba **başlamak\_ad alanı** ve **son\_ad alanı** makroları iki bağımsız değişken olarak hello modelinin hello ad alın. Bu makrolar arasında herhangi bir şey hello tanımını modeli veya modelleri ve hello modelleri kullanma hello veri yapılarını olduğunu beklenir.

Bu örnekte, yok adlı tek bir model **ContosoAnemometer**. Bu model Cihazınızı tooIoT Hub gönderebilirsiniz veri iki parça tanımlar: **DeviceID** ve **WindSpeed**. Ayrıca Cihazınızı alabilir üç eylem (iletileri) tanımlar: **TurnFanOn**, **TurnFanOff**, ve **SetAirResistance**. Her veri öğesi türüne sahip ve her eylemi bir ad (ve isteğe bağlı bir parametre kümesi) sahiptir.

Merhaba verilere ve eylemlere hello modelde tanımlanmış toosend iletileri tooIoT hub'ı kullanın ve gönderilen toomessages toohello aygıt yanıt API yüzeyi tanımlayın. Bu model kullanımı örnek en iyi anlaşılmalıdır.

### <a name="send-messages"></a>İletileri gönder

Merhaba modeli tooIoT Hub gönderebilirsiniz hello verileri tanımlar. Bu örnekte, anlamına hello birini hello kullanılarak tanımlanan iki veri öğeleri **WITH_DATA** makrosu. Çeşitli adımları gerekli toosend vardır **DeviceID** ve **WindSpeed** tooan IOT hub'ı değerleri. Merhaba, ilk toosend istediğiniz tooset hello veri şöyledir:

```c
myWeather->DeviceId = "myFirstDevice";
myWeather->WindSpeed = avgWindSpeed + (rand() % 4 + 2);
```

Hello daha önce tanımladığınız modeli tooset hello değerleri üyeleri ayarlayarak sağlayan bir **yapısı**. Ardından, selamlama iletisine toosend istediğiniz sıralayın:

```c
unsigned char* destination;
size_t destinationSize;
if (SERIALIZE(&destination, &destinationSize, myWeather->DeviceId, myWeather->WindSpeed) != CODEFIRST_OK)
{
    (void)printf("Failed tooserialize\r\n");
}
else
{
    sendMessage(iotHubClientHandle, destination, destinationSize);
    free(destination);
}
```

Bu kod hello cihaz bulut tooa arabellek serileştiren (tarafından başvurulan **hedef**). Merhaba kod sonra hello çağırır **sendMessage** toosend hello ileti tooIoT Hub işlev:

```c
static void sendMessage(IOTHUB_CLIENT_LL_HANDLE iotHubClientHandle, const unsigned char* buffer, size_t size)
{
    static unsigned int messageTrackingId;
    IOTHUB_MESSAGE_HANDLE messageHandle = IoTHubMessage_CreateFromByteArray(buffer, size);
    if (messageHandle == NULL)
    {
        printf("unable toocreate a new IoTHubMessage\r\n");
    }
    else
    {
        if (IoTHubClient_LL_SendEventAsync(iotHubClientHandle, messageHandle, sendCallback, (void*)(uintptr_t)messageTrackingId) != IOTHUB_CLIENT_OK)
        {
            printf("failed toohand over hello message tooIoTHubClient");
        }
        else
        {
            printf("IoTHubClient accepted hello message for delivery\r\n");
        }
        IoTHubMessage_Destroy(messageHandle);
    }
    messageTrackingId++;
}
```


İkinci toolast parametresinin hello **IoTHubClient\_ÜM\_SendEventAsync** hello veri başarıyla gönderildiğinde çağrılan bir başvuru tooa geri çağırma işlevi. Merhaba örnek hello geri çağırma işlevi şöyledir:

```c
void sendCallback(IOTHUB_CLIENT_CONFIRMATION_RESULT result, void* userContextCallback)
{
    unsigned int messageTrackingId = (unsigned int)(uintptr_t)userContextCallback;

    (void)printf("Message Id: %u Received.\r\n", messageTrackingId);

    (void)printf("Result Call Back Called! Result is: %s \r\n", ENUM_TO_STRING(IOTHUB_CLIENT_CONFIRMATION_RESULT, result));
}
```

Merhaba ikinci bir işaretçi toouser bağlamı parametredir; aynı işaretçi geçirilen çok hello**IoTHubClient\_ÜM\_SendEventAsync**. Bu durumda, basit bir sayaç hello bağlamı olduğu, ancak istediğiniz herhangi bir şey olabilir.

Tüm olan toosending cihaz bulut iletilerini yoktur. Merhaba toocover sol yalnızca şeydir nasıl tooreceive iletileri.

### <a name="receive-messages"></a>İleti alma

Bir ileti alma çalışır benzer şekilde iletileri çalışma hello toohello yöntemini **IoTHubClient** kitaplığı. İlk olarak, bir ileti geri çağırma işlevini kaydedin:

```c
if (IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, IoTHubMessage, myWeather) != IOTHUB_CLIENT_OK)
{
    printf("unable tooIoTHubClient_SetMessageCallback\r\n");
}
else
{
...
```

Ardından, bir ileti alındığında çağrılan hello geri çağırma işlevi yazın:

```c
static IOTHUBMESSAGE_DISPOSITION_RESULT IoTHubMessage(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    IOTHUBMESSAGE_DISPOSITION_RESULT result;
    const unsigned char* buffer;
    size_t size;
    if (IoTHubMessage_GetByteArray(message, &buffer, &size) != IOTHUB_MESSAGE_OK)
    {
        printf("unable tooIoTHubMessage_GetByteArray\r\n");
        result = IOTHUBMESSAGE_ABANDONED;
    }
    else
    {
        /*buffer is not zero terminated*/
        char* temp = malloc(size + 1);
        if (temp == NULL)
        {
            printf("failed toomalloc\r\n");
            result = IOTHUBMESSAGE_ABANDONED;
        }
        else
        {
            (void)memcpy(temp, buffer, size);
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

Bu kodu Demirbaş.--onu sahip hello aynı için herhangi bir çözümü. Bu işlev hello iletiyi alır ve bunu toohello uygun işlevi hello çağrısı ile çok yönlendirme mvc'deki**yürütme\_KOMUTU**. adlı hello işlevi bu noktada hello Eylemler modelinizdeki hello tanımını bağlıdır.

Bir eylem modelinizde tanımladığınızda, gerekli tooimplement Cihazınızı hello karşılık gelen ileti aldığında çağrılan işlev. Örneğin bu eylemi modelinizi tanımlar:

```c
WITH_ACTION(SetAirResistance, int, Position)
```

Bu imza işleviyle tanımlayın:

```c
EXECUTE_COMMAND_RESULT SetAirResistance(ContosoAnemometer* device, int Position)
{
    (void)device;
    (void)printf("Setting Air Resistance Position too%d.\r\n", Position);
    return EXECUTE_COMMAND_SUCCESS;
}
```

Nasıl hello hello işlevi hello eylemin hello modelinde hello adı adıyla ve hello işlevi hello parametreleriyle hello eylem için belirtilen başlangıç parametreleri aynı unutmayın. Merhaba ilk parametresi, her zaman gereklidir ve modelinizi bir işaretçi toohello örneğini içerir.

Merhaba karşılık gelen işlev Hello cihaz Bu imza eşleşen bir ileti aldığında çağrılır. Bu nedenle, yanı sıra tooinclude hello Demirbaş kod sahip **IoTHubMessage**, olan modelinizde tanımlı her eylem için basit bir işlevin tanımlamanın yalnızca sağlasa da iletileri alma.

### <a name="uninitialize-hello-library"></a>Merhaba kitaplığı kapatması

Ne zaman verileri gönderilirken işiniz bittiğinde ve iletileri alma, hello IOT kitaplığı kapatması:

```c
...
        DESTROY_MODEL_INSTANCE(myWeather);
    }
    IoTHubClient_LL_Destroy(iotHubClientHandle);
}
serializer_deinit();
```

Bu üç işlevlerin her biri daha önce açıklanan hello üç başlatma işlevleriyle hizalar. Bu API'larını çağırma önceden ayrılan kaynakları serbest sağlar.

## <a name="next-steps"></a>Sonraki Adımlar

Bu makalede ele alınan hello hello kitaplıklarında kullanma temelleri hello **C için Azure IOT cihaz SDK'sı**. Merhaba SDK, mimarisi ve tooget Windows örnekleri hello ile çalışmaya nasıl başlatılacağını içereceği yeterli bilgi toounderstand sağlanan. Merhaba sonraki makalede açıklayarak hello SDK hello açıklaması devam [hello IoTHubClient Kitaplığı hakkında daha fazla](iot-hub-device-sdk-c-iothubclient.md).

IOT hub'ı geliştirme hakkında daha fazla toolearn bkz hello [Azure IOT SDK'ları][lnk-sdks].

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]

[lnk-file upload]: iot-hub-csharp-csharp-file-upload.md
[lnk-create-hub]: iot-hub-rm-template-powershell.md
[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
