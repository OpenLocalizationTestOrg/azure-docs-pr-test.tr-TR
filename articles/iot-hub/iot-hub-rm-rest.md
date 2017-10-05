---
title: "Kaynak sağlayıcısı REST API kullanarak Azure IOT hub oluşturma | Microsoft Docs"
description: "IOT hub'ı oluşturmak için kaynak sağlayıcısı REST API kullanma"
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
ms.openlocfilehash: e443259507aacbefca141be4c9c1688ab19bf6ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-resource-provider-rest-api-net"></a><span data-ttu-id="286a4-103">Kaynak sağlayıcısı REST API (.NET) kullanılarak IOT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="286a4-103">Create an IoT hub using the resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="286a4-104">Kullanabileceğiniz [IOT hub'ı kaynak sağlayıcısı REST API] [ lnk-rest-api] oluşturmak ve Azure IOT hub'ları programlı olarak yönetmek için.</span><span class="sxs-lookup"><span data-stu-id="286a4-104">You can use the [IoT Hub resource provider REST API][lnk-rest-api] to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="286a4-105">Bu öğretici, IOT hub'ı kaynak sağlayıcısı REST API IOT hub'ı bir C# programı oluşturmak için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="286a4-105">This tutorial shows you how to use the IoT Hub resource provider REST API to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="286a4-106">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="286a4-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="286a4-107">Bu makalede, Azure Resource Manager dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="286a4-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="286a4-108">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="286a4-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="286a4-109">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="286a4-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="286a4-110">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="286a4-110">An active Azure account.</span></span> <br/><span data-ttu-id="286a4-111">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="286a4-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="286a4-112">[Azure PowerShell 1.0] [ lnk-powershell-install] veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="286a4-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="286a4-113">Visual Studio projenizi hazırlama</span><span class="sxs-lookup"><span data-stu-id="286a4-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="286a4-114">Visual Studio'da kullanarak bir Visual C# Windows Klasik Masaüstü projesi oluşturma **konsol uygulaması (.NET Framework)** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="286a4-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="286a4-115">Proje adı **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="286a4-115">Name the project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="286a4-116">Çözüm Gezgini'nde, projeye sağ tıklayın ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="286a4-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="286a4-117">NuGet Paket Yöneticisi'nde denetleyin **INCLUDE yayın öncesi**ve **Gözat** sayfası Ara **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="286a4-117">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="286a4-118">Paketi seçin, **yüklemek**, **değişiklikleri gözden** tıklatın **Tamam**, ardından **kabul ediyorum** lisanslar kabul etmek için.</span><span class="sxs-lookup"><span data-stu-id="286a4-118">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="286a4-119">NuGet Paket Yöneticisi'nde arayın **Microsoft.IdentityModel.Clients.activedirectory tarafından**.</span><span class="sxs-lookup"><span data-stu-id="286a4-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="286a4-120">' I tıklatın **yüklemek**, **değişiklikleri gözden** tıklatın **Tamam**, ardından **kabul ediyorum** lisans kabul etmek için.</span><span class="sxs-lookup"><span data-stu-id="286a4-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="286a4-121">Program.cs içinde varolan **kullanarak** deyimleri ile aşağıdaki kodu:</span><span class="sxs-lookup"><span data-stu-id="286a4-121">In Program.cs, replace the existing **using** statements with the following code:</span></span>

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

6. <span data-ttu-id="286a4-122">Program.cs içinde yer tutucu değerlerini değiştirerek aşağıdaki statik değişkenler ekleyin.</span><span class="sxs-lookup"><span data-stu-id="286a4-122">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="286a4-123">Not yapılan **ApplicationId**, **Subscriptionıd**, **Tenantıd**, ve **parola** Bu öğreticinin önceki.</span><span class="sxs-lookup"><span data-stu-id="286a4-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="286a4-124">**Kaynak grubu adı** IOT hub'ı oluşturduğunuzda kullandığınız kaynak grubunun adı.</span><span class="sxs-lookup"><span data-stu-id="286a4-124">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="286a4-125">Önceden varolan veya yeni bir kaynak grubu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="286a4-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="286a4-126">**IOT hub'ı adı** gibi oluşturduğunuz IOT Hub adı **MyIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="286a4-126">**IoT Hub name** is the name of the IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="286a4-127">IOT hub'ınızı adı genel olarak benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="286a4-127">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="286a4-128">**Dağıtım adı** dağıtımı için bir ad olduğu gibi **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="286a4-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

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

## <a name="use-the-resource-provider-rest-api-to-create-an-iot-hub"></a><span data-ttu-id="286a4-129">IOT hub'ı oluşturmak için kaynak sağlayıcısı REST API kullanın</span><span class="sxs-lookup"><span data-stu-id="286a4-129">Use the resource provider REST API to create an IoT hub</span></span>

<span data-ttu-id="286a4-130">Kullanım [IOT hub'ı kaynak sağlayıcısı REST API] [ lnk-rest-api] IOT hub'ı, kaynak grubu oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="286a4-130">Use the [IoT Hub resource provider REST API][lnk-rest-api] to create an IoT hub in your resource group.</span></span> <span data-ttu-id="286a4-131">Var olan bir IOT hub'ına değişiklik yapmak için kaynak sağlayıcısı REST API de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="286a4-131">You can also use the resource provider REST API to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="286a4-132">Aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="286a4-132">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="286a4-133">Aşağıdaki kodu ekleyin **CreateIoTHub** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="286a4-133">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="286a4-134">Bu kod oluşturur bir **HttpClient** nesne kimlik doğrulama belirteci üst bilgileri ile:</span><span class="sxs-lookup"><span data-stu-id="286a4-134">This code creates an **HttpClient** object with the authentication token in the headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="286a4-135">Aşağıdaki kodu ekleyin **CreateIoTHub** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="286a4-135">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="286a4-136">Bu kod, IOT hub'ı oluşturmak için açıklar ve bir JSON temsili üretir.</span><span class="sxs-lookup"><span data-stu-id="286a4-136">This code describes the IoT hub to create and generates a JSON representation.</span></span> <span data-ttu-id="286a4-137">IOT hub'ı destekleyen konumları geçerli listesi için bkz [Azure durumu][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="286a4-137">For the current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

4. <span data-ttu-id="286a4-138">Aşağıdaki kodu ekleyin **CreateIoTHub** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="286a4-138">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="286a4-139">Bu kod Azure REST isteği gönderir.</span><span class="sxs-lookup"><span data-stu-id="286a4-139">This code submits the REST request to Azure.</span></span> <span data-ttu-id="286a4-140">Kod yanıtı denetler ve dağıtım görev durumunu izlemek için kullanabileceğiniz URL'sini alır:</span><span class="sxs-lookup"><span data-stu-id="286a4-140">The code then checks the response and retrieves the URL you can use to monitor the state of the deployment task:</span></span>

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

5. <span data-ttu-id="286a4-141">Sonuna aşağıdaki kodu ekleyin **CreateIoTHub** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="286a4-141">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="286a4-142">Bu kodu kullanır **asyncStatusUri** adresi alınan dağıtım tamamlanmasını beklemek için önceki adımda:</span><span class="sxs-lookup"><span data-stu-id="286a4-142">This code uses the **asyncStatusUri** address retrieved in the previous step to wait for the deployment to complete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="286a4-143">Sonuna aşağıdaki kodu ekleyin **CreateIoTHub** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="286a4-143">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="286a4-144">Bu kod IOT hub oluşturulur ve bunları konsola yazdırır anahtarları alır:</span><span class="sxs-lookup"><span data-stu-id="286a4-144">This code retrieves the keys of the IoT hub you created and prints them to the console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="286a4-145">Tamamlayın ve uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="286a4-145">Complete and run the application</span></span>

<span data-ttu-id="286a4-146">Çağırarak uygulamayı şimdi tamamlayabilirsiniz **CreateIoTHub** oluşturmak ve çalıştırmak için önce yöntemi.</span><span class="sxs-lookup"><span data-stu-id="286a4-146">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="286a4-147">Sonuna aşağıdaki kodu ekleyin **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="286a4-147">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="286a4-148">Tıklatın **yapı** ve ardından **yapı çözümü**.</span><span class="sxs-lookup"><span data-stu-id="286a4-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="286a4-149">Hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="286a4-149">Correct any errors.</span></span>

3. <span data-ttu-id="286a4-150">Tıklatın **hata ayıklama** ve ardından **hata ayıklamayı Başlat** uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="286a4-150">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="286a4-151">Çalıştırmak için dağıtım için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="286a4-151">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="286a4-152">Uygulamanızı yeni IOT hub'ı eklediğinizi doğrulamak için ziyaret [Azure portal] [ lnk-azure-portal] ve kaynakları listesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="286a4-152">To verify that your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="286a4-153">Alternatif olarak, kullanın **Get-AzureRmResource** PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="286a4-153">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="286a4-154">Bu örnek uygulama S1 standart IOT için faturalandırılır hub'ı ekler.</span><span class="sxs-lookup"><span data-stu-id="286a4-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="286a4-155">İşiniz bittiğinde, IOT hub'ı aracılığıyla silebilirsiniz [Azure portal] [ lnk-azure-portal] veya kullanarak **Kaldır AzureRmResource** bitirdiğinizde PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="286a4-155">When you are finished, you can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="286a4-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="286a4-156">Next steps</span></span>
<span data-ttu-id="286a4-157">Kaynak sağlayıcısı REST API kullanarak IOT hub'ı dağıttığınız artık daha ayrıntılı incelemek isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="286a4-157">Now you have deployed an IoT hub using the resource provider REST API, you may want to explore further:</span></span>

* <span data-ttu-id="286a4-158">Özelliklerinin tamamı hakkında okuyun [IOT hub'ı kaynak sağlayıcısı REST API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="286a4-158">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="286a4-159">Okuma [Azure Resource Manager'a genel bakış] [ lnk-azure-rm-overview] Azure Kaynak Yöneticisi'nin özellikleri hakkında daha fazla bilgi edinmek için.</span><span class="sxs-lookup"><span data-stu-id="286a4-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="286a4-160">IOT Hub için geliştirme hakkında daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="286a4-160">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="286a4-161">[C SDK Giriş][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="286a4-161">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="286a4-162">[Azure IOT SDK'ları][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="286a4-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="286a4-163">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="286a4-163">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="286a4-164">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="286a4-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
