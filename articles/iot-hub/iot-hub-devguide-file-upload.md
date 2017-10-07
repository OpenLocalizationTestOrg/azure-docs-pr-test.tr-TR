---
title: "aaaUnderstand Azure IOT Hub dosya karşıya yükleme | Microsoft Docs"
description: "Geliştirici Kılavuzu - kullanım hello dosya karşıya yükleme özelliğini IOT hub'ı toomanage bir aygıt tooan Azure depolama blob kapsayıcısından dosyaları karşıya yükleme."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a0427925-3e40-4fcd-96c1-2a31d1ddc14b
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: d44f9303ead4fa282dc0baf70887af1b8a03293d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-with-iot-hub"></a>IOT Hub ile dosyaları karşıya yükleme

Merhaba ayrıntılı olarak [IOT Hub uç noktaları] [ lnk-endpoints] makale, bir cihaz başlatabilir dosyanın karşıya bir aygıt'e yönelik uç noktası aracılığıyla bir bildirim göndererek (**/devices/ {DeviceID} /dosyaları**). Bir cihaz IOT hub'ı bir karşıya yükleme tamamlanana bildirdiğinde, IOT hub'ı hello aracılığıyla dosya karşıya yükleme bildirim iletisi gönderir **/messages/servicebound/filenotifications** service'e yönelik uç noktası.

Azure depolama hesabı dağıtıcısı tooan ilişkili olarak iletileri IOT Hub kendisi aracılığıyla aracılığı yapmaktan yerine IOT Hub yerine davranır. Bir cihaz IOT Hub'belirli toohello dosya hello cihaz depolama belirtecinden tooupload istediği ister. Merhaba SAS URI'sini tooupload hello dosya toostorage Hello aygıt kullanır ve hello karşıya yükleme tamamlandığında hello cihaz tamamlama tooIoT Hub ilişkin bir bildirim gönderir. IOT hub'ı denetler: hello dosya karşıya yükleme tamamlandıktan ve bir dosya karşıya yükleme bildirim iletisi toohello hizmet dönük dosya bildirim uç noktası ekler.

Bir CİHAZDAN dosya tooIoT Hub karşıya yüklemeden önce tarafından hub'ınızı yapılandırmanız gerekir [bir Azure Storage ilişkilendirme] [ lnk-associate-storage] tooit hesap.

Cihazınızı böylece [karşıya yükleme başlatma] [ lnk-initialize] ve ardından [IOT hub'ı bildir] [ lnk-notify] hello karşıya yükleme tamamlandığında. İsteğe bağlı olarak, bir cihaz IOT hub'ı bu hello karşıya yükleme tamamlandığında bildirdiğinde, hello hizmet oluşturabilir bir [bildirim iletisi][lnk-service-notification].

### <a name="when-toouse"></a>Zaman toouse

Dosya karşıya yükleme toosend medya dosyaları ve zaman zaman bağlı cihazları veya sıkıştırılmış toosave bant genişliği tarafından karşıya yüklenen büyük telemetri toplu kullanın.

Çok başvuran[cihaz bulut iletişimi Kılavuzu] [ lnk-d2c-guidance] IF bildirilen özellikleri, cihaz bulut iletilerini veya karşıya dosya yükleme kullanarak arasında şüpheli.

## <a name="associate-an-azure-storage-account-with-iot-hub"></a>Bir Azure Storage hesabı IOT Hub ile ilişkilendirme

toouse hello dosya karşıya yükleme işlevselliği, ilk Azure Storage hesabı toohello IOT hub'ı bağlamanız gerekir. Merhaba aracılığıyla bu görevi tamamlayabilirsiniz [Azure portal][lnk-management-portal], veya program aracılığıyla hello aracılığıyla [IOT hub'ı kaynak sağlayıcısı REST API'leri] [ lnk-resource-provider-apis]. Bir Azure Storage hesabı IOT Hub'ınıza ilişkilendirdikten sonra hello hizmeti hello aygıt dosya karşıya yükleme isteği başlattığında tooa aygıt SAS URI'sini döndürür.

> [!NOTE]
> Merhaba [Azure IOT SDK'ları] [ lnk-sdks] otomatik olarak tanıtıcı alma izin ver hello SAS hello dosya karşıya yükleme ve tamamlanan karşıya yükleme, IOT Hub bildirme URI.


## <a name="initialize-a-file-upload"></a>Bir dosyayı karşıya yükleme başlatma
IOT Hub cihazları toorequest depolama tooupload bir dosya için bir SAS URI'si için özellikle bir uç nokta vardır. tooinitiate hello dosya karşıya yükleme işlemi, hello cihaz gönderen bir POST isteği çok`{iot hub}.azure-devices.net/devices/{deviceId}/files` JSON gövdesi aşağıdaki hello ile:

```json
{
    "blobName": "{name of hello file for which a SAS URI will be generated}"
}
```

IOT hub'ı veri hangi hello aygıt tooupload hello dosyasını kullanır, aşağıdaki hello döndürür:

```json
{
    "correlationId": "somecorrelationid",
    "hostName": "contoso.azure-devices.net",
    "containerName": "testcontainer",
    "blobName": "test-device1/image.jpg",
    "sasToken": "1234asdfSAStoken"
}
```

### <a name="deprecated-initialize-a-file-upload-with-a-get"></a>Kullanım dışı: karşıya dosya yükleme GET ile başlatma

> [!NOTE]
> Bu bölümde nasıl kullanım dışı bırakılan işlevsellik açıklanmaktadır tooreceive IOT hub'dan bir SAS URI'si. Daha önce açıklanan hello POST yöntemini kullanın.

IOT hub'ı karşıya yükleme, bir tooget hello SAS URI'sini depolama ve diğer toonotify hello IOT hub'ını tamamlanan karşıya yükleme hello iki REST uç noktaları toosupport dosyası vardır. Merhaba aygıt hello dosya karşıya yükleme işlemi bir GET toohello IOT hub'ına göndererek başlatır `{iot hub}.azure-devices.net/devices/{deviceId}/files/{filename}`. Merhaba IOT hub'ı döndürür:

* Bir SAS URI'sini belirli toohello dosya toobe karşıya yüklendi.
* Merhaba karşıya yükleme tamamlandığında kullanılan bağıntı kimliği toobe.

## <a name="notify-iot-hub-of-a-completed-file-upload"></a>IOT hub'ı bir tamamlanmış dosyanın karşıya yüklenmesi bildir

Merhaba aygıt hello dosya toostorage hello Azure depolama SDK'ları kullanarak yüklemek için sorumludur. Merhaba karşıya yükleme tamamlandığında, hello aygıt bir POST isteği çok gönderir`{iot hub}.azure-devices.net/devices/{deviceId}/files/notifications` JSON gövdesi aşağıdaki hello ile:

```json
{
    "correlationId": "{correlation ID received from hello initial request}",
    "isSuccess": bool,
    "statusCode": XXX,
    "statusDescription": "Description of status"
}
```

Merhaba değerini `isSuccess` hello dosyası başarıyla karşıya yüklendi olup olmadığını Boolean temsil eden bir değil. Merhaba durum kodunu `statusCode` hello hello dosya toostorage hello karşıya yükleme durumu ve hello `statusDescription` toohello karşılık gelen `statusCode`.

## <a name="reference-topics"></a>Başvuru konuları:

Merhaba aşağıdaki başvuru konuları aygıttan dosyaları karşıya yükleme hakkında daha fazla bilgi sağlar.

## <a name="file-upload-notifications"></a>Dosya karşıya yükleme bildirimleri

Bir cihaz IOT hub'ı bir karşıya yükleme tamamlandığını bildirir, isteğe bağlı olarak, IOT hub'ı hello adı ve depolama hello dosyasının konumunu içeren bir bildirim iletisi oluşturabilir.

İçinde anlatıldığı gibi [uç noktaları][lnk-endpoints], IOT hub'ı sunan bir hizmet'e yönelik uç noktası aracılığıyla dosya karşıya yükleme bildirimleri (**/messages/servicebound/fileuploadnotifications**) iletileri olarak. Merhaba alma semantiğini dosya karşıya yükleme bildirimlerini aynı bulut-cihaz iletilerini ettirilmesi hello ve sahip, hello aynı için [ileti yaşam döngüsü][lnk-lifecycle]. Merhaba dosya karşıya yükleme bildirim uç noktasından alınan her iletinin hello aşağıdaki özelliklere sahip bir JSON kaydıdır:

| Özellik | Açıklama |
| --- | --- |
| EnqueuedTimeUtc |Merhaba bildirim ne zaman oluşturulduğunu belirten bir zaman damgası. |
| Cihaz kimliği |**DeviceID** hello dosya karşıya hello cihazın. |
| BlobUri |Merhaba URI'sini dosyası karşıya yüklendi. |
| BlobName |Merhaba adını dosyası karşıya yüklendi. |
| LastUpdatedTime |Merhaba dosyasının en son güncelleştirildiği belirten bir zaman damgası. |
| BlobSizeInBytes |Merhaba boyutunu dosyası karşıya yüklendi. |

**Örnek**. Bu örnek, bir dosya hello gövdesi karşıya bildirim iletisi gösterir.

```json
{
    "deviceId":"mydevice",
    "blobUri":"https://{storage account}.blob.core.windows.net/{container name}/mydevice/myfile.jpg",
    "blobName":"mydevice/myfile.jpg",
    "lastUpdatedTime":"2016-06-01T21:22:41+00:00",
    "blobSizeInBytes":1234,
    "enqueuedTimeUtc":"2016-06-01T21:22:43.7996883Z"
}
```

## <a name="file-upload-notification-configuration-options"></a>Dosya karşıya yükleme bildirim yapılandırma seçenekleri

Her IOT hub'ı dosya karşıya yükleme bildirimleri için yapılandırma seçenekleri aşağıdaki hello sunar:

| Özellik | Açıklama | Aralık ve varsayılan |
| --- | --- | --- |
| **enableFileUploadNotifications** |Dosya karşıya yükleme bildirimlerini toohello dosya bildirimleri uç noktası yazılmış olup olmadığını denetler. |Bool. Varsayılan: True. |
| **fileNotifications.ttlAsIso8601** |Dosya karşıya yükleme bildirimleri için varsayılan TTL değeri. |Too48H ISO_8601 aralığı (en az 1 dakika). Varsayılan: 1 saat. |
| **fileNotifications.lockDuration** |Merhaba dosya karşıya yükleme bildirimleri sırası süresince kilitleyin. |5 too300 saniye (en az 5 saniye). Varsayılan: 60 saniye sayısı. |
| **fileNotifications.maxDeliveryCount** |Maksimum teslimat sayısı hello dosyası için bildirim sırası karşıya yükleyin. |1 too100. Varsayılan: 100. |

## <a name="additional-reference-material"></a>Ek başvuru bilgileri

Merhaba IOT Hub Geliştirici Kılavuzu diğer başvuru konularına şunları içerir:

* [IOT Hub uç noktaları] [ lnk-endpoints] açıklar çalışma zamanı ve yönetim işlemleri için her IOT hub'ı sunan çeşitli uç noktaları hello.
* [Azaltma ve kotaları] [ lnk-quotas] hello kotaları açıklar ve IOT Hub hizmeti toohello uygulamak davranışları azaltma.
* [Azure IOT cihaz ve hizmet SDK'ları] [ lnk-sdks] listeleri hello çeşitli dil SDK'ları, IOT Hub ile etkileşim hem cihaz hem de hizmet uygulamaları geliştirdiğinizde kullanabilirsiniz.
* [IOT hub'ı sorgu dili] [ lnk-query] tooretrieve bilgilerini IOT hub'dan cihaz çiftlerini ve işleri kullanabileceğiniz hello sorgu dili açıklar.
* [IOT Hub MQTT Destek] [ lnk-devguide-mqtt] hello MQTT protokolü için IOT hub'ı desteği hakkında daha fazla bilgi sağlar.

## <a name="next-steps"></a>Sonraki adımlar

IOT hub'ı kullanarak aygıtlardan tooupload nasıl dosyaları öğrendiniz artık IOT Hub Geliştirici Kılavuzu konuları aşağıdaki hello ilgilenen olabilir:

* [IOT Hub cihaz kimliklerini yönetme][lnk-devguide-identities]
* [Denetim erişim tooIoT Hub][lnk-devguide-security]
* [Cihaz çiftlerini toosynchronize durumu ve yapılandırmaları kullanacak][lnk-devguide-device-twins]
* [Bir cihazda doğrudan bir yöntem çağırma][lnk-devguide-directmethods]
* [Birden çok aygıta işleri zamanla][lnk-devguide-jobs]

Bu makalede açıklanan hello kavramların bazıları çıkışı tootry isterseniz, IOT hub'ı öğreticiyi izleyerek hello ilgilenen olabilir:

* [Aygıtları toohello tooupload dosyalarından IOT Hub ile nasıl bulut][lnk-fileupload-tutorial]

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-management-portal]: https://portal.azure.com
[lnk-fileupload-tutorial]: iot-hub-csharp-csharp-file-upload.md
[lnk-associate-storage]: iot-hub-devguide-file-upload.md#associate-an-azure-storage-account-with-iot-hub
[lnk-initialize]: iot-hub-devguide-file-upload.md#initialize-a-file-upload
[lnk-notify]: iot-hub-devguide-file-upload.md#notify-iot-hub-of-a-completed-file-upload
[lnk-service-notification]: iot-hub-devguide-file-upload.md#file-upload-notifications
[lnk-lifecycle]: iot-hub-devguide-messages-c2d.md#the-cloud-to-device-message-lifecycle
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-devguide-identities]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
