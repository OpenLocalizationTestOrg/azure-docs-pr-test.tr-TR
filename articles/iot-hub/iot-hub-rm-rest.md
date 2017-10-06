---
title: "bir Azure IOT hub'ı kullanarak aaaCreate hello kaynak sağlayıcısı REST API | Microsoft Docs"
description: "Nasıl toouse hello kaynak sağlayıcısı REST API toocreate IOT hub'ı."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 52814ee5-bc10-4abe-9eb2-f8973096c2d8
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 98d240ccce47dec13a255bce28943b40f5354ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a>Merhaba kaynak sağlayıcısı REST API (.NET) kullanılarak IOT hub oluşturma

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

Merhaba kullanabilirsiniz [IOT hub'ı kaynak sağlayıcısı REST API] [ lnk-rest-api] toocreate ve Azure IOT hub'ları program aracılığıyla yönetebilirsiniz. Bu öğretici nasıl toouse hello IOT hub'ı kaynak sağlayıcısı REST API toocreate C# programı IOT hub'ı gösterir.

> [!NOTE]
> Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).  Bu makalede, hello Azure Resource Manager dağıtım modeli kullanılarak yer almaktadır.

toocomplete Bu öğretici, aşağıdaki hello gerekir:

* Visual Studio 2015 veya Visual Studio 2017.
* Etkin bir Azure hesabı. <br/>Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.
* [Azure PowerShell 1.0] [ lnk-powershell-install] veya sonraki bir sürümü.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Visual Studio projenizi hazırlama

1. Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi oluşturma **konsol uygulaması (.NET Framework)** proje şablonu. Ad hello proje **CreateIoTHubREST**.

2. Çözüm Gezgini'nde, projeye sağ tıklayın ve ardından **NuGet paketlerini Yönet**.

3. NuGet Paket Yöneticisi'nde denetleyin **INCLUDE yayın öncesi**ve hello **Gözat** sayfası Ara **Microsoft.Azure.Management.ResourceManager**. Hello paketi seçin, **yüklemek**, **değişiklikleri gözden** tıklatın **Tamam**, ardından **kabul ediyorum** tooaccept hello lisansları.

4. NuGet Paket Yöneticisi'nde arayın **Microsoft.IdentityModel.Clients.activedirectory tarafından**.  ' I tıklatın **yüklemek**, **değişiklikleri gözden** tıklatın **Tamam**, ardından **kabul ediyorum** tooaccept hello lisans.

5. Program.cs içinde hello varolan **kullanarak** koddan hello ifadelerle:

    ```csharp
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```

6. Program.cs içinde statik değişkenler hello yer tutucu değerlerini değiştirerek aşağıdaki hello ekleyin. Not yapılan **ApplicationId**, **Subscriptionıd**, **Tenantıd**, ve **parola** Bu öğreticinin önceki. **Kaynak grubu adı** hello hello IOT hub'ı oluşturduğunuzda kullandığınız hello kaynak grubunun adıdır. Önceden varolan veya yeni bir kaynak grubu kullanabilirsiniz. **IOT hub'ı adı** hello IOT hub'ı oluşturduğunuz gibi hello adıdır **MyIoTHub**. IOT hub'ınızı Hello adı genel olarak benzersiz olması gerekir. **Dağıtım adı** hello dağıtımı için bir ad olduğu gibi **Deployment_01**.

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";

    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```
[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a>Merhaba kaynak sağlayıcısı REST API toocreate IOT hub'ı kullanın

Kullanım hello [IOT hub'ı kaynak sağlayıcısı REST API] [ lnk-rest-api] toocreate kaynak grubunuzdaki IOT hub'ı. Merhaba kaynak sağlayıcısı REST API toomake değişiklikleri tooan var olan IOT hub de kullanabilirsiniz.

1. Yöntem tooProgram.cs aşağıdaki hello ekleyin:

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. Aşağıdaki kodu toohello hello eklemek **CreateIoTHub** yöntemi. Bu kod oluşturur bir **HttpClient** hello kimlik doğrulama belirteci hello üstbilgilerindeki nesnesiyle:

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. Aşağıdaki kodu toohello hello eklemek **CreateIoTHub** yöntemi. Bu kod hello IOT hub toocreate açıklar ve bir JSON temsili üretir. Merhaba geçerli IOT hub'ı destekleyen konumların listesini için görmek [Azure durumu][lnk-status]:

    ```csharp
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };

    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```

4. Aşağıdaki kodu toohello hello eklemek **CreateIoTHub** yöntemi. Bu kod hello REST isteği tooAzure gönderir. Merhaba kod sonra hello yanıtı denetler ve toomonitor hello hello dağıtım görev durumunu kullanabileceğiniz hello URL'sini alır:

    ```csharp
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;

    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }

    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```

5. Kod toohello hello sonuna aşağıdaki hello eklemek **CreateIoTHub** yöntemi. Bu kodu hello kullanır **asyncStatusUri** adresi alınan hello dağıtım toocomplete için önceki adımı toowait hello içinde:

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. Kod toohello hello sonuna aşağıdaki hello eklemek **CreateIoTHub** yöntemi. Bu kod hello oluşturulur ve toohello konsol yazdırır IOT hub hello anahtarları alır:

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a>Tam ve çalışma Merhaba uygulaması

Merhaba uygulaması tarafından arama hello şimdi tamamlayabilirsiniz **CreateIoTHub** oluşturmak ve çalıştırmak için önce yöntemi.

1. Kod toohello hello sonuna aşağıdaki hello eklemek **ana** yöntemi:

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. Tıklatın **yapı** ve ardından **yapı çözümü**. Hataları düzeltin.

3. Tıklatın **hata ayıklama** ve ardından **hata ayıklamayı Başlat** toorun Merhaba uygulaması. Merhaba dağıtım toorun için birkaç dakika sürebilir.

4. Uygulamanızı eklenen tooverify hello yeni IOT hub'ı ziyaret edin hello [Azure portal] [ lnk-azure-portal] ve kaynakları listesini görüntüleyin. Alternatif olarak, hello kullanın **Get-AzureRmResource** PowerShell cmdlet'i.

> [!NOTE]
> Bu örnek uygulama S1 standart IOT için faturalandırılır hub'ı ekler. İşiniz bittiğinde, hello IOT hub'ı hello aracılığıyla silebilirsiniz [Azure portal] [ lnk-azure-portal] veya hello kullanarak **Kaldır AzureRmResource** bitirdiğinizde PowerShell cmdlet'i.

## <a name="next-steps"></a>Sonraki adımlar
Bir IOT hub'hello kaynak sağlayıcısı REST API kullanarak dağıttığınız artık daha fazla tooexplore isteyebilirsiniz:

* Merhaba Hello özellikleri hakkında okuyun [IOT hub'ı kaynak sağlayıcısı REST API][lnk-rest-api].
* Okuma [Azure Resource Manager'a genel bakış] [ lnk-azure-rm-overview] toolearn hello özellikleri Azure Kaynak Yöneticisi'nin hakkında daha fazla.

IOT hub'ı geliştirme hakkında daha fazla toolearn makaleler hello bakın:

* [Giriş tooC SDK][lnk-c-sdk]
* [Azure IOT SDK'ları][lnk-sdks]

toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:

* [Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
