---
title: "bir şablon (PowerShell) kullanarak Azure IOT Hub aaaCreate | Microsoft Docs"
description: "Nasıl toouse Azure Resource Manager şablonu toocreate PowerShell ile bir IOT Hub."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 7eade855-c289-4ffb-b5ef-02be8c5f670f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e98ff5e898200cd727b9326fb3df393e43b021e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-powershell"></a><span data-ttu-id="4c60f-103">Azure Resource Manager şablonu (PowerShell) kullanarak IOT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c60f-103">Create an IoT hub using Azure Resource Manager template (PowerShell)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="4c60f-104">Azure Resource Manager toocreate kullanın ve Azure IOT hub'ları program aracılığıyla yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c60f-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="4c60f-105">Bu öğretici şunların nasıl yapıldığını gösterir toouse Azure Resource Manager şablonu toocreate PowerShell ile bir IOT hub.</span><span class="sxs-lookup"><span data-stu-id="4c60f-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="4c60f-106">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4c60f-106">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4c60f-107">Bu makalede, hello Azure Resource Manager dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="4c60f-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="4c60f-108">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c60f-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="4c60f-109">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="4c60f-109">An active Azure account.</span></span> <br/><span data-ttu-id="4c60f-110">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c60f-110">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="4c60f-111">[Azure PowerShell 1.0] [ lnk-powershell-install] veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="4c60f-111">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

> [!TIP]
> <span data-ttu-id="4c60f-112">Merhaba makale [Azure PowerShell kullanarak Azure Resource Manager ile] [ lnk-powershell-arm] hakkında daha fazla bilgi sağlayan toouse PowerShell ve Azure Resource Manager şablonları toocreate Azure kaynakları.</span><span class="sxs-lookup"><span data-stu-id="4c60f-112">hello article [Using Azure PowerShell with Azure Resource Manager][lnk-powershell-arm] provides more information about how toouse PowerShell and Azure Resource Manager templates toocreate Azure resources.</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="4c60f-113">Tooyour Azure aboneliğine bağlanma</span><span class="sxs-lookup"><span data-stu-id="4c60f-113">Connect tooyour Azure subscription</span></span>

<span data-ttu-id="4c60f-114">PowerShell komut isteminde tooyour Azure aboneliği içindeki komut toosign aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="4c60f-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="4c60f-115">Birden çok Azure aboneliğiniz varsa tooAzure imzalama tooall erişim verir kimlik bilgilerinizle ilişkili Azure abonelik hello.</span><span class="sxs-lookup"><span data-stu-id="4c60f-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="4c60f-116">Toouse toolist hello Azure abonelikleri kullanılabilir sizin için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="4c60f-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="4c60f-117">IOT hub'ınızı toocreate toouse toorun hello komutları istediğiniz komut tooselect abonelik aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c60f-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="4c60f-118">Merhaba hello önceki komutunun çıktısından hello abonelik adı veya kimliği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c60f-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

<span data-ttu-id="4c60f-119">Burada bir IOT hub'ı dağıtabilir ve şu anda desteklenen API sürümleri hello komutları toodiscover aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c60f-119">You can use hello following commands toodiscover where you can deploy an IoT hub and hello currently supported API versions:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).Locations
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Devices).ResourceTypes | Where-Object ResourceTypeName -eq IoTHubs).ApiVersions
```

<span data-ttu-id="4c60f-120">Bir kaynak grubu toocontain komutu IOT hub'ına yönelik hello desteklenen konumlardan birinde aşağıdaki hello kullanarak IOT hub'ınızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c60f-120">Create a resource group toocontain your IoT hub using hello following command in one of hello supported locations for IoT Hub.</span></span> <span data-ttu-id="4c60f-121">Bu örnek adlı bir kaynak grubu oluşturur **MyIoTRG1**:</span><span class="sxs-lookup"><span data-stu-id="4c60f-121">This example creates a resource group called **MyIoTRG1**:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="4c60f-122">Bir şablon toocreate IOT hub'ı gönderme</span><span class="sxs-lookup"><span data-stu-id="4c60f-122">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="4c60f-123">Kaynak grubunda bir JSON şablonu toocreate IOT hub'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c60f-123">Use a JSON template toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="4c60f-124">Ayrıca, Azure Resource Manager şablonu toomake değişiklikleri tooan var olan IOT hub'ı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c60f-124">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="4c60f-125">Bir Azure Resource Manager şablonu olarak adlandırılan bir metin düzenleyicisi toocreate kullanmak **template.json** ile yeni bir standart IOT hub kaynak tanımı toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="4c60f-125">Use a text editor toocreate an Azure Resource Manager template called **template.json** with hello following resource definition toocreate a new standard IoT hub.</span></span> <span data-ttu-id="4c60f-126">Bu örnek, hello hello IOT hub'ı ekler **Doğu ABD** bölge, iki tüketici grupları oluşturur (**cg1** ve **cg2**) hello Event Hub ile uyumlu uç nokta ve kullandığı hello **2016-02-03** API sürümü.</span><span class="sxs-lookup"><span data-stu-id="4c60f-126">This example adds hello IoT Hub in hello **East US** region, creates two consumer groups (**cg1** and **cg2**) on hello Event Hub-compatible endpoint, and uses hello **2016-02-03** API version.</span></span> <span data-ttu-id="4c60f-127">Bu şablon Ayrıca, toopass hello IOT hub adı adlı bir parametre olarak bekliyor **hubName**.</span><span class="sxs-lookup"><span data-stu-id="4c60f-127">This template also expects you toopass in hello IoT hub name as a parameter called **hubName**.</span></span> <span data-ttu-id="4c60f-128">Merhaba geçerli IOT hub'ı destekleyen konumların listesini için görmek [Azure durumu][lnk-status].</span><span class="sxs-lookup"><span data-stu-id="4c60f-128">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status].</span></span>

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
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg1')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
      },
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs/eventhubEndpoints/ConsumerGroups",
        "name": "[concat(parameters('hubName'), '/events/cg2')]",
        "dependsOn": [
          "[concat('Microsoft.Devices/Iothubs/', parameters('hubName'))]"
        ]
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

2. <span data-ttu-id="4c60f-129">Yerel makinenizde Hello Azure Resource Manager şablonu dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="4c60f-129">Save hello Azure Resource Manager template file on your local machine.</span></span> <span data-ttu-id="4c60f-130">Bu örnek kaydettiğiniz bu adlı bir klasöre varsayar **c:\templates**.</span><span class="sxs-lookup"><span data-stu-id="4c60f-130">This example assumes you save it in a folder called **c:\templates**.</span></span>

3. <span data-ttu-id="4c60f-131">Komut toodeploy aşağıdaki hello IOT hub'ınızı hello adını parametre olarak geçirme, yeni IOT hub ' ınızı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4c60f-131">Run hello following command toodeploy your new IoT hub, passing hello name of your IoT hub as a parameter.</span></span> <span data-ttu-id="4c60f-132">Bu örnekte, hello hello IOT hub'ı adıdır `abcmyiothub`.</span><span class="sxs-lookup"><span data-stu-id="4c60f-132">In this example, hello name of hello IoT hub is `abcmyiothub`.</span></span> <span data-ttu-id="4c60f-133">IOT hub'ınızı Hello adı genel olarak benzersiz olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="4c60f-133">hello name of your IoT hub must be globally unique:</span></span>

    ```powershell
    New-AzureRmResourceGroupDeployment -ResourceGroupName MyIoTRG1 -TemplateFile C:\templates\template.json -hubName abcmyiothub
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

4. <span data-ttu-id="4c60f-134">Merhaba çıktı hello tuşları oluşturduğunuz hello IOT hub'ı görüntüler.</span><span class="sxs-lookup"><span data-stu-id="4c60f-134">hello output displays hello keys for hello IoT hub you created.</span></span>

5. <span data-ttu-id="4c60f-135">Uygulamanızı eklenen tooverify hello yeni IOT hub'ı ziyaret edin hello [Azure portal] [ lnk-azure-portal] ve kaynakları listesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="4c60f-135">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="4c60f-136">Alternatif olarak, hello kullanın **Get-AzureRmResource** PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="4c60f-136">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="4c60f-137">Bu örnek uygulama S1 standart IOT için faturalandırılır hub'ı ekler.</span><span class="sxs-lookup"><span data-stu-id="4c60f-137">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="4c60f-138">Merhaba IOT hub'ı hello aracılığıyla silebilirsiniz [Azure portal] [ lnk-azure-portal] veya hello kullanarak **Kaldır AzureRmResource** bitirdiğinizde PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="4c60f-138">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c60f-139">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c60f-139">Next steps</span></span>

<span data-ttu-id="4c60f-140">PowerShell ile bir Azure Resource Manager şablonu kullanarak bir IOT hub dağıttığınız artık daha fazla tooexplore isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4c60f-140">Now you have deployed an IoT hub using an Azure Resource Manager template with PowerShell, you may want tooexplore further:</span></span>

* <span data-ttu-id="4c60f-141">Merhaba Hello özellikleri hakkında okuyun [IOT hub'ı kaynak sağlayıcısı REST API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="4c60f-141">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="4c60f-142">Okuma [Azure Resource Manager'a genel bakış] [ lnk-azure-rm-overview] toolearn hello özellikleri Azure Kaynak Yöneticisi'nin hakkında daha fazla.</span><span class="sxs-lookup"><span data-stu-id="4c60f-142">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="4c60f-143">IOT hub'ı geliştirme hakkında daha fazla toolearn makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="4c60f-143">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="4c60f-144">[Giriş tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="4c60f-144">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="4c60f-145">[Azure IOT SDK'ları][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="4c60f-145">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="4c60f-146">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="4c60f-146">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="4c60f-147">[Bir aygıt ile Azure IOT kenar benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="4c60f-147">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: /powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-powershell-arm]: ../azure-resource-manager/powershell-azure-resource-manager.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
