---
title: "aaaConfigure dosya karşıya yükleme tooIoT Azure CLI (az.py) kullanarak Hub | Microsoft Docs"
description: "Nasıl tooconfigure fileuploads tooAzure IOT hub'ı kullanarak platformlar arası Azure CLI 2.0 (az.py) hello."
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
ms.openlocfilehash: 390113df2d96df9833b6aa383ed66805528614a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-iot-hub-file-uploads-using-azure-cli"></a><span data-ttu-id="f4038-103">IOT Hub'ın Azure CLI kullanarak dosya yüklemeleri yapılandırın</span><span class="sxs-lookup"><span data-stu-id="f4038-103">Configure IoT Hub file uploads using Azure CLI</span></span>

[!INCLUDE [iot-hub-file-upload-selector](../../includes/iot-hub-file-upload-selector.md)]

<span data-ttu-id="f4038-104">toouse hello [dosya karşıya yükleme işlevselliği IOT hub'da][lnk-upload], bir Azure Storage hesabı IOT hub'ınıza ilk ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4038-104">toouse hello [file upload functionality in IoT Hub][lnk-upload], you must first associate an Azure Storage account with your IoT hub.</span></span> <span data-ttu-id="f4038-105">Mevcut bir depolama hesabını kullanma veya yeni bir tane oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f4038-105">You can use an existing storage account or create a new one.</span></span>

<span data-ttu-id="f4038-106">toocomplete Bu öğretici, aşağıdaki hello gerekir:</span><span class="sxs-lookup"><span data-stu-id="f4038-106">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="f4038-107">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="f4038-107">An active Azure account.</span></span> <span data-ttu-id="f4038-108">Hesabınız yoksa, yalnızca birkaç dakika içinde [ücretsiz bir hesap][lnk-free-trial] oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f4038-108">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="f4038-109">[Azure CLI 2.0][lnk-CLI-install].</span><span class="sxs-lookup"><span data-stu-id="f4038-109">[Azure CLI 2.0][lnk-CLI-install].</span></span>
* <span data-ttu-id="f4038-110">Azure IOT hub'ı.</span><span class="sxs-lookup"><span data-stu-id="f4038-110">An Azure IoT hub.</span></span> <span data-ttu-id="f4038-111">IOT hub'ı yoksa, hello kullanabilirsiniz `az iot hub create` [komutu] [ lnk-cli-create-iothub] toocreate bir ya da kullanım hello portal çok [IOT hub'ı Oluştur] [lnk-portal-hub].</span><span class="sxs-lookup"><span data-stu-id="f4038-111">If you don't have an IoT hub, you can use hello `az iot hub create` [command][lnk-cli-create-iothub] toocreate one or use hello portal too[Create an IoT hub][lnk-portal-hub].</span></span>
* <span data-ttu-id="f4038-112">Bir Azure depolama hesabı.</span><span class="sxs-lookup"><span data-stu-id="f4038-112">An Azure Storage account.</span></span> <span data-ttu-id="f4038-113">Bir Azure depolama hesabınız yoksa, hello kullanabilirsiniz [Azure CLI 2.0 - depolama hesaplarını yönetme] [ lnk-manage-storage] toocreate bir ya da kullanım hello portal çok[depolama hesabı oluşturma] [lnk-portal-storage].</span><span class="sxs-lookup"><span data-stu-id="f4038-113">If you don't have an Azure Storage account, you can use hello [Azure CLI 2.0 - Manage storage accounts][lnk-manage-storage] toocreate one or use hello portal too[Create a storage account][lnk-portal-storage].</span></span>

## <a name="sign-in-and-set-your-azure-account"></a><span data-ttu-id="f4038-114">Oturum açma ve Azure hesabınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="f4038-114">Sign in and set your Azure account</span></span>

<span data-ttu-id="f4038-115">Tooyour Azure hesabı oturum ve aboneliğinizi seçin.</span><span class="sxs-lookup"><span data-stu-id="f4038-115">Sign in tooyour Azure account and select your subscription.</span></span>

1. <span data-ttu-id="f4038-116">Merhaba Hello komut isteminde çalıştırmak [oturum açma komut][lnk-login-command]:</span><span class="sxs-lookup"><span data-stu-id="f4038-116">At hello command prompt, run hello [login command][lnk-login-command]:</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="f4038-117">Merhaba yönergeleri tooauthenticate Hello kod kullanarak izleyin ve oturum açma tooyour bir web tarayıcısı aracılığıyla Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="f4038-117">Follow hello instructions tooauthenticate using hello code and sign in tooyour Azure account through a web browser.</span></span>

1. <span data-ttu-id="f4038-118">Birden çok Azure aboneliğiniz varsa tooAzure imzalama tooall erişim verir kimlik bilgilerinizle ilişkili Azure hesapları hello.</span><span class="sxs-lookup"><span data-stu-id="f4038-118">If you have multiple Azure subscriptions, signing in tooAzure grants you access tooall hello Azure accounts associated with your credentials.</span></span> <span data-ttu-id="f4038-119">Merhaba aşağıdaki kullanın [komutu toolist hello Azure hesapları] [ lnk-az-account-command] , toouse için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="f4038-119">Use hello following [command toolist hello Azure accounts][lnk-az-account-command] available for you toouse:</span></span>

    ```azurecli
    az account list
    ```

    <span data-ttu-id="f4038-120">IOT hub'ınızı toocreate toouse toorun hello komutları istediğiniz komut tooselect abonelik aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="f4038-120">Use hello following command tooselect subscription that you want toouse toorun hello commands toocreate your IoT hub.</span></span> <span data-ttu-id="f4038-121">Merhaba hello önceki komutunun çıktısından hello abonelik adı veya kimliği kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f4038-121">You can use either hello subscription name or ID from hello output of hello previous command:</span></span>

    ```azurecli
    az account set --subscription {your subscription name or id}
    ```

## <a name="retrieve-your-storage-account-details"></a><span data-ttu-id="f4038-122">Depolama hesabı ayrıntıları alma</span><span class="sxs-lookup"><span data-stu-id="f4038-122">Retrieve your storage account details</span></span>

<span data-ttu-id="f4038-123">Merhaba aşağıdaki adımlarda hello kullanarak depolama hesabınıza oluşturulan varsayılmaktadır **Resource Manager** dağıtım modeli ve değil hello **Klasik** dağıtım modeli.</span><span class="sxs-lookup"><span data-stu-id="f4038-123">hello following steps assume that you created your storage account using hello **Resource Manager** deployment model, and not hello **Classic** deployment model.</span></span>

<span data-ttu-id="f4038-124">cihazlarınızın tooconfigure dosya yüklemeleri, hello bağlantı dizesi için bir Azure depolama hesabı gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="f4038-124">tooconfigure file uploads from your devices, you need hello connection string for an Azure storage account.</span></span> <span data-ttu-id="f4038-125">Merhaba depolama hesabı hello olmalıdır IOT hub'ınızı aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="f4038-125">hello storage account must be in hello same subscription as your IoT hub.</span></span> <span data-ttu-id="f4038-126">Merhaba depolama hesabındaki bir blob kapsayıcısını hello adı da gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4038-126">You also need hello name of a blob container in hello storage account.</span></span> <span data-ttu-id="f4038-127">Komut tooretrieve aşağıdaki hello depolama hesabı anahtarları kullanın:</span><span class="sxs-lookup"><span data-stu-id="f4038-127">Use hello following command tooretrieve your storage account keys:</span></span>

```azurecli
az storage account show-connection-string --name {your storage account name} --resource-group {your storage account resource group}
```

<span data-ttu-id="f4038-128">Merhaba Not **connectionString** değeri.</span><span class="sxs-lookup"><span data-stu-id="f4038-128">Make a note of hello **connectionString** value.</span></span> <span data-ttu-id="f4038-129">Aşağıdaki adımları hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="f4038-129">You need it in hello following steps.</span></span>

<span data-ttu-id="f4038-130">Var olan bir blob kapsayıcı, dosya yüklemeleri için kullanabilir veya yeni bir tane oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f4038-130">You can either use an existing blob container for your file uploads or create new one:</span></span>

* <span data-ttu-id="f4038-131">toolist hello mevcut blob kapsayıcıları depolama hesabınızdaki hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f4038-131">toolist hello existing blob containers in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container list --connection-string "{your storage account connection string}"
    ```

* <span data-ttu-id="f4038-132">Depolama hesabınız, komutu aşağıdaki kullanım hello blob kapsayıcısında toocreate:</span><span class="sxs-lookup"><span data-stu-id="f4038-132">toocreate a blob container in your storage account, use hello following command:</span></span>

    ```azurecli
    az storage container create --name {container name} --connection-string "{your storage account connection string}"
    ```

## <a name="file-upload"></a><span data-ttu-id="f4038-133">Karşıya dosya yükleme</span><span class="sxs-lookup"><span data-stu-id="f4038-133">File upload</span></span>

<span data-ttu-id="f4038-134">Artık IOT hub tooenable yapılandırabilirsiniz [dosya karşıya yükleme işlevselliği] [ lnk-upload] depolama hesabı bilgilerinizi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f4038-134">You can now configure your IoT hub tooenable [file upload functionality][lnk-upload] using your storage account details.</span></span>

<span data-ttu-id="f4038-135">Merhaba yapılandırma değerlerini aşağıdaki hello gerektirir:</span><span class="sxs-lookup"><span data-stu-id="f4038-135">hello configuration requires hello following values:</span></span>

<span data-ttu-id="f4038-136">**Depolama kapsayıcısı**: geçerli, Azure aboneliği tooassociate IOT hub'ınızı ile Azure depolama hesabında blob kapsayıcısı.</span><span class="sxs-lookup"><span data-stu-id="f4038-136">**Storage container**: A blob container in an Azure storage account in your current Azure subscription tooassociate with your IoT hub.</span></span> <span data-ttu-id="f4038-137">Önceki bölümde hello hello gerekli depolama hesabı bilgileri alınamadı.</span><span class="sxs-lookup"><span data-stu-id="f4038-137">You retrieved hello necessary storage account information in hello preceding section.</span></span> <span data-ttu-id="f4038-138">Dosyaları karşıya yüklediğinizde IOT Hub cihazları toouse için yazma izinleri toothis blob kapsayıcısı ile SAS URI'ler otomatik olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f4038-138">IoT Hub automatically generates SAS URIs with write permissions toothis blob container for devices toouse when they upload files.</span></span>

<span data-ttu-id="f4038-139">**Karşıya yüklenen dosyalar için bildirimlerin**: etkinleştirmek veya dosya karşıya yükleme bildirimlerini devre dışı.</span><span class="sxs-lookup"><span data-stu-id="f4038-139">**Receive notifications for uploaded files**: Enable or disable file upload notifications.</span></span>

<span data-ttu-id="f4038-140">**SAS TTL**: hello zaman yaşam SAS URI'ler toohello cihaz IOT Hub tarafından döndürülen Merhaba, bu bir ayardır.</span><span class="sxs-lookup"><span data-stu-id="f4038-140">**SAS TTL**: This setting is hello time-to-live of hello SAS URIs returned toohello device by IoT Hub.</span></span> <span data-ttu-id="f4038-141">Tooone saat, varsayılan olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f4038-141">Set tooone hour by default.</span></span>

<span data-ttu-id="f4038-142">**Dosya bildirim ayarları varsayılan TTL**: hello zaman süresi doldu önce dosya karşıya yükleme bildirimi yaşam.</span><span class="sxs-lookup"><span data-stu-id="f4038-142">**File notification settings default TTL**: hello time-to-live of a file upload notification before it is expired.</span></span> <span data-ttu-id="f4038-143">Tooone günü varsayılan olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f4038-143">Set tooone day by default.</span></span>

<span data-ttu-id="f4038-144">**Dosya bildirim maksimum teslimat sayısı**: hello sayısı zaman hello IOT hub'ı denemeleri toodeliver dosya karşıya yükleme bildirimi.</span><span class="sxs-lookup"><span data-stu-id="f4038-144">**File notification maximum delivery count**: hello number of times hello IoT Hub attempts toodeliver a file upload notification.</span></span> <span data-ttu-id="f4038-145">Too10 varsayılan olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f4038-145">Set too10 by default.</span></span>

<span data-ttu-id="f4038-146">Azure CLI komutları tooconfigure hello dosya karşıya yükleme ayarları, IOT hub'ına aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="f4038-146">Use hello following Azure CLI commands tooconfigure hello file upload settings on your IoT hub:</span></span>

<span data-ttu-id="f4038-147">Bir bash Kabuğu'nu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f4038-147">In a bash shell use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.connectionString="{your storage account connection string}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.containerName="{your storage container name}"
az iot hub update --name {your iot hub name} --set properties.storageEndpoints.'$default'.sasTtlAsIso8601=PT1H0M0S

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="f4038-148">Windows komut istemi kullanın:</span><span class="sxs-lookup"><span data-stu-id="f4038-148">At a Windows command prompt use:</span></span>

```azurecli
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.connectionString="{your storage account connection string}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.containerName="{your storage container name}""
az iot hub update --name {your iot hub name} --set "properties.storageEndpoints.$default.sasTtlAsIso8601=PT1H0M0S"

az iot hub update --name {your iot hub name} --set properties.enableFileUploadNotifications=true
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.maxDeliveryCount=10
az iot hub update --name {your iot hub name} --set properties.messagingEndpoints.fileNotifications.ttlAsIso8601=PT1H0M0S
```

<span data-ttu-id="f4038-149">Komutu aşağıdaki hello kullanarak, IOT hub'ına hello dosya karşıya yükleme yapılandırmasını gözden geçirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f4038-149">You can review hello file upload configuration on your IoT hub using hello following command:</span></span>

```azurecli
az iot hub show --name {your iot hub name}
```

## <a name="next-steps"></a><span data-ttu-id="f4038-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f4038-150">Next steps</span></span>

<span data-ttu-id="f4038-151">IOT hub'ı hello dosya karşıya yükleme özellikleri hakkında daha fazla bilgi için bkz: [karşıya bir aygıtı dosyalarından][lnk-upload].</span><span class="sxs-lookup"><span data-stu-id="f4038-151">For more information about hello file upload capabilities of IoT Hub, see [Upload files from a device][lnk-upload].</span></span>

<span data-ttu-id="f4038-152">Azure IOT hub'ı yönetme hakkında daha fazla bu bağlantılar toolearn izleyin:</span><span class="sxs-lookup"><span data-stu-id="f4038-152">Follow these links toolearn more about managing Azure IoT Hub:</span></span>

* <span data-ttu-id="f4038-153">[Toplu IOT cihazları yönetme][lnk-bulk]</span><span class="sxs-lookup"><span data-stu-id="f4038-153">[Bulk manage IoT devices][lnk-bulk]</span></span>
* <span data-ttu-id="f4038-154">[IOT hub'ı ölçümleri][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="f4038-154">[IoT Hub metrics][lnk-metrics]</span></span>
* <span data-ttu-id="f4038-155">[İzleme işlemleri][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="f4038-155">[Operations monitoring][lnk-monitor]</span></span>

<span data-ttu-id="f4038-156">toofurther IOT hub'ı hello özelliklerini keşfedin, bakın:</span><span class="sxs-lookup"><span data-stu-id="f4038-156">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="f4038-157">[IOT Hub Geliştirici Kılavuzu][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="f4038-157">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="f4038-158">[Bir cihaz IOT Edge benzetimini yapma][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="f4038-158">[Simulating a device with IoT Edge][lnk-iotedge]</span></span>
* <span data-ttu-id="f4038-159">[IOT çözümünüzden plan hello güvenli][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="f4038-159">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

[13]: ./media/iot-hub-configure-file-upload/file-upload-settings.png
[14]: ./media/iot-hub-configure-file-upload/file-upload-container-selection.png
[15]: ./media/iot-hub-configure-file-upload/file-upload-selected-container.png

[lnk-upload]: iot-hub-devguide-file-upload.md

[lnk-bulk]: iot-hub-bulk-identity-mgmt.md
[lnk-metrics]: iot-hub-metrics.md
[lnk-monitor]: iot-hub-operations-monitoring.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-securing]: iot-hub-security-ground-up.md


[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-CLI-install]: https://docs.microsoft.com/cli/azure/install-az-cli2
[lnk-login-command]: https://docs.microsoft.com/cli/azure/get-started-with-az-cli2
[lnk-az-account-command]: https://docs.microsoft.com/cli/azure/account
[lnk-az-register-command]: https://docs.microsoft.com/cli/azure/provider
[lnk-az-addcomponent-command]: https://docs.microsoft.com/cli/azure/component
[lnk-az-resource-command]: https://docs.microsoft.com/cli/azure/resource
[lnk-az-iot-command]: https://docs.microsoft.com/cli/azure/iot
[lnk-iot-pricing]: https://azure.microsoft.com/pricing/details/iot-hub/
[lnk-manage-storage]:../storage/common/storage-azure-cli.md#manage-storage-accounts
[lnk-portal-storage]:../storage/common/storage-create-storage-account.md
[lnk-cli-create-iothub]: https://docs.microsoft.com/cli/azure/iot/hub#create