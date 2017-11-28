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
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a><span data-ttu-id="80a00-103">Merhaba kaynak sağlayıcısı REST API (.NET) kullanılarak IOT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="80a00-103">Create an IoT hub using hello resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="80a00-104">Merhaba kullanabilirsiniz [IOT hub'ı kaynak sağlayıcısı REST API] [ lnk-rest-api] toocreate ve Azure IOT hub'ları program aracılığıyla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80a00-104">You can use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="80a00-105">Bu öğretici nasıl toouse hello IOT hub'ı kaynak sağlayıcısı REST API toocreate C# programı IOT hub'ı gösterir.</span><span class="sxs-lookup"><span data-stu-id="80a00-105">This tutorial shows you how toouse hello IoT Hub resource provider REST API toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="80a00-106">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="80a00-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="80a00-107">Bu makalede, hello Azure Resource Manager dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="80a00-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="80a00-108">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="80a00-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="80a00-109">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="80a00-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="80a00-110">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="80a00-110">An active Azure account.</span></span> <br/><span data-ttu-id="80a00-111">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80a00-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="80a00-112">[Azure PowerShell 1.0] [ lnk-powershell-install] veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="80a00-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="80a00-113">Visual Studio projenizi hazırlama</span><span class="sxs-lookup"><span data-stu-id="80a00-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="80a00-114">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi oluşturma **konsol uygulaması (.NET Framework)** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="80a00-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="80a00-115">Ad hello proje **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="80a00-115">Name hello project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="80a00-116">Çözüm Gezgini'nde, projeye sağ tıklayın ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="80a00-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="80a00-117">NuGet Paket Yöneticisi'nde denetleyin **INCLUDE yayın öncesi**ve hello **Gözat** sayfası Ara **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="80a00-117">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="80a00-118">Hello paketi seçin, **yüklemek**, **değişiklikleri gözden** tıklatın **Tamam**, ardından **kabul ediyorum** tooaccept hello lisansları.</span><span class="sxs-lookup"><span data-stu-id="80a00-118">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="80a00-119">NuGet Paket Yöneticisi'nde arayın **Microsoft.IdentityModel.Clients.activedirectory tarafından**.</span><span class="sxs-lookup"><span data-stu-id="80a00-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="80a00-120">' I tıklatın **yüklemek**, **değişiklikleri gözden** tıklatın **Tamam**, ardından **kabul ediyorum** tooaccept hello lisans.</span><span class="sxs-lookup"><span data-stu-id="80a00-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="80a00-121">Program.cs içinde hello varolan **kullanarak** koddan hello ifadelerle:</span><span class="sxs-lookup"><span data-stu-id="80a00-121">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

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

6. <span data-ttu-id="80a00-122">Program.cs içinde statik değişkenler hello yer tutucu değerlerini değiştirerek aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="80a00-122">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="80a00-123">Not yapılan **ApplicationId**, **Subscriptionıd**, **Tenantıd**, ve **parola** Bu öğreticinin önceki.</span><span class="sxs-lookup"><span data-stu-id="80a00-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="80a00-124">**Kaynak grubu adı** hello hello IOT hub'ı oluşturduğunuzda kullandığınız hello kaynak grubunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="80a00-124">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="80a00-125">Önceden varolan veya yeni bir kaynak grubu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80a00-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="80a00-126">**IOT hub'ı adı** hello IOT hub'ı oluşturduğunuz gibi hello adıdır **MyIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="80a00-126">**IoT Hub name** is hello name of hello IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="80a00-127">IOT hub'ınızı Hello adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="80a00-127">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="80a00-128">**Dağıtım adı** hello dağıtımı için bir ad olduğu gibi **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="80a00-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a><span data-ttu-id="80a00-129">Merhaba kaynak sağlayıcısı REST API toocreate IOT hub'ı kullanın</span><span class="sxs-lookup"><span data-stu-id="80a00-129">Use hello resource provider REST API toocreate an IoT hub</span></span>

<span data-ttu-id="80a00-130">Kullanım hello [IOT hub'ı kaynak sağlayıcısı REST API] [ lnk-rest-api] toocreate kaynak grubunuzdaki IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="80a00-130">Use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="80a00-131">Merhaba kaynak sağlayıcısı REST API toomake değişiklikleri tooan var olan IOT hub de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80a00-131">You can also use hello resource provider REST API toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="80a00-132">Yöntem tooProgram.cs aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="80a00-132">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="80a00-133">Aşağıdaki kodu toohello hello eklemek **CreateIoTHub** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="80a00-133">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="80a00-134">Bu kod oluşturur bir **HttpClient** hello kimlik doğrulama belirteci hello üstbilgilerindeki nesnesiyle:</span><span class="sxs-lookup"><span data-stu-id="80a00-134">This code creates an **HttpClient** object with hello authentication token in hello headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="80a00-135">Aşağıdaki kodu toohello hello eklemek **CreateIoTHub** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="80a00-135">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="80a00-136">Bu kod hello IOT hub toocreate açıklar ve bir JSON temsili üretir.</span><span class="sxs-lookup"><span data-stu-id="80a00-136">This code describes hello IoT hub toocreate and generates a JSON representation.</span></span> <span data-ttu-id="80a00-137">Merhaba geçerli IOT hub'ı destekleyen konumların listesini için görmek [Azure durumu][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="80a00-137">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

4. <span data-ttu-id="80a00-138">Aşağıdaki kodu toohello hello eklemek **CreateIoTHub** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="80a00-138">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="80a00-139">Bu kod hello REST isteği tooAzure gönderir.</span><span class="sxs-lookup"><span data-stu-id="80a00-139">This code submits hello REST request tooAzure.</span></span> <span data-ttu-id="80a00-140">Merhaba kod sonra hello yanıtı denetler ve toomonitor hello hello dağıtım görev durumunu kullanabileceğiniz hello URL'sini alır:</span><span class="sxs-lookup"><span data-stu-id="80a00-140">hello code then checks hello response and retrieves hello URL you can use toomonitor hello state of hello deployment task:</span></span>

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

5. <span data-ttu-id="80a00-141">Kod toohello hello sonuna aşağıdaki hello eklemek **CreateIoTHub** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="80a00-141">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="80a00-142">Bu kodu hello kullanır **asyncStatusUri** adresi alınan hello dağıtım toocomplete için önceki adımı toowait hello içinde:</span><span class="sxs-lookup"><span data-stu-id="80a00-142">This code uses hello **asyncStatusUri** address retrieved in hello previous step toowait for hello deployment toocomplete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="80a00-143">Kod toohello hello sonuna aşağıdaki hello eklemek **CreateIoTHub** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="80a00-143">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="80a00-144">Bu kod hello oluşturulur ve toohello konsol yazdırır IOT hub hello anahtarları alır:</span><span class="sxs-lookup"><span data-stu-id="80a00-144">This code retrieves hello keys of hello IoT hub you created and prints them toohello console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="80a00-145">Tam ve çalışma Merhaba uygulaması</span><span class="sxs-lookup"><span data-stu-id="80a00-145">Complete and run hello application</span></span>

<span data-ttu-id="80a00-146">Merhaba uygulaması tarafından arama hello şimdi tamamlayabilirsiniz **CreateIoTHub** oluşturmak ve çalıştırmak için önce yöntemi.</span><span class="sxs-lookup"><span data-stu-id="80a00-146">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="80a00-147">Kod toohello hello sonuna aşağıdaki hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="80a00-147">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="80a00-148">Tıklatın **yapı** ve ardından **yapı çözümü**.</span><span class="sxs-lookup"><span data-stu-id="80a00-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="80a00-149">Hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="80a00-149">Correct any errors.</span></span>

3. <span data-ttu-id="80a00-150">Tıklatın **hata ayıklama** ve ardından **hata ayıklamayı Başlat** toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="80a00-150">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="80a00-151">Merhaba dağıtım toorun için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="80a00-151">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="80a00-152">Uygulamanızı eklenen tooverify hello yeni IOT hub'ı ziyaret edin hello [Azure portal] [ lnk-azure-portal] ve kaynakları listesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="80a00-152">tooverify that your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="80a00-153">Alternatif olarak, hello kullanın **Get-AzureRmResource** PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80a00-153">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="80a00-154">Bu örnek uygulama S1 standart IOT için faturalandırılır hub'ı ekler.</span><span class="sxs-lookup"><span data-stu-id="80a00-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="80a00-155">İşiniz bittiğinde, hello IOT hub'ı hello aracılığıyla silebilirsiniz [Azure portal] [ lnk-azure-portal] veya hello kullanarak **Kaldır AzureRmResource** bitirdiğinizde PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="80a00-155">When you are finished, you can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="80a00-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="80a00-156">Next steps</span></span>
<span data-ttu-id="80a00-157">Bir IOT hub'hello kaynak sağlayıcısı REST API kullanarak dağıttığınız artık daha fazla tooexplore isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="80a00-157">Now you have deployed an IoT hub using hello resource provider REST API, you may want tooexplore further:</span></span>

* <span data-ttu-id="80a00-158">Merhaba Hello özellikleri hakkında okuyun [IOT hub'ı kaynak sağlayıcısı REST API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="80a00-158">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="80a00-159">Okuma [Azure Resource Manager'a genel bakış] [ lnk-azure-rm-overview] toolearn hello özellikleri Azure Kaynak Yöneticisi'nin hakkında daha fazla.</span><span class="sxs-lookup"><span data-stu-id="80a00-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="80a00-160">IOT hub'ı geliştirme hakkında daha fazla toolearn makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="80a00-160">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="80a00-161">[Giriş tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="80a00-161">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="80a00-162">[Azure IOT SDK'ları][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="80a00-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="80a00-163">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="80a00-163">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="80a00-164">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="80a00-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
