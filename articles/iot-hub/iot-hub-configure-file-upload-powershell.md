---
title: "Karşıya dosya yükleme yapılandırmak için Azure PowerShell kullanın | Microsoft Docs"
description: "Azure PowerShell cmdlet'lerini dosya etkinleştirmek için IOT hub'ınızı yapılandırma için nasıl kullanılacağını bağlı aygıtlardan yükler. Hedef Azure depolama hesabı yapılandırma hakkında bilgi içerir."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 915f1597-272d-4fd4-8c5b-a0ccb1df0d91
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: a72bda794b2da3e044c46249559610d06b1f1843
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="a7f3e-104">IOT Hub'ın PowerShell kullanarak dosya yüklemeleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="a7f3e-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="a7f3e-105">Kullanılacak [dosya karşıya yükleme işlevselliği IOT hub'da][lnk-upload], IOT hub'ınıza ilk Azure storage hesabı ilişkilendirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-105">To use the [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="a7f3e-106">Mevcut bir depolama hesabını kullanma veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="a7f3e-107">Bu öğreticiyi tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="a7f3e-107">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="a7f3e-108">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-108">An active Azure account.</span></span> <span data-ttu-id="a7f3e-109">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="a7f3e-110">[Azure PowerShell cmdlet'leri][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="a7f3e-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="a7f3e-111">Azure IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-111">An Azure IoT hub.</span></span> <span data-ttu-id="a7f3e-112">IOT hub'ı yoksa, kullanabileceğiniz [yeni AzureRmIoTHub cmdlet] [ lnk-powershell-iothub] oluşturun veya portalını kullanarak [IOT hub oluşturma][lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="a7f3e-112">If you don't have an IoT hub, you can use the [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] to create one or use the portal to [Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="a7f3e-113">Bir Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-113">An Azure storage account.</span></span> <span data-ttu-id="a7f3e-114">Bir Azure depolama hesabınız yoksa, kullanabileceğiniz [Azure Storage PowerShell cmdlet'lerini] [ lnk-powershell-storage] oluşturun veya portalını kullanarak [depolama hesabı oluşturma] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="a7f3e-114">If you don't have an Azure storage account, you can use the [Azure Storage PowerShell cmdlets][lnk-powershell-storage] to create one or use the portal to [Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="a7f3e-115">Oturum açma ve Azure hesabınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="a7f3e-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="a7f3e-116">Azure hesabınızda oturum açın ve aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-116">Sign in to your Azure account and select your subscription.</span></span>

1. <span data-ttu-id="a7f3e-117">PowerShell komut isteminde çalıştırmak **Login-AzureRmAccount** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a7f3e-117">At the PowerShell prompt, run the **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="a7f3e-118">Birden çok Azure aboneliğiniz varsa, Azure'da oturum açma kimlik bilgileriyle ilişkili tüm Azure abonelikleri için size erişim verir.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-118">If you have multiple Azure subscriptions, signing in to Azure grants you access to all the Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="a7f3e-119">Azure aboneliklerini kullanabilmeniz için kullanılabilir listelemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="a7f3e-119">Use the following command to list the Azure subscriptions available for you to use:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="a7f3e-120">IOT hub'ınızı yönetmek için komutları çalıştırmak için kullanmak istediğiniz aboneliği seçmek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-120">Use the following command to select subscription that you want to use to run the commands to manage your IoT hub.</span></span> <span data-ttu-id="a7f3e-121">Önceki komut çıktısı abonelik adı veya kimliği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a7f3e-121">You can use either the subscription name or ID from the output of the previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="a7f3e-122">Depolama hesabı ayrıntıları alma</span><span class="sxs-lookup"><span data-stu-id="a7f3e-122">Retrieve your storage account details</span></span>

<span data-ttu-id="a7f3e-123">Aşağıdaki adımlarda, depolama hesabı kullanılarak oluşturulan varsayılmaktadır **Resource Manager** dağıtım modeli ve **Klasik** dağıtım modeli.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-123">The following steps assume that you created your storage account using the **Resource Manager** deployment model, and not the **Classic** deployment model.</span></span>

<span data-ttu-id="a7f3e-124">Aygıtlarınızı dosya yüklemelerini yapılandırmak için bağlantı dizesi için bir Azure depolama hesabı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-124">To configure file uploads from your devices, you need the connection string for an Azure storage account.</span></span> <span data-ttu-id="a7f3e-125">Depolama hesabı, IOT hub'ınızı ile aynı abonelikte olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-125">The storage account must be in the same subscription as your IoT hub.</span></span> <span data-ttu-id="a7f3e-126">Depolama hesabındaki blob kapsayıcısının adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-126">You also need the name of a blob container in the storage account.</span></span> <span data-ttu-id="a7f3e-127">Depolama hesabı anahtarlarını almak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="a7f3e-127">Use the following command to retrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="a7f3e-128">Not **key1** depolama hesabı anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-128">Make a note of the **key1** storage account key value.</span></span> <span data-ttu-id="a7f3e-129">Bunu aşağıdaki adımlarda gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-129">You need it in the following steps.</span></span>

<span data-ttu-id="a7f3e-130">Var olan bir blob kapsayıcı, dosya yüklemeleri için kullanabilir veya yeni bir tane oluşturun:</span><span class="sxs-lookup"><span data-stu-id="a7f3e-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="a7f3e-131">Depolama hesabınızdaki mevcut blob kapsayıcıları listelemek için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="a7f3e-131">To list the existing blob containers in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="a7f3e-132">Depolama hesabınızda blob kapsayıcısı oluşturmak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="a7f3e-132">To create a blob container in your storage account, use the following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="a7f3e-133">IOT hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="a7f3e-133">Configure your IoT hub</span></span>

<span data-ttu-id="a7f3e-134">Şimdi etkinleştirmek için IOT hub'ınızı yapılandırma [dosya karşıya yükleme işlevselliği] [ lnk-upload] depolama hesabı bilgilerinizi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-134">You can now configure your IoT hub to enable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="a7f3e-135">Aşağıdaki değerleri yapılandırmasını gerektirir:</span><span class="sxs-lookup"><span data-stu-id="a7f3e-135">The configuration requires the following values:</span></span>

<span data-ttu-id="a7f3e-136">**Depolama kapsayıcısı**: IOT hub ile ilişkilendirmek için geçerli Azure aboneliğinizde bir Azure depolama hesabındaki blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription to associate with your IoT hub.</span></span> <span data-ttu-id="a7f3e-137">Önceki bölümde gerekli depolama hesabı bilgilerini aldı.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-137">You retrieved the necessary storage account information in the preceding section.</span></span> <span data-ttu-id="a7f3e-138">IOT hub'ı SAS URI'ler dosyaları karşıya yükleme sırasında kullanmak cihazlar için bu blob kapsayıcısına yazma izinlerine sahip otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-138">IoT Hub automatically generates SAS URIs with write permissions to this blob container for devices to use when they upload files.</span></span>

<span data-ttu-id="a7f3e-139">**Karşıya yüklenen dosyalar için bildirimlerin**: etkinleştirmek veya dosya karşıya yükleme bildirimlerini devre dışı.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="a7f3e-140">**SAS TTL**: saat yaşam IOT Hub tarafından cihaza döndürülen SAS URI, bu ayar değildir.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-140">**SAS TTL**: This setting is the time-to-live of the SAS URIs returned to the device by IoT Hub.</span></span> <span data-ttu-id="a7f3e-141">Bir saat için varsayılan olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-141">Set to one hour by default.</span></span>

<span data-ttu-id="a7f3e-142">**Dosya bildirim ayarları varsayılan TTL**: süresi doldu önce bildirim zaman yaşam dosyasının karşıya.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-142">**File notification settings default TTL**: The time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="a7f3e-143">Bir gün için varsayılan olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-143">Set to one day by default.</span></span>

<span data-ttu-id="a7f3e-144">**Dosya bildirim maksimum teslimat sayısı**: IOT hub'ı bir dosya teslim etmek için kaç deneme sayısı bildirim karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-144">**File notification maximum delivery count**: The number of times the IoT Hub attempts to deliver a file upload notification.</span></span> <span data-ttu-id="a7f3e-145">Varsayılan olarak 10 olarak ayarlandı.</span><span class="sxs-lookup"><span data-stu-id="a7f3e-145">Set to 10 by default.</span></span>

<span data-ttu-id="a7f3e-146">Dosya yapılandırmak için aşağıdaki PowerShell cmdlet'ini IOT hub'ınızı ayarlarını karşıya yükle:</span><span class="sxs-lookup"><span data-stu-id="a7f3e-146">Use the following PowerShell cmdlet to configure the file upload settings on your IoT hub:</span></span>

```powershell
Set-AzureRmIotHub `
    -ResourceGroupName "{your iot hub resource group}" `
    -Name "{your iot hub name}" `
    -FileUploadNotificationTtl "01:00:00" `
    -FileUploadSasUriTtl "01:00:00" `
    -EnableFileUploadNotifications $true `
    -FileUploadStorageConnectionString "DefaultEndpointsProtocol=https;AccountName={your storage account name};AccountKey={your storage account key};EndpointSuffix=core.windows.net" `
    -FileUploadContainerName "{your blob container name}" `
    -FileUploadNotificationMaxDeliveryCount 10
```

## <a name="next-steps"></a><span data-ttu-id="a7f3e-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7f3e-147">Next steps</span></span>

<span data-ttu-id="a7f3e-148">IOT hub'ı dosya karşıya yükleme özellikleri hakkında daha fazla bilgi için bkz: [karşıya bir aygıtı dosyalarından][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="a7f3e-148">For more information about the file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="a7f3e-149">Azure IOT hub'ı yönetme hakkında daha fazla bilgi için bu bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="a7f3e-149">Follow these links to learn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="a7f3e-150">[Toplu IOT cihazları yönetme][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="a7f3e-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="a7f3e-151">[IOT hub'ı ölçümleri][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="a7f3e-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="a7f3e-152">[İzleme işlemleri][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="a7f3e-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="a7f3e-153">Daha fazla IOT hub'ı özelliklerini keşfetmek için bkz:</span><span class="sxs-lookup"><span data-stu-id="a7f3e-153">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="a7f3e-154">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="a7f3e-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="a7f3e-155">[Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="a7f3e-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="a7f3e-156">[IOT çözümünüzden zemin oluşturan güvenli][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="a7f3e-156">[Secure your IoT solution from the ground up][lnk-securing]</span></span>

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-powershell-storage]: https://docs.microsoft.com/powershell/module/azurerm.storage/
[lnk-powershell-iothub]: https://docs.microsoft.com/powershell/module/azurerm.iothub/new-azurermiothub
[lnk-portal-hub]: iot-hub-create-through-portal.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md