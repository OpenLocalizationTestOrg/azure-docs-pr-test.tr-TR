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
# <a name="use-dynamic-telemetry-with-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="ab2c5-103">Dinamik telemetri hello Uzaktan izleme çözümü ile kullanma</span><span class="sxs-lookup"><span data-stu-id="ab2c5-103">Use dynamic telemetry with hello remote monitoring preconfigured solution</span></span>

<span data-ttu-id="ab2c5-104">Dinamik telemetri, toovisualize herhangi gönderilen telemetri toohello Uzaktan izleme çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-104">Dynamic telemetry enables you toovisualize any telemetry sent toohello remote monitoring preconfigured solution.</span></span> <span data-ttu-id="ab2c5-105">Merhaba önceden yapılandırılmış çözümü ile dağıtın benzetimli hello aygıtları hello Panoda görselleştirebilirsiniz sıcaklık ve nem telemetrisi gönderin.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-105">hello simulated devices that deploy with hello preconfigured solution send temperature and humidity telemetry, which you can visualize on hello dashboard.</span></span> <span data-ttu-id="ab2c5-106">Varolan sanal cihazlar özelleştirirseniz, yeni sanal cihaz oluşturma ya da fiziksel aygıtların toohello önceden yapılandırılmış çözümü hello dış sıcaklığı, RPM ya da windspeed gibi diğer telemetri değerleri gönderebilirsiniz bağlantı.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-106">If you customize existing simulated devices, create new simulated devices, or connect physical devices toohello preconfigured solution you can send other telemetry values such as hello external temperature, RPM, or windspeed.</span></span> <span data-ttu-id="ab2c5-107">Ardından, bu ek telemetri hello Panoda görselleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-107">You can then visualize this additional telemetry on hello dashboard.</span></span>

<span data-ttu-id="ab2c5-108">Bu öğretici tooexperiment dinamik telemetri ile kolayca değiştirebilirsiniz basit bir Node.js sanal cihaz kullanır.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-108">This tutorial uses a simple Node.js simulated device that you can easily modify tooexperiment with dynamic telemetry.</span></span>

<span data-ttu-id="ab2c5-109">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="ab2c5-109">toocomplete this tutorial, you’ll need:</span></span>

* <span data-ttu-id="ab2c5-110">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-110">An active Azure subscription.</span></span> <span data-ttu-id="ab2c5-111">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-111">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="ab2c5-112">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="ab2c5-112">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="ab2c5-113">[Node.js] [ lnk-node] sürüm 0.12.x sürümü veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-113">[Node.js][lnk-node] version 0.12.x or later.</span></span>

<span data-ttu-id="ab2c5-114">Bu öğretici Windows veya Linux, Node.js yükleyebileceğiniz gibi herhangi bir işletim sistemini tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-114">You can complete this tutorial on any operating system, such as Windows or Linux, where you can install Node.js.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

## <a name="add-a-telemetry-type"></a><span data-ttu-id="ab2c5-115">Telemetri türü ekleme</span><span class="sxs-lookup"><span data-stu-id="ab2c5-115">Add a telemetry type</span></span>

<span data-ttu-id="ab2c5-116">Hello sonraki adım, yeni bir değer kümesiyle hello Node.js sanal cihaz tarafından oluşturulan tooreplace hello telemetri olacaktır:</span><span class="sxs-lookup"><span data-stu-id="ab2c5-116">hello next step is tooreplace hello telemetry generated by hello Node.js simulated device with a new set of values:</span></span>

1. <span data-ttu-id="ab2c5-117">Yazarak Dur hello Node.js sanal cihaz **Ctrl + C** komut istemi veya kabuk.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-117">Stop hello Node.js simulated device by typing **Ctrl+C** in your command prompt or shell.</span></span>
2. <span data-ttu-id="ab2c5-118">Merhaba remote_monitoring.js dosyasında hello varolan sıcaklık ve nem dış sıcaklığı telemetri için hello temel veri değerleri görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-118">In hello remote_monitoring.js file, you can see hello base data values for hello existing temperature, humidity, and external temperature telemetry.</span></span> <span data-ttu-id="ab2c5-119">İçin bir taban veri değer Ekle **rpm** gibi:</span><span class="sxs-lookup"><span data-stu-id="ab2c5-119">Add a base data value for **rpm** as follows:</span></span>

    ```nodejs
    // Sensors data
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    var rpm = 200;
    ```

3. <span data-ttu-id="ab2c5-120">Merhaba Node.js sanal cihaz kullanan hello **generateRandomIncrement** temel veri değerleri hello remote_monitoring.js dosya tooadd rastgele artışı toohello işlev.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-120">hello Node.js simulated device uses hello **generateRandomIncrement** function in hello remote_monitoring.js file tooadd a random increment toohello base data values.</span></span> <span data-ttu-id="ab2c5-121">Merhaba rasgele yap **rpm** hello varolan randomizations sonra şu şekilde bir kod satırı ekleyerek değeri:</span><span class="sxs-lookup"><span data-stu-id="ab2c5-121">Randomize hello **rpm** value by adding a line of code after hello existing randomizations as follows:</span></span>

    ```nodejs
    temperature += generateRandomIncrement();
    externalTemperature += generateRandomIncrement();
    humidity += generateRandomIncrement();
    rpm += generateRandomIncrement();
    ```

4. <span data-ttu-id="ab2c5-122">Merhaba yeni rpm değeri toohello JSON yükü hello aygıt gönderir tooIoT Hub ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ab2c5-122">Add hello new rpm value toohello JSON payload hello device sends tooIoT Hub:</span></span>

    ```nodejs
    var data = JSON.stringify({
      'DeviceID': deviceId,
      'Temperature': temperature,
      'Humidity': humidity,
      'ExternalTemperature': externalTemperature,
      'RPM': rpm
    });
    ```

5. <span data-ttu-id="ab2c5-123">Merhaba Node.js sanal cihaz komutu aşağıdaki hello kullanarak çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="ab2c5-123">Run hello Node.js simulated device using hello following command:</span></span>

    `node remote_monitoring.js`

6. <span data-ttu-id="ab2c5-124">Hello grafik hello Panoda görüntüleyen hello yeni RPM telemetri türü inceleyin:</span><span class="sxs-lookup"><span data-stu-id="ab2c5-124">Observe hello new RPM telemetry type that displays on hello chart in hello dashboard:</span></span>

![RPM toohello Pano Ekle][image3]

> [!NOTE]
> <span data-ttu-id="ab2c5-126">Toodisable ihtiyacınız ve hello Node.js hello cihazda etkinleştirmek **aygıtları** hello Pano toosee hello değişikliği hemen sayfasında.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-126">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="customize-hello-dashboard-display"></a><span data-ttu-id="ab2c5-127">Merhaba Pano ekranını özelleştirme</span><span class="sxs-lookup"><span data-stu-id="ab2c5-127">Customize hello dashboard display</span></span>

<span data-ttu-id="ab2c5-128">Merhaba **Device-Info** ileti meta veriler içerebilir hello telemetri hakkında hello aygıt tooIoT Hub gönderebilir.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-128">hello **Device-Info** message can include metadata about hello telemetry hello device can send tooIoT Hub.</span></span> <span data-ttu-id="ab2c5-129">Bu meta veriler hello cihaz gönderir hello telemetri türlerini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-129">This metadata can specify hello telemetry types hello device sends.</span></span> <span data-ttu-id="ab2c5-130">Merhaba değiştirme **deviceMetaData** hello remote_monitoring.js dosya tooinclude değerinde bir **Telemetri** hello aşağıdaki tanımı **komutları** tanımı.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-130">Modify hello **deviceMetaData** value in hello remote_monitoring.js file tooinclude a **Telemetry** definition following hello **Commands** definition.</span></span> <span data-ttu-id="ab2c5-131">Merhaba aşağıdaki kod parçacığını gösterir hello **komutları** tanımı (emin tooadd olması bir `,` hello sonra **komutları** tanımı):</span><span class="sxs-lookup"><span data-stu-id="ab2c5-131">hello following code snippet shows hello **Commands** definition (be sure tooadd a `,` after hello **Commands** definition):</span></span>

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
> <span data-ttu-id="ab2c5-132">Merhaba Uzaktan izleme çözümü bir küçük harf olarak eşleşen toocompare hello meta veri açıklamasında hello telemetri akışına verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-132">hello remote monitoring solution uses a case-insensitive match toocompare hello metadata definition with data in hello telemetry stream.</span></span>


<span data-ttu-id="ab2c5-133">Ekleme bir **Telemetri** hello önceki kod parçacığını hello Pano hello davranışını değiştirmez gösterildiği tanımı.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-133">Adding a **Telemetry** definition as shown in hello preceding code snippet does not change hello behavior of hello dashboard.</span></span> <span data-ttu-id="ab2c5-134">Merhaba meta verileri de içerir ancak, bir **DisplayName** özniteliği hello panosunda toocustomize hello görüntülemek.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-134">However, hello metadata can also include a **DisplayName** attribute toocustomize hello display in hello dashboard.</span></span> <span data-ttu-id="ab2c5-135">Güncelleştirme hello **Telemetri** hello aşağıdaki kod parçacığında gösterildiği gibi meta veri tanımı:</span><span class="sxs-lookup"><span data-stu-id="ab2c5-135">Update hello **Telemetry** metadata definition as shown in hello following snippet:</span></span>

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

<span data-ttu-id="ab2c5-136">Merhaba aşağıdaki ekran görüntüsü bu değişikliği hello grafik gösterge hello Panoda nasıl değiştirdiğini gösterir:</span><span class="sxs-lookup"><span data-stu-id="ab2c5-136">hello following screenshot shows how this change modifies hello chart legend on hello dashboard:</span></span>

![Merhaba grafik gösterge özelleştirme][image4]

> [!NOTE]
> <span data-ttu-id="ab2c5-138">Toodisable ihtiyacınız ve hello Node.js hello cihazda etkinleştirmek **aygıtları** hello Pano toosee hello değişikliği hemen sayfasında.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-138">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="filter-hello-telemetry-types"></a><span data-ttu-id="ab2c5-139">Merhaba telemetri türlerini filtre</span><span class="sxs-lookup"><span data-stu-id="ab2c5-139">Filter hello telemetry types</span></span>

<span data-ttu-id="ab2c5-140">Varsayılan olarak, hello grafik hello Panoda her veri serisi hello telemetrisi akışını gösterir.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-140">By default, hello chart on hello dashboard shows every data series in hello telemetry stream.</span></span> <span data-ttu-id="ab2c5-141">Merhaba kullanabilirsiniz **Device-Info** meta veri toosuppress hello belirli telemetri türlerini hello grafik görüntüsünü.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-141">You can use hello **Device-Info** metadata toosuppress hello display of specific telemetry types on hello chart.</span></span> 

<span data-ttu-id="ab2c5-142">toomake hello grafik atlayın yalnızca sıcaklık ve nem telemetrisi, Göster **ExternalTemperature** hello gelen **Device-Info** **Telemetri** aşağıdaki gibi meta veriler:</span><span class="sxs-lookup"><span data-stu-id="ab2c5-142">toomake hello chart show only Temperature and Humidity telemetry, omit **ExternalTemperature** from hello **Device-Info** **Telemetry** metadata as follows:</span></span>

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

<span data-ttu-id="ab2c5-143">Merhaba **dış sıcaklığı** artık hello grafiği görüntüler:</span><span class="sxs-lookup"><span data-stu-id="ab2c5-143">hello **Outdoor Temperature** no longer displays on hello chart:</span></span>

![Filtre hello telemetriyi hello Panosu][image5]

<span data-ttu-id="ab2c5-145">Bu değişiklik, yalnızca hello grafik görüntüleme etkiler.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-145">This change only affects hello chart display.</span></span> <span data-ttu-id="ab2c5-146">Merhaba **ExternalTemperature** veri değerleri hala depolanır ve tüm arka uç işleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-146">hello **ExternalTemperature** data values are still stored and made available for any backend processing.</span></span>

> [!NOTE]
> <span data-ttu-id="ab2c5-147">Toodisable ihtiyacınız ve hello Node.js hello cihazda etkinleştirmek **aygıtları** hello Pano toosee hello değişikliği hemen sayfasında.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-147">You may need toodisable and then enable hello Node.js device on hello **Devices** page in hello dashboard toosee hello change immediately.</span></span>

## <a name="handle-errors"></a><span data-ttu-id="ab2c5-148">Hata işleme</span><span class="sxs-lookup"><span data-stu-id="ab2c5-148">Handle errors</span></span>

<span data-ttu-id="ab2c5-149">Bir veri akışı toodisplay hello grafik için kendi **türü** hello içinde **Device-Info** meta verileri hello telemetri değerlerin hello veri türüyle eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-149">For a data stream toodisplay on hello chart, its **Type** in hello **Device-Info** metadata must match hello data type of hello telemetry values.</span></span> <span data-ttu-id="ab2c5-150">Örneğin, hello meta verileri bu hello belirtir **türü** nem veridir **int** ve **çift** hello nem telemetrisi mu sonra hello telemetrisi akışını bulundu Merhaba grafikte görüntülemeyecek.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-150">For example, if hello metadata specifies that hello **Type** of humidity data is **int** and a **double** is found in hello telemetry stream then hello humidity telemetry does not display on hello chart.</span></span> <span data-ttu-id="ab2c5-151">Ancak, hello **nem** değerleri hala depolanır ve tüm arka uç işleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ab2c5-151">However, hello **Humidity** values are still stored and made available for any back-end processing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab2c5-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ab2c5-152">Next steps</span></span>

<span data-ttu-id="ab2c5-153">Göre nasıl toouse dinamik telemetri nasıl hello önceden yapılandırılmış çözümleri hakkında daha fazla cihaz bilgilerini kullanmak öğrenebilir gördünüz: [hello Uzaktan izleme aygıt bilgileri meta verileri önceden yapılandırılmış çözüm] [ lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="ab2c5-153">Now that you've seen how toouse dynamic telemetry, you can learn more about how hello preconfigured solutions use device information: [Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[image3]: media/iot-suite-dynamic-telemetry/image3.png
[image4]: media/iot-suite-dynamic-telemetry/image4.png
[image5]: media/iot-suite-dynamic-telemetry/image5.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
