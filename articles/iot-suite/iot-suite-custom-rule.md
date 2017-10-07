---
title: "Azure IOT paketi özel bir kuralda aaaCreate | Microsoft Docs"
description: "Nasıl toocreate bir IOT paketi özel bir kuralda çözüm önceden yapılandırılmış."
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
ms.openlocfilehash: 6c5bb2ca54f3f17b99ad482e727c8e9fa28d7fe5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a>Özel bir kural hello Uzaktan izleme çözümü oluşturun

## <a name="introduction"></a>Giriş

Önceden yapılandırılmış hello çözümlerinde yapılandırdığınız [bir telemetri zaman tetikleyen kuralların değeri bir cihaz belirli bir eşiğe ulaştığında için][lnk-builtin-rule]. [Dinamik telemetri hello Uzaktan izleme çözümü ile kullanmak] [ lnk-dynamic-telemetry] özel telemetri değerleri gibi nasıl ekleyebileceğinizi açıklar *ExternalTemperature* tooyour çözümü. Bu makalede, nasıl özel bir kural toocreate dinamik telemetri için çözümünüzde türleri gösterilmektedir.

Bu öğretici, bir basit Node.js sanal cihaz toogenerate dinamik telemetri toosend toohello önceden yapılandırılmış çözüm arka ucu kullanır. Ardından özel kurallar hello ekleyin **RemoteMonitoring** Visual Studio çözümü ve bu özelleştirilmiş arka uç tooyour Azure aboneliği dağıtın.

toocomplete Bu öğretici, gerekir:

* Etkin bir Azure aboneliği. Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].
* [Node.js] [ lnk-node] sürüm 0.12.x sürümü veya üzeri toocreate sanal bir cihaz.
* Visual Studio 2015 veya Visual Studio 2017 toomodify hello önceden yapılandırılmış çözüm arka ucu yeni kurallarınızı.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

Dağıtımınız için seçtiğiniz hello çözüm adı not edin. Bu çözüm adı daha sonra Bu öğreticide gerekir.

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

Gönderme olduğunu belirlediğinizde hello Node.js konsol uygulaması durdurabilirsiniz **ExternalTemperature** telemetri toohello önceden yapılandırılmış çözümü. Merhaba özel kural toohello çözüm ekledikten sonra bu Node.js konsol uygulaması yeniden çalıştırmak için hello konsol penceresi açık tutun.

## <a name="rule-storage-locations"></a>Kural depolama konumları

Kurallar hakkında bilgileri iki konumda kalıcıdır:

* **DeviceRulesNormalizedTable** tablo – bu tablo bir normalleştirilmiş depolar hello çözüm portalı tarafından tanımlanan toohello kurallar başvuru. Merhaba çözüm portalı cihaz kuralları görüntülediğinde, bu tablo hello kuralı tanımları için sorgular.
* **DeviceRules** blob – bu blob tüm kayıtlı cihazlar ve bir başvuru giriş toohello Azure akış analizi işi tanımlanan tanımlanan tüm hello kurallar depolar.
 
Mevcut bir kuralı güncelleştirmek veya yeni bir kural hello çözüm Portalı'nda tanımlamak, hem hello tablosunda hem de blob güncelleştirilmiş tooreflect hello değişir. Merhaba kural tanımı hello Portalı'nda görüntülenen hello tablo deposu ve hello kural tanımı hello Stream Analytics işleri tarafından başvurulan hello blobundan gelen gelir. 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a>Merhaba RemoteMonitoring Visual Studio çözümünü güncelleştirme

Merhaba aşağıdaki adımlar, nasıl toomodify hello RemoteMonitoring Visual Studio çözümü tooinclude hello kullanan yeni bir kural gösterir **ExternalTemperature** hello benzetimli aygıtından gönderilen telemetri:

1. Zaten, kopya hello yapmadıysanız, **azure-iot-remote-monitoring** makinenizde Git komut aşağıdaki hello kullanarak yerel deposu tooa uygun konumu:

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. Visual Studio'da hello RemoteMonitoring.sln dosyasını hello yerel kopyadan açın **azure-iot-remote-monitoring** deposu.

3. Merhaba dosyasını Infrastructure\Models\DeviceRuleBlobEntity.cs açın ve eklemek bir **ExternalTemperature** özelliğini aşağıdaki gibi:

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. Buna Merhaba aynı dosya, ekleme bir **ExternalTemperatureRuleOutput** özelliğini aşağıdaki gibi:

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. Merhaba dosyasını Infrastructure\Models\DeviceRuleDataFields.cs açın ve hello aşağıdakileri ekleyin **ExternalTemperature** hello varolan sonra özelliği **nem** özelliği:

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. Buna Merhaba aynı dosya, güncelleştirme hello **_availableDataFields** yöntemi tooinclude **ExternalTemperature** gibi:

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. Merhaba dosyasını Infrastructure\Repository\DeviceRulesRepository.cs açın ve hello değiştirin **BuildBlobEntityListFromTableRows** yöntemini aşağıdaki şekilde:

    ```csharp
    else if (rule.DataField == DeviceRuleDataFields.Humidity)
    {
        entity.Humidity = rule.Threshold;
        entity.HumidityRuleOutput = rule.RuleOutput;
    }
    else if (rule.DataField == DeviceRuleDataFields.ExternalTemperature)
    {
      entity.ExternalTemperature = rule.Threshold;
      entity.ExternalTemperatureRuleOutput = rule.RuleOutput;
    }
    ```

## <a name="rebuild-and-redeploy-hello-solution"></a>Yeniden oluşturun ve hello çözümü yeniden dağıtın.

Güncelleştirilmiş hello çözüm tooyour Azure abonelik artık dağıtabilirsiniz.

1. Yükseltilmiş bir komut istemi açın ve hello azure-iot-remote-monitoring deposu yerel kopyasını toohello köküne gidin.

2. toodeploy komutu değiştirerek aşağıdaki hello çalıştırmak çözümünüzü güncelleştirilmiş **{dağıtım adı}** önceden yapılandırılmış çözüm dağıtımınızın, daha önce not ettiğiniz hello adıyla:

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a>Güncelleştirme hello Stream Analytics işi

Merhaba dağıtım tamamlandığında, hello Stream Analytics işi toouse hello yeni kural tanımları güncelleştirebilirsiniz.

1. Hello Azure portalı, önceden yapılandırılmış çözüm kaynaklarınızı içeren toohello kaynak grubunu gidin. Bu kaynak grubu aynı ad için belirttiğiniz hello sahip çözüm hello dağıtımı sırasında hello.

2. Toohello {dağıtım adı} gidin-kuralları Stream Analytics işi. 

3. Tıklatın **durdurmak** toostop hello Stream Analytics işi çalışmasını. (Merhaba sorgu düzenleyebilmeniz iş toostop akış hello için beklemeniz gerekir).

4. Tıklatın **sorgu**. Merhaba sorgu tooinclude hello Düzenle **seçin** bildirimi **ExternalTemperature**. Merhaba aşağıdaki örnek hello tam sorgu hello ile yeni gösterir **seçin** deyimi:

    ```
    WITH AlarmsData AS 
    (
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Temperature' as ReadingType,
         Stream.Temperature as Reading,
         Ref.Temperature as Threshold,
         Ref.TemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Temperature IS NOT null AND Stream.Temperature > Ref.Temperature
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'Humidity' as ReadingType,
         Stream.Humidity as Reading,
         Ref.Humidity as Threshold,
         Ref.HumidityRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.Humidity IS NOT null AND Stream.Humidity > Ref.Humidity
     
    UNION ALL
     
    SELECT
         Stream.IoTHub.ConnectionDeviceId AS DeviceId,
         'ExternalTemperature' as ReadingType,
         Stream.ExternalTemperature as Reading,
         Ref.ExternalTemperature as Threshold,
         Ref.ExternalTemperatureRuleOutput as RuleOutput,
         Stream.EventEnqueuedUtcTime AS [Time]
    FROM IoTTelemetryStream Stream
    JOIN DeviceRulesBlob Ref ON Stream.IoTHub.ConnectionDeviceId = Ref.DeviceID
    WHERE
         Ref.ExternalTemperature IS NOT null AND Stream.ExternalTemperature > Ref.ExternalTemperature
    )
     
    SELECT *
    INTO DeviceRulesMonitoring
    FROM AlarmsData
     
    SELECT *
    INTO DeviceRulesHub
    FROM AlarmsData
    ```

5. Tıklatın **kaydetmek** toochange hello kural sorgu güncelleştirildi.

6. Tıklatın **Başlat** toostart hello Stream Analytics işi yeniden çalıştırmayı.

## <a name="add-your-new-rule-in-hello-dashboard"></a>Merhaba panosunda, yeni bir kural ekleyin

Merhaba artık ekleyebilirsiniz **ExternalTemperature** hello çözüm panosunda kural tooa aygıt.

1. Toohello çözüm portalı gidin.

2. Toohello gidin **aygıtları** paneli.

3. Gönderen, oluşturduğunuz hello özel cihaz bulun **ExternalTemperature** telemetri ve hello **cihaz ayrıntıları** öğesine tıklayın **Kuralı Ekle**.

4. Seçin **ExternalTemperature** içinde **veri alanı**.

5. Ayarlama **eşik** too56. Ardından **kaydedin ve kuralları**.

6. Toohello Pano tooview hello alarm geçmişi döndür.

7. Hello konsol penceresi açık sol hello Node.js konsol uygulaması toobegin göndermeye Başla **ExternalTemperature** telemetri verileri.

8. Bu hello fark **Alarm geçmişi** tablo hello yeni kuralı tetiklendiğinde yeni uyarıları gösterir.
 
## <a name="additional-information"></a>Ek bilgiler

Değişen hello işleci  **>**  daha karmaşıktır ve Bu öğreticide gösterilen hello adımları ötesine geçer. İstediğiniz ne olursa olsun işleci hello Stream Analytics işi toouse değiştirebilirsiniz, ancak bu işleci hello çözüm portalında yansıtma daha karmaşık bir görevdir. 

## <a name="next-steps"></a>Sonraki adımlar
Nasıl toocreate özel kurallar, daha fazla hello önceden yapılandırılmış çözümleri hakkında bilgi edinebilirsiniz gördünüz göre:

- [Mantıksal uygulama tooyour Azure IOT paketi uzaktan önceden yapılandırılmış izleme çözümü bağlantı][lnk-logic-app]
- [Merhaba Uzaktan izleme aygıt bilgileri meta verileri önceden yapılandırılmış çözüm][lnk-devinfo].

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md