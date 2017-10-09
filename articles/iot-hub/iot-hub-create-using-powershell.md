---
title: aaaCreate PowerShell cmdlet'ini kullanarak Azure IOT Hub | Microsoft Docs
description: "Nasıl toouse PowerShell cmdlet toocreate IOT hub'ı."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 005cd8d48eb39d2e8b1bfb9ef84330d4aae4658f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-new-azurermiothub-cmdlet"></a><span data-ttu-id="1e58c-103">Merhaba yeni AzureRmIotHub cmdlet'ini kullanarak IOT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e58c-103">Create an IoT hub using hello New-AzureRmIotHub cmdlet</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

## <a name="introduction"></a><span data-ttu-id="1e58c-104">Giriş</span><span class="sxs-lookup"><span data-stu-id="1e58c-104">Introduction</span></span>

<span data-ttu-id="1e58c-105">Azure PowerShell cmdlet'leri toocreate kullanın ve Azure IOT hub'ları yönetin.</span><span class="sxs-lookup"><span data-stu-id="1e58c-105">You can use Azure PowerShell cmdlets toocreate and manage Azure IoT hubs.</span></span> <span data-ttu-id="1e58c-106">Bu öğretici şunların nasıl yapıldığını gösterir toocreate PowerShell ile bir IOT hub.</span><span class="sxs-lookup"><span data-stu-id="1e58c-106">This tutorial shows you how toocreate an IoT hub with PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="1e58c-107">Azure oluşturmak ve kaynaklarla çalışmak için iki farklı dağıtım modeli vardır: [Azure Resource Manager ve klasik](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="1e58c-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="1e58c-108">Bu makalede, hello Azure Resource Manager dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="1e58c-108">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="1e58c-109">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="1e58c-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="1e58c-110">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="1e58c-110">An active Azure account.</span></span> <br/><span data-ttu-id="1e58c-111">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e58c-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="1e58c-112">[Azure PowerShell cmdlet'leri][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="1e58c-112">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>

## <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="1e58c-113">Tooyour Azure aboneliğine bağlanma</span><span class="sxs-lookup"><span data-stu-id="1e58c-113">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="1e58c-114">PowerShell komut isteminde tooyour Azure aboneliği içindeki komut toosign aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="1e58c-114">In a PowerShell command prompt, enter hello following command toosign in tooyour Azure subscription:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="1e58c-115">Birden çok Azure aboneliğiniz varsa tooAzure imzalama tooall erişim verir kimlik bilgilerinizle ilişkili Azure abonelik hello.</span><span class="sxs-lookup"><span data-stu-id="1e58c-115">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="1e58c-116">Toouse toolist hello Azure abonelikleri kullanılabilir sizin için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="1e58c-116">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

```powershell
Get-AzureRMSubscription
```

<span data-ttu-id="1e58c-117">IOT hub'ınızı toocreate toouse toorun hello komutları istediğiniz komut tooselect abonelik aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e58c-117">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="1e58c-118">Merhaba hello önceki komutunun çıktısından hello abonelik adı veya kimliği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1e58c-118">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

```powershell
Select-AzureRMSubscription `
    -SubscriptionName "{your subscription name}"
```

## <a name="create-resource-group"></a><span data-ttu-id="1e58c-119">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e58c-119">Create resource group</span></span>

<span data-ttu-id="1e58c-120">Bir kaynak grubu toodeploy IOT hub'ı gerekir.</span><span class="sxs-lookup"><span data-stu-id="1e58c-120">You need a resource group toodeploy an IoT hub.</span></span> <span data-ttu-id="1e58c-121">Varolan bir kaynak grubunu kullanın veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1e58c-121">You can use an existing resource group or create a new one.</span></span>

<span data-ttu-id="1e58c-122">Aşağıdaki komut toodiscover hello konumlardan nerede IOT hub'ı dağıtabilirsiniz hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1e58c-122">You can use hello following command toodiscover hello locations where you can deploy an IoT hub:</span></span>

```powershell
((Get-AzureRmResourceProvider `
  -ProviderNamespace Microsoft.Devices).ResourceTypes `
  | Where-Object ResourceTypeName -eq IoTHubs).Locations
```

<span data-ttu-id="1e58c-123">toocreate IOT Hub, komutu aşağıdaki kullanım hello hello desteklenen konumlardan birinde IOT hub'ınız için bir kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="1e58c-123">toocreate a resource group for your IoT hub in one of hello supported locations for IoT Hub, use hello following command.</span></span> <span data-ttu-id="1e58c-124">Bu örnek adlı bir kaynak grubu oluşturur **MyIoTRG1** hello içinde **Doğu ABD** bölge:</span><span class="sxs-lookup"><span data-stu-id="1e58c-124">This example creates a resource group called **MyIoTRG1** in hello **East US** region:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyIoTRG1 -Location "East US"
```

## <a name="create-an-iot-hub"></a><span data-ttu-id="1e58c-125">IoT hub oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e58c-125">Create an IoT hub</span></span>

<span data-ttu-id="1e58c-126">toocreate hello kaynak grubunda hello önceki adımda, komutu aşağıdaki kullanım hello oluşturduğunuz IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="1e58c-126">toocreate an IoT hub in hello resource group you created in hello previous step, use hello following command.</span></span> <span data-ttu-id="1e58c-127">Bu örnekte bir **S1** adlı hub **MyTestIoTHub** hello içinde **Doğu ABD** bölge:</span><span class="sxs-lookup"><span data-stu-id="1e58c-127">This example creates an **S1** hub called **MyTestIoTHub** in hello **East US** region:</span></span>

```powershell
New-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub `
    -SkuName S1 -Units 1 `
    -Location "East US"
```

<span data-ttu-id="1e58c-128">hello IOT hub'Hello adı benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e58c-128">hello name of hello IoT hub must be unique.</span></span>

[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]


<span data-ttu-id="1e58c-129">Aboneliğinizi komutu aşağıdaki hello kullanarak tüm hello IOT hub'ları listeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1e58c-129">You can list all hello IoT hubs in your subscription using hello following command:</span></span>

```powershell
Get-AzureRmIotHub
```

<span data-ttu-id="1e58c-130">Merhaba önceki örnek S1 standart IOT için faturalandırılır hub'ı ekler.</span><span class="sxs-lookup"><span data-stu-id="1e58c-130">hello previous example adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="1e58c-131">Merhaba IOT hub'ı komut aşağıdaki hello kullanarak silebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1e58c-131">You can delete hello IoT hub using hello following command:</span></span>

```powershell
Remove-AzureRmIotHub `
    -ResourceGroupName MyIoTRG1 `
    -Name MyTestIoTHub
```

<span data-ttu-id="1e58c-132">Alternatif olarak, bir kaynak grubu kaldırabilir ve tüm komut aşağıdaki hello kullanarak içerdiği kaynakların hello:</span><span class="sxs-lookup"><span data-stu-id="1e58c-132">Alternatively, you can remove a resource group and all hello resources it contains using hello following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name MyIoTRG1
```

## <a name="next-steps"></a><span data-ttu-id="1e58c-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e58c-133">Next steps</span></span>

<span data-ttu-id="1e58c-134">PowerShell cmdlet'ini kullanarak bir IOT hub dağıttığınız artık daha fazla tooexplore isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="1e58c-134">Now you have deployed an IoT hub using a PowerShell cmdlet, you may want tooexplore further:</span></span>

* <span data-ttu-id="1e58c-135">Diğer Bul [IOT hub ile çalışmak için PowerShell cmdlet'leri][lnk-iothub-cmdlets].</span><span class="sxs-lookup"><span data-stu-id="1e58c-135">Discover other [PowerShell cmdlets for working with your IoT hub][lnk-iothub-cmdlets].</span></span>
* <span data-ttu-id="1e58c-136">Merhaba Hello özellikleri hakkında okuyun [IOT hub'ı kaynak sağlayıcısı REST API][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="1e58c-136">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>

<span data-ttu-id="1e58c-137">IOT hub'ı geliştirme hakkında daha fazla toolearn makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="1e58c-137">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="1e58c-138">[Giriş tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="1e58c-138">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="1e58c-139">[Azure IOT SDK'ları][lnk-sdks]</span><span class="sxs-lookup"><span data-stu-id="1e58c-139">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="1e58c-140">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="1e58c-140">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="1e58c-141">[Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="1e58c-141">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-iothub-cmdlets]: https://docs.microsoft.com/powershell/module/azurerm.iothub/
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
