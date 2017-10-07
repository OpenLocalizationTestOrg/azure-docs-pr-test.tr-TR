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
# <a name="azure-iot-device-sdk-for-c--more-about-iothubclient"></a>C – IoTHubClient hakkında daha fazla bilgi için Azure IOT cihaz SDK'sı
Merhaba [ilk makale](iot-hub-device-sdk-c-intro.md) bu sunulan serisi hello içinde **C için Azure IOT cihaz SDK'sı**. Bu makale, SDK içinde iki Mimari katman vardır açıklanmıştır. Merhaba Hello temel olan **IoTHubClient** doğrudan IOT Hub ile iletişim yöneten kitaplığı. Ayrıca hello olan **seri hale getirici** tooprovide seri hale getirme hizmetleri üzerinde üst o derlemeler kitaplığı. Bu makalede ek ayrıntı üzerinde hello sağlarız **IoTHubClient** kitaplığı.

Merhaba önceki makalede açıklanan nasıl toouse hello **IoTHubClient** kitaplığı toosend olayları tooIoT Hub ve iletileri alabilirsiniz. Bu makalede bu tartışma nasıl toomore tam olarak yönetmek açıklayarak genişletir *zaman* toohello Tanıtımı veri gönderip **düşük düzeyli API'leri**. Ayrıca açıklayacağız nasıl tooattach özellikleri tooevents (ve gelen iletileri almak) hello özelliklerinde işleme hello özelliğini kullanarak **IoTHubClient** kitaplığı. Son olarak, farklı şekillerde toohandle ek açıklaması sağlarız IOT Hub'ından alınan iletileri.

Merhaba makale birkaç cihaz kimlik bilgileri hakkında daha fazla bilgi ve nasıl toochange hello hello davranışını dahil olmak üzere çeşitli konuları kapsayan sonucuna **IoTHubClient** yapılandırma seçenekleri üzerinden.

Merhaba kullanacağız **IoTHubClient** SDK Bu konularda tooexplain örnekleri. Merhaba toofollow boyunca istiyorsanız bkz **ıothub\_istemci\_örnek\_http** ve **ıothub\_istemci\_örnek\_amqp** C. hello aşağıdaki bölümlerde açıklanan her şey bu örnekleri gösterilmiştir için hello Azure IOT cihaz SDK'sı bulunan uygulamalar.

Merhaba bulabilirsiniz [ **C için Azure IOT cihaz SDK'sı** ](https://github.com/Azure/azure-iot-sdk-c) GitHub depo ve görünüm ayrıntılarını hello hello API [C API Başvurusu](https://azure.github.io/azure-iot-sdk-c/index.html).

## <a name="hello-lower-level-apis"></a>Merhaba düşük düzeyli API'leri
Merhaba önceki makalede açıklanan hello temel hello işleyişi **IotHubClient** hello Merhaba içeriğine içinde **ıothub\_istemci\_örnek\_amqp** uygulama. Örneğin, nasıl tooinitialize hello bu kodu kullanarak kitaplığı açıklanmıştır.

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

Ayrıca, bu kullanarak toosend olayları nasıl işlev çağrısı açıklanmaktadır.

```
IoTHubClient_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message);
```

Merhaba makale, bir geri çağırma işlevini kaydederek tooreceive nasıl iletileri de açıklanmaktadır.

```
int receiveContext = 0;
IoTHubClient_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext);
```

Merhaba makale ayrıca nasıl kullanarak toofree kaynakları hello aşağıdaki gibi kod gösterdi.

```
IoTHubClient_Destroy(iotHubClientHandle);
```

Ancak bu API'lerden yardımcı işlevleri tooeach vardır:

* IoTHubClient\_ÜM\_CreateFromConnectionString
* IoTHubClient\_ÜM\_SendEventAsync
* IoTHubClient\_ÜM\_SetMessageCallback
* IoTHubClient\_ÜM\_yok

Tüm bu işlevler "Tümü" Merhaba API adına dahil et. Dışında bu işlevlerin her biri hello parametrelerinin aynı tootheir ÜM olmayan ortaklarınıza olan. Ancak, bu işlevler hello davranışını önemli bir şekilde farklıdır.

Çağırdığınızda **IoTHubClient\_CreateFromConnectionString**, hello temel kitaplıkları hello arka planda çalışan yeni bir iş parçacığı oluşturabilir. Bu iş parçacığı olayları gönderir ve IOT Hub'ından, iletileri alır. Bu tür bir iş parçacığı hello "Tümü" API'leri ile çalışırken oluşturulur. Merhaba arka plan iş parçacığı Hello oluşturulmasını kolaylık toohello geliştiricisi değildir. Açıkça olayları ileti gönderme ve IOT Hub'ından--hello arka planda otomatik olarak gerçekleşir alma hakkında tooworry yok. Buna karşılık, hello "Tümü" API'leri size IOT Hub ile iletişim açık denetime ihtiyacınız varsa.

toounderstand bu daha iyi bir örneğe bakalım:

Çağırdığınızda **IoTHubClient\_SendEventAsync**, ne gerçekte yaptığınız hello olay arabellekte koyuyor. Merhaba çağırdığınızda oluşturulan arka plan iş parçacığı **IoTHubClient\_CreateFromConnectionString** sürekli olarak bu arabellek izler ve herhangi bir veri gönderir tooIoT Hub içerir. Hello adresindeki hello arka planda bu hello aynı zaman böyle ana iş parçacığının başka işler gerçekleştirme.

Benzer şekilde, bir geri çağırma işlevini kullanarak iletileri için kaydettiğinizde **IoTHubClient\_SetMessageCallback**, hello SDK toohave hello arka plan sunuculardaki gerektiğini belirten bir ileti olduğunda iş parçacığı çağırma hello geri çağırma işlevi alınan, hello ana iş parçacığı bağımsızdır.

Merhaba "Tümü" API'leri arka plan iş parçacığı oluştur. Bunun yerine, yeni bir API tooexplicitly gönderme çağrılmalıdır ve IOT Hub'ından veri alırsınız. Bu örnekte aşağıdaki hello gösterilmiştir.

Merhaba **ıothub\_istemci\_örnek\_http** SDK gösteren hello dahil uygulama hello düşük düzeyli API'leri. Bu örnekte, hello aşağıdaki gibi kod ile olayları tooIoT Hub gönder:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Message_%d_From_IoTHubClient_LL_Over_HTTP", i);
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));

IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Merhaba ilk üç satırını hello iletisi oluşturun ve hello son satırında hello olay gönderir. Ancak, daha önce belirtildiği gibi "Merhaba veriler yalnızca bir arabellek yerleştirilir hello olay anlamına gelir gönderme". Biz çağırdığınızda hiçbir şey hello ağ üzerinde aktarılan **IoTHubClient\_ÜM\_SendEventAsync**. Sipariş tooactually giriş hello veri tooIoT içinde Hub, çağırmalısınız **IoTHubClient\_ÜM\_DoWork**, bu örnekteki gibi:

```
while (1)
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Bu kod (Merhaba gelen **ıothub\_istemci\_örnek\_http** uygulama) art arda çağırır **IoTHubClient\_ÜM\_DoWork** . Her zaman **IoTHubClient\_ÜM\_DoWork** olan çağrılır, hello arabellek tooIoT Hub bazı olayların gönderir ve toohello aygıt gönderilen sıraya alınmış bir iletiyi alır. Biz iletiler için bir geri çağırma işlevini kaydolduysanız hello geri çağırma (herhangi bir ileti kuyruğa varsayılarak) çağrıldıktan sonra hello ikinci durumda anlamına gelir. Biz bu tür bir geri çağırma işlevi hello aşağıdaki gibi kod ile kayıtlı:

```
IoTHubClient_LL_SetMessageCallback(iotHubClientHandle, ReceiveMessageCallback, &receiveContext)
```

Hello neden **IoTHubClient\_ÜM\_DoWork** genellikle adlandırılır bir döngü değil, her kez çağırıldığında, gönderir *bazı* arabelleğe alınmış olayları tooIoT Hub ve alır *hello sonraki* iletisi sıraya hello aygıt için. Her çağrı toosend tüm arabelleğe alınmış olayları garantisi yoktur veya tooretrieve tüm kuyruğa alınan iletileri. Tüm olaylar hello arabellek ve ardından başka bir işlem devam toosend istiyorsanız hello aşağıdaki gibi kod ile bu döngü değiştirebilirsiniz:

```
IOTHUB_CLIENT_STATUS status;

while ((IoTHubClient_LL_GetSendStatus(iotHubClientHandle, &status) == IOTHUB_CLIENT_OK) && (status == IOTHUB_CLIENT_SEND_STATUS_BUSY))
{
    IoTHubClient_LL_DoWork(iotHubClientHandle);
    ThreadAPI_Sleep(1000);
}
```

Bu kod çağırır **IoTHubClient\_ÜM\_DoWork** hello arabelleği tüm olayları tooIoT Hub gönderilen kadar. Bu ayrıca tüm sıraya alınan iletileri alınmış olan anlamına gelmez unutmayın. Bunun nedeni hello parçası "tümü" iletileri denetleme gibi belirleyici bir eylem olmadığından emin olur. "Tüm" Merhaba iletileri almak, ancak başka bir toohello aygıt gönderilir ne olur hemen sonra? Daha iyi bir şekilde toodeal, ile programlı bir zaman aşımı ile olur. Örneğin, çağrılması her zaman hello ileti geri çağırma işlevi bir süreölçer sıfırlanamadı. Örneğin, hiçbir hello en son alınan ileti yok, ardından mantığı toocontinue işleme yazabilirsiniz *X* saniye.

Ne zaman tamamlanmış ingressing olayları olduğunuz ve iletilerini alma emin toocall hello karşılık gelen işlevi tooclean kaynakları olabilir.

```
IoTHubClient_LL_Destroy(iotHubClientHandle);
```

Temel olarak yalnızca bir dizi API toosend yoktur ve arka plan iş parçacığı ve başka bir dizi hello arka plan iş parçacığı olmadan aynı şeyi hello API ile verilerini alma. Geliştiricilerin çok hello olmayan - ÜM API'leri tercih edebilirsiniz, ancak hello Geliştirici ağ aktarımları üzerinde açık denetim istediğinde hello düşük düzeyli API'leri yararlıdır. Örneğin, bazı aygıtlar veri zaman ve yalnızca giriş olayları belirtilen aralıklarla (örneğin, saatte bir kez veya günde bir kez) toplar. Merhaba IOT Hub'ından veri gönderip alırken özelliği tooexplicitly denetim hello alt düzey API'ler sağlar. Başkalarının yalnızca hello Basitlik alt düzey API'ler sağlar, hello tercih eder. Bazı iş oluşmasını hello arka planda yerine hello ana iş parçacığı her şeyi olur.

Seçtiğiniz hangi modeli olması emin toobe tutarlı hangi API'leri kullanın. Çağırarak başlatırsanız **IoTHubClient\_ÜM\_CreateFromConnectionString**, herhangi bir izleme iş için alt düzey API'leri karşılık gelen hello yalnızca kullandığınızdan emin olun:

* IoTHubClient\_ÜM\_SendEventAsync
* IoTHubClient\_ÜM\_SetMessageCallback
* IoTHubClient\_ÜM\_yok
* IoTHubClient\_ÜM\_DoWork

Merhaba ters de geçerlidir. İle başlatırsanız, **IoTHubClient\_CreateFromConnectionString**, kullanım hello sonra ÜM olmayan API'ler herhangi bir ek işlem için.

Merhaba Hello Azure IOT cihazı SDK C için bkz: **ıothub\_istemci\_örnek\_http** uygulama hello tam bir örnek için alt düzey API'leri. Merhaba **ıothub\_istemci\_örnek\_amqp** uygulama tam bir örnek için hello olmayan - ÜM API'leri başvuruda bulunabilir.

## <a name="property-handling"></a>Özellik işleme
Verileri gönderilirken açıklanan zaman kadarki biz toohello hello ileti gövdesi başvuran. Örneğin, bu kod göz önünde bulundurun:

```
EVENT_INSTANCE message;
sprintf_s(msgText, sizeof(msgText), "Hello World");
message.messageHandle = IoTHubMessage_CreateFromByteArray((const unsigned char*)msgText, strlen(msgText));
IoTHubClient_LL_SendEventAsync(iotHubClientHandle, message.messageHandle, SendConfirmationCallback, &message)
```

Bu örnekte, "Hello World." Merhaba metinle ileti tooIoT Hub gönderilir. Ancak, IOT Hub ayrıca özellikleri toobe ekli tooeach ileti imkan tanır. Ekli toohello ileti olabilir ad/değer çiftleri özelliklerdir. Örneğin, biz hello önceki kod tooattach özellik toohello iletisi değiştirebilirsiniz:

```
MAP_HANDLE propMap = IoTHubMessage_Properties(message.messageHandle);
sprintf_s(propText, sizeof(propText), "%d", i);
Map_AddOrUpdate(propMap, "SequenceNumber", propText);
```

Arayarak Başlat **IoTHubMessage\_özellikleri** ve onu bizim ileti hello tanıtıcısı. Ne biz geri alırsınız bir **harita\_İŞLEMEK** bize Özellikler ekleme toostart etkinleştirir başvuru. Merhaba ikinci çağırarak gerçekleştirilir **harita\_örnek**, başvuru tooa harita aldığı\_TANITICISI, hello özellik adı ve Başlangıç özellik değeri. Bu API ile biz istediğiniz sayıda özellik ekleyebiliriz.

Ne zaman hello olay okunur gelen **olay hub'ları**, hello alıcı hello özellikler numaralandırılmaya ve bunlara karşılık gelen değerler alır. Örneğin, .NET içinde bu hello erişerek gerçekleştirilmesi [hello EventData nesne üzerindeki özellikleri koleksiyonu](https://msdn.microsoft.com/library/azure/microsoft.servicebus.messaging.eventdata.properties.aspx).

Merhaba önceki örnekte, biz özellikleri tooan olayı biz tooIoT Hub Gönder ekleniyor. Özellikler, IOT Hub'ından alınan ekli toomessages de olabilir. Bir ileti tooretrieve özelliklerinden istiyoruz, hello aşağıdaki gibi kod bizim ileti geri çağırma işlevini kullanabilirsiniz:

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

Çağrı çok hello**IoTHubMessage\_özellikleri** döndürür hello **harita\_İŞLEMEK** başvuru. Biz daha sonra bu başvuruyu çok geçirin**harita\_GetInternals** tooobtain başvuru tooan dizisi hello ad/değer çiftleri (bir sayım hello özelliklerinin yanı sıra). Bu noktada hello özellikleri tooget toohello değerleri istiyoruz numaralandırma, atmaktan değil.

Uygulamanızda toouse özellikleri yok. Ancak, tooset ihtiyacınız varsa bunları olaylarına veya bunları gelen iletileri, hello almak **IoTHubClient** kitaplığı kolaylaştırır.

## <a name="message-handling"></a>İleti işleme
Daha önce belirtildiği gibi iletiler geldiğinde IOT hub'ı hello **IoTHubClient** kitaplığı yanıt kayıtlı geri çağırma işlevini çağırarak. Bazı ek açıklama hak bu işlevin dönüş parametresi yok. Merhaba hello geri çağırma işlevinin bir alıntı işte **ıothub\_istemci\_örnek\_http** örnek uygulama:

```
static IOTHUBMESSAGE_DISPOSITION_RESULT ReceiveMessageCallback(IOTHUB_MESSAGE_HANDLE message, void* userContextCallback)
{
    . . .
    return IOTHUBMESSAGE_ACCEPTED;
}
```

Merhaba dönüş türü olduğuna dikkat edin **IOTHUBMESSAGE\_değerlendirme\_sonuç** ve bu belirli durumda döndürürüz **IOTHUBMESSAGE\_kabul edilen**. Biz dönebilirsiniz bu işlevden değişiklik nasıl hello diğer değerler **IoTHubClient** kitaplığı tepki verdiğini toohello ileti geri çağırma. Merhaba seçenekler aşağıda belirtilmiştir.

* **IOTHUBMESSAGE\_kabul edilen** – selamlama iletisine başarıyla işlendiğinden. Merhaba **IoTHubClient** kitaplığı değil hello'yla yeniden hello geri çağırma işlevi çağırma aynı ileti.
* **IOTHUBMESSAGE\_reddedildi** – selamlama iletisine değil işlendiği ve yoktur hiçbir desire toodo bu nedenle de hello gelecekteki. Merhaba **IoTHubClient** kitaplığı çağrılamadı hello geri çağırma işlevi yeniden hello ile aynı ileti.
* **IOTHUBMESSAGE\_ABANDONED** – selamlama iletisine değil işlendiği başarıyla ancak hello **IoTHubClient** kitaplığı hello'yla yeniden hello geri çağırma işlevi çağırma aynı ileti.

Merhaba ilk iki, hello dönüş kodları **IoTHubClient** kitaplığı hello ileti belirten Hub hello aygıt sıradan silinir ve gerekir yeniden teslim edilmedi ileti tooIoT gönderir. Merhaba net etkisi aynı hello olduğu (selamlama iletisine hello aygıt sıradan silinir), ancak selamlama iletisine kabul edilen veya reddedilen hala kaydedilir.  Bu ayrım kaydı geri bildirim için dinleyen ve bir cihaz kabul ettiğini veya belirli bir ileti reddedildi varsa öğrenmek yararlı toosenders hello iletisinin olur.

Merhaba son durumda tooIoT Hub ayrıca bir ileti gönderilir, ancak bu hello ileti yeniden teslim edilebilir gösterir. Genellikle bazı hatayla karşılaşırsanız, ancak tootry tooprocess ileti yeniden hello isterseniz bir ileti abandon. Buna karşılık, bir ileti reddetme kurtarılamaz bir hatayla karşılaştığında (veya yalnızca tooprocess selamlama iletisine istemediğinize karar verirseniz) uygundur.

Böylece hello istediğiniz hello davranışı tasarlanmalıdır herhangi bir durumda, hello farklı dönüş kodları unutmayın **IoTHubClient** kitaplığı.

## <a name="alternate-device-credentials"></a>Alternatif aygıt kimlik bilgisi
Daha önce açıklandığı gibi ilk şey toodo hello ile çalışırken hello **IoTHubClient** kitaplığıdır tooobtain bir **IOTHUB\_istemci\_İŞLEMEK** hello gibi bir çağrıyla Aşağıdaki:

```
IOTHUB_CLIENT_HANDLE iotHubClientHandle;
iotHubClientHandle = IoTHubClient_CreateFromConnectionString(connectionString, AMQP_Protocol);
```

bağımsız değişkenler çok hello**IoTHubClient\_CreateFromConnectionString** hello cihaz bağlantı dizesini ve kullanırız toocommunicate IOT Hub ile Merhaba protokolü belirten bir parametre. Merhaba cihaz bağlantı dizesi şu şekilde görünen bir biçime sahiptir:

```
HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY
```

Bu dize bilgilerinde dört adet vardır: IOT hub'ı adı, IOT hub'ı soneki, cihaz kimliği ve paylaşılan erişim anahtarı. Hello Azure portal, IOT hub örneği oluşturduğunuzda, IOT hub'ı hello tam etki alanı adı (FQDN) elde — Bu, hello IOT hub adını (FQDN hello hello ilk bölümü) ve hello IOT hub soneki (Merhaba FQDN kalanı hello) sunar. IOT Hub ile Cihazınızı kaydederken hello cihaz kimliği ve hello paylaşılan erişim anahtarı almanız (hello açıklandığı gibi [önceki makalede](iot-hub-device-sdk-c-intro.md)).

**IoTHubClient\_CreateFromConnectionString** tek yönlü tooinitialize hello kitaplığı sağlar. İsterseniz, yeni bir oluşturabileceğiniz **IOTHUB\_istemci\_İŞLEMEK** hello cihaz bağlantı dizesi yerine bu tek tek parametreleri kullanarak. Bu kod aşağıdaki hello ile sağlanır:

```
IOTHUB_CLIENT_CONFIG iotHubClientConfig;
iotHubClientConfig.iotHubName = "";
iotHubClientConfig.deviceId = "";
iotHubClientConfig.deviceKey = "";
iotHubClientConfig.iotHubSuffix = "";
iotHubClientConfig.protocol = HTTP_Protocol;
IOTHUB_CLIENT_HANDLE iotHubClientHandle = IoTHubClient_LL_Create(&iotHubClientConfig);
```

Bunu hello gerçekleştirir aynı **IoTHubClient\_CreateFromConnectionString**.

Toouse istersiniz belirgin görünebilir **IoTHubClient\_CreateFromConnectionString** başlatma daha ayrıntılı bu yöntem yerine. IOT Hub ' bir aygıtı kaydederken bir cihaz kimliği ve aygıt anahtarı (olmayan bir bağlantı dizesi) aldığınızdır olduğunu, ancak unutmayın. Merhaba *aygıt explorer* hello sunulan SDK aracı [önceki makalede](iot-hub-device-sdk-c-intro.md) hello kitaplıklarında kullanır **Azure IOT hizmeti SDK'sını** toocreate hello cihaz bağlantı dizesinden Merhaba cihaz kimliği, aygıt anahtarı ve IOT Hub ana bilgisayar adı. Bu nedenle çağırma **IoTHubClient\_ÜM\_oluşturma** , kaydettiğinden tercih olabilir hello adım bir bağlantı dizesi oluşturma. Hangi yöntemi uygundur kullanın.

## <a name="configuration-options"></a>Yapılandırma seçenekleri
Şimdiye kadar her şeyi hello şekilde hello hakkında anlatılan **IoTHubClient** kitaplığı works varsayılan davranışını yansıtır. Ancak, hello kitaplığı nasıl çalıştığını toochange ayarlayabileceğiniz birkaç seçenek vardır. Bu hello yararlanarak gerçekleştirilir **IoTHubClient\_ÜM\_SetOption** API. Bu örneği göz önünde bulundurun:

```
unsigned int timeout = 30000;
IoTHubClient_LL_SetOption(iotHubClientHandle, "timeout", &timeout);
```

Birkaç yaygın olarak kullanılan seçenekler şunlardır:

* **SetBatching** (Boole) – varsa **doğru**, sonra gönderilen veriler tooIoT Hub toplu olarak gönderilir. Varsa **yanlış**, ayrı ayrı gönderilen iletileri sonra. Merhaba varsayılandır **false**. Bu hello Not **SetBatching** seçeneği yalnızca toohello HTTP protokolü ve değil toohello MQTT veya AMQP protokollerini uygulanır.
* **Zaman aşımı** (imzasız int) – bu değer milisaniye cinsinden gösterilir. Bir HTTP isteğinin ya da bir yanıt alırken bu süreden daha uzun sürer gönderme, ardından hello bağlantı zaman aşımına uğradı.

seçenek toplu işleme hello önemlidir. Varsayılan olarak, kitaplık ingresses olayları ayrı ayrı hello (tek bir olay ne olursa olsun çok geçirdiğiniz olan**IoTHubClient\_ÜM\_SendEventAsync**). Seçenek toplu işleme hello ise **doğru**, hello kitaplığı hello arabellek (yukarı, IOT hub'ı kabul toohello maksimum ileti boyutu) gelen mümkün olduğunca çok olayları toplar.  Merhaba olay toplu tooIoT Hub tek bir gönderilen HTTP çağrısıyla (Merhaba olayları tek tek paketlenmiş bir JSON dizisine). Ağ gidiş dönüş azaltma bu yana genellikle toplu etkinleştirme büyük performans artışları sonuçlanır. Tek bir olay toplu ile HTTP üstbilgi kümesi yerine tek tek her olay için üstbilgi kümesi gönderme beri bant genişliği de önemli ölçüde azaltır. Tipik olarak belirli bir nedenle toodo Aksi durumda olmadığı sürece tooenable toplu işleme isteyeceksiniz.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede ayrıntı hello davranışını hello içinde **IoTHubClient** kitaplığı bulunan hello **C için Azure IOT cihaz SDK'sı**. Bu bilgiyle hello hello özelliklerini iyi anlamış olmanız **IoTHubClient** kitaplığı. Merhaba [sonraki makalede](iot-hub-device-sdk-c-serializer.md) hello üzerinde benzer ayrıntı sağlar **seri hale getirici** kitaplığı.

IOT hub'ı geliştirme hakkında daha fazla toolearn bkz hello [Azure IOT SDK'ları][lnk-sdks].

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]

[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
