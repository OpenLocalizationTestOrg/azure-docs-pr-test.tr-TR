---
title: "bir Azure IOT Hub'in bir şablon (.NET) kullanılarak aaaCreate | Microsoft Docs"
description: "Nasıl toouse Azure Resource Manager şablonu toocreate bir IOT Hub ile C# programı."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a447b40c-c728-487e-875d-db554db5adc3
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6140deff3553701f994502fd4a60178f874e27cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="0f60e-103">Azure Resource Manager şablonu (.NET) kullanılarak IOT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f60e-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="0f60e-104">Azure Resource Manager toocreate kullanın ve Azure IOT hub'ları program aracılığıyla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f60e-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="0f60e-105">Bu öğretici şunların nasıl yapıldığını gösterir toouse Azure Resource Manager şablonu toocreate IOT hub'ından bir C# programı.</span><span class="sxs-lookup"><span data-stu-id="0f60e-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="0f60e-106">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="0f60e-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="0f60e-107">Bu makalede, hello Azure Resource Manager dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="0f60e-108">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="0f60e-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="0f60e-109">Visual Studio 2015 veya Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="0f60e-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="0f60e-110">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="0f60e-110">An active Azure account.</span></span> <br/><span data-ttu-id="0f60e-111">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f60e-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="0f60e-112">Bir [Azure depolama hesabı] [ lnk-storage-account] Azure Resource Manager şablonu dosyalarınızı depolayabileceğiniz.</span><span class="sxs-lookup"><span data-stu-id="0f60e-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="0f60e-113">[Azure PowerShell 1.0] [ lnk-powershell-install] veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="0f60e-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="0f60e-114">Visual Studio projenizi hazırlama</span><span class="sxs-lookup"><span data-stu-id="0f60e-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="0f60e-115">Visual Studio'da hello kullanarak bir Visual C# Windows Klasik Masaüstü projesi oluşturma **konsol uygulaması (.NET Framework)** proje şablonu.</span><span class="sxs-lookup"><span data-stu-id="0f60e-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="0f60e-116">Ad hello proje **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-116">Name hello project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="0f60e-117">Çözüm Gezgini'nde, projeye sağ tıklayın ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="0f60e-118">NuGet Paket Yöneticisi'nde denetleyin **INCLUDE yayın öncesi**ve hello **Gözat** sayfası Ara **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-118">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="0f60e-119">Hello paketi seçin, **yüklemek**, **değişiklikleri gözden** tıklatın **Tamam**, ardından **kabul ediyorum** tooaccept hello lisansları.</span><span class="sxs-lookup"><span data-stu-id="0f60e-119">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="0f60e-120">NuGet Paket Yöneticisi'nde arayın **Microsoft.IdentityModel.Clients.activedirectory tarafından**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="0f60e-121">' I tıklatın **yüklemek**, **değişiklikleri gözden** tıklatın **Tamam**, ardından **kabul ediyorum** tooaccept hello lisans.</span><span class="sxs-lookup"><span data-stu-id="0f60e-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="0f60e-122">Program.cs içinde hello varolan **kullanarak** koddan hello ifadelerle:</span><span class="sxs-lookup"><span data-stu-id="0f60e-122">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="0f60e-123">Program.cs içinde statik değişkenler hello yer tutucu değerlerini değiştirerek aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="0f60e-123">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="0f60e-124">Not yapılan **ApplicationId**, **Subscriptionıd**, **Tenantıd**, ve **parola** Bu öğreticinin önceki.</span><span class="sxs-lookup"><span data-stu-id="0f60e-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="0f60e-125">**Azure depolama hesabınızın adını** hello hello Azure depolama hesabı, Azure Resource Manager şablon dosyalarını depoladığınız adıdır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-125">**Your Azure Storage account name** is hello name of hello Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="0f60e-126">**Kaynak grubu adı** hello hello IOT hub'ı oluşturduğunuzda kullandığınız hello kaynak grubunun adıdır.</span><span class="sxs-lookup"><span data-stu-id="0f60e-126">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="0f60e-127">Merhaba adı önceden varolan veya yeni bir kaynak grubu olabilir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-127">hello name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="0f60e-128">**Dağıtım adı** hello dağıtımı için bir ad olduğu gibi **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    static string storageAddress = "https://{Your storage account name}.blob.core.windows.net";
    static string rgName = "{Resource group name}";
    static string deploymentName = "{Deployment name}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="0f60e-129">Bir şablon toocreate IOT hub'ı gönderme</span><span class="sxs-lookup"><span data-stu-id="0f60e-129">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="0f60e-130">Kaynak grubunda bir JSON şablonu ve parametre dosyası toocreate IOT hub'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f60e-130">Use a JSON template and parameter file toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="0f60e-131">Ayrıca, Azure Resource Manager şablonu toomake değişiklikleri tooan var olan IOT hub'ı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f60e-131">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="0f60e-132">Çözüm Gezgini'nde, projeye sağ tıklayın, **Ekle**ve ardından **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="0f60e-133">Adlı bir JSON dosyası ekleme **template.json** tooyour projesi.</span><span class="sxs-lookup"><span data-stu-id="0f60e-133">Add a JSON file called **template.json** tooyour project.</span></span>

2. <span data-ttu-id="0f60e-134">Standart bir IOT hub toohello tooadd **Doğu ABD** bölge, Değiştir Merhaba içeriğine **template.json** kaynak tanımı aşağıdaki hello ile.</span><span class="sxs-lookup"><span data-stu-id="0f60e-134">tooadd a standard IoT hub toohello **East US** region, replace hello contents of **template.json** with hello following resource definition.</span></span> <span data-ttu-id="0f60e-135">Merhaba geçerli IOT hub'ı destekleyen bölgelerin listesi için bkz: [Azure durumu][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="0f60e-135">For hello current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

3. <span data-ttu-id="0f60e-136">Çözüm Gezgini'nde, projeye sağ tıklayın, **Ekle**ve ardından **yeni öğe**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="0f60e-137">Adlı bir JSON dosyası ekleme **parameters.json** tooyour projesi.</span><span class="sxs-lookup"><span data-stu-id="0f60e-137">Add a JSON file called **parameters.json** tooyour project.</span></span>

4. <span data-ttu-id="0f60e-138">Merhaba Değiştir **parameters.json** hello yeni IOT hub için bir ad gibi ayarlar parametre bilgileri aşağıdaki hello ile **{adınızın baş harflerini} mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-138">Replace hello contents of **parameters.json** with hello following parameter information that sets a name for hello new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="0f60e-139">adı veya baş harfleri içermelidir şekilde hello IOT hub'ı adı genel olarak benzersiz olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="0f60e-139">hello IoT hub name must be globally unique so it should include your name or initials:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": { "value": "mynewiothub" }
      }
    }
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

5. <span data-ttu-id="0f60e-140">İçinde **Sunucu Gezgini**tooyour Azure aboneliğine bağlanma ve, Azure Storage hesabı oluşturma adlı bir kapsayıcı **şablonları**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-140">In **Server Explorer**, connect tooyour Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="0f60e-141">Merhaba, **özellikleri** paneli, kümesi hello **herkese okuma erişimi** hello izinlerini **şablonları** kapsayıcı çok**Blob**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-141">In hello **Properties** panel, set hello **Public Read Access** permissions for hello **templates** container too**Blob**.</span></span>

6. <span data-ttu-id="0f60e-142">İçinde **Sunucu Gezgini**, hello üzerinde sağ **şablonları** kapsayıcı ve ardından **görünüm Blob kapsayıcısını**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-142">In **Server Explorer**, right-click on hello **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="0f60e-143">Merhaba tıklatın **karşıya Blob** düğmesini tıklatın, hello iki dosyayı seçmeniz **parameters.json** ve **templates.json**ve ardından **açık** tooupload hello JSON dosyaları toohello **şablonları** kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="0f60e-143">Click hello **Upload Blob** button, select hello two files, **parameters.json** and **templates.json**, and then click **Open** tooupload hello JSON files toohello **templates** container.</span></span> <span data-ttu-id="0f60e-144">Merhaba JSON verilerini içeren hello BLOB'ları Hello URL'lerini şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0f60e-144">hello URLs of hello blobs containing hello JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="0f60e-145">Yöntem tooProgram.cs aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="0f60e-145">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="0f60e-146">Aşağıdaki kodu toohello hello eklemek **CreateIoTHub** yöntemi toosubmit hello şablonu ve parametre dosyalarını toohello Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="0f60e-146">Add hello following code toohello **CreateIoTHub** method toosubmit hello template and parameter files toohello Azure Resource Manager:</span></span>

    ```csharp
    var createResponse = client.Deployments.CreateOrUpdate(
        rgName,
        deploymentName,
        new Deployment()
        {
          Properties = new DeploymentProperties
          {
            Mode = DeploymentMode.Incremental,
            TemplateLink = new TemplateLink
            {
              Uri = storageAddress + "/templates/template.json"
            },
            ParametersLink = new ParametersLink
            {
              Uri = storageAddress + "/templates/parameters.json"
            }
          }
        });
    ```

9. <span data-ttu-id="0f60e-147">Aşağıdaki kodu toohello hello eklemek **CreateIoTHub** hello durumunu ve hello yeni IOT hub'ı hello tuşları görüntüler yöntemi:</span><span class="sxs-lookup"><span data-stu-id="0f60e-147">Add hello following code toohello **CreateIoTHub** method that displays hello status and hello keys for hello new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="0f60e-148">Tam ve çalışma Merhaba uygulaması</span><span class="sxs-lookup"><span data-stu-id="0f60e-148">Complete and run hello application</span></span>

<span data-ttu-id="0f60e-149">Merhaba uygulaması tarafından arama hello şimdi tamamlayabilirsiniz **CreateIoTHub** oluşturmak ve çalıştırmak için önce yöntemi.</span><span class="sxs-lookup"><span data-stu-id="0f60e-149">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="0f60e-150">Kod toohello hello sonuna aşağıdaki hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="0f60e-150">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="0f60e-151">Tıklatın **yapı** ve ardından **yapı çözümü**.</span><span class="sxs-lookup"><span data-stu-id="0f60e-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="0f60e-152">Hataları düzeltin.</span><span class="sxs-lookup"><span data-stu-id="0f60e-152">Correct any errors.</span></span>

3. <span data-ttu-id="0f60e-153">Tıklatın **hata ayıklama** ve ardından **hata ayıklamayı Başlat** toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="0f60e-153">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="0f60e-154">Merhaba dağıtım toorun için birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="0f60e-154">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="0f60e-155">Uygulamanızı eklenen tooverify hello yeni IOT hub'ı ziyaret edin hello [Azure portal] [ lnk-azure-portal] ve kaynakları listesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="0f60e-155">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="0f60e-156">Alternatif olarak, hello kullanın **Get-AzureRmResource** PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0f60e-156">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="0f60e-157">Bu örnek uygulama S1 standart IOT için faturalandırılır hub'ı ekler.</span><span class="sxs-lookup"><span data-stu-id="0f60e-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="0f60e-158">Merhaba IOT hub'ı hello aracılığıyla silebilirsiniz [Azure portal] [ lnk-azure-portal] veya hello kullanarak **Kaldır AzureRmResource** bitirdiğinizde PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="0f60e-158">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f60e-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0f60e-159">Next steps</span></span>
<span data-ttu-id="0f60e-160">Bir C# programı ile bir Azure Resource Manager şablonu kullanarak bir IOT hub dağıttığınız artık daha fazla tooexplore isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0f60e-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want tooexplore further:</span></span>

* <span data-ttu-id="0f60e-161">Merhaba Hello özellikleri hakkında okuyun [IOT hub'ı kaynak sağlayıcısı REST API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="0f60e-161">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="0f60e-162">Okuma [Azure Resource Manager'a genel bakış] [ lnk-azure-rm-overview] toolearn hello özellikleri Azure Kaynak Yöneticisi'nin hakkında daha fazla.</span><span class="sxs-lookup"><span data-stu-id="0f60e-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="0f60e-163">IOT hub'ı geliştirme hakkında daha fazla toolearn makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="0f60e-163">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="0f60e-164">[Giriş tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="0f60e-164">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="0f60e-165">[Azure IOT SDK'ları][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="0f60e-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="0f60e-166">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="0f60e-166">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="0f60e-167">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="0f60e-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
