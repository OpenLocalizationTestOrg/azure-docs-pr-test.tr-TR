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
# <a name="create-a-custom-rule-in-hello-remote-monitoring-preconfigured-solution"></a><span data-ttu-id="96834-103">Özel bir kural hello Uzaktan izleme çözümü oluşturun</span><span class="sxs-lookup"><span data-stu-id="96834-103">Create a custom rule in hello remote monitoring preconfigured solution</span></span>

## <a name="introduction"></a><span data-ttu-id="96834-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="96834-104">Introduction</span></span>

<span data-ttu-id="96834-105">Önceden yapılandırılmış hello çözümlerinde yapılandırdığınız [bir telemetri zaman tetikleyen kuralların değeri bir cihaz belirli bir eşiğe ulaştığında için][lnk-builtin-rule].</span><span class="sxs-lookup"><span data-stu-id="96834-105">In hello preconfigured solutions, you can configure [rules that trigger when a telemetry value for a device reaches a specific threshold][lnk-builtin-rule].</span></span> <span data-ttu-id="96834-106">[Dinamik telemetri hello Uzaktan izleme çözümü ile kullanmak] [ lnk-dynamic-telemetry] özel telemetri değerleri gibi nasıl ekleyebileceğinizi açıklar *ExternalTemperature* tooyour çözümü.</span><span class="sxs-lookup"><span data-stu-id="96834-106">[Use dynamic telemetry with hello remote monitoring preconfigured solution][lnk-dynamic-telemetry] describes how you can add custom telemetry values, such as *ExternalTemperature* tooyour solution.</span></span> <span data-ttu-id="96834-107">Bu makalede, nasıl özel bir kural toocreate dinamik telemetri için çözümünüzde türleri gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="96834-107">This article shows you how toocreate custom rule for dynamic telemetry types in your solution.</span></span>

<span data-ttu-id="96834-108">Bu öğretici, bir basit Node.js sanal cihaz toogenerate dinamik telemetri toosend toohello önceden yapılandırılmış çözüm arka ucu kullanır.</span><span class="sxs-lookup"><span data-stu-id="96834-108">This tutorial uses a simple Node.js simulated device toogenerate dynamic telemetry toosend toohello preconfigured solution back end.</span></span> <span data-ttu-id="96834-109">Ardından özel kurallar hello ekleyin **RemoteMonitoring** Visual Studio çözümü ve bu özelleştirilmiş arka uç tooyour Azure aboneliği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="96834-109">You then add custom rules in hello **RemoteMonitoring** Visual Studio solution and deploy this customized back end tooyour Azure subscription.</span></span>

<span data-ttu-id="96834-110">toocomplete Bu öğretici, gerekir:</span><span class="sxs-lookup"><span data-stu-id="96834-110">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="96834-111">Etkin bir Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="96834-111">An active Azure subscription.</span></span> <span data-ttu-id="96834-112">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96834-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="96834-113">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="96834-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
* <span data-ttu-id="96834-114">[Node.js] [ lnk-node] sürüm 0.12.x sürümü veya üzeri toocreate sanal bir cihaz.</span><span class="sxs-lookup"><span data-stu-id="96834-114">[Node.js][lnk-node] version 0.12.x or later toocreate a simulated device.</span></span>
* <span data-ttu-id="96834-115">Visual Studio 2015 veya Visual Studio 2017 toomodify hello önceden yapılandırılmış çözüm arka ucu yeni kurallarınızı.</span><span class="sxs-lookup"><span data-stu-id="96834-115">Visual Studio 2015 or Visual Studio 2017 toomodify hello preconfigured solution back end with your new rules.</span></span>

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

<span data-ttu-id="96834-116">Dağıtımınız için seçtiğiniz hello çözüm adı not edin.</span><span class="sxs-lookup"><span data-stu-id="96834-116">Make a note of hello solution name you chose for your deployment.</span></span> <span data-ttu-id="96834-117">Bu çözüm adı daha sonra Bu öğreticide gerekir.</span><span class="sxs-lookup"><span data-stu-id="96834-117">You need this solution name later in this tutorial.</span></span>

[!INCLUDE [iot-suite-send-external-temperature](../../includes/iot-suite-send-external-temperature.md)]

<span data-ttu-id="96834-118">Gönderme olduğunu belirlediğinizde hello Node.js konsol uygulaması durdurabilirsiniz **ExternalTemperature** telemetri toohello önceden yapılandırılmış çözümü.</span><span class="sxs-lookup"><span data-stu-id="96834-118">You can stop hello Node.js console app when you have verified that it is sending **ExternalTemperature** telemetry toohello preconfigured solution.</span></span> <span data-ttu-id="96834-119">Merhaba özel kural toohello çözüm ekledikten sonra bu Node.js konsol uygulaması yeniden çalıştırmak için hello konsol penceresi açık tutun.</span><span class="sxs-lookup"><span data-stu-id="96834-119">Keep hello console window open because you run this Node.js console app again after you add hello custom rule toohello solution.</span></span>

## <a name="rule-storage-locations"></a><span data-ttu-id="96834-120">Kural depolama konumları</span><span class="sxs-lookup"><span data-stu-id="96834-120">Rule storage locations</span></span>

<span data-ttu-id="96834-121">Kurallar hakkında bilgileri iki konumda kalıcıdır:</span><span class="sxs-lookup"><span data-stu-id="96834-121">Information about rules is persisted in two locations:</span></span>

* <span data-ttu-id="96834-122">**DeviceRulesNormalizedTable** tablo – bu tablo bir normalleştirilmiş depolar hello çözüm portalı tarafından tanımlanan toohello kurallar başvuru.</span><span class="sxs-lookup"><span data-stu-id="96834-122">**DeviceRulesNormalizedTable** table – This table stores a normalized reference toohello rules defined by hello solution portal.</span></span> <span data-ttu-id="96834-123">Merhaba çözüm portalı cihaz kuralları görüntülediğinde, bu tablo hello kuralı tanımları için sorgular.</span><span class="sxs-lookup"><span data-stu-id="96834-123">When hello solution portal displays device rules, it queries this table for hello rule definitions.</span></span>
* <span data-ttu-id="96834-124">**DeviceRules** blob – bu blob tüm kayıtlı cihazlar ve bir başvuru giriş toohello Azure akış analizi işi tanımlanan tanımlanan tüm hello kurallar depolar.</span><span class="sxs-lookup"><span data-stu-id="96834-124">**DeviceRules** blob – This blob stores all hello rules defined for all registered devices and is defined as a reference input toohello Azure Stream Analytics jobs.</span></span>
 
<span data-ttu-id="96834-125">Mevcut bir kuralı güncelleştirmek veya yeni bir kural hello çözüm Portalı'nda tanımlamak, hem hello tablosunda hem de blob güncelleştirilmiş tooreflect hello değişir.</span><span class="sxs-lookup"><span data-stu-id="96834-125">When you update an existing rule or define a new rule in hello solution portal, both hello table and blob are updated tooreflect hello changes.</span></span> <span data-ttu-id="96834-126">Merhaba kural tanımı hello Portalı'nda görüntülenen hello tablo deposu ve hello kural tanımı hello Stream Analytics işleri tarafından başvurulan hello blobundan gelen gelir.</span><span class="sxs-lookup"><span data-stu-id="96834-126">hello rule definition displayed in hello portal comes from hello table store, and hello rule definition referenced by hello Stream Analytics jobs comes from hello blob.</span></span> 

## <a name="update-hello-remotemonitoring-visual-studio-solution"></a><span data-ttu-id="96834-127">Merhaba RemoteMonitoring Visual Studio çözümünü güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="96834-127">Update hello RemoteMonitoring Visual Studio solution</span></span>

<span data-ttu-id="96834-128">Merhaba aşağıdaki adımlar, nasıl toomodify hello RemoteMonitoring Visual Studio çözümü tooinclude hello kullanan yeni bir kural gösterir **ExternalTemperature** hello benzetimli aygıtından gönderilen telemetri:</span><span class="sxs-lookup"><span data-stu-id="96834-128">hello following steps show you how toomodify hello RemoteMonitoring Visual Studio solution tooinclude a new rule that uses hello **ExternalTemperature** telemetry sent from hello simulated device:</span></span>

1. <span data-ttu-id="96834-129">Zaten, kopya hello yapmadıysanız, **azure-iot-remote-monitoring** makinenizde Git komut aşağıdaki hello kullanarak yerel deposu tooa uygun konumu:</span><span class="sxs-lookup"><span data-stu-id="96834-129">If you have not already done so, clone hello **azure-iot-remote-monitoring** repository tooa suitable location on your local machine using hello following Git command:</span></span>

    ```
    git clone https://github.com/Azure/azure-iot-remote-monitoring.git
    ```

2. <span data-ttu-id="96834-130">Visual Studio'da hello RemoteMonitoring.sln dosyasını hello yerel kopyadan açın **azure-iot-remote-monitoring** deposu.</span><span class="sxs-lookup"><span data-stu-id="96834-130">In Visual Studio, open hello RemoteMonitoring.sln file from your local copy of hello **azure-iot-remote-monitoring** repository.</span></span>

3. <span data-ttu-id="96834-131">Merhaba dosyasını Infrastructure\Models\DeviceRuleBlobEntity.cs açın ve eklemek bir **ExternalTemperature** özelliğini aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="96834-131">Open hello file Infrastructure\Models\DeviceRuleBlobEntity.cs and add an **ExternalTemperature** property as follows:</span></span>

    ```csharp
    public double? Temperature { get; set; }
    public double? Humidity { get; set; }
    public double? ExternalTemperature { get; set; }
    ```

4. <span data-ttu-id="96834-132">Buna Merhaba aynı dosya, ekleme bir **ExternalTemperatureRuleOutput** özelliğini aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="96834-132">In hello same file, add an **ExternalTemperatureRuleOutput** property as follows:</span></span>

    ```csharp
    public string TemperatureRuleOutput { get; set; }
    public string HumidityRuleOutput { get; set; }
    public string ExternalTemperatureRuleOutput { get; set; }
    ```

5. <span data-ttu-id="96834-133">Merhaba dosyasını Infrastructure\Models\DeviceRuleDataFields.cs açın ve hello aşağıdakileri ekleyin **ExternalTemperature** hello varolan sonra özelliği **nem** özelliği:</span><span class="sxs-lookup"><span data-stu-id="96834-133">Open hello file Infrastructure\Models\DeviceRuleDataFields.cs and add hello following **ExternalTemperature** property after hello existing **Humidity** property:</span></span>

    ```csharp
    public static string ExternalTemperature
    {
        get { return "ExternalTemperature"; }
    }
    ```

6. <span data-ttu-id="96834-134">Buna Merhaba aynı dosya, güncelleştirme hello **_availableDataFields** yöntemi tooinclude **ExternalTemperature** gibi:</span><span class="sxs-lookup"><span data-stu-id="96834-134">In hello same file, update hello **_availableDataFields** method tooinclude **ExternalTemperature** as follows:</span></span>

    ```csharp
    private static List<string> _availableDataFields = new List<string>
    {                    
        Temperature, Humidity, ExternalTemperature
    };
    ```

7. <span data-ttu-id="96834-135">Merhaba dosyasını Infrastructure\Repository\DeviceRulesRepository.cs açın ve hello değiştirin **BuildBlobEntityListFromTableRows** yöntemini aşağıdaki şekilde:</span><span class="sxs-lookup"><span data-stu-id="96834-135">Open hello file Infrastructure\Repository\DeviceRulesRepository.cs and modify hello **BuildBlobEntityListFromTableRows** method as follows:</span></span>

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

## <a name="rebuild-and-redeploy-hello-solution"></a><span data-ttu-id="96834-136">Yeniden oluşturun ve hello çözümü yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="96834-136">Rebuild and redeploy hello solution.</span></span>

<span data-ttu-id="96834-137">Güncelleştirilmiş hello çözüm tooyour Azure abonelik artık dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96834-137">You can now deploy hello updated solution tooyour Azure subscription.</span></span>

1. <span data-ttu-id="96834-138">Yükseltilmiş bir komut istemi açın ve hello azure-iot-remote-monitoring deposu yerel kopyasını toohello köküne gidin.</span><span class="sxs-lookup"><span data-stu-id="96834-138">Open an elevated command prompt and navigate toohello root of your local copy of hello azure-iot-remote-monitoring repository.</span></span>

2. <span data-ttu-id="96834-139">toodeploy komutu değiştirerek aşağıdaki hello çalıştırmak çözümünüzü güncelleştirilmiş **{dağıtım adı}** önceden yapılandırılmış çözüm dağıtımınızın, daha önce not ettiğiniz hello adıyla:</span><span class="sxs-lookup"><span data-stu-id="96834-139">toodeploy your updated solution, run hello following command substituting **{deployment name}** with hello name of your preconfigured solution deployment that you noted previously:</span></span>

    ```
    build.cmd cloud release {deployment name}
    ```

## <a name="update-hello-stream-analytics-job"></a><span data-ttu-id="96834-140">Güncelleştirme hello Stream Analytics işi</span><span class="sxs-lookup"><span data-stu-id="96834-140">Update hello Stream Analytics job</span></span>

<span data-ttu-id="96834-141">Merhaba dağıtım tamamlandığında, hello Stream Analytics işi toouse hello yeni kural tanımları güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96834-141">When hello deployment is complete, you can update hello Stream Analytics job toouse hello new rule definitions.</span></span>

1. <span data-ttu-id="96834-142">Hello Azure portalı, önceden yapılandırılmış çözüm kaynaklarınızı içeren toohello kaynak grubunu gidin.</span><span class="sxs-lookup"><span data-stu-id="96834-142">In hello Azure portal, navigate toohello resource group that contains your preconfigured solution resources.</span></span> <span data-ttu-id="96834-143">Bu kaynak grubu aynı ad için belirttiğiniz hello sahip çözüm hello dağıtımı sırasında hello.</span><span class="sxs-lookup"><span data-stu-id="96834-143">This resource group has hello same name you specified for hello solution during hello deployment.</span></span>

2. <span data-ttu-id="96834-144">Toohello {dağıtım adı} gidin-kuralları Stream Analytics işi.</span><span class="sxs-lookup"><span data-stu-id="96834-144">Navigate toohello {deployment name}-Rules Stream Analytics job.</span></span> 

3. <span data-ttu-id="96834-145">Tıklatın **durdurmak** toostop hello Stream Analytics işi çalışmasını.</span><span class="sxs-lookup"><span data-stu-id="96834-145">Click **Stop** toostop hello Stream Analytics job from running.</span></span> <span data-ttu-id="96834-146">(Merhaba sorgu düzenleyebilmeniz iş toostop akış hello için beklemeniz gerekir).</span><span class="sxs-lookup"><span data-stu-id="96834-146">(You must wait for hello streaming job toostop before you can edit hello query).</span></span>

4. <span data-ttu-id="96834-147">Tıklatın **sorgu**.</span><span class="sxs-lookup"><span data-stu-id="96834-147">Click **Query**.</span></span> <span data-ttu-id="96834-148">Merhaba sorgu tooinclude hello Düzenle **seçin** bildirimi **ExternalTemperature**.</span><span class="sxs-lookup"><span data-stu-id="96834-148">Edit hello query tooinclude hello **SELECT** statement for **ExternalTemperature**.</span></span> <span data-ttu-id="96834-149">Merhaba aşağıdaki örnek hello tam sorgu hello ile yeni gösterir **seçin** deyimi:</span><span class="sxs-lookup"><span data-stu-id="96834-149">hello following sample shows hello complete query with hello new **SELECT** statement:</span></span>

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

5. <span data-ttu-id="96834-150">Tıklatın **kaydetmek** toochange hello kural sorgu güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="96834-150">Click **Save** toochange hello updated rule query.</span></span>

6. <span data-ttu-id="96834-151">Tıklatın **Başlat** toostart hello Stream Analytics işi yeniden çalıştırmayı.</span><span class="sxs-lookup"><span data-stu-id="96834-151">Click **Start** toostart hello Stream Analytics job running again.</span></span>

## <a name="add-your-new-rule-in-hello-dashboard"></a><span data-ttu-id="96834-152">Merhaba panosunda, yeni bir kural ekleyin</span><span class="sxs-lookup"><span data-stu-id="96834-152">Add your new rule in hello dashboard</span></span>

<span data-ttu-id="96834-153">Merhaba artık ekleyebilirsiniz **ExternalTemperature** hello çözüm panosunda kural tooa aygıt.</span><span class="sxs-lookup"><span data-stu-id="96834-153">You can now add hello **ExternalTemperature** rule tooa device in hello solution dashboard.</span></span>

1. <span data-ttu-id="96834-154">Toohello çözüm portalı gidin.</span><span class="sxs-lookup"><span data-stu-id="96834-154">Navigate toohello solution portal.</span></span>

2. <span data-ttu-id="96834-155">Toohello gidin **aygıtları** paneli.</span><span class="sxs-lookup"><span data-stu-id="96834-155">Navigate toohello **Devices** panel.</span></span>

3. <span data-ttu-id="96834-156">Gönderen, oluşturduğunuz hello özel cihaz bulun **ExternalTemperature** telemetri ve hello **cihaz ayrıntıları** öğesine tıklayın **Kuralı Ekle**.</span><span class="sxs-lookup"><span data-stu-id="96834-156">Locate hello custom device you created that sends **ExternalTemperature** telemetry and on hello **Device Details** panel, click **Add Rule**.</span></span>

4. <span data-ttu-id="96834-157">Seçin **ExternalTemperature** içinde **veri alanı**.</span><span class="sxs-lookup"><span data-stu-id="96834-157">Select **ExternalTemperature** in **Data Field**.</span></span>

5. <span data-ttu-id="96834-158">Ayarlama **eşik** too56.</span><span class="sxs-lookup"><span data-stu-id="96834-158">Set **Threshold** too56.</span></span> <span data-ttu-id="96834-159">Ardından **kaydedin ve kuralları**.</span><span class="sxs-lookup"><span data-stu-id="96834-159">Then click **Save and view rules**.</span></span>

6. <span data-ttu-id="96834-160">Toohello Pano tooview hello alarm geçmişi döndür.</span><span class="sxs-lookup"><span data-stu-id="96834-160">Return toohello dashboard tooview hello alarm history.</span></span>

7. <span data-ttu-id="96834-161">Hello konsol penceresi açık sol hello Node.js konsol uygulaması toobegin göndermeye Başla **ExternalTemperature** telemetri verileri.</span><span class="sxs-lookup"><span data-stu-id="96834-161">In hello console window you left open, start hello Node.js console app toobegin sending **ExternalTemperature** telemetry data.</span></span>

8. <span data-ttu-id="96834-162">Bu hello fark **Alarm geçmişi** tablo hello yeni kuralı tetiklendiğinde yeni uyarıları gösterir.</span><span class="sxs-lookup"><span data-stu-id="96834-162">Notice that hello **Alarm History** table shows new alarms when hello new rule is triggered.</span></span>
 
## <a name="additional-information"></a><span data-ttu-id="96834-163">Ek bilgiler</span><span class="sxs-lookup"><span data-stu-id="96834-163">Additional information</span></span>

<span data-ttu-id="96834-164">Değişen hello işleci  **>**  daha karmaşıktır ve Bu öğreticide gösterilen hello adımları ötesine geçer.</span><span class="sxs-lookup"><span data-stu-id="96834-164">Changing hello operator **>** is more complex and goes beyond hello steps outlined in this tutorial.</span></span> <span data-ttu-id="96834-165">İstediğiniz ne olursa olsun işleci hello Stream Analytics işi toouse değiştirebilirsiniz, ancak bu işleci hello çözüm portalında yansıtma daha karmaşık bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="96834-165">While you can change hello Stream Analytics job toouse whatever operator you like, reflecting that operator in hello solution portal is a more complex task.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="96834-166">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="96834-166">Next steps</span></span>
<span data-ttu-id="96834-167">Nasıl toocreate özel kurallar, daha fazla hello önceden yapılandırılmış çözümleri hakkında bilgi edinebilirsiniz gördünüz göre:</span><span class="sxs-lookup"><span data-stu-id="96834-167">Now that you've seen how toocreate custom rules, you can learn more about hello preconfigured solutions:</span></span>

- <span data-ttu-id="96834-168">[Mantıksal uygulama tooyour Azure IOT paketi uzaktan önceden yapılandırılmış izleme çözümü bağlantı][lnk-logic-app]</span><span class="sxs-lookup"><span data-stu-id="96834-168">[Connect Logic App tooyour Azure IoT Suite Remote Monitoring preconfigured solution][lnk-logic-app]</span></span>
- <span data-ttu-id="96834-169">[Merhaba Uzaktan izleme aygıt bilgileri meta verileri önceden yapılandırılmış çözüm][lnk-devinfo].</span><span class="sxs-lookup"><span data-stu-id="96834-169">[Device information metadata in hello remote monitoring preconfigured solution][lnk-devinfo].</span></span>

[lnk-devinfo]: iot-suite-remote-monitoring-device-info.md

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-node]: http://nodejs.org
[lnk-builtin-rule]: iot-suite-getstarted-preconfigured-solutions.md#view-alarms
[lnk-dynamic-telemetry]: iot-suite-dynamic-telemetry.md
[lnk-logic-app]: iot-suite-logic-apps-tutorial.md