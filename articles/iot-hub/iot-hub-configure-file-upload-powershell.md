---
title: "aaaUse hello Azure PowerShell tooconfigure karşıya dosya yükleme | Microsoft Docs"
description: "Nasıl toouse hello Azure PowerShell cmdlet'leri tooconfigure bağlı aygıtlardan IOT hub tooenable dosyanızı karşıya yükleme. Merhaba hedef Azure depolama hesabı yapılandırma hakkında bilgi içerir."
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
ms.openlocfilehash: 9dcdc41693c09cece411921b30c91d7b3db47395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-powershell"></a><span data-ttu-id="c4d31-104">IOT Hub'ın PowerShell kullanarak dosya yüklemeleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="c4d31-104">Configure IoT Hub file uploads using PowerShell</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="c4d31-105">toouse hello [dosya karşıya yükleme işlevselliği IOT hub'da][lnk-upload], IOT hub'ınıza ilk Azure storage hesabı ilişkilendirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="c4d31-105">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure storage account with your IoT hub.</span></span> <span data-ttu-id="c4d31-106">Mevcut bir depolama hesabını kullanma veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c4d31-106">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="c4d31-107">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="c4d31-107">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="c4d31-108">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="c4d31-108">An active Azure account.</span></span> <span data-ttu-id="c4d31-109">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4d31-109">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="c4d31-110">[Azure PowerShell cmdlet'leri][lnk-powershell-install].</span><span class="sxs-lookup"><span data-stu-id="c4d31-110">[Azure PowerShell cmdlets][lnk-powershell-install].</span></span>
* <span data-ttu-id="c4d31-111">Azure IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="c4d31-111">An Azure IoT hub.</span></span> <span data-ttu-id="c4d31-112">IOT hub'ı yoksa, hello kullanabilirsiniz [yeni AzureRmIoTHub cmdlet] [ lnk-powershell-iothub] toocreate bir ya da kullanım hello portal çok[IOT hub oluşturma] [ lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="c4d31-112">If you don't have an IoT hub, you can use hello [New-AzureRmIoTHub cmdlet][lnk-powershell-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="c4d31-113">Bir Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="c4d31-113">An Azure storage account.</span></span> <span data-ttu-id="c4d31-114">Bir Azure depolama hesabınız yoksa, hello kullanabilirsiniz [Azure Storage PowerShell cmdlet'lerini] [ lnk-powershell-storage] toocreate bir ya da kullanım hello portal çok[depolama hesabı oluşturma] [ lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="c4d31-114">If you don't have an Azure storage account, you can use hello [Azure Storage PowerShell cmdlets][lnk-powershell-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="c4d31-115">Oturum açma ve Azure hesabınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="c4d31-115">Sign in and set your Azure account</span></span>

<span data-ttu-id="c4d31-116">Tooyour Azure hesabı oturum ve aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="c4d31-116">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="c4d31-117">Merhaba Hello PowerShell isteminde çalıştırın **Login-AzureRmAccount** cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c4d31-117">At hello PowerShell prompt, run hello **Login-AzureRmAccount** cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

1. <span data-ttu-id="c4d31-118">Birden çok Azure aboneliğiniz varsa tooAzure imzalama tooall erişim verir kimlik bilgilerinizle ilişkili Azure abonelik hello.</span><span class="sxs-lookup"><span data-stu-id="c4d31-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure subscriptions associated with your credentials.</span></span> <span data-ttu-id="c4d31-119">Toouse toolist hello Azure abonelikleri kullanılabilir sizin için komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="c4d31-119">Use hello following command toolist hello Azure subscriptions available for you toouse:</span></span>

    ```powershell
    Get-AzureRMSubscription
    ```

    <span data-ttu-id="c4d31-120">IOT hub'ınızı toomanage toouse toorun hello komutları istediğiniz komut tooselect abonelik aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4d31-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toomanage your IoT hub.</span></span> <span data-ttu-id="c4d31-121">Merhaba hello önceki komutunun çıktısından hello abonelik adı veya kimliği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c4d31-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```powershell
    Select-AzureRMSubscription `
        -SubscriptionName "{your subscription name}"
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="c4d31-122">Depolama hesabı ayrıntıları alma</span><span class="sxs-lookup"><span data-stu-id="c4d31-122">Retrieve your storage account details</span></span>

<span data-ttu-id="c4d31-123">Merhaba aşağıdaki adımlarda hello kullanarak depolama hesabınıza oluşturulan varsayılmaktadır **Resource Manager** dağıtım modeli ve değil hello **Klasik** dağıtım modeli.</span><span class="sxs-lookup"><span data-stu-id="c4d31-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="c4d31-124">cihazlarınızın tooconfigure dosya yüklemeleri, hello bağlantı dizesi için bir Azure depolama hesabı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="c4d31-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="c4d31-125">Merhaba depolama hesabı hello olmalıdır IOT hub'ınızı aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="c4d31-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="c4d31-126">Merhaba depolama hesabındaki bir blob kapsayıcısını hello adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4d31-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="c4d31-127">Komut tooretrieve aşağıdaki hello depolama hesabı anahtarları kullanın:</span><span class="sxs-lookup"><span data-stu-id="c4d31-127">Use hello following command tooretrieve your storage account keys:</span></span>

```powershell
Get-AzureRmStorageAccountKey `
  -Name {your storage account name} `
  -ResourceGroupName {your storage account resource group}
```

<span data-ttu-id="c4d31-128">Merhaba Not **key1** depolama hesabı anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="c4d31-128">Make a note of hello **key1** storage account key value.</span></span> <span data-ttu-id="c4d31-129">Aşağıdaki adımları hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="c4d31-129">You need it in hello following steps.</span></span>

<span data-ttu-id="c4d31-130">Var olan bir blob kapsayıcı, dosya yüklemeleri için kullanabilir veya yeni bir tane oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c4d31-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="c4d31-131">toolist hello mevcut blob kapsayıcıları depolama hesabınızdaki hello aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="c4d31-131">toolist hello existing blob containers in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    Get-AzureStorageContainer -Context $ctx
    ```

* <span data-ttu-id="c4d31-132">Depolama hesabınız, aşağıdaki komutları kullanın hello blob kapsayıcısında toocreate:</span><span class="sxs-lookup"><span data-stu-id="c4d31-132">toocreate a blob container in your storage account, use hello following commands:</span></span>

    ```powershell
    $ctx = New-AzureStorageContext `
        -StorageAccountName {your storage account name} `
        -StorageAccountKey {your storage account key}
    New-AzureStorageContainer `
        -Name {your new container name} `
        -Permission Off `
        -Context $ctx
    ```

## <a name="configure-your-iot-hub"></a><span data-ttu-id="c4d31-133">IOT hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c4d31-133">Configure your IoT hub</span></span>

<span data-ttu-id="c4d31-134">Artık IOT hub tooenable yapılandırabilirsiniz [dosya karşıya yükleme işlevselliği] [ lnk-upload] depolama hesabı bilgilerinizi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c4d31-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="c4d31-135">Merhaba yapılandırma değerlerini aşağıdaki hello gerektirir:</span><span class="sxs-lookup"><span data-stu-id="c4d31-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="c4d31-136">**Depolama kapsayıcısı**: geçerli, Azure aboneliği tooassociate IOT hub'ınızı ile Azure depolama hesabında blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="c4d31-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="c4d31-137">Önceki bölümde hello hello gerekli depolama hesabı bilgileri alınamadı.</span><span class="sxs-lookup"><span data-stu-id="c4d31-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="c4d31-138">Dosyaları karşıya yüklediğinizde IOT Hub cihazları toouse için yazma izinleri toothis blob kapsayıcısı ile SAS URI'ler otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c4d31-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="c4d31-139">**Karşıya yüklenen dosyalar için bildirimlerin**: etkinleştirmek veya dosya karşıya yükleme bildirimlerini devre dışı.</span><span class="sxs-lookup"><span data-stu-id="c4d31-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="c4d31-140">**SAS TTL**: hello zaman yaşam SAS URI'ler toohello cihaz IOT Hub tarafından döndürülen Merhaba, bu bir ayardır.</span><span class="sxs-lookup"><span data-stu-id="c4d31-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="c4d31-141">Tooone saat, varsayılan olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c4d31-141">Set tooone hour by default.</span></span>

<span data-ttu-id="c4d31-142">**Dosya bildirim ayarları varsayılan TTL**: hello zaman süresi doldu önce dosya karşıya yükleme bildirimi yaşam.</span><span class="sxs-lookup"><span data-stu-id="c4d31-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="c4d31-143">Tooone günü varsayılan olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c4d31-143">Set tooone day by default.</span></span>

<span data-ttu-id="c4d31-144">**Dosya bildirim maksimum teslimat sayısı**: hello sayısı zaman hello IOT hub'ı denemeleri toodeliver dosya karşıya yükleme bildirimi.</span><span class="sxs-lookup"><span data-stu-id="c4d31-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="c4d31-145">Too10 varsayılan olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c4d31-145">Set too10 by default.</span></span>

<span data-ttu-id="c4d31-146">PowerShell cmdlet tooconfigure hello dosya karşıya yükleme ayarları, IOT hub'ına aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="c4d31-146">Use hello following PowerShell cmdlet tooconfigure hello file upload settings on your IoT hub:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c4d31-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c4d31-147">Next steps</span></span>

<span data-ttu-id="c4d31-148">IOT hub'ı hello dosya karşıya yükleme özellikleri hakkında daha fazla bilgi için bkz: [karşıya bir aygıtı dosyalarından][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="c4d31-148">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="c4d31-149">Azure IOT hub'ı yönetme hakkında daha fazla bu bağlantılar toolearn izleyin:</span><span class="sxs-lookup"><span data-stu-id="c4d31-149">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="c4d31-150">[Toplu IOT cihazları yönetme][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="c4d31-150">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="c4d31-151">[IOT hub'ı ölçümleri][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="c4d31-151">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="c4d31-152">[İzleme işlemleri][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="c4d31-152">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="c4d31-153">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="c4d31-153">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="c4d31-154">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="c4d31-154">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="c4d31-155">[Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="c4d31-155">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="c4d31-156">[IOT çözümünüzden plan hello güvenli][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="c4d31-156">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

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