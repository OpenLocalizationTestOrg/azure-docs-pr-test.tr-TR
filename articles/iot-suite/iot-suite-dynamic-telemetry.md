---
title: aaaUse dinamik telemetri | Microsoft Docs
description: "Bu öğretici toolearn izleyin nasıl toouse dinamik telemetri hello Azure IOT paketi Uzaktan izleme çözümü önceden yapılandırılmış."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 562799dc-06ea-4cdd-b822-80d1f70d2f09
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 06cb2a370b67b4950efdfa4c7d906ac92106f4a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a>Dinamik telemetri hello Uzaktan izleme çözümü ile kullanma

Dinamik telemetri, toovisualize herhangi gönderilen telemetri toohello Uzaktan izleme çözümü sağlar. Merhaba önceden yapılandırılmış çözümü ile dağıtın benzetimli hello aygıtları hello Panoda görselleştirebilirsiniz sıcaklık ve nem telemetrisi gönderin. Varolan sanal cihazlar özelleştirirseniz, yeni sanal cihaz oluşturma ya da fiziksel aygıtların toohello önceden yapılandırılmış çözümü hello dış sıcaklığı, RPM ya da windspeed gibi diğer telemetri değerleri gönderebilirsiniz bağlantı. Ardından, bu ek telemetri hello Panoda görselleştirebilirsiniz.

Bu öğretici tooexperiment dinamik telemetri ile kolayca değiştirebilirsiniz basit bir Node.js sanal cihaz kullanır.

toocomplete Bu öğretici, gerekir:

* Etkin bir Azure aboneliği. Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].
* [Node.js] [ lnk-node] sürüm 0.12.x sürümü veya sonraki bir sürümü.

Bu öğretici Windows veya Linux, Node.js yükleyebileceğiniz gibi herhangi bir işletim sistemini tamamlayabilirsiniz.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a>Telemetri türü ekleme

Hello sonraki adım, yeni bir değer kümesiyle hello Node.js sanal cihaz tarafından oluşturulan tooreplace hello telemetri olacaktır:

1. Yazarak Dur hello Node.js sanal cihaz **Ctrl + C** komut istemi veya kabuk.
2. Merhaba remote_monitoring.js dosyasında hello varolan sıcaklık ve nem dış sıcaklığı telemetri için hello temel veri değerleri görebilirsiniz. İçin bir taban veri değer Ekle **rpm** gibi:

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. Merhaba Node.js sanal cihaz kullanan hello **generateRandomIncrement** temel veri değerleri hello remote_monitoring.js dosya tooadd rastgele artışı toohello işlev. Merhaba rasgele yap **rpm** hello varolan randomizations sonra şu şekilde bir kod satırı ekleyerek değeri:

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. Merhaba yeni rpm değeri toohello JSON yükü hello aygıt gönderir tooIoT Hub ekleyin:

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. Merhaba Node.js sanal cihaz komutu aşağıdaki hello kullanarak çalıştırın:

    `node remote_monitoring.js`

6. Hello grafik hello Panoda görüntüleyen hello yeni RPM telemetri türü inceleyin:

![RPM toohello Pano Ekle][image3]

> [!NOTE]
> Toodisable ihtiyacınız ve hello Node.js hello cihazda etkinleştirmek **aygıtları** hello Pano toosee hello değişikliği hemen sayfasında.

## <a name="customize-hello-dashboard-display"></a>Merhaba Pano ekranını özelleştirme

Merhaba **Device-Info** ileti meta veriler içerebilir hello telemetri hakkında hello aygıt tooIoT Hub gönderebilir. Bu meta veriler hello cihaz gönderir hello telemetri türlerini belirtebilirsiniz. Merhaba değiştirme **deviceMetaData** hello remote_monitoring.js dosya tooinclude değerinde bir **Telemetri** hello aşağıdaki tanımı **komutları** tanımı. Merhaba aşağıdaki kod parçacığını gösterir hello **komutları** tanımı (emin tooadd olması bir `,` hello sonra **komutları** tanımı):

```nodejs
'Commands': [{
  'Name': 'SetTemperature',
  'Parameters': [{
    'Name': 'Temperature',
    'Type': 'double'
  }]
},
{
  'Name': 'SetHumidity',
  'Parameters': [{
    'Name': 'Humidity',
    'Type': 'double'
  }]
}],
'Telemetry': [{
  'Name': 'Temperature',
  'Type': 'double'
},
{
  'Name': 'Humidity',
  'Type': 'double'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double'
}]
```

> [!NOTE]
> Merhaba Uzaktan izleme çözümü bir küçük harf olarak eşleşen toocompare hello meta veri açıklamasında hello telemetri akışına verileri kullanır.


Ekleme bir **Telemetri** hello önceki kod parçacığını hello Pano hello davranışını değiştirmez gösterildiği tanımı. Merhaba meta verileri de içerir ancak, bir **DisplayName** özniteliği hello panosunda toocustomize hello görüntülemek. Güncelleştirme hello **Telemetri** hello aşağıdaki kod parçacığında gösterildiği gibi meta veri tanımı:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
{
  'Name': 'ExternalTemperature',
  'Type': 'double',
  'DisplayName': 'Outdoor Temperature (C*)'
}
]
```

Merhaba aşağıdaki ekran görüntüsü bu değişikliği hello grafik gösterge hello Panoda nasıl değiştirdiğini gösterir:

![Merhaba grafik gösterge özelleştirme][image4]

> [!NOTE]
> Toodisable ihtiyacınız ve hello Node.js hello cihazda etkinleştirmek **aygıtları** hello Pano toosee hello değişikliği hemen sayfasında.

## <a name="filter-hello-telemetry-types"></a>Merhaba telemetri türlerini filtre

Varsayılan olarak, hello grafik hello Panoda her veri serisi hello telemetrisi akışını gösterir. Merhaba kullanabilirsiniz **Device-Info** meta veri toosuppress hello belirli telemetri türlerini hello grafik görüntüsünü. 

toomake hello grafik atlayın yalnızca sıcaklık ve nem telemetrisi, Göster **ExternalTemperature** hello gelen **Device-Info** **Telemetri** aşağıdaki gibi meta veriler:

```nodejs
'Telemetry': [
{
  'Name': 'Temperature',
  'Type': 'double',
  'DisplayName': 'Temperature (C*)'
},
{
  'Name': 'Humidity',
  'Type': 'double',
  'DisplayName': 'Humidity (relative)'
},
//{
//  'Name': 'ExternalTemperature',
//  'Type': 'double',
//  'DisplayName': 'Outdoor Temperature (C*)'
//}
]
```

Merhaba **dış sıcaklığı** artık hello grafiği görüntüler:

![Filtre hello telemetriyi hello Panosu][image5]

Bu değişiklik, yalnızca hello grafik görüntüleme etkiler. Merhaba **ExternalTemperature** veri değerleri hala depolanır ve tüm arka uç işleme için kullanılabilir.

> [!NOTE]
> Toodisable ihtiyacınız ve hello Node.js hello cihazda etkinleştirmek **aygıtları** hello Pano toosee hello değişikliği hemen sayfasında.

## <a name="handle-errors"></a>Hata işleme

Bir veri akışı toodisplay hello grafik için kendi **türü** hello içinde **Device-Info** meta verileri hello telemetri değerlerin hello veri türüyle eşleşmelidir. Örneğin, hello meta verileri bu hello belirtir **türü** nem veridir **int** ve **çift** hello nem telemetrisi mu sonra hello telemetrisi akışını bulundu Merhaba grafikte görüntülemeyecek. Ancak, hello **nem** değerleri hala depolanır ve tüm arka uç işleme için kullanılabilir.

## <a name="next-steps"></a>Sonraki adımlar

Göre nasıl toouse dinamik telemetri nasıl hello önceden yapılandırılmış çözümleri hakkında daha fazla cihaz bilgilerini kullanmak öğrenebilir gördünüz: [hello Uzaktan izleme aygıt bilgileri meta verileri önceden yapılandırılmış çözüm] [ lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
